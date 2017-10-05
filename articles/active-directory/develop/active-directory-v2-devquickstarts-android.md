---
title: "Aplikacji systemu Android w wersji 2.0 usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak utworzyć aplikację systemu Android, logujący się użytkownicy posiadający zarówno osobistego konta Microsoft i pracy lub kont służbowych i wywołania interfejsu API programu Graph przy użyciu bibliotek innych firm."
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
ms.openlocfilehash: c0a5a818c61f7af7ff04bf890b54e8364f3b21b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-an-android-app-using-a-third-party-library-with-graph-api-using-the-v20-endpoint"></a><span data-ttu-id="35d42-103">Dodaj logowanie do aplikacji systemu Android przy użyciu biblioteki innych firm z interfejsu API programu Graph przy użyciu punktu końcowego v2.0</span><span class="sxs-lookup"><span data-stu-id="35d42-103">Add sign-in to an Android app using a third-party library with Graph API using the v2.0 endpoint</span></span>
<span data-ttu-id="35d42-104">Platforma Microsoft Identity korzysta z otwartych standardów, takich jak OAuth2 i OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="35d42-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="35d42-105">Deweloperzy mogą używać dowolnej bibliotece potrzebnymi do integracji z naszych usług.</span><span class="sxs-lookup"><span data-stu-id="35d42-105">Developers can use any library they want to integrate with our services.</span></span> <span data-ttu-id="35d42-106">Aby pomóc deweloperom korzystać z innych bibliotek platformy, możemy napisanych kilka wskazówki podobny do pokazują, jak skonfigurować biblioteki innych firm, aby nawiązać połączenia z platformą tożsamości Microsoft.</span><span class="sxs-lookup"><span data-stu-id="35d42-106">To help developers use our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure third-party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="35d42-107">Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) można nawiązać połączenia z platformą tożsamości Microsoft.</span><span class="sxs-lookup"><span data-stu-id="35d42-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect to the Microsoft identity platform.</span></span>

<span data-ttu-id="35d42-108">Aplikacja, która tworzy tego przewodnika użytkownicy mogą zalogować się do organizacji i następnie wyszukaj się w organizacji za pomocą interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="35d42-108">With the application that this walkthrough creates, users can sign in to their organization and then search for themselves in their organization by using the Graph API.</span></span>

