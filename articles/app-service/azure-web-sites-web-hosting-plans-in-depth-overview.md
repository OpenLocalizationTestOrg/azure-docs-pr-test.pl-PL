---
title: "Szczegółowe omówienie planów usługi aplikacji Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak planów usługi App Service dla pracy w usłudze Azure App Service i korzyści do środowiska zarządzania."
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="07437-104">Szczegółowe omówienie planów usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="07437-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="07437-105">Plany usług aplikacji reprezentują kolekcji zasobów fizycznych używana do hostowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-105">App Service plans represent the collection of physical resources used to host your apps.</span></span>

<span data-ttu-id="07437-106">Plany usługi App Service definiują następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="07437-106">App Service plans define:</span></span>

- <span data-ttu-id="07437-107">Region (zachodnie stany USA, wschodnie stany USA, itp.)</span><span class="sxs-lookup"><span data-stu-id="07437-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="07437-108">Liczba skali (jedną, dwie trzy wystąpienia, itp.)</span><span class="sxs-lookup"><span data-stu-id="07437-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="07437-109">Rozmiar wystąpienia (mały, Średni, duże)</span><span class="sxs-lookup"><span data-stu-id="07437-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="07437-110">Jednostka magazynowa (Bezpłatna, Współdzielona, Podstawowa, Standardowa, Premium)</span><span class="sxs-lookup"><span data-stu-id="07437-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="07437-111">Sieci Web Apps, Mobile Apps, aplikacje interfejsu API, funkcja aplikacji (lub funkcji), w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) wszystkie działania w planie usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="07437-112">Aplikacje w tej samej subskrypcji i regionu można udostępnić plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-112">Apps in the same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="07437-113">Wszystkie aplikacje przypisane do **planu usługi aplikacji** udostępnianie zasobów zdefiniowana przez nią.</span><span class="sxs-lookup"><span data-stu-id="07437-113">All applications assigned to an **App Service plan** share the resources defined by it.</span></span> <span data-ttu-id="07437-114">Udostępnianie tego zapisuje pieniędzy odnośnie do hostowania wielu aplikacji w ramach jednego planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="07437-115">**Plan usługi App Service** może być jednostką magazynową typu **Bezpłatna**, **Współdzielona**, **Podstawowa**, **Standardowa** lub **Premium**, zapewniając dostęp do odpowiedniej liczby zasobów i funkcji.</span><span class="sxs-lookup"><span data-stu-id="07437-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span></span>

<span data-ttu-id="07437-116">Jeśli ustawiono planu usługi aplikacji **podstawowe** SKU lub nowszej, a następnie można kontrolować **rozmiar** i skalowanie liczby maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="07437-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span></span>

<span data-ttu-id="07437-117">Na przykład jeśli plan jest skonfigurowany do używania dwóch wystąpień "małe" w warstwie usług standardowa, wszystkie aplikacje, które są skojarzone z tym planem uruchamiane na obu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="07437-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="07437-118">Aplikacje mają także dostęp do funkcji warstwy standardowa usługi.</span><span class="sxs-lookup"><span data-stu-id="07437-118">Apps also have access to the standard service tier features.</span></span> <span data-ttu-id="07437-119">Wystąpieniach planu, na których działają aplikacje są pełni zarządzany i wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="07437-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07437-120">Ustawienia **Jednostka magazynowa** i **Skala** planu usługi App Service określają koszt i liczbę hostowanych w nim aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span></span>

<span data-ttu-id="07437-121">Ten artykuł opisuje klucza cechy, takie jak warstwy i skali, plan usługi aplikacji i sposób ich wchodzić w grę w aplikacji i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="07437-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="07437-122">Aplikacje i planów usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="07437-122">Apps and App Service plans</span></span>

<span data-ttu-id="07437-123">Aplikacji w usłudze App Service może być skojarzony tylko jeden plan usługi aplikacji w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="07437-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="07437-124">Aplikacjach i planów są zawarte w **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="07437-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="07437-125">Grupa zasobów służy jako granica cyklu życia dla każdego zasobu, który jest w nim.</span><span class="sxs-lookup"><span data-stu-id="07437-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="07437-126">Grupy zasobów można użyć do zarządzania ze sobą wszystkie elementy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-126">You can use resource groups to manage all the pieces of an application together.</span></span>

<span data-ttu-id="07437-127">Ponieważ pojedyncza grupa zasobów może mieć wiele planów usługi aplikacji, możesz przydzielić różnych aplikacji do różnych zasobów fizycznych.</span><span class="sxs-lookup"><span data-stu-id="07437-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span></span>

