---
title: "aaaGet uruchomiony przy użyciu uwierzytelniania dla aplikacji mobilnych w systemu Xamarin iOS"
description: "Dowiedz się, jak toouse Mobile Apps tooauthenticate użytkowników aplikacji platformy Xamarin iOS za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i firmy Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a>Dodaj aplikację platformy Xamarin.iOS tooyour uwierzytelniania
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

W tym temacie opisano sposób tooauthenticate użytkowników aplikację usługi Mobile aplikacji z poziomu aplikacji klienta. W tym samouczku możesz dodać uwierzytelniania toohello Xamarin.iOS projekt szybkiego startu przy użyciu dostawcy tożsamości, która jest obsługiwana przez usługę App Service. Po pomyślnie trwa uwierzytelnieniu i autoryzacji w aplikacji mobilnej, jest wyświetlana wartość Identyfikatora użytkownika hello i będą mogli tooaccess ograniczone tabeli danych.

Najpierw musisz zakończyć samouczek hello [tworzenie aplikacji platformy Xamarin.iOS]. Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać projekt tooyour hello uwierzytelniania rozszerzenie pakietu. Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello

Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji. Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji. W tym samouczku używamy schemat adresu URL hello _appname_ w ciągu. Można jednak użyć dowolnego wybranego schematu URL. Powinna być unikatowa tooyour aplikacji mobilnej. Przekierowanie hello tooenable na powitania po stronie serwera:

1. W hello [portalu Azure] wybierz usługę aplikacji.

2. Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.

3. W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.  Witaj **url_scheme_of_your_app** w tym ciągu jest hello schemat adresu URL aplikacji mobilnej.  Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).  Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.

4. Kliknij przycisk **OK**.

5. Kliknij pozycję **Zapisz**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Ogranicz uprawnienia tooauthenticated użytkowników
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. W programie Visual Studio lub Xamarin Studio Uruchom projekt klienta hello na urządzenia lub emulatora. Upewnij się, że wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello. Błąd Hello jest rejestrowane toohello konsoli hello debugera. Dlatego w programie Visual Studio hello awarii w oknie danych wyjściowych hello powinna zostać wyświetlona.

&nbsp;&nbsp;Ten błąd nieautoryzowanego wynika z faktu, aplikacja hello prób tooaccess zaplecza aplikacji mobilnej jako nieuwierzytelniony użytkownik. Witaj *TodoItem* tabeli teraz wymaga uwierzytelniania.

Następnie zaktualizuje powitania klienta aplikacji toorequest zasobów z zaplecza aplikacji mobilnej hello z uwierzytelnionego użytkownika.

## <a name="add-authentication-toohello-app"></a>Dodaj aplikację toohello uwierzytelniania
W tej sekcji należy zmodyfikować przed wyświetleniem danych toodisplay aplikacji hello ekran logowania. Po uruchomieniu aplikacji hello nie nie będą łączyć się tooyour usługi aplikacji i nie zawiera żadnych danych. Po powitania po raz pierwszy użytkownik hello wykonuje hello gestu odświeżania, zostanie wyświetlony ekran logowania hello; Po pojawi się lista zadań do wykonania w hello pomyślnego logowania.

1. W hello projektu klienta, otwórz plik hello **QSTodoService.cs** i dodaj następujące hello za pomocą instrukcji i `MobileServiceUser` z toohello akcesor QSTodoService klasy:
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. Dodaj nową metodę o nazwie **Uwierzytelnij** za**QSTodoService** z powitania po definicji:

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] Jeśli używasz dostawcy tożsamości innych niż Facebook, zmień wartość hello przekazano zbyt**LoginAsync** powyżej tooone następującego hello: _MicrosoftAccount_, _Twitter_, _Google_, lub _WindowsAzureActiveDirectory_.

3. Otwórz **QSTodoListViewController.cs**. Zmodyfikuj definicję metody hello **ViewDidLoad** usuwanie hello wywołanie za**RefreshAsync()** niemal zakończenia hello:
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. Zmodyfikuj metodę hello **RefreshAsync** tooauthenticate Jeśli hello **użytkownika** właściwość ma wartość null. Dodaj następującego kodu u góry hello definicję metody hello hello:
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. Otwórz **AppDelegate.cs**, Dodaj hello następujące metody:

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. Otwórz **Info.plist** pliku, przejdź do zbyt**typy adresu URL** w hello **zaawansowane** sekcji. Teraz skonfigurować hello **identyfikator** i hello **Schematy adresów URL** typ adresu URL i kliknij przycisk **Dodawanie adresu URL typu**. **Schematy adresów URL** powinny być takie same hello jako Twoje {url_scheme_of_your_app}.
7. W programie Visual Studio lub Xamarin Studio połączone tooyour Xamarin hosta kompilacji na komputerze Mac Uruchom projekt klienta hello przeznaczonych dla określonego urządzenia lub emulatora. Sprawdź, czy, aplikacja hello nie wyświetla żadnych danych.
   
    Wykonaj hello odświeżania gestu przez ściąganie hello listę elementów, które spowoduje, że tooappear ekranu logowania hello w dół. Po pomyślnie zostały wprowadzone prawidłowe poświadczenia, aplikacji hello zostaną wyświetlone powitalne Lista zadań do wykonania i można udostępnić dane toohello aktualizacji.

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[tworzenie aplikacji platformy Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md