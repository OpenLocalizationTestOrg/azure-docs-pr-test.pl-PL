---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — segmenty"
description: "Dowiedz się, jak toocreate i zarządzanie segmentami wzorców użycia tooidentify użytkowników przy użyciu usługi Azure Mobile Engagement"
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
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="e0f42-103">Jak toocreate i zarządzanie segmentami wzorców użycia tooidentify użytkowników</span><span class="sxs-lookup"><span data-stu-id="e0f42-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="e0f42-104">W tym artykule opisano hello **segmentów** kartę hello **Mobile Engagement** portalu.</span><span class="sxs-lookup"><span data-stu-id="e0f42-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="e0f42-105">Użyj hello **Mobile Engagement** toomonitor portalu i zarządzania aplikacjami mobilnymi.</span><span class="sxs-lookup"><span data-stu-id="e0f42-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="e0f42-106">sekcja segmentów Hello hello interfejsu użytkownika umożliwia toowork na segmentacji użytkowników na podstawie inaczej hello i analiz, można uzyskać z aplikacji hello przez użytkownika, który można również uzyskać dostęp za pośrednictwem hello segmentów interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e0f42-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="e0f42-107">Segmenty najpierw są obliczane 24 godziny po ich tworzenia i są one przeliczane co 24 godziny na podstawie najnowszych informacji analytics hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="e0f42-108">Po obliczeniu segment on wyświetla "Dzień tooday historii" wykres każdego dnia.</span><span class="sxs-lookup"><span data-stu-id="e0f42-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f42-109">Wiele sekcji hello **Mobile Engagement** interfejsu użytkownika portalu zawierają hello **Pokaż Pomoc** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e0f42-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="e0f42-110">Naciśnij ten przycisk tooget więcej informacje kontekstowe dotyczące sekcji.</span><span class="sxs-lookup"><span data-stu-id="e0f42-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="e0f42-111">Tworzyć segmenty</span><span class="sxs-lookup"><span data-stu-id="e0f42-111">Create Segments</span></span>
<span data-ttu-id="e0f42-112">Można utworzyć na podstawie kryteriów too10 określonego okresu się too60 dni w hello segment przeszłości z sekcji analytics hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="e0f42-113">Na przykład można utworzyć segment oparte na osoby hello wyświetlanie określonych stron lub wyszukiwane określonej zawartości w Twojej aplikacji w ramach hello ostatnich 10 dni.</span><span class="sxs-lookup"><span data-stu-id="e0f42-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="e0f42-114">Te informacje są dostępne w sekcji analytics hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="e0f42-115">Tak, można go użyć toocreate segment, a następnie ponowne skonfigurowanie tootarget powiadomień wypychanych ten podzestaw użytkowników tooget ich toocome wstecz toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0f42-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="e0f42-116">Po obliczeniu segmentu nie może być edytowany; można tylko sklonować (skopiowanych) lub zniszczony (usunięty).</span><span class="sxs-lookup"><span data-stu-id="e0f42-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="e0f42-117">W ramach hello można sklonować segmentu tej samej aplikacji (z hello tego samego AppID), i można go również sklonować do innych aplikacji (z różnych AppID).</span><span class="sxs-lookup"><span data-stu-id="e0f42-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="e0f42-119">Przykłady segmentów</span><span class="sxs-lookup"><span data-stu-id="e0f42-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="e0f42-121">Segmenty pozwalają użytkownikom końcowym hello toosegment aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0f42-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="e0f42-122">Segmentacji użytkowników jest ważne strategii marketingowej.</span><span class="sxs-lookup"><span data-stu-id="e0f42-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="e0f42-123">Usługa Azure Mobile Engagement pozwala tooget danych historycznych i tworzyć segmenty niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="e0f42-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="e0f42-124">To narzędzie zaawansowane umożliwia toolearn o obsługi klientów w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0f42-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="e0f42-125">Można łatwo analizować segmentów i używać segmentów jako miejsca docelowe wypychania.</span><span class="sxs-lookup"><span data-stu-id="e0f42-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="e0f42-126">Typowe przypadek użycia jest mają toosend tooencourage powiadomień wypychanych toorate Twojego użytkownicy końcowi aplikacji w sklepie hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="e0f42-127">Zamiast wysyłania tooall powiadomienie użytkowników końcowych, możesz utworzyć segment, który określa tylko w przypadku użytkowników, którzy używanych aplikacji codziennie dla hello ostatniego miesiąca i miały dużą interfejs użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e0f42-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="e0f42-128">Podczas wysyłania powiadomień wypychanych mniej, wysokiej docelowej, możesz uzyskać lepsze ROI.</span><span class="sxs-lookup"><span data-stu-id="e0f42-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="e0f42-130">Segmentów, które można tworzyć oparte na powitania główne elementy usługi Azure Mobile Engagement:</span><span class="sxs-lookup"><span data-stu-id="e0f42-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="e0f42-131">Zdarzenie: utworzyć segment tego cele jednego określonego zdarzenia aplikacji hello, który wystąpił więcej niż dwa razy w tygodniu.</span><span class="sxs-lookup"><span data-stu-id="e0f42-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="e0f42-132">Sesji: utworzenia segment użytkowników, którzy używali aplikacji hello więcej niż 5 razy w ostatnim tygodniu.</span><span class="sxs-lookup"><span data-stu-id="e0f42-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="e0f42-133">Działania: Utwórz segment użytkowników, którzy używali jedną stronę lub zawartość większa lub mniejsza niż 10 czas ostatniego miesiąca.</span><span class="sxs-lookup"><span data-stu-id="e0f42-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="e0f42-134">Zadania: Utwórz segment użytkowników, które zostały wykonane zadania więcej niż dwa razy dziennie.</span><span class="sxs-lookup"><span data-stu-id="e0f42-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="e0f42-135">Awarii: segmentem wszyscy użytkownicy hello, które miały awarii więcej niż 10 razy w ostatnim tygodniu.</span><span class="sxs-lookup"><span data-stu-id="e0f42-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="e0f42-136">(Ten segment Przeprosiny lub nawet papieru wartościowego można push)!</span><span class="sxs-lookup"><span data-stu-id="e0f42-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="e0f42-137">Błąd: segmentem wszyscy użytkownicy hello, które miały błąd więcej niż 100 razy ostatnich 3 dni.</span><span class="sxs-lookup"><span data-stu-id="e0f42-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="e0f42-138">Informacje o aplikacji: utworzyć segment przeznaczonego dla niestandardowych informacji o aplikacji, które wystąpiły podczas hello ostatnich dni 25.</span><span class="sxs-lookup"><span data-stu-id="e0f42-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="e0f42-140">toouse segmentu w optymalny sposób, musisz przeprowadzić dostosowane integracji hello zestawu SDK w aplikacji z planem znakowania tagów "Informacje o aplikacji".</span><span class="sxs-lookup"><span data-stu-id="e0f42-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="e0f42-141">Następnie przejdź toohello strona główna interfejsu hello, wybierz aplikacji hello i kliknij w sekcji "Segmentów" hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="e0f42-142">Wybierz sekcję "Segmentów" hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="e0f42-143">Kliknij przycisk "Nowy segment" hello przycisk toocreate nowy segment.</span><span class="sxs-lookup"><span data-stu-id="e0f42-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="e0f42-144">Rzeczywiste życia przykład: Tworzenie prostego segmentu, na podstawie informacji "Session"</span><span class="sxs-lookup"><span data-stu-id="e0f42-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="e0f42-145">Utwórz segment wszystkim użytkownikom końcowym hello, którzy używali aplikacji co najmniej 50 razy w ostatnim tygodniu hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="e0f42-146">Z tego miejsca Znajdź tylko hello użytkownicy końcowi, którzy poświęcony co najmniej 30 sekund w aplikacji na sesję.</span><span class="sxs-lookup"><span data-stu-id="e0f42-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="e0f42-147">Wyświetli wszystkim użytkownikom końcowym hello mających pozytywne doświadczenia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e0f42-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="e0f42-148">Następnie segmentu hello utworzone może być używane toopush tooask użytkownicy końcowi toothese powiadomienia ich przechowywania aplikacji w hello toorate.</span><span class="sxs-lookup"><span data-stu-id="e0f42-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="e0f42-150">Nadaj nazwę segmentu w kolejności toofind ją szybko liście hello "Segment".</span><span class="sxs-lookup"><span data-stu-id="e0f42-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="e0f42-151">Powitania kliknij przycisk "Utwórz".</span><span class="sxs-lookup"><span data-stu-id="e0f42-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="e0f42-153">Wybierz sesji.</span><span class="sxs-lookup"><span data-stu-id="e0f42-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="e0f42-155">Wybierz okres hello "W ostatnim tygodniu".</span><span class="sxs-lookup"><span data-stu-id="e0f42-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="e0f42-156">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="e0f42-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="e0f42-158">Witaj wybierz Operator, który jest odpowiedni liście hello: =; ≥, ≤.</span><span class="sxs-lookup"><span data-stu-id="e0f42-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="e0f42-159">Wprowadź hello liczba ma.</span><span class="sxs-lookup"><span data-stu-id="e0f42-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="e0f42-160">Wybierz wystąpienie ma hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="e0f42-161">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="e0f42-161">Click next.</span></span>
   <span data-ttu-id="e0f42-162">W tym przykładzie jest ustawiona, tak że over hello ostatniego tygodnia, dopasowanie użytkowników, którzy zostały wykonane co najmniej 50 sesji.</span><span class="sxs-lookup"><span data-stu-id="e0f42-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="e0f42-164">Witaj segmentacji sesji można hello długości sesji jako kryterium.</span><span class="sxs-lookup"><span data-stu-id="e0f42-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="e0f42-165">Wybierz hello operatora z listy hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="e0f42-166">Podaj hello długości sesji.</span><span class="sxs-lookup"><span data-stu-id="e0f42-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="e0f42-167">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="e0f42-167">Click Next.</span></span>
   <span data-ttu-id="e0f42-168">W tym przykładzie mówi to, że na wszystkich hello sesji, które zostały podzielone na powitania wystąpienia sekcji, wybierz tylko hello użytkowników, którzy poświęcony ponad 30 sekund na sesję.</span><span class="sxs-lookup"><span data-stu-id="e0f42-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="e0f42-170">Nazwa kryterium w kolejności tooretrieve w hello ukończyć Lejkowy, a następnie kliknij przycisk Zakończ.</span><span class="sxs-lookup"><span data-stu-id="e0f42-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="e0f42-172">Jeśli ukończono konfigurowanie kryterium, zostanie wyświetlony na powitania segmentów lejka.</span><span class="sxs-lookup"><span data-stu-id="e0f42-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="e0f42-173">Ponieważ segment jest oparta na dane analityczne, segmentów są obliczane raz dziennie.</span><span class="sxs-lookup"><span data-stu-id="e0f42-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="e0f42-174">W tym przykładzie 47,7% całkowitej użytkownicy końcowi hello dopasowane hello kryterium.</span><span class="sxs-lookup"><span data-stu-id="e0f42-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="e0f42-175">Powinny one być hello użytkowników, którzy miały dobrej środowisko i będzie można prawdopodobnie tooprovide klasyfikacji wyższej, jeśli wypychanie ich powiadomienie prośbą toorate hello aplikacji w sklepie hello.</span><span class="sxs-lookup"><span data-stu-id="e0f42-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="e0f42-176">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="e0f42-176">See also</span></span>
* <span data-ttu-id="e0f42-177">[Pojęcia][Link 6]</span><span class="sxs-lookup"><span data-stu-id="e0f42-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="e0f42-178">[Usługa Przewodnik rozwiązywania problemów][Link 24]</span><span class="sxs-lookup"><span data-stu-id="e0f42-178">[Troubleshooting Guide Service][Link 24]</span></span>

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

