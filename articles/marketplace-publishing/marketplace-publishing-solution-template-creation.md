---
title: "toocreating aaaGuide szablon rozwiązania hello Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje sposobu toocreate, certyfikować i wdrażanie szablonu rozwiązania obrazu wielu maszyn wirtualnych na zakupu na hello Azure Marketplace."
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
ms.openlocfilehash: b0e7067176337dd0d3f6f6ec04c963f80f706ab0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toocreate-a-solution-template-for-azure-marketplace"></a><span data-ttu-id="a59c7-103">Przewodnik toocreate szablon rozwiązania do portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="a59c7-103">Guide toocreate a solution template for Azure Marketplace</span></span>
<span data-ttu-id="a59c7-104">Po ukończeniu kroku 1, [o tworzeniu konta i rejestracji][link-acct-creation], możemy przewodnikiem po utworzeniu hello Azure zgodnego szablonu rozwiązania na [techniczne wymagania wstępne dotyczące tworzenia Szablon rozwiązania](marketplace-publishing-solution-template-creation-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="a59c7-104">After completing step 1, [Account creation and registration][link-acct-creation], we guided you on hello creation of an Azure-compatible solution template at [Technical prerequisites for creating a solution template](marketplace-publishing-solution-template-creation-prerequisites.md).</span></span> <span data-ttu-id="a59c7-105">Obecnie firma Microsoft przeprowadzi Cię przez kroki tworzenia szablonu rozwiązanie dla wielu maszyn wirtualnych na powitania hello [Portal publikowania] [ link-pubportal] dla hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a59c7-105">Now we will walk you through hello steps for creating a solution template for multiple VMs on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="create-your-solution-template-offer-in-hello-publishing-portal"></a><span data-ttu-id="a59c7-106">Utwórz ofertę szablon rozwiązania w hello Portal publikowania</span><span class="sxs-lookup"><span data-stu-id="a59c7-106">Create your solution template offer in hello Publishing Portal</span></span>
<span data-ttu-id="a59c7-107">Przejdź za [https://publish.windowsazure.com](http://publish.windowsazure.com). Podczas rejestrowania się w pierwszym toohello czasu hello [Portal publikowania](https://publish.windowsazure.com/), hello Użyj tego samego konta z został zarejestrowany w firmie sprzedawcy profilu.</span><span class="sxs-lookup"><span data-stu-id="a59c7-107">Go too [https://publish.windowsazure.com](http://publish.windowsazure.com). When signing in for hello first time toohello [Publishing Portal](https://publish.windowsazure.com/), use hello same account with which your company’s seller profile was registered.</span></span> <span data-ttu-id="a59c7-108">Później możesz dodać każdy pracownik firmy jako współadministrator w hello Portal publikowania.</span><span class="sxs-lookup"><span data-stu-id="a59c7-108">Later, you can add any employee of your company as a co-admin in hello Publishing Portal.</span></span>

### <a name="1-select-solution-templates"></a><span data-ttu-id="a59c7-109">1. Wybierz opcję "Szablony rozwiązań"</span><span class="sxs-lookup"><span data-stu-id="a59c7-109">1. Select "Solution templates"</span></span>
  ![Rysowanie][img-pubportal-menu-sol-templ]

### <a name="2-create-a-new-solution-template"></a><span data-ttu-id="a59c7-111">2. Utwórz nowy szablon rozwiązania</span><span class="sxs-lookup"><span data-stu-id="a59c7-111">2. Create a new solution template</span></span>
  ![Rysowanie][img-pubportal-sol-templ-new]

### <a name="3-start-with-topologies"></a><span data-ttu-id="a59c7-113">3. Rozpoczynać się od topologii</span><span class="sxs-lookup"><span data-stu-id="a59c7-113">3. Start with topologies</span></span>
<span data-ttu-id="a59c7-114">Szablon rozwiązania jest tooall "elementu nadrzędnego", jego topologii.</span><span class="sxs-lookup"><span data-stu-id="a59c7-114">A solution template is a "parent" tooall of its topologies.</span></span> <span data-ttu-id="a59c7-115">Można zdefiniować wiele topologii w jednym szablonie oferty/rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a59c7-115">You can define multiple topologies in one offer/solution template.</span></span> <span data-ttu-id="a59c7-116">Gdy oferta zostanie przeniesiona toostaging, spoczywa z wszystkich jego topologii.</span><span class="sxs-lookup"><span data-stu-id="a59c7-116">When an offer is pushed toostaging, it is pushed with all of its topologies.</span></span> <span data-ttu-id="a59c7-117">Wykonaj kroki hello poniżej toodefine ofertę:</span><span class="sxs-lookup"><span data-stu-id="a59c7-117">Follow hello steps below toodefine your offer:</span></span>     

* <span data-ttu-id="a59c7-118">Utworzyć topologię: "Identyfikator topologii" jest zazwyczaj nazwą hello topologii hello hello szablon rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="a59c7-118">Create a Topology: “Topology Identifier” is typically hello name of hello topology for hello solution template.</span></span> <span data-ttu-id="a59c7-119">identyfikator topologii Hello jest używany w adresie URL hello, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="a59c7-119">hello topology identifier is used in hello URL as shown below:</span></span>

  <span data-ttu-id="a59c7-120">Witrynę Azure Marketplace: http://azure.microsoft.com/marketplace/partners/ {PublisherNamespace} / {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="a59c7-120">Azure Marketplace: http://azure.microsoft.com/marketplace/partners/{PublisherNamespace}/{OfferIdentifier}{TopologyIdentifier}</span></span>

  <span data-ttu-id="a59c7-121">Portalu Azure: https://portal.azure.com/#gallery/ {PublisherNamespace}. {OfferIdentifier} {TopologyIdentifier}</span><span class="sxs-lookup"><span data-stu-id="a59c7-121">Azure Portal: https://portal.azure.com/#gallery/{PublisherNamespace}.{OfferIdentifier}{TopologyIdentifier}</span></span>
* <span data-ttu-id="a59c7-122">Dodaj nową wersję.</span><span class="sxs-lookup"><span data-stu-id="a59c7-122">Add a new version.</span></span>

### <a name="4-get-your-topology-versions-certified"></a><span data-ttu-id="a59c7-123">4. Pobieranie Twojej wersji topologii certyfikowane</span><span class="sxs-lookup"><span data-stu-id="a59c7-123">4. Get your topology versions certified</span></span>
<span data-ttu-id="a59c7-124">Przekaż plik zip, który zawiera wszystkie wymagane pliki tooprovision tej konkretnej wersji hello topologii.</span><span class="sxs-lookup"><span data-stu-id="a59c7-124">Upload a zip file that contains all required files tooprovision that particular version of hello topology.</span></span> <span data-ttu-id="a59c7-125">Ten plik zip musi zawierać następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a59c7-125">This zip file must contain hello following:</span></span>

* <span data-ttu-id="a59c7-126">*mainTemplate.json* i *createUiDefinition.json* pliku w katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="a59c7-126">*mainTemplate.json* and *createUiDefinition.json* file at its root directory.</span></span>
* <span data-ttu-id="a59c7-127">Szablony połączone i wszystkie wymagane skrypty.</span><span class="sxs-lookup"><span data-stu-id="a59c7-127">Any linked templates and all required scripts.</span></span>

  > [!TIP]
  > <span data-ttu-id="a59c7-128">Podczas pracy deweloperów na temat tworzenia rozwiązania hello topologie szablonu i pobieranie ich certyfikowane, hello business działu marketingu i/lub prawnych firmy może pracować na powitania marketing i prawnych zawartości.</span><span class="sxs-lookup"><span data-stu-id="a59c7-128">While your developers work on creating hello solution template topologies and getting them certified, hello business, marketing, and/or legal departments of your company can work on hello marketing and legal content.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="a59c7-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a59c7-129">Next steps</span></span>
<span data-ttu-id="a59c7-130">Teraz, gdy zostanie utworzony szablon rozwiązania i przekazać plik zip hello, wykonaj instrukcje hello hello [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) przed wypchnięciem toostaging oferta hello.</span><span class="sxs-lookup"><span data-stu-id="a59c7-130">Now that you created your solution template and uploaded hello zip file, please follow hello instructions in hello [Marketplace marketing content guide](marketplace-publishing-push-to-staging.md) before pushing hello offer toostaging.</span></span> <span data-ttu-id="a59c7-131">toosee hello pełny zestaw marketplace publikowanie artykułów, odwiedź stronę [wprowadzenie: jak toopublish toohello oferta portalu Azure Marketplace](marketplace-publishing-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="a59c7-131">toosee hello full set of marketplace publishing articles, visit [Getting started: How toopublish an offer toohello Azure Marketplace](marketplace-publishing-getting-started.md).</span></span>

<span data-ttu-id="a59c7-132">Być może zainteresuje te pokrewne artykuły:</span><span class="sxs-lookup"><span data-stu-id="a59c7-132">You might also be interested in these related articles:</span></span>

* <span data-ttu-id="a59c7-133">Obrazów maszyn wirtualnych: [o obrazy maszyny wirtualnej na platformie Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span><span class="sxs-lookup"><span data-stu-id="a59c7-133">VM images: [About Virtual Machine Images in Azure](https://msdn.microsoft.com/library/azure/dn790290.aspx)</span></span>
* <span data-ttu-id="a59c7-134">Rozszerzenia maszyny Wirtualnej: [omówienie rozszerzeń maszyny Wirtualnej i Agent maszyny Wirtualnej](https://msdn.microsoft.com/library/azure/dn832621.aspx) i [rozszerzeń maszyny Wirtualnej platformy Azure i funkcje](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span><span class="sxs-lookup"><span data-stu-id="a59c7-134">VM extensions: [VM Agent and VM Extensions Overview](https://msdn.microsoft.com/library/azure/dn832621.aspx) and [Azure VM Extensions and Features](https://msdn.microsoft.com/library/azure/dn606311.aspx)</span></span>
* <span data-ttu-id="a59c7-135">Usługa Azure Resource Manager: [tworzenia szablonów usługi Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) i [przykłady prostego szablonu](https://github.com/rjmax/ArmExamples)</span><span class="sxs-lookup"><span data-stu-id="a59c7-135">Azure Resource Manager: [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md) and [Simple Template Examples](https://github.com/rjmax/ArmExamples)</span></span>
* <span data-ttu-id="a59c7-136">Ogranicza konta magazynu: [jak tooMonitor dla ograniczania konta magazynu](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) i [magazyn w warstwie Premium](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span><span class="sxs-lookup"><span data-stu-id="a59c7-136">Storage account throttles: [How tooMonitor for Storage Account Throttling](http://blogs.msdn.com/b/mast/archive/2014/08/02/how-to-monitor-for-storage-account-throttling.aspx) and [Premium storage](../storage/common/storage-premium-storage.md#scalability-and-performance-targets)</span></span>

[img-pubportal-menu-sol-templ]:media/marketplace-publishing-solution-template-creation/pubportal-menu-solution-templates.png
[img-pubportal-sol-templ-new]:media/marketplace-publishing-solution-template-creation/pubportal-solution-template-new.png
[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
[link-pubportal]:https://publish.windowsazure.com
