---
title: "aaaDebug mikrousług Azure w systemie Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomonitor i diagnozowania usług napisane przy użyciu usługi sieć szkieletowa usług Microsoft Azure na maszynie lokalnej."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: edcc0631-ed2d-45a3-851d-2c4fa0f4a326
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/24/2017
ms.author: dekapur
ms.openlocfilehash: 24868aa194b8a28fa3e6de95c1de5506d912a544
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

Monitorowanie, wykrywanie, diagnozowanie i rozwiązywanie problemów z umożliwiają toocontinue usług z minimalnym przerw w działaniu toohello użytkowników. Podczas monitorowania i diagnostyki są szczególnie ważne w środowisku produkcyjnym wdrożony rzeczywisty, hello wydajność będzie zależeć od przyjęcia podobne modelu podczas tworzenia usługi tooensure, działają podczas przenoszenia instalacji rzeczywistych tooa. Sieć szkieletowa usług ułatwia diagnostyki tooimplement deweloperów usługi może bezproblemowo współpracować na konfiguracje pojedynczego komputera lokalnego rozwoju i w konfiguracji klastra produkcyjnego rzeczywistych.

## <a name="event-tracing-for-windows"></a>Śledzenie zdarzeń systemu Windows
[Śledzenie zdarzeń systemu Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803.aspx) (ETW) jest hello zalecane technologii śledzenie wiadomości w sieci szkieletowej usług. Niektóre zalety używania funkcji ETW są:

* **ETW jest szybkie.** Został skonstruowany jako technologia śledzenia, która ma minimalny wpływ na czas wykonywania kodu.
* **Śledzenie zdarzeń systemu Windows współdziała między środowisk deweloperskich lokalne, a także konfiguracje klastra rzeczywistych.** Oznacza to, że nie masz toorewrite Twojego śledzenia kodu po osiągnięciu gotowości toodeploy klastra rzeczywistych tooa kodu.
* **Kod systemu sieci szkieletowej usług używa również ETW śledzenia wewnętrznego.** Dzięki temu tooview przeplatana śladów aplikacji z usługi sieć szkieletowa systemu śledzenia. Pomaga również toomore łatwo zrozumieć hello sekwencji i wzajemne relacje między kodem aplikacji i zdarzeń w podstawowym systemie hello.
* **Zdarzenia ETW tooview jest wbudowana obsługa w narzędzia Service Fabric Visual Studio.** Zdarzenia ETW są wyświetlane w hello widoku zdarzeń diagnostycznych programu Visual Studio po Visual Studio jest poprawnie skonfigurowane z sieci szkieletowej usług. 

## <a name="view-service-fabric-system-events-in-visual-studio"></a>Wyświetl zdarzenia systemowe platformy Service Fabric w programie Visual Studio
Sieć szkieletowa usług emituje deweloperzy aplikacji toohelp zorientować się w platformę hello zdarzenia ETW. Jeśli jeszcze tego nie zrobiono, przejdź dalej i wykonaj kroki hello w [tworzenie pierwszej aplikacji w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md). Informacje te pomogą uzyskać z aplikacji działa z hello przedstawiający hello komunikatów śledzenia w Podglądzie zdarzeń diagnostycznych.

1. W przypadku diagnostyki hello okna zdarzeń nie są automatycznie wyświetlane, toohello **widoku** w programie Visual Studio, wybierz pozycję **inne okna** , a następnie **podglądu zdarzeń diagnostycznych**.
2. Każde zdarzenie zawiera informacje standardowe metadanych, które informuje, że pochodzą ze zdarzeń hello hello węzła, aplikacji i usług. Można również filtrować hello listę zdarzeń za pomocą hello **filtrować zdarzenia** pole u góry okna zdarzeń hello hello. Na przykład można filtrować na **nazwa węzła** lub **nazwy usługi.** I podczas przeglądania szczegóły zdarzenia, można również wstrzymać przy użyciu hello **wstrzymać** znajdujący się u góry okna zdarzeń hello hello i wznowić później, bez utraty zdarzeń.
   
   ![W Podglądzie zdarzeń diagnostycznych programu Visual Studio](./media/service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally/DiagEventsExamples2.png)

## <a name="add-your-own-custom-traces-toohello-application-code"></a>Dodaj kod aplikacji toohello własne niestandardowe dane śledzenia
Szablony projektu Visual Studio sieci szkieletowej usług Hello zawiera przykładowy kod. Witaj kod przedstawia, jak kod aplikacji niestandardowej tooadd ETW śledzi przedstawiające się w podglądzie programu Visual Studio ETW hello obok śledzenia systemu z sieci szkieletowej usług. Witaj zaletą tej metody jest metadanych jest automatycznie dodawany tootraces, czy hello Visual Studio diagnostycznych Podgląd zdarzeń jest już skonfigurowana toodisplay je.

Dla projektów utworzone na podstawie hello **szablony usługi** (bezstanowych lub stateful) po prostu wyszukaj hello `RunAsync` implementacji:

1. Witaj wywołanie za`ServiceEventSource.Current.ServiceMessage` w hello `RunAsync` metody przedstawiono przykład niestandardowych śledzenia funkcji ETW z kodu aplikacji hello.
2. W hello **ServiceEventSource.cs** plików, można znaleźć przeciążenia dla hello `ServiceEventSource.ServiceMessage` metody, które mają być używane dla zdarzeń o dużej częstotliwości powodu tooperformance powodów.

Dla projektów utworzone na podstawie hello **szablony aktora** (bezstanowych lub stateful):

1. Otwórz hello **.cs "ProjectName"** pliku where *ProjectName* jest nazwą hello wybrany dla projektu programu Visual Studio.  
2. Znajdź kod hello `ActorEventSource.Current.ActorMessage(this, "Doing Work");` w hello *DoWorkAsync* metody.  To jest przykład niestandardowych śledzenia funkcji ETW z kodu aplikacji.  
3. W pliku **ActorEventSource.cs**, znajdują się przeciążenia hello `ActorEventSource.ActorMessage` metody, które mają być używane dla zdarzeń o dużej częstotliwości powodu tooperformance powodów.

Po dodaniu niestandardowych ETW tracing tooyour kodu usługi, można tworzenie, wdrażanie i uruchamianie aplikacji hello ponownie toosee Twojego zdarzenia w hello podglądu zdarzeń diagnostycznych. Jeśli debugowanie aplikacji hello z **F5**, hello zostanie otwarty w Podglądzie zdarzeń diagnostycznych.

## <a name="next-steps"></a>Następne kroki
Hello sam kod śledzenia, dodania aplikacji tooyour powyżej Diagnostics lokalnej będzie działać z narzędzia, których można używać tooview te zdarzenia, podczas uruchamiania aplikacji w klastrze platformy Azure. Zapoznaj się z tych artykułów, omówiono w nim różne opcje narzędzia hello hello i opisujące, jak można skonfigurować je.

* [Sposób rejestrowania toocollect Diagnostyka Azure](service-fabric-diagnostics-how-to-setup-wad.md)
* [Agregacja zdarzeń i kolekcji przy użyciu EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md)

