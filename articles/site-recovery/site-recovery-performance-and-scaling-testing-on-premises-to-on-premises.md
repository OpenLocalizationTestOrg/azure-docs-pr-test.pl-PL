---
title: "wyniki aaaTest dla funkcji Hyper-V replikacji między lokacjami z usługi Azure Site Recovery | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje o testowanie wydajnościowe na potrzeby replikacji lokalnej tooon lokalnych maszyn wirtualnych funkcji Hyper-V za pomocą usługi Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 96ff404f-0d88-43fa-a00b-2dffde93d192
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/24/2017
ms.author: raynew
ms.openlocfilehash: 3b37542fc88e0af05e05cee78183983667618816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-results-for-on-premises-tooon-premises-hyper-v-replication-with-site-recovery"></a>Wyniki testu dla replikacji funkcji Hyper-V lokalnej tooon lokalnych z usługą Site Recovery

Można użyć tooorchestrate Microsoft Azure Site Recovery i Zarządzanie replikacją maszyn wirtualnych i serwerów fizycznych tooAzure lub tooa dodatkowego centrum danych. Ten artykuł zawiera hello wyników testowania wydajności, które robiliśmy podczas replikacji maszyn wirtualnych funkcji Hyper-V między dwiema lokalnymi centrami danych.

## <a name="test-goals"></a>Cele testu

Celem Hello testowania było tooexamine sposób wykonywania usługi Azure Site Recovery podczas replikacji stanie stabilności. Stanie stabilności replikacji występuje, gdy maszyny wirtualne ukończenie replikacji początkowej oraz synchronizacji zmiany różnicowe. Jest ważne toomeasure dane wydajności za pomocą stanie stabilności, ponieważ jest on stan hello pozostają większość maszyn wirtualnych, chyba że wystąpienia nieoczekiwanych awarii.

testowe wdrożenie na powitania obejmowały dwie lokacje lokalne na serwerze programu VMM w każdej lokacji. Tego wdrożenia testowego jest typowy head/oddział wdrożenia pakietu office, z centrali działający jako hello lokacji głównej i hello oddziału jako hello lokacji dodatkowej lub odzyskiwania.

## <a name="what-we-did"></a>Firma Microsoft może

Oto, co możemy w teście hello przeszedł:

1. Utworzone za pomocą programu VMM szablonów maszyn wirtualnych.
2. Uruchomiono maszyny wirtualne i metryk wydajności bazowej przechwytywania niż 12 godzin.
3. Utworzony chmury na serwerach VMM podstawowymi i odzyskiwania.
4. Ochrona chmury skonfigurowany w usłudze Azure Site Recovery, łącznie z mapowaniem chmur źródła i odzyskiwania.
5. Włączyć ochronę maszyn wirtualnych i zezwolić im toocomplete replikacji początkowej.
6. Oczekiwano kilku godzinach stabilizacji systemu.
7. Przechwytywane metryki wydajności niż 12 godzin, zapewnienie pozostały wszystkich maszyn wirtualnych w nieoczekiwany stan replikacji dla tych 12 godzin.
8. Miara hello różnica między metryki wydajności bazowej hello i metryk wydajności replikacji hello.


## <a name="primary-server-performance"></a>Wydajność serwera podstawowego

* Funkcja Hyper-V Replica asynchronicznie śledzi zmiany pliku dziennika tooa z narzut na przechowywanie minimalną na powitania serwera podstawowego.
* Repliki funkcji Hyper-V korzysta z własnym zapewnienia pamięci pamięci podręcznej toominimize IOPS obciążenie śledzenia. Przechowuje toohello zapisy, VHDX w pamięci i opróżnianie ich do pliku dziennika hello przed hello czasu tego dziennika hello jest wysyłana toohello odzyskiwania lokacji. Dysk opróżniania odbywa się, jeśli zapisy hello osiągnęła limit wcześniej.
* Wykres Hello poniżej przedstawia hello stanie stabilności IOPS obciążenie replikacji. Widać tego hello tooreplication nakłady pracy związane z powodu IOPS to około 5%, który jest bardzo mała.

![Podstawowy wyników](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744913.png)

