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
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="381c0-103">Zarządzanie maszynami wirtualnymi w zestawie skalowania maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="381c0-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="381c0-104">Używanie zadań hello na maszynach wirtualnych toomanage tego artykułu w zestawie skalowania maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="381c0-104">Use hello tasks in this article toomanage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="381c0-105">Większość zadań hello, które obejmują zarządzanie maszyny wirtualnej w zestawie skalowania wymagają, że znasz identyfikator wystąpienia hello hello maszyny, które mają toomanage.</span><span class="sxs-lookup"><span data-stu-id="381c0-105">Most of hello tasks that involve managing a virtual machine in a scale set require that you know hello instance ID of hello machine that you want toomanage.</span></span> <span data-ttu-id="381c0-106">Można użyć [Eksploratora zasobów Azure](https://resources.azure.com) toofind hello Identyfikatora wystąpienia zestawu skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="381c0-106">You can use [Azure Resource Explorer](https://resources.azure.com) toofind hello instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="381c0-107">Można również użyć Eksploratora zasobów tooverify hello stan hello zadań, które należy zakończyć.</span><span class="sxs-lookup"><span data-stu-id="381c0-107">You also use Resource Explorer tooverify hello status of hello tasks that you finish.</span></span>

<span data-ttu-id="381c0-108">Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) uzyskać informacji na temat instalowania najnowszej wersji programu Azure PowerShell hello, wybierając subskrypcję i logowanie tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="381c0-108">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="381c0-109">Wyświetlanie informacji o zestawie skali</span><span class="sxs-lookup"><span data-stu-id="381c0-109">Display information about a scale set</span></span>
<span data-ttu-id="381c0-110">Aby uzyskać informacje ogólne o zestawie skali, który jest także widok wystąpienia hello tooas określonego.</span><span class="sxs-lookup"><span data-stu-id="381c0-110">You can get general information about a scale set, which is also referred tooas hello instance view.</span></span> <span data-ttu-id="381c0-111">Alternatywnie można uzyskać bardziej szczegółowe informacje, takie jak informacje o zasobach hello w zestawie skalowania hello.</span><span class="sxs-lookup"><span data-stu-id="381c0-111">Or, you can get more specific information, such as information about hello resources in hello scale set.</span></span>

<span data-ttu-id="381c0-112">Zastąp hello podane wartości z nazwy hello lub grupy zasobów i skali ustawiona, a następnie uruchom polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="381c0-112">Replace hello quoted values with hello name or your resource group and scale set and then run hello command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="381c0-113">Zwraca podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="381c0-113">It returns something like this:</span></span>

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

<span data-ttu-id="381c0-114">Zastąp hello podane wartości o nazwie hello grupy i skalę zestawu zasobów.</span><span class="sxs-lookup"><span data-stu-id="381c0-114">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="381c0-115">Zastąp  *#*  z identyfikatorem wystąpienia hello hello maszyny wirtualnej chcesz uzyskać tooget informacje, a następnie uruchom go:</span><span class="sxs-lookup"><span data-stu-id="381c0-115">Replace *#* with hello instance identifier of hello virtual machine that you want tooget information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="381c0-116">Zwraca wartość inną tak jak ten przykład:</span><span class="sxs-lookup"><span data-stu-id="381c0-116">It returns something like this example:</span></span>

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="381c0-117">Uruchom maszynę wirtualną w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="381c0-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="381c0-118">Zastąp hello podane wartości o nazwie hello grupy i skalę zestawu zasobów.</span><span class="sxs-lookup"><span data-stu-id="381c0-118">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="381c0-119">Zastąp  *#*  o identyfikatorze hello hello maszyny wirtualnej mają toostart, a następnie uruchom go:</span><span class="sxs-lookup"><span data-stu-id="381c0-119">Replace *#* with hello identifier of hello virtual machine that you want toostart and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="381c0-120">W Eksploratorze zasobów, zobaczysz, że stan hello wystąpienia hello jest **systemem**:</span><span class="sxs-lookup"><span data-stu-id="381c0-120">In Resource Explorer, we can see that hello status of hello instance is **running**:</span></span>

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

