---
title: "uwierzytelniania serwisu Facebook tooconfigure aaaHow aplikacji usługi aplikacji"
description: "Dowiedz się, jak tooconfigure uwierzytelniania serwisu Facebook dla aplikacji usługi aplikacji."
services: app-service
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: b6b4f062-fcb4-47b3-b75a-ec4cb51a62fd
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 53d03445a2ad17de1d2f69f5e770d14385b48ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-facebook-login"></a>Jak tooconfigure logowanie Facebook toouse aplikacji usługi aplikacji
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

W tym temacie opisano sposób tooconfigure usłudze Azure App Service toouse usługi Facebook jako dostawcy uwierzytelniania.

toocomplete hello procedurze w tym temacie, musisz mieć konto usługi Facebook, ze zweryfikowanym adresem e-mail i numer telefonu komórkowego. toocreate nowe konto usługi Facebook, przejdź zbyt[facebook.com].

## <a name="register"></a>Zarejestrować aplikację w usłudze Facebook
1. Zaloguj się na toohello [portalu Azure]i przejdź tooyour aplikacji. Kopiowanie z **adres URL**. Użyjesz tego tooconfigure aplikacji Facebook.
2. W innym oknie przeglądarki Przejdź toohello [deweloperzy Facebook] poświadczenia konta witryny sieci Web i logowania z użytkownika usługi Facebook.
3. (Opcjonalnie) Jeśli nie została jeszcze zarejestrowana, kliknij przycisk **aplikacje** > **Zarejestruj się jako deweloper**, Zaakceptuj zasady hello i wykonaj kroki rejestracji hello.
4. Kliknij przycisk **Moje aplikacje** > **Dodaj nową aplikację** > **witryny sieci Web** > **pominąć i utworzyć identyfikator aplikacji**. 
5. W **Nazwa wyświetlana**, wpisz unikatową nazwę dla aplikacji, typ użytkownika **E-mail kontaktu**, wybierz **kategorii** dla aplikacji, następnie kliknij przycisk **utworzyć identyfikator aplikacji**i ukończyć powitalnych sprawdzania zabezpieczeń. Trwa pulpitu nawigacyjnego developer toohello dla nowej aplikacji usługi Facebook.
6. W obszarze "Logowanie usługi Facebook", kliknij przycisk **wprowadzenie**. Dodawanie aplikacji **identyfikator URI przekierowania** za**prawidłowy OAuth przekierowania URI**, następnie kliknij przycisk **Zapisz zmiany**. 
   
   > [!NOTE]
   > Twoje przekierowania URI jest adresem URL hello aplikacji dołączony ścieżki hello, */.auth/login/facebook/callback*. Na przykład `https://contoso.azurewebsites.net/.auth/login/facebook/callback`. Upewnij się, że używasz hello schematu HTTPS.
   > 
   > 
7. W nawigacji po lewej stronie powitania, kliknij przycisk **ustawienia**. Na powitania **klucz tajny aplikacji** kliknij **Pokaż**, podaj hasło, jeśli żądanie, a następnie zanotuj wartości hello **identyfikator aplikacji** i **klucz tajny aplikacji**. Te nowsze tooconfigure za pomocą aplikacji w usłudze Azure.
   
   > [!IMPORTANT]
   > klucz tajny aplikacji Hello jest ważne poświadczenie zabezpieczeń. Nie udostępniaj nikomu ten klucz tajny i rozpowszechnienie go w aplikacji klienta.
   > 
   > 
8. Witaj konta usługi Facebook, która była używana tooregister aplikacji hello jest administrator aplikacji hello. W tym momencie tylko administratorzy mogą Zaloguj się do tej aplikacji. tooauthenticate inne konta usługi Facebook, kliknij przycisk **aplikacji przejrzyj** i Włącz **publicznego upewnij < your-app-name >** tooenable ogólne publicznego dostępu przy użyciu uwierzytelniania serwisu Facebook.

## <a name="secrets"></a>Facebook dodać informacje tooyour aplikacji
1. Po powrocie do hello [portalu Azure], przejdź tooyour aplikacji. Kliknij przycisk **ustawienia** > **uwierzytelniania / autoryzacji**i upewnij się, że **aplikacji uwierzytelniania usługi** jest **na**.
2. Kliknij przycisk **Facebook**, Wklej wartości Identyfikatora aplikacji i klucz tajny aplikacji hello, które uzyskany wcześniej, opcjonalnie włączyć wszystkie zakresy wymagane przez aplikację, a następnie kliknij **OK**.
   
    ![][0]
   
    Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API. Musisz zezwolić użytkownikom w kodzie aplikacji.
3. (Opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkowników uwierzytelnionych przez Facebook, ustawić **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Facebook**. Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są tooFacebook przekierowany do uwierzytelniania.
4. Po zakończeniu konfigurowania uwierzytelniania, kliknij przycisk **zapisać**.

Wszystko jest teraz gotowy toouse Facebook dla uwierzytelniania w aplikacji.

## <a name="related-content"></a>Związane z zawartością
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->
[0]: ./media/app-service-mobile-how-to-configure-facebook-authentication/mobile-app-facebook-settings.png

<!-- URLs. -->
[Deweloperzy usługi Facebook]: http://go.microsoft.com/fwlink/p/?LinkId=268286
[Facebook.com]: http://go.microsoft.com/fwlink/p/?LinkId=268285
[Get started with authentication]: /en-us/develop/mobile/tutorials/get-started-with-users-dotnet/
[Witryna Azure Portal]: https://portal.azure.com/
