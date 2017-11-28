---
title: "Jak skalować pamięć podręczna Azure Redis | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skalować swoich wystąpień w pamięci podręcznej Redis Azure"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 350db214-3b7c-4877-bd43-fef6df2db96c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: sdanie
ms.openlocfilehash: 91b3580491a1e3504a3891b66606a9bd18c0638f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-scale-azure-redis-cache"></a><span data-ttu-id="777ca-103">Jak skalować pamięć podręczna Azure Redis</span><span class="sxs-lookup"><span data-stu-id="777ca-103">How to Scale Azure Redis Cache</span></span>
<span data-ttu-id="777ca-104">Pamięć podręczna Redis Azure ma inną pamięci podręcznej oferty, które zapewniają elastyczność w wyborze rozmiar pamięci podręcznej i funkcje.</span><span class="sxs-lookup"><span data-stu-id="777ca-104">Azure Redis Cache has different cache offerings, which provide flexibility in the choice of cache size and features.</span></span> <span data-ttu-id="777ca-105">Po utworzeniu pamięci podręcznej można skalować rozmiar i warstwę cenową pamięci podręcznej w przypadku zmiany wymagań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="777ca-105">After a cache is created, you can scale the size and the pricing tier of the cache if the requirements of your application change.</span></span> <span data-ttu-id="777ca-106">W tym artykule przedstawiono sposób skalowania pamięci podręcznej w portalu Azure i przy użyciu narzędzi, takich jak Azure PowerShell i interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="777ca-106">This article shows you how to scale your cache in both the Azure portal and using tools such as Azure PowerShell and Azure CLI.</span></span>

## <a name="when-to-scale"></a><span data-ttu-id="777ca-107">Kiedy skalować</span><span class="sxs-lookup"><span data-stu-id="777ca-107">When to scale</span></span>
<span data-ttu-id="777ca-108">Można użyć [monitorowania](cache-how-to-monitor.md) funkcje pamięci podręcznej Redis Azure do monitorowania kondycji i wydajności pamięci podręcznej i ułatwić określenie, kiedy skalować pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-108">You can use the [monitoring](cache-how-to-monitor.md) features of Azure Redis Cache to monitor the health and performance of your cache and help determine when to scale the cache.</span></span> 

<span data-ttu-id="777ca-109">Można monitorować następujące metryki w celu określenia, jeśli potrzebujesz do skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-109">You can monitor the following metrics to help determine if you need to scale.</span></span>

* <span data-ttu-id="777ca-110">Obciążenie serwera redis</span><span class="sxs-lookup"><span data-stu-id="777ca-110">Redis Server Load</span></span>
* <span data-ttu-id="777ca-111">Użycie pamięci</span><span class="sxs-lookup"><span data-stu-id="777ca-111">Memory Usage</span></span>
* <span data-ttu-id="777ca-112">Przepustowość sieci</span><span class="sxs-lookup"><span data-stu-id="777ca-112">Network Bandwidth</span></span>
* <span data-ttu-id="777ca-113">Użycie procesora CPU</span><span class="sxs-lookup"><span data-stu-id="777ca-113">CPU Usage</span></span>

<span data-ttu-id="777ca-114">Jeśli okaże się, czy pamięć podręczna jest już spełniający wymagania aplikacji, można skalować do pamięci podręcznej większy lub mniejszy cenowym, które jest odpowiednie dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="777ca-114">If you determine that your cache is no longer meeting your application's requirements, you can scale to a larger or smaller cache pricing tier that is right for your application.</span></span> <span data-ttu-id="777ca-115">Aby uzyskać więcej informacji na temat określania pamięci podręcznej, które cenowym do użycia, zobacz [jakie oferty pamięć podręczna Redis i rozmiar użyć](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span><span class="sxs-lookup"><span data-stu-id="777ca-115">For more information on determining which cache pricing tier to use, see [What Redis Cache offering and size should I use](cache-faq.md#what-redis-cache-offering-and-size-should-i-use).</span></span>

