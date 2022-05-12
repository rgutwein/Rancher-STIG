# Rancher-STIG
Simple guide for navigating the rke2 2.6 STIG from DISA. 
You can download the STIG itself from https://public.cyber.mil/stigs/downloads/
# V-252843 - Rancher MCM must use a centralized user management solution to support account management functions. For accounts using password authentication, the container platform must use FIPS-validated SHA-2 or later protocol to protect the integrity of the password authentication process.
  This STIG is written and tested with KeyCloak and not included with Rancher MCM. Installation instructions for KeyCloak can be found here:
https://www.keycloak.org/getting-started/getting-started-kube
  Mapped CCIs: 
  CCI-000015
The organization employs automated mechanisms to support the information system account management functions.
NIST SP 800-53 :: AC-2 (1)
NIST SP 800-53A :: AC-2 (1).1
NIST SP 800-53 Revision 4 :: AC-2 (1)

CCI-000016
The information system automatically removes or disables temporary accounts after an organization-defined time period for each type of account.
NIST SP 800-53 :: AC-2 (2)
NIST SP 800-53A :: AC-2 (2).1 (ii)
NIST SP 800-53 Revision 4 :: AC-2 (2)

CCI-000044
The information system enforces the organization-defined limit of consecutive invalid logon attempts by a user during the organization-defined time period.
NIST SP 800-53 :: AC-7 a
NIST SP 800-53A :: AC-7.1 (ii)
NIST SP 800-53 Revision 4 :: AC-7 a

CCI-000134
The information system generates audit records containing information that establishes the outcome of the event.
NIST SP 800-53 :: AU-3
NIST SP 800-53A :: AU-3.1
NIST SP 800-53 Revision 4 :: AU-3

CCI-000154
The information system provides the capability to centrally review and analyze audit records from multiple components within the system.
NIST SP 800-53 :: AU-6 (4)
NIST SP 800-53A :: AU-6 (4).1
NIST SP 800-53 Revision 4 :: AU-6 (4)

CCI-000162
The information system protects audit information from unauthorized access.
NIST SP 800-53 :: AU-9
NIST SP 800-53A :: AU-9.1
NIST SP 800-53 Revision 4 :: AU-9

CCI-000163
The information system protects audit information from unauthorized modification.
NIST SP 800-53 :: AU-9
NIST SP 800-53A :: AU-9.1
NIST SP 800-53 Revision 4 :: AU-9

CCI-000164
The information system protects audit information from unauthorized deletion.
NIST SP 800-53 :: AU-9
NIST SP 800-53A :: AU-9.1
NIST SP 800-53 Revision 4 :: AU-9

CCI-000187
The information system, for PKI-based authentication, maps the authenticated identity to the account of the individual or group.
NIST SP 800-53 :: IA-5 (2)
NIST SP 800-53A :: IA-5 (2).1
NIST SP 800-53 Revision 4 :: IA-5 (2) (c)

CCI-000192
The information system enforces password complexity by the minimum number of upper case characters used.
NIST SP 800-53 :: IA-5 (1) (a)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (a)

CCI-000193
The information system enforces password complexity by the minimum number of lower case characters used.
NIST SP 800-53 :: IA-5 (1) (a)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (a)

CCI-000194
The information system enforces password complexity by the minimum number of numeric characters used.
NIST SP 800-53 :: IA-5 (1) (a)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (a)

CCI-000195
The information system, for password-based authentication, when new passwords are created, enforces that at least an organization-defined number of characters are changed.
NIST SP 800-53 :: IA-5 (1) (b)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (b)

CCI-000196
The information system, for password-based authentication, stores only encrypted representations of passwords.
NIST SP 800-53 :: IA-5 (1) (c)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (c)

CCI-000197
The information system, for password-based authentication, transmits only encrypted representations of passwords.
NIST SP 800-53 :: IA-5 (1) (c)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (c)

CCI-000198
The information system enforces minimum password lifetime restrictions.
NIST SP 800-53 :: IA-5 (1) (d)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (d)

CCI-000199
The information system enforces maximum password lifetime restrictions.
NIST SP 800-53 :: IA-5 (1) (d)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (d)

CCI-000200
The information system prohibits password reuse for the organization defined number of generations.
NIST SP 800-53 :: IA-5 (1) (e)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (e)

CCI-000205
The information system enforces minimum password length.
NIST SP 800-53 :: IA-5 (1) (a)
NIST SP 800-53A :: IA-5 (1).1 (i)
NIST SP 800-53 Revision 4 :: IA-5 (1) (a)

CCI-000206
The information system obscures feedback of authentication information during the authentication process to protect the information from possible exploitation/use by unauthorized individuals.
NIST SP 800-53 :: IA-6
NIST SP 800-53A :: IA-6.1
NIST SP 800-53 Revision 4 :: IA-6

