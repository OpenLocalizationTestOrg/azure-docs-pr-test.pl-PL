---
title: "Użycie danych aaaAnalyze Log Analytics | Dokumentacja firmy Microsoft"
description: "Pulpit nawigacyjny użycia hello w tooview analizy dzienników, jak dużo danych jest wysyłana toohello usługi Log Analytics i rozwiązywanie problemów z powodu dużej ilości danych są wysyłane."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 74d0adcb-4dc2-425e-8b62-c65537cef270
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: magoedte
ms.openlocfilehash: c30373dd6edbe3ff900fbebc865575fee61ce14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-data-usage-in-log-analytics"></a>Analizowanie użycia danych w usłudze Log Analytics
Analiza dzienników informacje na temat hello ilość zebrane dane, które komputery wysyłane dane hello i hello różnych typów danych przesyłanych.  Użyj hello **dziennika analizy użycia** usługi analizy dzienników toohello wysyłane pulpitu nawigacyjnego toosee hello ilości danych. pulpit nawigacyjny Hello przedstawia ilość danych zbieranych przez każdego z rozwiązań i ilość danych komputerów wysyłania.

## <a name="understand-hello-usage-dashboard"></a>Zrozumienie hello nawigacyjnym użycia
Witaj **analizy dzienników użycia** pulpitu nawigacyjnego przedstawia hello następujących informacji:

- Ilość danych
    - Ilość danych w czasie (na podstawie bieżącego zakresu czasu)
    - Ilość danych wg rozwiązania
    - Dane nieskojarzone z komputerem
- Komputery
    - Komputery wysyłające dane
    - Komputery bez danych w ostatnich 24 godzinach
- Oferty
    - Węzły wglądu w dane i analizy
    - Węzły automatyzacji i kontroli
    - Węzły zabezpieczeń
- Wydajność
    - Czas poświęcony na dane toocollect i indeks
- Lista zapytań

![pulpit nawigacyjny Użycie](./media/log-analytics-usage/usage-dashboard01.png)

