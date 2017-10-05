---
title: "Przegląd kondycji zasobów platformy Azure | Dokumentacja firmy Microsoft"
description: "Przegląd kondycji zasobów platformy Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: d54979995ca97a70ba92c64915b919da09f548ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="fa6db-103">Przegląd kondycji zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fa6db-103">Azure resource health overview</span></span>
 
<span data-ttu-id="fa6db-104">Usługa Resource Health ułatwia diagnozowanie i uzyskanie pomocy technicznej, gdy problem z platformą Azure ma wpływ na zasoby.</span><span class="sxs-lookup"><span data-stu-id="fa6db-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="fa6db-105">Informuje o bieżącej i wcześniejszej kondycji zasobów oraz pomaga uniknąć problemów.</span><span class="sxs-lookup"><span data-stu-id="fa6db-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="fa6db-106">Usługa Resource Health oferuje pomoc techniczną w przypadku problemów z usługą platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6db-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="fa6db-107">Podczas gdy [stan Azure](https://status.azure.com) informuje o problemów dotyczących usługi, które mają wpływ na szerokiego zakresu klientów platformy Azure, kondycja zasobu zawiera spersonalizowane pulpit nawigacyjny kondycji zasobów.</span><span class="sxs-lookup"><span data-stu-id="fa6db-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span></span> <span data-ttu-id="fa6db-108">Kondycja zasobów zawiera cały czas, który zasoby były niedostępne w przeszłości z powodu problemów dotyczących usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6db-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span></span> <span data-ttu-id="fa6db-109">Upraszcza można łatwiej zrozumieć, jeśli zostało naruszone umowy dotyczącej poziomu usług.</span><span class="sxs-lookup"><span data-stu-id="fa6db-109">This makes it simple for you to understand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="fa6db-110">Co to jest uznawany za zasobu i jak kondycja zasobów decyduje o tym, jeśli zasób jest uszkodzony lub nie?</span><span class="sxs-lookup"><span data-stu-id="fa6db-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="fa6db-111">Zasób jest wystąpieniem typu zasobu oferowane przez usługę Azure za pomocą usługi Azure Resource Manager, na przykład: maszynę wirtualną, aplikacji sieci web lub bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="fa6db-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="fa6db-112">Kondycja zasobów polega na sygnały emitowane przez różne usługi platformy Azure do oceny, czy zasób jest uszkodzony lub nie.</span><span class="sxs-lookup"><span data-stu-id="fa6db-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span></span> <span data-ttu-id="fa6db-113">Jeśli zasób jest zła, kondycja zasobu analizuje dodatkowych informacji w celu ustalenia źródła problemu.</span><span class="sxs-lookup"><span data-stu-id="fa6db-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span></span> <span data-ttu-id="fa6db-114">Identyfikuje również akcje Microsoft trwa do rozwiązania problemu lub jakie akcje można wykonać w celu rozwiązania przyczynę problemu.</span><span class="sxs-lookup"><span data-stu-id="fa6db-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span></span> 

<span data-ttu-id="fa6db-115">Zapoznaj się z pełną listą typów zasobów i kontroli kondycji w [kondycji zasobów platformy Azure](resource-health-checks-resource-types.md) dodatkowe szczegóły dotyczące sposób jest oceny kondycji.</span><span class="sxs-lookup"><span data-stu-id="fa6db-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="fa6db-116">Dostarczone przez kondycji zasobów stan kondycji</span><span class="sxs-lookup"><span data-stu-id="fa6db-116">Health status provided by resource health</span></span>
<span data-ttu-id="fa6db-117">Kondycja zasobu jest jednym z następujących stanów:</span><span class="sxs-lookup"><span data-stu-id="fa6db-117">The health of a resource is one of the following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="fa6db-118">Dostępna</span><span class="sxs-lookup"><span data-stu-id="fa6db-118">Available</span></span>
<span data-ttu-id="fa6db-119">Usługa wykryła nie wszystkie zdarzenia wpływające na kondycję zasobu.</span><span class="sxs-lookup"><span data-stu-id="fa6db-119">The service has not detected any events impacting the health of the resource.</span></span> <span data-ttu-id="fa6db-120">W przypadkach, gdzie zasobu odzyskał sprawność po nieplanowanych przestojów w ciągu ostatnich 24 godzin zostanie wyświetlona **ostatnio odzyskana** powiadomień.</span><span class="sxs-lookup"><span data-stu-id="fa6db-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span></span>

![Maszyna wirtualna zasobów kondycji dostępności](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="fa6db-122">Niedostępne</span><span class="sxs-lookup"><span data-stu-id="fa6db-122">Unavailable</span></span>
<span data-ttu-id="fa6db-123">Usługa wykryła trwającą platformy lub zdarzenia-platforma wpływające na kondycję zasobu.</span><span class="sxs-lookup"><span data-stu-id="fa6db-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="fa6db-124">Zdarzenia platformy</span><span class="sxs-lookup"><span data-stu-id="fa6db-124">Platform events</span></span>
<span data-ttu-id="fa6db-125">Te zdarzenia są wyzwalane przez kilka składników infrastruktury platformy Azure i obejmują zarówno zaplanowanych akcji, takich jak planowanej konserwacji i nieoczekiwane zdarzenia, takie jak ponowne uruchomienie komputera hosta nieplanowane.</span><span class="sxs-lookup"><span data-stu-id="fa6db-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="fa6db-126">Kondycja zasobów zawiera dodatkowe szczegóły dotyczące zdarzeń, proces odzyskiwania i umożliwia się z pomocą techniczną, nawet jeśli nie masz aktywnych pomocy technicznej umowy firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="fa6db-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span></span>

![Zasób kondycji niedostępny maszyny wirtualnej z powodu zdarzenia platformy](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="fa6db-128">Zdarzenia non-platformy</span><span class="sxs-lookup"><span data-stu-id="fa6db-128">Non-Platform events</span></span>
<span data-ttu-id="fa6db-129">Te zdarzenia są wyzwalane przez akcje wykonywane przez użytkowników, na przykład zatrzymanie maszyny wirtualnej lub osiągnięciu maksymalnej liczby połączeń z pamięcią podręczną Redis.</span><span class="sxs-lookup"><span data-stu-id="fa6db-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span></span>

![Zasób kondycji niedostępny maszyny wirtualnej z powodu zdarzenia z systemem innym niż platformy](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="fa6db-131">Nieznany</span><span class="sxs-lookup"><span data-stu-id="fa6db-131">Unknown</span></span>
<span data-ttu-id="fa6db-132">Ten stan kondycji wskazuje, że kondycja zasobu nie otrzymano informacji na temat tego zasobu na więcej niż 10 minut.</span><span class="sxs-lookup"><span data-stu-id="fa6db-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="fa6db-133">Gdy ten stan nie jest oznaczenie ostateczne stanu zasobu, jest ważne dane w proces rozwiązywania problemów:</span><span class="sxs-lookup"><span data-stu-id="fa6db-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span></span>
* <span data-ttu-id="fa6db-134">Jeśli zasób działa zgodnie z oczekiwaniami stan zasobu zostaną zaktualizowane na dostępne po kilku minutach.</span><span class="sxs-lookup"><span data-stu-id="fa6db-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span></span>
* <span data-ttu-id="fa6db-135">Jeśli występują problemy z zasobem, stan kondycji nieznany może sugerują, że zasób jest wpływ zdarzenie w platformie.</span><span class="sxs-lookup"><span data-stu-id="fa6db-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span></span>

![Nieznany maszyny wirtualnej kondycji zasobów](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="fa6db-137">Niepoprawny stan raportu</span><span class="sxs-lookup"><span data-stu-id="fa6db-137">Report an incorrect status</span></span>
<span data-ttu-id="fa6db-138">Jeśli w dowolnym momencie uważasz bieżący stan kondycji jest niepoprawny, możesz można Daj nam znać, klikając **zgłoszenia stanu kondycji niepoprawne**.</span><span class="sxs-lookup"><span data-stu-id="fa6db-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="fa6db-139">W przypadkach, w których ma wpływ Azure problem, firma Microsoft zachęca się z pomocą techniczną w bloku kondycji zasobów.</span><span class="sxs-lookup"><span data-stu-id="fa6db-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span></span> 

![Kondycja zasobu raportu niepoprawny stan.](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="fa6db-141">Informacje historyczne</span><span class="sxs-lookup"><span data-stu-id="fa6db-141">Historical Information</span></span>
<span data-ttu-id="fa6db-142">Dostęp do danych historycznych kondycji do 14 dni, klikając **wyświetlanie historii** w bloku kondycji zasobów.</span><span class="sxs-lookup"><span data-stu-id="fa6db-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span></span> 

![Kondycja zasobów historii raportu](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="fa6db-144">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="fa6db-144">Getting started</span></span>
<span data-ttu-id="fa6db-145">Aby otworzyć kondycja zasobów dla jednego zasobu</span><span class="sxs-lookup"><span data-stu-id="fa6db-145">To open Resource health for one resource</span></span>
1.  <span data-ttu-id="fa6db-146">Zaloguj się do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6db-146">Sign in into the Azure portal.</span></span>
2.  <span data-ttu-id="fa6db-147">Przejdź do zasobu.</span><span class="sxs-lookup"><span data-stu-id="fa6db-147">Navigate to your resource.</span></span>
3.  <span data-ttu-id="fa6db-148">W menu zasobów znajdujący się po lewej stronie, kliknij przycisk **kondycja zasobów**.</span><span class="sxs-lookup"><span data-stu-id="fa6db-148">In the resource menu located in the left-hand side, click **Resource health**.</span></span>

![Otwórz kondycja zasobów z bloku zasobów](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="fa6db-150">Kondycja zasobów można również uzyskać, klikając **więcej usług**i wpisując **kondycja zasobów** w polu tekstowym filtru, aby otworzyć **Pomoc i obsługa techniczna** bloku.</span><span class="sxs-lookup"><span data-stu-id="fa6db-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span></span> <span data-ttu-id="fa6db-151">Na koniec kliknij [ **kondycja zasobów**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="fa6db-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Otwórz z usługi więcej kondycja zasobów](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="fa6db-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa6db-153">Next steps</span></span>

<span data-ttu-id="fa6db-154">Wyewidencjonuj tych zasobów, aby dowiedzieć się więcej na temat kondycji zasobów:</span><span class="sxs-lookup"><span data-stu-id="fa6db-154">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="fa6db-155">Typy zasobów i kondycji sprawdza w kondycji zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fa6db-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="fa6db-156">Często zadawane pytania dotyczące kondycji zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fa6db-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




