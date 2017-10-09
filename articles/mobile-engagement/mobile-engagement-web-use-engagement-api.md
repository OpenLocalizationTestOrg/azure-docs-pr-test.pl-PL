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
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>Użyj hello interfejsu API usługi Azure Mobile Engagement w aplikacji sieci web
Ten dokument jest dodanie toohello informuje, jak za[zintegrowana usługa Mobile Engagement w aplikacji sieci web](mobile-engagement-web-integrate-engagement.md). Zapewnia on szczegółowe informacje o jak toouse hello tooreport interfejsu API usługi Azure Mobile Engagement statystyk aplikacji.

Witaj Mobile Engagement API są dostarczane przez hello `engagement.agent` obiektu. Witaj domyślny zestaw SDK usługi Azure Mobile Engagement Web alias jest `engagement`. Można zmienić ten alias z hello SDK konfiguracji.

## <a name="mobile-engagement-concepts"></a>Pojęcia dotyczące usługi Mobile Engagement
Witaj następujące części uściślić wspólnej [pojęcia dotyczące usługi Mobile Engagement](mobile-engagement-concepts.md) hello platformy sieci web.

### <a name="session-and-activity"></a>`Session` i `Activity`
Jeśli użytkownik hello pozostaje bezczynności więcej niż kilka sekund pomiędzy dwoma działaniami, hello sekwencję działań użytkownika jest podzielony na dwie różne sesje. Te kilka sekund, są nazywane hello limit czasu sesji.

Aplikacji sieci web nie zadeklarować hello zakończenia działań użytkownika przez samego siebie (przez wywołanie hello `engagement.agent.endActivity` funkcji), serwer usługi Mobile Engagement hello automatycznie wygasa hello sesji użytkownika w ciągu trzech minut po zamknięciu strony aplikacji hello. Jest to limit czasu sesji serwera hello.

### `Crash`
Domyślnie nie są tworzone automatycznych raporty dotyczące nieprzechwyconych wyjątków JavaScript. Jednak możesz zgłosić awarię ręcznie, używając hello `sendCrash` funkcji (patrz sekcja hello raportowania awarii).

## <a name="reporting-activities"></a>Działania raportowania
Raporty dotyczące działań użytkownika zawiera gdy użytkownik uruchamia nowe działanie i hello użytkownika kończy się hello bieżącego działania.

### <a name="user-starts-a-new-activity"></a>Użytkownik uruchamia nowe działanie
    engagement.agent.startActivity("MyUserActivity");

Należy toocall `startActivity()` zmiany każdego działania użytkownika. Hello pierwszej wywołania funkcji toothis uruchamia nową sesję użytkownika.

### <a name="user-ends-hello-current-activity"></a>Użytkownik kończy się hello bieżące działanie
    engagement.agent.endActivity();

Należy toocall `endActivity()` co najmniej raz po hello użytkownik kończy swoje ostatnie działanie. Użytkownik hello jest obecnie w stanie bezczynności, czy wymagane przez sesję użytkownika hello toobe zamknięte po upływie limitu czasu sesji hello informuje hello zestaw SDK usługi Mobile Engagement w sieci Web. Jeśli należy wywołać `startActivity()` przed upłynięciem limitu czasu sesji hello, po prostu wznowieniu sesji hello.

Ponieważ nie ma niezawodne składania po zamknięciu okna navigator hello, często jest trudne lub niemożliwe toocatch hello zakończenia działań użytkownika w środowisku sieci web. Dlaczego jest który hello Mobile Engagement serwera automatycznie wygasa hello sesji użytkownika w ciągu trzech minut po stronie aplikacji hello jest zamknięty.

## <a name="reporting-events"></a>Zdarzenia raportowania
Raporty dotyczące zdarzeń obejmuje zdarzenia sesji i autonomicznych.

### <a name="session-events"></a>Zdarzenia sesji
Zdarzenia sesji są zwykle używane tooreport hello akcje wykonywane przez użytkownika podczas sesji użytkownika hello.

**Przykład bez dodatkowe dane:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**Przykład: dodatkowe dane:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>Autonomiczny zdarzenia
W przeciwieństwie do sesji zdarzeń mogą występować zdarzenia autonomiczny poza kontekstem hello sesji.

Do tego użyć ``engagement.agent.sendEvent`` zamiast ``engagement.agent.sendSessionEvent``.

## <a name="reporting-errors"></a>Raportowanie błędów
Raportowanie błędów obejmuje błędy sesji i błędy autonomicznych.

