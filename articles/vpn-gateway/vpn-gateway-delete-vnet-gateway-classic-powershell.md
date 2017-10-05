---
title: "Usuwanie bramy sieci wirtualnej: środowiska PowerShell: klasyczny Portal Azure | Dokumentacja firmy Microsoft"
description: "Usuń bramę sieci wirtualnej w klasycznym modelu wdrażania przy użyciu programu PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="f37f0-103">Usuwanie bramy sieci wirtualnej przy użyciu programu PowerShell (klasyczne)</span><span class="sxs-lookup"><span data-stu-id="f37f0-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f37f0-104">Resource Manager — witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f37f0-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="f37f0-105">Resource Manager — program PowerShell</span><span class="sxs-lookup"><span data-stu-id="f37f0-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="f37f0-106">Classic — PowerShell</span><span class="sxs-lookup"><span data-stu-id="f37f0-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="f37f0-107">W tym artykule opisano, jak usunąć bramę sieci VPN w klasycznym modelu wdrażania przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f37f0-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="f37f0-108">Po usunięciu bramy sieci wirtualnej, zmodyfikuj plik konfiguracji sieci, aby usunąć elementy, które są już używane.</span><span class="sxs-lookup"><span data-stu-id="f37f0-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="f37f0-109"><a name="connect"></a>Krok 1: Połączenia z platformą Azure</span><span class="sxs-lookup"><span data-stu-id="f37f0-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="f37f0-110">1. Zainstaluj najnowsze poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f37f0-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="f37f0-111">Pobierz i zainstaluj najnowszą wersję poleceń cmdlet programu PowerShell Azure usługi zarządzania (ko).</span><span class="sxs-lookup"><span data-stu-id="f37f0-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="f37f0-112">Aby uzyskać więcej informacji, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f37f0-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="f37f0-113">2. Połącz z kontem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f37f0-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="f37f0-114">Otwórz konsolę programu PowerShell z podwyższonym poziomem uprawnień i połącz się ze swoim kontem.</span><span class="sxs-lookup"><span data-stu-id="f37f0-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="f37f0-115">Użyj poniższego przykładu w celu łatwiejszego nawiązania połączenia:</span><span class="sxs-lookup"><span data-stu-id="f37f0-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="f37f0-116"><a name="export"></a>Krok 2: Eksportowanie i wyświetlania pliku konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="f37f0-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="f37f0-117">Utwórz katalog na komputerze, a następnie wyeksportuj plik konfiguracji sieci do tego katalogu.</span><span class="sxs-lookup"><span data-stu-id="f37f0-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="f37f0-118">Możesz użyć tego pliku do obu widoku informacje o bieżącej konfiguracji, a także modyfikowanie konfiguracji sieciowej.</span><span class="sxs-lookup"><span data-stu-id="f37f0-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="f37f0-119">W tym przykładzie plik konfiguracji sieci zostanie wyeksportowany do katalogu C:\AzureNet.</span><span class="sxs-lookup"><span data-stu-id="f37f0-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="f37f0-120">Otwórz plik w edytorze tekstów i wyświetlić nazwę klasycznej sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f37f0-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="f37f0-121">Po utworzeniu sieci wirtualnej w portalu Azure, pełna nazwa, która używa usługi Azure nie jest widoczne w portalu.</span><span class="sxs-lookup"><span data-stu-id="f37f0-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="f37f0-122">Na przykład sieci wirtualnej, który wydaje się być o nazwie "ClassicVNet1" w portalu Azure może mieć wiele nazwę dłużej w pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="f37f0-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="f37f0-123">Nazwa może wyglądać mniej więcej tak: "ClassicVNet1 ClassicRG1 grupy".</span><span class="sxs-lookup"><span data-stu-id="f37f0-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="f37f0-124">Nazwy sieci wirtualnej są wyświetlane jako **"VirtualNetworkSite name ="**.</span><span class="sxs-lookup"><span data-stu-id="f37f0-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="f37f0-125">Podczas uruchamiania polecenia cmdlet programu PowerShell, użyj nazw w pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="f37f0-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="f37f0-126"><a name="delete"></a>Krok 3: Usuń bramę sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f37f0-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="f37f0-127">Po usunięciu bramy sieci wirtualnej zostały odłączone wszystkich połączeń do sieci wirtualnej za pośrednictwem bramy.</span><span class="sxs-lookup"><span data-stu-id="f37f0-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="f37f0-128">Jeśli masz P2S klientów podłączonych do sieci wirtualnej zostanie rozłączone bez ostrzeżenia.</span><span class="sxs-lookup"><span data-stu-id="f37f0-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="f37f0-129">W tym przykładzie usuwa bramę sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f37f0-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="f37f0-130">Upewnij się użyć pełnej nazwy sieci wirtualnej z pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="f37f0-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="f37f0-131">W przypadku powodzenia zwracany zawiera:</span><span class="sxs-lookup"><span data-stu-id="f37f0-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="f37f0-132"><a name="modify"></a>Krok 4: Modyfikowanie pliku konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="f37f0-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="f37f0-133">Podczas usuwania bramy sieci wirtualnej, polecenie cmdlet nie powoduje modyfikacji pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="f37f0-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="f37f0-134">Musisz zmodyfikować plik w celu usunięcia elementów, które są już używane.</span><span class="sxs-lookup"><span data-stu-id="f37f0-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="f37f0-135">Poniższe sekcje pomóc zmodyfikować pobranego pliku konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="f37f0-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="f37f0-136"><a name="lnsref"></a>Odwołania do lokacji sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="f37f0-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="f37f0-137">Aby usunąć informacje o lokacji odniesienia, wprowadzić zmiany w konfiguracji **ConnectionsToLocalNetwork/elementu LocalNetworkSiteRef**.</span><span class="sxs-lookup"><span data-stu-id="f37f0-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="f37f0-138">Usuwanie wyzwalaczy odwołanie lokacji lokalnej platformy Azure, aby usunąć tunelu.</span><span class="sxs-lookup"><span data-stu-id="f37f0-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="f37f0-139">W zależności od konfiguracji, który został utworzony, nie masz **elementu LocalNetworkSiteRef** na liście.</span><span class="sxs-lookup"><span data-stu-id="f37f0-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="f37f0-140">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f37f0-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="f37f0-141"><a name="lns"></a>Lokacje sieci lokalnej</span><span class="sxs-lookup"><span data-stu-id="f37f0-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="f37f0-142">Usuń lokalnych witryn, które są już używane.</span><span class="sxs-lookup"><span data-stu-id="f37f0-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="f37f0-143">W zależności od konfiguracji został utworzony, jest możliwe, że nie masz **LocalNetworkSite** na liście.</span><span class="sxs-lookup"><span data-stu-id="f37f0-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="f37f0-144">W tym przykładzie firma Microsoft usunęła tylko Site3.</span><span class="sxs-lookup"><span data-stu-id="f37f0-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="f37f0-145"><a name="clientaddresss"></a>Pula adresów klienta</span><span class="sxs-lookup"><span data-stu-id="f37f0-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="f37f0-146">Jeśli zostały połączeń P2S sieci wirtualnej, konieczne będzie **VPNClientAddressPool**.</span><span class="sxs-lookup"><span data-stu-id="f37f0-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="f37f0-147">Usuń pule adresów klienta, odpowiadające bramy sieci wirtualnej, która została usunięta.</span><span class="sxs-lookup"><span data-stu-id="f37f0-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="f37f0-148">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f37f0-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="f37f0-149"><a name="gwsub"></a>GatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="f37f0-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="f37f0-150">Usuń **GatewaySubnet** odpowiadający sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f37f0-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="f37f0-151">Przykład:</span><span class="sxs-lookup"><span data-stu-id="f37f0-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="f37f0-152"><a name="upload"></a>Krok 5: Przekaż plik konfiguracji sieci</span><span class="sxs-lookup"><span data-stu-id="f37f0-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="f37f0-153">Zapisz zmiany i przekazać plik konfiguracji sieci na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f37f0-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="f37f0-154">Upewnij się, że w przypadku zmiany ścieżki pliku jako wymaganych w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="f37f0-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="f37f0-155">W przypadku powodzenia zwracany zawiera coś podobnego do tego przykładu:</span><span class="sxs-lookup"><span data-stu-id="f37f0-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded