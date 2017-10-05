---
title: "Ustawianie alertów rozliczeń lub faktury dla subskrypcji platformy Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak można skonfigurować alerty na rachunku Azure, aby uniknąć niespodzianki rozliczeń."
keywords: "środki alert, alert rozliczeń"
services: 
documentationcenter: 
author: vikdesai
manager: tonguyen
editor: 
tags: billing
ms.assetid: 9b7b3eeb-cd9d-4690-86a3-51b1e2a8974f
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: vikdesai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7a1b579fdde831fdc3afa0a2aee4c24890216ed1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="a7c95-104">Ustawianie alertów rozliczeń lub faktury dla subskrypcji platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a7c95-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="a7c95-105">Jeśli jesteś administratorem konta subskrypcji platformy Azure, aby utworzyć dostosowany, można użyć Usługa alertów rozliczenia Azure alerty dotyczące rozliczeń, które ułatwiają monitorowanie działań i zarządzania nimi rozliczeń dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a7c95-105">If you’re the Account Admin for an Azure subscription, you can use the Azure Billing Alert Service to create customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="a7c95-106">Ta usługa jest w wersji zapoznawczej, więc należy ją najpierw włączyć na stronie funkcji w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="a7c95-106">This service is in preview, so you need to enable it in the Preview Features page first.</span></span>

