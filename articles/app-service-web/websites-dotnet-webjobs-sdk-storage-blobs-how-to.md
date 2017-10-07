---
title: "toouse aaaHow magazynu obiektów blob platformy Azure z hello zestaw SDK zadań Webjob"
description: "Dowiedz się, jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob. Wyzwalanie proces po wyświetleniu nowego obiektu blob w kontenerze i obsługiwać \"skażone obiekty BLOB\"."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.assetid: bf32f919-f7bc-4aaa-916e-461c02f2e26c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: b34ea8cffee7c0475641886150dee521130a3132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-with-hello-webjobs-sdk"></a><span data-ttu-id="6ca78-104">Jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="6ca78-104">How toouse Azure blob storage with hello WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="6ca78-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6ca78-105">Overview</span></span>
<span data-ttu-id="6ca78-106">Ten przewodnik zawiera C# jak przykłady kodu przedstawiające tootrigger procesu podczas tworzenia lub aktualizowania obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6ca78-106">This guide provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="6ca78-107">Przykłady kodu Hello użyj [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="6ca78-107">hello code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="6ca78-108">Aby uzyskać przykłady kodu, które pokazują, jak obiekty BLOB toocreate, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="6ca78-108">For code samples that show how toocreate blobs, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="6ca78-109">Witaj przewodnika przyjęto założenia, wiadomo, [jak toocreate projektu zadania WebJob w programie Visual Studio z połączeniem ciągi konto magazynu punktu tooyour](websites-dotnet-webjobs-sdk-get-started.md) lub zbyt[wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="6ca78-109">hello guide assumes you know [how toocreate a WebJob project in Visual Studio with connection strings that point tooyour storage account](websites-dotnet-webjobs-sdk-get-started.md) or too[multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="6ca78-110"><a id="trigger"></a>Jak tootrigger funkcja, gdy obiekt blob jest tworzony lub aktualizowany</span><span class="sxs-lookup"><span data-stu-id="6ca78-110"><a id="trigger"></a> How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="6ca78-111">W tej sekcji przedstawiono sposób toouse hello `BlobTrigger` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="6ca78-111">This section shows how toouse hello `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="6ca78-112">zestaw SDK zadań Webjob skanowania dziennika Hello pliki toowatch dla nowych lub zmienionych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="6ca78-112">hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="6ca78-113">Ten proces nie jest w czasie rzeczywistym; funkcja może nie pobrać są uruchamiane kilka minut lub dłużej po utworzeniu obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="6ca78-113">This process is not real-time; a function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="6ca78-114">Ponadto [magazynu dzienniki są tworzone na "starań"](https://msdn.microsoft.com/library/azure/hh343262.aspx) ciągły, lub nie ma żadnej gwarancji, że wszystkie zdarzenia zostaną przechwycone.</span><span class="sxs-lookup"><span data-stu-id="6ca78-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="6ca78-115">W niektórych warunkach może pominąć dzienników.</span><span class="sxs-lookup"><span data-stu-id="6ca78-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="6ca78-116">Jeśli ograniczenia szybkości i niezawodności hello wyzwalaczy obiektu blob nie są dozwolone dla aplikacji, hello zalecana metoda jest toocreate komunikatu w kolejce, podczas tworzenia obiektu blob hello i użyj hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atrybutu zamiast Witaj `BlobTrigger` atrybutu w funkcji hello, który przetwarza hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="6ca78-116">If hello speed and reliability limitations of blob triggers are not acceptable for your application, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello `BlobTrigger` attribute on hello function that processes hello blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="6ca78-117">Jeden symbol zastępczy dla obiektu blob nazwy z rozszerzeniem</span><span class="sxs-lookup"><span data-stu-id="6ca78-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="6ca78-118">Witaj Poniższy przykładowy kod kopiuje tekst obiektów blob, które pojawiają się w hello *wejściowych* toohello kontenera *dane wyjściowe* kontenera:</span><span class="sxs-lookup"><span data-stu-id="6ca78-118">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="6ca78-119">Hello Konstruktor atrybutu ma parametr ciąg, który określa nazwę kontenera hello i hello nazwę obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="6ca78-119">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="6ca78-120">W tym przykładzie o nazwie obiektu blob *Blob1.txt* jest tworzony w hello *wejściowych* kontenera, funkcja hello tworzy obiektu blob o nazwie *Blob1.txt* w hello *danych wyjściowych*  kontenera.</span><span class="sxs-lookup"><span data-stu-id="6ca78-120">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span> 

