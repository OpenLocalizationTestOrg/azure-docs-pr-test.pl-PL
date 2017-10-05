---
title: "Azure implementacji usługi Mobile Engagement dla aplikacji do grania"
description: "Gry scenariusz aplikacji do wdrożenia usługi Azure Mobile Engagement"
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
ms.openlocfilehash: 0ca35a3d634db8eb5c63afacba046a35b8a3e7ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="1679d-103">Wdrożenie usługi Mobile Engagement z aplikacji do grania</span><span class="sxs-lookup"><span data-stu-id="1679d-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="1679d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1679d-104">Overview</span></span>
<span data-ttu-id="1679d-105">Uruchamiania gier uruchomiła nową aplikację gier role play/strategii połowy na podstawie.</span><span class="sxs-lookup"><span data-stu-id="1679d-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="1679d-106">Gry została uruchomiona przez 6 miesięcy.</span><span class="sxs-lookup"><span data-stu-id="1679d-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="1679d-107">Gry jest ogromny sukces i ma miliony pliki do pobrania i przechowywania w porównaniu do innych aplikacji gry rozruchu jest bardzo duże.</span><span class="sxs-lookup"><span data-stu-id="1679d-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="1679d-108">Na zgromadzeniu co kwartał przeglądu uczestników zgodę potrzebnych do zwiększenia Średni przychód na użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1679d-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="1679d-109">Premium w grze pakiety są dostępne jako ofertach specjalnych.</span><span class="sxs-lookup"><span data-stu-id="1679d-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="1679d-110">Te pakiety gier Zezwalaj użytkownikom na wygląd i wydajności ich linii połowy i przynętą lub tackles w grze uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="1679d-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="1679d-111">Jednak sprzedaży pakietu są bardzo niskie.</span><span class="sxs-lookup"><span data-stu-id="1679d-111">However, package sales are very low.</span></span> <span data-ttu-id="1679d-112">Tak zdecydują najpierw przeanalizować obsługi klienta za pomocą narzędzia analizy, a następnie do opracowywania konsultacje segmentacji Zaawansowane na zwiększenie sprzedaży przy użyciu programu.</span><span class="sxs-lookup"><span data-stu-id="1679d-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="1679d-113">Na podstawie [usługi Azure Mobile Engagement - Getting Started Guide z najlepszymi rozwiązaniami](mobile-engagement-getting-started-best-practices.md) tworzenia strategia zaangażowania.</span><span class="sxs-lookup"><span data-stu-id="1679d-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="1679d-114">Celów i wskaźników KPI</span><span class="sxs-lookup"><span data-stu-id="1679d-114">Objectives and KPIs</span></span>
<span data-ttu-id="1679d-115">Spełnia wymagania najważniejszych uczestników gry.</span><span class="sxs-lookup"><span data-stu-id="1679d-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="1679d-116">Wszystkie zgodzić się na jednym z celów głównego — zwiększenie sprzedaży pakietu premium 15%.</span><span class="sxs-lookup"><span data-stu-id="1679d-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="1679d-117">Tworzenia biznesowej kluczowych wskaźników wydajności (KPI) do mierzenia i dysk ten cel</span><span class="sxs-lookup"><span data-stu-id="1679d-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="1679d-118">Na poziom gry te pakiety zakupionych?</span><span class="sxs-lookup"><span data-stu-id="1679d-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="1679d-119">Co to jest przychód na użytkownika, na sesję punktów w tygodniu i miesiącu?</span><span class="sxs-lookup"><span data-stu-id="1679d-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="1679d-120">Co to są typy zakupu ulubionych?</span><span class="sxs-lookup"><span data-stu-id="1679d-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="1679d-121">Część 1 z [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) wyjaśniono, jak zdefiniować celów i wskaźników KPI.</span><span class="sxs-lookup"><span data-stu-id="1679d-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="1679d-122">Z biznesowe wskaźniki KPI dotyczące teraz zdefiniowany Menedżer produktu Mobile tworzy zaangażowania kluczowych wskaźników wydajności, aby określić nowy użytkownik trendów i przechowywania.</span><span class="sxs-lookup"><span data-stu-id="1679d-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="1679d-123">Monitorowanie przechowywania i używać w następujących odstępach: codziennie, co 2 dni, co tydzień, co miesiąc i co 3 miesiące</span><span class="sxs-lookup"><span data-stu-id="1679d-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="1679d-124">Liczby aktywnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="1679d-124">Active user counts</span></span>
* <span data-ttu-id="1679d-125">Klasyfikacja aplikacji w magazynie</span><span class="sxs-lookup"><span data-stu-id="1679d-125">The app rating in the store</span></span>

