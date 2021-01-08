# Other Pre-requisites

## Introduction

This lab walks you through the steps for performing other pre-requisite steps before we can begin installing HFM, Foundation, and FDMEE packages on the Windows server. 

Estimated Lab Time: 40 minutes

### Objectives

In this lab, you will:

* Disable UAC
* Creating epmservice user and assigning privileges
* Firewall setup
* Installing SQL Developer, Firefox, Notepad++ on all three servers
* Edit the host files

### Prerequisites

a. Ensure that the shared drive is mounted on all three Windows system from the previous lab and that you are able to view all the downloaded files on all Windows servers.

*Note: All the following steps need to be performed on all three Windows servers one after the other. *

## **STEP 1**: Disable UAC

1. Login to the Windows server for foundation service at empfndash11 using Remmina on VNC viewer. (The private IP for this server should be 172.16.3.4)
2. Once you are logged in to the Windows server, select Start > Control Panel 
3. Click System Security
4. Under Action Center, choose Change User Account Control settings
5. Move the slider bar down to the Never notify selection and click OK
6. Reboot the machine for changes to take effect.

## **STEP 2**: Creating epmservice user and giving it the access rights

### Part 1 - Create user and add to Admin group

1. From start menu, search for Server Manager and run it as an admin. 
2. Click on Tools from right top corner -> Click on Computer Management.
3. From the left pane, expand Local Users and Groups -> Right-click Users and select New User.
4. Enter the user name as **epmservice** and the Description as - **EPM Service Account**
5. Check only the option - Password never expires.
6. Setup the password as - **Welcome#1234** and click on Create.
7. From the list of users, select the user you just created - **epmservice**.
8. Right click on the user and click on Properties.
9. From the tabs on the prompt, select **Member Of** tab.
10. By default, the epmservice user is part of Users group. Select this and click on the remove button to remove the user from Users group.
11. Now click on **Add** button. In the dialog box that appears, under the **Enter the object names to select**, enter **ADMINISTRATORS** and click on OK.
12. Click on Apply. Click on OK.

### Part 2 - Assign roles to the user

1. From the start menu, search for MMC. Right-click and open as an admin.
2. Click on File option and select Add/Remove Snap-in.
3. Select **Group Policy Object** from the Available snap-ins and click on the Add button.
4. Keep the Group Policy Object as **Local Computer** and click on Finish.
5. Click on OK.
6. Now on the dialog, under **Console Root** on the left pane, under Local Computer Policy -> Windows Settings -> Click on Security Settings
7. On the Right side pane, click on **Local Policies** from the list. 
8. Select **User Rights Assignments** and select Act as part of the Operating System from the list of policies.
9. Click on Add User or Group. Enter the object names to select - **EPMSERVICE**.
10. Click on Apply and OK.

Repeat this for the following policies - Bypass Traverse Checking, Log on as a batch job, and Log-on as a service.
 
## **STEP 3**: Disable firewall

## **STEP 4**: Installing SQL Developer, Firefox, Notepad++ on all three servers

1. From the shared drive, access the installers for SQLDeveloper, Notepad++, and Firefox. 
2. Run the installers to install the three tools.

## **STEP 4**: Edit the host files

1. On you File Explorer, go to the path -> C:\Windows\System32\drivers\etc
2. Open the host file with Notepad ++ and add the following lines and save the file. 

```
172.16.2.2 epmwebash11 epmwebash11.dbsubnet.epmvcn.oraclevcn.com
172.16.3.4 epmfndash11 epmfndash11.dbsubnet.epmvcn.oraclevcn.com
172.16.3.5 epmhfmash11 epmhfmash11.dbsubnet.epmvcn.oraclevcn.com
```

3. Close the file.  

## Acknowledgements
* **Author** - Mitsu Mehta, Cloud Engineering
* **Contributors** - Rojal Bhadke, Software Development Director, EPM Consolidation
* **Last Updated By/Date** - Mitsu Mehta, Cloud Engineering, December 2020

## See an issue?
Please submit feedback using this [form](https://apexapps.oracle.com/pls/apex/f?p=133:1:::::P1_FEEDBACK:1). Please include the *workshop name*, *lab* and *step* in your request.  If you don't see the workshop name listed, please enter it manually. If you would like us to follow up with you, enter your email in the *Feedback Comments* section.
