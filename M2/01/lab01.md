## Lab 1: Creating data store resources in Azure

### Task 1: Open the Azure portal

1.  On the taskbar, select the **Microsoft Edge** icon.

1.  In the open browser window, browse to the Azure portal ([portal.azure.com](https://portal.azure.com)), and then sign in with the account you will be using for this lab.

    > **Note**: If this is your first time signing in to the Azure portal, you'll be offered a tour of the portal. Select **Get Started** to skip the tour and begin using the portal.

### Task 2: Create an Azure Cosmos DB account resource

1.  In the Azure portal, use the **Search resources, services, and docs** text box to search for **Azure Cosmos DB** and then in the list of results, select **Azure Cosmos DB**.

1.  On the **Azure Cosmos DB** blade, select **+ Create**.

1.  On the **Select API option** blade, select **Create** in the **Azure Cosmos DB for NoSQL** box.

1.  On the **Basics** tab of the **Create Azure Cosmos DB Account - Azure Cosmos DB for NoSQL** page, perform the following actions, and then select **Review + Create**:

    | Setting | Action |
    | -- | -- |
    | **Subscription** list | Retain defaults |
    | **Resource group** section  | Select **Create new** |
    | **Name** text box | Enter **Polyglotdata** and select **OK** |
    | **AccountName** text box | Enter **polycosmos**_[yourname]_ |
    | **Location** drop-down list | Select an Azure region that is closest to the location of your lab computer and where you can create a Cosmos DB account |
    | **Capacity mode** section | Select **Serverless** |
    
    The following screenshot displays the configured settings on the **Create Azure Cosmos DB Account - Azure Cosmos DB for NoSQL** page.
    
    ![Screenshot displaying the options configured for creating an Azure Cosmos DB account](/M2/01/images/l04_cosmosdb_create_summary.png)
    
1.  On the **Review + Create** tab of the **Create Azure Cosmos DB Account - Azure Cosmos DB for NoSQL** page, review the options that you selected during the previous steps. 

1.  Select **Create** to create the Azure Cosmos DB account by using your specified configuration.

    > **Note**: Wait for the creation task to complete before you move forward with this lab.

1.  Select **Go to resource**.

1.  On the **Azure Cosmos DB account** blade, find the **Settings** section, and then select the **Keys** link.

1.  In the **Keys** pane, on the **Read-write Keys** tab, record the values of the **URI**, **PRIMARY KEY**, and **PRIMARY CONNECTION STRING** text boxes. You'll use these values later in this lab.

### Task 3: Create an Azure Storage account resource

1.  In the Azure portal, use the **Search resources, services, and docs** text box to search for **Storage accounts** and, in the list of results, select **Storage accounts**.

1.  On the **Storage accounts** blade, select **+ Create**.

1.  On the **Basics** tab of the **Create a storage account** blade, perform the following actions, and then select **Review**:


    | Setting | Action |
    | -- | -- |
    | **Subscription** list | Retain defaults |
    | **Resource group** section | Select **PolyglotData** |
    | **Storage account name** text box | Enter **polystor**_[yourname]_ |
    | **Region** drop-down list | Select the same region where you created the Cosmos DB account earlier in this exercise |
    | **Performance** section | Select **Standard** |
    | **Redundancy** drop-down list | Select **Locally-redundant storage (LRS)** |
    
    
    The following screenshot displays the configured settings on the **Create a storage account** blade.
          
     ![Screenshot displaying the options configured for creating an Azure storage account](/M2/01/images/l04_storage_create_summary.png)
     
1.  On the **Review** tab of the **Create a storage account** blade, review the options that you selected during the previous steps.

1.  Select **Create** to create the storage account by using your specified configuration.

    > **Note**: Wait for the creation task to complete before you proceed with this lab.

## Review

In this exercise, you created the Azure resources that you'll need for the polyglot data solution you'll implement in this lab. The Azure resources you created include an Azure Cosmos DB account and an Azure Storage account.