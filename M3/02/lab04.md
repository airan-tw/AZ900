## Exercise 4: Access Azure Blob Storage data

### Task 1: Upload a sample storage blob

1. On the Azure portal's navigation pane, select the **Resource groups** link.

2. On the **Resource groups** blade, select the **ConfidentialStack** resource group.

3. On the **ConfidentialStack** blade, select the **securestor**_[yourname]_ storage account.

4. On the **Storage account** blade, select the **Containers** link in the **Data storage** section.

5. In the **Containers** section, select **+ Container**.

6. In the **New container** pop-up window, perform the following actions, and then select **Create**:

    | Setting | Action |
    | -- | -- |
    | **Name** text box | Enter **drop** |
    | **Public access level** drop-down list | Select **Blob (anonymous read access for blobs only)** |

7. Return to the **Containers** section, and then select the newly created **drop** container.

8. On the **Container** blade, select **Upload**.

9. In the **Upload blob** window, perform the following actions, and then select **Upload**:

    | Setting | Action |
    | -- | -- |
    | **Files** section | Select the **Folder** icon |
    | **File Explorer** window  | Browse to **$HOME\\training-az204\\Allfiles\\Labs\\07\\Starter**, select the **records.json** file, and then select **Open** |
    | **Overwrite if files already exist** check box | Ensure that this check box is selected |

    > **Note**: Wait for the blob to upload before you continue with this lab.

10. Return to the **Container** blade, and then select the **records.json** blob in the list of blobs.

11. On the **Blob** blade, find the blob metadata, and then copy the URL for the blob.

12. On the taskbar, activate the shortcut menu for the **Microsoft Edge** icon, and then select **New window**.

13. In the new browser window, refer to the URL that you copied for the blob.

14. The JavaScript Object Notation (JSON) contents of the blob should now display. Close the browser window with the JSON contents.

15. Return to the browser window with the Azure portal, and then close the **Blob** blade.

16. Return to the **Container** blade, and then select **Change access level**.

17. In the **Change access level** pop-up window, perform the following actions:

    1. In the **Public access level** drop-down list, select **Private (no anonymous access)**.
    2. Select **OK**.

18. On the taskbar, activate the shortcut menu for the **Microsoft Edge** icon, and then select **New window**.

19. In the new browser window, refer to the URL that you copied for the blob.

20. An error message indicating that the resource wasn't found should now display.

    > **Note**: If the error message doesn't display, your browser might have cached the file. Select Ctrl+F5 to refresh the page until the error message displays.

### Task 2: Pull and configure the Azure SDK for .NET

1. On the taskbar, select the **Windows Terminal** icon.

2. Run the following command to change the current directory to the **$HOME\\training-az204\\Allfiles\\Labs\\07\\Starter\\func** empty directory:

    ```powershell
    cd $HOME\training-az204\Allfiles\Labs\07\Starter\func
    ```

