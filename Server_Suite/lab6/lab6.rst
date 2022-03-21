.. _l6:

-----------------
Configuring Roles
-----------------

Introduction
------------

This sixth lab will cover:

1. Configuring and testing Unix Login Roles
2. Configuring and testing Windows Zone Roles
3. Configuring and testing Computer Roles

.. note::
    Estimated time to complete this lab: **60 minutes**

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab
- db-unix.greensafe.lab
- apps-unix.greensafe.lab

------

Configure and testing Unix Login Role
*************************************

As we have examined, privileged directory service users must have roles assigned to them before they can do anything on the system. This includes the login process. Roles can be assigned at different levels of the Centrify Zone structure – at zone levels, at computer group levels and at an individual server level. In this exercise, Alex (you) will create and assign a zone roles to permit privileged users to any system in the zone.

Creation
^^^^^^^^

#. Using Access Manager, expand the *UNIX Zone*
#. Expand *Authorization*, right-click on **Role Assignments** and select **Assign Role...**
#. Locate and select the **UNIX Login** for the *greeensafe.lab/Centrify/GLobal Zone/UNIX Zone*. Widen the *Zone* column to select the correct Zone

   .. figure:: images/lab-001.png

#. Click **OK**
#. Click **Add AD Account...**
#. Add the following *AD Groups* to this role assignment (type *Team_* and click **Find Now** to speed it up)

   - Team_Contractors
   - Team_Finance
   - Team_Helpdesk
   - Team_IT
   - Team_Sales
   - Team_UNIXAdmins

#. Click **OK**
#. Click **OK**
#. Right-click on *db-unix* and select **Show Effective User Rights**

   .. figure:: images/lab-002.png

#. Use the *Role Assignments* Tab to confirm the effective rights for each AD user listed below (make sure you check **Show omitted users** option)
   
   .. list-table::
      :widths: 15 15 70
      :header-rows: 1
   
      * - Username
        - AD Group
        - Does this user have the right to login?
      * - afoster
        - Team_IT & Team_Security
        - Yes
      * - badams
        - Team_Sales
        - Yes
      * - kim
        - Team_Finance & Team_UNIXAdmins
        - Yes
      * - snguyen
        - Domain Users
        - No
      * - ahouston
        - Team_Auditors
        - No

   .. NOTE:: 
       The user Sam is displayed because the local profile is listed under the system’s user UNIX Data. Sam is listed as an omitted user, because a role has not been assigned. Amy Houston (ahouston) is not listed because the AD user has not been added as an authorized user of a zone or the local machine.

   .. figure:: images/lab-003.png

#. Click **Close** to close the *Effective UNIX User Rights*

Test the role
^^^^^^^^^^^^^

#. Open Putty and login to db-unix with the following credentials:
   
   - **Username:** root
   - **Password:** *Provided by Trainer*

#. Run the following command to clear the zone cache

   .. code-block:: bash
       
       adflush

   .. figure:: images/lab-004.png

#. Logout of the session using *ctrl+d*. This will also close the PuTTY session
#. Use PuTTY to confirm the effective rights found in the step 8 by logging in using the username as given. The password for all account is the same and is *Provided by Trainer*

   .. list-table::
      :widths: 15 15 70
      :header-rows: 1
   
      * - Username
        - AD Group
        - Could the user login to db-unix?
      * - afoster
        - Team_IT & Team_Security
        - Yes
      * - badams
        - Team_Sales
        - Yes
      * - kim
        - Team_Finance & Team_UNIXAdmins
        - Yes
      * - snguyen
        - Domain Users
        - No
      * - ahouston
        - Team_Auditors
        - No


Configure and testing Windows Zone Role
***************************************

Windows Roles are slightly different as privilege will come in the form of the use of specific applications. Generally, assigning privilege to a user to access an application or administer a system results in local identities on the system that have the necessary privilege or moving the AD user into a group that not only has elevated privilege to the individual system or the application, but instead to a group of systems and all applications. In this exercise, Alex (you) will create and assign roles to the Windows Zone that include the login and elevated privilege to run a specific windows application with privilege, without the need of a local identity or shared privileged account.

