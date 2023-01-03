## Lab 1: Create Azure resources

### Task 1: Open the Azure portal

1.  On the taskbar, select the **Microsoft Edge** icon.

1. In the browser window, browse to the Azure portal (<https://portal.azure.com>), and then sign in with the account you'll be using for this lab.

   > **Note**: If this is your first time signing in to the Azure portal, you'll be offered a tour of the portal. Select **Get Started** to skip the tour and begin using the portal.

### Task 2: Create a Storage account

1.  In the Azure portal, use the **Search resources, services, and docs** text box to search for **Storage Accounts**, and then in the list of results, select **Storage Accounts**.

1.  On the **Storage accounts** blade, select **+ Create**.

1.  On the **Create a storage account** blade, on the **Basics** tab, perform the following actions, and then select **Review**:

   | Setting | Action |
   | -- | -- |
   | **Subscription** drop-down list | Retain the default value |
   | **Resource group** section | Select **Create new**, enter **StorageMedia**, and then select **OK** |
   | **Storage account name** text box | Enter **mediastor**_[yourname]_ |
   | **Region** drop-down list | Select **(US) East US** |
   | **Performance** section | Select the **Standard** option |
   | **Redundancy** drop-down list | select **Locally-redundant storage (LRS)** |

   The following screenshot displays the configured settings on the **Create a storage account blade**.
 
   ![Create a storage account blade](/M2/02/images/l03_create_a_storage_account.png)
   
1.  On the **Review** tab, review the options that you selected during the previous steps.

1.  Select **Create** to create the storage account by using your specified configuration.

    > **Note**: Wait for the creation task to complete before you move forward with this lab.

1.  Select **Go to resource**.

1.  On the **Storage account** blade, in the **Settings** section, select the **Endpoints** link.

1.  In the **Endpoints** section, copy the value of the **Blob Service** text box to the clipboard.

    > **Note**: You'll use this endpoint value later in the lab.

1.  Open Notepad, and then paste the copied blob service value to Notepad.

1.  On the **Storage account** blade, in the **Security + networking** section, select **Access keys**.

1.  Copy the **Storage account name** value to the clipboard and then paste it into Notepad.

1.  On the **Access keys** blade, select **Show keys**.

1.  Review any one of the keys, and then copy the value of either of the **Key** boxes to the clipboard.

    > **Note**: You'll use all these values later in this lab.

## Review

In this exercise, you created a new Storage account to use throughout the remainder of the lab.