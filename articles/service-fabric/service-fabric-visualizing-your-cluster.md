---
title: "aaaVisualizing klastra za pomocą Eksploratora usługi sieć szkieletowa | Dokumentacja firmy Microsoft"
description: "Eksploratora usługi sieć szkieletowa jest oparte na sieci web narzędzie do sprawdzania i zarządzanie aplikacjami w chmurze i węzłów w klastrze usługi sieć szkieletowa usług Microsoft Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a><span data-ttu-id="05bc0-103">Wizualizowanie klastra przy użyciu narzędzia Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="05bc0-103">Visualize your cluster with Service Fabric Explorer</span></span>
<span data-ttu-id="05bc0-104">Eksploratora usługi sieć szkieletowa jest oparte na sieci web narzędzie do sprawdzania i zarządzanie aplikacjami i węzły w klastrze usługi sieć szkieletowa usług Azure.</span><span class="sxs-lookup"><span data-stu-id="05bc0-104">Service Fabric Explorer is a web-based tool for inspecting and managing applications and nodes in an Azure Service Fabric cluster.</span></span> <span data-ttu-id="05bc0-105">Service Fabric Explorer znajduje się bezpośrednio w klastrze hello, dzięki czemu jest zawsze dostępne, niezależnie od tego, w którym jest uruchomiona klastra.</span><span class="sxs-lookup"><span data-stu-id="05bc0-105">Service Fabric Explorer is hosted directly within hello cluster, so it is always available, regardless of where your cluster is running.</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="05bc0-106">Samouczek wideo</span><span class="sxs-lookup"><span data-stu-id="05bc0-106">Video tutorial</span></span>

<span data-ttu-id="05bc0-107">jak toouse Service Fabric Explorer, obejrzyj toolearn hello po wideo Microsoft Virtual Academy:</span><span class="sxs-lookup"><span data-stu-id="05bc0-107">toolearn how toouse Service Fabric Explorer, watch hello following Microsoft Virtual Academy video:</span></span>

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a><span data-ttu-id="05bc0-108">Połącz tooService Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="05bc0-108">Connect tooService Fabric Explorer</span></span>
<span data-ttu-id="05bc0-109">Jeśli zostały wykonane instrukcje hello zbyt[przygotowywanie środowiska projektowego](service-fabric-get-started.md), Service Fabric Explorer można uruchomić w klastrze lokalnym, przechodząc toohttp://localhost:19080 / Explorer.</span><span class="sxs-lookup"><span data-stu-id="05bc0-109">If you have followed hello instructions too[prepare your development environment](service-fabric-get-started.md), you can launch Service Fabric Explorer on your local cluster by navigating toohttp://localhost:19080/Explorer.</span></span>

## <a name="understand-hello-service-fabric-explorer-layout"></a><span data-ttu-id="05bc0-110">Zrozumienie hello układu Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="05bc0-110">Understand hello Service Fabric Explorer layout</span></span>
<span data-ttu-id="05bc0-111">Za pomocą Eksploratora usługi sieć szkieletowa można nawigować przy użyciu hello drzewa po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="05bc0-111">You can navigate through Service Fabric Explorer by using hello tree on hello left.</span></span> <span data-ttu-id="05bc0-112">Witaj katalogu głównego drzewa hello pulpit nawigacyjny klastra hello zawiera omówienie klastra, w tym podsumowanie aplikacji i kondycji węzła.</span><span class="sxs-lookup"><span data-stu-id="05bc0-112">At hello root of hello tree, hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span>

