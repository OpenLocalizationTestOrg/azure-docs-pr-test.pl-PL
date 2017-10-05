---
title: "Uniknąć przerw w działaniu usługi z zadania usługi analiza strumienia Azure | Dokumentacja firmy Microsoft"
description: "Wskazówki na temat tworzenia Twojej usługi analiza strumienia zadań uaktualniania odporność."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8dc19e1b37082c87d2990ad910d1af786f8b9280
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="1733d-103">Zagwarantować niezawodność zadania usługi analiza strumienia podczas aktualizacji usługi</span><span class="sxs-lookup"><span data-stu-id="1733d-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="1733d-104">Część jest w pełni zarządzana usługa jest możliwość wprowadzenia nowych funkcji usługi i ulepszenia w tempie szybkie.</span><span class="sxs-lookup"><span data-stu-id="1733d-104">Part of being a fully managed service is the capability to introduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="1733d-105">W związku z tym usługi analiza strumienia może mieć aktualizacji usługi wdrażanie na podstawie co tydzień (lub częstsze).</span><span class="sxs-lookup"><span data-stu-id="1733d-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="1733d-106">Niezależnie od tego, ile testów jest wykonywane jest nadal ryzyko, że istniejący, uruchomione zadanie może zostać przerwane z powodu wprowadzenia usterki.</span><span class="sxs-lookup"><span data-stu-id="1733d-106">No matter how much testing is done there is still a risk that an existing, running job may break due to the introduction of a bug.</span></span> <span data-ttu-id="1733d-107">Dla klientów, którzy uruchomić krytycznego zadania przesyłania strumieniowego przetwarzania te zagrożenia, należy unikać.</span><span class="sxs-lookup"><span data-stu-id="1733d-107">For customers who run critical streaming processing jobs these risks need to be avoided.</span></span> <span data-ttu-id="1733d-108">Mechanizm klienci mogą użyć, aby zmniejszyć to ryzyko jest Azure  **[sparowanego region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modelu.</span><span class="sxs-lookup"><span data-stu-id="1733d-108">A mechanism customers can use to reduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="1733d-109">Jak regiony platformy Azure sparowanym rozwiązania tego problemu?</span><span class="sxs-lookup"><span data-stu-id="1733d-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="1733d-110">Analiza strumienia gwarantuje, że zadania w parach regiony są aktualizowane w oddzielnych partiach.</span><span class="sxs-lookup"><span data-stu-id="1733d-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="1733d-111">W związku z tym jest wystarczające odstęp czasu między aktualizacjami, aby zidentyfikować potencjalne błędy podziału i usuwać z nich.</span><span class="sxs-lookup"><span data-stu-id="1733d-111">As a result there is a sufficient time gap between the updates to identify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="1733d-112">_Z wyjątkiem Indie środkowe_ (których sparowanego regionu, Indie Południowe nie ma obecności Stream Analytics), wdrożenie aktualizacji do usługi Stream Analytics nie może mieć miejsce, w tym samym czasie w zestawie regionów pary.</span><span class="sxs-lookup"><span data-stu-id="1733d-112">_With the exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), the deployment of an update to Stream Analytics would not occur at the same time in a set of paired regions.</span></span> <span data-ttu-id="1733d-113">Wdrożenia w wielu regionach **w tej samej grupie** może wystąpić **w tym samym czasie**.</span><span class="sxs-lookup"><span data-stu-id="1733d-113">Deployments in multiple regions **in the same group** may occur **at the same time**.</span></span>

<span data-ttu-id="1733d-114">Artykuł na temat  **[dostępności i regiony sparowanego](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  zawiera najbardziej aktualne informacje, na którym są skojarzone regionów.</span><span class="sxs-lookup"><span data-stu-id="1733d-114">The article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has the most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="1733d-115">Klienci są zalecane jest wdrażanie identyczne zadania dla obu sparowanego regionów.</span><span class="sxs-lookup"><span data-stu-id="1733d-115">Customers are advised to deploy identical jobs to both paired regions.</span></span> <span data-ttu-id="1733d-116">Oprócz Stream Analytics wewnętrzny możliwości monitorowania, klienci także zalecana do monitorowania zadań tak, jakby **zarówno** zadań produkcji.</span><span class="sxs-lookup"><span data-stu-id="1733d-116">In addition to Stream Analytics internal monitoring capabilities, customers are also advised to monitor the jobs as if **both** are production jobs.</span></span> <span data-ttu-id="1733d-117">Jeśli podział została zidentyfikowana jako wynik aktualizacji usługi Stream Analytics, eskalować odpowiednio i pracy awaryjnej żadnych użytkowników podrzędne w danych wyjściowych zadania w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="1733d-117">If a break is identified to be a result of the Stream Analytics service update, escalate appropriately and fail over any downstream consumers to the healthy job output.</span></span> <span data-ttu-id="1733d-118">Eskalacji do obsługi będzie zapobiec wpływowi nowe wdrożenie sparowanego regionu i zachowanie spójności sparowanego zadań.</span><span class="sxs-lookup"><span data-stu-id="1733d-118">Escalation to support will prevent the paired region from being affected by the new deployment and maintain the integrity of the paired jobs.</span></span>
