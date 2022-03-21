.. _l10:

------------------------
Auditing and reporting
------------------------

Introduction
------------

This tenth lab will cover:

1. Install Auditing and Reporting
2. Configure Auditing and Reporting
3. Review Audit sessions
4. Configure Centrify Reporting Service
5. Review Centrify Reporting


.. note::
    Estimated time to complete this lab: **60 minutes**

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab
- apps-unix.greensafe.lab
- db-server.greensafe.lab
- db-unix.greensafe.lab

------

Installing Audit Architecture
*****************************

Greensafe is required to have audit records of sessions and users. In this exercise, Alex (you) will install and configure the Centrify Audit and Monitoring components for host-based auditing.

#. On the **apps-server** use Windows Explorer to navigate to **C:\\Share\\CSS2021**
#. Launch the **autorun** application
#. Click **Audit and Monitor**

   .. figure:: images/lab-001.png

#. Click **Next** at the Welcome Message
#. *Accept the EULA* and click **Next**
#. Maintain the default features and click **Next**
#. Maintain the default installation folder and click **Next**
#. Review the installation options and click **Next**
#. When the installation is completed, Click **Finish**
#. The Audit Configuration Wizard will launch automatically. Click **Next** at the *Welcome Message*
#. Click **Next** to create a new installation

   .. figure:: images/lab-002.png

#. Using Windows Explorer to navigate to *C:\\Share* and open the **Training License Keys.txt**
#. Copy the **Audit License Key (DirectAudit)** to the clipboard
#. Paste the key in the space provided in the Configuration Wizard and click **Add**
#. Click **Next**
#. Maintain the default publication location and click **Next** 
#. Click Use an existing SQL Server instance and use the drop-down menu to Browse for the SQL Server

   .. figure:: images/lab-003.png

#. Click the Network tab. Be patient while the network is browsed for available SQL servers
#. Click **DB-SERVER\\CENTRIFY**
#. Click **OK**
#. Once the SQL Server is selected, click **Next**. This step will take approx. 2 minutes
#. Click **Finish**
#. Close the Installation Wizard by clicking **Exit**

Configure Centrify Auditing
***************************

In this exercise, Alex (you) will configure Audit Roles and configure the host-based auditing.

#. Using the desktop shortcut, **launch Audit Manager**

   .. figure:: images/lab-004.png

#. Expand the **DefaultInstallation**
#. Expand **Audit Roles**. There is a default role (Master Role). We will now add the Security Team as Master Auditors.
#. Right-click the *Master Auditor* and click **Assign users and Groups**

   .. figure:: images/lab-005.png

#. Add **Team_Security** and click **OK**. 
#. We will now create a secondary role for the Auditors team and grant them all permissions *except the ability to delete recorded sessions*
#. Right-click on *Audit Roles* and click **Add Audit Role**
#. Name the audit role **Greensafe Auditors**
#. Click **Next**
#. Maintain all selected machine types and criteria settings and click **Next**
#. **Uncheck** the **Delete** privilege and click **Next**

   .. figure:: images/lab-006.png

#. Review the summary and click **Next**
#. Once completed, click **Finish** to assign users and groups to the new role.
#. Add **Team_Auditors** and click **OK**
#. Let’s now configure systems inside the AD environment for Host Based Auditing. Use the Skytap Navigation to login to the *db-server.greensafe.lab* server with the following credentials:

   - **Username:** afoster@greensafe.lab
   - **Password:** *Provided by Trainer*

#. Use the *Start Menu* to *launch* the **Agent Configuration**

   .. figure:: images/lab-007.png

#. Click **Add Service**
#. Select **Centrify Audit and Monitoring Service** and Click **OK**

   .. figure:: images/lab-008.png

#. Select *DefaultInstallation* and click **Next**
#. **Close** the Centrify Agent Configuration.
#. Let’s now prepare a Unix system for Host Based Auditing. Use the Skytap Navigation to return to the *apps-server.greensafe.lab* server.
#. Launch PuTTY and login to *db-unix.greensafe.lab* with the following credentials:
   
   - **Username:** root
   - **Password:** *Provided by Trainer*

#. Run the following command to install the Centrify DirectAudit Agent:

   .. code-block:: bash
       
       yum install CentrifyDA -y


   .. figure:: images/lab-009.png

#. Once completed, reboot the server using the ``reboot`` command

Review Audit Sessions
*********************

In this exercise, Alex (you) will then review the sessions, create specific queries and document sessions.

#. While still on the *apps-server.greensafe.lab* using the Google Chrome Incognito Window, login to the CIP with the following credentials:

   - **Username:** bhughes@greensafe.lab
   - **Password:** *Provided by Trainer*

#. Use the main menu on the left to navigate to *Resources > Systems*
#. Right-click on **db-server.greensafe.lab** and click **Enter Account**
#. Enter the following credentials to log into the server.

   - **Username:** bhughes@greensafe.lab
   - **Password:** *Provided by Trainer*

#. In the open session, use the start menu to *launch PowerShell* and run the following commands:

   - gpupdate /force
   - ipconfig

   .. figure:: images/lab-010.png

#. Once completed, **exit PowerShell**
#. Use the *Start Menu > Windows Administrative Tools > Windows Firewall and Advanced Security*
#. Logout of the session, *Start Menu > User Icon > Sign Out*

   .. figure:: images/lab-011.png

#. Let’s open another session using a UNIX system. Launch PuTTY and login to the db-unix.greensafe.lab server with the following credentials:
   
   - **Username:** lbennett@greensafe.lab
   - **Password:** *Provided by Trainer*

#. In the open session, execute the following commands:

   .. code-block:: bash

       cat /etc/passwd
       ifconfig
       clear
       history
       logout


