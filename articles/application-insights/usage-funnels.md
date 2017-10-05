---
title: "Lejki wgląd w aplikacji Azure"
description: "Dowiedz się, jak można użyć Lejki, aby dowiedzieć się, jak klienci są interakcji z aplikacją."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 59c4dfafc102b26e3b9873f433065715f4aec9ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="d1d5e-103">Wykryj, jak klienci używają aplikacji z rozdzielaczy Application Insights</span><span class="sxs-lookup"><span data-stu-id="d1d5e-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="d1d5e-104">Opis klientów są największe znaczenie dla Twojej firmy.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="d1d5e-105">Jeśli aplikacja obejmuje kilka etapów, musisz wiedzieć, jeśli większość klientów postępu są przez cały proces lub są one zakończenia procesu w pewnym momencie.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="d1d5e-106">Przejście przez kilka czynności w aplikacji sieci web nazywa się "lejka".</span><span class="sxs-lookup"><span data-stu-id="d1d5e-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="d1d5e-107">Rozdzielaczy Application Insights umożliwia uzyskać wgląd w użytkowników i monitor kursy wymiany krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="d1d5e-108">Rozpoczynanie pracy z bloku Lejki</span><span class="sxs-lookup"><span data-stu-id="d1d5e-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="d1d5e-109">Najprostszym sposobem, aby dowiedzieć się więcej o Lejki jest przeprowadzenie jednak przykładem.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="d1d5e-110">Poniższe ilustracje wykazanie, że kroki właściciele firm handlu elektronicznego zajmie się sposób interakcji klientów z aplikacją sieci web.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="d1d5e-111">Utwórz użytkownika lejka.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-111">Create your funnel</span></span>
<span data-ttu-id="d1d5e-112">Przed utworzeniem sieci lejka należy zdecydować się na pytanie, które chcesz odpowiedzieć.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="d1d5e-113">Można na przykład wiedzieć, ilu użytkowników Wyświetlanie przez stronę główną, kliknij na anonsu.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="d1d5e-114">W tym przykładzie właściciele firmy Fabrikam Fiber zapoznać się odsetek klientów, którzy tworzą zakupu po dodaniu elementów do ich koszyk w ciągu ostatniego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="d1d5e-115">Poniżej przedstawiono kroki, które podejmują tworzenia ich lejka.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="d1d5e-116">Kliknij przycisk Nowy blok lejki.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="d1d5e-117">Wybierz przedział czasu "Ostatni miesiąc" z **zakres czasu** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="d1d5e-118">Wybierz **stronę produktu** zdarzenia z **krok 1** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="d1d5e-119">Wybierz **Dodaj do koszyka** zdarzenia z **krok 2** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="d1d5e-120">Wybierz **kliknij zakupu** zdarzenia z **kroku 3** listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="d1d5e-121">Dodaj nazwę do lejka i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="d1d5e-122">Poniższa ilustracja przedstawia się, że generuje Lejki bloku danych.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="d1d5e-123">W tym miejscu Fabrikam właścicieli widoczny w zeszłym tygodniu 22.7% dla klientów, którzy dodać element do ich koszyk ukończone zakupu.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="d1d5e-124">Można również sprawdzić 1% klientów kliknięty anonsu, aby odwiedzić stronę produktu i 20% klientów wylogowany po zakończeniu ich zakupu.</span><span class="sxs-lookup"><span data-stu-id="d1d5e-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![Blok Lejki z danymi](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="d1d5e-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d1d5e-126">Next steps</span></span>
  * [<span data-ttu-id="d1d5e-127">Przegląd wykorzystania</span><span class="sxs-lookup"><span data-stu-id="d1d5e-127">Usage overview</span></span>](app-insights-usage-overview.md)
  * [<span data-ttu-id="d1d5e-128">Użytkownikami, sesjami i zdarzenia</span><span class="sxs-lookup"><span data-stu-id="d1d5e-128">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
  * [<span data-ttu-id="d1d5e-129">Przechowywanie</span><span class="sxs-lookup"><span data-stu-id="d1d5e-129">Retention</span></span>](app-insights-usage-retention.md)
  * [<span data-ttu-id="d1d5e-130">Skoroszyty</span><span class="sxs-lookup"><span data-stu-id="d1d5e-130">Workbooks</span></span>](app-insights-usage-workbooks.md)
  * [<span data-ttu-id="d1d5e-131">Dodaj kontekstu użytkownika</span><span class="sxs-lookup"><span data-stu-id="d1d5e-131">Add user context</span></span>](app-insights-usage-send-user-context.md)
