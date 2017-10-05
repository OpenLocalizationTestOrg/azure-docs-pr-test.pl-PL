---
title: "Konfigurowanie sieci wirtualnej platformy Azure (klasyczne) — plik konfiguracji sieci | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tworzyć i modyfikować sieci wirtualnych (klasyczne) przez eksportowanie, zmienianie i importowanie pliku konfiguracji sieci."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: f1e3ae26b6525f2235a6b0d53546b334dc027b94
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="93e83-103">Skonfiguruj sieć wirtualną (klasyczne) przy użyciu pliku konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="93e83-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="93e83-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93e83-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="93e83-105">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="93e83-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="93e83-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać modelu wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="93e83-106">Microsoft recommends that most new deployments use the Resource Manager deployment model.</span></span>

<span data-ttu-id="93e83-107">Można tworzyć i konfigurować sieć wirtualna (klasyczna) z pliku konfiguracji sieci przy użyciu interfejsu wiersza polecenia platformy Azure (CLI) 1.0 lub Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93e83-107">You can create and configure a virtual network (classic) with a network configuration file using the Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="93e83-108">Nie można utworzyć lub zmodyfikować sieć wirtualną przy użyciu modelu wdrażania usługi Azure Resource Manager przy użyciu pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="93e83-108">You cannot create or modify a virtual network through the Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="93e83-109">Nie można użyć portalu Azure do tworzenia lub modyfikowania sieci wirtualnej (klasyczne) przy użyciu pliku konfiguracji sieci, jednak można utworzyć sieć wirtualną (klasyczne), portalu Azure, bez użycia pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="93e83-109">You cannot use the Azure portal to create or modify a virtual network (classic) using a network configuration file, however you can use the Azure portal to create a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="93e83-110">Tworzenie i konfigurowanie sieci wirtualnej (klasyczne) przy użyciu pliku konfiguracji sieci wymaga eksportowania, zmienianie i importowanie pliku.</span><span class="sxs-lookup"><span data-stu-id="93e83-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing the file.</span></span>

## <span data-ttu-id="93e83-111"><a name="export"></a>Eksportowanie plików konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="93e83-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="93e83-112">Aby wyeksportować plik konfiguracji sieci, można użyć programu PowerShell lub wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="93e83-112">You can use PowerShell or the Azure CLI to export a network configuration file.</span></span> <span data-ttu-id="93e83-113">PowerShell eksportuje pliku XML podczas interfejsu wiersza polecenia Azure eksportuje pliku json.</span><span class="sxs-lookup"><span data-stu-id="93e83-113">PowerShell exports an XML file, while the Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="93e83-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93e83-114">PowerShell</span></span>
 
