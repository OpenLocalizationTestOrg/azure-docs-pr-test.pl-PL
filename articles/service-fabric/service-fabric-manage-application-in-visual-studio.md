---
title: aaaManage aplikacji w programie Visual Studio | Dokumentacja firmy Microsoft
description: "Użyj toocreate programu Visual Studio, tworzenie pakietów, wdrażanie i debugowanie usług i aplikacji sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: b2d5803d85e4f9645dcbece33a2208bc0955498d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-visual-studio-toosimplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="54f02-103">Użyj zapisu toosimplify programu Visual Studio i zarządzanie aplikacjami sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="54f02-103">Use Visual Studio toosimplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="54f02-104">Można zarządzać sieć szkieletowa usług Azure, aplikacji i usług za pomocą programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54f02-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="54f02-105">Po wprowadzeniu [Konfigurowanie środowiska deweloperskiego](service-fabric-get-started.md), korzystają z programu Visual Studio toocreate sieci szkieletowej usług aplikacji, Dodaj rejestru usług lub pakiet i wdrażania aplikacji w klastrze lokalnym programowanie.</span><span class="sxs-lookup"><span data-stu-id="54f02-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio toocreate Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="54f02-106">Wdrażanie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="54f02-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="54f02-107">Domyślnie wdrażanie aplikacji łączy hello w jednej operacji proste wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="54f02-107">By default, deploying an application combines hello following steps into one simple operation:</span></span>

1. <span data-ttu-id="54f02-108">Tworzenie pakietu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="54f02-108">Creating hello application package</span></span>
2. <span data-ttu-id="54f02-109">Przekazywanie hello pakietu toohello obrazu sklepu z aplikacjami</span><span class="sxs-lookup"><span data-stu-id="54f02-109">Uploading hello application package toohello image store</span></span>
3. <span data-ttu-id="54f02-110">Rejestracja typu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="54f02-110">Registering hello application type</span></span>
4. <span data-ttu-id="54f02-111">Usunąć wszystkie uruchomione wystąpienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="54f02-111">Removing any running application instances</span></span>
5. <span data-ttu-id="54f02-112">Tworzenie wystąpienia aplikacji</span><span class="sxs-lookup"><span data-stu-id="54f02-112">Creating an application instance</span></span>

