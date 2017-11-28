---
title: "aaaAzure zarządzanych aplikacji OptionsGroup elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Common.OptionsGroup interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="951eb-103">Element Microsoft.Common.OptionsGroup interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="951eb-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="951eb-104">Formant wyboru z wierszem dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="951eb-104">A selection control with a row of available options.</span></span> <span data-ttu-id="951eb-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="951eb-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="951eb-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="951eb-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="951eb-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="951eb-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="951eb-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="951eb-109">Remarks</span></span>
- <span data-ttu-id="951eb-110">Etykieta Hello `constraints.allowedValues` jest hello wyświetlany tekst dla elementu i jego wartość wynosi wartość wyjściowa hello elementu hello zaznaczenie.</span><span class="sxs-lookup"><span data-stu-id="951eb-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="951eb-111">Jeśli jest określony, wartość domyślna hello musi być obecne w etykiecie `constraints.allowedValues`.</span><span class="sxs-lookup"><span data-stu-id="951eb-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="951eb-112">Jeśli nie zostanie określony, hello pierwszy element `constraints.allowedValues` jest domyślnie zaznaczona.</span><span class="sxs-lookup"><span data-stu-id="951eb-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="951eb-113">Witaj, wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="951eb-113">hello default value is **null**.</span></span>
- <span data-ttu-id="951eb-114">`constraints.allowedValues`musi zawierać co najmniej jeden element.</span><span class="sxs-lookup"><span data-stu-id="951eb-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="951eb-115">Ten element nie obsługuje hello `constraints.required` właściwości; element musi być wybrany toovalidate pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="951eb-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="951eb-116">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="951eb-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="951eb-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="951eb-117">Next steps</span></span>
* <span data-ttu-id="951eb-118">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="951eb-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="951eb-119">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="951eb-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="951eb-120">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="951eb-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
