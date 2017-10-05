---
title: "Dokumentacja dla deweloperów usługi Azure funkcje skryptu C# | Dokumentacja firmy Microsoft"
description: "Zrozumienie sposobu tworzenia usługi Azure Functions przy użyciu języka C#."
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
ms.openlocfilehash: 83a351ce0279ada8ce7fe0513497349471334a86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-c-script-developer-reference"></a><span data-ttu-id="989e4-104">Azure funkcje skryptu developer odwołanie w C#</span><span class="sxs-lookup"><span data-stu-id="989e4-104">Azure Functions C# script developer reference</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="989e4-105">Skryptu C#</span><span class="sxs-lookup"><span data-stu-id="989e4-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="989e4-106">Skrypt F #</span><span class="sxs-lookup"><span data-stu-id="989e4-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="989e4-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="989e4-107">Node.js</span></span>](functions-reference-node.md)
>
>

<span data-ttu-id="989e4-108">Środowisko skryptu C# dla usługi Azure Functions opiera się na zestaw SDK zadań Webjob Azure.</span><span class="sxs-lookup"><span data-stu-id="989e4-108">The C# script experience for Azure Functions is based on the Azure WebJobs SDK.</span></span> <span data-ttu-id="989e4-109">Przepływy danych w funkcji języka C# za pomocą argumenty metody.</span><span class="sxs-lookup"><span data-stu-id="989e4-109">Data flows into your C# function via method arguments.</span></span> <span data-ttu-id="989e4-110">Argument nazwy zostały określone w `function.json`, i jest wstępnie zdefiniowanych nazw do uzyskiwania dostępu do elementów, jak funkcja tokenów rejestratora i anulowania.</span><span class="sxs-lookup"><span data-stu-id="989e4-110">Argument names are specified in `function.json`, and there are predefined names for accessing things like the function logger and cancellation tokens.</span></span>

