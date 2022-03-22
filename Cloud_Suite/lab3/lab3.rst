.. _cl3:

------------------------------------------
Least Privilege / Privilege Elevation, MFA
------------------------------------------

Introduction
------------

This third lab will cover:

1. Configure privilege elevation for Windows
2. Configure privilege elevation for Linux
3. Configure MFA requirement at elevation

.. note::
    Estimated time to complete this lab: **30 minutes**

------

Systems used in this lab:

- cloud-win-server
- cloud-linux-server
- \https://<tenant>.my.centrify.net

------

Privilege Elevation for Windows
*******************************

The Cloud Client installed on windows server provides privilege elevation capabilities. In the previous chapter, you have configured a CIP/Client based logins to windows server as a standard user with no administrative permissions on the server for the zcontractor user. The contractor as part of his role may need to view security events and resource and performance monitor only. In this lab, you are going to grant him the needed enough privileges in a form of privilege elevation.

Create Elevation Commands
^^^^^^^^^^^^^^^^^^^^^^^^^

1. Launch Google Chrome, login to CIP Portal as admin.
2. From the main menu on the left, navigate to **Settings > Resources > Privilege Elevation command**

   .. figure:: images/lab-001.png

3. Click **Add**
4. Fill in the following Information:

   • **Name:** Event Viewer
   • **Description:** Elevate Event Viewer to View Security Logs
   • **Command:**

   .. code-block:: powershell

       "C:\Windows\system32\mmc.exe" "C:\Windows\system32\eventvwr.msc" /s

   .. figure:: images/lab-002.png

5. **Save**
6. Repeat **Steps 3-5** to add another **Windows** command with the following info:
   
   • **Name:** Resource Monitor
   • **Description:** Elevate Resource & Performance Monitor Console
   • **Command:**

   .. code-block:: powershell

       "C:\Windows\system32\perfmon.exe" /res

7. Now your privilege Elevation Command List should include two windows type commands.

   .. figure:: images/lab-003.png


Assign commands to system(s)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. From the main menu on the left, Navigate to **Resources > Systems**

   .. figure:: images/lab-004.png

2. Click on the Windows server (**wins2019s**)
3. Click on **Privilege Elevation**
4. Click **Add**

   .. figure:: images/lab-005.png

5. In Search **Command or Application** window, Select **Event Viewer**

   .. figure:: images/lab-006.png

6. Click **Next**
7. In **Select User, Group, or Role** window, Search for **Contractor Role** and **select it**
8. Click **Add**
9. Repeat **Steps 3-8** to add **Resource Monitor Command** to *Contractor Role*.
10. Next to **Resource Monitor**, Check **Bypass MFA**
11. **Save**
12. The results:

    .. figure:: images/lab-007.png

Apply MFA at Elevation Rule as policy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. In the same system page, click **Policy** on the left.

   .. figure:: images/lab-008.png

2. Scroll down to the end of the page.
3. From **Default Privilege Elevation Profile (used if no conditions matched)** dropdown list, select **Contractors MFA Profile**
4. **Save**

   .. figure:: images/lab-009.png

Test Privilege Elevation
^^^^^^^^^^^^^^^^^^^^^^^^

1. Switch to/launch **Chrome incognito**, login to **The Portal** as **zcontractor**.
2. Navigate to **Resources > Systems**.
3. Right Click Windows Server (**wins2019s**)
4. Click **Use My Account** to login to the server.
5. Open **Windows Administrative tools** from **Start Menu**

   .. figure:: images/lab-010.png

6. Double click **Event Viewer** to launch it.
7. Navigate to **Windows Logs > Security**.
8. Note that as a standard user you’re **not allowed** to view the events.

   .. figure:: images/lab-011.png

9. Close Event Viewer window
10. In **Windows Administrative Tools** page, Right Click on **Event Viewer**, Click **Run as Administrator**

    .. figure:: images/lab-012.png

11. In UAC Prompt, Keep the default **Run with Privilege**
12. Click **Yes**

    .. figure:: images/lab-013.png

13. Based on the MFA Profile we assigned earlier, you will be prompted to reenter your **zcontractor** password and second factor (Security Question or Mobile Authenticator App).
14. Enter your credentials and click **Yes**

    .. figure:: images/lab-014.png
        
    .. figure:: images/lab-015.png

15. In the event viewer console, navigate to **Windows Logs > Security**.
16. Note that you have access to view the security events.

    .. figure:: images/lab-016.png

17. Repeat Steps **6-15** to test **Resource Monitor** Console Elevation
18. Note that you will gain access **without MFA** requirement, you have checked **Bypass MFA **for this command!


Privilege Elevation for Linux
*****************************

Create Elevation Commands
^^^^^^^^^^^^^^^^^^^^^^^^^

1. Launch Google Chrome, login to CIP Portal as admin.
2. From the main menu on the left, navigate to **Settings > Resources > Privilege Elevation command**

   .. figure:: images/lab-017.png

3. Click **Add**
4. Under *Operating System*, Select **Linux**

   .. figure:: images/lab-018.png

5. Fill in the following Information:

   • **Name:** SSH Config File - Edit
   • **Description:** Elevate to edit sshd server configuration file
   • **Command:**

     .. code-block:: bash

         vi /etc/ssh/sshd_config

6. Under *Match Criteria*, Select **Standard User Path**

   .. figure:: images/lab-019.png

7. **Save**
8. Repeat Steps **3 -6** to add another command, use the following information

   • **Name:** SSH Service - Restart
   • **Description:** Elevate to allow restart sshd service
   • **Command:**

    .. code-block:: bash

         systemctl restart sshd

9. Under *Match Criteria*, Select **Standard User Path**
10. **Save**

Assign commands to system(s)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. From the main menu on the left, Navigate to **Resources > Systems**

   .. figure:: images/lab-020.png

2. Click on the windows server (**rhel7sx64**)
3. Click on **Privilege Elevation**
4. Click **Add**
5. In **Search Command or Application Window**, Select **SSH Service – Restart**
6. Click **Next**

   .. figure:: images/lab-021.png

7. In **Select User, Group, or Role** window, Search for **Contractor Role** and **select** it
   
   .. figure:: images/lab-022.png

8. Click **Add**
9. Repeat **Steps 11-15** to add **SSH Config File – Edit** to **Contractor Role**.
10. **Save**
11. The results:

    .. figure:: images/lab-023.png

Apply MFA at Elevation Rule as policy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

1. In the same system page, click **Policy** on the left.

   .. figure:: images/lab-008.png

2. Scroll down to the end of the page.
3. From **Default Privilege Elevation Profile (used if no conditions matched)** dropdown list, select **Contractors MFA Profile**
4. **Save**

   .. figure:: images/lab-024.png

Test Privilege Elevation
^^^^^^^^^^^^^^^^^^^^^^^^

1. Switch to/launch **Chrome incognito**, login to *The Portal* as **zcontractor**.
2. Navigate to **Resources > Systems**.
3. Right Click Windows Server (**rhel7sx64**)
4. Click **Use My Account** to login to the server.
5. Execute the following command:

   .. code-block:: bash

       vi /etc/ssh/sshd_config

   The command will result **Permission Denied**

6. Quit by typing **ESC** and typing **:q!**
7. Execute the following command:

   .. code-block:: bash

       sudo vi /etc/ssh/sshd_config

8. You will be prompted to type your **zcontractor** password and **MFA**.

   .. figure:: images/lab-025.png

9. Now you should have access to **sshd_config** file.
10. Repeat **steps 5-9** to test *restarting the sshd service*.

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>