---
title: "Uwierzytelnianie usługi Azure Active Directory tooconfigure aaaHow dla aplikacji usługi aplikacji"
description: "Dowiedz się, jak tooconfigure uwierzytelniania usługi Azure Active Directory dla aplikacji usługi aplikacji."
author: mattchenderson
services: app-service
documentationcenter: 
manager: syntaxc4
editor: 
ms.assetid: 6ec6a46c-bce4-47aa-b8a3-e133baef22eb
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5b1d73f8fdf5831a266d900cd07f4e3b0917a7f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-your-app-service-application-toouse-azure-active-directory-login"></a>Jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji usługi aplikacji
[!INCLUDE [app-service-mobile-selector-authentication](../../includes/app-service-mobile-selector-authentication.md)]

W tym temacie opisano sposób tooconfigure toouse usługi aplikacji Azure usługi Azure Active Directory jako dostawcy uwierzytelniania.

## <a name="express"></a>Konfigurowanie usługi Azure Active Directory przy użyciu ustawień ekspresowych
1. W hello [portalu Azure], przejdź tooyour aplikacji. Kliknij przycisk **ustawienia**, a następnie **uwierzytelniania/autoryzacji**.
2. Jeśli hello uwierzytelniania / autoryzacji funkcja nie jest włączona, włącz przełącznik hello zbyt**na**.
3. Kliknij przycisk **usługi Azure Active Directory**, a następnie kliknij przycisk **Express** w obszarze **tryb zarządzania**.
4. Kliknij przycisk **OK** tooregister hello aplikacji w usłudze Azure Active Directory. Spowoduje to utworzenie nowej rejestracji. Jeśli zamiast tego chcesz toochoose rejestracją istniejącą, kliknij przycisk **wybierz istniejącą aplikację** , a następnie wyszukaj nazwę hello utworzonej wcześniej rejestracji w ramach dzierżawy.
   Kliknij przycisk tooselect rejestracji hello go i kliknij przycisk **OK**. Następnie kliknij przycisk **OK** w bloku ustawień hello Azure Active Directory.
   
   ![][0]
   
   Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API. Musisz zezwolić użytkownikom w kodzie aplikacji.
