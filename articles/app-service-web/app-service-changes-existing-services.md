---
title: "aaaAzure usługi aplikacji i jej wpływ na istniejące usługi platformy Azure"
description: "Wyjaśniono, jak hello nowej usłudze Azure App Service i jej funkcji wpływ na istniejące usługi na platformie Azure."
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
ms.openlocfilehash: a831a88fee38465e5b0b7c2c2340cf8a0d64c864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-and-existing-azure-services"></a><span data-ttu-id="3e570-103">Usługa Azure App Service i istniejące usługi Azure</span><span class="sxs-lookup"><span data-stu-id="3e570-103">Azure App Service and existing Azure services</span></span>
<span data-ttu-id="3e570-104">W tym artykule omówiono tooexisting zmiany hello Azure usługi jako część toobring zmiany hello razem kilka usług platformy Azure do [usłudze Azure App Service](https://azure.microsoft.com/services/app-service/), zintegrowane nową ofertę.</span><span class="sxs-lookup"><span data-stu-id="3e570-104">This article outlines hello changes tooexisting Azure services as part of hello change toobring together several Azure services into [Azure App Service](https://azure.microsoft.com/services/app-service/), a new integrated offering.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="overview"></a><span data-ttu-id="3e570-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="3e570-105">Overview</span></span>
<span data-ttu-id="3e570-106">[Usługa aplikacji Azure](https://azure.microsoft.com/services/app-service/) to usługa w chmurze nowych i unikatowych, który umożliwia deweloperom toocreate w sieci web i aplikacji mobilnych dla dowolnej platformy i każdego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="3e570-106">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a new and unique cloud service that enables developers toocreate web and mobile apps for any platform and any device.</span></span> <span data-ttu-id="3e570-107">Usługi aplikacji jest toostreamline zintegrowane rozwiązanie przeznaczone powtarzane funkcji kodowania, zintegrować z przedsiębiorstwa i systemy SaaS i automatyzować procesy biznesowe spełniając wymagania użytkownika dotyczące bezpieczeństwa, niezawodności i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="3e570-107">App Service is an integrated solution designed toostreamline repeated coding functions, integrate with enterprise and SaaS systems, and automate business processes while meeting your needs for security, reliability, and scalability.</span></span>

<span data-ttu-id="3e570-108">Usługi aplikacji, połączono powitania po Azure istniejących usług - [witryn sieci Web](https://azure.microsoft.com/services/websites/), [usług Mobile Services](https://azure.microsoft.com/services/mobile-services/), i [usługi Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) w pojedynczy połączone usługi, podczas Dodawanie nowe możliwości.</span><span class="sxs-lookup"><span data-stu-id="3e570-108">App Service brings together hello following existing Azure services - [Websites](https://azure.microsoft.com/services/websites/), [Mobile Services](https://azure.microsoft.com/services/mobile-services/), and [Biztalk Services](https://azure.microsoft.com/services/biztalk-services/) into a single combined service, while adding powerful new capabilities.</span></span>  <span data-ttu-id="3e570-109">Usługi aplikacji umożliwia hello toohost następujące typy aplikacji:</span><span class="sxs-lookup"><span data-stu-id="3e570-109">App Service allows you toohost hello following app types:</span></span>

* <span data-ttu-id="3e570-110">Web Apps</span><span class="sxs-lookup"><span data-stu-id="3e570-110">Web Apps</span></span>
* <span data-ttu-id="3e570-111">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="3e570-111">Mobile Apps</span></span>
* <span data-ttu-id="3e570-112">API Apps</span><span class="sxs-lookup"><span data-stu-id="3e570-112">API Apps</span></span>
* <span data-ttu-id="3e570-113">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3e570-113">Logic Apps</span></span>

<span data-ttu-id="3e570-114">Witaj poniższej tabeli opisano sposób istniejących Azure tooApp typu usługi i hello aplikacji dostępne w nim mapy usług.</span><span class="sxs-lookup"><span data-stu-id="3e570-114">hello following table explains how existing Azure services map tooApp Service and hello app types available within it.</span></span>

<table>
<thead>
<tr class="header">
<th align="left", style="width:10%"><span data-ttu-id="3e570-115">Istniejące usługi platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3e570-115">Existing Azure Service</span></span></th>
<th align="left", style="width:10%"><span data-ttu-id="3e570-116">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3e570-116">Azure App Service</span></span></th>
<th align="left", style="width:80%"><span data-ttu-id="3e570-117">Co zmieniono</span><span class="sxs-lookup"><span data-stu-id="3e570-117">What changed</span></span></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span data-ttu-id="3e570-118">Azure Websites</span><span class="sxs-lookup"><span data-stu-id="3e570-118">Azure Websites</span></span></td>
<td align="left"><span data-ttu-id="3e570-119">Web Apps</span><span class="sxs-lookup"><span data-stu-id="3e570-119">Web Apps</span></span></td>
<td align="left"><li><span data-ttu-id="3e570-120">Dla witryny sieci Web Azure App Service jest ograniczone toochanging hello nazwa witryny sieci Web tooWeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3e570-120">For Azure Websites, App Service is strictly limited toochanging hello name  Websites tooWeb Apps.</span></span>
<p><li><span data-ttu-id="3e570-121">Wszystkie wystąpienia istniejących witryn sieci Web są teraz aplikacje sieci Web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="3e570-121">All your existing instances of Websites are now Web Apps in App Service.</span></span></p>
<p><li><span data-ttu-id="3e570-122">Dostęp można uzyskać istniejących witryn sieci Web za pośrednictwem hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, gdzie można znaleźć wszystkich istniejących lokacji w obszarze <em>aplikacje sieci Web</em>.</span><span class="sxs-lookup"><span data-stu-id="3e570-122">You can access your existing websites via hello <a href="http://go.microsoft.com/fwlink/?LinkId=529715">Azure Portal</a>, where you will find all your existing sites under <em>Web Apps</em>.</span></span></p>
<p><li><span data-ttu-id="3e570-123"><em>Plan hostingu w sieci Web</em> jest teraz <em>planu usługi App Service</em>.</span><span class="sxs-lookup"><span data-stu-id="3e570-123"><em>Web Hosting Plan</em> is now <em>App Service Plan</em>.</span></span> <span data-ttu-id="3e570-124"><em>Planu usługi App Service</em> może obsługiwać dowolnego typu aplikacji usługi App Service, takich jak aplikacje sieci Web, mobilnych, logiki lub interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3e570-124">An <em>App Service Plan</em> can host any app type of App Service, such as Web, Mobile, Logic, or API apps.</span></span></p>
<p><li><span data-ttu-id="3e570-125">Aplikacje sieci Web usługi aplikacji platformy Azure jest ogólnie dostępności.</span><span class="sxs-lookup"><span data-stu-id="3e570-125">Azure App Service Web Apps is in General Availability.</span></span></p>
<p><li><span data-ttu-id="3e570-126"><a href="http://azure.microsoft.com/services/app-service/web/">Dowiedz się więcej o aplikacjach sieci Web</a>.</span><span class="sxs-lookup"><span data-stu-id="3e570-126"><a href="http://azure.microsoft.com/services/app-service/web/">Learn more about Web Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"><span data-ttu-id="3e570-127">Azure Mobile Services</span><span class="sxs-lookup"><span data-stu-id="3e570-127">Azure Mobile Services</span></span></td>
<td align="left"><span data-ttu-id="3e570-128">Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="3e570-128">Mobile Apps</span></span></td>
<td align="left"><p><li><span data-ttu-id="3e570-129">Usługi Mobile Services nadal dostępna jako autonomiczna usługa toobe i pozostają w pełni obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3e570-129">Mobile Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<p><li><span data-ttu-id="3e570-130">Aplikacje mobilne nie jest typem aplikacji w usłudze App Service, która integruje wszystkie funkcje hello usług Mobile Services i inne.</span><span class="sxs-lookup"><span data-stu-id="3e570-130">Mobile Apps is an app type in App Service, which integrates all of hello functionality of Mobile Services and more.</span></span></p>
<p><li><span data-ttu-id="3e570-131">Łatwo jest zbyt<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migracji z usług Mobile Services tooMobile aplikacji</a>.</span><span class="sxs-lookup"><span data-stu-id="3e570-131">It is easy too<a href="http://go.microsoft.com/fwlink/?LinkID=724279&clcid=0x409">migrate from Mobile Services tooMobile Apps</a>.</span></span></p>
<p><li><span data-ttu-id="3e570-132">W ramach usługi App Service Mobile Apps pobrać nowe możliwości poza usługi mobilne, takie jak integracji z lokalnymi i systemy SaaS przemieszczania miejsc, zadań Webjob, opcje lepiej skalowania i.</span><span class="sxs-lookup"><span data-stu-id="3e570-132">As part of App Service, Mobile Apps get new capabilities beyond Mobile Services, such as  integration with on-premises and SaaS systems, staging slots, WebJobs, better scaling options, and more.</span></span></p>
<p><li><span data-ttu-id="3e570-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Dowiedz się więcej o Mobile Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="3e570-133"><a href="http://azure.microsoft.com/services/app-service/mobile/">Learn more about Mobile Apps</a>.</span></span></p>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><span data-ttu-id="3e570-134">API Apps</span><span class="sxs-lookup"><span data-stu-id="3e570-134">API Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="3e570-135">Aplikacje interfejsu API jest nowy typ aplikacji w usłudze App Service, która umożliwia łatwe tworzenie i korzystanie z interfejsów API w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="3e570-135">API Apps is a new app type in App Service that lets you easily build and consume APIs in hello cloud.</span></span></p>
<p><li><span data-ttu-id="3e570-136"><a href="http://azure.microsoft.com/services/app-service/api/">Dowiedz się więcej o aplikacjach interfejsu API</a>.</span><span class="sxs-lookup"><span data-stu-id="3e570-136"><a href="http://azure.microsoft.com/services/app-service/api/">Learn more about API Apps</a>.</span></span></p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><span data-ttu-id="3e570-137">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="3e570-137">Logic Apps</span></span></td>
<td align="left">
<p><li><span data-ttu-id="3e570-138">Logic Apps jest nowy typ aplikacji w usłudze App Service pozwala łatwo automatyzować procesy biznesowe.</span><span class="sxs-lookup"><span data-stu-id="3e570-138">Logic Apps is a new app type in App Service that lets you easily automate business processes.</span></span></p>
<p><li><span data-ttu-id="3e570-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Dowiedz się więcej o aplikacjach Logic Apps</a>.</span><span class="sxs-lookup"><span data-stu-id="3e570-139"><a href="http://azure.microsoft.com/services/app-service/logic/">Learn more about Logic Apps</a>.</span></span></p></td>
</tr>
<tr class="odd">
<td align="left"><span data-ttu-id="3e570-140">Usługa Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="3e570-140">Azure BizTalk Services</span></span></td>
<td align="left"><span data-ttu-id="3e570-141">Aplikacje interfejsu API BizTalk</span><span class="sxs-lookup"><span data-stu-id="3e570-141">BizTalk API Apps</span></span></td>
<td align="left">
<li><p><span data-ttu-id="3e570-142">Usługi BizTalk Services nadal dostępna jako autonomiczna usługa toobe i pozostają w pełni obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3e570-142">BizTalk Services continue toobe available as a standalone service and remain fully supported.</span></span></p>
<li><p><span data-ttu-id="3e570-143">Wszystkie hello możliwości usługi BizTalk Services są zintegrowane z usługi aplikacji jako aplikacji interfejsu API umożliwienie użytkownikom tooperform enterprise integracji aplikacji i scenariusze B2B integracji ze wszystkimi typami aplikacji hello w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="3e570-143">All hello capabilities of BizTalk Services are integrated into App Service as API Apps enabling users tooperform enterprise application integration and B2B integration scenarios with any of hello app types in App Service.</span></span></p>
<li><p><span data-ttu-id="3e570-144">Dzięki aplikacjom logiki można teraz automatyzować procesy biznesowe, za pomocą visual Projektowanie przepływów pracy toocreate środowisko.</span><span class="sxs-lookup"><span data-stu-id="3e570-144">With Logic Apps, you can now automate business processes using a visual design experience toocreate workflows.</span></span></p></td>
</tr>
</tbody>
</table>

<span data-ttu-id="3e570-145">toolearn więcej, odwiedź stronę [dokumentacji usługi aplikacji](https://azure.microsoft.com/documentation/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="3e570-145">toolearn more, please visit [App Service documentation](https://azure.microsoft.com/documentation/services/app-service/).</span></span>

