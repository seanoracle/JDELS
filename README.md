# JD Edwards Lift and Shift / Functional User Guide Workshops

1. [ Description. ](#desc)
2. [ Usage tips. ](#usage)

<a name="desc"></a>
## 1. Description

sometext

<a name="usage"></a>
## 2. Usage tips


  ![](images/CloudSolutionHubs.png)

Welcome to the JD Edwards Lift and Shift Workshop and JD Edwards General User Guide. This workshop will walk you through the process of how to lift and shift your current JD Edwards environment into the cloud. 

The JD Edwards General User Guide will walk you through general walkthroughs on how to do functional tasks and setups.


To learn more about this workshop please watch the video below.

![](images/oraclecode/youtube.png)

<a href="https://youtu.be/" target="_video">Workshop Overview(InProgress)</a>

## Prerequisite Tools and Resources

The PuTTY tool (http://www.putty.org) for generating SSH key pairs on the client machine that you will use to connect to any Linux server deployed by One-Click Provisioning.

The table below specifies the minimum Oracle Cloud Infrastructure resource requirements to install and run JD Edwards. Your environment may require additional resources based on transaction volumes, number of users, availability requirement, integrations, and business requirements.

## Understanding Port Restrictions

You should be aware of restricted ports that cannot be defined or used while creating any web component and/or server. These specific port restrictions for any One-Click Provisioning deployment of JD Edwards EnterpriseOne are grouped as follows:
* One-Click Provisioning Console for JD Edwards
* All Internet Browsers
* Google Chrome and Mozilla Firefox Browsers

### One-Click Provisioning Console for JD Edwards
Any port below 1024 is restricted.

### All Internet Browsers
The following are restricted ports enforced by the rules of any internet browser:
* 2049
* 4045
* 6000

### Google Chrome and Mozilla Firefox Browsers
In addition to the above mentioned restricted ports for any internet browser, the Google Chrome and Mozilla Firefox browsers block specific ports which they deem as unsafe to use on HTTP/HTTPS protocol. Below are these restricted ports:
* 3659, // apple-sasl / PasswordServer
* 6665, // Alternate IRC [Apple addition]
* 6666, // Alternate IRC [Apple addition]
* 6667, // Standard IRC [Apple addition]
* 6668, // Alternate IRC [Apple addition]
* 6669, // Alternate IRC [Apple addition]

### **Step 1**: Acquire an Oracle Cloud Trial or Workshop Account

- Bookmark this page for future reference.

- Please click on the following link to create your <a href="https://cloud.oracle.com/tryit" target="_trial">Free Account</a> and complete all the required steps to get your free Oracle Cloud Trial Account. When you complete the registration process you'll receive a $300 credit that will enable you to complete the lab for free.  Additionally, you'll have 1000s of hours left over to continue to explore the Oracle Cloud.
  ![](images/Trail.png)
  
> NOTE: Soon after requesting your trial you will receive the following email. _You may begin working on Lab 100 before you receive this email_, but you will not be able to start Lab 200 until you have received it.


### **Step 2**: Navigate to [LabGuide100](https://github.com/OracleCPS/End-to-end-API-Workshop/blob/master/workshop/LabGuide100.md): import your data on Apirary

- _You can see a list of Lab Guides_ by clicking on the **Menu Icon** in the upper left corner of the browser window. You're now ready to continue with [LabGuide100](https://github.com/OracleCPS/End-to-end-API-Workshop/blob/master/workshop/LabGuide100.md)

### **Step 3**: Navigate to [LabGuide200](https://github.com/OracleCPS/End-to-end-API-Workshop/blob/master/workshop/LabGuide200.md): create Gateway by using OCI instance and API Platform Cloud
- The step by step installation instructions are found here, and you can follow them to install your gateway on Linux. After you finish this lab, your gateway is created and ready to use. 
 
  
### **Step 4**: Navigate to [LabGuide300](https://github.com/OracleCPS/End-to-end-API-Workshop/blob/master/workshop/LabGuide300.md): create and configure the API and deploy it to gateway
- This is the last step before your API is ready to use. In Lab 300, you will be able to create a API on APIPC, configure it with Apirary from Lab 100, and deploy it to the gateway you created in Lab 200. 

Now, your API is able to use with your business need. You may also wanna setup some security policies to have some restrictions on the use of your API. No worries, please refer to Lab 400 (coming soon) and APIPC cover you by simply clicking!