<span data-ttu-id="381c0-121">Wszystkie maszyny wirtualne hello można uruchomić w skali hello ustawione przez nie za pomocą parametru - InstanceId hello.</span><span class="sxs-lookup"><span data-stu-id="381c0-121">You can start all hello virtual machines in hello scale set by not using hello -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="381c0-122">Zatrzymaj maszynę wirtualną w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="381c0-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="381c0-123">Zastąp hello podane wartości o nazwie hello grupy i skalę zestawu zasobów.</span><span class="sxs-lookup"><span data-stu-id="381c0-123">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="381c0-124">Zastąp  *#*  o identyfikatorze hello hello maszyny wirtualnej mają toostop, a następnie uruchom go:</span><span class="sxs-lookup"><span data-stu-id="381c0-124">Replace *#* with hello identifier of hello virtual machine that you want toostop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="381c0-125">W Eksploratorze zasobów, zobaczysz, że stan hello wystąpienia hello jest **alokację**:</span><span class="sxs-lookup"><span data-stu-id="381c0-125">In Resource Explorer, we can see that hello status of hello instance is **deallocated**:</span></span>

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

<span data-ttu-id="381c0-126">toostop maszyny wirtualnej i jej deallocate, użyj parametru - StayProvisioned hello.</span><span class="sxs-lookup"><span data-stu-id="381c0-126">toostop a virtual machine and not deallocate it, use hello -StayProvisioned parameter.</span></span> <span data-ttu-id="381c0-127">Można zatrzymać wszystkie maszyny wirtualne hello hello ustawione przez nie za pomocą parametru - InstanceId hello.</span><span class="sxs-lookup"><span data-stu-id="381c0-127">You can stop all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="381c0-128">Uruchom ponownie maszynę wirtualną w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="381c0-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="381c0-129">Zastąp hello podane wartości o nazwie hello zestawu skali grupy i hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="381c0-129">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="381c0-130">Zastąp  *#*  o identyfikatorze hello hello maszyny wirtualnej mają toorestart, a następnie uruchom go:</span><span class="sxs-lookup"><span data-stu-id="381c0-130">Replace *#* with hello identifier of hello virtual machine that you want toorestart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="381c0-131">Można ponownie uruchomić wszystkie maszyny wirtualne hello w hello ustawione przez nie za pomocą parametru - InstanceId hello.</span><span class="sxs-lookup"><span data-stu-id="381c0-131">You can restart all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="381c0-132">Usuń maszynę wirtualną z zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="381c0-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="381c0-133">Zastąp hello podane wartości o nazwie hello zestawu skali grupy i hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="381c0-133">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="381c0-134">Zastąp  *#*  o identyfikatorze hello hello maszyny wirtualnej mają tooremove, a następnie uruchom go:</span><span class="sxs-lookup"><span data-stu-id="381c0-134">Replace *#* with hello identifier of hello virtual machine that you want tooremove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="381c0-135">Zestaw skali maszyny wirtualnej hello jednocześnie można usunąć, nie za pomocą parametru - InstanceId hello.</span><span class="sxs-lookup"><span data-stu-id="381c0-135">You can remove hello virtual machine scale set all at once by not using hello -InstanceId parameter.</span></span>

## <a name="change-hello-capacity-of-a-scale-set"></a><span data-ttu-id="381c0-136">Zmień hello pojemność zestawu skalowania</span><span class="sxs-lookup"><span data-stu-id="381c0-136">Change hello capacity of a scale set</span></span>
<span data-ttu-id="381c0-137">Można dodawać i usuwać maszyny wirtualne, zmieniając pojemności hello hello zestawu.</span><span class="sxs-lookup"><span data-stu-id="381c0-137">You can add or remove virtual machines by changing hello capacity of hello set.</span></span> <span data-ttu-id="381c0-138">Pobierz zestaw skali hello interesujące toochange, zestaw hello pojemności toowhat ma toobe, a następnie zaktualizuj zestaw skali hello z hello nowego miejsca.</span><span class="sxs-lookup"><span data-stu-id="381c0-138">Get hello scale set that you want toochange, set hello capacity toowhat you want it toobe, and then update hello scale set with hello new capacity.</span></span> <span data-ttu-id="381c0-139">W tych poleceń Zastąp hello podane wartości o nazwie hello zestawu skali grupy i hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="381c0-139">In these commands, replace hello quoted values with hello name of your resource group and hello scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="381c0-140">Spowoduje usunięcie z hello zestawu skalowania maszyn wirtualnych, hello maszyn wirtualnych o identyfikatorach najwyższy hello są najpierw usunąć.</span><span class="sxs-lookup"><span data-stu-id="381c0-140">If you are removing virtual machines from hello scale set, hello virtual machines with hello highest ids are removed first.</span></span>

