---
title: "Witaj tooUse aaaHow API zaangażowania na uniwersalnych systemu Windows"
description: "Jak tooUse hello API zaangażowania na uniwersalnych systemu Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a>Jak tooUse hello API zaangażowania na uniwersalnych systemu Windows
Ten dokument jest dodatek toohello [jak tooIntegrate zaangażowania na uniwersalnych systemu Windows](mobile-engagement-windows-store-integrate-engagement.md): dostarcza w głębokość szczegóły dotyczące sposobu toouse hello tooreport interfejsu API usługi Engagement statystyk aplikacji.

Należy pamiętać, że jeśli mają tylko tooreport zaangażowania sesji aplikacji, działań, awarii (Crash) i informacje techniczne, następnie hello Najprostszym sposobem jest toomake wszystkie Twoje `Page` klasy podrzędne dziedziczą hello `EngagementPage` klasy.

Jeśli chcesz, aby toodo więcej, na przykład, jeśli potrzebujesz tooreport aplikacji określonych zdarzeń, błędów i zadań, czy masz tooreport działania aplikacji w inny sposób niż jeden zaimplementowana w hello hello `EngagementPage` klas, wówczas należy toouse hello Interfejs API usługi Engagement.

Hello zaangażowania interfejsu API jest zapewniana przez hello `EngagementAgent` klasy. Można uzyskać dostępu do metody toothose za pośrednictwem `EngagementAgent.Instance`.

Nawet wtedy, gdy hello agenta modułu nie została zainicjowana, interfejsu API każdego wywołania toohello została odroczona i zostanie wykonana ponownie gdy hello agent jest dostępna.

## <a name="engagement-concepts"></a>Pojęcia dotyczące usługi Engagement
Hello następujące części uściślić hello wspólnej [Mobile Engagement pojęcia](mobile-engagement-concepts.md) dla platformy uniwersalnej systemu Windows hello.

### <a name="session-and-activity"></a>`Session` i `Activity`
*Działania* są zwykle skojarzone z jednej strony aplikacji hello, która jest toosay hello *działania* uruchamiana, gdy strona hello jest wyświetlany i zatrzymuje po zamknięciu strony hello: hello w przypadku gdy hello Engagement SDK jest zintegrowany przy użyciu hello `EngagementPage` klasy.

Ale *działania* można sterować także ręcznie przy użyciu hello interfejsu API usługi Engagement. Dzięki temu toosplit daną stronę w kilku sub tooget części więcej szczegółów na temat użycia hello tej strony (na przykład częstotliwość tooknow i jak długo okna dialogowe są używane wewnątrz tej strony).

## <a name="reporting-activities"></a>Działania raportowania
### <a name="user-starts-a-new-activity"></a>Użytkownik uruchamia nowe działanie
#### <a name="reference"></a>Dokumentacja
            void StartActivity(string name, Dictionary<object, object> extras = null)

Należy toocall `StartActivity()` każde działanie użytkownika hello czasu zmiany. Hello pierwszej wywołania funkcji toothis uruchamia nową sesję użytkownika.

> [!IMPORTANT]
> Hello SDK automatycznie wywołuje metodę EndActivity hello, gdy aplikacja hello jest zamknięty. W związku z tym zaleca toocall hello StartActivity metody podczas zmiany w natężeniu działań hello hello użytkownika i wywołania tooNEVER hello metody EndActivity, ponieważ wywołanie tej metody wymusza hello toobe bieżąca sesja została zakończona.
> 
> 

#### <a name="example"></a>Przykład
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>Użytkownik kończy swoje bieżące działanie
#### <a name="reference"></a>Dokumentacja
            void EndActivity()

Kończy działanie hello i hello sesji. Nie należy wywołać tej metody, znając naprawdę wykonywanych czynności.

#### <a name="example"></a>Przykład
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Zadania raportowania
### <a name="start-a-job"></a>Uruchom zadanie
#### <a name="reference"></a>Dokumentacja
            void StartJob(string name, Dictionary<object, object> extras = null)

Podaje tootrack zadania hello można użyć w danym okresie czasu.

#### <a name="example"></a>Przykład
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Zakończenia zadania
#### <a name="reference"></a>Dokumentacja
            void EndJob(string name)

Jak zadanie śledzone przez zadanie zostało zakończone, powinien wywoływać metodę EndJob powitania dla tego zadania, podając nazwę zadania hello.

#### <a name="example"></a>Przykład
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Zdarzenia raportowania
Brak trzy typy zdarzeń:

* Autonomiczny zdarzenia
* Zdarzenia sesji
* Zdarzenia zadań

### <a name="standalone-events"></a>Autonomiczny zdarzenia
#### <a name="reference"></a>Dokumentacja
            void SendEvent(string name, Dictionary<object, object> extras = null)

Autonomiczny zdarzeń może wystąpić poza hello kontekstu sesji.

#### <a name="example"></a>Przykład
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Zdarzenia sesji
#### <a name="reference"></a>Dokumentacja
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Zdarzenia sesji są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas jego sesji.

#### <a name="example"></a>Przykład
**Bez danych:**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**Z danymi:**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>Zdarzenia zadań
#### <a name="reference"></a>Dokumentacja
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Zdarzenia zadania są zazwyczaj używane tooreport hello akcje wykonywane przez użytkownika podczas wykonywania zadania.

