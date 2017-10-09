---
title: "aaaAzure zarządzanej aplikacji tworzenie funkcji interfejsu użytkownika definicji | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano hello funkcji toouse podczas konstruowania definicji interfejsu użytkownika dla aplikacji zarządzanych platformy Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: a34c6202372168cda769c471b1c9fdd539dd0f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="createuidefinition-elements"></a>Elementy CreateUiDefinition
W tym artykule opisano hello schematu i właściwości dla wszystkich elementów obsługiwanych CreateUiDefinition. Użyj tych elementów przy [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md). Schemat Hello większość elementów ma następującą składnię:

```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Keep calm and visit hello [Azure Portal](portal.azure.com).",
  "constraints": {},
  "options": {},
  "visible": true
}
```
| Właściwość | Wymagane | Opis |
| -------- | -------- | ----------- |
| name | Tak | Wewnętrzny identyfikator tooreference konkretne wystąpienie elementu. Witaj najbardziej typowe użycie nazwy elementu hello znajduje się w `outputs`, gdzie wartości danych wyjściowych hello hello określone elementy są mapowane toohello parametry szablonu hello. Umożliwia także jej wartości wyjściowej hello toobind toohello elementu `defaultValue` innego elementu. |
| type | Tak | Witaj toorender formantu interfejsu użytkownika dla elementu hello. Aby uzyskać listę obsługiwanych typów, zobacz [elementy](#elements). |
| Etykiety | Tak | Hello jest wyświetlany tekst elementu hello. Niektóre typy elementów zawiera wiele etykiet, więc hello wartość może być obiektu zawierającego wiele ciągów. |
| Wartość domyślna | Nie | Wartość domyślna Hello hello elementu. Niektóre typy elementu obsługuje wartości domyślne złożonych, więc hello wartość może być obiektem. |
| Etykietka narzędzia | Nie | Witaj toodisplay tekstu w etykietce narzędzia hello hello elementu. Podobnie za`label`, niektóre elementy obsługi wielu ciągów Porada narzędzia. Można ją osadzić łącza wbudowanego przy użyciu składni języka Markdown.
| Ograniczenia | Nie | Co najmniej jednej właściwości, które są używane toocustomize hello weryfikacji zachowanie elementu hello. właściwości Hello obsługiwane dla ograniczenia zależy od typu elementu. Niektóre typy elementu nie obsługuje dostosowywania hello sprawdzania poprawności działania i w związku z tym mieć żadnej właściwości ograniczenia. |
| Opcje | Nie | Dodatkowe właściwości, które dostosowują zachowanie hello hello elementu. Podobnie za`constraints`, właściwości hello obsługiwane zależy od typu elementu. |
| Widoczne | Nie | Wskazuje, czy hello element jest wyświetlany. Jeśli `true`, hello element i elementy podrzędne stosowane są wyświetlane. Witaj, wartość domyślna to `true`. Użyj [funkcje logiczne](managed-application-createuidefinition-functions.md#logical-functions) toodynamically kontrolować wartość tej właściwości.

## <a name="elements"></a>Elementy

Witaj dokumentacji dla każdego elementu zawiera przykładowe interfejsu użytkownika, schematem, uwagi na powitania zachowanie elementu hello (zazwyczaj dotyczących sprawdzania poprawności i dostosowywania obsługiwanych) i przykładowe dane wyjściowe.

- [Microsoft.Common.DropDown](managed-application-microsoft-common-dropdown.md)
- [Microsoft.Common.FileUpload](managed-application-microsoft-common-fileupload.md)
- [Microsoft.Common.OptionsGroup](managed-application-microsoft-common-optionsgroup.md)
- [Microsoft.Common.PasswordBox](managed-application-microsoft-common-passwordbox.md)
- [Microsoft.Common.Section](managed-application-microsoft-common-section.md)
- [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)
- [Microsoft.Compute.CredentialsCombo](managed-application-microsoft-compute-credentialscombo.md)
- [Microsoft.Compute.SizeSelector](managed-application-microsoft-compute-sizeselector.md)
- [Microsoft.Compute.UserNameTextBox](managed-application-microsoft-compute-usernametextbox.md)
- [Microsoft.Network.PublicIpAddressCombo](managed-application-microsoft-network-publicipaddresscombo.md)
- [Microsoft.Network.VirtualNetworkCombo](managed-application-microsoft-network-virtualnetworkcombo.md)
- [Microsoft.Storage.MultiStorageAccountCombo](managed-application-microsoft-storage-multistorageaccountcombo.md)
- [Microsoft.Storage.StorageAccountSelector](managed-application-microsoft-storage-storageaccountselector.md)

## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
