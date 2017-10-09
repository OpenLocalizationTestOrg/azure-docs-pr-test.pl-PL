---
title: "aaaLearn o skali maszyny wirtualnej ustawienie szablonów | Dokumentacja firmy Microsoft"
description: "Dowiedz się toocreate minimalnej wielkości Ustaw szablon zestawy skalowania maszyny wirtualnej"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: b7a1cf6c03b22585e16db9c071d45795c8ae75df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-virtual-machine-scale-set-templates"></a>Więcej informacji na temat szablonów zestaw skali maszyny wirtualnej
[Szablony usługi Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) są toodeploy doskonały sposób grup powiązanych zasobów. Ta seria samouczek pokazuje, jak toocreate minimalnej wielkości Ustaw szablon i jak toomodify toosuit ten szablon różnych scenariuszy. Wszystkie przykłady pochodzą od tego [repozytorium GitHub](https://github.com/gatneil/mvss). 

Ten szablon jest zamierzone toobe proste. Bardziej szczegółowy przykłady skali szablonów, zobacz hello [repozytorium GitHub szablonów Szybki Start Azure](https://github.com/Azure/azure-quickstart-templates) i Wyszukaj foldery zawierające ciąg hello `vmss`.

Jeśli znasz już tworzenie szablonów, można pominąć toohello toosee sekcji "Następne kroki" jak toomodify tego szablonu.

## <a name="review-hello-template"></a>Szablon hello przeglądu

Użyj GitHub tooreview naszych minimalnej wielkości Ustaw szablon, [azuredeploy.json](https://raw.githubusercontent.com/gatneil/mvss/minimum-viable-scale-set/azuredeploy.json).

W tym samouczku omówione różnicowego hello (`git diff master minimum-viable-scale-set`) toocreate hello minimalnej wielkości Ustaw szablon element przez element.

## <a name="define-schema-and-contentversion"></a>Zdefiniuj $schema i contentVersion
Najpierw należy zdefiniować `$schema` i `contentVersion` hello szablonu. Witaj `$schema` element definiuje hello wersji języka szablonu hello i jest używany dla programu Visual Studio wyróżnianie składni i podobne funkcje sprawdzania poprawności. Witaj `contentVersion` element nie jest używany przez platformę Azure. Zamiast tego należy go pomaga śledzić hello wersji szablonu.

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
  "contentVersion": "1.0.0.0",
```
## <a name="define-parameters"></a>Zdefiniuj parametry
Następnie należy zdefiniować dwa parametry `adminUsername` i `adminPassword`. Parametry są podane w czasie hello wdrożenia wartości. Hello `adminUsername` parametr jest po prostu `string` typu, ale ponieważ `adminPassword` jest klucz tajny, zapewniamy im typu `securestring`. Później te parametry są przekazywane do hello skali zestawu konfiguracji.

```json
  "parameters": {
    "adminUsername": {
      "type": "string"
    },
    "adminPassword": {
      "type": "securestring"
    }
  },
```
## <a name="define-variables"></a>Definiowanie zmiennych
Szablony Menedżera zasobów pozwalają również zdefiniować toobe zmienne używane w dalszej części hello szablonu. Naszym przykładzie nie używa żadnych zmiennych, więc mamy już puste hello obiekt JSON.

```json
  "variables": {},
```

## <a name="define-resources"></a>Definiowanie zasobów
Następnie jest sekcja zasobów hello hello szablonu. W tym miejscu możesz zdefiniować elementy faktycznie toodeploy. W odróżnieniu od `parameters` i `variables` (które są obiektów JSON), `resources` znajduje się lista JSON obiektów JSON.

```json
   "resources": [
```

Wszystkie zasoby wymagają `type`, `name`, `apiVersion`, i `location` właściwości. W tym przykładzie pierwszy zasób ma typ `Microsft.Network/virtualNetwork`, nazwa `myVnet`i apiVersion `2016-03-30`. (toofind hello najnowszą wersją interfejsu API dla typu zasobu, zobacz hello [dokumentacji interfejsu API REST Azure](https://docs.microsoft.com/rest/api/).)

```json
     {
       "type": "Microsoft.Network/virtualNetworks",
       "name": "myVnet",
       "apiVersion": "2016-12-01",
```

## <a name="specify-location"></a>Określ lokalizację
używamy lokalizacji hello toospecify hello sieci wirtualnej, [funkcji szablonu usługi Resource Manager](../azure-resource-manager/resource-group-template-functions.md). Ta funkcja musi być ujęta w cudzysłowy i nawiasy kwadratowe następująco: `"[<template-function>]"`. W takim przypadku stosujemy hello `resourceGroup` funkcji. Go przyjmuje żadnych argumentów i zwraca obiekt JSON z metadanymi o hello grupy zasobów, który jest wdrażany tego wdrożenia. Grupa zasobów Hello jest ustawione przez użytkownika hello w czasie hello wdrożenia. Firma Microsoft, a następnie indeks do tego obiektu JSON `.location` tooget hello lokalizacji z obiektu JSON hello.

```json
       "location": "[resourceGroup().location]",
```

## <a name="specify-virtual-network-properties"></a>Określ właściwości sieci wirtualnej
Każdy zasób usługi Resource Manager ma własną `properties` sekcji konfiguracji toohello określonego zasobu. W takim przypadku określono tej sieci wirtualnej hello powinny mieć jedną podsieć przy użyciu hello zakresu prywatnych adresów IP `10.0.0.0/16`. Zestaw skali zawsze znajduje się w obrębie jednej podsieci. Nie może występować w podsieci.

```json
       "properties": {
         "addressSpace": {
           "addressPrefixes": [
             "10.0.0.0/16"
           ]
         },
         "subnets": [
           {
             "name": "mySubnet",
             "properties": {
               "addressPrefix": "10.0.0.0/16"
             }
           }
         ]
       }
     },
```

## <a name="add-dependson-list"></a>Dodaj listę dependsOn
Ponadto wymagane toohello `type`, `name`, `apiVersion`, i `location` właściwości, każdy zasób może mieć opcjonalny `dependsOn` lista ciągów. Określa tej listy, która innych zasobów z tego wdrożenia musi zakończyć się przed wdrożeniem tego zasobu.

W takim przypadku istnieje tylko jeden element na liście hello hello sieci wirtualnej z poprzedniego przykładu hello. Możemy określić tę zależność, ponieważ hello zestawu skalowania wymaga hello tooexist sieci przed utworzeniem żadnej maszyny wirtualnej. W ten sposób hello zestaw skali można nadać tych maszyn wirtualnych prywatnych adresów IP z zakresu adresów IP hello wcześniej określona we właściwościach sieci hello. format Hello każdego ciągu na liście dependsOn hello jest `<type>/<name>`. Użyj hello sam `type` i `name` wcześniej używane w definicji zasobu hello sieci wirtualnej.

```json
     {
       "type": "Microsoft.Compute/virtualMachineScaleSets",
       "name": "myScaleSet",
       "apiVersion": "2016-04-30-preview",
       "location": "[resourceGroup().location]",
       "dependsOn": [
         "Microsoft.Network/virtualNetworks/myVnet"
       ],
```
## <a name="specify-scale-set-properties"></a>Określ właściwości zestawu skali
Zestawy skalowania ma wiele właściwości dostosowywania maszyn wirtualnych hello w zestawie skalowania hello. Aby uzyskać pełną listę tych właściwości, zobacz hello [dokumentacja interfejsu API REST zestawu skalowania](https://docs.microsoft.com/en-us/rest/api/virtualmachinescalesets/create-or-update-a-set). W tym samouczku będziemy ustawi tylko kilka właściwości często używane.
### <a name="supply-vm-size-and-capacity"></a>Rozmiar maszyny Wirtualnej i pojemności
skali Hello Ustaw tooknow potrzeb, jaki rozmiar toocreate maszyny Wirtualnej ("Nazwa jednostki sku") i jak wiele takich maszyn wirtualnych toocreate ("pojemność jednostki sku"). toosee rozmiarów maszyn wirtualnych, które są dostępne, zobacz hello [dokumentacji rozmiarów maszyn wirtualnych](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-sizes).

```json
       "sku": {
         "name": "Standard_A1",
         "capacity": 2
       },
```

### <a name="choose-type-of-updates"></a>Wybierz typ aktualizacji
zestaw skali Hello musi także tooknow sposób aktualizowania toohandle na powitania zestaw skali. Obecnie dostępne są dwie opcje `Manual` i `Automatic`. Aby uzyskać więcej informacji na powitania różnice między dwoma hello, zobacz dokumentację hello [tooupgrade skali konfiguracji](./virtual-machine-scale-sets-upgrade-scale-set.md).

```json
       "properties": {
         "upgradePolicy": {
           "mode": "Manual"
         },
```

### <a name="choose-vm-operating-system"></a>Wybierz system operacyjny maszyny Wirtualnej
Witaj zestawu skalowania tooknow potrzeb tooput jakiego systemu operacyjnego na maszynach wirtualnych hello. W tym miejscu utworzymy hello maszyn wirtualnych z obrazem 16.04 LTS Ubuntu pełni poprawioną.

```json
         "virtualMachineProfile": {
           "storageProfile": {
             "imageReference": {
               "publisher": "Canonical",
               "offer": "UbuntuServer",
               "sku": "16.04-LTS",
               "version": "latest"
             }
           },
```

### <a name="specify-computernameprefix"></a>Określ element computerNamePrefix
zestaw skali Hello wdraża wiele maszyn wirtualnych. Zamiast określania nazwy maszyny Wirtualnej, jest określona `computerNamePrefix`. Hello zestaw skali dołącza prefiks toohello indeksu dla każdej maszyny Wirtualnej, więc nazw maszyn wirtualnych jest formularz hello `<computerNamePrefix>_<auto-generated-index>`.

W następujących fragment hello używamy parametry hello z przed tooset hello administratora użytkownika i hasło dla wszystkich maszyn wirtualnych w zestawie skalowania hello. Firma Microsoft to zrobić z hello `parameters` funkcji szablonu. Ta funkcja przyjmuje ciąg, który określa, które tooand toorefer parametru generuje hello wartości tego parametru.

```json
           "osProfile": {
             "computerNamePrefix": "vm",
             "adminUsername": "[parameters('adminUsername')]",
             "adminPassword": "[parameters('adminPassword')]"
           },
```

### <a name="specify-vm-network-configuration"></a>Określ konfigurację sieci maszyny Wirtualnej
Na koniec potrzebujemy konfiguracji sieci hello toospecify dla maszyn wirtualnych hello w zestawie skalowania hello. W takim przypadku tylko potrzebujemy toospecify hello identyfikator podsieci hello utworzony wcześniej. Ta wartość informuje zestawu skali hello tooput hello interfejsów sieciowych w tej podsieci.

Możesz uzyskać identyfikator hello hello sieci wirtualnych zawierających hello podsieci przy użyciu hello `resourceId` funkcji szablonu. Ta funkcja przyjmuje hello typem i nazwą zasobu i zwraca hello pełny identyfikator zasobu. Ten identyfikator ma hello formularza:`/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/<resourceProviderNamespace>/<resourceType>/<resourceName>`

Jednak hello identyfikator hello sieci wirtualnej nie jest wystarczająco. Należy określić hello określonej podsieci, która hello zestawu skalowania maszyn wirtualnych powinny być w. toodo, łączenie `/subnets/mySubnet` toohello identyfikator hello sieci wirtualnej. wynik Hello jest identyfikator hello w pełni kwalifikowana hello podsieci. Czy to łączenia z hello `concat` funkcji, która przyjmuje w szeregu ciągi i zwraca ich łączenie.

```json
           "networkProfile": {
             "networkInterfaceConfigurations": [
               {
                 "name": "myNic",
                 "properties": {
                   "primary": "true",
                   "ipConfigurations": [
                     {
                       "name": "myIpConfig",
                       "properties": {
                         "subnet": {
                           "id": "[concat(resourceId('Microsoft.Network/virtualNetworks', 'myVnet'), '/subnets/mySubnet')]"
                         }
                       }
                     }
                   ]
                 }
               }
             ]
           }
         }
       }
     }
   ]
}

```

## <a name="next-steps"></a>Następne kroki

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
