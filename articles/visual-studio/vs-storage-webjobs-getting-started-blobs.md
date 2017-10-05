---
title: "Rozpoczynanie pracy z obiektu blob magazynu i Visual Studio połączone usługi (projekty zadania WebJob) | Dokumentacja firmy Microsoft"
description: "Jak rozpocząć korzystanie z magazynu obiektów Blob projektu zadania WebJob, po nawiązaniu połączenia z magazynem platformy Azure przy użyciu programu Visual Studio połączone usługi."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: a50a265feff8c0aec28825eb0bc4e33585ea5a02
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="56e49-103">Wprowadzenie do obiektów Blob platformy Azure magazynu i Visual Studio połączone usługi (zadania WebJob projekty)</span><span class="sxs-lookup"><span data-stu-id="56e49-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="56e49-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="56e49-104">Overview</span></span>
<span data-ttu-id="56e49-105">Ten artykuł zawiera C# przykłady kodu, których pokazano, jak do wyzwalania procesu podczas tworzenia lub aktualizowania obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="56e49-105">This article provides C# code samples that show how to trigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="56e49-106">Kod przykłady użycia [zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="56e49-106">The code samples use the [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="56e49-107">Podczas dodawania konta magazynu do projektu zadania WebJob za pomocą programu Visual Studio **dodać usług połączonych** okna dialogowego, odpowiedniego pakietu NuGet usługi Magazyn Azure jest zainstalowany, odpowiednie odwołania .NET są dodawane do projektu i parametry połączenia dla konta magazynu są aktualizowane w pliku App.config.</span><span class="sxs-lookup"><span data-stu-id="56e49-107">When you add a storage account to a WebJob project by using the Visual Studio **Add Connected Services** dialog, the appropriate Azure Storage NuGet package is installed, the appropriate .NET references are added to the project, and connection strings for the storage account are updated in the App.config file.</span></span>

