# Conditional Access vs Compliance – Clear Separation

## Intune Configuration
- Enforces device settings
- Example: Enable BitLocker, configure Defender

## Intune Compliance Policies
- Evaluate device state
- Result: Compliant / Non-compliant / Unknown
- Compliance status is written back to Entra ID

## Conditional Access (Entra ID)
- Evaluated at authentication time
- Uses signals such as:
  - User identity
  - Location
  - Device compliance state
- Does NOT configure or fix devices

Key principle:
Conditional Access never makes a device compliant.
It only decides whether access is granted.
