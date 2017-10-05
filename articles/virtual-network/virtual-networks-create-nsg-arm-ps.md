---
title: "Utwórz grupy zabezpieczeń sieci - programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć i wdrożyć przy użyciu programu PowerShell grup zabezpieczeń sieci."
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
ms.openlocfilehash: 26fe67b43d63c6685d8ae7644dd7df6931a4d2a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="ee7bb-103">Tworzenie sieci za pomocą programu PowerShell grup zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="ee7bb-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="ee7bb-104">Platforma Azure ma dwa modele wdrażania: usługa Azure Resource Manager i wersja klasyczna.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ee7bb-105">Firma Microsoft zaleca tworzenie zasobów za pomocą modelu wdrożenia usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="ee7bb-106">Aby dowiedzieć się więcej o różnicach między dwoma modelami, zapoznaj się z artykułem [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) (Informacje na temat modeli wdrażania platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="ee7bb-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="ee7bb-107">W tym artykule opisano model wdrażania usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="ee7bb-108">Możesz również [tworzenia grup NSG w klasycznym modelu wdrażania](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ee7bb-108">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="ee7bb-109">W powyższym scenariuszu na podstawie próbek PowerShell poniższe polecenia oczekiwać środowisku niezłożonym już utworzone.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="ee7bb-110">Jeśli chcesz uruchomić polecenia wyświetlaną w tym dokumencie, wdrażając najpierw utworzyć środowisko testowe [ten szablon](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), kliknij przycisk **wdrażanie na platformie Azure**, Zastąp domyślne wartości parametrów, jeśli to konieczne i postępuj zgodnie z instrukcjami w portalu.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-110">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="ee7bb-111">Jak utworzyć grupę NSG dla podsieci frontonu</span><span class="sxs-lookup"><span data-stu-id="ee7bb-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="ee7bb-112">Aby utworzyć grupy NSG o nazwie *frontonu NSG* oparte na scenariuszu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ee7bb-112">To create an NSG named *NSG-FrontEnd* based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="ee7bb-113">Jeśli nie znasz programu Azure PowerShell, zapoznaj się z artykułem [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i postępuj zgodnie z instrukcjami aż do momentu logowania się w programie Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-113">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="ee7bb-114">Utwórz regułę zabezpieczeń, umożliwiając dostęp z Internetu do portu 3389.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-114">Create a security rule allowing access from the Internet to port 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="ee7bb-115">Utwórz regułę zabezpieczeń, umożliwiając dostęp z Internetu do portu 80.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-115">Create a security rule allowing access from the Internet to port 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="ee7bb-116">Dodaj reguły utworzone powyżej, aby nowa grupa NSG o nazwie **frontonu NSG**.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-116">Add the rules created above to a new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="ee7bb-117">Sprawdź reguły utworzone w grupie NSG, wpisując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ee7bb-117">Check the rules created in the NSG by typing the following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="ee7bb-118">Dane wyjściowe przedstawiający tylko reguły zabezpieczeń:</span><span class="sxs-lookup"><span data-stu-id="ee7bb-118">Output showing just the security rules:</span></span>
   
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
6. <span data-ttu-id="ee7bb-119">Kojarzenie grupy NSG utworzone powyżej do *frontonu* podsieci.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-119">Associate the NSG created above to the *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="ee7bb-120">Dane wyjściowe są wyświetlane tylko *frontonu* ustawienia podsieci, zwróć uwagę, wartość **grupy NetworkSecurityGroup** właściwości:</span><span class="sxs-lookup"><span data-stu-id="ee7bb-120">Output showing only the *FrontEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
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
   > <span data-ttu-id="ee7bb-121">Dane wyjściowe po wprowadzeniu powyższego polecenia zawiera zawartość dla obiekt konfiguracji sieci wirtualnej, który istnieje tylko na komputerze, na którym uruchomiony jest program PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-121">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="ee7bb-122">Musisz uruchomić `Set-AzureRmVirtualNetwork` polecenia cmdlet, aby zapisać te ustawienia do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-122">You need to run the `Set-AzureRmVirtualNetwork` cmdlet to save these settings to Azure.</span></span>
   > 
   > 
7. <span data-ttu-id="ee7bb-123">Zapisz ustawienia w nowej sieci wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-123">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="ee7bb-124">Wyświetlanie tylko części NSG dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="ee7bb-124">Output showing just the NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="ee7bb-125">Jak utworzyć grupę NSG podsieci wewnętrznej</span><span class="sxs-lookup"><span data-stu-id="ee7bb-125">How to create the NSG for the back-end subnet</span></span>
<span data-ttu-id="ee7bb-126">Aby utworzyć grupy NSG o nazwie *zaplecza NSG* oparte na powyższym scenariuszu, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ee7bb-126">To create an NSG named *NSG-BackEnd* based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="ee7bb-127">Utwórz regułę zabezpieczeń zezwalającą na dostęp z podsieci frontonu do portu 1433 (domyślny port używany przez program SQL Server).</span><span class="sxs-lookup"><span data-stu-id="ee7bb-127">Create a security rule allowing access from the front-end subnet to port 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="ee7bb-128">Utwórz regułę zabezpieczeń blokuje dostęp do Internetu.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-128">Create a security rule blocking access to the Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="ee7bb-129">Dodaj reguły utworzone powyżej, aby nowa grupa NSG o nazwie **zaplecza NSG**.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-129">Add the rules created above to a new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="ee7bb-130">Kojarzenie grupy NSG utworzone powyżej do *zaplecza* podsieci.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-130">Associate the NSG created above to the *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="ee7bb-131">Dane wyjściowe są wyświetlane tylko *zaplecza* ustawienia podsieci, zwróć uwagę, wartość **grupy NetworkSecurityGroup** właściwości:</span><span class="sxs-lookup"><span data-stu-id="ee7bb-131">Output showing only the *BackEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
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
5. <span data-ttu-id="ee7bb-132">Zapisz ustawienia w nowej sieci wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-132">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-to-remove-an-nsg"></a><span data-ttu-id="ee7bb-133">Jak usunąć grupy NSG</span><span class="sxs-lookup"><span data-stu-id="ee7bb-133">How to remove an NSG</span></span>
<span data-ttu-id="ee7bb-134">Aby usunąć istniejące grupy NSG, nazywany *frontonu NSG* w takim przypadku należy wykonać kroki opisane poniżej:</span><span class="sxs-lookup"><span data-stu-id="ee7bb-134">To delete an existing NSG, called *NSG-Frontend* in this case, follow the step below:</span></span>

<span data-ttu-id="ee7bb-135">Uruchom **AzureRmNetworkSecurityGroup Usuń** pokazano poniżej i należy uwzględnić grupa NSG jest w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="ee7bb-135">Run the **Remove-AzureRmNetworkSecurityGroup** shown below and be sure to include the resource group the NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

