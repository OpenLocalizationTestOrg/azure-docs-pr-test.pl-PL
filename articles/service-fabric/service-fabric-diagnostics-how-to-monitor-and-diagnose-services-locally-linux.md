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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>Monitorowanie i diagnozowanie usług w Instalatorze programowanie komputera lokalnego


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

Monitorowanie, wykrywanie, diagnozowanie i rozwiązywanie problemów z umożliwiają toocontinue usług z minimalnym przerw w działaniu toohello użytkowników. Monitorowania i diagnostyki są szczególnie ważne w środowisku produkcyjnym wdrożony rzeczywisty. Przyjmowanie podobne modelu podczas tworzenia usług gwarantuje, że tego potoku diagnostycznych hello działa podczas przenoszenia tooa środowiska produkcyjnego. Sieć szkieletowa usług ułatwia diagnostyki tooimplement deweloperów usługi może bezproblemowo współpracować na konfiguracje pojedynczego komputera lokalnego rozwoju i w konfiguracji klastra produkcyjnego rzeczywistych.


## <a name="debugging-service-fabric-java-applications"></a>Debugowanie aplikacji Java sieci szkieletowej usług

W przypadku aplikacji Java [wiele platform rejestrowania](http://en.wikipedia.org/wiki/Java_logging_framework) są dostępne. Ponieważ `java.util.logging` jest opcja domyślna hello z hello środowiska JRE, jest również używana dla hello [przykładów kodu w witrynie github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  Hello następujące dyskusji wyjaśniono, jak tooconfigure hello `java.util.logging` framework.

Przy użyciu aplikacji można przekierowywać java.util.logging rejestruje toomemory, strumienie wyjściowe, pliki konsoli lub gniazda. Dla każdej z tych opcji są już udostępniane w ramach hello obsługi domyślne. Można utworzyć `app.properties` obsługi plików hello tooconfigure pliku dla twojej aplikacji tooredirect wszystkie dzienniki tooa pliku lokalnego.

Witaj następującego fragmentu kodu zawiera przykładową konfigurację:

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

Witaj Witaj tooby wskazywany folder `app.properties` plik musi istnieć. Po hello `app.properties` plik jest tworzony, należy tooalso zmodyfikować skrypt punktu wejścia `entrypoint.sh` w hello `<applicationfolder>/<servicePkg>/Code/` folderu tooset hello właściwości `java.util.logging.config.file` zbyt`app.propertes` pliku. wpis Hello powinna wyglądać powitania po fragment kodu:

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


Ta konfiguracja powoduje dzienniki są zbierane w sposób obracania w `/tmp/servicefabric/logs/`. w takim przypadku Hello plik dziennika ma nazwę mysfapp%u.%g.log gdzie:
* **%u** jest unikatowy tooresolve numer konfliktów między równoczesnych procesów Java.
* **%g** jest hello generowania numerów toodistinguish między obracanie dzienników.

Domyślnie jeśli jawnie jest skonfigurowany bez obsługi, program obsługi konsoli hello jest zarejestrowany. Jeden hello dzienniki można wyświetlać w syslog w obszarze /var/log/syslog.

Aby uzyskać więcej informacji, zobacz hello [przykładów kodu w witrynie github](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Debugowanie aplikacji usługi sieci szkieletowej C#


Wiele platform są dostępne dla śledzenia środowisko CoreCLR aplikacji w systemie Linux. Aby uzyskać więcej informacji, zobacz [GitHub: rejestrowanie](http:/github.com/aspnet/logging).  Ponieważ EventSource znanych tooC # deweloperów "w tym artykule wykorzystano źródła zdarzeń śledzenia w środowisko CoreCLR próbek w systemie Linux.

pierwszym krokiem Hello jest tooinclude System.Diagnostics.Tracing, aby mogły zapisywać Twoje toomemory dzienniki, strumienie wyjściowe lub pliki konsoli.  Do rejestrowania przy użyciu elementu EventSource, Dodaj powitania po project.json tooyour projektu:

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

Można użyć niestandardowych toolisten odbiornika zdarzeń dla zdarzenia usługi hello i następnie odpowiednio przekierować je tootrace plików. Witaj poniższy fragment kodu przedstawia przykładowe zastosowanie rejestrowania przy użyciu źródła zdarzeń i niestandardowych odbiornika zdarzeń:


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


Hello poprzedniego fragment danych wyjściowych pliku tooa dzienniki hello w `/tmp/MyServiceLog.txt`. Ta nazwa pliku musi toobe odpowiednio aktualizowane. W przypadku, gdy chcesz tooredirect hello dzienniki tooconsole, użyj hello następującego fragmentu kodu w klasie odbiornika zdarzeń niestandardowych:

```csharp
public static TextWriter Out = Console.Out;
```

Witaj próbek w [przykłady dotyczące języka C#](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) EventSource i niestandardowego pliku tooa zdarzenia toolog odbiornika danych.



## <a name="next-steps"></a>Następne kroki
Witaj sam kod śledzenia dodane tooyour aplikacji współdziała również z hello diagnostyki aplikacji w klastrze platformy Azure. Wyewidencjonowanie te artykuły omówiono w nim różne opcje narzędzia hello hello i opisujących sposób tooset je.
* [Sposób rejestrowania toocollect Diagnostyka Azure](service-fabric-diagnostics-how-to-setup-lad.md)
