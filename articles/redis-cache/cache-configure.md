---
title: "Konfigurowanie pamięci podręcznej Redis Azure | Dokumentacja firmy Microsoft"
description: "Omówienie domyślną konfigurację pamięci podręcznej Redis w pamięci podręcznej Redis Azure i Dowiedz się, jak skonfigurować swoich wystąpień w pamięci podręcznej Redis Azure"
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
ms.openlocfilehash: 0274e58eb2e83202d4dbc58da0c67d0fdde22ede
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-azure-redis-cache"></a><span data-ttu-id="c0d56-103">Konfigurowanie pamięci podręcznej Redis Azure</span><span class="sxs-lookup"><span data-stu-id="c0d56-103">How to configure Azure Redis Cache</span></span>
<span data-ttu-id="c0d56-104">W tym temacie opisano sposób przejrzeć i zaktualizować konfigurację dla swoich wystąpień w pamięci podręcznej Redis Azure i zawiera domyślną konfigurację serwera Redis wystąpienia pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d56-104">This topic describes how to review and update the configuration for your Azure Redis Cache instances, and covers the default Redis server configuration for Azure Redis Cache instances.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d56-105">Aby uzyskać więcej informacji na temat konfigurowania przy użyciu funkcji pamięci podręcznej premium, zobacz [Konfigurowanie trwałości](cache-how-to-premium-persistence.md), [sposobu konfigurowania klastra](cache-how-to-premium-clustering.md), i [Konfigurowanie obsługi sieci wirtualnej ](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-105">For more information on configuring and using premium cache features, see [How to configure persistence](cache-how-to-premium-persistence.md), [How to configure clustering](cache-how-to-premium-clustering.md), and [How to configure Virtual Network support](cache-how-to-premium-vnet.md).</span></span>
> 
> 

## <a name="configure-redis-cache-settings"></a><span data-ttu-id="c0d56-106">Skonfiguruj ustawienia pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-106">Configure Redis cache settings</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="c0d56-107">Ustawienia pamięci podręcznej Redis Azure są wyświetlane i skonfigurowane na **pamięci podręcznej Redis** za pomocą bloku **zasobów Menu**.</span><span class="sxs-lookup"><span data-stu-id="c0d56-107">Azure Redis Cache settings are viewed and configured on the **Redis Cache** blade using the **Resource Menu**.</span></span>

![Ustawienia pamięci podręcznej redis](./media/cache-configure/redis-cache-settings.png)

<span data-ttu-id="c0d56-109">Możesz wyświetlić i skonfigurować następujące ustawienia za pomocą **zasobów Menu**.</span><span class="sxs-lookup"><span data-stu-id="c0d56-109">You can view and configure the following settings using the **Resource Menu**.</span></span>

* [<span data-ttu-id="c0d56-110">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c0d56-110">Overview</span></span>](#overview)
* [<span data-ttu-id="c0d56-111">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="c0d56-111">Activity log</span></span>](#activity-log)
* [<span data-ttu-id="c0d56-112">Kontrola dostępu (IAM)</span><span class="sxs-lookup"><span data-stu-id="c0d56-112">Access control (IAM)</span></span>](#access-control-iam)
* [<span data-ttu-id="c0d56-113">Tagi</span><span class="sxs-lookup"><span data-stu-id="c0d56-113">Tags</span></span>](#tags)
* [<span data-ttu-id="c0d56-114">Diagnozowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="c0d56-114">Diagnose and solve problems</span></span>](#diagnose-and-solve-problems)
* [<span data-ttu-id="c0d56-115">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="c0d56-115">Settings</span></span>](#settings)
    * [<span data-ttu-id="c0d56-116">Klawisze dostępu</span><span class="sxs-lookup"><span data-stu-id="c0d56-116">Access keys</span></span>](#access-keys)
    * [<span data-ttu-id="c0d56-117">Ustawienia zaawansowane</span><span class="sxs-lookup"><span data-stu-id="c0d56-117">Advanced settings</span></span>](#advanced-settings)
    * [<span data-ttu-id="c0d56-118">Klasyfikator pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-118">Redis Cache Advisor</span></span>](#redis-cache-advisor)
    * [<span data-ttu-id="c0d56-119">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="c0d56-119">Scale</span></span>](#scale)
    * [<span data-ttu-id="c0d56-120">Rozmiar klastra redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-120">Redis cluster size</span></span>](#cluster-size)
    * [<span data-ttu-id="c0d56-121">Trwałość danych redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-121">Redis data persistence</span></span>](#redis-data-persistence)
    * [<span data-ttu-id="c0d56-122">Aktualizacje harmonogramu</span><span class="sxs-lookup"><span data-stu-id="c0d56-122">Schedule updates</span></span>](#schedule-updates)
    * <span data-ttu-id="c0d56-123">[Geo-replication](#geo-replication) (Replikacja geograficzna)</span><span class="sxs-lookup"><span data-stu-id="c0d56-123">[Geo-replication](#geo-replication)</span></span>
    * [<span data-ttu-id="c0d56-124">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="c0d56-124">Virtual Network</span></span>](#virtual-network)
    * [<span data-ttu-id="c0d56-125">Zapora</span><span class="sxs-lookup"><span data-stu-id="c0d56-125">Firewall</span></span>](#firewall)
    * [<span data-ttu-id="c0d56-126">Właściwości</span><span class="sxs-lookup"><span data-stu-id="c0d56-126">Properties</span></span>](#properties)
    * [<span data-ttu-id="c0d56-127">Blokady</span><span class="sxs-lookup"><span data-stu-id="c0d56-127">Locks</span></span>](#locks)
    * [<span data-ttu-id="c0d56-128">Skrypt automatyzacji</span><span class="sxs-lookup"><span data-stu-id="c0d56-128">Automation script</span></span>](#automation-script)
* [<span data-ttu-id="c0d56-129">Administracja</span><span class="sxs-lookup"><span data-stu-id="c0d56-129">Administration</span></span>](#administration)
    * [<span data-ttu-id="c0d56-130">Importowanie danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-130">Import data</span></span>](#importexport)
    * [<span data-ttu-id="c0d56-131">Eksportowanie danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-131">Export data</span></span>](#importexport)
    * [<span data-ttu-id="c0d56-132">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="c0d56-132">Reboot</span></span>](#reboot)
* [<span data-ttu-id="c0d56-133">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="c0d56-133">Monitoring</span></span>](#monitoring)
    * [<span data-ttu-id="c0d56-134">Redis metryk</span><span class="sxs-lookup"><span data-stu-id="c0d56-134">Redis metrics</span></span>](#redis-metrics)
    * [<span data-ttu-id="c0d56-135">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="c0d56-135">Alert rules</span></span>](#alert-rules)
    * [<span data-ttu-id="c0d56-136">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="c0d56-136">Diagnostics</span></span>](#diagnostics)
* [<span data-ttu-id="c0d56-137">Rozwiązywanie problemów z ustawieniami i pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="c0d56-137">Support & troubleshooting settings</span></span>](#support-amp-troubleshooting-settings)
    * [<span data-ttu-id="c0d56-138">Kondycja zasobów</span><span class="sxs-lookup"><span data-stu-id="c0d56-138">Resource health</span></span>](#resource-health)
    * [<span data-ttu-id="c0d56-139">Nowe żądanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="c0d56-139">New support request</span></span>](#new-support-request)


## <a name="overview"></a><span data-ttu-id="c0d56-140">Omówienie</span><span class="sxs-lookup"><span data-stu-id="c0d56-140">Overview</span></span>

<span data-ttu-id="c0d56-141">**Omówienie** zapewnia możesz podstawowych informacji o pamięci podręcznej, takie jak nazwa, porty, warstwa cenowa i metryki wybranego pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-141">**Overview** provides you with basic information about your cache, such as name, ports, pricing tier, and selected cache metrics.</span></span>

### <a name="activity-log"></a><span data-ttu-id="c0d56-142">Dziennik aktywności</span><span class="sxs-lookup"><span data-stu-id="c0d56-142">Activity log</span></span>

<span data-ttu-id="c0d56-143">Kliknij przycisk **dziennik aktywności** Aby wyświetlić akcje wykonywane w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-143">Click **Activity log** to view actions performed on your cache.</span></span> <span data-ttu-id="c0d56-144">Aby rozszerzyć ten widok ma zawierać inne zasoby, możesz również użyć filtrowania.</span><span class="sxs-lookup"><span data-stu-id="c0d56-144">You can also use filtering to expand this view to include other resources.</span></span> <span data-ttu-id="c0d56-145">Aby uzyskać więcej informacji na temat pracy z dziennikami inspekcji, zobacz [inspekcji operacji za pomocą Menedżera zasobów](../azure-resource-manager/resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-145">For more information on working with audit logs, see [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md).</span></span> <span data-ttu-id="c0d56-146">Aby uzyskać więcej informacji dotyczących monitorowania zdarzeń pamięć podręczna Redis Azure, zobacz [operacji i alerty](cache-how-to-monitor.md#operations-and-alerts).</span><span class="sxs-lookup"><span data-stu-id="c0d56-146">For more information on monitoring Azure Redis Cache events, see [Operations and alerts](cache-how-to-monitor.md#operations-and-alerts).</span></span>

### <a name="access-control-iam"></a><span data-ttu-id="c0d56-147">Kontrola dostępu (IAM)</span><span class="sxs-lookup"><span data-stu-id="c0d56-147">Access control (IAM)</span></span>

<span data-ttu-id="c0d56-148">**(IAM) kontroli dostępu** sekcji zapewnia obsługę kontroli dostępu opartej na rolach (RBAC) w portalu Azure, aby ułatwić organizacjom, które spełnia ich wymagania dotyczące zarządzania dostępu, wystarczy i dokładnie.</span><span class="sxs-lookup"><span data-stu-id="c0d56-148">The **Access control (IAM)** section provides support for role-based access control (RBAC) in the Azure portal to help organizations meet their access management requirements simply and precisely.</span></span> <span data-ttu-id="c0d56-149">Aby uzyskać więcej informacji, zobacz [kontroli dostępu opartej na rolach w portalu Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-149">For more information, see [Role-based access control in the Azure portal](../active-directory/role-based-access-control-configure.md).</span></span>

### <a name="tags"></a><span data-ttu-id="c0d56-150">Tagi</span><span class="sxs-lookup"><span data-stu-id="c0d56-150">Tags</span></span>

<span data-ttu-id="c0d56-151">**Tagi** sekcji pomaga organizować zasobów.</span><span class="sxs-lookup"><span data-stu-id="c0d56-151">The **Tags** section helps you organize your resources.</span></span> <span data-ttu-id="c0d56-152">Aby uzyskać więcej informacji, zobacz [organizowania zasobów na platformie Azure przy użyciu tagów](../azure-resource-manager/resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-152">For more information, see [Using tags to organize your Azure resources](../azure-resource-manager/resource-group-using-tags.md).</span></span>


### <a name="diagnose-and-solve-problems"></a><span data-ttu-id="c0d56-153">Diagnozowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="c0d56-153">Diagnose and solve problems</span></span>

<span data-ttu-id="c0d56-154">Kliknij przycisk **diagnozowanie i rozwiązywanie problemów** dostarczanych z najczęściej występujących problemów i strategii w celu ich rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="c0d56-154">Click **Diagnose and solve problems** to be provided with common issues and strategies for resolving them.</span></span>



## <a name="settings"></a><span data-ttu-id="c0d56-155">Ustawienia</span><span class="sxs-lookup"><span data-stu-id="c0d56-155">Settings</span></span>
<span data-ttu-id="c0d56-156">**Ustawienia** sekcja umożliwia dostęp i skonfiguruj następujące ustawienia dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-156">The **Settings** section allows you to access and configure the following settings for your cache.</span></span>

* [<span data-ttu-id="c0d56-157">Klawisze dostępu</span><span class="sxs-lookup"><span data-stu-id="c0d56-157">Access keys</span></span>](#access-keys)
* [<span data-ttu-id="c0d56-158">Ustawienia zaawansowane</span><span class="sxs-lookup"><span data-stu-id="c0d56-158">Advanced settings</span></span>](#advanced-settings)
* [<span data-ttu-id="c0d56-159">Klasyfikator pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-159">Redis Cache Advisor</span></span>](#redis-cache-advisor)
* [<span data-ttu-id="c0d56-160">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="c0d56-160">Scale</span></span>](#scale)
* [<span data-ttu-id="c0d56-161">Rozmiar klastra redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-161">Redis cluster size</span></span>](#cluster-size)
* [<span data-ttu-id="c0d56-162">Trwałość danych redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-162">Redis data persistence</span></span>](#redis-data-persistence)
* [<span data-ttu-id="c0d56-163">Aktualizacje harmonogramu</span><span class="sxs-lookup"><span data-stu-id="c0d56-163">Schedule updates</span></span>](#schedule-updates)
* <span data-ttu-id="c0d56-164">[Geo-replication](#geo-replication) (Replikacja geograficzna)</span><span class="sxs-lookup"><span data-stu-id="c0d56-164">[Geo-replication](#geo-replication)</span></span>
* [<span data-ttu-id="c0d56-165">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="c0d56-165">Virtual Network</span></span>](#virtual-network)
* [<span data-ttu-id="c0d56-166">Zapora</span><span class="sxs-lookup"><span data-stu-id="c0d56-166">Firewall</span></span>](#firewall)
* [<span data-ttu-id="c0d56-167">Właściwości</span><span class="sxs-lookup"><span data-stu-id="c0d56-167">Properties</span></span>](#properties)
* [<span data-ttu-id="c0d56-168">Blokady</span><span class="sxs-lookup"><span data-stu-id="c0d56-168">Locks</span></span>](#locks)
* [<span data-ttu-id="c0d56-169">Skrypt automatyzacji</span><span class="sxs-lookup"><span data-stu-id="c0d56-169">Automation script</span></span>](#automation-script)



### <a name="access-keys"></a><span data-ttu-id="c0d56-170">Klawisze dostępu</span><span class="sxs-lookup"><span data-stu-id="c0d56-170">Access keys</span></span>
<span data-ttu-id="c0d56-171">Kliknij przycisk **klucze dostępu** do wyświetlania lub ponownie wygenerować klucze dostępu pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-171">Click **Access keys** to view or regenerate the access keys for your cache.</span></span> <span data-ttu-id="c0d56-172">Klucze te są używane przez klientów nawiązywania połączenia z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-172">These keys are used by the clients connecting to your cache.</span></span>

![Klucze dostępu pamięci podręcznej redis](./media/cache-configure/redis-cache-manage-keys.png)

### <a name="advanced-settings"></a><span data-ttu-id="c0d56-174">Ustawienia zaawansowane</span><span class="sxs-lookup"><span data-stu-id="c0d56-174">Advanced settings</span></span>
<span data-ttu-id="c0d56-175">Następujące ustawienia są konfigurowane na **Zaawansowane ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="c0d56-175">The following settings are configured on the **Advanced settings** blade.</span></span>

* [<span data-ttu-id="c0d56-176">Porty dostępu</span><span class="sxs-lookup"><span data-stu-id="c0d56-176">Access Ports</span></span>](#access-ports)
* [<span data-ttu-id="c0d56-177">Zasady pamięci</span><span class="sxs-lookup"><span data-stu-id="c0d56-177">Memory policies</span></span>](#memory-policies)
* [<span data-ttu-id="c0d56-178">Powiadomienia przestrzeni kluczy (ustawienia zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="c0d56-178">Keyspace notifications (advanced settings)</span></span>](#keyspace-notifications-advanced-settings)

#### <a name="access-ports"></a><span data-ttu-id="c0d56-179">Porty dostępu</span><span class="sxs-lookup"><span data-stu-id="c0d56-179">Access Ports</span></span>
<span data-ttu-id="c0d56-180">Domyślnie dostęp inny niż za pomocą protokołu SSL jest zablokowany dla nowych pamięci podręcznych.</span><span class="sxs-lookup"><span data-stu-id="c0d56-180">By default, non-SSL access is disabled for new caches.</span></span> <span data-ttu-id="c0d56-181">Aby włączyć port bez protokołu SSL, kliknij przycisk **nr** dla **zezwolić na dostęp tylko za pośrednictwem protokołu SSL** na **Zaawansowane ustawienia** bloku, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="c0d56-181">To enable the non-SSL port, click **No** for **Allow access only via SSL** on the **Advanced settings** blade and then click **Save**.</span></span>

![Porty dostępu pamięci podręcznej redis](./media/cache-configure/redis-cache-access-ports.png)

<a name="maxmemory-policy-and-maxmemory-reserved"></a>
#### <a name="memory-policies"></a><span data-ttu-id="c0d56-183">Zasady pamięci</span><span class="sxs-lookup"><span data-stu-id="c0d56-183">Memory policies</span></span>
<span data-ttu-id="c0d56-184">**Zasad Maxmemory**, **zastrzeżone maxmemory**, i **zastrzeżone maxfragmentationmemory** ustawień na **Zaawansowane ustawienia** Blok skonfigurować zasady pamięci dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-184">The **Maxmemory policy**, **maxmemory-reserved**, and **maxfragmentationmemory-reserved** settings on the **Advanced settings** blade configure the memory policies for the cache.</span></span>

![Zasady Maxmemory pamięci podręcznej redis](./media/cache-configure/redis-cache-maxmemory-policy.png)

<span data-ttu-id="c0d56-186">**Zasady Maxmemory** konfiguruje zasady wykluczania dla pamięci podręcznej i można wybrać z następujących zasad wykluczenia:</span><span class="sxs-lookup"><span data-stu-id="c0d56-186">**Maxmemory policy** configures the eviction policy for the cache and allows you to choose from the following eviction policies:</span></span>

* <span data-ttu-id="c0d56-187">`volatile-lru`— jest to wartość domyślna.</span><span class="sxs-lookup"><span data-stu-id="c0d56-187">`volatile-lru` - this is the default.</span></span>
* `allkeys-lru`
* `volatile-random`
* `allkeys-random`
* `volatile-ttl`
* `noeviction`

<span data-ttu-id="c0d56-188">Aby uzyskać więcej informacji na temat `maxmemory` zasad, zobacz [zasady wykluczania](http://redis.io/topics/lru-cache#eviction-policies).</span><span class="sxs-lookup"><span data-stu-id="c0d56-188">For more information about `maxmemory` policies, see [Eviction policies](http://redis.io/topics/lru-cache#eviction-policies).</span></span>

<span data-ttu-id="c0d56-189">**Zastrzeżone maxmemory** ustawienie określa ilość pamięci w Megabajtach, które jest zastrzeżone dla operacji-cache, takich jak replikacji w trybie failover.</span><span class="sxs-lookup"><span data-stu-id="c0d56-189">The **maxmemory-reserved** setting configures the amount of memory in MB that is reserved for non-cache operations such as replication during failover.</span></span> <span data-ttu-id="c0d56-190">Ustawienie tej wartości pozwala na lepsze środowisko serwera Redis, gdy zmienia się obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c0d56-190">Setting this value allows you to have a more consistent Redis server experience when your load varies.</span></span> <span data-ttu-id="c0d56-191">Ta wartość musi być ustawiona wyższych obciążeń, które są zapisu ciężki.</span><span class="sxs-lookup"><span data-stu-id="c0d56-191">This value should be set higher for workloads that are write heavy.</span></span> <span data-ttu-id="c0d56-192">Pamięć jest zarezerwowana dla takich operacji, jest niedostępna dla magazynu danych z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-192">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="c0d56-193">**Zastrzeżone maxfragmentationmemory** ustawienie określa ilość pamięci w Megabajtach, aby pomieścić fragmentacji pamięci zarezerwowanej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-193">The **maxfragmentationmemory-reserved** setting configures the amount of memory in MB that is reserved to accommodate for memory fragmentation.</span></span> <span data-ttu-id="c0d56-194">Ustawienie tej wartości umożliwia bardziej spójny serwer Redis wystąpić przy pamięci podręcznej jest pełny lub bliski pełnej i fragmentacji stosunek również jest wysoka.</span><span class="sxs-lookup"><span data-stu-id="c0d56-194">Setting this value allows you to have a more consistent Redis server experience when the cache is full or close to full and the fragmentation ratio is also high.</span></span> <span data-ttu-id="c0d56-195">Pamięć jest zarezerwowana dla takich operacji, jest niedostępna dla magazynu danych z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-195">When memory is reserved for such operations, it is unavailable for storage of cached data.</span></span>

<span data-ttu-id="c0d56-196">Rzecz wziąć pod uwagę podczas wybierania nową wartość rezerwacji pamięci (**zastrzeżone maxmemory** lub **zastrzeżone maxfragmentationmemory**) jest jak tej zmiany mogą wpłynąć na pamięci podręcznej, który jest już uruchomione z duże ilości danych.</span><span class="sxs-lookup"><span data-stu-id="c0d56-196">One thing to consider when choosing a new memory reservation value (**maxmemory-reserved** or **maxfragmentationmemory-reserved**) is how this change might affect a cache that is already running with large amounts of data in it.</span></span> <span data-ttu-id="c0d56-197">Na przykład jeśli masz 53 GB pamięci podręcznej z 49 GB danych, a następnie zmień wartość rezerwacji na 8 GB, to spowoduje porzucenie maksymalną ilość dostępnej pamięci systemu do 45 GB.</span><span class="sxs-lookup"><span data-stu-id="c0d56-197">For instance, if you have a 53 GB cache with 49 GB of data, then change the reservation value to 8 GB, this will drop the max available memory for the system down to 45 GB.</span></span> <span data-ttu-id="c0d56-198">Jeśli bieżące `used_memory` lub `used_memory_rss` wartości są większe od nowego limitu 45 GB, a następnie system, należy wykluczyć danych przed zakończeniem `used_memory` i `used_memory_rss` są poniżej 45 GB.</span><span class="sxs-lookup"><span data-stu-id="c0d56-198">If either your current `used_memory` or your `used_memory_rss` values are higher than the new limit of 45 GB, then the system will have to evict data until both `used_memory` and `used_memory_rss` are below 45 GB.</span></span> <span data-ttu-id="c0d56-199">Wykluczanie może zwiększyć fragmentacji pamięci i obciążenia serwera.</span><span class="sxs-lookup"><span data-stu-id="c0d56-199">Eviction can increase server load and memory fragmentation.</span></span> <span data-ttu-id="c0d56-200">Aby uzyskać więcej informacji w pamięci podręcznej metryk, takich jak `used_memory` i `used_memory_rss`, zobacz [dostępne metryki i raportowania interwałów](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span><span class="sxs-lookup"><span data-stu-id="c0d56-200">For more information on cache metrics such as `used_memory` and `used_memory_rss`, see [Available metrics and reporting intervals](cache-how-to-monitor.md#available-metrics-and-reporting-intervals).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0d56-201">**Zastrzeżone maxmemory** i **zastrzeżone maxfragmentationmemory** ustawienia są dostępne tylko dla Standard i Premium przechowuje w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-201">The **maxmemory-reserved** and **maxfragmentationmemory-reserved** settings are only available for Standard and Premium caches.</span></span>
> 
> 

#### <a name="keyspace-notifications-advanced-settings"></a><span data-ttu-id="c0d56-202">Powiadomienia przestrzeni kluczy (ustawienia zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="c0d56-202">Keyspace notifications (advanced settings)</span></span>
<span data-ttu-id="c0d56-203">Powiadomienia są skonfigurowane na przestrzeni kluczy redis **Zaawansowane ustawienia** bloku.</span><span class="sxs-lookup"><span data-stu-id="c0d56-203">Redis keyspace notifications are configured on the **Advanced settings** blade.</span></span> <span data-ttu-id="c0d56-204">Powiadomienia przestrzeni kluczy pozwalają klientom odbierać powiadomienia w przypadku wystąpienia określonych zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c0d56-204">Keyspace notifications allow clients to receive notifications when certain events occur.</span></span>

![Zaawansowane ustawienia pamięci podręcznej redis](./media/cache-configure/redis-cache-advanced-settings.png)

> [!IMPORTANT]
> <span data-ttu-id="c0d56-206">Powiadomienia przestrzeni kluczy i **powiadomienia przestrzeni kluczy zdarzenia** ustawienia są dostępne tylko dla pamięci podręcznej standardowa i Premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-206">Keyspace notifications and the **notify-keyspace-events** setting are only available for Standard and Premium caches.</span></span>
> 
> 

<span data-ttu-id="c0d56-207">Aby uzyskać więcej informacji, zobacz [Redis powiadomienia przestrzeni kluczy](http://redis.io/topics/notifications).</span><span class="sxs-lookup"><span data-stu-id="c0d56-207">For more information, see [Redis Keyspace Notifications](http://redis.io/topics/notifications).</span></span> <span data-ttu-id="c0d56-208">Przykładowy kod, zobacz [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) w pliku [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) próbki.</span><span class="sxs-lookup"><span data-stu-id="c0d56-208">For sample code, see the [KeySpaceNotifications.cs](https://github.com/rustd/RedisSamples/blob/master/HelloWorld/KeySpaceNotifications.cs) file in the [Hello world](https://github.com/rustd/RedisSamples/tree/master/HelloWorld) sample.</span></span>


<a name="recommendations"></a>
## <a name="redis-cache-advisor"></a><span data-ttu-id="c0d56-209">Klasyfikator pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-209">Redis Cache Advisor</span></span>
<span data-ttu-id="c0d56-210">**Advisor pamięci podręcznej Redis** blok zawiera zalecenia dotyczące pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-210">The **Redis Cache Advisor** blade displays recommendations for your cache.</span></span> <span data-ttu-id="c0d56-211">Podczas wykonywania normalnych operacji zostaną wyświetlone żadnych zaleceń.</span><span class="sxs-lookup"><span data-stu-id="c0d56-211">During normal operations, no recommendations are displayed.</span></span> 

![Zalecenia](./media/cache-configure/redis-cache-no-recommendations.png)

<span data-ttu-id="c0d56-213">Jeśli wszystkie warunki wystąpić podczas operacji takich jak wysokie użycie pamięci przepustowości sieci i obciążenie serwera pamięci podręcznej, zostanie wyświetlony alert na **pamięci podręcznej Redis** bloku.</span><span class="sxs-lookup"><span data-stu-id="c0d56-213">If any conditions occur during the operations of your cache such as high memory usage, network bandwidth, or server load, an alert is displayed on the **Redis Cache** blade.</span></span>

![Zalecenia](./media/cache-configure/redis-cache-recommendations-alert.png)

<span data-ttu-id="c0d56-215">Więcej informacji można znaleźć w **zalecenia** bloku.</span><span class="sxs-lookup"><span data-stu-id="c0d56-215">Further information can be found on the **Recommendations** blade.</span></span>

![Zalecenia](./media/cache-configure/redis-cache-recommendations.png)

<span data-ttu-id="c0d56-217">Można monitorować te metryki na [monitorowania wykresy](cache-how-to-monitor.md#monitoring-charts) i [wykresy użycia](cache-how-to-monitor.md#usage-charts) sekcje **pamięci podręcznej Redis** bloku.</span><span class="sxs-lookup"><span data-stu-id="c0d56-217">You can monitor these metrics on the [Monitoring charts](cache-how-to-monitor.md#monitoring-charts) and [Usage charts](cache-how-to-monitor.md#usage-charts) sections of the **Redis Cache** blade.</span></span>

<span data-ttu-id="c0d56-218">Każda warstwa cenowa ma inną limity dla połączeń klienckich, pamięci oraz przepustowości.</span><span class="sxs-lookup"><span data-stu-id="c0d56-218">Each pricing tier has different limits for client connections, memory, and bandwidth.</span></span> <span data-ttu-id="c0d56-219">Jeśli pamięć podręczna zbliża się do maksymalnej pojemności dla tych metryk przez dłuższy czas, zostanie utworzony zalecenia.</span><span class="sxs-lookup"><span data-stu-id="c0d56-219">If your cache approaches maximum capacity for these metrics over a sustained period of time, a recommendation is created.</span></span> <span data-ttu-id="c0d56-220">Aby uzyskać więcej informacji o metryki i limity przeglądane przez **zalecenia** narzędzie, zobacz poniższą tabelę:</span><span class="sxs-lookup"><span data-stu-id="c0d56-220">For more information about the metrics and limits reviewed by the **Recommendations** tool, see the following table:</span></span>

| <span data-ttu-id="c0d56-221">Metryki pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-221">Redis Cache metric</span></span> | <span data-ttu-id="c0d56-222">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="c0d56-222">More information</span></span> |
| --- | --- |
| <span data-ttu-id="c0d56-223">Wykorzystanie przepustowości sieci</span><span class="sxs-lookup"><span data-stu-id="c0d56-223">Network bandwidth usage</span></span> |[<span data-ttu-id="c0d56-224">Wydajność pamięci podręcznej - dostępną przepustowość</span><span class="sxs-lookup"><span data-stu-id="c0d56-224">Cache performance - available bandwidth</span></span>](cache-faq.md#cache-performance) |
| <span data-ttu-id="c0d56-225">Podłączeni klienci</span><span class="sxs-lookup"><span data-stu-id="c0d56-225">Connected clients</span></span> |[<span data-ttu-id="c0d56-226">Domyślna konfiguracja serwera Redis - maxclients</span><span class="sxs-lookup"><span data-stu-id="c0d56-226">Default Redis server configuration - maxclients</span></span>](#maxclients) |
| <span data-ttu-id="c0d56-227">Obciążenie serwera</span><span class="sxs-lookup"><span data-stu-id="c0d56-227">Server load</span></span> |[<span data-ttu-id="c0d56-228">Wykresy użycia - obciążenia serwera Redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-228">Usage charts - Redis Server Load</span></span>](cache-how-to-monitor.md#usage-charts) |
| <span data-ttu-id="c0d56-229">Użycie pamięci</span><span class="sxs-lookup"><span data-stu-id="c0d56-229">Memory usage</span></span> |[<span data-ttu-id="c0d56-230">Wydajność pamięci podręcznej — rozmiar</span><span class="sxs-lookup"><span data-stu-id="c0d56-230">Cache performance - size</span></span>](cache-faq.md#cache-performance) |

<span data-ttu-id="c0d56-231">Aby uaktualnić pamięć podręczną, kliknij przycisk **Uaktualnij teraz** Aby zmienić warstwę cenową i [skali](#scale) pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-231">To upgrade your cache, click **Upgrade now** to change the pricing tier and [scale](#scale) your cache.</span></span> <span data-ttu-id="c0d56-232">Aby uzyskać więcej informacji o wyborze warstwy cenowej, zobacz [jakie oferty pamięć podręczna Redis i rozmiar należy używać?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span><span class="sxs-lookup"><span data-stu-id="c0d56-232">For more information on choosing a pricing tier, see [What Redis Cache offering and size should I use?](cache-faq.md#what-redis-cache-offering-and-size-should-i-use)</span></span>


### <a name="scale"></a><span data-ttu-id="c0d56-233">Skalowanie</span><span class="sxs-lookup"><span data-stu-id="c0d56-233">Scale</span></span>
<span data-ttu-id="c0d56-234">Kliknij przycisk **skali** Aby wyświetlić lub zmienić warstwę cenową dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-234">Click **Scale** to view or change the pricing tier for your cache.</span></span> <span data-ttu-id="c0d56-235">Aby uzyskać więcej informacji na temat skalowania, zobacz [jak pamięć podręczna Redis Azure skali](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-235">For more information on scaling, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>

![Warstwa cenowa pamięci podręcznej redis](./media/cache-configure/pricing-tier.png)

<a name="cluster-size"></a>

### <a name="redis-cluster-size"></a><span data-ttu-id="c0d56-237">Rozmiar klastra redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-237">Redis Cluster Size</span></span>
<span data-ttu-id="c0d56-238">Kliknij przycisk **rozmiar klastra Redis (wersja ZAPOZNAWCZA)** Aby zmienić rozmiar klastra dla bieżącej pamięci podręcznej premium z włączoną funkcją klastrowania.</span><span class="sxs-lookup"><span data-stu-id="c0d56-238">Click **(PREVIEW) Redis Cluster Size** to change the cluster size for a running premium cache with clustering enabled.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d56-239">Należy pamiętać, że podczas warstwy pamięci podręcznej Redis Azure Premium został zwolniony ogólnej dostępności, funkcja Redis rozmiar klastra obecnie w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-239">Note that while the Azure Redis Cache Premium tier has been released to General Availability, the Redis Cluster Size feature is currently in preview.</span></span>
> 
> 

![Rozmiar klastra redis](./media/cache-configure/redis-cache-redis-cluster-size.png)

<span data-ttu-id="c0d56-241">Aby zmienić rozmiar klastra, za pomocą suwaka, lub wpisz liczbę z zakresu od 1 do 10 w **liczby niezależnych** polu tekstowym i kliknij przycisk **OK** do zapisania.</span><span class="sxs-lookup"><span data-stu-id="c0d56-241">To change the cluster size, use the slider or type a number between 1 and 10 in the **Shard count** text box and click **OK** to save.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0d56-242">Klaster redis jest dostępna tylko dla pamięci podręcznej Premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-242">Redis clustering is only available for Premium caches.</span></span> <span data-ttu-id="c0d56-243">Aby uzyskać więcej informacji, zobacz temat [Konfigurowanie usługi klastrowania dla usługi Azure Redis Cache w warstwie Premium](cache-how-to-premium-clustering.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-243">For more information, see [How to configure clustering for a Premium Azure Redis Cache](cache-how-to-premium-clustering.md).</span></span>
> 
> 


### <a name="redis-data-persistence"></a><span data-ttu-id="c0d56-244">Trwałość danych redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-244">Redis data persistence</span></span>
<span data-ttu-id="c0d56-245">Kliknij przycisk **trwałość danych Redis** Aby włączyć, wyłączyć lub skonfiguruj trwałości danych dla pamięci podręcznej premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-245">Click **Redis data persistence** to enable, disable, or configure data persistence for your premium cache.</span></span> <span data-ttu-id="c0d56-246">Pamięć podręczna Redis Azure oferuje trwałość Redis przy użyciu [trwałości RDB](cache-how-to-premium-persistence.md#configure-rdb-persistence) lub [trwałości AOF](cache-how-to-premium-persistence.md#configure-aof-persistence).</span><span class="sxs-lookup"><span data-stu-id="c0d56-246">Azure Redis Cache offers Redis persistence using either [RDB persistence](cache-how-to-premium-persistence.md#configure-rdb-persistence) or [AOF persistence](cache-how-to-premium-persistence.md#configure-aof-persistence).</span></span>

<span data-ttu-id="c0d56-247">Aby uzyskać więcej informacji, zobacz [Konfigurowanie trwałości dla podręczna Redis Azure Premium](cache-how-to-premium-persistence.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-247">For more information, see [How to configure persistence for a Premium Azure Redis Cache](cache-how-to-premium-persistence.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="c0d56-248">Trwałości danych pamięci podręcznej redis jest dostępna tylko dla pamięci podręcznej Premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-248">Redis data persistence is only available for Premium caches.</span></span> 
> 
> 

### <a name="schedule-updates"></a><span data-ttu-id="c0d56-249">Aktualizacje harmonogramu</span><span class="sxs-lookup"><span data-stu-id="c0d56-249">Schedule updates</span></span>
<span data-ttu-id="c0d56-250">**Zaplanuj aktualizacje** bloku umożliwia wyznaczenie okna obsługi aktualizacji serwera Redis dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-250">The **Schedule updates** blade allows you to designate a maintenance window for Redis server updates for your cache.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c0d56-251">Okna obsługi dotyczą tylko aktualizacje serwera Redis i nie do dowolnego Azure aktualizacji lub aktualizuje systemowi operacyjnemu maszyn wirtualnych, które hostują pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-251">The maintenance window applies only to Redis server updates, and not to any Azure updates or updates to the operating system of the VMs that host the cache.</span></span>
> 
> 

![Aktualizacje harmonogramu](./media/cache-configure/redis-schedule-updates.png)

<span data-ttu-id="c0d56-253">Aby określić okna obsługi, sprawdź odpowiednią dni i określ godzina rozpoczęcia okna konserwacji codziennie i kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0d56-253">To specify a maintenance window, check the desired days and specify the maintenance window start hour for each day, and click **OK**.</span></span> <span data-ttu-id="c0d56-254">Należy pamiętać, że czas okna obsługi w formacie UTC.</span><span class="sxs-lookup"><span data-stu-id="c0d56-254">Note that the maintenance window time is in UTC.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c0d56-255">**Zaplanuj aktualizacje** funkcjonalność jest dostępna tylko dla pamięci podręcznej warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-255">The **Schedule updates** functionality is only available for Premium tier caches.</span></span> <span data-ttu-id="c0d56-256">Aby uzyskać więcej informacji oraz instrukcje, zobacz [administrowanie pamięć podręczna Redis Azure — Zaplanuj aktualizacje](cache-administration.md#schedule-updates).</span><span class="sxs-lookup"><span data-stu-id="c0d56-256">For more information and instructions, see [Azure Redis Cache administration - Schedule updates](cache-administration.md#schedule-updates).</span></span>
> 
> 

### <a name="geo-replication"></a><span data-ttu-id="c0d56-257">Replikacja geograficzna</span><span class="sxs-lookup"><span data-stu-id="c0d56-257">Geo-replication</span></span>

<span data-ttu-id="c0d56-258">**— Replikacja geograficzna** bloku udostępnia mechanizm do konsolidacji dwa wystąpienia pamięci podręcznej Redis Azure warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-258">The **Geo-replication** blade provides a mechanism for linking two Premium tier Azure Redis Cache instances.</span></span> <span data-ttu-id="c0d56-259">Jedna pamięć podręczna jest wyznaczony jako głównej połączonego pamięci podręcznej, a drugi jako dodatkowej pamięci podręcznej połączony.</span><span class="sxs-lookup"><span data-stu-id="c0d56-259">One cache is designated as the primary linked cache, and the other as the secondary linked cache.</span></span> <span data-ttu-id="c0d56-260">Dodatkowej pamięci podręcznej połączonego staje się tylko do odczytu, a dane zapisywane w pamięci podręcznej podstawowej są replikowane do dodatkowej połączonego pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-260">The secondary linked cache becomes read-only, and data written to the primary cache is replicated to the secondary linked cache.</span></span> <span data-ttu-id="c0d56-261">Ta funkcja umożliwia replikowanie pamięci podręcznej w regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d56-261">This functionality can be used to replicate a cache across Azure regions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0d56-262">**Replikacja geograficzna** jest dostępna tylko dla pamięci podręcznej warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-262">**Geo-replication** is only available for Premium tier caches.</span></span> <span data-ttu-id="c0d56-263">Aby uzyskać więcej informacji oraz instrukcje, zobacz [jak skonfigurować replikację geograficzną dla pamięci podręcznej Redis Azure](cache-how-to-geo-replication.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-263">For more information and instructions, see [How to configure Geo-replication for Azure Redis Cache](cache-how-to-geo-replication.md).</span></span>
> 
> 

### <a name="virtual-network"></a><span data-ttu-id="c0d56-264">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="c0d56-264">Virtual Network</span></span>
<span data-ttu-id="c0d56-265">**Sieci wirtualnej** sekcja umożliwia konfigurowanie ustawień sieci wirtualnej dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-265">The **Virtual Network** section allows you to configure the virtual network settings for your cache.</span></span> <span data-ttu-id="c0d56-266">Informacje na temat tworzenia pamięci podręcznej premium z sieciami Wirtualnymi obsługują i aktualizowanie jej ustawień, zobacz [Konfigurowanie obsługi sieci wirtualnej dla podręczna Redis Azure Premium](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-266">For information on creating a premium cache with VNET support and updating its settings, see [How to configure Virtual Network Support for a Premium Azure Redis Cache](cache-how-to-premium-vnet.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0d56-267">Ustawienia sieci wirtualnej są dostępne tylko dla pamięci podręcznej premium, które zostały skonfigurowane z obsługą sieci Wirtualnej podczas tworzenia pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-267">Virtual network settings are only available for premium caches that were configured with VNET support during cache creation.</span></span> 
> 
> 

### <a name="firewall"></a><span data-ttu-id="c0d56-268">Zapora</span><span class="sxs-lookup"><span data-stu-id="c0d56-268">Firewall</span></span>

<span data-ttu-id="c0d56-269">Kliknij przycisk **zapory** Aby wyświetlić i skonfigurować reguły zapory dla pamięć podręczna Redis Azure Premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-269">Click **Firewall** to view and configure firewall rules for your Premium Azure Redis Cache.</span></span>

![Zapora](./media/cache-configure/redis-firewall-rules.png)

<span data-ttu-id="c0d56-271">Początek i koniec zakresu adresów IP można określić reguły zapory.</span><span class="sxs-lookup"><span data-stu-id="c0d56-271">You can specify firewall rules with a start and end IP address range.</span></span> <span data-ttu-id="c0d56-272">Reguły zapory są skonfigurowane, tylko połączenia klienckie z podanych zakresów adresów IP umożliwia nawiązywanie pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-272">When firewall rules are configured, only client connections from the specified IP address ranges can connect to the cache.</span></span> <span data-ttu-id="c0d56-273">Po zapisaniu regułę zapory jest krótkie opóźnienie przed obowiązuje zasada.</span><span class="sxs-lookup"><span data-stu-id="c0d56-273">When a firewall rule is saved there is a short delay before the rule is effective.</span></span> <span data-ttu-id="c0d56-274">To opóźnienie jest zazwyczaj mniej niż minutę.</span><span class="sxs-lookup"><span data-stu-id="c0d56-274">This delay is typically less than one minute.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0d56-275">Połączenia z pamięcią podręczną Redis Azure monitorowania systemów będą zawsze dozwolone, nawet jeśli reguły zapory są skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="c0d56-275">Connections from Azure Redis Cache monitoring systems are always permitted, even if firewall rules are configured.</span></span>
> 
> <span data-ttu-id="c0d56-276">Reguły zapory są dostępne tylko dla pamięci podręcznej warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-276">Firewall rules are only available for Premium tier caches.</span></span>
> 
> 

### <a name="properties"></a><span data-ttu-id="c0d56-277">Właściwości</span><span class="sxs-lookup"><span data-stu-id="c0d56-277">Properties</span></span>
<span data-ttu-id="c0d56-278">Kliknij przycisk **właściwości** do wyświetlania informacji o pamięci podręcznej, łącznie z punktu końcowego pamięci podręcznej i portów.</span><span class="sxs-lookup"><span data-stu-id="c0d56-278">Click **Properties** to view information about your cache, including the cache endpoint and ports.</span></span>

![Właściwości pamięci podręcznej redis](./media/cache-configure/redis-cache-properties.png)

### <a name="locks"></a><span data-ttu-id="c0d56-280">Blokady</span><span class="sxs-lookup"><span data-stu-id="c0d56-280">Locks</span></span>
<span data-ttu-id="c0d56-281">**Blokuje** sekcji służy do blokowania subskrypcji, grupy zasobów lub zasobów uniemożliwić innym użytkownikom w organizacji przypadkowo usuwanie i modyfikowanie kluczowych zasobów.</span><span class="sxs-lookup"><span data-stu-id="c0d56-281">The **Locks** section allows you to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="c0d56-282">Aby uzyskać więcej informacji, zobacz [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md) (Blokowanie zasobów w usłudze Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="c0d56-282">For more information, see [Lock resources with Azure Resource Manager](../azure-resource-manager/resource-group-lock-resources.md).</span></span>

### <a name="automation-script"></a><span data-ttu-id="c0d56-283">Skrypt automatyzacji</span><span class="sxs-lookup"><span data-stu-id="c0d56-283">Automation script</span></span>

<span data-ttu-id="c0d56-284">Kliknij przycisk **skryptu automatyzacji** do tworzenia i eksportowania szablonu wdrożonych zasobów do przyszłych wdrożeń.</span><span class="sxs-lookup"><span data-stu-id="c0d56-284">Click **Automation script** to build and export a template of your deployed resources for future deployments.</span></span> <span data-ttu-id="c0d56-285">Aby uzyskać więcej informacji na temat pracy z szablonami, zobacz [wdrożenie zasobów przy użyciu szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-285">For more information about working with templates, see [Deploy resources with Azure Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

## <a name="administration-settings"></a><span data-ttu-id="c0d56-286">Ustawienia administracji</span><span class="sxs-lookup"><span data-stu-id="c0d56-286">Administration settings</span></span>
<span data-ttu-id="c0d56-287">Ustawienia w **administracji** sekcji umożliwiają wykonywanie następujących zadań administracyjnych dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-287">The settings in the **Administration** section allow you to perform the following administrative tasks for your cache.</span></span> 

![Administracja](./media/cache-configure/redis-cache-administration.png)

* [<span data-ttu-id="c0d56-289">Importowanie danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-289">Import data</span></span>](#importexport)
* [<span data-ttu-id="c0d56-290">Eksportowanie danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-290">Export data</span></span>](#importexport)
* [<span data-ttu-id="c0d56-291">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="c0d56-291">Reboot</span></span>](#reboot)


### <a name="importexport"></a><span data-ttu-id="c0d56-292">Import/Export</span><span class="sxs-lookup"><span data-stu-id="c0d56-292">Import/Export</span></span>
<span data-ttu-id="c0d56-293">Import/Eksport jest operacji zarządzania pamięcią podręczną Redis Azure danych, która umożliwia importowanie i eksportowanie danych w pamięci podręcznej przez importowanie i Eksportowanie migawki Redis pamięci podręcznej bazy danych (RDB) z usługi pamięć podręczna premium do stronicowych obiektów blob na koncie magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d56-293">Import/Export is an Azure Redis Cache data management operation, which allows you to import and export data in the cache by importing and exporting a Redis Cache Database (RDB) snapshot from a premium cache to a page blob in an Azure Storage Account.</span></span> <span data-ttu-id="c0d56-294">Importu/eksportu umożliwia migrację między różnymi wystąpieniami usługi pamięć podręczna Redis Azure lub wypełnienie pamięci podręcznej danych przed użyciem.</span><span class="sxs-lookup"><span data-stu-id="c0d56-294">Import/Export enables you to migrate between different Azure Redis Cache instances or populate the cache with data before use.</span></span>

<span data-ttu-id="c0d56-295">Import może służyć do pamięci podręcznej Redis zgodne RDB plików z dowolnego serwera Redis uruchomiona w chmurze lub środowiska, w tym Redis w systemie Linux, Windows albo dowolnego dostawcy chmury, takich jak usług Amazon Web Services i inne.</span><span class="sxs-lookup"><span data-stu-id="c0d56-295">Import can be used to bring Redis compatible RDB files from any Redis server running in any cloud or environment, including Redis running on Linux, Windows, or any cloud provider such as Amazon Web Services and others.</span></span> <span data-ttu-id="c0d56-296">Importowanie danych jest w prosty sposób tworzenia pamięci podręcznej z wstępnie wypełnione danych.</span><span class="sxs-lookup"><span data-stu-id="c0d56-296">Importing data is an easy way to create a cache with pre-populated data.</span></span> <span data-ttu-id="c0d56-297">Podczas procesu importowania pamięć podręczna Redis Azure ładuje RDB pliki z magazynu Azure do pamięci i wstawia klucze do pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-297">During the import process, Azure Redis Cache loads the RDB files from Azure storage into memory, and then inserts the keys into the cache.</span></span>

<span data-ttu-id="c0d56-298">Eksport pozwala na wyeksportowanie danych przechowywanych w pamięci podręcznej Redis Azure do Redis zgodne pliki RDB.</span><span class="sxs-lookup"><span data-stu-id="c0d56-298">Export allows you to export the data stored in Azure Redis Cache to Redis compatible RDB files.</span></span> <span data-ttu-id="c0d56-299">Ta funkcja służy do przenoszenia danych z jednego wystąpienia pamięci podręcznej Redis Azure do innego lub do innego serwera Redis.</span><span class="sxs-lookup"><span data-stu-id="c0d56-299">You can use this feature to move data from one Azure Redis Cache instance to another or to another Redis server.</span></span> <span data-ttu-id="c0d56-300">Podczas procesu eksportowania plik tymczasowy zostanie utworzony na maszynie Wirtualnej, która obsługuje wystąpienie serwera pamięci podręcznej Redis Azure, a plik jest przekazywany do konta magazynu wyznaczonego.</span><span class="sxs-lookup"><span data-stu-id="c0d56-300">During the export process, a temporary file is created on the VM that hosts the Azure Redis Cache server instance, and the file is uploaded to the designated storage account.</span></span> <span data-ttu-id="c0d56-301">Po zakończeniu operacji eksportowania stan powodzenia lub błędu, plik tymczasowy zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="c0d56-301">When the export operation completes with either a status of success or failure, the temporary file is deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0d56-302">Narzędzie importu/eksportu jest dostępna tylko dla pamięci podręcznej warstwy Premium.</span><span class="sxs-lookup"><span data-stu-id="c0d56-302">Import/Export is only available for Premium tier caches.</span></span> <span data-ttu-id="c0d56-303">Aby uzyskać więcej informacji oraz instrukcje, zobacz [importować i eksportować dane w pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-303">For more information and instructions, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

### <a name="reboot"></a><span data-ttu-id="c0d56-304">Ponowne uruchamianie</span><span class="sxs-lookup"><span data-stu-id="c0d56-304">Reboot</span></span>
<span data-ttu-id="c0d56-305">**Ponowny rozruch** bloku umożliwia ponownego uruchomienia węzłów pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-305">The **Reboot** blade allows you to reboot the nodes of your cache.</span></span> <span data-ttu-id="c0d56-306">Ta możliwość ponownego uruchomienia pozwala testować aplikację odporności w przypadku awarii węzła pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-306">This reboot capability enables you to test your application for resiliency if there is a failure of a cache node.</span></span>

![Ponowne uruchamianie](./media/cache-configure/redis-cache-reboot.png)

<span data-ttu-id="c0d56-308">Jeśli pamięć podręczna premium z włączoną funkcją klastrowania, można wybrać, które odłamków pamięci podręcznej, aby ponownie uruchomić system.</span><span class="sxs-lookup"><span data-stu-id="c0d56-308">If you have a premium cache with clustering enabled, you can select which shards of the cache to reboot.</span></span>

![Ponowne uruchamianie](./media/cache-configure/redis-cache-reboot-cluster.png)

<span data-ttu-id="c0d56-310">Ponownie uruchomić co najmniej jeden węzeł z pamięci podręcznej, wybierz żądany węzeł i kliknij przycisk **ponowny rozruch**.</span><span class="sxs-lookup"><span data-stu-id="c0d56-310">To reboot one or more nodes of your cache, select the desired nodes and click **Reboot**.</span></span> <span data-ttu-id="c0d56-311">Jeśli masz usługi pamięć podręczna premium z włączoną funkcją klastrowania shard(s) ponowny rozruch, a następnie kliknij przycisk Wybierz **ponowny rozruch**.</span><span class="sxs-lookup"><span data-stu-id="c0d56-311">If you have a premium cache with clustering enabled, select the shard(s) to reboot and then click **Reboot**.</span></span> <span data-ttu-id="c0d56-312">Po kilku minutach ponowne uruchomienie wybranych węzłów i można je do trybu online później za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c0d56-312">After a few minutes, the selected node(s) reboot, and are back online a few minutes later.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0d56-313">Ponowne uruchomienie jest teraz dostępna dla wszystkich warstw cenowych.</span><span class="sxs-lookup"><span data-stu-id="c0d56-313">Reboot is now available for all pricing tiers.</span></span> <span data-ttu-id="c0d56-314">Aby uzyskać więcej informacji oraz instrukcje, zobacz [administrowanie pamięć podręczna Redis Azure — ponowne uruchomienie](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="c0d56-314">For more information and instructions, see [Azure Redis Cache administration - Reboot](cache-administration.md#reboot).</span></span>
> 
> 


## <a name="monitoring"></a><span data-ttu-id="c0d56-315">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="c0d56-315">Monitoring</span></span>

<span data-ttu-id="c0d56-316">**Monitorowanie** sekcji pozwala na skonfigurowanie Diagnostyka i monitorowanie dla pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="c0d56-316">The **Monitoring** section allows you to configure diagnostics and monitoring for your Redis Cache.</span></span> <span data-ttu-id="c0d56-317">Aby uzyskać więcej informacji o pamięci podręcznej Redis Azure monitorowania i diagnostyki, zobacz [jak monitorować pamięć podręczna Redis Azure](cache-how-to-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-317">For more information on Azure Redis Cache monitoring and diagnostics, see [How to monitor Azure Redis Cache](cache-how-to-monitor.md).</span></span>

![Diagnostyka](./media/cache-configure/redis-cache-diagnostics.png)

* [<span data-ttu-id="c0d56-319">Redis metryk</span><span class="sxs-lookup"><span data-stu-id="c0d56-319">Redis metrics</span></span>](#redis-metrics)
* [<span data-ttu-id="c0d56-320">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="c0d56-320">Alert rules</span></span>](#alert-rules)
* [<span data-ttu-id="c0d56-321">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="c0d56-321">Diagnostics</span></span>](#diagnostics)

### <a name="redis-metrics"></a><span data-ttu-id="c0d56-322">Redis metryk</span><span class="sxs-lookup"><span data-stu-id="c0d56-322">Redis metrics</span></span>
<span data-ttu-id="c0d56-323">Kliknij przycisk **Redis metryki** do [wyświetlić metryki](cache-how-to-monitor.md#view-cache-metrics) dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-323">Click **Redis metrics** to [view metrics](cache-how-to-monitor.md#view-cache-metrics) for your cache.</span></span>

### <a name="alert-rules"></a><span data-ttu-id="c0d56-324">Reguły alertów</span><span class="sxs-lookup"><span data-stu-id="c0d56-324">Alert rules</span></span>

<span data-ttu-id="c0d56-325">Kliknij przycisk **reguły alertów** Konfigurowanie alertów w oparciu metryki pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="c0d56-325">Click **Alert rules** to configure alerts based on Redis Cache metrics.</span></span> <span data-ttu-id="c0d56-326">Aby uzyskać więcej informacji, zobacz [alerty](cache-how-to-monitor.md#alerts).</span><span class="sxs-lookup"><span data-stu-id="c0d56-326">For more information, see [Alerts](cache-how-to-monitor.md#alerts).</span></span>

### <a name="diagnostics"></a><span data-ttu-id="c0d56-327">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="c0d56-327">Diagnostics</span></span>

<span data-ttu-id="c0d56-328">Domyślnie są metryki pamięci podręcznej w monitorze Azure [przechowywane przez 30 dni](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) , a następnie usuwany.</span><span class="sxs-lookup"><span data-stu-id="c0d56-328">By default, cache metrics in Azure Monitor are [stored for 30 days](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md#store-and-archive) and then deleted.</span></span> <span data-ttu-id="c0d56-329">Aby zachować Twoje metryki pamięci podręcznej przez czas dłuższy niż 30 dni, kliknij przycisk **diagnostyki** do [Konfigurowanie konta magazynu](cache-how-to-monitor.md#export-cache-metrics) używany do przechowywania Diagnostyka pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-329">To persist your cache metrics for longer than 30 days, click **Diagnostics** to [configure the storage account](cache-how-to-monitor.md#export-cache-metrics) used to store cache diagnostics.</span></span>

>[!NOTE]
><span data-ttu-id="c0d56-330">Oprócz archiwizacji Twoje metryki pamięci podręcznej do magazynu, możesz również [strumienia je do Centrum zdarzeń lub wysłać je do analizy dzienników](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span><span class="sxs-lookup"><span data-stu-id="c0d56-330">In addition to archiving your cache metrics to storage, you can also [stream them to an Event hub or send them to Log Analytics](../monitoring-and-diagnostics/monitoring-overview-metrics.md#export-metrics).</span></span>
>
>

## <a name="support--troubleshooting-settings"></a><span data-ttu-id="c0d56-331">Rozwiązywanie problemów z ustawieniami i pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="c0d56-331">Support & troubleshooting settings</span></span>
<span data-ttu-id="c0d56-332">Ustawienia w **pomocy technicznej i rozwiązywania problemów** sekcja zawiera opcje rozwiązywania problemów związanych z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-332">The settings in the **Support + troubleshooting** section provide you with options for resolving issues with your cache.</span></span>

![Pomocy technicznej i rozwiązywania problemów](./media/cache-configure/redis-cache-support-troubleshooting.png)

* [<span data-ttu-id="c0d56-334">Kondycja zasobów</span><span class="sxs-lookup"><span data-stu-id="c0d56-334">Resource health</span></span>](#resource-health)
* [<span data-ttu-id="c0d56-335">Nowe żądanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="c0d56-335">New support request</span></span>](#new-support-request)

### <a name="resource-health"></a><span data-ttu-id="c0d56-336">Kondycja zasobów</span><span class="sxs-lookup"><span data-stu-id="c0d56-336">Resource health</span></span>
<span data-ttu-id="c0d56-337">**Kondycja zasobów** oczekuje zasobu i informuje, czy działa on zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="c0d56-337">**Resource health** watches your resource and tells you if it's running as expected.</span></span> <span data-ttu-id="c0d56-338">Aby uzyskać więcej informacji o usłudze kondycji zasobów Azure, zobacz [Przegląd kondycji zasobów Azure](../resource-health/resource-health-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-338">For more information about the Azure Resource health service, see [Azure Resource health overview](../resource-health/resource-health-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c0d56-339">Kondycja zasobu nie może obecnie raport dotyczący kondycji wystąpień pamięci podręcznej Redis Azure hostowanej w sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-339">Resource health is currently unable to report on the health of Azure Redis Cache instances hosted in a virtual network.</span></span> <span data-ttu-id="c0d56-340">Aby uzyskać więcej informacji, zobacz [wszystkie funkcje pamięci podręcznej działają odnośnie do hostowania pamięci podręcznej w sieci Wirtualnej?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span><span class="sxs-lookup"><span data-stu-id="c0d56-340">For more information, see [Do all cache features work when hosting a cache in a VNET?](cache-how-to-premium-vnet.md#do-all-cache-features-work-when-hosting-a-cache-in-a-vnet)</span></span>
> 
> 

### <a name="new-support-request"></a><span data-ttu-id="c0d56-341">Nowe żądanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="c0d56-341">New support request</span></span>
<span data-ttu-id="c0d56-342">Kliknij przycisk **nowy obsługuje żądania** otwarcia żądania pomocy technicznej dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-342">Click **New support request** to open a support request for your cache.</span></span>





## <a name="default-redis-server-configuration"></a><span data-ttu-id="c0d56-343">Domyślna konfiguracja serwera Redis</span><span class="sxs-lookup"><span data-stu-id="c0d56-343">Default Redis server configuration</span></span>
<span data-ttu-id="c0d56-344">Nowe wystąpienia pamięci podręcznej Redis Azure są skonfigurowane z następujących domyślnych wartości konfiguracji pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="c0d56-344">New Azure Redis Cache instances are configured with the following default Redis configuration values.</span></span>

> [!NOTE]
> <span data-ttu-id="c0d56-345">Nie można zmienić ustawienia w tej sekcji przy użyciu `StackExchange.Redis.IServer.ConfigSet` metody.</span><span class="sxs-lookup"><span data-stu-id="c0d56-345">The settings in this section cannot be changed using the `StackExchange.Redis.IServer.ConfigSet` method.</span></span> <span data-ttu-id="c0d56-346">Jeśli ta metoda jest wywoływana z jednego z poleceń w tej sekcji, jest zgłaszany wyjątek podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="c0d56-346">If this method is called with one of the commands in this section, an exception similar to the following is thrown:</span></span>  
> 
> `StackExchange.Redis.RedisServerException: ERR unknown command 'CONFIG'`
> 
> <span data-ttu-id="c0d56-347">Wartości, które można skonfigurować, takie jak **Maksymalna pamięć zasady**, można skonfigurować za pomocą portalu Azure lub narzędzia do zarządzania wiersza polecenia takich jak wiersza polecenia platformy Azure lub programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c0d56-347">Any values that are configurable, such as **max-memory-policy**, are configurable through the Azure portal or command-line management tools such as Azure CLI or PowerShell.</span></span>
> 
> 

| <span data-ttu-id="c0d56-348">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="c0d56-348">Setting</span></span> | <span data-ttu-id="c0d56-349">Wartość domyślna</span><span class="sxs-lookup"><span data-stu-id="c0d56-349">Default value</span></span> | <span data-ttu-id="c0d56-350">Opis</span><span class="sxs-lookup"><span data-stu-id="c0d56-350">Description</span></span> |
| --- | --- | --- |
| `databases` |<span data-ttu-id="c0d56-351">16</span><span class="sxs-lookup"><span data-stu-id="c0d56-351">16</span></span> |<span data-ttu-id="c0d56-352">Domyślna liczba baz danych jest 16, ale można skonfigurować wiele różnych oparte na warstwie cenowej. <sup>1</sup> domyślna baza danych jest DB 0, możesz wybrać inną na podstawę dla każdego połączenia przy użyciu `connection.GetDatabase(dbid)` gdzie `dbid` jest liczbą z zakresu od `0` i `databases - 1`.</span><span class="sxs-lookup"><span data-stu-id="c0d56-352">The default number of databases is 16 but you can configure a different number based on the pricing tier.<sup>1</sup> The default database is DB 0, you can select a different one on a per-connection basis using `connection.GetDatabase(dbid)` where `dbid` is a number between `0` and `databases - 1`.</span></span> |
| `maxclients` |<span data-ttu-id="c0d56-353">Zależy od warstwy cenowej<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="c0d56-353">Depends on the pricing tier<sup>2</sup></span></span> |<span data-ttu-id="c0d56-354">Jest to maksymalna liczba podłączonych klientów dozwolone w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="c0d56-354">This is the maximum number of connected clients allowed at the same time.</span></span> <span data-ttu-id="c0d56-355">Po osiągnięciu limitu pamięci podręcznej Redis zamyka wszystkie nowe połączenia, zwróci komunikat "Osiągnięto maksymalną liczbę klientów".</span><span class="sxs-lookup"><span data-stu-id="c0d56-355">Once the limit is reached Redis closes all the new connections, returning a 'max number of clients reached' error.</span></span> |
| `maxmemory-policy` |`volatile-lru` |<span data-ttu-id="c0d56-356">Zasady Maxmemory jest jak Redis wybiera co do usunięcia, gdy to ustawienie `maxmemory` osiągnięciu (rozmiar pamięci podręcznej oferty wybranej podczas tworzenia pamięci podręcznej).</span><span class="sxs-lookup"><span data-stu-id="c0d56-356">Maxmemory policy is the setting for how Redis selects what to remove when `maxmemory` (the size of the cache offering you selected when you created the cache) is reached.</span></span> <span data-ttu-id="c0d56-357">Z pamięci podręcznej Redis Azure jest ustawieniem domyślnym `volatile-lru`, które powoduje usunięcie kluczy z wygaśnięciem ustawić za pomocą algorytmu LRU.</span><span class="sxs-lookup"><span data-stu-id="c0d56-357">With Azure Redis Cache the default setting is `volatile-lru`, which removes the keys with an expiration set using an LRU algorithm.</span></span> <span data-ttu-id="c0d56-358">To ustawienie można skonfigurować w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d56-358">This setting can be configured in the Azure portal.</span></span> <span data-ttu-id="c0d56-359">Aby uzyskać więcej informacji, zobacz [zasady pamięci](#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="c0d56-359">For more information, see [Memory policies](#memory-policies).</span></span> |
| `maxmemory-samples` |<span data-ttu-id="c0d56-360">3</span><span class="sxs-lookup"><span data-stu-id="c0d56-360">3</span></span> |<span data-ttu-id="c0d56-361">Aby zapisać pamięci, LRU i minimalny czas wygaśnięcia algorytmy są przybliżona algorytmy zamiast dokładne algorytmów.</span><span class="sxs-lookup"><span data-stu-id="c0d56-361">To save memory, LRU and minimal TTL algorithms are approximated algorithms instead of precise algorithms.</span></span> <span data-ttu-id="c0d56-362">Domyślnie Redis kontroli trzy klucze i pobrania ten, który został użyty mniej ostatnio.</span><span class="sxs-lookup"><span data-stu-id="c0d56-362">By default Redis checks three keys and picks the one that was used less recently.</span></span> |
| `lua-time-limit` |<span data-ttu-id="c0d56-363">5,000</span><span class="sxs-lookup"><span data-stu-id="c0d56-363">5,000</span></span> |<span data-ttu-id="c0d56-364">Maksymalny czas wykonywania skryptu Lua (w milisekundach).</span><span class="sxs-lookup"><span data-stu-id="c0d56-364">Max execution time of a Lua script in milliseconds.</span></span> <span data-ttu-id="c0d56-365">Po osiągnięciu maksymalnego czasu wykonywania Redis rejestruje skryptu nadal trwa wykonywanie po maksymalny dozwolony czas i uruchamia na udzielenie odpowiedzi na zapytania z powodu błędu.</span><span class="sxs-lookup"><span data-stu-id="c0d56-365">If the maximum execution time is reached, Redis logs that a script is still in execution after the maximum allowed time, and starts to reply to queries with an error.</span></span> |
| `lua-event-limit` |<span data-ttu-id="c0d56-366">500</span><span class="sxs-lookup"><span data-stu-id="c0d56-366">500</span></span> |<span data-ttu-id="c0d56-367">Maksymalny rozmiar kolejki zdarzeń skryptu.</span><span class="sxs-lookup"><span data-stu-id="c0d56-367">Max size of script event queue.</span></span> |
| <span data-ttu-id="c0d56-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span><span class="sxs-lookup"><span data-stu-id="c0d56-368">`client-output-buffer-limit` `normalclient-output-buffer-limit` `pubsub`</span></span> |<span data-ttu-id="c0d56-369">0 0 mb 032 8mb 60</span><span class="sxs-lookup"><span data-stu-id="c0d56-369">0 0 032mb 8mb 60</span></span> |<span data-ttu-id="c0d56-370">Limity buforu wyjściowego klienta można wymusić odłączenie klientów, którzy nie są odczytywanie danych z serwera wystarczająca jakiegoś powodu (typową przyczyną jest, że klient Pub/Sub nie mogą korzystać z wiadomości tak szybko, jak wydawcy można tworzyć je).</span><span class="sxs-lookup"><span data-stu-id="c0d56-370">The client output buffer limits can be used to force disconnection of clients that are not reading data from the server fast enough for some reason (a common reason is that a Pub/Sub client can't consume messages as fast as the publisher can produce them).</span></span> <span data-ttu-id="c0d56-371">Aby uzyskać więcej informacji, zobacz [http://redis.io/topics/clients](http://redis.io/topics/clients).</span><span class="sxs-lookup"><span data-stu-id="c0d56-371">For more information, see [http://redis.io/topics/clients](http://redis.io/topics/clients).</span></span> |

<span data-ttu-id="c0d56-372"><a name="databases"></a>
<sup>1</sup>limit `databases` jest różne dla każdego pamięć podręczna Redis Azure warstwy cenowej i można ustawić na tworzenie pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-372"><a name="databases"></a>
<sup>1</sup>The limit for `databases` is different for each Azure Redis Cache pricing tier and can be set at cache creation.</span></span> <span data-ttu-id="c0d56-373">Jeśli nie `databases` ustawienie jest określone podczas tworzenia pamięci podręcznej, wartość domyślna to 16.</span><span class="sxs-lookup"><span data-stu-id="c0d56-373">If no `databases` setting is specified during cache creation, the default is 16.</span></span>

* <span data-ttu-id="c0d56-374">Podstawowa i standardowa pamięci podręczne</span><span class="sxs-lookup"><span data-stu-id="c0d56-374">Basic and Standard caches</span></span>
  * <span data-ttu-id="c0d56-375">C0 (250 MB) pamięci podręcznej - maksymalnie 16 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-375">C0 (250 MB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="c0d56-376">C1 pamięci podręcznej (1 GB) — maksymalnie 16 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-376">C1 (1 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="c0d56-377">C2 pamięci podręcznej (2,5 GB) — maksymalnie 16 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-377">C2 (2.5 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="c0d56-378">C3 pamięci podręcznej (6 GB) — maksymalnie 16 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-378">C3 (6 GB) cache - up to 16 databases</span></span>
  * <span data-ttu-id="c0d56-379">C4 (13 GB) pamięci podręcznej - maksymalnie 32 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-379">C4 (13 GB) cache - up to 32 databases</span></span>
  * <span data-ttu-id="c0d56-380">C5 (26 GB) pamięci podręcznej - maksymalnie 48 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-380">C5 (26 GB) cache - up to 48 databases</span></span>
  * <span data-ttu-id="c0d56-381">C6 (53 GB) pamięci podręcznej - maksymalnie 64 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-381">C6 (53 GB) cache - up to 64 databases</span></span>
* <span data-ttu-id="c0d56-382">Pamięci podręczne — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="c0d56-382">Premium caches</span></span>
  * <span data-ttu-id="c0d56-383">P1 (6 GB — 60 GB) — maksymalnie 16 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-383">P1 (6 GB - 60 GB) - up to 16 databases</span></span>
  * <span data-ttu-id="c0d56-384">P2 (13 GB - 130 GB) — maksymalnie 32 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-384">P2 (13 GB - 130 GB) - up to 32 databases</span></span>
  * <span data-ttu-id="c0d56-385">P3 (26 GB - 260 GB) — maksymalnie 48 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-385">P3 (26 GB - 260 GB) - up to 48 databases</span></span>
  * <span data-ttu-id="c0d56-386">P4 (53 GB - 530 GB) — maksymalnie 64 baz danych</span><span class="sxs-lookup"><span data-stu-id="c0d56-386">P4 (53 GB - 530 GB) - up to 64 databases</span></span>
  * <span data-ttu-id="c0d56-387">Wszystkie bufory premium z klastrem Redis enabled - klaster Redis obsługuje tylko bazy danych 0 tak `databases` limit pamięci podręcznej premium żadnych włączono klaster Redis skutecznie to 1 i [wybierz](http://redis.io/commands/select) polecenie nie jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="c0d56-387">All premium caches with Redis cluster enabled - Redis cluster only supports use of database 0 so the `databases` limit for any premium cache with Redis cluster enabled is effectively 1 and the [Select](http://redis.io/commands/select) command is not allowed.</span></span> <span data-ttu-id="c0d56-388">Aby uzyskać więcej informacji, zobacz [należy wprowadzać żadnych zmian do mojej aplikacji klienta do korzystania z klastra?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span><span class="sxs-lookup"><span data-stu-id="c0d56-388">For more information, see [Do I need to make any changes to my client application to use clustering?](cache-how-to-premium-clustering.md#do-i-need-to-make-any-changes-to-my-client-application-to-use-clustering)</span></span>

<span data-ttu-id="c0d56-389">Aby uzyskać więcej informacji na temat baz danych, zobacz [co to są Redis baz danych?](cache-faq.md#what-are-redis-databases)</span><span class="sxs-lookup"><span data-stu-id="c0d56-389">For more information about databases, see [What are Redis databases?](cache-faq.md#what-are-redis-databases)</span></span>

> [!NOTE]
> <span data-ttu-id="c0d56-390">`databases` Ustawienie może być skonfigurowany tylko podczas tworzenia pamięci podręcznej i tylko przy użyciu programu PowerShell, interfejsu wiersza polecenia lub innych klientów zarządzania.</span><span class="sxs-lookup"><span data-stu-id="c0d56-390">The `databases` setting can be configured only during cache creation and only using PowerShell, CLI, or other management clients.</span></span> <span data-ttu-id="c0d56-391">Aby uzyskać przykład konfigurowania `databases` podczas tworzenia pamięci podręcznej przy użyciu programu PowerShell, zobacz [AzureRmRedisCache nowy](cache-howto-manage-redis-cache-powershell.md#databases).</span><span class="sxs-lookup"><span data-stu-id="c0d56-391">For an example of configuring `databases` during cache creation using PowerShell, see [New-AzureRmRedisCache](cache-howto-manage-redis-cache-powershell.md#databases).</span></span>
> 
> 

<span data-ttu-id="c0d56-392"><a name="maxclients"></a>
<sup>2</sup> `maxclients` jest różne dla każdego pamięć podręczna Redis Azure warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-392"><a name="maxclients"></a>
<sup>2</sup>`maxclients` is different for each Azure Redis Cache pricing tier.</span></span>

* <span data-ttu-id="c0d56-393">Podstawowa i standardowa pamięci podręczne</span><span class="sxs-lookup"><span data-stu-id="c0d56-393">Basic and Standard caches</span></span>
  * <span data-ttu-id="c0d56-394">C0 (250 MB) pamięci podręcznej - maksymalnie 256 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-394">C0 (250 MB) cache - up to 256 connections</span></span>
  * <span data-ttu-id="c0d56-395">C1 pamięci podręcznej (1 GB) — maksymalnie 1000 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-395">C1 (1 GB) cache - up to 1,000 connections</span></span>
  * <span data-ttu-id="c0d56-396">C2 pamięci podręcznej (2,5 GB) — maksymalnie 2000 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-396">C2 (2.5 GB) cache - up to 2,000 connections</span></span>
  * <span data-ttu-id="c0d56-397">C3 pamięci podręcznej (6 GB) — maksymalnie 5000 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-397">C3 (6 GB) cache - up to 5,000 connections</span></span>
  * <span data-ttu-id="c0d56-398">C4 (13 GB) pamięci podręcznej - maksymalnie 10 000 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-398">C4 (13 GB) cache - up to 10,000 connections</span></span>
  * <span data-ttu-id="c0d56-399">C5 (26 GB) pamięci podręcznej - maksymalnie 15 000 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-399">C5 (26 GB) cache - up to 15,000 connections</span></span>
  * <span data-ttu-id="c0d56-400">C6 (53 GB) pamięci podręcznej - maksymalnie 20 000 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-400">C6 (53 GB) cache - up to 20,000 connections</span></span>
* <span data-ttu-id="c0d56-401">Pamięci podręczne — wersja Premium</span><span class="sxs-lookup"><span data-stu-id="c0d56-401">Premium caches</span></span>
  * <span data-ttu-id="c0d56-402">P1 (6 GB — 60 GB) — maksymalnie 7500 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-402">P1 (6 GB - 60 GB) - up to 7,500 connections</span></span>
  * <span data-ttu-id="c0d56-403">P2 (13 GB - 130 GB) — maksymalnie 15 000 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-403">P2 (13 GB - 130 GB) - up to 15,000 connections</span></span>
  * <span data-ttu-id="c0d56-404">P3 (26 GB - 260 GB) — maksymalnie 30 000 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-404">P3 (26 GB - 260 GB) - up to 30,000 connections</span></span>
  * <span data-ttu-id="c0d56-405">P4 (53 GB - 530 GB) — do 40 000 połączeń</span><span class="sxs-lookup"><span data-stu-id="c0d56-405">P4 (53 GB - 530 GB) - up to 40,000 connections</span></span>

> [!NOTE]
> <span data-ttu-id="c0d56-406">Podczas każdego rozmiaru pamięci podręcznej umożliwia *do* określonej liczby połączeń, każdego połączenia Redis obciążenie ma skojarzonych z nim.</span><span class="sxs-lookup"><span data-stu-id="c0d56-406">While each size of cache allows *up to* a certain number of connections, each connection to Redis has overhead associated with it.</span></span> <span data-ttu-id="c0d56-407">Przykładem takich obciążenie będzie użycia Procesora i pamięci w wyniku szyfrowania TLS/SSL.</span><span class="sxs-lookup"><span data-stu-id="c0d56-407">An example of such overhead would be CPU and memory usage as a result of TLS/SSL encryption.</span></span> <span data-ttu-id="c0d56-408">Limit maksymalnej liczby połączeń dla rozmiaru pamięci podręcznej danego zakłada lekkim załadować pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-408">The maximum connection limit for a given cache size assumes a lightly loaded cache.</span></span> <span data-ttu-id="c0d56-409">Czy ładowanie z połączenia koszty *plus* obciążenia z operacjami klienta przekracza pojemność dla systemu, pamięci podręcznej mogą doświadczyć problemów dotyczących pojemności, nawet jeśli nie przekroczono limit połączeń dla bieżący rozmiar pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-409">If load from connection overhead *plus* load from client operations exceeds capacity for the system, the cache can experience capacity issues even if you have not exceeded the connection limit for the current cache size.</span></span>
> 
> 



## <a name="redis-commands-not-supported-in-azure-redis-cache"></a><span data-ttu-id="c0d56-410">Redis polecenia nie są obsługiwane w pamięci podręcznej Redis Azure</span><span class="sxs-lookup"><span data-stu-id="c0d56-410">Redis commands not supported in Azure Redis Cache</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c0d56-411">Ponieważ konfiguracji i zarządzania wystąpienia pamięci podręcznej Redis Azure jest zarządzany przez firmę Microsoft, poniższe polecenia są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="c0d56-411">Because configuration and management of Azure Redis Cache instances is managed by Microsoft, the following commands are disabled.</span></span> <span data-ttu-id="c0d56-412">Jeśli spróbujesz ich wywołać, pojawi się komunikat o błędzie podobny do `"(error) ERR unknown command"`.</span><span class="sxs-lookup"><span data-stu-id="c0d56-412">If you try to invoke them, you receive an error message similar to `"(error) ERR unknown command"`.</span></span>
> 
> * <span data-ttu-id="c0d56-413">BGREWRITEAOF</span><span class="sxs-lookup"><span data-stu-id="c0d56-413">BGREWRITEAOF</span></span>
> * <span data-ttu-id="c0d56-414">BGSAVE</span><span class="sxs-lookup"><span data-stu-id="c0d56-414">BGSAVE</span></span>
> * <span data-ttu-id="c0d56-415">KONFIGURACJI</span><span class="sxs-lookup"><span data-stu-id="c0d56-415">CONFIG</span></span>
> * <span data-ttu-id="c0d56-416">DEBUGOWANIA</span><span class="sxs-lookup"><span data-stu-id="c0d56-416">DEBUG</span></span>
> * <span data-ttu-id="c0d56-417">MIGRACJA</span><span class="sxs-lookup"><span data-stu-id="c0d56-417">MIGRATE</span></span>
> * <span data-ttu-id="c0d56-418">ZAPISZ</span><span class="sxs-lookup"><span data-stu-id="c0d56-418">SAVE</span></span>
> * <span data-ttu-id="c0d56-419">ZAMKNIĘCIE</span><span class="sxs-lookup"><span data-stu-id="c0d56-419">SHUTDOWN</span></span>
> * <span data-ttu-id="c0d56-420">SLAVEOF</span><span class="sxs-lookup"><span data-stu-id="c0d56-420">SLAVEOF</span></span>
> * <span data-ttu-id="c0d56-421">KLASTER - klaster zapisu, które polecenia są wyłączone, ale tylko do odczytu klastra polecenia są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="c0d56-421">CLUSTER - Cluster write commands are disabled, but read-only Cluster commands are permitted.</span></span>
> 
> 

<span data-ttu-id="c0d56-422">Aby uzyskać więcej informacji o poleceniach Redis, zobacz [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="c0d56-422">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>

## <a name="redis-console"></a><span data-ttu-id="c0d56-423">Redis konsoli</span><span class="sxs-lookup"><span data-stu-id="c0d56-423">Redis console</span></span>
<span data-ttu-id="c0d56-424">Można bezpiecznie wysyłać polecenia do Twojego wystąpienia pamięci podręcznej Redis Azure za pomocą **Redis konsoli**, która jest dostępna w portalu Azure dla wszystkich warstw pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-424">You can securely issue commands to your Azure Redis Cache instances using the **Redis Console**, which is available in the Azure portal for all cache tiers.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="c0d56-425">Konsola Redis nie działa z [sieci Wirtualnej](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-425">The Redis Console does not work with [VNET](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="c0d56-426">Jeśli pamięć podręczna jest częścią sieci Wirtualnej, tylko klienci w sieci Wirtualnej można uzyskać dostępu do pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-426">When your cache is part of a VNET, only clients in the VNET can access the cache.</span></span> <span data-ttu-id="c0d56-427">Ponieważ Redis konsola jest uruchamiana w przeglądarce lokalnego znajduje się poza siecią Wirtualną, nie może nawiązać połączenia z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-427">Because Redis Console runs in your local browser, which is outside the VNET, it can't connect to your cache.</span></span>
> - <span data-ttu-id="c0d56-428">Nie wszystkie polecenia Redis są obsługiwane w pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="c0d56-428">Not all Redis commands are supported in Azure Redis Cache.</span></span> <span data-ttu-id="c0d56-429">Listę poleceń pamięci podręcznej Redis, które są wyłączone dla pamięci podręcznej Redis Azure, zobacz poprzedni [polecenia nie są obsługiwane w pamięci podręcznej Redis Azure Redis](#redis-commands-not-supported-in-azure-redis-cache) sekcji.</span><span class="sxs-lookup"><span data-stu-id="c0d56-429">For a list of Redis commands that are disabled for Azure Redis Cache, see the previous [Redis commands not supported in Azure Redis Cache](#redis-commands-not-supported-in-azure-redis-cache) section.</span></span> <span data-ttu-id="c0d56-430">Aby uzyskać więcej informacji o poleceniach Redis, zobacz [http://redis.io/commands](http://redis.io/commands).</span><span class="sxs-lookup"><span data-stu-id="c0d56-430">For more information about Redis commands, see [http://redis.io/commands](http://redis.io/commands).</span></span>
> 
> 

<span data-ttu-id="c0d56-431">Aby uzyskać dostęp do konsoli Redis, kliknij przycisk **konsoli** z **pamięci podręcznej Redis** bloku.</span><span class="sxs-lookup"><span data-stu-id="c0d56-431">To access the Redis Console, click **Console** from the **Redis Cache** blade.</span></span>

![Redis konsoli](./media/cache-configure/redis-console-menu.png)

<span data-ttu-id="c0d56-433">Aby wystawić poleceń w odniesieniu do wystąpienia pamięci podręcznej, po prostu wpisz odpowiedniego polecenia do konsoli.</span><span class="sxs-lookup"><span data-stu-id="c0d56-433">To issue commands against your cache instance, simply type the desired command into the console.</span></span>

![Redis konsoli](./media/cache-configure/redis-console.png)


### <a name="using-the-redis-console-with-a-premium-clustered-cache"></a><span data-ttu-id="c0d56-435">Za pomocą konsoli Redis z premium w klastrze pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="c0d56-435">Using the Redis Console with a premium clustered cache</span></span>

<span data-ttu-id="c0d56-436">Gdy za pomocą konsoli Redis z premium w klastrze pamięci podręcznej, można wydać polecenia jednego niezależnego fragmentu pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="c0d56-436">When using the Redis Console with a premium clustered cache, you can issue commands to a single shard of the cache.</span></span> <span data-ttu-id="c0d56-437">Można wydać polecenie do określonych niezależnego fragmentu, najpierw połączyć się z odpowiednią niezależnego fragmentu, klikając selektor niezależnego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="c0d56-437">To issue a command to a specific shard, first connect to the desired shard by clicking it on the shard picker.</span></span>

![Redis konsoli](./media/cache-configure/redis-console-premium-cluster.png)

<span data-ttu-id="c0d56-439">Jeśli użytkownik spróbuje uzyskać dostępu do klucza przechowywanego w różnych niezależnych od połączonych niezależnego fragmentu, pojawi się komunikat o błędzie podobny do następującego.</span><span class="sxs-lookup"><span data-stu-id="c0d56-439">If you attempt to access a key that is stored in a different shard than the connected shard, you receive an error message similar to the following message.</span></span>

```
shard1>get myKey
(error) MOVED 866 13.90.202.154:13000 (shard 0)
```

<span data-ttu-id="c0d56-440">W poprzednim przykładzie niezależnego fragmentu 1 jest wybrany niezależnego fragmentu, ale `myKey` znajduje się w niezależnych 0, co wynika z `(shard 0)` części komunikatu o błędzie.</span><span class="sxs-lookup"><span data-stu-id="c0d56-440">In the previous example, shard 1 is the selected shard, but `myKey` is located in shard 0, as indicated by the `(shard 0)` portion of the error message.</span></span> <span data-ttu-id="c0d56-441">W tym przykładzie, aby uzyskać dostęp do `myKey`wybierz niezależnego fragmentu 0 za pomocą selektora niezależnego fragmentu, a następnie wystawiania odpowiedniego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c0d56-441">In this example, to access `myKey`, select shard 0 using the shard picker, and then issue the desired command.</span></span>


## <a name="move-your-cache-to-a-new-subscription"></a><span data-ttu-id="c0d56-442">Przenieś pamięć podręczną na nową subskrypcję</span><span class="sxs-lookup"><span data-stu-id="c0d56-442">Move your cache to a new subscription</span></span>
<span data-ttu-id="c0d56-443">Pamięć podręczną można przenieść do nowej subskrypcji, klikając **Przenieś**.</span><span class="sxs-lookup"><span data-stu-id="c0d56-443">You can move your cache to a new subscription by clicking **Move**.</span></span>

![Przenieś pamięci podręcznej Redis](./media/cache-configure/redis-cache-move.png)

<span data-ttu-id="c0d56-445">Aby uzyskać informacje na przenoszenie zasobów między grupami zasobów do innej i z jedną subskrypcję do innego, zobacz [przenoszenia zasobów do nowej grupy zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c0d56-445">For information on moving resources from one resource group to another, and from one subscription to another, see [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0d56-446">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c0d56-446">Next steps</span></span>
* <span data-ttu-id="c0d56-447">Aby uzyskać więcej informacji na temat pracy z pamięci podręcznej Redis poleceń, zobacz [jak uruchomić polecenia Redis?](cache-faq.md#how-can-i-run-redis-commands)</span><span class="sxs-lookup"><span data-stu-id="c0d56-447">For more information on working with Redis commands, see [How can I run Redis commands?](cache-faq.md#how-can-i-run-redis-commands)</span></span>

