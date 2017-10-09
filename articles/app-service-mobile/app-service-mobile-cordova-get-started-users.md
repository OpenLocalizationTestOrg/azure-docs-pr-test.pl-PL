---
title: "Uwierzytelnianie aaaAdd na Apache Cordova w usłudze Mobile Apps | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Mobile Apps w usłudze Azure App Service tooauthenticate użytkowników aplikacji oprogramowania Apache Cordova za pomocą różnych dostawców tożsamości, obejmującej Google, Facebook, Twitter i Microsoft."
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 10dd6dc9-ddf5-423d-8205-00ad74929f0d
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 61a05c5ac67fd0f0bc4c9d6920954a9b464a0a8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-apache-cordova-app"></a>Dodawanie aplikacji oprogramowania Apache Cordova tooyour uwierzytelniania
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="summary"></a>Podsumowanie
W tym samouczku możesz dodać projekt szybkiego startu todolist toohello uwierzytelniania w przypadku oprogramowania Apache Cordova przy użyciu dostawcy tożsamości obsługiwane. W tym samouczku jest oparta na powitania [Rozpoczynanie pracy z usługą Mobile Apps] — samouczek, należy najpierw wykonać.

## <a name="register"></a>Zarejestrować aplikację do uwierzytelniania i skonfigurować hello usługi aplikacji
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

[Obejrzyj wideo przedstawiające podobne kroki](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-8-Azure-authentication)

## <a name="permissions"></a>Ogranicz uprawnienia tooauthenticated użytkowników
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Teraz możesz sprawdzić, czy ten dostęp anonimowy tooyour wewnętrznej bazy danych została wyłączona. W programie Visual Studio:

* Hello Otwórz projekt, który został utworzony po ukończeniu samouczka hello [Rozpoczynanie pracy z usługą Mobile Apps].
* Uruchom aplikację w hello **Emulator systemu Google Android**.
* Sprawdź, czy wystąpił nieoczekiwany błąd połączenia jest wyświetlany po uruchomieniu aplikacji hello.

Następnie zaktualizuj użytkownicy tooauthenticate aplikacji hello przed wysłaniem żądania zasobów z hello zaplecza aplikacji mobilnej.

## <a name="add-authentication"></a>Dodaj aplikację toohello uwierzytelniania
1. Otwórz projekt w **programu Visual Studio**, następnie otwórz hello `www/index.html` plik do edycji.
2. Zlokalizuj hello `Content-Security-Policy` metatag w sekcji head hello.  Dodaj hello OAuth hosta toohello listę dozwolonych źródeł.

   | Dostawca | Nazwa dostawcy zestawu SDK | OAuth Host |
   |:--- |:--- |:--- |
   | Usługa Azure Active Directory | usługi AAD | https://login.microsoftonline.com |
   | Facebook | Usługi Facebook | https://www.Facebook.com |
   | Google | Google | https://accounts.Google.com |
   | Microsoft | MicrosoftAccount | https://login.Live.com |
   | Twitter | W usłudze Twitter | https://API.twitter.com |

    Przykład zawartość--zasady zabezpieczeń (zaimplementowany dla usługi Azure Active Directory) jest następujący:

        <meta http-equiv="Content-Security-Policy" content="default-src 'self'
            data: gap: https://login.microsoftonline.com https://yourapp.azurewebsites.net; style-src 'self'">

    Zastąp `https://login.microsoftonline.com` z hostem OAuth hello hello powyższej tabeli.  Aby uzyskać więcej informacji na temat hello zawartości zabezpieczeń zasady metatag Zobacz hello [zasadę zawartość dokumentacji].

    Niektórzy dostawcy uwierzytelniania nie wymaga się, że zawartość zabezpieczeń zasady zostanie zmieniona, gdy na urządzeniach przenośnych odpowiednie.  Na przykład żadnych zmian zawartości zabezpieczeń zasady są wymagane w przypadku przy użyciu uwierzytelniania serwisu Google na urządzeniu z systemem Android.

3. Otwórz hello `www/js/index.js` pliku do edycji, Znajdź hello `onDeviceReady()` metody i w obszarze powitania klienta tworzenia kodu Dodaj hello następującego kodu:

        // Login toohello service
        client.login('SDK_Provider_Name')
            .then(function () {

                // BEGINNING OF ORIGINAL CODE

                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                // END OF ORIGINAL CODE

            }, handleError);

    Ten kod zastępuje hello istniejący kod, który tworzy odwołanie do tabeli hello i odświeża hello interfejsu użytkownika.

    Metoda: login() Hello uruchamia uwierzytelniania z dostawcą hello. Metoda: login() Hello jest z funkcji asynchronicznych, która zwraca JavaScript Promise.  rest Hello inicjowania hello jest umieszczony wewnątrz hello promise odpowiedź tak, aby nie jest wykonywany przed zakończeniem hello: login() metody.

4. W kodzie hello, który właśnie został dodany, Zastąp `SDK_Provider_Name` o nazwie hello dostawcy logowania. Na przykład dla usługi Azure Active Directory, należy użyć `client.login('aad')`.
5. Uruchom projekt.  Po zakończeniu projektu hello inicjowania aplikacji zawiera stronę logowania OAuth hello hello wybranego dostawcy uwierzytelniania.

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej [o uwierzytelniania] z usługi Azure App Service.
* Kontynuuj hello samouczek, dodając [powiadomień wypychanych] tooyour aplikacji oprogramowania Apache Cordova.

Dowiedz się, jak toouse hello zestawów SDK.

* [Zestaw Apache Cordova SDK]
* [Zestaw ASP.NET Server SDK]
* [Zestaw Node.js Server SDK]

<!-- URLs. -->
[Rozpoczynanie pracy z usługą Mobile Apps]: app-service-mobile-cordova-get-started.md
[zasadę zawartość dokumentacji]: https://cordova.apache.org/docs/en/latest/guide/appdev/whitelist/index.html
[powiadomień wypychanych]: app-service-mobile-cordova-get-started-push.md
[o uwierzytelniania]: app-service-mobile-auth.md
[Zestaw Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[Zestaw ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Zestaw Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
