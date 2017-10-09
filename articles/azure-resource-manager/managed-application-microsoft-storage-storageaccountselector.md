---
title: "aaaAzure zarządzanych aplikacji StorageAccountSelector elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Storage.StorageAccountSelector interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="910cd-103">Element Microsoft.Storage.StorageAccountSelector interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="910cd-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="910cd-104">Formant wyboru konta magazynu do nowego lub istniejącego.</span><span class="sxs-lookup"><span data-stu-id="910cd-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="910cd-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="910cd-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="910cd-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="910cd-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="910cd-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="910cd-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="910cd-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="910cd-109">Remarks</span></span>
- <span data-ttu-id="910cd-110">Jeśli zostanie określona, `defaultValue.name` automatycznie sprawdzania poprawności unikatowość.</span><span class="sxs-lookup"><span data-stu-id="910cd-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="910cd-111">Jeśli nazwa konta magazynu hello nie jest unikatowa, hello użytkownika musi określić inną nazwę lub wybierz istniejące konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="910cd-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="910cd-112">Witaj wartości domyślnej dla `defaultValue.type` jest **Premium_LRS**.</span><span class="sxs-lookup"><span data-stu-id="910cd-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="910cd-113">Dowolnego typu nie jest określona w `constraints.allowedTypes` jest ukryta i dowolnego typu nie jest określona w `constraints.excludedTypes` jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="910cd-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="910cd-114">`constraints.allowedTypes`i `constraints.excludedTypes` są opcjonalne, ale nie mogą być używane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="910cd-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="910cd-115">Jeśli `options.hideExisting` jest **true**, hello użytkownika nie można wybrać istniejące konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="910cd-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="910cd-116">Witaj, wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="910cd-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="910cd-117">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="910cd-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="910cd-118">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="910cd-118">Next steps</span></span>
* <span data-ttu-id="910cd-119">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="910cd-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="910cd-120">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="910cd-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="910cd-121">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="910cd-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
