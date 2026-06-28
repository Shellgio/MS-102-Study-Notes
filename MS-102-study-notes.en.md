# MS-102 Study Notes

> [!IMPORTANT]
> These are personal revision notes for the Microsoft MS-102 exam. They are not a complete exam guide and do not cover all exam objectives. Always check Microsoft Learn and the official exam skills outline for current requirements.

## Deploy and Manage a Microsoft 365 Tenant

### Tenant Administration

> [!NOTE]
> **Service health visibility:** users assigned the Global Administrator or Service Support Administrator role can view service health in the Microsoft 365 admin center.

> [!NOTE]
> **Service health vs. Message center:** use Service health to determine whether a service is down because of failures, outages, or regional issues. Use Message center to review planned service updates.

> [!NOTE]
> **Multi-Geo / data residency:** for a multi-region Microsoft 365 deployment, a single tenant with data residency configured per country or region is typically the easiest approach to manage.

### Sharing and External Collaboration

> [!NOTE]
> **Prevent external sharing in SharePoint and OneDrive:** organization-wide sharing settings can be changed from **Org settings > Services** in the Microsoft 365 admin center. More granular external sharing settings, including domain and security group controls, are managed from **Policies > Sharing** in the SharePoint admin center.

> [!NOTE]
> **Guest invitation setting:** if Microsoft Entra External collaboration settings are configured so that only users assigned to specific admin roles can invite guests, only Global Administrators, User Administrators, and Guest Inviters can invite guests.

> [!NOTE]
> **Privacy statement and global privacy contact:** these fields are configured from the Microsoft Entra admin center properties blade. If they are not populated, external guests see a message indicating that the organization has not provided terms for review.

### Groups and Users

> [!NOTE]
> **Public Microsoft 365 groups:** groups created from the Microsoft Entra admin center are private by default and cannot be made public during creation. Groups created from the Microsoft 365 admin center can be created as private or public, and this setting can be changed later.

> [!NOTE]
> **Deleted users:** deleted user accounts remain in a suspended state for 30 days and can be restored during that period.

> [!NOTE]
> **Deleted groups:** deleted Microsoft 365 groups and Microsoft Entra security groups are retained for 30 days and can be restored. This does not apply to distribution groups, and the 30-day period is not customizable.

> [!NOTE]
> **Importing users:** when importing users in the Microsoft 365 admin center, the only required values are Username, which becomes the user principal name, and Display Name.

> [!NOTE]
> **Dynamic membership:** only Microsoft 365 groups and security groups support dynamic membership.

> [!NOTE]
> **User license reporting:** `Get-MgUser` can be used to generate a report of active users and licenses. `Get-MgUserLicenseDetail` is used per user.

### Roles and Permissions

> [!NOTE]
> **MFA settings:** the Privileged Authentication Administrator role can manage MFA settings for users.

> [!IMPORTANT]
> **Microsoft Secure Score management:** Global Administrators, Security Administrators, Exchange Administrators, and SharePoint Administrators can manage Microsoft Secure Score and recommended actions. User Administrators have read-only access.

> [!NOTE]
> **Compare role permissions:** the Microsoft 365 admin center can compare permissions for up to three roles at a time, which helps apply least privilege.

> [!NOTE]
> **Compliance Manager assessments:** Compliance Data Administrator, Global Administrator, and Compliance Administrator can view Microsoft Purview Compliance Manager assessments. Compliance Data Administrator is the least-privileged option among those roles. Organization Management can view assessment templates, not assessments.

> [!NOTE]
> **Purview compliance portal roles:** common roles with access include Global Administrator, Compliance Data Administrator, Compliance Administrator, Security Administrator, and Information Protection preview roles such as Admins, Analysts, Investigators, and Readers.

> [!NOTE]
> **Password Administrator vs. Helpdesk Administrator:** Helpdesk Administrator can manage passwords for all users and administrators. Password Administrator can reset passwords for users but not administrators.

### Secure Defaults

> [!IMPORTANT]
> **Security defaults:** enabling Microsoft Entra security defaults contributes to Secure Score recommendations such as requiring MFA for administrators, ensuring users can complete MFA, and blocking legacy authentication.

## Implement and Manage Microsoft Entra Identity and Access

### Hybrid Identity and Synchronization

> [!NOTE]
> **Microsoft Entra Cloud Sync ports:** ports 80 and 443 are required. Port 80 downloads certificate revocation lists during TLS/SSL validation, and port 443 handles outbound communication with Microsoft Entra ID.

> [!NOTE]
> **Cloud Sync scoping:** configure Microsoft Entra Cloud Sync scope from the Microsoft Entra admin center under hybrid management and cloud sync. You can select which organizational units synchronize.

