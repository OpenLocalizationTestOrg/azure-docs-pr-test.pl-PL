---
title: "aaaAzure Mobile Engagement interfejsu użytkownika — osiągnąć kampanii"
description: "Laern jak toocreate i zarządzać nimi za pomocą usługi Azure Mobile Engagement kampanii obejmujących wysyłanie powiadomień wypychanych"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="2e3ca-103">Jak toocreate kampanii powiadomień wypychanych i zarządzanie nimi</span><span class="sxs-lookup"><span data-stu-id="2e3ca-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="2e3ca-104">Za pomocą hello Reach części toocreate interfejsu użytkownika hello nową kampanię wypychania i złożone formuły podając wszystkie informacje hello potrzebne toosend powiadomienie wypychane.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="2e3ca-105">Witaj opcje kampanii wypychania się nieco różnić w zależności od typów kampanii hello czterech: anonsów, ankiety, dane wypychane i Kafelki (tylko Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="2e3ca-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="2e3ca-106">Opcja ma zastosowanie do:</span><span class="sxs-lookup"><span data-stu-id="2e3ca-106">Option Applies to:</span></span>
* <span data-ttu-id="2e3ca-107">Języki: Wszystkie (anonse, ankiety, wypychania danych, Kafelki)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="2e3ca-108">Kampania: Wszystkie (anonse, ankiety, wypychania danych, Kafelki)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="2e3ca-109">Powiadomienie: Anonse, ankiety</span><span class="sxs-lookup"><span data-stu-id="2e3ca-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="2e3ca-110">Zawartość: Unikatowy dla każdego typu kampanii</span><span class="sxs-lookup"><span data-stu-id="2e3ca-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="2e3ca-111">Grupy odbiorców: Wszystkie (anonse, ankiety, wypychania danych, Kafelki)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="2e3ca-112">Przedział czasu: Kafelki anonse, ankiety,</span><span class="sxs-lookup"><span data-stu-id="2e3ca-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="2e3ca-113">Testowanie: Wszystkie (anonse, ankiety, wypychania danych, Kafelki)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach Campaign1][20]

