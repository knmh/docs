# How to Configure a Managed System using the LDAP Managed System

## Overview


This document provides step-by-step instructions for configuring the Managed System, specifically using the LDAP Managed System in OpenIAM that utilizes the LDAPS protocol.

-------------------------------------------------

## In this document we cover these topics.
 

**1.How to access OpenIAM** 
 
- 1.1 Find the IP address of OpenIAM 
- 1.2 Access the OpenIAM web console
- 1.3 Login as System Administrator

**2.How to configure managed system**
- 2.1 Access the Managed System 
- 2.2 Edit Managed System ( we chose AD Managed System )
- 2.3 Configure the necessary fields of a managed system 

**3.How to Install the LDAP Connector**
- 3.1 Start the connector
- 3.2 Reset connector
- 3.3 Running Connectors Status: `displayed in red`

**4.How to make a self-signed certificate?**
- 4.1 Accessing the Self-Signed Certificate in Active Directory
- 4.2 Refresh the Certificates System
- 4.3 Verifying Certificate Readability on using the LDAP Browser
- 4.4 Verifying Certificate Readability on Linux for OpenIAM
- 4.5 the private key associated with the certificate
- 4.6 Adding a Certificate to the Linux Trust Store

**5.How to create role?**
- 5.1 navigate to Create New Role
- 5.2 Configure the necessary fields to create new role

**6.How to create BusinessRules in OpenIAM?**
- 6.1 How to navigate to BusinessRules
- 6.2 define the target parameters
- 6.3 define the Business Rules parameters
- 6.4 Key Points About Business Rules

**7.How to provision?**
- 7.1 How to create a user in OpenIAM?
- 7.2 importance of assigning roles
- 7.3 verify if the user has been created in Active Directory by checking in OpenIAM
- 7.4 How to edit user details in OpenIAM
- 7.5 How can we determine the types of access that users have?
- 7.6 How can we get a comprehensive overview of all users?
- 7.7 verify if the user has been created in Active Directory by checking in Active Directory
- 7.8 How to Delete users in OpenIAM?

**8.Active Directory User Synchronization**
- 8.1 How to access the synchronization settings?
- 8.2 Validation Rule
- 8.3 Where is the log location of println?
- 8.4 Viewing the Log in Real-Time
- 8.5 Transformation Rule 
- 8.6 Viewing Synchronization History
- 8.7 Troubleshooting Sync Issues
- 8.8 Successful Synchronization
- 8.9 Editing the Active Directory Connector Script

**9.Differences Between AD Managed Systems and PowerShell Managed Systems**
- 9.1 Attribute Mapping Differences
- 9.2 PowerShell User Policy Configuration
- 9.3 LDAP User Policy Configuration


------------------------------------------------

## Prerequisites

**OpenIAM Installed:** Ensure OpenIAM is installed on your server.

------------------------------------------------

# 1.How to access OpenIAM

## 1.1 Find the IP address of OpenIAM 
 

To access OpenIAM via the web console, we need the IP address of the machine where OpenIAM is installed. This is crucial for entering the correct address in your web browser's address bar.

--------------------------------------------------

## 1.2 Access the OpenIAM web console

In your browser, enter `your IP address of OpenIAM + /webconsole`

For example: `192.168.1.139/webconsole`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nllvrxyfbyymfc9uyrtd.png)



--------------------------------------------------

## 1.3 Login as System Administrator

To gain the necessary permissions to modify all settings and configurations, you need to login as the `system administrator(sysadmin)`.

**note:**
The default password is usually 'passwd00', but you can change it to whatever you prefer.



![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zm58b630tjzab34s1ca9.png)


-------------------------------------------------------

# 2.How to configure managed system

## 2.1 Access the Managed System 

locate the **Provisioning tab** in the main menu.
Click on the **Managed System** section.

Here, we observed that some Managed System was already in place. 

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w9pbaf4pu50cyn7cx9qi.jpg)

---------------------------------------------------

## 2.2 Edit Managed System (we chose AD Managed System) 

In the list of managed systems, locate the **AD Managed System**.
In the action section next to it, click on **Edit**. This allows you to modify specific details of the managed system.




![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rtm3zrkna3eeupnw2818.png)




-------------------------------------------------

## 2.3 Configure the necessary fields of a managed system

### Parameter Details

**note:** 
In this section, the first four parameters are automatically filled, but you have the option to edit the description if desired.

**Connector :** `Refers to the specific connector used`. 
**Managed System Id :** `Represents the unique identifier assigned to the managed system`.
**Managed System Name:** `it refers to the name of managed system`.
**Description :** `Provide a detailed overview or relevant information about the managed system`.




![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ykwm6km153m2x98f83p0.png)




-----------------------------------------------------

### Required Options

To create a user and synchronize it with the managed system, ensure you activate the following three options.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/n5ox6zzdk9aozeeyf0rr.jpg)

### Active

**Description**: refers to a state where the managed system is performing tasks or operations.


### All users provisioned with this managed system

**Description**: refers to each user you create in OpenIAM who will automatically be provisioned with this specific managed system and connect to Active Directory.

**note:**
Provision: means that whenever you create a user, it is automatically added to the Active Directory and created without requiring manual intervention.

-------------------------------------------------

### Entering the Hostname or IP Address

In the **Host URL** field, you should enter the **LDAPs protocol**, (which is a secure protocol. This will ensure a secure connection between **OpenIAM** and **Active Directory**).

**note:**
It makes sure to use the domain name and the Active Directory machine name you want to connect to, rather than using a static IP address or including the IP in the URL.


**Example (based on our setup):** 
`ldaps://our Active Directory Machine Name(adds)  + .our Domain Component(saeigroup) + .our Network(local) `
**Host URL**:`ldaps://adds.saeigroup.local`


-------------------------------------------------

### Port Configuration

To configure the **LDAPS port**, ensure it is set to `636` for the connection. Additionally, make sure this port is open in firewall settings on the machines.

**Port:**`636`



-------------------------------------------------

### Password Policy

The **password policy** should be set to `Default pswd policy`.



-------------------------------------------------

### Communication Protocol

Set the **communication protocol** to `SSL`.


-------------------------------------------------

### Login ID and Password Setup


**note:**To fill in **Login ID**, you need access to **Active Directory Users and Computers**.

### Accessing Active Directory Users and Computers

- Login to your **Active Directory machine**.

- Press `Windows + R` .

- Type `dsa.msc` and press Enter.

