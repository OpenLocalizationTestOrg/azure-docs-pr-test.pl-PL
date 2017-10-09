---
title: "Omówienie narzędzia Monitor aaaAzure | Dokumentacja firmy Microsoft"
description: "Azure Monitor zbiera statystyki dla alertów, elementów webhook, skalowania automatycznego i automatyzacji. Artykuł listy również inne opcje monitorowania firmy Microsoft."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: robb
ms.openlocfilehash: ffa304e7b158f0fceb7f60ab88fab291976aa0e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-monitor"></a>Omówienie usługi Azure monitora
Ten artykuł zawiera omówienie hello Azure monitorowania usługi platformy Microsoft Azure. Zawarto informacje, co Azure Monitor i zawiera wskaźniki tooadditional informacje na temat toouse Azure Monitor.  Jeśli wolisz wprowadzenie wideo, zobacz dalej łącza kroki na powitania dolnej części tego artykułu. 

## <a name="why-monitor-your-application-or-system"></a>Dlaczego monitorowania aplikacji lub systemu
Aplikacje w chmurze są złożonych z wielu części ruchu. Monitorowania udostępnia tooensure danych, która aplikacja pozostaje w górę i uruchomiona w dobrej kondycji. Pomaga również należy toostave wyłączone potencjalne problemy lub Rozwiązywanie problemów z przeszłości te. Ponadto można użyć monitorowania danych toogain szczegółowych informacji o aplikacji. Wiedzy może pomóc tooimprove wydajność aplikacji lub utrzymania lub automatyzować czynności, które w przeciwnym razie wymagają ręcznej interwencji.


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Azure Monitor a firmą Microsoft przez innych produktów monitorowania
Azure Monitor udostępnia na podstawowym poziomie infrastruktury metryki i dzienniki dla większości usług platformy Microsoft Azure. Usługami Azure, których nie należy jeszcze umieszczać swoje dane do monitora Azure umieści ją w tym miejscu w hello przyszłych.

Microsoft jest dostarczany dodatkowe produkty i usługi, które zapewniają dodatkowe możliwości monitorowania dla deweloperów, metodyki DevOps lub Ops IT, który ma także w przypadku instalacji lokalnych. Omówienie i zrozumienia, jak te różne produkty i usługi współpracują ze sobą, zobacz [monitorowania na platformie Microsoft Azure](monitoring-overview.md).

## <a name="monitoring-sources---compute"></a>Monitorowanie źródeł - obliczeń

