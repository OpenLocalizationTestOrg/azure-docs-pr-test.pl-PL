---
title: "aaaMigrate dysków tooManaged maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Migrowanie maszyn wirtualnych platformy Azure utworzonych przy użyciu niezarządzanych dysków w toouse kont magazynu dysków zarządzanych."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 29420f13c4ffd5b25726e0ef1aafe89347286a89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-azure-vms-toomanaged-disks-in-azure"></a>Migrowanie maszyn wirtualnych platformy Azure tooManaged dysków na platformie Azure

Zarządzane dysku systemu Azure upraszcza zarządzanie magazynu, usuwając konieczność hello tooseparately Zarządzanie kontami magazynu.  Można migrować istniejące toobenefit dysków tooManaged maszynach wirtualnych platformy Azure z większą niezawodność maszyn wirtualnych w zestawie dostępności. Gwarantuje, że dyski hello różnych maszyn wirtualnych w zestawie dostępności będzie wystarczająco odizolowane od każdego innych tooavoid pojedynczy punkt awarii. Automatycznie umieszcza dysków różnych maszyn wirtualnych w zestawie dostępności w różnych jednostkach skalowania magazynu (sygnatury) ograniczająca hello skutków błędów jednostki skalowania magazynu w jednym wywołane awarii toohardware i oprogramowania.
Na podstawie Twoich potrzeb, możesz wybrać z dwóch typów pamięci masowej:

- [Dysków zarządzanych w warstwie Premium](../../storage/common/storage-premium-storage.md) nośnika, który dostarcza wysokowydajnej, małe opóźnienia dysku obsługę maszyn wirtualnych działających obciążeń/O wykonujących podstawie stałych dysków stanu (SSD). Może zająć wykorzystują hello szybkości i wydajności tych dysków Migrowanie tooPremium dysków zarządzanych.

- [Dyski standardowe zarządzane](../../storage/common/storage-standard-storage.md) Użyj stacji dysków twardych (HDD) na podstawie nośnikach magazynowania i są najbardziej odpowiednie dla: tworzenie i testowanie i innych obciążeń rzadkim dostępu, które są mniej wrażliwych zmienności tooperformance.

Można migrować tooManaged dysków w następujących scenariuszach:

| Migrowanie...                                            | Łącze dokumentacji                                                                                                                                                                                                                                                                  |
|----------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Konwertuj autonomiczny maszyny wirtualne i maszyny wirtualne w przypadku dysków toomanaged zestawu dostępności   | [Skonwertuj dyski toouse zarządzanych maszyn wirtualnych](convert-unmanaged-to-managed-disks.md) |
| Jednej maszyny Wirtualnej z klasycznym tooResource menedżera na dyskach zarządzanych     | [Migracja jednej maszyny Wirtualnej](migrate-single-classic-to-resource-manager.md)  | 
| Wszystkie hello maszyn wirtualnych w sieci wirtualnej z klasycznym tooResource menedżera na dyskach zarządzanych     | [Migracja zasobów IaaS z klasycznym tooResource Menedżera](migration-classic-resource-manager-ps.md) , a następnie [Konwertuj Maszynę wirtualną z dysków toomanaged niezarządzane dysków](convert-unmanaged-to-managed-disks.md) | 






## <a name="plan-for-hello-conversion-toomanaged-disks"></a>Planowanie na potrzeby konwersji hello tooManaged dysków

Ta sekcja pomoże toomake hello najlepszych decyzji w typach maszyny Wirtualnej i dysku.


## <a name="location"></a>Lokalizacja

Wybierz lokalizację, w której są dostępne dyski zarządzanych Azure. Jeśli przenosisz tooPremium zarządzane dysków, upewnij się również magazyn w warstwie Premium jest dostępna w regionie hello planowanego toomove do. Zobacz [regionów platformy Azure](https://azure.microsoft.com/regions/#services) aktualne informacje o dostępnych lokalizacji.

## <a name="vm-sizes"></a>Rozmiary maszyn wirtualnych

W przypadku migracji dysków zarządzanych tooPremium masz tooupdate rozmiar hello hello wirtualna tooPremium rozmiar możliwością magazynu dostępnych w regionie hello, w którym znajduje się maszyna wirtualna. Przejrzyj hello rozmiarów maszyn wirtualnych, które są funkcją Magazyn w warstwie Premium. specyfikacje rozmiaru maszyny Wirtualnej Azure Hello są wymienione w [rozmiary maszyn wirtualnych](sizes.md).
Przejrzyj hello charakterystyki wydajności maszyn wirtualnych, które pracować z magazyn w warstwie Premium i wybierz polecenie hello najbardziej odpowiedni rozmiar maszyny Wirtualnej najlepiej pasujące do obciążenia. Upewnij się, czy Brak dostępnej wystarczającą przepustowość na ruchu dysku hello toodrive maszyny Wirtualnej.

## <a name="disk-sizes"></a>Rozmiary dysków

**Dysków zarządzanych w warstwie Premium**

Istnieje siedem typów dysków zarządzanych w warstwie premium, które mogą być używane z maszyny Wirtualnej i każdy ma określonych IOPs i przepływność limity. Wziąć pod uwagę następujące limity wybierając hello Premium typ dysku dla maszyny Wirtualnej na podstawie hello potrzeb aplikacji pod względem wydajności, wydajności, skalowalności i ładuje godzinami szczytu.

| Typ dysków Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Rozmiar dysku           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| Liczba operacji wejścia/wyjścia na sekundę na dysk       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Przepływność na dysk | 25 MB na sekundę  | 50 MB / s  | 100 MB na sekundę | 150 MB na sekundę | 200 MB / s | 250 MB na sekundę | 250 MB na sekundę |

**Dyski standardowe zarządzanych**

Istnieje siedem typów dyski standardowe zarządzanych, które mogą być używane z maszyny Wirtualnej. Każdej z nich ma inną wydajności, ale ma tego samego IOPS i limity przepustowości. Wybierz typ hello dyski standardowe zarządzane na podstawie hello pojemności potrzeb aplikacji.

| Typ dysku standardowego  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Rozmiar dysku           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| Liczba operacji wejścia/wyjścia na sekundę na dysk       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Przepływność na dysk | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 

## <a name="disk-caching-policy"></a>Dyskowej pamięci podręcznej zasad

**Dysków zarządzanych w warstwie Premium**

Domyślnie jest dyskowej pamięci podręcznej zasad *tylko do odczytu* dla wszystkich hello dysków danych w warstwie Premium i *odczytu i zapisu* dla dysku systemu operacyjnego Premium hello dołączony toohello maszyny Wirtualnej. To ustawienie konfiguracji jest zalecane tooachieve hello optymalnej wydajności dla aplikacji systemu IOs. W przypadku dysków ciężki zapisu lub w trybie tylko do zapisu danych (takich jak pliki dziennika programu SQL Server) Wyłącz buforowanie dysku, dzięki czemu można osiągnąć lepszą wydajność aplikacji.

## <a name="pricing"></a>Cennik

Przejrzyj hello [ceny dysków zarządzanych](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Cen dysków zarządzanych w warstwie Premium jest taka sama jak hello niezarządzane dysków Premium. Ale ceny dyski standardowe zarządzanych jest inny niż dyski standardowe niezarządzane.



## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [dysków zarządzanych](managed-disks-overview.md)
