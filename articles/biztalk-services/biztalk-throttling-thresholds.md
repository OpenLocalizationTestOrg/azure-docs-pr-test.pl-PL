---
title: "Dowiedz się więcej o ograniczaniu przepustowości w usługi BizTalk Services | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 145e7470bbc01c676a1fb5856c0f9a8726e667fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-throttling"></a><span data-ttu-id="b2647-105">BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)</span><span class="sxs-lookup"><span data-stu-id="b2647-105">BizTalk Services: Throttling</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="b2647-106">Usługi BizTalk Azure implementuje ograniczania usługi na podstawie dwóch warunków: użycie pamięci i liczbę jednoczesnych przetwarzania komunikatów.</span><span class="sxs-lookup"><span data-stu-id="b2647-106">Azure BizTalk Services implements service throttling based on two conditions: memory usage and the number of simultaneous messages processing.</span></span> <span data-ttu-id="b2647-107">W tym temacie wymieniono progi ograniczania przepustowości i opisano zachowania w czasie wykonywania, jeśli dławienia stan występuje.</span><span class="sxs-lookup"><span data-stu-id="b2647-107">This topic lists the throttling thresholds and describes the Runtime behavior when a throttling condition occurs.</span></span>

## <a name="throttling-thresholds"></a><span data-ttu-id="b2647-108">Progi ograniczania przepustowości</span><span class="sxs-lookup"><span data-stu-id="b2647-108">Throttling Thresholds</span></span>
<span data-ttu-id="b2647-109">W poniższej tabeli wymieniono progi i ograniczania przepustowości źródła:</span><span class="sxs-lookup"><span data-stu-id="b2647-109">The following table lists the throttling source and thresholds:</span></span>

|  | <span data-ttu-id="b2647-110">Opis</span><span class="sxs-lookup"><span data-stu-id="b2647-110">Description</span></span> | <span data-ttu-id="b2647-111">Dolna wartość progowa</span><span class="sxs-lookup"><span data-stu-id="b2647-111">Low Threshold</span></span> | <span data-ttu-id="b2647-112">Górny próg</span><span class="sxs-lookup"><span data-stu-id="b2647-112">High Threshold</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b2647-113">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="b2647-113">Memory</span></span> |<span data-ttu-id="b2647-114">% całkowitej systemu pamięci dostępne/PageFileBytes.</span><span class="sxs-lookup"><span data-stu-id="b2647-114">% of total system memory available/PageFileBytes.</span></span> <p><p><span data-ttu-id="b2647-115">Całkowita liczba dostępnych PageFileBytes wynosi około 2 razy pamięci RAM systemu.</span><span class="sxs-lookup"><span data-stu-id="b2647-115">Total available PageFileBytes is approximately 2 times the RAM of the system.</span></span> |<span data-ttu-id="b2647-116">60%</span><span class="sxs-lookup"><span data-stu-id="b2647-116">60%</span></span> |<span data-ttu-id="b2647-117">70%</span><span class="sxs-lookup"><span data-stu-id="b2647-117">70%</span></span> |
| <span data-ttu-id="b2647-118">Przetwarzanie komunikatów</span><span class="sxs-lookup"><span data-stu-id="b2647-118">Message Processing</span></span> |<span data-ttu-id="b2647-119">Liczba komunikatów przetwarzania jednocześnie</span><span class="sxs-lookup"><span data-stu-id="b2647-119">Number of messages processing simultaneously</span></span> |<span data-ttu-id="b2647-120">40 * liczba rdzeni</span><span class="sxs-lookup"><span data-stu-id="b2647-120">40 * number of cores</span></span> |<span data-ttu-id="b2647-121">100 * Liczba rdzeni</span><span class="sxs-lookup"><span data-stu-id="b2647-121">100 * number of cores</span></span> |

