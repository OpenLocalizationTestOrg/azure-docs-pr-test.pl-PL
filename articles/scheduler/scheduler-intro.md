---
title: aaaWhat jest Harmonogram systemu Azure? | Microsoft Docs
description: "Harmonogram systemu Azure pozwala toodeclaratively opisano akcje toorun w chmurze hello. Usługa następnie planuje i uruchamia te akcje automatycznie."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 52aa6ae1-4c3d-43fb-81b0-6792c84bcfae
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 062e25ae473510264dc0038198c05e7ac1e86210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-scheduler"></a><span data-ttu-id="c2abc-105">Co to jest usługa Azure Scheduler?</span><span class="sxs-lookup"><span data-stu-id="c2abc-105">What is Azure Scheduler?</span></span>
<span data-ttu-id="c2abc-106">Harmonogram systemu Azure pozwala toodeclaratively opisano akcje toorun w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="c2abc-106">Azure Scheduler allows you toodeclaratively describe actions toorun in hello cloud.</span></span> <span data-ttu-id="c2abc-107">Usługa następnie planuje i uruchamia te akcje automatycznie.</span><span class="sxs-lookup"><span data-stu-id="c2abc-107">It then schedules and runs those actions automatically.</span></span>  <span data-ttu-id="c2abc-108">Harmonogram dokonuje tego przy użyciu [hello portalu Azure](scheduler-get-started-portal.md), kod, [interfejsu API REST](https://msdn.microsoft.com/library/mt629143.aspx), lub Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2abc-108">Scheduler does this by using [hello Azure portal](scheduler-get-started-portal.md), code, [REST API](https://msdn.microsoft.com/library/mt629143.aspx), or Azure PowerShell.</span></span>

<span data-ttu-id="c2abc-109">Usługa Scheduler tworzy, obsługuje i wywołuje zaplanowane prace.</span><span class="sxs-lookup"><span data-stu-id="c2abc-109">Scheduler creates, maintains, and invokes scheduled work.</span></span>  <span data-ttu-id="c2abc-110">Usługa Scheduler nie hostuje żadnych obciążeń ani nie uruchamia żadnego kodu.</span><span class="sxs-lookup"><span data-stu-id="c2abc-110">Scheduler does not host any workloads or run any code.</span></span> <span data-ttu-id="c2abc-111">*Wywołuje* ona jedynie kod hostowany gdzie indziej — na platformie Azure, lokalnie lub przez innego dostawcę.</span><span class="sxs-lookup"><span data-stu-id="c2abc-111">It only *invokes* code hosted elsewhere—in Azure, on-premises, or with another provider.</span></span> <span data-ttu-id="c2abc-112">Wywoływanie następuje z użyciem protokołu HTTP, HTTPS, kolejki magazynu, kolejki magistrali usług lub tematu magistrali usług.</span><span class="sxs-lookup"><span data-stu-id="c2abc-112">It invokes via HTTP, HTTPS, a storage queue, a service bus queue, or a service bus topic.</span></span>

<span data-ttu-id="c2abc-113">Harmonogramy harmonogramu [zadania](scheduler-concepts-terms.md), przechowuje historię wyników wykonania zadania jedną można sprawdzić, czy sposób niejednoznaczny i niezawodne toobe obciążeń harmonogramy uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="c2abc-113">Scheduler schedules [jobs](scheduler-concepts-terms.md), keeps a history of job execution results that one can review, and deterministically and reliably schedules workloads toobe run.</span></span> <span data-ttu-id="c2abc-114">Zadań Webjob Azure (część hello funkcja Web Apps w usłudze Azure App Service) i innych funkcji planowania platformy Azure za pomocą harmonogramu w tle hello.</span><span class="sxs-lookup"><span data-stu-id="c2abc-114">Azure WebJobs (part of hello Web Apps feature in Azure App Service) and other Azure scheduling capabilities use Scheduler in hello background.</span></span> <span data-ttu-id="c2abc-115">Witaj [interfejsu API REST harmonogramu](https://msdn.microsoft.com/library/mt629143.aspx) umożliwia zarządzanie hello komunikacji dla tych akcji.</span><span class="sxs-lookup"><span data-stu-id="c2abc-115">hello [Scheduler REST API](https://msdn.microsoft.com/library/mt629143.aspx) helps manage hello communication for these actions.</span></span> <span data-ttu-id="c2abc-116">W tym kontekście usługa Scheduler umożliwia prostą obsługę [złożonych harmonogramów i zaawansowanych cykli](scheduler-advanced-complexity.md).</span><span class="sxs-lookup"><span data-stu-id="c2abc-116">As such, Scheduler supports [complex schedules and advanced recurrence](scheduler-advanced-complexity.md) easily.</span></span>

<span data-ttu-id="c2abc-117">Istnieje kilka scenariuszy, które nadają się użycie toohello harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="c2abc-117">There are several scenarios that lend themselves toohello usage of Scheduler.</span></span> <span data-ttu-id="c2abc-118">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="c2abc-118">For example:</span></span>

* <span data-ttu-id="c2abc-119">*Cykliczne akcje aplikacji:* okresowe gromadzenie danych z serwisu Twitter w ramach źródła danych.</span><span class="sxs-lookup"><span data-stu-id="c2abc-119">*Recurring application actions:* Periodically gathering data from Twitter into a feed.</span></span>
* <span data-ttu-id="c2abc-120">*Codzienna konserwacja:* codzienne oczyszczanie dzienników, tworzenie kopii zapasowych i wykonywanie innych zadań konserwacji.</span><span class="sxs-lookup"><span data-stu-id="c2abc-120">*Daily maintenance:* Daily pruning of logs, performing backups, and other maintenance tasks.</span></span> <span data-ttu-id="c2abc-121">Na przykład administrator może wybrać tooback bazę danych hello godzinie 1:00</span><span class="sxs-lookup"><span data-stu-id="c2abc-121">For example, an administrator may choose tooback up hello database at 1:00 A.M.</span></span> <span data-ttu-id="c2abc-122">codziennie hello dalej 9 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="c2abc-122">every day for hello next nine months.</span></span>

<span data-ttu-id="c2abc-123">Harmonogram umożliwia toocreate, zaktualizować, usuwanie, wyświetlanie, zadania i zarządzać nimi i [zadania kolekcje](scheduler-concepts-terms.md) programowo, za pomocą skryptów i w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="c2abc-123">Scheduler allows you toocreate, update, delete, view, and manage jobs and [job collections](scheduler-concepts-terms.md) programmatically, by using scripts, and in hello portal.</span></span>

## <a name="see-also"></a><span data-ttu-id="c2abc-124">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c2abc-124">See also</span></span>
 [<span data-ttu-id="c2abc-125">Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek</span><span class="sxs-lookup"><span data-stu-id="c2abc-125">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="c2abc-126">Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c2abc-126">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="c2abc-127">Plany i rozliczenia w usłudze Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c2abc-127">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="c2abc-128">Jak planuje toobuild złożone i zaawansowane cyklu z Harmonogram systemu Azure</span><span class="sxs-lookup"><span data-stu-id="c2abc-128">How toobuild complex schedules and advanced recurrence with Azure Scheduler</span></span>](scheduler-advanced-complexity.md)

 [<span data-ttu-id="c2abc-129">Dokumentacja interfejsu API REST usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c2abc-129">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="c2abc-130">Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c2abc-130">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="c2abc-131">Wysoka dostępność i niezawodność usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c2abc-131">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="c2abc-132">Limity, wartości domyślne i kody błędów usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c2abc-132">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="c2abc-133">Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c2abc-133">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

