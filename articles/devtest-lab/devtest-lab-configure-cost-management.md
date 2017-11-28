---
title: "Wyświetl trend miesięczny koszt szacowany laboratorium w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Więcej informacji o usłudze Azure DevTest Labs miesięczne szacowany koszt wykresu trendu."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/25/2016
ms.author: tarcher
ms.openlocfilehash: b3ad1ead522908d4b41b7cca98d20ac91664998e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="eeaa9-103">Wyświetl trend miesięczny koszt szacowany laboratorium w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="eeaa9-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="eeaa9-104">Funkcja zarządzania koszt DevTest Labs pomaga śledzić koszt laboratorium.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="eeaa9-105">W tym artykule przedstawiono sposób użycia **miesięczny Trend szacowany koszt** wykresu, aby wyświetlić bieżącego miesiąca kalendarzowego szacowany koszt do daty i szacowany koszt koniec miesiąca dla bieżącego miesiąca kalendarzowego.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="eeaa9-106">W tym artykule Dowiedz się jak wyświetlić miesięczne wykresu trendu szacowany koszt w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-106">In this article, you learn how to view the monthly estimated cost trend chart in the Azure portal.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="eeaa9-107">Wyświetlanie wykresu miesięczny Trend szacowany koszt</span><span class="sxs-lookup"><span data-stu-id="eeaa9-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="eeaa9-108">Aby wyświetlić na wykresie miesięczny Trend szacowany koszt, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="eeaa9-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="eeaa9-109">Zaloguj się w witrynie [Azure Portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="eeaa9-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="eeaa9-110">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-110">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="eeaa9-111">Z listy labs wybierz żądany laboratorium.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-111">From the list of labs, select the desired lab.</span></span>   
4. <span data-ttu-id="eeaa9-112">W bloku laboratorium, wybierz **koszt ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-112">On the lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="eeaa9-113">W laboratorium **koszt ustawienia** bloku, wybierz opcję **trend koszt laboratorium**.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-113">On the lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="eeaa9-114">Poniższy zrzut ekranu przedstawia przykład wykresu kosztów.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-114">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![Wykres kosztu](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="eeaa9-116">**Szacowany koszt** wartość jest bieżącego miesiąca kalendarzowego szacowany koszt do daty.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-116">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="eeaa9-117">**Koszt planowany** jest szacowany koszt dla całego bieżącego miesiąca kalendarzowego obliczane przy użyciu koszt laboratorium dla poprzedniego pięć dni.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-117">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="eeaa9-118">Kwoty kosztów są zaokrąglona w górę do najbliższej liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-118">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="eeaa9-119">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eeaa9-119">For example:</span></span> 

* <span data-ttu-id="eeaa9-120">5.01 Zaokrągla do 6</span><span class="sxs-lookup"><span data-stu-id="eeaa9-120">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="eeaa9-121">5.50 Zaokrągla do 6</span><span class="sxs-lookup"><span data-stu-id="eeaa9-121">5.50 rounds up to 6</span></span>
* <span data-ttu-id="eeaa9-122">5.99 Zaokrągla do 6</span><span class="sxs-lookup"><span data-stu-id="eeaa9-122">5.99 rounds up to 6</span></span>

<span data-ttu-id="eeaa9-123">W trakcie jego stany powyżej wykresu, są koszty Zobacz na wykresie *szacowany* koszty przy użyciu [płatność za rzeczywiste użycie](https://azure.microsoft.com/offers/ms-azr-0003p/) stawek oferty.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-123">As it states above the chart, the costs you see in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="eeaa9-124">Ponadto są następujące *nie* uwzględnionych podczas obliczania kosztów:</span><span class="sxs-lookup"><span data-stu-id="eeaa9-124">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="eeaa9-125">Dostawca usług Kryptograficznych i Dreamspark subskrypcje obecnie nie są obsługiwane jako używa Azure DevTest Labs [Azure API rozliczeń](../billing/billing-usage-rate-card-overview.md) do obliczania kosztów, który nie obsługuje dostawcy usług Kryptograficznych lub Dreamspark subskrypcji laboratorium.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="eeaa9-126">Twoje stawek oferty.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-126">Your offer rates.</span></span> <span data-ttu-id="eeaa9-127">Obecnie nie możemy do użycia z stawek oferty (wyświetlany w obszarze subskrypcji) czy musisz mieć negocjowane z Microsoft lub partnerów.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-127">Currently, we are not able to use your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="eeaa9-128">Użyto płatność za rzeczywiste użycie stawki.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="eeaa9-129">Twoje podatki</span><span class="sxs-lookup"><span data-stu-id="eeaa9-129">Your taxes</span></span>
* <span data-ttu-id="eeaa9-130">Twoje zniżki</span><span class="sxs-lookup"><span data-stu-id="eeaa9-130">Your discounts</span></span>
* <span data-ttu-id="eeaa9-131">Waluta.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-131">Your billing currency.</span></span> <span data-ttu-id="eeaa9-132">Obecnie koszt laboratorium jest wyświetlany tylko w walucie USD.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-132">Currently, the lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="eeaa9-133">Wpisy na blogu pokrewne</span><span class="sxs-lookup"><span data-stu-id="eeaa9-133">Related blog posts</span></span>
* [<span data-ttu-id="eeaa9-134">Więcej opcji Zachowaj koszt zgodnie z planem w usłudze DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="eeaa9-134">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="eeaa9-135">Dlaczego koszt progi?</span><span class="sxs-lookup"><span data-stu-id="eeaa9-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="eeaa9-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eeaa9-136">Next steps</span></span>
<span data-ttu-id="eeaa9-137">Poniżej przedstawiono niektóre czynności, aby spróbować obok:</span><span class="sxs-lookup"><span data-stu-id="eeaa9-137">Here are some things to try next:</span></span>

* <span data-ttu-id="eeaa9-138">[Definiowanie zasad laboratorium](devtest-lab-set-lab-policy.md) — Dowiedz się, jak skonfigurowanie różnych zasad używane do sterowania korzystania laboratorium i jego maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="eeaa9-139">[Tworzenie niestandardowego obrazu](devtest-lab-create-template.md) — podczas tworzenia maszyny Wirtualnej, należy określić podstawowy, który może być niestandardowy obraz lub obrazu z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="eeaa9-140">W tym artykule przedstawiono sposób tworzenia niestandardowego obrazu z pliku VHD.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-140">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="eeaa9-141">[Konfigurowanie portalu Marketplace obrazów](devtest-lab-configure-marketplace-images.md) — DevTest Labs obsługuje tworzenie maszyn wirtualnych, oparte na obrazach portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="eeaa9-142">W tym artykule przedstawiono sposób określić, które, portalu Azure Marketplace obrazy mogą być używane podczas tworzenia maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-142">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="eeaa9-143">[Utwórz maszynę Wirtualną w laboratorium](devtest-lab-add-vm-with-artifacts.md) -ilustruje sposób tworzenia maszyny Wirtualnej z obrazu podstawowego (albo niestandardowe lub Marketplace) oraz sposób pracy z artefaktami w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eeaa9-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

