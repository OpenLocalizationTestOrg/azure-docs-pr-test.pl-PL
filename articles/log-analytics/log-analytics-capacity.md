---
title: "aaaCapacity i wydajne rozwiązanie w Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Użyj hello pojemność i wydajność rozwiązania rozumiesz toohelp analizy dzienników hello wydajności serwerów funkcji Hyper-V."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 51617a6f-ffdd-4ed2-8b74-1257149ce3d4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: c47bb1e8bb9d4460b0241e89a616f3b356844b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-hyper-v-virtual-machine-capacity-with-hello-capacity-and-performance-solution-preview"></a>Planowanie pojemności maszyn wirtualnych funkcji Hyper-V z hello pojemność i wydajność rozwiązania (wersja zapoznawcza)

![Symbol pojemność i wydajność](./media/log-analytics-capacity/capacity-solution.png)

Można użyć hello pojemność i wydajność rozwiązania toohelp analizy dzienników, które należy zrozumieć hello wydajności serwerów funkcji Hyper-V. Witaj rozwiązanie zapewnia wgląd w środowisku funkcji Hyper-V poprzez wyświetlenie hello całkowitego wykorzystania (Procesora, pamięci i dysku) hello hostów i hello maszyny wirtualne na tych hostach funkcji Hyper-V. Metryki są zbierane dla Procesora, pamięci i dysków między hostami i hello maszyny wirtualne uruchomione na nich.

rozwiązanie Hello:

-   Pokazuje hostów o najwyższej i najniższej wykorzystanie Procesora i pamięci
-   Pokazuje maszyn wirtualnych o najwyższej i najniższej wykorzystanie Procesora i pamięci
-   Pokazuje maszyn wirtualnych o najwyższej i najniższej wykorzystanie IOPS i przepływności
-   Które maszyny wirtualne są uruchomione na hostach, które zawiera
-   Pokazuje hello top dysków o wysokiej przepływności, IOPS, i opóźnienia w klastrze z udostępnionymi woluminami
- Pozwala toocustomize, filtr na podstawie grup

> [!NOTE]
> Poprzednia wersja hello pojemność i wydajność rozwiązania o nazwie Zarządzanie wydajnością Hello wymagane zarówno System Center Operations Manager i System Center Virtual Machine Manager. To rozwiązanie zaktualizowany nie ma tych zależności.


## <a name="connected-sources"></a>Połączone źródła

Witaj w poniższej tabeli opisano hello połączone źródeł, które są obsługiwane przez to rozwiązanie.

| Połączone źródło | Pomoc techniczna | Opis |
|---|---|---|
| [Agenci dla systemu Windows](log-analytics-windows-agents.md) | Tak | rozwiązanie Hello zbiera pojemność i wydajność, informacje o danych z agentów systemu Windows. |
| [Agenci dla systemu Linux](log-analytics-linux-agents.md) | Nie    | rozwiązanie Hello nie zbiera pojemność i wydajność, informacje o danych z bezpośredniej agentów systemu Linux.|
| [Grupa zarządzania programu SCOM](log-analytics-om-agents.md) | Tak |rozwiązanie Hello zbiera dane pojemność i wydajność z agentów w podłączonej grupy zarządzania SCOM. Połączenie bezpośrednie z tooOMS agenta programu SCOM hello nie jest wymagane. Dane są przesyłane z hello zarządzania grupy toohello OMS repozytorium.|
| [Konto usługi Azure Storage](log-analytics-azure-storage.md) | Nie | Usługa Azure storage nie zawiera danych pojemność i wydajność.|

## <a name="prerequisites"></a>Wymagania wstępne

- W systemie Windows Server 2012 lub nowszej hosty funkcji Hyper-V, nie maszyny wirtualne muszą zostać zainstalowane z systemem Windows lub agenty programu Operations Manager.


## <a name="configuration"></a>Konfiguracja

Wykonaj powitania po kroku tooadd hello pojemność i wydajność rozwiązania tooyour obszaru roboczego.

- Dodaj hello pojemność i wydajność rozwiązania tooyour obszarem roboczym pakietu OMS za pomocą hello procesu opisanego w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).

## <a name="management-packs"></a>Pakiety administracyjne

