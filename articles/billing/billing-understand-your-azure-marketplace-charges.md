---
title: "Zrozumienie sieci Azure koszty usługi zewnętrzne | Dokumentacja firmy Microsoft"
description: "Informacje o rozliczeniach usług zewnętrznych, wcześniej znana jako Marketplace, opłaty na platformie Azure."
services: 
documentationcenter: 
author: adpick
manager: tonguyen
editor: 
tags: billing
ms.assetid: 5e0e2a3c-d111-4054-8508-0c111c1b749b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: adpick
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 11701ce0162113ef6c8e056d3a30fe1d8f702f92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="understand-your-azure-billing-for-external-service-charges"></a><span data-ttu-id="36ba8-103">Zrozumienie dla zewnętrznych opłaty za usługę Azure rozliczeniowego</span><span class="sxs-lookup"><span data-stu-id="36ba8-103">Understand your Azure billing for external service charges</span></span>
<span data-ttu-id="36ba8-104">Usługi zewnętrzne używane do można wywołać portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="36ba8-104">External services used to be called Azure Marketplace.</span></span> <span data-ttu-id="36ba8-105">Ogólnie rzecz biorąc są w przypadku usług opublikowanych przez strony trzecie dostępne dla platformy Azure, ale są zintegrowane całkowicie w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36ba8-105">Generally, they're services published by third-parties available for Azure but are integrated completely within Azure.</span></span> <span data-ttu-id="36ba8-106">Na przykład ClearDB i SendGrid są usług zewnętrznych, które można kupić na platformie Azure, ale nie są publikowane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="36ba8-106">For example, ClearDB and SendGrid are external services that you can purchase in Azure, but are not published by Microsoft.</span></span>

<span data-ttu-id="36ba8-107">Podczas obsługi administracyjnej nowych zewnętrznej usługi lub zasobu, wyświetlane jest ostrzeżenie:</span><span class="sxs-lookup"><span data-stu-id="36ba8-107">When you provision a new external service or resource, a warning is shown:</span></span>

![Ostrzeżenie zakupu Marketplace](./media/billing-understand-your-azure-marketplace-charges/marketplace-warning.PNG)

> [!NOTE]
> <span data-ttu-id="36ba8-109">Zewnętrznych usług są publikowane przez firmy, które nie są firmy Microsoft, ale czasami produktów firmy Microsoft są również podzielone na usług zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="36ba8-109">External services are published by companies that are not Microsoft, but sometimes Microsoft products are also categorized as external services.</span></span>
> 
> 

## <a name="how-external-services-are-billed"></a><span data-ttu-id="36ba8-110">W jaki sposób są rozliczane usług zewnętrznych</span><span class="sxs-lookup"><span data-stu-id="36ba8-110">How external services are billed</span></span>
- <span data-ttu-id="36ba8-111">Zewnętrznych usług są rozliczane oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="36ba8-111">External services are billed separately.</span></span> <span data-ttu-id="36ba8-112">Są one traktowane jako pojedyncze zamówienia w ramach Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="36ba8-112">They are treated as individual orders within your Azure subscription.</span></span> <span data-ttu-id="36ba8-113">Okresie rozliczeniowym dla każdej usługi jest ustawiana po zakupie usługi.</span><span class="sxs-lookup"><span data-stu-id="36ba8-113">The billing period for each service is set when you purchase the service.</span></span> <span data-ttu-id="36ba8-114">Nie należy mylić z okresu rozliczeniowego subskrypcji, w ramach którego go zakupiono.</span><span class="sxs-lookup"><span data-stu-id="36ba8-114">Not to be confused with the billing period of the subscription under which you purchased it.</span></span> <span data-ttu-id="36ba8-115">Otrzymasz również oddzielne rachunków i karty kredytowej jest naliczane osobno.</span><span class="sxs-lookup"><span data-stu-id="36ba8-115">You also receive separate bills and your credit card is charged separately.</span></span>
- <span data-ttu-id="36ba8-116">Każda usługa zewnętrzny ma inny model rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="36ba8-116">Each external service has a different billing model.</span></span> <span data-ttu-id="36ba8-117">Niektóre usługi są rozliczane w sposób płatności obejmujące, podczas gdy inne miesięczne płatności na podstawie modelu.</span><span class="sxs-lookup"><span data-stu-id="36ba8-117">Some services are billed in a pay-as-you-go fashion while others use a monthly based payment model.</span></span> <span data-ttu-id="36ba8-118">Karty kredytowej jest wymagane dla zewnętrznych usług Azure, nie można kupić usług zewnętrznych o płatności faktury.</span><span class="sxs-lookup"><span data-stu-id="36ba8-118">You need a credit card for Azure external services, you can't buy external services with invoice pay.</span></span>
- <span data-ttu-id="36ba8-119">Nie można użyć miesięczne bezpłatnych środków dla usług zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="36ba8-119">You can't use monthly free credits for external services.</span></span> <span data-ttu-id="36ba8-120">Jeśli używasz subskrypcji platformy Azure, która obejmuje [wolne środków](https://azure.microsoft.com/pricing/spending-limits/), nie można zastosować do BOM zewnętrznej usługi.</span><span class="sxs-lookup"><span data-stu-id="36ba8-120">If you are using an Azure subscription that includes [free credits](https://azure.microsoft.com/pricing/spending-limits/), they can't be applied to external service bills.</span></span> <span data-ttu-id="36ba8-121">Za pomocą karty kredytowej kupić usług zewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="36ba8-121">Use a credit card to purchase external services.</span></span>


