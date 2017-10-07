---
title: "aaaAzure dokumentacja dla deweloperów funkcje skryptu C# | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu toodevelop usługi Azure Functions przy użyciu języka C#."
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "usługa Azure Functions, funkcje, przetwarzanie zdarzeń, elementy webhook, obliczanie dynamiczne, architektura bez serwera"
ms.assetid: f28cda01-15f3-4047-83f3-e89d5728301c
ms.service: functions
ms.devlang: dotnet
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/07/2017
ms.author: donnam
ms.openlocfilehash: 27a8f4eb77497a373ff4031539e2e930585e48e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="785ea-104">Azure funkcje skryptu developer odwołanie w C#</span><span class="sxs-lookup"><span data-stu-id="785ea-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="785ea-105">Skryptu C#</span><span class="sxs-lookup"><span data-stu-id="785ea-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="785ea-106">Skrypt F #</span><span class="sxs-lookup"><span data-stu-id="785ea-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="785ea-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="785ea-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="785ea-108">środowisko skryptu C# dla usługi Azure Functions Hello jest oparta na hello Azure WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="785ea-108">hello C# script experience for Azure Functions is based on hello Azure WebJobs SDK.</span></span> <span data-ttu-id="785ea-109">Przepływy danych w funkcji języka C# za pomocą argumenty metody.</span><span class="sxs-lookup"><span data-stu-id="785ea-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="785ea-110">Argument nazwy zostały określone w `function.json`, i jest wstępnie zdefiniowanych nazw do uzyskiwania dostępu do czynności, takie jak hello tokenów funkcja rejestratora i anulowania.</span><span class="sxs-lookup"><span data-stu-id="785ea-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like hello function logger and cancellation tokens.</span></span>

