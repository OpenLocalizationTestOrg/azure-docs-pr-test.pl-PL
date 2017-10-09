---
title: "aaaDebug mikrousług Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor i diagnozowania usług napisane przy użyciu usługi sieć szkieletowa usług Microsoft Azure na maszynie lokalnej."
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
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="f6078-103">Monitorowanie i diagnozowanie usług w Instalatorze programowanie komputera lokalnego</span><span class="sxs-lookup"><span data-stu-id="f6078-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="f6078-104">Windows</span><span class="sxs-lookup"><span data-stu-id="f6078-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="f6078-105">Linux</span><span class="sxs-lookup"><span data-stu-id="f6078-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="f6078-106">Monitorowanie, wykrywanie, diagnozowanie i rozwiązywanie problemów z umożliwiają toocontinue usług z minimalnym przerw w działaniu toohello użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f6078-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="f6078-107">Monitorowania i diagnostyki są szczególnie ważne w środowisku produkcyjnym wdrożony rzeczywisty.</span><span class="sxs-lookup"><span data-stu-id="f6078-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="f6078-108">Przyjmowanie podobne modelu podczas tworzenia usług gwarantuje, że tego potoku diagnostycznych hello działa podczas przenoszenia tooa środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="f6078-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="f6078-109">Sieć szkieletowa usług ułatwia diagnostyki tooimplement deweloperów usługi może bezproblemowo współpracować na konfiguracje pojedynczego komputera lokalnego rozwoju i w konfiguracji klastra produkcyjnego rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="f6078-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="f6078-110">Debugowanie aplikacji Java sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="f6078-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="f6078-111">W przypadku aplikacji Java [wiele platform rejestrowania](http://en.wikipedia.org/wiki/Java_logging_framework) są dostępne.</span><span class="sxs-lookup"><span data-stu-id="f6078-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="f6078-112">Ponieważ `java.util.logging` jest opcja domyślna hello z hello środowiska JRE, jest również używana dla hello [przykładów kodu w witrynie github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f6078-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="f6078-113">Hello następujące dyskusji wyjaśniono, jak tooconfigure hello `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="f6078-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="f6078-114">Przy użyciu aplikacji można przekierowywać java.util.logging rejestruje toomemory, strumienie wyjściowe, pliki konsoli lub gniazda.</span><span class="sxs-lookup"><span data-stu-id="f6078-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="f6078-115">Dla każdej z tych opcji są już udostępniane w ramach hello obsługi domyślne.</span><span class="sxs-lookup"><span data-stu-id="f6078-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="f6078-116">Można utworzyć `app.properties` obsługi plików hello tooconfigure pliku dla twojej aplikacji tooredirect wszystkie dzienniki tooa pliku lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f6078-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="f6078-117">Witaj następującego fragmentu kodu zawiera przykładową konfigurację:</span><span class="sxs-lookup"><span data-stu-id="f6078-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="f6078-118">Witaj Witaj tooby wskazywany folder `app.properties` plik musi istnieć.</span><span class="sxs-lookup"><span data-stu-id="f6078-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="f6078-119">Po hello `app.properties` plik jest tworzony, należy tooalso zmodyfikować skrypt punktu wejścia `entrypoint.sh` w hello `<applicationfolder>/<servicePkg>/Code/` folderu tooset hello właściwości `java.util.logging.config.file` zbyt`app.propertes` pliku.</span><span class="sxs-lookup"><span data-stu-id="f6078-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="f6078-120">wpis Hello powinna wyglądać powitania po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="f6078-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="f6078-121">Ta konfiguracja powoduje dzienniki są zbierane w sposób obracania w `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="f6078-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="f6078-122">w takim przypadku Hello plik dziennika ma nazwę mysfapp%u.%g.log gdzie:</span><span class="sxs-lookup"><span data-stu-id="f6078-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="f6078-123">**%u** jest unikatowy tooresolve numer konfliktów między równoczesnych procesów Java.</span><span class="sxs-lookup"><span data-stu-id="f6078-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="f6078-124">**%g** jest hello generowania numerów toodistinguish między obracanie dzienników.</span><span class="sxs-lookup"><span data-stu-id="f6078-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="f6078-125">Domyślnie jeśli jawnie jest skonfigurowany bez obsługi, program obsługi konsoli hello jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="f6078-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="f6078-126">Jeden hello dzienniki można wyświetlać w syslog w obszarze /var/log/syslog.</span><span class="sxs-lookup"><span data-stu-id="f6078-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="f6078-127">Aby uzyskać więcej informacji, zobacz hello [przykładów kodu w witrynie github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f6078-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="f6078-128">Debugowanie aplikacji usługi sieci szkieletowej C#</span><span class="sxs-lookup"><span data-stu-id="f6078-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="f6078-129">Wiele platform są dostępne dla śledzenia środowisko CoreCLR aplikacji w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="f6078-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="f6078-130">Aby uzyskać więcej informacji, zobacz [GitHub: rejestrowanie](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="f6078-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="f6078-131">Ponieważ EventSource znanych tooC # deweloperów "w tym artykule wykorzystano źródła zdarzeń śledzenia w środowisko CoreCLR próbek w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="f6078-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="f6078-132">pierwszym krokiem Hello jest tooinclude System.Diagnostics.Tracing, aby mogły zapisywać Twoje toomemory dzienniki, strumienie wyjściowe lub pliki konsoli.</span><span class="sxs-lookup"><span data-stu-id="f6078-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="f6078-133">Do rejestrowania przy użyciu elementu EventSource, Dodaj powitania po project.json tooyour projektu:</span><span class="sxs-lookup"><span data-stu-id="f6078-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="f6078-134">Można użyć niestandardowych toolisten odbiornika zdarzeń dla zdarzenia usługi hello i następnie odpowiednio przekierować je tootrace plików.</span><span class="sxs-lookup"><span data-stu-id="f6078-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="f6078-135">Witaj poniższy fragment kodu przedstawia przykładowe zastosowanie rejestrowania przy użyciu źródła zdarzeń i niestandardowych odbiornika zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="f6078-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


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

        // TBD: Need tooadd method for sample event.

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


<span data-ttu-id="f6078-136">Hello poprzedniego fragment danych wyjściowych pliku tooa dzienniki hello w `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="f6078-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="f6078-137">Ta nazwa pliku musi toobe odpowiednio aktualizowane.</span><span class="sxs-lookup"><span data-stu-id="f6078-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="f6078-138">W przypadku, gdy chcesz tooredirect hello dzienniki tooconsole, użyj hello następującego fragmentu kodu w klasie odbiornika zdarzeń niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="f6078-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="f6078-139">Witaj próbek w [przykłady dotyczące języka C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) EventSource i niestandardowego pliku tooa zdarzenia toolog odbiornika danych.</span><span class="sxs-lookup"><span data-stu-id="f6078-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="f6078-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6078-140">Next steps</span></span>
<span data-ttu-id="f6078-141">Witaj sam kod śledzenia dodane tooyour aplikacji współdziała również z hello diagnostyki aplikacji w klastrze platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f6078-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="f6078-142">Wyewidencjonowanie te artykuły omówiono w nim różne opcje narzędzia hello hello i opisujących sposób tooset je.</span><span class="sxs-lookup"><span data-stu-id="f6078-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="f6078-143">Sposób rejestrowania toocollect Diagnostyka Azure</span><span class="sxs-lookup"><span data-stu-id="f6078-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
