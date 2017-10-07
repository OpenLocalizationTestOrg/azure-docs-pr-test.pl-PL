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
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Użyj diagnostyki Azure tooenable programu PowerShell na maszynie wirtualnej z systemem Windows
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Diagnostyka Azure jest możliwość hello w ramach platformy Azure, która umożliwia hello zbieranie danych diagnostycznych o wdrożonej aplikacji. Można użyć hello diagnostyki rozszerzenia toocollect danych diagnostycznych, takich jak dzienniki aplikacji i liczników wydajności z maszyny wirtualnej platformy Azure (VM) z systemem Windows. W tym artykule opisano, jak tooenable środowiska Windows PowerShell toouse hello rozszerzenia diagnostyki dla maszyny Wirtualnej. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) hello wymagania wstępne wymagane dla tego artykułu.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Włączanie rozszerzenia diagnostyki hello, jeśli używasz modelu wdrażania usługi Resource Manager hello
Można włączyć rozszerzenia diagnostyki hello, podczas tworzenia maszyny Wirtualnej systemu Windows za pośrednictwem modelu wdrażania usługi Azure Resource Manager hello przez dodanie szablonu usługi Resource Manager toohello hello rozszerzenia konfiguracji. Zobacz [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Azure Resource Manager hello](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

rozszerzenie diagnostyki hello tooenable na istniejącej maszynie Wirtualnej, który został utworzony za pośrednictwem modelu wdrażania usługi Resource Manager hello, można użyć hello [AzureRMVMDiagnosticsExtension zestaw](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) polecenia cmdlet programu PowerShell, jak pokazano poniżej.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* jest hello ścieżka toohello pliku, który zawiera hello diagnostyki konfiguracji w formacie XML, zgodnie z opisem w hello [próbki](#sample-diagnostics-configuration) poniżej.  

Jeśli plik konfiguracji diagnostyki hello Określa **StorageAccount** element nazwy konta magazynu, następnie hello *AzureRMVMDiagnosticsExtension zestaw* skryptu automatycznie ustawi hello rozszerzenie toosend danych diagnostycznych toothat konto magazynu diagnostyki. Dla tego toowork hello konto magazynu na potrzeby toobe w hello tej samej subskrypcji, ponieważ hello maszyny Wirtualnej.

Jeśli nie **StorageAccount** została określona w konfiguracji diagnostyki hello, wówczas należy toopass w hello *StorageAccountName* polecenia cmdlet toohello parametru. Jeśli hello *StorageAccountName* określony parametr, a następnie hello cmdlet zawsze używać konta magazynu hello określonego w parametrze hello i nie Witaj, który jest określony w pliku konfiguracyjnym hello diagnostyki.

Jeśli konto magazynu jest w innej subskrypcji z hello maszyny Wirtualnej, a następnie należy tooexplicitly diagnostyki hello przekazywanie hello *StorageAccountName* i *StorageAccountKey* polecenia cmdlet toohello parametrów. Witaj *StorageAccountKey* parametru nie jest wymagana, gdy diagnostyki hello konto magazynu znajduje się w tej samej subskrypcji, Witaj, hello polecenia cmdlet można automatycznie zapytania i ustaw wartość klucza hello podczas włączania rozszerzenia diagnostyki hello. Jednak jeśli hello konto magazynu diagnostyki jest w innej subskrypcji, polecenia cmdlet hello może nie być możliwe tooget hello klucza automatycznie i potrzebujesz tooexplicitly określ klucz hello za pośrednictwem hello *StorageAccountKey* parametr.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

Po włączeniu rozszerzenia diagnostyki hello na maszynie Wirtualnej można uzyskać hello bieżące ustawienia za pomocą hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) polecenia cmdlet.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Witaj polecenie cmdlet zwraca *PublicSettings*, zawierającą hello konfiguracji diagnostyki. Istnieją dwa rodzaje konfiguracja jest obsługiwana, WadCfg i xmlCfg. WadCfg jest konfiguracji JSON, a xmlCfg jest konfiguracji XML w formacie zakodowanym w formacie Base64. tooread hello XML, należy toodecode go.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Witaj [AzureRMVmDiagnosticsExtension Usuń](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) polecenia cmdlet mogą być używane tooremove hello diagnostyki rozszerzenia hello maszyny Wirtualnej.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Włączanie rozszerzenia diagnostyki hello, jeśli używasz hello klasycznego modelu wdrażania
Można użyć hello [AzureVMDiagnosticsExtension zestaw](/powershell/module/azure/set-azurevmdiagnosticsextension) tooenable polecenia cmdlet dla diagnostyki rozszerzenia na maszynie Wirtualnej, który utworzono przy użyciu hello klasycznego modelu wdrażania. Witaj poniższy przykład przedstawia sposób toocreate nowej maszyny Wirtualnej za pośrednictwem hello klasycznego modelu wdrażania z rozszerzeniem diagnostyki hello włączone.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

rozszerzenie diagnostyki hello tooenable na istniejącej maszyny Wirtualnej, który został utworzony za pomocą hello klasycznego modelu wdrażania, pierwszy hello użyj [Get AzureVM](/powershell/module/azure/get-azurevm) konfiguracji maszyny Wirtualnej hello tooget polecenia cmdlet. Następnie zaktualizuj rozszerzenie diagnostyki hello tooinclude w konfiguracji maszyny Wirtualnej hello przy użyciu hello [AzureVMDiagnosticsExtension zestaw](/powershell/module/azure/set-azurevmdiagnosticsextension) polecenia cmdlet. Na koniec stosowania hello zaktualizowane toohello konfiguracji maszyny Wirtualnej za pomocą [AzureVM aktualizacji](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>Przykładowa konfiguracja diagnostyki
Witaj, następujące XML może być używane w przypadku hello diagnostyki publicznego konfiguracji hello powyżej skryptów. Ta przykładowa konfiguracja zostanie transfer różnych wydajności liczniki toohello konto magazynu diagnostyki, wraz z błędami z aplikacji hello, zabezpieczeń i system kanałów w dzienniku zdarzeń systemu Windows hello oraz wszelkie błędy z hello diagnostyki Dzienniki infrastruktury.

Konfiguracja Hello musi toobe tooinclude zaktualizowane hello następujące:

* Witaj *resourceID* atrybutu hello **metryki** element wymaga toobe aktualizacji o identyfikatorze zasobu hello na powitania maszyny Wirtualnej.
  
  * Witaj identyfikator można utworzyć przy użyciu następującego wzorca hello zasobu: "/ subscriptions / {*identyfikator subskrypcji dla subskrypcji hello z hello maszyny Wirtualnej*} /resourceGroups/ {*hello nazwę dla hello wirtualna*} / providers/Microsoft.Compute/virtualMachines/ {*hello nazwę maszyny Wirtualnej*} ".
  * Na przykład, jeśli hello jest identyfikator subskrypcji dla subskrypcji hello którym hello maszyna wirtualna jest uruchomiona **11111111-1111-1111-1111-111111111111**, hello Nazwa grupy zasobów dla grupy zasobów hello jest **MyResourceGroup**, i hello Nazwa maszyny Wirtualnej jest **MyWindowsVM**, następnie hello wartość *resourceID* będzie:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Aby uzyskać więcej informacji na to, jak metryki są generowane na podstawie hello liczniki wydajności i metryki konfiguracji, zobacz [diagnostyki Azure metryki tabeli w magazynie](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* Witaj **StorageAccount** toobe zaktualizowany o nazwie konto magazynu diagnostyki hello hello wymaga elementu.
  
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

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać dodatkowe wskazówki na temat używania możliwości diagnostyki Azure hello i innych technik tootroubleshoot problemów, zobacz [Włączanie diagnostyki w usług Azure Cloud Services i maszyn wirtualnych](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [Schemat konfiguracji diagnostyki](https://msdn.microsoft.com/library/azure/mt634524.aspx) opisano różne konfiguracje XML opcje rozszerzenia diagnostyki hello hello.

