---
title: aaaIntroduction tooStream Analytics | Dokumentacja firmy Microsoft
description: "Poznaj usługę Stream Analytics — zarządzaną usługę, która pomaga analizować dane przesyłane strumieniowo z Internetu rzeczy (IoT) hello w czasie rzeczywistym."
keywords: "analiza jako usługa, usługi zarządzane, przetwarzanie strumienia, stream analytics, co to jest stream analytics"
services: stream-analytics
documentationcenter: 
author: jenniehubbard
manager: jhubbard
editor: cgronlun
ms.assetid: 613c9b01-d103-46e0-b0ca-0839fee94ca8
ms.service: stream-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/08/2017
ms.author: jhubbard
ms.openlocfilehash: 6dd7ea1d358bcc94e927a3e699a2771a25104d72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-stream-analytics"></a>Co to jest usługa Stream Analytics?

Usługa Azure Stream Analytics jest w pełni zarządzanym aparatem przetwarzania zdarzeń, który umożliwia ustawienie w czasie rzeczywistym obliczeń analitycznych na danych przesyłanych strumieniowo. Witaj dane mogą pochodzić z urządzeń, czujników, witryn sieci web, mediów społecznościowych źródeł danych, aplikacji, systemów infrastruktury i inne. 

## <a name="what-can-i-do-with-stream-analytics"></a>Do czego można używać usługi Stream Analytics?

Użyj Stream Analytics tooexamine dużych ilości danych wynikających z urządzeń lub procesy, wyodrębnienia informacji z hello strumienia danych i sprawdź wzorców, trendów i relacji. W zależności w danych hello, można wykonywać zadań aplikacji. Może na przykład zgłaszanie alertów, zaczną działać poza przepływy pracy usługi Automatyzacja, źródła danych raportowania narzędzia, takiego jak usługi Power BI tooa informacji lub przechowywania danych dla nowszej dochodzenia. 

Przykłady:

* Spersonalizowana analiza giełdowych transakcji handlowych w czasie rzeczywistym i alerty oferowane przez firmy z branży usług finansowych.
* Wykrywanie oszustw w czasie rzeczywistym w oparciu o badanie danych transakcji. 
* Usługi ochrony danych i tożsamości.
* Analiza danych wygenerowanych przez czujniki i siłowniki osadzone w obiektach fizycznych (Internet rzeczy — IoT).
* Analiza strumienia kliknięć w sieci Web.
* Zastosowania związane z zarządzaniem relacjami z klientami (CRM, Customer Relationship Management), takie jak generowanie alertów w sytuacji spadku poziomu obsługi klienta w danym przedziale czasu.

## <a name="how-does-stream-analytics-work"></a>Jak działa usługa Stream Analytics?

Ten diagram przedstawia hello Stream Analytics potoku, przedstawiający sposób przesłany prezentacji lub akcji, analizy i pozyskanych danych. 

![Potok usługi Stream Analytics](./media/stream-analytics-introduction/stream_analytics_intro_pipeline.png)

Analiza przesyłania strumieniowego jest uruchamiana w powiązaniu ze źródłem danych przesyłanych strumieniowo. Witaj danych można pozyskanych na platformie Azure przy użyciu urządzenia przy użyciu Centrum zdarzeń platformy Azure lub Centrum IoT. można również pobrania Hello danych z magazynu danych, takie jak magazyn obiektów Blob Azure. 

strumień hello tooexamine, Utwórz Stream Analytics *zadania* Określa, gdzie hello pochodzą dane. Określa także zadania Hello *przekształcania*&mdash;jak toolook danych, wzorce lub relacji. Dla tego zadania usługa Stream Analytics obsługuje język zapytań przypominający SQL, który umożliwia filtrowanie, sortowanie, agregowanie i łączenie danych przesyłanych strumieniowo w określonym czasie.

Ponadto zadania hello określa toosend hello przekształcone dane do. Umożliwia to kontrolę przeanalizowane toodo, jakie informacje toohello odpowiedzi. Na przykład w odpowiedzi tooanalysis, użytkownik może:

* Wyślij toochange polecenia ustawień dla urządzenia. 
* Wysyłanie danych tooa kolejki, która jest monitorowana przez proces, który podejmuje działania, po czym zależności. 
* Wyślij pulpit nawigacyjny usługi Power BI tooa danych raportowania.
* Wyślij toostorage danych, takich jak Data Lake Store, bazy danych programu SQL Server lub magazynu obiektów Blob platformy Azure lub tabeli.

W trakcie trwania zadania można je monitorować i dostosować liczbę zdarzeń przetwarzanych w ciągu sekundy. Można także ustawić zadania tak, aby tworzyły dzienniki diagnostyczne na potrzeby rozwiązywania problemów.

## <a name="key-capabilities-and-benefits"></a>Najważniejsze funkcje i korzyści

Analiza strumienia jest zaprojektowana toobe łatwe toouse zadania elastyczne, skalowalne tooany rozmiarze i ekonomiczny.

### <a name="connectivity-toomany-inputs-and-outputs"></a>Łączność toomany wejścia i wyjścia

