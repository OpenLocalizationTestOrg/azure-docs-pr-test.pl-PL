---
title: "zachowanie aaaOverride HTTP przy użyciu aparatu reguł hello Azure CDN | Dokumentacja firmy Microsoft"
description: "aparat reguł Hello umożliwia toocustomize sposób obsługi żądań HTTP przez usługi Azure CDN, takich jak blokowanie hello dostarczania niektórych typów zawartości, definiowania zasad buforowania i modyfikować nagłówki HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="4d71c-103">Zastąpienie zachowania HTTP przy użyciu aparatu reguł hello Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4d71c-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="4d71c-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="4d71c-104">Overview</span></span>
<span data-ttu-id="4d71c-105">aparat reguł Hello umożliwia toocustomize sposób obsługi żądań HTTP, takich jak blokowanie hello dostarczania niektórych typów zawartości, definiowania zasad buforowania i modyfikowanie nagłówków HTTP.</span><span class="sxs-lookup"><span data-stu-id="4d71c-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="4d71c-106">W tym samouczku zostanie pokazują, że tworzenia reguły, która zmieni hello buforowanie zasobów w sieci CDN.</span><span class="sxs-lookup"><span data-stu-id="4d71c-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="4d71c-107">Również jest dostępna w hello zawartości wideo "[Zobacz też](#see-also)" sekcji.</span><span class="sxs-lookup"><span data-stu-id="4d71c-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="4d71c-108">Odwołanie składni toohello szczegółowo, zobacz [odwołanie do aparatu reguł](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="4d71c-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="4d71c-109">Samouczek</span><span class="sxs-lookup"><span data-stu-id="4d71c-109">Tutorial</span></span>
1. <span data-ttu-id="4d71c-110">Blok profilu CDN hello, kliknij hello **Zarządzaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4d71c-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![Przycisk Zarządzaj blok profilu CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="4d71c-112">Otwiera portalu zarządzania Hello CDN.</span><span class="sxs-lookup"><span data-stu-id="4d71c-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="4d71c-113">Polecenie hello **HTTP dużych** kartę, a następnie **aparatu reguł**.</span><span class="sxs-lookup"><span data-stu-id="4d71c-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="4d71c-114">Opcje dla nowej reguły są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="4d71c-114">Options for a new rule are displayed.</span></span>
   
    ![Nowe opcje reguły CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="4d71c-116">kolejność Hello, w którym są wyświetlane wiele reguł ma wpływ na sposób obsługi.</span><span class="sxs-lookup"><span data-stu-id="4d71c-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="4d71c-117">Kolejne reguły mogą zastąpić akcje hello określone przez poprzednie reguły.</span><span class="sxs-lookup"><span data-stu-id="4d71c-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="4d71c-118">Wprowadź nazwę w hello **nazwę / opis** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="4d71c-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="4d71c-119">Określ typ hello żądań, które hello reguła będzie dotyczyć.</span><span class="sxs-lookup"><span data-stu-id="4d71c-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="4d71c-120">Domyślnie program hello **zawsze** wybrano warunek dopasowania.</span><span class="sxs-lookup"><span data-stu-id="4d71c-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="4d71c-121">Użyjesz **zawsze** w tym samouczku, dlatego pozostaw wybrany.</span><span class="sxs-lookup"><span data-stu-id="4d71c-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Warunek dopasowania CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="4d71c-123">Istnieje wiele typów dopasowania dostępne w listy rozwijanej hello warunki.</span><span class="sxs-lookup"><span data-stu-id="4d71c-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="4d71c-124">Kliknięcie toohello informacyjną ikona hello niebieski lewej warunku dopasowania hello objaśnia hello aktualnie wybrany warunek szczegółowo.</span><span class="sxs-lookup"><span data-stu-id="4d71c-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="4d71c-125">Witaj pełną listę wyrażeń warunkowych szczegółowo, zobacz [wyrażenia warunkowe aparatu reguł](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="4d71c-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="4d71c-126">Witaj pełną listę warunków dopasowania szczegółowo, zobacz [warunki odpowiada aparatu reguł](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="4d71c-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="4d71c-127">Kliknij przycisk hello  **+**  obok przycisku zbyt**funkcje** tooadd nowej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4d71c-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="4d71c-128">Z listy rozwijanej hello powitania po lewej stronie, wybierz **życie wewnętrzny Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="4d71c-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="4d71c-129">W polu tekstowym hello, która jest wyświetlana, wprowadź **300**.</span><span class="sxs-lookup"><span data-stu-id="4d71c-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="4d71c-130">Pozostaw hello pozostałe wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="4d71c-130">Leave hello remaining default values.</span></span>
   
   ![Funkcja CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="4d71c-132">Zgodnie z warunkami dopasowania, klikając toohello informacyjną ikona hello blue lewej strony hello nowe funkcji wyświetli szczegółowe informacje na temat tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4d71c-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="4d71c-133">W przypadku hello **życie wewnętrzny Max-Age**, możemy są zastępowanie zasobów hello **Cache-Control** i **Expires** toocontrol nagłówków, gdy węzeł brzegowy CDN hello odświeży hello zasobów z hello źródła.</span><span class="sxs-lookup"><span data-stu-id="4d71c-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="4d71c-134">Naszym przykładzie 300 sekund oznacza, że węzeł brzegowy CDN hello będą buforowane hello zasobów przez 5 minut przed odświeżeniem zawartości hello ze swoją witryną źródłową.</span><span class="sxs-lookup"><span data-stu-id="4d71c-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="4d71c-135">Witaj pełną listę funkcji, które szczegółowo, zobacz [Szczegóły funkcji aparatu reguł](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="4d71c-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="4d71c-136">Kliknij przycisk hello **Dodaj** przycisk toosave hello nowej reguły.</span><span class="sxs-lookup"><span data-stu-id="4d71c-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="4d71c-137">Nowa reguła Hello teraz oczekuje na zatwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="4d71c-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="4d71c-138">Po jej zatwierdzeniu hello stan zmieni się z **oczekujące XML** za**Active XML**.</span><span class="sxs-lookup"><span data-stu-id="4d71c-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4d71c-139">Zmiany zasad może trwać too90 toopropagate minut za pośrednictwem hello CDN.</span><span class="sxs-lookup"><span data-stu-id="4d71c-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="4d71c-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4d71c-140">See also</span></span>
* [<span data-ttu-id="4d71c-141">Omówienie usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4d71c-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="4d71c-142">Odwołanie do aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="4d71c-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="4d71c-143">Warunki uzgadniania aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="4d71c-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="4d71c-144">Wyrażenia warunkowe aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="4d71c-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="4d71c-145">Funkcje aparatu reguł</span><span class="sxs-lookup"><span data-stu-id="4d71c-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="4d71c-146">Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł hello</span><span class="sxs-lookup"><span data-stu-id="4d71c-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="4d71c-147">[Azure piątki: Usługi Azure CDN zaawansowanych nowych funkcji Premium](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (klip wideo)</span><span class="sxs-lookup"><span data-stu-id="4d71c-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>