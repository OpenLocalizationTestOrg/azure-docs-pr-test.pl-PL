---
title: Anulowanie subskrypcji platformy Azure | Dokumentacja firmy Microsoft
description: "Opis sposobu anulowania subskrypcji platformy Azure, takich jak subskrypcji bezpłatnej wersji próbnej"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 3051d6b0-179f-4e3a-bda4-3fee7135eac5
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: genli
ms.openlocfilehash: c415fada30aa0b0bd9b9d1e416bc37ef30653f68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="cancel-your-subscription-for-azure"></a><span data-ttu-id="2d1fa-103">Anulowanie subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2d1fa-103">Cancel your subscription for Azure</span></span>

<span data-ttu-id="2d1fa-104">Możesz anulować subskrypcję platformy Azure jako [administratora konta](billing-subscription-transfer.md#whoisaa).</span><span class="sxs-lookup"><span data-stu-id="2d1fa-104">You can cancel your Azure subscription as the [Account Administrator](billing-subscription-transfer.md#whoisaa).</span></span> <span data-ttu-id="2d1fa-105">Po anulowaniu subskrypcji kończy się dostępu do usług platformy Azure i zasobów.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-105">After you cancel the subscription, your access to Azure services and resources ends.</span></span>

<span data-ttu-id="2d1fa-106">Zanim anulujesz subskrypcję:</span><span class="sxs-lookup"><span data-stu-id="2d1fa-106">Before you cancel your subscription:</span></span>

* <span data-ttu-id="2d1fa-107">Utwórz kopię zapasową danych.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-107">Back up your data.</span></span> <span data-ttu-id="2d1fa-108">Na przykład jeśli dane są przechowywane w magazynu Azure i SQL, Pobierz kopię.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-108">For example, if you're storing data in Azure storage or SQL, download a copy.</span></span> <span data-ttu-id="2d1fa-109">Jeśli maszynę wirtualną, Zapisz obraz ją lokalnie.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-109">If you have a virtual machine, save an image of it locally.</span></span>
* <span data-ttu-id="2d1fa-110">Zamknij usługi.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-110">Shut down your services.</span></span> <span data-ttu-id="2d1fa-111">Przejdź do [zasobów strony w portalu zarządzania](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), i **zatrzymać** wszelkie uruchomione maszyny wirtualne, aplikacji lub innych usług.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-111">Go to the [resources page in the management portal](https://ms.portal.azure.com/?flight=1#blade/HubsExtension/Resources/resourceType/Microsoft.Resources%2Fresources), and **Stop** any running virtual machines, applications, or other services.</span></span>
* <span data-ttu-id="2d1fa-112">Należy rozważyć przeprowadzenie migracji danych.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-112">Consider migrating your data.</span></span> <span data-ttu-id="2d1fa-113">Zobacz [przenoszenia zasobów do nowej grupy zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="2d1fa-113">See [Move resources to new resource group or subscription](../azure-resource-manager/resource-group-move-resources.md).</span></span>

<span data-ttu-id="2d1fa-114">Jeśli anulujesz płatna [plan pomocy technicznej platformy Azure](https://azure.microsoft.com/support/plans/), możesz nadal są naliczane co miesiąc w pozostałej części termin 6 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-114">If you cancel a paid [Azure Support plan](https://azure.microsoft.com/support/plans/), you are still billed monthly for the rest of the 6-months term.</span></span>

## <a name="cancel-subscription-using-the-azure-portal"></a><span data-ttu-id="2d1fa-115">Anulowanie subskrypcji przy użyciu portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2d1fa-115">Cancel subscription using the Azure portal</span></span>

1. <span data-ttu-id="2d1fa-116">Wybierz subskrypcję z [subskrypcji](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span><span class="sxs-lookup"><span data-stu-id="2d1fa-116">Select your subscription from the [Subscriptions page](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade).</span></span>

1. <span data-ttu-id="2d1fa-117">Wybierz subskrypcję, którą chcesz anulować i kliknij przycisk **anulować subskrypcję**.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-117">Select the subscription that you want to cancel and click **Cancel subscription**.</span></span>

    ![Zrzut ekranu pokazujący przycisk Anuluj](./media/billing-how-to-cancel-azure-subscription/cancel_ibiza.png)

1. <span data-ttu-id="2d1fa-119">Postępuj zgodnie z monitami i zakończenia anulowania.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-119">Follow prompts and finish cancellation.</span></span>

## <a name="cancel-subscription-using-the-azure-account-center"></a><span data-ttu-id="2d1fa-120">Anulowanie subskrypcji przy użyciu Centrum konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="2d1fa-120">Cancel subscription using the Azure Account Center</span></span>

1. <span data-ttu-id="2d1fa-121">Zaloguj się do [Centrum konta platformy Azure](https://account.windowsazure.com/subscriptions) jako administratora konta.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-121">Sign in to the [Azure Account Center](https://account.windowsazure.com/subscriptions) as the Account Administrator.</span></span>

1. <span data-ttu-id="2d1fa-122">W obszarze **kliknij subskrypcję, aby wyświetlić szczegóły i użycie**, zaznacz subskrypcję, którą chcesz anulować.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-122">Under **Click a subscription to view details and usage**, select the subscription that you want to cancel.</span></span>

    ![Zrzut ekranu pokazujący wybranej subskrypcji przykład](./media/billing-how-to-cancel-azure-subscription/Selectsub.png)

1. <span data-ttu-id="2d1fa-124">W prawej części strony, wybierz **Anuluj subskrypcję**.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-124">On the right side of the page, select **Cancel Subscription**.</span></span>

    ![Zrzut ekranu pokazujący przycisk Anuluj subskrypcję](./media/billing-how-to-cancel-azure-subscription/cancelsub.png)

1. <span data-ttu-id="2d1fa-126">Wybierz **tak, anulowanie subskrypcji**.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-126">Select **Yes, cancel my subscription**.</span></span>

    ![Zrzut ekranu pokazujący okno dialogowe Anuluj](./media/billing-how-to-cancel-azure-subscription/cancelbox.png)

1. <span data-ttu-id="2d1fa-128">Kliknij pozycję</span><span class="sxs-lookup"><span data-stu-id="2d1fa-128">Click</span></span> ![Zaznacz przycisk symbolu](./media/billing-how-to-cancel-azure-subscription/checkbutton.png) <span data-ttu-id="2d1fa-130">Aby zamknąć okno dialogowe i wrócić do strony swojego subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-130">to close the dialog window and return to your subscription page.</span></span>

## <a name="what-happens-after-i-cancel-my-subscription"></a><span data-ttu-id="2d1fa-131">Co się stanie po I anulowanie subskrypcji?</span><span class="sxs-lookup"><span data-stu-id="2d1fa-131">What happens after I cancel my subscription?</span></span>

<span data-ttu-id="2d1fa-132">Anulowanie, zatrzymaniu natychmiast rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-132">Once you cancel, billing is stopped immediately.</span></span> <span data-ttu-id="2d1fa-133">Jednak może potrwać do 10 minut pokazu anulowania w portalu.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-133">However, it can take up to 10 minutes for the cancellation show in the portal.</span></span>

<span data-ttu-id="2d1fa-134">Po wykonaniu tej usługi są wyłączone.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-134">After that, your services are disabled.</span></span> <span data-ttu-id="2d1fa-135">Oznacza to, maszynach wirtualnych są alokację tymczasowe adresy IP są zwalniane i magazynu jest tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-135">That means your virtual machines are deallocated, temporary IP addresses are freed, and storage is read-only.</span></span>

<span data-ttu-id="2d1fa-136">Chyba że w ramach bezpłatnej wersji próbnej lub masz punkty są rozliczane koszt opłat naliczanych oczekujących użycia wygenerowane między z ostatniego cyklu rozliczeniowego i datę anulowania.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-136">Unless you’re on a Free Trial or have credits available, you’re billed for any outstanding usage charges generated between your last billing cycle and the cancellation date.</span></span> <span data-ttu-id="2d1fa-137">Otrzymasz rachunku ostatniego końca cyklu rozliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-137">You get your last bill at the end of the billing cycle.</span></span>

<span data-ttu-id="2d1fa-138">Po anulowaniu subskrypcji oczekiwania 90 dni przed trwałe usunięcie danych w przypadku, gdy trzeba do niego dostęp, czy zmienisz zdanie.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-138">After you cancel your subscription, we wait 90 days before permanently deleting your data in case you need to access it or you change your mind.</span></span> <span data-ttu-id="2d1fa-139">Nie możemy pobierać przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-139">We don't charge you for retaining the data.</span></span> <span data-ttu-id="2d1fa-140">Aby dowiedzieć się więcej, zobacz [Microsoft Center Trust — jak możemy zarządzać danymi](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="2d1fa-140">To learn more, see [Microsoft Trust Center - How we manage your data](https://go.microsoft.com/fwLink/p/?LinkID=822930&clcid=0x409).</span></span>

## <a name="reactivate-subscription"></a><span data-ttu-id="2d1fa-141">Ponowne uaktywnianie subskrypcji</span><span class="sxs-lookup"><span data-stu-id="2d1fa-141">Reactivate subscription</span></span>

<span data-ttu-id="2d1fa-142">Jeśli anulujesz subskrypcję z przypadkowo, możesz [uaktywnić go ponownie w Centrum konta](billing-subscription-become-disable.md).</span><span class="sxs-lookup"><span data-stu-id="2d1fa-142">If you cancel your Pay-As-You-Go subscription accidentally, you can [reactivate it in the Accounts Center](billing-subscription-become-disable.md).</span></span>

<span data-ttu-id="2d1fa-143">Jeśli Twoja subskrypcja nie jest płatność za rzeczywiste użycie, się z pomocą techniczną w ciągu 90 dni od anulowania, aby ponownie aktywować subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-143">If your subscription is not Pay-As-You-Go, contact support within 90 days of cancellation to reactivate your subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="2d1fa-144">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="2d1fa-144">Need help?</span></span> <span data-ttu-id="2d1fa-145">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-145">Contact support.</span></span>

<span data-ttu-id="2d1fa-146">Jeśli nadal masz pytania, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="2d1fa-146">If you still have questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
