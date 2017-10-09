---
title: "aaaAzure zarządzanych aplikacji PublicIpAddressCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Network.PublicIpAddressCombo interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Element Microsoft.Network.PublicIpAddressCombo interfejsu użytkownika
Grupa służy do wybierania nowego lub istniejącego publicznego adresu IP. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Jeśli użytkownik hello wybiera 'Brak' publicznego adresu IP, pole tekstowe etykieta nazwy domeny hello jest ukryty.
- Jeśli użytkownik hello wybiera istniejącego publicznego adresu IP, pole tekstowe etykieta nazwy domeny hello jest wyłączone. Jego wartość wynosi hello etykieta nazwy domeny adresu IP hello wybrane.
- Witaj aktualizacje sufiks (na przykład westus.cloudapp.azure.com) nazwa domeny automatycznie na podstawie hello wybrane lokalizacji.

## <a name="schema"></a>Schemat
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a>Uwagi
- Jeśli `constraints.required.domainNameLabel` ustawiono zbyt**true**, hello użytkownik musi podać etykieta nazwy domeny, podczas tworzenia nowego publicznego adresu IP. Istniejącego publicznego adresu IP, adresy bez etykiety nie są dostępne do wyboru.
- Jeśli `options.hideNone` ustawiono zbyt**true**, następnie hello tooselect opcji **Brak** hello publicznego adresu IP adres jest ukryty. Witaj, wartość domyślna to **false**.
- Jeśli `options.hideDomainNameLabel` ustawiono zbyt**true**, a następnie ukryte pole tekstowe hello etykieta nazwy domeny. Witaj, wartość domyślna to **false**.
- Jeśli `options.hideExisting` ma wartość true, a następnie hello użytkownik nie jest możliwe toochoose istniejącego publicznego adresu IP. Witaj, wartość domyślna to **false**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
Jeśli użytkownik hello wybiera żadnego publicznego adresu IP, hello następujące dane wyjściowe Oczekiwano:
```json
{
  "newOrExistingOrNone": "none"
}
```

Jeśli użytkownik hello wybiera nowy lub istniejący adres IP, hello następujące dane wyjściowe Oczekiwano:
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- Gdy `options.hideNone` jest określony, `newOrExistingOrNone` zawsze zwraca **Brak**.
- Gdy `options.hideDomainNameLabel` jest określony, `domainNameLabel` jest niezadeklarowany.

## <a name="next-steps"></a>Następne kroki
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
