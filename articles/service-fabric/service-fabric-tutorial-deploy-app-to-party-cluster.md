---
title: "Sieć szkieletowa usług Azure tooa aplikacji klastra strona aaaDeploy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy tooa aplikacji firm klastra."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a><span data-ttu-id="f116b-103">Wdrażanie aplikacji tooa klastra strony na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f116b-103">Deploy an application tooa Party Cluster in Azure</span></span>
<span data-ttu-id="f116b-104">W tym samouczku jest częścią dwóch serii i przedstawiono toodeploy tooa aplikacji sieci szkieletowej usług Azure klastra strony na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f116b-104">This tutorial is part two of a series and shows you how toodeploy an Azure Service Fabric application tooa Party Cluster in Azure.</span></span>

<span data-ttu-id="f116b-105">W części samouczka serii hello, możesz dowiedzieć się, jak:</span><span class="sxs-lookup"><span data-stu-id="f116b-105">In part two of hello tutorial series, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="f116b-106">Wdrażanie aplikacji tooa zdalnego klastra przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f116b-106">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="f116b-107">Usuń aplikację z klastra przy użyciu Eksploratora usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="f116b-107">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="f116b-108">W tym samouczku dowiesz się, jak:</span><span class="sxs-lookup"><span data-stu-id="f116b-108">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="f116b-109">Tworzenie aplikacji sieci szkieletowej usług .NET</span><span class="sxs-lookup"><span data-stu-id="f116b-109">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * <span data-ttu-id="f116b-110">Wdrażanie klastra zdalnego tooa aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="f116b-110">Deploy hello application tooa remote cluster</span></span>
> * [<span data-ttu-id="f116b-111">Konfigurowanie elementu konfiguracji/CD za pomocą programu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="f116b-111">Configure CI/CD using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a><span data-ttu-id="f116b-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f116b-112">Prerequisites</span></span>
<span data-ttu-id="f116b-113">Przed rozpoczęciem tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="f116b-113">Before you begin this tutorial:</span></span>
- <span data-ttu-id="f116b-114">Jeśli nie masz subskrypcji platformy Azure, Utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="f116b-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="f116b-115">[Zainstaluj program Visual Studio 2017](https://www.visualstudio.com/) i zainstaluj hello **Azure programowanie** i **ASP.NET i sieć web development** obciążeń.</span><span class="sxs-lookup"><span data-stu-id="f116b-115">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="f116b-116">Zainstaluj hello zestawu SDK sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="f116b-116">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="f116b-117">Pobierz hello głosowania przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="f116b-117">Download hello Voting sample application</span></span>
<span data-ttu-id="f116b-118">Jeśli nie zbudować hello głosowania przykładowej aplikacji [część jednego z tego samouczka serii](service-fabric-tutorial-create-dotnet-app.md), można go pobrać.</span><span class="sxs-lookup"><span data-stu-id="f116b-118">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="f116b-119">W oknie polecenie Uruchom hello następujące polecenia tooclone hello przykładowej aplikacji repozytorium tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f116b-119">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a><span data-ttu-id="f116b-120">Konfigurowanie klastra strony</span><span class="sxs-lookup"><span data-stu-id="f116b-120">Set up a Party Cluster</span></span>
<span data-ttu-id="f116b-121">Klastry firm są bezpłatne, ograniczonej czasowo klastrów sieci szkieletowej usług hostowanej na platformie Azure i uruchom przez zespół usługi sieć szkieletowa hello którym każda osoba, która wdrażania aplikacji i Dowiedz się więcej o hello platformy.</span><span class="sxs-lookup"><span data-stu-id="f116b-121">Party clusters are free, limited-time Service Fabric clusters hosted on Azure and run by hello Service Fabric team where anyone can deploy applications and learn about hello platform.</span></span> <span data-ttu-id="f116b-122">Bezpłatnie!</span><span class="sxs-lookup"><span data-stu-id="f116b-122">For free!</span></span>

<span data-ttu-id="f116b-123">tooget dostępu tooa klastra strony Przeglądanie witryny toothis: http://aka.ms/tryservicefabric i wykonaj hello instrukcje tooget tooa klastra dostępu.</span><span class="sxs-lookup"><span data-stu-id="f116b-123">tooget access tooa Party Cluster, browse toothis site: http://aka.ms/tryservicefabric and follow hello instructions tooget access tooa cluster.</span></span> <span data-ttu-id="f116b-124">Należy Facebook lub GitHub konta tooget dostępu tooa strona klastra.</span><span class="sxs-lookup"><span data-stu-id="f116b-124">You need a Facebook or GitHub account tooget access tooa Party Cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="f116b-125">Klastry firm nie są zabezpieczone, dlatego aplikacji i danych, które należy umieścić w nich może być widoczny tooothers.</span><span class="sxs-lookup"><span data-stu-id="f116b-125">Party clusters are not secured, so your applications and any data you put in them may be visible tooothers.</span></span> <span data-ttu-id="f116b-126">Nie zostanie wdrożona niczego nie ma innych toosee.</span><span class="sxs-lookup"><span data-stu-id="f116b-126">Don't deploy anything you don't want others toosee.</span></span> <span data-ttu-id="f116b-127">Być tooread się za pośrednictwem szczegółowe hello naszych warunków użytkowania.</span><span class="sxs-lookup"><span data-stu-id="f116b-127">Be sure tooread over our Terms of Use for all hello details.</span></span>

## <a name="configure-hello-listening-port"></a><span data-ttu-id="f116b-128">Skonfiguruj port nasłuchujący hello</span><span class="sxs-lookup"><span data-stu-id="f116b-128">Configure hello listening port</span></span>
<span data-ttu-id="f116b-129">Po utworzeniu hello VotingWeb frontonu usługi Visual Studio losowo wybiera port toolisten usługi hello na.</span><span class="sxs-lookup"><span data-stu-id="f116b-129">When hello VotingWeb front-end service is created, Visual Studio randomly selects a port for hello service toolisten on.</span></span>  <span data-ttu-id="f116b-130">Hello usługi VotingWeb działa jako hello frontonu dla tej aplikacji i akceptuje ruch zewnętrzny, więc warto powiązać tooa tej usługi, stałe i także znać port.</span><span class="sxs-lookup"><span data-stu-id="f116b-130">hello VotingWeb service acts as hello front-end for this application and accepts external traffic, so let's bind that service tooa fixed and well-know port.</span></span> <span data-ttu-id="f116b-131">W Eksploratorze rozwiązań Otwórz *VotingWeb/PackageRoot/ServiceManifest.xml*.</span><span class="sxs-lookup"><span data-stu-id="f116b-131">In Solution Explorer, open  *VotingWeb/PackageRoot/ServiceManifest.xml*.</span></span>  <span data-ttu-id="f116b-132">Znajdź hello **punktu końcowego** zasobu w hello **zasobów** sekcji i zmień hello **portu** too80 wartość.</span><span class="sxs-lookup"><span data-stu-id="f116b-132">Find hello **Endpoint** resource in hello **Resources** section and change hello **Port** value too80.</span></span>

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="f116b-133">Również zaktualizować wartość właściwości adresu URL aplikacji hello w projekcie głosowania hello, więc przeglądarki sieci web otwiera toohello poprawnego portu podczas debugowania za pomocą "F5".</span><span class="sxs-lookup"><span data-stu-id="f116b-133">Also update hello Application URL property value in hello Voting project so a web browser opens toohello correct port when you debug using 'F5'.</span></span>  <span data-ttu-id="f116b-134">W Eksploratorze rozwiązań wybierz hello **głosowania** hello projektu i zaktualizuj **adres URL aplikacji** właściwości.</span><span class="sxs-lookup"><span data-stu-id="f116b-134">In Solution Explorer, select hello **Voting** project and update hello **Application URL** property.</span></span>

![Adres URL aplikacji](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a><span data-ttu-id="f116b-136">Wdrażanie toohello aplikacji hello Azure</span><span class="sxs-lookup"><span data-stu-id="f116b-136">Deploy hello app toohello Azure</span></span>
<span data-ttu-id="f116b-137">Teraz, aplikacja hello jest gotowy, można wdrożyć toohello strona klastra bezpośrednio z programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f116b-137">Now that hello application is ready, you can deploy it toohello Party Cluster direct from Visual Studio.</span></span>

1. <span data-ttu-id="f116b-138">Kliknij prawym przyciskiem myszy **głosowania** w hello Eksploratorze rozwiązań i wybierz polecenie **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="f116b-138">Right-click **Voting** in hello Solution Explorer and choose **Publish**.</span></span>

    ![Okno dialogowe Publikowanie](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. <span data-ttu-id="f116b-140">Typ w hello punktu końcowego połączenia hello klastra strony w hello **punktu końcowego połączenia** a następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="f116b-140">Type in hello Connection Endpoint of hello Party Cluster in hello **Connection Endpoint** field and click **Publish**.</span></span>

    <span data-ttu-id="f116b-141">Po hello Publikowanie zakończone, należy stanie toosend aplikacją toohello żądanie za pośrednictwem przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="f116b-141">Once hello publish has finished, you should be able toosend a request toohello application via a browser.</span></span>

3. <span data-ttu-id="f116b-142">Otwórz preferowane przeglądarkę i wprowadź adres klastra hello (hello punktu końcowego połączenia bez informacji o porcie hello — na przykład win1kw5649s.westus.cloudapp.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f116b-142">Open you preferred browser and type in hello cluster address (hello connection endpoint without hello port information - for example, win1kw5649s.westus.cloudapp.azure.com).</span></span>

    <span data-ttu-id="f116b-143">Powinna zostać wyświetlona hello powoduje takie same, jak przedstawiono przy uruchamianiu aplikacji hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f116b-143">You should now see hello same result as you saw when running hello application locally.</span></span>

    ![Interfejs API odpowiedzi z klastra](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="f116b-145">Usuwanie aplikacji hello z klastra za pomocą Eksploratora usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="f116b-145">Remove hello application from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="f116b-146">Eksploratora usługi sieć szkieletowa jest tooexplore interfejsu graficznego użytkownika aplikacji i zarządzanie nimi w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="f116b-146">Service Fabric Explorer is a graphical user interface tooexplore and manage applications in a Service Fabric cluster.</span></span>

<span data-ttu-id="f116b-147">Aplikacja hello tooremove z hello strona klastra:</span><span class="sxs-lookup"><span data-stu-id="f116b-147">tooremove hello application from hello Party Cluster:</span></span>

1. <span data-ttu-id="f116b-148">Przeglądaj toohello Service Fabric Explorer, za pomocą łącza hello dostarczonych przez stronę tworzenia konta hello strona klastra.</span><span class="sxs-lookup"><span data-stu-id="f116b-148">Browse toohello Service Fabric Explorer, using hello link provided by hello Party Cluster sign-up page.</span></span> <span data-ttu-id="f116b-149">Na przykład http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="f116b-149">For example, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.</span></span>

2. <span data-ttu-id="f116b-150">W narzędziu Service Fabric Explorer, przejdź toohello **fabric://Voting** węzła w elemencie treeview hello na powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="f116b-150">In Service Fabric Explorer, navigate toohello **fabric://Voting** node in hello treeview on hello left-hand side.</span></span>

3. <span data-ttu-id="f116b-151">Kliknij przycisk hello **akcji** przycisku na powitania po prawej stronie **Essentials** okienko i wybierz polecenie **Usuń aplikację**.</span><span class="sxs-lookup"><span data-stu-id="f116b-151">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Delete Application**.</span></span> <span data-ttu-id="f116b-152">Potwierdź usunięcie hello wystąpienia aplikacji, co spowoduje usunięcie wystąpienia hello naszej aplikacji uruchomionych w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="f116b-152">Confirm deleting hello application instance, which removes hello instance of our application running in hello cluster.</span></span>

![Usuwanie aplikacji w narzędziu Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a><span data-ttu-id="f116b-154">Usuń typ aplikacji hello z klastra przy użyciu Eksploratora usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="f116b-154">Remove hello application type from a cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="f116b-155">Jako typy aplikacji w klastrze usługi sieć szkieletowa, dzięki czemu można toohave wiele wystąpień i wersji aplikacji hello uruchomiona w klastrze hello wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f116b-155">Applications are deployed as application types in a Service Fabric cluster, which enables you toohave multiple instances and versions of hello application running within hello cluster.</span></span> <span data-ttu-id="f116b-156">Po usunięto hello uruchomione wystąpienie aplikacji, firma Microsoft również usunąć hello typu oczyszczania hello toocomplete hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="f116b-156">After having removed hello running instance of our application, we can also remove hello type, toocomplete hello cleanup of hello deployment.</span></span>

<span data-ttu-id="f116b-157">Aby uzyskać więcej informacji na temat modelu aplikacji hello w sieci szkieletowej usług, zobacz [modelu aplikacji w sieci szkieletowej usług](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="f116b-157">For more information about hello application model in Service Fabric, see [Model an application in Service Fabric](service-fabric-application-model.md).</span></span>

1. <span data-ttu-id="f116b-158">Przejdź toohello **VotingType** węzła w elemencie treeview hello.</span><span class="sxs-lookup"><span data-stu-id="f116b-158">Navigate toohello **VotingType** node in hello treeview.</span></span>

2. <span data-ttu-id="f116b-159">Kliknij przycisk hello **akcji** przycisku na powitania po prawej stronie **Essentials** okienko i wybierz polecenie **Cofnij Aprowizację typu**.</span><span class="sxs-lookup"><span data-stu-id="f116b-159">Click hello **Action** button in hello right-hand **Essentials** pane, and choose **Unprovision Type**.</span></span> <span data-ttu-id="f116b-160">Potwierdź cofanie aprowizacji typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f116b-160">Confirm unprovisioning hello application type.</span></span>

![Cofnij aprowizację typu aplikacji w narzędziu Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

<span data-ttu-id="f116b-162">To jest zakończenie samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="f116b-162">This concludes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f116b-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f116b-163">Next steps</span></span>
<span data-ttu-id="f116b-164">W niniejszym samouczku zawarto informacje na temat wykonywania następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="f116b-164">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f116b-165">Wdrażanie aplikacji tooa zdalnego klastra przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f116b-165">Deploy an application tooa remote cluster using Visual Studio</span></span>
> * <span data-ttu-id="f116b-166">Usuń aplikację z klastra przy użyciu Eksploratora usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="f116b-166">Remove an application from a cluster using Service Fabric Explorer</span></span>

<span data-ttu-id="f116b-167">Następny samouczek toohello wyprzedzeniem:</span><span class="sxs-lookup"><span data-stu-id="f116b-167">Advance toohello next tutorial:</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="f116b-168">Konfigurowanie ciągłej integracji przy użyciu programu Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="f116b-168">Set up continuous integration using Visual Studio Team Services</span></span>](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)