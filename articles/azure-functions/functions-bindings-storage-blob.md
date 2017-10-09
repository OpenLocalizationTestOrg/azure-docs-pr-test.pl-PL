---
title: "powiązania funkcji magazynu obiektów Blob aaaAzure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wyzwala toouse usługi Azure Storage i powiązania usługi Azure Functions."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "funkcje usługi Azure, funkcje, przetwarzania zdarzeń, dynamiczne obliczeń niekorzystającą architektury"
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a><span data-ttu-id="e2fc2-104">Azure powiązania magazynu obiektów Blob funkcji</span><span class="sxs-lookup"><span data-stu-id="e2fc2-104">Azure Functions Blob storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e2fc2-105">W tym artykule opisano sposób tooconfigure i korzystanie z usługi Azure Functions powiązania magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-105">This article explains how tooconfigure and work with Azure Blob storage bindings in Azure Functions.</span></span> <span data-ttu-id="e2fc2-106">Wyzwalacz obsługuje funkcje platformy Azure, wejściowa i wyjściowa powiązania dla magazynu obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-106">Azure Functions supports trigger, input, and output bindings for Azure Blob storage.</span></span> <span data-ttu-id="e2fc2-107">Na temat funkcji, które są dostępne w wszystkie powiązania [usługi Azure Functions wyzwalaczy i powiązań pojęcia](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="e2fc2-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> <span data-ttu-id="e2fc2-108">A [tylko kontem magazynu obiektów blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts) nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-108">A [blob only storage account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) is not supported.</span></span> <span data-ttu-id="e2fc2-109">Obiekt blob magazynu wyzwalaczy i powiązań wymagają konta magazynu ogólnego przeznaczenia.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-109">Blob storage triggers and bindings require a general-purpose storage account.</span></span> 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a><span data-ttu-id="e2fc2-110">Obiekt blob magazynu wyzwalaczy i powiązań</span><span class="sxs-lookup"><span data-stu-id="e2fc2-110">Blob storage triggers and bindings</span></span>

<span data-ttu-id="e2fc2-111">Za pomocą wyzwalacza magazynu obiektów Blob platformy Azure hello, kodzie funkcja jest wywoływana po wykryciu nowych lub zaktualizowanych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-111">Using hello Azure Blob storage trigger, your function code is called when a new or updated blob is detected.</span></span> <span data-ttu-id="e2fc2-112">zawartość obiektu blob Hello podano jako funkcja toohello wejściowego.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-112">hello blob contents are provided as input toohello function.</span></span>

<span data-ttu-id="e2fc2-113">Zdefiniuj wyzwalacz magazynu obiektów blob przy użyciu hello **integracji** kartę w hello funkcje portalu.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-113">Define a blob storage trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="e2fc2-114">Witaj portal tworzy powitania po definicji w hello **powiązania** sekcji *function.json*:</span><span class="sxs-lookup"><span data-stu-id="e2fc2-114">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

