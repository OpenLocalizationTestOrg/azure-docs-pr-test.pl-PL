---
title: "Lokalne wdrażanie i uaktualnianie mikrousług platformy Azure | Microsoft Docs"
description: "Dowiedz się, jak skonfigurować lokalny klaster usługi Service Fabric, wdrożyć w nim istniejącą aplikację, a następnie uaktualnić tę aplikację."
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
ms.openlocfilehash: 359677972c7e1fa3f7435052021ddfae5b1ed85e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="b7000-103">Pierwsze kroki wdrażania i aktualizowania aplikacji w klastrze lokalnym</span><span class="sxs-lookup"><span data-stu-id="b7000-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="b7000-104">Zestaw SDK usługi Azure Service Fabric zawiera pełne lokalne środowisko deweloperskie, którego można użyć, aby szybko rozpocząć wdrażanie aplikacji i zarządzanie nimi w klastrze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b7000-104">The Azure Service Fabric SDK includes a full local development environment that you can use to quickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="b7000-105">Z tego artykułu dowiesz się, jak utworzyć klaster lokalny, wdrożyć w nim istniejącą aplikację, a następnie uaktualnić ją do nowej wersji — a wszystko to z programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7000-105">In this article, you create a local cluster, deploy an existing application to it, and then upgrade that application to a new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b7000-106">W tym artykule przyjęto, że czynności [konfigurowania środowiska deweloperskiego](service-fabric-get-started.md) zostały już ukończone.</span><span class="sxs-lookup"><span data-stu-id="b7000-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="b7000-107">Tworzenie klastra lokalnego</span><span class="sxs-lookup"><span data-stu-id="b7000-107">Create a local cluster</span></span>
<span data-ttu-id="b7000-108">Klaster usługi Service Fabric stanowi zestaw zasobów sprzętowych, w którym można wdrażać aplikacje.</span><span class="sxs-lookup"><span data-stu-id="b7000-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="b7000-109">Zazwyczaj klaster składa się z dowolnej liczby maszyn z zakresu od pięciu sztuk do wielu tysięcy.</span><span class="sxs-lookup"><span data-stu-id="b7000-109">Typically, a cluster is made up of anywhere from five to many thousands of machines.</span></span> <span data-ttu-id="b7000-110">Jednak zestaw SDK usługi Service Fabric obejmuje konfigurację klastra, która może działać na jednej maszynie.</span><span class="sxs-lookup"><span data-stu-id="b7000-110">However, the Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="b7000-111">Należy zrozumieć, że klaster lokalny usługi Service Fabric nie jest emulatorem ani symulatorem.</span><span class="sxs-lookup"><span data-stu-id="b7000-111">It is important to understand that the Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="b7000-112">Jest na nim wykonywany ten sam kod platformy, który można znaleźć w klastrach obejmujących wiele maszyn.</span><span class="sxs-lookup"><span data-stu-id="b7000-112">It runs the same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="b7000-113">Jedyna różnica polega na tym, że na jednej maszynie realizuje on procesy platformowe, które standardowo są rozmieszczone na pięciu maszynach.</span><span class="sxs-lookup"><span data-stu-id="b7000-113">The only difference is that it runs the platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="b7000-114">Zestaw SDK udostępnia dwa sposoby instalacji klastra lokalnego: skrypt programu Windows PowerShell i aplikacja Local Cluster Manager dostępna na pasku zadań.</span><span class="sxs-lookup"><span data-stu-id="b7000-114">The SDK provides two ways to set up a local cluster: a Windows PowerShell script and the Local Cluster Manager system tray app.</span></span> <span data-ttu-id="b7000-115">W tym samouczku używany jest skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7000-115">In this tutorial, we use the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="b7000-116">Jeśli utworzono już klaster lokalny poprzez wdrożenie aplikacji z programu Visual Studio, tę sekcję można pominąć.</span><span class="sxs-lookup"><span data-stu-id="b7000-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="b7000-117">Uruchom nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b7000-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="b7000-118">Uruchom skrypt instalacji klastra z folderu zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="b7000-118">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="b7000-119">Instalacja klastra trwa kilka chwil.</span><span class="sxs-lookup"><span data-stu-id="b7000-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="b7000-120">Po zakończeniu instalacji powinny być widoczne dane wyjściowe podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="b7000-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Dane wyjściowe instalacji klastra][cluster-setup-success]
   
    <span data-ttu-id="b7000-122">Teraz możesz spróbować wdrożyć aplikację na swoim klastrze.</span><span class="sxs-lookup"><span data-stu-id="b7000-122">You are now ready to try deploying an application to your cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="b7000-123">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b7000-123">Deploy an application</span></span>
