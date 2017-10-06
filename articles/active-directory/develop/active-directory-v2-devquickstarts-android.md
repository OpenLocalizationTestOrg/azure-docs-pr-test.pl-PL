---
title: "aaaAzure aplikacji systemu Android w wersji 2.0 usługi Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toobuild aplikację systemu Android, który loguje się użytkownikom zarówno osobistego konta Microsoft i pracy lub kont służbowych i wywołania hello interfejsu API programu Graph przy użyciu bibliotek innych firm."
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 16294c07-f27d-45c9-833f-7dbb12083794
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1dd40bd3bcea28c629abce09abaed66b38774162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Dodaj tooan logowania aplikacji systemu Android przy użyciu biblioteki innych firm z interfejsu API programu Graph przy użyciu punktu końcowego v2.0 hello
korzysta z platformą tożsamości Microsoft Hello Otwórz standardy, takie jak OAuth2 i OpenID Connect. Deweloperzy mogą używać dowolnej bibliotece mają toointegrate z naszych usług. Deweloperzy toohelp używać platformy z innych bibliotek, możemy napisanych kilka wskazówki, takich jak ta toodemonstrate jeden sposób platformą tożsamości Microsoft tooconnect toohello tooconfigure bibliotek innych firm. Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2 hello](https://tools.ietf.org/html/rfc6749) mogą łączyć się z platformą tożsamości Microsoft toohello.

Aplikacja hello, która tworzy tego przewodnika użytkownicy mogą zarejestrować się w organizacji tootheir i następnie wyszukaj się w organizacji za pomocą hello interfejsu API programu Graph.

Jeśli nowy tooOAuth2 lub OpenID Connect znacznie to przykładowa konfiguracja może nie mieć tooyou znaczeniu. Zalecamy przeczytanie [2.0 protokołów - przepływu kodu autoryzacji OAuth 2.0](active-directory-v2-protocols-oauth-code.md) w tle.

> [!NOTE]
> Funkcje platformy, które mają wyrażenia w hello OAuth2 lub standardy OpenID Connect, takie jak dostęp warunkowy i zarządzanie zasadami usługi Intune, wymagają możesz toouse naszych Otwórz źródło bibliotek tożsamości usługi Microsoft Azure.
> 
> 

punktu końcowego v2.0 Hello nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji.

> [!NOTE]
> toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).
> 
> 

## <a name="download-hello-code-from-github"></a>Pobierz kod hello z usługi GitHub
Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).  toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) lub klonowania hello szkielet:

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

