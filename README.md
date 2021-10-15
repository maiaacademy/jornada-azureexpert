# Jornada Azure Expert

Participe da **Jornada Azure Expert de 11 a 18 de outubro**, evento ONLINE e gratuito: https://guilhermemaia.com/inscricoes-jae-out21

Hands-on Lab

# Projeto - Implantação 100% prática de uma Aplicação em Alta disponibilidade e Escalável no Azure

## Exercise #01 - Deploy Application (30 minutes)
## Parts Unlimited Online Auto Parts

![A slide shows the Parts Unlimited](/AllFiles/Images/partsunlimited.png)

## Application Archicture

![A slide shows the Parts Unlimited Architecture](/AllFiles/Images/architecture-partsunlimited.png)

1. Deploy the template **Template.json** to a new resource group. This template deploy a virtual machine with Application and Database.

2. You can deploy the template by selecting the 'Deploy to Azure' button below. You will need to create a new resource group **RG-PU-App**. You will also need to select a location **East US** close to you to deploy the template to. Then choose **Review + create** followed by **Create**. 

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmaiaacademy%2Fjornada-azureexpert%2Fmain%2FAllFiles%2FTemplates%2Ftemplate.json)

     > **Note:** The template will take around 10-15 minutes to deploy. Once template deployment is complete, several additional scripts are executed to bootstrap the lab environment. **Allow at least 15 hour from the start of template deployment for the scripts to run.**

1. In the Azure portal, select the Virtual machines icon, after selecting More services. You should see a single VM named **webVM** listed.

1. Select the **webVM** item in the list. The details for the VM appear.

1. On the upper details toolbar, select Connect, and then select RDP from the dropdown list.

1. On the Connect pane, select Download RDP File.

1. Open the **webVM.rdp file**. You'll be prompted for the VM's security credentials in the Windows Security dialog box. Select Use a different account. Copy and paste the username and password from step 1 into the dialog box, and select OK.

1. On the remote desktop, open Internet Explorer, and go to http://localhost. Confirm that the Parts Unlimited website is successfully running. This site is hosted in IIS in the virtual machine, and connects to an Azure SQL database. Over the course of this exercise, you'll perform a migration assessment on this site and then migrate it to App Service.

1. On the remote VM's desktop, double-click the icon to open the Azure App Service Migration Assistant. The user interface then lists the Migration Assistant's steps with the first step highlighted, **Choose a site.** In the main area, the Migration Assistant informs that it found one site to assess.

1. Select the **Default Web Site** option.

1. After a moment, the assessment report step should finish. You should see that all **13 assessments were successful** with no warnings or errors.

1. Select Next to display the **Login to Azure** step. Here you'll use a special code to associate this assessment on your server to your Azure account.

1. In the **Migration Assistant**, you'll see the Login to Azure page with a device code and a button. Copy the device code to the clipboard.

1. Go to the device login service. You should see the **Enter code webpage** on your local computer.

1. On your local computer, select Next. Sign in by using the same account that you used to sign in to Azure.

1. Back in the **Migration Assistant** running in the remote VM, the step Azure Options is displayed. Here you'll enter details about the target App Service instance to which you'll move your app.

1. Use the following table to make your selections:

    | Field | Value |
    | --- | ---|
    | Resource Group | Select the **Use exiting option** |
    | Destination Site Name | Enter a valid name for the destination site |
    | App Service Plan | Select the **Use exiting option**
    | Azure Migrate Project | **Leave this field empty**

1. **Select Migrate.** The Migration in Progress screen displays the current status of the migration.

1. After the migration is complete, you'll continue to the **Migration Results** step.

1. Open the Azure portal on a new tab on your local computer. Select **App Service** from the home page. From the list of deployed services, select the one that matches the name that you created earlier. This will display the settings for your new App Service account.

1. Select the **Browse** button at the top of the overview page to browse to your migrated site running in Azure.

# Exercise #02 - Deploy Azure Front Door (30 minutes)

1. From the Azure portal, select **+Create a resource**, then search for and select **Front Door**. Select **Create**. 

2. Complete the **Basics** tab of the **Create a Front Door** blade using the following inputs, then select **Next: Configuration >**:

    - **Resource group**: Use existing / **RG-PU-Web**
    - **Location**: Automatically assigned based on the region of **RG-PU-Web**.

