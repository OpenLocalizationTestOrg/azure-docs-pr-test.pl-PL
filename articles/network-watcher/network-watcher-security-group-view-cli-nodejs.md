---
title: "Analizowanie zabezpieczeń sieci z widokiem grupy obserwatora zabezpieczeń Azure sieci - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób użycia interfejsu wiersza polecenia platformy Azure w wersji 1.0 do analizy zabezpieczeń maszyn wirtualnych z widokiem grupy zabezpieczeń."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: a986ff4f-7e0c-4994-95e1-4ac824986500
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2c4c494dcc4fe1a85c5feb29506c35fb03066479
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="63e37-103">Analizowanie zabezpieczeń maszyny wirtualnej z widoku grupy zabezpieczeń przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="63e37-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="63e37-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="63e37-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="63e37-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="63e37-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="63e37-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="63e37-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="63e37-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="63e37-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="63e37-108">Widok grupy zabezpieczeń zwraca reguły zabezpieczeń sieci skonfigurowane i skuteczne, które są stosowane do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="63e37-108">Security group view returns configured and effective network security rules that are applied to a virtual machine.</span></span> <span data-ttu-id="63e37-109">Ta funkcja jest przydatna do inspekcji i diagnostyki sieciowych grup zabezpieczeń i reguł, które są skonfigurowane na maszynie Wirtualnej dla zapewnienia ruchu jest poprawnie dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="63e37-109">This capability is useful to audit and diagnose Network Security Groups and rules that are configured on a VM to ensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="63e37-110">W tym artykule firma Microsoft opisano, jak pobrać zasady zabezpieczeń skonfigurowane i skuteczne z maszyną wirtualną za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="63e37-110">In this article, we show you how to retrieve the configured and effective security rules to a virtual machine using Azure CLI</span></span>

<span data-ttu-id="63e37-111">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="63e37-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="63e37-112">Obserwatora sieciowego aktualnie używa interfejsu wiersza polecenia platformy Azure w wersji 1.0 do obsługi interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="63e37-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="63e37-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="63e37-113">Before you begin</span></span>

<span data-ttu-id="63e37-114">W tym scenariuszu przyjęto zostały już wykonane kroki przedstawione w [utworzyć obserwatora sieciowego](network-watcher-create.md) utworzyć obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="63e37-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="63e37-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="63e37-115">Scenario</span></span>

<span data-ttu-id="63e37-116">Scenariusz omówione w tym artykule pobiera reguły zabezpieczeń skonfigurowane i efektywny dla podanej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="63e37-116">The scenario covered in this article retrieves the configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="63e37-117">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="63e37-117">Get a VM</span></span>

<span data-ttu-id="63e37-118">Maszyna wirtualna jest wymagana do uruchamiania `vm list` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="63e37-118">A virtual machine is required to run the `vm list` cmdlet.</span></span> <span data-ttu-id="63e37-119">Następujące polecenie wyświetla listę wirtualnych machinese w grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="63e37-119">The following command lists the virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="63e37-120">Jeśli znasz już maszyny wirtualnej, można użyć `vm show` polecenia cmdlet, aby pobrać jego identyfikator zasobu:</span><span class="sxs-lookup"><span data-stu-id="63e37-120">Once you know the virtual machine, you can use the `vm show` cmdlet to get its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="63e37-121">Pobierz widok grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="63e37-121">Retrieve security group view</span></span>

<span data-ttu-id="63e37-122">Następnym krokiem jest do pobierania wyników widoku grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="63e37-122">The next step is to retrieve the security group view result.</span></span> <span data-ttu-id="63e37-123">Dodawanie "--json" flagi sformatuje wyniki w formacie json.</span><span class="sxs-lookup"><span data-stu-id="63e37-123">Adding the "--json" flag will format the results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-the-results"></a><span data-ttu-id="63e37-124">Wyświetlanie wyników</span><span class="sxs-lookup"><span data-stu-id="63e37-124">Viewing the results</span></span>

<span data-ttu-id="63e37-125">Poniższy przykład jest skróconą odpowiedzi wyników zwróconych.</span><span class="sxs-lookup"><span data-stu-id="63e37-125">The following example is a shortened response of the results returned.</span></span> <span data-ttu-id="63e37-126">Wyniki Pokaż wszystkie reguły zabezpieczeń skuteczne i zastosowane na maszynie wirtualnej podziale grupy **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, i **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="63e37-126">The results show all the effective and applied security rules on the virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

```json
{
  "networkInterfaces": [
    {
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testnic",
      "securityRuleAssociations": {
        "networkInterfaceAssociation": {
          "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testvm",
          "securityRules": [
            {
              "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/test-nsg/securityRules/default-allow-rdp",
              "protocol": "TCP",
              "sourcePortRange": "*",
              "destinationPortRange": "3389",
              "sourceAddressPrefix": "*",
              "destinationAddressPrefix": "*",
              "access": "Allow",
              "priority": 1000,
              "direction": "Inbound",
              "provisioningState": "Succeeded",
              "name": "default-allow-rdp",
              "etag": "W/\"00000000-0000-0000-0000-000000000000\""
            }
          ]
        },
        "defaultSecurityRules": [
          {
            "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/networkSecurityGroups//defaultSecurityRules/",
            "description": "Allow inbound traffic from all VMs in VNET",
            "protocol": "*",
            "sourcePortRange": "*",
            "destinationPortRange": "*",
            "sourceAddressPrefix": "VirtualNetwork",
            "destinationAddressPrefix": "VirtualNetwork",
            "access": "Allow",
            "priority": 65000,
            "direction": "Inbound",
            "provisioningState": "Succeeded",
            "name": "AllowVnetInBound"
          }
        ]
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="63e37-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="63e37-127">Next steps</span></span>

<span data-ttu-id="63e37-128">Odwiedź stronę [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md) sposób automatyzacji sprawdzania poprawności grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="63e37-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) to learn how to automate validation of Network Security Groups.</span></span>

<span data-ttu-id="63e37-129">Dowiedz się więcej na temat reguł zabezpieczeń, które są stosowane do zasobów sieciowych, odwiedzając [Omówienie widoku grupy zabezpieczeń](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="63e37-129">Learn more about the security rules that are applied to your network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
