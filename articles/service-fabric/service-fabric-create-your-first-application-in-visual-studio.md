---
title: "aaaCreate niezawodnej usługi sieć szkieletowa usług Azure języku C#"
description: "Twórz, wdrażaj i debuguj aplikację niezawodnej usługi skompilowaną w usłudze Azure Service Fabric przy użyciu programu Visual Studio."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>Tworzenie pierwszej aplikacji niezawodnych usług stanowych w usłudze Service Fabric w języku C#

Dowiedz się, jak toodeploy swoją pierwszą aplikację usługi sieć szkieletowa usług dla platformy .NET w systemie Windows w ciągu kilku minut. Po zakończeniu będziesz mieć lokalny klaster z uruchomioną aplikacją niezawodnej usługi.

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem upewnij się, że masz [skonfigurowane środowisko programowania](service-fabric-get-started.md). Dotyczy to również instalowanie hello zestawu SDK usług sieci szkieletowej i Visual Studio 2017 lub 2015.

## <a name="create-hello-application"></a>Tworzenie aplikacji hello

Uruchom program Visual Studio jako **administrator**.

Tworzenie projektu przy użyciu klawiszy `CTRL`+`SHIFT`+`N`

W hello **nowy projekt** okno dialogowe, wybierz **chmury > aplikacji sieci szkieletowej usług**.

Nadaj nazwę aplikacji hello **MyApplication** i naciśnij klawisz **OK**.

   
![Okno dialogowe nowego projektu w programie Visual Studio][1]

Można utworzyć dowolnego typu aplikacji usługi Service Fabric z hello następnego okna dialogowego. Na potrzeby tego przewodnika Szybki start wybierz pozycję **Usługa stanowa**.

Nazwa usługi hello **MyStatefulService** i naciśnij klawisz **OK**.

![Okno dialogowe nowej usługi w programie Visual Studio][2]


Visual Studio tworzy projekt aplikacji hello i projekt usługi stanowej hello i wyświetla je w Eksploratorze rozwiązań.

![Eksplorator rozwiązań po utworzeniu aplikacji z usługą stanową][3]

Projekt aplikacji Hello (**MyApplication**) nie zawiera żadnego kodu bezpośrednio. Zamiast tego odwołuje się do zestawu projektów usług. Ponadto zawiera trzy inne typy zawartości:

* **Profile publikowania**  
Profile wdrażania środowisk toodifferent.

* **Skrypty**  
Skrypt programu PowerShell przeznaczony do wdrażania/uaktualniania aplikacji.

* **Definicja aplikacji**  
Obejmuje hello pliku ApplicationManifest.xml *ApplicationPackageRoot* która opisuje kompozycji aplikacji. Pliki parametru skojarzonej aplikacji znajdują się w obszarze *ApplicationParameters*, które mogą być używane toospecify parametry określonego środowiska. Visual Studio wybiera, skojarzony plik parametrów aplikacji określonego w hello profilu publikowania podczas wdrażania tooa w danym środowisku.
    
Omówienie hello zawartości projektu usługi hello, zobacz [Rozpoczynanie pracy z usługami Reliable Services](service-fabric-reliable-services-quick-start.md).

## <a name="deploy-and-debug-hello-application"></a>Wdrażanie i debugowanie aplikacji hello

Teraz, gdy masz już aplikację, uruchom ją.

W programie Visual Studio, naciśnij klawisz `F5` toodeploy hello aplikację do debugowania.

>[!NOTE]
>Witaj pierwszego uruchomienia i wdrażanie aplikacji hello lokalnie, Visual Studio tworzy lokalny klaster na potrzeby debugowania. Może to potrwać jakiś czas. Stan tworzenia klastra Hello jest wyświetlany w oknie danych wyjściowych programu Visual Studio hello.

Gdy klaster hello jest gotowy, można uzyskać powiadomienie od hello klastra lokalnego aplikacji Menedżera paska zadań dołączonego hello zestawu SDK.
   
![Powiadomienie klastra lokalnego na pasku zadań][4]

Po uruchomieniu aplikacji hello, Visual Studio automatycznie wywołuje hello **podglądu zdarzeń diagnostycznych**, w którym można zobaczyć wyniki śledzenia z usług.
   
