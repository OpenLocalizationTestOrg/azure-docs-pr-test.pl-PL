---
title: aaaAzure Mobile Engagement interfejs - Reach
description: "Dowiedz się, jak tooreach toohello użytkowników aplikacji za pomocą powiadomień wypychanych przy użyciu usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="2728a-103">Jak tooreach toohello użytkowników aplikacji za pomocą powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="2728a-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="2728a-104">W tym artykule opisano hello **OSIĄGNĄĆ** kartę hello **Mobile Engagement** portalu.</span><span class="sxs-lookup"><span data-stu-id="2728a-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="2728a-105">Użyj hello **Mobile Engagement** toomonitor portalu i zarządzania aplikacjami mobilnymi.</span><span class="sxs-lookup"><span data-stu-id="2728a-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="2728a-106">Należy pamiętać, że toostart przy użyciu portalu hello, musisz najpierw toocreate **usługi Azure Mobile Engagement** konta.</span><span class="sxs-lookup"><span data-stu-id="2728a-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="2728a-107">Aby uzyskać więcej informacji, zobacz [utworzyć konto usługi Azure Mobile Engagement](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="2728a-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="2728a-108">Hello osiągnąć sekcji powitalne interfejsu użytkownika jest hello wypychania kampanii narzędzie do zarządzania można utworzyć/edytowanie/aktywować/Zakończ/monitor i uzyskać statystyki kampanii obejmujących wysyłanie powiadomień wypychanych i funkcji, które są dostępne za pośrednictwem interfejsu API Reach hello (i niektóre elementy hello niski poziom Push interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="2728a-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="2728a-109">Należy pamiętać, że zarówno w przypadku korzystania z interfejsów API hello lub hello interfejsu użytkownika należy toointegrate zarówno usługi Azure Mobile Engagement i Reach do aplikacji dla poszczególnych platform z hello SDK przed użyciem osiągnąć kampanii.</span><span class="sxs-lookup"><span data-stu-id="2728a-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="2728a-110">Wiele sekcji hello **Mobile Engagement** interfejsu użytkownika portalu zawierają hello **Pokaż Pomoc** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2728a-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="2728a-111">Naciśnij ten przycisk tooget więcej informacje kontekstowe dotyczące sekcji.</span><span class="sxs-lookup"><span data-stu-id="2728a-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="2728a-112">Cztery typy powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="2728a-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="2728a-113">Anonse — Zezwalaj toosend toousers wiadomości reklamy, który przekierowanie tooanother położenie wewnątrz aplikację lub toosend ich tooa strony sieci Web ani do przechowywania poza aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2728a-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="2728a-114">Ankiety — Zezwalaj toogather informacji od użytkowników końcowych za pośrednictwem pytań.</span><span class="sxs-lookup"><span data-stu-id="2728a-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="2728a-115">Wypychania danych - pozwalają toosend pliku danych binarnych lub base64.</span><span class="sxs-lookup"><span data-stu-id="2728a-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="2728a-116">Witaj informacje zawarte w wypychanych danych są wysyłane toomodify aplikacji tooyour bieżącego środowiska użytkowników w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2728a-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="2728a-117">Aplikacja wymaga toobe tooprocess stanie hello danych w wypychanych danych.</span><span class="sxs-lookup"><span data-stu-id="2728a-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="2728a-118">Szczegóły kampanii</span><span class="sxs-lookup"><span data-stu-id="2728a-118">Campaign Details</span></span>
<span data-ttu-id="2728a-119">Można edytować, klonowanie, usunąć lub aktywowania kampanii, które nie zostały jeszcze aktywowane, ustawiając kursor nad ich nazwy lub kliknięciu tooopen je.</span><span class="sxs-lookup"><span data-stu-id="2728a-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="2728a-120">Można sklonować kampanii, które zostały już aktywowana, ustawiając kursor nad ich nazwy lub kliknięciu tooopen je.</span><span class="sxs-lookup"><span data-stu-id="2728a-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="2728a-121">Jednak nie można zmienić kampanii, gdy został już aktywowany.</span><span class="sxs-lookup"><span data-stu-id="2728a-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="2728a-123">Osiągnąć opinii</span><span class="sxs-lookup"><span data-stu-id="2728a-123">Reach Feedback</span></span>
<span data-ttu-id="2728a-124">Polecenie **statystyki** toosee hello szczegóły kampanii Reach.</span><span class="sxs-lookup"><span data-stu-id="2728a-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="2728a-125">Witaj **proste** widok zawiera wizualną reprezentację w postaci hello wykres słupkowy kolumny o co się stało po kampanii został aktywowany.</span><span class="sxs-lookup"><span data-stu-id="2728a-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="2728a-126">Witaj **zaawansowane** widoku szczegółowe bardziej szczegółowe informacje na temat hello wypychania kampanii.</span><span class="sxs-lookup"><span data-stu-id="2728a-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="2728a-127">Te informacje nie będą dostępne w przypadku wysyłania kampanii testowej np. urządzenie testowe wysłane tooa wypychania.</span><span class="sxs-lookup"><span data-stu-id="2728a-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="2728a-128">Oto, jak należy interpretować te szczegóły:</span><span class="sxs-lookup"><span data-stu-id="2728a-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="2728a-129">**Wypychana** — określa hello liczba komunikatów wypchniętych toohello urządzeń.</span><span class="sxs-lookup"><span data-stu-id="2728a-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="2728a-130">Ta liczba będzie zależeć od hello docelowych odbiorców określone podczas tworzenia hello wypychania kampanii.</span><span class="sxs-lookup"><span data-stu-id="2728a-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="2728a-131">Jeśli nie określono żadnych docelowych odbiorców, to wypychane będą wysyłane w tooall hello zarejestrowanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="2728a-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="2728a-132">Podobnie jak inne usługi wypychania, firma Microsoft nie hello powiadomienia wypychane bezpośrednio toohello urządzenia, ale zamiast tego wypychanie ich odpowiednich platform toohello określonych usług powiadomień wypychanych (PNS - WNS-APNS/GCM) tak, aby ich dostarczenia powiadomienia hello toohello urządzeń.</span><span class="sxs-lookup"><span data-stu-id="2728a-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="2728a-133">**Dostarczone** — określa hello liczbę wiadomości, które są pomyślnie dostarczone przez urządzenie toohello systemu powiadomień platformy hello i potwierdzone jako odebrane przez zestaw SDK usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2728a-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="2728a-134">*Przyczyny dostarczone liczba była mniejsza niż liczba wciśnięcia:*</span><span class="sxs-lookup"><span data-stu-id="2728a-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="2728a-135">Jeśli użytkownik hello odinstalował aplikacji hello z urządzenia hello, ale hello systemu powiadomień platformy nie wiesz w czasie hello wyślemy hello wypychania toohello systemu powiadomień platformy wiadomość hello zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="2728a-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="2728a-136">Jeśli urządzenie hello jest aplikacja hello, ale samymi urządzeniami hello były w trybie offline przez dłuższy czas, następnie hello systemu powiadomień platformy zakończy się niepowodzeniem urządzenia toohello wiadomość hello toodeliver.</span><span class="sxs-lookup"><span data-stu-id="2728a-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="2728a-137">Jeśli wiadomość hello dostarczenie toohello urządzenia, ale hello zestaw Mobile Engagement SDK w aplikacji hello nie rozpoznaje zawartości hello wiadomość hello, jego porzuca tej wiadomości.</span><span class="sxs-lookup"><span data-stu-id="2728a-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="2728a-138">Może to się zdarzyć, jeśli dostosowania hello hello powiadomienia w aplikacji hello generuje wyjątek, który mamy catch w wiadomość hello zestawu SDK i upuszczanie powitania.</span><span class="sxs-lookup"><span data-stu-id="2728a-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="2728a-139">Może to także wystąpić, jeśli aplikacja hello na urządzeniu hello jest przy użyciu wersji hello zestaw Mobile Engagement SDK, który nie jest możliwe toounderstand hello nowszej wersji wiadomości wypychanych hello wysyłane z platformy hello, ale jest to tylko wtedy, gdy aplikacja hello został uaktualniony po powiadomieniu hello została wysłana z hello usługi platformy.</span><span class="sxs-lookup"><span data-stu-id="2728a-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="2728a-140">Witaj **zaawansowane** kartę informuje, ile komunikatów zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="2728a-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="2728a-141">Na urządzeniach z systemem iOS wiadomości czasami nie dostarczenie albo urządzenia hello znajduje się na niskim poziomie naładowania baterii lub aplikacji hello zajmuje dużo mocy podczas przetwarzania zdalnego powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="2728a-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="2728a-142">Jest to ograniczenie hello urządzeń z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="2728a-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="2728a-143">**Wyświetlane** — określa hello liczbę wiadomości, które pomyślnie toohello aplikacji użytkownika na urządzeniu hello w postaci hello systemu powiadomienie wypychane/out z — aplikacji w Centrum powiadomień hello lub powiadomienie w aplikacji w ramach hello przenośnych aplikacja.</span><span class="sxs-lookup"><span data-stu-id="2728a-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="2728a-144">Witaj **zaawansowane** kartę informuje o ile zostały powiadomień systemowych i ile były powiadomienia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2728a-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="2728a-145">*Liczba powody mogą być wyświetlane jest mniejsza niż liczba dostarczone (wyświetlane toobe oczekiwania)*</span><span class="sxs-lookup"><span data-stu-id="2728a-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="2728a-146">Jeśli kampanię z użyciem powiadomień hello ma datę końcową w nim, a następnie jest możliwe, że hello powiadomienie zostało dostarczone, ale jeśli czas hello pochodzi tooopen i wyświetl ją toohello aplikacji użytkownika, już została usunięta, nigdy nie została wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="2728a-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="2728a-147">Jeśli powiadomienia hello jest powiadomienie w aplikacji hello powiadomień zostanie wyświetlony tylko po otwarciu użytkownika aplikacji hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="2728a-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="2728a-148">W przypadkach, gdy użytkownik aplikacji hello nie otworzyła aplikacji hello hello SDK będzie zgłaszać czy hello powiadomienie zostało dostarczone, ale nie została jeszcze wyświetlany, dopóki aplikacja hello jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="2728a-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="2728a-149">Jeśli powiadomienie hello jest powiadomienie w aplikacji i skonfigurować toobe wyświetlany na określone działanie/ekran również hello powiadomień zostanie zgłoszone jako wydana, ale nie zostały jeszcze dostarczone do hello otwarciu aplikacji hello na ekranie określonego.</span><span class="sxs-lookup"><span data-stu-id="2728a-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="2728a-150">**Interakcje użytkownika** — określa hello liczba wiadomości, który użytkownik aplikacji hello treść instrukcji i będzie zawierać wiadomości powitania, które są akcje lub Zakończono.</span><span class="sxs-lookup"><span data-stu-id="2728a-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="2728a-151">*użytkownik aplikacji Hello może wykonać akcję powiadomień w jednej z hello następujące sposoby:*</span><span class="sxs-lookup"><span data-stu-id="2728a-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="2728a-152">Jeśli hello powiadomień jest powiadomienie systemu/out elementu aplikacji lub wysyłane powiadomienie w aplikacji jako tylko do powiadomienia, hello aplikacji użytkownik kliknie powiadomienie hello.</span><span class="sxs-lookup"><span data-stu-id="2728a-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="2728a-153">Jeśli powiadomienia hello jest powiadomienie w aplikacji z tekstem lub widok sieci web lub sond następnie hello użytkownika aplikacji kliknie hello przycisku akcji hello powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="2728a-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="2728a-154">Jeśli powiadomienie o hello powiadomienie w aplikacji z widoku sieci web następnie hello kliknięć użytkowników aplikacji przy użyciu adresu URL hello sieci web tylko w widoku [Android]</span><span class="sxs-lookup"><span data-stu-id="2728a-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="2728a-155">*użytkownik aplikacji Hello może wyjść powiadomień w jednej z hello następujące sposoby:*</span><span class="sxs-lookup"><span data-stu-id="2728a-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="2728a-156">Kliknięcie przycisku Zamknij hello na powitania powiadomienia bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="2728a-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="2728a-157">Szybko przesuwając optymalizacji lub usunięcie hello powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="2728a-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="2728a-158">Powiadomienia w aplikacji z zawartością tekstu/sieci web i sond są zwykle wyświetlane toohello aplikacji użytkownika w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="2728a-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="2728a-159">Najpierw widzą powiadomienie, a po kliknięciu na nim, zobacz temat hello kolejnych zawartości tekstu/sieci web/sondowania.</span><span class="sxs-lookup"><span data-stu-id="2728a-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="2728a-160">użytkownik aplikacji Hello może wyjść powiadomień w jednej z następujących czynności i hello szczegółów w widoku Zaawansowane hello przechwytuje to.</span><span class="sxs-lookup"><span data-stu-id="2728a-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="2728a-161">**Których wykonano akcje** — określa hello liczba wiadomości, które zostały jawnie których wykonano akcje przez użytkownika aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="2728a-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="2728a-162">Jest to numer najbardziej interesujące hello informuje ilu użytkowników aplikacji zostały zainteresowanych przez wiadomość hello wypchnięty hello powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="2728a-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="2728a-163">Dla systemu iOS & platformy systemu Windows, jeśli użytkownik hello ma aplikacji hello otwarte i kampanii hello został kampanii "W każdej chwili", możliwe, zarówno z aplikacji i w aplikacji Powiadomienia są wyświetlane pod kątem hello jest tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="2728a-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="2728a-164">Może to spowodować liczbą wyświetlane wyższe niż hello dostarczone.</span><span class="sxs-lookup"><span data-stu-id="2728a-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="2728a-165">Jeśli użytkownik hello wchodzi w interakcję lub akcje hello powiadomień, następnie nawet hello Liczba interakcji użytkownika/Actioned może być większa niż dostarczone.</span><span class="sxs-lookup"><span data-stu-id="2728a-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="2728a-167">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2728a-167">See also</span></span>
* <span data-ttu-id="2728a-168">[Pojęcia][Link 6]</span><span class="sxs-lookup"><span data-stu-id="2728a-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="2728a-169">[Usługa Przewodnik rozwiązywania problemów][Link 24]</span><span class="sxs-lookup"><span data-stu-id="2728a-169">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