<span data-ttu-id="1679d-126">Na podstawie zaleceń IT przez zespół, następujące kluczowe wskaźniki wydajności techniczne zostały dodane do odpowiedzieć na następujące pytania:</span><span class="sxs-lookup"><span data-stu-id="1679d-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="1679d-127">Co to jest ścieżka do użytkownika (odwiedzenia strony, ile czasu użytkownicy poświęcają na nim)</span><span class="sxs-lookup"><span data-stu-id="1679d-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="1679d-128">Liczba awarii (Crash) i zgłaszanie usterek napotkał na sesję</span><span class="sxs-lookup"><span data-stu-id="1679d-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="1679d-129">Które wersje systemu operacyjnego działają moich użytkowników?</span><span class="sxs-lookup"><span data-stu-id="1679d-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="1679d-130">Co to jest to średni rozmiar ekranu dla moich użytkowników?</span><span class="sxs-lookup"><span data-stu-id="1679d-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="1679d-131">Jakiego rodzaju łączności z Internetem masz moich użytkowników?</span><span class="sxs-lookup"><span data-stu-id="1679d-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="1679d-132">Dla poszczególnych wskaźników Mobile Manager produktu określa potrzebuje i gdzie znajduje się w jej podręcznika dotyczącego danych.</span><span class="sxs-lookup"><span data-stu-id="1679d-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="1679d-133">Program zaangażowania i integracja</span><span class="sxs-lookup"><span data-stu-id="1679d-133">Engagement program and integration</span></span>
<span data-ttu-id="1679d-134">Przed zbudowaniem program zaangażowania zaawansowane, dyrektor projektu Mobile odpowiedzialnym za projektu powinien mieć bezpośredni zrozumienia, jak i produktów są używane przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1679d-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="1679d-135">Po 3 miesiące Dyrektor projektu Mobile zebrał wystarczającej ilości danych w celu zwiększenia jego sprzedaży powiadomień wypychanych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1679d-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="1679d-136">ADAM uzyskuje informacje o który:</span><span class="sxs-lookup"><span data-stu-id="1679d-136">He learns that:</span></span>

* <span data-ttu-id="1679d-137">Pierwszy zakup zwykle odbywa się na poziomie 14.</span><span class="sxs-lookup"><span data-stu-id="1679d-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="1679d-138">90% tych przypadkach zakupu jest bronie legendarnych $3.</span><span class="sxs-lookup"><span data-stu-id="1679d-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="1679d-139">W takich przypadkach 80% użytkowników, które dokonały zakupu, kontynuuj produktu i wprowadź więcej zakupów.</span><span class="sxs-lookup"><span data-stu-id="1679d-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="1679d-140">Użytkownicy, którzy przekazanego poziom 20, uruchom poświęcić więcej niż 10/ tydzień.</span><span class="sxs-lookup"><span data-stu-id="1679d-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="1679d-141">Użytkownicy często kupić pakiety premium na poziomie 16, 24 i 32.</span><span class="sxs-lookup"><span data-stu-id="1679d-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="1679d-142">Dzięki tej analizy Dyrektor projektu Mobile decyduje się na utworzenie konkretnych sekwencji powiadomień, zwiększenie sprzedaży aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1679d-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="1679d-143">Tworzy trzy sekwencji powiadomień wypychanych, które wywołuje on: powitalny programu, Program sprzedaży i Program nieaktywne.</span><span class="sxs-lookup"><span data-stu-id="1679d-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="1679d-144">Więcej informacji można znaleźć w [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="1679d-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
