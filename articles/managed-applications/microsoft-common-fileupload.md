---
title: "Azure zarządzanych aplikacji przekazywaniem plików elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Common.FileUpload interfejsu użytkownika dla aplikacji Azure"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: 095880322ba801895a22efcf3476fa37d9e2ac3c
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Element Microsoft.Common.FileUpload interfejsu użytkownika
Formant, który umożliwia użytkownikowi określenie co najmniej jeden plik do przekazania. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](publish-service-catalog-app.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>Schemat
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>Uwagi
- `constraints.accept`Określa typy plików, które są wyświetlane w oknie dialogowym pliku przeglądarki. Zobacz [specyfikacji HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) dla dozwolone wartości. Wartość domyślna to **null**.
- Jeśli `options.multiple` ustawiono **true**, użytkownik może wybrać więcej niż jednego pliku w oknie dialogowym pliku przeglądarki. Wartość domyślna to **false**.
- Ten element obsługuje przekazywanie plików w dwóch trybach, w oparciu o wartości `options.uploadMode`. Jeśli **pliku** jest określony, dane wyjściowe zawierają zawartość pliku jako obiekt blob. Jeśli **adres url** jest określona, plik jest przekazywany do tymczasowej lokalizacji, a dane wyjściowe zawierają adresu URL obiektu blob. Tymczasowe obiekty BLOB zostaną usunięte po 24 godzinach. Wartość domyślna to **pliku**.
- Wartość `options.openMode` określa sposób odczytać pliku. Jeśli plik powinien być zwykłego tekstu, określ **tekst**; w przeciwnym razie, określ **binarne**. Wartość domyślna to **tekstu**.
- Jeśli `options.uploadMode` ma ustawioną wartość **pliku** i `options.openMode` ustawiono **binarne**, dane wyjściowe są algorytmem Base64.
- `options.encoding`Określa kodowanie używane podczas odczytu pliku. Wartość domyślna to **UTF-8**i jest używany tylko wtedy, gdy `options.openMode` ustawiono **tekstu**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
Jeśli options.uploadMode jest plikiem options.multiple ma wartość false, następnie dane wyjściowe zawierają zawartość pliku jako ciągu JSON:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Jeśli options.multiple ma wartość true and'options.uploadMode pliku, wówczas dane wyjściowe zawierają zawartość plików w postaci tablicy JSON:

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

Jeśli adres url jest options.uploadMode options.multiple ma wartość false, następnie dane wyjściowe zawiera adres URL jako ciągu JSON:

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

Jeśli adres url jest options.uploadMode options.multiple ma wartość true, następnie dane wyjściowe zawierają listę adresów URL jako tablica JSON:
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

Podczas testowania CreateUiDefinition, niektóre przeglądarki (np. Google Chrome) obciąć adresy URL wygenerowanym przez dany element Microsoft.Common.FileUpload w konsoli przeglądarki. Konieczne może być kliknij prawym przyciskiem myszy poszczególnych łączy do skopiowania pełne adresy URL.


## <a name="next-steps"></a>Następne kroki
* Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](overview.md).
* Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](create-uidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](create-uidefinition-elements.md).
