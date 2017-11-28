---
title: "aaaAzure zarządzanych aplikacji hello Marketplace | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano Azure zarządzane aplikacje, które są dostępne za pośrednictwem hello Marketplace."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b3cdf3f1fccdd47db699e4892ae8bce35118bfd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-managed-applications-in-hello-marketplace"></a><span data-ttu-id="f9610-103">Azure zarządzanych aplikacji hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="f9610-103">Azure managed applications in hello Marketplace</span></span>

 <span data-ttu-id="f9610-104">MSPs, niezależnym dostawcom oprogramowania i integratorów systemów. platforma (SIs) mogą korzystać z usługi Azure zarządzane aplikacje toooffer swoim klientom rozwiązań tooall portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9610-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications toooffer their solutions tooall Azure Marketplace customers.</span></span> <span data-ttu-id="f9610-105">W przypadku takich rozwiązań zmniejszyć hello konserwacji i obsługi obciążenia dla klientów.</span><span class="sxs-lookup"><span data-stu-id="f9610-105">Such solutions reduce hello maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="f9610-106">Wydawcy sprzedać infrastruktury i oprogramowaniem za pośrednictwem hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9610-106">Publishers can sell infrastructure and software through hello Marketplace.</span></span> <span data-ttu-id="f9610-107">Ich można dołączyć usługi i aplikacje toomanaged operacyjne pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="f9610-107">They can attach services and operational support toomanaged applications.</span></span> <span data-ttu-id="f9610-108">Aby uzyskać więcej informacji, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="f9610-109">W tym artykule opisano, jak MSP, niezależnego dostawcy oprogramowania lub SI publikowania aplikacji toohello Marketplace i stał się toocustomers szeroko dostępne.</span><span class="sxs-lookup"><span data-stu-id="f9610-109">This article explains how an MSP, ISV, or SI can publish an application toohello Marketplace and make it broadly available toocustomers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="f9610-110">Wymagania wstępne dotyczące publikowania aplikacji zarządzanej</span><span class="sxs-lookup"><span data-stu-id="f9610-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="f9610-111">Wymagania wstępne toolisting w hello Marketplace:</span><span class="sxs-lookup"><span data-stu-id="f9610-111">Prerequisites toolisting in hello Marketplace:</span></span>

