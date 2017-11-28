---
title: "szczegółowe omówienie planów usługi aplikacji aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="04119-104">Szczegółowe omówienie planów usługi Azure App Service</span><span class="sxs-lookup"><span data-stu-id="04119-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="04119-105">Plany usług aplikacji reprezentują hello zbiór toohost fizyczne zasoby używane aplikacje.</span><span class="sxs-lookup"><span data-stu-id="04119-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="04119-106">Plany usługi App Service definiują następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="04119-106">App Service plans define:</span></span>

- <span data-ttu-id="04119-107">Region (zachodnie stany USA, wschodnie stany USA, itp.)</span><span class="sxs-lookup"><span data-stu-id="04119-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="04119-108">Liczba skali (jedną, dwie trzy wystąpienia, itp.)</span><span class="sxs-lookup"><span data-stu-id="04119-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="04119-109">Rozmiar wystąpienia (mały, Średni, duże)</span><span class="sxs-lookup"><span data-stu-id="04119-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="04119-110">Jednostka magazynowa (Bezpłatna, Współdzielona, Podstawowa, Standardowa, Premium)</span><span class="sxs-lookup"><span data-stu-id="04119-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="04119-111">Sieci Web Apps, Mobile Apps, aplikacje interfejsu API, funkcja aplikacji (lub funkcji), w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) wszystkie działania w planie usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04119-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="04119-112">Aplikacje w hello tej samej subskrypcji i regionu można udostępniać plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04119-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="04119-113">Wszystkie aplikacje przypisane tooan **planu usługi aplikacji** udostępnianie zasobów hello zdefiniowana przez nią.</span><span class="sxs-lookup"><span data-stu-id="04119-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="04119-114">Udostępnianie tego zapisuje pieniędzy odnośnie do hostowania wielu aplikacji w ramach jednego planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04119-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="04119-115">Twoje **planu usługi aplikacji** można skalować z **wolne** i **Shared** jednostki SKU zbyt**podstawowe**, **standardowe**, i **Premium** jednostki SKU, umożliwiając dostęp do zasobów toomore i funkcje wzdłuż hello sposób.</span><span class="sxs-lookup"><span data-stu-id="04119-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="04119-116">Jeśli plan usługi aplikacji jest ustawiona zbyt**podstawowe** SKU lub nowszej, a następnie można kontrolować hello **rozmiar** i skalować liczbę hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="04119-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="04119-117">Na przykład jeśli plan jest skonfigurowany toouse dwa wystąpienia "małe" w warstwie usług standardowa na powitania, wszystkie aplikacje, które są skojarzone z tym planem uruchamiane na obu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="04119-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="04119-118">Aplikacje mają również funkcje warstwy standardowa usługa toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="04119-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="04119-119">Wystąpieniach planu, na których działają aplikacje są pełni zarządzany i wysokiej dostępności.</span><span class="sxs-lookup"><span data-stu-id="04119-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04119-120">Witaj **SKU** i **skali** z usługi aplikacji hello plan określa hello kosztów i nie hello liczbę aplikacje znajdujące się w nim.</span><span class="sxs-lookup"><span data-stu-id="04119-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="04119-121">Ten artykuł opisuje hello właściwości klucza, takie jak warstwy i skali plan usługi aplikacji i sposób ich wchodzić w grę w aplikacji i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="04119-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="04119-122">Aplikacje i planów usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="04119-122">Apps and App Service plans</span></span>