<span data-ttu-id="e2fc2-115">Obiekt blob danych wejściowych i powiązania dane wyjściowe są definiowane przy użyciu `blob` jako typ powiązania hello:</span><span class="sxs-lookup"><span data-stu-id="e2fc2-115">Blob input and output bindings are defined using `blob` as hello binding type:</span></span>

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* <span data-ttu-id="e2fc2-116">Witaj `path` obsługuje właściwość powiązania wyrażeń i parametry filtru.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-116">hello `path` property supports binding expressions and filter parameters.</span></span> <span data-ttu-id="e2fc2-117">Zobacz [nazwy wzorców](#pattern).</span><span class="sxs-lookup"><span data-stu-id="e2fc2-117">See [Name patterns](#pattern).</span></span>
* <span data-ttu-id="e2fc2-118">Witaj `connection` właściwości musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-118">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="e2fc2-119">W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji, można wybrać konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-119">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="e2fc2-120">Podczas korzystania z wyzwalacza obiektu blob w planie zużycia, może istnieć się tooa 10-minutowych opóźnienia podczas przetwarzania nowe obiekty BLOB po aplikacji funkcji przeszedł bezczynności.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-120">When you're using a blob trigger on a Consumption plan, there can be up tooa 10-minute delay in processing new blobs after a function app has gone idle.</span></span> <span data-ttu-id="e2fc2-121">Po uruchomieniu aplikacji funkcja hello obiekty BLOB są przetwarzane natychmiast.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-121">After hello function app is running, blobs are processed immediately.</span></span> <span data-ttu-id="e2fc2-122">tooavoid tym początkowej opóźnienia, weź pod uwagę jedną hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="e2fc2-122">tooavoid this initial delay, consider one of hello following options:</span></span>
> - <span data-ttu-id="e2fc2-123">Za pomocą plan usługi aplikacji na zawsze włączone.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-123">Use an App Service plan with Always On enabled.</span></span>
> - <span data-ttu-id="e2fc2-124">Użyj innego mechanizmu tootrigger hello obiektu blob przetwarzania, takich jak wiadomość z kolejki hello nazwa obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-124">Use another mechanism tootrigger hello blob processing, such as a queue message that contains hello blob name.</span></span> <span data-ttu-id="e2fc2-125">Na przykład zobacz [wyzwalacza kolejki z obiektu blob danych wejściowych powiązania](#input-sample).</span><span class="sxs-lookup"><span data-stu-id="e2fc2-125">For an example, see [Queue trigger with blob input binding](#input-sample).</span></span>

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="e2fc2-126">Wzorce nazw</span><span class="sxs-lookup"><span data-stu-id="e2fc2-126">Name patterns</span></span>
<span data-ttu-id="e2fc2-127">Wzorzec nazwy obiektów blob można określić w hello `path` właściwość, która może być wyrażenie filtru lub powiązanie.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-127">You can specify a blob name pattern in hello `path` property, which can be a filter or binding expression.</span></span> <span data-ttu-id="e2fc2-128">Zobacz [powiązania wyrażeń i wzorce](functions-triggers-bindings.md#binding-expressions-and-patterns).</span><span class="sxs-lookup"><span data-stu-id="e2fc2-128">See [Binding expressions and patterns](functions-triggers-bindings.md#binding-expressions-and-patterns).</span></span>

<span data-ttu-id="e2fc2-129">Na przykład tooblobs toofilter, rozpoczynających się od "oryginalnego" ciąg hello użyć powitania po definicji.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-129">For example, toofilter tooblobs that start with hello string "original," use hello following definition.</span></span> <span data-ttu-id="e2fc2-130">Ta ścieżka znajduje obiektu blob o nazwie *Blob1.txt oryginalne* w hello *wejściowych* kontenera i wartość hello hello `name` zmienna w funkcji kodu jest `Blob1`.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-130">This path finds a blob named *original-Blob1.txt* in hello *input* container, and hello value of hello `name` variable in function code is `Blob1`.</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="e2fc2-131">Nazwa pliku obiektu blob toohello toobind i rozszerzenie oddzielnie, użyć dwóch wzorców.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-131">toobind toohello blob file name and extension separately, use two patterns.</span></span> <span data-ttu-id="e2fc2-132">Ta ścieżka umożliwia znalezienie obiektu blob o nazwie *Blob1.txt oryginalne*i wartość hello hello `blobname` i `blobextension` zmienne w kodzie funkcji *Blob1 oryginalne* i *txt*.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-132">This path also finds a blob named *original-Blob1.txt*, and hello value of hello `blobname` and `blobextension` variables in function code are *original-Blob1* and *txt*.</span></span>

```json
"path": "input/{blobname}.{blobextension}",
```

<span data-ttu-id="e2fc2-133">Typ pliku hello obiektów blob można ograniczyć za pomocą wartości stałej dla hello rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-133">You can restrict hello file type of blobs by using a fixed value for hello file extension.</span></span> <span data-ttu-id="e2fc2-134">Na przykład tootrigger tylko na pliki PNG hello Użyj następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="e2fc2-134">For instance, tootrigger only on .png files, use hello following pattern:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="e2fc2-135">Nawiasy klamrowe są znaki specjalne w wzorce nazw.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-135">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="e2fc2-136">toospecify nazwy obiektów blob, które mają nawiasy klamrowe w nazwie hello, można wprowadzić za pomocą dwa nawiasy klamrowe nawiasy hello.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-136">toospecify blob names that have curly braces in hello name, you can escape hello braces using two braces.</span></span> <span data-ttu-id="e2fc2-137">Witaj poniższy przykład umożliwia znalezienie obiektu blob o nazwie *{20140101}-soundfile.mp3* w hello *obrazów* kontenera i hello `name` wartość zmiennej w kodzie funkcja hello jest  *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-137">hello following example finds a blob named *{20140101}-soundfile.mp3* in hello *images* container, and hello `name` variable value in hello function code is *soundfile.mp3*.</span></span> 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a><span data-ttu-id="e2fc2-138">Wyzwalacz metadanych</span><span class="sxs-lookup"><span data-stu-id="e2fc2-138">Trigger metadata</span></span>

