---
title: "aaaAdd uwierzytelniania w systemie iOS w usłudze Azure Mobile Apps"
description: "Dowiedz się, jak toouse Azure Mobile Apps tooauthenticate użytkowników aplikacji systemu iOS za pomocą różnych dostawców tożsamości, obejmującej AAD, Google, Facebook, Twitter i firmy Microsoft."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a>Dodawanie aplikacji dla systemu iOS tooyour uwierzytelniania
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

W tym samouczku, możesz dodać uwierzytelniania toohello [iOS szybki start] projektu przy użyciu dostawcy tożsamości obsługiwane. W tym samouczku jest oparta na powitania [iOS szybki start] — samouczek, należy najpierw wykonać.

## <a name="register"></a>Zarejestrować aplikację do uwierzytelniania i skonfigurować hello usługi aplikacji
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Dodaj adresy URL przekierowania zewnętrznych dozwolone Twojej aplikacji toohello

Bezpieczne uwierzytelnianie wymaga Zdefiniuj nowy schemat adresu URL dla aplikacji.  Po zakończeniu procesu uwierzytelniania hello dzięki temu hello uwierzytelniania systemu tooredirect wstecz tooyour aplikacji.  W tym samouczku używamy schemat adresu URL _appname_ w ciągu.  Można jednak użyć dowolnego wybranego schematu URL.  Powinna być unikatowa tooyour aplikacji mobilnej.  Przekierowanie hello tooenable na th po stronie serwera:

1. W hello [portalu Azure], wybierz usługę aplikacji.

2. Kliknij przycisk hello **uwierzytelniania / autoryzacji** opcji menu.

3. Kliknij przycisk **usługi Azure Active Directory** w obszarze hello **dostawców uwierzytelniania** sekcji.

4. Zestaw hello **tryb zarządzania** za**zaawansowane**.

5. W hello **dozwolone zewnętrznych adresów URL przekierowań**, wprowadź `appname://easyauth.callback`.  Witaj _appname_ ten ciąg jest hello schemat adresu URL aplikacji mobilnej.  Musi on być zgodny normalne Specyfikacja adresu URL dla protokołu (Użyj litery i tylko cyfry i rozpoczyna się od litery).  Należy zanotuj ciąg hello, który możesz wybrać, ponieważ będzie potrzebny tooadjust kodu aplikacji mobilnej przy użyciu hello schemat adresu URL w kilku miejscach.

6. Kliknij przycisk **OK**.

7. Kliknij pozycję **Zapisz**.

## <a name="permissions"></a>Ogranicz uprawnienia tooauthenticated użytkowników
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

W programie Xcode, naciśnij klawisz **Uruchom** toostart hello aplikacji. Zgłoszony wyjątek, ponieważ aplikacja hello prób tooaccess wewnętrznej bazy danych jako nieuwierzytelniony użytkownik, ale hello *TodoItem* tabeli teraz wymaga uwierzytelniania.

## <a name="add-authentication"></a>Dodaj tooapp uwierzytelniania
**Objective-C**:

1. Na komputerze Mac Otwórz *QSTodoListViewController.m* w środowisku Xcode i dodaj następujące metody hello:

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    Zmień *google* za*microsoftaccount*, *twitter*, *facebook*, lub *windowsazureactivedirectory* Jeśli nie używasz Google jako dostawcy tożsamości. Jeśli korzystasz z usługi Facebook, należy najpierw [dozwolonych domen Facebook] [ 1] w aplikacji.

    Zastąp hello **urlScheme** z unikatową nazwę aplikacji.  Hello urlScheme powinny być hello sam jako hello protokół schemat adresu URL, który określono w hello **dozwolone zewnętrznych adresów URL przekierowań** w hello portalu Azure. Hello urlScheme jest używany przez hello uwierzytelniania wywołania zwrotnego tooswitch wstecz tooyour aplikacji, po zakończeniu żądania uwierzytelnienia.

2. Zastąp `[self refresh]` w `viewDidLoad` w *QSTodoListViewController.m* z hello następującego kodu:

    ```Objective-C
    [self loginAndGetData];
    ```

