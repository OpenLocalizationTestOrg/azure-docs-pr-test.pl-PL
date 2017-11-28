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
# <a name="azure-functions-f-developer-reference"></a><span data-ttu-id="0f01e-104">Azure Functions dokumentacja dla deweloperów języka F #</span><span class="sxs-lookup"><span data-stu-id="0f01e-104">Azure Functions F# Developer Reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0f01e-105">Skryptu C#</span><span class="sxs-lookup"><span data-stu-id="0f01e-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="0f01e-106">Skrypt F #</span><span class="sxs-lookup"><span data-stu-id="0f01e-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="0f01e-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="0f01e-107">Node.js</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="0f01e-108">F # dla usługi Azure Functions to rozwiązanie umożliwiające łatwe uruchamianie małych fragmentów kodu lub "funkcji" w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="0f01e-108">F# for Azure Functions is a solution for easily running small pieces of code, or "functions," in hello cloud.</span></span> <span data-ttu-id="0f01e-109">Przepływy danych w funkcji F # za pomocą argumentów funkcji.</span><span class="sxs-lookup"><span data-stu-id="0f01e-109">Data flows into your F# function via function arguments.</span></span> <span data-ttu-id="0f01e-110">Argument nazwy zostały określone w `function.json`, i jest wstępnie zdefiniowanych nazw do uzyskiwania dostępu do czynności, takie jak hello tokenów funkcja rejestratora i anulowania.</span><span class="sxs-lookup"><span data-stu-id="0f01e-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="0f01e-111">W tym artykule przyjęto, że został już przeczytany hello [dokumentacja dla deweloperów usługi Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0f01e-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="how-fsx-works"></a><span data-ttu-id="0f01e-112">Jak działa fsx</span><span class="sxs-lookup"><span data-stu-id="0f01e-112">How .fsx works</span></span>
<span data-ttu-id="0f01e-113">`.fsx` Plik jest skryptu języka F #.</span><span class="sxs-lookup"><span data-stu-id="0f01e-113">An `.fsx` file is an F# script.</span></span> <span data-ttu-id="0f01e-114">Go można traktować jako projekt F #, który jest zawarty w jednym pliku.</span><span class="sxs-lookup"><span data-stu-id="0f01e-114">It can be thought of as an F# project that's contained in a single file.</span></span> <span data-ttu-id="0f01e-115">Witaj plik zawiera zarówno kod hello programu (w tym przypadku funkcji Azure) i wytyczne dotyczące zarządzania zależności.</span><span class="sxs-lookup"><span data-stu-id="0f01e-115">hello file contains both hello code for your program (in this case, your Azure Function) and directives for managing dependencies.</span></span>

<span data-ttu-id="0f01e-116">Jeśli używasz `.fsx` dla funkcji platformy Azure, zwykle wymagane zestawy są automatycznie dołączane dla Ciebie, umożliwiając toofocus na kod funkcji, a nie "standardowy" hello.</span><span class="sxs-lookup"><span data-stu-id="0f01e-116">When you use an `.fsx` for an Azure Function, commonly required assemblies are automatically included for you, allowing you toofocus on hello function rather than "boilerplate" code.</span></span>

