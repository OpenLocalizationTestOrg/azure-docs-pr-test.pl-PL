---
title: "Omówienie narzędzia Monitor systemu Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 619a004b9aff99be68988e1f7be3ccad400a8a0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="overview-of-azure-monitor"></a>Omówienie usługi Azure monitora
Ten artykuł zawiera omówienie usługi Azure Monitor w Microsoft Azure. Zawarto informacje, co Azure Monitor i zawiera łącza do dodatkowych informacji na temat korzystania z monitora Azure.  Jeśli wolisz wprowadzenie wideo, zobacz dalej łącza kroki w dolnej części tego artykułu. 

## <a name="why-monitor-your-application-or-system"></a>Dlaczego monitorowania aplikacji lub systemu
Aplikacje w chmurze są złożonych z wielu części ruchu. Monitorowanie zawiera danych, aby upewnić się, że aplikacja pozostaje w górę i działa w dobrej kondycji. Pomaga również umożliwia stave potencjalne problemy i rozwiązywanie problemów w przeszłości te. Ponadto można użyć danych monitorowania w celu uzyskania szczegółowych informacji o aplikacji. Wiedzy może pomóc zwiększyć wydajność aplikacji lub utrzymania lub automatyzować czynności, które w przeciwnym razie wymagają ręcznej interwencji.


## <a name="azure-monitor-and-microsofts-other-monitoring-products"></a>Azure Monitor a firmą Microsoft przez innych produktów monitorowania
Azure Monitor udostępnia na podstawowym poziomie infrastruktury metryki i dzienniki dla większości usług platformy Microsoft Azure. Usługami Azure, których nie należy jeszcze umieszczać swoje dane do monitora Azure będzie umieszczono go w przyszłości.

Microsoft jest dostarczany dodatkowe produkty i usługi, które zapewniają dodatkowe możliwości monitorowania dla deweloperów, metodyki DevOps lub Ops IT, który ma także w przypadku instalacji lokalnych. Omówienie i zrozumienia, jak te różne produkty i usługi współpracują ze sobą, zobacz [monitorowania na platformie Microsoft Azure](monitoring-overview.md).

## <a name="monitoring-sources---compute"></a>Monitorowanie źródeł - obliczeń

![Model do monitorowania i diagnostyki dla zasobów obliczeniowych z systemem innym niż](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-compute_v6.png)

Usługi obliczeniowe obejmują: 
- Cloud Services 
- Maszyny wirtualne 
- Zestawy skalowania maszyny wirtualnej 
- Service Fabric

### <a name="application---diagnostics-logs-application-logs-and-metrics"></a>Aplikacja — dzienniki diagnostyczne, dzienniki aplikacji i metryki
Aplikacje mogą działać na podstawie systemu operacyjnego gościa w modelu obliczeń. Wysyłają własny zestaw dzienniki i metryki. Azure Monitor polega na rozszerzenia diagnostyki Azure (Windows lub Linux) do zbierania większości dzienniki i metryki na poziomie aplikacji. Typy

* Liczniki wydajności
* Dzienniki aplikacji
* Dzienniki zdarzeń systemu Windows
* Źródło zdarzenia platformy .NET
* Dzienniki programu IIS
* Manifest na podstawie ETW
* Zrzuty awaryjne
* Dzienniki błędów klienta

Bez rozszerzenia diagnostyki dostępne są tylko kilka metryk, takich jak użycie procesora CPU. 

### <a name="host-and-guest-vm-metrics"></a>Metryki hosta i gościa maszyny Wirtualnej
Zasoby obliczeniowe wymienione wcześniej mieć dedykowanego hosta maszyny Wirtualnej i ich interakcji z system operacyjny gościa. Host maszyny Wirtualnej i system operacyjny gościa są równoważne głównych maszyny Wirtualnej i gościa maszyny Wirtualnej w funkcji Hyper-V modelu funkcji hypervisor. Można zbierać metryki na serwerze. Może również zbierać dzienniki diagnostyczne na system operacyjny gościa.   

### <a name="activity-log"></a>Dziennik aktywności
Możesz wyszukać dziennik aktywności (wcześniej nazywane Operational lub dzienniki inspekcji) informacji o zasobie widziany przez infrastrukturę platformy Azure. Dziennik zawiera informacje, takie jak czas, kiedy zasoby są tworzone lub zniszczony.  Aby uzyskać więcej informacji, zobacz [omówienie dziennik aktywności](monitoring-overview-activity-logs.md). 

## <a name="monitoring-sources---everything-else"></a>Monitorowanie źródeł - wszystkie inne

![Model do monitorowania i diagnostyki dla zasobów obliczeniowych](./media/monitoring-overview-azure-monitor/Monitoring_Azure_Resources-non-compute_v6.png)


### <a name="resource---metrics-and-diagnostics-logs"></a>Zasobu, metryki i dzienniki diagnostyczne
Do zebrania metryki i informacji diagnostycznych dzienników różnić w zależności od typu zasobu. Na przykład aplikacje sieci Web zawiera dane statystyczne dotyczące operacji We/Wy dysku i procesora CPU w procentach. Te metryki nie istnieje dla kolejki usługi Service Bus, która przekazuje metryk, takich jak kolejki przepływności rozmiaru i komunikatów. Lista do zebrania metryki dla każdego zasobu jest dostępna na [obsługiwane metryki](monitoring-supported-metrics.md). 

### <a name="host-and-guest-vm-metrics"></a>Metryki hosta i gościa maszyny Wirtualnej
Nie jest zawsze mapowanie 1:1 od zasobu do określonego hosta lub maszyny Wirtualnej gościa, metryki nie są dostępne.

