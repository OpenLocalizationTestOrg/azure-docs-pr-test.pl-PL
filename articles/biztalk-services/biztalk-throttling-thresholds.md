---
title: "aaaLearn dotyczące ograniczenia przepustowości w usługi BizTalk Services | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat ograniczania progów i wynikowa zachowanie w czasie wykonywania dla usługi BizTalk Services. Ograniczanie opiera się na użycie pamięci i liczbę komunikatów. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: f6663cf2-cda4-4bac-855e-27d2ad5c4fa4
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 46c8806c3a1f4eeb793f721f849771e0ec155197
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="55657-105">BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)</span><span class="sxs-lookup"><span data-stu-id="55657-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="55657-106">Usługi BizTalk Azure implementuje ograniczania usługi na podstawie dwóch warunków: pamięci użycia i hello liczbę jednoczesnych przetwarzania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="55657-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and hello number of simultaneous messages processing.</span></span> <span data-ttu-id="55657-107">W tym temacie wymieniono hello ograniczania progów i opisano hello zachowania w czasie wykonywania, jeśli dławienia stan występuje.</span><span class="sxs-lookup"><span data-stu-id="55657-107">This topic lists hello throttling thresholds and describes hello Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="55657-108">Progi ograniczania przepustowości</span><span class="sxs-lookup"><span data-stu-id="55657-108">Throttling Thresholds</span></span>
<span data-ttu-id="55657-109">Witaj w następującej tabeli przedstawiono hello progi i ograniczania przepustowości źródła:</span><span class="sxs-lookup"><span data-stu-id="55657-109">hello following table lists hello throttling source and thresholds:</span></span>

|  | <span data-ttu-id="55657-110">Opis</span><span class="sxs-lookup"><span data-stu-id="55657-110">Description</span></span> | <span data-ttu-id="55657-111">Dolna wartość progowa</span><span class="sxs-lookup"><span data-stu-id="55657-111">Low Threshold</span></span> | <span data-ttu-id="55657-112">Górny próg</span><span class="sxs-lookup"><span data-stu-id="55657-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="55657-113">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="55657-113">Memory</span></span> |<span data-ttu-id="55657-114">% całkowitej systemu pamięci dostępne/PageFileBytes.</span><span class="sxs-lookup"><span data-stu-id="55657-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="55657-115">Całkowita liczba dostępnych PageFileBytes wynosi około 2 razy hello pamięci RAM hello systemu.</span><span class="sxs-lookup"><span data-stu-id="55657-115">Total available PageFileBytes is approximately 2 times hello RAM of hello system.</span></span> |<span data-ttu-id="55657-116">60%</span><span class="sxs-lookup"><span data-stu-id="55657-116">60%</span></span> |<span data-ttu-id="55657-117">70%</span><span class="sxs-lookup"><span data-stu-id="55657-117">70%</span></span> |
| <span data-ttu-id="55657-118">Przetwarzanie komunikatów</span><span class="sxs-lookup"><span data-stu-id="55657-118">Message Processing</span></span> |<span data-ttu-id="55657-119">Liczba komunikatów przetwarzania jednocześnie</span><span class="sxs-lookup"><span data-stu-id="55657-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="55657-120">40 * liczba rdzeni</span><span class="sxs-lookup"><span data-stu-id="55657-120">40 * number of cores</span></span> |<span data-ttu-id="55657-121">100 * Liczba rdzeni</span><span class="sxs-lookup"><span data-stu-id="55657-121">100 * number of cores</span></span> |

<span data-ttu-id="55657-122">Po osiągnięciu progu wysokiego toothrottle zostaną uruchomione usługi BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="55657-122">When a high threshold is reached, Azure BizTalk Services starts toothrottle.</span></span> <span data-ttu-id="55657-123">Ograniczanie zatrzymuje po osiągnięciu progu dolnego hello.</span><span class="sxs-lookup"><span data-stu-id="55657-123">Throttling stops when hello low threshold is reached.</span></span> <span data-ttu-id="55657-124">Na przykład usługi używa 65% pamięci systemowej.</span><span class="sxs-lookup"><span data-stu-id="55657-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="55657-125">W takiej sytuacji usługa hello nie ograniczenie przepustowości.</span><span class="sxs-lookup"><span data-stu-id="55657-125">In this situation, hello service does not throttle.</span></span> <span data-ttu-id="55657-126">Usługa uruchamia przy użyciu 70% pamięci systemowej.</span><span class="sxs-lookup"><span data-stu-id="55657-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="55657-127">W takiej sytuacji usługa hello ogranicza i kontynuuje toothrottle, dopóki usługa hello używa pamięci systemowej (progu dolnego) 60%.</span><span class="sxs-lookup"><span data-stu-id="55657-127">In this situation, hello service throttles and continues toothrottle until hello service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="55657-128">Usługi BizTalk Azure śledzi hello ograniczania stanu (normalnym stanie a stanu ograniczeniem przepustowości) i hello ograniczania czas trwania.</span><span class="sxs-lookup"><span data-stu-id="55657-128">Azure BizTalk Services tracks hello throttling status (normal state vs. throttled state) and hello throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="55657-129">Zachowania w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="55657-129">Runtime Behavior</span></span>
<span data-ttu-id="55657-130">Podczas usług BizTalk Azure przechodzi do stanu ograniczania przepustowości, występuje hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="55657-130">When Azure BizTalk Services enters a throttling state, hello following occurs:</span></span>

