---
title: "aaaGet wprowadzenie do magazynu obiektów blob i Visual Studio podłączonych usług (projekty zadania WebJob) | Dokumentacja firmy Microsoft"
description: "Sposób uruchamiania przy użyciu magazynu obiektów Blob w projektu zadania WebJob po połączeniu tooan magazynu platformy Azure przy użyciu programu Visual Studio tooget połączone usługi."
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 324c9376-0225-4092-9825-5d1bd5550058
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: cb2cecacbb1a59f093d5453a91fae33e0f279d85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-webjob-projects"></a><span data-ttu-id="bdc15-103">Wprowadzenie do obiektów Blob platformy Azure magazynu i Visual Studio połączone usługi (zadania WebJob projekty)</span><span class="sxs-lookup"><span data-stu-id="bdc15-103">Get started with Azure Blob storage and Visual Studio connected services (WebJob projects)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="bdc15-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="bdc15-104">Overview</span></span>
<span data-ttu-id="bdc15-105">Ten artykuł zawiera C# jak przykłady kodu przedstawiające tootrigger procesu podczas tworzenia lub aktualizowania obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc15-105">This article provides C# code samples that show how tootrigger a process when an Azure blob is created or updated.</span></span> <span data-ttu-id="bdc15-106">Przykłady kodu Hello Użyj hello [zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk.md) wersja 1.x.</span><span class="sxs-lookup"><span data-stu-id="bdc15-106">hello code samples use hello [WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md) version 1.x.</span></span> <span data-ttu-id="bdc15-107">Po dodaniu projektu zadania WebJob tooa konto magazynu przy użyciu programu Visual Studio hello **dodać usług połączonych** okna dialogowego, hello odpowiedniego pakietu NuGet usługi Magazyn Azure jest zainstalowany, hello odpowiednie .NET odwołania są dodane toohello Projekt i parametry połączenia dla konta magazynu hello są aktualizowane w pliku App.config hello.</span><span class="sxs-lookup"><span data-stu-id="bdc15-107">When you add a storage account tooa WebJob project by using hello Visual Studio **Add Connected Services** dialog, hello appropriate Azure Storage NuGet package is installed, hello appropriate .NET references are added toohello project, and connection strings for hello storage account are updated in hello App.config file.</span></span>

## <a name="how-tootrigger-a-function-when-a-blob-is-created-or-updated"></a><span data-ttu-id="bdc15-108">Jak tootrigger funkcja, gdy obiekt blob jest tworzony lub aktualizowany</span><span class="sxs-lookup"><span data-stu-id="bdc15-108">How tootrigger a function when a blob is created or updated</span></span>
<span data-ttu-id="bdc15-109">W tej sekcji przedstawiono sposób toouse hello **BlobTrigger** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="bdc15-109">This section shows how toouse hello **BlobTrigger** attribute.</span></span>

 <span data-ttu-id="bdc15-110">**Uwaga:** hello zestaw SDK zadań Webjob skanowania dziennika pliki toowatch dla nowych lub zmienionych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="bdc15-110">**Note:** hello WebJobs SDK scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="bdc15-111">Ten proces jest z założenia powolne; funkcja może nie pobrać są uruchamiane kilka minut lub dłużej po utworzeniu obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="bdc15-111">This process is inherently slow; a function might not get triggered until several minutes or longer after hello blob is created.</span></span>  <span data-ttu-id="bdc15-112">Jeśli aplikacja wymaga obiekty BLOB tooprocess natychmiast, hello zalecana metoda to toocreate komunikatu w kolejce, podczas tworzenia obiektu blob hello i użyj hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) zamiast hello atrybutu **BlobTrigger** atrybutu w funkcji hello, który przetwarza hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bdc15-112">If your application needs tooprocess blobs immediately, hello recommended method is toocreate a queue message when you create hello blob, and use hello [QueueTrigger](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#trigger) attribute instead of hello **BlobTrigger** attribute on hello function that processes hello blob.</span></span>

