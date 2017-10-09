---
title: "aaaCreate środowiska Linux z hello Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "Tworzenie magazynu, Maszynę wirtualną systemu Linux, sieci wirtualnej i podsieci, usługi równoważenia obciążenia, karty Sieciowej, publicznego adresu IP i sieciową grupę zabezpieczeń, z hello tła przy użyciu hello Azure CLI 2.0."
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
ms.openlocfilehash: 7287ea178e76001b84dade628ead04a59dc27f40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="c89a1-103">Utwórz pełną maszyny wirtualnej systemu Linux z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c89a1-103">Create a complete Linux virtual machine with hello Azure CLI</span></span>
<span data-ttu-id="c89a1-104">tooquickly Utwórz maszynę wirtualną (VM) na platformie Azure, możesz użyć jednego polecenia wiersza polecenia platformy Azure, który używa domyślnej wartości toocreate wymagane zasoby obsługi.</span><span class="sxs-lookup"><span data-stu-id="c89a1-104">tooquickly create a virtual machine (VM) in Azure, you can use a single Azure CLI command that uses default values toocreate any required supporting resources.</span></span> <span data-ttu-id="c89a1-105">Zasoby, takie jak sieć wirtualną, publiczny adres IP i reguły grupy zabezpieczeń sieci są tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c89a1-105">Resources such as a virtual network, public IP address, and network security group rules are automatically created.</span></span> <span data-ttu-id="c89a1-106">Aby uzyskać większą kontrolę nad środowiskiem w środowisku produkcyjnym należy używać, może utworzyć te zasoby wcześniejsze, a następnie dodać toothem sieci maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c89a1-106">For more control of your environment in production use, you may create these resources ahead of time and then add your VMs toothem.</span></span> <span data-ttu-id="c89a1-107">Ten artykuł przeprowadzi Cię przez jak toocreate maszyny Wirtualnej, a każde z hello pomocnicze zasoby jeden po drugim.</span><span class="sxs-lookup"><span data-stu-id="c89a1-107">This article guides you through how toocreate a VM and each of hello supporting resources one by one.</span></span>

