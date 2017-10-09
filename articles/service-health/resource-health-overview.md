---
title: "Przegląd kondycji zasobów aaaAzure | Dokumentacja firmy Microsoft"
description: "Przegląd kondycji zasobów platformy Azure"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="eb0f8-103">Przegląd kondycji zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eb0f8-103">Azure resource health overview</span></span>
 
<span data-ttu-id="eb0f8-104">Usługa Resource Health ułatwia diagnozowanie i uzyskanie pomocy technicznej, gdy problem z platformą Azure ma wpływ na zasoby.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="eb0f8-105">Informuje o hello kondycji do bieżących i starszych zasobów, a pomaga ograniczać problemy.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="eb0f8-106">Usługa Resource Health oferuje pomoc techniczną w przypadku problemów z usługą platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="eb0f8-107">Podczas gdy [stan Azure](https://status.azure.com) informuje o problemów dotyczących usługi, które mają wpływ na szerokiego zakresu klientów platformy Azure, kondycja zasobu zawiera spersonalizowane pulpit nawigacyjny kondycji hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="eb0f8-108">Kondycja zasobów zawiera zawsze hello zasoby były niedostępne w hello minął termin płatności tooAzure problemów dotyczących usługi.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="eb0f8-109">Dzięki temu proste dla toounderstand możesz Jeśli umowa SLA zostało naruszone.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="eb0f8-110">Co to jest uznawany za zasobu i jak kondycja zasobów decyduje o tym, jeśli zasób jest uszkodzony lub nie?</span><span class="sxs-lookup"><span data-stu-id="eb0f8-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="eb0f8-111">Zasób jest wystąpieniem typu zasobu oferowane przez usługę Azure za pomocą usługi Azure Resource Manager, na przykład: maszynę wirtualną, aplikacji sieci web lub bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="eb0f8-112">Kondycja zasobów polega na sygnały emitowane przez hello tooassess różnych usług platformy Azure, jeśli zasób jest uszkodzony lub nie.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="eb0f8-113">Jeśli zasób jest zła, kondycja zasobu analizuje dodatkowe informacje toodetermine hello źródłem problemu hello.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="eb0f8-114">Identyfikuje również akcje, które Microsoft trwa toofix hello problem lub akcji może zająć tooaddress hello spowodować hello problemu.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="eb0f8-115">Przejrzyj hello pełną listę typów zasobów i kondycji sprawdza [kondycji zasobów platformy Azure](resource-health-checks-resource-types.md) dodatkowe szczegóły dotyczące sposób jest oceny kondycji.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="eb0f8-116">Dostarczone przez kondycji zasobów stan kondycji</span><span class="sxs-lookup"><span data-stu-id="eb0f8-116">Health status provided by resource health</span></span>
<span data-ttu-id="eb0f8-117">Witaj kondycji zasobu jest jednym z hello następujące stany:</span><span class="sxs-lookup"><span data-stu-id="eb0f8-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="eb0f8-118">Dostępna</span><span class="sxs-lookup"><span data-stu-id="eb0f8-118">Available</span></span>
<span data-ttu-id="eb0f8-119">Usługa Hello nie wykrył wszelkie zdarzenia wpływające na kondycję hello hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="eb0f8-120">W przypadkach, gdzie zasobów hello odzyskał sprawność po nieplanowane przestoje podczas hello ostatnie 24 godziny, zobaczysz hello **ostatnio odzyskana** powiadomień.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![Maszyna wirtualna zasobów kondycji dostępności](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="eb0f8-122">Niedostępne</span><span class="sxs-lookup"><span data-stu-id="eb0f8-122">Unavailable</span></span>
<span data-ttu-id="eb0f8-123">usługi Hello wykrył trwającą platformy lub zdarzenia-platforma wpływające na kondycję hello hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="eb0f8-124">Zdarzenia platformy</span><span class="sxs-lookup"><span data-stu-id="eb0f8-124">Platform events</span></span>
<span data-ttu-id="eb0f8-125">Te zdarzenia są wyzwalane przez kilka składników hello infrastruktury platformy Azure i obejmują zarówno zaplanowanych akcji, takich jak planowanej konserwacji i nieoczekiwane zdarzenia, takie jak ponowne uruchomienie komputera hosta nieplanowane.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="eb0f8-126">Kondycja zasobów zawiera dodatkowe szczegóły dotyczące zdarzeń hello, proces odzyskiwania hello i umożliwia obsługę toocontact nawet, jeśli nie masz aktywnych pomocy technicznej umowy firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![Zasób kondycji niedostępny maszyny wirtualnej powodu tooplatform zdarzeń](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="eb0f8-128">Zdarzenia non-platformy</span><span class="sxs-lookup"><span data-stu-id="eb0f8-128">Non-Platform events</span></span>
<span data-ttu-id="eb0f8-129">Te zdarzenia są wyzwalane przez akcje wykonywane przez użytkowników, na przykład zatrzymanie maszyny wirtualnej lub osiągnięcia hello maksymalną liczbę połączeń tooa pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![Zasób kondycji niedostępny maszyny wirtualnej powodu zdarzenia toonon platformy](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="eb0f8-131">Nieznany</span><span class="sxs-lookup"><span data-stu-id="eb0f8-131">Unknown</span></span>
<span data-ttu-id="eb0f8-132">Ten stan kondycji wskazuje, że kondycja zasobu nie otrzymano informacji na temat tego zasobu na więcej niż 10 minut.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="eb0f8-133">Gdy ten stan nie jest oznaczenie ostateczne hello stanu zasobu hello, jest ważne dane w hello proces rozwiązywania problemów:</span><span class="sxs-lookup"><span data-stu-id="eb0f8-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="eb0f8-134">Jeśli zasobów hello jest uruchomiona jako oczekiwanego hello stan zasobu hello zaktualizuje tooAvailable po kilku minutach.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="eb0f8-135">Jeśli występują problemy z zasobem hello, hello stan kondycji nieznany może sugerują, że zasób hello jest wpływ zdarzenie platformy hello.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![Nieznany maszyny wirtualnej kondycji zasobów](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="eb0f8-137">Niepoprawny stan raportu</span><span class="sxs-lookup"><span data-stu-id="eb0f8-137">Report an incorrect status</span></span>
<span data-ttu-id="eb0f8-138">Jeśli w dowolnym momencie uważasz hello bieżący stan kondycji jest niepoprawny, możesz można Daj nam znać, klikając **zgłoszenia stanu kondycji niepoprawne**.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="eb0f8-139">W przypadkach, w których ma wpływ Azure problem, firma Microsoft zachęca obsługę toocontact za pomocą bloku kondycji zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![Kondycja zasobu raportu niepoprawny stan.](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="eb0f8-141">Informacje historyczne</span><span class="sxs-lookup"><span data-stu-id="eb0f8-141">Historical Information</span></span>
<span data-ttu-id="eb0f8-142">Można uzyskać się dane historyczne kondycji too14 dni, klikając **wyświetlanie historii** w bloku kondycji zasobów hello.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![Kondycja zasobów historii raportu](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="eb0f8-144">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="eb0f8-144">Getting started</span></span>
<span data-ttu-id="eb0f8-145">tooopen kondycja zasobów dla jednego zasobu</span><span class="sxs-lookup"><span data-stu-id="eb0f8-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="eb0f8-146">Zaloguj się do hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="eb0f8-147">Przejdź tooyour zasobów.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="eb0f8-148">W menu zasobów hello znajduje się w lewej hello, kliknij przycisk **kondycja zasobów**.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![Otwórz kondycja zasobów z bloku zasobów](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="eb0f8-150">Kondycja zasobów można również uzyskać, klikając **więcej usług**i wpisując **kondycja zasobów** w hello tooopen pole tekstowe filtru **Pomoc i obsługa techniczna** bloku.</span><span class="sxs-lookup"><span data-stu-id="eb0f8-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="eb0f8-151">Na koniec kliknij [ **kondycja zasobów**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span><span class="sxs-lookup"><span data-stu-id="eb0f8-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![Otwórz z usługi więcej kondycja zasobów](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="eb0f8-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb0f8-153">Next steps</span></span>

<span data-ttu-id="eb0f8-154">Wyewidencjonuj toolearn tych zasobów, więcej informacji na temat kondycji zasobów:</span><span class="sxs-lookup"><span data-stu-id="eb0f8-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="eb0f8-155">Typy zasobów i kondycji sprawdza w kondycji zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eb0f8-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="eb0f8-156">Często zadawane pytania dotyczące kondycji zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eb0f8-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