This opens the **Active Directory Users and Computers console**.
CN = `Your common Name`
CN = `Your Container Name`
DC = `Your Domain Component`
DC = `Your Network`

You should replace each of these with the appropriate values from your **Active Directory Users and Computers console**.

Login ID : CN = Your common Name,CN = Your Container Name,DC = Your Domain Component,DC = Your Network


**Example (based on our setup):**

**Login ID :** `CN = Administrator,CN = Users,DC = Saeigroup,DC = local` 

**Password:**`administrator's Password of your Active Directory machine`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nl3bkoa2isb4kpb1ezhd.png)



----------------------------------------------------------

### Object primary key for the user


**object primary key for the user**: `cn`.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gxzqgwmk1b3z666ycbq5.png)

------------------------------------------------------------------

### Configure the Base DN for user and Search Base DN for user 

Search Base DN for user: `The place in Active Directory where OpenIAM looks for users to sync.`

Base DN for User: `Specifies the location in Active Directory where new user accounts will be created.`

**note:**
To fill in these two fields, you need access to Active Directory Users and Computers.

### Accessing Active Directory Users and Computers

- Login to your Active Directory machine.

- Press Windows + R .

- Type `dsa.msc` and press Enter.

This opens the **Active Directory Users and Computers console**.

You should replace each of these with the appropriate values from your Active Directory Users and Computers console.

OU = `Your Organizational Unit` 
DC = `Your Domain Component`
DC = `Your Network`

Base DN for user: OU = `Your Organizational Unit`,DC = `Your Domain Component`,DC = `Your Network`

Search Base DN for user: OU = `Your Organizational Unit`,DC = `Your Domain Component`,DC = `Your Network`

**Example (based on our setup):**

`OU=SaeiUsers`,`DC=Saeigroup`,`DC=local`

Base DN for user:`OU=SaeiUsers`,`DC=Saeigroup`,`DC=local`
Search Base DN for user:`OU=SaeiUsers`,`DC=Saeigroup`,`DC=local`


**notes:** DC=local indicating that it is internal network (based on our setup).


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hhklbi2bdnkcq428xgxv.png)


------------------------------------------------------------------------

### Search filter for user

**Search filter for user:** `(&(objectclass=user)(cn=?))`

**note:**
The LDAP command provided is designed to find user objects with a specific common name (cn).

--------------------------------------------------------------------------

### Downstream managed system


**Downstream managed system:**`OPENIAM`


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dwryo3bj9l16y1tbt507.png)



_Congratulations, your editing is complete and all required fields have been filled in. You can now click the Save button._


------------------------------------------------------------------------

### No active connectors found

In the **Management System Dashboard**, under the **Running Connectors Status** section, you may see the message:
`No active connector found`.

#### Cause:

This issue occurs because the connection to Active Directory has been configured in **OpenIAM**, but the required Active Directory connector has not been installed.

#### Solution:

To resolve this, you need to install the appropriate connector in your **OPenIAM** machine .


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vmlsics6nc2lehrnf8jv.jpg)


------------------------------------------------------------------------

# 3.How to Install the LDAP Connector

**note:** 
The LDAP connector needs to be installed in OpenIAM machine.


#### RPM File

First, download jar file into `/usr/local/openiam/connectors/bin` and change owner to openiam user.

```
wget https://download.openiam.com/release/enterprise/4.2.1.3/connectors/ldap-connector-rabbitmq.jar
chown openiam:openiam /usr/local/openiam/connectors/bin/ldap-connector-rabbitmq.jar
```

Next, create new `.sh` file for starting **ldap connector** by running:

```
nano ldap_start.sh
```

#### Content of the file

```
#!/bin/bash
. /usr/local/openiam/env.conf
export VAULT_CERTS="$HOME_DIR/vault/certs/"
export JAVA_HOME="$HOME_DIR/jdk"
export JAR_FILE="ldap-connector-rabbitmq"
export JAVA_OPTS="-Xmx256m -Djdk.tls.client.protocols=TLSv1.2"
su openiam -c "$JAVA_HOME/bin/java -Dlogging.level.root=ERROR -Dlogging.level.org.openiam=ERROR -Dconfpath=$HOME_DIR/ -Djavax.net.ssl.keyStorePassword=changeit -Djavax.net.ssl.trustStore=$HOME_DIR/conf/$JAR_FILE/ -jar $JAVA_OPTS $HOME_DIR/connectors/bin/$JAR_FILE.jar > $HOME_DIR/logs/$JAR_FILE.log&"
```

Make file executable by running:

```
chmod +x ldap_start.sh
```

## 3.1 Start the connector


To **start the connector**, use the following command:

```
./ldap_start.sh
```


--------------------------------------------------------------------------

## 3.2 Reset connector


- Navigate to the **Provisioning** tab


- Select the **Connectors** Tab


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1ilg3o5xla3clt7746zs.jpg)



- Locate the **LDAP Connector** 


- Click on the Edit button associated with the **LDAP Connector**.

 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jmweu0vc1ldi2uc0qceg.png)


- click on the **Save** button.


 **Note:** Saving will reset the connector.



### Open the Terminal on your OpenIAM machine.


- Type `systemctl status openiam-connector@ldap-connector-rabbitmq` and press Enter



```
systemctl status openiam-connector@ldap-connector-rabbitmq
```

**Example Output**(based on our setup status is active(running)).

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mj3rfl2z34jr19ae4dlj.png)


**note:**

but if you did not get this output you should run `systemctl start openiam-connector@ldap-connector-rabbitmq` in your cmd. 



```
systemctl start openiam-connector@ldap-connector-rabbitmq
```

**note:**
After run this command check the status with `systemctl status openiam-connector@ldap-connector-rabbitmq` and make sure you get active(running).


After completing all these steps, make sure to reset the connector in OpenIAM. Refer to the instructions provided earlier on how to perform this reset.


-----------------------------------------------------------------------

## 3.3 Running Connectors Status: `displayed in green`

After that, we need to check the **Running Connectors Status** so you should locate the **managed system dashboard**.


### locate the managed system dashboard


- locate the **Provisioning tab** in the main menu.

- Click on the **Managed System** section.


- In the list of managed systems, locate the **AD Managed System**.

When everything is functioning correctly,you should see the **Running Connectors Status** displayed in **green**.

-----------------------------------------------------------------------

## Running Connectors Status: `displayed in red`

But if you see the **Running Connectors Status** displayed in **red**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w6npmv9zatqqn9l56gzb.png)

#### Cause:
This error indicates that you cannot connect to **SSL**. Access is denied and there is no certificate to fix this problem. 


