---
title: aaaUse analityka magazynu Azure toocollect dzienniki i metryki danych | Dokumentacja firmy Microsoft
description: "Analityka magazynu umożliwia tootrack danych metryki dla wszystkich usług magazynu i toocollect dzienniki dla magazynu obiektów Blob, kolejki i tabeli."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7894993b-ca42-4125-8f17-8f6dfe3dca76
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: aba1a236cb69fa2e60bcb8fda5d34841e36e379a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="storage-analytics"></a>Analityka magazynu

Analityka usługi Azure Storage umożliwia rejestrowanie i dostarcza danych metrycznych dotyczących konta magazynu. Można użyć tego żądania tootrace danych, analizować trendy użycia i diagnozowanie problemów z kontem magazynu.

toouse analityka magazynu, należy ją włączyć osobno dla każdej usługi ma toomonitor. Możesz je włączyć z hello [Azure Portal](https://portal.azure.com). Aby uzyskać więcej informacji, zobacz [monitorować konta magazynu w portalu Azure hello](storage-monitor-storage-account.md). Można również włączyć analityka magazynu programowo przy użyciu interfejsu API REST hello lub powitania klienta biblioteki. Użyj hello [pobrać właściwości usługi Blob](https://msdn.microsoft.com/library/hh452239.aspx), [pobrać właściwości usługi kolejki](https://msdn.microsoft.com/library/hh452243.aspx), [pobrać właściwości usługi tabeli](https://msdn.microsoft.com/library/hh452238.aspx), i [pobrać właściwości usługi plików](https://msdn.microsoft.com/library/mt427369.aspx) tooenable operacji analityka magazynu dla każdej usługi.

Hello zagregowane dane są przechowywane w dobrze znany obiekt blob (w przypadku rejestrowania) i dobrze znanego tabele (dla metryki), które mogą uzyskać dostęp za pomocą usługi Blob hello i tabeli interfejsów API.

Analityka magazynu ma limit 20 TB na powitania ilość przechowywanych danych, która jest niezależna od hello całkowitego limitu konta magazynu. Aby uzyskać więcej informacji dotyczących rozliczeń i zasad przechowywania danych, zobacz [analizy magazynu i rozliczeń](https://msdn.microsoft.com/library/hh360997.aspx). Aby uzyskać więcej informacji na temat limitów konta magazynu, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md).

Szczegółowy przewodnik przy użyciu analizy magazynu i inne narzędzia tooidentify, diagnozowanie i rozwiązywanie problemów związanych z usługą Azure Storage, zobacz [monitorowanie, diagnozowanie i rozwiązywanie problemów z usługi Magazyn Microsoft Azure](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="about-storage-analytics-logging"></a>Temat rejestrowania analityka magazynu
Analityka magazynu rejestruje szczegółowe informacje na temat usługi Magazyn tooa udane i nieudane żądania. Te informacje mogą być używane toomonitor poszczególnych żądań i toodiagnose problemy z usługą magazynu. Żądania są rejestrowane w sposób optymalny.

Wpisy dziennika są tworzone tylko w przypadku działania usługi magazynu. Na przykład jeśli konto magazynu ma działania, jego usługa Blob, ale nie w jej tabel lub kolejek usługi, zostanie utworzone tylko dzienniki dotyczące toohello usługi Blob.

Rejestrowanie analityka magazynu jest niedostępna dla usługi Magazyn plików Azure.

### <a name="logging-authenticated-requests"></a>Rejestrowanie uwierzytelnić żądania
rejestrowane są następujące typy żądań uwierzytelnionych Hello:

* Liczba pomyślnych żądań.
* Nieudane żądania, w tym limitu czasu, ograniczania przepustowości sieci, autoryzacji i inne błędy.
* Żądania przy użyciu dostępu sygnatury dostępu Współdzielonego, włącznie z żądaniami nie powiodło się i powiodło się.
* Dane tooanalytics żądań.

Żądania wysyłane przez analityka magazynu, takich jak dziennika utworzeniu lub usunięciu, nie są rejestrowane. Pełną listę hello zarejestrowane dane są udokumentowane WE hello [operacje rejestrowane analityka magazynu i komunikaty o stanie](https://msdn.microsoft.com/library/hh343260.aspx) i [Format dziennika analityka magazynu](https://msdn.microsoft.com/library/hh343259.aspx) tematów.

### <a name="logging-anonymous-requests"></a>Rejestrowanie żądań anonimowych
rejestrowane są następujące typy żądań anonimowych Hello:

* Liczba pomyślnych żądań.
* Błąd serwera.
* Błędy przekroczenia limitu czasu dla klienta i serwera.
* Nieudane żądania GET z kodem błędu 304 (nie jest modyfikowany).

Inne nieudanych żądań anonimowych nie są rejestrowane. Pełną listę hello zarejestrowane dane są udokumentowane WE hello [operacje rejestrowane analityka magazynu i komunikaty o stanie](https://msdn.microsoft.com/library/hh343260.aspx) i [Format dziennika analityka magazynu](https://msdn.microsoft.com/library/hh343259.aspx) tematów.

### <a name="how-logs-are-stored"></a>Jak są przechowywane dzienniki
Wszystkie dzienniki są przechowywane w blokowych obiektów blob w kontenerze o nazwie $logs, który jest tworzony automatycznie podczas analityka magazynu jest włączona dla konta magazynu. kontener Hello $logs znajduje się w przestrzeni nazw obiektu blob hello hello konta magazynu, na przykład: `http://<accountname>.blob.core.windows.net/$logs`. Ten kontener nie można usunąć po włączeniu analityka magazynu, jeśli jego zawartość można usunąć.

> [!NOTE]
> kontener Hello $logs nie jest wyświetlane, gdy jest wykonywana kontener listę operacji, takich jak hello [ListContainers](https://msdn.microsoft.com/library/azure/dd179352.aspx) metody. Muszą być dostępne bezpośrednio. Na przykład można użyć hello [ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx) obiekty BLOB hello tooaccess metody w hello `$logs` kontenera.
> Jak żądania są rejestrowane, analityka magazynu przekazać wyników pośrednich jako bloki. Okresowo analityka magazynu zatwierdzić te bloki i udostępnić je jako obiektu blob.
> 
> 

Dla dzienników utworzone w hello może istnieją zduplikowane rekordy tę samą godzinę. Można określić, czy rekord jest duplikatem sprawdzając hello **RequestId** i **operacji** numer.

### <a name="log-naming-conventions"></a>Zaloguj się konwencje nazewnictwa
Każdy dziennika zostanie zapisany w hello zgodny z formatem.

    <service-name>/YYYY/MM/DD/hhmm/<counter>.log

Witaj poniższej tabeli opisano każdego atrybutu w parametrze hello nazwę dziennika.

| Atrybut | Opis |
| --- | --- |
| < nazwa usługi > |Nazwa Hello hello usługi magazynu. Na przykład: obiektów blob, tabel lub kolejek. |
| RRRR |Witaj czterocyfrowy rok hello dziennika. Na przykład: 2011. |
| MM |miesiąc dwucyfrowe Hello hello dziennika. Na przykład: 07. |
| DD |miesiąc dwucyfrowe Hello hello dziennika. Na przykład: 07. |
| hh |rejestruje godzinę dwucyfrowe Hello wskazuje hello począwszy od godziny dla hello w formacie 24-godzinnym formacie UTC. Na przykład: 18. |
| mm |Liczba dwucyfrowe Hello wskazuje hello uruchamianie minutę hello dzienników. Ta wartość nie jest obsługiwana w bieżącej wersji hello analizy magazynu, a jego wartość zawsze będzie 00. |
| <counter> |Liczony od zera licznik z sześciu cyfr wskazującą hello liczbę obiektów blob dziennika wygenerowany dla usługi magazynowania hello godziny przedziale czasu. Ten licznik rozpoczyna się od 000000. Na przykład: 000001. |

Witaj poniżej znajduje się nazwa dziennika kompletnego przykładu, łączącą hello poprzednich przykładach.

    blob/2011/07/31/1800/000001.log

Hello poniżej przedstawiono przykładowy identyfikator URI, który może być używane tooaccess hello poprzednim dzienniku.

    https://<accountname>.blob.core.windows.net/$logs/blob/2011/07/31/1800/000001.log

Podczas rejestrowania żądania magazynu hello wynikowa nazwa dziennika są powiązane z toohello godzinę, kiedy hello Żądana operacja została zakończona. Na przykład, jeśli żądanie GetBlob zostało ukończone w 6:00. na 2011-7-31 hello dziennika będzie zapisany z hello prefiksie:`blob/2011/07/31/1800/`

### <a name="log-metadata"></a>Metadane dziennika
Wszystkie obiekty BLOB dziennika są przechowywane metadane, które mogą być używane tooidentify zawiera jakie blob hello danych rejestrowania. Witaj w poniższej tabeli opisano każdego atrybutu metadanych.

| Atrybut | Opis |
| --- | --- |
| LogType |Opisuje, czy hello dziennik zawiera informacje dotyczące tooread, zapisu lub operacje usuwania. Ta wartość może zawierać jeden typ lub kombinację wszystkich trzech rozdzielonych przecinkami. Przykład 1: zapisu; Przykład 2: Odczyt, zapis; Przykład 3: Odczyt, zapis, Usuń. |
| Czas rozpoczęcia |Witaj Najwcześniejsza godzina wpisu w dzienniku hello w formie hello RRRR-MM-Ddtgg. Na przykład: 2011-07-31T18:21:46Z. |
| wartość endTime |Witaj Najpóźniejsza godzina wpisu w dzienniku hello w formie hello RRRR-MM-Ddtgg. Na przykład: 2011-07-31T18:22:09Z. |
| LogVersion |Wersja Hello hello format dziennika. Wartość hello tylko obsługiwane jest obecnie 1.0. |

Witaj Poniższa lista zawiera kompletnego przykładu metadanych za pomocą hello poprzednich przykładach.

* LogType = zapisu
* Wartość StartTime = 2011-07-31T18:21:46Z
* Wartość EndTime = 2011-07-31T18:22:09Z
* LogVersion = 1.0

### <a name="accessing-logging-data"></a>Uzyskiwanie dostępu do danych rejestrowania
Wszystkie dane w hello `$logs` kontenera jest możliwy za pomocą interfejsów API usług obiektów Blob hello, tym hello .NET interfejsów API dostarczonych przez hello Azure biblioteki zarządzanej. administratorem konta magazynu Hello można odczytywać i Usuń dzienniki, ale nie można utworzyć lub zaktualizować je. Metadane hello dziennika i nazwa dziennika można podczas badania dziennika. Istnieje możliwość tooappear dzienniki danego godzinę poza kolejnością, ale metadane hello zawsze określa timespan hello wpisów dziennika w dzienniku. W związku z tym można użyć kombinacji nazwy dzienników i metadanych podczas wyszukiwania dla określonego dziennika.

## <a name="about-storage-analytics-metrics"></a>O metryki analityka magazynu
Analityka magazynu można przechowywać metryki, które zawierają zagregowane transakcji statystyk i pojemności dane dotyczące usługi Magazyn tooa żądań. Transakcje są raportowane zarówno na poziomie operacji hello interfejsu API, a także na poziomie usługi magazynu hello i pojemności jest zgłaszany na poziomie usługi hello magazynu. Dane metryk można wykorzystania usługi magazynu używanych tooanalyze, diagnozowanie problemów z żądania wysyłane przed hello usługi magazynu i tooimprove hello wydajności aplikacji korzystających z usługi.

toouse analityka magazynu, należy ją włączyć osobno dla każdej usługi ma toomonitor. Możesz je włączyć z hello [Azure Portal](https://portal.azure.com). Aby uzyskać więcej informacji, zobacz [monitorować konta magazynu w portalu Azure hello](storage-monitor-storage-account.md). Można również włączyć analityka magazynu programowo przy użyciu interfejsu API REST hello lub powitania klienta biblioteki. Użyj hello **pobrać właściwości usługi** operacji tooenable analityka magazynu dla każdej usługi.

### <a name="transaction-metrics"></a>Metryki transakcji
Niezawodny zestaw danych jest rejestrowany w odstępach czasu godzinowe i minutowe dla każdej usługi magazynu i żądanej operacji interfejsu API, takich jak wejście/wyjście, dostępności, błędów i skategoryzowane wartości procentowe żądania. Można wyświetlić pełną listę szczegółów transakcji hello w hello [schemat tabeli metryki analityka magazynu](https://msdn.microsoft.com/library/hh343264.aspx) tematu.

Dane transakcji są rejestrowane na dwa poziomy — poziom usługi hello i hello interfejsu API operacji. Na poziomie usługi hello statystyki podsumowania wszystkie żądane operacje interfejsu API są zapisywane jednostkę tabeli tooa co godzinę, nawet jeśli żadne żądania nie wprowadzono toohello usługi. Na poziomie operacji hello interfejsu API statystyki są jednostki tooan zapisywane tylko, jeśli zażądano operacji hello w ciągu tej godziny.

Na przykład, jeśli wykonywane **GetBlob** operacji w usłudze obiektów Blob, metryki analityka magazynu będzie hello żądania logowania i uwzględnić go w hello zagregowane dane dla obu hello usługi obiektów Blob, a także hello **GetBlob** operacji. Jednak jeśli nie **GetBlob** operacji jest wymagane w ciągu godziny hello, jednostki nie zostaną zapisane toohello `$MetricsTransactionsBlob` dla tej operacji.

Metryki transakcji są rejestrowane dla żądań użytkowników i żądań wysyłanych przez analityka magazynu, samej siebie. Na przykład żądania przez analityka magazynu toowrite dzienniki i jednostek tabeli są rejestrowane. Aby uzyskać więcej informacji o sposobie te żądania są rozliczane, zobacz [analizy magazynu i rozliczeń](https://msdn.microsoft.com/library/hh360997.aspx).

### <a name="capacity-metrics"></a>Metryki pojemności
> [!NOTE]
> Obecnie metryki pojemności są dostępne tylko dla hello usługi Blob. Metryki wydajności dla hello tabeli kolejki usług i będzie dostępna w przyszłych wersjach analityka magazynu.
> 
> 

Dane wydajności są rejestrowane codziennie dla konta magazynu obiektów Blob usługi, a dwie jednostki tabeli są zapisywane. Jedną jednostkę zawiera dane statystyczne dotyczące danych użytkowników i hello innych zawiera dane statystyczne dotyczące hello `$logs` kontenera obiektów blob używane przez analityka magazynu. Witaj `$MetricsCapacityBlob` tabela zawiera hello następujące statystyki:

* **Pojemność**: hello ilość Magazyn używany przez usługę obiektu Blob konta magazynu hello, w bajtach.
* **ContainerCount**: hello liczbę kontenerów obiektów blob w usłudze obiektów Blob konta magazynu hello.
* **ObjectCount**: hello liczbę zatwierdzonej i niezatwierdzone bloku lub strony obiektów blob w usłudze obiektów Blob konta magazynu hello.

Aby uzyskać więcej informacji na temat hello metryki pojemności, zobacz [schemat tabeli metryki analityka magazynu](https://msdn.microsoft.com/library/hh343264.aspx).

### <a name="how-metrics-are-stored"></a>Jak są przechowywane metryk
Wszystkie dane metryki dla każdej z usług magazynu hello są przechowywane w trzy tabele zastrzeżone dla tej usługi: jedną tabelę dla informacji o transakcji, jedną tabelę dla informacji o transakcji minute i pojemności informacji z innej tabeli. Transakcji i minutowe transakcji zawiera dane żądań i odpowiedzi, a informacje o pojemności składa się z magazynu danych użycia. Metryki godzina, minuta metryki i pojemności konta magazynu obiektów Blob usługi są dostępne w tabelach, które są nazywane zgodnie z opisem w poniższej tabeli hello.

| Metryki poziomu | Nazwy tabel | Obsługiwane wersje |
| --- | --- | --- |
| Metryki co godzinę, lokalizacji głównej |$MetricsTransactionsBlob <br/>$MetricsTransactionsTable <br/> $MetricsTransactionsQueue |Wersje wcześniejsze too2013-08-15 tylko. Te nazwy nadal są obsługiwane, zaleca się przełączyć się toousing hello tabel wymienionych poniżej. |
| Metryki co godzinę, lokalizacji głównej |$MetricsHourPrimaryTransactionsBlob <br/>$MetricsHourPrimaryTransactionsTable <br/>$MetricsHourPrimaryTransactionsQueue |Wszystkie wersje, w tym 2013-08-15. |
| Minuta metryki, lokalizacji głównej |$MetricsMinutePrimaryTransactionsBlob <br/>$MetricsMinutePrimaryTransactionsTable <br/>$MetricsMinutePrimaryTransactionsQueue |Wszystkie wersje, w tym 2013-08-15. |
| Metryki co godzinę, dodatkowej lokalizacji |$MetricsHourSecondaryTransactionsBlob <br/>$MetricsHourSecondaryTransactionsTable <br/>$MetricsHourSecondaryTransactionsQueue |Wszystkie wersje, w tym 2013-08-15. Musi być włączona replikacja geograficznie nadmiarowa dostęp do odczytu. |
| Minuta metryki, dodatkowej lokalizacji |$MetricsMinuteSecondaryTransactionsBlob <br/>$MetricsMinuteSecondaryTransactionsTable <br/>$MetricsMinuteSecondaryTransactionsQueue |Wszystkie wersje, w tym 2013-08-15. Musi być włączona replikacja geograficznie nadmiarowa dostęp do odczytu. |
| Wydajność (tylko usługa Blob) |$MetricsCapacityBlob |Wszystkie wersje, w tym 2013-08-15. |

Te tabele są tworzone automatycznie, gdy analityka magazynu jest włączona dla konta magazynu. Są one używane za pośrednictwem przestrzeni nazw hello hello konta magazynu, na przykład:`https://<accountname>.table.core.windows.net/Tables("$MetricsTransactionsBlob")`

### <a name="accessing-metrics-data"></a>Uzyskiwanie dostępu do danych metryk
Wszystkie dane w tabelach metryki hello jest możliwy za pomocą interfejsów API usług tabeli hello, tym hello .NET interfejsów API dostarczonych przez hello Azure biblioteki zarządzanej. administratorem konta magazynu Hello można odczytać i usuwania jednostek tabeli, ale nie można utworzyć lub zaktualizować je.

## <a name="billing-for-storage-analytics"></a>Rozliczeń analiz magazynu
Wszystkie dane metryki są zapisywane przez usługi hello konta magazynu. W związku z tym każdej operacji zapisu, wykonywane przez analityka magazynu jest rozliczeniowy. Ponadto hello ilość Magazyn używany przez dane metryk jest również rozliczeniowy.

następujące akcje wykonywane przez analityka magazynu Hello są rozliczeniowy:

* Obiekty BLOB toocreate żądania logowania. 
* Żądania toocreate jednostek tabeli dla metryki.

Skonfigurowanie zasad przechowywania danych są nie naliczane dla transakcji delete podczas analizy magazynu usuwa stare dane rejestrowania i metryki. Usuń transakcji od klienta, są jednak rozliczeniowy. Aby uzyskać więcej informacji na temat zasad przechowywania, zobacz [ustawienie zasad przechowywania danych analizy magazynu](https://msdn.microsoft.com/library/azure/hh343263.aspx).

### <a name="understanding-billable-requests"></a>Opis rozliczeniowy żądań
Każde żądanie tooan konta usługi storage jest rozliczana lub niepodlegającego rozliczaniu. Magazynu analizy dzienników każdego żądania poszczególnych tooa usługi, w tym wskazującą obsługi żądania hello komunikat o stanie. Podobnie analityka magazynu przechowuje metryki dla operacji interfejsu API usługę i hello tej usługi, w tym wartości procentowe hello i liczba komunikatów stanu. Razem te funkcje ułatwiają analizowanie rozliczeniowy żądań, poprawiają w swojej aplikacji i diagnozowanie problemów z usługami tooyour żądań. Aby uzyskać więcej informacji dotyczących rozliczeń, zobacz [opis Azure magazynu rozliczeń - przepustowość, transakcje i pojemności](http://blogs.msdn.com/b/windowsazurestorage/archive/2010/07/09/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity.aspx).

Podczas przeglądania danych analizy magazynu, możesz użyć hello tabel w hello [operacje rejestrowane analityka magazynu i komunikaty o stanie](https://msdn.microsoft.com/library/azure/hh343260.aspx) toodetermine tematu co żądań są rozliczeniowy. Następnie można porównać z dzienników i metryki danych toohello stan wiadomości toosee, jeśli opłata za poszczególnych żądań. Umożliwia także hello tabel w hello poprzedniego tematu tooinvestigate dostępności usługi magazynu lub poszczególnych operacji interfejsu API.

## <a name="next-steps"></a>Następne kroki
### <a name="setting-up-storage-analytics"></a>Konfigurowanie magazynu analityka
* [Monitor konta magazynu w hello portalu Azure](storage-monitor-storage-account.md)
* [Włączanie i konfigurowanie analityka magazynu](https://msdn.microsoft.com/library/hh360996.aspx)

### <a name="storage-analytics-logging"></a>Rejestrowanie analityka magazynu
* [Temat rejestrowania analityka magazynu](https://msdn.microsoft.com/library/hh343262.aspx)
* [Format dziennika analityka magazynu](https://msdn.microsoft.com/library/hh343259.aspx)
* [Analityka magazynu rejestrowane operacje i komunikaty o stanie](https://msdn.microsoft.com/library/hh343260.aspx)

### <a name="storage-analytics-metrics"></a>Metryki analityka magazynu
* [O metryki analityka magazynu](https://msdn.microsoft.com/library/hh343258.aspx)
* [Schemat tabeli metryki analityka magazynu](https://msdn.microsoft.com/library/hh343264.aspx)
* [Analityka magazynu rejestrowane operacje i komunikaty o stanie](https://msdn.microsoft.com/library/hh343260.aspx)  

