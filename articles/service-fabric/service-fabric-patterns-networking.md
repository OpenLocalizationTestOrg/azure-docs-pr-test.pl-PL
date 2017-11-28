---
title: "wzorce aaaNetworking dla sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano typowe wzorce sieciowych dla sieci szkieletowej usług i w jaki sposób toocreate klastra przy użyciu funkcji obsługi sieci platformy Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="709d2-103">Wzorce sieci sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="709d2-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="709d2-104">Klaster sieci szkieletowej usług Azure można zintegrować z innymi funkcjami sieci platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="709d2-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="709d2-105">W tym artykule zostanie przedstawiony zostanie sposób toocreate klastrów tego hello Użyj następujących funkcji:</span><span class="sxs-lookup"><span data-stu-id="709d2-105">In this article, we show you how toocreate clusters that use hello following features:</span></span>

- [<span data-ttu-id="709d2-106">Istniejącej sieci wirtualnej lub podsieci</span><span class="sxs-lookup"><span data-stu-id="709d2-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="709d2-107">Statycznego publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="709d2-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="709d2-108">Moduł równoważenia obciążenia tylko do wewnętrznego</span><span class="sxs-lookup"><span data-stu-id="709d2-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="709d2-109">Moduł równoważenia obciążenia wewnętrznych i zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="709d2-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="709d2-110">Sieć szkieletowa usług jest uruchamiany w zestaw skali maszyny wirtualnej standardowego.</span><span class="sxs-lookup"><span data-stu-id="709d2-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="709d2-111">Wszystkie funkcje są dostępne w zestawie skalowania maszyn wirtualnych, korzystania z klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="709d2-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="709d2-112">sekcje sieci Hello szablonów usługi Azure Resource Manager hello zestawy skalowania maszyny wirtualnej i sieci szkieletowej usług są identyczne.</span><span class="sxs-lookup"><span data-stu-id="709d2-112">hello networking sections of hello Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="709d2-113">Po wdrożeniu tooan istniejącej sieci wirtualnej jest łatwe tooincorporate inne funkcje, takie jak usługa Azure ExpressRoute, Brama sieci VPN platformy Azure, sieciowej grupy zabezpieczeń i sieci wirtualnej komunikacji równorzędnej sieciowe.</span><span class="sxs-lookup"><span data-stu-id="709d2-113">After you deploy tooan existing virtual network, it's easy tooincorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="709d2-114">Sieć szkieletowa usług to inaczej niż inne funkcje sieci w jednym aspekcie.</span><span class="sxs-lookup"><span data-stu-id="709d2-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="709d2-115">Witaj [portalu Azure](https://portal.azure.com) wewnętrznie używa hello sieci szkieletowej usług zasobów dostawcy toocall tooa klastra tooget informacji o węzłach i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="709d2-115">hello [Azure portal](https://portal.azure.com) internally uses hello Service Fabric resource provider toocall tooa cluster tooget information about nodes and applications.</span></span> <span data-ttu-id="709d2-116">Dostawca zasobów sieci szkieletowej usług Hello wymaga publicznie dostępu ruchu przychodzącego toohello HTTP bramy portu (domyślnie z portu 19080,) w punkcie końcowym zarządzania hello.</span><span class="sxs-lookup"><span data-stu-id="709d2-116">hello Service Fabric resource provider requires publicly accessible inbound access toohello HTTP gateway port (port 19080, by default) on hello management endpoint.</span></span> <span data-ttu-id="709d2-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) używa hello toomanage punkt końcowy zarządzania klastrem.</span><span class="sxs-lookup"><span data-stu-id="709d2-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses hello management endpoint toomanage your cluster.</span></span> <span data-ttu-id="709d2-118">Dostawca zasobów sieci szkieletowej usług Hello używa również port tooquery informacje o klastrze toodisplay w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="709d2-118">hello Service Fabric resource provider also uses this port tooquery information about your cluster, toodisplay in hello Azure portal.</span></span> 

<span data-ttu-id="709d2-119">Jeśli port 19080 nie jest dostępny od dostawcy zasobów usługi Service Fabric hello, takich jak wiadomość *węzłów nie można odnaleźć* jest wyświetlana w portalu hello i listy węzeł i aplikacja zostanie wyświetlona pusta.</span><span class="sxs-lookup"><span data-stu-id="709d2-119">If port 19080 is not accessible from hello Service Fabric resource provider, a message like *Nodes Not Found* appears in hello portal, and your node and application list appears empty.</span></span> <span data-ttu-id="709d2-120">Jeśli chcesz toosee klastra w hello portalu Azure, moduł równoważenia obciążenia musi ujawniać publicznego adresu IP, a swojej grupy zabezpieczeń sieciowych muszą zezwalać na ruch przychodzący port 19080.</span><span class="sxs-lookup"><span data-stu-id="709d2-120">If you want toosee your cluster in hello Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="709d2-121">Jeśli ustawienia nie spełnia te wymagania, hello portalu Azure nie wyświetla hello stan klastra.</span><span class="sxs-lookup"><span data-stu-id="709d2-121">If your setup does not meet these requirements, hello Azure portal does not display hello status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="709d2-122">Szablony</span><span class="sxs-lookup"><span data-stu-id="709d2-122">Templates</span></span>

<span data-ttu-id="709d2-123">Wszystkie szablony usługi sieć szkieletowa znajdują się w [jednego pobierania pliku](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="709d2-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="709d2-124">Powinien być stanie toodeploy szablony hello jako — za pomocą następującego polecenia programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="709d2-124">You should be able toodeploy hello templates as-is by using hello following PowerShell commands.</span></span> <span data-ttu-id="709d2-125">Jeśli wdrażasz hello istniejącego szablonu usługi Azure Virtual Network lub hello statycznego publicznego adresu IP szablonu, najpierw przeczytać artykuł hello [początkowej instalacji](#initialsetup) sekcji tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="709d2-125">If you are deploying hello existing Azure Virtual Network template or hello static public IP template, first read hello [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="709d2-126">Początkowej konfiguracji</span><span class="sxs-lookup"><span data-stu-id="709d2-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="709d2-127">Istniejącej sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="709d2-127">Existing virtual network</span></span>

<span data-ttu-id="709d2-128">W hello poniższy przykład, Rozpoczniemy z istniejącą siecią wirtualną o nazwie ExistingRG sieci wirtualnej, w hello **ExistingRG** grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="709d2-128">In hello following example, we start with an existing virtual network named ExistingRG-vnet, in hello **ExistingRG** resource group.</span></span> <span data-ttu-id="709d2-129">podsieci Hello nosi nazwę domyślny.</span><span class="sxs-lookup"><span data-stu-id="709d2-129">hello subnet is named default.</span></span> <span data-ttu-id="709d2-130">Tych domyślnych zasobów są tworzone, gdy używasz hello Azure toocreate portalu standardowe maszynę wirtualną (VM).</span><span class="sxs-lookup"><span data-stu-id="709d2-130">These default resources are created when you use hello Azure portal toocreate a standard virtual machine (VM).</span></span> <span data-ttu-id="709d2-131">Można utworzyć sieci wirtualnej hello i podsieć bez tworzenia hello maszyny Wirtualnej, ale hello głównym celem dodawania klastra tooan istniejącej sieci wirtualnej jest tooother łączności sieciowej tooprovide maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="709d2-131">You could create hello virtual network and subnet without creating hello VM, but hello main goal of adding a cluster tooan existing virtual network is tooprovide network connectivity tooother VMs.</span></span> <span data-ttu-id="709d2-132">Hello tworzenia maszyn wirtualnych zapewnia dobrym przykładem sposobu istniejącej sieci wirtualnej zwykle jest używana.</span><span class="sxs-lookup"><span data-stu-id="709d2-132">Creating hello VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="709d2-133">Jeśli klaster sieci szkieletowej usług używa tylko do wewnętrznego modułu równoważenia obciążenia, bez publicznego adresu IP, możesz użyć hello maszyny Wirtualnej i jej publicznego adresu IP jako bezpieczny *skoku pole*.</span><span class="sxs-lookup"><span data-stu-id="709d2-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use hello VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="709d2-134">Statycznego publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="709d2-134">Static public IP address</span></span>

<span data-ttu-id="709d2-135">Statycznego publicznego adresu IP jest zazwyczaj zasobów dedykowanych, zarządzanym oddzielnie z hello maszyny Wirtualnej lub jest przypisany do maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="709d2-135">A static public IP address generally is a dedicated resource that's managed separately from hello VM or VMs it's assigned to.</span></span> <span data-ttu-id="709d2-136">Udostępniane w grupie zasobów sieciowych dedykowanych (jako tooin min. hello sieci szkieletowej usług grupa zasobów klastra sam).</span><span class="sxs-lookup"><span data-stu-id="709d2-136">It's provisioned in a dedicated networking resource group (as opposed tooin hello Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="709d2-137">Tworzenie statycznego publicznego adresu IP o nazwie staticIP1 w hello tej samej grupie zasobów ExistingRG hello portalu Azure lub za pomocą programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="709d2-137">Create a static public IP address named staticIP1 in hello same ExistingRG resource group, either in hello Azure portal or by using PowerShell:</span></span>

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a><span data-ttu-id="709d2-138">Szablon usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="709d2-138">Service Fabric template</span></span>

<span data-ttu-id="709d2-139">W przykładach hello w tym artykule używamy hello template.json sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="709d2-139">In hello examples in this article, we use hello Service Fabric template.json.</span></span> <span data-ttu-id="709d2-140">Można użyć hello standardowy kreator portalu toodownload hello szablonu z portalu hello, przed utworzeniem klastra.</span><span class="sxs-lookup"><span data-stu-id="709d2-140">You can use hello standard portal wizard toodownload hello template from hello portal before you create a cluster.</span></span> <span data-ttu-id="709d2-141">Można też użyć jednego z szablonów hello w hello [galerię szablonów](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), takich jak hello [pięcioma węzłami klastra sieci szkieletowej usług](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="709d2-141">You also can use one of hello templates in hello [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like hello [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="709d2-142">Istniejącej sieci wirtualnej lub podsieci</span><span class="sxs-lookup"><span data-stu-id="709d2-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="709d2-143">Zmień nazwę toohello parametru podsieci hello hello istniejących podsieci, a następnie dodaj dwa nowe parametry tooreference hello istniejącej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="709d2-143">Change hello subnet parameter toohello name of hello existing subnet, and then add two new parameters tooreference hello existing virtual network:</span></span>

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. <span data-ttu-id="709d2-144">Zmień hello `vnetID` zmiennej toopoint toohello istniejącej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="709d2-144">Change hello `vnetID` variable toopoint toohello existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="709d2-145">Usuń `Microsoft.Network/virtualNetworks` z Twoich zasobów, dlatego Azure nie Utwórz nową sieć wirtualną:</span><span class="sxs-lookup"><span data-stu-id="709d2-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. <span data-ttu-id="709d2-146">Komentarz hello sieci wirtualnej z hello `dependsOn` atrybutu `Microsoft.Compute/virtualMachineScaleSets`, więc nie zależą od tworzenia nowej sieci wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="709d2-146">Comment out hello virtual network from hello `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. <span data-ttu-id="709d2-147">Wdrażanie szablonu hello:</span><span class="sxs-lookup"><span data-stu-id="709d2-147">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="709d2-148">Po wdrożeniu sieci wirtualnej powinna zawierać hello nowego zestawu skalowania maszyny wirtualnej maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="709d2-148">After deployment, your virtual network should include hello new scale set VMs.</span></span> <span data-ttu-id="709d2-149">Typ węzła zestawu skali maszyny wirtualnej Hello powinny być widoczne hello istniejącej sieci wirtualnej i podsieci.</span><span class="sxs-lookup"><span data-stu-id="709d2-149">hello virtual machine scale set node type should show hello existing virtual network and subnet.</span></span> <span data-ttu-id="709d2-150">Można również użyć protokołu RDP (Remote Desktop) tooaccess hello maszynę Wirtualną, która została już w sieci wirtualnej hello i tooping hello nowego zestawu skalowania maszyny wirtualnej maszyny wirtualne:</span><span class="sxs-lookup"><span data-stu-id="709d2-150">You also can use Remote Desktop Protocol (RDP) tooaccess hello VM that was already in hello virtual network, and tooping hello new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="709d2-151">Na przykład innego, zobacz [, który nie jest określonym tooService sieci szkieletowej](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="709d2-151">For another example, see [one that is not specific tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="709d2-152">Statycznego publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="709d2-152">Static public IP address</span></span>

1. <span data-ttu-id="709d2-153">Dodaj parametry dla nazwy hello hello istniejące grupy zasobów w usłudze statycznego adresu IP, nazwa i Pełna nazwa domeny (FQDN):</span><span class="sxs-lookup"><span data-stu-id="709d2-153">Add parameters for hello name of hello existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. <span data-ttu-id="709d2-154">Usuń hello `dnsName` parametru.</span><span class="sxs-lookup"><span data-stu-id="709d2-154">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="709d2-155">(hello statyczny adres IP już istnieje.)</span><span class="sxs-lookup"><span data-stu-id="709d2-155">(hello static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="709d2-156">Dodawanie zmiennej tooreference hello istniejących statyczny adres IP:</span><span class="sxs-lookup"><span data-stu-id="709d2-156">Add a variable tooreference hello existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="709d2-157">Usuń `Microsoft.Network/publicIPAddresses` z Twoich zasobów, dlatego Azure nie Utwórz nowy adres IP:</span><span class="sxs-lookup"><span data-stu-id="709d2-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. <span data-ttu-id="709d2-158">Komentarz hello adresu IP z hello `dependsOn` atrybutu `Microsoft.Network/loadBalancers`, więc nie zależą od tworzenia nowego adresu IP:</span><span class="sxs-lookup"><span data-stu-id="709d2-158">Comment out hello IP address from hello `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. <span data-ttu-id="709d2-159">W hello `Microsoft.Network/loadBalancers` zasobów, zmień hello `publicIPAddress` elementu `frontendIPConfigurations` tooreference hello istniejących statyczny adres IP, zamiast nowo utworzone:</span><span class="sxs-lookup"><span data-stu-id="709d2-159">In hello `Microsoft.Network/loadBalancers` resource, change hello `publicIPAddress` element of `frontendIPConfigurations` tooreference hello existing static IP address instead of a newly created one:</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. <span data-ttu-id="709d2-160">W hello `Microsoft.ServiceFabric/clusters` zasobów, zmień `managementEndpoint` toohello nazwy FQDN DNS hello statycznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="709d2-160">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toohello DNS FQDN of hello static IP address.</span></span> <span data-ttu-id="709d2-161">Jeśli używane są bezpieczne klastra, upewnij się, możesz zmienić *http://* za*https://*.</span><span class="sxs-lookup"><span data-stu-id="709d2-161">If you are using a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="709d2-162">(Należy pamiętać, że ten krok ma zastosowanie tylko klastry tooService w sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="709d2-162">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="709d2-163">Jeśli korzystasz z zestawu skalowania maszyn wirtualnych, Pomiń ten krok.)</span><span class="sxs-lookup"><span data-stu-id="709d2-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="709d2-164">Wdrażanie szablonu hello:</span><span class="sxs-lookup"><span data-stu-id="709d2-164">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="709d2-165">Po wdrożeniu widać, że moduł równoważenia obciążenia jest powiązane toohello publiczny statyczny adres IP z hello innej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="709d2-165">After deployment, you can see that your load balancer is bound toohello public static IP address from hello other resource group.</span></span> <span data-ttu-id="709d2-166">Witaj punktu końcowego połączenia klienta usługi Service Fabric i [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) toohello punktu końcowego nazwy FQDN DNS hello statycznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="709d2-166">hello Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point toohello DNS FQDN of hello static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="709d2-167">Moduł równoważenia obciążenia tylko do wewnętrznego</span><span class="sxs-lookup"><span data-stu-id="709d2-167">Internal-only load balancer</span></span>

<span data-ttu-id="709d2-168">W tym scenariuszu zastępuje hello zewnętrznej usługi równoważenia obciążenia w szablonie usługi sieć szkieletowa domyślne hello usługi równoważenia obciążenia wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="709d2-168">This scenario replaces hello external load balancer in hello default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="709d2-169">Aby uzyskać konsekwencje dla hello portalu Azure i dostawcy zasobów usługi Service Fabric hello Zobacz hello powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="709d2-169">For implications for hello Azure portal and for hello Service Fabric resource provider, see hello preceding section.</span></span>

1. <span data-ttu-id="709d2-170">Usuń hello `dnsName` parametru.</span><span class="sxs-lookup"><span data-stu-id="709d2-170">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="709d2-171">(Nie jest wymagana.)</span><span class="sxs-lookup"><span data-stu-id="709d2-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="709d2-172">Opcjonalnie Jeśli używasz statyczną metodą przydziału, można dodać parametr statyczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="709d2-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="709d2-173">Jeśli używasz metody przydzielania, nie trzeba toodo ten krok.</span><span class="sxs-lookup"><span data-stu-id="709d2-173">If you use a dynamic allocation method, you do not need toodo this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="709d2-174">Usuń `Microsoft.Network/publicIPAddresses` z Twoich zasobów, dlatego Azure nie Utwórz nowy adres IP:</span><span class="sxs-lookup"><span data-stu-id="709d2-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. <span data-ttu-id="709d2-175">Usuń adres IP hello `dependsOn` atrybutu `Microsoft.Network/loadBalancers`, więc nie zależą od tworzenia nowego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="709d2-175">Remove hello IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="709d2-176">Dodawanie sieci wirtualnej hello `dependsOn` atrybutu, ponieważ moduł równoważenia obciążenia hello zależy od teraz hello podsieci z sieci wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="709d2-176">Add hello virtual network `dependsOn` attribute because hello load balancer now depends on hello subnet from hello virtual network:</span></span>

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. <span data-ttu-id="709d2-177">Zmień równoważenia obciążenia hello `frontendIPConfigurations` z przy użyciu `publicIPAddress`, toousing podsieci i `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="709d2-177">Change hello load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, toousing a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="709d2-178">`privateIPAddress`używa wstępnie zdefiniowanych statyczne wewnętrzne adresy IP.</span><span class="sxs-lookup"><span data-stu-id="709d2-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="709d2-179">toouse dynamicznego adresu IP, Usuń hello `privateIPAddress` elementu, a następnie zmień `privateIPAllocationMethod` za**dynamiczne**.</span><span class="sxs-lookup"><span data-stu-id="709d2-179">toouse a dynamic IP address, remove hello `privateIPAddress` element, and then change `privateIPAllocationMethod` too**Dynamic**.</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. <span data-ttu-id="709d2-180">W hello `Microsoft.ServiceFabric/clusters` zasobów, zmień `managementEndpoint` adres usługi równoważenia obciążenia wewnętrznego toohello toopoint.</span><span class="sxs-lookup"><span data-stu-id="709d2-180">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toopoint toohello internal load balancer address.</span></span> <span data-ttu-id="709d2-181">Jeśli używasz bezpiecznego klastra, upewnij się, można zmienić *http://* za*https://*.</span><span class="sxs-lookup"><span data-stu-id="709d2-181">If you use a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="709d2-182">(Należy pamiętać, że ten krok ma zastosowanie tylko klastry tooService w sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="709d2-182">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="709d2-183">Jeśli korzystasz z zestawu skalowania maszyn wirtualnych, Pomiń ten krok.)</span><span class="sxs-lookup"><span data-stu-id="709d2-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="709d2-184">Wdrażanie szablonu hello:</span><span class="sxs-lookup"><span data-stu-id="709d2-184">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="709d2-185">Po wdrożeniu przez moduł równoważenia obciążenia używa hello 10.0.0.250 statycznego prywatnego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="709d2-185">After deployment, your load balancer uses hello private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="709d2-186">Jeśli masz inną maszynę w tej samej sieci wirtualnej, można przejść toohello wewnętrzny [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="709d2-186">If you have another machine in that same virtual network, you can go toohello internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="709d2-187">Uwaga łączy tooone węzłów hello za hello równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-187">Note that it connects tooone of hello nodes behind hello load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="709d2-188">Moduł równoważenia obciążenia wewnętrznych i zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="709d2-188">Internal and external load balancer</span></span>

<span data-ttu-id="709d2-189">W tym scenariuszu zaczynać się hello istniejącego typu jednowęzłowej zewnętrznej usługi równoważenia obciążenia i dodać wewnętrznego modułu równoważenia obciążenia dla hello tego samego typu węzła.</span><span class="sxs-lookup"><span data-stu-id="709d2-189">In this scenario, you start with hello existing single-node type external load balancer, and add an internal load balancer for hello same node type.</span></span> <span data-ttu-id="709d2-190">Pulę adresów zaplecza tooa portu zaplecza dołączony można przypisać tylko tooa jednego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-190">A back-end port attached tooa back-end address pool can be assigned only tooa single load balancer.</span></span> <span data-ttu-id="709d2-191">Wybierz, które usługa równoważenia obciążenia będzie miał porty Twojej aplikacji i które usługa równoważenia obciążenia mają zarządzania punktów końcowych (porty 19000 i 19080).</span><span class="sxs-lookup"><span data-stu-id="709d2-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="709d2-192">Punkty końcowe zarządzania hello umieszczenie na powitania wewnętrznego modułu równoważenia obciążenia, należy przechowywać w uwadze hello zasobów sieci szkieletowej usług omówionych w artykule hello ograniczenia dostawcy.</span><span class="sxs-lookup"><span data-stu-id="709d2-192">If you put hello management endpoints on hello internal load balancer, keep in mind hello Service Fabric resource provider restrictions discussed earlier in hello article.</span></span> <span data-ttu-id="709d2-193">W przykładzie hello używanych punkty końcowe zarządzania hello pozostają na powitania zewnętrznej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-193">In hello example we use, hello management endpoints remain on hello external load balancer.</span></span> <span data-ttu-id="709d2-194">Możesz również dodać port 80 aplikacji portu i umieść ją na hello wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-194">You also add a port 80 application port, and place it on hello internal load balancer.</span></span>

<span data-ttu-id="709d2-195">W klastrze typu węzła dwa jest jednego typu węzła na powitania zewnętrznej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-195">In a two-node-type cluster, one node type is on hello external load balancer.</span></span> <span data-ttu-id="709d2-196">Witaj innego typu węzła znajduje się na powitania wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-196">hello other node type is on hello internal load balancer.</span></span> <span data-ttu-id="709d2-197">toouse klastrze typu węzła dwa hello utworzonych przez portal dwóch węzłów typu szablonu (który pochodzi z dwóch usług równoważenia obciążenia), Przełącz hello drugi obciążenia równoważenia tooan wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-197">toouse a two-node-type cluster, in hello portal-created two-node-type template (which comes with two load balancers), switch hello second load balancer tooan internal load balancer.</span></span> <span data-ttu-id="709d2-198">Aby uzyskać więcej informacji, zobacz hello [modułu równoważenia obciążenia tylko do wewnętrznego](#internallb) sekcji.</span><span class="sxs-lookup"><span data-stu-id="709d2-198">For more information, see hello [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="709d2-199">Dodaj parametr adres IP hello statyczna obciążenia wewnętrznego modułu równoważenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-199">Add hello static internal load balancer IP address parameter.</span></span> <span data-ttu-id="709d2-200">(Aby uzyskać informacje o powiązanych toousing dynamicznego adresu IP, zobacz wcześniejszej części tego artykułu).</span><span class="sxs-lookup"><span data-stu-id="709d2-200">(For notes related toousing a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="709d2-201">Dodaj parametr port 80 aplikacji.</span><span class="sxs-lookup"><span data-stu-id="709d2-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="709d2-202">Wersje wewnętrzne tooadd hello istniejących sieci zmiennych, skopiuj i wklej je i Dodaj "-Int" Nazwa toohello:</span><span class="sxs-lookup"><span data-stu-id="709d2-202">tooadd internal versions of hello existing networking variables, copy and paste them, and add "-Int" toohello name:</span></span>

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. <span data-ttu-id="709d2-203">Jeśli na początku zasubskrybujesz generowanych przez portal szablonu hello, który korzysta z aplikacji portu 80, hello domyślnego szablonu portalu dodaje AppPort1 (port 80) na powitania zewnętrznej usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-203">If you start with hello portal-generated template that uses application port 80, hello default portal template adds AppPort1 (port 80) on hello external load balancer.</span></span> <span data-ttu-id="709d2-204">W takim przypadku usuń AppPort1 z hello zewnętrznej usługi równoważenia obciążenia `loadBalancingRules` i sond, dzięki czemu można je dodać toohello wewnętrznego modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="709d2-204">In this case, remove AppPort1 from hello external load balancer `loadBalancingRules` and probes, so you can add it toohello internal load balancer:</span></span>

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. <span data-ttu-id="709d2-205">Dodaj drugi `Microsoft.Network/loadBalancers` zasobów.</span><span class="sxs-lookup"><span data-stu-id="709d2-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="709d2-206">Wygląda podobnie toohello wewnętrznego modułu równoważenia obciążenia utworzony w hello [modułu równoważenia obciążenia tylko do wewnętrznego](#internallb) sekcji, ale używa powitania "-Int" obciążenia równoważenia zmienne i implementuje wyłącznie hello aplikacji port 80.</span><span class="sxs-lookup"><span data-stu-id="709d2-206">It looks similar toohello internal load balancer created in hello [Internal-only load balancer](#internallb) section, but it uses hello "-Int" load balancer variables, and implements only hello application port 80.</span></span> <span data-ttu-id="709d2-207">Spowoduje to również usunięcie `inboundNatPools`, punkty końcowe protokołu RDP tookeep hello publiczny moduł równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-207">This also removes `inboundNatPools`, tookeep RDP endpoints on hello public load balancer.</span></span> <span data-ttu-id="709d2-208">Jeśli chcesz RDP na powitania wewnętrznego modułu równoważenia obciążenia, Przenieś `inboundNatPools` toothis usługi równoważenia obciążenia zewnętrznych hello wewnętrznego modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="709d2-208">If you want RDP on hello internal load balancer, move `inboundNatPools` from hello external load balancer toothis internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. <span data-ttu-id="709d2-209">W `networkProfile` dla hello `Microsoft.Compute/virtualMachineScaleSets` zasobów, dodać puli adresów zaplecza wewnętrzny hello:</span><span class="sxs-lookup"><span data-stu-id="709d2-209">In `networkProfile` for hello `Microsoft.Compute/virtualMachineScaleSets` resource, add hello internal back-end address pool:</span></span>

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. <span data-ttu-id="709d2-210">Wdrażanie szablonu hello:</span><span class="sxs-lookup"><span data-stu-id="709d2-210">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="709d2-211">Po wdrożeniu widać dwie usługi równoważenia obciążenia w grupie zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="709d2-211">After deployment, you can see two load balancers in hello resource group.</span></span> <span data-ttu-id="709d2-212">Po przejściu usługi równoważenia obciążenia hello widoczne hello publicznego adresu IP i zarządzania przypisany punktów końcowych (porty 19000 i 19080) toohello publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="709d2-212">If you browse hello load balancers, you can see hello public IP address and management endpoints (ports 19000 and 19080) assigned toohello public IP address.</span></span> <span data-ttu-id="709d2-213">Również widoczne hello statyczne wewnętrzne IP adres i aplikacji przypisany punkt końcowy (port 80) toohello wewnętrznego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="709d2-213">You also can see hello static internal IP address and application endpoint (port 80) assigned toohello internal load balancer.</span></span> <span data-ttu-id="709d2-214">Zarówno załadować wykorzystania równoważenia hello tego samego zestawu skalowania maszyn wirtualnych puli zaplecza.</span><span class="sxs-lookup"><span data-stu-id="709d2-214">Both load balancers use hello same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="709d2-215">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="709d2-215">Next steps</span></span>
[<span data-ttu-id="709d2-216">Tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="709d2-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
