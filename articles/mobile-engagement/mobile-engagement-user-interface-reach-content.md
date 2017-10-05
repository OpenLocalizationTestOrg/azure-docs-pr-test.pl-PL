---
title: "Interfejs użytkownika usługi Azure Mobile Engagement - Reach zawartości"
description: "Informacje o sposobie zarządzania zawartością unikatowy różnych typów kampanii obejmujących wysyłanie powiadomień wypychanych w usłudze Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3741a43b74af5846e95e42d8a7b533621e780f2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-the-unique-content-of-the-different-types-of-push-notification-campaigns"></a><span data-ttu-id="a1feb-103">Jak zarządzać unikatową zawartość różnych typów kampanii obejmujących wysyłanie powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="a1feb-103">How to manage the unique content of the different types of push notification campaigns</span></span>
<span data-ttu-id="a1feb-104">Sekcji zawartości nową kampanię reach służy do zmiany zawartości anonse, ankiety, dane wypychane i Kafelki (tylko Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="a1feb-104">You can use the Content section of a new reach campaign to modify the content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="a1feb-105">Ustawienie zawartości kampanie wypychania jest specyficzne dla typu kampanii.</span><span class="sxs-lookup"><span data-stu-id="a1feb-105">The content setting of Push campaigns is specific to the type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="a1feb-106">Typy zawartości:</span><span class="sxs-lookup"><span data-stu-id="a1feb-106">Content types:</span></span>
* <span data-ttu-id="a1feb-107">Anonse</span><span class="sxs-lookup"><span data-stu-id="a1feb-107">Announcements</span></span>
* <span data-ttu-id="a1feb-108">Ankiety</span><span class="sxs-lookup"><span data-stu-id="a1feb-108">Polls</span></span>
* <span data-ttu-id="a1feb-109">Wypychania danych</span><span class="sxs-lookup"><span data-stu-id="a1feb-109">Data pushes</span></span>
* <span data-ttu-id="a1feb-110">Kafelki (tylko Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="a1feb-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="a1feb-111">Zawartość anonsów</span><span class="sxs-lookup"><span data-stu-id="a1feb-111">Content of Announcements</span></span>
 ![Reach Content1][30] 

### <a name="choose-the-type-of-your-announcement"></a><span data-ttu-id="a1feb-113">Wybierz typ anonsu:</span><span class="sxs-lookup"><span data-stu-id="a1feb-113">Choose the type of your announcement:</span></span>
* <span data-ttu-id="a1feb-114">Tylko powiadomienie: jest proste powiadomień w wersji standard.</span><span class="sxs-lookup"><span data-stu-id="a1feb-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="a1feb-115">Oznacza to, że jeśli użytkownik go kliknie, bez dodatkowego widoku będą wyświetlane, ale zostanie przeprowadzona tylko akcję skojarzoną do niego.</span><span class="sxs-lookup"><span data-stu-id="a1feb-115">Meaning that if a user clicks on it, no additional view will appear, but only the action associated to it will occur.</span></span>
* <span data-ttu-id="a1feb-116">Tekst anonsu: to powiadomienie, które angażujący użytkownikowi przyjrzeć widoku tekstu.</span><span class="sxs-lookup"><span data-stu-id="a1feb-116">Text announcement: It is a notification that engages the user to have a look at a text view.</span></span>
* <span data-ttu-id="a1feb-117">Sieci Web anonsu: to powiadomienie, które angażujący użytkownikowi przyjrzeć widoku sieci web.</span><span class="sxs-lookup"><span data-stu-id="a1feb-117">Web announcement: It is a notification that engages the user to have a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="a1feb-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a1feb-118">See also</span></span>
* <span data-ttu-id="a1feb-119">[Osiągnąć — jak OT - anonsów][Link 3]</span><span class="sxs-lookup"><span data-stu-id="a1feb-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="a1feb-120">O anonsach widoku sieci Web:</span><span class="sxs-lookup"><span data-stu-id="a1feb-120">About Web View Announcements:</span></span>
<span data-ttu-id="a1feb-121">Wystąpienia wzorca "{deviceid}" w kodzie HTML lub kod JavaScript, podana tutaj będą automatycznie zastępowane identyfikatorem urządzenia wyświetlającego anons.</span><span class="sxs-lookup"><span data-stu-id="a1feb-121">Occurrences of the pattern "{deviceid}" in the HTML code or JavaScript code you provide here will be automatically replaced by the identifier of the device displaying the announcement.</span></span> <span data-ttu-id="a1feb-122">Jest to prosty sposób pobierać identyfikatory urządzeń usługi Azure Mobile Engagement w zewnętrznej usłudze sieci web hostowanej na zapleczu biura.</span><span class="sxs-lookup"><span data-stu-id="a1feb-122">This is an easy way to retrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="a1feb-123">Jeśli chcesz utworzyć pełnoekranowy widok sieci Web (bez domyślnych przycisków akcji i wyjścia), możesz użyć następujących funkcji z kodu JavaScript anonsu widoku sieci Web:</span><span class="sxs-lookup"><span data-stu-id="a1feb-123">If you want to create a full screen web view (without the default Action and Exit buttons we provide) you can use the following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="a1feb-124">Wykonaj akcję anonsu: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="a1feb-124">perform the announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="a1feb-125">Wyjdź z anonsu: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="a1feb-125">exit from the announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="a1feb-126">Wybierz akcję:</span><span class="sxs-lookup"><span data-stu-id="a1feb-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="a1feb-127">O adresach URL akcji:</span><span class="sxs-lookup"><span data-stu-id="a1feb-127">About Action URLs:</span></span>
<span data-ttu-id="a1feb-128">Każdy adres URL, który może zostać zinterpretowany przez system operacyjny urządzenia docelowego, może być używany jako adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="a1feb-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="a1feb-129">Każdy dedykowany adres URL obsługiwany przez aplikację (np. umożliwiający użytkownikowi przejście do konkretnego ekranu) również może być używany jako adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="a1feb-129">Any dedicated URL that your application might support (e.g. to make users jump to a particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="a1feb-130">Każde wystąpienie wzorca {deviceid} jest automatycznie zastępowane identyfikatorem urządzenia wykonującego akcję.</span><span class="sxs-lookup"><span data-stu-id="a1feb-130">Each occurrence of the {deviceid} pattern is automatically replaced by the identifier of the device performing the action.</span></span> <span data-ttu-id="a1feb-131">To można łatwo pobierać identyfikatory urządzeń usługi Azure Mobile Engagement za pomocą zewnętrznej usługi sieci web hostowanej na zapleczu biura.</span><span class="sxs-lookup"><span data-stu-id="a1feb-131">This can be used to easily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="a1feb-132">**Android i iOS akcje**</span><span class="sxs-lookup"><span data-stu-id="a1feb-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="a1feb-133">Otwórz stronę sieci web</span><span class="sxs-lookup"><span data-stu-id="a1feb-133">Open a web page</span></span>
  * <span data-ttu-id="a1feb-134">http://\[domeny w przypadku witryny sieci web\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="a1feb-135">Przykład: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="a1feb-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="a1feb-136">Wyślij wiadomość e-mail</span><span class="sxs-lookup"><span data-stu-id="a1feb-136">Send an e-mail</span></span>
  * <span data-ttu-id="a1feb-137">mailto:\[e-mail poczty e-mail odbiorcy\]? podmiotu =\[podmiotu\]& body =\[wiadomości\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="a1feb-138">Example:mailto:foo@example.com? podmiotu = pozdrowienia % 20from % 20Azure % 20Mobile % 20Engagement! & body = 20stuff dobrej %!</span><span class="sxs-lookup"><span data-stu-id="a1feb-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="a1feb-139">Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="a1feb-139">Send a SMS</span></span>
  * <span data-ttu-id="a1feb-140">SMS:\[numer telefonu\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="a1feb-141">Przykład: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="a1feb-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="a1feb-142">Wybierz numer telefonu</span><span class="sxs-lookup"><span data-stu-id="a1feb-142">Dial a phone number</span></span>
  * <span data-ttu-id="a1feb-143">Tel.:\[numer telefonu\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="a1feb-144">Przykład: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="a1feb-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="a1feb-145">**Android tylko akcje**</span><span class="sxs-lookup"><span data-stu-id="a1feb-145">**Android only actions**</span></span>
  * <span data-ttu-id="a1feb-146">Pobierz aplikację ze sklepu Play</span><span class="sxs-lookup"><span data-stu-id="a1feb-146">Download an application on the Play Store</span></span>
  * <span data-ttu-id="a1feb-147">Market://details?ID=\[pakiet aplikacji\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="a1feb-148">Przykład: market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="a1feb-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="a1feb-149">Rozpocznij wyszukiwanie z określoną lokalizacją geograficzną</span><span class="sxs-lookup"><span data-stu-id="a1feb-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="a1feb-150">Geo:0, 0? q =\[zapytania wyszukiwania\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="a1feb-151">Przykład: geo:0, 0? q = starbucks, Paryża</span><span class="sxs-lookup"><span data-stu-id="a1feb-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="a1feb-152">**tylko akcje dla systemu iOS**</span><span class="sxs-lookup"><span data-stu-id="a1feb-152">**iOS only actions**</span></span>
  * <span data-ttu-id="a1feb-153">Pobierz aplikację ze sklepu App Store</span><span class="sxs-lookup"><span data-stu-id="a1feb-153">Download an application on the App Store</span></span>
  * <span data-ttu-id="a1feb-154">http://iTunes.Apple.com/ [Kraj] /app/ [Nazwa aplikacji] /id [identyfikator aplikacji]? mt = 8</span><span class="sxs-lookup"><span data-stu-id="a1feb-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="a1feb-155">Przykład: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="a1feb-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="a1feb-156">Akcje systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a1feb-156">Windows Actions</span></span>
  * <span data-ttu-id="a1feb-157">Otwórz stronę sieci web</span><span class="sxs-lookup"><span data-stu-id="a1feb-157">Open a web page</span></span>
  * <span data-ttu-id="a1feb-158">http://\[domeny w przypadku witryny sieci web\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="a1feb-159">Przykład: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="a1feb-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="a1feb-160">Wyślij wiadomość e-mail</span><span class="sxs-lookup"><span data-stu-id="a1feb-160">Send an e-mail</span></span>
  * <span data-ttu-id="a1feb-161">mailto:\[e-mail poczty e-mail odbiorcy\]? podmiotu =\[podmiotu\]& body =\[wiadomości\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="a1feb-162">Example:mailto:foo@example.com? podmiotu = pozdrowienia % 20from % 20Azure % 20Mobile % 20Engagement! & body = 20stuff dobrej %!</span><span class="sxs-lookup"><span data-stu-id="a1feb-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="a1feb-163">Wyślij wiadomość SMS (wymagana jest aplikacja Skype ze Sklepu)</span><span class="sxs-lookup"><span data-stu-id="a1feb-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="a1feb-164">SMS:\[numer telefonu\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="a1feb-165">Przykład: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="a1feb-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="a1feb-166">Wybierz numer telefonu (wymagana jest aplikacja Skype ze Sklepu)</span><span class="sxs-lookup"><span data-stu-id="a1feb-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="a1feb-167">Tel.:\[numer telefonu\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="a1feb-168">Przykład: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="a1feb-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="a1feb-169">Pobierz aplikację ze sklepu Play</span><span class="sxs-lookup"><span data-stu-id="a1feb-169">Download an application on the Play Store</span></span>
  * <span data-ttu-id="a1feb-170">MS-windows-magazynu: strony szczegółów projektu? PFN =\[identyfikator pakietu aplikacji\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="a1feb-171">Przykład: ms-windows-magazynu: strony szczegółów projektu? PFN = 4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="a1feb-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="a1feb-172">Rozpocznij wyszukiwanie na mapach Bing</span><span class="sxs-lookup"><span data-stu-id="a1feb-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="a1feb-173">bingmaps:? q =\[zapytania wyszukiwania\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="a1feb-174">Przykład: bingmaps:? q = starbucks, Paryża</span><span class="sxs-lookup"><span data-stu-id="a1feb-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="a1feb-175">Użyj schematu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="a1feb-175">Use a custom scheme</span></span>
  * <span data-ttu-id="a1feb-176">\[schemat niestandardowy\]://\[parametry schematu niestandardowego\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="a1feb-177">Przykład: myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="a1feb-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="a1feb-178">Użyj danych pakietu (w sklepie dla rozszerzenia odczytu wymagane)</span><span class="sxs-lookup"><span data-stu-id="a1feb-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="a1feb-179">\[folder\]\[danych\].\[ rozszerzenia\]</span><span class="sxs-lookup"><span data-stu-id="a1feb-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="a1feb-180">Example:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="a1feb-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="a1feb-181">Utwórz adres URL śledzenia:</span><span class="sxs-lookup"><span data-stu-id="a1feb-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="a1feb-182">Zobacz sekcję "Ustawienia" <UI Documentation> dla instrukcji na temat budowania adres URL śledzenia, który pozwoli użytkownikom na pobranie jednej z innych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a1feb-182">See the “Settings” section of the <UI Documentation> for instruction on building a tracking URL that will allow users to download one of your other applications.</span></span>

### <a name="define-the-texts-of-your-announcement"></a><span data-ttu-id="a1feb-183">Zdefiniuj teksty anonsu</span><span class="sxs-lookup"><span data-stu-id="a1feb-183">Define the texts of your announcement</span></span>
<span data-ttu-id="a1feb-184">Wprowadź tytuł, zawartość i przycisk teksty anonsu.</span><span class="sxs-lookup"><span data-stu-id="a1feb-184">Fill in the title, content, and button texts of your announcement.</span></span> <span data-ttu-id="a1feb-185">Możesz zastosować odbiorców przyszłych kampanii na podstawie opinii reach o jak użytkownicy odpowiedzi kampanii.</span><span class="sxs-lookup"><span data-stu-id="a1feb-185">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="a1feb-186">Określenie grupy docelowej odbiorców może bazować na informacji zwrotnych dotyczących czy ta kampania została właśnie wypychana, odpowiedzi, akcje lub Zakończono.</span><span class="sxs-lookup"><span data-stu-id="a1feb-186">Audience targeting can be based on the feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="a1feb-187">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a1feb-187">See also</span></span>
* <span data-ttu-id="a1feb-188">[Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]</span><span class="sxs-lookup"><span data-stu-id="a1feb-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="a1feb-189">Zawartość sond</span><span class="sxs-lookup"><span data-stu-id="a1feb-189">Content of Polls</span></span>
![Reach Content2][31] 

<span data-ttu-id="a1feb-191">Wprowadź tytuł, opis i przycisk teksty anonsu.</span><span class="sxs-lookup"><span data-stu-id="a1feb-191">Fill in the title, description, and button texts of your announcement.</span></span> <span data-ttu-id="a1feb-192">Następnie należy dodać pytania i dostępnych wyborów w odpowiedzi na pytania.</span><span class="sxs-lookup"><span data-stu-id="a1feb-192">Then, add questions and choices for the answers to your questions.</span></span>
<span data-ttu-id="a1feb-193">Możesz zastosować odbiorców przyszłych kampanii na podstawie opinii reach o jak użytkownicy odpowiedzi kampanii.</span><span class="sxs-lookup"><span data-stu-id="a1feb-193">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="a1feb-194">Określenie grupy docelowej odbiorców może bazować na czy ta kampania została właśnie wypychana, odpowiedzi, akcje lub Zakończono.</span><span class="sxs-lookup"><span data-stu-id="a1feb-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="a1feb-195">Określenie grupy docelowej odbiorców mogą być również oparte na opinii odpowiedzi sondowania, w którym pytanie i odpowiedź wyboru są użyte jako kryteria.</span><span class="sxs-lookup"><span data-stu-id="a1feb-195">Audience targeting can also be based on Poll answer feedback, where the question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="a1feb-196">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a1feb-196">See also</span></span>
* <span data-ttu-id="a1feb-197">[Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]</span><span class="sxs-lookup"><span data-stu-id="a1feb-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="a1feb-198">Zawartość wypychania danych</span><span class="sxs-lookup"><span data-stu-id="a1feb-198">Content of Data Pushes</span></span>
![Reach Content3][32] 

### <a name="choose-the-type-of-your-data"></a><span data-ttu-id="a1feb-200">Wybierz typ danych:</span><span class="sxs-lookup"><span data-stu-id="a1feb-200">Choose the type of your data:</span></span>
* <span data-ttu-id="a1feb-201">Tekst</span><span class="sxs-lookup"><span data-stu-id="a1feb-201">Text</span></span>
* <span data-ttu-id="a1feb-202">Dane binarne</span><span class="sxs-lookup"><span data-stu-id="a1feb-202">Binary data</span></span>
* <span data-ttu-id="a1feb-203">Dane w formacie Base64</span><span class="sxs-lookup"><span data-stu-id="a1feb-203">Base64 data</span></span>

### <a name="define-the-content-of-your-data"></a><span data-ttu-id="a1feb-204">Zdefiniuj zawartość danych</span><span class="sxs-lookup"><span data-stu-id="a1feb-204">Define the content of your data</span></span>
* <span data-ttu-id="a1feb-205">W przypadku wybrania do dystrybuowania danych tekst, skopiuj i wklej tekst w polu "zawartość".</span><span class="sxs-lookup"><span data-stu-id="a1feb-205">If you selected to push text data, copy and paste the text into the "content" box.</span></span>
* <span data-ttu-id="a1feb-206">W przypadku wybrania do dystrybuowania danych binarnych lub base64, użyj przycisku "przesłać plik" Aby przesłać plik.</span><span class="sxs-lookup"><span data-stu-id="a1feb-206">If you selected to push either binary or base64 data, use the "upload your file" button to upload your file.</span></span>
* <span data-ttu-id="a1feb-207">Możesz zastosować odbiorców przyszłych kampanii na podstawie opinii reach o jak użytkownicy odpowiedzi kampanii.</span><span class="sxs-lookup"><span data-stu-id="a1feb-207">You can target an audience of a future campaign based on the reach feedback of how users responded to this campaign.</span></span> <span data-ttu-id="a1feb-208">Określenie grupy docelowej odbiorców może bazować na czy ta kampania została właśnie wypychana, odpowiedzi, akcje lub Zakończono.</span><span class="sxs-lookup"><span data-stu-id="a1feb-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="a1feb-209">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a1feb-209">See also</span></span>
* <span data-ttu-id="a1feb-210">[Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]</span><span class="sxs-lookup"><span data-stu-id="a1feb-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="a1feb-211">Zawartość Kafelki (tylko Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="a1feb-211">Content of Tiles (Windows Phone only)</span></span>
![Reach Content4][33]

### <a name="define-the-content-of-your-tile"></a><span data-ttu-id="a1feb-213">Zdefiniuj zawartość kafelka</span><span class="sxs-lookup"><span data-stu-id="a1feb-213">Define the content of your tile</span></span>
<span data-ttu-id="a1feb-214">Ładunek kafelka jest tekst, który ma być wyświetlane na kafelku aplikacji na urządzeniach Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a1feb-214">The tile payload is the text to be displayed in the tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="a1feb-215">Wypychania kafelka jest wersja usługi powiadomień wypychanych firmy Microsoft (MPNS) natywnych powiadomień wypychanych dla Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="a1feb-215">A tile push is the Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="a1feb-216">Typu kafelka wypychania jest jedynym typem wypychania, który nie ma odpowiedzi i tak odbiorców przyszłych kampanii nie może być oparty na wyniki kampanii wypychania kafelka.</span><span class="sxs-lookup"><span data-stu-id="a1feb-216">The tile push type is the only push type that does not have a response and so the audience of future campaigns can't be built on the results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="a1feb-217">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="a1feb-217">See also</span></span>
* <span data-ttu-id="a1feb-218">[Natywnych powiadomień wypychanych - API Reach — dokumentacja interfejsu API][Link 4]</span><span class="sxs-lookup"><span data-stu-id="a1feb-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

