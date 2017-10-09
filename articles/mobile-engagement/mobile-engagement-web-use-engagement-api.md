---
title: "aaaAzure interfejsów API zestawu Mobile Engagement sieci Web zestawu SDK | Dokumentacja firmy Microsoft"
description: "Witaj najnowsze aktualizacje i procedury dotyczące hello zestawu SDK sieci Web dla usługi Azure Mobile Engagement"
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
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="75e77-103">Użyj hello interfejsu API usługi Azure Mobile Engagement w aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="75e77-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="75e77-104">Ten dokument jest dodanie toohello informuje, jak za[zintegrowana usługa Mobile Engagement w aplikacji sieci web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="75e77-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="75e77-105">Zapewnia on szczegółowe informacje o jak toouse hello tooreport interfejsu API usługi Azure Mobile Engagement statystyk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="75e77-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="75e77-106">Witaj Mobile Engagement API są dostarczane przez hello `engagement.agent` obiektu.</span><span class="sxs-lookup"><span data-stu-id="75e77-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="75e77-107">Witaj domyślny zestaw SDK usługi Azure Mobile Engagement Web alias jest `engagement`.</span><span class="sxs-lookup"><span data-stu-id="75e77-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="75e77-108">Można zmienić ten alias z hello SDK konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="75e77-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="75e77-109">Pojęcia dotyczące usługi Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="75e77-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="75e77-110">Witaj następujące części uściślić wspólnej [pojęcia dotyczące usługi Mobile Engagement](mobile-engagement-concepts.md) hello platformy sieci web.</span><span class="sxs-lookup"><span data-stu-id="75e77-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="75e77-111">`Session` i `Activity`</span><span class="sxs-lookup"><span data-stu-id="75e77-111">`Session` and `Activity`</span></span>
<span data-ttu-id="75e77-112">Jeśli użytkownik hello pozostaje bezczynności więcej niż kilka sekund pomiędzy dwoma działaniami, hello sekwencję działań użytkownika jest podzielony na dwie różne sesje.</span><span class="sxs-lookup"><span data-stu-id="75e77-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="75e77-113">Te kilka sekund, są nazywane hello limit czasu sesji.</span><span class="sxs-lookup"><span data-stu-id="75e77-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="75e77-114">Aplikacji sieci web nie zadeklarować hello zakończenia działań użytkownika przez samego siebie (przez wywołanie hello `engagement.agent.endActivity` funkcji), serwer usługi Mobile Engagement hello automatycznie wygasa hello sesji użytkownika w ciągu trzech minut po zamknięciu strony aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="75e77-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="75e77-115">Jest to limit czasu sesji serwera hello.</span><span class="sxs-lookup"><span data-stu-id="75e77-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="75e77-116">Domyślnie nie są tworzone automatycznych raporty dotyczące nieprzechwyconych wyjątków JavaScript.</span><span class="sxs-lookup"><span data-stu-id="75e77-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="75e77-117">Jednak możesz zgłosić awarię ręcznie, używając hello `sendCrash` funkcji (patrz sekcja hello raportowania awarii).</span><span class="sxs-lookup"><span data-stu-id="75e77-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="75e77-118">Działania raportowania</span><span class="sxs-lookup"><span data-stu-id="75e77-118">Reporting activities</span></span>
<span data-ttu-id="75e77-119">Raporty dotyczące działań użytkownika zawiera gdy użytkownik uruchamia nowe działanie i hello użytkownika kończy się hello bieżącego działania.</span><span class="sxs-lookup"><span data-stu-id="75e77-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="75e77-120">Użytkownik uruchamia nowe działanie</span><span class="sxs-lookup"><span data-stu-id="75e77-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="75e77-121">Należy toocall `startActivity()` zmiany każdego działania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75e77-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="75e77-122">Hello pierwszej wywołania funkcji toothis uruchamia nową sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75e77-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="75e77-123">Użytkownik kończy się hello bieżące działanie</span><span class="sxs-lookup"><span data-stu-id="75e77-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="75e77-124">Należy toocall `endActivity()` co najmniej raz po hello użytkownik kończy swoje ostatnie działanie.</span><span class="sxs-lookup"><span data-stu-id="75e77-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="75e77-125">Użytkownik hello jest obecnie w stanie bezczynności, czy wymagane przez sesję użytkownika hello toobe zamknięte po upływie limitu czasu sesji hello informuje hello zestaw SDK usługi Mobile Engagement w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="75e77-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="75e77-126">Jeśli należy wywołać `startActivity()` przed upłynięciem limitu czasu sesji hello, po prostu wznowieniu sesji hello.</span><span class="sxs-lookup"><span data-stu-id="75e77-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="75e77-127">Ponieważ nie ma niezawodne składania po zamknięciu okna navigator hello, często jest trudne lub niemożliwe toocatch hello zakończenia działań użytkownika w środowisku sieci web.</span><span class="sxs-lookup"><span data-stu-id="75e77-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="75e77-128">Dlaczego jest który hello Mobile Engagement serwera automatycznie wygasa hello sesji użytkownika w ciągu trzech minut po stronie aplikacji hello jest zamknięty.</span><span class="sxs-lookup"><span data-stu-id="75e77-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="75e77-129">Zdarzenia raportowania</span><span class="sxs-lookup"><span data-stu-id="75e77-129">Reporting events</span></span>
<span data-ttu-id="75e77-130">Raporty dotyczące zdarzeń obejmuje zdarzenia sesji i autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="75e77-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="75e77-131">Zdarzenia sesji</span><span class="sxs-lookup"><span data-stu-id="75e77-131">Session events</span></span>
<span data-ttu-id="75e77-132">Zdarzenia sesji są zwykle używane tooreport hello akcje wykonywane przez użytkownika podczas sesji użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="75e77-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="75e77-133">**Przykład bez dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="75e77-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="75e77-134">**Przykład: dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="75e77-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="75e77-135">Autonomiczny zdarzenia</span><span class="sxs-lookup"><span data-stu-id="75e77-135">Standalone events</span></span>
<span data-ttu-id="75e77-136">W przeciwieństwie do sesji zdarzeń mogą występować zdarzenia autonomiczny poza kontekstem hello sesji.</span><span class="sxs-lookup"><span data-stu-id="75e77-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="75e77-137">Do tego użyć ``engagement.agent.sendEvent`` zamiast ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="75e77-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="75e77-138">Raportowanie błędów</span><span class="sxs-lookup"><span data-stu-id="75e77-138">Reporting errors</span></span>
<span data-ttu-id="75e77-139">Raportowanie błędów obejmuje błędy sesji i błędy autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="75e77-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="75e77-140">Błędy sesji</span><span class="sxs-lookup"><span data-stu-id="75e77-140">Session errors</span></span>
<span data-ttu-id="75e77-141">Błędy sesji są zwykle używane tooreport hello błędów, które mają wpływ na powitania użytkownika podczas sesji użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="75e77-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="75e77-142">**Przykład bez dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="75e77-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="75e77-143">**Przykład: dodatkowe dane:**</span><span class="sxs-lookup"><span data-stu-id="75e77-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="75e77-144">Błędy autonomiczny</span><span class="sxs-lookup"><span data-stu-id="75e77-144">Standalone errors</span></span>
<span data-ttu-id="75e77-145">W przeciwieństwie do błędów sesji mogą wystąpić błędy autonomiczny poza kontekstem hello sesji.</span><span class="sxs-lookup"><span data-stu-id="75e77-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="75e77-146">Do tego użyć `engagement.agent.sendError` zamiast `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="75e77-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="75e77-147">Zadania raportowania</span><span class="sxs-lookup"><span data-stu-id="75e77-147">Reporting jobs</span></span>
<span data-ttu-id="75e77-148">Raporty dotyczące obejmuje zadania raportowania błędów i zdarzeń występujących podczas wykonywania zadania i raportowania awarii (Crash).</span><span class="sxs-lookup"><span data-stu-id="75e77-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="75e77-149">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="75e77-149">**Example:**</span></span>

