---
title: "Usługa aplikacji Azure: Skalowanie aplikacji usługi aplikacji"
description: "Dowiedz się, dokumentów i ins hello skalowania aplikacji w usłudze App Service."
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a><span data-ttu-id="24ad8-104">Usługa aplikacji Azure: Skalowanie aplikacji usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="24ad8-104">Azure App Service: Scaling App Service Applications</span></span>
<span data-ttu-id="24ad8-105">Aplikacje hostowane w usłudze Azure App Service można [osiągnięcia bardzo dużej skali](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span><span class="sxs-lookup"><span data-stu-id="24ad8-105">Applications hosted in Azure App Service can [achieve massive scale](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).</span></span>
<span data-ttu-id="24ad8-106">Jednak skalowanie aplikacji to złożony problem, który nie ma rozwiązania "dostosowane do wszystkich".</span><span class="sxs-lookup"><span data-stu-id="24ad8-106">However, scaling an application is a complex problem that does not have a "one size fits all" solution.</span></span> <span data-ttu-id="24ad8-107">toocorrectly skalowanie aplikacji przyczyni Powodzenie aplikacji tooyour 3 klucza obszary:</span><span class="sxs-lookup"><span data-stu-id="24ad8-107">toocorrectly scale your application there are 3 key areas that will contribute tooyour applications success:</span></span>

1. <span data-ttu-id="24ad8-108">Opis architektury aplikacji i jej słabe strony algorytmu.</span><span class="sxs-lookup"><span data-stu-id="24ad8-108">Understanding your application architecture and its weaknesses.</span></span>
   * <span data-ttu-id="24ad8-109">To jest Twoje Stateful aplikacji?</span><span class="sxs-lookup"><span data-stu-id="24ad8-109">Is your Application Stateful?</span></span> <span data-ttu-id="24ad8-110">Bezstanowe?</span><span class="sxs-lookup"><span data-stu-id="24ad8-110">Stateless?</span></span>
   * <span data-ttu-id="24ad8-111">Co to są wszystkie składniki hello aplikacji?</span><span class="sxs-lookup"><span data-stu-id="24ad8-111">What are all hello components of your application?</span></span>
     * <span data-ttu-id="24ad8-112">Gdzie są wąskich gardeł hello w aplikacji hello?</span><span class="sxs-lookup"><span data-stu-id="24ad8-112">Where are hello bottlenecks in hello application?</span></span>
   * <span data-ttu-id="24ad8-113">Gdy obciążenie zastosowane tooyour aplikacji, co spowoduje przerwanie pierwszy?</span><span class="sxs-lookup"><span data-stu-id="24ad8-113">When load is applied tooyour app, what will break first?</span></span>
2. <span data-ttu-id="24ad8-114">Opis hello oczekiwano wymagania dotyczące wydajności i obciążenia.</span><span class="sxs-lookup"><span data-stu-id="24ad8-114">Understanding hello expected load and performance requirements.</span></span>
   * <span data-ttu-id="24ad8-115">Czy aplikacja hello musi tooserve tysiąca użytkowników? lub milion?</span><span class="sxs-lookup"><span data-stu-id="24ad8-115">Does hello application need tooserve one thousand users? or one million?</span></span>
   * <span data-ttu-id="24ad8-116">Zostanie ruchu pochodzić z jednej lokalizacji geograficznej lub globalnie?</span><span class="sxs-lookup"><span data-stu-id="24ad8-116">Will traffic come from a single geographic location or globally?</span></span>
   * <span data-ttu-id="24ad8-117">Czy istnieją różnice w okresach? pików ruchu?</span><span class="sxs-lookup"><span data-stu-id="24ad8-117">Are there seasonal variations? traffic peaks?</span></span>
   * <span data-ttu-id="24ad8-118">Szybkość aplikacji hello powinno odpowiedzieć?</span><span class="sxs-lookup"><span data-stu-id="24ad8-118">How fast should hello app respond?</span></span> <span data-ttu-id="24ad8-119">1 sekundę?</span><span class="sxs-lookup"><span data-stu-id="24ad8-119">1 second?</span></span> <span data-ttu-id="24ad8-120">1 milisekundy?</span><span class="sxs-lookup"><span data-stu-id="24ad8-120">1 millisecond?</span></span>
3. <span data-ttu-id="24ad8-121">Opis i poprawnie platformy hello wykorzystać hosting aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24ad8-121">Understanding and correctly leverage hello platform hosting your app.</span></span>
   * <span data-ttu-id="24ad8-122">Funkcje należy wykorzystać I tooachieve Moje cele skali?</span><span class="sxs-lookup"><span data-stu-id="24ad8-122">What features should I leverage tooachieve my scale goals?</span></span>

<span data-ttu-id="24ad8-123">W tej sekcji pomoże Ci zrozumieć wszystkie czynniki hello i pomocy opracować strategię wykorzystującego hello niezbędne usługi aplikacji — funkcje tooachieve cele skalowalności.</span><span class="sxs-lookup"><span data-stu-id="24ad8-123">This section will help you understand all hello factors and help you devise a strategy that takes advantage of hello necessary App Service features tooachieve your scalability goals.</span></span>

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