## <a name="set-the-alert-threshold-and-email-recipients"></a><span data-ttu-id="a7c95-107">Ustawiony próg i adres e-mail odbiorcy alertów</span><span class="sxs-lookup"><span data-stu-id="a7c95-107">Set the alert threshold and email recipients</span></span>
1. <span data-ttu-id="a7c95-108">Odwiedź stronę [strona funkcje w wersji zapoznawczej](https://account.windowsazure.com/PreviewFeatures) i Włącz **rozliczeń Usługa alertów**.</span><span class="sxs-lookup"><span data-stu-id="a7c95-108">Visit [the Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="a7c95-109">Po otrzymaniu potwierdzenie adresu e-mail, który usługa rozliczeń jest włączona dla Twojej subskrypcji, odwiedź stronę [stronie subskrypcji](https://account.windowsazure.com/Subscriptions) w portalu konta.</span><span class="sxs-lookup"><span data-stu-id="a7c95-109">After you receive the email confirmation that the billing service is turned on for your subscription, visit [the Subscriptions page](https://account.windowsazure.com/Subscriptions) in the account portal.</span></span> <span data-ttu-id="a7c95-110">Kliknij subskrypcję, którą chcesz monitorować, a następnie kliknij przycisk **alerty**.</span><span class="sxs-lookup"><span data-stu-id="a7c95-110">Click the subscription you want to monitor, and then click **Alerts**.</span></span>

    ![Zrzut ekranu przedstawiający widok subskrypcji Centrum konta platformy Azure, z wyróżnionym alerty][Image1]

2. <span data-ttu-id="a7c95-112">Następnie kliknij przycisk **dodać alertu** utworzyć pierwsza.</span><span class="sxs-lookup"><span data-stu-id="a7c95-112">Next, click **Add Alert** to create your first one.</span></span> <span data-ttu-id="a7c95-113">Można skonfigurować łącznie pięć alerty dotyczące rozliczeń dla subskrypcji, z różnych próg i maksymalnie dwóch adresatów wiadomości e-mail o każdym alercie.</span><span class="sxs-lookup"><span data-stu-id="a7c95-113">You can set up a total of five billing alerts per subscription, with a different threshold and up to two email recipients for each alert.</span></span>

    ![Zrzut ekranu przedstawiający widok alertów, w którym można dodać alertu][Image2]

3. <span data-ttu-id="a7c95-115">Po dodaniu alert nadaj unikatową nazwę, wybierz próg wydatków i wybrać adresy e-mail, gdy alerty są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="a7c95-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose the email addresses where alerts are sent.</span></span> <span data-ttu-id="a7c95-116">Podczas ustawiania wartości progowej, można wybrać jedną **rozliczeń całkowita** lub **środki pieniężne** z **alertów dla** listy.</span><span class="sxs-lookup"><span data-stu-id="a7c95-116">When setting up the threshold, you can choose either a **Billing Total** or a **Monetary Credit** from the **Alert For** list.</span></span> <span data-ttu-id="a7c95-117">Łącznie rozliczeń alert jest wysyłany, gdy subskrypcja wydatków przekracza wartość progową.</span><span class="sxs-lookup"><span data-stu-id="a7c95-117">For a billing total, an alert is sent when subscription spending exceeds the threshold.</span></span> <span data-ttu-id="a7c95-118">Uzyskać środki pieniężne alert jest wysyłany, gdy kwota środków pieniężnych spadnie poniżej limitu.</span><span class="sxs-lookup"><span data-stu-id="a7c95-118">For a monetary credit, an alert is sent when monetary credits drop below the limit.</span></span> <span data-ttu-id="a7c95-119">Kwota środków pieniężnych zazwyczaj mają zastosowanie do subskrypcji bezpłatnej wersji próbnej i Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a7c95-119">Monetary credits usually apply to Free Trial and Visual Studio subscriptions.</span></span>

    ![Zrzut ekranu przedstawiający widok dodawania alertów, którym można skonfigurować adresatów][Image3]

<span data-ttu-id="a7c95-121">Azure obsługuje dowolnego adresu e-mail, ale nie Sprawdź, czy działa adres e-mail, więc dokładnie literówki.</span><span class="sxs-lookup"><span data-stu-id="a7c95-121">Azure supports any email address but doesn't verify that the email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="a7c95-122">Sprawdź alerty</span><span class="sxs-lookup"><span data-stu-id="a7c95-122">Check on your alerts</span></span>
<span data-ttu-id="a7c95-123">Po skonfigurowaniu alerty Centrum konta je i pokazuje, ile więcej można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="a7c95-123">After you set up alerts, the Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="a7c95-124">Dla każdego alertu Zobacz Data i godzina wysłania, czy jest alert dotyczący rozliczeń całkowita lub środki pieniężne i skonfigurowanego limitu.</span><span class="sxs-lookup"><span data-stu-id="a7c95-124">For each alert, you see the date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and the limit you set up.</span></span> <span data-ttu-id="a7c95-125">Format daty i godziny jest 24-godzinnym koordynować czasu uniwersalnego (UTC), a data jest w formacie rrrr mm-dd.</span><span class="sxs-lookup"><span data-stu-id="a7c95-125">The date and time format is 24-hour Universal Time Coordinate (UTC) and the date is yyyy-mm-dd format.</span></span> <span data-ttu-id="a7c95-126">Kliknij znak plus alertu na liście, aby go edytować, lub kliknij przycisk Kosz go usunąć.</span><span class="sxs-lookup"><span data-stu-id="a7c95-126">Click the plus sign for an alert in the list to edit it, or click the trash-can to delete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="a7c95-127">Karta alerty dla klientów Enterprise Agreement (EA)</span><span class="sxs-lookup"><span data-stu-id="a7c95-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="a7c95-128">Umowa EA klienci mogą uzyskać alerty dla każdego działu w ramach rejestracji przez ustawienie wydatków przydziałów.</span><span class="sxs-lookup"><span data-stu-id="a7c95-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="a7c95-129">Zobacz [przydziały wydatków działu](https://ea.azure.com/helpdocs/departmentSpendingQuotas) w portalu EA, aby rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="a7c95-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in the EA portal to get started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="a7c95-130">Dowiedz się więcej na temat zarządzania Azure koszt</span><span class="sxs-lookup"><span data-stu-id="a7c95-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="a7c95-131">Oszacowanie kosztów przy użyciu [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/), [całkowity koszt posiadania kalkulatora](https://aka.ms/azure-tco-calculator), a po dodaniu usługi.</span><span class="sxs-lookup"><span data-stu-id="a7c95-131">Estimate costs using the [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="a7c95-132">[Przejrzyj użycia i kosztów regularnie w portalu Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="a7c95-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="a7c95-133">Włącz [Azure Advisor koszt zalecenia](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="a7c95-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="a7c95-134">Aby dowiedzieć się więcej, zobacz [Azure koszt wskazówki dotyczące zarządzania](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a7c95-134">To learn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
