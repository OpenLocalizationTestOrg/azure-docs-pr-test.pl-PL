---
title: "Azure zarządzanych aplikacji StorageAccountSelector elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Storage.StorageAccountSelector interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="c6bac-103">Element Microsoft.Storage.StorageAccountSelector interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="c6bac-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="c6bac-104">Formant wyboru konta magazynu do nowego lub istniejącego.</span><span class="sxs-lookup"><span data-stu-id="c6bac-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="c6bac-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="c6bac-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="c6bac-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="c6bac-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="c6bac-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="c6bac-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="c6bac-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c6bac-109">Remarks</span></span>
- <span data-ttu-id="c6bac-110">Jeśli zostanie określona, `defaultValue.name` automatycznie sprawdzania poprawności unikatowość.</span><span class="sxs-lookup"><span data-stu-id="c6bac-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="c6bac-111">Jeśli nazwa konta magazynu nie jest unikatowa, użytkownik musi określić inną nazwę lub wybierz istniejące konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="c6bac-111">If the storage account name is not unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="c6bac-112">Wartość domyślna dla `defaultValue.type` jest **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="c6bac-112">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="c6bac-113">Dowolnego typu nie jest określona w `constraints.allowedTypes` jest ukryta i dowolnego typu nie jest określona w `constraints.excludedTypes` jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="c6bac-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="c6bac-114">`constraints.allowedTypes`i `constraints.excludedTypes` są opcjonalne, ale nie mogą być używane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="c6bac-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="c6bac-115">Jeśli `options.hideExisting` jest **true**, użytkownik nie może wybrać istniejące konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="c6bac-115">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="c6bac-116">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="c6bac-116">The default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="c6bac-117">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="c6bac-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="c6bac-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6bac-118">Next steps</span></span>
* <span data-ttu-id="c6bac-119">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6bac-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="c6bac-120">Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6bac-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="c6bac-121">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="c6bac-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