## <a name="scale-a-cache"></a><span data-ttu-id="777ca-116">Skala pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="777ca-116">Scale a cache</span></span>
<span data-ttu-id="777ca-117">Aby skalować pamięć podręczną [przejdź do pamięci podręcznej](cache-configure.md#configure-redis-cache-settings) w [portalu Azure](https://portal.azure.com) i kliknij przycisk **skali** z **zasobów menu**.</span><span class="sxs-lookup"><span data-stu-id="777ca-117">To scale your cache, [browse to the cache](cache-configure.md#configure-redis-cache-settings) in the [Azure portal](https://portal.azure.com) and click **Scale** from the **Resource menu**.</span></span>

![Skalowanie](./media/cache-how-to-scale/redis-cache-scale-menu.png)

<span data-ttu-id="777ca-119">Wybierz żądaną warstwę cenową z **wybierz warstwę cenową** bloku i kliknij przycisk **wybierz**.</span><span class="sxs-lookup"><span data-stu-id="777ca-119">Select the desired pricing tier from the **Select pricing tier** blade and click **Select**.</span></span>

![Warstwa cenowa][redis-cache-pricing-tier-blade]


<span data-ttu-id="777ca-121">Można skalować do innej warstwy cenowej z następującymi ograniczeniami:</span><span class="sxs-lookup"><span data-stu-id="777ca-121">You can scale to a different pricing tier with the following restrictions:</span></span>

* <span data-ttu-id="777ca-122">Nie można skalować z wyższej warstwy cenowej do dolnej warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="777ca-122">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="777ca-123">Nie można skalować z **Premium** pamięci podręcznej w dół do **standardowe** lub **podstawowe** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-123">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="777ca-124">Nie można skalować z **standardowe** pamięci podręcznej w dół do **podstawowe** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-124">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="777ca-125">Możesz skalować z **podstawowe** pamięci podręcznej do **standardowe** pamięci podręcznej, ale nie można zmienić rozmiar w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="777ca-125">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="777ca-126">Jeśli potrzebujesz zmienić rozmiar, należy na żądany rozmiar kolejnych operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-126">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="777ca-127">Nie można skalować z **podstawowe** bezpośrednio do pamięci podręcznej **Premium** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-127">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="777ca-128">Należy skalować z **podstawowe** do **standardowe** w jednej operacji skalowania, a następnie z **standardowe** do **Premium** w kolejnych operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-128">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="777ca-129">Nie można skalować z większego rozmiaru w dół do **C0 (250 MB)** rozmiar.</span><span class="sxs-lookup"><span data-stu-id="777ca-129">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
 
<span data-ttu-id="777ca-130">Gdy pamięć podręczna jest skalowanie do nowej warstwy cenowej **skalowanie** stan jest wyświetlany w **pamięci podręcznej Redis** bloku.</span><span class="sxs-lookup"><span data-stu-id="777ca-130">While the cache is scaling to the new pricing tier, a **Scaling** status is displayed in the **Redis Cache** blade.</span></span>

![Skalowanie][redis-cache-scaling]

<span data-ttu-id="777ca-132">Po zakończeniu skalowanie stan zmieni się z **skalowanie** do **systemem**.</span><span class="sxs-lookup"><span data-stu-id="777ca-132">When scaling is complete, the status changes from **Scaling** to **Running**.</span></span>

## <a name="how-to-automate-a-scaling-operation"></a><span data-ttu-id="777ca-133">Jak zautomatyzować operacji skalowania</span><span class="sxs-lookup"><span data-stu-id="777ca-133">How to automate a scaling operation</span></span>
<span data-ttu-id="777ca-134">Oprócz skalowania swoich wystąpień w pamięci podręcznej w portalu Azure, można skalować przy użyciu poleceń cmdlet programu PowerShell, interfejsu wiersza polecenia Azure i przy użyciu programu Microsoft Azure Management bibliotek (MAML).</span><span class="sxs-lookup"><span data-stu-id="777ca-134">In addition to scaling your cache instances in the Azure portal, you can scale using PowerShell cmdlets, Azure CLI, and by using the Microsoft Azure Management Libraries (MAML).</span></span> 

* [<span data-ttu-id="777ca-135">Skala przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="777ca-135">Scale using PowerShell</span></span>](#scale-using-powershell)
* [<span data-ttu-id="777ca-136">Skala przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="777ca-136">Scale using Azure CLI</span></span>](#scale-using-azure-cli)
* [<span data-ttu-id="777ca-137">Przy użyciu MAML skali</span><span class="sxs-lookup"><span data-stu-id="777ca-137">Scale using MAML</span></span>](#scale-using-maml)

### <a name="scale-using-powershell"></a><span data-ttu-id="777ca-138">Skala przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="777ca-138">Scale using PowerShell</span></span>
<span data-ttu-id="777ca-139">Możesz skalować swoich wystąpień pamięci podręcznej Redis Azure przy użyciu programu PowerShell przy użyciu [AzureRmRedisCache zestaw](https://msdn.microsoft.com/library/azure/mt634518.aspx) polecenia cmdlet podczas `Size`, `Sku`, lub `ShardCount` są modyfikowane właściwości.</span><span class="sxs-lookup"><span data-stu-id="777ca-139">You can scale your Azure Redis Cache instances with PowerShell by using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> <span data-ttu-id="777ca-140">Poniższy przykład przedstawia sposób skalowania pamięci podręcznej o nazwie `myCache` do 2,5 GB pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-140">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> 

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="777ca-141">Aby uzyskać więcej informacji na temat skalowania przy użyciu programu PowerShell, zobacz [można skalować pamięć podręczną Redis przy użyciu programu Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span><span class="sxs-lookup"><span data-stu-id="777ca-141">For more information on scaling with PowerShell, see [To scale a Redis cache using Powershell](cache-howto-manage-redis-cache-powershell.md#scale).</span></span>

### <a name="scale-using-azure-cli"></a><span data-ttu-id="777ca-142">Skala przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="777ca-142">Scale using Azure CLI</span></span>
<span data-ttu-id="777ca-143">Aby skalować swoich wystąpień pamięci podręcznej Redis Azure za pomocą interfejsu wiersza polecenia Azure, należy wywołać `azure rediscache set` poleceń i podaj żądane zmiany w konfiguracji obejmujących nowy rozmiar, jednostki sku lub rozmiar klastra, w zależności od żądanej operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-143">To scale your Azure Redis Cache instances using Azure CLI, call the `azure rediscache set` command and pass in the desired configuration changes that include a new size, sku, or cluster size, depending on the desired scaling operation.</span></span>

<span data-ttu-id="777ca-144">Aby uzyskać więcej informacji na temat skalowania z wiersza polecenia platformy Azure, zobacz [zmienić ustawienia istniejących pamięci podręcznej Redis](cache-manage-cli.md#scale).</span><span class="sxs-lookup"><span data-stu-id="777ca-144">For more information on scaling with Azure CLI, see [Change settings of an existing Redis Cache](cache-manage-cli.md#scale).</span></span>

### <a name="scale-using-maml"></a><span data-ttu-id="777ca-145">Przy użyciu MAML skali</span><span class="sxs-lookup"><span data-stu-id="777ca-145">Scale using MAML</span></span>
<span data-ttu-id="777ca-146">Aby skalować pamięć podręczna Redis Azure wystąpienia przy użyciu [Microsoft Azure Management bibliotek (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), wywołaj `IRedisOperations.CreateOrUpdate` — metoda i Przekaż nowy rozmiar `RedisProperties.SKU.Capacity`.</span><span class="sxs-lookup"><span data-stu-id="777ca-146">To scale your Azure Redis Cache instances using the [Microsoft Azure Management Libraries (MAML)](http://azure.microsoft.com/updates/management-libraries-for-net-release-announcement/), call the `IRedisOperations.CreateOrUpdate` method and pass in the new size for the `RedisProperties.SKU.Capacity`.</span></span>

    static void Main(string[] args)
    {
        // For instructions on getting the access token, see
        // https://azure.microsoft.com/documentation/articles/cache-configure/#access-keys
        string token = GetAuthorizationHeader();

        TokenCloudCredentials creds = new TokenCloudCredentials(subscriptionId,token);

        RedisManagementClient client = new RedisManagementClient(creds);
        var redisProperties = new RedisProperties();

        // To scale, set a new size for the redisSKUCapacity parameter.
        redisProperties.Sku = new Sku(redisSKUName,redisSKUFamily,redisSKUCapacity);
        redisProperties.RedisVersion = redisVersion;
        var redisParams = new RedisCreateOrUpdateParameters(redisProperties, redisCacheRegion);
        client.Redis.CreateOrUpdate(resourceGroupName,cacheName, redisParams);
    }

<span data-ttu-id="777ca-147">Aby uzyskać więcej informacji, zobacz [zarządzania pamięcią podręczną Redis przy użyciu MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) próbki.</span><span class="sxs-lookup"><span data-stu-id="777ca-147">For more information, see the [Manage Redis Cache using MAML](https://github.com/rustd/RedisSamples/tree/master/ManageCacheUsingMAML) sample.</span></span>

## <a name="scaling-faq"></a><span data-ttu-id="777ca-148">Skalowanie — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="777ca-148">Scaling FAQ</span></span>
<span data-ttu-id="777ca-149">Poniższa lista zawiera odpowiedzi na często zadawane pytania dotyczące pamięci podręcznej Redis Azure skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-149">The following list contains answers to commonly asked questions about Azure Redis Cache scaling.</span></span>

* [<span data-ttu-id="777ca-150">Aby z lub w pamięci podręcznej Premium I skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-150">Can I scale to, from, or within a Premium cache?</span></span>](#can-i-scale-to-from-or-within-a-premium-cache)
* [<span data-ttu-id="777ca-151">Po skalowania, muszę zmienić klucze nazwy lub dostępu do pamięci podręcznej?</span><span class="sxs-lookup"><span data-stu-id="777ca-151">After scaling, do I have to change my cache name or access keys?</span></span>](#after-scaling-do-i-have-to-change-my-cache-name-or-access-keys)
* [<span data-ttu-id="777ca-152">Jak działa skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-152">How does scaling work?</span></span>](#how-does-scaling-work)
* [<span data-ttu-id="777ca-153">Spowoduje utratę danych z mojej pamięci podręcznej podczas skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-153">Will I lose data from my cache during scaling?</span></span>](#will-i-lose-data-from-my-cache-during-scaling)
* [<span data-ttu-id="777ca-154">Jest niestandardowe baz danych zmodyfikowane ustawienie podczas skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-154">Is my custom databases setting affected during scaling?</span></span>](#is-my-custom-databases-setting-affected-during-scaling)
* [<span data-ttu-id="777ca-155">Moje pamięci podręcznej będzie dostępna podczas skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-155">Will my cache be available during scaling?</span></span>](#will-my-cache-be-available-during-scaling)
* [<span data-ttu-id="777ca-156">Operacje, które nie są obsługiwane</span><span class="sxs-lookup"><span data-stu-id="777ca-156">Operations that are not supported</span></span>](#operations-that-are-not-supported)
* [<span data-ttu-id="777ca-157">Jak długo skalowanie podąża?</span><span class="sxs-lookup"><span data-stu-id="777ca-157">How long does scaling take?</span></span>](#how-long-does-scaling-take)
* [<span data-ttu-id="777ca-158">Jak sprawdzić, kiedy jest ukończone skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-158">How can I tell when scaling is complete?</span></span>](#how-can-i-tell-when-scaling-is-complete)

### <a name="can-i-scale-to-from-or-within-a-premium-cache"></a><span data-ttu-id="777ca-159">Aby z lub w pamięci podręcznej Premium I skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-159">Can I scale to, from, or within a Premium cache?</span></span>
* <span data-ttu-id="777ca-160">Nie można skalować z **Premium** pamięci podręcznej w dół do **podstawowe** lub **standardowe** warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="777ca-160">You can't scale from a **Premium** cache down to a **Basic** or **Standard** pricing tier.</span></span>
* <span data-ttu-id="777ca-161">Możesz skalować z jednego **Premium** pamięci podręcznej cenowym do innego.</span><span class="sxs-lookup"><span data-stu-id="777ca-161">You can scale from one **Premium** cache pricing tier to another.</span></span>
* <span data-ttu-id="777ca-162">Nie można skalować z **podstawowe** bezpośrednio do pamięci podręcznej **Premium** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-162">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="777ca-163">Użytkownik musi najpierw skali: od **podstawowe** do **standardowe** w jednej operacji skalowania, a następnie z **standardowe** do **Premium** w kolejnych operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-163">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="777ca-164">Jeśli włączono klaster podczas tworzenia Twojej **Premium** pamięci podręcznej, możesz [zmienić rozmiar klastra](cache-how-to-premium-clustering.md#cluster-size).</span><span class="sxs-lookup"><span data-stu-id="777ca-164">If you enabled clustering when you created your **Premium** cache, you can [change the cluster size](cache-how-to-premium-clustering.md#cluster-size).</span></span> <span data-ttu-id="777ca-165">Jeśli pamięć podręczna została utworzona bez klastra włączone, nie można skonfigurować klaster w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="777ca-165">If your cache was created without clustering enabled, you can't configure clustering at a later time.</span></span>
  
  <span data-ttu-id="777ca-166">Aby uzyskać więcej informacji, zobacz temat [Konfigurowanie usługi klastrowania dla usługi Azure Redis Cache w warstwie Premium](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="777ca-166">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>

### <a name="after-scaling-do-i-have-to-change-my-cache-name-or-access-keys"></a><span data-ttu-id="777ca-167">Po skalowania, muszę zmienić klucze nazwy lub dostępu do pamięci podręcznej?</span><span class="sxs-lookup"><span data-stu-id="777ca-167">After scaling, do I have to change my cache name or access keys?</span></span>
<span data-ttu-id="777ca-168">Nie, nazwa pamięci podręcznej, a klucze nie uległy zmianie podczas operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-168">No, your cache name and keys are unchanged during a scaling operation.</span></span>

### <a name="how-does-scaling-work"></a><span data-ttu-id="777ca-169">Jak działa skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-169">How does scaling work?</span></span>
* <span data-ttu-id="777ca-170">Gdy **podstawowe** skalowania do innego rozmiaru pamięci podręcznej, zostanie zamknięta i nową pamięć podręczną zostanie zainicjowana przy użyciu nowego rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="777ca-170">When a **Basic** cache is scaled to a different size, it is shut down and a new cache is provisioned using the new size.</span></span> <span data-ttu-id="777ca-171">W tym czasie pamięci podręcznej jest niedostępna i nie zostały utracone wszystkie dane w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-171">During this time, the cache is unavailable and all data in the cache is lost.</span></span>
* <span data-ttu-id="777ca-172">Gdy **podstawowe** skalowania do pamięci podręcznej **standardowe** pamięci podręcznej, zainicjowaniu obsługi pamięci podręcznej repliki, a dane są kopiowane z głównej pamięci podręcznej w pamięci podręcznej repliki.</span><span class="sxs-lookup"><span data-stu-id="777ca-172">When a **Basic** cache is scaled to a **Standard** cache, a replica cache is provisioned and the data is copied from the primary cache to the replica cache.</span></span> <span data-ttu-id="777ca-173">Pamięci podręcznej pozostaje dostępna w trakcie skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-173">The cache remains available during the scaling process.</span></span>
* <span data-ttu-id="777ca-174">Gdy **standardowe** pamięci podręcznej jest skalowana do innego rozmiaru lub do **Premium** pamięci podręcznej, jednej z replik jest zamknięte i ponownie zainicjować obsługi administracyjnej do nowego rozmiaru i dane przesyłane przez, a następnie innej repliki wykonuje trybu failover przed jej ponownym zainicjowaniu obsługi, podobny do procesu, która występuje podczas awarii jednego z węzłów pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-174">When a **Standard** cache is scaled to a different size or to a **Premium** cache, one of the replicas is shut down and re-provisioned to the new size and the data transferred over, and then the other replica performs a failover before it is re-provisioned, similar to the process that occurs during a failure of one of the cache nodes.</span></span>

### <a name="will-i-lose-data-from-my-cache-during-scaling"></a><span data-ttu-id="777ca-175">Spowoduje utratę danych z mojej pamięci podręcznej podczas skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-175">Will I lose data from my cache during scaling?</span></span>
* <span data-ttu-id="777ca-176">Gdy **podstawowe** skalowania do nowego rozmiaru pamięci podręcznej, wszystkie dane zostaną utracone i pamięci podręcznej jest niedostępny podczas operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-176">When a **Basic** cache is scaled to a new size, all data is lost and the cache is unavailable during the scaling operation.</span></span>
* <span data-ttu-id="777ca-177">Gdy **podstawowe** skalowania do pamięci podręcznej **standardowe** pamięci podręcznej, dane w pamięci podręcznej zwykle są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="777ca-177">When a **Basic** cache is scaled to a **Standard** cache, the data in the cache is typically preserved.</span></span>
* <span data-ttu-id="777ca-178">Podczas **standardowe** pamięci podręcznej jest skalowana większy rozmiar lub warstwy, lub **Premium** skalowania do większy rozmiar pamięci podręcznej, wszystkie dane zwykle są zachowywane.</span><span class="sxs-lookup"><span data-stu-id="777ca-178">When a **Standard** cache is scaled to a larger size or tier, or a **Premium** cache is scaled to a larger size, all data is typically preserved.</span></span> <span data-ttu-id="777ca-179">Podczas skalowania **standardowe** lub **Premium** pamięci podręcznej w dół mniejszy rozmiar, dane mogą zostać utracone w zależności od tego, jak dużo danych jest w pamięci podręcznej związane z nowy rozmiar podczas jego skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-179">When scaling a **Standard** or **Premium** cache down to a smaller size, data may be lost depending on how much data is in the cache related to the new size when it is scaled.</span></span> <span data-ttu-id="777ca-180">Jeśli dane zostaną utracone podczas skalowania, klucze są wykluczony przy użyciu [allkeys lru](http://redis.io/topics/lru-cache) zasady wykluczania.</span><span class="sxs-lookup"><span data-stu-id="777ca-180">If data is lost when scaling down, keys are evicted using the [allkeys-lru](http://redis.io/topics/lru-cache) eviction policy.</span></span> 

### <a name="is-my-custom-databases-setting-affected-during-scaling"></a><span data-ttu-id="777ca-181">Jest niestandardowe baz danych zmodyfikowane ustawienie podczas skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-181">Is my custom databases setting affected during scaling?</span></span>
<span data-ttu-id="777ca-182">Niektóre warstw cenowych mają różne [baz danych limity](cache-configure.md#databases), więc istnieją pewne zagadnienia dotyczące skalowania Jeśli skonfigurowana wartość niestandardową dla `databases` ustawienie podczas tworzenia pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-182">Some pricing tiers have different [databases limits](cache-configure.md#databases), so there are some considerations when scaling down if you configured a custom value for the `databases` setting during cache creation.</span></span>

* <span data-ttu-id="777ca-183">Podczas skalowania do warstwy cenowej o niższej `databases` limit niż warstwa bieżąca:</span><span class="sxs-lookup"><span data-stu-id="777ca-183">When scaling to a pricing tier with a lower `databases` limit than the current tier:</span></span>
  * <span data-ttu-id="777ca-184">Jeśli używasz domyślną liczbę `databases` czyli 16 dla wszystkich warstw cenowych zostały utracone żadne dane.</span><span class="sxs-lookup"><span data-stu-id="777ca-184">If you are using the default number of `databases` which is 16 for all pricing tiers, no data is lost.</span></span>
  * <span data-ttu-id="777ca-185">Jeśli używasz niestandardowego liczba `databases` który mieści się w granicach na warstwę, do której należy są skalowania, to `databases` ustawienie jest zachowywane i nie zostały utracone żadne dane.</span><span class="sxs-lookup"><span data-stu-id="777ca-185">If you are using a custom number of `databases` that falls within the limits for the tier to which you are scaling, this `databases` setting is retained and no data is lost.</span></span>
  * <span data-ttu-id="777ca-186">Jeśli używasz niestandardowego liczba `databases` przekraczający limit nową warstwę `databases` ustawienie jest obniżona z limitami nową warstwę, a wszystkie dane w usunięte bazy danych zostaną utracone.</span><span class="sxs-lookup"><span data-stu-id="777ca-186">If you are using a custom number of `databases` that exceeds the limits of the new tier, the `databases` setting is lowered to the limits of the new tier and all data in the removed databases is lost.</span></span>
* <span data-ttu-id="777ca-187">Podczas skalowania do warstwy cenowej z tego samego lub wyższego `databases` limit niż warstwa bieżąca Twojej `databases` ustawienie jest zachowywane i nie zostały utracone żadne dane.</span><span class="sxs-lookup"><span data-stu-id="777ca-187">When scaling to a pricing tier with the same or higher `databases` limit than the current tier your `databases` setting is retained and no data is lost.</span></span>

<span data-ttu-id="777ca-188">Zwróć uwagę, że chociaż standardowa i Premium pamięci podręcznych SLA 99,9%, dostępności, nie umowy dotyczącej poziomu usług dla utraty danych.</span><span class="sxs-lookup"><span data-stu-id="777ca-188">Note that while Standard and Premium caches have a 99.9% SLA for availability, there is no SLA for data loss.</span></span>

### <a name="will-my-cache-be-available-during-scaling"></a><span data-ttu-id="777ca-189">Moje pamięci podręcznej będzie dostępna podczas skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-189">Will my cache be available during scaling?</span></span>
* <span data-ttu-id="777ca-190">**Standardowe** i **Premium** pamięci podręcznych pozostają dostępne podczas operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-190">**Standard** and **Premium** caches remain available during the scaling operation.</span></span>
* <span data-ttu-id="777ca-191">**Podstawowe** pamięci podręcznych są w trybie offline podczas skalowania na inny rozmiar operacji, ale pozostają dostępne podczas skalowania z **podstawowe** do **standardowe**.</span><span class="sxs-lookup"><span data-stu-id="777ca-191">**Basic** caches are offline during scaling operations to a different size, but remain available when scaling from **Basic** to **Standard**.</span></span>

### <a name="operations-that-are-not-supported"></a><span data-ttu-id="777ca-192">Operacje, które nie są obsługiwane</span><span class="sxs-lookup"><span data-stu-id="777ca-192">Operations that are not supported</span></span>
* <span data-ttu-id="777ca-193">Nie można skalować z wyższej warstwy cenowej do dolnej warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="777ca-193">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
  * <span data-ttu-id="777ca-194">Nie można skalować z **Premium** pamięci podręcznej w dół do **standardowe** lub **podstawowe** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-194">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
  * <span data-ttu-id="777ca-195">Nie można skalować z **standardowe** pamięci podręcznej w dół do **podstawowe** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-195">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
* <span data-ttu-id="777ca-196">Możesz skalować z **podstawowe** pamięci podręcznej do **standardowe** pamięci podręcznej, ale nie można zmienić rozmiar w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="777ca-196">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="777ca-197">Jeśli potrzebujesz zmienić rozmiar, należy na żądany rozmiar kolejnych operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-197">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
* <span data-ttu-id="777ca-198">Nie można skalować z **podstawowe** bezpośrednio do pamięci podręcznej **Premium** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-198">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="777ca-199">Użytkownik musi najpierw skali: od **podstawowe** do **standardowe** w jednej operacji skalowania, a następnie z **standardowe** do **Premium** w kolejnych operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-199">You must first scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
* <span data-ttu-id="777ca-200">Nie można skalować z większego rozmiaru w dół do **C0 (250 MB)** rozmiar.</span><span class="sxs-lookup"><span data-stu-id="777ca-200">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>

<span data-ttu-id="777ca-201">W przypadku niepowodzenia operacji skalowania usługi spróbuje przywrócić działanie i pamięci podręcznej zostanie przywrócony oryginalny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="777ca-201">If a scaling operation fails, the service will try to revert the operation and the cache will revert to the original size.</span></span>

### <a name="how-long-does-scaling-take"></a><span data-ttu-id="777ca-202">Jak długo skalowanie podąża?</span><span class="sxs-lookup"><span data-stu-id="777ca-202">How long does scaling take?</span></span>
<span data-ttu-id="777ca-203">Skalowanie trwa około 20 minut w zależności od tego, jak dużo danych jest w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="777ca-203">Scaling takes approximately 20 minutes, depending on how much data is in the cache.</span></span>

### <a name="how-can-i-tell-when-scaling-is-complete"></a><span data-ttu-id="777ca-204">Jak sprawdzić, kiedy jest ukończone skalowania?</span><span class="sxs-lookup"><span data-stu-id="777ca-204">How can I tell when scaling is complete?</span></span>
<span data-ttu-id="777ca-205">W portalu Azure może zobaczyć trwających operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="777ca-205">In the Azure portal you can see the scaling operation in progress.</span></span> <span data-ttu-id="777ca-206">Po zakończeniu skalowanie zmiany stanu pamięci podręcznej na **systemem**.</span><span class="sxs-lookup"><span data-stu-id="777ca-206">When scaling is complete, the status of the cache changes to **Running**.</span></span>

<!-- IMAGES -->

[redis-cache-pricing-tier-blade]: ./media/cache-how-to-scale/redis-cache-pricing-tier-blade.png

[redis-cache-scaling]: ./media/cache-how-to-scale/redis-cache-scaling.png