### <a name="session-errors"></a>Błędy sesji
Błędy sesji są zwykle używane tooreport hello błędów, które mają wpływ na powitania użytkownika podczas sesji użytkownika hello.

**Przykład bez dodatkowe dane:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**Przykład: dodatkowe dane:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>Błędy autonomiczny
W przeciwieństwie do błędów sesji mogą wystąpić błędy autonomiczny poza kontekstem hello sesji.

Do tego użyć `engagement.agent.sendError` zamiast `engagement.agent.sendSessionError`.

## <a name="reporting-jobs"></a>Zadania raportowania
Raporty dotyczące obejmuje zadania raportowania błędów i zdarzeń występujących podczas wykonywania zadania i raportowania awarii (Crash).

**Przykład:**

Jeśli chcesz toomonitor żądaniem AJAX, należy użyć następujących hello:

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

### <a name="reporting-errors-during-a-job"></a>Raportowanie błędów podczas wykonywania zadania
Błędy mogą być powiązane tooa uruchomienia zadania zamiast toohello bieżącą sesję użytkownika.

**Przykład:**

Jeśli chcesz, aby tooreport wystąpił błąd, jeśli żądanie AJAX nie powiodło się:

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

### <a name="reporting-events-during-a-job"></a>Zdarzenia raportowania podczas wykonywania zadania
Zdarzenia mogą być powiązane tooa uruchomienia zadania zamiast toohello bieżącej sesji użytkownika, dzięki toohello `engagement.agent.sendJobEvent` funkcji.

Ta funkcja działa dokładnie tak samo, jak `engagement.agent.sendJobError`.

### <a name="reporting-crashes"></a>Raportowanie awarii (Crash)
Użyj hello `sendCrash` tooreport funkcja awarii ręcznie.

Witaj `crashid` argument jest ciąg identyfikujący hello typu awarii (Crash).
Witaj `crash` argument jest zazwyczaj ślad stosu hello hello awarii (Crash) jako ciąg.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>Dodatkowe parametry
Możesz dołączyć zdarzeń tooan dowolne dane, błąd, działania lub zadania.

Witaj danych może być dowolny obiekt JSON (ale nie tablicy lub typu pierwotnego).

**Przykład:**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>Limity
Ograniczenia dotyczące parametrów tooextra są w obszarach hello wyrażeń regularnych klucze, typy wartości i rozmiaru.

#### <a name="keys"></a>Klucze
Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:

    ^[a-zA-Z][a-zA-Z_0-9]*

Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, po której następują litery, cyfry i znaki podkreślenia (\_).

#### <a name="values"></a>Wartości
Wartości są ograniczone toostring, liczbę i typy Boolean.

#### <a name="size"></a>Rozmiar
Dodatki są ograniczone too1, 024 znaków na wywołanie (po hello zestaw SDK usługi Mobile Engagement Web kodowane w formacie JSON).

## <a name="reporting-application-information"></a>Raportowanie informacji o aplikacji
Możesz ręcznie zgłosić śledzenia informacji (lub inne informacje specyficzne dla aplikacji) przy użyciu hello `sendAppInfo()` funkcji.

Należy pamiętać, że te informacje mogą być wysyłane przyrostowo. Tylko hello wartość najnowszej dla określonego klucza zostaną zachowane dla określonego urządzenia.

Podobnie jak dodatkowe zdarzenia można użyć żadnych informacji aplikacji tooabstract obiekt JSON. Należy pamiętać, że tablice lub obiekty podrzędne są traktowane jako płaska ciągów (za pomocą serializacji JSON).

**Przykład:**

Oto przykładowy kod, płci hello użytkownika wysyłania i Data urodzenia:

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>Limity
Limity dotyczące tooapplication informacje znajdują się w obszarach hello wyrażeń regularnych kluczy i rozmiaru.

#### <a name="keys"></a>Klucze
Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:

    ^[a-zA-Z][a-zA-Z_0-9]*

Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, po której następują litery, cyfry i znaki podkreślenia (\_).

#### <a name="size"></a>Rozmiar
Informacje o aplikacji są ograniczone too1, 024 znaków na wywołanie (po hello zestaw SDK usługi Mobile Engagement Web kodowane w formacie JSON).

W hello poprzedzających przykład hello JSON wysłano toohello serwera jest 44 znaków:

    {"birthdate":"1983-12-07","gender":"female"}
