## Lab 3: Configure a .NET web application

### Task 1: Update references to data stores and build the web application

1.  In the **Explorer** pane of the **Visual Studio Code** window, expand the **AdventureWorks.Web** project.

1.  Open the **appsettings.json** file.

1.  In the JSON object on line 3, find the **ConnectionStrings.AdventureWorksCosmosContext** path. Note that the current value is empty:

    ```json
    "ConnectionStrings": {
        "AdventureWorksCosmosContext": "",
    },
    ```

1.  Update the value of the **AdventureWorksCosmosContext** property by setting its value to the **PRIMARY CONNECTION STRING** of the Azure Cosmos DB account that you recorded earlier in this lab.

1.  In the JSON object on line 6, find the **Settings.BlobContainerUrl** path. Note that the current value is empty:

    ```json
    "Settings": {
        "BlobContainerUrl": "",
        ...
    }
    ```

1.  Update the **BlobContainerUrl** property by setting its value to the **URL** property of the Azure Storage blob container named **images** that you recorded earlier in this lab.

1.  Save the **appsettings.json** file and close it.

    > **Note**: Select **Overwrite** if you received a prompt that the file is read-only.

1.  In the **Visual Studio Code** window, select **AdventureWorks.Context**, activate the shortcut menu, and then select **Open in Integrated Terminal**.

    > **Note**:Before you perform the next step, open Windows Explorer and remove the Read-only attribute from the file **$HOME\training-az204\Labs\04\Starter\AdventureWorks\AdventureWorks.Context\AdventureWorks.Context.csproj**

