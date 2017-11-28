---
title: "zabezpieczenia sieci aaaAnalyze z widokiem grupy obserwatorów zabezpieczeń Azure sieci - PowerShell | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toouse tooanalyze programu PowerShell, a wirtualnych maszyn zabezpieczeń z widokiem grupy zabezpieczeń."
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
ms.openlocfilehash: 5e1990d97899bd8585025ec13dd556ab2e034c3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-powershell"></a><span data-ttu-id="861c6-103">Analizowanie zabezpieczeń maszyny wirtualnej z widokiem grupy zabezpieczeń przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="861c6-103">Analyze your Virtual Machine security with Security Group View using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="861c6-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="861c6-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="861c6-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="861c6-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="861c6-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="861c6-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="861c6-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="861c6-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="861c6-108">Widok grupy zabezpieczeń zwraca reguły zabezpieczeń sieci skonfigurowane i skuteczne, które są stosowane tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="861c6-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="861c6-109">Ta funkcja jest przydatna tooaudit i diagnozowanie grup zabezpieczeń sieci i reguł, które są skonfigurowane na ruch tooensure maszyn wirtualnych są poprawnie dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="861c6-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="861c6-110">W tym artykule możemy wyświetlić konfiguracji tooretrieve hello i efektywnym elementem systemu zabezpieczeń reguły tooa maszyny wirtualnej przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="861c6-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using PowerShell</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="861c6-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="861c6-111">Before you begin</span></span>

<span data-ttu-id="861c6-112">W tym scenariuszu można uruchomić hello `Get-AzureRmNetworkWatcherSecurityGroupView` danych reguły zabezpieczeń hello tooretrieve polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="861c6-112">In this scenario, you run hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet tooretrieve hello security rule information.</span></span>

<span data-ttu-id="861c6-113">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="861c6-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="861c6-114">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="861c6-114">Scenario</span></span>

<span data-ttu-id="861c6-115">Scenariusz Hello omówione w tym artykule pobiera hello skonfigurowane i reguły efektywnym elementem systemu zabezpieczeń dla podanej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="861c6-115">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="861c6-116">Pobrać obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="861c6-116">Retrieve Network Watcher</span></span>

<span data-ttu-id="861c6-117">pierwszym krokiem Hello jest tooretrieve hello obserwatora sieciowego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="861c6-117">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="861c6-118">Ta zmienna jest przekazywana toohello `Get-AzureRmNetworkWatcherSecurityGroupView` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="861c6-118">This variable is passed toohello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="get-a-vm"></a><span data-ttu-id="861c6-119">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="861c6-119">Get a VM</span></span>

<span data-ttu-id="861c6-120">Maszyna wirtualna jest wymagana toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` polecenia cmdlet przed.</span><span class="sxs-lookup"><span data-stu-id="861c6-120">A virtual machine is required toorun hello `Get-AzureRmNetworkWatcherSecurityGroupView` cmdlet against.</span></span> <span data-ttu-id="861c6-121">Poniższy przykład Hello pobiera obiekt maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="861c6-121">hello following example gets a VM object.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName testrg -Name testvm1
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="861c6-122">Pobierz widok grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="861c6-122">Retrieve security group view</span></span>

<span data-ttu-id="861c6-123">Witaj następnym krokiem jest wynik widoku tooretrieve hello zabezpieczeń grupy.</span><span class="sxs-lookup"><span data-stu-id="861c6-123">hello next step is tooretrieve hello security group view result.</span></span>

```powershell
$secgroup = Get-AzureRmNetworkWatcherSecurityGroupView -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id
```

## <a name="viewing-hello-results"></a><span data-ttu-id="861c6-124">Wyświetlanie wyników hello</span><span class="sxs-lookup"><span data-stu-id="861c6-124">Viewing hello results</span></span>

<span data-ttu-id="861c6-125">Witaj poniższy przykład jest skróconą odpowiedzi hello wyniki zwrócone.</span><span class="sxs-lookup"><span data-stu-id="861c6-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="861c6-126">Witaj w wynikach wszystkich reguł zabezpieczeń skuteczne i zastosowane hello na maszynie wirtualnej hello podziale grupy **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, i  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="861c6-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="861c6-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="861c6-127">Next steps</span></span>

<span data-ttu-id="861c6-128">Odwiedź stronę [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md) toolearn sposób weryfikacji tooautomate grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="861c6-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>


