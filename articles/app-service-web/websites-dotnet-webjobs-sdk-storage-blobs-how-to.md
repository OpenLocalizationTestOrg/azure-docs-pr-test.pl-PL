---
title: "Jak korzystać z Magazynu obiektów blob platformy Azure przy użyciu zestawu SDK WebJobs"
description: "Dowiedz się, jak używać magazynu obiektów blob platformy Azure przy użyciu zestawu SDK zadań Webjob. Wyzwalanie proces po wyświetleniu nowego obiektu blob w kontenerze i obsługiwać \"skażone obiekty BLOB\"."
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
ms.openlocfilehash: e0a792ccdf8097d5cde254d6d4690a64838378ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-with-the-webjobs-sdk"></a><span data-ttu-id="57add-104">Jak korzystać z Magazynu obiektów blob platformy Azure przy użyciu zestawu SDK WebJobs</span><span class="sxs-lookup"><span data-stu-id="57add-104">How to use Azure blob storage with the WebJobs SDK</span></span>
## <a name="overview"></a><span data-ttu-id="57add-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="57add-105">Overview</span></span>
<span data-ttu-id="57add-106">Ten przewodnik zawiera C# przykłady kodu, których pokazano, jak do wyzwalania procesu podczas tworzenia lub aktualizowania obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57add-106">This guide provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="57add-107">Kod przykłady użycia [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="57add-107">The code samples use [WebJobs SDK](websites-dotnet-webjobs-sdk.md) version 1.x.</span></span>

