---
title: "aaaGet uruchomiony przy użyciu uwierzytelniania dla aplikacji mobilnych w dla systemu Xamarin Android"
description: "Dowiedz się, jak toouse Mobile Apps tooauthenticate użytkowników aplikacji platformy Xamarin Android za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i firmy Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>Dodawanie aplikacji platformy Xamarin.Android tooyour uwierzytelniania
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

W tym temacie opisano sposób tooauthenticate użytkowników aplikacji mobilnych z aplikacji klienta. W tym samouczku należy dodać projekt szybkiego startu toohello uwierzytelniania przy użyciu dostawcy tożsamości, który jest obsługiwany przez usługi Azure Mobile Apps. Po trwa pomyślnym uwierzytelnieniu i autoryzacji w aplikacji mobilnej hello wartość Identyfikatora użytkownika hello jest wyświetlany.

W tym samouczku jest oparta na powitania aplikacja mobilna — Szybki Start. Samouczek hello również najpierw musisz zakończyć [tworzenie aplikacji platformy Xamarin.Android]. Jeśli nie używasz hello pobrany Projekt serwera szybki start, należy dodać projekt tooyour hello uwierzytelniania rozszerzenie pakietu. Aby uzyskać więcej informacji na temat pakietów rozszerzenia serwera, zobacz [pracować z serwera wewnętrznej bazy danych hello .NET SDK usługi Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register"></a>Zarejestrować aplikację do uwierzytelniania i konfigurowanie usługi aplikacji
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

W programie Visual Studio lub Xamarin Studio Uruchom projekt klienta hello na urządzenia lub emulatora. Upewnij się, że wystąpił nieobsługiwany wyjątek przy użyciu kodu stanu 401 (bez autoryzacji) jest wywoływane po uruchomieniu aplikacji hello. Dzieje się tak, ponieważ aplikacja hello prób tooaccess zaplecza aplikacji mobilnej jako nieuwierzytelniony użytkownik. Witaj *TodoItem* tabeli teraz wymaga uwierzytelniania.

Następnie zaktualizuje powitania klienta aplikacji toorequest zasobów z zaplecza aplikacji mobilnej hello z uwierzytelnionego użytkownika.

## <a name="add-authentication"></a>Dodaj aplikację toohello uwierzytelniania
Aplikacja Hello jest toorequire zaktualizowanych użytkowników tootap hello **Zaloguj** przycisk i uwierzytelniania przed wyświetleniem danych.

1. Dodaj hello następującego kodu toohello **TodoActivity** klasy:
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    Spowoduje to utworzenie nowego tooauthenticate — metoda użytkownika i metody obsługi nowej **Zaloguj** przycisku. Użytkownik Hello w powyższym hello przykładowy kod jest uwierzytelniany przy użyciu identyfikatora logowania usługi Facebook. Okno dialogowe jest identyfikator użytkownika hello używane toodisplay raz uwierzytelnić.
   
   > [!NOTE]
   > Jeśli używasz dostawcy tożsamości innego niż usługi Facebook, zmień wartość hello przekazano zbyt**LoginAsync** powyżej tooone następującego hello: *MicrosoftAccount*, *Twitter*, *Google*, lub *WindowsAzureActiveDirectory*.
   > 
   > 
2. W hello **OnCreate** metody, usuń lub hello komentarz po wierszu kodu:
   
        OnRefreshItemsSelected ();
3. W pliku Activity_To_Do.axml hello Dodaj następujące hello *odwoływały* przycisk definicji przed istniejących hello *AddItem* przycisk:
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Dodaj hello następującego pliku zasobów Strings.xml toohello elementu:
   
        <string name="login_button_text">Sign in</string>
5. Otwórz pliku AndroidManifest.xml hello, Dodaj hello następującego kodu wewnątrz `<application>` — element XML:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. W programie Visual Studio lub Xamarin Studio Uruchom projekt klienta hello na urządzeniu lub emulatorze i zaloguj się przy użyciu dostawcy tożsamości wybrany. Pomyślnie zalogowany, aplikacji hello zostaną wyświetlone Identyfikatora logowania i hello Lista zadań do wykonania, a można udostępnić dane toohello aktualizacji.

<!-- URLs. -->
[tworzenie aplikacji platformy Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md