<span data-ttu-id="6ca78-121">Wzorzec nazwy można określić za pomocą hello blob nazwa symbolu zastępczego, jak pokazano w powitania po przykładowy kod:</span><span class="sxs-lookup"><span data-stu-id="6ca78-121">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="6ca78-122">Ten kod kopiuje tylko obiekty BLOB o nazwach rozpoczynających się od "oryginalnego-".</span><span class="sxs-lookup"><span data-stu-id="6ca78-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="6ca78-123">Na przykład *Blob1.txt oryginalne* w hello *wejściowych* kontenera jest kopiowana za*Blob1.txt kopiowania* w hello *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="6ca78-123">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="6ca78-124">Jeśli potrzebujesz toospecify wzorzec nazw dla nazwy obiektów blob, które mają nawiasy klamrowe w nazwie hello dwukrotnie hello nawiasów klamrowych.</span><span class="sxs-lookup"><span data-stu-id="6ca78-124">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="6ca78-125">Na przykład, jeśli chcesz, aby obiekty BLOB toofind na powitania *obrazów* kontenera, w którym mają nazwy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="6ca78-125">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="6ca78-126">Użyj tego deseniu:</span><span class="sxs-lookup"><span data-stu-id="6ca78-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="6ca78-127">Przykład Witaj Witaj *nazwa* wartość symbolu zastępczego będzie *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="6ca78-127">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="6ca78-128">Symbole zastępcze nazwę i rozszerzenie oddzielnych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="6ca78-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="6ca78-129">Witaj następujące zmiany przykładowy kod hello rozszerzenie pliku jako kopiuje obiektów blob, które są wyświetlane w hello *wejściowych* toohello kontenera *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="6ca78-129">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="6ca78-130">Kod Hello rejestruje rozszerzenie hello hello *wejściowych* obiektu blob i Ustawia rozszerzenie hello hello *dane wyjściowe* obiektów blob za*.txt*.</span><span class="sxs-lookup"><span data-stu-id="6ca78-130">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

        public static void CopyBlobToTxtFile([BlobTrigger("input/{name}.{ext}")] TextReader input,
            [Blob("output/{name}.txt")] out string output,
            string name,
            string ext,
            TextWriter logger)
        {
            logger.WriteLine("Blob name:" + name);
            logger.WriteLine("Blob extension:" + ext);
            output = input.ReadToEnd();
        }

## <span data-ttu-id="6ca78-131"><a id="types"></a>Czy można powiązać tooblobs typów</span><span class="sxs-lookup"><span data-stu-id="6ca78-131"><a id="types"></a> Types that you can bind tooblobs</span></span>
<span data-ttu-id="6ca78-132">Można użyć hello `BlobTrigger` atrybutu na powitania następujące typy:</span><span class="sxs-lookup"><span data-stu-id="6ca78-132">You can use hello `BlobTrigger` attribute on hello following types:</span></span>

