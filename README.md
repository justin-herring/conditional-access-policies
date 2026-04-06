# Conditional Access Policies — Microsoft Entra ID

Documents the creation and configuration of Conditional Access policies in Microsoft Entra ID 
following Zero Trust principles. Conditional Access acts as the policy engine for access 
decisions, replacing per-app MFA settings with centralized, org-wide controls.

---

## Policies Configured

### 1. Require MFA — All Users
**Purpose:** Enforce Multi-Factor Authentication for every user across all cloud apps.

| Setting | Value |
|---|---|
| Users | All users |
| Target resources | All cloud apps |
| Grant control | Require MFA |
| Policy state | Report-only |

> **Why Report-only?** Microsoft best practice is to run new policies in Report-only mode first.
> This lets you monitor impact and catch unintended blocks before enforcing the policy.
> In a production environment this would move to **On** after a review period.

📷 Policy overview*<img width="1440" height="852" alt="Screenshot 2026-04-06 162243" src="https://github.com/user-attachments/assets/3e345d71-7853-4c5c-86a8-48804134583e" />
📷 User assignment*<img width="1440" height="852" alt="Screenshot 2026-04-06 162326" src="https://github.com/user-attachments/assets/fdc28f81-9ed1-4b56-a40b-edc913c159eb" />

📷 Grant control — Require MFA*<img width="1440" height="852" alt="Screenshot 2026-04-06 162359" src="https://github.com/user-attachments/assets/cc1bb641-8517-4da1-9fa7-4281f09ef09b" />

📷 Policy saved and visible in the CA policy list*<img width="1440" height="852" alt="Screenshot 2026-04-06 163628" src="https://github.com/user-attachments/assets/85990a32-24c3-444d-95c9-3e52b3a4443a" />


---

### 2. Block Legacy Authentication
**Purpose:** Block authentication protocols that do not support MFA (e.g., SMTP, IMAP, POP3).
Legacy authentication is a common attack vector and should be disabled in all modern environments.

| Setting | Value |
|---|---|
| Users | All users |
| Target resources | All cloud apps |
| Conditions — Client apps | Exchange ActiveSync, Other clients |
| Grant control | Block access |
| Policy state | Report-only |

> **Why block legacy auth?** Microsoft reports that over 99% of password spray attacks
> and a large percentage of credential stuffing attacks use legacy authentication protocols.
> These protocols cannot prompt for MFA, making them a critical gap in identity security.

📷 Client apps condition configured*<img width="1440" height="852" alt="Screenshot 2026-04-06 162651" src="https://github.com/user-attachments/assets/f38947d6-a046-4bf9-af97-5b96a21d3244" />

📷 Block access grant control*<img width="1440" height="852" alt="Screenshot 2026-04-06 162803" src="https://github.com/user-attachments/assets/6353b8c3-ba14-486e-9274-72ff91b15a1a" />

📷 Completed policy in policy list*<img width="1440" height="852" alt="Screenshot 2026-04-06 164720" src="https://github.com/user-attachments/assets/908c5e9f-b49b-405a-a254-95ab2dfd7089" />


---

## Key Concepts Demonstrated

- **Zero Trust principle:** Never trust, always verify — CA enforces this at every login
- **Report-only mode:** Safe testing before enforcement — avoids accidental lockouts
- **Legacy auth blocking:** Closes a major attack vector ignored by basic MFA rollouts
- **Centralized policy management:** One policy covers all apps vs. configuring MFA per app

---

## Related Projects

- [Bulk User Provisioning](https://github.com/justin-herring/bulk-user-provisioning)
- [IAM Portfolio Hub](https://github.com/justin-herring/IAM-)
