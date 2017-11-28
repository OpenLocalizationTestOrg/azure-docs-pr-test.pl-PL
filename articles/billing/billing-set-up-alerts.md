---
title: "aaaSet rozliczeń lub środki alerty dotyczące subskrypcji platformy Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 711b9c72c59874792b0e229cdc5ec0fa517c24c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-billing-or-credit-alerts-for-your-microsoft-azure-subscriptions"></a><span data-ttu-id="1fd15-104">Ustawianie alertów rozliczeń lub faktury dla subskrypcji platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1fd15-104">Set up billing or credit alerts for your Microsoft Azure subscriptions</span></span>
<span data-ttu-id="1fd15-105">Jeśli jesteś hello administratora konta subskrypcji platformy Azure, można użyć hello Azure rozliczeń Usługa alertów rozliczeń toocreate dostosować alerty ułatwiające monitorowanie i zarządzanie działania rozliczeń dla konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1fd15-105">If you’re hello Account Admin for an Azure subscription, you can use hello Azure Billing Alert Service toocreate customized billing alerts that help you monitor and manage billing activity for your Azure accounts.</span></span>

<span data-ttu-id="1fd15-106">Ta usługa jest w wersji zapoznawczej, więc należy tooenable go na stronie funkcji w wersji zapoznawczej hello najpierw.</span><span class="sxs-lookup"><span data-stu-id="1fd15-106">This service is in preview, so you need tooenable it in hello Preview Features page first.</span></span>

