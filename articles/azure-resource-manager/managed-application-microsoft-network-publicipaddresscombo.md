---
title: "Azure zarządzanych aplikacji PublicIpAddressCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Network.PublicIpAddressCombo interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a>Element Microsoft.Network.PublicIpAddressCombo interfejsu użytkownika
Grupa służy do wybierania nowego lub istniejącego publicznego adresu IP. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- Jeśli użytkownik wybierze opcję "Brak" publicznego adresu IP, pole tekstowe etykieta nazwy domeny jest ukryty.
- Jeśli użytkownik wybierze istniejącego publicznego adresu IP, pole tekstowe etykieta nazwy domeny jest wyłączone. Wartość jest etykieta nazwy domeny wybranego adresu IP.
- Aktualizacje sufiks (na przykład westus.cloudapp.azure.com) nazwa domeny automatycznie na podstawie wybranej lokalizacji.

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
- Jeśli `constraints.required.domainNameLabel` ustawiono **true**, użytkownik musi podać etykieta nazwy domeny, podczas tworzenia nowego publicznego adresu IP. Istniejącego publicznego adresu IP, adresy bez etykiety nie są dostępne do wyboru.
- Jeśli `options.hideNone` ustawiono **true**, następnie wybrać opcję **Brak** publicznego adresu IP adres jest ukryty. Wartość domyślna to **false**.
- Jeśli `options.hideDomainNameLabel` ustawiono **true**, a następnie w polu tekstowym dla etykiety nazwy domeny jest ukryty. Wartość domyślna to **false**.
- Jeśli `options.hideExisting` ma wartość true, a następnie użytkownik nie będzie mógł wybrać istniejącego publicznego adresu IP. Wartość domyślna to **false**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
Jeśli użytkownik wybierze żadnego publicznego adresu IP, oczekiwano następujące dane wyjściowe:
```json
{
  "newOrExistingOrNone": "none"
}
```

Jeśli użytkownik wybierze nowy lub istniejący adres IP, oczekiwano następujące dane wyjściowe:
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
* Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