<span data-ttu-id="989e4-111">W tym artykule przyjęto założenie, że został już przeczytany [dokumentacja dla deweloperów usługi Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="989e4-111">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

<span data-ttu-id="989e4-112">Aby uzyskać informacje o użyciu języka C# klasy biblioteki, zobacz [.NET przy użyciu biblioteki klas z usługi Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="989e4-112">For information on using C# class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span>

## <a name="how-csx-works"></a><span data-ttu-id="989e4-113">Jak działa csx</span><span class="sxs-lookup"><span data-stu-id="989e4-113">How .csx works</span></span>
<span data-ttu-id="989e4-114">`.csx` Format umożliwia pisanie mniej "standardowy" i skoncentrować się na zapisywanie tylko C# funkcję.</span><span class="sxs-lookup"><span data-stu-id="989e4-114">The `.csx` format allows you to write less "boilerplate" and focus on writing just a C# function.</span></span> <span data-ttu-id="989e4-115">Jak zwykle obejmują wszelkie odwołania do zestawów i przestrzeni nazw na początku pliku.</span><span class="sxs-lookup"><span data-stu-id="989e4-115">Include any assembly references and namespaces at the beginning of the file as usual.</span></span> <span data-ttu-id="989e4-116">Zamiast zawijania wszystkie elementy w przestrzeni nazw i klasy, wystarczy zdefiniować `Run` metody.</span><span class="sxs-lookup"><span data-stu-id="989e4-116">Instead of wrapping everything in a namespace and class, just define a `Run` method.</span></span> <span data-ttu-id="989e4-117">Jeśli musisz obejmują wszystkie klasy, na przykład aby zdefiniować obiekty zwykłego obiektu CLR stary (POCO), można dołączyć klasy wewnątrz tego samego pliku.</span><span class="sxs-lookup"><span data-stu-id="989e4-117">If you need to include any classes, for instance to define Plain Old CLR Object (POCO) objects, you can include a class inside the same file.</span></span>   

## <a name="binding-to-arguments"></a><span data-ttu-id="989e4-118">Powiązanie z argumentów</span><span class="sxs-lookup"><span data-stu-id="989e4-118">Binding to arguments</span></span>
<span data-ttu-id="989e4-119">Różne powiązania są powiązane z funkcją języka C# za pomocą `name` właściwości w *function.json* konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="989e4-119">The various bindings are bound to a C# function via the `name` property in the *function.json* configuration.</span></span> <span data-ttu-id="989e4-120">Każdego powiązania ma własną obsługiwanych typów; na przykład wyzwalacza obiektu blob może obsługiwać ciąg, POCO lub CloudBlockBlob.</span><span class="sxs-lookup"><span data-stu-id="989e4-120">Each binding has its own supported types; for instance, a blob trigger can support a string, a POCO, or a CloudBlockBlob.</span></span> <span data-ttu-id="989e4-121">Obsługiwane typy są udokumentowane w odwołaniu dla każdego powiązania.</span><span class="sxs-lookup"><span data-stu-id="989e4-121">The supported types are documented in the reference for each binding.</span></span> <span data-ttu-id="989e4-122">Obiekt POCO musi mieć określonej metody pobierającej i ustawiającej zdefiniowane dla każdej właściwości.</span><span class="sxs-lookup"><span data-stu-id="989e4-122">A POCO object must have a getter and setter defined for each property.</span></span>

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

## <a name="using-method-return-value-for-output-binding"></a><span data-ttu-id="989e4-123">Dla powiązania danych wyjściowych przy użyciu wartości zwracanej — metoda</span><span class="sxs-lookup"><span data-stu-id="989e4-123">Using method return value for output binding</span></span>

<span data-ttu-id="989e4-124">Można użyć wartość zwracaną metody dla powiązania danych wyjściowych przy użyciu nazwy `$return` w *function.json*:</span><span class="sxs-lookup"><span data-stu-id="989e4-124">You can use a method return value for an output binding, by using the name `$return` in *function.json*:</span></span>

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

## <a name="writing-multiple-output-values"></a><span data-ttu-id="989e4-125">Trwa zapisywanie wielu wartości danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="989e4-125">Writing multiple output values</span></span>

<span data-ttu-id="989e4-126">Aby napisać wiele wartości do powiązania danych wyjściowych, użyj [ `ICollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) lub [ `IAsyncCollector` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) typów.</span><span class="sxs-lookup"><span data-stu-id="989e4-126">To write multiple values to an output binding, use the [`ICollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [`IAsyncCollector`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) types.</span></span> <span data-ttu-id="989e4-127">Te typy są kolekcji tylko do zapisu, które są zapisywane w powiązaniu danych wyjściowych, po zakończeniu metody.</span><span class="sxs-lookup"><span data-stu-id="989e4-127">These types are write-only collections that are written to the output binding when the method completes.</span></span>

<span data-ttu-id="989e4-128">W tym przykładzie zapisuje wiele wiadomości w kolejce za pomocą `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="989e4-128">This example writes multiple queue messages using `ICollector`:</span></span>

```csharp
public static void Run(ICollector<string> myQueueItem, TraceWriter log)
{
    myQueueItem.Add("Hello");
    myQueueItem.Add("World!");
}
```

## <a name="logging"></a><span data-ttu-id="989e4-129">Rejestrowanie</span><span class="sxs-lookup"><span data-stu-id="989e4-129">Logging</span></span>
<span data-ttu-id="989e4-130">Aby rejestrować dane wyjściowe do dzienników przesyłania strumieniowego w języku C#, obejmują argumentu typu `TraceWriter`.</span><span class="sxs-lookup"><span data-stu-id="989e4-130">To log output to your streaming logs in C#, include an argument of type `TraceWriter`.</span></span> <span data-ttu-id="989e4-131">Zaleca się jej nazwa `log`.</span><span class="sxs-lookup"><span data-stu-id="989e4-131">We recommend that you name it `log`.</span></span> <span data-ttu-id="989e4-132">Unikaj używania `Console.Write` w funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="989e4-132">Avoid using `Console.Write` in Azure Functions.</span></span> 

<span data-ttu-id="989e4-133">`TraceWriter`jest zdefiniowany w [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span><span class="sxs-lookup"><span data-stu-id="989e4-133">`TraceWriter` is defined in the [Azure WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/TraceWriter.cs).</span></span> <span data-ttu-id="989e4-134">Poziom dziennika `TraceWriter` można skonfigurować w [hosta\.json].</span><span class="sxs-lookup"><span data-stu-id="989e4-134">The log level for `TraceWriter` can be configured in [host\.json].</span></span>

```csharp
public static void Run(string myBlob, TraceWriter log)
{
    log.Info($"C# Blob trigger function processed: {myBlob}");
}
```

## <a name="async"></a><span data-ttu-id="989e4-135">Asynchroniczne</span><span class="sxs-lookup"><span data-stu-id="989e4-135">Async</span></span>
<span data-ttu-id="989e4-136">Aby funkcja asynchronicznego, użyj `async` — słowo kluczowe i przywracać `Task` obiektu.</span><span class="sxs-lookup"><span data-stu-id="989e4-136">To make a function asynchronous, use the `async` keyword and return a `Task` object.</span></span>

```csharp
public async static Task ProcessQueueMessageAsync(
        string blobName,
        Stream blobInput,
        Stream blobOutput)
{
    await blobInput.CopyToAsync(blobOutput, 4096, token);
}
```

## <a name="cancellation-token"></a><span data-ttu-id="989e4-137">Token anulowania</span><span class="sxs-lookup"><span data-stu-id="989e4-137">Cancellation Token</span></span>
<span data-ttu-id="989e4-138">Niektóre operacje wymagają łagodne zamykanie.</span><span class="sxs-lookup"><span data-stu-id="989e4-138">Some operations require graceful shutdown.</span></span> <span data-ttu-id="989e4-139">Mimo że zawsze jest najlepiej napisać kod, który może obsługiwać awarii, w przypadkach, w którym ma do obsługi bezpiecznego zamknięcia żądań, należy zdefiniować [ `CancellationToken` ](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typu argumentu.</span><span class="sxs-lookup"><span data-stu-id="989e4-139">While it's always best to write code that can handle crashing,  in cases where you want to handle graceful shutdown requests, you define a [`CancellationToken`](https://msdn.microsoft.com/library/system.threading.cancellationtoken.aspx) typed argument.</span></span>  <span data-ttu-id="989e4-140">A `CancellationToken` podano sygnalizują wyzwoleniu zamknięcie hosta.</span><span class="sxs-lookup"><span data-stu-id="989e4-140">A `CancellationToken` is provided to signal that a host shutdown is triggered.</span></span>

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

## <a name="importing-namespaces"></a><span data-ttu-id="989e4-141">Importowanie przestrzenie nazw</span><span class="sxs-lookup"><span data-stu-id="989e4-141">Importing namespaces</span></span>
<span data-ttu-id="989e4-142">Należy zaimportować przestrzeni nazw, należy tak jak zwykle, z `using` klauzuli.</span><span class="sxs-lookup"><span data-stu-id="989e4-142">If you need to import namespaces, you can do so as usual, with the `using` clause.</span></span>

```csharp
using System.Net;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="989e4-143">Następujących przestrzeni nazw są automatycznie importowane i w związku z tym są opcjonalne:</span><span class="sxs-lookup"><span data-stu-id="989e4-143">The following namespaces are automatically imported and are therefore optional:</span></span>

* `System`
* `System.Collections.Generic`
* `System.IO`
* `System.Linq`
* `System.Net.Http`
* `System.Threading.Tasks`
* `Microsoft.Azure.WebJobs`
* `Microsoft.Azure.WebJobs.Host`

## <a name="referencing-external-assemblies"></a><span data-ttu-id="989e4-144">Zewnętrzne zestawy odwołujące</span><span class="sxs-lookup"><span data-stu-id="989e4-144">Referencing External Assemblies</span></span>
<span data-ttu-id="989e4-145">Dla zestawów struktury, dodaj odwołania przy użyciu `#r "AssemblyName"` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="989e4-145">For framework assemblies, add references by using the `#r "AssemblyName"` directive.</span></span>

```csharp
#r "System.Web.Http"

using System.Net;
using System.Net.Http;
using System.Threading.Tasks;

public static Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
```

<span data-ttu-id="989e4-146">Następujące zestawy są automatycznie dodawane przez usługi Azure Functions Środowisko hostingu:</span><span class="sxs-lookup"><span data-stu-id="989e4-146">The following assemblies are automatically added by the Azure Functions hosting environment:</span></span>

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

<span data-ttu-id="989e4-147">Następujące zestawy mogą być używane przez prostą nazwę (na przykład `#r "AssemblyName"`):</span><span class="sxs-lookup"><span data-stu-id="989e4-147">The following assemblies may be referenced by simple-name (for example, `#r "AssemblyName"`):</span></span>

* `Newtonsoft.Json`
* `Microsoft.WindowsAzure.Storage`
* `Microsoft.ServiceBus`
* `Microsoft.AspNet.WebHooks.Receivers`
* `Microsoft.AspNet.WebHooks.Common`
* `Microsoft.Azure.NotificationHubs`

## <a name="referencing-custom-assemblies"></a><span data-ttu-id="989e4-148">Odwołania do zestawów niestandardowych</span><span class="sxs-lookup"><span data-stu-id="989e4-148">Referencing custom assemblies</span></span>

<span data-ttu-id="989e4-149">Aby odwołać niestandardowego zestawu, możesz użyć dowolnej *udostępnionego* zestawu lub *prywatnej* zestawu:</span><span class="sxs-lookup"><span data-stu-id="989e4-149">To reference a custom assembly, you can use either a *shared* assembly or a *private* assembly:</span></span>
- <span data-ttu-id="989e4-150">Zestawy udostępnione są współużytkowane przez wszystkie funkcje w aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="989e4-150">Shared assemblies are shared across all functions within a function app.</span></span> <span data-ttu-id="989e4-151">Aby odwołać się do niestandardowego zestawu Przekaż zestawu do aplikacji funkcji, takich jak w `bin` folder w katalogu głównym aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="989e4-151">To reference a custom assembly, upload the assembly to your function app, such as in a `bin` folder in the function app root.</span></span> 
- <span data-ttu-id="989e4-152">Zestawy prywatne są częścią kontekstu daną funkcję i obsługuje ładowania bezpośredniego w różnych wersjach.</span><span class="sxs-lookup"><span data-stu-id="989e4-152">Private assemblies are part of a given function's context, and support side-loading of different versions.</span></span> <span data-ttu-id="989e4-153">Zestawy prywatne należy przekazać w `bin` folderu w katalogu funkcji.</span><span class="sxs-lookup"><span data-stu-id="989e4-153">Private assemblies should be uploaded in a `bin` folder in the function directory.</span></span> <span data-ttu-id="989e4-154">Odwołanie przy użyciu nazwy pliku, takich jak `#r "MyAssembly.dll"`.</span><span class="sxs-lookup"><span data-stu-id="989e4-154">Reference using the file name, such as  `#r "MyAssembly.dll"`.</span></span> 

<span data-ttu-id="989e4-155">Aby uzyskać informacje na temat przekazywania plików do folderu funkcji zobacz sekcję poniżej pakietu zarządzania.</span><span class="sxs-lookup"><span data-stu-id="989e4-155">For information on how to upload files to your function folder, see the following section on package management.</span></span>

### <a name="watched-directories"></a><span data-ttu-id="989e4-156">Monitorowane katalogów</span><span class="sxs-lookup"><span data-stu-id="989e4-156">Watched directories</span></span>

<span data-ttu-id="989e4-157">Katalog zawierający plik skryptu funkcji automatycznie jest monitorowana zmian do zestawów.</span><span class="sxs-lookup"><span data-stu-id="989e4-157">The directory that contains the function script file is automatically watched for changes to assemblies.</span></span> <span data-ttu-id="989e4-158">Aby obejrzeć zmiany zestawu w innych katalogów, dodaj je do `watchDirectories` na liście [hosta\.json].</span><span class="sxs-lookup"><span data-stu-id="989e4-158">To watch for assembly changes in other directories, add them to the `watchDirectories` list in [host\.json].</span></span>

## <a name="using-nuget-packages"></a><span data-ttu-id="989e4-159">Za pomocą pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="989e4-159">Using NuGet packages</span></span>
<span data-ttu-id="989e4-160">Aby użyć pakietów NuGet w funkcji języka C#, Przekaż *project.json* plik do folderu funkcji w systemie plików aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="989e4-160">To use NuGet packages in a C# function, upload a *project.json* file to the function's folder in the function app's file system.</span></span> <span data-ttu-id="989e4-161">Oto przykład *project.json* pliku, który dodaje odwołanie do wersji 1.1.0 Microsoft.ProjectOxford.Face:</span><span class="sxs-lookup"><span data-stu-id="989e4-161">Here is an example *project.json* file that adds a reference to Microsoft.ProjectOxford.Face version 1.1.0:</span></span>

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

<span data-ttu-id="989e4-162">Obsługiwane jest tylko .NET Framework 4.6, upewnij się, że Twoje *project.json* Określa plik `net46` w sposób pokazany poniżej.</span><span class="sxs-lookup"><span data-stu-id="989e4-162">Only the .NET Framework 4.6 is supported, so make sure that your *project.json* file specifies `net46` as shown here.</span></span>

<span data-ttu-id="989e4-163">Po przekazaniu *project.json* plików, środowisko uruchomieniowe pobiera pakiety i automatycznie dodaje odwołania do zestawów pakietu.</span><span class="sxs-lookup"><span data-stu-id="989e4-163">When you upload a *project.json* file, the runtime gets the packages and automatically adds references to the package assemblies.</span></span> <span data-ttu-id="989e4-164">Nie trzeba dodać `#r "AssemblyName"` dyrektywy.</span><span class="sxs-lookup"><span data-stu-id="989e4-164">You don't need to add `#r "AssemblyName"` directives.</span></span> <span data-ttu-id="989e4-165">Aby użyć typów zdefiniowanych w pakietach NuGet, Dodaj wymagane `using` instrukcje do Twojej *run.csx* pliku</span><span class="sxs-lookup"><span data-stu-id="989e4-165">To use the types defined in the NuGet packages, add the required `using` statements to your *run.csx* file</span></span> 

<span data-ttu-id="989e4-166">W środowisku wykonawczym funkcji Przywracanie NuGet działa na podstawie porównania ilości `project.json` i `project.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="989e4-166">In the Functions runtime, NuGet restore works by comparing `project.json` and `project.lock.json`.</span></span> <span data-ttu-id="989e4-167">Jeśli pliki sygnatur Data i godzina **nie** uruchamia Przywracanie NuGet dopasowania i pliki do pobrania NuGet zaktualizowane pakiety.</span><span class="sxs-lookup"><span data-stu-id="989e4-167">If the date and time stamps of the files **do not** match, a NuGet restore runs and NuGet downloads updated packages.</span></span> <span data-ttu-id="989e4-168">Jednak jeśli oznaczenie daty i godziny plików **czy** dopasowania, NuGet nie wykonuje operację przywracania.</span><span class="sxs-lookup"><span data-stu-id="989e4-168">However, if the date and time stamps of the files **do** match, NuGet does not perform a restore.</span></span> <span data-ttu-id="989e4-169">W związku z tym `project.lock.json` nie powinny zostać wdrożone, ponieważ powoduje on NuGet pominąć Przywracanie pakietu.</span><span class="sxs-lookup"><span data-stu-id="989e4-169">Therefore, `project.lock.json` should not be deployed as it causes NuGet to skip package restore.</span></span> <span data-ttu-id="989e4-170">Aby uniknąć wdrażanie pliku blokady, Dodaj `project.lock.json` do `.gitignore` pliku.</span><span class="sxs-lookup"><span data-stu-id="989e4-170">To avoid deploying the lock file, add the `project.lock.json` to the `.gitignore` file.</span></span>

<span data-ttu-id="989e4-171">Aby użyć niestandardowej NuGet źródła danych, określ źródła danych w *Nuget.Config* w katalogu głównym aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="989e4-171">To use a custom NuGet feed, specify the feed in a *Nuget.Config* file in the Function App root.</span></span> <span data-ttu-id="989e4-172">Aby uzyskać więcej informacji, zobacz [NuGet Konfigurowanie zachowania](/nuget/consume-packages/configuring-nuget-behavior).</span><span class="sxs-lookup"><span data-stu-id="989e4-172">For more information, see [Configuring NuGet behavior](/nuget/consume-packages/configuring-nuget-behavior).</span></span>

### <a name="using-a-projectjson-file"></a><span data-ttu-id="989e4-173">Przy użyciu pliku project.json</span><span class="sxs-lookup"><span data-stu-id="989e4-173">Using a project.json file</span></span>
1. <span data-ttu-id="989e4-174">Otwarcie funkcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="989e4-174">Open the function in the Azure portal.</span></span> <span data-ttu-id="989e4-175">Na karcie dzienniki są wyświetlane dane wyjściowe instalacji pakietu.</span><span class="sxs-lookup"><span data-stu-id="989e4-175">The logs tab displays the package installation output.</span></span>
2. <span data-ttu-id="989e4-176">Aby przekazać plik project.json, użyj jednej z metod opisanych w [jak zaktualizować pliki aplikacji funkcji](functions-reference.md#fileupdate) w temacie Odwołanie do usługi Azure Functions dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="989e4-176">To upload a project.json file, use one of the methods described in the [How to update function app files](functions-reference.md#fileupdate) in the Azure Functions developer reference topic.</span></span>
3. <span data-ttu-id="989e4-177">Po *project.json* przekazać pliku, wyświetlone dane wyjściowe podobne do poniższego przykładu w funkcji do przesyłania strumieniowego dzienników:</span><span class="sxs-lookup"><span data-stu-id="989e4-177">After the *project.json* file is uploaded, you see output like the following example in your function's streaming log:</span></span>

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

## <a name="environment-variables"></a><span data-ttu-id="989e4-178">Zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="989e4-178">Environment variables</span></span>
<span data-ttu-id="989e4-179">Aby uzyskać wartość zmiennej środowiskowej lub wartość ustawienia aplikacji, należy użyć `System.Environment.GetEnvironmentVariable`, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="989e4-179">To get an environment variable or an app setting value, use `System.Environment.GetEnvironmentVariable`, as shown in the following code example:</span></span>

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

## <a name="reusing-csx-code"></a><span data-ttu-id="989e4-180">Ponowne wykorzystywanie kodu csx</span><span class="sxs-lookup"><span data-stu-id="989e4-180">Reusing .csx code</span></span>
<span data-ttu-id="989e4-181">Można użyć klasy i metody zdefiniowane w innych *csx* pliki w Twojej *run.csx* pliku.</span><span class="sxs-lookup"><span data-stu-id="989e4-181">You can use classes and methods defined in other *.csx* files in your *run.csx* file.</span></span> <span data-ttu-id="989e4-182">Aby to zrobić, użyj `#load` dyrektywy w Twojej *run.csx* pliku.</span><span class="sxs-lookup"><span data-stu-id="989e4-182">To do that, use `#load` directives in your *run.csx* file.</span></span> <span data-ttu-id="989e4-183">W poniższym przykładzie o nazwie Procedura rejestrowania `MyLogger` są udostępniane w *myLogger.csx* i ładowane do *run.csx* przy użyciu `#load` dyrektywy:</span><span class="sxs-lookup"><span data-stu-id="989e4-183">In the following example, a logging routine named `MyLogger` is shared in *myLogger.csx* and loaded into *run.csx* using the `#load` directive:</span></span>

<span data-ttu-id="989e4-184">Przykład *run.csx*:</span><span class="sxs-lookup"><span data-stu-id="989e4-184">Example *run.csx*:</span></span>

```csharp
#load "mylogger.csx"

public static void Run(TimerInfo myTimer, TraceWriter log)
{
    log.Verbose($"Log by run.csx: {DateTime.Now}");
    MyLogger(log, $"Log by MyLogger: {DateTime.Now}");
}
```

<span data-ttu-id="989e4-185">Przykład *mylogger.csx*:</span><span class="sxs-lookup"><span data-stu-id="989e4-185">Example *mylogger.csx*:</span></span>

```csharp
public static void MyLogger(TraceWriter log, string logtext)
{
    log.Verbose(logtext);
}
```

<span data-ttu-id="989e4-186">Za pomocą udostępnionej *csx* jest wspólnym wzorcem można zdecydowanie wpisz argumentów pomiędzy funkcjami przy użyciu obiektu POCO.</span><span class="sxs-lookup"><span data-stu-id="989e4-186">Using a shared *.csx* is a common pattern when you want to strongly type your arguments between functions using a POCO object.</span></span> <span data-ttu-id="989e4-187">W poniższym przykładzie uproszczony wyzwalacza HTTP i kolejki wyzwalacza udziału obiektu POCO o nazwie `Order` do silnie typu danych kolejności:</span><span class="sxs-lookup"><span data-stu-id="989e4-187">In the following simplified example, an HTTP trigger and queue trigger share a POCO object named `Order` to strongly type the order data:</span></span>

<span data-ttu-id="989e4-188">Przykład *run.csx* wyzwalacza HTTP:</span><span class="sxs-lookup"><span data-stu-id="989e4-188">Example *run.csx* for HTTP trigger:</span></span>

```cs
#load "..\shared\order.csx"

using System.Net;

public static async Task<HttpResponseMessage> Run(Order req, IAsyncCollector<Order> outputQueueItem, TraceWriter log)
{
    log.Info("C# HTTP trigger function received an order.");
    log.Info(req.ToString());
    log.Info("Submitting to processing queue.");

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

<span data-ttu-id="989e4-189">Przykład *run.csx* wyzwalacza kolejki:</span><span class="sxs-lookup"><span data-stu-id="989e4-189">Example *run.csx* for queue trigger:</span></span>

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

<span data-ttu-id="989e4-190">Przykład *order.csx*:</span><span class="sxs-lookup"><span data-stu-id="989e4-190">Example *order.csx*:</span></span>

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

<span data-ttu-id="989e4-191">Można użyć ścieżki względnej z `#load` dyrektywy:</span><span class="sxs-lookup"><span data-stu-id="989e4-191">You can use a relative path with the `#load` directive:</span></span>

* <span data-ttu-id="989e4-192">`#load "mylogger.csx"`ładuje plik znajduje się w folderze funkcji.</span><span class="sxs-lookup"><span data-stu-id="989e4-192">`#load "mylogger.csx"` loads a file located in the function folder.</span></span>
* <span data-ttu-id="989e4-193">`#load "loadedfiles\mylogger.csx"`ładuje plik znajdujący się w folderze w folderze funkcji.</span><span class="sxs-lookup"><span data-stu-id="989e4-193">`#load "loadedfiles\mylogger.csx"` loads a file located in a folder in the function folder.</span></span>
* <span data-ttu-id="989e4-194">`#load "..\shared\mylogger.csx"`ładuje plik znajdujący się w folderze na tym samym poziomie co folder funkcji, bezpośrednio pod *wwwroot*.</span><span class="sxs-lookup"><span data-stu-id="989e4-194">`#load "..\shared\mylogger.csx"` loads a file located in a folder at the same level as the function folder, that is, directly under *wwwroot*.</span></span>

<span data-ttu-id="989e4-195">`#load` Dyrektywy działa tylko w przypadku *csx* plików (C# skrypt), nie z *.cs* plików.</span><span class="sxs-lookup"><span data-stu-id="989e4-195">The `#load` directive works only with *.csx* (C# script) files, not with *.cs* files.</span></span>

<a name="imperative-bindings"></a> 

## <a name="binding-at-runtime-via-imperative-bindings"></a><span data-ttu-id="989e4-196">Powiązanie w czasie wykonywania za pośrednictwem powiązania imperatywne</span><span class="sxs-lookup"><span data-stu-id="989e4-196">Binding at runtime via imperative bindings</span></span>

<span data-ttu-id="989e4-197">W języku C# i innych języków .NET, można użyć [imperatywnych](https://en.wikipedia.org/wiki/Imperative_programming) powiązanie wzorzec, w przeciwieństwie do [ *deklaratywne* ](https://en.wikipedia.org/wiki/Declarative_programming) powiązania w *function.json*.</span><span class="sxs-lookup"><span data-stu-id="989e4-197">In C# and other .NET languages, you can use an [imperative](https://en.wikipedia.org/wiki/Imperative_programming) binding pattern, as opposed to the [*declarative*](https://en.wikipedia.org/wiki/Declarative_programming) bindings in *function.json*.</span></span> <span data-ttu-id="989e4-198">Powiązanie konieczne jest przydatne, gdy Parametry wiążące muszą ma zostać obliczony w czasie środowiska uruchomieniowego zamiast projektu.</span><span class="sxs-lookup"><span data-stu-id="989e4-198">Imperative binding is useful when binding parameters need to be computed at runtime rather than design time.</span></span> <span data-ttu-id="989e4-199">Z tego wzorca można powiązać z obsługiwanych danych wejściowych i wyjściowych powiązania na bieżąco w kodzie funkcji.</span><span class="sxs-lookup"><span data-stu-id="989e4-199">With this pattern, you can bind to supported input and output binding on-the-fly in your function code.</span></span>

<span data-ttu-id="989e4-200">Zdefiniuj staje się niezbędna powiązania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="989e4-200">Define an imperative binding as follows:</span></span>

- <span data-ttu-id="989e4-201">**Nie** obejmują wpis w *function.json* dla żądanego imperatywnych powiązania.</span><span class="sxs-lookup"><span data-stu-id="989e4-201">**Do not** include an entry in *function.json* for your desired imperative bindings.</span></span>
- <span data-ttu-id="989e4-202">Przekaż parametr wejściowy [ `Binder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) lub [ `IBinder binder` ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span><span class="sxs-lookup"><span data-stu-id="989e4-202">Pass in an input parameter [`Binder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Host/Bindings/Runtime/Binder.cs) or [`IBinder binder`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IBinder.cs).</span></span>
- <span data-ttu-id="989e4-203">Aby wykonać wiązania danych, użyj następującego wzorca C#.</span><span class="sxs-lookup"><span data-stu-id="989e4-203">Use the following C# pattern to perform the data binding.</span></span>

```cs
using (var output = await binder.BindAsync<T>(new BindingTypeAttribute(...)))
{
    ...
}
```

<span data-ttu-id="989e4-204">gdzie `BindingTypeAttribute` jest atrybut .NET, który definiuje wiązania i `T` jest typ danych wejściowych lub wyjściowych, który jest obsługiwany przez ten typ powiązania.</span><span class="sxs-lookup"><span data-stu-id="989e4-204">where `BindingTypeAttribute` is the .NET attribute that defines your binding and `T` is the input or output type that's supported by that binding type.</span></span> <span data-ttu-id="989e4-205">`T`nie może być `out` typ parametru (takie jak `out JObject`).</span><span class="sxs-lookup"><span data-stu-id="989e4-205">`T` also cannot be an `out` parameter type (such as `out JObject`).</span></span> <span data-ttu-id="989e4-206">Na przykład, w tabeli Mobile Apps output powiązanie obsługuje [sześć output typy](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), ale można używać tylko [ICollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) lub [IAsyncCollector<T> ](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) dla `T`.</span><span class="sxs-lookup"><span data-stu-id="989e4-206">For example, the Mobile Apps table output binding supports [six output types](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs#L17-L22), but you can only use [ICollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/ICollector.cs) or [IAsyncCollector<T>](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/IAsyncCollector.cs) for `T`.</span></span>

<span data-ttu-id="989e4-207">Poniższy przykładowy kod tworzy [powiązania wyjściowego obiektu blob magazynu](functions-bindings-storage-blob.md#using-a-blob-output-binding) z obiektu blob ścieżki, która jest zdefiniowana w czasie wykonywania, następnie zapisuje ciąg obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="989e4-207">The following example code creates a [Storage blob output binding](functions-bindings-storage-blob.md#using-a-blob-output-binding) with blob path that's defined at run time, then writes a string to the blob.</span></span>

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

<span data-ttu-id="989e4-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) definiuje [obiektu blob magazynu](functions-bindings-storage-blob.md) wejściowych lub wyjściowych powiązanie, i [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) jest typ powiązania obsługiwanych danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="989e4-208">[BlobAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs) defines the [Storage blob](functions-bindings-storage-blob.md) input or output binding, and [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) is a supported output binding type.</span></span>
<span data-ttu-id="989e4-209">Jest dostępna, kod pobiera domyślne ustawienie aplikacji dla parametrów połączenia konta magazynu (czyli `AzureWebJobsStorage`).</span><span class="sxs-lookup"><span data-stu-id="989e4-209">As is, the code gets the default app setting for the Storage account connection string (which is `AzureWebJobsStorage`).</span></span> <span data-ttu-id="989e4-210">Można określić ustawienia aplikacji niestandardowej do użycia przez dodanie [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) i przekazanie tablicy atrybut do `BindAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="989e4-210">You can specify a custom app setting to use by adding the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) and passing the attribute array into `BindAsync<T>()`.</span></span> <span data-ttu-id="989e4-211">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="989e4-211">For example,</span></span>

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

<span data-ttu-id="989e4-212">W poniższej tabeli przedstawiono atrybuty .NET dla każdego typu powiązania i pakiety, w których są zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="989e4-212">The following table lists the .NET attributes for each binding type and the packages in which they are defined.</span></span>

> [!div class="mx-codeBreakAll"]
| <span data-ttu-id="989e4-213">Powiązanie</span><span class="sxs-lookup"><span data-stu-id="989e4-213">Binding</span></span> | <span data-ttu-id="989e4-214">Atrybut</span><span class="sxs-lookup"><span data-stu-id="989e4-214">Attribute</span></span> | <span data-ttu-id="989e4-215">Dodaj odwołanie</span><span class="sxs-lookup"><span data-stu-id="989e4-215">Add reference</span></span> |
|------|------|------|
| <span data-ttu-id="989e4-216">Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="989e4-216">Cosmos DB</span></span> | [`Microsoft.Azure.WebJobs.DocumentDBAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.DocumentDB"` |
| <span data-ttu-id="989e4-217">Usługa Event Hubs</span><span class="sxs-lookup"><span data-stu-id="989e4-217">Event Hubs</span></span> | <span data-ttu-id="989e4-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="989e4-218">[`Microsoft.Azure.WebJobs.ServiceBus.EventHubAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/EventHubs/EventHubAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.Jobs.ServiceBus"` |
| <span data-ttu-id="989e4-219">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="989e4-219">Mobile Apps</span></span> | [`Microsoft.Azure.WebJobs.MobileTableAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.MobileApps"` |
| <span data-ttu-id="989e4-220">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="989e4-220">Notification Hubs</span></span> | [`Microsoft.Azure.WebJobs.NotificationHubAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.NotificationHubs/NotificationHubAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.NotificationHubs"` |
| <span data-ttu-id="989e4-221">Service Bus</span><span class="sxs-lookup"><span data-stu-id="989e4-221">Service Bus</span></span> | <span data-ttu-id="989e4-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="989e4-222">[`Microsoft.Azure.WebJobs.ServiceBusAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAttribute.cs), [`Microsoft.Azure.WebJobs.ServiceBusAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.ServiceBus/ServiceBusAccountAttribute.cs)</span></span> | `#r "Microsoft.Azure.WebJobs.ServiceBus"` |
| <span data-ttu-id="989e4-223">Kolejki magazynu</span><span class="sxs-lookup"><span data-stu-id="989e4-223">Storage queue</span></span> | <span data-ttu-id="989e4-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="989e4-224">[`Microsoft.Azure.WebJobs.QueueAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/QueueAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="989e4-225">Obiektu blob magazynu</span><span class="sxs-lookup"><span data-stu-id="989e4-225">Storage blob</span></span> | <span data-ttu-id="989e4-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="989e4-226">[`Microsoft.Azure.WebJobs.BlobAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/BlobAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="989e4-227">Tabela magazynu</span><span class="sxs-lookup"><span data-stu-id="989e4-227">Storage table</span></span> | <span data-ttu-id="989e4-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span><span class="sxs-lookup"><span data-stu-id="989e4-228">[`Microsoft.Azure.WebJobs.TableAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/TableAttribute.cs), [`Microsoft.Azure.WebJobs.StorageAccountAttribute`](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs)</span></span> | |
| <span data-ttu-id="989e4-229">Twilio</span><span class="sxs-lookup"><span data-stu-id="989e4-229">Twilio</span></span> | [`Microsoft.Azure.WebJobs.TwilioSmsAttribute`](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.Twilio/TwilioSMSAttribute.cs) | `#r "Microsoft.Azure.WebJobs.Extensions.Twilio"` |



## <a name="next-steps"></a><span data-ttu-id="989e4-230">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="989e4-230">Next steps</span></span>
<span data-ttu-id="989e4-231">Więcej informacji zawierają następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="989e4-231">For more information, see the following resources:</span></span>

* [<span data-ttu-id="989e4-232">Najlepsze rozwiązania dotyczące usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="989e4-232">Best Practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="989e4-233">Dokumentacja usługi Azure Functions dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="989e4-233">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="989e4-234">Azure dokumentacja dla deweloperów funkcje F #</span><span class="sxs-lookup"><span data-stu-id="989e4-234">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="989e4-235">Dokumentacja dla deweloperów NodeJS funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="989e4-235">Azure Functions NodeJS developer reference</span></span>](functions-reference-node.md)
* [<span data-ttu-id="989e4-236">Azure funkcje wyzwalaczy i powiązań</span><span class="sxs-lookup"><span data-stu-id="989e4-236">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

[host\.json]: https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json