#### Solution:
LDAP requires a certificate to enable SSL for secure communication. When connecting systems, you need a **self-signed certificate** to establish this secure connection.


-------------------------------------------------------------------

# 4.How to make a self-signed certificate?

### Navigate to the Active Directory machine

- Login to your **Active Directory machine**.

- Press `Windows + R` on your keyboard.

- Type `cmd` and press Enter.

- Copy all these commands and past into `cmd` that runs as **an administrator**


## certificate commands

```
New-SelfSignedCertificate `
  -DnsName "adds.Saeigroup.local" `
  -CertStoreLocation "Cert:\LocalMachine\My" `
  -KeySpec KeyExchange `
  -KeyUsage DigitalSignature, KeyEncipherment `
  -NotBefore (Get-Date).AddMinutes(-5) `
  -NotAfter (Get-Date).AddYears(5) `
  -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1")

```

**Machine Full Name:** ` Type echo %logonserver% and press Enter the output is your Machine Full Name`

**Domain Component:**  `Your Domain Component`

**Network:** `Your Network`

**DnsName:** `Machine Full Name+Your Domain Component+Your Network`

**Example (based on our setup):**
 `adds.Saeigroup.local`

**NotBefore:**
This is the date and time when the certificate becomes valid.

**NotAfter:**
This is the expiration date and time of the certificate. 

note:
Ensure that both machines are set to the same **timezone**, and pay close attention to the details you input for the **NotAfter** and **NotBefore** fields.


------------------------------------------------------------------------


## 4.1 Accessing the Self-Signed Certificate in Active Directory


**note:** 
self-signed certificate is created in the specified path on the **Active Directory machine**.


### Navigate to the Console Root Certificates(local computer)

**note:**
 This is the console of all certificates in **Active Directory machine**.

- Login to your **Active Directory machine**.

- Press `Windows + R` on your keyboard.

- Type `mmc.exe` and press Enter.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v9bderighln3il8ssxey.png)

Navigate to: `Console Root > Certificates (Local Computer) > Personal > Certificates`.  

Here, you will find the self-signed certificate that has been created.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fptp7ofvopl53colcklm.png)

### not trusted 

If you click on that certificate, you can see an error that says its not trusted 



#### Solution:

- You need to **copy** the certificates.

- Navigate to the **Trusted Root Certification Authorities** section.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/18rbhqml9xc0qvot6tfd.png)

- In the **certificate folder**. 

- **Add** the self-signed certificate in here.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bb24k3xbtjgrs35r6lma.png)

 After completing these steps, you should notice that the script is recognized as trusted.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9ahp4t2cpd80sdyk63ou.png)

------------------------------------------------------------------------

## 4.2 Refresh the Certificates System

To refresh the certificates system we use two commands in `cmd` of **Active Directory machine**.


**Warning:**
When the command `net stop ntds` is executed, all login activities on the **Active Directory machine** will be interrupted."


```
net stop ntds
```

**it will ask:**
**Do you want to continue this operation? [Y/N]** 
You should type `Y` to confirm it.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2s989idpz897jc0t9k9d.png)

**Example Output:**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jiihxylhkfmv1qya2rwb.png)


after that we should run `net start ntds` command.

```
net start ntds
```

**Example Output:**


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d2wrlfap2h86s19blwbo.png)


-------------------------------------------------------------------

## 4.3 Verifying Certificate Readability on using the LDAP Browser

- Login to your **Active Directory machine**.

- Press `Windows + R` to open the Run dialog.

- Type `cmd` and press Enter.

- Type `ldp.exe` and press Enter.


```
ldp.exe
```


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7029gmijc151bzc1mn7g.png)

**Example Output:**

You should see the **LDAP Browser**, where you can set up the **LDAP connection**.

**note:**
You can connect to a different system using LDAP commands.

- locate the **connection tab** in the main menu.

- Click on the **connect section**.  

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jf1kgay83iictnbo1u86.png)

### Configure the connection section

**Server:** `localhost`
**SSL checkbox:** `Active`
**Port:** `636`
click on **ok**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ujtr6vf32duejgc8d94o.png)


There are no errors in this section.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/krr28vq2qhavz59tikf1.png)

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7b5szwdbynym9153pkcv.png)

As you can see, with `zero errors` and `an established connection to localhost` certificate is working and the **Active Directory** can use **LDAP communication** with it self.


-------------------------------------------------------------------

## 4.4 Verifying Certificate Readability on Linux for OpenIAM


- Login to your **Active Directory machine**.

- Press `Windows + R` to open the Run dialog.

- Type `cmd` and press Enter.


Before running the command, ensure you set the following values:

Your **Active Directory machine name**

Your **domain components** 

Your **network** 

- Type `openssl s_client -connect your Active Directory Machine Name+.your Domain Component Name+ .your Network Name:636 -servername adds.Saeigroup.local </dev/null` and press Enter.

**Example (based on our setup):**
`our Active Directory Machine Name(adds)  + .our Domain Component(saeigroup) + .our Network(local)`

```
openssl s_client -connect adds.Saeigroup.local:636 -servername adds.Saeigroup.local </dev/null
```
**Example Output:**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cb26u9coiq13vbyohkz9.png)

**verified return code:18** `means everything is okay`.
**(Self Signed Certificate)** `means the certificate is not official`.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ae5ypc97hs6voef8ef8d.png)

If you encounter this error
**Verification error:** `certificate is not yet valid`

**Cause:**

 it is likely due to a **mismatch in timezones**. 

**Solution:**

To resolve this issue, you should check and adjust the **notBefore** field in the certificate to ensure it aligns with the correct timezone.

-------------------------------------------------------------------

## 4.5 the private key associated with the certificate

The following image displays the **private key** associated with the certificate.

We should save this key to a separate file, as it will be needed later.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rzwuxxwvhqht0obbvuvs.png)

To save it to a file, you can use the following command.
Before running the command, make sure to set the following:

Your **Active Directory machine name**

Your **domain components** 

Your **network**

`echo | openssl s_client -connect your Active Directory Machine Name+.your Domain Component Name+ .your Network Name:636 | sed -n '/-----BEGIN CERTIFICATE-----/,/-----END CERTIFICATE-----/p' > ldap_server.crt`


**note:**
The name we chose is **ldap_server.crt**, but feel free to select any unique name.

**Example (based on our setup):**
`Active Directory Machine Name(adds)  + .our Domain Component(saeigroup) + .our Network(local)`

```
echo | openssl s_client -connect adds.Saeigroup.local:636 | sed -n '/-----BEGIN CERTIFICATE-----/,/-----END CERTIFICATE-----/p' > ldap_server.crt
```
---------------------------------------------------------------------

**note:**
To connect to a **Linux machine**, it is necessary to ensure that the **certificate** is added to the **truststore** of the system.

## 4.6 Adding a Certificate to the Linux Trust Store

**note:**
There are three possible locations to add the certificate based on your preferences. 

- Use own Java Development Kit (JDK)

- Operating system layer

- Use java version

**note:**
OpenIAM utilizes its own Java Development Kit (JDK), and there are two additional methods available.
If you want to add a certificate in OpenIAM, you can proceed by utilizing your own Java Development Kit (JDK). 




### Use own Java Development Kit (JDK)

Some systems do not use the operating system's Java version and instead use their own Java Development Kit (jdk).


 **you can find JDK in OpenIAM here:**

 `/usr/local/openiam/jdk/lib/security/cacerts`


proceed by executing the following commands.

```
sudo keytool -importcert \
 -trustcacerts \
 -alias adds-ldaps \
 -file ldap_server.crt \ 
 -keystore /usr/local/openiam/jdk/lib/security/cacerts\
 -storepass changeit \
 -noprompt
