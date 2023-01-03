## Lab 3: Access containers by using the .NET SDK

### Task 1: Create .NET project

1.  On the **Start** screen, select the **Visual Studio Code** tile.

1.  On the **File** menu, select **Open Folder**, browse to **$HOME\\training-az204\\Labs\\03\\Starter\\BlobManager**, and then select **Select Folder**.

1.  In the **Visual Studio Code** window, on the Menu Bar, select **Terminal** and then select **New Terminal**.

1.  In the terminal, run the following command to create a new .NET project named **BlobManager** in the current folder:

    ```
    dotnet new console --framework net6.0 --name BlobManager --output .
    ```

    > **Note**: The **dotnet new** command will create a new **console** project in a folder with the same name as the project.

1.  In the terninal, run the following command to import version 12.12.0 of **Azure.Storage.Blobs** from NuGet:

    ```
    dotnet add package Azure.Storage.Blobs --version 12.12.0
    ```

    > **Note**: The **dotnet add package** command will add the **Azure.Storage.Blobs** package from NuGet. For more information, refer to [Azure.Storage.Blobs](https://www.nuget.org/packages/Azure.Storage.Blobs/12.12.0).

1.  In the terminal, run the following command to build the .NET web application:

    ```
    dotnet build
    ```

1.  Select **Kill Terminal** or the **Recycle Bin** icon to close the currently open terminal and any associated processes.

### Task 2: Modify the Program class to access Storage

1.  On the **Explorer** pane of the **Visual Studio Code** window, open the **Program.cs** file.

1.  On the code editor tab for the **Program.cs** file, delete all the code in the existing file.

1.  Add the following line of code to import the **Azure.Storage**, **Azure.Storage.Blobs**, and **Azure.Storage.Blobs.Models** namespaces from the **Azure.Storage.Blobs** package imported from NuGet:

    ```csharp
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;
    ```
    
1.  Add the following lines of code to add **using** directives for the built-in namespaces that will be used in this file:

    ```csharp
    using System;
    using System.Threading.Tasks;
    ```

1.  Enter the following code to create a new **Program** class:

    ```csharp
    public class Program
    {
    }
    ```

1.  In the **Program** class, enter the following line of code to create a new string constant named **blobServiceEndpoint**:

    ```csharp
    private const string blobServiceEndpoint = "";
    ```

1.  Update the **blobServiceEndpoint** string constant by setting its value to the **Primary Blob Service Endpoint** of the storage account that you recorded previously in this lab.

1.  In the **Program** class, enter the following line of code to create a new string constant named **storageAccountName**:

    ```csharp
    private const string storageAccountName = "";
    ```

1.  Update the **storageAccountName** string constant by setting its value to the **Storage account name** of the storage account that you recorded previously in this lab.

1.  In the **Program** class, enter the following line of code to create a new string constant named **storageAccountKey**:

    ```csharp
    private const string storageAccountKey = "";
    ```

1.  Update the **storageAccountKey** string constant by setting its value to the **Key** of the storage account that you recorded previously in this lab.

1.  In the **Program** class, enter the following code to create a new asynchronous **Main** method:

    ```csharp
    public static async Task Main(string[] args)
    {
    }
    ```

1.  Review the **Program.cs** file, which should now include:

    ```csharp
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;
    using System;
    using System.Threading.Tasks;    
    public class Program
    {
        private const string blobServiceEndpoint = "<primary-blob-service-endpoint>";
        private const string storageAccountName = "<storage-account-name>";
        private const string storageAccountKey = "<key>";    
        public static async Task Main(string[] args)
        {
        }
    }
    ```

### Task 3: Connect to the Azure Storage blob service endpoint

1.  In the **Main** method, add the following line of code to create a new instance of the **StorageSharedKeyCredential** class by using the **storageAccountName** and **storageAccountKey** constants as constructor parameters:

    ```csharp
    StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);
    ```

1.  In the **Main** method, add the following line of code to create a new instance of the **BlobServiceClient** class by using the **blobServiceEndpoint** constant and the *accountCredentials* variable as constructor parameters:

    ```csharp
    BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);
    ```

1.  In the **Main** method, add the following line of code to invoke the **GetAccountInfoAsync** method of the **BlobServiceClient** class to retrieve account metadata from the service:

    ```csharp
    AccountInfo info = await serviceClient.GetAccountInfoAsync();
    ```
    
1.  In the **Main** method, add the following line of code to render a welcome message:

    ```csharp
    await Console.Out.WriteLineAsync($"Connected to Azure Storage Account");
    ```
    
1.  In the **Main** method, add the following line of code to render the storage account's name:

    ```csharp
    await Console.Out.WriteLineAsync($"Account name:\t{storageAccountName}");
    ```
    
1.  In the **Main** method, add the following line of code to render the type of storage account:

    ```csharp
    await Console.Out.WriteLineAsync($"Account kind:\t{info?.AccountKind}");
    ```
    
1.  In the **Main** method, add the following line of code to render the currently selected stock keeping unit (SKU) for the storage account:

    ```csharp
    await Console.Out.WriteLineAsync($"Account sku:\t{info?.SkuName}");
    ```

1.  Review the **Main** method, which should now include:

    ```csharp
    public static async Task Main(string[] args)
    {
        StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);
        BlobServiceClient serviceClient = new BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);
        AccountInfo info = await serviceClient.GetAccountInfoAsync();
        await Console.Out.WriteLineAsync($"Connected to Azure Storage Account");
        await Console.Out.WriteLineAsync($"Account name:\t{storageAccountName}");
        await Console.Out.WriteLineAsync($"Account kind:\t{info?.AccountKind}");
        await Console.Out.WriteLineAsync($"Account sku:\t{info?.SkuName}");
    }
    ```

1.  Save the **Program.cs** file.

1.  In the **Visual Studio Code** window, on the Menu Bar, select **Terminal** and then select **New Terminal**.

1.  In the terminal, run the following command to run the .NET web application:

    ```
    dotnet run
    ```

    > **Note**: If there are any build errors, review the **Program.cs** file in the **$HOME\\training-az204\\\Labs\\03\\Solution\\BlobManager** folder.

1.  Observe the output from the currently running console application. The output contains metadata for the storage account that was retrieved from the service.

1.  Select **Kill Terminal** or the **Recycle Bin** icon to close the currently open terminal and any associated processes.

### Task 4: Enumerate the existing containers

1.  In the **Program** class, enter the following code to create a new **private static** method named **EnumerateContainersAsync**, that's asynchronous and has a single **BlobServiceClient** parameter type:

    ```csharp
    private static async Task EnumerateContainersAsync(BlobServiceClient client)
    {        
    }
    ```

1.  In the **EnumerateContainersAsync** method, enter the following code to create an asynchronous **foreach** loop that iterates over the results of an invocation of the **GetBlobContainersAsync** method of the **BlobServiceClient** class:

    ```csharp
    await foreach (BlobContainerItem container in client.GetBlobContainersAsync())
    {
    }
    ```

1.  Within the **foreach** loop, enter the following code to print the name of each container:

    ```csharp
    await Console.Out.WriteLineAsync($"Container:\t{container.Name}");
    ```

1.  Review the **EnumerateContainersAsync** method, which should now include:

    ```csharp
    private static async Task EnumerateContainersAsync(BlobServiceClient client)
    {        
        await foreach (BlobContainerItem container in client.GetBlobContainersAsync())
        {
            await Console.Out.WriteLineAsync($"Container:\t{container.Name}");
        }
    }
    ```

1.  In the **Main** method, enter the following code at the end of the method to invoke the **EnumerateContainersAsync** method, passing in the *serviceClient* variable as a parameter:

    ```csharp
    await EnumerateContainersAsync(serviceClient);
    ```

1.  Observe the **Program.cs** file, which should now include:
    ```csharp
    using Azure.Storage;
    using Azure.Storage.Blobs;
    using Azure.Storage.Blobs.Models;
    using System;
    using System.Threading.Tasks;
    
    public class Program
    {
        private const string blobServiceEndpoint = "your blobServiceEndpoint";
        private const string storageAccountName = "your storageAccountName";
        private const string storageAccountKey = "your storageAccountKey";    
        public static async Task Main(string[] args)
        {
            StorageSharedKeyCredential accountCredentials = new StorageSharedKeyCredential(storageAccountName, storageAccountKey);
            BlobServiceClient serviceClient = new     BlobServiceClient(new Uri(blobServiceEndpoint), accountCredentials);
            AccountInfo info = await serviceClient.GetAccountInfoAsync();
            await Console.Out.WriteLineAsync($"Connected to Azure Storage Account");
            await Console.Out.WriteLineAsync($"Account name:\t{storageAccountName}");
            await Console.Out.WriteLineAsync($"Account kind:\t{info?.AccountKind}");
            await Console.Out.WriteLineAsync($"Account sku:\t{info?.SkuName}");
            await EnumerateContainersAsync(serviceClient);
        }        
        private static async Task EnumerateContainersAsync(BlobServiceClient client)
        {        
            await foreach (BlobContainerItem container in client.GetBlobContainersAsync())
            {
                await Console.Out.WriteLineAsync($"Container:\t{container.Name}");
            }
    }
    }
    ```

1.  Save the **Program.cs** file.

1.  In the **Visual Studio Code** window, on the Menu Bar, select **Terminal** and then select **New Terminal**.

1.  In the terminal, run the following command to run the .NET web application:

    ```
    dotnet run
    ```

    > **Note**: If there are any build errors, review the **Program.cs** file in the **$HOME\\training-az204\\Labs\\03\\Solution\\BlobManager** folder.

1.  Observe the output from the currently running console application. The updated output includes a list of every existing container in the account.

1.  Select **Kill Terminal** or the **Recycle Bin** icon to close the currently open terminal and any associated processes.

## Review

In this exercise, you accessed existing containers by using the Azure Storage SDK.
