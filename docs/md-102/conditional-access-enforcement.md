# Phase 3 – Conditional Access & Device Compliance Enforcement

## 🎯 Objective
Implement a Zero Trust access control model by enforcing Conditional Access policies that restrict cloud resource access to compliant devices only.

The goal was to simulate a real-world enterprise security scenario where device posture directly impacts authentication and authorization decisions.

---

## 🧱 Architecture Overview

This lab was built on three core identity and security pillars:

- **User Identity (Entra ID)**
- **Device Trust (Intune Compliance)**
- **Access Control (Conditional Access)**

By combining these layers, access decisions move beyond credentials toward a posture-based security model.

---

## ⚙️ Implementation Steps

### 1. Device Enrollment
- Windows VM was Azure AD joined.
- Device successfully enrolled into Microsoft Intune.
- Verified MDM authority and device visibility in both Entra ID and Intune.

---

### 2. Compliance Policy Design

Created a custom compliance policy:

**Policy Name:**  
`LAB – Compliance – FORCE NonCompliant (OS Version)`

**Configuration:**
- Enforced a minimum OS version intentionally higher than the device version.

**Purpose:**
To deliberately push the device into a **Non-Compliant** state and validate downstream access enforcement.

✅ Result:  
Device correctly evaluated as **Non-Compliant**.

---

### 3. Conditional Access Strategy

Instead of targeting all users immediately, a **pilot-first approach** was used.

**Policy Name:**  
`CA – Block NonCompliant Devices (LAB)`

**Assignments:**
- Included: Test User  
- Excluded: Global Admin (Safety Net)

**Target Resources:**
- All Cloud Apps (via Microsoft Graph)

**Grant Control:**
✔ Require device to be marked as compliant.

---

### 4. Safe Deployment Methodology

Followed a professional rollout pattern:

1. Deploy in **Report-only mode**
2. Validate behavior via Sign-in Logs
3. Confirm policy evaluation
4. Enforce policy

This approach mirrors enterprise change-control practices and prevents tenant lockout scenarios.

---

## 🔎 Validation

Using **Entra Sign-in Logs**, the policy produced:

**Result:**  
`Report-only: Failure`

**Root Cause:**  
Grant control not satisfied → Device not compliant.

This confirmed that Conditional Access was correctly evaluating device posture during token issuance.

---

### Final Enforcement Test

After switching the policy to **On**:

Attempted login from the non-compliant device resulted in:

> **"This device must meet your organization's compliance requirements."**

✅ Access successfully blocked.

---

## 🧠 Key Technical Insights

### Identity Alone Is No Longer Sufficient
Authentication succeeded, but authorization failed due to device posture.

This demonstrates a fundamental Zero Trust principle:

> **Trust is evaluated continuously and contextually.**

---

### Conditional Access Protects Tokens — Not Apps
Blocking Microsoft Graph effectively prevents access to nearly all Microsoft 365 services.

Control the token → control the environment.

---

### Compliance Is a Security Signal
Without Conditional Access, compliance is merely informational.

Combined together, they form a powerful enforcement mechanism.

---

## 🔐 Security Design Principles Applied

- Pilot-first deployment
- Explicit admin exclusion
- Controlled failure testing
- Log-driven validation
- Zero Trust alignment

---

## 🚀 Outcome

Successfully implemented a posture-based access control model where:

✔ Non-compliant devices cannot access cloud resources  
✔ Admin access remains protected  
✔ Policies behave predictably  
✔ Security enforcement is validated through telemetry  

---

## 📌 Next Phase

Future labs will focus on:

- Device remediation workflows  
- Restoring compliance states  
- Risk-based Conditional Access  
- MFA + Device trust layering  
- Session controls  
- Dynamic device targeting  

Goal: evolve toward a fully mature Zero Trust architecture.
