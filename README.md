---
services: virtual-machines
platforms: dotnet
author: xiaopingpingcn
---

# Mange Azure Virtual Machines using REST API

This sample demonstrates a how to mange Azure Virtual Machines using REST API.
 To operate Azure Virtual Machines, using the Azure PowerShell isn't the only way. We also can use management service API to achieve this target. We can use GET/POST/DELETE requests to operate an Azure Virtual Machine.
##Running this sample
To run this sample you will need:

- Visual Studio 2015
- An Azure subscription 

###Step 1:  Clone or download this repository.
From your shell or command line:

`git clone https://github.com/Azure-Samples/virtual-machines-dotnet-rest-api-manage.git`

###Step 2: Create a cloud service.
The cloud service to which you want to deploy the Virtual Machine.If you already have a cloud service in your Azure, you can skip to the next step. If you create a cloud service, you can create it by using the Management Portal, by using Create Cloud Service, or by using the New-AzureService cmdlet. 

###Step3 : Create and Upload a Management Certificate for Azure.
You make sure that the Create Virtual Machine Deployment request that is made to the management service is secure.Secure requests to the management service can be authenticated by using management certificates over SSL. To use a management certificate, it must be uploaded to Azure.

###Step 4: Open the AddVirtualMachine.xml, fill your own value to this xml file.
This xml file shows the message we need when create a Virtual Machine.
###Step 5: Run the Sample.

1.	Press Ctrl+F5 to show the console application.
2.	Fill your own Subscription Id, Cloud Service name, Certificate Thumbprint.
3.	Choose the operation, and check it on your Azure portal.


##More Information
- [Create Virtual Machine Deployment](https://msdn.microsoft.com/library/azure/jj157194.aspx)
- [Get Deployment](https://msdn.microsoft.com/en-us/library/azure/ee460804.aspx)
- [Delete Deployment](https://msdn.microsoft.com/en-us/library/azure/ee460815.aspx)
