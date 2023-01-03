## Lab 3: Build an Azure Functions app

### Task 1: Initialize a function project

1. On the taskbar, select the **Windows Terminal** icon.

2. Run the following command to change the current directory to the **$HOME\\training-az204\\\Allfiles\\Labs\\07\\Starter\\func** empty directory:

    ```powershell
    $HOME\training-az204\Allfiles\Labs\07\Starter\func
    ```

    > **Note**: In Windows Explorer remove the Read-only attribute from $HOME\training-az204\Allfiles\Labs\07\Starter\func\.gitignore file.

3. Run the following command to use the **Azure Functions Core Tools** to create a new local Functions project in the current directory using the **dotnet** runtime:

    ```powershell
    func init --worker-runtime dotnet --force
    ```

    > **Note**: You can review the documentation to [create a new project][azure-functions-core-tools-new-project] using the **Azure Functions Core Tools**.

4. Run the following command to **build** the .NET 6 project:

    ```powershell
    dotnet build
    ```

### Task 2: Create an HTTP-triggered function

1. Run the following command to use the **Azure Functions Core Tools** to create a new function named **FileParser** using the **HTTP trigger** template:

    ```powershell
    func new --template "HTTP trigger" --name "FileParser"
    ```

    > **Note**: You can review the documentation to [create a new function][azure-functions-core-tools-new-function] using the **Azure Functions Core Tools**.

2. Close the currently running **Windows Terminal** application.

### Task 3: Configure and read an application setting

1. On the **Start** screen, select the **Visual Studio Code** tile.

2. On the **File** menu, select **Open Folder**.

3. In the **File Explorer** window that opens, browse to **$HOME\\training-az204\\Allfiles\\Labs\\07\\Starter\\func**, and then select **Select Folder**.

4. On the **Explorer** pane of the **Visual Studio Code** window, open the **local.settings.json** file.

5. Note the current value of the **Values** object:

    ```json
    "Values": {
        "AzureWebJobsStorage": "UseDevelopmentStorage=true",
        "FUNCTIONS_WORKER_RUNTIME": "dotnet"
    }
    ```

6. Update the value of the **Values** object by adding a new setting named **StorageConnectionString**, and then assigning it a string value of **[TEST VALUE]**:

    ```json
    "Values": {
        "AzureWebJobsStorage": "UseDevelopmentStorage=true",
        "FUNCTIONS_WORKER_RUNTIME": "dotnet",
        "StorageConnectionString": "[TEST VALUE]"
    }
    ```

7. The **local.settings.json** file should now include:

    ```json
    {
        "IsEncrypted": false,
        "Values": {
            "AzureWebJobsStorage": "UseDevelopmentStorage=true",
            "FUNCTIONS_WORKER_RUNTIME": "dotnet",
            "StorageConnectionString": "[TEST VALUE]"
        }
    }
    ```

8. Select **Save** to save your changes to the **local.settings.json** file.

9. On the **Explorer** pane of the **Visual Studio Code** window, open the **FileParser.cs** file.

10. In the code editor, review the example implementation:

    ```csharp
    using System;
    using System.IO;
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Extensions.Http;
    using Microsoft.AspNetCore.Http;
    using Microsoft.Extensions.Logging;
    using Newtonsoft.Json;
    namespace func
    {
        public static class FileParser
        {
            [FunctionName("FileParser")]
            public static async Task<IActionResult> Run(
                [HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
                ILogger log)
            {
                log.LogInformation("C# HTTP trigger function processed a request.");
                string name = req.Query["name"];
                string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
                dynamic data = JsonConvert.DeserializeObject(requestBody);
                name = name ?? data?.name;
                string responseMessage = string.IsNullOrEmpty(name)
                    ? "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
                    : $"Hello, {name}. This HTTP triggered function executed successfully.";
                return new OkObjectResult(responseMessage);
            }
        }
    }
    ```

11. Delete all of the content within the **FileParser.cs** file.

12. Add the following lines of code to add **using directives** for the **Microsoft.AspNetCore.Mvc**, **Microsoft.Azure.WebJobs**, **Microsoft.AspNetCore.Http**, **System**, and **System.Threading.Tasks** namespaces:

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;
    ```

13. Create a new **public static** class named **FileParser**:

    ```csharp
    public static class FileParser
    { }
    ```

14. Observe the **FileParser.cs** file again, which should now include:

    ```csharp
    using Microsoft.AspNetCore.Mvc;
    using Microsoft.Azure.WebJobs;
    using Microsoft.AspNetCore.Http;
    using System;
    using System.Threading.Tasks;
    public static class FileParser
    { }
    ```

15. Within the **FileParser** class, add the following code block to create a new **public static** *asynchronous* method named **Run**. This method returns a variable of type **Task\<IActionResult\>** and also takes in a variable of type **HttpRequest** named *request*:

    ```csharp
    public static async Task<IActionResult> Run(
        HttpRequest request)
    { }
    ```

16. Add the following code to append an attribute to the **Run** method of type **FunctionNameAttribute** that has its **name** parameter set to a value of **FileParser**:

    ```csharp
    [FunctionName("FileParser")]
    public static async Task<IActionResult> Run(
        HttpRequest request)
    { }
    ```

17. Add the following code to append an attribute to the **request** parameter of type **HttpTriggerAttribute** that has its **methods** parameter array set to a single value of **GET**:

    ```csharp
    [FunctionName("FileParser")]
    public static async Task<IActionResult> Run(
        [HttpTrigger("GET")] HttpRequest request)
    { }
    ```

18. Review the content of the **FileParser.cs** file again, which should now include:

    ```csharp
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
        { }
    }
    ```

19. In the **Run** method, enter the following line of code to retrieve the value of the **StorageConnectionString** application setting by using the **Environment.GetEnvironmentVariable** method and to store the result in a **string** variable named **connectionString**:

    ```csharp
    string connectionString = Environment.GetEnvironmentVariable("StorageConnectionString");
    ```

20. Enter the following line of code to return the value of the **connectionString** variable as the HTTP response:

    ```csharp
    return new OkObjectResult(connectionString);
    ```

21. Review the content of the **FileParser.cs** file again, which should now include:

    ```csharp
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

