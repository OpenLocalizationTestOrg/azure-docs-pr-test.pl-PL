---
title: "aaaStatic wewnętrzny prywatnej Classic IP - Azure VM -"
description: "Opis statyczne wewnętrzne adresy IP (DIP) i w jaki sposób toomanage ich"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 93444c6f-af1b-41f8-a035-77f5c0302bf0
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2016
ms.author: jdial
ms.openlocfilehash: 5abe1c59f2f3ed19bcf56c269dfe57ac32d4f601
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-a-static-internal-private-ip-address-using-powershell-classic"></a><span data-ttu-id="43ee6-103">Jak tooset wewnętrzny statycznego prywatnego adresu IP adresów przy użyciu programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="43ee6-103">How tooset a static internal private IP address using PowerShell (Classic)</span></span>
<span data-ttu-id="43ee6-104">W większości przypadków nie ma potrzeby toospecify wewnętrzny statyczny adres IP dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="43ee6-104">In most cases, you won’t need toospecify a static internal IP address for your virtual machine.</span></span> <span data-ttu-id="43ee6-105">Maszyn wirtualnych w sieci wirtualnej zostanie automatycznie otrzymują wewnętrzny adres IP z zakresu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="43ee6-105">VMs in a virtual network will automatically receive an internal IP address from a range that you specify.</span></span> <span data-ttu-id="43ee6-106">Jednak w niektórych przypadkach Określanie statycznego adresu IP dla określonej maszyny Wirtualnej ma sens.</span><span class="sxs-lookup"><span data-stu-id="43ee6-106">But in certain cases, specifying a static IP address for a particular VM makes sense.</span></span> <span data-ttu-id="43ee6-107">Na przykład, jeśli maszyna wirtualna będzie toorun DNS jest lub będzie kontroler domeny.</span><span class="sxs-lookup"><span data-stu-id="43ee6-107">For example, if your VM is going toorun DNS or will be a domain controller.</span></span> <span data-ttu-id="43ee6-108">Statyczny adres IP wewnętrznego utrzymane hello maszyny Wirtualnej, nawet za pośrednictwem stanu zatrzymania/deprovision.</span><span class="sxs-lookup"><span data-stu-id="43ee6-108">A static internal IP address stays with hello VM even through a stop/deprovision state.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="43ee6-109">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="43ee6-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="43ee6-110">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="43ee6-110">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="43ee6-111">Firma Microsoft zaleca się, że większości nowych wdrożeń korzystać hello [modelu wdrażania usługi Resource Manager](virtual-networks-static-private-ip-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="43ee6-111">Microsoft recommends that most new deployments use hello [Resource Manager deployment model](virtual-networks-static-private-ip-arm-ps.md).</span></span>
> 
> 

## <a name="how-tooverify-if-a-specific-ip-address-is-available"></a><span data-ttu-id="43ee6-112">Jak tooverify, jeśli określony adres IP jest dostępna</span><span class="sxs-lookup"><span data-stu-id="43ee6-112">How tooverify if a specific IP address is available</span></span>
<span data-ttu-id="43ee6-113">tooverify Jeśli hello adres IP *10.0.0.7* jest dostępny w sieci wirtualnej o nazwie *TestVnet*, uruchom następujące polecenia programu PowerShell hello i sprawdź wartość hello *IsAvailable*:</span><span class="sxs-lookup"><span data-stu-id="43ee6-113">tooverify if hello IP address *10.0.0.7* is available in a vnet named *TestVnet*, run hello following PowerShell command and verify hello value for *IsAvailable*:</span></span>

    Test-AzureStaticVNetIP –VNetName TestVNet –IPAddress 10.0.0.7 

    IsAvailable          : True
    AvailableAddresses   : {}
    OperationDescription : Test-AzureStaticVNetIP
    OperationId          : fd3097e1-5f4b-9cac-8afa-bba1e3492609
    OperationStatus      : Succeeded

> [!NOTE]
> <span data-ttu-id="43ee6-114">Polecenie hello tootest powyżej w bezpiecznym środowisku należy wykonać wytyczne hello w [utworzyć sieć wirtualną (klasyczne)](virtual-networks-create-vnet-classic-pportal.md) toocreate sieć wirtualną o nazwie *TestVnet* i upewnij się, używa hello  *10.0.0.0/8* przestrzeni adresów.</span><span class="sxs-lookup"><span data-stu-id="43ee6-114">If you want tootest hello command above in a safe environment follow hello guidelines in [Create a virtual network (classic)](virtual-networks-create-vnet-classic-pportal.md) toocreate a vnet named *TestVnet* and ensure it uses hello *10.0.0.0/8* address space.</span></span>
> 
> 

