---
title: "toocreating aaaGuide usługi danych dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje sposobu toocreate, certyfikować i wdrożyć usługę Data zakupu na hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a><span data-ttu-id="6ea6a-103">Podręcznik publikowania danych usługi dla hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6ea6a-103">Data Service Publishing Guide for hello Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6ea6a-104">**W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.**</span><span class="sxs-lookup"><span data-stu-id="6ea6a-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="6ea6a-105">Jeśli masz aplikacji biznesowej SaaS chcesz toopublish na AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="6ea6a-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="6ea6a-106">Jeśli masz aplikacje IaaS lub dewelopera usługi będzie jak toopublish w witrynie Azure Marketplace więcej informacji można znaleźć [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="6ea6a-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="6ea6a-107">Po ukończeniu hello w kroku 1, [tworzenia kont i rejestracji](marketplace-publishing-accounts-creation-registration.md), możemy przewodnikiem za pośrednictwem hello [ogólne nietechnicznej](marketplace-publishing-pre-requisites.md) i [wymagania techniczne](marketplace-publishing-data-service-creation-prerequisites.md) usługi danych oferty w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-107">After completing hello step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through hello [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="6ea6a-108">Obecnie firma Microsoft przeprowadzi Cię przez kroki hello tworzenia oferty usługi danych na powitania [Portal publikowania] [ link-pubportal] dla hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-108">Now we will walk you through hello steps for creating a Data Service offer on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="1----login-toohello-publishing-portal"></a><span data-ttu-id="6ea6a-109">1.    Toohello logowania Portal publikowania.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-109">1.    Login toohello Publishing Portal.</span></span>
<span data-ttu-id="6ea6a-110">Przejdź do zbyt[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="6ea6a-110">Go too[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="6ea6a-111">**Dla pierwszego czasu tooPublishing logowania portalu Użyj tego samego konta, z którą profil sprzedawcy firmy zarejestrowano w Centrum deweloperów powitalne.**</span><span class="sxs-lookup"><span data-stu-id="6ea6a-111">**For first time login tooPublishing Portal, use hello same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="6ea6a-112">(Później możesz dodać każdy pracownik firmy jako współadministrator w hello publikowania portalu).</span><span class="sxs-lookup"><span data-stu-id="6ea6a-112">(Later you can add any employee of your company as a co-admin in hello Publishing Portal).</span></span>

<span data-ttu-id="6ea6a-113">Polecenie hello **publikowania usług danych** kafelka, jeśli jest to hello pierwszego logowania do portalu publikowania hello.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-113">Click on hello **Publish a Data Services** tile if this is hello first login into hello publishing portal.</span></span>

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a><span data-ttu-id="6ea6a-114">2.    Wybierz **usług danych** w menu nawigacji hello na powitania po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-114">2.    Choose **Data Services** in hello navigation menu on hello left side.</span></span>
  ![Rysowanie](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="6ea6a-116">3.    Tworzenie nowej usługi danych</span><span class="sxs-lookup"><span data-stu-id="6ea6a-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="6ea6a-117">Wypełnij hello tytuł dla Twojej nowych danych usługi oferty i kliknij na "+" na powitania prawo.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-117">Fill in hello title for your new Data Service Offer and click on “+” on hello right.</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a><span data-ttu-id="6ea6a-119">4.    Przejrzyj hello podmenu w obszarze hello nowo utworzona Usługa danych w menu nawigacji hello.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-119">4.    Review hello sub-menu under hello newly created Data Service in hello navigation menu.</span></span>
<span data-ttu-id="6ea6a-120">Polecenie hello **wskazówki** i przejrzyj wszelkie niezbędne kroki potrzebne toopublish prawidłowo hello Usługa danych na hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-120">Click on hello **Walkthrough** tab and review all necessary steps needed toopublish properly hello Data Service on hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="6ea6a-121">Należy zawsze kliknij hello łączy na stronie "Wskazówki" hello lub użyj karty w podmenu oferty usługi danych powitania po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-121">You always can click on hello links in hello “Walkthrough” page or use tabs on hello Data Service offer’s sub-menu on hello left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="6ea6a-122">5.    Utwórz nowy Plan.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="6ea6a-123">Oferuje planów, transakcje.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="6ea6a-124">Każda oferta może mieć wiele planów, ale musi mieć co najmniej jednego (1) planu.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="6ea6a-125">Użytkownicy końcowi subskrypcji oferta tooyour one subskrypcji dla jednego planu hello oferty.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-125">When end-users subscribe tooyour offer they subscribe for one of hello offer’s Plan.</span></span> <span data-ttu-id="6ea6a-126">Każdy plan określa, jak użytkownicy końcowi będą się mogli toouse usługi.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-126">Each plan defines how end-users will be able toouse your service.</span></span>

<span data-ttu-id="6ea6a-127">Obecnie portalu Azure Marketplace obsługuje tylko miesięczne transakcji subskrypcji na podstawie modelu usług danych, tj. użytkownicy końcowi będą zwrócić miesięczna zgodnie z toohello ceny hello specjalnego planu subskrybowanego one tooand będą mogli tooconsume numer każdego miesiąca zdefiniowane przez hello plan transakcji.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according toohello price of hello specific plan they subscribed tooand will be able tooconsume each month number of transaction defined by hello plan.</span></span>

<span data-ttu-id="6ea6a-128">Każdą transakcję zazwyczaj definiowane jako liczba rekordów, który zwróci dane usługi na podstawie hello zapytania wysyłane toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-128">Each Transaction usually defined as number of records your Data Service will return based on hello query sent toohello Service.</span></span> <span data-ttu-id="6ea6a-129">Witaj domyślna to 100.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-129">hello default is 100.</span></span> <span data-ttu-id="6ea6a-130">Liczba transakcji zwrócił tooeach zapytanie zostanie liczba rekordów podzielona przez 100 i zostać zaokrąglona w górę do najbliższej liczby całkowitej toohello.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-130">Number of transactions returned tooeach query will be number of records divided by 100 and rounded up toohello closest integer.</span></span>

<span data-ttu-id="6ea6a-131">Jest usługę Azure Marketplace warstwy odpowiedzialność toomonitor (licznik) liczba transakcji używane przez każdego zapytania.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-131">It’s Azure Marketplace Service layer responsibility toomonitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ea6a-132">Użytkowników końcowych, które osiągnęła limit transakcji hello w miesiącu hello zostanie zablokowane przed kontynuowaniem toouse hello usługi do końca ich miesięcznego cyklu subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-132">End-Users which reached hello transaction limit during hello month will be blocked from continuing toouse hello service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="6ea6a-133">Hello planu lub jeden z planów hello może ale nie musi zawierać nieograniczoną liczbę transakcji.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-133">hello plan or one of hello plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="6ea6a-134">Tworzenie planu.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-134">Create a plan.</span></span>
1. <span data-ttu-id="6ea6a-135">Polecenie **"+"** dalej toohello "Dodaj nowy plan".</span><span class="sxs-lookup"><span data-stu-id="6ea6a-135">Click on **“+”** next toohello “Add a new plan”.</span></span>
2. <span data-ttu-id="6ea6a-136">Wybierz jedną z opcji hello: **nieograniczone** lub **ograniczone** użycia tego planu.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-136">Choose one of hello options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="6ea6a-137">Jeśli Limited następnie podaj numer hello planu hello transakcji umożliwia tooconsume w ciągu miesiąca.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-137">If Limited then provide hello number of transaction hello plan will allow tooconsume in a month.</span></span>
   
    ![Rysowanie](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="6ea6a-139">Publikowanie portalu będzie również sugerować "Identyfikator planu", który będzie używany toocommunicate toohello użytkowników końcowych hello Nazwa planu hello hello interfejsu użytkownika i również używane przez hello usługi rynek tooidentify hello planu.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-139">Publishing Portal will also suggest “Plan Identifier”, which will be used toocommunicate toohello end-users hello name of hello plan in hello UI and also used by hello Market Place Service tooidentify hello Plan.</span></span> <span data-ttu-id="6ea6a-140">Witaj "Identyfikator planu" można zmienić, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-140">You can change hello “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6ea6a-141">Witaj "Identyfikator planu" musi być unikatowa w zakresie hello każdego oferty.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-141">hello “Plan Identifier” must be unique within hello scope of each offer.</span></span> <span data-ttu-id="6ea6a-142">Jak użyć innych identyfikatorów w hello identyfikator zostanie zablokowane po hello pierwszy tooproduction publikowania i nie będzie możliwe toochange publikowania planowanie portalu tego identyfikatora.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-142">As many other Identifiers used in hello Publishing Portal Plan identifier will be locked after hello first publishing tooproduction and you will not be able toochange this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="6ea6a-143">Kliknij przycisk tooaccept wybór.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-143">Click tooaccept your choice.</span></span>
4. <span data-ttu-id="6ea6a-144">Następnie użytkownik zostanie poproszony kilka dodatkowych pytań dotyczących nowo utworzony Plan.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![Rysowanie](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="6ea6a-146">Zapytania</span><span class="sxs-lookup"><span data-stu-id="6ea6a-146">Question</span></span> | <span data-ttu-id="6ea6a-147">Istotności.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="6ea6a-148">**Ten Plan jest wolne i dostępne na całym świecie?**</span><span class="sxs-lookup"><span data-stu-id="6ea6a-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="6ea6a-149">Można utworzyć planu całkowicie wolne z — bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="6ea6a-150">Jego hello tylko plan dla tej oferty — oznacza, że w przypadku publikowania "Oferty bezpłatnej" w hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-150">If it’s hello only plan for this offer – it means that you are publishing “Free Offer” in hello Marketplace.</span></span> <span data-ttu-id="6ea6a-151">Jeśli jest tylko dla jednego (z kilku) planu, hello umożliwia toolearn użytkownicy końcowi toooffer opcję więcej informacji na temat usługi z stosunkowo małej liczby transakcji w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-151">If it’s only for one (of few) Plan, hello it gives you an option toooffer end-users toolearn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="6ea6a-152">W przypadku odpowiedzi hello "Tak", nie dalsze pytania będzie monitowany.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-152">If hello answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="6ea6a-153">Użytkownicy końcowi zawsze można uaktualnić toohello płatnej planów.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-153">End users can always upgrade toohello paid plans.</span></span>
> 
> 

| <span data-ttu-id="6ea6a-154">Zapytania</span><span class="sxs-lookup"><span data-stu-id="6ea6a-154">Question</span></span> | <span data-ttu-id="6ea6a-155">Istotności.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="6ea6a-156">**Bezpłatna wersja próbna jest dostępny?**</span><span class="sxs-lookup"><span data-stu-id="6ea6a-156">**Is free trial available?**</span></span> |<span data-ttu-id="6ea6a-157">Można wybrać między słowo "Trial nr" na wszystkich lub podać toouse opcji Plan "Miesiąc".</span><span class="sxs-lookup"><span data-stu-id="6ea6a-157">You can choose between “No Trial” at all or give an option toouse your Plan for “One Month”.</span></span> <span data-ttu-id="6ea6a-158">Wydawcy, takich jak toouse tej opcji tooprovide użytkownicy końcowi hello możliwości toounderstand hello zalet hello oferuje bezpłatnie przez jeden miesiąc.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-158">Publishers like toouse this option tooprovide end-users hello possibility toounderstand hello benefits of hello offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6ea6a-159">Użytkownicy końcowi będą tylko stanie toopurchase bezpłatnej wersji próbnej, jeśli ustanowionego instrumentem płatniczym np. karty kredytowej, umowy enterprise agreement.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-159">End-users will only be able toopurchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="6ea6a-160">Po upływie miesiąca hello bezpłatnej wersji próbnej portalu Azure Marketplace spowoduje uruchomienie ładowania klientów cen hello dzień hello hello subskrypcji, chyba że powitania klienta inicjowane hello anulowania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-160">After one month of hello free trial, Azure Marketplace will start charging customers hello price as of hello date of hello subscription, unless hello customer initiated hello subscription cancellation.</span></span> <span data-ttu-id="6ea6a-161">Nie specjalne powiadomienia będą dostarczane toohello użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-161">No special notification will be provided toohello end-users.</span></span>
> 
> 

| <span data-ttu-id="6ea6a-162">Zapytania</span><span class="sxs-lookup"><span data-stu-id="6ea6a-162">Question</span></span> | <span data-ttu-id="6ea6a-163">Istotności.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="6ea6a-164">**Ten plan wymaga toopurchase kod promocji?**</span><span class="sxs-lookup"><span data-stu-id="6ea6a-164">**This plan requires a promotion code toopurchase?**</span></span> |<span data-ttu-id="6ea6a-165">Wydawcy ma tootheir dostępu toolimit opcji plany usługi podając specjalne kodu, o nazwie "A Promocode" toospecific klientów.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-165">Publishers have an option toolimit access tootheir Service Plans by providing a special code, called “A Promocode” toospecific customers.</span></span> <span data-ttu-id="6ea6a-166">Tylko użytkownicy końcowi, których ten Promocode będą mogli toosubscribe toohello planu.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-166">Only end-users which will have this Promocode will be able toosubscribe toohello Plan.</span></span> <span data-ttu-id="6ea6a-167">Jeśli wybierzesz opcję "Nie", potwierdzam, że wszyscy z regionu hello gdzie oferują hello są dostępne (zobacz [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) więcej szczegółów) będą mogli toosubscribe toothis planu.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-167">If you choose “No”, then you agree that everyone from hello region where hello offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able toosubscribe toothis plan.</span></span> <span data-ttu-id="6ea6a-168">Nie dalsze pytania pojawi się monit.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="6ea6a-169">**Również ukryć ten plan z każdego, kto nie ma kod promocyjny prawidłowy?**</span><span class="sxs-lookup"><span data-stu-id="6ea6a-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="6ea6a-170">Jeśli hello odpowiedzi toohello poprzedniego pytania "Tak" hello wydawcy ma toocompletely opcja Usuń ten plan z znajdujących się w hello UI hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-170">If hello answer toohello previous question is “Yes” hello Publisher has an option toocompletely remove this plan from appearing in hello UI of hello Marketplace.</span></span> <span data-ttu-id="6ea6a-171">Oznacza to, klienci nie będą widzieć tego planu, na stronie Szczegóły hello oferty.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-171">It means, customers will not see this plan in hello Offer’s details page.</span></span> <span data-ttu-id="6ea6a-172">Użytkownicy końcowi, które otrzymają promocode toopurchase, będzie on tooit toosubscribe możliwe przy użyciu tego promocode.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-172">End-users which will receive a promocode toopurchase it, will be able toosubscribe tooit using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="6ea6a-173">6.    Tworzenie z witryny Marketplace marketingu zawartości</span><span class="sxs-lookup"><span data-stu-id="6ea6a-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="6ea6a-174">Dla jak tooprovide informacje wymagane w **Marketing, cennik, pomocy technicznej i kategorie** karty odwiedź [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) co jest typowe artefakty tooall opublikowane w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-174">For How tooprovide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common tooall artifacts published in hello Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="6ea6a-175">7.    Połącz z tooyour oferty usługi (na podstawie usług SQL Azure lub usługi sieci Web na podstawie).</span><span class="sxs-lookup"><span data-stu-id="6ea6a-175">7.    Connect your offer tooyour Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="6ea6a-176">Polecenie hello **usług danych** podmenu.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-176">Click on hello **Data Services** sub-menu.</span></span>

<span data-ttu-id="6ea6a-177">W górnej części strony hello hello użytkownik zostanie zapytany oferta hello tooprovide **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-177">On hello upper half of hello page you’ll be asked tooprovide hello offer’s **Namespace**.</span></span>  

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="6ea6a-179">Hello poniżej pytanie definiują sposób hello wydawcy będzie tooexpose nowo utworzony tooAzure oferta portalu Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-179">hello below question will define how hello Publisher is going tooexpose newly created offer tooAzure Marketplace.</span></span> <span data-ttu-id="6ea6a-180">(Więcej informacji można znaleźć hello [podręcznik techniczny wymagań wstępnych usług danych](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="6ea6a-180">(For more details see hello [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="6ea6a-182">**Publikowanie hello na podstawie bazy danych usługi**</span><span class="sxs-lookup"><span data-stu-id="6ea6a-182">**Publishing hello Database based service**</span></span>

<span data-ttu-id="6ea6a-183">Polecenie **bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-183">Click on **Database**.</span></span> <span data-ttu-id="6ea6a-184">pojawi się Hello następujące strony:</span><span class="sxs-lookup"><span data-stu-id="6ea6a-184">hello following page will appear:</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="6ea6a-186">toocreate mapowanie CSDL hello zestawu danych oparte na powitania bazy danych SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="6ea6a-186">toocreate a CSDL mapping for hello Dataset based on hello SQL Azure DB:</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="6ea6a-188">A następnie dla każdej tabeli</span><span class="sxs-lookup"><span data-stu-id="6ea6a-188">And then for each table</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="6ea6a-191">Jeśli usługa sieci Web</span><span class="sxs-lookup"><span data-stu-id="6ea6a-191">If Web Service</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="6ea6a-193">Odczyt [mapowania istniejące sieci web tooOData usługi za pośrednictwem CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) Aby uzyskać szczegółowe instrukcje i przykłady dotyczące tworzenia CSDL usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-193">Read [Mapping an existing web service tooOData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6ea6a-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ea6a-194">Next Steps</span></span>
<span data-ttu-id="6ea6a-195">Teraz, po utworzeniu tej oferty usługi danych, upewnij się, że ukończeniu instrukcjami hello hello [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) przed przejściem do przodu zbyt[testowania w przejściowymusługidanych](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="6ea6a-195">Now that you've created your Data Service offer, please ensure that you complete hello instructions in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward too[Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="6ea6a-196">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6ea6a-196">See Also</span></span>
* [<span data-ttu-id="6ea6a-197">Wprowadzenie: Jak toopublish toohello oferta portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6ea6a-197">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="6ea6a-198">Jeśli interesuje Cię w uzgodnieniu hello ogólny proces mapowania OData i cel, przeczytaj ten artykuł [danych usługi OData mapowania](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definicje, struktur i instrukcje.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-198">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="6ea6a-199">Jeśli interesuje Cię learning oraz opis hello określonych węzłów i ich parametry, przeczytaj ten artykuł [węzły mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) definicje i wyjaśnienia, przykłady i kontekstu przypadków użycia.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-199">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="6ea6a-200">Jeśli jesteś zrecenzować przykłady, przeczytaj ten artykuł [przykłady mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee przykładowy kod i zrozumienie Składnia kodu i kontekstu.</span><span class="sxs-lookup"><span data-stu-id="6ea6a-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
