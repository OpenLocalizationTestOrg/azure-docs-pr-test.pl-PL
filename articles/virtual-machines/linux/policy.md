---
title: "aaaEnforce zabezpieczeń przy użyciu zasad na maszynach wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "Jak tooapply tooan zasad maszyny wirtualnej systemu Linux Menedżera zasobów Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 06778ab4-f8ff-4eed-ae10-26a276fc3faa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: singhkay
ms.openlocfilehash: 5abd0c937578aba7e72b62c65b4eef9a9737aa2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-policies-toolinux-vms-with-azure-resource-manager"></a><span data-ttu-id="c863c-103">Zastosuj zasady tooLinux maszyn wirtualnych z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c863c-103">Apply policies tooLinux VMs with Azure Resource Manager</span></span>
<span data-ttu-id="c863c-104">Przy użyciu zasad, organizacja może wymusić różnych konwencje i reguł w całej organizacji hello.</span><span class="sxs-lookup"><span data-stu-id="c863c-104">By using policies, an organization can enforce various conventions and rules throughout hello enterprise.</span></span> <span data-ttu-id="c863c-105">Wymuszanie hello żądanego zachowania można zmniejszenia ryzyka podczas pracy nad powodzeniu toohello organizacji hello.</span><span class="sxs-lookup"><span data-stu-id="c863c-105">Enforcement of hello desired behavior can help mitigate risk while contributing toohello success of hello organization.</span></span> <span data-ttu-id="c863c-106">W tym artykule opisano sposób korzystania zachowanie hello potrzeby toodefine zasady usługi Azure Resource Manager dla maszyn wirtualnych w organizacji.</span><span class="sxs-lookup"><span data-stu-id="c863c-106">In this article, we describe how you can use Azure Resource Manager policies toodefine hello desired behavior for your organization's Virtual Machines.</span></span>

<span data-ttu-id="c863c-107">Dla toopolicies wprowadzenie [zasady toomanage zasobów i kontroli dostępu](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c863c-107">For an introduction toopolicies, see [Use Policy toomanage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="c863c-108">Dozwolone maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="c863c-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="c863c-109">tooensure, że maszyny wirtualne w Twojej organizacji są zgodne z aplikacji, można ograniczyć hello dozwolone systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c863c-109">tooensure that virtual machines for your organization are compatible with an application, you can restrict hello permitted operating systems.</span></span> <span data-ttu-id="c863c-110">Poniższy przykład zasad hello, pozwala tylko Ubuntu maszyn wirtualnych 14.04.2-LTS toobe utworzony.</span><span class="sxs-lookup"><span data-stu-id="c863c-110">In hello following policy example, you allow only Ubuntu 14.04.2-LTS Virtual Machines toobe created.</span></span>

```json
{
  "if": {
    "allOf": [
      {
        "field": "type",
        "in": [
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/VirtualMachineScaleSets"
        ]
      },
      {
        "not": {
          "allOf": [
            {
              "field": "Microsoft.Compute/imagePublisher",
              "in": [
                "Canonical"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "UbuntuServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "14.04.2-LTS"
              ]
            },
            {
              "field": "Microsoft.Compute/imageVersion",
              "in": [
                "latest"
              ]
            }
          ]
        }
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

<span data-ttu-id="c863c-111">Użyj hello toomodify przy użyciu symboli wieloznacznych, poprzedzających żadnego obrazu Ubuntu LTS tooallow zasad:</span><span class="sxs-lookup"><span data-stu-id="c863c-111">Use a wild card toomodify hello preceding policy tooallow any Ubuntu LTS image:</span></span> 

```json
{
  "field": "Microsoft.Compute/virtualMachines/imageSku",
  "like": "*LTS"
}
```

<span data-ttu-id="c863c-112">Aby uzyskać informacji o polach zasad, zobacz [aliasy zasad](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="c863c-112">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="c863c-113">Dyski zarządzane</span><span class="sxs-lookup"><span data-stu-id="c863c-113">Managed disks</span></span>

<span data-ttu-id="c863c-114">toorequire hello użycie zarządzanego dysku, użyj hello następujące zasady:</span><span class="sxs-lookup"><span data-stu-id="c863c-114">toorequire hello use of managed disks, use hello following policy:</span></span>

```json
{
  "if": {
    "anyOf": [
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/virtualMachines"
          },
          {
            "field": "Microsoft.Compute/virtualMachines/osDisk.uri",
            "exists": true
          }
        ]
      },
      {
        "allOf": [
          {
            "field": "type",
            "equals": "Microsoft.Compute/VirtualMachineScaleSets"
          },
          {
            "anyOf": [
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osDisk.vhdContainers",
                "exists": true
              },
              {
                "field": "Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl",
                "exists": true
              }
            ]
          }
        ]
      }
    ]
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="images-for-virtual-machines"></a><span data-ttu-id="c863c-115">Obrazy maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="c863c-115">Images for Virtual Machines</span></span>

