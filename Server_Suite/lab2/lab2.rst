.. _l2:

-----
Zones
-----

Introduction
------------

This second lab will cover:

1. Creation of Zones
2. Preparing Zone Server objects

In this exercise, Alex (you) will continue the initial configuration of the Centrify solution by assigning Centrify Administrators and creating Parent and Child Zones for Centrify privilege management. There will be one Global Zone for all users, and two child zones based on server operating systems.

| As part of your preparations to implement Centrify Server Suite features to the infrastructure, you can prepare the objects prior to the implementation of each server. This will avoid any interruptions in service and provide you the opportunity to confirm effective security rights are accurate. In this exercise, Alex (you) will use Centrify Access Manager to create the AD objects in the appropriate Centrify Zones so they are organized properly and effective rights are applied prior to the server being joined.


.. note::
    Estimated time to complete this lab: **25 minutes**

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab

------

Creation of Zones
*****************

#. While stilling being logged in in the **apps-server.greensfae.lab**, open Active Directory Users and Computers (ADUC) 

   .. figure:: images/lab-001.png

#. Navigate to **greensafe.lab > Centrify > Centrify Administration**

   .. figure:: images/lab-002.png

#. Open the AD group **cfyA_Global_CentrifyAdmins**
#. Click **Members**
#. Click **Add...**
#. Type **Team_Security** and click **Check Names** that will show the below screenshot

   .. figure:: images/lab-003.png

#. Click **Ok**
#. Close the group properties by clicking **Ok**
#. Close **ADUC**
#. Let’s now create the Parent Zone, back in **Delinea Access Manager**, expand *Access Manager [dc-server.greensafe.lab]*
#. *Right Click on Zones* and select **Create New Zone**

   .. figure:: images/lab-004.png

#. Name the new zone **Global Zone**, *leave all other options default*
#. Click **Next**
#. Click **Finish** 
#. Let’s now delegate zone controls to the appropriate administrators, expand the *Zones* 
#. Right-click the new *Global Zone* and select **Delegate Zone Control**

   .. figure:: images/lab-005.png

#. Click **Add**
#. Use the following steps

   - **Find:** Group
   - **Name:** cfyA
   - Click **Find Now**
   - Select the **cfyA_Global_CentrifyAdmins** group

     .. figure:: images/lab-006.png
   
   - Click **Ok**

#. Click **Next**
#. Under *Tasks to Delegate*, click **All**
#. Click **Next**
#. When prompted about the *msDS-azScope objects*, click **Yes**

   .. figure:: images/lab-007.png

#. Click **Next** in the *Tasks to Delegate* for the whole AD to the group
#. Click **Finish**
#. Let’s now create the *Child Zones*. Right Click Global Zone and select **Create Child Zone**

   .. figure:: images/lab-008.png

#. *Name* the new child zone **UNIX Zone**, *leave all other options default*
#. Click **Next**
#. Click **Finish**. 
#. We have to remember to delegate zone controls to each zone. In some cases, you may have different administrators responsible for each zone. 
#. Expand the *Global Zone > Child Zones* and right-click the new *UNIX Zone* and select **Delegate Zone Control**
#. Click **Add**
#. Search for and add the AD group **cfyA_Global_CentrifyAdmins**
#. Click **Ok** to add the group
#. Click **Next**
#. Under *Tasks to Delegate*, click **All**
#. When prompted about the *msDS-azScope objects*, click **Yes**
#. Click **Next** in the *Tasks to Delegate* for the whole AD to the group
#. Click **Finish** 
#. Let’s now create the Windows Child Zones. Right-click *Global Zone* and select **Create Child Zone**
#. Name the new child zone **Windows Zone**
#. Click **Next**
#. Click **Finish**. 
#. Don’t forget to delegate zone controls for this zone. Right-click the new *Windows Zone* and select **Delegate Zone Control**
#. Click **Add**
#. Search for and add the AD group **cfyA_Global_CentrifyAdmins**
#. Click **Ok** to add the group
#. Click **Next**
#. Under *Tasks to Delegate*, click **All**
#. When prompted about the *msDS-azScope objects*, click **Yes**
#. Click **Next** in the *Tasks to Delegate* for the whole AD to the group
#. Click **Finish** 


Prepare Zone Server objects
***************************

Unix Servers
^^^^^^^^^^^^

#. Using Delinea Access Manager, expand **UNIX Zone**
#. Right-click *Computers* and select **Prepare UNIX Computer**
#. Under *Prepare Computer*, maintain the default settings and click **Next**
#. Under *Specify Computer*, click **Next** to add a new computer object
#. Name the computer **db-unix**
#. Click **Change** to change the computer container
#. Navigate to *greensafe.lab > Centrify > Computers* and Click **Ok**

   .. figure:: images/lab-009.png

#. Click **Next**
#. Under *Read Only Domain Controller Compatibility and License Type* settings, *maintain the default settings* and license selection and click **Next**
#. Under *SPN Configuration*, maintain the default settings and click **Next**
#. Under *Delegate Join Permissions*, *maintain the default setting* to allow the computer to join itself to the zone and click **Next**
#. Under *Delegate Machine Overrides*, click **Browse** to change the AD group
#. Search for and select **cfyA_Global_CentrifyAdmins**
#. Click **Next**
#. Under *Delegate Permission*, *maintain the default settings* and click **Next**
#. Click **Next** to confirm the selection
#. Click **Finish** 
#. **Repeat the above steps** *(Prepare Zone Server Objects)* **for the apps-unix server**

Windows Servers
^^^^^^^^^^^^^^^

#. Expand **Windows Zone**
#. Right-click Computers and select **Prepare Windows Computer**
#. Search and Add **db-server.greensafe.lab**
#. Click **OK**
#. In the *Skip delegation permission* popup box, click **Yes**

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>
