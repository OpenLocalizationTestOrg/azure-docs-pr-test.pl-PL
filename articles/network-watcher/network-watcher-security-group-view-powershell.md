---
title: "Analizowanie zabezpieczeń sieci z widokiem grupy obserwatora zabezpieczeń Azure sieci - PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób analizowania zabezpieczeń maszyn wirtualnych z widokiem grupy zabezpieczeń przy użyciu programu PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 04e76b49-6a1b-4d0f-9a9b-51cf2f4df5a2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 363fdd9f1de933bb4050f91e1e111aaf3e419058
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="c1c5d-103">Analizowanie zabezpieczeń maszyny wirtualnej z widokiem grupy zabezpieczeń przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1c5d-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="c1c5d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1c5d-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="c1c5d-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="c1c5d-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="c1c5d-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="c1c5d-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="c1c5d-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="c1c5d-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="c1c5d-108">Widok grupy zabezpieczeń zwraca reguły zabezpieczeń sieci skonfigurowane i skuteczne, które są stosowane do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="c1c5d-109">Ta funkcja jest przydatna do inspekcji i diagnostyki sieciowych grup zabezpieczeń i reguł, które są skonfigurowane na maszynie Wirtualnej dla zapewnienia ruchu jest poprawnie dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="c1c5d-110">W tym artykule firma Microsoft opisano, jak pobrać zasady skonfigurowane i skuteczne zabezpieczeń do maszyny wirtualnej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1c5d-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c1c5d-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="c1c5d-111">Before you begin</span></span>

<span data-ttu-id="c1c5d-112">W tym scenariuszu można uruchomić `Get-AzureRmNetworkWatcherSecurityGroupView` polecenia cmdlet można pobrać danych reguły zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-112">In this scenario, you run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet to retrieve the security rule information.</span></span>

<span data-ttu-id="c1c5d-113">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="c1c5d-114">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="c1c5d-114">Scenario</span></span>

<span data-ttu-id="c1c5d-115">Scenariusz omówione w tym artykule pobiera reguły zabezpieczeń skonfigurowane i efektywny dla podanej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-115">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="c1c5d-116">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="c1c5d-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="c1c5d-117">Pierwszym krokiem jest pobrać wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-117">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="c1c5d-118">Ta zmienna jest przekazywana do `Get-AzureRmNetworkWatcherSecurityGroupView` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-118">This variable is passed to the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="c1c5d-119">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="c1c5d-119">Get a VM</span></span>

<span data-ttu-id="c1c5d-120">Maszyna wirtualna jest wymagana do uruchamiania `Get-AzureRmNetworkWatcherSecurityGroupView` polecenia cmdlet przed.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-120">A virtual machine is required to run the `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="c1c5d-121">Poniższy przykład pobiera obiekt maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-121">The following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="c1c5d-122">Pobierz widok grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c1c5d-122">Retrieve security group view</span></span>

<span data-ttu-id="c1c5d-123">Następnym krokiem jest do pobierania wyników widoku grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-123">The next step is to retrieve the security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-the-results"></a><span data-ttu-id="c1c5d-124">Wyświetlanie wyników</span><span class="sxs-lookup"><span data-stu-id="c1c5d-124">Viewing the results</span></span>

<span data-ttu-id="c1c5d-125">Poniższy przykład jest skróconą odpowiedzi wyników zwróconych.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="c1c5d-126">Wyniki Pokaż wszystkie reguły zabezpieczeń skuteczne i zastosowane na maszynie wirtualnej podziale grupy **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, i **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```
NetworkInterfaces : [
                      {
                        "NetworkInterfaceSecurityRules": [
                          {
                            "Name": "default-allow-rdp",
                            "Etag": "W/\"d4c411d4-0d62-49dc-8092-3d4b57825740\"",
                            "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/securityRules/default-allow-rdp",
                            "Protocol": "TCP",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "3389",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "Access": "Allow",
                            "Priority": 1000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "DefaultSecurityRules": [
                          {
                            "Name": "AllowVnetInBound",
                            "Id": "/subscriptions00000000-0000-0000-0000-000000000000/resourceGroups/testrg2/providers/Microsoft.Network/networkSecurityGroups/testvm2-nsg/defaultSecurityRules/",
                            "Description": "Allow inbound traffic from all VMs in VNET",
                            "Protocol": "*",
                            "SourcePortRange": "*",
                            "DestinationPortRange": "*",
                            "SourceAddressPrefix": "VirtualNetwork",
                            "DestinationAddressPrefix": "VirtualNetwork",
                            "Access": "Allow",
                            "Priority": 65000,
                            "Direction": "Inbound",
                            "ProvisioningState": "Succeeded"
                          }
                          ...
                        ],
                        "EffectiveSecurityRules": [
                          {
                            "Name": "DefaultOutboundDenyAll",
                            "Protocol": "All",
                            "SourcePortRange": "0-65535",
                            "DestinationPortRange": "0-65535",
                            "SourceAddressPrefix": "*",
                            "DestinationAddressPrefix": "*",
                            "ExpandedSourceAddressPrefix": [],
                            "ExpandedDestinationAddressPrefix": [],
                            "Access": "Deny",
                            "Priority": 65500,
                            "Direction": "Outbound"
                          },
                          ...
                        ]
                      }
                    ]
```

## <a name="next-steps"></a><span data-ttu-id="c1c5d-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1c5d-127">Next steps</span></span>

<span data-ttu-id="c1c5d-128">Odwiedź stronę [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md) sposób automatyzacji sprawdzania poprawności grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="c1c5d-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>


