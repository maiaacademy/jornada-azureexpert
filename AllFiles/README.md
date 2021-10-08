## Azure Expert - Mod 07 - Aula 08 
## Deploy the On-premises environment on Hyper-V (60 minutes)

## Requirements

1. You will need Owner or Contributor permissions for an Azure subscription to use in the lab.

2. Your subscription must have sufficient unused quota to deploy the VMs used in this lab. To check your quota:

    - Log in to the [Azure portal](https://portal.azure.com), select **All services** then **Subscriptions**. Select your subscription, then choose **Usage + quotas**.
  
    - From the **Select a provider** drop-down, select **Microsoft.Compute**.
  
    - From the **All service quotas** drop down, select **Standard DSv3 Family vCPUs**, **Standard FSv2 Family vCPUs** and **Total Regional vCPUs**.
  
    - From the **All locations** drop down, select the location where you will deploy the lab.
  
    - From the last drop-down, select **Show all**.
  
    - Check that the selected quotas have sufficient unused capacity:
  
        - Standard DSv3 Family vCPUs: **at least 8 vCPUs**.
  
        - Standard FSv2 Family vCPUs: **at least 6 vCPUs**.

        - Total Regional vCPUs: **at least 14 vCPUs**.

    > **Note:** If you are using an Azure Pass subscription, you may not meet the vCPU quotas above. In this case, you can still complete the lab.

## Deploy the on-premises environment

1. Deploy the template **SmartHotelHost.json** to a new resource group. This template deploys a virtual machine running nested Hyper-V, with 4 nested VMs. This comprises the 'on-premises' environment which you will assess and migrate during this lab.

    You can deploy the template by selecting the 'Deploy to Azure' button below. You will need to create a new resource group **RG-TAE-SmartHotel-Onpremises**. You will also need to select a location **East US 2 or other** close to you to deploy the template to. Then choose **Review + create** followed by **Create**. 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fcloudworkshop.blob.core.windows.net%2Fline-of-business-application-migration%2Fsept-2020%2FSmartHotelHost.json" target="_blank">![Button to deploy the SmartHotelHost template to Azure.](/Mod07-AllFiles/Images/deploy-to-azure.png)</a>

    > **Note:** The template will take around 6-7 minutes to deploy. Once template deployment is complete, several additional scripts are executed to bootstrap the lab environment. **Allow at least 1 hour from the start of template deployment for the scripts to run.**

### Verify the on-premises environment

1. Navigate to the **SmartHotelHost** VM that was deployed by the template in the previous step.

2. Make a note of the public IP address.

3. Open a browser tab and navigate to **http://\<SmartHotelHostIP-Address\>**. You should see the SmartHotel application, which is running on nested VMs within Hyper-V on the SmartHotelHost. (The application doesn't do much: you can refresh the page to see the list of guests or select 'CheckIn' or 'CheckOut' to toggle their status.)

    ![Browser screenshot showing the SmartHotel application.](/Mod07-AllFiles/Images/smarthotel.png)

    > **Note:** If the SmartHotel application is not shown, wait 10 minutes and try again. It takes **at least 1 hour** from the start of template deployment. You can also check the CPU, network and disk activity levels for the SmartHotelHost VM in the Azure portal, to see if the provisioning is still active.

4. Connect RDP session in the **SmartHotelHost**  with credentials, username: **demouser**, and password: **demo!pass123** and Virtual Machines username: **administrator** and password same.

You should follow all steps provided *before* performing the Hands-on lab.

## Solution architecture

The SmartHotel application comprises 4 VMs hosted in Hyper-V:

- **Database tier** Hosted on the smarthotelSQL1 VM, which is running Windows Server 2016 and SQL Server 2017.

- **Application tier** Hosted on the smarthotelweb2 VM, which is running Windows Server 2012 R2.

- **Web tier** Hosted on the smarthotelweb1 VM, which is running Windows Server 2012 R2.

- **Web proxy** Hosted on the  UbuntuWAF VM, which is running Nginx on Ubuntu 18.04 LTS.

For simplicity, there is no redundancy in any of the tiers.

![A slide shows the on-premises SmartHotel application architecture.](/Mod07-AllFiles/Images/overview.png)

## Azure Expert - Mod 07 - Aula 09
# Deploy the VMs environment on Azure (30 minutes)

1. Deploy the template **RG-TAE-PartsUnlimited** to a new resource group. This template deploy a virtual machine with Application and Database.

2. You can deploy the template by selecting the 'Deploy to Azure' button below. You will need to create a new resource group **RG-TAE-PartsUnlimited**. You will also need to select a location **Central US** close to you to deploy the template to. Then choose **Review + create** followed by **Create**.

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmaiaacademy%2FAppService-Migration-Assistant%2Fmain%2Ftemplate.json)

     > **Note:** The template will take around 6-7 minutes to deploy. Once template deployment is complete, several additional scripts are executed to bootstrap the lab environment. **Allow at least 1 hour from the start of template deployment for the scripts to run.**

1. In the Azure portal, select the Virtual machines icon, after selecting More services. You should see a single VM named **webvm** listed.

2. Make a note of the public IP address.

3. Open a browser tab and navigate to **http://webvm-IP-Address>**. You should see the Parts Unlimited application, which is running on VM.

   ![Screenshot of the Application on Azure VM](/Mod07-AllFiles/Images/partsunlimited.png)

1. Continue in the **Treinamento Azure Expert**.
