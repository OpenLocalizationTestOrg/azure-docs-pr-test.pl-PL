---
title: "Azure zarządzanych aplikacji SizeSelector elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Compute.SizeSelector interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="688cd-103">Element Microsoft.Compute.SizeSelector interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="688cd-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="688cd-104">Formant wyboru rozmiar dla co najmniej jedno wystąpienie maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="688cd-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="688cd-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="688cd-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="688cd-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="688cd-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="688cd-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="688cd-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="688cd-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="688cd-109">Remarks</span></span>
- <span data-ttu-id="688cd-110">`recommendedSizes`powinien zawierać co najmniej jeden rozmiar.</span><span class="sxs-lookup"><span data-stu-id="688cd-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="688cd-111">Zalecany rozmiar pierwszy jest używany jako domyślny.</span><span class="sxs-lookup"><span data-stu-id="688cd-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="688cd-112">Jeśli zalecany rozmiar nie jest dostępny w wybranej lokalizacji, rozmiar automatycznie zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="688cd-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="688cd-113">Zamiast tego dalej zalecany rozmiar jest używany.</span><span class="sxs-lookup"><span data-stu-id="688cd-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="688cd-114">Dowolnej wielkości, nie jest określona w `constraints.allowedSizes` jest ukryta i rozmiarze nie jest określona w `constraints.excludedSizes` jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="688cd-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="688cd-115">`constraints.allowedSizes`i `constraints.excludedSizes` są opcjonalne, ale nie mogą być używane jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="688cd-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="688cd-116">Listę dostępnych rozmiarów można ustalić wywołując [listy dostępne rozmiary maszyny wirtualnej w ramach subskrypcji](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span><span class="sxs-lookup"><span data-stu-id="688cd-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="688cd-117">`osPlatform`należy określić i mogą być **Windows** lub **Linux**.</span><span class="sxs-lookup"><span data-stu-id="688cd-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="688cd-118">Służy do określenia koszty sprzętu, maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="688cd-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="688cd-119">`imageReference`Pominięto obrazów firmy, ale podany dla obrazów innych firm.</span><span class="sxs-lookup"><span data-stu-id="688cd-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="688cd-120">Służy do określania oprogramowania kosztów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="688cd-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="688cd-121">`count`Służy do ustawiania odpowiednich mnożnik dla elementu.</span><span class="sxs-lookup"><span data-stu-id="688cd-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="688cd-122">Obsługuje ona wartość statyczną, takie jak **2**, lub wartość dynamiczną z innego elementu, tak jak `[steps('step1').vmCount]`.</span><span class="sxs-lookup"><span data-stu-id="688cd-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="688cd-123">Wartość domyślna to **1**.</span><span class="sxs-lookup"><span data-stu-id="688cd-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="688cd-124">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="688cd-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="688cd-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="688cd-125">Next steps</span></span>
* <span data-ttu-id="688cd-126">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="688cd-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="688cd-127">Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="688cd-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="688cd-128">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="688cd-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
