---
title: "aaaAzure poziomie wystąpienia publicznego adresu IP (klasyczne) dotyczy | Dokumentacja firmy Microsoft"
description: "Zrozumienie poziomu publiczne adresy IP (ILPIP) wystąpienia i w jaki sposób toomanage ich przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
ms.assetid: 07eef6ec-7dfe-4c4d-a2c2-be0abfb48ec5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2016
ms.author: jdial
ms.openlocfilehash: 832143ee6fdd80b634e1cebfddc759a8cacda583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="09cc9-103">Wystąpienia publicznego adresu IP (klasyczne) omówienie</span><span class="sxs-lookup"><span data-stu-id="09cc9-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="09cc9-104">Wystąpienie poziomu publicznego adresu IP (ILPIP) to publiczny adres IP, który można przypisać bezpośrednio tooa wystąpienia roli maszyny Wirtualnej lub usługi w chmurze, a nie toohello usługi w chmurze maszyny Wirtualnej lub roli wystąpienia znajdują się w.</span><span class="sxs-lookup"><span data-stu-id="09cc9-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly tooa VM or Cloud Services role instance, rather than toohello cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="09cc9-105">ILPIP nie została wykonana hello z hello wirtualnego adresu IP (VIP) przypisany tooyour usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="09cc9-105">An ILPIP doesn’t take hello place of hello virtual IP (VIP) that is assigned tooyour cloud service.</span></span> <span data-ttu-id="09cc9-106">Jest to raczej dodatkowy adres IP służy tooconnect bezpośrednio tooyour maszyny Wirtualnej lub roli wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="09cc9-106">Rather, it’s an additional IP address that you can use tooconnect directly tooyour VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09cc9-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="09cc9-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="09cc9-108">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="09cc9-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="09cc9-109">Firma Microsoft zaleca tworzenie maszyn wirtualnych za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="09cc9-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="09cc9-110">Upewnij się, że rozumiesz, jak [adresów IP](virtual-network-ip-addresses-overview-classic.md) pracy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="09cc9-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Różnica między ILPIP i adresu VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="09cc9-112">Jak pokazano na rysunku 1, usługa w chmurze hello jest dostępny przy użyciu adresu VIP, podczas hello poszczególnych maszyn wirtualnych są zwykle dostępne przy użyciu adresu VIP:&lt;numer portu&gt;.</span><span class="sxs-lookup"><span data-stu-id="09cc9-112">As shown in Figure 1, hello cloud service is accessed using a VIP, while hello individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="09cc9-113">Przypisując tooa ILPIP określonej maszyny Wirtualnej, które mogą być maszyny Wirtualnej dostępne bezpośrednio przy użyciu tego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="09cc9-113">By assigning an ILPIP tooa specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="09cc9-114">Podczas tworzenia usługi w chmurze na platformie Azure, odpowiednie rekordy A systemu DNS są tworzone automatycznie tooallow dostępu toohello usługi za pośrednictwem pełną nazwę domeny (FQDN), zamiast rzeczywistego adresu VIP hello.</span><span class="sxs-lookup"><span data-stu-id="09cc9-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically tooallow access toohello service through a fully qualified domain name (FQDN), instead of using hello actual VIP.</span></span> <span data-ttu-id="09cc9-115">Witaj, który sam proces odbywa się w ILPIP, umożliwiając dostęp toohello maszyny Wirtualnej lub roli wystąpienia przez nazwę FQDN zamiast hello ILPIP.</span><span class="sxs-lookup"><span data-stu-id="09cc9-115">hello same process happens for an ILPIP, allowing access toohello VM or role instance by FQDN instead of hello ILPIP.</span></span> <span data-ttu-id="09cc9-116">Na przykład w przypadku utworzenia usługi w chmurze o nazwie *contosoadservice*, i skonfigurować rolę sieci web o nazwie *contosoweb* z dwoma wystąpieniami hello Azure rejestruje następujące A rekordów dla wystąpień hello:</span><span class="sxs-lookup"><span data-stu-id="09cc9-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers hello following A records for hello instances:</span></span>

