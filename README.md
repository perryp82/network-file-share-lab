# Microsoft Azure Lab: Network File Shares and Permissions

## Overview
In this lab, you will work with Network File Shares and Permissions on Microsoft Azure to demonstrate your understanding of file share configurations and permissions. **We will be using the DC-1 and Client-1 virtual machines (VMs) from the previous Active Directory lab.**

### Prerequisites
1. Access to the DC-1 VM as a domain administrator account (`mydomain.com\jane_admin`).
2. Access to the Client-1 VM as a normal domain user (`mydomain\<someuser>`).
3. Previous setup of an Active Directory environment with DC-1 and Client-1.

---

## Lab Instructions

### Step 1: Create Sample File Shares with Various Permissions
1. **Log into DC-1** using the domain admin account `mydomain.com\jane_admin`.
2. On the `C:\` drive of DC-1, create the following four folders:
   - `read-access`
   - `write-access`
   - `no-access`
   - `accounting`

3. Set the following permissions for each folder:
   - **Folder:** `read-access`  
     **Group:** `Domain Users`  
     **Permission:** `Read`  
     *(Share the folder with these settings.)*

   - **Folder:** `write-access`  
     **Group:** `Domain Users`  
     **Permission:** `Read/Write`  
     *(Share the folder with these settings.)*

   - **Folder:** `no-access`  
     **Group:** `Domain Admins`  
     **Permission:** `Read/Write`  
     *(Share the folder with these settings.)*

   - **Folder:** `accounting`  
     *(Do not configure permissions yet; skip this for now.)*

---

### Step 2: Attempt to Access File Shares as a Normal User
1. **Log into Client-1** using a normal user account (`mydomain\<someuser>`).
2. Navigate to the shared folders:
   - Open the **Run** dialog (`Start` → **Run** or `Windows Key + R`).
   - Enter `\\dc-1` to access shared folders on DC-1.
3. Test access to the folders:
   - Which folders can you access? 
   - Which folders can you create files in?
   - Does the access behavior make sense based on the permissions configured?

---

### Step 3: Create an "ACCOUNTANTS" Security Group, Assign Permissions, and Test Access
1. **Log into DC-1** as the domain admin account (`mydomain.com\jane_admin`).
2. Open Active Directory and create a security group named `ACCOUNTANTS`.

3. Set permissions for the `accounting` folder:
   - **Folder:** `accounting`  
     **Group:** `ACCOUNTANTS`  
     **Permission:** `Read/Write`  
     *(Share the folder with these settings.)*

4. Test access as the normal user:
   - On Client-1, while logged in as `<someuser>`, try to access the `accounting` share via `\\dc-1`.  
     - **Expected Result:** Access to the folder should fail.

5. Assign `<someuser>` to the `ACCOUNTANTS` group:
   - On DC-1, add `<someuser>` as a member of the `ACCOUNTANTS` security group.

6. Re-test access as `<someuser>`:
   - **Log out of Client-1** and log back in as `<someuser>`.
   - Try to access the `accounting` share via `\\dc-1`.
     - **Expected Result:** Access to the folder should now succeed.

---

## Conclusion
By completing this lab, you will have demonstrated:
- Configuring file shares with varying permissions.
- Testing access to file shares from different user accounts.
- Managing Active Directory security groups and applying permissions effectively.
