---
title: "AAA \"Tworzenie puli partii zadań Azure zdarzenia | Dokumentacja firmy Microsoft\""
description: "Dokumentacja dotycząca puli partii utworzyć zdarzenia."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: ad31251969af553baa21e8c533d8ea95d3eeaf91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-create-event"></a>Tworzenie puli zdarzenia

 To zdarzenie jest emitowany po utworzeniu puli. Ogólne informacje o puli hello powoduje to udostępnienie zawartości Hello hello dziennika. Należy pamiętać, że jeśli rozmiar docelowy hello puli hello jest większa niż 0 węzły obliczeniowe, start zdarzenie zmiany rozmiaru puli będzie występować natychmiast po tym zdarzeniu.

 Witaj poniższy przykład przedstawia treści hello puli utworzyć zdarzenia dla puli utworzone za pomocą właściwości CloudServiceConfiguration hello.

```
{
    "id": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "3",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicated": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoScale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

|Element|Typ|Uwagi|
|-------------|----------|-----------|
|id|Ciąg|Identyfikator Hello hello puli.|
|Nazwa wyświetlana|Ciąg|Nazwa puli hello wyświetlana Hello.|
|vmSize|Ciąg|rozmiar Hello hello maszyn wirtualnych w puli hello. Wszystkie maszyny wirtualne w puli są hello sam rozmiar. <br/><br/> Aby uzyskać informacje o dostępnych rozmiarów maszyn wirtualnych dla usług w chmurze pule (pule utworzone za pomocą cloudServiceConfiguration), zobacz [rozmiary dla usług w chmurze](http://azure.microsoft.com/documentation/articles/cloud-services-sizes-specs/). Wsadowe obsługuje wszystkich rozmiarów maszyn wirtualnych usługi w chmurze, z wyjątkiem `ExtraSmall`.<br/><br/> Informacje o dostępności VM rozmiary pule przy użyciu obrazów z hello Marketplace maszyn wirtualnych (pule utworzone za pomocą virtualMachineConfiguration) dla [rozmiary maszyn wirtualnych](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-sizes/) (Linux) lub [rozmiarów dla Maszyny wirtualne](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) (system Windows). Usługa Batch obsługuje wszystkie rozmiary maszyn wirtualnych platformy Azure oprócz `STANDARD_A0` i maszyn z usługi Premium Storage (seria `STANDARD_GS`, `STANDARD_DS` i `STANDARD_DSV2`).|
|[cloudServiceConfiguration](#bk_csconf)|Typ złożony|Konfiguracja usługi chmury Hello hello puli.|
|[virtualMachineConfiguration](#bk_vmconf)|Typ złożony|konfiguracja maszyny wirtualnej Hello hello puli.|
|[Konfiguracja sieci](#bk_netconf)|Typ złożony|Konfiguracja sieci Hello hello puli.|
|resizeTimeout|Time|limit czasu Hello alokacji puli toohello węzły obliczeniowe określony dla ostatniej operacji zmiany rozmiaru hello na powitania puli.  (hello początkowej zmiany rozmiaru, gdy hello tworzona jest pula liczby jako zmiany rozmiaru).|
|targetDedicated|Int32|Witaj liczba węzłów obliczeniowych, które są żądane hello puli.|
|enableAutoScale|wartość logiczna|Określa, czy rozmiar puli hello automatycznie dostosowuje się wraz z upływem czasu.|
|enableInterNodeCommunication|wartość logiczna|Określa, czy pula hello jest skonfigurowane do bezpośrednia komunikacja między węzłami.|
|isAutoPool|wartość logiczna|Speficies czy puli hello został utworzony za pomocą mechanizmu AutoPool zadania.|
|maxTasksPerNode|Int32|Witaj maksymalna liczba zadań, które można uruchomić jednocześnie w jednym węźle obliczeń w puli hello.|
|vmFillType|Ciąg|Określa, jak usługa partia zadań hello dystrybuuje zadań między węzły obliczeń w puli hello. Prawidłowe wartości są rozkładane lub pakiecie.|

###  <a name="bk_csconf"></a>cloudServiceConfiguration

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|Rodzina systemów operacyjnych|Ciąg|Hello Azure systemu operacyjnego gościa rodziny toobe zainstalowane na powitania maszyn wirtualnych w puli hello.<br /><br /> Możliwe wartości:<br /><br /> **2** — systemu operacyjnego z rodziny 2, odpowiednik tooWindows Server 2008 R2 z dodatkiem SP1.<br /><br /> **3** — 3 rodziny systemu operacyjnego, odpowiednik tooWindows Server 2012.<br /><br /> **4** — 4 rodziny systemu operacyjnego, odpowiednik tooWindows Server 2012 R2.<br /><br /> Aby uzyskać więcej informacji, zobacz [poszczególnych wersji systemu operacyjnego gościa Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|
|targetOSVersion|Ciąg|Witaj zainstalowane na powitania maszyn wirtualnych w puli hello toobe wersji systemu operacyjnego gościa Azure.<br /><br /> Witaj, wartość domyślna to  **\***  określającej hello najnowszej wersji systemu operacyjnego dla hello określonej rodziny.<br /><br /> Dla innych dozwolonych wartości [poszczególnych wersji systemu operacyjnego gościa Azure](https://azure.microsoft.com/documentation/articles/cloud-services-guestos-update-matrix/#releases).|

###  <a name="bk_vmconf"></a>virtualMachineConfiguration

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|[elementu imageReference](#bk_imgref)|Typ złożony|Określa informacje dotyczące platformy hello lub toouse obrazu witryny Marketplace.|
|nodeAgentSKUId|Ciąg|Witaj jednostki SKU agenta węzła partii hello udostępniane w węźle obliczeń hello.|
|[windowsConfiguration](#bk_winconf)|Typ złożony|Określa ustawienia systemu operacyjnego Windows hello maszyny wirtualnej. Ta właściwość nie może być określony, jeśli elementu imageReference hello odwołuje się do obrazu systemu operacyjnego Linux.|

###  <a name="bk_imgref"></a>elementu imageReference

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|Wydawcy|Ciąg|Wydawca Hello hello obrazu.|
|Oferta|Ciąg|Oferta Hello hello obrazu.|
|Jednostka SKU|Ciąg|Jednostka SKU obrazu hello Hello.|
|Wersja|Ciąg|Wersja Hello hello obrazu.|

###  <a name="bk_winconf"></a>windowsConfiguration

|Nazwa elementu|Typ|Uwagi|
|------------------|----------|-----------|
|enableAutomaticUpdates|Wartość logiczna|Wskazuje, czy hello maszyny wirtualnej jest włączona funkcja Aktualizacje automatyczne. Jeśli ta właściwość nie jest określona, wartością domyślną hello jest PRAWDA.|

###  <a name="bk_netconf"></a>Konfiguracja sieci

|Nazwa elementu|Typ|Uwagi|
|------------------|--------------|----------|
|subnetId|Ciąg|Określa identyfikator zasobu hello hello podsieci, w których puli hello obliczeń węzły zostały utworzone.|