![Model do monitorowania i diagnostyki dla zasobów obliczeniowych z systemem innym niż](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

usługi obliczeniowe Hello obejmują: 
- Cloud Services 
- Maszyny wirtualne 
- Zestawy skalowania maszyny wirtualnej 
- Service Fabric

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>Aplikacja — dzienniki diagnostyczne, dzienniki aplikacji i metryki
Aplikacje mogą działać na powitania systemu operacyjnego gościa w hello obliczeń modelu. Wysyłają własny zestaw dzienniki i metryki. Azure Monitor zależy od hello Azure diagnostics rozszerzenia (Windows lub Linux) toocollect większość dzienniki i metryki na poziomie aplikacji. typy Hello

* Liczniki wydajności
* Dzienniki aplikacji
* Dzienniki zdarzeń systemu Windows
* Źródło zdarzenia platformy .NET
* Dzienniki programu IIS
* Manifest na podstawie ETW
* Zrzuty awaryjne
* Dzienniki błędów klienta

Bez rozszerzenia diagnostyki hello dostępne są tylko kilka metryk, takich jak użycie procesora CPU. 

### <a name="host-and-guest-vm-metrics"></a>Metryki hosta i gościa maszyny Wirtualnej
Witaj zasoby obliczeniowe wymienione wcześniej mieć dedykowanego hosta maszyny Wirtualnej i ich interakcji z system operacyjny gościa. Hello hosta maszyny Wirtualnej i system operacyjny gościa są równoważne hello głównego maszyny Wirtualnej, jak i gościa maszyny Wirtualnej w modelu funkcji hypervisor Hyper-V hello. Można zbierać metryki na serwerze. Może również zbierać dzienniki diagnostyczne na system operacyjny gościa hello.   

### <a name="activity-log"></a>Dziennik aktywności
Możesz wyszukać hello dziennik aktywności (wcześniej nazywane Operational lub dzienniki inspekcji) informacji o zasobie widziany przez hello infrastruktury platformy Azure. Witaj dziennik zawiera informacje, takie jak czas, kiedy zasoby są tworzone lub zniszczony.  Aby uzyskać więcej informacji, zobacz [omówienie dziennik aktywności](monitoring-overview-activity-logs.md). 

## <a name="monitoring-sources---everything-else"></a>Monitorowanie źródeł - wszystkie inne

![Model do monitorowania i diagnostyki dla zasobów obliczeniowych](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>Zasobu, metryki i dzienniki diagnostyczne
Do zebrania metryki i informacji diagnostycznych dzienników różnić w zależności od typu zasobu hello. Na przykład aplikacje sieci Web zawiera dane statystyczne dotyczące hello We/Wy dysku i procesora CPU w procentach. Te metryki nie istnieje dla kolejki usługi Service Bus, która przekazuje metryk, takich jak kolejki przepływności rozmiaru i komunikatów. Lista do zebrania metryki dla każdego zasobu jest dostępna na [obsługiwane metryki](monitoring-supported-metrics.md). 

### <a name="host-and-guest-vm-metrics"></a>Metryki hosta i gościa maszyny Wirtualnej
Nie jest zawsze mapowanie 1:1 od zasobu do określonego hosta lub maszyny Wirtualnej gościa, metryki nie są dostępne.

### <a name="activity-log"></a>Dziennik aktywności
Dziennik aktywności Hello jest hello taki sam jak dla zasobów obliczeniowych.  

## <a name="uses-for-monitoring-data"></a>Używane do monitorowania danych
Po zebraniu danych można wykonać hello zgodnie z nią w monitorze Azure

### <a name="route"></a>Trasa
Można przesłać strumieniowo monitorowania lokalizacje tooother danych w czasie rzeczywistym.

Przykłady:

- Wyślij tooApplication Insights, dzięki czemu można używać jej bardziej zaawansowane funkcje narzędzi wizualizacji i analizy.
- Wyślij tooEvent koncentratory, można kierować toothird innych narzędzi. 

### <a name="store-and-archive"></a>Magazyn i archiwum
Niektóre dane monitorowania jest już przechowywane i dostępne w monitorze Azure dla określonej ilości czasu. 
- Metryki są przechowywane przez 30 dni. 
- Wpisy dziennika aktywności są przechowywane przez 90 dni. 
- Dzienniki diagnostyczne nie są przechowywane w ogóle. 

Jeśli chcesz toostore dane dłuższe niż hello okresów wymienionych powyżej, można użyć usługi Azure storage. Monitorowanie danych jest przechowywana w na podstawie zasad przechowywania, które można ustawić konto magazynu. Masz toopay dla powitalne miejsca hello danych zajmuje w magazynie Azure. 

Kilka sposobów toouse te dane:

- Po zapisaniu, może mieć inne narzędzia wewnątrz lub na zewnątrz Azure Przeczytaj je i go przetworzyć.
- Pobierz dane hello lokalnie archiwum lokalnego lub zmienić z zasadami przechowywania danych tookeep chmury hello przez dłuższy czas.  
- Możesz pozostawić hello danych w magazynie Azure przez czas nieograniczony na potrzeby archiwizacji. 

### <a name="query"></a>Zapytanie
Można użyć hello Azure Monitor REST API, międzyplatformowego interfejsu wiersza polecenia (CLI) poleceń, w przypadku poleceń cmdlet programu PowerShell lub tooaccess zestawu .NET SDK hello hello danych w systemie hello lub magazynu Azure

Przykłady:

* Pobieranie danych dla niestandardowych aplikacji monitorowania zapisane
* Tworzenie niestandardowych kwerend i wysyłanie tej aplikacji innych firm tooa danych.

### <a name="visualize"></a>Wizualizowanie
Wizualizacja danych monitorowania w grafiki i wykresy ułatwia trendów szybsze niż wyszukiwanie za pomocą hello samych danych.  

Kilka metod wizualizacji obejmują:

* Użyj hello portalu Azure
* TooAzure danych trasy usługi Application Insights
* Trasy tooMicrosoft danych usługi Power BI
* Trasy hello danych tooa wizualizacji innych firm narzędzie przy użyciu albo przesyłanie strumieniowe na żywo lub przez narzędzie hello odczytywać archiwum w magazynie Azure


### <a name="automate"></a>Automatyzacja
Możesz użyć alertów monitorowania tootrigger danych lub nawet cały proces. Przykłady:

* Użyj wystąpienia obliczeniowe tooautoscale danych w górę lub w dół oparte na obciążenia aplikacji.
* Wysyłaj wiadomości e-mail, gdy metryki przecina wstępnie określoną wartość progową.
* Wywołanie tooexecute (webhook) adres URL sieci web w systemie poza platformą Azure
* Uruchom element runbook w automatyzacji Azure tooperform żadnych różnych zadań

## <a name="methods-of-accessing-azure-monitor"></a>Metody dostępu do monitora Azure
Ogólnie rzecz biorąc można manipulować danych śledzenia, routing i pobierania za pomocą jednej z następujących metod hello. Nie wszystkie metody są dostępne dla wszystkich akcji lub typów danych.

* [Witryna Azure Portal](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [Interfejs wiersza polecenia i platform (CLI)](insights-cli-samples.md)
* [Interfejs API REST](https://docs.microsoft.com/rest/api/monitor/)
* [Zestaw SDK platformy .NET](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o
- Przewodnik wideo tylko monitora Azure znajduje się w temacie  
[Wprowadzenie do platformy Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor). Dodatkowe wideo wyjaśniający scenariusz, w których można użyć Monitora Azure znajduje się w temacie [Eksploruj Microsoft Azure, monitorowania i diagnostyki](https://channel9.msdn.com/events/Ignite/2016/BRK2234) i [Azure Monitor wideo z Ignite 2016](https://myignite.microsoft.com/videos/4977)
- Uruchom za pomocą interfejsu Azure Monitor hello w [wprowadzenie Azure Monitor](monitoring-get-started.md)
- Konfigurowanie hello [rozszerzenia diagnostyki Azure](../azure-diagnostics.md) Jeśli próbujesz toodiagnose problemów w usłudze chmury maszyny wirtualnej maszyny wirtualnej skalowanie zestawów lub aplikacji sieci szkieletowej usług.
- [Usługa Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) Jeśli próbujesz toodiagnostic problemy w aplikacji sieci Web usługi aplikacji.
- [Rozwiązywanie problemów z magazynem Azure](../storage/common/storage-e2e-troubleshooting.md) przy użyciu magazynu obiektów blob, tabel lub kolejek
- [Zaloguj się Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) i hello [Operations Management Suite](https://www.microsoft.com/oms/)
