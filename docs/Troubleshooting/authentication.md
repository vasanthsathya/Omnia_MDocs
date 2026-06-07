# Authentication Issues[¶](#authentication-issues "Permanent link")

Issues related to LDAP authentication, user login, the `omnia_auth` container, and TLS certificate errors.

## LDAP bind failures[¶](#ldap-bind-failures "Permanent link")

Symptom

LDAP client operations fail with bind errors:
 
 
```text title="LDAP bind error
ldap_bind: Invalid credentials (49)
```

Or Ansible playbooks fail when attempting to configure LDAP with authentication errors.

Cause

 * The LDAP admin bind DN or password is incorrect.
 * The LDAP server is not running.
 * TLS certificate verification fails, preventing the secure bind.

Resolution

 1. Verify the LDAP server is running:

```bash title="Run on: auth_server node
# If running as a container on the auth_server node
ssh <auth_server> podman ps | grep ldap
# or
ssh <auth_server> systemctl status slapd
```

 1. Test a manual bind:

```bash title="Run on: auth_server node
ldapsearch -x -H ldap://<auth_server>:389 \
-D "cn=admin,dc=example,dc=com" \
-W -b "dc=example,dc=com" "(objectClass=*)"
```

 1. Verify credentials in the Omnia vault:

```bash title="Run on: OIM host
ssh omnia_core
ansible-vault view /omnia/input/credentials.yml
```

Confirm the LDAP bind DN and password match what the LDAP server expects.

 1. If TLS is the issue, test without TLS first to isolate:

```bash title="Run on: auth_server node
ldapsearch -x -H ldap://<auth_server>:389 \
-D "cn=admin,dc=example,dc=com" -W -b "dc=example,dc=com"
```

Then test with TLS:
```bash title="Run on: auth_server node
ldapsearch -x -H ldaps://<auth_server>:636 \
-D "cn=admin,dc=example,dc=com" -W -b "dc=example,dc=com"
```

## User login fails on cluster nodes[¶](#user-login-fails-on-cluster-nodes "Permanent link")

Symptom

Users cannot log in to Slurm compute nodes or login nodes via SSH. Login attempts fail with:
```text title="SSH login error
Permission denied, please try again.
```

Even though the user exists in LDAP and can authenticate on the auth server directly.

Cause

 * The LDAP client (`sssd` or `nslcd`) is not running on the target node.
 * The LDAP client is configured with the wrong server URI or search base.
 * NSS (Name Service Switch) is not configured to use LDAP.
 * The user's home directory does not exist on the target node.

Resolution

 1. Check SSSD status on the target node:

```bash title="Run on: target node
ssh <node> systemctl status sssd
```

If not running:
```bash title="Run on: target node
ssh <node> systemctl start sssd
```

 1. Verify SSSD configuration:

```bash title="Run on: target node
ssh <node> cat /etc/sssd/sssd.conf | grep -E 'ldap_uri|ldap_search_base'
```

 1. Test user lookup via NSS:

```bash title="Run on: target node
ssh <node> getent passwd <username>
```

If the user does not appear, SSSD or NSS is misconfigured.

 1. Check if the home directory exists:

```bash title="Run on: target node
ssh <node> ls -la /home/<username>
```

If it does not exist, enable automatic home directory creation:
```bash title="Run on: target node
ssh <node> authconfig --enablemkhomedir --update
```

 1. Clear the SSSD cache and restart:

```bash title="Run on: target node
ssh <node> sss_cache -E
ssh <node> systemctl restart sssd
```

## `omnia_auth` container not starting[¶](#omnia_auth-container-not-starting "Permanent link")

Symptom

The `omnia_auth` container fails to start or repeatedly crashes. `podman ps -a` shows it in `Exited` state.

Cause

 * Port conflicts (another service is using ports 389 or 636).
 * Missing or corrupt TLS certificates.
 * Insufficient permissions on data volumes.
 * The container image is missing or corrupt.

Resolution

 1. Check container logs:

```bash title="Run on: OIM host
podman logs omnia_auth
```

 1. Check for port conflicts:

```bash title="Run on: OIM host
ss -tlnp | grep -E '389|636'
```

If another service is using the ports, stop it or reconfigure:
```bash title="Run on: OIM host
systemctl stop <conflicting_service>
```

 1. Verify TLS certificate files exist and are readable:

```bash title="Run on: OIM host
ls -la /etc/omnia/certs/ldap/
```

 1. Verify data directory permissions:

```bash title="Run on: OIM host
ls -la /var/lib/omnia/ldap/
```

 1. Re-pull the container image if it is corrupt:

```bash title="Run on: OIM host
podman pull <registry>/omnia_auth:<tag>
```

 1. Re-run the authentication playbook:

```bash title="Run on: OIM host
ssh omnia_core
cd /omnia
ansible-playbook playbooks/auth.yml
```

## Certificate errors[¶](#certificate-errors "Permanent link")

Symptom

LDAP or other services fail with TLS certificate errors:
```text title="TLS certificate error
TLS: peer cert untrusted or revoked
SSL routines:ssl3_get_server_certificate:certificate verify failed
```

Cause

 * The CA certificate used by step-ca is not installed on the client node.
 * The service certificate has expired.
 * The certificate's Subject Alternative Name (SAN) does not match the hostname or IP being used to connect.

Resolution

 1. Check the certificate expiry:

```bash title="Run on: OIM host
# Using openssl
openssl x509 -in /etc/step/certs/server.crt -noout -dates

# Using step-cli
step certificate inspect /etc/step/certs/server.crt --short
```

 1. If expired, renew the certificate:

```bash title="Run on: OIM host
step ca renew /etc/step/certs/server.crt /etc/step/certs/server.key
```

 1. Verify the CA certificate is installed on client nodes:

```bash title="Run on: client node
ssh <client_node> ls /etc/pki/ca-trust/source/anchors/
```

If the CA cert is missing, copy it and update the trust store:
```bash title="Run on: OIM host, then client node
scp /etc/step/certs/root_ca.crt <client_node>:/etc/pki/ca-trust/source/anchors/
ssh <client_node> update-ca-trust
```

 1. Verify the SAN matches the connection target:

```bash title="Run on: OIM host
openssl x509 -in /etc/step/certs/server.crt -noout -ext subjectAltName
```

If the SAN does not include the correct hostname or IP, reissue the certificate:
```bash title="Run on: OIM host
step ca certificate <hostname> /etc/step/certs/server.crt \
/etc/step/certs/server.key --san <hostname> --san <ip_address>
```

 1. Restart services after updating certificates:

```bash title="Run on: client node
systemctl restart sssd
podman restart omnia_auth
```

Info

 * [Setup Openldap](../HowTo/Authentication/setup_openldap.md) \-- OpenLDAP setup guide.
 * [Security Hardening](../Operations/security_hardening.md) \-- TLS and LDAP hardening.
 * [Security Hardening](../Operations/security_hardening.md) \-- Credential rotation procedures.