<span data-ttu-id="c89a1-108">Upewnij się, czy hello zostały zainstalowane najnowsze [Azure CLI 2.0](/cli/azure/install-az-cli2) i zarejestrowane tooan Azure konta przy użyciu [logowania az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c89a1-108">Make sure that you have installed hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and logged tooan Azure account in with [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c89a1-109">Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości.</span><span class="sxs-lookup"><span data-stu-id="c89a1-109">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c89a1-110">Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.</span><span class="sxs-lookup"><span data-stu-id="c89a1-110">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="c89a1-111">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="c89a1-111">Create resource group</span></span>
<span data-ttu-id="c89a1-112">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="c89a1-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="c89a1-113">Grupy zasobów musi zostać utworzone przed maszyny wirtualnej i dodatkowe zasoby sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c89a1-113">A resource group must be created before a virtual machine and supporting virtual network resources.</span></span> <span data-ttu-id="c89a1-114">Utwórz grupę zasobów hello z [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c89a1-114">Create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c89a1-115">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="c89a1-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="c89a1-116">Domyślnie dane wyjściowe polecenia interfejsu wiersza polecenia Azure hello jest w formacie JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="c89a1-116">By default, hello output of Azure CLI commands is in JSON (JavaScript Object Notation).</span></span> <span data-ttu-id="c89a1-117">toochange hello domyślnego wyjścia tooa listy lub tabeli, na przykład użyć [skonfigurować az — dane wyjściowe](/cli/azure/#configure).</span><span class="sxs-lookup"><span data-stu-id="c89a1-117">toochange hello default output tooa list or table, for example, use [az configure --output](/cli/azure/#configure).</span></span> <span data-ttu-id="c89a1-118">Można również dodać `--output` tooany polecenia jeden raz, Zmień format danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="c89a1-118">You can also add `--output` tooany command for a one time change in output format.</span></span> <span data-ttu-id="c89a1-119">Witaj poniższy przykład przedstawia dane wyjściowe JSON hello hello `az group create` polecenia:</span><span class="sxs-lookup"><span data-stu-id="c89a1-119">hello following example shows hello JSON output from hello `az group create` command:</span></span>

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

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="c89a1-120">Tworzenie sieci wirtualnej i podsieci</span><span class="sxs-lookup"><span data-stu-id="c89a1-120">Create a virtual network and subnet</span></span>
<span data-ttu-id="c89a1-121">Następnie utwórz sieć wirtualną na platformie Azure i podsieci toowhich można tworzyć maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c89a1-121">Next you create a virtual network in Azure and a subnet in toowhich you can create your VMs.</span></span> <span data-ttu-id="c89a1-122">Użyj [tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create) toocreate sieć wirtualną o nazwie *myVnet* z hello *192.168.0.0/16* prefiks adresu.</span><span class="sxs-lookup"><span data-stu-id="c89a1-122">Use [az network vnet create](/cli/azure/network/vnet#create) toocreate a virtual network named *myVnet* with hello *192.168.0.0/16* address prefix.</span></span> <span data-ttu-id="c89a1-123">Możesz również dodać podsieć o nazwie *mySubnet* z prefiksu adresu hello *192.168.1.0/24*:</span><span class="sxs-lookup"><span data-stu-id="c89a1-123">You also add a subnet named *mySubnet* with hello address prefix of *192.168.1.0/24*:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

<span data-ttu-id="c89a1-124">dane wyjściowe Hello zawierają hello podsieci logicznie utworzonego w sieci wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="c89a1-124">hello output shows hello subnet as logically created inside hello virtual network:</span></span>

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


## <a name="create-a-public-ip-address"></a><span data-ttu-id="c89a1-125">Tworzenie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="c89a1-125">Create a public IP address</span></span>
<span data-ttu-id="c89a1-126">Teraz Utwórzmy publiczny adres IP z [utworzyć az sieci publicznej ip](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="c89a1-126">Now let's create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="c89a1-127">Ten publiczny adres IP umożliwia możesz tooconnect tooyour maszyn wirtualnych z hello Internet.</span><span class="sxs-lookup"><span data-stu-id="c89a1-127">This public IP address enables you tooconnect tooyour VMs from hello Internet.</span></span> <span data-ttu-id="c89a1-128">Ponieważ hello domyślnym adresem jest dynamiczny, będziemy również utworzyć nazwanego wpisu DNS o hello `--domain-name-label` opcji.</span><span class="sxs-lookup"><span data-stu-id="c89a1-128">Because hello default address is dynamic, we also create a named DNS entry with hello `--domain-name-label` option.</span></span> <span data-ttu-id="c89a1-129">Witaj poniższy przykład tworzy publicznego adresu IP o nazwie *myPublicIP* o nazwie DNS hello *mypublicdns*.</span><span class="sxs-lookup"><span data-stu-id="c89a1-129">hello following example creates a public IP named *myPublicIP* with hello DNS name of *mypublicdns*.</span></span> <span data-ttu-id="c89a1-130">Ponieważ nazwy DNS hello musi być unikatowa, należy podać własną unikatową nazwę DNS:</span><span class="sxs-lookup"><span data-stu-id="c89a1-130">Because hello DNS name must be unique, provide your own unique DNS name:</span></span>

```azurecli
az network public-ip create \
    --resource-group myResourceGroup \
    --name myPublicIP \
    --dns-name mypublicdns
```

<span data-ttu-id="c89a1-131">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c89a1-131">Output:</span></span>

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


## <a name="create-a-network-security-group"></a><span data-ttu-id="c89a1-132">Utwórz grupę zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="c89a1-132">Create a network security group</span></span>
<span data-ttu-id="c89a1-133">Przepływ hello toocontrol ruch do i z maszyn wirtualnych, Utwórz grupę zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="c89a1-133">toocontrol hello flow of traffic in and out of your VMs, create a network security group.</span></span> <span data-ttu-id="c89a1-134">Grupa zabezpieczeń sieci może być zastosowane tooa karty Sieciowej lub podsieci.</span><span class="sxs-lookup"><span data-stu-id="c89a1-134">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="c89a1-135">Witaj poniższym przykładzie użyto [utworzyć nsg sieci az](/cli/azure/network/nsg#create) toocreate sieciową grupę zabezpieczeń o nazwie *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="c89a1-135">hello following example uses [az network nsg create](/cli/azure/network/nsg#create) toocreate a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="c89a1-136">Można zdefiniować reguły, które akceptować lub odrzucać hello określonego ruchu.</span><span class="sxs-lookup"><span data-stu-id="c89a1-136">You define rules that allow or deny hello specific traffic.</span></span> <span data-ttu-id="c89a1-137">tooallow połączenia przychodzące do portu 22 (toosupport SSH), Utwórz regułę ruchu przychodzącego dla sieciowej grupy zabezpieczeń z hello [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="c89a1-137">tooallow inbound connections on port 22 (toosupport SSH), create an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="c89a1-138">Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRuleSSH*:</span><span class="sxs-lookup"><span data-stu-id="c89a1-138">hello following example creates a rule named *myNetworkSecurityGroupRuleSSH*:</span></span>

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

<span data-ttu-id="c89a1-139">tooallow połączeń przychodzących na porcie 80 (ruchu w sieci web toosupport), Dodaj inną regułę grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="c89a1-139">tooallow inbound connections on port 80 (toosupport web traffic), add another network security group rule.</span></span> <span data-ttu-id="c89a1-140">Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myNetworkSecurityGroupRuleHTTP*:</span><span class="sxs-lookup"><span data-stu-id="c89a1-140">hello following example creates a rule named *myNetworkSecurityGroupRuleHTTP*:</span></span>

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

<span data-ttu-id="c89a1-141">Sprawdź, czy hello sieciowej grupy zabezpieczeń i reguły z [Pokaż nsg sieci az](/cli/azure/network/nsg#show):</span><span class="sxs-lookup"><span data-stu-id="c89a1-141">Examine hello network security group and rules with [az network nsg show](/cli/azure/network/nsg#show):</span></span>

```azurecli
az network nsg show --resource-group myResourceGroup --name myNetworkSecurityGroup
```

<span data-ttu-id="c89a1-142">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c89a1-142">Output:</span></span>

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
      "description": "Allow outbound traffic from all VMs tooall VMs in VNET",
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
      "description": "Allow outbound traffic from all VMs tooInternet",
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

## <a name="create-a-virtual-nic"></a><span data-ttu-id="c89a1-143">Tworzenie wirtualnej karty Sieciowej</span><span class="sxs-lookup"><span data-stu-id="c89a1-143">Create a virtual NIC</span></span>
<span data-ttu-id="c89a1-144">Wirtualne karty sieciowe (NIC) są programowo dostępne, ponieważ możesz zastosować zasady tootheir użycia.</span><span class="sxs-lookup"><span data-stu-id="c89a1-144">Virtual network interface cards (NICs) are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="c89a1-145">Może także zawierać więcej niż jeden.</span><span class="sxs-lookup"><span data-stu-id="c89a1-145">You can also have more than one.</span></span> <span data-ttu-id="c89a1-146">W następujących hello [tworzenie kart interfejsu sieciowego az](/cli/azure/network/nic#create) polecenia Utwórz karty Sieciowej o nazwie *myNic* i powiązać ją z hello sieciowej grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c89a1-146">In hello following [az network nic create](/cli/azure/network/nic#create) command, you create a NIC named *myNic* and associate it with hello network security group.</span></span> <span data-ttu-id="c89a1-147">Witaj publicznego adresu IP *myPublicIP* jest także powiązany z hello wirtualnych kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="c89a1-147">hello public IP address *myPublicIP* is also associated with hello virtual NIC.</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --public-ip-address myPublicIP \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="c89a1-148">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c89a1-148">Output:</span></span>

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


## <a name="create-an-availability-set"></a><span data-ttu-id="c89a1-149">Tworzenie zestawu dostępności</span><span class="sxs-lookup"><span data-stu-id="c89a1-149">Create an availability set</span></span>
<span data-ttu-id="c89a1-150">Zestawy dostępności rozpowszechniania pomocy maszyn wirtualnych w domenach awarii i Aktualizacja domeny.</span><span class="sxs-lookup"><span data-stu-id="c89a1-150">Availability sets help spread your VMs across fault domains and update domains.</span></span> <span data-ttu-id="c89a1-151">Mimo że można utworzyć tylko jedną maszynę Wirtualną od razu, toomake zestawów dostępności toouse najlepszym rozwiązaniem jest ona łatwiej tooexpand w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="c89a1-151">Even though you only create one VM right now, it's best practice toouse availability sets toomake it easier tooexpand in hello future.</span></span> 

<span data-ttu-id="c89a1-152">Domen błędów Definiowanie grup maszyn wirtualnych, które współużytkują wspólne przełącznik źródła i sieci zasilania.</span><span class="sxs-lookup"><span data-stu-id="c89a1-152">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="c89a1-153">Domyślnie program hello maszyn wirtualnych, które są skonfigurowane w zestawie dostępności są rozdzielone przez się toothree domen błędów.</span><span class="sxs-lookup"><span data-stu-id="c89a1-153">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="c89a1-154">Problemem sprzętowym w jednym z tych domen błędów nie ma wpływu na każdej maszynie Wirtualnej, która jest uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="c89a1-154">A hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span>

<span data-ttu-id="c89a1-155">Aktualizacja domen wskazują grupy maszyn wirtualnych i podstawowym sprzętem fizycznym, który może zostać uruchomiony ponownie na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="c89a1-155">Update domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="c89a1-156">Podczas zaplanowanej konserwacji kolejności hello w aktualizacji, które są ponownie uruchamiane domen mogą nie być sekwencyjnych, ale tylko jedna aktualizacja domeny ponownego uruchomienia w czasie.</span><span class="sxs-lookup"><span data-stu-id="c89a1-156">During planned maintenance, hello order in which update domains are rebooted might not be sequential, but only one update domain is rebooted at a time.</span></span>

<span data-ttu-id="c89a1-157">Azure automatycznie dystrybuuje maszyn wirtualnych w domenach awarii i aktualizacji hello podczas umieszczania ich w zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="c89a1-157">Azure automatically distributes VMs across hello fault and update domains when placing them in an availability set.</span></span> <span data-ttu-id="c89a1-158">Aby uzyskać więcej informacji, zobacz [Zarządzanie hello dostępność maszyn wirtualnych](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="c89a1-158">For more information, see [managing hello availability of VMs](manage-availability.md).</span></span>

<span data-ttu-id="c89a1-159">Utwórz zbiór dostępności dla maszyny Wirtualnej z [tworzenia maszyny wirtualnej az zestawu dostępności](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="c89a1-159">Create an availability set for your VM with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="c89a1-160">Witaj poniższy przykład tworzy zbiór nazwanego dostępności *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="c89a1-160">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet
```

<span data-ttu-id="c89a1-161">Witaj domen błędów wyjścia uwagi i zaktualizuj domen:</span><span class="sxs-lookup"><span data-stu-id="c89a1-161">hello output notes fault domains and update domains:</span></span>

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


## <a name="create-hello-linux-vms"></a><span data-ttu-id="c89a1-162">Tworzenie maszyn wirtualnych systemu Linux hello</span><span class="sxs-lookup"><span data-stu-id="c89a1-162">Create hello Linux VMs</span></span>
<span data-ttu-id="c89a1-163">Po utworzeniu toosupport zasobów sieciowych hello dostępny z Internetu maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c89a1-163">You've created hello network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="c89a1-164">Teraz Utwórz maszynę Wirtualną i zabezpiecz ją przy użyciu klucza SSH.</span><span class="sxs-lookup"><span data-stu-id="c89a1-164">Now create a VM and secure it with an SSH key.</span></span> <span data-ttu-id="c89a1-165">W takim przypadku zamierzamy toocreate maszyny Wirtualnej systemu Ubuntu oparte na powitania najnowszych LTS.</span><span class="sxs-lookup"><span data-stu-id="c89a1-165">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="c89a1-166">Można znaleźć dodatkowe obrazy z [listy obrazów maszyny wirtualnej az](/cli/azure/vm/image#list), zgodnie z opisem w [znajdowanie obrazów maszyn wirtualnych Azure](cli-ps-findimage.md).</span><span class="sxs-lookup"><span data-stu-id="c89a1-166">You can find additional images with [az vm image list](/cli/azure/vm/image#list), as described in [finding Azure VM images](cli-ps-findimage.md).</span></span>

<span data-ttu-id="c89a1-167">Możemy również określić toouse klucza SSH do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="c89a1-167">We also specify an SSH key toouse for authentication.</span></span> <span data-ttu-id="c89a1-168">Jeśli nie masz pary kluczy publicznych SSH, możesz [je utworzyć](mac-create-ssh-keys.md) lub użyj hello `--generate-ssh-keys` toocreate parametru je automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c89a1-168">If you do not have an SSH public key pair, you can [create them](mac-create-ssh-keys.md) or use hello `--generate-ssh-keys` parameter toocreate them for you.</span></span> <span data-ttu-id="c89a1-169">Jeśli możesz już parę kluczy, ten parametr wykorzystuje istniejące klucze w `~/.ssh`.</span><span class="sxs-lookup"><span data-stu-id="c89a1-169">If you already a key pair, this parameter uses existing keys in `~/.ssh`.</span></span>

<span data-ttu-id="c89a1-170">Utwórz hello wirtualna przełączając naszych zasobów i informacji wraz z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="c89a1-170">Create hello VM by bringing all our resources and information together with hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="c89a1-171">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*:</span><span class="sxs-lookup"><span data-stu-id="c89a1-171">hello following example creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="c89a1-172">Tooyour SSH maszyny Wirtualnej z hello wpisu DNS, dostępne podczas tworzenia hello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="c89a1-172">SSH tooyour VM with hello DNS entry you provided when you created hello public IP address.</span></span> <span data-ttu-id="c89a1-173">To `fqdn` jest wyświetlany w danych wyjściowych hello podczas tworzenia maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="c89a1-173">This `fqdn` is shown in hello output as you create your VM:</span></span>

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

<span data-ttu-id="c89a1-174">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="c89a1-174">Output:</span></span>

```bash
hello authenticity of host 'mypublicdns.eastus.cloudapp.azure.com (13.90.94.252)' can't be established.
ECDSA key fingerprint is SHA256:SylINP80Um6XRTvWiFaNz+H+1jcrKB1IiNgCDDJRj6A.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added 'mypublicdns.eastus.cloudapp.azure.com,13.90.94.252' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.2 LTS (GNU/Linux 4.4.0-81-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.


hello programs included with hello Ubuntu system are free software;
hello exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, toohello extent permitted by
applicable law.

toorun a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

azureuser@myVM:~$
```

<span data-ttu-id="c89a1-175">Można zainstalować NGINX i zobacz toohello przepływu ruchu hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c89a1-175">You can install NGINX and see hello traffic flow toohello VM.</span></span> <span data-ttu-id="c89a1-176">Zainstaluj NGINX w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c89a1-176">Install NGINX as follows:</span></span>

```bash
sudo apt-get install -y nginx
```

<span data-ttu-id="c89a1-177">toosee hello domyślnej NGINX witryny akcji, otwórz przeglądarkę sieci web i wprowadź nazwę FQDN:</span><span class="sxs-lookup"><span data-stu-id="c89a1-177">toosee hello default NGINX site in action, open your web browser and enter your FQDN:</span></span>

![Domyślna witryna NGINX na maszynie Wirtualnej](media/create-cli-complete/nginx.png)

## <a name="export-as-a-template"></a><span data-ttu-id="c89a1-179">Eksportowanie jako szablon</span><span class="sxs-lookup"><span data-stu-id="c89a1-179">Export as a template</span></span>
<span data-ttu-id="c89a1-180">Co zrobić, jeśli teraz ma toocreate dodatkowe środowiska hello takie same parametry lub w środowisku produkcyjnym, odpowiadający jej?</span><span class="sxs-lookup"><span data-stu-id="c89a1-180">What if you now want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="c89a1-181">Menedżer zasobów używa szablony JSON, definiują wszystkie parametry hello w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="c89a1-181">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="c89a1-182">Limit całego środowiska kompilacji, umieszczając odwołanie do tego szablonu JSON.</span><span class="sxs-lookup"><span data-stu-id="c89a1-182">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="c89a1-183">Możesz [ręcznie utworzyć szablony JSON](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub wyeksportować istniejącego środowiska toocreate hello JSON szablonu dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="c89a1-183">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you.</span></span> <span data-ttu-id="c89a1-184">Użyj [eksportowanie grupy az](/cli/azure/group#export) tooexport zasób grupy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c89a1-184">Use [az group export](/cli/azure/group#export) tooexport your resource group as follows:</span></span>

```azurecli
az group export --name myResourceGroup > myResourceGroup.json
```

<span data-ttu-id="c89a1-185">To polecenie tworzy hello `myResourceGroup.json` plik w bieżącym katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="c89a1-185">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="c89a1-186">Podczas tworzenia środowiska z tego szablonu, wyświetlany jest monit dla wszystkich nazw zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="c89a1-186">When you create an environment from this template, you are prompted for all hello resource names.</span></span> <span data-ttu-id="c89a1-187">Można go wypełnić te nazwy w pliku szablonu, dodając hello `--include-parameter-default-value` toohello parametru `az group export` polecenia.</span><span class="sxs-lookup"><span data-stu-id="c89a1-187">You can populate these names in your template file by adding hello `--include-parameter-default-value` parameter toohello `az group export` command.</span></span> <span data-ttu-id="c89a1-188">Edytowanie nazwy JSON szablonu toospecify hello zasobów lub [Tworzenie pliku parameters.JSON następującym kodem](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) określający hello nazw zasobów.</span><span class="sxs-lookup"><span data-stu-id="c89a1-188">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="c89a1-189">toocreate środowisko z szablonu, użyj [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c89a1-189">toocreate an environment from your template, use [az group deployment create](/cli/azure/group/deployment#create) as follows:</span></span>

```azurecli
az group deployment create \
    --resource-group myNewResourceGroup \
    --template-file myResourceGroup.json
```

<span data-ttu-id="c89a1-190">Może być tooread [więcej informacji na temat toodeploy z szablonów](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c89a1-190">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c89a1-191">Więcej informacji na temat jak tooincrementally środowisk aktualizacji, użyj pliku parametrów hello i uzyskiwać dostęp do szablonów z lokalizacji magazynu jednego.</span><span class="sxs-lookup"><span data-stu-id="c89a1-191">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c89a1-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c89a1-192">Next steps</span></span>
<span data-ttu-id="c89a1-193">Teraz wszystko jest gotowe toobegin Praca z wielu składników sieciowych i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="c89a1-193">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="c89a1-194">Za pomocą hello podstawowe składniki wprowadzone w tym miejscu, można użyć tej próbki toobuild środowiska limit aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c89a1-194">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