```

**alias:** `Please make sure the name you select,'adds-ldaps'(based on our setup) is unique to avoid any conflicts`.

**file:** `You should replace full path of your own SelfSignedCertificate.`

**keystore:**`replace address you want to install keystone in it.` 

**Example (based on our setup):**we Use Java Development Kit so we replace this 

address `/usr/local/openiam/jdk/lib/security/cacerts`

**storepass:**`use the password changeit.`

**note:**
please restart your **web console**  and check if everything is functioning properly.

### locate the managed system dashboard in OpenIAM

locate the **Provisioning** tab in the main menu.

Click on the **Managed System** section.

In the list of managed systems, locate the **AD Managed System**.

When everything is functioning correctly,you should see **the Running Connectors Status displayed** in **green**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/o2v0uydamu395mfc5lt4.png)


_Congratulations on successfully configuring the AD Managed System in OpenIAM ._

---------------------------------------------------------------

### operating system layer

To place the file named `ldap_server.crt`, you should navigate to the operating system layer in this direction.
`/etc/pki/ca-trust/source/anchors/`


proceed by executing the following commands.

```
sudo keytool -importcert \
 -trustcacerts \
 -alias adds-ldaps \
 -file ldap_server.crt \ 
 -keystore /etc/pki/ca-trust/source/anchors/
 -storepass changeit \
 -noprompt
```

**alias:** `Please make sure the name you select,'adds-ldaps'(based on our setup) is unique to avoid any conflicts`.

**file:** `You should replace full path of your own SelfSignedCertificate.`

**keystore:**`replace address you want to install keystone in it.` 
**Example (based on our setup)we Use operating system layer so we replace this address:**`/etc/pki/ca-trust/source/anchors/`

**storepass:**`use the password changeit.`

**note:**
please restart your system and check if everything is functioning properly.

------------------------------------------------
### Use java version

For each **Java version**, there is a designated location where all **keystores** and **truststores** are stored. 


**The certificate is placed at this location:**
` /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.392.b08-4.el8.x86_64/jre/lib/security/cacerts. `

**Example (based on our setup):**
This is a version of our certificate:`-openjdk-1.8.0.392.b08-4.el8.x86_64 You should replace it with your own version.`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gm395mq99onuxx4pil9f.png)


proceed by executing the following commands.

```
sudo keytool -importcert \
 -trustcacerts \
 -alias adds-ldaps \
 -file ldap_server.crt \ 
 -keystore /usr/lib/jvm/java-1.8.0-openjdk-*/jre/lib/security/cacerts \
 -storepass changeit \
 -noprompt
