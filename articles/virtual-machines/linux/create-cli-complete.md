---
title: "Utworzenie środowiska systemu Linux 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie magazynu, Maszynę wirtualną systemu Linux, sieci wirtualnej i podsieci, usługi równoważenia obciążenia, karty Sieciowej, publicznego adresu IP i sieciową grupę zabezpieczeń, wszystkie od podstaw przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/06/2017
ms.author: iainfou
ms.openlocfilehash: e5c4785428b2150e951923e98079e00808a82d87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="0722f-103">Utwórz pełną maszyny wirtualnej systemu Linux z wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0722f-103">Create a complete Linux virtual machine with the Azure CLI</span></span>
<span data-ttu-id="0722f-104">Aby szybko utworzyć maszynę wirtualną (VM) na platformie Azure, korzystając jednego polecenia interfejsu wiersza polecenia Azure, który można utworzyć wszelkie wymagane zasoby towarzyszące są używane wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="0722f-104">To quickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values to create any required supporting resources.</span></span> <span data-ttu-id="0722f-105">Zasoby, takie jak sieć wirtualną, publiczny adres IP i reguły grupy zabezpieczeń sieci są tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="0722f-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="0722f-106">Aby uzyskać większą kontrolę nad środowiskiem w środowisku produkcyjnym należy używać, może utworzyć te zasoby wcześniejsze i następnie dodać do nich maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0722f-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs to them.</span></span> <span data-ttu-id="0722f-107">W tym artykule prowadzi użytkownika przez proces tworzenia maszyny Wirtualnej i każdy z zasobów pomocniczych jeden po drugim.</span><span class="sxs-lookup"><span data-stu-id="0722f-107">This article guides you through how to create a VM and each of the supporting resources one by one.</span></span>

<span data-ttu-id="0722f-108">Upewnij się, że zainstalowano najnowszą [Azure CLI 2.0](/cli/azure/install-az-cli2) i logowania do konta platformy Azure przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0722f-108">Make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged to an Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0722f-109">W poniższych przykładach Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="0722f-109">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="0722f-110">Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="0722f-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="0722f-111">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="0722f-111">Create resource group</span></span>
<span data-ttu-id="0722f-112">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="0722f-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="0722f-113">Grupy zasobów musi zostać utworzone przed maszyny wirtualnej i dodatkowe zasoby sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0722f-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="0722f-114">Tworzenie grupy zasobów z [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0722f-114">Create the resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0722f-115">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="0722f-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0722f-116">Domyślnie dane wyjściowe polecenia wiersza polecenia platformy Azure jest w formacie JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="0722f-116">By default, the output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="0722f-117">Aby zmienić domyślne dane wyjściowe do listy lub tabeli, na przykład użyć [skonfigurować az — dane wyjściowe](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="0722f-117">To change the default output to a list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="0722f-118">Można również dodać `--output` do dowolnego polecenia jeden raz Zmień format danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0722f-118">You can also add `--output` to any command for a one time change in output format.</span></span> <span data-ttu-id="0722f-119">W poniższym przykładzie przedstawiono dane wyjściowe JSON `az group create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="0722f-119">The following example shows the JSON output from the `az group create` command:</span></span>

```json                       
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "location": "eastus",
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="0722f-120">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="0722f-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="0722f-121">Dalej przez tworzenie sieci wirtualnej platformy Azure i podsieci do której można utworzyć maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="0722f-121">Next you create a virtual network in Azure and a subnet in to which you can create your VMs.</span></span> <span data-ttu-id="0722f-122">Użyj [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create) można utworzyć sieci wirtualnej o nazwie *myVnet* z *192.168.0.0/16* prefiks adresu.</span><span class="sxs-lookup"><span data-stu-id="0722f-122">Use [az network vnet create](/cli/azure/network/vnet#create) to create a virtual network named *myVnet* with the *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="0722f-123">Możesz również dodać podsieć o nazwie *mySubnet* z prefiksem adresu o *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="0722f-123">You also add a subnet named *mySubnet* with the address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="0722f-124">Dane wyjściowe zawierają podsieci logicznie utworzone w sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="0722f-124">The output shows the subnet as logically created inside the virtual network:</span></span>

