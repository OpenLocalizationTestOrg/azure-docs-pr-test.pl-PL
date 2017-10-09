---
title: "aaaCreate aplikacją sieci szkieletowej usług .NET na platformie Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji .NET na platformie Azure przy użyciu usługi Service Fabric hello — przykład szybki start."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 20ef88dbf9fb0def31234ef05679a19009b9b529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-service-fabric-application-in-azure"></a><span data-ttu-id="82e4b-103">Tworzenie aplikacji sieci szkieletowej usług .NET na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="82e4b-103">Create a .NET Service Fabric application in Azure</span></span>
<span data-ttu-id="82e4b-104">Usługa Azure Service Fabric to platforma systemów rozproszonych ułatwiająca pakowanie i wdrażanie skalowalnych oraz niezawodnych mikrousług i kontenerów, a także zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="82e4b-104">Azure Service Fabric is a distributed systems platform for deploying and managing scalable and reliable microservices and containers.</span></span> 

<span data-ttu-id="82e4b-105">Ta opcja szybkiego startu przedstawia sposób toodeploy Twojego pierwszego tooService aplikacja .NET sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="82e4b-105">This quickstart shows how toodeploy your first .NET application tooService Fabric.</span></span> <span data-ttu-id="82e4b-106">Po zakończeniu, masz aplikację do głosowania z frontonu, który zapisuje wyniki głosowania stanowe usługi zaplecza w klastrze hello sieci web platformy ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="82e4b-106">When you're finished, you have a voting application with an ASP.NET Core web front-end that saves voting results in a stateful back-end service in hello cluster.</span></span>

![Zrzut ekranu aplikacji](./media/service-fabric-quickstart-dotnet/application-screenshot.png)