## <a name="binding-tooarguments"></a><span data-ttu-id="0f01e-117">Powiązanie tooarguments</span><span class="sxs-lookup"><span data-stu-id="0f01e-117">Binding tooarguments</span></span>
<span data-ttu-id="0f01e-118">Każdego powiązania obsługuje niektóre zestaw argumentów, jako hello szczegółowe w [dokumentacja dla deweloperów usługi Azure Functions wyzwalaczy i powiązań](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="0f01e-118">Each binding supports some set of arguments, as detailed in hello [Azure Functions triggers and bindings developer reference](functions-triggers-bindings.md).</span></span> <span data-ttu-id="0f01e-119">Na przykład jednym z powiązań argument hello obsługuje wyzwalacza obiektu blob jest POCO, które można wyrazić przy użyciu rekordu języka F #.</span><span class="sxs-lookup"><span data-stu-id="0f01e-119">For example, one of hello argument bindings a blob trigger supports is a POCO, which can be expressed using an F# record.</span></span> <span data-ttu-id="0f01e-120">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f01e-120">For example:</span></span>

```fsharp
type Item = { Id: string }

let Run(blob: string, output: byref<Item>) =
    let item = { Id = "Some ID" }
    output <- item
```

<span data-ttu-id="0f01e-121">Funkcja Azure F # potrwa co najmniej jeden argument.</span><span class="sxs-lookup"><span data-stu-id="0f01e-121">Your F# Azure Function will take one or more arguments.</span></span> <span data-ttu-id="0f01e-122">Przy omawianiu usługi Azure Functions argumenty określane za*wejściowych* argumentów i *dane wyjściowe* argumentów.</span><span class="sxs-lookup"><span data-stu-id="0f01e-122">When we talk about Azure Functions arguments, we refer too*input* arguments and *output* arguments.</span></span> <span data-ttu-id="0f01e-123">Argument wejściowy jest dokładnie wydaje takich jak: dane wejściowe tooyour funkcji platformy Azure F #.</span><span class="sxs-lookup"><span data-stu-id="0f01e-123">An input argument is exactly what it sounds like: input tooyour F# Azure Function.</span></span> <span data-ttu-id="0f01e-124">*Dane wyjściowe* argument jest modyfikowalna danych lub `byref<>` argumentu, który służy jako Wstecz danych toopass sposób *limit* funkcji.</span><span class="sxs-lookup"><span data-stu-id="0f01e-124">An *output* argument is mutable data or a `byref<>` argument that serves as a way toopass data back *out* of your function.</span></span>

<span data-ttu-id="0f01e-125">W powyższym przykładzie hello `blob` jest argument wejściowy i `output` jest argumentem danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="0f01e-125">In hello example above, `blob` is an input argument, and `output` is an output argument.</span></span> <span data-ttu-id="0f01e-126">Należy zauważyć, że użyliśmy `byref<>` dla `output` (nie konieczności tooadd hello nie istnieje `[<Out>]` adnotacji).</span><span class="sxs-lookup"><span data-stu-id="0f01e-126">Notice that we used `byref<>` for `output` (there's no need tooadd hello `[<Out>]` annotation).</span></span> <span data-ttu-id="0f01e-127">Przy użyciu `byref<>` typ umożliwia Twojej toochange funkcji, który argument hello rekordu lub obiekt odwołuje się do.</span><span class="sxs-lookup"><span data-stu-id="0f01e-127">Using a `byref<>` type allows your function toochange which record or object hello argument refers to.</span></span>

<span data-ttu-id="0f01e-128">Gdy rekordu języka F # jest używany jako typ danych wejściowych, muszą być oznaczone definicji rekordów hello `[<CLIMutable>]` w celu tooallow hello Azure Functions framework tooset pola hello odpowiednio przed przekazaniem hello rekordów tooyour funkcji.</span><span class="sxs-lookup"><span data-stu-id="0f01e-128">When an F# record is used as an input type, hello record definition must be marked with `[<CLIMutable>]` in order tooallow hello Azure Functions framework tooset hello fields appropriately before passing hello record tooyour function.</span></span> <span data-ttu-id="0f01e-129">Pod maską hello `[<CLIMutable>]` generuje metody ustawiające właściwości rekordu hello.</span><span class="sxs-lookup"><span data-stu-id="0f01e-129">Under hello hood, `[<CLIMutable>]` generates setters for hello record properties.</span></span> <span data-ttu-id="0f01e-130">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f01e-130">For example:</span></span>

```fsharp
[<CLIMutable>]
type TestObject =
    { SenderName : string
      Greeting : string }

let Run(req: TestObject, log: TraceWriter) =
    { req with Greeting = sprintf "Hello, %s" req.SenderName }
```

<span data-ttu-id="0f01e-131">Można także klasy F # dla wejściowe i wyjściowe argumentów.</span><span class="sxs-lookup"><span data-stu-id="0f01e-131">An F# class can also be used for both in and out arguments.</span></span> <span data-ttu-id="0f01e-132">Dla klasy właściwości należy zwykle ustawiających i pobierających.</span><span class="sxs-lookup"><span data-stu-id="0f01e-132">For a class, properties will usually need getters and setters.</span></span> <span data-ttu-id="0f01e-133">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f01e-133">For example:</span></span>

```fsharp
type Item() =
    member val Id = "" with get,set
    member val Text = "" with get,set

let Run(input: string, item: byref<Item>) =
    let result = Item(Id = input, Text = "Hello from F#!")
    item <- result
```

## <a name="logging"></a><span data-ttu-id="0f01e-134">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="0f01e-134">Logging</span></span>
<span data-ttu-id="0f01e-135">toolog output tooyour [Podgląd dzienników przesyłanych strumieniowo](../app-service-web/web-sites-streaming-logs-and-console.md) w języku F #, funkcja powinno zająć argumentu typu `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="0f01e-135">toolog output tooyour [streaming logs](../app-service-web/web-sites-streaming-logs-and-console.md) in F#, your function should take an argument of type `TraceWriter`.</span></span> <span data-ttu-id="0f01e-136">W celu zachowania spójności, firma Microsoft zaleca, nosi nazwę tego argumentu `log`.</span><span class="sxs-lookup"><span data-stu-id="0f01e-136">For consistency, we recommend this argument is named `log`.</span></span> <span data-ttu-id="0f01e-137">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f01e-137">For example:</span></span>

```fsharp
let Run(blob: string, output: byref<string>, log: TraceWriter) =
    log.Verbose(sprintf "F# Azure Function processed a blob: %s" blob)
    output <- input
```

## <a name="async"></a><span data-ttu-id="0f01e-138">Asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="0f01e-138">Async</span></span>
<span data-ttu-id="0f01e-139">Witaj `async` przepływ pracy może być używany, ale wynik hello wymagane tooreturn `Task`.</span><span class="sxs-lookup"><span data-stu-id="0f01e-139">hello `async` workflow can be used, but hello result needs tooreturn a `Task`.</span></span> <span data-ttu-id="0f01e-140">Można to zrobić z `Async.StartAsTask`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f01e-140">This can be done with `Async.StartAsTask`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage) =
    async {
        return new HttpResponseMessage(HttpStatusCode.OK)
    } |> Async.StartAsTask
```

## <a name="cancellation-token"></a><span data-ttu-id="0f01e-141">Token anulowania</span><span class="sxs-lookup"><span data-stu-id="0f01e-141">Cancellation Token</span></span>
<span data-ttu-id="0f01e-142">Jeśli funkcja wymaga zamknięcia toohandle bezpiecznie, można nadać [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argumentu.</span><span class="sxs-lookup"><span data-stu-id="0f01e-142">If your function needs toohandle shutdown gracefully, you can give it a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) argument.</span></span> <span data-ttu-id="0f01e-143">Może to być łączone z `async`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f01e-143">This can be combined with `async`, for example:</span></span>

```fsharp
let Run(req: HttpRequestMessage, token: CancellationToken)
    let f = async {
        do! Async.Sleep(10)
        return new HttpResponseMessage(HttpStatusCode.OK)
    }
    Async.StartAsTask(f, token)
```

## <a name="importing-namespaces"></a><span data-ttu-id="0f01e-144">Importowanie przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="0f01e-144">Importing namespaces</span></span>
<span data-ttu-id="0f01e-145">Przestrzenie nazw mogą być otwierane w hello zwykły sposób:</span><span class="sxs-lookup"><span data-stu-id="0f01e-145">Namespaces can be opened in hello usual way:</span></span>

```fsharp
open System.Net
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="0f01e-146">Witaj następujące przestrzenie nazw są automatycznie otwierane:</span><span class="sxs-lookup"><span data-stu-id="0f01e-146">hello following namespaces are automatically opened:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* <span data-ttu-id="0f01e-147">`Microsoft.Azure.WebJobs.Host`.</span><span class="sxs-lookup"><span data-stu-id="0f01e-147">`Microsoft.Azure.WebJobs.Host`.</span></span>

## <a name="referencing-external-assemblies"></a><span data-ttu-id="0f01e-148">Zewnętrzne zestawy odwołujące</span><span class="sxs-lookup"><span data-stu-id="0f01e-148">Referencing External Assemblies</span></span>
<span data-ttu-id="0f01e-149">Podobnie, zestawu struktury odwołania do dodania z hello `#r "AssemblyName"` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="0f01e-149">Similarly, framework assembly references be added with hello `#r "AssemblyName"` directive.</span></span>

```fsharp
#r "System.Web.Http"

open System.Net
open System.Net.Http
open System.Threading.Tasks

let Run(req: HttpRequestMessage, log: TraceWriter) =
    ...
```

<span data-ttu-id="0f01e-150">Witaj następujące zestawy są automatycznie dodawane hello Azure Functions Środowisko hostingu:</span><span class="sxs-lookup"><span data-stu-id="0f01e-150">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* <span data-ttu-id="0f01e-151">`mscorlib`,</span><span class="sxs-lookup"><span data-stu-id="0f01e-151">`mscorlib`,</span></span>
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* <span data-ttu-id="0f01e-152">`System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="0f01e-152">`System.Net.Http.Formatting`.</span></span>

<span data-ttu-id="0f01e-153">Ponadto hello następujące zestawy są specjalne z uwzględnieniem wielkości liter i odwołuje simplename (np. `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="0f01e-153">In addition, hello following assemblies are special cased and may be referenced by simplename (e.g. `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* <span data-ttu-id="0f01e-154">`Microsoft.AspNEt.WebHooks.Common`.</span><span class="sxs-lookup"><span data-stu-id="0f01e-154">`Microsoft.AspNEt.WebHooks.Common`.</span></span>

<span data-ttu-id="0f01e-155">Jeśli potrzebujesz tooreference zestaw prywatny, możesz przekazać plik zestawu hello do `bin` folderu względna tooyour funkcji i odwołanie hello go przy użyciu nazwy pliku (np.  `#r "MyAssembly.dll"`).</span><span class="sxs-lookup"><span data-stu-id="0f01e-155">If you need tooreference a private assembly, you can upload hello assembly file into a `bin` folder relative tooyour function and reference it by using hello file name (e.g.  `#r "MyAssembly.dll"`).</span></span> <span data-ttu-id="0f01e-156">Dla informacji na temat sposobu tooupload folder funkcja tooyour plików Zobacz hello następujących sekcji, pakiet zarządzania.</span><span class="sxs-lookup"><span data-stu-id="0f01e-156">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

## <a name="editor-prelude"></a><span data-ttu-id="0f01e-157">Edytor Prelude</span><span class="sxs-lookup"><span data-stu-id="0f01e-157">Editor Prelude</span></span>
<span data-ttu-id="0f01e-158">Edytor, który obsługuje usługi kompilatora F # nie będą świadomi hello obszary nazw i zestawy, które automatycznie uwzględnia usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0f01e-158">An editor that supports F# Compiler Services will not be aware of hello namespaces and assemblies that Azure Functions automatically includes.</span></span> <span data-ttu-id="0f01e-159">Tak może być przydatne tooinclude prelude, pomocne w edytorze hello odnaleźć zestawów hello, którego używasz, i tooexplicitly otworzyć przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="0f01e-159">As such, it can be useful tooinclude a prelude that helps hello editor find hello assemblies you are using, and tooexplicitly open namespaces.</span></span> <span data-ttu-id="0f01e-160">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f01e-160">For example:</span></span>

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

<span data-ttu-id="0f01e-161">Azure Functions wykonuje kodu, przetwarza hello źródło o `COMPILED` zdefiniowane, więc prelude Edytor hello zostaną zignorowane.</span><span class="sxs-lookup"><span data-stu-id="0f01e-161">When Azure Functions executes your code, it processes hello source with `COMPILED` defined, so hello editor prelude will be ignored.</span></span>

<a name="package"></a>

## <a name="package-management"></a><span data-ttu-id="0f01e-162">Pakiet zarządzania</span><span class="sxs-lookup"><span data-stu-id="0f01e-162">Package management</span></span>
<span data-ttu-id="0f01e-163">Dodawanie pakietów NuGet toouse w F # funkcji `project.json` toohello hello funkcja folder pliku w systemie plików hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0f01e-163">toouse NuGet packages in an F# function, add a `project.json` file toohello hello function's folder in hello function app's file system.</span></span> <span data-ttu-id="0f01e-164">Oto przykład `project.json` pliku, który dodaje odwołanie do pakietu NuGet zbyt`Microsoft.ProjectOxford.Face` wersji 1.1.0:</span><span class="sxs-lookup"><span data-stu-id="0f01e-164">Here is an example `project.json` file that adds a NuGet package reference too`Microsoft.ProjectOxford.Face` version 1.1.0:</span></span>

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

<span data-ttu-id="0f01e-165">Witaj .NET Framework 4.6 jest obsługiwana tylko, upewnij się, że Twoje `project.json` Określa plik `net46` w sposób pokazany poniżej.</span><span class="sxs-lookup"><span data-stu-id="0f01e-165">Only hello .NET Framework 4.6 is supported, so make sure that your `project.json` file specifies `net46` as shown here.</span></span>

<span data-ttu-id="0f01e-166">Po przekazaniu `project.json` plików, hello środowiska uruchomieniowego pobiera pakiety hello i automatycznie dodaje odwołania toohello pakiet zestawów.</span><span class="sxs-lookup"><span data-stu-id="0f01e-166">When you upload a `project.json` file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="0f01e-167">Nie ma potrzeby tooadd `#r "AssemblyName"` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="0f01e-167">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="0f01e-168">Po prostu Dodaj wymagane hello `open` tooyour instrukcje `.fsx` pliku.</span><span class="sxs-lookup"><span data-stu-id="0f01e-168">Just add hello required `open` statements tooyour `.fsx` file.</span></span>

<span data-ttu-id="0f01e-169">Warto zapoznać się, że tooput automatycznie odwołuje się do zestawów w Twojej prelude edytora, tooimprove w edytorze interakcji z F # kompilacji usługi.</span><span class="sxs-lookup"><span data-stu-id="0f01e-169">You may wish tooput automatically references assemblies in your editor prelude, tooimprove your editor's interaction with F# Compile Services.</span></span>

### <a name="how-tooadd-a-projectjson-file-tooyour-azure-function"></a><span data-ttu-id="0f01e-170">Jak tooadd `project.json` pliku tooyour funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0f01e-170">How tooadd a `project.json` file tooyour Azure Function</span></span>
1. <span data-ttu-id="0f01e-171">Rozpocznij od upewnić się, że funkcja aplikacji jest uruchomiony, co można zrobić, otwierając funkcji w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0f01e-171">Begin by making sure your function app is running, which you can do by opening your function in hello Azure portal.</span></span> <span data-ttu-id="0f01e-172">Zapewnia to również dostęp do dzienników przesyłania strumieniowego toohello gdzie zostaną wyświetlone dane wyjściowe instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="0f01e-172">This also gives access toohello streaming logs where package installation output will be displayed.</span></span>
2. <span data-ttu-id="0f01e-173">tooupload `project.json` plików, użyj jednej z metod hello opisanych w [jak tooupdate funkcji pliki aplikacji](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="0f01e-173">tooupload a `project.json` file, use one of hello methods described in [how tooupdate function app files](functions-reference.md#fileupdate).</span></span> <span data-ttu-id="0f01e-174">Jeśli używasz [ciągłego wdrażania usługi Azure Functions](functions-continuous-deployment.md), możesz dodać `project.json` pliku tooyour przemieszczania gałąź w kolejności tooexperiment z nim przed dodaniem go tooyour wdrożenia gałęzi.</span><span class="sxs-lookup"><span data-stu-id="0f01e-174">If you are using [Continuous Deployment for Azure Functions](functions-continuous-deployment.md), you can add a `project.json` file tooyour staging branch in order tooexperiment with it before adding it tooyour deployment branch.</span></span>
3. <span data-ttu-id="0f01e-175">Po hello `project.json` zostanie dodany plik, zostanie wyświetlone dane wyjściowe toohello podobnie poniższy przykład w funkcji do przesyłania strumieniowego dziennika:</span><span class="sxs-lookup"><span data-stu-id="0f01e-175">After hello `project.json` file is added, you will see output similar toohello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="0f01e-176">Zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="0f01e-176">Environment variables</span></span>
<span data-ttu-id="0f01e-177">tooget zmienną środowiskową lub wartość ustawienia aplikacji, użyj `System.Environment.GetEnvironmentVariable`, na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f01e-177">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, for example:</span></span>

```fsharp
open System.Environment

let Run(timer: TimerInfo, log: TraceWriter) =
    log.Info("Storage = " + GetEnvironmentVariable("AzureWebJobsStorage"))
    log.Info("Site = " + GetEnvironmentVariable("WEBSITE_SITE_NAME"))
```

## <a name="reusing-fsx-code"></a><span data-ttu-id="0f01e-178">Ponowne wykorzystywanie kodu fsx</span><span class="sxs-lookup"><span data-stu-id="0f01e-178">Reusing .fsx code</span></span>
<span data-ttu-id="0f01e-179">Można użyć kodu z innych `.fsx` plików za pomocą `#load` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="0f01e-179">You can use code from other `.fsx` files by using a `#load` directive.</span></span> <span data-ttu-id="0f01e-180">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="0f01e-180">For example:</span></span>

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

<span data-ttu-id="0f01e-181">Ścieżki zapewnia toohello `#load` dyrektywy są lokalizacji względnej toohello Twojego `.fsx` pliku.</span><span class="sxs-lookup"><span data-stu-id="0f01e-181">Paths provides toohello `#load` directive are relative toohello location of your `.fsx` file.</span></span>

* <span data-ttu-id="0f01e-182">`#load "logger.fsx"`ładuje plik znajdujący się w folderze funkcja hello.</span><span class="sxs-lookup"><span data-stu-id="0f01e-182">`#load "logger.fsx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="0f01e-183">`#load "package\logger.fsx"`ładuje plik znajduje się w hello `package` folderu w folderze funkcja hello.</span><span class="sxs-lookup"><span data-stu-id="0f01e-183">`#load "package\logger.fsx"` loads a file located in hello `package` folder in hello function folder.</span></span>
* <span data-ttu-id="0f01e-184">`#load "..\shared\mylogger.fsx"`ładuje plik znajduje się w hello `shared` folderu na powitania sam poziom jako folder funkcja hello, oznacza to, bezpośrednio pod `wwwroot`.</span><span class="sxs-lookup"><span data-stu-id="0f01e-184">`#load "..\shared\mylogger.fsx"` loads a file located in hello `shared` folder at hello same level as hello function folder, that is, directly under `wwwroot`.</span></span>

<span data-ttu-id="0f01e-185">Hello `#load` dyrektywy działa tylko z `.fsx` plików (F # skrypt), a nie z `.fs` plików.</span><span class="sxs-lookup"><span data-stu-id="0f01e-185">hello `#load` directive only works with `.fsx` (F# script) files, and not with `.fs` files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f01e-186">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0f01e-186">Next steps</span></span>
<span data-ttu-id="0f01e-187">Aby uzyskać więcej informacji zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="0f01e-187">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="0f01e-188">Przewodnik F #</span><span class="sxs-lookup"><span data-stu-id="0f01e-188">F# Guide</span></span>](/dotnet/articles/fsharp/index)
* [<span data-ttu-id="0f01e-189">Najlepsze rozwiązania dotyczące usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="0f01e-189">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="0f01e-190">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="0f01e-190">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="0f01e-191">Azure dokumentacja dla deweloperów funkcje C#</span><span class="sxs-lookup"><span data-stu-id="0f01e-191">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="0f01e-192">Dokumentacja dla deweloperów NodeJS funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0f01e-192">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="0f01e-193">Azure funkcje wyzwalaczy i powiązań</span><span class="sxs-lookup"><span data-stu-id="0f01e-193">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)
* [<span data-ttu-id="0f01e-194">Środowisko Azure Functions testowania</span><span class="sxs-lookup"><span data-stu-id="0f01e-194">Azure Functions testing</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="0f01e-195">Środowisko Azure Functions skalowania</span><span class="sxs-lookup"><span data-stu-id="0f01e-195">Azure Functions scaling</span></span>](functions-scale.md)

