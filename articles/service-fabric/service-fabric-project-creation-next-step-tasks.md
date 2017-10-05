---
title: "Następne kroki tworzenia projektu sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera łącza do zestawu zadań związanych z projektowaniem core dla sieci szkieletowej usług"
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
ms.openlocfilehash: 74019850c507902d9ef7ec47a364fff234aaf32b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="d82de-103">Sieć szkieletowa usług aplikacji i następne kroki</span><span class="sxs-lookup"><span data-stu-id="d82de-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="d82de-104">Utworzono aplikację sieci szkieletowej usług Azure.</span><span class="sxs-lookup"><span data-stu-id="d82de-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="d82de-105">W tym artykule opisano w skład projektu i potencjalne poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="d82de-105">This article describes the makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="d82de-106">Aplikacja</span><span class="sxs-lookup"><span data-stu-id="d82de-106">Your application</span></span>
<span data-ttu-id="d82de-107">Każdej nowej aplikacji zawiera projekt aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d82de-107">Every new application includes an application project.</span></span> <span data-ttu-id="d82de-108">Może to być jeden lub dwa dodatkowe projekty, w zależności od typu wybranych usług.</span><span class="sxs-lookup"><span data-stu-id="d82de-108">There may be one or two additional projects, depending on the type of service chosen.</span></span>

### <a name="the-application-project"></a><span data-ttu-id="d82de-109">Projekt aplikacji</span><span class="sxs-lookup"><span data-stu-id="d82de-109">The application project</span></span>
<span data-ttu-id="d82de-110">Projekt aplikacji obejmuje:</span><span class="sxs-lookup"><span data-stu-id="d82de-110">The application project consists of:</span></span>

* <span data-ttu-id="d82de-111">Zestaw odwołania do usług, które składają się na aplikację.</span><span class="sxs-lookup"><span data-stu-id="d82de-111">A set of references to the services that make up your application.</span></span>
* <span data-ttu-id="d82de-112">Profilów (węzła 1 lokalnego, 5 węzła lokalnego i chmura) używanych do obsługi preferencje dotyczące pracy z różnych środowiskach — takie jak preferencje dotyczące punktu końcowego klastra oraz czy można wykonywać wdrożenia uaktualnienia domyślnie trzy publikowania.</span><span class="sxs-lookup"><span data-stu-id="d82de-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span></span>
* <span data-ttu-id="d82de-113">Parametr aplikacji trzy pliki (taki sam jak powyżej) można do obsługi konfiguracje specyficzne dla środowiska aplikacji, takie jak liczba partycji można utworzyć dla usługi.</span><span class="sxs-lookup"><span data-stu-id="d82de-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span></span>
* <span data-ttu-id="d82de-114">Skrypt wdrożenia, który służy do wdrażania aplikacji z poziomu wiersza polecenia lub w ramach automatycznych ciągłego potoku integracji i wdrażania.</span><span class="sxs-lookup"><span data-stu-id="d82de-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="d82de-115">Manifest aplikacji zawiera opis aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d82de-115">The application manifest, which describes the application.</span></span> <span data-ttu-id="d82de-116">Manifest można znaleźć w folderze ApplicationPackageRoot.</span><span class="sxs-lookup"><span data-stu-id="d82de-116">You can find the manifest under the ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="d82de-117">Usługi bezstanowej</span><span class="sxs-lookup"><span data-stu-id="d82de-117">Stateless service</span></span>
<span data-ttu-id="d82de-118">Po dodaniu nowej usługi bezstanowej Visual Studio dodaje projekt do rozwiązania, który zawiera typ podrzędne w stosunku `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="d82de-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="d82de-119">Usługa zwiększa zmienną lokalną w licznika.</span><span class="sxs-lookup"><span data-stu-id="d82de-119">The service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="d82de-120">Usługi stanowej</span><span class="sxs-lookup"><span data-stu-id="d82de-120">Stateful service</span></span>
<span data-ttu-id="d82de-121">Po dodaniu nowej usługi stanowej Visual Studio dodaje projekt do rozwiązania, który zawiera typ podrzędne w stosunku `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="d82de-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="d82de-122">Usługa zwiększa licznik w jego `RunAsync` — metoda i przechowuje wyniki w `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="d82de-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="d82de-123">Usługa aktora</span><span class="sxs-lookup"><span data-stu-id="d82de-123">Actor service</span></span>
<span data-ttu-id="d82de-124">Po dodaniu nowego niezawodnego aktora Visual Studio dodaje dwa projekty do rozwiązania: aktora projektu i projektu interfejsu.</span><span class="sxs-lookup"><span data-stu-id="d82de-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span></span>

