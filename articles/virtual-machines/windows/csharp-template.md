---
title: "aaaDeploy a maszyny Wirtualnej przy użyciu języka C# i szablonu usługi Resource Manager | Dokumentacja firmy Microsoft"
description: "Poznaj toouse toohow C# i Menedżer zasobów toodeploy szablonu maszyny Wirtualnej platformy Azure."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a>Wdróż maszynę wirtualną platformy Azure przy użyciu języka C# i szablonu usługi Resource Manager
W tym artykule opisano sposób toodeploy szablonu usługi Azure Resource Manager przy użyciu języka C#. tworzony szablon Hello wdraża jednej maszyny wirtualnej z systemem Windows Server w nowej sieci wirtualnej z pojedynczą podsiecią.

Aby uzyskać szczegółowy opis hello zasobu maszyny wirtualnej, zobacz [maszyn wirtualnych w szablonie usługi Azure Resource Manager](template-description.md). Aby uzyskać więcej informacji o wszystkich zasobów hello w szablonie, zobacz [Przewodnik po szablonie usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).

Trwa około 10 minut toodo następujące kroki.

## <a name="create-a-visual-studio-project"></a>Tworzenie projektu programu Visual Studio

W tym kroku należy się upewnić się, że jest zainstalowany program Visual Studio i tworzenia szablonu hello toodeploy aplikacji konsoli.

1. Jeśli nie jest jeszcze zainstalować [programu Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Wybierz **tworzenia klasycznych aplikacji .NET** na hello obciążeń strony, a następnie kliknij przycisk **zainstalować**. W podsumowaniu hello, można stwierdzić, że **narzędzi programistycznych platformy .NET Framework 4 4.6** jest automatycznie wybrana. Jeśli zainstalowano program Visual Studio można dodać hello obciążenia .NET przy użyciu hello uruchamiania usługi Visual Studio.
2. W programie Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.
3. W **szablony** > **Visual C#**, wybierz pozycję **aplikacji konsoli (.NET Framework)**, wprowadź *myDotnetProject* hello nazwy Witaj projektu, zaznacz hello lokalizację projektu hello, a następnie kliknij przycisk **OK**.

## <a name="install-hello-packages"></a>Instalowanie pakietów hello

Pakiety NuGet są hello najprostszy sposób tooinstall hello biblioteki muszą toofinish następujące kroki. tooget hello bibliotek, które należy w programie Visual Studio, wykonaj następujące kroki:

1. Kliknij przycisk **narzędzia** > **Menedżera pakietów Nuget**, a następnie kliknij przycisk **Konsola Menedżera pakietów**.
2. W konsoli hello, wpisz następujące polecenia:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a>Tworzenie plików hello

W tym kroku utworzysz plik szablonu, który wdraża hello zasobów i pliku parametrów, który dostarcza szablonu toohello wartości parametru. Możesz również utworzyć pliku autoryzacji, który jest używane tooperform operacji usługi Azure Resource Manager.

### <a name="create-hello-template-file"></a>Utwórz plik szablonu hello

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *myDotnetProject* > **Dodaj** > **nowy element**, a następnie wybierz **pliku tekstowego** w *elementów Visual C#*. Nazwa pliku hello *CreateVMTemplate.json*, a następnie kliknij przycisk **Dodaj**.
2. Dodaj ten plik toohello kodu JSON, który został utworzony:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. Zapisz plik CreateVMTemplate.json hello.

### <a name="create-hello-parameters-file"></a>Tworzenie pliku parametrów hello

toospecify wartości parametrów zasobów hello, które są zdefiniowane w szablonie hello, Utwórz plik parametrów zawierający wartości hello.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *myDotnetProject* > **Dodaj** > **nowy element**, a następnie wybierz **pliku tekstowego** w *elementów Visual C#*. Nazwa pliku hello *parameters.JSON następującym kodem*, a następnie kliknij przycisk **Dodaj**.
2. Dodaj ten plik toohello kodu JSON, który został utworzony:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. Zapisz hello pliku parameters.JSON następującym kodem.

### <a name="create-hello-authorization-file"></a>Tworzenie pliku autoryzacji hello

Zanim będzie można wdrożyć szablon, upewnij się, że masz dostęp do tooan [nazwy głównej usługi Active Directory](../../resource-group-authenticate-service-principal.md). Z hello nazwy głównej usługi należy uzyskać token dla uwierzytelniania żądania tooAzure Menedżera zasobów. Należy również zarejestrować identyfikator aplikacji hello, klucz uwierzytelniania hello i identyfikator dzierżawcy hello potrzebne w pliku autoryzacji hello.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *myDotnetProject* > **Dodaj** > **nowy element**, a następnie wybierz **pliku tekstowego** w *elementów Visual C#*. Nazwa pliku hello *azureauth.properties*, a następnie kliknij przycisk **Dodaj**.
2. Dodaj te właściwości autoryzacji:

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    Zastąp  **&lt;identyfikator subskrypcji&gt;**  z identyfikatorem subskrypcji  **&lt;identyfikator aplikacji&gt;**  z hello aplikacji usługi Active Directory Identyfikator,  **&lt;klucz uwierzytelniania&gt;**  kluczem aplikacji hello i  **&lt;identyfikator dzierżawcy&gt;**  z dzierżawcą hello Identyfikator.

3. Zapisz plik azureauth.properties hello.
4. Ustaw zmienną środowiskową systemu Windows o nazwie AZURE_AUTH_LOCATION z hello Pełna ścieżka tooauthorization pliku, który został utworzony, na przykład Witaj następujące polecenia można użyć programu PowerShell:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a>Utwórz powitania klienta zarządzania

1. Otwórz plik Program.cs hello hello projektu, który został utworzony, a następnie dodaj te instrukcje toohello istniejące instrukcje using u góry pliku hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. Klient zarządzania hello toocreate, Dodaj ten kod toohello metody Main:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

wartości toospecify dla aplikacji hello, Dodaj metodę Main toohello kodu:

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Szablon Hello i parametry są wdrażane z konta magazynu na platformie Azure. W tym kroku utwórz konto hello i przekazać pliki hello. 

toocreate hello konta, Dodaj ten kod toohello metody Main:

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a>Wdrażanie szablonu hello

Wdrażanie szablonu hello i parametrów z hello konta magazynu, który został utworzony. 

Szablon hello toodeploy, Dodaj ten kod toohello metody Main:

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a>Usuwanie zasobów hello

Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne. Nie trzeba toodelete każdego zasobu niezależnie od grupy zasobów. Usuń grupę zasobów hello i wszystkie jej zasoby są automatycznie usuwane. 

zasób hello toodelete grupy, Dodaj ten kod toohello metody Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Należy trwa około pięciu minut, zanim ta toorun aplikacji konsoli całkowicie od początku toofinish. 

1. toorun hello aplikacji konsoli, kliknij przycisk **Start**.

2. Przed naciśnięciem przycisku **Enter** toostart usuwanie zasobów, można wykonać kilka minut tooverify hello tworzenia zasobów hello w hello portalu Azure. Kliknij przycisk hello wdrożenia toosee informacje o stanie wdrożenia hello.

## <a name="next-steps"></a>Następne kroki
* Jeśli wystąpiły problemy z wdrażaniem hello, następnym krokiem będzie toolook w [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](../../resource-manager-common-deployment-errors.md).
* Dowiedz się, jak toodeploy maszyny wirtualnej i jej zasobach pomocnicze, przeglądając [wdrażanie Azure maszyny wirtualnej przy użyciu języka C#](csharp.md).