Stream Analytics łączy się bezpośrednio za[Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) i [Centrum IoT Azure](https://azure.microsoft.com/services/iot-hub/) wprowadzanie strumienia i hello [usługi magazynu obiektów Blob platformy Azure](https://docs.microsoft.com/azure/storage/storage-introduction#blob-storage-accounts) tooingest danych historycznych. W przypadku pobierania danych z centrów zdarzeń usługę Stream Analytics można łączyć z innymi źródłami danych i aparatami przetwarzania.

Dane wejściowe zadania mogą także zawierać dane referencyjne (dane statyczne lub zmieniające się powoli). Możesz także dołączyć do przesyłania strumieniowego danych toothis odwołania danych tooperform wyszukiwania operacje hello tak samo jak z zapytań bazy danych.

Możesz kierować dane wyjściowe zadania usługi Stream Analytics w wielu kierunkach. Można napisać toostorage, takie jak obiekty BLOB magazynu Azure lub tabele, bazy danych SQL Azure, Azure Data Lake magazynów lub bazy danych Azure rozwiązania Cosmos. Z tego miejsca hello danych może odwiedź analizach wsadowych za pomocą usługi Azure HDInsight. Może wysłać usługi tooanother dane wyjściowe hello wykorzystania przez inny proces, takie jak usługi event hubs, tematów usługi Azure Service Bus lub kolejek. Może wysyłać hello dane wyjściowe tooPower BI do wizualizacji.

### <a name="ease-of-use"></a>Łatwość obsługi

przekształcenia toodefine Użyj prostego, deklaratywnego [języka zapytań usługi Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx) , która umożliwia tworzenie zaawansowanej analizy nie programowania. język zapytań Hello przyjmuje dane przesyłane strumieniowo jako dane wejściowe. Mogą być następnie filtrowania i sortowania danych hello agregowanie wartości, obliczeń dołączenia danych (w ramach strumienia lub tooreference danych) i funkcji geoprzestrzenne. Można edytować zapytania w portalu hello przy użyciu funkcji IntelliSense i sprawdzanie składni i przetestować zapytań przy użyciu przykładowych danych, które można wyodrębnić z hello strumień na żywo.

### <a name="extensible-query-language"></a>Rozszerzalny język zapytań

Można rozszerzyć możliwości hello języka kwerend hello przez zdefiniowanie i wywoływanie dodatkowe funkcje. Wywołania funkcji można zdefiniować w hello korzyści tootake usługi Azure Machine Learning rozwiązań do uczenia maszynowego Azure. Można również zintegrować JavaScript funkcje zdefiniowane przez użytkownika (UDF) w kolejności tooperform złożonych obliczeń, w ramach zapytań usługi Stream Analytics.

### <a name="scalability"></a>Skalowalność

Analiza strumienia może obsługiwać się too1 GB danych przychodzących na sekundę. Integracja z [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) i [Centrum IoT Azure](https://azure.microsoft.com/services/iot-hub/) umożliwia kilka zadań tooingest miliony zdarzeń na sekundę, przychodzących z połączonych urządzeń, kliknięć i pliki dziennika tooname. Za pomocą funkcji partycji hello usługi event hubs, można podzielić obliczenia na etapy logiczne, każde z nich hello możliwość dalszego toobe skalowalność tooincrease podzielona na partycje.

### <a name="low-cost"></a>Niski koszt

Jako usługa w chmurze Stream Analytics jest zoptymalizowana toolet, które możesz zacząć przy niskich kosztach. Płaci się zgodnie z rzeczywistym na jednostek przesyłania strumieniowego użycia i hello ilości danych przetwarzanych przez hello system. Użycie jest określane w oparciu o hello ilości przetworzonych zdarzeń i hello ilości mocy obliczeniowej udostępnionej w toohandle klastra hello zadania usługi analiza strumienia.

### <a name="reliability-quick-recovery-and-repeatability"></a>Niezawodność, szybkie odzyskiwanie i powtarzalność

Jako zarządzana usługa w chmurze hello Stream Analytics pomaga uniknąć utraty danych i zapewnia ciągłość prowadzenia działalności biznesowej. Jeśli wystąpią błędy, hello udostępnia wbudowanych funkcji odzyskiwania. Z możliwością hello toointernally zarządzania stanem, usługa hello zapewnia powtarzalne wyniki, zapewniając jest możliwe tooarchive zdarzeń i ponownie zastosuj przetwarzania w przyszłości hello zawsze pobierania hello takie same wyniki. To pozwala toogo Wstecz w czasie i badanie obliczeń podczas ustalania analizy głównej przyczyny problemu, analizy warunkowej i tak dalej.

## <a name="next-steps"></a>Następne kroki

* Rozpoczynanie pracy przez [eksperymentowanie z danymi wejściowymi i zapytaniami z urządzeń IoT](stream-analytics-get-started-with-azure-stream-analytics-to-process-data-from-iot-devices.md).
* Tworzenie [rozwiązania analizy strumienia end-to-end](stream-analytics-real-time-fraud-detection.md) która sprawdza telefonu toolook metadanych dla fałszywych wywołań.
* Więcej informacji o hello języka przypominającego SQL zapytań usługi Stream Analytics oraz o koncepcjach unikatowe, takich jak [funkcje okna](stream-analytics-window-functions.md).
* Dowiedz się, jak za[skalowanie zadania usługi analiza strumienia](stream-analytics-scale-jobs.md). 
* Dowiedz się, jak za[integracji usługi analiza strumienia i usługi Azure Machine Learning](stream-analytics-machine-learning-integration-tutorial.md).
* Odpowiedzi tooyour Stream Analytics pytania w hello [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