<span data-ttu-id="04119-123">Aplikacji w usłudze App Service może być skojarzony tylko jeden plan usługi aplikacji w danym momencie.</span><span class="sxs-lookup"><span data-stu-id="04119-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="04119-124">Aplikacjach i planów są zawarte w **grupy zasobów**.</span><span class="sxs-lookup"><span data-stu-id="04119-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="04119-125">Grupa zasobów służy jako hello cyklu życia granic dla każdego zasobu, który jest w nim.</span><span class="sxs-lookup"><span data-stu-id="04119-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="04119-126">Możesz użyć toomanage grup zasobów wszystkich elementów hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04119-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="04119-127">Ponieważ pojedyncza grupa zasobów może mieć wiele planów usługi aplikacji, możesz przydzielić różnych aplikacji toodifferent zasobów fizycznych.</span><span class="sxs-lookup"><span data-stu-id="04119-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="04119-128">Na przykład można oddzielić zasobów w środowiskach deweloperów, badanie i produkcji.</span><span class="sxs-lookup"><span data-stu-id="04119-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="04119-129">Posiadanie oddzielnego środowiska produkcyjnego i tworzenie/testowanie oprogramowania pozwala izolować zasobów.</span><span class="sxs-lookup"><span data-stu-id="04119-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="04119-130">W ten sposób obciążenia testowanie nowej wersji aplikacji nie konkurują o hello samo zasobów co aplikacji produkcyjnych, które służy rzeczywistych klientów.</span><span class="sxs-lookup"><span data-stu-id="04119-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="04119-131">Jeśli masz wiele planów w pojedynczej grupy zasobów można także zdefiniować aplikacji obejmującej regionów geograficznych.</span><span class="sxs-lookup"><span data-stu-id="04119-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="04119-132">Na przykład aplikację o wysokiej dostępności w dwóch regionach zawiera co najmniej dwa pakiety, po jednej dla każdego regionu i jeden aplikacji skojarzonej z każdego planu.</span><span class="sxs-lookup"><span data-stu-id="04119-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="04119-133">W takiej sytuacji wszystkie kopie hello aplikacji hello następnie znajdują się w pojedynczej grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="04119-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="04119-134">Dostępność grupy zasobów z wieloma planami i wielu aplikacji, ułatwia toomanage łatwe, sterowania i Wyświetl kondycję hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="04119-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="04119-135">Tworzenie planu usługi App Service lub użyć istniejącego</span><span class="sxs-lookup"><span data-stu-id="04119-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="04119-136">Podczas tworzenia aplikacji, należy rozważyć utworzenie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="04119-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="04119-137">Na powitania drugiej strony, jeśli ta aplikacja jest składnikiem większej aplikacji, utwórz go w grupie zasobów hello przydzielonej do większych aplikację.</span><span class="sxs-lookup"><span data-stu-id="04119-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="04119-138">Czy aplikacja hello jest całkowicie nowa aplikacja lub część większego, możesz wybrać toouse istniejących toohost planu go lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="04119-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="04119-139">Ta decyzja jest bardziej pytanie pojemności i oczekiwane obciążenia.</span><span class="sxs-lookup"><span data-stu-id="04119-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="04119-140">Zalecamy Izolowanie aplikacji do nowej usługi aplikacji podczas planowania:</span><span class="sxs-lookup"><span data-stu-id="04119-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="04119-141">Aplikacja jest obciążający zasoby.</span><span class="sxs-lookup"><span data-stu-id="04119-141">App is resource-intensive.</span></span>
- <span data-ttu-id="04119-142">Aplikacja ma różne czynniki skalowania z hello innych aplikacji hostowanej w istniejącego planu.</span><span class="sxs-lookup"><span data-stu-id="04119-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="04119-143">Aplikacja potrzebuje zasobów w innym regionie geograficznym.</span><span class="sxs-lookup"><span data-stu-id="04119-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="04119-144">W ten sposób można przydzielić nowego zestawu zasobów dla aplikacji i uzyskać większą kontrolę nad aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="04119-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="04119-145">Tworzenie planu usługi App Service</span><span class="sxs-lookup"><span data-stu-id="04119-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="04119-146">Jeśli masz środowisko usługi aplikacji, można przejrzeć hello dokumentacji określonych tooApp środowiska usługi tutaj: [Utwórz plan usługi aplikacji w środowisku usługi aplikacji](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="04119-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="04119-147">Można utworzyć pusty plan usługi aplikacji, z hello środowisko przeglądania planu usługi aplikacji lub w ramach tworzenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04119-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="04119-148">W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność**, a następnie wybierz **aplikacji sieci Web** lub innego typu aplikacji usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04119-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Tworzenie aplikacji w hello portalu Azure.][createWebApp]

<span data-ttu-id="04119-150">Można następnie wybrać lub utworzyć hello planu usługi App Service dla nowej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="04119-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![Tworzenie planu usługi aplikacji.][createASP]

<span data-ttu-id="04119-152">Kliknij toocreate plan usługi aplikacji **[+] Utwórz nowy**, hello typu **planu usługi aplikacji** nazwy, a następnie wybierz odpowiedni **lokalizacji**.</span><span class="sxs-lookup"><span data-stu-id="04119-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="04119-153">Kliknij przycisk **warstwa cenowa**, a następnie wybierz odpowiednią warstwę cenową dla usługi hello.</span><span class="sxs-lookup"><span data-stu-id="04119-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="04119-154">Wybierz **Wyświetl wszystkie** tooview więcej cennik opcje, takie jak **wolne** i **Shared**.</span><span class="sxs-lookup"><span data-stu-id="04119-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="04119-155">Po wybraniu warstwy cenowej powitania kliknij hello **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="04119-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="04119-156">Przenoszenie aplikacji tooa inny plan usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="04119-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="04119-157">Można przenosić aplikacji tooa inny plan usługi aplikacji hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="04119-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="04119-158">Aplikacje można przenosić między planami tak długo, jak plany hello znajdują się w hello tej samej grupie zasobów i region geograficzny.</span><span class="sxs-lookup"><span data-stu-id="04119-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="04119-159">toomove plan tooanother aplikacji:</span><span class="sxs-lookup"><span data-stu-id="04119-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="04119-160">Przejdź toohello aplikacji, które mają toomove.</span><span class="sxs-lookup"><span data-stu-id="04119-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="04119-161">W hello **Menu**, wyszukaj hello **planu usługi App Service** sekcji.</span><span class="sxs-lookup"><span data-stu-id="04119-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="04119-162">Wybierz **planu usługi aplikacji zmiany** toostart hello procesu.</span><span class="sxs-lookup"><span data-stu-id="04119-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="04119-163">**Zmień plan usługi aplikacji** hello otwiera **planu usługi aplikacji** selektora.</span><span class="sxs-lookup"><span data-stu-id="04119-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="04119-164">W tym momencie można wybrać istniejący plan toomove tej aplikacji do.</span><span class="sxs-lookup"><span data-stu-id="04119-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04119-165">Wybierz plan usługi aplikacji Hello interfejsu użytkownika są filtrowane według hello następujące kryteria:</span><span class="sxs-lookup"><span data-stu-id="04119-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="04119-166">Istnieje w ramach hello same grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="04119-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="04119-167">Istnieje w hello sam Region geograficzny</span><span class="sxs-lookup"><span data-stu-id="04119-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="04119-168">Istnieje w ramach hello sam przestrzeni sieci Web</span><span class="sxs-lookup"><span data-stu-id="04119-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="04119-169">Przestrzeni sieci Web jest konstrukcją logiczną, w ramach usługi aplikacji, który definiuje grupę zasobów serwera.</span><span class="sxs-lookup"><span data-stu-id="04119-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="04119-170">Region geograficzny (na przykład zachodnie stany USA) zawiera wiele Webspaces w kolejności tooallocate klientów korzystających z usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04119-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="04119-171">Obecnie zasobów usługi aplikacji nie są toobe można przenosić między Webspaces.</span><span class="sxs-lookup"><span data-stu-id="04119-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![Selektor planu usługi aplikacji.][change]

<span data-ttu-id="04119-173">Każdy plan ma własną warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="04119-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="04119-174">Umożliwia przenoszenie lokacji z warstwy standardowej tooa warstwę bezpłatna, na przykład wszystkie aplikacje przypisane tooit toouse hello funkcje i zasoby hello warstwy standardowa.</span><span class="sxs-lookup"><span data-stu-id="04119-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="04119-175">Klonowanie aplikacji tooa inny plan usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="04119-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="04119-176">Jeśli chcesz toomove hello aplikacji tooa innym regionie, co alternatywa to aplikacji klonowania.</span><span class="sxs-lookup"><span data-stu-id="04119-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="04119-177">Klonowanie tworzy kopię aplikacji w nowy lub istniejący plan usługi aplikacji w dowolnym regionie.</span><span class="sxs-lookup"><span data-stu-id="04119-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="04119-178">Można znaleźć **aplikacji w klonowania** w hello **narzędzi programistycznych** część hello menu.</span><span class="sxs-lookup"><span data-stu-id="04119-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04119-179">Klonowanie ma pewne ograniczenia, które możesz przeczytać temat na [klonowania aplikacji usługi aplikacji Azure przy użyciu portalu Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="04119-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="04119-180">Skalowanie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="04119-180">Scale an App Service plan</span></span>

<span data-ttu-id="04119-181">Istnieją trzy sposoby tooscale plan:</span><span class="sxs-lookup"><span data-stu-id="04119-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="04119-182">**Zmiany planu hello do warstwy cenowej**.</span><span class="sxs-lookup"><span data-stu-id="04119-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="04119-183">Planu w warstwie podstawowa hello może być przekonwertowany tooStandard i wszystkie aplikacje przypisane tooit toouse funkcje hello hello warstwy standardowa.</span><span class="sxs-lookup"><span data-stu-id="04119-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="04119-184">**Zmień rozmiar wystąpienia planu hello**.</span><span class="sxs-lookup"><span data-stu-id="04119-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="04119-185">Na przykład planu w warstwie podstawowa hello korzystającej z małej wystąpień może być zmienione toouse dużych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="04119-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="04119-186">Wszystkie aplikacje, które są skojarzone z tym planem teraz można używać hello dodatkową pamięć i zasoby Procesora, które hello większych oferty rozmiar wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="04119-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="04119-187">**Zmiana liczby wystąpień w planie hello**.</span><span class="sxs-lookup"><span data-stu-id="04119-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="04119-188">Na przykład standardowy plan, który jest skalowana w poziomie toothree wystąpień może być skalowana too10 wystąpień.</span><span class="sxs-lookup"><span data-stu-id="04119-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="04119-189">Premium plan można skalować w poziomie too20 wystąpień (tooavailability podmiotu).</span><span class="sxs-lookup"><span data-stu-id="04119-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="04119-190">Wszystkie aplikacje, które są skojarzone z tym planem teraz można używać hello dodatkową pamięć i zasoby Procesora, które hello większych oferty liczba wystąpień.</span><span class="sxs-lookup"><span data-stu-id="04119-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="04119-191">Możesz zmienić hello cennik rozmiar warstwy i wystąpienia, klikając hello **Skaluj w górę** elementu w obszarze Ustawienia aplikacji hello lub hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="04119-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="04119-192">Zmiany zastosować toohello planu usługi aplikacji i wpływają na wszystkie aplikacje, które obsługuje.</span><span class="sxs-lookup"><span data-stu-id="04119-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![Ustaw wartości tooscale zapasowej aplikacji.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="04119-194">Oczyszczanie planu usługi aplikacji</span><span class="sxs-lookup"><span data-stu-id="04119-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="04119-195">**Planów usługi App Service** nie toothem aplikacji skojarzonych z nadal spowodować naliczenie opłat, ponieważ nadal wydajności obliczeniowej hello tooreserve, która ma.</span><span class="sxs-lookup"><span data-stu-id="04119-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="04119-196">tooavoid nieoczekiwany opłat, po usunięciu aplikacji ostatniego hello hostowanej w planie usługi aplikacji hello wynikowy pusta planu usługi aplikacji są także usuwane.</span><span class="sxs-lookup"><span data-stu-id="04119-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="04119-197">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="04119-197">Summary</span></span>

<span data-ttu-id="04119-198">Plany usług aplikacji reprezentują zestaw funkcji i możliwości, które można udostępniać między swoimi aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="04119-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="04119-199">Planów usługi App Service zapewnia hello elastyczność tooallocate określonych aplikacji tooa zestawu zasobów i dalszą optymalizację z wykorzystania zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="04119-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="04119-200">W ten sposób Jeśli chcesz toosave pieniądze na środowisku do testowania, można udostępnić plan wielu aplikacjom.</span><span class="sxs-lookup"><span data-stu-id="04119-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="04119-201">Można również zmaksymalizować przepustowość dla środowiska produkcyjnego skalując w wielu regionach i planów.</span><span class="sxs-lookup"><span data-stu-id="04119-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="04119-202">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="04119-202">What's changed</span></span>

- <span data-ttu-id="04119-203">Przewodnik toohello zmian z tooApp witryn sieci Web Service, zobacz: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="04119-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