5. Uwierzytelniony przez usługę Azure Active Directory (opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkownicy **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Zaloguj się za pomocą usługi Azure Active Directory**. Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są przekierowane tooAzure usługi Active Directory do uwierzytelniania.
6. Kliknij pozycję **Zapisz**.

Wszystko jest teraz gotowy toouse usługi Azure Active Directory do uwierzytelniania w aplikacji.

## <a name="advanced"></a>(Metoda alternatywna) ręcznie skonfigurować usługi Azure Active Directory z ustawieniami zaawansowanymi
Możesz również wybrać tooprovide konfiguracji ustawienia ręcznie. Jeśli chcesz toouse dzierżawę usługi AAD hello różni się od dzierżawcy hello, z którym należy zalogować się do usługi Azure jest hello preferowane rozwiązanie. toocomplete hello konfiguracji, należy najpierw utworzyć rejestracji w usłudze Azure Active Directory, a należy podać niektóre hello rejestracji szczegóły tooApp usługi.

### <a name="register"></a>Zarejestrować aplikację w usłudze Azure Active Directory
1. Zaloguj się na toohello [portalu Azure]i przejdź tooyour aplikacji. Kopiowanie z **adres URL**. Użyjesz tooconfigure tej aplikacji usługi Azure Active Directory.
2. Zaloguj się toohello [klasycznego portalu Azure] i przejdź zbyt**usługi Active Directory**.
   
    ![][2]
3. Wybierz katalog, a następnie wybierz hello **aplikacji** u góry hello. Kliknij przycisk **dodać** na powitania dolnej toocreate nowej rejestracji aplikacji.
4. Kliknij przycisk **Dodaj aplikację moją organizację**.
5. W Kreatorze dodawania aplikacji hello, wprowadź **nazwa** dla twojej aplikacji i kliknij przycisk hello **interfejsu API sieci Web i/lub aplikacji sieci Web** typu. Następnie kliknij przycisk toocontinue.
6. W hello **adres URL logowania** Wklej skopiowane wcześniej adres URL aplikacji hello. Wprowadź tego samego adresu URL w hello **identyfikator URI aplikacji** pole. Następnie kliknij przycisk toocontinue.
7. Po dodaniu aplikacji hello kliknij hello **Konfiguruj** kartę. Edytuj hello **adres URL odpowiedzi** w obszarze **rejestracji jednokrotnej** toobe hello adres URL aplikacji dołączony ścieżki hello */.auth/login/aad/callback*. Na przykład `https://contoso.azurewebsites.net/.auth/login/aad/callback`. Upewnij się, że używasz hello schematu HTTPS.
   
    ![][3]
8. Kliknij pozycję **Zapisz**. Następnie hello kopiowania **identyfikator klienta** aplikacji hello. Skonfiguruj toouse Twojej aplikacji to później.
9. Na pasku poleceń dolnej hello, kliknij przycisk **Wyświetl punkty końcowe**i następnie kopiowania hello **dokument metadanych usług federacyjnych** adresu URL i pobierania dokumentu lub przejdź tooit w przeglądarce.
10. W głównym hello **EntityDescriptor** elementu, powinny być **entityID** atrybutu formularza hello `https://sts.windows.net/` następuje dzierżawcy tooyour określonego identyfikatora GUID (nazywanych "identyfikator dzierżawy"). Skopiuj tę wartość — będzie służyć jako sieci **adres URL wystawcy**. Skonfiguruj toouse Twojej aplikacji to później.

### <a name="secrets"></a>Dodaj usługi Azure Active Directory informacji tooyour aplikacji
1. Po powrocie do hello [portalu Azure], przejdź tooyour aplikacji. Kliknij przycisk **ustawienia**, a następnie **uwierzytelniania/autoryzacji**.
2. Jeśli nie włączono funkcji uwierzytelniania/autoryzacji hello, włącz przełącznik hello zbyt**na**.
3. Kliknij przycisk **usługi Azure Active Directory**, a następnie kliknij przycisk **zaawansowane** w obszarze **tryb zarządzania**. Wklej w hello identyfikator klienta i adres URL wystawcy wartość, która będzie uzyskany wcześniej. Następnie kliknij przycisk **OK**.
   
   ![][1]
   
   Domyślnie usługi App Service zapewnia uwierzytelnianie, ale nie ogranicza autoryzowany dostęp do zawartości witryny tooyour i interfejsów API. Musisz zezwolić użytkownikom w kodzie aplikacji.
4. Uwierzytelniony przez usługę Azure Active Directory (opcjonalnie) toorestrict dostępu tooyour lokacji tooonly użytkownicy **tootake akcji w przypadku nieuwierzytelnionego żądania** za**Zaloguj się za pomocą usługi Azure Active Directory**. Wymaga to, że wszystkie żądania uwierzytelnienia, a wszystkie nieuwierzytelnione żądania są przekierowane tooAzure usługi Active Directory do uwierzytelniania.
5. Kliknij pozycję **Zapisz**.

Wszystko jest teraz gotowy toouse usługi Azure Active Directory do uwierzytelniania w aplikacji.

## <a name="optional-configure-a-native-client-application"></a>(Opcjonalnie) Skonfiguruj aplikację native client
Usługa Azure Active Directory umożliwia także tooregister klientach natywnych, co zapewnia większą kontrolę nad uprawnieniami mapowania. Należy to w razie potrzeby tooperform logowania za pomocą biblioteki, takich jak hello **biblioteki uwierzytelniania usługi Active Directory**.

1. Przejdź za**usługi Active Directory** w hello [klasycznego portalu Azure].
2. Wybierz katalog, a następnie wybierz hello **aplikacji** u góry hello. Kliknij przycisk **dodać** na powitania dolnej toocreate nowej rejestracji aplikacji.
3. Kliknij przycisk **Dodaj aplikację moją organizację**.
4. W Kreatorze dodawania aplikacji hello, wprowadź **nazwa** dla twojej aplikacji i kliknij przycisk hello **natywną aplikację kliencką** typu. Następnie kliknij przycisk toocontinue.
5. W hello **identyfikator URI przekierowania** wprowadź witryny */.auth/login/done* punktu końcowego, za pomocą hello schematu HTTPS. Ta wartość powinna być podobna zbyt*https://contoso.azurewebsites.net/.auth/login/done*. W przypadku tworzenia aplikacji systemu Windows, zamiast tego użyć hello [identyfikatora SID pakietu](app-service-mobile-dotnet-how-to-use-client-library.md#package-sid) jako hello identyfikatora URI.
6. Po dodaniu aplikacji natywnej powitania kliknij hello **Konfiguruj** kartę. Znajdź hello **identyfikator klienta** i zanotuj tę wartość.
7. Strona hello przewiń w dół toohello **uprawnienia aplikacji tooother** sekcji, a następnie kliknij przycisk **Dodaj aplikację**.
8. Wyszukaj hello aplikacji sieci web, który został wcześniej zarejestrowany, a następnie kliknij przycisk hello plus ikony. Następnie kliknij przycisk hello wyboru tooclose hello w oknie dialogowym. Jeśli hello aplikacji sieci web nie można odnaleźć, przejdź tooits rejestracji i dodać nowy adres URL odpowiedzi (np. hello wersji HTTP bieżącą adres URL), kliknij przycisk Zapisz, a następnie powtórz te kroki — powinny być widoczne aplikacji hello hello na liście.
9. Na powitania właśnie dodano nowy wpis, otwórz hello **delegowane uprawnienia** listy rozwijanej i wybierz **dostępu (appName)**. Następnie kliknij przycisk **Save** (Zapisz).

Aplikację native client, który ma dostęp do aplikacji usługi aplikacji został skonfigurowany.

## <a name="related-content"></a>Związane z zawartością
[!INCLUDE [app-service-mobile-related-content-get-started-users](../../includes/app-service-mobile-related-content-get-started-users.md)]

<!-- Images. -->

[0]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-express-settings.png
[1]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/mobile-app-aad-advanced-settings.png
[2]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-navigate-aad.png
[3]: ./media/app-service-mobile-how-to-configure-active-directory-authentication/app-service-aad-app-configure.png

<!-- URLs. -->

[portalu Azure]: https://portal.azure.com/
[klasycznego portalu Azure]: https://manage.windowsazure.com/
[alternative method]:#advanced
