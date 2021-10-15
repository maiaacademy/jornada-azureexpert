# Jornada Azure Expert

Participe da **Jornada Azure Expert de 11 a 18 de outubro**, evento ONLINE e gratuito: https://guilhermemaia.com/inscricoes-jae-out21

Hands-on Lab

# Projeto Implantação 100% prática de uma Aplicação em Alta disponibilidade e Escalável no Azure

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmaiaacademy%2Fjornada-azureexpert%2Fmain%2FAllFiles%2FTemplates%2Ftemplate.json)

![A slide shows the Parts Unlimited](/AllFiles/Images/partsunlimited.png)

1. Deploy the template **Template.json** to a new resource group. This template deploy a virtual machine with Application and Database.

2. You can deploy the template by selecting the 'Deploy to Azure' button below. You will need to create a new resource group **RG-PU**. You will also need to select a location **East US** close to you to deploy the template to. Then choose **Review + create** followed by **Create**. 

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