Możesz także po prostu pobrać przykładowy hello i od razu rozpocząć:

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a>Rejestracja aplikacji
Utwórz nową aplikację na powitania [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj hello szczegółowe kroki opisane w temacie [jak tooregister aplikacji z punktem końcowym v2.0 hello](active-directory-v2-app-registration.md).  Upewnij się, że:

* Kopiuj hello **identyfikator aplikacji** wynika to z przypisaną tooyour aplikacji należy ją szybko.
* Dodaj hello **Mobile** platformy aplikacji.

> Uwaga: portal rejestracji aplikacji hello zapewnia **identyfikator URI przekierowania** wartość. Jednak w tym przykładzie należy użyć hello domyślna wartość `https://login.microsoftonline.com/common/oauth2/nativeclient`.
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a>Pobierz hello NXOAuth2 innych firm biblioteki i tworzenie obszaru roboczego
W ramach tego przewodnika skorzystasz hello OIDCAndroidLib z serwisu GitHub, które jest oparte na powitania kod Google OpenID Connect biblioteką OAuth2. Ona profilu natywnych aplikacji hello implementuje i obsługuje hello punktu końcowego autoryzacji użytkownika hello. Są to wszystko, co hello należy toointegrate z platformą tożsamości Microsoft hello.

Klonowanie hello OIDCAndroidLib repozytorium tooyour komputera.

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a>Konfigurowanie środowiska Android Studio
1. Utwórz nowy projekt Android Studio i zaakceptuj ustawienia domyślne powitania w Kreatorze hello.
   
    ![Utwórz nowy projekt w programie Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Docelowych urządzeń z systemem Android](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Dodaj toomobile działania](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. tooset się moduły projektu, Przenieś hello sklonować repozytorium toohello projektu lokalizacji. Można także utworzyć hello projektu, a następnie sklonować go bezpośrednio toohello lokalizacji projektu.
   
    ![Moduły projektu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. Otwórz ustawienia modułów projektu hello za pomocą menu kontekstowe hello lub przy użyciu skrótu Ctrl + Alt + główn + S hello.
   
    ![Ustawienia modułów projektu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. Usuń moduł aplikacji domyślne hello, ponieważ tylko ustawienia hello projektu kontenera.
   
    ![Witaj domyślnego modułu aplikacji](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. Zaimportuj moduły z hello sklonowanego repozytorium toohello bieżącego projektu.
   
    ![Importowanie projektu gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Utwórz nową stronę modułu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)
6. Powtórz te kroki dla hello `oidlib-sample` modułu.
7. Sprawdź zależności oidclib hello na powitania `oidlib-sample` modułu.
   
    ![zależności oidclib na powitania próbki oidlib modułu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. Kliknij przycisk **OK** i poczekaj, aż synchronizacja narzędzia gradle.
   
    Twoje settings.gradle powinna wyglądać:
   
    ![Zrzut ekranu przedstawiający settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. Tworzenie hello przykładowej aplikacji toomake się z próbką hello poprawnie działać.
   
    Użytkownik nie będzie możliwe toouse to usłudze Azure Active Directory jeszcze. Potrzebujemy tooconfigure niektóre punkty końcowe najpierw. Jest to tooensure masz problemy z systemem Android Studio przed Rozpoczniemy Dostosowywanie hello przykładowej aplikacji.
10. Tworzenie i uruchamianie `oidlib-sample` jako cel hello w programie Android Studio.
    
    ![Postęp kompilacji oidlib próbki](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. Usuń hello `app ` katalogu, w którym pozostawało po usunięciu hello modułu z hello projektu, ponieważ Android Studio nie powoduje usunięcia go dla bezpieczeństwa.
    
    ![Struktura pliku, który zawiera katalog aplikacji hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. Otwórz hello **Edytuj konfiguracje** menu tooremove hello Uruchom konfigurację, która również pozostawało usunięcie modułu hello z hello projektu.
    
    ![Edytuj konfiguracje menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Uruchom konfiguracji aplikacji](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)

## <a name="configure-hello-endpoints-of-hello-sample"></a>Skonfiguruj punkty końcowe hello hello próbki
Teraz, gdy masz hello `oidlib-sample` uruchomiony pomyślnie, umożliwia edytowanie tooget niektóre punkty końcowe tej pracy z usługą Azure Active Directory.

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a>Konfigurowanie klienta, edytując plik oidc_clientconf.xml hello
1. Ponieważ używasz OAuth2 przepływów tylko tooget token i wywołania interfejsu API programu Graph hello, należy ustawić hello toodo klienta OAuth2 tylko. OIDC wejdzie w przykładzie nowsze.
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. Konfigurowanie Identyfikatora klienta, otrzymany z hello portalu rejestracji.
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. Skonfiguruj przekierowania URI z hello jedną poniżej.
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. Skonfiguruj zakresach czy użytkownik musi w kolejności tooaccess hello interfejsu API programu Graph.
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

Witaj `User.Read` wartość w `oidc_scopes` umożliwia możesz tooread hello profilu podstawowego hello zalogowany użytkownik.
Dowiedz się więcej o wszystkie dostępne zakresy hello na [zakresy uprawnień Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Jeśli chcesz wyjaśnień dotyczących `openid` lub `offline_access` jako zakresów w OpenID Connect, zobacz [2.0 protokołów - przepływu kodu autoryzacji OAuth 2.0](active-directory-v2-protocols-oauth-code.md).

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a>Skonfiguruj punkty końcowe klienta, edytując plik oidc_endpoints.xml hello
* Otwórz hello `oidc_endpoints.xml` plików i wprowadź następujące zmiany hello:
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

Tymi punktami końcowymi nigdy nie należy zmieniać, jeśli używasz protokołu OAuth2 jako protokołów.

> [!NOTE]
> Witaj punktów końcowych dla `userInfoEndpoint` i `revocationEndpoint` nie są obecnie obsługiwane przez usługę Azure Active Directory. Pozostawienie tych z wartością example.com domyślną hello przypomnienie pojawi się czy nie są one dostępne w przykładowym hello :-)
> 
> 

## <a name="configure-a-graph-api-call"></a>Konfigurowanie wywołania interfejsu API programu Graph
* Otwórz hello `HomeActivity.java` plików i wprowadź następujące zmiany hello:
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

W tym miejscu proste wywołania interfejsu API programu Graph zwraca naszych informacje.

Są to wszystkie zmiany hello konieczność toodo. Uruchom hello `oidlib-sample` aplikacji, a następnie kliknij przycisk **Zaloguj**.

Po pomyślnie uwierzytelniono, wybierz hello **żądania zasobów chronionych** przycisk tootest Twojego toohello wywołania interfejsu API programu Graph.

## <a name="get-security-updates-for-our-product"></a>Pobierz aktualizacje zabezpieczeń naszych produktów
Firma Microsoft zachęca tooget powiadomień dotyczących zdarzeń, przechodząc na stronę hello [Witryna TechCenter poświęcona zabezpieczeniom](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.

