---
title: "Usługa Azure Search w portalu hello aaaCreate | Dokumentacja firmy Microsoft"
description: "Udostępnić usługi Azure Search w portalu hello."
services: search
manager: jhubbard
author: HeidiSteen
documentationcenter: 
ms.assetid: c8c88922-69aa-4099-b817-60f7b54e62df
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: f1c7197a1467e32bd4b360b165c9059e6bb0e496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-service-in-hello-portal"></a><span data-ttu-id="e8ba2-103">Tworzenie usługi Azure Search w portalu hello</span><span class="sxs-lookup"><span data-stu-id="e8ba2-103">Create an Azure Search service in hello portal</span></span>

<span data-ttu-id="e8ba2-104">W tym artykule opisano, jak toocreate lub świadczenia usługi Azure Search w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-104">This article explains how toocreate or provision an Azure Search service in hello portal.</span></span> <span data-ttu-id="e8ba2-105">Aby uzyskać instrukcje programu PowerShell, zobacz [zarządzania usługi Azure Search przy użyciu programu PowerShell](search-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-105">For PowerShell instructions, see [Manage Azure Search with PowerShell](search-manage-powershell.md).</span></span>

## <a name="subscribe-free-or-paid"></a><span data-ttu-id="e8ba2-106">Subskrypcja (wolne lub płatną)</span><span class="sxs-lookup"><span data-stu-id="e8ba2-106">Subscribe (free or paid)</span></span>

<span data-ttu-id="e8ba2-107">[Załóż bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) i użyj tootry bezpłatnych środków limit płatnej usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-107">[Open a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) and use free credits tootry out paid Azure services.</span></span> <span data-ttu-id="e8ba2-108">Po wyczerpaniu kredytu, Zachowaj konto hello i kontynuować toouse wolnego usług platformy Azure, takich jak witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-108">After credits are used up, keep hello account and continue toouse free Azure services, such as Websites.</span></span> <span data-ttu-id="e8ba2-109">Karta kredytowa nigdy nie jest obciążona, chyba że jawnie zmienić ustawienia i poproś toobe obciążona.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-109">Your credit card is never charged unless you explicitly change your settings and ask toobe charged.</span></span>