```
**alias:** `Please make sure the name you select,'adds-ldaps'(based on our setup) is unique to avoid any conflicts`.

**file:** `You should replace full path of your own SelfSignedCertificate.`

**keystore:**`replace address you want to install keystone in it.` 
**Example (based on our setup)we Use java version so we replace this address:**`/usr/lib/jvm/java-1.8.0-openjdk-*/jre/lib/security/cacerts`

**storepass:**`use the password changeit.`

**note:**
please restart your system and check if everything is functioning properly.

------------------------------------------

# 5.How to create role?
## Overview
 
This section provides step-by-step instructions for creating a role in OpenIAM. In our setup, we established an 'Active Directory Members' role.

**note:**
If the **Active Directory members role** is not specified or declared, provisioning will not occur successfully.

-----------------------------------------------------------------

## 5.1 navigate to Create New Role

- Navigate to the **Access Control** section

- Select the **Role** Tab

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nhggw6pe1m7visalgquw.png)

- click on **Create New Role**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3elasei1styn57eiys3g.png)

------------------------------------------------------------------

## 5.2 Configure the necessary fields to create new role


**Role type:** `Provision Role`
**the password policy:** `Default Pswd Policy`
**Role Name:** `Active Directory members`
**Role Description:** `The role is used to provision users to  Active Directory using LDAP managed system`



![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3dat7u0srrhkj6g7unsg.png)

------------------------------------------------------------------

**Role Managed System:** `AD managed system`
**Role status:** `Active`


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2mf533ppzj77egllbflk.png)



----------------------------------------------------------------

**Is Visible:** `The checkbox is ticked`
**Participate in Access Certification:** `The checkbox is ticked`
click the **Save** button to ensure everything is stored properly.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vsdb3f5mmc2qyr9dc6uh.png)

_Congratulations! The Active Directory Members role has been successfully created in the OpenIAM._

-------------------------------------------------------------------

# 6.How to create a business rules in OpenIAM?

## Overview
To ensure proper provisioning of users, we should implement a system where each user is automatically assigned a specific Managed System, such as "AD Managed System." This rule will be added to the user's profile upon creation. 

----------------------------------------------------------------------

**Prerequisites:**

If you haven't yet created the necessary **Active Directory members**, please follow the instructions (5.How to create role?) provided to do so. 

------------------------------------------------------------------------

## 6.1 How to navigate to BusinessRules

- Navigate to the **Access Control** section

- Select the **BusinessRules** Tab

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/n4ooaix7pqhjn5ail0am.png)

-------------------------------------------------

## 6.2 define the target parameters

To begin, we need to define the target parameters.

- click on the **Add Target**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h5ubiex0rfkkyzz5wgjl.png)

**Name:** `LDAP User Role (based on our setup)`
**Description:** `Please fill this with relevant LDAP role data`

**Active checkbox**:`ticked`
Then click on **Save**.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nr49jnxoaalnz4o87yl9.png)


## Configure the necessary fields

- **Right-click** on the LDAP User Role(based on our setup) and select **Add Action**


**Type:** `Add User to Role(based on our setup)`
**Roles:** `LDAP Managed System`
**Roles:** `Active Directory members`
Then click on **Save**


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qkmz9p65jqfhupvpx4ui.jpg)

-----------------------------------------------

## 6.3 define the Business Rules parameters

To add **Business Rules**, first 

- click on the **Add Business Rules** option.


**Name:** `testforBusinessLDAP based on our setup`
**Operation:** `Add-triggered only upon user creation`

**note:**
This means that a user is allowed to add only after their account has been successfully created.

**status:**`pending modifications`

**note:**
This means that when our user is created, it is not active.

**Apply selected rule when conditions match:** `LDAP User Role(based on our setup)`

**note:**
When the user defines the specific target to be achieved, we link it to the LDAP User Role that was previously created.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oh48t4auvjlonls8cvjh.png)


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lyexbzw6s23omicgr5zu.png)


## Configure the necessary fields

- **Right-click** on the column of the table where it says **Type**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/e2cbqs2oa88ptahri1hi.png)

- Then, click **Edit**
 

- choose **Expression**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ybj2ga58derdmo06b7rb.png)

**Attribute:**`First Name`
**Operation:**`Is empty`
**Negation:** `enable`

**note:**
this ensure that when the **First Name** field is empty, LDAP User Rule is not triggered.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/orwghqtzjr1il82v2cjn.png)

- Then click **save**

------------------------------------------------------------------------

## 6.4 Key Points About Business Rules

When we add users, they are automatically added to all **Active** business rules based on our setup.
**Example (based on our setup):** The **Test for Business LDAP** and **Test for Business PowerShell** are the business rules that we have.


### Possible Conflict
This can cause problems because the same user is being added to both roles at the same time. We need to only  **Active** one of them base on our manage system and diactive the others.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/etcjwwx7xrfhgfwqyp4k.png)

Because we want to configure the **business rule** for the **AD Managed System**, we activate the **LDAP User Role** and deactivate the others.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/00bmp2bds5ewgb1u4npo.png)
 
also need to configure a managed system.

### How to configure managed system?

#### Access the Managed System 

locate the **Provisioning tab** in the main menu.
Click on the **Managed System** section.

Here, we observed that some Managed System was already in place. 

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w9pbaf4pu50cyn7cx9qi.jpg)

We should ensure that only the **AD Managed System** is **Active**.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/b665krify28271khq5ve.png)


In the list of managed systems, if any of them, regardless of the **AD Managed System**, are also **active**, they should be edited.


---------------------------------------------------

#### Edit Managed System

In the action section next to it, click on **Edit**. This allows you to modify specific details of the managed system.


**Show on User Change Password Screen:** `The checkbox is ticked. This is the only checkbox that should be ticked.`


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/98rvjhk4vyzv1mwoz9yh.png)



But in **AD Managed System** ensure you activate the following three options.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/39ujfvd3oit483g84ntx.png)


_Congratulations all this work will be connected to the **Active Directory member** used by all users. It will pass through the **LDAP Managed System**, ensuring the user is created correctly._


-------------------------------------------------

# 7.How to provision?

## Overview:
This section provides step-by-step instructions for provisioning.

we first create a new user in OpenIAM and It also includes steps to verify the user's existence in Active Directory setup successfully.

#### note:
Provision: means that whenever you create a user, it is automatically added to the Active Directory and created without requiring manual intervention.

-------------------------------------------------------------------

## 7.1 How to create a user in OpenIAM


### Configure the necessary fields to Create New User 


Navigate to **User Admin** Tab
Select the option to **Create New User**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nhgeqgupdxmvk92p7moj.png)


**Select User Type**: `Default User`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/id952d4yd1pz2ct2eikv.jpg)


------------------------------------------------

### Template based view vs. Classic view 

We chose the `classic view` as it allows us to provide more detailed information to the user.

-------------------------------------------------

### login

 **login**: `It is generated after the user creates the interface`.
 

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uyimt3dg2njwxnwgbi8e.png)


-------------------------------------------------

### Fill in User Information

First Name: `User First Name`
Last Name: `User Last Name`
Metadata Type: `Default User`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t437gxpp0y5ntlqwlh6y.png)


-------------------------------------------------

## 7.2 importance of assigning roles

**Importance**: Roles are crucial in OpenIAM as it operates on a **role-based** system. Without assigning roles, users cannot be provisioned.

**note:**
**Some fields are not mandatory, but certain ones, like the role field, must be filled in for sure.**


#### Active Directory Members


In our set up you should first ensure that the **Active Directory Members** role is already created.

If it hasn't been created yet, please create the **Active Directory Members** role first before proceeding to create a user.

In this section of the document (5. How to Create a Role?), guidance is provided on creating roles for Active Directory members.


#### create business rules

After setting the **Active Directory Members**, you should proceed to configure the **Business Rules**. 

Detailed instructions on how to do this can be found within at this (6.How to create a business rules in OpenIAM?) section of the document.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zjzgyvnq90qe6tlvufui.png)

After completing these steps, you can proceed to assign the managed system and relevant role.

**Select a Managed System:** `LDAP Managed System`
**Type a Role Name:** `Active Directory Members` 



-------------------------------------------------

### Fill in Email Address
 Email Address Type:`primary email`
 Email Address:`Type your email address in here`

**note:**
The reasoning behind selecting this type can be found at this (7.How to Do Attribute Mapping?) section of the document.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mzpe2c3lawqze4lhg8md.png)


------------------------------------------------

### Fill in phone 

Phone Type: `Office Phone ( The Office Phone attribute exists in OpenIAM and is linked to the corresponding attribute in Active Directory )`

**note:**
The type is something that is the same in Groovy script and in our Groovy script, which is `office phone`.

Country Code: `Since we have Iranian user,the country code is +98 `
Area Code: `Since we have Iranian user,the area code is also +98`
Phone Number:`Please provide your phone number`


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/26avz1cb3q5wt6tuzkj0.jpg)

------------------------------------------------

### Fill in notifications

First Checkbox: ` Unticked `
Second Checkbox: ` Unticked `

**note:**
If the email is fake, we need to untick the first two checkboxes. Since the email is not genuine, notifications won't be received.

Third Checkbox: ` unticked `

**note:**
the third checkbox should be unticked as it is meant to wait until the user starts using the system and then provisioning which is not the desired behavior in this case.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0msyb4ex44mvwldly9e4.png)

------------------------------------------------

### Click on the save button

After completing all these steps, make sure to click **Save**. Once the user is provisioned.

------------------------------------------------

## 7.3 verify if the user has been created in Active Directory by checking in OpenIAM

**note:**
When a user is created in any service or machine, it appears in **user identities**.

### How to navigate to the user identities

- We navigate to the **user info**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6hakppv9a4br5iyc3zwp.png)

- In the **classic view**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/30hxyoxdvwal2e0f67cp.jpg)

Under **user identifies**, you will be able to locate the **Active Directory managed system** by scrolling down.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mszgthvo3p2lbdaziymi.jpg)


_Congratulations! The user has been successfully created in OpenIAM._

------------------------------------------------


### type First Name into the search bar and review the results

- simply type **First Name** into the **search bar**

- click on the **First Name** 


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/24a5sxkm8zx68yto96p1.jpg)

- switch to the **classic view**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h17ol3f7z25c79z4f5zy.jpg)


you can view the **OpenIAM ID**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6duh6kiwku10353k0mgn.png)


**User Status**: refers to the current state of a user account within the OpenIAM system.


**Example (based on our setup):**
**User Status:** `The status of this user indicates that they have not logged in for the first time yet`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/o43unjvcsmisiclj5ljh.png)



------------------------------------------------

## 7.4 How to edit user details in OpenIAM

### How to navigate to the user you want to edit.

- simply type First Name into the search bar.

- click on the First Name.

- Clicking on the **edit** option allows modification of user attributes.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jy2hc21bpv41c2cn66no.png)

**note:**
Be careful when choosing the attribute type It should also be the same in Groovy script to ensure accurate mapping.  

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jb4bqj30gpqg2deydh5a.jpg)

------------------------------------------------

## 7.5 How can we determine the types of access that users have?
 
### How to navigate to the User Entitlement

click on **User Entitlement**
 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/55hxf0wtww0r5d9v2h5q.png)

**note:**
it will display the types of access the user has, along with the groups and services they are entitled to.

**Example (based on our setup):**

Only the **account group** is authorized for this, and it also holds the role of **Active Directory Members**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/keytsuvx2rt82rvnx95u.png)

------------------------------------------------

## 7.6 How can we get a comprehensive overview of each user?

**note:**
The user history section provides a overview of all past activities in a timeline format.

### How to navigate to the user history

click on **User history**

**create user :** `time that user is created.`
**Provision add :** `when a user is added to Active Directory.`
**Provisioning :** `when ensuring all attributes, such as email and phone number, are properly configured.` 
**save connector response:** `The response from Active Directory to OpenIAM indicates whether the connector response was successful or if it failed.`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ndvrvqbkpg70vtf7tekl.png)

**note:**
you can open it to review the description and identify the type of error it displays.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mqdjzk0i2gbv7m0hbzy7.png)


------------------------------------------------

## 7.7 verify if the user has been created in Active Directory by checking in Active Directory

### How to navigate to the Active Directory Users and Computers tool

- Login to your **Active Directory machine**.

- Press `Windows + R` on your keyboard.

- type `dsa.msc` to launch the **Active Directory Users and Computers tool**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/79b66zud0tb4yfbow054.png)

- Please navigate to your domain.

**Example (based on our setup):**
 **domain=** `Saeigroup.local`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lj919jzqgiegojvyh71e.png)

- Please navigate to your Organizational Unit.

**Example (based on our setup):**
**Organizational Unit=** `SaeiUser`

**note:**
If you are looking for a user created earlier, you can refresh the screen to locate them in the specified directory.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rx48xotzgt3gsramq4gx.png)

_Congratulations! The user has been successfully created in the Active Directory._

**note:**
Also if you click on it, you will be able to see the display name and the email address that you have set.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vqb7rehy4t8eo5fs4bsu.png)

The problem with the telephone field lies in the fact that the area code and country code are merged, which is not ideal.
You can resolve this problem by referring to this section of the document.(7.How to Do Attribute Mapping?)




-------------------------------------------------

## 7.8 How to Delete users in OpenIAM?

**note:**

When you **delete** a user in **OpenIAM** the corresponding user  provisioned in **active directory** is also deleted.

- We navigate to the **user info**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fu6oj868hkztf8thzbsn.png)
## Attribute Mappings
- Clicking on the **Delete** option

- type **First Name** and **Last Name**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3xtwyea6dyrdu00qtkwz.png)

click on **Save**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wubhsbkxx3lzmmlu32oq.png)


 _Congratulations! The user has been successfully removed from Active Directory, and OpenIAM._

----------------------------------------------------------

# 8.Active Directory User Synchronization

## Overview:

Synchronization is the process of creating users from Active Directory in OpenIAM.

## Prerequisites

Navigate to the business rules section and activate only the business rule (6.How to create a business rules in OpenIAM?) for the **AD Managed System**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j0j5ycqr4vp5nvnrxtxc.png)


---------------------------------------------------------------

### How to find users in Active Directory machine?

#### Accessing Active Directory Users and Computers

Login to your **Active Directory** machine.

Press `Windows + R` .

Type `dsa.msc` and press Enter.

This will open the **Active Directory Users and Computers console**.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dm1ef5eufg7obtjo4wka.png)


Please navigate to **your domain**
**based on our setup:**`Saeigroup.local is our domain`

Then, navigate to **your Organizational Unit**
**based on our setup:** `SaeiUsers is our Organizational Unit`

**note:**
All users have a **first name**, **last name**, **telephone number**, and **email address** as an attribute.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dg4ip29w5qm6vgwflbun.png)

To proceed, we need to import them into **OpenIAM** and then perform a **one-way synchronization**.

-------------------------------------------------------------------

## 8.1 How to access the synchronization settings?

#### To access the synchronization settings

- navigate to the **provisioning tab** 

- select **synchronization**
 

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/94fym23nstgbjvnfahiw.png)

Synchronization occurred with the **Managed System**, and this managed system is referred to as the **AD Managed System**.

- In the Managed System column, we select **AD Managed System**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lxtxtwtwmyb1y7se9myn.png)

#### Choose Synchronization Type

And there are two options available: **syncing either group or user**. 

- We selected the **AD USER Example** and proceeded to click on the edit option.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9ad3z8zh95cgbe0ct89m.png)



-------------------------------------------------------------------

### Configure the fields

**Name:** `please enter the desired name`

**Records count in one Branch:** `1000`

**Active checkbox:** `ticked`


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/21yx7kmwsq6t1ulm6n3c.png)



-------------------------------------------------------------------

### Provision to target system

**Provision to target system? (checkbox) :** `Unticked`


**note:**
`If we didn't tick this checkbox, it would be one way, and it's from Active Directory users going to create in OpenIAM `

**note:**
But if we want to have it two-way, we can `tick` the checkbox.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0ksfywr1p4qe5t3ivmvt.png)


-------------------------------------------------------------------

**Managed System:** `AD Managed System`
**synchronize Object:** `user`


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/n50kauzbrmgad1o16fx0.png)



-------------------------------------------------------------------

**Synch Type:** `Complete`
**Synch Frequency:** `Execute once on exact data` 
**Run on:** `select data that you want to sync executed`

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ifx7tirn60qp6nvbui4j.png)

-------------------------------------------------------------------

## 8.2 Validation Rule

**Validation Rule:** `/sync/User/ad/ADValidationgroovy`



![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i1c91k8u1ggb2sknykl0.png)




When you click on **Edit**, you can view the script.
 
![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4dbw80scxxh0p1tqq3mb.png)


The **validation script** checks whether the user retrieved from Active Directory is valid or not.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/n850mr76zokzl8v5fpvn.png)


if it's not valid it is going to println it is not valid


## 8.3 Where is the log location of println?

**note:**
The `println` is logged in the file located at this path on the **OpenIAM machine**: `/user/local/openIAM/logs`. 

#### Steps to Access the Log File:

- Login to your **OpenIAm machine**.

- Press `Windows + R` on your keyboard.

- Type `cmd` and press Enter

- In this path `/user/local/openIAM/logs` Type `ls` press Enter

you should see synchronization.log

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3wmoau2cg5keixd1ojm4.png)
 --------------------------------------------------------------

## 8.4 Viewing the Log in Real-Time


If you type `tail -f synchronization.log` you would see **validation script** in your **OpenIAm machine**

```
tail -f synchronization.log
```
**note:**

You can identify errors in the script by using `println` to debug. Additionally, you can check the log of **OpenIAm machine** in `synchronization.log`, file which is located in the path `/user/local/openIAM/logs`.

this the log from **OpenIAm machine** for syncronization

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ioc60vgrsnwyjiyhr559.png)


--------------------------------------------------------------

## 8.5 Transformation Rule: 

`/sync/User/ad/ADTransformationgroovy`


After **successful validation**, user data sourced from **Active Directory** is transformed into an attribute in **OpenIAm machine**. 


When you click on **Edit**, you can view the script.



![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4ofnwjr9jtrcf2s7anj0.png)



### Some Attributes Not Synced by Default


#### Issue

The **transformation script** did not automatically sync all attributes because it was designed to transform only a limited set of attributes.

#### Solution

To address this issue, we have added a function to the script that enables the synchronization of additional attributes, including **phone numbers**.

Now we want to mention some changes in the `ADTransformationgroovy` script as follows.

#### logging functionality

This script includes logging functionality.

    

```
            def lg = new Login()
                lg.operation = AttributeOperationEnum.ADD
                lg.login = attrVal.value
                lg.managedSysId = "0"
                lg.setActive(true)
                pUser.principalList.add(lg)

                /*Login lg2 = new Login()
                lg2.operation = AttributeOperationEnum.ADD
                lg2.login = attrVal.value
                lg2.managedSysId = config.getManagedSysId()
                lg2.setActive(true)
                pUser.principalList.add(lg2)*/

            }
        }
