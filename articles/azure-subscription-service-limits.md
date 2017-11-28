---
title: "Subskrypcja aaaAzure limity i przydziały | Dokumentacja firmy Microsoft"
description: "Zawiera listę typowych subskrypcji platformy Azure i ograniczenia usługi, przydziały i ograniczenia. W tym informacji na temat sposobu tooincrease ogranicza wraz z maksymalne wartości."
services: 
documentationcenter: 
author: rothja
manager: jeffreyg
editor: 
tags: billing
ms.assetid: 60d848f9-ff26-496e-a5ec-ccf92ad7d125
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: byvinyal
ms.openlocfilehash: a754d56124520791254ab8f1729808f0750ff222
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-service-limits-quotas-and-constraints"></a><span data-ttu-id="10650-104">Limity subskrypcji i usługi Azure, przydziały i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="10650-104">Azure subscription and service limits, quotas, and constraints</span></span>
<span data-ttu-id="10650-105">Ten dokument przedstawia niektóre z najczęściej limity Microsoft Azure hello, nazywane również przydziałów.</span><span class="sxs-lookup"><span data-stu-id="10650-105">This document lists some of hello most common Microsoft Azure limits, which are also sometimes called quotas.</span></span> <span data-ttu-id="10650-106">Ten dokument obecnie nie obejmuje wszystkich usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10650-106">This document doesn't currently cover all Azure services.</span></span> <span data-ttu-id="10650-107">Wraz z upływem czasu hello zostaną rozwinięte i aktualizacji listy toocover więcej hello platformy.</span><span class="sxs-lookup"><span data-stu-id="10650-107">Over time, hello list will be expanded and updated toocover more of hello platform.</span></span>

