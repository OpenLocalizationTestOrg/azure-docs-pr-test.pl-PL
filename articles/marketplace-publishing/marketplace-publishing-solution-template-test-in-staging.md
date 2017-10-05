---
title: "Testowanie ofertę szablon rozwiązania dla witryny Marketplace | Dokumentacja firmy Microsoft"
description: "Zrozumienie, jak przetestować ofertę szablon rozwiązania dla portalu Azure Marketplace."
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
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="bce16-103">Testowanie ofertę szablon rozwiązania tymczasowych</span><span class="sxs-lookup"><span data-stu-id="bce16-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="bce16-104">Przemieszczania oznacza wdrażanie ofertę w prywatnej "piaskownicy", gdzie należy przetestować i sprawdzić jego działanie przed wypchnięciem go do produkcji.</span><span class="sxs-lookup"><span data-stu-id="bce16-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="bce16-105">Oferta jest wyświetlany w przemieszczania analogiczny, jak na rzecz klienta, który został wdrożony go.</span><span class="sxs-lookup"><span data-stu-id="bce16-105">The offer appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="bce16-106">Aby zostać przeniesiony do przemieszczania muszą być certyfikowane ofertę.</span><span class="sxs-lookup"><span data-stu-id="bce16-106">Your offer must be certified to be pushed to staging.</span></span>

<span data-ttu-id="bce16-107">Po przemieszczeniu oferty można wyświetlać i przetestować oferty w [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bce16-107">After the offer is staged, you can view and test the offer in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="bce16-108">Wykonaj poniższe kroki, aby push Twojej oferty przemieszczania i przetestować go w [Azure Portal](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="bce16-108">Follow the steps below to push your offer to staging and test it in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="bce16-109">Przejdź do [Portal publikowania](https://publish.windowsazure.com) > **szablony rozwiązań** kartę > ofertę > **publikowania** > **wypychania do przemieszczania**.</span><span class="sxs-lookup"><span data-stu-id="bce16-109">Go to the [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push to Staging**.</span></span>
2. <span data-ttu-id="bce16-110">Podaj listę subskrypcji platformy Azure, które będą używane do przetestowania ofertę.</span><span class="sxs-lookup"><span data-stu-id="bce16-110">Provide the list of Azure subscriptions that you will use to preview and test your offer.</span></span>
3. <span data-ttu-id="bce16-111">Zaloguj się do portalu Azure w wersji zapoznawczej przy użyciu Identyfikatora subskrypcji, który został użyty w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="bce16-111">Sign in to the Azure preview portal by using the subscription ID that you used in the previous step.</span></span>
4. <span data-ttu-id="bce16-112">Wykonuje round co najmniej jedną testowania w portalu Azure w wersji zapoznawczej w punktach wymienionych poniżej:</span><span class="sxs-lookup"><span data-stu-id="bce16-112">Carry out at least one round of testing in the Azure preview portal on the points mentioned below:</span></span>
   * <span data-ttu-id="bce16-113">Upewnij się, że marketingu zawartość zostaną wyświetlone poprawnie w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="bce16-113">Make sure that marketing content shows up correctly in the Azure Marketplace.</span></span>
   * <span data-ttu-id="bce16-114">Wdrażanie na trasie topologii.</span><span class="sxs-lookup"><span data-stu-id="bce16-114">End-to-end deployment of the topology.</span></span>
   * <span data-ttu-id="bce16-115">Wykonaj test wydajności, a testy obciążenia.</span><span class="sxs-lookup"><span data-stu-id="bce16-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="bce16-116">Upewnij się, że topologii opiera się na najlepsze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="bce16-116">Ensure that your topology adheres to the best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bce16-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bce16-117">Next steps</span></span>
<span data-ttu-id="bce16-118">Jeśli są zadowalające wyniki, a następnie można przejść do fazy publikowania końcowego oferta **krok 4**: [wdrażanie Twojej oferty w portalu Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="bce16-118">If you are satisfied with the results, then you can proceed to the final offer publishing phase, **Step 4**:  [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="bce16-119">W przeciwnym razie zmiany w ramach Twojej oferty, a żądanie certyfikacji ponownie.</span><span class="sxs-lookup"><span data-stu-id="bce16-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="bce16-120">Marketing zmian zawartości certyfikacji nie jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="bce16-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="bce16-121">Zobacz [wprowadzenie: jak publikowanie oferty w portalu Azure Marketplace](marketplace-publishing-getting-started.md) przewodnik dotyczący wszystkie zadania wydawcy.</span><span class="sxs-lookup"><span data-stu-id="bce16-121">See [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md) for a guide to all publisher tasks.</span></span>