* <span data-ttu-id="f9610-112">Techniczne</span><span class="sxs-lookup"><span data-stu-id="f9610-112">Technical</span></span>

    *  <span data-ttu-id="f9610-113">Uzyskać informacje o podstawowej struktury hello i składni szablonów usługi Azure Resource Manager, zobacz [szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-113">For information about hello basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="f9610-114">tooview pełny szablon rozwiązania, zobacz [szablonów Szybki Start Azure](https://azure.microsoft.com/en-us/documentation/templates/) lub hello [repozytorium szablonów Szybki Start](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="f9610-114">tooview complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or hello [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="f9610-115">Informacje, jak toocreate hello interfejs dla klientów, którzy wdrażania aplikacji za pośrednictwem hello Marketplace, zobacz [Utwórz plik definicji interfejsu użytkownika](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-115">For information about how toocreate hello interface for customers who deploy your application through hello Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="f9610-116">Nietechnicznym (wymagania biznesowe)</span><span class="sxs-lookup"><span data-stu-id="f9610-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="f9610-117">Firmy lub zależnemu musi znajdować się w danym kraju, w którym sprzedaży są obsługiwane przez hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9610-117">Your company or its subsidiary must be located in a country where sales are supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="f9610-118">W taki sposób, który jest zgodny z rozliczeń modeli obsługiwanych przez hello Marketplace muszą mieć licencję na produkt.</span><span class="sxs-lookup"><span data-stu-id="f9610-118">Your product must be licensed in a way that is compatible with billing models supported by hello Marketplace.</span></span>
    *   <span data-ttu-id="f9610-119">Wszystko jest odpowiedzialny za tworzenie toocustomers dostępna Pomoc techniczna w sposób uzasadnione ekonomicznie.</span><span class="sxs-lookup"><span data-stu-id="f9610-119">You're responsible for making technical support available toocustomers in a commercially reasonable manner.</span></span> <span data-ttu-id="f9610-120">Obsługa Hello można wolny, płatną, lub za pośrednictwem społeczności obsługuje.</span><span class="sxs-lookup"><span data-stu-id="f9610-120">hello support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="f9610-121">Wszystko jest odpowiedzialny za Licencjonowanie oprogramowanie oraz wszystkie zależności oprogramowania innych firm.</span><span class="sxs-lookup"><span data-stu-id="f9610-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="f9610-122">Należy udostępnić zawartość, która spełnia kryteria dotyczące Twojej oferty toobe wymienione w hello Marketplace hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f9610-122">You must provide content that meets criteria for your offering toobe listed in hello Marketplace and in hello Azure portal.</span></span>
    *   <span data-ttu-id="f9610-123">Musisz zaakceptować warunki toohello hello Azure Marketplace udział zasad i umowy wydawcy.</span><span class="sxs-lookup"><span data-stu-id="f9610-123">You must agree toohello terms of hello Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="f9610-124">Musisz zaakceptować toocomply hello warunki użytkowania, zasady zachowania poufności informacji firmy Microsoft i certyfikowane umowę programu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f9610-124">You must agree toocomply with hello Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="f9610-125">Tworzenie nowej oferty aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="f9610-125">Create a new Azure application offer</span></span>

<span data-ttu-id="f9610-126">Po hello wymagania wstępne zostały spełnione, wszystko jest gotowe toocreate ofertę zarządzanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f9610-126">After you meet hello prerequisites, you're ready toocreate your managed application offer.</span></span> <span data-ttu-id="f9610-127">Spójrzmy szybki przegląd oferty i jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f9610-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="f9610-128">Oferta</span><span class="sxs-lookup"><span data-stu-id="f9610-128">Offer</span></span>

<span data-ttu-id="f9610-129">Oferta Hello zarządzanych aplikacji odpowiada klasy tooa produktu oferty od wydawcy.</span><span class="sxs-lookup"><span data-stu-id="f9610-129">hello offer for a managed application corresponds tooa class of product offering from a publisher.</span></span> <span data-ttu-id="f9610-130">Jeśli masz nowy typ aplikacji rozwiązania, które mają toomake dostępne w portalu Marketplace hello, można go skonfigurować jako nowej oferty.</span><span class="sxs-lookup"><span data-stu-id="f9610-130">If you have a new type of solution/application that you want toomake available in hello Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="f9610-131">Oferta jest kolekcją jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f9610-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="f9610-132">Każdy oferty jest wyświetlany jako własnej jednostce w hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9610-132">Every offer appears as its own entity in hello Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="f9610-133">SKU</span><span class="sxs-lookup"><span data-stu-id="f9610-133">SKU</span></span>

<span data-ttu-id="f9610-134">Jednostka SKU jest hello najmniejszej płatnej wersji jednostki oferty.</span><span class="sxs-lookup"><span data-stu-id="f9610-134">A SKU is hello smallest purchasable unit of an offer.</span></span> <span data-ttu-id="f9610-135">SKU w hello można użyć tego samego produktu toodifferentiate klasy (Oferta) między:</span><span class="sxs-lookup"><span data-stu-id="f9610-135">You can use a SKU within hello same product class (offer) toodifferentiate between:</span></span>

* <span data-ttu-id="f9610-136">Różne funkcje, które są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f9610-136">Different features that are supported.</span></span>
* <span data-ttu-id="f9610-137">Określa, czy oferta hello jest zarządzane lub niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="f9610-137">Whether hello offer is managed or unmanaged.</span></span>
* <span data-ttu-id="f9610-138">Modele rozliczeń, które są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f9610-138">Billing models that are supported.</span></span>

<span data-ttu-id="f9610-139">Jednostka SKU jest wyświetlany w obszarze hello nadrzędnego oferty w hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9610-139">A SKU appears under hello parent offer in hello Marketplace.</span></span> <span data-ttu-id="f9610-140">Wygląda na to jako własnej jednostce oferowane w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f9610-140">It appears as its own purchasable entity in hello Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="f9610-141">Konfigurowanie oferty</span><span class="sxs-lookup"><span data-stu-id="f9610-141">Set up an offer</span></span>

1. <span data-ttu-id="f9610-142">Zaloguj się toohello [portalu dla partnerów chmury](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f9610-142">Sign in toohello [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="f9610-143">W okienku nawigacji hello powitania po lewej stronie wybierz **+ nowe oferty** > **aplikacji Azure**.</span><span class="sxs-lookup"><span data-stu-id="f9610-143">In hello navigation pane on hello left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Nowa oferta](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="f9610-145">Wypełnianie formularzy hello, pojawiające się na powitania w hello **edytor** widoku.</span><span class="sxs-lookup"><span data-stu-id="f9610-145">Fill out hello forms that appear on hello left in hello **Editor** view.</span></span> <span data-ttu-id="f9610-146">Wymagane pola są oznaczone czerwoną gwiazdką (*).</span><span class="sxs-lookup"><span data-stu-id="f9610-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Ustawienia oferty](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="f9610-148">Cztery główne formularze są używane toocreate zarządzanej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f9610-148">Four main forms are used toocreate a managed application:</span></span>

    <span data-ttu-id="f9610-149">a.</span><span class="sxs-lookup"><span data-stu-id="f9610-149">a.</span></span> <span data-ttu-id="f9610-150">Ustawienia oferty</span><span class="sxs-lookup"><span data-stu-id="f9610-150">Offer Settings</span></span>

    <span data-ttu-id="f9610-151">b.</span><span class="sxs-lookup"><span data-stu-id="f9610-151">b.</span></span> <span data-ttu-id="f9610-152">Jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="f9610-152">SKUs</span></span>

    <span data-ttu-id="f9610-153">c.</span><span class="sxs-lookup"><span data-stu-id="f9610-153">c.</span></span> <span data-ttu-id="f9610-154">Portal Marketplace</span><span class="sxs-lookup"><span data-stu-id="f9610-154">Marketplace</span></span>

    <span data-ttu-id="f9610-155">d.</span><span class="sxs-lookup"><span data-stu-id="f9610-155">d.</span></span> <span data-ttu-id="f9610-156">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="f9610-156">Support</span></span>

<span data-ttu-id="f9610-157">Formularze są opisane bardziej szczegółowo na powitania następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="f9610-157">These forms are described in greater detail in hello following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="f9610-158">Formularz Ustawienia oferty</span><span class="sxs-lookup"><span data-stu-id="f9610-158">Offer Settings form</span></span>
<span data-ttu-id="f9610-159">Użyj tego formularza podstawowego toospecify hello oferta ustawień.</span><span class="sxs-lookup"><span data-stu-id="f9610-159">Use this basic form toospecify hello offer settings.</span></span>

1. <span data-ttu-id="f9610-160">Wypełnij hello **oferują ustawienia** formularza.</span><span class="sxs-lookup"><span data-stu-id="f9610-160">Fill in hello **Offer Settings** form.</span></span> <span data-ttu-id="f9610-161">są polami Hello:</span><span class="sxs-lookup"><span data-stu-id="f9610-161">hello different fields are:</span></span>

    <span data-ttu-id="f9610-162">a.</span><span class="sxs-lookup"><span data-stu-id="f9610-162">a.</span></span> <span data-ttu-id="f9610-163">**Identyfikator oferty**: ten unikatowy identyfikator identyfikuje oferta hello w profilu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="f9610-163">**Offer ID**: This unique identifier identifies hello offer within a publisher profile.</span></span> <span data-ttu-id="f9610-164">Ten identyfikator jest widoczny w adresach URL produktu, szablony usługi Resource Manager i raporty rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="f9610-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="f9610-165">Go mogą się składać tylko małe znaki alfanumeryczne i łączniki (-).</span><span class="sxs-lookup"><span data-stu-id="f9610-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="f9610-166">Identyfikator Hello nie może kończyć się łącznikiem.</span><span class="sxs-lookup"><span data-stu-id="f9610-166">hello ID can't end in a dash.</span></span> <span data-ttu-id="f9610-167">Jest ograniczona tooa maksymalnie 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="f9610-167">It's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="f9610-168">Po ofertę odbywa się na żywo, to pole jest zablokowane.</span><span class="sxs-lookup"><span data-stu-id="f9610-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="f9610-169">b.</span><span class="sxs-lookup"><span data-stu-id="f9610-169">b.</span></span> <span data-ttu-id="f9610-170">**Identyfikator wydawcy**: za pomocą tej listy rozwijanej toochoose hello wydawcy profilu ma toopublish tej oferty, w obszarze.</span><span class="sxs-lookup"><span data-stu-id="f9610-170">**Publisher ID**: Use this drop-down list toochoose hello publisher profile you want toopublish this offer under.</span></span> <span data-ttu-id="f9610-171">Po ofertę odbywa się na żywo, to pole jest zablokowane.</span><span class="sxs-lookup"><span data-stu-id="f9610-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="f9610-172">c.</span><span class="sxs-lookup"><span data-stu-id="f9610-172">c.</span></span> <span data-ttu-id="f9610-173">**Nazwa**: Ta nazwa wyświetlana dla danej oferty pojawia się w hello Marketplace oraz w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="f9610-173">**Name**: This display name for your offer appears in hello Marketplace and in hello portal.</span></span> <span data-ttu-id="f9610-174">Może mieć maksymalnie 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="f9610-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="f9610-175">Obejmują rozpoznawalną nazwę markę produktu.</span><span class="sxs-lookup"><span data-stu-id="f9610-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="f9610-176">Nie zawierają nazwę swojej firmy, chyba że jest sposób jest ona sprzedawane.</span><span class="sxs-lookup"><span data-stu-id="f9610-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="f9610-177">Jeśli ta oferta jest marketingu na własne witryny sieci Web, upewnij się, czy nazwa hello jest dokładnie sposobu jej wyświetlania w witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f9610-177">If you're marketing this offer on your own website, ensure that hello name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="f9610-178">Wybierz **zapisać** toosave postęp.</span><span class="sxs-lookup"><span data-stu-id="f9610-178">Select **Save** toosave your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="f9610-179">Formularz jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="f9610-179">SKUs form</span></span>
<span data-ttu-id="f9610-180">Witaj następnym krokiem jest jednostki SKU tooadd dla danej oferty.</span><span class="sxs-lookup"><span data-stu-id="f9610-180">hello next step is tooadd SKUs for your offer.</span></span>

1. <span data-ttu-id="f9610-181">Wybierz **jednostki SKU** > **nowe jednostki SKU**.</span><span class="sxs-lookup"><span data-stu-id="f9610-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Wybierz nowe jednostki SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="f9610-183">Wprowadź **identyfikator jednostki SKU**.</span><span class="sxs-lookup"><span data-stu-id="f9610-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="f9610-184">Identyfikator jednostki SKU to unikatowy identyfikator dla hello SKU oferta.</span><span class="sxs-lookup"><span data-stu-id="f9610-184">A SKU ID is a unique identifier for hello SKU within an offer.</span></span> <span data-ttu-id="f9610-185">Ten identyfikator jest widoczny w adresach URL produktu, szablony usługi Resource Manager i raporty rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="f9610-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="f9610-186">Go mogą się składać tylko małe znaki alfanumeryczne i łączniki (-).</span><span class="sxs-lookup"><span data-stu-id="f9610-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="f9610-187">Identyfikator Hello nie może kończyć się kreską i jest ograniczone tooa maksymalnie 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="f9610-187">hello ID can't end in a dash, and it's limited tooa maximum of 50 characters.</span></span> <span data-ttu-id="f9610-188">Po ofertę odbywa się na żywo, to pole jest zablokowane.</span><span class="sxs-lookup"><span data-stu-id="f9610-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="f9610-189">Może mieć wiele jednostek SKU oferta.</span><span class="sxs-lookup"><span data-stu-id="f9610-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="f9610-190">Należy jednostki SKU dla każdego obrazu planujesz toopublish.</span><span class="sxs-lookup"><span data-stu-id="f9610-190">You need a SKU for each image you plan toopublish.</span></span>

3. <span data-ttu-id="f9610-191">Wypełnianie hello **szczegóły jednostki SKU** sekcji na powitania następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="f9610-191">Fill out hello **SKU Details** section on hello following form:</span></span>

    ![Podaj nowe jednostki SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="f9610-193">Wypełnianie hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f9610-193">Fill out hello following fields:</span></span>
    
    <span data-ttu-id="f9610-194">a.</span><span class="sxs-lookup"><span data-stu-id="f9610-194">a.</span></span> <span data-ttu-id="f9610-195">**Tytuł**: Podaj tytuł tej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f9610-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="f9610-196">Ten tytuł pojawi się w galerii powitania dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="f9610-196">This title appears in hello gallery for this item.</span></span>

    <span data-ttu-id="f9610-197">b.</span><span class="sxs-lookup"><span data-stu-id="f9610-197">b.</span></span> <span data-ttu-id="f9610-198">**Podsumowanie**: Podaj krótkie podsumowanie dla tej wersji produktu.</span><span class="sxs-lookup"><span data-stu-id="f9610-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="f9610-199">Ten tekst jest wyświetlany poniżej hello tytułu.</span><span class="sxs-lookup"><span data-stu-id="f9610-199">This text appears underneath hello title.</span></span>

    <span data-ttu-id="f9610-200">c.</span><span class="sxs-lookup"><span data-stu-id="f9610-200">c.</span></span> <span data-ttu-id="f9610-201">**Opis elementu**: Podaj szczegółowy opis hello jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f9610-201">**Description**: Enter a detailed description about hello SKU.</span></span>

    <span data-ttu-id="f9610-202">d.</span><span class="sxs-lookup"><span data-stu-id="f9610-202">d.</span></span> <span data-ttu-id="f9610-203">**Typ jednostki SKU**: hello dozwolone wartości to **zarządzanej aplikacji** i **szablony rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="f9610-203">**SKU Type**: hello allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="f9610-204">W tym przypadku wybierz **zarządzanej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="f9610-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="f9610-205">Wypełnianie hello **informacje szczegółowe dotyczące pakietu** sekcji na powitania następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="f9610-205">Fill out hello **Package Details** section on hello following form:</span></span>

    ![Pakiet](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="f9610-207">Wypełnianie hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f9610-207">Fill out hello following fields:</span></span>

    <span data-ttu-id="f9610-208">a.</span><span class="sxs-lookup"><span data-stu-id="f9610-208">a.</span></span> <span data-ttu-id="f9610-209">**Bieżąca wersja**: wprowadź wersję pakietu hello przekazywania.</span><span class="sxs-lookup"><span data-stu-id="f9610-209">**Current Version**: Enter a version for hello package you upload.</span></span> <span data-ttu-id="f9610-210">Powinna być w formacie hello `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="f9610-210">It should be in hello format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="f9610-211">b.</span><span class="sxs-lookup"><span data-stu-id="f9610-211">b.</span></span> <span data-ttu-id="f9610-212">**Wybierz plik pakietu**: ten pakiet zawiera następujące pliki, które są kompresowane do pliku zip hello:</span><span class="sxs-lookup"><span data-stu-id="f9610-212">**Select a package file**: This package contains hello following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="f9610-213">**applianceMainTemplate.json**: hello wdrażania szablonu pliku, który został użyty hello toodeploy rozwiązania/aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f9610-213">**applianceMainTemplate.json**: hello deployment template file that's used toodeploy hello solution/application.</span></span> <span data-ttu-id="f9610-214">Aby uzyskać informacje na temat toocreate plików szablonu wdrażania, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-214">For information about how toocreate deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="f9610-215">**appliancecreateUIDefinition.json**: ten plik jest używany przez interfejs użytkownika hello Azure toogenerate portalu hello, który został użyty tooprovision rozwiązania/aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f9610-215">**appliancecreateUIDefinition.json**: This file is used by hello Azure portal toogenerate hello user interface that's used tooprovision this solution/application.</span></span> <span data-ttu-id="f9610-216">Aby uzyskać więcej informacji, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="f9610-217">**mainTemplate.json**: ten plik szablonu zawiera tylko hello Microsoft.Solution/appliances zasobu.</span><span class="sxs-lookup"><span data-stu-id="f9610-217">**mainTemplate.json**: This template file contains only hello Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="f9610-218">Plik mainTemplate Hello zawiera hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="f9610-218">hello mainTemplate file includes hello following properties:</span></span>

        *  <span data-ttu-id="f9610-219">**rodzaj**: Użyj **Marketplace** zarządzanych aplikacji w hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9610-219">**kind**: Use **Marketplace** for managed applications in hello Marketplace.</span></span>
        *  <span data-ttu-id="f9610-220">**ManagedResourceGroupId**: Ta grupa zasobów w subskrypcji powitania klienta jest wdrożonym wszystkie zasoby hello zdefiniowane w applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="f9610-220">**ManagedResourceGroupId**: This resource group in hello customer's subscription is where all hello resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="f9610-221">**PublisherPackageId**: ten ciąg unikatowo identyfikujący hello pakietu.</span><span class="sxs-lookup"><span data-stu-id="f9610-221">**PublisherPackageId**: This string uniquely identifies hello package.</span></span> <span data-ttu-id="f9610-222">Podaj wartość hello w formacie hello `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="f9610-222">Provide hello value in hello format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="f9610-223">Uzyskaj hello **identyfikator oferty** i **identyfikator wydawcy** z hello publikowania portalu, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="f9610-223">Obtain hello **Offer ID** and **Publisher ID** from hello publishing portal, as shown in hello following image:</span></span>

![Identyfikator oferty](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="f9610-225">Uzyskaj hello **identyfikator jednostki SKU**, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="f9610-225">Obtain hello **SKU ID**, as shown in hello following image:</span></span>

![IDENTYFIKATOR JEDNOSTKI SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="f9610-227">Uzyskiwanie pakietu hello **wersji**, jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="f9610-227">Obtain hello package **Version**, as shown in hello following image:</span></span>

![Wersja pakietu](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="f9610-229">Oparte na powitania poprzedzających przykłady, hello wartość **PublisherPackageId** jest `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="f9610-229">Based on hello preceding examples, hello value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="f9610-230">Przykładowe mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="f9610-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify hello name of hello storage account"
        }
      },
      "storageAccountType": {
        "type": "string"
      }
    },
    "variables": {
      "managedResourceGroup": "[concat(resourceGroup().id,uniquestring(resourceGroup().id))]"
    },
    "resources": [{
      "type": "Microsoft.Solutions/appliances",
      "apiVersion": "2016-09-01-preview",
      "name": "[concat(parameters('storageAccountNamePrefix'), '-', 'managed')]",
      "location": "[resourceGroup().location]",
      "kind": "marketplace",
      "properties": {
        "managedResourceGroupId": "[variables('managedResourceGroup')]",
        "PublisherPackageId":"azureappliancetest.ravmanagedapptest.ravpreviewmanagedsku.1.0.0",
        "parameters": {
          "storageAccountName": {
            "value": "[parameters('storageAccountNamePrefix')]"
          },
          "storageAccountType": {
            "value": "[parameters('storageAccountType')]"
          }
        }
      }
    }],
    "outputs": {

    }
  }
  ```

<span data-ttu-id="f9610-231">Ten pakiet powinien zawierać zagnieżdżone szablony i skrypty, które są wymagane toosuccessfully inicjowania obsługi administracyjnej tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f9610-231">This package should contain any other nested templates or scripts that are required toosuccessfully provision this application.</span></span> <span data-ttu-id="f9610-232">Witaj mainTemplate.json, applianceMainTemplate.json i applianceCreateUIDefinition.json pliki muszą znajdować się w folderze głównym hello.</span><span class="sxs-lookup"><span data-stu-id="f9610-232">hello mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at hello root folder.</span></span>

* <span data-ttu-id="f9610-233">**Autoryzacje**: Ta właściwość określa, kto otrzymuje dostęp i hello poziom dostępu toohello zasobów w subskrypcji klientów.</span><span class="sxs-lookup"><span data-stu-id="f9610-233">**Authorizations**: This property defines who gets access and hello level of access toohello resources in customers' subscriptions.</span></span> <span data-ttu-id="f9610-234">Wydawca Hello można użyć aplikacji hello toomanage w imieniu powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="f9610-234">hello publisher can use it toomanage hello application on behalf of hello customer.</span></span>
* <span data-ttu-id="f9610-235">**PrincipalId**: Ta właściwość jest hello Azure Active Directory (Azure AD) identyfikator użytkownika, grupy użytkowników lub aplikacji, która ma pewne uprawnienia na powitania zasobów w subskrypcji powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="f9610-235">**PrincipalId**: This property is hello Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on hello resources in hello customer's subscription.</span></span> <span data-ttu-id="f9610-236">Witaj definicji roli opisano hello uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="f9610-236">hello Role Definition describes hello permissions.</span></span> 
* <span data-ttu-id="f9610-237">**Definicja roli**: Ta właściwość jest lista wszystkich hello wbudowanych kontroli dostępu opartej na rolach (RBAC) ról dostarczane przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9610-237">**Role Definition**: This property is a list of all hello built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="f9610-238">Możesz wybrać hello roli, która jest najbardziej odpowiednia toouse toomanage hello zasobów w imieniu powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="f9610-238">You can select hello role that's most appropriate toouse toomanage hello resources on behalf of hello customer.</span></span>

<span data-ttu-id="f9610-239">Można dodać wiele zezwolenia.</span><span class="sxs-lookup"><span data-stu-id="f9610-239">You can add multiple authorizations.</span></span> <span data-ttu-id="f9610-240">Zaleca się utworzenie grupy użytkowników usługi AD i określić jej identyfikator w **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="f9610-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="f9610-241">W ten sposób można dodać więcej użytkowników toohello grupy użytkowników bez hello potrzeby tooupdate hello jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f9610-241">This way, you can add more users toohello user group without hello need tooupdate hello SKU.</span></span>

<span data-ttu-id="f9610-242">Aby uzyskać więcej informacji o RBAC, zobacz [wprowadzenie RBAC w portalu Azure hello](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-242">For more information about RBAC, see [Get started with RBAC in hello Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="f9610-243">Formularz Marketplace</span><span class="sxs-lookup"><span data-stu-id="f9610-243">Marketplace form</span></span>

<span data-ttu-id="f9610-244">Hello formularza Marketplace wprowadza się pola, które są widoczne na powitania [portalu Azure Marketplace](https://azuremarketplace.microsoft.com) i na powitania [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f9610-244">hello Marketplace form asks for fields that show up on hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and on hello [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="f9610-245">Identyfikatory subskrypcji w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="f9610-245">Preview subscription IDs</span></span>

<span data-ttu-id="f9610-246">Wprowadź listę identyfikatorów, które mogą uzyskiwać dostęp do oferty powitania po opublikowaniu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f9610-246">Enter a list of Azure subscription IDs that can access hello offer after it's published.</span></span> <span data-ttu-id="f9610-247">Można użyć tych oferta hello podglądu tootest wymienione biały subskrypcji przed wprowadzeniem jej na żywo.</span><span class="sxs-lookup"><span data-stu-id="f9610-247">You can use these white-listed subscriptions tootest hello previewed offer before you make it live.</span></span> <span data-ttu-id="f9610-248">Kompiluje listę biały się too100 subskrypcji w portalu dla partnerów hello.</span><span class="sxs-lookup"><span data-stu-id="f9610-248">You can compile a white list of up too100 subscriptions in hello partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="f9610-249">Kategorii sugerowanych</span><span class="sxs-lookup"><span data-stu-id="f9610-249">Suggested categories</span></span>

<span data-ttu-id="f9610-250">Wybierz się toofive kategorii z listy hello ofertę może być najlepiej skojarzone z.</span><span class="sxs-lookup"><span data-stu-id="f9610-250">Select up toofive categories from hello list that your offer can be best associated with.</span></span> <span data-ttu-id="f9610-251">Te kategorie są używane toomap kategorie produktów toohello oferta dostępnych w hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com) i hello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f9610-251">These categories are used toomap your offer toohello product categories that are available in hello [Azure Marketplace](https://azuremarketplace.microsoft.com) and hello [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="f9610-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f9610-252">Azure Marketplace</span></span>

<span data-ttu-id="f9610-253">Podsumowanie Hello zarządzanych aplikacji wyświetla hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f9610-253">hello summary of your managed application displays hello following fields:</span></span>

![Podsumowanie witryny Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="f9610-255">Witaj **omówienie** karcie dla aplikacji zarządzanej Wyświetla hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f9610-255">hello **Overview** tab for your managed application displays hello following fields:</span></span>

![Omówienie portalu Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="f9610-257">Witaj **planów + cennik** karcie dla aplikacji zarządzanej Wyświetla hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f9610-257">hello **Plans + Pricing** tab for your managed application displays hello following fields:</span></span>

![Plany Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="f9610-259">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f9610-259">Azure portal</span></span>

<span data-ttu-id="f9610-260">Podsumowanie Hello zarządzanych aplikacji wyświetla hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f9610-260">hello summary of your managed application displays hello following fields:</span></span>

![Portal podsumowania](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="f9610-262">Omówienie Hello aplikacji zarządzanej Wyświetla hello następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f9610-262">hello overview for your managed application displays hello following fields:</span></span>

![Przegląd portalu](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="f9610-264">Wytycznych dotyczących logo</span><span class="sxs-lookup"><span data-stu-id="f9610-264">Logo guidelines</span></span>

<span data-ttu-id="f9610-265">Skorzystaj z następujących wskazówek dla dowolnego logo, które należy przekazać w portalu dla partnerów chmury hello:</span><span class="sxs-lookup"><span data-stu-id="f9610-265">Follow these guidelines for any logo that you upload in hello Cloud Partner portal:</span></span>

*   <span data-ttu-id="f9610-266">Hello Azure projekt ma paletę kolorów proste.</span><span class="sxs-lookup"><span data-stu-id="f9610-266">hello Azure design has a simple color palette.</span></span> <span data-ttu-id="f9610-267">Ogranicz liczbę hello podstawowym i pomocniczym kolorów na logo.</span><span class="sxs-lookup"><span data-stu-id="f9610-267">Limit hello number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="f9610-268">kolorów motywu Hello portalu hello są białe i czarne.</span><span class="sxs-lookup"><span data-stu-id="f9610-268">hello theme colors of hello portal are white and black.</span></span> <span data-ttu-id="f9610-269">Nie używaj kolorów te jako kolor tła hello logo.</span><span class="sxs-lookup"><span data-stu-id="f9610-269">Don't use these colors as hello background color for your logo.</span></span> <span data-ttu-id="f9610-270">Użyj kolor, który umożliwia widoczne w portalu hello logo.</span><span class="sxs-lookup"><span data-stu-id="f9610-270">Use a color that makes your logo prominent in hello portal.</span></span> <span data-ttu-id="f9610-271">Zaleca się proste kolorów podstawowych.</span><span class="sxs-lookup"><span data-stu-id="f9610-271">We recommend simple primary colors.</span></span> <span data-ttu-id="f9610-272">*Jeśli używasz przezroczyste tło, upewnij się, hello logo i tekst są białe, czarne lub niebieski.*</span><span class="sxs-lookup"><span data-stu-id="f9610-272">*If you use a transparent background, make sure that hello logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="f9610-273">Nie używaj gradientu tła na powitania logo.</span><span class="sxs-lookup"><span data-stu-id="f9610-273">Don't use a gradient background on hello logo.</span></span>
*   <span data-ttu-id="f9610-274">Nie należy umieszczać na powitania logo, nawet Twoja firma lub marką tekstu.</span><span class="sxs-lookup"><span data-stu-id="f9610-274">Don't place text on hello logo, not even your company or brand name.</span></span> <span data-ttu-id="f9610-275">Witaj wygląd i działanie logo powinny być płaski i uniknąć gradienty.</span><span class="sxs-lookup"><span data-stu-id="f9610-275">hello look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="f9610-276">Upewnij się, że nie jest rozciągana hello logo.</span><span class="sxs-lookup"><span data-stu-id="f9610-276">Make sure hello logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="f9610-277">Logo bohater</span><span class="sxs-lookup"><span data-stu-id="f9610-277">Hero logo</span></span>

<span data-ttu-id="f9610-278">logo bohater Hello jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="f9610-278">hello hero logo is optional.</span></span> <span data-ttu-id="f9610-279">Wydawca Hello można nie tooupload logo bohater.</span><span class="sxs-lookup"><span data-stu-id="f9610-279">hello publisher can choose not tooupload a hero logo.</span></span> <span data-ttu-id="f9610-280">Po przekazaniu hello bohater ikony, nie można usunąć.</span><span class="sxs-lookup"><span data-stu-id="f9610-280">After hello hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="f9610-281">W tym czasie partnera hello musi występować po hello Marketplace wytyczne dotyczące bohater ikon.</span><span class="sxs-lookup"><span data-stu-id="f9610-281">At that time, hello partner must follow hello Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="f9610-282">Skorzystaj z następujących wskazówek dla ikony logo bohater hello:</span><span class="sxs-lookup"><span data-stu-id="f9610-282">Follow these guidelines for hello hero logo icon:</span></span>

*   <span data-ttu-id="f9610-283">Nazwa wyświetlana Hello wydawcy, tytuł planu hello i długie Podsumowanie oferty hello są wyświetlane w biały.</span><span class="sxs-lookup"><span data-stu-id="f9610-283">hello publisher display name, hello plan title, and hello offer long summary are displayed in white.</span></span> <span data-ttu-id="f9610-284">W związku z tym nie należy używać jasny kolor tła hello hello bohater ikony.</span><span class="sxs-lookup"><span data-stu-id="f9610-284">Therefore, don't use a light color for hello background of hello hero icon.</span></span> <span data-ttu-id="f9610-285">Czarne, białe lub przezroczyste tło nie jest dozwolona dla bohater ikon.</span><span class="sxs-lookup"><span data-stu-id="f9610-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="f9610-286">Po oferta hello jest wyświetlana, hello wydawcy nazwę wyświetlaną, tytuł planu hello, długie Podsumowanie oferty hello i hello **Utwórz** przycisk programowo osadzone wewnątrz hello bohater logo.</span><span class="sxs-lookup"><span data-stu-id="f9610-286">After hello offer is listed, hello publisher display name, hello plan title, hello offer long summary, and hello **Create** button are embedded programmatically inside hello hero logo.</span></span> <span data-ttu-id="f9610-287">W rezultacie nie wprowadź tekst, podczas projektowania hello bohater logo.</span><span class="sxs-lookup"><span data-stu-id="f9610-287">Consequently, don't enter any text while you design hello hero logo.</span></span> <span data-ttu-id="f9610-288">Pozostaw puste miejsce na powitania prawo ponieważ hello tekst jest uwzględniany programowo w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="f9610-288">Leave empty space on hello right because hello text is included programmatically in that space.</span></span> <span data-ttu-id="f9610-289">Witaj wolnego miejsca dla tekstu hello powinna być 415 x 100 pikseli na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="f9610-289">hello empty space for hello text should be 415 x 100 pixels on hello right.</span></span> <span data-ttu-id="f9610-290">Jest on przesunięcia pikseli 370 od lewej hello.</span><span class="sxs-lookup"><span data-stu-id="f9610-290">It's offset by 370 pixels from hello left.</span></span>

    ![Przykład logo bohater](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="f9610-292">Obsługa formularza</span><span class="sxs-lookup"><span data-stu-id="f9610-292">Support form</span></span>

<span data-ttu-id="f9610-293">Wypełnianie hello **obsługuje** formularza z obsługą kontaktuje się z Twojej firmy.</span><span class="sxs-lookup"><span data-stu-id="f9610-293">Fill out hello **Support** form with support contacts from your company.</span></span> <span data-ttu-id="f9610-294">Te informacje mogą inżynierii, kontaktów i kontaktów pomocy technicznej klienta.</span><span class="sxs-lookup"><span data-stu-id="f9610-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="f9610-295">Publikowanie oferty</span><span class="sxs-lookup"><span data-stu-id="f9610-295">Publish an offer</span></span>

<span data-ttu-id="f9610-296">Po wypełnieniu wszystkie sekcje hello wybierz **publikowania** toostart hello procesu, który sprawia, że Twoje toocustomers dostępne oferty.</span><span class="sxs-lookup"><span data-stu-id="f9610-296">After you fill out all hello sections, select **Publish** toostart hello process that makes your offer available toocustomers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9610-297">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9610-297">Next steps</span></span>

* <span data-ttu-id="f9610-298">Wprowadzenie toomanaged aplikacji, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-298">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f9610-299">Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanej z hello Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w portalu Marketplace hello](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-299">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="f9610-300">Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="f9610-301">Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanych katalogu usług, zobacz [korzystać z aplikacji zarządzanych katalogu usług](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="f9610-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
