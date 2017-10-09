---
title: "Limity aaaScheduler oraz wartości domyślnych"
description: "Limity harmonogramu oraz wartości domyślnych"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="c004a-103">Limity harmonogramu oraz wartości domyślnych</span><span class="sxs-lookup"><span data-stu-id="c004a-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="c004a-104">Przydziały harmonogramu, limity ustawień domyślnych i limity</span><span class="sxs-lookup"><span data-stu-id="c004a-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a><span data-ttu-id="c004a-105">Witaj x-ms-request-id nagłówka</span><span class="sxs-lookup"><span data-stu-id="c004a-105">hello x-ms-request-id Header</span></span>
<span data-ttu-id="c004a-106">Każde żądanie dotyczące hello usługa Harmonogram zwraca nagłówka odpowiedzi o nazwie**x-ms-request-id**. Ten nagłówek zawiera wartości nieprzezroczystej, który unikatowo identyfikuje hello żądania.</span><span class="sxs-lookup"><span data-stu-id="c004a-106">Every request made against hello Scheduler service returns a response header named**x-ms-request-id**. This header contains an opaque value that uniquely identifies hello request.</span></span>

<span data-ttu-id="c004a-107">Jeśli żądanie jest stale się niepowodzeniem, a ma zweryfikowaniu, że Żądanie hello jest poprawnie sformułowany, możesz użyć tej wartości tooreport hello błąd tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="c004a-107">If a request is consistently failing and you have verified that hello request is properly formulated, you may use this value tooreport hello error tooMicrosoft.</span></span> <span data-ttu-id="c004a-108">W raporcie, uwzględniania hello wartości x-ms-request-id hello przybliżony czas tego hello żądanie, hello identyfikator subskrypcji hello, kolekcji zadań i/lub zadania i hello typ operacji, która hello próby żądania.</span><span class="sxs-lookup"><span data-stu-id="c004a-108">In your report, include hello value of x-ms-request-id, hello approximate time that hello request was made, hello identifier of hello subscription, job collection, and/or job, and hello type of operation that hello request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="c004a-109">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c004a-109">See Also</span></span>
 [<span data-ttu-id="c004a-110">Co to jest Scheduler?</span><span class="sxs-lookup"><span data-stu-id="c004a-110">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="c004a-111">Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek</span><span class="sxs-lookup"><span data-stu-id="c004a-111">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="c004a-112">Rozpoczynanie pracy przy użyciu harmonogramu w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="c004a-112">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="c004a-113">Plany i rozliczenia w usłudze Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c004a-113">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="c004a-114">Dokumentacja interfejsu API REST usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c004a-114">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="c004a-115">Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c004a-115">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="c004a-116">Wysoka dostępność i niezawodność usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c004a-116">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="c004a-117">Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="c004a-117">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

