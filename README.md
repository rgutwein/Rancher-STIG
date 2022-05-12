# Rancher-STIG
Simple guide for navigating the rke2 2.6 STIG from DISA. 
You can download the STIG itself from https://public.cyber.mil/stigs/downloads/
# V-252843 - Rancher MCM must use a centralized user management solution to support account management functions. For accounts using password authentication, the container platform must use FIPS-validated SHA-2 or later protocol to protect the integrity of the password authentication process.
  This STIG is written and tested with KeyCloak and not included with Rancher MCM. Installation instructions for KeyCloak can be found here:
https://www.keycloak.org/getting-started/getting-started-kube
