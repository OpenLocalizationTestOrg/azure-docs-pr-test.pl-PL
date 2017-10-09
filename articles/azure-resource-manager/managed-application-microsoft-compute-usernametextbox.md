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
# <a name="microsoftcomputeusernametextbox-ui-element"></a>Element Microsoft.Compute.UserNameTextBox interfejsu użytkownika
Formant pola tekstowego z wbudowanych sprawdzania poprawności nazwy użytkownika systemu Windows i Linux. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a>Schemat
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

## <a name="remarks"></a>Uwagi
- Jeśli `constraints.required` ustawiono zbyt**true**, a następnie w polu tekstowym hello musi zawierać toovalidate wartość pomyślnie. Witaj, wartość domyślna to **true**.
- `osPlatform`należy określić i mogą być **Windows** lub **Linux**.
- `constraints.regex`jest wzorzec wyrażenia regularnego JavaScript. Jeśli zostanie określona, to wartość w polu tekstowym hello muszą odpowiadać toovalidate wzorzec hello pomyślnie. Wartość domyślna to **null**.
- `constraints.validationMessage`jest toodisplay ciąg nieudanej weryfikacji hello określony przez wartość w polu tekstowym hello `constraints.regex`. Jeśli nie określona, a następnie hello weryfikacji wbudowane pola tekstowego, komunikaty są używane. Witaj, wartość domyślna to **null**.
- Ten element ma wbudowane sprawdzanie poprawności opartego na powitania wartość określona dla `osPlatform`. wbudowane weryfikacji Hello może służyć wraz z niestandardowe wyrażenie regularne.
Jeśli określono wartość `constraints.regex` jest określony, a następnie zarówno hello wbudowanych i niestandardowych operacji sprawdzania poprawności są wyzwalane.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
```json
"tabrezm"
```

## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