3. Otwórz hello `QSAppDelegate.h` plik i dodać hello następującego kodu:

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. Otwórz hello `QSAppDelegate.m` plik i dodać hello następującego kodu:

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   Dodaj ten kod bezpośrednio przed przeczytaniem wiersza hello `#pragma mark - Core Data stack`.  Zastąp _appname_ o hello urlScheme wartość, który został użyty w kroku 1.

5. Otwórz hello `AppName-Info.plist` pliku (zastępując AppName o nazwie hello aplikacji), a następnie dodaj hello następującego kodu:

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    Ten kod powinien być umieszczony wewnątrz hello `<dict>` elementu.  Zastąp hello _appname_ ciągu (w tablicy dla **CFBundleURLSchemes**) o nazwie aplikacji hello wybranymi w kroku 1.  Możesz również wprowadzić te zmiany w hello plist Edytor — Witaj, kliknij polecenie `AppName-Info.plist` plik w edytorze plist hello tooopen XCode.

    Zastąp hello `com.microsoft.azure.zumo` ciągu dla **CFBundleURLName** z Twojej firmy Apple identyfikator pakietu.

6. Naciśnij klawisz *Uruchom* toostart hello aplikacji, a następnie zaloguj. Gdy użytkownik jest zalogowany, należy listy Todo hello stanie tooview i aktualizacje.

**Kod SWIFT**:

1. Na komputerze Mac Otwórz *ToDoTableViewController.swift* w środowisku Xcode i dodaj następujące metody hello:

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    Zmień *google* za*microsoftaccount*, *twitter*, *facebook*, lub *windowsazureactivedirectory* Jeśli nie używasz Google jako dostawcy tożsamości. Jeśli korzystasz z usługi Facebook, należy najpierw [dozwolonych domen Facebook] [ 1] w aplikacji.

    Zastąp hello **urlScheme** z unikatową nazwę aplikacji.  Hello urlScheme powinny być hello sam jako hello protokół schemat adresu URL, który określono w hello **dozwolone zewnętrznych adresów URL przekierowań** w hello portalu Azure. Hello urlScheme jest używany przez hello uwierzytelniania wywołania zwrotnego tooswitch wstecz tooyour aplikacji, po zakończeniu żądania uwierzytelnienia.

2. Usuń wiersze hello `self.refreshControl?.beginRefreshing()` i `self.onRefresh(self.refreshControl)` na końcu `viewDidLoad()` w *ToDoTableViewController.swift*. Dodaj wywołanie za`loginAndGetData()` zamiast nich:

    ```swift
    loginAndGetData()
    ```

3. Otwórz hello `AppDelegate.swift` plik i dodać powitania po wierszu toohello `AppDelegate` klasy:

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    Zastąp hello _appname_ o hello urlScheme wartość, który został użyty w kroku 1.

4. Otwórz hello `AppName-Info.plist` pliku (zastępując AppName o nazwie hello aplikacji), a następnie dodaj hello następującego kodu:

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    Ten kod powinien być umieszczony wewnątrz hello `<dict>` elementu.  Zastąp hello _appname_ ciągu (w tablicy dla **CFBundleURLSchemes**) o nazwie aplikacji hello wybranymi w kroku 1.  Możesz również wprowadzić te zmiany w hello plist Edytor — Witaj, kliknij polecenie `AppName-Info.plist` plik w edytorze plist hello tooopen XCode.

    Zastąp hello `com.microsoft.azure.zumo` ciągu dla **CFBundleURLName** z Twojej firmy Apple identyfikator pakietu.

5. Naciśnij klawisz *Uruchom* toostart hello aplikacji, a następnie zaloguj. Gdy użytkownik jest zalogowany, należy listy Todo hello stanie tooview i aktualizacje.

Usługi aplikacji — uwierzytelnianie przy użyciu jabłek komunikacji między aplikacjami.  Aby uzyskać więcej informacji na ten temat można znaleźć toohello [dokumentacji firmy Apple][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portalu Azure]: https://portal.azure.com

[iOS szybki start]: app-service-mobile-ios-get-started.md