<span data-ttu-id="b2647-122">Po osiągnięciu progu wysokiego usług BizTalk Azure rozpoczyna ograniczenie przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b2647-122">When a high threshold is reached, Azure BizTalk Services starts to throttle.</span></span> <span data-ttu-id="b2647-123">Ograniczanie zatrzymuje po osiągnięciu progu dolnego.</span><span class="sxs-lookup"><span data-stu-id="b2647-123">Throttling stops when the low threshold is reached.</span></span> <span data-ttu-id="b2647-124">Na przykład usługi używa 65% pamięci systemowej.</span><span class="sxs-lookup"><span data-stu-id="b2647-124">For example, your service is using 65% system memory.</span></span> <span data-ttu-id="b2647-125">W takiej sytuacji usługa nie ograniczenie przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b2647-125">In this situation, the service does not throttle.</span></span> <span data-ttu-id="b2647-126">Usługa uruchamia przy użyciu 70% pamięci systemowej.</span><span class="sxs-lookup"><span data-stu-id="b2647-126">Your service starts using 70% system memory.</span></span> <span data-ttu-id="b2647-127">W takiej sytuacji usługa ogranicza i ograniczenie przepustowości, dopóki usługa korzysta z pamięci systemowej (progu dolnego) 60% w dalszym ciągu.</span><span class="sxs-lookup"><span data-stu-id="b2647-127">In this situation, the service throttles and continues to throttle until the service uses 60% (low threshold) system memory.</span></span>

<span data-ttu-id="b2647-128">Usługi BizTalk Azure śledzi stan ograniczenia przepustowości (normalnym stanie a stanu ograniczeniem przepustowości) i czas trwania ograniczania przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b2647-128">Azure BizTalk Services tracks the throttling status (normal state vs. throttled state) and the throttling duration.</span></span>

## <a name="runtime-behavior"></a><span data-ttu-id="b2647-129">Zachowania w czasie wykonywania</span><span class="sxs-lookup"><span data-stu-id="b2647-129">Runtime Behavior</span></span>
<span data-ttu-id="b2647-130">Gdy usługi BizTalk Azure przechodzi do stanu ograniczania przepustowości, są następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="b2647-130">When Azure BizTalk Services enters a throttling state, the following occurs:</span></span>

* <span data-ttu-id="b2647-131">Ograniczenie jest dla każdego wystąpienia roli.</span><span class="sxs-lookup"><span data-stu-id="b2647-131">Throttling is per role instance.</span></span> <span data-ttu-id="b2647-132">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b2647-132">For example:</span></span><br/>
  <span data-ttu-id="b2647-133">RoleInstanceA jest ograniczanie.</span><span class="sxs-lookup"><span data-stu-id="b2647-133">RoleInstanceA is throttling.</span></span> <span data-ttu-id="b2647-134">Nie jest ograniczanie RoleInstanceB.</span><span class="sxs-lookup"><span data-stu-id="b2647-134">RoleInstanceB is not throttling.</span></span> <span data-ttu-id="b2647-135">W takim przypadku komunikatów w RoleInstanceB są przetwarzane zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="b2647-135">In this situation, messages in RoleInstanceB are processed as expected.</span></span> <span data-ttu-id="b2647-136">Komunikaty w RoleInstanceA zostaną odrzucone i zakończyć się niepowodzeniem z powodu następującego błędu:</span><span class="sxs-lookup"><span data-stu-id="b2647-136">Messages in RoleInstanceA are discarded and fail with the following error:</span></span><br/><br/><span data-ttu-id="b2647-137">
  **Serwer jest zajęty. Spróbuj ponownie.**</span><span class="sxs-lookup"><span data-stu-id="b2647-137">
**Server is busy. Please try again.**</span></span><br/><br/>
* <span data-ttu-id="b2647-138">Wszystkie źródła ściągania nie sondowania lub pobierania wiadomości.</span><span class="sxs-lookup"><span data-stu-id="b2647-138">Any pull sources do not poll or download a message.</span></span> <span data-ttu-id="b2647-139">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b2647-139">For example:</span></span><br/>
  <span data-ttu-id="b2647-140">Potok ściąga komunikatów ze źródła zewnętrznego FTP.</span><span class="sxs-lookup"><span data-stu-id="b2647-140">A pipeline pulls messages from an external FTP source.</span></span> <span data-ttu-id="b2647-141">Pobiera wystąpienia roli, podczas replikacji ściąganej stan ograniczania przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b2647-141">The role instance doing the pull gets into a throttling state.</span></span> <span data-ttu-id="b2647-142">W takiej sytuacji potoku zatrzymuje pobieranie dodatkowych komunikatów, do momentu wystąpienia roli zatrzymuje ograniczania.</span><span class="sxs-lookup"><span data-stu-id="b2647-142">In this situation, the pipeline stops downloading additional messages until the role instance stops throttling.</span></span>
