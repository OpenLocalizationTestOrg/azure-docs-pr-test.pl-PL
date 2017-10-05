---
title: "Azure zarządzanych aplikacji pola tekstowego elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Common.TextBox interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="d9b95-103">Element Microsoft.Common.TextBox interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d9b95-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="d9b95-104">Formant, który może służyć do edycji niesformatowanego tekstu.</span><span class="sxs-lookup"><span data-stu-id="d9b95-104">A control that can be used to edit unformatted text.</span></span> <span data-ttu-id="d9b95-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="d9b95-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d9b95-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d9b95-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="d9b95-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="d9b95-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="d9b95-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d9b95-109">Remarks</span></span>
- <span data-ttu-id="d9b95-110">Jeśli `constraints.required` ustawiono **true**, a następnie w polu tekstowym musi zawierać wartość do zweryfikowania pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="d9b95-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="d9b95-111">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="d9b95-111">The default value is **false**.</span></span>
- <span data-ttu-id="d9b95-112">`constraints.regex`jest wzorzec wyrażenia regularnego JavaScript.</span><span class="sxs-lookup"><span data-stu-id="d9b95-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="d9b95-113">Jeśli jest określony, wartość pola tekstowego musi odpowiadać wzorzec można pomyślnie zweryfikować.</span><span class="sxs-lookup"><span data-stu-id="d9b95-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="d9b95-114">Wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="d9b95-114">The default value is **null**.</span></span>
- <span data-ttu-id="d9b95-115">`constraints.validationMessage`jest to ciąg wyświetlany, gdy wartość w polu tekstowym weryfikacji nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="d9b95-115">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="d9b95-116">Jeśli nie zostanie określony, komunikaty o błędach weryfikacji wbudowane pole tekstowe są używane.</span><span class="sxs-lookup"><span data-stu-id="d9b95-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="d9b95-117">Wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="d9b95-117">The default value is **null**.</span></span>
- <span data-ttu-id="d9b95-118">Można określić wartość dla `constraints.regex` podczas `constraints.required` ustawiono **false**.</span><span class="sxs-lookup"><span data-stu-id="d9b95-118">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="d9b95-119">W tym scenariuszu wartość nie jest wymagane dla pola tekstowego sprawdzić poprawność pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="d9b95-119">In this scenario, a value is not required for the text box to validate successfully.</span></span> <span data-ttu-id="d9b95-120">Jeśli jest określony, musi być zgodna ze wzorcem wyrażenia regularnego.</span><span class="sxs-lookup"><span data-stu-id="d9b95-120">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d9b95-121">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="d9b95-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="d9b95-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9b95-122">Next steps</span></span>
* <span data-ttu-id="d9b95-123">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9b95-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d9b95-124">Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d9b95-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d9b95-125">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d9b95-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
