---
title: "aaaAzure zarządzanych aplikacji PasswordBox elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Common.PasswordBox interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="f6ab3-103">Element Microsoft.Common.PasswordBox interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="f6ab3-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="f6ab3-104">Formant, który może być używane tooprovide i Potwierdź hasło.</span><span class="sxs-lookup"><span data-stu-id="f6ab3-104">A control that can be used tooprovide and confirm a password.</span></span> <span data-ttu-id="f6ab3-105">Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f6ab3-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="f6ab3-106">Przykład interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="f6ab3-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="f6ab3-108">Schemat</span><span class="sxs-lookup"><span data-stu-id="f6ab3-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="f6ab3-109">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f6ab3-109">Remarks</span></span>
- <span data-ttu-id="f6ab3-110">Ten element nie obsługuje hello `defaultValue` właściwości.</span><span class="sxs-lookup"><span data-stu-id="f6ab3-110">This element doesn't support hello `defaultValue` property.</span></span>
- <span data-ttu-id="f6ab3-111">Aby uzyskać szczegóły implementacji `constraints`, zobacz [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span><span class="sxs-lookup"><span data-stu-id="f6ab3-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="f6ab3-112">Jeśli `options.hideConfirmation` ustawiono zbyt**true**, hello drugie pole tekstowe potwierdzania hasła użytkownika hello jest ukryty.</span><span class="sxs-lookup"><span data-stu-id="f6ab3-112">If `options.hideConfirmation` is set too**true**, hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="f6ab3-113">Witaj, wartość domyślna to **false**.</span><span class="sxs-lookup"><span data-stu-id="f6ab3-113">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="f6ab3-114">Przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="f6ab3-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="f6ab3-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6ab3-115">Next steps</span></span>
* <span data-ttu-id="f6ab3-116">Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6ab3-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f6ab3-117">Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6ab3-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="f6ab3-118">Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="f6ab3-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
