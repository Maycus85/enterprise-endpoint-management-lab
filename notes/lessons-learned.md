## Tenant Verification (Initial Setup)

Tenant verification pending after Business Premium trial creation.
Access to Entra ID and Endpoint Manager is restricted during this phase.

## Tenant Rebuild (Billing Verification Deadlock)

Initial tenant entered a stuck verification state (>7 days).
Billing actions were blocked while organization fields were read-only.
Decision: discard tenant and rebuild clean.

Lesson learned:
- If verification exceeds ~5 days with billing blocked, rebuild is faster than waiting.

  
Conditional Access & Compliance (Practice Lab)

Lesson learned:
- Configuration Policies enforce settings, while Compliance Policies evaluate device state as a compliance signal that Conditional Access can use.
- Conditional Access is evaluated per sign-in, not per device check-in.
- “Not applied” in Conditional Access does not indicate misconfiguration, only that scope or conditions did not match.
- Device-level views (device compliance, device configuration) are more reliable than policy summary dashboards.


## Autopilot & Intune – Practical Pitfalls and Fixes

### Device vs User Scope Misconfiguration
Issue:
A BitLocker configuration policy showed no evaluation results (all counters = 0).

Cause:
The policy was assigned to users, although the settings were device-only.

Fix:
Reassigned the policy to a device group.

Lesson learned:
Correct scope (user vs device) is mandatory for policy evaluation.
A valid policy with a wrong scope behaves as if it does not exist.


### Configuration Policy vs Compliance Visibility
Observation:
A configuration policy successfully enforced BitLocker, but policy-level reporting remained empty.

Cause:
The device already met the required state before policy assignment.

Lesson learned:
Configuration policies enforce state.
Compliance policies provide visibility and reporting.
Policy overview reports can lag behind device-level status.


### Autopilot Device Preparation – Group Ownership Requirement
Issue:
Autopilot Device Preparation policy creation failed with an error stating that
the Intune Provisioning Client was not an owner of the selected group.

Cause:
Autopilot Device Preparation relies on a service principal with ownership
permissions on the target device group.

Fix:
Assigned the Intune Provisioning Client service principal as owner of the device group.

Lesson learned:
Some Autopilot operations depend on service principal permissions,
not on admin user roles.


### Enrollment vs Compliance Timing
Initial assumption:
Device compliance must be met before enrollment and login.

Actual behavior:
Enrollment and user sign-in must succeed before compliance can be evaluated.

Lesson learned:
Users must be able to sign in and enroll devices in order to become compliant.
Conditional Access enforces compliance only at resource access, not during setup.


### Hardware Hash Registration Behavior
Observation:
After device reset, Windows reported the device as already registered.

Explanation:
The hardware hash uniquely identifies the device and remains registered
until explicitly removed from Autopilot.

Lesson learned:
Autopilot device recognition is hardware-based, not installation-based.
Device resets do not invalidate Autopilot registration.


### Update Rings vs Feature Updates
Lesson learned:
A successful Update Ring assignment does not guarantee a visible OS version change.
Windows version control requires a dedicated Feature Update Policy.

### Lesson learned: Custom Compliance limitations

- Custom compliance policies may remain in "Not applicable" state
- Behavior is tenant- and timing-dependent
- Not suitable for deterministic Conditional Access demonstrations
- Prefer user- and app-based Conditional Access conditions for testing and documentation


