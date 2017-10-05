---
title: "Azure zarządzanych aplikacji w witrynie Marketplace | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano Azure zarządzane aplikacje, które są dostępne na rynku."
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/09/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: 58ac7665abf7e75a43bb0b92bdf6f41005c3efe8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-managed-applications-in-the-marketplace"></a><span data-ttu-id="f781f-103">Azure zarządzanych aplikacji w witrynie Marketplace</span><span class="sxs-lookup"><span data-stu-id="f781f-103">Azure managed applications in the Marketplace</span></span>

 <span data-ttu-id="f781f-104">MSPs, niezależnym dostawcom oprogramowania i integratorów systemów. platforma (SIs) można używać platformy Azure zarządzanych aplikacji w celu zaoferowania ich rozwiązania dla wszystkich klientów w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f781f-104">MSPs, ISVs, and system integrators (SIs) can use Azure managed applications to offer their solutions to all Azure Marketplace customers.</span></span> <span data-ttu-id="f781f-105">W przypadku takich rozwiązań zmniejszyć konserwacji i obsługi obciążenia dla klientów.</span><span class="sxs-lookup"><span data-stu-id="f781f-105">Such solutions reduce the maintenance and servicing overhead for customers.</span></span> <span data-ttu-id="f781f-106">Wydawcy sprzedać infrastruktury i oprogramowaniem za pośrednictwem portalu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f781f-106">Publishers can sell infrastructure and software through the Marketplace.</span></span> <span data-ttu-id="f781f-107">One dołączyć usług oraz obsługi do zarządzanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f781f-107">They can attach services and operational support to managed applications.</span></span> <span data-ttu-id="f781f-108">Aby uzyskać więcej informacji, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-108">For more information, see [Managed application overview](managed-application-overview.md).</span></span>

<span data-ttu-id="f781f-109">W tym artykule opisano, jak MSP, niezależnego dostawcy oprogramowania lub SI publikowanie aplikacji w portalu Marketplace i były szeroko dostępne dla klientów.</span><span class="sxs-lookup"><span data-stu-id="f781f-109">This article explains how an MSP, ISV, or SI can publish an application to the Marketplace and make it broadly available to customers.</span></span>

## <a name="prerequisites-for-publishing-a-managed-application"></a><span data-ttu-id="f781f-110">Wymagania wstępne dotyczące publikowania aplikacji zarządzanej</span><span class="sxs-lookup"><span data-stu-id="f781f-110">Prerequisites for publishing a managed application</span></span>

<span data-ttu-id="f781f-111">Wymagania wstępne dotyczące listy w witrynie Marketplace:</span><span class="sxs-lookup"><span data-stu-id="f781f-111">Prerequisites to listing in the Marketplace:</span></span>

