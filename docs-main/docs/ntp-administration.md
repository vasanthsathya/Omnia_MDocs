# NTP Administration

## Introduction

NTP (Network Time Protocol) keeps system clocks synchronized within a few milliseconds of Coordinated Universal Time (UTC). This ensures certificate expiration times are handled accurately as well as viewing unified system logs.

NTP can operate in one of three modes:

1. Unauthenticated
2. Authenticated via a shared key
3. Authenticated via PKI (using a variant of NTP called NTS)

Out of the box, the vNetC uses unauthenticated NTP with the "Frankenbox" host and a public pool of NTP servers. If no "Frankenbox" host is present, that server entry never synchronizes, and the public servers maintain the time instead.

---
## Configure a Local Unauthenticated NTP

Use this when the vNetC has no internet access and your NTP server does not require authentication.

1. Copy `/usr/ns/etc/ntp-lead-servers.conf` to `/var/ns/etc/ntp-local.conf`
1. Edit `/var/ns/etc/ntp-local.conf` to add or remove NTP servers
1. Edit `/etc/ntp.conf` to uncomment the line that references `ntp-local.conf` and comment out the `ntp-lead-servers.conf` line
1. Run `service ntpd onerestart` (an error message saying `WARNING: failed to start ntpd` can be ignored)
1. Verify with `ntpq -p` that your server appears in the output

---
## Configure Authenticated NTP (Shared Key)

Use this when your environment requires that the vNetC authenticate its time sources — for example, in JITC-compliant or air-gapped deployments. Your NTP server administrator will need to provide the shared keys.

### Step 1: Create the Key File

With shared-key authentication, the servers and the clients must all have a key in common, though it is not necessary for all servers and all clients to have the same keys.

One easy way to handle this is to get a copy of the server key file, or you can construct the file by hand. The file should be placed at `/var/ns/etc/ntp.keys` and should look like this:
```
# ntpkey_MD5key_ivn-ext2.dev.ipho.lan.3898159044

# Wed Jul 12 08:57:24 2023

# Sample keys only!
# Your keys will be provided by your NTP server administrator
#
1 MD5 L";Nw<*.I<{4U0)247"i  # MD5 key
2 MD5 &>10%XXK90'51VwV<xq~  # MD5 key
3 MD5 1b4zLW~d^!K:]RsD'qb6  # MD5 key
4 SHA1 a27872d3030a902568446c751b4551a7629af65c  # SHA1 key
5 SHA1 21bc3b4865dbb9e920902abdccb3e04ff97a5e74  # SHA1 key
6 SHA1 267736fe24fef5ba85ae11594132ab5d6f6daba9  # SHA1 key
```

The key index numbers (1 through 6 above) must match between the server and client configurations. Some organizations issue per-network keys to limit exposure — if that is the case, you will need to edit the file manually rather than copying it directly from the server.

### Step 2: Create the Local Configuration File

Create `/var/ns/etc/ntp-local.conf` with the following structure:

```
server 192.168.0.41 iburst key 1
server 192.168.0.42 iburst key 2

keys /var/ns/etc/ntp.keys
trustedkey 1 2

# Optional: fall back to local hardware clock if all upstream servers are unreachable
server 127.127.1.1
fudge 127.127.1.1 stratum 10
```

Replace the IP addresses with your actual NTP server addresses. Using IP addresses rather than hostnames means time synchronization will still work if DNS is unavailable. The `key` value on each server line must match the index for that server in your key file. The `trustedkey` line must list every key index referenced in the server lines.

The `server 127.127.1.1` block is optional. It causes the vNetC to fall back to its local hardware clock if all upstream servers become unreachable, so that any downstream clients remain synchronized even if the time is no longer UTC-accurate.

### Step 3: Apply the Configuration

Edit `/etc/ntp.conf` to comment out the default servers line and uncomment the local config line:

```
includefile /usr/ns/etc/ntp-lead-head.conf
#includefile /usr/ns/etc/ntp-lead-servers.conf
includefile /var/ns/etc/ntp-local.conf
```

The NTP daemon restarts automatically when this file is saved.

### Step 4: Verify Synchronization

Run `ntpq -p` after a few seconds (allow up to a few minutes). A healthy output looks like this:

| remote | refid | st | t | when | poll | reach | delay | offset | jitter |
|---|---|---|---|---|---|---|---|---|---|
| \*192.168.0.41 | 166.129.200.1 | 4 | u | 324 | 1024 | 377 | 3.247 | -1.121 | 1.955 |
| +192.168.0.42 | 144.90.5.123 | 3 | u | 589 | 1024 | 377 | 2.503 | -0.820 | 1.581 |
| LOCAL(0) | .LOCL. | 10 | l | - | 64 | 0 | 0.000 | 0.000 | 0.000 |

A `*` in the first column means that server is actively selected for synchronization. A `+` means it is a candidate if the primary becomes unavailable. `LOCAL(0)` reflects the optional hardware clock fallback — because it is forced to stratum 10, it will only be used if all other servers become unreachable.

### Troubleshooting

If `ntpq -p` shows `.INIT` in the `refid` column after several minutes, the most common causes are:

- The server hostname is not resolving — try using an IP address to rule out DNS issues
- The key on the client does not match the key configured on the server
- UDP port 123 is blocked between the vNetC and the NTP server