#### <a name="example"></a>Przykład
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Raportowanie błędów
Istnieją trzy typy błędów:

* Błędy autonomiczny
* Błędy sesji
* Błędy zadań

### <a name="standalone-errors"></a>Błędy autonomiczny
#### <a name="reference"></a>Dokumentacja
            void SendError(string name, Dictionary<object, object> extras = null)

Błędy sprzeczne toosession poza hello kontekstu sesji mogą wystąpić błędy autonomicznych.

#### <a name="example"></a>Przykład
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Błędy sesji
#### <a name="reference"></a>Dokumentacja
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Błędy sesji są błędy hello zwykle używanych tooreport wpływające na powitania użytkownika podczas jego sesji.

#### <a name="example"></a>Przykład
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Błędy zadań
#### <a name="reference"></a>Dokumentacja
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Błędy mogą być powiązane tooa uruchomienia zadania zamiast powiązane toohello bieżącą sesję użytkownika.

#### <a name="example"></a>Przykład
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Raportowanie awarii (Crash)
Hello agent dostarcza dwóch metod toodeal awarii (Crash).

### <a name="send-an-exception"></a>Wyślij Wystąpił wyjątek
#### <a name="reference"></a>Dokumentacja
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Przykład
Wystąpił wyjątek w dowolnym momencie możesz wysłać przez wywołanie metody:

            EngagementAgent.Instance.SendCrash(aCatchedException);

Umożliwia także opcjonalny parametr tooterminate hello zaangażowania sesji na powitania tym samym czasie niż wysyłanie hello awarii. toodo tak, wywołania:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Jeśli możesz to zrobić, zadania i hello sesji zostanie zamknięte zaraz po awarii hello wysyłania.

### <a name="send-an-unhandled-exception"></a>Wyślij nieobsługiwany wyjątek
#### <a name="reference"></a>Dokumentacja
            void SendCrash(Exception e)

Jeśli masz zaangażowania również zapewnia wyjątki toosend nieobsługiwany — metoda **wyłączone** automatyczne zaangażowania **awarii** raportowania. Jest to szczególnie przydatne, gdy jest używany wewnątrz obsługi zdarzeń UnhandledException aplikacji hello.

Ta metoda będzie **zawsze** przerwanie hello zaangażowania sesji i zadania po wywołaniu.

#### <a name="example"></a>Przykład
Można użyć tooimplement własne UnhandledExceptionEventArgs programu obsługi. Na przykład dodać hello `Current_UnhandledException` metody hello `App.xaml.cs` pliku:

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

W pliku App.xaml.cs "Publicznego App() {}" należy dodać:

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a>Identyfikator urządzenia
            String EngagementAgent.Instance.GetDeviceId()

Identyfikator urządzenia usługi engagement hello można uzyskać przez wywołanie tej metody.

## <a name="extras-parameters"></a>Dodatkowe parametry
Dowolne dane można zdarzeń dołączonych tooan, błąd, działania lub zadania. Dane te mogą być elementami struktury, za pomocą słownika. Klucze i wartości mogą być dowolnego typu.

Dodatkowe dane są serializowane, więc jeśli chcesz tooinsert własne typu w dodatki masz tooadd kontraktu danych dla tego typu.

### <a name="example"></a>Przykład
Utworzymy nową klasę "Osoby".

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

Następnie dodamy `Person` dodatkowe tooan wystąpienia.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Jeśli inne typy obiektów, upewnij się, że ich metodę ToString() jest implementowane tooreturn człowieka czytelnych ciągów.
> 
> 

### <a name="limits"></a>Limity
#### <a name="keys"></a>Klucze
Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).

#### <a name="size"></a>Rozmiar
Dodatki są zbyt ograniczone**1024** znaków w wywołaniu.

## <a name="reporting-application-information"></a>Raportowanie informacji o aplikacji
### <a name="reference"></a>Dokumentacja
            void SendAppInfo(Dictionary<object, object> appInfos)

Można ręcznie raportu śledzenia informacji (lub innych aplikacji szczegółowych informacji) przy użyciu funkcji SendAppInfo() hello.

Należy pamiętać, że te dane mogą być wysyłane przyrostowo: tylko hello wartość najnowszej dla danego klucza zostaną zachowane dla danego urządzenia. Podobnie jak dodatkowe zdarzenia użycie słownika\<obiektu, obiekt\> tooattach danych.

### <a name="example"></a>Przykład
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Limity
#### <a name="keys"></a>Klucze
Każdy klucz w obiekcie hello musi odpowiadać hello następującego wyrażenia regularnego:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Oznacza to, że klucze musi rozpoczynać się od co najmniej jedną literą, następują litery, cyfry i znaki podkreślenia (\_).

#### <a name="size"></a>Rozmiar
Informacje o aplikacji są zbyt ograniczone**1024** znaków w wywołaniu.

W hello poprzedni przykład, hello JSON wysyłane toohello serwera jest 44 znaków:

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a>Rejestrowanie
### <a name="enable-logging"></a>Włączanie rejestrowania
Hello SDK może być skonfigurowany tooproduce dzienników testu w konsoli środowiska IDE hello.
Dzienniki te nie są uaktywnione domyślnie. toocustomize ta, właściwość hello aktualizacji `EngagementAgent.Instance.TestLogEnabled` tooone hello wartość dostępna hello `EngagementTestLogLevel` wyliczenia, na przykład:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

