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
 
  <img width="auto" height="auto" alt="Lockout threshold" src="https://github.com/user-attachments/assets/22508ebd-cd62-440a-aceb-fe8c54bf41aa" />

- If you double click on Account Lockout Threshold, and change the threshold to 5, after 5 incorrect password attempts, the account will be locked.
- Click Apply, then Click OK.

<img width="700" height="700" alt="Polity Setting Change Auto complete" src="https://github.com/user-attachments/assets/6470e82e-02ee-439d-af0d-18df4fc44593" />


- Notice how the Account lockout duration, Administrator account lockout, and Reset Account lockout counter all change as well.
- In order for us to actually update the Group Policy, we can either wait for the Group Policy to propagate automatically, or force an update immediately.
- For this lab we are going to force the update now.

<img width="auto" height="auto" alt="cmd /force" src="https://github.com/user-attachments/assets/67014323-b00d-4326-ab27-55afead830d6" />

- In order to do so, log into Client-1 as Jane_admin.
- Open Command Prompt and type gpupdate /force, then press Enter.
  - reminder: the above image of the Command Prompt is taken from Client-1, logged in as our admin for this lab.

---

We have now successfully configured an account lockout policy in Active Directory using Group Policy.
- Log out of Jane_admin on Client-1 and attempt to log into Client-1 with any of the domain users we created in our last lab; using the wrong password 5 times, to effectively get locked out of the account.
  - You can use the same account you used last lab if you have the credentials saved for ease of access, or navigate to Active Directory Users and Computers > mydomain.com > _EMPLOYEES on DC-1 to observe your users.
 
 



