---
title: "aaaMigrate z usług AWS i innych platform tooManaged dyski na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie maszyn wirtualnych na platformie Azure za pomocą dysków VHD przekazanego z innych chmur, takich jak usług AWS lub innych platform wirtualizacji i korzystanie z dysków zarządzanych platformy Azure."
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
ms.date: 02/07/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 66c3912397ab905aafb3910e13ac711befb8f502
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-amazon-web-services-aws-and-other-platforms-toomanaged-disks-in-azure"></a>Migrowanie z usługi Amazon Web Services (AWS) i innych platform tooManaged dysków na platformie Azure

Możesz przekazać pliki VHD z usług AWS lub lokalnymi toocreate tooAzure rozwiązań wirtualizacji maszyn wirtualnych, które korzystają z dysków zarządzanych. Azure dysków zarządzanych eliminuje potrzebę hello toomanaging kont magazynu maszyn wirtualnych IaaS platformy Azure. Możesz tooonly, określ typ hello (Premium lub Standard) oraz rozmiar dysku, należy mieć i Azure utworzy i zarządzać hello dysku. 

Możesz przekazać ogólnych i specjalnych wirtualne dyski twarde. 
- **Uogólniony wirtualny dysk twardy** -ma wszystkie informacje osobiste Konto usunięte za pomocą programu Sysprep. 
- **Specjalizowany wirtualnego dysku twardego** -przechowuje konta użytkowników hello, aplikacji i innych danych o stanie z oryginalnego maszyny Wirtualnej. 

