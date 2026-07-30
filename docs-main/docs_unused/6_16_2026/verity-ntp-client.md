# Configure vNetC as an Authenticated NTP client

## Introduction

NTP, the Network Time Protocol, is used to keep system clocks synchronized within a few milliseconds of Coordinated Universal Time (UTC). On our systems this is important because it ensures certificate expiration times are handled accurately, and because it means we can merge log files from multiple systems so cross-system events can be tracked.

From a security perspective, NTP can operate in three modes:

1. Unauthenticated
1. Authenticated via a shared key
1. Authenticated via PKI (using a variant of NTP called NTS)

Note that the client authenticates the server because the client needs to trust the time sent to it. Generally, the server does not care about which clients are connecting, and if it does care, this would typically be handled by limiting network access to the server.

We're concerned here with the second style as this is the only one that is both required and supported in the JITC lab. However, this configuration is not limited to lockdown systems. Any customer may want to use authenticated NTP with servers they manage.

When first installed, the vNetC is configured to use unauthenticated NTP with the "Frankenbox" host as well as a public pool of NTP servers. If there is no "Frankenbox" host, that server entry just never synchronizes, so time is maintained via the public servers.

### STEP 1: NTP Key File

With shared-key authentication, the servers and the clients must all have a key in common, though it is not necessary for all servers and all clients to have the same keys.

One easy way to handle this is to get a copy the server key file, or you can construct the file by hand. The file should be placed in /var/ns/etc/ntp.keys, and should look like this:



    # ntpkey_MD5key_ivn-ext2.dev.ipho.lan.3898159044

    # Wed Jul 12 08:57:24 2023

    # Sample keys only!  
    # Your keys will be provided by your NTP server administrator  
    #  
    1 MD5 L";Nw\<\*.I\<{4U0)247"i \# MD5 key  
    2 MD5 &\>10%XXK90'51VwV\<xq\~ \# MD5 key  
    3 MD5 1b4zLW\~d\^!K:]RsD'qb6 \# MD5 key  
    4 SHA1 a27872d3030a902568446c751b4551a7629af65c \# SHA1 key  
    5 SHA1 21bc3b4865dbb9e920902abdccb3e04ff97a5e74 \# SHAl key  
    6 SHA1 267736fe24fef5ba85ae11594132ab5d6f6daba9 \# SHA1 key


Note that some organizations may issue an individual key for each client network. That way they are not releasing keys broadly, which if stolen could be used to spoof a large number of networks. In that case, manual editing will be required.

However constructed, the key index (1 thru 6 above) must be consistent between a server and a client.

### STEP 2: NTP Local Configuration File

Now we create the local configuration to associate the vNetC NTP client with each server, and with the shared key for that server. This file should be created as /var/ns/etc/ntp-local.conf.

This file should be based on this:



    server 192.168.0.41 iburst key 1

    server 192.168.0.42 iburst key 2

    keys /var/ns/etc/ntp.keys

    trustedkey 1 2

    # This provides fallback high-stratum time based on the

    # hardware clock when upstream servers are inaccessible.

    #

    server 127.127.1.1

    fudge 127.127.1.1 stratum 10


The server lines will have the address of each server listed. The address can be either an IP address or a fully qualified domain name. The advantage of using an IP address is that DNS does not have to be functional for time synchronization to occur. The disadvantage is that if the server addresses ever change, each system will have to be updated.

The "key" in the server line indicates which key should be used to authenticate the server. The keys can be the same as long as the corresponding server has that key configured with that index.

The "trustedkey" line should list all the keys used in the server lines.

The "server 127.127.1.1" section is optional. This causes NTP on the vNetC to use its local clock when acting as a server and no upstream servers can be reached. The effect is that downstream clients will stay synchronized with the vNetC even though the time they receive is not fully synchronized with Coordinated Universal Time.

### STEP 3: Apply New Configuration

On the vNetC, the NTP configuration file is /etc/ntp.conf and initially looks like this:


    #

    # See ntp-lead-servers.conf for information about

    # changing default servers.

    #

    includefile /usr/ns/etc/ntp-lead-head.conf

    includefile /usr/ns/etc/ntp-lead-servers.conf

    #includefile /var/ns/etc/ntp-local.conf



To apply the configuration built in steps 1 and 2, simply change this file to point to the new configuration by commenting out the `ntp-lead-servers.conf` line and uncommenting the `ntp-local.conf` line, so the file would now look like this:

    #

    # See ntp-lead-servers.conf for information about

    # changing default servers.

    #

    includefile /usr/ns/etc/ntp-lead-head.conf

    #includefile /usr/ns/etc/ntp-lead-servers.conf

    includefile /var/ns/etc/ntp-local.conf

The ntp daemon will be automatically restarted when this file is changed.

#### STEP 4: Verify the New Configuration

It may take up to several minutes for the new configuration to complete synchronization but typically it only takes a few seconds. Use the command `ntpq -p`, to check synchronization. The output should look like this:


    | remote        | refid         | st | t | when | poll | reach | delay | offset | jitter |
    |---------------|---------------|----|---|------|------|-------|-------|--------|--------|
    | *192.168.0.41 | 166.129.200.1 | 4  | u | 324  | 1024 | 377   | 3.247 | -1.121 | 1.955  |
    | +192.168.0.41 | 144.90.5.123  | 3  | u | 589  | 1024 | 377   | 2.503 | -0.820 | 1.581  |
    | LOCAL(1)      | .LOCL.        | 10 | l | -    | 64   | 0     | 0.000 | 0.000  | 0.000  |


The "\*" in the first column indicates this server has been selected for synchronization. The "+" indicates this server is a candidate for synchronization if the first server becomes inaccessible or loses synchronization quality.

The "refid" column indicates the source of the server's time, which is often its upstream server's IP address.

The LOCAL(1) refers to the optional "server 127.127.1.1" entry. Because this server has been forced to "stratum 10" (ten hops from a primary time source), its clock is not considered even to be a candidate for synchronization. That will only change if all the other high-quality servers become inaccessible.

## Troubleshooting

If `ntpq -p`does not show server synchronization after a few minutes, the most common issues encountered are:

1. The server hostname is not resolving. You can use an IP address in the configuration to check this and return to using a hostname once the DNS issue has been corrected.
1. The server key is not consistent with the client key configuration.
1. The NTP protocol (UDP port 123) is blocked between the vNetC and the servers.

There is no explicit indication about the cause of synchronization problems. In all the cases above, the "refid" in the `ntpq -p` output will be shown as `.INIT`.
