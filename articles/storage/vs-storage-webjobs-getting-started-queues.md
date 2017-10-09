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
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="f12d0-103">Rozpoczynanie pracy z magazynem kolejek Azure i programu Visual Studio połączone usługi (zadania WebJob projekty)</span><span class="sxs-lookup"><span data-stu-id="f12d0-103">Getting started with Azure Queue storage and Visual Studio connected services (WebJob Projects)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="f12d0-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f12d0-104">Overview</span></span>
<span data-ttu-id="f12d0-105">W tym artykule opisano sposób uzyskać uruchomić za pomocą kolejek Azure hello magazynu w projekcie zadania programu Visual Studio Azure WebJob po utworzony lub odwołanie do konta magazynu platformy Azure przy użyciu programu Visual Studio **dodać usług połączonych** — okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f12d0-105">This article describes how get started using Azure Queue storage in a Visual Studio Azure WebJob project after you have created or referenced an Azure storage account by using hello Visual Studio  **Add Connected Services** dialog box.</span></span> <span data-ttu-id="f12d0-106">Po dodaniu projektu zadania WebJob tooa konto magazynu przy użyciu programu Visual Studio hello **dodać usług połączonych** okna dialogowego, hello odpowiednie pakiety NuGet magazynu Azure są zainstalowane, hello odpowiednie .NET odwołania są dodane toohello Projekt i parametry połączenia dla konta magazynu hello są aktualizowane w pliku App.config hello.</span><span class="sxs-lookup"><span data-stu-id="f12d0-106">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet packages are installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>  

<span data-ttu-id="f12d0-107">Ten artykuł zawiera C# przykłady pokazujące, jak toouse hello zestawu SDK zadań Webjob Azure w wersji 1.x z hello usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="f12d0-107">This article provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure Queue storage service.</span></span>

