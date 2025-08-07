<p align="center">
<img width="auto" height="auto" alt="AD" src="https://github.com/user-attachments/assets/8997adb8-3e38-4019-9da5-6fadf4bab369" />
</p>

# Group Policy & Managing Accounts

## Lab Prerequisites

- [Lab Architecture: Preparing Active Directory Infrastructure in Azure](https://github.com/EddieJIV/Lab-Architecture-Preparing-Active-Directory-Infrastructure-in-Azure/blob/main/README.md)
- [Deploying & Configuring Active Directory](https://github.com/EddieJIV/Deploying-and-Configuring-Active-Directory)
- [Creating Users with Powershell](https://github.com/EddieJIV/Creating-Users-with-PowerShell)

## Lab Enviorments

-  Microsoft Azure
-  Windows Domain Controller
-  Windows 10
- Remote Desktop Protocol 
- Active Directory Users and Computers
- Group Policy Management Console


## Configuring an Account Lockout Threshold Policy in Active Directory using Group Policy
*Step-by-Step insturctions for defining settings that control when an account is locked after multiple failed login attempts, how long the account remains locked, and how the lockout counter is reset.*

- First things first, get logged into DC-1 as an Administrator (mydomain.com\jane_admin)

- Click Start, and type gpmc.msc in the search box, then press Enter. This opens the Group Policy Management Console.

<img width="700" height="700" alt="GPMC.MSC" src="https://github.com/user-attachments/assets/f1a42755-dc02-40b9-b5a1-8ba821efa393" />


- Navigate to the Default Domain Policy by going to:
  - Forest: mydomain.com > Domains > mydomain.com > Default Domain Policy
 
<img width="700" height="700" alt="rightclickedit" src="https://github.com/user-attachments/assets/3e4a9aa4-d34f-411f-8d24-a2ae8eb15ff8" />

- Right click on Default Domain Policy and click on edit to be brought to the Group Policy Management Editor.

<img width="700" height="700" alt="Account Lockout Policy" src="https://github.com/user-attachments/assets/d4513e76-9f39-499e-b328-35226894e6b0" />



- Navigate to the Account Lockout Policy Settings. In the Group Policy Management Editor, expand the following:
   - Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.