#. Let’s review recorded audit sessions. Use the desktop shortcut to launch **Audit Analyzer**
#. Expand **Audit Sessions** and click **Today** to see a list of recorded sessions
#. Double click on the session for **db-server.greensafe.lab** for user *bhughes@greensafe.lab*
#. Let’s document this session so other auditors and management have the auditor’s notes. Click *Session > Update Review Status* and select **to be Reviewed**

   .. figure:: images/lab-012.png

#. Add notes related to the session:"witnessed.." and click **OK**. You can then *close* this session
#. Now let’s look at a UNIX session. Double click on the session for **db-unix.greensafe.lab**
#. Let’s document this session so other auditors and management have the auditor’s notes. UClick *Session > Update Review Status* and select **Pending for action**
#. Add notes and instructions of the actions that need to be taken and click **OK**. For example: "Security permissions need to be reviewed for this logged in user". You can now *close* this session
#. Let’s now group sessions based on specific executed commands. Right-click on **Audit Sessions** and select **New Private Query**

   .. figure:: images/lab-013.png

#. Name the new query **UNIX cat Command Execution**
#. Under *Definition Type*, **uncheck Windows systems**
#. Under *Criteria*, click the **Add** button
#. Use the *Attributes drop-down menu* to select **UNIX Output and Commands**
#. Use the *Criteria drop-down menu* to select **Contains any of...**
#. In the space provided, type **cat** (lowercase)
#. Click **OK**
#. Click **OK** to save the query
#. Under *Audit Sessions*, expand **Private Queries**

   .. figure:: images/lab-014.png

#. Click **UNIX cat Command Execution** 
#. The session where you have typed the ``cat`` command, lbennett@greensafe.lab, should be seen..

   .. figure:: images/lab-015.png

Configure Centrify Reporting Service
************************************

In this exercise, Alex (you) will configure Centrify Reporting Service to report on Centrify Server Suite management tasks.

#. Navigate to *Start Menu > Centrify Server Suite 2021.1 > Configuration Wizard*
#. Click **Next**
#. Under Database Type click **Next**
#. Use the *drop-down menu* and select for **Browse for more...**
#. Click the **Network Servers** tab
#. Select Use an Existing SQL Server Instance (**DB-SERVER\\CENTRIFY**) and click **OK**
#. Click **Next**. It may take a few moments before the next screen is presented!
#. Confirm the selection Deploy Centrify Reports and URL Addresses:

   - **Web Service URL:** \http://DB-SERVER /ReportServer_CENTRIFY
   - **Report Manager URL:** \http://DB-SERVER /Reports_CENTRIFY

#. Click **Next**. It may take a few moments before the next screen is presented!
#. Under *Synchronization Mode*, select *Zone-based mode* and click **Next**
#. Under *Hierarchical Zones*, select **Monitor all hierarchical zones...** and Click **Next**
#. Under *Classic Zones*, select **Monitor all classic zones...** and click **Next**
#. Under the *Domain Controllers*, click **Add**
#. Select in the Domain: **greensafe.lab** domain. The DC **dc-server.greensafe.lab** will be populated automatically, click **OK**

   .. figure:: images/lab-016.png

#. click **Next**
#. Under the *Synchronization Schedule*, maintain the default settings, making no changes and click **Next**

   .. figure:: images/lab-017.png

#. Under *Report Services Option*, Select *Use Built-In Account (Local System)* and click **Next**
#. Permissions will be verified, identifying successes and failures. Click **Close**

   .. figure:: images/lab-018.png

#. Under *Summary*, click **Next**. Please be patient as the database is configured. The process takes approx. minutes
#. Check the option to *Start synchronizing data from Active Directory* and click **Finish** to close the Report Configuration Wizard

   .. figure:: images/lab-019.png

#. Open Google Chrome and browse to http://DB-SERVER/Reports_CENTRIFY

   .. note::
       If you are being asked for login, use **afoster** with the password: *Provided by Trainer*

#. Confirm Centrify Report Services Folder is displayed. Leave the Browser window open to complete the next lab exercise

   .. figure:: images/lab-020.png


Review Centrify Reporting
*************************

In this exercise, Alex (you) will use Centrify Reporting Services and Centrify Identity Platform to examine specific reports.

#. From the Centrify Reporting Services (SRSS) website, click **Details View**

   .. figure:: images/lab-021.png

#. Click **Centrify Reporting Services**
#. Click **Access Manager Reports**
#. Click **Delegation Report**. This reports on AD groups with assigned Zone Delegation tasks
#. Under **Trustee filter**, *remove the check mark under Null* and enter in the space provided **cfyS_ZPA**

   .. figure:: images/lab-022.png

#. Click **View Report**. We delegated specific zone tasks to this account as part of automated provisioning through the ZPA and the results will be shown in this report. 

.. TODO: No builtin reports are available in the installed CIP! Did we forgot to do this???
    #. Close the web page and return to the *Centrify Identity Platform*, as Alex Foster
    #. Use the main menu on the left to navigate to *Reports*
    #. Expand **Builtin Reports**
    #. Expand **Security**
    #. Click **Users Security Question State**
    #. Click **OK** to view the report. This report will indicate who has and who has not satisfied the MFA challenge the company now requires to access company servers.
    #. Use the main menu on the left to navigate to *Reports*
    #. Expand **Builtin Reports**
    #. Expand **Effective Rights**
    #. Expand **Role to Object**
    #. Click **Systems**
    #. Select a system in the list to view the current role-based privilege that has been granted to the single system. This will help determine if too much privilege is being granted to critical systems.

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#80BB01">This concludes this lab</font>
    </CENTER>