* <span data-ttu-id="09cc9-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="09cc9-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="09cc9-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="09cc9-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="09cc9-119">Można przypisać tylko jednego ILPIP dla każdego wystąpienia maszyny Wirtualnej lub roli.</span><span class="sxs-lookup"><span data-stu-id="09cc9-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="09cc9-120">Może zużywać ILPIPs too5 na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="09cc9-120">You can use up too5 ILPIPs per subscription.</span></span> <span data-ttu-id="09cc9-121">ILPIPs nie są obsługiwane dla maszyn wirtualnych z wieloma kartami Sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="09cc9-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="09cc9-122">Dlaczego może zażądać ILPIP?</span><span class="sxs-lookup"><span data-stu-id="09cc9-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="09cc9-123">Toobe stanie tooconnect tooyour maszyny Wirtualnej lub wystąpienia roli przy użyciu adresu IP bezpośrednio przypisać tooit, zamiast używania hello chmury usługi VIP:&lt;numer portu&gt;, żądania ILPIP dla maszyny Wirtualnej lub wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="09cc9-123">If you want toobe able tooconnect tooyour VM or role instance by an IP address assigned directly tooit, rather than using hello cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="09cc9-124">**Aktywne FTP** -przypisując tooa ILPIP maszyny Wirtualnej, może odbierać ruch na dowolnym porcie.</span><span class="sxs-lookup"><span data-stu-id="09cc9-124">**Active FTP** - By assigning an ILPIP tooa VM, it can receive traffic on any port.</span></span> <span data-ttu-id="09cc9-125">Punkty końcowe nie są wymagane dla hello ruch tooreceive maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="09cc9-125">Endpoints are not required for hello VM tooreceive traffic.</span></span>  <span data-ttu-id="09cc9-126">Zobacz (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [Omówienie protokołu FTP] szczegółowe informacje na temat protokołu hello FTP.</span><span class="sxs-lookup"><span data-stu-id="09cc9-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on hello FTP protocol.</span></span>
* <span data-ttu-id="09cc9-127">**Wychodzącego** — ruch wychodzący z hello maszyna wirtualna jest zamapowany toohello ILPIP jako źródło hello i hello ILPIP unikatowo identyfikuje jednostki tooexternal maszyny Wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="09cc9-127">**Outbound IP** - Outbound traffic originating from hello VM is mapped toohello ILPIP as hello source and hello ILPIP uniquely identifies hello VM tooexternal entities.</span></span>

> [!NOTE]
> <span data-ttu-id="09cc9-128">W ciągu ostatnich hello adres ILPIP został określony tooas publicznego adresu IP (PIP).</span><span class="sxs-lookup"><span data-stu-id="09cc9-128">In hello past, an ILPIP address was referred tooas a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="09cc9-129">Zarządzanie ILPIP dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="09cc9-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="09cc9-130">następujące zadania Hello Włącz toocreate, przypisz i Usuń ILPIPs z maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="09cc9-130">hello following tasks enable you toocreate, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-toorequest-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="09cc9-131">Jak toorequest ILPIP podczas tworzenia maszyny Wirtualnej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="09cc9-131">How toorequest an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="09cc9-132">usługi w chmurze o nazwie tworzy Hello następującego skryptu programu PowerShell *FTPService*, pobiera obraz z platformy Azure, tworzy Maszynę wirtualną o nazwie *FTPInstance* przy użyciu obrazu hello pobrać ustawia hello wirtualna toouse ILPIP i dodaje hello wirtualna toohello nowej usługi:</span><span class="sxs-lookup"><span data-stu-id="09cc9-132">hello following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using hello retrieved image, sets hello VM toouse an ILPIP, and adds hello VM toohello new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-tooretrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="09cc9-133">Jak tooretrieve ILPIP informacji dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="09cc9-133">How tooretrieve ILPIP information for a VM</span></span>
<span data-ttu-id="09cc9-134">hello tooview informacji ILPIP dla hello maszyny Wirtualnej utworzone za pomocą skryptu poprzedniej hello, uruchom następujące polecenia programu PowerShell hello i obserwować wartości hello *PublicIPAddress* i *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="09cc9-134">tooview hello ILPIP information for hello VM created with hello previous script, run hello following PowerShell command and observe hello values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="09cc9-135">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="09cc9-135">Expected output:</span></span>
 
    DeploymentName              : FTPService
    Name                        : FTPInstance
    Label                       : 
    VM                          : Microsoft.WindowsAzure.Commands.ServiceManagement.Model.PersistentVM
    InstanceStatus              : ReadyRole
    IpAddress                   : 100.74.118.91
    InstanceStateDetails        : 
    PowerState                  : Started
    InstanceErrorCode           : 
    InstanceFaultDomain         : 0
    InstanceName                : FTPInstance
    InstanceUpgradeDomain       : 0
    InstanceSize                : Small
    HostName                    : FTPInstance
    AvailabilitySetName         : 
    DNSName                     : http://ftpservice888.cloudapp.net/
    Status                      : ReadyRole
    GuestAgentStatus            :   Microsoft.WindowsAzure.Commands.ServiceManagement.Model.GuestAgentStatus
    ResourceExtensionStatusList : {Microsoft.Compute.BGInfo}
    PublicIPAddress             : 104.43.142.188
    PublicIPName                : ftpip
    NetworkInterfaces           : {}
    ServiceName                 : FTPService
    OperationDescription        : Get-AzureVM
    OperationId                 : 568d88d2be7c98f4bbb875e4d823718e
    OperationStatus             : OK

