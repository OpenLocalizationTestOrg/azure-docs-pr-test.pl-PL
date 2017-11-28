---
title: "aaaAzure zarządzanych aplikacji SizeSelector elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Compute.SizeSelector interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="7d6c2-103">Element Microsoft.Compute.SizeSelector interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="7d6c2-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="7d6c2-104">Formant wyboru rozmiar dla co najmniej jedno wystąpienie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="7d6c2-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="7d6c2-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="7d6c2-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="7d6c2-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="7d6c2-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="7d6c2-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="7d6c2-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="7d6c2-109">Remarks</span></span>
- <span data-ttu-id="7d6c2-110">`recommendedSizes`powinien zawierać co najmniej jeden rozmiar.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="7d6c2-111">Witaj najpierw zaleca się, że rozmiar jest używana jako domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="7d6c2-112">Jeśli zalecany rozmiar nie jest dostępny w lokalizacji hello zaznaczone, rozmiar hello automatycznie zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="7d6c2-113">Zamiast tego hello dalej zalecany rozmiar jest używany.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="7d6c2-114">Dowolnej wielkości, nie jest określony w hello `constraints.allowedSizes` jest ukryta i rozmiarze nie jest określona w `constraints.excludedSizes` jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="7d6c2-115">`constraints.allowedSizes`i `constraints.excludedSizes` są opcjonalne, ale nie mogą być używane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="7d6c2-116">Witaj listę dostępnych rozmiarów można ustalić wywołując [listy dostępne rozmiary maszyny wirtualnej w ramach subskrypcji](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="7d6c2-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="7d6c2-117">`osPlatform`należy określić i mogą być **Windows** lub **Linux**.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="7d6c2-118">Został on użyty koszty sprzętu hello toodetermine hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="7d6c2-119">`imageReference`Pominięto obrazów firmy, ale podany dla obrazów innych firm.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="7d6c2-120">Został on użyty koszty oprogramowania hello toodetermine hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="7d6c2-121">`count`jest używana tooset hello odpowiednie mnożnik dla elementu hello.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="7d6c2-122">Obsługuje ona wartość statyczną, takie jak **2**, lub wartość dynamiczną z innego elementu, tak jak `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="7d6c2-123">Witaj, wartość domyślna to **1**.</span><span class="sxs-lookup"><span data-stu-id="7d6c2-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="7d6c2-124">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="7d6c2-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="7d6c2-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7d6c2-125">Next steps</span></span>
* <span data-ttu-id="7d6c2-126">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7d6c2-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="7d6c2-127">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7d6c2-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="7d6c2-128">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="7d6c2-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
