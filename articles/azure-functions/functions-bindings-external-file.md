---
title: "powiązania zewnętrznego pliku funkcji aaaAzure (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Przy użyciu powiązań zewnętrznych plików w usługi Azure Functions"
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a><span data-ttu-id="c6952-103">Powiązania zewnętrznego pliku funkcji platformy Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="c6952-103">Azure Functions External File bindings (Preview)</span></span>
<span data-ttu-id="c6952-104">W tym artykule opisano, jak pliki toomanipulate w z SaaS różnych dostawców (np. OneDrive, Dropbox) w ramach funkcji przy użyciu wbudowanych powiązania.</span><span class="sxs-lookup"><span data-stu-id="c6952-104">This article shows how toomanipulate files from different SaaS providers (e.g. OneDrive, Dropbox) within your function utilizing built-in bindings.</span></span> <span data-ttu-id="c6952-105">Azure functions obsługuje wyzwolenia, danych wejściowych i wyjściowych powiązania zewnętrznego pliku.</span><span class="sxs-lookup"><span data-stu-id="c6952-105">Azure functions supports trigger, input, and output bindings for external file.</span></span>

<span data-ttu-id="c6952-106">To powiązanie tworzy połączenia interfejsu API dostawcy tooSaaS lub wykorzystuje istniejące połączenia interfejsu API z grupy zasobów aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6952-106">This binding creates API connections tooSaaS providers, or uses existing API connections from your Function App's resource group.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a><span data-ttu-id="c6952-107">Obsługiwane połączenia plików</span><span class="sxs-lookup"><span data-stu-id="c6952-107">Supported File connections</span></span>