* <span data-ttu-id="55657-131">Ograniczenie jest dla każdego wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="55657-131">Throttling is per role instance.</span></span> <span data-ttu-id="55657-132">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="55657-132">For example:</span></span><br/>
  <span data-ttu-id="55657-133">RoleInstanceA jest ograniczanie.</span><span class="sxs-lookup"><span data-stu-id="55657-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="55657-134">Nie jest ograniczanie RoleInstanceB.</span><span class="sxs-lookup"><span data-stu-id="55657-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="55657-135">W takim przypadku komunikatów w RoleInstanceB są przetwarzane zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="55657-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="55657-136">Komunikaty w RoleInstanceA zostaną odrzucone i zakończyć się niepowodzeniem z hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="55657-136">Messages in RoleInstanceA are discarded and fail with hello following error:</span></span><br/><br/><span data-ttu-id="55657-137">
  **Serwer jest zajęty. Spróbuj ponownie.**</span><span class="sxs-lookup"><span data-stu-id="55657-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="55657-138">Wszystkie źródła ściągania nie sondowania lub pobierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="55657-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="55657-139">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="55657-139">For example:</span></span><br/>
  <span data-ttu-id="55657-140">Potok ściąga komunikatów ze źródła zewnętrznego FTP.</span><span class="sxs-lookup"><span data-stu-id="55657-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="55657-141">Pobiera wystąpienia roli Hello czynności ściągania hello stan ograniczania przepustowości.</span><span class="sxs-lookup"><span data-stu-id="55657-141">hello role instance doing hello pull gets into a throttling state.</span></span> <span data-ttu-id="55657-142">W takiej sytuacji potoku hello zatrzymuje pobieranie dodatkowych komunikatów, do momentu wystąpienia roli hello zatrzymuje ograniczania.</span><span class="sxs-lookup"><span data-stu-id="55657-142">In this situation, hello pipeline stops downloading additional messages until hello role instance stops throttling.</span></span>
* <span data-ttu-id="55657-143">Odpowiedź jest wysyłana toohello klienta, więc powitania klienta można ponownie przesłać wiadomość hello.</span><span class="sxs-lookup"><span data-stu-id="55657-143">A response is sent toohello client so hello client can resubmit hello message.</span></span>
* <span data-ttu-id="55657-144">Musisz poczekać, aż ograniczania hello zostanie rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="55657-144">You must wait until hello throttling is resolved.</span></span> <span data-ttu-id="55657-145">W szczególności należy poczekać, aż do osiągnięcia progu dolnego hello.</span><span class="sxs-lookup"><span data-stu-id="55657-145">Specifically, you must wait until hello low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="55657-146">Ważne uwagi</span><span class="sxs-lookup"><span data-stu-id="55657-146">Important notes</span></span>
* <span data-ttu-id="55657-147">Nie można wyłączyć ograniczenia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="55657-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="55657-148">Nie można zmodyfikować ograniczania progów.</span><span class="sxs-lookup"><span data-stu-id="55657-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="55657-149">Ograniczanie zaimplementowano całego systemu.</span><span class="sxs-lookup"><span data-stu-id="55657-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="55657-150">powitania serwera bazy danych SQL Azure ma również wbudowane ograniczenia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="55657-150">hello Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="55657-151">Dodatkowe tematy Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="55657-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="55657-152">Instalowanie hello Azure zestawu SDK usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="55657-152">Installing hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="55657-153">Samouczki: Usługi Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="55657-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="55657-154">Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="55657-154">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="55657-155">Usługi Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="55657-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="55657-156">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="55657-156">See Also</span></span>
* [<span data-ttu-id="55657-157">Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu</span><span class="sxs-lookup"><span data-stu-id="55657-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="55657-158">Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="55657-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="55657-159">BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)</span><span class="sxs-lookup"><span data-stu-id="55657-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="55657-160">BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)</span><span class="sxs-lookup"><span data-stu-id="55657-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="55657-161">BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)</span><span class="sxs-lookup"><span data-stu-id="55657-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="55657-162">BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)</span><span class="sxs-lookup"><span data-stu-id="55657-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

