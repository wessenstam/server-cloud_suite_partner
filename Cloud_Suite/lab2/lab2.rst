.. _l2:

--------------------
Install Cloud Client
--------------------

Introduction
------------

This second lab will cover:

1. Prepare for Client Installation
2. Install Cloud Client on Windows Server
3. Enroll Cloud Client with CIP
4. Install Cloud Client on Linux Server
5. Enroll Cloud Client with CIP
6. Create Login from CIP

.. note::
    Estimated time to complete this lab: **60 minutes**

------

Systems used in this lab:

- apps-server.greensafe.lab
- cloud-win-server
- cloud-linux-server
- \https://<tenant>.my.centrify.net

------

Prepare for Client Installation
*******************************

1. Login to **cloud-win-server** using the following **Local** credentials:

   • **Username:** Administrator
   • **Password:** provided by trainer

2. Launch **Google Chrome** from Desktop and navigate to your unique CIP URL, **\https://<tenantID>.my.centrify.net**
3. Login to CIP using your admin credentials
4. From main menu, navigate to **Settings > Enrollment > Enrollment Codes**

   .. figure:: images/lab-001.png

5. In **Enrollment Codes** page, click **Add** button

   .. figure:: images/lab-002.png

6. Under **Owner**, click on **Select** button.
7. Choose **System Administrator** Role from the list.
8. Click **Select**
9. **Save**

   .. figure:: images/lab-003.png

10. Click **Copy**, to copy the enrolment code to clipboard. **This will be used to enroll Cloud Clients**.

    .. figure:: images/lab-004.png

Install & Enroll Cloud Client on Windows Server
***********************************************

1. In **cloud-win-server**, navigate to **downloads** folder and launch Centrify Client installer (**cagentinstaller-<version>**)

   .. figure:: images/lab-005.png

