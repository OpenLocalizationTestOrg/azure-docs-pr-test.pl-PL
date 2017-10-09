---
title: "aaaGetting pracę z magazynu kolejek i Visual Studio podłączonych usług (projekty zadania WebJob) | Dokumentacja firmy Microsoft"
description: "Jak tooget pracy z magazynem kolejek Azure w projektu zadania WebJob po łączenie tooa konto magazynu przy użyciu programu Visual Studio połączenia usługi."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 720e96fda734c31e1b1d68d4f95aa9531a20a3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a>Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (zadania WebJob projekty)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Omówienie
W tym artykule opisano sposób uzyskać uruchomić za pomocą kolejek Azure hello magazynu w projekcie zadania programu Visual Studio Azure WebJob po utworzony lub odwołanie do konta magazynu platformy Azure przy użyciu programu Visual Studio **dodać usług połączonych** — okno dialogowe. Po dodaniu projektu zadania WebJob tooa konto magazynu przy użyciu programu Visual Studio hello **dodać usług połączonych** okna dialogowego, hello odpowiednie pakiety NuGet magazynu Azure są zainstalowane, hello odpowiednie .NET odwołania są dodane toohello Projekt i parametry połączenia dla konta magazynu hello są aktualizowane w pliku App.config hello.  

Ten artykuł zawiera C# przykłady pokazujące, jak toouse hello zestawu SDK zadań Webjob Azure w wersji 1.x z hello usługi magazynu kolejek Azure.

Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS. Pojedynczy komunikat z kolejki można się too64 KB, rozmiar, a kolejka może zawierać miliony komunikatów w górę toohello całkowitego limitu pojemności konta magazynu. Zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md) Aby uzyskać więcej informacji. Aby uzyskać więcej informacji na temat platformy ASP.NET, zobacz [ASP.NET](http://www.asp.net).

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a>Jak tootrigger funkcja po odebraniu komunikatu w kolejce
wywołuje funkcję hello zestaw SDK zadań Webjob toowrite po odebraniu komunikatu w kolejce, użyj hello **QueueTrigger** atrybutu. Konstruktor atrybutu Hello przyjmuje parametr ciąg określający nazwę hello hello toopoll kolejki. toosee jak tooset hello Nazwa kolejki dynamicznie, zapoznaj się z [jak tooset opcje konfiguracji](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Ciąg wiadomości w kolejce
W hello poniższy przykład, kolejki hello zawiera komunikat, więc **QueueTrigger** jest stosowane tooa parametr ciągu o nazwie **logMessage** zawierającą hello zawartość hello kolejki wiadomości. Witaj funkcja [zapisuje dziennik komunikatów toohello pulpitu nawigacyjnego](#how-to-write-logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Oprócz **ciąg**, parametr hello może być tablicą bajtów **CloudQueueMessage** obiektu lub POCO, które należy zdefiniować.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce
Poniższy przykład hello, komunikatu w kolejce hello zawiera JSON dla **BlobInformation** obiektu, który zawiera **element BlobName** właściwości. Witaj SDK automatycznie deserializuje obiekt hello.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Witaj SDK używa hello [pakietu Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize i deserializować wiadomości. Wiadomości w kolejce w przypadku utworzenia w programie, który nie używa hello zestaw SDK zadań Webjob, można napisać kod, takich jak powitania po toocreate przykład komunikatu w kolejce POCO powitalne tego zestawu SDK można przeanalizować.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Funkcje asynchroniczne
Witaj następujących funkcji asynchronicznej [zapisuje dziennik toohello pulpitu nawigacyjnego](#how-to-write-logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Funkcje asynchroniczne może potrwać [token anulowania](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), jak pokazano w hello poniższy przykład, który kopiuje obiektu blob. (Aby uzyskać informacje o hello **queueTrigger** symbolu zastępczego, zobacz hello [obiekty BLOB](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) sekcji.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a>Atrybut QueueTrigger hello typy współpracuje z
Można użyć **QueueTrigger** z hello następujące typy:

* **ciąg**
* Typ POCO zserializowanym w formacie JSON
* **Byte]**
* **CloudQueueMessage**

## <a name="polling-algorithm"></a>Algorytm sondowania
Witaj SDK implementuje efekt losowe wykładniczego wycofywania algorytmu tooreduce hello bezczynności-kolejki sondowania kosztów transakcji magazynu.  Po znalezieniu wiadomość hello SDK oczekuje dwóch sekund i następnie wyszukuje kolejną wiadomość; gdy zostanie znaleziony żaden komunikat czeka około czterech sekund przed ponowną próbą. Po kolejnych nieudanych prób tooget komunikatu w kolejce, czas oczekiwania hello nadal tooincrease dopóki nie osiągnie hello maksymalny czas oczekiwania, które minutę tooone wartości domyślnych. [Witaj maksymalny czas oczekiwania jest konfigurowalne](#how-to-set-configuration-options).

## <a name="multiple-instances"></a>Wiele wystąpień
Jeśli aplikacja sieci web jest uruchamiana na wiele wystąpień, ciągłe zadania Webjob działa na każdym komputerze, a każda maszyna zostanie poczekaj, aż usługa wyzwalaczy i podejmować toorun funkcji. W niektórych scenariuszach, które może to spowodować funkcje toosome przetwarzania hello tych samych danych dwa razy, więc funkcje powinno być idempotentności (zapisany, który je wielokrotnie wywołuje z tymi samymi danymi wejściowymi nie tworzy powitalne Duplikuj wyniki).  

## <a name="parallel-execution"></a>Wykonywanie równoległe
Jeśli masz wiele funkcji nasłuchiwanie w kolejkach różnych hello SDK wywoła je równolegle po odebraniu wiadomości jednocześnie.

Witaj samo dotyczy po odebraniu wiele komunikatów dla pojedynczej kolejki. Domyślnie hello SDK pobiera partii 16 wiadomości w kolejce w czasie i wykonuje hello funkcja, która przetwarza je równolegle. [rozmiar partii Hello jest konfigurowalne](#how-to-set-configuration-options). Gdy numer hello przetwarzanych pobiera dół toohalf rozmiar partii hello, hello SDK pobiera inna partia i rozpoczyna przetwarzanie tych wiadomości. W związku z tym hello maksymalną liczbę równoczesnych komunikatów przetwarzanych dla każdej funkcji jest rozmiar partii hello co oraz wielokrotności. Ten limit dotyczy oddzielnie tooeach funkcja, która ma **QueueTrigger** atrybutu. Jeśli nie chcesz wykonywanie równoległe dla wiadomości otrzymanych w jednej kolejki, należy ustawić too1 rozmiar partii hello.

## <a name="get-queue-or-queue-message-metadata"></a>Pobierz kolejki lub kolejka komunikatów metadanych
Możesz uzyskać hello następujące właściwości wiadomości przez dodanie podpis metody toohello parametry:

* **DateTimeOffset** expirationTime
* **DateTimeOffset** insertionTime
* **DateTimeOffset** nextVisibleTime
* **ciąg** queueTrigger (zawiera tekst wiadomości)
* **ciąg** id
* **ciąg** elementu popReceipt
* **int** dequeueCount

Jeśli chcesz toowork bezpośrednio z hello interfejsu API magazynu Azure, możesz także dodać **CloudStorageAccount** parametru.

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

## <a name="graceful-shutdown"></a>Łagodne zamykanie
Funkcja, która działa w ciągłego zadania WebJob może akceptować **CancellationToken** parametr, który umożliwia hello systemu operacyjnego toonotify hello funkcji hello zadania WebJob dotyczy toobe zakończone. Możesz użyć tego toomake powiadomień, się, że funkcja hello nie nieoczekiwane zakończenie w sposób powodujący, że dane w niespójnym stanie.

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

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a>Jak toocreate kolejki komunikatów podczas przetwarzania komunikatu w kolejce
toowrite funkcję, która tworzy nowy komunikat kolejki, użyj hello **kolejki** atrybutu. Podobnie jak **QueueTrigger**, podaj nazwę kolejki hello jako ciąg lub możesz [Ustaw nazwę kolejki hello dynamicznie](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Ciąg wiadomości w kolejce
powitania po przykładowy kod z systemem innym niż async tworzy nowego komunikatu w kolejce w kolejce hello o nazwie "outputqueue" z hello sama zawartość jako hello kolejki wiadomości odebrane w kolejce hello o nazwie "inputqueue". (Asynchroniczne Użyj funkcji **IAsyncCollector<T>**  opisane dalej w tej sekcji.)

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce
toocreate komunikat z kolejki zawiera POCO niż ciąg hello przebiegu POCO typu jako dane wyjściowe parametru toohello **kolejki** atrybut konstruktora.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Witaj SDK automatycznie serializuje hello tooJSON obiektu. Komunikatu w kolejce zawsze jest tworzony, nawet jeśli obiekt hello jest pusty.

### <a name="create-multiple-messages-or-in-async-functions"></a>Tworzenie wielu wiadomości lub w funkcji asynchronicznych
toocreate wiele komunikatów upewnij hello typu parametru dla kolejki wyjściowej hello **ICollector<T>**  lub **IAsyncCollector<T>**, jak pokazano w hello poniższy przykład.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Każdy komunikat kolejki jest tworzony natychmiast po hello **Dodaj** metoda jest wywoływana.

### <a name="types-that-hello-queue-attribute-works-with"></a>Typy atrybutu kolejki hello współpracuje z
Można użyć hello **kolejki** atrybutu na powitania następujące typy parametrów:

* **limit ciąg** (tworzy komunikat z kolejki, jeśli wartość parametru jest różna od null, gdy funkcja hello kończy się)
* **limit byte []** (takich jak działa **ciąg**)
* **limit CloudQueueMessage** (takich jak działa **ciąg**)
* **limit POCO** (typ możliwy do serializacji, tworzy komunikat z obiektem null, jeśli parametru hello ma wartość null, gdy funkcja hello kończy się)
* **ICollector**
* **IAsyncCollector**
* **CloudQueue** (do tworzenia komunikatów ręcznie przy użyciu hello interfejsu API magazynu Azure bezpośrednio)

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a>Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji
Jeśli potrzebujesz toodo niektóre działają w funkcji przed przy użyciu atrybutu zestaw SDK zadań Webjob, takich jak **kolejki**, **obiektu Blob**, lub **tabeli**, można użyć hello **IBinder** interfejsu.

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

Witaj **IBinder** interfejsu można również z hello **tabeli** i **obiektu Blob** atrybutów.

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a>Jak tooread i zapisu obiektów blob i tabelach podczas przetwarzania komunikatu w kolejce
Witaj **obiektu Blob** i **tabeli** atrybutów umożliwiają tooread i zapisywać obiekty BLOB i tabelach. Witaj próbek w tej sekcji mają zastosowanie tooblobs. Aby uzyskać przykłady kodu, które pokazują, jak tootrigger przetwarza podczas tworzenia lub aktualizowania obiektów blob, zobacz [jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)oraz przykłady kodu, do odczytu i zapisu tabel, zobacz [jak toouse tabeli platformy Azure Magazyn z hello zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Ciąg wiadomości w kolejce wyzwalania operacje obiektów blob
Dla komunikatu w kolejce, który zawiera ciąg **queueTrigger** to symbol zastępczy, można użyć w hello **obiektu Blob** atrybutu **blobPath** parametr, który zawiera zawartość hello wiadomości powitania.

Witaj poniższym przykładzie użyto **strumienia** obiekty BLOB tooread i zapisu. komunikat z kolejki Hello jest hello nazwa obiektu blob znajdujących się w kontenerze textblobs hello. Kopiowania obiektu blob hello z "-nowych" Nazwa toohello dołączany jest tworzony w hello sam kontenera.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Witaj **obiektów Blob** atrybutu ma konstruktora **blobPath** parametr, który określa kontener hello i nazwa obiektu blob. Aby uzyskać więcej informacji dotyczących tego symbolu zastępczego, zobacz [jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).

Gdy atrybut hello decorates **strumienia** obiekt inny parametr konstruktora określa hello **FileAccess** trybie odczytu, zapisu lub odczytu/zapisu.

Witaj poniższym przykładzie użyto **CloudBlockBlob** obiekt toodelete obiektu blob. komunikat z kolejki Hello jest nazwą hello hello obiektu blob.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce
POCO, zapisane w formacie JSON hello kolejki wiadomości, można użyć zastępcze nazw właściwości obiektu hello w hello **kolejki** atrybutu **blobPath** parametru. Nazwy właściwości metadanych kolejki służy również jako symbole zastępcze. Zobacz [uzyskać kolejki lub kolejka komunikatów metadanych](#get-queue-or-queue-message-metadata).

Witaj Poniższy przykładowy kod kopiuje obiekt blob tooa nowego obiektu blob z innym rozszerzeniem. komunikat z kolejki Hello jest **BlobInformation** obiekt, który zawiera **element BlobName** i **BlobNameWithoutExtension** właściwości. nazwy właściwości Hello są używane jako symbole zastępcze w ścieżce obiektu blob hello hello **obiektu Blob** atrybutów.

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

Jeśli potrzebujesz toodo niektóre działają w funkcji przed powiązania obiektu blob tooan można użyć atrybutu hello w treści hello funkcji hello, jak pokazano w [Użyj zestawu SDK zadań Webjob atrybutów w treści funkcji hello](#use-webjobs-sdk-attributes-in-the-body-of-a-function).

### <a name="types-you-can-use-hello-blob-attribute-with"></a>Typy, można użyć hello obiektu Blob atrybutu z
Witaj **obiektu Blob** atrybut może być używany z hello następujące typy:

* **Strumień** (Odczyt lub zapis, określić przy użyciu parametru konstruktora FileAccess hello)
* **TextReader**
* **Element TextWriter**
* **ciąg** (odczyt)
* **limit ciąg** (zapisu; tworzy obiektu blob tylko wtedy, gdy parametr ciąg hello jest inną niż null, gdy funkcja hello zwraca)
* POCO (odczyt)
* limit POCO (zapisu; zawsze tworzy obiektu blob, tworzy jako obiekt null, jeśli parametr POCO ma wartość null, gdy funkcja hello zwraca)
* **CloudBlobStream** (zapis)
* **ICloudBlob** (odczytu i zapisu)
* **CloudBlockBlob** (odczytu i zapisu)
* **CloudPageBlob** (odczytu i zapisu)

## <a name="how-toohandle-poison-messages"></a>Jak toohandle zanieczyszczonych komunikatów
Komunikaty, których zawartość powoduje toofail funkcji są nazywane *zanieczyszczonych komunikatów*. W przypadku awarii funkcja hello hello kolejki wiadomości nie zostanie usunięta i ostatecznie zostaje pobrana ponownie, powodując toobe cyklu hello powtarzany. Hello SDK automatycznie może przerwać cyklu powitania po ograniczonej liczby iteracji, lub możesz zrobić to ręcznie.

### <a name="automatic-poison-message-handling"></a>Obsługa automatycznego Trująca wiadomość
Hello zestawu SDK wywoła funkcję się too5 razy tooprocess komunikatu w kolejce. W przypadku niepowodzenia spróbuj piątym powitania wiadomość hello jest przeniesionego tooa skażone kolejki. Zobacz temat jak tooconfigure hello maksymalnej liczby ponownych prób w [jak opcje konfiguracji tooset](#how-to-set-configuration-options).

nosi nazwę kolejki skażone Hello *{originalqueuename}*-skażone. Można napisać tooprocess funkcji wiadomości z kolejki skażone hello rejestrowania ich lub wysyłania powiadomienia, że wymagana jest ręczne uwagi.

W powitania po hello przykład **CopyBlob** funkcja zakończy się niepowodzeniem, gdy komunikatu w kolejce zawiera nazwę hello obiektu blob, który nie istnieje. W takim przypadku wiadomość hello jest przenoszona z hello copyblobqueue kolejki toohello copyblobqueue poison kolejki. Witaj **ProcessPoisonMessage** , a następnie Trująca wiadomość hello dzienników.

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

![Dane wyjściowe konsoli dotyczące obsługi uszkodzonych komunikatów](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a>Trująca wiadomość została ręcznej obsługi
Można uzyskać hello liczba wiadomości została pobrana do przetworzenia przez dodanie **int** parametru o nazwie **dequeueCount** tooyour funkcji. Mogą być następnie hello wyboru usuwania z kolejki liczby w kodzie funkcji i wykonać własne Trująca wiadomość została obsługa podczas numer hello przekracza próg, jak pokazano w hello poniższy przykład.

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

## <a name="how-tooset-configuration-options"></a>Jak tooset opcje konfiguracji
Można użyć hello **JobHostConfiguration** hello tooset typu następujące opcje konfiguracji:

* Ustawianie parametrów połączenia SDK hello w kodzie.
* Skonfiguruj **QueueTrigger** ustawienia, takie jak maksymalna liczba usuwania z kolejki.
* Pobierz nazwy kolejki z konfiguracji.

### <a name="set-sdk-connection-strings-in-code"></a>Ustawianie parametrów połączenia SDK w kodzie
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

### <a name="configure-queuetrigger--settings"></a>Skonfiguruj ustawienia QueueTrigger
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

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a>Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie
Czasami trzeba toospecify nazwę kolejki, nazwa obiektu blob lub kontener lub tabeli nazw w kodzie, a nie kodowane. Na przykład może być nazwę kolejki hello toospecify **QueueTrigger** w zmiennej środowisku i pliku konfiguracji.

Możesz to zrobić przez przekazywanie **NameResolver** obiekt toohello **JobHostConfiguration** typu. Obejmują specjalne symbole zastępcze ujęta w znaki procentu (%) w parametrach konstruktora atrybut zestaw SDK zadań Webjob i **NameResolver** kodu określa toobe wartości rzeczywistych hello używany zamiast te symbole zastępcze.

Na przykład załóżmy, że chcesz toouse kolejki o nazwie logqueuetest w środowisku testowym hello i jedną o nazwie logqueueprod w środowisku produkcyjnym. Zamiast nazwę kolejki ustalony ma nazwę hello toospecify wpis w hello **appSettings** kolekcji mające hello nazwa rzeczywista kolejki. Jeśli hello **appSettings** klucz jest logqueue, funkcja może wyglądać hello poniższy przykład.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Twoje **NameResolver** klasy, można uzyskać nazwy kolejki hello z **appSettings** pokazane na powitania poniższy przykład:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Przekaż hello **NameResolver** klasy w toohello **JobHost** obiektów, jak pokazano w hello poniższy przykład.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Uwaga:** nazwy obiektów blob, tabel i kolejki rozwiązywane są zawsze funkcja jest nazywana, ale nazwy kontenera obiektów blob są rozpoznawane tylko wtedy, gdy uruchamiana jest aplikacja hello. Nie można zmienić nazwy kontenera obiektów blob, gdy jest wykonywane zadanie hello.

## <a name="how-tootrigger-a-function-manually"></a>Jak tootrigger funkcji ręcznie
tootrigger funkcję ręcznie, użyj hello **wywołać** lub **CallAsync** metody na powitania **JobHost** obiekt i hello **NoAutomaticTrigger** atrybut na powitania funkcji, jak pokazano w hello poniższy przykład.

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

## <a name="how-toowrite-logs"></a>Sposób rejestrowania toowrite
Witaj pulpitu nawigacyjnego przedstawia dzienniki w dwóch miejscach: hello stronę hello zadania WebJob i hello strony dla poszczególnych wywołań zadania WebJob.

![Dzienniki na stronie zadania WebJob](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Dzienniki na stronie wywołania funkcji](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Dane wyjściowe z konsoli metody, które należy wywołać funkcję lub hello **Main()** metoda pojawia się na stronie pulpitu nawigacyjnego hello na powitania zadania WebJob, nie na stronie powitania dla wywołania metody określonej. Na stronie pulpitu nawigacyjnego hello wywołania metody zostaną wyświetlone dane wyjściowe z hello TextWriter obiektu, który można pobrać z parametrem w podpisie metody.

Dane wyjściowe konsoli nie może być wywołanie metody określonej tooa połączonej, ponieważ hello konsoli jest pojedynczym wątku, podczas gdy wiele funkcji zadanie może działać na powitania tym samym czasie. Dlatego hello SDK udostępnia każde wywołanie funkcji z własnego obiektu zapisującego unikatowy dziennika.

toowrite [dzienniki śledzenia aplikacji](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), użyj **Console.Out** (tworzy Dzienniki oznaczone jako informacje) i **Console.Error** (tworzy Dzienniki oznaczone jako błąd). Alternatywą jest toouse [śledzenia lub TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), która zapewnia pełne, ostrzeżenie, i krytyczne poziomy tooInfo dodanie i błąd. Dzienniki śledzenia aplikacji są wyświetlane w plikach dziennika aplikacji sieci web hello, tabelach platformy Azure lub w zależności od sposobu skonfigurowania aplikacji sieci web platformy Azure obiektów blob Azure. Jak wszystkie dane wyjściowe konsoli, najnowsze dzienniki 100 aplikacji hello również zostać wyświetlony na stronie pulpitu nawigacyjnego hello na powitania zadania WebJob, nie hello strony dla wywołania funkcji.

Dane wyjściowe konsoli zostanie wyświetlony w hello pulpitu nawigacyjnego tylko wtedy, gdy hello program działa w zadań WebJob Azure, nie, jeśli hello program działa lokalnie lub w niektórych innych środowiska.

Rejestrowanie można wyłączyć, ustawiając toonull ciąg połączenia pulpitu nawigacyjnego hello. Aby uzyskać więcej informacji, zobacz [jak tooset opcje konfiguracji](#how-to-set-configuration-options).

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

W hello pulpitu nawigacyjnego zestawu SDK zadań Webjob hello dane wyjściowe hello **TextWriter** pokazuje się po przejściu do strony toohello dla określonego wywołania funkcji i wybierz obiektów **dane wyjściowe Przełącz**:

![Łącze wywołania](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Dzienniki na stronie wywołania funkcji](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

W hello pulpitu nawigacyjnego zestawu SDK zadań Webjob hello najnowszych 100 wierszy konsoli output Pokaż się po stronie toohello hello zadania WebJob (a nie dla wywołania funkcji hello) wybierz **dane wyjściowe Przełącz**.

![Przełącz danych wyjściowych](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

Ciągłe zadanie WebJob Dzienniki aplikacji wyświetlani w/data/zadania/ciągłego/*{webjobname}*/job_log.txt w systemie plików aplikacji hello w sieci web.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

W aplikacji hello obiektów blob platformy Azure dzienniki wyglądać następująco: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write — Witaj świecie! w, 2014-09-26T21:01:13, błąd, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.error — Witaj świecie!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out — Witaj świecie!,

W tabeli platformy Azure hello **Console.Out** i **Console.Error** dzienniki wyglądać następująco:

![Dziennik informacyjny w tabeli](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Dziennik błędów w tabeli](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a>Następne kroki
W tym artykule dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z kolejek platformy Azure. Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).

