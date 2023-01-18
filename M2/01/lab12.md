---
wts:
  title: 14 – Manage access with RBAC (5 min)
  module: 'Module 05: Describe identity, governance, privacy, and compliance features'
---
## Lab 12: Manage access with RBAC (5 min)

In this Lab, we will assign permission roles to resources and view logs.

### Task 1: View and assign roles

In this task, we will assign the Virtual machine contributor role. 

1 - Sign-in to the [Azure Portal](https://portal.azure.com/). 

2 - From the **All services** blade, search for and select **Resource groups**, then click **+ Add**, **+ New**, **+ Create**.

3 - Create a new resource group. Click Create when you are finished.

 | **Setting** | **Valus** | 
 | --- | --- |
 | Subscription | ***Use default provided*** |
 | Resource group | **myRGRBAC** |
 | Region | **(US) East US** |
   
4 - Create **Review + Create** and then click **Create**. 

5 - **Refresh** the resource group page and click the entry representing the newly created resource group.

6 - Click on the **Access control (IAM)** blade, and then switch to the **Roles** tab. Scroll through the large number of role definitions that are available. Use the Informational icons to get an idea of each role's permissions. Notice there is also information on the number of users and groups that are assigned to each role.

![alt text](/M2/01/images/1401.png)

7 - Switch to the **Role assignments** tab of the **myRGRBAC - Access control (IAM)** blade, click **+ Add** and then click **Add role assignment**. Search for the Virtual Machine Contributor role and select. Switch to the "Members" tab and Assign access to: User, group, or service principal. Then click + Select members and type in your name to the popup search function and hit 'select.' Then hit 'Review and Assign'

![alt text](/M2/01/images/1402.png)

**Note:** The Virtual machine contributor role lets you manage virtual machines, but not access their operating system or manage the virtual network and storage account they are connected to.

8 - Refresh the Role assignments page and ensure you are now listed as a Virtual machine contributor.

**Note:** This assignment does not actually grant you any additional privileges, since your account already has the Owner role, which includes all privileges associated with the Contributor role.

### Task 2: Monitor role assignments and remove a role

In this task, we will view the activity log to verify the role assignment, and then remove the role.

1 - On the **myRGRBAC resource group** blade, click **Activity log**.

2 - Click **Add filter**, select **Operation**, and then **Create role assignment**.

![alt text](/M2/01/images/1403.png)

3 - Verify the Activity log shows your role assignment.

**Note:** Can you figure out how to remove your role assignment? 

**Congratulations!** You created a resource group, assigned an access role to it and viewed activity logs.

**Note:** To avoid additional costs, you can optionally remove this resource group. Search for resource groups, click your resource group, and then click **Delete resource group**. Verify the name of the resource group and then click **Delete**.
Monitor the **Notifications** to see how the delete is proceeding.