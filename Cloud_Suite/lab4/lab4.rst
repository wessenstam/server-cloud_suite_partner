.. _cl4:

----------------------
Extras for Cloud Suite
----------------------

Introduction
------------

This fourth lab will cover:

1. Apply MFA Everywhere
2. Unenroll and reenroll clients
3. Review Audit Sessions

.. note::
    Estimated time to complete this lab: **20 minutes**

------

Systems used in this lab:

- cloud-win-server
- cloud-linux-server
- \https://<tenant>.my.centrify.net

------

Apply MFA Everywhere
********************

Cloud Suite / CIP portal provides MFA requirements on the following:
1. Portal login
2. Portal Based Remote Login
3. Privilege Elevation for both Cloud Client & Server Suite agent
4. Host-based system login for both Cloud Client & Server Suite Agent
In the previous labs, you have configured MFA at Portal login & MFA at Cloud Client Privilege Elevation. In this lab you will configure the rest of MFA available options.

Portal Based Remote Login
^^^^^^^^^^^^^^^^^^^^^^^^^

1. While logged in The Portal using Admin credentials, navigate to **Resources > Systems**
2. Click on the Linux system (**rhel7sx64**)
3. Click on **Policy**

   .. figure:: images/lab-001.png

4. Under **Default System Login Profile (used if no conditions matched)**, select **Contractors MFA Profile**

   .. figure:: images/lab-002.png

5. **Save**
6. Switch to **Chrome Incognito** session and login as **zcontractor@labguide** user
7. From main menu on the left, navigate to **Resources > Systems**
8. Right click the Linux system (**rhel7sx64**) and click **Use My Account**

   .. figure:: images/lab-003.png

9. You will be prompted to enter your credentials again.

   .. figure:: images/lab-004.png

   .. figure:: images/lab-005.png

10. Provide the response and Click **Next**
11. Close the session after successful login to Linux Server.
12. Repeat **Steps 2 – 11** on the Windows server.

Host Based System Login – Cloud Client
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. While in The Portal logged in as Admin, in the main menu on the left navigate to **Access > Policies**

   .. figure:: images/lab-006.png

2. Click on **Contractor Policy**
3. Expand **Authentication > Centrify Clients > Login**
4. Select **Yes** from dropdown list next to **Enable authentication policy controls**
5. Select **Contractor MFA Profile** from dropdown list under **Default Profile (used if no conditions matched)**
6. **Save**

   .. figure:: images/lab-007.png

7. In **Skytap** portal , click on the **server name** to launch console access (**cloud-RHEL-server**)

   .. figure:: images/lab-008.png

8. To login to the server, use the following credentials:

   a. **Username:** zcontractor@lab.<tenant>
   b. **Password:** Provided by the trainer
9. You will be prompted to choose one of the available MFA options, **type the number** that corresponds the MFA mechanism you prefer to choose and hit **Enter**

   .. figure:: images/lab-009.png

10. Repeat **Steps 7-9** to test MFA at **Windows** Server Console login (**Cloud-win-server**), using same *zcontractor@lab.<tenant>*

    .. figure:: images/lab-010.png

Unenroll & Re-enrol Cloud Client
********************************

In a previous chapter, we have used the Wizard to enrol Windows Server with The Portal. In some cases, you may need to unenroll the client and re-enrol it. In this lab we will un-enroll and re-enrol Cloud Client using command line interface.

1. From Skytap portal, open (cloud-win-server) console and login using the following credentials:
   
   a. **Username:** Administrator
   b. **Password:** Provided by the trainer.

2. From **start menu**, launch **CMD** as **administrator**.
3. Navigate to cagent folder using the following path

   .. code-block:: powershell

       cd "C:\Program Files\Centrify\cagent"

   .. figure:: images/lab-011.png


4. To unenroll, type the following command. The user provided is your tenant admin user account.

   .. code-block:: powershell

       cunenroll.exe -d -u <your-tenant-admin-user>

5. The system will be successfully **unenrolled**.

   .. figure:: images/lab-012.png

6. Open The Portal and refresh, navigate to **Resources > Systems**. The system no longer exists.

Re-enrol the windows server:
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

7. While in CMD session on the windows server, type the following command:

   .. code-block:: powershell

       cenroll.exe -F all -t <your-tenant-url> -u <your-tenant-admin-user>>

   .. figure:: images/lab-013.png

   .. Note:: 
       You can use the registration code to enrol the system by replacing ( **-u** ) switch with ( **-c** ) followed by the registration code retrieved from The Portal.

       .. code-block:: powershell

           cenroll.exe -F all -t <your-tenant-url> -c <registration-code>

8. Refresh The Portal and navigate to **Resources > Systems** page to see the newly created windows server.

Review Portal Based – Gateway Audits
************************************

1. Login to *apps-server* using **afoster** credentials
2. Launch **Audit Manager** by click on the icon available on the Desktop
   
   .. figure:: images/lab-014.png

3. To View the list of systems were audited via CIP Portal, Click on **DefaultInstallation > Audited Systems (Vault-based)**

   .. figure:: images/lab-015.png

4. **Close** Audit Manager
5. To replay Recorded sessions, Launch **Audit Analyzer** by click on the icon available on the Desktop

   .. figure:: images/lab-016.png

6. Expand Audited Sessions
7. Choose Today filter

   .. figure:: images/lab-017.png

   .. figure:: images/lab-018.png


.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>