<span data-ttu-id="82e4b-108">Za pomocą tej aplikacji, możesz dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="82e4b-108">Using this application you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="82e4b-109">Tworzenie aplikacji przy użyciu platformy .NET i sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="82e4b-109">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="82e4b-110">Użyj jako frontonu sieci web platformy ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="82e4b-110">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="82e4b-111">Przechowywanie danych aplikacji w usługi stanowej</span><span class="sxs-lookup"><span data-stu-id="82e4b-111">Store application data in a stateful service</span></span>
> * <span data-ttu-id="82e4b-112">Debugowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="82e4b-112">Debug your application locally</span></span>
> * <span data-ttu-id="82e4b-113">Wdrażanie klastra tooa aplikacji hello na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="82e4b-113">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="82e4b-114">Aplikacja hello skalowalnego w poziomie w wielu węzłach</span><span class="sxs-lookup"><span data-stu-id="82e4b-114">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="82e4b-115">Uaktualnienie stopniowe aplikacji</span><span class="sxs-lookup"><span data-stu-id="82e4b-115">Perform a rolling application upgrade</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82e4b-116">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="82e4b-116">Prerequisites</span></span>
<span data-ttu-id="82e4b-117">toocomplete tego przewodnika Szybki Start:</span><span class="sxs-lookup"><span data-stu-id="82e4b-117">toocomplete this quickstart:</span></span>
1. <span data-ttu-id="82e4b-118">[Zainstaluj program Visual Studio 2017](https://www.visualstudio.com/) z hello **Azure programowanie** i **ASP.NET i sieć web development** obciążeń.</span><span class="sxs-lookup"><span data-stu-id="82e4b-118">[Install Visual Studio 2017](https://www.visualstudio.com/) with hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
2. [<span data-ttu-id="82e4b-119">Zainstaluj oprogramowanie Git</span><span class="sxs-lookup"><span data-stu-id="82e4b-119">Install Git</span></span>](https://git-scm.com/)
3. [<span data-ttu-id="82e4b-120">Zainstaluj zestaw SDK usługi Microsoft Azure Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="82e4b-120">Install hello Microsoft Azure Service Fabric SDK</span></span>](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-CoreSDK)
4. <span data-ttu-id="82e4b-121">Uruchom następujące polecenie tooenable Visual Studio toodeploy toohello lokalnego klastra sieci szkieletowej usług hello:</span><span class="sxs-lookup"><span data-stu-id="82e4b-121">Run hello following command tooenable Visual Studio toodeploy toohello local Service Fabric cluster:</span></span>
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force -Scope CurrentUser
    ```

## <a name="download-hello-sample"></a><span data-ttu-id="82e4b-122">Pobierz przykładowe hello</span><span class="sxs-lookup"><span data-stu-id="82e4b-122">Download hello sample</span></span>
<span data-ttu-id="82e4b-123">W oknie polecenie Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="82e4b-123">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>
```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="82e4b-124">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="82e4b-124">Run hello application locally</span></span>
<span data-ttu-id="82e4b-125">Kliknij prawym przyciskiem myszy ikonę programu Visual Studio hello hello Start Menu i wybierz polecenie **Uruchom jako administrator**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-125">Right-click hello Visual Studio icon in hello Start Menu and choose **Run as administrator**.</span></span> <span data-ttu-id="82e4b-126">W kolejności tooattach hello debugera tooyour usługi należy toorun Visual Studio jako administrator.</span><span class="sxs-lookup"><span data-stu-id="82e4b-126">In order tooattach hello debugger tooyour services, you need toorun Visual Studio as administrator.</span></span>

<span data-ttu-id="82e4b-127">Otwórz hello **Voting.sln** rozwiązania Visual Studio z sklonowanego repozytorium hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-127">Open hello **Voting.sln** Visual Studio solution from hello repository you cloned.</span></span>

<span data-ttu-id="82e4b-128">Aplikacja hello toodeploy, naciśnij klawisz **F5**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-128">toodeploy hello application, press **F5**.</span></span>

> [!NOTE]
> <span data-ttu-id="82e4b-129">Witaj pierwszego uruchomienia i wdrażanie aplikacji hello, Visual Studio tworzy lokalny klaster na potrzeby debugowania.</span><span class="sxs-lookup"><span data-stu-id="82e4b-129">hello first time you run and deploy hello application, Visual Studio creates a local cluster for debugging.</span></span> <span data-ttu-id="82e4b-130">Ta operacja może potrwać pewien czas.</span><span class="sxs-lookup"><span data-stu-id="82e4b-130">This operation may take some time.</span></span> <span data-ttu-id="82e4b-131">Stan tworzenia klastra Hello jest wyświetlany w oknie danych wyjściowych programu Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-131">hello cluster creation status is displayed in hello Visual Studio output window.</span></span>

<span data-ttu-id="82e4b-132">Po zakończeniu wdrażania hello przeglądarkę i otwórz tę stronę: `http://localhost:8080` -hello frontonu hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="82e4b-132">When hello deployment is complete, launch a browser and open this page: `http://localhost:8080` - hello web front-end of hello application.</span></span>

![Aplikacji frontonu](./media/service-fabric-quickstart-dotnet/application-screenshot-new.png)

<span data-ttu-id="82e4b-134">Można teraz dodać zestaw głosowania opcje i Rozpocznij tworzenie głosów.</span><span class="sxs-lookup"><span data-stu-id="82e4b-134">You can now add a set of voting options, and start taking votes.</span></span> <span data-ttu-id="82e4b-135">Aplikacja Hello jest uruchamiana i przechowuje wszystkie dane w klastrze usługi sieć szkieletowa, bez potrzeby hello oddzielnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="82e4b-135">hello application runs and stores all data in your Service Fabric cluster, without hello need for a separate database.</span></span>

## <a name="walk-through-hello-voting-sample-application"></a><span data-ttu-id="82e4b-136">Przewodnik po głosowanie w przykładowej aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="82e4b-136">Walk through hello voting sample application</span></span>
<span data-ttu-id="82e4b-137">głosowania aplikacji Hello składa się z dwóch usług:</span><span class="sxs-lookup"><span data-stu-id="82e4b-137">hello voting application consists of two services:</span></span>
- <span data-ttu-id="82e4b-138">Usługa frontonu (VotingWeb) sieci Web — platformy ASP.NET Core usługi frontonu, która służy hello strony sieci web i ujawnia sieci web API toocommunicate hello usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="82e4b-138">Web front-end service (VotingWeb)- An ASP.NET Core web front-end service, which serves hello web page and exposes web APIs toocommunicate with hello backend service.</span></span>
- <span data-ttu-id="82e4b-139">Usługi zaplecza (VotingData) — usługi sieci web platformy ASP.NET Core, która ujawnia interfejsu API toostore hello głos powoduje niezawodnej słownika utrwalony na dysku.</span><span class="sxs-lookup"><span data-stu-id="82e4b-139">Back-end service (VotingData)- An ASP.NET Core web service, which exposes an API toostore hello vote results in a reliable dictionary persisted on disk.</span></span>

![Diagram aplikacji](./media/service-fabric-quickstart-dotnet/application-diagram.png)

<span data-ttu-id="82e4b-141">Po głosowanie w hello aplikacji hello następującego wystąpienia zdarzeń:</span><span class="sxs-lookup"><span data-stu-id="82e4b-141">When you vote in hello application hello following events occur:</span></span>
1. <span data-ttu-id="82e4b-142">JavaScript wysyła hello głos żądanie toohello interfejsu API sieci web usługi frontonu sieci web hello jako żądanie HTTP PUT.</span><span class="sxs-lookup"><span data-stu-id="82e4b-142">A JavaScript sends hello vote request toohello web API in hello web front-end service as an HTTP PUT request.</span></span>

2. <span data-ttu-id="82e4b-143">Usługa frontonu sieci web Hello używa toolocate serwera proxy i przesyła usługi zaplecza HTTP PUT toohello żądania.</span><span class="sxs-lookup"><span data-stu-id="82e4b-143">hello web front-end service uses a proxy toolocate and forward an HTTP PUT request toohello back-end service.</span></span>

3. <span data-ttu-id="82e4b-144">usługi zaplecza Hello przyjmuje hello żądania przychodzącego, a hello magazynów zaktualizowany wynik w niezawodnej słownik, który pobiera replikowanych toomultiple węzłów w klastrze hello i utrwalony na dysku.</span><span class="sxs-lookup"><span data-stu-id="82e4b-144">hello back-end service takes hello incoming request, and stores hello updated result in a reliable dictionary, which gets replicated toomultiple nodes within hello cluster and persisted on disk.</span></span> <span data-ttu-id="82e4b-145">Dane wszystkich aplikacji hello są przechowywane w klastrze hello, więc nie bazy danych nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="82e4b-145">All hello application's data is stored in hello cluster, so no database is needed.</span></span>

## <a name="debug-in-visual-studio"></a><span data-ttu-id="82e4b-146">Debugowanie w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82e4b-146">Debug in Visual Studio</span></span>
<span data-ttu-id="82e4b-147">Podczas debugowania aplikacji w programie Visual Studio, czy używasz klastra lokalnego Projektowanie sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="82e4b-147">When debugging application in Visual Studio, you are using a local Service Fabric development cluster.</span></span> <span data-ttu-id="82e4b-148">Masz hello tooadjust opcji debugowania scenariusz tooyour środowisko.</span><span class="sxs-lookup"><span data-stu-id="82e4b-148">You have hello option tooadjust your debugging experience tooyour scenario.</span></span> <span data-ttu-id="82e4b-149">W tej aplikacji są przechowywane dane w naszej usługi zaplecza przy użyciu niezawodnych słownika.</span><span class="sxs-lookup"><span data-stu-id="82e4b-149">In this application, we store data in our back-end service, using a reliable dictionary.</span></span> <span data-ttu-id="82e4b-150">Po zatrzymaniu debugera hello programu Visual Studio spowoduje usunięcie aplikacji hello na domyślne.</span><span class="sxs-lookup"><span data-stu-id="82e4b-150">Visual Studio removes hello application per default when you stop hello debugger.</span></span> <span data-ttu-id="82e4b-151">Usunięcie aplikacji hello powoduje hello danych w wewnętrznej hello tooalso usługi można usunąć.</span><span class="sxs-lookup"><span data-stu-id="82e4b-151">Removing hello application causes hello data in hello back-end service tooalso be removed.</span></span> <span data-ttu-id="82e4b-152">toopersist hello danych między sesji debugowania, możesz zmienić hello **tryb debugowania aplikacji** jako właściwość hello **głosowania** projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82e4b-152">toopersist hello data between debugging sessions, you can change hello **Application Debug Mode** as a property on hello **Voting** project in Visual Studio.</span></span>

<span data-ttu-id="82e4b-153">toolook na co się stanie w kodzie hello, pełną hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="82e4b-153">toolook at what happens in hello code, complete hello following steps:</span></span>
1. <span data-ttu-id="82e4b-154">Otwórz hello **VotesController.cs** pliku i ustaw punkt przerwania w składniku web API hello **Put** — metoda (linii 47) — możesz wyszukać plik hello w hello Eksploratora rozwiązań w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82e4b-154">Open hello **VotesController.cs** file and set a breakpoint in hello web API's **Put** method (line 47) - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>

2. <span data-ttu-id="82e4b-155">Otwórz hello **VoteDataController.cs** pliku i ustaw punkt przerwania w tym składnika web API **Put** — metoda (wiersz 50).</span><span class="sxs-lookup"><span data-stu-id="82e4b-155">Open hello **VoteDataController.cs** file and set a breakpoint in this web API's **Put** method (line 50).</span></span>

3. <span data-ttu-id="82e4b-156">Przejść toohello przeglądarki i kliknij opcję głosu lub dodać nową opcję głosu.</span><span class="sxs-lookup"><span data-stu-id="82e4b-156">Go back toohello browser and click a voting option or add a new voting option.</span></span> <span data-ttu-id="82e4b-157">Naciśniesz hello pierwszy punkt przerwania hello web przodu end w kontrolerze interfejsu api.</span><span class="sxs-lookup"><span data-stu-id="82e4b-157">You hit hello first breakpoint in hello web front-end's api controller.</span></span>
    - <span data-ttu-id="82e4b-158">Jest to, gdzie hello JavaScript w przeglądarce hello wysyła kontrolera interfejsu API sieci web toohello żądania w hello usługi frontonu.</span><span class="sxs-lookup"><span data-stu-id="82e4b-158">This is where hello JavaScript in hello browser sends a request toohello web API controller in hello front-end service.</span></span>
    
    ![Dodawanie usługi frontonu głosu](./media/service-fabric-quickstart-dotnet/addvote-frontend.png)

    - <span data-ttu-id="82e4b-160">Najpierw możemy utworzyć hello adresu URL toohello ReverseProxy dla naszej usługi zaplecza **(1)**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-160">First we construct hello URL toohello ReverseProxy for our back-end service **(1)**.</span></span>
    - <span data-ttu-id="82e4b-161">Następnie możemy wysłać hello HTTP PUT żądanie toohello ReverseProxy **(2)**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-161">Then we send hello HTTP PUT Request toohello ReverseProxy **(2)**.</span></span>
    - <span data-ttu-id="82e4b-162">Na koniec hello zostanie zwrócona odpowiedź hello z klienta toohello usługi zaplecza hello **(3)**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-162">Finally hello we return hello response from hello back-end service toohello client **(3)**.</span></span>

4. <span data-ttu-id="82e4b-163">Naciśnij klawisz **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="82e4b-163">Press **F5** toocontinue</span></span>
    - <span data-ttu-id="82e4b-164">Jesteś teraz w punkcie przerwania hello hello usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="82e4b-164">You are now at hello break point in hello back-end service.</span></span>
    
    ![Dodawania usługi zaplecza głosu](./media/service-fabric-quickstart-dotnet/addvote-backend.png)

    - <span data-ttu-id="82e4b-166">W hello pierwszego wiersza w metodzie hello **(1)** używamy hello `StateManager` tooget lub dodać słownika niezawodnej o nazwie `counts`.</span><span class="sxs-lookup"><span data-stu-id="82e4b-166">In hello first line in hello method **(1)** we are using hello `StateManager` tooget or add a reliable dictionary called `counts`.</span></span>
    - <span data-ttu-id="82e4b-167">Wszystkie interakcje z wartości w słowniku niezawodnej wymagają transakcji, za pomocą tej instrukcji **(2)** tworzy tej transakcji.</span><span class="sxs-lookup"><span data-stu-id="82e4b-167">All interactions with values in a reliable dictionary require a transaction, this using statement **(2)** creates that transaction.</span></span>
    - <span data-ttu-id="82e4b-168">W transakcji hello modyfikacjom następnie hello wartość hello odpowiedniego klucza hello głosowania opcji i zatwierdzeń hello operacji **(3)**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-168">In hello transaction, we then update hello value of hello relevant key for hello voting option and commits hello operation **(3)**.</span></span> <span data-ttu-id="82e4b-169">Po zatwierdzić hello metoda zwróci wartość, hello danych jest aktualizowany w słowniku hello i replikowane tooother węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-169">Once hello commit method returns, hello data is updated in hello dictionary and replicated tooother nodes in hello cluster.</span></span> <span data-ttu-id="82e4b-170">dane Hello teraz są bezpiecznie przechowywane w hello klastra, a usługi zaplecza hello może przełączyć się węzłów tooother zachowaniu hello dostępnych danych.</span><span class="sxs-lookup"><span data-stu-id="82e4b-170">hello data is now safely stored in hello cluster, and hello back-end service can fail over tooother nodes, still having hello data available.</span></span>
5. <span data-ttu-id="82e4b-171">Naciśnij klawisz **F5** toocontinue</span><span class="sxs-lookup"><span data-stu-id="82e4b-171">Press **F5** toocontinue</span></span>

<span data-ttu-id="82e4b-172">hello toostop sesję, naciśnij klawisz debugowania **Shift + F5**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-172">toostop hello debugging session, press **Shift+F5**.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="82e4b-173">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="82e4b-173">Deploy hello application tooAzure</span></span>
<span data-ttu-id="82e4b-174">toodeploy hello tooa klastrze aplikacji na platformie Azure, można wybrać toocreate własnych klastra lub użyj klastra strony.</span><span class="sxs-lookup"><span data-stu-id="82e4b-174">toodeploy hello application tooa cluster in Azure, you can either choose toocreate your own cluster, or use a Party Cluster.</span></span>

<span data-ttu-id="82e4b-175">Klastry firm są bezpłatne, ograniczonej czasowo klastrów sieci szkieletowej usług hostowanej na platformie Azure i uruchom przez zespół usługi sieć szkieletowa hello którym każda osoba, która wdrażania aplikacji i Dowiedz się więcej o hello platformy.</span><span class="sxs-lookup"><span data-stu-id="82e4b-175">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="82e4b-176">tooget dostępu tooa klastra strona [postępuj zgodnie z instrukcjami hello](http://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="82e4b-176">tooget access tooa Party Cluster, [follow hello instructions](http://aka.ms/tryservicefabric).</span></span> 

<span data-ttu-id="82e4b-177">Aby uzyskać informacje na temat tworzenia własnego klastra, zobacz [Tworzenie pierwszego klastra usługi Service Fabric na platformie Azure](service-fabric-get-started-azure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="82e4b-177">For information about creating your own cluster, see [Create your first Service Fabric cluster on Azure](service-fabric-get-started-azure-cluster.md).</span></span>

> [!Note]
> <span data-ttu-id="82e4b-178">Usługa frontonu sieci web Hello jest skonfigurowany toolisten na porcie 8080 dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="82e4b-178">hello web front-end service is configured toolisten on port 8080 for incoming traffic.</span></span> <span data-ttu-id="82e4b-179">Upewnij się, że port w klastrze został otwarty.</span><span class="sxs-lookup"><span data-stu-id="82e4b-179">Make sure that port is open in your cluster.</span></span> <span data-ttu-id="82e4b-180">Jeśli używasz hello klastra strona ten port jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="82e4b-180">If you are using hello Party Cluster, this port is open.</span></span>
>

### <a name="deploy-hello-application-using-visual-studio"></a><span data-ttu-id="82e4b-181">Wdrażanie aplikacji hello przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="82e4b-181">Deploy hello application using Visual Studio</span></span>
<span data-ttu-id="82e4b-182">Teraz, aplikacja hello jest gotowy, można wdrożyć klaster tooa bezpośrednio z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82e4b-182">Now that hello application is ready, you can deploy it tooa cluster directly from Visual Studio.</span></span>

1. <span data-ttu-id="82e4b-183">Kliknij prawym przyciskiem myszy **głosowania** w hello Eksploratorze rozwiązań i wybierz polecenie **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-183">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="82e4b-184">zostanie wyświetlone okno dialogowe publikowania Hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-184">hello Publish dialog appears.</span></span>

    ![Okno dialogowe Publikowanie](./media/service-fabric-quickstart-dotnet/publish-app.png)

2. <span data-ttu-id="82e4b-186">Typ w hello punktu końcowego połączenia klastra hello w hello **punktu końcowego połączenia** a następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-186">Type in hello Connection Endpoint of hello cluster in hello **Connection Endpoint** field and click **Publish**.</span></span> <span data-ttu-id="82e4b-187">Podczas rejestracji hello strona klastra, hello punktu końcowego połączenia znajduje się w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-187">When signing up for hello Party Cluster, hello Connection Endpoint is provided in hello browser.</span></span> <span data-ttu-id="82e4b-188">— na przykład `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span><span class="sxs-lookup"><span data-stu-id="82e4b-188">- for example, `winh1x87d1d.westus.cloudapp.azure.com:19000`.</span></span>

3. <span data-ttu-id="82e4b-189">Otwórz przeglądarkę i typ adres klastra hello — na przykład `http://winh1x87d1d.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="82e4b-189">Open a browser and type in hello cluster address - for example, `http://winh1x87d1d.westus.cloudapp.azure.com`.</span></span> <span data-ttu-id="82e4b-190">Powinna zostać wyświetlona aplikacja hello uruchomiona w klastrze hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="82e4b-190">You should now see hello application running in hello cluster in Azure.</span></span>

![Aplikacji frontonu](./media/service-fabric-quickstart-dotnet/application-screenshot-new-azure.png)

## <a name="scale-applications-and-services-in-a-cluster"></a><span data-ttu-id="82e4b-192">Skalowanie aplikacji i usług w klastrze</span><span class="sxs-lookup"><span data-stu-id="82e4b-192">Scale applications and services in a cluster</span></span>
<span data-ttu-id="82e4b-193">Łatwo można skalować usługi sieć szkieletowa usług między tooaccommodate klastra, zmiany w hello obciążenie hello usług.</span><span class="sxs-lookup"><span data-stu-id="82e4b-193">Service Fabric services can easily be scaled across a cluster tooaccommodate for a change in hello load on hello services.</span></span> <span data-ttu-id="82e4b-194">Zmieniając hello liczbę wystąpień w klastrze hello zmiany skali usługi.</span><span class="sxs-lookup"><span data-stu-id="82e4b-194">You scale a service by changing hello number of instances running in hello cluster.</span></span> <span data-ttu-id="82e4b-195">Istnieje wiele sposobów skalowania usługi, możesz użyć skryptów lub poleceń programu PowerShell lub interfejsu wiersza polecenia usługi sieci szkieletowej (sfctl).</span><span class="sxs-lookup"><span data-stu-id="82e4b-195">You have multiple ways of scaling your services, you can use scripts or commands from PowerShell or Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="82e4b-196">W tym przykładzie użyto Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="82e4b-196">In this example, we are using Service Fabric Explorer.</span></span>

<span data-ttu-id="82e4b-197">Service Fabric Explorer działa we wszystkich klastrach sieci szkieletowej usług i jest dostępny z poziomu przeglądarki, przeglądając port zarządzania klastrami HTTP toohello (19080), na przykład `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="82e4b-197">Service Fabric Explorer runs in all Service Fabric clusters and can be accessed from a browser, by browsing toohello clusters HTTP management port (19080), for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>

<span data-ttu-id="82e4b-198">Witaj tooscale usługi frontonu sieci web, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="82e4b-198">tooscale hello web front-end service, do hello following steps:</span></span>

1. <span data-ttu-id="82e4b-199">Otwórz narzędzie Service Fabric Explorer w klastrze — na przykład `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="82e4b-199">Open Service Fabric Explorer in your cluster - for example,`http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
2. <span data-ttu-id="82e4b-200">Kliknij pozycję dalej toohello wielokropka (wielokropek) hello **sieci szkieletowej: / głosowania/VotingWeb** węzła w hello treeview i wybierz polecenie **skali usługi**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-200">Click on hello ellipsis (three dots) next toohello **fabric:/Voting/VotingWeb** node in hello treeview and choose **Scale Service**.</span></span>

    ![Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scale.png)

    <span data-ttu-id="82e4b-202">Teraz możesz tooscale hello liczbę wystąpień usługi frontonu sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-202">You can now choose tooscale hello number of instances of hello web front-end service.</span></span>

3. <span data-ttu-id="82e4b-203">Zmień numer hello zbyt**2** i kliknij przycisk **skali usługi**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-203">Change hello number too**2** and click **Scale Service**.</span></span>
4. <span data-ttu-id="82e4b-204">Polecenie hello **fabric: / głosowania/VotingWeb** węzeł w widoku drzewa hello i rozwiń węzeł partycji hello (reprezentowane przez identyfikator GUID).</span><span class="sxs-lookup"><span data-stu-id="82e4b-204">Click on hello **fabric:/Voting/VotingWeb** node in hello tree-view and expand hello partition node (represented by a GUID).</span></span>

    ![Usługa skalowania Eksploratora sieci szkieletowej usług](./media/service-fabric-quickstart-dotnet/service-fabric-explorer-scaled-service.png)

    <span data-ttu-id="82e4b-206">Usługa hello ma dwa wystąpienia, czy w widoku drzewa hello Zobacz węzły, których wystąpienia hello uruchamiane na będą teraz widoczne.</span><span class="sxs-lookup"><span data-stu-id="82e4b-206">You can now see that hello service has two instances, and in hello tree view you see which nodes hello instances run on.</span></span>

<span data-ttu-id="82e4b-207">Przez to zadanie proste zarządzanie możemy podwójny dostępnych zasobów hello obciążenie użytkownikami tooprocess naszej usługi frontonu.</span><span class="sxs-lookup"><span data-stu-id="82e4b-207">By this simple management task, we doubled hello resources available for our front-end service tooprocess user load.</span></span> <span data-ttu-id="82e4b-208">Jest ważne toounderstand, który nie ma potrzeby wielu wystąpień toohave usługi, działa on prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="82e4b-208">It's important toounderstand that you do not need multiple instances of a service toohave it run reliably.</span></span> <span data-ttu-id="82e4b-209">W przypadku niepowodzenia usługi sieć szkieletowa usług zapewnia, że nowe wystąpienie usługi działa w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-209">If a service fails, Service Fabric makes sure a new service instance runs in hello cluster.</span></span>

## <a name="perform-a-rolling-application-upgrade"></a><span data-ttu-id="82e4b-210">Uaktualnienie stopniowe aplikacji</span><span class="sxs-lookup"><span data-stu-id="82e4b-210">Perform a rolling application upgrade</span></span>
<span data-ttu-id="82e4b-211">Podczas wdrażania nowej aplikacji tooyour aktualizacje, Service Fabric wprowadza hello aktualizacji w bezpieczny sposób.</span><span class="sxs-lookup"><span data-stu-id="82e4b-211">When deploying new updates tooyour application, Service Fabric rolls out hello update in a safe way.</span></span> <span data-ttu-id="82e4b-212">Uaktualnień stopniowych daje bez przestojów podczas uaktualniania oraz automatycznego wycofywania powinien wystąpić błędy.</span><span class="sxs-lookup"><span data-stu-id="82e4b-212">Rolling upgrades gives you no downtime while upgrading as well as automated rollback should errors occur.</span></span>

<span data-ttu-id="82e4b-213">tooupgrade hello aplikacji, hello następujące:</span><span class="sxs-lookup"><span data-stu-id="82e4b-213">tooupgrade hello application, do hello following:</span></span>

1. <span data-ttu-id="82e4b-214">Otwórz hello **Index.cshtml** pliku w Visual Studio — można wyszukać plik hello w hello Eksploratora rozwiązań w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82e4b-214">Open hello **Index.cshtml** file in Visual Studio - You can search for hello file in hello Solution Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="82e4b-215">Zmień nagłówek hello na stronie powitania przez dodanie tekstem — na przykład.</span><span class="sxs-lookup"><span data-stu-id="82e4b-215">Change hello heading on hello page by adding some text - for example.</span></span>
    ```html
        <div class="col-xs-8 col-xs-offset-2 text-center">
            <h2>Service Fabric Voting Sample v2</h2>
        </div>
    ```
3. <span data-ttu-id="82e4b-216">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-216">Save hello file.</span></span>
4. <span data-ttu-id="82e4b-217">Kliknij prawym przyciskiem myszy **głosowania** w hello Eksploratorze rozwiązań i wybierz polecenie **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-217">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span> <span data-ttu-id="82e4b-218">zostanie wyświetlone okno dialogowe publikowania Hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-218">hello Publish dialog appears.</span></span>
5. <span data-ttu-id="82e4b-219">Kliknij przycisk hello **wersji manifestu** przycisk toochange hello wersji hello usług i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="82e4b-219">Click hello **Manifest Version** button toochange hello version of hello service and application.</span></span>
6. <span data-ttu-id="82e4b-220">Zmiana wersji hello hello **kod** elementu w obszarze **VotingWebPkg** zbyt "2.0.0", na przykład, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-220">Change hello version of hello **Code** element under **VotingWebPkg** too"2.0.0", for example, and click **Save**.</span></span>

    ![Zmiana wersji w oknie dialogowym](./media/service-fabric-quickstart-dotnet/change-version.png)
7. <span data-ttu-id="82e4b-222">W hello **publikowania aplikacji sieci szkieletowej usług** okna dialogowego, sprawdź hello hello uaktualniania aplikacji wyboru i kliknij **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="82e4b-222">In hello **Publish Service Fabric Application** dialog, check hello Upgrade hello Application checkbox, and click **Publish**.</span></span>

    ![Okno dialogowe publikowania uaktualnienia ustawienie](./media/service-fabric-quickstart-dotnet/upgrade-app.png)
8. <span data-ttu-id="82e4b-224">Otwórz przeglądarkę i przejdź toohello adres klastra na porcie 19080 — na przykład `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span><span class="sxs-lookup"><span data-stu-id="82e4b-224">Open your browser and browse toohello cluster address on port 19080 - for example, `http://winh1x87d1d.westus.cloudapp.azure.com:19080`.</span></span>
9. <span data-ttu-id="82e4b-225">Polecenie hello **aplikacji** węzła w widoku drzewa hello, a następnie **uaktualnień w toku** w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="82e4b-225">Click on hello **Applications** node in hello tree view, and then **Upgrades in Progress** in hello right-hand pane.</span></span> <span data-ttu-id="82e4b-226">Zostanie wyświetlony sposobu uaktualniania hello przedstawia za pośrednictwem hello domen uaktualnienia w klastrze, upewniając się, że każdej domeny jest w dobrej kondycji przed kontynuowaniem toohello dalej.</span><span class="sxs-lookup"><span data-stu-id="82e4b-226">You see how hello upgrade rolls through hello upgrade domains in your cluster, making sure each domain is healthy before proceeding toohello next.</span></span>
    <span data-ttu-id="82e4b-227">![Uaktualnij widok w narzędziu Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span><span class="sxs-lookup"><span data-stu-id="82e4b-227">![Upgrade View in Service Fabric Explorer](./media/service-fabric-quickstart-dotnet/upgrading.png)</span></span>

    <span data-ttu-id="82e4b-228">Sieć szkieletowa usług pozwala uaktualnienia bezpieczne oczekuje dwóch minut po uaktualnieniu usługi hello w każdym węźle klastra hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-228">Service Fabric makes upgrades safe by waiting two minutes after upgrading hello service on each node in hello cluster.</span></span> <span data-ttu-id="82e4b-229">Oczekiwane tootake aktualizowania hello około 8 minut.</span><span class="sxs-lookup"><span data-stu-id="82e4b-229">Expect hello entire update tootake approximately eight minutes.</span></span>

10. <span data-ttu-id="82e4b-230">Podczas uaktualniania hello, można nadal używać aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="82e4b-230">While hello upgrade is running, you can still use hello application.</span></span> <span data-ttu-id="82e4b-231">Ponieważ dwa wystąpienia usługi hello uruchomiona w klastrze hello, niektóre żądania mogą wystąpić uaktualnionej wersji aplikacji hello, podczas gdy inne osoby, może nadal otrzymywać hello starą wersję.</span><span class="sxs-lookup"><span data-stu-id="82e4b-231">Because you have two instances of hello service running in hello cluster, some of your requests may get an upgraded version of hello application, while others may still get hello old version.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82e4b-232">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="82e4b-232">Next steps</span></span>
<span data-ttu-id="82e4b-233">W tym przewodniku Szybki start zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="82e4b-233">In this quickstart, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="82e4b-234">Tworzenie aplikacji przy użyciu platformy .NET i sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="82e4b-234">Create an application using .NET and Service Fabric</span></span>
> * <span data-ttu-id="82e4b-235">Użyj jako frontonu sieci web platformy ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="82e4b-235">Use ASP.NET core as a web front-end</span></span>
> * <span data-ttu-id="82e4b-236">Przechowywanie danych aplikacji w usługi stanowej</span><span class="sxs-lookup"><span data-stu-id="82e4b-236">Store application data in a stateful service</span></span>
> * <span data-ttu-id="82e4b-237">Debugowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="82e4b-237">Debug your application locally</span></span>
> * <span data-ttu-id="82e4b-238">Wdrażanie klastra tooa aplikacji hello na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="82e4b-238">Deploy hello application tooa cluster in Azure</span></span>
> * <span data-ttu-id="82e4b-239">Aplikacja hello skalowalnego w poziomie w wielu węzłach</span><span class="sxs-lookup"><span data-stu-id="82e4b-239">Scale-out hello application across multiple nodes</span></span>
> * <span data-ttu-id="82e4b-240">Uaktualnienie stopniowe aplikacji</span><span class="sxs-lookup"><span data-stu-id="82e4b-240">Perform a rolling application upgrade</span></span>

<span data-ttu-id="82e4b-241">toolearn więcej informacji na temat sieci szkieletowej usług i .NET, zapoznaj się z informacjami w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="82e4b-241">toolearn more about Service Fabric and .NET, take a look at this tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="82e4b-242">Aplikacji .NET w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="82e4b-242">.NET application on Service Fabric</span></span>](service-fabric-tutorial-create-dotnet-app.md)