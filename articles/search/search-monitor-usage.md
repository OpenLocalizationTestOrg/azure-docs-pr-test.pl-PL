---
title: "aaaMonitor użycia oraz statystyki w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Śledzenie rozmiar konsumenckich i indeksu zasobów dla usługi wyszukiwanie Azure, Usługa wyszukiwania w chmurze hostowanej w systemie Microsoft Azure."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Monitorowanie usługi Azure Search

Usługa Azure Search udostępnia różnych zasobów do śledzenia użycia i wydajności usługi wyszukiwania. Daje dostęp do toometrics, dzienniki statystyki indeksu i rozszerzone możliwości monitorowania usługi Power BI. W tym artykule opisano sposób tooenable hello różne strategie monitorowania i jak toointerpret hello danych.

## <a name="azure-search-metrics"></a>Metryki usługi Azure Search
Metryki zapewniają niemal w czasie rzeczywistym widoczność usługi wyszukiwania i są dostępne dla każdej usługi, bez dodatkowych ustawień. Umożliwiają one śledzenia wydajności hello usługi dla się too30 dni.

Usługa Azure Search zbiera dane dla trzech różnych metryki:

* Wyszukaj opóźnienia: czasu usługi wyszukiwania hello potrzebne tooprocess kwerendy wyszukiwania, agregowane na minutę.
* Wyszukaj zapytania na sekundę (QPS): liczba wyszukiwania zapytań odebranych na sekundę, agregowane na minutę.
* Wartość procentowa zapytań wyszukiwania z ograniczeniem przepustowości: procent zapytania wyszukiwania, które zostały ograniczany agregowana na minutę.

![Zrzut ekranu QPS działania][1]

### <a name="set-up-alerts"></a>Konfigurowanie alertów
Na stronie szczegółów metryki hello można skonfigurować tootrigger alerty przeniesienia wiadomość e-mail z powiadomieniem lub akcji automatycznej podczas metrykę przekracza wartość progową, który został zdefiniowany.

Aby uzyskać więcej informacji na temat metryki dokumentacji hello pełna w monitorze Azure.  

## <a name="how-tootrack-resource-usage"></a>Sposób użycia zasobów tootrack
Śledzenia wzrostu hello indeksy i rozmiar dokumentu może pomóc aktywnie Dostosuj wydajność przed szukaniem hello górny limit, który został określony dla usługi. Można to zrobić w portalu hello lub programowo przy użyciu hello interfejsu API REST.

### <a name="using-hello-portal"></a>Za pomocą portalu hello