Creating a custom application right
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. On the apps-server open *Start Menu* and navigate and open *Windows Administrative Tools*
#. Launch *Windows Firewall and Advanced Security* 
#. Minimize the Firewall Window to leave it running. We will be using this later in the exercise
#. Using *Access Manager*, expand the *Windows Zone*
#. Expand *Authorization*
#. Expand *Windows Right Definitions*
#. Right-click on *Applications* and select **New Windows Application**

   .. figure:: images/lab-005.png

#. Name the *New Application* **Windows Firewall Management**
#. Click the *Match Criteria* Tab
#. Click **Add**
#. Click **Import Process...** on the bottom of the window
#. Under the *Import From Running Process*, select the **mmc.exe** *Image name* that relates to the command line for the Windows Firewall "C:\\Windows\\system32\\mmc.exe" "C:\\Windows\\system32\\WF.msc"

   .. figure:: images/lab-007.png

#. Click **OK**
#. Change the Description to **Windows Firewall** and Click **OK**

   .. figure:: images/lab-008.png

#. Click the **Run As** tab.
#. Click **Add AD Groups**
#. Search for and select **Domain Admins** and click **OK**
#. Click **OK** to Save the New Windows Application Right.

Create role and assign the Right
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Right-click on *Role Definitions* and select **Add Role**

   .. figure:: images/lab-010.png

#. Name the *New Role* **Firewall Management**
#. Click **OK**
#. Right-click the **Firewall Management** Role and select **Add Right**
#. Locate and Select **Windows Firewall Management**
#. Click **OK**


Assign Windows Login
^^^^^^^^^^^^^^^^^^^^

#. Right-click on *Role Assignment*s and select **Assign Role...**

   .. figure:: images/lab-011.png

#. Select *Windows Login* for the *greeensafe.lab/Centrify/GLobal Zone/Windows* Zone. Widen the Zone column to select the correct Zone.

   .. figure:: images/lab-012.png

#. Click **OK**
#. Click **Add AD Account...**
#. Add the following *AD groups* to this role assignment (type *Team_* and click **Find Now** to speed it up)

   - Team_Contractors
   - Team_Finance
   - Team_Helpdesk
   - Team_IT
   - Team_Sales

#. Click **OK** to save the role assignment

Assign Firewall Management Roles to privileged users
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Right-click on *Role Assignments* and select **Assign Role..**
#. Select **Firewall Management**
#. Click **OK**
#. Click Add **AD Account...**
#. Add the following AD Groups to this role assignment (type *Team_* and click **Find Now** to speed it up)

   - Team_Helpdesk
   - Team_IT

#. Click **OK** to save the role assignment.

Test the Windows roles
^^^^^^^^^^^^^^^^^^^^^^

#. Open db-server and login as Alex Foster. Once logged in, open PowerShell and type the following command to refresh the cache

   .. code-block:: PowerShell
    
      dzflush

   .. figure:: images/lab-013.png

#. We have already established that since Alex Foster is a domain admin, he has privilege to login and access the firewall
#. *Logout of db-server*
#. Log in as each of the users listed below to confirm the roles you have assigned, and open Windows Exporer and navigate to **C:\\Windows\\System32** and right-click WF > 
   
   .. list-table::
      :widths: 15 15 25 25 20
      :header-rows: 1
   
      * - User
        - AD Group
        - Can the user login?
        - Can the user see firewall settings?
        - Can the user see firewall settings with Privilege?
      * - bhughes
        - Team_Helpdesk
        - Yes
        - No
        - Yes
      * - badams
        - Team_Sales
        - Yes
        - No
        - No
      * - krogers
        - Team_Finance
        - Yes
        - No
        - No
      * - lbennett
        - Team_Contractors
        - Yes
        - No
        - No
      * - lscott
        - Team_IT
        - Yes
        - No
        - Yes

   .. note:: 
       Running the Windows Firewall without Privilege should result in the following message:
       
       .. figure:: images/lab-014.png

       To run the application with privilege, right-click on the application and select **Run With Privilege**

        .. figure:: images/lab-017.png

       If the user has been granted privilege via the *assigned role*, they should see the Windows Firewall options shown below

       .. figure:: images/lab-016.png


Configure Computer Roles
************************

The current zone structure has systems grouped by operating system, but not all systems have the same role within the organization. Computer roles are configured so privilege can be granted automatically when a new server is added to the role or removed when a system is retired or removed from the role. In this exercise, Alex (you) will configure a computer role that will grant privilege to users of server members of the role.