<span data-ttu-id="75e77-150">Jeśli chcesz toomonitor żądaniem AJAX, należy użyć następujących hello:</span><span class="sxs-lookup"><span data-stu-id="75e77-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="75e77-151">Raportowanie błędów podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="75e77-151">Reporting errors during a job</span></span>
<span data-ttu-id="75e77-152">Błędy mogą być powiązane tooa uruchomienia zadania zamiast toohello bieżącą sesję użytkownika.</span><span class="sxs-lookup"><span data-stu-id="75e77-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="75e77-153">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="75e77-153">**Example:**</span></span>

<span data-ttu-id="75e77-154">Jeśli chcesz, aby tooreport wystąpił błąd, jeśli żądanie AJAX nie powiodło się:</span><span class="sxs-lookup"><span data-stu-id="75e77-154">If you want tooreport an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="75e77-155">Zdarzenia raportowania podczas wykonywania zadania</span><span class="sxs-lookup"><span data-stu-id="75e77-155">Reporting events during a job</span></span>
<span data-ttu-id="75e77-156">Zdarzenia mogą być powiązane tooa uruchomienia zadania zamiast toohello bieżącej sesji użytkownika, dzięki toohello `engagement.agent.sendJobEvent` funkcji.</span><span class="sxs-lookup"><span data-stu-id="75e77-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="75e77-157">Ta funkcja działa dokładnie tak samo, jak `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="75e77-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="75e77-158">Raportowanie awarii (Crash)</span><span class="sxs-lookup"><span data-stu-id="75e77-158">Reporting crashes</span></span>
<span data-ttu-id="75e77-159">Użyj hello `sendCrash` tooreport funkcja awarii ręcznie.</span><span class="sxs-lookup"><span data-stu-id="75e77-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="75e77-160">Witaj `crashid` argument jest ciąg identyfikujący hello typu awarii (Crash).</span><span class="sxs-lookup"><span data-stu-id="75e77-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="75e77-161">Witaj `crash` argument jest zazwyczaj ślad stosu hello hello awarii (Crash) jako ciąg.</span><span class="sxs-lookup"><span data-stu-id="75e77-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="75e77-162">Dodatkowe parametry</span><span class="sxs-lookup"><span data-stu-id="75e77-162">Extra parameters</span></span>
<span data-ttu-id="75e77-163">Możesz dołączyć zdarzeń tooan dowolne dane, błąd, działania lub zadania.</span><span class="sxs-lookup"><span data-stu-id="75e77-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="75e77-164">Witaj danych może być dowolny obiekt JSON (ale nie tablicy lub typu pierwotnego).</span><span class="sxs-lookup"><span data-stu-id="75e77-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="75e77-165">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="75e77-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="75e77-166">Limity</span><span class="sxs-lookup"><span data-stu-id="75e77-166">Limits</span></span>
<span data-ttu-id="75e77-167">Ograniczenia dotyczące parametrów tooextra są w obszarach hello wyrażeń regularnych klucze, typy wartości i rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="75e77-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="75e77-168">Klucze</span><span class="sxs-lookup"><span data-stu-id="75e77-168">Keys</span></span>
<span data-ttu-id="75e77-169">Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="75e77-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="75e77-170">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, po której następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="75e77-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="75e77-171">Wartości</span><span class="sxs-lookup"><span data-stu-id="75e77-171">Values</span></span>
<span data-ttu-id="75e77-172">Wartości są ograniczone toostring, liczbę i typy Boolean.</span><span class="sxs-lookup"><span data-stu-id="75e77-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="75e77-173">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="75e77-173">Size</span></span>
<span data-ttu-id="75e77-174">Dodatki są ograniczone too1, 024 znaków na wywołanie (po hello zestaw SDK usługi Mobile Engagement Web kodowane w formacie JSON).</span><span class="sxs-lookup"><span data-stu-id="75e77-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="75e77-175">Raportowanie informacji o aplikacji</span><span class="sxs-lookup"><span data-stu-id="75e77-175">Reporting application information</span></span>
<span data-ttu-id="75e77-176">Możesz ręcznie zgłosić śledzenia informacji (lub inne informacje specyficzne dla aplikacji) przy użyciu hello `sendAppInfo()` funkcji.</span><span class="sxs-lookup"><span data-stu-id="75e77-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="75e77-177">Należy pamiętać, że te informacje mogą być wysyłane przyrostowo.</span><span class="sxs-lookup"><span data-stu-id="75e77-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="75e77-178">Tylko hello wartość najnowszej dla określonego klucza zostaną zachowane dla określonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="75e77-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="75e77-179">Podobnie jak dodatkowe zdarzenia można użyć żadnych informacji aplikacji tooabstract obiekt JSON.</span><span class="sxs-lookup"><span data-stu-id="75e77-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="75e77-180">Należy pamiętać, że tablice lub obiekty podrzędne są traktowane jako płaska ciągów (za pomocą serializacji JSON).</span><span class="sxs-lookup"><span data-stu-id="75e77-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="75e77-181">**Przykład:**</span><span class="sxs-lookup"><span data-stu-id="75e77-181">**Example:**</span></span>