Jeśli obszar roboczy OMS tooyour połączonych grupę zarządzania programu SCOM, następnie hello następujące pakiety administracyjne będą instalowani w SCOM po dodaniu tego rozwiązania. Nie jest wymagana żadna konfiguracja ani obsługa tych pakietów administracyjnych.

- Microsoft.IntelligencePacks.CapacityPerformance

podobne zdarzenia 1201 Hello:


```
New Management Pack with id:"Microsoft.IntelligencePacks.CapacityPerformance", version:"1.10.3190.0" received.
```

Po zaktualizowaniu hello pojemność i wydajność rozwiązania, numer wersji hello ulegnie zmianie.

Aby uzyskać więcej informacji dotyczących sposobu aktualizowania rozwiązania pakietów administracyjnych, zobacz [tooLog połączenie programu Operations Manager Analytics](log-analytics-om-agents.md).

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello

Po dodaniu hello pojemność i wydajność tooyour obszar roboczy rozwiązania hello pojemności i wydajności jest dodawana toohello pulpitu nawigacyjnego przeglądu. Ten Kafelek jest wyświetlana liczba hello liczba aktywnych hostów funkcji Hyper-V i hello liczby aktywnych maszyn wirtualnych, monitorowane wybrany okres czasu hello.

![Kafelek pojemność i wydajność](./media/log-analytics-capacity/capacity-tile.png)


### <a name="review-utilization"></a>Przegląd wykorzystania

Kliknij na powitania pojemności i wydajności kafelka tooopen hello pojemność i wydajność pulpit nawigacyjny. pulpit nawigacyjny Hello zawiera kolumny hello w hello w poniższej tabeli. Każda kolumna zawiera listę się tooten elementów pasujących do kryteriów kolumny hello określenia zakresu zakresu i czasu. Można uruchomić wyszukiwania dziennika, który zwraca wszystkie rekordy, klikając **zobaczyć wszystkie** u dołu hello hello kolumny lub przez kliknięcie nagłówka kolumny hello.

- **Hosty**
    - **Użycie procesora CPU hosta** zawiera graficzny trend wykorzystania hello Procesora hosta komputerów oraz listę hostów, oparte na powitania w wybranym okresie. Umieść kursor nad szczegóły tooview hello wiersza wykresu dla określonego punktu w czasie. Kliknij przycisk tooview wykresu hello więcej szczegółów w dzienniku wyszukiwania. Kliknij przycisk wyszukiwania dziennika tooopen nazwy hosta i Wyświetl szczegóły licznika procesora CPU dla maszyn wirtualnych w hostowanej.
    - **Użycie pamięci hosta** zawiera graficzny trend wykorzystania pamięci hello hostów i listę hostów, oparte na powitania w wybranym okresie. Umieść kursor nad szczegóły tooview hello wiersza wykresu dla określonego punktu w czasie. Kliknij przycisk tooview wykresu hello więcej szczegółów w dzienniku wyszukiwania. Kliknij przycisk dowolnego hosta nazwa tooopen dziennika wyszukiwania i widoku pamięci licznik szczegóły dla maszyn wirtualnych w hostowanej.
