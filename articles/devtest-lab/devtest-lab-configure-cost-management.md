---
title: "aaaView hello miesięczne laboratorium szacowany koszt trendu w usłudze Azure DevTest Labs | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello Azure DevTest Labs miesięczne wykresu trendu szacowany koszt."
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
ms.openlocfilehash: 47c7dd4cf91b76de74b502c50f05e79cd501ee35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="view-hello-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="01f57-103">Widok hello miesięczne laboratorium szacowany koszt trendu w usłudze Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="01f57-103">View hello monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="01f57-104">Funkcja zarządzania koszt Hello DevTest Labs pomaga śledzić hello koszt laboratorium.</span><span class="sxs-lookup"><span data-stu-id="01f57-104">hello Cost Management feature of DevTest Labs helps you track hello cost of your lab.</span></span> <span data-ttu-id="01f57-105">W tym artykule przedstawiono sposób toouse hello **miesięczny Trend szacowany koszt** tooview wykresu hello bieżącego miesiąca kalendarzowego szacowany koszt do daty i hello szacowany koszt koniec miesiąca hello bieżącego miesiąca kalendarzowego.</span><span class="sxs-lookup"><span data-stu-id="01f57-105">This article illustrates how toouse hello **Monthly Estimated Cost Trend** chart tooview hello current calendar month's estimated cost-to-date and hello projected end-of-month cost for hello current calendar month.</span></span> <span data-ttu-id="01f57-106">W tym artykule dowiesz się, jak tooview hello miesięczne wykresu trendu szacowany koszt w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="01f57-106">In this article, you learn how tooview hello monthly estimated cost trend chart in hello Azure portal.</span></span>

