---
title: "aaaAzure zarządzanych aplikacji listy rozwijanej elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Common.DropDown interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a>Element Microsoft.Common.DropDown interfejsu użytkownika
Formant wyboru z listy rozwijanej. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a>Schemat
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
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
- Jeśli jest określony, wartość domyślna hello musi być obecne w etykiecie `constraints.allowedValues`. Jeśli nie zostanie określony, hello pierwszy element `constraints.allowedValues` jest zaznaczone. Witaj, wartość domyślna to **null**.
- `constraints.allowedValues`musi zawierać co najmniej jeden element.
- Ten element nie obsługuje hello `constraints.required` właściwości. tooemulate to zachowanie, Dodaj element z etykiety i wartości `""` (pusty ciąg) zbyt`constraints.allowedValues`.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
```json
"Bar"
```

## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
