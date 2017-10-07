---
title: "aaaTroubleshoot Azure Stream Analytics z dzienników diagnostycznych | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak diagnostyki tooanalyze dzienniki z usługi Stream Analytics zadań w systemie Microsoft Azure."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 600fce73636dd137f8f3a137f1d77b59b4a88801
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-stream-analytics-by-using-diagnostics-logs"></a>Rozwiązywanie problemów z usługą Azure Stream Analytics przy użyciu dzienników diagnostycznych

Czasami zadanie usługi analiza strumienia Azure nieoczekiwanie zatrzymuje przetwarzanie. Jest ważne toobe stanie tootroubleshoot tego rodzaju zdarzenia. Witaj zdarzeń może być spowodowany przez wynik nieoczekiwane zapytanie, toodevices łączności lub awaria usługi nieoczekiwany. Hello dzienników diagnostyki w Stream Analytics ułatwia określenie hello przyczyny problemów, jeśli występują i skrócić czas odzyskiwania.

## <a name="log-types"></a>Typy dziennika

Analiza strumienia oferuje dwa typy dzienników: 
* [Dzienniki aktywności](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) (zawsze włączona). Dzienniki aktywności zapewniają wgląd w operacji wykonywanych zadań.
* [Dzienniki diagnostyczne](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) (można konfigurować). Dzienniki diagnostyczne wgląd bardziej rozbudowane w wszystko, co się dzieje z zadaniem. Diagnostyka rejestruje start po utworzeniu zadania hello i zakończenia po usunięciu hello zadania. Obejmują one zdarzeń po zaktualizowaniu hello zadania i jest uruchomiona.

> [!NOTE]
> Można użyć usług, takich jak dane przesłane tooanalyze magazynu Azure, Azure Event Hubs i analiza dzienników Azure. Naliczane są opłaty oparte na powitania cennik modelu dla tych usług.
>

## <a name="turn-on-diagnostics-logs"></a>Włączanie dzienników diagnostycznych

Dzienniki diagnostyczne są **poza** domyślnie. tooturn dzienników diagnostycznych, wykonaj następujące kroki:

1.  Zaloguj się toohello portalu Azure i przejdź toohello przesyłania strumieniowego bloku zadania. W obszarze **monitorowanie**, wybierz pozycję **dzienników diagnostycznych**.

    ![Dzienniki toodiagnostics nawigacji bloku](./media/stream-analytics-job-diagnostic-logs/image1.png)  

2.  Wybierz **Włącz diagnostykę**.

    ![Włączanie dzienników diagnostycznych](./media/stream-analytics-job-diagnostic-logs/image2.png)

3.  Na powitania **ustawień diagnostycznych** strony, dla **stan**, wybierz pozycję **na**.

    ![Zmiana stanu dzienników diagnostycznych](./media/stream-analytics-job-diagnostic-logs/image3.png)

4.  Konfigurowanie docelowego archiwizacji hello (konto magazynu, Centrum zdarzeń, analizy dzienników), który ma. Wybierz kategorie hello dzienników, które mają toocollect (wykonanie, tworzenie). 

5.  Zapisz nową konfigurację diagnostyki hello.

Konfiguracja diagnostyki Hello obowiązuje około 10 minut tootake. Po wykonaniu tej hello rejestruje start znajdujących się w celu archiwizacji hello skonfigurowane (widoczny na powitania **dzienników diagnostycznych** strony):

![Dzienniki toodiagnostics nawigacji bloku — Archiwizacja elementów docelowych](./media/stream-analytics-job-diagnostic-logs/image4.png)

Aby uzyskać więcej informacji na temat konfigurowania diagnostyki, zobacz [zbierania i wykorzystywania danych diagnostycznych z zasobów platformy Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs).

## <a name="diagnostics-log-categories"></a>Kategorie dziennika diagnostycznego

Obecnie możemy przechwytywania dwie kategorie dzienników diagnostycznych:

* **Tworzenie**. Przechwytywanie dziennika zdarzeń, które są powiązane toojob tworzenia operacji: zadania tworzenia, dodawania i usuwania wejściach i wyjściach, dodawanie i aktualizowanie hello zapytania, uruchamianie i zatrzymywanie hello zadania.
* **Wykonanie**. Przechwytywania zdarzeń występujących podczas wykonywania zadania:
    * Błędy połączenia
    * Błędy przetwarzania danych, w tym:
        * Zdarzenia, które nie jest zgodna z toohello zapytania definicji (typy niezgodne pól i wartości, brakujące pola itd.)
        * Wyrażenie oceny błędów
    * Inne zdarzenia i błędy

## <a name="diagnostics-logs-schema"></a>Schemat dzienników diagnostycznych

Wszystkie dzienniki są przechowywane w formacie JSON. Każdy wpis ma następujące typowe pola ciąg hello:

