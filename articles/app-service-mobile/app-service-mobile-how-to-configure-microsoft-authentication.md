---
title: "Uwierzytelnianie Microsoft Account tooconfigure aaaHow aplikacji usługi aplikacji"
description: "Dowiedz się, jak uwierzytelnianie Microsoft Account tooconfigure aplikacji usługi aplikacji."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: ffbc6064-edf6-474d-971c-695598fd08bf
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: d86d8dab26a189f4454082fc18e44e3fb6e0a01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-microsoft-account-login"></a>Jak tooconfigure logowanie Account Microsoft toouse aplikacji usługi aplikacji
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

W tym temacie opisano sposób tooconfigure usłudze Azure App Service toouse Account Microsoft jako dostawcy uwierzytelniania. 

## <a name="register-microsoft-account"></a>Zarejestrować aplikację z kontem Microsoft
1. Zaloguj się na toohello [portalu Azure]i przejdź tooyour aplikacji. Kopiowania z **adres URL**, który później możesz użyć tooconfigure aplikacji z Account Microsoft.
2. Przejdź toohello [Moje aplikacje] strony hello Microsoft Account Developer Center i zaloguj się przy użyciu konta Microsoft, jeśli jest to wymagane.
3. Kliknij przycisk **Dodaj aplikację**, następnie wpisz nazwę aplikacji i kliknij przycisk **tworzenie aplikacji**.
4. Zanotuj hello **identyfikator aplikacji**, ponieważ będzie potrzebny później. 
5. W obszarze "Platform," kliknij **dodać platformy** i wybierz pozycję "Web".
6. W obszarze "Identyfikator URI przekierowania" Podaj punkt końcowy hello aplikacji, następnie kliknij przycisk **zapisać**. 
   
   > [!NOTE]
   > Twoje przekierowania URI jest adresem URL hello aplikacji dołączony ścieżki hello, */.auth/login/microsoftaccount/callback*. Na przykład `https://contoso.azurewebsites.net/.auth/login/microsoftaccount/callback`.   
   > Upewnij się, że używasz hello schematu HTTPS.
   
7. W obszarze "Klucze tajne aplikacji," kliknij **wygenerować nowe hasło**. Zanotuj wartość hello wyświetlana. Po wyjściu strony hello go nie pojawi się ponownie.

    > [!IMPORTANT]
    > hasło Hello jest ważne poświadczenie zabezpieczeń. Nie udostępniaj nikomu hasła hello lub opublikować go w aplikacji klienta.

## <a name="secrets"></a>Dodawanie konta Microsoft informacji tooyour aplikacji usługi aplikacji
1. Po powrocie do hello [portalu Azure]Przejdź tooyour aplikacji, kliknij przycisk **ustawienia** > **uwierzytelniania / autoryzacji**.
2. Jeśli hello uwierzytelniania / autoryzacji funkcja nie jest włączona, przełącz go **na**.
3. Kliknij przycisk **konta Microsoft**. Wklej w wartości Identyfikatora aplikacji i hasło hello, które uzyskany wcześniej i opcjonalnie włączyć wszystkie zakresy wymaganych przez aplikację. Następnie kliknij przycisk **OK**.
   
    ![][1]
   
    Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API. Musisz zezwolić użytkownikom w kodzie aplikacji.
4. (Opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkowników uwierzytelnionych przez konta Microsoft, ustaw **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Account Microsoft**. Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są przekierowywane tooMicrosoft konto do uwierzytelniania.
5. Kliknij pozycję **Zapisz**.

Wszystko jest teraz gotowy toouse Account Microsoft do uwierzytelniania w aplikacji.

## <a name="related-content"></a>Związane z zawartością
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/app-service-microsoftaccount-redirect.png
[1]: ./media/app-service-mobile-how-to-configure-microsoft-authentication/mobile-app-microsoftaccount-settings.png

<!-- URLs. -->

[Moje aplikacje]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Witryna Azure Portal]: https://portal.azure.com/
