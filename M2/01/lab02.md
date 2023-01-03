## Lab 2: Review and upload data

### Task 1: Upload images to Azure Blob Storage

1.  In the Azure portal's navigation pane, navigate back to the **Storage accounts** blade, and then select the **polystor**_[yourname]_ storage account that you created in this lab's previous exercise.

1.  On the **polystor**_[yourname]_ storage account blade, select the **Containers** link in the **Data storage** section.

1.  In the **Containers** section, select **+ Container**.

1.  In the **New container** pop-up window, perform the following actions, and then select **Create**:

    | Setting | Action |
    | -- | -- |
    | **Name** text box | Enter **images** |
    | **Public access level** drop-down list | Select **Blob (anonymous read access for blobs only)** |
    
   
1.  Back in the **Containers** section, select the newly created **images** container.

1.  Find the **Settings** section on the **Container** blade, and then select the **Properties** link.

1.  In the **Properties** pane, note and record the value in the **URL** text box. You'll use this value later in this lab.

1.  Find and select the **Overview** link on the blade.
1.  On the blade, select **Upload**.

1.  In the **Upload blob** pop-up, perform the following actions:
    
    a.  In the **Files** section, select the **Folder** icon.
    
    b.  In the **File Explorer** window, browse to **$HOME\\training-az204\\Labs\\04\\Starter\\Images**, select all 42 individual **.jpg** image files, and then select **Open**.
    
    c.  Ensure that **Overwrite if files already exist** is selected, and then select **Upload**.

    > **Note**: Wait for all blobs to upload before you continue with this lab.

### Task 2: Review JSON data

1.  From the lab computer, start Visual Studio Code.

1.  From the **File** menu, select **Open File**, browse to **$HOME\\training-az204\\Labs\\04\\Starter\\AdventureWorks\\AdventureWorks.Upload**, select **models.json**, and then select **Open**.

1.  Review the format of the **models.json** file and note that it contains an array of JSON objects, with a nested array of objects that are part of the **Products** property.

    > **Note**: This will determine the classes you'll define to deserialize the JSON file's contents before uploading it to a Cosmos DB collection.

1.  Within the **models.json** file, note that one of the properties is named **Category**.

    > **Note**: You'll use the **Category** property to define partitioning of the target Cosmos DB collection.

1.  Close Visual Studio Code.

### Task 3: Create a Cosmos DB database and collection, and perform a JSON data upload

1.  On the **Start** screen, select the **Visual Studio Code** tile.

1.  From the **File** menu, select **Open Folder**.

1.  In the **File Explorer** window that opens, browse to **$HOME\\training-az204\\Labs\\04\\Starter\\AdventureWorks**, and then select **Select Folder**.

1.  In the **Visual Studio Code** window, on the Menu Bar, select **Terminal** and then select **New Terminal**.

