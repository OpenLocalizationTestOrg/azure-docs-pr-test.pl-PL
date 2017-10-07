---
title: "wprowadzenie do systemu Windows Universal aplikacji usługi Azure Mobile Engagement aaaGet"
description: "Dowiedz się, jak toouse usługi Azure Mobile Engagement z analizy i powiadomieniami wypychanymi dla aplikacji uniwersalnych systemu Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Wprowadzenie do usługi Azure Mobile Engagement na potrzeby uniwersalnych aplikacji systemu Windows
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

W tym temacie opisano sposób toounderstand usługi Azure Mobile Engagement toouse użycia aplikacji, a wysłać wypychanie powiadomień użytkowników toosegmented aplikacji uniwersalnych systemu Windows.
W tym samouczku przedstawiono hello Prosty scenariusz emisji przy użyciu usługi Mobile Engagement. Utworzysz pustą uniwersalną aplikację systemu Windows, za pomocą której będą zbierane dane dotyczące zużycia i odbierane powiadomienia wypychane przy użyciu Usługi powiadomień systemu Windows.

> [!NOTE]
> Usługa Azure Mobile Engagement Hello zostaną wycofane 2018 marca i jest obecnie tylko dostępne tooexisting klientów. Aby uzyskać więcej informacji, zobacz [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

## <a name="prerequisites"></a>Wymagania wstępne
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Konfigurowanie usługi Mobile Engagement dla aplikacji uniwersalnej systemu Windows
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Połączenie z zapleczem usługi Mobile Engagement toohello aplikacji
Ten samouczek przedstawia "podstawową integrację", który czy hello minimalny wymagany toocollect danych i wysyłania powiadomień wypychanych. Witaj kompletna dokumentacja integracji znajduje się w hello [integracja zestawu Mobile Engagement Windows Universal SDK](mobile-engagement-windows-store-sdk-overview.md).

Utworzeniu Podstawowa aplikacja za pomocą programu Visual Studio toodemonstrate hello integracji.

### <a name="create-a-windows-universal-app-project"></a>Tworzenie projektu aplikacji uniwersalnej systemu Windows
Hello następujących krokach założono użycie hello programu Visual Studio 2015 chociaż hello kroki są podobne we wcześniejszych wersjach programu Visual Studio.

1. Uruchom program Visual Studio w hello **Home** ekranu wybierz **nowy projekt**.
2. W oknie podręcznym hello wybierz **Windows** -> **uniwersalnych** -> **pusta aplikacja (uniwersalna systemu Windows)**. Wypełnij aplikacji hello **nazwa** i **Nazwa rozwiązania**, a następnie kliknij przycisk **OK**.

    ![][1]

Został utworzony projekt aplikacji uniwersalnej systemu Windows, do którego obok integracji hello zestaw SDK usługi Azure Mobile Engagement.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Połącz zapleczu swojej aplikacji tooMobile zaangażowania
1. Zainstaluj hello [MicrosoftAzure.MobileEngagement] pakietu Nuget w projekcie. Jeśli ma być przeznaczona dla platform systemów Windows i Windows Phone, musisz toodo to dla obu tych projektów. Dla systemu Windows 8.x i Windows Phone 8.1, hello tego samego Nuget pakietu miejsca hello poprawne specyficzne dla platformy pliki binarne w każdym projekcie.
2. Otwórz **Package.appxmanifest** i upewnij się, że dodano tego hello następujące możliwości:

        Internet (Client)

    ![][2]
3. Teraz skopiuj parametry połączenia hello, które wcześniej zostały skopiowane dla aplikacji usługi Mobile Engagement i wklej go w hello `Resources\EngagementConfiguration.xml` plików między hello `<connectionString>` i `</connectionString>` tagów:

    ![][3]

    > [!TIP]
    > Jeśli aplikacja jest przeznaczona zarówno dla platformy Windows, jak i Windows Phone, nadal powinny zostać utworzone dwie aplikacje usługi Mobile Engagement — jedna dla każdej z obsługiwanych platform. Mając dwie aplikacje gwarantuje, że można utworzyć poprawnej segmentacji odbiorców hello i można wysyłanie odpowiednio skierowanych powiadomień dla każdej platformy.

    > [!IMPORTANT]
    > NuGet nie kopiuje automatycznie hello zasobów zestawu SDK w aplikacji platformy uniwersalnej systemu Windows do systemu Windows 10. Masz toodo go ręcznie następujące kroki hello, które widać (readme.txt) jest zainstalowany pakiet Nuget hello.  

1. W hello `App.xaml.cs` pliku:

    a. Dodaj hello `using` instrukcji:

            using Microsoft.Azure.Engagement;

    b. Dodaj metodę, która inicjuje hello Engagement:

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Inicjowanie hello zestawu SDK w hello **OnLaunched** metody:

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Wstaw następujące hello w hello **OnActivated** — metoda i Dodawanie metody hello, jeśli nie jest już istnieje:

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>Włączanie monitorowania w czasie rzeczywistym
toostart wysyłanie danych i zapewnienia, że hello użytkownicy są aktywni, konieczne jest wysłanie co najmniej jeden zapleczem usługi Mobile Engagement toohello ekranu (działanie).

1. W hello **MainPage.xaml.cs**, Dodaj następujące hello `using` instrukcji:

    using Microsoft.Azure.Engagement.Overlay;
2. Zmień klasę podstawową hello **MainPage** z **strony** za**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. W hello `MainPage.xaml` pliku:

    a. Dodaj deklaracje przestrzeni nazw tooyour:

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Zastąp hello **strony** w nazwie tagu XML hello z **engagement: EngagementPageOverlay**

> [!IMPORTANT]
> Jeśli strona zastępuje hello `OnNavigatedTo` metody, należy się toocall `base.OnNavigatedTo(e)`. W przeciwnym razie hello działania nie został zgłoszony `EngagementPage` wywołania `StartActivity` wewnątrz jego `OnNavigatedTo` metody). Jest to szczególnie ważne w projekcie Windows Phone, gdzie ma hello domyślny szablon `OnNavigatedTo` metody.
>
> Dla **aplikacji uniwersalnych systemu Windows 10**, należy użyć metody hello zalecane w hello "zalecana metoda: przeciążenia klas strony" sekcji [zaawansowane raporty dzięki hello Windows Universal SDK zaangażowania aplikacji](mobile-engagement-windows-store-advanced-reporting.md) , zamiast hello jedną wymienionych powyżej.

