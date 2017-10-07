---
title: "aaaAzure implementacji usługi Mobile Engagement dla aplikacji do grania"
description: "Gry tooimplement scenariusza aplikacji usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="8f215-103">Wdrożenie usługi Mobile Engagement z aplikacji do grania</span><span class="sxs-lookup"><span data-stu-id="8f215-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="8f215-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="8f215-104">Overview</span></span>
<span data-ttu-id="8f215-105">Uruchamiania gier uruchomiła nową aplikację gier role play/strategii połowy na podstawie.</span><span class="sxs-lookup"><span data-stu-id="8f215-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="8f215-106">gry Hello została uruchomiona przez 6 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="8f215-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="8f215-107">Gry jest ogromny sukces i ma miliony pliki do pobrania i przechowywania hello jest bardzo duże tooother porównaniu uruchamiania gier aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8f215-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="8f215-108">Na powitania spotkaniu przeglądu co kwartał, uczestników zgodę potrzebnych tooincrease Średni przychód na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f215-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="8f215-109">Premium w grze pakiety są dostępne jako ofertach specjalnych.</span><span class="sxs-lookup"><span data-stu-id="8f215-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="8f215-110">Te pakiety gier Zezwalaj użytkowników tooupgrade hello wygląd i wydajność swoich połowy wierszy i przynętą lub tackles w grze hello.</span><span class="sxs-lookup"><span data-stu-id="8f215-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="8f215-111">Jednak sprzedaży pakietu są bardzo niskie.</span><span class="sxs-lookup"><span data-stu-id="8f215-111">However, package sales are very low.</span></span> <span data-ttu-id="8f215-112">Dzięki zdecydują pierwszego tooanalyze powitania klienta doświadczenia z narzędziem analytics i następnie toodevelop zaangażowania program tooincrease sprzedaży, używając zaawansowane segmentacji.</span><span class="sxs-lookup"><span data-stu-id="8f215-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="8f215-113">Oparte na powitania [usługi Azure Mobile Engagement - Getting Started Guide z najlepszymi rozwiązaniami](mobile-engagement-getting-started-best-practices.md) tworzenia strategia zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="8f215-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="8f215-114">Celów i wskaźników KPI</span><span class="sxs-lookup"><span data-stu-id="8f215-114">Objectives and KPIs</span></span>
<span data-ttu-id="8f215-115">Spełnia wymagania najważniejszych uczestników hello gier.</span><span class="sxs-lookup"><span data-stu-id="8f215-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="8f215-116">Wszystkie zgodzić się na jednym głównym celem - tooincrease premium pakietu sprzedaży przez 15%.</span><span class="sxs-lookup"><span data-stu-id="8f215-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="8f215-117">Tworzenie one toomeasure firm kluczowych wskaźników wydajności (KPI) i dysk ten cel</span><span class="sxs-lookup"><span data-stu-id="8f215-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="8f215-118">Na poziom gry hello te pakiety zakupionych?</span><span class="sxs-lookup"><span data-stu-id="8f215-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="8f215-119">Co to jest hello przychód na użytkownika, na sesję na tydzień i miesięcznie?</span><span class="sxs-lookup"><span data-stu-id="8f215-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="8f215-120">Co to są typy ulubionych zakupu hello?</span><span class="sxs-lookup"><span data-stu-id="8f215-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="8f215-121">Część 1 hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) wyjaśniono, jak toodefine hello celów i wskaźników KPI.</span><span class="sxs-lookup"><span data-stu-id="8f215-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="8f215-122">Z powitalne biznesowe wskaźniki KPI dotyczące teraz zdefiniowany hello Mobile produktu Manager tworzy wskaźników KPI zaangażowania toodetermine nowego użytkownika trendów i przechowywania.</span><span class="sxs-lookup"><span data-stu-id="8f215-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="8f215-123">Monitorowanie przechowywania i użyj na powitania po interwałów: codziennie, co 2 dni, co tydzień, co miesiąc i co 3 miesiące</span><span class="sxs-lookup"><span data-stu-id="8f215-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="8f215-124">Liczby aktywnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="8f215-124">Active user counts</span></span>
* <span data-ttu-id="8f215-125">Klasyfikacja aplikacji Hello w hello przechowywania</span><span class="sxs-lookup"><span data-stu-id="8f215-125">hello app rating in hello store</span></span>