Ilość pamięci na powitania serwera podstawowego toooptimize dysku wydajności korzysta z funkcji Hyper-V Replica. Jak pokazano na powitania po wykresu, pamięć, narzut na wszystkich serwerach w klastrze głównej hello jest brzegowych. Narzut pamięć Hello jest hello w procentach ilością pamięci używanej przez replikacji w porównaniu toohello całkowita zainstalowana pamięć na powitania serwera funkcji Hyper-V.

![Podstawowy wyników](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744914.png)

Funkcja Hyper-V Replica ma minimalną obciążenia Procesora. Jak pokazano na wykresie hello, obciążenia związanego z replikacją jest w zakresie hello % 2 – 3.

![Podstawowy wyników](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744915.png)

## <a name="secondary-recovery-server-performance"></a>Wydajność serwera pomocniczym (odzyskiwania)

Repliki funkcji Hyper-V korzysta z małej ilości pamięci hello odzyskiwania serwera toooptimize hello liczby operacji magazynu. Wykres Hello zawiera podsumowanie hello zużycie pamięci na powitania serwera odzyskiwania. Narzut pamięć Hello jest hello w procentach ilością pamięci używanej przez replikacji w porównaniu toohello całkowita zainstalowana pamięć na powitania serwera funkcji Hyper-V.

![Wyniki dodatkowej](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744916.png)

Hello liczby operacji We/Wy w lokacji odzyskiwania hello jest funkcją hello liczbę operacji zapisu na powitania lokacji głównej. Załóżmy Spójrz na powitania całkowita liczba operacji We/Wy na powitania odzyskiwania lokacji w porównaniu z hello całkowita liczba operacji We/Wy i operacje zapisu w lokacji głównej hello. Wykresy Hello Pokaż tym łączną hello jest IOPS na powitania odzyskiwania lokacji

* Witaj około 1,5 raza zapisu IOPS na powitania podstawowego.
* 37% hello całkowity około IOPS hello lokacji głównej.

![Wyniki dodatkowej](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744917.png)

![Wyniki dodatkowej](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744918.png)

## <a name="effect-on-network-utilization"></a>Wpływ na wykorzystanie sieci

Średnio 275 Mb na sekundę przepustowość sieci zostało użyte między hello podstawowego i węzły odzyskiwania (z włączoną kompresją) względem istniejących przepustowości 5 Gb na sekundę.

![Wykorzystanie sieci wyników](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744919.png)

## <a name="effect-on-vm-performance"></a>Wpływ na wydajność maszyny Wirtualnej

Ważną kwestią jest wpływ hello replikację w przypadku obciążeń produkcyjnych uruchomionych na maszynach wirtualnych hello. Jeśli lokacja główna hello odpowiednio jest przeznaczona do replikacji, na powitania obciążeń nie powinny istnieć żadnych skutków. Lightweight funkcji Hyper-V Replica śledzenia mechanizm zapewnia nie dotyczy obciążeń uruchomionych na maszynach wirtualnych hello podczas replikacji stanie stabilności. Jest to zilustrowane w powitania po wykresy.

Ten wykres pokazuje liczbę IOPS wykonywane przez różnych obciążeń przed maszynami wirtualnymi, po włączeniu replikacji. Można obserwować, czy nie ma żadnej różnicy między hello dwa.

![Wyniki efekt repliki](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744920.png)

Witaj Wykres ukazuje przepływności hello maszyn wirtualnych uruchomionych w różnych obciążeń przed i po włączeniu replikacji. Można obserwować, czy replikacja nie ma znaczący wpływu.

![Efekty repliki wyników](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744921.png)

## <a name="conclusion"></a>Podsumowanie