| Greensafe has made the decision to add additional database servers. The new servers will have the same configuration as db-unix.greensafe.lab but will be added over the course of several months. In order to ensure the configuration is completed ahead of time, the new computers will be pre-created and a computer role will be established.

Pre-create New Systems
^^^^^^^^^^^^^^^^^^^^^^

#. Using Centrify Access Manager, expand *Child Zones*
#. Expand *Unix Zone*
#. Right-click *Computers* and select **Prepare UNIX Computer**
#. Under *Prepare Computer*, maintain the default settings and click **Next**
#. Under *Specify the Computer*, click **Next** to add a *new computer object*
#. Name the computer **db2-unix**
#. Click **Change** to change the computer container
#. Navigate to *greensafe.lab > Centrify > Computers* and Click **OK**
#. Click **Next**
#. Under *Read Only Domain Controller Compatibility and License Type*, maintain the default settings and license selection and click **Next**
#. Under *SPN Configuration*, maintain the default settings and click **Next**
#. Under *Delegate Join Permissions*, maintain the default setting to allow the computer to join itself to the zone and click **Next**
#. Under *Delegate Machine Overrides*, click **Browse**
#. Search for and select **cfyA_Global_CentrifyAdmins**
#. Click **OK**
#. Click **Next**
#. Under *Delegate Permissions*, maintain the default settings and click **Next**
#. Click **Next** to confirm the configuration

   .. figure:: images/lab-018.png

#. Click **Finish**
#. *Repeat Steps 1-19* to pre-create **db3-unix** and **db4-unix**

Create AD Groups for the Computer Role
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Open Active Directory Users and Computers (ADUC).
#. Navigate to *Centrify > Computer Roles*
#. *Create a new AD group with a Global group scope* named **cfyC_Unix_Systems**

   .. figure:: images/lab-020.png

#. *Create* three additional AD groups with Global group scopes.

   - cfyU_Unix_UnixLogin
   - cfyU_Unix_ServiceMgr
   - cfyU_Unix_UnixAdmin

#. Open the *cfyU_Unix_UnixAdmin group* and **add** the following AD groups as members:

   - Team_Helpdesk
   - Team_IT
   - Team_UnixAdmins

#. Open the *cfyU_Unix_ServiceMgr* group and **add** the following AD groups as members.

   - Team_Contractors

#. Open the *cfyU_Unix_UnixLogin* group and **add** the following AD groups as members:

   - Team_Contractors
   - Team_Helpdesk
   - Team_IT
   - Team_UnixAdmins

#. Close ADUC

Create Command Rights
^^^^^^^^^^^^^^^^^^^^^

#. Using Access Manager, expand *Child Zone > Unix Zone*
#. Expand *Authorization*
#. Expand *Unix Right Definitions*
#. Right-click *Commands* and select **New Command**

   .. figure:: images/lab-021.png

#. *Name* the new command right **ALL** with a *description* of **Root Equivalent Command Rights**
#. Under *Command*, type an **asterisk (\*)**
#. Select *Specific Path* and type an **asterisk (\*)**

   .. figure:: images/lab-022.png

#. Click **OK**
#. Right-click *Commands* and select **New Command Right**
#. *Name* the new command right **Service Restart**
#. Under Command, type **systemctl restart\***
#. Select *Specific Path* and type an **asterisk (\*)**
#. Click **OK**


Create Privileged Role Definitions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Right-click on *Role Definitions* and select **Add Role**
#. Name the new role **UNIX Admin**
#. Click **OK**
#. Right-click on *Role Definitions* and select **Add Role**
#. Name the new role **Unix Service Manager**
#. Click **OK**

Add the Rights to the Roles
^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Right-click on the *UNIX Admin* Role in the *Role Definitions* sections and select **Add Right**

   .. figure:: images/lab-023.png

#. Select the **ALL** command right created earlier
#. Click **OK**
#. Right-click on the *UNIX Service Manager* Role and select **Add Right**
#. Select the **Service Restart** command right created earlier
#. Click **OK**

Create the Computer Role
^^^^^^^^^^^^^^^^^^^^^^^^^

#. Right-click *Computer Roles* and select **Create Computer Role**
#. Name the Computer Role **Greensafe_UNIX_Systems**
#. Use the drop-down menu under **computer groups** and select *<...>* to browse for the AD group
#. Search and select **cfyC_Unix_Systems**
#. Click **OK**

   .. figure:: images/lab-024.png

