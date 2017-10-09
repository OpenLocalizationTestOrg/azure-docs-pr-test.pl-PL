---
title: "Przetwarzanie aaaStream analizy w czasie rzeczywistym dla usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse funkcji platformy Azure połączony z kolejką usługi Service Bus, toopopulate pamięć podręczna Redis Azure z hello dane wyjściowe zadania usługi analiza strumienia."
keywords: "strumień danych, pamięć podręczna redis, kolejką usługi service bus"
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a>Jak toostore dane z usługi Azure Stream Analytics w pamięci podręcznej Redis Azure za pomocą usługi Azure Functions
Usługa Azure Stream Analytics umożliwia szybkie tworzenie i wdrażanie wgląd w czasie rzeczywistym toogain niskokosztowych rozwiązań z urządzeń, czujników, infrastruktury i aplikacji lub dowolny strumień danych. Umożliwia on różnych przypadków użycia, np. w czasie rzeczywistym zarządzania i monitorowania, polecenia kontroli, wykrywanie oszustw, połączonych samochodów i wiele innych. W wielu scenariuszach takich można toostore danych wyjściowych z usługi Azure Stream Analytics do magazynu danych rozproszonych, takich jak pamięć podręczna Azure Redis.

Załóżmy, że są częścią telekomunikacyjnych firmy. Próbujesz toodetect SIM oszustwa, gdzie wiele wywołań pochodzące z hello tej samej tożsamości, na hello sam czasu, ale w różnych geograficznie lokalizacje. Możesz są zlecił mu przechowywania wszystkich hello potencjalnych fałszywych rozmów telefonicznych w pamięci podręcznej Azure Redis. W tym wpisie udostępniamy wskazówki na jak łatwo można wykonać zadanie. 

## <a name="prerequisites"></a>Wymagania wstępne
Zakończenie hello [wykrywanie oszustw w czasie rzeczywistym] [ fraud-detection] przewodnika dla ASA

## <a name="architecture-overview"></a>Przegląd architektury
![Zrzut ekranu przedstawiający architektury](./media/stream-analytics-functions-redis/architecture-overview.png)

Jak pokazano na powyższej ilustracji hello, Stream Analytics umożliwia przesyłanie strumieniowe danych wejściowych toobe zbadać i wysyłane tooan danych wyjściowych. W oparciu o dane wyjściowe hello, usługi Azure Functions można wyzwolić pewien typ zdarzenia. 

W tym wpisie możemy skupić się na powitania usługi Azure Functions częścią tego potoku lub dokładniej hello wyzwolenie zdarzenia, które przechowuje w pamięci podręcznej hello fałszywych danych.
Po zakończeniu hello [wykrywanie oszustw w czasie rzeczywistym] [ fraud-detection] samouczek, masz danych wejściowych (Centrum zdarzeń), kwerendy i danych wyjściowych (magazynu obiektów blob) już skonfigurowane i uruchomione. W tym wpisie zamiast tego zmienić toouse dane wyjściowe hello kolejką usługi Service Bus. Po wykonaniu tej połączymy kolejki toothis funkcji platformy Azure. 

## <a name="create-and-connect-a-service-bus-queue-output"></a>Tworzenie i łączenie wyjściowego kolejką usługi Service Bus
toocreate kolejką usługi Service Bus, wykonaj kroki 1 i 2 hello .NET części [Rozpoczynanie pracy z kolejek usługi Service Bus][servicebus-getstarted].
Teraz załóżmy połączyć zadanie usługi Stream Analytics toohello kolejki hello, który został utworzony w hello wcześniejszych przewodnika wykrywanie oszustw.

1. W hello portalu Azure, przejdź do pozycji toohello **dane wyjściowe** bloku zadania i wybierz **Dodaj** u góry hello hello strony.
   
    ![Dodawanie danych wyjściowych](./media/stream-analytics-functions-redis/adding-outputs.png)
2. Wybierz **kolejką usługi Service Bus** jako hello **Sink** i wykonaj instrukcje hello na ekranie powitania. Czy toochoose hello przestrzeń nazw hello kolejką usługi Service Bus można utworzyć w [Rozpoczynanie pracy z kolejek usługi Service Bus][servicebus-getstarted]. Kliknij przycisk "prawa" hello, po zakończeniu.
3. Określ hello następujące wartości:
   
   * **Format serializator zdarzeń**: JSON
   * **Kodowanie**: UTF8
   * **FORMAT**: rozdzielone