## <a name="how-toospecify-a-static-internal-ip-when-creating-a-vm"></a><span data-ttu-id="43ee6-115">Jak toospecify statycznego wewnętrznego adresu IP podczas tworzenia maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="43ee6-115">How toospecify a static internal IP when creating a VM</span></span>
<span data-ttu-id="43ee6-116">Poniższy skrypt programu PowerShell Hello tworzy nową usługę w chmurze o nazwie *TestService*, pobiera obraz z platformy Azure, a następnie tworzy Maszynę wirtualną o nazwie *TestVM* hello nowego w usłudze w chmurze przy użyciu obrazu hello pobrać Ustawia hello toobe maszyn wirtualnych w podsieci o nazwie *podsieć 1*i ustawia *10.0.0.7* jako statyczny adres IP wewnętrznego dla hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="43ee6-116">hello PowerShell script below creates a new cloud service named *TestService*, then retrieves an image from Azure, then creates a VM named *TestVM* in hello new cloud service using hello retrieved image, sets hello VM toobe in a subnet named *Subnet-1*, and sets *10.0.0.7* as a static internal IP for hello VM:</span></span>

    New-AzureService -ServiceName TestService -Location "Central US"
    $image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"}
    New-AzureVMConfig -Name TestVM -InstanceSize Small -ImageName $image.ImageName `
    | Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
    | Set-AzureSubnet –SubnetNames Subnet-1 `
    | Set-AzureStaticVNetIP -IPAddress 10.0.0.7 `
    | New-AzureVM -ServiceName "TestService" –VNetName TestVnet

## <a name="how-tooretrieve-static-internal-ip-information-for-a-vm"></a><span data-ttu-id="43ee6-117">Jak tooretrieve statyczne wewnętrzne informacje o adresie IP dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="43ee6-117">How tooretrieve static internal IP information for a VM</span></span>
<span data-ttu-id="43ee6-118">tooview hello wewnętrznego adresu IP informacje dotyczące statycznych hello maszyny Wirtualnej utworzone za pomocą skryptu hello powyżej, uruchom następujące polecenia programu PowerShell hello i sprawdź wartości hello *IpAddress*:</span><span class="sxs-lookup"><span data-stu-id="43ee6-118">tooview hello static internal IP information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *IpAddress*:</span></span>

    Get-AzureVM -Name TestVM -ServiceName TestService

    DeploymentName              : TestService
    Name                        : TestVM
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : Provisioning
    IpAddress                   : 10.0.0.7
    InstanceStateDetails        : Windows is preparing your computer for first use...
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : TestVM
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : rsR2-797
    AvailabilitySetName         : 
    DNSName                     : http://testservice000.cloudapp.net/
    Status                      : Provisioning
    GuestAgentStatus            : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 
    PublicIPName                : 
    NetworkInterfaces           : {}
    ServiceName                 : TestService
    OperationDescription        : Get-AzureVM
    OperationId                 : 34c1560a62f0901ab75cde4fed8e8bd1
    OperationStatus             : OK

## <a name="how-tooremove-a-static-internal-ip-from-a-vm"></a><span data-ttu-id="43ee6-119">Jak tooremove statyczny adres IP wewnętrznego z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="43ee6-119">How tooremove a static internal IP from a VM</span></span>
<span data-ttu-id="43ee6-120">tooremove hello statycznego wewnętrznego adresu IP dodane toohello maszyny Wirtualnej w skrypcie hello powyżej, uruchom hello następującego polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="43ee6-120">tooremove hello static internal IP added toohello VM in hello script above, run hello following PowerShell command:</span></span>

    Get-AzureVM -ServiceName TestService -Name TestVM `
    | Remove-AzureStaticVNetIP `
    | Update-AzureVM

## <a name="how-tooadd-a-static-internal-ip-tooan-existing-vm"></a><span data-ttu-id="43ee6-121">Jak tooadd statyczne wewnętrzne tooan IP istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="43ee6-121">How tooadd a static internal IP tooan existing VM</span></span>
<span data-ttu-id="43ee6-122">tooadd statyczne wewnętrzne toohello IP maszyny Wirtualnej utworzonej przy użyciu skryptu hello powyżej runt następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="43ee6-122">tooadd a static internal IP toohello VM created using hello script above, runt he following command:</span></span>

    Get-AzureVM -ServiceName TestService000 -Name TestVM `
    | Set-AzureStaticVNetIP -IPAddress 10.10.0.7 `
    | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="43ee6-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43ee6-123">Next steps</span></span>
[<span data-ttu-id="43ee6-124">Zastrzeżony adres IP</span><span class="sxs-lookup"><span data-stu-id="43ee6-124">Reserved IP</span></span>](virtual-networks-reserved-public-ip.md)

[<span data-ttu-id="43ee6-125">Poziom wystąpienia publicznego adresu IP (ILPIP)</span><span class="sxs-lookup"><span data-stu-id="43ee6-125">Instance-Level Public IP (ILPIP)</span></span>](virtual-networks-instance-level-public-ip.md)

[<span data-ttu-id="43ee6-126">Interfejsy API REST zastrzeżonego adresu IP</span><span class="sxs-lookup"><span data-stu-id="43ee6-126">Reserved IP REST APIs</span></span>](https://msdn.microsoft.com/library/azure/dn722420.aspx)

