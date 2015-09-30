---
services: virtual-machines
platforms: dotnet
author: xiaopingpingcn
---

# Mange Azure Virtual Machines using REST API

This sample demonstrates a how to mange Azure Virtual Machines using REST API.
 To operate Azure Virtual Machines, using the Azure PowerShell isn't the only way. We also can use management service API to achieve this target. We can use GET/POST/DELETE requests to operate an Azure Virtual Machine.

###Step 1:  Create a Console app named CSAzureControlVM.
###Step 2: Add an xml file called AddVirtualMachine.xml.
The following code shows the message we need when create a Virtual Machine.
```XML
<Deployment xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
  <!--Replace this property to avaliable value-->
  <Name>name-of-deployment</Name>
  <DeploymentSlot>Production</DeploymentSlot>
    <!--Replace this property to avaliable value-->
  <Label>identifier-of-deployment</Label>
  <RoleList>
    <Role>
      <!--Replace this property to avaliable value-->
      <RoleName>name-of-the-virtual-machine</RoleName>
      <RoleType>PersistentVMRole</RoleType>
      <ConfigurationSets>
        <ConfigurationSet i:type="WindowsProvisioningConfigurationSet">
          <ConfigurationSetType>WindowsProvisioningConfiguration</ConfigurationSetType>
          <!--Replace this property to avaliable value-->
          <ComputerName>name-of-computer</ComputerName>
          <!--Replace this property to avaliable value-->
          <AdminPassword>administrator-password</AdminPassword>
          <EnableAutomaticUpdates>true</EnableAutomaticUpdates>
          <!--Replace this property to avaliable value-->
          <AdminUsername>name-of-administrator-account</AdminUsername>
        </ConfigurationSet>
        <ConfigurationSet i:type="NetworkConfigurationSet">
          <ConfigurationSetType>NetworkConfiguration</ConfigurationSetType>
          <InputEndpoints>
            <InputEndpoint>
              <LocalPort>5976</LocalPort>
              <Name>PowerShell</Name>
              <Port>5976</Port>
              <Protocol>tcp</Protocol>
              <EnableDirectServerReturn>false</EnableDirectServerReturn>
            </InputEndpoint>
          </InputEndpoints>
        </ConfigurationSet>
      </ConfigurationSets>
      <DataVirtualHardDisks/>
      <OSVirtualHardDisk>
        <!--Replace this property to avaliable value-->
        <DiskName>name-of-disk</DiskName>
        <!--Replace these two properties to avaliable value-->
        <MediaLink>https://portalvhdswslbyw3kdv748.blob.core.windows.net/vhds/vhdtest</MediaLink>       
        <SourceImageName>a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20150916-en.us-127GB.vhd</SourceImageName>
      </OSVirtualHardDisk>
    </Role>
  </RoleList>
</Deployment>
```
###Step 3: Add the operation method to the program.cs file.
1.How to create an Azure Virtual Machine Deployment via RESTAPI.

This operation creates a deployment and then creates a Virtual Machine in the deployment based on the specified configuration.

Some code snippets:
```C#
static HttpWebRequest AddVirtualMachine()
{
    //For more details about how to add virtual machine please refer to:
    //http://msdn.microsoft.com/en-us/library/windowsazure/jj157194.aspx
    HttpWebRequest request = (HttpWebRequest)HttpWebRequest.Create(new Uri("https://management.core.windows.net/" + SubscriptionID
    + "/services/hostedservices/" + ServiceName + "/deployments" ));

    request.Method = "POST";
    request.ClientCertificates.Add(Certificate);
    request.ContentType = "application/xml";
    request.Headers.Add("x-ms-version", "2015-04-01");

    // Add body to the request
    XmlDocument xmlDoc = new XmlDocument();
    xmlDoc.Load("..\\..\\AddVirtualMachine.xml");

    Stream requestStream = request.GetRequestStream();
    StreamWriter streamWriter = new StreamWriter(requestStream, System.Text.UTF8Encoding.UTF8);
    xmlDoc.Save(streamWriter);

    streamWriter.Close();
    requestStream.Close();

    return request;

}
```
2.How to get an Azure Virtual Machine Deployment via RESTAPI.

This operation returns configuration information, status, and system properties for a deployment.

3.How to delete an Azure Virtual Machine Deployment via RESTAPI

This operation deletes the specified deployment.

###Step 4: Please follow these demonstration steps below.

1.	Open the AddVirtualMachine.xml, fill your own value to this xml file.
2.	Press Ctrl+F5 to show the console application.
3.	Fill your own Subscription Id, Service name, Certificate Thumbprint.
4.	Choose the operation, and check it on your Azure portal.


###Step5:More Information
[Create Virtual Machine Deployment](https://msdn.microsoft.com/library/azure/jj157194.aspx)