<span data-ttu-id="f12d0-108">Magazyn kolejek Azure to usługa do przechowywania dużej liczby komunikatów, które można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem uwierzytelnionego połączenia za pomocą protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f12d0-108">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="f12d0-109">Pojedynczy komunikat z kolejki można się too64 KB, rozmiar, a kolejka może zawierać miliony komunikatów w górę toohello całkowitego limitu pojemności konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-109">A single queue message can be up too64 KB in size, and a queue can contain millions of messages, up toohello total capacity limit of a storage account.</span></span> <span data-ttu-id="f12d0-110">Zobacz [Rozpoczynanie pracy z magazynem kolejek Azure przy użyciu platformy .NET](storage-dotnet-how-to-use-queues.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f12d0-110">See [Get started with Azure Queue Storage using .NET](storage-dotnet-how-to-use-queues.md) for more information.</span></span> <span data-ttu-id="f12d0-111">Aby uzyskać więcej informacji na temat platformy ASP.NET, zobacz [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="f12d0-111">For more information about ASP.NET, see [ASP.NET](http://www.asp.net).</span></span>

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a><span data-ttu-id="f12d0-112">Jak tootrigger funkcja po odebraniu komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="f12d0-112">How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="f12d0-113">wywołuje funkcję hello zestaw SDK zadań Webjob toowrite po odebraniu komunikatu w kolejce, użyj hello **QueueTrigger** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-113">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello **QueueTrigger** attribute.</span></span> <span data-ttu-id="f12d0-114">Konstruktor atrybutu Hello przyjmuje parametr ciąg określający nazwę hello hello toopoll kolejki.</span><span class="sxs-lookup"><span data-stu-id="f12d0-114">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="f12d0-115">toosee jak tooset hello Nazwa kolejki dynamicznie, zapoznaj się z [jak tooset opcje konfiguracji](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="f12d0-115">toosee how tooset hello queue name dynamically, check out [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="f12d0-116">Ciąg wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="f12d0-116">String queue messages</span></span>
<span data-ttu-id="f12d0-117">W hello poniższy przykład, kolejki hello zawiera komunikat, więc **QueueTrigger** jest stosowane tooa parametr ciągu o nazwie **logMessage** zawierającą hello zawartość hello kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f12d0-117">In hello following example, hello queue contains a string message, so **QueueTrigger** is applied tooa string parameter named **logMessage** which contains hello content of hello queue message.</span></span> <span data-ttu-id="f12d0-118">Witaj funkcja [zapisuje dziennik komunikatów toohello pulpitu nawigacyjnego](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="f12d0-118">hello function [writes a log message toohello Dashboard](#how-to-write-logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="f12d0-119">Oprócz **ciąg**, parametr hello może być tablicą bajtów **CloudQueueMessage** obiektu lub POCO, które należy zdefiniować.</span><span class="sxs-lookup"><span data-stu-id="f12d0-119">Besides **string**, hello parameter may be a byte array, a **CloudQueueMessage** object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="f12d0-120">POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="f12d0-120">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="f12d0-121">Poniższy przykład hello, komunikatu w kolejce hello zawiera JSON dla **BlobInformation** obiektu, który zawiera **element BlobName** właściwości.</span><span class="sxs-lookup"><span data-stu-id="f12d0-121">In hello following example, hello queue message contains JSON for a **BlobInformation** object which includes a **BlobName** property.</span></span> <span data-ttu-id="f12d0-122">Witaj SDK automatycznie deserializuje obiekt hello.</span><span class="sxs-lookup"><span data-stu-id="f12d0-122">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="f12d0-123">Witaj SDK używa hello [pakietu Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize i deserializować wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f12d0-123">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="f12d0-124">Wiadomości w kolejce w przypadku utworzenia w programie, który nie używa hello zestaw SDK zadań Webjob, można napisać kod, takich jak powitania po toocreate przykład komunikatu w kolejce POCO powitalne tego zestawu SDK można przeanalizować.</span><span class="sxs-lookup"><span data-stu-id="f12d0-124">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="f12d0-125">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="f12d0-125">Async functions</span></span>
<span data-ttu-id="f12d0-126">Witaj następujących funkcji asynchronicznej [zapisuje dziennik toohello pulpitu nawigacyjnego](#how-to-write-logs).</span><span class="sxs-lookup"><span data-stu-id="f12d0-126">hello following async function [writes a log toohello Dashboard](#how-to-write-logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="f12d0-127">Funkcje asynchroniczne może potrwać [token anulowania](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), jak pokazano w hello poniższy przykład, który kopiuje obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f12d0-127">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="f12d0-128">(Aby uzyskać informacje o hello **queueTrigger** symbolu zastępczego, zobacz hello [obiekty BLOB](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) sekcji.)</span><span class="sxs-lookup"><span data-stu-id="f12d0-128">(For an explanation of hello **queueTrigger** placeholder, see hello [Blobs](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a><span data-ttu-id="f12d0-129">Atrybut QueueTrigger hello typy współpracuje z</span><span class="sxs-lookup"><span data-stu-id="f12d0-129">Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="f12d0-130">Można użyć **QueueTrigger** z hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="f12d0-130">You can use **QueueTrigger** with hello following types:</span></span>

* <span data-ttu-id="f12d0-131">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="f12d0-131">**string**</span></span>
* <span data-ttu-id="f12d0-132">Typ POCO zserializowanym w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="f12d0-132">A POCO type serialized as JSON</span></span>
* <span data-ttu-id="f12d0-133">**Byte]**</span><span class="sxs-lookup"><span data-stu-id="f12d0-133">**byte[]**</span></span>
* <span data-ttu-id="f12d0-134">**CloudQueueMessage**</span><span class="sxs-lookup"><span data-stu-id="f12d0-134">**CloudQueueMessage**</span></span>

## <a name="polling-algorithm"></a><span data-ttu-id="f12d0-135">Algorytm sondowania</span><span class="sxs-lookup"><span data-stu-id="f12d0-135">Polling algorithm</span></span>
<span data-ttu-id="f12d0-136">Witaj SDK implementuje efekt losowe wykładniczego wycofywania algorytmu tooreduce hello bezczynności-kolejki sondowania kosztów transakcji magazynu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-136">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="f12d0-137">Po znalezieniu wiadomość hello SDK oczekuje dwóch sekund i następnie wyszukuje kolejną wiadomość; gdy zostanie znaleziony żaden komunikat czeka około czterech sekund przed ponowną próbą.</span><span class="sxs-lookup"><span data-stu-id="f12d0-137">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="f12d0-138">Po kolejnych nieudanych prób tooget komunikatu w kolejce, czas oczekiwania hello nadal tooincrease dopóki nie osiągnie hello maksymalny czas oczekiwania, które minutę tooone wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="f12d0-138">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="f12d0-139">[Witaj maksymalny czas oczekiwania jest konfigurowalne](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="f12d0-139">[hello maximum wait time is configurable](#how-to-set-configuration-options).</span></span>

## <a name="multiple-instances"></a><span data-ttu-id="f12d0-140">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="f12d0-140">Multiple instances</span></span>
<span data-ttu-id="f12d0-141">Jeśli aplikacja sieci web jest uruchamiana na wiele wystąpień, ciągłe zadania Webjob działa na każdym komputerze, a każda maszyna zostanie poczekaj, aż usługa wyzwalaczy i podejmować toorun funkcji.</span><span class="sxs-lookup"><span data-stu-id="f12d0-141">If your web app runs on multiple instances, a continuous WebJobs runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="f12d0-142">W niektórych scenariuszach, które może to spowodować funkcje toosome przetwarzania hello tych samych danych dwa razy, więc funkcje powinno być idempotentności (zapisany, który je wielokrotnie wywołuje z tymi samymi danymi wejściowymi nie tworzy powitalne Duplikuj wyniki).</span><span class="sxs-lookup"><span data-stu-id="f12d0-142">In some scenarios this can lead toosome functions processing hello same data twice, so functions should be idempotent (written so that calling them repeatedly with hello same input data doesn't produce duplicate results).</span></span>  

## <a name="parallel-execution"></a><span data-ttu-id="f12d0-143">Wykonywanie równoległe</span><span class="sxs-lookup"><span data-stu-id="f12d0-143">Parallel execution</span></span>
<span data-ttu-id="f12d0-144">Jeśli masz wiele funkcji nasłuchiwanie w kolejkach różnych hello SDK wywoła je równolegle po odebraniu wiadomości jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="f12d0-144">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="f12d0-145">Witaj samo dotyczy po odebraniu wiele komunikatów dla pojedynczej kolejki.</span><span class="sxs-lookup"><span data-stu-id="f12d0-145">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="f12d0-146">Domyślnie hello SDK pobiera partii 16 wiadomości w kolejce w czasie i wykonuje hello funkcja, która przetwarza je równolegle.</span><span class="sxs-lookup"><span data-stu-id="f12d0-146">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="f12d0-147">[rozmiar partii Hello jest konfigurowalne](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="f12d0-147">[hello batch size is configurable](#how-to-set-configuration-options).</span></span> <span data-ttu-id="f12d0-148">Gdy numer hello przetwarzanych pobiera dół toohalf rozmiar partii hello, hello SDK pobiera inna partia i rozpoczyna przetwarzanie tych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f12d0-148">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="f12d0-149">W związku z tym hello maksymalną liczbę równoczesnych komunikatów przetwarzanych dla każdej funkcji jest rozmiar partii hello co oraz wielokrotności.</span><span class="sxs-lookup"><span data-stu-id="f12d0-149">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="f12d0-150">Ten limit dotyczy oddzielnie tooeach funkcja, która ma **QueueTrigger** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-150">This limit applies separately tooeach function that has a **QueueTrigger** attribute.</span></span> <span data-ttu-id="f12d0-151">Jeśli nie chcesz wykonywanie równoległe dla wiadomości otrzymanych w jednej kolejki, należy ustawić too1 rozmiar partii hello.</span><span class="sxs-lookup"><span data-stu-id="f12d0-151">If you don't want parallel execution for messages received on one queue, set hello batch size too1.</span></span>

## <a name="get-queue-or-queue-message-metadata"></a><span data-ttu-id="f12d0-152">Pobierz kolejki lub kolejka komunikatów metadanych</span><span class="sxs-lookup"><span data-stu-id="f12d0-152">Get queue or queue message metadata</span></span>
<span data-ttu-id="f12d0-153">Możesz uzyskać hello następujące właściwości wiadomości przez dodanie podpis metody toohello parametry:</span><span class="sxs-lookup"><span data-stu-id="f12d0-153">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="f12d0-154">**DateTimeOffset** expirationTime</span><span class="sxs-lookup"><span data-stu-id="f12d0-154">**DateTimeOffset** expirationTime</span></span>
* <span data-ttu-id="f12d0-155">**DateTimeOffset** insertionTime</span><span class="sxs-lookup"><span data-stu-id="f12d0-155">**DateTimeOffset** insertionTime</span></span>
* <span data-ttu-id="f12d0-156">**DateTimeOffset** nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="f12d0-156">**DateTimeOffset** nextVisibleTime</span></span>
* <span data-ttu-id="f12d0-157">**ciąg** queueTrigger (zawiera tekst wiadomości)</span><span class="sxs-lookup"><span data-stu-id="f12d0-157">**string** queueTrigger (contains message text)</span></span>
* <span data-ttu-id="f12d0-158">**ciąg** id</span><span class="sxs-lookup"><span data-stu-id="f12d0-158">**string** id</span></span>
* <span data-ttu-id="f12d0-159">**ciąg** elementu popReceipt</span><span class="sxs-lookup"><span data-stu-id="f12d0-159">**string** popReceipt</span></span>
* <span data-ttu-id="f12d0-160">**int** dequeueCount</span><span class="sxs-lookup"><span data-stu-id="f12d0-160">**int** dequeueCount</span></span>

<span data-ttu-id="f12d0-161">Jeśli chcesz toowork bezpośrednio z hello interfejsu API magazynu Azure, możesz także dodać **CloudStorageAccount** parametru.</span><span class="sxs-lookup"><span data-stu-id="f12d0-161">If you want toowork directly with hello Azure storage API, you can also add a **CloudStorageAccount** parameter.</span></span>

<span data-ttu-id="f12d0-162">Witaj poniższy przykład zapisuje wszystkie ten dziennik metadanych tooan informacje o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f12d0-162">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="f12d0-163">Przykład Witaj zarówno logMessage i queueTrigger zawartością hello hello kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f12d0-163">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="f12d0-164">Poniżej przedstawiono przykładowy dziennik napisane przez hello przykładowy kod:</span><span class="sxs-lookup"><span data-stu-id="f12d0-164">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a><span data-ttu-id="f12d0-165">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="f12d0-165">Graceful shutdown</span></span>
<span data-ttu-id="f12d0-166">Funkcja, która działa w ciągłego zadania WebJob może akceptować **CancellationToken** parametr, który umożliwia hello systemu operacyjnego toonotify hello funkcji hello zadania WebJob dotyczy toobe zakończone.</span><span class="sxs-lookup"><span data-stu-id="f12d0-166">A function that runs in a continuous WebJob can accept a **CancellationToken** parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="f12d0-167">Możesz użyć tego toomake powiadomień, się, że funkcja hello nie nieoczekiwane zakończenie w sposób powodujący, że dane w niespójnym stanie.</span><span class="sxs-lookup"><span data-stu-id="f12d0-167">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="f12d0-168">powitania po przykładzie pokazano, jak toocheck zbliżającym się zakończenia zadania WebJob w funkcji.</span><span class="sxs-lookup"><span data-stu-id="f12d0-168">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="f12d0-169">**Uwaga:** hello pulpit nawigacyjny może nie poprawnie pokazać hello stan i dane wyjściowe funkcji, które została zamknięta.</span><span class="sxs-lookup"><span data-stu-id="f12d0-169">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="f12d0-170">Aby uzyskać więcej informacji, zobacz [łagodne zamykanie zadań Webjob](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="f12d0-170">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a><span data-ttu-id="f12d0-171">Jak toocreate kolejki komunikatów podczas przetwarzania komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="f12d0-171">How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="f12d0-172">toowrite funkcję, która tworzy nowy komunikat kolejki, użyj hello **kolejki** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-172">toowrite a function that creates a new queue message, use hello **Queue** attribute.</span></span> <span data-ttu-id="f12d0-173">Podobnie jak **QueueTrigger**, podaj nazwę kolejki hello jako ciąg lub możesz [Ustaw nazwę kolejki hello dynamicznie](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="f12d0-173">Like **QueueTrigger**, you pass in hello queue name as a string or you can [set hello queue name dynamically](#how-to-set-configuration-options).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="f12d0-174">Ciąg wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="f12d0-174">String queue messages</span></span>
<span data-ttu-id="f12d0-175">powitania po przykładowy kod z systemem innym niż async tworzy nowego komunikatu w kolejce w kolejce hello o nazwie "outputqueue" z hello sama zawartość jako hello kolejki wiadomości odebrane w kolejce hello o nazwie "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="f12d0-175">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="f12d0-176">(Asynchroniczne Użyj funkcji **IAsyncCollector<T>**  opisane dalej w tej sekcji.)</span><span class="sxs-lookup"><span data-stu-id="f12d0-176">(For async functions use **IAsyncCollector<T>** as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="f12d0-177">POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="f12d0-177">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="f12d0-178">toocreate komunikat z kolejki zawiera POCO niż ciąg hello przebiegu POCO typu jako dane wyjściowe parametru toohello **kolejki** atrybut konstruktora.</span><span class="sxs-lookup"><span data-stu-id="f12d0-178">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello **Queue** attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="f12d0-179">Witaj SDK automatycznie serializuje hello tooJSON obiektu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-179">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="f12d0-180">Komunikatu w kolejce zawsze jest tworzony, nawet jeśli obiekt hello jest pusty.</span><span class="sxs-lookup"><span data-stu-id="f12d0-180">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="f12d0-181">Tworzenie wielu wiadomości lub w funkcji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="f12d0-181">Create multiple messages or in async functions</span></span>
<span data-ttu-id="f12d0-182">toocreate wiele komunikatów upewnij hello typu parametru dla kolejki wyjściowej hello **ICollector<T>**  lub **IAsyncCollector<T>**, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f12d0-182">toocreate multiple messages, make hello parameter type for hello output queue **ICollector<T>** or **IAsyncCollector<T>**, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="f12d0-183">Każdy komunikat kolejki jest tworzony natychmiast po hello **Dodaj** metoda jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="f12d0-183">Each queue message is created immediately when hello **Add** method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="f12d0-184">Typy atrybutu kolejki hello współpracuje z</span><span class="sxs-lookup"><span data-stu-id="f12d0-184">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="f12d0-185">Można użyć hello **kolejki** atrybutu na powitania następujące typy parametrów:</span><span class="sxs-lookup"><span data-stu-id="f12d0-185">You can use hello **Queue** attribute on hello following parameter types:</span></span>

* <span data-ttu-id="f12d0-186">**limit ciąg** (tworzy komunikat z kolejki, jeśli wartość parametru jest różna od null, gdy funkcja hello kończy się)</span><span class="sxs-lookup"><span data-stu-id="f12d0-186">**out string** (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="f12d0-187">**limit byte []** (takich jak działa **ciąg**)</span><span class="sxs-lookup"><span data-stu-id="f12d0-187">**out byte[]** (works like **string**)</span></span>
* <span data-ttu-id="f12d0-188">**limit CloudQueueMessage** (takich jak działa **ciąg**)</span><span class="sxs-lookup"><span data-stu-id="f12d0-188">**out CloudQueueMessage** (works like **string**)</span></span>
* <span data-ttu-id="f12d0-189">**limit POCO** (typ możliwy do serializacji, tworzy komunikat z obiektem null, jeśli parametru hello ma wartość null, gdy funkcja hello kończy się)</span><span class="sxs-lookup"><span data-stu-id="f12d0-189">**out POCO** (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* <span data-ttu-id="f12d0-190">**ICollector**</span><span class="sxs-lookup"><span data-stu-id="f12d0-190">**ICollector**</span></span>
* <span data-ttu-id="f12d0-191">**IAsyncCollector**</span><span class="sxs-lookup"><span data-stu-id="f12d0-191">**IAsyncCollector**</span></span>
* <span data-ttu-id="f12d0-192">**CloudQueue** (do tworzenia komunikatów ręcznie przy użyciu hello interfejsu API magazynu Azure bezpośrednio)</span><span class="sxs-lookup"><span data-stu-id="f12d0-192">**CloudQueue** (for creating messages manually using hello Azure Storage API directly)</span></span>

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a><span data-ttu-id="f12d0-193">Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji</span><span class="sxs-lookup"><span data-stu-id="f12d0-193">Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="f12d0-194">Jeśli potrzebujesz toodo niektóre działają w funkcji przed przy użyciu atrybutu zestaw SDK zadań Webjob, takich jak **kolejki**, **obiektu Blob**, lub **tabeli**, można użyć hello **IBinder** interfejsu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-194">If you need toodo some work in your function before using a WebJobs SDK attribute such as **Queue**, **Blob**, or **Table**, you can use hello **IBinder** interface.</span></span>

<span data-ttu-id="f12d0-195">Poniższy przykład Hello pobiera wiadomość z kolejki wejściowej i tworzy nowy komunikat o tej samej zawartości w kolejki wyjściowej hello.</span><span class="sxs-lookup"><span data-stu-id="f12d0-195">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="f12d0-196">Nazwa kolejki danych wyjściowych Hello jest ustawiana przez kod w treści hello hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="f12d0-196">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="f12d0-197">Witaj **IBinder** interfejsu można również z hello **tabeli** i **obiektu Blob** atrybutów.</span><span class="sxs-lookup"><span data-stu-id="f12d0-197">hello **IBinder** interface can also be used with hello **Table** and **Blob** attributes.</span></span>

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a><span data-ttu-id="f12d0-198">Jak tooread i zapisu obiektów blob i tabelach podczas przetwarzania komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="f12d0-198">How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="f12d0-199">Witaj **obiektu Blob** i **tabeli** atrybutów umożliwiają tooread i zapisywać obiekty BLOB i tabelach.</span><span class="sxs-lookup"><span data-stu-id="f12d0-199">hello **Blob** and **Table** attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="f12d0-200">Witaj próbek w tej sekcji mają zastosowanie tooblobs.</span><span class="sxs-lookup"><span data-stu-id="f12d0-200">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="f12d0-201">Aby uzyskać przykłady kodu, które pokazują, jak tootrigger przetwarza podczas tworzenia lub aktualizowania obiektów blob, zobacz [jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)oraz przykłady kodu, do odczytu i zapisu tabel, zobacz [jak toouse tabeli platformy Azure Magazyn z hello zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="f12d0-201">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="f12d0-202">Ciąg wiadomości w kolejce wyzwalania operacje obiektów blob</span><span class="sxs-lookup"><span data-stu-id="f12d0-202">String queue messages triggering blob operations</span></span>
<span data-ttu-id="f12d0-203">Dla komunikatu w kolejce, który zawiera ciąg **queueTrigger** to symbol zastępczy, można użyć w hello **obiektu Blob** atrybutu **blobPath** parametr, który zawiera zawartość hello wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="f12d0-203">For a queue message that contains a string, **queueTrigger** is a placeholder you can use in hello **Blob** attribute's **blobPath** parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="f12d0-204">Witaj poniższym przykładzie użyto **strumienia** obiekty BLOB tooread i zapisu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-204">hello following example uses **Stream** objects tooread and write blobs.</span></span> <span data-ttu-id="f12d0-205">komunikat z kolejki Hello jest hello nazwa obiektu blob znajdujących się w kontenerze textblobs hello.</span><span class="sxs-lookup"><span data-stu-id="f12d0-205">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="f12d0-206">Kopiowania obiektu blob hello z "-nowych" Nazwa toohello dołączany jest tworzony w hello sam kontenera.</span><span class="sxs-lookup"><span data-stu-id="f12d0-206">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="f12d0-207">Witaj **obiektów Blob** atrybutu ma konstruktora **blobPath** parametr, który określa kontener hello i nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f12d0-207">hello **Blob** attribute constructor takes a **blobPath** parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="f12d0-208">Aby uzyskać więcej informacji dotyczących tego symbolu zastępczego, zobacz [jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="f12d0-208">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).</span></span>

<span data-ttu-id="f12d0-209">Gdy atrybut hello decorates **strumienia** obiekt inny parametr konstruktora określa hello **FileAccess** trybie odczytu, zapisu lub odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-209">When hello attribute decorates a **Stream** object, another constructor parameter specifies hello **FileAccess** mode as read, write, or read/write.</span></span>

<span data-ttu-id="f12d0-210">Witaj poniższym przykładzie użyto **CloudBlockBlob** obiekt toodelete obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f12d0-210">hello following example uses a **CloudBlockBlob** object toodelete a blob.</span></span> <span data-ttu-id="f12d0-211">komunikat z kolejki Hello jest nazwą hello hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f12d0-211">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="f12d0-212">POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="f12d0-212">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="f12d0-213">POCO, zapisane w formacie JSON hello kolejki wiadomości, można użyć zastępcze nazw właściwości obiektu hello w hello **kolejki** atrybutu **blobPath** parametru.</span><span class="sxs-lookup"><span data-stu-id="f12d0-213">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello **Queue** attribute's **blobPath** parameter.</span></span> <span data-ttu-id="f12d0-214">Nazwy właściwości metadanych kolejki służy również jako symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="f12d0-214">You can also use queue metadata property names as placeholders.</span></span> <span data-ttu-id="f12d0-215">Zobacz [uzyskać kolejki lub kolejka komunikatów metadanych](#get-queue-or-queue-message-metadata).</span><span class="sxs-lookup"><span data-stu-id="f12d0-215">See [Get queue or queue message metadata](#get-queue-or-queue-message-metadata).</span></span>

<span data-ttu-id="f12d0-216">Witaj Poniższy przykładowy kod kopiuje obiekt blob tooa nowego obiektu blob z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="f12d0-216">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="f12d0-217">komunikat z kolejki Hello jest **BlobInformation** obiekt, który zawiera **element BlobName** i **BlobNameWithoutExtension** właściwości.</span><span class="sxs-lookup"><span data-stu-id="f12d0-217">hello queue message is a **BlobInformation** object that includes **BlobName** and **BlobNameWithoutExtension** properties.</span></span> <span data-ttu-id="f12d0-218">nazwy właściwości Hello są używane jako symbole zastępcze w ścieżce obiektu blob hello hello **obiektu Blob** atrybutów.</span><span class="sxs-lookup"><span data-stu-id="f12d0-218">hello property names are used as placeholders in hello blob path for hello **Blob** attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="f12d0-219">Witaj SDK używa hello [pakietu Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize i deserializować wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f12d0-219">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="f12d0-220">Wiadomości w kolejce w przypadku utworzenia w programie, który nie używa hello zestaw SDK zadań Webjob, można napisać kod, takich jak powitania po toocreate przykład komunikatu w kolejce POCO powitalne tego zestawu SDK można przeanalizować.</span><span class="sxs-lookup"><span data-stu-id="f12d0-220">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="f12d0-221">Jeśli potrzebujesz toodo niektóre działają w funkcji przed powiązania obiektu blob tooan można użyć atrybutu hello w treści hello funkcji hello, jak pokazano w [Użyj zestawu SDK zadań Webjob atrybutów w treści funkcji hello](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span><span class="sxs-lookup"><span data-stu-id="f12d0-221">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, as shown in [Use WebJobs SDK attributes in hello body of a function](#use-webjobs-sdk-attributes-in-the-body-of-a-function).</span></span>

### <a name="types-you-can-use-hello-blob-attribute-with"></a><span data-ttu-id="f12d0-222">Typy, można użyć hello obiektu Blob atrybutu z</span><span class="sxs-lookup"><span data-stu-id="f12d0-222">Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="f12d0-223">Witaj **obiektu Blob** atrybut może być używany z hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="f12d0-223">hello **Blob** attribute can be used with hello following types:</span></span>

* <span data-ttu-id="f12d0-224">**Strumień** (Odczyt lub zapis, określić przy użyciu parametru konstruktora FileAccess hello)</span><span class="sxs-lookup"><span data-stu-id="f12d0-224">**Stream** (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* <span data-ttu-id="f12d0-225">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="f12d0-225">**TextReader**</span></span>
* <span data-ttu-id="f12d0-226">**Element TextWriter**</span><span class="sxs-lookup"><span data-stu-id="f12d0-226">**TextWriter**</span></span>
* <span data-ttu-id="f12d0-227">**ciąg** (odczyt)</span><span class="sxs-lookup"><span data-stu-id="f12d0-227">**string** (read)</span></span>
* <span data-ttu-id="f12d0-228">**limit ciąg** (zapisu; tworzy obiektu blob tylko wtedy, gdy parametr ciąg hello jest inną niż null, gdy funkcja hello zwraca)</span><span class="sxs-lookup"><span data-stu-id="f12d0-228">**out string** (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="f12d0-229">POCO (odczyt)</span><span class="sxs-lookup"><span data-stu-id="f12d0-229">POCO (read)</span></span>
* <span data-ttu-id="f12d0-230">limit POCO (zapisu; zawsze tworzy obiektu blob, tworzy jako obiekt null, jeśli parametr POCO ma wartość null, gdy funkcja hello zwraca)</span><span class="sxs-lookup"><span data-stu-id="f12d0-230">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="f12d0-231">**CloudBlobStream** (zapis)</span><span class="sxs-lookup"><span data-stu-id="f12d0-231">**CloudBlobStream** (write)</span></span>
* <span data-ttu-id="f12d0-232">**ICloudBlob** (odczytu i zapisu)</span><span class="sxs-lookup"><span data-stu-id="f12d0-232">**ICloudBlob** (read or write)</span></span>
* <span data-ttu-id="f12d0-233">**CloudBlockBlob** (odczytu i zapisu)</span><span class="sxs-lookup"><span data-stu-id="f12d0-233">**CloudBlockBlob** (read or write)</span></span>
* <span data-ttu-id="f12d0-234">**CloudPageBlob** (odczytu i zapisu)</span><span class="sxs-lookup"><span data-stu-id="f12d0-234">**CloudPageBlob** (read or write)</span></span>

## <a name="how-toohandle-poison-messages"></a><span data-ttu-id="f12d0-235">Jak toohandle zanieczyszczonych komunikatów</span><span class="sxs-lookup"><span data-stu-id="f12d0-235">How toohandle poison messages</span></span>
<span data-ttu-id="f12d0-236">Komunikaty, których zawartość powoduje toofail funkcji są nazywane *zanieczyszczonych komunikatów*.</span><span class="sxs-lookup"><span data-stu-id="f12d0-236">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="f12d0-237">W przypadku awarii funkcja hello hello kolejki wiadomości nie zostanie usunięta i ostatecznie zostaje pobrana ponownie, powodując toobe cyklu hello powtarzany.</span><span class="sxs-lookup"><span data-stu-id="f12d0-237">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="f12d0-238">Hello SDK automatycznie może przerwać cyklu powitania po ograniczonej liczby iteracji, lub możesz zrobić to ręcznie.</span><span class="sxs-lookup"><span data-stu-id="f12d0-238">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="f12d0-239">Obsługa automatycznego Trująca wiadomość</span><span class="sxs-lookup"><span data-stu-id="f12d0-239">Automatic poison message handling</span></span>
<span data-ttu-id="f12d0-240">Hello zestawu SDK wywoła funkcję się too5 razy tooprocess komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="f12d0-240">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="f12d0-241">W przypadku niepowodzenia spróbuj piątym powitania wiadomość hello jest przeniesionego tooa skażone kolejki.</span><span class="sxs-lookup"><span data-stu-id="f12d0-241">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="f12d0-242">Zobacz temat jak tooconfigure hello maksymalnej liczby ponownych prób w [jak opcje konfiguracji tooset](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="f12d0-242">You can see how tooconfigure hello maximum number of retries in [How tooset configuration options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="f12d0-243">nosi nazwę kolejki skażone Hello *{originalqueuename}*-skażone.</span><span class="sxs-lookup"><span data-stu-id="f12d0-243">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="f12d0-244">Można napisać tooprocess funkcji wiadomości z kolejki skażone hello rejestrowania ich lub wysyłania powiadomienia, że wymagana jest ręczne uwagi.</span><span class="sxs-lookup"><span data-stu-id="f12d0-244">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="f12d0-245">W powitania po hello przykład **CopyBlob** funkcja zakończy się niepowodzeniem, gdy komunikatu w kolejce zawiera nazwę hello obiektu blob, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f12d0-245">In hello following example hello **CopyBlob** function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="f12d0-246">W takim przypadku wiadomość hello jest przenoszona z hello copyblobqueue kolejki toohello copyblobqueue poison kolejki.</span><span class="sxs-lookup"><span data-stu-id="f12d0-246">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="f12d0-247">Witaj **ProcessPoisonMessage** , a następnie Trująca wiadomość hello dzienników.</span><span class="sxs-lookup"><span data-stu-id="f12d0-247">hello **ProcessPoisonMessage** then logs hello poison message.</span></span>

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

<span data-ttu-id="f12d0-248">Witaj poniżej przedstawiono dane wyjściowe konsoli z tych funkcji po skażone komunikat jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="f12d0-248">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Dane wyjściowe konsoli dotyczące obsługi uszkodzonych komunikatów](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="f12d0-250">Trująca wiadomość została ręcznej obsługi</span><span class="sxs-lookup"><span data-stu-id="f12d0-250">Manual poison message handling</span></span>
<span data-ttu-id="f12d0-251">Można uzyskać hello liczba wiadomości została pobrana do przetworzenia przez dodanie **int** parametru o nazwie **dequeueCount** tooyour funkcji.</span><span class="sxs-lookup"><span data-stu-id="f12d0-251">You can get hello number of times a message has been picked up for processing by adding an **int** parameter named **dequeueCount** tooyour function.</span></span> <span data-ttu-id="f12d0-252">Mogą być następnie hello wyboru usuwania z kolejki liczby w kodzie funkcji i wykonać własne Trująca wiadomość została obsługa podczas numer hello przekracza próg, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f12d0-252">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

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

## <a name="how-tooset-configuration-options"></a><span data-ttu-id="f12d0-253">Jak tooset opcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f12d0-253">How tooset configuration options</span></span>
<span data-ttu-id="f12d0-254">Można użyć hello **JobHostConfiguration** hello tooset typu następujące opcje konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="f12d0-254">You can use hello **JobHostConfiguration** type tooset hello following configuration options:</span></span>

* <span data-ttu-id="f12d0-255">Ustawianie parametrów połączenia SDK hello w kodzie.</span><span class="sxs-lookup"><span data-stu-id="f12d0-255">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="f12d0-256">Skonfiguruj **QueueTrigger** ustawienia, takie jak maksymalna liczba usuwania z kolejki.</span><span class="sxs-lookup"><span data-stu-id="f12d0-256">Configure **QueueTrigger** settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="f12d0-257">Pobierz nazwy kolejki z konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f12d0-257">Get queue names from configuration.</span></span>

### <a name="set-sdk-connection-strings-in-code"></a><span data-ttu-id="f12d0-258">Ustawianie parametrów połączenia SDK w kodzie</span><span class="sxs-lookup"><span data-stu-id="f12d0-258">Set SDK connection strings in code</span></span>
<span data-ttu-id="f12d0-259">Ustawianie parametrów połączenia SDK hello w kodzie umożliwia toouse możesz własne nazwy ciągu połączenia w plikach konfiguracji lub zmiennych środowiskowych, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f12d0-259">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <a name="configure-queuetrigger--settings"></a><span data-ttu-id="f12d0-260">Skonfiguruj ustawienia QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="f12d0-260">Configure QueueTrigger  settings</span></span>
<span data-ttu-id="f12d0-261">Można skonfigurować następujące ustawienia dotyczące przetwarzania komunikatu w kolejce toohello hello:</span><span class="sxs-lookup"><span data-stu-id="f12d0-261">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="f12d0-262">Maksymalna liczba wiadomości w kolejce, które są pobierane jednocześnie toobe wykonywane równolegle Hello (wartość domyślna to 16).</span><span class="sxs-lookup"><span data-stu-id="f12d0-262">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="f12d0-263">Witaj maksymalnej liczby ponownych prób przed wysłaniem komunikatu w kolejce tooa skażone kolejki (wartość domyślna to 5).</span><span class="sxs-lookup"><span data-stu-id="f12d0-263">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="f12d0-264">Witaj maksymalny czas oczekiwania przed sondowania ponownie, gdy kolejka jest pusta (wartość domyślna to 1 minuta).</span><span class="sxs-lookup"><span data-stu-id="f12d0-264">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="f12d0-265">powitania po przykładzie pokazano, jak tooconfigure te ustawienia:</span><span class="sxs-lookup"><span data-stu-id="f12d0-265">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a><span data-ttu-id="f12d0-266">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="f12d0-266">Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="f12d0-267">Czasami trzeba toospecify nazwę kolejki, nazwa obiektu blob lub kontener lub tabeli nazw w kodzie, a nie kodowane.</span><span class="sxs-lookup"><span data-stu-id="f12d0-267">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="f12d0-268">Na przykład może być nazwę kolejki hello toospecify **QueueTrigger** w zmiennej środowisku i pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f12d0-268">For example, you might want toospecify hello queue name for **QueueTrigger** in a configuration file or environment variable.</span></span>

<span data-ttu-id="f12d0-269">Możesz to zrobić przez przekazywanie **NameResolver** obiekt toohello **JobHostConfiguration** typu.</span><span class="sxs-lookup"><span data-stu-id="f12d0-269">You can do that by passing in a **NameResolver** object toohello **JobHostConfiguration** type.</span></span> <span data-ttu-id="f12d0-270">Obejmują specjalne symbole zastępcze ujęta w znaki procentu (%) w parametrach konstruktora atrybut zestaw SDK zadań Webjob i **NameResolver** kodu określa toobe wartości rzeczywistych hello używany zamiast te symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="f12d0-270">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your **NameResolver** code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="f12d0-271">Na przykład załóżmy, że chcesz toouse kolejki o nazwie logqueuetest w środowisku testowym hello i jedną o nazwie logqueueprod w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="f12d0-271">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="f12d0-272">Zamiast nazwę kolejki ustalony ma nazwę hello toospecify wpis w hello **appSettings** kolekcji mające hello nazwa rzeczywista kolejki.</span><span class="sxs-lookup"><span data-stu-id="f12d0-272">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello **appSettings** collection that would have hello actual queue name.</span></span> <span data-ttu-id="f12d0-273">Jeśli hello **appSettings** klucz jest logqueue, funkcja może wyglądać hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f12d0-273">If hello **appSettings** key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="f12d0-274">Twoje **NameResolver** klasy, można uzyskać nazwy kolejki hello z **appSettings** pokazane na powitania poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f12d0-274">Your **NameResolver** class could then get hello queue name from **appSettings** as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="f12d0-275">Przekaż hello **NameResolver** klasy w toohello **JobHost** obiektów, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f12d0-275">You pass hello **NameResolver** class in toohello **JobHost** object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="f12d0-276">**Uwaga:** nazwy obiektów blob, tabel i kolejki rozwiązywane są zawsze funkcja jest nazywana, ale nazwy kontenera obiektów blob są rozpoznawane tylko wtedy, gdy uruchamiana jest aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="f12d0-276">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="f12d0-277">Nie można zmienić nazwy kontenera obiektów blob, gdy jest wykonywane zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="f12d0-277">You can't change blob container name while hello job is running.</span></span>

## <a name="how-tootrigger-a-function-manually"></a><span data-ttu-id="f12d0-278">Jak tootrigger funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="f12d0-278">How tootrigger a function manually</span></span>
<span data-ttu-id="f12d0-279">tootrigger funkcję ręcznie, użyj hello **wywołać** lub **CallAsync** metody na powitania **JobHost** obiekt i hello **NoAutomaticTrigger** atrybut na powitania funkcji, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="f12d0-279">tootrigger a function manually, use hello **Call** or **CallAsync** method on hello **JobHost** object and hello **NoAutomaticTrigger** attribute on hello function, as shown in hello following example.</span></span>

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

## <a name="how-toowrite-logs"></a><span data-ttu-id="f12d0-280">Sposób rejestrowania toowrite</span><span class="sxs-lookup"><span data-stu-id="f12d0-280">How toowrite logs</span></span>
<span data-ttu-id="f12d0-281">Witaj pulpitu nawigacyjnego przedstawia dzienniki w dwóch miejscach: hello stronę hello zadania WebJob i hello strony dla poszczególnych wywołań zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="f12d0-281">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Dzienniki na stronie zadania WebJob](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Dzienniki na stronie wywołania funkcji](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="f12d0-284">Dane wyjściowe z konsoli metody, które należy wywołać funkcję lub hello **Main()** metoda pojawia się na stronie pulpitu nawigacyjnego hello na powitania zadania WebJob, nie na stronie powitania dla wywołania metody określonej.</span><span class="sxs-lookup"><span data-stu-id="f12d0-284">Output from Console methods that you call in a function or in hello **Main()** method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="f12d0-285">Na stronie pulpitu nawigacyjnego hello wywołania metody zostaną wyświetlone dane wyjściowe z hello TextWriter obiektu, który można pobrać z parametrem w podpisie metody.</span><span class="sxs-lookup"><span data-stu-id="f12d0-285">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="f12d0-286">Dane wyjściowe konsoli nie może być wywołanie metody określonej tooa połączonej, ponieważ hello konsoli jest pojedynczym wątku, podczas gdy wiele funkcji zadanie może działać na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="f12d0-286">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="f12d0-287">Dlatego hello SDK udostępnia każde wywołanie funkcji z własnego obiektu zapisującego unikatowy dziennika.</span><span class="sxs-lookup"><span data-stu-id="f12d0-287">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="f12d0-288">toowrite [dzienniki śledzenia aplikacji](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), użyj **Console.Out** (tworzy Dzienniki oznaczone jako informacje) i **Console.Error** (tworzy Dzienniki oznaczone jako błąd).</span><span class="sxs-lookup"><span data-stu-id="f12d0-288">toowrite [application tracing logs](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use **Console.Out** (creates logs marked as INFO) and **Console.Error** (creates logs marked as ERROR).</span></span> <span data-ttu-id="f12d0-289">Alternatywą jest toouse [śledzenia lub TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), która zapewnia pełne, ostrzeżenie, i krytyczne poziomy tooInfo dodanie i błąd.</span><span class="sxs-lookup"><span data-stu-id="f12d0-289">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="f12d0-290">Dzienniki śledzenia aplikacji są wyświetlane w plikach dziennika aplikacji sieci web hello, tabelach platformy Azure lub w zależności od sposobu skonfigurowania aplikacji sieci web platformy Azure obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f12d0-290">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="f12d0-291">Jak wszystkie dane wyjściowe konsoli, najnowsze dzienniki 100 aplikacji hello również zostać wyświetlony na stronie pulpitu nawigacyjnego hello na powitania zadania WebJob, nie hello strony dla wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="f12d0-291">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="f12d0-292">Dane wyjściowe konsoli zostanie wyświetlony w hello pulpitu nawigacyjnego tylko wtedy, gdy hello program działa w zadań WebJob Azure, nie, jeśli hello program działa lokalnie lub w niektórych innych środowiska.</span><span class="sxs-lookup"><span data-stu-id="f12d0-292">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="f12d0-293">Rejestrowanie można wyłączyć, ustawiając toonull ciąg połączenia pulpitu nawigacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="f12d0-293">You can disable logging by setting hello Dashboard connection string toonull.</span></span> <span data-ttu-id="f12d0-294">Aby uzyskać więcej informacji, zobacz [jak tooset opcje konfiguracji](#how-to-set-configuration-options).</span><span class="sxs-lookup"><span data-stu-id="f12d0-294">For more information, see [How tooset Configuration Options](#how-to-set-configuration-options).</span></span>

<span data-ttu-id="f12d0-295">Witaj poniższym przykładzie pokazano kilka sposobów toowrite dzienników:</span><span class="sxs-lookup"><span data-stu-id="f12d0-295">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="f12d0-296">W hello pulpitu nawigacyjnego zestawu SDK zadań Webjob hello dane wyjściowe hello **TextWriter** pokazuje się po przejściu do strony toohello dla określonego wywołania funkcji i wybierz obiektów **dane wyjściowe Przełącz**:</span><span class="sxs-lookup"><span data-stu-id="f12d0-296">In hello WebJobs SDK Dashboard, hello output from hello **TextWriter** object shows up when you go toohello page for a particular function invocation and select **Toggle Output**:</span></span>

![Łącze wywołania](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Dzienniki na stronie wywołania funkcji](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

<span data-ttu-id="f12d0-299">W hello pulpitu nawigacyjnego zestawu SDK zadań Webjob hello najnowszych 100 wierszy konsoli output Pokaż się po stronie toohello hello zadania WebJob (a nie dla wywołania funkcji hello) wybierz **dane wyjściowe Przełącz**.</span><span class="sxs-lookup"><span data-stu-id="f12d0-299">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and select **Toggle Output**.</span></span>

![Przełącz danych wyjściowych](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

<span data-ttu-id="f12d0-301">Ciągłe zadanie WebJob Dzienniki aplikacji wyświetlani w/data/zadania/ciągłego/*{webjobname}*/job_log.txt w systemie plików aplikacji hello w sieci web.</span><span class="sxs-lookup"><span data-stu-id="f12d0-301">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="f12d0-302">W aplikacji hello obiektów blob platformy Azure dzienniki wyglądać następująco: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write — Witaj świecie! w, 2014-09-26T21:01:13, błąd, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.error — Witaj świecie!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out — Witaj świecie!,</span><span class="sxs-lookup"><span data-stu-id="f12d0-302">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="f12d0-303">W tabeli platformy Azure hello **Console.Out** i **Console.Error** dzienniki wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="f12d0-303">And in an Azure table hello **Console.Out** and **Console.Error** logs look like this:</span></span>

![Dziennik informacyjny w tabeli](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Dziennik błędów w tabeli](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a><span data-ttu-id="f12d0-306">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f12d0-306">Next steps</span></span>
<span data-ttu-id="f12d0-307">W tym artykule dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z kolejek platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f12d0-307">This article has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="f12d0-308">Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="f12d0-308">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

