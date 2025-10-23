# 🔐 Conditional-Access-PIM-Passwordless-Entra-ID
Lab demonstrating how Conditional Access, PIM, and PasswordLess authentication integrate in Microsoft 365 Entra ID to enforce Zero-Trust, step-up access control and protect privileged roles.

 ### [Repro Lab Demo](https://youtu.be/7eJexJVCqJo)

## 📘 Repository Description
Hands-on lab demonstrating how Conditional Access, Privileged Identity Management (PIM), and Passwordless authentication integrate within Microsoft Entra ID to deliver a Zero-Trust, step-up authentication experience.
This scenario showcases end-to-end configuration from Authentication Strength and Authentication  Context creation to Conditional Access enforcement and PIM role activation proving practical understanding of Microsoft 365 E5 security architecture.
<br />

## 🎯 Lab Objective
To configure a Conditional Access policy that enforces **passwordless authentication (via Microsoft Authenticator or Temporary Access Pass)** when a user attempts to **activate a privileged role through PIM**, ensuring sensitive operations require stronger authentication.

## ⚙️ Key Configuration Steps
1. **Create an Authentication Strength**  
   - Include **Microsoft Authenticator phone sign-in** and **Temporary Access Pass (TAP)** as valid passwordless methods.

2. **Create an Authentication Context**  
   - Define a tag (e.g., `pim-auth-context`) to identify when stronger authentication should be applied.

3. **Configure a Conditional Access Policy**  
   - Target the Authentication Context created above.  
   - Apply the **Authentication Strength** requiring passwordless methods.  
   - Enforce this policy when users access or activate PIM-protected roles.

4. **Set Up Privileged Identity Management (PIM)**  
   - Assign a user as eligible for a privileged role (e.g., *Security Administrator*).  
   - Require activation with justification and apply the step-up Conditional Access policy.  
   - During activation, the policy triggers the passwordless requirement (TAP or Authenticator).


<h2>Platforms & Tools Used</h2>

| Category | Portal / Tool | Purpose |
|-----------|----------------|----------|
| **Identity & Access** | Microsoft Entra ID Portal| Configure Conditional Access, PIM, Authentication Methods, Authentication Contexts and Authentication Strengths |
| **Administration** | Microsoft 365 Admin Center| Manage users, licenses, and global tenant configuration |
| **ID Governance** | Entra ID > ID Governance > Privileged Identity Management| Assign and activate eligible roles for privileged access testing |
| **Device Access** | Mobile Device with Microsoft Authenticator App | Enable passwordless sign-in and approve multi-factor authentication requests |
| **Temporary Access Pass (TAP)** | Entra ID > Authentication Methods | Generate and use TAP for passwordless testing |


<h2>Labs walk-through:</h2>
### 1️⃣ Configure Authentication Methods
1. Go to **Entra ID → Protection → Authentication methods**  
2. Enable:  
   - **Microsoft Authenticator (Passwordless sign-in)**  
   - **Temporary Access Pass (TAP)**  
3. Target to all users or a test group

<p align="center">
Authentication Method: <br/>
<img src="https://imgur.com/bY42WaD.png" height="80%" width="80%" alt=/>
<br />
<br />

 ### 2️⃣ Create an Authentication Strength
1. Navigate to **Authentication Strengths**  
2. Create New Authentication Strength: `AuthStrenght_PSWLess_PIM`  
3. Include:  
   - ✅ Microsoft Authenticator (Phone sign-in)  
   - ✅ Temporary Access Pass (One-time Use)  
4. Save and confirm 

Create New Authentication Strenght:  <br/>
<img src="https://imgur.com/buqnj7R.png" height="80%" width="80%" alt=/>
<br />
<br />

### 3️⃣ Create an Authentication Context
1. Go to **Protection → Conditional Access → Authentication Contexts**  
2. Create a new context named `PIM-Auth`  
3. Add description and save  
   *(Acts as a logical tag for the CA policy)*

New Authentication Context: <br/>
<img src="https://imgur.com/z3x6zvK.png" height="80%" width="80%" alt=/>
<br />
<br />

### 4️⃣ Create a Conditional Access Policy
1. Go to **Conditional Access → Policies → New Policy**  
2. Give it a Name
3. Assignments:  
   - **Users**: Target your test user or group  
   - **Target Resources**: Select *Authentication context → Choose the custom auth context created PIM-Auth*  
4. Grant Controls:  
   - Require **Authentication Strength → Choose the custom Strength Created**  
5. Enable the policy

Traget Resources:  <br/>
<img src="https://imgur.com/Il7nGzW.png" height="80%" width="80%" alt=/>
<br />
<br />

Access Control:  <br/>
<img src="https://imgur.com/ggzKtoQ.png" height="80%" width="80%" alt=/>
<br />
<br />

### 5️⃣ Configure PIM
1. Navigate to **Entra ID → Roles and Administrators**  
2. Select **Security Administrator** (or preferred role)  
3. Under **Privileged Access (PIM)**, enable *eligible assignments*  
4. Assign your test user as *eligible* for the role

Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

### 6️⃣ Test the Scenario
1. Sign in as the test user  
2. Go to **Entra ID → Privileged Identity Management → My Roles**  
3. Attempt to **activate** the `Security Administrator` role  
4. Observe:  
   - If signed in with password → prompt for TAP (stronger auth)  
   - If signed in passwordlessly → activation succeeds  
5. After TAP setup, activation completes successfully

## 📈 Result & Behavior
> When users activate a privileged role, Conditional Access evaluates the **Authentication Context (`PIM-Auth`)**.  
>  
> The CA policy enforces the **Passwordless_Strength**, requiring either passwordless sign-in or TAP.  
>  
> If initial sign-in used a password, Entra ID steps up the session to meet the passwordless requirement before role activation.  
>  
> The result is a secure, Zero Trust aligned design with **adaptive authentication** and **role-based protection**.

---

## 💡 Key Learnings

| Area | Learning Outcome |
|------|------------------|
| **Conditional Access** | Designed and applied a CA policy linked to authentication context and custom strength |
| **Authentication Strengths** | Defined passwordless and TAP methods to enforce strong MFA |
| **PIM Integration** | Implemented step-up authentication for privileged role activation |
| **Zero Trust Design** | Achieved context-aware access and strong identity assurance |<img width="641" height="415" alt="image" src="https://github.com/user-attachments/assets/6f50e86a-c2ae-43d9-96db-d88c2ec34373" />

--!>