1. <span data-ttu-id="93e83-115">[Instalowanie programu Azure PowerShell i logowanie do platformy Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93e83-115">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="93e83-116">Zmień katalog (i upewnij się, istnieje) i nazwę pliku w poniższym poleceniu zgodnie z potrzebami, następnie uruchom polecenie, aby wyeksportować plik konfiguracji sieci:</span><span class="sxs-lookup"><span data-stu-id="93e83-116">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="93e83-117">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="93e83-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="93e83-118">[Zainstaluj Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93e83-118">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="93e83-119">Wykonaj pozostałe kroki w wierszu polecenia, Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="93e83-119">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="93e83-120">Logowanie do platformy Azure, wprowadzając `azure login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="93e83-120">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="93e83-121">Upewnij się, jest w trybie asm wprowadzając `azure config mode asm` polecenia.</span><span class="sxs-lookup"><span data-stu-id="93e83-121">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="93e83-122">Zmień katalog (i upewnij się, istnieje) i nazwę pliku w poniższym poleceniu zgodnie z potrzebami, następnie uruchom polecenie, aby wyeksportować plik konfiguracji sieci:</span><span class="sxs-lookup"><span data-stu-id="93e83-122">Change the directory (and ensure it exists) and filename in the following command as desired, then run the command to export the network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="93e83-123">Utwórz lub zmodyfikuj plik konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="93e83-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="93e83-124">Plik konfiguracji sieci jest plik XML (w przypadku używania programu PowerShell) lub plik json (w przypadku używania interfejsu wiersza polecenia Azure).</span><span class="sxs-lookup"><span data-stu-id="93e83-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using the Azure CLI).</span></span> <span data-ttu-id="93e83-125">Można edytować plik w dowolnym tekstu lub edytora XML/json.</span><span class="sxs-lookup"><span data-stu-id="93e83-125">You can edit the file in any text, or XML/json editor.</span></span> <span data-ttu-id="93e83-126">[Ustawienia schematu pliku konfiguracji sieci](https://msdn.microsoft.com/library/azure/jj157100.aspx) artykuł zawiera szczegółowe informacje o wszystkich ustawieniach.</span><span class="sxs-lookup"><span data-stu-id="93e83-126">The [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="93e83-127">Opis dodatkowych ustawień, zobacz [wyświetlić sieci wirtualnych i ustawienia](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="93e83-127">For additional explanation of the settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="93e83-128">Zmiany wprowadzone w pliku:</span><span class="sxs-lookup"><span data-stu-id="93e83-128">The changes you make to the file:</span></span>

- <span data-ttu-id="93e83-129">Musi być zgodne z schematu lub importowanie niepowodzenia pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="93e83-129">Must comply with the schema, or importing the network configuration file will fail.</span></span>
- <span data-ttu-id="93e83-130">Zastąp wszystkie istniejące ustawienia sieci dla Twojej subskrypcji, dlatego należy zachować wyjątkową ostrożność podczas wprowadzania zmian.</span><span class="sxs-lookup"><span data-stu-id="93e83-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="93e83-131">Na przykład odwołanie pliki konfiguracyjne przykład sieci, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="93e83-131">For example, reference the example network configuration files that follow.</span></span> <span data-ttu-id="93e83-132">Powiedz oryginalny plik zawiera dwa **VirtualNetworkSite** wystąpienia, a uległ zmianie, jak przedstawiono w przykładach.</span><span class="sxs-lookup"><span data-stu-id="93e83-132">Say the original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in the examples.</span></span> <span data-ttu-id="93e83-133">Podczas importowania pliku Azure usuwa sieć wirtualną **VirtualNetworkSite** wystąpienia usunięte w pliku.</span><span class="sxs-lookup"><span data-stu-id="93e83-133">When you import the file, Azure deletes the virtual network for the **VirtualNetworkSite** instance you removed in the file.</span></span> <span data-ttu-id="93e83-134">W tym scenariuszu uproszczony przyjęto zostały żadnych zasobów w sieci wirtualnej, jak w przypadku, nie można usunąć sieci wirtualnej, a import nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="93e83-134">This simplified scenario assumes no resources were in the virtual network, as if there were, the virtual network could not be deleted, and the import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93e83-135">Azure uwzględnia podsieć, która ma coś wdrożone w niej jako **używany**.</span><span class="sxs-lookup"><span data-stu-id="93e83-135">Azure considers a subnet that has something deployed to it as **in use**.</span></span> <span data-ttu-id="93e83-136">Gdy używany jest podsieci, nie można modyfikować.</span><span class="sxs-lookup"><span data-stu-id="93e83-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="93e83-137">Przed zmodyfikowaniem informacji o podsieci w pliku konfiguracji sieci, należy przenieść wszystkie elementy, które zostały wdrożone do podsieci do innej podsieci, która nie jest modyfikowana.</span><span class="sxs-lookup"><span data-stu-id="93e83-137">Before modifying subnet information in a network configuration file, move anything that you have deployed to the subnet to a different subnet that isn't being modified.</span></span> <span data-ttu-id="93e83-138">Zobacz [przenieść do innej podsieci maszyny Wirtualnej lub wystąpienia roli](virtual-networks-move-vm-role-to-subnet.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="93e83-138">See [Move a VM or Role Instance to a Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="93e83-139">Przykład XML do użycia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="93e83-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="93e83-140">Następujący przykładowy plik konfiguracji sieci tworzy sieć wirtualną o nazwie *myVirtualNetwork* się na przestrzeń adresową z *10.0.0.0/16* w *wschodnie stany USA* Azure region.</span><span class="sxs-lookup"><span data-stu-id="93e83-140">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="93e83-141">Sieć wirtualna zawiera jedną podsieć o nazwie *mySubnet* z prefiksem adresu o *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="93e83-141">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

<span data-ttu-id="93e83-142">Wyeksportowany plik konfiguracji sieci zawiera zawartość nie, można skopiować kod XML w poprzednim przykładzie i wklej go do nowego pliku.</span><span class="sxs-lookup"><span data-stu-id="93e83-142">If the network configuration file you exported contains no contents, you can copy the XML in the previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-the-azure-cli-10"></a><span data-ttu-id="93e83-143">Przykład JSON do użytku z interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="93e83-143">Example JSON for use with the Azure CLI 1.0</span></span>

<span data-ttu-id="93e83-144">Następujący przykładowy plik konfiguracji sieci tworzy sieć wirtualną o nazwie *myVirtualNetwork* się na przestrzeń adresową z *10.0.0.0/16* w *wschodnie stany USA* Azure region.</span><span class="sxs-lookup"><span data-stu-id="93e83-144">The following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in the *East US* Azure region.</span></span> <span data-ttu-id="93e83-145">Sieć wirtualna zawiera jedną podsieć o nazwie *mySubnet* z prefiksem adresu o *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="93e83-145">The virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

<span data-ttu-id="93e83-146">Wyeksportowany plik konfiguracji sieci zawiera zawartość nie, można skopiować dane json w poprzednim przykładzie i wklej go do nowego pliku.</span><span class="sxs-lookup"><span data-stu-id="93e83-146">If the network configuration file you exported contains no contents, you can copy the json in the previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="93e83-147"><a name="import"></a>Importowanie pliku konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="93e83-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="93e83-148">Aby zaimportować plik konfiguracji sieci, można użyć programu PowerShell lub interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="93e83-148">You can use PowerShell or the Azure CLI to import a network configuration file.</span></span> <span data-ttu-id="93e83-149">PowerShell importuje plik XML podczas interfejsu wiersza polecenia Azure importuje plik json.</span><span class="sxs-lookup"><span data-stu-id="93e83-149">PowerShell imports an XML file, while the Azure CLI imports a json file.</span></span> <span data-ttu-id="93e83-150">Jeśli import zakończy się niepowodzeniem, upewnij się, że plik spełnia [schemat konfiguracji sieci](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="93e83-150">If the import fails, confirm that the file complies with the [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="93e83-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93e83-151">PowerShell</span></span>
 
1. <span data-ttu-id="93e83-152">[Instalowanie programu Azure PowerShell i logowanie do platformy Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93e83-152">[Install Azure PowerShell and sign in to Azure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="93e83-153">Zmień katalog i nazwę pliku w poniższym poleceniu w razie potrzeby, następnie uruchom polecenie, aby zaimportować plik konfiguracji sieci:</span><span class="sxs-lookup"><span data-stu-id="93e83-153">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="93e83-154">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="93e83-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="93e83-155">[Zainstaluj Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="93e83-155">[Install the Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="93e83-156">Wykonaj pozostałe kroki w wierszu polecenia, Azure CLI w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="93e83-156">Complete the remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="93e83-157">Logowanie do platformy Azure, wprowadzając `azure login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="93e83-157">Log in to Azure by entering the `azure login` command.</span></span>
3. <span data-ttu-id="93e83-158">Upewnij się, jest w trybie asm wprowadzając `azure config mode asm` polecenia.</span><span class="sxs-lookup"><span data-stu-id="93e83-158">Ensure you're in asm mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="93e83-159">Zmień katalog i nazwę pliku w poniższym poleceniu w razie potrzeby, następnie uruchom polecenie, aby zaimportować plik konfiguracji sieci:</span><span class="sxs-lookup"><span data-stu-id="93e83-159">Change the directory and filename in the following command as necessary, then run the command to import the network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