## <a id="monitor"></a>Łączenie aplikacji z funkcją monitorowania w czasie rzeczywistym
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Włączanie powiadomień wypychanych i funkcji komunikatów w aplikacji
Usługa Mobile Engagement umożliwia toointeract i użytkownikami przy użyciu powiadomień wypychanych i komunikatów w kontekście kampanii hello w aplikacji. Ten moduł ma nazwę REACH w portalu Mobile Engagement hello.
Witaj sekcje skonfigurować tooreceive Twojej aplikacji je.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>Włącz tooreceive Twojej aplikacji powiadomień wypychanych usługi WNS
1. W hello `Package.appxmanifest` pliku w hello **aplikacji** , w obszarze **powiadomienia**ustaw **wyskakujące funkcją:** zbyt**tak**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>Inicjowanie hello OSIĄGNĄĆ zestawu SDK
W `App.xaml.cs`, wywołaj **EngagementReach.Instance.Init(e);** w hello **InitEngagement** bezpośrednio po zainicjowaniu agenta hello:

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

Wszystko jest gotowe toosend wyskakującego powiadomienia. Następnie zweryfikujemy, czy podstawowa integracja została przeprowadzona prawidłowo.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>Udziel dostępu tooMobile zaangażowania toosend powiadomienia
1. Otwórz [Centrum deweloperów Sklepu Windows] w przeglądarce internetowej, a następnie zaloguj się i utwórz konto, jeśli to konieczne.
2. Kliknij przycisk **pulpitu nawigacyjnego** na powitania prawym górnym rogu, a następnie kliknij przycisk **Utwórz nową aplikację** z menu lewego panelu hello.

    ![][9]
3. Utwórz aplikację przez zarezerwowanie jej nazwy.

    ![][10]
4. Po utworzeniu aplikacji hello Przejdź zbyt**usługi -> powiadomienia wypychane** z menu po lewej stronie powitania.

    ![][11]
5. W hello Push sekcji powiadomień, kliknij przycisk hello **witryna usług Live** łącza.

    ![][12]
6. Możesz przejść sekcji poświadczeń wypychania toohello. Upewnij się, że jesteś w hello **ustawień aplikacji** sekcji, a następnie skopiuj z **identyfikatora SID pakietu** i **klucz tajny klienta**

    ![][13]
7. Przejdź toohello **ustawienia** z portalu usługi Mobile Engagement i kliknij przycisk hello **natywnych powiadomień wypychanych** sekcji powitania po lewej stronie. Kliknięcie hello **Edytuj** tooenter przycisk z **identyfikator zabezpieczeń (SID) pakietu** i **klucz tajny** pokazany:

    ![][6]
8. Na koniec upewnij się, że aplikacja programu Visual Studio został skojarzony z tą utworzoną aplikacją w sklepie z aplikacjami hello. W programie Visual Studio kliknij pozycję **Skojarz aplikację ze sklepem**.

    ![][7]

## <a id="send"></a>Wyślij aplikacji tooyour powiadomień
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Jeśli aplikacja hello jest uruchomiona, zobaczysz powiadomienie w aplikacji. Jeśli aplikacja hello są zamknięte, w przeciwnym razie Zobacz wyskakujące powiadomienie.
Jeśli zobaczysz powiadomienie w aplikacji, ale nie powiadomienie wyskakujące, a aplikacja hello są uruchomione w trybie debugowania w programie Visual Studio, spróbuj **zdarzenia cyklu życia -> Wstrzymaj** w tooensure narzędzi hello jest wstrzymana, aplikacja hello. Jeśli kliknięto przycisk Strona główna hello podczas debugowania aplikacji hello w programie Visual Studio, następnie go nie zawsze zostanie wstrzymana, a gdy zostanie wyświetlone powiadomienie hello w aplikacji, nie wyświetla jako powiadomienie wyskakujące.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Centrum deweloperów Sklepu Windows]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
