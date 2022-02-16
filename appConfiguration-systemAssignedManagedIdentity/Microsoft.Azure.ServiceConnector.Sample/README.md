# Connect Azure WebApp with Azure App Configuration using system assigned managed indentity

## Prerequisite
- An Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/en-in/free/)
- Azure CLI. You can use it in [CloudShell](https://shell.azure.com) or [install it locally](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
- Git.
- **Optional** [Visual Studio](https://visualstudio.microsoft.com/downloads/) or [VSCode](https://code.visualstudio.com/download)


## How to run the sample
1. Setup Azure resources
   1. Create Azure WebApp.
   ```
   # login to Azure in CLI, no need if running in Cloudshell.
   az login
   # switch to a subscription where you have Subscription Contributor role.
   az account set -s <myTestSubsId>
   # create resource group
   az group create -n <myResourceGroupName> -l eastus
   # create appservice plan
   az appservice plan create -g <myResourceGroupName> -n <myPlanName> --is-linux --sku B1
   # create webapp
   az webapp create -g <myResourceGroupName> -n <myWebAppName> --runtime "DOTNETCORE|3.1" --plan <myPlanName>
   ```
   1. Create Azure App Configuration Store, import test configuration file [./sampleconfigs.json](./sampleconfigs.json).
   ```
   # create app configuration store
   az appconfig create -g <myResourceGroupName> -n <myAppConfigStoreName> --sku Free -l eastus
   # import test config into app configuration store. If you're using Cloudshell, [upload](https://docs.microsoft.com/en-us/azure/cloud-shell/persisting-shell-storage#upload-files) [sampleconfigs.json](./sampleconfigs.json) before run the command.
   az appconfig kv import -n <myAppConfigStoreName> --source file --format json --path ./sampleconfigs.json --separator : --yes
   ```
   

1. Create connection between the WebApp and App Configuration via Service Connector. WebApp will connect to App Config with system assigned Managed Identity.
   ```
   az webapp connection create appconfig -g <myResourceGroupName> -n <myWebAppName> --app-config <myAppConfigStoreName> --tg <myResourceGroupName> --connection <myConnectioName> --system-identity
   ```
   `system-identity` is authentication type, other supported authentication type: user assigned managed identity; secret; service principle. Pls refer to [more samples]().
   Behind the scene, Service Connector service do the connection configuration for you. Such as, set WebApp Setting `AZURE_APPCONFIG_ENDPOINT`, 
   so the application could consume it to connect to the webapp at [codeline](link);
   enabled system Managed Identity on the WebApp and grant App Configuration Data Reader role to it, so the application code could [use system Managed Identity auth via `DefaultTokenCredential`](code link) to authenticated to the App Configuration.
   Learn more about the detail from [Service Connector Internal](https://docs.microsoft.com/en-us/azure/service-connector/concept-service-connector-internals).

1. Build and Deploy App to Azure. Use command line or any approach you're familiar with to build code and publish it to the WebApp.
   1. Clone the sample repo.
   ```
   git clone xxx
   ```
   1. cd to the folder ``, do build
   ```
   cd webapp-serviceconnector-samples\appConfiguration-systemAssignedManagedIdentity\Microsoft.Azure.ServiceConnector.Sample
   dotnet publish .\Microsoft.Azure.ServiceConnector.Sample.csproj -c Release -o output
   ```
   3. Deploy to the Azure Web App.
   Recommend to use Visual Studio or VSCode.
      - Visual Studio. Open the sample solution in Visual Studio, right click on the project name, click `Publish`, follow the wizard to publish to Azure. 
        More detail at [instruction](https://docs.microsoft.com/en-us/azure/app-service/tutorial-dotnetcore-sqldb-app?toc=%2Faspnet%2Fcore%2Ftoc.json&bc=%2Faspnet%2Fcore%2Fbreadcrumb%2Ftoc.json&view=aspnetcore-6.0&tabs=azure-portal%2Cvisualstudio-deploy%2Cdeploy-instructions-azcli%2Cazure-portal-logs%2Cazure-portal-resources#4---deploy-to-the-app-service).
      - VSCode. use VSCode. Install extension [Azure App Service extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azureappservice). 
        Open the sample folder with VSCode, right click on the project, click "Deploy to WebApp`, follow the wizard to publish to Azure. 
        More detail at [instruction](https://docs.microsoft.com/en-us/azure/app-service/tutorial-dotnetcore-sqldb-app?toc=%2Faspnet%2Fcore%2Ftoc.json&bc=%2Faspnet%2Fcore%2Fbreadcrumb%2Ftoc.json&view=aspnetcore-6.0&tabs=azure-portal%2Cvisualstudio-deploy%2Cdeploy-instructions-azcli%2Cazure-portal-logs%2Cazure-portal-resources#4---deploy-to-the-app-service).
      - Azure CLI.
        ```
        az webapp deployment source config-local-git -g <myResourceGroupName> -n <myWebAppName>
        az webapp deployment list-publishing-credentials -g <myResourceGroupName> -n <myWebAppName>  --query "{Username:publishingUserName, Password:publishingPassword}"
        git remote add azure https://<myWebAppName>.scm.azurewebsites.net/<myWebAppName>.git
        # push local main branch to remote master branch, the command will prompt for username and password, which are in output of above list-publishing-credentials command
        git push azure main:master
        ```
1. Validate the connection is working. Nagivate to your WebApp https://<myWebAppName>.azurewebsites.net/ from browser, you can see the site is up, displaying hello message.

## Test (optional)
1. Update value of key `SampleApplication:Settings:Messages` in the App Configuration Store.
```
az appconfig kv set -n <myAppConfigStoreName> --key SampleApplication:Settings:Messages --value hello --yes
```
1. Navigate to your WebApp on Azure ``, refresh the page, you'll see the message displayed is `hello`.

## Cleanup
Delete the resource group with the WebApp and App Configuration Store in it.
```
az group delete -n <myResourceGroupName> --yes
```

## Useful reference
There're more Service Connector samples to connect Azure WebApp, Azure Spring Cloud to other Azure services, check them out!
- xxxxx
- Spring cloud sample repo
Learn more about [Service Connector](https://aka.ms/scdoc).

## License
[link]()