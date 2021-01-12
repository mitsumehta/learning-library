# Other Pre-requisites

## Introduction

This lab walks you through the steps for setting up the database for Hyperion on OCI. 

Estimated Lab Time: 50 minutes

### Objectives

In this lab, you will:

*	Accessing the DB
*	Set parameters on SQLnet.ora file
*	Set other system parameters
*	Create tablespaces, users, assigning access and rights
*	Set Autoextend property
*	RCU config

### Prerequisites

1. You need to have the private key of your ssh bundle on the Bastion host. Copy the private key file from your local computer to the Desktop of the Bastion host.
``
scp /Users/mimehta/Desktop/sshkeybundle/privateKey -i /Users/mimehta/Desktop/sshkeybundle/privateKey opc@193.122.148.251:/home/opc/Desktop
``
2. You will need the private IP address of the database instance. You can extract this information from the OCI console. 

a. Login to your OCI tenancy using your tenancy admin username and password. 
b. From the left hamburger menu, select Barametal, VM, Exadata under Oracle Database.
c. Navigate to the compartment where you have provisioned the resources for this workshop from the drop down menu. 
d. Select the database - epmdbash11 from the list of the database. 
e. From the left hand options, select Nodes and copy the private IP address as shown below. 
f. Make a note of this DB private IP address. 


## **STEP 1**: Accessing the DB

To access your database on the VM on private subnet, follow the steps given below - 

1. Login to the Bastion host as we did in the previous exercise - 

``ssh -i <path_of_the_private_key> opc@<public_IP_address>``

   *e.g. ssh -i /Users/mimehta/Desktop/sshkeybundle/privateKey opc@193.122.148.251*
   
2. Now we will login to the VM of the database using the privatekey we copied on the desktop as a pre-requistie of this lab. 

``sudo ssh -i <path_of_the_private_key> opc@DB_private_IP_address``

*e.g. sudo ssh -i /home/opc/Desktop/privateKey opc@172.16.4.2*

3. Now switch the user to oracle. 

``sudo su oracle``

4. Now lets login to the database using the SQL command as below to verify you can access the database using sql prompt - 

``sqlplus sys/WElcome#1234#@epmdbash11.dbsubnet.epmvcn.oraclevcn.com:1521/epmdb.dbsubnet.epmvcn.oraclevcn.com as sysdba``

5,. Type ``exit`` to get out of the sql prompt.

## **STEP 2**: Set parameters on SQLnet.ora file

1. Now you are going to edit the Sqlnet.ora file. In the command prompt logged in as oracle user, enter the command - ``cd $ORACLE_HOME``
2. You will be taken to **db_home1** folder. Now navigate to the following folder - ``cd network/admin``
3. Now edit the sqlnet.ora in the editor using the command - ``vi sqlnet.ora``
4. In the editor, enter the ``i`` key on your keyboard to get into the edit mode.
5. Add the following line to the end of the file - **max_string_size=standard** 
6. Hit escape and enter ``:wq!`` to save the changes and quit. 

## **STEP 3**: Set other system parameters

``
ALTER SYSTEM SET processes=2000 SCOPE=SPFILE;
ALTER SYSTEM SET OPEN_CURSORS=5000 SCOPE=SPFILE;
ALTER SYSTEM SET SESSION_CACHED_CURSORS=200 SCOPE=SPFILE;
ALTER SYSTEM SET SESSIONS=2000 SCOPE=SPFILE;
``

## **STEP 4**: Create tablespaces, users, assigning access and rights
## **STEP 5**: Set Autoextend property

## Acknowledgements
* **Author** - Mitsu Mehta, Cloud Engineering
* **Contributors** - Rojal Bhadke, Software Development Director, EPM Consolidation
* **Last Updated By/Date** - Mitsu Mehta, Cloud Engineering, December 2020

## See an issue?
Please submit feedback using this [form](https://apexapps.oracle.com/pls/apex/f?p=133:1:::::P1_FEEDBACK:1). Please include the *workshop name*, *lab* and *step* in your request.  If you don't see the workshop name listed, please enter it manually. If you would like us to follow up with you, enter your email in the *Feedback Comments* section.

