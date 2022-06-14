.. _l4:

--------------------------------------------
Configure a Centrify Zone Provisioning Agent
--------------------------------------------

Introduction
------------

This fourth lab will cover:

1. Create AD account for the ZPA
2. Configure the ZPA Service
3. Configure the ZPA
4. Configure ZPA for automatic provisioning
5. Assign the automatic provisioning to the zone
6. Test automatic provisioning

.. note::
    Estimated time to complete this lab: **20 minutes**

In this exercise, Alex (you) will configure the Delinea Zone Provisioning Agent (ZPA) to automatically provision and deprovision users and groups for access to privileged resources. This will include the configuration of a domain service account that will facilitate this automation as users are added to monitored groups.

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab

------

Add domain user and groups for the ZPA
**************************************

#. Open **Active Directory Users and Computers (ADUC)**
#. Navigate to *greensafe.lab > Centrify > Service Accounts*
#. **Create a new AD account** with the following parameters:

   - **First Name:** Centrify
   - **Last Name:** Zone Provisioning Agent
   - **User logon name:** cfyS_zpa

   .. figure:: images/lab-001.png

#. Click **Next**
#. Set the *Password* to *Provided by Trainer* and 

   - **UNCHECK** User must change password at logon
   - **CHECK** User cannot change password
   - **CHECK** Password never expires

6. Click **Next**
7. Click **Finish**

   .. note::
       Make sure that the account has not been disabled after the creation. In some cases this happens. You can see thatthe account has been disabled if there is a downwards pointing arrow next to the account. To enable the account, right-click th account and select **Enable Account**. Not having the account Enabled will lead to issues later in the lab.

       .. figure:: images/lab-006.png       

8. Navigate to *greensafe.lab > Centrify > Provisioning Groups*
9. **Create two new AD groups** that will be used for auto provisioning and deprovisioning, name them (*leave the settings default*):

   - **cfyP_Global_Users**
   - **cfyP_Global_Groups**

   .. figure:: images/lab-002.png

#. Close ADUC

Configuring the Zone Provisioning Agent Service
***********************************************

#. Open Windows Services using *Start > typing Services.msc*

   .. figure:: images/lab-003.png

#. Open the properties of the Centrify Zone Provisioning Agent by right-clicking and selecting **Properties**
#. Click the **Log On** tab.
#. Select **This Account:**
#. Click **Browse**
#. Change *Location* to the *Entire Directory* and click **Ok**
#. Search for and select **cfyS_zpa**
#. Click **Check Names** and click **Ok**
#. Once selected, type in the *Password* fields the set password and click **Apply**.
#. Click **Ok** to confirm the account will be used to *Log On as a Service*.
#. Click **Ok**
#. Close **Services**

Configure the Zone Provisioning Agent
*************************************

#. Navigate to *Start Menu > Delinea Server Suite 2022 > Zone Provisioning Agent Configuration Panel*
#. Click the **Add** button

   .. figure:: images/lab-004.png

#. Navigate and select *greensafe.lab > Centrify > Zones* and click **OK**
#. Select *<Entire Forest: greensafe.lab>* and click **Remove** from the list (Leaving the Centrify Zones Container)

   .. figure:: images/lab-005.png

#. Under the *Event Log*, select **Write the UNIX Profiles for the provisioned users and groups to the Event Log**
#. Confirm the ZPA service Account is correct (cfyS_zpa) and click **Start** to start the service
#. The *Current Status:* must change to **Running**

   .. figure:: images/lab-007.png

#. Click **Apply** to save the changes
#. Click **Close** to exit the Configuration Panel

Configure the Zones to be automatically provisioned
***************************************************

#. Open Delinea Access Manager if you have closed it
#. Right-click the *Global Zone* and select **Delegate Zone Control**
#. Click **Add**
#. Search for and add the AD user **cfyS_zpa**
#. Click **Next**
#. Click the following administrative tasks to be applied to the ZPA service account.
    
   - Add Users
   - Add Groups
   - Remove Users
   - Remove Groups   
   
   .. note:: 
       The ZPA does not require all administrative tasks – only those tasks that the service account will be performing.     
   
   .. figure:: images/lab-008.png

#. Click **Next**
#. When prompted about the *UID/GID auto-increment functionality*, click **NO**
#. Click **Finish**

   .. figure:: images/lab-009.png

Assigning the provisioning to the zone
**************************************

#. Using *Access Manager*, right-click *Global Zone* and select **Properties**
#. Click the *Provisioning Tab* and **Enable auto-provisioning of User Profiles**

   .. figure:: images/lab-009a.png

#. Click the :fa:`search` button
#. Find and select **cfyP_Global_Users** and Click **OK**
#. Under the *Provisioning* tab, *Enable auto-provisioning of Group Profiles*
#. Click the :fa:`search` button
#. Find and select **cfyP_Global_Groups**
#. Click **OK**
#. Click **OK** to save the changes
#. Click **OK** in the *This zone is now....* popup screen

Test the auto provisioning
**************************

#. Launch Active Directory Users and Computers (ADUC) if you have closed it
#. Navigate to *greensafe.lab > Centrify > Provisioning Groups*
#. Open the *properties* of **cfyP_Global_Users**
#. Click the **Members** Tab
#. Click **Add**
#. Find and Select the following groups (type *Team_* and click **Check Names** to speed it up):

   - Team_Contractors
   - Team_Finance
   - Team_Helpdesk
   - Team_IT
   - Team_Sales
   - Team_Security

   .. figure:: images/lab-010.png

#. Click **OK**
#. Close ADUC
#. To speed up the process, we will use the zoneupdate utility. Navigate to *Start Menu > Delinea Server Suite 2022 > Zone Provisioning Agent Command Prompt*

   .. figure:: images/lab-011.png

#. Type and run 

   .. code-block:: bash
       
       zoneupdate /p "Global Zone"

#. You will see a preview of a number of users that are going to be provisioned by the ZPA

   .. figure:: images/lab-014.png

#. Type and run the below command to commit the changes immediately

   .. code-block:: bash
   
      zoneupdate “Global Zone”



   .. figure:: images/lab-015.png

#. Close *Zone Provisioning Agent Command Prompt*
#. Using Access Manager Expand **Global zone > UNIX Data**
#. Click **Users**. Users from the groups we added will now be configured with UNIX Profiles under the *Global zone > UNIX Data > Users*.

   .. figure:: images/lab-016.png

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>