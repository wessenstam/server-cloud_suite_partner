.. _l5:

----------------------------------------
Install and configure the Centrify Agent
----------------------------------------

Introduction
------------

This fifth lab will cover:

1. Install the Centrify Agent
3. Join to AD (Unix) and correct Zone
2. Configure the Centrify Agent

.. note::
    Estimated time to complete this lab: **15 minutes**

In this exercise, Alex (you) will configure the Centrify Zone Provisioning Agent (ZPA) to automatically provision and deprovision users and groups for access to privileged resources. This will include the configuration of a domain service account that will facilitate this automation as users are added to monitored groups.

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab
- apps-unix.greensafe.lab
- db-unix.greensafe.lab

------

Installing the Centrify Agent on Unix
*************************************

#. Open PuTTY on *apps-server.greensafe.lab* and login to **db-unix.greensafe.lab** with the following credentials:

   - **Username:** root
   - **Password:** *Provided by Trainer*

   .. Note:: 
       On the Security Alert, click **Yes**

#. Run the following command to install the *Delinea DirectControl Agent (the -y in the command, make sure that the yum will not prompt during installation)* **PLEASE NOTE THAT THE COMMAND IS CASE SENSITIVE!**

   .. code-block:: bash

       yum install CentrifyDC -y

#. Once completed, run the following command to check the domain and zone connection status for the system:

   .. code-block:: bash

       adinfo

   .. note:: 
       You will notice that installing the client did not automatically join the system to the zone.

       .. figure:: images/lab-001.png

Join the Unix machine to the AD and Unix Zone
*********************************************

#. Run the following command to join the system to the zone:

   .. code-block:: bash

       adjoin -S greensafe.lab

   .. note::
       During the process you will notice that the system was automatically joined to the correct UNIX zone because the system was pre-created and matched the DNS record.

       .. figure:: images/lab-002.png

#. Run the following command to reboot the server:

   .. code-block:: bash

       reboot

#. **Repeat the steps taken in** *Installing the Delinea Agent on Unix* **and** *Join the Unix machine to the AD and Unix Zone* **for the apps-unix server**

Join a Windows machine to the correct Zone
******************************************

#. Open **db-server** UI 
#. Login with the following credentials:
   
   - **Username:** afoster
   - **Password:** *Provided by Trainer*

#. Open **Windows Explorer** and navigate to the Agent folder on the desktop and launch the **Delinea Agent for Windows64** application
#. On the Welcome Message, click **Next**
#. *Accept the EULA* and click **Next**
#. Under the *Destination Folder*, click **Next**
#. Click **Install**

   .. note::
       If prompted to close applications, please proceed
       If you get an message that the system needs to be reboot after the install or services need to be restarted, click **OK**

#. When the installation is complete, click **Finish**
#. The Agent Configuration Wizard will automatically run
#. Click **Add Service**
#. Click **Privilege Elevation Service**

   .. figure:: images/lab-003.png

#. Click **OK**
#. Join the system to the **Windows Zone** and click **Next**

   .. figure:: images/lab-004.png

#. When prompted, select **Yes** to create a Windows Login Role for the Domain Admins group so they can continue to login to the system
    
   .. note::
       If/ When prompted about multifactor authentication enrollment, click Yes to skip the enrollment and continue the configuration

#. When prompted to restart the system, click **Yes**
#. Login with the users listed below on the machines being mentioned and confirm the ability to login according to the below table

   .. list-table::
      :widths: 15 15 15 55
      :header-rows: 1
   
      * - Username
        - Password
        - Server
        - Able to login?
      * - afoster
        - *Provided by Trainer*
        - db-unix
        - **No** (No Local Profile or Role)
      * - afoster
        - *Provided by Trainer*
        - db-server
        - **Yes** (Domain Admin Roles ia applied)
      * - badams
        - *Provided by Trainer*
        - db-server
        - **No** (badams is not assigned a Role)
     
.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>