# Windows Autopilot – End-to-End Flow (Real World)

This document describes the real execution order of Windows Autopilot,
Microsoft Entra ID, Intune enrollment, compliance evaluation and Conditional Access.

## Phase 0 – Windows Installation
- Clean Windows installation or reset
- No cloud interaction yet

## Phase 1 – Autopilot Hardware Identification
- Autopilot client sends hardware hash to Microsoft
- Microsoft Autopilot service identifies tenant ownership
- Assigned Autopilot deployment profile is returned to the device

Important:
At this stage, neither Entra ID nor Intune enrollment is involved.

## Phase 2 – Out-of-Box Experience (OOBE)
- OOBE behavior is customized by Autopilot profile
- User-driven deployment
- Microsoft Entra join is enforced

## Phase 3 – User Authentication (Entra ID)
- User signs in with Entra ID credentials
- Conditional Access evaluates:
  - User identity
  - MFA requirements
  - Location and risk
- Device compliance is NOT evaluated yet

## Phase 4 – MDM Enrollment (Intune)
- Device is enrolled into Intune after successful Entra sign-in
- Management channel is established
- Device becomes a managed device

## Phase 5 – Configuration and Compliance
- Configuration profiles are applied
- Security settings enforced (BitLocker, Defender, etc.)
- Compliance state is evaluated asynchronously

## Phase 6 – Conditional Access Enforcement
- Conditional Access checks device compliance at resource access
- Access is allowed or blocked based on last known compliance state

Key takeaway:
Enrollment and login must succeed before compliance can be enforced.