### <a name="activity-log"></a>Dziennik aktywności
Dziennik aktywności jest taka sama, jak w przypadku zasobów obliczeniowych.  

## <a name="uses-for-monitoring-data"></a>Używane do monitorowania danych
Po zebraniu danych można wykonywać następujące z nim w monitorze Azure

### <a name="route"></a>Trasa
Można przesyłać strumieniowo dane monitorowania do innych lokalizacji w czasie rzeczywistym.

Przykłady:

- Wyślij do usługi Application Insights, dzięki czemu można używać jej bardziej zaawansowane funkcje narzędzi wizualizacji i analizy.
- Wyślij do usługi Event Hubs, można kierować do narzędzi innych firm. 

### <a name="store-and-archive"></a>Magazyn i archiwum
Niektóre dane monitorowania jest już przechowywane i dostępne w monitorze Azure dla określonej ilości czasu. 
- Metryki są przechowywane przez 30 dni. 
- Wpisy dziennika aktywności są przechowywane przez 90 dni. 
- Dzienniki diagnostyczne nie są przechowywane w ogóle. 

Jeśli chcesz przechowywać dane dłużej niż okresów wymienionych powyżej, można użyć usługi Azure storage. Monitorowanie danych jest przechowywana w na podstawie zasad przechowywania, które można ustawić konto magazynu. Trzeba płacić za obszar danych zajmuje w magazynie Azure. 

Na kilka sposobów, aby użyć tych danych:

- Po zapisaniu, może mieć inne narzędzia wewnątrz lub na zewnątrz Azure Przeczytaj je i go przetworzyć.
- Pobierz dane lokalnie archiwum lokalnego lub zmień Twoje zasady przechowywania w chmurze i Zachowaj dane przez dłuższy czas.  
- Możesz pozostawić dane w magazynie Azure przez czas nieograniczony na potrzeby archiwizacji. 

### <a name="query"></a>Zapytanie
Azure monitora interfejsu API REST, krzyżyk polecenia interfejsu wiersza polecenia (CLI) platformy, poleceń cmdlet programu PowerShell lub zestawu .NET SDK służy do uzyskiwania dostępu do danych w systemie lub magazynu Azure

Przykłady:

* Pobieranie danych dla niestandardowych aplikacji monitorowania zapisane
* Tworzenie niestandardowych kwerend i wysyłania danych do aplikacji innych firm.

### <a name="visualize"></a>Wizualizowanie
Wizualizacja danych monitorowania w grafiki i wykresy ułatwia trendów szybsze niż wyszukiwanie za pomocą samych danych.  

Kilka metod wizualizacji obejmują:

* Korzystanie z witryny Azure Portal
* Dane trasy do usługi Azure Application Insights
* Dane trasy do Microsoft PowerBI
* Dane trasy, narzędzie wizualizacji innych firm przy użyciu albo transmisja strumieniowa na żywo lub przez narzędzie odczytywać archiwum w magazynie Azure


### <a name="automate"></a>Automatyzacja
Można użyć danych monitorowania do wyzwalania alertów lub nawet cały proces. Przykłady:

* Użyj danych do wystąpienia obliczeniowe automatycznego skalowania w górę lub w dół oparte na obciążenia aplikacji.
* Wysyłaj wiadomości e-mail, gdy metryki przecina wstępnie określoną wartość progową.
* Wywołaj adres URL sieci web (webhook) do wykonywania akcji w systemie poza platformą Azure
* Uruchom element runbook w automatyzacji Azure, aby wykonać wszelkie różnych zadań

## <a name="methods-of-accessing-azure-monitor"></a>Metody dostępu do monitora Azure
Ogólnie rzecz biorąc można manipulować danych śledzenia, routingu i pobierania za pomocą jednej z poniższych metod. Nie wszystkie metody są dostępne dla wszystkich akcji lub typów danych.

* [Witryna Azure Portal](https://portal.azure.com)
* [PowerShell](insights-powershell-samples.md)  
* [Interfejs wiersza polecenia i platform (CLI)](insights-cli-samples.md)
* [Interfejs API REST](https://docs.microsoft.com/rest/api/monitor/)
* [Zestaw SDK platformy .NET](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor)

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o
- Przewodnik wideo tylko monitora Azure znajduje się w temacie  
[Wprowadzenie do platformy Azure Monitor](https://channel9.msdn.com/Blogs/Azure-Monitoring/Get-Started-with-Azure-Monitor). Dodatkowe wideo wyjaśniający scenariusz, w których można użyć Monitora Azure znajduje się w temacie [Eksploruj Microsoft Azure, monitorowania i diagnostyki](https://channel9.msdn.com/events/Ignite/2016/BRK2234) i [Azure Monitor wideo z Ignite 2016](https://myignite.microsoft.com/videos/4977)
- Uruchom za pomocą interfejsu Azure Monitor w [wprowadzenie Azure Monitor](monitoring-get-started.md)
- Konfigurowanie [rozszerzenia diagnostyki Azure](../azure-diagnostics.md) Jeśli próbujesz do diagnozowania problemów w usłudze chmury maszyny wirtualnej maszyny wirtualnej skalowanie zestawów lub aplikacji sieci szkieletowej usług.
- [Usługa Application Insights](https://azure.microsoft.com/documentation/services/application-insights/) Jeśli próbujesz diagnostycznych problemy w aplikacji sieci Web usługi aplikacji.
- [Rozwiązywanie problemów z magazynem Azure](../storage/common/storage-e2e-troubleshooting.md) przy użyciu magazynu obiektów blob, tabel lub kolejek
- [Zaloguj się Analytics](https://azure.microsoft.com/documentation/services/log-analytics/) i [Operations Management Suite](https://www.microsoft.com/oms/)
