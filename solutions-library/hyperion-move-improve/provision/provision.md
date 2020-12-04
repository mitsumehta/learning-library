# Provision an Instance

## Introduction

This lab walks you through the steps to provision all the required resources for running Hyperion on OCI. We will use a resource manager zip folder to provision the resources. 

Estimated Lab Time: 40 minutes

### About Product/Technology
Enter background information here..

### Objectives

In this lab, you will:
* Download the zip folder for HFM installation on OCI
* Run resource manager to provision the environment

### Prerequisites

* An Oracle Free Tier, Always Free, Paid or LiveLabs Cloud Account

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


*At the conclusion of the lab add this statement:*
You may proceed to the next lab.

## Learn More

*(optional - include links to docs, white papers, blogs, etc)*

* [URL text 1](http://docs.oracle.com)
* [URL text 2](http://docs.oracle.com)

## Acknowledgements
* **Author** - <Name, Title, Group>
* **Contributors** -  <Name, Group> -- optional
* **Last Updated By/Date** - <Name, Group, Month Year>
* **Workshop (or Lab) Expiry Date** - <Month Year> -- optional, use this when you are using a Pre-Authorized Request (PAR) URL to an object in Oracle Object Store.

## See an issue?
Please submit feedback using this [form](https://apexapps.oracle.com/pls/apex/f?p=133:1:::::P1_FEEDBACK:1). Please include the *workshop name*, *lab* and *step* in your request.  If you don't see the workshop name listed, please enter it manually. If you would like us to follow up with you, enter your email in the *Feedback Comments* section.
