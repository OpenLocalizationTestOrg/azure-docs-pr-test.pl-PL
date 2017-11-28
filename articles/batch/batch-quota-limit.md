---
title: "aaaService przydziały i limity partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat przydziałów domyślnych partii zadań Azure, limity i ograniczenia i jak zwiększenie przydziału toorequest"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="7c2f4-103">Limity przydziału i limity usługi Batch</span><span class="sxs-lookup"><span data-stu-id="7c2f4-103">Batch service quotas and limits</span></span>

<span data-ttu-id="7c2f4-104">Jako z innymi usługami Azure, limity na istnieją pewne zasoby skojarzone z hello usługa partia zadań.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="7c2f4-105">Wiele z tych limitów jest przydziałów domyślnych zastosowane przez platformę Azure w subskrypcji hello lub na poziomie konta.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="7c2f4-106">W tym artykule omówiono te ustawienia domyślne, i jak mogą żądać przydziału zwiększa.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="7c2f4-107">Pamiętaj o tych limitach przydziału podczas projektowania i skalowania obciążeń usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="7c2f4-108">Na przykład jeśli pulę nie jest osiągnięciu hello docelowej liczby węzłów obliczeniowych, określonych przez Ciebie, może osiągnięto limit przydziału rdzeni hello konta partii zadań lub regionalnych przydziału rdzeni maszyn wirtualnych dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="7c2f4-109">Można uruchomić wiele obciążeń partii w jednym konta usługi partia zadań lub dystrybucji obciążeń między kontami partii zadań, które znajdują się w hello tej samej subskrypcji, ale w różnych regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="7c2f4-110">Jeśli planujesz toorun obciążeń produkcyjnych w partii, konieczne może tooincrease co najmniej jednego przydziały hello powyżej hello domyślne.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="7c2f4-111">Jeśli chcesz tooraise limit przydziału, możesz otworzyć online [żądania obsługi klienta](#increase-a-quota) bez dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="7c2f4-112">Limit przydziału jest limit kredytu nie gwarancji pojemności.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="7c2f4-113">Jeśli wymagana pojemność na dużą skalę, skontaktuj się z pomocą techniczną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="7c2f4-114">Limity przydziałów zasobów</span><span class="sxs-lookup"><span data-stu-id="7c2f4-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="7c2f4-115">Przydziały w trybie użytkownika subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7c2f4-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="7c2f4-116">Dla konta wsadowego z trybem przydziału puli ustawić także**subskrypcji użytkownika**, partii maszyny wirtualne i inne zasoby, takie jak kont magazynu, są tworzone bezpośrednio w ramach Twojej subskrypcji po utworzeniu puli.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="7c2f4-117">limit przydziału rdzeni partii zadań Azure Hello tooan konto utworzone w tym trybie nie ma zastosowania.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="7c2f4-118">Zamiast tego są stosowane przydziały hello w subskrypcji dla rdzeni regionalnych obliczeniowych i innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="7c2f4-119">Dowiedz się więcej o te przydziały w [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="7c2f4-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="7c2f4-120">Podczas planowania użycia zasobów dla konto utworzone w trybie użytkownika subskrypcji, hello Uwaga po partii zasobów (Dodawanie toocompute rdzenie) są wymagane dla każdego 40 maszyn wirtualnych systemu Linux lub 20 maszyn wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="7c2f4-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="7c2f4-121">Zasób</span><span class="sxs-lookup"><span data-stu-id="7c2f4-121">Resource</span></span> | <span data-ttu-id="7c2f4-122">Przydział</span><span class="sxs-lookup"><span data-stu-id="7c2f4-122">Quota</span></span> | <span data-ttu-id="7c2f4-123">Dostawca</span><span class="sxs-lookup"><span data-stu-id="7c2f4-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="7c2f4-124">Jedno konto magazynu</span><span class="sxs-lookup"><span data-stu-id="7c2f4-124">One storage account</span></span> | <span data-ttu-id="7c2f4-125">Konta magazynu</span><span class="sxs-lookup"><span data-stu-id="7c2f4-125">Storage Accounts</span></span> | <span data-ttu-id="7c2f4-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="7c2f4-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="7c2f4-127">Jeden publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="7c2f4-127">One public IP address</span></span> | <span data-ttu-id="7c2f4-128">Publiczne adresy IP</span><span class="sxs-lookup"><span data-stu-id="7c2f4-128">Public IP Addresses</span></span> | <span data-ttu-id="7c2f4-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="7c2f4-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="7c2f4-130">Jedną sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="7c2f4-130">One virtual network</span></span> | <span data-ttu-id="7c2f4-131">Sieci wirtualne</span><span class="sxs-lookup"><span data-stu-id="7c2f4-131">Virtual Networks</span></span> | <span data-ttu-id="7c2f4-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="7c2f4-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="7c2f4-133">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="7c2f4-133">One network security group</span></span> | <span data-ttu-id="7c2f4-134">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="7c2f4-134">Network Security Groups</span></span> | <span data-ttu-id="7c2f4-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="7c2f4-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="7c2f4-136">Jeden zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="7c2f4-136">One virtual machine scale set</span></span> | <span data-ttu-id="7c2f4-137">Zestawy skali maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="7c2f4-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="7c2f4-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="7c2f4-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="7c2f4-139">Jedna usługa równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="7c2f4-139">One load balancer</span></span> | <span data-ttu-id="7c2f4-140">Moduły równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="7c2f4-140">Load Balancers</span></span> | <span data-ttu-id="7c2f4-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="7c2f4-141">Microsoft.Network</span></span> | 

<span data-ttu-id="7c2f4-142">Hello rdzeni przydziału na poziomie regionalnym lub na rodzinę maszyny Wirtualnej powinny być zestaw zgodnie z toohello rozmiar maszyny Wirtualnej wymagana dla puli partii lub pul:</span><span class="sxs-lookup"><span data-stu-id="7c2f4-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="7c2f4-143">Przydział</span><span class="sxs-lookup"><span data-stu-id="7c2f4-143">Quota</span></span> | <span data-ttu-id="7c2f4-144">Dostawca</span><span class="sxs-lookup"><span data-stu-id="7c2f4-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="7c2f4-145">Całkowita liczba rdzeni regionalne</span><span class="sxs-lookup"><span data-stu-id="7c2f4-145">Total Regional Cores</span></span> | <span data-ttu-id="7c2f4-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="7c2f4-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="7c2f4-147">…</span><span class="sxs-lookup"><span data-stu-id="7c2f4-147">…</span></span> <span data-ttu-id="7c2f4-148">Rodziny rdzeni</span><span class="sxs-lookup"><span data-stu-id="7c2f4-148">Family Cores</span></span> | <span data-ttu-id="7c2f4-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="7c2f4-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="7c2f4-150">Inne ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-150">Other limits</span></span>
| <span data-ttu-id="7c2f4-151">**Zasób**</span><span class="sxs-lookup"><span data-stu-id="7c2f4-151">**Resource**</span></span> | <span data-ttu-id="7c2f4-152">**Limit maksymalny**</span><span class="sxs-lookup"><span data-stu-id="7c2f4-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="7c2f4-153">[Równoczesnych zadań](batch-parallel-node-tasks.md) na węzeł obliczeń</span><span class="sxs-lookup"><span data-stu-id="7c2f4-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="7c2f4-154">4 x liczba rdzeni węzła</span><span class="sxs-lookup"><span data-stu-id="7c2f4-154">4 x number of node cores</span></span> |
| <span data-ttu-id="7c2f4-155">[Aplikacje](batch-application-packages.md) na konto usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="7c2f4-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="7c2f4-156">20</span><span class="sxs-lookup"><span data-stu-id="7c2f4-156">20</span></span> |
| <span data-ttu-id="7c2f4-157">Pakiety aplikacji na aplikację</span><span class="sxs-lookup"><span data-stu-id="7c2f4-157">Application packages per application</span></span> |<span data-ttu-id="7c2f4-158">40</span><span class="sxs-lookup"><span data-stu-id="7c2f4-158">40</span></span> |
| <span data-ttu-id="7c2f4-159">Rozmiar pakietu aplikacji (wszystkie)</span><span class="sxs-lookup"><span data-stu-id="7c2f4-159">Application package size (each)</span></span> |<span data-ttu-id="7c2f4-160">Około 195GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="7c2f4-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="7c2f4-161">Maksymalna początkowy rozmiar zadań</span><span class="sxs-lookup"><span data-stu-id="7c2f4-161">Maximum start task size</span></span> | <span data-ttu-id="7c2f4-162">znaki 32768<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="7c2f4-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="7c2f4-163"><sup>1</sup> limit bloku maksymalny rozmiar obiektu blob magazynu azure</span><span class="sxs-lookup"><span data-stu-id="7c2f4-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="7c2f4-164">
<sup>2</sup> obejmuje plików zasobów i zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="7c2f4-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="7c2f4-165">Przydziały partii widoku</span><span class="sxs-lookup"><span data-stu-id="7c2f4-165">View Batch quotas</span></span>
<span data-ttu-id="7c2f4-166">Wyświetl przydziałami konta wsadowego w hello [portalu Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="7c2f4-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="7c2f4-167">Wybierz **partii kont** w portalu hello, a następnie wybierz konto usługi partia zadań hello interesuje Cię.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="7c2f4-168">Wybierz **właściwości** na konto usługi partia zadań hello menu bloku.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="7c2f4-169">bloku właściwości Hello Wyświetla hello **przydziały** obecnie stosowane toohello konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="7c2f4-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![Przydziały konta usługi partia zadań][account_quotas]

<span data-ttu-id="7c2f4-171">Dla konta wsadowego, utworzony w trybie użytkownika subskrypcji hello widoku powiązanych przydziały subskrypcji w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="7c2f4-172">Wybierz **subskrypcje**i wybierz subskrypcję hello używasz hello konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="7c2f4-173">Na powitania **subskrypcji** bloku, wybierz opcję **użycia + przydziały**.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="7c2f4-174">Zwiększ limit przydziału</span><span class="sxs-lookup"><span data-stu-id="7c2f4-174">Increase a quota</span></span>
<span data-ttu-id="7c2f4-175">Wykonaj te kroki toorequest, zwiększ limit przydziału dla konta partii zadań lub subskrypcję za pomocą hello [portalu Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="7c2f4-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="7c2f4-176">Typ Hello zwiększenia limitu przydziału zależy od trybu alokacji puli hello konta partii zadań.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="7c2f4-177">Zwiększ limit przydziału rdzeni partii</span><span class="sxs-lookup"><span data-stu-id="7c2f4-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="7c2f4-178">Jeśli Twoje konto usługi partia zadań została utworzona w **partii usługi** tryb, wykonaj te kroki toorequest zwiększenia limitu przydziału rdzeni partii:</span><span class="sxs-lookup"><span data-stu-id="7c2f4-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="7c2f4-179">Wybierz hello **Pomoc i obsługa techniczna** kafelka na pulpicie nawigacyjnym portalu lub hello znak zapytania (**?**) w hello prawym górnym rogu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="7c2f4-180">Wybierz **nowy obsługuje żądania** > **podstawy**.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="7c2f4-181">Na powitania **podstawy** bloku:</span><span class="sxs-lookup"><span data-stu-id="7c2f4-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="7c2f4-182">a.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-182">a.</span></span> <span data-ttu-id="7c2f4-183">**Wystawianie typu** > **przydziału**</span><span class="sxs-lookup"><span data-stu-id="7c2f4-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="7c2f4-184">b.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-184">b.</span></span> <span data-ttu-id="7c2f4-185">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-185">Select your subscription.</span></span>
   
    <span data-ttu-id="7c2f4-186">c.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-186">c.</span></span> <span data-ttu-id="7c2f4-187">**Typ limitu przydziału** > **partii**</span><span class="sxs-lookup"><span data-stu-id="7c2f4-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="7c2f4-188">d.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-188">d.</span></span> <span data-ttu-id="7c2f4-189">**Plan pomocy technicznej** > **Obsługa przydziałów — włączone**</span><span class="sxs-lookup"><span data-stu-id="7c2f4-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="7c2f4-190">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-190">Click **Next**.</span></span>
4. <span data-ttu-id="7c2f4-191">Na powitania **Problem** bloku:</span><span class="sxs-lookup"><span data-stu-id="7c2f4-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="7c2f4-192">a.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-192">a.</span></span> <span data-ttu-id="7c2f4-193">Wybierz **ważność** zgodnie z tooyour [wpływ na prowadzoną działalność][support_sev].</span><span class="sxs-lookup"><span data-stu-id="7c2f4-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="7c2f4-194">b.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-194">b.</span></span> <span data-ttu-id="7c2f4-195">W **szczegóły**, określ każdy przydział ma toochange, nazwa konta wsadowego hello i hello nowego limitu.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="7c2f4-196">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-196">Click **Next**.</span></span>
5. <span data-ttu-id="7c2f4-197">Na powitania **informacje kontaktowe** bloku:</span><span class="sxs-lookup"><span data-stu-id="7c2f4-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="7c2f4-198">a.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-198">a.</span></span> <span data-ttu-id="7c2f4-199">Wybierz **preferowana metoda kontaktu**.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="7c2f4-200">b.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-200">b.</span></span> <span data-ttu-id="7c2f4-201">Sprawdź, a następnie wprowadź szczegóły dotyczące kontaktu hello wymagane.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="7c2f4-202">Kliknij przycisk **Utwórz** toosubmit hello obsługi żądania.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="7c2f4-203">Po przesłaniu żądania obsługi pomocy technicznej platformy Azure skontaktuje się z Tobą.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="7c2f4-204">Pamiętaj, że Kończenie żądania hello może potrwać too2 dni roboczych.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="7c2f4-205">Zwiększ limit przydziału rdzeni subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7c2f4-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="7c2f4-206">Jeśli Twoje konto usługi partia zadań została utworzona w **subskrypcji użytkownika** tryb i potrzebujesz dodatkowych regionalnych lub wirtualna rodziny rdzeni żądania, a limit przydziału Zwiększ w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="7c2f4-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="7c2f4-207">Aby uzyskać instrukcje, zobacz [żądań Zwiększ limit przydziału rdzeni Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="7c2f4-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="7c2f4-208">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="7c2f4-208">Related topics</span></span>
* [<span data-ttu-id="7c2f4-209">Tworzenie konta usługi partia zadań Azure za pomocą portalu Azure hello</span><span class="sxs-lookup"><span data-stu-id="7c2f4-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="7c2f4-210">Omówienie funkcji usługi partia zadań Azure</span><span class="sxs-lookup"><span data-stu-id="7c2f4-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="7c2f4-211">Subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="7c2f4-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
