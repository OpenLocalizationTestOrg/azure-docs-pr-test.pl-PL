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
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="945b7-103">Wdróż maszynę wirtualną platformy Azure przy użyciu języka C# i szablonu usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="945b7-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="945b7-104">W tym artykule opisano sposób toodeploy szablonu usługi Azure Resource Manager przy użyciu języka C#.</span><span class="sxs-lookup"><span data-stu-id="945b7-104">This article shows you how toodeploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="945b7-105">tworzony szablon Hello wdraża jednej maszyny wirtualnej z systemem Windows Server w nowej sieci wirtualnej z pojedynczą podsiecią.</span><span class="sxs-lookup"><span data-stu-id="945b7-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="945b7-106">Aby uzyskać szczegółowy opis hello zasobu maszyny wirtualnej, zobacz [maszyn wirtualnych w szablonie usługi Azure Resource Manager](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="945b7-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="945b7-107">Aby uzyskać więcej informacji o wszystkich zasobów hello w szablonie, zobacz [Przewodnik po szablonie usługi Azure Resource Manager](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="945b7-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="945b7-108">Trwa około 10 minut toodo następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="945b7-108">It takes about 10 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="945b7-109">Tworzenie projektu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="945b7-109">Create a Visual Studio project</span></span>

<span data-ttu-id="945b7-110">W tym kroku należy się upewnić się, że jest zainstalowany program Visual Studio i tworzenia szablonu hello toodeploy aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="945b7-110">In this step, you make sure that Visual Studio is installed and you create a console application used toodeploy hello template.</span></span>

