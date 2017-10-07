---
title: dane aplikacji Azure Application Insights aaaView | Dokumentacja firmy Microsoft
description: "Można użyć hello Application Insights łącznika rozwiązania toodiagnose wydajności problemów i zrozumieć, co zrobić użytkownicy, z aplikacji podczas monitorowania z usługą Application Insights."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 49280cad-3526-43e1-a365-c6a3bf66db52
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: banders
ms.openlocfilehash: 38109337ebbc8970dccb65365ba8284d9cee19a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-connector-solution-preview-in-operations-management-suite-oms"></a>Rozwiązanie aplikacji łącznik usługi Insights (wersja zapoznawcza) w Operations Management Suite (OMS)

![Application Insights symbol](./media/log-analytics-app-insights-connector/app-insights-connector-symbol.png)

rozwiązanie łącznik usługi Insights aplikacji Hello ułatwia diagnozowanie problemów z wydajnością i zrozumieć, co zrobić użytkownicy z aplikacją, gdy jest monitorowany z [usługi Application Insights](../application-insights/app-insights-overview.md). Widoki programu hello są dostępne w OMS tego samego deweloperzy zobaczyć w usłudze Application Insights danych telemetrii w aplikacji. Jednak w przypadku aplikacji usługi Application Insights jest zintegrowane z usługą OMS, widoczność aplikacji zwiększa się o zebranie danych operacji i aplikacji w jednym miejscu. Mających takie same hello widoków pomaga toocollaborate z deweloperów w Twojej aplikacji. Widok typowych Hello może pomóc zmniejszyć toodetect czasu hello i rozwiązać zarówno aplikacji, jak i problemów platformy.

Korzystając z hello rozwiązania, można:

- Wyświetl wszystkie aplikacje usługi Application Insights w jednym miejscu, nawet wtedy, gdy znajdują się w różnych subskrypcji platformy Azure
- Skorelować danych infrastruktury z danych aplikacji
- Wizualizuj dane aplikacji z perspektywy wyszukiwania dziennika
- Przestawianie z portale Azure i aplikacji usługi Application Insights tooyour danych analizy dzienników w hello OMS

## <a name="connected-sources"></a>Połączone źródła

W przeciwieństwie do większości innych rozwiązań analizy dzienników nie jest zebranym dla hello Application Insights łącznika przez agentów. Wszystkie dane używane przez rozwiązanie hello pochodzi bezpośrednio z platformy Azure.