## <a name="view-external-service-spending-and-history-in-the-azure-portal"></a><span data-ttu-id="36ba8-122">Widok zewnętrznej usługi wydatków i historię w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="36ba8-122">View external service spending and history in the Azure portal</span></span>
<span data-ttu-id="36ba8-123">Można wyświetlić listę usług zewnętrznych, które znajdują się na każdej subskrypcji w ramach [portalu Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="36ba8-123">You can view a list of the external services that are on each subscription within the [Azure portal](https://portal.azure.com/):</span></span> 

1. <span data-ttu-id="36ba8-124">Zaloguj się do [portalu Azure](https://portal.azure.com/) jako administratora konta.</span><span class="sxs-lookup"><span data-stu-id="36ba8-124">Sign in to the [Azure portal](https://portal.azure.com/) as the account administrator.</span></span>
2. <span data-ttu-id="36ba8-125">W menu Centrum wybierz **subskrypcje**.</span><span class="sxs-lookup"><span data-stu-id="36ba8-125">In the Hub menu, select **Subscriptions**.</span></span>
   
    ![W menu Centrum Wybierz subskrypcje](./media/billing-understand-your-azure-marketplace-charges/sub-button.png) 
3. <span data-ttu-id="36ba8-127">W **subskrypcje** bloku, wybierz subskrypcję, którą chcesz wyświetlić, a następnie wybierz **usług zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="36ba8-127">In the **Subscriptions** blade, select the subscription that you want to view, and then select **External services**.</span></span>
   
    ![Wybierz subskrypcję w bloku rozliczeń](./media/billing-understand-your-azure-marketplace-charges/select-sub-external-services.png)
4. <span data-ttu-id="36ba8-129">Powinna zostać wyświetlona każdego zamówień zewnętrznej usługi, nazwę wydawcy, warstwy usług, których używasz, nazwa nadana zasób i bieżący stan zlecenia.</span><span class="sxs-lookup"><span data-stu-id="36ba8-129">You should see each of your external service orders, the publisher name, service tier you bought, name you gave the resource, and the current order status.</span></span> <span data-ttu-id="36ba8-130">Aby wyświetlić poza rachunków, wybierz zewnętrznej usługi.</span><span class="sxs-lookup"><span data-stu-id="36ba8-130">To see past bills, select an external service.</span></span>
   
    ![Wybierz zewnętrznej usługi](./media/billing-understand-your-azure-marketplace-charges/external-service-blade2.png)
5. <span data-ttu-id="36ba8-132">W tym miejscu można wyświetlić poza tym podział podatku kwoty rachunku.</span><span class="sxs-lookup"><span data-stu-id="36ba8-132">From here, you can view past bill amounts including the tax breakdown.</span></span>
   
    ![Widok usług zewnętrznych historię rozliczeń](./media/billing-understand-your-azure-marketplace-charges/billing-overview-blade.png)

## <a name="view-external-service-spending-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="36ba8-134">Zewnętrzna usługa widoku wydatków dla klientów Enterprise Agreement (EA)</span><span class="sxs-lookup"><span data-stu-id="36ba8-134">View external service spending for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="36ba8-135">Zobacz wydatków zewnętrznej usługi klientom EA i pobierania raportów w portalu EA.</span><span class="sxs-lookup"><span data-stu-id="36ba8-135">EA customers can see external service spending and download reports in the EA portal.</span></span> <span data-ttu-id="36ba8-136">Zobacz [Azure Marketplace w celu EA klienci](https://ea.azure.com/helpdocs/azureMarketplace) rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="36ba8-136">See [Azure Marketplace for EA Customers](https://ea.azure.com/helpdocs/azureMarketplace) to get started.</span></span>

## <a name="manage-payment-methods-for-external-service-orders"></a><span data-ttu-id="36ba8-137">Zarządzanie formy płatności dla zewnętrznych zleceniami</span><span class="sxs-lookup"><span data-stu-id="36ba8-137">Manage payment methods for external service orders</span></span>
<span data-ttu-id="36ba8-138">Aktualizowanie metody płatności zamówień zewnętrznej usługi z [Centrum konta](https://account.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="36ba8-138">Update your payment methods for external service orders from the [Account Center](https://account.windowsazure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="36ba8-139">Jeśli zakupiono subskrypcję za pomocą konta służbowego [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) wprowadzać zmiany do metody płatności.</span><span class="sxs-lookup"><span data-stu-id="36ba8-139">If you purchased your subscription with a Work or School account, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to make changes to your payment method.</span></span>
> 
> 

1. <span data-ttu-id="36ba8-140">Zaloguj się do [Centrum konta](https://account.windowsazure.com/) i [przejdź do **marketplace** kartę](https://account.windowsazure.com/Store)</span><span class="sxs-lookup"><span data-stu-id="36ba8-140">Sign in to the [Account Center](https://account.windowsazure.com/) and [navigate to the **marketplace** tab](https://account.windowsazure.com/Store)</span></span>
   
    ![Wybierz w Centrum konta witryny marketplace](./media/billing-understand-your-azure-marketplace-charges/select-marketplace.png)
2. <span data-ttu-id="36ba8-142">Wybierz usługę zewnętrznych, którą chcesz zarządzać</span><span class="sxs-lookup"><span data-stu-id="36ba8-142">Select the external service you want to manage</span></span>
   
    ![Wybierz usługę zewnętrznych, którą chcesz zarządzać](./media/billing-understand-your-azure-marketplace-charges/select-ext-service.png)
3. <span data-ttu-id="36ba8-144">Kliknij przycisk **Zmień formę płatności** w prawej części strony.</span><span class="sxs-lookup"><span data-stu-id="36ba8-144">Click **Change payment method** on the right side of the page.</span></span> <span data-ttu-id="36ba8-145">To łącze powoduje przeniesienie do innego portalu do zarządzania formy płatności.</span><span class="sxs-lookup"><span data-stu-id="36ba8-145">This link brings you to a different portal to manage your payment method.</span></span>
   
    ![Podsumowanie zlecenia](./media/billing-understand-your-azure-marketplace-charges/change-payment.PNG)
4. <span data-ttu-id="36ba8-147">Kliknij przycisk **Edytuj informacje o** i postępuj zgodnie z instrukcjami, aby zaktualizować dane o płatności.</span><span class="sxs-lookup"><span data-stu-id="36ba8-147">Click **Edit info** and follow instructions to update your payment information.</span></span>
   
    ![Wybierz pozycję Edytuj informacje](./media/billing-understand-your-azure-marketplace-charges/edit-info.png)

## <a name="cancel-an-external-service-order"></a><span data-ttu-id="36ba8-149">Anulowanie zamówienia zewnętrznej usługi</span><span class="sxs-lookup"><span data-stu-id="36ba8-149">Cancel an external service order</span></span>
<span data-ttu-id="36ba8-150">Jeśli chcesz anulować zamówienia zewnętrznej usługi, Usuń zasób w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="36ba8-150">If you want to cancel your external service order, delete the resource in the [Azure portal](https://portal.azure.com).</span></span>

![Usuwanie zasobu](./media/billing-understand-your-azure-marketplace-charges/deleteMarketplaceOrder.PNG)

## <a name="need-help-contact-support"></a><span data-ttu-id="36ba8-152">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="36ba8-152">Need help?</span></span> <span data-ttu-id="36ba8-153">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="36ba8-153">Contact support.</span></span>
<span data-ttu-id="36ba8-154">Jeśli nadal masz pytania, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="36ba8-154">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>

