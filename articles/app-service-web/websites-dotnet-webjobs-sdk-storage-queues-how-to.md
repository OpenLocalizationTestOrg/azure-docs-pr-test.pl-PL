---
title: "toouse aaaHow magazynu kolejek Azure z hello zestaw SDK zadań Webjob"
description: "Dowiedz się, jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob. Tworzenie i usuwanie kolejek; Wstaw, zaglądanie, Pobierz i usuwanie wiadomości w kolejce i inne."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: dbfac5d9-f4a0-4e3e-9ecc-af3d7bf80463
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 49f844436b0453489800b2762a5c7dc30b9db805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a>Jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob
## <a name="overview"></a>Omówienie
Ten przewodnik zawiera C# przykłady pokazujące, jak toouse hello zestawu SDK zadań Webjob Azure w wersji 1.x z hello usługi magazynu kolejek Azure.

Witaj przewodnika przyjęto założenia, wiadomo, [jak toocreate projektu zadania WebJob w programie Visual Studio z połączeniem ciągi konto magazynu punktu tooyour](websites-dotnet-webjobs-sdk-get-started.md) lub zbyt[wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).

Większość fragmentów kodu hello Pokaż tylko funkcje, nie hello kod, który tworzy hello `JobHost` obiektu jak w poniższym przykładzie:

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

Witaj przewodnika hello następujące tematy:

