---
title: "aaaAzure zarządzanych aplikacji VirtualNetworkCombo elementu interfejsu użytkownika | Dokumentacja firmy Microsoft"
description: "Opisuje hello elementu Microsoft.Network.VirtualNetworkCombo interfejsu użytkownika dla aplikacji Azure"
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a>Element Microsoft.Network.VirtualNetworkCombo interfejsu użytkownika
Grupa służy do wybierania nowej lub istniejącej sieci wirtualnej. Użyj tego elementu po [tworzenie aplikacji zarządzanych Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Przykład interfejsu użytkownika
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- W górnym szkielet hello hello użytkownika pobrał nowej sieci wirtualnej, więc hello użytkownik może dostosować prefiks nazwy i adresu każdej podsieci. W takim przypadku Konfigurowanie podsieci jest opcjonalne.
- W szkielet dolnej hello hello użytkownik pobrał istniejącej sieci wirtualnej, więc hello użytkownika musi być zamapowany każdego szablonu wdrożenia hello podsieci wymaga tooan istniejącą podsieć. W takim przypadku Konfigurowanie podsieci jest wymagana.

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
- Jeśli zostanie określona, hello pierwszy nienakładający prefiksu adresu rozmiar `defaultValue.addressPrefixSize` jest określane automatycznie w oparciu o istniejących sieci wirtualnych w subskrypcji hello użytkownika.
- Witaj wartości domyślnej dla `defaultValue.name` i `defaultValue.addressPrefixSize` jest **null**.
- `constraints.minAddressPrefixSize`musi być określona. Wszystkie istniejące sieci wirtualne się na przestrzeń adresową mniejsze niż hello określona wartość jest niedostępna w przypadku zaznaczenia.
- `subnets`musi być określona, i `constraints.minAddressPrefixSize` musi być określona dla każdej podsieci.
- Podczas tworzenia nowej sieci wirtualnej, prefiks adresu w każdej podsieci jest obliczana automatycznie na podstawie prefiksów adresów sieci wirtualnej hello i odpowiednio `addressPrefixSize`.
- Podczas korzystania z istniejącej wirtualnych sieci, żadnych podsieci mniejsze niż odpowiednie `constraints.minAddressPrefixSize` nie są dostępne do wyboru. Ponadto jeśli jest określony, podsieci, które nie zawierają co najmniej `minAddressCount` dostępne adresy są niedostępne do wybrania.
Witaj, wartość domyślna to **0**. tooensure, który hello dostępnych adresów są ciągłe, określ **true** dla `requireContiguousAddresses`. Witaj, wartość domyślna to **true**.
- Tworzenie podsieci w istniejącej sieci wirtualnej nie jest obsługiwane.
- Jeśli `options.hideExisting` jest **true**, hello użytkownika nie można wybrać istniejącą sieć wirtualną. Witaj, wartość domyślna to **false**.

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
* Wprowadzenie toomanaged aplikacji, zobacz [zarządzanej aplikacji Azure — omówienie](managed-application-overview.md).
* Definicje interfejsu użytkownika toocreating wprowadzenie, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Opis właściwości wspólnych elementów interfejsu użytkownika, zobacz [elementy CreateUiDefinition](managed-application-createuidefinition-elements.md).