### <a name="single-placeholder-for-blob-name-with-extension"></a><span data-ttu-id="bdc15-113">Jeden symbol zastępczy dla obiektu blob nazwy z rozszerzeniem</span><span class="sxs-lookup"><span data-stu-id="bdc15-113">Single placeholder for blob name with extension</span></span>
<span data-ttu-id="bdc15-114">Witaj Poniższy przykładowy kod kopiuje tekst obiektów blob, które pojawiają się w hello *wejściowych* toohello kontenera *dane wyjściowe* kontenera:</span><span class="sxs-lookup"><span data-stu-id="bdc15-114">hello following code sample copies text blobs that appear in hello *input* container toohello *output* container:</span></span>

        public static void CopyBlob([BlobTrigger("input/{name}")] TextReader input,
            [Blob("output/{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="bdc15-115">Hello Konstruktor atrybutu ma parametr ciąg, który określa nazwę kontenera hello i hello nazwę obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bdc15-115">hello attribute constructor takes a string parameter that specifies hello container name and a placeholder for hello blob name.</span></span> <span data-ttu-id="bdc15-116">W tym przykładzie o nazwie obiektu blob *Blob1.txt* jest tworzony w hello *wejściowych* kontenera, funkcja hello tworzy obiektu blob o nazwie *Blob1.txt* w hello *danych wyjściowych*  kontenera.</span><span class="sxs-lookup"><span data-stu-id="bdc15-116">In this example, if a blob named *Blob1.txt* is created in hello *input* container, hello function creates a blob named *Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="bdc15-117">Wzorzec nazwy można określić za pomocą hello blob nazwa symbolu zastępczego, jak pokazano w powitania po przykładowy kod:</span><span class="sxs-lookup"><span data-stu-id="bdc15-117">You can specify a name pattern with hello blob name placeholder, as shown in hello following code sample:</span></span>

        public static void CopyBlob([BlobTrigger("input/original-{name}")] TextReader input,
            [Blob("output/copy-{name}")] out string output)
        {
            output = input.ReadToEnd();
        }

<span data-ttu-id="bdc15-118">Ten kod kopiuje tylko obiekty BLOB o nazwach rozpoczynających się od "oryginalnego-".</span><span class="sxs-lookup"><span data-stu-id="bdc15-118">This code copies only blobs that have names beginning with "original-".</span></span> <span data-ttu-id="bdc15-119">Na przykład *Blob1.txt oryginalne* w hello *wejściowych* kontenera jest kopiowana za*Blob1.txt kopiowania* w hello *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="bdc15-119">For example, *original-Blob1.txt* in hello *input* container is copied too*copy-Blob1.txt* in hello *output* container.</span></span>

<span data-ttu-id="bdc15-120">Jeśli potrzebujesz toospecify wzorzec nazw dla nazwy obiektów blob, które mają nawiasy klamrowe w nazwie hello dwukrotnie hello nawiasów klamrowych.</span><span class="sxs-lookup"><span data-stu-id="bdc15-120">If you need toospecify a name pattern for blob names that have curly braces in hello name, double hello curly braces.</span></span> <span data-ttu-id="bdc15-121">Na przykład, jeśli chcesz, aby obiekty BLOB toofind na powitania *obrazów* kontenera, w którym mają nazwy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bdc15-121">For example, if you want toofind blobs in hello *images* container that have names like this:</span></span>

        {20140101}-soundfile.mp3

<span data-ttu-id="bdc15-122">Użyj tego deseniu:</span><span class="sxs-lookup"><span data-stu-id="bdc15-122">use this for your pattern:</span></span>

        images/{{20140101}}-{name}

<span data-ttu-id="bdc15-123">Przykład Witaj Witaj *nazwa* wartość symbolu zastępczego będzie *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="bdc15-123">In hello example, hello *name* placeholder value would be *soundfile.mp3*.</span></span>

### <a name="separate-blob-name-and-extension-placeholders"></a><span data-ttu-id="bdc15-124">Symbole zastępcze nazwę i rozszerzenie oddzielnych obiektów blob</span><span class="sxs-lookup"><span data-stu-id="bdc15-124">Separate blob name and extension placeholders</span></span>
<span data-ttu-id="bdc15-125">Witaj następujące zmiany przykładowy kod hello rozszerzenie pliku jako kopiuje obiektów blob, które są wyświetlane w hello *wejściowych* toohello kontenera *dane wyjściowe* kontenera.</span><span class="sxs-lookup"><span data-stu-id="bdc15-125">hello following code sample changes hello file extension as it copies blobs that appear in hello *input* container toohello *output* container.</span></span> <span data-ttu-id="bdc15-126">Kod Hello rejestruje rozszerzenie hello hello *wejściowych* obiektu blob i Ustawia rozszerzenie hello hello *dane wyjściowe* obiektów blob za*.txt*.</span><span class="sxs-lookup"><span data-stu-id="bdc15-126">hello code logs hello extension of hello *input* blob and sets hello extension of hello *output* blob too*.txt*.</span></span>

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

## <a name="types-that-you-can-bind-tooblobs"></a><span data-ttu-id="bdc15-127">Czy można powiązać tooblobs typów</span><span class="sxs-lookup"><span data-stu-id="bdc15-127">Types that you can bind tooblobs</span></span>
<span data-ttu-id="bdc15-128">Można użyć hello **BlobTrigger** atrybutu na powitania następujące typy:</span><span class="sxs-lookup"><span data-stu-id="bdc15-128">You can use hello **BlobTrigger** attribute on hello following types:</span></span>

* <span data-ttu-id="bdc15-129">**ciąg**</span><span class="sxs-lookup"><span data-stu-id="bdc15-129">**string**</span></span>
* <span data-ttu-id="bdc15-130">**TextReader**</span><span class="sxs-lookup"><span data-stu-id="bdc15-130">**TextReader**</span></span>
* <span data-ttu-id="bdc15-131">**Strumień**</span><span class="sxs-lookup"><span data-stu-id="bdc15-131">**Stream**</span></span>
* <span data-ttu-id="bdc15-132">**ICloudBlob**</span><span class="sxs-lookup"><span data-stu-id="bdc15-132">**ICloudBlob**</span></span>
* <span data-ttu-id="bdc15-133">**CloudBlockBlob**</span><span class="sxs-lookup"><span data-stu-id="bdc15-133">**CloudBlockBlob**</span></span>
* <span data-ttu-id="bdc15-134">**CloudPageBlob**</span><span class="sxs-lookup"><span data-stu-id="bdc15-134">**CloudPageBlob**</span></span>
* <span data-ttu-id="bdc15-135">Inne typy deserializacji przez [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span><span class="sxs-lookup"><span data-stu-id="bdc15-135">Other types deserialized by [ICloudBlobStreamBinder](#getting-serialized-blob-content-by-using-icloudblobstreambinder)</span></span>

<span data-ttu-id="bdc15-136">Jeśli chcesz toowork bezpośrednio z hello kontem magazynu platformy Azure, możesz także dodać **CloudStorageAccount** podpis metody toohello parametru.</span><span class="sxs-lookup"><span data-stu-id="bdc15-136">If you want toowork directly with hello Azure storage account, you can also add a **CloudStorageAccount** parameter toohello method signature.</span></span>

## <a name="getting-text-blob-content-by-binding-toostring"></a><span data-ttu-id="bdc15-137">Pobieranie zawartości obiektu blob tekstu przez powiązanie toostring</span><span class="sxs-lookup"><span data-stu-id="bdc15-137">Getting text blob content by binding toostring</span></span>
<span data-ttu-id="bdc15-138">Jeśli oczekiwano tekstu w obiektach blob, **BlobTrigger** może być zastosowane tooa **ciąg** parametru.</span><span class="sxs-lookup"><span data-stu-id="bdc15-138">If text blobs are expected, **BlobTrigger** can be applied tooa **string** parameter.</span></span> <span data-ttu-id="bdc15-139">Witaj Poniższy przykładowy kod wiąże tooa obiektu blob tekst **ciąg** parametru o nazwie **logMessage**.</span><span class="sxs-lookup"><span data-stu-id="bdc15-139">hello following code sample binds a text blob tooa **string** parameter named **logMessage**.</span></span> <span data-ttu-id="bdc15-140">Funkcja Hello korzysta zawartości hello toowrite parametru tego toohello obiektu blob hello zestaw SDK zadań Webjob pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="bdc15-140">hello function uses that parameter toowrite hello contents of hello blob toohello WebJobs SDK dashboard.</span></span>

        public static void WriteLog([BlobTrigger("input/{name}")] string logMessage,
            string name,
            TextWriter logger)
        {
             logger.WriteLine("Blob name: {0}", name);
             logger.WriteLine("Content:");
             logger.WriteLine(logMessage);
        }

## <a name="getting-serialized-blob-content-by-using-icloudblobstreambinder"></a><span data-ttu-id="bdc15-141">Pobieranie serializacji zawartość obiektu blob przy użyciu ICloudBlobStreamBinder</span><span class="sxs-lookup"><span data-stu-id="bdc15-141">Getting serialized blob content by using ICloudBlobStreamBinder</span></span>
<span data-ttu-id="bdc15-142">Witaj Poniższy przykładowy kod używa klasy, która implementuje **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** toobind toohello obiektu blob atrybutu **WebImage** typu.</span><span class="sxs-lookup"><span data-stu-id="bdc15-142">hello following code sample uses a class that implements **ICloudBlobStreamBinder** tooenable hello **BlobTrigger** attribute toobind a blob toohello **WebImage** type.</span></span>

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

<span data-ttu-id="bdc15-143">Witaj **WebImage** powiązanie kod znajduje się w **WebImageBinder** klasą pochodzącą z **ICloudBlobStreamBinder**.</span><span class="sxs-lookup"><span data-stu-id="bdc15-143">hello **WebImage** binding code is provided in a **WebImageBinder** class that derives from **ICloudBlobStreamBinder**.</span></span>

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

## <a name="how-toohandle-poison-blobs"></a><span data-ttu-id="bdc15-144">Jak obiekty BLOB toohandle poison</span><span class="sxs-lookup"><span data-stu-id="bdc15-144">How toohandle poison blobs</span></span>
<span data-ttu-id="bdc15-145">Gdy **BlobTrigger** funkcja kończy się niepowodzeniem, hello zestawu SDK wywołania go ponownie, w przypadku hello błąd został spowodowany przez błąd przejściowy.</span><span class="sxs-lookup"><span data-stu-id="bdc15-145">When a **BlobTrigger** function fails, hello SDK calls it again, in case hello failure was caused by a transient error.</span></span> <span data-ttu-id="bdc15-146">Jeśli hello jest przyczyną niepowodzenia hello zawartości obiektu hello blob, funkcja hello zakończy się niepowodzeniem, zawsze próbuje tooprocess hello blob.</span><span class="sxs-lookup"><span data-stu-id="bdc15-146">If hello failure is caused by hello content of hello blob, hello function fails every time it tries tooprocess hello blob.</span></span> <span data-ttu-id="bdc15-147">Domyślnie program hello SDK wywołuje funkcję się too5 razy dla danego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bdc15-147">By default, hello SDK calls a function up too5 times for a given blob.</span></span> <span data-ttu-id="bdc15-148">W przypadku niepowodzenia spróbuj piątym powitania hello SDK dodaje tooa kolejki komunikatów o nazwie *webjob blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="bdc15-148">If hello fifth try fails, hello SDK adds a message tooa queue named *webjobs-blobtrigger-poison*.</span></span>

<span data-ttu-id="bdc15-149">konfiguruje się Hello maksymalnej liczby ponownych prób.</span><span class="sxs-lookup"><span data-stu-id="bdc15-149">hello maximum number of retries is configurable.</span></span> <span data-ttu-id="bdc15-150">Witaj sam [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) ustawienie służy do obsługi skażone obiektów blob i kolejki skażone komunikat — Obsługa.</span><span class="sxs-lookup"><span data-stu-id="bdc15-150">hello same [MaxDequeueCount](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md#configqueue) setting is used for poison blob handling and poison queue message handling.</span></span>

<span data-ttu-id="bdc15-151">komunikat z kolejki Hello skażone obiektów blob jest obiekt JSON, który zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="bdc15-151">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="bdc15-152">FunctionId (w formacie hello *{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*, na przykład: WebJob1.Functions.CopyBlob)</span><span class="sxs-lookup"><span data-stu-id="bdc15-152">FunctionId (in hello format *{WebJob name}*.Functions.*{Function name}*, for example: WebJob1.Functions.CopyBlob)</span></span>
* <span data-ttu-id="bdc15-153">BlobType ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="bdc15-153">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="bdc15-154">Właściwość ContainerName</span><span class="sxs-lookup"><span data-stu-id="bdc15-154">ContainerName</span></span>
* <span data-ttu-id="bdc15-155">Element BlobName</span><span class="sxs-lookup"><span data-stu-id="bdc15-155">BlobName</span></span>
* <span data-ttu-id="bdc15-156">Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="bdc15-156">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="bdc15-157">W następujących hello kodu próbki hello **CopyBlob** funkcja ma kod powodujący toofail za każdym razem, gdy jest ona wywoływana.</span><span class="sxs-lookup"><span data-stu-id="bdc15-157">In hello following code sample, hello **CopyBlob** function has code that causes it toofail every time it's called.</span></span> <span data-ttu-id="bdc15-158">Po hello zestaw SDK wymaga on hello maksymalnej liczby ponownych prób, wiadomość jest tworzona na powitania skażone blob kolejki, a ten komunikat jest przetwarzany przez hello **LogPoisonBlob** funkcji.</span><span class="sxs-lookup"><span data-stu-id="bdc15-158">After hello SDK calls it for hello maximum number of retries, a message is created on hello poison blob queue, and that message is processed by hello **LogPoisonBlob** function.</span></span>

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

<span data-ttu-id="bdc15-159">Witaj SDK automatycznie deserializuje wiadomości powitania JSON.</span><span class="sxs-lookup"><span data-stu-id="bdc15-159">hello SDK automatically deserializes hello JSON message.</span></span> <span data-ttu-id="bdc15-160">Oto hello **PoisonBlobMessage** klasy:</span><span class="sxs-lookup"><span data-stu-id="bdc15-160">Here is hello **PoisonBlobMessage** class:</span></span>

        public class PoisonBlobMessage
        {
            public string FunctionId { get; set; }
            public string BlobType { get; set; }
            public string ContainerName { get; set; }
            public string BlobName { get; set; }
            public string ETag { get; set; }
        }

### <a name="blob-polling-algorithm"></a><span data-ttu-id="bdc15-161">Algorytm sondowania obiektów blob</span><span class="sxs-lookup"><span data-stu-id="bdc15-161">Blob polling algorithm</span></span>
<span data-ttu-id="bdc15-162">Witaj zestaw SDK zadań Webjob skanuje wszystkie kontenery określony przez **BlobTrigger** atrybuty podczas uruchamiania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bdc15-162">hello WebJobs SDK scans all containers specified by **BlobTrigger** attributes at application start.</span></span> <span data-ttu-id="bdc15-163">Na koncie magazynu dużych ten tryb skanowania może zająć trochę czasu, dlatego może być trochę czasu, zanim znajdują się nowe obiekty BLOB i **BlobTrigger** funkcje są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="bdc15-163">In a large storage account this scan can take some time, so it might be a while before new blobs are found and **BlobTrigger** functions are executed.</span></span>

<span data-ttu-id="bdc15-164">rejestruje powitalne SDK okresowo odczytuje z magazynu obiektów blob hello toodetect nowych lub zmienionych obiektów blob w po uruchomieniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bdc15-164">toodetect new or changed blobs after application start, hello SDK periodically reads from hello blob storage logs.</span></span> <span data-ttu-id="bdc15-165">Witaj dzienniki obiektów blob są buforowane i tylko fizycznie zapisane co 10 minut lub tak, więc mogą występować znaczne opóźnienia po obiektu blob jest tworzony lub aktualizowany przed hello odpowiadającego **BlobTrigger** wykonuje funkcji.</span><span class="sxs-lookup"><span data-stu-id="bdc15-165">hello blob logs are buffered and only get physically written every 10 minutes or so, so there may be significant delay after a blob is created or updated before hello corresponding **BlobTrigger** function executes.</span></span>

<span data-ttu-id="bdc15-166">Brak wyjątek dla obiektów blob, które są tworzone przy użyciu hello **obiektu Blob** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="bdc15-166">There is an exception for blobs that you create by using hello **Blob** attribute.</span></span> <span data-ttu-id="bdc15-167">Gdy hello zestaw SDK zadań Webjob tworzy nowy obiekt blob, natychmiast przekazaniem nowego obiektu blob hello dopasowania tooany **BlobTrigger** funkcji.</span><span class="sxs-lookup"><span data-stu-id="bdc15-167">When hello WebJobs SDK creates a new blob, it passes hello new blob immediately tooany matching **BlobTrigger** functions.</span></span> <span data-ttu-id="bdc15-168">W związku z tym jeśli łańcuch blob wejściach i wyjściach, hello SDK może je przetwarzać wydajnie.</span><span class="sxs-lookup"><span data-stu-id="bdc15-168">Therefore if you have a chain of blob inputs and outputs, hello SDK can process them efficiently.</span></span> <span data-ttu-id="bdc15-169">Ale jeśli chcesz małych opóźnieniach uruchomiona z obiektu blob funkcji przetwarzania dla obiektów blob, które są tworzone lub zaktualizowany w inny sposób, firma Microsoft zaleca używanie **QueueTrigger** zamiast **BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="bdc15-169">But if you want low latency running your blob processing functions for blobs that are created or updated by other means, we recommend using **QueueTrigger** rather than **BlobTrigger**.</span></span>

### <a name="blob-receipts"></a><span data-ttu-id="bdc15-170">Potwierdzenia obiektów blob</span><span class="sxs-lookup"><span data-stu-id="bdc15-170">Blob receipts</span></span>
<span data-ttu-id="bdc15-171">zestaw SDK zadań Webjob Hello, sprawdza nie **BlobTrigger** funkcja jest wywoływana więcej niż raz dla hello sam nowe lub zaktualizowane obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bdc15-171">hello WebJobs SDK makes sure that no **BlobTrigger** function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="bdc15-172">Dzieje się tak dzięki utrzymywaniu *obiektu blob potwierdzenia* w kolejności toodetermine wersji danego obiektu blob został przetworzony.</span><span class="sxs-lookup"><span data-stu-id="bdc15-172">It does this by maintaining *blob receipts* in order toodetermine if a given blob version has been processed.</span></span>

<span data-ttu-id="bdc15-173">Potwierdzenia obiektów blob są przechowywane w kontenerze o nazwie *azure webjobs hostów* na koncie magazynu Azure hello określona przez ciąg połączenia AzureWebJobsStorage hello.</span><span class="sxs-lookup"><span data-stu-id="bdc15-173">Blob receipts are stored in a container named *azure-webjobs-hosts* in hello Azure storage account specified by hello AzureWebJobsStorage connection string.</span></span> <span data-ttu-id="bdc15-174">Potwierdzenie obiektu blob ma hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="bdc15-174">A blob receipt has hello following  information:</span></span>

* <span data-ttu-id="bdc15-175">Funkcja, która została wywołana dla obiektu blob hello Hello ("*{Nazwa zadania WebJob}*. Funkcje. *{Nazwa funkcji}*", na przykład:"WebJob1.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="bdc15-175">hello function that was called for hello blob ("*{WebJob name}*.Functions.*{Function name}*", for example: "WebJob1.Functions.CopyBlob")</span></span>
* <span data-ttu-id="bdc15-176">Nazwa kontenera Hello</span><span class="sxs-lookup"><span data-stu-id="bdc15-176">hello container name</span></span>
* <span data-ttu-id="bdc15-177">Typ obiektu blob Hello ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="bdc15-177">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="bdc15-178">Nazwa obiektu blob Hello</span><span class="sxs-lookup"><span data-stu-id="bdc15-178">hello blob name</span></span>
* <span data-ttu-id="bdc15-179">Witaj ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="bdc15-179">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="bdc15-180">Jeśli chcesz tooforce ponowne przetworzenie obiektu blob, można ręcznie usunąć hello potwierdzenia obiektu blob dla tego obiektu blob z hello *azure webjobs hostów* kontenera.</span><span class="sxs-lookup"><span data-stu-id="bdc15-180">If you want tooforce reprocessing of a blob, you can manually delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container.</span></span>

## <a name="related-topics-covered-by-hello-queues-article"></a><span data-ttu-id="bdc15-181">Tematy pokrewne objętych hello kolejek artykułu</span><span class="sxs-lookup"><span data-stu-id="bdc15-181">Related topics covered by hello queues article</span></span>
<span data-ttu-id="bdc15-182">Informacje dotyczące sposobu przetwarzania obiektu blob toohandle wyzwalane komunikatu w kolejce, lub dla zadań Webjob scenariusze zestawu SDK nie określonych tooblob przetwarzania, zobacz [jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="bdc15-182">For information about how toohandle blob processing triggered by a queue message, or for WebJobs SDK scenarios not specific tooblob processing, see [How toouse Azure queue storage with hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-queues-how-to.md).</span></span>

<span data-ttu-id="bdc15-183">Tematy pokrewne omówione w tym artykule Uwzględnij hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bdc15-183">Related topics covered in that article include hello following:</span></span>

* <span data-ttu-id="bdc15-184">Funkcje asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="bdc15-184">Async functions</span></span>
* <span data-ttu-id="bdc15-185">Wiele wystąpień</span><span class="sxs-lookup"><span data-stu-id="bdc15-185">Multiple instances</span></span>
* <span data-ttu-id="bdc15-186">Łagodne zamykanie</span><span class="sxs-lookup"><span data-stu-id="bdc15-186">Graceful shutdown</span></span>
* <span data-ttu-id="bdc15-187">Użyj zestawu SDK zadań Webjob atrybutów w hello treści funkcji</span><span class="sxs-lookup"><span data-stu-id="bdc15-187">Use WebJobs SDK attributes in hello body of a function</span></span>
* <span data-ttu-id="bdc15-188">Ustawianie parametrów połączenia SDK hello w kodzie.</span><span class="sxs-lookup"><span data-stu-id="bdc15-188">Set hello SDK connection strings in code.</span></span>
* <span data-ttu-id="bdc15-189">Ustawianie wartości dla zestawu SDK zadań Webjob parametrami konstruktora w kodzie</span><span class="sxs-lookup"><span data-stu-id="bdc15-189">Set values for WebJobs SDK constructor parameters in code</span></span>
* <span data-ttu-id="bdc15-190">Skonfiguruj **MaxDequeueCount** obsługi skażone obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="bdc15-190">Configure **MaxDequeueCount** for poison blob handling.</span></span>
* <span data-ttu-id="bdc15-191">Wyzwalanie funkcji ręcznie</span><span class="sxs-lookup"><span data-stu-id="bdc15-191">Trigger a function manually</span></span>
* <span data-ttu-id="bdc15-192">Zapisywanie dzienników</span><span class="sxs-lookup"><span data-stu-id="bdc15-192">Write logs</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdc15-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bdc15-193">Next steps</span></span>
<span data-ttu-id="bdc15-194">W tym artykule udostępnił przykłady kodu przedstawiające jak obiekty BLOB toohandle typowe scenariusze dotyczące pracy z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc15-194">This article has provided code samples that show how toohandle common scenarios for working with Azure blobs.</span></span> <span data-ttu-id="bdc15-195">Aby uzyskać więcej informacji na temat sposobu toouse zadań Webjob Azure i hello zestaw SDK zadań Webjob, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?linkid=390226).</span><span class="sxs-lookup"><span data-stu-id="bdc15-195">For more information about how toouse Azure WebJobs and hello WebJobs SDK, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?linkid=390226).</span></span>

