---
title: "Uzyskiwanie tokenu przy użyciu aplikacji systemu iOS — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate aplikację systemu iOS, która korzysta z tożsamości użytkowników usługi Azure Active Directory B2C toomanage AppAuth i uwierzytelnianie użytkowników."
services: active-directory-b2c
documentationcenter: ios
author: saeedakhter-msft
manager: krassk
editor: parakhj
ms.assetid: d818a634-42c2-4cbd-bf73-32fa0c8c69d3
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objectivec
ms.topic: article
ms.date: 03/07/2017
ms.author: saeedakhter-msft
ms.openlocfilehash: e7cbe2de6e9ae3d45448cdd36292c457a0ef4887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="ea6cf-103">Usługa Azure AD B2C: Zaloguj się przy użyciu aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="ea6cf-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="ea6cf-104">korzysta z platformą tożsamości Microsoft Hello Otwórz standardy, takie jak OAuth2 i OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="ea6cf-105">Przy użyciu standardowego protokołu zapewniającego Otwórz oferuje większy wybór developer, wybierając toointegrate biblioteki z naszych usług.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-105">Using an open standard protocol offers more developer choice when selecting a library toointegrate with our services.</span></span> <span data-ttu-id="ea6cf-106">Przygotowaliśmy tego przewodnika oraz innym osobom podoba Ci się tooaid deweloperom pisanie aplikacje łączące toohello platformy pakietu Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-106">We've provided this walkthrough and others like it tooaid developers with writing applications that connect toohello Microsoft Identity platform.</span></span> <span data-ttu-id="ea6cf-107">Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2 hello](https://tools.ietf.org/html/rfc6749) są możliwe tooconnect toohello pakietu Microsoft Identity platformy.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="ea6cf-108">Firma Microsoft zapewnia poprawki dla bibliotek innych firm, a nie przeprowadził Przegląd tych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="ea6cf-109">Ten przykład jest przy użyciu biblioteki innej firmy o nazwie AppAuth, które zostały przetestowane zgodność w podstawowe scenariusze z hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="ea6cf-110">Problemy i żądania funkcji powinny być projekt open source ukierunkowanej toohello biblioteki.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="ea6cf-111">Więcej informacji znajduje się w [tym artykule](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="ea6cf-112">Jeśli nowy tooOAuth2 lub OpenID Connect znacznie to przykładowa konfiguracja może nie mieć znacznie tooyou znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-112">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="ea6cf-113">Firma Microsoft zaleca, Obejrzyj krótkie [Omówienie protokołu hello mamy już opisanych tutaj](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="ea6cf-114">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ea6cf-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="ea6cf-115">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="ea6cf-116">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i inne.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="ea6cf-117">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="ea6cf-118">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="ea6cf-118">Create an application</span></span>
<span data-ttu-id="ea6cf-119">Następnie należy toocreate aplikację w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="ea6cf-120">rejestracji aplikacji Hello zawiera informacje usługi Azure AD, że wymaga ona toocommunicate bezpiecznie z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-120">hello app registration gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="ea6cf-121">toocreate aplikacji mobilnej, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="ea6cf-122">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="ea6cf-122">Be sure to:</span></span>

* <span data-ttu-id="ea6cf-123">Obejmują **Native client** w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-123">Include a **Native client** in hello application.</span></span>
* <span data-ttu-id="ea6cf-124">Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="ea6cf-125">Ten identyfikator GUID jest potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-125">You need this GUID later.</span></span>
* <span data-ttu-id="ea6cf-126">Konfigurowanie **identyfikator URI przekierowania** z schematu niestandardowego (na przykład com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="ea6cf-127">Ten identyfikator URI potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="ea6cf-128">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="ea6cf-128">Create your policies</span></span>
<span data-ttu-id="ea6cf-129">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="ea6cf-130">Ta aplikacja zawiera jeden obsługi tożsamości: połączone logowania i rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="ea6cf-131">Utwórz te zasady, zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="ea6cf-132">Po utworzeniu hello zasad należy koniecznie:</span><span class="sxs-lookup"><span data-stu-id="ea6cf-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="ea6cf-133">W obszarze **atrybuty rejestracji**, wybierz atrybut hello **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-133">Under **Sign-up attributes**, select hello attribute **Display name**.</span></span>  <span data-ttu-id="ea6cf-134">Możesz wybrać także inne atrybuty.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="ea6cf-135">W obszarze **oświadczenia aplikacji**, wybierz oświadczeń hello **Nazwa wyświetlana** i **Identyfikatora obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-135">Under **Application claims**, select hello claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="ea6cf-136">Możesz wybrać także inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-136">You can select other claims as well.</span></span>
* <span data-ttu-id="ea6cf-137">Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-137">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="ea6cf-138">Nazwę zasad jest prefiksem `b2c_1_` podczas zapisywania hello zasad.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-138">Your policy name is prefixed with `b2c_1_` when you save hello policy.</span></span>  <span data-ttu-id="ea6cf-139">Nazwa zasad hello potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-139">You need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="ea6cf-140">Po utworzeniu zasad, wszystko jest gotowe toobuild aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-140">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="ea6cf-141">Pobierz hello przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="ea6cf-141">Download hello sample code</span></span>
<span data-ttu-id="ea6cf-142">Firma Microsoft umieściła próbki pracy, który korzysta z usługi Azure AD B2C AppAuth [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="ea6cf-143">Można pobrać kodu hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-143">You can download hello code and run it.</span></span> <span data-ttu-id="ea6cf-144">toouse dzierżawy własne usługi Azure AD B2C, wykonaj te instrukcje hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-144">toouse your own Azure AD B2C tenant, follow hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="ea6cf-145">W tym przykładzie został utworzony przez instrukcjami README hello przez hello [iOS AppAuth projektu w witrynie GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-145">This sample was created by following hello README instructions by hello [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="ea6cf-146">Aby uzyskać więcej informacji na temat działania przykładowe hello i biblioteki hello odwołanie hello README AppAuth w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-146">For more details on how hello sample and hello library work, reference hello AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="ea6cf-147">Modyfikowanie toouse Twojej aplikacji usługi Azure AD B2C z AppAuth</span><span class="sxs-lookup"><span data-stu-id="ea6cf-147">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="ea6cf-148">AppAuth obsługuje system iOS 7 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="ea6cf-149">Jednak toosupport logowania społecznościowych Google, SFSafariViewController jest potrzebna, które wymaga systemu iOS 9 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-149">However, toosupport social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="ea6cf-150">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="ea6cf-150">Configuration</span></span>

<span data-ttu-id="ea6cf-151">Komunikację można skonfigurować z usługi Azure AD B2C, określając zarówno punktu końcowego autoryzacji hello, jak i punktu końcowego tokena identyfikatorów URI.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-151">You can configure communication with Azure AD B2C by specifying both hello authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="ea6cf-152">toogenerate tych identyfikatorów należy hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ea6cf-152">toogenerate these URIs, you need hello following information:</span></span>
* <span data-ttu-id="ea6cf-153">Identyfikator dzierżawcy (np. contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="ea6cf-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="ea6cf-154">Nazwa zasady (na przykład B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="ea6cf-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="ea6cf-155">Witaj punktu końcowego tokena identyfikatora URI może zostać wygenerowany przez zastąpienie hello dzierżawy\_identyfikator i hello zasad\_nazwy w hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="ea6cf-155">hello token endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="ea6cf-156">Witaj zastępując można wygenerować identyfikatora URI punktu końcowego autoryzacji hello dzierżawy\_identyfikator i hello zasad\_nazwy w hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="ea6cf-156">hello authorization endpoint URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="ea6cf-157">Uruchom hello poniższy kod toocreate obiektu AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="ea6cf-157">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready tooperform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="ea6cf-158">Autoryzowanie</span><span class="sxs-lookup"><span data-stu-id="ea6cf-158">Authorizing</span></span>

<span data-ttu-id="ea6cf-159">Po Konfigurowanie lub pobieranie konfiguracji usługi autoryzacji, można utworzyć żądania autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="ea6cf-160">Witaj toocreate żądania, należy hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ea6cf-160">toocreate hello request, you need hello following information:</span></span>  
* <span data-ttu-id="ea6cf-161">Identyfikator klienta (na przykład 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="ea6cf-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="ea6cf-162">Identyfikator URI przekierowania z schematu niestandardowego (na przykład com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="ea6cf-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="ea6cf-163">Oba elementy powinny zostały zapisane, gdy użytkownik [rejestrowanie aplikacji](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```objc
OIDAuthorizationRequest *request = 
    [[OIDAuthorizationRequest alloc] initWithConfiguration:configuration
                                                  clientId:kClientId
                                                    scopes:@[OIDScopeOpenID, OIDScopeProfile]
                                               redirectURL:[NSURL URLWithString:kRedirectUri]
                                              responseType:OIDResponseTypeCode
                                      additionalParameters:nil];

AppDelegate *appDelegate = (AppDelegate *)[UIApplication sharedApplication].delegate;
appDelegate.currentAuthorizationFlow = 
    [OIDAuthState authStateByPresentingAuthorizationRequest:request
                                   presentingViewController:self
                                                   callback:^(OIDAuthState *_Nullable authState, NSError *_Nullable error) {
        if (authState) {
            NSLog(@"Got authorization tokens. Access token: %@", authState.lastTokenResponse.accessToken);
            [self setAuthState:authState];
        } else {
            NSLog(@"Authorization error: %@", [error localizedDescription]);
            [self setAuthState:nil];
        }
    }];
```

<span data-ttu-id="ea6cf-164">tooset się Twojej aplikacji toohandle hello przekierowania toohello URI ze schematem niestandardowych hello, tooupdate hello listy programów"URL" potrzebne w Twojej Info.pList:</span><span class="sxs-lookup"><span data-stu-id="ea6cf-164">tooset up your application toohandle hello redirect toohello URI with hello custom scheme, you need tooupdate hello list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="ea6cf-165">Otwórz Info.pList.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-165">Open Info.pList.</span></span>
* <span data-ttu-id="ea6cf-166">Umieść kursor nad wiersza, takie jak "Kod typu systemu operacyjnego pakietu", a następnie kliknij przycisk hello \+ symbolu.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-166">Hover over a row like 'Bundle OS Type Code' and click hello \+ symbol.</span></span>
* <span data-ttu-id="ea6cf-167">Zmień nazwę hello nowego wiersza "adres URL typy".</span><span class="sxs-lookup"><span data-stu-id="ea6cf-167">Rename hello new row 'URL types'.</span></span>
* <span data-ttu-id="ea6cf-168">Kliknij przycisk toohello Strzałka hello "Adres URL typy" tooopen hello drzewa w lewo.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-168">Click hello arrow toohello left of 'URL types' tooopen hello tree.</span></span>
* <span data-ttu-id="ea6cf-169">Kliknij przycisk hello Strzałka toohello lewej "Elementu 0" tooopen hello drzewa.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-169">Click hello arrow toohello left of 'Item 0' tooopen hello tree.</span></span>
* <span data-ttu-id="ea6cf-170">Zmień nazwę pierwszego elementu poniżej schematy 0 too'URL elementów.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-170">Rename first item underneath Item 0 too'URL Schemes'.</span></span>
* <span data-ttu-id="ea6cf-171">Kliknij przycisk toohello Strzałka hello "Schematy adresów URL" tooopen hello drzewa w lewo.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-171">Click hello arrow toohello left of 'URL Schemes' tooopen hello tree.</span></span>
* <span data-ttu-id="ea6cf-172">W kolumnie "Wartość" hello, jest puste pole toohello po lewej "Elementu 0" poniżej "Schematy adresów URL".</span><span class="sxs-lookup"><span data-stu-id="ea6cf-172">In hello 'Value' column, there is a blank field toohello left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="ea6cf-173">Ustawienie aplikacji hello wartość tooyour unikatowy schematu.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-173">Set hello value tooyour application's unique scheme.</span></span>  <span data-ttu-id="ea6cf-174">wartość Hello musi odpowiadać używany w redirectURL, podczas tworzenia obiektu OIDAuthorizationRequest hello schemat hello.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-174">hello value must match hello scheme used in redirectURL when creating hello OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="ea6cf-175">W naszym przykładzie użyliśmy hello schemat "com.onmicrosoft.fabrikamb2c.exampleapp".</span><span class="sxs-lookup"><span data-stu-id="ea6cf-175">In our sample, we used hello scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="ea6cf-176">Zobacz toohello [przewodnik AppAuth](https://openid.github.io/AppAuth-iOS/) w sposób toocomplete hello resztę procesu hello.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-176">Refer toohello [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="ea6cf-177">Jeśli potrzebujesz tooquickly rozpocząć pracę z aplikacją pracy, zapoznaj się z [naszej próbki](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-177">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="ea6cf-178">Wykonaj kroki hello hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter konfigurację usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-178">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="ea6cf-179">Jesteśmy zawsze toofeedback otwarte i sugestie!</span><span class="sxs-lookup"><span data-stu-id="ea6cf-179">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="ea6cf-180">Jeśli masz trudności w tym temacie lub mają zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ea6cf-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="ea6cf-181">Funkcja żądań, dodaj ich zbyt[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="ea6cf-181">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
