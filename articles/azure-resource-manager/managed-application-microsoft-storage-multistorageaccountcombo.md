---
title: "Azure zarządzanych aplikacji MultiStorageAccountCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Storage.MultiStorageAccountCombo interfejsu użytkownika dla aplikacji Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="fc0a8-103">Element Microsoft.Storage.MultiStorageAccountCombo interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fc0a8-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="fc0a8-104">Grupa służy do tworzenia wielu kont magazynu, których nazwy rozpoczynają się typowe prefiksu.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="fc0a8-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fc0a8-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="fc0a8-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fc0a8-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="fc0a8-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="fc0a8-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="fc0a8-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fc0a8-109">Remarks</span></span>
- <span data-ttu-id="fc0a8-110">Wartość `defaultValue.prefix` jest połączony z co najmniej jeden liczb całkowitych na generowanie sekwencji nazw kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-110">The value for `defaultValue.prefix` is concatenated with one or more integers to generate the sequence of storage account names.</span></span> <span data-ttu-id="fc0a8-111">Na przykład jeśli `defaultValue.prefix` jest **foobar** i `count` jest **2**, następnie nazwy konta magazynu **foobar1** i **foobar2** są generowane.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="fc0a8-112">Unikatowość nazw kont magazynu generowane są weryfikowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="fc0a8-113">Nazwy konta magazynu są generowane lexicographically na podstawie `count`.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-113">The storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="fc0a8-114">Na przykład jeśli `count` to 10, a następnie nazwy konta magazynu kończyć 2-cyfrowe liczby całkowite (01, 02, 03, itp.).</span><span class="sxs-lookup"><span data-stu-id="fc0a8-114">For example, if `count` is 10, then the storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="fc0a8-115">Wartość domyślna dla `defaultValue.prefix` jest **null**oraz `defaultValue.type` jest **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-115">The default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="fc0a8-116">Dowolnego typu nie jest określona w `constraints.allowedTypes` jest ukryta i dowolnego typu nie jest określona w `constraints.excludedTypes` jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="fc0a8-117">`constraints.allowedTypes`i `constraints.excludedTypes` są opcjonalne, ale nie mogą być używane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="fc0a8-118">Oprócz generowania nazw kont magazynu, `count` służy do ustawiania odpowiednich mnożnik dla elementu.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-118">In addition to generating storage account names, `count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="fc0a8-119">Obsługuje ona wartość statyczną, takie jak **2**, lub wartość dynamiczną z innego elementu, tak jak `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="fc0a8-120">Wartość domyślna to **1**.</span><span class="sxs-lookup"><span data-stu-id="fc0a8-120">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="fc0a8-121">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="fc0a8-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="fc0a8-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fc0a8-122">Next steps</span></span>
* <span data-ttu-id="fc0a8-123">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc0a8-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="fc0a8-124">Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc0a8-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="fc0a8-125">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="fc0a8-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
