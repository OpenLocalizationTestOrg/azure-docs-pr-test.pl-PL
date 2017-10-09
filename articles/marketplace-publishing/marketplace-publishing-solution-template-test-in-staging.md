---
title: "aaaTesting szablonu rozwiązanie oferuje dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootest szablon rozwiązania oferty dla hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: 9c195c465d2fc6aa349e4bbcc348e5325f32850d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="c1e3b-103">Testowanie ofertę szablon rozwiązania tymczasowych</span><span class="sxs-lookup"><span data-stu-id="c1e3b-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="c1e3b-104">Oznacza, że wdrażanie ofertę w prywatnej "piaskownicy", gdzie należy przetestować i sprawdzić jego działanie przed wypchnięciem go tooproduction przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="c1e3b-105">Oferta Hello pojawia się w tymczasowej analogiczny, jak tooa klienta, który został wdrożony go.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-105">hello offer appears in staging just as it would tooa customer who has deployed it.</span></span> <span data-ttu-id="c1e3b-106">Ofertę musi być toostaging certyfikowanych toobe naciśnięty.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-106">Your offer must be certified toobe pushed toostaging.</span></span>

<span data-ttu-id="c1e3b-107">Po przemieszczeniu oferta hello można wyświetlać i przetestować hello oferty w hello [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c1e3b-107">After hello offer is staged, you can view and test hello offer in hello [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="c1e3b-108">Wykonaj kroki hello poniżej toopush toostaging Twojej oferty i przetestować go w hello [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="c1e3b-108">Follow hello steps below toopush your offer toostaging and test it in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="c1e3b-109">Przejdź toohello [Portal publikowania](https://publish.windowsazure.com) > **szablony rozwiązań** kartę > ofertę > **publikowania** > **Push tooStaging** .</span><span class="sxs-lookup"><span data-stu-id="c1e3b-109">Go toohello [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push tooStaging**.</span></span>
2. <span data-ttu-id="c1e3b-110">Zawierają hello listę subskrypcji platformy Azure, będzie używać toopreview i przetestować ofertę.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-110">Provide hello list of Azure subscriptions that you will use toopreview and test your offer.</span></span>
3. <span data-ttu-id="c1e3b-111">Zaloguj się w portalu Azure w wersji zapoznawczej toohello przy użyciu Identyfikatora subskrypcji hello, który został użyty w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-111">Sign in toohello Azure preview portal by using hello subscription ID that you used in hello previous step.</span></span>
4. <span data-ttu-id="c1e3b-112">Wykonuje round co najmniej jedną testowania w portalu Azure w wersji zapoznawczej hello w punktach hello wymienionych poniżej:</span><span class="sxs-lookup"><span data-stu-id="c1e3b-112">Carry out at least one round of testing in hello Azure preview portal on hello points mentioned below:</span></span>
   * <span data-ttu-id="c1e3b-113">Upewnij się, że marketingu zawartości jest wyświetlane poprawnie w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-113">Make sure that marketing content shows up correctly in hello Azure Marketplace.</span></span>
   * <span data-ttu-id="c1e3b-114">Wdrażanie na trasie hello topologii.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-114">End-to-end deployment of hello topology.</span></span>
   * <span data-ttu-id="c1e3b-115">Wykonaj test wydajności, a testy obciążenia.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="c1e3b-116">Upewnij się, że topologii opiera się toohello najlepszych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-116">Ensure that your topology adheres toohello best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1e3b-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1e3b-117">Next steps</span></span>
<span data-ttu-id="c1e3b-118">Jeśli są zadowalające hello wyniki, a następnie przejściem toohello oferta końcowego publikowania fazy, **krok 4**: [wdrażanie toohello Twojego oferta portalu Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="c1e3b-118">If you are satisfied with hello results, then you can proceed toohello final offer publishing phase, **Step 4**:  [Deploying your offer toohello Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="c1e3b-119">W przeciwnym razie zmiany w ramach Twojej oferty, a żądanie certyfikacji ponownie.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="c1e3b-120">Marketing zmian zawartości certyfikacji nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="c1e3b-121">Zobacz [wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md) dla zadań wydawca przewodnika tooall.</span><span class="sxs-lookup"><span data-stu-id="c1e3b-121">See [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md) for a guide tooall publisher tasks.</span></span>