> [!IMPORTANT]
> **Manual Microsoft Entra Connect Sync cycle:** use `Start-ADSyncSyncCycle -PolicyType Delta` to synchronize only changes instead of running a full synchronization.

> [!NOTE]
> **Synchronizing specific objects:** select the required domains and organizational units from each domain.

> [!NOTE]
> **Microsoft Entra Connect Health insights:** Extranet lockout trends, failed sign-in report, and privacy-compliant reporting are available through Microsoft Entra Connect Health. Risky sign-ins, deleted users, and failed MFA reports are Microsoft Entra ID features.

> [!NOTE]
> **Unique attributes:** `mail`, `signInName`, and `userPrincipalName` must be unique for Microsoft Entra synchronization to succeed. A common error is `AttributeValueMustBeUnique`.

> [!NOTE]
> **Sync error analysis:** synchronization errors can be analyzed from the Microsoft Entra Connect server and Microsoft Entra Connect Health.

> [!NOTE]
> **Pass-through and federated authentication:** both support using an on-premises Active Directory domain for Microsoft 365 authentication.

> [!NOTE]
> **Password protection on domain controllers:** the DC Agent service initiates download of new Microsoft Entra password protection policies.

> [!NOTE]
> **Accidental deletion threshold:** the default Microsoft Entra Cloud Sync accidental deletion threshold is 500. You can lower it to match the size and risk profile of your environment.

### Administrative Units

> [!NOTE]
> If an administrator is assigned Groups Administrator and User Administrator roles scoped to an administrative unit, but only a security group is added to that administrative unit, the administrator can manage group membership. Users must be added directly to the administrative unit to be managed directly.

### Authentication and Secure Access

> [!NOTE]
> **Authenticator number matching:** configure Microsoft Authenticator policies to require number matching for push notifications.

> [!NOTE]
> **Pilot app notifications for MFA:** configure Microsoft Authenticator settings to Push and require users to re-register MFA to enforce the method.

> [!TIP]
> **Passwordless RDP with Windows Hello for Business:** Certificate Trust is the solution that supports passwordless RDP.

> [!NOTE]
> **Persistent browser cookie:** the maximum persistent cookie duration is 365 days.

### Licensing and Identity Protection

> [!NOTE]
> **Microsoft Entra ID Protection prerequisites:** Microsoft 365 E3 and EMS E3 do not include Microsoft Entra ID P2. Microsoft 365 E5 and EMS E5 include the capabilities needed for risk detection and automated remediation. A Microsoft Entra P2 add-on can also be used with lower tiers such as Microsoft 365 E3 or Business Premium.

> [!IMPORTANT]
> **Security questions:** administrators cannot use security questions to reset their passwords.

> [!IMPORTANT]
> **Leaked credential detection:** Microsoft Entra ID Protection requires password hashes in Microsoft Entra ID, so password hash synchronization must be deployed.

> [!NOTE]
> **Risky sign-in reports:** Global Reader, Security Administrator, and Security Reader can access Microsoft Entra ID Protection risky sign-in reports.

> [!NOTE]
> **User risk policy:** requiring a password change is the only allow-access requirement in a user risk policy.

## Manage Security and Threats with Microsoft Defender XDR

### Microsoft Defender for Endpoint

> [!NOTE]
> **Supported onboarding targets:** Defender for Endpoint supports supported Windows versions, Windows Server 2012 and later, Azure Virtual Desktop, Windows 365, macOS, Linux, Android, and iOS.

> [!NOTE]
> **iOS without enrollment:** Defender for Endpoint on iOS supports MAM, Intune MDM + MAM, and MAM without enrollment. MAM without enrollment manages apps with app protection policies on devices not enrolled in Intune MDM.

> [!IMPORTANT]
> **Turning on RBAC:** only Global Administrators and Security Administrators can enable RBAC in Defender for Endpoint. When RBAC is enabled, users with read-only Microsoft Entra roles such as Security Reader lose access until they are assigned a Defender for Endpoint RBAC role.

> [!NOTE]
> **Onboarding clients with Intune:** first turn on the Microsoft Intune connection in Microsoft Defender XDR settings. Then enable Microsoft Defender for Endpoint in Intune. Finally, create a configuration profile using the Defender for Endpoint template for Windows devices.

> [!NOTE]
> **Vulnerability Management exposure score:** the exposure score reflects real-world device compromise risk by considering attack surface, misconfigurations, network context, software vulnerability risk, configuration, and exploitability.

### Reports, Alerts, and Secure Score

> [!NOTE]
> **Alert aggregation:** when multiple events match an alert policy in a short time, alert aggregation adds them to an existing alert. In Microsoft 365 E5, the alert aggregation interval is one minute.

> [!NOTE]
> **Recommended action statuses that increase Secure Score:** Completed, Resolved through third party, and Resolved through alternate mitigation.