<span data-ttu-id="785ea-111">W tym artykule przyjęto, że został już przeczytany hello [dokumentacja dla deweloperów usługi Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="785ea-111">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="785ea-112">Aby uzyskać informacje o użyciu języka C# klasy biblioteki, zobacz [.NET przy użyciu biblioteki klas z usługi Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="785ea-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="785ea-113">Jak działa csx</span><span class="sxs-lookup"><span data-stu-id="785ea-113">How .csx works</span></span>
<span data-ttu-id="785ea-114">Witaj `.csx` format umożliwia toowrite mniej "standardowy" i skoncentrować się na temat pisania tylko C# funkcję.</span><span class="sxs-lookup"><span data-stu-id="785ea-114">hello `.csx` format allows you toowrite less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="785ea-115">Obejmują wszystkie odwołania do zestawów i przestrzeni nazw na początku hello pliku hello w zwykły sposób.</span><span class="sxs-lookup"><span data-stu-id="785ea-115">Include any assembly references and namespaces at hello beginning of hello file as usual.</span></span> <span data-ttu-id="785ea-116">Zamiast zawijania wszystkie elementy w przestrzeni nazw i klasy, wystarczy zdefiniować `Run` metody.</span><span class="sxs-lookup"><span data-stu-id="785ea-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="785ea-117">Jeśli potrzebujesz tooinclude wszystkie klasy, dla wystąpienia toodefine zwykły obiekty stary obiekt CLR (POCO), można dołączyć klasy wewnątrz hello tego samego pliku.</span><span class="sxs-lookup"><span data-stu-id="785ea-117">If you need tooinclude any classes, for instance toodefine Plain Old CLR Object (POCO) objects, you can include a class inside hello same file.</span></span>   

## <a name="binding-tooarguments"></a><span data-ttu-id="785ea-118">Powiązanie tooarguments</span><span class="sxs-lookup"><span data-stu-id="785ea-118">Binding tooarguments</span></span>
<span data-ttu-id="785ea-119">Witaj różnych powiązania są powiązane tooa C# funkcja za pośrednictwem hello `name` właściwości w hello *function.json* konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="785ea-119">hello various bindings are bound tooa C# function via hello `name` property in hello *function.json* configuration.</span></span> <span data-ttu-id="785ea-120">Każdego powiązania ma własną obsługiwanych typów; na przykład wyzwalacza obiektu blob może obsługiwać ciąg, POCO lub CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="785ea-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="785ea-121">Witaj, obsługiwane typy są udokumentowane w hello odwołania dla każdego powiązania.</span><span class="sxs-lookup"><span data-stu-id="785ea-121">hello supported types are documented in hello reference for each binding.</span></span> <span data-ttu-id="785ea-122">Obiekt POCO musi mieć określonej metody pobierającej i ustawiającej zdefiniowane dla każdej właściwości.</span><span class="sxs-lookup"><span data-stu-id="785ea-122">A POCO object must have a getter and setter defined for each property.</span></span>

```csharp
public static void Run(string myBlob, out MyClass myQueueItem)
{
    log.Verbose($"C# Blob trigger function processed: {myBlob}");
    myQueueItem = new MyClass() { Id = "myid" };
}

public class MyClass
{
    public string Id { get; set; }
}
```

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="785ea-123">Dla powiązania danych wyjściowych przy użyciu wartości zwracanej — metoda</span><span class="sxs-lookup"><span data-stu-id="785ea-123">Using method return value for output binding</span></span>

<span data-ttu-id="785ea-124">Można użyć wartość zwracaną metody dla powiązania danych wyjściowych przy użyciu nazwy hello `$return` w *function.json*:</span><span class="sxs-lookup"><span data-stu-id="785ea-124">You can use a method return value for an output binding, by using hello name `$return` in *function.json*:</span></span>

```json
{
    "type": "queue",
    "direction": "out",
    "name": "$return",
    "queueName": "outqueue",
    "connection": "MyStorageConnectionString",
}
```

```csharp
public static string Run(string input, TraceWriter log)
{
    return input;
}
```

## <a name="writing-multiple-output-values"></a><span data-ttu-id="785ea-125">Trwa zapisywanie wielu wartości danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="785ea-125">Writing multiple output values</span></span>

<span data-ttu-id="785ea-126">Powiązanie output wiele wartości tooan toowrite, użyj hello [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) lub [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) typów.</span><span class="sxs-lookup"><span data-stu-id="785ea-126">toowrite multiple values tooan output binding, use hello [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="785ea-127">Te typy są tylko do zapisu kolekcje, które są napisane toohello powiązanie dane wyjściowe po zakończeniu metody hello.</span><span class="sxs-lookup"><span data-stu-id="785ea-127">These types are write-only collections that are written toohello output binding when hello method completes.</span></span>

<span data-ttu-id="785ea-128">W tym przykładzie zapisuje wiele wiadomości w kolejce za pomocą `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="785ea-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="785ea-129">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="785ea-129">Logging</span></span>
<span data-ttu-id="785ea-130">toolog output tooyour dzienniki przesyłania strumieniowego w języku C#, obejmują argumentu typu `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="785ea-130">toolog output tooyour streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="785ea-131">Zaleca się jej nazwa `log`.</span><span class="sxs-lookup"><span data-stu-id="785ea-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="785ea-132">Unikaj używania `Console.Write` w funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="785ea-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="785ea-133">`TraceWriter`jest zdefiniowany w hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="785ea-133">`TraceWriter` is defined in hello [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="785ea-134">Witaj poziom dziennika `TraceWriter` można skonfigurować w [hosta\.json].</span><span class="sxs-lookup"><span data-stu-id="785ea-134">hello log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="785ea-135">Asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="785ea-135">Async</span></span>
<span data-ttu-id="785ea-136">toomake funkcję asynchroniczną, użyj hello `async` — słowo kluczowe i przywracać `Task` obiektu.</span><span class="sxs-lookup"><span data-stu-id="785ea-136">toomake a function asynchronous, use hello `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="785ea-137">Token anulowania</span><span class="sxs-lookup"><span data-stu-id="785ea-137">Cancellation Token</span></span>
<span data-ttu-id="785ea-138">Niektóre operacje wymagają łagodne zamykanie.</span><span class="sxs-lookup"><span data-stu-id="785ea-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="785ea-139">Mimo że zawsze jest najlepsze kodu toowrite, który może obsługiwać awarii w przypadkach, w którym ma toohandle łagodne zamykanie żądania, należy zdefiniować [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typu argumentu.</span><span class="sxs-lookup"><span data-stu-id="785ea-139">While it's always best toowrite code that can handle crashing,  in cases where you want toohandle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="785ea-140">A `CancellationToken` podano toosignal wyzwoleniu zamknięcie hosta.</span><span class="sxs-lookup"><span data-stu-id="785ea-140">A `CancellationToken` is provided toosignal that a host shutdown is triggered.</span></span>

```csharp
public async static Task ProcessQueueMessageAsyncCancellationToken(
        string blobName,
        Stream blobInput,
        Stream blobOutput,
        CancellationToken token)
    {
        await blobInput.CopyToAsync(blobOutput, 4096, token);
    }
```

## <a name="importing-namespaces"></a><span data-ttu-id="785ea-141">Importowanie przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="785ea-141">Importing namespaces</span></span>
<span data-ttu-id="785ea-142">Jeśli potrzebujesz tooimport przestrzeni nazw, możesz to zrobić w zwykły sposób, z hello `using` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="785ea-142">If you need tooimport namespaces, you can do so as usual, with hello `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="785ea-143">Witaj następujących przestrzeni nazw są automatycznie importowane i w związku z tym są opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="785ea-143">hello following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="785ea-144">Zewnętrzne zestawy odwołujące</span><span class="sxs-lookup"><span data-stu-id="785ea-144">Referencing External Assemblies</span></span>
<span data-ttu-id="785ea-145">Dla zestawów struktury, dodaj odwołania przy użyciu hello `#r "AssemblyName"` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="785ea-145">For framework assemblies, add references by using hello `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="785ea-146">Witaj następujące zestawy są automatycznie dodawane hello Azure Functions Środowisko hostingu:</span><span class="sxs-lookup"><span data-stu-id="785ea-146">hello following assemblies are automatically added by hello Azure Functions hosting environment:</span></span>

* `mscorlib`
* `System`
* `System.Core`
* `System.Xml`
* `System.Net.Http`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`
* `Microsoft.Azure.WebJobs.Extensions`
* `System.Web.Http`
* `System.Net.Http.Formatting`

<span data-ttu-id="785ea-147">Witaj następujące zestawy mogą odwoływać się prostą nazwę (na przykład `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="785ea-147">hello following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="785ea-148">Odwołania do zestawów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="785ea-148">Referencing custom assemblies</span></span>

<span data-ttu-id="785ea-149">tooreference niestandardowego zestawu, możesz użyć dowolnej *udostępnionego* zestawu lub *prywatnej* zestawu:</span><span class="sxs-lookup"><span data-stu-id="785ea-149">tooreference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="785ea-150">Zestawy udostępnione są współużytkowane przez wszystkie funkcje w aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="785ea-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="785ea-151">tooreference niestandardowego zestawu, Przekaż hello zestawu tooyour funkcji aplikacji, takich jak w `bin` folder w katalogu głównym aplikacji funkcja hello.</span><span class="sxs-lookup"><span data-stu-id="785ea-151">tooreference a custom assembly, upload hello assembly tooyour function app, such as in a `bin` folder in hello function app root.</span></span> 
- <span data-ttu-id="785ea-152">Zestawy prywatne są częścią kontekstu daną funkcję i obsługuje ładowania bezpośredniego w różnych wersjach.</span><span class="sxs-lookup"><span data-stu-id="785ea-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="785ea-153">Zestawy prywatne należy przekazać w `bin` folderu w katalogu funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="785ea-153">Private assemblies should be uploaded in a `bin` folder in hello function directory.</span></span> <span data-ttu-id="785ea-154">Odwołanie przy użyciu nazwy pliku hello, takich jak `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="785ea-154">Reference using hello file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="785ea-155">Dla informacji na temat sposobu tooupload folder funkcja tooyour plików Zobacz hello następujących sekcji, pakiet zarządzania.</span><span class="sxs-lookup"><span data-stu-id="785ea-155">For information on how tooupload files tooyour function folder, see hello following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="785ea-156">Monitorowane katalogów</span><span class="sxs-lookup"><span data-stu-id="785ea-156">Watched directories</span></span>

<span data-ttu-id="785ea-157">Witaj katalog, który zawiera plik skryptu funkcji hello automatycznie jest monitorowana dla tooassemblies zmiany.</span><span class="sxs-lookup"><span data-stu-id="785ea-157">hello directory that contains hello function script file is automatically watched for changes tooassemblies.</span></span> <span data-ttu-id="785ea-158">toowatch zestawu zmian w innych katalogów, dodaj je toohello `watchDirectories` na liście [hosta\.json].</span><span class="sxs-lookup"><span data-stu-id="785ea-158">toowatch for assembly changes in other directories, add them toohello `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="785ea-159">Za pomocą pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="785ea-159">Using NuGet packages</span></span>
<span data-ttu-id="785ea-160">Przekaż toouse pakietów NuGet w języku C# funkcję, *project.json* toohello funkcja folder pliku w systemie plików hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="785ea-160">toouse NuGet packages in a C# function, upload a *project.json* file toohello function's folder in hello function app's file system.</span></span> <span data-ttu-id="785ea-161">Oto przykład *project.json* pliku, który dodaje 1.1.0 odwołania tooMicrosoft.ProjectOxford.Face wersji:</span><span class="sxs-lookup"><span data-stu-id="785ea-161">Here is an example *project.json* file that adds a reference tooMicrosoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="785ea-162">Witaj .NET Framework 4.6 jest obsługiwana tylko, upewnij się, że Twoje *project.json* Określa plik `net46` w sposób pokazany poniżej.</span><span class="sxs-lookup"><span data-stu-id="785ea-162">Only hello .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="785ea-163">Po przekazaniu *project.json* plików, hello środowiska uruchomieniowego pobiera pakiety hello i automatycznie dodaje odwołania toohello pakiet zestawów.</span><span class="sxs-lookup"><span data-stu-id="785ea-163">When you upload a *project.json* file, hello runtime gets hello packages and automatically adds references toohello package assemblies.</span></span> <span data-ttu-id="785ea-164">Nie ma potrzeby tooadd `#r "AssemblyName"` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="785ea-164">You don't need tooadd `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="785ea-165">toouse hello typów zdefiniowanych w pakietach NuGet hello, Dodaj wymagane hello `using` tooyour instrukcje *run.csx* pliku</span><span class="sxs-lookup"><span data-stu-id="785ea-165">toouse hello types defined in hello NuGet packages, add hello required `using` statements tooyour *run.csx* file</span></span> 

<span data-ttu-id="785ea-166">W środowisku uruchomieniowym funkcje hello, przywracanie NuGet działa na podstawie porównania ilości `project.json` i `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="785ea-166">In hello Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="785ea-167">Jeśli hello Data i godzina sygnatur plików hello **nie** uruchamia Przywracanie NuGet dopasowania i pliki do pobrania NuGet zaktualizowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="785ea-167">If hello date and time stamps of hello files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="785ea-168">Jednakże, jeżeli hello Data i godzina sygnatur plików hello **czy** dopasowania, NuGet nie wykonuje operację przywracania.</span><span class="sxs-lookup"><span data-stu-id="785ea-168">However, if hello date and time stamps of hello files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="785ea-169">W związku z tym `project.lock.json` nie powinny zostać wdrożone, ponieważ powoduje ona przywracanie pakietu NuGet tooskip.</span><span class="sxs-lookup"><span data-stu-id="785ea-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet tooskip package restore.</span></span> <span data-ttu-id="785ea-170">Wdrażanie blokady hello tooavoid plików, dodawanie hello `project.lock.json` toohello `.gitignore` pliku.</span><span class="sxs-lookup"><span data-stu-id="785ea-170">tooavoid deploying hello lock file, add hello `project.lock.json` toohello `.gitignore` file.</span></span>

<span data-ttu-id="785ea-171">toouse niestandardowe źródło danych NuGet, określ hello źródła danych w *Nuget.Config* pliku w katalogu głównym aplikacji funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="785ea-171">toouse a custom NuGet feed, specify hello feed in a *Nuget.Config* file in hello Function App root.</span></span> <span data-ttu-id="785ea-172">Aby uzyskać więcej informacji, zobacz [NuGet Konfigurowanie zachowania](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="785ea-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="785ea-173">Przy użyciu pliku project.json</span><span class="sxs-lookup"><span data-stu-id="785ea-173">Using a project.json file</span></span>
1. <span data-ttu-id="785ea-174">Open — funkcja hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="785ea-174">Open hello function in hello Azure portal.</span></span> <span data-ttu-id="785ea-175">Hello rejestruje dane wyjściowe kartę Wyświetla hello pakietu instalacji.</span><span class="sxs-lookup"><span data-stu-id="785ea-175">hello logs tab displays hello package installation output.</span></span>
2. <span data-ttu-id="785ea-176">tooupload pliku project.json, użyj jednej z metod hello opisanych w hello [jak tooupdate funkcji pliki aplikacji](functions-reference.md#fileupdate) w temacie odwołania dla deweloperów usługi Azure Functions hello.</span><span class="sxs-lookup"><span data-stu-id="785ea-176">tooupload a project.json file, use one of hello methods described in hello [How tooupdate function app files](functions-reference.md#fileupdate) in hello Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="785ea-177">Po hello *project.json* przekazać pliku, wyświetlone dane wyjściowe podobne hello poniższy przykład w funkcji do przesyłania strumieniowego dzienników:</span><span class="sxs-lookup"><span data-stu-id="785ea-177">After hello *project.json* file is uploaded, you see output like hello following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="785ea-178">Zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="785ea-178">Environment variables</span></span>
<span data-ttu-id="785ea-179">tooget zmienną środowiskową lub wartość ustawienia aplikacji, użyj `System.Environment.GetEnvironmentVariable`, jak pokazano w hello poniższy przykład kodu:</span><span class="sxs-lookup"><span data-stu-id="785ea-179">tooget an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in hello following code example:</span></span>

```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}");
    log.Info(GetEnvironmentVariable("AzureWebJobsStorage"));
    log.Info(GetEnvironmentVariable("WEBSITE_SITE_NAME"));
}

public static string GetEnvironmentVariable(string name)
{
    return name + ": " +
        System.Environment.GetEnvironmentVariable(name, EnvironmentVariableTarget.Process);
}
```

## <a name="reusing-csx-code"></a><span data-ttu-id="785ea-180">Ponowne wykorzystywanie kodu csx</span><span class="sxs-lookup"><span data-stu-id="785ea-180">Reusing .csx code</span></span>
<span data-ttu-id="785ea-181">Można użyć klasy i metody zdefiniowane w innych *csx* pliki w Twojej *run.csx* pliku.</span><span class="sxs-lookup"><span data-stu-id="785ea-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="785ea-182">toodo używanego, `#load` dyrektywy w Twojej *run.csx* pliku.</span><span class="sxs-lookup"><span data-stu-id="785ea-182">toodo that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="785ea-183">W hello poniższy przykład, nazwę procedury rejestrowania `MyLogger` są udostępniane w *myLogger.csx* i ładowane do *run.csx* przy użyciu hello `#load` dyrektywy:</span><span class="sxs-lookup"><span data-stu-id="785ea-183">In hello following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using hello `#load` directive:</span></span>

<span data-ttu-id="785ea-184">Przykład *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="785ea-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="785ea-185">Przykład *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="785ea-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="785ea-186">Za pomocą udostępnionej *csx* wspólnego wzorca należy toostrongly wpisać argumentów pomiędzy funkcjami przy użyciu obiektu POCO.</span><span class="sxs-lookup"><span data-stu-id="785ea-186">Using a shared *.csx* is a common pattern when you want toostrongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="785ea-187">W hello poniższy przykład uproszczony, wyzwalacza HTTP i kolejki wyzwalacza udziału obiektu POCO o nazwie `Order` toostrongly typu hello kolejność danych:</span><span class="sxs-lookup"><span data-stu-id="785ea-187">In hello following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` toostrongly type hello order data:</span></span>

<span data-ttu-id="785ea-188">Przykład *run.csx* wyzwalacza HTTP:</span><span class="sxs-lookup"><span data-stu-id="785ea-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting tooprocessing queue.");

    if (req.orderId == null)
    {
        return new HttpResponseMessage(HttpStatusCode.BadRequest);
    }
    else
    {
        await outputQueueItem.AddAsync(req);
        return new HttpResponseMessage(HttpStatusCode.OK);
    }
}
```

<span data-ttu-id="785ea-189">Przykład *run.csx* wyzwalacza kolejki:</span><span class="sxs-lookup"><span data-stu-id="785ea-189">Example *run.csx* for queue trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System;

public static void Run(Order myQueueItem, out Order outputQueueItem,TraceWriter log)
{
    log.Info($"C# Queue trigger function processed order...");
    log.Info(myQueueItem.ToString());

    outputQueueItem = myQueueItem;
}
```

<span data-ttu-id="785ea-190">Przykład *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="785ea-190">Example *order.csx*:</span></span>

```cs
public class Order
{
    public string orderId {get; set; }
    public string custName {get; set;}
    public string custAddress {get; set;}
    public string custEmail {get; set;}
    public string cartId {get; set; }

    public override String ToString()
    {
        return "\n{\n\torderId : " + orderId +
                  "\n\tcustName : " + custName +             
                  "\n\tcustAddress : " + custAddress +             
                  "\n\tcustEmail : " + custEmail +             
                  "\n\tcartId : " + cartId + "\n}";             
    }
}
```

<span data-ttu-id="785ea-191">Można użyć ścieżki względnej z hello `#load` dyrektywy:</span><span class="sxs-lookup"><span data-stu-id="785ea-191">You can use a relative path with hello `#load` directive:</span></span>

* <span data-ttu-id="785ea-192">`#load "mylogger.csx"`ładuje plik znajdujący się w folderze funkcja hello.</span><span class="sxs-lookup"><span data-stu-id="785ea-192">`#load "mylogger.csx"` loads a file located in hello function folder.</span></span>
* <span data-ttu-id="785ea-193">`#load "loadedfiles\mylogger.csx"`ładuje plik znajdujący się w folderze w folderze funkcja hello.</span><span class="sxs-lookup"><span data-stu-id="785ea-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in hello function folder.</span></span>
* <span data-ttu-id="785ea-194">`#load "..\shared\mylogger.csx"`ładuje plik znajdujący się w folderze na powitania sam poziom jako folder funkcja hello, oznacza to, bezpośrednio pod *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="785ea-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at hello same level as hello function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="785ea-195">Witaj `#load` dyrektywy działa tylko w przypadku *csx* plików (C# skrypt), nie z *.cs* plików.</span><span class="sxs-lookup"><span data-stu-id="785ea-195">hello `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="785ea-196">Powiązanie w czasie wykonywania za pośrednictwem powiązania imperatywne</span><span class="sxs-lookup"><span data-stu-id="785ea-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="785ea-197">W języku C# i innych języków .NET, można użyć [imperatywnych](https://en.wikipedia.org/wiki/Imperative_programming) wzorca wiązania jako min. toohello [ *deklaratywne* ](https://en.wikipedia.org/wiki/Declarative_programming) powiązania w *function.json*.</span><span class="sxs-lookup"><span data-stu-id="785ea-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed toohello [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="785ea-198">Powiązanie konieczne jest przydatne, gdy Parametry wiążące muszą toobe obliczane w czasie środowiska uruchomieniowego zamiast projektu.</span><span class="sxs-lookup"><span data-stu-id="785ea-198">Imperative binding is useful when binding parameters need toobe computed at runtime rather than design time.</span></span> <span data-ttu-id="785ea-199">Z tego wzorca można powiązać toosupported danych wejściowych i wyjściowych powiązania na bieżąco w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="785ea-199">With this pattern, you can bind toosupported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="785ea-200">Zdefiniuj staje się niezbędna powiązania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="785ea-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="785ea-201">**Nie** obejmują wpis w *function.json* dla żądanego imperatywnych powiązania.</span><span class="sxs-lookup"><span data-stu-id="785ea-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="785ea-202">Przekaż parametr wejściowy [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) lub [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="785ea-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="785ea-203">Użyj powitania po C# wzorzec tooperform hello wiązania z danymi.</span><span class="sxs-lookup"><span data-stu-id="785ea-203">Use hello following C# pattern tooperform hello data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="785ea-204">gdzie `BindingTypeAttribute` hello .NET atrybutu, który definiuje wiązania i `T` jest hello wejściowych lub wyjściowych typu, który jest obsługiwany przez ten typ powiązania.</span><span class="sxs-lookup"><span data-stu-id="785ea-204">where `BindingTypeAttribute` is hello .NET attribute that defines your binding and `T` is hello input or output type that's supported by that binding type.</span></span> <span data-ttu-id="785ea-205">`T`nie może być `out` typ parametru (takie jak `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="785ea-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="785ea-206">Na przykład, w tabeli Mobile Apps output powiązanie obsługuje [sześć output typy](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ale można używać tylko [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) lub [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) dla `T`.</span><span class="sxs-lookup"><span data-stu-id="785ea-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="785ea-207">Tworzy Hello następującego przykładowego kodu [powiązania wyjściowego obiektu blob magazynu](functions-bindings-storage-blob.md#using-a-blob-output-binding) z obiektu blob ścieżki, która jest zdefiniowana w czasie wykonywania, następnie zapisuje obiektu blob toohello ciągu.</span><span class="sxs-lookup"><span data-stu-id="785ea-207">hello following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string toohello blob.</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    using (var writer = await binder.BindAsync<TextWriter>(new BlobAttribute("samples-output/path")))
    {
        writer.Write("Hello World!!");
    }
}
```

<span data-ttu-id="785ea-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definiuje hello [obiektu blob magazynu](functions-bindings-storage-blob.md) wejściowych lub wyjściowych powiązanie, i [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) jest typ powiązania obsługiwanych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="785ea-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines hello [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="785ea-209">Jest dostępna, hello kod pobiera hello domyślnym ustawieniem aplikacji hello parametry połączenia konta magazynu (czyli `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="785ea-209">As is, hello code gets hello default app setting for hello Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="785ea-210">Toouse ustawienie niestandardowych aplikacji można określić, dodając [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) i przekazanie tablicy atrybutu hello do `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="785ea-210">You can specify a custom app setting toouse by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing hello attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="785ea-211">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="785ea-211">For example,</span></span>

```cs
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host.Bindings.Runtime;

public static async Task Run(string input, Binder binder)
{
    var attributes = new Attribute[]
    {    
        new BlobAttribute("samples-output/path"),
        new StorageAccountAttribute("MyStorageAccount")
    };

    using (var writer = await binder.BindAsync<TextWriter>(attributes))
    {
        writer.Write("Hello World!");
    }
}
```

<span data-ttu-id="785ea-212">Witaj poniższej tabeli wymieniono hello .NET atrybuty dla każdego powiązania typu hello pakietów i w których są zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="785ea-212">hello following table lists hello .NET attributes for each binding type and hello packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="785ea-213">Powiązanie</span><span class="sxs-lookup"><span data-stu-id="785ea-213">Binding</span></span> | <span data-ttu-id="785ea-214">Atrybut</span><span class="sxs-lookup"><span data-stu-id="785ea-214">Attribute</span></span> | <span data-ttu-id="785ea-215">Dodaj odwołanie</span><span class="sxs-lookup"><span data-stu-id="785ea-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="785ea-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="785ea-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="785ea-217">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="785ea-217">Event Hubs</span></span> | <span data-ttu-id="785ea-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="785ea-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="785ea-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="785ea-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="785ea-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="785ea-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="785ea-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="785ea-221">Service Bus</span></span> | <span data-ttu-id="785ea-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="785ea-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="785ea-223">Kolejki magazynu</span><span class="sxs-lookup"><span data-stu-id="785ea-223">Storage queue</span></span> | <span data-ttu-id="785ea-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="785ea-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="785ea-225">Obiektu blob magazynu</span><span class="sxs-lookup"><span data-stu-id="785ea-225">Storage blob</span></span> | <span data-ttu-id="785ea-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="785ea-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="785ea-227">Tabela magazynu</span><span class="sxs-lookup"><span data-stu-id="785ea-227">Storage table</span></span> | <span data-ttu-id="785ea-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="785ea-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="785ea-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="785ea-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="785ea-230">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="785ea-230">Next steps</span></span>
<span data-ttu-id="785ea-231">Aby uzyskać więcej informacji zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="785ea-231">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="785ea-232">Najlepsze rozwiązania dotyczące usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="785ea-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="785ea-233">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="785ea-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="785ea-234">Azure dokumentacja dla deweloperów funkcje F #</span><span class="sxs-lookup"><span data-stu-id="785ea-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="785ea-235">Dokumentacja dla deweloperów NodeJS funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="785ea-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="785ea-236">Azure funkcje wyzwalaczy i powiązań</span><span class="sxs-lookup"><span data-stu-id="785ea-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
