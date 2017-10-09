---
title: kroki dalej tworzenia projektu sieci szkieletowej aaaService | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera łącza tooa zestaw zadań związanych z projektowaniem core dla sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="5369f-103">Sieć szkieletowa usług aplikacji i następne kroki</span><span class="sxs-lookup"><span data-stu-id="5369f-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="5369f-104">Utworzono aplikację sieci szkieletowej usług Azure.</span><span class="sxs-lookup"><span data-stu-id="5369f-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="5369f-105">W tym artykule opisano w skład hello projektu i potencjalne poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="5369f-105">This article describes hello makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="5369f-106">Aplikacja</span><span class="sxs-lookup"><span data-stu-id="5369f-106">Your application</span></span>
<span data-ttu-id="5369f-107">Każdej nowej aplikacji zawiera projekt aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5369f-107">Every new application includes an application project.</span></span> <span data-ttu-id="5369f-108">Może to być jeden lub dwa dodatkowe projekty, w zależności od typu hello wybrane usługi.</span><span class="sxs-lookup"><span data-stu-id="5369f-108">There may be one or two additional projects, depending on hello type of service chosen.</span></span>

### <a name="hello-application-project"></a><span data-ttu-id="5369f-109">Projekt aplikacji Hello</span><span class="sxs-lookup"><span data-stu-id="5369f-109">hello application project</span></span>
<span data-ttu-id="5369f-110">Projekt aplikacji Hello obejmuje:</span><span class="sxs-lookup"><span data-stu-id="5369f-110">hello application project consists of:</span></span>