```

#### eliminate the space

In this part of the code, we eliminate the space in the surname to prevent errors that occur when such a space exists. This ensures that if you search for a username in the search bar, it will appear correctly without that space.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p31a2uo1f72sd39yjfsn.png)



```
        attrVal = columnMap.get("Surname")
        if (attrVal) {
            pUser.lastName = attrVal.value?.replaceAll("\\s", "")//empty space check
        }

```

#### Handling Telephone Numbers in the Transformation Script
  
```
        def telAttr = columnMap.get("telephoneNumber")
        if (telAttr && StringUtils.isNotEmpty(telAttr.value)) {
            def phoneNumber = telAttr.value.trim()
            println("Preparing phone number for user: ${phoneNumber}")
        
            def areaCd = ""
            def countryCd = ""
        
            // Detect if phone number starts with 0
            if (phoneNumber.startsWith("0")) {
                areaCd = "021"    // Tehran example
                countryCd = "+98" // Iran code
                println("Detected local Iranian number, setting area and country codes.")
            } else {
                areaCd = "?"    
                countryCd = "?" 
                println("International or unknown format, no area/country codes assigned.")
            }
```
        
In this part of the **transformation script**, the telephoneNumber is retrieved from **Active Directory**. The script then prepares to assign values for the **Area code** and **Country code**.

By default, both the **Area code** and **Country code** are left empty. The script then checks if the phoneNumber starts with `0`—which is typical for **Iranian phoneNumbers**.

If the number starts with `0`, the script:

Sets the **Area code** to `021`

Sets the **Country code** to `+98`

Logs a message: `Detected local Iranian number, setting area and country codes.`

As a result, you can see that the user sync is functioning properly, and both the **area code** and **country code** are set correctly.


![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/u9t9ei0qxp3heizutyuq.png)


If the number does not start with `0`, the script:

Sets both the **Area code** and **Country code** to `?` as placeholders

Logs a message:`Phone number not found on user — adding new phone.`

**note:**
To avoid errors, it sets both the **Area code** and **Country code** to `?` as placeholders when they are not explicitly defined.


---------------------------------------------------------

```
           // Check if phone already exists for user
            boolean phoneExists = pUser.phones?.any { it.phoneNbr == phoneNumber }
            if (phoneExists) {
                println("Phone number already exists on user — skipping addition.")
            } else {
                println("Phone number not found on user — adding new phone.")
```


#### If a phone number already exists, the script:

- Skips adding it again

- Logs the message: `Phone number already exists on user — skipping addition.`

#### If no phone number is found, the script:

- Proceeds to add the new phone number

- Logs the message: `Phone number not found on user — adding new phone.`

---------------------------------------------------------

### Handling Missing Phone Numbers

If the phone number is null or missing, the script assigns a placeholder value of # to the phone number.



```

import org.openiam.idm.srvc.continfo.dto.Phone //phone
                def phone = new Phone()
                phone.mdTypeId = "CELL_PHONE"
                phone.phoneNbr = phoneNumber
                phone.areaCd = areaCd
                phone.countryCd = countryCd
                phone.active = true
                phone.default = false
                phone.operation = AttributeOperationEnum.ADD
        
                if (pUser.phones == null) {
                    pUser.phones = new HashSet<Phone>()
                }
                pUser.phones.add(phone)
                println("Phone added successfully:")
            }
        }
       