- **Virtual Machines**
    - **Użycie procesora CPU VM** zawiera graficzny trend wykorzystania procesora CPU hello maszyn wirtualnych oraz listę maszyn wirtualnych w wybranym okresie hello. Umieść kursor nad szczegóły tooview hello wiersza wykresu dla określonego punktu w czasie dla hello top 3 maszyn wirtualnych. Kliknij przycisk tooview wykresu hello więcej szczegółów w dzienniku wyszukiwania. Kliknij przycisk wyszukiwania dziennika tooopen nazwę maszyny Wirtualnej oraz zagregowane szczegóły licznika procesora CPU dla hello maszyny Wirtualnej.
    - **Użycie pamięci maszyny Wirtualnej** zawiera graficzny trend wykorzystania pamięci hello maszyn wirtualnych oraz listę maszyn wirtualnych w wybranym okresie hello. Umieść kursor nad szczegóły tooview hello wiersza wykresu dla określonego punktu w czasie dla hello top 3 maszyn wirtualnych. Kliknij przycisk tooview wykresu hello więcej szczegółów w dzienniku wyszukiwania. Kliknij przycisk wyszukiwania dziennika tooopen nazwę maszyny Wirtualnej i Wyświetl szczegóły licznika zagregowane pamięci dla hello maszyny Wirtualnej.
    - **Całkowita liczba IOPS dysku maszyny Wirtualnej** zawiera graficzny trend hello całkowita dysku IOPS dla maszyn wirtualnych i listę maszyn wirtualnych z hello IOPS dla poszczególnych usług, oparte na powitania w wybranym okresie. Umieść kursor nad szczegóły tooview hello wiersza wykresu dla określonego punktu w czasie dla hello top 3 maszyn wirtualnych. Kliknij przycisk tooview wykresu hello więcej szczegółów w dzienniku wyszukiwania. Kliknij przycisk wyszukiwania dziennika tooopen nazwę maszyny Wirtualnej, a widok zagregowane dysku IOPS licznika szczegóły hello maszyny Wirtualnej.
    - **Całkowita liczba przepływność dysku maszyny Wirtualnej** pokazuje graficzny trend hello przepływność dysku dla maszyn wirtualnych i listę maszyn wirtualnych o hello dysku całkowitej przepływności dla każdej, na podstawie hello wybrany okres czasu. Umieść kursor nad szczegóły tooview hello wiersza wykresu dla określonego punktu w czasie dla hello top 3 maszyn wirtualnych. Kliknij przycisk tooview wykresu hello więcej szczegółów w dzienniku wyszukiwania. Kliknij przycisk wyszukiwania dziennika tooopen nazwę maszyny Wirtualnej i wyświetlić szczegóły licznika przepływności zagregowanych całkowita dysku hello maszyny Wirtualnej.
- **Udostępnione woluminy klastra**
    - **Łączna liczba przepływności** pokazuje hello sumę zarówno odczytuje i zapisuje na udostępnione woluminy klastra.
    - **Łączna liczba IOPS** hello przedstawia sumę operacji wejścia/wyjścia na sekundę na udostępnione woluminy klastra.
    - **Całkowity czas oczekiwania** przedstawia hello łączny czas oczekiwania na udostępnione woluminy klastra.
- **Host gęstość** hello górny Kafelek zawiera hello łączna liczba rozwiązania toohello dostępnych hostów i maszyn wirtualnych. Kliknij przycisk hello najwyższym kafelków tooview dodatkowe szczegóły w dzienniku wyszukiwania. Wyświetla również wszystkie hosty i hello liczbę maszyn wirtualnych, które są obsługiwane. Kliknij przycisk toodrill hosta do maszyny Wirtualnej powoduje hello wyszukiwania dziennika.


![pulpit nawigacyjny hostów bloku](./media/log-analytics-capacity/dashboard-hosts.png)

![pulpit nawigacyjny bloku maszyny wirtualne](./media/log-analytics-capacity/dashboard-vms.png)


### <a name="evaluate-performance"></a>Ocena wydajności

Środowiska obliczeniowe o produkcyjnym się znacznie różnić tooanother jednej z organizacji. Ponadto pojemność i wydajność obciążeń może być zależna od jak maszyny wirtualne są uruchomione, i co należy wziąć pod uwagę normalne. Szczegółowe procedury toohelp pomiaru wydajności prawdopodobnie nie będą miały zastosowania tooyour środowiska. Dlatego więcej uogólniony wskazówki działa lepiej dostosowane toohelp. Firma Microsoft publikuje różnych z toohelp artykuły wskazówki pomiaru wydajności.