* [Jak tootrigger funkcja po odebraniu komunikatu w kolejce](#trigger)
  * Ciąg wiadomości w kolejce
  * Wiadomości w kolejce POCO
  * Funkcje asynchroniczne
  * Atrybut QueueTrigger hello typy współpracuje z
  * Algorytm sondowania
  * Wiele wystąpień
  * Wykonywanie równoległe
  * Pobierz kolejki lub kolejka komunikatów metadanych
  * Łagodne zamykanie
* [Jak toocreate kolejki komunikatów podczas przetwarzania komunikatu w kolejce](#createqueue)
  * Ciąg wiadomości w kolejce
  * Wiadomości w kolejce POCO
  * Tworzenie wielu wiadomości lub w funkcji asynchronicznych
  * Atrybut kolejki hello typy współpracuje z
  * Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji
* [Jak tooread i zapisu obiektów blob podczas przetwarzania komunikatu w kolejce](#blobs)
  * Ciąg wiadomości w kolejce
  * Wiadomości w kolejce POCO
  * Typy hello obiektu Blob atrybutu współpracuje z
* [Jak toohandle zanieczyszczonych komunikatów](#poison)
  * Obsługa automatycznego Trująca wiadomość
  * Trująca wiadomość została ręcznej obsługi
* [Jak tooset opcje konfiguracji](#config)
  * Ustawianie parametrów połączenia SDK w kodzie
  * Skonfiguruj ustawienia QueueTrigger
  * Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
* [Jak tootrigger funkcji ręcznie](#manual)
* [Sposób rejestrowania toowrite](#logs)
* [Jak błędy toohandle i Konfigurowanie limitów czasu](#errors)
* [Następne kroki](#nextsteps)

## <a id="trigger"></a>Jak tootrigger funkcja po odebraniu komunikatu w kolejce
wywołuje funkcję hello zestaw SDK zadań Webjob toowrite po odebraniu komunikatu w kolejce, użyj hello `QueueTrigger` atrybutu. Konstruktor atrybutu Hello przyjmuje parametr ciąg określający nazwę hello hello toopoll kolejki. Możesz również [Ustaw nazwę kolejki hello dynamicznie](#config).

### <a name="string-queue-messages"></a>Ciąg wiadomości w kolejce
W hello poniższy przykład, kolejki hello zawiera komunikat, więc `QueueTrigger` jest stosowane tooa parametr ciągu o nazwie `logMessage` zawierającą hello zawartość hello kolejki wiadomości. Witaj funkcja [zapisuje dziennik komunikatów toohello pulpitu nawigacyjnego](#logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Oprócz `string`, parametr hello może być tablicą bajtów `CloudQueueMessage` obiektu lub POCO, które należy zdefiniować.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce
Poniższy przykład hello, komunikatu w kolejce hello zawiera JSON dla `BlobInformation` obiektu, który zawiera `BlobName` właściwości. Witaj SDK automatycznie deserializuje obiekt hello.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Witaj SDK używa hello [pakietu Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize i deserializować wiadomości. Wiadomości w kolejce w przypadku utworzenia w programie, który nie używa hello zestaw SDK zadań Webjob, można napisać kod, takich jak powitania po toocreate przykład komunikatu w kolejce POCO powitalne tego zestawu SDK można przeanalizować.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Funkcje asynchroniczne
Witaj następujących funkcji asynchronicznej [zapisuje dziennik toohello pulpitu nawigacyjnego](#logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Funkcje asynchroniczne może potrwać [token anulowania](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), jak pokazano w hello poniższy przykład, który kopiuje obiektu blob. (Aby uzyskać informacje o hello `queueTrigger` symbolu zastępczego, zobacz hello [obiekty BLOB](#blobs) sekcji.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <a id="qtattributetypes"></a>Atrybut QueueTrigger hello typy współpracuje z
Można użyć `QueueTrigger` z hello następujące typy:

* `string`
* Typ POCO zserializowanym w formacie JSON
* `byte[]`
* `CloudQueueMessage`

### <a id="polling"></a>Algorytm sondowania
Witaj SDK implementuje efekt losowe wykładniczego wycofywania algorytmu tooreduce hello bezczynności-kolejki sondowania kosztów transakcji magazynu.  Po znalezieniu wiadomość hello SDK oczekuje dwóch sekund i następnie wyszukuje kolejną wiadomość; gdy zostanie znaleziony żaden komunikat czeka około czterech sekund przed ponowną próbą. Po kolejnych nieudanych prób tooget komunikatu w kolejce, czas oczekiwania hello nadal tooincrease dopóki nie osiągnie hello maksymalny czas oczekiwania, które minutę tooone wartości domyślnych. [Witaj maksymalny czas oczekiwania jest konfigurowalne](#config).

### <a id="instances"></a>Wiele wystąpień
Jeśli aplikacja sieci web jest uruchamiana na wiele wystąpień, ciągłe zadanie WebJob jest uruchamiany na każdym komputerze, a każda maszyna zostanie poczekaj, aż usługa wyzwalaczy i podejmować toorun funkcji. Witaj zestaw SDK zadań Webjob kolejki wyzwalacza automatycznie uniemożliwia funkcji przetwarzania komunikatu w kolejce wiele razy; funkcje nie są zapisywane idempotentności toobe toobe. Jednak jeśli chcesz tooensure tego tylko jedno wystąpienie funkcji jest uruchamiany nawet wtedy, gdy istnieje wiele wystąpień aplikacji sieci web hosta hello, można użyć hello `Singleton` atrybutu.

### <a id="parallel"></a>Wykonywanie równoległe
Jeśli masz wiele funkcji nasłuchiwanie w kolejkach różnych hello SDK wywoła je równolegle po odebraniu wiadomości jednocześnie.

Witaj samo dotyczy po odebraniu wiele komunikatów dla pojedynczej kolejki. Domyślnie hello SDK pobiera partii 16 wiadomości w kolejce w czasie i wykonuje hello funkcja, która przetwarza je równolegle. [rozmiar partii Hello jest konfigurowalne](#config). Gdy numer hello przetwarzanych pobiera dół toohalf rozmiar partii hello, hello SDK pobiera inna partia i rozpoczyna przetwarzanie tych wiadomości. W związku z tym hello maksymalną liczbę równoczesnych komunikatów przetwarzanych dla każdej funkcji jest rozmiar partii hello co oraz wielokrotności. Ten limit dotyczy oddzielnie tooeach funkcja, która ma `QueueTrigger` atrybutu.

Jeśli nie chcesz wykonywanie równoległe dla wiadomości otrzymanych w jednej kolejki, można ustawić too1 rozmiar partii hello. Zobacz też **większą kontrolę nad kolejki przetwarzania** w [RTM zestawu Azure WebJobs SDK w wersji 1.1.0](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).

### <a id="queuemetadata"></a>Pobierz kolejki lub kolejka komunikatów metadanych
Możesz uzyskać hello następujące właściwości wiadomości przez dodanie podpis metody toohello parametry:

* `DateTimeOffset`expirationTime
* `DateTimeOffset`insertionTime
* `DateTimeOffset`nextVisibleTime
* `string`queueTrigger (tekst wiadomości zawiera)
* `string`Identyfikator
* `string`elementu popReceipt
* `int`dequeueCount

Jeśli chcesz toowork bezpośrednio z hello interfejsu API magazynu Azure, możesz także dodać `CloudStorageAccount` parametru.

Witaj poniższy przykład zapisuje wszystkie ten dziennik metadanych tooan informacje o aplikacji. Przykład Witaj zarówno logMessage i queueTrigger zawartością hello hello kolejki wiadomości.

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

Poniżej przedstawiono przykładowy dziennik napisane przez hello przykładowy kod:

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <a id="graceful"></a>Łagodne zamykanie
Funkcja, która działa w ciągłego zadania WebJob może akceptować `CancellationToken` parametr, który umożliwia hello systemu operacyjnego toonotify hello funkcji hello zadania WebJob dotyczy toobe zakończone. Możesz użyć tego toomake powiadomień, się, że funkcja hello nie nieoczekiwane zakończenie w sposób powodujący, że dane w niespójnym stanie.

powitania po przykładzie pokazano, jak toocheck zbliżającym się zakończenia zadania WebJob w funkcji.

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

**Uwaga:** hello pulpit nawigacyjny może nie poprawnie pokazać hello stan i dane wyjściowe funkcji, które została zamknięta.

Aby uzyskać więcej informacji, zobacz [łagodne zamykanie zadań Webjob](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).   

## <a id="createqueue"></a>Jak toocreate kolejki komunikatów podczas przetwarzania komunikatu w kolejce
toowrite funkcję, która tworzy nowy komunikat kolejki, użyj hello `Queue` atrybutu. Podobnie jak `QueueTrigger`, podaj nazwę kolejki hello jako ciąg lub możesz [Ustaw nazwę kolejki hello dynamicznie](#config).

### <a name="string-queue-messages"></a>Ciąg wiadomości w kolejce
powitania po przykładowy kod z systemem innym niż async tworzy nowego komunikatu w kolejce w kolejce hello o nazwie "outputqueue" z hello sama zawartość jako hello kolejki wiadomości odebrane w kolejce hello o nazwie "inputqueue". (Asynchroniczne Użyj funkcji `IAsyncCollector<T>` opisane dalej w tej sekcji.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce
toocreate komunikat z kolejki zawiera POCO niż ciąg hello przebiegu POCO wpisać jako toohello parametru wyjściowego `Queue` atrybut konstruktora.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Witaj SDK automatycznie serializuje hello tooJSON obiektu. Komunikatu w kolejce zawsze jest tworzony, nawet jeśli obiekt hello jest pusty.

### <a name="create-multiple-messages-or-in-async-functions"></a>Tworzenie wielu wiadomości lub w funkcji asynchronicznych
toocreate wiele komunikatów upewnij hello typu parametru dla kolejki wyjściowej hello `ICollector<T>` lub `IAsyncCollector<T>`, jak pokazano w hello poniższy przykład.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Każdy komunikat kolejki jest tworzony natychmiast po hello `Add` metoda jest wywoływana.

### <a name="types-that-hello-queue-attribute-works-with"></a>Typy atrybutu kolejki hello współpracuje z
Można użyć hello `Queue` atrybutu na powitania następujące typy parametrów:

* `out string`(tworzy komunikat z kolejki, jeśli wartość parametru jest różna od null, gdy funkcja hello kończy się)
* `out byte[]`(takich jak działa `string`)
* `out CloudQueueMessage`(takich jak działa `string`)
* `out POCO`(typ możliwy do serializacji, tworzy komunikat z obiektem null, jeśli parametru hello ma wartość null, gdy funkcja hello kończy się)
* `ICollector`
* `IAsyncCollector`
* `CloudQueue`(do tworzenia komunikatów ręcznie bezpośrednio za pomocą hello interfejsu API magazynu Azure)

### <a id="ibinder"></a>Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji
Jeśli potrzebujesz toodo niektóre działają w funkcji przed przy użyciu atrybutu zestaw SDK zadań Webjob, takich jak `Queue`, `Blob`, lub `Table`, można użyć hello `IBinder` interfejsu.

Poniższy przykład Hello pobiera wiadomość z kolejki wejściowej i tworzy nowy komunikat o tej samej zawartości w kolejki wyjściowej hello. Nazwa kolejki danych wyjściowych Hello jest ustawiana przez kod w treści hello hello funkcji.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

Witaj `IBinder` interfejsu można również z hello `Table` i `Blob` atrybutów.

## <a id="blobs"></a>Jak tooread i zapisu obiektów blob i tabelach podczas przetwarzania komunikatu w kolejce
Witaj `Blob` i `Table` atrybutów umożliwiają tooread i zapisywać obiekty BLOB i tabelach. Witaj próbek w tej sekcji mają zastosowanie tooblobs. Aby uzyskać przykłady kodu, które pokazują, jak tootrigger przetwarza podczas tworzenia lub aktualizowania obiektów blob, zobacz [jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)oraz przykłady kodu, do odczytu i zapisu tabel, zobacz [jak toouse tabeli platformy Azure Magazyn z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Ciąg wiadomości w kolejce wyzwalania operacje obiektów blob
Dla komunikatu w kolejce, który zawiera ciąg `queueTrigger` to symbol zastępczy, można użyć w hello `Blob` atrybutu `blobPath` parametr, który zawiera hello zawartość wiadomości powitania.

Witaj poniższym przykładzie użyto `Stream` obiekty BLOB tooread i zapisu. komunikat z kolejki Hello jest hello nazwa obiektu blob znajdujących się w kontenerze textblobs hello. Kopiowania obiektu blob hello z "-nowych" Nazwa toohello dołączany jest tworzony w hello sam kontenera.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Witaj `Blob` atrybutu ma konstruktora `blobPath` parametr, który określa kontener hello i nazwa obiektu blob. Aby uzyskać więcej informacji dotyczących tego symbolu zastępczego, zobacz [jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),

Gdy atrybut hello decorates `Stream` obiekt inny parametr konstruktora określa hello `FileAccess` trybie odczytu, zapisu lub odczytu/zapisu.

Witaj poniższym przykładzie użyto `CloudBlockBlob` obiekt toodelete obiektu blob. komunikat z kolejki Hello jest nazwą hello hello obiektu blob.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a id="pocoblobs"></a>POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce
POCO, zapisane w formacie JSON hello kolejki wiadomości, można użyć zastępcze nazw właściwości obiektu hello w hello `Queue` atrybutu `blobPath` parametru. Można również użyć [kolejka nazw właściwości metadanych](#queuemetadata) jako symbole zastępcze.

Witaj Poniższy przykładowy kod kopiuje obiekt blob tooa nowego obiektu blob z innym rozszerzeniem. komunikat z kolejki Hello jest `BlobInformation` obiekt, który zawiera `BlobName` i `BlobNameWithoutExtension` właściwości. nazwy właściwości Hello są używane jako symbole zastępcze w ścieżce obiektu blob hello hello `Blob` atrybutów.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Witaj SDK używa hello [pakietu Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize i deserializować wiadomości. Wiadomości w kolejce w przypadku utworzenia w programie, który nie używa hello zestaw SDK zadań Webjob, można napisać kod, takich jak powitania po toocreate przykład komunikatu w kolejce POCO powitalne tego zestawu SDK można przeanalizować.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Jeśli potrzebujesz toodo niektóre działają w funkcji przed powiązania obiektu blob tooan, można użyć atrybutu hello w treści funkcji hello hello [jak pokazano wcześniej atrybutu kolejki hello](#ibinder).

### <a id="blobattributetypes"></a>Typy, można użyć hello obiektu Blob atrybutu z
Witaj `Blob` atrybut może być używany z hello następujące typy:

* `Stream`(Odczyt lub zapis, określić przy użyciu parametru konstruktora FileAccess hello)
* `TextReader`
* `TextWriter`
* `string`(odczyt)
* `out string`(zapisu; tworzy obiektu blob tylko wtedy, gdy parametr ciąg hello jest inną niż null, gdy funkcja hello zwraca)
* POCO (odczyt)
* limit POCO (zapisu; zawsze tworzy obiektu blob, tworzy jako obiekt null, jeśli parametr POCO ma wartość null, gdy funkcja hello zwraca)
* `CloudBlobStream`(Zapisz)
* `ICloudBlob`(Odczyt lub zapis)
* `CloudBlockBlob`(Odczyt lub zapis)
* `CloudPageBlob`(Odczyt lub zapis)

## <a id="poison"></a>Jak toohandle zanieczyszczonych komunikatów
Komunikaty, których zawartość powoduje toofail funkcji są nazywane *zanieczyszczonych komunikatów*. W przypadku awarii funkcja hello hello kolejki wiadomości nie zostanie usunięta i ostatecznie zostaje pobrana ponownie, powodując toobe cyklu hello powtarzany. Hello SDK automatycznie może przerwać cyklu powitania po ograniczonej liczby iteracji, lub możesz zrobić to ręcznie.

### <a name="automatic-poison-message-handling"></a>Obsługa automatycznego Trująca wiadomość
Hello zestawu SDK wywoła funkcję się too5 razy tooprocess komunikatu w kolejce. W przypadku niepowodzenia spróbuj piątym powitania wiadomość hello jest przeniesionego tooa skażone kolejki. [konfiguruje się Hello maksymalnej liczby ponownych prób](#config).

nosi nazwę kolejki skażone Hello *{originalqueuename}*-skażone. Można napisać tooprocess funkcji wiadomości z kolejki skażone hello rejestrowania ich lub wysyłania powiadomienia, że wymagana jest ręczne uwagi.

W powitania po hello przykład `CopyBlob` funkcja zakończy się niepowodzeniem, gdy komunikatu w kolejce zawiera nazwę hello obiektu blob, który nie istnieje. W takim przypadku wiadomość hello jest przenoszona z hello copyblobqueue kolejki toohello copyblobqueue poison kolejki. Witaj `ProcessPoisonMessage` , a następnie Trująca wiadomość hello dzienników.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

Witaj poniżej przedstawiono dane wyjściowe konsoli z tych funkcji po skażone komunikat jest przetwarzany.

![Dane wyjściowe konsoli dotyczące obsługi uszkodzonych komunikatów](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a>Trująca wiadomość została ręcznej obsługi
Można uzyskać hello liczba wiadomości została pobrana do przetworzenia przez dodanie `int` parametru o nazwie `dequeueCount` tooyour funkcji. Mogą być następnie hello wyboru usuwania z kolejki liczby w kodzie funkcji i wykonać własne Trująca wiadomość została obsługa podczas numer hello przekracza próg, jak pokazano w hello poniższy przykład.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a id="config"></a>Jak tooset opcje konfiguracji
Można użyć hello `JobHostConfiguration` hello tooset typu następujące opcje konfiguracji:

* Ustawianie parametrów połączenia SDK hello w kodzie.
* Skonfiguruj `QueueTrigger` ustawienia, takie jak maksymalna liczba usuwania z kolejki.
* Pobierz nazwy kolejki z konfiguracji.

### <a id="setconnstr"></a>Ustawianie parametrów połączenia SDK w kodzie
Ustawianie parametrów połączenia SDK hello w kodzie umożliwia toouse możesz własne nazwy ciągu połączenia w plikach konfiguracji lub zmiennych środowiskowych, jak pokazano w hello poniższy przykład.

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="configqueue"></a>Skonfiguruj ustawienia QueueTrigger
Można skonfigurować następujące ustawienia dotyczące przetwarzania komunikatu w kolejce toohello hello:

* Maksymalna liczba wiadomości w kolejce, które są pobierane jednocześnie toobe wykonywane równolegle Hello (wartość domyślna to 16).
* Witaj maksymalnej liczby ponownych prób przed wysłaniem komunikatu w kolejce tooa skażone kolejki (wartość domyślna to 5).
* Witaj maksymalny czas oczekiwania przed sondowania ponownie, gdy kolejka jest pusta (wartość domyślna to 1 minuta).

powitania po przykładzie pokazano, jak tooconfigure te ustawienia:

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a id="setnamesincode"></a>Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
Czasami trzeba toospecify nazwę kolejki, nazwa obiektu blob lub kontener lub tabeli nazw w kodzie, a nie kodowane. Na przykład może być nazwę kolejki hello toospecify `QueueTrigger` w zmiennej środowisku i pliku konfiguracji.

Możesz to zrobić przez przekazywanie `NameResolver` obiekt toohello `JobHostConfiguration` typu. Obejmują specjalne symbole zastępcze ujęta w znaki procentu (%) w parametrach konstruktora atrybut zestaw SDK zadań Webjob i `NameResolver` kodu określa toobe wartości rzeczywistych hello używany zamiast te symbole zastępcze.

Na przykład załóżmy, że chcesz toouse kolejki o nazwie logqueuetest w środowisku testowym hello i jedną o nazwie logqueueprod w środowisku produkcyjnym. Zamiast nazwę kolejki ustalony ma nazwę hello toospecify wpis w hello `appSettings` kolekcji mające hello nazwa rzeczywista kolejki. Jeśli hello `appSettings` klucz jest logqueue, funkcja może wyglądać hello poniższy przykład.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Twoje `NameResolver` klasy, można uzyskać nazwy kolejki hello z `appSettings` pokazane na powitania poniższy przykład:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Przekaż hello `NameResolver` klasy w toohello `JobHost` obiektów, jak pokazano w hello poniższy przykład.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Uwaga:** nazwy obiektów blob, tabel i kolejki rozwiązywane są zawsze funkcja jest nazywana, ale nazwy kontenera obiektów blob są rozpoznawane tylko wtedy, gdy uruchamiana jest aplikacja hello. Nie można zmienić nazwy kontenera obiektów blob, gdy jest wykonywane zadanie hello.

## <a id="manual"></a>Jak tootrigger funkcji ręcznie
tootrigger funkcję ręcznie, użyj hello `Call` lub `CallAsync` metody na powitania `JobHost` obiekt i hello `NoAutomaticTrigger` atrybutu hello funkcji, jak pokazano w hello poniższy przykład.

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a id="logs"></a>Sposób rejestrowania toowrite
Witaj pulpitu nawigacyjnego przedstawia dzienniki w dwóch miejscach: hello stronę hello zadania WebJob i hello strony dla poszczególnych wywołań zadania WebJob.

![Dzienniki na stronie zadania WebJob](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Dzienniki na stronie wywołania funkcji](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

Dane wyjściowe z konsoli metody, które należy wywołać funkcję lub hello `Main()` metoda pojawia się na stronie pulpitu nawigacyjnego hello na powitania zadania WebJob, nie na stronie powitania dla wywołania metody określonej. Na stronie pulpitu nawigacyjnego hello wywołania metody zostaną wyświetlone dane wyjściowe z hello TextWriter obiektu, który można pobrać z parametrem w podpisie metody.

Dane wyjściowe konsoli nie może być wywołanie metody określonej tooa połączonej, ponieważ hello konsoli jest pojedynczym wątku, podczas gdy wiele funkcji zadanie może działać na powitania tym samym czasie. Dlatego hello SDK udostępnia każde wywołanie funkcji z własnego obiektu zapisującego unikatowy dziennika.

toowrite [dzienniki śledzenia aplikacji](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), użyj `Console.Out` (tworzy Dzienniki oznaczone jako informacje) i `Console.Error` (tworzy Dzienniki oznaczone jako błąd). Alternatywą jest toouse [śledzenia lub TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), która zapewnia pełne, ostrzeżenie, i krytyczne poziomy tooInfo dodanie i błąd. Dzienniki śledzenia aplikacji są wyświetlane w plikach dziennika aplikacji sieci web hello, tabelach platformy Azure lub w zależności od sposobu skonfigurowania aplikacji sieci web platformy Azure obiektów blob Azure. Jak wszystkie dane wyjściowe konsoli, najnowsze dzienniki 100 aplikacji hello również zostać wyświetlony na stronie pulpitu nawigacyjnego hello na powitania zadania WebJob, nie hello strony dla wywołania funkcji.

Dane wyjściowe konsoli zostanie wyświetlony w hello pulpitu nawigacyjnego tylko wtedy, gdy hello program działa w zadań WebJob Azure, nie, jeśli hello program działa lokalnie lub w niektórych innych środowiska.

Wyłącz rejestrowanie pulpitu nawigacyjnego dla scenariuszy wysokiej przepływności. Domyślnie program hello SDK zapisuje dzienniki toostorage, a to działanie może spowodować obniżenie wydajności podczas przetwarzania wielu komunikatów. Rejestrowanie toodisable ustawione toonull ciąg połączenia pulpitu nawigacyjnego hello, jak pokazano w hello poniższy przykład.

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

Witaj poniższym przykładzie pokazano kilka sposobów toowrite dzienników:

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

W hello pulpitu nawigacyjnego zestawu SDK zadań Webjob hello dane wyjściowe hello `TextWriter` pokazuje się po przejściu do strony toohello dla określonego wywołania funkcji i kliknij przycisk obiektów **Przełącz dane wyjściowe**:

![Kliknij łącze wywołania funkcji](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Dzienniki na stronie wywołania funkcji](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

W hello pulpitu nawigacyjnego zestawu SDK zadań Webjob hello najnowszych 100 wierszy konsoli output Pokaż zapasowej przejdź na stronę toohello hello zadania WebJob (a nie dla wywołania funkcji hello) i kliknięcie **dane wyjściowe Przełącz**.

![Kliknij przycisk przełączania danych wyjściowych](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

Ciągłe zadanie WebJob Dzienniki aplikacji wyświetlani w/data/zadania/ciągłego/*{webjobname}*/job_log.txt w systemie plików aplikacji hello w sieci web.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

W aplikacji hello obiektów blob platformy Azure dzienniki wyglądać następująco: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write — Witaj świecie! w, 2014-09-26T21:01:13, błąd, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.error — Witaj świecie!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out — Witaj świecie!,

W tabeli platformy Azure hello `Console.Out` i `Console.Error` dzienniki wyglądać następująco:

![Dziennik informacyjny w tabeli](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Dziennik błędów w tabeli](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

Chcąc własne rejestratora tooplug, zobacz [w tym przykładzie](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).

## <a id="errors"></a>Jak błędy toohandle i Konfigurowanie limitów czasu
Witaj zestaw SDK zadań Webjob obejmuje również [limitu czasu](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) atrybut, który można użyć toocause toobe funkcji anulowana, jeśli nie zakończył się w określonym czasie. Jeśli chcesz tooraise alert, gdy wystąpi zbyt wiele błędów w danym okresie czasu, można użyć hello `ErrorTrigger` atrybutu. Oto [przykład ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).

```
public static void ErrorMonitor(
[ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
[SendGrid(
    too= "admin@emailaddress.com",
    Subject = "Error!")]
 SendGridMessage message)
{
    // log last 5 detailed errors toohello Dashboard
   log.WriteLine(filter.GetDetailedMessage(5));
   message.Text = filter.GetDetailedMessage(1);
}
```

Można też dynamicznie Wyłącz i Włącz funkcje toocontrol, czy one mogą być wyzwalane, za pomocą przełącznika konfiguracji, który może być ustawienie aplikacji lub nazwę zmiennej środowiskowej. Przykładowy kod, zobacz hello `Disable` atrybutu w [hello zestaw SDK zadań Webjob przykłady repozytorium](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).

## <a id="nextsteps"></a> Następne kroki
W tym przewodniku dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z kolejek platformy Azure. Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).