> [!IMPORTANT]
> Przed przekazaniem tooAzure dowolnego wirtualnego dysku twardego, należy wykonać [przygotowanie tooAzure tooupload Windows VHD lub VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
>
>


| Scenariusz                                                                                                                         | Dokumentacja                                                                                                                       |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Masz istniejące wystąpienia usług AWS EC2, czy może chcesz tooAzure toomigrate dysków zarządzanych                                     | [Przenieś Maszynę wirtualną z tooAzure Amazon Web Services (AWS)](aws-to-azure.md)                           |
| Z maszyny Wirtualnej i innych platform wirtualizacji chcieliby toouse toouse jako toocreate obrazu wiele maszyn wirtualnych Azure. | [Przekaż uogólniony wirtualny dysk twardy i korzystać z niego toocreate nowych maszyn wirtualnych na platformie Azure](upload-generalized-managed.md) |
| Masz jednoznacznie dostosowane maszyny Wirtualnej chcesz toorecreate na platformie Azure.                                                      | [Przekazywanie specjalne tooAzure wirtualnego dysku twardego i utworzyć nową maszynę Wirtualną](create-vm-specialized.md)         |


## <a name="overview-of-managed-disks"></a>Omówienie dysków zarządzanych

Zarządzane dysku systemu Azure upraszcza zarządzanie maszyny Wirtualnej przez usunięcie konta magazynu toomanage potrzeby hello. Zarządzany dysków również korzyści z większą niezawodność maszyn wirtualnych w zestawie dostępności. Gwarantuje, że dyski hello różnych maszyn wirtualnych w zestawie dostępności będzie wystarczająco odizolowane od każdego innych tooavoid pojedynczy punkt awarii. Automatycznie umieszcza dysków różnych maszyn wirtualnych w zestawie dostępności w różnych jednostkach skalowania magazynu (sygnatury) ograniczająca hello skutków błędów jednostki skalowania magazynu w jednym wywołane awarii toohardware i oprogramowania. Na podstawie Twoich potrzeb, możesz wybrać z dwóch typów pamięci masowej: 
 
- [Dysków zarządzanych w warstwie Premium](../../storage/common/storage-premium-storage.md) magazynu nośnika, który dostarcza wysokowydajnej, małe opóźnienia dysku obsługę maszyn wirtualnych działających obciążeń/O wykonujących podstawie stałych dysków stanu (SSD). Może zająć wykorzystują hello szybkości i wydajności tych dysków Migrowanie tooPremium dysków zarządzanych.  

- [Dyski standardowe zarządzane](../../storage/common/storage-standard-storage.md) Użyj stacji dysków twardych (HDD) na podstawie nośnikach magazynowania i są najbardziej odpowiednie dla: tworzenie i testowanie i innych obciążeń rzadkim dostępu, które są mniej wrażliwych zmienności tooperformance.  

## <a name="plan-for-hello-migration-toomanaged-disks"></a>Planowanie migracji hello tooManaged dysków

Ta sekcja pomoże toomake hello najlepszych decyzji w typach maszyny Wirtualnej i dysku.


### <a name="location"></a>Lokalizacja

Wybierz lokalizację, w której są dostępne dyski zarządzanych Azure. W przypadku migracji dysków zarządzanych tooPremium, upewnij się również magazyn w warstwie Premium jest dostępna w regionie hello planowanego toomigrate do. Zobacz [regionów platformy Azure](https://azure.microsoft.com/regions/#services) aktualne informacje o dostępnych lokalizacji.

### <a name="vm-sizes"></a>Rozmiary maszyn wirtualnych

W przypadku migracji dysków zarządzanych tooPremium masz tooupdate rozmiar hello hello wirtualna tooPremium rozmiar możliwością magazynu dostępnych w regionie hello, w którym znajduje się maszyna wirtualna. Przejrzyj hello rozmiarów maszyn wirtualnych, które są funkcją Magazyn w warstwie Premium. specyfikacje rozmiaru maszyny Wirtualnej Azure Hello są wymienione w [rozmiary maszyn wirtualnych](sizes.md).
Przejrzyj hello charakterystyki wydajności maszyn wirtualnych, które pracować z magazyn w warstwie Premium i wybierz polecenie hello najbardziej odpowiedni rozmiar maszyny Wirtualnej najlepiej pasujące do obciążenia. Upewnij się, czy Brak dostępnej wystarczającą przepustowość na ruchu dysku hello toodrive maszyny Wirtualnej.

### <a name="disk-sizes"></a>Rozmiary dysków

**Dysków zarządzanych w warstwie Premium**

Istnieją trzy typy dysków zarządzanych w warstwie Premium, które mogą być używane z maszyny Wirtualnej, a każdy ma określonych IOPs i przepływność limity. W przypadku wybrania hello Premium typ dysku dla maszyny Wirtualnej na podstawie hello potrzeb aplikacji pod względem wydajności, wydajności, skalowalności i ładuje szczytu, należy wziąć pod uwagę te limity.

| Typ dysków Premium  | P10               | P20               | P30               |
|---------------------|-------------------|-------------------|-------------------|
| Rozmiar dysku           | 128 GB            | 512 GB            | 1024 GB (1 TB)    |
| Liczba operacji wejścia/wyjścia na sekundę na dysk       | 500               | 2300              | 5000              |
| Przepływność na dysk | 100 MB na sekundę | 150 MB na sekundę | 200 MB / s |

**Dyski standardowe zarządzanych**

Istnieje pięć typów zarządzane standardowych dysków, które mogą być używane z maszyny Wirtualnej. Każdej z nich ma inną wydajności, ale ma tego samego IOPS i limity przepustowości. Wybierz typ hello dyski standardowe zarządzane na podstawie hello pojemności potrzeb aplikacji.

| Typ dysku standardowego  | S4               | S6               | S10              | S20              | S30              |
|---------------------|------------------|------------------|------------------|------------------|------------------|
| Rozmiar dysku           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   |
| Liczba operacji wejścia/wyjścia na sekundę na dysk       | 500              | 500              | 500              | 500              | 500              |
| Przepływność na dysk | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę | 60 MB na sekundę |

### <a name="disk-caching-policy"></a>Dyskowej pamięci podręcznej zasad 

**Dysków zarządzanych w warstwie Premium**

Domyślnie jest dyskowej pamięci podręcznej zasad *tylko do odczytu* dla wszystkich hello dysków danych w warstwie Premium i *odczytu i zapisu* dla dysku systemu operacyjnego Premium hello dołączony toohello maszyny Wirtualnej. To ustawienie konfiguracji jest zalecane tooachieve hello optymalnej wydajności dla aplikacji systemu IOs. W przypadku dysków ciężki zapisu lub w trybie tylko do zapisu danych (takich jak pliki dziennika programu SQL Server) Wyłącz buforowanie dysku, dzięki czemu można osiągnąć lepszą wydajność aplikacji.

### <a name="pricing"></a>Cennik

Przejrzyj hello [ceny dysków zarządzanych](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Cen dysków zarządzanych w warstwie Premium jest taka sama jak hello niezarządzane dysków Premium. Ale ceny dyski standardowe zarządzanych jest inny niż dyski standardowe niezarządzane.


## <a name="next-steps"></a>Następne kroki

- Przed przekazaniem tooAzure dowolnego wirtualnego dysku twardego, należy wykonać [przygotowanie tooAzure tooupload Windows VHD lub VHDX](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
