# Provision an Instance

## Introduction

This lab walks you through the steps to preparing the Windows compute instances for running Hyperion on OCI. We will be creating shared drive to be accessed across all the compute instances, download all the required tools, and the HFM installation files from e-delivery. 

Estimated Lab Time: 40 minutes

### Objectives

In this lab, you will:
* Create Block volume 
*	Mount and Attach (Have to try using paravirtualized instead)
*	Download required files on shared drive and make sure all compute boxes are able to access it. 
a.	SQL Developer
b.	Notepad ++
c.	All HFM installation from edelivery
d.	Firefox ESR

### Prerequisites

* An Oracle Free Tier, Always Free, Paid or LiveLabs Cloud Account
* Tenancy Admin User
* Tenancy Admin Password

## **STEP 1**: Download the resource manager package 

Go the URL and download the hyperion.zip folder from this link - HERE. (add pre-auth request here)

## **STEP 2:** Create OCI infrastructyre using terraform configuration file

1.	Login to OCI

2.	Go to Menu -> Compute

3.	Go to Menu -> Resource Manger -> Stacks

4.	Click on Create Stack
 
5.	Browse or drop terraform configuration file created in section 1. Provide the name and description. Select a compartment.
 
6.	Click Next. Provide a public SSH key. Select the Availability Domain

7.	Select an EPM Application
 
In this case we have selected Financial Management
Select Number of Nodes for an application
Select Instance Shape, Volume Size and Volume performance.

8.	Select the Number of Instance shape Volume Size and Volume performance for the Foundation

9.	Select Create EPM Database

Provide the required details

Select the DB Node, Shape and DB Size. 

10.	Select the Web Server Configuration

11.	Load Balance Configuration

12.	Click Next 
 
Go through the summary of the selection and confirm your selection
13.	Click on Create

14.	Click on Terraform Actions -> Plan

15.	Click on Plan

Notice that Plan is in progress.
Once the Plan Succeeded
 
16.	Go back to Stack Details 

Notice that you plan is listed in succeeded status.

17.	Click on Terraform Actions -> Apply
 
18.	Click on Apply

Plan will be in Accepted state

Plan is in progress

19.	Once it completes, Apply state will be succeeded and all the instance will have assigned host, ips , user and password.

You can click on the Outputs option under Resources on the left pane. Record all the IPs and default passwords for the compute instances. 

You may proceed to the next lab.


## Acknowledgements
* **Author** - Mitsu Mehta, Cloud Engineering
* **Contributors** - Rojal Bhadke, Software Development Director, EPM Consolidation
* **Last Updated By/Date** - Mitsu Mehta, Cloud Engineering, December 2020