<span data-ttu-id="b7000-124">Zestaw SDK usługi Service Fabric zawiera bogaty zestaw struktur i narzędzi programistycznych przeznaczonych do tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7000-124">The Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="b7000-125">Jeśli chcesz się dowiedzieć, jak tworzyć aplikacje w programie Visual Studio, zobacz [Tworzenie pierwszej aplikacji usługi Service Fabric w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b7000-125">If you are interested in learning how to create applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="b7000-126">W tym samouczku użyto istniejącej aplikacji przykładowej (o nazwie WordCount), dzięki czemu można skupić się na kwestiach związanych zarządzaniem na platformie, takich jak wdrażanie, monitorowanie i uaktualnianie.</span><span class="sxs-lookup"><span data-stu-id="b7000-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on the management aspects of the platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="b7000-127">Uruchom nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b7000-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="b7000-128">Zaimportuj moduł programu PowerShell zestawu SDK usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b7000-128">Import the Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="b7000-129">Utwórz katalog do przechowywania aplikacji, która zostanie pobrana i wdrożona, na przykład C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="b7000-129">Create a directory to store the application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="b7000-130">[Pobierz aplikację WordCount](http://aka.ms/servicefabric-wordcountapp) do utworzonej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b7000-130">[Download the WordCount application](http://aka.ms/servicefabric-wordcountapp) to the location you created.</span></span>  <span data-ttu-id="b7000-131">Uwaga: przeglądarka Microsoft Edge zapisuje plik z rozszerzeniem *zip*.</span><span class="sxs-lookup"><span data-stu-id="b7000-131">Note: the Microsoft Edge browser saves the file with a *.zip* extension.</span></span>  <span data-ttu-id="b7000-132">Zmień rozszerzenie pliku na *sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="b7000-132">Change the file extension to *.sfpkg*.</span></span>
5. <span data-ttu-id="b7000-133">Nawiąż połączenie z klastrem lokalnym:</span><span class="sxs-lookup"><span data-stu-id="b7000-133">Connect to the local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="b7000-134">Utwórz nową aplikację za pomocą polecenia wdrożenia zestawu SDK z nazwą pakietu aplikacji i ścieżką do niego.</span><span class="sxs-lookup"><span data-stu-id="b7000-134">Create a new application using the SDK's deployment command with a name and a path to the application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="b7000-135">Jeśli wszystko przebiegnie poprawnie, powinny pojawić się następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="b7000-135">If all goes well, you should see the following output:</span></span>
   
    ![Wdrażanie aplikacji w klastrze lokalnym][deploy-app-to-local-cluster]
7. <span data-ttu-id="b7000-137">Aby zobaczyć aplikację w akcji, uruchom przeglądarkę i przejdź pod adres [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="b7000-137">To see the application in action, launch the browser and navigate to [http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="b7000-138">Powinien zostać wyświetlony następujący ekran:</span><span class="sxs-lookup"><span data-stu-id="b7000-138">You should see:</span></span>
   
    ![Interfejs użytkownika wdrożonej aplikacji][deployed-app-ui]
   
    <span data-ttu-id="b7000-140">Aplikacja WordCount jest prosta.</span><span class="sxs-lookup"><span data-stu-id="b7000-140">The WordCount application is simple.</span></span> <span data-ttu-id="b7000-141">Zawiera kliencki kod JavaScript generujący losowe pięcioznakowe „słowa”, które są następnie przekazywane do aplikacji za pośrednictwem interfejsu API ASP.NET Web.</span><span class="sxs-lookup"><span data-stu-id="b7000-141">It includes client-side JavaScript code to generate random five-character "words", which are then relayed to the application via ASP.NET Web API.</span></span> <span data-ttu-id="b7000-142">Usługa stanowa śledzi liczbę zliczonych słów.</span><span class="sxs-lookup"><span data-stu-id="b7000-142">A stateful service tracks the number of words counted.</span></span> <span data-ttu-id="b7000-143">Są one przydzielane do partycji na podstawie pierwszego znaku słowa.</span><span class="sxs-lookup"><span data-stu-id="b7000-143">They are partitioned based on the first character of the word.</span></span> <span data-ttu-id="b7000-144">Kod źródłowy aplikacji WordCount można znaleźć w [klasycznych przykładach wprowadzających](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="b7000-144">You can find the source code for the WordCount app in the [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="b7000-145">Aplikacja, którą wdrożyliśmy, zawiera cztery partycje.</span><span class="sxs-lookup"><span data-stu-id="b7000-145">The application that we deployed contains four partitions.</span></span> <span data-ttu-id="b7000-146">Słowa zaczynające się na litery od A do G są przechowywane w pierwszej partycji, słowa zaczynające się na litery od H do N są przechowywane w drugiej partycji i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="b7000-146">So words beginning with A through G are stored in the first partition, words beginning with H through N are stored in the second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="b7000-147">Wyświetlanie szczegółów i stanu aplikacji</span><span class="sxs-lookup"><span data-stu-id="b7000-147">View application details and status</span></span>
<span data-ttu-id="b7000-148">Po wdrożeniu aplikacji przyjrzymy się części jej szczegółów w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b7000-148">Now that we have deployed the application, let's look at some of the app details in PowerShell.</span></span>

1. <span data-ttu-id="b7000-149">Wygeneruj zapytanie dotyczące wszystkich aplikacji wdrożonych w klastrze:</span><span class="sxs-lookup"><span data-stu-id="b7000-149">Query all deployed applications on the cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="b7000-150">Jeśli została wdrożona tylko aplikacja WordCount, powinny pojawić się dane podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="b7000-150">Assuming that you have only deployed the WordCount app, you see something similar to:</span></span>
   
    ![Zapytanie dotyczące wszystkich wdrożonych aplikacji w powłoce PowerShell][ps-getsfapp]
2. <span data-ttu-id="b7000-152">Przejdź do następnego poziomu, generując zapytanie dotyczące zestawu usług zawartych w aplikacji WordCount.</span><span class="sxs-lookup"><span data-stu-id="b7000-152">Go to the next level by querying the set of services that are included in the WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lista usług dla aplikacji w programie PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="b7000-154">Aplikacja składa się z dwóch usług — frontonu sieci Web i usługi stanowej, która zarządza słowami.</span><span class="sxs-lookup"><span data-stu-id="b7000-154">The application is made up of two services, the web front end, and the stateful service that manages the words.</span></span>
3. <span data-ttu-id="b7000-155">Na koniec przyjrzyj się liście partycji dla usługi WordCountService:</span><span class="sxs-lookup"><span data-stu-id="b7000-155">Finally, look at the list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Widok partycji usługi w programie PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="b7000-157">Użyty zestaw poleceń, podobnie jak wszystkie polecenia programu PowerShell usługi Service Fabric, jest dostępny dla dowolnego klastra, z którym można nawiązać połączenie — lokalnego lub zdalnego.</span><span class="sxs-lookup"><span data-stu-id="b7000-157">The set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="b7000-158">Interakcje z klastrem w sposób bardziej wizualny można realizować przy użyciu opartego na sieci Web narzędzia Service Fabric Explorer, które jest dostępne po przejściu w przeglądarce pod adres [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="b7000-158">For a more visual way to interact with the cluster, you can use the web-based Service Fabric Explorer tool by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer) in the browser.</span></span>
   
    ![Wyświetlanie szczegółów aplikacji w narzędziu Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="b7000-160">Aby uzyskać więcej informacji na temat narzędzia Service Fabric Explorer, zobacz [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) (Wizualizacja klastra przy użyciu narzędzia Service Fabric Explorer).</span><span class="sxs-lookup"><span data-stu-id="b7000-160">To learn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="b7000-161">Uaktualnianie aplikacji</span><span class="sxs-lookup"><span data-stu-id="b7000-161">Upgrade an application</span></span>
<span data-ttu-id="b7000-162">Usługa Service Fabric realizuje uaktualnienia bez przestojów, ponieważ monitoruje stan aplikacji wdrażanej w klastrze.</span><span class="sxs-lookup"><span data-stu-id="b7000-162">Service Fabric provides no-downtime upgrades by monitoring the health of the application as it rolls out across the cluster.</span></span> <span data-ttu-id="b7000-163">Przeprowadź uaktualnienie aplikacji WordCount.</span><span class="sxs-lookup"><span data-stu-id="b7000-163">Perform an upgrade of the WordCount application.</span></span>

<span data-ttu-id="b7000-164">Nowa wersja aplikacji zlicza teraz tylko słowa zaczynające się od samogłosek.</span><span class="sxs-lookup"><span data-stu-id="b7000-164">The new version of the application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="b7000-165">Podczas wdrażania tego uaktualnienia będzie można zaobserwować dwie zmiany w zachowaniu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7000-165">As the upgrade rolls out, we see two changes in the application's behavior.</span></span> <span data-ttu-id="b7000-166">Po pierwsze szybkości narastania licznika powinna być mniejsza, ponieważ liczba zliczanych słów będzie mniejsza.</span><span class="sxs-lookup"><span data-stu-id="b7000-166">First, the rate at which the count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="b7000-167">Po drugie w pierwszej partycji znajdują się dwie samogłoski (A i E), a wszystkie pozostałe partycje zawierają po jednej sylabie, dlatego licznik pierwszej partycji powinien po pewnym czasie narastać szybciej niż pozostałych.</span><span class="sxs-lookup"><span data-stu-id="b7000-167">Second, since the first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start to outpace the others.</span></span>

1. <span data-ttu-id="b7000-168">[Pobierz pakiet WordCount w wersji 2](http://aka.ms/servicefabric-wordcountappv2) do tej samej lokalizacji, do której pobrano pakiet w wersji 1.</span><span class="sxs-lookup"><span data-stu-id="b7000-168">[Download the WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) to the same location where you downloaded the version 1 package.</span></span>
2. <span data-ttu-id="b7000-169">Wróć do okna programu PowerShell i użyj w zestawie SDK polecenia uaktualniania, aby zarejestrować nową wersję w klastrze.</span><span class="sxs-lookup"><span data-stu-id="b7000-169">Return to your PowerShell window and use the SDK's upgrade command to register the new version in the cluster.</span></span> <span data-ttu-id="b7000-170">Następnie rozpocznij uaktualnianie aplikacji fabric:/WordCount.</span><span class="sxs-lookup"><span data-stu-id="b7000-170">Then begin upgrading the fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="b7000-171">Po rozpoczęciu uaktualnienia w programie PowerShell powinny zostać wyświetlone poniższe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="b7000-171">You should see the following output in PowerShell as the upgrade begins.</span></span>
   
    ![Postęp uaktualniania w programie PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="b7000-173">Podczas uaktualniania łatwiejsze może być monitorowanie stanu tego procesu z narzędzia Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b7000-173">While the upgrade is proceeding, you may find it easier to monitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="b7000-174">Uruchom okno przeglądarki i przejdź pod adres [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="b7000-174">Launch a browser window and navigate to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="b7000-175">Rozwiń węzeł **Aplikacje** w drzewie po lewej stronie, wybierz pozycję **WordCount**, a na koniec wybierz pozycję **fabric:/WordCount**.</span><span class="sxs-lookup"><span data-stu-id="b7000-175">Expand **Applications** in the tree on the left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="b7000-176">Na karcie danych podstawowych jest widoczny stan uaktualnienia obejmującego domeny uaktualnienia klastra.</span><span class="sxs-lookup"><span data-stu-id="b7000-176">In the essentials tab, you see the status of the upgrade as it proceeds through the cluster's upgrade domains.</span></span>
   
    ![Postęp uaktualniania w narzędziu Service Fabric Explorer][sfx-upgradeprogress]
   
    <span data-ttu-id="b7000-178">W trakcie uaktualnienia w poszczególnych domenach wykonywane jest sprawdzanie kondycji w celu zapewnienia, że aplikacja zachowuje się prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="b7000-178">As the upgrade proceeds through each domain, health checks are performed to ensure that the application is behaving properly.</span></span>
4. <span data-ttu-id="b7000-179">Jeśli uruchomisz ponownie wcześniejsze zapytanie względem zestawu usług zawartych w aplikacji fabric:/WordCount, zauważysz, że wersja usługi WordCountService uległa zmianie, ale wersja usługi WordCountWebService nie zmieniła się:</span><span class="sxs-lookup"><span data-stu-id="b7000-179">If you rerun the earlier query for the set of services in the fabric:/WordCount application, notice that the WordCountService version changed but the WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Zapytanie dotyczące usług aplikacji po uaktualnieniu][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="b7000-181">W tym przykładzie podkreślono sposób, w jaki usługa Service Fabric zarządza uaktualnieniami aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7000-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="b7000-182">Działania związane z uaktualnieniami są realizowane tylko względem zestawu usług (albo pakietów kodu/konfiguracji w tych usługach), które uległy zmianie, co sprawia, że proces uaktualniania przebiega szybciej i bardziej niezawodnie.</span><span class="sxs-lookup"><span data-stu-id="b7000-182">It touches only the set of services (or code/configuration packages within those services) that have changed, which makes the process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="b7000-183">Na koniec wróć do przeglądarki, aby przyjrzeć się zachowaniu nowej wersji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7000-183">Finally, return to the browser to observe the behavior of the new application version.</span></span> <span data-ttu-id="b7000-184">Zgodnie z oczekiwaniami liczniki narastają wolniej, a ilość w pierwszej partycji jest nieznacznie większa.</span><span class="sxs-lookup"><span data-stu-id="b7000-184">As expected, the count progresses more slowly, and the first partition ends up with slightly more of the volume.</span></span>
   
    ![Widok nowej wersji aplikacji w przeglądarce][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="b7000-186">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="b7000-186">Cleaning up</span></span>
<span data-ttu-id="b7000-187">Przed zakończeniem należy pamiętać, że klaster lokalny jest prawdziwy.</span><span class="sxs-lookup"><span data-stu-id="b7000-187">Before wrapping up, it's important to remember that the local cluster is real.</span></span> <span data-ttu-id="b7000-188">Aplikacje pozostaną uruchomione w tle, dopóki nie zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="b7000-188">Applications continue to run in the background until you remove them.</span></span>  <span data-ttu-id="b7000-189">W zależności od charakteru działające aplikacje mogą wykorzystywać znaczące ilości zasobów na maszynie.</span><span class="sxs-lookup"><span data-stu-id="b7000-189">Depending on the nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="b7000-190">Istnieje kilka możliwości zarządzania aplikacjami i klastrem:</span><span class="sxs-lookup"><span data-stu-id="b7000-190">You have several options to manage applications and the cluster:</span></span>

1. <span data-ttu-id="b7000-191">Aby usunąć pojedynczą aplikację i wszystkie jej dane, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b7000-191">To remove an individual application and all it's data, run the following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="b7000-192">Możesz również usunąć aplikację z poziomu menu **AKCJE** narzędzia Service Fabric Explorer lub menu kontekstowego w widoku listy aplikacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="b7000-192">Or, delete the application from the Service Fabric Explorer **ACTIONS** menu or the context menu in the left-hand application list view.</span></span>
   
    ![Usuwanie aplikacji w narzędziu Service Fabric Explorer][sfe-delete-application]
2. <span data-ttu-id="b7000-194">Po usunięciu aplikacji z klastra wyrejestruj wersje 1.0.0 i 2.0.0 typu aplikacji WordCount.</span><span class="sxs-lookup"><span data-stu-id="b7000-194">After deleting the application from the cluster, unregister versions 1.0.0 and 2.0.0 of the WordCount application type.</span></span> <span data-ttu-id="b7000-195">Spowoduje to usunięcie z magazynu obrazów klastra pakietów aplikacji, w tym kodu i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b7000-195">Deletion removes the application packages, including the code and configuration, from the cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="b7000-196">W narzędziu Service Fabric Explorer można również wybrać pozycję **Cofnij aprowizację typu** dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b7000-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for the application.</span></span>
3. <span data-ttu-id="b7000-197">Aby zamknąć klaster, zachowując dane i ślady aplikacji, kliknij opcję **Zatrzymaj klaster lokalny** na pasku zadań systemu.</span><span class="sxs-lookup"><span data-stu-id="b7000-197">To shut down the cluster but keep the application data and traces, click **Stop Local Cluster** in the system tray app.</span></span>
4. <span data-ttu-id="b7000-198">Aby całkowicie usunąć klaster, kliknij opcję **Usuń klaster lokalny** na pasku zadań systemu.</span><span class="sxs-lookup"><span data-stu-id="b7000-198">To delete the cluster entirely, click **Remove Local Cluster** in the system tray app.</span></span> <span data-ttu-id="b7000-199">Zastosowanie tej opcji spowoduje powolne wdrożenie po następnym naciśnięciu klawisza F5 w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7000-199">This option will result in another slow deployment the next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="b7000-200">Klaster lokalny należy usuwać tylko wtedy, gdy nie będzie planowane używanie klastra lokalnego przez pewien czas lub konieczne jest odzyskanie zasobów.</span><span class="sxs-lookup"><span data-stu-id="b7000-200">Remove the local cluster only if you don't intend to use it for some time or if you need to reclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="b7000-201">Tryb klastra z jednym węzłem i pięcioma węzłami</span><span class="sxs-lookup"><span data-stu-id="b7000-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="b7000-202">Podczas opracowywania aplikacji często są wykonywane szybkie iteracje podczas pisania kodu, debugowania, zmiany kodu i debugowania.</span><span class="sxs-lookup"><span data-stu-id="b7000-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="b7000-203">Aby pomóc zoptymalizować ten proces, klaster lokalny można uruchomić w dwóch trybach: z jednym węzłem lub z pięcioma węzłami.</span><span class="sxs-lookup"><span data-stu-id="b7000-203">To help optimize this process, the local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="b7000-204">Oba tryby klastra mają swoje zalety.</span><span class="sxs-lookup"><span data-stu-id="b7000-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="b7000-205">Tryb klastra z pięcioma węzłami umożliwia pracę z rzeczywistym klastrem.</span><span class="sxs-lookup"><span data-stu-id="b7000-205">Five-node cluster mode enables you to work with a real cluster.</span></span> <span data-ttu-id="b7000-206">Można przetestować scenariusze pracy awaryjnej i pracować z większą liczbą wystąpień i replik usług.</span><span class="sxs-lookup"><span data-stu-id="b7000-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="b7000-207">Tryb klastra z jednym węzłem jest zoptymalizowany do szybkiego wdrażania i rejestrowania usług, co ułatwia szybkie weryfikowanie kodu za pomocą środowiska uruchomieniowego usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b7000-207">One-node cluster mode is optimized to do quick deployment and registration of services, to help you quickly validate code using the Service Fabric runtime.</span></span>

<span data-ttu-id="b7000-208">Tryby klastra z jednym węzłem i z pięcioma węzłami nie są emulatorami ani symulatorami.</span><span class="sxs-lookup"><span data-stu-id="b7000-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="b7000-209">W lokalnym klastrze projektowy jest wykonywany ten sam kod platformy, który można znaleźć w klastrach obejmujących wiele maszyn.</span><span class="sxs-lookup"><span data-stu-id="b7000-209">The local development cluster runs the same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="b7000-210">Zmiana trybu klastra polega na usunięciu bieżącego klastra z systemu i utworzeniu nowego klastra.</span><span class="sxs-lookup"><span data-stu-id="b7000-210">When you change the cluster mode, the current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="b7000-211">Dane przechowywane w klastrze są usuwane podczas zmiany trybu klastra.</span><span class="sxs-lookup"><span data-stu-id="b7000-211">The data stored in the cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="b7000-212">Aby zmienić tryb na klaster z jednym węzłem, wybierz pozycję **Przełącz tryb klastra** w menedżerze klastra lokalnego usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b7000-212">To change the mode to one-node cluster, select **Switch Cluster Mode** in the Service Fabric Local Cluster Manager.</span></span>

![Przełączanie trybu klastra][switch-cluster-mode]

<span data-ttu-id="b7000-214">Możesz też zmienić tryb klastra przy użyciu programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b7000-214">Or, change the cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="b7000-215">Uruchom nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b7000-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="b7000-216">Uruchom skrypt instalacji klastra z folderu zestawu SDK:</span><span class="sxs-lookup"><span data-stu-id="b7000-216">Run the cluster setup script from the SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="b7000-217">Instalacja klastra trwa kilka chwil.</span><span class="sxs-lookup"><span data-stu-id="b7000-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="b7000-218">Po zakończeniu instalacji powinny być widoczne dane wyjściowe podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="b7000-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Dane wyjściowe instalacji klastra][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="b7000-220">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b7000-220">Next steps</span></span>
* <span data-ttu-id="b7000-221">Po wdrożeniu i uaktualnieniu wstępnie przygotowanych aplikacji możesz [spróbować utworzyć własne aplikacje w programie Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="b7000-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="b7000-222">Wszystkie akcje wykonane w tym artykule w klastrze lokalnym można również wykonać w [klastrze platformy Azure](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b7000-222">All the actions performed on the local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="b7000-223">Uaktualnienie wykonane w tym artykule było podstawowe.</span><span class="sxs-lookup"><span data-stu-id="b7000-223">The upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="b7000-224">Aby dowiedzieć się więcej o możliwościach i elastyczności uaktualnień w usłudze Service Fabric, zobacz [dokumentację uaktualniania](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="b7000-224">See the [upgrade documentation](service-fabric-application-upgrade.md) to learn more about the power and flexibility of Service Fabric upgrades.</span></span>

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
