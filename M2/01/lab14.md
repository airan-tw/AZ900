---
wts:
  title: 07 – Implement an Azure IoT Hub (10 min)
  module: 'Module 03: Describe core solutions and management tools'
---
## Lab 14: Implement an Azure IoT Hub (10 min)

In this Lab, we will configure a new Azure IoT Hub in Azure Portal, and then authenticate a connection to an IoT device using the online Raspberry Pi device simulator. Sensor data and messages are passed from the Raspberry Pi simulator to your Azure IoT Hub, and you view metrics for the messaging activity in Azure Portal.

### Task 1: Create an IoT hub

In this task, we will create an IoT hub.

1 - Sign-in to the [Azure Portal](https://portal.azure.com/). 

2 - From the **All services** blade, search for and select **IoT Hub** and then click **+ Add**, **+ Create**, **+ New**.

3 - On the Basics tab of the IoT hub blade, fill in the fields with the following details (replace xxxx in the name of the storage account with letters and digits such that the name is globally unique):

 | **Setting** | **Value** | 
 | --- | --- |
 | Subscription | ***Keep default supplied*** |
 | Resource Group | **Create new resource group** |
 | IoT Hub Name | **my-hub-groupxxxxx** |
 | Region | **East US** |

**Note:** Remember to change the **xxxxx** so that it makes a unique **IoT Hub Name**.

4 - Go to the **Management** tab, and use the dropdown to set the **Pricing and scale tier** to **S1: Standard tier**.

5 - Click the **Review + Create** button.

6 - Click the **Create** button to begin creating your new Azure IoT Hub instance.

7 - Wait until the Azure IoT Hub instance is deployed.

### Task 2: Add an IoT device

In this task, we will add an IoT device to the IoT hub.

1 - When the deployment has completed, click **Go to resource** from the deployment blade. Alternatively, from the **All services** blade, search for and select **IoT Hub** and locate your new IoT Hub instance

![alt text](/M2/01/images/0601.png)

2 - To add a new IoT device, scroll down to the **Device management** section and click **Devices**. Then, click **+ Add Device**.

![alt text](/M2/01/images/0602.png)

3 - Provide a name for your new IoT device, **myRaspberryPi**, and click the **Save** button. This will create a new IoT device identity in your Azure IoT Hub.

4 - If you do not see your new device, **Refresh** the IoT Devices page.

5  Select **myRaspberryPi** and copy the **Primary Connection String** value. You will use this key in the next task to authenticate a connection to the Raspberry Pi simulator.

![alt text](/M2/01/images/0603.png)

### Task 3: Test the device using a Raspberry Pi Simulator

In this task, we will test our device using the Raspberry Pi Simulator.

1 - Open a new tab in the web browser and type this shortcut link https://aka.ms/RaspPi. It will take you to a Raspberry Pi Simulator site. If you have time, read about the Raspberry Pi simulator. When done select **"X"** to close the pop-up window.

2 - In the code area on the right side, locate the line with 'const connectionString ='. Replace it with the connection string you copied from the Azure portal. Note that the connection sting includes the DeviceId (**myRaspberryPi**) and SharedAccessKey entries.

![alt text](/M2/01/images/0604.png)

3 - Click **Run** (below the code area) to run the application. The console output should show the sensor data and messages that are sent from the Raspberry Pi simulator to your Azure IoT Hub. Data and messages are sent each time the Raspberry Pi simulator LED flashes.

![alt text](/M2/01/images/0605.png)

4 - Click **Stop** to stop sending data.

5 - Return to the Azure portal.

6 - Switch the IoT Hub **Overview** blade and scroll down to the **IoT Hub Usage** information to view usage. Change your timeframe in the **show data for last** to see data in the last hour.

![alt text](/M2/01/images/0606.png)

**Congratulations!** You have set up Azure IoT Hub to collect sensor data from an IoT device.

**Note:** To avoid additional costs, you can optionally remove this resource group. Search for resource groups, click your resource group, and then click **Delete resource group**. Verify the name of the resource group and then click **Delete**.
Monitor the **Notifications** to see how the delete is proceeding.