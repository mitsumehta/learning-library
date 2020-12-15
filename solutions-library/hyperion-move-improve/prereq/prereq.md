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
6. Reboot the machine for changes to take effect

## **STEP 2**: Creating epmservice user and giving it the access rights

-	Creating epmservice user and giving it the access rights

## **STEP 3**: Disable firewall

## **STEP 4**: Installing SQL Developer, Firefox, Notepad++ on all three servers

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