<span data-ttu-id="07437-128">Na przykład można oddzielić zasobów w środowiskach deweloperów, badanie i produkcji.</span><span class="sxs-lookup"><span data-stu-id="07437-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="07437-129">Posiadanie oddzielnego środowiska produkcyjnego i tworzenie/testowanie oprogramowania pozwala izolować zasobów.</span><span class="sxs-lookup"><span data-stu-id="07437-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="07437-130">W ten sposób obciążenia testowanie nowej wersji aplikacji nie konkurują o tych samych zasobów co aplikacji produkcyjnych, które służy rzeczywistych klientów.</span><span class="sxs-lookup"><span data-stu-id="07437-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="07437-131">Jeśli masz wiele planów w pojedynczej grupy zasobów można także zdefiniować aplikacji obejmującej regionów geograficznych.</span><span class="sxs-lookup"><span data-stu-id="07437-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="07437-132">Na przykład aplikację o wysokiej dostępności w dwóch regionach zawiera co najmniej dwa pakiety, po jednej dla każdego regionu i jeden aplikacji skojarzonej z każdego planu.</span><span class="sxs-lookup"><span data-stu-id="07437-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="07437-133">W takiej sytuacji wszystkie kopie aplikacji następnie znajdują się w pojedynczej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="07437-133">In such a situation, all the copies of the app are then contained in a single resource group.</span></span> <span data-ttu-id="07437-134">Grupy zasobów z wieloma planami i wiele aplikacji o ułatwia zarządzanie, sterowanie i wyświetlić informacje o kondycji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="07437-135">Tworzenie planu usługi App Service lub użyć istniejącego</span><span class="sxs-lookup"><span data-stu-id="07437-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="07437-136">Podczas tworzenia aplikacji, należy rozważyć utworzenie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="07437-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="07437-137">Z drugiej strony Jeśli ta aplikacja jest składnikiem większej aplikacji, utwórz je w grupie zasobów przydzielonej dla danego zastosowania większej.</span><span class="sxs-lookup"><span data-stu-id="07437-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="07437-138">Czy aplikacja jest całkowicie nowa aplikacja lub część większego, można użyć istniejącego planu hostingu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="07437-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span></span> <span data-ttu-id="07437-139">Ta decyzja jest bardziej pytanie pojemności i oczekiwane obciążenia.</span><span class="sxs-lookup"><span data-stu-id="07437-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="07437-140">Zalecamy Izolowanie aplikacji do nowej usługi aplikacji podczas planowania:</span><span class="sxs-lookup"><span data-stu-id="07437-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="07437-141">Aplikacja jest obciążający zasoby.</span><span class="sxs-lookup"><span data-stu-id="07437-141">App is resource-intensive.</span></span>
- <span data-ttu-id="07437-142">Aplikacja ma różne czynniki skalowania z innych aplikacji hostowanej w istniejącego planu.</span><span class="sxs-lookup"><span data-stu-id="07437-142">App has different scaling factors from the other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="07437-143">Aplikacja potrzebuje zasobów w innym regionie geograficznym.</span><span class="sxs-lookup"><span data-stu-id="07437-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="07437-144">W ten sposób można przydzielić nowego zestawu zasobów dla aplikacji i uzyskać większą kontrolę nad aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="07437-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="07437-145">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="07437-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="07437-146">Jeśli masz środowisko usługi aplikacji zapoznanie się z dokumentacją specyficzną dla środowiska usługi App Service w tym miejscu: [Utwórz plan usługi aplikacji w środowisku usługi aplikacji](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="07437-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="07437-147">Środowisko przeglądania planu usługi aplikacji lub w ramach tworzenia aplikacji, można utworzyć pusty plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="07437-148">W [portalu Azure](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność**, a następnie wybierz **aplikacji sieci Web** lub innego typu aplikacji usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-148">In the [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Utwórz aplikację w portalu Azure.][createWebApp]

<span data-ttu-id="07437-150">Możesz wybrać lub utworzyć plan usługi App Service dla nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-150">You can then select or create the App Service plan for the new app.</span></span>

 ![Tworzenie planu usługi aplikacji.][createASP]

<span data-ttu-id="07437-152">Aby utworzyć plan usługi aplikacji, kliknij przycisk **[+] Tworzenie nowych**, typ **planu usługi aplikacji** nazwy, a następnie wybierz odpowiedni **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="07437-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="07437-153">Kliknij przycisk **warstwa cenowa**, a następnie wybierz odpowiednią warstwę cenową dla usługi.</span><span class="sxs-lookup"><span data-stu-id="07437-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="07437-154">Wybierz **Wyświetl wszystkie** do widoku więcej cennik opcje, takie jak **wolne** i **Shared**.</span><span class="sxs-lookup"><span data-stu-id="07437-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="07437-155">Po wybraniu warstwy cenowej kliknij **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="07437-155">After you have selected the pricing tier, click the **Select** button.</span></span>

## <a name="move-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="07437-156">Przenieś aplikację do innego planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="07437-156">Move an app to a different App Service plan</span></span>

<span data-ttu-id="07437-157">Aplikację można przenieść do innego planu usługi aplikacji w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07437-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="07437-158">Aplikacje można przenosić między planami tak długo, jak plany znajdują się w tej samej grupie zasobów i region geograficzny.</span><span class="sxs-lookup"><span data-stu-id="07437-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span></span>

<span data-ttu-id="07437-159">Aby przenieść aplikację do innego planu:</span><span class="sxs-lookup"><span data-stu-id="07437-159">To move an app to another plan:</span></span>

- <span data-ttu-id="07437-160">Przejdź do aplikacji, którą chcesz przenieść.</span><span class="sxs-lookup"><span data-stu-id="07437-160">Navigate to the app that you want to move.</span></span>
- <span data-ttu-id="07437-161">W **Menu**, wyszukaj **planu usługi App Service** sekcji.</span><span class="sxs-lookup"><span data-stu-id="07437-161">In the **Menu**, look for the **App Service Plan** section.</span></span>
- <span data-ttu-id="07437-162">Wybierz **planu usługi aplikacji zmiany** do rozpoczęcia procesu.</span><span class="sxs-lookup"><span data-stu-id="07437-162">Select **Change App Service plan** to start the process.</span></span>

<span data-ttu-id="07437-163">**Zmień plan usługi aplikacji** otwiera **planu usługi aplikacji** selektora.</span><span class="sxs-lookup"><span data-stu-id="07437-163">**Change App Service plan** opens the **App Service plan** selector.</span></span> <span data-ttu-id="07437-164">W tym momencie można wybrać istniejący plan można przenieść tej aplikacji do.</span><span class="sxs-lookup"><span data-stu-id="07437-164">At this point, you can pick an existing plan to move this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07437-165">Wybierz plan usługi aplikacji interfejsu użytkownika są filtrowane według następujących kryteriów:</span><span class="sxs-lookup"><span data-stu-id="07437-165">The select App Service plan UI is filtered by the following criteria:</span></span>
> - <span data-ttu-id="07437-166">Istnieje w tej samej grupie zasobów</span><span class="sxs-lookup"><span data-stu-id="07437-166">Exists within the same Resource Group</span></span>
> - <span data-ttu-id="07437-167">Istnieje w tym samym regionie geograficznym</span><span class="sxs-lookup"><span data-stu-id="07437-167">Exists in the same Geographical Region</span></span>
> - <span data-ttu-id="07437-168">Istnieje w tej samej przestrzeni sieci Web</span><span class="sxs-lookup"><span data-stu-id="07437-168">Exists within the same Webspace</span></span>
>
> <span data-ttu-id="07437-169">Przestrzeni sieci Web jest konstrukcją logiczną, w ramach usługi aplikacji, który definiuje grupę zasobów serwera.</span><span class="sxs-lookup"><span data-stu-id="07437-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="07437-170">Region geograficzny (na przykład zachodnie stany USA) zawiera wiele Webspaces Aby przydzielić klientów korzystających z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-170">A Geographical region (such as West US) contains many Webspaces in order to allocate customers using App Service.</span></span> <span data-ttu-id="07437-171">Obecnie zasobów usługi aplikacji — nie można przenieść między Webspaces.</span><span class="sxs-lookup"><span data-stu-id="07437-171">Currently, App Service resources aren’t able to be moved between Webspaces.</span></span>
>

![Selektor planu usługi aplikacji.][change]

<span data-ttu-id="07437-173">Każdy plan ma własną warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="07437-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="07437-174">Na przykład przejście lokacji z warstwę bezpłatna do warstwy standardowa, włącza wszystkie aplikacje przypisane do korzystania z funkcji i zasoby warstwy standardowa.</span><span class="sxs-lookup"><span data-stu-id="07437-174">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span></span>

## <a name="clone-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="07437-175">Klonowanie aplikację do innego planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="07437-175">Clone an app to a different App Service plan</span></span>

<span data-ttu-id="07437-176">Jeśli chcesz przenieść aplikację w innym regionie, co alternatywa to aplikacji klonowania.</span><span class="sxs-lookup"><span data-stu-id="07437-176">If you want to move the app to a different region, one alternative is app cloning.</span></span> <span data-ttu-id="07437-177">Klonowanie tworzy kopię aplikacji w nowy lub istniejący plan usługi aplikacji w dowolnym regionie.</span><span class="sxs-lookup"><span data-stu-id="07437-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="07437-178">Można znaleźć **aplikacji w klonowania** w **narzędzi programistycznych** części menu.</span><span class="sxs-lookup"><span data-stu-id="07437-178">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07437-179">Klonowanie ma pewne ograniczenia, które możesz przeczytać temat na [klonowania aplikacji usługi aplikacji Azure przy użyciu portalu Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="07437-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="07437-180">Skalowanie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="07437-180">Scale an App Service plan</span></span>

<span data-ttu-id="07437-181">Istnieją trzy sposoby skalowanie planu:</span><span class="sxs-lookup"><span data-stu-id="07437-181">There are three ways to scale a plan:</span></span>

- <span data-ttu-id="07437-182">**Zmień plan na warstwie cenowej**.</span><span class="sxs-lookup"><span data-stu-id="07437-182">**Change the plan’s pricing tier**.</span></span> <span data-ttu-id="07437-183">Standard, a wszystkie aplikacje przypisane do niej można użyć funkcji warstwy standardowa można przekonwertować planu w warstwie podstawowej.</span><span class="sxs-lookup"><span data-stu-id="07437-183">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span></span>
- <span data-ttu-id="07437-184">**Zmień rozmiar wystąpienia planu**.</span><span class="sxs-lookup"><span data-stu-id="07437-184">**Change the plan’s instance size**.</span></span> <span data-ttu-id="07437-185">Na przykład można zmienić planu w warstwie podstawowa korzystającej z małej wystąpień do użycia dużych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="07437-185">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span></span> <span data-ttu-id="07437-186">Wszystkie aplikacje, które są skojarzone z tym planem teraz można użyć dodatkowych pamięć i zasoby Procesora, które oferuje większy rozmiar wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="07437-186">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span></span>
- <span data-ttu-id="07437-187">**Zmień liczbę wystąpień planu**.</span><span class="sxs-lookup"><span data-stu-id="07437-187">**Change the plan’s instance count**.</span></span> <span data-ttu-id="07437-188">Na przykład standardowy plan, który jest skalowana w poziomie do trzech przypadkach mogą być skalowane do 10 wystąpień.</span><span class="sxs-lookup"><span data-stu-id="07437-188">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span></span> <span data-ttu-id="07437-189">Premium plan można skalować w poziomie do 20 wystąpień (pod warunkiem dostępności).</span><span class="sxs-lookup"><span data-stu-id="07437-189">A Premium plan can be scaled out to 20 instances (subject to availability).</span></span> <span data-ttu-id="07437-190">Wszystkie aplikacje, które są skojarzone z tym planem teraz służy dodatkową pamięć i zasoby Procesora, które oferuje większej liczby wystąpień.</span><span class="sxs-lookup"><span data-stu-id="07437-190">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span></span>

<span data-ttu-id="07437-191">Cenową rozmiar warstwy i wystąpienia można zmienić, klikając **Skaluj w górę** elementu w obszarze ustawień aplikacji lub plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="07437-191">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span></span> <span data-ttu-id="07437-192">Zmiany dotyczą plan usługi aplikacji i wpływają na wszystkie aplikacje, które obsługuje.</span><span class="sxs-lookup"><span data-stu-id="07437-192">Changes apply to the App Service plan and affect all apps that it hosts.</span></span>

 ![Ustaw wartości, aby skalować aplikację.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="07437-194">Oczyszczanie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="07437-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07437-195">**Planów usługi App Service** , która ma żadnych aplikacji powiązanych z nimi nadal spowodować naliczenie opłat, ponieważ nadal zarezerwować wydajności obliczeniowej.</span><span class="sxs-lookup"><span data-stu-id="07437-195">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span></span>

<span data-ttu-id="07437-196">Aby uniknąć nieoczekiwanego opłat, po usunięciu ostatniej aplikacji hostowanej w planie usługi aplikacji, wynikowy pusty plan usługi aplikacji są także usuwane.</span><span class="sxs-lookup"><span data-stu-id="07437-196">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="07437-197">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="07437-197">Summary</span></span>

<span data-ttu-id="07437-198">Plany usług aplikacji reprezentują zestaw funkcji i możliwości, które można udostępniać między swoimi aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="07437-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="07437-199">Planów usługi aplikacji umożliwiają elastyczne do przydzielenie danej aplikacji do zestawu zasobów i dalszą optymalizację z wykorzystania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="07437-199">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="07437-200">Ten sposób, jeśli chcesz oszczędzić pieniądze na środowisku do testowania, można udostępnić plan wielu aplikacjom.</span><span class="sxs-lookup"><span data-stu-id="07437-200">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="07437-201">Można również zmaksymalizować przepustowość dla środowiska produkcyjnego skalując w wielu regionach i planów.</span><span class="sxs-lookup"><span data-stu-id="07437-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="07437-202">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="07437-202">What's changed</span></span>

- <span data-ttu-id="07437-203">Przewodnik dotyczący zmiany z witryn sieci Web w usłudze App Service, zobacz: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="07437-203">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
