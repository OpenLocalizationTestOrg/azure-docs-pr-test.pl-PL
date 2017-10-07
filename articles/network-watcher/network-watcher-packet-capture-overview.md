---
title: Przechwytywanie tooPacket aaaIntroduction w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera przegląd możliwości przechwytywania pakietów obserwatora sieciowego hello"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3a81afaa-ecd9-4004-b68e-69ab56913356
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2ce01b391b9c1a1c19aa29c8620628c55586df03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toovariable-packet-capture-in-azure-network-watcher"></a>Wprowadzenie przechwytywania pakietów toovariable w obserwatora sieciowego Azure

Przechwytywania pakietów zmiennej obserwatora sieciowego umożliwia toocreate pakietów przechwytywania sesji tootrack ruch tooand z maszyny wirtualnej. Przechwytywania pakietów pomaga anomalii sieci toodiagnose zarówno rozbudowy i proactivity. Innych celów obejmują zbieranie statystyk sieciowych, uzyskanie informacji na temat sieci wtargnięcia toodebug klient serwer, komunikację i o wiele więcej.

Przechwytywania pakietów jest uruchamiana zdalnie za pomocą Monitora sieci rozszerzenia maszyny wirtualnej. Funkcja ta ułatwia hello obciążeń uruchomionych przechwytywania pakietów ręcznego na potrzeby hello maszynę wirtualną, która zapisuje cenny czas. Przechwytywania pakietów mogą być wyzwalane za pośrednictwem portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST. Przykład sposobu przechwytywania pakietów mogą być wyzwalane jest z alertami maszyny wirtualnej. Filtry są dostarczane do tooensure sesji przechwytywania hello przechwytywania ruchu sieciowego ma toomonitor. Filtry są oparte na krotce 5 (protokół, lokalny adres IP zdalnego adresu IP, portu lokalnego i portu zdalnego) informacje. Witaj przechwycone dane są przechowywane w hello dysku lokalnego lub obiektu blob magazynu. Ma limitu 10 sesji przechwytywania pakietów, na region na subskrypcję. Ten limit dotyczy tylko toohello sesje i nie ma zastosowania toohello zapisane pliki przechwytywania pakietów lokalnie na powitania maszyny Wirtualnej lub na koncie magazynu.

> [!IMPORTANT]
> Rozszerzenie maszyny wirtualnej wymaga przechwytywania pakietów `AzureNetworkWatcherExtension`. Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).

informacje hello tooreduce przechwytywania tooonly hello informacje, które mają, hello poniższe opcje są dostępne dla sesji przechwytywania pakietów:

**Przechwytywanie konfiguracji**

|Właściwość|Opis|
|---|---|
|**Maksymalna liczba bajtów na pakietu (w bajtach)** | Witaj liczbę bajtów z każdego pakietu, które są przechwytywane, wszystkie bajty są przechwytywane, jeśli pole pozostanie puste. Witaj liczbę bajtów z każdego pakietu, które są przechwytywane, wszystkie bajty są przechwytywane, jeśli pole pozostanie puste. Jeśli potrzebujesz tylko nagłówek IPv4 hello — wskazuje 34 tutaj |
|**Maksymalna liczba bajtów na sesji (w bajtach)** | Całkowita liczba bajtów, w którym są przechwytywane po wartości hello osiągnięciu hello zakończenia sesji.|
|**Limit czasu (w sekundach)** | Ustawia czas ograniczenie pakietów hello przechwytywania sesji. Wartość domyślna Hello jest 18000 sekund lub 5 godzin.|

**Filtrowanie (opcjonalnie)**

|Właściwość|Opis|
|---|---|
|**Protokół** | Witaj toofilter protokołu dla pakietów hello przechwytywania. Witaj dostępne wartości to TCP, UDP i wszystkie.|
|**Lokalny adres IP** | Ta wartość filtruje toopackets przechwytywania pakietów hello, jeśli hello lokalny adres IP odpowiada to wartości filtru.|
|**Port lokalny** | Ten pakiet hello filtry wartość przechwytywania toopackets, jeśli port lokalny hello odpowiada tej wartości filtru.|
|**Zdalny adres IP** | Ten pakiet hello filtry wartość przechwytywania toopackets Jeśli hello zdalny adres IP odpowiada to wartości filtru.|
|**Port zdalny** | Ten pakiet hello filtry wartość przechwytywania toopackets, jeśli port zdalny hello odpowiada tej wartości filtru.|

### <a name="next-steps"></a>Następne kroki

Dowiedz się, jak można zarządzać przechwytywania pakietów, za pośrednictwem portalu hello odwiedzając [Zarządzanie przechwytywania pakietów w portalu Azure hello](network-watcher-packet-capture-manage-portal.md) lub przy użyciu programu PowerShell, odwiedzając [Zarządzanie przechwytywania pakietów przy użyciu programu PowerShell](network-watcher-packet-capture-manage-powershell.md).

Dowiedz się, jak przechwytywanie pakietów aktywnego toocreate na podstawie maszyny wirtualnej alertów, odwiedzając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)

<!--Image references-->
[1]: ./media/network-watcher-packet-capture-overview/figure1.png