* <span data-ttu-id="b2647-143">Odpowiedź jest wysyłane do klienta, dzięki czemu klient może ponownie przesłać wiadomości.</span><span class="sxs-lookup"><span data-stu-id="b2647-143">A response is sent to the client so the client can resubmit the message.</span></span>
* <span data-ttu-id="b2647-144">Musisz poczekać, aż ograniczenie został rozwiązany.</span><span class="sxs-lookup"><span data-stu-id="b2647-144">You must wait until the throttling is resolved.</span></span> <span data-ttu-id="b2647-145">W szczególności należy poczekać, aż do osiągnięcia dolna wartość progowa.</span><span class="sxs-lookup"><span data-stu-id="b2647-145">Specifically, you must wait until the low threshold is reached.</span></span>

## <a name="important-notes"></a><span data-ttu-id="b2647-146">Ważne uwagi</span><span class="sxs-lookup"><span data-stu-id="b2647-146">Important notes</span></span>
* <span data-ttu-id="b2647-147">Nie można wyłączyć ograniczenia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b2647-147">Throttling cannot be disabled.</span></span>
* <span data-ttu-id="b2647-148">Nie można zmodyfikować ograniczania progów.</span><span class="sxs-lookup"><span data-stu-id="b2647-148">Throttling thresholds cannot be modified.</span></span>
* <span data-ttu-id="b2647-149">Ograniczanie zaimplementowano całego systemu.</span><span class="sxs-lookup"><span data-stu-id="b2647-149">Throttling is implemented system-wide.</span></span>
* <span data-ttu-id="b2647-150">Serwer bazy danych SQL Azure ma również wbudowane ograniczenia przepustowości.</span><span class="sxs-lookup"><span data-stu-id="b2647-150">The Azure SQL Database Server also has built-in throttling.</span></span>

## <a name="additional-azure-biztalk-services-topics"></a><span data-ttu-id="b2647-151">Dodatkowe tematy Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="b2647-151">Additional Azure BizTalk Services topics</span></span>
* [<span data-ttu-id="b2647-152">Instalowanie usług Azure BizTalk SDK</span><span class="sxs-lookup"><span data-stu-id="b2647-152">Installing the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [<span data-ttu-id="b2647-153">Samouczki: Usługi Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="b2647-153">Tutorials: Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [<span data-ttu-id="b2647-154">Jak rozpocząć pracę z zestawem SDK usługi Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="b2647-154">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="b2647-155">Usługi Azure BizTalk</span><span class="sxs-lookup"><span data-stu-id="b2647-155">Azure BizTalk Services</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a><span data-ttu-id="b2647-156">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b2647-156">See Also</span></span>
* [<span data-ttu-id="b2647-157">Usługi BizTalk Services: Developer, podstawowa, standardowa i Premium Edition wykresu</span><span class="sxs-lookup"><span data-stu-id="b2647-157">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [<span data-ttu-id="b2647-158">Usługi BizTalk Services: Klasyczny portal Azure przy użyciu inicjowania obsługi</span><span class="sxs-lookup"><span data-stu-id="b2647-158">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [<span data-ttu-id="b2647-159">BizTalk Services: Provisioning Status Chart (Usługa BizTalk Services: aprowizowanie wykresu stanu)</span><span class="sxs-lookup"><span data-stu-id="b2647-159">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [<span data-ttu-id="b2647-160">BizTalk Services: Dashboard, Monitor and Scale tabs (Usługa BizTalk Services: karty Pulpit nawigacyjny, Monitor i Skalowanie)</span><span class="sxs-lookup"><span data-stu-id="b2647-160">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [<span data-ttu-id="b2647-161">BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)</span><span class="sxs-lookup"><span data-stu-id="b2647-161">BizTalk Services: Backup and Restore</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [<span data-ttu-id="b2647-162">BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)</span><span class="sxs-lookup"><span data-stu-id="b2647-162">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>

