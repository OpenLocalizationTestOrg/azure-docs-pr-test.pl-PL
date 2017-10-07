---
title: Application Insights Lejki aaaAzure
description: "Dowiedz się, jak używasz toodiscover Lejki jak klienci są interakcji z aplikacją."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 3a90cfd11cb193e303136504df44008ffd04a290
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="5f964-103">Wykryj, jak klienci za pomocą aplikacji hello Lejki Insights aplikacji</span><span class="sxs-lookup"><span data-stu-id="5f964-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="5f964-104">Opis klientów są hello największe znaczenie tooyour działalności.</span><span class="sxs-lookup"><span data-stu-id="5f964-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="5f964-105">Jeśli aplikacja obejmuje kilka etapów, konieczne będzie tooknow Jeśli większość klientów postępu są przez cały proces hello lub jeśli ich kończą się proces hello w pewnym momencie.</span><span class="sxs-lookup"><span data-stu-id="5f964-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="5f964-106">postęp Hello na kolejnych czynności w aplikacji sieci web nazywa się "lejka".</span><span class="sxs-lookup"><span data-stu-id="5f964-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="5f964-107">Możesz użyć hello Application Insights Lejki toogain wgląd w użytkowników i monitor kursy wymiany krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="5f964-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="5f964-108">Rozpoczynanie pracy z bloku Lejki hello</span><span class="sxs-lookup"><span data-stu-id="5f964-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="5f964-109">Hello Najprostszym sposobem toolearn o Lejki jest toowalk, jednak w przykładzie.</span><span class="sxs-lookup"><span data-stu-id="5f964-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="5f964-110">Hello poniższych ilustracjach pokazują, że hello kroki właściciele firm handlu elektronicznego zajmie toolearn sposób interakcji klientów z aplikacją sieci web.</span><span class="sxs-lookup"><span data-stu-id="5f964-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="5f964-111">Utwórz użytkownika lejka.</span><span class="sxs-lookup"><span data-stu-id="5f964-111">Create your funnel</span></span>
<span data-ttu-id="5f964-112">Przed utworzeniem sieci lejka należy toodecide na pytanie hello ma tooanswer.</span><span class="sxs-lookup"><span data-stu-id="5f964-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="5f964-113">Na przykład można tooknow ilu użytkowników Wyświetlanie przez stronę główną, kliknij na anonsu.</span><span class="sxs-lookup"><span data-stu-id="5f964-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="5f964-114">W tym przykładzie hello właścicieli hello firmy Fabrikam Fiber mają tooknow hello odsetek klientów, którzy dokonać zakupu po dodaniu elementów tootheir koszyku podczas hello ostatniego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="5f964-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="5f964-115">Poniżej przedstawiono kroki hello podejmują toocreate ich lejka.</span><span class="sxs-lookup"><span data-stu-id="5f964-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="5f964-116">Kliknij przycisk Nowy hello na powitania Lejki bloku.</span><span class="sxs-lookup"><span data-stu-id="5f964-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="5f964-117">Wybierz przedział czasu hello "Ostatni miesiąc" z hello **zakres czasu** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="5f964-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="5f964-118">Wybierz hello **stronę produktu** zdarzenia z hello **krok 1** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="5f964-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="5f964-119">Wybierz hello **koszyka tooshopping Dodaj** zdarzenia z hello **krok 2** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="5f964-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="5f964-120">Wybierz hello **kliknij zakupu** zdarzenia z hello **kroku 3** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="5f964-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="5f964-121">Dodaj lejka toohello nazwę, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5f964-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="5f964-122">Witaj poniższej ilustracji przedstawiono generuje hello danych hello Lejki bloku.</span><span class="sxs-lookup"><span data-stu-id="5f964-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="5f964-123">Z tutaj hello właścicieli Fabrikam widoczny podczas hello ostatniego tygodnia, 22.7% dla klientów, którzy dodany element tootheir zakupy koszyka zakupu hello ukończone.</span><span class="sxs-lookup"><span data-stu-id="5f964-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="5f964-124">Można również sprawdzić 1% klientom Witaj kliknięty anonsu, aby odwiedzić stronę produktu hello i 20% klientów wylogowany po zakończeniu ich zakupu.</span><span class="sxs-lookup"><span data-stu-id="5f964-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Blok Lejki z danymi](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="5f964-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5f964-126">Next steps</span></span>
- <span data-ttu-id="5f964-127">Dowiedz się więcej o [analizy użycia](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5f964-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 
