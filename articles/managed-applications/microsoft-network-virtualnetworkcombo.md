---
title: "Azure zarządzanych aplikacji VirtualNetworkCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opis elementu Microsoft.Network.VirtualNetworkCombo interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: c17ef740dcc709b5b344c4e60ef997a948b2e5de
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Element Microsoft.Network.VirtualNetworkCombo interfejsu użytkownika
Grupa służy do wybierania nowej lub istniejącej sieci wirtualnej. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](publish-service-catalog-app.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- Szkielet top użytkownik pobrał nowej sieci wirtualnej, więc użytkownik może dostosować prefiks nazwy i adresu każdej podsieci. W takim przypadku Konfigurowanie podsieci jest opcjonalne.
- Szkielet dolnej użytkownik pobrał istniejącej sieci wirtualnej, więc użytkownik musi być zamapowany każdej podsieci, wymagane przez szablon wdrożenia na istniejącą podsieć. W takim przypadku Konfigurowanie podsieci jest wymagana.

## <a name="schema"></a>Schemat
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a>Uwagi
- Jeśli jest określony, pierwszy nienakładający adres prefiks rozmiar `defaultValue.addressPrefixSize` jest określane automatycznie w oparciu o istniejących sieci wirtualnych w subskrypcji użytkownika.
- Wartość domyślna dla `defaultValue.name` i `defaultValue.addressPrefixSize` jest **null**.
- `constraints.minAddressPrefixSize`musi być określona. Istniejących sieci wirtualnych się na przestrzeń adresową mniejszą niż określona wartość są niedostępne do wybrania.
- `subnets`musi być określona, i `constraints.minAddressPrefixSize` musi być określona dla każdej podsieci.
- Podczas tworzenia nowej sieci wirtualnej, prefiks adresu w każdej podsieci jest obliczana automatycznie na podstawie prefiksów adresów sieci wirtualnej i odpowiednio `addressPrefixSize`.
- Podczas korzystania z istniejącej wirtualnych sieci, żadnych podsieci mniejsze niż odpowiednie `constraints.minAddressPrefixSize` nie są dostępne do wyboru. Ponadto jeśli jest określony, podsieci, które nie zawierają co najmniej `minAddressCount` dostępne adresy są niedostępne do wybrania.
Wartość domyślna to **0**. Aby upewnić się, że dostępnych adresów są ciągłe, określ **true** dla `requireContiguousAddresses`. Wartość domyślna to **true**.
- Tworzenie podsieci w istniejącej sieci wirtualnej nie jest obsługiwane.
- Jeśli `options.hideExisting` jest **true**, użytkownik nie może wybrać istniejącej sieci wirtualnej. Wartość domyślna to **false**.

## <a name="sample-output"></a>Przykładowe dane wyjściowe
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a>Następne kroki
* Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [zarządzanej aplikacji Azure — omówienie](overview.md).
* Aby obejrzeć wprowadzenie do tworzenia definicji interfejsu użytkownika, zobacz [wprowadzenie CreateUiDefinition](create-uidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](create-uidefinition-elements.md).
