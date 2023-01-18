---
wts:
  title: 03 – Deploy Azure Container Instances (10 min)
  module: Module 02 - Core Azure Services (Workloads)
---

## Lab 6: Deploy Azure Container Instances (10 min)

In this Lab we create, configure, and deploy a container by using Azure Container Instances (ACI) in the Azure Portal. The container is a Welcome to ACI web application that displays a static HTML page.

### Task 1: Create a container instance

In this task, we will create a new container instance for the web application.

1 - Sign-in to the [Azure Portal](https://portal.azure.com/). 

2 - From the **All services** blade, search for and select **Container instances**, and click **+ Add**, **+ Create**, **+ New**.

3 - Provide the following Basic details for the new container instance (leave the defaults for everything else):

 | **Setting** | **Value** |
 |----|----|
 | Subscription | ***Use default supplied*** |
 | Resource group | **Create new resource group** |
 | Container name | **mycontainer**|
 | Region | **(US) East US** |
 | Image Source | **Docker Hub or other registry**|
 | Image type | **Public**|
 | Image| **mcr.microsoft.com/azuredocs/aci-helloworld**|
 | OS type | **Linux** |
 | Size | ***Leave at the default***|

4 - Configure the Networking tab (replace **xxxxx** with letters and digits such that the name is globally unique). Leave all other settings at their default values.

 | **Setting** | **Value** |
 |--- |--- |
 | DNS name label | **mycontainerdnsxxxxx** |

**Note:** Your container will be publicly reachable at dns-name-label.region.azurecontainer.io. If you receive a DNS name label not available error message following the deployment, specify a different DNS name label (replacing the xxxxx) and re-deploy.

5 - Click **Review and Create** to start the automatic validation process.

6 - Click **Create** to create the container instance.

7 - Monitor the deployment page and the **Notifications** page.

### Task 2: erificar a implaVerify deployment of the container instance

In this task, we verify that the container instance is running by ensuring that the welcome page displays.

1 - After the deployment is complete, click the **Go to resource** link the deployment blade or the link to the resource in the Notification area.

2 - On the **Overview** blade of **mycontainer**, ensure your container Status is **Running**.

3 - Locate the Fully Qualified Domain Name (FQDN).

![alt text](/M2/01/images/0202.png)

4 - Copy the container's FQDN into a new web browser tab and press **Enter**. The Welcome page should display.

![alt text](/M2/01/images/0203.png)

**Congratulations!** You have used Azure Portal to successfully deploy an application to a container in Azure Container Instances.

**Note:** To avoid additional costs, you can optionally remove this resource group. Search for resource groups, click your resource group, and then click **Delete resource group**. Verify the name of the resource group and then click **Delete**.
Monitor the **Notifications** to see how the delete is proceeding.