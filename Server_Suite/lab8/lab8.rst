.. _l8:

----------------------------------
Prepare Centrify Identity Platform
----------------------------------

Introduction
------------

This eighth lab will cover:

1. Customizing the Centrify Identity Platform (CIP)
2. Create Directory Service Users in CIP
3. Create Privileged Roles
4. Install and Configure the Centrify Connector


.. note::
    Estimated time to complete this lab: **50 minutes**

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab
- \https://<tenant>.my.centrify.net

------

Customizing the CIP
*******************

In this exercise, Alex (you) will login to the Centrify Identity Platform and perform initial configuration to "brand" the platform with Greensafe Logos and colors.

#. Login to *apps-server.greensafe.lab* with the following credentials:
   
   - **Username:** afoster
   - **Password:** *Provided by Trainer*

#. Launch Google Chrome and browse to your unique Identity Platform URL https://<tenant>.my.centrify.net
#. Login to your unique Identity Platform with the following credentials:

   - **Username:** admin
   - **Password:** *Provided by Trainer*

#. On the Welcome Message, click **Cancel**
#. Use the Main Menu on the left, navigate to *Settings > General*
#. Under *Account Customization*, change the *Portal Ribbon Accent Color* to **#F1F1F1**
#. Click the **Upload** button to change the *Portal Image*, select C:\\Share\\Greensafe Portal.png
#. Under *Login Customization*, click the **Upload** button to change the Login Image, select C:\\Share\\Greensafe Login.png

   .. figure:: images/lab-002.png

#. Under *Message Customization*, click the **Upload** button to change the E-Mail Image, select C:\\Share\\Greensafe Portal.png
#. Click **Save**


Create Directory Service Users in CIP
*************************************

Part of the initial configuration includes creating Centrify Directory Service User Accounts that will be used for specific privileged access to Greensafe servers without requiring specific domain identities. In this exercise, Alex (you) will create an account that will manage Centrify Connectors and a second account that will be used by 3rd party contractors who support specific Greensafe servers.

#. While still in the CIP, use the main menu on the left to navigate to *Access > Users*
#. Click **Add User**

   .. figure:: images/lab-003.png

   .. note::
       When you get the message that you have to add a suffix to the username@ account, user **labguide** as te prefix!!

       .. figure:: images/lab-004.png

#. Enter the required information to create a new Centrify Directory Service User for Centrify Connector Management.
 
   - **Username:** ConnectorMgr (leave the suffix to *labguide*)
   - **E-Mail Address:** ConnectorMgr@greensafe.lab
   - **Display Name:** Centrify Connector Manager
   - **Password:** *Provided by Trainer*
   - **Check** the box to *Password never expires*

#. Click **Create User**
#. Click **Add User** button to create a second user
#. Enter the required information to create a new Centrify Directory Service User for 3rd Party Contractor Support
 
   - **Username:** zContractor (leave the suffix to *labguide*)
   - **E-Mail Address:** contractors@greensafe.lab
   - **Display Name:** Contractor Support Account
   - **Password:** *Provided by Trainer*
   - **Check** the box to *Password never expires*

#. Click Create User


Create Privileged Roles
***********************

Privileged roles are created to group privilege to the infrastructure. Roles can be assigned to users, groups, systems and other roles. In this exercise, Alex (you) will create specific Privileged Access Roles that will be used during the implementation and day to day management of the solution. 

#. From the Centrify Identity Platform, use the main menu on the left to navigate to *Access > Roles*
#. Click **Add Role**
#. Use as name **Connector Manager Role**
#. Click **Administrative Rights** left to the *Name*
#. Click **Add**
#. This role requires the privilege to Register and Manage Centrify Connectors, select **Register and Administer Connectors**

   .. figure:: images/lab-009.png

#. Click **Add**
#. Click **Members** left to the *Administrative Rights*
#. Click **Add**
#. Search for *ConnectorMgr@labguide* and click **Add**

   .. figure:: images/lab-005.png

#. Click **Save**

   .. figure:: images/lab-007.png
  
#. Click **Add Role** to add a second role.
#. Use as name **Contractor Role**
#. Click **Administrative Rights**
#. Click **Add**
#. This role requires privilege assigned by an administrator and should be limited to servers that are specifically assigned to the role. Greensafe  has contractors that manage Greensafe database servers. Select **Privilege Access Service Users**

   .. figure:: images/lab-008.png

