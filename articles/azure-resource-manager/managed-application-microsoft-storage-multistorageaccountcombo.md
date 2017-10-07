---
title: "aaaAzure zarządzanych aplikacji MultiStorageAccountCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Storage.MultiStorageAccountCombo interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="2279a-103">Element Microsoft.Storage.MultiStorageAccountCombo interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="2279a-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="2279a-104">Grupa służy do tworzenia wielu kont magazynu, których nazwy rozpoczynają się typowe prefiksu.</span><span class="sxs-lookup"><span data-stu-id="2279a-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="2279a-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="2279a-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="2279a-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="2279a-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="2279a-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="2279a-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="2279a-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2279a-109">Remarks</span></span>
- <span data-ttu-id="2279a-110">Witaj wartość `defaultValue.prefix` jest połączony z co najmniej jeden liczb całkowitych toogenerate hello sekwencji nazw kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="2279a-110">hello value for `defaultValue.prefix` is concatenated with one or more integers toogenerate hello sequence of storage account names.</span></span> <span data-ttu-id="2279a-111">Na przykład jeśli `defaultValue.prefix` jest **foobar** i `count` jest **2**, następnie nazwy konta magazynu **foobar1** i **foobar2** są generowane.</span><span class="sxs-lookup"><span data-stu-id="2279a-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="2279a-112">Unikatowość nazw kont magazynu generowane są weryfikowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2279a-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="2279a-113">nazwy kont magazynu Hello są generowane lexicographically na podstawie `count`.</span><span class="sxs-lookup"><span data-stu-id="2279a-113">hello storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="2279a-114">Na przykład jeśli `count` to 10, a następnie nazwy konta magazynu hello kończyć 2-cyfrowe liczby całkowite (01, 02, 03, itp.).</span><span class="sxs-lookup"><span data-stu-id="2279a-114">For example, if `count` is 10, then hello storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="2279a-115">Witaj wartości domyślnej dla `defaultValue.prefix` jest **null**oraz `defaultValue.type` jest **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="2279a-115">hello default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="2279a-116">Dowolnego typu nie jest określona w `constraints.allowedTypes` jest ukryta i dowolnego typu nie jest określona w `constraints.excludedTypes` jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="2279a-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="2279a-117">`constraints.allowedTypes`i `constraints.excludedTypes` są opcjonalne, ale nie mogą być używane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="2279a-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="2279a-118">W polu nazwy konta magazynu toogenerating dodanie `count` jest używane tooset odpowiednie mnożnik hello elementu.</span><span class="sxs-lookup"><span data-stu-id="2279a-118">In addition toogenerating storage account names, `count` is used tooset the appropriate multiplier for hello element.</span></span> <span data-ttu-id="2279a-119">Obsługuje ona wartość statyczną, takie jak **2**, lub wartość dynamiczną z innego elementu, tak jak `[steps('step1').storageAccountCount]`.</span><span class="sxs-lookup"><span data-stu-id="2279a-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="2279a-120">Witaj, wartość domyślna to **1**.</span><span class="sxs-lookup"><span data-stu-id="2279a-120">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="2279a-121">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="2279a-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="2279a-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2279a-122">Next steps</span></span>
* <span data-ttu-id="2279a-123">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2279a-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="2279a-124">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2279a-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="2279a-125">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="2279a-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
