---
title: "aaaConfigure sieci wirtualnej platformy Azure (klasyczne) — plik konfiguracji sieci | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i modyfikowania sieci wirtualnych (klasyczne) przez eksportowanie, zmienianie i importowanie pliku konfiguracji sieci."
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
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a><span data-ttu-id="a7772-103">Skonfiguruj sieć wirtualną (klasyczne) przy użyciu pliku konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="a7772-103">Configure a virtual network (classic) using a network configuration file</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a7772-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7772-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="a7772-105">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="a7772-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="a7772-106">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="a7772-106">Microsoft recommends that most new deployments use hello Resource Manager deployment model.</span></span>

<span data-ttu-id="a7772-107">Można tworzyć i konfigurować sieć wirtualna (klasyczna) z pliku konfiguracji sieci przy użyciu hello Azure interfejsu wiersza polecenia (CLI) 1.0 lub Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a7772-107">You can create and configure a virtual network (classic) with a network configuration file using hello Azure command-line interface (CLI) 1.0 or Azure PowerShell.</span></span> <span data-ttu-id="a7772-108">Nie można utworzyć lub zmodyfikować sieć wirtualną przy użyciu modelu wdrażania usługi Azure Resource Manager hello przy użyciu pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="a7772-108">You cannot create or modify a virtual network through hello Azure Resource Manager deployment model using a network configuration file.</span></span> <span data-ttu-id="a7772-109">Nie można użyć hello toocreate portalu Azure lub zmodyfikować sieci wirtualnej (klasyczne) przy użyciu pliku konfiguracji sieci, jednak można korzystać hello toocreate portalu Azure (klasyczną), sieci wirtualnej bez użycia pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="a7772-109">You cannot use hello Azure portal toocreate or modify a virtual network (classic) using a network configuration file, however you can use hello Azure portal toocreate a virtual network (classic), without using a network configuration file.</span></span>

<span data-ttu-id="a7772-110">Tworzenie i konfigurowanie sieci wirtualnej (klasyczne) przy użyciu pliku konfiguracji sieci wymaga eksportowanie, zmienianie i importowanie pliku hello.</span><span class="sxs-lookup"><span data-stu-id="a7772-110">Creating and configuring a virtual network (classic) with a network configuration file requires exporting, changing, and importing hello file.</span></span>

## <span data-ttu-id="a7772-111"><a name="export"></a>Eksportowanie plików konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="a7772-111"><a name="export"></a>Export a network configuration file</span></span>

<span data-ttu-id="a7772-112">Możesz użyć programu PowerShell lub hello Azure CLI tooexport pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="a7772-112">You can use PowerShell or hello Azure CLI tooexport a network configuration file.</span></span> <span data-ttu-id="a7772-113">PowerShell eksportuje pliku XML, gdy hello Azure CLI eksportuje pliku json.</span><span class="sxs-lookup"><span data-stu-id="a7772-113">PowerShell exports an XML file, while hello Azure CLI exports a json file.</span></span>

### <a name="powershell"></a><span data-ttu-id="a7772-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7772-114">PowerShell</span></span>
 