1.  In the terminal, verify that the current directory is set to **AdventureWorks** (or change it to that if it's not), and then run the following command to switch your terminal context to the **AdventureWorks.Upload** folder:

    ```
    cd .\AdventureWorks.Upload\
    ```

    > **Note**: Before you perform the next step, open Windows Explorer and remove the **Read-only** attribute from the file **$HOME\\training-az204\\Labs\\04\\Starter\\AdventureWorks\\AdventureWorks.Upload\\AdventureWorks.Upload.csproj**

1.  From the terminal prompt, run the following command to add the Azure Cosmos DB .NET client library to the currently opened project:

    ```
    dotnet add package Microsoft.Azure.Cosmos --version 3.28.0
    ```

    > **Note**: The **dotnet add package** command will add the **Microsoft.Azure.Cosmos** package from **NuGet**. For more information, refer to [Microsoft.Azure.Cosmos](https://www.nuget.org/packages/Microsoft.Azure.Cosmos).

1.  Observe the results of the build printed in the terminal. The build should complete successfully with no errors or warning messages.

1.  In the **Explorer** pane of the **Visual Studio Code** window, expand the **AdventureWorks.Upload** project.

1.  Open the **Program.cs** file.

1.  In the **Program.cs** file, review the **using** directives and note that they include **Microsoft.Azure.Cosmos**, **System.IO;**, **System.Text.Json**, **System.Threading.Tasks**, and **System.Collections.Generic**. This enables asynchronous upload of JSON items from a local file on your lab computer to a collection in a Cosmos DB database.

1.  In the **Program.cs** file, on line 14, set the value of **EndpointUrl** by replacing the empty string with the **URI** property of the Cosmos DB account that you recorded earlier in this lab. Ensure that the value is enclosed in double quotes.

1.  On line 15, set the value of **AuthorizationKey** by replacing the empty string with the **PRIMARY KEY** property of the Cosmos DB account that you recorded earlier in this lab. Ensure that the value is enclosed in double quotes.

1.  On line 18, set the value of **PartitionKey** by replacing the empty string with **"/Category"**.

1.  On line 19, set the value of **JsonFilePath** by replacing the empty string with **"$HOME\\\\training-az204\\\\Labs\\\\04\\\\Starter\\\\AdventureWorks\\\\AdventureWorks.Upload\\\\models.json"**.

1.  Within the try block, note the invocation of the **CreateDatabaseIfNotExistsAsync** method of the **CosmosClient** class. This will create a database if one doesn't already exist.

1.  Note the invocation of the **DefineContainer** method of the **Database** class. This will create a container that will host the JSON items if one doesn't already exist.

    > **Note**: The **DefineContainer** method includes a cost-minimizing option whereby you can modify the default indexing policy (which automatically indexes all attributes).

1.  Note the **using** statement that relies on a **StreamReader** object to read JSON items from a text file and deserializes them into objects of the **Model** class defined further in the **Program.cs** file.

1.  Note the foreach loop that iterates over the collection of deserialized objects and asynchronously inserts each of them into the target collection.

1.  Review the **Model** and **Product** classes that reflect the format of the objects stored in the JSON-formatted file you reviewed earlier in this lab.

1.  Save and close the **Program.cs** file.

    > **Note**: Select **Overwrite** if you received a prompt that the file is read-only.

1. In terminal, run the following command to restore any missing NuGet packages and build the project in the folder:

    ```
    dotnet build
    ```

    > **Note**: The **dotnet build** command will automatically restore any missing NuGet packages prior to building all projects in the folder.

1.  From the terminal prompt, run the following command to run the .NET Core console application:

    ```
    dotnet run
    ```

    > **Note**: The **dotnet run** command will automatically build any changes to the project and then start the web application without a debugger attached. The command will output the messages indicating the data load's progress, including the number of items inserted into the target collection and the duration of the insert operation.

1.  Observe the results of running the command printed in the terminal. The run should complete successfully, displaying the message about there being 119 items inserted into the target Cosmos DB collection.

1.  Select **Kill Terminal** (the **Recycle Bin** icon) to close the terminal pane and any associated processes.

### Task 4: Validate JSON data upload

1.  On your lab computer, switch to the **Microsoft Edge** browser window displaying the Azure portal.

1. In the Azure portal, select the **Search resources, services, and docs** text box, in the **Recent resources** list, select the **polycosmos**_[yourname]_ Azure Cosmos DB account that you created earlier in this lab.

1.  On the **Azure Cosmos DB account** blade, find and select the **Data Explorer** link on the blade.

1.  In the **Data Explorer** pane, expand the **Retail** database node.

1.  Expand the **Online** container node, and then select **New SQL Query**.

    > **Note**: The label for this option might be hidden. You can display labels by hovering over the icons in the **Data Explorer** pane.

1.  On the query tab, enter the following text:

    ```sql
    SELECT * FROM models
    ```

1.  Select **Execute Query**, and then observe the list of JSON items returned by the query.

1.  Back in the query editor, replace the existing text with the following text:

    ```sql
    SELECT VALUE COUNT(1) FROM models
    ```

1.  Select **Execute Query**, and then observe the result of the **COUNT** aggregate operation.

1.  Switch back to the **Visual Studio Code** window.

## Review

In this exercise, you used the .NET SDK for Azure Cosmos DB to insert data into Azure Cosmos DB. The web application that you implement next will use this data.