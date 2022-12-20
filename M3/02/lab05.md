## Lab 5: Clean up your subscription

### Task 1: Open Azure Cloud Shell

1. In the Azure portal, select the **Cloud Shell** icon ![Cloud Shell icon](images/az204_lab_CloudShell.png) to open a new Bash session. If Cloud Shell defaults to a PowerShell session, select **PowerShell**, and in the drop-down menu, select **Bash**.

    > **Note**: If this is the first time you're starting **Cloud Shell**, when prompted to select either **Bash** or **PowerShell**, select **PowerShell**. When you're presented with the **You have no storage mounted** message, select the subscription you're using in this lab, and then select **Create storage**.

### Task 2: Delete a resource group

1. On the **Cloud Shell** pane, run the following command to delete the **ConfidentialStack** resource group:

    ```bash
    az group delete --name ConfidentialStack --no-wait --yes
    ```

     > **Note**: The command runs asynchronously (as determined by the *--no-wait* parameter), so while you'll be able to run another Azure CLI command immediately afterwards within the same Bash session, it'll take a few minutes before the resource groups are actually removed.

1. Close the **Cloud Shell** pane in the portal.

### Task 3: Close the active application

- Close the currently running Microsoft Edge application.

## Review

In this exercise, you cleaned up your subscription by removing the resource groups used in this lab.