* <span data-ttu-id="f781f-112">Techniczne</span><span class="sxs-lookup"><span data-stu-id="f781f-112">Technical</span></span>

    *  <span data-ttu-id="f781f-113">Aby uzyskać informacje o podstawowej struktury i składni szablonów usługi Azure Resource Manager, zobacz [szablonów usługi Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-113">For information about the basic structure and syntax of Azure Resource Manager templates, see [Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
    *  <span data-ttu-id="f781f-114">Aby wyświetlić pełny szablon rozwiązania, zobacz [szablonów Szybki Start Azure](https://azure.microsoft.com/en-us/documentation/templates/) lub [repozytorium szablonów Szybki Start](https://github.com/azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="f781f-114">To view complete template solutions, see [Azure Quickstart templates](https://azure.microsoft.com/en-us/documentation/templates/) or the [Quickstart template repository](https://github.com/azure/azure-quickstart-templates).</span></span>
    *  <span data-ttu-id="f781f-115">Informacje o sposobie tworzenia interfejsu dla klientów, którzy wdrażania aplikacji za pośrednictwem portalu Marketplace, zobacz [Utwórz plik definicji interfejsu użytkownika](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-115">For information about how to create the interface for customers who deploy your application through the Marketplace, see [Create a user interface definition file](managed-application-createuidefinition-overview.md).</span></span>

* <span data-ttu-id="f781f-116">Nietechnicznym (wymagania biznesowe)</span><span class="sxs-lookup"><span data-stu-id="f781f-116">Nontechnical (business requirements)</span></span>

    *   <span data-ttu-id="f781f-117">Firmy lub zależnemu musi znajdować się w danym kraju, w którym sprzedaży są obsługiwane przez witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f781f-117">Your company or its subsidiary must be located in a country where sales are supported by the Marketplace.</span></span>
    *   <span data-ttu-id="f781f-118">W taki sposób, który jest zgodny z rozliczeń modeli obsługiwanych przez witryny Marketplace muszą mieć licencję na produkt.</span><span class="sxs-lookup"><span data-stu-id="f781f-118">Your product must be licensed in a way that is compatible with billing models supported by the Marketplace.</span></span>
    *   <span data-ttu-id="f781f-119">Wszystko jest odpowiedzialny za udostępnienie pomocy technicznej dla klientów w sposób uzasadnione ekonomicznie.</span><span class="sxs-lookup"><span data-stu-id="f781f-119">You're responsible for making technical support available to customers in a commercially reasonable manner.</span></span> <span data-ttu-id="f781f-120">Obsługa można wolny, płatnej, lub za pośrednictwem społeczności obsługuje.</span><span class="sxs-lookup"><span data-stu-id="f781f-120">The support can be free, paid, or through community support.</span></span>
    *   <span data-ttu-id="f781f-121">Wszystko jest odpowiedzialny za Licencjonowanie oprogramowanie oraz wszystkie zależności oprogramowania innych firm.</span><span class="sxs-lookup"><span data-stu-id="f781f-121">You're responsible for licensing your software and any third-party software dependencies.</span></span>
    *   <span data-ttu-id="f781f-122">Należy podać zawartość, która spełnia kryteria dla Twojej oferty był wyświetlany w witrynie Marketplace oraz w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f781f-122">You must provide content that meets criteria for your offering to be listed in the Marketplace and in the Azure portal.</span></span>
    *   <span data-ttu-id="f781f-123">Musisz zaakceptować postanowienia Umowy o Azure Marketplace udział zasad i wydawcy.</span><span class="sxs-lookup"><span data-stu-id="f781f-123">You must agree to the terms of the Azure Marketplace Participation Policies and Publisher Agreement.</span></span>
    *   <span data-ttu-id="f781f-124">Musisz zaakceptować warunki użytkowania, zasady zachowania poufności informacji firmy Microsoft i certyfikowane umowę programu Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f781f-124">You must agree to comply with the Terms of Use, Microsoft Privacy Statement, and Microsoft Azure Certified Program Agreement.</span></span>

## <a name="create-a-new-azure-application-offer"></a><span data-ttu-id="f781f-125">Tworzenie nowej oferty aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="f781f-125">Create a new Azure application offer</span></span>

<span data-ttu-id="f781f-126">Po spełniają wymagania wstępne, możesz utworzyć ofertę zarządzanej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f781f-126">After you meet the prerequisites, you're ready to create your managed application offer.</span></span> <span data-ttu-id="f781f-127">Spójrzmy szybki przegląd oferty i jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f781f-127">Let's take a quick overview of an offer and a SKU.</span></span>

### <a name="offer"></a><span data-ttu-id="f781f-128">Oferta</span><span class="sxs-lookup"><span data-stu-id="f781f-128">Offer</span></span>

<span data-ttu-id="f781f-129">Oferta dla aplikacji zarządzanej odpowiada klasie produktu oferty od wydawcy.</span><span class="sxs-lookup"><span data-stu-id="f781f-129">The offer for a managed application corresponds to a class of product offering from a publisher.</span></span> <span data-ttu-id="f781f-130">Jeśli masz nowy typ rozwiązania/aplikacji, które mają być dostępne w witrynie Marketplace go skonfigurować, jako nowego oferty.</span><span class="sxs-lookup"><span data-stu-id="f781f-130">If you have a new type of solution/application that you want to make available in the Marketplace, you can set it up as a new offer.</span></span> <span data-ttu-id="f781f-131">Oferta jest kolekcją jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f781f-131">An offer is a collection of SKUs.</span></span> <span data-ttu-id="f781f-132">Co oferta zostanie wyświetlony jako własny element w witrynie Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f781f-132">Every offer appears as its own entity in the Marketplace.</span></span>

### <a name="sku"></a><span data-ttu-id="f781f-133">SKU</span><span class="sxs-lookup"><span data-stu-id="f781f-133">SKU</span></span>

<span data-ttu-id="f781f-134">Jednostka SKU jest najmniejszej jednostki oferowane oferty.</span><span class="sxs-lookup"><span data-stu-id="f781f-134">A SKU is the smallest purchasable unit of an offer.</span></span> <span data-ttu-id="f781f-135">SKU w tej samej klasie produktu (Oferta) umożliwia rozróżnianie między:</span><span class="sxs-lookup"><span data-stu-id="f781f-135">You can use a SKU within the same product class (offer) to differentiate between:</span></span>

* <span data-ttu-id="f781f-136">Różne funkcje, które są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f781f-136">Different features that are supported.</span></span>
* <span data-ttu-id="f781f-137">Określa, czy oferty jest zarządzane lub niezarządzane.</span><span class="sxs-lookup"><span data-stu-id="f781f-137">Whether the offer is managed or unmanaged.</span></span>
* <span data-ttu-id="f781f-138">Modele rozliczeń, które są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f781f-138">Billing models that are supported.</span></span>

<span data-ttu-id="f781f-139">Jednostka SKU jest wyświetlany w obszarze oferta nadrzędnego w witrynie Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f781f-139">A SKU appears under the parent offer in the Marketplace.</span></span> <span data-ttu-id="f781f-140">Wygląda na to jako własny element oferowane w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f781f-140">It appears as its own purchasable entity in the Azure portal.</span></span>

### <a name="set-up-an-offer"></a><span data-ttu-id="f781f-141">Konfigurowanie oferty</span><span class="sxs-lookup"><span data-stu-id="f781f-141">Set up an offer</span></span>

1. <span data-ttu-id="f781f-142">Zaloguj się do [portalu dla partnerów chmury](https://cloudpartner.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f781f-142">Sign in to the [Cloud Partner portal](https://cloudpartner.azure.com/).</span></span>

2. <span data-ttu-id="f781f-143">W okienku nawigacji po lewej stronie wybierz **+ nowe oferty** > **aplikacji Azure**.</span><span class="sxs-lookup"><span data-stu-id="f781f-143">In the navigation pane on the left, select **+ New offer** > **Azure Applications**.</span></span>

    ![Nowa oferta](./media/managed-application-author-marketplace/newOffer.png)

3. <span data-ttu-id="f781f-145">Wypełnianie formularzy, które pojawiają się po lewej stronie w **edytor** widoku.</span><span class="sxs-lookup"><span data-stu-id="f781f-145">Fill out the forms that appear on the left in the **Editor** view.</span></span> <span data-ttu-id="f781f-146">Wymagane pola są oznaczone czerwoną gwiazdką (*).</span><span class="sxs-lookup"><span data-stu-id="f781f-146">Required fields are marked with a red asterisk (*).</span></span>

    ![Ustawienia oferty](./media/managed-application-author-marketplace/newOffer_OfferSettings.png)

    <span data-ttu-id="f781f-148">Cztery główne formularze są używane do tworzenia zarządzanej aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f781f-148">Four main forms are used to create a managed application:</span></span>

    <span data-ttu-id="f781f-149">a.</span><span class="sxs-lookup"><span data-stu-id="f781f-149">a.</span></span> <span data-ttu-id="f781f-150">Ustawienia oferty</span><span class="sxs-lookup"><span data-stu-id="f781f-150">Offer Settings</span></span>

    <span data-ttu-id="f781f-151">b.</span><span class="sxs-lookup"><span data-stu-id="f781f-151">b.</span></span> <span data-ttu-id="f781f-152">Jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="f781f-152">SKUs</span></span>

    <span data-ttu-id="f781f-153">c.</span><span class="sxs-lookup"><span data-stu-id="f781f-153">c.</span></span> <span data-ttu-id="f781f-154">Portal Marketplace</span><span class="sxs-lookup"><span data-stu-id="f781f-154">Marketplace</span></span>

    <span data-ttu-id="f781f-155">d.</span><span class="sxs-lookup"><span data-stu-id="f781f-155">d.</span></span> <span data-ttu-id="f781f-156">Pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="f781f-156">Support</span></span>

<span data-ttu-id="f781f-157">Formularze są opisane bardziej szczegółowo w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="f781f-157">These forms are described in greater detail in the following sections.</span></span>

## <a name="offer-settings-form"></a><span data-ttu-id="f781f-158">Formularz Ustawienia oferty</span><span class="sxs-lookup"><span data-stu-id="f781f-158">Offer Settings form</span></span>
<span data-ttu-id="f781f-159">Ten formularz podstawowy do określenia ustawień oferty.</span><span class="sxs-lookup"><span data-stu-id="f781f-159">Use this basic form to specify the offer settings.</span></span>

1. <span data-ttu-id="f781f-160">Wypełnij **oferują ustawienia** formularza.</span><span class="sxs-lookup"><span data-stu-id="f781f-160">Fill in the **Offer Settings** form.</span></span> <span data-ttu-id="f781f-161">Różne pola to:</span><span class="sxs-lookup"><span data-stu-id="f781f-161">The different fields are:</span></span>

    <span data-ttu-id="f781f-162">a.</span><span class="sxs-lookup"><span data-stu-id="f781f-162">a.</span></span> <span data-ttu-id="f781f-163">**Identyfikator oferty**: ten unikatowy identyfikator identyfikuje oferta w profilu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="f781f-163">**Offer ID**: This unique identifier identifies the offer within a publisher profile.</span></span> <span data-ttu-id="f781f-164">Ten identyfikator jest widoczny w adresach URL produktu, szablony usługi Resource Manager i raporty rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="f781f-164">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="f781f-165">Go mogą się składać tylko małe znaki alfanumeryczne i łączniki (-).</span><span class="sxs-lookup"><span data-stu-id="f781f-165">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="f781f-166">Identyfikator nie może kończyć się łącznikiem.</span><span class="sxs-lookup"><span data-stu-id="f781f-166">The ID can't end in a dash.</span></span> <span data-ttu-id="f781f-167">Jego ograniczone do maksymalnie 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="f781f-167">It's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="f781f-168">Po ofertę odbywa się na żywo, to pole jest zablokowane.</span><span class="sxs-lookup"><span data-stu-id="f781f-168">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="f781f-169">b.</span><span class="sxs-lookup"><span data-stu-id="f781f-169">b.</span></span> <span data-ttu-id="f781f-170">**Identyfikator wydawcy**: Użyj tej listy rozwijanej, aby wybrać profil wydawcy, którą chcesz opublikować tej oferty, w obszarze.</span><span class="sxs-lookup"><span data-stu-id="f781f-170">**Publisher ID**: Use this drop-down list to choose the publisher profile you want to publish this offer under.</span></span> <span data-ttu-id="f781f-171">Po ofertę odbywa się na żywo, to pole jest zablokowane.</span><span class="sxs-lookup"><span data-stu-id="f781f-171">After an offer goes live, this field is locked.</span></span>

    <span data-ttu-id="f781f-172">c.</span><span class="sxs-lookup"><span data-stu-id="f781f-172">c.</span></span> <span data-ttu-id="f781f-173">**Nazwa**: Ta nazwa wyświetlana dla danej oferty pojawia się w witrynie Marketplace oraz w portalu.</span><span class="sxs-lookup"><span data-stu-id="f781f-173">**Name**: This display name for your offer appears in the Marketplace and in the portal.</span></span> <span data-ttu-id="f781f-174">Może mieć maksymalnie 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="f781f-174">It can have a maximum of 50 characters.</span></span> <span data-ttu-id="f781f-175">Obejmują rozpoznawalną nazwę markę produktu.</span><span class="sxs-lookup"><span data-stu-id="f781f-175">Include a recognizable brand name for your product.</span></span> <span data-ttu-id="f781f-176">Nie zawierają nazwę swojej firmy, chyba że jest sposób jest ona sprzedawane.</span><span class="sxs-lookup"><span data-stu-id="f781f-176">Don't include your company name here unless that's how it's marketed.</span></span> <span data-ttu-id="f781f-177">Ta oferta jest marketingu na własne witryny sieci Web, upewnij się, że nazwa jest dokładnie sposobu jej wyświetlania w witrynie sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f781f-177">If you're marketing this offer on your own website, ensure that the name is exactly how it appears on your website.</span></span>

2. <span data-ttu-id="f781f-178">Wybierz **zapisać** Aby zapisać postęp.</span><span class="sxs-lookup"><span data-stu-id="f781f-178">Select **Save** to save your progress.</span></span> 

## <a name="skus-form"></a><span data-ttu-id="f781f-179">Formularz jednostki SKU</span><span class="sxs-lookup"><span data-stu-id="f781f-179">SKUs form</span></span>
<span data-ttu-id="f781f-180">Następnym krokiem jest można dodać jednostki SKU dla danej oferty.</span><span class="sxs-lookup"><span data-stu-id="f781f-180">The next step is to add SKUs for your offer.</span></span>

1. <span data-ttu-id="f781f-181">Wybierz **jednostki SKU** > **nowe jednostki SKU**.</span><span class="sxs-lookup"><span data-stu-id="f781f-181">Select **SKUs** > **New SKU**.</span></span> 

    ![Wybierz nowe jednostki SKU](./media/managed-application-author-marketplace/newOffer_skus.png)

2. <span data-ttu-id="f781f-183">Wprowadź **identyfikator jednostki SKU**.</span><span class="sxs-lookup"><span data-stu-id="f781f-183">Enter a **SKU ID**.</span></span> <span data-ttu-id="f781f-184">Identyfikator jednostki SKU to unikatowy identyfikator dla jednostki SKU oferta.</span><span class="sxs-lookup"><span data-stu-id="f781f-184">A SKU ID is a unique identifier for the SKU within an offer.</span></span> <span data-ttu-id="f781f-185">Ten identyfikator jest widoczny w adresach URL produktu, szablony usługi Resource Manager i raporty rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="f781f-185">This ID is visible in product URLs, Resource Manager templates, and billing reports.</span></span> <span data-ttu-id="f781f-186">Go mogą się składać tylko małe znaki alfanumeryczne i łączniki (-).</span><span class="sxs-lookup"><span data-stu-id="f781f-186">It can only be composed of lowercase alphanumeric characters or dashes (-).</span></span> <span data-ttu-id="f781f-187">Identyfikator nie może kończyć się kreską i ograniczone do maksymalnie 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="f781f-187">The ID can't end in a dash, and it's limited to a maximum of 50 characters.</span></span> <span data-ttu-id="f781f-188">Po ofertę odbywa się na żywo, to pole jest zablokowane.</span><span class="sxs-lookup"><span data-stu-id="f781f-188">After an offer goes live, this field is locked.</span></span> <span data-ttu-id="f781f-189">Może mieć wiele jednostek SKU oferta.</span><span class="sxs-lookup"><span data-stu-id="f781f-189">You can have multiple SKUs within an offer.</span></span> <span data-ttu-id="f781f-190">Należy jednostki SKU dla każdego obrazu, który chcesz opublikować.</span><span class="sxs-lookup"><span data-stu-id="f781f-190">You need a SKU for each image you plan to publish.</span></span>

3. <span data-ttu-id="f781f-191">Wypełnianie **szczegóły jednostki SKU** sekcji w następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="f781f-191">Fill out the **SKU Details** section on the following form:</span></span>

    ![Podaj nowe jednostki SKU](./media/managed-application-author-marketplace/newOffer_newsku.png)

    <span data-ttu-id="f781f-193">Wypełnij następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f781f-193">Fill out the following fields:</span></span>
    
    <span data-ttu-id="f781f-194">a.</span><span class="sxs-lookup"><span data-stu-id="f781f-194">a.</span></span> <span data-ttu-id="f781f-195">**Tytuł**: Podaj tytuł tej jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f781f-195">**Title**: Enter a title for this SKU.</span></span> <span data-ttu-id="f781f-196">Ten tytuł pojawi się w galerii dla tego elementu.</span><span class="sxs-lookup"><span data-stu-id="f781f-196">This title appears in the gallery for this item.</span></span>

    <span data-ttu-id="f781f-197">b.</span><span class="sxs-lookup"><span data-stu-id="f781f-197">b.</span></span> <span data-ttu-id="f781f-198">**Podsumowanie**: Podaj krótkie podsumowanie dla tej wersji produktu.</span><span class="sxs-lookup"><span data-stu-id="f781f-198">**Summary**: Enter a short summary for this SKU.</span></span> <span data-ttu-id="f781f-199">Ten tekst jest wyświetlany pod tytułem.</span><span class="sxs-lookup"><span data-stu-id="f781f-199">This text appears underneath the title.</span></span>

    <span data-ttu-id="f781f-200">c.</span><span class="sxs-lookup"><span data-stu-id="f781f-200">c.</span></span> <span data-ttu-id="f781f-201">**Opis elementu**: Podaj szczegółowy opis jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f781f-201">**Description**: Enter a detailed description about the SKU.</span></span>

    <span data-ttu-id="f781f-202">d.</span><span class="sxs-lookup"><span data-stu-id="f781f-202">d.</span></span> <span data-ttu-id="f781f-203">**Typ jednostki SKU**: dozwolone wartości **zarządzanej aplikacji** i **szablony rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="f781f-203">**SKU Type**: The allowed values are **Managed Application** and **Solution Templates**.</span></span> <span data-ttu-id="f781f-204">W tym przypadku wybierz **zarządzanej aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="f781f-204">For this case, select **Managed Application**.</span></span>

4. <span data-ttu-id="f781f-205">Wypełnianie **informacje szczegółowe dotyczące pakietu** sekcji w następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="f781f-205">Fill out the **Package Details** section on the following form:</span></span>

    ![Pakiet](./media/managed-application-author-marketplace/newOffer_newsku_package.png)

    <span data-ttu-id="f781f-207">Wypełnij następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f781f-207">Fill out the following fields:</span></span>

    <span data-ttu-id="f781f-208">a.</span><span class="sxs-lookup"><span data-stu-id="f781f-208">a.</span></span> <span data-ttu-id="f781f-209">**Bieżąca wersja**: wprowadź wersję pakietu przekazywania.</span><span class="sxs-lookup"><span data-stu-id="f781f-209">**Current Version**: Enter a version for the package you upload.</span></span> <span data-ttu-id="f781f-210">Powinna być w formacie `{number}.{number}.{number}{number}`.</span><span class="sxs-lookup"><span data-stu-id="f781f-210">It should be in the format `{number}.{number}.{number}{number}`.</span></span>

    <span data-ttu-id="f781f-211">b.</span><span class="sxs-lookup"><span data-stu-id="f781f-211">b.</span></span> <span data-ttu-id="f781f-212">**Wybierz plik pakietu**: ten pakiet zawiera następujące pliki skompresowane do pliku zip:</span><span class="sxs-lookup"><span data-stu-id="f781f-212">**Select a package file**: This package contains the following files that are compressed into a .zip file:</span></span>
    * <span data-ttu-id="f781f-213">**applianceMainTemplate.json**: plik szablonu wdrożenia, który służy do wdrażania rozwiązania/aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f781f-213">**applianceMainTemplate.json**: The deployment template file that's used to deploy the solution/application.</span></span> <span data-ttu-id="f781f-214">Aby uzyskać informacje o sposobach tworzenia wdrożenia pliki szablonów, zobacz [Tworzenie pierwszego szablonu usługi Azure Resource Manager](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-214">For information about how to create deployment template files, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
    * <span data-ttu-id="f781f-215">**appliancecreateUIDefinition.json**: ten plik jest używany w portalu Azure, aby wygenerować interfejs użytkownika, który jest używany do udostępniania tego rozwiązania/aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f781f-215">**appliancecreateUIDefinition.json**: This file is used by the Azure portal to generate the user interface that's used to provision this solution/application.</span></span> <span data-ttu-id="f781f-216">Aby uzyskać więcej informacji, zobacz [wprowadzenie CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-216">For more information, see [Get started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
    * <span data-ttu-id="f781f-217">**mainTemplate.json**: ten plik szablonu zawiera tylko zasobu Microsoft.Solution/appliances.</span><span class="sxs-lookup"><span data-stu-id="f781f-217">**mainTemplate.json**: This template file contains only the Microsoft.Solution/appliances resource.</span></span> <span data-ttu-id="f781f-218">Plik mainTemplate zawiera następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="f781f-218">The mainTemplate file includes the following properties:</span></span>

        *  <span data-ttu-id="f781f-219">**rodzaj**: Użyj **Marketplace** zarządzanych aplikacji w witrynie Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f781f-219">**kind**: Use **Marketplace** for managed applications in the Marketplace.</span></span>
        *  <span data-ttu-id="f781f-220">**ManagedResourceGroupId**: jest to grupa zasobów w subskrypcji klienta wdrożonym wszystkie zasoby zdefiniowane w applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="f781f-220">**ManagedResourceGroupId**: This resource group in the customer's subscription is where all the resources defined in applianceMainTemplate.json are deployed.</span></span>
        *  <span data-ttu-id="f781f-221">**PublisherPackageId**: ten ciąg unikatowo identyfikujący pakietu.</span><span class="sxs-lookup"><span data-stu-id="f781f-221">**PublisherPackageId**: This string uniquely identifies the package.</span></span> <span data-ttu-id="f781f-222">Podaj wartość w formacie `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span><span class="sxs-lookup"><span data-stu-id="f781f-222">Provide the value in the format of `{publisherId}.{OfferId}.{SKUID}.{PackageVersion}`.</span></span>

<span data-ttu-id="f781f-223">Uzyskaj **identyfikator oferty** i **identyfikator wydawcy** z portalu publikowania, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="f781f-223">Obtain the **Offer ID** and **Publisher ID** from the publishing portal, as shown in the following image:</span></span>

![Identyfikator oferty](./media/managed-application-author-marketplace/UniqueString_pubid_offerid.png)
        
<span data-ttu-id="f781f-225">Uzyskaj **identyfikator jednostki SKU**, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="f781f-225">Obtain the **SKU ID**, as shown in the following image:</span></span>

![IDENTYFIKATOR JEDNOSTKI SKU](./media/managed-application-author-marketplace/UniqueString_skuid.png)
        
<span data-ttu-id="f781f-227">Uzyskiwanie pakietu **wersji**, jak pokazano na poniższej ilustracji:</span><span class="sxs-lookup"><span data-stu-id="f781f-227">Obtain the package **Version**, as shown in the following image:</span></span>

![Wersja pakietu](./media/managed-application-author-marketplace/UniqueString_packageversion.png)
    
  <span data-ttu-id="f781f-229">W poprzednich przykładach, wartość w oparciu **PublisherPackageId** jest `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="f781f-229">Based on the preceding examples, the value of **PublisherPackageId** is `azureappliance-test.ravmanagedapptest.ravpreviewmanagedsku.1.0.0`.</span></span>

  <span data-ttu-id="f781f-230">Przykładowe mainTemplate.json:</span><span class="sxs-lookup"><span data-stu-id="f781f-230">Sample mainTemplate.json:</span></span>

  ```json
  {
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
      "storageAccountNamePrefix": {
        "type": "string",
        "metadata": {
          "description": "Specify the name of the storage account"
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

<span data-ttu-id="f781f-231">Ten pakiet powinien zawierać wszystkie zagnieżdżone szablony lub skryptów, które są wymagane do udostępnienia pomyślnie tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f781f-231">This package should contain any other nested templates or scripts that are required to successfully provision this application.</span></span> <span data-ttu-id="f781f-232">MainTemplate.json, applianceMainTemplate.json i applianceCreateUIDefinition.json pliki muszą być obecne w folderze głównym.</span><span class="sxs-lookup"><span data-stu-id="f781f-232">The mainTemplate.json, applianceMainTemplate.json, and applianceCreateUIDefinition.json files must be present at the root folder.</span></span>

* <span data-ttu-id="f781f-233">**Autoryzacje**: Ta właściwość określa, kto dostępu i poziom dostępu do zasobów w subskrypcji klientów.</span><span class="sxs-lookup"><span data-stu-id="f781f-233">**Authorizations**: This property defines who gets access and the level of access to the resources in customers' subscriptions.</span></span> <span data-ttu-id="f781f-234">Wydawca służy do zarządzania aplikacją w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="f781f-234">The publisher can use it to manage the application on behalf of the customer.</span></span>
* <span data-ttu-id="f781f-235">**PrincipalId**: Ta właściwość jest identyfikator użytkownika, grupy użytkowników lub aplikacji, która ma pewne uprawnienia do zasobów w subskrypcji klienta usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f781f-235">**PrincipalId**: This property is the Azure Active Directory (Azure AD) identifier of a user, user group, or application that's granted certain permissions on the resources in the customer's subscription.</span></span> <span data-ttu-id="f781f-236">Definicja roli Opisuje uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="f781f-236">The Role Definition describes the permissions.</span></span> 
* <span data-ttu-id="f781f-237">**Definicja roli**: Ta właściwość jest lista wszystkich kontroli dostępu opartej na rolach (RBAC) role wbudowane dostarczane przez usługę Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f781f-237">**Role Definition**: This property is a list of all the built-in Role-Based Access Control (RBAC) roles provided by Azure AD.</span></span> <span data-ttu-id="f781f-238">Możesz wybrać rolę, która jest najbardziej odpowiednia na potrzeby zarządzania zasobami w imieniu klienta.</span><span class="sxs-lookup"><span data-stu-id="f781f-238">You can select the role that's most appropriate to use to manage the resources on behalf of the customer.</span></span>

<span data-ttu-id="f781f-239">Można dodać wiele zezwolenia.</span><span class="sxs-lookup"><span data-stu-id="f781f-239">You can add multiple authorizations.</span></span> <span data-ttu-id="f781f-240">Zaleca się utworzenie grupy użytkowników usługi AD i określić jej identyfikator w **PrincipalId**.</span><span class="sxs-lookup"><span data-stu-id="f781f-240">We recommend that you create an AD user group and specify its ID in **PrincipalId**.</span></span> <span data-ttu-id="f781f-241">W ten sposób można dodać więcej użytkowników do grupy użytkowników, bez konieczności aktualizacji jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f781f-241">This way, you can add more users to the user group without the need to update the SKU.</span></span>

<span data-ttu-id="f781f-242">Aby uzyskać więcej informacji o RBAC, zobacz [wprowadzenie RBAC w portalu Azure](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-242">For more information about RBAC, see [Get started with RBAC in the Azure portal](../active-directory/role-based-access-control-what-is.md).</span></span>

## <a name="marketplace-form"></a><span data-ttu-id="f781f-243">Formularz Marketplace</span><span class="sxs-lookup"><span data-stu-id="f781f-243">Marketplace form</span></span>

<span data-ttu-id="f781f-244">Formularz Marketplace wprowadza się pola, które są widoczne na [portalu Azure Marketplace](https://azuremarketplace.microsoft.com) i na [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f781f-244">The Marketplace form asks for fields that show up on the [Azure Marketplace](https://azuremarketplace.microsoft.com) and on the [Azure portal](https://portal.azure.com/).</span></span>

### <a name="preview-subscription-ids"></a><span data-ttu-id="f781f-245">Identyfikatory subskrypcji w wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="f781f-245">Preview subscription IDs</span></span>

<span data-ttu-id="f781f-246">Wprowadź listę identyfikatorów, które mogą uzyskać dostęp do oferty po opublikowaniu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f781f-246">Enter a list of Azure subscription IDs that can access the offer after it's published.</span></span> <span data-ttu-id="f781f-247">Te subskrypcje wymienione biały można użyć do testowania przeglądanego oferty, przed wprowadzeniem go na żywo.</span><span class="sxs-lookup"><span data-stu-id="f781f-247">You can use these white-listed subscriptions to test the previewed offer before you make it live.</span></span> <span data-ttu-id="f781f-248">Można kompilować białą listę maksymalnie 100 subskrypcji w portalu dla partnerów.</span><span class="sxs-lookup"><span data-stu-id="f781f-248">You can compile a white list of up to 100 subscriptions in the partner portal.</span></span>

### <a name="suggested-categories"></a><span data-ttu-id="f781f-249">Kategorii sugerowanych</span><span class="sxs-lookup"><span data-stu-id="f781f-249">Suggested categories</span></span>

<span data-ttu-id="f781f-250">Wybierz kategorie do pięciu z Twoją ofertę może być najlepiej skojarzony z listy.</span><span class="sxs-lookup"><span data-stu-id="f781f-250">Select up to five categories from the list that your offer can be best associated with.</span></span> <span data-ttu-id="f781f-251">Te kategorie są używane do mapowania kategorie produktów, które są dostępne w Twojej oferty [portalu Azure Marketplace](https://azuremarketplace.microsoft.com) i [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f781f-251">These categories are used to map your offer to the product categories that are available in the [Azure Marketplace](https://azuremarketplace.microsoft.com) and the [Azure portal](https://portal.azure.com/).</span></span>

#### <a name="azure-marketplace"></a><span data-ttu-id="f781f-252">Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="f781f-252">Azure Marketplace</span></span>

<span data-ttu-id="f781f-253">Podsumowanie aplikacji zarządzanej wyświetla następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f781f-253">The summary of your managed application displays the following fields:</span></span>

![Podsumowanie witryny Marketplace](./media/managed-application-author-marketplace/publishvm10.png)

<span data-ttu-id="f781f-255">**Omówienie** karcie dla aplikacji zarządzanej wyświetla następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f781f-255">The **Overview** tab for your managed application displays the following fields:</span></span>

![Omówienie portalu Marketplace](./media/managed-application-author-marketplace/publishvm11.png)

<span data-ttu-id="f781f-257">**Planów + cennik** karcie dla aplikacji zarządzanej wyświetla następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f781f-257">The **Plans + Pricing** tab for your managed application displays the following fields:</span></span>

![Plany Marketplace](./media/managed-application-author-marketplace/publishvm15.png)

#### <a name="azure-portal"></a><span data-ttu-id="f781f-259">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f781f-259">Azure portal</span></span>

<span data-ttu-id="f781f-260">Podsumowanie aplikacji zarządzanej wyświetla następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f781f-260">The summary of your managed application displays the following fields:</span></span>

![Portal podsumowania](./media/managed-application-author-marketplace/publishvm12.png)

<span data-ttu-id="f781f-262">Omówienie aplikacji zarządzanej wyświetla następujące pola:</span><span class="sxs-lookup"><span data-stu-id="f781f-262">The overview for your managed application displays the following fields:</span></span>

![Przegląd portalu](./media/managed-application-author-marketplace/publishvm13.png)

#### <a name="logo-guidelines"></a><span data-ttu-id="f781f-264">Wytycznych dotyczących logo</span><span class="sxs-lookup"><span data-stu-id="f781f-264">Logo guidelines</span></span>

<span data-ttu-id="f781f-265">Skorzystaj z następujących wskazówek dla dowolnego logo, które można przekazać w portalu dla partnerów chmury:</span><span class="sxs-lookup"><span data-stu-id="f781f-265">Follow these guidelines for any logo that you upload in the Cloud Partner portal:</span></span>

*   <span data-ttu-id="f781f-266">Projekt platformy Azure ma paletę kolorów proste.</span><span class="sxs-lookup"><span data-stu-id="f781f-266">The Azure design has a simple color palette.</span></span> <span data-ttu-id="f781f-267">Ogranicz liczbę podstawowy i pomocniczy kolorów w logo.</span><span class="sxs-lookup"><span data-stu-id="f781f-267">Limit the number of primary and secondary colors on your logo.</span></span>
*   <span data-ttu-id="f781f-268">Kolorów motywu portalu są białe i czarne.</span><span class="sxs-lookup"><span data-stu-id="f781f-268">The theme colors of the portal are white and black.</span></span> <span data-ttu-id="f781f-269">Nie używaj kolorów te jako kolor tła dla logo.</span><span class="sxs-lookup"><span data-stu-id="f781f-269">Don't use these colors as the background color for your logo.</span></span> <span data-ttu-id="f781f-270">Użyj kolor, który sprawia, że logo jest widoczne w portalu.</span><span class="sxs-lookup"><span data-stu-id="f781f-270">Use a color that makes your logo prominent in the portal.</span></span> <span data-ttu-id="f781f-271">Zaleca się proste kolorów podstawowych.</span><span class="sxs-lookup"><span data-stu-id="f781f-271">We recommend simple primary colors.</span></span> <span data-ttu-id="f781f-272">*Jeśli używasz przezroczyste tło, upewnij się, logo i tekst są białe, czarne lub niebieski.*</span><span class="sxs-lookup"><span data-stu-id="f781f-272">*If you use a transparent background, make sure that the logo and text aren't white, black, or blue.*</span></span>
*   <span data-ttu-id="f781f-273">Nie używaj gradientu tła na logo.</span><span class="sxs-lookup"><span data-stu-id="f781f-273">Don't use a gradient background on the logo.</span></span>
*   <span data-ttu-id="f781f-274">Nie należy umieszczać na logo, nawet Twoja firma lub marką tekstu.</span><span class="sxs-lookup"><span data-stu-id="f781f-274">Don't place text on the logo, not even your company or brand name.</span></span> <span data-ttu-id="f781f-275">Wygląd i działanie logo powinny być płaski i uniknąć gradienty.</span><span class="sxs-lookup"><span data-stu-id="f781f-275">The look and feel of your logo should be flat and avoid gradients.</span></span>
*   <span data-ttu-id="f781f-276">Upewnij się, że nie jest rozciągana logo.</span><span class="sxs-lookup"><span data-stu-id="f781f-276">Make sure the logo isn't stretched.</span></span>

#### <a name="hero-logo"></a><span data-ttu-id="f781f-277">Logo bohater</span><span class="sxs-lookup"><span data-stu-id="f781f-277">Hero logo</span></span>

<span data-ttu-id="f781f-278">Logo bohater jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="f781f-278">The hero logo is optional.</span></span> <span data-ttu-id="f781f-279">Wydawcy można zrezygnować z przekazać logo bohater.</span><span class="sxs-lookup"><span data-stu-id="f781f-279">The publisher can choose not to upload a hero logo.</span></span> <span data-ttu-id="f781f-280">Po przekazaniu ikona bohater nie można usunąć.</span><span class="sxs-lookup"><span data-stu-id="f781f-280">After the hero icon is uploaded, it can't be deleted.</span></span> <span data-ttu-id="f781f-281">W tym czasie partnera musi postępuj zgodnie z wytycznymi Marketplace, bohater ikon.</span><span class="sxs-lookup"><span data-stu-id="f781f-281">At that time, the partner must follow the Marketplace guidelines for hero icons.</span></span>

<span data-ttu-id="f781f-282">Skorzystaj z następujących wskazówek bohater ikony logo:</span><span class="sxs-lookup"><span data-stu-id="f781f-282">Follow these guidelines for the hero logo icon:</span></span>

*   <span data-ttu-id="f781f-283">Nazwa wyświetlana wydawca, tytuł planu i długie Podsumowanie oferty są wyświetlane w biały.</span><span class="sxs-lookup"><span data-stu-id="f781f-283">The publisher display name, the plan title, and the offer long summary are displayed in white.</span></span> <span data-ttu-id="f781f-284">W związku z tym nie należy używać jasny kolor tła ikon bohater.</span><span class="sxs-lookup"><span data-stu-id="f781f-284">Therefore, don't use a light color for the background of the hero icon.</span></span> <span data-ttu-id="f781f-285">Czarne, białe lub przezroczyste tło nie jest dozwolona dla bohater ikon.</span><span class="sxs-lookup"><span data-stu-id="f781f-285">A black, white, or transparent background isn't allowed for hero icons.</span></span>
*   <span data-ttu-id="f781f-286">Po oferty jest wyświetlana, wydawcy Nazwa wyświetlana, tytuł planu, długie Podsumowanie oferty i **Utwórz** przycisk programowo osadzone wewnątrz bohater logo.</span><span class="sxs-lookup"><span data-stu-id="f781f-286">After the offer is listed, the publisher display name, the plan title, the offer long summary, and the **Create** button are embedded programmatically inside the hero logo.</span></span> <span data-ttu-id="f781f-287">W rezultacie nie wprowadź tekst, podczas projektowania logo bohater.</span><span class="sxs-lookup"><span data-stu-id="f781f-287">Consequently, don't enter any text while you design the hero logo.</span></span> <span data-ttu-id="f781f-288">Pozostaw puste miejsce po prawej stronie, ponieważ tekst stanowi programowo, w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="f781f-288">Leave empty space on the right because the text is included programmatically in that space.</span></span> <span data-ttu-id="f781f-289">Puste miejsce na tekst powinien być 415 x 100 pikseli po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="f781f-289">The empty space for the text should be 415 x 100 pixels on the right.</span></span> <span data-ttu-id="f781f-290">Jest on przesunięcia 370 pikseli z lewej strony.</span><span class="sxs-lookup"><span data-stu-id="f781f-290">It's offset by 370 pixels from the left.</span></span>

    ![Przykład logo bohater](./media/managed-application-author-marketplace/publishvm14.png)

## <a name="support-form"></a><span data-ttu-id="f781f-292">Obsługa formularza</span><span class="sxs-lookup"><span data-stu-id="f781f-292">Support form</span></span>

<span data-ttu-id="f781f-293">Wypełnianie **obsługuje** formularza z obsługą kontaktuje się z Twojej firmy.</span><span class="sxs-lookup"><span data-stu-id="f781f-293">Fill out the **Support** form with support contacts from your company.</span></span> <span data-ttu-id="f781f-294">Te informacje mogą inżynierii, kontaktów i kontaktów pomocy technicznej klienta.</span><span class="sxs-lookup"><span data-stu-id="f781f-294">This information might be engineering contacts and customer support contacts.</span></span>

## <a name="publish-an-offer"></a><span data-ttu-id="f781f-295">Publikowanie oferty</span><span class="sxs-lookup"><span data-stu-id="f781f-295">Publish an offer</span></span>

<span data-ttu-id="f781f-296">Po wypełnieniu wszystkie sekcje wybierz **publikowania** można uruchomić procesu, który udostępnia klientom ofertę.</span><span class="sxs-lookup"><span data-stu-id="f781f-296">After you fill out all the sections, select **Publish** to start the process that makes your offer available to customers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f781f-297">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f781f-297">Next steps</span></span>

* <span data-ttu-id="f781f-298">Aby obejrzeć wprowadzenie do aplikacji zarządzanych, zobacz [Omówienie aplikacji zarządzanych](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-298">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="f781f-299">Aby dowiedzieć się, jak korzystanie z zarządzanych aplikacji z portalu Marketplace, zobacz [korzystać z platformy Azure zarządzanych aplikacji w witrynie Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-299">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
* <span data-ttu-id="f781f-300">Aby dowiedzieć się, jak publikowanie aplikacji zarządzanych katalogu usług, zobacz [Utwórz i publikowanie aplikacji katalogu usług zarządzanych](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-300">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="f781f-301">Aby dowiedzieć się, jak korzystanie z aplikacji zarządzanych katalogu usług, zobacz [korzystać z aplikacji zarządzanych katalogu usług](managed-application-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="f781f-301">For information about consuming a Service Catalog managed application, see [Consume a Service Catalog managed application](managed-application-consumption.md).</span></span>