* `string`
* `TextReader`
* `Stream`
* `ICloudBlob`
* `CloudBlockBlob`
* `CloudPageBlob`
* `CloudBlobContainer`
* `CloudBlobDirectory`
* `IEnumerable<CloudBlockBlob>`
* `IEnumerable<CloudPageBlob>`
* <span data-ttu-id="6ca78-133">Inne typy deserializacji przez [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="6ca78-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="6ca78-134">Jeśli chcesz toowork bezpośrednio z hello kontem magazynu platformy Azure, możesz także dodać `CloudStorageAccount` podpis metody toohello parametru.</span><span class="sxs-lookup"><span data-stu-id="6ca78-134">If you want toowork directly with hello Azure storage account, you can also add a `CloudStorageAccount` parameter toohello method signature.</span></span>

<span data-ttu-id="6ca78-135">Przykłady można znaleźć hello [obiektu blob powiązanie kod w repozytorium zestaw sdk zadań webjob azure hello w witrynie GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="6ca78-135">For examples, see hello [blob binding code in hello azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="6ca78-136"><a id="string"></a>Pobieranie zawartości obiektu blob tekstu przez powiązanie toostring</span><span class="sxs-lookup"><span data-stu-id="6ca78-136"><a id="string"></a> Getting text blob content by binding toostring</span></span>
<span data-ttu-id="6ca78-137">Jeśli oczekiwano tekstu w obiektach blob, `BlobTrigger` może być zastosowane tooa `string` parametru.</span><span class="sxs-lookup"><span data-stu-id="6ca78-137">If text blobs are expected, `BlobTrigger` can be applied tooa `string` parameter.</span></span> <span data-ttu-id="6ca78-138">Witaj Poniższy przykładowy kod wiąże tooa obiektu blob tekst `string` parametru o nazwie `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="6ca78-138">hello following code sample binds a text blob tooa `string` parameter named `logMessage`.</span></span> <span data-ttu-id="6ca78-139">Funkcja Hello korzysta zawartości hello toowrite parametru tego toohello obiektu blob hello zestaw SDK zadań Webjob pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6ca78-139">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="6ca78-140"><a id="icbsb"></a>Pobieranie serializacji zawartość obiektu blob przy użyciu ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="6ca78-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="6ca78-141">Witaj Poniższy przykładowy kod używa klasy, która implementuje `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` toobind toohello obiektu blob atrybutu `WebImage` typu.</span><span class="sxs-lookup"><span data-stu-id="6ca78-141">hello following code sample uses a class that implements `ICloudBlobStreamBinder` tooenable hello `BlobTrigger` attribute toobind a blob toohello `WebImage` type.</span></span>

        public static void WaterMark(
            [BlobTrigger("images3/{name}")] WebImage input,
            [Blob("images3-watermarked/{name}")] out WebImage output)
        {
            output = input.AddTextWatermark("WebJobs SDK", 
                horizontalAlign: "Center", verticalAlign: "Middle",
                fontSize: 48, opacity: 50);
        }
        public static void Resize(
            [BlobTrigger("images3-watermarked/{name}")] WebImage input,
            [Blob("images3-resized/{name}")] out WebImage output)
        {
            var width = 180;
            var height = Convert.ToInt32(input.Height * 180 / input.Width);
            output = input.Resize(width, height);
        }

<span data-ttu-id="6ca78-142">Witaj `WebImage` powiązanie kod znajduje się w `WebImageBinder` klasą pochodzącą z `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="6ca78-142">hello `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

        public class WebImageBinder : ICloudBlobStreamBinder<WebImage>
        {
            public Task<WebImage> ReadFromStreamAsync(Stream input, 
                System.Threading.CancellationToken cancellationToken)
            {
                return Task.FromResult<WebImage>(new WebImage(input));
            }
            public Task WriteToStreamAsync(WebImage value, Stream output,
                System.Threading.CancellationToken cancellationToken)
            {
                var bytes = value.GetBytes();
                return output.WriteAsync(bytes, 0, bytes.Length, cancellationToken);
            }
        }

## <a name="getting-hello-blob-path-for-hello-triggering-blob"></a><span data-ttu-id="6ca78-143">Trwa pobieranie ścieżka obiektu blob hello hello wyzwalania obiektów blob</span><span class="sxs-lookup"><span data-stu-id="6ca78-143">Getting hello blob path for hello triggering blob</span></span>
<span data-ttu-id="6ca78-144">Nazwa kontenera hello tooget i nazwa obiektu blob hello obiektu blob, który wyzwolił funkcja hello obejmują `blobTrigger` parametr w sygnaturze funkcji hello typu string.</span><span class="sxs-lookup"><span data-stu-id="6ca78-144">tooget hello container name and blob name of hello blob that has triggered hello function, include a `blobTrigger` string parameter in hello function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="6ca78-145"><a id="poison"></a>Jak obiekty BLOB toohandle poison</span><span class="sxs-lookup"><span data-stu-id="6ca78-145"><a id="poison"></a> How toohandle poison blobs</span></span>
<span data-ttu-id="6ca78-146">Gdy `BlobTrigger` funkcja kończy się niepowodzeniem, hello zestawu SDK wywołania go ponownie, w przypadku hello błąd został spowodowany przez błąd przejściowy.</span><span class="sxs-lookup"><span data-stu-id="6ca78-146">When a `BlobTrigger` function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="6ca78-147">Jeśli hello jest przyczyną niepowodzenia hello zawartości obiektu hello blob, funkcja hello zakończy się niepowodzeniem, zawsze próbuje tooprocess hello blob.</span><span class="sxs-lookup"><span data-stu-id="6ca78-147">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="6ca78-148">Domyślnie program hello SDK wywołuje funkcję się too5 razy dla danego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="6ca78-148">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="6ca78-149">W przypadku niepowodzenia spróbuj piątym powitania hello SDK dodaje tooa kolejki komunikatów o nazwie *webjob blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="6ca78-149">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="6ca78-150">konfiguruje się Hello maksymalnej liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="6ca78-150">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="6ca78-151">Witaj sam [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ustawienie służy do obsługi skażone obiektów blob i kolejki skażone komunikat — Obsługa.</span><span class="sxs-lookup"><span data-stu-id="6ca78-151">hello same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="6ca78-152">komunikat z kolejki Hello skażone obiektów blob jest obiekt JSON, który zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="6ca78-152">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="6ca78-153">FunctionId (w formacie hello *{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*, na przykład: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="6ca78-153">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="6ca78-154">BlobType ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="6ca78-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="6ca78-155">Właściwość ContainerName</span><span class="sxs-lookup"><span data-stu-id="6ca78-155">ContainerName</span></span>
* <span data-ttu-id="6ca78-156">Element BlobName</span><span class="sxs-lookup"><span data-stu-id="6ca78-156">BlobName</span></span>
* <span data-ttu-id="6ca78-157">Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6ca78-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="6ca78-158">W następujących hello kodu próbki hello `CopyBlob` funkcja ma kod powodujący toofail za każdym razem, gdy jest ona wywoływana.</span><span class="sxs-lookup"><span data-stu-id="6ca78-158">In hello following code sample, hello `CopyBlob` function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="6ca78-159">Po hello zestaw SDK wymaga on hello maksymalnej liczby ponownych prób, wiadomość jest tworzona na powitania skażone blob kolejki, a ten komunikat jest przetwarzany przez hello `LogPoisonBlob` funkcji.</span><span class="sxs-lookup"><span data-stu-id="6ca78-159">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello `LogPoisonBlob` function.</span></span> 

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("textblobs/output-{name}")] out string output)
        {
            throw new Exception("Exception for testing poison blob handling");
            output = input.ReadToEnd();
        }

        public static void LogPoisonBlob(
        [QueueTrigger("webjobs-blobtrigger-poison")] PoisonBlobMessage message,
            TextWriter logger)
        {
            logger.WriteLine("FunctionId: {0}", message.FunctionId);
            logger.WriteLine("BlobType: {0}", message.BlobType);
            logger.WriteLine("ContainerName: {0}", message.ContainerName);
            logger.WriteLine("BlobName: {0}", message.BlobName);
            logger.WriteLine("ETag: {0}", message.ETag);
        }

<span data-ttu-id="6ca78-160">Witaj SDK automatycznie deserializuje wiadomości powitania JSON.</span><span class="sxs-lookup"><span data-stu-id="6ca78-160">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="6ca78-161">Oto hello `PoisonBlobMessage` klasy:</span><span class="sxs-lookup"><span data-stu-id="6ca78-161">Here is hello `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="6ca78-162"><a id="polling"></a>Algorytm sondowania obiektów blob</span><span class="sxs-lookup"><span data-stu-id="6ca78-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="6ca78-163">Witaj zestaw SDK zadań Webjob skanuje wszystkie kontenery określony przez `BlobTrigger` atrybuty podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6ca78-163">hello WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="6ca78-164">Na koncie magazynu dużych ten tryb skanowania może zająć trochę czasu, dlatego może być trochę czasu, zanim znajdują się nowe obiekty BLOB i `BlobTrigger` funkcje są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="6ca78-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="6ca78-165">rejestruje powitalne SDK okresowo odczytuje z magazynu obiektów blob hello toodetect nowych lub zmienionych obiektów blob w po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6ca78-165">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="6ca78-166">Witaj dzienniki obiektów blob są buforowane i tylko fizycznie zapisane co 10 minut lub tak, więc mogą występować znaczne opóźnienia po obiektu blob jest tworzony lub aktualizowany przed odpowiadającego hello `BlobTrigger` wykonuje funkcji.</span><span class="sxs-lookup"><span data-stu-id="6ca78-166">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="6ca78-167">Brak wyjątek dla obiektów blob, które są tworzone przy użyciu hello `Blob` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="6ca78-167">There is an exception for blobs that you create by using hello `Blob` attribute.</span></span> <span data-ttu-id="6ca78-168">Gdy hello zestaw SDK zadań Webjob tworzy nowy obiekt blob, natychmiast przekazaniem nowego obiektu blob hello dopasowania tooany `BlobTrigger` funkcji.</span><span class="sxs-lookup"><span data-stu-id="6ca78-168">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching `BlobTrigger` functions.</span></span> <span data-ttu-id="6ca78-169">W związku z tym jeśli łańcuch blob wejściach i wyjściach, hello SDK może je przetwarzać wydajnie.</span><span class="sxs-lookup"><span data-stu-id="6ca78-169">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="6ca78-170">Ale jeśli chcesz małych opóźnieniach uruchomiona z obiektu blob funkcji przetwarzania dla obiektów blob, które są tworzone lub zaktualizowany w inny sposób, firma Microsoft zaleca używanie `QueueTrigger` zamiast `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="6ca78-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="6ca78-171"><a id="receipts"></a>Potwierdzenia obiektów blob</span><span class="sxs-lookup"><span data-stu-id="6ca78-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="6ca78-172">zestaw SDK zadań Webjob Hello, sprawdza nie `BlobTrigger` funkcja jest wywoływana więcej niż raz dla hello sam nowe lub zaktualizowane obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="6ca78-172">hello WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="6ca78-173">Dzieje się tak dzięki utrzymywaniu *obiektu blob potwierdzenia* w kolejności toodetermine wersji danego obiektu blob został przetworzony.</span><span class="sxs-lookup"><span data-stu-id="6ca78-173">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="6ca78-174">Potwierdzenia obiektów blob są przechowywane w kontenerze o nazwie *azure webjobs hostów* na koncie magazynu Azure hello określona przez ciąg połączenia AzureWebJobsStorage hello.</span><span class="sxs-lookup"><span data-stu-id="6ca78-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="6ca78-175">Potwierdzenie obiektu blob ma hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="6ca78-175">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="6ca78-176">Funkcja, która została wywołana dla obiektu blob hello Hello ("*{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*", na przykład:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="6ca78-176">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="6ca78-177">Nazwa kontenera Hello</span><span class="sxs-lookup"><span data-stu-id="6ca78-177">hello container name</span></span>
* <span data-ttu-id="6ca78-178">Typ obiektu blob Hello ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="6ca78-178">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="6ca78-179">Nazwa obiektu blob Hello</span><span class="sxs-lookup"><span data-stu-id="6ca78-179">hello blob name</span></span>
* <span data-ttu-id="6ca78-180">Witaj ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="6ca78-180">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="6ca78-181">Jeśli chcesz tooforce ponowne przetworzenie obiektu blob, można ręcznie usunąć hello potwierdzenia obiektu blob dla tego obiektu blob z hello *azure webjobs hostów* kontenera.</span><span class="sxs-lookup"><span data-stu-id="6ca78-181">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="6ca78-182"><a id="queues"></a>Tematy pokrewne objętych hello kolejek artykułu</span><span class="sxs-lookup"><span data-stu-id="6ca78-182"><a id="queues"></a>Related topics covered by hello queues article</span></span>
<span data-ttu-id="6ca78-183">Informacje dotyczące sposobu przetwarzania obiektu blob toohandle wyzwalane komunikatu w kolejce, lub dla zadań Webjob scenariusze zestawu SDK nie określonych tooblob przetwarzania, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="6ca78-183">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="6ca78-184">Tematy pokrewne omówione w tym artykule Uwzględnij hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6ca78-184">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="6ca78-185">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="6ca78-185">Async functions</span></span>
* <span data-ttu-id="6ca78-186">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="6ca78-186">Multiple instances</span></span>
* <span data-ttu-id="6ca78-187">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="6ca78-187">Graceful shutdown</span></span>
* <span data-ttu-id="6ca78-188">Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji</span><span class="sxs-lookup"><span data-stu-id="6ca78-188">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="6ca78-189">Ustawianie parametrów połączenia SDK hello w kodzie.</span><span class="sxs-lookup"><span data-stu-id="6ca78-189">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="6ca78-190">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="6ca78-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="6ca78-191">Skonfiguruj `MaxDequeueCount` obsługi skażone obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="6ca78-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="6ca78-192">Wyzwalanie funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="6ca78-192">Trigger a function manually</span></span>
* <span data-ttu-id="6ca78-193">Zapisywanie dzienników</span><span class="sxs-lookup"><span data-stu-id="6ca78-193">Write logs</span></span>

## <span data-ttu-id="6ca78-194"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ca78-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="6ca78-195">W tym przewodniku udostępnił przykłady kodu przedstawiające jak obiekty BLOB toohandle typowe scenariusze dotyczące pracy z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="6ca78-195">This guide has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="6ca78-196">Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="6ca78-196">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