![Podgląd zdarzeń diagnostycznych][5]

Witaj szablonu usługi stanowej użyliśmy po prostu zawiera wartość licznika w hello zwiększanie `RunAsync` metody **pliku MyStatefulService.cs**.

Rozwiń jeden toosee zdarzenia hello więcej szczegółów, w tym węzeł hello którym wykonywany jest kod hello. W tym przypadku jest to węzeł \_Node\_2, ale może się to różnić w zależności od maszyny.
   
![Szczegóły w podglądzie zdarzeń diagnostycznych][6]

Witaj klaster lokalny zawiera pięć węzłów hostowanych na jednym komputerze. W środowisku produkcyjnym każdy węzeł jest hostowany na odrębnej maszynie fizycznej lub wirtualnej. toosimulate hello utratę maszyny podczas wykonywania hello Visual Studio debugera na powitania sam raz, wyłączmy jeden hello węzłów w klastrze lokalnym hello.

W hello **Eksploratora rozwiązań** okna, otwórz **pliku MyStatefulService.cs**. 

Znajdź hello `RunAsync` — metoda i ustaw punkt przerwania hello w pierwszym wierszu metody hello.

![Punkt przerwania w metodzie RunAsync usługi stanowej][7]

Uruchamianie hello **Service Fabric Explorer** narzędzia, klikając prawym przyciskiem myszy na powitania **Menedżera klastra lokalnego** aplikacji na pasku zadań systemu i wybierz polecenie **Zarządzaj klastrem lokalnym**.

![Uruchom Eksploratora usługi sieć szkieletowa z hello Menedżera klastra lokalnego][systray-launch-sfx]

Narzędzie [**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) oferuje wizualną reprezentację klastra. Zawiera zestaw hello tooit aplikacje wdrożone i hello zestaw węzłów fizycznych, które go tworzą.

W okienku po lewej stronie powitania rozwiń **klaster > węzły** i Znajdź hello węzła, gdy wykonywany jest kod.

Kliknij przycisk **Akcje > Dezaktywuj (ponowne uruchomienie)** toosimulate ponowne uruchomienie maszyny.

![Zatrzymanie węzła w narzędziu Service Fabric Explorer][sfx-stop-node]

Chwilowo powinien zostać wyświetlony punkt przerwania osiągane w programie Visual Studio w hello obliczenia wykonywane w jednym węźle bezproblemowo awaryjnie tooanother.


Następnie wróć toohello podglądu zdarzeń diagnostycznych i obserwować wiadomości powitania. Witaj licznika nadal wzrastała, mimo że zdarzenia hello faktycznie pochodzą z innego węzła.

![Szczegóły w podglądzie zdarzeń diagnostycznych po przełączeniu do trybu failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>Czyszczenie hello klaster lokalny (opcjonalnie)

Pamiętaj, że ten klaster lokalny to klaster rzeczywisty. Zatrzymanie debugera hello usuwa wystąpienie aplikacji i wyrejestrowuje typ aplikacji hello. Jednak hello klaster nadal toorun w tle hello. Jeśli wszystko jest gotowe toostop hello lokalnym klastrem, dostępnych jest kilka opcji.

### <a name="keep-application-and-trace-data"></a>Przechowywanie danych aplikacji i śledzenia

Zamknij hello klastra, klikając prawym przyciskiem myszy na powitania **Menedżera klastra lokalnego** aplikacji na pasku zadań systemu, a następnie wybierz **Zatrzymaj klaster lokalny**.

### <a name="delete-hello-cluster-and-all-data"></a>Usuwanie klastra hello i wszystkich danych

Usuń klaster hello klikając prawym przyciskiem myszy na powitania **Menedżera klastra lokalnego** aplikacji na pasku zadań systemu, a następnie wybierz **Usuń klaster lokalny**. 

Jeśli wybierzesz tę opcję, Visual Studio będzie ponownie wdrożyć hello klastra hello następnym razem z Uruchom hello aplikacji. Wybierz tę opcję, jeśli nie chcesz klastra lokalnego hello toouse przez pewien czas lub jeśli potrzebujesz tooreclaim zasobów.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o [niezawodnych usługach](service-fabric-reliable-services-introduction.md).
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
