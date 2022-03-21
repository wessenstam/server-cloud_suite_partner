.. _l9:

------------------------
Configuration of the CIP
------------------------

Introduction
------------

This ninth lab will cover:

1. Configure Role-Based Permissions
2. Configure a Domain Administrative Account
3. Configure System Discovery Profiles
4. Configure System Sets
5. Configure Multifactor Authentication for Privilege Elevation


.. note::
    Estimated time to complete this lab: **90 minutes**

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab
- \https://<tenant>.my.centrify.net

------

Configure Role-Based Permissions
********************************

Now that Privilege Roles have been established and the Centrify Connector has been deployed, we can now assign privilege to Active Directory Users and Groups. In this exercise, Alex (you) will assign AD groups to recently created roles and configure global security settings and permissions.

#. From the Centrify Identity Platform, use the main menu on the left to navigate to *Access > Roles*
#. Click the **System Administrators Role**
#. Click **Members**
#. Click **Add**
#. Search for **Team_Security** and click **Add**

   .. figure:: images/lab-001.png

#. Click **Save**
#. From the Centrify Identity Platform, use the main menu on the left to navigate to *Access > Roles*
#. Click the **PAS Admin Role**
#. Click **Members**
#. Click **Add**
#. Search for **Domain Admins** and click **Add**
#. Click **Save**
#. From the Centrify Identity Platform, use the main menu on the left to navigate to *Access > Roles*
#. Click the **PAS Power Users**
#. Click **Members**
#. Click **Add**
#. Search for **Team_Helpdesk** and click **Add**
#. Click **Save**
#. From the Centrify Identity Platform, use the main menu on the left to navigate to *Access > Roles*
#. Click the **PAS User Role**
#. Click **Members**
#. Click **Add**
#. Search for the following groups and click **Add**:

   - Team_Sales
   - Team_Finance

#. Click **Save**
#. From the Centrify Identity Platform, use the main menu on the left to navigate to *Access > Roles*
#. Click the **Contractor Role**
#. Click **Members**
#. You will notice one member (zContractor) which was added earlier, click **Add**
#. Search for **Team_Contractors** and click **Add**
#. Click **Save**
#. Use the main menu on the left to navigate to *Settings > Resources > Security > Global Account Permissions*

   .. figure:: images/lab-002.png

#. Global Account Permissions identifies privileged account permissions granted to users, groups and roles in the Centrify Identity Platform. Greensafe has decided to grant specific privilege to administrators and power users. Click **Add**
#. Search for **PAS Admin Role** and click **Add**
#. Check the boxes for the role to provide the following permissions:

   - Grant
   - View
   - Checkout
   - Login
   - Edit
   - Delete
   - Update Password
   - Rotate

   .. figure:: images/lab-003.png

   .. figure:: images/lab-004.png

   .. note:: 
       For the options *Edit, Delete, Update Password and Rotate* you may have to scroll to the right!



#. Click **Add**
#. Search for **PAS Power User Role** and click **Add**
#. Check the boxes for the role to provide the following permissions:
   
   - View
   - Login

#. Click **Save**
#. Use the main menu on the left to navigate to *Settings > Resources > Security > Global System Permissions*
#. Global System Permissions identifies privileged system permissions granted to users, groups and roles in the Centrify Identity Platform. Greensafe has decided to grant specific privilege to administrators and power users. Click **Add**
#. Search for **PAS Admin Role** and click **Add**
#. Check the boxes for the role to provide the following permissions:

   - Grant
   - View
   - Manage Session
   - Edit
   - Delete
   - Add Account
   - Unlock Account

   .. figure:: images/lab-005.png

   .. figure:: images/lab-006.png

   .. note:: 
       For the options *Add Account and Unlock Account* you may have to scroll to the right!

#. Click **Add**
#. Search for **PAS Power User Role** and click **Add**
#. Check the boxes for the role to provide the following permissions:

   - View
   - Manage Session
   - Unlock Account

#. Click **Save**
#. Use the main menu on the left to navigate to *Settings > Resources > Security*
#. Under *Security > Security Settings*, check the box to enable periodic password rotation at specified interval (days). Use the default duration of 90 days.

   .. figure:: images/lab-007.png

#. Under *Global System Security*, check the box to allow access from a public network (web clients only)

   .. figure:: images/lab-008.png