#. Click **Add**
#. Click **Members** left to the *Administrative Rights*
#. Click **Add**
#. Search for *zContractor@labguide* and click **Add**
#. Click **Save**
#. Click **Add Role** to add a third role.
#. Use as name **PAS Admin Role**
#. Click **Administrative Rights**
#. Click **Add**
#. This role provides members privilege to administer all resources within the Centrify Identity Platform. Select **Privilege Access Service Administrator**
#. Click **Add**
#. Click **Save** (members will be added later)
#. Click **Add Role** to add a fourth role.
#. Use as name **PAS Power User Role**
#. Click **Administrative Rights**
#. Click **Add**
#. This role provides members privilege to administer resources they explicitly add to the Centrify Identity Platform and have limited privilege to administer currently added resources. Select **Privilege Access Service Power User**
#. Click **Add**
#. Click **Save** (members will be added later)
#. Click **Add Role** to add a fifth role
#. Use as name **PAS User Role**
#. Click **Administrative Rights**
#. Click **Add**
#. This role provides members privilege to access resources that are explicitly added to this role with no privilege to add resources to the Centrify Identity Platform. Select **Privilege Access Service User**
#. Click **Add**
#. Click **Save** (members will be added later)


Install and Configure Centrify Connector
****************************************

Centrify Connectors are deployed in the environment to facilitate specific access between the Centrify Identity Platform and Greensafe Infrastructure Resources. In this exercise, Alex (you) will install the Centrify Connector software and configure it to communicate with the Centrify Identity Platform and Greensafe Active Directory environment. 

#. From the Centrify Identity Platform, use the main menu on the left to navigate to *Settings > Network > Centrify Connector*

   .. figure:: images/lab-010.png

#. Click **Add Centrify Connector**
#. Click the *64-bit* link to download the Centrify Connector installation package
#. Navigate, using the *Windows Explorer*, to the location where the download has been saved (default *Downloads*)
#. Launch the application **Centrify-Connector-Installer**
#. At the *Do you want to run this file?*, message click **Run**
#. At the Welcome Message, click **Next**
#. Accept the EULA *(Check the "I have read and accept..." message)* and click **Next**
#. Keep the default features selected and click **Next**
#. Click **Install** (Some open applications will be closed automatically)
#. When completed, click **Finish** (The Connector Configuration Wizard will start automatically)
#. At the Welcome Message, click **Next**
#. Maintain strong encryption options and click **Next**
#. Greensafe is not using a proxy server and no changes are needed. Click **Next**
#. Change the Tenant URL with your unique platform URL. \https://<tenant>.my.centrify.net (You can copy and paste the URL directly from the address bar of the browser.) Leave all other options *default*!!!

   .. figure:: images/lab-011.png

#. Check the **Use Registration Code**
#. Open the CID UI and navigate to **Settings > Network > Registration Codes**

   .. figure:: images/lab-012.png

#. Check the **Account Creation** Line and under **Action**, select **Retrieve Code**

   .. figure:: images/lab-013.png

   .. figure:: images/lab-014.png

#. Click **Copy** to copy the code to the clipboard
#. Back in the **Centrify Connector Configuration**, paste the *Registration Code*

   .. figure:: images/lab-015.png


   .. note::
      Your codes will be different!!! Don't use the codes as mentioned in the screenshots

#. Click **Next**

..
   #. You will be prompted to login to the Centrify Identity Platform to register the Connector. Login using the following credentials:

      - **Username:** ConnectorMgr@labguide
      - **Password:** *Provided by Trainer*

#. Check the box associated to the *greensafe.lab* domain and click **Next**
#. In the *Permissions are required to domain deleted objects* click **Yes** to assign the permissions
#. The checks should be successfully run and click **Next**

   .. figure:: images/lab-016.png

#. After the connector has been configured successfully and registered with the Centrify Identity Platform, Click **Finish**
#. The *Centrify Connector Control Panel* will be displayed indicating the current status and connection with the Centrify Identity Platform. You can **close** the Control Panel and return to the Centrify Identity Platform
#. Close the Centrify Connector Download window and refresh the Centrify Identity Platform. The Centrify Connector (*apps-server.greensafe.lab*) should be displayed as an available connector

   .. figure:: images/lab-017.png



.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>