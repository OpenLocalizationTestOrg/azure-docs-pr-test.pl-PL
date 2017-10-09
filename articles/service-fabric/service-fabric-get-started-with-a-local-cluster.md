---
title: "aaaDeploy i uaktualnić Azure mikrousług lokalnie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wdrożyć istniejących tooit aplikacji tooset instalacji klastra lokalnego sieci szkieletowej usług, a następnie Uaktualnianie tej aplikacji."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="c397a-103">Pierwsze kroki wdrażania i aktualizowania aplikacji w klastrze lokalnym</span><span class="sxs-lookup"><span data-stu-id="c397a-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="c397a-104">Hello zestawu SDK usługi Azure Service Fabric zawiera pełne lokalne środowisko, którego można używać tooquickly wprowadzenie do wdrażania aplikacji i zarządzanie nimi w klastrze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="c397a-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="c397a-105">W tym artykule możesz utworzyć klaster lokalny, wdrożyć istniejącą tooit aplikacji, a następnie Uaktualnij aplikacji tooa nowej wersji, wszystkie ze środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c397a-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="c397a-106">W tym artykule przyjęto, że czynności [konfigurowania środowiska deweloperskiego](service-fabric-get-started.md) zostały już ukończone.</span><span class="sxs-lookup"><span data-stu-id="c397a-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="c397a-107">Tworzenie klastra lokalnego</span><span class="sxs-lookup"><span data-stu-id="c397a-107">Create a local cluster</span></span>
<span data-ttu-id="c397a-108">Klaster usługi Service Fabric stanowi zestaw zasobów sprzętowych, w którym można wdrażać aplikacje.</span><span class="sxs-lookup"><span data-stu-id="c397a-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="c397a-109">Zazwyczaj klaster składa się z dowolnym z pięciu toomany tysięcy komputerów.</span><span class="sxs-lookup"><span data-stu-id="c397a-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="c397a-110">Jednak hello zestawu SDK usług sieci szkieletowej obejmuje konfigurację klastra, który można uruchomić na jednym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c397a-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="c397a-111">Jest ważne, czy toounderstand, który hello lokalnego klastra usługi sieć szkieletowa nie jest emulatorem ani symulatorem.</span><span class="sxs-lookup"><span data-stu-id="c397a-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="c397a-112">Go uruchamia hello sam kod platformy, która znajduje się w klastrach obejmujących wiele maszyn.</span><span class="sxs-lookup"><span data-stu-id="c397a-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="c397a-113">Witaj jedyna różnica polega na tym, że będzie ono przeprowadzane hello procesy platformowe, które standardowo są rozmieszczone na pięciu maszynach na jednej maszynie.</span><span class="sxs-lookup"><span data-stu-id="c397a-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="c397a-114">Hello SDK udostępnia dwa sposoby tooset instalacji klastra lokalnego: środowiska Windows PowerShell skrypt i hello Menedżera klastra lokalnego systemu na pasku aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c397a-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="c397a-115">W tym samouczku używamy skryptu programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="c397a-116">Jeśli utworzono już klaster lokalny poprzez wdrożenie aplikacji z programu Visual Studio, tę sekcję można pominąć.</span><span class="sxs-lookup"><span data-stu-id="c397a-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="c397a-117">Uruchom nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c397a-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="c397a-118">Uruchom skrypt instalacji klastra hello z folderu zestawu SDK hello:</span><span class="sxs-lookup"><span data-stu-id="c397a-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="c397a-119">Instalacja klastra trwa kilka chwil.</span><span class="sxs-lookup"><span data-stu-id="c397a-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="c397a-120">Po zakończeniu instalacji powinny być widoczne dane wyjściowe podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="c397a-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Dane wyjściowe instalacji klastra][cluster-setup-success]
   
    <span data-ttu-id="c397a-122">Wszystko jest teraz gotowy tootry wdrażanie klastra tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c397a-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="c397a-123">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="c397a-123">Deploy an application</span></span>
