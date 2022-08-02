.. _l7:

--------------
Group Policies
--------------

Introduction
------------

This seventh lab will cover:

1. Configuring and testing Group Policies

.. note::
    Estimated time to complete this lab: **15 minutes**

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab
- db-server.greensafe.com
- db-unix.greensafe.lab
- apps-unix.greensafe.lab

------

Delinea Server Suite Group Policies (GPO)
******************************************

Create a GPO
^^^^^^^^^^^^

#. Use the Desktop Shortcut to launch Group Policy Management, or *Start Menu > Windows Administrative Tools > Group Policy Management*
#. Navigate to *Forest: greensafe.lab > greensafe.lab > Centrify*
#. Right-click **Centrify** and select **Create a GPO in this domain and Link it here**

   .. figure:: images/lab-001.png

#. *Name* the new GPO **Centrify GPO** and click **OK**
#. Right-click the *Centrify GPO* and click **Edit**
#. Expand *Computer Configuration > Policies*
#. Right-click *Delinea Settings* and click **Add/Remove Templates**
#. Click **Add**
#. Select all Centrify Templates in the window that opens and click **Open**
#. Click **OK**
#. Expand *DirectControl Settings*

   .. figure:: images/lab-002.png

#. Open **Password Prompts**
#. Right-click *Set login password prompt* on select **Properties**
#. Enable the option and set the login password prompt to **Enter your AD Password:**

   .. figure:: images/lab-003.png

#. Click **OK**

Test the set GPO on Unix
^^^^^^^^^^^^^^^^^^^^^^^^
#. Use PuTTY to login to the *db-unix* server with the following credentials (accept the warning screen by clicking **Yes**):

   - **Username:** root
   - **Password:** *Provided by Trainer*

#. Execute **adgpupdate** to update group policies on the system
#. Logout of db-unix and **repeat these 2 steps (1 and 2)** for the *apps-unix* server
#. Log back in using the following credentials:
   
   - **Username:** badams@greensafe.lab
   - **Password:** *Provided by Trainer*
   
   You should notice the password prompt has been changed.
   
   .. figure:: images/lab-004.png

#. Logout of the session


#. Open the UI of the *apps-unix* server
#. From the GUI Login interface, click *Not Listed?*
  
   .. figure:: images/lab-005.png
  
#. Enter the username **badams** and you will notice the password prompt is the same as the terminal window login

   .. figure:: images/lab-006.png

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>
