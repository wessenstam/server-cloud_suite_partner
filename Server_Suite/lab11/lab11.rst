.. _l11:

------------------------
Troubleshooting
------------------------

Introduction
------------

This eleventh lab will cover:

1. Troubleshoot Centrify Licensing
2. Analyze the Environment


.. note::
    Estimated time to complete this lab: **20 minutes**

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab
- apps-unix.greensafe.lab
- db-server.greensafe.lab
- db-unix.greensafe.lab

------

Troubleshooting Centrify Licensing
**********************************

In this exercise, Alex (you) will use the Centrify Licensing Service to examine the installed licensing applied to the environment.

#. On the **apps-server.greensafe.lab**, navigate to *Start Menu > Centrify Server Suite 2021.1 > Centrify Licensing Service Control Panel*

   .. figure:: images/lab-001.png

#. Confirm service is running, bottom of the screen *Service status*:
#. Click **DC/DZ Deployment** tab to determine # of devices currently licensed

   .. figure:: images/lab-002.png

   .. note::
       As we are using Evaluation Licenses the number of licenses available is Unlimited.

#. Click **Troubleshooting** tab
#. Click **Export Diagnostic Data**

   .. figure:: images/lab-003.png

#. Navigate to **Desktop** and Click **OK**
#. Click **Ok**
#. **Close** Centrify Licensing Service Control Panel
#. Open the saved diagnostic data file.
#. Review the files included in the zip file. Close the explorer window
#. Using the *Start Menu > Centrify Server Suite 2021.1 > Licensing Report*
#. Confirm the Domain Controller *dc-server.greensafe.lab* and click **Next**
#. Select the default location to store the report and leave the *Hide host, zone and installation names from the report* and click **Next**
#. Click **Next** to run the report
#. Leave *Open the output report* **checked** and click **Exit**
#. Look at the report that has just been opened in Notepad...
#. CLose **Notepad**
#. Click **OK**

Analyzing the Environment
*************************

In this exercise, Alex (you) will use Centrify Access Manager to examine possible issues with the health of the environment.

#. Open **Access Manager**, right-click *Centrify Access Manager* and select **Analyze**

   .. figure:: images/lab-004.png

#. Click **All**
#. Click **Next**
#. Click **Finish**
#. Click **Analysis Results** from the Navigational Tree on the left of the Access Manager Console

   .. figure:: images/lab-005.png

#. Double click the issue to review the details (with the Exclamation Mark)
#. Check whether the computer object in Active Directory has sufficient permission to update the version number property of the operating system in the computer’s serviceConnectionPoint object. If the computer object does not have permission to change this property, the operating system version number cannot be displayed.

   .. figure:: images/lab-006.png

#. Click **OK** to close the Issue Details

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>

