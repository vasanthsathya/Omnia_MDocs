# System Security
System security is expressed in these three categories: 
•	User Security (Protection of users)
•	Device Security (Protection of devices)
•	Client System Security (Protection of the system as a client)


After install, the initial state of the vNetC contains two certificates.
•	A self-signed server certificate that allows web connections. Web browsers will prompt the user for a real certificate until replaced.
•	The internally generated certificate authority and its certificate chains.


## User Security

Verity employs a combination of conventional login/password authentication, authorization and certificate issuance/revocation to protect users.

-   **Login / Passwords**: Traditional method of user authentication using a username and password
-   **User Certificates**: Secure user authentication using certificates that can be integrated into Chrome or issued through CAC (Common Access Card) cards.
-   **Revocation List**: A detailed process for invalidating certificates when necessary.
-   

### Login / Passwords

Upon opening the Verity landing page, an authentication call-to-action is presented as the entry point to the application’s UI.

![](media/72c50ba61314d5e008bc12dca3820c96.png)

!!!NOTE
     The system can be configured to authenticate locally or using a Radius server.

### User Permissions

**User Permissions** allows the granting or restricting of feature access to selected user roles. Roles are presented as column headings, and the assigned features can be enabled or disabled by clicking the checkbox of the desired feature in each row. Feature descriptions are listed to the left of the page vertically.

To access this section, go to **LAN /Administration / Permissions**

![](media/718b44051f232659009546e6d01bd705.png)

### Accounts

**User Accounts** lets you set the user’s access level, add/remove new users, and change their passwords.

To access this feature, go to **Installation Admin** / **Users** / **Accounts**.

![](media/8f70f4abff07b57a1f5df16f760b050f.png)

### SSH Access

**SSH Access** is where SSL certificates are uploaded to grant select users SSH access to the system. Users with the relevant certificate credentials are listed here.

To access this section, go to **Installation Admin** / **Users** / **SSH Keys**.

![](media/radius_log_ins_6_3.png)

## Radius Logins

**Radius Logins** is where RADIUS server configurations are performed. If a RADIUS server is configured, it is used for authentication and authorization by default. Multiple RADIUS servers can be used for redundancy purposes.

Radius settings are available in **Installation** **Admin** / **Users** / **Radius Logins**.

![](media/radius_log_ins_6_3.png)