<span data-ttu-id="57add-108">Aby uzyskać przykłady kodu, które pokazują, jak utworzyć obiekty BLOB, zobacz [jak używać magazynu kolejek Azure przy użyciu zestawu SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="57add-108">For code samples that show how to create blobs, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="57add-109">Przewodnik zakłada wiesz, [Tworzenie projektu zadania WebJob w programie Visual Studio z połączeniem ciągi prowadzące do konta magazynu](websites-dotnet-webjobs-sdk-get-started.md) lub [wielu kont magazynu](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="57add-109">The guide assumes you know [how to create a WebJob project in Visual Studio with connection strings that point to your storage account](websites-dotnet-webjobs-sdk-get-started.md) or to [multiple storage accounts](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span>

## <span data-ttu-id="57add-110"><a id="trigger"></a>Sposób włączania funkcji podczas tworzenia lub aktualizowania obiektu blob</span><span class="sxs-lookup"><span data-stu-id="57add-110"><a id="trigger"></a> How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="57add-111">W tej sekcji przedstawiono sposób użycia `BlobTrigger` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="57add-111">This section shows how to use the `BlobTrigger` attribute.</span></span> 

> [!NOTE]
> <span data-ttu-id="57add-112">Zestaw SDK zadań Webjob skanuje pliki dziennika, aby wyszukiwać nowych lub zmienionych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="57add-112">The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="57add-113">Ten proces nie jest w czasie rzeczywistym; funkcja może nie pobrać są uruchamiane kilka minut lub dłużej po utworzeniu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="57add-113">This process is not real-time; a function might not get triggered until several minutes or longer after the blob is created.</span></span> <span data-ttu-id="57add-114">Ponadto [magazynu dzienniki są tworzone na "starań"](https://msdn.microsoft.com/library/azure/hh343262.aspx) ciągły, lub nie ma żadnej gwarancji, że wszystkie zdarzenia zostaną przechwycone.</span><span class="sxs-lookup"><span data-stu-id="57add-114">In addition, [storage logs are created on a "best efforts"](https://msdn.microsoft.com/library/azure/hh343262.aspx) basis; there is no guarantee that all events will be captured.</span></span> <span data-ttu-id="57add-115">W niektórych warunkach może pominąć dzienników.</span><span class="sxs-lookup"><span data-stu-id="57add-115">Under some conditions, logs might be missed.</span></span> <span data-ttu-id="57add-116">Jeśli szybkość i niezawodność ograniczenia wyzwalacze obiektu blob nie są dozwolone dla aplikacji, zalecaną metodą jest utworzenie komunikatu w kolejce podczas tworzenia obiektu blob i użyj [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) zamiast atrybutu`BlobTrigger` atrybutu w funkcji, która przetwarza obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="57add-116">If the speed and reliability limitations of blob triggers are not acceptable for your application, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the `BlobTrigger` attribute on the function that processes the blob.</span></span>
> 
> 

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="57add-117">Jeden symbol zastępczy dla obiektu blob nazwy z rozszerzeniem</span><span class="sxs-lookup"><span data-stu-id="57add-117">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="57add-118">Poniższy przykładowy kod kopiuje tekst obiektów blob, które są widoczne w *wejściowych* kontener, aby *dane wyjściowe* kontenera:</span><span class="sxs-lookup"><span data-stu-id="57add-118">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="57add-119">Konstruktor atrybutu ma parametr typu string, który określa nazwę kontenera i nazwę obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="57add-119">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="57add-120">W tym przykładzie o nazwie obiektu blob *Blob1.txt* jest tworzony w *wejściowych* kontenera, funkcja ta umożliwia tworzenie obiektu blob o nazwie *Blob1.txt* w *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="57add-120">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span> 

<span data-ttu-id="57add-121">Wzorzec nazwy można określić za pomocą nazwy obiektu blob — symbol zastępczy, jak pokazano w poniższym przykładzie kodu:</span><span class="sxs-lookup"><span data-stu-id="57add-121">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="57add-122">Ten kod kopiuje tylko obiekty BLOB o nazwach rozpoczynających się od "oryginalnego-".</span><span class="sxs-lookup"><span data-stu-id="57add-122">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="57add-123">Na przykład *Blob1.txt oryginalne* w *wejściowych* kontenera jest kopiowany do *Blob1.txt kopiowania* w *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="57add-123">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="57add-124">Jeśli musisz określić wzorzec nazw dla nazwy obiektów blob, które mają nawiasy klamrowe w nazwie dwukrotnie nawiasów klamrowych.</span><span class="sxs-lookup"><span data-stu-id="57add-124">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="57add-125">Na przykład, jeśli chcesz znaleźć obiekty BLOB w *obrazów* kontenera, w którym mają nazwy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="57add-125">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="57add-126">Użyj tego deseniu:</span><span class="sxs-lookup"><span data-stu-id="57add-126">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="57add-127">W tym przykładzie *nazwa* wartość symbolu zastępczego będzie *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="57add-127">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span> 

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="57add-128">Symbole zastępcze nazwę i rozszerzenie oddzielnych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="57add-128">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="57add-129">Poniższy przykładowy kod powoduje zmianę rozszerzenia pliku jako kopiowania obiektów blob, które są widoczne w *wejściowych* kontener, aby *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="57add-129">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="57add-130">Kod rejestruje rozszerzenie *wejściowych* obiektu blob i Ustawia rozszerzenie *dane wyjściowe* obiektu blob do *.txt*.</span><span class="sxs-lookup"><span data-stu-id="57add-130">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <span data-ttu-id="57add-131"><a id="types"></a>Typy, które można powiązać obiekty BLOB</span><span class="sxs-lookup"><span data-stu-id="57add-131"><a id="types"></a> Types that you can bind to blobs</span></span>
<span data-ttu-id="57add-132">Można użyć `BlobTrigger` atrybutu w następujących typów:</span><span class="sxs-lookup"><span data-stu-id="57add-132">You can use the `BlobTrigger` attribute on the following types:</span></span>

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
* <span data-ttu-id="57add-133">Inne typy deserializacji przez [ICloudBlobStreamBinder](#icbsb)</span><span class="sxs-lookup"><span data-stu-id="57add-133">Other types deserialized by [ICloudBlobStreamBinder](#icbsb)</span></span> 

<span data-ttu-id="57add-134">Jeśli chcesz pracować bezpośrednio z kontem magazynu platformy Azure, możesz także dodać `CloudStorageAccount` parametru w podpisie metody.</span><span class="sxs-lookup"><span data-stu-id="57add-134">If you want to work directly with the Azure storage account, you can also add a `CloudStorageAccount` parameter to the method signature.</span></span>

<span data-ttu-id="57add-135">Aby uzyskać przykłady, zobacz [obiektu blob powiązanie kod w repozytorium zestaw sdk zadań webjob azure w witrynie GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="57add-135">For examples, see the [blob binding code in the azure-webjobs-sdk repository on GitHub.com](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/BlobBindingEndToEndTests.cs).</span></span>

## <span data-ttu-id="57add-136"><a id="string"></a>Pobieranie zawartości obiektu blob tekstu przez powiązanie do ciągu</span><span class="sxs-lookup"><span data-stu-id="57add-136"><a id="string"></a> Getting text blob content by binding to string</span></span>
<span data-ttu-id="57add-137">Jeśli oczekiwano tekstu w obiektach blob, `BlobTrigger` można zastosować do `string` parametru.</span><span class="sxs-lookup"><span data-stu-id="57add-137">If text blobs are expected, `BlobTrigger` can be applied to a `string` parameter.</span></span> <span data-ttu-id="57add-138">Poniższy przykładowy kod wiąże obiektu blob tekstu do `string` parametru o nazwie `logMessage`.</span><span class="sxs-lookup"><span data-stu-id="57add-138">The following code sample binds a text blob to a `string` parameter named `logMessage`.</span></span> <span data-ttu-id="57add-139">Funkcja używa parametru do zapisania zawartości obiektu blob do pulpitu nawigacyjnego, zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="57add-139">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span> 

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name, 
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <span data-ttu-id="57add-140"><a id="icbsb"></a>Pobieranie serializacji zawartość obiektu blob przy użyciu ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="57add-140"><a id="icbsb"></a> Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="57add-141">Poniższy przykład kodu wykorzystuje klasy, która implementuje `ICloudBlobStreamBinder` umożliwiające `BlobTrigger` atrybutu będzie tworzone powiązanie obiektu blob do `WebImage` typu.</span><span class="sxs-lookup"><span data-stu-id="57add-141">The following code sample uses a class that implements `ICloudBlobStreamBinder` to enable the `BlobTrigger` attribute to bind a blob to the `WebImage` type.</span></span>

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

<span data-ttu-id="57add-142">`WebImage` Powiązanie kod znajduje się w `WebImageBinder` klasą pochodzącą z `ICloudBlobStreamBinder`.</span><span class="sxs-lookup"><span data-stu-id="57add-142">The `WebImage` binding code is provided in a `WebImageBinder` class that derives from `ICloudBlobStreamBinder`.</span></span>

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

## <a name="getting-the-blob-path-for-the-triggering-blob"></a><span data-ttu-id="57add-143">Pobieranie ścieżki obiektu blob wyzwalająca obiektu blob</span><span class="sxs-lookup"><span data-stu-id="57add-143">Getting the blob path for the triggering blob</span></span>
<span data-ttu-id="57add-144">Aby uzyskać nazwę kontenera i nazwa obiektu blob obiektu blob, który ma wywołał funkcję, dołącz `blobTrigger` parametr w sygnaturze funkcji typu string.</span><span class="sxs-lookup"><span data-stu-id="57add-144">To get the container name and blob name of the blob that has triggered the function, include a `blobTrigger` string parameter in the function signature.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            string blobTrigger,
            TextWriter logger)
        {
             logger.WriteLine("Full blob path: {0}", blobTrigger);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }


## <span data-ttu-id="57add-145"><a id="poison"></a>Sposób obsługi skażone obiektów blob</span><span class="sxs-lookup"><span data-stu-id="57add-145"><a id="poison"></a> How to handle poison blobs</span></span>
<span data-ttu-id="57add-146">Gdy `BlobTrigger` funkcja kończy się niepowodzeniem, zestaw SDK wymaga go ponownie, w przypadku, gdy błąd został spowodowany przez błąd przejściowy.</span><span class="sxs-lookup"><span data-stu-id="57add-146">When a `BlobTrigger` function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="57add-147">Jeśli niepowodzenie jest spowodowane zawartość obiektu blob, funkcja zakończy się niepowodzeniem, za każdym razem, gdy próbuje przetworzyć obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="57add-147">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="57add-148">Domyślnie zestaw SDK wywołuje funkcję maksymalnie 5 razy dla danego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="57add-148">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="57add-149">Jeśli piątym spróbuj kończy się niepowodzeniem, zestaw SDK dodaje komunikat do kolejki o nazwie *webjob blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="57add-149">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="57add-150">Konfiguruje się maksymalnej liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="57add-150">The maximum number of retries is configurable.</span></span> <span data-ttu-id="57add-151">Taki sam [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ustawienie służy do obsługi skażone obiektów blob i kolejki skażone komunikat — Obsługa.</span><span class="sxs-lookup"><span data-stu-id="57add-151">The same [MaxDequeueCount](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span> 

<span data-ttu-id="57add-152">Komunikat z kolejki skażone obiektów blob jest obiekt JSON, który zawiera następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="57add-152">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="57add-153">FunctionId (w formacie *{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*, na przykład: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="57add-153">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="57add-154">BlobType ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="57add-154">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="57add-155">Właściwość ContainerName</span><span class="sxs-lookup"><span data-stu-id="57add-155">ContainerName</span></span>
* <span data-ttu-id="57add-156">Element BlobName</span><span class="sxs-lookup"><span data-stu-id="57add-156">BlobName</span></span>
* <span data-ttu-id="57add-157">Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="57add-157">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="57add-158">W poniższym przykładzie kodu `CopyBlob` funkcja ma kod powodujący niepowodzenie za każdym razem, gdy jest ona wywoływana.</span><span class="sxs-lookup"><span data-stu-id="57add-158">In the following code sample, the `CopyBlob` function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="57add-159">Po zestaw SDK wymaga on maksymalnej liczby ponownych prób, wiadomość jest tworzony w kolejce skażone obiektów blob, a ten komunikat jest przetwarzany przez `LogPoisonBlob` funkcji.</span><span class="sxs-lookup"><span data-stu-id="57add-159">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the `LogPoisonBlob` function.</span></span> 

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

<span data-ttu-id="57add-160">Zestaw SDK automatycznie deserializuje komunikat JSON.</span><span class="sxs-lookup"><span data-stu-id="57add-160">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="57add-161">Oto `PoisonBlobMessage` klasy:</span><span class="sxs-lookup"><span data-stu-id="57add-161">Here is the `PoisonBlobMessage` class:</span></span> 

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <span data-ttu-id="57add-162"><a id="polling"></a>Algorytm sondowania obiektów blob</span><span class="sxs-lookup"><span data-stu-id="57add-162"><a id="polling"></a> Blob polling algorithm</span></span>
<span data-ttu-id="57add-163">Zestaw SDK zadań Webjob skanuje wszystkie kontenery określony przez `BlobTrigger` atrybuty podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="57add-163">The WebJobs SDK scans all containers specified by `BlobTrigger` attributes at application start.</span></span> <span data-ttu-id="57add-164">Na koncie magazynu dużych ten tryb skanowania może zająć trochę czasu, dlatego może być trochę czasu, zanim znajdują się nowe obiekty BLOB i `BlobTrigger` funkcje są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="57add-164">In a large storage account this scan can take some time, so it might be a while before new blobs are found and `BlobTrigger` functions are executed.</span></span>

<span data-ttu-id="57add-165">Aby wykryć nowe lub zmienione obiekty BLOB po uruchomieniu aplikacji, zestaw SDK okresowo odczytuje z dzienników magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="57add-165">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="57add-166">Dzienniki obiektów blob są buforowane oraz tylko fizycznie zapisane co 10 minut lub tak, więc mogą występować znaczne opóźnienie po obiektu blob jest tworzony lub aktualizowany przed odpowiadającego `BlobTrigger` wykonuje funkcji.</span><span class="sxs-lookup"><span data-stu-id="57add-166">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding `BlobTrigger` function executes.</span></span> 

<span data-ttu-id="57add-167">Występuje wyjątek dla obiektów blob, które utworzono za pomocą `Blob` atrybutu.</span><span class="sxs-lookup"><span data-stu-id="57add-167">There is an exception for blobs that you create by using the `Blob` attribute.</span></span> <span data-ttu-id="57add-168">Gdy zestaw SDK zadań Webjob tworzy nowy obiekt blob, przekazaniem nowego obiektu blob natychmiast żadnych zgodnych `BlobTrigger` funkcji.</span><span class="sxs-lookup"><span data-stu-id="57add-168">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching `BlobTrigger` functions.</span></span> <span data-ttu-id="57add-169">W związku z tym jeśli łańcuch blob wejściach i wyjściach, zestaw SDK może je przetwarzać wydajnie.</span><span class="sxs-lookup"><span data-stu-id="57add-169">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="57add-170">Ale jeśli chcesz małych opóźnieniach uruchomiona z obiektu blob funkcji przetwarzania dla obiektów blob, które są tworzone lub zaktualizowany w inny sposób, firma Microsoft zaleca używanie `QueueTrigger` zamiast `BlobTrigger`.</span><span class="sxs-lookup"><span data-stu-id="57add-170">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using `QueueTrigger` rather than `BlobTrigger`.</span></span>

### <span data-ttu-id="57add-171"><a id="receipts"></a>Potwierdzenia obiektów blob</span><span class="sxs-lookup"><span data-stu-id="57add-171"><a id="receipts"></a> Blob receipts</span></span>
<span data-ttu-id="57add-172">Zestaw SDK zadań Webjob, sprawdza nie `BlobTrigger` funkcja jest wywoływana więcej niż raz dla tego samego obiektu blob nowe lub zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="57add-172">The WebJobs SDK makes sure that no `BlobTrigger` function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="57add-173">Dzieje się tak dzięki utrzymywaniu *obiektu blob potwierdzenia* w celu ustalenia, czy wersja danego obiektu blob został przetworzony.</span><span class="sxs-lookup"><span data-stu-id="57add-173">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="57add-174">Potwierdzenia obiektów blob są przechowywane w kontenerze o nazwie *azure webjobs hostów* w określona przez ciąg połączenia AzureWebJobsStorage konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="57add-174">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="57add-175">Potwierdzenie obiektu blob zawiera następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="57add-175">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="57add-176">Funkcja, która została wywołana dla obiektu blob ("*{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*", na przykład:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="57add-176">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="57add-177">Nazwa kontenera</span><span class="sxs-lookup"><span data-stu-id="57add-177">The container name</span></span>
* <span data-ttu-id="57add-178">Typ obiektów blob ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="57add-178">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="57add-179">Nazwa obiektu blob</span><span class="sxs-lookup"><span data-stu-id="57add-179">The blob name</span></span>
* <span data-ttu-id="57add-180">Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="57add-180">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="57add-181">Jeśli chcesz wymusić ponowne przetworzenie obiektu blob, należy ręcznie usunąć potwierdzenia obiektu blob dla tego obiektu blob z *azure webjobs hostów* kontenera.</span><span class="sxs-lookup"><span data-stu-id="57add-181">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <span data-ttu-id="57add-182"><a id="queues"></a>Tematy pokrewne objętych artykułem kolejek</span><span class="sxs-lookup"><span data-stu-id="57add-182"><a id="queues"></a>Related topics covered by the queues article</span></span>
<span data-ttu-id="57add-183">Informacje dotyczące obsługi przetwarzania obiektu blob wyzwalane przez komunikatu w kolejce, lub zestaw SDK zadań Webjob do obiektu blob nie są typowe scenariusze przetwarzania, zobacz [jak używać magazynu kolejek Azure przy użyciu zestawu SDK zadań Webjob](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="57add-183">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span> 

<span data-ttu-id="57add-184">Tematy pokrewne omówione w tym artykule są następujące:</span><span class="sxs-lookup"><span data-stu-id="57add-184">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="57add-185">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="57add-185">Async functions</span></span>
* <span data-ttu-id="57add-186">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="57add-186">Multiple instances</span></span>
* <span data-ttu-id="57add-187">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="57add-187">Graceful shutdown</span></span>
* <span data-ttu-id="57add-188">Użyj zestawu SDK zadań Webjob atrybutów w treści funkcji</span><span class="sxs-lookup"><span data-stu-id="57add-188">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="57add-189">Ustaw parametry połączenia SDK w kodzie.</span><span class="sxs-lookup"><span data-stu-id="57add-189">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="57add-190">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="57add-190">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="57add-191">Skonfiguruj `MaxDequeueCount` obsługi skażone obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="57add-191">Configure `MaxDequeueCount` for poison blob handling.</span></span>
* <span data-ttu-id="57add-192">Wyzwalanie funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="57add-192">Trigger a function manually</span></span>
* <span data-ttu-id="57add-193">Zapisywanie dzienników</span><span class="sxs-lookup"><span data-stu-id="57add-193">Write logs</span></span>

## <span data-ttu-id="57add-194"><a id="nextsteps"></a> Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57add-194"><a id="nextsteps"></a> Next steps</span></span>
<span data-ttu-id="57add-195">W tym przewodniku udostępnił przykłady kodu, które przedstawiają sposób obsługi typowe scenariusze dotyczące pracy z obiektami blob Azure.</span><span class="sxs-lookup"><span data-stu-id="57add-195">This guide has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="57add-196">Aby uzyskać więcej informacji o sposobie używania zadań Webjob Azure i zestaw SDK zadań Webjob, zobacz [zasobów zalecane zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="57add-196">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs Recommended Resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