3. Run the following command to add version **12.12.0** of the **Azure.Storage.Blobs** package from NuGet:

    ```powershell
    dotnet add package Azure.Storage.Blobs --version 12.12.0
    ```

    > **Note**: The [Azure.Storage.Blobs](https://www.nuget.org/packages/Azure.Storage.Blobs) NuGet package references the subset of the Azure SDK for .NET required to write code for Azure Blob Storage.

4. Close the currently running **Windows Terminal** application.

5. On the **Start** screen, select the **Visual Studio Code** tile.

6. On the **File** menu, select **Open Folder**.

7. In the **File Explorer** window that opens, browse to **$HOME\\training-az204\\Allfiles\\Labs\\07\\Starter\\func**, and then select **Select Folder**.

8. On the **Explorer** pane of the **Visual Studio Code** window, open the **FileParser.cs** file.

9. Add a **using directive** for the **Azure.Storage.Blobs** namespace:

    ```csharp
    using Azure.Storage.Blobs;
    ```

10. Review the content of the **FileParser.cs** file, which should now include:

    ```csharp
    using Azure.Storage.Blobs;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;   
    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        {
            string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
            return new OkObjectResult(connectionString);
        }
    }
    ```

### Task 3: Write Azure Blob Storage code using the Azure SDK for .NET

1. Within the **Run** method of the **FileParser** class, delete the following line of code:

    ```csharp
    return new OkObjectResult(connectionString);
    ```

2. Still within the **Run** method, add the following code block to create a new instance of the **BlobClient** class by passing in your *connectionString* variable, a  ``"drop"`` string value, and a ``"records.json"`` string value to the constructor:

    ```csharp
    BlobClient blob = new BlobClient(connectionString, "drop", "records.json");
    ```

3. Still within the **Run** method, add the following code block to use the **BlobClient.DownloadAsync** method to download the contents of the referenced blob asynchronously, and then store the result in a variable named *response*:

    ```csharp
    var response = await blob.DownloadAsync();
    ```

4. Still within the **Run** method, add the following code block to return the value of the various content stored in the *content* variable by using the **FileStreamResult** class constructor:

    ```csharp
    return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
    ```

5. Review the content of the **FileParser.cs** file again, which should now include:

    ```csharp
    using Azure.Storage.Blobs;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;
    public static class FileParser
    {
        [FunctionName("FileParser")]
        public static async Task<IActionResult> Run(
            [HttpTrigger("GET")] HttpRequest request)
        {
            string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
            BlobClient blob = new BlobClient(connectionString, "drop", "records.json");
            var response = await blob.DownloadAsync();
            return new FileStreamResult(response?.Value?.Content, response?.Value?.ContentType);
        }
    }
    ```

6. Select **Save** to save your changes to the **FileParser.cs** file.

### Task 4: Deploy and validate the Azure Functions app

1. On the taskbar, select the **Windows Terminal** icon.

2. Run the following command to change the current directory to the **$HOME\\training-az204\\Allfiles\\Labs\\07\\Starter\\func** empty directory:

    ```powershell
    cd $HOME\training-az204\Allfiles\Labs\07\Starter\func
    ```

3. Run the following command to sign in to the Azure CLI:

    ```powershell
    az login
    ```

4. In the **Microsoft Edge** browser window, enter the email address and password for your Microsoft account, and then select **Sign in**.

5. Return to the currently open **Windows Terminal** window. Wait for the sign-in process to finish.

6. Run the following command to publish the function app project again (replace the `<function-app-name>` placeholder with the name of the function app you used earlier in this lab):

    ```powershell
    func azure functionapp publish <function-app-name>
    ```

    > **Note**: As an example, if your **Function App name** is **securefuncstudent**, your command would be ``func azure functionapp publish securefuncstudent``. You can review the documentation to [publish the local function app project][azure-functions-core-tools-publish-azure] using the **Azure Functions Core Tools**.

7. Wait for the deployment to finalize before you move forward with the lab.

8. Close the currently running **Windows Terminal** application.

9. On the taskbar, select the **Microsoft Edge** icon, and then refer to the Azure portal (<https://portal.azure.com>).

10. On the Azure portal's navigation pane, select the **Resource groups** link.

11. On the **Resource groups** blade, select the **ConfidentialStack** resource group.

12. On the **ConfidentialStack** blade, select the **securefunc[yourname]** function app.

13. On the **App Service** blade, select the **Functions** option in the **Functions** section.

14. On the **Functions** pane, select the existing **FileParser** function.

15. On the **Function** blade, select the **Code + Test** option in the **Developer** section.

16. In the function editor, select **Test/Run**.

17. In the automatically displayed pane, in the **HTTP method** list, select **GET**.

18. Select **Run** to test the function.

19. Review the results of the test run. The output will contain the content of the **$/drop/records.json** blob stored in your Azure Storage account.

## Review

In this exercise, you used C\# code to access a storage account, and then downloaded the contents of a blob.