Witaj wyraźnie w wynikach usługi Azure Site Recovery, w połączeniu z funkcji Hyper-V Replica skaluje się z co najmniej w czasie dużych klastra.  Usługa Azure Site Recovery zawiera proste wdrożenie, replikacji, zarządzania i monitorowania. Repliki funkcji Hyper-V zapewnia infrastrukturę niezbędne hello zakończona pomyślnie replikacja skalowania. Do planowania wdrożenia optymalne Sugerujemy Pobierz hello [funkcji Hyper-V Replica Capacity Planner](https://www.microsoft.com/download/details.aspx?id=39057).

## <a name="test-environment-details"></a>Szczegóły środowiska testowego

### <a name="primary-site"></a>Lokacja główna

* lokacja główna Hello ma klastrze zawierającym pięć serwerów funkcji Hyper-V uruchomione maszyny wirtualne 470.
* Hello maszyny wirtualne są uruchamiane różnych obciążeń i mieć włączone ochrony Azure Site Recovery.
* Magazyn dla węzła klastra hello są udostępniane przez sieci SAN iSCSI. Model — Hitachi HUS130.
* Każdy serwer klastra ma cztery karty sieciowe (NIC) z jedną GB.
* Dwie karty sieciowe hello są sieci prywatnej iSCSI połączony tooan i są dwie sieci przedsiębiorstwa zewnętrznego podłączonego tooan. Jedną z sieci zewnętrznych hello jest zarezerwowana dla tylko na komunikację klastra.

![Podstawowe wymagania sprzętowe](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744922.png)

| Serwer | Pamięć RAM | Model | Procesor | Liczba procesorów | KARTA SIECIOWA | Oprogramowanie |
| --- | --- | --- | --- | --- | --- | --- |
| Serwery funkcji Hyper-V w klastrze: <br />ESTLAB HOST11<br />ESTLAB HOST12<br />ESTLAB HOST13<br />ESTLAB HOST14<br />ESTLAB HOST25 |128ESTLAB HOST25 ma 256 |R820 firmy Dell PowerEdge™ |Intel(R) Xeon(R) E5 procesora CPU — 4620 0 @ 2,20 GHz |4 |I GB/s x 4 |Windows Server Datacenter 2012 R2 (x64) + roli funkcji Hyper-V |
| Serwer programu VMM |2 | | |2 |1 Gb/s |Windows Server bazy danych 2012 R2 (x 64) + VMM 2012 R2 |

### <a name="secondary-recovery-site"></a>Lokacja dodatkowa (odzyskiwania)

* Witaj lokacji dodatkowej ma klastra pracy awaryjnej sześciu węzłów.
* Magazyn dla węzła klastra hello są udostępniane przez sieci SAN iSCSI. Model — Hitachi HUS130.

![Specyfikacja podstawowy sprzęt](./media/site-recovery-performance-and-scaling-testing-on-premises-to-on-premises/IC744923.png)

| Serwer | Pamięć RAM | Model | Procesor | Liczba procesorów | KARTA SIECIOWA | Oprogramowanie |
| --- | --- | --- | --- | --- | --- | --- |
| Serwery funkcji Hyper-V w klastrze: <br />ESTLAB HOST07<br />ESTLAB HOST08<br />ESTLAB HOST09<br />ESTLAB HOST10 |96 |R720 firmy Dell PowerEdge™ |Intel(R) Xeon(R) E5 procesora CPU — 2630 0 @ 2.30GHz |2 |I GB/s x 4 |Windows Server Datacenter 2012 R2 (x64) + roli funkcji Hyper-V |
| ESTLAB HOST17 |128 |R820 firmy Dell PowerEdge™ |Intel(R) Xeon(R) E5 procesora CPU — 4620 0 @ 2,20 GHz |4 | |Windows Server Datacenter 2012 R2 (x64) + roli funkcji Hyper-V |
| ESTLAB HOST24 |256 |R820 firmy Dell PowerEdge™ |Intel(R) Xeon(R) E5 procesora CPU — 4620 0 @ 2,20 GHz |2 | |Windows Server Datacenter 2012 R2 (x64) + roli funkcji Hyper-V |
| Serwer programu VMM |2 | | |2 |1 Gb/s |Windows Server bazy danych 2012 R2 (x 64) + VMM 2012 R2 |

### <a name="server-workloads"></a>Obciążenie serwera

* Do celów testowych możemy pobrać obciążeń często używane w scenariuszach dla przedsiębiorstw klienta.
* Używamy [IOMeter](http://www.iometer.org) z cech obciążenia hello podsumowane w tabeli hello na symulacyjnych.
* Wszystkie profile IOMeter są ustawiane toowrite losowych bajtów toosimulate najgorszych zapisu wzorce dla obciążeń.

| Obciążenie | We/Wy rozmiar (KB) | % Dostępu | % Odczytu | Oczekujące operacje We/Wy | Wzorzec operacji We/Wy |
| --- | --- | --- | --- | --- | --- |
| Serwer plików |48163264 |60%20%5%5%10% |80%80%80%80%80% |88888 |Wszystkie 100% losowych |
| SQL Server (woluminu 1) programu SQL Server (woluminu 2) |864 |100%100% |70%0% |88 |100% random100% sekwencyjne |
| Exchange |32 |100% |67% |8 |losowe 100% |
| Stacja robocza/VDI |464 |66%34% |70%95% |11 |Losowe zarówno 100% |
| Serwer plików w sieci Web |4864 |33%34%33% |95%95%95% |888 |Wszystkie 75% losowych |

### <a name="vm-configuration"></a>Konfiguracja maszyny Wirtualnej

* 470 maszyn wirtualnych w klastrze głównej hello.
* Wszystkie maszyny wirtualne z dysku VHDX.
* Maszyny wirtualne z obciążeniami podsumowane w tabeli hello. Wszystkie zostały utworzone szablony programu VMM.

| Obciążenie | # Maszyny wirtualne | Minimalna ilość pamięci RAM (GB) | Maksymalna ilość pamięci RAM (GB) | Rozmiar dysku logicznego (GB) dla maszyny Wirtualnej | Maksymalna liczba IOPS |
| --- | --- | --- | --- | --- | --- |
| Oprogramowanie SQL Server |51 |1 |4 |167 |10 |
| Exchange Server |71 |1 |4 |552 |10 |
| Serwer plików |50 |1 |2 |552 |22 |
| VDI |149 |.5 |1 |80 |6 |
| Serwer sieci Web |149 |.5 |1 |80 |6 |
| CAŁKOWITA LICZBA |470 | | |96.83 TB |4108 |

### <a name="site-recovery-settings"></a>Ustawienia odzyskiwania lokacji

* Usługa Azure Site Recovery został skonfigurowany do ochrony lokalnego tooon lokalnej
* Serwer VMM Hello ma cztery skonfigurowaną chmurę, zawierającą serwery klastra funkcji Hyper-V hello oraz ich maszyn wirtualnych.

| Podstawowy chmury VMM | Chronione maszyny wirtualne w chmurze hello | Częstotliwość replikacji | Dodatkowe punkty odzyskiwania |
| --- | --- | --- | --- |
| PrimaryCloudRpo15m |142 |15 minut. |Brak |
| PrimaryCloudRpo30s |47 |30 sekund |Brak |
| PrimaryCloudRpo30sArp1 |47 |30 sekund |1 |
| PrimaryCloudRpo5m |235 |5 minut. |Brak |

### <a name="performance-metrics"></a>Metryki wydajności

Tabela Hello zawiera podsumowanie hello metryki wydajności i liczniki, które zostały mierzony w hello wdrożenia.

| Metryka | Licznik |
| --- | --- |
| Procesor CPU |\Processor(_Total)\% Processor Time |
| Dostępna pamięć |\Memory\Available (MB) |
| Operacje wejścia/wyjścia |Transfery \Disk \PhysicalDisk (_Total) na sekundę |
| Maszyna wirtualna (IOPS) operacje odczytu/s |\Hyper-V wirtualne urządzenie magazynujące (<VHD>) \Read operacji na sekundę |
| Operacje zapisu (IOPS) maszyny Wirtualnej na sekundę |\Hyper-V wirtualne urządzenie magazynujące (<VHD>) \Write operacji/S |
| Przepływność odczytu dla maszyny Wirtualnej |\Hyper-V wirtualne urządzenie magazynujące (<VHD>) \Read bajty/s |
| Przepływność zapisu maszyny Wirtualnej |\Hyper-V wirtualne urządzenie magazynujące (<VHD>) \Write bajty/s |

## <a name="next-steps"></a>Następne kroki

[Konfigurowanie replikacji między dwiema lokacjami programu VMM lokalnie](site-recovery-vmm-to-vmm.md)
