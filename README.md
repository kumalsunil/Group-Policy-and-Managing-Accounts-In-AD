<p align="center">
<img width="624" height="426" alt="image" src="https://github.com/user-attachments/assets/3ca1dcc8-79de-4a2b-96a6-4769c2920658" />
</p>

## 🔒 Group Policy and User Account Management

This guide documents how to implement account security using Group Policy (Account Lockout Policy) and demonstrates basic user account management tasks (Disabling/Enabling and Unlocking) within Active Directory.

---

## 1. Implement Account Lockout Policy (on DC-1)

We will configure a security policy to automatically lock a user account after a specified number of failed login attempts, then test this policy.

### 1.1 Configure Account Lockout Threshold via GPO

1.  On **DC-1**, open the **Group Policy Management Console (GPMC)** (`gpmc.msc`).
2.  Navigate to the **Default Domain Policy**, right-click, and select **Edit**.
3.  In the Group Policy Management Editor, navigate to: **Computer Configuration** > **Policies** > **Windows Settings** > **Security Settings** > **Account Policies** > **Account Lockout Policy**.
4.  Set the **Account lockout threshold** to **5 invalid logon attempts**.

| Description | Screenshot |
| :--- | :--- |
| **Configuring Account Lockout** |<img width="1722" height="960" alt="image" src="https://github.com/user-attachments/assets/9510fcc0-ddb9-4d11-a66e-b4d3964b625f" />|

### 1.2 Test the Account Lockout Policy

1.  Log in to **Client-1** (or any domain-joined machine).
2.  Open a Command Prompt and run `gpupdate /force` to ensure the new policy is applied immediately.
3.  Attempt to log in **6 times** using a **bad password** for a random domain user (e.g., `bob.xox`).
4.  Observe the connection attempt failure message after the 6th attempt.

| Description | Screenshot |
| :--- | :--- |
| **Forcing Policy Update** |<img width="1093" height="356" alt="Screenshot (2)" src="https://github.com/user-attachments/assets/30f69bc0-476e-4994-8755-f1d7f36ac162" />|
| **Observation: Account Locked** | <img width="687" height="177" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/7629d4e3-b982-496c-83d6-4c641679611f" /> |

---

## 2. Managing Locked and Disabled Accounts

This section demonstrates how to manage locked and disabled accounts using Active Directory Users and Computers (ADUC) on the Domain Controller.

### 2.1 Unlocking Accounts

1.  On **DC-1**, open the **Active Directory Users and Computers (ADUC)** console.
2.  Locate the user account that was locked (e.g., `bob.xox`). Use the **Find** tool if necessary.
3.  Right-click the user and select **Properties** > **Account** and **Unlock Account**

| Description | Screenshot |
| :--- | :--- |
| **Unlocking Account** | <img width="522" height="639" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/39ad1a29-65ab-4bc3-a42c-4250602ae5a4" />|

### 2.2 Disable and Re-enable an Account

1.  In **ADUC**, right-click the same user account and select **Disable Account**.
2.  Attempt to log in with the disabled account on **Client-1** and observe the error.
3.  Return to **ADUC**, right-click the user, and select **Enable Account**.
4.  Attempt to log in successfully on **Client-1**.

| Description | Screenshot |
| :--- | :--- |
| **Account Tab** | <img width="656" height="840" alt="Screenshot (5)" src="https://github.com/user-attachments/assets/151c47f4-2af3-4a33-8af8-a94df84beb58" />|