#. Click **OK** to save the computer role

Assign the Role Definitions to the Computer Role
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Navigate to *UNIX Zone > Authorization > Computer Roles > Greensafe_UNIX_Systems*
#. Right-click on *Role Assignments* and select **Assign Role**
#. Select *UNIX Login for Unix Zone* and click **OK** (widen the Zone column to select the correct Zone)
#. Click **Add AD Account...**
#. Search for the group **cfyU_Unix_UnixLogin** and select it
#. Click **OK**
#. Click **OK** to save the Role Assignment
#. Right-click on **Role Assignments** and select **Assign Role**
#. Select *UNIX Admin* and click **OK**
#. Click **Add AD Account..**
#. Search for group **cfyU_Unix_UnixAdmin** and select it
#. Click **OK**
#. Click **OK** to save the Role Assignment
#. Right-click on *Role Assignments* and select **Assign Role**
#. Select *UNIX Service Manager* and Click **OK**
#. Click **Add AD Account...**
#. Search for group **cfyU_Unix_ServiceMgr** and select it
#. Click **OK**
#. Click **OK** to save the Role Assignment
#. Your Role Assignments should look like this

   .. figure:: images/lab-025.png

Add System to the Computer Role
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
#. Under the *Greensafe_Unix_Systems Computer Role*, right click on members and select Add Computer

   .. figure:: images/lab-026.png

#. Search for and add all of the systems below:

   - db-unix
   - db2-unix
   - db3-unix
   - db4-unix

#. Click on *Members* and it should look like the below screenshot

   .. figure:: images/lab-027.png

Check Effective Rights and Test Roles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Right-click on the CHild Zone *UNIX Zone* and select **Effective Unix User Rights** to check the configuration (Use the *Role Assigment* and the *Commands* tabs to see the information):

   .. list-table::
      :widths: 10 20 10 30 30 
      :header-rows: 1
   
      * - Username
        - AD Group
        - Server
        - Can the user login? (Unix Login Role Assigments tab)
        - Can the user Restart Services? (Commands Tab)
      * - bhughes
        - Team_Helpdesk
        - db2-unix
        - Yes
        - Yes
      * - badams
        - Team_Sales
        - db2-unix
        - Yes
        - No
      * - krogers
        - Team_Finance & Team_UNIXAdmins
        - db2-unix
        - Yes
        - Yes
      * - lbennett
        - Team_Contractors
        - db2-unix
        - Yes
        - Yes
      * - ahouston
        - Team_Auditors
        - db2-unix
        - No
        - No

   .. figure:: images/lab-029.png

   .. figure:: images/lab-028.png

#. Close *Effective Unix User Rights**

Test the configured roles
^^^^^^^^^^^^^^^^^^^^^^^^^

#. Use PuTTY to login to the db-unix server to confirm the results listed below: Use the command 

   .. code-block:: bash

       dzdo systemctl restart sshd


   .. list-table::
      :widths: 10 20 10 30 30 
      :header-rows: 1
   
      * - Username
        - AD Group
        - Server
        - Can the user login? (Unix Login Role Assigments tab)
        - Can the user Restart Services? (Commands Tab)
      * - bhughes
        - Team_Helpdesk
        - db-unix
        - Yes
        - Yes
      * - badams
        - Team_Sales
        - db-unix
        - Yes
        - No
      * - krogers
        - Team_Finance & Team_UNIXAdmins
        - db-unix
        - Yes
        - Yes
      * - lbennett
        - Team_Contractors
        - db-unix
        - Yes
        - Yes
      * - ahouston
        - Team_Auditors
        - db-unix
        - No
        - No

#. Logged in as lbennett, execute the following command:

   .. code-block:: bash

       dzdo cat /etc/shadow

   .. figure:: images/lab-030.png

#. This demonstrates how the role permits just enough privilege to restart services, but not run other elevated commands

   .. note::
       The command **dzdo** is the Centrify \`sudo\` implementation with extra options. If the user lbennet tries to use **sudo**, there is an error that the user is not in the sudoers files and therefore can NOT run any privileged commands. Try **sudo systemctl restart sshd** and you will see the sudoers error
   
       .. figure:: images/lab-031.png
   
.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>