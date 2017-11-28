---
title: "Limity harmonogramu oraz wartości domyślnych"
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
ms.openlocfilehash: db6b1c196cb468f41c7a7ce34758de346b522abb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scheduler-limits-and-defaults"></a><span data-ttu-id="a943a-103">Limity harmonogramu oraz wartości domyślnych</span><span class="sxs-lookup"><span data-stu-id="a943a-103">Scheduler Limits and Defaults</span></span>
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a><span data-ttu-id="a943a-104">Przydziały harmonogramu, limity ustawień domyślnych i limity</span><span class="sxs-lookup"><span data-stu-id="a943a-104">Scheduler Quotas, Limits, Defaults, and Throttles</span></span>
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="the-x-ms-request-id-header"></a><span data-ttu-id="a943a-105">Nagłówek x-ms-request-id</span><span class="sxs-lookup"><span data-stu-id="a943a-105">The x-ms-request-id Header</span></span>
<span data-ttu-id="a943a-106">Każde żądanie dotyczące usługi harmonogramu zwraca nagłówka odpowiedzi o nazwie**x-ms-request-id**.</span><span class="sxs-lookup"><span data-stu-id="a943a-106">Every request made against the Scheduler service returns a response header named**x-ms-request-id**.</span></span> <span data-ttu-id="a943a-107">Ten nagłówek zawiera wartości nieprzezroczystej, który unikatowo identyfikuje żądania.</span><span class="sxs-lookup"><span data-stu-id="a943a-107">This header contains an opaque value that uniquely identifies the request.</span></span>

<span data-ttu-id="a943a-108">Jeśli żądanie jest zawsze kończy się niepowodzeniem i upewnieniu się, że żądanie jest poprawnie sformułowany, można użyć tej wartości na raport o błędzie do firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a943a-108">If a request is consistently failing and you have verified that the request is properly formulated, you may use this value to report the error to Microsoft.</span></span> <span data-ttu-id="a943a-109">W raporcie zawiera wartość x-ms-request-id, przybliżony czas, który odebrał żądanie, identyfikator subskrypcji, kolekcji zadań i/lub zadania i typ operacji, które próbowało żądania.</span><span class="sxs-lookup"><span data-stu-id="a943a-109">In your report, include the value of x-ms-request-id, the approximate time that the request was made, the identifier of the subscription, job collection, and/or job, and the type of operation that the request attempted.</span></span>

## <a name="see-also"></a><span data-ttu-id="a943a-110">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a943a-110">See Also</span></span>
 [<span data-ttu-id="a943a-111">Co to jest Scheduler?</span><span class="sxs-lookup"><span data-stu-id="a943a-111">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="a943a-112">Pojęcia i terminologia dotyczące usługi Azure Scheduler oraz hierarchia jednostek</span><span class="sxs-lookup"><span data-stu-id="a943a-112">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="a943a-113">Rozpoczynanie pracy z usługą Scheduler w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a943a-113">Get started using Scheduler in the Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="a943a-114">Plany i rozliczenia w usłudze Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="a943a-114">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="a943a-115">Dokumentacja interfejsu API REST usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="a943a-115">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="a943a-116">Dokumentacja poleceń cmdlet programu PowerShell dla usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="a943a-116">Azure Scheduler PowerShell cmdlets reference</span></span>](scheduler-powershell-reference.md)

 [<span data-ttu-id="a943a-117">Wysoka dostępność i niezawodność usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="a943a-117">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="a943a-118">Uwierzytelnianie połączeń wychodzących usługi Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="a943a-118">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