#. Click **Save**
#. Use the main menu on the left to navigate to *Resources > Domains*
#. Click the **greensafe.lab** domain
#. Under *Permissions*, click **Add**
#. Search for **PAS Admin Role** and click **Add**
#. Check the boxes for the role to provide the following permissions:

   - View
   - Edit
   - Unlock Account
   - Add Account

   .. figure:: images/lab-009.png

#. Click **Save**

Configure a Domain Administrative Account
*****************************************

Centrify Identity Platform can be configured to facilitate domain tasks. In this exercise, Alex (you) will configure a domain administrative account to perform these tasks. This training environment has been preconfigured with a domain account (cfyadmin@greensafe.lab) to act in this capacity.

#. Logout of the Centrify Identity Platform by clicking in the top right corner the *admin account > Sign Out*

   .. figure:: images/lab-010.png

#. Login back into the Centrify Identity Platform using the following credentials:

   - **Username:** afoster@greensafe.lab
   - **Password:** *Provided by Trainer*

#. On the Welcome Message, check the box *Do not show again* and click **Cancel**
#. Use the main menu on the left to navigate to *Resources > Domains*
#. Click the **greensafe.lab** domain
#. Click **Advanced**
#. Under *Domain Accounts and Windows Local Accounts*, click the **Set** button to identify the Domain Administrative Account
#. Select the option for Active Directory and click the **Select** button to add the account
#. Search for **cfyadmin@greensafe.lab** and click **Select**
#. Enter the password (*Provided by Trainer*) and click **Select**

   .. figure:: images/lab-011.png

#. Under *Reconciliation Options*, check the boxes for:

   - Domain Account Manual Unlock
   - Windows Local Account Manual Unlock

   .. figure:: images/lab-012.png

#. Click **Save**

Configure System Discovery Profiles
***********************************

Now that role-based permissions and privilege has been established, it is time to locate and add systems to the Centrify Identity Platform. In this exercise, Alex (you) will create two distinct discovery profiles so systems can be found and added to the platform, and privilege can be administered.

#. Use the main menu on the left to navigate to *Discovery > Systems and Accounts > Profiles*
#. Click **Add Discovery Profile**
#. Make sure **Active Directory** is selected in the *Discovery Method*
#. Name the profile **Domain Server Discovery**
#. Click **Next** to select a domain account that can read the domain objects
#. Click **Select**
#. Search for **cfyadmin@greensafe.lab** and click **Select**
#. Under *Scope of Search*, check the **greensafe.lab** domain

   .. figure:: images/lab-013.png

#. Click **Next**
#. Click **Next**
#. Click **Done**

#. Right click the newly created *discovery profile* and click **Run**

   .. figure:: images/lab-013.png

#. While the discovery is running, click Add Discovery Profile to add a second discovery profile.
#. Under Discovery Method, Select **Port Scan**
#. Name the profile **Network Port Scan Discovery**

   .. figure:: images/lab-014.png

#. Click **Next**
#. Click **Add** to set the Scope
#. Select *Range* and enter **10.0.0.30** and **10.0.0.35** in the corresponding start/end fields

   .. figure:: images/lab-015.png