2. On the *Welcome Page*, click **Next**
3. On the *EULA* page, *check* the box (*I Accept the terms in the license agreement*) and click **Next**
4. In Enrollment Parameters page, type your unique CIP URL (\https://<tenant>.my.centrify.net) in the first field
5. **Paste** the enrollment code from clipboard in the second field (Enrollment Code).
6. Keep *Optional Parameters* field empty.
7. Click **Next**

   .. figure:: images/lab-006.png

8. Click **Install**

   .. figure:: images/lab-008.png

9. After successful installation, click **Finish**
10. Keep Cloud-win-server session active. You will use the session in the next step.

.. note:: 
    To verify a successful enrolment, **cloud-win-server** must be added automatically and available in systems list in **The Portal**. Reopen Chrome, in The Portal and navigate to **Resources > System**. You should see the windows server listed.

Install & Enroll Cloud Client on Linux Server
*********************************************

1. While in **cloud-win-server**, open *Putty* available on Desktop and connect to cloud-nix-server using the following details:
   
   • **IP Address:** 10.0.0.37
   • **Username:** root
   • **Password:** provided by trainer

2. Navigate to (temp) directory and check it contains client package using the following command:

   .. code-block:: bash
       
       cd temp 
       ls    

   .. figure:: images/lab-010.png

3. To start the installation, use the following command

   .. code-block:: bash
       
       rpm -Uvh CentrifyCC-<version>.rpm

   .. figure:: images/lab-011.png


4. To enroll the server, type the following command:

   .. code-block:: bash
       
       cenroll -t https://<tenant>.my.centrify.com -c <paste the same enrolment code used earlier> -F all

   .. figure:: images/lab-012.png

   .. Note:: 
       Linux Server logins using Directory accounts requires extra steps compared to windows.

5. Download the SSH Master Key file from the Portal to the Linux server, using the following command.

   .. code-block:: bash
       
       curl -o /etc/ssh/centrify_tenant_ca.pub https://<tenantID>/servermanage/getmastersshkey

   .. figure:: images/lab-013.png

6. Modify the SSHD configuration file for the client, type the following command:

   .. code-block:: bash
       
       vi /etc/ssh/sshd_config

7. Locate **Challenge Response Authentication** and change it to **yes**

   .. code-block:: bash
       
       ChallengeResponseAuthentication yes
       UsePam Yes


8. Add the following to the file:

   .. code-block:: bash
       
       TrustedUserCAKeys /etc/ssh/centrify_tenant_ca.pub

   .. figure:: images/lab-014.png

9. **Write and quit** by clicking *Escape* button on keyboard > type **wq!** > hit **Enter**

.. Note:: 
    To verify a successful enrolment, **cloud-nix-server** must be added automatically and available in systems list in **The Portal**. Reopen Chrome, in CIP and navigate to **Resources > System**. You should see the Linux server listed.


Agent Authentication Login
**************************

Windows Server
^^^^^^^^^^^^^^

1. While in CIP Portal, navigate to **Resources > Systems**

   .. figure:: images/lab-015.png

2. In the system list, Click on the windows server object name (**wins2019s**)
3. Click on **Permissions**.
4. Click **Add**

   .. figure:: images/lab-016.png   

5. Type (**Contractor Role**) in the search box, **check the box** next to it once it appears.
6. Click **Add**

   .. note:: 
       The search is case sensitive.

   .. figure:: images/lab-017.png   

7. In the **Permissions** list, Check **Agent Auth** for the **Contractor Role**

   .. figure:: images/lab-018.png   

   .. Note:: 
       Agent Auth allows the **Contractor Role** member **users** to authenticate to the servers leveraging the client installed on it as themselves using a feature (**Use My Account**)

8. Switch to **Chrome Incognito** Windows and login to CIP Portal as:

   • **Username:** zcontractor@labguide
   • **Password:** Provided by trainer

9. Navigate to **Resources > Systems**
10. Right Click on Windows Server object (**wins2019s**).
11. Click Use **My Account**

    .. figure:: images/lab-019.png

12. After a successful automatic login to the system, open **start > computer management**

    .. figure:: images/lab-020.png

13. Click on **Local User and Groups > Users**
14. Note that the users list now contains (**zcontractor**) as a local user. This user was **auto created** by the client upon (Use My Account) step.
15. Double click on the user to open properties, click Member Of tab.

    .. Note:: 
        The **zcontractor** was added to two groups, Remote Desktop Users & Users. This means this is a standard user with no administrative rights on the windows server.

    .. figure:: images/lab-021.png

16. **Sign out** of the windows server session.
17. Switch back to **Normal Chrome** session with **admin** login to **CIP Portal**.
18. Navigate to **Resources > Systems**
19. Click on the Windows server object (**wins2019s**)
20. Click on **Local Group Mapping**
21. Click **Add** button

    .. figure:: images/lab-022.png

22. click **Select** button
23. Check **System Administrator**
24. click **Select**
25. Under **Local Groups** click the **Add** button
26. Type **Administrators**
27. Click **Add**

    .. figure:: images/lab-022.png

28. Click **Ok**
29. Click **Permissions**

    .. figure:: images/lab-023.png

30. Check **Agent Auth** for **System Administrator** Role.
31. Click on *Actions* and Select **Use My Account**

    .. figure:: images/lab-024.png

32. You will be auto logged in to the server with CIP Portal Admin Account. Note that this account membership on the server is different. This account must be member of **Local Administrators** group.

    .. figure:: images/lab-025.png

Linux Server
^^^^^^^^^^^^

1. While in **The Portal** logged in as **Admin** user, navigate to **Resources > Systems**
2. Click on the Linux system object (*rhel7sx64*).
3. Click *Settings*, scroll down and *check (Use My Account is configured on this system)*

   .. figure:: images/lab-026.png

4. Click on **Permissions > Add**
5. Search for (**Contractor Role**)

   .. figure:: images/lab-027.png

6. Check the box, click **Add**
7. Check **Agent Auth** box for **Contractor Role**
8. **Save**
9. Switch to **Chrome Incognito** session, Refresh the page or login using **zcontractor** again if session was logged out.
10. Navigate to **Resources > Systems**.
11. Right click on linux system (**rhel7sx64**)
12. Click on **Use My Account**

    .. figure:: images/lab-028.png

13. You will be auto logged in using **zcontractor** account. Home Directory auto created.

    .. figure:: images/lab-029.png

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>