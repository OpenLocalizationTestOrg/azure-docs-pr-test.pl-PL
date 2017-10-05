---
title: "Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak włączyć diagnostyki usługi w chmurze przy użyciu programu PowerShell"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 8dd9724981860c9cd4ccc443cc2bfdc465811e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="b3859-103">Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3859-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="b3859-104">Można zebrać danych diagnostycznych, takich jak dzienniki aplikacji z usługą w chmurze przy użyciu rozszerzenia diagnostyki Azure itp. liczniki wydajności.</span><span class="sxs-lookup"><span data-stu-id="b3859-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using the Azure Diagnostics extension.</span></span> <span data-ttu-id="b3859-105">W tym artykule opisano sposób włączania rozszerzenia diagnostyki Azure dla usługi w chmurze przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3859-105">This article describes how to enable the Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="b3859-106">Zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) wymagań wstępnych wymagane dla tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="b3859-106">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="b3859-107">Włączanie rozszerzenia diagnostyki w ramach wdrażania usługi Cloud Service</span><span class="sxs-lookup"><span data-stu-id="b3859-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="b3859-108">Takie podejście stosuje się do typu ciągłej integracji scenariuszy, w którym można włączyć rozszerzenia diagnostyki w ramach wdrażania usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b3859-108">This approach is applicable to continuous integration type of scenarios, where the diagnostics extension can be enabled as part of deploying the cloud service.</span></span> <span data-ttu-id="b3859-109">Podczas tworzenia nowego wdrożenia usługi w chmurze można włączyć rozszerzenia diagnostyki przez przekazywanie *ExtensionConfiguration* parametr [AzureDeployment nowy](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b3859-109">When creating a new Cloud Service deployment you can enable the diagnostics extension by passing in the *ExtensionConfiguration* parameter to the [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="b3859-110">*ExtensionConfiguration* parametr pobiera tablicę diagnostyki konfiguracje, które mogą być tworzone przy użyciu [AzureServiceDiagnosticsExtensionConfig nowy](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b3859-110">The *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using the [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="b3859-111">W poniższym przykładzie pokazano, jak można włączyć diagnostyki sieć Web i proces roboczy, o konfiguracji diagnostyki innej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b3859-111">The following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

<span data-ttu-id="b3859-112">Jeśli plik konfiguracji diagnostyki Określa `StorageAccount` element nazwy konta magazynu, a następnie `New-AzureServiceDiagnosticsExtensionConfig` polecenia cmdlet będą automatycznie używać tego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="b3859-112">If the diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="b3859-113">Aby to zrobić konta magazynu musi być w tej samej subskrypcji co wdrażania usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b3859-113">For this to work, the storage account needs to be in the same subscription as the Cloud Service being deployed.</span></span>

<span data-ttu-id="b3859-114">Z Azure SDK 2.6 ponownego udostępnienia plików konfiguracji rozszerzeń, które są generowane przez program MSBuild publikowanie danych wyjściowych będzie zawierać nazwy konta magazynu, które są oparte na ciąg konfiguracji diagnostyki określony w pliku konfiguracji usługi (cscfg).</span><span class="sxs-lookup"><span data-stu-id="b3859-114">From Azure SDK 2.6 onward the extension configuration files generated by the MSBuild publish target output will include the storage account name based on the diagnostics configuration string specified in the service configuration file (.cscfg).</span></span> <span data-ttu-id="b3859-115">Poniższy skrypt pokazuje, jak przeanalizować pliki konfiguracji rozszerzenia z danych wyjściowych publikowania i skonfigurować rozszerzenia diagnostyki dla każdej roli, podczas wdrażania usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b3859-115">The script below shows you how to parse the Extension configuration files from the publish target output and configure diagnostics extension for each role when deploying the cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find the Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find the RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

<span data-ttu-id="b3859-116">Visual Studio Online używa podejście podobne zautomatyzowanych wdrożeń usług w chmurze z rozszerzeniem diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="b3859-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with the diagnostics extension.</span></span> <span data-ttu-id="b3859-117">Zobacz [AzureCloudDeployment.ps1 publikowania](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) pełny przykład.</span><span class="sxs-lookup"><span data-stu-id="b3859-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="b3859-118">Jeśli nie `StorageAccount` został określony w konfiguracji diagnostyki muszą podawać *StorageAccountName* parametr w poleceniu cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b3859-118">If no `StorageAccount` was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="b3859-119">Jeśli *StorageAccountName* określony parametr, a następnie polecenia cmdlet będzie zawsze używać konta magazynu, które jest określone w parametrze i nie ten, który jest określony w pliku konfiguracji diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="b3859-119">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="b3859-120">Jeśli konto magazynu diagnostyki jest w innej subskrypcji z usługi w chmurze, a następnie jawnie przekazywane w *StorageAccountName* i *StorageAccountKey* parametry polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b3859-120">If the diagnostics storage account is in a different subscription from the Cloud Service, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="b3859-121">*StorageAccountKey* parametru nie jest wymagana, gdy konto magazynu diagnostyki jest w tej samej subskrypcji, ponieważ polecenie cmdlet można automatycznie zapytania i ustaw wartość klucza podczas włączania rozszerzenia diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="b3859-121">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="b3859-122">Jednak jeśli konto magazynu diagnostyki jest w innej subskrypcji, to polecenie cmdlet nie może być może automatycznie pobrać klucz i musisz jawnie określić klucz przy użyciu *StorageAccountKey* parametru.</span><span class="sxs-lookup"><span data-stu-id="b3859-122">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="b3859-123">Włączanie rozszerzenia diagnostyki w istniejącej usłudze Cloud Service</span><span class="sxs-lookup"><span data-stu-id="b3859-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="b3859-124">Można użyć [AzureServiceDiagnosticsExtension zestaw](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) polecenia cmdlet, aby włączyć lub zaktualizować diagnostyki konfiguracji usługi w chmurze, która jest już uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="b3859-124">You can use the [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to enable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="b3859-125">Pobieranie bieżącej konfiguracji rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="b3859-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="b3859-126">Użyj [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) polecenia cmdlet, aby uzyskać bieżącą konfigurację diagnostyki w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b3859-126">Use the [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to get the current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="b3859-127">Usuwanie rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="b3859-127">Remove diagnostics extension</span></span>
<span data-ttu-id="b3859-128">Aby wyłączyć funkcję diagnostyki na usługi w chmurze można użyć [AzureServiceDiagnosticsExtension Usuń](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b3859-128">To turn off diagnostics on a cloud service you can use the [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="b3859-129">Jeśli włączono rozszerzenie diagnostyki za pomocą *AzureServiceDiagnosticsExtension zestaw* lub *AzureServiceDiagnosticsExtensionConfig nowy* bez *roli*parametr, a następnie można usunąć przy użyciu rozszerzenia *AzureServiceDiagnosticsExtension Usuń* bez *roli* parametru.</span><span class="sxs-lookup"><span data-stu-id="b3859-129">If you enabled the diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or the *New-AzureServiceDiagnosticsExtensionConfig* without the *Role* parameter then you can remove the extension using *Remove-AzureServiceDiagnosticsExtension* without the *Role* parameter.</span></span> <span data-ttu-id="b3859-130">Jeśli *roli* parametr został użyty podczas włączania rozszerzenia, a następnie go należy użyć podczas usuwania rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="b3859-130">If the *Role* parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="b3859-131">Aby usunąć rozszerzenie diagnostyki z pojedynczej roli:</span><span class="sxs-lookup"><span data-stu-id="b3859-131">To remove the diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="b3859-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b3859-132">Next Steps</span></span>
* <span data-ttu-id="b3859-133">Aby uzyskać dodatkowe wskazówki na temat używania diagnostyki Azure i innych technik rozwiązywania problemów, zobacz [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="b3859-133">For additional guidance on using Azure diagnostics and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="b3859-134">[Schemat konfiguracji diagnostyki](https://msdn.microsoft.com/library/azure/dn782207.aspx) opisano różne opcje konfiguracji xml rozszerzenia diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="b3859-134">The [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains the various xml configurations options for the diagnostics extension.</span></span>
* <span data-ttu-id="b3859-135">Aby dowiedzieć się, jak włączyć rozszerzenie diagnostyki dla maszyn wirtualnych, zobacz [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Resource Manager Azure](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="b3859-135">To learn how to enable the diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