For more information on Radius Logins view the Radius content under the section titled [](../system-security/#radius-client-certificate).

## Certificate Revocation Management

Certificate Revocation Management is used to revoke certificates prior to their validity date.

The revocation list should be in PEM format and contain a list of “X509 CRL” entries that revoke client certificates that are no longer valid for use by web browsers or devices. The file will also be delivered to the ACS. The Certificate Revocation Management is not used on systems that are not in secure lockdown.

To access this section, go to **Installation Admin**/**Certificate Management**/ **Certificate Revocation Management**

![](media/4601eea3dd835313312899c232aaa799.png)

## Limits

**Limit** sets the maximum number of users for Admin, Read-Write and Read-Only permission categories.

To access this section, go to **Installation Admin** / **Users** / **Limits**

![](media/2899ba1a56ee2f95fe8017a74ecb0a46.png)

### Certificate Chains

Certificate Chains are used to authenticate user client certificates (e.g., CAC) and device client certificates.

!!!info 
    For systems in secure lockdown, all the root certificate chains needed to authenticate user client certificates (e.g., CAC) and device client certificates must be uploaded. Multiple files can be uploaded and will be used when validating all TLS client connections (users or devices). A merged set of all certificate chains is also delivered to the ACS. Certificate chains are not used on systems that are not in secure lockdown.

To access this section, go to **Installation Admin** / **Certificate Management**/ **Certificate Chains**

![](media/8518d0b555233e3a8e2a70d696238ac8.png)


## Device Security

The system's security for devices is established from the initial installation phase. By default, the system is placed in a high-security, locked-down state. This isolation prevents any devices from contacting the ACS or vNetC, ensuring that no unauthorized or potentially harmful connections are made during the setup phase.

!!!warning
    Only secured devices are allowed to connect to the system

### Onboarding Mode

!!! INFO
    This section describes how to perform certificate issuance using Onboarding Mode. Onboarding mode is not required, and devices can be loaded with certificates locally

Administrators use **Onboarding Mode** to integrate new devices, temporarily relaxing security settings for a predefined period. This controlled time window allows the automatic issuance of security certificates to connected devices.

In environments where new devices are being added to an already-configured system, the security measures ensure that devices with existing valid certificates continue to operate without disruption. Once **Onboarding Mode** expires, the system reverts to its stringent security state, allowing only devices with valid certificates to connect. Devices without valid certificates or with invalid ones are automatically rejected, maintaining a secure network environment.

For device safety, all devices must be in a clean factory reset condition before connecting to the system, ensuring no pre-existing configurations or potential vulnerabilities are present.

!!!WARNING
      All devices must be in a clean factory reset condition before connecting to the system

### Enable Onboarding Mode

To use **Onboarding Mode,** click the **Topology** icon and select the tab titled **VNFs**.

![](media/a7ffa5956fcbcb5c1c62f648e4996138.png)

Zoom into the **vNetC Commander** tile and scroll all the way to the right until you see the **Lock** icon.

![](media/481e9a8e0f2407db438584882e808292.png)

![](media/603443f65a4304bb1939c6c8ac2bffa2.png)![](media/4fd2689e6ed9ae6e016f8eb80f46777e.png)

To enable **Onboarding Mode**, click the Lock icon and place it in the *unlocked* state.

![](media/681de3fbd8099a66239f426ee93883a6.png)

A dialog box appears asking how long the onboarding should last. What you choose determines how long the **Onboarding Mode** is enabled for.

![](media/acd9d49bfb912d3b12f6cb0fede5accc.png)



### Terminating Onboarding Mode

If you click the unlock (![](media/681de3fbd8099a66239f426ee93883a6.png)) icon prior to the **onboarding session** expiration, you are provided with a message asking if you want to preemptively end the session.

![](media/1f52e2e52c3717dfeb8c105fb4518bfa.png)





## Client System Security

The following outlines the processes and procedures required to safeguard the vNetc from security threats when it is a client of other devices.

### Certificate Management

All tiles referenced in this section are opened from **Installation Admin**

![](media/1ff876bf24516d7caad5cff7a15f9eac.png)

### vNetC Web-Server Certificates

The vNetC requires a web server certificate. This certificate provides TLS validation ensuring secure communication when web browsers and devices contact the vNETC. The certificate must fit one of two criteria.

1.  The certificate contains the private key, has FQDN set as the common-name, and a certificate authority chain.
2.  The certificate contains the private key, a certificate with a "wildcard" common-name, and a certificate authority chain. The "wildcard" would be of the form: \***.dept.branch.mil**

The certificate is uploaded to the **vNETC Server Certificate** panel shown below.

![](media/fa1a72ec65ed0fc5e80176eb4d2351d2.png)

### vNETC Server Certificate Panel

![](media/7d00e9895ef3be4dabd0538a29a6fe7b.png)

![](media/8051fda0b341b8cf7135b664a07758eb.png)



### Certificate Authority Chains

The vNETC must be loaded with certificate authority chains composed of intermediate and root certificates. For systems in secure lockdown, all **Root Certificate Chains** are used to validate client certificates (such as CAC) and device client certificates. All such certificate chains should be uploaded to the **Root Certificate Chains** panel (as shown below). Multiple files can be uploaded and are used when validating all TLS client connections (users or devices).

### Root Certificate Chains

![](media/c87dc0883a2f5a74e6b52ba29a7b5f8a.png)

![](media/e5c87aa12f2e39e1322092b6450760ae.png) 




### RADIUS Client Certificate

The Radius client certificate authenticates the vNetC with the RADIUS authentication server(s). The RADIUS authentication server is configured under the **User** panel as shown in the following diagram.

![](media/6bda36abaf3963756d3ae3cd1430929f.png)

![](media/37e9b814b3c32db70b5790953b459ca0.png)





The vNetC must have a client certificate file containing the private key and a certificate signed by an authority recognized by the RADIUS server. The certificate is required for systems in secure lockdown, and until it is loaded, only the emergency admin user will have access to the system. For other systems, the certificate is used if provided.

The RADIUS client certificate is uploaded using the panel shown below.

![](media/7624b4ff3e51be5650711537a80318b9.png)


### SNMP
todo
### DB Backups
todo
### SYSLOG
todo

### Revocation List

The **Certificate Revocation List** contains a list of "X509 CRL" entries that revoke client certificates that are no longer valid for use by web browsers or devices.

#### Certificate Revocation List

![](media/d9c35ac58de364e697fd738e082a33a3.png)

![](media/8ff3b288558f43bc88c15802cff1825b.png)



![](media/796dec2b7139056af88cf91448536ee0.png)


## Transitioning the vNetC to Secure Lockdown Mode

Once the system is configured with the required certificates you perform the following actions.

-   Login as Root user with root password vis SSH
-   Run the following command: **ns_vnc_setup --features [ASK ANDY ......... jitc_mode]=1.**
-   When the vNETC becomes accessible, you are required to provide a PIN for CAC based authentication before being able to access the login page. Complete the PIN submission action.
-   If you are then able to access the login page and login in, the vNETC is secure and can be made accessible from the production network.

**When in Lockdown Mode**

-   A client certificate from an approved authority is required.
-   The emergency username is always "admin”, and its password is set during system installation.
-   If no RADIUS servers are enabled, or none can be reached, only the emergency user will have access.
-   If any  RADIUS servers are accessible, the emergency user will not have access \_unless\_ the RADIUS server gives authorization.
-   All other users must be authorized via the RADIUS server(s).
-   The three-login failure limit leads to a 15 min cooling-off period.s
