# Modern Endpoint Engineering Lab

Hands-on reference environment for designing and validating modern workplace security using Microsoft Intune, Entra ID, Windows Autopilot and Conditional Access.

This lab focuses on **real-world security architecture**, not just feature configuration.

---

## 🎯 Objective

Build and document a production-oriented modern device management environment that reflects how enterprises establish trust between:

- User identity  
- Device posture  
- Compliance state  
- Access control  

The lab follows a Zero Trust-inspired model where **authentication alone is not sufficient — device trust is required.**

---

## 🧠 Architecture Focus

Rather than documenting isolated features, this repository follows the lifecycle of modern endpoint security:

1. **Identity** → Who is requesting access?  
2. **Device Enrollment** → What device is being used?  
3. **Compliance** → Can the device be trusted?  
4. **Conditional Access** → Should access be granted?

👉 Together, these layers form the foundation of a Zero Trust access model.

---

## 🔐 Key Security Scenario Implemented

✔ Enrolled a Windows device into Intune  
✔ Forced a non-compliant state intentionally  
✔ Implemented Conditional Access requiring compliant devices  
✔ Validated enforcement through sign-in telemetry  
✔ Successfully blocked cloud access from an untrusted device  

This demonstrates how device posture directly impacts authorization decisions.

---

## 📚 Repository Structure

docs/md102/

identity-access.md
→ Identity foundation and access concepts

device-enrollment.md
→ Azure AD Join and MDM enrollment

compliance-security.md
→ Device trust evaluation

conditional-access-enforcement.md
→ Access control based on compliance state


---

## 🎓 Purpose

This repository serves as:

- A deep technical learning environment  
- MD-102 certification support  
- A security architecture reference  
- A demonstration of practical endpoint engineering skills  

---

## 🚫 Out of Scope

To maintain architectural clarity, this lab intentionally excludes:

- On-prem Active Directory  
- Hybrid Join  
- Legacy management models  
- Production workloads  

The focus is fully on **cloud-native device management.**

---

## 🚀 Direction

Future expansions will explore:

- Device remediation workflows  
- Risk-based Conditional Access  
- MFA + device trust layering  
- Update governance  
- Security baselines  
- Endpoint hardening  

Goal: evolve toward a mature enterprise-grade Zero Trust model.
