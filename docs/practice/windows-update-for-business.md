# Windows Update for Business – Practice Notes

## Update Rings vs Feature Update Policies

### Update Rings
- Control update behavior, not Windows versions
- Govern:
  - Quality updates (security patches)
  - Restart behavior
  - Active hours
  - Update deferral timing
- Assigned to device groups
- Success status means policy is applied, not that updates are installed

Key point:
Update Rings define *how* updates are installed, not *which* Windows version is used.


### Feature Update Policies
- Explicitly define a target Windows version
- Example:
  - Windows 11, version 23H2
- Devices below the target version can upgrade up to it
- Devices already above the target version are not downgraded

Important:
Feature Update Policies never trigger downgrades.
They act as an upper upgrade boundary, not a rollback mechanism.


### Observed Behavior
- After assigning a Feature Update Policy, the device initiated a new update scan
- Quality updates were installed despite the device being previously reported as up to date

Explanation:
- Quality updates are governed by Update Rings
- Feature Update Policies only affect feature upgrades
- A new policy assignment can trigger a fresh update evaluation cycle


### Key Takeaways
- Update Rings control update behavior
- Feature Update Policies control target versions
- Quality updates and feature updates are managed independently
- Policy success does not imply immediate visible changes