toosummarize, rozwiązanie hello zbiera dane pojemności i wydajności z różnych źródeł, łącznie z liczników wydajności. Tych danych pojemność i wydajność w różnych powierzchni w rozwiązaniu hello i porównać toothose Twojego wyników na powitania [pomiaru wydajności w ramach funkcji Hyper-V](https://msdn.microsoft.com/library/cc768535.aspx) artykułu. Mimo że artykuł hello został opublikowany pewien czas temu, metryki hello, uwagi i wskazówki są nadal ważne. Artykuł Hello zawiera przydatne zasoby tooother łącza.


## <a name="sample-log-searches"></a>Przykładowe wyszukiwania dzienników

Witaj w poniższej tabeli zawiera przykładowy dziennik wyszukuje pojemność i wydajność danych zebranych i obliczana na podstawie tego rozwiązania.

| Zapytanie | Opis |
|---|---|
| Wszystkie konfiguracje pamięci hosta | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="Host Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Wszystkie konfiguracje pamięci maszyny Wirtualnej | <code>Type=Perf ObjectName="Capacity and Performance" CounterName="VM Assigned Memory MB" &#124; measure avg(CounterValue) as MB by InstanceName</code> |
| Podział całkowita IOPS dysku na wszystkich maszynach wirtualnych | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Reads/s" OR CounterName="VHD Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Podział całkowitą przepływność dysku na wszystkich maszynach wirtualnych | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="VHD Read MB/s" OR CounterName="VHD Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Podział całkowita IOPS przez wszystkie woluminy CSV | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Reads/s" OR CounterName="CSV Writes/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Podział ogólnej przepustowości przez wszystkie woluminy CSV | <code>Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read MB/s" OR CounterName="CSV Write MB/s") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |
| Podział łączny czas oczekiwania przez wszystkie woluminy CSV | <code> Type=Perf ObjectName="Capacity and Performance" (CounterName="CSV Read Latency" OR CounterName="CSV Write Latency") &#124; top 2500 &#124; measure avg(CounterValue) by CounterName, InstanceName interval 1HOUR</code> |

>[!NOTE]
> Jeśli obszaru roboczego został uaktualniony toohello [języka zapytań nowe analizy dzienników](log-analytics-log-search-upgrade.md), następnie hello powyżej zapytania spowoduje zmianę następujących toohello.

> | Zapytanie | Opis |
|:--- |:--- |
| Wszystkie konfiguracje pamięci hosta | Wydajności &#124; Gdzie ObjectName == "Pojemności i wydajności" i CounterName == "Host MB pamięci przypisanej" &#124; Podsumuj MB = avg(CounterValue) przez InstanceName |
| Wszystkie konfiguracje pamięci maszyny Wirtualnej | Wydajności &#124; Gdzie ObjectName == "Pojemności i wydajności" i CounterName == "Maszyny Wirtualnej przypisanej pamięć (MB)" &#124; Podsumuj MB = avg(CounterValue) przez InstanceName |
| Podział całkowita IOPS dysku na wszystkich maszynach wirtualnych | Wydajności &#124; Gdzie ObjectName == "Pojemności i wydajności" i (CounterName == "Wirtualnego dysku twardego odczyty/s" albo CounterName == "Wirtualnego dysku twardego zapisy/s") &#124; Podsumuj AggregatedValue = avg(CounterValue) przez bin (TimeGenerated, 1 godz.), CounterName, InstanceName |
| Podział całkowitą przepływność dysku na wszystkich maszynach wirtualnych | Wydajności &#124; Gdzie ObjectName == "Pojemności i wydajności" i (CounterName == "Wirtualnego dysku twardego odczytu MB/s" albo CounterName == "MB/s zapisu dysku VHD") &#124; Podsumuj AggregatedValue = avg(CounterValue) przez bin (TimeGenerated, 1 godz.), CounterName, InstanceName |
| Podział całkowita IOPS przez wszystkie woluminy CSV | Wydajności &#124; Gdzie ObjectName == "Pojemności i wydajności" i (CounterName == "CSV odczyty/s" albo CounterName == "CSV zapisy/s") &#124; Podsumuj AggregatedValue = avg(CounterValue) przez bin (TimeGenerated, 1 godz.), CounterName, InstanceName |
| Podział ogólnej przepustowości przez wszystkie woluminy CSV | Wydajności &#124; Gdzie ObjectName == "Pojemności i wydajności" i (CounterName == "CSV odczyty/s" albo CounterName == "CSV zapisy/s") &#124; Podsumuj AggregatedValue = avg(CounterValue) przez bin (TimeGenerated, 1 godz.), CounterName, InstanceName |
| Podział łączny czas oczekiwania przez wszystkie woluminy CSV | Wydajności &#124; Gdzie ObjectName == "Pojemności i wydajności" i (CounterName == "Opóźnienie odczytu CSV" lub CounterName == "Opóźnienie zapisu CSV") &#124; Podsumuj AggregatedValue = avg(CounterValue) przez bin (TimeGenerated, 1 godz.), CounterName, InstanceName |


## <a name="next-steps"></a>Następne kroki
* Użyj [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) tooview szczegółowe dane pojemność i wydajność.