<span data-ttu-id="54f02-113">W programie Visual Studio naciskając klawisz **F5** wdraża aplikację i Dołącz hello debugera tooall aplikacji wystąpień.</span><span class="sxs-lookup"><span data-stu-id="54f02-113">In Visual Studio, pressing **F5** deploys your application and attach hello debugger tooall application instances.</span></span> <span data-ttu-id="54f02-114">Można użyć **Ctrl + F5** toodeploy aplikacji bez debugowania lub możesz opublikować tooa lokalnego lub zdalnego klastra przy użyciu hello profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="54f02-114">You can use **Ctrl+F5** toodeploy an application without debugging, or you can publish tooa local or remote cluster by using hello publish profile.</span></span> <span data-ttu-id="54f02-115">Aby uzyskać więcej informacji, zobacz [publikowanie aplikacji tooa zdalnego klastra przy użyciu programu Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="54f02-115">For more information, see [Publish an application tooa remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="54f02-116">Tryb debugowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="54f02-116">Application Debug Mode</span></span>
<span data-ttu-id="54f02-117">Visual Studio Udostępnij właściwość o nazwie **tryb debugowania aplikacji**, która kontroluje sposób wdrażania aplikacji toohandle programu Visual Studio w ramach debugowania.</span><span class="sxs-lookup"><span data-stu-id="54f02-117">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios toohandle Application deployment as part of debugging.</span></span>

#### <a name="tooset-hello-application-debug-mode-property"></a><span data-ttu-id="54f02-118">Witaj tooset właściwość tryb debugowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="54f02-118">tooset hello Application Debug Mode property</span></span>
1. <span data-ttu-id="54f02-119">Na powitania sieci szkieletowej usług aplikacji projektu (*.sfproj) menu skrótów wybierz **właściwości** (lub naciśnij klawisz hello **F4** klucza).</span><span class="sxs-lookup"><span data-stu-id="54f02-119">On hello Service Fabric application project's (*.sfproj) shortcut menu, choose **Properties** (or press hello **F4** key).</span></span>
2. <span data-ttu-id="54f02-120">W hello **właściwości** okna, zestaw hello **tryb debugowania aplikacji** właściwości.</span><span class="sxs-lookup"><span data-stu-id="54f02-120">In hello **Properties** window, set hello **Application Debug Mode** property.</span></span>

![Ustaw właściwość tryb debugowania aplikacji][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="54f02-122">Tryb debugowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="54f02-122">Application Debug Modes</span></span>

1. <span data-ttu-id="54f02-123">**Odświeżanie aplikacji** tego trybu umożliwia zmianę tooquickly i debugować kod i obsługuje edycję plików statycznych sieci web podczas debugowania.</span><span class="sxs-lookup"><span data-stu-id="54f02-123">**Refresh Application** This mode enables you tooquickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="54f02-124">W tym trybie działa tylko, jeśli klaster lokalny rozwój jest w [tryb węzła 1](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="54f02-124">This mode only works if your local development cluster is in [1-Node mode](/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="54f02-125">**Usuń aplikację** przyczyny hello usuwane, gdy kończy się sesja debugowania hello toobe aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54f02-125">**Remove Application** causes hello application toobe removed when hello debug session ends.</span></span>
3. <span data-ttu-id="54f02-126">**Automatyczne uaktualnienie** aplikacji hello nadal toorun podczas kończenia hello sesji debugowania.</span><span class="sxs-lookup"><span data-stu-id="54f02-126">**Auto Upgrade** hello application continues toorun when hello debug session ends.</span></span> <span data-ttu-id="54f02-127">Witaj następnej sesji debugowania, będą traktować wdrożenia hello uaktualnienie.</span><span class="sxs-lookup"><span data-stu-id="54f02-127">hello next debug session will treat hello deployment as an upgrade.</span></span> <span data-ttu-id="54f02-128">proces uaktualniania Hello zachowuje dane, które wprowadzono w poprzedniej sesji debugowania.</span><span class="sxs-lookup"><span data-stu-id="54f02-128">hello upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="54f02-129">**Zachowaj aplikacji** hello przechowuje aplikacji uruchomionych w klastrze hello gdy hello debugowania zakończenia sesji.</span><span class="sxs-lookup"><span data-stu-id="54f02-129">**Keep Application** hello application keeps running in hello cluster when hello debug session ends.</span></span> <span data-ttu-id="54f02-130">Początek hello hello następnej sesji debugowania, aplikacja hello zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="54f02-130">At hello beginning of hello next debug session, hello application will be removed.</span></span>

<span data-ttu-id="54f02-131">Aby uzyskać **automatycznego uaktualnienia** dane zostaną zachowane, stosując możliwości uaktualnienia aplikacji hello sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="54f02-131">For **Auto Upgrade** data is preserved by applying hello application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="54f02-132">Aby uzyskać więcej informacji o uaktualnianiu aplikacji i jak może wykonać uaktualnienie w środowisku prawdziwe, zobacz [uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="54f02-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-tooyour-service-fabric-application"></a><span data-ttu-id="54f02-133">Dodaj tooyour usługi sieć szkieletowa usług aplikacji</span><span class="sxs-lookup"><span data-stu-id="54f02-133">Add a service tooyour Service Fabric application</span></span>
<span data-ttu-id="54f02-134">Można dodać nowych usług tooyour aplikacji tooextend jego funkcjonalność.</span><span class="sxs-lookup"><span data-stu-id="54f02-134">You can add new services tooyour application tooextend its functionality.</span></span>  <span data-ttu-id="54f02-135">tooensure, czy usługa hello jest uwzględniona w pakiet aplikacji, Dodaj hello usługi za pośrednictwem hello **nowa sieci szkieletowej usług...**  elementu menu.</span><span class="sxs-lookup"><span data-stu-id="54f02-135">tooensure that hello service is included in your application package, add hello service through hello **New Fabric Service...** menu item.</span></span>

![Dodaj nową usługę sieci szkieletowej usług][newservice]

<span data-ttu-id="54f02-137">Wybierz aplikację tooyour tooadd typ projektu sieci szkieletowej usług i określ nazwę usługi hello.</span><span class="sxs-lookup"><span data-stu-id="54f02-137">Select a Service Fabric project type tooadd tooyour application, and specify a name for hello service.</span></span>  <span data-ttu-id="54f02-138">Zobacz [Wybieranie framework usługi](service-fabric-choose-framework.md) toohelp zdecydujesz usługi, która wpisz toouse.</span><span class="sxs-lookup"><span data-stu-id="54f02-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) toohelp you decide which service type toouse.</span></span>

![Wybierz aplikację tooyour tooadd typ projektu sieci szkieletowej usług usługi][addserviceproject]

<span data-ttu-id="54f02-140">Nowa usługa Hello jest dodawany tooyour rozwiązanie i istniejący pakiet aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54f02-140">hello new service is added tooyour solution and existing application package.</span></span> <span data-ttu-id="54f02-141">odwołania do usług Hello i domyślnego wystąpienia usługi będzie dodany toohello manifest aplikacji, powodując toobe usługi hello utworzeniu i uruchomieniu hello następnym wdrażania aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="54f02-141">hello service references and a default service instance will be added toohello application manifest, causing hello service toobe created and started hello next time you deploy hello application.</span></span>

![Nowa usługa Hello jest dodawany tooyour manifest aplikacji][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="54f02-143">Pakiet aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="54f02-143">Package your Service Fabric application</span></span>
<span data-ttu-id="54f02-144">Aplikacja hello toodeploy i jej usług tooa klastra, należy toocreate pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54f02-144">toodeploy hello application and its services tooa cluster, you need toocreate an application package.</span></span>  <span data-ttu-id="54f02-145">Pakiet HELLO organizuje manifest aplikacji hello, manifesty usługi i inne niezbędne pliki w określonym układzie.</span><span class="sxs-lookup"><span data-stu-id="54f02-145">hello package organizes hello application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="54f02-146">Visual Studio konfiguruje i zarządza hello pakietu w folderze projekt aplikacji hello w katalogu "pkg" hello.</span><span class="sxs-lookup"><span data-stu-id="54f02-146">Visual Studio sets up and manages hello package in hello application project's folder, in hello 'pkg' directory.</span></span>  <span data-ttu-id="54f02-147">Kliknięcie przycisku **pakietu** z hello **aplikacji** tworzy menu kontekstowego lub aktualizacje hello pakietu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54f02-147">Clicking **Package** from hello **Application** context menu creates or updates hello application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="54f02-148">Usuwanie aplikacji i typów aplikacji, w Eksploratorze chmury</span><span class="sxs-lookup"><span data-stu-id="54f02-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="54f02-149">Można wykonać operacji zarządzania podstawowy klaster z poziomu programu Visual Studio za pomocą Eksploratora chmury, które można uruchomić z hello **widoku** menu.</span><span class="sxs-lookup"><span data-stu-id="54f02-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from hello **View** menu.</span></span> <span data-ttu-id="54f02-150">Na przykład można usunąć aplikacji i wstrzymał obsługi administracyjnej typy aplikacji w klastrze lokalnym lub zdalnym.</span><span class="sxs-lookup"><span data-stu-id="54f02-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Usuwanie aplikacji][removeapplication]

> [!TIP]
> <span data-ttu-id="54f02-152">Aby uzyskać bardziej rozbudowane funkcje zarządzania klastrem, zobacz [wizualizacja klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="54f02-152">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="54f02-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54f02-153">Next steps</span></span>
* [<span data-ttu-id="54f02-154">Model aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="54f02-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="54f02-155">Wdrażanie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="54f02-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="54f02-156">Zarządzanie parametry aplikacji dla wielu środowisk</span><span class="sxs-lookup"><span data-stu-id="54f02-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="54f02-157">Debugowanie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="54f02-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="54f02-158">Wizualizacja klastra przy użyciu Eksploratora usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="54f02-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png