### <a name="how-tooremove-an-ilpip-from-a-vm"></a><span data-ttu-id="09cc9-136">Jak tooremove ILPIP z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="09cc9-136">How tooremove an ILPIP from a VM</span></span>
<span data-ttu-id="09cc9-137">w poprzedniej skryptu hello, uruchom następujące polecenia programu PowerShell hello tooremove hello ILPIP dodaje toohello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="09cc9-137">tooremove hello ILPIP added toohello VM in hello previous script, run hello following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-tooadd-an-ilpip-tooan-existing-vm"></a><span data-ttu-id="09cc9-138">Jak tooadd tooan ILPIP istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="09cc9-138">How tooadd an ILPIP tooan existing VM</span></span>
<span data-ttu-id="09cc9-139">tooadd toohello ILPIP maszyny Wirtualnej utworzonej przy użyciu skryptu hello poprzedniego, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="09cc9-139">tooadd an ILPIP toohello VM created using hello script previous, run hello following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="09cc9-140">Zarządzanie ILPIP dla wystąpienia roli usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="09cc9-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="09cc9-141">tooadd ILPIP tooa usługi w chmurze wystąpienia roli, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="09cc9-141">tooadd an ILPIP tooa Cloud Services role instance, complete hello following steps:</span></span>

1. <span data-ttu-id="09cc9-142">Pobrać plik .cscfg hello hello usługi w chmurze, wykonując hello etapami hello [jak usług w chmurze tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artykułu.</span><span class="sxs-lookup"><span data-stu-id="09cc9-142">Download hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="09cc9-143">Plik .cscfg hello aktualizacji przez dodanie hello `InstanceAddress` elementu.</span><span class="sxs-lookup"><span data-stu-id="09cc9-143">Update hello .cscfg file by adding hello `InstanceAddress` element.</span></span> <span data-ttu-id="09cc9-144">Witaj następującym przykładowym dodaje ILPIP o nazwie *MyPublicIP* tooa wystąpienia roli o nazwie *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="09cc9-144">hello following sample adds an ILPIP named *MyPublicIP* tooa role instance named *WebRole1*:</span></span> 

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ServiceConfiguration serviceName="ILPIPSample" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="4" osVersion="*" schemaVersion="2014-01.2.3">
      <Role name="WebRole1">
        <Instances count="1" />
          <ConfigurationSettings>
        <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
          </ConfigurationSettings>
      </Role>
      <NetworkConfiguration>
        <AddressAssignments>
          <InstanceAddress roleName="WebRole1">
        <PublicIPs>
          <PublicIP name="MyPublicIP" domainNameLabel="MyPublicIP" />
            </PublicIPs>
          </InstanceAddress>
        </AddressAssignments>
      </NetworkConfiguration>
    </ServiceConfiguration>
    ```
3. <span data-ttu-id="09cc9-145">Przesyłanie pliku .cscfg hello hello usługi w chmurze, wykonując hello etapami hello [jak usług w chmurze tooConfigure](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artykułu.</span><span class="sxs-lookup"><span data-stu-id="09cc9-145">Upload hello .cscfg file for hello cloud service by completing hello steps in hello [How tooConfigure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09cc9-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09cc9-146">Next steps</span></span>
* <span data-ttu-id="09cc9-147">Zrozumienie sposobu [adresowanie IP](virtual-network-ip-addresses-overview-classic.md) działa w hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="09cc9-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in hello classic deployment model.</span></span>
* <span data-ttu-id="09cc9-148">Dowiedz się więcej o [zastrzeżone adresy IP](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="09cc9-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
