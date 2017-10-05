---
title: "Portalu Azure: tworzenie i zarządzanie puli elastycznej bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać portalu Azure i SQL Database wbudowane narzędzie analizy do zarządzania, monitorowania i skalowalnej elastycznej puli w celu zoptymalizowania wydajności bazy danych i zarządzanie nimi kosztów odpowiedniego rozmiaru."
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
ms.openlocfilehash: 4ffd1db31f42967dc7f07aa979898dddbb333641
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-an-elastic-pool-with-the-azure-portal"></a><span data-ttu-id="e0a4b-103">Tworzenie i zarządzanie nimi puli elastycznej z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e0a4b-103">Create and manage an elastic pool with the Azure portal</span></span>
<span data-ttu-id="e0a4b-104">W tym temacie przedstawiono sposób tworzenia i zarządzania nimi skalowalne [pule elastyczne](sql-database-elastic-pool.md) z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-104">This topic shows you how to create and manage scalable [elastic pools](sql-database-elastic-pool.md) with the Azure portal.</span></span> <span data-ttu-id="e0a4b-105">Można również utworzyć i zarządzać nimi Azure pula elastyczna o [PowerShell](sql-database-elastic-pool-manage-powershell.md), interfejsu API REST lub [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-105">You can also create and manage an Azure elastic pool with [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="e0a4b-106">Można również tworzyć i przenoszenie baz danych do i z pul elastycznych, używając [języka Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

## <a name="create-an-elastic-pool"></a><span data-ttu-id="e0a4b-107">Tworzenie puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-107">Create an elastic pool</span></span> 

<span data-ttu-id="e0a4b-108">Istnieją dwa sposoby tworzenia puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-108">There are two ways you can create an elastic pool.</span></span> <span data-ttu-id="e0a4b-109">Można utworzyć ją od podstaw, znając wymagane ustawienia puli, lub uruchomić zgodnie z zaleceniami usługi.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-109">You can do it from scratch if you know the pool setup you want, or start with a recommendation from the service.</span></span> <span data-ttu-id="e0a4b-110">SQL Database ma wbudowane narzędzie analizy zalecane ustawienia puli elastycznej, jeśli jest to bardziej ekonomiczne na podstawie ostatnich danych telemetrii użycia baz danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-110">SQL Database has built-in intelligence that recommends an elastic pool setup if it's more cost-efficient for you based on the past usage telemetry for your databases.</span></span>

<span data-ttu-id="e0a4b-111">Można utworzyć wiele pul na serwerze, ale nie można dodać bazy danych z różnych serwerów do tej samej puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-111">You can create multiple pools on a server, but you can't add databases from different servers into the same pool.</span></span> 

> [!NOTE]
> <span data-ttu-id="e0a4b-112">Pule elastyczne są ogólnodostępne we wszystkich regionach platformy Azure oprócz Indii Zachodnich, gdzie są obecnie dostępne w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-112">Elastic pools are generally available (GA) in all Azure regions except West India where it is currently in preview.</span></span>  <span data-ttu-id="e0a4b-113">Pule elastyczne zostaną udostępnione ogólnie w tych regionach tak szybko, jak to możliwe.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-113">GA of elastic pools in this region will occur as soon as possible.</span></span>
>

### <a name="step-1-create-an-elastic-pool"></a><span data-ttu-id="e0a4b-114">Krok 1: Tworzenie puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-114">Step 1: Create an elastic pool</span></span>

<span data-ttu-id="e0a4b-115">Tworzenie z istniejącej puli elastycznej **serwera** bloku w portalu jest najprostszym sposobem, aby przenieść istniejące bazy danych w puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-115">Creating an elastic pool from an existing **server** blade in the portal is the easiest way to move existing databases into an elastic pool.</span></span>

> [!NOTE]
> <span data-ttu-id="e0a4b-116">Można również utworzyć puli elastycznej, wyszukując **puli elastycznej SQL** w **Marketplace** lub klikając **+ Dodaj** w **puli elastycznej SQL** Przeglądaj bloku.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-116">You can also create an elastic pool by searching **SQL elastic pool** in the **Marketplace** or clicking **+Add** in the **SQL elastic pools** browse blade.</span></span> <span data-ttu-id="e0a4b-117">Jesteś w stanie umożliwia określenie nowego lub istniejącego serwera do obsługi przepływu pracy w tej puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-117">You are able to specify a new or existing server through this pool provisioning workflow.</span></span>
>
>

1. <span data-ttu-id="e0a4b-118">W [portalu Azure](http://portal.azure.com/), kliknij przycisk **więcej usług**  **>**  **serwerów SQL**, a następnie kliknij serwer, który zawiera bazy danych, które chcesz dodać do puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-118">In the [Azure portal](http://portal.azure.com/), click **More services** **>** **SQL servers**, and then click the server that contains the databases you want to add to an elastic pool.</span></span>
2. <span data-ttu-id="e0a4b-119">Kliknij przycisk **Nowa pula**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-119">Click **New pool**.</span></span>

    ![Dodawanie puli na serwerze](./media/sql-database-elastic-pool-create-portal/new-pool.png)

    <span data-ttu-id="e0a4b-121">**— Lub —**</span><span class="sxs-lookup"><span data-stu-id="e0a4b-121">**-OR-**</span></span>

    <span data-ttu-id="e0a4b-122">Może zostać wyświetlony komunikat z informacją, że są zalecane elastyczne pule serwera.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-122">You may see a message saying there are recommended elastic pools for the server.</span></span> <span data-ttu-id="e0a4b-123">Kliknij komunikat, aby wyświetlić pule zalecane na podstawie historycznych danych telemetrycznych użycia baz danych, a następnie kliknij przycisk warstwy, aby zobaczyć więcej szczegółów i dostosować pulę.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-123">Click the message to see the recommended pools based on historical database usage telemetry, and then click the tier to see more details and customize the pool.</span></span> <span data-ttu-id="e0a4b-124">Zobacz sekcję [Pojęcie zaleceń puli](#understand-elastic-pool-recommendations) w dalszej części tego artykułu, aby dowiedzieć się, w jaki sposób tworzone są zalecenia.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-124">See [Understand pool recommendations](#understand-elastic-pool-recommendations) later in this topic for how the recommendation is made.</span></span>

    ![zalecana pula](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)

3. <span data-ttu-id="e0a4b-126">**Puli elastycznej** zostanie wyświetlony blok, czyli gdzie Określ ustawienia dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-126">The **elastic pool** blade appears, which is where you specify the settings for your pool.</span></span> <span data-ttu-id="e0a4b-127">Jeśli kliknięto **nowej puli** w poprzednim kroku, warstwa cenowa jest **standardowe** jest wybrany domyślnie i nie baz danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-127">If you clicked **New pool** in the previous step, the pricing tier is **Standard** by default and no databases is selected.</span></span> <span data-ttu-id="e0a4b-128">Możesz utworzyć pustą pulę lub określić zestaw istniejących baz danych z tego serwera w celu przeniesienia ich do puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-128">You can create an empty pool, or specify a set of existing databases from that server to move into the pool.</span></span> <span data-ttu-id="e0a4b-129">Jeśli tworzysz zalecanej puli zalecana warstwa cenowa, ustawienia wydajności i listy baz danych są wstępnie, ale nadal można je zmienić.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-129">If you are creating a recommended pool, the recommended pricing tier, performance settings, and list of databases are prepopulated, but you can still change them.</span></span>

    ![Konfigurowanie puli elastycznej](./media/sql-database-elastic-pool-create-portal/configure-elastic-pool.png)

4. <span data-ttu-id="e0a4b-131">Określ nazwę puli elastycznej lub pozostaw wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-131">Specify a name for the elastic pool, or leave it as the default.</span></span>

### <a name="step-2-choose-a-pricing-tier"></a><span data-ttu-id="e0a4b-132">Krok 2. Wybieranie warstwy cenowej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-132">Step 2: Choose a pricing tier</span></span>

<span data-ttu-id="e0a4b-133">Warstwa cenowa puli Określa funkcje dostępne dla elastics w puli, a maksymalna liczba jednostek Edtu (maks. wartość eDTU) i dostępne dla każdej bazy danych magazynu (GB).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-133">The pool's pricing tier determines the features available to the elastics in the pool, and the maximum number of eDTUs (eDTU MAX), and storage (GBs) available to each database.</span></span> <span data-ttu-id="e0a4b-134">Aby uzyskać szczegółowe informacje, zobacz Warstwy usługi.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-134">For details, see Service Tiers.</span></span>

<span data-ttu-id="e0a4b-135">Aby zmienić warstwę cenową dla puli, kliknij przycisk **Warstwa cenowa**, kliknij wybraną warstwę cenową, a następnie kliknij przycisk **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-135">To change the pricing tier for the pool, click **Pricing tier**, click the pricing tier you want, and then click **Select**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0a4b-136">Po wybraniu warstwy cenowej i kliknięciu przycisku **OK** w ostatnim kroku w celu zatwierdzenia wprowadzonych zmian nie można już zmienić warstwy cenowej puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-136">After you choose the pricing tier and commit your changes by clicking **OK** in the last step, you won't be able to change the pricing tier of the pool.</span></span> <span data-ttu-id="e0a4b-137">Aby zmienić warstwę cenową istniejącej puli elastycznej, tworzenie elastycznej puli w ramach żądanej warstwy cenowej i przeprowadzić migrację bazy danych do nowej puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-137">To change the pricing tier for an existing elastic pool, create an elastic pool in the desired pricing tier and migrate the databases to this new pool.</span></span>
>

![Wybór warstwy cenowej](./media/sql-database-elastic-pool-create-portal/pricing-tier.png)

### <a name="step-3-configure-the-pool"></a><span data-ttu-id="e0a4b-139">Krok 3. Konfigurowanie puli</span><span class="sxs-lookup"><span data-stu-id="e0a4b-139">Step 3: Configure the pool</span></span>

<span data-ttu-id="e0a4b-140">Po ustawieniu warstwy cenowej, kliknij przycisk Konfiguruj pulę, którego można dodać bazy danych, ustawić jednostki Edtu i magazyn (GB puli), a wartość minimalna i maksymalna liczba jednostek Edtu dla elastics w puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-140">After setting the pricing tier, click Configure pool where you add databases, set pool eDTUs and storage (pool GBs), and where you set the min and max eDTUs for the elastics in the pool.</span></span>

1. <span data-ttu-id="e0a4b-141">Kliknij przycisk **Konfiguruj pulę**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-141">Click **Configure pool**</span></span>
2. <span data-ttu-id="e0a4b-142">Wybierz bazy danych, które chcesz dodać do puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-142">Select the databases you want to add to the pool.</span></span> <span data-ttu-id="e0a4b-143">Ten krok jest opcjonalny podczas tworzenia puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-143">This step is optional while creating the pool.</span></span> <span data-ttu-id="e0a4b-144">Bazy danych można dodać po jej utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-144">Databases can be added after the pool has been created.</span></span>
    <span data-ttu-id="e0a4b-145">Aby dodać bazy danych, kliknij przycisk **Dodaj bazę danych**, kliknij bazy danych, które chcesz dodać, a następnie kliknij przycisk **Wybierz**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-145">To add databases, click **Add database**, click the databases that you want to add, and then click the **Select** button.</span></span>

    ![Dodawanie baz danych](./media/sql-database-elastic-pool-create-portal/add-databases.png)

    <span data-ttu-id="e0a4b-147">Jeśli bazy danych, z którymi pracujesz, mają wystarczającą ilość historycznych danych telemetrycznych dotyczących użycia, aktualizacje wykresu **Szacowany poziom użycia jednostek eDTU i GB** oraz wykresu słupkowego **Rzeczywiste użycie jednostek eDTU** ułatwiają podejmowanie decyzji związanych z konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-147">If the databases you're working with have enough historical usage telemetry, the **Estimated eDTU and GB usage** graph and the **Actual eDTU usage** bar chart update to help you make configuration decisions.</span></span> <span data-ttu-id="e0a4b-148">Ponadto usługa może ułatwić wybranie odpowiedniego rozmiaru puli, wyświetlając komunikat z zaleceniami.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-148">Also, the service may give you a recommendation message to help you right-size the pool.</span></span> <span data-ttu-id="e0a4b-149">Patrz sekcja [Zalecenia dynamiczne](#understand-elastic-pool-recommendations).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-149">See [Dynamic Recommendations](#understand-elastic-pool-recommendations).</span></span>

3. <span data-ttu-id="e0a4b-150">Użyj elementów sterujących na stronie **Konfigurowanie puli**, aby eksplorować ustawienia i skonfigurować pulę.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-150">Use the controls on the **Configure pool** page to explore settings and configure your pool.</span></span> <span data-ttu-id="e0a4b-151">Zobacz [elastyczne pule limity](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) uzyskać więcej szczegółów na temat limitów dla każdej warstwy usług i zobacz [zagadnienia dotyczące cen i wydajności dla pul elastycznych](sql-database-elastic-pool.md) Aby uzyskać szczegółowe wskazówki dotyczące doboru wielkości puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-151">See [Elastic pools limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for more detail about limits for each service tier, and see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md) for detailed guidance on right-sizing an elastic pool.</span></span> <span data-ttu-id="e0a4b-152">Aby uzyskać więcej informacji na temat ustawień puli, zobacz [właściwości puli elastycznej](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-152">For more information about pool settings, see [Elastic pool properties](sql-database-elastic-pool.md#database-properties-for-pooled-databases).</span></span>

    ![Konfigurowanie puli elastycznej](./media/sql-database-elastic-pool-create-portal/configure-performance.png)

4. <span data-ttu-id="e0a4b-154">Po wprowadzeniu zmian w ustawieniach kliknij przycisk **Wybierz** w bloku **Konfigurowanie puli**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-154">Click **Select** in the **Configure Pool** blade after changing settings.</span></span>
5. <span data-ttu-id="e0a4b-155">Kliknij przycisk **OK**, aby utworzyć pulę.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-155">Click **OK** to create the pool.</span></span>

## <a name="understand-elastic-pool-recommendations"></a><span data-ttu-id="e0a4b-156">Omówienie zaleceń puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-156">Understand elastic pool recommendations</span></span>

<span data-ttu-id="e0a4b-157">Usługa SQL Database ocenia historyczne dane użycia bazy danych i zaleca zastosowanie co najmniej jednej puli baz danych, jeśli okaże się, że jest to bardziej ekonomiczne rozwiązanie niż używanie pojedynczych baz danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-157">The SQL Database service evaluates usage history and recommends one or more pools when it is more cost-effective than using single databases.</span></span> <span data-ttu-id="e0a4b-158">Każde zalecenie jest konfigurowane z unikatowym podzbiorem baz danych serwera, które są najlepiej dopasowane do puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-158">Each recommendation is configured with a unique subset of the server's databases that best fit the pool.</span></span>

![zalecana pula](./media/sql-database-elastic-pool-create-portal/recommended-pool.png)  

<span data-ttu-id="e0a4b-160">Zalecenie puli obejmuje:</span><span class="sxs-lookup"><span data-stu-id="e0a4b-160">The pool recommendation comprises:</span></span>

- <span data-ttu-id="e0a4b-161">Warstwę cenową dla puli (podstawowa, standardowa, Premium lub Premium RS)</span><span class="sxs-lookup"><span data-stu-id="e0a4b-161">A pricing tier for the pool (Basic, Standard, Premium, or Premium RS)</span></span>
- <span data-ttu-id="e0a4b-162">Odpowiednie **Jednostki eDTU PULI** (określane również jako Maks. wartość eDTU na pulę)</span><span class="sxs-lookup"><span data-stu-id="e0a4b-162">Appropriate **POOL eDTUs** (also called Max eDTUs per pool)</span></span>
- <span data-ttu-id="e0a4b-163">**Maks. wartość eDTU** i **Min. wartość eDTU** na bazę danych</span><span class="sxs-lookup"><span data-stu-id="e0a4b-163">The **eDTU MAX** and **eDTU Min** per database</span></span>
- <span data-ttu-id="e0a4b-164">Listę zalecanych baz danych dla puli</span><span class="sxs-lookup"><span data-stu-id="e0a4b-164">The list of recommended databases for the pool</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e0a4b-165">Podczas rekomendowania pul usługa uwzględnia dane telemetryczne z ostatnich 30 dni.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-165">The service takes the last 30 days of telemetry into account when recommending pools.</span></span> <span data-ttu-id="e0a4b-166">Dla bazy danych wziąć pod uwagę jako potencjalny puli elastycznej musi istnieć co najmniej 7 dni.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-166">For a database to be considered as a candidate for an elastic pool, it must exist for at least 7 days.</span></span> <span data-ttu-id="e0a4b-167">Bazy, które znajdują się już w puli elastycznej, nie są brane pod uwagę podczas tworzenia zaleceń dla puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-167">Databases that are already in an elastic pool are not considered as candidates for elastic pool recommendations.</span></span>
>

<span data-ttu-id="e0a4b-168">Usługa oblicza zapotrzebowanie na zasoby oraz opłacalność przenoszenia pojedynczych baz danych w każdej warstwie usług do pul w tej samej warstwie.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-168">The service evaluates resource needs and cost effectiveness of moving the single databases in each service tier into pools of the same tier.</span></span> <span data-ttu-id="e0a4b-169">Na przykład wszystkie bazy danych w warstwie Standardowej na serwerze są oceniane pod względem dopasowania do Standardowej puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-169">For example, all Standard databases on a server are assessed for their fit into a Standard Elastic Pool.</span></span> <span data-ttu-id="e0a4b-170">Oznacza to, że usługa nie tworzy zaleceń międzywarstwowych, takich jak przeniesienie bazy danych z warstwy Standardowej do puli Premium.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-170">This means the service does not make cross-tier recommendations such as moving a Standard database into a Premium pool.</span></span>

<span data-ttu-id="e0a4b-171">Po dodaniu bazy danych do puli, zalecenia są generowane dynamicznie na podstawie historycznych danych użycia wybranych baz danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-171">After adding databases to the pool, recommendations are dynamically generated based on the historical usage of the databases you have selected.</span></span> <span data-ttu-id="e0a4b-172">Te zalecenia są wyświetlane w jednostek eDTU i GB wykres użycia i transparent zalecenia w górnej części **Konfigurowanie puli** bloku.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-172">These recommendations are shown in the eDTU and GB usage chart and in a recommendation banner at the top of the **Configure pool** blade.</span></span> <span data-ttu-id="e0a4b-173">Zalecenia te mają na celu ułatwić tworzenie puli elastycznej zoptymalizowane pod kątem konkretnych baz danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-173">These recommendations are intended to assist you in creating an elastic pool optimized for your specific databases.</span></span>

![zalecenia dynamiczne](./media/sql-database-elastic-pool-create-portal/dynamic-recommendation.png)

## <a name="manage-and-monitor-an-elastic-pool"></a><span data-ttu-id="e0a4b-175">Zarządzanie i monitorowanie puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-175">Manage and monitor an elastic pool</span></span>

<span data-ttu-id="e0a4b-176">Azure portal umożliwia monitorowanie i zarządzanie elastycznej puli baz danych w puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-176">You can use the Azure portal to monitor and manage an elastic pool and the databases in the pool.</span></span> <span data-ttu-id="e0a4b-177">W portalu można monitorować użycie puli elastycznej i baz danych w tej puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-177">From the portal, you can monitor the utilization of an elastic pool and the databases within that pool.</span></span> <span data-ttu-id="e0a4b-178">Można również utworzyć zestaw zmian do puli elastycznej i Prześlij wszystkie zmiany w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-178">You can also make a set of changes to your elastic pool and submit all changes at the same time.</span></span> <span data-ttu-id="e0a4b-179">Te zmiany obejmują dodawanie lub usuwanie baz danych, zmiana ustawień puli elastycznej lub zmiany ustawień bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-179">These changes include adding or removing databases, changing your elastic pool settings, or changing your database settings.</span></span>

<span data-ttu-id="e0a4b-180">Na poniższym rysunku przedstawiono przykład puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-180">The following graphic shows an example elastic pool.</span></span> <span data-ttu-id="e0a4b-181">Widok zawiera:</span><span class="sxs-lookup"><span data-stu-id="e0a4b-181">The view includes:</span></span>

*  <span data-ttu-id="e0a4b-182">Wykresy do monitorowania użycia zasobów w puli elastycznej i baz danych zawartych w puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-182">Charts for monitoring resource usage of both the elastic pool and the databases contained in the pool.</span></span>
*  <span data-ttu-id="e0a4b-183">**Konfiguruj** puli przycisk, aby wprowadzić zmiany w puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-183">The **Configure** pool button to make changes to the elastic pool.</span></span>
*  <span data-ttu-id="e0a4b-184">**Utwórz bazę danych** przycisku, który tworzy bazę danych i dodaje go do bieżącej puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-184">The **Create database** button that creates a database and adds it to the current elastic pool.</span></span>
*  <span data-ttu-id="e0a4b-185">Zadania elastyczne, które ułatwiają zarządzanie dużej liczby baz danych, uruchamiając skrypty Transact SQL wszystkich baz danych na liście.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-185">Elastic jobs that help you manage large numbers of databases by running Transact SQL scripts against all databases in a list.</span></span>

![Widok puli][2]

<span data-ttu-id="e0a4b-187">Można przejść do określonej puli, aby wyświetlić jego wykorzystania zasobów.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-187">You can go to a particular pool to see its resource utilization.</span></span> <span data-ttu-id="e0a4b-188">Domyślnie skonfigurowano puli pokazanie użycia magazynu i liczby jednostek eDTU w ciągu ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-188">By default, the pool is configured to show storage and eDTU usage for the last hour.</span></span> <span data-ttu-id="e0a4b-189">Wykres można skonfigurować do wyświetlenia różnych metryk za pośrednictwem różnych okna czasowe.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-189">The chart can be configured to show different metrics over various time windows.</span></span>

1. <span data-ttu-id="e0a4b-190">Wybierz do pracy z puli elastycznej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-190">Select an elastic pool to work with.</span></span>
2. <span data-ttu-id="e0a4b-191">W obszarze **monitorowania puli elastycznej** jest wykres z etykietą **wykorzystania zasobów**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-191">Under **Elastic Pool Monitoring** is a chart labeled **Resource utilization**.</span></span> <span data-ttu-id="e0a4b-192">Kliknij wykres.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-192">Click the chart.</span></span>

    ![Monitorowanie puli elastycznej][3]

    <span data-ttu-id="e0a4b-194">**Metryka** zostanie otwarty blok, przedstawiając wyświetlenia szczegółowych informacji o określonej metryki w określone okno czasu.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-194">The **Metric** blade opens, showing a detailed view of the specified metrics over the specified time window.</span></span>   

    ![Blok metryki][9]

### <a name="to-customize-the-chart-display"></a><span data-ttu-id="e0a4b-196">Aby dostosować wyświetlanie wykresu</span><span class="sxs-lookup"><span data-stu-id="e0a4b-196">To customize the chart display</span></span>

<span data-ttu-id="e0a4b-197">Wykres i metryki bloku, aby wyświetlić innych metryk, takich jak procent, procent we/wy danych i dziennika we/wy procent wykorzystania procesora CPU można edytować.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-197">You can edit the chart and the metric blade to display other metrics such as CPU percentage, data IO percentage, and log IO percentage used.</span></span>

1. <span data-ttu-id="e0a4b-198">W bloku metryki, kliknij **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-198">On the metric blade, click **Edit**.</span></span>

    ![Kliknij przycisk Edytuj][6]

2. <span data-ttu-id="e0a4b-200">W **Edytuj wykres** bloku, wybierz zakres czasu (Ostatnia godzina dzisiaj, lub ostatni tydzień), lub kliknij przycisk **niestandardowych** aby wybrać wszystkie zakres dat w ciągu ostatnich dwóch tygodni.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-200">In the **Edit Chart** blade, select a time range (past hour, today, or past week), or click **custom** to select any date range in the last two weeks.</span></span> <span data-ttu-id="e0a4b-201">Wybierz typ wykresu (paska lub linii), a następnie wybierz zasoby do monitorowania.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-201">Select the chart type (bar or line), then select the resources to monitor.</span></span>

   > [!Note]
   > <span data-ttu-id="e0a4b-202">Tylko metryki z tej samej jednostki miary mogą być wyświetlane na wykresie, w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-202">Only metrics with the same unit of measure can be displayed in the chart at the same time.</span></span> <span data-ttu-id="e0a4b-203">Na przykład w przypadku wybrania "procent liczby jednostek eDTU" następnie można wybrać tylko innych metryk odsetku jako jednostka miary.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-203">For example, if you select "eDTU percentage" then you can only select other metrics with percentage as the unit of measure.</span></span>
   >

    ![Kliknij przycisk Edytuj](./media/sql-database-elastic-pool-manage-portal/edit-chart.png)

3. <span data-ttu-id="e0a4b-205">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-205">Then click **OK**.</span></span>

## <a name="manage-and-monitor-databases-in-an-elastic-pool"></a><span data-ttu-id="e0a4b-206">Zarządzanie i monitorowanie baz danych w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-206">Manage and monitor databases in an elastic pool</span></span>

<span data-ttu-id="e0a4b-207">Można również monitorować pojedyncze bazy danych dla potencjalne problemy.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-207">Individual databases can also be monitored for potential trouble.</span></span>

1. <span data-ttu-id="e0a4b-208">W obszarze **elastycznej bazy danych monitorowania**, jest wykres przedstawia metryki pięć baz danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-208">Under **Elastic Database Monitoring**, there is a chart that displays metrics for five databases.</span></span> <span data-ttu-id="e0a4b-209">Domyślnie wykresu wyświetla top 5 baz danych w puli przez użycie w jednostkach eDTU średni w ostatniej godziny.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-209">By default, the chart displays the top 5 databases in the pool by average eDTU usage in the past hour.</span></span> <span data-ttu-id="e0a4b-210">Kliknij wykres.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-210">Click the chart.</span></span>

    ![Monitorowanie puli elastycznej][4]

2. <span data-ttu-id="e0a4b-212">**Wykorzystania zasobów bazy danych** zostanie wyświetlony blok.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-212">The **Database Resource Utilization** blade appears.</span></span> <span data-ttu-id="e0a4b-213">Zapewnia to szczegółowy widok użycia bazy danych w puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-213">This provides a detailed view of the database usage in the pool.</span></span> <span data-ttu-id="e0a4b-214">Przy użyciu siatki w dolnej części bloku, można wybrać żadnych baz danych w puli, aby wyświetlić jego użycia na wykresie (maksymalnie 5 bazy danych).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-214">Using the grid in the lower part of the blade, you can select any databases in the pool to display its usage in the chart (up to 5 databases).</span></span> <span data-ttu-id="e0a4b-215">Można również dostosować metryki i przedziału czasowego wyświetlane na wykresie, klikając **Edytuj wykres**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-215">You can also customize the metrics and time window displayed in the chart by clicking **Edit chart**.</span></span>

    ![Blok wykorzystanie zasobów bazy danych][8]

### <a name="to-customize-the-view"></a><span data-ttu-id="e0a4b-217">Aby dostosować widok</span><span class="sxs-lookup"><span data-stu-id="e0a4b-217">To customize the view</span></span>

1. <span data-ttu-id="e0a4b-218">W **bazy danych wykorzystania zasobów** bloku, kliknij przycisk **Edytuj wykres**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-218">In the **Database resource utilization** blade, click **Edit chart**.</span></span>

    ![Kliknij pozycję Edytuj wykres](./media/sql-database-elastic-pool-manage-portal/db-utilization-blade.png)

2. <span data-ttu-id="e0a4b-220">W **Edytuj** wykresu bloku, wybierz zakres czasu (Ostatnia godzina lub po 24 godzinach) lub kliknij przycisk **niestandardowych** wybierz inny dzień w ciągu ostatnich 2 tygodni do wyświetlenia.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-220">In the **Edit** chart blade, select a time range (past hour or past 24 hours), or click **custom** to select a different day in the past 2 weeks to display.</span></span>

    ![Kliknij przycisk niestandardowe](./media/sql-database-elastic-pool-manage-portal/editchart-date-time.png)

3. <span data-ttu-id="e0a4b-222">Kliknij przycisk **porównania baz danych przez** listy rozwijanej, aby wybrać inną metrykę do używania przy porównywaniu baz danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-222">Click the **Compare databases by** dropdown to select a different metric to use when comparing databases.</span></span>

    ![Edytuj wykres](./media/sql-database-elastic-pool-manage-portal/edit-comparison-metric.png)

### <a name="to-select-databases-to-monitor"></a><span data-ttu-id="e0a4b-224">Aby wybrać baz danych do monitorowania</span><span class="sxs-lookup"><span data-stu-id="e0a4b-224">To select databases to monitor</span></span>

<span data-ttu-id="e0a4b-225">Na liście bazy danych w **wykorzystania zasobów bazy danych** bloku można znaleźć określonej bazy danych przez wyszukiwanie na stronach na liście lub wpisując nazwy bazy danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-225">In the database list in the **Database Resource Utilization** blade, you can find particular databases by looking through the pages in the list or by typing in the name of a database.</span></span> <span data-ttu-id="e0a4b-226">Użyj pola wyboru, aby wybrać bazę danych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-226">Use the checkbox to select the database.</span></span>

![Wyszukaj baz danych do monitorowania][7]


## <a name="add-an-alert-to-an-elastic-pool-resource"></a><span data-ttu-id="e0a4b-228">Dodawanie alertu do zasobu puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-228">Add an alert to an elastic pool resource</span></span>

<span data-ttu-id="e0a4b-229">Reguły można dodać do puli elastycznej puli elastycznej trafienia ustawiony próg użycia wysyłania wiadomości e-mail do osób lub alertu ciągów do adresu URL punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-229">You can add rules to an elastic pool that send email to people or alert strings to URL endpoints when the elastic pool hits a utilization threshold that you set up.</span></span>

<span data-ttu-id="e0a4b-230">**Aby dodać alert do dowolnego zasobu:**</span><span class="sxs-lookup"><span data-stu-id="e0a4b-230">**To add an alert to any resource:**</span></span>

1. <span data-ttu-id="e0a4b-231">Kliknij przycisk **wykorzystania zasobów** wykresu, aby otworzyć **Metryka** bloku, kliknij przycisk **Dodaj alert**, a następnie wypełnij informacje w **dodać regułę alertu** bloku (**zasobów** jest automatycznie ustawiony do pracy z puli).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-231">Click the **Resource utilization** chart to open the **Metric** blade, click **Add alert**, and then fill out the information in the **Add an alert rule** blade (**Resource** is automatically set up to be the pool you're working with).</span></span>
2. <span data-ttu-id="e0a4b-232">Wpisz **nazwa** i **opis** , które identyfikują alert i adresaci.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-232">Type a **Name** and **Description** that identifies the alert to you and the recipients.</span></span>
3. <span data-ttu-id="e0a4b-233">Wybierz **Metryka** przewidzianą do alertów z listy.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-233">Choose a **Metric** that you want to alert from the list.</span></span>

    <span data-ttu-id="e0a4b-234">Wykres przedstawia dynamicznie wykorzystania zasobów dla tej metryki, pomaga wybrać progu.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-234">The chart dynamically shows resource utilization for that metric to help you choose a threshold.</span></span>

4. <span data-ttu-id="e0a4b-235">Wybierz **warunku** (większe niż poniżej, itd.) i **próg**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-235">Choose a **Condition** (greater than, less than, etc.) and a **Threshold**.</span></span>
5. <span data-ttu-id="e0a4b-236">Wybierz **okres** czas, przez który metryki reguły muszą zostać spełnione przed wyzwalaczy alertu.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-236">Choose a **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span>
6. <span data-ttu-id="e0a4b-237">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-237">Click **OK**.</span></span>

<span data-ttu-id="e0a4b-238">Aby uzyskać więcej informacji, zobacz [tworzyć alerty bazy danych SQL w portalu Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-238">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="e0a4b-239">Przenoszenie bazy danych w puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-239">Move a database into an elastic pool</span></span>

<span data-ttu-id="e0a4b-240">Można dodać lub usunąć bazy danych z istniejącej puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-240">You can add or remove databases from an existing pool.</span></span> <span data-ttu-id="e0a4b-241">Bazy danych może być w innych pulach.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-241">The databases can be in other pools.</span></span> <span data-ttu-id="e0a4b-242">Jednak można dodawać tylko baz danych, które znajdują się na tym samym serwerze logicznym.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-242">However, you can only add databases that are on the same logical server.</span></span>

1. <span data-ttu-id="e0a4b-243">W bloku dla puli w obszarze **elastycznych baz danych** kliknij **Konfigurowanie puli**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-243">In the blade for the pool, under **Elastic databases** click **Configure pool**.</span></span>

    ![Kliknij przycisk Konfiguruj pulę][1]

2. <span data-ttu-id="e0a4b-245">W **Konfigurowanie puli** bloku, kliknij przycisk **dodać do puli**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-245">In the **Configure pool** blade, click **Add to pool**.</span></span>

    ![Kliknij przycisk Dodaj do puli](./media/sql-database-elastic-pool-manage-portal/add-to-pool.png)


3. <span data-ttu-id="e0a4b-247">W **dodać bazy danych** bloku, wybierz bazę danych lub baz danych do dodania do puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-247">In the **Add databases** blade, select the database or databases to add to the pool.</span></span> <span data-ttu-id="e0a4b-248">Następnie kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-248">Then click **Select**.</span></span>

    ![Wybierz bazy danych do dodania](./media/sql-database-elastic-pool-manage-portal/add-databases-pool.png)

    <span data-ttu-id="e0a4b-250">**Konfigurowanie puli** blok zawiera teraz bazy danych wybrane do dodania z jego stan **oczekujące**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-250">The **Configure pool** blade now lists the database you selected to be added, with its status set to **Pending**.</span></span>

    ![Dodawanie puli oczekujące](./media/sql-database-elastic-pool-manage-portal/pending-additions.png)

3. <span data-ttu-id="e0a4b-252">W **bloku Konfigurowanie puli**, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-252">In the **Configure pool blade**, click **Save**.</span></span>

    ![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="e0a4b-254">Przenoszenie bazy danych z puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-254">Move a database out of an elastic pool</span></span>

1. <span data-ttu-id="e0a4b-255">W **Konfigurowanie puli** bloku, wybierz bazę danych lub baz danych do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-255">In the **Configure pool** blade, select the database or databases to remove.</span></span>

    ![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/select-pools-removal.png)

2. <span data-ttu-id="e0a4b-257">Kliknij przycisk **usunąć z puli**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-257">Click **Remove from pool**.</span></span>

    ![Wyświetlanie listy baz danych](./media/sql-database-elastic-pool-manage-portal/click-remove.png)

    <span data-ttu-id="e0a4b-259">**Konfigurowanie puli** blok zawiera teraz bazy danych wybrane do usunięcia z jego stan **oczekujące**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-259">The **Configure pool** blade now lists the database you selected to be removed with its status set to **Pending**.</span></span>

    ![Podgląd bazy danych Dodawanie i usuwanie](./media/sql-database-elastic-pool-manage-portal/pending-removal.png)

3. <span data-ttu-id="e0a4b-261">W **bloku Konfigurowanie puli**, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-261">In the **Configure pool blade**, click **Save**.</span></span>

    ![Klikanie pozycji Zapisz.](./media/sql-database-elastic-pool-manage-portal/click-save.png)

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="e0a4b-263">Zmień ustawienia wydajności puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-263">Change performance settings of an elastic pool</span></span>

<span data-ttu-id="e0a4b-264">Podczas monitorowania wykorzystania zasobów w puli elastycznej może stwierdzić, że pewnych zmian są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-264">As you monitor the resource utilization of an elastic pool, you may discover that some adjustments are needed.</span></span> <span data-ttu-id="e0a4b-265">Może być puli wymaga zmian w granicach wydajność lub pamięć masową.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-265">Maybe the pool needs a change in the performance or storage limits.</span></span> <span data-ttu-id="e0a4b-266">Prawdopodobnie chcesz zmienić ustawienia bazy danych w puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-266">Possibly you want to change the database settings in the pool.</span></span> <span data-ttu-id="e0a4b-267">Ustawienia puli można zmienić w dowolnym momencie można uzyskać równowagę wydajności i kosztów.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-267">You can change the setup of the pool at any time to get the best balance of performance and cost.</span></span> <span data-ttu-id="e0a4b-268">Zobacz [kiedy należy puli elastycznej użyć?](sql-database-elastic-pool.md) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-268">See [When should an elastic pool be used?](sql-database-elastic-pool.md) for more information.</span></span>

<span data-ttu-id="e0a4b-269">Aby zmienić limitów jednostek Edtu i magazynu dla każdej puli i jednostek Edtu na bazę danych:</span><span class="sxs-lookup"><span data-stu-id="e0a4b-269">To change the eDTUs or storage limits per pool, and eDTUs per database:</span></span>

1. <span data-ttu-id="e0a4b-270">Otwórz **Konfigurowanie puli** bloku.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-270">Open the **Configure pool** blade.</span></span>

    <span data-ttu-id="e0a4b-271">W obszarze **ustawienia puli elastycznej**, za pomocą suwaka albo wprowadzenia zmian ustawień puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-271">Under **elastic pool settings**, use either slider to change the pool settings.</span></span>

    ![Użycie zasobów w puli elastycznej](./media/sql-database-elastic-pool-manage-portal/resize-pool.png)

2. <span data-ttu-id="e0a4b-273">Po zmianie ustawienia pokazuje szacowany koszt miesięczne zmiany.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-273">When the setting changes, the display shows the estimated monthly cost of the change.</span></span>

    ![Aktualizacja puli elastycznej i nowych miesięczny koszt](./media/sql-database-elastic-pool-manage-portal/pool-change-edtu.png)

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="e0a4b-275">Czas oczekiwania operacji puli elastycznej</span><span class="sxs-lookup"><span data-stu-id="e0a4b-275">Latency of elastic pool operations</span></span>
* <span data-ttu-id="e0a4b-276">Zmiana wartości min Edtu na bazę danych lub maksymalna liczba jednostek Edtu na bazę danych zazwyczaj kończy się w ciągu 5 minut lub mniej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-276">Changing the min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="e0a4b-277">Zmiana jednostek Edtu na pulę zależy od całkowitej ilości miejsca używanego przez wszystkie bazy danych w puli.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-277">Changing the eDTUs per pool depends on the total amount of space used by all databases in the pool.</span></span> <span data-ttu-id="e0a4b-278">Wprowadzanie zmian trwa średnio 90 minut na każde 100 GB.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-278">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="e0a4b-279">Na przykład jeśli całkowita ilość miejsca, używany przez wszystkie bazy danych w puli jest 200 GB, oczekiwany czas oczekiwania do zmiany puli liczbę jednostek eDTU na pulę wynosi 3 godziny, a następnie lub mniej.</span><span class="sxs-lookup"><span data-stu-id="e0a4b-279">For example, if the total space used by all databases in the pool is 200 GB, then the expected latency for changing the pool eDTU per pool is 3 hours or less.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0a4b-280">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0a4b-280">Next steps</span></span>

- <span data-ttu-id="e0a4b-281">Aby zrozumieć, co puli elastycznej zobacz [puli elastycznej bazy danych SQL](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-281">To understand what an elastic pool is, see [SQL Database elastic pool](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="e0a4b-282">Aby uzyskać wskazówki dotyczące wykorzystujących pule elastyczne, zobacz [zagadnienia dotyczące cen i wydajności dla pul elastycznych](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-282">For guidance on using elastic pools, see [Price and performance considerations for elastic pools](sql-database-elastic-pool.md).</span></span>
- <span data-ttu-id="e0a4b-283">Aby użyć zadania elastyczne umożliwiają uruchamianie skryptów języka Transact-SQL na dowolnej liczbie baz danych w puli, zobacz [omówienie zadania elastyczne](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-283">To use elastic jobs to run Transact-SQL scripts against any number of databases in the pool, see [Elastic jobs overview](sql-database-elastic-jobs-overview.md).</span></span>
- <span data-ttu-id="e0a4b-284">Aby zapytania na dowolnej liczbie baz danych w puli, zobacz [elastycznej zapytań — omówienie](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-284">To query across any number of databases in the pool, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
- <span data-ttu-id="e0a4b-285">Dla transakcji dowolnej liczbie baz danych w puli, zobacz [transakcji elastycznej](sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0a4b-285">For transactions any number of databases in the pool, see [Elastic transactions](sql-database-elastic-transactions-overview.md).</span></span>


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
