---
title: "Wymuszanie zabezpieczeń przy użyciu zasad na maszynach wirtualnych systemu Windows na platformie Azure | Dokumentacja firmy Microsoft"
description: "Sposób stosowania zasad do Menedżera zasobów systemu Windows maszyny wirtualnej platformy Azure"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0b71ba54-01db-43ad-9bca-8ab358ae141b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: kasing
ms.openlocfilehash: 246f5958478fd6d9afc9ba990413ab08429bd25d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="apply-policies-to-windows-vms-with-azure-resource-manager"></a><span data-ttu-id="11139-103">Stosowania zasad do maszyn wirtualnych systemu Windows z usługą Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="11139-103">Apply policies to Windows VMs with Azure Resource Manager</span></span>
<span data-ttu-id="11139-104">Korzystając z zasad, organizacja może wymusić różnych konwencje i zasady w całym przedsiębiorstwie.</span><span class="sxs-lookup"><span data-stu-id="11139-104">By using policies, an organization can enforce various conventions and rules throughout the enterprise.</span></span> <span data-ttu-id="11139-105">Wymuszanie zachowanie można zmniejszenia ryzyka podczas pracy nad dla sukcesu organizacji.</span><span class="sxs-lookup"><span data-stu-id="11139-105">Enforcement of the desired behavior can help mitigate risk while contributing to the success of the organization.</span></span> <span data-ttu-id="11139-106">W tym artykule opisano sposób można użyć zasad usługi Azure Resource Manager do definiowania zachowanie w przypadku maszyn wirtualnych w organizacji.</span><span class="sxs-lookup"><span data-stu-id="11139-106">In this article, we describe how you can use Azure Resource Manager policies to define the desired behavior for your organization’s Virtual Machines.</span></span>

