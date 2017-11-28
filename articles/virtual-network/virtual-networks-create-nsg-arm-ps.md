---
title: "aaaCreate sieciowej grupy zabezpieczeń - programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate i wdrażanie grup zabezpieczeń sieci przy użyciu programu PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1c8db773febb163d9cb010d23f2913b5ebe0fa94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="29cc3-103">Tworzenie sieci za pomocą programu PowerShell grup zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="29cc3-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="29cc3-104">Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna.</span><span class="sxs-lookup"><span data-stu-id="29cc3-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="29cc3-105">Firma Microsoft zaleca utworzenie zasobów za pośrednictwem modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="29cc3-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="29cc3-106">więcej informacji o toolearn hello różnice między modelami hello dwa odczytu hello [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="29cc3-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="29cc3-107">W tym artykule omówiono modelu wdrażania usługi Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="29cc3-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="29cc3-108">Możesz również [tworzenia grup NSG w hello klasycznego modelu wdrażania](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="29cc3-108">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="29cc3-109">w powyższym scenariuszu hello na podstawie próbek Hello PowerShell poniższe polecenia oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="29cc3-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="29cc3-110">Jeśli chcesz korzystać z poleceń hello toorun wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe hello [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), kliknij przycisk **wdrażanie tooAzure**, Zastąp hello domyślne wartości parametrów Jeśli to konieczne i wykonaj instrukcje hello hello portalu.</span><span class="sxs-lookup"><span data-stu-id="29cc3-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="29cc3-111">Jak toocreate hello NSG dla podsieci frontonu hello</span><span class="sxs-lookup"><span data-stu-id="29cc3-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="29cc3-112">toocreate o nazwie grupy NSG *frontonu NSG* oparte na powitania scenariusz, wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="29cc3-112">toocreate an NSG named *NSG-FrontEnd* based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="29cc3-113">Jeśli nie znasz programu Azure PowerShell, zobacz [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i wykonaj instrukcje hello wszystkich toohello sposób hello kończyć toosign na platformie Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="29cc3-113">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="29cc3-114">Utwórz regułę zabezpieczeń zezwalającą na dostęp z hello Internet tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="29cc3-114">Create a security rule allowing access from hello Internet tooport 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="29cc3-115">Utwórz regułę zabezpieczeń zezwalającą na dostęp z hello Internet tooport 80.</span><span class="sxs-lookup"><span data-stu-id="29cc3-115">Create a security rule allowing access from hello Internet tooport 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="29cc3-116">Dodawanie reguł hello utworzone powyżej tooa o nazwie Nowa grupa NSG **frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="29cc3-116">Add hello rules created above tooa new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="29cc3-117">Sprawdź zasady hello utworzone w hello NSG, wpisując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="29cc3-117">Check hello rules created in hello NSG by typing hello following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="29cc3-118">Dane wyjściowe reguły zabezpieczeń tylko hello przedstawiający:</span><span class="sxs-lookup"><span data-stu-id="29cc3-118">Output showing just hello security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="29cc3-119">Skojarz hello NSG utworzone powyżej toohello *frontonu* podsieci.</span><span class="sxs-lookup"><span data-stu-id="29cc3-119">Associate hello NSG created above toohello *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="29cc3-120">Dane wyjściowe przedstawiający tylko hello *frontonu* ustawienia podsieci, wartość hello powiadomienia hello **grupy NetworkSecurityGroup** właściwości:</span><span class="sxs-lookup"><span data-stu-id="29cc3-120">Output showing only hello *FrontEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="29cc3-121">Witaj dane wyjściowe polecenia hello powyżej przedstawiono hello zawartości dla obiekt konfiguracji sieci wirtualnej hello, który istnieje tylko na komputerze hello, w którym uruchomiony jest program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="29cc3-121">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="29cc3-122">Należy toorun hello `Set-AzureRmVirtualNetwork` toosave polecenia cmdlet tooAzure tych ustawień.</span><span class="sxs-lookup"><span data-stu-id="29cc3-122">You need toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave these settings tooAzure.</span></span>
   > 
   > 
7. <span data-ttu-id="29cc3-123">Zapisz hello nowe tooAzure ustawień sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29cc3-123">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="29cc3-124">Dane wyjściowe, pokazujący tylko części NSG hello:</span><span class="sxs-lookup"><span data-stu-id="29cc3-124">Output showing just hello NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="29cc3-125">Jak toocreate hello NSG dla podsieci wewnętrznej hello</span><span class="sxs-lookup"><span data-stu-id="29cc3-125">How toocreate hello NSG for hello back-end subnet</span></span>
<span data-ttu-id="29cc3-126">grupy NSG o nazwie toocreate *zaplecza NSG* oparte na powyższym scenariuszu hello, ukończyć powitalnych następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="29cc3-126">toocreate an NSG named *NSG-BackEnd* based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="29cc3-127">Utwórz regułę zabezpieczeń zezwalającą na dostęp z hello podsieci frontonu tooport 1433 (domyślny port używany przez program SQL Server).</span><span class="sxs-lookup"><span data-stu-id="29cc3-127">Create a security rule allowing access from hello front-end subnet tooport 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="29cc3-128">Utwórz regułę zabezpieczeń blokuje toohello dostęp do Internetu.</span><span class="sxs-lookup"><span data-stu-id="29cc3-128">Create a security rule blocking access toohello Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="29cc3-129">Dodawanie reguł hello utworzone powyżej tooa o nazwie Nowa grupa NSG **zaplecza NSG**.</span><span class="sxs-lookup"><span data-stu-id="29cc3-129">Add hello rules created above tooa new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="29cc3-130">Skojarz hello NSG utworzone powyżej toohello *zaplecza* podsieci.</span><span class="sxs-lookup"><span data-stu-id="29cc3-130">Associate hello NSG created above toohello *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="29cc3-131">Dane wyjściowe przedstawiający tylko hello *wewnętrznej bazy danych* ustawienia podsieci, wartość hello powiadomienia hello **grupy NetworkSecurityGroup** właściwości:</span><span class="sxs-lookup"><span data-stu-id="29cc3-131">Output showing only hello *BackEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="29cc3-132">Zapisz hello nowe tooAzure ustawień sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="29cc3-132">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a><span data-ttu-id="29cc3-133">Jak tooremove grupy NSG</span><span class="sxs-lookup"><span data-stu-id="29cc3-133">How tooremove an NSG</span></span>
<span data-ttu-id="29cc3-134">toodelete istniejącej grupy NSG, nazywany *frontonu NSG* w takim przypadku należy wykonać krok hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="29cc3-134">toodelete an existing NSG, called *NSG-Frontend* in this case, follow hello step below:</span></span>

<span data-ttu-id="29cc3-135">Uruchom hello **AzureRmNetworkSecurityGroup Usuń** pokazano poniżej i można się tooinclude hello zasobów grupy hello grupa NSG jest.</span><span class="sxs-lookup"><span data-stu-id="29cc3-135">Run hello **Remove-AzureRmNetworkSecurityGroup** shown below and be sure tooinclude hello resource group hello NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

