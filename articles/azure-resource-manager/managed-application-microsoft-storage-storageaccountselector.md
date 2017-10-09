---
title: "aaaAzure zarządzanych aplikacji StorageAccountSelector elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Storage.StorageAccountSelector interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a>Element Microsoft.Storage.StorageAccountSelector interfejsu użytkownika
Formant wyboru konta magazynu do nowego lub istniejącego. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a>Schemat
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>Uwagi
- Jeśli zostanie określona, `defaultValue.name` automatycznie sprawdzania poprawności unikatowość. Jeśli nazwa konta magazynu hello nie jest unikatowa, hello użytkownika musi określić inną nazwę lub wybierz istniejące konto magazynu.
- Witaj wartości domyślnej dla `defaultValue.type` jest **Premium_LRS**.
- Dowolnego typu nie jest określona w `constraints.allowedTypes` jest ukryta i dowolnego typu nie jest określona w `constraints.excludedTypes` jest wyświetlany.
`constraints.allowedTypes`i `constraints.excludedTypes` są opcjonalne, ale nie mogą być używane jednocześnie.
- Jeśli `options.hideExisting` jest **true**, hello użytkownika nie można wybrać istniejące konto magazynu. Witaj, wartość domyślna to **false**.


## <a name="sample-output"></a>Przykładowe dane wyjściowe
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
