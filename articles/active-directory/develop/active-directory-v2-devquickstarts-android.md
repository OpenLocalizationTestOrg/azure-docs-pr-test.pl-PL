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
# <a name="add-sign-in-tooan-android-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="cbcab-103">Dodaj tooan logowania aplikacji systemu Android przy użyciu biblioteki innych firm z interfejsu API programu Graph przy użyciu punktu końcowego v2.0 hello</span><span class="sxs-lookup"><span data-stu-id="cbcab-103">Add sign-in tooan Android app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="cbcab-104">korzysta z platformą tożsamości Microsoft Hello Otwórz standardy, takie jak OAuth2 i OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="cbcab-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="cbcab-105">Deweloperzy mogą używać dowolnej bibliotece mają toointegrate z naszych usług.</span><span class="sxs-lookup"><span data-stu-id="cbcab-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="cbcab-106">Deweloperzy toohelp używać platformy z innych bibliotek, możemy napisanych kilka wskazówki, takich jak ta toodemonstrate jeden sposób platformą tożsamości Microsoft tooconnect toohello tooconfigure bibliotek innych firm.</span><span class="sxs-lookup"><span data-stu-id="cbcab-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="cbcab-107">Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2 hello](https://tools.ietf.org/html/rfc6749) mogą łączyć się z platformą tożsamości Microsoft toohello.</span><span class="sxs-lookup"><span data-stu-id="cbcab-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="cbcab-108">Aplikacja hello, która tworzy tego przewodnika użytkownicy mogą zarejestrować się w organizacji tootheir i następnie wyszukaj się w organizacji za pomocą hello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcab-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for themselves in their organization by using hello Graph API.</span></span>

