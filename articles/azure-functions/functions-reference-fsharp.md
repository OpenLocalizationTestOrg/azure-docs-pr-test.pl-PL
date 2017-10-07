---
title: "Dokumentacja dla deweloperów funkcje F # aaaAzure | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toodevelop usługi Azure Functions przy użyciu języka F #."
services: functions
documentationcenter: fsharp
author: sylvanc
manager: jbronsk
editor: 
tags: 
keywords: "Azure funkcji, funkcji, zdarzenia przetwarzania elementów webhook, dynamiczne obliczeń, niekorzystającą architektury, F #"
ms.assetid: e60226e5-2630-41d7-9e5b-9f9e5acc8e50
ms.service: functions
ms.devlang: fsharp
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/09/2016
ms.author: syclebsc
ms.openlocfilehash: 1ac366ba6f73d191c582dcd9214b688ef719617a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-f-developer-reference"></a>Azure Functions dokumentacja dla deweloperów języka F #
> [!div class="op_single_selector"]
> * [Skryptu C#](functions-reference-csharp.md)
> * [Skrypt F #](functions-reference-fsharp.md)
> * [Node.js](functions-reference-node.md)
> 
> 

F # dla usługi Azure Functions to rozwiązanie umożliwiające łatwe uruchamianie małych fragmentów kodu lub "funkcji" w chmurze hello. Przepływy danych w funkcji F # za pomocą argumentów funkcji. Argument nazwy zostały określone w `function.json`, i jest wstępnie zdefiniowanych nazw do uzyskiwania dostępu do czynności, takie jak hello tokenów funkcja rejestratora i anulowania.

W tym artykule przyjęto, że został już przeczytany hello [dokumentacja dla deweloperów usługi Azure Functions](functions-reference.md).

## <a name="how-fsx-works"></a>Jak działa fsx
`.fsx` Plik jest skryptu języka F #. Go można traktować jako projekt F #, który jest zawarty w jednym pliku. Witaj plik zawiera zarówno kod hello programu (w tym przypadku funkcji Azure) i wytyczne dotyczące zarządzania zależności.

Jeśli używasz `.fsx` dla funkcji platformy Azure, zwykle wymagane zestawy są automatycznie dołączane dla Ciebie, umożliwiając toofocus na kod funkcji, a nie "standardowy" hello.

## <a name="binding-tooarguments"></a>Powiązanie tooarguments
Każdego powiązania obsługuje niektóre zestaw argumentów, jako hello szczegółowe w [dokumentacja dla deweloperów usługi Azure Functions wyzwalaczy i powiązań](functions-triggers-bindings.md). Na przykład jednym z powiązań argument hello obsługuje wyzwalacza obiektu blob jest POCO, które można wyrazić przy użyciu rekordu języka F #. Na przykład:

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

Funkcja Azure F # potrwa co najmniej jeden argument. Przy omawianiu usługi Azure Functions argumenty określane za*wejściowych* argumentów i *dane wyjściowe* argumentów. Argument wejściowy jest dokładnie wydaje takich jak: dane wejściowe tooyour funkcji platformy Azure F #. *Dane wyjściowe* argument jest modyfikowalna danych lub `byref<>` argumentu, który służy jako Wstecz danych toopass sposób *limit* funkcji.

W powyższym przykładzie hello `blob` jest argument wejściowy i `output` jest argumentem danych wyjściowych. Należy zauważyć, że użyliśmy `byref<>` dla `output` (nie konieczności tooadd hello nie istnieje `[<Out>]` adnotacji). Przy użyciu `byref<>` typ umożliwia Twojej toochange funkcji, który argument hello rekordu lub obiekt odwołuje się do.

Gdy rekordu języka F # jest używany jako typ danych wejściowych, muszą być oznaczone definicji rekordów hello `[<CLIMutable>]` w celu tooallow hello Azure Functions framework tooset pola hello odpowiednio przed przekazaniem hello rekordów tooyour funkcji. Pod maską hello `[<CLIMutable>]` generuje metody ustawiające właściwości rekordu hello. Na przykład:

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

Można także klasy F # dla wejściowe i wyjściowe argumentów. Dla klasy właściwości należy zwykle ustawiających i pobierających. Na przykład:

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a>Rejestrowanie
toolog output tooyour [Podgląd dzienników przesyłanych strumieniowo](../app-service-web/web-sites-streaming-logs-and-console.md) w języku F #, funkcja powinno zająć argumentu typu `TraceWriter`. W celu zachowania spójności, firma Microsoft zaleca, nosi nazwę tego argumentu `log`. Na przykład:

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a>Asynchroniczne
Witaj `async` przepływ pracy może być używany, ale wynik hello wymagane tooreturn `Task`. Można to zrobić z `Async.StartAsTask`, na przykład:

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a>Token anulowania
Jeśli funkcja wymaga zamknięcia toohandle bezpiecznie, można nadać [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argumentu. Może to być łączone z `async`, na przykład:

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a>Importowanie przestrzenie nazw
Przestrzenie nazw mogą być otwierane w hello zwykły sposób:

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Witaj następujące przestrzenie nazw są automatycznie otwierane:

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`.

## <a name="referencing-external-assemblies"></a>Zewnętrzne zestawy odwołujące
Podobnie, zestawu struktury odwołania do dodania z hello `#r "AssemblyName"` dyrektywy.

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

Witaj następujące zestawy są automatycznie dodawane hello Azure Functions Środowisko hostingu:

* `mscorlib`,
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`.

Ponadto hello następujące zestawy są specjalne z uwzględnieniem wielkości liter i odwołuje simplename (np. `#r "AssemblyName"`):

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNEt.WebHooks.Common`.

Jeśli potrzebujesz tooreference zestaw prywatny, możesz przekazać plik zestawu hello do `bin` folderu względna tooyour funkcji i odwołanie hello go przy użyciu nazwy pliku (np.  `#r "MyAssembly.dll"`). Dla informacji na temat sposobu tooupload folder funkcja tooyour plików Zobacz hello następujących sekcji, pakiet zarządzania.

## <a name="editor-prelude"></a>Edytor Prelude
Edytor, który obsługuje usługi kompilatora F # nie będą świadomi hello obszary nazw i zestawy, które automatycznie uwzględnia usługi Azure Functions. Tak może być przydatne tooinclude prelude, pomocne w edytorze hello odnaleźć zestawów hello, którego używasz, i tooexplicitly otworzyć przestrzeni nazw. Na przykład:

```fsharp
#if !COMPILED
#I "../../bin/Binaries/WebJobs.Script.Host"
#r "Microsoft.Azure.WebJobs.Host.dll"
#endif

open Sytem
open Microsoft.Azure.WebJobs.Host

let Run(blob: string, output: byref<string>, log: TraceWriter) =
    ...
```

Azure Functions wykonuje kodu, przetwarza hello źródło o `COMPILED` zdefiniowane, więc prelude Edytor hello zostaną zignorowane.

<a name="package"></a>

## <a name="package-management"></a>Pakiet zarządzania
Dodawanie pakietów NuGet toouse w F # funkcji `project.json` toohello hello funkcja folder pliku w systemie plików hello funkcji aplikacji. Oto przykład `project.json` pliku, który dodaje odwołanie do pakietu NuGet zbyt`Microsoft.ProjectOxford.Face` wersji 1.1.0:

```json
{
  "frameworks": {
    "net46":{
      "dependencies": {
        "Microsoft.ProjectOxford.Face": "1.1.0"
      }
    }
   }
}
```

Witaj .NET Framework 4.6 jest obsługiwana tylko, upewnij się, że Twoje `project.json` Określa plik `net46` w sposób pokazany poniżej.

Po przekazaniu `project.json` plików, hello środowiska uruchomieniowego pobiera pakiety hello i automatycznie dodaje odwołania toohello pakiet zestawów. Nie ma potrzeby tooadd `#r "AssemblyName"` dyrektywy. Po prostu Dodaj wymagane hello `open` tooyour instrukcje `.fsx` pliku.

Warto zapoznać się, że tooput automatycznie odwołuje się do zestawów w Twojej prelude edytora, tooimprove w edytorze interakcji z F # kompilacji usługi.

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a>Jak tooadd `project.json` pliku tooyour funkcji platformy Azure
1. Rozpocznij od upewnić się, że funkcja aplikacji jest uruchomiony, co można zrobić, otwierając funkcji w hello portalu Azure. Zapewnia to również dostęp do dzienników przesyłania strumieniowego toohello gdzie zostaną wyświetlone dane wyjściowe instalacji pakietu.
2. tooupload `project.json` plików, użyj jednej z metod hello opisanych w [jak tooupdate funkcji pliki aplikacji](functions-reference.md#fileupdate). Jeśli używasz [ciągłego wdrażania usługi Azure Functions](functions-continuous-deployment.md), możesz dodać `project.json` pliku tooyour przemieszczania gałąź w kolejności tooexperiment z nim przed dodaniem go tooyour wdrożenia gałęzi.
3. Po hello `project.json` zostanie dodany plik, zostanie wyświetlone dane wyjściowe toohello podobnie poniższy przykład w funkcji do przesyłania strumieniowego dziennika:

```
2016-04-04T19:02:48.745 Restoring packages.
2016-04-04T19:02:48.745 Starting NuGet restore
2016-04-04T19:02:50.183 MSBuild auto-detection: using msbuild version '14.0' from 'D:\Program Files (x86)\MSBuild\14.0\bin'.
2016-04-04T19:02:50.261 Feeds used:
2016-04-04T19:02:50.261 C:\DWASFiles\Sites\facavalfunctest\LocalAppData\NuGet\Cache
2016-04-04T19:02:50.261 https://api.nuget.org/v3/index.json
2016-04-04T19:02:50.261
2016-04-04T19:02:50.511 Restoring packages for D:\home\site\wwwroot\HttpTriggerCSharp1\Project.json...
2016-04-04T19:02:52.800 Installing Newtonsoft.Json 6.0.8.
2016-04-04T19:02:52.800 Installing Microsoft.ProjectOxford.Face 1.1.0.
2016-04-04T19:02:57.095 All packages are compatible with .NETFramework,Version=v4.6.
2016-04-04T19:02:57.189
2016-04-04T19:02:57.189
2016-04-04T19:02:57.455 Packages restored.
```

## <a name="environment-variables"></a>Zmienne środowiskowe
tooget zmienną środowiskową lub wartość ustawienia aplikacji, użyj `System.Environment.GetEnvironmentVariable`, na przykład:

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a>Ponowne wykorzystywanie kodu fsx
Można użyć kodu z innych `.fsx` plików za pomocą `#load` dyrektywy. Na przykład:

`run.fsx`

```fsharp
#load "logger.fsx"

let Run(timer: TimerInfo, log: TraceWriter) =
    mylog log (sprintf "Timer: %s" DateTime.Now.ToString())
```

`logger.fsx`

```fsharp
let mylog(log: TraceWriter, text: string) =
    log.Verbose(text);
```

Ścieżki zapewnia toohello `#load` dyrektywy są lokalizacji względnej toohello Twojego `.fsx` pliku.

* `#load "logger.fsx"`ładuje plik znajdujący się w folderze funkcja hello.
* `#load "package\logger.fsx"`ładuje plik znajduje się w hello `package` folderu w folderze funkcja hello.
* `#load "..\shared\mylogger.fsx"`ładuje plik znajduje się w hello `shared` folderu na powitania sam poziom jako folder funkcja hello, oznacza to, bezpośrednio pod `wwwroot`.

Hello `#load` dyrektywy działa tylko z `.fsx` plików (F # skrypt), a nie z `.fs` plików.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji zobacz następujące zasoby hello:

* [Przewodnik F #](/dotnet/articles/fsharp/index)
* [Najlepsze rozwiązania dotyczące usługi Azure Functions](functions-best-practices.md)
* [Dokumentacja usługi Azure Functions dla deweloperów](functions-reference.md)
* [Azure dokumentacja dla deweloperów funkcje C#](functions-reference-csharp.md)
* [Dokumentacja dla deweloperów NodeJS funkcji platformy Azure](functions-reference-node.md)
* [Azure funkcje wyzwalaczy i powiązań](functions-triggers-bindings.md)
* [Środowisko Azure Functions testowania](functions-test-a-function.md)
* [Środowisko Azure Functions skalowania](functions-scale.md)

