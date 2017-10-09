---
title: "aaaAzure zarządzanych aplikacji przekazywaniem plików elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Common.FileUpload interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Element Microsoft.Common.FileUpload interfejsu użytkownika
Formant, który umożliwia toospecify użytkownika jednego lub więcej plików tooupload. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

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
- `constraints.accept`Określa hello typy plików, które są wyświetlane w oknie dialogowym pliku hello przeglądarki. Zobacz hello [specyfikacji HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) dla dozwolone wartości. Witaj, wartość domyślna to **null**.
- Jeśli `options.multiple` ustawiono zbyt**true**, hello użytkownik może tooselect więcej niż jeden plik w przeglądarce hello okna dialogowego pliku. Witaj, wartość domyślna to **false**.
- Ten element obsługuje przekazywanie plików w dwóch trybach na podstawie wartości hello `options.uploadMode`. Jeśli **pliku** jest określony, dane wyjściowe hello zawierają hello zawartość pliku hello jako obiektu blob. Jeśli **adres url** jest określony, program hello plik jest przekazany tooa tymczasowej lokalizacji, a hello dane wyjściowe zawierają hello adres URL obiektu blob hello. Tymczasowe obiekty BLOB zostaną usunięte po 24 godzinach. Witaj, wartość domyślna to **pliku**.
- Witaj wartość `options.openMode` Określa, jak plik hello jest do odczytu. Jeśli plik hello jest oczekiwany toobe zwykłego tekstu, określ **tekst**; w przeciwnym razie, określ **binarne**. Witaj, wartość domyślna to **tekstu**.
- Jeśli `options.uploadMode` ustawiono zbyt**pliku** i `options.openMode` ustawiono zbyt**binarne**, dane wyjściowe hello jest zakodowany w formacie base64.
- `options.encoding`Określa kodowanie toouse hello podczas odczytywania pliku hello. Witaj, wartość domyślna to **UTF-8**i jest używany tylko wtedy, gdy `options.openMode` ustawiono zbyt**tekstu**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
Jeśli options.uploadMode jest plikiem options.multiple ma wartość false, następnie dane wyjściowe zawierają hello zawartość pliku hello jako ciągu JSON:

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Jeśli options.multiple ma wartość true and'options.uploadMode pliku, wówczas dane wyjściowe zawierają hello zawartość plików hello jako tablica JSON:

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

Podczas testowania CreateUiDefinition, niektóre przeglądarki (np. Google Chrome) obciąć wygenerowanym przez element Microsoft.Common.FileUpload hello w konsoli przeglądarki hello adresów URL. Może być konieczne kliknięcie tooright poszczególnych łączy toocopy hello pełne adresy URL.


## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
