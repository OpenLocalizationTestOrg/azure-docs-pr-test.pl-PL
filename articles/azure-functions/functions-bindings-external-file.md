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
# <a name="azure-functions-external-file-bindings-preview"></a>Powiązania zewnętrznego pliku funkcji platformy Azure (wersja zapoznawcza)
W tym artykule opisano, jak pliki toomanipulate w z SaaS różnych dostawców (np. OneDrive, Dropbox) w ramach funkcji przy użyciu wbudowanych powiązania. Azure functions obsługuje wyzwolenia, danych wejściowych i wyjściowych powiązania zewnętrznego pliku.

To powiązanie tworzy połączenia interfejsu API dostawcy tooSaaS lub wykorzystuje istniejące połączenia interfejsu API z grupy zasobów aplikacji funkcji.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>Obsługiwane połączenia plików

|Łącznik|Wyzwalacz|Dane wejściowe|Dane wyjściowe|
|:-----|:---:|:---:|:---:|
|[Pole](https://www.box.com)|x|x|x
|[Skrzynki](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[Usługi OneDrive](https://onedrive.live.com)|x|x|x
|[OneDrive dla Firm](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Dysk Google](https://www.google.com/drive/)||x|x|

> [!NOTE]
> Połączenia zewnętrzne pliku można również w [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)

## <a name="external-file-trigger-binding"></a>Plik zewnętrzny wyzwolenia powiązania

Hello Azure zewnętrzny plik wyzwalacza umożliwia monitorowanie folderu zdalnego i uruchomić kod funkcja, gdy zostaną wykryte zmiany.

wyzwalacz zewnętrzny plik Hello wykorzystuje następujące obiekty JSON w hello hello `bindings` tablicy function.json

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

### <a name="name-patterns"></a>Wzorce nazw
Wzorzec nazwy pliku można określić w hello `path` właściwości. Odwołanie do folderu Hello musi istnieć w hello SaaS dostawcy.
Przykłady:

```json
"path": "input/original-{name}",
```

Ta ścieżka znajdował się plik o nazwie *więc Plik1.txt oryginalne* w hello *wejściowych* folderu, a wartość hello hello `name` byłoby zmiennej w kodzie funkcja `File1.txt`.

Inny przykład:

```json
"path": "input/{filename}.{fileextension}",
```

Ta ścieżka będzie również znaleźć w pliku o nazwie *więc Plik1.txt oryginalne*i wartość hello hello `filename` i `fileextension` będzie zmienne w kodzie funkcja *plik1 oryginalne* i  *txt*.

Typ pliku hello plików można ograniczyć za pomocą wartości stałej dla hello rozszerzenia pliku. Na przykład:

```json
"path": "samples/{name}.png",
```

W takim przypadku tylko *.png* pliki w hello *przykłady* funkcja hello wyzwalacza folderu.

Nawiasy klamrowe są znaki specjalne w wzorce nazw. nazwy plików toospecify, które mają nawiasy klamrowe w nazwie hello podwójne hello nawiasów klamrowych.
Na przykład:

```json
"path": "images/{{20140101}}-{name}",
```

Ta ścieżka znajdował się plik o nazwie *{20140101}-soundfile.mp3* w hello *obrazów* folder i hello `name` wartość zmiennej w kodzie funkcja hello będzie *soundfile.mp3*.

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

### <a name="handling-poison-files"></a>Obsługa plików skażone
W przypadku awarii funkcja wyzwalacza zewnętrznego pliku usługi Azure Functions ponowi próbę tej funkcji w górę razy too5 domyślnie (w tym hello pierwszej próby) dla danego pliku.
Jeśli nie wszystkie próby 5, funkcje dodaje kolejki komunikatów tooa magazynu o nazwie *webjob apihubtrigger-poison*. komunikat z kolejki Hello skażone plików jest obiekt JSON, który zawiera hello następujące właściwości:

* FunctionId (w formacie hello  *&lt;funkcja Nazwa aplikacji >*. Funkcje.  *&lt;nazwy funkcji >*)
* Typ pliku
* Nazwa folderu
* Nazwa pliku
* Element ETag (identyfikator wersji pliku, na przykład: "0x8D1DC6E70A277EF")


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Użycie wyzwalacza
W języku C# funkcji, powiązania danych wejściowych plików toohello przy użyciu nazwanego parametru w podpisu funkcji tak samo, jak `<T> <name>`.
Gdzie `T` jest typ danych hello, które mają toodeserialize hello dane, i `paramName` jest określony w nazwie hello [wyzwolenia JSON](#trigger). W przypadku funkcji Node.js dostęp przy użyciu danych pliku wejściowego hello `context.bindings.<name>`.

Plik Hello może być zdeserializowany, w każdym hello następujące typy:

* Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — jest to przydatne w przypadku danych pliku serializacji JSON.
  W przypadku niestandardowy typ danych wejściowych (np. `FooType`), usługi Azure Functions prób toodeserialize hello JSON danych w sieci określonego typu.
* Parametry - przydatne w przypadku danych pliku tekstowego.

W języku C# funkcje może także powiązać tooany hello następujące typy i środowisko uruchomieniowe Functions hello podejmuje próbę deserializacji hello pliku danych przy użyciu typu:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>Przykładowe wyzwalacza
Załóżmy, że masz następujące function.json hello, który definiuje wyzwalacza zewnętrznego pliku:

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

Zobacz przykład specyficzny dla języka hello, który rejestruje hello zawartości każdego pliku, który zostanie dodany folder monitorowanych toohello.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>Użycie wyzwalacza w języku C# #

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

### <a name="trigger-usage-in-nodejs"></a>Użycie wyzwalacza w środowisku Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>Powiązanie danych wejściowych plików zewnętrznych
powiązania wejściowego Hello Azure zewnętrznego pliku umożliwia toouse pliku z zewnętrznego folderu w funkcji.

Witaj zewnętrznego pliku wejściowego tooa funkcja używa hello następujące obiekty JSON w hello `bindings` tablicy function.json:

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

Należy uwzględnić następujące hello:

* `path`musi zawierać nazwę folderu hello i nazwa pliku hello. Na przykład, jeśli masz [wyzwalacza kolejki](functions-bindings-storage-queue.md) w funkcji, można użyć `"path": "samples-workitems/{queueTrigger}"` toopoint tooa pliku w hello `samples-workitems` folder o nazwie, który odpowiada nazwie pliku hello określonymi w komunikacie wyzwalacza hello.   

<a name="inputusage"></a>

## <a name="input-usage"></a>Użycie wejściowych
W języku C# funkcji, powiązania danych wejściowych plików toohello przy użyciu nazwanego parametru w podpisu funkcji tak samo, jak `<T> <name>`.
Gdzie `T` jest typ danych hello, które mają toodeserialize hello dane, i `paramName` jest określony w nazwie hello [wejściowych powiązania](#input). W przypadku funkcji Node.js dostęp przy użyciu danych pliku wejściowego hello `context.bindings.<name>`.

Plik Hello może być zdeserializowany, w każdym hello następujące typy:

* Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — jest to przydatne w przypadku danych pliku serializacji JSON.
  W przypadku niestandardowy typ danych wejściowych (np. `InputType`), usługi Azure Functions prób toodeserialize hello JSON danych w sieci określonego typu.
* Parametry - przydatne w przypadku danych pliku tekstowego.

W języku C# funkcje może także powiązać tooany hello następujące typy i środowisko uruchomieniowe Functions hello podejmuje próbę deserializacji hello pliku danych przy użyciu typu:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>Powiązania wyjściowego pliku zewnętrznego
Hello Azure zewnętrznego pliku danych wyjściowych powiązanie umożliwia toowrite pliki tooan zewnętrznego folderu w funkcji.

Witaj zewnętrznego pliku wyjściowego dla następujących obiektów JSON w hello hello używa funkcji `bindings` tablicy function.json:

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

Należy uwzględnić następujące hello:

* `path`musi zawierać nazwę folderu hello i toowrite nazwę pliku hello do. Na przykład, jeśli masz [wyzwalacza kolejki](functions-bindings-storage-queue.md) w funkcji, można użyć `"path": "samples-workitems/{queueTrigger}"` toopoint tooa pliku w hello `samples-workitems` folder o nazwie, który odpowiada nazwie pliku hello określonymi w komunikacie wyzwalacza hello.   

<a name="outputusage"></a>

## <a name="output-usage"></a>Użycie danych wyjściowych
W języku C# funkcji, powiązania toohello pliku wyjściowego przy użyciu hello o nazwie `out` parametru w podpisu funkcji, takich jak `out <T> <name>`, gdzie `T` jest typ danych hello, które mają tooserialize hello dane, i `paramName` jest hello wybraną nazwę określony w [powiązania wyjściowego](#output). W funkcji Node.js uzyskujesz dostęp za pomocą pliku wyjściowego hello `context.bindings.<name>`.

Można zapisać pliku wyjściowego toohello przy użyciu dowolnego hello następujące typy:

* Wszelkie [obiektu](https://msdn.microsoft.com/library/system.object.aspx) — jest to przydatne w przypadku serializacji JSON.
  W przypadku typu danych wyjściowych niestandardowego (np. `out OutputType paramName`), usługi Azure Functions prób tooserialize obiektu do postaci JSON. Jeśli parametr wyjściowy hello ma wartość null, gdy funkcja hello jest kończona, środowisko uruchomieniowe Functions hello tworzy plik jako obiekt null.
* Parametry - (`out string paramName`) przydatne w przypadku danych pliku tekstowego. środowisko uruchomieniowe Functions Hello tworzy plik tylko wtedy, gdy parametr ciągu jest różna od null, gdy funkcja hello jest kończona.

W języku C# funkcji można również output tooany hello następujące typy:

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>Dane wejściowe + przykładowe dane wyjściowe
Załóżmy, że masz następujące function.json hello, który definiuje [wyzwalacza kolejki magazynu](functions-bindings-storage-queue.md)zewnętrzny plik wejściowy i wyjściowy plik:

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

Zobacz hello próbki specyficzny dla języka, który kopiuje plik wyjściowy toohello pliku wejściowego hello.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>Użycie w języku C# #

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

### <a name="usage-in-nodejs"></a>Użycie w środowisku Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
