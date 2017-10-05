---
title: "Azure zarządzanych aplikacji OptionsGroup elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Common.OptionsGroup interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 6e147ed28c8248f7f17cb36fd7ae13468141dced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="aad65-103">Element Microsoft.Common.OptionsGroup interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="aad65-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="aad65-104">Formant wyboru z wierszem dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="aad65-104">A selection control with a row of available options.</span></span> <span data-ttu-id="aad65-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="aad65-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="aad65-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="aad65-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="aad65-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="aad65-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="aad65-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="aad65-109">Remarks</span></span>
- <span data-ttu-id="aad65-110">Etykieta dla `constraints.allowedValues` jest wyświetlany tekst dla elementu i jego wartość jest wartością danych wyjściowych w przypadku wybrania elementu.</span><span class="sxs-lookup"><span data-stu-id="aad65-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="aad65-111">Jeśli jest określony, wartość domyślna musi być obecne w etykiecie `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="aad65-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="aad65-112">Jeśli nie zostanie określony, pierwszy element `constraints.allowedValues` jest domyślnie zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="aad65-112">If not specified, the first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="aad65-113">Wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="aad65-113">The default value is **null**.</span></span>
- <span data-ttu-id="aad65-114">`constraints.allowedValues`musi zawierać co najmniej jeden element.</span><span class="sxs-lookup"><span data-stu-id="aad65-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="aad65-115">Ten element nie obsługuje `constraints.required` właściwości; można pomyślnie zweryfikować należy wybrać element.</span><span class="sxs-lookup"><span data-stu-id="aad65-115">This element doesn't support the `constraints.required` property; an item must be selected to validate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="aad65-116">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="aad65-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="aad65-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="aad65-117">Next steps</span></span>
* <span data-ttu-id="aad65-118">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aad65-118">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="aad65-119">Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aad65-119">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="aad65-120">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="aad65-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