```json
{
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "location": "eastus",
  "name": "myVnet",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "ed62fd03-e9de-430b-84df-8a3b87cacdbb",
  "subnets": [
    {
      "addressPrefix": "192.168.1.0/24",
      "etag": "W/\"e95496fc-f417-426e-a4d8-c9e4d27fc2ee\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
      "ipConfigurations": null,
      "name": "mySubnet",
      "networkSecurityGroup": null,
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "resourceNavigationLinks": null,
      "routeTable": null
    }
  ],
  "tags": {},
  "type": "Microsoft.Network/virtualNetworks",
  "virtualNetworkPeerings": null
}
```


## <a name="create-a-public-ip-address"></a><span data-ttu-id="0722f-125">Tworzenie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="0722f-125">Create a public IP address</span></span>
<span data-ttu-id="0722f-126">Teraz Utwórzmy publiczny adres IP z [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="0722f-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="0722f-127">Ten publiczny adres IP umożliwia nawiązywanie połączenia z Internetu do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="0722f-127">This public IP address enables you to connect to your VMs from the Internet.</span></span> <span data-ttu-id="0722f-128">Ponieważ domyślnym adresem jest dynamiczny, utworzymy również nazwanego wpisu DNS z `--domain-name-label` opcji.</span><span class="sxs-lookup"><span data-stu-id="0722f-128">Because the default address is dynamic, we also create a named DNS entry with the `--domain-name-label` option.</span></span> <span data-ttu-id="0722f-129">Poniższy przykład tworzy publicznego adresu IP o nazwie *myPublicIP* o nazwie DNS *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="0722f-129">The following example creates a public IP named *myPublicIP* with the DNS name of *mypublicdns*.</span></span> <span data-ttu-id="0722f-130">Ponieważ nazwy DNS musi być unikatowa, należy podać własną unikatową nazwę DNS:</span><span class="sxs-lookup"><span data-stu-id="0722f-130">Because the DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="0722f-131">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0722f-131">Output:</span></span>

```json
{
  "publicIp": {
    "dnsSettings": {
      "domainNameLabel": "mypublicdns",
      "fqdn": "mypublicdns.eastus.cloudapp.azure.com",
      "reverseFqdn": null
    },
    "etag": "W/\"2632aa72-3d2d-4529-b38e-b622b4202925\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "idleTimeoutInMinutes": 4,
    "ipAddress": null,
    "ipConfiguration": null,
    "location": "eastus",
    "name": "myPublicIP",
    "provisioningState": "Succeeded",
    "publicIpAddressVersion": "IPv4",
    "publicIpAllocationMethod": "Dynamic",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "4c65de38-71f5-4684-be10-75e605b3e41f",
    "tags": null,
    "type": "Microsoft.Network/publicIPAddresses"
  }
}
```


## <a name="create-a-network-security-group"></a><span data-ttu-id="0722f-132">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="0722f-132">Create a network security group</span></span>
<span data-ttu-id="0722f-133">Sterowanie przepływem ruchu do i z maszyn wirtualnych, należy utworzyć grupę zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="0722f-133">To control the flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="0722f-134">Grupa zabezpieczeń sieci może odnosić się do karty Sieciowej lub podsieci.</span><span class="sxs-lookup"><span data-stu-id="0722f-134">A network security group can be applied to a NIC or subnet.</span></span> <span data-ttu-id="0722f-135">W poniższym przykładzie użyto [utworzyć nsg sieci az](/cli/azure/network/nsg#create) utworzyć sieciowej grupy zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="0722f-135">The following example uses [az network nsg create](/cli/azure/network/nsg#create) to create a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="0722f-136">Można zdefiniować reguły, które akceptować lub odrzucać określonego ruchu.</span><span class="sxs-lookup"><span data-stu-id="0722f-136">You define rules that allow or deny the specific traffic.</span></span> <span data-ttu-id="0722f-137">Aby zezwolić na połączenia przychodzące do portu 22 (do obsługi protokołu SSH), należy utworzyć regułę ruchu przychodzącego dla sieciowej grupy zabezpieczeń z [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="0722f-137">To allow inbound connections on port 22 (to support SSH), create an inbound rule for the network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="0722f-138">Poniższy przykład tworzy reguły o nazwie *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="0722f-138">The following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 22 \
    --access allow
```

<span data-ttu-id="0722f-139">Aby zezwolić na połączenia przychodzące na porcie 80 (dla obsługi ruchu w sieci web), Dodaj inną regułę grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="0722f-139">To allow inbound connections on port 80 (to support web traffic), add another network security group rule.</span></span> <span data-ttu-id="0722f-140">Poniższy przykład tworzy reguły o nazwie *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="0722f-140">The following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleWeb \
    --protocol tcp \
    --priority 1001 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="0722f-141">Sprawdź, czy grupy zabezpieczeń sieci i reguły z [Pokaż nsg sieci az](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="0722f-141">Examine the network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="0722f-142">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0722f-142">Output:</span></span>

```json
{
  "defaultSecurityRules": [
    {
      "access": "Allow",
      "description": "Allow inbound traffic from all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetInBound",
      "name": "AllowVnetInBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow inbound traffic from azure load balancer",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowAzureLoadBalancerInBou
      "name": "AllowAzureLoadBalancerInBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "AzureLoadBalancer",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all inbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Inbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllInBound",
      "name": "DenyAllInBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to all VMs in VNET",
      "destinationAddressPrefix": "VirtualNetwork",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowVnetOutBound",
      "name": "AllowVnetOutBound",
      "priority": 65000,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "VirtualNetwork",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": "Allow outbound traffic from all VMs to Internet",
      "destinationAddressPrefix": "Internet",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/AllowInternetOutBound",
      "name": "AllowInternetOutBound",
      "priority": 65001,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Deny",
      "description": "Deny all outbound traffic",
      "destinationAddressPrefix": "*",
      "destinationPortRange": "*",
      "direction": "Outbound",
      "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/defaultSecurityRules/DenyAllOutBound",
      "name": "DenyAllOutBound",
      "priority": 65500,
      "protocol": "*",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "etag": "W/\"3371b313-ea9f-4687-a336-a8ebdfd80523\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
  "location": "eastus",
  "name": "myNetworkSecurityGroup",
  "networkInterfaces": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "resourceGuid": "47a9964e-23a3-438a-a726-8d60ebbb1c3c",
  "securityRules": [
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "22",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleSSH",
      "name": "myNetworkSecurityGroupRuleSSH",
      "priority": 1000,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    },
    {
      "access": "Allow",
      "description": null,
      "destinationAddressPrefix": "*",
      "destinationPortRange": "80",
      "direction": "Inbound",
      "etag": "W/\"9e344b60-0daa-40a6-84f9-0ebbe4a4b640\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup/securityRules/myNetworkSecurityGroupRuleWeb",
      "name": "myNetworkSecurityGroupRuleWeb",
      "priority": 1001,
      "protocol": "Tcp",
      "provisioningState": "Succeeded",
      "resourceGroup": "myResourceGroup",
      "sourceAddressPrefix": "*",
      "sourcePortRange": "*"
    }
  ],
  "subnets": null,
  "tags": null,
  "type": "Microsoft.Network/networkSecurityGroups"
}
```

## <a name="create-a-virtual-nic"></a><span data-ttu-id="0722f-143">Tworzenie wirtualnej karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="0722f-143">Create a virtual NIC</span></span>
<span data-ttu-id="0722f-144">Wirtualne karty sieciowe (NIC) są programowo dostępne, ponieważ reguły można stosować do ich używania.</span><span class="sxs-lookup"><span data-stu-id="0722f-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules to their use.</span></span> <span data-ttu-id="0722f-145">Może także zawierać więcej niż jeden.</span><span class="sxs-lookup"><span data-stu-id="0722f-145">You can also have more than one.</span></span> <span data-ttu-id="0722f-146">W następujących [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create) polecenia Utwórz karty Sieciowej o nazwie *myNic* i skojarzyć go z grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="0722f-146">In the following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with the network security group.</span></span> <span data-ttu-id="0722f-147">Publiczny adres IP *myPublicIP* jest także powiązany z wirtualnej karty sieciowej.</span><span class="sxs-lookup"><span data-stu-id="0722f-147">The public IP address *myPublicIP* is also associated with the virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="0722f-148">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0722f-148">Output:</span></span>

```json
{
  "NewNIC": {
    "dnsSettings": {
      "appliedDnsServers": [],
      "dnsServers": [],
      "internalDnsNameLabel": null,
      "internalDomainNameSuffix": "brqlt10lvoxedgkeuomc4pm5tb.bx.internal.cloudapp.net",
      "internalFqdn": null
    },
    "enableAcceleratedNetworking": false,
    "enableIpForwarding": false,
    "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic",
    "ipConfigurations": [
      {
        "applicationGatewayBackendAddressPools": null,
        "etag": "W/\"04b5ab44-d8f4-422a-9541-e5ae7de8466d\"",
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic/ipConfigurations/ipconfig1",
        "loadBalancerBackendAddressPools": null,
        "loadBalancerInboundNatRules": null,
        "name": "ipconfig1",
        "primary": true,
        "privateIpAddress": "192.168.1.4",
        "privateIpAddressVersion": "IPv4",
        "privateIpAllocationMethod": "Dynamic",
        "provisioningState": "Succeeded",
        "publicIpAddress": {
          "dnsSettings": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
          "idleTimeoutInMinutes": null,
          "ipAddress": null,
          "ipConfiguration": null,
          "location": null,
          "name": null,
          "provisioningState": null,
          "publicIpAddressVersion": null,
          "publicIpAllocationMethod": null,
          "resourceGroup": "myResourceGroup",
          "resourceGuid": null,
          "tags": null,
          "type": null
        },
        "resourceGroup": "myResourceGroup",
        "subnet": {
          "addressPrefix": null,
          "etag": null,
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet",
          "ipConfigurations": null,
          "name": null,
          "networkSecurityGroup": null,
          "provisioningState": null,
          "resourceGroup": "myResourceGroup",
          "resourceNavigationLinks": null,
          "routeTable": null
        }
      }
    ],
    "location": "eastus",
    "macAddress": null,
    "name": "myNic",
    "networkSecurityGroup": {
      "defaultSecurityRules": null,
      "etag": null,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myNetworkSecurityGroup",
      "location": null,
      "name": null,
      "networkInterfaces": null,
      "provisioningState": null,
      "resourceGroup": "myResourceGroup",
      "resourceGuid": null,
      "securityRules": null,
      "subnets": null,
      "tags": null,
      "type": null
    },
    "primary": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "myResourceGroup",
    "resourceGuid": "b3dbaa0e-2cf2-43be-a814-5cc49fea3304",
    "tags": null,
    "type": "Microsoft.Network/networkInterfaces",
    "virtualMachine": null
  }
}
```


## <a name="create-an-availability-set"></a><span data-ttu-id="0722f-149">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="0722f-149">Create an availability set</span></span>
<span data-ttu-id="0722f-150">Zestawy dostępności rozpowszechniania pomocy maszyn wirtualnych w domenach awarii i Aktualizacja domeny.</span><span class="sxs-lookup"><span data-stu-id="0722f-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="0722f-151">Mimo że można utworzyć tylko jedną maszynę Wirtualną od razu, jest najlepszym rozwiązaniem jest użycie zestawów dostępności, aby ułatwić w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="0722f-151">Even though you only create one VM right now, it's best practice to use availability sets to make it easier to expand in the future.</span></span> 

<span data-ttu-id="0722f-152">Domen błędów Definiowanie grup maszyn wirtualnych, które współużytkują wspólne przełącznik źródła i sieci zasilania.</span><span class="sxs-lookup"><span data-stu-id="0722f-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="0722f-153">Domyślnie maszyny wirtualne, które są skonfigurowane w zestawie dostępności są rozdzielone przez maksymalnie trzy domen błędów.</span><span class="sxs-lookup"><span data-stu-id="0722f-153">By default, the virtual machines that are configured within your availability set are separated across up to three fault domains.</span></span> <span data-ttu-id="0722f-154">Problemem sprzętowym w jednym z tych domen błędów nie ma wpływu na każdej maszynie Wirtualnej, która jest uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="0722f-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="0722f-155">Aktualizacja domen wskazują grupy maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać uruchomiony ponownie w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="0722f-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="0722f-156">Podczas zaplanowanej konserwacji kolejności w aktualizacji, które są ponownie uruchamiane domen mogą nie być sekwencyjnych, ale tylko jedna aktualizacja domeny ponownego uruchomienia w czasie.</span><span class="sxs-lookup"><span data-stu-id="0722f-156">During planned maintenance, the order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="0722f-157">Azure automatycznie dystrybuuje maszyn wirtualnych w domenach awarii i aktualizacji podczas umieszczania ich w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="0722f-157">Azure automatically distributes VMs across the fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="0722f-158">Aby uzyskać więcej informacji, zobacz [Zarządzanie dostępność maszyn wirtualnych](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="0722f-158">For more information, see [managing the availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="0722f-159">Utwórz zbiór dostępności dla maszyny Wirtualnej z [tworzenia maszyny wirtualnej az zestawu dostępności](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="0722f-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="0722f-160">Poniższy przykład tworzy zbiór nazwanego dostępności *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="0722f-160">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="0722f-161">Domen błędów wyjścia uwagi i domen aktualizacji:</span><span class="sxs-lookup"><span data-stu-id="0722f-161">The output notes fault domains and update domains:</span></span>

```json
{
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet",
  "location": "eastus",
  "managed": null,
  "name": "myAvailabilitySet",
  "platformFaultDomainCount": 2,
  "platformUpdateDomainCount": 5,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": null,
    "managed": true,
    "tier": null
  },
  "statuses": null,
  "tags": {},
  "type": "Microsoft.Compute/availabilitySets",
  "virtualMachines": []
}
```


## <a name="create-the-linux-vms"></a><span data-ttu-id="0722f-162">Tworzenie maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="0722f-162">Create the Linux VMs</span></span>
<span data-ttu-id="0722f-163">Po utworzeniu zasobów sieciowych do obsługi maszyn wirtualnych dostęp do Internetu.</span><span class="sxs-lookup"><span data-stu-id="0722f-163">You've created the network resources to support Internet-accessible VMs.</span></span> <span data-ttu-id="0722f-164">Teraz Utwórz maszynę Wirtualną i zabezpiecz ją przy użyciu klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="0722f-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="0722f-165">W takim przypadku zamierzamy utworzyć Ubuntu oparte na najnowszych LTS maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0722f-165">In this case, we're going to create an Ubuntu VM based on the most recent LTS.</span></span> <span data-ttu-id="0722f-166">Można znaleźć dodatkowe obrazy z [listy obrazów maszyny wirtualnej az](/cli/azure/vm/image#list), zgodnie z opisem w [znajdowanie obrazów maszyn wirtualnych Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="0722f-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="0722f-167">Możemy również określić klucza SSH do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0722f-167">We also specify an SSH key to use for authentication.</span></span> <span data-ttu-id="0722f-168">Jeśli nie masz pary kluczy publicznych SSH, możesz [je utworzyć](mac-create-ssh-keys.md) lub użyj `--generate-ssh-keys` parametr, aby je utworzyć automatycznie.</span><span class="sxs-lookup"><span data-stu-id="0722f-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use the `--generate-ssh-keys` parameter to create them for you.</span></span> <span data-ttu-id="0722f-169">Jeśli możesz już parę kluczy, ten parametr wykorzystuje istniejące klucze w `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="0722f-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="0722f-170">Tworzenie maszyny Wirtualnej, przełączając naszych zasobów i informacji razem z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0722f-170">Create the VM by bringing all our resources and information together with the [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="0722f-171">Poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="0722f-171">The following example creates a VM named *myVM*:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --availability-set myAvailabilitySet \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="0722f-172">SSH do maszyny Wirtualnej z wpisu DNS podany podczas tworzenia publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="0722f-172">SSH to your VM with the DNS entry you provided when you created the public IP address.</span></span> <span data-ttu-id="0722f-173">To `fqdn` jest wyświetlany w danych wyjściowych podczas tworzenia maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="0722f-173">This `fqdn` is shown in the output as you create your VM:</span></span>

```json
{
  "fqdns": "mypublicdns.eastus.cloudapp.azure.com",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-13-71-C8",
  "powerState": "VM running",
  "privateIpAddress": "192.168.1.5",
  "publicIpAddress": "13.90.94.252",
  "resourceGroup": "myResourceGroup"
}
```

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="0722f-174">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="0722f-174">Output:</span></span>

```bash
The authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) to the list of known hosts.
Welcome to Ubuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="0722f-175">Można zainstalować NGINX i widoczne ruchu przepływu do maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0722f-175">You can install NGINX and see the traffic flow to the VM.</span></span> <span data-ttu-id="0722f-176">Zainstaluj NGINX w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0722f-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="0722f-177">Aby wyświetlić NGINX domyślnej witryny w akcji, otwórz przeglądarkę sieci web i wprowadzić swoją nazwę FQDN:</span><span class="sxs-lookup"><span data-stu-id="0722f-177">To see the default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Domyślna witryna NGINX na maszynie Wirtualnej](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="0722f-179">Eksportowanie jako szablon</span><span class="sxs-lookup"><span data-stu-id="0722f-179">Export as a template</span></span>
<span data-ttu-id="0722f-180">Co zrobić, jeśli chcesz teraz Utwórz środowisko rozwoju dodatkowych z takimi samymi parametrami lub w środowisku produkcyjnym, które odpowiadają go?</span><span class="sxs-lookup"><span data-stu-id="0722f-180">What if you now want to create an additional development environment with the same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="0722f-181">Menedżer zasobów używa szablony JSON, które definiują wszystkie parametry dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="0722f-181">Resource Manager uses JSON templates that define all the parameters for your environment.</span></span> <span data-ttu-id="0722f-182">Limit całego środowiska kompilacji, umieszczając odwołanie do tego szablonu JSON.</span><span class="sxs-lookup"><span data-stu-id="0722f-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="0722f-183">Możesz [ręcznie utworzyć szablony JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub wyeksportować utworzenie szablonu JSON do istniejącego środowiska.</span><span class="sxs-lookup"><span data-stu-id="0722f-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment to create the JSON template for you.</span></span> <span data-ttu-id="0722f-184">Użyj [eksportowanie grupy az](/cli/azure/group#export) Aby wyeksportować grupy zasobów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0722f-184">Use [az group export](/cli/azure/group#export) to export your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="0722f-185">To polecenie tworzy `myResourceGroup.json` plik w bieżącym katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="0722f-185">This command creates the `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="0722f-186">Podczas tworzenia środowiska z tego szablonu, wyświetlany jest monit dla nazw zasobów.</span><span class="sxs-lookup"><span data-stu-id="0722f-186">When you create an environment from this template, you are prompted for all the resource names.</span></span> <span data-ttu-id="0722f-187">Można go wypełnić te nazwy w pliku szablonu, dodając `--include-parameter-default-value` parametr `az group export` polecenia.</span><span class="sxs-lookup"><span data-stu-id="0722f-187">You can populate these names in your template file by adding the `--include-parameter-default-value` parameter to the `az group export` command.</span></span> <span data-ttu-id="0722f-188">Edytuj szablon JSON można określić nazwy zasobu lub [Tworzenie pliku parameters.JSON następującym kodem](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , który określa nazwy zasobu.</span><span class="sxs-lookup"><span data-stu-id="0722f-188">Edit your JSON template to specify the resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies the resource names.</span></span>

<span data-ttu-id="0722f-189">Aby utworzyć środowisko z szablonu, należy użyć [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0722f-189">To create an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="0722f-190">Warto przeczytać [więcej informacji na temat sposobu wdrażania z szablonów](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0722f-190">You might want to read [more about how to deploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0722f-191">Więcej informacji na temat sposobu przyrostowo aktualizacja środowisk, użyj pliku parametrów i dostępu do szablonów z lokalizacji magazynu jednego.</span><span class="sxs-lookup"><span data-stu-id="0722f-191">Learn about how to incrementally update environments, use the parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0722f-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0722f-192">Next steps</span></span>
<span data-ttu-id="0722f-193">Teraz możesz przystąpić do rozpoczęcia pracy z wieloma składnikami sieciowymi i maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="0722f-193">Now you're ready to begin working with multiple networking components and VMs.</span></span> <span data-ttu-id="0722f-194">To środowisko próbki służy do tworzenia aplikacji przy użyciu podstawowe składniki wprowadzone w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="0722f-194">You can use this sample environment to build out your application by using the core components introduced here.</span></span>