3. Select the **plus** icon on the **Frontend/domains** box to set the host name of Front Door. In the **Add a frontend host** pane, enter the following values, then select **Add**:

    - **Host name**: Enter a unique name with the prefix of `puwebafd####`.
    - **Session affinity**: Disabled
    - **Web application firewall**: Disabled

4. Select the **plus** button on the **Backend pools** box to begin adding endpoints to the backend pool. On the **Add a backend pool** pane, enter the following value, then select the **Add a backend** link.

    - **Name**: `PUPool`
    - **Health Probes - Protocol**: HTTPS

5. On the **Add a backend** pane, enter the following values (leave others as defaults), then select **Add**:

    - **Backend host type**: Public IP Address
    - **Backend host name**: ContosoWebLBPrimaryIP
    - **Backend host header**: Paste in the DNS name for the **ContosoWebLBPrimaryIP** Public IP Address (in the **RG-PU-App** resource group).

7. Select **Add** to create the backend pool.

8. Select the **plus** button on the **Routing rules** box. On the **Add a rule** pane, enter the following values (leave others as defaults), then select **Add**.

    - **Name**: `PURule`
    - **Accepted protocol**: HTTPs only
    - **Backend pool**: PUPool
    - **Forwarding protocol**: HTTPs Only

9. Select **Review + Create**. Once validation has completed, select **Create** to provision the Front Door service.

10. Navigate to the Azure Front Door resource. Select the **Frontend host** URL of Azure Front Door, the Policy Connect web application will load.

    > **Note:** If you get a "Our services aren't available right now" error (or a 404-type error) accessing the web application, then continue on with the lab and come back to this later. Sometime this can take a ~10 minutes for the routing rules to publish before it's "live".

## Exercise #03 - Autoscale Application (30 minutes)

Configure and test autoscaling of the Azure Web app

1. Open the Azure portal on a new tab on your local computer. Select **App Service** from the home page. From the list of deployed services, select the one that matches the name that you created earlier.

1. On the blade displaying the production slot of the web app, in the **Settings** section, click **Scale out (App Service plan)**.

1. Click **Custom autoscale**.

    >**Note**: You also have the option of scaling the web app manually.

1. Leave the default option **Scale based on a metric** selected and click **+ Add a rule**

1. On the **Scale rule** blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- |--- |
    | Metric source | **Current resource** |
    | Time aggregation | **Maximum** |
    | Metric namespace | **App Service plans standard metrics** |
    | Metric name | **CPU Percentage** |
    | Operator | **Greater than** |
    | Metric threshold to trigger scale action | **10** |
    | Duration (in minutes) | **1** |
    | Time grain statistic | **Maximum** |
    | Operation | **Increase count by** |
    | Instance count | **1** |
    | Cool down (minutes) | **5** |

    >**Note**: Obviously these values do not represent a realistic configuration, since their purpose is to trigger autoscaling as soon as possible, without extended wait period.

1. Click **Add** and, back on the App Service plan scaling blade, specify the following settings (leave others with their default values):

    | Setting | Value |
    | --- |--- |
    | Instance limits Minimum | **1** |
    | Instance limits Maximum | **2** |
    | Instance limits Default | **1** |

1. Click **Save**.

1. In the Azure portal, open the **Azure Cloud Shell** by clicking on the icon in the top right of the Azure Portal.

1. If prompted to select either **Bash** or **PowerShell**, select **PowerShell**.

1. From the Cloud Shell pane, run the following to start and infinite loop that sends the HTTP requests to the web app:

   ```powershell
   while ($true) { Invoke-WebRequest -Uri URLAPPSERVICE }
   ```

1. Minimize the Cloud Shell pane (but do not close it) and, on the web app blade, in the **Monitoring** section, click **Process explorer**.

    >**Note**: Process explorer facilitates monitoring the number of instances and their resource utilization.

1. Monitor the utilization and the number of instances for a few minutes.

    >**Note**: You may need to **Refresh** the page.

1. Once you notice that the number of instances has increased to 2, reopen the Cloud Shell pane and terminate the script by pressing **Ctrl+C**.

1. Close the Cloud Shell pane.
