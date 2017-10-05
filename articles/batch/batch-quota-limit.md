---
title: "Usługa przydziały i limity dla partii zadań Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat przydziałów domyślnych partii zadań Azure, ograniczenia i ograniczenia i zwiększa jak utworzyć żądanie przydziału"
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
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="2e29b-103">Limity przydziału i limity usługi Batch</span><span class="sxs-lookup"><span data-stu-id="2e29b-103">Batch service quotas and limits</span></span>

<span data-ttu-id="2e29b-104">Zgodnie z innymi usługami Azure, istnieją ograniczenia na niektóre zasoby skojarzone z usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="2e29b-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="2e29b-105">Wiele tych limitów jest przydziałów domyślnych zastosowane przez platformę Azure na poziomie konta lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2e29b-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="2e29b-106">W tym artykule omówiono te ustawienia domyślne, i jak mogą żądać przydziału zwiększa.</span><span class="sxs-lookup"><span data-stu-id="2e29b-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="2e29b-107">Pamiętaj o tych limitach przydziału podczas projektowania i skalowania obciążeń usługi Batch.</span><span class="sxs-lookup"><span data-stu-id="2e29b-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="2e29b-108">Na przykład jeśli pulę nie jest osiągnięciu docelowej liczby węzłów obliczeniowych, określonych przez Ciebie, może osiągnięto limit przydziału rdzeni dla swojego konta usługi partia zadań lub regionalnych przydziału rdzeni maszyn wirtualnych dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2e29b-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="2e29b-109">Można uruchomić wiele obciążeń usługi Batch na jednym koncie usługi Batch lub rozdzielić obciążenia pomiędzy konta tej usługi znajdujące się w jednej subskrypcji, ale różnych regionach świadczenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="2e29b-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="2e29b-110">Jeśli planujesz uruchamianie obciążeń produkcyjnych w partii, może być konieczne zwiększyć co najmniej jeden przydziały powyżej domyślny.</span><span class="sxs-lookup"><span data-stu-id="2e29b-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="2e29b-111">Jeśli użytkownik chce podnieść limit przydziału, możesz otworzyć online [żądania obsługi klienta](#increase-a-quota) bez dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="2e29b-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="2e29b-112">Limit przydziału jest limit kredytu nie gwarancji pojemności.</span><span class="sxs-lookup"><span data-stu-id="2e29b-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="2e29b-113">Jeśli wymagana pojemność na dużą skalę, skontaktuj się z pomocą techniczną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2e29b-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="2e29b-114">Limity przydziałów zasobów</span><span class="sxs-lookup"><span data-stu-id="2e29b-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="2e29b-115">Przydziały w trybie użytkownika subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2e29b-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="2e29b-116">Dla konta wsadowego z trybem przydziału puli ustawioną **subskrypcji użytkownika**, partii maszyny wirtualne i inne zasoby, takie jak kont magazynu, są tworzone bezpośrednio w ramach Twojej subskrypcji po utworzeniu puli.</span><span class="sxs-lookup"><span data-stu-id="2e29b-116">For a Batch account with pool allocation mode set to **user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="2e29b-117">Limit przydziału rdzeni partii zadań Azure nie ma zastosowania do konto utworzone w tym trybie.</span><span class="sxs-lookup"><span data-stu-id="2e29b-117">The Azure Batch cores quota does not apply to an account created in this mode.</span></span> <span data-ttu-id="2e29b-118">Zamiast tego przydziały w subskrypcji dla regionalne obliczeniowe rdzeni i inne zasoby są stosowane.</span><span class="sxs-lookup"><span data-stu-id="2e29b-118">Instead, the quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="2e29b-119">Dowiedz się więcej o te przydziały w [subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="2e29b-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="2e29b-120">Podczas planowania użycia zasobów dla konto utworzone w trybie użytkownika subskrypcji, należy pamiętać, że następujące zasoby partii (oprócz obliczeń rdzenie) są wymagane dla każdego 40 maszyn wirtualnych systemu Linux lub 20 maszyn wirtualnych systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="2e29b-120">When planning resource usage for an account created in user subscription mode, note the following Batch resources (in addition to compute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="2e29b-121">Zasób</span><span class="sxs-lookup"><span data-stu-id="2e29b-121">Resource</span></span> | <span data-ttu-id="2e29b-122">Przydział</span><span class="sxs-lookup"><span data-stu-id="2e29b-122">Quota</span></span> | <span data-ttu-id="2e29b-123">Dostawca</span><span class="sxs-lookup"><span data-stu-id="2e29b-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="2e29b-124">Jedno konto magazynu</span><span class="sxs-lookup"><span data-stu-id="2e29b-124">One storage account</span></span> | <span data-ttu-id="2e29b-125">Konta magazynu</span><span class="sxs-lookup"><span data-stu-id="2e29b-125">Storage Accounts</span></span> | <span data-ttu-id="2e29b-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="2e29b-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="2e29b-127">Jeden publiczny adres IP</span><span class="sxs-lookup"><span data-stu-id="2e29b-127">One public IP address</span></span> | <span data-ttu-id="2e29b-128">Publiczne adresy IP</span><span class="sxs-lookup"><span data-stu-id="2e29b-128">Public IP Addresses</span></span> | <span data-ttu-id="2e29b-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="2e29b-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="2e29b-130">Jedną sieć wirtualną</span><span class="sxs-lookup"><span data-stu-id="2e29b-130">One virtual network</span></span> | <span data-ttu-id="2e29b-131">Sieci wirtualne</span><span class="sxs-lookup"><span data-stu-id="2e29b-131">Virtual Networks</span></span> | <span data-ttu-id="2e29b-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="2e29b-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="2e29b-133">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="2e29b-133">One network security group</span></span> | <span data-ttu-id="2e29b-134">Grupy zabezpieczeń sieci</span><span class="sxs-lookup"><span data-stu-id="2e29b-134">Network Security Groups</span></span> | <span data-ttu-id="2e29b-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="2e29b-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="2e29b-136">Jeden zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="2e29b-136">One virtual machine scale set</span></span> | <span data-ttu-id="2e29b-137">Zestawy skali maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="2e29b-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="2e29b-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="2e29b-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="2e29b-139">Jedna usługa równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="2e29b-139">One load balancer</span></span> | <span data-ttu-id="2e29b-140">Moduły równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="2e29b-140">Load Balancers</span></span> | <span data-ttu-id="2e29b-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="2e29b-141">Microsoft.Network</span></span> | 

<span data-ttu-id="2e29b-142">Należy ustawić limit przydziału rdzeni na poziomie regionalnym lub na rodzinę maszyny Wirtualnej na podstawie rozmiaru maszyny Wirtualnej wymagana dla puli partii lub pule:</span><span class="sxs-lookup"><span data-stu-id="2e29b-142">The cores quota at a regional level or per VM family should be set according to the VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="2e29b-143">Przydział</span><span class="sxs-lookup"><span data-stu-id="2e29b-143">Quota</span></span> | <span data-ttu-id="2e29b-144">Dostawca</span><span class="sxs-lookup"><span data-stu-id="2e29b-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="2e29b-145">Całkowita liczba rdzeni regionalne</span><span class="sxs-lookup"><span data-stu-id="2e29b-145">Total Regional Cores</span></span> | <span data-ttu-id="2e29b-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="2e29b-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="2e29b-147">…</span><span class="sxs-lookup"><span data-stu-id="2e29b-147">…</span></span> <span data-ttu-id="2e29b-148">Rodziny rdzeni</span><span class="sxs-lookup"><span data-stu-id="2e29b-148">Family Cores</span></span> | <span data-ttu-id="2e29b-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="2e29b-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="2e29b-150">Inne ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="2e29b-150">Other limits</span></span>
| <span data-ttu-id="2e29b-151">**Zasób**</span><span class="sxs-lookup"><span data-stu-id="2e29b-151">**Resource**</span></span> | <span data-ttu-id="2e29b-152">**Limit maksymalny**</span><span class="sxs-lookup"><span data-stu-id="2e29b-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="2e29b-153">[Równoczesnych zadań](batch-parallel-node-tasks.md) na węzeł obliczeń</span><span class="sxs-lookup"><span data-stu-id="2e29b-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="2e29b-154">4 x liczba rdzeni węzła</span><span class="sxs-lookup"><span data-stu-id="2e29b-154">4 x number of node cores</span></span> |
| <span data-ttu-id="2e29b-155">[Aplikacje](batch-application-packages.md) na konto usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="2e29b-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="2e29b-156">20</span><span class="sxs-lookup"><span data-stu-id="2e29b-156">20</span></span> |
| <span data-ttu-id="2e29b-157">Pakiety aplikacji na aplikację</span><span class="sxs-lookup"><span data-stu-id="2e29b-157">Application packages per application</span></span> |<span data-ttu-id="2e29b-158">40</span><span class="sxs-lookup"><span data-stu-id="2e29b-158">40</span></span> |
| <span data-ttu-id="2e29b-159">Rozmiar pakietu aplikacji (wszystkie)</span><span class="sxs-lookup"><span data-stu-id="2e29b-159">Application package size (each)</span></span> |<span data-ttu-id="2e29b-160">Około 195GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="2e29b-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="2e29b-161">Maksymalna początkowy rozmiar zadań</span><span class="sxs-lookup"><span data-stu-id="2e29b-161">Maximum start task size</span></span> | <span data-ttu-id="2e29b-162">znaki 32768<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="2e29b-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="2e29b-163"><sup>1</sup> limit bloku maksymalny rozmiar obiektu blob magazynu azure</span><span class="sxs-lookup"><span data-stu-id="2e29b-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="2e29b-164">
<sup>2</sup> obejmuje plików zasobów i zmienne środowiskowe</span><span class="sxs-lookup"><span data-stu-id="2e29b-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="2e29b-165">Przydziały partii widoku</span><span class="sxs-lookup"><span data-stu-id="2e29b-165">View Batch quotas</span></span>
<span data-ttu-id="2e29b-166">Wyświetl przydziałami konta wsadowego w [portalu Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="2e29b-166">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="2e29b-167">Wybierz **partii kont** w portalu, a następnie wybierz konto usługi partia zadań interesuje Cię.</span><span class="sxs-lookup"><span data-stu-id="2e29b-167">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="2e29b-168">Wybierz **właściwości** w bloku menu konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="2e29b-168">Select **Properties** on the Batch account's menu blade.</span></span>
3. <span data-ttu-id="2e29b-169">Wyświetla bloku właściwości **przydziały** zastosowanym do konta usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="2e29b-169">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![Przydziały konta usługi partia zadań][account_quotas]

<span data-ttu-id="2e29b-171">Dla konta wsadowego, utworzony w trybie użytkownika subskrypcji należy wyświetlić przydziały pokrewne subskrypcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2e29b-171">For a Batch account created in user subscription mode, view the related subscription quotas in the Azure Portal.</span></span>

1. <span data-ttu-id="2e29b-172">Wybierz **subskrypcje**i wybierz subskrypcję, której używasz dla konta usługi partia zadań.</span><span class="sxs-lookup"><span data-stu-id="2e29b-172">Select **Subscriptions**, and select the subscription you are using for the Batch account.</span></span>

2. <span data-ttu-id="2e29b-173">Na **subskrypcji** bloku, wybierz opcję **użycia + przydziały**.</span><span class="sxs-lookup"><span data-stu-id="2e29b-173">On the **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="2e29b-174">Zwiększ limit przydziału</span><span class="sxs-lookup"><span data-stu-id="2e29b-174">Increase a quota</span></span>
<span data-ttu-id="2e29b-175">Wykonaj następujące kroki, aby zażądać przydział zwiększyć dla swojego konta usługi partia zadań lub subskrypcją za pomocą [portalu Azure][portal].</span><span class="sxs-lookup"><span data-stu-id="2e29b-175">Follow these steps to request a quota increase for your Batch account or your subscription using the [Azure portal][portal].</span></span> <span data-ttu-id="2e29b-176">Typ zwiększenia limitu przydziału zależy od trybu alokacji puli konta partii zadań.</span><span class="sxs-lookup"><span data-stu-id="2e29b-176">The type of quota increase depends on the pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="2e29b-177">Zwiększ limit przydziału rdzeni partii</span><span class="sxs-lookup"><span data-stu-id="2e29b-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="2e29b-178">Jeśli Twoje konto usługi partia zadań została utworzona w **partii usługi** tryb, wykonaj następujące kroki, aby zażądać przydziału rdzeni partii zwiększyć:</span><span class="sxs-lookup"><span data-stu-id="2e29b-178">If your Batch account was created in **Batch service** mode, follow these steps to request a Batch cores quota increase:</span></span>

1. <span data-ttu-id="2e29b-179">Wybierz **Pomoc i obsługa techniczna** kafelka na pulpicie nawigacyjnym portalu lub znak zapytania (**?**) w prawym górnym rogu portalu.</span><span class="sxs-lookup"><span data-stu-id="2e29b-179">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="2e29b-180">Wybierz **nowy obsługuje żądania** > **podstawy**.</span><span class="sxs-lookup"><span data-stu-id="2e29b-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="2e29b-181">Na **podstawy** bloku:</span><span class="sxs-lookup"><span data-stu-id="2e29b-181">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="2e29b-182">a.</span><span class="sxs-lookup"><span data-stu-id="2e29b-182">a.</span></span> <span data-ttu-id="2e29b-183">**Wystawianie typu** > **przydziału**</span><span class="sxs-lookup"><span data-stu-id="2e29b-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="2e29b-184">b.</span><span class="sxs-lookup"><span data-stu-id="2e29b-184">b.</span></span> <span data-ttu-id="2e29b-185">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="2e29b-185">Select your subscription.</span></span>
   
    <span data-ttu-id="2e29b-186">c.</span><span class="sxs-lookup"><span data-stu-id="2e29b-186">c.</span></span> <span data-ttu-id="2e29b-187">**Typ limitu przydziału** > **partii**</span><span class="sxs-lookup"><span data-stu-id="2e29b-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="2e29b-188">d.</span><span class="sxs-lookup"><span data-stu-id="2e29b-188">d.</span></span> <span data-ttu-id="2e29b-189">**Plan pomocy technicznej** > **Obsługa przydziałów — włączone**</span><span class="sxs-lookup"><span data-stu-id="2e29b-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="2e29b-190">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2e29b-190">Click **Next**.</span></span>
4. <span data-ttu-id="2e29b-191">Na **Problem** bloku:</span><span class="sxs-lookup"><span data-stu-id="2e29b-191">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="2e29b-192">a.</span><span class="sxs-lookup"><span data-stu-id="2e29b-192">a.</span></span> <span data-ttu-id="2e29b-193">Wybierz **ważność** zgodnie z [wpływ na prowadzoną działalność][support_sev].</span><span class="sxs-lookup"><span data-stu-id="2e29b-193">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="2e29b-194">b.</span><span class="sxs-lookup"><span data-stu-id="2e29b-194">b.</span></span> <span data-ttu-id="2e29b-195">W **szczegóły**, określ każdego przydziału, aby zmienić nazwę konta wsadowego i nowego limitu.</span><span class="sxs-lookup"><span data-stu-id="2e29b-195">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="2e29b-196">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2e29b-196">Click **Next**.</span></span>
5. <span data-ttu-id="2e29b-197">Na **informacje kontaktowe** bloku:</span><span class="sxs-lookup"><span data-stu-id="2e29b-197">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="2e29b-198">a.</span><span class="sxs-lookup"><span data-stu-id="2e29b-198">a.</span></span> <span data-ttu-id="2e29b-199">Wybierz **preferowana metoda kontaktu**.</span><span class="sxs-lookup"><span data-stu-id="2e29b-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="2e29b-200">b.</span><span class="sxs-lookup"><span data-stu-id="2e29b-200">b.</span></span> <span data-ttu-id="2e29b-201">Sprawdź i wprowadź wymagane szczegóły dotyczące kontaktu.</span><span class="sxs-lookup"><span data-stu-id="2e29b-201">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="2e29b-202">Kliknij przycisk **Utwórz**, aby przesłać żądanie pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2e29b-202">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="2e29b-203">Po przesłaniu żądania obsługi pomocy technicznej platformy Azure skontaktuje się z Tobą.</span><span class="sxs-lookup"><span data-stu-id="2e29b-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="2e29b-204">Należy pamiętać, że wykonywania żądania może potrwać maksymalnie 2 dni roboczych.</span><span class="sxs-lookup"><span data-stu-id="2e29b-204">Note that completing the request can take up to 2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="2e29b-205">Zwiększ limit przydziału rdzeni subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2e29b-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="2e29b-206">Jeśli Twoje konto usługi partia zadań została utworzona w **subskrypcji użytkownika** tryb i potrzebujesz dodatkowych regionalnych lub wirtualna rodziny rdzeni żądania, a limit przydziału Zwiększ w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2e29b-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="2e29b-207">Aby uzyskać instrukcje, zobacz [żądań Zwiększ limit przydziału rdzeni Resource Manager](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="2e29b-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="2e29b-208">Powiązane tematy</span><span class="sxs-lookup"><span data-stu-id="2e29b-208">Related topics</span></span>
* [<span data-ttu-id="2e29b-209">Tworzenie konta usługi partia zadań Azure za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2e29b-209">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="2e29b-210">Omówienie funkcji usługi partia zadań Azure</span><span class="sxs-lookup"><span data-stu-id="2e29b-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="2e29b-211">Subskrypcji platformy Azure i usługi limity, przydziały i ograniczenia</span><span class="sxs-lookup"><span data-stu-id="2e29b-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG
