## Lab 01: Build a backend API by using Azure Storage and the Web Apps feature of Azure App Service

### Task 1: Open the Azure portal

1. In the browser window, browse to the Azure portal (<https://portal.azure.com>), and then sign in with the account you'll be using for this lab.

   > **Note**: If this is your first time signing in to the Azure portal, you'll be offered a tour of the portal. If you prefer to skip the tour, select **Maybe later** to begin using the portal.

### Task 2: Create a Storage account

1. In the Azure portal, use the **Search resources, services, and docs** text box to search for **Storage Accounts**, and then in the list of results, select **Storage Accounts**.

1. On the **Storage accounts** blade, select **+ Create**.

1. On the **Create a storage account** blade, on the **Basics** tab, perform the following actions, and then select **Review**:

    | Setting | Action |
    | -- | -- |
    | **Subscription** drop-down list | Retain the default value |
    | **Resource group** section | Select **Create new**, enter **ManagedPlatform**, and then select **OK** |
    | **Storage account name** text box | Enter **imgstor**_[yourname]_ | 
    | **Region** drop-down list | Select **(US) East US** |
    | **Performance** section | Select the **Standard** option |
    | **Redundancy** drop-down list | Select **Locally-redundant storage (LRS)** |

    The following screenshot displays the configured settings on the **Basics** tab of the **Create a storage account** blade.

   ![alt text](images/l01_create_a_storage_account.png)

1. On the **Review** tab, review the options that you selected during the previous steps.

1. Select **Create** to create the storage account by using your specified configuration.

    > **Note**: Wait for the creation task to complete before you proceed with this lab.

1. On the **Overview** blade, select the **Go to resource** button to navigate to the blade of the newly created storage account.

1. On the **Storage account** blade, in the **Security + networking** section, select **Access keys**.

1. On the **Access keys** blade, select **Show keys**.

1. Review any one of the keys, and then copy the value of either of the **Connection string** boxes to the clipboard.

    > **Note**: It doesn't matter which connection string you choose. They are interchangeable.

1. Open Notepad, and then paste the copied connection string value to Notepad. You'll use this value later in this lab.

### Task 3: Upload a sample blob

1. On the **Storage Account** blade, in the **Data storage** section, select the **Containers** link.

1. On the **Containers** blade, select **+ Container**.

1. In the **New container** window, perform the following actions:

    | Setting  | Action |
    | -- | -- |
    | **Name** text box | Enter **images** |
    | **Public access level** list | Select **Blob (anonymous read access for blobs only)**, and then select **Create** |

1. On the **Containers** blade, select the newly created **images** container.

1. On the **images** blade, select **Upload**.

1. In the **Upload blob** window, perform the following actions:

    | Setting | Action |
    | -- | -- |
    | **Files** section | Select the **Folder** icon |
    | **File Explorer** window | Browse to **Allfiles (F):\\Allfiles\\Labs\\01\\Starter\\Images**, select the **grilledcheese.jpg** file, and then select **Open** |
    | **Overwrite if files already exist** check box | Ensure that the check box is selected, and then select **Upload** |

    > **Note**: Wait for the blob to upload before you continue with this lab.

### Task 4: Create a web app

1. On the Azure portal's navigation pane, select **Create a resource**.

1. On the **Create a resource** blade, in the **Search services and marketplace** text box, enter **Web App**, and then select Enter.

1. On the **Marketplace** search results blade, select the **Web App** result.

1. On the **Web App** blade, select **Create**.

1. On the **Create Web App** blade, on the **Basics** tab, perform the following actions, and then select the **Monitoring** tab:

    | Setting | Action |
    | -- | -- |
    | **Subscription** drop-down list | Retain the default value |
    | **Resource group** section | Select **ManagedPlatform** |
    | **Name** text box | Enter **imgapi**_[yourname]_ |
    | **Publish** section | Select **Code** |
    | **Runtime stack** drop-down list | Select **.NET 6 (LTS)** |
    | **Operating System** section | Select **Windows** |
    | **Region** drop-down list | Select the **East US** region |
    | **Windows Plan (East US)** section | Select **Create new**, enter the value **ManagedPlan** in the **Name** text box, and then select **OK** |
    | **SKU and size** section | Retain the default value |

    The following screenshot displays the configured settings on the **Create web app** blade.

    ![alt text](images/l01_create_a_web_app.png)

1. On the **Monitoring** tab, in the **Enable Application Insights** section, select **No**, and then select **Review + create**.

1. On the **Review + create** tab, review the options that you selected during the previous steps.

1. Select **Create** to create the web app by using your specified configuration. 

   > **Note**: Wait for the web app to be created before you continue with this lab.

1. On the **Overview** blade, select the **Go to resource** button to navigate to the blade of the newly created web app.

### Task 5: Configure the web app

1. On the **App Service** blade, in the **Settings** section, select the **Configuration** link.

1. In the **Configuration** section, perform the following actions, select **Save**, and then select **Continue**.

    | Setting | Action |
    | -- | -- |
    | **Application settings** tab | Select **New application setting** |
    | **Add/Edit application setting** pop-up dialog | In the **Name** text box, enter **StorageConnectionString** |
    | **Value** text box | Paste the storage connection string that you previously copied to Notepad |
    | **Deployment slot setting** text box | Retain the default value, and then select **OK** to close the pop-up dialog and return to the **Configuration** section |

    Wait for your application settings to save before you continue with the lab.

1. On the **App Service** blade in the **Settings** section, select the **Properties** link.

1. In the **Properties** section, copy the value of the **URL** hyperlink, and then paste it to Notepad. You'll use this value later in the lab.

    > **Note**: At this point, the web server at this URL will return a placeholder webpage. You haven't deployed any code to the Web App yet. You'll deploy code to the Web App later in this lab.

### Task 6: Deploy an `ASP.NET` web application to Web Apps

1. On the taskbar, select the **Visual Studio Code** icon.

1. On the **File** menu, select **Open Folder**.

1. In the **File Explorer** window, browse to **Allfiles (F):\\Allfiles\\Labs\\01\\Starter\\API**, and then select **Select Folder**.

    > **Note**: Ignore any prompts to add required assets to build and debug and to run the restore command to address unresolved dependencies.

1. On the **Explorer** pane of the **Visual Studio Code** window, expand the **Controllers** folder, and then select the **ImagesController.cs** file to open the file in the editor.

1. In the editor, in the **ImagesController** class on line 26, observe the **GetCloudBlobContainer** method and the code used to retrieve a container.

1. In the **ImagesController** class on line 36, observe the **Get** method and the code used to retrieve all blobs asynchronously from the **images** container.

1. In the **ImagesController** class on line 55, observe the **Post** method and the code used to persist an uploaded image to  Storage.

1. On the taskbar, select the **Windows Terminal** icon.

1. At the open command prompt, enter the following command, and then select Enter to sign in to the Azure Command-Line Interface (CLI):

    ```
    az login
    ```

1. In the **Microsoft Edge** browser window, enter the email address and password for your Microsoft account, and then select **Sign in**.

1. Return to the currently open Windows terminal **Command Prompt** window. Wait for the sign-in process to finish.

1. At the command prompt, enter the following command, and then select Enter to list all the apps in your **ManagedPlatform** resource group:

    ```
    az webapp list --resource-group ManagedPlatform
    ```

1. Enter the following command, and then select Enter to find the apps that have the **imgapi\*** prefix:

    ```
    az webapp list --resource-group ManagedPlatform --query "[?starts_with(name, 'imgapi')]"
    ```

1. Enter the following command, and then select Enter to render only the name of the single app that has the **imgapi\*** prefix:

    ```
    az webapp list --resource-group ManagedPlatform --query "[?starts_with(name, 'imgapi')].{Name:name}" --output tsv
    ```

1. Enter the following command, and then select Enter to change the current directory to the **Allfiles (F):\\Allfiles\\Labs\\01\\Starter\\API** directory that contains the lab files:

    ```
    cd F:\Allfiles\Labs\01\Starter\API\
    ```

1. Enter the following command, and then select Enter to deploy the **api.zip** file to the web app that you created previously in this lab:

    ```
    az webapp deployment source config-zip --resource-group ManagedPlatform --src api.zip --name <name-of-your-api-app>
    ```

    > **Note**: Replace the *\<name-of-your-api-app\>* placeholder with the name of the web app that you created previously in this lab. You recently queried this app’s name in the previous steps.

    Wait for the deployment to complete before you continue with this lab.

1. On the Azure portal's **navigation** pane, select the **Resource groups** link.

1. On the **Resource groups** blade, select the **ManagedPlatform** resource group that you created previously in this lab.

1. On the **ManagedPlatform** blade, select the **imgapi**_[yourname]_ web app that you created previously in this lab.

1. From the **App Service** blade, select **Browse**.

    > **Note**: The **Browse** command will perform a GET request to the root of the website, which returns a JavaScript Object Notation (JSON) array. This array should contain the URL for your single uploaded image in your Storage account.

1. Return to your browser window that contains the Azure portal.

1. Close the currently running Visual Studio Code and Windows Terminal applications.

## Review

In this exercise, you created a web app in Azure, and then deployed your `ASP.NET` web application to Web Apps by using the Azure CLI and Apache Kudu zip file deployment utility.