* <span data-ttu-id="5369f-111">Zestaw odwołuje się do toohello usług, które składają się na aplikację.</span><span class="sxs-lookup"><span data-stu-id="5369f-111">A set of references toohello services that make up your application.</span></span>
* <span data-ttu-id="5369f-112">Profilów (węzła 1 lokalnego, 5 węzła lokalnego i chmura) służy toomaintain preferencje dotyczące pracy z różnych środowiskach — na przykład punktu końcowego klastra pokrewne tooa preferencji i czy tooperform uaktualniania wdrożenia domyślnie trzy publikowania.</span><span class="sxs-lookup"><span data-stu-id="5369f-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use toomaintain preferences for working with different environments--such as preferences related tooa cluster endpoint and whether tooperform upgrade deployments by default.</span></span>
* <span data-ttu-id="5369f-113">Trzy pliki parametrów aplikacji (tak samo jak powyżej) można toomaintain konfiguracje specyficzne dla środowiska aplikacji, takie jak liczba hello toocreate partycji dla usługi.</span><span class="sxs-lookup"><span data-stu-id="5369f-113">Three application parameter files (same as above) that you can use toomaintain environment-specific application configurations, such as hello number of partitions toocreate for a service.</span></span>
* <span data-ttu-id="5369f-114">Skrypt wdrożenia, których można używać toodeploy z wiersza polecenia hello lub w ramach automatycznych ciągłego potoku integracji i wdrażania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5369f-114">A deployment script that you can use toodeploy your application from hello command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="5369f-115">manifest aplikacji Hello, który opisuje aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5369f-115">hello application manifest, which describes hello application.</span></span> <span data-ttu-id="5369f-116">Hello manifest można znaleźć w folderze ApplicationPackageRoot hello.</span><span class="sxs-lookup"><span data-stu-id="5369f-116">You can find hello manifest under hello ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="5369f-117">Usługi bezstanowej</span><span class="sxs-lookup"><span data-stu-id="5369f-117">Stateless service</span></span>
<span data-ttu-id="5369f-118">Po dodaniu nowej usługi bezstanowej Visual Studio dodaje rozwiązania tooyour projektu usługi, który zawiera typ podrzędne w stosunku `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="5369f-118">When you add a new stateless service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="5369f-119">Usługa Hello zwiększa zmienną lokalną w licznika.</span><span class="sxs-lookup"><span data-stu-id="5369f-119">hello service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="5369f-120">Usługi stanowej</span><span class="sxs-lookup"><span data-stu-id="5369f-120">Stateful service</span></span>
<span data-ttu-id="5369f-121">Po dodaniu nowej usługi stanowej, Visual Studio dodaje rozwiązania tooyour projektu usługi, który zawiera typ podrzędne w stosunku `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="5369f-121">When you add a new stateful service, Visual Studio adds a service project tooyour solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="5369f-122">Witaj usługi zwiększa licznik w jego `RunAsync` — metoda i magazyny wynik hello w `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="5369f-122">hello service increments a counter in its `RunAsync` method and stores hello result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="5369f-123">Usługa aktora</span><span class="sxs-lookup"><span data-stu-id="5369f-123">Actor service</span></span>
<span data-ttu-id="5369f-124">Po dodaniu nowego niezawodnego aktora Visual Studio dodaje dwa projekty tooyour rozwiązania: aktora projektu i projektu interfejsu.</span><span class="sxs-lookup"><span data-stu-id="5369f-124">When you add a new reliable actor, Visual Studio adds two projects tooyour solution: an actor project and an interface project.</span></span>

<span data-ttu-id="5369f-125">Projekt aktora Hello udostępnia metody dla ustawienia i uzyskiwanie hello wartości licznika, który jest niezawodnie utrwalone w ramach stanu aktora hello.</span><span class="sxs-lookup"><span data-stu-id="5369f-125">hello actor project provides methods for setting and getting hello value of a counter that is reliably persisted within hello actor's state.</span></span> <span data-ttu-id="5369f-126">Witaj projektu interfejsu udostępnia interfejs, że inne usługi można użyć tooinvoke hello aktora.</span><span class="sxs-lookup"><span data-stu-id="5369f-126">hello interface project provides an interface that other services can use tooinvoke hello actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="5369f-127">Bezstanowe interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="5369f-127">Stateless Web API</span></span>
<span data-ttu-id="5369f-128">Hello bezstanowych projektu interfejsu API sieci Web udostępnia podstawowego usługi, których można używać tooopen klientów tooexternal aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5369f-128">hello stateless Web API project provides a basic web service that you can use tooopen your application tooexternal clients.</span></span> <span data-ttu-id="5369f-129">Aby uzyskać więcej informacji na temat struktury projektu hello, zobacz [usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="5369f-129">For more information about how hello project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="5369f-130">Platformy ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="5369f-130">ASP.NET core</span></span>
<span data-ttu-id="5369f-131">Witaj zestawu SDK usług sieci szkieletowej udostępnia hello sam zestaw platformy ASP.NET Core szablonów, które są dostępne dla projektów platformy ASP.NET Core autonomicznej: pusta, [interfejsu API sieci Web][aspnet-webapi], i [aplikacji sieci Web][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="5369f-131">hello Service Fabric SDK provides hello same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="5369f-132">Gość kontenerów plików wykonywalnych i gościa</span><span class="sxs-lookup"><span data-stu-id="5369f-132">Guest executables and guest containers</span></span>

<span data-ttu-id="5369f-133">Usługa sieci szkieletowej "Gość" to usługa, która jest kompilowany bez modele programowania hello platformy.</span><span class="sxs-lookup"><span data-stu-id="5369f-133">A Service Fabric 'guest' is a service that is not built with hello platform's programming models.</span></span> <span data-ttu-id="5369f-134">Pliki binarne hello gościa można spakować albo [bezpośrednio w pakiecie aplikacji hello](service-fabric-deploy-existing-app.md) lub [za pośrednictwem obrazu kontenera](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="5369f-134">You can package hello binaries for a guest either [directly in hello application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="5369f-135">W obu przypadkach program Visual Studio tworzy hello artefakty niezbędne w hello **ApplicationPackageRoot** folderu projekt aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="5369f-135">In both cases, Visual Studio creates hello necessary artifacts in hello **ApplicationPackageRoot** folder of hello application project.</span></span> <span data-ttu-id="5369f-136">Visual Studio nie utworzy nowy projekt usługi, ponieważ kod hello już istnieje w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="5369f-136">Visual Studio will not create a new service project because hello code already exists elsewhere.</span></span> <span data-ttu-id="5369f-137">Jeśli chcesz toomanage użytkownika gościa projektów obok projekt aplikacji hello sieci szkieletowej usług, możesz dodać je toohello tym samym rozwiązaniu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5369f-137">If you would like toomanage your guest projects alongside hello Service Fabric application project, you can add them toohello same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5369f-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5369f-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="5369f-139">Tworzenie klastra platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5369f-139">Create an Azure cluster</span></span>
<span data-ttu-id="5369f-140">Witaj zestawu SDK usług sieci szkieletowej udostępnia klastra lokalnego dla projektowania i testowania.</span><span class="sxs-lookup"><span data-stu-id="5369f-140">hello Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="5369f-141">toocreate klastra na platformie Azure, zobacz [konfigurowania klastra sieci szkieletowej usług z portalu Azure hello][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="5369f-141">toocreate a cluster in Azure, see [Setting up a Service Fabric cluster from hello Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-tooazure"></a><span data-ttu-id="5369f-142">Publikowanie tooAzure Twojej aplikacji</span><span class="sxs-lookup"><span data-stu-id="5369f-142">Publish your application tooAzure</span></span>
<span data-ttu-id="5369f-143">Można opublikować aplikacji bezpośrednio z programu Visual Studio tooan klastrze platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5369f-143">You can publish your application directly from Visual Studio tooan Azure cluster.</span></span> <span data-ttu-id="5369f-144">toolearn, zobacz temat [publikowania tooAzure Twojej aplikacji][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="5369f-144">toolearn how, see [Publishing your application tooAzure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a><span data-ttu-id="5369f-145">Użyj Eksploratora usługi sieć szkieletowa toovisualize klastra</span><span class="sxs-lookup"><span data-stu-id="5369f-145">Use Service Fabric Explorer toovisualize your cluster</span></span>
<span data-ttu-id="5369f-146">Service Fabric Explorer oferuje łatwe toovisualize klastra, w tym wdrożone aplikacje i fizycznego układu.</span><span class="sxs-lookup"><span data-stu-id="5369f-146">Service Fabric Explorer offers an easy way toovisualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="5369f-147">toolearn więcej, zobacz [wizualizacja klastra przy użyciu Eksploratora usługi sieć szkieletowa][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="5369f-147">toolearn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="5369f-148">Wersja i uaktualniania usług</span><span class="sxs-lookup"><span data-stu-id="5369f-148">Version and upgrade your services</span></span>
<span data-ttu-id="5369f-149">Sieć szkieletowa usług umożliwia niezależnie od wersji i uaktualniania usług niezależne w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5369f-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="5369f-150">toolearn więcej, zobacz [wersji i uaktualniania usług][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="5369f-150">toolearn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="5369f-151">Konfigurowanie ciągłej integracji z Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="5369f-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="5369f-152">toolearn proces ciągłej integracji można skonfigurować dla aplikacji sieci szkieletowej usług, zobacz [skonfigurować ciągłe integrację z programem Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="5369f-152">toolearn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