<span data-ttu-id="e8ba2-110">Alternatywnie [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-110">Alternatively, [activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span> <span data-ttu-id="e8ba2-111">Subskrypcję MSDN otrzymasz kredyt, co miesiąc, w której można skorzystać w celu płatnych usług Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-111">An MSDN subscription gives you credits every month you can use for paid Azure services.</span></span> 

## <a name="find-azure-search"></a><span data-ttu-id="e8ba2-112">Znajdź wyszukiwanie Azure</span><span class="sxs-lookup"><span data-stu-id="e8ba2-112">Find Azure Search</span></span>
1. <span data-ttu-id="e8ba2-113">Zaloguj się toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-113">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e8ba2-114">Kliknij znak ("+") plus hello hello górnym lewym rogu.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-114">Click hello plus sign ("+") in hello top left corner.</span></span>
3. <span data-ttu-id="e8ba2-115">Wybierz **sieci Web i mobilność** > **wyszukiwanie Azure**.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-115">Select **Web + Mobile** > **Azure Search**.</span></span>

![](./media/search-create-service-portal/find-search2.png)

## <a name="name-hello-service-and-url-endpoint"></a><span data-ttu-id="e8ba2-116">Usługa hello nazwa i adres URL punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="e8ba2-116">Name hello service and URL endpoint</span></span>

<span data-ttu-id="e8ba2-117">Nazwa usługi jest częścią hello końcowy adres URL, względem którego są wydawane wywołań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-117">A service name is part of hello URL endpoint against which API calls are issued.</span></span> <span data-ttu-id="e8ba2-118">Wpisz nazwę usługi w hello **adres URL** pola.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-118">Type your service name in hello **URL** field.</span></span> 

<span data-ttu-id="e8ba2-119">Wymagania dotyczące nazw usługi:</span><span class="sxs-lookup"><span data-stu-id="e8ba2-119">Service name requirements:</span></span>
   * <span data-ttu-id="e8ba2-120">2 do 60 znaków</span><span class="sxs-lookup"><span data-stu-id="e8ba2-120">2 and 60 characters in length</span></span>
   * <span data-ttu-id="e8ba2-121">małe litery, cyfry i łączniki ("-")</span><span class="sxs-lookup"><span data-stu-id="e8ba2-121">lowercase letters, digits, or dashes ("-")</span></span>
   * <span data-ttu-id="e8ba2-122">nie dash ("-") jako hello najpierw 2 znaki lub ostatni pojedynczy znak</span><span class="sxs-lookup"><span data-stu-id="e8ba2-122">no dash ("-") as hello first 2 characters or last single character</span></span>
   * <span data-ttu-id="e8ba2-123">nie następujących po sobie kresek ("--")</span><span class="sxs-lookup"><span data-stu-id="e8ba2-123">no consecutive dashes ("--")</span></span>

## <a name="select-a-subscription"></a><span data-ttu-id="e8ba2-124">Wybierz subskrypcję</span><span class="sxs-lookup"><span data-stu-id="e8ba2-124">Select a subscription</span></span>
<span data-ttu-id="e8ba2-125">Jeśli masz więcej niż jedną subskrypcję, wybierz jedną z usług magazynu danych lub pliku.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-125">If you have more than one subscription, choose one that also has data or file storage services.</span></span> <span data-ttu-id="e8ba2-126">Usługa wyszukiwanie Azure można Autowykrywanie magazynu tabel Azure i obiektów Blob, bazy danych SQL i bazy danych Azure rozwiązania Cosmos indeksowania za pośrednictwem *indeksatory*, ale tylko w przypadku usług w hello tej samej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-126">Azure Search can auto-detect Azure Table and Blob storage, SQL Database, and Azure Cosmos DB for indexing via *indexers*, but only for services in hello same subscription.</span></span>

## <a name="select-a-resource-group"></a><span data-ttu-id="e8ba2-127">Wybierz grupę zasobów</span><span class="sxs-lookup"><span data-stu-id="e8ba2-127">Select a resource group</span></span>
<span data-ttu-id="e8ba2-128">Grupa zasobów to zbiór usług platformy Azure i zasoby używane razem.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-128">A resource group is a collection of Azure services and resources used together.</span></span> <span data-ttu-id="e8ba2-129">Na przykład, jeśli używasz usługi Azure Search tooindex bazy danych SQL, obie te usługi powinny być częścią hello tej samej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-129">For example, if you are using Azure Search tooindex a SQL database, then both services should be part of hello same resource group.</span></span>

> [!TIP]
> <span data-ttu-id="e8ba2-130">Usunięcie grupy zasobów powoduje usunięcie usług hello w niej.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-130">Deleting a resource group also deletes hello services within it.</span></span> <span data-ttu-id="e8ba2-131">Prototyp projektów przy użyciu wielu usług, wprowadzenie wszystkich z nich hello tej samej grupie zasobów ułatwia oczyszczania po zakończeniu hello projektu.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-131">For prototype projects utilizing multiple services, putting all of them in hello same resource group makes cleanup easier after hello project is over.</span></span> 

## <a name="select-a-hosting-location"></a><span data-ttu-id="e8ba2-132">Wybierz lokalizację hostingu</span><span class="sxs-lookup"><span data-stu-id="e8ba2-132">Select a hosting location</span></span> 
<span data-ttu-id="e8ba2-133">Jak usługa Azure usługi Azure Search może być hostowana w centrach danych wokół hello world.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-133">As an Azure service, Azure Search can be hosted in datacenters around hello world.</span></span> <span data-ttu-id="e8ba2-134">Należy pamiętać, że [ceny może się różnić](https://azure.microsoft.com/pricing/details/search/) według ich położenia.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-134">Note that [prices can differ](https://azure.microsoft.com/pricing/details/search/) by geography.</span></span>

## <a name="select-a-pricing-tier-sku"></a><span data-ttu-id="e8ba2-135">Wybierz warstwę cenową (SKU)</span><span class="sxs-lookup"><span data-stu-id="e8ba2-135">Select a pricing tier (SKU)</span></span>
<span data-ttu-id="e8ba2-136">[Usługa Azure Search jest dostępne w wielu warstw cenowych](https://azure.microsoft.com/pricing/details/search/): wolnego, podstawowa lub standardowa.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-136">[Azure Search is currently offered in multiple pricing tiers](https://azure.microsoft.com/pricing/details/search/): Free, Basic, or Standard.</span></span> <span data-ttu-id="e8ba2-137">Każda warstwa ma własną [pojemności i limity](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-137">Each tier has its own [capacity and limits](search-limits-quotas-capacity.md).</span></span> <span data-ttu-id="e8ba2-138">Zobacz [wybierz warstwę cenową lub jednostki SKU](search-sku-tier.md) orientacji.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-138">See [Choose a pricing tier or SKU](search-sku-tier.md) for guidance.</span></span>

<span data-ttu-id="e8ba2-139">W tym przewodniku Wybraliśmy warstwy standardowa hello naszej usługi.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-139">In this walkthrough, we have chosen hello Standard tier for our service.</span></span>

## <a name="create-your-service"></a><span data-ttu-id="e8ba2-140">Tworzenie usługi</span><span class="sxs-lookup"><span data-stu-id="e8ba2-140">Create your service</span></span>

<span data-ttu-id="e8ba2-141">Należy pamiętać, toopin pulpitu nawigacyjnego toohello usługi łatwy dostęp przy każdym logowaniu.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-141">Remember toopin your service toohello dashboard for easy access whenever you sign in.</span></span>

![](./media/search-create-service-portal/new-service2.png)

## <a name="scale-your-service"></a><span data-ttu-id="e8ba2-142">Skalowanie usługi</span><span class="sxs-lookup"><span data-stu-id="e8ba2-142">Scale your service</span></span>
<span data-ttu-id="e8ba2-143">Może upłynąć kilka minut toocreate usługi (15 minut lub dłużej w zależności od warstwy hello).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-143">It can take a few minutes toocreate a service (15 minutes or more depending on hello tier).</span></span> <span data-ttu-id="e8ba2-144">Po zainicjowaniu obsługi usługi, to można go skalować toomeet potrzeb.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-144">After your service is provisioned, you can scale it toomeet your needs.</span></span> <span data-ttu-id="e8ba2-145">Ponieważ wybrano warstwy standardowa powitania dla usługi Azure Search w dwóch wymiarów można skalować usługi: repliki i partycji.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-145">Because you chose hello Standard tier for your Azure Search service, you can scale your service in two dimensions: replicas and partitions.</span></span> <span data-ttu-id="e8ba2-146">Czy wybierze hello warstwy Basic, można dodać tylko repliki.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-146">Had you chosen hello Basic tier, you can only add replicas.</span></span> <span data-ttu-id="e8ba2-147">Jeśli elastycznie bezpłatnej usługi hello, skalowanie jest niedostępne.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-147">If you provisioned hello free service, scale is not available.</span></span>

<span data-ttu-id="e8ba2-148">***Partycje*** Zezwalaj toostore usługi, a wyszukiwanie za pomocą więcej dokumentów.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-148">***Partitions*** allow your service toostore and search through more documents.</span></span>

<span data-ttu-id="e8ba2-149">***Repliki*** Zezwalaj toohandle Twojego usługi większych obciążeń zapytań wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-149">***Replicas*** allow your service toohandle a higher load of search queries.</span></span>

> [!Important]
> <span data-ttu-id="e8ba2-150">Usługa musi mieć [2 replik do umowy SLA tylko do odczytu i 3 repliki do odczytu/zapisu SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-150">A service must have [2 replicas for read-only SLA and 3 replicas for read/write SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

1. <span data-ttu-id="e8ba2-151">Przejdź tooyour bloku usługi wyszukiwania w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-151">Go tooyour search service blade in hello Azure portal.</span></span>
2. <span data-ttu-id="e8ba2-152">Wybierz w okienku nawigacji po lewej hello **ustawienia** > **skali**.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-152">In hello left-navigation pane, select **Settings** > **Scale**.</span></span>
3. <span data-ttu-id="e8ba2-153">Użyj hello slidebar tooadd repliki lub partycji.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-153">Use hello slidebar tooadd Replicas or Partitions.</span></span>

![](./media/search-create-service-portal/settings-scale.png)

> [!Note] 
> <span data-ttu-id="e8ba2-154">Każda warstwa ma inną [limity](search-limits-quotas-capacity.md) hello całkowitej liczby jednostek wyszukiwania dozwolonych w jednej usługi (replik * partycje = Suma jednostek wyszukiwania).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-154">Each tier has different [limits](search-limits-quotas-capacity.md) on hello total number of Search Units allowed in a single service (Replicas * Partitions = Total Search Units).</span></span>

## <a name="when-tooadd-a-second-service"></a><span data-ttu-id="e8ba2-155">Gdy tooadd drugi usługi</span><span class="sxs-lookup"><span data-stu-id="e8ba2-155">When tooadd a second service</span></span>

<span data-ttu-id="e8ba2-156">Duże większość klientów używać tylko jednej usługi zainicjowana dla warstwy, która zapewnia hello [prawym przyciskiem myszy salda środków](search-sku-tier.md).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-156">A large majority of customers use just one service provisioned at a tier that provides hello [right balance of resources](search-sku-tier.md).</span></span> <span data-ttu-id="e8ba2-157">Jedna usługa może obsługiwać wiele indeksów, toohello podmiotu [maksymalnych wybrania warstwy hello](search-capacity-planning.md), każdy indeks odizolowane od siebie.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-157">One service can host multiple indexes, subject toohello [maximum limits of hello tier you select](search-capacity-planning.md), with each index isolated from another.</span></span> <span data-ttu-id="e8ba2-158">W usłudze Azure Search żądań może jedynie być indeksem ukierunkowanej tooone, minimalizując szansy hello pobierania przypadkowym lub zamierzone danych z innych indeksy w hello sama usługa.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-158">In Azure Search, requests can only be directed tooone index, minimizing hello chance of accidental or intentional data retrieval from other indexes in hello same service.</span></span>

<span data-ttu-id="e8ba2-159">Mimo że większość klientów używają tylko jedną usługę, nadmiarowości usługi może być konieczne, jeśli wymagań operacyjnych Uwzględnij hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e8ba2-159">Although most customers use just one service, service redundancy might be necessary if operational requirements include hello following:</span></span>

+ <span data-ttu-id="e8ba2-160">Odzyskiwanie po awarii (awarii centrum danych).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-160">Disaster recovery (data center outage).</span></span> <span data-ttu-id="e8ba2-161">Usługa Azure Search nie zapewnia błyskawiczne trybu failover w przypadku hello awarii.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-161">Azure Search does not provide instant failover in hello event of an outage.</span></span> <span data-ttu-id="e8ba2-162">Aby uzyskać wskazówki i zalecenia, zobacz [usługi administracyjnej](search-manage.md).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-162">For recommendations and guidance, see [Service administration](search-manage.md).</span></span>
+ <span data-ttu-id="e8ba2-163">Badaniu modelowania wielodostępność stwierdził, że dodatkowe usługi jest hello optymalne projektu.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-163">Your investigation of multi-tenancy modeling has determined that additional services is hello optimal design.</span></span> <span data-ttu-id="e8ba2-164">Aby uzyskać więcej informacji, zobacz [projektu dla wielu dzierżawców](search-modeling-multitenant-saas-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-164">For more information, see [Design for multi-tenancy](search-modeling-multitenant-saas-applications.md).</span></span>
+ <span data-ttu-id="e8ba2-165">Globalny wdrożonej aplikacji może wymagać wystąpienia usługi Azure Search wiele regionów opóźnienia toominimize aplikacji międzynarodowych ruchu.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-165">For globally deployed applications, you might require an instance of Azure Search in multiple regions toominimize latency of your application’s international traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="e8ba2-166">W usłudze Azure Search nie może też oddzielić obciążeń indeksowania i wykonywanie zapytania; w związku z tym nigdy nie spowodowałoby utworzenie wielu usług dla obciążeń rozdzielone.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-166">In Azure Search, you cannot segregate indexing and querying workloads; thus, you would never create multiple services for segregated workloads.</span></span> <span data-ttu-id="e8ba2-167">Indeks jest zawsze wykonać zapytania w usłudze hello w którym został utworzony (nie można utworzyć indeksu w jedną usługę i skopiuj go tooanother).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-167">An index is always queried on hello service in which it was created (you cannot create an index in one service and copy it tooanother).</span></span>
>

<span data-ttu-id="e8ba2-168">Drugi usługi nie jest wymagane w celu zapewnienia wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-168">A second service is not required for high availability.</span></span> <span data-ttu-id="e8ba2-169">Wysoka dostępność dla zapytania jest osiągana, gdy używasz 2 lub więcej replik w hello tę samą usługę.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-169">High availability for queries is achieved when you use 2 or more replicas in hello same service.</span></span> <span data-ttu-id="e8ba2-170">Repliki są aktualizacje sekwencyjnych, co oznacza, że co najmniej jeden działa podczas aktualizacji usługi jest wdrażana. Aby uzyskać więcej informacji o dostępności, zobacz [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span><span class="sxs-lookup"><span data-stu-id="e8ba2-170">Replica updates are sequential, which means at least one is operational when a service update is rolled out. For more information about uptime, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8ba2-171">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8ba2-171">Next steps</span></span>
<span data-ttu-id="e8ba2-172">Po zainicjowaniu obsługi administracyjnej usługi Azure Search, wszystko jest gotowe za[zdefiniuj indeks](search-what-is-an-index.md) , można przekazać i wyszukiwać dane.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-172">After provisioning an Azure Search service, you are ready too[define an index](search-what-is-an-index.md) so you can upload and search your data.</span></span>

<span data-ttu-id="e8ba2-173">Usługa hello tooaccess z kodu lub skryptu, podaj adres URL hello (*nazwa usługi*. search.windows.net) i klucz.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-173">tooaccess hello service from code or script, provide hello URL (*service-name*.search.windows.net) and a key.</span></span> <span data-ttu-id="e8ba2-174">Klucze administratora przyznają dostęp; klucze zapytań przyznać dostęp tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-174">Admin keys grant full access; query keys grant read-only access.</span></span> <span data-ttu-id="e8ba2-175">Zobacz [jak toouse wyszukiwanie Azure .NET](search-howto-dotnet-sdk.md) tooget uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-175">See [How toouse Azure Search in .NET](search-howto-dotnet-sdk.md) tooget started.</span></span>

<span data-ttu-id="e8ba2-176">Zobacz [kompilacji i tworzenie zapytań względem indeksu pierwszego](search-get-started-portal.md) zawiera krótki samouczek oparte na portalu.</span><span class="sxs-lookup"><span data-stu-id="e8ba2-176">See [Build and query your first index](search-get-started-portal.md) for a quick portal-based tutorial.</span></span>

