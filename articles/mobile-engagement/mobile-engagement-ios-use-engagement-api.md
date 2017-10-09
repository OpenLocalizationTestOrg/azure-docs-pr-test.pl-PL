---
title: "aaaHow tooUse hello zaangażowania interfejsu API w systemie iOS"
description: "Najnowsze iOS SDK — jak tooUse hello zaangażowania interfejsu API w systemie iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a>Jak tooUse hello zaangażowania interfejsu API w systemie iOS
Ten dokument jest dodatek toohello jak tooIntegrate zaangażowania w systemie iOS: dostarcza w głębokość szczegóły dotyczące sposobu toouse hello tooreport interfejsu API usługi Engagement statystyk aplikacji.

Należy pamiętać, że jeśli mają tylko tooreport zaangażowania sesji aplikacji, działań, awarii (Crash) i informacje techniczne, następnie hello najprostszy sposób jest toomake wszystkie niestandardowe `UIViewController` obiekty dziedziczyć odpowiadającego hello `EngagementViewController` — klasa .

Jeśli chcesz, aby toodo więcej, na przykład, jeśli potrzebujesz tooreport aplikacji określonych zdarzeń, błędów i zadań, czy masz tooreport działania aplikacji w inny sposób niż jeden zaimplementowana w hello hello `EngagementViewController` klas, wówczas należy toouse hello Interfejs API usługi Engagement.

Hello zaangażowania interfejsu API jest zapewniana przez hello `EngagementAgent` klasy. Wystąpienie tej klasy może być pobierane przez wywołanie hello `[EngagementAgent shared]` metody statycznej (należy pamiętać, że hello `EngagementAgent` obiektu zwróconego jest pojedyncza).

Zanim wszystkie wywołania interfejsu API, hello `EngagementAgent` obiekt musi zostać zainicjowany przez wywołanie metody hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Pojęcia dotyczące usługi Engagement
Hello następujące części uściślić hello wspólnej [Mobile Engagement pojęcia](mobile-engagement-concepts.md) dla platformy iOS hello.

### <a name="session-and-activity"></a>`Session` i `Activity`
*Działania* są zwykle skojarzone z jednego ekranu aplikacji hello, która jest toosay hello *działania* uruchamiana, gdy hello ekran jest wyświetlany i zatrzymuje po zamknięciu ekranu hello: hello jest przypadek, kiedy Witaj Engagement SDK jest zintegrowany przy użyciu hello `EngagementViewController` klasy.

Ale *działania* można sterować także ręcznie przy użyciu hello interfejsu API usługi Engagement. Umożliwia to toosplit danego ekranu w kilku tooget części sub więcej szczegółów na temat hello użycia tego ekranu (na przykład częstotliwość tooknown i jak długo okna dialogowe są używane wewnątrz tego ekranu).

## <a name="reporting-activities"></a>Działania raportowania
### <a name="user-starts-a-new-activity"></a>Użytkownik uruchamia nowe działanie
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

Należy toocall `startActivity()` każde działanie użytkownika hello czasu zmiany. Hello pierwszej wywołania funkcji toothis uruchamia nową sesję użytkownika.

### <a name="user-ends-his-current-activity"></a>Użytkownik kończy swoje bieżące działanie
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> Należy **nigdy** wywołanie tej funkcji przez użytkownika, z wyjątkiem, jeśli chcesz, aby toosplit jedno użycie aplikacji na kilka sesji: wywołanie funkcji toothis spowodowałoby zakończenie hello bieżącej sesji, dlatego kolejne wywołanie za`startActivity()`czy Rozpocznij nową sesję. Ta funkcja jest wywoływana automatycznie przez hello zestawu SDK, po zamknięciu aplikacji.
> 
> 

## <a name="reporting-events"></a>Zdarzenia raportowania
### <a name="session-events"></a>Zdarzenia sesji
Zdarzenia sesji są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas jego sesji.

**Przykład bez dodatkowe dane:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

**Przykład: dodatkowe dane:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a>Autonomiczny zdarzenia
Zdarzenia toosession inaczej, zdarzenia autonomiczny można poza hello kontekstu sesji.

**Przykład:**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>Raportowanie błędów
### <a name="session-errors"></a>Błędy sesji
Błędy sesji są błędy hello zwykle używanych tooreport wpływające na powitania użytkownika podczas jego sesji.

**Przykład:**

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a>Błędy autonomiczny
Sprzeczne toosession błędy, błędy autonomiczny mogła być używana poza hello kontekstu sesji.

**Przykład:**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>Zadania raportowania
**Przykład:**

Załóżmy, że chcesz tooreport hello czas trwania procesu logowania:

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a>Zgłoś błędy podczas wykonywania zadania
Błędy mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.

**Przykład:**

Załóżmy, że chcesz tooreport wystąpił błąd podczas procesu logowania:

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a>Zdarzenia podczas wykonywania zadania
Zdarzenia mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.

**Przykład:**

Załóżmy, że mamy sieci społecznościowych i używamy zadania tooreport hello całkowity czas podczas którego hello użytkownika jest serwer połączony toohello. Witaj użytkownika mogą odbierać komunikaty z jego znajomych, to zdarzenia zadania.

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a>Dodatkowe parametry
Dowolne dane mogą być dołączone tooevents, błędów, działań i zadań.

Te dane mogą być elementami struktury, używa klasy NSDictionary dla systemu iOS.

Należy pamiętać, że może zawierać dodatkowe `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` lub innych `NSDictionary` wystąpień.

> [!NOTE]
> Witaj dodatkowy parametr jest serializowany w formacie JSON. Jeśli chcesz toopass różnych obiektów niż hello opisane powyżej, musi implementować następujące metody w klasie hello:
> 
> -(NSString*) JSONRepresentation;
> 
> Metoda Hello powinna zwrócić reprezentację obiektu w formacie JSON.
> 
> 

### <a name="example"></a>Przykład
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>Limity
#### <a name="keys"></a>Klucze
Każdy klucz w hello `NSDictionary` musi odpowiadać hello następującego wyrażenia regularnego:

`^[a-zA-Z][a-zA-Z_0-9]*`

Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).

#### <a name="size"></a>Rozmiar
Dodatki są zbyt ograniczone**1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez agenta zaangażowania hello).

W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 58 znaków:

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Raportowanie informacji o aplikacji
Można ręcznie raportu śledzenia informacji (lub innych aplikacji szczegółowych informacji) przy użyciu hello `sendAppInfo:` funkcji.

Należy pamiętać, że te informacje mogą zostać przesłane przyrostowo: tylko hello wartość najnowszej dla danego klucza zostaną zachowane dla danego urządzenia.

Takich jak dodatkowe zdarzenia hello `NSDictionary` klasa jest używana tooabstract informacje o aplikacji, należy pamiętać, że stałych lub słowników podrzędnej będzie traktowany jako płaska ciągów (za pomocą serializacji JSON).

**Przykład:**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>Limity
#### <a name="keys"></a>Klucze
Każdy klucz w hello `NSDictionary` musi odpowiadać hello następującego wyrażenia regularnego:

`^[a-zA-Z][a-zA-Z_0-9]*`

Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).

#### <a name="size"></a>Rozmiar
Informacje o aplikacji są zbyt ograniczone**1024** znaków na wywołanie (po zakodowaniu w formacie JSON przez agenta zaangażowania hello).

W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 44 znaków:

    {"birthdate":"1983-12-07","gender":"female"}
