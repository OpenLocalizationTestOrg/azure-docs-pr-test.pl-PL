---
title: "Interfejs użytkownika usługi Azure Mobile Engagement — segmenty"
description: "Dowiedz się, jak utworzyć i zarządzanie segmentami użytkowników w celu identyfikowania wzorców użycia za pomocą usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 087f4a1fef420abe9669f8dfe2b84c7a847ce263
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-and-manage-segments-of-users-to-identify-usage-patterns"></a><span data-ttu-id="f7b5b-103">Tworzenie i zarządzanie segmentami użytkowników w celu identyfikowania wzorców użycia</span><span class="sxs-lookup"><span data-stu-id="f7b5b-103">How to create and manage segments of users to identify usage patterns</span></span>
<span data-ttu-id="f7b5b-104">W tym artykule opisano **segmentów** karcie **Mobile Engagement** portalu.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-104">This article describes the **SEGMENTS** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="f7b5b-105">Możesz użyć **Mobile Engagement** portalu do monitorowania i zarządzania aplikacjami mobilnymi.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span>

<span data-ttu-id="f7b5b-106">Sekcja segmentów interfejsu użytkownika umożliwia pracę na podzielenie na podstawie inaczej i analizy, który można uzyskać z aplikacji i można również uzyskać dostęp za pośrednictwem interfejsu API segmentów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-106">The Segments section of the UI allows you to work on segmenting your users based on the different behavior and analytics that you can get from the application and can also access through the Segments API.</span></span> <span data-ttu-id="f7b5b-107">Segmenty najpierw są obliczane 24 godziny po ich tworzenia i są one przeliczane co 24 godziny na podstawie najnowszych informacji analizy.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on the latest analytics information.</span></span> <span data-ttu-id="f7b5b-108">Po obliczeniu segment on wyświetla "Od dnia na dzień historii" wykres każdego dnia.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-108">Once a segment is calculated, it displays a "Day to day history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="f7b5b-109">Wiele sekcji **Mobile Engagement** zawierają interfejsu użytkownika portalu **Pokaż Pomoc** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-109">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="f7b5b-110">Naciśnij ten przycisk, aby uzyskać dodatkowe informacje kontekstowe o sekcji.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-110">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="f7b5b-111">Tworzyć segmenty</span><span class="sxs-lookup"><span data-stu-id="f7b5b-111">Create Segments</span></span>
<span data-ttu-id="f7b5b-112">Można utworzyć na podstawie kryteriów maksymalnie 10 w danym okresie się do 60 dni w przeszłości z sekcji analytics segment.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-112">You can create a segment based on up to 10 criteria on a specific period up to 60 days in the past from the analytics section.</span></span> <span data-ttu-id="f7b5b-113">Na przykład można utworzyć segment oparte na osoby, które mają wyświetlać określonych stron lub wyszukiwane określonej zawartości w Twojej aplikacji w ciągu ostatnich 10 dni.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-113">For example, you can create a segment based on the people who have viewed certain pages or searched for specific content within your app within the last 10 days.</span></span> <span data-ttu-id="f7b5b-114">Te informacje są dostępne w sekcji analytics.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-114">This information is available in the analytics section.</span></span> <span data-ttu-id="f7b5b-115">Tak można go utworzyć segment, a następnie ponowne skonfigurowanie powiadomienie wypychane pod kątem tego podzbioru użytkowników można uzyskać je, aby wrócić do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-115">So, you can use it to create a segment, and then set up a push notification to target this subset of users to get them to come back to the application.</span></span> 