#. Under *Discovery Accounts*, Click **Add**
#. Use the drop-down menu and select **Add Discovery Account**
#. Name the account **UNIX Admin**
#. Enter the **Username:** cfyadmin
#. Enter the **password:** *Provided by Trainer*
#. Click **Done**
#. Click **Add** to add the new *UNIX Admin Discovery Account*
#. Click **Next**
#. Click **Next**
#. Click **Done**
#. Right click the newly *created discovery profile* and click **Run**
#. Use the main menu on the left to navigate to *Resources > Systems*

   .. note::
       Once the discovery profiles are completed the following systems should be listed (it may be necessary to refresh the page or use the user profile menu at the top right and select Reload Rights
#. You should see the following systems being mentioned:

   - apps-server.greensafe.lab
   - apps-unix.greensafe.lab
   - db-server.greensafe.lab
   - db-unix.greensafe
   - dc.greensafe.lab
   - win-id-platform.greensafe.lab (the CIP server)

Configure System Sets
*********************

Systems have been added into the Centrify Identity Platform and while global and role-based permissions have been applied, there will be instances where systems need to be grouped based on their role within the organization. In this exercise, Alex (you) will create a number of system sets that will be configured and shared with other privileged users. Additionally, you will understand how to apply role-based permissions to the members of the set as well as the set itself.

#. Using the main menu on the left to navigate to *Resources > Systems* to display all systems
#. Using Google Chrome Menu, establish a *New Incognito Window* so you can login as different users and confirm the information in the table below:

   .. list-table::
         :widths: 10 20 10 30
         :header-rows: 1
      
         * - Username
           - AD Group
           - Centrify Role
           - Available Systems
         * - jmiller@greensafe.lab
           - Domain Admins
           - PAS Admin Role
           - apps-server.greensafe.lab, apps-unix.greensafe.lab, db-server.greensafe.lab, db-unix.greensafe.lab, dc.greensafe.lab
         * - bhughes@greensafe.lab
           - Team_Helpdesk
           - PAS Power User Role
           - apps-server.greensafe.lab, apps-unix.greensafe.lab, db-server.greensafe.lab, db-unix.greensafe.lab, dc.greensafe.lab
         * - krogers@greensafe.lab
           - Team_UnixAdmins
           - Pas User Role
           - No Systems
         * - zContractor@labguide
           - N/A CDS User 
           - Contractors Role
           - No Systems
         * - lbennett@greensafe.lab 
           - Team_Contractors
           - Contractors Role
           - No Systems

   .. note::
       You will notice that due to role based administrative rights applied earlier, the main menu at the left will look different for specific users. 
       
       | You will also notice that due to global system permissions applied earlier, systems are viewable to Joe Miller (jmiller@greensafe.lab) and Bob Hughes (bhughes@greensafe.lab). 

#. Return to the Centrify Identity Platform (*logged in as Ales Foster*) and navigate to *Resources > Systems* click the **Add** button on the **far right under Sets**

   .. figure:: images/lab-018.png

#. Name the new system set **Greensafe Domain Controllers**
#. Click **Save**
#. Under Systems, click the **Add** button on the far right under Sets, to create a second set
#. Name the new system set **Greensafe Windows Servers**
#. Click **Save**
#. Under Systems, click the **Add** button on the far right under Sets, to create a third set
#. Name the new set **Greensafe Unix Servers**
#. Click **Save**
#. Under Systems, click the **Add** button on the far right under Sets, to create a fourth set
#. Name the new set **Greensafe Contractor Supported**
#. Click **Save**
#. To add a system to a set, select the systems and use the Actions button and select **Add to Set** 

   .. figure:: images/lab-019.png

   .. figure:: images/lab-020.png

#. Select the set, as described below in the table, and click **Save** to add the selected systems to the *Set*

   .. list-table::
         :widths:  50 50
         :header-rows: 1
      
         * - System Set
           - Assigned Systems
         * - Greensafe Domain Controllers 
           - dc.greensafe.lab
         * - Greensafe Windows Servers 
           - apps-server.greensafe.lab, db-server.greensafe.lab
         * - Greensafe Unix Servers 
           - apps-unix.greensafe.lab, db-unix.greensafe.lab
         * - Greensafe Contractor Supported
           - db-server.greensafe.lab, db-unix.greensafe.lab
   
   .. note::
       Once completed, the sets are currently available to Alex Foster (you). The next steps will be to assign permissions to others to see the set and to set explicit permissions to the members of the sets without assigning the permission to each system individually.
       
       | If you have made a mistake and want to remove a system from a set, select the set and the to be removed system, not systems!!, and under the **Action** button, slect *Remove from this Set*
       
       .. figure:: images/lab-021.png


#. Right-click on the *Greensafe Domain Controllers* set and click **Modify**

   .. figure:: images/lab-022.png

#. Under *Permissions*, click the **Add** button
#. Search for **PAS Admin Role** and click **Add**
#. Under PAS Admin Role permissions, assign **View** permissions
#. Click **Save**. This change will grant PAS Administrators permission to see the system set when they login
#. Use the main menu on the left to navigate to *Resources > Systems*
#. Right Click on the *Greensafe Windows Servers* set and click **Modify**
#. Under *Permissions*, click the **Add** button
#. Search for **PAS Admin Role** and **PAS Power User Role** click **Add**
#. Under each of the roles added, confirm the **View** permissions has been added
#. Click **Save**. This change will grant PAS Administrators and PAS Power Users permission to see the system set when they login
#. Use the main menu on the left to navigate to *Resources > Systems*
#. Right-click on the *Greensafe Unix Servers* set and click **Modify**
#. Under *Permissions*, click the *Add* button.
#. Search for **PAS Admin Role** and **PAS Power User Role** and click **Add**
#. Under each of the roles added, confirm the **View** permissions has been added.
#. Click **Save**. This change will grant PAS Administrators and PAS Power Users permission to see the system set when they login
#. Use the main menu on the left to navigate to *Resources > Systems*
#. Right Click on the *Greensafe Contractor Supported* set and click **Modify**
#. Under *Permissions*, click the **Add** button
#. Search for **PAS Admin Role** and **PAS Power User Role** and click **Add**
#. Under each of the roles added, confirm the **View** permissions has been added.
#. Click **Save**. This change will grant PAS Administrators and PAS Power Users permission to see the system set when they login

   .. note::
       Now that permissions are assigned to view the set, let’s assign permissions to members of specific sets.

#. Use the main menu on the left to navigate to *Resources > Systems*
#. Right-click on the *Greensafe Unix Servers* set and click **Modify**
#. Under *Member Permissions*, click the** Add** button
#. Search for **Team_UnixAdmins** and click **Add**
#. Under the *Team_UnixAdmin* Permissions, confirm the **View** permissions has been added.
#. Click **Save**
#. Use the main menu on the left to navigate to *Resources > Systems*
#. Right Click on the *Greensafe Contractor Supported* set and click **Modify**
#. Under *Member Permissions*, click the **Add** button
#. Search for **Contractor Role** and click **Add**
#. Under the *Contractor Role* Permissions, confirm the **View** permissions has been added.
#. Click Save.

   .. note::
       Now permissions have been assigned to specific groups to see specific sets. We have also assigned member permissions to specific groups so individual system permissions do not need to be assigned individually. Now let’s confirm the permissions, using the same accounts we worked with at the beginning of the exercise.

#. Using Google Chrome Menu, establish a New Incognito Window so you can login as each of the users (on the following page) to confirm the information in the table.

   .. list-table::
            :widths: 5 5 10 40 40
            :header-rows: 1
         
            * - Username
              - AD Group
              - Centrify Role
              - Available Systems
              - Available Sets
            * - jmiller@greensafe.lab
              - Domain Admins
              - PAS Admin Role
              - apps-server.greensafe.lab, apps-unix.greensafe.lab, db-server.greensafe.lab, db-unix.greensafe.lab, dc.greensafe.lab
              - Greensafe Domain Controllers, Greensafe Windows Servers, Greensafe Unix Servers, Greensafe Contractor Supported
            * - bhughes@greensafe.lab
              - Team_Helpdesk
              - PAS Power User Role
              - apps-server.greensafe.lab, apps-unix.greensafe.lab, db-server.greensafe.lab, db-unix.greensafe.lab, dc.greensafe.lab
              - Greensafe Windows Servers, Greensafe Unix Servers, Greensafe Contractor Supported
            * - krogers@greensafe.lab
              - Team_UnixAdmins
              - Pas User Role
              - apps-unix.greensafe.lab, db-unix.greensafe.lab,
              - No sets
            * - zContractor@labguide
              - N/A CDS User 
              - Contractors Role
              - db-server.greensafe.lab, db-unix.greensafe.lab
              - No sets
            * - lbennett@greensafe.lab 
              - Team_Contractors
              - Contractors Role
              - db-server.greensafe.lab, db-unix.greensafe.lab
              - No sets
   
   .. note::
       As you can see, permissions can be granted to systems without giving access to view the set or by granting permission to each system individually.


Configure Multifactor Authentication for Privilege Elevation
************************************************************

In this exercise, Alex (you) will configure systems to validate users with multifactor authentication when logging in at the console or when using a 3rd party remote access tool.

#. Let’s start by downloaded the *IWA certificate* needed to configure the systems for MFA
#. Using the *Centrify Identity Platform*, login as Alex Foster (afoster), or switch back to the Chrome UI where the user is still logged in.
#. Use the main menu on the left to navigate to *Settings > Network > Centrify Connectors*

   .. figure:: images/lab-023.png

#. Click the **apps-server** Centrify Connector
#. Click **IWA Service**
#. Click the Blue link **Download your IWA root CA certificate** ans save the file

   .. note::
       When the Warning is mentioned, click **Keep**

#. Click **Cancel** to close the properties of the Connector
#. Let’s now configure the Centrify Identity Platform Authentication Profile for client side login with MFA
#. Use main menu on the left to navigate to *Settings > Authentication > Authentication Profiles*
#. Click **Add Profile**
#. Name the Profile **CSS_MFA_Profile**
#. Set *Challenge #1* equal to **Security Question > 1**
#. Set the *Challenge Pass-Through Duration* to **No Passthrough**

   .. figure:: images/lab-024.png

#. Click **OK** to save the new profile
#. Let’s now configure the Centrify Identity Platform Privilege Role for client side login with MFA
#. Use the main menu on the left to navigate to **Access > Roles**
#. Click **Add Role**
#. Name the new role **CSS_MFA_Role**
#. Click **Members**
#. Search for and add the following **AD Groups** and **Computers** (make sure you have *Computers* checked!)

   - db-unix.greensafe.lab
   - db-server.greensafe.lab
   - Team_Contractors
   - Team_Helpdesk
   - Team_IT
   - Team_UnixAdmins

   .. figure:: images/lab-025.png

#. Click **Administrative Rights**
#. Click **Add**
#. Click and select **Computer Login and Privilege Elevation** and click **Add**

   .. figure:: images/lab-026.png

#. Click **Save**
#. Let’s now configure the Centrify Identity Platform Policy for client side login with MFA
#. Use the main menu on the left to navigate to *Access > Policies*
#. Click **Add Policy Set**
#. Name the new policy **CSS_MFA_Policy**
#. Under *Policy Assignment*, click *Specified Roles* and add the **CSS_MFA_Role**

   .. figure:: images/lab-027.png

#. Expand *Authentication*
#. Expand *Centrify Server Suite Agents*
#. Click **Linux, Unix, and Windows Servers**
#. Use the drop-down menu and select **Yes** to enable the authentication policy controls
#. Use the drop-down menu to change the *Default Profile* to **CSS_MFA_Profile**

   .. figure:: images/lab-028.png

#. Click *Privilege Elevation*
#. Use the drop-down menu and select **Yes** to enable the authentication policy controls
#. Use the drop-down menu to change the Default Profile to **CSS_MFA_Profile**

   .. figure:: images/lab-029.png

#. Click **Save** to save the policy
#. Let’s now configure GPO to push the certificate to all systems
#. Open **Group Policy Management Editor**

   .. note::
       If the Group Policy Management Editor has been closed, or not available, open a MMC and add the Group Policy Management Editor snapin.
       When asked for the *Browse for a Group Policy Object*, select *Centrify.greensafe.lab > Centrify GPO* and click **OK**, **Finish** and **OK**

       .. figure:: images/lab-030.png

#. Navigate to *Computer Configuration > Policies > Windows Settings > Security Settings > Public Key Policies*
#. Right-click the *Trusted Root Certificate Authorities* and select **Import**

   .. figure:: images/lab-031.png

#. Click **Next**
#. Click **Browse** and select the IWA certificate downloaded earlier (common location is *Downloads*)
#. Click **Next**
#. Confirm the store location (*Trusted Root Certificate Authorities*) and click **Next**
#. Click **Finish** and **OK** on the successful import message
#. Let’s now configure an existing command right to require MFA
#. In *Access Manager*, expand to **Zone > Global Zone > Child Zone > Unix Zone**
#. Expand **Authorization**
#. Expand **Unix Right Definitions**
#. Under *Commands*, double click on the **Service Restart** Command Right created earlier in the course
#. Click the **Attributes** Tab
#. Select *Re-authenticate current user* and **UNCHECK use password** and **CHECK Require multi-factor authentication**

   .. figure:: images/lab-032.png

#. Click **OK** to save the changes
#. Let’s now update the group policies on systems and test the MFA settings
#. Launch **PuTTY** and login to **db-unix** with the following credentials:
   
   - **Username:** root
   - **Password:** *Provided by Trainer*

#. Run **adflush** to clear the zone cache
#. Run **adgpupdate** to update the group policies on the system
#. Logout of the session
#. Relogin to the **db-unix** system using the credentials below:

   - **Username:** lbennett@greensafe.lab
   - **Password:** *Provided by Trainer*

#. Was Laura Bennett permitted to login?
#. Run dzdo systemctl restart firewalld
#. Was Laura Bennett permitted to run this command?

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#80BB01">This concludes this lab</font>
    </CENTER>

.. TODO:
    Need to figure out why the MFA is not working for jbennett... Also no Secret Questions has been defined!!!