<span data-ttu-id="cbcab-109">Jeśli nowy tooOAuth2 lub OpenID Connect znacznie to przykładowa konfiguracja może nie mieć tooyou znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="cbcab-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="cbcab-110">Zalecamy przeczytanie [2.0 protokołów - przepływu kodu autoryzacji OAuth 2.0](active-directory-v2-protocols-oauth-code.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="cbcab-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="cbcab-111">Funkcje platformy, które mają wyrażenia w hello OAuth2 lub standardy OpenID Connect, takie jak dostęp warunkowy i zarządzanie zasadami usługi Intune, wymagają możesz toouse naszych Otwórz źródło bibliotek tożsamości usługi Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cbcab-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="cbcab-112">punktu końcowego v2.0 Hello nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji.</span><span class="sxs-lookup"><span data-stu-id="cbcab-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="cbcab-113">toodetermine, jeśli powinien używać punktu końcowego v2.0 hello, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="cbcab-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-hello-code-from-github"></a><span data-ttu-id="cbcab-114">Pobierz kod hello z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="cbcab-114">Download hello code from GitHub</span></span>
<span data-ttu-id="cbcab-115">Kod Hello w tym samouczku jest przechowywany [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="cbcab-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="cbcab-116">toofollow wzdłuż, możesz [pobrać szkielet aplikacji hello jako .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) lub klonowania hello szkielet:</span><span class="sxs-lookup"><span data-stu-id="cbcab-116">toofollow along, you can  [download hello app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="cbcab-117">Możesz także po prostu pobrać przykładowy hello i od razu rozpocząć:</span><span class="sxs-lookup"><span data-stu-id="cbcab-117">You can also just download hello sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="cbcab-118">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="cbcab-118">Register an app</span></span>
<span data-ttu-id="cbcab-119">Utwórz nową aplikację na powitania [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj hello szczegółowe kroki opisane w temacie [jak tooregister aplikacji z punktem końcowym v2.0 hello](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="cbcab-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="cbcab-120">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="cbcab-120">Make sure to:</span></span>

* <span data-ttu-id="cbcab-121">Kopiuj hello **identyfikator aplikacji** wynika to z przypisaną tooyour aplikacji należy ją szybko.</span><span class="sxs-lookup"><span data-stu-id="cbcab-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="cbcab-122">Dodaj hello **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbcab-122">Add hello **Mobile** platform for your app.</span></span>

> <span data-ttu-id="cbcab-123">Uwaga: portal rejestracji aplikacji hello zapewnia **identyfikator URI przekierowania** wartość.</span><span class="sxs-lookup"><span data-stu-id="cbcab-123">Note: hello Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="cbcab-124">Jednak w tym przykładzie należy użyć hello domyślna wartość `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="cbcab-124">However, in this example you must use hello default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-hello-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="cbcab-125">Pobierz hello NXOAuth2 innych firm biblioteki i tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="cbcab-125">Download hello NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="cbcab-126">W ramach tego przewodnika skorzystasz hello OIDCAndroidLib z serwisu GitHub, które jest oparte na powitania kod Google OpenID Connect biblioteką OAuth2.</span><span class="sxs-lookup"><span data-stu-id="cbcab-126">For this walkthrough, you will use hello OIDCAndroidLib from GitHub, which is an OAuth2 library based on hello OpenID Connect code of Google.</span></span> <span data-ttu-id="cbcab-127">Ona profilu natywnych aplikacji hello implementuje i obsługuje hello punktu końcowego autoryzacji użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="cbcab-127">It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="cbcab-128">Są to wszystko, co hello należy toointegrate z platformą tożsamości Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="cbcab-128">These are all hello things that you'll need toointegrate with hello Microsoft identity platform.</span></span>

<span data-ttu-id="cbcab-129">Klonowanie hello OIDCAndroidLib repozytorium tooyour komputera.</span><span class="sxs-lookup"><span data-stu-id="cbcab-129">Clone hello OIDCAndroidLib repo tooyour computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="cbcab-131">Konfigurowanie środowiska Android Studio</span><span class="sxs-lookup"><span data-stu-id="cbcab-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="cbcab-132">Utwórz nowy projekt Android Studio i zaakceptuj ustawienia domyślne powitania w Kreatorze hello.</span><span class="sxs-lookup"><span data-stu-id="cbcab-132">Create a new Android Studio project and accept hello defaults in hello wizard.</span></span>
   
    ![Utwórz nowy projekt w programie Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Docelowych urządzeń z systemem Android](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Dodaj toomobile działania](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="cbcab-136">tooset się moduły projektu, Przenieś hello sklonować repozytorium toohello projektu lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="cbcab-136">tooset up your project modules, move hello cloned repo toohello project location.</span></span> <span data-ttu-id="cbcab-137">Można także utworzyć hello projektu, a następnie sklonować go bezpośrednio toohello lokalizacji projektu.</span><span class="sxs-lookup"><span data-stu-id="cbcab-137">You can also create hello project and then clone it directly toohello project location.</span></span>
   
    ![Moduły projektu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="cbcab-139">Otwórz ustawienia modułów projektu hello za pomocą menu kontekstowe hello lub przy użyciu skrótu Ctrl + Alt + główn + S hello.</span><span class="sxs-lookup"><span data-stu-id="cbcab-139">Open hello project modules settings by using hello context menu or by using hello Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Ustawienia modułów projektu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="cbcab-141">Usuń moduł aplikacji domyślne hello, ponieważ tylko ustawienia hello projektu kontenera.</span><span class="sxs-lookup"><span data-stu-id="cbcab-141">Remove hello default app module because you only want hello project container settings.</span></span>
   
    ![Witaj domyślnego modułu aplikacji](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="cbcab-143">Zaimportuj moduły z hello sklonowanego repozytorium toohello bieżącego projektu.</span><span class="sxs-lookup"><span data-stu-id="cbcab-143">Import modules from hello cloned repo toohello current project.</span></span>
   
    <span data-ttu-id="cbcab-144">![Importowanie projektu gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Utwórz nową stronę modułu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="cbcab-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="cbcab-145">Powtórz te kroki dla hello `oidlib-sample` modułu.</span><span class="sxs-lookup"><span data-stu-id="cbcab-145">Repeat these steps for hello `oidlib-sample` module.</span></span>
7. <span data-ttu-id="cbcab-146">Sprawdź zależności oidclib hello na powitania `oidlib-sample` modułu.</span><span class="sxs-lookup"><span data-stu-id="cbcab-146">Check hello oidclib dependencies on hello `oidlib-sample` module.</span></span>
   
    ![zależności oidclib na powitania próbki oidlib modułu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="cbcab-148">Kliknij przycisk **OK** i poczekaj, aż synchronizacja narzędzia gradle.</span><span class="sxs-lookup"><span data-stu-id="cbcab-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="cbcab-149">Twoje settings.gradle powinna wyglądać:</span><span class="sxs-lookup"><span data-stu-id="cbcab-149">Your settings.gradle should look like:</span></span>
   
    ![Zrzut ekranu przedstawiający settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="cbcab-151">Tworzenie hello przykładowej aplikacji toomake się z próbką hello poprawnie działać.</span><span class="sxs-lookup"><span data-stu-id="cbcab-151">Build hello sample app toomake sure that hello sample running correctly.</span></span>
   
    <span data-ttu-id="cbcab-152">Użytkownik nie będzie możliwe toouse to usłudze Azure Active Directory jeszcze.</span><span class="sxs-lookup"><span data-stu-id="cbcab-152">You won't be able toouse this with Azure Active Directory yet.</span></span> <span data-ttu-id="cbcab-153">Potrzebujemy tooconfigure niektóre punkty końcowe najpierw.</span><span class="sxs-lookup"><span data-stu-id="cbcab-153">We'll need tooconfigure some endpoints first.</span></span> <span data-ttu-id="cbcab-154">Jest to tooensure masz problemy z systemem Android Studio przed Rozpoczniemy Dostosowywanie hello przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cbcab-154">This is tooensure you don't have an Android Studio issues before we start customizing hello sample app.</span></span>
10. <span data-ttu-id="cbcab-155">Tworzenie i uruchamianie `oidlib-sample` jako cel hello w programie Android Studio.</span><span class="sxs-lookup"><span data-stu-id="cbcab-155">Build and run `oidlib-sample` as hello target in Android Studio.</span></span>
    
    ![Postęp kompilacji oidlib próbki](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="cbcab-157">Usuń hello `app ` katalogu, w którym pozostawało po usunięciu hello modułu z hello projektu, ponieważ Android Studio nie powoduje usunięcia go dla bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="cbcab-157">Delete hello `app ` directory that was left when you removed hello module from hello project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Struktura pliku, który zawiera katalog aplikacji hello](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="cbcab-159">Otwórz hello **Edytuj konfiguracje** menu tooremove hello Uruchom konfigurację, która również pozostawało usunięcie modułu hello z hello projektu.</span><span class="sxs-lookup"><span data-stu-id="cbcab-159">Open hello **Edit Configurations** menu tooremove hello run configuration that was also left when you removed hello module from hello project.</span></span>
    
    <span data-ttu-id="cbcab-160">![Edytuj konfiguracje menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Uruchom konfiguracji aplikacji](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="cbcab-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-hello-endpoints-of-hello-sample"></a><span data-ttu-id="cbcab-161">Skonfiguruj punkty końcowe hello hello próbki</span><span class="sxs-lookup"><span data-stu-id="cbcab-161">Configure hello endpoints of hello sample</span></span>
<span data-ttu-id="cbcab-162">Teraz, gdy masz hello `oidlib-sample` uruchomiony pomyślnie, umożliwia edytowanie tooget niektóre punkty końcowe tej pracy z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbcab-162">Now that you have hello `oidlib-sample` running successfully, let's edit some endpoints tooget this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-hello-oidcclientconfxml-file"></a><span data-ttu-id="cbcab-163">Konfigurowanie klienta, edytując plik oidc_clientconf.xml hello</span><span class="sxs-lookup"><span data-stu-id="cbcab-163">Configure your client by editing hello oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="cbcab-164">Ponieważ używasz OAuth2 przepływów tylko tooget token i wywołania interfejsu API programu Graph hello, należy ustawić hello toodo klienta OAuth2 tylko.</span><span class="sxs-lookup"><span data-stu-id="cbcab-164">Because you are using OAuth2 flows only tooget a token and call hello Graph API, set hello client toodo OAuth2 only.</span></span> <span data-ttu-id="cbcab-165">OIDC wejdzie w przykładzie nowsze.</span><span class="sxs-lookup"><span data-stu-id="cbcab-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="cbcab-166">Konfigurowanie Identyfikatora klienta, otrzymany z hello portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="cbcab-166">Configure your client ID that you received from hello registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="cbcab-167">Skonfiguruj przekierowania URI z hello jedną poniżej.</span><span class="sxs-lookup"><span data-stu-id="cbcab-167">Configure your redirect URI with hello one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="cbcab-168">Skonfiguruj zakresach czy użytkownik musi w kolejności tooaccess hello interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcab-168">Configure your scopes that you need in order tooaccess hello Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="cbcab-169">Witaj `User.Read` wartość w `oidc_scopes` umożliwia możesz tooread hello profilu podstawowego hello zalogowany użytkownik.</span><span class="sxs-lookup"><span data-stu-id="cbcab-169">hello `User.Read` value in `oidc_scopes` allows you tooread hello basic profile hello signed in user.</span></span>
<span data-ttu-id="cbcab-170">Dowiedz się więcej o wszystkie dostępne zakresy hello na [zakresy uprawnień Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="cbcab-170">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="cbcab-171">Jeśli chcesz wyjaśnień dotyczących `openid` lub `offline_access` jako zakresów w OpenID Connect, zobacz [2.0 protokołów - przepływu kodu autoryzacji OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="cbcab-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-hello-oidcendpointsxml-file"></a><span data-ttu-id="cbcab-172">Skonfiguruj punkty końcowe klienta, edytując plik oidc_endpoints.xml hello</span><span class="sxs-lookup"><span data-stu-id="cbcab-172">Configure your client endpoints by editing hello oidc_endpoints.xml file</span></span>
* <span data-ttu-id="cbcab-173">Otwórz hello `oidc_endpoints.xml` plików i wprowadź następujące zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="cbcab-173">Open hello `oidc_endpoints.xml` file and make hello following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="cbcab-174">Tymi punktami końcowymi nigdy nie należy zmieniać, jeśli używasz protokołu OAuth2 jako protokołów.</span><span class="sxs-lookup"><span data-stu-id="cbcab-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="cbcab-175">Witaj punktów końcowych dla `userInfoEndpoint` i `revocationEndpoint` nie są obecnie obsługiwane przez usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbcab-175">hello endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="cbcab-176">Pozostawienie tych z wartością example.com domyślną hello przypomnienie pojawi się czy nie są one dostępne w przykładowym hello :-)</span><span class="sxs-lookup"><span data-stu-id="cbcab-176">If you leave these with hello default example.com value, you will be reminded that they are not available in hello sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="cbcab-177">Konfigurowanie wywołania interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="cbcab-177">Configure a Graph API call</span></span>
* <span data-ttu-id="cbcab-178">Otwórz hello `HomeActivity.java` plików i wprowadź następujące zmiany hello:</span><span class="sxs-lookup"><span data-stu-id="cbcab-178">Open hello `HomeActivity.java` file and make hello following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="cbcab-179">W tym miejscu proste wywołania interfejsu API programu Graph zwraca naszych informacje.</span><span class="sxs-lookup"><span data-stu-id="cbcab-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="cbcab-180">Są to wszystkie zmiany hello konieczność toodo.</span><span class="sxs-lookup"><span data-stu-id="cbcab-180">Those are all hello changes that you need toodo.</span></span> <span data-ttu-id="cbcab-181">Uruchom hello `oidlib-sample` aplikacji, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="cbcab-181">Run hello `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="cbcab-182">Po pomyślnie uwierzytelniono, wybierz hello **żądania zasobów chronionych** przycisk tootest Twojego toohello wywołania interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="cbcab-182">After you've successfully authenticated, select hello **Request Protected Resource** button tootest your call toohello Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="cbcab-183">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="cbcab-183">Get security updates for our product</span></span>
<span data-ttu-id="cbcab-184">Firma Microsoft zachęca tooget powiadomień dotyczących zdarzeń, przechodząc na stronę hello [Witryna TechCenter poświęcona zabezpieczeniom](https://technet.microsoft.com/security/dd252948) i subskrypcji tooSecurity doradczych alertów.</span><span class="sxs-lookup"><span data-stu-id="cbcab-184">We encourage you tooget notifications about security incidents by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