<span data-ttu-id="75e77-182">Oto przykładowy kod, płci hello użytkownika wysyłania i Data urodzenia:</span><span class="sxs-lookup"><span data-stu-id="75e77-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="75e77-183">Limity</span><span class="sxs-lookup"><span data-stu-id="75e77-183">Limits</span></span>
<span data-ttu-id="75e77-184">Limity dotyczące tooapplication informacje znajdują się w obszarach hello wyrażeń regularnych kluczy i rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="75e77-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="75e77-185">Klucze</span><span class="sxs-lookup"><span data-stu-id="75e77-185">Keys</span></span>
<span data-ttu-id="75e77-186">Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:</span><span class="sxs-lookup"><span data-stu-id="75e77-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="75e77-187">Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, po której następują litery, cyfry i znaki podkreślenia (\_).</span><span class="sxs-lookup"><span data-stu-id="75e77-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="75e77-188">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="75e77-188">Size</span></span>
<span data-ttu-id="75e77-189">Informacje o aplikacji są ograniczone too1, 024 znaków na wywołanie (po hello zestaw SDK usługi Mobile Engagement Web kodowane w formacie JSON).</span><span class="sxs-lookup"><span data-stu-id="75e77-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="75e77-190">W hello poprzedzających przykład hello JSON wysłano toohello serwera jest 44 znaków:</span><span class="sxs-lookup"><span data-stu-id="75e77-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
