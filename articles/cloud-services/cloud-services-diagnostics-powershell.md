---
title: "Diagnostyka aaaEnable w usług Azure Cloud Services przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooenable diagnostyki dla chmury usług przy użyciu programu PowerShell"
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
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="f90df-103">Włącz diagnostykę w usług Azure Cloud Services przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f90df-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="f90df-104">Można zebrać danych diagnostycznych, takich jak dzienniki aplikacji, liczniki wydajności itp. z usługi w chmurze przy użyciu hello rozszerzenia diagnostycznych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f90df-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="f90df-105">W tym artykule opisano, jak tooenable hello rozszerzenia diagnostyki Azure dla usługi w chmurze przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f90df-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="f90df-106">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) hello wymagania wstępne wymagane dla tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="f90df-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="f90df-107">Włączanie rozszerzenia diagnostyki w ramach wdrażania usługi Cloud Service</span><span class="sxs-lookup"><span data-stu-id="f90df-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="f90df-108">Ta metoda jest typ integracji toocontinuous odpowiednich scenariuszach, w którym można włączyć rozszerzenia w ramach wdrażania diagnostyki hello hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f90df-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="f90df-109">Podczas tworzenia nowego wdrożenia usługi w chmurze można włączyć rozszerzenia diagnostyki hello przez przekazywanie hello *ExtensionConfiguration* toohello parametru [AzureDeployment nowy](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f90df-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="f90df-110">Witaj *ExtensionConfiguration* parametr pobiera tablicę diagnostyki konfiguracje, które mogą być tworzone przy użyciu hello [AzureServiceDiagnosticsExtensionConfig nowy](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f90df-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="f90df-111">Witaj poniższy przykład przedstawia sposób można włączyć diagnostyki z sieć Web i proces roboczy, o konfiguracji diagnostyki innej usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f90df-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="f90df-112">Jeśli plik konfiguracji diagnostyki hello Określa `StorageAccount` element nazwy konta magazynu, następnie hello `New-AzureServiceDiagnosticsExtensionConfig` polecenia cmdlet będą automatycznie używać tego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f90df-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="f90df-113">Dla tego toowork hello konto magazynu na potrzeby toobe w hello tej samej subskrypcji, ponieważ hello wdrażania usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f90df-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="f90df-114">Z Azure SDK 2.6 publikowania plików konfiguracji rozszerzenia dalszego hello generowanych przez hello MSBuild danych wyjściowych będzie zawierać nazwy konta magazynu hello oparte na ciąg konfiguracji diagnostyki hello określony w pliku konfiguracji usługi hello (cscfg).</span><span class="sxs-lookup"><span data-stu-id="f90df-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="f90df-115">skrypt Hello poniżej pokazano, jak pliki konfiguracji rozszerzenia hello tooparse z hello publikowanie danych wyjściowych i skonfigurować rozszerzenia diagnostyki dla każdej roli, podczas wdrażania usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f90df-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
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

<span data-ttu-id="f90df-116">Visual Studio Online używa podejście podobne zautomatyzowanych wdrożeń usług w chmurze z rozszerzeniem diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="f90df-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="f90df-117">Zobacz [AzureCloudDeployment.ps1 publikowania](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) pełny przykład.</span><span class="sxs-lookup"><span data-stu-id="f90df-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="f90df-118">Jeśli nie `StorageAccount` została określona w konfiguracji diagnostyki hello, wówczas należy toopass w hello *StorageAccountName* polecenia cmdlet toohello parametru.</span><span class="sxs-lookup"><span data-stu-id="f90df-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="f90df-119">Jeśli hello *StorageAccountName* określony parametr, a następnie hello cmdlet zawsze używać konta magazynu hello określonego w parametrze hello i nie Witaj, który jest określony w pliku konfiguracyjnym hello diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="f90df-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="f90df-120">Jeśli konto magazynu jest w innej subskrypcji z hello usługi w chmurze, a następnie należy tooexplicitly diagnostyki hello przekazywanie hello *StorageAccountName* i *StorageAccountKey* parametrów polecenia cmdlet toohello.</span><span class="sxs-lookup"><span data-stu-id="f90df-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="f90df-121">Witaj *StorageAccountKey* parametru nie jest wymagana, gdy diagnostyki hello konto magazynu znajduje się w tej samej subskrypcji, Witaj, hello polecenia cmdlet można automatycznie zapytania i ustaw wartość klucza hello podczas włączania rozszerzenia diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="f90df-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="f90df-122">Jednak jeśli hello konto magazynu diagnostyki jest w innej subskrypcji, polecenia cmdlet hello może nie być możliwe tooget hello klucza automatycznie i potrzebujesz tooexplicitly określ klucz hello za pośrednictwem hello *StorageAccountKey* parametr.</span><span class="sxs-lookup"><span data-stu-id="f90df-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="f90df-123">Włączanie rozszerzenia diagnostyki w istniejącej usłudze Cloud Service</span><span class="sxs-lookup"><span data-stu-id="f90df-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="f90df-124">Można użyć hello [AzureServiceDiagnosticsExtension zestaw](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) polecenia cmdlet tooenable lub aktualizacji konfiguracji diagnostyki na usługi w chmurze, która jest już uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="f90df-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="f90df-125">Pobieranie bieżącej konfiguracji rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="f90df-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="f90df-126">Użyj hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) polecenia cmdlet tooget hello bieżącej diagnostyki konfiguracji dla usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f90df-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="f90df-127">Usuwanie rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="f90df-127">Remove diagnostics extension</span></span>
<span data-ttu-id="f90df-128">tooturn poza diagnostyki w chmurze usługi, należy użyć hello [AzureServiceDiagnosticsExtension Usuń](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f90df-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="f90df-129">Jeśli włączono rozszerzenie diagnostyki hello przy użyciu *AzureServiceDiagnosticsExtension zestawu* lub hello *AzureServiceDiagnosticsExtensionConfig nowy* bez hello *roli* parametr, a następnie można usunąć za pomocą rozszerzenia hello *AzureServiceDiagnosticsExtension Usuń* bez hello *roli* parametru.</span><span class="sxs-lookup"><span data-stu-id="f90df-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="f90df-130">Jeśli hello *roli* parametr został użyty podczas włączania rozszerzenia hello to należy użyć podczas usuwania hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="f90df-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="f90df-131">rozszerzenie diagnostyki hello tooremove z poszczególnych poszczególnych ról:</span><span class="sxs-lookup"><span data-stu-id="f90df-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="f90df-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f90df-132">Next Steps</span></span>
* <span data-ttu-id="f90df-133">Aby uzyskać dodatkowe wskazówki na temat używania innych technik tootroubleshoot problemów i Diagnostyka Azure, zobacz [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="f90df-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="f90df-134">Witaj [schemat konfiguracji diagnostyki](https://msdn.microsoft.com/library/azure/dn782207.aspx) opisano różne konfiguracje xml opcje rozszerzenia diagnostyki hello hello.</span><span class="sxs-lookup"><span data-stu-id="f90df-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="f90df-135">toolearn tooenable hello diagnostyki rozszerzenia dla maszyn wirtualnych, zobacz temat [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Resource Manager Azure](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="f90df-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
