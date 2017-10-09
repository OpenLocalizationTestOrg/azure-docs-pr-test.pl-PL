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
# <a name="how-toouse-azure-queue-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="7c3e8-104">Jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="7c3e8-104">How toouse Azure queue storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="7c3e8-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7c3e8-105">Overview</span></span>
<span data-ttu-id="7c3e8-106">Ten przewodnik zawiera C# przykłady pokazujące, jak toouse hello zestawu SDK zadań Webjob Azure w wersji 1.x z hello usługi magazynu kolejek Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-106">This guide provides C# code samples that show how toouse hello Azure WebJobs SDK version 1.x with hello Azure queue storage service.</span></span>

<span data-ttu-id="7c3e8-107">Witaj przewodnika przyjęto założenia, wiadomo, [jak toocreate projektu zadania WebJob w programie Visual Studio z połączeniem ciągi konto magazynu punktu tooyour](websites-dotnet-webjobs-sdk-get-started.md) lub zbyt[wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-107">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

<span data-ttu-id="7c3e8-108">Większość fragmentów kodu hello Pokaż tylko funkcje, nie hello kod, który tworzy hello `JobHost` obiektu jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-108">Most of hello code snippets only show functions, not hello code that creates hello `JobHost` object as in this example:</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

<span data-ttu-id="7c3e8-109">Witaj przewodnika hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-109">hello guide includes hello following topics:</span></span>

* [<span data-ttu-id="7c3e8-110">Jak tootrigger funkcja po odebraniu komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-110">How tootrigger a function when a queue message is received</span></span>](#trigger)
  * <span data-ttu-id="7c3e8-111">Ciąg wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-111">String queue messages</span></span>
  * <span data-ttu-id="7c3e8-112">Wiadomości w kolejce POCO</span><span class="sxs-lookup"><span data-stu-id="7c3e8-112">POCO queue messages</span></span>
  * <span data-ttu-id="7c3e8-113">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="7c3e8-113">Async functions</span></span>
  * <span data-ttu-id="7c3e8-114">Atrybut QueueTrigger hello typy współpracuje z</span><span class="sxs-lookup"><span data-stu-id="7c3e8-114">Types hello QueueTrigger attribute works with</span></span>
  * <span data-ttu-id="7c3e8-115">Algorytm sondowania</span><span class="sxs-lookup"><span data-stu-id="7c3e8-115">Polling algorithm</span></span>
  * <span data-ttu-id="7c3e8-116">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="7c3e8-116">Multiple instances</span></span>
  * <span data-ttu-id="7c3e8-117">Wykonywanie równoległe</span><span class="sxs-lookup"><span data-stu-id="7c3e8-117">Parallel execution</span></span>
  * <span data-ttu-id="7c3e8-118">Pobierz kolejki lub kolejka komunikatów metadanych</span><span class="sxs-lookup"><span data-stu-id="7c3e8-118">Get queue or queue message metadata</span></span>
  * <span data-ttu-id="7c3e8-119">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="7c3e8-119">Graceful shutdown</span></span>
* [<span data-ttu-id="7c3e8-120">Jak toocreate kolejki komunikatów podczas przetwarzania komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-120">How toocreate a queue message while processing a queue message</span></span>](#createqueue)
  * <span data-ttu-id="7c3e8-121">Ciąg wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-121">String queue messages</span></span>
  * <span data-ttu-id="7c3e8-122">Wiadomości w kolejce POCO</span><span class="sxs-lookup"><span data-stu-id="7c3e8-122">POCO queue messages</span></span>
  * <span data-ttu-id="7c3e8-123">Tworzenie wielu wiadomości lub w funkcji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="7c3e8-123">Create multiple messages or in async functions</span></span>
  * <span data-ttu-id="7c3e8-124">Atrybut kolejki hello typy współpracuje z</span><span class="sxs-lookup"><span data-stu-id="7c3e8-124">Types hello Queue attribute works with</span></span>
  * <span data-ttu-id="7c3e8-125">Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji</span><span class="sxs-lookup"><span data-stu-id="7c3e8-125">Use WebJobs SDK attributes in hello body of a function</span></span>
* [<span data-ttu-id="7c3e8-126">Jak tooread i zapisu obiektów blob podczas przetwarzania komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-126">How tooread and write blobs while processing a queue message</span></span>](#blobs)
  * <span data-ttu-id="7c3e8-127">Ciąg wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-127">String queue messages</span></span>
  * <span data-ttu-id="7c3e8-128">Wiadomości w kolejce POCO</span><span class="sxs-lookup"><span data-stu-id="7c3e8-128">POCO queue messages</span></span>
  * <span data-ttu-id="7c3e8-129">Typy hello obiektu Blob atrybutu współpracuje z</span><span class="sxs-lookup"><span data-stu-id="7c3e8-129">Types hello Blob attribute works with</span></span>
* [<span data-ttu-id="7c3e8-130">Jak toohandle zanieczyszczonych komunikatów</span><span class="sxs-lookup"><span data-stu-id="7c3e8-130">How toohandle poison messages</span></span>](#poison)
  * <span data-ttu-id="7c3e8-131">Obsługa automatycznego Trująca wiadomość</span><span class="sxs-lookup"><span data-stu-id="7c3e8-131">Automatic poison message handling</span></span>
  * <span data-ttu-id="7c3e8-132">Trująca wiadomość została ręcznej obsługi</span><span class="sxs-lookup"><span data-stu-id="7c3e8-132">Manual poison message handling</span></span>
* [<span data-ttu-id="7c3e8-133">Jak tooset opcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7c3e8-133">How tooset configuration options</span></span>](#config)
  * <span data-ttu-id="7c3e8-134">Ustawianie parametrów połączenia SDK w kodzie</span><span class="sxs-lookup"><span data-stu-id="7c3e8-134">Set SDK connection strings in code</span></span>
  * <span data-ttu-id="7c3e8-135">Skonfiguruj ustawienia QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="7c3e8-135">Configure QueueTrigger settings</span></span>
  * <span data-ttu-id="7c3e8-136">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="7c3e8-136">Set values for WebJobs SDK constructor parameters in code</span></span>
* [<span data-ttu-id="7c3e8-137">Jak tootrigger funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="7c3e8-137">How tootrigger a function manually</span></span>](#manual)
* [<span data-ttu-id="7c3e8-138">Sposób rejestrowania toowrite</span><span class="sxs-lookup"><span data-stu-id="7c3e8-138">How toowrite logs</span></span>](#logs)
* [<span data-ttu-id="7c3e8-139">Jak błędy toohandle i Konfigurowanie limitów czasu</span><span class="sxs-lookup"><span data-stu-id="7c3e8-139">How toohandle errors and configure timeouts</span></span>](#errors)
* [<span data-ttu-id="7c3e8-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c3e8-140">Next steps</span></span>](#nextsteps)

## <span data-ttu-id="7c3e8-141"><a id="trigger"></a>Jak tootrigger funkcja po odebraniu komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-141"><a id="trigger"></a> How tootrigger a function when a queue message is received</span></span>
<span data-ttu-id="7c3e8-142">wywołuje funkcję hello zestaw SDK zadań Webjob toowrite po odebraniu komunikatu w kolejce, użyj hello `QueueTrigger` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-142">toowrite a function that hello WebJobs SDK calls when a queue message is received, use hello `QueueTrigger` attribute.</span></span> <span data-ttu-id="7c3e8-143">Konstruktor atrybutu Hello przyjmuje parametr ciąg określający nazwę hello hello toopoll kolejki.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-143">hello attribute constructor takes a string parameter that specifies hello name of hello queue toopoll.</span></span> <span data-ttu-id="7c3e8-144">Możesz również [Ustaw nazwę kolejki hello dynamicznie](#config).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-144">You can also [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="7c3e8-145">Ciąg wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-145">String queue messages</span></span>
<span data-ttu-id="7c3e8-146">W hello poniższy przykład, kolejki hello zawiera komunikat, więc `QueueTrigger` jest stosowane tooa parametr ciągu o nazwie `logMessage` zawierającą hello zawartość hello kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-146">In hello following example, hello queue contains a string message, so `QueueTrigger` is applied tooa string parameter named `logMessage` which contains hello content of hello queue message.</span></span> <span data-ttu-id="7c3e8-147">Witaj funkcja [zapisuje dziennik komunikatów toohello pulpitu nawigacyjnego](#logs).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-147">hello function [writes a log message toohello Dashboard](#logs).</span></span>

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

<span data-ttu-id="7c3e8-148">Oprócz `string`, parametr hello może być tablicą bajtów `CloudQueueMessage` obiektu lub POCO, które należy zdefiniować.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-148">Besides `string`, hello parameter may be a byte array, a `CloudQueueMessage` object, or a POCO  that you define.</span></span>

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="7c3e8-149">POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-149">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="7c3e8-150">Poniższy przykład hello, komunikatu w kolejce hello zawiera JSON dla `BlobInformation` obiektu, który zawiera `BlobName` właściwości.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-150">In hello following example, hello queue message contains JSON for a `BlobInformation` object which includes a `BlobName` property.</span></span> <span data-ttu-id="7c3e8-151">Witaj SDK automatycznie deserializuje obiekt hello.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-151">hello SDK automatically deserializes hello object.</span></span>

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

<span data-ttu-id="7c3e8-152">Witaj SDK używa hello [pakietu Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize i deserializować wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-152">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="7c3e8-153">Wiadomości w kolejce w przypadku utworzenia w programie, który nie używa hello zestaw SDK zadań Webjob, można napisać kod, takich jak powitania po toocreate przykład komunikatu w kolejce POCO powitalne tego zestawu SDK można przeanalizować.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-153">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a><span data-ttu-id="7c3e8-154">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="7c3e8-154">Async functions</span></span>
<span data-ttu-id="7c3e8-155">Witaj następujących funkcji asynchronicznej [zapisuje dziennik toohello pulpitu nawigacyjnego](#logs).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-155">hello following async function [writes a log toohello Dashboard](#logs).</span></span>

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

<span data-ttu-id="7c3e8-156">Funkcje asynchroniczne może potrwać [token anulowania](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), jak pokazano w hello poniższy przykład, który kopiuje obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-156">Async functions may take a [cancellation token](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), as shown in hello following example which copies a blob.</span></span> <span data-ttu-id="7c3e8-157">(Aby uzyskać informacje o hello `queueTrigger` symbolu zastępczego, zobacz hello [obiekty BLOB](#blobs) sekcji.)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-157">(For an explanation of hello `queueTrigger` placeholder, see hello [Blobs](#blobs) section.)</span></span>

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

### <span data-ttu-id="7c3e8-158"><a id="qtattributetypes"></a>Atrybut QueueTrigger hello typy współpracuje z</span><span class="sxs-lookup"><span data-stu-id="7c3e8-158"><a id="qtattributetypes"></a> Types hello QueueTrigger attribute works with</span></span>
<span data-ttu-id="7c3e8-159">Można użyć `QueueTrigger` z hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-159">You can use `QueueTrigger` with hello following types:</span></span>

* `string`
* <span data-ttu-id="7c3e8-160">Typ POCO zserializowanym w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="7c3e8-160">A POCO type serialized as JSON</span></span>
* `byte[]`
* `CloudQueueMessage`

### <span data-ttu-id="7c3e8-161"><a id="polling"></a>Algorytm sondowania</span><span class="sxs-lookup"><span data-stu-id="7c3e8-161"><a id="polling"></a> Polling algorithm</span></span>
<span data-ttu-id="7c3e8-162">Witaj SDK implementuje efekt losowe wykładniczego wycofywania algorytmu tooreduce hello bezczynności-kolejki sondowania kosztów transakcji magazynu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-162">hello SDK implements a random exponential back-off algorithm tooreduce hello effect of idle-queue polling on storage transaction costs.</span></span>  <span data-ttu-id="7c3e8-163">Po znalezieniu wiadomość hello SDK oczekuje dwóch sekund i następnie wyszukuje kolejną wiadomość; gdy zostanie znaleziony żaden komunikat czeka około czterech sekund przed ponowną próbą.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-163">When a message is found, hello SDK waits two seconds and then checks for another message; when no message is found it waits about four seconds before trying again.</span></span> <span data-ttu-id="7c3e8-164">Po kolejnych nieudanych prób tooget komunikatu w kolejce, czas oczekiwania hello nadal tooincrease dopóki nie osiągnie hello maksymalny czas oczekiwania, które minutę tooone wartości domyślnych.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-164">After subsequent failed attempts tooget a queue message, hello wait time continues tooincrease until it reaches hello maximum wait time, which defaults tooone minute.</span></span> <span data-ttu-id="7c3e8-165">[Witaj maksymalny czas oczekiwania jest konfigurowalne](#config).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-165">[hello maximum wait time is configurable](#config).</span></span>

### <span data-ttu-id="7c3e8-166"><a id="instances"></a>Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="7c3e8-166"><a id="instances"></a> Multiple instances</span></span>
<span data-ttu-id="7c3e8-167">Jeśli aplikacja sieci web jest uruchamiana na wiele wystąpień, ciągłe zadanie WebJob jest uruchamiany na każdym komputerze, a każda maszyna zostanie poczekaj, aż usługa wyzwalaczy i podejmować toorun funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-167">If your web app runs on multiple instances, a continuous WebJob runs on each machine, and each machine will wait for triggers and attempt toorun functions.</span></span> <span data-ttu-id="7c3e8-168">Witaj zestaw SDK zadań Webjob kolejki wyzwalacza automatycznie uniemożliwia funkcji przetwarzania komunikatu w kolejce wiele razy; funkcje nie są zapisywane idempotentności toobe toobe.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-168">hello WebJobs SDK queue trigger automatically prevents a function from processing a queue message multiple times; functions do not have toobe written toobe idempotent.</span></span> <span data-ttu-id="7c3e8-169">Jednak jeśli chcesz tooensure tego tylko jedno wystąpienie funkcji jest uruchamiany nawet wtedy, gdy istnieje wiele wystąpień aplikacji sieci web hosta hello, można użyć hello `Singleton` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-169">However, if you want tooensure that only one instance of a function runs even when there are multiple instances of hello host web app, you can use hello `Singleton` attribute.</span></span>

### <span data-ttu-id="7c3e8-170"><a id="parallel"></a>Wykonywanie równoległe</span><span class="sxs-lookup"><span data-stu-id="7c3e8-170"><a id="parallel"></a> Parallel execution</span></span>
<span data-ttu-id="7c3e8-171">Jeśli masz wiele funkcji nasłuchiwanie w kolejkach różnych hello SDK wywoła je równolegle po odebraniu wiadomości jednocześnie.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-171">If you have multiple functions listening on different queues, hello SDK will call them in parallel when messages are received simultaneously.</span></span>

<span data-ttu-id="7c3e8-172">Witaj samo dotyczy po odebraniu wiele komunikatów dla pojedynczej kolejki.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-172">hello same is true when multiple messages are received for a single queue.</span></span> <span data-ttu-id="7c3e8-173">Domyślnie hello SDK pobiera partii 16 wiadomości w kolejce w czasie i wykonuje hello funkcja, która przetwarza je równolegle.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-173">By default, hello SDK gets a batch of 16 queue messages at a time and executes hello function that processes them in parallel.</span></span> <span data-ttu-id="7c3e8-174">[rozmiar partii Hello jest konfigurowalne](#config).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-174">[hello batch size is configurable](#config).</span></span> <span data-ttu-id="7c3e8-175">Gdy numer hello przetwarzanych pobiera dół toohalf rozmiar partii hello, hello SDK pobiera inna partia i rozpoczyna przetwarzanie tych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-175">When hello number being processed gets down toohalf of hello batch size, hello SDK gets another batch and starts processing those messages.</span></span> <span data-ttu-id="7c3e8-176">W związku z tym hello maksymalną liczbę równoczesnych komunikatów przetwarzanych dla każdej funkcji jest rozmiar partii hello co oraz wielokrotności.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-176">Therefore hello maximum number of concurrent messages being processed per function is one and a half times hello batch size.</span></span> <span data-ttu-id="7c3e8-177">Ten limit dotyczy oddzielnie tooeach funkcja, która ma `QueueTrigger` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-177">This limit applies separately tooeach function that has a `QueueTrigger` attribute.</span></span>

<span data-ttu-id="7c3e8-178">Jeśli nie chcesz wykonywanie równoległe dla wiadomości otrzymanych w jednej kolejki, można ustawić too1 rozmiar partii hello.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-178">If you don't want parallel execution for messages received on one queue, you can set hello batch size too1.</span></span> <span data-ttu-id="7c3e8-179">Zobacz też **większą kontrolę nad kolejki przetwarzania** w [RTM zestawu Azure WebJobs SDK w wersji 1.1.0](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-179">See also **More control over Queue processing** in [Azure WebJobs SDK 1.1.0 RTM](https://azure.microsoft.com/blog/azure-webjobs-sdk-1-1-0-rtm/).</span></span>

### <span data-ttu-id="7c3e8-180"><a id="queuemetadata"></a>Pobierz kolejki lub kolejka komunikatów metadanych</span><span class="sxs-lookup"><span data-stu-id="7c3e8-180"><a id="queuemetadata"></a>Get queue or queue message metadata</span></span>
<span data-ttu-id="7c3e8-181">Możesz uzyskać hello następujące właściwości wiadomości przez dodanie podpis metody toohello parametry:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-181">You can get hello following message properties by adding parameters toohello method signature:</span></span>

* <span data-ttu-id="7c3e8-182">`DateTimeOffset`expirationTime</span><span class="sxs-lookup"><span data-stu-id="7c3e8-182">`DateTimeOffset` expirationTime</span></span>
* <span data-ttu-id="7c3e8-183">`DateTimeOffset`insertionTime</span><span class="sxs-lookup"><span data-stu-id="7c3e8-183">`DateTimeOffset` insertionTime</span></span>
* <span data-ttu-id="7c3e8-184">`DateTimeOffset`nextVisibleTime</span><span class="sxs-lookup"><span data-stu-id="7c3e8-184">`DateTimeOffset` nextVisibleTime</span></span>
* <span data-ttu-id="7c3e8-185">`string`queueTrigger (tekst wiadomości zawiera)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-185">`string` queueTrigger (contains message text)</span></span>
* <span data-ttu-id="7c3e8-186">`string`Identyfikator</span><span class="sxs-lookup"><span data-stu-id="7c3e8-186">`string` id</span></span>
* <span data-ttu-id="7c3e8-187">`string`elementu popReceipt</span><span class="sxs-lookup"><span data-stu-id="7c3e8-187">`string` popReceipt</span></span>
* <span data-ttu-id="7c3e8-188">`int`dequeueCount</span><span class="sxs-lookup"><span data-stu-id="7c3e8-188">`int` dequeueCount</span></span>

<span data-ttu-id="7c3e8-189">Jeśli chcesz toowork bezpośrednio z hello interfejsu API magazynu Azure, możesz także dodać `CloudStorageAccount` parametru.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-189">If you want toowork directly with hello Azure storage API, you can also add a `CloudStorageAccount` parameter.</span></span>

<span data-ttu-id="7c3e8-190">Witaj poniższy przykład zapisuje wszystkie ten dziennik metadanych tooan informacje o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-190">hello following example writes all of this metadata tooan INFO application log.</span></span> <span data-ttu-id="7c3e8-191">Przykład Witaj zarówno logMessage i queueTrigger zawartością hello hello kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-191">In hello example, both logMessage and queueTrigger contain hello content of hello queue message.</span></span>

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

<span data-ttu-id="7c3e8-192">Poniżej przedstawiono przykładowy dziennik napisane przez hello przykładowy kod:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-192">Here is a sample log written by hello sample code:</span></span>

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

### <span data-ttu-id="7c3e8-193"><a id="graceful"></a>Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="7c3e8-193"><a id="graceful"></a>Graceful shutdown</span></span>
<span data-ttu-id="7c3e8-194">Funkcja, która działa w ciągłego zadania WebJob może akceptować `CancellationToken` parametr, który umożliwia hello systemu operacyjnego toonotify hello funkcji hello zadania WebJob dotyczy toobe zakończone.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-194">A function that runs in a continuous WebJob can accept a `CancellationToken` parameter which enables hello operating system toonotify hello function when hello WebJob is about toobe terminated.</span></span> <span data-ttu-id="7c3e8-195">Możesz użyć tego toomake powiadomień, się, że funkcja hello nie nieoczekiwane zakończenie w sposób powodujący, że dane w niespójnym stanie.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-195">You can use this notification toomake sure hello function doesn't terminate unexpectedly in a way that leaves data in an inconsistent state.</span></span>

<span data-ttu-id="7c3e8-196">powitania po przykładzie pokazano, jak toocheck zbliżającym się zakończenia zadania WebJob w funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-196">hello following example shows how toocheck for impending WebJob termination in a function.</span></span>

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

<span data-ttu-id="7c3e8-197">**Uwaga:** hello pulpit nawigacyjny może nie poprawnie pokazać hello stan i dane wyjściowe funkcji, które została zamknięta.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-197">**Note:** hello Dashboard might not correctly show hello status and output of functions that have been shut down.</span></span>

<span data-ttu-id="7c3e8-198">Aby uzyskać więcej informacji, zobacz [łagodne zamykanie zadań Webjob](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-198">For more information, see [WebJobs Graceful Shutdown](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).</span></span>   

## <span data-ttu-id="7c3e8-199"><a id="createqueue"></a>Jak toocreate kolejki komunikatów podczas przetwarzania komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-199"><a id="createqueue"></a> How toocreate a queue message while processing a queue message</span></span>
<span data-ttu-id="7c3e8-200">toowrite funkcję, która tworzy nowy komunikat kolejki, użyj hello `Queue` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-200">toowrite a function that creates a new queue message, use hello `Queue` attribute.</span></span> <span data-ttu-id="7c3e8-201">Podobnie jak `QueueTrigger`, podaj nazwę kolejki hello jako ciąg lub możesz [Ustaw nazwę kolejki hello dynamicznie](#config).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-201">Like `QueueTrigger`, you pass in hello queue name as a string or you can [set hello queue name dynamically](#config).</span></span>

### <a name="string-queue-messages"></a><span data-ttu-id="7c3e8-202">Ciąg wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-202">String queue messages</span></span>
<span data-ttu-id="7c3e8-203">powitania po przykładowy kod z systemem innym niż async tworzy nowego komunikatu w kolejce w kolejce hello o nazwie "outputqueue" z hello sama zawartość jako hello kolejki wiadomości odebrane w kolejce hello o nazwie "inputqueue".</span><span class="sxs-lookup"><span data-stu-id="7c3e8-203">hello following non-async code sample creates a new queue message in hello queue named "outputqueue" with hello same content as hello queue message received in hello queue named "inputqueue".</span></span> <span data-ttu-id="7c3e8-204">(Asynchroniczne Użyj funkcji `IAsyncCollector<T>` opisane dalej w tej sekcji.)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-204">(For async functions use `IAsyncCollector<T>` as shown later in this section.)</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a><span data-ttu-id="7c3e8-205">POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-205">POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="7c3e8-206">toocreate komunikat z kolejki zawiera POCO niż ciąg hello przebiegu POCO wpisać jako toohello parametru wyjściowego `Queue` atrybut konstruktora.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-206">toocreate a queue message that contains a POCO rather than a string, pass hello POCO type as an output parameter toohello `Queue` attribute constructor.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

<span data-ttu-id="7c3e8-207">Witaj SDK automatycznie serializuje hello tooJSON obiektu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-207">hello SDK automatically serializes hello object tooJSON.</span></span> <span data-ttu-id="7c3e8-208">Komunikatu w kolejce zawsze jest tworzony, nawet jeśli obiekt hello jest pusty.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-208">A queue message is always created, even if hello object is null.</span></span>

### <a name="create-multiple-messages-or-in-async-functions"></a><span data-ttu-id="7c3e8-209">Tworzenie wielu wiadomości lub w funkcji asynchronicznych</span><span class="sxs-lookup"><span data-stu-id="7c3e8-209">Create multiple messages or in async functions</span></span>
<span data-ttu-id="7c3e8-210">toocreate wiele komunikatów upewnij hello typu parametru dla kolejki wyjściowej hello `ICollector<T>` lub `IAsyncCollector<T>`, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-210">toocreate multiple messages, make hello parameter type for hello output queue `ICollector<T>` or `IAsyncCollector<T>`, as shown in hello following example.</span></span>

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

<span data-ttu-id="7c3e8-211">Każdy komunikat kolejki jest tworzony natychmiast po hello `Add` metoda jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-211">Each queue message is created immediately when hello `Add` method is called.</span></span>

### <a name="types-that-hello-queue-attribute-works-with"></a><span data-ttu-id="7c3e8-212">Typy atrybutu kolejki hello współpracuje z</span><span class="sxs-lookup"><span data-stu-id="7c3e8-212">Types that hello Queue attribute works with</span></span>
<span data-ttu-id="7c3e8-213">Można użyć hello `Queue` atrybutu na powitania następujące typy parametrów:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-213">You can use hello `Queue` attribute on hello following parameter types:</span></span>

* <span data-ttu-id="7c3e8-214">`out string`(tworzy komunikat z kolejki, jeśli wartość parametru jest różna od null, gdy funkcja hello kończy się)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-214">`out string` (creates queue message if parameter value is non-null when hello function ends)</span></span>
* <span data-ttu-id="7c3e8-215">`out byte[]`(takich jak działa `string`)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-215">`out byte[]` (works like `string`)</span></span>
* <span data-ttu-id="7c3e8-216">`out CloudQueueMessage`(takich jak działa `string`)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-216">`out CloudQueueMessage` (works like `string`)</span></span>
* <span data-ttu-id="7c3e8-217">`out POCO`(typ możliwy do serializacji, tworzy komunikat z obiektem null, jeśli parametru hello ma wartość null, gdy funkcja hello kończy się)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-217">`out POCO` (a serializable type, creates a message with a null object if hello paramter is null when hello function ends)</span></span>
* `ICollector`
* `IAsyncCollector`
* <span data-ttu-id="7c3e8-218">`CloudQueue`(do tworzenia komunikatów ręcznie bezpośrednio za pomocą hello interfejsu API magazynu Azure)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-218">`CloudQueue` (for creating messages manually using hello Azure Storage API directly)</span></span>

### <span data-ttu-id="7c3e8-219"><a id="ibinder"></a>Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji</span><span class="sxs-lookup"><span data-stu-id="7c3e8-219"><a id="ibinder"></a>Use WebJobs SDK attributes in hello body of a function</span></span>
<span data-ttu-id="7c3e8-220">Jeśli potrzebujesz toodo niektóre działają w funkcji przed przy użyciu atrybutu zestaw SDK zadań Webjob, takich jak `Queue`, `Blob`, lub `Table`, można użyć hello `IBinder` interfejsu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-220">If you need toodo some work in your function before using a WebJobs SDK attribute such as `Queue`, `Blob`, or `Table`, you can use hello `IBinder` interface.</span></span>

<span data-ttu-id="7c3e8-221">Poniższy przykład Hello pobiera wiadomość z kolejki wejściowej i tworzy nowy komunikat o tej samej zawartości w kolejki wyjściowej hello.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-221">hello following example takes an input queue message and creates a new message with hello same content in an output queue.</span></span> <span data-ttu-id="7c3e8-222">Nazwa kolejki danych wyjściowych Hello jest ustawiana przez kod w treści hello hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-222">hello output queue name is set by code in hello body of hello function.</span></span>

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

<span data-ttu-id="7c3e8-223">Witaj `IBinder` interfejsu można również z hello `Table` i `Blob` atrybutów.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-223">hello `IBinder` interface can also be used with hello `Table` and `Blob` attributes.</span></span>

## <span data-ttu-id="7c3e8-224"><a id="blobs"></a>Jak tooread i zapisu obiektów blob i tabelach podczas przetwarzania komunikatu w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-224"><a id="blobs"></a> How tooread and write blobs and tables while processing a queue message</span></span>
<span data-ttu-id="7c3e8-225">Witaj `Blob` i `Table` atrybutów umożliwiają tooread i zapisywać obiekty BLOB i tabelach.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-225">hello `Blob` and `Table` attributes enable you tooread and write blobs and tables.</span></span> <span data-ttu-id="7c3e8-226">Witaj próbek w tej sekcji mają zastosowanie tooblobs.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-226">hello samples in this section apply tooblobs.</span></span> <span data-ttu-id="7c3e8-227">Aby uzyskać przykłady kodu, które pokazują, jak tootrigger przetwarza podczas tworzenia lub aktualizowania obiektów blob, zobacz [jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)oraz przykłady kodu, do odczytu i zapisu tabel, zobacz [jak toouse tabeli platformy Azure Magazyn z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-227">For code samples that show how tootrigger processes when blobs are created or updated, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md), and for code samples that read and write tables, see [How toouse Azure table storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-tables-how-to.md).</span></span>

### <a name="string-queue-messages-triggering-blob-operations"></a><span data-ttu-id="7c3e8-228">Ciąg wiadomości w kolejce wyzwalania operacje obiektów blob</span><span class="sxs-lookup"><span data-stu-id="7c3e8-228">String queue messages triggering blob operations</span></span>
<span data-ttu-id="7c3e8-229">Dla komunikatu w kolejce, który zawiera ciąg `queueTrigger` to symbol zastępczy, można użyć w hello `Blob` atrybutu `blobPath` parametr, który zawiera hello zawartość wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-229">For a queue message that contains a string, `queueTrigger` is a placeholder you can use in hello `Blob` attribute's `blobPath` parameter that contains hello contents of hello message.</span></span>

<span data-ttu-id="7c3e8-230">Witaj poniższym przykładzie użyto `Stream` obiekty BLOB tooread i zapisu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-230">hello following example uses `Stream` objects tooread and write blobs.</span></span> <span data-ttu-id="7c3e8-231">komunikat z kolejki Hello jest hello nazwa obiektu blob znajdujących się w kontenerze textblobs hello.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-231">hello queue message is hello name of a blob located in hello textblobs container.</span></span> <span data-ttu-id="7c3e8-232">Kopiowania obiektu blob hello z "-nowych" Nazwa toohello dołączany jest tworzony w hello sam kontenera.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-232">A copy of hello blob with "-new" appended toohello name is created in hello same container.</span></span>

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="7c3e8-233">Witaj `Blob` atrybutu ma konstruktora `blobPath` parametr, który określa kontener hello i nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-233">hello `Blob` attribute constructor takes a `blobPath` parameter that specifies hello container and blob name.</span></span> <span data-ttu-id="7c3e8-234">Aby uzyskać więcej informacji dotyczących tego symbolu zastępczego, zobacz [jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span><span class="sxs-lookup"><span data-stu-id="7c3e8-234">For more information about this placeholder, see [How toouse Azure blob storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md),</span></span>

<span data-ttu-id="7c3e8-235">Gdy atrybut hello decorates `Stream` obiekt inny parametr konstruktora określa hello `FileAccess` trybie odczytu, zapisu lub odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-235">When hello attribute decorates a `Stream` object, another constructor parameter specifies hello `FileAccess` mode as read, write, or read/write.</span></span>

<span data-ttu-id="7c3e8-236">Witaj poniższym przykładzie użyto `CloudBlockBlob` obiekt toodelete obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-236">hello following example uses a `CloudBlockBlob` object toodelete a blob.</span></span> <span data-ttu-id="7c3e8-237">komunikat z kolejki Hello jest nazwą hello hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-237">hello queue message is hello name of hello blob.</span></span>

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <span data-ttu-id="7c3e8-238"><a id="pocoblobs"></a>POCO [(zwykły stary obiekt CLR](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) wiadomości w kolejce</span><span class="sxs-lookup"><span data-stu-id="7c3e8-238"><a id="pocoblobs"></a> POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object)) queue messages</span></span>
<span data-ttu-id="7c3e8-239">POCO, zapisane w formacie JSON hello kolejki wiadomości, można użyć zastępcze nazw właściwości obiektu hello w hello `Queue` atrybutu `blobPath` parametru.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-239">For a POCO stored as JSON in hello queue message, you can use placeholders that name properties of hello object in hello `Queue` attribute's `blobPath` parameter.</span></span> <span data-ttu-id="7c3e8-240">Można również użyć [kolejka nazw właściwości metadanych](#queuemetadata) jako symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-240">You can also use [queue metadata property names](#queuemetadata) as placeholders.</span></span>

<span data-ttu-id="7c3e8-241">Witaj Poniższy przykładowy kod kopiuje obiekt blob tooa nowego obiektu blob z innym rozszerzeniem.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-241">hello following example copies a blob tooa new blob with a different extension.</span></span> <span data-ttu-id="7c3e8-242">komunikat z kolejki Hello jest `BlobInformation` obiekt, który zawiera `BlobName` i `BlobNameWithoutExtension` właściwości.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-242">hello queue message is a `BlobInformation` object that includes `BlobName` and `BlobNameWithoutExtension` properties.</span></span> <span data-ttu-id="7c3e8-243">nazwy właściwości Hello są używane jako symbole zastępcze w ścieżce obiektu blob hello hello `Blob` atrybutów.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-243">hello property names are used as placeholders in hello blob path for hello `Blob` attributes.</span></span>

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

<span data-ttu-id="7c3e8-244">Witaj SDK używa hello [pakietu Newtonsoft.Json NuGet](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize i deserializować wiadomości.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-244">hello SDK uses hello [Newtonsoft.Json NuGet package](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize and deserialize messages.</span></span> <span data-ttu-id="7c3e8-245">Wiadomości w kolejce w przypadku utworzenia w programie, który nie używa hello zestaw SDK zadań Webjob, można napisać kod, takich jak powitania po toocreate przykład komunikatu w kolejce POCO powitalne tego zestawu SDK można przeanalizować.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-245">If you create queue messages in a program that doesn't use hello WebJobs SDK, you can write code like hello following example toocreate a POCO queue message that hello SDK can parse.</span></span>

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

<span data-ttu-id="7c3e8-246">Jeśli potrzebujesz toodo niektóre działają w funkcji przed powiązania obiektu blob tooan, można użyć atrybutu hello w treści funkcji hello hello [jak pokazano wcześniej atrybutu kolejki hello](#ibinder).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-246">If you need toodo some work in your function before binding a blob tooan object, you can use hello attribute in hello body of hello function, [as shown earlier for hello Queue attribute](#ibinder).</span></span>

### <span data-ttu-id="7c3e8-247"><a id="blobattributetypes"></a>Typy, można użyć hello obiektu Blob atrybutu z</span><span class="sxs-lookup"><span data-stu-id="7c3e8-247"><a id="blobattributetypes"></a> Types you can use hello Blob attribute with</span></span>
<span data-ttu-id="7c3e8-248">Witaj `Blob` atrybut może być używany z hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-248">hello `Blob` attribute can be used with hello following types:</span></span>

* <span data-ttu-id="7c3e8-249">`Stream`(Odczyt lub zapis, określić przy użyciu parametru konstruktora FileAccess hello)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-249">`Stream` (read or write, specified by using hello FileAccess constructor parameter)</span></span>
* `TextReader`
* `TextWriter`
* <span data-ttu-id="7c3e8-250">`string`(odczyt)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-250">`string` (read)</span></span>
* <span data-ttu-id="7c3e8-251">`out string`(zapisu; tworzy obiektu blob tylko wtedy, gdy parametr ciąg hello jest inną niż null, gdy funkcja hello zwraca)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-251">`out string` (write; creates a blob only if hello string parameter is non-null when hello function returns)</span></span>
* <span data-ttu-id="7c3e8-252">POCO (odczyt)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-252">POCO (read)</span></span>
* <span data-ttu-id="7c3e8-253">limit POCO (zapisu; zawsze tworzy obiektu blob, tworzy jako obiekt null, jeśli parametr POCO ma wartość null, gdy funkcja hello zwraca)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-253">out POCO (write; always creates a blob, creates as null object if POCO parameter is null when hello function returns)</span></span>
* <span data-ttu-id="7c3e8-254">`CloudBlobStream`(Zapisz)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-254">`CloudBlobStream` (write)</span></span>
* <span data-ttu-id="7c3e8-255">`ICloudBlob`(Odczyt lub zapis)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-255">`ICloudBlob` (read or write)</span></span>
* <span data-ttu-id="7c3e8-256">`CloudBlockBlob`(Odczyt lub zapis)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-256">`CloudBlockBlob` (read or write)</span></span>
* <span data-ttu-id="7c3e8-257">`CloudPageBlob`(Odczyt lub zapis)</span><span class="sxs-lookup"><span data-stu-id="7c3e8-257">`CloudPageBlob` (read or write)</span></span>

## <span data-ttu-id="7c3e8-258"><a id="poison"></a>Jak toohandle zanieczyszczonych komunikatów</span><span class="sxs-lookup"><span data-stu-id="7c3e8-258"><a id="poison"></a> How toohandle poison messages</span></span>
<span data-ttu-id="7c3e8-259">Komunikaty, których zawartość powoduje toofail funkcji są nazywane *zanieczyszczonych komunikatów*.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-259">Messages whose content causes a function toofail are called *poison messages*.</span></span> <span data-ttu-id="7c3e8-260">W przypadku awarii funkcja hello hello kolejki wiadomości nie zostanie usunięta i ostatecznie zostaje pobrana ponownie, powodując toobe cyklu hello powtarzany.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-260">When hello function fails, hello queue message is not deleted and eventually is picked up again, causing hello cycle toobe repeated.</span></span> <span data-ttu-id="7c3e8-261">Hello SDK automatycznie może przerwać cyklu powitania po ograniczonej liczby iteracji, lub możesz zrobić to ręcznie.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-261">hello SDK can automatically interrupt hello cycle after a limited number of iterations, or you can do it manually.</span></span>

### <a name="automatic-poison-message-handling"></a><span data-ttu-id="7c3e8-262">Obsługa automatycznego Trująca wiadomość</span><span class="sxs-lookup"><span data-stu-id="7c3e8-262">Automatic poison message handling</span></span>
<span data-ttu-id="7c3e8-263">Hello zestawu SDK wywoła funkcję się too5 razy tooprocess komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-263">hello SDK will call a function up too5 times tooprocess a queue message.</span></span> <span data-ttu-id="7c3e8-264">W przypadku niepowodzenia spróbuj piątym powitania wiadomość hello jest przeniesionego tooa skażone kolejki.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-264">If hello fifth try fails, hello message is moved tooa poison queue.</span></span> <span data-ttu-id="7c3e8-265">[konfiguruje się Hello maksymalnej liczby ponownych prób](#config).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-265">[hello maximum number of retries is configurable](#config).</span></span>

<span data-ttu-id="7c3e8-266">nosi nazwę kolejki skażone Hello *{originalqueuename}*-skażone.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-266">hello poison queue is named *{originalqueuename}*-poison.</span></span> <span data-ttu-id="7c3e8-267">Można napisać tooprocess funkcji wiadomości z kolejki skażone hello rejestrowania ich lub wysyłania powiadomienia, że wymagana jest ręczne uwagi.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-267">You can write a function tooprocess messages from hello poison queue by logging them or sending a notification that manual attention is needed.</span></span>

<span data-ttu-id="7c3e8-268">W powitania po hello przykład `CopyBlob` funkcja zakończy się niepowodzeniem, gdy komunikatu w kolejce zawiera nazwę hello obiektu blob, który nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-268">In hello following example hello `CopyBlob` function will fail when a queue message contains hello name of a blob that doesn't exist.</span></span> <span data-ttu-id="7c3e8-269">W takim przypadku wiadomość hello jest przenoszona z hello copyblobqueue kolejki toohello copyblobqueue poison kolejki.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-269">When that happens, hello message is moved from hello copyblobqueue queue toohello copyblobqueue-poison queue.</span></span> <span data-ttu-id="7c3e8-270">Witaj `ProcessPoisonMessage` , a następnie Trująca wiadomość hello dzienników.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-270">hello `ProcessPoisonMessage` then logs hello poison message.</span></span>

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

<span data-ttu-id="7c3e8-271">Witaj poniżej przedstawiono dane wyjściowe konsoli z tych funkcji po skażone komunikat jest przetwarzany.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-271">hello following illustration shows console output from these functions when a poison message is processed.</span></span>

![Dane wyjściowe konsoli dotyczące obsługi uszkodzonych komunikatów](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/poison.png)

### <a name="manual-poison-message-handling"></a><span data-ttu-id="7c3e8-273">Trująca wiadomość została ręcznej obsługi</span><span class="sxs-lookup"><span data-stu-id="7c3e8-273">Manual poison message handling</span></span>
<span data-ttu-id="7c3e8-274">Można uzyskać hello liczba wiadomości została pobrana do przetworzenia przez dodanie `int` parametru o nazwie `dequeueCount` tooyour funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-274">You can get hello number of times a message has been picked up for processing by adding an `int` parameter named `dequeueCount` tooyour function.</span></span> <span data-ttu-id="7c3e8-275">Mogą być następnie hello wyboru usuwania z kolejki liczby w kodzie funkcji i wykonać własne Trująca wiadomość została obsługa podczas numer hello przekracza próg, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-275">You can then check hello dequeue count in function code and perform your own poison message handling when hello number exceeds a threshold, as shown in hello following example.</span></span>

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

## <span data-ttu-id="7c3e8-276"><a id="config"></a>Jak tooset opcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="7c3e8-276"><a id="config"></a> How tooset configuration options</span></span>
<span data-ttu-id="7c3e8-277">Można użyć hello `JobHostConfiguration` hello tooset typu następujące opcje konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-277">You can use hello `JobHostConfiguration` type tooset hello following configuration options:</span></span>

* <span data-ttu-id="7c3e8-278">Ustawianie parametrów połączenia SDK hello w kodzie.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-278">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="7c3e8-279">Skonfiguruj `QueueTrigger` ustawienia, takie jak maksymalna liczba usuwania z kolejki.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-279">Configure `QueueTrigger` settings such as maximum dequeue count.</span></span>
* <span data-ttu-id="7c3e8-280">Pobierz nazwy kolejki z konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-280">Get queue names from configuration.</span></span>

### <span data-ttu-id="7c3e8-281"><a id="setconnstr"></a>Ustawianie parametrów połączenia SDK w kodzie</span><span class="sxs-lookup"><span data-stu-id="7c3e8-281"><a id="setconnstr"></a>Set SDK connection strings in code</span></span>
<span data-ttu-id="7c3e8-282">Ustawianie parametrów połączenia SDK hello w kodzie umożliwia toouse możesz własne nazwy ciągu połączenia w plikach konfiguracji lub zmiennych środowiskowych, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-282">Setting hello SDK connection strings in code enables you toouse your own connection string names in configuration files or environment variables, as shown in hello following example.</span></span>

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

### <span data-ttu-id="7c3e8-283"><a id="configqueue"></a>Skonfiguruj ustawienia QueueTrigger</span><span class="sxs-lookup"><span data-stu-id="7c3e8-283"><a id="configqueue"></a>Configure QueueTrigger  settings</span></span>
<span data-ttu-id="7c3e8-284">Można skonfigurować następujące ustawienia dotyczące przetwarzania komunikatu w kolejce toohello hello:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-284">You can configure hello following settings that apply toohello queue message processing:</span></span>

* <span data-ttu-id="7c3e8-285">Maksymalna liczba wiadomości w kolejce, które są pobierane jednocześnie toobe wykonywane równolegle Hello (wartość domyślna to 16).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-285">hello maximum number of queue messages that are picked up simultaneously toobe executed in parallel (default is 16).</span></span>
* <span data-ttu-id="7c3e8-286">Witaj maksymalnej liczby ponownych prób przed wysłaniem komunikatu w kolejce tooa skażone kolejki (wartość domyślna to 5).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-286">hello maximum number of retries before a queue message is sent tooa poison queue (default is 5).</span></span>
* <span data-ttu-id="7c3e8-287">Witaj maksymalny czas oczekiwania przed sondowania ponownie, gdy kolejka jest pusta (wartość domyślna to 1 minuta).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-287">hello maximum wait time before polling again when a queue is empty (default is 1 minute).</span></span>

<span data-ttu-id="7c3e8-288">powitania po przykładzie pokazano, jak tooconfigure te ustawienia:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-288">hello following example shows how tooconfigure these settings:</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <span data-ttu-id="7c3e8-289"><a id="setnamesincode"></a>Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="7c3e8-289"><a id="setnamesincode"></a>Set values for WebJobs SDK constructor parameters in code</span></span>
<span data-ttu-id="7c3e8-290">Czasami trzeba toospecify nazwę kolejki, nazwa obiektu blob lub kontener lub tabeli nazw w kodzie, a nie kodowane.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-290">Sometimes you want toospecify a queue name, a blob name or container, or a table name in code rather than hard-code it.</span></span> <span data-ttu-id="7c3e8-291">Na przykład może być nazwę kolejki hello toospecify `QueueTrigger` w zmiennej środowisku i pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-291">For example, you might want toospecify hello queue name for `QueueTrigger` in a configuration file or environment variable.</span></span>

<span data-ttu-id="7c3e8-292">Możesz to zrobić przez przekazywanie `NameResolver` obiekt toohello `JobHostConfiguration` typu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-292">You can do that by passing in a `NameResolver` object toohello `JobHostConfiguration` type.</span></span> <span data-ttu-id="7c3e8-293">Obejmują specjalne symbole zastępcze ujęta w znaki procentu (%) w parametrach konstruktora atrybut zestaw SDK zadań Webjob i `NameResolver` kodu określa toobe wartości rzeczywistych hello używany zamiast te symbole zastępcze.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-293">You include special placeholders surrounded by percent (%) signs in WebJobs SDK attribute constructor parameters, and your `NameResolver` code specifies hello actual values toobe used in place of those placeholders.</span></span>

<span data-ttu-id="7c3e8-294">Na przykład załóżmy, że chcesz toouse kolejki o nazwie logqueuetest w środowisku testowym hello i jedną o nazwie logqueueprod w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-294">For example, suppose you want toouse a queue named logqueuetest in hello test environment and one named logqueueprod in production.</span></span> <span data-ttu-id="7c3e8-295">Zamiast nazwę kolejki ustalony ma nazwę hello toospecify wpis w hello `appSettings` kolekcji mające hello nazwa rzeczywista kolejki.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-295">Instead of a hard-coded queue name, you want toospecify hello name of an entry in hello `appSettings` collection that would have hello actual queue name.</span></span> <span data-ttu-id="7c3e8-296">Jeśli hello `appSettings` klucz jest logqueue, funkcja może wyglądać hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-296">If hello `appSettings` key is logqueue, your function could look like hello following example.</span></span>

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

<span data-ttu-id="7c3e8-297">Twoje `NameResolver` klasy, można uzyskać nazwy kolejki hello z `appSettings` pokazane na powitania poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-297">Your `NameResolver` class could then get hello queue name from `appSettings` as shown in hello following example:</span></span>

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

<span data-ttu-id="7c3e8-298">Przekaż hello `NameResolver` klasy w toohello `JobHost` obiektów, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-298">You pass hello `NameResolver` class in toohello `JobHost` object as shown in hello following example.</span></span>

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

<span data-ttu-id="7c3e8-299">**Uwaga:** nazwy obiektów blob, tabel i kolejki rozwiązywane są zawsze funkcja jest nazywana, ale nazwy kontenera obiektów blob są rozpoznawane tylko wtedy, gdy uruchamiana jest aplikacja hello.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-299">**Note:** Queue, table, and blob names are resolved each time a function is called, but blob container names are resolved only when hello application starts.</span></span> <span data-ttu-id="7c3e8-300">Nie można zmienić nazwy kontenera obiektów blob, gdy jest wykonywane zadanie hello.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-300">You can't change blob container name while hello job is running.</span></span>

## <span data-ttu-id="7c3e8-301"><a id="manual"></a>Jak tootrigger funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="7c3e8-301"><a id="manual"></a>How tootrigger a function manually</span></span>
<span data-ttu-id="7c3e8-302">tootrigger funkcję ręcznie, użyj hello `Call` lub `CallAsync` metody na powitania `JobHost` obiekt i hello `NoAutomaticTrigger` atrybutu hello funkcji, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-302">tootrigger a function manually, use hello `Call` or `CallAsync` method on hello `JobHost` object and hello `NoAutomaticTrigger` attribute on hello function, as shown in hello following example.</span></span>

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

## <span data-ttu-id="7c3e8-303"><a id="logs"></a>Sposób rejestrowania toowrite</span><span class="sxs-lookup"><span data-stu-id="7c3e8-303"><a id="logs"></a>How toowrite logs</span></span>
<span data-ttu-id="7c3e8-304">Witaj pulpitu nawigacyjnego przedstawia dzienniki w dwóch miejscach: hello stronę hello zadania WebJob i hello strony dla poszczególnych wywołań zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-304">hello Dashboard shows logs in two places: hello page for hello WebJob, and hello page for a particular WebJob invocation.</span></span>

![Dzienniki na stronie zadania WebJob](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

![Dzienniki na stronie wywołania funkcji](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="7c3e8-307">Dane wyjściowe z konsoli metody, które należy wywołać funkcję lub hello `Main()` metoda pojawia się na stronie pulpitu nawigacyjnego hello na powitania zadania WebJob, nie na stronie powitania dla wywołania metody określonej.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-307">Output from Console methods that you call in a function or in hello `Main()` method appears in hello Dashboard page for hello WebJob, not in hello page for a particular method invocation.</span></span> <span data-ttu-id="7c3e8-308">Na stronie pulpitu nawigacyjnego hello wywołania metody zostaną wyświetlone dane wyjściowe z hello TextWriter obiektu, który można pobrać z parametrem w podpisie metody.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-308">Output from hello TextWriter object that you get from a parameter in your method signature appears in hello Dashboard page for a method invocation.</span></span>

<span data-ttu-id="7c3e8-309">Dane wyjściowe konsoli nie może być wywołanie metody określonej tooa połączonej, ponieważ hello konsoli jest pojedynczym wątku, podczas gdy wiele funkcji zadanie może działać na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-309">Console output can't be linked tooa particular method invocation because hello Console is single-threaded, while many job functions may be running at hello same time.</span></span> <span data-ttu-id="7c3e8-310">Dlatego hello SDK udostępnia każde wywołanie funkcji z własnego obiektu zapisującego unikatowy dziennika.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-310">That's why hello  SDK provides each function invocation with its own unique log writer object.</span></span>

<span data-ttu-id="7c3e8-311">toowrite [dzienniki śledzenia aplikacji](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), użyj `Console.Out` (tworzy Dzienniki oznaczone jako informacje) i `Console.Error` (tworzy Dzienniki oznaczone jako błąd).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-311">toowrite [application tracing logs](web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), use `Console.Out` (creates logs marked as INFO) and `Console.Error` (creates logs marked as ERROR).</span></span> <span data-ttu-id="7c3e8-312">Alternatywą jest toouse [śledzenia lub TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), która zapewnia pełne, ostrzeżenie, i krytyczne poziomy tooInfo dodanie i błąd.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-312">An alternative is toouse [Trace or TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), which provides Verbose, Warning, and Critical levels in addition tooInfo and Error.</span></span> <span data-ttu-id="7c3e8-313">Dzienniki śledzenia aplikacji są wyświetlane w plikach dziennika aplikacji sieci web hello, tabelach platformy Azure lub w zależności od sposobu skonfigurowania aplikacji sieci web platformy Azure obiektów blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-313">Application tracing logs appear in hello web app log files, Azure tables, or Azure blobs depending on how you configure your Azure web app.</span></span> <span data-ttu-id="7c3e8-314">Jak wszystkie dane wyjściowe konsoli, najnowsze dzienniki 100 aplikacji hello również zostać wyświetlony na stronie pulpitu nawigacyjnego hello na powitania zadania WebJob, nie hello strony dla wywołania funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-314">As is true of all Console output, hello most recent 100 application logs also appear in hello Dashboard page for hello WebJob, not hello page for a function invocation.</span></span>

<span data-ttu-id="7c3e8-315">Dane wyjściowe konsoli zostanie wyświetlony w hello pulpitu nawigacyjnego tylko wtedy, gdy hello program działa w zadań WebJob Azure, nie, jeśli hello program działa lokalnie lub w niektórych innych środowiska.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-315">Console output appears in hello Dashboard only if hello program is running in an Azure WebJob, not if hello program is running locally or in some other environment.</span></span>

<span data-ttu-id="7c3e8-316">Wyłącz rejestrowanie pulpitu nawigacyjnego dla scenariuszy wysokiej przepływności.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-316">Disable dashboard logging for high throughput scenarios.</span></span> <span data-ttu-id="7c3e8-317">Domyślnie program hello SDK zapisuje dzienniki toostorage, a to działanie może spowodować obniżenie wydajności podczas przetwarzania wielu komunikatów.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-317">By default, hello SDK writes logs toostorage, and this activity could degrade performance when you are processing many messages.</span></span> <span data-ttu-id="7c3e8-318">Rejestrowanie toodisable ustawione toonull ciąg połączenia pulpitu nawigacyjnego hello, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-318">toodisable logging, set hello dashboard connection string toonull as shown in hello following example.</span></span>

        JobHostConfiguration config = new JobHostConfiguration();       
        config.DashboardConnectionString = "";        
        JobHost host = new JobHost(config);
        host.RunAndBlock();

<span data-ttu-id="7c3e8-319">Witaj poniższym przykładzie pokazano kilka sposobów toowrite dzienników:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-319">hello following example shows several ways toowrite logs:</span></span>

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

<span data-ttu-id="7c3e8-320">W hello pulpitu nawigacyjnego zestawu SDK zadań Webjob hello dane wyjściowe hello `TextWriter` pokazuje się po przejściu do strony toohello dla określonego wywołania funkcji i kliknij przycisk obiektów **Przełącz dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-320">In hello WebJobs SDK Dashboard, hello output from hello `TextWriter` object shows up when you go toohello page for a particular function invocation and click **Toggle Output**:</span></span>

![Kliknij łącze wywołania funkcji](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardinvocations.png)

![Dzienniki na stronie wywołania funkcji](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardlogs.png)

<span data-ttu-id="7c3e8-323">W hello pulpitu nawigacyjnego zestawu SDK zadań Webjob hello najnowszych 100 wierszy konsoli output Pokaż zapasowej przejdź na stronę toohello hello zadania WebJob (a nie dla wywołania funkcji hello) i kliknięcie **dane wyjściowe Przełącz**.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-323">In hello WebJobs SDK Dashboard, hello most recent 100 lines of Console output show up when you go toohello page for hello WebJob (not for hello function invocation) and click **Toggle Output**.</span></span>

![Kliknij przycisk przełączania danych wyjściowych](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/dashboardapplogs.png)

<span data-ttu-id="7c3e8-325">Ciągłe zadanie WebJob Dzienniki aplikacji wyświetlani w/data/zadania/ciągłego/*{webjobname}*/job_log.txt w systemie plików aplikacji hello w sieci web.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-325">In a continuous WebJob, application logs show up in /data/jobs/continuous/*{webjobname}*/job_log.txt in hello web app file system.</span></span>

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

<span data-ttu-id="7c3e8-326">W aplikacji hello obiektów blob platformy Azure dzienniki wyglądać następująco: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write — Witaj świecie! w, 2014-09-26T21:01:13, błąd, contosoadsnew, 491e54, 635473620738373502,0,17404,19,Console.error — Witaj świecie!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out — Witaj świecie!,</span><span class="sxs-lookup"><span data-stu-id="7c3e8-326">In an Azure blob hello application logs look like this: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13,Error,contosoadsnew,491e54,635473620738373502,0,17404,19,Console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,</span></span>

<span data-ttu-id="7c3e8-327">W tabeli platformy Azure hello `Console.Out` i `Console.Error` dzienniki wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="7c3e8-327">And in an Azure table hello `Console.Out` and `Console.Error` logs look like this:</span></span>

![Dziennik informacyjny w tabeli](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableinfo.png)

![Dziennik błędów w tabeli](./media/websites-dotnet-webjobs-sdk-storage-queues-how-to/tableerror.png)

<span data-ttu-id="7c3e8-330">Chcąc własne rejestratora tooplug, zobacz [w tym przykładzie](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-330">If you want tooplug in your own logger, see [this example](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Program.cs).</span></span>

## <span data-ttu-id="7c3e8-331"><a id="errors"></a>Jak błędy toohandle i Konfigurowanie limitów czasu</span><span class="sxs-lookup"><span data-stu-id="7c3e8-331"><a id="errors"></a>How toohandle errors and configure timeouts</span></span>
<span data-ttu-id="7c3e8-332">Witaj zestaw SDK zadań Webjob obejmuje również [limitu czasu](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) atrybut, który można użyć toocause toobe funkcji anulowana, jeśli nie zakończył się w określonym czasie.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-332">hello WebJobs SDK also includes a [Timeout](http://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs) attribute that you can use toocause a function toobe canceled if doesn't complete within a specified amount of time.</span></span> <span data-ttu-id="7c3e8-333">Jeśli chcesz tooraise alert, gdy wystąpi zbyt wiele błędów w danym okresie czasu, można użyć hello `ErrorTrigger` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-333">And if you want tooraise an alert when too many errors happen within a specified period of time, you can use hello `ErrorTrigger` attribute.</span></span> <span data-ttu-id="7c3e8-334">Oto [przykład ErrorTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-334">Here is an [ErrorTrigger example](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Error-Monitoring).</span></span>

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

<span data-ttu-id="7c3e8-335">Można też dynamicznie Wyłącz i Włącz funkcje toocontrol, czy one mogą być wyzwalane, za pomocą przełącznika konfiguracji, który może być ustawienie aplikacji lub nazwę zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-335">You can also dynamically disable and enable functions toocontrol whether they can be triggered, by using a configuration switch that could be an app setting or environment variable name.</span></span> <span data-ttu-id="7c3e8-336">Przykładowy kod, zobacz hello `Disable` atrybutu w [hello zestaw SDK zadań Webjob przykłady repozytorium](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-336">For sample code, see hello `Disable` attribute in [hello WebJobs SDK samples repository](https://github.com/Azure/azure-webjobs-sdk-samples/blob/master/BasicSamples/MiscOperations/Functions.cs).</span></span>

## <span data-ttu-id="7c3e8-337"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c3e8-337"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="7c3e8-338">W tym przewodniku dostarczył kodu przykłady przedstawiające sposób toohandle typowe scenariusze dotyczące pracy z kolejek platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c3e8-338">This guide has provided code samples that show how toohandle common scenarios for working with Azure queues.</span></span> <span data-ttu-id="7c3e8-339">Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="7c3e8-339">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>
