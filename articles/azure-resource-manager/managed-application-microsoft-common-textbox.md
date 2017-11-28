---
title: "aaaAzure zarządzanych aplikacji pola tekstowego elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Common.TextBox interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="fb77e-103">Element Microsoft.Common.TextBox interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fb77e-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="fb77e-104">Formant, który może być używane tooedit niesformatowanego tekstu.</span><span class="sxs-lookup"><span data-stu-id="fb77e-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="fb77e-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="fb77e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="fb77e-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="fb77e-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="fb77e-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="fb77e-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="fb77e-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="fb77e-109">Remarks</span></span>
- <span data-ttu-id="fb77e-110">Jeśli `constraints.required` ustawiono zbyt**true**, a następnie w polu tekstowym hello musi zawierać toovalidate wartość pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="fb77e-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="fb77e-111">Witaj, wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="fb77e-111">hello default value is **false**.</span></span>
- <span data-ttu-id="fb77e-112">`constraints.regex`jest wzorzec wyrażenia regularnego JavaScript.</span><span class="sxs-lookup"><span data-stu-id="fb77e-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="fb77e-113">Jeśli zostanie określona, to wartość w polu tekstowym hello muszą odpowiadać toovalidate wzorzec hello pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="fb77e-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="fb77e-114">Wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="fb77e-114">The default value is **null**.</span></span>
- <span data-ttu-id="fb77e-115">`constraints.validationMessage`jest toodisplay ciągiem, gdy wartość w polu tekstowym hello weryfikacji nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="fb77e-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="fb77e-116">Jeśli nie określona, a następnie hello weryfikacji wbudowane pola tekstowego, komunikaty są używane.</span><span class="sxs-lookup"><span data-stu-id="fb77e-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="fb77e-117">Witaj, wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="fb77e-117">hello default value is **null**.</span></span>
- <span data-ttu-id="fb77e-118">Jego możliwe toospecify wartość `constraints.regex` podczas `constraints.required` ustawiono zbyt**false**.</span><span class="sxs-lookup"><span data-stu-id="fb77e-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="fb77e-119">W tym scenariuszu wartość nie jest wymagane dla toovalidate pole tekstowe hello pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="fb77e-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="fb77e-120">Jeśli jest określony, musi on być zgodny hello wzorzec wyrażenia regularnego.</span><span class="sxs-lookup"><span data-stu-id="fb77e-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="fb77e-121">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="fb77e-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="fb77e-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fb77e-122">Next steps</span></span>
* <span data-ttu-id="fb77e-123">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb77e-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="fb77e-124">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb77e-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="fb77e-125">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="fb77e-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
