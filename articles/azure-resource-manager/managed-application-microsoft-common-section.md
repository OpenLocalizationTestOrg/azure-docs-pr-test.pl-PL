---
title: "Azure zarządzanych aplikacji sekcji elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Common.Section interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 34c0f2f88e6af5a0f822ec116e7e2334e4e29e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="02bc5-103">Element Microsoft.Common.Section interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="02bc5-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="02bc5-104">Formant, który grupuje co najmniej jeden element w pozycji.</span><span class="sxs-lookup"><span data-stu-id="02bc5-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="02bc5-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="02bc5-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="02bc5-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="02bc5-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="02bc5-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="02bc5-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="02bc5-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="02bc5-109">Remarks</span></span>
- <span data-ttu-id="02bc5-110">`elements`musi zawierać co najmniej jeden element i może zawierać wszystkie typy elementów, z wyjątkiem `Microsoft.Common.Section`.</span><span class="sxs-lookup"><span data-stu-id="02bc5-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="02bc5-111">Ten element nie obsługuje `toolTip` właściwości.</span><span class="sxs-lookup"><span data-stu-id="02bc5-111">This element doesn't support the `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="02bc5-112">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="02bc5-112">Sample output</span></span>
<span data-ttu-id="02bc5-113">Aby uzyskać dostęp do danych wyjściowych wartości elementów w `elements`, użyj [basics()](managed-application-createuidefinition-functions.md#basics) lub [steps()](managed-application-createuidefinition-functions.md#steps) funkcje i kropkowego:</span><span class="sxs-lookup"><span data-stu-id="02bc5-113">To access the output values of elements in `elements`, use the [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="02bc5-114">Elementy typu `Microsoft.Common.Section` ma same wartości nie danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="02bc5-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02bc5-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02bc5-115">Next steps</span></span>
* <span data-ttu-id="02bc5-116">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02bc5-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="02bc5-117">Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02bc5-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="02bc5-118">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="02bc5-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
