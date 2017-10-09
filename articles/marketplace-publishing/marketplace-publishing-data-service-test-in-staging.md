---
title: "aaaTesting oferty usługi danych dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tootest usługi danych oferty dla hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="5805c-103">Testowanie tej oferty usługi danych tymczasowych</span><span class="sxs-lookup"><span data-stu-id="5805c-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5805c-104">**W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.**</span><span class="sxs-lookup"><span data-stu-id="5805c-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="5805c-105">Jeśli masz aplikacji biznesowej SaaS chcesz toopublish na AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="5805c-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="5805c-106">Jeśli masz aplikacje IaaS lub dewelopera usługi będzie jak toopublish w witrynie Azure Marketplace więcej informacji można znaleźć [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="5805c-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="5805c-107">Po zakończeniu hello dwa pierwsze kroki z [utworzenie konta Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) i [Tworzenie oferty usługi danych w portalu publikowania](marketplace-publishing-data-service-creation.md) możesz przystąpić do udostępnianie w hello ofertę Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5805c-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="5805c-108">W tym temacie zostanie najpierw przeprowadzi użytkownika przez proces hello, pośrednie, krok o nazwie "tymczasowości"</span><span class="sxs-lookup"><span data-stu-id="5805c-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="5805c-109">Oznacza, że wdrażanie ofertę w prywatnej "piaskownicy", gdzie należy przetestować i sprawdzić jego działanie przed wypchnięciem go tooproduction przemieszczania.</span><span class="sxs-lookup"><span data-stu-id="5805c-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="5805c-110">Oferta Hello będą wyświetlane w tymczasowej analogiczny, jak tooa klienta, który został wdrożony go.</span><span class="sxs-lookup"><span data-stu-id="5805c-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="5805c-111">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="5805c-111">Step 1.</span></span> <span data-ttu-id="5805c-112">Wypychanie toostaging Twojej oferty</span><span class="sxs-lookup"><span data-stu-id="5805c-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="5805c-113">Wypychanie toostaging Twojego oferta pozwala oferta hello tootest przed staje się dostępna toofuture subskrybentów.</span><span class="sxs-lookup"><span data-stu-id="5805c-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="5805c-114">Widać, jak pojawiają się i funkcji dla tych danych tooyour subskrypcji przez Twoją ofertę.</span><span class="sxs-lookup"><span data-stu-id="5805c-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![Rysowanie](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="5805c-116">Zaloguj się do hello [Portal publikowania](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="5805c-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="5805c-117">Wybierz **usług danych** hello nawigacji po lewej stronie okna</span><span class="sxs-lookup"><span data-stu-id="5805c-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="5805c-118">Wybierz ofertę ma toopush toostaging.</span><span class="sxs-lookup"><span data-stu-id="5805c-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="5805c-119">Zostanie wyświetlone powitalne powyżej ekranu.</span><span class="sxs-lookup"><span data-stu-id="5805c-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="5805c-120">Kliknij przycisk **Push tooStaging** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5805c-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="5805c-121">Jeśli występują problemy z hello oferty, które potrzebne toobe ukończone toostaging wcześniejsze toopushing, zostanie wyświetlona lista wyświetlana.</span><span class="sxs-lookup"><span data-stu-id="5805c-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="5805c-122">Popraw te elementy, klikając każdego elementu listy hello.</span><span class="sxs-lookup"><span data-stu-id="5805c-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="5805c-123">Po wszystkich poprawek wprowadzonych, kliknij przycisk **Push tooStaging** przycisk ponownie.</span><span class="sxs-lookup"><span data-stu-id="5805c-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="5805c-124">Jeśli nie występują problemy z Twoją ofertę zobaczysz oknie podręcznym hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="5805c-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="5805c-125">Jeśli nie masz planowania nie zatwierdzone toosurface Twojej oferty w portalu Azure (aktualnie ma ograniczoną pojemność), a następnie hello właśnie Zamknij okno podręczne.</span><span class="sxs-lookup"><span data-stu-id="5805c-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="5805c-126">tootest danych usługi w portalu Azure (w portalu DataMarket toohello dodanie), konieczne będzie tootest identyfikator subskrypcji platformy Azure z.</span><span class="sxs-lookup"><span data-stu-id="5805c-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="5805c-127">Ten identyfikator subskrypcji określi hello konta, które będą dozwolone tootest ofertę.</span><span class="sxs-lookup"><span data-stu-id="5805c-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="5805c-128">Wyciąć i wkleić identyfikator subskrypcji, a następnie kliknij przycisk hello toocontinue znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="5805c-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="5805c-130">Te identyfikatory subskrypcji platformy Azure są tylko wymaganych do testowania i przejściowych w hello [portalu zarządzania Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="5805c-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="5805c-131">Nie są one wymagane tootest w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5805c-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="5805c-132">Hello dalej ekran pokazuje czy publikowanie odbywa się za pomocą wyświetlania hello "w toku" ikona wyróżnione żółty poniżej.</span><span class="sxs-lookup"><span data-stu-id="5805c-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="5805c-133">Wypychanie toostaging zajmuje od 10 minut too15.</span><span class="sxs-lookup"><span data-stu-id="5805c-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="5805c-134">Jeśli trwa dłużej, najpierw należy odświeżyć przeglądarkę (klawisz F5 w programie Internet Explorer).</span><span class="sxs-lookup"><span data-stu-id="5805c-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="5805c-135">W rzadkich przypadkach hello gdzie ofertę nadal jest wypychanie toostaging po upływie godziny kliknij przycisk hello skontaktuj się z nami link toolet nam znać, że występuje problem.</span><span class="sxs-lookup"><span data-stu-id="5805c-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="5805c-137">Zakończeniu tooStaging wypychania hello hello "w toku" ikony zostanie zatrzymane, przenoszenie, a hello stan zostanie zaktualizowany za "przemieszczane".</span><span class="sxs-lookup"><span data-stu-id="5805c-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="5805c-138">Użytkownik jest teraz gotowy tootest ofertę.</span><span class="sxs-lookup"><span data-stu-id="5805c-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="5805c-139">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="5805c-139">Step 2.</span></span> <span data-ttu-id="5805c-140">Testowanie przemieszczanego ofertę w DataMarket</span><span class="sxs-lookup"><span data-stu-id="5805c-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="5805c-141">Kliknij łącze powitania po tekst hello **"Zobacz usługi oferują na..."**</span><span class="sxs-lookup"><span data-stu-id="5805c-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="5805c-142">ekran hello toodisplay hello subskrybenta zobaczą, gdy ofertę przechodzi tooproduction i pojawi się w sekcji DataMarket witryny.</span><span class="sxs-lookup"><span data-stu-id="5805c-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="5805c-144">Test lub sprawdź każdy z elementów 12 hello oznaczone powyżej tooensure wszystkich logo, ceny/transakcji, tekst, obrazy, dokumentacji i łącza są poprawne i działają prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="5805c-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="5805c-145">Jest to tooensure odpowiedni moment, w których wszystkie wartości testowe wprowadzona podczas tworzenia Twojej oferty zostały zastąpione rzeczywistymi wartościami.</span><span class="sxs-lookup"><span data-stu-id="5805c-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="5805c-146">Oferta logo</span><span class="sxs-lookup"><span data-stu-id="5805c-146">Offer logo</span></span>
2. <span data-ttu-id="5805c-147">Nazwa oferty</span><span class="sxs-lookup"><span data-stu-id="5805c-147">Offer name</span></span>
3. <span data-ttu-id="5805c-148">Witryna sieci Web firmy wydawcy łącze/nazwy tooyour</span><span class="sxs-lookup"><span data-stu-id="5805c-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="5805c-149">Kategorie wyszukiwania dla danej oferty</span><span class="sxs-lookup"><span data-stu-id="5805c-149">Search categories for your offer</span></span>
5. <span data-ttu-id="5805c-150">Subskrybenci tooassist łącza pomocy technicznej Twojej oferty</span><span class="sxs-lookup"><span data-stu-id="5805c-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="5805c-151">Kontekstowe opis dla danej oferty</span><span class="sxs-lookup"><span data-stu-id="5805c-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="5805c-152">Plan oferta przedstawiające szczegółów rozliczeń</span><span class="sxs-lookup"><span data-stu-id="5805c-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="5805c-153">Kod tooimplementation powiązania</span><span class="sxs-lookup"><span data-stu-id="5805c-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="5805c-154">Przykładowe obrazy, które ilustrują korzystanie z danych oferty</span><span class="sxs-lookup"><span data-stu-id="5805c-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="5805c-155">Metadane wejścia/wyjścia dla każdej usługi w ramach hello oferty</span><span class="sxs-lookup"><span data-stu-id="5805c-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="5805c-156">Oferty warunki użytkowania</span><span class="sxs-lookup"><span data-stu-id="5805c-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="5805c-157">Podgląd danych hello oferty</span><span class="sxs-lookup"><span data-stu-id="5805c-157">Preview of hello offer's data</span></span>

<span data-ttu-id="5805c-158">Na koniec sprawdzenie, czy usługa hello będzie działać przez hello Datamarket, klikając łącze hello "EKSPLORUJ ten zestaw danych".</span><span class="sxs-lookup"><span data-stu-id="5805c-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="5805c-159">Zostanie otwarty w nowym oknie narzędzia hello nazywamy "Eksploratora usługi", można wyświetlić podgląd wyników zapytania hello wysyłane do usługi.</span><span class="sxs-lookup"><span data-stu-id="5805c-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="5805c-160">W tym oknie można wprowadzić hello parametry potrzebne i wyświetlić wyniki hello wyświetlony w wyniku zapytania względem usługi.</span><span class="sxs-lookup"><span data-stu-id="5805c-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="5805c-161">Wyświetlana jest również hello adres URL dla zapytania.</span><span class="sxs-lookup"><span data-stu-id="5805c-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="5805c-162">Należy się tooreview hello opis tekstowy wyświetlany u góry hello usługi hello.</span><span class="sxs-lookup"><span data-stu-id="5805c-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="5805c-163">A jeśli ofertę składa się z więcej niż jedna usługa wywołania, kliknij karty hello na powitania dolnej tooswitch toohello dalej usługi tooreview i przetestowania.</span><span class="sxs-lookup"><span data-stu-id="5805c-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="5805c-164">Następny krok</span><span class="sxs-lookup"><span data-stu-id="5805c-164">Next step</span></span>
<span data-ttu-id="5805c-165">Jeśli występują problemy dotyczące i potrzebujesz pomocy ich rozwiązywanie skontaktuj się z pomocą [techniczną wydawcy Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="5805c-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="5805c-166">Jeśli są prawidłowe i gotowe toopublish ofertę przeczytaj hello [tooProduction tooPush zatwierdzenie żądania](marketplace-publishing-push-to-production.md) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="5805c-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="5805c-167">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5805c-167">See Also</span></span>
* [<span data-ttu-id="5805c-168">Wprowadzenie: Jak toopublish toohello oferta portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="5805c-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

