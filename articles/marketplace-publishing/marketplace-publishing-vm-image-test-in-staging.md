---
title: "aaaTest oferują maszyny Wirtualnej na powitania Marketplace | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootest, obraz maszyny Wirtualnej, dla hello Azure Marketplace."
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
ms.openlocfilehash: ab166d2c3c536810a3a8f48330f0482b9b4e58d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-vm-offer-for-hello-azure-marketplace-in-staging"></a><span data-ttu-id="ef6a3-103">Testowanie ofertę maszyny Wirtualnej dla hello Azure Marketplace tymczasowych</span><span class="sxs-lookup"><span data-stu-id="ef6a3-103">Test your VM offer for hello Azure Marketplace in staging</span></span>
<span data-ttu-id="ef6a3-104">Sposób wdrażania programu jednostki SKU w prywatnej "piaskownicy", gdzie testowania i zweryfikować jego działanie przed jego wdrożeniem toohello Marketplace przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-104">Staging means deploying your SKU in a private “sandbox” where you can test and validate its functionality before deploying it toohello Marketplace.</span></span> <span data-ttu-id="ef6a3-105">Witaj SKU pojawia się w przemieszczania analogiczny, jak tooa klienta, który został wdrożony go.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-105">hello SKU appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="ef6a3-106">Obraz maszyny Wirtualnej musi być toostaging certyfikowanych toobe naciśnięty.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-106">Your VM image must be certified toobe pushed toostaging.</span></span>

## <a name="step-1-push-your-offer-toostaging"></a><span data-ttu-id="ef6a3-107">Krok 1: Push toostaging Twojej oferty</span><span class="sxs-lookup"><span data-stu-id="ef6a3-107">Step 1: Push your offer toostaging</span></span>
1. <span data-ttu-id="ef6a3-108">Na powitania **publikowania** , kliknij pozycję **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-108">On hello **Publish** tab, click **Push tooStaging**.</span></span>
   
    ![Rysowanie](media/marketplace-publishing-vm-image-test-in-staging/vm-image-push-to-staging.png)
