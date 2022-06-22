.. _l1:

--------------------------------------
Installation and initial configuration
--------------------------------------

Introduction
------------

This first lab will cover:

1. Initial installation of Server Suite, Authentication and Privilege
2. Initial configuration


Greensafe Payroll Services has recently purchased Delinea Server Suite. Alex Foster has been identified as the project engineer in charge of implementing the solution. In this exercise, Alex (you) will install Authentication and Privilege.

.. note::
    Estimated time to complete this lab: **20 minutes**

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab

------

Installation and Configuration
******************************

Installation
^^^^^^^^^^^^

#. Login to **apps-server.greensafe.lab** with the following credentials: 

   - **Username:** afoster
   - **Password:** *Provided by Trainer*

#. Open Windows Explorer and navigate to C:\\Share\\DS2022\\Delinea-Server-Suite-2022-mgmt-win64
#. Launch the **Autorun** application and click **Authentication and Privilege**

   .. figure:: images/lab-001.png

#. When prompted to install *Microsoft SQL Compact 4.0* for support of the Sudoers Import process, click **No**
#. At the Welcome Message, click **Next**
#. Accept the EULA and click **Next**
#. Leave the **User Name** as *afoster* and enter the Company Name **Greensafe Payroll Services**, click **Next**
#. Under *Select Product Components*, expand *Utilities* and click the **checkbox** next to *Zone Provisioning Agent*
#. Click **Next**
#. Under the *Destination* folder, click **Next**
#. Under *Confirm Installation Settings*, click **Next** to start the installation
#. Once completed, **UNCHECK** the options to configure the following products:

   - Centrify Reporting Services
   - Centrify Zone Provisioning Agent

   .. figure:: images/lab-003.png

#. Click **Finish**
#. Click **Yes** when prompted about using a Local system account to manage the Zone Provisioning Agent (ZPA)

   .. figure:: images/lab-004.png

#. Close the Delinea Server Suite Installation Package by clicking **Exit**

Configuration
^^^^^^^^^^^^^

In this exercise, Alex (you) will complete the initial configuration of the solution using the management console, Delinea Access Manager. This configuration will include the creation of an active directory deployment structure and licensing.

#. While still being on the *apps-server.greensafe.lab* Open Windows Explorer and navigate to **C:\\Share**
#. Open **Training License Keys** and copy the **DirectControl License Key** to the clipboard
#. **Close** the file
#. Launch **Access Manager** from the Desktop shortcut

   .. figure:: images/lab-005.png

#. Click **OK** to connect to **dc-server.greensafe.lab**
#. At the *Welcome Message*, click **Next**
#. Under *User Credentials*, maintain the default setting and click **Next**
#. Under *Generate Delinea Recommended Deployment Structure*, Click the **checkbox** to generate the structure and click **Next**

   .. figure:: images/lab-006.png

#. Under *Choose Container*, click **Browse**
#. Select **greensafe.lab** and click **Ok**
#. Click **Next** once the deployment structure container has been populated

   .. figure:: images/lab-007.png

#. Under *Install License*, maintain the default container and click **Next**
#. When prompted, click **Yes** to grant all users read permissions to the license container
#. Paste the License key (copied earlier) in the space provided and click **Add**

   .. figure:: images/lab-008.png

#. Click **Next**
#. Under the *Default Container for Zones*, maintain the default settings and click **Next**
#. Under *Delegate Permission*, maintain the default settings and click **Next**
#. Under *Register the AD Administrative Notification Handler*, maintain the default settings and click **Next**
#. Under *Setup Properties Pages*, maintain the default settings and click **Next**
#. Under *Summary*, Click **Next**
#. Click **Finish** to complete the initial configuration wizard
#. The UI of Centrify Access Manager will open

   .. figure:: images/lab-009.png



.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>
