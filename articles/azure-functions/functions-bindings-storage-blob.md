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
# <a name="azure-functions-blob-storage-bindings"></a>Azure powiązania magazynu obiektów Blob funkcji
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

W tym artykule opisano sposób tooconfigure i korzystanie z usługi Azure Functions powiązania magazynu obiektów Blob platformy Azure. Wyzwalacz obsługuje funkcje platformy Azure, wejściowa i wyjściowa powiązania dla magazynu obiektów Blob platformy Azure. Na temat funkcji, które są dostępne w wszystkie powiązania [usługi Azure Functions wyzwalaczy i powiązań pojęcia](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> A [tylko kontem magazynu obiektów blob](../storage/common/storage-create-storage-account.md#blob-storage-accounts) nie jest obsługiwane. Obiekt blob magazynu wyzwalaczy i powiązań wymagają konta magazynu ogólnego przeznaczenia. 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>Obiekt blob magazynu wyzwalaczy i powiązań

Za pomocą wyzwalacza magazynu obiektów Blob platformy Azure hello, kodzie funkcja jest wywoływana po wykryciu nowych lub zaktualizowanych obiektów blob. zawartość obiektu blob Hello podano jako funkcja toohello wejściowego.

Zdefiniuj wyzwalacz magazynu obiektów blob przy użyciu hello **integracji** kartę w hello funkcje portalu. Witaj portal tworzy powitania po definicji w hello **powiązania** sekcji *function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

Obiekt blob danych wejściowych i powiązania dane wyjściowe są definiowane przy użyciu `blob` jako typ powiązania hello:

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* Witaj `path` obsługuje właściwość powiązania wyrażeń i parametry filtru. Zobacz [nazwy wzorców](#pattern).
* Witaj `connection` właściwości musi zawierać nazwę hello ustawienia aplikacji, która zawiera parametry połączenia magazynu. W portalu Azure hello, hello standardowego edytora w hello **integracji** kartę konfiguruje to ustawienie aplikacji, można wybrać konto magazynu.

> [!NOTE]
> Podczas korzystania z wyzwalacza obiektu blob w planie zużycia, może istnieć się tooa 10-minutowych opóźnienia podczas przetwarzania nowe obiekty BLOB po aplikacji funkcji przeszedł bezczynności. Po uruchomieniu aplikacji funkcja hello obiekty BLOB są przetwarzane natychmiast. tooavoid tym początkowej opóźnienia, weź pod uwagę jedną hello następujące opcje:
> - Za pomocą plan usługi aplikacji na zawsze włączone.
> - Użyj innego mechanizmu tootrigger hello obiektu blob przetwarzania, takich jak wiadomość z kolejki hello nazwa obiektu blob. Na przykład zobacz [wyzwalacza kolejki z obiektu blob danych wejściowych powiązania](#input-sample).

<a name="pattern"></a>

### <a name="name-patterns"></a>Wzorce nazw
Wzorzec nazwy obiektów blob można określić w hello `path` właściwość, która może być wyrażenie filtru lub powiązanie. Zobacz [powiązania wyrażeń i wzorce](functions-triggers-bindings.md#binding-expressions-and-patterns).

Na przykład tooblobs toofilter, rozpoczynających się od "oryginalnego" ciąg hello użyć powitania po definicji. Ta ścieżka znajduje obiektu blob o nazwie *Blob1.txt oryginalne* w hello *wejściowych* kontenera i wartość hello hello `name` zmienna w funkcji kodu jest `Blob1`.

```json
"path": "input/original-{name}",
```

Nazwa pliku obiektu blob toohello toobind i rozszerzenie oddzielnie, użyć dwóch wzorców. Ta ścieżka umożliwia znalezienie obiektu blob o nazwie *Blob1.txt oryginalne*i wartość hello hello `blobname` i `blobextension` zmienne w kodzie funkcji *Blob1 oryginalne* i *txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

Typ pliku hello obiektów blob można ograniczyć za pomocą wartości stałej dla hello rozszerzenia pliku. Na przykład tootrigger tylko na pliki PNG hello Użyj następującego wzorca:

```json
"path": "samples/{name}.png",
```

Nawiasy klamrowe są znaki specjalne w wzorce nazw. toospecify nazwy obiektów blob, które mają nawiasy klamrowe w nazwie hello, można wprowadzić za pomocą dwa nawiasy klamrowe nawiasy hello. Witaj poniższy przykład umożliwia znalezienie obiektu blob o nazwie *{20140101}-soundfile.mp3* w hello *obrazów* kontenera i hello `name` wartość zmiennej w kodzie funkcja hello jest  *soundfile.mp3*. 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>Wyzwalacz metadanych

wyzwalacz blob Hello udostępnia kilka właściwości metadanych. Te właściwości mogą służyć jako część wyrażenia powiązania w pozostałych powiązaniach lub parametrów w kodzie. Te wartości mogą być hello tej samej semantyki jako [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).

- **BlobTrigger**. Wpisz polecenie `string`. Ścieżka obiektu blob wyzwalająca Hello
- **Identyfikator URI**. Wpisz polecenie `System.Uri`. Identyfikator URI obiektu blob Hello hello lokalizacji głównej.
- **Właściwości**. Wpisz polecenie `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`. Witaj właściwości systemu obiektu blob.
- **Metadane**. Wpisz polecenie `IDictionary<string,string>`. Metadane użytkownika Hello hello obiektu blob.

<a name="receipts"></a>

### <a name="blob-receipts"></a>Potwierdzenia obiektów blob
Hello Azure Functions środowiska uruchomieniowego gwarantuje, że żadna funkcja wyzwalacza obiektu blob jest wywoływana więcej niż raz dla hello tego samego nowych lub zaktualizowanych obiektów blob. przechowuje toodetermine wersji danego obiektu blob został przetworzony, *obiektu blob potwierdzenia*.

Potwierdzenia w kontenerze o nazwie obiektu blob Azure magazynów funkcji *azure webjobs hostów* w hello kontem magazynu platformy Azure dla aplikacji funkcji (zdefiniowane przez ustawienie aplikacji hello `AzureWebJobsStorage`). Potwierdzenie obiektu blob ma hello następujących informacji:

* Funkcja wyzwalana Hello ("*&lt;funkcja Nazwa aplikacji >*. Funkcje.  *&lt;nazwy funkcji >*", na przykład:"MyFunctionApp.Functions.CopyBlob")
* Nazwa kontenera Hello
* Typ obiektu blob Hello ("BlockBlob" lub "PageBlob")
* Nazwa obiektu blob Hello
* Witaj ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")

tooforce ponowne przetworzenie obiektu blob, Usuń hello potwierdzenia obiektu blob dla tego obiektu blob z hello *azure webjobs hostów* kontenera ręcznie.

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>Obsługa skażone obiektów blob
Jeśli funkcja wyzwalacza obiektu blob nie powiodło się dla danego obiektu blob usługi Azure Functions ponownych prób, które działać łącznie 5 razy domyślnie. 

Jeśli nie wszystkie próby 5, usługi Azure Functions dodaje kolejki komunikatów tooa magazynu o nazwie *webjob blobtrigger-poison*. komunikat z kolejki Hello skażone obiektów blob jest obiekt JSON, który zawiera hello następujące właściwości:

* FunctionId (w formacie hello  *&lt;funkcja Nazwa aplikacji >*. Funkcje.  *&lt;nazwy funkcji >*)
* BlobType ("BlockBlob" lub "PageBlob")
* Właściwość ContainerName
* Element BlobName
* Element ETag (identyfikator wersji obiektów blob, na przykład: "0x8D1DC6E70A277EF")

### <a name="blob-polling-for-large-containers"></a>Sondowanie w dużych kontenerów obiektów blob
Jeśli monitorowana kontenera obiektów blob hello zawiera więcej niż 10 000 obiektów blob, hello toowatch pliki funkcji środowiska uruchomieniowego skanowania dziennika dla nowych lub zmienionych obiektów blob. Ten proces nie jest w czasie rzeczywistym. Funkcja może nie pobrać są uruchamiane kilka minut lub dłużej po utworzeniu obiektu blob hello. Ponadto [magazynu dzienniki są tworzone na "optymalnego"](/rest/api/storageservices/About-Storage-Analytics-Logging) podstawy. Nie ma żadnej gwarancji, że wszystkie zdarzenia są przechwytywane. W niektórych warunkach Dzienniki mogą zostać pominięci. Jeśli potrzebujesz przetwarzania szybsze i bardziej niezawodny obiektów blob, należy rozważyć utworzenie [komunikatu w kolejce](../storage/queues/storage-dotnet-how-to-use-queues.md) podczas tworzenia obiektu blob hello. Następnie należy użyć [wyzwalacza kolejki](functions-bindings-storage-queue.md) zamiast obiektu blob hello tooprocess wyzwalacza obiektu blob.

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>Za pomocą wyzwalacza obiektu blob i powiązania wejściowego
W przypadku funkcji .NET dostęp do danych obiektów blob hello przy użyciu parametru metody, takich jak `Stream paramName`. W tym miejscu `paramName` jest wartością hello określone w hello [konfiguracji wyzwalacza](#trigger). W przypadku funkcji Node.js hello dostępu do danych wejściowych obiektu blob danych przy użyciu `context.bindings.<name>`.

W środowisku .NET tooany hello typów można powiązać z poniższej listy hello. Jeśli używany jako powiązania wejściowego, niektóre z tych typów wymagają `inout` powiązanie kierunek *function.json*. Tym kierunku nie jest obsługiwana przez hello standardowego edytora, dlatego należy użyć hello Zaawansowany edytor.

* `TextReader`
* `Stream`
* `ICloudBlob`(wymaga kierunek powiązania "inout")
* `CloudBlockBlob`(wymaga kierunek powiązania "inout")
* `CloudPageBlob`(wymaga kierunek powiązania "inout")
* `CloudAppendBlob`(wymaga kierunek powiązania "inout")

Jeśli oczekiwano tekstu w obiektach blob, może także powiązać tooa .NET `string` typu. Tylko jest to zalecane, jeśli rozmiar obiektu blob hello jest mała, ponieważ zawartość obiektu blob całego hello są ładowane do pamięci. Ogólnie rzecz biorąc, jest preferowana toouse `Stream` lub `CloudBlockBlob` typu.

## <a name="trigger-sample"></a>Przykładowe wyzwalacza
Załóżmy, że masz powitania po function.json, który definiuje wyzwalacz magazynu obiektów blob:

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

Zobacz przykład specyficzny dla języka hello, który rejestruje hello zawartość każdy obiekt blob dodaną toohello monitorowanych kontenera.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>Przykłady wyzwalacza obiektu blob w języku C# #

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

### <a name="trigger-example-in-nodejs"></a>Przykład wyzwalacza w środowisku Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>Przy użyciu obiektu blob powiązania wyjściowego

W przypadku funkcji .NET należy użyj `out string` parametru w sygnatura funkcji lub użyj jednego z typów hello w hello następującej listy. W przypadku funkcji Node.js można uzyskiwać dostęp za pomocą obiektu blob danych wyjściowych hello `context.bindings.<name>`.

W przypadku funkcji .NET danych wyjściowych tooany hello następujące typy:

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>Wyzwalacz kolejki z obiektu blob wejściowymi i wyjściowymi próbki
Załóżmy, że masz następujące function.json hello, który definiuje [wyzwalacza magazynu kolejek](functions-bindings-storage-queue.md)magazynu obiektów blob danych wejściowych i wyjściowych magazynu obiektów blob. Użycie hello powiadomienia hello `queueTrigger` właściwości metadanych. w obiekcie blob hello, wejściowa i wyjściowa `path` właściwości:

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

Zobacz hello przykład specyficzny dla języka, który kopiuje hello blob danych wejściowych toohello dane wyjściowe z obiektu blob.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>Przykład powiązania obiektu blob w języku C# #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>Przykład powiązania obiektu blob w środowisku Node.js

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