|<span data-ttu-id="c6952-108">Łącznik</span><span class="sxs-lookup"><span data-stu-id="c6952-108">Connector</span></span>|<span data-ttu-id="c6952-109">Wyzwalacz</span><span class="sxs-lookup"><span data-stu-id="c6952-109">Trigger</span></span>|<span data-ttu-id="c6952-110">Dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="c6952-110">Input</span></span>|<span data-ttu-id="c6952-111">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="c6952-111">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="c6952-112">Pole</span><span class="sxs-lookup"><span data-stu-id="c6952-112">Box</span></span>](https://www.box.com)|<span data-ttu-id="c6952-113">x</span><span class="sxs-lookup"><span data-stu-id="c6952-113">x</span></span>|<span data-ttu-id="c6952-114">x</span><span class="sxs-lookup"><span data-stu-id="c6952-114">x</span></span>|<span data-ttu-id="c6952-115">x</span><span class="sxs-lookup"><span data-stu-id="c6952-115">x</span></span>
|[<span data-ttu-id="c6952-116">Skrzynki</span><span class="sxs-lookup"><span data-stu-id="c6952-116">Dropbox</span></span>](https://www.dropbox.com)|<span data-ttu-id="c6952-117">x</span><span class="sxs-lookup"><span data-stu-id="c6952-117">x</span></span>|<span data-ttu-id="c6952-118">x</span><span class="sxs-lookup"><span data-stu-id="c6952-118">x</span></span>|<span data-ttu-id="c6952-119">x</span><span class="sxs-lookup"><span data-stu-id="c6952-119">x</span></span>
|[<span data-ttu-id="c6952-120">FTP</span><span class="sxs-lookup"><span data-stu-id="c6952-120">FTP</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|<span data-ttu-id="c6952-121">x</span><span class="sxs-lookup"><span data-stu-id="c6952-121">x</span></span>|<span data-ttu-id="c6952-122">x</span><span class="sxs-lookup"><span data-stu-id="c6952-122">x</span></span>|<span data-ttu-id="c6952-123">x</span><span class="sxs-lookup"><span data-stu-id="c6952-123">x</span></span>
|[<span data-ttu-id="c6952-124">Usługi OneDrive</span><span class="sxs-lookup"><span data-stu-id="c6952-124">OneDrive</span></span>](https://onedrive.live.com)|<span data-ttu-id="c6952-125">x</span><span class="sxs-lookup"><span data-stu-id="c6952-125">x</span></span>|<span data-ttu-id="c6952-126">x</span><span class="sxs-lookup"><span data-stu-id="c6952-126">x</span></span>|<span data-ttu-id="c6952-127">x</span><span class="sxs-lookup"><span data-stu-id="c6952-127">x</span></span>
|[<span data-ttu-id="c6952-128">OneDrive dla Firm</span><span class="sxs-lookup"><span data-stu-id="c6952-128">OneDrive for Business</span></span>](https://onedrive.live.com/about/business/)|<span data-ttu-id="c6952-129">x</span><span class="sxs-lookup"><span data-stu-id="c6952-129">x</span></span>|<span data-ttu-id="c6952-130">x</span><span class="sxs-lookup"><span data-stu-id="c6952-130">x</span></span>|<span data-ttu-id="c6952-131">x</span><span class="sxs-lookup"><span data-stu-id="c6952-131">x</span></span>
|[<span data-ttu-id="c6952-132">SFTP</span><span class="sxs-lookup"><span data-stu-id="c6952-132">SFTP</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|<span data-ttu-id="c6952-133">x</span><span class="sxs-lookup"><span data-stu-id="c6952-133">x</span></span>|<span data-ttu-id="c6952-134">x</span><span class="sxs-lookup"><span data-stu-id="c6952-134">x</span></span>|<span data-ttu-id="c6952-135">x</span><span class="sxs-lookup"><span data-stu-id="c6952-135">x</span></span>
|[<span data-ttu-id="c6952-136">Dysk Google</span><span class="sxs-lookup"><span data-stu-id="c6952-136">Google Drive</span></span>](https://www.google.com/drive/)||<span data-ttu-id="c6952-137">x</span><span class="sxs-lookup"><span data-stu-id="c6952-137">x</span></span>|<span data-ttu-id="c6952-138">x</span><span class="sxs-lookup"><span data-stu-id="c6952-138">x</span></span>|

> [!NOTE]
> <span data-ttu-id="c6952-139">Połączenia zewnętrzne pliku można również w [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="c6952-139">External File connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

## <a name="external-file-trigger-binding"></a><span data-ttu-id="c6952-140">Plik zewnętrzny wyzwolenia powiązania</span><span class="sxs-lookup"><span data-stu-id="c6952-140">External File trigger binding</span></span>

<span data-ttu-id="c6952-141">Hello Azure zewnętrzny plik wyzwalacza umożliwia monitorowanie folderu zdalnego i uruchomić kod funkcja, gdy zostaną wykryte zmiany.</span><span class="sxs-lookup"><span data-stu-id="c6952-141">hello Azure external file trigger lets you monitor a remote folder and run your function code when changes are detected.</span></span>

<span data-ttu-id="c6952-142">wyzwalacz zewnętrzny plik Hello wykorzystuje następujące obiekty JSON w hello hello `bindings` tablicy function.json</span><span class="sxs-lookup"><span data-stu-id="c6952-142">hello external file trigger uses hello following JSON objects in hello `bindings` array of function.json</span></span>

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a><span data-ttu-id="c6952-143">Wzorce nazw</span><span class="sxs-lookup"><span data-stu-id="c6952-143">Name patterns</span></span>
<span data-ttu-id="c6952-144">Wzorzec nazwy pliku można określić w hello `path` właściwości.</span><span class="sxs-lookup"><span data-stu-id="c6952-144">You can specify a file name pattern in hello `path` property.</span></span> <span data-ttu-id="c6952-145">Odwołanie do folderu Hello musi istnieć w hello SaaS dostawcy.</span><span class="sxs-lookup"><span data-stu-id="c6952-145">hello folder referenced must exist in hello SaaS provider.</span></span>
<span data-ttu-id="c6952-146">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="c6952-146">Examples:</span></span>

```json
"path": "input/original-{name}",
```

<span data-ttu-id="c6952-147">Ta ścieżka znajdował się plik o nazwie *więc Plik1.txt oryginalne* w hello *wejściowych* folderu, a wartość hello hello `name` byłoby zmiennej w kodzie funkcja `File1.txt`.</span><span class="sxs-lookup"><span data-stu-id="c6952-147">This path would find a file named *original-File1.txt* in hello *input* folder, and hello value of hello `name` variable in function code would be `File1.txt`.</span></span>

<span data-ttu-id="c6952-148">Inny przykład:</span><span class="sxs-lookup"><span data-stu-id="c6952-148">Another example:</span></span>

```json
"path": "input/{filename}.{fileextension}",
```

<span data-ttu-id="c6952-149">Ta ścieżka będzie również znaleźć w pliku o nazwie *więc Plik1.txt oryginalne*i wartość hello hello `filename` i `fileextension` będzie zmienne w kodzie funkcja *plik1 oryginalne* i  *txt*.</span><span class="sxs-lookup"><span data-stu-id="c6952-149">This path would also find a file named *original-File1.txt*, and hello value of hello `filename` and `fileextension` variables in function code would be *original-File1* and *txt*.</span></span>

<span data-ttu-id="c6952-150">Typ pliku hello plików można ograniczyć za pomocą wartości stałej dla hello rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="c6952-150">You can restrict hello file type of files by using a fixed value for hello file extension.</span></span> <span data-ttu-id="c6952-151">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c6952-151">For example:</span></span>

```json
"path": "samples/{name}.png",
```

<span data-ttu-id="c6952-152">W takim przypadku tylko *.png* pliki w hello *przykłady* funkcja hello wyzwalacza folderu.</span><span class="sxs-lookup"><span data-stu-id="c6952-152">In this case, only *.png* files in hello *samples* folder trigger hello function.</span></span>

<span data-ttu-id="c6952-153">Nawiasy klamrowe są znaki specjalne w wzorce nazw.</span><span class="sxs-lookup"><span data-stu-id="c6952-153">Curly braces are special characters in name patterns.</span></span> <span data-ttu-id="c6952-154">nazwy plików toospecify, które mają nawiasy klamrowe w nazwie hello podwójne hello nawiasów klamrowych.</span><span class="sxs-lookup"><span data-stu-id="c6952-154">toospecify file names that have curly braces in hello name, double hello curly braces.</span></span>
<span data-ttu-id="c6952-155">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c6952-155">For example:</span></span>

```json
"path": "images/{{20140101}}-{name}",
```

<span data-ttu-id="c6952-156">Ta ścieżka znajdował się plik o nazwie *{20140101}-soundfile.mp3* w hello *obrazów* folder i hello `name` wartość zmiennej w kodzie funkcja hello będzie *soundfile.mp3*.</span><span class="sxs-lookup"><span data-stu-id="c6952-156">This path would find a file named *{20140101}-soundfile.mp3* in hello *images* folder, and hello `name` variable value in hello function code would be *soundfile.mp3*.</span></span>

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a><span data-ttu-id="c6952-157">Obsługa plików skażone</span><span class="sxs-lookup"><span data-stu-id="c6952-157">Handling poison files</span></span>
<span data-ttu-id="c6952-158">W przypadku awarii funkcja wyzwalacza zewnętrznego pliku usługi Azure Functions ponowi próbę tej funkcji w górę razy too5 domyślnie (w tym hello pierwszej próby) dla danego pliku.</span><span class="sxs-lookup"><span data-stu-id="c6952-158">When an external file trigger function fails, Azure Functions retries that function up too5 times by default (including hello first try) for a given file.</span></span>
<span data-ttu-id="c6952-159">Jeśli nie wszystkie próby 5, funkcje dodaje kolejki komunikatów tooa magazynu o nazwie *webjob apihubtrigger-poison*.</span><span class="sxs-lookup"><span data-stu-id="c6952-159">If all 5 tries fail, Functions adds a message tooa Storage queue named *webjobs-apihubtrigger-poison*.</span></span> <span data-ttu-id="c6952-160">komunikat z kolejki Hello skażone plików jest obiekt JSON, który zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="c6952-160">hello queue message for poison files is a JSON object that contains hello following properties:</span></span>

* <span data-ttu-id="c6952-161">FunctionId (w formacie hello  *&lt;funkcja Nazwa aplikacji >*. Funkcje.  *&lt;nazwy funkcji >*)</span><span class="sxs-lookup"><span data-stu-id="c6952-161">FunctionId (in hello format *&lt;function app name>*.Functions.*&lt;function name>*)</span></span>
* <span data-ttu-id="c6952-162">Typ pliku</span><span class="sxs-lookup"><span data-stu-id="c6952-162">FileType</span></span>
* <span data-ttu-id="c6952-163">Nazwa folderu</span><span class="sxs-lookup"><span data-stu-id="c6952-163">FolderName</span></span>
* <span data-ttu-id="c6952-164">Nazwa pliku</span><span class="sxs-lookup"><span data-stu-id="c6952-164">FileName</span></span>
* <span data-ttu-id="c6952-165">Element ETag (identyfikator wersji pliku, na przykład: "0x8D1DC6E70A277EF")</span><span class="sxs-lookup"><span data-stu-id="c6952-165">ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")</span></span>


<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="c6952-166">Użycie wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="c6952-166">Trigger usage</span></span>
<span data-ttu-id="c6952-167">W języku C# funkcji, powiązania danych wejściowych plików toohello przy użyciu nazwanego parametru w podpisu funkcji tak samo, jak `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="c6952-167">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="c6952-168">Gdzie `T` jest typ danych hello, które mają toodeserialize hello dane, i `paramName` jest określony w nazwie hello [wyzwolenia JSON](#trigger).</span><span class="sxs-lookup"><span data-stu-id="c6952-168">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [trigger JSON](#trigger).</span></span> <span data-ttu-id="c6952-169">W przypadku funkcji Node.js dostęp przy użyciu danych pliku wejściowego hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="c6952-169">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="c6952-170">Plik Hello może być zdeserializowany, w każdym hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="c6952-170">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="c6952-171">Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — jest to przydatne w przypadku danych pliku serializacji JSON.</span><span class="sxs-lookup"><span data-stu-id="c6952-171">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="c6952-172">W przypadku niestandardowy typ danych wejściowych (np. `FooType`), usługi Azure Functions prób toodeserialize hello JSON danych w sieci określonego typu.</span><span class="sxs-lookup"><span data-stu-id="c6952-172">If you declare a custom input type (e.g. `FooType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="c6952-173">Parametry - przydatne w przypadku danych pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c6952-173">String - useful for text file data.</span></span>

<span data-ttu-id="c6952-174">W języku C# funkcje może także powiązać tooany hello następujące typy i środowisko uruchomieniowe Functions hello podejmuje próbę deserializacji hello pliku danych przy użyciu typu:</span><span class="sxs-lookup"><span data-stu-id="c6952-174">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a><span data-ttu-id="c6952-175">Przykładowe wyzwalacza</span><span class="sxs-lookup"><span data-stu-id="c6952-175">Trigger sample</span></span>
<span data-ttu-id="c6952-176">Załóżmy, że masz następujące function.json hello, który definiuje wyzwalacza zewnętrznego pliku:</span><span class="sxs-lookup"><span data-stu-id="c6952-176">Suppose you have hello following function.json, that defines an external file trigger:</span></span>

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

<span data-ttu-id="c6952-177">Zobacz przykład specyficzny dla języka hello, który rejestruje hello zawartości każdego pliku, który zostanie dodany folder monitorowanych toohello.</span><span class="sxs-lookup"><span data-stu-id="c6952-177">See hello language-specific sample that logs hello contents of each file that is added toohello monitored folder.</span></span>

* [<span data-ttu-id="c6952-178">C#</span><span class="sxs-lookup"><span data-stu-id="c6952-178">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="c6952-179">Node.js</span><span class="sxs-lookup"><span data-stu-id="c6952-179">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a><span data-ttu-id="c6952-180">Użycie wyzwalacza w języku C#</span><span class="sxs-lookup"><span data-stu-id="c6952-180">Trigger usage in C#</span></span> #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a><span data-ttu-id="c6952-181">Użycie wyzwalacza w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="c6952-181">Trigger usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a><span data-ttu-id="c6952-182">Powiązanie danych wejściowych plików zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="c6952-182">External File input binding</span></span>
<span data-ttu-id="c6952-183">powiązania wejściowego Hello Azure zewnętrznego pliku umożliwia toouse pliku z zewnętrznego folderu w funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6952-183">hello Azure external file input binding enables you toouse a file from an external folder in your function.</span></span>

<span data-ttu-id="c6952-184">Witaj zewnętrznego pliku wejściowego tooa funkcja używa hello następujące obiekty JSON w hello `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="c6952-184">hello external file input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

<span data-ttu-id="c6952-185">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c6952-185">Note hello following:</span></span>

* <span data-ttu-id="c6952-186">`path`musi zawierać nazwę folderu hello i nazwa pliku hello.</span><span class="sxs-lookup"><span data-stu-id="c6952-186">`path` must contain hello folder name and hello file name.</span></span> <span data-ttu-id="c6952-187">Na przykład, jeśli masz [wyzwalacza kolejki](functions-bindings-storage-queue.md) w funkcji, można użyć `"path": "samples-workitems/{queueTrigger}"` toopoint tooa pliku w hello `samples-workitems` folder o nazwie, który odpowiada nazwie pliku hello określonymi w komunikacie wyzwalacza hello.</span><span class="sxs-lookup"><span data-stu-id="c6952-187">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="c6952-188">Użycie wejściowych</span><span class="sxs-lookup"><span data-stu-id="c6952-188">Input usage</span></span>
<span data-ttu-id="c6952-189">W języku C# funkcji, powiązania danych wejściowych plików toohello przy użyciu nazwanego parametru w podpisu funkcji tak samo, jak `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="c6952-189">In C# functions, you bind toohello input file data by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="c6952-190">Gdzie `T` jest typ danych hello, które mają toodeserialize hello dane, i `paramName` jest określony w nazwie hello [wejściowych powiązania](#input).</span><span class="sxs-lookup"><span data-stu-id="c6952-190">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in the [input binding](#input).</span></span> <span data-ttu-id="c6952-191">W przypadku funkcji Node.js dostęp przy użyciu danych pliku wejściowego hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="c6952-191">In Node.js functions, you access hello input file data using `context.bindings.<name>`.</span></span>

<span data-ttu-id="c6952-192">Plik Hello może być zdeserializowany, w każdym hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="c6952-192">hello file can be deserialized into any of hello following types:</span></span>

* <span data-ttu-id="c6952-193">Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — jest to przydatne w przypadku danych pliku serializacji JSON.</span><span class="sxs-lookup"><span data-stu-id="c6952-193">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized file data.</span></span>
  <span data-ttu-id="c6952-194">W przypadku niestandardowy typ danych wejściowych (np. `InputType`), usługi Azure Functions prób toodeserialize hello JSON danych w sieci określonego typu.</span><span class="sxs-lookup"><span data-stu-id="c6952-194">If you declare a custom input type (e.g. `InputType`), Azure Functions attempts toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="c6952-195">Parametry - przydatne w przypadku danych pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c6952-195">String - useful for text file data.</span></span>

<span data-ttu-id="c6952-196">W języku C# funkcje może także powiązać tooany hello następujące typy i środowisko uruchomieniowe Functions hello podejmuje próbę deserializacji hello pliku danych przy użyciu typu:</span><span class="sxs-lookup"><span data-stu-id="c6952-196">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime attempts to deserialize hello file data using that type:</span></span>

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a><span data-ttu-id="c6952-197">Powiązania wyjściowego pliku zewnętrznego</span><span class="sxs-lookup"><span data-stu-id="c6952-197">External File output binding</span></span>
<span data-ttu-id="c6952-198">Hello Azure zewnętrznego pliku danych wyjściowych powiązanie umożliwia toowrite pliki tooan zewnętrznego folderu w funkcji.</span><span class="sxs-lookup"><span data-stu-id="c6952-198">hello Azure external file output binding enables you toowrite files tooan external folder in your function.</span></span>

<span data-ttu-id="c6952-199">Witaj zewnętrznego pliku wyjściowego dla następujących obiektów JSON w hello hello używa funkcji `bindings` tablicy function.json:</span><span class="sxs-lookup"><span data-stu-id="c6952-199">hello external file output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

<span data-ttu-id="c6952-200">Należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c6952-200">Note hello following:</span></span>

* <span data-ttu-id="c6952-201">`path`musi zawierać nazwę folderu hello i toowrite nazwę pliku hello do.</span><span class="sxs-lookup"><span data-stu-id="c6952-201">`path` must contain hello folder name and hello file name toowrite to.</span></span> <span data-ttu-id="c6952-202">Na przykład, jeśli masz [wyzwalacza kolejki](functions-bindings-storage-queue.md) w funkcji, można użyć `"path": "samples-workitems/{queueTrigger}"` toopoint tooa pliku w hello `samples-workitems` folder o nazwie, który odpowiada nazwie pliku hello określonymi w komunikacie wyzwalacza hello.</span><span class="sxs-lookup"><span data-stu-id="c6952-202">For example, if you have a [queue trigger](functions-bindings-storage-queue.md) in your function, you can use `"path": "samples-workitems/{queueTrigger}"` toopoint tooa file in hello `samples-workitems` folder with a name that matches hello file name specified in hello trigger message.</span></span>   

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="c6952-203">Użycie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c6952-203">Output usage</span></span>
<span data-ttu-id="c6952-204">W języku C# funkcji, powiązania toohello pliku wyjściowego przy użyciu hello o nazwie `out` parametru w podpisu funkcji, takich jak `out <T> <name>`, gdzie `T` jest typ danych hello, które mają tooserialize hello dane, i `paramName` jest hello wybraną nazwę określony w [powiązania wyjściowego](#output).</span><span class="sxs-lookup"><span data-stu-id="c6952-204">In C# functions, you bind toohello output file by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in the [output binding](#output).</span></span> <span data-ttu-id="c6952-205">W funkcji Node.js uzyskujesz dostęp za pomocą pliku wyjściowego hello `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="c6952-205">In Node.js functions, you access hello output file using `context.bindings.<name>`.</span></span>

<span data-ttu-id="c6952-206">Można zapisać pliku wyjściowego toohello przy użyciu dowolnego hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="c6952-206">You can write toohello output file using any of hello following types:</span></span>

* <span data-ttu-id="c6952-207">Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — jest to przydatne w przypadku serializacji JSON.</span><span class="sxs-lookup"><span data-stu-id="c6952-207">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialization.</span></span>
  <span data-ttu-id="c6952-208">W przypadku typu danych wyjściowych niestandardowego (np. `out OutputType paramName`), usługi Azure Functions prób tooserialize obiektu do postaci JSON.</span><span class="sxs-lookup"><span data-stu-id="c6952-208">If you declare a custom output type (e.g. `out OutputType paramName`), Azure Functions attempts tooserialize object into JSON.</span></span> <span data-ttu-id="c6952-209">Jeśli parametr wyjściowy hello ma wartość null, gdy funkcja hello jest kończona, środowisko uruchomieniowe Functions hello tworzy plik jako obiekt null.</span><span class="sxs-lookup"><span data-stu-id="c6952-209">If hello output parameter is null when hello function exits, hello Functions runtime creates a file as a null object.</span></span>
* <span data-ttu-id="c6952-210">Parametry - (`out string paramName`) przydatne w przypadku danych pliku tekstowego.</span><span class="sxs-lookup"><span data-stu-id="c6952-210">String - (`out string paramName`) useful for text file data.</span></span> <span data-ttu-id="c6952-211">środowisko uruchomieniowe Functions Hello tworzy plik tylko wtedy, gdy parametr ciągu jest różna od null, gdy funkcja hello jest kończona.</span><span class="sxs-lookup"><span data-stu-id="c6952-211">hello Functions runtime creates a file only if the string parameter is non-null when hello function exits.</span></span>

<span data-ttu-id="c6952-212">W języku C# funkcji można również output tooany hello następujące typy:</span><span class="sxs-lookup"><span data-stu-id="c6952-212">In C# functions you can also output tooany of hello following types:</span></span>

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a><span data-ttu-id="c6952-213">Dane wejściowe + przykładowe dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="c6952-213">Input + Output sample</span></span>
<span data-ttu-id="c6952-214">Załóżmy, że masz następujące function.json hello, który definiuje [wyzwalacza kolejki magazynu](functions-bindings-storage-queue.md)zewnętrzny plik wejściowy i wyjściowy plik:</span><span class="sxs-lookup"><span data-stu-id="c6952-214">Suppose you have hello following function.json, that defines a [Storage queue trigger](functions-bindings-storage-queue.md), an external file input, and an external file output:</span></span>

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="c6952-215">Zobacz hello próbki specyficzny dla języka, który kopiuje plik wyjściowy toohello pliku wejściowego hello.</span><span class="sxs-lookup"><span data-stu-id="c6952-215">See hello language-specific sample that copies hello input file toohello output file.</span></span>

* [<span data-ttu-id="c6952-216">C#</span><span class="sxs-lookup"><span data-stu-id="c6952-216">C#</span></span>](#incsharp)
* [<span data-ttu-id="c6952-217">Node.js</span><span class="sxs-lookup"><span data-stu-id="c6952-217">Node.js</span></span>](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="c6952-218">Użycie w języku C#</span><span class="sxs-lookup"><span data-stu-id="c6952-218">Usage in C#</span></span> #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a><span data-ttu-id="c6952-219">Użycie w środowisku Node.js</span><span class="sxs-lookup"><span data-stu-id="c6952-219">Usage in Node.js</span></span>

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="c6952-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c6952-220">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
