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
# <a name="microsoftcommonoptionsgroup-ui-element"></a>Element Microsoft.Common.OptionsGroup interfejsu użytkownika
Formant wyboru z wierszem dostępnych opcji. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a>Schemat
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

## <a name="remarks"></a>Uwagi
- Etykieta Hello `constraints.allowedValues` jest hello wyświetlany tekst dla elementu i jego wartość wynosi wartość wyjściowa hello elementu hello zaznaczenie.
- Jeśli jest określony, wartość domyślna hello musi być obecne w etykiecie `constraints.allowedValues`. Jeśli nie zostanie określony, hello pierwszy element `constraints.allowedValues` jest domyślnie zaznaczona. Witaj, wartość domyślna to **null**.
- `constraints.allowedValues`musi zawierać co najmniej jeden element.
- Ten element nie obsługuje hello `constraints.required` właściwości; element musi być wybrany toovalidate pomyślnie.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
```json
"Bar"
```

## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