<span data-ttu-id="d82de-125">Projektu aktora zapewnia metody ustawiania i pobierania wartości licznika, który jest niezawodnie utrwalone w ramach stanu aktora.</span><span class="sxs-lookup"><span data-stu-id="d82de-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span></span> <span data-ttu-id="d82de-126">Projekt interfejsu udostępnia interfejs, który inne usługi można użyć do wywołania aktora.</span><span class="sxs-lookup"><span data-stu-id="d82de-126">The interface project provides an interface that other services can use to invoke the actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="d82de-127">Bezstanowe interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="d82de-127">Stateless Web API</span></span>
<span data-ttu-id="d82de-128">Bezstanowych projekt interfejsu API sieci Web udostępnia usługi sieci web podstawowe, który można otworzyć aplikację dla klientów zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="d82de-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span></span> <span data-ttu-id="d82de-129">Aby uzyskać więcej informacji na temat projektu strukturę, zobacz [usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="d82de-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="d82de-130">Platformy ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="d82de-130">ASP.NET core</span></span>
<span data-ttu-id="d82de-131">Zestaw SDK sieci szkieletowej usług zawiera ten sam zestaw platformy ASP.NET Core szablonów, które są dostępne dla projektów platformy ASP.NET Core autonomicznej: pusta, [interfejsu API sieci Web][aspnet-webapi], i [aplikacji sieci Web][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="d82de-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="d82de-132">Gość kontenerów plików wykonywalnych i gościa</span><span class="sxs-lookup"><span data-stu-id="d82de-132">Guest executables and guest containers</span></span>

<span data-ttu-id="d82de-133">Usługa sieci szkieletowej "Gość" to usługa, która jest kompilowany bez modele programowania dla platformy.</span><span class="sxs-lookup"><span data-stu-id="d82de-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span></span> <span data-ttu-id="d82de-134">Pliki binarne gościa można spakować albo [bezpośrednio w pakiecie aplikacji](service-fabric-deploy-existing-app.md) lub [za pośrednictwem obrazu kontenera](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="d82de-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="d82de-135">W obu przypadkach program Visual Studio tworzy artefakty niezbędne w **ApplicationPackageRoot** folderu projektu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d82de-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span></span> <span data-ttu-id="d82de-136">Visual Studio nie utworzy nowy projekt usługi, ponieważ kod już istnieje w innym miejscu.</span><span class="sxs-lookup"><span data-stu-id="d82de-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span></span> <span data-ttu-id="d82de-137">Jeśli chcesz zarządzać projektów gościa równolegle z projektu aplikacji sieci szkieletowej usług, możesz dodać je do tego samego rozwiązania Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d82de-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d82de-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d82de-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="d82de-139">Tworzenie klastra platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d82de-139">Create an Azure cluster</span></span>
<span data-ttu-id="d82de-140">Zestaw SDK sieci szkieletowej usług zapewnia klaster lokalny projektowania i testowania.</span><span class="sxs-lookup"><span data-stu-id="d82de-140">The Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="d82de-141">Aby utworzyć klaster na platformie Azure, zobacz [konfigurowania klastra sieci szkieletowej usług w portalu Azure][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="d82de-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-to-azure"></a><span data-ttu-id="d82de-142">Publikowanie aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="d82de-142">Publish your application to Azure</span></span>
<span data-ttu-id="d82de-143">Można opublikować aplikacji bezpośrednio z programu Visual Studio z klastrem platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d82de-143">You can publish your application directly from Visual Studio to an Azure cluster.</span></span> <span data-ttu-id="d82de-144">Aby dowiedzieć się więcej, zobacz temat [publikowania aplikacji na platformie Azure][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="d82de-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a><span data-ttu-id="d82de-145">Wizualizowanie klastra za pomocą Eksploratora sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="d82de-145">Use Service Fabric Explorer to visualize your cluster</span></span>
<span data-ttu-id="d82de-146">Service Fabric Explorer oferuje prosty sposób na wizualizowanie klastra, w tym wdrożone aplikacje i fizycznego układu.</span><span class="sxs-lookup"><span data-stu-id="d82de-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="d82de-147">Aby dowiedzieć się więcej, zobacz [wizualizacja klastra przy użyciu Eksploratora usługi sieć szkieletowa][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="d82de-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="d82de-148">Wersja i uaktualniania usług</span><span class="sxs-lookup"><span data-stu-id="d82de-148">Version and upgrade your services</span></span>
<span data-ttu-id="d82de-149">Sieć szkieletowa usług umożliwia niezależnie od wersji i uaktualniania usług niezależne w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d82de-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="d82de-150">Aby dowiedzieć się więcej, zobacz [wersji i uaktualniania usług][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="d82de-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="d82de-151">Konfigurowanie ciągłej integracji z Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="d82de-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="d82de-152">Aby dowiedzieć się, jak można skonfigurować procesu ciągłej integracji aplikacji usługi Service Fabric, zobacz [skonfigurować ciągłe integrację z programem Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="d82de-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

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