Nazwa | Opis
------- | -------
time | Znacznik czasu (w formacie UTC) hello dziennika.
resourceId | Identyfikator zasobu hello hello operacji miało miejsce, wielkimi literami. Zawiera hello identyfikator subskrypcji, grupy zasobów hello i hello nazwę zadania. Na przykład   **/SUBSCRIPTIONS/6503D296-DAC1-4449-9B03-609A1F4A1C87/RESOURCEGROUPS/MY-RESOURCE-GROUP/PROVIDERS/MICROSOFT. STREAMANALYTICS/STREAMINGJOBS/MYSTREAMINGJOB**.
category | Dziennika kategorii, albo **wykonywania** lub **tworzenie**.
operationName | Nazwa operacji hello, którym jest zalogowany. Na przykład **wysyłania zdarzeń: niepowodzenie toomysqloutput zapisu danych wyjściowych SQL**.
status | Stan operacji hello. Na przykład **** lub **zakończyło się pomyślnie**.
poziom | Poziom dziennika. Na przykład **błąd**, **ostrzeżenie**, lub **komunikat o charakterze informacyjnym**.
properties | Szczegóły konkretnego wpisu dziennika, zserializowanym w formacie ciągu JSON. Aby uzyskać więcej informacji zobacz następujące sekcje hello.

### <a name="execution-log-properties-schema"></a>Schemat właściwości dziennika wykonywania

Dzienniki wykonywania ma informacji o zdarzeniach, które wystąpiły podczas wykonywania zadania usługi analiza strumienia. Schemat Hello właściwości różni się w zależności od typu hello zdarzenia. Mamy obecnie hello następujące typy dzienniki wykonywania:

### <a name="data-errors"></a>Błędy danych

Wszelkie błędy występujące podczas hello zadania przetwarzania danych jest w tej kategorii dzienników. Najczęściej te dzienniki są tworzone podczas odczytu, dane serializacji i operacji zapisu. Dzienniki te nie zawierają błędów połączenia. Błędy łączności są traktowane jako zdarzenia ogólne.

Nazwa | Opis
------- | -------
Element źródłowy | Nazwa zadania hello wejściowych lub wyjściowych, którym wystąpił błąd hello.
Komunikat | Komunikat skojarzony z powodu błędu hello.
Typ | Typ błędu. Na przykład **DataConversionError**, **CsvParserError**, lub **ServiceBusPropertyColumnMissingError**.
Dane | Zawiera dane, które są przydatne tooaccurately Znajdź źródło hello hello błędu. Temat tootruncation, w zależności od wielkości.

W zależności od hello **operationName** wartości błędów danych ma hello następującego schematu:
* **Serializować zdarzenia**. Serializacji wystąpienia zdarzeń podczas operacji odczytu zdarzenia. Występują, gdy hello danych na dane wejściowe hello nie spełnia hello zapytanie schematu dla jednego z następujących powodów:
    * *Niezgodność typów podczas zdarzenia (de) serializować*: identyfikuje hello pola, które powoduje błąd hello.
    * *Nie można odczytać zdarzeń, nieprawidłowy serializacji*: zawiera informacje o lokalizacji hello w danych wejściowych hello którym wystąpił błąd hello. Zawiera nazwę obiektu blob danych wejściowych obiektu blob, przesunięcie oraz przykładowych danych hello.
* **Wysyłanie zdarzeń**. Wysłanie zdarzenia występują w trakcie operacji zapisu. Identyfikują one hello strumienia zdarzeń, który spowodował błąd hello.

### <a name="generic-events"></a>Zdarzenia ogólne

Zdarzenia ogólne obejmuje wszystkie inne elementy.

Nazwa | Opis
-------- | --------
Błąd | (opcjonalnie) Informacje o błędzie. Zazwyczaj jest to informacje o wyjątku, jeśli jest dostępna.
Komunikat| Komunikat w dzienniku.
Typ | Typ komunikatu. Mapuje kategoryzacji toointernal błędów. Na przykład **JobValidationError** lub **BlobOutputAdapterInitializationFailure**.
Identyfikator korelacji | [Identyfikator GUID](https://en.wikipedia.org/wiki/Universally_unique_identifier) który unikatowo identyfikuje hello wykonywania zadania. Wszystkie wpisy dziennika wykonywania z hello czasu hello zadania rozpoczyna się, dopóki Zatrzymuje zadanie hello mają takie same hello **identyfikator korelacji** wartość.

## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie tooStream analityka](stream-analytics-introduction.md)
* [Wprowadzenie do usługi analiza strumienia](stream-analytics-real-time-fraud-detection.md)
* [Zadania usługi analiza strumienia skali](stream-analytics-scale-jobs.md)
* [Dokumentacja języka zapytania usługi analiza strumienia](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Strumienia Analytics management REST API reference](https://msdn.microsoft.com/library/azure/dn835031.aspx)
