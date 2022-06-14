.. _l3:

---------------------------------
Managing Users (Local and Domain)
---------------------------------

Introduction
------------

This third lab will cover:

1. Add domain users to a Unix Zone
2. Consolidate Unix local profiles

.. note::
    Estimated time to complete this lab: **15 minutes**

------

Systems used in this lab:

- dc-server.greensafe.lab
- apps-server.greensafe.lab

------

Add domain users
****************

#. Using *Delinea Access Manager*, expand *Child Zones*
#. Expand **UNIX Zone**
#. Expand **Computers** 
#. First, we will manually add a domain user as an authorized user of the system. Right-click the **db-unix** server and select **Add User**

   .. figure:: images/lab-001.png

#. Select **Active Directory user** and click **Next**
#. Click **Browse**
#. Search for **Linda Scott**

   .. figure:: images/lab-002.png

#. Click **Ok**
#. Click **Next**
#. Under *Add User to Zone*, click **Next**
#. Under *Define User UNIX Profile*, click **Next**
#. Under *Assign Roles*, click **Next**
#. Under *Confirm Your Selection*, click **Next**
#. Click **Finish** 


Consolidate Unix local profiles
*******************************

#. Let’s now import users that are currently installed on the local system. The /etc/passwd and /etc/group files were downloaded to this server and will be used for the next series of steps. Expand the **db-unix** server
#. Right-click **Unix Data** and select **Import from UNIX**

   .. figure:: images/lab-003.png

#. Select **UNIX configuration files**
#. Click the top **Browse** button to select the /etc/passwd file that is located in the C:\\Share folder (this file has already been downloaded earlier)
#. Click the bottom **Browse** button to select the /etc/group file that is located in the C:\\Share folder (this file has already been downloaded earlier)

   .. figure:: images/lab-004.png

#. Click **Next**
#. Under *Select Import Objects*, click **Next**
#. Under *Select Destination*, click **Next**
#. Click **Finish**
#. Under the *db-unix server*, expand *UNIX Data*
#. Expand *Users* and click *Pending Users*. There will be a list of users that have been imported but are not yet accepted. At the bottom of the list will be the following users: 

   - afoster-a 
   - cfyadmin 
   - helpdesk-a 
   - kim 
   - sam

   .. figure:: images/lab-005.png

#. Select users *Kim and Sam*, right click and select **Check Status**. This process will check the identities against active directory to look for a matching user candidate

   .. figure:: images/lab-006.png

#. When prompted to select a domain, click **OK** to accept *greensafe.lab*
#. In the AD User Candidate column, you will notice an AD user has been identified as a POSSIBLE match for the local profile that was imported

   - kim :fa:`arrow-right` greensafe.lab/staff/krogers (Kim Rogers)
   - sam :fa:`arrow-right` greensafe.lab/staff/snguyen (Sam Nguyen)

   .. figure:: images/lab-007.png

#. As the two accounts are still selected, right-click them and click **Accept**. This will consolidate the local profile with the domain account, permitting the domain account to be used to login once a role has been assigned. 

   .. figure:: images/lab-008.png

#. All remaining Pending Users can be deleted by selecting them, right-click and select **Delete** and click **Yes** in the popup screen

   .. figure:: images/lab-009.png

#. Let’s now create a new AD group based on the UNIX local users group. Expand *Groups* under *UNIX Data* for the db-unix server
#. Click **Pending Groups**

   .. figure:: images/lab-010.png

#. Right-click on the *users* group and select **Create new AD groups**

   .. figure:: images/lab-011.png

#. Under *Location of Container*, click **Browse**
#. Select **greensafe.lab > Centrify > Unix Groups** and click **Ok**

   .. figure:: images/lab-012.png

#. Click **Next**
#. Name the group name (for both group name fields) **cfyG_db-unix_users**, *leave prefix and suffix related fields unchecked*
#. Under *Group Scope*, select **Global**

   .. figure:: images/lab-014.png

#. Click **Next**
#. Click **Next** to confirm the settings
#. Click **Finish**

   .. figure:: images/lab-015.png

#. All remaining Pending Groups can be deleted by selecting them all, right-click and click **Delete** and click **Yes** in the popup screen
#. Let’s now add the imported users and Linda Scott who was added manually to the new AD group, click **Users** under *UNIX Data of db-unix*

   .. note::
      If only Linda Scott is shown  in the Users section, click the refresh button in the Delinea Access Manager UI. This will show the other two users.

      .. figure:: images/lab-016.png

#. Select all users, right click and select Add to a Group. 

   .. figure:: images/lab-017.png

#. Search for and select **cfyG_db-unix-users**
#. Click **Ok** and **Ok** in the popup screen telling the *The Add to Group was successfully completed for 3 user(s)*

   .. figure:: images/lab-018.png

.. raw:: html

    <hr><CENTER>
    <H2 style="color:#00FF59">This concludes this lab</font>
    </CENTER>