---
title: "aaaAzure zarządzanych aplikacji UserNameTextBox elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Compute.UserNameTextBox interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="392ea-103">Element Microsoft.Compute.UserNameTextBox interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="392ea-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="392ea-104">Formant pola tekstowego z wbudowanych sprawdzania poprawności nazwy użytkownika systemu Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="392ea-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="392ea-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="392ea-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="392ea-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="392ea-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="392ea-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="392ea-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="392ea-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="392ea-109">Remarks</span></span>
- <span data-ttu-id="392ea-110">Jeśli `constraints.required` ustawiono zbyt**true**, a następnie w polu tekstowym hello musi zawierać toovalidate wartość pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="392ea-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="392ea-111">Witaj, wartość domyślna to **true**.</span><span class="sxs-lookup"><span data-stu-id="392ea-111">hello default value is **true**.</span></span>
- <span data-ttu-id="392ea-112">`osPlatform`należy określić i mogą być **Windows** lub **Linux**.</span><span class="sxs-lookup"><span data-stu-id="392ea-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="392ea-113">`constraints.regex`jest wzorzec wyrażenia regularnego JavaScript.</span><span class="sxs-lookup"><span data-stu-id="392ea-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="392ea-114">Jeśli zostanie określona, to wartość w polu tekstowym hello muszą odpowiadać toovalidate wzorzec hello pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="392ea-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="392ea-115">Wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="392ea-115">The default value is **null**.</span></span>
- <span data-ttu-id="392ea-116">`constraints.validationMessage`jest toodisplay ciąg nieudanej weryfikacji hello określony przez wartość w polu tekstowym hello `constraints.regex`.</span><span class="sxs-lookup"><span data-stu-id="392ea-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="392ea-117">Jeśli nie określona, a następnie hello weryfikacji wbudowane pola tekstowego, komunikaty są używane.</span><span class="sxs-lookup"><span data-stu-id="392ea-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="392ea-118">Witaj, wartość domyślna to **null**.</span><span class="sxs-lookup"><span data-stu-id="392ea-118">hello default value is **null**.</span></span>
- <span data-ttu-id="392ea-119">Ten element ma wbudowane sprawdzanie poprawności opartego na powitania wartość określona dla `osPlatform`.</span><span class="sxs-lookup"><span data-stu-id="392ea-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="392ea-120">wbudowane weryfikacji Hello może służyć wraz z niestandardowe wyrażenie regularne.</span><span class="sxs-lookup"><span data-stu-id="392ea-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="392ea-121">Jeśli określono wartość `constraints.regex` jest określony, a następnie zarówno hello wbudowanych i niestandardowych operacji sprawdzania poprawności są wyzwalane.</span><span class="sxs-lookup"><span data-stu-id="392ea-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="392ea-122">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="392ea-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="392ea-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="392ea-123">Next steps</span></span>
* <span data-ttu-id="392ea-124">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="392ea-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="392ea-125">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="392ea-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="392ea-126">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="392ea-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
