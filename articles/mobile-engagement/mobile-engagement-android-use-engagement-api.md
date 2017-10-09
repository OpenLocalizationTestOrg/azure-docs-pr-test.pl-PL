---
title: "Witaj tooUse aaaHow API zaangażowania w systemie Android"
description: "Najnowszy zestaw SDK systemu Android — jak tooUse hello API zaangażowania w systemie Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a>Jak tooUse hello API zaangażowania w systemie Android
Ten dokument jest dodatek toohello [opcje zaawansowane raportowanie dla systemu Android zestaw SDK usługi Mobile Engagement](mobile-engagement-android-advanced-reporting.md). Zapewnia on głębokość szczegóły dotyczące sposobu toouse hello tooreport interfejsu API usługi Engagement statystyk aplikacji.

Należy pamiętać, że jeśli mają tylko tooreport zaangażowania sesji aplikacji, działań, awarii (Crash) i informacje techniczne, następnie hello Najprostszym sposobem jest toomake wszystkie Twoje `Activity` klasy podrzędne dziedziczą odpowiadającego hello `EngagementActivity` klasy.

Jeśli chcesz, aby toodo więcej, na przykład, jeśli potrzebujesz tooreport aplikacji określonych zdarzeń, błędów i zadań, czy masz tooreport działania aplikacji w inny sposób niż jeden zaimplementowana w hello hello `EngagementActivity` klas, wówczas należy toouse hello Interfejs API usługi Engagement.

Hello zaangażowania interfejsu API jest zapewniana przez hello `EngagementAgent` klasy. Wystąpienie tej klasy może być pobierane przez wywołanie hello `EngagementAgent.getInstance(Context)` metody statycznej (należy pamiętać, że hello `EngagementAgent` obiektu zwróconego jest pojedyncza).

## <a name="engagement-concepts"></a>Pojęcia dotyczące usługi Engagement
Hello następujące części uściślić hello wspólnej [Mobile Engagement pojęcia](mobile-engagement-concepts.md), hello platformy Android.

### <a name="session-and-activity"></a>`Session` i `Activity`
Jeśli użytkownik hello pozostaje więcej niż kilka sekund bezczynności między dwiema *działania*, następnie ta sekwencja z *działania* jest podzielony na dwie różne *sesji*. Te kilka sekund, są nazywane hello "limit czasu sesji".

*Działania* są zwykle skojarzone z jednego ekranu aplikacji hello, która jest toosay hello *działania* uruchamiana, gdy hello ekran jest wyświetlany i zatrzymuje po zamknięciu ekranu hello: hello jest przypadek, kiedy Witaj Engagement SDK jest zintegrowany przy użyciu hello `EngagementActivity` klasy.

Ale *działania* można sterować także ręcznie przy użyciu hello interfejsu API usługi Engagement. Umożliwia to toosplit danego ekranu w kilku tooget części sub więcej szczegółów na temat hello użycia tego ekranu (na przykład częstotliwość tooknown i jak długo okna dialogowe są używane wewnątrz tego ekranu).

## <a name="reporting-activities"></a>Działania raportowania
> [!IMPORTANT]
> Nie ma potrzeby tooreport działań, takich jak opisane w tej sekcji, jeśli używasz hello `EngagementActivity` klasy i jej wariantów zgodnie z objaśnieniem w hello jak tooIntegrate Engagement Android dokumentu.
> 
> 

### <a name="user-starts-a-new-activity"></a>Użytkownik uruchamia nowe działanie
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

Należy toocall `startActivity()` każde działanie użytkownika hello czasu zmiany. Hello pierwszej wywołania funkcji toothis uruchamia nową sesję użytkownika.

Witaj najlepsze miejsce toocall, ta funkcja jest na każde działanie `onResume` wywołania zwrotnego.

### <a name="user-ends-his-current-activity"></a>Użytkownik kończy swoje bieżące działanie
            EngagementAgent.getInstance(this).endActivity();

Należy toocall `endActivity()` co najmniej raz, gdy użytkownik hello kończy swoje ostatnie działanie. Informuje hello Engagement SDK hello użytkownik jest obecnie w stanie bezczynności, czy że sesji użytkownika hello muszą toobe zamknąć raz limit czasu sesji hello wygaśnie (jeśli wywołujesz `startActivity()` przed upłynięciem limitu czasu sesji hello, po prostu wznowieniu sesji hello).

Witaj najlepsze miejsce toocall, ta funkcja jest na każde działanie `onPause` wywołania zwrotnego.

## <a name="reporting-events"></a>Zdarzenia raportowania
### <a name="session-events"></a>Zdarzenia sesji
Zdarzenia sesji są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas jego sesji.