```
In this section of the script, several **mandatory attributes** are being set for the phone entry. All of these fields are required by **OpenIAM**. If any one of them is missing, an error will occur during processing.

If the phone number is null or missing, it assigns a placeholder value of `#` to **Phone number**.



**note:**
After all these changes, all attributes synced.
including **phone numbers**.

--------------------------------------------------

You can see the all log messages here (8.3 Where is the log location of println? )

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1pddp6numk3wdyxlgaqq.png)

--------------------------------------------------

### SQL Query/Directory Filter

In this part we say which users should call to sync and with which attributes.

 **SQL Query/Directory Filter:** `(&(objectClass=user)(objectCategory=person))`



![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vttgzv6tf9xcd8jpn0q8.png)



--------------------------------------------------

### Source attribute names

 it refer to what attribute name and  what is the source of it?

**Source attribute names:** `/sync/User/ad/ADAttributes.groovy`

When you click on **Edit**, you can view the script.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lczqby39fkwmg7sel7e2.png)


```
import org.openiam.sync.service.AttributesScript


class ADUserSyncAttributes implements AttributesScript {
    @Override
    String[] getAttributes() {
        return ["memberOf","members", "cn", "sn", "streetAddress", "l","postalCode","st",
                "givenName", "sAMAccountName", "dn", "DistinguishedName", "mobile", "telephoneNumber","mail",
                "modifyTimestamp", "createTimestamp", "mail", "userPrincipalName"] as String[];
    }

}

```

