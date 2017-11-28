---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — osiągnąć zawartości"
description: "Dowiedz się, jak kampanie toomanage hello unikatową zawartość hello różnych typów powiadomień wypychanych w usłudze Azure Mobile Engagement"
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
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="b5078-103">Jak toomanage hello unikatową zawartość różnych typów hello kampanii obejmujących wysyłanie powiadomień wypychanych</span><span class="sxs-lookup"><span data-stu-id="b5078-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="b5078-104">Można użyć sekcji zawartości hello nowe reach kampanii toomodify hello zawartości anonse, ankiety, dane wypychane i Kafelki (tylko Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="b5078-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="b5078-105">ustawienie zawartości Hello kampanie wypychania jest typu toohello określonej kampanii.</span><span class="sxs-lookup"><span data-stu-id="b5078-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="b5078-106">Typy zawartości:</span><span class="sxs-lookup"><span data-stu-id="b5078-106">Content types:</span></span>
* <span data-ttu-id="b5078-107">Anonse</span><span class="sxs-lookup"><span data-stu-id="b5078-107">Announcements</span></span>
* <span data-ttu-id="b5078-108">Ankiety</span><span class="sxs-lookup"><span data-stu-id="b5078-108">Polls</span></span>
* <span data-ttu-id="b5078-109">Wypychania danych</span><span class="sxs-lookup"><span data-stu-id="b5078-109">Data pushes</span></span>
* <span data-ttu-id="b5078-110">Kafelki (tylko Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="b5078-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="b5078-111">Zawartość anonsów</span><span class="sxs-lookup"><span data-stu-id="b5078-111">Content of Announcements</span></span>
 ![Reach Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="b5078-113">Wybierz typ hello anonsu:</span><span class="sxs-lookup"><span data-stu-id="b5078-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="b5078-114">Tylko powiadomienie: jest proste powiadomień w wersji standard.</span><span class="sxs-lookup"><span data-stu-id="b5078-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="b5078-115">Co oznacza, że jeśli użytkownik go kliknie, bez dodatkowego widoku będą wyświetlane, ale tylko hello akcji skojarzonych tooit nastąpi.</span><span class="sxs-lookup"><span data-stu-id="b5078-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="b5078-116">Tekst anonsu: to powiadomienie, które angażujący toohave użytkownika hello przyjrzeć się widoku tekstu.</span><span class="sxs-lookup"><span data-stu-id="b5078-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="b5078-117">Sieci Web anonsu: to powiadomienie, które angażujący toohave użytkownika hello przyjrzeć się widok sieci web.</span><span class="sxs-lookup"><span data-stu-id="b5078-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="b5078-118">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b5078-118">See also</span></span>
* <span data-ttu-id="b5078-119">[Osiągnąć — jak OT - anonsów][Link 3]</span><span class="sxs-lookup"><span data-stu-id="b5078-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="b5078-120">O anonsach widoku sieci Web:</span><span class="sxs-lookup"><span data-stu-id="b5078-120">About Web View Announcements:</span></span>
<span data-ttu-id="b5078-121">Wystąpienia wzorca hello "{deviceid}" w kodzie hello HTML lub kod JavaScript podana tutaj zostaną automatycznie zastąpione hello identyfikator hello urządzenia wyświetlającego anons hello.</span><span class="sxs-lookup"><span data-stu-id="b5078-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="b5078-122">Jest to identyfikatory urządzeń łatwy sposób tooretrieve usługi Azure Mobile Engagement w zewnętrznej sieci web usługi hostowanej w zapleczu biura.</span><span class="sxs-lookup"><span data-stu-id="b5078-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="b5078-123">Jeśli chcesz, aby toocreate pełnego ekranu widoku sieci web (bez hello domyślnych przycisków akcji i wyjścia udostępniamy) można użyć następujących funkcji z kodu JavaScript anonsu widoku sieci web hello:</span><span class="sxs-lookup"><span data-stu-id="b5078-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="b5078-124">Wykonaj akcję anonsu hello: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="b5078-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="b5078-125">wyjść z anonsów hello: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="b5078-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="b5078-126">Wybierz akcję:</span><span class="sxs-lookup"><span data-stu-id="b5078-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="b5078-127">O adresach URL akcji:</span><span class="sxs-lookup"><span data-stu-id="b5078-127">About Action URLs:</span></span>
<span data-ttu-id="b5078-128">Każdy adres URL, który może zostać zinterpretowany przez system operacyjny urządzenia docelowego, może być używany jako adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="b5078-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="b5078-129">Każdy dedykowany adres URL aplikacji może pomocy technicznej (np. użytkownicy toomake skoku tooa konkretnego ekranu) również może służyć jako adres URL akcji.</span><span class="sxs-lookup"><span data-stu-id="b5078-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="b5078-130">Każde wystąpienie wzorca hello {deviceid} jest automatycznie zastępowane hello identyfikator hello urządzenia wykonującego akcję hello.</span><span class="sxs-lookup"><span data-stu-id="b5078-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="b5078-131">Może to być identyfikatory urządzeń usługi Azure Mobile Engagement używane tooeasily pobrać za pomocą zewnętrznej usługi sieci web hostowanej na zapleczu biura.</span><span class="sxs-lookup"><span data-stu-id="b5078-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="b5078-132">**Android i iOS akcje**</span><span class="sxs-lookup"><span data-stu-id="b5078-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="b5078-133">Otwórz stronę sieci web</span><span class="sxs-lookup"><span data-stu-id="b5078-133">Open a web page</span></span>
  * <span data-ttu-id="b5078-134">http://\[domeny w przypadku witryny sieci web\]</span><span class="sxs-lookup"><span data-stu-id="b5078-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="b5078-135">Przykład: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="b5078-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="b5078-136">Wyślij wiadomość e-mail</span><span class="sxs-lookup"><span data-stu-id="b5078-136">Send an e-mail</span></span>
  * <span data-ttu-id="b5078-137">mailto:\[e-mail poczty e-mail odbiorcy\]? podmiotu =\[podmiotu\]& body =\[wiadomości\]</span><span class="sxs-lookup"><span data-stu-id="b5078-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="b5078-138">Example:mailto:foo@example.com? podmiotu = pozdrowienia % 20from % 20Azure % 20Mobile % 20Engagement! & body = 20stuff dobrej %!</span><span class="sxs-lookup"><span data-stu-id="b5078-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="b5078-139">Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="b5078-139">Send a SMS</span></span>
  * <span data-ttu-id="b5078-140">SMS:\[numer telefonu\]</span><span class="sxs-lookup"><span data-stu-id="b5078-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="b5078-141">Przykład: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="b5078-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="b5078-142">Wybierz numer telefonu</span><span class="sxs-lookup"><span data-stu-id="b5078-142">Dial a phone number</span></span>
  * <span data-ttu-id="b5078-143">Tel.:\[numer telefonu\]</span><span class="sxs-lookup"><span data-stu-id="b5078-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="b5078-144">Przykład: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="b5078-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="b5078-145">**Android tylko akcje**</span><span class="sxs-lookup"><span data-stu-id="b5078-145">**Android only actions**</span></span>
  * <span data-ttu-id="b5078-146">Pobierz aplikację ze sklepu Play hello</span><span class="sxs-lookup"><span data-stu-id="b5078-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="b5078-147">Market://details?ID=\[pakiet aplikacji\]</span><span class="sxs-lookup"><span data-stu-id="b5078-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="b5078-148">Przykład: market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="b5078-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="b5078-149">Rozpocznij wyszukiwanie z określoną lokalizacją geograficzną</span><span class="sxs-lookup"><span data-stu-id="b5078-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="b5078-150">Geo:0, 0? q =\[zapytania wyszukiwania\]</span><span class="sxs-lookup"><span data-stu-id="b5078-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="b5078-151">Przykład: geo:0, 0? q = starbucks, Paryża</span><span class="sxs-lookup"><span data-stu-id="b5078-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="b5078-152">**tylko akcje dla systemu iOS**</span><span class="sxs-lookup"><span data-stu-id="b5078-152">**iOS only actions**</span></span>
  * <span data-ttu-id="b5078-153">Pobierz aplikację ze sklepu z aplikacjami hello</span><span class="sxs-lookup"><span data-stu-id="b5078-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="b5078-154">http://iTunes.Apple.com/ [Kraj] /app/ [Nazwa aplikacji] /id [identyfikator aplikacji]? mt = 8</span><span class="sxs-lookup"><span data-stu-id="b5078-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="b5078-155">Przykład: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="b5078-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="b5078-156">Akcje systemu Windows</span><span class="sxs-lookup"><span data-stu-id="b5078-156">Windows Actions</span></span>
  * <span data-ttu-id="b5078-157">Otwórz stronę sieci web</span><span class="sxs-lookup"><span data-stu-id="b5078-157">Open a web page</span></span>
  * <span data-ttu-id="b5078-158">http://\[domeny w przypadku witryny sieci web\]</span><span class="sxs-lookup"><span data-stu-id="b5078-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="b5078-159">Przykład: http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="b5078-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="b5078-160">Wyślij wiadomość e-mail</span><span class="sxs-lookup"><span data-stu-id="b5078-160">Send an e-mail</span></span>
  * <span data-ttu-id="b5078-161">mailto:\[e-mail poczty e-mail odbiorcy\]? podmiotu =\[podmiotu\]& body =\[wiadomości\]</span><span class="sxs-lookup"><span data-stu-id="b5078-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="b5078-162">Example:mailto:foo@example.com? podmiotu = pozdrowienia % 20from % 20Azure % 20Mobile % 20Engagement! & body = 20stuff dobrej %!</span><span class="sxs-lookup"><span data-stu-id="b5078-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="b5078-163">Wyślij wiadomość SMS (wymagana jest aplikacja Skype ze Sklepu)</span><span class="sxs-lookup"><span data-stu-id="b5078-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="b5078-164">SMS:\[numer telefonu\]</span><span class="sxs-lookup"><span data-stu-id="b5078-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="b5078-165">Przykład: sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="b5078-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="b5078-166">Wybierz numer telefonu (wymagana jest aplikacja Skype ze Sklepu)</span><span class="sxs-lookup"><span data-stu-id="b5078-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="b5078-167">Tel.:\[numer telefonu\]</span><span class="sxs-lookup"><span data-stu-id="b5078-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="b5078-168">Przykład: tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="b5078-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="b5078-169">Pobierz aplikację ze sklepu Play hello</span><span class="sxs-lookup"><span data-stu-id="b5078-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="b5078-170">MS-windows-magazynu: strony szczegółów projektu? PFN =\[identyfikator pakietu aplikacji\]</span><span class="sxs-lookup"><span data-stu-id="b5078-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="b5078-171">Przykład: ms-windows-magazynu: strony szczegółów projektu? PFN = 4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="b5078-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="b5078-172">Rozpocznij wyszukiwanie na mapach Bing</span><span class="sxs-lookup"><span data-stu-id="b5078-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="b5078-173">bingmaps:? q =\[zapytania wyszukiwania\]</span><span class="sxs-lookup"><span data-stu-id="b5078-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="b5078-174">Przykład: bingmaps:? q = starbucks, Paryża</span><span class="sxs-lookup"><span data-stu-id="b5078-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="b5078-175">Użyj schematu niestandardowego</span><span class="sxs-lookup"><span data-stu-id="b5078-175">Use a custom scheme</span></span>
  * <span data-ttu-id="b5078-176">\[schemat niestandardowy\]://\[parametry schematu niestandardowego\]</span><span class="sxs-lookup"><span data-stu-id="b5078-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="b5078-177">Przykład: myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="b5078-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="b5078-178">Użyj danych pakietu (w sklepie dla rozszerzenia odczytu wymagane)</span><span class="sxs-lookup"><span data-stu-id="b5078-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="b5078-179">\[folder\]\[danych\].\[ rozszerzenia\]</span><span class="sxs-lookup"><span data-stu-id="b5078-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="b5078-180">Example:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="b5078-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="b5078-181">Utwórz adres URL śledzenia:</span><span class="sxs-lookup"><span data-stu-id="b5078-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="b5078-182">Zobacz sekcję "Ustawienia" hello hello <UI Documentation> dla instrukcje dotyczące tworzenia adres URL śledzenia, który umożliwi użytkownikom toodownload jednego z innych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b5078-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="b5078-183">Zdefiniuj Teksty anonsu hello</span><span class="sxs-lookup"><span data-stu-id="b5078-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="b5078-184">Wprowadź tytuł hello, zawartość i przycisk teksty anonsu.</span><span class="sxs-lookup"><span data-stu-id="b5078-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="b5078-185">Możesz zastosować odbiorców przyszłych kampanii na podstawie opinii reach hello o jak użytkownicy odpowiedział toothis kampanii.</span><span class="sxs-lookup"><span data-stu-id="b5078-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="b5078-186">Określenie grupy docelowej odbiorców może bazować na powitania opinie o czy ta kampania została właśnie wypychana, odpowiedzi, akcje lub Zakończono.</span><span class="sxs-lookup"><span data-stu-id="b5078-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="b5078-187">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b5078-187">See also</span></span>
* <span data-ttu-id="b5078-188">[Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]</span><span class="sxs-lookup"><span data-stu-id="b5078-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="b5078-189">Zawartość sond</span><span class="sxs-lookup"><span data-stu-id="b5078-189">Content of Polls</span></span>
![Reach Content2][31] 

<span data-ttu-id="b5078-191">Wypełnij hello tytuł, opis i przycisk teksty anonsu.</span><span class="sxs-lookup"><span data-stu-id="b5078-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="b5078-192">Następnie należy dodać pytania i możliwości tooyour hello odpowiedzi na pytania.</span><span class="sxs-lookup"><span data-stu-id="b5078-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="b5078-193">Możesz zastosować odbiorców przyszłych kampanii na podstawie opinii reach hello o jak użytkownicy odpowiedział toothis kampanii.</span><span class="sxs-lookup"><span data-stu-id="b5078-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="b5078-194">Określenie grupy docelowej odbiorców może bazować na czy ta kampania została właśnie wypychana, odpowiedzi, akcje lub Zakończono.</span><span class="sxs-lookup"><span data-stu-id="b5078-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="b5078-195">Określenie grupy docelowej odbiorców mogą być również oparte na sondowania odpowiedzi opinii, gdy wybór pytanie i odpowiedź hello są używane jako kryteria.</span><span class="sxs-lookup"><span data-stu-id="b5078-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="b5078-196">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b5078-196">See also</span></span>
* <span data-ttu-id="b5078-197">[Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]</span><span class="sxs-lookup"><span data-stu-id="b5078-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="b5078-198">Zawartość wypychania danych</span><span class="sxs-lookup"><span data-stu-id="b5078-198">Content of Data Pushes</span></span>
![Reach Content3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="b5078-200">Wybierz typ hello danych:</span><span class="sxs-lookup"><span data-stu-id="b5078-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="b5078-201">Tekst</span><span class="sxs-lookup"><span data-stu-id="b5078-201">Text</span></span>
* <span data-ttu-id="b5078-202">Dane binarne</span><span class="sxs-lookup"><span data-stu-id="b5078-202">Binary data</span></span>
* <span data-ttu-id="b5078-203">Dane w formacie Base64</span><span class="sxs-lookup"><span data-stu-id="b5078-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="b5078-204">Zdefiniuj zawartość danych hello</span><span class="sxs-lookup"><span data-stu-id="b5078-204">Define hello content of your data</span></span>
* <span data-ttu-id="b5078-205">Jeśli wybrane dane tekstowe toopush, skopiuj i Wklej hello tekst w polu "zawartość" hello.</span><span class="sxs-lookup"><span data-stu-id="b5078-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="b5078-206">W przypadku wybrania toopush danych binarnych lub base64, użyj tooupload przycisk "Przekaż plik" hello pliku.</span><span class="sxs-lookup"><span data-stu-id="b5078-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="b5078-207">Możesz zastosować odbiorców przyszłych kampanii na podstawie opinii reach hello o jak użytkownicy odpowiedział toothis kampanii.</span><span class="sxs-lookup"><span data-stu-id="b5078-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="b5078-208">Określenie grupy docelowej odbiorców może bazować na czy ta kampania została właśnie wypychana, odpowiedzi, akcje lub Zakończono.</span><span class="sxs-lookup"><span data-stu-id="b5078-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="b5078-209">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b5078-209">See also</span></span>
* <span data-ttu-id="b5078-210">[Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]</span><span class="sxs-lookup"><span data-stu-id="b5078-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="b5078-211">Zawartość Kafelki (tylko Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="b5078-211">Content of Tiles (Windows Phone only)</span></span>
![Reach Content4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="b5078-213">Zdefiniuj zawartość kafelka hello</span><span class="sxs-lookup"><span data-stu-id="b5078-213">Define hello content of your tile</span></span>
<span data-ttu-id="b5078-214">ładunek kafelka Hello jest hello toobe tekst wyświetlany w kafelku hello aplikacji na urządzeniach Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b5078-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="b5078-215">Wypychania kafelka jest wersja usługi powiadomień wypychanych firmy Microsoft (MPNS) hello natywnych powiadomień wypychanych dla Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b5078-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="b5078-216">typu wypychania kafelka Hello jest hello tylko wypychania typ, który nie ma odpowiedzi i tak odbiorców hello przyszłych kampanii nie może być oparty na hello wyniki kampanii wypychania kafelka.</span><span class="sxs-lookup"><span data-stu-id="b5078-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="b5078-217">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="b5078-217">See also</span></span>
* <span data-ttu-id="b5078-218">[Natywnych powiadomień wypychanych - API Reach — dokumentacja interfejsu API][Link 4]</span><span class="sxs-lookup"><span data-stu-id="b5078-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