## <a name="set-hello-alert-threshold-and-email-recipients"></a><span data-ttu-id="1fd15-107">Ustaw hello próg i adres e-mail odbiorcy alertów</span><span class="sxs-lookup"><span data-stu-id="1fd15-107">Set hello alert threshold and email recipients</span></span>
1. <span data-ttu-id="1fd15-108">Odwiedź stronę [strona funkcje w wersji zapoznawczej hello](https://account.windowsazure.com/PreviewFeatures) i Włącz **rozliczeń Usługa alertów**.</span><span class="sxs-lookup"><span data-stu-id="1fd15-108">Visit [hello Preview Features page](https://account.windowsazure.com/PreviewFeatures) and enable **Billing Alert Service**.</span></span>

1. <span data-ttu-id="1fd15-109">Po otrzymaniu hello e-mail potwierdzenie, że usługa rozliczeń hello jest włączona dla Twojej subskrypcji, odwiedź stronę [strony subskrypcje hello](https://account.windowsazure.com/Subscriptions) w portalu konta hello.</span><span class="sxs-lookup"><span data-stu-id="1fd15-109">After you receive hello email confirmation that hello billing service is turned on for your subscription, visit [hello Subscriptions page](https://account.windowsazure.com/Subscriptions) in hello account portal.</span></span> <span data-ttu-id="1fd15-110">Kliknij subskrypcję hello toomonitor, a następnie kliknij przycisk **alerty**.</span><span class="sxs-lookup"><span data-stu-id="1fd15-110">Click hello subscription you want toomonitor, and then click **Alerts**.</span></span>

    ![Zrzut ekranu przedstawiający widok subskrypcji hello Centrum konta platformy Azure z wyróżnioną pozycją alertami][Image1]

2. <span data-ttu-id="1fd15-112">Następnie kliknij przycisk **dodać alertu** toocreate Twojego pierwszego z nich.</span><span class="sxs-lookup"><span data-stu-id="1fd15-112">Next, click **Add Alert** toocreate your first one.</span></span> <span data-ttu-id="1fd15-113">Można ustawić łącznie pięć alerty dotyczące rozliczeń dla subskrypcji o różnych progu i zapasowej tootwo adresatów wiadomości e-mail o każdym alercie.</span><span class="sxs-lookup"><span data-stu-id="1fd15-113">You can set up a total of five billing alerts per subscription, with a different threshold and up tootwo email recipients for each alert.</span></span>

    ![Zrzut ekranu przedstawiający hello widok alertów, w którym można dodać alertu][Image2]

3. <span data-ttu-id="1fd15-115">Po dodaniu alert nadaj unikatową nazwę, wybierz próg wydatków i wybierz hello adresów e-mail, gdy alerty są wysyłane.</span><span class="sxs-lookup"><span data-stu-id="1fd15-115">When you add an alert, you give it a unique name, choose a spending threshold, and choose hello email addresses where alerts are sent.</span></span> <span data-ttu-id="1fd15-116">Podczas konfigurowania hello próg, można wybrać jedną **rozliczeń całkowita** lub **środki pieniężne** z hello **alertów dla** listy.</span><span class="sxs-lookup"><span data-stu-id="1fd15-116">When setting up hello threshold, you can choose either a **Billing Total** or a **Monetary Credit** from hello **Alert For** list.</span></span> <span data-ttu-id="1fd15-117">Łącznie rozliczeń alert jest wysyłany, gdy subskrypcja wydatków przekracza próg hello.</span><span class="sxs-lookup"><span data-stu-id="1fd15-117">For a billing total, an alert is sent when subscription spending exceeds hello threshold.</span></span> <span data-ttu-id="1fd15-118">Uzyskać środki pieniężne alert jest wysyłany, gdy kwota środków pieniężnych spadnie poniżej hello limit.</span><span class="sxs-lookup"><span data-stu-id="1fd15-118">For a monetary credit, an alert is sent when monetary credits drop below hello limit.</span></span> <span data-ttu-id="1fd15-119">Kwota środków pieniężnych stosowane są zazwyczaj tooFree subskrypcji wersji próbnej i Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1fd15-119">Monetary credits usually apply tooFree Trial and Visual Studio subscriptions.</span></span>

    ![Zrzut ekranu przedstawiający widok alertu dodanie hello, którym można skonfigurować adresatów][Image3]

<span data-ttu-id="1fd15-121">Azure obsługuje dowolnego adresu e-mail, ale nie Sprawdź, czy adres e-mail hello działa, więc dokładnie literówki.</span><span class="sxs-lookup"><span data-stu-id="1fd15-121">Azure supports any email address but doesn't verify that hello email address works, so double-check for typos.</span></span>

## <a name="check-on-your-alerts"></a><span data-ttu-id="1fd15-122">Sprawdź alerty</span><span class="sxs-lookup"><span data-stu-id="1fd15-122">Check on your alerts</span></span>
<span data-ttu-id="1fd15-123">Po skonfigurowaniu alerty hello Centrum konta je i pokazuje, ile więcej można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="1fd15-123">After you set up alerts, hello Account Center lists them and shows how many more you can set up.</span></span> <span data-ttu-id="1fd15-124">Dla każdego alertu Zobacz hello daty i godziny, wysłania, czy jest alert dotyczący rozliczeń całkowita lub środki pieniężne oraz limit hello, skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="1fd15-124">For each alert, you see hello date and time it was sent, whether it’s an alert for Billing Total or Monetary Credit, and hello limit you set up.</span></span> <span data-ttu-id="1fd15-125">format daty i godziny Hello 24-godzinnym koordynować czasu uniwersalnego (UTC) i Data hello jest format rrrr mm-dd.</span><span class="sxs-lookup"><span data-stu-id="1fd15-125">hello date and time format is 24-hour Universal Time Coordinate (UTC) and hello date is yyyy-mm-dd format.</span></span> <span data-ttu-id="1fd15-126">Kliknij hello oraz zarejestrować alertu w tooedit listy hello lub hello toodelete Kosza może go.</span><span class="sxs-lookup"><span data-stu-id="1fd15-126">Click hello plus sign for an alert in hello list tooedit it, or click hello trash-can toodelete it.</span></span>

## <a name="billing-alerts-for-enterprise-agreement-ea-customers"></a><span data-ttu-id="1fd15-127">Karta alerty dla klientów Enterprise Agreement (EA)</span><span class="sxs-lookup"><span data-stu-id="1fd15-127">Billing alerts for Enterprise Agreement (EA) customers</span></span>
<span data-ttu-id="1fd15-128">Umowa EA klienci mogą uzyskać alerty dla każdego działu w ramach rejestracji przez ustawienie wydatków przydziałów.</span><span class="sxs-lookup"><span data-stu-id="1fd15-128">EA customers can get alerts for each department under an enrollment by setting spending quotas.</span></span> <span data-ttu-id="1fd15-129">Zobacz [przydziały wydatków działu](https://ea.azure.com/helpdocs/departmentSpendingQuotas) w tooget portalu EA hello uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="1fd15-129">See [Department Spending Quotas](https://ea.azure.com/helpdocs/departmentSpendingQuotas) in hello EA portal tooget started.</span></span>

## <a name="learn-more-about-azure-cost-management"></a><span data-ttu-id="1fd15-130">Dowiedz się więcej na temat zarządzania Azure koszt</span><span class="sxs-lookup"><span data-stu-id="1fd15-130">Learn more about Azure cost management</span></span>
- <span data-ttu-id="1fd15-131">Szacowanie kosztów przy użyciu hello [Kalkulator cen](https://azure.microsoft.com/pricing/calculator/), [całkowity koszt posiadania kalkulatora](https://aka.ms/azure-tco-calculator), a po dodaniu usługi.</span><span class="sxs-lookup"><span data-stu-id="1fd15-131">Estimate costs using hello [pricing calculator](https://azure.microsoft.com/pricing/calculator/), [total cost of ownership calculator](https://aka.ms/azure-tco-calculator), and when you add a service.</span></span>
- <span data-ttu-id="1fd15-132">[Przejrzyj użycia i kosztów regularnie w portalu Azure](billing-getting-started.md#costs).</span><span class="sxs-lookup"><span data-stu-id="1fd15-132">[Review your usage and costs regularly in Azure portal](billing-getting-started.md#costs).</span></span>
- <span data-ttu-id="1fd15-133">Włącz [Azure Advisor koszt zalecenia](../advisor/advisor-cost-recommendations.md).</span><span class="sxs-lookup"><span data-stu-id="1fd15-133">Turn on [Azure Advisor cost recommendations](../advisor/advisor-cost-recommendations.md).</span></span>

<span data-ttu-id="1fd15-134">toolearn więcej, zobacz [Azure koszt wskazówki dotyczące zarządzania](billing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="1fd15-134">toolearn more, see [Azure cost management guidance](billing-getting-started.md).</span></span>

[Image1]: ./media/azure-billing-set-up-alerts/billingalert1.png 
[Image2]: ./media/azure-billing-set-up-alerts/billingalert2.png
[Image3]: ./media/azure-billing-set-up-alerts/billingalerts3.png 