**Przykład bez dodatkowe dane:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Przykład: dodatkowe dane:**

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a>Autonomiczny zdarzenia
Zdarzenia toosession sprzeczne poza hello kontekstu sesji mogą występować zdarzenia autonomicznych.

**Przykład:**

Załóżmy, że tooreport zdarzenia występujące po wyzwoleniu emisji odbiornik:

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Raportowanie błędów
### <a name="session-errors"></a>Błędy sesji
Błędy sesji są błędy hello zwykle używanych tooreport wpływające na powitania użytkownika podczas jego sesji.

**Przykład:**

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a>Błędy autonomiczny
Błędy sprzeczne toosession poza hello kontekstu sesji mogą wystąpić błędy autonomicznych.

**Przykład:**

Witaj poniższy przykład przedstawia sposób tooreport wystąpił błąd, gdy pamięć hello staje się niskim w telefonie hello podczas procesu aplikacji jest uruchomiony.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Zadania raportowania
### <a name="example"></a>Przykład
Załóżmy, że chcesz tooreport hello czas trwania procesu logowania:

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a>Zgłoś błędy podczas wykonywania zadania
Błędy mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.

**Przykład:**

Załóżmy, że chcesz tooreport wystąpił błąd podczas możesz zalogować się proces:

[...] publiczny rejestrowanie void (kontekstu kontekstu,...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a>Zdarzenia raportowania podczas wykonywania zadania
Zdarzenia mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.

**Przykład:**

Załóżmy, że mamy sieci społecznościowych i używamy zadania tooreport hello całkowity czas podczas którego hello użytkownika jest serwer połączony toohello. Witaj użytkownika można łączność w tle nawet wtedy, gdy jest on za pomocą innej aplikacji, lub gdy hello phone jest uśpiony, więc nie ma żadnej sesji.

Witaj użytkownika mogą odbierać komunikaty z jego znajomych, to zdarzenia zadania.

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a>Dodatkowe parametry
Dowolne dane mogą być dołączone tooevents, błędów, działań i zadań.

Te dane mogą być elementami struktury, używa klasy pakietu dla systemu Android (w rzeczywistości działa jak dodatkowe parametry w lokalizacji docelowych z systemem Android). Należy pamiętać, że pakiet może zawierać tablic lub innego wystąpienia pakietu.

> [!IMPORTANT]
> Jeśli umieścisz w parcelable lub które można serializować parametrów, upewnij się, ich `toString()` metoda jest implementowane tooreturn ciąg zrozumiałą dla użytkownika. Klas możliwych do serializacji, zawierające pola z systemem innym niż przejściowy, które nie są serializacji spowoduje awarii systemu Android, gdy będzie wywoływać`bundle.putSerializable("key",value);`
> 
> [!WARNING]
> Tablice rozrzedzonych w dodatkowe parametry nie są obsługiwane, oznacza to, że nie można serializować jako tablica. Należy przekonwertować je na standardowe tablice przed jego użyciem w dodatkowe parametry.
> 
> 

### <a name="example"></a>Przykład
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Limity
#### <a name="keys"></a>Klucze
Każdy klucz w hello `Bundle` musi odpowiadać hello następującego wyrażenia regularnego:

`^[a-zA-Z][a-zA-Z_0-9]*`

Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).

#### <a name="size"></a>Rozmiar
Dodatki są zbyt ograniczone**1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez usługę zaangażowania hello).

W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 58 znaków:

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Raportowanie informacji o aplikacji
Można ręcznie raportu śledzenia informacji (lub innych aplikacji szczegółowych informacji) przy użyciu hello `sendAppInfo()` funkcji.

Należy pamiętać, że te informacje mogą zostać przesłane przyrostowo: tylko hello wartość najnowszej dla danego klucza zostaną zachowane dla danego urządzenia.

Podobnie jak dodatkowe zdarzenia hello klasy pakietu jest używane tooabstract informacje o aplikacji, należy pamiętać, że stałych lub podrzędna zawiera będzie traktowany jako płaska ciągów (za pomocą serializacji JSON).

### <a name="example"></a>Przykład
Oto kod przykładowy toosend użytkownika płci i Data urodzenia:

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>Limity
#### <a name="keys"></a>Klucze
Każdy klucz w hello `Bundle` musi odpowiadać hello następującego wyrażenia regularnego:

`^[a-zA-Z][a-zA-Z_0-9]*`

Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).

#### <a name="size"></a>Rozmiar
Informacje o aplikacji są zbyt ograniczone**1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez usługę zaangażowania hello).

W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 44 znaków:

            {"expiration":"2016-12-07","status":"premium"}
