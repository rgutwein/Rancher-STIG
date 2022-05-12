# Rancher-STIG
Simple guide for navigating the rke2 2.6 STIG from DISA. 
You can download the STIG itself from https://public.cyber.mil/stigs/downloads/
# V-252843 - CAT I - Rancher MCM must use a centralized user management solution to support account management functions. For accounts using password authentication, the container platform must use FIPS-validated SHA-2 or later protocol to protect the integrity of the password authentication process.
Fix Text: This STIG is written and tested with KeyCloak and not included with Rancher MCM. Installation instructions for KeyCloak can be found here:
https://www.keycloak.org/getting-started/getting-started-kube

NIST 800-53r4 References:

```bash
AC-2.b; AC-2(1); AC-2(2); AC-2(4); AC-3; AC-4; AC-4(17); AC-7.a; AU-3; AU-6(4); AU-9; AU-9(3); AU-12(3); CM-5(6); CM-8.b; CM-8(3)(b);
CM-10(1); IA-2; IA-2(1); IA-2(2); IA-4.e; IA-5(1)(a); IA-5(1)(b); IA-5(1)(c); IA-5(1)(d); IA-5(1)(e); IA-5(2)(c); IA-6; SC-4
```
# V-252849 - CAT I - Prohibit or restrict the use of protocols

This control is for limiting the ports that are allowed for ingress to the Rancher UI/API.

Fix Text: Navigate to Triple Bar Symbol >> Explore Cluster >> local
From the kubectl shell (>_) execute the following:

```bash
kubectl patch -n cattle-system service rancher -p '{"spec":{"ports":[{"port":443,"targetPort":443}]}}'

# change the hostname to match your ingress URL.
export RANCHER_HOSTNAME=rancher.rfed.io

kubectl -n cattle-system patch ingress rancher -p "{\"metadata\":{\"annotations\":{\"nginx.ingress.Kubernetes.io/backend-protocol\":\"HTTPS\"}},\"spec\":{\"rules\":[{\"host\":\"$RANCHER_HOSTNAME\",\"http\":{\"paths\":[{\"backend\":{\"service\":{\"name\":\"rancher\",\"port\":{\"number\":443}}},\"pathType\":\"ImplementationSpecific\"}]}}]}}"

kubectl patch -n cattle-system service rancher --type=json -p '[{"op":"remove","path":"/spec/ports/0"}]'
```
NIST 800-53r4 References:

```bash
CM-7.b
```

# V-252844 - CAT II - Generate audit records for all DoD-defined auditable events within all components in the platform.
Fix Text: Ensure audit logging is enabled:

- Navigate to Triple Bar Symbol >> Explore Cluster >> local
- In the top Select ALL Namespaces from the drop down that currently says "Only User Namespaces".
- Click "deployments" under Workload menu item.
- Select "rancher" in the Deployments section under the 'cattle-system' namespace.
- Click the three dot config menu on the right.
- Choose "Edit Config".
- Scroll down to the "Environment Variables" section.
- Change the AUDIT_LEVEL value to "2" or "3" and then click "Save".

If the variable does not exist:

- Click "Add Variable".
- Keep Default key/Value Pair as "Type"
- Add "AUDIT_LEVEL" as Variable Name.
- Input "2,3" for a value.
- Click "Save".

A better option is to update Helm. Here is a best way to update the audit log level. Using Helm we can set a few things like the initial bootstrap password and number of replicas. Notice the `auditlog` settings.
```bash
helm upgrade -i rancher rancher-latest/rancher --create-namespace --namespace cattle-system --set hostname=rancher.$domain --set bootstrapPassword=bootStrapAllTheThings --set replicas=1 --set auditLog.level=2 --set auditLog.destination=hostPath
```

NIST 800-53r4 References:

```bash
AC-2(4); AC-3; AC-4(15); AU-3; AU-5.b; AU-5(3); AU-5(4); AU-12.a; AU-12.b; AU-12.c; AU-14(1); CM-1.a.1
```

# V-252845 - CAT II - The default role needs to be changed to allow least privilege access.

Allowed by the central authentication system, the default role assigned to a user must be User-Base

Fix Text: From the GUI, navigate to Triple Bar Symbol >> Users & Authentication. In the left navigation menu, click "Roles".

- Click "Standard User".
- At the top right, click the three dots, and then "Edit Config".
- Under "New User Default", select "No" and click "Save".
- Click "User-Base".
- At the top right, click the three dots, and then click "Edit Config".
- Under "New User Default", select "Yes", and then click "Save".

NIST 800-53r4 References:

```bash
AC-2(4)
```

# V-252846 - CAT II - Allocate Audit Record Storage | Log Aggregation

Allocate audit record storage and generate audit records associated with events, users, and groups.

Fix Text: Enable log aggregation:
Navigate to Triple Bar Symbol.

For each cluster in  "EXPLORE CLUSTER":

- Select "Cluster".
- Select "Cluster Tools" (bottom left).
- In the "Logging Block", select "Install".
- Select the newest version of logging in the dropdown. 
- Open the "Install into Project Dropdown".
- Select the Project. (Note: Kubernetes STIG requires creating new project & namespace for deployments. Using Default or System is not best practice.)
- Click "Next".
- Review the options and click "Install".

NIST 800-53r4 References:

```bash
AU-3; AU-3(1); AU-3(2); AU-9 (3); AU-12.c; CM-1.a.2; CM-3.d; CM-5(5) (b);CM-6.b
```

# V-252847 - CAT II - Never automatically remove or disable emergency accounts

Emergency accounts are administrator accounts that are established in response to crisis situations where the need for rapid account activation is required. Therefore, emergency account activation may bypass normal account authorization processes. If these accounts are automatically disabled, system maintenance during emergencies may not be possible, thus adversely affecting system availability.

Fix Text: Ensure local emergency admin account has not been removed and is the only Local account.

Navigate to the Triple Bar Symbol >> Users & Authentication. In the left navigation menu, click "Users".
To Create a User:

- Click "Create".
- Complete the "Add User" form. Ensure Global Permissions are set to "Administrator".
- Click "Create".

To Delete a User:

- Select the user and click "Delete".

NIST 800-53r4 References:

```bash
AC-2(2)
```

# V-252848 - CAT II - Enforce organization-defined circumstances and/or usage conditions for organization-defined accounts.

Must verify the certificate used for Rancher's ingress is a valid DoD certificate. This is achieved by verifying the helm installation contains correct parameters.

Fix Text: Update the secrets to contain valid certificates.

Put the correct and valid DOD certificate and key in files called "tls.crt" and "tls.key", respectively, and then run:
`kubectl -n cattle-system create secret tls tls-rancher-ingress  --cert=tls.crt   --key=tls.key`

Upload the CA required for the certs by creating another file called "cacerts.pem" and running:
`kubectl -n cattle-system create secret generic tls-ca \   --from-file=cacerts.pem=./cacerts.pem`

The helm chart values need to be updated to include the check section:
privateCA: true
ingress:
tls:
ce: secret

Re-run helm upgrade with the new values for the certs to take effect.

NIST 800-53r4 References:

```bash
AC-2.d
```
