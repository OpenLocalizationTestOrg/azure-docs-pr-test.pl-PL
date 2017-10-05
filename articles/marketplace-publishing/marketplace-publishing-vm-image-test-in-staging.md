---
title: "Testowanie ofertę maszyny Wirtualnej dla witryny Marketplace | Dokumentacja firmy Microsoft"
description: Zrozumienie sposobu testowania obrazu maszyny Wirtualnej w portalu Azure Marketplace.
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 7a41c3c6-625c-4478-b804-e124dee89040
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2016
ms.author: hascipio
ms.openlocfilehash: 26f856059b381be91b9cdd1f98a11dc90813c0c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-vm-offer-for-the-azure-marketplace-in-staging"></a><span data-ttu-id="71c7c-103">Testowanie ofertę maszyny Wirtualnej do portalu Azure Marketplace tymczasowych</span><span class="sxs-lookup"><span data-stu-id="71c7c-103">Test your VM offer for the Azure Marketplace in staging</span></span>
<span data-ttu-id="71c7c-104">Przemieszczania oznacza wdrażanie Twojego jednostki SKU w prywatnej "piaskownicy", gdzie testowania i zweryfikować jego działanie przed jego wdrożeniem w portalu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71c7c-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it to the Marketplace.</span></span> <span data-ttu-id="71c7c-105">Jednostka SKU jest wyświetlany w przemieszczania analogiczny, jak na rzecz klienta, który został wdrożony go.</span><span class="sxs-lookup"><span data-stu-id="71c7c-105">The SKU appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="71c7c-106">Obraz maszyny Wirtualnej muszą być certyfikowane do zostać przeniesiony do tymczasowego.</span><span class="sxs-lookup"><span data-stu-id="71c7c-106">Your VM image must be certified to be pushed to staging.</span></span>

