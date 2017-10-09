---
title: "zabezpieczenia sieci aaaAnalyze z widokiem grupy obserwatorów zabezpieczeń Azure sieci — interfejs API REST | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse tooanalyze programu PowerShell, a wirtualnych maszyn zabezpieczeń z widokiem grupy zabezpieczeń."
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
ms.openlocfilehash: 0858a64a9454816e05f06dadb9536ad0c755e90e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-rest-api"></a><span data-ttu-id="4b9fc-103">Analizowanie zabezpieczeń maszyny wirtualnej z widoku grupy zabezpieczeń przy użyciu interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="4b9fc-103">Analyze your Virtual Machine security with Security Group View using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4b9fc-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b9fc-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="4b9fc-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="4b9fc-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="4b9fc-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="4b9fc-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="4b9fc-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="4b9fc-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="4b9fc-108">Widok grupy zabezpieczeń zwraca reguły zabezpieczeń sieci skonfigurowane i skuteczne, które są stosowane tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="4b9fc-109">Ta funkcja jest przydatna tooaudit i diagnozowanie grup zabezpieczeń sieci i reguł, które są skonfigurowane na ruch tooensure maszyn wirtualnych są poprawnie dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="4b9fc-110">W tym artykule zostanie przedstawiony zostanie sposób tooretrieve hello skuteczne i zastosowane reguł tooa maszyny wirtualnej za pomocą interfejsu API REST</span><span class="sxs-lookup"><span data-stu-id="4b9fc-110">In this article, we show you how tooretrieve hello effective and applied security rules tooa virtual machine using REST API</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4b9fc-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="4b9fc-111">Before you begin</span></span>

<span data-ttu-id="4b9fc-112">W tym scenariuszu należy wywołać widok grupy zabezpieczeń tooget hello hello interfejsu API Rest obserwatorów sieci dla maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-112">In this scenario, you call hello Network Watcher Rest API tooget hello security group view for a virtual machine.</span></span> <span data-ttu-id="4b9fc-113">ARMclient jest używane toocall: hello interfejsu API REST przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="4b9fc-114">ARMClient znajduje się na chocolatey w [ARMClient na Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="4b9fc-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="4b9fc-115">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="4b9fc-116">Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="4b9fc-117">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="4b9fc-117">Scenario</span></span>

<span data-ttu-id="4b9fc-118">Scenariusz Hello omówione w tym artykule pobiera hello reguły zabezpieczeń skuteczne i zastosowane dla podanej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-118">hello scenario covered in this article retrieves hello effective and applied security rules for a given virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="4b9fc-119">Zaloguj się za pomocą ARMClient</span><span class="sxs-lookup"><span data-stu-id="4b9fc-119">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="4b9fc-120">Pobieranie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4b9fc-120">Retrieve a virtual machine</span></span>

<span data-ttu-id="4b9fc-121">Uruchom hello następującego skryptu tooreturn wirtualnego machineThe następującego kodu wymaga zmiennych:</span><span class="sxs-lookup"><span data-stu-id="4b9fc-121">Run hello following script tooreturn a virtual machineThe following code needs variables:</span></span>

- <span data-ttu-id="4b9fc-122">**Identyfikator subskrypcji** -hello identyfikator subskrypcji można również pobrać z hello **Get-AzureRMSubscription** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-122">**subscriptionId** - hello subscription id can also be retrieved with hello **Get-AzureRMSubscription** cmdlet.</span></span>
- <span data-ttu-id="4b9fc-123">**resourceGroupName** — Witaj Nazwa grupy zasobów, która zawiera maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-123">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="4b9fc-124">Witaj potrzebna jest hello **identyfikator** typu hello `Microsoft.Compute/virtualMachines` w odpowiedzi, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="4b9fc-124">hello information that is needed is hello **id** under hello type `Microsoft.Compute/virtualMachines` in response, as seen in hello following example:</span></span>

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

## <a name="get-security-group-view-for-virtual-machine"></a><span data-ttu-id="4b9fc-125">Pobierz widok grupy zabezpieczeń dla maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="4b9fc-125">Get security group view for virtual machine</span></span>

<span data-ttu-id="4b9fc-126">Poniższy przykład Hello żądań widok grupy zabezpieczeń hello docelowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-126">hello following example requests hello security group view of a targeted virtual machine.</span></span> <span data-ttu-id="4b9fc-127">wyniki Hello w tym przykładzie może być używane toocompare toohello reguł i zdefiniowanych przez hello utworzenia toolook dla odejście konfiguracji zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-127">hello results from this example can be used toocompare toohello rules and security defined by hello origination toolook for configuration drift.</span></span>

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

## <a name="view-hello-response"></a><span data-ttu-id="4b9fc-128">Wyświetl hello odpowiedź</span><span class="sxs-lookup"><span data-stu-id="4b9fc-128">View hello response</span></span>

<span data-ttu-id="4b9fc-129">następujące przykładowe Hello jest hello odpowiedź zwrócona z hello poprzedzających polecenia.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-129">hello following sample is hello response returned from hello preceding command.</span></span> <span data-ttu-id="4b9fc-130">Witaj w wynikach wszystkich reguł zabezpieczeń skuteczne i zastosowane hello na maszynie wirtualnej hello podziale grupy **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, i  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-130">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4b9fc-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4b9fc-131">Next steps</span></span>

<span data-ttu-id="4b9fc-132">Odwiedź stronę [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-security-group-view-powershell.md) toolearn sposób weryfikacji tooautomate grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="4b9fc-132">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-security-group-view-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