## <a name="how-to-trigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="56e49-108">Sposób włączania funkcji podczas tworzenia lub aktualizowania obiektu blob</span><span class="sxs-lookup"><span data-stu-id="56e49-108">How to trigger a function when a blob is created or updated</span></span>
<span data-ttu-id="56e49-109">W tej sekcji przedstawiono sposób użycia **BlobTrigger** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="56e49-109">This section shows how to use the **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="56e49-110">**Uwaga:** zestaw SDK zadań Webjob skanuje pliki dzienników, które należy obserwować nowych lub zmienionych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="56e49-110">**Note:** The WebJobs SDK scans log files to watch for new or changed blobs.</span></span> <span data-ttu-id="56e49-111">Ten proces jest z założenia powolne; funkcja może nie pobrać są uruchamiane kilka minut lub dłużej po utworzeniu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="56e49-111">This process is inherently slow; a function might not get triggered until several minutes or longer after the blob is created.</span></span>  <span data-ttu-id="56e49-112">Jeśli aplikacja wymaga natychmiast przetwarza obiekty BLOB, zalecaną metodą jest utworzenie komunikatu w kolejce podczas tworzenia obiektu blob i użyj [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) atrybutu zamiast **BlobTrigger** atrybutu w funkcji, która przetwarza obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="56e49-112">If your application needs to process blobs immediately, the recommended method is to create a queue message when you create the blob, and use the [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of the **BlobTrigger** attribute on the function that processes the blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="56e49-113">Jeden symbol zastępczy dla obiektu blob nazwy z rozszerzeniem</span><span class="sxs-lookup"><span data-stu-id="56e49-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="56e49-114">Poniższy przykładowy kod kopiuje tekst obiektów blob, które są widoczne w *wejściowych* kontener, aby *dane wyjściowe* kontenera:</span><span class="sxs-lookup"><span data-stu-id="56e49-114">The following code sample copies text blobs that appear in the *input* container to the *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="56e49-115">Konstruktor atrybutu ma parametr typu string, który określa nazwę kontenera i nazwę obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="56e49-115">The attribute constructor takes a string parameter that specifies the container name and a placeholder for the blob name.</span></span> <span data-ttu-id="56e49-116">W tym przykładzie o nazwie obiektu blob *Blob1.txt* jest tworzony w *wejściowych* kontenera, funkcja ta umożliwia tworzenie obiektu blob o nazwie *Blob1.txt* w *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="56e49-116">In this example, if a blob named *Blob1.txt* is created in the *input* container, the function creates a blob named *Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="56e49-117">Wzorzec nazwy można określić za pomocą nazwy obiektu blob — symbol zastępczy, jak pokazano w poniższym przykładzie kodu:</span><span class="sxs-lookup"><span data-stu-id="56e49-117">You can specify a name pattern with the blob name placeholder, as shown in the following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="56e49-118">Ten kod kopiuje tylko obiekty BLOB o nazwach rozpoczynających się od "oryginalnego-".</span><span class="sxs-lookup"><span data-stu-id="56e49-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="56e49-119">Na przykład *Blob1.txt oryginalne* w *wejściowych* kontenera jest kopiowany do *Blob1.txt kopiowania* w *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="56e49-119">For example, *original-Blob1.txt* in the *input* container is copied to *copy-Blob1.txt* in the *output* container.</span></span>

<span data-ttu-id="56e49-120">Jeśli musisz określić wzorzec nazw dla nazwy obiektów blob, które mają nawiasy klamrowe w nazwie dwukrotnie nawiasów klamrowych.</span><span class="sxs-lookup"><span data-stu-id="56e49-120">If you need to specify a name pattern for blob names that have curly braces in the name, double the curly braces.</span></span> <span data-ttu-id="56e49-121">Na przykład, jeśli chcesz znaleźć obiekty BLOB w *obrazów* kontenera, w którym mają nazwy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="56e49-121">For example, if you want to find blobs in the *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="56e49-122">Użyj tego deseniu:</span><span class="sxs-lookup"><span data-stu-id="56e49-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="56e49-123">W tym przykładzie *nazwa* wartość symbolu zastępczego będzie *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="56e49-123">In the example, the *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="56e49-124">Symbole zastępcze nazwę i rozszerzenie oddzielnych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="56e49-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="56e49-125">Poniższy przykładowy kod powoduje zmianę rozszerzenia pliku jako kopiowania obiektów blob, które są widoczne w *wejściowych* kontener, aby *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="56e49-125">The following code sample changes the file extension as it copies blobs that appear in the *input* container to the *output* container.</span></span> <span data-ttu-id="56e49-126">Kod rejestruje rozszerzenie *wejściowych* obiektu blob i Ustawia rozszerzenie *dane wyjściowe* obiektu blob do *.txt*.</span><span class="sxs-lookup"><span data-stu-id="56e49-126">The code logs the extension of the *input* blob and sets the extension of the *output* blob to *.txt*.</span></span>

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

## <a name="types-that-you-can-bind-to-blobs"></a><span data-ttu-id="56e49-127">Typy, które można powiązać obiekty BLOB</span><span class="sxs-lookup"><span data-stu-id="56e49-127">Types that you can bind to blobs</span></span>
<span data-ttu-id="56e49-128">Można użyć **BlobTrigger** atrybutu w następujących typów:</span><span class="sxs-lookup"><span data-stu-id="56e49-128">You can use the **BlobTrigger** attribute on the following types:</span></span>

* <span data-ttu-id="56e49-129">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="56e49-129">**string**</span></span>
* <span data-ttu-id="56e49-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="56e49-130">**TextReader**</span></span>
* <span data-ttu-id="56e49-131">**Strumień**</span><span class="sxs-lookup"><span data-stu-id="56e49-131">**Stream**</span></span>
* <span data-ttu-id="56e49-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="56e49-132">**ICloudBlob**</span></span>
* <span data-ttu-id="56e49-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="56e49-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="56e49-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="56e49-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="56e49-135">Inne typy deserializacji przez [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="56e49-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="56e49-136">Jeśli chcesz pracować bezpośrednio z kontem magazynu platformy Azure, możesz także dodać **CloudStorageAccount** parametru w podpisie metody.</span><span class="sxs-lookup"><span data-stu-id="56e49-136">If you want to work directly with the Azure storage account, you can also add a **CloudStorageAccount** parameter to the method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-to-string"></a><span data-ttu-id="56e49-137">Pobieranie zawartości obiektu blob tekstu przez powiązanie do ciągu</span><span class="sxs-lookup"><span data-stu-id="56e49-137">Getting text blob content by binding to string</span></span>
<span data-ttu-id="56e49-138">Jeśli oczekiwano tekstu w obiektach blob, **BlobTrigger** można zastosować do **ciąg** parametru.</span><span class="sxs-lookup"><span data-stu-id="56e49-138">If text blobs are expected, **BlobTrigger** can be applied to a **string** parameter.</span></span> <span data-ttu-id="56e49-139">Poniższy przykładowy kod wiąże obiektu blob tekstu do **ciąg** parametru o nazwie **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="56e49-139">The following code sample binds a text blob to a **string** parameter named **logMessage**.</span></span> <span data-ttu-id="56e49-140">Funkcja używa parametru do zapisania zawartości obiektu blob do pulpitu nawigacyjnego, zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="56e49-140">The function uses that parameter to write the contents of the blob to the WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="56e49-141">Pobieranie serializacji zawartość obiektu blob przy użyciu ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="56e49-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="56e49-142">Poniższy przykład kodu wykorzystuje klasy, która implementuje **ICloudBlobStreamBinder** umożliwiające **BlobTrigger** atrybutu będzie tworzone powiązanie obiektu blob do **WebImage** typu.</span><span class="sxs-lookup"><span data-stu-id="56e49-142">The following code sample uses a class that implements **ICloudBlobStreamBinder** to enable the **BlobTrigger** attribute to bind a blob to the **WebImage** type.</span></span>

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

<span data-ttu-id="56e49-143">**WebImage** powiązanie kod znajduje się w **WebImageBinder** klasą pochodzącą z **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="56e49-143">The **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-to-handle-poison-blobs"></a><span data-ttu-id="56e49-144">Sposób obsługi skażone obiektów blob</span><span class="sxs-lookup"><span data-stu-id="56e49-144">How to handle poison blobs</span></span>
<span data-ttu-id="56e49-145">Gdy **BlobTrigger** funkcja kończy się niepowodzeniem, zestaw SDK wymaga go ponownie, w przypadku, gdy błąd został spowodowany przez błąd przejściowy.</span><span class="sxs-lookup"><span data-stu-id="56e49-145">When a **BlobTrigger** function fails, the SDK calls it again, in case the failure was caused by a transient error.</span></span> <span data-ttu-id="56e49-146">Jeśli niepowodzenie jest spowodowane zawartość obiektu blob, funkcja zakończy się niepowodzeniem, za każdym razem, gdy próbuje przetworzyć obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="56e49-146">If the failure is caused by the content of the blob, the function fails every time it tries to process the blob.</span></span> <span data-ttu-id="56e49-147">Domyślnie zestaw SDK wywołuje funkcję maksymalnie 5 razy dla danego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="56e49-147">By default, the SDK calls a function up to 5 times for a given blob.</span></span> <span data-ttu-id="56e49-148">Jeśli piątym spróbuj kończy się niepowodzeniem, zestaw SDK dodaje komunikat do kolejki o nazwie *webjob blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="56e49-148">If the fifth try fails, the SDK adds a message to a queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="56e49-149">Konfiguruje się maksymalnej liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="56e49-149">The maximum number of retries is configurable.</span></span> <span data-ttu-id="56e49-150">Taki sam [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ustawienie służy do obsługi skażone obiektów blob i kolejki skażone komunikat — Obsługa.</span><span class="sxs-lookup"><span data-stu-id="56e49-150">The same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="56e49-151">Komunikat z kolejki skażone obiektów blob jest obiekt JSON, który zawiera następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="56e49-151">The queue message for poison blobs is a JSON object that contains the following properties:</span></span>

* <span data-ttu-id="56e49-152">FunctionId (w formacie *{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*, na przykład: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="56e49-152">FunctionId (in the format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="56e49-153">BlobType ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="56e49-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="56e49-154">Właściwość ContainerName</span><span class="sxs-lookup"><span data-stu-id="56e49-154">ContainerName</span></span>
* <span data-ttu-id="56e49-155">Element BlobName</span><span class="sxs-lookup"><span data-stu-id="56e49-155">BlobName</span></span>
* <span data-ttu-id="56e49-156">Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="56e49-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="56e49-157">W poniższym przykładzie kodu **CopyBlob** funkcja ma kod powodujący niepowodzenie za każdym razem, gdy jest ona wywoływana.</span><span class="sxs-lookup"><span data-stu-id="56e49-157">In the following code sample, the **CopyBlob** function has code that causes it to fail every time it's called.</span></span> <span data-ttu-id="56e49-158">Po zestaw SDK wymaga on maksymalnej liczby ponownych prób, wiadomość jest tworzony w kolejce skażone obiektów blob, a ten komunikat jest przetwarzany przez **LogPoisonBlob** funkcji.</span><span class="sxs-lookup"><span data-stu-id="56e49-158">After the SDK calls it for the maximum number of retries, a message is created on the poison blob queue, and that message is processed by the **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="56e49-159">Zestaw SDK automatycznie deserializuje komunikat JSON.</span><span class="sxs-lookup"><span data-stu-id="56e49-159">The SDK automatically deserializes the JSON message.</span></span> <span data-ttu-id="56e49-160">Oto **PoisonBlobMessage** klasy:</span><span class="sxs-lookup"><span data-stu-id="56e49-160">Here is the **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="56e49-161">Algorytm sondowania obiektów blob</span><span class="sxs-lookup"><span data-stu-id="56e49-161">Blob polling algorithm</span></span>
<span data-ttu-id="56e49-162">Zestaw SDK zadań Webjob skanuje wszystkie kontenery określony przez **BlobTrigger** atrybuty podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="56e49-162">The WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="56e49-163">Na koncie magazynu dużych ten tryb skanowania może zająć trochę czasu, dlatego może być trochę czasu, zanim znajdują się nowe obiekty BLOB i **BlobTrigger** funkcje są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="56e49-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="56e49-164">Aby wykryć nowe lub zmienione obiekty BLOB po uruchomieniu aplikacji, zestaw SDK okresowo odczytuje z dzienników magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="56e49-164">To detect new or changed blobs after application start, the SDK periodically reads from the blob storage logs.</span></span> <span data-ttu-id="56e49-165">Dzienniki obiektów blob są buforowane oraz tylko fizycznie zapisane co 10 minut lub tak, więc mogą występować znaczne opóźnienie po obiektu blob jest tworzony lub aktualizowany przed odpowiadającego **BlobTrigger** wykonuje funkcji.</span><span class="sxs-lookup"><span data-stu-id="56e49-165">The blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before the corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="56e49-166">Występuje wyjątek dla obiektów blob, które utworzono za pomocą **obiektu Blob** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="56e49-166">There is an exception for blobs that you create by using the **Blob** attribute.</span></span> <span data-ttu-id="56e49-167">Gdy zestaw SDK zadań Webjob tworzy nowy obiekt blob, przekazaniem nowego obiektu blob natychmiast żadnych zgodnych **BlobTrigger** funkcji.</span><span class="sxs-lookup"><span data-stu-id="56e49-167">When the WebJobs SDK creates a new blob, it passes the new blob immediately to any matching **BlobTrigger** functions.</span></span> <span data-ttu-id="56e49-168">W związku z tym jeśli łańcuch blob wejściach i wyjściach, zestaw SDK może je przetwarzać wydajnie.</span><span class="sxs-lookup"><span data-stu-id="56e49-168">Therefore if you have a chain of blob inputs and outputs, the SDK can process them efficiently.</span></span> <span data-ttu-id="56e49-169">Ale jeśli chcesz małych opóźnieniach uruchomiona z obiektu blob funkcji przetwarzania dla obiektów blob, które są tworzone lub zaktualizowany w inny sposób, firma Microsoft zaleca używanie **QueueTrigger** zamiast **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="56e49-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="56e49-170">Potwierdzenia obiektów blob</span><span class="sxs-lookup"><span data-stu-id="56e49-170">Blob receipts</span></span>
<span data-ttu-id="56e49-171">Zestaw SDK zadań Webjob, sprawdza nie **BlobTrigger** funkcja jest wywoływana więcej niż raz dla tego samego obiektu blob nowe lub zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="56e49-171">The WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for the same new or updated blob.</span></span> <span data-ttu-id="56e49-172">Dzieje się tak dzięki utrzymywaniu *obiektu blob potwierdzenia* w celu ustalenia, czy wersja danego obiektu blob został przetworzony.</span><span class="sxs-lookup"><span data-stu-id="56e49-172">It does this by maintaining *blob receipts* in order to determine if a given blob version has been processed.</span></span>

<span data-ttu-id="56e49-173">Potwierdzenia obiektów blob są przechowywane w kontenerze o nazwie *azure webjobs hostów* w określona przez ciąg połączenia AzureWebJobsStorage konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="56e49-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in the Azure storage account specified by the AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="56e49-174">Potwierdzenie obiektu blob zawiera następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="56e49-174">A blob receipt has the following  information:</span></span>

* <span data-ttu-id="56e49-175">Funkcja, która została wywołana dla obiektu blob ("*{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*", na przykład:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="56e49-175">The function that was called for the blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="56e49-176">Nazwa kontenera</span><span class="sxs-lookup"><span data-stu-id="56e49-176">The container name</span></span>
* <span data-ttu-id="56e49-177">Typ obiektów blob ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="56e49-177">The blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="56e49-178">Nazwa obiektu blob</span><span class="sxs-lookup"><span data-stu-id="56e49-178">The blob name</span></span>
* <span data-ttu-id="56e49-179">Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="56e49-179">The ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="56e49-180">Jeśli chcesz wymusić ponowne przetworzenie obiektu blob, należy ręcznie usunąć potwierdzenia obiektu blob dla tego obiektu blob z *azure webjobs hostów* kontenera.</span><span class="sxs-lookup"><span data-stu-id="56e49-180">If you want to force reprocessing of a blob, you can manually delete the blob receipt for that blob from the *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-the-queues-article"></a><span data-ttu-id="56e49-181">Tematy pokrewne objętych artykułem kolejek</span><span class="sxs-lookup"><span data-stu-id="56e49-181">Related topics covered by the queues article</span></span>
<span data-ttu-id="56e49-182">Informacje dotyczące obsługi przetwarzania obiektu blob wyzwalane przez komunikatu w kolejce, lub zestaw SDK zadań Webjob do obiektu blob nie są typowe scenariusze przetwarzania, zobacz [jak używać magazynu kolejek Azure przy użyciu zestawu SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="56e49-182">For information about how to handle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific to blob processing, see [How to use Azure queue storage with the WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="56e49-183">Tematy pokrewne omówione w tym artykule są następujące:</span><span class="sxs-lookup"><span data-stu-id="56e49-183">Related topics covered in that article include the following:</span></span>

* <span data-ttu-id="56e49-184">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="56e49-184">Async functions</span></span>
* <span data-ttu-id="56e49-185">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="56e49-185">Multiple instances</span></span>
* <span data-ttu-id="56e49-186">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="56e49-186">Graceful shutdown</span></span>
* <span data-ttu-id="56e49-187">Użyj zestawu SDK zadań Webjob atrybutów w treści funkcji</span><span class="sxs-lookup"><span data-stu-id="56e49-187">Use WebJobs SDK attributes in the body of a function</span></span>
* <span data-ttu-id="56e49-188">Ustaw parametry połączenia SDK w kodzie.</span><span class="sxs-lookup"><span data-stu-id="56e49-188">Set the SDK connection strings in code.</span></span>
* <span data-ttu-id="56e49-189">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="56e49-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="56e49-190">Skonfiguruj **MaxDequeueCount** obsługi skażone obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="56e49-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="56e49-191">Wyzwalanie funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="56e49-191">Trigger a function manually</span></span>
* <span data-ttu-id="56e49-192">Zapisywanie dzienników</span><span class="sxs-lookup"><span data-stu-id="56e49-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="56e49-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="56e49-193">Next steps</span></span>
<span data-ttu-id="56e49-194">W tym artykule udostępnił przykłady kodu, które przedstawiają sposób obsługi typowe scenariusze dotyczące pracy z obiektami blob Azure.</span><span class="sxs-lookup"><span data-stu-id="56e49-194">This article has provided code samples that show how to handle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="56e49-195">Aby uzyskać więcej informacji o sposobie używania zadań Webjob Azure i zestaw SDK zadań Webjob, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="56e49-195">For more information about how to use Azure WebJobs and the WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