## <a name="step-1-push-your-offer-to-staging"></a><span data-ttu-id="71c7c-107">Krok 1: Push Twojej oferty przemieszczania</span><span class="sxs-lookup"><span data-stu-id="71c7c-107">Step 1: Push your offer to staging</span></span>
1. <span data-ttu-id="71c7c-108">Na **publikowania** , kliknij pozycję **wypychania do przemieszczania**.</span><span class="sxs-lookup"><span data-stu-id="71c7c-108">On the **Publish** tab, click **Push to Staging**.</span></span>
   
    ![Rysowanie](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="71c7c-110">Jeśli Portal publikowania powiadamia użytkownika o błędach, należy je poprawić.</span><span class="sxs-lookup"><span data-stu-id="71c7c-110">If the Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="71c7c-111">W **kto ma dostęp do Twojej oferty przemieszczanego?** okna dialogowego wprowadź listę subskrypcji platformy Azure, które będą używane do podglądu ofertę w [portalu Azure w wersji zapoznawczej](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="71c7c-111">In the **Who can access your staged offer?** dialog box, enter the list of Azure subscriptions that you will use to preview your offer in the [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="71c7c-112">W przypadku maszyn wirtualnych i szablonów rozwiązania należy **nie** dozwolonych subskrypcje typu Dostawca usług Kryptograficznych, DreamSpark lub Azure otwartym.</span><span class="sxs-lookup"><span data-stu-id="71c7c-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="71c7c-113">W przypadku maszyn wirtualnych, po kliknięciu przycisku **WYPYCHANYCH STAGING**, są wykonywane następujące czynności, za sceny.</span><span class="sxs-lookup"><span data-stu-id="71c7c-113">In case of Virtual Machines, when you click on the button **PUSH TO STAGING**, the following steps are performed behind the scene.</span></span> <span data-ttu-id="71c7c-114">Można wyświetlić postęp każdego kroku na karcie PUBLIKUJ w publikacji portalu.</span><span class="sxs-lookup"><span data-stu-id="71c7c-114">You will be able to view the progress of each step under the PUBLISH tab in the Publishing portal.</span></span> <span data-ttu-id="71c7c-115">Należy sprawdzić tę stronę w regularnych odstępach czasu (do czasu stan pokazuje przejściowa) Aby uzyskać informacje o błędzie, który konieczne korekty użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="71c7c-115">You must check this page at regular interval (until the status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="71c7c-116">Na początku przemieszczania żądania prowadzi do zespołu certyfikacji, który zweryfikować dysku vhd.</span><span class="sxs-lookup"><span data-stu-id="71c7c-116">At first your staging request goes to the certification team who validate the vhd.</span></span> <span data-ttu-id="71c7c-117">Jednak jeśli — Otrzymano żądanie tylko marketingu zmiany, następnie certyfikacji krok zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="71c7c-117">However, if your request has got only marketing change, then the certification step is skipped.</span></span>
    > - <span data-ttu-id="71c7c-118">Po zakończeniu certyfikacji rozpoczęcia replikacji oferty, we wszystkich centrach danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71c7c-118">Once the certification is complete, replication of the offer start across all the Azure datacenters.</span></span> <span data-ttu-id="71c7c-119">Zazwyczaj zajmuje 24-48hours na zakończenie replikacji ale może potrwać do tygodnia, w zależności od rozmiaru wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="71c7c-119">It generally takes 24-48hours for the replication to complete but may take up to a week depending on the size of the vhd.</span></span> <span data-ttu-id="71c7c-120">Jeśli jednak — Otrzymano żądanie tylko marketingu zmiany, następnie replikacji jest szybsze.</span><span class="sxs-lookup"><span data-stu-id="71c7c-120">However, if your request has got only marketing change, then the replication is faster.</span></span>
    > - <span data-ttu-id="71c7c-121">Po ukończeniu replikacji jest to oferta, dla której będą dostępne w [portalu Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="71c7c-121">When the replication is complete, then the offer will be available in the [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="71c7c-122">W tym czasie stan zostać UMIESZCZONE w publikacji portalu.</span><span class="sxs-lookup"><span data-stu-id="71c7c-122">At that time the status become STAGED in the Publishing portal.</span></span> <span data-ttu-id="71c7c-123">Przemieszczanego oferta nie jest widoczna [portalu Azure](http:/portal.azure.com) wyłącznie przy użyciu nazwy e-mail skojarzonego z subskrypcją, z którym są przygotowywane oferty.</span><span class="sxs-lookup"><span data-stu-id="71c7c-123">A staged offer is visible in the [Azure portal](http:/portal.azure.com) only using the email id(s) associated with the subscription with which the offer is staged.</span></span>

1. <span data-ttu-id="71c7c-124">Zaloguj się do [portalu Azure w wersji zapoznawczej](https://portal.azure.com) przy użyciu jednej z subskrypcji platformy Azure wymienionych w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="71c7c-124">Sign in to the [Azure preview portal](https://portal.azure.com) by using one of the Azure subscriptions listed in the previous step.</span></span>
2. <span data-ttu-id="71c7c-125">Znajdź Twoją ofertę i zweryfikować punkty obrazu maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="71c7c-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="71c7c-126">Upewnij się, że marketingu zawartości wyświetlane prawidłowo w witrynie Marketplace.</span><span class="sxs-lookup"><span data-stu-id="71c7c-126">Make sure that marketing content shows up correctly in the Marketplace.</span></span>
   * <span data-ttu-id="71c7c-127">Wdrażanie na trasie obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="71c7c-127">End-to-end deployment of the VM image.</span></span>
     
      ![img mapy portalu](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="71c7c-129">Ofertę pozostanie w przejściowym dopóki powiadamiania firmy Microsoft za pośrednictwem portalu publikowania [**publikowania** kartę > kliknij przycisk **"Żądania zatwierdzenia do wypychania do produkcji"**] można przystąpić do produkcji.</span><span class="sxs-lookup"><span data-stu-id="71c7c-129">Your offer will remain in staging until you notify Microsoft via the Publishing Portal [**Publish** tab > click on the button **"Request Approval to Push to Production"**] that you are ready to push to production.</span></span> <span data-ttu-id="71c7c-130">Jest to idealne czasu na wszystkie elementy członkowskie wyboru Twojego zespołu nad wszystko w ramach przygotowania do Twojej oferty, przechodząc do listy.</span><span class="sxs-lookup"><span data-stu-id="71c7c-130">This is an ideal time to have all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="71c7c-131">Platformy przemieszczania jest przeznaczony do testowania oferty w trybie podglądu przez wydawcę.</span><span class="sxs-lookup"><span data-stu-id="71c7c-131">The staging platform is designed for testing the offer in a preview mode by the publisher.</span></span> <span data-ttu-id="71c7c-132">Zdecydowanie zniechęcić się przy użyciu tego platofrm do celów dostępnych w handlu.</span><span class="sxs-lookup"><span data-stu-id="71c7c-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="71c7c-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71c7c-133">Next steps</span></span>
<span data-ttu-id="71c7c-134">Teraz, gdy ofertę jest "przemieszczone" i jego funkcje zostały przetestowane i marketingu zawartości, możesz przejść do fazy publikowania końcowego **krok 4**: [wdrażanie Twojej oferty w portalu Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="71c7c-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed to the final publishing phase, **Step 4**: [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="71c7c-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="71c7c-135">See also</span></span>
* [<span data-ttu-id="71c7c-136">Wprowadzenie: jak publikowanie oferty w portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="71c7c-136">Getting started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