> [!NOTE]
> **Triggered alert properties:** status and comment can be modified after an alert is triggered. Severity and category are defined in the alert policy and cannot be modified on the triggered alert.

> [!NOTE]
> **View-Only Manage Alerts role:** this Microsoft Purview role allows users to view only alerts categorized as Others.

> [!NOTE]
> **Alert policy email notifications:** the highest daily notification limit is No limit. Other available values include 1, 5, 10, 25, 50, 100, 150, and 200.

### Microsoft Defender for Office 365

> [!NOTE]
> **Attack simulation training:** when creating a credential harvest simulation payload, Email is the available payload type.

> [!NOTE]
> **SecOps mailbox:** use a SecOps mailbox when messages for a user must remain unfiltered and not protected by Microsoft Defender for Office 365 so that security teams can collect and analyze messages.

> [!NOTE]
> **Assigning a SecOps mailbox:** configure it in the Microsoft Defender portal under Email & collaboration, threat policies, Advanced delivery.

> [!NOTE]
> **Custom quarantine retention:** anti-spam and anti-phishing policies have a default 15-day quarantine period that can be customized. Anti-malware and Safe Attachments quarantines use 30 days and are not customizable.

> [!NOTE]
> **Restricted entities:** accounts that exceed outbound email limits can be added to Restricted entities. To allow sending again, unblock the account in the Microsoft Defender portal under Email & collaboration > Review > Restricted entities. Global Administrators, Security Administrators, or members of Exchange Organization Management can unblock users.

> [!NOTE]
> **Tenant Allow/Block List:** Microsoft Defender for Office 365 Plan 1 supports 1,000 allow and 1,000 block entries. Plan 2 supports 5,000 allow and 10,000 block entries. Organization Management is the least-privileged role group for adding and removing entries.

> [!NOTE]
> **Detailed URL threat protection report:** detailed exports support a maximum time range of one day. Summary reports can cover a longer period.

### Microsoft Defender for Cloud Apps

> [!NOTE]
> **Microsoft 365 app connector:** adding the Microsoft 365 app connector to Defender for Cloud Apps requires Global Administrator permissions during initial authorization.

> [!NOTE]
> **Session policy not blocking downloads:** if downloads still occur and blocked attempts are not logged, add the missing application domains so all traffic routes through the Defender for Cloud Apps reverse proxy.

> [!IMPORTANT]
> **MDCA policy types:** activity policies filter user activities and thresholds over time. Anomaly detection policies identify behavioral anomalies. App discovery policies evaluate discovered app traffic from logs. Session policies apply real-time controls during proxied sessions.

## Manage Compliance with Microsoft Purview

### Retention

> [!NOTE]
> **Minimum retention policies for Teams:** Teams channel messages and Teams private channel messages each require separate retention policies. Other locations such as Exchange email, SharePoint sites, OneDrive accounts, and Exchange public folders can be configured in one policy. At least three retention policies are required for that scenario.

> [!NOTE]
> **Retention precedence:** a retention policy that is published and then manually applied to content takes precedence over policies applied to a location.

> [!NOTE]
> **Teams chat retention:** Teams chats can receive retention settings only through a retention policy. Retention label policies can apply retention to Exchange Online, SharePoint Online, OneDrive, and Microsoft 365 groups.

> [!NOTE]
> **MRM retention policy for Exchange Online mailboxes:** enable mailbox archiving, create an MRM retention tag in Microsoft Purview, create an MRM retention policy, and then apply the policy to mailboxes from the Exchange admin center.

### DLP

> [!NOTE]
> **DLP Policy Tips priority:** DLP rules run in priority order, where the lowest priority number wins. Only the Policy Tip from the first matching rule is shown.

> [!NOTE]
> **Endpoint DLP supported devices:** Microsoft Purview endpoint DLP supports Windows 10 or later and macOS devices.

> [!NOTE]
> **DLP reports:** DLP Policy Matches shows files matched by DLP policies, but not rule-level detail. DLP Incidents shows matches over time at the rule level.

> [!TIP]
> **Scheduled DLP Policy Matches report:** it can be scheduled weekly or monthly.

> [!WARNING]
> **DLP locations:** one DLP policy can apply to all locations except Microsoft 365 Copilot. A separate policy is required for Microsoft 365 Copilot.

> [!NOTE]
> **False positives:** users can report false positives for items identified by DLP policies only when the DLP policy status is On.

> [!NOTE]
> **Teams one-to-one chat files:** files uploaded to a Teams one-to-one or group chat are stored in the sender's OneDrive and shared with chat participants. Channel files are stored in the team's SharePoint folder.

### Sensitivity and Site Settings

> [!NOTE]
> **SharePoint default privacy:** the default privacy setting of a SharePoint Online site can be configured in a sensitivity label.