**note:**
We’ve added the **telephoneNumber** attribute to the **Attributes script** this is the only change made. However, you can add more attributes if needed, based on your requirements

--------------------------------------------------------------

- We check the connection first, so click on **Test Connection** 

- and then click on **Save** 

- click on **Sync Now**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zhb62in2vjxdi0ghwmwo.png)

---------------------------------------------------------

## 8.6 Viewing Synchronization History
- Navigate to **synchronization history**
  

- you can see the history of sync that you make.



![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ju7rwlfl9xlnw6q5zoyn.png)




----------------------------------------------------------------

## 8.7 Troubleshooting Sync Issues

The reason the sync might not happen could be because the transformation doesn't occur correctly. 

if clicking on **edit** resolves the issue.


- the system displays **New User**  instead of the actual name of the user from Active Directory.

- the **result column** shows `failure`

**note:**
The request body contains all attributes retrieved from Active Directory

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/68nqaqqbcbsikyfrk1qs.png)

if you click on **New User** 

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ot7skgqp0za4smb1go9a.png)

You would see the error displayed in the **user interface** as well as in the **log** we included in the **TransportationGroovy script**. You can access the log from here(8.3 Where is the log location of println?) to identify and resolve the issue.

**For example:** 
The telephone number was not present in the **request body**. This indicates that the request did not retrieve it from the **active directory**. Therefore, we configure the query with properties to include both **mandatory** attributes and **optional** ones together in the **SQL Query/Directory Filter**.


 -----------------------------------------------------------

## 8.8 Successful Synchronization
When synced correctly, you will see all the users who have been successfully synced.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uwpx1hxeqcrh4c2jsyjm.png)


And there is no error in here

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ud7xda6etykooxb6imgx.png)

Additionally, you will see a column map where you can view all the attributes associated with the user.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yd3aif9m2o5jobb53l2i.png)

 _Congratulations! You have successfully synchronized the user from Active Directory to OpenIAM.
 

-------------------------------------------------------------------

## 8.9 Editing the Active Directory Connector Script
Login to your Active Directory machine.

locate this path: `This PC>Local Disk C>ADConnector>Connector`

- Then click on **Edit with Notepad**

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/g5io8p769ly7ujsdfkaf.png)

**note:**
Open the file it contains a script that manages updating user, retrieving user data, and sending user details.

**note:**
We will implement changes to the script and create a **log file**. This log file will include information such as messages like `user not found` or details like the username and telephone number of users

**note:**
If you check the log file created by the script, you'll find details about the user synchronized with their telephone number and other related information printed within the script.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fzscvxasv1owwpitjbpo.png)

-------------------------------------------------------------------

# 9.Differences Between AD Managed Systems and PowerShell Managed Systems

The difference between an **AD Managed System** using **LDAP** and a **PowerShell Managed System** uses **scripts** to communicate with **Active Directory**.


**note:**
LDAP and PowerShell both communicate with Active Directory, but in different ways. LDAP uses a protocol, while PowerShell uses scripts to interact with Active Directory.

## 9.1 Attribute Mapping Differences
the other difference between an **AD Managed System** and **PowerShell Managed System** is the way of attribute mapping 


### Navigate to the Policy Map

locate the **Provisioning** tab in the main menu.
Then go to **Manage System**. 
Select the **AD Managed System**.
Click on **Edit**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p4n0zxwgs80py44zo0pd.jpg)

**note:**
In every **Managed System**, there is a designated **Policy Map**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/q3m1qlhf7bj158ia5f82.png)

### edit the user policy
 
navigate to the **user policy** section

select the **Edit** option.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k5s5792m6mcxuaj1jged.png)

## 9.2 PowerShell User Policy Configuration


The Principal for **PowerShell** is set to **SamAccountNAMe**.
The Password is set to **AccountPassword**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/liq75zbzuzythtrq42we.png)

## 9.3 LDAP User Policy Configuration

The Password for **LDAP** is set to **Unicodepwd**.
The Principal is set to **cn**.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5ern1ttnvchp8hbqwo3q.png)


Another difference between LDAP and PowerShell is that the attribute names in OpenIAM and Active Directory are **different** in **PowerShell**.



![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w0z0qt9dxyzhbayl61nd.png)



In LDAP, the attribute names in Active Directory and OpenIAM are 
indeed **the same**.



![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fn0vnqfotmf7w4xa162o.PNG)

If you use an incorrect attribute name in LDAP, it will result in `error code 16`.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8xu7gg8hhlcq9l3ciw2y.png)


------------------------------------------------------------

