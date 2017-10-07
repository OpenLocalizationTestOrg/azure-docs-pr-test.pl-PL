---
title: "aaaQuickly wdrażanie istniejącego klastra usługi sieć szkieletowa usług Azure tooan aplikacji"
description: "Sieć szkieletowa usług Azure klastra toohost istniejącą aplikację Node.js za pomocą programu Visual Studio."
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="0320c-103">Hostowanie aplikacji w technologii Node.js w usłudze Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0320c-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="0320c-104">Ta opcja szybkiego startu ułatwia wdrożenie klastra usługi sieć szkieletowa istniejących tooa (Node.js w tym przykładzie) aplikacji działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0320c-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0320c-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0320c-105">Prerequisites</span></span>

<span data-ttu-id="0320c-106">Przed rozpoczęciem upewnij się, że masz [skonfigurowane środowisko programowania](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0320c-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="0320c-107">W tym zainstalowanie hello zestawu SDK usług sieci szkieletowej i Visual Studio 2017 lub 2015.</span><span class="sxs-lookup"><span data-stu-id="0320c-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="0320c-108">Należy również toohave istniejącą aplikację Node.js do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0320c-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="0320c-109">Przewodnik Szybki Start używa prostej witryny sieci Web w technologii Node.js, którą można pobrać [stąd][download-sample].</span><span class="sxs-lookup"><span data-stu-id="0320c-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="0320c-110">Wyodrębnij tooyour tego pliku `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder po utworzeniu projektu hello w hello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="0320c-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="0320c-111">Jeśli nie masz subskrypcji platformy Azure, utwórz [bezpłatne konto][create-account].</span><span class="sxs-lookup"><span data-stu-id="0320c-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="0320c-112">Tworzenie usługi hello</span><span class="sxs-lookup"><span data-stu-id="0320c-112">Create hello service</span></span>

<span data-ttu-id="0320c-113">Uruchom program Visual Studio jako **administrator**.</span><span class="sxs-lookup"><span data-stu-id="0320c-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="0320c-114">Tworzenie projektu przy użyciu klawiszy `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="0320c-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="0320c-115">W hello **nowy projekt** okno dialogowe, wybierz **chmury > aplikacji sieci szkieletowej usług**.</span><span class="sxs-lookup"><span data-stu-id="0320c-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="0320c-116">Nadaj nazwę aplikacji hello **MyGuestApp** i naciśnij klawisz **OK**.</span><span class="sxs-lookup"><span data-stu-id="0320c-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="0320c-117">Łatwo mogą być dzielone limit 260 znaków hello dla ścieżek zawierających system windows ma node.js.</span><span class="sxs-lookup"><span data-stu-id="0320c-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="0320c-118">Użyj krótkiej ścieżki dla projektu hello, takiego jak **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="0320c-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Okno dialogowe nowego projektu w programie Visual Studio][new-project]

<span data-ttu-id="0320c-120">Można utworzyć dowolnego typu usługi sieć szkieletowa usług z hello następnego okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0320c-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="0320c-121">Na potrzeby tego przewodnika Szybki start wybierz pozycję **Wykonywalna gościa**.</span><span class="sxs-lookup"><span data-stu-id="0320c-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="0320c-122">Nazwa usługi hello **MyGuestService** i ustawianie opcji hello na powitania prawo toohello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="0320c-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="0320c-123">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="0320c-123">Setting</span></span>                   | <span data-ttu-id="0320c-124">Wartość</span><span class="sxs-lookup"><span data-stu-id="0320c-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="0320c-125">Folder pakietu kodu</span><span class="sxs-lookup"><span data-stu-id="0320c-125">Code Package Folder</span></span>       | <span data-ttu-id="0320c-126">_&lt;folder Hello z aplikacji Node.js&gt;_</span><span class="sxs-lookup"><span data-stu-id="0320c-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="0320c-127">Zachowanie pakietu kodu</span><span class="sxs-lookup"><span data-stu-id="0320c-127">Code Package Behavior</span></span>     | <span data-ttu-id="0320c-128">Skopiuj folder zawartości tooproject</span><span class="sxs-lookup"><span data-stu-id="0320c-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="0320c-129">Program</span><span class="sxs-lookup"><span data-stu-id="0320c-129">Program</span></span>                   | <span data-ttu-id="0320c-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="0320c-130">node.exe</span></span> |
| <span data-ttu-id="0320c-131">Argumenty</span><span class="sxs-lookup"><span data-stu-id="0320c-131">Arguments</span></span>                 | <span data-ttu-id="0320c-132">server.js</span><span class="sxs-lookup"><span data-stu-id="0320c-132">server.js</span></span> |
| <span data-ttu-id="0320c-133">Folder roboczy</span><span class="sxs-lookup"><span data-stu-id="0320c-133">Working Folder</span></span>            | <span data-ttu-id="0320c-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="0320c-134">CodePackage</span></span> |

<span data-ttu-id="0320c-135">Naciśnij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0320c-135">Press **OK**.</span></span>

![Okno dialogowe nowej usługi w programie Visual Studio][new-service]

<span data-ttu-id="0320c-137">Visual Studio tworzy projekt aplikacji hello i projekt usługi aktora hello i wyświetla je w Eksploratorze rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="0320c-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="0320c-138">Projekt aplikacji Hello (**MyGuestApp**) nie zawiera żadnego kodu bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="0320c-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="0320c-139">Zamiast tego odwołuje się do zestawu projektów usług.</span><span class="sxs-lookup"><span data-stu-id="0320c-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="0320c-140">Ponadto zawiera trzy inne typy zawartości:</span><span class="sxs-lookup"><span data-stu-id="0320c-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="0320c-141">**Profile publikowania**</span><span class="sxs-lookup"><span data-stu-id="0320c-141">**Publish profiles**</span></span>  
<span data-ttu-id="0320c-142">Preferencje narzędzi dla różnych środowisk.</span><span class="sxs-lookup"><span data-stu-id="0320c-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="0320c-143">**Skrypty**</span><span class="sxs-lookup"><span data-stu-id="0320c-143">**Scripts**</span></span>  
<span data-ttu-id="0320c-144">Skrypt programu PowerShell przeznaczony do wdrażania/uaktualniania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0320c-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="0320c-145">**Definicja aplikacji**</span><span class="sxs-lookup"><span data-stu-id="0320c-145">**Application definition**</span></span>  
<span data-ttu-id="0320c-146">Zawiera manifest aplikacji hello w ramach *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="0320c-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="0320c-147">Pliki parametru skojarzonej aplikacji znajdują się w obszarze *ApplicationParameters*, który Definiowanie aplikacji hello i pozwala tooconfigure specjalnie dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="0320c-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="0320c-148">Omówienie hello zawartości projektu usługi hello, zobacz [Rozpoczynanie pracy z usługami Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="0320c-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="0320c-149">Konfigurowanie zasobów sieciowych</span><span class="sxs-lookup"><span data-stu-id="0320c-149">Set up networking</span></span>

<span data-ttu-id="0320c-150">przykład Witaj aplikacja Node.js jest wdrażany firma Microsoft korzysta z portu **80** i potrzebujemy tootell usługi Service Fabric, czego potrzebujemy portem udostępnianym.</span><span class="sxs-lookup"><span data-stu-id="0320c-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="0320c-151">Otwórz hello **ServiceManifest.xml** plik w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="0320c-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="0320c-152">Dole hello manifestu hello jest `<Resources> \ <Endpoints>` z wpisu, który został już zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="0320c-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="0320c-153">Zmodyfikuj ten wpis tooadd `Port`, `Protocol`, i `Type`.</span><span class="sxs-lookup"><span data-stu-id="0320c-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="0320c-154">Wdrażanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="0320c-154">Deploy tooAzure</span></span>

<span data-ttu-id="0320c-155">Jeśli naciśniesz **F5** i uruchomić projekt hello, jest wdrożone toohello klastra lokalnego.</span><span class="sxs-lookup"><span data-stu-id="0320c-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="0320c-156">Jednak wdróżmy tooAzure zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="0320c-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="0320c-157">Kliknij prawym przyciskiem myszy na powitania projektu i wybierz polecenie **publikowania...**  otwierający tooAzure toopublish okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0320c-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![Publikowanie tooazure okno dialogowe Usługa sieci szkieletowej usług][publish]

<span data-ttu-id="0320c-159">Wybierz hello **PublishProfiles\Cloud.xml** docelowego profilu.</span><span class="sxs-lookup"><span data-stu-id="0320c-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="0320c-160">Jeśli jeszcze nie zostało to wcześniej, wybierz toodeploy konto platformy Azure do.</span><span class="sxs-lookup"><span data-stu-id="0320c-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="0320c-161">Jeśli nie masz jeszcze konta, [utwórz je][create-account].</span><span class="sxs-lookup"><span data-stu-id="0320c-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="0320c-162">W obszarze **punktu końcowego połączenia**, wybierz hello toodeploy klastra sieci szkieletowej usług do.</span><span class="sxs-lookup"><span data-stu-id="0320c-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="0320c-163">Jeśli nie masz, wybierz  **&lt;Utwórz nowy klaster... &gt;**  który otwiera toohello okna przeglądarki sieci web portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0320c-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="0320c-164">Aby uzyskać więcej informacji, zobacz [utworzyć klaster w portalu hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0320c-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="0320c-165">Podczas tworzenia klastra usługi sieć szkieletowa hello, upewnij się, że hello tooset **niestandardowe punkty końcowe** ustawienie zbyt**80**.</span><span class="sxs-lookup"><span data-stu-id="0320c-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![Konfiguracja typu węzła usługi sieci szkieletowej z niestandardowym punktem końcowym][custom-endpoint]

<span data-ttu-id="0320c-167">Tworzenie nowego klastra usługi sieć szkieletowa przyjmuje niektórych toocomplete czasu.</span><span class="sxs-lookup"><span data-stu-id="0320c-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="0320c-168">Po został utworzony, przejdź wstecz toohello okna dialogowego publikowania i wybierz  **&lt;Odśwież&gt;**.</span><span class="sxs-lookup"><span data-stu-id="0320c-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="0320c-169">Hello nowy klaster znajduje się w polu listy rozwijanej hello; Wybierz go.</span><span class="sxs-lookup"><span data-stu-id="0320c-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="0320c-170">Naciśnij klawisz **publikowania** i poczekaj, aż hello toofinish wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0320c-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="0320c-171">Może to potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0320c-171">This may take a few minutes.</span></span> <span data-ttu-id="0320c-172">Po jej zakończeniu, może upłynąć kilka minut dla toobe aplikacji hello pełni dostępna.</span><span class="sxs-lookup"><span data-stu-id="0320c-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="0320c-173">Test hello witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="0320c-173">Test hello website</span></span>

<span data-ttu-id="0320c-174">Po opublikowaniu usługi przetestuj ją w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="0320c-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="0320c-175">Najpierw otwórz hello portalu Azure i Znajdź usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="0320c-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="0320c-176">Przejdź do bloku omówienie hello hello adresu usługi.</span><span class="sxs-lookup"><span data-stu-id="0320c-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="0320c-177">Użyj nazwy domeny hello z hello _punktu końcowego połączenia klienta_ właściwości.</span><span class="sxs-lookup"><span data-stu-id="0320c-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="0320c-178">Na przykład `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="0320c-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Usługa sieci szkieletowej omówienie bloku na powitania portalu Azure][overview]

<span data-ttu-id="0320c-180">Przejdź do adresu toothis gdzie zobaczysz hello `HELLO WORLD` odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="0320c-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="0320c-181">Usuń klaster hello</span><span class="sxs-lookup"><span data-stu-id="0320c-181">Delete hello cluster</span></span>

<span data-ttu-id="0320c-182">Nie zapomnij toodelete wszystkie zasoby hello, utworzone dla tego przewodnika Szybki Start, jak naliczane są opłaty za te zasoby.</span><span class="sxs-lookup"><span data-stu-id="0320c-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0320c-183">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0320c-183">Next steps</span></span>
<span data-ttu-id="0320c-184">Przeczytaj więcej na temat [plików wykonywalnych gościa](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="0320c-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F