<span data-ttu-id="8f215-126">Na podstawie zaleceń z hello zespół IT, powitania po techniczne kluczowych wskaźników wydajności zostały dodane hello tooanswer następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="8f215-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="8f215-127">Co to jest ścieżka do użytkownika (odwiedzenia strony, ile czasu użytkownicy poświęcają na nim)</span><span class="sxs-lookup"><span data-stu-id="8f215-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="8f215-128">Liczba awarii (Crash) i zgłaszanie usterek napotkał na sesję</span><span class="sxs-lookup"><span data-stu-id="8f215-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="8f215-129">Które wersje systemu operacyjnego działają moich użytkowników?</span><span class="sxs-lookup"><span data-stu-id="8f215-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="8f215-130">Co to jest hello średni rozmiar ekranu dla moich użytkowników?</span><span class="sxs-lookup"><span data-stu-id="8f215-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="8f215-131">Jakiego rodzaju łączności z Internetem masz moich użytkowników?</span><span class="sxs-lookup"><span data-stu-id="8f215-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="8f215-132">Dla poszczególnych wskaźników hello Mobile produktu Manager określa dane hello potrzebuje i gdzie znajduje się w jej podręcznikowym.</span><span class="sxs-lookup"><span data-stu-id="8f215-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="8f215-133">Program zaangażowania i integracja</span><span class="sxs-lookup"><span data-stu-id="8f215-133">Engagement program and integration</span></span>
<span data-ttu-id="8f215-134">Przed zbudowaniem program zaangażowania zaawansowane, hello Dyrektor projektu Mobile odpowiedzialnym za hello projektu powinien wiedzę głębokie jak i kiedy produkty są używane przez użytkowników na powitania.</span><span class="sxs-lookup"><span data-stu-id="8f215-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="8f215-135">Po 3 miesiące hello Dyrektor projektu Mobile zebrał tooenhance wystarczającej ilości danych sprzedaży powiadomień wypychanych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8f215-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="8f215-136">ADAM uzyskuje informacje o który:</span><span class="sxs-lookup"><span data-stu-id="8f215-136">He learns that:</span></span>

* <span data-ttu-id="8f215-137">Witaj pierwszego zakupu zwykle odbywa się na poziomie hello 14.</span><span class="sxs-lookup"><span data-stu-id="8f215-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="8f215-138">90% tych przypadkach zakupu hello jest bronie legendarnych $3.</span><span class="sxs-lookup"><span data-stu-id="8f215-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="8f215-139">W takich przypadkach 80% użytkowników, które dokonały zakupu, kontynuuj hello produktu i wprowadź więcej zakupów.</span><span class="sxs-lookup"><span data-stu-id="8f215-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="8f215-140">Użytkownicy, którzy przekazanego poziom hello 20, uruchom toospend więcej niż 10/ tydzień.</span><span class="sxs-lookup"><span data-stu-id="8f215-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="8f215-141">Użytkownicy często toobuy pakietów premium na poziomie 16, 24 i 32.</span><span class="sxs-lookup"><span data-stu-id="8f215-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="8f215-142">Dziękujemy analizy toothis hello Dyrektor projektu Mobile decyduje toocreate konkretnych powiadomienia sekwencji tooincrease sprzedaży aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8f215-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="8f215-143">Tworzy trzy sekwencji powiadomień wypychanych, które wywołuje on: powitalny programu, Program sprzedaży i Program nieaktywne.</span><span class="sxs-lookup"><span data-stu-id="8f215-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="8f215-144">Aby uzyskać więcej informacji można znaleźć toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="8f215-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