| Połączone źródło | Obsługiwane | Opis |
| --- | --- | --- |
| [Agenci dla systemu Windows](log-analytics-windows-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje z agentów systemu Windows. |
| [Agenci dla systemu Linux](log-analytics-linux-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje z agentów systemu Linux. |
| [Grupa zarządzania programu SCOM](log-analytics-om-agents.md) | Nie | rozwiązanie Hello nie zbiera informacje z agentów w podłączonej grupy zarządzania SCOM. |
| [Konto usługi Azure Storage](log-analytics-azure-storage.md) | Nie | rozwiązanie Hello nie nie zbierają informacje z usługi Azure storage. |

## <a name="prerequisites"></a>Wymagania wstępne

- tooaccess informacji Application Insights łącznik, musi mieć subskrypcję platformy Azure
- Musi mieć co najmniej jeden zasób usługi Application Insights skonfigurowany.
- Musi być hello właścicielem lub współautorem hello zasobu usługi Application Insights.

## <a name="configuration"></a>Konfiguracja

1. Włącz hello Azure Web Apps Analytics rozwiązania z hello [witrynę Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ApplicationInsights?tab=Overview) lub za pomocą hello procesu opisanego w temacie [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).
2. W portalu OMS hello, kliknij przycisk **ustawienia** &gt; **danych** &gt; **usługi Application Insights**.
3. W obszarze **Wybierz subskrypcję**, wybierz subskrypcję, która ma zasobów usługi Application Insights, a następnie w obszarze **Nazwa aplikacji**, wybierz co najmniej jednej aplikacji.
4. Kliknij pozycję **Zapisz**.

W ciągu 30 minut dane będą dostępne, i powitalne Kafelek usługi Application Insights został zaktualizowany o dane, takie jak powitania po obrazu:

![Kafelek usługi Application Insights](./media/log-analytics-app-insights-connector/app-insights-tile.png)

Inne punkty tookeep pamiętać:

- Można połączyć tylko roboczy OMS tooone aplikacje usługi Application Insights.
- Można połączyć tylko [Standard lub Premium Application Insights zasobów](https://azure.microsoft.com/pricing/details/application-insights) tooOMS analizy dzienników. Można jednak użyć hello warstwę bezpłatna analizy dziennika.

## <a name="management-packs"></a>Pakiety administracyjne

To rozwiązanie nie instalować żadnych pakietów administracyjnych w podłączonych grup zarządzania.

## <a name="use-hello-solution"></a>Użyj hello rozwiązania

Witaj poniższych sekcjach opisano sposób użycia bloków hello pokazano tooview pulpitu nawigacyjnego usługi Application Insights hello i interakcji z danymi z aplikacji.

### <a name="view-application-insights-connector-information"></a>Wyświetlanie informacji o aplikacji Insights łącznika

Kliknij przycisk hello **usługi Application Insights** hello tooopen kafelka **usługi Application Insights** hello toosee pulpitu nawigacyjnego po bloków.

![Pulpit nawigacyjny szczegółowych informacji w aplikacji](./media/log-analytics-app-insights-connector/app-insights-dash01.png)

![Pulpit nawigacyjny szczegółowych informacji w aplikacji](./media/log-analytics-app-insights-connector/app-insights-dash02.png)

pulpit nawigacyjny Hello zawiera bloki hello hello tabelą. Każdy blok wyświetla się too10 elementów pasujących do kryteriów w bloku hello określenia zakresu zakresu i czasu. Można uruchomić wyszukiwania dziennika, który zwraca wszystkie rekordy po kliknięciu **zobaczyć wszystkie** u dołu hello bloku hello lub po kliknięciu nagłówka bloku hello.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

| **Kolumny** | **Opis** |
| --- | --- |
| Aplikacje — liczba aplikacji | Pokazuje liczbę hello aplikacji w zasobów aplikacji. Również listy aplikacji nazwy i dla każdej, hello liczbę rekordów aplikacji. Kliknij przycisk toorun numer hello dziennik wyszukiwania<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by ApplicationName</code> <br><br>  Kliknij przycisk toorun nazwy aplikacji wyszukiwania dziennika aplikacji hello, która zawiera rekordy aplikacji według hosta, rekordów typu telemetrii i wszystkie dane według typu (na podstawie hello ostatni dzień). |
| Ilość danych — obsługuje wysyłanie danych | Pokazuje liczbę hello komputerów hostów, które wysyłają dane. Zawiera także listę hostów komputera i liczba rekordów dla każdego hosta. Kliknij przycisk toorun numer hello dziennik wyszukiwania<code>Type=ApplicationInsights &#124; measure sum(SampledCount) by Host</code> <br><br> Polecenie toorun nazwy komputera dziennika wyszukiwanie hello hosta, który zawiera rekordy aplikacji według hosta, rekordów typu telemetrii i wszystkie dane według typu (na podstawie hello ostatni dzień). |
| Dostępność — wyniki w teście sieci Web | Przedstawia wykres pierścieniowy dla wyników testu sieci web, wskazując pomyślnie lub niepowodzeniem. Kliknij przycisk wyszukiwania dziennika hello toorun wykresu<code>Type=ApplicationInsights TelemetryType=Availability &#124; measure sum(SampledCount) by AvailabilityResult</code> <br><br> Liczba hello błędy wszystkich testów i przebiegów w wynikach. Wszystkie aplikacje sieci Web z ruchem będzie wyświetlana dla hello ostatniej minuty. Kliknij przycisk tooview nazwy aplikacji wyszukiwania dziennika zawierającego szczegóły testów sieci web nie powiodło się. |
| Żądań serwera — żądań na godzinę | Przedstawia wykres liniowy w hello żądań serwera na godzinę dla różnych aplikacji. Umieść wskaźnik myszy linię w hello wykresu toosee hello 3 pierwszych aplikacji odbierania żądań do punktu w czasie. Zawiera także listę aplikacji hello odbieranie żądań i liczba żądań hello hello wybrany okres. <br><br>Kliknij toorun wykres hello dziennika wyszukiwanie <code>Type=ApplicationInsights TelemetryType=Request &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> który przedstawia bardziej szczegółowe wykres wiersza hello żądań serwera na godzinę dla różnych aplikacji. <br><br> Kliknij aplikację w toorun listy hello dziennika wyszukiwanie <code>Type=ApplicationInsights  ApplicationName=yourapplicationname  TelemetryType=Request</code> który pokazuje listę żądań, wykresy żądań w czasie trwania czasu i żądania i listę żądania kody odpowiedzi.   |
| Błędy — nieudane żądania na godzinę | Przedstawia wykres liniowy żądań aplikacji nie powiodło się na godzinę. Umieść kursor nad hello wykresu toosee hello pierwsze 3 aplikacji z żądań zakończonych niepowodzeniem dla punktu w czasie. Zawiera także listę aplikacji hello liczby żądań zakończonych niepowodzeniem dla każdego. Kliknij przycisk wyszukiwania dziennika toorun wykresu hello <code>Type=ApplicationInsights TelemetryType=Request  RequestSuccess = false &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> który przedstawiono bardziej szczegółowe wykres liniowy żądań aplikacji nie powiodło się. <br><br>Kliknij element toorun listy hello dziennika wyszukiwanie <code>Type=ApplicationInsights ApplicationName=yourapplicationname TelemetryType=Request  RequestSuccess=false</code> czy pokazuje nieudanych żądań, wykresy dla niepomyślnych żądań przez okres czasu i żądania i listę kodów odpowiedzi nieudanych żądań. |
| Wyjątki — wyjątków na godzinę | Przedstawia wykres liniowy wyjątków na godzinę. Umieść kursor nad hello wykresu toosee hello pierwsze 3 aplikacji wyjątków dla punktu w czasie. Przedstawiono również listę aplikacji za pomocą hello liczba wyjątków dla każdego. Kliknij przycisk wyszukiwania dziennika toorun wykresu hello <code>Type=ApplicationInsights TelemetryType=Exception &#124; measure sum(SampledCount) by ApplicationName interval 1hour</code> który przedstawiono bardziej szczegółowe wykres łącze wyjątków. <br><br>Kliknij element toorun listy hello dziennika wyszukiwanie <code>Type=ApplicationInsights  ApplicationName=yourapplicationname TelemetryType=Exception</code> którym wyświetlana jest lista wyjątków, wykresy dotyczące wyjątków w czasie, jak i nieudane żądania i listę typów wyjątków.  |

### <a name="view-hello-application-insights-perspective-with-log-search"></a>Witaj widoku perspektywy usługi Application Insights z dziennika wyszukiwania

Po kliknięciu dowolny element w pulpicie nawigacyjnym hello, zostanie wyświetlony perspektywy usługi Application Insights wyświetlany w obszarze wyszukiwania. perspektywy Hello udostępnia rozszerzone wizualizacji na podstawie typu danych telemetrycznych hello, wybrany. Tak, wizualizacji zmiany zawartości telemetrii różnych typów.

Gdy użytkownik kliknij w dowolnym miejscu w bloku aplikacji hello, zobacz domyślne hello **aplikacji** perspektywy.

![Perspektywa aplikacji Insights aplikacji](./media/log-analytics-app-insights-connector/applications-blade-drill-search.png)

Perspektywa Hello zawiera omówienie aplikacji hello, które wybrano.

Witaj **dostępności** bloku pokazuje widoku perspektywy różnych umożliwia wyświetlenie wyników testu sieci web i powiązane żądań zakończonych niepowodzeniem.

![Perspektywa Insights dostępność aplikacji](./media/log-analytics-app-insights-connector/availability-blade-drill-search.png)

Po kliknięciu dowolnej lokalizacji w hello **żądań serwera** lub **błędów** bloków, perspektywy hello składniki zmienić toogive możesz związany toorequests wizualizacji.

![Application Insights błędów bloku](./media/log-analytics-app-insights-connector/server-requests-failures-drill-search.png)

Po kliknięciu dowolnej lokalizacji w hello **wyjątki** bloku, zobacz wizualizacji dostosowane tooexceptions.

![Application Insights wyjątki bloku](./media/log-analytics-app-insights-connector/exceptions-blade-drill-search.png)

Niezależnie od tego, czy można kliknąć element jedną hello **Application Insights łącznik** pulpitu nawigacyjnego w hello **wyszukiwania** strony, każde zapytanie zwraca dane usługi Application Insights zawiera hello Application Insights perspektywy. Na przykład, jeśli można przeglądać dane usługi Application Insights **& #42;** zapytanie wyświetla również hello kartę perspektywy takich jak powitania po obrazu:

![Application Insights ](./media/log-analytics-app-insights-connector/app-insights-search.png)

Składniki perspektywy są aktualizowane w zależności od hello zapytania wyszukiwania. Oznacza to, że wyniki hello można filtrować przy użyciu każde pole wyszukiwania, które zapewnia hello toosee możliwości hello danych z:

- Wszystkie aplikacje
- Pojedynczy wybranej aplikacji
- Grupy aplikacji

### <a name="pivot-tooan-app-in-hello-azure-portal"></a>Przestawne tooan aplikacji w portalu Azure hello

Application Insights łącznika bloki są zaprojektowane tooenable toopivot toohello wybrane aplikacji usługi Application Insights *Jeśli używasz portalu OMS hello*. Za pomocą rozwiązania hello jako platforma wysokiego poziomu monitorowania, ułatwiające rozwiązywanie problemów z aplikacją. Po wyświetleniu potencjalny problem w żadnym z połączonych aplikacji, można albo Przechodzenie do szczegółów w nim OMS wyszukiwania lub można przestawiać bezpośrednio toohello aplikacji usługi Application Insights.

toopivot, kliknij wielokropek hello (**... **) pojawi się na końcu hello w każdym wierszu, a wybierz **Otwórz w usłudze Application Insights**.

>[!NOTE]
>**Otwórz w usłudze Application Insights** nie jest dostępna w hello portalu Azure.

![Otwórz w usłudze Application Insights](./media/log-analytics-app-insights-connector/open-in-app-insights.png)

### <a name="sample-corrected-data"></a>Poprawione próbki danych

Usługa Application Insights udostępnia * [próbkowania korekty](../application-insights/app-insights-sampling.md) * toohelp zmniejszenie ruchu w danych telemetrycznych. Po włączeniu próbkowania w aplikacji usługi Application Insights, możesz uzyskać zmniejszenie liczby wpisów przechowywanych zarówno w usłudze Application Insights i OMS. Gdy spójność danych jest zachowywana w hello **Application Insights łącznik** strony i perspektywy, należy ręcznie rozwiązać próbki danych dla zapytań niestandardowych.

Oto przykład korekty próbkowania w kwerendzie wyszukiwania dziennika:

```
Type=ApplicationInsights | measure sum(SampledCount) by TelemetryType
```

Witaj **próbkowany liczba** pole jest obecne w wszystkie wpisy i pokazuje hello liczbę punktów danych, które reprezentuje hello wpisu. Jeśli włączysz próbkowania dla aplikacji usługi Application Insights, **próbkowany liczba** jest większa niż 1. Rzeczywista liczba wpisów, które generuje aplikacji hello Suma hello toocount **próbkowany liczba** pola.

Próbkowanie dotyczy tylko hello całkowita liczba wpisów, które generuje aplikacji. Nie ma potrzeby toocorrect próbkowania dla pola metryk, takich jak **RequestDuration** lub **AvailabilityDuration** ponieważ te zawierają hello średnia dla reprezentowanego wpisów.

## <a name="input-data"></a>Dane wejściowe

rozwiązanie Hello otrzymuje hello poniższych typów danych telemetrycznych z połączonych aplikacji usługi Application Insights:

- Dostępność
- Wyjątki
- Żądania
- Wyświetlenia strony wyświetleń strony — dla Twojego tooreceive obszaru roboczego, należy skonfigurować Twoje aplikacje toocollect tych informacji. Aby uzyskać więcej informacji, zobacz [PageViews](../application-insights/app-insights-api-custom-events-metrics.md#page-views).
- Niestandardowe zdarzenia — zdarzenia niestandardowe tooreceive obszaru roboczego, należy skonfigurować Twoje aplikacje toocollect tych informacji. Aby uzyskać więcej informacji, zobacz [TrackEvent](../application-insights/app-insights-api-custom-events-metrics.md#trackevent).

Danych jest odbierany przez OMS z usługi Application Insights po jej udostępnieniu.

## <a name="output-data"></a>dane wyjściowe

Rekord z *typu* z *ApplicationInsights* jest tworzony dla każdego typu danych wejściowych. Rejestruje ApplicationInsights mają właściwości wyświetlane hello następujące sekcje:

### <a name="generic-fields"></a>Ogólny pól

| Właściwość | Opis |
| --- | --- |
| Typ | ApplicationInsights |
| ClientIP |   |
| TimeGenerated | Czas hello rekordu |
| Identyfikator aplikacji | Klucz Instrumentacji hello aplikacji usługi Application Insights |
| ApplicationName | Nazwa aplikacji usługi Application Insights hello |
| RoleInstance | Identyfikator serwera hosta |
| DeviceType | Urządzenia klienckiego |
| ScreenResolution |   |
| Kontynent | Kontynencie, skąd pochodzi żądanie hello |
| Kraj | Kraju, w której pochodzi żądanie hello |
| Województwo | Województwo, stanu lub ustawień regionalnych, których hello pochodzi żądanie |
| Miasto | Miasta lub miejscowości, w której pochodzi żądanie hello |
| isSynthetic | Wskazuje, czy Żądanie hello został utworzony przez użytkownika lub przez metodę automatycznego. = TRUE użytkownika wygenerowany lub = false zautomatyzowanych — metoda |
| SamplingRate | Wartość procentowa generowane przez hello zestawu SDK, który jest wysyłany tooportal telemetrii. Zakres niż 100,0 0,0. |
| SampledCount | 100/(SamplingRate). Na przykład, 4 =&gt; 25% |
| IsAuthenticated | Prawda lub fałsz |
| OperationID | Elementy, które mają tego samego Identyfikatora operacji są wyświetlane jako elementy powiązane w portalu hello hello. Zazwyczaj hello identyfikator żądania |
| ParentOperationID | Identyfikator działania nadrzędnego hello |
| OperationName |   |
| Identyfikator sesji | Identyfikator GUID toouniquely identyfikacji sesji hello, w którym utworzono Żądanie hello |
| SourceSystem | ApplicationInsights |

### <a name="availability-specific-fields"></a>Dostępność określonych pól

| Właściwość | Opis |
| --- | --- |
| TelemetryType | Dostępność |
| AvailabilityTestName | Nazwa testu sieci web hello |
| AvailabilityRunLocation | Geograficzne źródłowego żądania http |
| AvailabilityResult | Wskazuje wynik wskazujący Powodzenie hello hello testu sieci web |
| AvailabilityMessage | wiadomości powitania dołączony toohello testu sieci web |
| AvailabilityCount | 100 /(Sampling Rate). Na przykład, 4 =&gt; 25% |
| DataSizeMetricValue | w wersji 1.0 lub 0,0 |
| DataSizeMetricCount | 100 /(Sampling Rate). Na przykład, 4 =&gt; 25% |
| AvailabilityDuration | Czas w milisekundach czas trwania testu sieci web hello |
| AvailabilityDurationCount | 100 /(Sampling Rate). Na przykład, 4 =&gt; 25% |
| AvailabilityValue |   |
| AvailabilityMetricCount |   |
| AvailabilityTestId | Unikatowy identyfikator GUID dla hello testu sieci web |
| AvailabilityTimestamp | Dokładne sygnatura czasowa hello test dostępności |
| AvailabilityDurationMin | Próbki rekordów to pole zawiera hello web minimalny czas trwania testu (w milisekundach) dla punktów danych hello reprezentowane |
| AvailabilityDurationMax | Próbki rekordów to pole zawiera hello web maksymalny czas trwania testu (w milisekundach) dla punktów danych hello reprezentowane |
| AvailabilityDurationStdDev | Próbki rekordów to pole zawiera odchylenie standardowe powitania od wszystkich sieci web testu czasów trwania (w milisekundach) dla punktów danych hello reprezentowane |
| AvailabilityMin |   |
| AvailabilityMax |   |
| AvailabilityStdDev | &nbsp;  |

### <a name="exception-specific-fields"></a>Wyjątek określonych pól

| Typ | ApplicationInsights |
| --- | --- |
| TelemetryType | Wyjątek |
| ExceptionType | Typ wyjątku hello |
| ExceptionMethod | Metoda Hello, która tworzy wyjątek hello |
| ExceptionAssembly | Zestaw zawiera hello framework i wersji oraz hello token klucza publicznego |
| ExceptionGroup | Typ wyjątku hello |
| ExceptionHandledAt | Wskazuje poziom hello, obsługi wyjątków hello |
| ExceptionCount | 100 /(Sampling Rate). Na przykład, 4 =&gt; 25% |
| ExceptionMessage | Wiadomość hello wyjątku |
| ExceptionStack | Pełna stosu wyjątku hello |
| ExceptionHasStack | Wartość true, jeśli wyjątek ma stosu |



### <a name="request-specific-fields"></a>Pola specyficzne dla żądania

| Właściwość | Opis |
| --- | --- |
| Typ | ApplicationInsights |
| TelemetryType | Żądanie |
| ResponseCode | Tooclient wysłanych odpowiedzi HTTP |
| RequestSuccess | Wskazuje powodzenie lub niepowodzenie. Wartość PRAWDA lub FAŁSZ. |
| Identyfikator żądania | Identyfikator toouniquely zidentyfikować hello żądania |
| RequestName | GET/POST + baza adresów URL |
| RequestDuration | Czas w sekundach czas trwania żądania hello |
| ADRES URL | Adres URL żądania hello wyłączeniem hosta |
| Host | Hosta serwera sieci Web |
| URLBase | Pełny adres URL żądania hello |
| ApplicationProtocol | Typ protokołu używanego przez aplikację hello |
| RequestCount | 100 /(Sampling Rate). Na przykład, 4 =&gt; 25% |
| RequestDurationCount | 100 /(Sampling Rate). Na przykład, 4 =&gt; 25% |
| RequestDurationMin | Próbki rekordów w tym polu jest wyświetlana hello minimalny czas trwania żądania (w milisekundach) dla punktów danych hello reprezentowane. |
| RequestDurationMax | Próbki rekordów to pole zawiera hello maksymalny czas trwania żądania (w milisekundach) dla punktów danych hello reprezentowane |
| RequestDurationStdDev | Próbki rekordów to pole zawiera odchylenie standardowe hello między wszystkie żądania wartości czasu trwania (w milisekundach) dla punktów danych hello reprezentowane |

## <a name="sample-log-searches"></a>Przykładowe wyszukiwania dzienników

To rozwiązanie nie ma zestaw przykładowy dziennik wyszukiwania wyświetlane na pulpicie nawigacyjnym hello. Jednak w hello przedstawiono przykładowy dziennik wyszukiwania zapytania z opisami [informacji o widoku Application Insights łącznika](#view-application-insights-connector-information) sekcji.

## <a name="next-steps"></a>Następne kroki

- Użyj [wyszukiwania dziennika](log-analytics-log-searches.md) tooview szczegółowe informacje o aplikacjach Application Insights.