CCI-000213
The information system enforces approved authorizations for logical access to information and system resources in accordance with applicable access control policies.
NIST SP 800-53 :: AC-3
NIST SP 800-53A :: AC-3.1
NIST SP 800-53 Revision 4 :: AC-3

CCI-000764
The information system uniquely identifies and authenticates organizational users (or processes acting on behalf of organizational users).
NIST SP 800-53 :: IA-2
NIST SP 800-53A :: IA-2.1
NIST SP 800-53 Revision 4 :: IA-2

CCI-000765
The information system implements multifactor authentication for network access to privileged accounts.
NIST SP 800-53 :: IA-2 (1)
NIST SP 800-53A :: IA-2 (1).1
NIST SP 800-53 Revision 4 :: IA-2 (1)

CCI-000766
The information system implements multifactor authentication for network access to non-privileged accounts.
NIST SP 800-53 :: IA-2 (2)
NIST SP 800-53A :: IA-2 (2).1
NIST SP 800-53 Revision 4 :: IA-2 (2)

CCI-000795
The organization manages information system identifiers by disabling the identifier after an organization defined time period of inactivity.
NIST SP 800-53 :: IA-4 e
NIST SP 800-53A :: IA-4.1 (iii)
NIST SP 800-53 Revision 4 :: IA-4 e

CCI-001090
The information system prevents unauthorized and unintended information transfer via shared system resources.
NIST SP 800-53 :: SC-4
NIST SP 800-53A :: SC-4.1
NIST SP 800-53 Revision 4 :: SC-4

CCI-001350
The information system implements cryptographic mechanisms to protect the integrity of audit information.
NIST SP 800-53 :: AU-9 (3)
NIST SP 800-53A :: AU-9 (3).1
NIST SP 800-53 Revision 4 :: AU-9 (3)

CCI-001368
The information system enforces approved authorizations for controlling the flow of information within the system based on organization-defined information flow control policies.
NIST SP 800-53 :: AC-4
NIST SP 800-53A :: AC-4.1 (iii)
NIST SP 800-53 Revision 4 :: AC-4

CCI-001403
The information system automatically audits account modification actions.
NIST SP 800-53 :: AC-2 (4)
NIST SP 800-53A :: AC-2 (4).1 (i&ii)
NIST SP 800-53 Revision 4 :: AC-2 (4)

CCI-001493
The information system protects audit tools from unauthorized access.
NIST SP 800-53 :: AU-9
NIST SP 800-53A :: AU-9.1
NIST SP 800-53 Revision 4 :: AU-9

CCI-001494
The information system protects audit tools from unauthorized modification.
NIST SP 800-53 :: AU-9
NIST SP 800-53A :: AU-9.1
NIST SP 800-53 Revision 4 :: AU-9

CCI-001495
The information system protects audit tools from unauthorized deletion.
NIST SP 800-53 :: AU-9
NIST SP 800-53A :: AU-9.1
NIST SP 800-53 Revision 4 :: AU-9

CCI-001499
The organization limits privileges to change software resident within software libraries.
NIST SP 800-53 :: CM-5 (6)
NIST SP 800-53A :: CM-5 (6).1
NIST SP 800-53 Revision 4 :: CM-5 (6)

CCI-001619
The information system enforces password complexity by the minimum number of special characters used.
NIST SP 800-53 :: IA-5 (1) (a)
NIST SP 800-53A :: IA-5 (1).1 (v)
NIST SP 800-53 Revision 4 :: IA-5 (1) (a)

CCI-001734
The organization defines the restrictions to be followed on the use of open source software.
NIST SP 800-53 Revision 4 :: CM-10 (1)

CCI-001782
The organization updates the information system component inventory per organization-defined frequency.
NIST SP 800-53 Revision 4 :: CM-8 b

CCI-001783
The organization defines the personnel or roles to be notified when unauthorized hardware, software, and firmware components are detected within the information system.
NIST SP 800-53 Revision 4 :: CM-8 (3) (b)

CCI-001784
When unauthorized hardware, software, and firmware components are detected within the information system, the organization takes action to disable network access by such components, isolates the components, and/or notifies organization-defined personnel or roles.
NIST SP 800-53 Revision 4 :: CM-8 (3) (b)

CCI-001911
The organization defines the selectable event criteria to be used as the basis for changes to the auditing to be performed on organization-defined information system components, by organization-defined individuals or roles, within organization-defined time thresholds.
NIST SP 800-53 Revision 4 :: AU-12 (3)

CCI-002112
The organization assigns account managers for information system accounts.
NIST SP 800-53 Revision 4 :: AC-2 b

CCI-002205
The information system uniquely identifies and authenticates source by organization, system, application, and/or individual for information transfer.
NIST SP 800-53 Revision 4 :: AC-4 (17)

CCI-002208
The information system uniquely authenticates destination by organization, system, application, and/or individual for information transfer.
NIST SP 800-53 Revision 4 :: AC-4 (17)
