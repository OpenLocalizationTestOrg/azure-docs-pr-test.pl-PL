---
title: "zabezpieczenia sieci aaaAnalyze z widokiem grupy obserwatorów zabezpieczeń Azure sieci - Azure CLI 1.0 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooanalyze toouse 1.0 interfejsu wiersza polecenia Azure, a wirtualnych maszyn zabezpieczeń z widokiem grupy zabezpieczeń."
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
ms.openlocfilehash: 96383a734b94d215d5b0f3d47339e46940d700b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-your-virtual-machine-security-with-security-group-view-using-azure-cli-10"></a><span data-ttu-id="7c0c0-103">Analizowanie zabezpieczeń maszyny wirtualnej z widoku grupy zabezpieczeń przy użyciu interfejsu wiersza polecenia platformy Azure w wersji 1.0</span><span class="sxs-lookup"><span data-stu-id="7c0c0-103">Analyze your Virtual Machine security with Security Group View using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="7c0c0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c0c0-104">PowerShell</span></span>](network-watcher-security-group-view-powershell.md)
> - [<span data-ttu-id="7c0c0-105">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="7c0c0-105">CLI 1.0</span></span>](network-watcher-security-group-view-cli-nodejs.md)
> - [<span data-ttu-id="7c0c0-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="7c0c0-106">CLI 2.0</span></span>](network-watcher-security-group-view-cli.md)
> - [<span data-ttu-id="7c0c0-107">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="7c0c0-107">REST API</span></span>](network-watcher-security-group-view-rest.md)

<span data-ttu-id="7c0c0-108">Widok grupy zabezpieczeń zwraca reguły zabezpieczeń sieci skonfigurowane i skuteczne, które są stosowane tooa maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-108">Security group view returns configured and effective network security rules that are applied tooa virtual machine.</span></span> <span data-ttu-id="7c0c0-109">Ta funkcja jest przydatna tooaudit i diagnozowanie grup zabezpieczeń sieci i reguł, które są skonfigurowane na ruch tooensure maszyn wirtualnych są poprawnie dozwolony lub niedozwolony.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-109">This capability is useful tooaudit and diagnose Network Security Groups and rules that are configured on a VM tooensure traffic is being correctly allowed or denied.</span></span> <span data-ttu-id="7c0c0-110">W tym artykule możemy wyświetlić konfiguracji tooretrieve hello i efektywnym elementem systemu zabezpieczeń reguły tooa maszyny wirtualnej za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c0c0-110">In this article, we show you how tooretrieve hello configured and effective security rules tooa virtual machine using Azure CLI</span></span>

<span data-ttu-id="7c0c0-111">W tym artykule wykorzystano 1.0 interfejsu wiersza polecenia platformy Azure i platform, która jest dostępna dla systemu Windows, Mac i Linux.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="7c0c0-112">Obserwatora sieciowego aktualnie używa interfejsu wiersza polecenia platformy Azure w wersji 1.0 do obsługi interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7c0c0-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="7c0c0-113">Before you begin</span></span>

<span data-ttu-id="7c0c0-114">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="7c0c0-115">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="7c0c0-115">Scenario</span></span>

<span data-ttu-id="7c0c0-116">Scenariusz Hello omówione w tym artykule pobiera hello skonfigurowane i reguły efektywnym elementem systemu zabezpieczeń dla podanej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-116">hello scenario covered in this article retrieves hello configured and effective security rules for a given virtual machine.</span></span>

## <a name="get-a-vm"></a><span data-ttu-id="7c0c0-117">Uzyskiwanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7c0c0-117">Get a VM</span></span>

<span data-ttu-id="7c0c0-118">Maszyna wirtualna jest wymagana toorun hello `vm list` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-118">A virtual machine is required toorun hello `vm list` cmdlet.</span></span> <span data-ttu-id="7c0c0-119">Witaj następujące polecenie wyświetla listę hello machinese wirtualne w grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="7c0c0-119">hello following command lists hello virtual machinese in a resource group:</span></span>

```azurecli
azure vm list -g resourceGroupName
```

<span data-ttu-id="7c0c0-120">Jeśli znasz już hello maszyny wirtualnej, można użyć hello `vm show` tooget polecenia cmdlet jego identyfikator zasobu:</span><span class="sxs-lookup"><span data-stu-id="7c0c0-120">Once you know hello virtual machine, you can use hello `vm show` cmdlet tooget its resource Id:</span></span>

```azurecli
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="retrieve-security-group-view"></a><span data-ttu-id="7c0c0-121">Pobierz widok grupy zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="7c0c0-121">Retrieve security group view</span></span>

<span data-ttu-id="7c0c0-122">Witaj następnym krokiem jest wynik widoku tooretrieve hello zabezpieczeń grupy.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-122">hello next step is tooretrieve hello security group view result.</span></span> <span data-ttu-id="7c0c0-123">Dodawanie hello "--json" flagi sformatuje hello wyniki w formacie json.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-123">Adding hello "--json" flag will format hello results in json.</span></span>

```azurecli
azure network watcher security-group-view -g resourceGroupName -n networkWatcherName -t targetResourceId --json
```

## <a name="viewing-hello-results"></a><span data-ttu-id="7c0c0-124">Wyświetlanie wyników hello</span><span class="sxs-lookup"><span data-stu-id="7c0c0-124">Viewing hello results</span></span>

<span data-ttu-id="7c0c0-125">Witaj poniższy przykład jest skróconą odpowiedzi hello wyniki zwrócone.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-125">hello following example is a shortened response of hello results returned.</span></span> <span data-ttu-id="7c0c0-126">Witaj w wynikach wszystkich reguł zabezpieczeń skuteczne i zastosowane hello na maszynie wirtualnej hello podziale grupy **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, i  **EffectiveSecurityRules**.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-126">hello results show all hello effective and applied security rules on hello virtual machine broken down in groups of **NetworkInterfaceSecurityRules**, **DefaultSecurityRules**, and **EffectiveSecurityRules**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7c0c0-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c0c0-127">Next steps</span></span>

<span data-ttu-id="7c0c0-128">Odwiedź stronę [inspekcji sieci zabezpieczeń grupy (NSG) z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md) toolearn sposób weryfikacji tooautomate grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="7c0c0-128">Visit [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md) toolearn how tooautomate validation of Network Security Groups.</span></span>

<span data-ttu-id="7c0c0-129">Dowiedz się więcej o hello reguły zabezpieczeń, które są stosowane tooyour zasobów sieciowych, odwiedzając [Omówienie widoku grupy zabezpieczeń](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7c0c0-129">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
