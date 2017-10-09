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
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a><span data-ttu-id="1743e-103">Tworzenie pierwszej aplikacji niezawodnych usług stanowych w usłudze Service Fabric w języku C#</span><span class="sxs-lookup"><span data-stu-id="1743e-103">Create your first C# Service Fabric stateful reliable services application</span></span>

<span data-ttu-id="1743e-104">Dowiedz się, jak toodeploy swoją pierwszą aplikację usługi sieć szkieletowa usług dla platformy .NET w systemie Windows w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="1743e-104">Learn how toodeploy your first Service Fabric application for .NET on Windows in just a few minutes.</span></span> <span data-ttu-id="1743e-105">Po zakończeniu będziesz mieć lokalny klaster z uruchomioną aplikacją niezawodnej usługi.</span><span class="sxs-lookup"><span data-stu-id="1743e-105">When you're finished, you'll have a local cluster running with a reliable service application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1743e-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1743e-106">Prerequisites</span></span>

<span data-ttu-id="1743e-107">Przed rozpoczęciem upewnij się, że masz [skonfigurowane środowisko programowania](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1743e-107">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="1743e-108">Dotyczy to również instalowanie hello zestawu SDK usług sieci szkieletowej i Visual Studio 2017 lub 2015.</span><span class="sxs-lookup"><span data-stu-id="1743e-108">This includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="1743e-109">Tworzenie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="1743e-109">Create hello application</span></span>

<span data-ttu-id="1743e-110">Uruchom program Visual Studio jako **administrator**.</span><span class="sxs-lookup"><span data-stu-id="1743e-110">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="1743e-111">Tworzenie projektu przy użyciu klawiszy `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="1743e-111">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="1743e-112">W hello **nowy projekt** okno dialogowe, wybierz **chmury > aplikacji sieci szkieletowej usług**.</span><span class="sxs-lookup"><span data-stu-id="1743e-112">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="1743e-113">Nadaj nazwę aplikacji hello **MyApplication** i naciśnij klawisz **OK**.</span><span class="sxs-lookup"><span data-stu-id="1743e-113">Name hello application **MyApplication** and press **OK**.</span></span>

   
![Okno dialogowe nowego projektu w programie Visual Studio][1]

<span data-ttu-id="1743e-115">Można utworzyć dowolnego typu aplikacji usługi Service Fabric z hello następnego okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1743e-115">You can create any type of Service Fabric application from hello next dialog.</span></span> <span data-ttu-id="1743e-116">Na potrzeby tego przewodnika Szybki start wybierz pozycję **Usługa stanowa**.</span><span class="sxs-lookup"><span data-stu-id="1743e-116">For this Quickstart, choose **Stateful Service**.</span></span>

<span data-ttu-id="1743e-117">Nazwa usługi hello **MyStatefulService** i naciśnij klawisz **OK**.</span><span class="sxs-lookup"><span data-stu-id="1743e-117">Name hello service **MyStatefulService** and press **OK**.</span></span>

![Okno dialogowe nowej usługi w programie Visual Studio][2]


<span data-ttu-id="1743e-119">Visual Studio tworzy projekt aplikacji hello i projekt usługi stanowej hello i wyświetla je w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="1743e-119">Visual Studio creates hello application project and hello stateful service project and displays them in Solution Explorer.</span></span>

![Eksplorator rozwiązań po utworzeniu aplikacji z usługą stanową][3]

<span data-ttu-id="1743e-121">Projekt aplikacji Hello (**MyApplication**) nie zawiera żadnego kodu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1743e-121">hello application project (**MyApplication**) does not contain any code directly.</span></span> <span data-ttu-id="1743e-122">Zamiast tego odwołuje się do zestawu projektów usług.</span><span class="sxs-lookup"><span data-stu-id="1743e-122">Instead, it references a set of service projects.</span></span> <span data-ttu-id="1743e-123">Ponadto zawiera trzy inne typy zawartości:</span><span class="sxs-lookup"><span data-stu-id="1743e-123">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="1743e-124">**Profile publikowania**</span><span class="sxs-lookup"><span data-stu-id="1743e-124">**Publish profiles**</span></span>  
<span data-ttu-id="1743e-125">Profile wdrażania środowisk toodifferent.</span><span class="sxs-lookup"><span data-stu-id="1743e-125">Profiles for deploying toodifferent environments.</span></span>

* <span data-ttu-id="1743e-126">**Skrypty**</span><span class="sxs-lookup"><span data-stu-id="1743e-126">**Scripts**</span></span>  
<span data-ttu-id="1743e-127">Skrypt programu PowerShell przeznaczony do wdrażania/uaktualniania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1743e-127">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="1743e-128">**Definicja aplikacji**</span><span class="sxs-lookup"><span data-stu-id="1743e-128">**Application definition**</span></span>  
<span data-ttu-id="1743e-129">Obejmuje hello pliku ApplicationManifest.xml *ApplicationPackageRoot* która opisuje kompozycji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1743e-129">Includes hello ApplicationManifest.xml file under *ApplicationPackageRoot* which describes your application's composition.</span></span> <span data-ttu-id="1743e-130">Pliki parametru skojarzonej aplikacji znajdują się w obszarze *ApplicationParameters*, które mogą być używane toospecify parametry określonego środowiska.</span><span class="sxs-lookup"><span data-stu-id="1743e-130">Associated application parameter files are under *ApplicationParameters*, which can be used toospecify environment-specific parameters.</span></span> <span data-ttu-id="1743e-131">Visual Studio wybiera, skojarzony plik parametrów aplikacji określonego w hello profilu publikowania podczas wdrażania tooa w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="1743e-131">Visual Studio selects an application parameter file that's specified in hello associated publish profile during deployment tooa specific environment.</span></span>
    
<span data-ttu-id="1743e-132">Omówienie hello zawartości projektu usługi hello, zobacz [Rozpoczynanie pracy z usługami Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="1743e-132">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="deploy-and-debug-hello-application"></a><span data-ttu-id="1743e-133">Wdrażanie i debugowanie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="1743e-133">Deploy and debug hello application</span></span>

<span data-ttu-id="1743e-134">Teraz, gdy masz już aplikację, uruchom ją.</span><span class="sxs-lookup"><span data-stu-id="1743e-134">Now that you have an application, run it.</span></span>

<span data-ttu-id="1743e-135">W programie Visual Studio, naciśnij klawisz `F5` toodeploy hello aplikację do debugowania.</span><span class="sxs-lookup"><span data-stu-id="1743e-135">In Visual Studio, press `F5` toodeploy hello application for debugging.</span></span>

>[!NOTE]
><span data-ttu-id="1743e-136">Witaj pierwszego uruchomienia i wdrażanie aplikacji hello lokalnie, Visual Studio tworzy lokalny klaster na potrzeby debugowania.</span><span class="sxs-lookup"><span data-stu-id="1743e-136">hello first time you run and deploy hello application locally, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="1743e-137">Może to potrwać jakiś czas.</span><span class="sxs-lookup"><span data-stu-id="1743e-137">This may take some time.</span></span> <span data-ttu-id="1743e-138">Stan tworzenia klastra Hello jest wyświetlany w oknie danych wyjściowych programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="1743e-138">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="1743e-139">Gdy klaster hello jest gotowy, można uzyskać powiadomienie od hello klastra lokalnego aplikacji Menedżera paska zadań dołączonego hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="1743e-139">When hello cluster is ready, you get a notification from hello local cluster system tray manager application included with hello SDK.</span></span>
   
![Powiadomienie klastra lokalnego na pasku zadań][4]

<span data-ttu-id="1743e-141">Po uruchomieniu aplikacji hello, Visual Studio automatycznie wywołuje hello **podglądu zdarzeń diagnostycznych**, w którym można zobaczyć wyniki śledzenia z usług.</span><span class="sxs-lookup"><span data-stu-id="1743e-141">Once hello application starts, Visual Studio automatically brings up hello **Diagnostics Event Viewer**, where you can see trace output from your services.</span></span>
   
![Podgląd zdarzeń diagnostycznych][5]

<span data-ttu-id="1743e-143">Witaj szablonu usługi stanowej użyliśmy po prostu zawiera wartość licznika w hello zwiększanie `RunAsync` metody **pliku MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="1743e-143">hello stateful service template we used simply shows a counter value incrementing in hello `RunAsync` method of **MyStatefulService.cs**.</span></span>

<span data-ttu-id="1743e-144">Rozwiń jeden toosee zdarzenia hello więcej szczegółów, w tym węzeł hello którym wykonywany jest kod hello.</span><span class="sxs-lookup"><span data-stu-id="1743e-144">Expand one of hello events toosee more details, including hello node where hello code is running.</span></span> <span data-ttu-id="1743e-145">W tym przypadku jest to węzeł \_Node\_2, ale może się to różnić w zależności od maszyny.</span><span class="sxs-lookup"><span data-stu-id="1743e-145">In this case, it is \_Node\_2, though it may differ on your machine.</span></span>
   
![Szczegóły w podglądzie zdarzeń diagnostycznych][6]

<span data-ttu-id="1743e-147">Witaj klaster lokalny zawiera pięć węzłów hostowanych na jednym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1743e-147">hello local cluster contains five nodes hosted on a single machine.</span></span> <span data-ttu-id="1743e-148">W środowisku produkcyjnym każdy węzeł jest hostowany na odrębnej maszynie fizycznej lub wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1743e-148">In a production environment, each node is hosted on a distinct physical or virtual machine.</span></span> <span data-ttu-id="1743e-149">toosimulate hello utratę maszyny podczas wykonywania hello Visual Studio debugera na powitania sam raz, wyłączmy jeden hello węzłów w klastrze lokalnym hello.</span><span class="sxs-lookup"><span data-stu-id="1743e-149">toosimulate hello loss of a machine while exercising hello Visual Studio debugger at hello same time, let's take down one of hello nodes on hello local cluster.</span></span>

<span data-ttu-id="1743e-150">W hello **Eksploratora rozwiązań** okna, otwórz **pliku MyStatefulService.cs**.</span><span class="sxs-lookup"><span data-stu-id="1743e-150">In hello **Solution Explorer** window, open **MyStatefulService.cs**.</span></span> 

<span data-ttu-id="1743e-151">Znajdź hello `RunAsync` — metoda i ustaw punkt przerwania hello w pierwszym wierszu metody hello.</span><span class="sxs-lookup"><span data-stu-id="1743e-151">Find hello `RunAsync` method and set a breakpoint on hello first line of hello method.</span></span>

![Punkt przerwania w metodzie RunAsync usługi stanowej][7]

<span data-ttu-id="1743e-153">Uruchamianie hello **Service Fabric Explorer** narzędzia, klikając prawym przyciskiem myszy na powitania **Menedżera klastra lokalnego** aplikacji na pasku zadań systemu i wybierz polecenie **Zarządzaj klastrem lokalnym**.</span><span class="sxs-lookup"><span data-stu-id="1743e-153">Launch hello **Service Fabric Explorer** tool by right-clicking on hello **Local Cluster Manager** system tray application and choose **Manage Local Cluster**.</span></span>

![Uruchom Eksploratora usługi sieć szkieletowa z hello Menedżera klastra lokalnego][systray-launch-sfx]

<span data-ttu-id="1743e-155">Narzędzie [**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) oferuje wizualną reprezentację klastra.</span><span class="sxs-lookup"><span data-stu-id="1743e-155">[**Service Fabric Explorer**](service-fabric-visualizing-your-cluster.md) offers a visual representation of a cluster.</span></span> <span data-ttu-id="1743e-156">Zawiera zestaw hello tooit aplikacje wdrożone i hello zestaw węzłów fizycznych, które go tworzą.</span><span class="sxs-lookup"><span data-stu-id="1743e-156">It includes hello set of applications deployed tooit and hello set of physical nodes that make it up.</span></span>

<span data-ttu-id="1743e-157">W okienku po lewej stronie powitania rozwiń **klaster > węzły** i Znajdź hello węzła, gdy wykonywany jest kod.</span><span class="sxs-lookup"><span data-stu-id="1743e-157">In hello left pane, expand **Cluster > Nodes** and find hello node where your code is running.</span></span>

<span data-ttu-id="1743e-158">Kliknij przycisk **Akcje > Dezaktywuj (ponowne uruchomienie)** toosimulate ponowne uruchomienie maszyny.</span><span class="sxs-lookup"><span data-stu-id="1743e-158">Click **Actions > Deactivate (Restart)** toosimulate a machine restarting.</span></span>

![Zatrzymanie węzła w narzędziu Service Fabric Explorer][sfx-stop-node]

<span data-ttu-id="1743e-160">Chwilowo powinien zostać wyświetlony punkt przerwania osiągane w programie Visual Studio w hello obliczenia wykonywane w jednym węźle bezproblemowo awaryjnie tooanother.</span><span class="sxs-lookup"><span data-stu-id="1743e-160">Momentarily, you should see your breakpoint hit in Visual Studio as hello computation you were doing on one node seamlessly fails over tooanother.</span></span>


<span data-ttu-id="1743e-161">Następnie wróć toohello podglądu zdarzeń diagnostycznych i obserwować wiadomości powitania.</span><span class="sxs-lookup"><span data-stu-id="1743e-161">Next, return toohello Diagnostic Events Viewer and observe hello messages.</span></span> <span data-ttu-id="1743e-162">Witaj licznika nadal wzrastała, mimo że zdarzenia hello faktycznie pochodzą z innego węzła.</span><span class="sxs-lookup"><span data-stu-id="1743e-162">hello counter has continued incrementing, even though hello events are actually coming from a different node.</span></span>

![Szczegóły w podglądzie zdarzeń diagnostycznych po przełączeniu do trybu failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a><span data-ttu-id="1743e-164">Czyszczenie hello klaster lokalny (opcjonalnie)</span><span class="sxs-lookup"><span data-stu-id="1743e-164">Cleaning up hello local cluster (optional)</span></span>

<span data-ttu-id="1743e-165">Pamiętaj, że ten klaster lokalny to klaster rzeczywisty.</span><span class="sxs-lookup"><span data-stu-id="1743e-165">Remember, this local cluster is real.</span></span> <span data-ttu-id="1743e-166">Zatrzymanie debugera hello usuwa wystąpienie aplikacji i wyrejestrowuje typ aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1743e-166">Stopping hello debugger removes your application instance and unregisters hello application type.</span></span> <span data-ttu-id="1743e-167">Jednak hello klaster nadal toorun w tle hello.</span><span class="sxs-lookup"><span data-stu-id="1743e-167">However, hello cluster continues toorun in hello background.</span></span> <span data-ttu-id="1743e-168">Jeśli wszystko jest gotowe toostop hello lokalnym klastrem, dostępnych jest kilka opcji.</span><span class="sxs-lookup"><span data-stu-id="1743e-168">When you're ready toostop hello local cluster, there are a couple options.</span></span>

### <a name="keep-application-and-trace-data"></a><span data-ttu-id="1743e-169">Przechowywanie danych aplikacji i śledzenia</span><span class="sxs-lookup"><span data-stu-id="1743e-169">Keep application and trace data</span></span>

<span data-ttu-id="1743e-170">Zamknij hello klastra, klikając prawym przyciskiem myszy na powitania **Menedżera klastra lokalnego** aplikacji na pasku zadań systemu, a następnie wybierz **Zatrzymaj klaster lokalny**.</span><span class="sxs-lookup"><span data-stu-id="1743e-170">Shut down hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Stop Local Cluster**.</span></span>

### <a name="delete-hello-cluster-and-all-data"></a><span data-ttu-id="1743e-171">Usuwanie klastra hello i wszystkich danych</span><span class="sxs-lookup"><span data-stu-id="1743e-171">Delete hello cluster and all data</span></span>

<span data-ttu-id="1743e-172">Usuń klaster hello klikając prawym przyciskiem myszy na powitania **Menedżera klastra lokalnego** aplikacji na pasku zadań systemu, a następnie wybierz **Usuń klaster lokalny**.</span><span class="sxs-lookup"><span data-stu-id="1743e-172">Remove hello cluster by right-clicking on hello **Local Cluster Manager** system tray application and then choose **Remove Local Cluster**.</span></span> 

<span data-ttu-id="1743e-173">Jeśli wybierzesz tę opcję, Visual Studio będzie ponownie wdrożyć hello klastra hello następnym razem z Uruchom hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1743e-173">If you choose this option, Visual Studio will redeploy hello cluster hello next time your run hello application.</span></span> <span data-ttu-id="1743e-174">Wybierz tę opcję, jeśli nie chcesz klastra lokalnego hello toouse przez pewien czas lub jeśli potrzebujesz tooreclaim zasobów.</span><span class="sxs-lookup"><span data-stu-id="1743e-174">Choose this option if you don't intend toouse hello local cluster for some time or if you need tooreclaim resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1743e-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1743e-175">Next steps</span></span>
<span data-ttu-id="1743e-176">Dowiedz się więcej o [niezawodnych usługach](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1743e-176">Read more about [reliable services](service-fabric-reliable-services-introduction.md).</span></span>
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
