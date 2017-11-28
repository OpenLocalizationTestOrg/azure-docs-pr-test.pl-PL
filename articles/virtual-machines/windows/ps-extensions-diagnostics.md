---
title: aaaUse diagnostyki tooenable programu Azure PowerShell na maszynie Wirtualnej z systemem Windows | Dokumentacja firmy Microsoft
services: virtual-machines-windows
documentationcenter: 
description: "Dowiedz się, jak toouse PowerShell tooenable diagnostyki Azure na maszynie wirtualnej z systemem Windows"
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="22dbb-103">Użyj diagnostyki Azure tooenable programu PowerShell na maszynie wirtualnej z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="22dbb-103">Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="22dbb-104">Diagnostyka Azure jest możliwość hello w ramach platformy Azure, która umożliwia hello zbieranie danych diagnostycznych o wdrożonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22dbb-104">Azure Diagnostics is hello capability within Azure that enables hello collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="22dbb-105">Można użyć hello diagnostyki rozszerzenia toocollect danych diagnostycznych, takich jak dzienniki aplikacji i liczników wydajności z maszyny wirtualnej platformy Azure (VM) z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="22dbb-105">You can use hello diagnostics extension toocollect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="22dbb-106">W tym artykule opisano, jak tooenable środowiska Windows PowerShell toouse hello rozszerzenia diagnostyki dla maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22dbb-106">This article describes how toouse Windows PowerShell tooenable hello diagnostics extension for a VM.</span></span> <span data-ttu-id="22dbb-107">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) hello wymagania wstępne wymagane dla tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="22dbb-107">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a><span data-ttu-id="22dbb-108">Włączanie rozszerzenia diagnostyki hello, jeśli używasz modelu wdrażania usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="22dbb-108">Enable hello diagnostics extension if you use hello Resource Manager deployment model</span></span>
<span data-ttu-id="22dbb-109">Można włączyć rozszerzenia diagnostyki hello, podczas tworzenia maszyny Wirtualnej systemu Windows za pośrednictwem modelu wdrażania usługi Azure Resource Manager hello przez dodanie szablonu usługi Resource Manager toohello hello rozszerzenia konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="22dbb-109">You can enable hello diagnostics extension while you create a Windows VM through hello Azure Resource Manager deployment model by adding hello extension configuration toohello Resource Manager template.</span></span> <span data-ttu-id="22dbb-110">Zobacz [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Azure Resource Manager hello](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="22dbb-110">See [Create a Windows virtual machine with monitoring and diagnostics by using hello Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="22dbb-111">rozszerzenie diagnostyki hello tooenable na istniejącej maszynie Wirtualnej, który został utworzony za pośrednictwem modelu wdrażania usługi Resource Manager hello, można użyć hello [AzureRMVMDiagnosticsExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) polecenia cmdlet programu PowerShell, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="22dbb-111">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="22dbb-112">*$diagnosticsconfig_path* jest hello ścieżka toohello pliku, który zawiera hello diagnostyki konfiguracji w formacie XML, zgodnie z opisem w hello [próbki](#sample-diagnostics-configuration) poniżej.</span><span class="sxs-lookup"><span data-stu-id="22dbb-112">*$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML, as described in hello [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="22dbb-113">Jeśli plik konfiguracji diagnostyki hello Określa **StorageAccount** element nazwy konta magazynu, następnie hello *AzureRMVMDiagnosticsExtension zestaw* skryptu automatycznie ustawi hello rozszerzenie toosend danych diagnostycznych toothat konto magazynu diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="22dbb-113">If hello diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then hello *Set-AzureRMVMDiagnosticsExtension* script will automatically set hello diagnostics extension toosend diagnostic data toothat storage account.</span></span> <span data-ttu-id="22dbb-114">Dla tego toowork hello konto magazynu na potrzeby toobe w hello tej samej subskrypcji, ponieważ hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22dbb-114">For this toowork, hello storage account needs toobe in hello same subscription as hello VM.</span></span>

<span data-ttu-id="22dbb-115">Jeśli nie **StorageAccount** została określona w konfiguracji diagnostyki hello, wówczas należy toopass w hello *StorageAccountName* polecenia cmdlet toohello parametru.</span><span class="sxs-lookup"><span data-stu-id="22dbb-115">If no **StorageAccount** was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="22dbb-116">Jeśli hello *StorageAccountName* określony parametr, a następnie hello cmdlet zawsze używać konta magazynu hello określonego w parametrze hello i nie Witaj, który jest określony w pliku konfiguracyjnym hello diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="22dbb-116">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="22dbb-117">Jeśli konto magazynu jest w innej subskrypcji z hello maszyny Wirtualnej, a następnie należy tooexplicitly diagnostyki hello przekazywanie hello *StorageAccountName* i *StorageAccountKey* polecenia cmdlet toohello parametrów.</span><span class="sxs-lookup"><span data-stu-id="22dbb-117">If hello diagnostics storage account is in a different subscription from hello VM, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="22dbb-118">Witaj *StorageAccountKey* parametru nie jest wymagana, gdy diagnostyki hello konto magazynu znajduje się w tej samej subskrypcji, Witaj, hello polecenia cmdlet można automatycznie zapytania i ustaw wartość klucza hello podczas włączania rozszerzenia diagnostyki hello.</span><span class="sxs-lookup"><span data-stu-id="22dbb-118">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="22dbb-119">Jednak jeśli hello konto magazynu diagnostyki jest w innej subskrypcji, polecenia cmdlet hello może nie być możliwe tooget hello klucza automatycznie i potrzebujesz tooexplicitly określ klucz hello za pośrednictwem hello *StorageAccountKey* parametr.</span><span class="sxs-lookup"><span data-stu-id="22dbb-119">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="22dbb-120">Po włączeniu rozszerzenia diagnostyki hello na maszynie Wirtualnej można uzyskać hello bieżące ustawienia za pomocą hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22dbb-120">Once hello diagnostics extension is enabled on a VM, you can get hello current settings by using hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="22dbb-121">Witaj polecenie cmdlet zwraca *PublicSettings*, zawierającą hello konfiguracji diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="22dbb-121">hello cmdlet returns *PublicSettings*, which contains hello diagnostics configuration.</span></span> <span data-ttu-id="22dbb-122">Istnieją dwa rodzaje konfiguracja jest obsługiwana, WadCfg i xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="22dbb-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="22dbb-123">WadCfg jest konfiguracji JSON, a xmlCfg jest konfiguracji XML w formacie zakodowanym w formacie Base64.</span><span class="sxs-lookup"><span data-stu-id="22dbb-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="22dbb-124">tooread hello XML, należy toodecode go.</span><span class="sxs-lookup"><span data-stu-id="22dbb-124">tooread hello XML, you need toodecode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="22dbb-125">Witaj [AzureRMVmDiagnosticsExtension Usuń](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) polecenia cmdlet mogą być używane tooremove hello diagnostyki rozszerzenia hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22dbb-125">hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used tooremove hello diagnostics extension from hello VM.</span></span>  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a><span data-ttu-id="22dbb-126">Włączanie rozszerzenia diagnostyki hello, jeśli używasz hello klasycznego modelu wdrażania</span><span class="sxs-lookup"><span data-stu-id="22dbb-126">Enable hello diagnostics extension if you use hello classic deployment model</span></span>
<span data-ttu-id="22dbb-127">Można użyć hello [AzureVMDiagnosticsExtension zestaw](/powershell/module/azure/set-azurevmdiagnosticsextension) tooenable polecenia cmdlet dla diagnostyki rozszerzenia na maszynie Wirtualnej, który utworzono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="22dbb-127">You can use hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable a diagnostics extension on a VM that you create through hello classic deployment model.</span></span> <span data-ttu-id="22dbb-128">Witaj poniższy przykład przedstawia sposób toocreate nowej maszyny Wirtualnej za pośrednictwem hello klasycznego modelu wdrażania z rozszerzeniem diagnostyki hello włączone.</span><span class="sxs-lookup"><span data-stu-id="22dbb-128">hello following example shows how toocreate a new VM through hello classic deployment model with hello diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="22dbb-129">rozszerzenie diagnostyki hello tooenable na istniejącej maszyny Wirtualnej, który został utworzony za pomocą hello klasycznego modelu wdrażania, pierwszy hello użyj [Get AzureVM](/powershell/module/azure/get-azurevm) konfiguracji maszyny Wirtualnej hello tooget polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22dbb-129">tooenable hello diagnostics extension on an existing VM that was created through hello classic deployment model, first use hello [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM configuration.</span></span> <span data-ttu-id="22dbb-130">Następnie zaktualizuj rozszerzenie diagnostyki hello tooinclude w konfiguracji maszyny Wirtualnej hello przy użyciu hello [AzureVMDiagnosticsExtension zestaw](/powershell/module/azure/set-azurevmdiagnosticsextension) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22dbb-130">Then update hello VM configuration tooinclude hello diagnostics extension by using hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="22dbb-131">Na koniec stosowania hello zaktualizowane toohello konfiguracji maszyny Wirtualnej za pomocą [AzureVM aktualizacji](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="22dbb-131">Finally, apply hello updated configuration toohello VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="22dbb-132">Przykładowa konfiguracja diagnostyki</span><span class="sxs-lookup"><span data-stu-id="22dbb-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="22dbb-133">Witaj, następujące XML może być używane w przypadku hello diagnostyki publicznego konfiguracji hello powyżej skryptów.</span><span class="sxs-lookup"><span data-stu-id="22dbb-133">hello following XML can be used for hello diagnostics public configuration with hello above scripts.</span></span> <span data-ttu-id="22dbb-134">Ta przykładowa konfiguracja zostanie transfer różnych wydajności liczniki toohello konto magazynu diagnostyki, wraz z błędami z aplikacji hello, zabezpieczeń i system kanałów w dzienniku zdarzeń systemu Windows hello oraz wszelkie błędy z hello diagnostyki Dzienniki infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="22dbb-134">This sample configuration will transfer various performance counters toohello diagnostics storage account, along with errors from hello application, security, and system channels in hello Windows event logs and any errors from hello diagnostics infrastructure logs.</span></span>

<span data-ttu-id="22dbb-135">Konfiguracja Hello musi toobe tooinclude zaktualizowane hello następujące:</span><span class="sxs-lookup"><span data-stu-id="22dbb-135">hello configuration needs toobe updated tooinclude hello following:</span></span>

* <span data-ttu-id="22dbb-136">Witaj *resourceID* atrybutu hello **metryki** element wymaga toobe aktualizacji o identyfikatorze zasobu hello na powitania maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="22dbb-136">hello *resourceID* attribute of hello **Metrics** element needs toobe updated with hello resource ID for hello VM.</span></span>
  
  * <span data-ttu-id="22dbb-137">Witaj identyfikator można utworzyć przy użyciu następującego wzorca hello zasobu: "/ subscriptions / {*identyfikator subskrypcji dla subskrypcji hello z hello maszyny Wirtualnej*} /resourceGroups/ {*hello nazwę dla hello wirtualna*} / providers/Microsoft.Compute/virtualMachines/ {*hello nazwę maszyny Wirtualnej*} ".</span><span class="sxs-lookup"><span data-stu-id="22dbb-137">hello resource ID can be constructed by using hello following pattern: "/subscriptions/{*subscription ID for hello subscription with hello VM*}/resourceGroups/{*hello resourcegroup name for hello VM*}/providers/Microsoft.Compute/virtualMachines/{*hello VM Name*}".</span></span>
  * <span data-ttu-id="22dbb-138">Na przykład, jeśli hello jest identyfikator subskrypcji dla subskrypcji hello którym hello maszyna wirtualna jest uruchomiona **11111111-1111-1111-1111-111111111111**, hello Nazwa grupy zasobów dla grupy zasobów hello jest **MyResourceGroup**, i hello Nazwa maszyny Wirtualnej jest **MyWindowsVM**, następnie hello wartość *resourceID* będzie:</span><span class="sxs-lookup"><span data-stu-id="22dbb-138">For example, if hello subscription ID for hello subscription where hello VM is running is **11111111-1111-1111-1111-111111111111**, hello resource group name for hello resource group is **MyResourceGroup**, and hello VM Name is **MyWindowsVM**, then hello value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="22dbb-139">Aby uzyskać więcej informacji na to, jak metryki są generowane na podstawie hello liczniki wydajności i metryki konfiguracji, zobacz [diagnostyki Azure metryki tabeli w magazynie](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="22dbb-139">For more information on how metrics are generated based on hello performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="22dbb-140">Witaj **StorageAccount** toobe zaktualizowany o nazwie konto magazynu diagnostyki hello hello wymaga elementu.</span><span class="sxs-lookup"><span data-stu-id="22dbb-140">hello **StorageAccount** element needs toobe updated with hello name of hello diagnostics storage account.</span></span>
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for hello VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a><span data-ttu-id="22dbb-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22dbb-141">Next steps</span></span>
* <span data-ttu-id="22dbb-142">Aby uzyskać dodatkowe wskazówki na temat używania możliwości diagnostyki Azure hello i innych technik tootroubleshoot problemów, zobacz [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="22dbb-142">For additional guidance on using hello Azure Diagnostics capability and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="22dbb-143">[Schemat konfiguracji diagnostyki](https://msdn.microsoft.com/library/azure/mt634524.aspx) opisano różne konfiguracje XML opcje rozszerzenia diagnostyki hello hello.</span><span class="sxs-lookup"><span data-stu-id="22dbb-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains hello various XML configurations options for hello diagnostics extension.</span></span>