4. Kliknij przycisk hello **Utwórz** przycisk tooadd tego źródła i czy Stream Analytics może pomyślnie połączyć z konta magazynu toohello tooverify.
5. W hello **zapytania** karcie, Zastąp następujące hello hello bieżącego zapytania. Zastąp * [YOUR SERVICE BUS NAME] * o nazwie dane wyjściowe hello utworzonego w kroku 3. 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a>Tworzenie usługi Azure Redis Cache
Utwórz pamięci podręcznej Azure Redis, wykonując hello .NET części [jak tooUse pamięć podręczna Redis Azure] [ use-rediscache] dopóki hello sekcji o nazwie ***Konfigurowanie klientów pamięci podręcznej hello***.
Po wykonaniu tych czynności należy nowej pamięci podręcznej Redis. W obszarze **wszystkie ustawienia**, wybierz pozycję **klucze dostępu** i zanotuj hello ***parametry połączenia podstawowej***.

![Zrzut ekranu przedstawiający architektury](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a>Tworzenie funkcji platformy Azure
Postępuj zgodnie z [tworzenie pierwszej funkcji platformy Azure] [ functions-getstarted] tooget samouczka Wprowadzenie do usługi Azure Functions. Jeśli masz już funkcję platformy Azure będzie toouse, takich jak następnie przejść od razu zbyt[zapisywania tooRedis pamięci podręcznej](#Writing-to-Redis-Cache)

1. W portalu hello wybierać usługi aplikacji hello nawigacji po lewej stronie, a następnie kliknij witrynę sieci Web z funkcji Azure app nazwa tooget toohello funkcji aplikacji.
    ![Zrzut ekranu przedstawiający listę funkcji usług aplikacji](./media/stream-analytics-functions-redis/app-services-function-list.png)
2. Kliknij przycisk **nową funkcję > ServiceBusQueueTrigger — C#**. Hello następujących pól, wykonaj te instrukcje:
   
   * **Nazwa kolejki**: hello takie same nazwy jako nazwy hello wprowadzona podczas tworzenia kolejki hello w [Rozpoczynanie pracy z kolejek usługi Service Bus] [ servicebus-getstarted] (nie nazwę hello hello service Bus). Upewnij się, że używasz hello kolejki, który jest połączony toohello, którego analiza strumienia wyjściowego.
   * **Połączenia magistrali usług**: Wybierz **dodać parametry połączenia**. Wybierz parametry połączenia hello toofind, przejdź toohello klasycznego portalu **usługi Service Bus**, hello usługi service bus został utworzony, i **informacje o połączeniu** u dołu hello hello ekranu. Upewnij się, że znajdują się na ekranie głównym hello na tej stronie. Skopiuj i Wklej parametry połączenia hello. Możesz tooenter wolne dowolna nazwa połączenia.
     
       ![Zrzut ekranu przedstawiający połączenia magistrali usług](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * **AccessRights**: Wybierz **zarządzania**
3. Kliknij przycisk **Utwórz**

## <a name="writing-tooredis-cache"></a>Zapisywanie tooRedis pamięci podręcznej
Teraz utworzono funkcji platformy Azure, która odczytuje z kolejką usługi Service Bus. Pozostało toodo jest użyć naszych toowrite funkcja tego toohello danych pamięci podręcznej Redis. 

1. Wybierz nowo utworzony **ServiceBusQueueTrigger**i kliknij przycisk **funkcji ustawienia aplikacji** na powitania prawym górnym rogu. Wybierz **Przejdź ustawień usługi tooApp > Ustawienia > Ustawienia aplikacji**
2. W hello sekcji ciągów połączenia, Utwórz nazwę w hello **nazwa** sekcji. Wklej parametry połączenia podstawowej hello znaleziony w hello **Tworzenie pamięci podręcznej Redis** Wkrocz do hello **wartość** sekcji. Wybierz **niestandardowy** gdzie mówi **bazy danych SQL**.
3. Kliknij przycisk **zapisać** u góry hello.
   
    ![Zrzut ekranu przedstawiający połączenia magistrali usług](./media/stream-analytics-functions-redis/function-connection-string.png)
4. Teraz wróć toohello aplikacji usługi ustawień i wybierz **Narzędzia > Edytor usług aplikacji (wersja zapoznawcza) > na > Przejdź**.
   
    ![Zrzut ekranu przedstawiający połączenia magistrali usług](./media/stream-analytics-functions-redis/app-service-editor.png)
5. W wybranym edytorze, Utwórz plik JSON o nazwie **project.json** z hello po i zapisaniu tooyour dysku lokalnym.
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. Przekazywanie tego pliku w katalogu głównym hello funkcji (nie WWWROOT). Powinny pojawić się w pliku o nazwie **plikiem project.lock.json** pojawiają się automatycznie, potwierdzenie, że hello Nuget "Programie StackExchange.Redis" i "Newtonsoft.Json" importowaniu pakietów.
7. W hello **run.csx** pliku, Zastąp hello wstępnie wygenerowanego kodu hello następującego kodu. W funkcji lazyConnection hello, zastąp "POŁ NAME" o nazwie hello utworzonego w kroku 2 **przechowywania danych w pamięci podręcznej Redis hello**.

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a>Uruchom zadanie usługi Stream Analytics hello
1. Uruchom aplikację telcodatagen.exe hello. Użycie Hello jest następujący:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````
2. W bloku zadania usługi analiza strumienia hello w portalu powitania kliknij **Start** u góry hello hello strony.
   
    ![Zrzut ekranu przedstawiający zadanie rozpoczęcia](./media/stream-analytics-functions-redis/starting-job.png)
3. W hello **rozpoczęcia zadania** wyświetlonym bloku, wybierz **teraz** , a następnie kliknij przycisk hello **Start** przycisk u dołu hello hello ekranu. Stan zadania Hello zmienia tooStarting i po czasie niektóre tooRunning zmiany.
   
    ![Zrzut ekranu przedstawiający wybór godziny rozpoczęcia zadania](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a>Uruchamianie rozwiązania i wyniki sprawdzenia
Cofnięcie tooyour **ServiceBusQueueTrigger** strony, powinien zostać wyświetlony dziennika instrukcje. Te dzienniki pokazują, że coś uzyskanego od hello kolejką usługi Service Bus, umieść ją do bazy danych hello, oraz pobranych go się przy użyciu czasu hello jako klucz hello!

tooverify, które dane są w pamięci podręcznej Redis, przejdź strony pamięci podręcznej Redis tooyour hello nowego portalu (jak pokazano w poprzednim hello [Tworzenie pamięci podręcznej Redis Azure](#Create-an-Azure-Redis-Cache) krok) i wybierz konsoli.

Teraz można napisać tooconfirm polecenia Redis dane znajdują się w pamięci podręcznej hello w rzeczywistości.

![Zrzut ekranu konsoli pamięci podręcznej Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a>Następne kroki
Firma Microsoft Cieszymy się o nowościach hello Azure Functions Stream analytics można zrobić ze sobą i mamy nadzieję, że to zyskujesz dzięki nowych możliwości. Jeśli masz opinię na następny mają uznać hello wolnego toouse [witryny Azure UserVoice](https://feedback.azure.com/forums/270577-stream-analytics).

Jeśli nowy Microsoft Azure, zachęcamy tootry go przez skorzystania [bezpłatnego konta wersji próbnej Azure](https://azure.microsoft.com/pricing/free-trial/). Jeśli są nowe tooStream Analytics, a następnie zachęcamy zbyt[utworzyć swoją pierwszą pracę Stream Analytics](stream-analytics-create-a-job.md).

Jeśli potrzebujesz żadnego pomocy lub masz pytania, opublikuj wpis na [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) lub [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forach. 

Można również wyświetlić hello następujące zasoby:

* [Dokumentacja usługi Azure Functions dla deweloperów](../azure-functions/functions-reference.md)
* [Azure dokumentacja dla deweloperów funkcje C#](../azure-functions/functions-reference-csharp.md)
* [Azure dokumentacja dla deweloperów funkcje F #](../azure-functions/functions-reference-fsharp.md)
* [Dokumentacja dla deweloperów NodeJS funkcji platformy Azure](../azure-functions/functions-reference.md)
* [Azure funkcje wyzwalaczy i powiązań](../azure-functions/functions-triggers-bindings.md)
* [Jak toomonitor Azure pamięci podręcznej Redis](../redis-cache/cache-how-to-monitor.md)

Wykonaj toostay aktualne we wszystkich najnowsze wiadomości powitania i funkcje, [ @AzureStreaming ](https://twitter.com/AzureStreaming) w serwisie Twitter.

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