<span data-ttu-id="10650-108">Odwiedź stronę [omówienie cennik usługi Azure](https://azure.microsoft.com/pricing/) toolearn więcej informacji na temat cennik platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10650-108">Please visit [Azure Pricing Overview](https://azure.microsoft.com/pricing/) toolearn more about Azure pricing.</span></span> <span data-ttu-id="10650-109">Istnieje, można oszacować koszty przy użyciu hello [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/) lub poprzez odwiedzenie hello szczegóły cennikiem usługi (na przykład [maszyn wirtualnych systemu Windows](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span><span class="sxs-lookup"><span data-stu-id="10650-109">There, you can estimate your costs using hello [Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) or by visiting hello pricing details page for a service (for example, [Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/#Windows)).</span></span> <span data-ttu-id="10650-110">Dla toohelp wskazówki dotyczące zarządzania kosztów, zobacz [uniknąć kosztów nieoczekiwany rozliczenia Azure i kosztów zarządzania](billing/billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="10650-110">For tips toohelp manage your costs, see [Prevent unexpected costs with Azure billing and cost management](billing/billing-getting-started.md).</span></span>

> [!NOTE]
> <span data-ttu-id="10650-111">Jeśli chcesz tooraise hello limit przydziału powyżej hello **domyślny Limit**, [otwarcia żądania pomocy technicznej online klienta bez dodatkowych opłat](azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="10650-111">If you want tooraise hello limit or quota above hello **Default Limit**, [open an online customer support request at no charge](azure-supportability/resource-manager-core-quotas-request.md).</span></span> <span data-ttu-id="10650-112">Witaj limity nie można zgłosić powyżej hello **maksymalny Limit** wartość pokazana w hello następujące tabele.</span><span class="sxs-lookup"><span data-stu-id="10650-112">hello limits can't be raised above hello **Maximum Limit** value shown in hello following tables.</span></span> <span data-ttu-id="10650-113">W przypadku nie **maksymalny Limit** kolumny, a następnie hello zasobów nie ma regulowany limity.</span><span class="sxs-lookup"><span data-stu-id="10650-113">If there is no **Maximum Limit** column, then hello resource doesn't have adjustable limits.</span></span> 
> 
> <span data-ttu-id="10650-114">Bezpłatna wersja próbna subskrypcji nie kwalifikują się do limitu lub zwiększenie limitu przydziału.</span><span class="sxs-lookup"><span data-stu-id="10650-114">Free Trial subscriptions are not eligible for limit or quota increases.</span></span> <span data-ttu-id="10650-115">Jeśli masz bezpłatnej wersji próbnej, możesz uaktualnić tooa [płatność za rzeczywiste użycie](https://azure.microsoft.com/offers/ms-azr-0003p/) subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="10650-115">If you have a Free Trial, you can upgrade tooa [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) subscription.</span></span> <span data-ttu-id="10650-116">Aby uzyskać więcej informacji, zobacz [uaktualnienia bezpłatna wersja próbna platformy Azure tooPay jako — użytkownik-przenośna](billing/billing-upgrade-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="10650-116">For more information, see [Upgrade Azure Free Trial tooPay-As-You-Go](billing/billing-upgrade-azure-subscription.md).</span></span>
> 

## <a name="limits-and-hello-azure-resource-manager"></a><span data-ttu-id="10650-117">Ograniczenia i hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10650-117">Limits and hello Azure Resource Manager</span></span>
<span data-ttu-id="10650-118">Teraz jest możliwe toocombine wielu zasobów platformy Azure w tooa pojedyncza grupa zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="10650-118">It is now possible toocombine multiple Azure resources in tooa single Azure Resource Group.</span></span> <span data-ttu-id="10650-119">Podczas korzystania z grup zasobów, ograniczeń, które raz były globalne stanie zarządzaną na poziomie regionalnym z hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10650-119">When using Resource Groups, limits that once were global become managed at a regional level with hello Azure Resource Manager.</span></span> <span data-ttu-id="10650-120">Aby uzyskać więcej informacji na temat grup zasobów platformy Azure, zobacz [Omówienie usługi Azure Resource Manager](azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="10650-120">For more information about Azure Resource Groups, see [Azure Resource Manager overview](azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="10650-121">W granicach hello poniżej nowej tabeli został dodany tooreflect różnice w granicach przy użyciu hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10650-121">In hello limits below, a new table has been added tooreflect any differences in limits when using hello Azure Resource Manager.</span></span> <span data-ttu-id="10650-122">Na przykład istnieje **limity subskrypcji** tabeli i **limity subskrypcji — usługi Azure Resource Manager** tabeli.</span><span class="sxs-lookup"><span data-stu-id="10650-122">For example, there is a **Subscription Limits** table and a **Subscription Limits - Azure Resource Manager** table.</span></span> <span data-ttu-id="10650-123">Gdy limit dotyczy scenariuszy tooboth, jego jest wyświetlana tylko w pierwszej tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="10650-123">When a limit applies tooboth scenarios, it is only shown in hello first table.</span></span> <span data-ttu-id="10650-124">O ile nie wskazano inaczej, limity są globalne we wszystkich regionach.</span><span class="sxs-lookup"><span data-stu-id="10650-124">Unless otherwise indicated, limits are global across all regions.</span></span>

> [!NOTE]
> <span data-ttu-id="10650-125">Jest ważne tooemphasize przydziałów dla zasobów w grupach zasobów platformy Azure są na regionem dostępny dla Twojej subskrypcji i nie są na subskrypcji, są hello usługi zarządzania przydziałów.</span><span class="sxs-lookup"><span data-stu-id="10650-125">It is important tooemphasize that quotas for resources in Azure Resource Groups are per-region accessible by your subscription, and are not per-subscription, as hello service management quotas are.</span></span> <span data-ttu-id="10650-126">Na przykład użyjmy podstawowej przydziałów.</span><span class="sxs-lookup"><span data-stu-id="10650-126">Let's use core quotas as an example.</span></span> <span data-ttu-id="10650-127">Jeśli potrzebujesz toorequest Zwiększ limit przydziału z obsługą rdzeni, jak należy toodecide wiele rdzeni zostanie mają toouse, w których regionach, a następnie określone żądanie dla grupy zasobów platformy Azure podstawowe przydziały hello kwoty i regionów, które mają.</span><span class="sxs-lookup"><span data-stu-id="10650-127">If you need toorequest a quota increase with support for cores, you need toodecide how many cores you want toouse in which regions, and then make a specific request for Azure Resource Group core quotas for hello amounts and regions that you want.</span></span> <span data-ttu-id="10650-128">W związku z tym jeśli potrzebujesz toouse 30 rdzenie w toorun Europa aplikacji w szczególności należy zażądać 30 rdzeni Europa Zachodnia.</span><span class="sxs-lookup"><span data-stu-id="10650-128">Therefore, if you need toouse 30 cores in West Europe toorun your application there; you should specifically request 30 cores in West Europe.</span></span> <span data-ttu-id="10650-129">Ale nie ma limit przydziału rdzeni zwiększyć w innym regionie — tylko Europa Zachodnia, będzie miał hello 30-core przydziału.</span><span class="sxs-lookup"><span data-stu-id="10650-129">But you will not have a core quota increase in any other region -- only West Europe will have hello 30-core quota.</span></span>
> <!-- -->
> <span data-ttu-id="10650-130">W związku z tym użytkownik może być przydatne tooconsider podejmowania decyzji o elementach przydziałami grupy zasobów platformy Azure, należy toobe dla obciążenia w dowolnej jeden region, a żądanie które kwota w każdym regionie, w którym rozważane jest wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="10650-130">As a result, you may find it useful tooconsider deciding what your Azure Resource Group quotas need toobe for your workload in any one region, and request that amount in each region into which you are considering deployment.</span></span> <span data-ttu-id="10650-131">Zobacz [Rozwiązywanie problemów dotyczących wdrożenia](resource-manager-common-deployment-errors.md) Aby uzyskać dodatkową pomoc odnajdywania bieżącego przydziałami dla konkretnych regionów.</span><span class="sxs-lookup"><span data-stu-id="10650-131">See [troubleshooting deployment issues](resource-manager-common-deployment-errors.md) for more help discovering your current quotas for specific regions.</span></span>
> 
> 

## <a name="service-specific-limits"></a><span data-ttu-id="10650-132">Limity specyficzne dla usługi</span><span class="sxs-lookup"><span data-stu-id="10650-132">Service-specific limits</span></span>
* [<span data-ttu-id="10650-133">Usługa Active Directory</span><span class="sxs-lookup"><span data-stu-id="10650-133">Active Directory</span></span>](#active-directory-limits)
* [<span data-ttu-id="10650-134">Zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="10650-134">API Management</span></span>](#api-management-limits)
* [<span data-ttu-id="10650-135">App Service</span><span class="sxs-lookup"><span data-stu-id="10650-135">App Service</span></span>](#app-service-limits)
* [<span data-ttu-id="10650-136">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="10650-136">Application Gateway</span></span>](#application-gateway-limits)
* [<span data-ttu-id="10650-137">Usługa Application Insights</span><span class="sxs-lookup"><span data-stu-id="10650-137">Application Insights</span></span>](#application-insights-limits)
* [<span data-ttu-id="10650-138">Automatyzacja</span><span class="sxs-lookup"><span data-stu-id="10650-138">Automation</span></span>](#automation-limits)
* [<span data-ttu-id="10650-139">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="10650-139">Azure Cosmos DB</span></span>](#azure-cosmos-db-limits)
* [<span data-ttu-id="10650-140">Usługi Azure Event siatki</span><span class="sxs-lookup"><span data-stu-id="10650-140">Azure Event Grid</span></span>](#azure-event-grid-limits)
* [<span data-ttu-id="10650-141">Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="10650-141">Azure Redis Cache</span></span>](#azure-redis-cache-limits)
* [<span data-ttu-id="10650-142">Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="10650-142">Azure RemoteApp</span></span>](#azure-remoteapp-limits)
* [<span data-ttu-id="10650-143">Tworzenie kopii zapasowych</span><span class="sxs-lookup"><span data-stu-id="10650-143">Backup</span></span>](#backup-limits)
* [<span data-ttu-id="10650-144">Batch</span><span class="sxs-lookup"><span data-stu-id="10650-144">Batch</span></span>](#batch-limits)
* [<span data-ttu-id="10650-145">Usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="10650-145">BizTalk Services</span></span>](#biztalk-services-limits)
* [<span data-ttu-id="10650-146">CDN</span><span class="sxs-lookup"><span data-stu-id="10650-146">CDN</span></span>](#cdn-limits)
* [<span data-ttu-id="10650-147">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="10650-147">Cloud Services</span></span>](#cloud-services-limits)
* [<span data-ttu-id="10650-148">Container Instances</span><span class="sxs-lookup"><span data-stu-id="10650-148">Container Instances</span></span>](#container-instances-limits)
* [<span data-ttu-id="10650-149">Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="10650-149">Data Factory</span></span>](#data-factory-limits)
* [<span data-ttu-id="10650-150">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="10650-150">Data Lake Analytics</span></span>](#data-lake-analytics-limits)
* [<span data-ttu-id="10650-151">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="10650-151">Data Lake Store</span></span>](#data-lake-store-limits)
* [<span data-ttu-id="10650-152">DNS</span><span class="sxs-lookup"><span data-stu-id="10650-152">DNS</span></span>](#dns-limits)
* [<span data-ttu-id="10650-153">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="10650-153">Event Hubs</span></span>](#event-hubs-limits)
* [<span data-ttu-id="10650-154">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="10650-154">IoT Hub</span></span>](#iot-hub-limits)
* [<span data-ttu-id="10650-155">Usługa Key Vault</span><span class="sxs-lookup"><span data-stu-id="10650-155">Key Vault</span></span>](#key-vault-limits)
* [<span data-ttu-id="10650-156">Zaloguj się Analytics / Operational Insights</span><span class="sxs-lookup"><span data-stu-id="10650-156">Log Analytics / Operational Insights</span></span>](#log-analytics-limits)
* [<span data-ttu-id="10650-157">Media Services</span><span class="sxs-lookup"><span data-stu-id="10650-157">Media Services</span></span>](#media-services-limits)
* [<span data-ttu-id="10650-158">Wykorzystanie urządzeń przenośnych</span><span class="sxs-lookup"><span data-stu-id="10650-158">Mobile Engagement</span></span>](#mobile-engagement-limits)
* [<span data-ttu-id="10650-159">Usługi mobilne</span><span class="sxs-lookup"><span data-stu-id="10650-159">Mobile Services</span></span>](#mobile-services-limits)
* [<span data-ttu-id="10650-160">Monitorowanie</span><span class="sxs-lookup"><span data-stu-id="10650-160">Monitor</span></span>](#monitor-limits)
* [<span data-ttu-id="10650-161">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="10650-161">Multi-Factor Authentication</span></span>](#multi-factor-authentication)
* [<span data-ttu-id="10650-162">Sieć</span><span class="sxs-lookup"><span data-stu-id="10650-162">Networking</span></span>](#networking-limits)
* [<span data-ttu-id="10650-163">Obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="10650-163">Network Watcher</span></span>](#network-watcher-limits)
* [<span data-ttu-id="10650-164">Usługa Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="10650-164">Notification Hub Service</span></span>](#notification-hub-service-limits)
* [<span data-ttu-id="10650-165">Grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="10650-165">Resource Group</span></span>](#resource-group-limits)
* [<span data-ttu-id="10650-166">Scheduler</span><span class="sxs-lookup"><span data-stu-id="10650-166">Scheduler</span></span>](#scheduler-limits)
* [<span data-ttu-id="10650-167">Wyszukiwanie</span><span class="sxs-lookup"><span data-stu-id="10650-167">Search</span></span>](#search-limits)
* [<span data-ttu-id="10650-168">Service Bus</span><span class="sxs-lookup"><span data-stu-id="10650-168">Service Bus</span></span>](#service-bus-limits)
* [<span data-ttu-id="10650-169">Site Recovery</span><span class="sxs-lookup"><span data-stu-id="10650-169">Site Recovery</span></span>](#site-recovery-limits)
* [<span data-ttu-id="10650-170">SQL Database</span><span class="sxs-lookup"><span data-stu-id="10650-170">SQL Database</span></span>](#sql-database-limits)
* [<span data-ttu-id="10650-171">Storage</span><span class="sxs-lookup"><span data-stu-id="10650-171">Storage</span></span>](#storage-limits)
* [<span data-ttu-id="10650-172">StorSimple System</span><span class="sxs-lookup"><span data-stu-id="10650-172">StorSimple System</span></span>](#storsimple-system-limits)
* [<span data-ttu-id="10650-173">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10650-173">Stream Analytics</span></span>](#stream-analytics-limits)
* [<span data-ttu-id="10650-174">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="10650-174">Subscription</span></span>](#subscription-limits)
* [<span data-ttu-id="10650-175">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="10650-175">Traffic Manager</span></span>](#traffic-manager-limits)
* [<span data-ttu-id="10650-176">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="10650-176">Virtual Machines</span></span>](#virtual-machines-limits)
* [<span data-ttu-id="10650-177">Zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10650-177">Virtual Machine Scale Sets</span></span>](#virtual-machine-scale-sets-limits)

### <a name="subscription-limits"></a><span data-ttu-id="10650-178">Limity subskrypcji</span><span class="sxs-lookup"><span data-stu-id="10650-178">Subscription limits</span></span>
#### <a name="subscription-limits"></a><span data-ttu-id="10650-179">Limity subskrypcji</span><span class="sxs-lookup"><span data-stu-id="10650-179">Subscription limits</span></span>
[!INCLUDE [azure-subscription-limits](../includes/azure-subscription-limits.md)]

#### <a name="subscription-limits---azure-resource-manager"></a><span data-ttu-id="10650-180">Limity subskrypcji — usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10650-180">Subscription limits - Azure Resource Manager</span></span>
<span data-ttu-id="10650-181">Witaj następujące ograniczenia obowiązują w przypadku hello Azure Resource Manager i grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10650-181">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="10650-182">Ograniczenia, które nie zostały zmienione z hello Azure Resource Manager nie są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="10650-182">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="10650-183">Te limity można znaleźć w poprzedniej tabeli toohello.</span><span class="sxs-lookup"><span data-stu-id="10650-183">Please refer toohello previous table for those limits.</span></span>

<span data-ttu-id="10650-184">Aby uzyskać informacje na temat obsługi limity żądań Resource Manager, zobacz [ograniczania Resource Manager zażąda](resource-manager-request-limits.md).</span><span class="sxs-lookup"><span data-stu-id="10650-184">For information about handling limits on Resource Manager requests, see [Throttling Resource Manager requests](resource-manager-request-limits.md).</span></span>

[!INCLUDE [azure-subscription-limits-azure-resource-manager](../includes/azure-subscription-limits-azure-resource-manager.md)]

### <a name="resource-group-limits"></a><span data-ttu-id="10650-185">Limity grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="10650-185">Resource Group limits</span></span>
[!INCLUDE [azure-resource-groups-limits](../includes/azure-resource-groups-limits.md)]

### <a name="virtual-machines-limits"></a><span data-ttu-id="10650-186">Limity maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="10650-186">Virtual Machines limits</span></span>
#### <a name="virtual-machine-limits"></a><span data-ttu-id="10650-187">Limity maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10650-187">Virtual Machine limits</span></span>
[!INCLUDE [azure-virtual-machines-limits](../includes/azure-virtual-machines-limits.md)]

#### <a name="virtual-machines-limits---azure-resource-manager"></a><span data-ttu-id="10650-188">Maszyny wirtualne limity — usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10650-188">Virtual Machines limits - Azure Resource Manager</span></span>
<span data-ttu-id="10650-189">Witaj następujące ograniczenia obowiązują w przypadku hello Azure Resource Manager i grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10650-189">hello following limits apply when using hello Azure Resource Manager and Azure Resource Groups.</span></span> <span data-ttu-id="10650-190">Ograniczenia, które nie zostały zmienione z hello Azure Resource Manager nie są wymienione poniżej.</span><span class="sxs-lookup"><span data-stu-id="10650-190">Limits that have not changed with hello Azure Resource Manager are not listed below.</span></span> <span data-ttu-id="10650-191">Te limity można znaleźć w poprzedniej tabeli toohello.</span><span class="sxs-lookup"><span data-stu-id="10650-191">Please refer toohello previous table for those limits.</span></span>

[!INCLUDE [azure-virtual-machines-limits-azure-resource-manager](../includes/azure-virtual-machines-limits-azure-resource-manager.md)]

### <a name="virtual-machine-scale-sets-limits"></a><span data-ttu-id="10650-192">Limity zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10650-192">Virtual Machine Scale Sets limits</span></span>
[!INCLUDE [virtual-machine-scale-sets-limits](../includes/azure-virtual-machine-scale-sets-limits.md)]

### <a name="container-instances-limits"></a><span data-ttu-id="10650-193">Limity wystąpień kontenera</span><span class="sxs-lookup"><span data-stu-id="10650-193">Container Instances Limits</span></span>
[!INCLUDE [container-instances-limits](../includes/container-instances-limits.md)]

### <a name="networking-limits"></a><span data-ttu-id="10650-194">Limity sieci</span><span class="sxs-lookup"><span data-stu-id="10650-194">Networking limits</span></span>
[!INCLUDE [expressroute-limits](../includes/expressroute-limits.md)]

#### <a name="networking-limits"></a><span data-ttu-id="10650-195">Limity sieci</span><span class="sxs-lookup"><span data-stu-id="10650-195">Networking limits</span></span>
[!INCLUDE [azure-virtual-network-limits](../includes/azure-virtual-network-limits.md)]

#### <a name="application-gateway-limits"></a><span data-ttu-id="10650-196">Ogranicza bramy aplikacji</span><span class="sxs-lookup"><span data-stu-id="10650-196">Application Gateway limits</span></span>
[!INCLUDE [application-gateway-limits](../includes/application-gateway-limits.md)]

#### <a name="network-watcher-limits"></a><span data-ttu-id="10650-197">Ogranicza obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="10650-197">Network Watcher limits</span></span>
[!INCLUDE [network-watcher-limits](../includes/network-watcher-limits.md)]

#### <a name="traffic-manager-limits"></a><span data-ttu-id="10650-198">Limity Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="10650-198">Traffic Manager limits</span></span>
[!INCLUDE [traffic-manager-limits](../includes/traffic-manager-limits.md)]

#### <a name="dns-limits"></a><span data-ttu-id="10650-199">Limity DNS</span><span class="sxs-lookup"><span data-stu-id="10650-199">DNS limits</span></span>
[!INCLUDE [dns-limits](../includes/dns-limits.md)]

### <a name="storage-limits"></a><span data-ttu-id="10650-200">Limity magazynu</span><span class="sxs-lookup"><span data-stu-id="10650-200">Storage limits</span></span>
<span data-ttu-id="10650-201">Aby uzyskać więcej informacji na temat limitów konta magazynu, zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage/common/storage-scalability-targets.md).</span><span class="sxs-lookup"><span data-stu-id="10650-201">For additional details on storage account limits, see [Azure Storage Scalability and Performance Targets](storage/common/storage-scalability-targets.md).</span></span>
<!--like # storage accts --> 
#### <a name="storage-service-limits"></a><span data-ttu-id="10650-202">Ograniczenia usługi magazynu</span><span class="sxs-lookup"><span data-stu-id="10650-202">Storage Service limits</span></span>
[!INCLUDE [azure-storage-limits](../includes/azure-storage-limits.md)]

<!-- conceptual info about disk limits -- applies toounmanaged and managed -->
#### <a name="virtual-machine-disk-limits"></a><span data-ttu-id="10650-203">Limity dysku maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10650-203">Virtual machine disk limits</span></span> 
[!INCLUDE [azure-storage-limits-vm-disks](../includes/azure-storage-limits-vm-disks.md)]

<span data-ttu-id="10650-204">Zobacz [rozmiarów maszyn wirtualnych](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) dodatkowe szczegóły.</span><span class="sxs-lookup"><span data-stu-id="10650-204">See [Virtual machine sizes](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for additional details.</span></span>

#### <a name="managed-virtual-machine-disks"></a><span data-ttu-id="10650-205">Dyski zarządzane maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="10650-205">Managed virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-managed](../includes/azure-storage-limits-vm-disks-managed.md)]

#### <a name="unmanaged-virtual-machine-disks"></a><span data-ttu-id="10650-206">Dyski maszyny wirtualnej niezarządzanej</span><span class="sxs-lookup"><span data-stu-id="10650-206">Unmanaged virtual machine disks</span></span>

[!INCLUDE [azure-storage-limits-vm-disks-standard](../includes/azure-storage-limits-vm-disks-standard.md)]

[!INCLUDE [azure-storage-limits-vm-disks-premium](../includes/azure-storage-limits-vm-disks-premium.md)]

#### <a name="storage-resource-provider-limits"></a><span data-ttu-id="10650-207">Limity dostawcy zasobów magazynu</span><span class="sxs-lookup"><span data-stu-id="10650-207">Storage Resource Provider limits</span></span>
[!INCLUDE [azure-storage-limits-azure-resource-manager](../includes/azure-storage-limits-azure-resource-manager.md)]

### <a name="cloud-services-limits"></a><span data-ttu-id="10650-208">Limity usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="10650-208">Cloud Services limits</span></span>
[!INCLUDE [azure-cloud-services-limits](../includes/azure-cloud-services-limits.md)]

### <a name="app-service-limits"></a><span data-ttu-id="10650-209">Ograniczenia usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="10650-209">App Service limits</span></span>
<span data-ttu-id="10650-210">następujące Hello, który ogranicza usługi aplikacji obejmują limity dla aplikacji sieci Web, aplikacje mobilne, aplikacje API Apps i Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="10650-210">hello following App Service limits include limits for Web Apps, Mobile Apps, API Apps, and Logic Apps.</span></span>

[!INCLUDE [azure-websites-limits](../includes/azure-websites-limits.md)]

### <a name="scheduler-limits"></a><span data-ttu-id="10650-211">Limity harmonogramu</span><span class="sxs-lookup"><span data-stu-id="10650-211">Scheduler limits</span></span>
[!INCLUDE [scheduler-limits-table](../includes/scheduler-limits-table.md)]

### <a name="batch-limits"></a><span data-ttu-id="10650-212">Limity partii</span><span class="sxs-lookup"><span data-stu-id="10650-212">Batch limits</span></span>
[!INCLUDE [azure-batch-limits](../includes/azure-batch-limits.md)]

### <a name="biztalk-services-limits"></a><span data-ttu-id="10650-213">Limity usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="10650-213">BizTalk Services limits</span></span>
<span data-ttu-id="10650-214">Witaj poniższej tabeli przedstawiono hello limity dotyczące usług Biztalk Azure.</span><span class="sxs-lookup"><span data-stu-id="10650-214">hello following table shows hello limits for Azure Biztalk Services.</span></span>

[!INCLUDE [biztalk-services-service-limits](../includes/biztalk-services-service-limits.md)]

### <a name="azure-cosmos-db-limits"></a><span data-ttu-id="10650-215">Ogranicza Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="10650-215">Azure Cosmos DB limits</span></span>
<span data-ttu-id="10650-216">Azure DB rozwiązania Cosmos jest skali globalnej bazy danych, w którym przepływność i Magazyn może być skalowana toohandle niezależnie od aplikacja wymaga.</span><span class="sxs-lookup"><span data-stu-id="10650-216">Azure Cosmos DB is a global scale database in which throughput and storage can be scaled toohandle whatever your application requires.</span></span> <span data-ttu-id="10650-217">Jeśli masz pytania dotyczące skalowania hello Azure DB rozwiązania Cosmos dostarcza Wyślij e-mail tooaskcosmosdb@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="10650-217">If you have any questions about hello scale Azure Cosmos DB provides, please send email tooaskcosmosdb@microsoft.com.</span></span>

### <a name="mobile-engagement-limits"></a><span data-ttu-id="10650-218">Limity usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="10650-218">Mobile Engagement limits</span></span>
[!INCLUDE [azure-mobile-engagement-limits](../includes/azure-mobile-engagement-limits.md)]

### <a name="search-limits"></a><span data-ttu-id="10650-219">Limity wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="10650-219">Search limits</span></span>
<span data-ttu-id="10650-220">Warstw cenowych określają hello pojemności i limity usługi wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="10650-220">Pricing tiers determine hello capacity and limits of your search service.</span></span> <span data-ttu-id="10650-221">Warstwy obejmują:</span><span class="sxs-lookup"><span data-stu-id="10650-221">Tiers include:</span></span>

* <span data-ttu-id="10650-222">*Bezpłatne* usługę wielodostępną, współużytkowana z innymi subskrybenci platformy Azure, przeznaczonych do oceny i małych tworzenia projektów.</span><span class="sxs-lookup"><span data-stu-id="10650-222">*Free* multi-tenant service, shared with other Azure subscribers, intended for evaluation and small development projects.</span></span>
* <span data-ttu-id="10650-223">*Podstawowe* zapewnia dedykowany zasobów obliczeniowych obciążeń produkcyjnych na mniejszą skalę na zapasową replik toothree dla obciążeń zapytania wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="10650-223">*Basic* provides dedicated computing resources for production workloads at a smaller scale, with up toothree replicas for highly available query workloads.</span></span>
* <span data-ttu-id="10650-224">*Standardowa (S1, S2, S3, o wysokiej gęstości S3)* jest przeznaczony dla większych obciążeń produkcyjnych.</span><span class="sxs-lookup"><span data-stu-id="10650-224">*Standard (S1, S2, S3, S3 High Density)* is for larger production workloads.</span></span> <span data-ttu-id="10650-225">Wiele poziomów istnieć hello warstwy standardowa, w którym można wybrać konfiguracji zasobu, który najlepiej odpowiada Twoim profilu obciążenia.</span><span class="sxs-lookup"><span data-stu-id="10650-225">Multiple levels exist within hello standard tier so that you can choose a resource configuration that best matches your workload profile.</span></span>

<span data-ttu-id="10650-226">**Limity dla subskrypcji**</span><span class="sxs-lookup"><span data-stu-id="10650-226">**Limits per subscription**</span></span>

[!INCLUDE [azure-search-limits-per-subscription](../includes/azure-search-limits-per-subscription.md)]

<span data-ttu-id="10650-227">**Limity dla usługi wyszukiwania**</span><span class="sxs-lookup"><span data-stu-id="10650-227">**Limits per search service**</span></span>

[!INCLUDE [azure-search-limits-per-service](../includes/azure-search-limits-per-service.md)]

<span data-ttu-id="10650-228">toolearn więcej informacji na temat limitów na bardziej szczegółowym poziomie, takich jak rozmiar dokumentu, zapytania na sekundę, klucze żądań i odpowiedzi, zobacz [usługi limity w usłudze Azure Search](search/search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="10650-228">toolearn more about limits on a more granular level, such as document size, queries per second, keys, requests, and responses, see [Service limits in Azure Search](search/search-limits-quotas-capacity.md).</span></span>

### <a name="media-services-limits"></a><span data-ttu-id="10650-229">Limity usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="10650-229">Media Services limits</span></span>
[!INCLUDE [azure-mediaservices-limits](../includes/azure-mediaservices-limits.md)]

### <a name="cdn-limits"></a><span data-ttu-id="10650-230">Limity CDN</span><span class="sxs-lookup"><span data-stu-id="10650-230">CDN limits</span></span>
[!INCLUDE [cdn-limits](../includes/cdn-limits.md)]

### <a name="mobile-services-limits"></a><span data-ttu-id="10650-231">Limity usług Mobile Services</span><span class="sxs-lookup"><span data-stu-id="10650-231">Mobile Services limits</span></span>
[!INCLUDE [mobile-services-limits](../includes/mobile-services-limits.md)]

### <a name="monitor-limits"></a><span data-ttu-id="10650-232">Limity monitora</span><span class="sxs-lookup"><span data-stu-id="10650-232">Monitor limits</span></span>
[!INCLUDE [monitoring-limits](../includes/monitoring-limits.md)]

### <a name="notification-hub-service-limits"></a><span data-ttu-id="10650-233">Ograniczenia usługi Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="10650-233">Notification Hub Service limits</span></span>
[!INCLUDE [notification-hub-limits](../includes/notification-hub-limits.md)]

### <a name="event-hubs-limits"></a><span data-ttu-id="10650-234">Limity centra zdarzeń</span><span class="sxs-lookup"><span data-stu-id="10650-234">Event Hubs limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/event-hubs-limits.md)]

### <a name="service-bus-limits"></a><span data-ttu-id="10650-235">Limity usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="10650-235">Service Bus limits</span></span>
[!INCLUDE [azure-servicebus-limits](../includes/service-bus-quotas-table.md)]

### <a name="iot-hub-limits"></a><span data-ttu-id="10650-236">Centrum IoT limitami</span><span class="sxs-lookup"><span data-stu-id="10650-236">IoT Hub limits</span></span>
[!INCLUDE [azure-iothub-limits](../includes/iot-hub-limits.md)]

### <a name="data-factory-limits"></a><span data-ttu-id="10650-237">Limity fabryki danych</span><span class="sxs-lookup"><span data-stu-id="10650-237">Data Factory limits</span></span>
[!INCLUDE [azure-data-factory-limits](../includes/azure-data-factory-limits.md)]

### <a name="data-lake-analytics-limits"></a><span data-ttu-id="10650-238">Ogranicza usługi Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="10650-238">Data Lake Analytics limits</span></span>
[!INCLUDE [azure-data-lake-analytics-limits](../includes/azure-data-lake-analytics-limits.md)]

### <a name="data-lake-store-limits"></a><span data-ttu-id="10650-239">Limity usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="10650-239">Data Lake Store limits</span></span>
[!INCLUDE [azure-data-lake-store-limits](../includes/azure-data-lake-store-limits.md)]

### <a name="stream-analytics-limits"></a><span data-ttu-id="10650-240">Ogranicza usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="10650-240">Stream Analytics limits</span></span>
[!INCLUDE [stream-analytics-limits-table](../includes/stream-analytics-limits-table.md)]

### <a name="active-directory-limits"></a><span data-ttu-id="10650-241">Ogranicza usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="10650-241">Active Directory limits</span></span>
[!INCLUDE [AAD-service-limits](../includes/active-directory-service-limits-include.md)]

### <a name="azure-event-grid-limits"></a><span data-ttu-id="10650-242">Ogranicza Azure siatki zdarzeń</span><span class="sxs-lookup"><span data-stu-id="10650-242">Azure Event Grid limits</span></span>
[!INCLUDE [event-grid-limits](../includes/event-grid-limits.md)]

### <a name="azure-remoteapp-limits"></a><span data-ttu-id="10650-243">Ogranicza usługi Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="10650-243">Azure RemoteApp limits</span></span>
[!INCLUDE [azure-remoteapp-limits](../includes/azure-remoteapp-limits.md)]

### <a name="storsimple-system-limits"></a><span data-ttu-id="10650-244">Limity systemu StorSimple</span><span class="sxs-lookup"><span data-stu-id="10650-244">StorSimple System limits</span></span>
[!INCLUDE [storsimple-limits-table](../includes/storsimple-limits-table.md)]

### <a name="log-analytics-limits"></a><span data-ttu-id="10650-245">Ogranicza analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="10650-245">Log Analytics limits</span></span>
[!INCLUDE [operational-insights-limits](../includes/operational-insights-limits.md)]

### <a name="backup-limits"></a><span data-ttu-id="10650-246">Limity kopii zapasowej</span><span class="sxs-lookup"><span data-stu-id="10650-246">Backup limits</span></span>
[!INCLUDE [azure-backup-limits](../includes/azure-backup-limits.md)]

### <a name="site-recovery-limits"></a><span data-ttu-id="10650-247">Limity usługi Site Recovery</span><span class="sxs-lookup"><span data-stu-id="10650-247">Site Recovery limits</span></span>
[!INCLUDE [site-recovery-limits](../includes/site-recovery-limits.md)]

### <a name="application-insights-limits"></a><span data-ttu-id="10650-248">Application Insights limity</span><span class="sxs-lookup"><span data-stu-id="10650-248">Application Insights limits</span></span>
[!INCLUDE [application-insights-limits](../includes/application-insights-limits.md)]

### <a name="api-management-limits"></a><span data-ttu-id="10650-249">Zarządzanie interfejsami API limity</span><span class="sxs-lookup"><span data-stu-id="10650-249">API Management limits</span></span>
[!INCLUDE [api-management-service-limits](../includes/api-management-service-limits.md)]

### <a name="azure-redis-cache-limits"></a><span data-ttu-id="10650-250">Limity pamięci podręcznej Redis Azure</span><span class="sxs-lookup"><span data-stu-id="10650-250">Azure Redis Cache limits</span></span>
[!INCLUDE [redis-cache-service-limits](../includes/redis-cache-service-limits.md)]

### <a name="key-vault-limits"></a><span data-ttu-id="10650-251">Limity magazynu kluczy</span><span class="sxs-lookup"><span data-stu-id="10650-251">Key Vault limits</span></span>
[!INCLUDE [key-vault-limits](../includes/key-vault-limits.md)]

### <a name="multi-factor-authentication"></a><span data-ttu-id="10650-252">Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="10650-252">Multi-Factor Authentication</span></span>
[!INCLUDE [azure-mfa-service-limits](../includes/azure-mfa-service-limits.md)]

### <a name="automation-limits"></a><span data-ttu-id="10650-253">Limity automatyzacji</span><span class="sxs-lookup"><span data-stu-id="10650-253">Automation limits</span></span>
[!INCLUDE [automation-limits](../includes/azure-automation-service-limits.md)]

### <a name="sql-database-limits"></a><span data-ttu-id="10650-254">Limity bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="10650-254">SQL Database limits</span></span>
<span data-ttu-id="10650-255">Limitów bazy danych SQL, zobacz [limity zasobów bazy danych SQL](sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="10650-255">For SQL Database limits, see [SQL Database Resource Limits](sql-database/sql-database-resource-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="10650-256">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="10650-256">See also</span></span>
[<span data-ttu-id="10650-257">Opis ograniczeń Azure i zwiększa</span><span class="sxs-lookup"><span data-stu-id="10650-257">Understanding Azure Limits and Increases</span></span>](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/)

[<span data-ttu-id="10650-258">Maszyny wirtualnej i rozmiary usługi chmury dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="10650-258">Virtual Machine and Cloud Service Sizes for Azure</span></span>](virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="10650-259">Rozmiary dla usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="10650-259">Sizes for Cloud Services</span></span>](cloud-services/cloud-services-sizes-specs.md)