<span data-ttu-id="c863c-116">Ze względów bezpieczeństwa może wymagać, aby zatwierdzone niestandardowych obrazów są wdrażane w środowisku.</span><span class="sxs-lookup"><span data-stu-id="c863c-116">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="c863c-117">Można określić hello grupę zasobów, która zawiera obrazy zatwierdzone hello lub hello określonych obrazy zatwierdzone.</span><span class="sxs-lookup"><span data-stu-id="c863c-117">You can specify either hello resource group that contains hello approved images, or hello specific approved images.</span></span>

<span data-ttu-id="c863c-118">Poniższy przykład Hello wymaga obrazów z grupy zasobów zatwierdzonych:</span><span class="sxs-lookup"><span data-stu-id="c863c-118">hello following example requires images from an approved resource group:</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in": [
                    "Microsoft.Compute/virtualMachines",
                    "Microsoft.Compute/VirtualMachineScaleSets"
                ]
            },
            {
                "not": {
                    "field": "Microsoft.Compute/imageId",
                    "contains": "resourceGroups/CustomImage"
                }
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
} 
```

<span data-ttu-id="c863c-119">Witaj poniższy przykład określa hello zatwierdzony obraz identyfikatory:</span><span class="sxs-lookup"><span data-stu-id="c863c-119">hello following example specifies hello approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="c863c-120">Rozszerzenia maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="c863c-120">Virtual Machine extensions</span></span>

<span data-ttu-id="c863c-121">Może być użycie tooforbid niektórych typów rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="c863c-121">You may want tooforbid usage of certain types of extensions.</span></span> <span data-ttu-id="c863c-122">Na przykład rozszerzenie nie może być zgodna z niektórych obrazy niestandardowe maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c863c-122">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="c863c-123">powitania po przykładzie pokazano, jak tooblock określonym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="c863c-123">hello following example shows how tooblock a specific extension.</span></span> <span data-ttu-id="c863c-124">Używa toodetermine wydawcy i typ które tooblock rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="c863c-124">It uses publisher and type toodetermine which extension tooblock.</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "equals": "Microsoft.Compute/virtualMachines/extensions"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                "equals": "Microsoft.Compute"
            },
            {
                "field": "Microsoft.Compute/virtualMachines/extensions/type",
                "equals": "{extension-type}"

      }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="c863c-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c863c-125">Next steps</span></span>
* <span data-ttu-id="c863c-126">Po zdefiniowaniu reguły zasad (jak pokazano w hello poprzedzających przykłady), wymagają definicji zasad hello toocreate i przypisz do niego tooa zakresu.</span><span class="sxs-lookup"><span data-stu-id="c863c-126">After defining a policy rule (as shown in hello preceding examples), you need toocreate hello policy definition and assign it tooa scope.</span></span> <span data-ttu-id="c863c-127">zakres Hello można subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="c863c-127">hello scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="c863c-128">Zobacz zasady tooassign za pośrednictwem portalu hello [tooassign portalu Azure użycia zasad zasobów i zarządzanie nimi](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c863c-128">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="c863c-129">zasady tooassign za pośrednictwem interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="c863c-129">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="c863c-130">Wprowadzenie tooresource zasad, zobacz [Przegląd zasad zasobów](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="c863c-130">For an introduction tooresource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="c863c-131">Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](../../azure-resource-manager/resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="c863c-131">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