<span data-ttu-id="35d42-109">Jeśli jesteś nowym użytkownikiem OAuth2 lub OpenID Connect, znacznie to przykładowa konfiguracja może nie mieć sensu do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="35d42-109">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make sense to you.</span></span> <span data-ttu-id="35d42-110">Zalecamy przeczytanie [2.0 protokołów - przepływu kodu autoryzacji OAuth 2.0](active-directory-v2-protocols-oauth-code.md) w tle.</span><span class="sxs-lookup"><span data-stu-id="35d42-110">We recommend that you read [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="35d42-111">Niektóre funkcje platformy, które mają wyrażenia OAuth2 lub OpenID Connect standardy, takie jak dostęp warunkowy i zarządzanie zasadami usługi Intune, trzeba użyć naszych Otwórz źródło bibliotek tożsamości usługi Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="35d42-111">Some features of our platform that do have an expression in the OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you to use our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="35d42-112">Punktu końcowego v2.0 nie obsługuje wszystkich scenariuszy Azure Active Directory i funkcji.</span><span class="sxs-lookup"><span data-stu-id="35d42-112">The v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="35d42-113">Aby ustalić, czy należy używać punktu końcowego v2.0, przeczytaj o [ograniczenia v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="35d42-113">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-the-code-from-github"></a><span data-ttu-id="35d42-114">Pobierz kod z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="35d42-114">Download the code from GitHub</span></span>
<span data-ttu-id="35d42-115">Kod używany w tym samouczku jest przechowywany [ w serwisie GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span><span class="sxs-lookup"><span data-stu-id="35d42-115">The code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2).</span></span>  <span data-ttu-id="35d42-116">Aby z niego skorzystać, można [pobrać szkielet aplikacji w formie .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) lub sklonować szkielet:</span><span class="sxs-lookup"><span data-stu-id="35d42-116">To follow along, you can  [download the app's skeleton as a .zip](https://github.com/Azure-Samples/active-directory-android-native-oidcandroidlib-v2/archive/skeleton.zip) or clone the skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

<span data-ttu-id="35d42-117">Można także po prostu pobrać przykład i od razu rozpocząć:</span><span class="sxs-lookup"><span data-stu-id="35d42-117">You can also just download the sample and get started right away:</span></span>

```
git@github.com:Azure-Samples/active-directory-android-native-oidcandroidlib-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="35d42-118">Rejestracja aplikacji</span><span class="sxs-lookup"><span data-stu-id="35d42-118">Register an app</span></span>
<span data-ttu-id="35d42-119">Utwórz nową aplikację na [portalu rejestracji aplikacji](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), lub wykonaj szczegółowy opis kroków w [jak zarejestrować aplikację z punktem końcowym v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="35d42-119">Create a new app at the [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow the detailed steps at [How to register an app with the v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="35d42-120">Upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="35d42-120">Make sure to:</span></span>

* <span data-ttu-id="35d42-121">Kopiuj **identyfikator aplikacji** przypisany do aplikacji, ponieważ będzie on potrzebny wkrótce.</span><span class="sxs-lookup"><span data-stu-id="35d42-121">Copy the **Application Id** that's assigned to your app because you'll need it soon.</span></span>
* <span data-ttu-id="35d42-122">Dodaj **Mobile** platformy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35d42-122">Add the **Mobile** platform for your app.</span></span>

> <span data-ttu-id="35d42-123">Uwaga: Portal rejestracji aplikacji udostępnia **identyfikator URI przekierowania** wartość.</span><span class="sxs-lookup"><span data-stu-id="35d42-123">Note: The Application registration portal provides a **Redirect URI** value.</span></span> <span data-ttu-id="35d42-124">Jednak w tym przykładzie należy użyć wartość domyślną `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span><span class="sxs-lookup"><span data-stu-id="35d42-124">However, in this example you must use the default value of `https://login.microsoftonline.com/common/oauth2/nativeclient`.</span></span>
> 
> 

## <a name="download-the-nxoauth2-third-party-library-and-create-a-workspace"></a><span data-ttu-id="35d42-125">Pobierz NXOAuth2 biblioteki innych firm i tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="35d42-125">Download the NXOAuth2 third-party library and create a workspace</span></span>
<span data-ttu-id="35d42-126">W ramach tego przewodnika skorzystasz OIDCAndroidLib z serwisu GitHub, które jest oparte na kodzie Google OpenID Connect biblioteką OAuth2.</span><span class="sxs-lookup"><span data-stu-id="35d42-126">For this walkthrough, you will use the OIDCAndroidLib from GitHub, which is an OAuth2 library based on the OpenID Connect code of Google.</span></span> <span data-ttu-id="35d42-127">Ona profil aplikacji natywnej implementuje i obsługuje punktu końcowego autoryzacji użytkownika.</span><span class="sxs-lookup"><span data-stu-id="35d42-127">It implements the native application profile and supports the authorization endpoint of the user.</span></span> <span data-ttu-id="35d42-128">Są to wszystkie czynności, które należy zintegrować z platformą tożsamości Microsoft.</span><span class="sxs-lookup"><span data-stu-id="35d42-128">These are all the things that you'll need to integrate with the Microsoft identity platform.</span></span>

<span data-ttu-id="35d42-129">Klonowanie repozytorium OIDCAndroidLib do komputera.</span><span class="sxs-lookup"><span data-stu-id="35d42-129">Clone the OIDCAndroidLib repo to your computer.</span></span>

```
git@github.com:kalemontes/OIDCAndroidLib.git
```

![androidStudio](../media/active-directory-android-native-oidcandroidlib-v2/emotes-url.png)

## <a name="set-up-your-android-studio-environment"></a><span data-ttu-id="35d42-131">Konfigurowanie środowiska Android Studio</span><span class="sxs-lookup"><span data-stu-id="35d42-131">Set up your Android Studio environment</span></span>
1. <span data-ttu-id="35d42-132">Utwórz nowy projekt Android Studio i zaakceptuj ustawienia domyślne w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="35d42-132">Create a new Android Studio project and accept the defaults in the wizard.</span></span>
   
    ![Utwórz nowy projekt w programie Android Studio](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample1.PNG)
   
    ![Docelowych urządzeń z systemem Android](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample2.PNG)
   
    ![Dodawanie działania na telefon komórkowy](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample3.PNG)
2. <span data-ttu-id="35d42-136">Aby skonfigurować moduły projektu, należy przenieść sklonowanego repozytorium do lokalizacji projektu.</span><span class="sxs-lookup"><span data-stu-id="35d42-136">To set up your project modules, move the cloned repo to the project location.</span></span> <span data-ttu-id="35d42-137">Można także utworzyć projekt, a następnie sklonować bezpośrednio do lokalizacji projektu.</span><span class="sxs-lookup"><span data-stu-id="35d42-137">You can also create the project and then clone it directly to the project location.</span></span>
   
    ![Moduły projektu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4_1.PNG)
3. <span data-ttu-id="35d42-139">Otwórz ustawienia modułów projektu za pomocą menu kontekstowego lub przy użyciu skrótu Ctrl + Alt + główn + S.</span><span class="sxs-lookup"><span data-stu-id="35d42-139">Open the project modules settings by using the context menu or by using the Ctrl+Alt+Maj+S shortcut.</span></span>
   
    ![Ustawienia modułów projektu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample4.PNG)
4. <span data-ttu-id="35d42-141">Usunąć domyślnego modułu aplikacji, ponieważ mają tylko ustawienia kontenera projektu.</span><span class="sxs-lookup"><span data-stu-id="35d42-141">Remove the default app module because you only want the project container settings.</span></span>
   
    ![Domyślny moduł aplikacji](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample5.PNG)
5. <span data-ttu-id="35d42-143">Zaimportuj moduły z sklonowanego repozytorium dla bieżącego projektu.</span><span class="sxs-lookup"><span data-stu-id="35d42-143">Import modules from the cloned repo to the current project.</span></span>
   
    <span data-ttu-id="35d42-144">![Importowanie projektu gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Utwórz nową stronę modułu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span><span class="sxs-lookup"><span data-stu-id="35d42-144">![Import gradle project](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample6.PNG) ![Create new module page](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample7.PNG)</span></span>
6. <span data-ttu-id="35d42-145">Powtórz te kroki dla `oidlib-sample` modułu.</span><span class="sxs-lookup"><span data-stu-id="35d42-145">Repeat these steps for the `oidlib-sample` module.</span></span>
7. <span data-ttu-id="35d42-146">Sprawdź zależności oidclib na `oidlib-sample` modułu.</span><span class="sxs-lookup"><span data-stu-id="35d42-146">Check the oidclib dependencies on the `oidlib-sample` module.</span></span>
   
    ![zależności oidclib w module oidlib próbki](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8.PNG)
8. <span data-ttu-id="35d42-148">Kliknij przycisk **OK** i poczekaj, aż synchronizacja narzędzia gradle.</span><span class="sxs-lookup"><span data-stu-id="35d42-148">Click **OK** and wait for gradle sync.</span></span>
   
    <span data-ttu-id="35d42-149">Twoje settings.gradle powinna wyglądać:</span><span class="sxs-lookup"><span data-stu-id="35d42-149">Your settings.gradle should look like:</span></span>
   
    ![Zrzut ekranu przedstawiający settings.gradle](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample8_1.PNG)
9. <span data-ttu-id="35d42-151">Tworzenie przykładowej aplikacji, aby upewnić się, że Przykładowe prawidłowe działanie.</span><span class="sxs-lookup"><span data-stu-id="35d42-151">Build the sample app to make sure that the sample running correctly.</span></span>
   
    <span data-ttu-id="35d42-152">Nie można użyć tego jeszcze z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="35d42-152">You won't be able to use this with Azure Active Directory yet.</span></span> <span data-ttu-id="35d42-153">Potrzebujemy najpierw skonfigurować niektóre punkty końcowe.</span><span class="sxs-lookup"><span data-stu-id="35d42-153">We'll need to configure some endpoints first.</span></span> <span data-ttu-id="35d42-154">To upewnij się, że masz problemy z systemem Android Studio przed Rozpoczniemy Dostosowywanie przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35d42-154">This is to ensure you don't have an Android Studio issues before we start customizing the sample app.</span></span>
10. <span data-ttu-id="35d42-155">Tworzenie i uruchamianie `oidlib-sample` jako cel w programie Android Studio.</span><span class="sxs-lookup"><span data-stu-id="35d42-155">Build and run `oidlib-sample` as the target in Android Studio.</span></span>
    
    ![Postęp kompilacji oidlib próbki](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample9.png)
11. <span data-ttu-id="35d42-157">Usuń `app ` katalogu, w którym pozostawało po usunięciu modułu z projektu, ponieważ Android Studio nie powoduje usunięcia go dla bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="35d42-157">Delete the `app ` directory that was left when you removed the module from the project because Android Studio doesn't delete it for safety.</span></span>
    
    ![Struktura pliku, który zawiera katalog aplikacji](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample12.PNG)
12. <span data-ttu-id="35d42-159">Otwórz **Edytuj konfiguracje** menu do usunięcia konfiguracji procesu, który pozostawało również usunięcie modułu z projektu.</span><span class="sxs-lookup"><span data-stu-id="35d42-159">Open the **Edit Configurations** menu to remove the run configuration that was also left when you removed the module from the project.</span></span>
    
    <span data-ttu-id="35d42-160">![Edytuj konfiguracje menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
    ![Uruchom konfiguracji aplikacji](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span><span class="sxs-lookup"><span data-stu-id="35d42-160">![Edit configurations menu](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample10.PNG)
![Run configuration of app](../media/active-directory-android-native-oidcandroidlib-v2/SetUpSample11.PNG)</span></span>

## <a name="configure-the-endpoints-of-the-sample"></a><span data-ttu-id="35d42-161">Skonfiguruj punkty końcowe próbki</span><span class="sxs-lookup"><span data-stu-id="35d42-161">Configure the endpoints of the sample</span></span>
<span data-ttu-id="35d42-162">Teraz, gdy masz `oidlib-sample` uruchomiony pomyślnie, umożliwia edytowanie niektórych punktów końcowych, aby działało z usługą Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="35d42-162">Now that you have the `oidlib-sample` running successfully, let's edit some endpoints to get this working with Azure Active Directory.</span></span>

### <a name="configure-your-client-by-editing-the-oidcclientconfxml-file"></a><span data-ttu-id="35d42-163">Konfigurowanie klienta, edytując plik oidc_clientconf.xml</span><span class="sxs-lookup"><span data-stu-id="35d42-163">Configure your client by editing the oidc_clientconf.xml file</span></span>
1. <span data-ttu-id="35d42-164">Ponieważ używasz przepływów OAuth2 tylko do pobrania tokenu i wywołania interfejsu API programu Graph, Ustaw klienta OAuth2 tylko.</span><span class="sxs-lookup"><span data-stu-id="35d42-164">Because you are using OAuth2 flows only to get a token and call the Graph API, set the client to do OAuth2 only.</span></span> <span data-ttu-id="35d42-165">OIDC wejdzie w przykładzie nowsze.</span><span class="sxs-lookup"><span data-stu-id="35d42-165">OIDC will come in a later example.</span></span>
   
    ```xml
        <bool name="oidc_oauth2only">true</bool>
    ```
2. <span data-ttu-id="35d42-166">Konfigurowanie Identyfikatora klienta, otrzymany z portalu rejestracji.</span><span class="sxs-lookup"><span data-stu-id="35d42-166">Configure your client ID that you received from the registration portal.</span></span>
   
    ```xml
        <string name="oidc_clientId">86172f9d-a1ae-4348-aafa-7b3e5d1b36f5</string>
        <string name="oidc_clientSecret"></string>
    ```
3. <span data-ttu-id="35d42-167">Skonfiguruj identyfikator URI przekierowania, poniżej.</span><span class="sxs-lookup"><span data-stu-id="35d42-167">Configure your redirect URI with the one below.</span></span>
   
    ```xml
        <string name="oidc_redirectUrl">https://login.microsoftonline.com/common/oauth2/nativeclient</string>
    ```
4. <span data-ttu-id="35d42-168">Skonfiguruj zakresach potrzebne w celu uzyskania dostępu do interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="35d42-168">Configure your scopes that you need in order to access the Graph API.</span></span>
   
    ```xml
        <string-array name="oidc_scopes">
            <item>openid</item>
            <item>https://graph.microsoft.com/User.Read</item>
            <item>offline_access</item>
        </string-array>
    ```

<span data-ttu-id="35d42-169">`User.Read` Wartość w `oidc_scopes` umożliwia odczytanie profilu podstawowego podpisanej w użytkownika.</span><span class="sxs-lookup"><span data-stu-id="35d42-169">The `User.Read` value in `oidc_scopes` allows you to read the basic profile the signed in user.</span></span>
<span data-ttu-id="35d42-170">Dowiedz się więcej o wszystkie dostępne zakresy na [zakresy uprawnień Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="35d42-170">You can learn more about all the available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="35d42-171">Jeśli chcesz wyjaśnień dotyczących `openid` lub `offline_access` jako zakresów w OpenID Connect, zobacz [2.0 protokołów - przepływu kodu autoryzacji OAuth 2.0](active-directory-v2-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="35d42-171">If you'd like explanations about `openid` or `offline_access` as scopes in OpenID Connect, see [2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md).</span></span>

### <a name="configure-your-client-endpoints-by-editing-the-oidcendpointsxml-file"></a><span data-ttu-id="35d42-172">Skonfiguruj punkty końcowe klienta, edytując plik oidc_endpoints.xml</span><span class="sxs-lookup"><span data-stu-id="35d42-172">Configure your client endpoints by editing the oidc_endpoints.xml file</span></span>
* <span data-ttu-id="35d42-173">Otwórz `oidc_endpoints.xml` plik, a następnie dokonaj następujących zmian:</span><span class="sxs-lookup"><span data-stu-id="35d42-173">Open the `oidc_endpoints.xml` file and make the following changes:</span></span>
  
    ```xml
    <!-- Stores OpenID Connect provider endpoints. -->
    <resources>
        <string name="op_authorizationEnpoint">https://login.microsoftonline.com/common/oauth2/v2.0/authorize</string>
        <string name="op_tokenEndpoint">https://login.microsoftonline.com/common/oauth2/v2.0/token</string>
        <string name="op_userInfoEndpoint">https://www.example.com/oauth2/userinfo</string>
        <string name="op_revocationEndpoint">https://www.example.com/oauth2/revoketoken</string>
    </resources>
    ```

<span data-ttu-id="35d42-174">Tymi punktami końcowymi nigdy nie należy zmieniać, jeśli używasz protokołu OAuth2 jako protokołów.</span><span class="sxs-lookup"><span data-stu-id="35d42-174">These endpoints should never change if you are using OAuth2 as your protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="35d42-175">Punkty końcowe dla `userInfoEndpoint` i `revocationEndpoint` nie są obecnie obsługiwane przez usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="35d42-175">The endpoints for `userInfoEndpoint` and `revocationEndpoint` are currently not supported by Azure Active Directory.</span></span> <span data-ttu-id="35d42-176">Pozostawienie tych z wartością domyślną example.com przypomnienie pojawi się czy nie są one dostępne w próbce :-)</span><span class="sxs-lookup"><span data-stu-id="35d42-176">If you leave these with the default example.com value, you will be reminded that they are not available in the sample :-)</span></span>
> 
> 

## <a name="configure-a-graph-api-call"></a><span data-ttu-id="35d42-177">Konfigurowanie wywołania interfejsu API programu Graph</span><span class="sxs-lookup"><span data-stu-id="35d42-177">Configure a Graph API call</span></span>
* <span data-ttu-id="35d42-178">Otwórz `HomeActivity.java` plik, a następnie dokonaj następujących zmian:</span><span class="sxs-lookup"><span data-stu-id="35d42-178">Open the `HomeActivity.java` file and make the following changes:</span></span>
  
    ```Java
       //TODO: set your protected resource url
        private static final String protectedResUrl = "https://graph.microsoft.com/v1.0/me/";
    ```

<span data-ttu-id="35d42-179">W tym miejscu proste wywołania interfejsu API programu Graph zwraca naszych informacje.</span><span class="sxs-lookup"><span data-stu-id="35d42-179">Here a simple Graph API call returns our information.</span></span>

<span data-ttu-id="35d42-180">Są to wszystkie zmiany, które należy wykonać.</span><span class="sxs-lookup"><span data-stu-id="35d42-180">Those are all the changes that you need to do.</span></span> <span data-ttu-id="35d42-181">Uruchom `oidlib-sample` aplikacji, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="35d42-181">Run the `oidlib-sample` application, and click **Sign in**.</span></span>

<span data-ttu-id="35d42-182">Po pomyślnie uwierzytelniono, wybierz **żądania zasobów chronionych** przycisk, aby przetestować wywołania do interfejsu API programu Graph.</span><span class="sxs-lookup"><span data-stu-id="35d42-182">After you've successfully authenticated, select the **Request Protected Resource** button to test your call to the Graph API.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="35d42-183">Pobierz aktualizacje zabezpieczeń naszych produktów</span><span class="sxs-lookup"><span data-stu-id="35d42-183">Get security updates for our product</span></span>
<span data-ttu-id="35d42-184">Firma Microsoft zachęca do otrzymywać powiadomień o przypadki naruszenia zabezpieczeń poprzez wizytę [Witryna TechCenter poświęcona zabezpieczeniom](https://technet.microsoft.com/security/dd252948) i subskrybowanie doradczych alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="35d42-184">We encourage you to get notifications about security incidents by visiting the [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

