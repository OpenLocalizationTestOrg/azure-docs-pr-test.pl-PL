---
title: "aaaWindows uniwersalnych zaawansowane raporty dzięki MobileApps zaangażowania"
description: "Jak tooIntegrate usługi Azure Mobile Engagement z uniwersalnych aplikacji systemu Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>Zaawansowane raportowanie z hello SDK zaangażowania aplikacji uniwersalnych systemu Windows
> [!div class="op_single_selector"]
> * [Platforma uniwersalna systemu Windows](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

W tym temacie opisano dodatkowe scenariusze raportowania w aplikacji uniwersalnych systemu Windows. Te scenariusze obejmują opcje, które można wybrać tooapply toohello aplikacji utworzonych w hello [wprowadzenie](mobile-engagement-windows-store-dotnet-get-started.md) samouczka.

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

Przed rozpoczęciem tego samouczka, należy najpierw wykonać hello [wprowadzenie](mobile-engagement-windows-store-dotnet-get-started.md) samouczka jest celowo bezpośredniego i prosty. Ten samouczek obejmuje dodatkowe opcje, które są dostępne.

## <a name="specifying-engagement-configuration-at-runtime"></a>Określenie konfiguracji zaangażowania w czasie wykonywania
konfiguracji usługi Engagement Hello jest scentralizowana w hello `Resources\EngagementConfiguration.xml` pliku projektu jest, gdzie został określony w hello [wprowadzenie](mobile-engagement-windows-store-dotnet-get-started.md) tematu.

Można jednak również określić go w czasie wykonywania: należy wywołać hello następujące metody przed zainicjowaniem agenta zaangażowania hello:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>Zalecana metoda: przeciążenia sieci `Page` klas
tooactivate hello raportowanie wszystkie dzienniki hello wymagane przez zaangażowania toocompute użytkowników, sesji, działania, awarii (Crash) i statystyki technicznych, wprowadź wszystkie Twoje `Page` klasy podrzędne dziedziczą hello `EngagementPage` klasy.

Oto przykład strony aplikacji. Możesz zrobić hello samo dla wszystkich stron w aplikacji.

### <a name="c-source-file"></a>Plik źródłowy języka C#
Zmodyfikuj stronę `.xaml.cs` pliku:

* Dodaj tooyour `using` instrukcji:
  
      using Microsoft.Azure.Engagement;
* Zastąp `Page` z `EngagementPage`:

**Bez usługi Engagement:**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**Z usługi Engagement:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> Jeśli strona zastępuje hello `OnNavigatedTo` metody, należy się toocall `base.OnNavigatedTo(e)`. W przeciwnym razie hello działania nie został zgłoszony (hello `EngagementPage` wywołania `StartActivity` wewnątrz jego `OnNavigatedTo` metody).
> 
> 

### <a name="xaml-file"></a>Plik XAML
Zmodyfikuj stronę `.xaml` pliku:

* Dodaj deklaracje przestrzeni nazw tooyour:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* Zastąp `Page` z `engagement:EngagementPage`:

**Bez usługi Engagement:**

        <Page>
            <!-- layout -->
            ...
        </Page>

**Z usługi Engagement:**

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a>Zastąpienie zachowania domyślnego hello
Domyślnie nazwa klasy hello strony hello został zgłoszony jako nazwę działania hello, bez dodatkowych. Jeśli klasa hello korzysta z sufiksem "Page" hello, Engagement usuwa go.

toooverride hello domyślne zachowanie dla nazwy hello, Dodaj ten kod:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport dodatkowe informacje o Twoich działaniach, Dodaj ten kod:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Te metody są wywoływane z wewnątrz hello `OnNavigatedTo` metody na stronie.

### <a name="alternate-method-call-startactivity-manually"></a>Alternatywna metoda: wywołanie `StartActivity()` ręcznie
Jeśli nie możesz lub nie ma toooverload Twojego `Page` klas, zamiast tego można uruchomić działań przez wywołanie metody `EngagementAgent` metody bezpośrednio.

Firma Microsoft zaleca wywoływania `StartActivity` wewnątrz sieci `OnNavigatedTo` metody na stronie.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Upewnij się, że prawidłowo zakończyć sesję.
> 
> Witaj uniwersalnego zestawu SDK automatycznie wywołuje hello `EndActivity` metody, gdy aplikacja hello jest zamknięty. W związku z tym jest **wysokiej** zalecane toocall hello `StartActivity` metody zmianie działania hello hello użytkownika i zbyt**nigdy** hello wywołania `EndActivity` — metoda. Ta metoda powiadamia hello zaangażowania serwera bieżącego użytkownika hello opuścił aplikacji hello, która będzie miało wpływ na wszystkie dzienniki aplikacji.
> 
> 

## <a name="advanced-reporting"></a>Zaawansowane raportowanie
Opcjonalnie możesz tooreport zdarzenia specyficzne dla aplikacji, błędy i zadań, toodo tak, użyj hello innych metod znalezione w hello `EngagementAgent` klasy. Hello zaangażowania API umożliwia korzystanie z zaawansowanych możliwości wszystkich zaangażowania.

Aby uzyskać więcej informacji, zobacz [jak toouse hello zaawansowane znakowanie interfejsu API w aplikacji uniwersalnych systemu Windows usługi Mobile Engagement](mobile-engagement-windows-store-use-engagement-api.md).