<span data-ttu-id="c397a-124">Hello zestaw SDK usługi Service Fabric zawiera bogaty zestaw struktur i narzędzi do tworzenia aplikacji programistycznych.</span><span class="sxs-lookup"><span data-stu-id="c397a-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="c397a-125">Jeśli interesuje Cię w uczeniu toocreate aplikacji w programie Visual Studio, zobacz temat [tworzenie pierwszej aplikacji platformy Service Fabric w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="c397a-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="c397a-126">W tym samouczku, można użyć istniejącej aplikacji przykładowej (o nazwie WordCount), dzięki czemu można skupić się na aspektach zarządzania hello platformy hello: wdrażanie, monitorowanie i uaktualnianie.</span><span class="sxs-lookup"><span data-stu-id="c397a-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="c397a-127">Uruchom nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c397a-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="c397a-128">Zaimportuj moduł programu PowerShell zestawu SDK sieci szkieletowej usług hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="c397a-129">Tworzenie aplikacji hello toostore katalogu, który można pobrać i wdrożyć, na przykład C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="c397a-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="c397a-130">[Pobierz aplikację WordCount hello](http://aka.ms/servicefabric-wordcountapp) toohello lokalizacji został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c397a-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="c397a-131">Uwaga: hello przeglądarki Microsoft Edge zapisuje plik hello o *.zip* rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="c397a-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="c397a-132">Zmień rozszerzenie pliku hello zbyt*.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="c397a-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="c397a-133">Połącz klaster lokalny toohello:</span><span class="sxs-lookup"><span data-stu-id="c397a-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="c397a-134">Utwórz nową aplikację za pomocą polecenia wdrażania hello SDK z nazwą i pakiet aplikacji toohello ścieżki.</span><span class="sxs-lookup"><span data-stu-id="c397a-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="c397a-135">Jeśli wszystko przebiegnie poprawnie, powinny być widoczne następujące dane wyjściowe hello:</span><span class="sxs-lookup"><span data-stu-id="c397a-135">If all goes well, you should see hello following output:</span></span>
   
    ![Wdrożenie klastra lokalnego toohello aplikacji][deploy-app-to-local-cluster]
7. <span data-ttu-id="c397a-137">Aplikacja hello toosee akcji, uruchom hello przeglądarki i przejdź zbyt[http://localhost: 8081/WordCount/index.HTML](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="c397a-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="c397a-138">Powinien zostać wyświetlony następujący ekran:</span><span class="sxs-lookup"><span data-stu-id="c397a-138">You should see:</span></span>
   
    ![Interfejs użytkownika wdrożonej aplikacji][deployed-app-ui]
   
    <span data-ttu-id="c397a-140">Witaj aplikacja WordCount jest proste.</span><span class="sxs-lookup"><span data-stu-id="c397a-140">hello WordCount application is simple.</span></span> <span data-ttu-id="c397a-141">Obejmuje on po stronie klienta JavaScript kodu toogenerate losowe pięć znaków "wyrazy", które są następnie przekazywane toohello aplikacji za pomocą interfejsu API sieci Web platformy ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="c397a-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="c397a-142">Usługa stanowa śledzi hello liczbę zliczonych słów.</span><span class="sxs-lookup"><span data-stu-id="c397a-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="c397a-143">Są one dzielone oparte na powitania pierwszego znaku słowa hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="c397a-144">Kod źródłowy hello można znaleźć aplikacji WordCount hello w hello [klasycznego wprowadzenie przykłady](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="c397a-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="c397a-145">Aplikacja Hello, którą wdrożyliśmy, zawiera cztery partycje.</span><span class="sxs-lookup"><span data-stu-id="c397a-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="c397a-146">Dlatego wyrazów rozpoczynających się od A do G są przechowywane w pierwszej partycji hello, wyrazów rozpoczynających się od H do N są przechowywane w hello drugiej partycji i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="c397a-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="c397a-147">Wyświetlanie szczegółów i stanu aplikacji</span><span class="sxs-lookup"><span data-stu-id="c397a-147">View application details and status</span></span>
<span data-ttu-id="c397a-148">Teraz, gdy wdrożyliśmy aplikacji hello, Przyjrzyjmy się niektóre szczegóły aplikacji hello w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c397a-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="c397a-149">Zapytanie wszystkich aplikacji wdrożonych w klastrze hello:</span><span class="sxs-lookup"><span data-stu-id="c397a-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="c397a-150">Przy założeniu, że została wdrożona tylko aplikacja WordCount hello, zobacz polecenie podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="c397a-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![Zapytanie dotyczące wszystkich wdrożonych aplikacji w powłoce PowerShell][ps-getsfapp]
2. <span data-ttu-id="c397a-152">Przejdź toohello następny poziom, badając hello zestawu usług zawartych w aplikacji WordCount hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lista usług dla aplikacji hello w programie PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="c397a-154">Aplikacja Hello składa się z dwóch usług, frontonu sieci web hello i hello usługi stanowej, która zarządza hello słów.</span><span class="sxs-lookup"><span data-stu-id="c397a-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="c397a-155">Na koniec przyjrzeć się hello listę partycji dla usługi WordCountService:</span><span class="sxs-lookup"><span data-stu-id="c397a-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Widok partycji usługi hello w programie PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="c397a-157">Witaj zestaw poleceń, których używasz, podobnie jak wszystkie polecenia programu PowerShell usługi Service Fabric, są dostępne dla dowolnego klastra, podłączoną do lokalnego lub zdalnego.</span><span class="sxs-lookup"><span data-stu-id="c397a-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="c397a-158">Bardziej wizualny toointeract sposób hello klastra, można użyć narzędzia Service Fabric Explorer opartych na sieci web hello przechodząc zbyt[http://localhost: 19080/Explorer](http://localhost:19080/Explorer) w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![Wyświetlanie szczegółów aplikacji w narzędziu Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="c397a-160">toolearn więcej informacji o narzędziu Service Fabric Explorer, zobacz [wizualizacja klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="c397a-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="c397a-161">Uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="c397a-161">Upgrade an application</span></span>
<span data-ttu-id="c397a-162">Usługa Service Fabric realizuje uaktualnienia bez przestojów przez monitorowanie kondycji hello aplikacji hello wdrażanej w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="c397a-163">Uaktualnienie hello aplikacji WordCount.</span><span class="sxs-lookup"><span data-stu-id="c397a-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="c397a-164">Witaj nowej wersji aplikacji hello teraz zlicza tylko słowa zaczynające się od samogłosek.</span><span class="sxs-lookup"><span data-stu-id="c397a-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="c397a-165">Jak uaktualnienie hello wprowadza, przedstawiono dwie zmiany w zachowaniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="c397a-166">Po pierwsze szybkość hello jaką zwiększania liczby hello powinna być mniejsza, ponieważ zliczane są mniej słów.</span><span class="sxs-lookup"><span data-stu-id="c397a-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="c397a-167">Po drugie ponieważ hello pierwszej partycji znajdują się dwie samogłoski (A i E), a wszystkie pozostałe partycje zawierają po jednej sylabie, licznika po pewnym czasie rozpocząć toooutpace hello innych.</span><span class="sxs-lookup"><span data-stu-id="c397a-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="c397a-168">[Pobierz pakiet w wersji 2 WordCount hello](http://aka.ms/servicefabric-wordcountappv2) toohello tej samej lokalizacji, w której pobrano pakiet w wersji 1 hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="c397a-169">Zwraca tooyour okno programu PowerShell i użyć hello SDK polecenia uaktualniania tooregister hello nową wersję w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="c397a-170">Następnie Rozpocznij uaktualnianie hello fabric: / WordCount aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c397a-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="c397a-171">Powinna zostać wyświetlona zaczyna hello następujące dane wyjściowe w programie PowerShell, ponieważ hello uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="c397a-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![Postęp uaktualniania w programie PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="c397a-173">Podczas uaktualniania hello może być łatwiejsze toomonitor stanu z Eksploratora usługi sieć szkieletowa.</span><span class="sxs-lookup"><span data-stu-id="c397a-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="c397a-174">Uruchom okno przeglądarki i przejdź zbyt[http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="c397a-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="c397a-175">Rozwiń węzeł **aplikacji** hello drzewa po lewej stronie powitania, następnie wybierz pozycję **WordCount**, a na końcu **sieci szkieletowej: / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="c397a-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="c397a-176">Na karcie essentials hello Zobacz stan hello hello uaktualnienia obejmującego domeny uaktualnienia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![Postęp uaktualniania w narzędziu Service Fabric Explorer][sfx-upgradeprogress]
   
    <span data-ttu-id="c397a-178">W trakcie wykonywania uaktualnienia hello za pośrednictwem każdej domeny kontroli kondycji są wykonywane tooensure, która aplikacja hello zachowuje się poprawnie.</span><span class="sxs-lookup"><span data-stu-id="c397a-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="c397a-179">Jeśli uruchomisz hello wcześniej kwerendy hello zbiór usług w sieci szkieletowej hello: / WordCount aplikacji, zwróć uwagę, że hello wersja usługi wordcountservice uległa zmianie, ale hello wersji WordCountWebService nie:</span><span class="sxs-lookup"><span data-stu-id="c397a-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Zapytanie dotyczące usług aplikacji po uaktualnieniu][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="c397a-181">W tym przykładzie podkreślono sposób, w jaki usługa Service Fabric zarządza uaktualnieniami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c397a-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="c397a-182">Krawędzi tylko hello zestawu usług (albo pakietów kodu/konfiguracji w tych usługach) czy uległy zmianie, co sprawia, że proces hello uaktualniania szybszy i bardziej niezawodny.</span><span class="sxs-lookup"><span data-stu-id="c397a-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="c397a-183">Na koniec wróć toohello przeglądarki tooobserve hello zachowanie hello nowej wersji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c397a-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="c397a-184">Zgodnie z oczekiwaniami, hello realizowany liczba wolniej, a hello pierwszej partycji kończy nieznacznie większa ilość hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![Widok hello nowej wersji aplikacji hello w przeglądarce hello][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="c397a-186">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="c397a-186">Cleaning up</span></span>
<span data-ttu-id="c397a-187">Przed zakończeniem, ważne jest tooremember, który hello klaster lokalny jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c397a-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="c397a-188">Aplikacje nadal toorun w tle hello, chyba że zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="c397a-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="c397a-189">W zależności od charakteru aplikacji hello uruchomionej aplikacji może zajmować znaczące ilości zasobów na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="c397a-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="c397a-190">Masz kilka opcji toomanage aplikacji i hello klastra:</span><span class="sxs-lookup"><span data-stu-id="c397a-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="c397a-191">tooremove poszczególnych aplikacji i wszystkich swoich danych, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c397a-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="c397a-192">Lub usuwanie aplikacji hello z hello Service Fabric Explorer **akcje** menu lub menu kontekstowego hello w widoku listy aplikacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="c397a-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![Usuwanie aplikacji w narzędziu Service Fabric Explorer][sfe-delete-application]
2. <span data-ttu-id="c397a-194">Po usunięciu aplikacji hello z hello klastra, należy wyrejestrować w wersji 1.0.0 i 2.0.0 hello typ aplikacji WordCount.</span><span class="sxs-lookup"><span data-stu-id="c397a-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="c397a-195">Usuwanie usuwa pakiety aplikacji hello, w tym kod hello i konfiguracji z magazynu obrazu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="c397a-196">Lub, w narzędziu Service Fabric Explorer, wybierz **Cofnij Aprowizację typu** dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="c397a-197">tooshut hello klastra, ale dane aplikacji hello keep i ślady, kliknij przycisk **Zatrzymaj klaster lokalny** w aplikacji na pasku zadań systemu hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="c397a-198">klaster hello toodelete całkowicie, kliknij przycisk **Usuń klaster lokalny** w aplikacji na pasku zadań systemu hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="c397a-199">Ta opcja spowoduje innego hello powolne wdrożenie po następnym naciśnięciu klawisza F5 w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c397a-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="c397a-200">Usuń klaster lokalny hello tylko wtedy, gdy nie będziesz toouse go przez pewien czas lub jeśli potrzebujesz tooreclaim zasobów.</span><span class="sxs-lookup"><span data-stu-id="c397a-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="c397a-201">Tryb klastra z jednym węzłem i pięcioma węzłami</span><span class="sxs-lookup"><span data-stu-id="c397a-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="c397a-202">Podczas opracowywania aplikacji często są wykonywane szybkie iteracje podczas pisania kodu, debugowania, zmiany kodu i debugowania.</span><span class="sxs-lookup"><span data-stu-id="c397a-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="c397a-203">toohelp zoptymalizować ten proces, hello klastra lokalnego można uruchomić w dwóch trybach: jednym węzłem lub pięcioma węzłami.</span><span class="sxs-lookup"><span data-stu-id="c397a-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="c397a-204">Oba tryby klastra mają swoje zalety.</span><span class="sxs-lookup"><span data-stu-id="c397a-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="c397a-205">Tryb pięcioma węzłami klastra umożliwia toowork z klastrem prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="c397a-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="c397a-206">Można przetestować scenariusze pracy awaryjnej i pracować z większą liczbą wystąpień i replik usług.</span><span class="sxs-lookup"><span data-stu-id="c397a-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="c397a-207">Tryb klastra z jednym węzłem jest zoptymalizowany toodo szybkiego wdrożenia i rejestracji usługi, toohelp szybko sprawdzić poprawność kodu za pomocą środowiska uruchomieniowego platformy Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="c397a-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="c397a-208">Tryby klastra z jednym węzłem i z pięcioma węzłami nie są emulatorami ani symulatorami.</span><span class="sxs-lookup"><span data-stu-id="c397a-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="c397a-209">Witaj lokalnego klastra projektowego uruchamia hello sam kod platformy, która znajduje się w klastrach obejmujących wiele maszyn.</span><span class="sxs-lookup"><span data-stu-id="c397a-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="c397a-210">Jeśli zmienisz tryb klastra hello hello bieżący klaster zostanie usunięty z systemu i jest tworzony nowy klaster.</span><span class="sxs-lookup"><span data-stu-id="c397a-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="c397a-211">Hello danych przechowywanych w klastrze hello jest usunięte w przypadku zmiany trybu klastra.</span><span class="sxs-lookup"><span data-stu-id="c397a-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="c397a-212">toochange hello tryb tooone węzła klastra, wybierz opcję **Przełącz tryb klastra** w hello usługi sieć szkieletowa Local Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="c397a-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![Przełączanie trybu klastra][switch-cluster-mode]

<span data-ttu-id="c397a-214">Lub zmień tryb klastra hello przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c397a-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="c397a-215">Uruchom nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c397a-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="c397a-216">Uruchom skrypt instalacji klastra hello z folderu zestawu SDK hello:</span><span class="sxs-lookup"><span data-stu-id="c397a-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="c397a-217">Instalacja klastra trwa kilka chwil.</span><span class="sxs-lookup"><span data-stu-id="c397a-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="c397a-218">Po zakończeniu instalacji powinny być widoczne dane wyjściowe podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="c397a-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Dane wyjściowe instalacji klastra][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="c397a-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c397a-220">Next steps</span></span>
* <span data-ttu-id="c397a-221">Po wdrożeniu i uaktualnieniu wstępnie przygotowanych aplikacji możesz [spróbować utworzyć własne aplikacje w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="c397a-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="c397a-222">Wszystkie operacje hello hello klaster lokalny w tym artykule można wykonać na [Azure klastra](service-fabric-cluster-creation-via-portal.md) również.</span><span class="sxs-lookup"><span data-stu-id="c397a-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="c397a-223">podstawowa została Hello uaktualnienie wykonane w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="c397a-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="c397a-224">Zobacz hello [dokumentacji uaktualnienia](service-fabric-application-upgrade.md) toolearn więcej informacji na temat hello możliwościach i elastyczności uaktualnień sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="c397a-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
