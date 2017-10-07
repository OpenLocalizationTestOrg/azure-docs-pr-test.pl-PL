---
title: "zasobu podrzędnego aaaDefine szablonu Azure | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak tooset hello typ zasobu i nazwę zasobu podrzędnego w szablonie usługi Azure Resource Manager"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a>Ustaw nazwę i typ zasobu podrzędnego w szablonie usługi Resource Manager
Podczas tworzenia szablonu, należy często tooinclude zasobu podrzędnego, który jest zasobem nadrzędnej tooa powiązane. Na przykład do szablonu może zawierać programu SQL server i bazy danych. Hello programu SQL server jest zasobem nadrzędnej hello i zasobu podrzędnego hello jest hello bazy danych. 

format Hello typu zasobu podrzędnego hello jest:`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`

format nazwy zasobu podrzędnego hello Hello jest:`{parent-resource-name}/{child-resource-name}`

Można jednak określić hello typem i nazwą w szablonie inaczej na podstawie tego, czy jest zagnieżdżony w obrębie zasobu nadrzędnego hello, lub na jego własnej na najwyższym poziomie hello. W tym temacie przedstawiono, jak zbliża się toohandle obu.

Podczas tworzenia zasobu tooa odwołanie w pełni kwalifikowana, toocombine kolejności hello segmenty z typu hello i nazwa nie jest po prostu złączeniem hello dwa.  Po hello przestrzeni nazw, użyj sekwencji *typ/nazwa* pary z najmniej specyficznych toomost określonych:

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

Na przykład:

`Microsoft.Compute/virtualMachines/myVM/extensions/myExt`jest poprawna `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` jest nieprawidłowy

## <a name="nested-child-resource"></a>Zasób zagnieżdżonych elementów podrzędnych
Witaj najprostszy sposób toodefine zasobu podrzędnego jest toonest jej w ciągu zasobu nadrzędnego hello. Witaj poniższy przykład przedstawia bazy danych SQL zagnieżdżone w obrębie w programie SQL Server.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

Dla zasobu podrzędnego hello, hello ustawiono zbyt`databases` , ale jego typ zasobu pełne jest `Microsoft.Sql/servers/databases`. Nie podawaj `Microsoft.Sql/servers/` ponieważ zakłada się od typu zasobu nadrzędnego hello. Nazwa zasobu podrzędnego Hello ustawiono zbyt`exampledatabase` , ale hello imię i nazwisko zawiera nazwę nadrzędnego hello. Nie podawaj `exampleserver` ponieważ zakłada się od zasobu nadrzędnego hello.

## <a name="top-level-child-resource"></a>Zasobu podrzędnego najwyższego poziomu
Można zdefiniować zasobu podrzędnego hello hello najwyższego poziomu. Można użyć tej metody, gdy hello zasobu nadrzędnego nie została wdrożona w hello tego samego szablonu lub, jeśli chcesz toouse `copy` toocreate wielu zasoby podrzędne. Z tej metody musi podać typ zasobu pełne hello i poddać Nazwa zasobu nadrzędnego hello nazwy zasobu podrzędnego hello.

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

Hello bazy danych jest podrzędny serwer toohello zasobów, nawet jeśli są zdefiniowane na poziomie samo w szablonie hello hello.

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać zalecenia dotyczące toocreate szablonów, zobacz [najlepszych rozwiązań dotyczących tworzenia szablonów usługi Azure Resource Manager](resource-manager-template-best-practices.md).
* Przykład tworzenia wielu podrzędnych zasobów, zobacz [wdrażanie wielu wystąpień zasobów w szablonach usługi Azure Resource Manager](resource-group-create-multiple.md).
