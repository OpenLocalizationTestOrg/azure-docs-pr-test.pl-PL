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
# <a name="microsoftcommontextbox-ui-element"></a>Element Microsoft.Common.TextBox interfejsu użytkownika
Formant, który może służyć do edycji niesformatowanego tekstu. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a>Schemat
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

## <a name="remarks"></a>Uwagi
- Jeśli `constraints.required` ustawiono **true**, a następnie w polu tekstowym musi zawierać wartość do zweryfikowania pomyślnie. Wartość domyślna to **false**.
- `constraints.regex`jest wzorzec wyrażenia regularnego JavaScript. Jeśli jest określony, wartość pola tekstowego musi odpowiadać wzorzec można pomyślnie zweryfikować. Wartość domyślna to **null**.
- `constraints.validationMessage`jest to ciąg wyświetlany, gdy wartość w polu tekstowym weryfikacji nie powiedzie się. Jeśli nie zostanie określony, komunikaty o błędach weryfikacji wbudowane pole tekstowe są używane. Wartość domyślna to **null**.
- Można określić wartość dla `constraints.regex` podczas `constraints.required` ustawiono **false**. W tym scenariuszu wartość nie jest wymagane dla pola tekstowego sprawdzić poprawność pomyślnie. Jeśli jest określony, musi być zgodna ze wzorcem wyrażenia regularnego.

## <a name="sample-output"></a>Przykładowe dane wyjściowe

```json
"foobar"
```

## <a name="next-steps"></a>Następne kroki
* Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