## See an issue?
Please submit feedback using this [form](https://apexapps.oracle.com/pls/apex/f?p=133:1:::::P1_FEEDBACK:1). Please include the *workshop name*, *lab* and *step* in your request.  If you don't see the workshop name listed, please enter it manually. If you would like us to follow up with you, enter your email in the *Feedback Comments* section.



Pre-requisites –
a.	Ports opening
A.	Setting up a shared drive on the foundation server. 
1.	Create a shareable block volume on OCI. Login to OCI -> Click on left hamburger menu -> Block Storage -> Block Volume. 
2.	Click on Create Block Volume. 

 
3.	Enter the name for the block volume – EPMSharedDrive. Leave all the other settings to default and click on Create Block Volume. 
 

4.	Once the volume is created, click on Attached Instances under the Resources heading, click on Attach to Instance. Select ISCSI under Attachment Type. Select Read/Write – Shareable under Access Type. 

5.	Check the checkbox – 
I understand that data might become corrupted if the volume is used before a clustered file system is installed and configured.
6.	Select the instance – epmfndash11 from the dropdown and click on Attach. 
 

7.	Repeat this step of attaching the block volume for the other two instances – epmwebash11, epmhfmash11
 

8.	After mounting the shared drive on all three instances, you will have to login to all the three Windows compute boxes individually, as done on previous lab, and connect the volume to the instances. To attach the block volume to the compute instance, follow the steps –
a.	Open the navigation menu. Under Core Infrastructure, go to Compute and click Instances. 
b.	Click your instance name to view the instance details.
c.	In the Resources section, click Attached Block Volumes.
d.	Click the Actions icon (three dots) next to the volume you just attached and then click iSCSI Commands and Information. The iSCSI Commands and Information dialog box opens. Notice that the dialog box displays specific identifying information about your volume (such as IP address and port) as well as the iSCSI commands that you can use.
e.	On your Windows instance, open the iSCSI Initiator - Open Server Manager, click Tools, and select iSCSI Initiator.
 

f.	In the iSCSI Initiator Properties dialog box, click the Discovery tab. Click Discover Portal.

 
g.	Enter the block volume IP address retrieved from the console in previous step and port. Click OK.
 

h.	Click the Targets tab. In the Discovered Targets region, select the volume IQN.
 
i.	Click Connect and then click OK to close the dialog.
 
 
j.	You are now ready to format (if needed) and mount the volume. To get a list of mountable iSCSI devices on the instance, in Server Manager, click File and Storage Services and then click Disks.
 

 
k.	You will now see the 1.00 TB driver that we have just mounted on the list.

 

l.	Right click on the drive and click on New Volume.  
m.	Select the disk from the list and click on Next. And click OK on the dialog box.
 
 
n.	Leave the settings to default on the size screen.  Click on Next.
 
o.	Assign a Drive letter on the prompt.
 
p.	Click Next. Choose the file system as NTFS and assign a Volume label as EPMSharedDrive and click on Next.
 
q.	On the confirmation page, make sure all the settings are correct and hit create button. 


 
r.	Once all the processes are completed successfully, click on close button.  			
 


s.	You can confirm the drive is mounted by checking the folders in your file explorer. Repeat this exercise for the other Windows instance of web and app tier.
 

NOTE: - The steps to create, attach, and connect to the block volume is given at the URL - https://docs.cloud.oracle.com/en-us/iaas/Content/GSG/Tasks/addingstorageForWindows.html

B. Create EPM service user
•	Service account will be required since HFM and Foundation are on different servers 
•	 Assigning rights to “epmservice” user (Administrators group and the rights - Act as part of the OS, Bypass Traverse Checking, Log on as a batch job, and Log-on as a service)
1.	Go to your Foundation Windows instance. Open Start -> Server Manager.
 
2.	Click on Tools -> Computer Management.
 



3.	From the left pane window, under Local Users and Groups, right-click and click on New User to add a user.
 
4.	Add new user with the following details –
a.	User name – epmservice
b.	Description – EPM service account
c.	Password – Welcome#1234 (confirm the password)
5.	Click on Create button. 
  
6.	Once the user is created, double click on the epmservice user.
  
7.	You will see Users group is added by default. Select Users group and click on Remove to remove the access of User rights.
  
8.	Click on Add to add a new user group. In the Enter the object names dialog box, enter – ADMINISTRATORS. Click on OK.
 
9.	Click on Apply and OK. Close this window.
 

10.	From the start window, open MMC. 
 
11.	Click on File -> Add/Remove Snap-in
 
12.	Select Group Policy Object and click on Add. 
 
13.	You will see Local Computer Policy added under Selected snap-ins. Click on OK.
 
14.	From the left pane, Expand Computer Configuration, expand Windows settings, select Security settings.
 
 
15.	Under Local Policies, select User Rights Assignment.
 
16.	Double-click “Log on as a service” from the list of services. 
 
17.	Click on Add User or Group..
 

18.	Enter epmservice in the object names text area and click on OK.
 
19.	Click on Apply and click on OK.
20.	Assign following rights for epmservice user in the similar manner: 
	Act as part of the OS
	Bypass Traverse Checking
	Log on as a batch job
	Log-on as a service
C. Database setup

Objective:
•	Creating database users and tablespaces
•	Alter parameters
Step 1 – Login to the database. 

a.	SSH into your Linux bastion host on public subnet. 
1. You will need the IP address of your Linux bastion host from OCI console. 
 
2. Open a terminal window and type the following command. 
ssh -i <path_of_your_ssh_private_key> opc@<public_ip_address>

e.g. ssh -i /Users/local/Desktop/sshkeybundle/privateKey opc@193.122.148.251

3. Once you are logged in to the compute instance, we will now connect to the database. 

D. Disable UAC 

Login to all 3 Windows compute boxes and follow the following steps – 

1. Open Control Panel ->  User Accounts

 



2. Click on User Accounts.

 



3. Click on Change User Account Control settings.

 

4. Drag the slider to NEVER NOTIFY and click on OK.

 

5. Restart the compute from Start window -> Restart option.

6. You will also have to reboot the system from OCI console for the changes to reflect. 
 

Repeat these steps for all 3 compute instances. Refer the steps at the link -

https://docs.oracle.com/en/applications/enterprise-performance-management/11.2/hitis/disabling_user_access_control.html



