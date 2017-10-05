---
title: "Przewodnik dotyczący tworzenia usługi danych dla witryny Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje dotyczące sposobu tworzenia, certyfikować i wdrażania usługi danych dla kupić w witrynie Azure Marketplace."
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
ms.openlocfilehash: c0c9362f1c2e15c947aaaf7187f3383ad243140f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="data-service-publishing-guide-for-the-azure-marketplace"></a><span data-ttu-id="ba727-103">Usługi danych publikowania przewodnik witrynę Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ba727-103">Data Service Publishing Guide for the Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ba727-104">**W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.**</span><span class="sxs-lookup"><span data-stu-id="ba727-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="ba727-105">Jeśli masz aplikacji biznesowych SaaS chcesz publikować w AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="ba727-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="ba727-106">Jeśli masz aplikacje IaaS lub więcej informacji można znaleźć usługi developer chcesz publikować w witrynie Azure Marketplace [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="ba727-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="ba727-107">Po ukończeniu kroku 1, [tworzenia kont i rejestracji](marketplace-publishing-accounts-creation-registration.md), możemy narzuconego przez [ogólne nietechnicznej](marketplace-publishing-pre-requisites.md) i [wymagania techniczne](marketplace-publishing-data-service-creation-prerequisites.md) usługi danych oferty w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ba727-107">After completing the step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through the [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="ba727-108">Obecnie firma Microsoft przeprowadzi Cię przez kolejne etapy tworzenia oferty usługi danych na [Portal publikowania] [ link-pubportal] dla portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ba727-108">Now we will walk you through the steps for creating a Data Service offer on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="1----login-to-the-publishing-portal"></a><span data-ttu-id="ba727-109">1.    Zaloguj się do publikowania portalu.</span><span class="sxs-lookup"><span data-stu-id="ba727-109">1.    Login to the Publishing Portal.</span></span>
<span data-ttu-id="ba727-110">Przejdź do [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="ba727-110">Go to [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="ba727-111">**Pierwszy czasu logowania do portalu publikowania Użyj tego samego konta, z którym firmy sprzedawcy profil został zarejestrowany w Centrum deweloperów.**</span><span class="sxs-lookup"><span data-stu-id="ba727-111">**For first time login to Publishing Portal, use the same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="ba727-112">(Później możesz dodać każdy pracownik firmy jako współadministrator w portalu publikowania).</span><span class="sxs-lookup"><span data-stu-id="ba727-112">(Later you can add any employee of your company as a co-admin in the Publishing Portal).</span></span>

<span data-ttu-id="ba727-113">Polecenie **publikowania usług danych** kafelka, jeśli jest to pierwsze logowanie do portalu publikowania.</span><span class="sxs-lookup"><span data-stu-id="ba727-113">Click on the **Publish a Data Services** tile if this is the first login into the publishing portal.</span></span>

## <a name="2----choose-data-services-in-the-navigation-menu-on-the-left-side"></a><span data-ttu-id="ba727-114">2.    Wybierz **usług danych** w menu nawigacji po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="ba727-114">2.    Choose **Data Services** in the navigation menu on the left side.</span></span>
  ![Rysowanie](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="ba727-116">3.    Tworzenie nowej usługi danych</span><span class="sxs-lookup"><span data-stu-id="ba727-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="ba727-117">Wprowadź tytuł dla Twojej nowych danych usługi oferty i kliknij na "+" po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="ba727-117">Fill in the title for your new Data Service Offer and click on “+” on the right.</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-the-sub-menu-under-the-newly-created-data-service-in-the-navigation-menu"></a><span data-ttu-id="ba727-119">4.    Przejrzyj podmenu w obszarze usługi Data nowo utworzonego w menu nawigacji.</span><span class="sxs-lookup"><span data-stu-id="ba727-119">4.    Review the sub-menu under the newly created Data Service in the navigation menu.</span></span>
<span data-ttu-id="ba727-120">Polecenie **wskazówki** i przejrzyj wszystkie niezbędne kroki niezbędne do publikowania prawidłowo usługę danych w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ba727-120">Click on the **Walkthrough** tab and review all necessary steps needed to publish properly the Data Service on the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="ba727-121">Należy zawsze kliknięcie łącza na stronie "Wskazówki" lub użyj karty w podmenu oferty usługi danych po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="ba727-121">You always can click on the links in the “Walkthrough” page or use tabs on the Data Service offer’s sub-menu on the left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="ba727-122">5.    Utwórz nowy Plan.</span><span class="sxs-lookup"><span data-stu-id="ba727-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="ba727-123">Oferuje planów, transakcje.</span><span class="sxs-lookup"><span data-stu-id="ba727-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="ba727-124">Każda oferta może mieć wiele planów, ale musi mieć co najmniej jednego (1) planu.</span><span class="sxs-lookup"><span data-stu-id="ba727-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="ba727-125">Użytkownicy końcowi subskrybować ofertę one subskrypcji dla jednej z jej planu.</span><span class="sxs-lookup"><span data-stu-id="ba727-125">When end-users subscribe to your offer they subscribe for one of the offer’s Plan.</span></span> <span data-ttu-id="ba727-126">Każdy plan określa, jak użytkownicy końcowi będą mogli korzystać z usługi.</span><span class="sxs-lookup"><span data-stu-id="ba727-126">Each plan defines how end-users will be able to use your service.</span></span>

<span data-ttu-id="ba727-127">Obecnie portalu Azure Marketplace obsługuje tylko miesięczne transakcji subskrypcji na podstawie modelu usług danych, tj. użytkownicy końcowi będą płatności zgodnie z cen określonych planu, który one subskrybuje opłata miesięczna i będą mogli korzystać z każdego miesiąca liczba transakcji zdefiniowany w planie.</span><span class="sxs-lookup"><span data-stu-id="ba727-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according to the price of the specific plan they subscribed to and will be able to consume each month number of transaction defined by the plan.</span></span>

<span data-ttu-id="ba727-128">Każdą transakcję zazwyczaj definiowane jako liczba rekordów, który zwróci dane usługi na podstawie kwerendy wysyłane do usługi.</span><span class="sxs-lookup"><span data-stu-id="ba727-128">Each Transaction usually defined as number of records your Data Service will return based on the query sent to the Service.</span></span> <span data-ttu-id="ba727-129">Wartość domyślna to 100.</span><span class="sxs-lookup"><span data-stu-id="ba727-129">The default is 100.</span></span> <span data-ttu-id="ba727-130">Liczba transakcji zwracanych do każdego zapytania, które będzie liczba rekordów podzielona przez 100 i zaokrąglony do najbliższej liczby całkowitej.</span><span class="sxs-lookup"><span data-stu-id="ba727-130">Number of transactions returned to each query will be number of records divided by 100 and rounded up to the closest integer.</span></span>

<span data-ttu-id="ba727-131">Odpowiada usługę Azure Marketplace warstwy monitorować (licznik) liczbę transakcji używane przez każdego zapytania.</span><span class="sxs-lookup"><span data-stu-id="ba727-131">It’s Azure Marketplace Service layer responsibility to monitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba727-132">Kontynuowanie korzystania z usługi do końca ich miesięcznego cyklu subskrypcji zostanie zablokowane użytkowników końcowych, które osiągnęły limit transakcji w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="ba727-132">End-Users which reached the transaction limit during the month will be blocked from continuing to use the service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="ba727-133">Plan lub jeden z planów może ale nie musi zawierać nieograniczoną liczbę transakcji.</span><span class="sxs-lookup"><span data-stu-id="ba727-133">The plan or one of the plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="ba727-134">Tworzenie planu.</span><span class="sxs-lookup"><span data-stu-id="ba727-134">Create a plan.</span></span>
1. <span data-ttu-id="ba727-135">Polecenie **"+"** obok "Dodaj nowy plan".</span><span class="sxs-lookup"><span data-stu-id="ba727-135">Click on **“+”** next to the “Add a new plan”.</span></span>
2. <span data-ttu-id="ba727-136">Wybierz jedną z opcji: **nieograniczone** lub **ograniczone** użycia tego planu.</span><span class="sxs-lookup"><span data-stu-id="ba727-136">Choose one of the options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="ba727-137">Jeśli Limited następnie podaj liczbę transakcji plan umożliwia użycie w ciągu miesiąca.</span><span class="sxs-lookup"><span data-stu-id="ba727-137">If Limited then provide the number of transaction the plan will allow to consume in a month.</span></span>
   
    ![Rysowanie](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="ba727-139">Publikowanie portalu również sugerować "Identyfikator planu", który będzie używany do komunikacji użytkownicy końcowi Nazwa planu w interfejsie użytkownika i również używane przez usługę rynku, aby zidentyfikować Plan.</span><span class="sxs-lookup"><span data-stu-id="ba727-139">Publishing Portal will also suggest “Plan Identifier”, which will be used to communicate to the end-users the name of the plan in the UI and also used by the Market Place Service to identify the Plan.</span></span> <span data-ttu-id="ba727-140">"Identyfikator planu" można zmienić, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="ba727-140">You can change the “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ba727-141">"Identyfikator planu" musi być unikatowa w zakresie każdej oferty.</span><span class="sxs-lookup"><span data-stu-id="ba727-141">The “Plan Identifier” must be unique within the scope of each offer.</span></span> <span data-ttu-id="ba727-142">Jak wiele innych identyfikatorów używany w identyfikatorze planowanie publikowania portalu zostanie zablokowane po pierwszym publikowanie do produkcji, a nie będzie mógł zmienić ten identyfikator.</span><span class="sxs-lookup"><span data-stu-id="ba727-142">As many other Identifiers used in the Publishing Portal Plan identifier will be locked after the first publishing to production and you will not be able to change this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="ba727-143">Kliknij, aby zaakceptować wybór.</span><span class="sxs-lookup"><span data-stu-id="ba727-143">Click to accept your choice.</span></span>
4. <span data-ttu-id="ba727-144">Następnie użytkownik zostanie poproszony kilka dodatkowych pytań dotyczących nowo utworzony Plan.</span><span class="sxs-lookup"><span data-stu-id="ba727-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![Rysowanie](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="ba727-146">Zapytania</span><span class="sxs-lookup"><span data-stu-id="ba727-146">Question</span></span> | <span data-ttu-id="ba727-147">Istotności.</span><span class="sxs-lookup"><span data-stu-id="ba727-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="ba727-148">**Ten Plan jest wolne i dostępne na całym świecie?**</span><span class="sxs-lookup"><span data-stu-id="ba727-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="ba727-149">Można utworzyć planu całkowicie wolne z — bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="ba727-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="ba727-150">Jest tylko plan dla tej oferty — oznacza, że w przypadku publikowania "Oferty bezpłatnej" w witrynie Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ba727-150">If it’s the only plan for this offer – it means that you are publishing “Free Offer” in the Marketplace.</span></span> <span data-ttu-id="ba727-151">Jeśli jest tylko dla jednego (z kilku) planu, it udostępnia opcję umożliwiającą użytkownikom końcowym, aby dowiedzieć się więcej o usłudze z stosunkowo małej liczby transakcji w miesiącu.</span><span class="sxs-lookup"><span data-stu-id="ba727-151">If it’s only for one (of few) Plan, the it gives you an option to offer end-users to learn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="ba727-152">Jeśli odpowiedź brzmi "Tak", nie dalsze pytania będzie monitowany.</span><span class="sxs-lookup"><span data-stu-id="ba727-152">If the answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="ba727-153">Użytkownicy końcowi zawsze można uaktualnić do planów płatną.</span><span class="sxs-lookup"><span data-stu-id="ba727-153">End users can always upgrade to the paid plans.</span></span>
> 
> 

| <span data-ttu-id="ba727-154">Zapytania</span><span class="sxs-lookup"><span data-stu-id="ba727-154">Question</span></span> | <span data-ttu-id="ba727-155">Istotności.</span><span class="sxs-lookup"><span data-stu-id="ba727-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="ba727-156">**Bezpłatna wersja próbna jest dostępny?**</span><span class="sxs-lookup"><span data-stu-id="ba727-156">**Is free trial available?**</span></span> |<span data-ttu-id="ba727-157">Można wybrać między słowo "Trial nr" na wszystkich lub podać opcję do użycia z planem "Miesiąca".</span><span class="sxs-lookup"><span data-stu-id="ba727-157">You can choose between “No Trial” at all or give an option to use your Plan for “One Month”.</span></span> <span data-ttu-id="ba727-158">Aby użyć tej opcji, aby zapewnić użytkownikom końcowym możliwość korzyści oferta bezpłatnie przez jeden miesiąc, takich jak wydawcy.</span><span class="sxs-lookup"><span data-stu-id="ba727-158">Publishers like to use this option to provide end-users the possibility to understand the benefits of the offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ba727-159">Użytkownicy końcowi będą mogli tylko do zakupu bezpłatnej wersji próbnej, jeśli ustanowionego instrumentem płatniczym np. karty kredytowej, umowy enterprise agreement.</span><span class="sxs-lookup"><span data-stu-id="ba727-159">End-users will only be able to purchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="ba727-160">Po upływie miesiąca bezpłatnej wersji próbnej portalu Azure Marketplace spowoduje uruchomienie ładowania klientów cen dniu subskrypcji, chyba że klient zainicjował anulowania subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ba727-160">After one month of the free trial, Azure Marketplace will start charging customers the price as of the date of the subscription, unless the customer initiated the subscription cancellation.</span></span> <span data-ttu-id="ba727-161">Użytkownicy końcowi zostaną przekazane nie specjalne powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="ba727-161">No special notification will be provided to the end-users.</span></span>
> 
> 

| <span data-ttu-id="ba727-162">Zapytania</span><span class="sxs-lookup"><span data-stu-id="ba727-162">Question</span></span> | <span data-ttu-id="ba727-163">Istotności.</span><span class="sxs-lookup"><span data-stu-id="ba727-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="ba727-164">**Ten plan wymaga kod promocji, aby kupić?**</span><span class="sxs-lookup"><span data-stu-id="ba727-164">**This plan requires a promotion code to purchase?**</span></span> |<span data-ttu-id="ba727-165">Wydawcy mieć opcję, aby ograniczyć dostęp do swoich planów usługi podając specjalne kodu, o nazwie "A Promocode" dla specyficznych klientów.</span><span class="sxs-lookup"><span data-stu-id="ba727-165">Publishers have an option to limit access to their Service Plans by providing a special code, called “A Promocode” to specific customers.</span></span> <span data-ttu-id="ba727-166">Tylko użytkownicy końcowi, których ten Promocode będzie można zasubskrybować planu.</span><span class="sxs-lookup"><span data-stu-id="ba727-166">Only end-users which will have this Promocode will be able to subscribe to the Plan.</span></span> <span data-ttu-id="ba727-167">Jeśli wybierzesz opcję "Nie", a następnie oświadczasz, że wszyscy z regionu, w którym oferta jest dostępna (zobacz [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) więcej szczegółów) będzie mógł subskrybować tego planu.</span><span class="sxs-lookup"><span data-stu-id="ba727-167">If you choose “No”, then you agree that everyone from the region where the offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able to subscribe to this plan.</span></span> <span data-ttu-id="ba727-168">Nie dalsze pytania pojawi się monit.</span><span class="sxs-lookup"><span data-stu-id="ba727-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="ba727-169">**Również ukryć ten plan z każdego, kto nie ma kod promocyjny prawidłowy?**</span><span class="sxs-lookup"><span data-stu-id="ba727-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="ba727-170">Jeśli odpowiedź na powyższe pytanie jest "Tak" wydawcy ma opcję, aby całkowicie usunąć ten plan były wyświetlane w Interfejsie użytkownika witryny Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ba727-170">If the answer to the previous question is “Yes” the Publisher has an option to completely remove this plan from appearing in the UI of the Marketplace.</span></span> <span data-ttu-id="ba727-171">Oznacza to, klienci nie będą widzieć tego planu, na stronie Szczegóły oferty.</span><span class="sxs-lookup"><span data-stu-id="ba727-171">It means, customers will not see this plan in the Offer’s details page.</span></span> <span data-ttu-id="ba727-172">Użytkownicy końcowi, które otrzymają promocode zakupu, będzie można go przy użyciu tego promocode subskrybować.</span><span class="sxs-lookup"><span data-stu-id="ba727-172">End-users which will receive a promocode to purchase it, will be able to subscribe to it using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="ba727-173">6.    Tworzenie z witryny Marketplace marketingu zawartości</span><span class="sxs-lookup"><span data-stu-id="ba727-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="ba727-174">Jak informacji wymaganych w **Marketing, cennik, pomocy technicznej i kategorie** kart można znaleźć [Marketing przewodnik zawartości witryny Marketplace](marketplace-publishing-push-to-staging.md) co jest typowe do artefaktów wszystkie opublikowane na platformie Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ba727-174">For How to provide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common to all artifacts published in the Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-to-your-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="ba727-175">7.    Ofertę nawiązać połączenia z usługą (na podstawie usług SQL Azure lub usługi sieci Web na podstawie).</span><span class="sxs-lookup"><span data-stu-id="ba727-175">7.    Connect your offer to your Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="ba727-176">Polecenie **usług danych** podmenu.</span><span class="sxs-lookup"><span data-stu-id="ba727-176">Click on the **Data Services** sub-menu.</span></span>

<span data-ttu-id="ba727-177">W górnej części strony zostanie wyświetlony monit zapewnienie oferta **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="ba727-177">On the upper half of the page you’ll be asked to provide the offer’s **Namespace**.</span></span>  

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="ba727-179">Poniżej pytanie definiują sposób wydawcy ma oferta Uwidacznianie nowo utworzone w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ba727-179">The below question will define how the Publisher is going to expose newly created offer to Azure Marketplace.</span></span> <span data-ttu-id="ba727-180">(Więcej informacji można znaleźć [podręcznik techniczny wymagań wstępnych usług danych](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="ba727-180">(For more details see the [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="ba727-182">**Usługa bazy danych na podstawie publikowania**</span><span class="sxs-lookup"><span data-stu-id="ba727-182">**Publishing the Database based service**</span></span>

<span data-ttu-id="ba727-183">Polecenie **bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="ba727-183">Click on **Database**.</span></span> <span data-ttu-id="ba727-184">Pojawi się następujące strony:</span><span class="sxs-lookup"><span data-stu-id="ba727-184">The following page will appear:</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="ba727-186">Można utworzyć mapowania pliku CSDL dla zestawu danych, w oparciu o bazy danych SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="ba727-186">To create a CSDL mapping for the Dataset based on the SQL Azure DB:</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="ba727-188">A następnie dla każdej tabeli</span><span class="sxs-lookup"><span data-stu-id="ba727-188">And then for each table</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="ba727-191">Jeśli usługa sieci Web</span><span class="sxs-lookup"><span data-stu-id="ba727-191">If Web Service</span></span>

  ![Rysowanie](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="ba727-193">Odczyt [mapowania istniejące usługi OData za pomocą pliku CSDL sieci web](marketplace-publishing-data-service-creation-odata-mapping.md) Aby uzyskać szczegółowe instrukcje i przykłady dotyczące tworzenia CSDL usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="ba727-193">Read [Mapping an existing web service to OData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ba727-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ba727-194">Next Steps</span></span>
<span data-ttu-id="ba727-195">Teraz, po utworzeniu tej oferty usługi danych, sprawdź, czy wykonać instrukcje [Marketplace Przewodnik po zawartości marketingowej](marketplace-publishing-push-to-staging.md) przed przejściem do przodu do [testowanie usługi danych w tymczasowej](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="ba727-195">Now that you've created your Data Service offer, please ensure that you complete the instructions in the [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward to [Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="ba727-196">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ba727-196">See Also</span></span>
* [<span data-ttu-id="ba727-197">Wprowadzenie: Jak publikowanie oferty w portalu Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ba727-197">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="ba727-198">Jeśli interesuje Cię zrozumieć ogólny proces mapowania OData i cel, przeczytaj ten artykuł [danych usługi OData mapowania](marketplace-publishing-data-service-creation-odata-mapping.md) Aby przejrzeć definicje, struktur i instrukcje.</span><span class="sxs-lookup"><span data-stu-id="ba727-198">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="ba727-199">Jeśli interesuje Cię uczenia i zrozumienie określonych węzłów i ich parametry, przeczytaj ten artykuł [węzły mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) definicje i wyjaśnienia, przykłady i kontekstu przypadków użycia.</span><span class="sxs-lookup"><span data-stu-id="ba727-199">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="ba727-200">Jeśli jesteś zrecenzować przykłady, przeczytaj ten artykuł [przykłady mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-examples.md) aby zobaczyć przykładowy kod i zrozumieć Składnia kodu i kontekstu.</span><span class="sxs-lookup"><span data-stu-id="ba727-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
