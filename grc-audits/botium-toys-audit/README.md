# Internal IT Security Audit: Botium Toys

## Project Overview
This project documents an internal IT security audit for Botium Toys, a U.S.-based company that develops and sells toys through an e-commerce platform and a single physical retail location.

The audit evaluates the organization's security posture against the NIST Cybersecurity Framework (CSF) and reviews compliance alignment with:
- PCI DSS
- GDPR
- SOC (Type 1 and Type 2)

## Audit Scope and Goals
### Scope
The review covers the full security program, including:
- Employee endpoints (desktops, laptops, smartphones)
- Internal networks
- E-commerce systems
- Inventory management systems

### Goals
- Assess and document existing assets and controls
- Complete controls and compliance evaluations
- Identify security gaps and regulatory risks
- Recommend prioritized improvements to strengthen overall security posture

## Risk Assessment Summary
- **Overall Risk Score:** 8/10 (High)
- **Primary Risk Driver:** Inadequate asset management and missing control coverage for U.S. and international compliance obligations
- **Potential Business Impact:**
  - Medium risk of asset loss and operational disruption
  - High risk of regulatory penalties and legal exposure due to non-compliance

## Critical Findings
1. **Access Control Deficiencies**
	- Least privilege and separation of duties are not implemented.
	- All employees can access internally stored data, including customer PII/SPII.

2. **Data Security Gaps**
	- Customer credit card data is not encrypted.

3. **Network Defense Weakness**
	- No Intrusion Detection System (IDS) is deployed.

4. **Resilience and Recovery Gaps**
	- No formal disaster recovery plan exists.
	- No backups are maintained for critical business data.

5. **Password Governance Weaknesses**
	- Password policy does not meet current complexity standards.
	- No centralized password management solution is in place.

## Controls Assessment
| Control | Status | Notes |
|---|---|---|
| Firewall | Implemented | Traffic is filtered based on security rules |
| Antivirus Software | Implemented | Installed and monitored regularly |
| Intrusion Detection System (IDS) | Not Implemented | No active network intrusion monitoring |
| Encryption for Sensitive Data | Not Implemented | Credit card data is stored/transmitted without encryption controls |
| Least Privilege | Not Implemented | Excessive access rights across employees |
| Disaster Recovery Plan | Not Implemented | No formal recovery process for outages/incidents |
| Backups | Not Implemented | No scheduled backup strategy for critical systems |
| CCTV / Physical Locks | Implemented | Physical security safeguards are present |

## Compliance Assessment
| Framework | Status | Key Observations |
|---|---|---|
| PCI DSS | Non-compliant | Credit card data is not encrypted; password management controls are inadequate |
| GDPR | Partially compliant | Breach notification process (72-hour) and privacy policies exist; data classification and asset inventory are incomplete |
| SOC (Type 1 and Type 2) | Non-compliant | Access governance is not defined; confidentiality controls for PII/SPII are insufficient |

## Recommendations
### 1) Technical Controls
- Deploy an Intrusion Detection System (IDS) for network monitoring and alerting.
- Implement encryption for all sensitive data, especially cardholder and customer personal data.

### 2) Administrative Controls
- Enforce least privilege and separation of duties through role-based access control (RBAC).
- Define formal access governance procedures (provisioning, review, deprovisioning).

### 3) Operational Resilience
- Develop and approve a disaster recovery plan.
- Implement routine, tested backups for critical systems and data.

### 4) Identity and Password Security
- Deploy centralized password management.
- Enforce password complexity baseline:
  - Minimum 8 characters
  - At least one special character
  - Additional complexity controls recommended (uppercase, lowercase, numeric, lockout thresholds)

## Priority Action Plan
### Immediate (0-30 days)
- Encrypt cardholder data in storage and transit
- Establish minimum password policy and centralized enforcement
- Restrict high-risk data access based on role

### Near-Term (30-90 days)
- Implement IDS and alert response workflow
- Stand up automated backup jobs and backup verification
- Draft and approve disaster recovery procedures

### Mid-Term (90+ days)
- Perform access recertification reviews
- Complete data classification and asset inventory process
- Conduct internal control testing for PCI DSS, GDPR, and SOC readiness

## Conclusion
Botium Toys currently faces a high risk posture due to major control and compliance gaps in access management, data protection, and operational resilience. Addressing the identified priorities will materially reduce regulatory exposure and strengthen the organization's ability to protect sensitive data and sustain business operations.
