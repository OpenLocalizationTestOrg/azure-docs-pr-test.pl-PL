---
title: Aplikacja systemu Windows platformy Uniwersalnej tooyour authentication aaaAdd | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Azure App Service Mobile Apps tooauthenticate użytkowników aplikacji systemu Windows platformy Uniwersalnej przy użyciu różnych dostawców tożsamości, obejmującej: usługi AAD, Google, Facebook, Twitter i firmy Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a>Dodawanie aplikacji dla systemu Windows tooyour uwierzytelniania
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

W tym temacie opisano sposób tooadd aplikacji mobilnej tooyour uwierzytelniania opartego na chmurze. W tym samouczku możesz dodać projekt szybkiego startu Windows platformy Uniwersalnej toohello uwierzytelniania aplikacji mobilnej przy użyciu dostawcy tożsamości, która jest obsługiwana przez usługę Azure App Service. Po pomyślnym są uwierzytelnieni i upoważnieni przez zaplecza aplikacji mobilnej, wartość Identyfikatora użytkownika hello jest wyświetlany.

W tym samouczku jest oparta na powitania Mobile Apps — Szybki Start. Najpierw musisz zakończyć samouczek hello [Rozpoczynanie pracy z usługą Mobile Apps](app-service-mobile-windows-store-dotnet-get-started.md).

## <a name="register"></a>Zarejestrować aplikację do uwierzytelniania i skonfigurować hello usługi aplikacji
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello

Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji. Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji. W tym samouczku używamy schemat adresu URL hello _appname_ w ciągu. Można jednak użyć dowolnego wybranego schematu URL. Powinna być unikatowa tooyour aplikacji mobilnej. Przekierowanie hello tooenable na powitania po stronie serwera:

1. W hello [portalu Azure] wybierz usługę aplikacji.

2. Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.

3. W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `url_scheme_of_your_app://easyauth.callback`.  Witaj **url_scheme_of_your_app** w tym ciągu jest hello schemat adresu URL aplikacji mobilnej.  Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).  Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.

4. Kliknij przycisk **OK**.

5. Kliknij pozycję **Zapisz**.

## <a name="permissions"></a>Ogranicz uprawnienia tooauthenticated użytkowników
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Teraz możesz sprawdzić, czy ten dostęp anonimowy tooyour wewnętrznej bazy danych została wyłączona. Ustaw jako projekt uruchamiania hello projektu aplikacji platformy uniwersalnej systemu Windows hello wdrażanie i uruchamianie aplikacji hello; Upewnij się, że wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello. Dzieje się tak, ponieważ aplikacja hello prób tooaccess kodu aplikacji mobilnej jako nieuwierzytelniony użytkownik, ale hello *TodoItem* tabeli teraz wymaga uwierzytelniania.

Następnie zaktualizuje użytkownicy tooauthenticate aplikacji hello przed wysłaniem żądania zasobów z usługi aplikacji.

## <a name="add-authentication"></a>Dodaj aplikację toohello uwierzytelniania
1. W projekcie aplikacji platformy uniwersalnej systemu Windows hello pliku MainPage.xaml.cs i Dodaj hello następującego fragmentu kodu:
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    Ten kod uwierzytelnia użytkownika hello za pomocą nazwy logowania usługi Facebook. Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, zmień wartość hello **MobileServiceAuthenticationProvider** większa niż wartość toohello przez dostawcę.
2. Zastąp hello **OnNavigatedTo()** metody w MainPage.xaml.cs. Następnie należy dodać **Zaloguj** przycisk toohello aplikacji, które wyzwala uwierzytelniania.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. Dodaj następujące toohello fragment kodu MainPage.xaml.cs hello:
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. Otwórz plik projektu MainPage.xaml hello, zlokalizować hello elementu, który definiuje hello **zapisać** przycisk i zastąp go hello następującego kodu:
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. Dodaj następujące toohello fragment kodu App.xaml.cs hello:

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. Otwórz plik Package.appxmanifest, przejdź do zbyt**deklaracje**w **dostępne deklaracje** listy rozwijanej wybierz **protokołu** i kliknij przycisk **Dodaj** przycisku. Teraz skonfigurować hello **właściwości** z hello **protokołu** deklaracji. W **Nazwa wyświetlana**, Dodaj nazwę hello mają toousers toodisplay aplikacji. W **nazwa**, Dodaj użytkownika {url_scheme_of_your_app}.
7. Naciśnij klawisz hello F5 klucza toorun hello aplikacji, kliknij przycisk hello **Zaloguj** przycisk i zaloguj się do aplikacji hello u dostawcy tożsamości wybrany. Po logowanie zakończy się pomyślnie, aplikacja hello jest uruchamiana bez błędów i możesz są możliwe tooquery z wewnętrzną bazą danych i toodata aktualizacji.

## <a name="tokens"></a>Token uwierzytelniania hello magazynu na powitania klienta
Hello w poprzednim przykładzie pokazano standardowe logowania, która wymaga powitania klienta toocontact zarówno hello dostawcy tożsamości i hello App Service w każdym uruchomieniu danej aplikacji hello. Nie tylko jest nieefektywne, można uruchomić tej metody do użycia — odnosi się problemy z wielu klientów Wypróbuj toostart aplikacji na powitania tym samym czasie. Lepszym rozwiązaniem jest token autoryzacji hello toocache zwracane w aplikacji usługi, a następnie spróbuj toouse to najpierw przed przy użyciu opartych na dostawcy logowania.

> [!NOTE]
> Może buforować hello token wystawiony przez usługi aplikacji niezależnie od tego, czy używasz zarządzanych przez klienta lub zarządzane przez usługę uwierzytelniania. W tym samouczku korzysta z zarządzanymi przez usługę uwierzytelniania.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Następne kroki
Teraz, aby ukończyć w tym samouczku uwierzytelnianie podstawowe, należy wziąć pod uwagę kontynuować tooone hello następujące samouczki:

* [Dodaj aplikację tooyour powiadomień wypychanych](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Dowiedz się, jak powiadomień wypychanych tooadd obsługują tooyour aplikacji i Konfigurowanie powiadomień wypychanych toosend usługi Azure Notification Hubs toouse aplikacji mobilnej wewnętrznej bazy danych.
* [Włączanie synchronizacji w trybie offline dla aplikacji](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Dowiedz się, jak w trybie offline tooadd obsługują aplikację przy użyciu zaplecza aplikacji mobilnej. Synchronizacja w trybie offline umożliwia użytkownikom końcowym toointeract z aplikacją mobilną&mdash;przeglądanie, dodawanie lub modyfikowanie danych&mdash;nawet wtedy, gdy istnieje połączenie sieciowe.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