1.  From the terminal prompt, verify that the current directory is set to **AdventureWorks.Context** (or change it to that if it's not), and then run the following command to import **Microsoft.Azure.Cosmos** from NuGet:

    ```
    dotnet add package Microsoft.Azure.Cosmos --version 3.28.0
    ```

1.  From the terminal prompt, run the following command to build the .NET web application:

    ```
    dotnet build
    ```

1.  Observe the results of the build printed in the terminal. The build should complete successfully with no errors or warning messages.

### Task 2: Configure connectivity to Azure Cosmos DB

1.  In the **Explorer** pane of the **Visual Studio Code** window, expand the **AdventureWorks.Context** project.

1.  From the shortcut menu of the **AdventureWorks.Context** folder node, select **New File**.

1.  At the new file prompt, enter **AdventureWorksCosmosContext.cs**.

1.  From the code editor tab for the **AdventureWorksCosmosContext.cs** file, add the following lines of code to import the **AdventureWorks.Models** namespace from the referenced **AdventureWorks.Models** project:

    ```csharp
    using AdventureWorks.Models;
    ```

1.  Add the following lines of code to import the **Microsoft.Azure.Cosmos** and **Microsoft.Azure.Cosmos.Linq** namespaces from the **Microsoft.Azure.Cosmos** package imported from NuGet:

    ```csharp
    using Microsoft.Azure.Cosmos;
    using Microsoft.Azure.Cosmos.Linq;
    ```

1.  Add the following lines of code to include **using** directives for the built-in namespaces that this file will use:

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Threading.Tasks;
    ```

1.  Enter the following code to add an **AdventureWorks.Context** namespace block:

    ```csharp
    namespace AdventureWorks.Context
    {
    }
    ```

1.  Within the **AdventureWorks.Context** namespace, enter the following code to create a new **AdventureWorksCosmosContext** class:

    ```csharp
    public class AdventureWorksCosmosContext
    {
    }
    ```

1.  Update the declaration of the **AdventureWorksCosmosContext** class by adding a specification indicating that this class will implement the **IAdventureWorksProductContext** interface:

    ```csharp
    public class AdventureWorksCosmosContext : IAdventureWorksProductContext
    {
    }
    ```

1.  Within the **AdventureWorksCosmosContext** class, enter the following code to create a new read-only *Container* variable named **_container**:

    ```csharp
    private readonly Container _container;
    ```

1.  Within the **AdventureWorksCosmosContext** class, add a new constructor with the following signature:

    ```csharp
    public AdventureWorksCosmosContext(string connectionString, string database = "Retail", string container = "Online")
    {
    }
    ```

1.  Within the constructor, add the following block of code to create a new instance of the **CosmosClient** class, and then obtain both a **Database** and **Container** instance from the client:

    ```csharp
    _container = new CosmosClient(connectionString)
        .GetDatabase(database)
        .GetContainer(container);
    ```

1.  Within the **AdventureWorksCosmosContext** class, add a new **FindModelAsync** method with the following signature:

    ```csharp
    public async Task<Model> FindModelAsync(Guid id)
    {
    }
    ```

1.  Within the **FindModelAsync** method, add the following blocks of code to create a LINQ query, transform it into an iterator, iterate over the result set, and then return the single item in the result set:

    ```csharp
    var iterator = _container.GetItemLinqQueryable<Model>()
        .Where(m => m.id == id)
        .ToFeedIterator<Model>();
    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }
    return matches.SingleOrDefault();
    ```

1.  Within the **AdventureWorksCosmosContext** class, add a new **GetModelsAsync** method with the following signature:

    ```csharp
    public async Task<List<Model>> GetModelsAsync()
    {
    }
    ```

1.  Within the **GetModelsAsync** method, add the following blocks of code to run an SQL query, get the query result iterator, iterate over the result set, and then return the union of all results:

    ```csharp
    string query = $@"SELECT * FROM items";
    var iterator = _container.GetItemQueryIterator<Model>(query);
    List<Model> matches = new List<Model>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }
    return matches;
    ```

1.  Within the **AdventureWorksCosmosContext** class, add a new **FindProductAsync** method with the following signature:

    ```csharp
    public async Task<Product> FindProductAsync(Guid id)
    {
    }
    ```

1.  Within the **FindProductAsync** method, add the following blocks of code to run an SQL query, get the query result iterator, iterate over the result set, and then return the single item in the result set:

    ```csharp
    string query = $@"SELECT VALUE products
                        FROM models
                        JOIN products in models.Products
                        WHERE products.id = '{id}'";
    var iterator = _container.GetItemQueryIterator<Product>(query);
    List<Product> matches = new List<Product>();
    while (iterator.HasMoreResults)
    {
        var next = await iterator.ReadNextAsync();
        matches.AddRange(next);
    }
    return matches.SingleOrDefault();
    ```

1.  Save and close the **AdventureWorksCosmosContext.cs** file.
   
1.  From the terminal prompt, with the current directory set to **AdventureWorks.Context**, run the following command to build the .NET web application:

    ```
    dotnet build
    ```

    > **Note**: If there are any build errors, review the **AdventureWorksCosmosContext.cs** file in the **$HOME\\training-az204\\Labs\\04\\Solution\\AdventureWorks\\AdventureWorks.Context** folder.

### Task 3: Review the .NET application startup logic

1.  In the **Explorer** pane of the **Visual Studio Code** window, expand the **AdventureWorks.Web** project.

1.  Open the **Startup.cs** file.

1.  In the **Startup** class, note the existing **ConfigureProductService** method:

    ```csharp
    public void ConfigureProductService(IServiceCollection services)
    {
        services.AddScoped<IAdventureWorksProductContext, AdventureWorksCosmosContext>(provider =>
            new AdventureWorksCosmosContext(
                _configuration.GetConnectionString(nameof(AdventureWorksCosmosContext))
            )
        );
    }
    ```

    > **Note**: The product service uses Cosmos DB as its database.

1.  Close the **Startup.cs** file without making any modifications.

### Task 4: Validate that the .NET application successfully connects to data stores

1.  In Visual Studio Code, from the terminal prompt, run the following command to switch your terminal context to the **AdventureWorks.Web** folder:

    ```
    cd ..\AdventureWorks.Web\
    ```

1.  From the terminal prompt, run the following command to run the ASP.NET web application:

    ```
    dotnet run
    ```

    > **Note**: The **dotnet run** command will automatically build any changes to the project and then start the web application without a debugger attached. The command will output the URL of the running application and any assigned ports.

1.  On the taskbar, select the **Microsoft Edge** icon.

1.  In the open browser window, browse to the currently running web application (<http://localhost:5000>).

1.  In the web application, observe the list of models displayed from the front page.

1.  Find the **Touring-1000** model, and then select **View Details**.

1.  On the **Touring-1000** product detail page, review the listing of options.

1.  Close the browser window displaying your web application.

1.  Switch to the **Visual Studio Code** window, and then select **Kill Terminal** (the **Recycle Bin** icon) to close the currently open terminal and any associated processes.

## Review

In this exercise, you wrote C# code to query an Azure Cosmos DB collection by using the .NET SDK.