> [!NOTE]
> <span data-ttu-id="f7b5b-116">Po obliczeniu segmentu nie może być edytowany; można tylko sklonować (skopiowanych) lub zniszczony (usunięty).</span><span class="sxs-lookup"><span data-stu-id="f7b5b-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="f7b5b-117">W tej samej aplikacji (z tej samej AppID) można sklonować segmentu i można sklonować również do innych aplikacji (z różnych AppID).</span><span class="sxs-lookup"><span data-stu-id="f7b5b-117">A segment can be cloned within the same application (with the same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="f7b5b-119">Przykłady segmentów</span><span class="sxs-lookup"><span data-stu-id="f7b5b-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="f7b5b-121">Segmenty umożliwiają segmentu użytkowników końcowych w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-121">Segments allow you to segment the end-users of your application.</span></span>
<span data-ttu-id="f7b5b-122">Segmentacji użytkowników jest ważne strategii marketingowej.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="f7b5b-123">Usługa Azure Mobile Engagement pozwala na pobieranie danych historycznych i tworzyć segmenty niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-123">Azure Mobile Engagement allows you to get historic data and create custom segments.</span></span> <span data-ttu-id="f7b5b-124">To narzędzie zaawansowane umożliwia więcej informacji na temat obsługi klientów w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-124">This powerful tool enables you to learn about your customers’ experience in your application.</span></span> <span data-ttu-id="f7b5b-125">Można łatwo analizować segmentów i używać segmentów jako miejsca docelowe wypychania.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="f7b5b-126">Typowe przypadek użycia jest chcesz wysłać powiadomienie do zachęcić użytkowników końcowych do klasyfikowania aplikacji w magazynie wypychania.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-126">A common use-case is that you want to send a push a notification to encourage your end-users to rate your application in the store.</span></span> <span data-ttu-id="f7b5b-127">Zamiast wysyła powiadomienie do wszystkich użytkowników końcowych, można utworzyć segment, który określa tylko użytkownicy użyty aplikacji codziennie w ciągu ostatniego miesiąca i miały dużą interfejs użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-127">Rather than sending a notification to all your end-users, you can create a segment that would specify only users that have used your application every day for the last month and have had a great user experience.</span></span> <span data-ttu-id="f7b5b-128">Podczas wysyłania powiadomień wypychanych mniej, wysokiej docelowej, możesz uzyskać lepsze ROI.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-the-major-azure-mobile-engagement-elements"></a><span data-ttu-id="f7b5b-130">Segmentów, które można tworzyć oparte na elementy główne usługi Azure Mobile Engagement:</span><span class="sxs-lookup"><span data-stu-id="f7b5b-130">Segments you can create based on the major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="f7b5b-131">Zdarzenie: utworzyć segment tego cele jednego określonego zdarzenia aplikacji przypada więcej niż dwa razy w tygodniu.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-131">Event: create a segment that targets one specific event of the application that happened more than twice a week.</span></span> 
* <span data-ttu-id="f7b5b-132">Sesji: utworzenia segment użytkowników, którzy używali aplikacji więcej niż 5 razy w ostatnim tygodniu.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-132">Session: create a segment of users that have used the application more than 5 times last week.</span></span>
* <span data-ttu-id="f7b5b-133">Działania: Utwórz segment użytkowników, którzy używali jedną stronę lub zawartość większa lub mniejsza niż 10 czas ostatniego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="f7b5b-134">Zadania: Utwórz segment użytkowników, które zostały wykonane zadania więcej niż dwa razy dziennie.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="f7b5b-135">Awarii: segmentem wszystkich użytkowników, których awarii więcej niż 10 razy w ostatnim tygodniu.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-135">Crash: create a segment of all the users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="f7b5b-136">(Ten segment Przeprosiny lub nawet papieru wartościowego można push)!</span><span class="sxs-lookup"><span data-stu-id="f7b5b-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="f7b5b-137">Błąd: segmentem wszystkich użytkowników, których wystąpił błąd więcej niż 100 razy ostatnich 3 dni.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-137">Error: create a segment of all the users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="f7b5b-138">Informacje o aplikacji: utworzyć segment przeznaczonego dla niestandardowych informacji o aplikacji, które wystąpiły w ciągu ostatnich 25 dni.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-138">App Info: create a segment that targets a custom App Info that happened during the last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="f7b5b-140">Aby użyć segmentu w optymalny sposób, musisz przeprowadzić dostosowane integracji zestawu SDK w aplikacji z planem znakowania tagów "Informacje o aplikacji".</span><span class="sxs-lookup"><span data-stu-id="f7b5b-140">To use Segment in an optimal way, you must have done a customized integration of the SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="f7b5b-141">Następnie przejdź do strony głównej interfejsu, wybierz aplikację i kliknij w sekcji "Segmentów".</span><span class="sxs-lookup"><span data-stu-id="f7b5b-141">Then, go to the home page of the interface, select the application you want and click on the "Segments" section.</span></span>

