---
title: "Analizowanie zabezpieczeń sieci z widokiem grupy obserwatorów zabezpieczeń Azure sieci - interfejsu API REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób analizowania zabezpieczeń maszyn wirtualnych z widokiem grupy zabezpieczeń przy użyciu programu PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a2f418fe-f5d2-43ed-8dc3-df0ed2a4d4ac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: afced52b3ae6f3b7f400364f5ec7d049aa166590
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="06475-103">Analizowanie zabezpieczeń maszyny wirtualnej z widoku grupy zabezpieczeń przy użyciu interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="06475-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="06475-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="06475-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="06475-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="06475-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="06475-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="06475-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="06475-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="06475-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="06475-108">Widok grupy zabezpieczeń zwraca reguły zabezpieczeń sieci skonfigurowane i skuteczne, które są stosowane do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06475-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="06475-109">Ta funkcja jest przydatna do inspekcji i diagnostyki sieciowych grup zabezpieczeń i reguł, które są skonfigurowane na maszynie Wirtualnej dla zapewnienia ruchu jest poprawnie dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="06475-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="06475-110">W tym artykule firma Microsoft opisano, jak pobrać zasady zabezpieczeń skuteczne i zastosowane do maszyny wirtualnej przy użyciu interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="06475-110">In this article, we show you how to retrieve the effective and applied security rules to a virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="06475-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="06475-111">Before you begin</span></span>

<span data-ttu-id="06475-112">W tym scenariuszu można wywołać interfejsu API Rest obserwatora sieciowego można pobrać widoku grupy zabezpieczeń dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06475-112">In this scenario, you call the Network Watcher Rest API to get the security group view for a virtual machine.</span></span> <span data-ttu-id="06475-113">ARMclient służy do wywołania interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06475-113">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="06475-114">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="06475-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="06475-115">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="06475-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="06475-116">Scenariusz również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje ma być używany.</span><span class="sxs-lookup"><span data-stu-id="06475-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="06475-117">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="06475-117">Scenario</span></span>

<span data-ttu-id="06475-118">Scenariusz omówione w tym artykule pobiera reguły zabezpieczeń skuteczne i zastosowane dla podanej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06475-118">The scenario covered in this article retrieves the effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="06475-119">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="06475-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="06475-120">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="06475-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="06475-121">Uruchom następujący skrypt, aby zwrócić wirtualnego machineThe następujący kod wymaga zmiennych:</span><span class="sxs-lookup"><span data-stu-id="06475-121">Run the following script to return a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="06475-122">**Identyfikator subskrypcji** — identyfikator subskrypcji można również pobrać z **Get-AzureRMSubscription** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="06475-122">**subscriptionId** - The subscription id can also be retrieved with the **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="06475-123">**resourceGroupName** — Nazwa grupy zasobów, która zawiera maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="06475-123">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="06475-124">Informacje potrzebne jest **identyfikator** w obszarze typu `Microsoft.Compute/virtualMachines` w odpowiedzi, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="06475-124">The information that is needed is the **id** under the type `Microsoft.Compute/virtualMachines` in response, as seen in the following example:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft
.Network/networkInterfaces/{nicName}"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Com
pute/virtualMachines/{vmName}/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Compute
/virtualMachines/{vmName}",
      "name": "{vmName}"
    }
  ]
}
```

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="06475-125">Pobierz widok grupy zabezpieczeń dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="06475-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="06475-126">Poniższy przykład żądań widok grupy zabezpieczeń docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="06475-126">The following example requests the security group view of a targeted virtual machine.</span></span> <span data-ttu-id="06475-127">Wyniki z tego przykładu może służyć do porównania zasad i zdefiniowanych przez inicjowanie do wyszukania odejście konfiguracji zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="06475-127">The results from this example can be used to compare to the rules and security defined by the origination to look for configuration drift.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/$subscriptionId/resourceGroups/$resourceGroupName/providers/Microsoft.compute/virtualMachine/$vmName

$requestBody = @"
{
    'targetResourceId': '${targetUri}'

}
"@
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/securityGroupView?api-version=2016-12-01" $requestBody -verbose
```

## <a name="view-the-response"></a><span data-ttu-id="06475-128">Widok odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="06475-128">View the response</span></span>

<span data-ttu-id="06475-129">Poniższy przykład jest odpowiedź zwrócona z poprzedniego polecenia.</span><span class="sxs-lookup"><span data-stu-id="06475-129">The following sample is the response returned from the preceding command.</span></span> <span data-ttu-id="06475-130">Wyniki Pokaż wszystkie reguły zabezpieczeń skuteczne i zastosowane na maszynie wirtualnej podziale grupy **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, i **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="06475-130">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json

{
  "networkInterfaces": [
    {
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkInterfaces/{nicName}",
          "securityRules": [
            {
              "name": "default-allow-rdp",
              "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/securityRules/default-allow-rdp",
              "etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
              "properties": {
                "provisioningState": "Succeeded",
                "protocol": "TCP",
                "sourcePortRange": "*",
                "destinationPortRange": "3389",
                "sourceAddressPrefix": "*",
                "destinationAddressPrefix": "*",
                "access": "Allow",
                "priority": 1000,
                "direction": "Inbound"
              }
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "name": "AllowVnetInBound",
            "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}/defaultSecurityRules/",
            "properties": {
              "provisioningState": "Succeeded",
              "description": "Allow inbound traffic from all VMs in VNET",
              "protocol": "*",
              "sourcePortRange": "*",
              "destinationPortRange": "*",
              "sourceAddressPrefix": "VirtualNetwork",
              "destinationAddressPrefix": "VirtualNetwork",
              "access": "Allow",
              "priority": 65000,
              "direction": "Inbound"
            }
          },
          ...
        ],
        "effectiveSecurityRules": [
          {
            "name": "DefaultOutboundDenyAll",
            "protocol": "All",
            "sourcePortRange": "0-65535",
            "destinationPortRange": "0-65535",
            "sourceAddressPrefix": "*",
            "destinationAddressPrefix": "*",
            "access": "Deny",
            "priority": 65500,
            "direction": "Outbound"
          },
          ...
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="06475-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="06475-131">Next steps</span></span>

<span data-ttu-id="06475-132">Odwiedź stronę [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-security-group-view-powershell.md) sposób automatyzacji sprawdzania poprawności grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="06475-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