22. Select **Save** to save your changes to the **FileParser.cs** file.

### Task 4: Validate the local function

1. On the taskbar, select the **Windows Terminal** icon.

2. Run the following command to change the current directory to the **$HOME\\training-az204\\Allfiles\\Labs\\07\\Starter\\func** empty directory:

    ```powershell
    cd $HOME\training-az204\Allfiles\Labs\07\Starter\func
    ```

3. Run the following command to run the function app project:

    ```powershell
    func start --build
    ```

    > **Note**: You can review the documentation to [start the function app project locally][azure-functions-core-tools-start-function] using the **Azure Functions Core Tools**.

4. On the taskbar, select the **Windows Terminal** icon again to open a new instance of the **Windows Terminal** application. Run the following command to change the current directory to the **$HOME\\training-az204\\Allfiles\\Labs\\07\\Starter\\func** empty directory:

    ```powershell
    cd $HOME\training-az204\Allfiles\Labs\07\Starter\func
    ```
    
5. When you receive the open command prompt, run the following command to start the **httprepl** tool, setting the base Uniform Resource Identifier (URI) to ``http://localhost:7071``:

    ```powershell
    httprepl http://localhost:7071
    ```

    > **Note**: An error message is displayed by the **httprepl** tool. This message occurs because the tool is searching for a Swagger definition file to use to traverse the API. Because your function project doesn't produce a Swagger definition file, you'll need to traverse the API manually.
6. When you receive the tool prompt, run the following command to browse to the relative **api** directory:

    ```powershell
    cd api
    ```

7. Run the following command to browse to the relative **fileparser** directory:

    ```powershell
    cd fileparser
    ```

8. Run the following command to run the **get** command:

    ```powershell
    get
    ```

9. Observe the **[TEST VALUE]** value of the **StorageConnectionString** being returned as the result of the HTTP request:

    ```powershell
    HTTP/1.1 200 OK
    Content-Type: text/plain; charset=utf-8
    Date: Tue, 01 Sep 2020 23:35:39 GMT
    Server: Kestrel
    Transfer-Encoding: chunked
    [TEST VALUE]
    ```

10. Run the following command to exit the **httprepl** tool:

    ```powershell
    exit
    ```

11. Close all currently running instances of the **Windows Terminal** application.

### Task 5: Deploy the function using the Azure Functions Core Tools

1. On the taskbar, select the **Windows Terminal** icon.

2. Run the following command to change the current directory to the **$HOME\\training-az204\\Allfiles\\Labs\\07\\Starter\\func** empty directory:

    ```powershell
    cd $HOME\training-az204\Allfiles\Labs\07\Starter\func
    ```

3. Run the following command to sign in to the Azure Command-Line Interface (CLI):

    ```powershell
    az login
    ```

4. In the **Microsoft Edge** browser window, enter the email address and password for your Microsoft account, and then select **Sign in**.

5. Return to the currently open **Windows Terminal** window. Wait for the sign-in process to finish.

6. Run the following command to publish the function app project (replace the `<function-app-name>` placeholder with the name of the function app you created earlier in this lab):

    ```powershell
    func azure functionapp publish <function-app-name>
    ```

    > **Note**: As an example, if your **Function App name** is **securefuncstudent**, your command would be ``func azure functionapp publish securefuncstudent``. You can review the documentation to [publish the local function app project][azure-functions-core-tools-publish-azure] using the **Azure Functions Core Tools**.

7. Wait for the deployment to finalize before you move forward with the lab.

8. Close the currently running **Windows Terminal** application.

### Task 6: Test the Key Vault-derived application setting

1. On the taskbar, select the **Microsoft Edge** icon, and then select the tab that contains the Azure portal (<https://portal.azure.com>).

2. On the Azure portal's navigation pane, select the **Resource groups** link.

3. On the **Resource groups** blade, select the **ConfidentialStack** resource group.

4. On the **ConfidentialStack** blade, select the **securefunc[yourname]** function app.

5. On the **Function App** blade, select the **Functions** option in the **Functions** section.

6. On the **Functions** pane, select the existing **FileParser** function.

7. On the **Function** blade, select the **Code + Test** option in the **Developer** section.

8. In the function editor, select **Test/Run**.

9. In the automatically displayed pane, in the **HTTP method** list, select **GET**.

10. Select **Run** to test the function.

11. Review the results of the test run. The result should be your Azure Storage connection string.

## Review

In this exercise, you used a service identity to read the value of a secret stored in Key Vault and returned that value as the result of a function app.