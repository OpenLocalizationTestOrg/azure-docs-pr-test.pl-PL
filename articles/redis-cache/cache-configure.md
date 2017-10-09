---
title: "tooconfigure aaaHow pamięć podręczna Redis Azure | Dokumentacja firmy Microsoft"
description: "Omówienie hello domyślną konfigurację pamięci podręcznej Redis pamięć podręczna Redis Azure i Dowiedz się, jak tooconfigure Azure Redis wystąpień pamięci podręcznej"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: d0bf2e1f-6a26-4e62-85ba-d82b35fc5aa6
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 08/22/2017
ms.author: sdanie
ms.openlocfilehash: 46bffb74cdf40e0e0a99c3a83dbe06d6fe1ea65b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-azure-redis-cache"></a><span data-ttu-id="d527b-103">Jak tooconfigure Azure pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="d527b-103">How tooconfigure Azure Redis Cache</span></span>
<span data-ttu-id="d527b-104">W tym temacie opisano, jak aktualizacja i tooreview hello konfiguracji dla swoich wystąpień w pamięci podręcznej Redis Azure i konfigurację domyślną hello obejmuje serwera Redis dla wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="d527b-104">This topic describes how tooreview and update hello configuration for your Azure Redis Cache instances, and covers hello default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="d527b-105">Aby uzyskać więcej informacji na temat konfigurowania przy użyciu funkcji pamięci podręcznej premium, zobacz [jak trwałości tooconfigure](cache-how-to-premium-persistence.md), [jak tooconfigure klastrowanie](cache-how-to-premium-clustering.md), i [obsługi tooconfigure sieci wirtualnej ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-105">For more information on configuring and using premium cache features, see [How tooconfigure persistence](cache-how-to-premium-persistence.md), [How tooconfigure clustering](cache-how-to-premium-clustering.md), and [How tooconfigure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="d527b-106">Skonfiguruj ustawienia pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="d527b-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="d527b-107">Ustawienia pamięci podręcznej Redis Azure są wyświetlane i skonfigurowane na powitania **pamięci podręcznej Redis** bloku przy użyciu hello **zasobów Menu**.</span><span class="sxs-lookup"><span data-stu-id="d527b-107">Azure Redis Cache settings are viewed and configured on hello **Redis Cache** blade using hello **Resource Menu**.</span></span>

![Ustawienia pamięci podręcznej redis](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="d527b-109">Można wyświetlić i skonfigurować następujące ustawienia za pomocą hello hello **zasobów Menu**.</span><span class="sxs-lookup"><span data-stu-id="d527b-109">You can view and configure hello following settings using hello **Resource Menu**.</span></span>

* [<span data-ttu-id="d527b-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d527b-110">Overview</span></span>](#overview)
* [<span data-ttu-id="d527b-111">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="d527b-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="d527b-112">Kontrola dostępu (IAM)</span><span class="sxs-lookup"><span data-stu-id="d527b-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="d527b-113">Tagi</span><span class="sxs-lookup"><span data-stu-id="d527b-113">Tags</span></span>](#tags)
* [<span data-ttu-id="d527b-114">Diagnozowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="d527b-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="d527b-115">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="d527b-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="d527b-116">Klawisze dostępu</span><span class="sxs-lookup"><span data-stu-id="d527b-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="d527b-117">Ustawienia zaawansowane</span><span class="sxs-lookup"><span data-stu-id="d527b-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="d527b-118">Klasyfikator pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="d527b-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="d527b-119">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="d527b-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="d527b-120">Rozmiar klastra redis</span><span class="sxs-lookup"><span data-stu-id="d527b-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="d527b-121">Trwałość danych redis</span><span class="sxs-lookup"><span data-stu-id="d527b-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="d527b-122">Aktualizacje harmonogramu</span><span class="sxs-lookup"><span data-stu-id="d527b-122">Schedule updates</span></span>](#schedule-updates)
    * <span data-ttu-id="d527b-123">[Geo-replication](#geo-replication) (Replikacja geograficzna)</span><span class="sxs-lookup"><span data-stu-id="d527b-123">[Geo-replication](#geo-replication)</span></span>
    * [<span data-ttu-id="d527b-124">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="d527b-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="d527b-125">Zapora</span><span class="sxs-lookup"><span data-stu-id="d527b-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="d527b-126">Właściwości</span><span class="sxs-lookup"><span data-stu-id="d527b-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="d527b-127">Blokady</span><span class="sxs-lookup"><span data-stu-id="d527b-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="d527b-128">Skrypt automatyzacji</span><span class="sxs-lookup"><span data-stu-id="d527b-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="d527b-129">Administracja</span><span class="sxs-lookup"><span data-stu-id="d527b-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="d527b-130">Importowanie danych</span><span class="sxs-lookup"><span data-stu-id="d527b-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="d527b-131">Eksportowanie danych</span><span class="sxs-lookup"><span data-stu-id="d527b-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="d527b-132">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="d527b-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="d527b-133">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="d527b-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="d527b-134">Redis metryk</span><span class="sxs-lookup"><span data-stu-id="d527b-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="d527b-135">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="d527b-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="d527b-136">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="d527b-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="d527b-137">Rozwiązywanie problemów z ustawieniami i pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="d527b-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="d527b-138">Kondycja zasobów</span><span class="sxs-lookup"><span data-stu-id="d527b-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="d527b-139">Nowe żądanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="d527b-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="d527b-140">Omówienie</span><span class="sxs-lookup"><span data-stu-id="d527b-140">Overview</span></span>

<span data-ttu-id="d527b-141">**Omówienie** zapewnia możesz podstawowych informacji o pamięci podręcznej, takie jak nazwa, porty, warstwa cenowa i metryki wybranego pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="d527b-142">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="d527b-142">Activity log</span></span>

<span data-ttu-id="d527b-143">Kliknij przycisk **dziennik aktywności** tooview akcje wykonywane w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-143">Click **Activity log** tooview actions performed on your cache.</span></span> <span data-ttu-id="d527b-144">Można również użyć filtrowania tooexpand tooinclude tego widoku inne zasoby.</span><span class="sxs-lookup"><span data-stu-id="d527b-144">You can also use filtering tooexpand this view tooinclude other resources.</span></span> <span data-ttu-id="d527b-145">Aby uzyskać więcej informacji na temat pracy z dziennikami inspekcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="d527b-146">Aby uzyskać więcej informacji dotyczących monitorowania zdarzeń pamięć podręczna Redis Azure, zobacz [operacji i alerty](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="d527b-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="d527b-147">Kontrola dostępu (IAM)</span><span class="sxs-lookup"><span data-stu-id="d527b-147">Access control (IAM)</span></span>

<span data-ttu-id="d527b-148">Witaj **(IAM) kontroli dostępu** sekcji zapewnia obsługę kontroli dostępu opartej na rolach (RBAC) w hello Azure toohelp portalu organizacji spełniają ich wymagania dotyczące zarządzania dostępu po prostu i dokładnie.</span><span class="sxs-lookup"><span data-stu-id="d527b-148">hello **Access control (IAM)** section provides support for role-based access control (RBAC) in hello Azure portal toohelp organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="d527b-149">Aby uzyskać więcej informacji, zobacz [kontroli dostępu opartej na rolach w portalu Azure hello](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-149">For more information, see [Role-based access control in hello Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="d527b-150">Tagi</span><span class="sxs-lookup"><span data-stu-id="d527b-150">Tags</span></span>

<span data-ttu-id="d527b-151">Witaj **tagi** sekcji pomaga organizować zasobów.</span><span class="sxs-lookup"><span data-stu-id="d527b-151">hello **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="d527b-152">Aby uzyskać więcej informacji, zobacz [używanie tagów tooorganize zasobów platformy Azure](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-152">For more information, see [Using tags tooorganize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="d527b-153">Diagnozowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="d527b-153">Diagnose and solve problems</span></span>

<span data-ttu-id="d527b-154">Kliknij przycisk **diagnozowanie i rozwiązywanie problemów** toobe dostarczone z najczęściej występujących problemów i strategii w celu ich rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d527b-154">Click **Diagnose and solve problems** toobe provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="d527b-155">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="d527b-155">Settings</span></span>
<span data-ttu-id="d527b-156">Witaj **ustawienia** sekcji pozwala tooaccess i skonfiguruj następujące ustawienia dla pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="d527b-156">hello **Settings** section allows you tooaccess and configure hello following settings for your cache.</span></span>

* [<span data-ttu-id="d527b-157">Klawisze dostępu</span><span class="sxs-lookup"><span data-stu-id="d527b-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="d527b-158">Ustawienia zaawansowane</span><span class="sxs-lookup"><span data-stu-id="d527b-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="d527b-159">Klasyfikator pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="d527b-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="d527b-160">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="d527b-160">Scale</span></span>](#scale)
* [<span data-ttu-id="d527b-161">Rozmiar klastra redis</span><span class="sxs-lookup"><span data-stu-id="d527b-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="d527b-162">Trwałość danych redis</span><span class="sxs-lookup"><span data-stu-id="d527b-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="d527b-163">Aktualizacje harmonogramu</span><span class="sxs-lookup"><span data-stu-id="d527b-163">Schedule updates</span></span>](#schedule-updates)
* <span data-ttu-id="d527b-164">[Geo-replication](#geo-replication) (Replikacja geograficzna)</span><span class="sxs-lookup"><span data-stu-id="d527b-164">[Geo-replication](#geo-replication)</span></span>
* [<span data-ttu-id="d527b-165">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="d527b-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="d527b-166">Zapora</span><span class="sxs-lookup"><span data-stu-id="d527b-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="d527b-167">Właściwości</span><span class="sxs-lookup"><span data-stu-id="d527b-167">Properties</span></span>](#properties)
* [<span data-ttu-id="d527b-168">Blokady</span><span class="sxs-lookup"><span data-stu-id="d527b-168">Locks</span></span>](#locks)
* [<span data-ttu-id="d527b-169">Skrypt automatyzacji</span><span class="sxs-lookup"><span data-stu-id="d527b-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="d527b-170">Klawisze dostępu</span><span class="sxs-lookup"><span data-stu-id="d527b-170">Access keys</span></span>
<span data-ttu-id="d527b-171">Kliknij przycisk **klucze dostępu** tooview lub regenerate hello dostępu do kluczy dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-171">Click **Access keys** tooview or regenerate hello access keys for your cache.</span></span> <span data-ttu-id="d527b-172">Klucze te są używane przez klientów hello łączenie tooyour pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-172">These keys are used by hello clients connecting tooyour cache.</span></span>

![Klucze dostępu pamięci podręcznej redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="d527b-174">Ustawienia zaawansowane</span><span class="sxs-lookup"><span data-stu-id="d527b-174">Advanced settings</span></span>
<span data-ttu-id="d527b-175">Witaj następujące ustawienia są konfigurowane na powitania **Zaawansowane ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="d527b-175">hello following settings are configured on hello **Advanced settings** blade.</span></span>

* [<span data-ttu-id="d527b-176">Porty dostępu</span><span class="sxs-lookup"><span data-stu-id="d527b-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="d527b-177">Zasady pamięci</span><span class="sxs-lookup"><span data-stu-id="d527b-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="d527b-178">Powiadomienia przestrzeni kluczy (ustawienia zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="d527b-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="d527b-179">Porty dostępu</span><span class="sxs-lookup"><span data-stu-id="d527b-179">Access Ports</span></span>
<span data-ttu-id="d527b-180">Domyślnie dostęp inny niż za pomocą protokołu SSL jest zablokowany dla nowych pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="d527b-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="d527b-181">tooenable hello bez użycia protokołu SSL portu, kliknij przycisk **nr** dla **zezwolić na dostęp tylko za pośrednictwem protokołu SSL** na powitania **Zaawansowane ustawienia** bloku, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d527b-181">tooenable hello non-SSL port, click **No** for **Allow access only via SSL** on hello **Advanced settings** blade and then click **Save**.</span></span>

![Porty dostępu pamięci podręcznej redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="d527b-183">Zasady pamięci</span><span class="sxs-lookup"><span data-stu-id="d527b-183">Memory policies</span></span>
<span data-ttu-id="d527b-184">Witaj **zasad Maxmemory**, **zastrzeżone maxmemory**, i **zastrzeżone maxfragmentationmemory** ustawień na powitania **Zaawansowane ustawienia**bloku konfigurowania zasad pamięci hello hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-184">hello **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on hello **Advanced settings** blade configure hello memory policies for hello cache.</span></span>

![Zasady Maxmemory pamięci podręcznej redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="d527b-186">**Zasady Maxmemory** skonfiguruje zasady wykluczania hello hello pamięci podręcznej i pozwala toochoose z hello następujące zasady wykluczenia:</span><span class="sxs-lookup"><span data-stu-id="d527b-186">**Maxmemory policy** configures hello eviction policy for hello cache and allows you toochoose from hello following eviction policies:</span></span>

* <span data-ttu-id="d527b-187">`volatile-lru`— jest to domyślna hello.</span><span class="sxs-lookup"><span data-stu-id="d527b-187">`volatile-lru` - this is hello default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="d527b-188">Aby uzyskać więcej informacji na temat `maxmemory` zasad, zobacz [zasady wykluczania](http://redis.io/topics/lru-cache#eviction-policies).</span><span class="sxs-lookup"><span data-stu-id="d527b-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="d527b-189">Witaj **zastrzeżone maxmemory** skonfigurowanie hello ilość pamięci w Megabajtach, które jest zastrzeżone dla operacji-cache, takich jak replikacji w trybie failover.</span><span class="sxs-lookup"><span data-stu-id="d527b-189">hello **maxmemory-reserved** setting configures hello amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="d527b-190">Ustawienie tej wartości umożliwia toohave więcej spójne środowisko serwera Redis gdy zmienia się obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d527b-190">Setting this value allows you toohave a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="d527b-191">Ta wartość musi być ustawiona wyższych obciążeń, które są zapisu ciężki.</span><span class="sxs-lookup"><span data-stu-id="d527b-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="d527b-192">Pamięć jest zarezerwowana dla takich operacji, jest niedostępna dla magazynu danych z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="d527b-193">Witaj **zastrzeżone maxfragmentationmemory** skonfigurowanie hello ilość pamięci w Megabajtach, które jest zastrzeżone tooaccommodate fragmentacji pamięci.</span><span class="sxs-lookup"><span data-stu-id="d527b-193">hello **maxfragmentationmemory-reserved** setting configures hello amount of memory in MB that is reserved tooaccommodate for memory fragmentation.</span></span> <span data-ttu-id="d527b-194">Ustawienie tej wartości umożliwia toohave więcej spójne środowisko serwera Redis hello pamięć podręczna jest pełna lub Współczynnik zamknięcia toofull i hello fragmentacji również jest wysoka.</span><span class="sxs-lookup"><span data-stu-id="d527b-194">Setting this value allows you toohave a more consistent Redis server experience when hello cache is full or close toofull and hello fragmentation ratio is also high.</span></span> <span data-ttu-id="d527b-195">Pamięć jest zarezerwowana dla takich operacji, jest niedostępna dla magazynu danych z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="d527b-196">Tooconsider rzecz, wybierając nową wartość rezerwacji pamięci (**zastrzeżone maxmemory** lub **zastrzeżone maxfragmentationmemory**) jest jak tej zmiany mogą wpłynąć na pamięci podręcznej, który jest już uruchomione z duże ilości danych.</span><span class="sxs-lookup"><span data-stu-id="d527b-196">One thing tooconsider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="d527b-197">Na przykład jeśli użytkownik ma 53 GB pamięci podręcznej z 49 GB danych, a następnie zmień hello rezerwacji wartość too8 GB, to spowoduje porzucenie hello maksymalna dostępna pamięć dla systemu hello too45 GB.</span><span class="sxs-lookup"><span data-stu-id="d527b-197">For instance, if you have a 53 GB cache with 49 GB of data, then change hello reservation value too8 GB, this will drop hello max available memory for hello system down too45 GB.</span></span> <span data-ttu-id="d527b-198">Jeśli bieżące `used_memory` lub `used_memory_rss` wartości są wyższe niż hello nowego limitu 45 GB, a następnie hello system będzie mieć danych tooevict przed zakończeniem `used_memory` i `used_memory_rss` są poniżej 45 GB.</span><span class="sxs-lookup"><span data-stu-id="d527b-198">If either your current `used_memory` or your `used_memory_rss` values are higher than hello new limit of 45 GB, then hello system will have tooevict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="d527b-199">Wykluczanie może zwiększyć fragmentacji pamięci i obciążenia serwera.</span><span class="sxs-lookup"><span data-stu-id="d527b-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="d527b-200">Aby uzyskać więcej informacji w pamięci podręcznej metryk, takich jak `used_memory` i `used_memory_rss`, zobacz [dostępne metryki i raportowania interwałów](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="d527b-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d527b-201">Witaj **zastrzeżone maxmemory** i **zastrzeżone maxfragmentationmemory** ustawienia są dostępne tylko dla Standard i Premium przechowuje w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-201">hello **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="d527b-202">Powiadomienia przestrzeni kluczy (ustawienia zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="d527b-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="d527b-203">Redis na powitania skonfigurowano powiadomienia przestrzeni kluczy **Zaawansowane ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="d527b-203">Redis keyspace notifications are configured on hello **Advanced settings** blade.</span></span> <span data-ttu-id="d527b-204">Powiadomienia przestrzeni kluczy pozwalają klientom tooreceive powiadomienia w przypadku wystąpienia określonych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="d527b-204">Keyspace notifications allow clients tooreceive notifications when certain events occur.</span></span>

![Zaawansowane ustawienia pamięci podręcznej redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="d527b-206">Przestrzeni kluczy powiadomień i hello **powiadomienia przestrzeni kluczy zdarzenia** ustawienia są dostępne tylko dla pamięci podręcznej standardowa i Premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-206">Keyspace notifications and hello **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="d527b-207">Aby uzyskać więcej informacji, zobacz [Redis powiadomienia przestrzeni kluczy](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="d527b-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="d527b-208">Przykładowy kod, zobacz hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) pliku w hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) próbki.</span><span class="sxs-lookup"><span data-stu-id="d527b-208">For sample code, see hello [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in hello [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="d527b-209">Klasyfikator pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="d527b-209">Redis Cache Advisor</span></span>
<span data-ttu-id="d527b-210">Witaj **Advisor pamięci podręcznej Redis** blok zawiera zalecenia dotyczące pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-210">hello **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="d527b-211">Podczas wykonywania normalnych operacji zostaną wyświetlone żadnych zaleceń.</span><span class="sxs-lookup"><span data-stu-id="d527b-211">During normal operations, no recommendations are displayed.</span></span> 

![Zalecenia](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="d527b-213">Jeśli wszystkie warunki wystąpić w jego trakcie hello operacje takie jak wysokie użycie pamięci przepustowości sieci i obciążenie serwera pamięci podręcznej, zostanie wyświetlony alert na powitania **pamięci podręcznej Redis** bloku.</span><span class="sxs-lookup"><span data-stu-id="d527b-213">If any conditions occur during hello operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on hello **Redis Cache** blade.</span></span>

![Zalecenia](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="d527b-215">Dalsze informacje znajdują się na powitania **zalecenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="d527b-215">Further information can be found on hello **Recommendations** blade.</span></span>

![Zalecenia](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="d527b-217">Można monitorować te metryki na powitania [monitorowania wykresy](cache-how-to-monitor.md#monitoring-charts) i [wykresy użycia](cache-how-to-monitor.md#usage-charts) sekcje hello **pamięci podręcznej Redis** bloku.</span><span class="sxs-lookup"><span data-stu-id="d527b-217">You can monitor these metrics on hello [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of hello **Redis Cache** blade.</span></span>

<span data-ttu-id="d527b-218">Każda warstwa cenowa ma inną limity dla połączeń klienckich, pamięci oraz przepustowości.</span><span class="sxs-lookup"><span data-stu-id="d527b-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="d527b-219">Jeśli pamięć podręczna zbliża się do maksymalnej pojemności dla tych metryk przez dłuższy czas, zostanie utworzony zalecenia.</span><span class="sxs-lookup"><span data-stu-id="d527b-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="d527b-220">Aby uzyskać więcej informacji o hello metryki i limity przeglądane przez hello **zalecenia** narzędzie, zobacz hello w poniższej tabeli:</span><span class="sxs-lookup"><span data-stu-id="d527b-220">For more information about hello metrics and limits reviewed by hello **Recommendations** tool, see hello following table:</span></span>

| <span data-ttu-id="d527b-221">Metryki pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="d527b-221">Redis Cache metric</span></span> | <span data-ttu-id="d527b-222">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="d527b-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="d527b-223">Wykorzystanie przepustowości sieci</span><span class="sxs-lookup"><span data-stu-id="d527b-223">Network bandwidth usage</span></span> |[<span data-ttu-id="d527b-224">Wydajność pamięci podręcznej - dostępną przepustowość</span><span class="sxs-lookup"><span data-stu-id="d527b-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="d527b-225">Podłączeni klienci</span><span class="sxs-lookup"><span data-stu-id="d527b-225">Connected clients</span></span> |[<span data-ttu-id="d527b-226">Domyślna konfiguracja serwera Redis - maxclients</span><span class="sxs-lookup"><span data-stu-id="d527b-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="d527b-227">Obciążenie serwera</span><span class="sxs-lookup"><span data-stu-id="d527b-227">Server load</span></span> |[<span data-ttu-id="d527b-228">Wykresy użycia - obciążenia serwera Redis</span><span class="sxs-lookup"><span data-stu-id="d527b-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="d527b-229">Użycie pamięci</span><span class="sxs-lookup"><span data-stu-id="d527b-229">Memory usage</span></span> |[<span data-ttu-id="d527b-230">Wydajność pamięci podręcznej — rozmiar</span><span class="sxs-lookup"><span data-stu-id="d527b-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="d527b-231">tooupgrade pamięć podręczną, kliknij przycisk **Uaktualnij teraz** hello toochange warstwy cenowej i [skali](#scale) pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-231">tooupgrade your cache, click **Upgrade now** toochange hello pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="d527b-232">Aby uzyskać więcej informacji o wyborze warstwy cenowej, zobacz [jakie oferty pamięć podręczna Redis i rozmiar należy używać?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="d527b-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="d527b-233">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="d527b-233">Scale</span></span>
<span data-ttu-id="d527b-234">Kliknij przycisk **skali** hello tooview lub Zmień warstwę cenową dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-234">Click **Scale** tooview or change hello pricing tier for your cache.</span></span> <span data-ttu-id="d527b-235">Aby uzyskać więcej informacji na temat skalowania, zobacz [jak tooScale Azure pamięci podręcznej Redis](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-235">For more information on scaling, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Warstwa cenowa pamięci podręcznej redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="d527b-237">Rozmiar klastra redis</span><span class="sxs-lookup"><span data-stu-id="d527b-237">Redis Cluster Size</span></span>
<span data-ttu-id="d527b-238">Kliknij przycisk **rozmiar klastra Redis (wersja ZAPOZNAWCZA)** rozmiar klastra hello toochange uruchomionych Premium pamięci podręcznej z włączoną funkcją klastrowania.</span><span class="sxs-lookup"><span data-stu-id="d527b-238">Click **(PREVIEW) Redis Cluster Size** toochange hello cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="d527b-239">Należy pamiętać, że podczas hello Azure Redis Premium usługi pamięć podręczna warstwy zostało zwolnione tooGeneral dostępności, funkcja Redis rozmiar klastra hello jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="d527b-239">Note that while hello Azure Redis Cache Premium tier has been released tooGeneral Availability, hello Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Rozmiar klastra redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="d527b-241">rozmiar klastra hello toochange, za pomocą suwaka hello lub wpisz liczbę z zakresu od 1 do 10 w hello **liczby niezależnych** polu tekstowym i kliknij przycisk **OK** toosave.</span><span class="sxs-lookup"><span data-stu-id="d527b-241">toochange hello cluster size, use hello slider or type a number between 1 and 10 in hello **Shard count** text box and click **OK** toosave.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d527b-242">Klaster redis jest dostępna tylko dla pamięci podręcznej Premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="d527b-243">Aby uzyskać więcej informacji, zobacz [jak tooconfigure klastrowania podręczna Redis Azure Premium](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-243">For more information, see [How tooconfigure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="d527b-244">Trwałość danych redis</span><span class="sxs-lookup"><span data-stu-id="d527b-244">Redis data persistence</span></span>
<span data-ttu-id="d527b-245">Kliknij przycisk **trwałość danych Redis** tooenable, wyłączyć lub konfigurowanie trwałości danych dla pamięci podręcznej premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-245">Click **Redis data persistence** tooenable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="d527b-246">Pamięć podręczna Redis Azure oferuje trwałość Redis przy użyciu [trwałości RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) lub [trwałości AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="d527b-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="d527b-247">Aby uzyskać więcej informacji, zobacz [jak tooconfigure trwałości dla podręczna Redis Azure Premium](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-247">For more information, see [How tooconfigure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="d527b-248">Trwałości danych pamięci podręcznej redis jest dostępna tylko dla pamięci podręcznej Premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="d527b-249">Aktualizacje harmonogramu</span><span class="sxs-lookup"><span data-stu-id="d527b-249">Schedule updates</span></span>
<span data-ttu-id="d527b-250">Witaj **Zaplanuj aktualizacje** bloku umożliwia toodesignate okna obsługi aktualizacji serwera Redis dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-250">hello **Schedule updates** blade allows you toodesignate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d527b-251">okna obsługi Hello stosuje tylko aktualizacje serwera tooRedis i nie tooany Azure aktualizacji lub aktualizacji systemu operacyjnego toohello hello maszyn wirtualnych, obsługujące hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-251">hello maintenance window applies only tooRedis server updates, and not tooany Azure updates or updates toohello operating system of hello VMs that host hello cache.</span></span>
> 
> 

![Aktualizacje harmonogramu](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="d527b-253">Sprawdź dni hello potrzeby toospecify okna konserwacji i określ hello godzina rozpoczęcia okna konserwacji dla każdego dnia i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="d527b-253">toospecify a maintenance window, check hello desired days and specify hello maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="d527b-254">Należy pamiętać, że czas okna obsługi hello jest w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="d527b-254">Note that hello maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d527b-255">Witaj **Zaplanuj aktualizacje** funkcjonalność jest dostępna tylko dla pamięci podręcznej warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-255">hello **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="d527b-256">Aby uzyskać więcej informacji oraz instrukcje, zobacz [administrowanie pamięć podręczna Redis Azure — Zaplanuj aktualizacje](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="d527b-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="d527b-257">Replikacja geograficzna</span><span class="sxs-lookup"><span data-stu-id="d527b-257">Geo-replication</span></span>

<span data-ttu-id="d527b-258">Witaj **— replikacja geograficzna** bloku udostępnia mechanizm do konsolidacji dwa wystąpienia pamięci podręcznej Redis Azure warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-258">hello **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="d527b-259">Jedna pamięć podręczna jest wyznaczony jako hello głównej połączonego pamięci podręcznej i hello innych jako hello dodatkowej połączonego pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-259">One cache is designated as hello primary linked cache, and hello other as hello secondary linked cache.</span></span> <span data-ttu-id="d527b-260">Hello pamięci podręcznej połączonego dodatkowej staje się tylko do odczytu i jest zapisany toohello głównej pamięci podręcznej danych replikowane toohello dodatkowej połączonego pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-260">hello secondary linked cache becomes read-only, and data written toohello primary cache is replicated toohello secondary linked cache.</span></span> <span data-ttu-id="d527b-261">Ta funkcja może być używana tooreplicate pamięci podręcznej w regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d527b-261">This functionality can be used tooreplicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d527b-262">**Replikacja geograficzna** jest dostępna tylko dla pamięci podręcznej warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="d527b-263">Aby uzyskać więcej informacji oraz instrukcje, zobacz [jak tooconfigure — replikacja geograficzna dla pamięci podręcznej Redis Azure](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-263">For more information and instructions, see [How tooconfigure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="d527b-264">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="d527b-264">Virtual Network</span></span>
<span data-ttu-id="d527b-265">Witaj **sieci wirtualnej** sekcja umożliwia ustawień sieci wirtualnej hello tooconfigure dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-265">hello **Virtual Network** section allows you tooconfigure hello virtual network settings for your cache.</span></span> <span data-ttu-id="d527b-266">Informacje na temat tworzenia pamięci podręcznej premium z sieciami Wirtualnymi obsługują i aktualizowanie jej ustawień, zobacz [jak tooconfigure sieci wirtualnej obsługę podręczna Redis Azure Premium](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-266">For information on creating a premium cache with VNET support and updating its settings, see [How tooconfigure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d527b-267">Ustawienia sieci wirtualnej są dostępne tylko dla pamięci podręcznej premium, które zostały skonfigurowane z obsługą sieci Wirtualnej podczas tworzenia pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="d527b-268">Zapora</span><span class="sxs-lookup"><span data-stu-id="d527b-268">Firewall</span></span>

<span data-ttu-id="d527b-269">Kliknij przycisk **zapory** tooview i konfigurowanie reguł zapory dla pamięć podręczna Redis Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-269">Click **Firewall** tooview and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Zapora](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="d527b-271">Początek i koniec zakresu adresów IP można określić reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="d527b-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="d527b-272">Jeśli reguły zapory są skonfigurowane, tylko połączenia klienckie z hello określony, zakresów adresów IP można połączyć toohello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-272">When firewall rules are configured, only client connections from hello specified IP address ranges can connect toohello cache.</span></span> <span data-ttu-id="d527b-273">Po zapisaniu regułę zapory jest krótkie opóźnienie przed obowiązuje zasada hello.</span><span class="sxs-lookup"><span data-stu-id="d527b-273">When a firewall rule is saved there is a short delay before hello rule is effective.</span></span> <span data-ttu-id="d527b-274">To opóźnienie jest zazwyczaj mniej niż minutę.</span><span class="sxs-lookup"><span data-stu-id="d527b-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d527b-275">Połączenia z pamięcią podręczną Redis Azure monitorowania systemów będą zawsze dozwolone, nawet jeśli reguły zapory są skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="d527b-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="d527b-276">Reguły zapory są dostępne tylko dla pamięci podręcznej warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="d527b-277">Właściwości</span><span class="sxs-lookup"><span data-stu-id="d527b-277">Properties</span></span>
<span data-ttu-id="d527b-278">Kliknij przycisk **właściwości** tooview informacji o pamięci podręcznej, łącznie z punktu końcowego pamięci podręcznej hello i portów.</span><span class="sxs-lookup"><span data-stu-id="d527b-278">Click **Properties** tooview information about your cache, including hello cache endpoint and ports.</span></span>

![Właściwości pamięci podręcznej redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="d527b-280">Blokady</span><span class="sxs-lookup"><span data-stu-id="d527b-280">Locks</span></span>
<span data-ttu-id="d527b-281">Witaj **blokuje** sekcja pozwala toolock subskrypcji, grupy zasobów lub tooprevent zasobów innym użytkownikom w organizacji przypadkowo usuwanie i modyfikowanie kluczowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="d527b-281">hello **Locks** section allows you toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="d527b-282">Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="d527b-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="d527b-283">Skrypt automatyzacji</span><span class="sxs-lookup"><span data-stu-id="d527b-283">Automation script</span></span>

<span data-ttu-id="d527b-284">Kliknij przycisk **skryptu automatyzacji** toobuild i eksportowanie szablonu wdrożonych zasobów do przyszłych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="d527b-284">Click **Automation script** toobuild and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="d527b-285">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [wdrożenie zasobów przy użyciu szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="d527b-286">Ustawienia administracji</span><span class="sxs-lookup"><span data-stu-id="d527b-286">Administration settings</span></span>
<span data-ttu-id="d527b-287">Witaj ustawienia w hello **administracji** sekcji pozwalają hello tooperform następujące zadania administracyjne dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-287">hello settings in hello **Administration** section allow you tooperform hello following administrative tasks for your cache.</span></span> 

![Administracja](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="d527b-289">Importowanie danych</span><span class="sxs-lookup"><span data-stu-id="d527b-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="d527b-290">Eksportowanie danych</span><span class="sxs-lookup"><span data-stu-id="d527b-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="d527b-291">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="d527b-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="d527b-292">Import/Export</span><span class="sxs-lookup"><span data-stu-id="d527b-292">Import/Export</span></span>
<span data-ttu-id="d527b-293">Import/Eksport jest operacji zarządzania pamięcią podręczną Redis Azure danych, która umożliwia tooimport i eksportowanie danych w pamięci podręcznej hello przez importowanie i Eksportowanie migawki Redis pamięci podręcznej bazy danych (RDB) z premium pamięci podręcznej tooa stronicowy obiekt blob na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="d527b-293">Import/Export is an Azure Redis Cache data management operation, which allows you tooimport and export data in hello cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache tooa page blob in an Azure Storage Account.</span></span> <span data-ttu-id="d527b-294">Narzędzie importu/eksportu umożliwia toomigrate między różnymi wystąpieniami usługi pamięć podręczna Redis Azure lub wypełnienia pamięci podręcznej hello danych przed użyciem.</span><span class="sxs-lookup"><span data-stu-id="d527b-294">Import/Export enables you toomigrate between different Azure Redis Cache instances or populate hello cache with data before use.</span></span>

<span data-ttu-id="d527b-295">Import może być używane toobring Redis zgodne RDB plików z dowolnego serwera Redis uruchomiona w chmurze lub środowiska, w tym Redis w systemie Linux, Windows albo dowolnego dostawcy chmury, takich jak usług Amazon Web Services i innych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d527b-295">Import can be used toobring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="d527b-296">Importowanie danych jest łatwe toocreate pamięci podręcznej z wstępnie wypełnione danych.</span><span class="sxs-lookup"><span data-stu-id="d527b-296">Importing data is an easy way toocreate a cache with pre-populated data.</span></span> <span data-ttu-id="d527b-297">Podczas procesu importowania hello pamięć podręczna Redis Azure ładuje hello RDB pliki z magazynu Azure do pamięci i wstawia hello klucze do pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="d527b-297">During hello import process, Azure Redis Cache loads hello RDB files from Azure storage into memory, and then inserts hello keys into hello cache.</span></span>

<span data-ttu-id="d527b-298">Eksport umożliwia tooexport hello danych przechowywanych w pamięci podręcznej Redis Azure tooRedis zgodne pliki RDB.</span><span class="sxs-lookup"><span data-stu-id="d527b-298">Export allows you tooexport hello data stored in Azure Redis Cache tooRedis compatible RDB files.</span></span> <span data-ttu-id="d527b-299">Można użyć tych danych toomove funkcji z jednego tooanother wystąpienia pamięci podręcznej Redis Azure lub tooanother serwera Redis.</span><span class="sxs-lookup"><span data-stu-id="d527b-299">You can use this feature toomove data from one Azure Redis Cache instance tooanother or tooanother Redis server.</span></span> <span data-ttu-id="d527b-300">W procesie eksportu hello plik tymczasowy zostanie utworzony na powitania wirtualna hostów hello wystąpienie serwera pamięci podręcznej Redis Azure, czy plik hello jest przekazany toohello wyznaczony konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d527b-300">During hello export process, a temporary file is created on hello VM that hosts hello Azure Redis Cache server instance, and hello file is uploaded toohello designated storage account.</span></span> <span data-ttu-id="d527b-301">Po ukończeniu operacji eksportowania hello ze stanem powodzenie lub niepowodzenie hello plik tymczasowy zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="d527b-301">When hello export operation completes with either a status of success or failure, hello temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d527b-302">Narzędzie importu/eksportu jest dostępna tylko dla pamięci podręcznej warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="d527b-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="d527b-303">Aby uzyskać więcej informacji oraz instrukcje, zobacz [importować i eksportować dane w pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="d527b-304">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="d527b-304">Reboot</span></span>
<span data-ttu-id="d527b-305">Witaj **ponowny rozruch** bloku umożliwia tooreboot hello węzłów pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-305">hello **Reboot** blade allows you tooreboot hello nodes of your cache.</span></span> <span data-ttu-id="d527b-306">Ta możliwość ponownego uruchomienia umożliwia tootest możesz aplikacji zapewnia odporność na awarie w przypadku awarii węzła pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-306">This reboot capability enables you tootest your application for resiliency if there is a failure of a cache node.</span></span>

![Ponowne uruchamianie](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="d527b-308">Jeśli pamięć podręczna premium z włączoną funkcją klastrowania, można wybrać, które odłamków hello tooreboot pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-308">If you have a premium cache with clustering enabled, you can select which shards of hello cache tooreboot.</span></span>

![Ponowne uruchamianie](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="d527b-310">tooreboot co najmniej jeden węzeł z pamięci podręcznej, wybierz węzeł hello potrzebne i kliknij przycisk **ponowny rozruch**.</span><span class="sxs-lookup"><span data-stu-id="d527b-310">tooreboot one or more nodes of your cache, select hello desired nodes and click **Reboot**.</span></span> <span data-ttu-id="d527b-311">Jeśli masz usługi pamięć podręczna premium z włączoną funkcją klastrowania, wybierz hello shard(s) tooreboot, a następnie kliknij przycisk **ponowny rozruch**.</span><span class="sxs-lookup"><span data-stu-id="d527b-311">If you have a premium cache with clustering enabled, select hello shard(s) tooreboot and then click **Reboot**.</span></span> <span data-ttu-id="d527b-312">Po kilku minutach hello ponownego uruchomienia wybranych węzłów i jest znowu w trybie online później za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d527b-312">After a few minutes, hello selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d527b-313">Ponowne uruchomienie jest teraz dostępna dla wszystkich warstw cenowych.</span><span class="sxs-lookup"><span data-stu-id="d527b-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="d527b-314">Aby uzyskać więcej informacji oraz instrukcje, zobacz [administrowanie pamięć podręczna Redis Azure — ponowne uruchomienie](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="d527b-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="d527b-315">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="d527b-315">Monitoring</span></span>

<span data-ttu-id="d527b-316">Witaj **monitorowanie** sekcja pozwala tooconfigure Diagnostyka i monitorowanie dla pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="d527b-316">hello **Monitoring** section allows you tooconfigure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="d527b-317">Aby uzyskać więcej informacji o pamięci podręcznej Redis Azure monitorowania i diagnostyki, zobacz [jak toomonitor Azure pamięci podręcznej Redis](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How toomonitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnostyka](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="d527b-319">Redis metryk</span><span class="sxs-lookup"><span data-stu-id="d527b-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="d527b-320">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="d527b-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="d527b-321">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="d527b-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="d527b-322">Redis metryk</span><span class="sxs-lookup"><span data-stu-id="d527b-322">Redis metrics</span></span>
<span data-ttu-id="d527b-323">Kliknij przycisk **Redis metryki** za[wyświetlić metryki](cache-how-to-monitor.md#view-cache-metrics) dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-323">Click **Redis metrics** too[view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="d527b-324">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="d527b-324">Alert rules</span></span>

<span data-ttu-id="d527b-325">Kliknij przycisk **reguły alertów** tooconfigure alertów w oparciu metryki pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="d527b-325">Click **Alert rules** tooconfigure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="d527b-326">Aby uzyskać więcej informacji, zobacz [alerty](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="d527b-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="d527b-327">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="d527b-327">Diagnostics</span></span>

<span data-ttu-id="d527b-328">Domyślnie są metryki pamięci podręcznej w monitorze Azure [przechowywane przez 30 dni](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) , a następnie usuwany.</span><span class="sxs-lookup"><span data-stu-id="d527b-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="d527b-329">toopersist Twojego metryki pamięci podręcznej przez czas dłuższy niż 30 dni, kliknij przycisk **diagnostyki** za[Konfigurowanie konta magazynu hello](cache-how-to-monitor.md#export-cache-metrics) używane toostore Diagnostyka pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-329">toopersist your cache metrics for longer than 30 days, click **Diagnostics** too[configure hello storage account](cache-how-to-monitor.md#export-cache-metrics) used toostore cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="d527b-330">Dodanie tooarchiving Twojego toostorage metryki pamięci podręcznej, można też [strumienia ich Centrum zdarzeń tooan lub wysyłanie do nich tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="d527b-330">In addition tooarchiving your cache metrics toostorage, you can also [stream them tooan Event hub or send them tooLog Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="d527b-331">Rozwiązywanie problemów z ustawieniami i pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="d527b-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="d527b-332">Witaj ustawienia w hello **pomocy technicznej i rozwiązywania problemów** sekcja zawiera opcje rozwiązywania problemów związanych z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-332">hello settings in hello **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Pomocy technicznej i rozwiązywania problemów](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="d527b-334">Kondycja zasobów</span><span class="sxs-lookup"><span data-stu-id="d527b-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="d527b-335">Nowe żądanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="d527b-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="d527b-336">Kondycja zasobów</span><span class="sxs-lookup"><span data-stu-id="d527b-336">Resource health</span></span>
<span data-ttu-id="d527b-337">**Kondycja zasobów** oczekuje zasobu i informuje, czy działa on zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="d527b-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="d527b-338">Aby uzyskać więcej informacji na temat hello usługi kondycji zasobów Azure, zobacz [Przegląd kondycji zasobów Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-338">For more information about hello Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d527b-339">Kondycja zasobu jest aktualnie w stanie tooreport na powitania kondycji wystąpień pamięci podręcznej Redis Azure hostowanej w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d527b-339">Resource health is currently unable tooreport on hello health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="d527b-340">Aby uzyskać więcej informacji, zobacz [wszystkie funkcje pamięci podręcznej działają odnośnie do hostowania pamięci podręcznej w sieci Wirtualnej?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="d527b-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="d527b-341">Nowe żądanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="d527b-341">New support request</span></span>
<span data-ttu-id="d527b-342">Kliknij przycisk **nowy obsługuje żądania** tooopen żądania pomocy technicznej dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-342">Click **New support request** tooopen a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="d527b-343">Domyślna konfiguracja serwera Redis</span><span class="sxs-lookup"><span data-stu-id="d527b-343">Default Redis server configuration</span></span>
<span data-ttu-id="d527b-344">Nowe wystąpienia pamięci podręcznej Redis Azure są skonfigurowane z hello następujących domyślnych wartości konfiguracji pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="d527b-344">New Azure Redis Cache instances are configured with hello following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="d527b-345">Ustawienia Hello w tej sekcji nie można zmienić za pomocą hello `StackExchange.Redis.IServer.ConfigSet` metody.</span><span class="sxs-lookup"><span data-stu-id="d527b-345">hello settings in this section cannot be changed using hello `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="d527b-346">Jeśli ta metoda jest wywoływana z jednego z poleceń hello w tej sekcji, zostanie zgłoszony następujący wyjątek podobne toohello:</span><span class="sxs-lookup"><span data-stu-id="d527b-346">If this method is called with one of hello commands in this section, an exception similar toohello following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="d527b-347">Wartości, które można skonfigurować, takie jak **Maksymalna pamięć zasady**, można konfigurować za pośrednictwem portalu Azure hello lub narzędzia do zarządzania wiersza polecenia takich jak wiersza polecenia platformy Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d527b-347">Any values that are configurable, such as **max-memory-policy**, are configurable through hello Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="d527b-348">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="d527b-348">Setting</span></span> | <span data-ttu-id="d527b-349">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="d527b-349">Default value</span></span> | <span data-ttu-id="d527b-350">Opis</span><span class="sxs-lookup"><span data-stu-id="d527b-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="d527b-351">16</span><span class="sxs-lookup"><span data-stu-id="d527b-351">16</span></span> |<span data-ttu-id="d527b-352">Witaj domyślną liczbę baz danych jest 16, ale można skonfigurować inny numer hello na podstawie warstwy cenowej. <sup>1</sup> hello domyślna baza danych jest DB 0, możesz wybrać inną na podstawę dla każdego połączenia przy użyciu `connection.GetDatabase(dbid)` gdzie `dbid` jest liczbą z zakresu od `0` i `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="d527b-352">hello default number of databases is 16 but you can configure a different number based on hello pricing tier.<sup>1</sup> hello default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="d527b-353">Zależy od warstwy cenowej hello<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d527b-353">Depends on hello pricing tier<sup>2</sup></span></span> |<span data-ttu-id="d527b-354">Jest to maksymalna liczba podłączonych klientów dozwolone na powitania sam hello czasu.</span><span class="sxs-lookup"><span data-stu-id="d527b-354">This is hello maximum number of connected clients allowed at hello same time.</span></span> <span data-ttu-id="d527b-355">Po osiągnięciu limitu hello Redis zamyka wszystkie hello nowych połączeń, zwróci komunikat "Maksymalna liczba klientów osiągnięto".</span><span class="sxs-lookup"><span data-stu-id="d527b-355">Once hello limit is reached Redis closes all hello new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="d527b-356">Zasady Maxmemory jest ustawienie hello jak Redis wybiera jakie tooremove podczas `maxmemory` osiągnięciu (hello rozmiar pamięci podręcznej hello oferty wybranej podczas tworzenia pamięci podręcznej hello).</span><span class="sxs-lookup"><span data-stu-id="d527b-356">Maxmemory policy is hello setting for how Redis selects what tooremove when `maxmemory` (hello size of hello cache offering you selected when you created hello cache) is reached.</span></span> <span data-ttu-id="d527b-357">Z pamięci podręcznej Redis Azure hello domyślne ustawienie to `volatile-lru`, które powoduje usunięcie kluczy hello z wygaśnięciem ustawić za pomocą algorytmu LRU.</span><span class="sxs-lookup"><span data-stu-id="d527b-357">With Azure Redis Cache hello default setting is `volatile-lru`, which removes hello keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="d527b-358">To ustawienie można skonfigurować w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d527b-358">This setting can be configured in hello Azure portal.</span></span> <span data-ttu-id="d527b-359">Aby uzyskać więcej informacji, zobacz [zasady pamięci](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="d527b-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="d527b-360">3</span><span class="sxs-lookup"><span data-stu-id="d527b-360">3</span></span> |<span data-ttu-id="d527b-361">toosave pamięci, LRU i minimalny czas wygaśnięcia algorytmy są przybliżona algorytmy zamiast dokładne algorytmów.</span><span class="sxs-lookup"><span data-stu-id="d527b-361">toosave memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="d527b-362">Domyślnie Redis kontroli trzy klucze i pobrania hello jedną używany mniej ostatnio.</span><span class="sxs-lookup"><span data-stu-id="d527b-362">By default Redis checks three keys and picks hello one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="d527b-363">5,000</span><span class="sxs-lookup"><span data-stu-id="d527b-363">5,000</span></span> |<span data-ttu-id="d527b-364">Maksymalny czas wykonywania skryptu Lua (w milisekundach).</span><span class="sxs-lookup"><span data-stu-id="d527b-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="d527b-365">Po osiągnięciu maksymalnego czasu wykonywania hello Redis rejestruje skryptu nadal trwa wykonywanie po hello maksymalny dozwolony czas i uruchamia tooreply tooqueries z powodu błędu.</span><span class="sxs-lookup"><span data-stu-id="d527b-365">If hello maximum execution time is reached, Redis logs that a script is still in execution after hello maximum allowed time, and starts tooreply tooqueries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="d527b-366">500</span><span class="sxs-lookup"><span data-stu-id="d527b-366">500</span></span> |<span data-ttu-id="d527b-367">Maksymalny rozmiar kolejki zdarzeń skryptu.</span><span class="sxs-lookup"><span data-stu-id="d527b-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="d527b-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="d527b-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="d527b-369">0 0 mb 032 8mb 60</span><span class="sxs-lookup"><span data-stu-id="d527b-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="d527b-370">Witaj limity buforu wyjściowego klienta mogą być używane rozłączenia tooforce klientów, które nie są odczytywanie danych z serwera hello wystarczająca jakiegoś powodu (typową przyczyną jest, że klient Pub/Sub nie mogą korzystać z wiadomości tak szybko, jak wydawcy hello może utworzyć je).</span><span class="sxs-lookup"><span data-stu-id="d527b-370">hello client output buffer limits can be used tooforce disconnection of clients that are not reading data from hello server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as hello publisher can produce them).</span></span> <span data-ttu-id="d527b-371">Aby uzyskać więcej informacji, zobacz [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="d527b-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="d527b-372"><a name="databases"></a>
<sup>1</sup>hello limit `databases` jest różne dla każdego pamięć podręczna Redis Azure warstwy cenowej i można ustawić na tworzenie pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-372"><a name="databases"></a>
<sup>1</sup>hello limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="d527b-373">Jeśli nie `databases` ustawienie jest określone podczas tworzenia pamięci podręcznej hello domyślna to 16.</span><span class="sxs-lookup"><span data-stu-id="d527b-373">If no `databases` setting is specified during cache creation, hello default is 16.</span></span>

* <span data-ttu-id="d527b-374">Podstawowa i standardowa pamięci podręczne</span><span class="sxs-lookup"><span data-stu-id="d527b-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="d527b-375">C0 (250 MB) pamięci podręcznej - zapasowe too16 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-375">C0 (250 MB) cache - up too16 databases</span></span>
  * <span data-ttu-id="d527b-376">C1 pamięci podręcznej (1 GB) — zapasowe too16 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-376">C1 (1 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="d527b-377">C2 (2,5 GB) pamięci podręcznej - zapasowe too16 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-377">C2 (2.5 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="d527b-378">C3 (6 GB) pamięci podręcznej - zapasowe too16 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-378">C3 (6 GB) cache - up too16 databases</span></span>
  * <span data-ttu-id="d527b-379">C4 (13 GB) pamięci podręcznej - zapasowe too32 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-379">C4 (13 GB) cache - up too32 databases</span></span>
  * <span data-ttu-id="d527b-380">C5 (26 GB) pamięci podręcznej - zapasowe too48 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-380">C5 (26 GB) cache - up too48 databases</span></span>
  * <span data-ttu-id="d527b-381">C6 (53 GB) pamięci podręcznej - zapasowe too64 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-381">C6 (53 GB) cache - up too64 databases</span></span>
* <span data-ttu-id="d527b-382">Pamięci podręczne — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="d527b-382">Premium caches</span></span>
  * <span data-ttu-id="d527b-383">P1 (6 GB — 60 GB) — zapasowe too16 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-383">P1 (6 GB - 60 GB) - up too16 databases</span></span>
  * <span data-ttu-id="d527b-384">P2 (13 GB - 130 GB) — zapasowe too32 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-384">P2 (13 GB - 130 GB) - up too32 databases</span></span>
  * <span data-ttu-id="d527b-385">P3 (26 GB - 260 GB) — zapasowe too48 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-385">P3 (26 GB - 260 GB) - up too48 databases</span></span>
  * <span data-ttu-id="d527b-386">P4 (53 GB - 530 GB) — zapasowe too64 baz danych</span><span class="sxs-lookup"><span data-stu-id="d527b-386">P4 (53 GB - 530 GB) - up too64 databases</span></span>
  * <span data-ttu-id="d527b-387">Wszystkie bufory premium z klastrem Redis enabled - Redis klastra obsługuje tylko tekst hello korzystania z bazy danych 0 `databases` limit dla dowolnego pamięć podręczna premium z klastrem Redis włączone jest 1 i hello [wybierz](http://redis.io/commands/select) polecenia jest niedozwolone.</span><span class="sxs-lookup"><span data-stu-id="d527b-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so hello `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and hello [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="d527b-388">Aby uzyskać więcej informacji, zobacz [należy toomake wszelkie zmiany toomy klienta aplikacji toouse klastra?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="d527b-388">For more information, see [Do I need toomake any changes toomy client application toouse clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="d527b-389">Aby uzyskać więcej informacji na temat baz danych, zobacz [co to są Redis baz danych?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="d527b-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="d527b-390">Witaj `databases` ustawienie może być skonfigurowany tylko podczas tworzenia pamięci podręcznej i tylko przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych klientów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="d527b-390">hello `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="d527b-391">Aby uzyskać przykład konfigurowania `databases` podczas tworzenia pamięci podręcznej przy użyciu programu PowerShell, zobacz [AzureRmRedisCache nowy](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="d527b-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="d527b-392"><a name="maxclients"></a>
<sup>2</sup> `maxclients` jest różne dla każdego pamięć podręczna Redis Azure warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="d527b-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="d527b-393">Podstawowa i standardowa pamięci podręczne</span><span class="sxs-lookup"><span data-stu-id="d527b-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="d527b-394">C0 (250 MB) pamięci podręcznej - too256 połączenia</span><span class="sxs-lookup"><span data-stu-id="d527b-394">C0 (250 MB) cache - up too256 connections</span></span>
  * <span data-ttu-id="d527b-395">C1 pamięci podręcznej (1 GB) — się too1, 000 połączenia</span><span class="sxs-lookup"><span data-stu-id="d527b-395">C1 (1 GB) cache - up too1,000 connections</span></span>
  * <span data-ttu-id="d527b-396">C2 (2,5 GB) pamięci podręcznej - się too2, 000 połączenia</span><span class="sxs-lookup"><span data-stu-id="d527b-396">C2 (2.5 GB) cache - up too2,000 connections</span></span>
  * <span data-ttu-id="d527b-397">C3 (6 GB) pamięci podręcznej - się too5, 000 połączenia</span><span class="sxs-lookup"><span data-stu-id="d527b-397">C3 (6 GB) cache - up too5,000 connections</span></span>
  * <span data-ttu-id="d527b-398">C4 (13 GB) pamięci podręcznej - się too10, 000 połączenia</span><span class="sxs-lookup"><span data-stu-id="d527b-398">C4 (13 GB) cache - up too10,000 connections</span></span>
  * <span data-ttu-id="d527b-399">C5 (26 GB) pamięci podręcznej - się too15, 000 połączenia</span><span class="sxs-lookup"><span data-stu-id="d527b-399">C5 (26 GB) cache - up too15,000 connections</span></span>
  * <span data-ttu-id="d527b-400">C6 (53 GB) pamięci podręcznej - się too20, 000 połączenia</span><span class="sxs-lookup"><span data-stu-id="d527b-400">C6 (53 GB) cache - up too20,000 connections</span></span>
* <span data-ttu-id="d527b-401">Pamięci podręczne — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="d527b-401">Premium caches</span></span>
  * <span data-ttu-id="d527b-402">P1 (6 GB — 60 GB) — się too7, połączenia o szybkości 500</span><span class="sxs-lookup"><span data-stu-id="d527b-402">P1 (6 GB - 60 GB) - up too7,500 connections</span></span>
  * <span data-ttu-id="d527b-403">P2 (13 GB - 130 GB) — się too15, 000 połączeń</span><span class="sxs-lookup"><span data-stu-id="d527b-403">P2 (13 GB - 130 GB) - up too15,000 connections</span></span>
  * <span data-ttu-id="d527b-404">P3 (26 GB - 260 GB) — się too30, 000 połączeń</span><span class="sxs-lookup"><span data-stu-id="d527b-404">P3 (26 GB - 260 GB) - up too30,000 connections</span></span>
  * <span data-ttu-id="d527b-405">P4 (53 GB - 530 GB) — się too40, 000 połączeń</span><span class="sxs-lookup"><span data-stu-id="d527b-405">P4 (53 GB - 530 GB) - up too40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="d527b-406">Podczas każdego rozmiaru pamięci podręcznej umożliwia *do* określonej liczby połączeń, każdy tooRedis połączenia obciążenie ma skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="d527b-406">While each size of cache allows *up to* a certain number of connections, each connection tooRedis has overhead associated with it.</span></span> <span data-ttu-id="d527b-407">Przykładem takich obciążenie będzie użycia Procesora i pamięci w wyniku szyfrowania TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="d527b-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="d527b-408">Hello limit maksymalnej liczby połączeń dla rozmiaru pamięci podręcznej danego zakłada lekkim załadować pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-408">hello maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="d527b-409">Czy ładowanie z połączenia koszty *plus* obciążenia z operacjami klienta przekracza pojemność systemu hello, hello pamięci podręcznej można doświadczyć problemów dotyczących pojemności, nawet jeśli nie przekroczono limit połączenia hello hello bieżący rozmiar pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-409">If load from connection overhead *plus* load from client operations exceeds capacity for hello system, hello cache can experience capacity issues even if you have not exceeded hello connection limit for hello current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="d527b-410">Redis polecenia nie są obsługiwane w pamięci podręcznej Redis Azure</span><span class="sxs-lookup"><span data-stu-id="d527b-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d527b-411">Ponieważ konfiguracji i zarządzania wystąpienia pamięci podręcznej Redis Azure jest zarządzany przez firmę Microsoft, hello poniższe polecenia są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="d527b-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, hello following commands are disabled.</span></span> <span data-ttu-id="d527b-412">Jeśli spróbujesz tooinvoke ich zbyt otrzymasz komunikat o błędzie podobny`"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="d527b-412">If you try tooinvoke them, you receive an error message similar too`"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="d527b-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="d527b-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="d527b-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="d527b-414">BGSAVE</span></span>
> * <span data-ttu-id="d527b-415">KONFIGURACJI</span><span class="sxs-lookup"><span data-stu-id="d527b-415">CONFIG</span></span>
> * <span data-ttu-id="d527b-416">DEBUGOWANIA</span><span class="sxs-lookup"><span data-stu-id="d527b-416">DEBUG</span></span>
> * <span data-ttu-id="d527b-417">MIGRACJA</span><span class="sxs-lookup"><span data-stu-id="d527b-417">MIGRATE</span></span>
> * <span data-ttu-id="d527b-418">ZAPISZ</span><span class="sxs-lookup"><span data-stu-id="d527b-418">SAVE</span></span>
> * <span data-ttu-id="d527b-419">ZAMKNIĘCIE</span><span class="sxs-lookup"><span data-stu-id="d527b-419">SHUTDOWN</span></span>
> * <span data-ttu-id="d527b-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="d527b-420">SLAVEOF</span></span>
> * <span data-ttu-id="d527b-421">KLASTER - klaster zapisu, które polecenia są wyłączone, ale tylko do odczytu klastra polecenia są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="d527b-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="d527b-422">Aby uzyskać więcej informacji o poleceniach Redis, zobacz [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="d527b-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="d527b-423">Redis konsoli</span><span class="sxs-lookup"><span data-stu-id="d527b-423">Redis console</span></span>
<span data-ttu-id="d527b-424">Można bezpiecznie wysyłać polecenia tooyour wystąpienia pamięci podręcznej Redis Azure za pomocą hello **Redis konsoli**, która jest dostępna w hello portalu Azure dla wszystkich warstw pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-424">You can securely issue commands tooyour Azure Redis Cache instances using hello **Redis Console**, which is available in hello Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="d527b-425">Witaj konsoli Redis nie działa z [sieci Wirtualnej](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-425">hello Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="d527b-426">Jeśli pamięć podręczna jest częścią sieci Wirtualnej, tylko klienci w sieci Wirtualnej hello można uzyskać dostępu do pamięci podręcznej hello.</span><span class="sxs-lookup"><span data-stu-id="d527b-426">When your cache is part of a VNET, only clients in hello VNET can access hello cache.</span></span> <span data-ttu-id="d527b-427">Ponieważ Redis konsola jest uruchamiana w przeglądarce lokalnego znajduje się poza hello sieci Wirtualnej, nie można połączyć z pamięci podręcznej tooyour.</span><span class="sxs-lookup"><span data-stu-id="d527b-427">Because Redis Console runs in your local browser, which is outside hello VNET, it can't connect tooyour cache.</span></span>
> - <span data-ttu-id="d527b-428">Nie wszystkie polecenia Redis są obsługiwane w pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="d527b-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="d527b-429">Listę poleceń pamięci podręcznej Redis, które są wyłączone dla pamięci podręcznej Redis Azure, zobacz hello poprzedniej [polecenia nie są obsługiwane w pamięci podręcznej Redis Azure Redis](#redis-commands-not-supported-in-azure-redis-cache) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d527b-429">For a list of Redis commands that are disabled for Azure Redis Cache, see hello previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="d527b-430">Aby uzyskać więcej informacji o poleceniach Redis, zobacz [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="d527b-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="d527b-431">Witaj tooaccess Redis konsoli, kliknij przycisk **konsoli** z hello **pamięci podręcznej Redis** bloku.</span><span class="sxs-lookup"><span data-stu-id="d527b-431">tooaccess hello Redis Console, click **Console** from hello **Redis Cache** blade.</span></span>

![Redis konsoli](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="d527b-433">tooissue polecenia dla wystąpienia pamięci podręcznej, po prostu typu hello żądanego polecenia do konsoli hello.</span><span class="sxs-lookup"><span data-stu-id="d527b-433">tooissue commands against your cache instance, simply type hello desired command into hello console.</span></span>

![Redis konsoli](./media/cache-configure/redis-console.png)


### <a name="using-hello-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="d527b-435">Przy użyciu hello Redis konsoli z premium w klastrze pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="d527b-435">Using hello Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="d527b-436">Przy użyciu hello Redis konsoli premium pamięć podręczna klastra można wydać polecenia tooa jednego niezależnego fragmentu hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="d527b-436">When using hello Redis Console with a premium clustered cache, you can issue commands tooa single shard of hello cache.</span></span> <span data-ttu-id="d527b-437">tooissue niezależnych określonych tooa polecenia, najpierw połączyć toohello żądany identyfikator niezależnego fragmentu, klikając hello niezależnego fragmentu selektora.</span><span class="sxs-lookup"><span data-stu-id="d527b-437">tooissue a command tooa specific shard, first connect toohello desired shard by clicking it on hello shard picker.</span></span>

![Redis konsoli](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="d527b-439">Przy próbie tooaccess klucz, który znajduje się w różnych niezależnego fragmentu niż hello niezależnych połączonych otrzymujesz błąd komunikat podobny toohello następującą wiadomości.</span><span class="sxs-lookup"><span data-stu-id="d527b-439">If you attempt tooaccess a key that is stored in a different shard than hello connected shard, you receive an error message similar toohello following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="d527b-440">W poprzednim przykładzie hello niezależnego fragmentu 1 jest wybrany niezależnego fragmentu hello, ale `myKey` znajduje się w niezależnych 0, wskazywany przez hello `(shard 0)` część komunikatu o błędzie hello.</span><span class="sxs-lookup"><span data-stu-id="d527b-440">In hello previous example, shard 1 is hello selected shard, but `myKey` is located in shard 0, as indicated by hello `(shard 0)` portion of hello error message.</span></span> <span data-ttu-id="d527b-441">W tym przykładzie tooaccess `myKey`, wybierz za pomocą niezależnego fragmentu 0 hello selektora niezależnego fragmentu, a następnie polecenie hello potrzeby problem.</span><span class="sxs-lookup"><span data-stu-id="d527b-441">In this example, tooaccess `myKey`, select shard 0 using hello shard picker, and then issue hello desired command.</span></span>


## <a name="move-your-cache-tooa-new-subscription"></a><span data-ttu-id="d527b-442">Przenieś nowej subskrypcji tooa pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="d527b-442">Move your cache tooa new subscription</span></span>
<span data-ttu-id="d527b-443">Przenieś z nowej subskrypcji tooa pamięci podręcznej, klikając **Przenieś**.</span><span class="sxs-lookup"><span data-stu-id="d527b-443">You can move your cache tooa new subscription by clicking **Move**.</span></span>

![Przenieś pamięci podręcznej Redis](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="d527b-445">Aby uzyskać informacje na temat przenoszenia zasobów z jednego zasobu grupy tooanother i tooanother jedną subskrypcję, zobacz [przenieść grupy zasobów toonew zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="d527b-445">For information on moving resources from one resource group tooanother, and from one subscription tooanother, see [Move resources toonew resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d527b-446">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d527b-446">Next steps</span></span>
* <span data-ttu-id="d527b-447">Aby uzyskać więcej informacji na temat pracy z pamięci podręcznej Redis poleceń, zobacz [jak uruchomić polecenia Redis?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="d527b-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

