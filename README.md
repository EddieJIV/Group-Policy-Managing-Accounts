<p align="center">
<img width="auto" height="auto" alt="AD" src="https://github.com/user-attachments/assets/8997adb8-3e38-4019-9da5-6fadf4bab369" />
</p>

# Group Policy & Managing Accounts

## Skills Demonstrated

- **Active Directory Administration** – Managing user accounts and domain resources  
- **Group Policy Management** – Enforcing domain-wide security policies 
- **Windows Server Tools** – Using Group Policy Management Console and Active Directory Users and Computers effectively  
- **PowerShell & Command Line** – Running commands like `gpupdate /force` to apply changes  
- **Troubleshooting** – Identifying and resolving account lockout issues  
- **Cloud Infrastructure** – Deploying and managing an AD environment in Microsoft Azure 

## Lab Prerequisites

- [Lab Architecture: Preparing Active Directory Infrastructure in Azure](https://github.com/EddieJIV/Lab-Architecture-Preparing-Active-Directory-Infrastructure-in-Azure/blob/main/README.md)
- [Deploying & Configuring Active Directory](https://github.com/EddieJIV/Deploying-and-Configuring-Active-Directory)
- [Creating Users with PowerShell](https://github.com/EddieJIV/Creating-Users-with-PowerShell)

## Lab Enviorments

-  Microsoft Azure
-  Windows Domain Controller
-  Windows 10 Client
- Remote Desktop Protocol 
- Active Directory Users and Computers
- Group Policy Management Console
- Commant Prompt / PowerShell

---

## Introduction
In this lab, we configure and test an **Account Lockout Threshold Policy** in Active Directory using Group Policy. This security setting defines when an account is locked after failed login attempts, how long the lockout lasts, and how the counter resets.

---


## Configuring an Account Lockout Threshold Policy in Active Directory using Group Policy
*Step-by-Step instructions for defining settings that control when an account is locked after multiple failed login attempts, how long the account remains locked, and how the lockout counter is reset.*

- First things first, get logged into DC-1 as an Administrator (mydomain.com\jane_admin)

- Click Start, and type gpmc.msc in the search box, then press Enter. This opens the Group Policy Management Console.

<img width="700" height="700" alt="GPMC.MSC" src="https://github.com/user-attachments/assets/f1a42755-dc02-40b9-b5a1-8ba821efa393" />


- Navigate to the Default Domain Policy by going to:
  - Forest: mydomain.com > Domains > mydomain.com > Default Domain Policy
 
<img width="700" height="700" alt="rightclickedit" src="https://github.com/user-attachments/assets/3e4a9aa4-d34f-411f-8d24-a2ae8eb15ff8" />

- Right-click on Default Domain Policy and click on edit to be brought to the Group Policy Management Editor.

<img width="700" height="700" alt="Account Lockout Policy" src="https://github.com/user-attachments/assets/d4513e76-9f39-499e-b328-35226894e6b0" />

- Navigate to the Account Lockout Policy Settings. In the Group Policy Management Editor, expand the following:
   - Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.
 
  <img width="auto" height="auto" alt="Lockout threshold" src="https://github.com/user-attachments/assets/22508ebd-cd62-440a-aceb-fe8c54bf41aa" />

- If you double-click on Account Lockout Threshold and change the threshold to 5, after 5 incorrect password attempts, the account will be locked.
- Click Apply, then click OK.

<img width="700" height="700" alt="Polity Setting Change Auto complete" src="https://github.com/user-attachments/assets/6470e82e-02ee-439d-af0d-18df4fc44593" />


- Notice how the Account lockout duration, Administrator account lockout, and Reset Account lockout counter all change as well.
- In order for us to actually update the Group Policy, we can either wait for the Group Policy to propagate automatically or force an update immediately.
- For this lab, we are going to force the update now.

<img width="auto" height="auto" alt="cmd /force" src="https://github.com/user-attachments/assets/67014323-b00d-4326-ab27-55afead830d6" />

- In order to do so, log in to Client-1 as Jane_admin.
- Open Command Prompt and run:  
  ```bash
  gpupdate /force
  ``` 
  - reminder: the above image of the Command Prompt is taken from Client-1, logged in as our admin for this lab.

---

Congratulations! We have now successfully configured an account lockout policy in Active Directory using Group Policy. Let's put it to the test by logging in to one of our domain users and see the account lockout policy in action.

---

<img width="500" height="500" alt="Failed logon attempt" src="https://github.com/user-attachments/assets/6b1435d8-fd2d-4f3e-85a0-3a846a9c4899" />


- Log out of Jane_admin on Client-1 and "attempt" to log into Client-1 with any of the domain users we created in our last lab, using the wrong password 5 times, to effectively get locked out of the account.
  - You can use the same account you used in the last lab if you have the credentials saved for ease of access, or navigate to Active Directory Users and Computers > mydomain.com > _EMPLOYEES on DC-1 to observe your users.
  - Again, as a reminder, the default password for each of our users is Password1, but your user's account names will be different than what I used above.

 <img width="700" height="700" alt="Lockout policy verification" src="https://github.com/user-attachments/assets/6372fcf5-bb4f-4d3f-8733-159681a7b626" />

- Once you've entered an incorrect password into the logon screen 5 times and received this error message, you can be sure that you've successfully configured your Account Lockout Policy.


<img width="700" height="700" alt="Find ADUC" src="https://github.com/user-attachments/assets/8c63c77e-47ea-4a5b-a44e-4909129abf0c" />

- We are now going to go back into DC-1 and resolve the issue for the Domain User. You should still be logged into DC-1 as Jane_admin, but if you not do so and open up Active Directory Users and Computers.
- Once you open up Active Directory Users and Computers from within DC-1, you can simply right-click on mydomain.com and click on Find.

<img width="auto" height="auto" alt="properties" src="https://github.com/user-attachments/assets/81924564-6216-4d7b-abc0-ddd9cedd8a5d" />


- Once you locate your locked-out user, you can simply double-click on their profile and you will be brought to the users properties.
- Click on Account within the user's properties.

<img width="auto" height="auto" alt="Account properties" src="https://github.com/user-attachments/assets/7550f188-330e-43f7-ab79-0d5d031f1dce" />

- You will notice that the account is currently locked out. As the administrator you have the option to unlock the account.
- Check the box that says unlock account, and hit apply.

<img width="auto" height="auto" alt="retry the login" src="https://github.com/user-attachments/assets/61e0fdfd-66aa-4872-9af5-d30b79f7c01d" />

- Now, go back to the Client-1 log in and attempt to login to Client-1 with the user you just unlocked using the correct password and you should be able to log in just fine!


<img width="auto" height="auto" alt="reset if necessary" src="https://github.com/user-attachments/assets/c73f0ae3-779d-4c7a-92a1-7c69839e7633" />


- When you search for your user on DC-1 in the Find section of Active Directory Users and Computers, instead of double-clicking on the user, you can right-click and, from there, you have the option to reset the user's password as well as unlock it if necessary.
- You will notice there are plenty of other things we can do from there such as disable the account, add them to a group, and more all from within Active Directory Users and Computers on the domain controller.


---

## Conclusion

In this lab, we configured and tested an Account Lockout Policy using Group Policy, then unlocked and managed a user account through Active Directory Users and Computers. This demonstrated how administrators can enforce security standards, troubleshoot account issues, and directly manage domain users.  

While this lab focused on lockout thresholds and account recovery, ADUC offers a wide range of administrative capabilities—from resetting passwords and disabling accounts to managing groups and permissions. Exploring these features is highly encouraged to build a deeper understanding of Active Directory administration and account management!  

**Reminder:** When you are finished with this lab, be sure to pause your virtual machines in Azure to avoid unnecessary costs. We will continue to use DC-1 and Client-1 in the next lab, so do not delete them. Just stop them until you’re ready to continue on to the next lab! 








 

 
 







---

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