<span data-ttu-id="e2fc2-139">wyzwalacz blob Hello udostępnia kilka właściwości metadanych.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-139">hello blob trigger provides several metadata properties.</span></span> <span data-ttu-id="e2fc2-140">Te właściwości mogą służyć jako część wyrażenia powiązania w pozostałych powiązaniach lub parametrów w kodzie.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-140">These properties can be used as part of bindings expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="e2fc2-141">Te wartości mogą być hello tej samej semantyki jako [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="e2fc2-141">These values have hello same semantics as [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).</span></span>

- <span data-ttu-id="e2fc2-142">**BlobTrigger**.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-142">**BlobTrigger**.</span></span> <span data-ttu-id="e2fc2-143">Wpisz polecenie `string`.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-143">Type `string`.</span></span> <span data-ttu-id="e2fc2-144">Ścieżka obiektu blob wyzwalająca Hello</span><span class="sxs-lookup"><span data-stu-id="e2fc2-144">hello triggering blob path</span></span>
- <span data-ttu-id="e2fc2-145">**Identyfikator URI**.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-145">**Uri**.</span></span> <span data-ttu-id="e2fc2-146">Wpisz polecenie `System.Uri`.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-146">Type `System.Uri`.</span></span> <span data-ttu-id="e2fc2-147">Identyfikator URI obiektu blob Hello hello lokalizacji głównej.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-147">hello blob's URI for hello primary location.</span></span>
- <span data-ttu-id="e2fc2-148">**Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-148">**Properties**.</span></span> <span data-ttu-id="e2fc2-149">Wpisz polecenie `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-149">Type `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`.</span></span> <span data-ttu-id="e2fc2-150">Witaj właściwości systemu obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-150">hello blob's system properties.</span></span>
- <span data-ttu-id="e2fc2-151">**Metadane**.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-151">**Metadata**.</span></span> <span data-ttu-id="e2fc2-152">Wpisz polecenie `IDictionary<string,string>`.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-152">Type `IDictionary<string,string>`.</span></span> <span data-ttu-id="e2fc2-153">Metadane użytkownika Hello hello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-153">hello user-defined metadata for hello blob.</span></span>

<a name="receipts"></a>

### <a name="blob-receipts"></a><span data-ttu-id="e2fc2-154">Potwierdzenia obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e2fc2-154">Blob receipts</span></span>
<span data-ttu-id="e2fc2-155">Hello Azure Functions środowiska uruchomieniowego gwarantuje, że żadna funkcja wyzwalacza obiektu blob jest wywoływana więcej niż raz dla hello tego samego nowych lub zaktualizowanych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-155">hello Azure Functions runtime ensures that no blob trigger function gets called more than once for hello same new or updated blob.</span></span> <span data-ttu-id="e2fc2-156">przechowuje toodetermine wersji danego obiektu blob został przetworzony, *obiektu blob potwierdzenia*.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-156">toodetermine if a given blob version has been processed, it maintains *blob receipts*.</span></span>

<span data-ttu-id="e2fc2-157">Potwierdzenia w kontenerze o nazwie obiektu blob Azure magazynów funkcji *azure webjobs hostów* w hello kontem magazynu platformy Azure dla aplikacji funkcji (zdefiniowane przez ustawienie aplikacji hello `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="e2fc2-157">Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in hello Azure storage account for your function app (defined by hello app setting `AzureWebJobsStorage`).</span></span> <span data-ttu-id="e2fc2-158">Potwierdzenie obiektu blob ma hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="e2fc2-158">A blob receipt has hello following information:</span></span>

* <span data-ttu-id="e2fc2-159">Funkcja wyzwalana Hello ("*&lt;funkcja Nazwa aplikacji >*. Funkcje.  *&lt;nazwy funkcji >*", na przykład:"MyFunctionApp.Functions.CopyBlob")</span><span class="sxs-lookup"><span data-stu-id="e2fc2-159">hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "MyFunctionApp.Functions.CopyBlob")</span></span>
* <span data-ttu-id="e2fc2-160">Nazwa kontenera Hello</span><span class="sxs-lookup"><span data-stu-id="e2fc2-160">hello container name</span></span>
* <span data-ttu-id="e2fc2-161">Typ obiektu blob Hello ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="e2fc2-161">hello blob type ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="e2fc2-162">Nazwa obiektu blob Hello</span><span class="sxs-lookup"><span data-stu-id="e2fc2-162">hello blob name</span></span>
* <span data-ttu-id="e2fc2-163">Witaj ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="e2fc2-163">hello ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

<span data-ttu-id="e2fc2-164">tooforce ponowne przetworzenie obiektu blob, Usuń hello potwierdzenia obiektu blob dla tego obiektu blob z hello *azure webjobs hostów* kontenera ręcznie.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-164">tooforce reprocessing of a blob, delete hello blob receipt for that blob from hello *azure-webjobs-hosts* container manually.</span></span>

<a name="poison"></a>

### <a name="handling-poison-blobs"></a><span data-ttu-id="e2fc2-165">Obsługa skażone obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e2fc2-165">Handling poison blobs</span></span>
<span data-ttu-id="e2fc2-166">Jeśli funkcja wyzwalacza obiektu blob nie powiodło się dla danego obiektu blob usługi Azure Functions ponownych prób, które działać łącznie 5 razy domyślnie.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-166">When a blob trigger function fails for a given blob, Azure Functions retries that function a total of 5 times by default.</span></span> 

<span data-ttu-id="e2fc2-167">Jeśli nie wszystkie próby 5, usługi Azure Functions dodaje kolejki komunikatów tooa magazynu o nazwie *webjob blobtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-167">If all 5 tries fail, Azure Functions adds a message tooa Storage queue named *webjobs-blobtrigger-poison*.</span></span> <span data-ttu-id="e2fc2-168">komunikat z kolejki Hello skażone obiektów blob jest obiekt JSON, który zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="e2fc2-168">hello queue message for poison blobs is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="e2fc2-169">FunctionId (w formacie hello  *&lt;funkcja Nazwa aplikacji >*. Funkcje.  *&lt;nazwy funkcji >*)</span><span class="sxs-lookup"><span data-stu-id="e2fc2-169">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="e2fc2-170">BlobType ("BlockBlob" lub "PageBlob")</span><span class="sxs-lookup"><span data-stu-id="e2fc2-170">BlobType ("BlockBlob" or "PageBlob")</span></span>
* <span data-ttu-id="e2fc2-171">Właściwość ContainerName</span><span class="sxs-lookup"><span data-stu-id="e2fc2-171">ContainerName</span></span>
* <span data-ttu-id="e2fc2-172">Element BlobName</span><span class="sxs-lookup"><span data-stu-id="e2fc2-172">BlobName</span></span>
* <span data-ttu-id="e2fc2-173">Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="e2fc2-173">ETag (a blob version identifier, for example: "0x8D1DC6E70A277EF")</span></span>

### <a name="blob-polling-for-large-containers"></a><span data-ttu-id="e2fc2-174">Sondowanie w dużych kontenerów obiektów blob</span><span class="sxs-lookup"><span data-stu-id="e2fc2-174">Blob polling for large containers</span></span>
<span data-ttu-id="e2fc2-175">Jeśli monitorowana kontenera obiektów blob hello zawiera więcej niż 10 000 obiektów blob, hello toowatch pliki funkcji środowiska uruchomieniowego skanowania dziennika dla nowych lub zmienionych obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-175">If hello blob container being monitored contains more than 10,000 blobs, hello Functions runtime scans log files toowatch for new or changed blobs.</span></span> <span data-ttu-id="e2fc2-176">Ten proces nie jest w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-176">This process is not real time.</span></span> <span data-ttu-id="e2fc2-177">Funkcja może nie pobrać są uruchamiane kilka minut lub dłużej po utworzeniu obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-177">A function might not get triggered until several minutes or longer after hello blob is created.</span></span> <span data-ttu-id="e2fc2-178">Ponadto [magazynu dzienniki są tworzone na "optymalnego"](/rest/api/storageservices/About-Storage-Analytics-Logging) podstawy.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-178">In addition, [storage logs are created on a "best effort"](/rest/api/storageservices/About-Storage-Analytics-Logging) basis.</span></span> <span data-ttu-id="e2fc2-179">Nie ma żadnej gwarancji, że wszystkie zdarzenia są przechwytywane.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-179">There is no guarantee that all events are captured.</span></span> <span data-ttu-id="e2fc2-180">W niektórych warunkach Dzienniki mogą zostać pominięci.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-180">Under some conditions, logs may be missed.</span></span> <span data-ttu-id="e2fc2-181">Jeśli potrzebujesz przetwarzania szybsze i bardziej niezawodny obiektów blob, należy rozważyć utworzenie [komunikatu w kolejce](../storage/queues/storage-dotnet-how-to-use-queues.md) podczas tworzenia obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-181">If you require faster or more reliable blob processing, consider creating a [queue message](../storage/queues/storage-dotnet-how-to-use-queues.md) when you create hello blob.</span></span> <span data-ttu-id="e2fc2-182">Następnie należy użyć [wyzwalacza kolejki](functions-bindings-storage-queue.md) zamiast obiektu blob hello tooprocess wyzwalacza obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-182">Then, use a [queue trigger](functions-bindings-storage-queue.md) instead of a blob trigger tooprocess hello blob.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a><span data-ttu-id="e2fc2-183">Za pomocą wyzwalacza obiektu blob i powiązania wejściowego</span><span class="sxs-lookup"><span data-stu-id="e2fc2-183">Using a blob trigger and input binding</span></span>
<span data-ttu-id="e2fc2-184">W przypadku funkcji .NET dostęp do danych obiektów blob hello przy użyciu parametru metody, takich jak `Stream paramName`.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-184">In .NET functions, access hello blob data using a method parameter such as `Stream paramName`.</span></span> <span data-ttu-id="e2fc2-185">W tym miejscu `paramName` jest wartością hello określone w hello [konfiguracji wyzwalacza](#trigger).</span><span class="sxs-lookup"><span data-stu-id="e2fc2-185">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="e2fc2-186">W przypadku funkcji Node.js hello dostępu do danych wejściowych obiektu blob danych przy użyciu `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-186">In Node.js functions, access hello input blob data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e2fc2-187">W środowisku .NET tooany hello typów można powiązać z poniższej listy hello.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-187">In .NET, you can bind tooany of hello types in hello list below.</span></span> <span data-ttu-id="e2fc2-188">Jeśli używany jako powiązania wejściowego, niektóre z tych typów wymagają `inout` powiązanie kierunek *function.json*.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-188">If used as an input binding, some of these types require an `inout` binding direction in *function.json*.</span></span> <span data-ttu-id="e2fc2-189">Tym kierunku nie jest obsługiwana przez hello standardowego edytora, dlatego należy użyć hello Zaawansowany edytor.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-189">This direction is not supported by hello standard editor, so you must use hello advanced editor.</span></span>

* `TextReader`
* `Stream`
* <span data-ttu-id="e2fc2-190">`ICloudBlob`(wymaga kierunek powiązania "inout")</span><span class="sxs-lookup"><span data-stu-id="e2fc2-190">`ICloudBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="e2fc2-191">`CloudBlockBlob`(wymaga kierunek powiązania "inout")</span><span class="sxs-lookup"><span data-stu-id="e2fc2-191">`CloudBlockBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="e2fc2-192">`CloudPageBlob`(wymaga kierunek powiązania "inout")</span><span class="sxs-lookup"><span data-stu-id="e2fc2-192">`CloudPageBlob` (requires "inout" binding direction)</span></span>
* <span data-ttu-id="e2fc2-193">`CloudAppendBlob`(wymaga kierunek powiązania "inout")</span><span class="sxs-lookup"><span data-stu-id="e2fc2-193">`CloudAppendBlob` (requires "inout" binding direction)</span></span>

<span data-ttu-id="e2fc2-194">Jeśli oczekiwano tekstu w obiektach blob, może także powiązać tooa .NET `string` typu.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-194">If text blobs are expected, you can also bind tooa .NET `string` type.</span></span> <span data-ttu-id="e2fc2-195">Tylko jest to zalecane, jeśli rozmiar obiektu blob hello jest mała, ponieważ zawartość obiektu blob całego hello są ładowane do pamięci.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-195">This is only recommended if hello blob size is small, as hello entire blob contents are loaded into memory.</span></span> <span data-ttu-id="e2fc2-196">Ogólnie rzecz biorąc, jest preferowana toouse `Stream` lub `CloudBlockBlob` typu.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-196">Generally, it is preferable toouse a `Stream` or `CloudBlockBlob` type.</span></span>

## <a name="trigger-sample"></a><span data-ttu-id="e2fc2-197">Przykładowe wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="e2fc2-197">Trigger sample</span></span>
<span data-ttu-id="e2fc2-198">Załóżmy, że masz powitania po function.json, który definiuje wyzwalacz magazynu obiektów blob:</span><span class="sxs-lookup"><span data-stu-id="e2fc2-198">Suppose you have hello following function.json that defines a blob storage trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

<span data-ttu-id="e2fc2-199">Zobacz przykład specyficzny dla języka hello, który rejestruje hello zawartość każdy obiekt blob dodaną toohello monitorowanych kontenera.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-199">See hello language-specific sample that logs hello contents of each blob that is added toohello monitored container.</span></span>

* [<span data-ttu-id="e2fc2-200">C#</span><span class="sxs-lookup"><span data-stu-id="e2fc2-200">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="e2fc2-201">Node.js</span><span class="sxs-lookup"><span data-stu-id="e2fc2-201">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a><span data-ttu-id="e2fc2-202">Przykłady wyzwalacza obiektu blob w języku C#</span><span class="sxs-lookup"><span data-stu-id="e2fc2-202">Blob trigger examples in C#</span></span> #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a><span data-ttu-id="e2fc2-203">Przykład wyzwalacza w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="e2fc2-203">Trigger example in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a><span data-ttu-id="e2fc2-204">Przy użyciu obiektu blob powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="e2fc2-204">Using a blob output binding</span></span>

<span data-ttu-id="e2fc2-205">W przypadku funkcji .NET należy użyj `out string` parametru w sygnatura funkcji lub użyj jednego z typów hello w hello następującej listy.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-205">In .NET functions, you should either use a `out string` parameter in your function signature or use one of hello types in hello following list.</span></span> <span data-ttu-id="e2fc2-206">W przypadku funkcji Node.js można uzyskiwać dostęp za pomocą obiektu blob danych wyjściowych hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-206">In Node.js functions, you access hello output blob using `context.bindings.<name>`.</span></span>

<span data-ttu-id="e2fc2-207">W przypadku funkcji .NET danych wyjściowych tooany hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="e2fc2-207">In .NET functions you can output tooany of hello following types:</span></span>

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a><span data-ttu-id="e2fc2-208">Wyzwalacz kolejki z obiektu blob wejściowymi i wyjściowymi próbki</span><span class="sxs-lookup"><span data-stu-id="e2fc2-208">Queue trigger with blob input and output sample</span></span>
<span data-ttu-id="e2fc2-209">Załóżmy, że masz następujące function.json hello, który definiuje [wyzwalacza magazynu kolejek](functions-bindings-storage-queue.md)magazynu obiektów blob danych wejściowych i wyjściowych magazynu obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-209">Suppose you have hello following function.json, that defines a [Queue Storage trigger](functions-bindings-storage-queue.md), a blob storage input, and a blob storage output.</span></span> <span data-ttu-id="e2fc2-210">Użycie hello powiadomienia hello `queueTrigger` właściwości metadanych.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-210">Notice hello use of hello `queueTrigger` metadata property.</span></span> <span data-ttu-id="e2fc2-211">w obiekcie blob hello, wejściowa i wyjściowa `path` właściwości:</span><span class="sxs-lookup"><span data-stu-id="e2fc2-211">in hello blob input and output `path` properties:</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

<span data-ttu-id="e2fc2-212">Zobacz hello przykład specyficzny dla języka, który kopiuje hello blob danych wejściowych toohello dane wyjściowe z obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="e2fc2-212">See hello language-specific sample that copies hello input blob toohello output blob.</span></span>

* [<span data-ttu-id="e2fc2-213">C#</span><span class="sxs-lookup"><span data-stu-id="e2fc2-213">C#</span></span>](#incsharp)
* [<span data-ttu-id="e2fc2-214">Node.js</span><span class="sxs-lookup"><span data-stu-id="e2fc2-214">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a><span data-ttu-id="e2fc2-215">Przykład powiązania obiektu blob w języku C#</span><span class="sxs-lookup"><span data-stu-id="e2fc2-215">Blob binding example in C#</span></span> #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a><span data-ttu-id="e2fc2-216">Przykład powiązania obiektu blob w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="e2fc2-216">Blob binding example in Node.js</span></span>

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="e2fc2-217">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e2fc2-217">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