1. <span data-ttu-id="f7b5b-142">Wybierz sekcję "Segmentów".</span><span class="sxs-lookup"><span data-stu-id="f7b5b-142">Select the "Segments" section.</span></span>
2. <span data-ttu-id="f7b5b-143">Kliknij przycisk "nowy segment" przycisk, aby utworzyć nowy segment.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-143">Click on the "New segment" button to create a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="f7b5b-144">Rzeczywiste życia przykład: Tworzenie prostego segmentu, na podstawie informacji "Session"</span><span class="sxs-lookup"><span data-stu-id="f7b5b-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="f7b5b-145">Segmentem wszystkich użytkowników końcowych, którzy używali aplikacji w co najmniej 50 razy w ciągu ostatniego tygodnia.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-145">Create a segment of all the end-users that have used your app at least 50 times in the last week.</span></span> <span data-ttu-id="f7b5b-146">Z tego miejsca Znajdź tylko użytkownicy końcowi, którzy poświęcony co najmniej 30 sekund w aplikacji na sesję.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-146">From there, find only the end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="f7b5b-147">Będzie to wyświetlenie wszystkich użytkowników końcowych, którzy mają pozytywne doświadczenia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-147">This will show all the end-users who have a positive experience in your app.</span></span> <span data-ttu-id="f7b5b-148">Następnie segmentu utworzone może zostać wykorzystane do zmuszenia powiadomienie dla tych użytkowników końcowych, aby zadać je, aby oceniać aplikację w magazynie.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-148">Then, the segment created could be used to push a notification to these end-users to ask them to rate your app in the store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="f7b5b-150">Nadaj nazwę segmentu, aby szybko znaleźć na liście "Segmentu".</span><span class="sxs-lookup"><span data-stu-id="f7b5b-150">Give your segment a name in order to find it quickly in the "Segment" list.</span></span>
2. <span data-ttu-id="f7b5b-151">Kliknij przycisk "Utwórz".</span><span class="sxs-lookup"><span data-stu-id="f7b5b-151">Click on the "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="f7b5b-153">Wybierz sesji.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="f7b5b-155">Wybierz okres "Ostatniego tygodnia".</span><span class="sxs-lookup"><span data-stu-id="f7b5b-155">Select the period of "Last week".</span></span>
2. <span data-ttu-id="f7b5b-156">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="f7b5b-158">Wybierz Operator, który jest odpowiedni na liście: =; ≥, ≤.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-158">Select the Operator that is relevant among the list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="f7b5b-159">Wprowadź liczbę, ma.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-159">Enter the Count you want.</span></span>
5. <span data-ttu-id="f7b5b-160">Wybierz wystąpienie ma.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-160">Select the Occurrence you want.</span></span> 
6. <span data-ttu-id="f7b5b-161">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-161">Click next.</span></span>
   <span data-ttu-id="f7b5b-162">W tym przykładzie jest ustawiona, więc w ostatnim tygodniu pasujących użytkowników, których dokonano co najmniej 50 sesji.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-162">This example is set so that over the last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="f7b5b-164">W przypadku segmentacji sesji można długości sesji jako kryterium.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-164">For the Session segmentation, you can choose the length per session as a criteria.</span></span>

1. <span data-ttu-id="f7b5b-165">Wybierz Operator, z listy.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-165">Select the Operator from the list.</span></span>
2. <span data-ttu-id="f7b5b-166">Podaj długości sesji.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-166">Provide the Length per session.</span></span>
3. <span data-ttu-id="f7b5b-167">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-167">Click Next.</span></span>
   <span data-ttu-id="f7b5b-168">W tym przykładzie mówi czy przez wszystkie sesje który zostały podzielone w sekcji wystąpienie, wybierz użytkowników, które poświęcony ponad 30 sekund na sesję.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-168">In this example, it says that over all the sessions that have been segmented on the occurrence section, select only the users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="f7b5b-170">Nazwa kryterium Aby pobrać go w pełną lejka, a następnie kliknij przycisk Zakończ.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-170">Name your criterion in order to retrieve it in the complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="f7b5b-172">Jeśli ukończono konfigurowanie kryterium, pojawi się w segmencie lejka.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-172">When you have finished setting up your criterion, it will appear in the segment funnel.</span></span>
<span data-ttu-id="f7b5b-173">Ponieważ segment jest oparta na dane analityczne, segmentów są obliczane raz dziennie.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="f7b5b-174">W tym przykładzie 47,7% całkowitej użytkownicy końcowi zgodny z kryterium.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-174">In this example, 47,7% of the total end-users matched the criterion.</span></span> <span data-ttu-id="f7b5b-175">Powinny one być użytkowników, którzy miały dobrej środowisko i będzie może zapewnić wyższy klasyfikacji, jeśli wypychanie ich powiadomienie z prośbą do klasyfikowania aplikacji w sklepie.</span><span class="sxs-lookup"><span data-stu-id="f7b5b-175">They should be the users who have had a good experience and will be likely to provide a higher rating if you push them a notification asking them to rate the app in the store.</span></span>

## <a name="see-also"></a><span data-ttu-id="f7b5b-176">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f7b5b-176">See also</span></span>
* <span data-ttu-id="f7b5b-177">[Pojęcia][Link 6]</span><span class="sxs-lookup"><span data-stu-id="f7b5b-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="f7b5b-178">[Usługa Przewodnik rozwiązywania problemów][Link 24]</span><span class="sxs-lookup"><span data-stu-id="f7b5b-178">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