użycie zasobów toomonitor, wyświetlanie liczby hello i statystyki dla usługi hello [portal](https://portal.azure.com).

1. Zaloguj się toohello [portal](https://portal.azure.com).
2. Otwórz pulpit nawigacyjny usługi hello usługi Azure Search. Kafelki hello usługi można znaleźć na stronie głównej hello, lub możesz wyszukać usługę toohello przy użyciu funkcji przeglądania na powitania przechodzenia.

Witaj sekcji użycia obejmuje miernika, informujący o tym, jaka część dostępne zasoby są obecnie używane. Aby informacji na temat limitów-service dla indeksów, dokumentów i magazynu, zobacz [usługi limity](search-limits-quotas-capacity.md).

  ![Kafelek użycie][2]

> [!NOTE]
> Zrzut ekranu Hello powyżej dla bezpłatnej usługi hello, która może zawierać maksymalnie jedną replikę i każdej partycji i można indeksów hosta 3, 10 000 dokumentów lub 50 MB danych, zależnie od zostanie osiągnięty jako pierwszy. Usługi utworzonego w dniu warstwy Basic lub Standard mają znacznie większe ograniczenia usługi. Aby uzyskać więcej informacji o wyborze warstwy, zobacz [wybierz warstwę lub SKU](search-sku-tier.md).
>
>

### <a name="using-hello-rest-api"></a>Przy użyciu hello interfejsu API REST
Zarówno hello API REST usługi Azure Search i hello zestawu .NET SDK zapewniają dostęp programistyczny tooservice metryki.  Jeśli używasz [indeksatory](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload usługi indeksu usługi Azure SQL Database lub bazy danych rozwiązania Cosmos platformy Azure, interfejsu API jest wymagane numery hello tooget dostępne.

* [Uzyskać statystyki indeksu](/rest/api/searchservice/get-index-statistics)
* [Liczba dokumentów](/rest/api/searchservice/count-documents)
* [Pobierz stan indeksatora](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Sposób rejestrowania tooexport i metryki

Możesz wyeksportować hello dzienniki operacji usługi i hello pierwotnych danych dla metryki hello opisane w powyższej sekcji hello. Dzienniki operacji informacją o tym jak usługi hello jest używany i mogą być używane z usługi Power BI, gdy dane są kopiowane tooa konta magazynu. Usługa Azure search udostępnia monitorowania pakiet zawartości usługi Power BI w tym celu.


### <a name="enabling-monitoring"></a>Włączanie monitorowania
Otwórz usługi Azure Search w hello [portalu Azure](http://portal.azure.com) w obszarze hello opcji Włącz monitorowanie.

Wybierz dane hello ma tooexport: dzienniki, metryki lub oba. Można skopiować go tooa konta magazynu, przesyła Centrum zdarzeń tooan lub wyeksportować je tooLog Analytics.

![Jak tooenable monitorowania w portalu hello][3]

tooenable przy użyciu programu PowerShell lub hello wiersza polecenia platformy Azure, zobacz dokumentację hello [tutaj](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).

### <a name="logs-and-metrics-schemas"></a>Schematy dzienniki i metryki
Gdy danych hello jest skopiowany tooa magazynu konto, hello danych jest w formacie JSON i jego miejsce w dwóch kontenerów:

* insights — dzienniki operationlogs: dzienników ruchu wyszukiwania
* insights metryki pt1m: dla metryki

Brak obiektu blob na godzinę na kontenera.

Przykład ścieżki:`resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>Schemat dziennika
obiekty BLOB dzienniki Hello zawierają dzienniki ruchu usługi wyszukiwania.
Każdy obiekt blob ma jeden obiekt głównego o nazwie **rekordów** zawiera tablicę obiektów dziennika.
Każdy obiekt blob zawiera rekordy na wszystkich operacji hello, które miało miejsce podczas hello tę samą godzinę.

| Nazwa | Typ | Przykład | Uwagi |
| --- | --- | --- | --- |
| time |Data i godzina |"2015-12-07T00:00:43.6872559Z" |Sygnatura czasowa hello operacji |
| resourceId |Ciąg |"11111111-1111-1111-1111-111111111111/SUBSCRIPTIONS / /<br/>DOSTAWCÓW RESOURCEGROUPS/DOMYŚLNIE /<br/> FIRMY MICROSOFT. WYSZUKIWANIE/SEARCHSERVICES/SEARCHSERVICE" |Twoje ResourceId |
| operationName |Ciąg |"Query.Search" |Nazwa Hello hello operacji |
| operationVersion |Ciąg |"2015-02-28" |wersja interfejsu api Hello używane |
| category |Ciąg |"OperationLogs" |Stała |
| resultType |Ciąg |"Powodzenie" |Możliwe wartości: powodzenie lub niepowodzenie |
| resultSignature |int |200 |Kod wyniku protokołu HTTP |
| durationMS |int |50 |Czas trwania operacji hello w milisekundach |
| properties |Obiekt |Witaj w poniższej tabeli w temacie |Obiekt zawierający dane specyficzne dla operacji |

**Schemat właściwości**
| Nazwa | Typ | Przykład | Uwagi |
| --- | --- | --- | --- |
| Opis |Ciąg |"GET /indexes('content')/docs" |Operacja Hello punktu końcowego |
| Zapytanie |Ciąg |"? wyszukiwania = AzureSearch & $count = true & api-version = 2015-02-28" |Witaj parametrów zapytania |
| Dokumenty |int |42 |Liczba przetworzonych dokumentów |
| indexName |Ciąg |"testindex" |Nazwa indeksu hello skojarzonych z operacją hello |

#### <a name="metrics-schema"></a>Metryki schematu
| Nazwa | Typ | Przykład | Uwagi |
| --- | --- | --- | --- |
| resourceId |Ciąg |"11111111-1111-1111-1111-111111111111/SUBSCRIPTIONS / /<br/>DOSTAWCÓW RESOURCEGROUPS/DOMYŚLNIE /<br/>FIRMY MICROSOFT. WYSZUKIWANIE/SEARCHSERVICES/SEARCHSERVICE" |Identyfikator zasobu |
| metricName |Ciąg |"Opóźnienie" |Nazwa Hello hello metryki |
| time |Data i godzina |"2015-12-07T00:00:43.6872559Z" |Sygnatura czasowa Hello operacji |
| Średnia |int |64 |Średnia wartość próbek pierwotnych hello w przedziale czasu metryki hello Hello |
| Minimalna |int |37 |Minimalna wartość Hello hello pierwotnych próbek w przedziale czasu metryki hello |
| Maksymalna |int |78 |Maksymalna wartość Hello hello pierwotnych próbek w przedziale czasu metryki hello |
| Całkowita liczba |int |258 |Łączna wartość hello pierwotnych próbek w przedziale czasu metryki hello Hello |
| Liczba |int |4 |Metryka hello toogenerate używane Hello liczba próbek pierwotnych |
| ziarnem czasu |Ciąg |"PT1M" |Witaj ziarnem czasu metryki hello w ISO 8601 |

Wszystkie metryki są zgłaszane w odstępach jednej minuty. Każdy pomiar przedstawia minimalne, maksymalne i średnie wartości na minutę.

Metryki SearchQueriesPerSecond hello co najmniej jest najniższa wartość hello zapytań wyszukiwania na sekundę, który został zarejestrowany w ciągu tej minuty. Witaj dotyczy toohello wartość maksymalna. Średnia, to łączny hello przez hello całego minutę.
Pomyśl o tym scenariuszu w ciągu jednej minuty: jednej sekundzie wysokie obciążenie, który jest hello SearchQueriesPerSecond, wartość maksymalna, a następnie 58 sekund średniego i koniec jednej sekundy z tylko jednego zapytania, który jest hello minimalna.

Dla ThrottledSearchQueriesPercentage, minimalna, maksymalna, średni i sumy, wszystkie hello mają tę samą wartość: hello procent zapytania wyszukiwania, które zostały ograniczany z hello łączna liczba zapytań wyszukiwania w ciągu jednej minuty.

## <a name="analyzing-your-data-with-power-bi"></a>Analizowanie danych z usługi Power BI

Firma Microsoft zaleca używanie [usługi Power BI](https://powerbi.microsoft.com) tooexplore i wizualizować dane. Można łatwo łączyć go z tooyour konta magazynu Azure i szybko rozpocząć analizowanie danych.

Usługa Azure Search udostępnia [pakiet zawartości Power BI](https://app.powerbi.com/getdata/services/azure-search) pozwala toomonitor i zrozumienie ruchu wyszukiwania z wstępnie zdefiniowanych wykresów i tabel. Zawiera zestaw raportów usługi Power BI, które automatycznie połączyć tooyour danych i podaj visual informacjami na temat usługi wyszukiwania. Aby uzyskać więcej informacji, zobacz hello [strona pomocy pakietu zawartości](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).

![Power BI, odwiedź pulpit nawigacyjny usługi Azure Search][4]

## <a name="next-steps"></a>Następne kroki
Przegląd [skalowania repliki i partycje](search-limits-quotas-capacity.md) wskazówki dotyczące sposobu toobalance hello alokacji partycji i replik dla istniejącej usługi.

Odwiedź stronę [Zarządzanie usługą wyszukiwania w systemie Microsoft Azure](search-manage.md) uzyskać więcej informacji dotyczących administracji usługi lub [wydajności i optymalizacji](search-performance-optimization.md) dostrojenia wskazówki.

Dowiedz się więcej na temat tworzenia wspaniałych raportów. Zobacz [wprowadzenie Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/) Aby uzyskać więcej informacji

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
