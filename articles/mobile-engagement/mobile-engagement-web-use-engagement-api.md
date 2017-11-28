---
title: "Interfejsy API zestawu SDK sieci Web usługi Azure Mobile Engagement | Dokumentacja firmy Microsoft"
description: "Najnowsze aktualizacje i procedury dotyczące zestawu SDK sieci Web dla usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="30cf8-103">Użyj interfejsu API Azure Mobile Engagement w aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="30cf8-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="30cf8-104">Ten dokument jest dodaną do dokumentu, który informuje o sposobie do [zintegrowana usługa Mobile Engagement w aplikacji sieci web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="30cf8-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="30cf8-105">Zapewnia on szczegółowe informacje o raport statystyk aplikacji przy użyciu interfejsu API Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="30cf8-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="30cf8-106">Interfejs API Mobile Engagement jest zapewniana przez `engagement.agent` obiektu.</span><span class="sxs-lookup"><span data-stu-id="30cf8-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="30cf8-107">Domyślny zestaw SDK usługi Azure Mobile Engagement Web alias jest `engagement`.</span><span class="sxs-lookup"><span data-stu-id="30cf8-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="30cf8-108">Można zmienić ten alias z konfiguracji zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="30cf8-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="30cf8-109">Pojęcia dotyczące usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="30cf8-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="30cf8-110">Następujące części uściślić wspólnej [pojęcia dotyczące usługi Mobile Engagement](mobile-engagement-concepts.md) platformy sieci web.</span><span class="sxs-lookup"><span data-stu-id="30cf8-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="30cf8-111">`Session` i `Activity`</span><span class="sxs-lookup"><span data-stu-id="30cf8-111">`Session` and `Activity`</span></span>
<span data-ttu-id="30cf8-112">Jeśli użytkownik pozostaje bezczynności więcej niż kilka sekund pomiędzy dwoma działaniami, sekwencję działań użytkownika jest podzielony na dwie różne sesje.</span><span class="sxs-lookup"><span data-stu-id="30cf8-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="30cf8-113">Te kilka sekund, są nazywane limit czasu sesji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="30cf8-114">Jeśli aplikacja sieci web nie deklaruje zakończenia działań użytkownika samodzielnie (przez wywołanie metody `engagement.agent.endActivity` funkcji), serwer usługi Mobile Engagement automatycznie wygaśnięcia sesji użytkownika w ciągu trzech minut po zamknięciu strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="30cf8-115">Jest to limit czasu sesji serwera.</span><span class="sxs-lookup"><span data-stu-id="30cf8-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="30cf8-116">Domyślnie nie są tworzone automatycznych raporty dotyczące nieprzechwyconych wyjątków JavaScript.</span><span class="sxs-lookup"><span data-stu-id="30cf8-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="30cf8-117">Jednak możesz zgłosić awarię ręcznie przy użyciu `sendCrash` funkcji (zobacz sekcję dotyczącą raportowania awarii).</span><span class="sxs-lookup"><span data-stu-id="30cf8-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="30cf8-118">Działania raportowania</span><span class="sxs-lookup"><span data-stu-id="30cf8-118">Reporting activities</span></span>
<span data-ttu-id="30cf8-119">Raporty dotyczące działań użytkownika zawiera gdy użytkownik uruchamia nowe działanie, a bieżące działanie kończy się użytkownika.</span><span class="sxs-lookup"><span data-stu-id="30cf8-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="30cf8-120">Użytkownik uruchamia nowe działanie</span><span class="sxs-lookup"><span data-stu-id="30cf8-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="30cf8-121">Należy wywołać `startActivity()` zmiany każdego działania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="30cf8-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="30cf8-122">W pierwszym wywołaniu tej funkcji uruchamia nową sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="30cf8-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="30cf8-123">Użytkownik kończy się bieżące działanie</span><span class="sxs-lookup"><span data-stu-id="30cf8-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="30cf8-124">Należy wywołać `endActivity()` co najmniej raz, gdy użytkownik zakończy swoje ostatnie działanie.</span><span class="sxs-lookup"><span data-stu-id="30cf8-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="30cf8-125">Zestaw SDK usługi Mobile Engagement w sieci Web to informuje, czy użytkownik jest obecnie w stanie bezczynności i że sesji użytkownika musi zostać zamknięty, po upływie limitu czasu sesji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="30cf8-126">Jeśli należy wywołać `startActivity()` przed upłynięciem limitu czasu sesji, po prostu wznowić sesji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="30cf8-127">Ponieważ nie ma niezawodne składania po zamknięciu okna navigator, często jest trudne lub niemożliwe do wychwytywania zakończenia działań użytkownika w środowisku sieci web.</span><span class="sxs-lookup"><span data-stu-id="30cf8-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="30cf8-128">Dlatego serwer usługi Mobile Engagement automatycznie wygaśnięcia sesji użytkownika w ciągu trzech minut po zamknięciu strony aplikacji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="30cf8-129">Zdarzenia raportowania</span><span class="sxs-lookup"><span data-stu-id="30cf8-129">Reporting events</span></span>
<span data-ttu-id="30cf8-130">Raporty dotyczące zdarzeń obejmuje zdarzenia sesji i autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="30cf8-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="30cf8-131">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="30cf8-131">Session events</span></span>
<span data-ttu-id="30cf8-132">Zdarzenia sesji są zwykle używane do zgłaszania akcji wykonywanych przez użytkownika podczas sesji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="30cf8-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="30cf8-133">**Przykład bez dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="30cf8-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="30cf8-134">**Przykład: dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="30cf8-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="30cf8-135">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="30cf8-135">Standalone events</span></span>
<span data-ttu-id="30cf8-136">W przeciwieństwie do sesji zdarzeń mogą występować zdarzenia autonomiczny poza kontekstem sesji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="30cf8-137">Do tego użyć ``engagement.agent.sendEvent`` zamiast ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="30cf8-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="30cf8-138">Raportowanie błędów</span><span class="sxs-lookup"><span data-stu-id="30cf8-138">Reporting errors</span></span>
<span data-ttu-id="30cf8-139">Raportowanie błędów obejmuje błędy sesji i błędy autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="30cf8-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="30cf8-140">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="30cf8-140">Session errors</span></span>
<span data-ttu-id="30cf8-141">Błędy sesji zwykle są używane do zgłaszania błędów, które mają wpływ na użytkownika podczas sesji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="30cf8-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="30cf8-142">**Przykład bez dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="30cf8-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="30cf8-143">**Przykład: dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="30cf8-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="30cf8-144">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="30cf8-144">Standalone errors</span></span>
<span data-ttu-id="30cf8-145">W przeciwieństwie do błędów sesji mogą wystąpić błędy autonomiczny poza kontekstem sesji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="30cf8-146">Do tego użyć `engagement.agent.sendError` zamiast `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="30cf8-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="30cf8-147">Zadania raportowania</span><span class="sxs-lookup"><span data-stu-id="30cf8-147">Reporting jobs</span></span>
<span data-ttu-id="30cf8-148">Raporty dotyczące obejmuje zadania raportowania błędów i zdarzeń występujących podczas wykonywania zadania i raportowania awarii (Crash).</span><span class="sxs-lookup"><span data-stu-id="30cf8-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="30cf8-149">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="30cf8-149">**Example:**</span></span>

<span data-ttu-id="30cf8-150">Jeśli chcesz monitorować żądaniem AJAX użyje następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="30cf8-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="30cf8-151">Raportowanie błędów podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="30cf8-151">Reporting errors during a job</span></span>
<span data-ttu-id="30cf8-152">Błędy może być powiązane z uruchomionym zadaniem, a nie do bieżącej sesji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="30cf8-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="30cf8-153">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="30cf8-153">**Example:**</span></span>

<span data-ttu-id="30cf8-154">Jeśli chcesz zgłosić błąd, jeśli żądanie AJAX nie powiedzie się:</span><span class="sxs-lookup"><span data-stu-id="30cf8-154">If you want to report an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="30cf8-155">Zdarzenia raportowania podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="30cf8-155">Reporting events during a job</span></span>
<span data-ttu-id="30cf8-156">Zdarzenia może być związany z uruchomionym zadaniem, a nie z bieżącą sesją użytkownika Podziękowania `engagement.agent.sendJobEvent` funkcji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="30cf8-157">Ta funkcja działa dokładnie tak samo, jak `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="30cf8-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="30cf8-158">Raportowanie awarii (Crash)</span><span class="sxs-lookup"><span data-stu-id="30cf8-158">Reporting crashes</span></span>
<span data-ttu-id="30cf8-159">Użyj `sendCrash` ręcznie ulega awarii funkcji do raportu.</span><span class="sxs-lookup"><span data-stu-id="30cf8-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="30cf8-160">`crashid` Argument jest ciąg identyfikujący typ awarii.</span><span class="sxs-lookup"><span data-stu-id="30cf8-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="30cf8-161">`crash` Argument jest zazwyczaj ślad stosu awarii (Crash) jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="30cf8-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="30cf8-162">Dodatkowe parametry</span><span class="sxs-lookup"><span data-stu-id="30cf8-162">Extra parameters</span></span>
<span data-ttu-id="30cf8-163">Dowolne dane można dołączyć do zdarzenia, błąd, działania lub zadania.</span><span class="sxs-lookup"><span data-stu-id="30cf8-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="30cf8-164">Dane mogą być dowolnego obiektu JSON (ale nie tablicy lub typu pierwotnego).</span><span class="sxs-lookup"><span data-stu-id="30cf8-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="30cf8-165">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="30cf8-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="30cf8-166">Limity</span><span class="sxs-lookup"><span data-stu-id="30cf8-166">Limits</span></span>
<span data-ttu-id="30cf8-167">Ograniczenia, które dotyczą dodatkowe parametry są w zakresie wyrażeń regularnych do kluczy, typy wartości i rozmiar.</span><span class="sxs-lookup"><span data-stu-id="30cf8-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="30cf8-168">Klucze</span><span class="sxs-lookup"><span data-stu-id="30cf8-168">Keys</span></span>
<span data-ttu-id="30cf8-169">Każdy klucz w obiekcie musi odpowiadać następującym wyrażeniem regularnym:</span><span class="sxs-lookup"><span data-stu-id="30cf8-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="30cf8-170">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, po której następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="30cf8-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="30cf8-171">Wartości</span><span class="sxs-lookup"><span data-stu-id="30cf8-171">Values</span></span>
<span data-ttu-id="30cf8-172">Wartości są ograniczone do ciągu, liczbę i typy Boolean.</span><span class="sxs-lookup"><span data-stu-id="30cf8-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="30cf8-173">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="30cf8-173">Size</span></span>
<span data-ttu-id="30cf8-174">Dodatki mogą zawierać maksymalnie 1024 znaków na wywołanie (po zestaw SDK usługi Mobile Engagement Web kodowane w formacie JSON).</span><span class="sxs-lookup"><span data-stu-id="30cf8-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="30cf8-175">Raportowanie informacji o aplikacji</span><span class="sxs-lookup"><span data-stu-id="30cf8-175">Reporting application information</span></span>
<span data-ttu-id="30cf8-176">Możesz ręcznie zgłosić śledzenia informacji (lub inne informacje specyficzne dla aplikacji) przy użyciu `sendAppInfo()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="30cf8-177">Należy pamiętać, że te informacje mogą być wysyłane przyrostowo.</span><span class="sxs-lookup"><span data-stu-id="30cf8-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="30cf8-178">Tylko najnowszą wartość dla określonego klucza zostaną zachowane dla określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="30cf8-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="30cf8-179">Podobnie jak dodatkowe zdarzenia służy dowolny obiekt JSON abstrakcyjnej informacje o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="30cf8-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="30cf8-180">Należy pamiętać, że tablice lub obiekty podrzędne są traktowane jako płaska ciągów (za pomocą serializacji JSON).</span><span class="sxs-lookup"><span data-stu-id="30cf8-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="30cf8-181">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="30cf8-181">**Example:**</span></span>

<span data-ttu-id="30cf8-182">Oto przykładowy kod do wysyłania płci użytkownika oraz data urodzenia:</span><span class="sxs-lookup"><span data-stu-id="30cf8-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="30cf8-183">Limity</span><span class="sxs-lookup"><span data-stu-id="30cf8-183">Limits</span></span>
<span data-ttu-id="30cf8-184">Ograniczenia, które są stosowane do informacji o aplikacji są w obszarach wyrażeń regularnych kluczy i rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="30cf8-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="30cf8-185">Klucze</span><span class="sxs-lookup"><span data-stu-id="30cf8-185">Keys</span></span>
<span data-ttu-id="30cf8-186">Każdy klucz w obiekcie musi odpowiadać następującym wyrażeniem regularnym:</span><span class="sxs-lookup"><span data-stu-id="30cf8-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="30cf8-187">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, po której następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="30cf8-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="30cf8-188">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="30cf8-188">Size</span></span>
<span data-ttu-id="30cf8-189">Informacje o aplikacji jest ograniczony do 1024 znaków na wywołanie (po zestaw SDK usługi Mobile Engagement Web kodowane w formacie JSON).</span><span class="sxs-lookup"><span data-stu-id="30cf8-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="30cf8-190">W powyższym przykładzie JSON na serwer wysyłane jest 44 znaków:</span><span class="sxs-lookup"><span data-stu-id="30cf8-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
