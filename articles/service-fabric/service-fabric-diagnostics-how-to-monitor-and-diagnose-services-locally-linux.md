---
title: "Debugowanie mikrousług Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak monitorowanie i diagnozowanie usługi napisane przy użyciu usługi sieć szkieletowa usług Microsoft Azure na maszynie lokalnej."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 4bc73f581f4855ebc724df19dd56fab8bf103854
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="3e934-103">Monitorowanie i diagnozowanie usług w Instalatorze programowanie komputera lokalnego</span><span class="sxs-lookup"><span data-stu-id="3e934-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e934-104">Windows</span><span class="sxs-lookup"><span data-stu-id="3e934-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="3e934-105">Linux</span><span class="sxs-lookup"><span data-stu-id="3e934-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="3e934-106">Monitorowanie, wykrywanie, diagnozowanie i rozwiązywanie problemów z umożliwiają usług kontynuować przy minimalnym przerw w działaniu środowiska użytkownika.</span><span class="sxs-lookup"><span data-stu-id="3e934-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services to continue with minimal disruption to the user experience.</span></span> <span data-ttu-id="3e934-107">Monitorowania i diagnostyki są szczególnie ważne w środowisku produkcyjnym wdrożony rzeczywisty.</span><span class="sxs-lookup"><span data-stu-id="3e934-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="3e934-108">Przyjmowanie podobne modelu podczas tworzenia usługi gwarantuje, że diagnostycznych potoku działa w przypadku przenoszenia do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="3e934-108">Adopting a similar model during development of services ensures that the diagnostic pipeline works when you move to a production environment.</span></span> <span data-ttu-id="3e934-109">Sieć szkieletowa usług ułatwia deweloperom usługa implementuje diagnostyki bezproblemowo działającej na konfiguracje pojedynczego komputera lokalnego rozwoju i w konfiguracji klastra produkcyjnego rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="3e934-109">Service Fabric makes it easy for service developers to implement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="3e934-110">Debugowanie aplikacji Java sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="3e934-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="3e934-111">W przypadku aplikacji Java [wiele platform rejestrowania](http://en.wikipedia.org/wiki/Java_logging_framework) są dostępne.</span><span class="sxs-lookup"><span data-stu-id="3e934-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="3e934-112">Ponieważ `java.util.logging` jest domyślną opcją ze środowiska JRE, jest również używana dla [przykładów kodu w witrynie github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="3e934-112">Since `java.util.logging` is the default option with the JRE, it is also used for the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="3e934-113">Następujące dyskusji wyjaśniono sposób konfigurowania `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="3e934-113">The following discussion explains how to configure the `java.util.logging` framework.</span></span>

<span data-ttu-id="3e934-114">Przy użyciu java.util.logging można przekierować Dzienniki aplikacji do pamięci, strumienie wyjściowe, pliki konsoli lub gniazda.</span><span class="sxs-lookup"><span data-stu-id="3e934-114">Using java.util.logging you can redirect your application logs to memory, output streams, console files, or sockets.</span></span> <span data-ttu-id="3e934-115">Dla każdej z tych opcji są już udostępniane w ramach obsługi domyślne.</span><span class="sxs-lookup"><span data-stu-id="3e934-115">For each of these options, there are default handlers already provided in the framework.</span></span> <span data-ttu-id="3e934-116">Można utworzyć `app.properties` pliku, aby skonfigurować obsługę plików dla aplikacji przekierować wszystkie dzienniki do pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="3e934-116">You can create a `app.properties` file to configure the file handler for your application to redirect all logs to a local file.</span></span>

<span data-ttu-id="3e934-117">Poniższy fragment kodu zawiera przykładową konfigurację:</span><span class="sxs-lookup"><span data-stu-id="3e934-117">The following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="3e934-118">Folder wskazywana przez `app.properties` plik musi istnieć.</span><span class="sxs-lookup"><span data-stu-id="3e934-118">The folder pointed to by the `app.properties` file must exist.</span></span> <span data-ttu-id="3e934-119">Po `app.properties` plik jest tworzony, musisz także zmodyfikować skrypt punktu wejścia `entrypoint.sh` w `<applicationfolder>/<servicePkg>/Code/` folderu można ustawić właściwości `java.util.logging.config.file` do `app.propertes` pliku.</span><span class="sxs-lookup"><span data-stu-id="3e934-119">After the `app.properties` file is created, you need to also modify your entry point script, `entrypoint.sh` in the `<applicationfolder>/<servicePkg>/Code/` folder to set the property `java.util.logging.config.file` to `app.propertes` file.</span></span> <span data-ttu-id="3e934-120">Wpis powinien wyglądać w następujący fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="3e934-120">The entry should look like the following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path to app.properties> -jar <service name>.jar
```


<span data-ttu-id="3e934-121">Ta konfiguracja powoduje dzienniki są zbierane w sposób obracania w `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="3e934-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="3e934-122">W takim przypadku plik dziennika ma nazwę mysfapp%u.%g.log gdzie:</span><span class="sxs-lookup"><span data-stu-id="3e934-122">The log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="3e934-123">**%u** to unikatowy numer, aby rozwiązać konflikty między równoczesnych procesów Java.</span><span class="sxs-lookup"><span data-stu-id="3e934-123">**%u** is a unique number to resolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="3e934-124">**%g** jest to liczba generacji, aby odróżnić obracanie dzienniki.</span><span class="sxs-lookup"><span data-stu-id="3e934-124">**%g** is the generation number to distinguish between rotating logs.</span></span>

<span data-ttu-id="3e934-125">Domyślnie jeśli jawnie jest skonfigurowany bez obsługi, program obsługi konsoli jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="3e934-125">By default if no handler is explicitly configured, the console handler is registered.</span></span> <span data-ttu-id="3e934-126">Jeden Wyświetl dzienniki SYSLOG w obszarze /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="3e934-126">One can view the logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="3e934-127">Aby uzyskać więcej informacji, zobacz [przykładów kodu w witrynie github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="3e934-127">For more information, see the [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="3e934-128">Debugowanie aplikacji usługi sieci szkieletowej C#</span><span class="sxs-lookup"><span data-stu-id="3e934-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="3e934-129">Wiele platform są dostępne dla śledzenia środowisko CoreCLR aplikacji w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="3e934-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="3e934-130">Aby uzyskać więcej informacji, zobacz [GitHub: rejestrowanie](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="3e934-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="3e934-131">Ponieważ EventSource jest znane deweloperom korzystającym z języka C#, "w tym artykule wykorzystano źródła zdarzeń śledzenia w środowisko CoreCLR próbek w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="3e934-131">Since EventSource is familiar to C# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="3e934-132">Pierwszym krokiem jest uwzględnienie System.Diagnostics.Tracing, dzięki czemu może zapisać dzienników pamięci, strumienie wyjściowe lub pliki konsoli.</span><span class="sxs-lookup"><span data-stu-id="3e934-132">The first step is to include System.Diagnostics.Tracing so that you can write your logs to memory, output streams, or console files.</span></span>  <span data-ttu-id="3e934-133">Przy użyciu źródła zdarzeń logowania, należy dodać następującego projektu do pliku project.json:</span><span class="sxs-lookup"><span data-stu-id="3e934-133">For logging using EventSource, add the following project to your project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="3e934-134">Niestandardowe odbiornika danych służy do nasłuchiwania zdarzeń usługi, a następnie odpowiednio przekierować je do plików śledzenia.</span><span class="sxs-lookup"><span data-stu-id="3e934-134">You can use a custom EventListener to listen for the service event and then appropriately redirect them to trace files.</span></span> <span data-ttu-id="3e934-135">Poniższy fragment kodu przedstawia przykładowe zastosowanie rejestrowania przy użyciu źródła zdarzeń i niestandardowych odbiornika zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="3e934-135">The following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need to add method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="3e934-136">Poprzedni fragment danych wyjściowych dzienników do pliku w `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="3e934-136">The preceding snippet outputs the logs to a file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="3e934-137">Ta nazwa pliku musi odpowiednio aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="3e934-137">This file name needs to be appropriately updated.</span></span> <span data-ttu-id="3e934-138">W przypadku, gdy chcesz przekierowywać dzienniki, aby konsoli, użyj następującego fragmentu kodu w klasie odbiornika zdarzeń niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="3e934-138">In case you want to redirect the logs to console, use the following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="3e934-139">Przykłady w [przykłady dotyczące języka C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) Użyj EventSource i niestandardowych odbiornika zdarzeń do dziennika zdarzeń do pliku.</span><span class="sxs-lookup"><span data-stu-id="3e934-139">The samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener to log events to a file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="3e934-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3e934-140">Next steps</span></span>
<span data-ttu-id="3e934-141">Ten sam kod śledzenia dodany do aplikacji współdziała również z diagnostyki aplikacji w klastrze platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3e934-141">The same tracing code added to your application also works with the diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="3e934-142">Zapoznaj się z tych artykułach, omówiono w nim różne opcje dla narzędzi, które opisano, jak je skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="3e934-142">Check out these articles that discuss the different options for the tools and describe how to set them up.</span></span>
* [<span data-ttu-id="3e934-143">Jak zebrać dzienniki Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="3e934-143">How to collect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
