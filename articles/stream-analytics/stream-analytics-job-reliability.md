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
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="cc290-103">Zagwarantować niezawodność zadania usługi analiza strumienia podczas aktualizacji usługi</span><span class="sxs-lookup"><span data-stu-id="cc290-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="cc290-104">Część jest w pełni zarządzana usługa jest hello możliwości toointroduce nowej usługi funkcji i ulepszeń w tempie szybkie.</span><span class="sxs-lookup"><span data-stu-id="cc290-104">Part of being a fully managed service is hello capability toointroduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="cc290-105">W związku z tym usługi analiza strumienia może mieć aktualizacji usługi wdrażanie na podstawie co tydzień (lub częstsze).</span><span class="sxs-lookup"><span data-stu-id="cc290-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="cc290-106">Niezależnie od tego, ile testów jest wykonywane jest nadal ryzyko, że istniejący, uruchomione zadania mogą być dzielone powodu wprowadzenia toohello usterki.</span><span class="sxs-lookup"><span data-stu-id="cc290-106">No matter how much testing is done there is still a risk that an existing, running job may break due toohello introduction of a bug.</span></span> <span data-ttu-id="cc290-107">Dla klientów, którzy uruchomić krytycznego zadania przesyłania strumieniowego przetwarzania te zagrożenia, należy unikać toobe.</span><span class="sxs-lookup"><span data-stu-id="cc290-107">For customers who run critical streaming processing jobs these risks need toobe avoided.</span></span> <span data-ttu-id="cc290-108">Mechanizm mogą używać tooreduce to zagrożenie jest platformy Azure  **[sparowanego region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modelu.</span><span class="sxs-lookup"><span data-stu-id="cc290-108">A mechanism customers can use tooreduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="cc290-109">Jak regiony platformy Azure sparowanym rozwiązania tego problemu?</span><span class="sxs-lookup"><span data-stu-id="cc290-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="cc290-110">Analiza strumienia gwarantuje, że zadania w parach regiony są aktualizowane w oddzielnych partiach.</span><span class="sxs-lookup"><span data-stu-id="cc290-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="cc290-111">W związku z tym istnieje wystarczająca odstęp czasu między aktualizacjami hello tooidentify potencjalne dzielenie usterek i usuwać z nich.</span><span class="sxs-lookup"><span data-stu-id="cc290-111">As a result there is a sufficient time gap between hello updates tooidentify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="cc290-112">_Z wyjątkiem hello Indie środkowe_ (których sparowanego regionu, Indie Południowe nie ma obecności Stream Analytics), wdrożenie hello tooStream aktualizacji Analytics nie może mieć miejsce, w hello sam czasu w zestawie regionów sparowany.</span><span class="sxs-lookup"><span data-stu-id="cc290-112">_With hello exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), hello deployment of an update tooStream Analytics would not occur at hello same time in a set of paired regions.</span></span> <span data-ttu-id="cc290-113">Wdrożenia w wielu regionach **w hello tej samej grupie** może wystąpić **na powitania jednocześnie**.</span><span class="sxs-lookup"><span data-stu-id="cc290-113">Deployments in multiple regions **in hello same group** may occur **at hello same time**.</span></span>

<span data-ttu-id="cc290-114">Artykuł Hello na  **[dostępności i regiony sparowanego](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  ma hello najbardziej aktualne informacje, na którym są skojarzone regionów.</span><span class="sxs-lookup"><span data-stu-id="cc290-114">hello article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has hello most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="cc290-115">Klienci są toodeploy zaleca identyczne zadania tooboth łączyć regionów.</span><span class="sxs-lookup"><span data-stu-id="cc290-115">Customers are advised toodeploy identical jobs tooboth paired regions.</span></span> <span data-ttu-id="cc290-116">Ponadto zaleca się tooStream Analytics wewnętrznego, możliwości, klienci są również toomonitor hello zadania tak, jakby **zarówno** zadań produkcji.</span><span class="sxs-lookup"><span data-stu-id="cc290-116">In addition tooStream Analytics internal monitoring capabilities, customers are also advised toomonitor hello jobs as if **both** are production jobs.</span></span> <span data-ttu-id="cc290-117">Jeśli podział toobe zidentyfikowanego w wyniku aktualizacji usługi Stream Analytics hello, eskalować odpowiednio i tryb failover wszelkie dane wyjściowe zadania w dobrej kondycji toohello podrzędne konsumentów.</span><span class="sxs-lookup"><span data-stu-id="cc290-117">If a break is identified toobe a result of hello Stream Analytics service update, escalate appropriately and fail over any downstream consumers toohello healthy job output.</span></span> <span data-ttu-id="cc290-118">Toosupport eskalacji region sparowanego hello zapobiec wpływowi hello nowe wdrożenie, a zachowanie spójności hello hello łączyć zadań.</span><span class="sxs-lookup"><span data-stu-id="cc290-118">Escalation toosupport will prevent hello paired region from being affected by hello new deployment and maintain hello integrity of hello paired jobs.</span></span>