1. <span data-ttu-id="945b7-111">Jeśli nie jest jeszcze zainstalować [programu Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="945b7-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="945b7-112">Wybierz **tworzenia klasycznych aplikacji .NET** na hello obciążeń strony, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="945b7-112">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="945b7-113">W podsumowaniu hello, można stwierdzić, że **narzędzi programistycznych platformy .NET Framework 4 4.6** jest automatycznie wybrana.</span><span class="sxs-lookup"><span data-stu-id="945b7-113">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="945b7-114">Jeśli zainstalowano program Visual Studio można dodać hello obciążenia .NET przy użyciu hello uruchamiania usługi Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="945b7-114">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="945b7-115">W programie Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="945b7-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="945b7-116">W **szablony** > **Visual C#**, wybierz pozycję **aplikacji konsoli (.NET Framework)**, wprowadź *myDotnetProject* hello nazwy Witaj projektu, zaznacz hello lokalizację projektu hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="945b7-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-packages"></a><span data-ttu-id="945b7-117">Instalowanie pakietów hello</span><span class="sxs-lookup"><span data-stu-id="945b7-117">Install hello packages</span></span>

<span data-ttu-id="945b7-118">Pakiety NuGet są hello najprostszy sposób tooinstall hello biblioteki muszą toofinish następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="945b7-118">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="945b7-119">tooget hello bibliotek, które należy w programie Visual Studio, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="945b7-119">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="945b7-120">Kliknij przycisk **narzędzia** > **Menedżera pakietów Nuget**, a następnie kliknij przycisk **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="945b7-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="945b7-121">W konsoli hello, wpisz następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="945b7-121">Type these commands in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a><span data-ttu-id="945b7-122">Tworzenie plików hello</span><span class="sxs-lookup"><span data-stu-id="945b7-122">Create hello files</span></span>

<span data-ttu-id="945b7-123">W tym kroku utworzysz plik szablonu, który wdraża hello zasobów i pliku parametrów, który dostarcza szablonu toohello wartości parametru.</span><span class="sxs-lookup"><span data-stu-id="945b7-123">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="945b7-124">Możesz również utworzyć pliku autoryzacji, który jest używane tooperform operacji usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="945b7-124">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

### <a name="create-hello-template-file"></a><span data-ttu-id="945b7-125">Utwórz plik szablonu hello</span><span class="sxs-lookup"><span data-stu-id="945b7-125">Create hello template file</span></span>

1. <span data-ttu-id="945b7-126">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *myDotnetProject* > **Dodaj** > **nowy element**, a następnie wybierz **pliku tekstowego** w *elementów Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="945b7-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="945b7-127">Nazwa pliku hello *CreateVMTemplate.json*, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="945b7-127">Name hello file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="945b7-128">Dodaj ten plik toohello kodu JSON, który został utworzony:</span><span class="sxs-lookup"><span data-stu-id="945b7-128">Add this JSON code toohello file that you created:</span></span>

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

3. <span data-ttu-id="945b7-129">Zapisz plik CreateVMTemplate.json hello.</span><span class="sxs-lookup"><span data-stu-id="945b7-129">Save hello CreateVMTemplate.json file.</span></span>

### <a name="create-hello-parameters-file"></a><span data-ttu-id="945b7-130">Tworzenie pliku parametrów hello</span><span class="sxs-lookup"><span data-stu-id="945b7-130">Create hello parameters file</span></span>

<span data-ttu-id="945b7-131">toospecify wartości parametrów zasobów hello, które są zdefiniowane w szablonie hello, Utwórz plik parametrów zawierający wartości hello.</span><span class="sxs-lookup"><span data-stu-id="945b7-131">toospecify values for hello resource parameters that are defined in hello template, you create a parameters file that contains hello values.</span></span>

1. <span data-ttu-id="945b7-132">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *myDotnetProject* > **Dodaj** > **nowy element**, a następnie wybierz **pliku tekstowego** w *elementów Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="945b7-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="945b7-133">Nazwa pliku hello *parameters.JSON następującym kodem*, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="945b7-133">Name hello file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="945b7-134">Dodaj ten plik toohello kodu JSON, który został utworzony:</span><span class="sxs-lookup"><span data-stu-id="945b7-134">Add this JSON code toohello file that you created:</span></span>

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

4. <span data-ttu-id="945b7-135">Zapisz hello pliku parameters.JSON następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="945b7-135">Save hello Parameters.json file.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="945b7-136">Tworzenie pliku autoryzacji hello</span><span class="sxs-lookup"><span data-stu-id="945b7-136">Create hello authorization file</span></span>

<span data-ttu-id="945b7-137">Zanim będzie można wdrożyć szablon, upewnij się, że masz dostęp do tooan [nazwy głównej usługi Active Directory](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="945b7-137">Before you can deploy a template, make sure that you have access tooan [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="945b7-138">Z hello nazwy głównej usługi należy uzyskać token dla uwierzytelniania żądania tooAzure Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="945b7-138">From hello service principal, you acquire a token for authenticating requests tooAzure Resource Manager.</span></span> <span data-ttu-id="945b7-139">Należy również zarejestrować identyfikator aplikacji hello, klucz uwierzytelniania hello i identyfikator dzierżawcy hello potrzebne w pliku autoryzacji hello.</span><span class="sxs-lookup"><span data-stu-id="945b7-139">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in hello authorization file.</span></span>

1. <span data-ttu-id="945b7-140">W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy *myDotnetProject* > **Dodaj** > **nowy element**, a następnie wybierz **pliku tekstowego** w *elementów Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="945b7-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="945b7-141">Nazwa pliku hello *azureauth.properties*, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="945b7-141">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="945b7-142">Dodaj te właściwości autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="945b7-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="945b7-143">Zastąp  **&lt;identyfikator subskrypcji&gt;**  z identyfikatorem subskrypcji  **&lt;identyfikator aplikacji&gt;**  z hello aplikacji usługi Active Directory Identyfikator,  **&lt;klucz uwierzytelniania&gt;**  kluczem aplikacji hello i  **&lt;identyfikator dzierżawcy&gt;**  z dzierżawcą hello Identyfikator.</span><span class="sxs-lookup"><span data-stu-id="945b7-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="945b7-144">Zapisz plik azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="945b7-144">Save hello azureauth.properties file.</span></span>
4. <span data-ttu-id="945b7-145">Ustaw zmienną środowiskową systemu Windows o nazwie AZURE_AUTH_LOCATION z hello Pełna ścieżka tooauthorization pliku, który został utworzony, na przykład Witaj następujące polecenia można użyć programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="945b7-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created, for example hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a><span data-ttu-id="945b7-146">Utwórz powitania klienta zarządzania</span><span class="sxs-lookup"><span data-stu-id="945b7-146">Create hello management client</span></span>

1. <span data-ttu-id="945b7-147">Otwórz plik Program.cs hello hello projektu, który został utworzony, a następnie dodaj te instrukcje toohello istniejące instrukcje using u góry pliku hello:</span><span class="sxs-lookup"><span data-stu-id="945b7-147">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="945b7-148">Klient zarządzania hello toocreate, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="945b7-148">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="945b7-149">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="945b7-149">Create a resource group</span></span>

<span data-ttu-id="945b7-150">wartości toospecify dla aplikacji hello, Dodaj metodę Main toohello kodu:</span><span class="sxs-lookup"><span data-stu-id="945b7-150">toospecify values for hello application, add code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="945b7-151">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="945b7-151">Create a storage account</span></span>

<span data-ttu-id="945b7-152">Szablon Hello i parametry są wdrażane z konta magazynu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="945b7-152">hello template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="945b7-153">W tym kroku utwórz konto hello i przekazać pliki hello.</span><span class="sxs-lookup"><span data-stu-id="945b7-153">In this step, you create hello account and upload hello files.</span></span> 

<span data-ttu-id="945b7-154">toocreate hello konta, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="945b7-154">toocreate hello account, add this code toohello Main method:</span></span>

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

## <a name="deploy-hello-template"></a><span data-ttu-id="945b7-155">Wdrażanie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="945b7-155">Deploy hello template</span></span>

<span data-ttu-id="945b7-156">Wdrażanie szablonu hello i parametrów z hello konta magazynu, który został utworzony.</span><span class="sxs-lookup"><span data-stu-id="945b7-156">Deploy hello template and parameters from hello storage account that was created.</span></span> 

<span data-ttu-id="945b7-157">Szablon hello toodeploy, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="945b7-157">toodeploy hello template, add this code toohello Main method:</span></span>

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

## <a name="delete-hello-resources"></a><span data-ttu-id="945b7-158">Usuwanie zasobów hello</span><span class="sxs-lookup"><span data-stu-id="945b7-158">Delete hello resources</span></span>

<span data-ttu-id="945b7-159">Naliczane są opłaty za zasoby używane na platformie Azure, dlatego jest zawsze zasobów toodelete dobrym rozwiązaniem, które nie są już potrzebne.</span><span class="sxs-lookup"><span data-stu-id="945b7-159">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="945b7-160">Nie trzeba toodelete każdego zasobu niezależnie od grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="945b7-160">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="945b7-161">Usuń grupę zasobów hello i wszystkie jej zasoby są automatycznie usuwane.</span><span class="sxs-lookup"><span data-stu-id="945b7-161">Delete hello resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="945b7-162">zasób hello toodelete grupy, Dodaj ten kod toohello metody Main:</span><span class="sxs-lookup"><span data-stu-id="945b7-162">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="945b7-163">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="945b7-163">Run hello application</span></span>

<span data-ttu-id="945b7-164">Należy trwa około pięciu minut, zanim ta toorun aplikacji konsoli całkowicie od początku toofinish.</span><span class="sxs-lookup"><span data-stu-id="945b7-164">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="945b7-165">toorun hello aplikacji konsoli, kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="945b7-165">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="945b7-166">Przed naciśnięciem przycisku **Enter** toostart usuwanie zasobów, można wykonać kilka minut tooverify hello tworzenia zasobów hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="945b7-166">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="945b7-167">Kliknij przycisk hello wdrożenia toosee informacje o stanie wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="945b7-167">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="945b7-168">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="945b7-168">Next steps</span></span>
* <span data-ttu-id="945b7-169">Jeśli wystąpiły problemy z wdrażaniem hello, następnym krokiem będzie toolook w [Rozwiąż typowe błędy wdrożenia usługi Azure z usługą Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="945b7-169">If there were issues with hello deployment, a next step would be toolook at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="945b7-170">Dowiedz się, jak toodeploy maszyny wirtualnej i jej zasobach pomocnicze, przeglądając [wdrażanie Azure maszyny wirtualnej przy użyciu języka C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="945b7-170">Learn how toodeploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