## <a name="viewing-hello-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="01f57-107">Wyświetlanie hello miesięczny Trend szacowany koszt wykresu</span><span class="sxs-lookup"><span data-stu-id="01f57-107">Viewing hello Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="01f57-108">Witaj tooview miesięczny Trend szacowany koszt wykresu, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="01f57-108">tooview hello Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="01f57-109">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="01f57-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="01f57-110">Wybierz **więcej usług**, a następnie wybierz **DevTest Labs** z listy hello.</span><span class="sxs-lookup"><span data-stu-id="01f57-110">Select **More Services**, and then select **DevTest Labs** from hello list.</span></span>
3. <span data-ttu-id="01f57-111">Z listy hello labs wybierz żądany laboratorium hello.</span><span class="sxs-lookup"><span data-stu-id="01f57-111">From hello list of labs, select hello desired lab.</span></span>   
4. <span data-ttu-id="01f57-112">W bloku hello laboratorium, wybierz **koszt ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="01f57-112">On hello lab's blade, select **Cost settings**.</span></span>
5. <span data-ttu-id="01f57-113">W laboratorium hello **koszt ustawienia** bloku, wybierz opcję **trend koszt laboratorium**.</span><span class="sxs-lookup"><span data-stu-id="01f57-113">On hello lab's **Cost settings** blade, select **Lab cost trend**.</span></span>
6. <span data-ttu-id="01f57-114">Witaj Poniższy zrzut ekranu przedstawia przykład wykresu kosztów.</span><span class="sxs-lookup"><span data-stu-id="01f57-114">hello following screen shot shows an example of a cost chart.</span></span> 
   
    ![Wykres kosztu](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="01f57-116">Witaj **szacowany koszt** wartość jest hello bieżącego miesiąca kalendarzowego szacowany koszt do daty.</span><span class="sxs-lookup"><span data-stu-id="01f57-116">hello **Estimated cost** value is hello current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="01f57-117">Witaj **koszt planowany** hello szacowany koszt hello całego bieżącego miesiąca kalendarzowego oblicza się przy użyciu hello koszt laboratorium dla hello poprzedniej pięć dni.</span><span class="sxs-lookup"><span data-stu-id="01f57-117">hello **Projected cost** is hello estimated cost for hello entire current calendar month, calculated using hello lab cost for hello previous five days.</span></span>

<span data-ttu-id="01f57-118">koszty Hello jest zaokrąglana toohello najbliższej liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="01f57-118">hello cost amounts are rounded up toohello next whole number.</span></span> <span data-ttu-id="01f57-119">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="01f57-119">For example:</span></span> 

* <span data-ttu-id="01f57-120">5.01 Zaokrągla liczbę w górę too6</span><span class="sxs-lookup"><span data-stu-id="01f57-120">5.01 rounds up too6</span></span> 
* <span data-ttu-id="01f57-121">5.50 Zaokrągla liczbę w górę too6</span><span class="sxs-lookup"><span data-stu-id="01f57-121">5.50 rounds up too6</span></span>
* <span data-ttu-id="01f57-122">5.99 Zaokrągla liczbę w górę too6</span><span class="sxs-lookup"><span data-stu-id="01f57-122">5.99 rounds up too6</span></span>

<span data-ttu-id="01f57-123">W trakcie jego stany powyżej wykresu hello, hello koszty Zobacz na wykresie hello są *szacowany* koszty przy użyciu [płatność za rzeczywiste użycie](https://azure.microsoft.com/offers/ms-azr-0003p/) oferuje.</span><span class="sxs-lookup"><span data-stu-id="01f57-123">As it states above hello chart, hello costs you see in hello chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span>
<span data-ttu-id="01f57-124">Ponadto następujące hello są *nie* objęte hello obliczania kosztów:</span><span class="sxs-lookup"><span data-stu-id="01f57-124">Additionally, hello following are *not* included in hello cost calculation:</span></span>

* <span data-ttu-id="01f57-125">Dostawca usług Kryptograficznych i Dreamspark subskrypcje obecnie nie są obsługiwane jako Azure DevTest Labs używa hello [Azure API rozliczeń](../billing/billing-usage-rate-card-overview.md) laboratorium hello toocalculate koszt, który nie obsługuje dostawcy usług Kryptograficznych lub Dreamspark subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="01f57-125">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses hello [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) toocalculate hello lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="01f57-126">Twoje stawek oferty.</span><span class="sxs-lookup"><span data-stu-id="01f57-126">Your offer rates.</span></span> <span data-ttu-id="01f57-127">Obecnie nie jesteśmy w stanie toouse Twojego stawek oferty (wyświetlany w obszarze subskrypcji) czy musisz mieć negocjowane z Microsoft lub partnerów.</span><span class="sxs-lookup"><span data-stu-id="01f57-127">Currently, we are not able toouse your offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="01f57-128">Użyto płatność za rzeczywiste użycie stawki.</span><span class="sxs-lookup"><span data-stu-id="01f57-128">We are using Pay-As-You-Go rates.</span></span>
* <span data-ttu-id="01f57-129">Twoje podatki</span><span class="sxs-lookup"><span data-stu-id="01f57-129">Your taxes</span></span>
* <span data-ttu-id="01f57-130">Twoje zniżki</span><span class="sxs-lookup"><span data-stu-id="01f57-130">Your discounts</span></span>
* <span data-ttu-id="01f57-131">Waluta.</span><span class="sxs-lookup"><span data-stu-id="01f57-131">Your billing currency.</span></span> <span data-ttu-id="01f57-132">Obecnie koszt laboratorium hello jest wyświetlana tylko w walucie USD.</span><span class="sxs-lookup"><span data-stu-id="01f57-132">Currently, hello lab cost is displayed only in USD currency.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="01f57-133">Wpisy na blogu pokrewne</span><span class="sxs-lookup"><span data-stu-id="01f57-133">Related blog posts</span></span>
* [<span data-ttu-id="01f57-134">Dwa więcej tookeep rzeczy koszt zgodnie z planem w usłudze DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="01f57-134">Two more things tookeep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="01f57-135">Dlaczego koszt progi?</span><span class="sxs-lookup"><span data-stu-id="01f57-135">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="01f57-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="01f57-136">Next steps</span></span>
<span data-ttu-id="01f57-137">Oto obok niektórych tootry rzeczy:</span><span class="sxs-lookup"><span data-stu-id="01f57-137">Here are some things tootry next:</span></span>

* <span data-ttu-id="01f57-138">[Definiowanie zasad laboratorium](devtest-lab-set-lab-policy.md) — Dowiedz się, jak tooset hello różnych zasad używane toogovern korzystania laboratorium i jego maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="01f57-138">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how tooset hello various policies used toogovern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="01f57-139">[Tworzenie niestandardowego obrazu](devtest-lab-create-template.md) — podczas tworzenia maszyny Wirtualnej, należy określić podstawowy, który może być niestandardowy obraz lub obrazu z witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="01f57-139">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="01f57-140">W tym artykule przedstawiono sposób toocreate niestandardowego obrazu z pliku VHD.</span><span class="sxs-lookup"><span data-stu-id="01f57-140">This article illustrates how toocreate a custom image from a VHD file.</span></span>
* <span data-ttu-id="01f57-141">[Konfigurowanie portalu Marketplace obrazów](devtest-lab-configure-marketplace-images.md) — DevTest Labs obsługuje tworzenie maszyn wirtualnych, oparte na obrazach portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="01f57-141">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="01f57-142">W tym artykule przedstawiono sposób toospecify, którego, portalu Azure Marketplace obrazy mogą być używane podczas tworzenia maszyn wirtualnych w laboratorium.</span><span class="sxs-lookup"><span data-stu-id="01f57-142">This article illustrates how toospecify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="01f57-143">[Utwórz maszynę Wirtualną w laboratorium](devtest-lab-add-vm-with-artifacts.md) -ilustruje sposób toocreate maszyny Wirtualnej z obrazu podstawowego (albo niestandardowe lub Marketplace) i w jaki sposób toowork z artefaktami w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="01f57-143">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how toocreate a VM from a base image (either custom or Marketplace), and how toowork with artifacts in your VM.</span></span>

