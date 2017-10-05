---
title: "Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure"
description: "W tym artykule wyjaśniono, jak nowej usłudze Azure App Service i jej funkcji wpływ na istniejące usługi platformy Azure."
services: app-service
documentationcenter: 
author: yochay
manager: nirma
editor: 
ms.assetid: 86c6a292-3c33-49f4-890c-89cc0321b397
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/12/2016
ms.author: yochaykk
ms.openlocfilehash: ed967fda7a216ed49532be54228ebe888cf16b6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="718d9-103">Usługa Azure App Service i istniejące usługi Azure</span><span class="sxs-lookup"><span data-stu-id="718d9-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="718d9-104">W tym artykule omówiono zmian do istniejących usług platformy Azure w ramach ze sobą kilka usług platformy Azure do zmiany [usłudze Azure App Service](https://azure.microsoft.com/services/app-service/), zintegrowane nową ofertę.</span><span class="sxs-lookup"><span data-stu-id="718d9-104">This article outlines the changes to existing Azure services as part of the change to bring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="718d9-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="718d9-105">Overview</span></span>
<span data-ttu-id="718d9-106">[Usługa aplikacji Azure](https://azure.microsoft.com/services/app-service/) to usługa w chmurze nowych i unikatowych, który umożliwia deweloperom tworzenie aplikacji sieci web i aplikacji mobilnych dla dowolnej platformy i każdego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="718d9-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers to create web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="718d9-107">Usługi aplikacji to zintegrowane rozwiązanie przeznaczone do usprawnić powtarzane funkcji kodowania, zintegrować z przedsiębiorstwa i systemy SaaS i automatyzować procesy biznesowe spełniając wymagania użytkownika dotyczące bezpieczeństwa, niezawodności i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="718d9-107">App Service is an integrated solution designed to streamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="718d9-108">Usługi aplikacji, połączono następujące istniejące usługi platformy Azure - [witryn sieci Web](https://azure.microsoft.com/services/websites/), [usług Mobile Services](https://azure.microsoft.com/services/mobile-services/), i [usługi Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) w pojedynczy połączone usługi, podczas dodawania nowe możliwości.</span><span class="sxs-lookup"><span data-stu-id="718d9-108">App Service brings together the following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="718d9-109">Usługi aplikacji umożliwia hostowanie następujących typów aplikacji:</span><span class="sxs-lookup"><span data-stu-id="718d9-109">App Service allows you to host the following app types:</span></span>

* <span data-ttu-id="718d9-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="718d9-110">Web Apps</span></span>
* <span data-ttu-id="718d9-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="718d9-111">Mobile Apps</span></span>
* <span data-ttu-id="718d9-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="718d9-112">API Apps</span></span>
* <span data-ttu-id="718d9-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="718d9-113">Logic Apps</span></span>

<span data-ttu-id="718d9-114">W poniższej tabeli opisano, jak istniejącej mapy usług Azure App Service i dostępne w nim typów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="718d9-114">The following table explains how existing Azure services map to App Service and the app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="718d9-115">Istniejące usługi platformy Azure</span><span class="sxs-lookup"><span data-stu-id="718d9-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="718d9-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="718d9-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="718d9-117">Co zmieniono</span><span class="sxs-lookup"><span data-stu-id="718d9-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="718d9-118">Azure Websites</span><span class="sxs-lookup"><span data-stu-id="718d9-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="718d9-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="718d9-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="718d9-120">Dla witryn sieci Web platformy Azure usługa aplikacji jest ograniczone do zmiany nazwy witryny sieci Web do aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="718d9-120">For Azure Websites, App Service is strictly limited to changing the name  Websites to Web Apps.</span></span>
<p><li><span data-ttu-id="718d9-121">Wszystkie wystąpienia istniejących witryn sieci Web są teraz aplikacje sieci Web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="718d9-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="718d9-122">Dostęp można uzyskać istniejących witryn sieci Web za pośrednictwem <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, gdzie można znaleźć wszystkich istniejących lokacji w obszarze <em>aplikacje sieci Web</em>.</span><span class="sxs-lookup"><span data-stu-id="718d9-122">You can access your existing websites via the <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="718d9-123"><em>Plan hostingu w sieci Web</em> jest teraz <em>planu usługi App Service</em>.</span><span class="sxs-lookup"><span data-stu-id="718d9-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="718d9-124"><em>Planu usługi App Service</em> może obsługiwać dowolnego typu aplikacji usługi App Service, takich jak aplikacje sieci Web, mobilnych, logiki lub interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="718d9-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="718d9-125">Aplikacje sieci Web usługi aplikacji platformy Azure jest ogólnie dostępności.</span><span class="sxs-lookup"><span data-stu-id="718d9-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="718d9-126"><a href="http://azure.microsoft.com/services/app-service/web/">Dowiedz się więcej o aplikacjach sieci Web</a>.</span><span class="sxs-lookup"><span data-stu-id="718d9-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="718d9-127">Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="718d9-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="718d9-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="718d9-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="718d9-129">Mobile Services nadal dostępna jako autonomiczna usługa i pozostają w pełni obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="718d9-129">Mobile Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="718d9-130">Aplikacje mobilne nie jest typem aplikacji w usłudze App Service, która integruje wszystkie funkcje usługi Mobile Services i inne.</span><span class="sxs-lookup"><span data-stu-id="718d9-130">Mobile Apps is an app type in App Service, which integrates all of the functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="718d9-131">Ułatwia <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migracji z usług Mobile Services do Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="718d9-131">It is easy to <a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services to Mobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="718d9-132">W ramach usługi App Service Mobile Apps pobrać nowe możliwości poza usługi mobilne, takie jak integracji z lokalnymi i systemy SaaS przemieszczania miejsc, zadań Webjob, opcje lepiej skalowania i.</span><span class="sxs-lookup"><span data-stu-id="718d9-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="718d9-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Dowiedz się więcej o Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="718d9-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="718d9-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="718d9-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="718d9-135">Aplikacje interfejsu API jest nowy typ aplikacji w usłudze App Service, która umożliwia łatwe tworzenie i korzystanie z interfejsów API w chmurze.</span><span class="sxs-lookup"><span data-stu-id="718d9-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in the cloud.</span></span></p>
<p><li><span data-ttu-id="718d9-136"><a href="http://azure.microsoft.com/services/app-service/api/">Dowiedz się więcej o aplikacjach interfejsu API</a>.</span><span class="sxs-lookup"><span data-stu-id="718d9-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="718d9-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="718d9-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="718d9-138">Logic Apps jest nowy typ aplikacji w usłudze App Service pozwala łatwo automatyzować procesy biznesowe.</span><span class="sxs-lookup"><span data-stu-id="718d9-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="718d9-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Dowiedz się więcej o aplikacjach Logic Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="718d9-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="718d9-140">Usługa Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="718d9-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="718d9-141">Aplikacje interfejsu API BizTalk</span><span class="sxs-lookup"><span data-stu-id="718d9-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="718d9-142">Usługi BizTalk Services nadal dostępna jako autonomiczna usługa i pozostają w pełni obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="718d9-142">BizTalk Services continue to be available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="718d9-143">Możliwości usługi BizTalk Services są zintegrowane z usługi aplikacji jako aplikacji interfejsu API umożliwienie użytkownikom wykonywanie integracji aplikacji przedsiębiorstwa i scenariusze B2B integracji ze wszystkimi typami aplikacji w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="718d9-143">All the capabilities of BizTalk Services are integrated into App Service as API Apps enabling users to perform enterprise application integration and B2B integration scenarios with any of the app types in App Service.</span></span></p>
<li><p><span data-ttu-id="718d9-144">Dzięki aplikacjom logiki można teraz automatyzować procesy biznesowe, do tworzenia przepływów pracy za pomocą środowiska projektowania visual.</span><span class="sxs-lookup"><span data-stu-id="718d9-144">With Logic Apps, you can now automate business processes using a visual design experience to create workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="718d9-145">Aby dowiedzieć się więcej, odwiedź [dokumentacji usługi aplikacji](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="718d9-145">To learn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