### <a name="toowork-with-usage-data"></a>toowork z danych użycia
1. Jeśli jeszcze tego nie zrobiono, zaloguj się w toohello [portalu Azure](https://portal.azure.com) przy użyciu subskrypcji platformy Azure.
2. Na powitania **Centrum** menu, kliknij przycisk **więcej usług** i hello listy zasobów, wpisz **analizy dzienników**. Po rozpoczęciu wpisywania, hello listy filtry oparte na dane wejściowe. Kliknij pozycję **Log Analytics**.  
    ![Centrum platformy Azure](./media/log-analytics-usage/hub.png)
3. Witaj **analizy dzienników** pulpit nawigacyjny zawiera listę obszarów roboczych. Wybierz obszar roboczy.
4. W hello *obszaru roboczego* pulpitu nawigacyjnego, kliknij przycisk **analizy dzienników użycia**.
5. Na powitania **dziennika analizy użycia** pulpitu nawigacyjnego, kliknij przycisk **czasu: ostatnich 24 godzin** toochange hello interwału.  
    ![przedział czasu](./media/log-analytics-usage/time.png)
6. Widok hello użycia kategorii bloków, które Pokaż obszary Cię interesują. Wybierz blok, a następnie kliknij element w nim tooview więcej szczegółów w [wyszukiwania dziennika](log-analytics-log-searches.md).  
    ![przykładowy blok użycia danych](./media/log-analytics-usage/blade.png)
7. Na pulpicie nawigacyjnym wyszukiwania dziennika hello Przejrzyj hello wyniki zwrócone z hello wyszukiwania.  
    ![przykład wyszukiwania w dzienniku użycia](./media/log-analytics-usage/usage-log-search.png)

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Tworzenie alertu, gdy ilość zebranych danych jest większa od oczekiwanej
W tej sekcji opisano sposób toocreate alert, jeśli:
- Ilość danych przekracza określoną wartość.
- Ilość danych jest przewidywane tooexceed określonej wartości.

[Alerty](log-analytics-alerts-creating.md) usługi Log Analytics używają zapytań wyszukiwania. Witaj następujące zapytanie ma wynik po więcej niż 100 GB danych zebranych w hello ostatnich 24 godzinach:

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`

Witaj następujące zapytanie używa prostego toopredict formuły podczas więcej niż 100 GB danych, które zostaną wysłane w dniu: 

`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`

tooalert w woluminie danych różnych, zmień hello 100 hello zapytania toohello liczbę GB ma tooalert na.

Użyj hello procedury opisanej w [Tworzenie reguły alertu](log-analytics-alerts-creating.md#create-an-alert-rule) toobe powiadomienie, gdy funkcja zbierania danych jest większa niż oczekiwano.

Podczas tworzenia hello alert dla pierwszego zapytania hello — Jeśli istnieje więcej niż 100 GB danych w ciągu 24 godzin, skonfigurować:
- **Nazwa** zbyt*ilość danych jest większa niż 100 GB w ciągu 24 godzin*
- **Ważność** zbyt*ostrzeżenie*
- **Zapytania wyszukiwania** zbyt`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(Quantity,1024)) as DataGB by Type | where DataGB > 100`
- **Przedział czasu** za*24 godziny*.
- **Alert częstotliwości** toobe jedną godzinę, ponieważ dane użycia hello aktualizację tylko raz na godzinę.
- **Generuj alert, na podstawie** toobe *liczba wyników*
- **Liczba wyników** toobe *większa niż 0*

Użyj hello procedury opisanej w [dodać reguły tooalert akcje](log-analytics-alerts-actions.md) konfigurowanie poczty e-mail, webhook lub runbook akcji hello reguły alertów.

Podczas tworzenia alertu powitania dla drugiego zapytania hello — jest przewidzieć, że będzie więcej niż 100 GB danych w ciągu 24 godzin, ustawić:
- **Nazwa** zbyt*ilość danych oczekiwano toogreater niż 100 GB w ciągu 24 godzin*
- **Ważność** zbyt*ostrzeżenie*
- **Zapytania wyszukiwania** zbyt`Type=Usage QuantityUnit=MBytes IsBillable=true | measure sum(div(mul(Quantity,8),1024)) as EstimatedGB by Type | where EstimatedGB > 100`
- **Przedział czasu** za*3 godziny*.
- **Alert częstotliwości** toobe jedną godzinę, ponieważ dane użycia hello aktualizację tylko raz na godzinę.
- **Generuj alert, na podstawie** toobe *liczba wyników*
- **Liczba wyników** toobe *większa niż 0*

Po otrzymaniu alertu hello kroki należy wykonać w powitania po tootroubleshoot sekcji Dlaczego użycia jest większa niż oczekiwano.

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Rozwiązywanie problemów związanych z użyciem przekraczającym oczekiwania
Witaj użycia pulpit nawigacyjny pomaga tooidentify Dlaczego użycia (i w związku z tym koszt) jest większa niż oczekiwana.

Większe użycie jest spowodowane przez jedną lub obie z następujących przyczyn:
- Więcej danych niż oczekiwano wysyłane tooLog analityka
- Więcej węzłów niż oczekiwano wysyłania danych tooLog Analytics

### <a name="check-if-there-is-more-data-than-expected"></a>Sprawdzanie, czy ilość danych przekracza oczekiwania 
Istnieją dwie sekcje klucza strony użycia hello ułatwiające rozpoznanie, co jest przyczyną hello większości toobe dane zbierane.

Witaj *ilość danych w czasie* wykres przedstawia łączną ilość danych przesyłanych hello i komputerach hello wysyłania hello większość danych. Wykres Hello u góry hello umożliwia toosee Jeśli rośnie użycie ogólne dane pozostały stałej lub malejącej. Witaj Lista komputerów przedstawia komputery hello 10 wysyłania hello większość danych.

Witaj *ilość danych wg rozwiązania* wykres pokazuje hello ilość danych przesyłanych przez każdego rozwiązania i rozwiązań hello wysyłania hello większość danych. Wykres Hello u góry hello pokazuje hello łączną ilość danych przesyłanych przez każde rozwiązanie w czasie. Te informacje można tooidentify czy rozwiązania wysyła więcej danych dotyczących hello sama ilość danych, albo mniejsza ilość danych w czasie. Lista Hello rozwiązania zawiera rozwiązania hello 10 wysyłania hello większość danych. 

Na tych dwóch wykresach są pokazywane wszystkie dane. Niektóre dane podlegają opłatom, a inne nie. toofocus tylko na takim rozliczeniowy danych zmodyfikować zapytanie hello na powitania wyszukiwania strony tooinclude `IsBillable=true`.  

![wykresy woluminów danych](./media/log-analytics-usage/log-analytics-usage-data-volume.png)

Przyjrzyj się hello *ilość danych w czasie* wykresu. toosee hello rozwiązania i typy danych, które wysyłają hello większość danych dla określonego komputera, kliknij nazwę hello hello komputera. Kliknij nazwę hello hello pierwszy komputer w hello listy.

W hello następującego zrzutu ekranu, hello *zarządzanie dziennikiem / wydajności* — typ danych wysyła hello większość danych hello komputera. 

![wolumin danych na komputerze](./media/log-analytics-usage/log-analytics-usage-data-volume-computer.png)

Następnie wróć toohello *użycia* pulpitu nawigacyjnego i Przeglądaj hello *ilość danych wg rozwiązania* wykresu. komputery hello toosee wysyłania hello większość danych dotyczących rozwiązania, kliknij nazwę hello rozwiązania hello hello na liście. Kliknij nazwę hello hello pierwsze rozwiązanie hello liście. 

W hello następującego zrzutu ekranu, potwierdza to, że hello *acmetomcat* komputer wysyła hello większość danych rozwiązania do zarządzania dziennika hello.

![wolumin danych dla rozwiązania](./media/log-analytics-usage/log-analytics-usage-data-volume-solution.png)

W razie potrzeby wykonaj dodatkowe analizy tooidentify dużych woluminów w rozwiązaniu lub typu danych. Przykładowe zapytania:

+ Rozwiązanie **zabezpieczające**
  - `Type=SecurityEvent | measure count() by EventID`
+ Rozwiązanie do **zarządzania dziennikami**
  - `Type=Usage Solution=LogManagement IsBillable=true | measure count() by DataType`
+ Typ danych **Perf**
  - `Type=Perf | measure count() by CounterPath`
  - `Type=Perf | measure count() by CounterName`
+ Typ danych **Event**
  - `Type=Event | measure count() by EventID`
  - `Type=Event | measure count() by EventLog, EventLevelName`
+ Typ danych **Syslog**
  - `Type=Syslog | measure count() by Facility, SeverityLevel`
  - `Type=Syslog | measure count() by ProcessName`
+ Typ danych **AzureDiagnostics**
  - `Type=AzureDiagnostics | measure count() by ResourceProvider, ResourceId`

Zbierane hello Użyj następującego kroki tooreduce hello woluminu dzienników:

| Źródło dużego woluminu danych | Jak tooreduce ilość danych |
| -------------------------- | ------------------------- |
| Zdarzenia zabezpieczeń            | Wybierz [pospolite lub minimalne zdarzenia zabezpieczeń](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/). <br> Zmień zdarzenia toocollect wymagane tylko zasad inspekcji zabezpieczeń hello. W szczególności Przejrzyj hello potrzeby toocollect zdarzenia dla <br> - [inspekcja platformy filtrowania](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [inspekcja rejestru](https://docs.microsoft.com/windows/device-security/auditing/audit-registry)<br> - [inspekcja systemu plików](https://docs.microsoft.com/windows/device-security/auditing/audit-file-system)<br> - [inspekcja obiektu jądra](https://docs.microsoft.com/windows/device-security/auditing/audit-kernel-object)<br> - [inspekcja manipulowania dojściem](https://docs.microsoft.com/windows/device-security/auditing/audit-handle-manipulation)<br> - [inspekcja magazynu wymiennego](https://docs.microsoft.com/windows/device-security/auditing/audit-removable-storage) |
| Liczniki wydajności       | Zmień [konfigurację licznika wydajności](log-analytics-data-sources-performance-counters.md) w następujący sposób: <br> -Zmniejszyć częstotliwość hello kolekcji <br> — Zmniejsz liczbę liczników wydajności |
| Dzienniki zdarzeń                 | Zmień [konfigurację dziennika zdarzeń](log-analytics-data-sources-windows-events.md) w następujący sposób: <br> — Ogranicz liczbę hello dzienników zdarzeń zbierane <br> — Zbieraj wyłącznie zdarzenia o wymaganym poziomie. Na przykład nie zbieraj zdarzeń na poziomie *Informacje*. |
| Dziennik systemu                     | Zmień [konfigurację dziennika systemu](log-analytics-data-sources-syslog.md) w następujący sposób: <br> -Zmniejsz hello liczbę urządzeń, zebranych <br> — Zbieraj wyłącznie zdarzenia o wymaganym poziomie. Na przykład nie zbieraj zdarzeń na poziomie *Informacje* i *Debugowanie*. |
| AzureDiagnostics           | Zmień kolekcję dziennika zasobów, aby: <br> -Zmniejsz liczbę hello zasobów wysyłania dzienników tooLog analityka <br> — zbierać tylko wymagane dzienniki. |
| Rozwiązanie danych z komputerów, które nie wymagają hello rozwiązania | Użyj [przeznaczonych dla rozwiązania](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect danych z tylko wymaganych grup komputerów. |

### <a name="check-if-there-are-more-nodes-than-expected"></a>Sprawdzanie, czy liczba węzłów przekracza oczekiwania
Jeśli jesteś na powitania *na węzeł (OMS)* cenowym, a następnie są naliczane na podstawie hello liczby węzłów i rozwiązania, można użyć. Widać liczbę węzłów każdej oferty są używane w hello *ofert* części pulpitu nawigacyjnego użycia hello.

![pulpit nawigacyjny Użycie](./media/log-analytics-usage/log-analytics-usage-offerings.png)

Polecenie **zobaczyć wszystkie...**  tooview hello pełną listę komputerów, wysyłanie danych do wybranej oferty hello.

Użyj [przeznaczonych dla rozwiązania](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect danych z tylko wymaganych grup komputerów.


## <a name="next-steps"></a>Następne kroki
* Zobacz [Zaloguj wyszukiwania analizy dzienników](log-analytics-log-searches.md) toolearn jak toouse hello wyszukiwania języka. Analizy dodatkowe tooperform zapytań wyszukiwania można użyć na powitania użycia danych.
* Użyj hello procedury opisanej w [Tworzenie reguły alertu](log-analytics-alerts-creating.md#create-an-alert-rule) spełnić toobe powiadomienie, gdy kryteria wyszukiwania
* Użyj [przeznaczonych dla rozwiązania](../operations-management-suite/operations-management-suite-solution-targeting.md) toocollect danych z tylko wymaganych grup komputerów
* Wybierz [pospolite lub minimalne zdarzenia zabezpieczeń](https://blogs.technet.microsoft.com/msoms/2016/11/08/filter-the-security-events-the-oms-security-collects/).
* Zmień [konfigurację licznika wydajności](log-analytics-data-sources-performance-counters.md)
* Zmień [konfigurację dziennika zdarzeń](log-analytics-data-sources-windows-events.md)
* Zmień [konfigurację dziennika systemu](log-analytics-data-sources-syslog.md)