2. <span data-ttu-id="ef6a3-110">Jeśli Portal publikowania hello powiadamia o błędy, należy je poprawić.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-110">If hello Publishing Portal notifies you of any errors, correct them.</span></span>
3. <span data-ttu-id="ef6a3-111">W hello **kto ma dostęp do Twojej oferty przemieszczanego?** okna dialogowego wprowadź hello Lista subskrypcji platformy Azure, który będzie używany toopreview ofertę w hello [portalu Azure w wersji zapoznawczej](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef6a3-111">In hello **Who can access your staged offer?** dialog box, enter hello list of Azure subscriptions that you will use toopreview your offer in hello [Azure preview portal](https://portal.azure.com).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ef6a3-112">W przypadku maszyn wirtualnych i szablonów rozwiązania należy **nie** dozwolonych subskrypcje typu Dostawca usług Kryptograficznych, DreamSpark lub Azure otwartym.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-112">In case of Virtual Machines and Solution templates, please **do not** whitelist subscriptions of type CSP, DreamSpark or Azure in Open.</span></span>
   > 
   > 

    > <span data-ttu-id="ef6a3-113">W przypadku maszyn wirtualnych, po kliknięciu przycisku hello **tooSTAGING WYPYCHANIA**, hello następujące kroki są wykonywane za hello sceny.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-113">In case of Virtual Machines, when you click on hello button **PUSH tooSTAGING**, hello following steps are performed behind hello scene.</span></span> <span data-ttu-id="ef6a3-114">Będziesz w stanie tooview postęp hello każdego kroku karcie publikowania hello w hello publikowania portalu.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-114">You will be able tooview hello progress of each step under hello PUBLISH tab in hello Publishing portal.</span></span> <span data-ttu-id="ef6a3-115">Należy sprawdzić tej strony w regularnych odstępach czasu (do czasu hello stan pokazuje przejściowa) Aby uzyskać informacje o błędzie, który konieczne korekty użytkownika końcowego.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-115">You must check this page at regular interval (until hello status shows STAGED) for any failure information which need correction from your end.</span></span>

    > - <span data-ttu-id="ef6a3-116">Na początku przemieszczania żądanie przejdzie do zespołu certyfikacji toohello, który zweryfikować hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-116">At first your staging request goes toohello certification team who validate hello vhd.</span></span> <span data-ttu-id="ef6a3-117">Jednak jeśli — Otrzymano żądanie tylko marketingu zmiany, następnie hello certyfikacji krok zostanie pominięty.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-117">However, if your request has got only marketing change, then hello certification step is skipped.</span></span>
    > - <span data-ttu-id="ef6a3-118">Po zakończeniu certyfikacji hello replikacji rozpoczęcia oferty hello we wszystkich hello centrach danych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-118">Once hello certification is complete, replication of hello offer start across all hello Azure datacenters.</span></span> <span data-ttu-id="ef6a3-119">Zazwyczaj zajmuje 24-48hours dla toocomplete replikacji hello ale może potrwać tooa tygodnia, w zależności od rozmiaru hello hello wirtualnego dysku twardego.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-119">It generally takes 24-48hours for hello replication toocomplete but may take up tooa week depending on hello size of hello vhd.</span></span> <span data-ttu-id="ef6a3-120">Jeśli jednak — Otrzymano żądanie tylko marketingu zmiany, następnie replikacji hello jest szybsze.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-120">However, if your request has got only marketing change, then hello replication is faster.</span></span>
    > - <span data-ttu-id="ef6a3-121">Po ukończeniu replikacji hello jest to oferta hello będą dostępne w hello [portalu Azure](http:/portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef6a3-121">When hello replication is complete, then hello offer will be available in hello [Azure portal](http:/portal.azure.com).</span></span> <span data-ttu-id="ef6a3-122">W tym hello czas stanu stają się UMIESZCZONE w hello publikowania portalu.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-122">At that time hello status become STAGED in hello Publishing portal.</span></span> <span data-ttu-id="ef6a3-123">Przemieszczanego oferta nie jest widoczna hello [portalu Azure](http:/portal.azure.com) wyłącznie przy użyciu nazwy e-mail hello skojarzone z subskrypcją hello, z których hello są przygotowywane oferty.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-123">A staged offer is visible in hello [Azure portal](http:/portal.azure.com) only using hello email id(s) associated with hello subscription with which hello offer is staged.</span></span>

1. <span data-ttu-id="ef6a3-124">Zaloguj się toohello [portalu Azure w wersji zapoznawczej](https://portal.azure.com) przy użyciu jednej z hello subskrypcji platformy Azure na liście hello w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-124">Sign in toohello [Azure preview portal](https://portal.azure.com) by using one of hello Azure subscriptions listed in hello previous step.</span></span>
2. <span data-ttu-id="ef6a3-125">Znajdź Twoją ofertę i zweryfikować punkty obrazu maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="ef6a3-125">Find your offer and validate your VM image points:</span></span>
   
   * <span data-ttu-id="ef6a3-126">Upewnij się, że marketingu zawartości jest wyświetlane poprawnie w hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-126">Make sure that marketing content shows up correctly in hello Marketplace.</span></span>
   * <span data-ttu-id="ef6a3-127">Wdrażanie na trasie hello obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-127">End-to-end deployment of hello VM image.</span></span>
     
      ![img mapy portalu](media/marketplace-publishing-push-to-staging/pubportal-mapping-azure-portal.jpg)

> [!IMPORTANT]
> <span data-ttu-id="ef6a3-129">Ofertę pozostanie w przejściowym dopóki bezzwłocznego powiadamiania firmy Microsoft za pośrednictwem hello Portal publikowania [**publikowania** kartę > kliknij przycisk hello **"TooProduction tooPush zatwierdzenie żądania"**] czy toopush gotowe tooproduction.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-129">Your offer will remain in staging until you notify Microsoft via hello Publishing Portal [**Publish** tab > click on hello button **"Request Approval tooPush tooProduction"**] that you are ready toopush tooproduction.</span></span> <span data-ttu-id="ef6a3-130">Jest to toohave idealne czas, sprawdź wszyscy członkowie zespołu nad wszystko w ramach przygotowania do Twojej oferty, przechodząc do listy.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-130">This is an ideal time toohave all members of your team check over everything in preparation for your offer going listed.</span></span>
> 
> <span data-ttu-id="ef6a3-131">Hello przemieszczania platformy jest przeznaczony do testowania oferta hello w trybie podglądu przez wydawcę hello.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-131">hello staging platform is designed for testing hello offer in a preview mode by hello publisher.</span></span> <span data-ttu-id="ef6a3-132">Zdecydowanie zniechęcić się przy użyciu tego platofrm do celów dostępnych w handlu.</span><span class="sxs-lookup"><span data-stu-id="ef6a3-132">We strongly discourage using this platofrm for commerical purposes.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ef6a3-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ef6a3-133">Next steps</span></span>
<span data-ttu-id="ef6a3-134">Ofertę jest "przemieszczony", a zostały przetestowane jego funkcjonalność i marketingu zawartości, możesz przejść publikowanie końcowego toohello fazy **krok 4**: [wdrażanie toohello Twojego oferta portalu Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="ef6a3-134">Now that your offer is "staged" and you have tested its functionality and marketing content, you can proceed toohello final publishing phase, **Step 4**: [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ef6a3-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ef6a3-135">See also</span></span>
* [<span data-ttu-id="ef6a3-136">Wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ef6a3-136">Getting started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

