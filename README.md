---
page_type: sample
languages:
- java
- dotnet
- python
products:
- service connector
description: "Sample projects for Service Connector"
urlFragment: "serviceconnector-samples"
---

# ServiceConnetor-Samples
<!-- 
Guidelines on README format: https://review.docs.microsoft.com/help/onboard/admin/samples/concepts/readme-template?branch=master

Guidance on onboarding samples to docs.microsoft.com/samples: https://review.docs.microsoft.com/help/onboard/admin/samples/process/onboarding?branch=master

Taxonomies for products and languages: https://review.docs.microsoft.com/new-hope/information-architecture/metadata/taxonomies?branch=master
-->

## Overview
[Service Connector](https://docs.microsoft.com/en-us/azure/service-connector/) is an Azure-managed service that helps developers easily connect compute service to target backing services. This service configures the network settings and connection information (for example, generating environment variables) between compute service and target backing service in management plane. Developers just use preferred SDK or library that consumes the connection information to do data plane operations against target backing service.

Service Connector supports Azure WebApp, Azure Spring Cloud as source of connection, and over [10+ Azure services](https://docs.microsoft.com/en-us/azure/service-connector/overview#what-services-are-supported-in-service-connector) as target, such as PostgreSQL, MySQL, Storage, Keyvault, ServiceBus, SignalR etc.

This repository contains sample projects for Service Connector. 

## Sample list
Below table shows the list of the samples available in this repository. Folder name is on convention "<source service>-<target service>-<client type>".
| Folder               | Description|
|-------------|-----------------------------|
|[appconfiguration-system-assigned-managed-identity](./webapp-keyvault-java)| Sample of connecting Azure WebApp hosting Java application to Azure Keyvault|
|[appconfiguration-user-assigned-managed-identity](./webapp-keyvault-java)| Sample of connecting Azure WebApp hosting Java application to Azure Keyvault|
|[appconfiguration-access-key](./webapp-signalr-dotnet)| Sample of connecting Azure WebApp hosting DotNet application to Azure SignalR|
|[appconfiguration-systemAssignedManagedIdentity](./webapp-keyvault-java)| Sample of connecting Azure WebApp hosting Java application to Azure Keyvault|
|[appconfiguration-userAssignedManagedIdentity](./webapp-keyvault-java)| Sample of connecting Azure WebApp hosting Java application to Azure Keyvault|
|[appconfiguration-accessKey](./webapp-signalr-dotnet)| Sample of connecting Azure WebApp hosting DotNet application to Azure SignalR|
|[mysqlSignal-systemAssignedManagedIdentity](./webapp-keyvault-java)| Sample of connecting Azure WebApp hosting Java application to Azure Keyvault|
|[mysqlSignal-userAssignedManagedIdentity](./webapp-keyvault-java)| Sample of connecting Azure WebApp hosting Java application to Azure Keyvault|
|[mysqlSignal-accessKey](./webapp-signalr-dotnet)| Sample of connecting Azure WebApp hosting DotNet application to Azure SignalR|
|[mysqlFlexible-systemAssignedManagedIdentity](./webapp-keyvault-java)| Sample of connecting Azure WebApp hosting Java application to Azure Keyvault|
|[mysqlFlexible-userAssignedManagedIdentity](./webapp-keyvault-java)| Sample of connecting Azure WebApp hosting Java application to Azure Keyvault|
|[mysqlFlexible-accessKey](./webapp-signalr-dotnet)| Sample of connecting Azure WebApp hosting DotNet application to Azure SignalR|

| source | target | description |
|-----------------|-----------------|-----------------|
| webapp | keyvalt | test |
| | signalr|  test|
| azure spring cloud | keyvault | test |
| | storage | |

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## License