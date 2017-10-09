---
title: "aaaWorking z duże zestawy skalowania maszyny wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Co należy zestawów skalowania tooknow toouse dużych maszyny wirtualnej platformy Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a>Praca z dużymi zestawami skalowania maszyn wirtualnych
Możesz teraz utworzyć Azure [zestawy skalowania maszyny wirtualnej](/azure/virtual-machine-scale-sets/) o pojemności zapasowej too1, 000 maszyn wirtualnych. W tym dokumencie _zestaw skali maszyny wirtualnej dużych_ jest zdefiniowany jako skali ustawić możliwość skalowania toogreater niż 100 maszyn wirtualnych. Ta funkcja jest ustawiana za pomocą właściwości zestawu skalowania (_singlePlacementGroup=False_). 

Ustawia niektórych aspektów dużej skali, takie jak obciążenia równoważenia i odporność domen zachowywać się inaczej zestaw standardowych skali tooa. Ten dokument opisano charakterystyki hello dużych zestawów, a w tym artykule opisano, jakie muszą tooknow toosuccessfully używane w aplikacji. 

Typowym podejściem wdrażania infrastruktury chmury na dużą skalę jest toocreate zbiór _jednostek skalowania_, na przykład przez utworzenie wielu maszyn wirtualnych skalowanie zestawów między wieloma sieciami wirtualnymi i kontami magazynu. Metoda ta umożliwia łatwiejsze zarządzanie w porównaniu toosingle maszyn wirtualnych, a wiele jednostek skalowania są przydatne w przypadku wielu aplikacji, zwłaszcza tych, które wymagają innymi urządzeniami składników, takich jak wiele sieci wirtualnych i punktów końcowych. Jeśli aplikacja wymaga jednak jeden klaster duży, może być bardziej bezpośrednie toodeploy pojedynczego skali Konfigurowanie z too1, 000 maszyn wirtualnych. Przykładowe scenariusze obejmują scentralizowane wdrożenia danych big data lub sieci obliczeniowe wymagające prostego zarządzania dużą pulą węzłów procesu roboczego. Połączone z zestawu skalowania maszyny Wirtualnej [dołączone dyski danych](virtual-machine-scale-sets-attached-disks.md), dużych zestawów pozwalają toodeploy skalowalnej infrastruktury składające się z tysiącami rdzeni i petabajtów magazynu jako jedna operacja.

## <a name="placement-groups"></a>Grupy umieszczania 
Co sprawia, że _dużych_ zestaw specjalne skalowania nie jest hello liczbę maszyn wirtualnych, ale liczba hello _umieszczania grupy_ zawiera. Grupy umieszczania to konstrukcja podobne tooan dostępności Azure zestaw, z domen błędów i domen uaktualnienia. Domyślnie zestaw skalowania składa się z pojedynczej grupy umieszczania zawierającej maksymalnie 100 maszyn wirtualnych. Jeśli właściwość o nazwie zestawu skalowania _singlePlacementGroup_ ustawiono too_false_, zestaw skali hello może składać się z wielu grup umieszczania i ma zakres 0-1000 maszyn wirtualnych. Kiedy należy ustawić wartość domyślną toohello _true_, zestaw skali składa się z grupą pojedynczego umieszczania i ma zakres 0-100 maszyn wirtualnych.

## <a name="checklist-for-using-large-scale-sets"></a>Lista kontrolna na potrzeby używania dużych zestawów skalowania
toodecide czy aplikacji ułatwia efektywne korzystanie z zestawów na dużą skalę, należy wziąć pod uwagę hello następujące wymagania:

- Duże zestawy skalowania wymagają użycia usługi Azure Managed Disks. Zestawy skalowania, które nie zostaną utworzone za pomocą usługi Managed Disks, wymagają wielu kont magazynu (jednego dla każdych 20 maszyn wirtualnych). Ustawia dużej skali są zaprojektowane toowork wyłącznie w przypadku dysków zarządzanych tooreduce ogranicza magazynu nakładów pracy zarządzania i tooavoid hello ryzyka uruchomione w subskrypcji dla konta magazynu. Nie dysków zarządzanych, zestaw skalowania jest ograniczona too100 maszyn wirtualnych.
- Zestawy skalowania utworzone z obrazów Azure Marketplace można skalować too1, 000 maszyn wirtualnych.
- Zestawy skalowania utworzone na podstawie niestandardowych obrazów (obrazów maszyn wirtualnych można utworzyć i przekazać samodzielnie) można obecnie skalowanie w górę too100 maszyn wirtualnych.
- Hello Azure Load Balancer równoważenia obciążenia dla warstwy 4 nie jest jeszcze obsługiwana dla zestawów skalowania składa się z wielu grup umieszczania. Hello toouse modułu równoważenia obciążenia Azure upewnij się, że zestaw skalowania hello jest skonfigurowany toouse grupy pojedynczego umieszczania jest ustawienie domyślne hello.
- Wszystkie zestawy skalowania warstwy 7 równoważenia obciążenia z hello Azure Application Gateway jest obsługiwana.
- Zestaw skalowania jest zdefiniowana z pojedynczą podsiecią — upewnij się, że podsieć ma przestrzeń adresową wystarczająco duży dla wszystkich hello maszyn wirtualnych należy. Domyślnie overprovisions zestawu skalowania (tworzy dodatkowe maszyny wirtualne w czasie wdrażania lub w trakcie skalowania, które nie są naliczane opłaty dotyczące) tooimprove wdrożenia niezawodność i wydajność. Zezwalaj na adres miejsca 20% większa niż liczba hello planujesz tooscale do maszyn wirtualnych.
- Jeśli planujesz toodeploy wiele maszyn wirtualnych, sieci limity przydziału rdzeni obliczeń może być konieczne toobe zwiększyć.
- Domeny błędów i domeny uaktualnień są spójne tylko w ramach grupy umieszczania. Tej architektury nie zmienia hello ogólne zestawu dostępności skali, zgodnie z maszyn wirtualnych jest rozmieszczana równomiernie wzdłuż różne sprzętu fizycznego, ale go nie oznacza, że jeśli potrzebujesz tooguarantee dwóch maszyn wirtualnych znajdują się na inny sprzęt, upewnij się, znajdują się w różnych błędów domen w hello tej samej grupie umieszczania. Identyfikator grupy błędów domeny i umieszczania są wyświetlane w hello _wystąpienia widoku_ skalę ustawić maszyny Wirtualnej. Witaj widok wystąpienia zestawu skali maszyny Wirtualnej można wyświetlić w hello [Eksploratora zasobów Azure](https://resources.azure.com/).


## <a name="creating-a-large-scale-set"></a>Tworzenie dużego zestawu skalowania
Po utworzeniu skali w hello portalu Azure, można zezwolić tooscale toomultiple umieszczania grupy przez ustawienie hello _Limit tooa umieszczania jednej grupy_ too_False_ opcji w hello _podstawy_ bloku. Z tym too_False_ zestaw opcji, możesz określić _wystąpienia licznika_ wartość zapasową too1, 000.

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

Możesz utworzyć dużej skali maszyny Wirtualnej ustawić za pomocą hello [interfejsu wiersza polecenia Azure](https://github.com/Azure/azure-cli) _az vmss utworzyć_ polecenia. To polecenie ustawia inteligentnego wartości domyślnych, takich jak rozmiar podsieci oparte na powitania _liczba wystąpień_ argumentu:

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
Należy pamiętać, że hello _vmss utworzyć_ polecenia domyślnie niektóre wartości konfiguracji, jeśli nie zostanie określony. Spróbuj toosee hello dostępne opcje, które można zastąpić:
```bash
az vmss create --help
```

Jeśli tworzysz dużej skali ustawione przez tworzenie szablonu usługi Azure Resource Manager, upewnij się, że szablon hello tworzy zestaw skalowania oparte na dyskach zarządzanych Azure. Można ustawić hello _singlePlacementGroup_ too_false_ właściwości w hello _właściwości_ sekcji hello _Microsoft.Compute/virtualMAchineScaleSets_ zasobów. Witaj poniższy fragment JSON zawiera hello początku szablonem zestaw skali, w tym hello 1000 możliwą liczbę maszyn wirtualnych i hello _"singlePlacementGroup": false_ ustawienia:
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
Pełny przykład dużą skalę należy ustawić szablon, zapoznaj się zbyt[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json).

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a>Konwertowanie istniejących skali ustawić toospan wiele grup umieszczania
toomake istniejącego zestawu skalowania maszyny wirtualnej umożliwia skalowanie toomore niż 100 maszyn wirtualnych, należy toochange hello _singplePlacementGroup_ too_false_ właściwości w skali hello wartość modelu. Możesz przetestować, zmienianie tej właściwości z hello [Eksploratora zasobów Azure](https://resources.azure.com/). Znajdowanie istniejącego zestawu skalowania, wybierz opcję _Edytuj_ i zmień hello _singlePlacementGroup_ właściwości. Jeśli ta właściwość nie jest widoczny, mogą być wyświetlane skali hello ustawić przy użyciu starszej wersji hello Microsoft.Compute interfejsu API.

>[!NOTE] 
Ustaw obsługę jednego umieszczania grupy tylko (hello domyślne zachowanie) tooa Obsługa wielu grup umieszczania skali można zmienić, ale nie można przekonwertować hello odwrotnie. W związku z tym upewnij się, że rozumiesz właściwości hello dużych zestawów przed konwersją. W szczególności upewnij się, że nie ma potrzeby hello Azure Load Balancer równoważenia obciążenia dla warstwy 4.


