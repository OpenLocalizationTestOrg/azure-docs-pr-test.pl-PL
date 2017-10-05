---
title: "Azure zarządzanych aplikacji PasswordBox elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Common.PasswordBox interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="5f233-103">Element Microsoft.Common.PasswordBox interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="5f233-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="5f233-104">Formant, który może służyć do udostępniania i Potwierdź hasło.</span><span class="sxs-lookup"><span data-stu-id="5f233-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="5f233-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5f233-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5f233-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="5f233-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="5f233-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="5f233-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5f233-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5f233-109">Remarks</span></span>
- <span data-ttu-id="5f233-110">Ten element nie obsługuje `defaultValue` właściwości.</span><span class="sxs-lookup"><span data-stu-id="5f233-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="5f233-111">Aby uzyskać szczegóły implementacji `constraints`, zobacz [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="5f233-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="5f233-112">Jeśli `options.hideConfirmation` ustawiono **true**, drugie pole tekstowe potwierdzania hasła jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="5f233-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="5f233-113">Wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="5f233-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5f233-114">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="5f233-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="5f233-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f233-115">Next steps</span></span>
* <span data-ttu-id="5f233-116">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f233-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5f233-117">Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f233-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5f233-118">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="5f233-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