<span data-ttu-id="11139-107">Aby obejrzeć wprowadzenie do zasad, zobacz [używanie zasad do zarządzania zasobami i kontrola dostępu](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="11139-107">For an introduction to policies, see [Use Policy to manage resources and control access](../../azure-resource-manager/resource-manager-policy.md).</span></span>

## <a name="permitted-virtual-machines"></a><span data-ttu-id="11139-108">Dozwolone maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="11139-108">Permitted Virtual Machines</span></span>
<span data-ttu-id="11139-109">Aby upewnić się, że maszyny wirtualne w Twojej organizacji są zgodne z aplikacji, można ograniczyć dozwolonych systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="11139-109">To ensure that virtual machines for your organization are compatible with an application, you can restrict the permitted operating systems.</span></span> <span data-ttu-id="11139-110">W poniższym przykładzie zasad musisz zezwolić na tylko systemu Windows Server 2012 R2 Datacenter maszyn wirtualnych należy utworzyć:</span><span class="sxs-lookup"><span data-stu-id="11139-110">In the following policy example, you allow only Windows Server 2012 R2 Datacenter Virtual Machines to be created:</span></span>

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
                "MicrosoftWindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageOffer",
              "in": [
                "WindowsServer"
              ]
            },
            {
              "field": "Microsoft.Compute/imageSku",
              "in": [
                "2012-R2-Datacenter"
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

<span data-ttu-id="11139-111">Użyj symbolu wieloznacznego, aby zmodyfikować poprzedniego zasadę, aby dopuścić żadnego obrazu systemu Windows Server Datacenter:</span><span class="sxs-lookup"><span data-stu-id="11139-111">Use a wild card to modify the preceding policy to allow any Windows Server Datacenter image:</span></span>

```json
{
  "field": "Microsoft.Compute/imageSku",
  "like": "*Datacenter"
}
```

<span data-ttu-id="11139-112">Użyj anyOf zmodyfikować zasady poprzedniego zezwalająca na wszystkie Windows Server 2012 R2 Datacenter lub wyższej obrazu:</span><span class="sxs-lookup"><span data-stu-id="11139-112">Use anyOf to modify the preceding policy to allow any Windows Server 2012 R2 Datacenter or higher image:</span></span>

```json
{
  "anyOf": [
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2012-R2-Datacenter*"
    },
    {
      "field": "Microsoft.Compute/imageSku",
      "like": "2016-Datacenter*"
    }
  ]
}
```

<span data-ttu-id="11139-113">Aby uzyskać informacji o polach zasad, zobacz [aliasy zasad](../../azure-resource-manager/resource-manager-policy.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="11139-113">For information about policy fields, see [Policy aliases](../../azure-resource-manager/resource-manager-policy.md#aliases).</span></span>

## <a name="managed-disks"></a><span data-ttu-id="11139-114">Dyski zarządzane</span><span class="sxs-lookup"><span data-stu-id="11139-114">Managed disks</span></span>

<span data-ttu-id="11139-115">Aby wymagać używania dysków zarządzanych, należy użyć następujące zasady:</span><span class="sxs-lookup"><span data-stu-id="11139-115">To require the use of managed disks, use the following policy:</span></span>

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

## <a name="images-for-virtual-machines"></a><span data-ttu-id="11139-116">Obrazy maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="11139-116">Images for Virtual Machines</span></span>

<span data-ttu-id="11139-117">Ze względów bezpieczeństwa może wymagać, aby zatwierdzone niestandardowych obrazów są wdrażane w środowisku.</span><span class="sxs-lookup"><span data-stu-id="11139-117">For security reasons, you can require that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="11139-118">Można określić albo grupę zasobów, która zawiera obrazy zatwierdzone lub konkretnym zatwierdzone obrazów.</span><span class="sxs-lookup"><span data-stu-id="11139-118">You can specify either the resource group that contains the approved images, or the specific approved images.</span></span>

<span data-ttu-id="11139-119">Poniższy przykład wymaga obrazów z grupy zasobów zatwierdzonych:</span><span class="sxs-lookup"><span data-stu-id="11139-119">The following example requires images from an approved resource group:</span></span>

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

<span data-ttu-id="11139-120">W poniższym przykładzie identyfikatorów zatwierdzonych obrazu:</span><span class="sxs-lookup"><span data-stu-id="11139-120">The following example specifies the approved image IDs:</span></span>

```json
{
    "field": "Microsoft.Compute/imageId",
    "in": ["{imageId1}","{imageId2}"]
}
```

## <a name="virtual-machine-extensions"></a><span data-ttu-id="11139-121">Rozszerzenia maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="11139-121">Virtual Machine extensions</span></span>

<span data-ttu-id="11139-122">Może zajść potrzeba zabraniać użycia pewnych typów rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="11139-122">You may want to forbid usage of certain types of extensions.</span></span> <span data-ttu-id="11139-123">Na przykład rozszerzenie nie może być zgodna z niektórych obrazy niestandardowe maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="11139-123">For example, an extension may not be compatible with certain custom virtual machine images.</span></span> <span data-ttu-id="11139-124">Poniższy przykład pokazuje, jak mają być blokowane z określonym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="11139-124">The following example shows how to block a specific extension.</span></span> <span data-ttu-id="11139-125">Aby określić, które rozszerzenia, aby zablokować używa wydawcy i typu.</span><span class="sxs-lookup"><span data-stu-id="11139-125">It uses publisher and type to determine which extension to block.</span></span>

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


## <a name="azure-hybrid-use-benefit"></a><span data-ttu-id="11139-126">Korzyści Użyj hybrydowe platformy Azure</span><span class="sxs-lookup"><span data-stu-id="11139-126">Azure Hybrid Use Benefit</span></span>

<span data-ttu-id="11139-127">Gdy użytkownik ma licencję lokalnie, można zapisać opłata licencji na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="11139-127">When you have an on-premise license, you can save the license fee on your virtual machines.</span></span> <span data-ttu-id="11139-128">Jeśli nie masz licencji, należy zabraniać opcji.</span><span class="sxs-lookup"><span data-stu-id="11139-128">When you don't have the license, you should forbid the option.</span></span> <span data-ttu-id="11139-129">Następujące zasady zabrania użycia korzyści Użyj Azure hybrydowych (AHUB):</span><span class="sxs-lookup"><span data-stu-id="11139-129">The following policy forbids usage of Azure Hybrid Use Benefit (AHUB):</span></span>

```json
{
    "if": {
        "allOf": [
            {
                "field": "type",
                "in":[ "Microsoft.Compute/virtualMachines","Microsoft.Compute/VirtualMachineScaleSets"]
            },
            {
                "field": "Microsoft.Compute/licenseType",
                "exists": true
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="11139-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="11139-130">Next steps</span></span>
* <span data-ttu-id="11139-131">Po zdefiniowaniu reguły zasad (jak pokazano w powyższych przykładach), należy utworzyć definicji zasad i przypisać je do zakresu.</span><span class="sxs-lookup"><span data-stu-id="11139-131">After defining a policy rule (as shown in the preceding examples), you need to create the policy definition and assign it to a scope.</span></span> <span data-ttu-id="11139-132">Zakres może być subskrypcji, grupy zasobów lub zasobów.</span><span class="sxs-lookup"><span data-stu-id="11139-132">The scope can be a subscription, resource group, or resource.</span></span> <span data-ttu-id="11139-133">Aby przypisać zasady za pośrednictwem portalu, zobacz [portal Azure używany do przypisywania i zarządzanie zasadami zasobów](../../azure-resource-manager/resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11139-133">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](../../azure-resource-manager/resource-manager-policy-portal.md).</span></span> <span data-ttu-id="11139-134">Aby przypisać zasady za pomocą interfejsu API REST, programu PowerShell lub interfejsu wiersza polecenia Azure, zobacz [przypisania zasad i zarządzania nimi za pośrednictwem skryptu](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="11139-134">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](../../azure-resource-manager/resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="11139-135">Aby obejrzeć wprowadzenie do zasad zasobów, zobacz [Przegląd zasad zasobów](../../azure-resource-manager/resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="11139-135">For an introduction to resource policies, see [Resource policy overview](../../azure-resource-manager/resource-manager-policy.md).</span></span>
* <span data-ttu-id="11139-136">Aby uzyskać instrukcje dla przedsiębiorstw dotyczące użycia usługi Resource Manager w celu efektywnego zarządzania subskrypcjami, zobacz [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md) (Szkielet platformy Azure dla przedsiębiorstwa — narzucony nadzór subskrypcji).</span><span class="sxs-lookup"><span data-stu-id="11139-136">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](../../azure-resource-manager/resource-manager-subscription-governance.md).</span></span>
