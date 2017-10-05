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
# <a name="microsoftcommonpasswordbox-ui-element"></a>Element Microsoft.Common.PasswordBox interfejsu użytkownika
Formant, który może służyć do udostępniania i Potwierdź hasło. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a>Schemat
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

## <a name="remarks"></a>Uwagi
- Ten element nie obsługuje `defaultValue` właściwości.
- Aby uzyskać szczegóły implementacji `constraints`, zobacz [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).
- Jeśli `options.hideConfirmation` ustawiono **true**, drugie pole tekstowe potwierdzania hasła jest ukryty. Wartość domyślna to **false**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
```json
"p4ssw0rd"
```

## <a name="next-steps"></a>Następne kroki
* Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