![Pulpit nawigacyjny klastra Service Fabric Explorer][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a><span data-ttu-id="05bc0-114">Wyświetl układ hello klastra</span><span class="sxs-lookup"><span data-stu-id="05bc0-114">View hello cluster's layout</span></span>
<span data-ttu-id="05bc0-115">Węzły w klastrze usługi sieć szkieletowa usług są umieszczane między dwuwymiarowa siatki domen błędów i uaktualnienia domen.</span><span class="sxs-lookup"><span data-stu-id="05bc0-115">Nodes in a Service Fabric cluster are placed across a two-dimensional grid of fault domains and upgrade domains.</span></span> <span data-ttu-id="05bc0-116">Ten umieszczania gwarantuje, że aplikacje pozostają dostępne w obecności hello awarie sprzętu i uaktualnień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="05bc0-116">This placement ensures that your applications remain available in hello presence of hardware failures and application upgrades.</span></span> <span data-ttu-id="05bc0-117">Możesz wyświetlić bieżący klaster hello układ przy użyciu mapy klastra hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-117">You can view how hello current cluster is laid out by using hello cluster map.</span></span>

![Mapa klastra Service Fabric Explorer][sfx-cluster-map]

### <a name="view-applications-and-services"></a><span data-ttu-id="05bc0-119">Wyświetl aplikacje i usługi</span><span class="sxs-lookup"><span data-stu-id="05bc0-119">View applications and services</span></span>
<span data-ttu-id="05bc0-120">Witaj klaster zawiera dwa poddrzewa: jeden dla aplikacji i drugi dla węzłów.</span><span class="sxs-lookup"><span data-stu-id="05bc0-120">hello cluster contains two subtrees: one for applications and another for nodes.</span></span>

<span data-ttu-id="05bc0-121">Można użyć toonavigate widoku aplikacji hello za pośrednictwem usługi Service Fabric logicznej hierarchii: aplikacji, usług, partycji i replik.</span><span class="sxs-lookup"><span data-stu-id="05bc0-121">You can use hello application view toonavigate through Service Fabric's logical hierarchy: applications, services, partitions, and replicas.</span></span>

<span data-ttu-id="05bc0-122">W poniższym przykładzie hello, hello aplikacji **moja_aplikacja** składa się z dwóch usług **MyStatefulService** i **WebService**.</span><span class="sxs-lookup"><span data-stu-id="05bc0-122">In hello example below, hello application **MyApp** consists of two services, **MyStatefulService** and **WebService**.</span></span> <span data-ttu-id="05bc0-123">Ponieważ **MyStatefulService** jest obiektem stanowym, zawiera partycji z jednego podstawowego i dwóch replik pomocniczych.</span><span class="sxs-lookup"><span data-stu-id="05bc0-123">Since **MyStatefulService** is stateful, it includes a partition with one primary and two secondary replicas.</span></span> <span data-ttu-id="05bc0-124">Z kolei WebSvcService jest bezstanowych i zawiera pojedyncze wystąpienie.</span><span class="sxs-lookup"><span data-stu-id="05bc0-124">By contrast, WebSvcService is stateless and contains a single instance.</span></span>

![Widok aplikacji w narzędziu Service Fabric Explorer][sfx-application-tree]

<span data-ttu-id="05bc0-126">Na każdym poziomie drzewa hello hello głównego w okienku zostaną wyświetlone odpowiednie informacje o elemencie hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-126">At each level of hello tree, hello main pane shows pertinent information about hello item.</span></span> <span data-ttu-id="05bc0-127">Można na przykład zobacz hello stan kondycji i wersji określonej usługi.</span><span class="sxs-lookup"><span data-stu-id="05bc0-127">For example, you can see hello health status and version for a particular service.</span></span>

![Okienko essentials Service Fabric Explorer][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a><span data-ttu-id="05bc0-129">Wyświetlanie węzłów klastra hello</span><span class="sxs-lookup"><span data-stu-id="05bc0-129">View hello cluster's nodes</span></span>
<span data-ttu-id="05bc0-130">Widok węzła Hello przedstawia hello fizycznego układu hello klastra.</span><span class="sxs-lookup"><span data-stu-id="05bc0-130">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="05bc0-131">Dla danego węzła można sprawdzić, które aplikacje mają kod wdrożony w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="05bc0-131">For a given node, you can inspect which applications have code deployed on that node.</span></span> <span data-ttu-id="05bc0-132">W szczególności widać replik, które są aktualnie uruchomione istnieje.</span><span class="sxs-lookup"><span data-stu-id="05bc0-132">More specifically, you can see which replicas are currently running there.</span></span>

## <a name="actions"></a><span data-ttu-id="05bc0-133">Akcje</span><span class="sxs-lookup"><span data-stu-id="05bc0-133">Actions</span></span>
<span data-ttu-id="05bc0-134">Service Fabric Explorer oferuje tooinvoke szybkie akcje na węzłach, aplikacji i usług w ramach klastra.</span><span class="sxs-lookup"><span data-stu-id="05bc0-134">Service Fabric Explorer offers a quick way tooinvoke actions on nodes, applications, and services within your cluster.</span></span>

<span data-ttu-id="05bc0-135">Na przykład toodelete wystąpienie aplikacji wybierz aplikacji hello z hello drzewa po lewej stronie powitania, a następnie wybierz **akcje** > **Usuń aplikację**.</span><span class="sxs-lookup"><span data-stu-id="05bc0-135">For example, toodelete an application instance, choose hello application from hello tree on hello left, and then choose **Actions** > **Delete Application**.</span></span>

![Usunięcie aplikacji w narzędziu Service Fabric Explorer][sfx-delete-application]

> [!TIP]
> <span data-ttu-id="05bc0-137">Można wykonywać hello same akcje, klikając przycisk wielokropka hello następnego elementu tooeach.</span><span class="sxs-lookup"><span data-stu-id="05bc0-137">You can perform hello same actions by clicking hello ellipsis next tooeach element.</span></span>
>
>

<span data-ttu-id="05bc0-138">Witaj Poniższa tabela zawiera listę dostępnych dla każdej jednostki akcji hello:</span><span class="sxs-lookup"><span data-stu-id="05bc0-138">hello following table lists hello actions available for each entity:</span></span>

| <span data-ttu-id="05bc0-139">**Jednostki**</span><span class="sxs-lookup"><span data-stu-id="05bc0-139">**Entity**</span></span> | <span data-ttu-id="05bc0-140">**Akcja**</span><span class="sxs-lookup"><span data-stu-id="05bc0-140">**Action**</span></span> | <span data-ttu-id="05bc0-141">**Opis**</span><span class="sxs-lookup"><span data-stu-id="05bc0-141">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="05bc0-142">Typ aplikacji</span><span class="sxs-lookup"><span data-stu-id="05bc0-142">Application type</span></span> |<span data-ttu-id="05bc0-143">Cofnij aprowizację typu</span><span class="sxs-lookup"><span data-stu-id="05bc0-143">Unprovision type</span></span> |<span data-ttu-id="05bc0-144">Usunięcie pakietu aplikacji hello z magazynu obrazu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-144">Removes hello application package from hello cluster's image store.</span></span> <span data-ttu-id="05bc0-145">Wymaga wszystkie aplikacje tego typu toobe, najpierw usunąć.</span><span class="sxs-lookup"><span data-stu-id="05bc0-145">Requires all applications of that type toobe removed first.</span></span> |
| <span data-ttu-id="05bc0-146">Aplikacja</span><span class="sxs-lookup"><span data-stu-id="05bc0-146">Application</span></span> |<span data-ttu-id="05bc0-147">Usuń aplikację</span><span class="sxs-lookup"><span data-stu-id="05bc0-147">Delete Application</span></span> |<span data-ttu-id="05bc0-148">Usunięcie aplikacji hello, łącznie z jej usług i ich stan (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="05bc0-148">Delete hello application, including all its services and their state (if any).</span></span> |
| <span data-ttu-id="05bc0-149">Usługa</span><span class="sxs-lookup"><span data-stu-id="05bc0-149">Service</span></span> |<span data-ttu-id="05bc0-150">Usuwanie usługi</span><span class="sxs-lookup"><span data-stu-id="05bc0-150">Delete Service</span></span> |<span data-ttu-id="05bc0-151">Usuń usługi hello i jego stan (jeśli istnieje).</span><span class="sxs-lookup"><span data-stu-id="05bc0-151">Delete hello service and its state (if any).</span></span> |
| <span data-ttu-id="05bc0-152">Węzeł</span><span class="sxs-lookup"><span data-stu-id="05bc0-152">Node</span></span> |<span data-ttu-id="05bc0-153">Activate</span><span class="sxs-lookup"><span data-stu-id="05bc0-153">Activate</span></span> |<span data-ttu-id="05bc0-154">Aktywuj hello węzła.</span><span class="sxs-lookup"><span data-stu-id="05bc0-154">Activate hello node.</span></span> |
| <span data-ttu-id="05bc0-155">Węzeł</span><span class="sxs-lookup"><span data-stu-id="05bc0-155">Node</span></span> | <span data-ttu-id="05bc0-156">Dezaktywuj (Wstrzymaj)</span><span class="sxs-lookup"><span data-stu-id="05bc0-156">Deactivate (pause)</span></span> | <span data-ttu-id="05bc0-157">Wstrzymaj węzeł hello w jego bieżącym stanie.</span><span class="sxs-lookup"><span data-stu-id="05bc0-157">Pause hello node in its current state.</span></span> <span data-ttu-id="05bc0-158">Usługi nadal toorun, ale usługi sieć szkieletowa nie aktywnego przenosi niczego na lub wyłącz go, chyba że jest wymagane tooprevent awarii lub niespójność danych.</span><span class="sxs-lookup"><span data-stu-id="05bc0-158">Services continue toorun but Service Fabric does not proactively move anything onto or off it unless it is required tooprevent an outage or data inconsistency.</span></span> <span data-ttu-id="05bc0-159">Ta akcja jest zwykle używana tooenable debugowanie usług na tooensure określonego węzła, który nie należy przenosić podczas kontroli.</span><span class="sxs-lookup"><span data-stu-id="05bc0-159">This action is typically used tooenable debugging services on a specific node tooensure that they do not move during inspection.</span></span> | |
| <span data-ttu-id="05bc0-160">Węzeł</span><span class="sxs-lookup"><span data-stu-id="05bc0-160">Node</span></span> | <span data-ttu-id="05bc0-161">Dezaktywuj (ponowne uruchomienie)</span><span class="sxs-lookup"><span data-stu-id="05bc0-161">Deactivate (restart)</span></span> | <span data-ttu-id="05bc0-162">Bezpieczne przenoszenie wszystkich usług w pamięci wyłącz węzeł i zamknij usług trwałych.</span><span class="sxs-lookup"><span data-stu-id="05bc0-162">Safely move all in-memory services off a node and close persistent services.</span></span> <span data-ttu-id="05bc0-163">Zazwyczaj używany podczas hello procesy hosta lub maszyny toobe konieczność ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="05bc0-163">Typically used when hello host processes or machine need toobe restarted.</span></span> | |
| <span data-ttu-id="05bc0-164">Węzeł</span><span class="sxs-lookup"><span data-stu-id="05bc0-164">Node</span></span> | <span data-ttu-id="05bc0-165">Dezaktywuj (Usuń dane)</span><span class="sxs-lookup"><span data-stu-id="05bc0-165">Deactivate (remove data)</span></span> | <span data-ttu-id="05bc0-166">Bezpiecznie zamknąć wszystkie usługi uruchomione w węźle powitania po utworzeniu wystarczające zapasowe replik.</span><span class="sxs-lookup"><span data-stu-id="05bc0-166">Safely close all services running on hello node after building sufficient spare replicas.</span></span> <span data-ttu-id="05bc0-167">Zazwyczaj używane do węzła (lub co najmniej jej magazynem) jest przełączana trwale poza Komisji.</span><span class="sxs-lookup"><span data-stu-id="05bc0-167">Typically used when a node (or at least its storage) is being permanently taken out of commission.</span></span> | |
| <span data-ttu-id="05bc0-168">Węzeł</span><span class="sxs-lookup"><span data-stu-id="05bc0-168">Node</span></span> | <span data-ttu-id="05bc0-169">Usuń stan węzła</span><span class="sxs-lookup"><span data-stu-id="05bc0-169">Remove node state</span></span> | <span data-ttu-id="05bc0-170">Usuń wiedzy replik węzła z klastra hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-170">Remove knowledge of a node's replicas from hello cluster.</span></span> <span data-ttu-id="05bc0-171">Zazwyczaj używany podczas uznaje nieodwracalny węzeł już nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="05bc0-171">Typically used when an already failed node is deemed unrecoverable.</span></span> | |
| <span data-ttu-id="05bc0-172">Węzeł</span><span class="sxs-lookup"><span data-stu-id="05bc0-172">Node</span></span> | <span data-ttu-id="05bc0-173">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="05bc0-173">Restart</span></span> | <span data-ttu-id="05bc0-174">Symulację awarii węzła poprzez ponowne uruchomienie węzła hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-174">Simulate a node failure by restarting hello node.</span></span> <span data-ttu-id="05bc0-175">Więcej informacji [tutaj](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="05bc0-175">More information [here](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps)</span></span> | |

<span data-ttu-id="05bc0-176">Ponieważ wiele działań destrukcyjnego, może być zadawane tooconfirm Twojego zamiar przed zakończeniem działania hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-176">Since many actions are destructive, you may be asked tooconfirm your intent before hello action is completed.</span></span>

> [!TIP]
> <span data-ttu-id="05bc0-177">Wszystkie akcje, które mogą być wykonywane za pomocą Eksploratora usługi sieć szkieletowa można również przeprowadzić za pomocą programu PowerShell lub interfejsu API REST, tooenable automatyzacji.</span><span class="sxs-lookup"><span data-stu-id="05bc0-177">Every action that can be performed through Service Fabric Explorer can also be performed through PowerShell or a REST API, tooenable automation.</span></span>
>
>

<span data-ttu-id="05bc0-178">Umożliwia także wystąpień aplikacji usługi Service Fabric Explorer toocreate aplikacji danego typu i wersji.</span><span class="sxs-lookup"><span data-stu-id="05bc0-178">You can also use Service Fabric Explorer toocreate application instances for a given application type and version.</span></span> <span data-ttu-id="05bc0-179">Wybierz typ aplikacji hello w widoku drzewa hello, a następnie kliknij przycisk hello **Utwórz wystąpienie aplikacji** łącze następnej wersji toohello chcesz w okienku po prawej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="05bc0-179">Choose hello application type in hello tree view, then click hello **Create app instance** link next toohello version you'd like in hello right pane.</span></span>

![Tworzenie wystąpienia aplikacji w narzędziu Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> <span data-ttu-id="05bc0-181">Obecnie nie mogą być parametryczne wystąpień aplikacji utworzonych za pomocą Eksploratora usługi sieć szkieletowa.</span><span class="sxs-lookup"><span data-stu-id="05bc0-181">Application instances created through Service Fabric Explorer cannot currently be parameterized.</span></span> <span data-ttu-id="05bc0-182">Są one tworzone przy użyciu wartości parametrów domyślnych.</span><span class="sxs-lookup"><span data-stu-id="05bc0-182">They are created using default parameter values.</span></span>
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a><span data-ttu-id="05bc0-183">Połącz tooa zdalnego klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="05bc0-183">Connect tooa remote Service Fabric cluster</span></span>
<span data-ttu-id="05bc0-184">Jeśli znasz punktu końcowego hello klastra i masz wystarczające uprawnienia dostępne Service Fabric Explorer z dowolnej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="05bc0-184">If you know hello cluster's endpoint and have sufficient permissions you can access Service Fabric Explorer from any browser.</span></span> <span data-ttu-id="05bc0-185">Jest to spowodowane Eksploratora usługi sieć szkieletowa jest po prostu innej usługi, która działa w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="05bc0-185">This is because Service Fabric Explorer is just another service that runs in hello cluster.</span></span>

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a><span data-ttu-id="05bc0-186">Odnajdywanie punktu końcowego Service Fabric Explorer hello zdalnego klastra</span><span class="sxs-lookup"><span data-stu-id="05bc0-186">Discover hello Service Fabric Explorer endpoint for a remote cluster</span></span>
<span data-ttu-id="05bc0-187">tooreach Service Fabric Explorer, w przypadku danego klastra punktu przeglądarkę, aby:</span><span class="sxs-lookup"><span data-stu-id="05bc0-187">tooreach Service Fabric Explorer for a given cluster, point your browser to:</span></span>

<span data-ttu-id="05bc0-188">http://&lt;your klastra endpoint&gt;: 19080/Explorer</span><span class="sxs-lookup"><span data-stu-id="05bc0-188">http://&lt;your-cluster-endpoint&gt;:19080/Explorer</span></span>

<span data-ttu-id="05bc0-189">W przypadku klastrów Azure hello pełny adres URL jest również dostępna w okienku essentials klastra hello hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="05bc0-189">For Azure clusters, hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="05bc0-190">Połącz tooa bezpiecznego klastra</span><span class="sxs-lookup"><span data-stu-id="05bc0-190">Connect tooa secure cluster</span></span>
<span data-ttu-id="05bc0-191">Można kontrolować klienta dostępu tooyour klastra sieci szkieletowej usług z certyfikatów lub przy użyciu usługi Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="05bc0-191">You can control client access tooyour Service Fabric cluster either with certificates or using Azure Active Directory (AAD).</span></span>

<span data-ttu-id="05bc0-192">Jeśli tooconnect tooService Eksploratora sieci szkieletowej w klastrze bezpieczny, następnie w zależności od konfiguracji klastra hello można będzie można toopresent wymagany certyfikat klienta lub zaloguj się za pomocą usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="05bc0-192">If you attempt tooconnect tooService Fabric Explorer on a secure cluster, then depending on hello cluster's configuration you'll be required toopresent a client certificate or log in using AAD.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05bc0-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="05bc0-193">Next steps</span></span>
* [<span data-ttu-id="05bc0-194">Omówienie testowania</span><span class="sxs-lookup"><span data-stu-id="05bc0-194">Testability overview</span></span>](service-fabric-testability-overview.md)
* [<span data-ttu-id="05bc0-195">Zarządzanie aplikacji usługi Service Fabric w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="05bc0-195">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="05bc0-196">Wdrażanie aplikacji sieci szkieletowej usług za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="05bc0-196">Service Fabric application deployment using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
