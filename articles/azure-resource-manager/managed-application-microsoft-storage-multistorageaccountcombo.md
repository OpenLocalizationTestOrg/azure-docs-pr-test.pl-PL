---
title: "Azure zarządzanych aplikacji MultiStorageAccountCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Storage.MultiStorageAccountCombo interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 27843b116d949899e4eae65f342324f77ebca70b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a>Element Microsoft.Storage.MultiStorageAccountCombo interfejsu użytkownika
Grupa służy do tworzenia wielu kont magazynu, których nazwy rozpoczynają się typowe prefiksu. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a>Schemat
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a>Uwagi
- Wartość `defaultValue.prefix` jest połączony z co najmniej jeden liczb całkowitych na generowanie sekwencji nazw kont magazynu. Na przykład jeśli `defaultValue.prefix` jest **foobar** i `count` jest **2**, następnie nazwy konta magazynu **foobar1** i **foobar2** są generowane. Unikatowość nazw kont magazynu generowane są weryfikowane automatycznie.
- Nazwy konta magazynu są generowane lexicographically na podstawie `count`. Na przykład jeśli `count` to 10, a następnie nazwy konta magazynu kończyć 2-cyfrowe liczby całkowite (01, 02, 03, itp.).
- Wartość domyślna dla `defaultValue.prefix` jest **null**oraz `defaultValue.type` jest **Premium_LRS**.
- Dowolnego typu nie jest określona w `constraints.allowedTypes` jest ukryta i dowolnego typu nie jest określona w `constraints.excludedTypes` jest wyświetlany.
`constraints.allowedTypes`i `constraints.excludedTypes` są opcjonalne, ale nie mogą być używane jednocześnie.
- Oprócz generowania nazw kont magazynu, `count` służy do ustawiania odpowiednich mnożnik dla elementu. Obsługuje ona wartość statyczną, takie jak **2**, lub wartość dynamiczną z innego elementu, tak jak `[steps('step1').storageAccountCount]`. Wartość domyślna to **1**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a>Następne kroki
* Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
