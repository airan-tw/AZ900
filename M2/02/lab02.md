## Lab 2: Upload a blob into a container

### Task 1: Create storage account containers

1. On the **Storage account** blade, select the **Containers** link in the **Data storage** section.

1. In the **Containers** section, select **+ Container**.

1. In the **New container** pop-up window, perform the following actions, and then select **Create**:

    | Setting | Action |
    | -- | -- |
    | **Name** text box | Enter **raster-graphics** |
    | **Public access level** drop-down list | Select **Private (no anonymous access)** |

1. In the **Containers** section, select **+ Container**.

1. In the **New container** pop-up window, perform the following actions and then select **Create**:

    | Setting | Action |
    | -- | -- |
    | **Name** text box | Enter **compressed-audio** |
    | **Public access level** drop-down list | Select **Private (no anonymous access)** |

1. In the **Containers** section, observe the updated list of containers.

    The following screenshot displays the configured settings on the **Create a storage account blade**.

    ![Create a storage account blade](/M2/02/images/l03_containers.png)

### Task 2: Upload a storage account blob

1.  In the **Containers** section, select the recently created **raster-graphics** container.

1.	On the **Container** blade, select **Upload**.

1.	In the **Upload blob** window, perform the following actions, and then select **Upload**:

   | Setting | Action |
   | -- | -- |
   | **Files** section | Select the **Folder** icon |
   | **File Explorer** window | Browse to **$HOME\\training-az204\\Labs\\03\\Starter\\Images**, select the **graph.jpg** file, and then select **Open** |
   | **Overwrite if files already exist** check box | Ensure that the check box is selected |
   
   > **Note**: Wait for the blob to upload before you continue with this lab.

## Review

In this exercise, you created placeholder containers in the Storage account, and then populated one of the containers with a blob.