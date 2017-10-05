---
title: "Interfejs użytkownika usługi Azure Mobile Engagement - Reach"
description: "Dowiedz się, jak dotrzeć do użytkowników aplikacji z powiadomień wypychanych przy użyciu usługi Azure Mobile Engagement"
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
ms.openlocfilehash: ce30456e41ff1a2f4824bcb64246ee115fdd1ef7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reach-out-to-the-users-of-your-application-with-push-notifications"></a><span data-ttu-id="65256-103">Jak dotrzeć do użytkowników aplikacji przy użyciu powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="65256-103">How to reach out to the users of your application with push notifications</span></span>
<span data-ttu-id="65256-104">W tym artykule opisano **OSIĄGNĄĆ** karcie **Mobile Engagement** portalu.</span><span class="sxs-lookup"><span data-stu-id="65256-104">This article describes the **REACH** tab of the **Mobile Engagement** portal.</span></span> <span data-ttu-id="65256-105">Możesz użyć **Mobile Engagement** portalu do monitorowania i zarządzania aplikacjami mobilnymi.</span><span class="sxs-lookup"><span data-stu-id="65256-105">You use the **Mobile Engagement** portal to monitor and manage your mobile apps.</span></span> <span data-ttu-id="65256-106">Należy pamiętać, że można uruchomić przy użyciu portalu należy najpierw utworzyć **usługi Azure Mobile Engagement** konta.</span><span class="sxs-lookup"><span data-stu-id="65256-106">Note that to start using the portal you first need to create an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="65256-107">Aby uzyskać więcej informacji, zobacz [utworzyć konto usługi Azure Mobile Engagement](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="65256-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="65256-108">Sekcja Reach interfejsu użytkownika jest wypychane kampanii narzędzie do zarządzania można utworzyć/edytowanie/aktywować/Zakończ/monitor i uzyskać statystyki kampanii obejmujących wysyłanie powiadomień wypychanych i funkcji, które są dostępne za pośrednictwem interfejsu API Reach (i niektóre elementy niski poziom Push interfejsu API) .</span><span class="sxs-lookup"><span data-stu-id="65256-108">The Reach section of the UI is the Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via the Reach API (and some elements of the low level Push API).</span></span> <span data-ttu-id="65256-109">Należy pamiętać, czy używane są interfejsy API lub interfejsu użytkownika, konieczne będzie zintegrować zarówno usługi Azure Mobile Engagement i Reach do aplikacji dla poszczególnych platform przy użyciu zestawu SDK można osiągnąć kampanii.</span><span class="sxs-lookup"><span data-stu-id="65256-109">Remember that whether you are using the APIs or the UI, you will need to integrate both Azure Mobile Engagement and Reach into your application for each platform with the SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="65256-110">Wiele sekcji **Mobile Engagement** zawierają interfejsu użytkownika portalu **Pokaż Pomoc** przycisku.</span><span class="sxs-lookup"><span data-stu-id="65256-110">Many sections of the **Mobile Engagement** portal UI contain the **SHOW HELP** button.</span></span> <span data-ttu-id="65256-111">Naciśnij ten przycisk, aby uzyskać dodatkowe informacje kontekstowe o sekcji.</span><span class="sxs-lookup"><span data-stu-id="65256-111">Press this button to get more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="65256-112">Cztery typy powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="65256-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="65256-113">Anonse — pozwalają wysyłać reklamy przez sieć do użytkowników, którzy przekierować je do innej lokalizacji w aplikacji lub w celu wysłania ich sklep poza aplikacji lub strony sieci Web.</span><span class="sxs-lookup"><span data-stu-id="65256-113">Announcements - allow you to send advertising messages to users that redirect them to another location inside your app or to send them to a webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="65256-114">Ankiety — umożliwiają zbieranie informacji od użytkowników końcowych za pośrednictwem pytań.</span><span class="sxs-lookup"><span data-stu-id="65256-114">Polls - allow you to gather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="65256-115">Wypychania danych — umożliwia wysyłanie pliku danych binarnych lub base64.</span><span class="sxs-lookup"><span data-stu-id="65256-115">Data Pushes - allow you to send a binary or base64 data file.</span></span> <span data-ttu-id="65256-116">Informacje zawarte w wypychanych danych są wysyłane do aplikacji, aby zmodyfikować bieżącego środowiska użytkowników w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65256-116">The information contained in a data push is sent to your application to modify your users' current experience in your app.</span></span> <span data-ttu-id="65256-117">Aplikacja musi być w stanie przetwarzać dane w wypychanych danych.</span><span class="sxs-lookup"><span data-stu-id="65256-117">Your application needs to be able to process the data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="65256-118">Szczegóły kampanii</span><span class="sxs-lookup"><span data-stu-id="65256-118">Campaign Details</span></span>
<span data-ttu-id="65256-119">Można edytować, klonowanie, usunąć lub aktywowania kampanii, które nie zostały jeszcze aktywowane, ustawiając kursor nad ich nazwy lub można kliknąć, aby je otworzyć.</span><span class="sxs-lookup"><span data-stu-id="65256-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="65256-120">Można sklonować kampanii, które zostały już aktywowana, ustawiając kursor nad ich nazwy lub można kliknąć, aby je otworzyć.</span><span class="sxs-lookup"><span data-stu-id="65256-120">You can clone campaigns that have already been activated by hovering over their names or you can click to open them.</span></span> <span data-ttu-id="65256-121">Jednak nie można zmienić kampanii, gdy został już aktywowany.</span><span class="sxs-lookup"><span data-stu-id="65256-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="65256-123">Osiągnąć opinii</span><span class="sxs-lookup"><span data-stu-id="65256-123">Reach Feedback</span></span>
<span data-ttu-id="65256-124">Polecenie **statystyki** Aby wyświetlić szczegóły kampanii Reach.</span><span class="sxs-lookup"><span data-stu-id="65256-124">Click on **Statistics** to see the details of a Reach campaign.</span></span> <span data-ttu-id="65256-125">**Proste** widok zawiera wizualną reprezentację w postaci wykresu słupkowego kolumny o co się stało po kampanii został aktywowany.</span><span class="sxs-lookup"><span data-stu-id="65256-125">The **Simple** view provides a visual representation in the form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="65256-126">**Zaawansowane** widoku szczegółowe bardziej szczegółowe informacje na temat kampanii wypychania.</span><span class="sxs-lookup"><span data-stu-id="65256-126">The **Advanced** view provides more granular details about the push campaign.</span></span> <span data-ttu-id="65256-127">Te informacje nie będą dostępne w przypadku wysyłania kampanii testowej tj wypychanej wysłane do urządzenia testu.</span><span class="sxs-lookup"><span data-stu-id="65256-127">These details will not be available if you are sending a test campaign i.e. a push sent to a test device.</span></span> <span data-ttu-id="65256-128">Oto, jak należy interpretować te szczegóły:</span><span class="sxs-lookup"><span data-stu-id="65256-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="65256-129">**Wypychana** — określa to liczba komunikatów wypchniętych do urządzeń.</span><span class="sxs-lookup"><span data-stu-id="65256-129">**Pushed** - This specifies the number of messages pushed to the devices.</span></span> <span data-ttu-id="65256-130">Ta liczba będzie zależeć od docelowych odbiorców określone podczas tworzenia kampanii wypychania.</span><span class="sxs-lookup"><span data-stu-id="65256-130">This number will depend on the target audience you specified while creating the push campaign.</span></span> <span data-ttu-id="65256-131">Jeśli nie określono żadnych docelowych odbiorców, następnie tego wypychane będą wysyłane do zarejestrowanych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="65256-131">If you do not specify any target audience, then this push will be sent out to all the registered devices.</span></span> <span data-ttu-id="65256-132">Podobnie jak inne usługi wypychania, firma Microsoft nie powiadomienia wypychane bezpośrednio do urządzenia, ale zamiast tego Wypchnij je do odpowiednich platform określonych usług powiadomień wypychanych (PNS - WNS-APNS/GCM) tak, aby ich dostarczenia powiadomienia do urządzeń.</span><span class="sxs-lookup"><span data-stu-id="65256-132">Like all other push services, we do not push the notifications directly to the devices but instead push them to the respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver the notifications to the devices.</span></span> 
2. <span data-ttu-id="65256-133">**Dostarczone** — określa liczbę wiadomości, które pomyślnie są dostarczane przez system powiadomień platformy na urządzeniu i potwierdzone jako odebrane przez zestaw SDK usługi Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="65256-133">**Delivered** - This specifies the number of messages which are successfully delivered by the PNS to the device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="65256-134">*Przyczyny dostarczone liczba była mniejsza niż liczba wciśnięcia:*</span><span class="sxs-lookup"><span data-stu-id="65256-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="65256-135">Jeśli użytkownik odinstalował aplikacji z urządzenia, ale systemu powiadomień platformy nie może ustalić o nim w chwili wyślemy powiadomienia wypychanego do systemu powiadomień platformy, komunikat zostanie usunięty.</span><span class="sxs-lookup"><span data-stu-id="65256-135">If the user has uninstalled the app from the device but the PNS doesn't know about it at the time we send the push to the PNS then the message will be dropped.</span></span>
   2. <span data-ttu-id="65256-136">Jeśli urządzenie jest aplikacja, ale z samymi urządzeniami były w trybie offline przez dłuższy czas, PNS zakończy się niepowodzeniem na dostarczenie wiadomości do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="65256-136">If the device has the app but the devices themselves were offline for long periods of time, then the PNS will fail to deliver the message to the device.</span></span> 
   3. <span data-ttu-id="65256-137">Jeśli dostarczenie wiadomości do urządzenia, ale zestaw Mobile Engagement SDK w aplikacji nie rozpoznaje zawartości komunikatu, jego porzuca tej wiadomości.</span><span class="sxs-lookup"><span data-stu-id="65256-137">If the message does get delivered to the device but the Mobile Engagement SDK in the app doesn’t recognize the content of the message, then it drops that message.</span></span> <span data-ttu-id="65256-138">Może to się zdarzyć, jeśli dostosowywania powiadomień w aplikacji generuje wyjątek, który mamy catch w zestawu SDK i upuszczanie wiadomości.</span><span class="sxs-lookup"><span data-stu-id="65256-138">This could happen if the customization of the notification in the app generates an exception which we catch in the SDK and drop the message.</span></span> <span data-ttu-id="65256-139">Można to także wystąpić w przypadku aplikacji na urządzeniu jest używana jest wersja zestaw Mobile Engagement SDK, który nie jest w stanie zrozumieć nowszej wersji wiadomości wypychanych wysyłane z platformy, ale jest to tylko wtedy, gdy aplikacja został uaktualniony po powiadomienia została wysłana z t Platforma service on.</span><span class="sxs-lookup"><span data-stu-id="65256-139">This could also occur if the app on the device is using a version of the Mobile Engagement SDK which is not able to understand the newer version of the push message sent from the platform but this is only when the app was upgraded after the notification was dispatched from the service platform.</span></span> <span data-ttu-id="65256-140">**Zaawansowane** kartę informuje, ile komunikatów zostały usunięte.</span><span class="sxs-lookup"><span data-stu-id="65256-140">The **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="65256-141">Na urządzeniach z systemem iOS wiadomości czasami nie dostarczenie czy albo urządzenie znajduje się na niskim poziomie naładowania baterii, czy aplikacja zużywa dużo mocy podczas przetwarzania zdalnego powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="65256-141">On iOS devices, messages sometimes do not get delivered if either the device is on low battery or if the app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="65256-142">Jest to ograniczenie urządzeń z systemem iOS.</span><span class="sxs-lookup"><span data-stu-id="65256-142">This is a limitation of the iOS devices.</span></span>   
3. <span data-ttu-id="65256-143">**Wyświetlane** — określa liczbę wiadomości, które pomyślnie zostały przedstawione dla użytkownika aplikacji na urządzeniu w formularzu systemu powiadomienia wypychane/out z — aplikacji w Centrum powiadomień lub powiadomienie w aplikacji w aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="65256-143">**Displayed** - This specifies the number of messages which are successfully shown to the app user on the device in the form of a system push/out-of-app notification in the notification center or an in-app notification within the mobile app.</span></span>  <span data-ttu-id="65256-144">**Zaawansowane** kartę informuje o ile zostały powiadomień systemowych i ile były powiadomienia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65256-144">The **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="65256-145">*Liczba powody mogą być wyświetlane jest mniejsza niż liczba dostarczone (oczekiwanie, który będzie wyświetlany)*</span><span class="sxs-lookup"><span data-stu-id="65256-145">*Reasons for Displayed count being less than Delivered count (waiting to be displayed)*</span></span>
   
   1. <span data-ttu-id="65256-146">Gdyby kampanię powiadomień datę końcową w nim następnie jest możliwe, że powiadomienie zostało dostarczone, ale po chwili pochodzi otworzyć i wyświetlić je użytkownikowi aplikacji, on już wygasł, nigdy nie została wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="65256-146">If the notification campaign had an end date on it then it is possible that the notification was delivered but when the time came to open and display it to the app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="65256-147">Jeśli powiadomienie jest powiadomienie w aplikacji, a następnie powiadomienie jest wyświetlane tylko wtedy, gdy aplikacji użytkownik otwiera aplikację.</span><span class="sxs-lookup"><span data-stu-id="65256-147">If the notification is an in-app notification then the notification is only displayed when the app user opens the app.</span></span> <span data-ttu-id="65256-148">W przypadkach, gdy użytkownik aplikacji nie otworzyła aplikacji zestaw SDK będzie zgłaszać czy powiadomienie zostało dostarczone, ale nie została jeszcze wyświetlany, dopóki otwarciu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65256-148">In cases where the app user hasn't opened the app, the SDK will report that the notification was delivered but not yet displayed until the app is opened.</span></span> 
   3. <span data-ttu-id="65256-149">Jeśli powiadomienie jest powiadomienie w aplikacji i skonfigurowane do pokazania na określone działanie/ekranu, a następnie również powiadomienia będą raportowane jako wydana, ale nie zostały jeszcze dostarczone do użytkownik otwiera aplikację na określonych ekranu.</span><span class="sxs-lookup"><span data-stu-id="65256-149">If the notification is an in-app notification and configured to be shown on a specific activity/screen then also the notification will be reported as delivered but not yet delivered until the user opens the app on a specific screen.</span></span> 
4. <span data-ttu-id="65256-150">**Interakcje użytkownika** — określa liczbę wiadomości, które ma interakcją użytkowników aplikacji z i będzie zawierać komunikaty, które są akcje lub Zakończono.</span><span class="sxs-lookup"><span data-stu-id="65256-150">**User Interactions** - This specifies the number of messages which the app user has interacted with and will include the messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="65256-151">*Użytkownik aplikacji może wykonać akcję powiadomień w jednej z następujących sposobów:*</span><span class="sxs-lookup"><span data-stu-id="65256-151">*The app user can action a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="65256-152">Jeśli powiadomienie jest powiadomienie systemu/out elementu aplikacji lub powiadomienie w aplikacji, wysyłane jako tylko do powiadomień, a następnie użytkownik aplikacji kliknie powiadomienie.</span><span class="sxs-lookup"><span data-stu-id="65256-152">If the notification is a system/out-of-app notification or an in-app notification sent as notification-only then the app user clicks on the notification.</span></span>
     2. <span data-ttu-id="65256-153">Jeśli powiadomienie jest powiadomienie w aplikacji z tekstu lub widok sieci web lub sondy aplikacji użytkownik kliknie przycisk akcji w powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="65256-153">If the notification is an in-app notification with a text or web-view or polls then the app user clicks on the Action button in the notification.</span></span>
     3. <span data-ttu-id="65256-154">Jeśli powiadomienie jest powiadomienie w aplikacji z widoku sieci web, a następnie kliknięciu aplikacji przy użyciu adresu URL sieci web tylko w widoku [Android]</span><span class="sxs-lookup"><span data-stu-id="65256-154">If the notification is an in-app notification with a web-view then the app user clicks on a URL in the web view [Android Only]</span></span>
   * <span data-ttu-id="65256-155">*Użytkownik aplikacji może wyjść powiadomień w jednej z następujących sposobów:*</span><span class="sxs-lookup"><span data-stu-id="65256-155">*The app user can exit a notification in either of the following ways:*</span></span>
     
     1. <span data-ttu-id="65256-156">Kliknięcie przycisku Zamknij powiadomienie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="65256-156">Clicking the close button on the notification directly.</span></span> 
     2. <span data-ttu-id="65256-157">Szybko przesuwając optymalizacji lub usunięcie powiadomienia.</span><span class="sxs-lookup"><span data-stu-id="65256-157">Swiping away or deleting the notification.</span></span> 
     3. <span data-ttu-id="65256-158">Powiadomienia w aplikacji przy użyciu zawartości tekstu/sieci web i sond zwykle są wyświetlane użytkownikowi aplikacji w dwóch etapach.</span><span class="sxs-lookup"><span data-stu-id="65256-158">In-app notifications with text/web content and polls are typically displayed to the app user in a two-step process.</span></span> <span data-ttu-id="65256-159">Najpierw widzą powiadomienie, a po kliknięciu na nim, zobacz temat kolejnych zawartości tekstu/sieci web/sondowania.</span><span class="sxs-lookup"><span data-stu-id="65256-159">They see a notification first and when they click on it, they see the subsequent text/web/poll content.</span></span> <span data-ttu-id="65256-160">Użytkownik aplikacji może wyjść powiadomień w jednej z następujących czynności i szczegółów w widoku Zaawansowane przechwytuje to.</span><span class="sxs-lookup"><span data-stu-id="65256-160">The app user can exit a notification in either of these steps and the details in the Advanced view captures this.</span></span> 
5. <span data-ttu-id="65256-161">**Których wykonano akcje** — to określa liczbę wiadomości, które zostały jawnie których wykonano akcje przez użytkownika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="65256-161">**Actioned** - This specifies the number of messages which were explicitly actioned by the app user.</span></span> <span data-ttu-id="65256-162">Jest to najbardziej interesujące liczba jako informuje ilu użytkowników aplikacji zostały zainteresowanych przez komunikat, który zostanie umieszczony w powiadomieniu.</span><span class="sxs-lookup"><span data-stu-id="65256-162">This is the most interesting number as this tells how many app users were interested by the message you pushed out in the notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="65256-163">W systemie iOS & Windows otwórz platformy, jeśli użytkownik ma aplikacji i kampanii został kampanii "W każdej chwili", a następnie jest możliwe, zarówno z aplikacji i powiadomienia w aplikacji są wyświetlane w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="65256-163">On iOS & Windows platforms, if the user has the app open and the campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at the same time.</span></span> <span data-ttu-id="65256-164">Może to spowodować liczbą wyświetlane wyższe niż dostarczone.</span><span class="sxs-lookup"><span data-stu-id="65256-164">This may cause a Displayed count higher than the Delivered.</span></span> <span data-ttu-id="65256-165">Jeśli użytkownik wchodzi w interakcję lub akcje powiadomienia, a następnie nawet liczba interakcji użytkownika/Actioned może być większa niż dostarczone.</span><span class="sxs-lookup"><span data-stu-id="65256-165">If the user interacts or actions the notification, then even the User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="65256-167">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="65256-167">See also</span></span>
* <span data-ttu-id="65256-168">[Pojęcia][Link 6]</span><span class="sxs-lookup"><span data-stu-id="65256-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="65256-169">[Usługa Przewodnik rozwiązywania problemów][Link 24]</span><span class="sxs-lookup"><span data-stu-id="65256-169">[Troubleshooting Guide Service][Link 24]</span></span>

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

