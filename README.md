# JD Edwards Lift and Shift / Functional User Guide Workshops

  ![](images/CloudSolutionHubs.png)
  
  
**Welcome to the JD Edwards Lift and Shift Workshop and JD Edwards General User Guide. This workshop will walk you through the process of how to lift and shift your current JD Edwards environment into the cloud.** 

## Table of Contents
1. [ Prerequisites. ](#Prerequisites)
2. [ Generating Secure SHell (SSH) Key Pairs on Your Local System. ](#SSH)

![](images/oraclecode/youtube.png)


<a name="Prerequisites"></a>
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

### Acquire an Oracle Cloud Trial or Workshop Account

- Bookmark this page for future reference.

- Please click on the following link to create your <a href="https://cloud.oracle.com/tryit" target="_trial">Free Account</a> and complete all the required steps to get your free Oracle Cloud Trial Account. When you complete the registration process you'll receive a $300 credit that will enable you to complete the lab for free.  Additionally, you'll have 1000s of hours left over to continue to explore the Oracle Cloud.
  ![](images/Trail.png)
  
> NOTE: You may proceed to the section below if you already have the access and credentials.

Before You Begin
----------------

This 15-minute tutorial shows you how to generate instance SSH key pairs in openssh format on your local system, which can be UNIX or Windows. Key pairs in this format are required if you need to connect directly to any Linux instance.

Best practice is to generate two sets of keys pairs:

-   **Key pair for access to the Bastion host.** This key pair is use for production purposes to access the Bastion host which in turn securely connects to all the other servers in the JD Edwards EnterpriseOne environment deployed by Infrastructure Provisioning. **Tip:** For organizational purposes, you should give these keys a significant name tying them to their use, like Bastion.pub and **Bastion.ppk**.
-   **Key pair for access to all hosts created by Infrastructure Provisioning except the Bastion host.** The use case for such connections are not for production purposes; for example these would be required in cases where Troubleshooting an instance might be necessary. Tip: For organizational purposes, you should give these keys a significant name tying them to their use, like **OCI_Instance.pub** and OCI_Instance.ppk.

### Background

JD Edwards EnterpriseOne Infrastructure Provisioning uses multiple methods of securely connection to Oracle Cloud Infrastructure, where "key pairs" means a Public Key and a Private Key:

1.  **Instance Key Pair.** Secure Shell (SSH) provides an encrypted login method that is a more secure replacement for Telnet for logging on to Oracle Cloud Infrastructure. Before you can use Infrastructure Provisioning to create instances, you must generate **Instance Key Pairs** and upload the SSH Public Key to Oracle Cloud Infrastructure. This SSH Public Key is used for authentication for any Oracle Cloud Infrastructure instance except the Bastion Server. The generation of this key pair is described in this section of this Learning Path entitled: ***Generating Instance Key Pairs in openssh Format***.

2.  **Bastion Host Key Pair**. This key pair is similar to **Instance Key Pairs** but are strongly recommended as best practice for the highest level of security. That is, you should the same procedure to create a different set of **Bastion Host Key Pairs** for public production access to the Bastion host, while keeping access to other host instances securely separated. The generation of these keys is described in this section of this Learning Path entitled: ***Generating Instance Key Pairs in openssh Format***.
3.  **Infrastructure Provisioning User Key Pair**. Instead of SSH key format, this key pair must be generated in Privacy Enhanced Mail (PEM) container format. The Public key of this key pair must be added to the account for the Infrastructure Provisioning User. When this Public key is uploaded, the system automatically creates a fingerprint that is displayed in the console of Oracle Cloud Infrastructure and is required for input into the Infrastructure Provisioning Console. In order to enable provisioning in Oracle Cloud Infrastructure, the Private key of this key pair is required as an input in the Infrastructure Provisioning Console.. The generation of this key pair, along with associated functions, are described in the section of this Learning Path entitled: ***Configuring a User for Infrastructure Provisioning***. 
4.  **CA Certificates.** You must generate CA certificates in order to support Load Balancing as a Service (LBaaS), which is core functionality that is deployed and configured by JD Edwards EnterpriseOne Infrastructure Provisioning. These certificates are used to configure LBaaS with SSL.  The procedure is described in the section of this Learning Path entitled: ***Generating CA Certificates for Load Balancing as a Service (LBaaS***). 

**Tip:** Best practice is to create at least two SSH key pairs for each purpose, because if for any reason a single SSH Key is no longer valid, access to the server would be lost permanently with no means to recover. There is no access to the server without using an SSH Key. Additional keys can be added manually after the instance is started.

**Warning:** Use caution if prompted to overwrite a previously generated SSH Key. If you overwrite a key previously used to connect to a prior Oracle Cloud Infrastructure instance, you may permanently lose access to (that is, the ability to log in to) any prior Oracle Cloud Infrastructure instance that used that key.

### What Do You Need?

Depending on your systems, you will need to create SSH key pairs either on a UNIX local system or on a Microsoft Windows local system.

-   **UNIX Local Systems**. If you are generating he **ssh-keygen** utility is required for generating SSH key pairs that you will use to connect to Oracle Cloud Infrastructure Compute Classic. Many UNIX installations already include ssh-keygen. Run the ssh-keygen command to verify that your installation has this utility; otherwise, you may obtain OpenSSH from this link:

    <http://www.openssh.com/portable.html>

    **Note:** All references to UNIX also apply to Linux.

-   **Microsoft Windows Local Systems.** The PuTTY key generator is required for generating SSH key pairs. The utility is available at this link:

    <http://www.putty.org>

* * * * *

<a name="SSH"></a>
![section 1](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/img/32_1.png)Generating Secure SHell (SSH) Key Pairs on Your Local System
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Secure SHell (SSH) provides an encrypted login method that is a more secure replacement for Telnet for logging on to the JD Edwards One-Click Provisioning Server on the Oracle Cloud Infrastructure. Before you create your Oracle Cloud Infrastructure instance, you must generate SSH key pairs and upload the SSH public keys to Oracle Cloud Infrastructure. These SSH public keys will be used for authentication when you log in to the instance. You must also create pairs of private keys, one pair for use by the One-Click Provisioning Server to create instances for JD Edwards EnterpriseOne servers and another pair to enable access to the instances. Below is a summary of the required SSH keys and their formats:

**Note:** You cannot set a passphrase for any SSH key (for example, provisioning user keys, Oracle Cloud Infrastructure instance keys, or Bastion Server keys).

-   **Public Key in OpenSSH Format**\
    Required when creating an instance for the Provisioning Server instance.

    See Step 4 in the following procedure.

-   **Private Key in OpenSSH Linux/UNIX Format**\
    Required as an input value to the One-Click Provisioning Console which uses the SSH keys to create instances for JD Edwards EnterpriseOne servers.

    See Step 5 in the following procedure.
-   **Private Key in .ppk Microsoft Windows Format**\
    Required to connect from a Microsoft Windows machine to an Oracle Cloud Service instance including the Provisioning Server itself and also to connect to any provisioned server such as DBCS, Enterprise Server, and JCS servers (such as HTML and AIS servers).

    See Step 6 in the following procedure.

1.  Locate and run **puttygen.exe** in the PuTTY folder of your local Microsoft Windows computer.
2.  On PuTTY Key Generator, accept the default key type, **SSH-2 RSA**, and in the **Number of bits in a generated key:** field, ensure the value is set to **2048**.
3.  Click the **Generate** button.

    ![PuTTY Key Generator ](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/img/PuTTY_Key_Generator.jpg)

    [PuTTY Key Generator](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/files/PuTTY_Key_Generator.txt)

    After you have clicked the **Generate** button, move your mouse around the blank area to generate randomness for the SSH key pair you generate.

    ![name](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/img/PuTTY_Key_Generator_Generate.jpg)

    [PuTTY Key Generator](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/files/PuTTY_Key_Generator_Generate.txt)

4.  Use this step to create a Public Key in OpenSSH Format.

    1.  In the PuTTY Key Generator dialog, select all the characters in the **Public key for pasting into OpenSSH authorized_keys file** field.\
        **Note:** Be sure you select all the characters, not just the ones you can see in the narrow window. If a scroll bar appears next to the characters, scroll through the entire window to select all the characters.
    2.  On the selected text, right-click to show the context menu and select **Copy**.

        ![name](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/img/PuTTY_Key_Generator_Public_Key.jpg)

        [PuTTY Key Generator - Public Key](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/files/PuTTY_Key_Generator_Public_Key.txt)

    3.  Open a plain text editor (such as vi on UNIX or Notepad on Microsoft Windows) and paste in the characters you just copied. Ensure that you paste the text at the first character in the text editor, and do not insert any line breaks.
    4.  Save the plain text file as a file name with a .pub extension and keep a record of the file name.

        **Tip:** As mentioned in the ***Before You Begin*** section of this task, for organizational purposes, you should give these keys a significant name tying them to their use, like **Bastion.pub** for the Bastion server and OCI_Instance.pub for Oracle Cloud Infrastructure instances.

        **Note:** The key saved in this step will save the first key of a key pair as recommended in the preceding\
        **Tip** just prior to the first step of this procedure.

    5.  Click the **Save public key** button to save the key to a file.

        **Tip:** You may give the file for the key any extension, but .pub is a useful convention to indicate that this is a public key.

        **Note:** The key saved in this step will save a second key of a key pair as recommended in the preceding **Tip** just prior to the first step of this procedure.

    6.  Keep a record of the file name and location which you will need when you upload this key when you create an instance and for other purposes as well.
    7.  Repeat this step to create another key pair, where one key pair will be for accessing the Bastion host, and the other key pair will be for accessing all other Oracle Cloud Infrastructure instances by tunneling through the Bastion host.
5.  Use this step to create a Private Key in OpenSSH Linux/UNIX Format.

    1.  In the PuTTY Key Generator dialog, from the menu bar, select Conversions > Export OpenSSH key.

        ![name](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/img/conversions_export_openSSH.jpg)

        [PuTTY Key Generator - Conversions > Export OpenSSH Key in Linux/UNIX Format](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/files/conversions_export_openSSH.txt)

    2.  On PuTTYgen Warning, click the **Yes** button to confirm you want to create the Private Key without a passphrase.

    ![PuTTY Key Generator ](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/img/no_passphrase.jpg)

    [PuTTY Warning - Click No](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/files/no_passphrase.txt)

    4.  Keep a record of the file name and location, which you will need when you upload this key as prompted by the One-Click Provisioning Console.

        **Tip:** As mentioned in the ***Before You Begin*** section of this task, for organizational purposes, you should give these keys a significant name tying them to their use, like **Bastion.openssh** for the Bastion server and OCI_Instance.openssh for Oracle Cloud Infrastructure instances.

1.  Use this step to create a Private Key in .ppk Microsoft Windows Format.

    1.  In the PuTTY Key Generator dialog, click the **Save private key** button to save your private key to the system.
    2.  The **Key comment** is the name of the key. You may keep the generated key comment or create your own.
    3.  Do not enter a **Key passphrase**.
    4.  To save the private key in the PuTTY Private Key (PPK) format, click the **Save private key** button.\
        **Note:** The PuTTY Private Key (PPK) format works only with the PuTTY toolset.

    ![PuTTY Key Generator ](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/img/PuTTY_Key_Generator_Save.jpg)

    [PuTTY Key Generator](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/files/PuTTY_Key_Generator_Save.txt)

    6.  On PuTTYgen Warning, click the **Yes** button to confirm you want to create the Private Key without a passphrase.

        ![PuTTY Key Generator ](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/img/no_passphrase.jpg)

        [PuTTY Warning - Click No](https://docs.oracle.com/en/applications/jd-edwards/tutorial-generate-ssh-keypair_terra/files/no_passphrase.txt)

    7.  Keep a record of the file name and location which you will need when you upload this key from a Microsoft Windows machine that is accessing the JD Edwards EnterpriseOne One-Click Provisioning Server and any JD Edwards EnterpriseOne server that it has deployed.

        **Important:** The file name you specify for this Private Key must have a .ppk extension.\\
        **Tip:** As mentioned in the ***Before You Begin*** section of this task, for organizational purposes, you should give these keys a significant name tying them to their use, like **Bastion.ppk** for the Bastion server and **OCI_Instance.ppk** for Oracle Cloud Infrastructure instances.
    8.  Repeat this step to create another Private key pair, where one key pair will be for accessing the Bastion host, and the other key pair will be for accessing all other Oracle Cloud Infrastructure instances by tunneling through the Bastion host.