1. <span data-ttu-id="a7772-115">[Instalowanie programu Azure PowerShell i logowanie tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7772-115">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="a7772-116">Zmień katalog hello (i upewnij się, istnieje) i nazwę pliku w hello następujące polecenie jako odpowiednie, a następnie uruchom hello polecenia tooexport hello sieci pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a7772-116">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="a7772-117">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="a7772-117">Azure CLI 1.0</span></span>

1. <span data-ttu-id="a7772-118">[Zainstaluj hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7772-118">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="a7772-119">Wykonaj pozostałe kroki w wierszu polecenia, Azure CLI 1.0 hello.</span><span class="sxs-lookup"><span data-stu-id="a7772-119">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="a7772-120">Zaloguj się za tooAzure wprowadzając hello `azure login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a7772-120">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="a7772-121">Upewnij się, jest w trybie asm wprowadzając hello `azure config mode asm` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a7772-121">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="a7772-122">Zmień katalog hello (i upewnij się, istnieje) i nazwę pliku w hello następujące polecenie jako odpowiednie, a następnie uruchom hello polecenia tooexport hello sieci pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a7772-122">Change hello directory (and ensure it exists) and filename in hello following command as desired, then run hello command tooexport hello network configuration file:</span></span>
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a><span data-ttu-id="a7772-123">Utwórz lub zmodyfikuj plik konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="a7772-123">Create or modify a network configuration file</span></span>

<span data-ttu-id="a7772-124">Plik konfiguracji sieci jest plik XML (w przypadku używania programu PowerShell) lub plik json (w przypadku używania hello Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="a7772-124">A network configuration file is an XML file (when using PowerShell) or a json file (when using hello Azure CLI).</span></span> <span data-ttu-id="a7772-125">Możesz edytować plik hello w dowolnym tekstu lub edytora XML/json.</span><span class="sxs-lookup"><span data-stu-id="a7772-125">You can edit hello file in any text, or XML/json editor.</span></span> <span data-ttu-id="a7772-126">Witaj [ustawienia schematu pliku konfiguracji sieci](https://msdn.microsoft.com/library/azure/jj157100.aspx) artykuł zawiera szczegółowe informacje o wszystkich ustawieniach.</span><span class="sxs-lookup"><span data-stu-id="a7772-126">hello [Network configuration file schema settings](https://msdn.microsoft.com/library/azure/jj157100.aspx) article includes details for all settings.</span></span> <span data-ttu-id="a7772-127">Dodatkowe wyjaśnienie hello ustawień, zobacz [wyświetlić sieci wirtualnych i ustawienia](virtual-network-manage-network.md#view-vnet).</span><span class="sxs-lookup"><span data-stu-id="a7772-127">For additional explanation of hello settings, see [View virtual networks and settings](virtual-network-manage-network.md#view-vnet).</span></span> <span data-ttu-id="a7772-128">Witaj wprowadzone zmiany pliku toohello:</span><span class="sxs-lookup"><span data-stu-id="a7772-128">hello changes you make toohello file:</span></span>

- <span data-ttu-id="a7772-129">Musi być zgodne z hello schematu lub importowania sieci hello pliku konfiguracji nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="a7772-129">Must comply with hello schema, or importing hello network configuration file will fail.</span></span>
- <span data-ttu-id="a7772-130">Zastąp wszystkie istniejące ustawienia sieci dla Twojej subskrypcji, dlatego należy zachować wyjątkową ostrożność podczas wprowadzania zmian.</span><span class="sxs-lookup"><span data-stu-id="a7772-130">Overwrite any existing network settings for your subscription, so use extreme caution when making modifications.</span></span> <span data-ttu-id="a7772-131">Na przykład odwołanie hello przykład sieci pliki konfiguracyjne, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="a7772-131">For example, reference hello example network configuration files that follow.</span></span> <span data-ttu-id="a7772-132">Powiedz hello oryginalny plik zawiera dwa **VirtualNetworkSite** wystąpienia, a uległ zmianie, jak przedstawiono w przykładach hello.</span><span class="sxs-lookup"><span data-stu-id="a7772-132">Say hello original file contained two **VirtualNetworkSite** instances, and you changed it, as shown in hello examples.</span></span> <span data-ttu-id="a7772-133">Podczas importowania pliku hello Azure usuwa hello sieć wirtualną hello **VirtualNetworkSite** usunięte w pliku hello wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="a7772-133">When you import hello file, Azure deletes hello virtual network for hello **VirtualNetworkSite** instance you removed in hello file.</span></span> <span data-ttu-id="a7772-134">W tym scenariuszu uproszczony przyjęto zostały żadnych zasobów w sieci wirtualnej hello, jak w przypadku, nie można usunąć sieci wirtualnej hello i hello import nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="a7772-134">This simplified scenario assumes no resources were in hello virtual network, as if there were, hello virtual network could not be deleted, and hello import would fail.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7772-135">Azure uwzględnia podsieć, która ma coś wdrożone tooit jako **używany**.</span><span class="sxs-lookup"><span data-stu-id="a7772-135">Azure considers a subnet that has something deployed tooit as **in use**.</span></span> <span data-ttu-id="a7772-136">Gdy używany jest podsieci, nie można modyfikować.</span><span class="sxs-lookup"><span data-stu-id="a7772-136">When a subnet is in use, it cannot be modified.</span></span> <span data-ttu-id="a7772-137">Przed zmodyfikowaniem informacji o podsieci w pliku konfiguracji sieci, należy przenieść wszystkie elementy, które zostały wdrożone toohello podsieci tooa innej podsieci, która nie jest modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="a7772-137">Before modifying subnet information in a network configuration file, move anything that you have deployed toohello subnet tooa different subnet that isn't being modified.</span></span> <span data-ttu-id="a7772-138">Zobacz [przenoszenia maszyny Wirtualnej lub wystąpienia roli tooa innej podsieci](virtual-networks-move-vm-role-to-subnet.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="a7772-138">See [Move a VM or Role Instance tooa Different Subnet](virtual-networks-move-vm-role-to-subnet.md) for details.</span></span>

### <a name="example-xml-for-use-with-powershell"></a><span data-ttu-id="a7772-139">Przykład XML do użycia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7772-139">Example XML for use with PowerShell</span></span>

<span data-ttu-id="a7772-140">Witaj następujący przykładowy plik konfiguracji sieci tworzy sieć wirtualną o nazwie *myVirtualNetwork* się na przestrzeń adresową z *10.0.0.0/16* w hello *wschodnie stany USA* Azure region.</span><span class="sxs-lookup"><span data-stu-id="a7772-140">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="a7772-141">sieć wirtualna Hello zawiera jedną podsieć o nazwie *mySubnet* z prefiksem adresu o *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="a7772-141">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="a7772-142">Plik konfiguracji sieci hello wyeksportowanymi zawiera zawartość nie, można skopiować hello XML w poprzednim przykładzie hello i wklej go do nowego pliku.</span><span class="sxs-lookup"><span data-stu-id="a7772-142">If hello network configuration file you exported contains no contents, you can copy hello XML in hello previous example, and paste it into a new file.</span></span>

### <a name="example-json-for-use-with-hello-azure-cli-10"></a><span data-ttu-id="a7772-143">Przykład JSON do użycia z hello Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="a7772-143">Example JSON for use with hello Azure CLI 1.0</span></span>

<span data-ttu-id="a7772-144">Witaj następujący przykładowy plik konfiguracji sieci tworzy sieć wirtualną o nazwie *myVirtualNetwork* się na przestrzeń adresową z *10.0.0.0/16* w hello *wschodnie stany USA* Azure region.</span><span class="sxs-lookup"><span data-stu-id="a7772-144">hello following example network configuration file creates a virtual network named *myVirtualNetwork* with an address space of *10.0.0.0/16* in hello *East US* Azure region.</span></span> <span data-ttu-id="a7772-145">sieć wirtualna Hello zawiera jedną podsieć o nazwie *mySubnet* z prefiksem adresu o *10.0.0.0/24*.</span><span class="sxs-lookup"><span data-stu-id="a7772-145">hello virtual network contains one subnet named *mySubnet* with an address prefix of *10.0.0.0/24*.</span></span>

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

<span data-ttu-id="a7772-146">Plik konfiguracji sieci hello wyeksportowanymi zawiera zawartość nie, można skopiować hello json w poprzednim przykładzie hello i wklej go do nowego pliku.</span><span class="sxs-lookup"><span data-stu-id="a7772-146">If hello network configuration file you exported contains no contents, you can copy hello json in hello previous example, and paste it into a new file.</span></span>

## <span data-ttu-id="a7772-147"><a name="import"></a>Importowanie pliku konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="a7772-147"><a name="import"></a>Import a network configuration file</span></span>

<span data-ttu-id="a7772-148">Możesz użyć programu PowerShell lub hello Azure CLI tooimport pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="a7772-148">You can use PowerShell or hello Azure CLI tooimport a network configuration file.</span></span> <span data-ttu-id="a7772-149">PowerShell importuje plik XML, gdy hello Azure CLI importuje plik json.</span><span class="sxs-lookup"><span data-stu-id="a7772-149">PowerShell imports an XML file, while hello Azure CLI imports a json file.</span></span> <span data-ttu-id="a7772-150">Jeśli hello zakończyła się niepowodzeniem, upewnij się, czy plik hello jest zgodny z hello [schemat konfiguracji sieci](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7772-150">If hello import fails, confirm that hello file complies with hello [network configuration schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span> 

### <a name="powershell"></a><span data-ttu-id="a7772-151">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7772-151">PowerShell</span></span>
 
1. <span data-ttu-id="a7772-152">[Instalowanie programu Azure PowerShell i logowanie tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7772-152">[Install Azure PowerShell and sign in tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="a7772-153">Zmień katalog hello i nazwę pliku w hello następujące polecenie, w razie potrzeby, a następnie uruchom plik konfiguracji sieci tooimport hello hello polecenia:</span><span class="sxs-lookup"><span data-stu-id="a7772-153">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a><span data-ttu-id="a7772-154">Interfejs wiersza polecenia platformy Azure CLI w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="a7772-154">Azure CLI 1.0</span></span>

1. <span data-ttu-id="a7772-155">[Zainstaluj hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7772-155">[Install hello Azure CLI 1.0](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="a7772-156">Wykonaj pozostałe kroki w wierszu polecenia, Azure CLI 1.0 hello.</span><span class="sxs-lookup"><span data-stu-id="a7772-156">Complete hello remaining steps from an Azure CLI 1.0 command prompt.</span></span>
2. <span data-ttu-id="a7772-157">Zaloguj się za tooAzure wprowadzając hello `azure login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a7772-157">Log in tooAzure by entering hello `azure login` command.</span></span>
3. <span data-ttu-id="a7772-158">Upewnij się, jest w trybie asm wprowadzając hello `azure config mode asm` polecenia.</span><span class="sxs-lookup"><span data-stu-id="a7772-158">Ensure you're in asm mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="a7772-159">Zmień katalog hello i nazwę pliku w hello następujące polecenie, w razie potrzeby, a następnie uruchom plik konfiguracji sieci tooimport hello hello polecenia:</span><span class="sxs-lookup"><span data-stu-id="a7772-159">Change hello directory and filename in hello following command as necessary, then run hello command tooimport hello network configuration file:</span></span>

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```
