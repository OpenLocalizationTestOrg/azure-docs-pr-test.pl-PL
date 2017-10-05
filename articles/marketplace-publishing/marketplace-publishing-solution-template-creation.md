---
title: "Przewodnik dotyczący tworzenia szablonu rozwiązania dla witryny Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje dotyczące sposobu tworzenia, certyfikować i wdrażania wielu maszyn wirtualnych szablon rozwiązania obrazu dla kupić w witrynie Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e14e05f2-2385-4ce0-b351-0747cb74ba19
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: b753bfb4bd69bd9aacf4eebd8999397394c28bc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="guide-to-create-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="54871-103">Przewodnik, aby utworzyć szablon rozwiązania dla portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="54871-103">Guide to create a solution template for Azure Marketplace</span></span>
<span data-ttu-id="54871-104">Po ukończeniu kroku 1, [o tworzeniu konta i rejestracji][link-acct-creation], możemy przewodnikiem po utworzeniu szablonu rozwiązania Azure zgodnego w [techniczne wymagania wstępne dotyczące tworzenia szablonu rozwiązania](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="54871-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on the creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="54871-105">Obecnie firma Microsoft przeprowadzi Cię przez kolejne etapy tworzenia szablonu rozwiązanie dla wielu maszyn wirtualnych na [Portal publikowania] [ link-pubportal] dla portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="54871-105">Now we will walk you through the steps for creating a solution template for multiple VMs on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-the-publishing-portal"></a><span data-ttu-id="54871-106">Utwórz ofertę szablon rozwiązania w portalu publikowania</span><span class="sxs-lookup"><span data-stu-id="54871-106">Create your solution template offer in the Publishing Portal</span></span>
<span data-ttu-id="54871-107">Przejdź do [https://publish.windowsazure.com](http://publish.windowsazure.com). Po zalogowaniu po raz pierwszy do [Portal publikowania](https://publish.windowsazure.com/), użyj tego samego konta z został zarejestrowany w firmie sprzedawcy profilu.</span><span class="sxs-lookup"><span data-stu-id="54871-107">Go to  [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for the first time to the [Publishing Portal](https://publish.windowsazure.com/), use the same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="54871-108">Później możesz dodać każdy pracownik firmy jako współadministrator w portalu publikowania.</span><span class="sxs-lookup"><span data-stu-id="54871-108">Later, you can add any employee of your company as a co-admin in the Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="54871-109">1. Wybierz opcję "Szablony rozwiązań"</span><span class="sxs-lookup"><span data-stu-id="54871-109">1. Select "Solution templates"</span></span>
  ![Rysowanie][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="54871-111">2. Utwórz nowy szablon rozwiązania</span><span class="sxs-lookup"><span data-stu-id="54871-111">2. Create a new solution template</span></span>
  ![Rysowanie][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="54871-113">3. Rozpoczynać się od topologii</span><span class="sxs-lookup"><span data-stu-id="54871-113">3. Start with topologies</span></span>
<span data-ttu-id="54871-114">Szablon rozwiązania jest nadrzędny dla wszystkich jego topologii.</span><span class="sxs-lookup"><span data-stu-id="54871-114">A solution template is a "parent" to all of its topologies.</span></span> <span data-ttu-id="54871-115">Można zdefiniować wiele topologii w jednym szablonie oferty/rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="54871-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="54871-116">Gdy oferta zostanie przeniesiona do etapu przemieszczania, razem z nią zostaną przeniesione wszystkie jej topologie.</span><span class="sxs-lookup"><span data-stu-id="54871-116">When an offer is pushed to staging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="54871-117">Wykonaj poniższe kroki, aby zdefiniować ofertę:</span><span class="sxs-lookup"><span data-stu-id="54871-117">Follow the steps below to define your offer:</span></span>     

* <span data-ttu-id="54871-118">Utworzyć topologię: "Identyfikator topologii" jest zazwyczaj nazwą topologii szablon rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="54871-118">Create a Topology: “Topology Identifier” is typically the name of the topology for the solution template.</span></span> <span data-ttu-id="54871-119">Identyfikator topologii jest używana w adresie URL, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="54871-119">The topology identifier is used in the URL as shown below:</span></span>

  <span data-ttu-id="54871-120">Witrynę Azure Marketplace: http://azure.microsoft.com/marketplace/partners/ {PublisherNamespace} / {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="54871-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="54871-121">Portalu Azure: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="54871-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="54871-122">Dodaj nową wersję.</span><span class="sxs-lookup"><span data-stu-id="54871-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="54871-123">4. Pobieranie Twojej wersji topologii certyfikowane</span><span class="sxs-lookup"><span data-stu-id="54871-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="54871-124">Przekaż plik zip, który zawiera wszystkie wymagane pliki do udostępnienia tej konkretnej wersji topologii.</span><span class="sxs-lookup"><span data-stu-id="54871-124">Upload a zip file that contains all required files to provision that particular version of the topology.</span></span> <span data-ttu-id="54871-125">Ten plik zip musi zawierać następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="54871-125">This zip file must contain the following:</span></span>

* <span data-ttu-id="54871-126">*mainTemplate.json* i *createUiDefinition.json* pliku w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="54871-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="54871-127">Szablony połączone i wszystkie wymagane skrypty.</span><span class="sxs-lookup"><span data-stu-id="54871-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="54871-128">Podczas pracy deweloperów na temat tworzenia rozwiązania topologie szablonu i pobieranie ich certyfikowane, business, marketingu i/lub prawnych działy firmy mogą pracować na zawartość marketing i prawnych.</span><span class="sxs-lookup"><span data-stu-id="54871-128">While your developers work on creating the solution template topologies and getting them certified, the business, marketing, and/or legal departments of your company can work on the marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="54871-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54871-129">Next steps</span></span>
<span data-ttu-id="54871-130">Teraz, gdy zostanie utworzony szablon rozwiązania i przekazać plik zip, postępuj zgodnie z instrukcjami wyświetlanymi w [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) przed wypchnięciem ofertę przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="54871-130">Now that you created your solution template and uploaded the zip file, please follow the instructions in the [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing the offer to staging.</span></span> <span data-ttu-id="54871-131">Aby wyświetlić pełny zestaw marketplace publikowanie artykułów, odwiedź stronę [wprowadzenie: jak publikowanie oferty w portalu Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="54871-131">To see the full set of marketplace publishing articles, visit [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="54871-132">Być może zainteresuje te pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="54871-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="54871-133">Obrazów maszyn wirtualnych: [o obrazy maszyny wirtualnej na platformie Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="54871-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="54871-134">Rozszerzenia maszyny Wirtualnej: [omówienie rozszerzeń maszyny Wirtualnej i Agent maszyny Wirtualnej](https://msdn.microsoft.com/library/azure/dn832621.aspx) i [rozszerzeń maszyny Wirtualnej platformy Azure i funkcje](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="54871-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="54871-135">Usługa Azure Resource Manager: [tworzenia szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) i [przykłady prostego szablonu](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="54871-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="54871-136">Ogranicza konta magazynu: [jak monitorować dla ograniczania konta magazynu](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) i [magazyn w warstwie Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="54871-136">Storage account throttles: [How to Monitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
