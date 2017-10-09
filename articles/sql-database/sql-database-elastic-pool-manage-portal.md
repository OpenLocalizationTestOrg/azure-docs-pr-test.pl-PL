---
title: "Portalu Azure: tworzenie i zarządzanie puli elastycznej bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello portalu Azure i SQL Database toomanage wbudowane narzędzie analizy, monitor i odpowiedniego rozmiaru bazy danych wydajności toooptimize skalowalnej elastycznej puli i zarządzania nimi kosztów."
keywords: 
services: sql-database
documentationcenter: 
author: ninarn
manager: jhubbard
editor: cgronlun
ms.assetid: 3dc9b7a3-4b10-423a-8e44-9174aca5cf3d
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.date: 06/06/2016
ms.author: ninarn
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: e0de952bc0c91177f64c04363630783d72435741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-hello-azure-portal"></a><span data-ttu-id="680cc-103">Tworzenie i zarządzanie nimi pula elastyczna o hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="680cc-103">Create and manage an elastic pool with hello Azure portal</span></span>
<span data-ttu-id="680cc-104">W tym temacie opisano sposób toocreate i zarządzanie nimi skalowalne [pule elastyczne](sql-database-elastic-pool.md) z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="680cc-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with hello Azure portal.</span></span> <span data-ttu-id="680cc-105">Można również utworzyć i zarządzać nimi Azure pula elastyczna o [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello interfejsu API REST, lub [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="680cc-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="680cc-106">Można również tworzyć i przenoszenie baz danych do i z pul elastycznych, używając [języka Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="680cc-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="680cc-107">Tworzenie puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="680cc-107">Create an elastic pool</span></span> 

<span data-ttu-id="680cc-108">Istnieją dwa sposoby tworzenia puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="680cc-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="680cc-109">Możesz zrobić to od początku, jeśli znasz ustawienia puli hello, lub uruchomić zgodnie z zaleceniami hello usługi.</span><span class="sxs-lookup"><span data-stu-id="680cc-109">You can do it from scratch if you know hello pool setup you want, or start with a recommendation from hello service.</span></span> <span data-ttu-id="680cc-110">SQL Database ma wbudowane narzędzie analizy zalecane ustawienia puli elastycznej, jeśli jest to bardziej ekonomiczne na podstawie hello poza danych telemetrii użycia baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on hello past usage telemetry for your databases.</span></span>

<span data-ttu-id="680cc-111">Można utworzyć wiele pul na serwerze, ale nie można dodać bazy danych z różnych serwerów do hello tej samej puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-111">You can create multiple pools on a server, but you can't add databases from different servers into hello same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="680cc-112">Pule elastyczne są ogólnodostępne we wszystkich regionach platformy Azure oprócz Indii Zachodnich, gdzie są obecnie dostępne w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="680cc-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="680cc-113">Pule elastyczne zostaną udostępnione ogólnie w tych regionach tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="680cc-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="680cc-114">Krok 1: Tworzenie puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="680cc-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="680cc-115">Tworzenie z istniejącej puli elastycznej **serwera** bloku w portalu hello jest hello Najprostszym sposobem toomove istniejących baz danych w puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="680cc-115">Creating an elastic pool from an existing **server** blade in hello portal is hello easiest way toomove existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="680cc-116">Można również utworzyć puli elastycznej, wyszukując **puli elastycznej SQL** w hello **Marketplace** lub klikając **+ Dodaj** w hello **pule elastyczne SQL**Przeglądaj bloku.</span><span class="sxs-lookup"><span data-stu-id="680cc-116">You can also create an elastic pool by searching **SQL elastic pool** in hello **Marketplace** or clicking **+Add** in hello **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="680cc-117">Jesteś toospecify stanie nowego lub istniejącego serwera do obsługi przepływu pracy w tej puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-117">You are able toospecify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="680cc-118">W hello [portalu Azure](http://portal.azure.com/), kliknij przycisk **więcej usług**  **>**  **serwerów SQL**, a następnie kliknij przycisk powitania serwera, który zawiera hello ma tooadd tooan elastycznej puli baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-118">In hello [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click hello server that contains hello databases you want tooadd tooan elastic pool.</span></span>
2. <span data-ttu-id="680cc-119">Kliknij przycisk **Nowa pula**.</span><span class="sxs-lookup"><span data-stu-id="680cc-119">Click **New pool**.</span></span>

    ![Dodaj serwer tooa puli](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="680cc-121">**— Lub —**</span><span class="sxs-lookup"><span data-stu-id="680cc-121">**-OR-**</span></span>

    <span data-ttu-id="680cc-122">Może zostać wyświetlony komunikat z informacją, że są zalecane elastyczne pule powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="680cc-122">You may see a message saying there are recommended elastic pools for hello server.</span></span> <span data-ttu-id="680cc-123">Kliknij hello toosee wiadomość hello zalecane zależności telemetrycznych użycia baz danych historycznych, a następnie kliknąć toosee warstwy hello więcej szczegółów i dostosować hello puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-123">Click hello message toosee hello recommended pools based on historical database usage telemetry, and then click hello tier toosee more details and customize hello pool.</span></span> <span data-ttu-id="680cc-124">Zobacz [omówienie zaleceń puli](#understand-elastic-pool-recommendations) dalszej części tego tematu dla jak hello tworzone są zalecenia.</span><span class="sxs-lookup"><span data-stu-id="680cc-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how hello recommendation is made.</span></span>

    ![zalecana pula](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="680cc-126">Witaj **puli elastycznej** zostanie wyświetlony blok, czyli gdzie Określ ustawienia hello z puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-126">hello **elastic pool** blade appears, which is where you specify hello settings for your pool.</span></span> <span data-ttu-id="680cc-127">Jeśli kliknięto **nowej puli** w poprzednim kroku hello jest hello warstwy cenowej **standardowe** jest wybrany domyślnie i nie baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-127">If you clicked **New pool** in hello previous step, hello pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="680cc-128">Tworzenie puli pustych lub określ zestaw istniejących baz danych z tej toomove serwera na powitania puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-128">You can create an empty pool, or specify a set of existing databases from that server toomove into hello pool.</span></span> <span data-ttu-id="680cc-129">W przypadku tworzenia puli zalecana hello zalecane cenowym ustawienia wydajności i listy baz danych są wstępnie, ale nadal można je zmienić.</span><span class="sxs-lookup"><span data-stu-id="680cc-129">If you are creating a recommended pool, hello recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Konfigurowanie puli elastycznej](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="680cc-131">Określ nazwę puli elastycznej hello, lub pozostaw domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="680cc-131">Specify a name for hello elastic pool, or leave it as hello default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="680cc-132">Krok 2. Wybieranie warstwy cenowej</span><span class="sxs-lookup"><span data-stu-id="680cc-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="680cc-133">Witaj warstwa cenowa puli określa hello funkcji elastics toohello dostępne w puli hello i hello maksymalną liczbę jednostek Edtu (maks. wartość eDTU) i bazy danych dostępności tooeach magazynu (GB).</span><span class="sxs-lookup"><span data-stu-id="680cc-133">hello pool's pricing tier determines hello features available toohello elastics in hello pool, and hello maximum number of eDTUs (eDTU MAX), and storage (GBs) available tooeach database.</span></span> <span data-ttu-id="680cc-134">Aby uzyskać szczegółowe informacje, zobacz Warstwy usługi.</span><span class="sxs-lookup"><span data-stu-id="680cc-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="680cc-135">Kliknij toochange hello warstwę cenową dla puli hello **warstwa cenowa**, kliknij hello cenowym, a następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="680cc-135">toochange hello pricing tier for hello pool, click **Pricing tier**, click hello pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="680cc-136">Po wybraniu hello warstwy cenowej i zatwierdź zmiany, klikając **OK** w ostatnim kroku hello, nie będzie hello stanie toochange cenowym hello puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-136">After you choose hello pricing tier and commit your changes by clicking **OK** in hello last step, you won't be able toochange hello pricing tier of hello pool.</span></span> <span data-ttu-id="680cc-137">toochange hello warstwę cenową istniejącej puli elastycznej, tworzenie elastycznej puli w hello żądanej warstwy cenowej i Migrowanie hello baz danych toothis nową pulę.</span><span class="sxs-lookup"><span data-stu-id="680cc-137">toochange hello pricing tier for an existing elastic pool, create an elastic pool in hello desired pricing tier and migrate hello databases toothis new pool.</span></span>
>

![Wybór warstwy cenowej](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-hello-pool"></a><span data-ttu-id="680cc-139">Krok 3: Konfigurowanie puli hello</span><span class="sxs-lookup"><span data-stu-id="680cc-139">Step 3: Configure hello pool</span></span>

<span data-ttu-id="680cc-140">Po ustawieniu warstwy cenowej hello, kliknij przycisk Konfiguruj pulę, którego można dodać bazy danych, ustawić jednostki Edtu i magazyn (GB puli) oraz ustawić hello min i max jednostek Edtu dla hello elastics hello puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-140">After setting hello pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set hello min and max eDTUs for hello elastics in hello pool.</span></span>

1. <span data-ttu-id="680cc-141">Kliknij przycisk **Konfiguruj pulę**.</span><span class="sxs-lookup"><span data-stu-id="680cc-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="680cc-142">Zaznacz hello bazy danych ma tooadd toohello puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-142">Select hello databases you want tooadd toohello pool.</span></span> <span data-ttu-id="680cc-143">Ten krok jest opcjonalny podczas tworzenia puli hello.</span><span class="sxs-lookup"><span data-stu-id="680cc-143">This step is optional while creating hello pool.</span></span> <span data-ttu-id="680cc-144">Po utworzeniu puli hello można dodać bazy danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-144">Databases can be added after hello pool has been created.</span></span>
    <span data-ttu-id="680cc-145">tooadd baz danych, kliknij przycisk **Dodaj bazę danych**, kliknij przycisk hello baz danych, że mają tooadd, a następnie kliknij przycisk hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="680cc-145">tooadd databases, click **Add database**, click hello databases that you want tooadd, and then click hello **Select** button.</span></span>

    ![Dodawanie baz danych](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="680cc-147">Jeśli hello baz danych, z którymi pracujesz ma za mało danych telemetrii historycznych danych użycia, hello **szacowane eDTU i GB użycia** wykresu i hello **rzeczywiste użycie jednostek eDTU** toohelp aktualizacji wykresu słupkowego wprowadzeniu konfiguracji decyzji.</span><span class="sxs-lookup"><span data-stu-id="680cc-147">If hello databases you're working with have enough historical usage telemetry, hello **Estimated eDTU and GB usage** graph and hello **Actual eDTU usage** bar chart update toohelp you make configuration decisions.</span></span> <span data-ttu-id="680cc-148">Ponadto hello usługi może spowodować toohelp komunikat zalecenie hello możesz odpowiedniego rozmiaru puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-148">Also, hello service may give you a recommendation message toohelp you right-size hello pool.</span></span> <span data-ttu-id="680cc-149">Patrz sekcja [Zalecenia dynamiczne](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="680cc-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="680cc-150">Używanie formantów hello na powitania **Konfigurowanie puli** tooexplore ustawienia strony i skonfigurować pulę.</span><span class="sxs-lookup"><span data-stu-id="680cc-150">Use hello controls on hello **Configure pool** page tooexplore settings and configure your pool.</span></span> <span data-ttu-id="680cc-151">Zobacz [elastyczne pule limity](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) uzyskać więcej szczegółów na temat limitów dla każdej warstwy usług i zobacz [zagadnienia dotyczące cen i wydajności dla pul elastycznych](sql-database-elastic-pool.md) Aby uzyskać szczegółowe wskazówki dotyczące doboru wielkości puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="680cc-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="680cc-152">Aby uzyskać więcej informacji na temat ustawień puli, zobacz [właściwości puli elastycznej](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="680cc-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Konfigurowanie puli elastycznej](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="680cc-154">Kliknij przycisk **wybierz** w hello **Konfigurowanie puli** blok po zmianie ustawień.</span><span class="sxs-lookup"><span data-stu-id="680cc-154">Click **Select** in hello **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="680cc-155">Kliknij przycisk **OK** toocreate hello puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-155">Click **OK** toocreate hello pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="680cc-156">Omówienie zaleceń puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="680cc-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="680cc-157">Hello usługi SQL Database ocenia historyczne dane użycia i zaleca jednej lub kilku pul, gdy jest bardziej ekonomiczne rozwiązanie niż używanie pojedynczych baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-157">hello SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="680cc-158">Każde zalecenie jest konfigurowane z unikatowym podzbiorem powitania serwera baz danych, które najlepiej odpowiadają hello puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-158">Each recommendation is configured with a unique subset of hello server's databases that best fit hello pool.</span></span>

![zalecana pula](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="680cc-160">Witaj zalecenie puli obejmuje:</span><span class="sxs-lookup"><span data-stu-id="680cc-160">hello pool recommendation comprises:</span></span>

- <span data-ttu-id="680cc-161">Warstwę cenową dla puli hello (Basic, Standard, Premium lub Premium RS)</span><span class="sxs-lookup"><span data-stu-id="680cc-161">A pricing tier for hello pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="680cc-162">Odpowiednie **Jednostki eDTU PULI** (określane również jako Maks. wartość eDTU na pulę)</span><span class="sxs-lookup"><span data-stu-id="680cc-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="680cc-163">Witaj **maks. wartość eDTU** i **min. wartość eDTU** na bazę danych</span><span class="sxs-lookup"><span data-stu-id="680cc-163">hello **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="680cc-164">Witaj listę zalecanych baz danych dla puli hello</span><span class="sxs-lookup"><span data-stu-id="680cc-164">hello list of recommended databases for hello pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="680cc-165">Usługa Hello uwzględnia hello ostatnich 30 dni telemetrii podczas rekomendowania pul.</span><span class="sxs-lookup"><span data-stu-id="680cc-165">hello service takes hello last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="680cc-166">Dla toobe bazy danych, traktowane jako kandydatem do puli elastycznej musi istnieć co najmniej 7 dni.</span><span class="sxs-lookup"><span data-stu-id="680cc-166">For a database toobe considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="680cc-167">Bazy, które znajdują się już w puli elastycznej, nie są brane pod uwagę podczas tworzenia zaleceń dla puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="680cc-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="680cc-168">Hello usługa oblicza zapotrzebowanie na zasoby oraz opłacalność przenoszenia hello jednej bazy danych w poszczególnych warstwach usług w pulach hello sam warstwy.</span><span class="sxs-lookup"><span data-stu-id="680cc-168">hello service evaluates resource needs and cost effectiveness of moving hello single databases in each service tier into pools of hello same tier.</span></span> <span data-ttu-id="680cc-169">Na przykład wszystkie bazy danych w warstwie Standardowej na serwerze są oceniane pod względem dopasowania do Standardowej puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="680cc-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="680cc-170">Oznacza to, że usługa hello nie tworzy zalecenia dotyczące warstwy między takich jak przeniesienie standardowe bazy danych do puli Premium.</span><span class="sxs-lookup"><span data-stu-id="680cc-170">This means hello service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="680cc-171">Po dodaniu puli toohello baz danych, zalecenia są generowane dynamicznie na podstawie hello historycznych danych użycia hello baz danych, wybrana przez Ciebie.</span><span class="sxs-lookup"><span data-stu-id="680cc-171">After adding databases toohello pool, recommendations are dynamically generated based on hello historical usage of hello databases you have selected.</span></span> <span data-ttu-id="680cc-172">Te zalecenia są wyświetlane w hello jednostek eDTU i GB wykres użycia i transparent zalecenie u góry hello hello **Konfigurowanie puli** bloku.</span><span class="sxs-lookup"><span data-stu-id="680cc-172">These recommendations are shown in hello eDTU and GB usage chart and in a recommendation banner at hello top of hello **Configure pool** blade.</span></span> <span data-ttu-id="680cc-173">Te zalecenia są zamierzone tooassist można utworzyć puli elastycznej zoptymalizowane pod kątem konkretnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-173">These recommendations are intended tooassist you in creating an elastic pool optimized for your specific databases.</span></span>

![zalecenia dynamiczne](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="680cc-175">Zarządzanie i monitorowanie puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="680cc-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="680cc-176">Można użyć hello toomonitor portalu Azure i zarządzać puli elastycznej i hello hello puli baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-176">You can use hello Azure portal toomonitor and manage an elastic pool and hello databases in hello pool.</span></span> <span data-ttu-id="680cc-177">Z portalu hello można monitorować użycie hello puli elastycznej i baz danych hello w tej puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-177">From hello portal, you can monitor hello utilization of an elastic pool and hello databases within that pool.</span></span> <span data-ttu-id="680cc-178">Można również utworzyć zestaw zmian tooyour puli elastycznej i Prześlij wszystkie zmiany na powitania sam czas.</span><span class="sxs-lookup"><span data-stu-id="680cc-178">You can also make a set of changes tooyour elastic pool and submit all changes at hello same time.</span></span> <span data-ttu-id="680cc-179">Te zmiany obejmują dodawanie lub usuwanie baz danych, zmiana ustawień puli elastycznej lub zmiany ustawień bazy danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="680cc-180">powitania po grafika przedstawia przykład puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="680cc-180">hello following graphic shows an example elastic pool.</span></span> <span data-ttu-id="680cc-181">Widok Hello zawiera:</span><span class="sxs-lookup"><span data-stu-id="680cc-181">hello view includes:</span></span>

*  <span data-ttu-id="680cc-182">Wykresy do monitorowania użycia zasobów, zarówno hello puli elastycznej i hello zawartych baz danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="680cc-182">Charts for monitoring resource usage of both hello elastic pool and hello databases contained in hello pool.</span></span>
*  <span data-ttu-id="680cc-183">Witaj **Konfiguruj** puli toomake przycisku zmienia toohello puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="680cc-183">hello **Configure** pool button toomake changes toohello elastic pool.</span></span>
*  <span data-ttu-id="680cc-184">Witaj **Utwórz bazę danych** przycisku, który tworzy bazę danych i dodaje go toohello bieżącej puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="680cc-184">hello **Create database** button that creates a database and adds it toohello current elastic pool.</span></span>
*  <span data-ttu-id="680cc-185">Zadania elastyczne, które ułatwiają zarządzanie dużej liczby baz danych, uruchamiając skrypty Transact SQL wszystkich baz danych na liście.</span><span class="sxs-lookup"><span data-stu-id="680cc-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Widok puli][2]

<span data-ttu-id="680cc-187">Możesz toosee określonej puli tooa jego wykorzystania zasobów.</span><span class="sxs-lookup"><span data-stu-id="680cc-187">You can go tooa particular pool toosee its resource utilization.</span></span> <span data-ttu-id="680cc-188">Domyślnie pula hello jest użycie magazynu i eDTU tooshow skonfigurowanych hello ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="680cc-188">By default, hello pool is configured tooshow storage and eDTU usage for hello last hour.</span></span> <span data-ttu-id="680cc-189">Wykres Hello może być skonfigurowany tooshow różnych metryk za pośrednictwem różnych czas systemu windows.</span><span class="sxs-lookup"><span data-stu-id="680cc-189">hello chart can be configured tooshow different metrics over various time windows.</span></span>

1. <span data-ttu-id="680cc-190">Wybierz pulę elastyczną toowork z.</span><span class="sxs-lookup"><span data-stu-id="680cc-190">Select an elastic pool toowork with.</span></span>
2. <span data-ttu-id="680cc-191">W obszarze **monitorowania puli elastycznej** jest wykres z etykietą **wykorzystania zasobów**.</span><span class="sxs-lookup"><span data-stu-id="680cc-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="680cc-192">Kliknij przycisk hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="680cc-192">Click hello chart.</span></span>

    ![Monitorowanie puli elastycznej][3]

    <span data-ttu-id="680cc-194">Witaj **Metryka** zostanie otwarty blok, wyświetlanie szczegółowego widoku hello określonej metryki za pośrednictwem hello określone okno czasu.</span><span class="sxs-lookup"><span data-stu-id="680cc-194">hello **Metric** blade opens, showing a detailed view of hello specified metrics over hello specified time window.</span></span>   

    ![Blok metryki][9]

### <a name="toocustomize-hello-chart-display"></a><span data-ttu-id="680cc-196">Wyświetl wykres hello toocustomize</span><span class="sxs-lookup"><span data-stu-id="680cc-196">toocustomize hello chart display</span></span>

<span data-ttu-id="680cc-197">Można edytować hello wykres i toodisplay bloku metryki hello innych metryk, takich jak procent, procent we/wy danych i dziennika we/wy procent wykorzystania procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="680cc-197">You can edit hello chart and hello metric blade toodisplay other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="680cc-198">W bloku metryki hello, kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="680cc-198">On hello metric blade, click **Edit**.</span></span>

    ![Kliknij przycisk Edytuj][6]

2. <span data-ttu-id="680cc-200">W hello **Edytuj wykres** bloku, wybierz zakres czasu (Ostatnia godzina dzisiaj, lub ostatni tydzień), lub kliknij przycisk **niestandardowych** tooselect data zakresu w hello ostatnich dwóch tygodni.</span><span class="sxs-lookup"><span data-stu-id="680cc-200">In hello **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** tooselect any date range in hello last two weeks.</span></span> <span data-ttu-id="680cc-201">Wybierz typ wykresu hello (paska lub linii), a następnie wybierz hello toomonitor zasobów.</span><span class="sxs-lookup"><span data-stu-id="680cc-201">Select hello chart type (bar or line), then select hello resources toomonitor.</span></span>

   > [!Note]
   > <span data-ttu-id="680cc-202">Tylko metryki z tej samej jednostki miary można wyświetlić w hello hello pod adresem hello sam czas.</span><span class="sxs-lookup"><span data-stu-id="680cc-202">Only metrics with hello same unit of measure can be displayed in hello chart at hello same time.</span></span> <span data-ttu-id="680cc-203">Na przykład w przypadku wybrania "procent liczby jednostek eDTU" następnie możesz wybrać tylko innych metryk odsetku hello jednostką miary.</span><span class="sxs-lookup"><span data-stu-id="680cc-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as hello unit of measure.</span></span>
   >

    ![Kliknij przycisk Edytuj](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="680cc-205">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="680cc-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="680cc-206">Zarządzanie i monitorowanie baz danych w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="680cc-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="680cc-207">Można również monitorować pojedyncze bazy danych dla potencjalne problemy.</span><span class="sxs-lookup"><span data-stu-id="680cc-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="680cc-208">W obszarze **elastycznej bazy danych monitorowania**, jest wykres przedstawia metryki pięć baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="680cc-209">Domyślnie program hello wykres Wyświetla hello top 5 baz danych w puli hello przez użycie średnią liczbę jednostek eDTU w hello ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="680cc-209">By default, hello chart displays hello top 5 databases in hello pool by average eDTU usage in hello past hour.</span></span> <span data-ttu-id="680cc-210">Kliknij przycisk hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="680cc-210">Click hello chart.</span></span>

    ![Monitorowanie puli elastycznej][4]

2. <span data-ttu-id="680cc-212">Witaj **wykorzystania zasobów bazy danych** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="680cc-212">hello **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="680cc-213">Zapewnia to szczegółowy widok hello użycia bazy danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="680cc-213">This provides a detailed view of hello database usage in hello pool.</span></span> <span data-ttu-id="680cc-214">Przy użyciu siatki hello w dolnej części bloku hello hello, można wybrać żadnych baz danych w toodisplay puli hello jej użycie w hello wykresu (w górę too5 baz danych).</span><span class="sxs-lookup"><span data-stu-id="680cc-214">Using hello grid in hello lower part of hello blade, you can select any databases in hello pool toodisplay its usage in hello chart (up too5 databases).</span></span> <span data-ttu-id="680cc-215">Można również dostosować hello metryki i przedziału czasowego wyświetlane na wykresie hello klikając **Edytuj wykres**.</span><span class="sxs-lookup"><span data-stu-id="680cc-215">You can also customize hello metrics and time window displayed in hello chart by clicking **Edit chart**.</span></span>

    ![Blok wykorzystanie zasobów bazy danych][8]

### <a name="toocustomize-hello-view"></a><span data-ttu-id="680cc-217">Widok hello toocustomize</span><span class="sxs-lookup"><span data-stu-id="680cc-217">toocustomize hello view</span></span>

1. <span data-ttu-id="680cc-218">W hello **bazy danych wykorzystania zasobów** bloku, kliknij przycisk **Edytuj wykres**.</span><span class="sxs-lookup"><span data-stu-id="680cc-218">In hello **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Kliknij pozycję Edytuj wykres](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="680cc-220">W hello **Edytuj** wykresu bloku, wybierz zakres czasu (Ostatnia godzina lub po 24 godzinach) lub kliknij przycisk **niestandardowych** tooselect różnych dziennie w hello poza toodisplay 2 tygodnie.</span><span class="sxs-lookup"><span data-stu-id="680cc-220">In hello **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** tooselect a different day in hello past 2 weeks toodisplay.</span></span>

    ![Kliknij przycisk niestandardowe](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="680cc-222">Kliknij przycisk hello **porównania baz danych przez** tooselect listy rozwijanej różne metryki toouse podczas porównywania baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-222">Click hello **Compare databases by** dropdown tooselect a different metric toouse when comparing databases.</span></span>

    ![Edytuj wykres hello](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="tooselect-databases-toomonitor"></a><span data-ttu-id="680cc-224">tooselect toomonitor baz danych</span><span class="sxs-lookup"><span data-stu-id="680cc-224">tooselect databases toomonitor</span></span>

<span data-ttu-id="680cc-225">Na liście bazy danych hello w hello **wykorzystania zasobów bazy danych** bloku można znaleźć określonej bazy danych przez wyszukiwanie stronach hello liście hello lub wpisując hello nazwę bazy danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-225">In hello database list in hello **Database Resource Utilization** blade, you can find particular databases by looking through hello pages in hello list or by typing in hello name of a database.</span></span> <span data-ttu-id="680cc-226">Użyj hello wyboru tooselect hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-226">Use hello checkbox tooselect hello database.</span></span>

![Wyszukaj toomonitor baz danych][7]


## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="680cc-228">Dodaj zasób puli elastycznej tooan alertu</span><span class="sxs-lookup"><span data-stu-id="680cc-228">Add an alert tooan elastic pool resource</span></span>

<span data-ttu-id="680cc-229">Można dodać reguły tooan elastycznej puli, która Wyślij wiadomość e-mail punkty końcowe tooURL ciągów toopeople lub alert, kiedy puli elastycznej hello trafienia ustawiony próg użycia.</span><span class="sxs-lookup"><span data-stu-id="680cc-229">You can add rules tooan elastic pool that send email toopeople or alert strings tooURL endpoints when hello elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="680cc-230">**tooadd zasobów tooany alertu:**</span><span class="sxs-lookup"><span data-stu-id="680cc-230">**tooadd an alert tooany resource:**</span></span>

1. <span data-ttu-id="680cc-231">Kliknij hello **wykorzystania zasobów** hello tooopen wykresu **Metryka** bloku, kliknij przycisk **Dodaj alert**, a następnie wprowadź informacje hello w hello **Dodawanie alertu Reguła** bloku (**zasobów** są automatycznie konfigurowane pracy z puli hello toobe).</span><span class="sxs-lookup"><span data-stu-id="680cc-231">Click hello **Resource utilization** chart tooopen hello **Metric** blade, click **Add alert**, and then fill out hello information in hello **Add an alert rule** blade (**Resource** is automatically set up toobe hello pool you're working with).</span></span>
2. <span data-ttu-id="680cc-232">Wpisz **nazwa** i **opis** , które identyfikują hello tooyou alertów oraz odbiorców hello.</span><span class="sxs-lookup"><span data-stu-id="680cc-232">Type a **Name** and **Description** that identifies hello alert tooyou and hello recipients.</span></span>
3. <span data-ttu-id="680cc-233">Wybierz **Metryka** , które mają tooalert z listy hello.</span><span class="sxs-lookup"><span data-stu-id="680cc-233">Choose a **Metric** that you want tooalert from hello list.</span></span>

    <span data-ttu-id="680cc-234">Wykres Hello dynamicznie pokazuje wykorzystania zasobów dla tego toohelp metryki, wybierz próg.</span><span class="sxs-lookup"><span data-stu-id="680cc-234">hello chart dynamically shows resource utilization for that metric toohelp you choose a threshold.</span></span>

4. <span data-ttu-id="680cc-235">Wybierz **warunku** (większe niż poniżej, itd.) i **próg**.</span><span class="sxs-lookup"><span data-stu-id="680cc-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="680cc-236">Wybierz **okres** hello metryki czasu reguły muszą zostać spełnione przed hello wyzwalaczy alertu.</span><span class="sxs-lookup"><span data-stu-id="680cc-236">Choose a **Period** of time that hello metric rule must be satisfied before hello alert triggers.</span></span>
6. <span data-ttu-id="680cc-237">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="680cc-237">Click **OK**.</span></span>

<span data-ttu-id="680cc-238">Aby uzyskać więcej informacji, zobacz [tworzyć alerty bazy danych SQL w portalu Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="680cc-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="680cc-239">Przenoszenie bazy danych w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="680cc-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="680cc-240">Można dodać lub usunąć bazy danych z istniejącej puli.</span><span class="sxs-lookup"><span data-stu-id="680cc-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="680cc-241">Witaj baz danych może być w innych pulach.</span><span class="sxs-lookup"><span data-stu-id="680cc-241">hello databases can be in other pools.</span></span> <span data-ttu-id="680cc-242">Jednak można dodawać tylko baz danych, które są na hello sam serwer logiczny.</span><span class="sxs-lookup"><span data-stu-id="680cc-242">However, you can only add databases that are on hello same logical server.</span></span>

1. <span data-ttu-id="680cc-243">W bloku hello hello puli w obszarze **elastycznych baz danych** kliknij **Konfigurowanie puli**.</span><span class="sxs-lookup"><span data-stu-id="680cc-243">In hello blade for hello pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Kliknij przycisk Konfiguruj pulę][1]

2. <span data-ttu-id="680cc-245">W hello **Konfigurowanie puli** bloku, kliknij przycisk **dodać toopool**.</span><span class="sxs-lookup"><span data-stu-id="680cc-245">In hello **Configure pool** blade, click **Add toopool**.</span></span>

    ![Kliknij przycisk Dodaj toopool](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="680cc-247">W hello **dodać bazy danych** bloku, wybierz hello bazy danych lub puli toohello tooadd baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-247">In hello **Add databases** blade, select hello database or databases tooadd toohello pool.</span></span> <span data-ttu-id="680cc-248">Następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="680cc-248">Then click **Select**.</span></span>

    ![Wybierz tooadd baz danych](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="680cc-250">Witaj **Konfigurowanie puli** bloku teraz list hello wybranej toobe dodane o jej stanie ustawić także bazy danych**oczekujące**.</span><span class="sxs-lookup"><span data-stu-id="680cc-250">hello **Configure pool** blade now lists hello database you selected toobe added, with its status set too**Pending**.</span></span>

    ![Dodawanie puli oczekujące](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="680cc-252">W hello **bloku Konfigurowanie puli**, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="680cc-252">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="680cc-254">Przenoszenie bazy danych z puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="680cc-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="680cc-255">W hello **Konfigurowanie puli** bloku, wybierz hello bazy danych lub tooremove baz danych.</span><span class="sxs-lookup"><span data-stu-id="680cc-255">In hello **Configure pool** blade, select hello database or databases tooremove.</span></span>

    ![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="680cc-257">Kliknij przycisk **usunąć z puli**.</span><span class="sxs-lookup"><span data-stu-id="680cc-257">Click **Remove from pool**.</span></span>

    ![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="680cc-259">Hello **Konfigurowanie puli** bloku teraz list hello bazy danych wybrane toobe usuwane z jego stan zbyt**oczekujące**.</span><span class="sxs-lookup"><span data-stu-id="680cc-259">hello **Configure pool** blade now lists hello database you selected toobe removed with its status set too**Pending**.</span></span>

    ![Podgląd bazy danych Dodawanie i usuwanie](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="680cc-261">W hello **bloku Konfigurowanie puli**, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="680cc-261">In hello **Configure pool blade**, click **Save**.</span></span>

    ![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="680cc-263">Zmień ustawienia wydajności puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="680cc-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="680cc-264">Podczas monitorowania wykorzystania zasobów hello elastycznej puli może stwierdzić, że pewnych zmian są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="680cc-264">As you monitor hello resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="680cc-265">Może być pula hello wymaga zmiany hello limity wydajność lub pamięć masową.</span><span class="sxs-lookup"><span data-stu-id="680cc-265">Maybe hello pool needs a change in hello performance or storage limits.</span></span> <span data-ttu-id="680cc-266">Prawdopodobnie ma toochange hello ustawienia do bazy danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="680cc-266">Possibly you want toochange hello database settings in hello pool.</span></span> <span data-ttu-id="680cc-267">Można zmienić ustawienia hello puli hello w dowolnym czasie tooget hello równowagę wydajności i kosztów.</span><span class="sxs-lookup"><span data-stu-id="680cc-267">You can change hello setup of hello pool at any time tooget hello best balance of performance and cost.</span></span> <span data-ttu-id="680cc-268">Zobacz [kiedy należy puli elastycznej użyć?](sql-database-elastic-pool.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="680cc-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="680cc-269">toochange hello jednostek Edtu i Magazyn limity dla każdej puli i jednostek Edtu na bazę danych:</span><span class="sxs-lookup"><span data-stu-id="680cc-269">toochange hello eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="680cc-270">Otwórz hello **Konfigurowanie puli** bloku.</span><span class="sxs-lookup"><span data-stu-id="680cc-270">Open hello **Configure pool** blade.</span></span>

    <span data-ttu-id="680cc-271">W obszarze **ustawienia puli elastycznej**, użyj albo ustawienia puli hello toochange suwaka.</span><span class="sxs-lookup"><span data-stu-id="680cc-271">Under **elastic pool settings**, use either slider toochange hello pool settings.</span></span>

    ![Użycie zasobów w puli elastycznej](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="680cc-273">Po zmianie ustawienia hello wyświetlania hello pokazuje hello szacowany miesięczny koszt hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="680cc-273">When hello setting changes, hello display shows hello estimated monthly cost of hello change.</span></span>

    ![Aktualizacja puli elastycznej i nowych miesięczny koszt](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="680cc-275">Czas oczekiwania operacji puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="680cc-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="680cc-276">Zmiana hello minimalna liczba jednostek Edtu na bazę danych lub maksymalna liczba jednostek Edtu na bazę danych zazwyczaj kończy się w ciągu 5 minut lub mniej.</span><span class="sxs-lookup"><span data-stu-id="680cc-276">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="680cc-277">Zmiana hello Edtu na pulę, zależy od hello łączną ilość miejsca używanego przez wszystkie bazy danych w puli hello.</span><span class="sxs-lookup"><span data-stu-id="680cc-277">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="680cc-278">Wprowadzanie zmian trwa średnio 90 minut na każde 100 GB.</span><span class="sxs-lookup"><span data-stu-id="680cc-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="680cc-279">Na przykład jeśli całkowita ilość miejsca hello jest używany przez wszystkie bazy danych w puli hello jest 200 GB, a następnie hello oczekuje się, że czas oczekiwania na zmianę hello puli eDTU na pulę wynosi 3 godziny lub mniej.</span><span class="sxs-lookup"><span data-stu-id="680cc-279">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="680cc-280">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="680cc-280">Next steps</span></span>

- <span data-ttu-id="680cc-281">toounderstand jakie puli elastycznej zobacz [puli elastycznej bazy danych SQL](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="680cc-281">toounderstand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="680cc-282">Aby uzyskać wskazówki dotyczące wykorzystujących pule elastyczne, zobacz [zagadnienia dotyczące cen i wydajności dla pul elastycznych](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="680cc-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="680cc-283">toouse zadania elastyczne toorun języka Transact-SQL skryptów na dowolnej liczbie baz danych w puli hello, zobacz [omówienie zadania elastyczne](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="680cc-283">toouse elastic jobs toorun Transact-SQL scripts against any number of databases in hello pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="680cc-284">Zobacz tooquery na dowolnej liczbie baz danych w puli hello [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="680cc-284">tooquery across any number of databases in hello pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="680cc-285">Dla transakcji Zobacz dowolnej liczbie baz danych w puli hello [transakcji elastycznej](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="680cc-285">For transactions any number of databases in hello pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


<!--Image references-->
[1]: ./media/sql-database-elastic-pool-manage-portal/configure-pool.png
[2]: ./media/sql-database-elastic-pool-manage-portal/basic.png
[3]: ./media/sql-database-elastic-pool-manage-portal/basic-2.png
[4]: ./media/sql-database-elastic-pool-manage-portal/basic-3.png
[5]: ./media/sql-database-elastic-pool-manage-portal/elastic-jobs.png
[6]: ./media/sql-database-elastic-pool-manage-portal/edit-metric.png
[7]: ./media/sql-database-elastic-pool-manage-portal/select-dbs.png
[8]: ./media/sql-database-elastic-pool-manage-portal/db-utilization.png
[9]: ./media/sql-database-elastic-pool-manage-portal/metric.png
