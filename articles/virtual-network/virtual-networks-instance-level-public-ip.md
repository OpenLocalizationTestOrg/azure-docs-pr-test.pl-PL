---
title: "Azure poziomie wystąpienia publicznego adresu IP (klasyczne) dotyczy | Dokumentacja firmy Microsoft"
description: "Zrozumienie wystąpienia adresów poziomu publicznego adresu IP (ILPIP) i jak nimi zarządzać przy użyciu programu PowerShell."
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
ms.openlocfilehash: 773043f2841ec7539b0d49357dec6bcb9f4f78a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="instance-level-public-ip-classic-overview"></a><span data-ttu-id="f47a2-103">Wystąpienia publicznego adresu IP (klasyczne) omówienie</span><span class="sxs-lookup"><span data-stu-id="f47a2-103">Instance level public IP (Classic) overview</span></span>
<span data-ttu-id="f47a2-104">Wystąpienie poziomu publicznego adresu IP (ILPIP) to publiczny adres IP, który można przypisać bezpośrednio do wystąpienia roli maszyny Wirtualnej lub usługi w chmurze, a nie do usługi w chmurze, które wystąpienie maszyny Wirtualnej lub roli znajdują się w.</span><span class="sxs-lookup"><span data-stu-id="f47a2-104">An instance level public IP (ILPIP) is a public IP address that you can assign directly to a VM or Cloud Services role instance, rather than to the cloud service that your VM or role instance reside in.</span></span> <span data-ttu-id="f47a2-105">ILPIP nie została wykonana z wirtualnego adresu IP (VIP) przypisany do usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f47a2-105">An ILPIP doesn’t take the place of the virtual IP (VIP) that is assigned to your cloud service.</span></span> <span data-ttu-id="f47a2-106">Zamiast jest dodatkowy adres IP, który umożliwia bezpośrednie łączenie się z wystąpieniem maszyny Wirtualnej lub roli.</span><span class="sxs-lookup"><span data-stu-id="f47a2-106">Rather, it’s an additional IP address that you can use to connect directly to your VM or role instance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f47a2-107">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: [model wdrażania przy użyciu usługi Azure Resource Manager i model klasyczny](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f47a2-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="f47a2-108">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f47a2-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="f47a2-109">Firma Microsoft zaleca tworzenie maszyn wirtualnych za pomocą Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="f47a2-109">Microsoft recommends creating VMs through Resource Manager.</span></span> <span data-ttu-id="f47a2-110">Upewnij się, że rozumiesz, jak [adresów IP](virtual-network-ip-addresses-overview-classic.md) pracy na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f47a2-110">Make sure you understand how [IP addresses](virtual-network-ip-addresses-overview-classic.md) work in Azure.</span></span>

![Różnica między ILPIP i adresu VIP](./media/virtual-networks-instance-level-public-ip/Figure1.png)

<span data-ttu-id="f47a2-112">Jak pokazano na rysunku 1, usługa w chmurze jest dostępny przy użyciu adresu VIP, podczas gdy poszczególnych maszyn wirtualnych są zwykle dostępne przy użyciu adresu VIP:&lt;numer portu&gt;.</span><span class="sxs-lookup"><span data-stu-id="f47a2-112">As shown in Figure 1, the cloud service is accessed using a VIP, while the individual VMs are normally accessed using VIP:&lt;port number&gt;.</span></span> <span data-ttu-id="f47a2-113">Przypisując ILPIP do określonej maszyny Wirtualnej, że można uzyskać dostępu do maszyny Wirtualnej bezpośrednio przy użyciu tego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="f47a2-113">By assigning an ILPIP to a specific VM, that VM can be accessed directly using that IP address.</span></span>

<span data-ttu-id="f47a2-114">Podczas tworzenia usługi w chmurze na platformie Azure, odpowiednie rekordy A systemu DNS są tworzone automatycznie, aby zezwolić na dostęp do usługi za pośrednictwem pełną nazwę domeny (FQDN) zamiast rzeczywistego adresu VIP.</span><span class="sxs-lookup"><span data-stu-id="f47a2-114">When you create a cloud service in Azure, corresponding DNS A records are created automatically to allow access to the service through a fully qualified domain name (FQDN), instead of using the actual VIP.</span></span> <span data-ttu-id="f47a2-115">Ten sam proces odbywa się w ILPIP zezwalania na dostęp do maszyny Wirtualnej lub roli wystąpienia przez nazwę FQDN zamiast ILPIP.</span><span class="sxs-lookup"><span data-stu-id="f47a2-115">The same process happens for an ILPIP, allowing access to the VM or role instance by FQDN instead of the ILPIP.</span></span> <span data-ttu-id="f47a2-116">Na przykład w przypadku utworzenia usługi w chmurze o nazwie *contosoadservice*, i skonfigurować rolę sieci web o nazwie *contosoweb* z dwoma wystąpieniami Azure rejestruje następujące rekordy A wystąpień:</span><span class="sxs-lookup"><span data-stu-id="f47a2-116">For instance, if you create a cloud service named *contosoadservice*, and you configure a web role named *contosoweb* with two instances, Azure registers the following A records for the instances:</span></span>

* <span data-ttu-id="f47a2-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="f47a2-117">contosoweb\_IN_0.contosoadservice.cloudapp.net</span></span>
* <span data-ttu-id="f47a2-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="f47a2-118">contosoweb\_IN_1.contosoadservice.cloudapp.net</span></span> 

> [!NOTE]
> <span data-ttu-id="f47a2-119">Można przypisać tylko jednego ILPIP dla każdego wystąpienia maszyny Wirtualnej lub roli.</span><span class="sxs-lookup"><span data-stu-id="f47a2-119">You can assign only one ILPIP for each VM or role instance.</span></span> <span data-ttu-id="f47a2-120">Możesz użyć maksymalnie 5 ILPIPs na subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="f47a2-120">You can use up to 5 ILPIPs per subscription.</span></span> <span data-ttu-id="f47a2-121">ILPIPs nie są obsługiwane dla maszyn wirtualnych z wieloma kartami Sieciowymi.</span><span class="sxs-lookup"><span data-stu-id="f47a2-121">ILPIPs are not supported for multi-NIC VMs.</span></span>
> 
> 

## <a name="why-would-i-request-an-ilpip"></a><span data-ttu-id="f47a2-122">Dlaczego może zażądać ILPIP?</span><span class="sxs-lookup"><span data-stu-id="f47a2-122">Why would I request an ILPIP?</span></span>
<span data-ttu-id="f47a2-123">Jeśli chcesz można było nawiązać połączenia z wystąpieniem maszyny Wirtualnej lub roli przy użyciu adresu IP przypisane do niego bezpośrednio, zamiast używania chmury usługi VIP:&lt;numer portu&gt;, żądania ILPIP dla maszyny Wirtualnej lub wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="f47a2-123">If you want to be able to connect to your VM or role instance by an IP address assigned directly to it, rather than using the cloud service VIP:&lt;port number&gt;, request an ILPIP for your VM or your role instance.</span></span>

* <span data-ttu-id="f47a2-124">**Aktywne FTP** -przypisując ILPIP do maszyny Wirtualnej, może odbierać ruch na dowolnym porcie.</span><span class="sxs-lookup"><span data-stu-id="f47a2-124">**Active FTP** - By assigning an ILPIP to a VM, it can receive traffic on any port.</span></span> <span data-ttu-id="f47a2-125">Punkty końcowe nie są wymagane dla maszyny Wirtualnej, aby odbierać ruch.</span><span class="sxs-lookup"><span data-stu-id="f47a2-125">Endpoints are not required for the VM to receive traffic.</span></span>  <span data-ttu-id="f47a2-126">Zobacz (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview) [Omówienie protokołu FTP] szczegółowe informacje na temat protokołu FTP.</span><span class="sxs-lookup"><span data-stu-id="f47a2-126">See (https://en.wikipedia.org/wiki/File_Transfer_Protocol#Protocol_overview)[FTP Protocol Overview] for details on the FTP protocol.</span></span>
* <span data-ttu-id="f47a2-127">**Wychodzącego** — ruch wychodzący z maszyny Wirtualnej jest mapowany na ILPIP jako źródło i ILPIP unikatowo identyfikuje maszynę Wirtualną do jednostek zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="f47a2-127">**Outbound IP** - Outbound traffic originating from the VM is mapped to the ILPIP as the source and the ILPIP uniquely identifies the VM to external entities.</span></span>

> [!NOTE]
> <span data-ttu-id="f47a2-128">W przeszłości adres ILPIP została przekazana jako publiczny adres IP (PIP).</span><span class="sxs-lookup"><span data-stu-id="f47a2-128">In the past, an ILPIP address was referred to as a public IP (PIP) address.</span></span>
> 

## <a name="manage-an-ilpip-for-a-vm"></a><span data-ttu-id="f47a2-129">Zarządzanie ILPIP dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f47a2-129">Manage an ILPIP for a VM</span></span>
<span data-ttu-id="f47a2-130">Następujące zadania umożliwiają tworzenia, przypisywania i usuwania ILPIPs z maszyn wirtualnych:</span><span class="sxs-lookup"><span data-stu-id="f47a2-130">The following tasks enable you to create, assign, and remove ILPIPs from VMs:</span></span>

### <a name="how-to-request-an-ilpip-during-vm-creation-using-powershell"></a><span data-ttu-id="f47a2-131">Jak utworzyć żądanie ILPIP podczas tworzenia maszyny Wirtualnej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f47a2-131">How to request an ILPIP during VM creation using PowerShell</span></span>
<span data-ttu-id="f47a2-132">Poniższy skrypt programu PowerShell tworzy usługi w chmurze o nazwie *FTPService*, pobiera obraz z platformy Azure, tworzy Maszynę wirtualną o nazwie *FTPInstance* przy użyciu obrazu pobrane, ustawia maszynę Wirtualną do obsługi ILPIP i dodaje maszyny Wirtualnej do nowej usługi:</span><span class="sxs-lookup"><span data-stu-id="f47a2-132">The following PowerShell script creates a cloud service named *FTPService*, retrieves an image from Azure, creates a VM named *FTPInstance* using the retrieved image, sets the VM to use an ILPIP, and adds the VM to the new service:</span></span>

```powershell
New-AzureService -ServiceName FTPService -Location "Central US"

$image = Get-AzureVMImage|?{$_.ImageName -like "*RightImage-Windows-2012R2-x64*"} `
New-AzureVMConfig -Name FTPInstance -InstanceSize Small -ImageName $image.ImageName `
| Add-AzureProvisioningConfig -Windows -AdminUsername adminuser -Password MyP@ssw0rd!! `
| Set-AzurePublicIP -PublicIPName ftpip | New-AzureVM -ServiceName FTPService -Location "Central US"
```

### <a name="how-to-retrieve-ilpip-information-for-a-vm"></a><span data-ttu-id="f47a2-133">Jak można pobrać informacji o ILPIP dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f47a2-133">How to retrieve ILPIP information for a VM</span></span>
<span data-ttu-id="f47a2-134">Aby wyświetlić informacje ILPIP dla maszyny Wirtualnej utworzone z poprzednim skryptu, uruchom następujące polecenie programu PowerShell i sprawdź wartości *PublicIPAddress* i *PublicIPName*:</span><span class="sxs-lookup"><span data-stu-id="f47a2-134">To view the ILPIP information for the VM created with the previous script, run the following PowerShell command and observe the values for *PublicIPAddress* and *PublicIPName*:</span></span>

```powershell
Get-AzureVM -Name FTPInstance -ServiceName FTPService
```

<span data-ttu-id="f47a2-135">Oczekiwane dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="f47a2-135">Expected output:</span></span>
 
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

### <a name="how-to-remove-an-ilpip-from-a-vm"></a><span data-ttu-id="f47a2-136">Jak usunąć ILPIP z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f47a2-136">How to remove an ILPIP from a VM</span></span>
<span data-ttu-id="f47a2-137">Aby usunąć ILPIP dodane do maszyny Wirtualnej w ramach poprzedniego skryptu, uruchom następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f47a2-137">To remove the ILPIP added to the VM in the previous script, run the following PowerShell command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Remove-AzurePublicIP | Update-AzureVM
```

### <a name="how-to-add-an-ilpip-to-an-existing-vm"></a><span data-ttu-id="f47a2-138">Jak dodać ILPIP do istniejącej maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f47a2-138">How to add an ILPIP to an existing VM</span></span>
<span data-ttu-id="f47a2-139">Aby dodać ILPIP do maszyny Wirtualnej utworzone za pomocą skryptu poprzedniej, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f47a2-139">To add an ILPIP to the VM created using the script previous, run the following command:</span></span>

```powershell
Get-AzureVM -ServiceName FTPService -Name FTPInstance | Set-AzurePublicIP -PublicIPName ftpip2 | Update-AzureVM
```

## <a name="manage-an-ilpip-for-a-cloud-services-role-instance"></a><span data-ttu-id="f47a2-140">Zarządzanie ILPIP dla wystąpienia roli usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="f47a2-140">Manage an ILPIP for a Cloud Services role instance</span></span>

<span data-ttu-id="f47a2-141">Aby dodać ILPIP do wystąpienia roli usługi w chmurze, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f47a2-141">To add an ILPIP to a Cloud Services role instance, complete the following steps:</span></span>

1. <span data-ttu-id="f47a2-142">Pobierz plik .cscfg dla usługi w chmurze, wykonując kroki opisane w [sposobu skonfigurowania usługi w chmurze](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artykułu.</span><span class="sxs-lookup"><span data-stu-id="f47a2-142">Download the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>
2. <span data-ttu-id="f47a2-143">Zaktualizuj plik .cscfg przez dodanie `InstanceAddress` elementu.</span><span class="sxs-lookup"><span data-stu-id="f47a2-143">Update the .cscfg file by adding the `InstanceAddress` element.</span></span> <span data-ttu-id="f47a2-144">Poniższy przykład dodaje ILPIP o nazwie *MyPublicIP* do wystąpienia roli o nazwie *WebRole1*:</span><span class="sxs-lookup"><span data-stu-id="f47a2-144">The following sample adds an ILPIP named *MyPublicIP* to a role instance named *WebRole1*:</span></span> 

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
3. <span data-ttu-id="f47a2-145">Przekaż plik .cscfg dla usługi w chmurze, wykonując kroki opisane w [sposobu skonfigurowania usługi w chmurze](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) artykułu.</span><span class="sxs-lookup"><span data-stu-id="f47a2-145">Upload the .cscfg file for the cloud service by completing the steps in the [How to Configure Cloud Services](../cloud-services/cloud-services-how-to-configure-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#reconfigure-your-cscfg) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f47a2-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f47a2-146">Next steps</span></span>
* <span data-ttu-id="f47a2-147">Zrozumienie sposobu [adresowanie IP](virtual-network-ip-addresses-overview-classic.md) działa w klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f47a2-147">Understand how [IP addressing](virtual-network-ip-addresses-overview-classic.md) works in the classic deployment model.</span></span>
* <span data-ttu-id="f47a2-148">Dowiedz się więcej o [zastrzeżone adresy IP](virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="f47a2-148">Learn about [Reserved IPs](virtual-networks-reserved-public-ip.md).</span></span>
