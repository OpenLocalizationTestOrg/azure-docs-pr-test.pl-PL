---
title: "Definicja zasobu podrzędnego w szablonie Azure | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak ustawić typ zasobu i nazwę zasobu podrzędnego w szablonie usługi Azure Resource Manager"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="1c653-103">Ustaw nazwę i typ zasobu podrzędnego w szablonie usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1c653-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="1c653-104">Podczas tworzenia szablonu, często konieczne jest uwzględnienie zasobu podrzędnego, która jest powiązana z zasobem nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="1c653-104">When creating a template, you frequently need to include a child resource that is related to a parent resource.</span></span> <span data-ttu-id="1c653-105">Na przykład do szablonu może zawierać programu SQL server i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="1c653-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="1c653-106">Serwer SQL jest zasobem nadrzędnej, a baza danych jest zasobu podrzędnego.</span><span class="sxs-lookup"><span data-stu-id="1c653-106">The SQL server is the parent resource, and the database is the child resource.</span></span> 

<span data-ttu-id="1c653-107">Format podrzędny typ zasobu jest:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="1c653-107">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="1c653-108">Format podrzędny Nazwa zasobu jest:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="1c653-108">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="1c653-109">Jednak należy określić typ i nazwa w szablonie inaczej na podstawie tego, czy jest zagnieżdżony w obrębie zasobu nadrzędnego, lub na jego własnej na najwyższym poziomie.</span><span class="sxs-lookup"><span data-stu-id="1c653-109">However, you specify the type and name in a template differently based on whether it is nested within the parent resource, or on its own at the top level.</span></span> <span data-ttu-id="1c653-110">W tym temacie przedstawiono sposób obsługi obu podejść.</span><span class="sxs-lookup"><span data-stu-id="1c653-110">This topic shows how to handle both approaches.</span></span>

<span data-ttu-id="1c653-111">Podczas konstruowania pełni kwalifikowane odwołanie do zasobu, aby połączyć segmenty z typem i nazwą nie jest po prostu składa się z dwóch.</span><span class="sxs-lookup"><span data-stu-id="1c653-111">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name  is not simply a concatenation of the two.</span></span>  <span data-ttu-id="1c653-112">Po obszarze nazw, użyj sekwencji *typ/nazwa* pary z najmniej specyficznych, które specyficzny:</span><span class="sxs-lookup"><span data-stu-id="1c653-112">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="1c653-113">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1c653-113">For example:</span></span>

<span data-ttu-id="1c653-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`jest poprawna `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="1c653-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="1c653-115">Zasób zagnieżdżonych elementów podrzędnych</span><span class="sxs-lookup"><span data-stu-id="1c653-115">Nested child resource</span></span>
<span data-ttu-id="1c653-116">Najprostszym sposobem definiowania zasobu podrzędnego jest zagnieździć w obrębie zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="1c653-116">The easiest way to define a child resource is to nest it within the parent resource.</span></span> <span data-ttu-id="1c653-117">W poniższym przykładzie przedstawiono bazy danych SQL zagnieżdżone w obrębie w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1c653-117">The following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="1c653-118">Dla zasobu podrzędnego ustawiono typ `databases` , ale jego typ zasobu pełne jest `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="1c653-118">For the child resource, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="1c653-119">Nie podawaj `Microsoft.Sql/servers/` ponieważ zakłada się z nadrzędnego typu zasobu.</span><span class="sxs-lookup"><span data-stu-id="1c653-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from the parent resource type.</span></span> <span data-ttu-id="1c653-120">Ustawiono nazwę zasobu podrzędnego `exampledatabase` , ale imię i nazwisko zawiera nazwę nadrzędnej.</span><span class="sxs-lookup"><span data-stu-id="1c653-120">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="1c653-121">Nie podawaj `exampleserver` ponieważ zakłada się od zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="1c653-121">You do not provide `exampleserver` because it is assumed from the parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="1c653-122">Zasobu podrzędnego najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="1c653-122">Top-level child resource</span></span>
<span data-ttu-id="1c653-123">Można zdefiniować zasobu podrzędnego na najwyższym poziomie.</span><span class="sxs-lookup"><span data-stu-id="1c653-123">You can define the child resource at the top level.</span></span> <span data-ttu-id="1c653-124">Tej metody może użyć, jeśli zasobu nadrzędnego nie została wdrożona w tym samym szablonie, lub jeśli chcesz użyć `copy` utworzyć wiele podrzędnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="1c653-124">You might use this approach if the parent resource is not deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="1c653-125">Z tej metody należy udostępniają typ zasobu pełne i nazwy zasobu podrzędne zawierają nazwę zasobu nadrzędnego.</span><span class="sxs-lookup"><span data-stu-id="1c653-125">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="1c653-126">Baza danych jest zasobu podrzędnego z serwerem, nawet jeśli są one zdefiniowane w tym samym poziomie w szablonie.</span><span class="sxs-lookup"><span data-stu-id="1c653-126">The database is a child resource to the server even though they are defined on the same level in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c653-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c653-127">Next steps</span></span>
* <span data-ttu-id="1c653-128">Aby uzyskać zalecenia dotyczące tworzenia szablonów, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="1c653-128">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="1c653-129">Przykład tworzenia wielu podrzędnych zasobów, zobacz [wdrażanie wielu wystąpień zasobów w szablonach usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="1c653-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
