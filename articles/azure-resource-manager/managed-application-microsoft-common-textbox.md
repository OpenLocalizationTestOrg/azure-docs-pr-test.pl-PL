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
# <a name="microsoftcommontextbox-ui-element"></a>Element Microsoft.Common.TextBox interfejsu użytkownika
Formant, który może być używane tooedit niesformatowanego tekstu. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a>Uwagi
- Jeśli `constraints.required` ustawiono zbyt**true**, a następnie w polu tekstowym hello musi zawierać toovalidate wartość pomyślnie. Witaj, wartość domyślna to **false**.
- `constraints.regex`jest wzorzec wyrażenia regularnego JavaScript. Jeśli zostanie określona, to wartość w polu tekstowym hello muszą odpowiadać toovalidate wzorzec hello pomyślnie. Wartość domyślna to **null**.
- `constraints.validationMessage`jest toodisplay ciągiem, gdy wartość w polu tekstowym hello weryfikacji nie powiedzie się. Jeśli nie określona, a następnie hello weryfikacji wbudowane pola tekstowego, komunikaty są używane. Witaj, wartość domyślna to **null**.
- Jego możliwe toospecify wartość `constraints.regex` podczas `constraints.required` ustawiono zbyt**false**. W tym scenariuszu wartość nie jest wymagane dla toovalidate pole tekstowe hello pomyślnie. Jeśli jest określony, musi on być zgodny hello wzorzec wyrażenia regularnego.

## <a name="sample-output"></a>Przykładowe dane wyjściowe

```json
"foobar"
```

## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
