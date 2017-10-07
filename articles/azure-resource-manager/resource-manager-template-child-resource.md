---
title: "zasobu podrzędnego aaaDefine szablonu Azure | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak tooset hello typ zasobu i nazwę zasobu podrzędnego w szablonie usługi Azure Resource Manager"
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="205be-103">Ustaw nazwę i typ zasobu podrzędnego w szablonie usługi Resource Manager</span><span class="sxs-lookup"><span data-stu-id="205be-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="205be-104">Podczas tworzenia szablonu, należy często tooinclude zasobu podrzędnego, który jest zasobem nadrzędnej tooa powiązane.</span><span class="sxs-lookup"><span data-stu-id="205be-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="205be-105">Na przykład do szablonu może zawierać programu SQL server i bazy danych.</span><span class="sxs-lookup"><span data-stu-id="205be-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="205be-106">Hello programu SQL server jest zasobem nadrzędnej hello i zasobu podrzędnego hello jest hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="205be-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="205be-107">format Hello typu zasobu podrzędnego hello jest:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="205be-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="205be-108">format nazwy zasobu podrzędnego hello Hello jest:`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="205be-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="205be-109">Można jednak określić hello typem i nazwą w szablonie inaczej na podstawie tego, czy jest zagnieżdżony w obrębie zasobu nadrzędnego hello, lub na jego własnej na najwyższym poziomie hello.</span><span class="sxs-lookup"><span data-stu-id="205be-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="205be-110">W tym temacie przedstawiono, jak zbliża się toohandle obu.</span><span class="sxs-lookup"><span data-stu-id="205be-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="205be-111">Podczas tworzenia zasobu tooa odwołanie w pełni kwalifikowana, toocombine kolejności hello segmenty z typu hello i nazwa nie jest po prostu złączeniem hello dwa.</span><span class="sxs-lookup"><span data-stu-id="205be-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="205be-112">Po hello przestrzeni nazw, użyj sekwencji *typ/nazwa* pary z najmniej specyficznych toomost określonych:</span><span class="sxs-lookup"><span data-stu-id="205be-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="205be-113">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="205be-113">For example:</span></span>

<span data-ttu-id="205be-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`jest poprawna `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` jest nieprawidłowy</span><span class="sxs-lookup"><span data-stu-id="205be-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="205be-115">Zasób zagnieżdżonych elementów podrzędnych</span><span class="sxs-lookup"><span data-stu-id="205be-115">Nested child resource</span></span>
<span data-ttu-id="205be-116">Witaj najprostszy sposób toodefine zasobu podrzędnego jest toonest jej w ciągu zasobu nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="205be-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="205be-117">Witaj poniższy przykład przedstawia bazy danych SQL zagnieżdżone w obrębie w programie SQL Server.</span><span class="sxs-lookup"><span data-stu-id="205be-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="205be-118">Dla zasobu podrzędnego hello, hello ustawiono zbyt`databases` , ale jego typ zasobu pełne jest `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="205be-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="205be-119">Nie podawaj `Microsoft.Sql/servers/` ponieważ zakłada się od typu zasobu nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="205be-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="205be-120">Nazwa zasobu podrzędnego Hello ustawiono zbyt`exampledatabase` , ale hello imię i nazwisko zawiera nazwę nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="205be-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="205be-121">Nie podawaj `exampleserver` ponieważ zakłada się od zasobu nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="205be-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="205be-122">Zasobu podrzędnego najwyższego poziomu</span><span class="sxs-lookup"><span data-stu-id="205be-122">Top-level child resource</span></span>
<span data-ttu-id="205be-123">Można zdefiniować zasobu podrzędnego hello hello najwyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="205be-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="205be-124">Można użyć tej metody, gdy hello zasobu nadrzędnego nie została wdrożona w hello tego samego szablonu lub, jeśli chcesz toouse `copy` toocreate wielu zasoby podrzędne.</span><span class="sxs-lookup"><span data-stu-id="205be-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="205be-125">Z tej metody musi podać typ zasobu pełne hello i poddać Nazwa zasobu nadrzędnego hello nazwy zasobu podrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="205be-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="205be-126">Hello bazy danych jest podrzędny serwer toohello zasobów, nawet jeśli są zdefiniowane na poziomie samo w szablonie hello hello.</span><span class="sxs-lookup"><span data-stu-id="205be-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="205be-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="205be-127">Next steps</span></span>
* <span data-ttu-id="205be-128">Aby uzyskać zalecenia dotyczące toocreate szablonów, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="205be-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="205be-129">Przykład tworzenia wielu podrzędnych zasobów, zobacz [wdrażanie wielu wystąpień zasobów w szablonach usługi Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="205be-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
