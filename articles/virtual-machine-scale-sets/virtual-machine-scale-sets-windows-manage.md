---
title: aaaManage maszyn wirtualnych w zestawie skalowania maszyn wirtualnych | Dokumentacja firmy Microsoft
description: "Zarządzanie maszynami wirtualnymi w skali maszyny wirtualnej ustawić za pomocą programu Azure PowerShell."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>Zarządzanie maszynami wirtualnymi w zestawie skalowania maszyn wirtualnych
Używanie zadań hello na maszynach wirtualnych toomanage tego artykułu w zestawie skalowania maszyn wirtualnych.

Większość zadań hello, które obejmują zarządzanie maszyny wirtualnej w zestawie skalowania wymagają, że znasz identyfikator wystąpienia hello hello maszyny, które mają toomanage. Można użyć [Eksploratora zasobów Azure](https://resources.azure.com) toofind hello Identyfikatora wystąpienia zestawu skali maszyny wirtualnej. Można również użyć Eksploratora zasobów tooverify hello stan hello zadań, które należy zakończyć.

Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooyour konta.

## <a name="display-information-about-a-scale-set"></a>Wyświetlanie informacji o zestawie skali
Aby uzyskać informacje ogólne o zestawie skali, który jest także widok wystąpienia hello tooas określonego. Alternatywnie można uzyskać bardziej szczegółowe informacje, takie jak informacje o zasobach hello w zestawie skalowania hello.

Zastąp hello podane wartości z nazwy hello lub grupy zasobów i skali ustawiona, a następnie uruchom polecenie hello:

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

Zwraca podobny do następującego:

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

Zastąp hello podane wartości o nazwie hello grupy i skalę zestawu zasobów. Zastąp  *#*  z identyfikatorem wystąpienia hello hello maszyny wirtualnej chcesz uzyskać tooget informacje, a następnie uruchom go:

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Zwraca wartość inną tak jak ten przykład:

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a>Uruchom maszynę wirtualną w zestawie skalowania
Zastąp hello podane wartości o nazwie hello grupy i skalę zestawu zasobów. Zastąp  *#*  o identyfikatorze hello hello maszyny wirtualnej mają toostart, a następnie uruchom go:

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

W Eksploratorze zasobów, zobaczysz, że stan hello wystąpienia hello jest **systemem**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

Wszystkie maszyny wirtualne hello można uruchomić w skali hello ustawione przez nie za pomocą parametru - InstanceId hello.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>Zatrzymaj maszynę wirtualną w zestawie skalowania
Zastąp hello podane wartości o nazwie hello grupy i skalę zestawu zasobów. Zastąp  *#*  o identyfikatorze hello hello maszyny wirtualnej mają toostop, a następnie uruchom go:

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

W Eksploratorze zasobów, zobaczysz, że stan hello wystąpienia hello jest **alokację**:

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

toostop maszyny wirtualnej i jej deallocate, użyj parametru - StayProvisioned hello. Można zatrzymać wszystkie maszyny wirtualne hello hello ustawione przez nie za pomocą parametru - InstanceId hello.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>Uruchom ponownie maszynę wirtualną w zestawie skalowania
Zastąp hello podane wartości o nazwie hello zestawu skali grupy i hello zasobów. Zastąp  *#*  o identyfikatorze hello hello maszyny wirtualnej mają toorestart, a następnie uruchom go:

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Można ponownie uruchomić wszystkie maszyny wirtualne hello w hello ustawione przez nie za pomocą parametru - InstanceId hello.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>Usuń maszynę wirtualną z zestawu skalowania
Zastąp hello podane wartości o nazwie hello zestawu skali grupy i hello zasobów. Zastąp  *#*  o identyfikatorze hello hello maszyny wirtualnej mają tooremove, a następnie uruchom go:  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

Zestaw skali maszyny wirtualnej hello jednocześnie można usunąć, nie za pomocą parametru - InstanceId hello.

## <a name="change-hello-capacity-of-a-scale-set"></a>Zmień hello pojemność zestawu skalowania
Można dodawać i usuwać maszyny wirtualne, zmieniając pojemności hello hello zestawu. Pobierz zestaw skali hello interesujące toochange, zestaw hello pojemności toowhat ma toobe, a następnie zaktualizuj zestaw skali hello z hello nowego miejsca. W tych poleceń Zastąp hello podane wartości o nazwie hello zestawu skali grupy i hello zasobów.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

Spowoduje usunięcie z hello zestawu skalowania maszyn wirtualnych, hello maszyn wirtualnych o identyfikatorach najwyższy hello są najpierw usunąć.