## <a name="languages"></a><span data-ttu-id="2e3ca-115">Języki</span><span class="sxs-lookup"><span data-stu-id="2e3ca-115">Languages</span></span>
<span data-ttu-id="2e3ca-116">Możesz użyć toosend menu hello rozwijanej języki innej wersji toodevices Twojego wypychania, są ustawione toouse w różnych językach.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="2e3ca-117">Domyślnie wszystkie urządzenia będą otrzymywać hello Push sama niezależnie od tego, jakie są ustawione toouse.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="2e3ca-118">Użytkownicy z ich urządzeń zestaw tooa innego języka będą otrzymywać wersji język domyślny hello hello wypychania.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="2e3ca-119">Wiele opcji kampanii wypychania hello pozwalają toospecify alternatywny zawartości dla każdego z języków dodatkowe hello, którą wybierzesz.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![Reach Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="2e3ca-121">Różnice języka dotyczą:</span><span class="sxs-lookup"><span data-stu-id="2e3ca-121">Language differences apply to:</span></span>
* <span data-ttu-id="2e3ca-122">Języki: Unikatowy języków można wybrać w języku domyślnym toohello dodanie</span><span class="sxs-lookup"><span data-stu-id="2e3ca-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="2e3ca-123">Kampania: Takie Same dla wszystkich języków</span><span class="sxs-lookup"><span data-stu-id="2e3ca-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="2e3ca-124">Powiadomienie: Unikatowy dla każdego języka dodatkowo toohello język domyślny</span><span class="sxs-lookup"><span data-stu-id="2e3ca-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="2e3ca-125">Zawartość: Unikatowy dla każdego języka dodatkowo toohello język domyślny</span><span class="sxs-lookup"><span data-stu-id="2e3ca-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="2e3ca-126">Grupy odbiorców: Mogą być filtrowane według kryterium oddzielne języka</span><span class="sxs-lookup"><span data-stu-id="2e3ca-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="2e3ca-127">Przedział czasu: tej samej dla wszystkich języków</span><span class="sxs-lookup"><span data-stu-id="2e3ca-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="2e3ca-128">Testowanie: Mogą być wysyłane języka tooeach naraz</span><span class="sxs-lookup"><span data-stu-id="2e3ca-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="2e3ca-129">Obsługiwane języki:</span><span class="sxs-lookup"><span data-stu-id="2e3ca-129">Supported Languages:</span></span>
* <span data-ttu-id="2e3ca-130">Arabski (ar)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-130">Arabic (ar)</span></span> 
* <span data-ttu-id="2e3ca-131">Bułgarski (bg)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="2e3ca-132">Katalońskim (ca)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-132">Catalan (ca)</span></span> 
* <span data-ttu-id="2e3ca-133">Chiński (zh)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-133">Chinese (zh)</span></span> 
* <span data-ttu-id="2e3ca-134">Chorwacki (hr)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-134">Croatian (hr)</span></span> 
* <span data-ttu-id="2e3ca-135">Czech (CS)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-135">Czech (cs)</span></span> 
* <span data-ttu-id="2e3ca-136">Duński (da)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-136">Danish (da)</span></span> 
* <span data-ttu-id="2e3ca-137">Holenderski (Holandia)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-137">Dutch (nl)</span></span> 
* <span data-ttu-id="2e3ca-138">Angielski (en)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-138">English (en)</span></span> 
* <span data-ttu-id="2e3ca-139">Fiński (fi)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-139">Finnish (fi)</span></span> 
* <span data-ttu-id="2e3ca-140">Francuski (fr)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-140">French (fr)</span></span> 
* <span data-ttu-id="2e3ca-141">Niemiecki (de)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-141">German (de)</span></span> 
* <span data-ttu-id="2e3ca-142">Grecki (el)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-142">Greek (el)</span></span> 
* <span data-ttu-id="2e3ca-143">Hebrajski (osoba)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-143">Hebrew (he)</span></span> 
* <span data-ttu-id="2e3ca-144">Hindi (cześć)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-144">Hindi (hi)</span></span> 
* <span data-ttu-id="2e3ca-145">Węgierski (hu)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="2e3ca-146">Indonezyjski (id)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-146">Indonesian (id)</span></span> 
* <span data-ttu-id="2e3ca-147">Włoski (go)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-147">Italian (it)</span></span> 
* <span data-ttu-id="2e3ca-148">Japoński (ja)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-148">Japanese (ja)</span></span> 
* <span data-ttu-id="2e3ca-149">Koreański (ko)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-149">Korean (ko)</span></span> 
* <span data-ttu-id="2e3ca-150">Łotewski (lv)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-150">Latvian (lv)</span></span> 
* <span data-ttu-id="2e3ca-151">Litewski (lt)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="2e3ca-152">Malajski (macrolanguage) (ms)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="2e3ca-153">Norweski, Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="2e3ca-154">Polski (pl)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-154">Polish (pl)</span></span> 
* <span data-ttu-id="2e3ca-155">Portugalski (pt)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="2e3ca-156">Rumuński (ro)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-156">Romanian (ro)</span></span> 
* <span data-ttu-id="2e3ca-157">Rosyjski (ru)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-157">Russian (ru)</span></span> 
* <span data-ttu-id="2e3ca-158">Serbski (sr)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-158">Serbian (sr)</span></span> 
* <span data-ttu-id="2e3ca-159">Słowacki (sk)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-159">Slovak (sk)</span></span> 
* <span data-ttu-id="2e3ca-160">Słoweński (sl)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="2e3ca-161">Hiszpański (es)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-161">Spanish (es)</span></span> 
* <span data-ttu-id="2e3ca-162">Szwedzki (sv)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-162">Swedish (sv)</span></span> 
* <span data-ttu-id="2e3ca-163">Tagalski (tl)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="2e3ca-164">Tajski (th)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-164">Thai (th)</span></span> 
* <span data-ttu-id="2e3ca-165">Turecki (tr)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-165">Turkish (tr)</span></span> 
* <span data-ttu-id="2e3ca-166">Ukraiński (Zjednoczone Królestwo)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="2e3ca-167">Wietnamski (IV)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="2e3ca-168">Kampanii</span><span class="sxs-lookup"><span data-stu-id="2e3ca-168">Campaign</span></span>
<span data-ttu-id="2e3ca-169">Używając hello kampanii sekcji tooset hello nazwy i Kategoria kampanii również tak, jakby planowanie tooignore hello odbiorców sekcji kampanii wypychania i zamiast tego Wyślij kampanii za pośrednictwem interfejsu API Reach hello (i niektóre elementy z niskim poziomem hello Push interfejsu API).</span><span class="sxs-lookup"><span data-stu-id="2e3ca-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="2e3ca-170">Kategorie można łączyć z szablonu niestandardowego powiadomień toocontrol powiadomienia w aplikacji na podstawie wstępnie zdefiniowanych ustawień.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="2e3ca-171">Można uzyskać listę istniejących "kategorii" za pośrednictwem interfejsu API Reach hello.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="2e3ca-172">Jeśli używasz opcji "Ignoruj odbiorców, powiadomienia wypychane będą wysyłane toousers za pośrednictwem interfejsu API hello" hello w sekcji "Kampanii" hello kampanii Reach kampanii hello nie będzie automatycznie wysyłać, konieczne będzie toosend go ręcznie za pomocą interfejsu API Reach hello.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![Reach Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="2e3ca-174">Opcja ma zastosowanie do:</span><span class="sxs-lookup"><span data-stu-id="2e3ca-174">Option Applies to:</span></span>
* <span data-ttu-id="2e3ca-175">Nazwa: wszystkie</span><span class="sxs-lookup"><span data-stu-id="2e3ca-175">Name:    All</span></span>
* <span data-ttu-id="2e3ca-176">Kategoria: Anonse, ankiety</span><span class="sxs-lookup"><span data-stu-id="2e3ca-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="2e3ca-177">Ignoruj odbiorców, wypychane będą wysyłane toousers za pośrednictwem interfejsu API hello: wszystkie</span><span class="sxs-lookup"><span data-stu-id="2e3ca-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="2e3ca-178">Powiadomienia</span><span class="sxs-lookup"><span data-stu-id="2e3ca-178">Notification</span></span>
<span data-ttu-id="2e3ca-179">Umożliwia hello powiadomień sekcji tooset podstawowych ustawień z tym wypychania: hello tytuł hello wypychanie, wiadomość hello, obrazu w aplikacji, czy jest możliwe do odrzucenia.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="2e3ca-180">Wiele ustawień powiadomień są platformy toohello określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="2e3ca-181">Można wybrać, czy Twoje wypychane będą wysyłane "w aplikacji" lub "poza aplikacją" lub oba.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="2e3ca-182">(Pamiętać, że użytkownicy mogą "opt w" lub "Wypisz" "poza aplikacji" wypchnięcia na powitania systemu operacyjnego poziomu na ich urządzeniach i usługi Azure Mobile Engagement nie będą się mogli toooverride to ustawienie.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="2e3ca-183">Również należy pamiętać, że obsługi interfejsu API Reach hello "w aplikacji" i "out aplikacji" wypchnięcia.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="2e3ca-184">Hello Push interfejsu API może być używane toohandle "mieszczą się w aplikacji" zbyt wypchnięcia). Wypchnięcia można dostosować za pomocą obrazów lub zawartość HTML, w tym linków bezpośrednich do konsolidacji poza Twojej aplikacji lub tooanother lokalizacji w aplikacji (zestaw SDK systemu Android 2.1.0 lub nowsze kategorii konwersji wymagane).</span><span class="sxs-lookup"><span data-stu-id="2e3ca-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="2e3ca-185">Możesz zmienić identyfikator ikony lub iOS hello i wysyłania zawartości tekstu lub w sieci web (podręcznego html, adres URL łącza tooanother lokalizacji zawartości wewnątrz lub na zewnątrz aplikacji hello).</span><span class="sxs-lookup"><span data-stu-id="2e3ca-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="2e3ca-186">Można również dzwonek urządzenia z systemem Android lub też z hello wypychania.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="2e3ca-187">(Należy pamiętać, że można będzie konieczne hello poprawne uprawnienia zestawu SDK dla systemu Android tooring pliku manifestu lub Włącz wibrację urządzenia). Nie ma żadnych branży standardowe dla systemu Android "szerszej" rozmiary, od rozmiaru ekranu różnią się na każdym urządzeniu, ale obrazy 400 x 100 pracować z prawie każdego rozmiaru ekranu.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="2e3ca-188">Typy dostarczania:</span><span class="sxs-lookup"><span data-stu-id="2e3ca-188">Delivery Types:</span></span>
* <span data-ttu-id="2e3ca-189">Tylko poza aplikacją: hello powiadomień zostanie dostarczona, gdy użytkownik hello nie korzysta z aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="2e3ca-190">Witaj poza tylko powiadomienie aplikacji wymaga certyfikatu od firmy Apple lub Google (certyfikat usługi APNS lub GCM).</span><span class="sxs-lookup"><span data-stu-id="2e3ca-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="2e3ca-191">W aplikacji tylko: hello powiadomień zostanie wyświetlona tylko wtedy, gdy aplikacja hello jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="2e3ca-192">powiadomienie Hello używa hello Capptain system dostarczania tooreach hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="2e3ca-193">Witaj układu/wyświetlanie Twoje zamówienie pełni można dostosować.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="2e3ca-194">Zawsze: Ta opcja zapewnia wysyłanie powiadomień, który aplikacja hello jest uruchomiona lub nie.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![Reach Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="2e3ca-196">Opcja ma zastosowanie do:</span><span class="sxs-lookup"><span data-stu-id="2e3ca-196">Option Applies to:</span></span>
* <span data-ttu-id="2e3ca-197">Powiadomienie: Anonse, ankiety</span><span class="sxs-lookup"><span data-stu-id="2e3ca-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="2e3ca-198">Zawartość</span><span class="sxs-lookup"><span data-stu-id="2e3ca-198">Content</span></span>
<span data-ttu-id="2e3ca-199">Możesz użyć hello sekcji zawartości toomodify hello zawartości anonse, ankiety, dane wypychane i Kafelki (tylko Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="2e3ca-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="2e3ca-200">ustawienie zawartości Hello kampanie wypychania jest typu toohello określonej kampanii.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="2e3ca-201">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2e3ca-201">See also</span></span>
* <span data-ttu-id="2e3ca-202">[Dokumentacja interfejsu użytkownika — osiągnąć — wypychania zawartości][Link 29]</span><span class="sxs-lookup"><span data-stu-id="2e3ca-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach Campaign5][24]

## <a name="audience"></a><span data-ttu-id="2e3ca-204">Grupy odbiorców</span><span class="sxs-lookup"><span data-stu-id="2e3ca-204">Audience</span></span>
<span data-ttu-id="2e3ca-205">Możesz użyć hello odbiorców sekcji toodefine listę standardowych elementów toolimit kampanii lub limity kampanii na podstawie niestandardowych kryteriów.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="2e3ca-206">Standardowy zestaw opcji tooLimit Hello odbiorców pozwala toopush tooeither nowej lub starej użytkowników czy tylko użytkowników natywnych powiadomień wypychanych.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="2e3ca-207">Można również ustawić limit przydziału toolimit hello szereg użytkownicy, którzy otrzymają hello wypychania.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="2e3ca-208">Można ręcznie edytować wyrażenie hello jak kampanii jest filtrowany tooinclude co najmniej jednego kryterium tootarget użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="2e3ca-209">Można ręcznie wpisz wyrażenie odbiorców.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-209">You can manually type an audience expression.</span></span> <span data-ttu-id="2e3ca-210">Takie wyrażenie musi jawnie definiować hello relację między kryteriami.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="2e3ca-211">Kryterium jest opisane przez identyfikator, który musi rozpoczynać się wielką literą i nie może zawierać spacji.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="2e3ca-212">Witaj relację między kryteriami hello można opisać za pomocą "i", "lub" operatory "nie", a także "(",")".</span><span class="sxs-lookup"><span data-stu-id="2e3ca-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="2e3ca-213">Przykład: "Criterion1 lub (Criterion1 i nie Criterion2)".</span><span class="sxs-lookup"><span data-stu-id="2e3ca-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="2e3ca-214">Wiele osób zawarte w kampanie, po stronie serwera hello przeznaczonych dla skanowania może działać powoli, zwłaszcza, jeśli próba toostart wiele kampanii w hello sam czas.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="2e3ca-215">Jeśli to możliwe tylko należy uruchomić jeden kampanii.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="2e3ca-216">W hello najbardziej, tylko rozpoczęcia kampanii cztery naraz.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="2e3ca-217">Push tylko tooyour aktywnych użytkowników (pole wyboru "Uwzględnij tylko użytkowników osiągalnych przy użyciu natywnych powiadomień wypychanych" i "Uwzględnij tylko aktywnych użytkowników"), aby tylko użytkownikom, którzy nadal mieć zainstalowanej aplikacji hello i korzystać z niego potrzebne toobe skanowania.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="2e3ca-218">Po zdefiniowaniu odbiorców można użyć hello symulować toofind przycisk limit ile użytkownicy otrzymają ten wypychania.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="2e3ca-219">Spowoduje to obliczeniowe hello liczby znanych użytkowników potencjalnie docelowe w ramach tych odbiorców (jest to wartość szacowana na podstawie losowej próbki użytkowników).</span><span class="sxs-lookup"><span data-stu-id="2e3ca-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="2e3ca-220">Należy pamiętać, że użytkownicy, którzy odinstalowali aplikacji hello będą również należeli do tych odbiorców, ale nie można nawiązać połączenia.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="2e3ca-221">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2e3ca-221">See also</span></span>
* <span data-ttu-id="2e3ca-222">[Nowe kryterium wypychania - Reach — dokumentacja interfejsu użytkownika][Link 28]</span><span class="sxs-lookup"><span data-stu-id="2e3ca-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="2e3ca-224">Edytowanie wyrażeń</span><span class="sxs-lookup"><span data-stu-id="2e3ca-224">Edit expression</span></span>
![Reach Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="2e3ca-226">Limit Twojego odbiorców opcja ma zastosowanie do:</span><span class="sxs-lookup"><span data-stu-id="2e3ca-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="2e3ca-227">Uwzględnij tylko podzestaw użytkowników: wszystkie (anonse, ankiety, wypycha dane, Kafelki)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="2e3ca-228">Uwzględnij tylko starych użytkowników: wszystkie (anonse, ankiety, wypycha dane, Kafelki)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="2e3ca-229">Uwzględnij tylko nowych użytkowników: wszystkie (anonse, ankiety, wypycha dane, Kafelki)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="2e3ca-230">Uwzględnij tylko bezczynnych użytkowników: Kafelki anonse, ankiety,</span><span class="sxs-lookup"><span data-stu-id="2e3ca-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="2e3ca-231">Uwzględnij tylko aktywnych użytkowników: wszystkie (anonse, ankiety, wypycha dane, Kafelki)</span><span class="sxs-lookup"><span data-stu-id="2e3ca-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="2e3ca-232">Uwzględnij tylko użytkowników osiągalnych przy użyciu natywnych powiadomień wypychanych: anonse, ankiety</span><span class="sxs-lookup"><span data-stu-id="2e3ca-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="2e3ca-233">Przedział czasu</span><span class="sxs-lookup"><span data-stu-id="2e3ca-233">Time Frame</span></span>
<span data-ttu-id="2e3ca-234">Użyciem hello okresie sekcji tooset hello wypychane będą wysyłane można także pozostawić hello okresie puste toostart hello kampanii natychmiast.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="2e3ca-235">Należy pamiętać, że przy użyciu strefy czasowej użytkownicy końcowi hello może rozpocząć kampanii hello dzień wcześniej, niż oczekiwano dla użytkowników końcowych w Azji, a małych partii wypchnięć jednocześnie do wszystkich stref czasowych w przedziale czasu hello hello world dopasowania kampanii wysyłania.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="2e3ca-236">Przy użyciu strefy czasowej użytkownicy końcowi hello mogą powodować opóźnienia w kampaniach ponieważ ma ona toorequest hello czasu z telefonu hello przed rozpoczęciem hello wypychania.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="2e3ca-237">Kampanie, bez daty zakończenia może buforować wypchnięć lokalnie i nadal wyświetlane po ręcznie pełną kampanii.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="2e3ca-238">tooavoid tego zachowania, określonej godziny zakończenia kampanii.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="2e3ca-239">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2e3ca-239">See also</span></span>
* <span data-ttu-id="2e3ca-240">[Osiągnąć — jak Tos — Planowanie][Link 3]</span><span class="sxs-lookup"><span data-stu-id="2e3ca-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="2e3ca-242">Ustawienia mają zastosowanie do:</span><span class="sxs-lookup"><span data-stu-id="2e3ca-242">Settings Apply to:</span></span>
* <span data-ttu-id="2e3ca-243">Przedział czasu: Kafelki anonse, ankiety,</span><span class="sxs-lookup"><span data-stu-id="2e3ca-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="2e3ca-244">Testowanie</span><span class="sxs-lookup"><span data-stu-id="2e3ca-244">Test</span></span>
<span data-ttu-id="2e3ca-245">Można użyć hello testu sekcji toosend urządzenia własne testu tooyour wypychania przed zapisaniem hello kampanii.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="2e3ca-246">Jeśli skonfigurowano wszelkie niestandardowe języków dla kampanii, można przetestować wypychania hello w każdego języka.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="2e3ca-247">Możesz skonfigurować urządzenia testu z "Moje konto".</span><span class="sxs-lookup"><span data-stu-id="2e3ca-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="2e3ca-248">Wypchnięcia nie po stronie serwera, którego dane są rejestrowane, korzystając z przycisku hello zbyt "test", tylko rejestrowane są dane dla kampanie wypychania prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="2e3ca-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="2e3ca-249">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2e3ca-249">See also</span></span>
* <span data-ttu-id="2e3ca-250">[Dokumentacja interfejsu użytkownika — Moje konto][Link 14]</span><span class="sxs-lookup"><span data-stu-id="2e3ca-250">[UI Documentation - My Account][Link 14]</span></span>

![Reach Campaign9][28]

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

