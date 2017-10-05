---
title: "Uzyskiwanie tokenu przy użyciu aplikacji systemu iOS — usługi Azure AD B2C | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tworzenia aplikacji systemu iOS, która używa AppAuth z usługi Azure Active Directory B2C do zarządzania tożsamościami użytkowników i uwierzytelniania użytkowników."
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
ms.openlocfilehash: ebec5d910b8987dcc8155cd4ead00f87d219941c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-ios-application"></a><span data-ttu-id="324d0-103">Usługa Azure AD B2C: Zaloguj się przy użyciu aplikacji systemu iOS</span><span class="sxs-lookup"><span data-stu-id="324d0-103">Azure AD B2C: Sign-in using an iOS application</span></span>

<span data-ttu-id="324d0-104">Platforma Microsoft Identity korzysta z otwartych standardów, takich jak OAuth2 i OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="324d0-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="324d0-105">Przy użyciu standardowego protokołu zapewniającego Otwórz oferuje większy wybór developer, wybierając biblioteki do integracji z naszych usług.</span><span class="sxs-lookup"><span data-stu-id="324d0-105">Using an open standard protocol offers more developer choice when selecting a library to integrate with our services.</span></span> <span data-ttu-id="324d0-106">Podobnie jak jego pomóc deweloperom pisanie aplikacji łączących się z platformą Microsoft Identity przygotowaliśmy tego przewodnika oraz innym osobom.</span><span class="sxs-lookup"><span data-stu-id="324d0-106">We've provided this walkthrough and others like it to aid developers with writing applications that connect to the Microsoft Identity platform.</span></span> <span data-ttu-id="324d0-107">Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) są w stanie nawiązać połączenia z platformą Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="324d0-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) are able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="324d0-108">Firma Microsoft zapewnia poprawki dla bibliotek innych firm, a nie przeprowadził Przegląd tych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="324d0-108">Microsoft does not provide fixes for third-party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="324d0-109">Ten przykład jest przy użyciu biblioteki innej firmy o nazwie AppAuth, które zostały przetestowane na zgodność w podstawowe scenariusze w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="324d0-109">This sample is using a third-party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="324d0-110">Problemy i żądania funkcji powinny być kierowane do biblioteki projektu open source.</span><span class="sxs-lookup"><span data-stu-id="324d0-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="324d0-111">Więcej informacji znajduje się w [tym artykule](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span><span class="sxs-lookup"><span data-stu-id="324d0-111">For more information, see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries).</span></span>
>
>

<span data-ttu-id="324d0-112">Jeśli jesteś nowym użytkownikiem OAuth2 lub OpenID Connect, znacznie to przykładowa konfiguracja może nie mieć sensu dużo do Ciebie.</span><span class="sxs-lookup"><span data-stu-id="324d0-112">If you're new to OAuth2 or OpenID Connect, much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="324d0-113">Zalecamy zapoznanie się z [krótkim omówieniem protokołu w tej dokumentacji](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="324d0-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="324d0-114">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="324d0-114">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="324d0-115">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="324d0-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="324d0-116">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i inne.</span><span class="sxs-lookup"><span data-stu-id="324d0-116">A directory is a container for all your users, apps, groups, and more.</span></span> <span data-ttu-id="324d0-117">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="324d0-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="324d0-118">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="324d0-118">Create an application</span></span>
<span data-ttu-id="324d0-119">Następnie musisz utworzyć aplikację w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="324d0-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="324d0-120">Rejestracja aplikacji zapewnia informacje wymagane do bezpiecznego komunikowania się z aplikacją usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="324d0-120">The app registration gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="324d0-121">Aby utworzyć aplikacji mobilnej, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="324d0-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="324d0-122">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="324d0-122">Be sure to:</span></span>

* <span data-ttu-id="324d0-123">Obejmują **Native client** w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="324d0-123">Include a **Native client** in the application.</span></span>
* <span data-ttu-id="324d0-124">Skopiuj **Identyfikator aplikacji** przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="324d0-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="324d0-125">Ten identyfikator GUID jest potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="324d0-125">You need this GUID later.</span></span>
* <span data-ttu-id="324d0-126">Konfigurowanie **identyfikator URI przekierowania** z schematu niestandardowego (na przykład com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="324d0-126">Set up a **Redirect URI** with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="324d0-127">Ten identyfikator URI potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="324d0-127">You need this URI later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="324d0-128">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="324d0-128">Create your policies</span></span>
<span data-ttu-id="324d0-129">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="324d0-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="324d0-130">Ta aplikacja zawiera jeden obsługi tożsamości: połączone logowania i rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="324d0-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="324d0-131">Utwórz te zasady, zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="324d0-131">Create this policy as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="324d0-132">Podczas tworzenia zasad należy:</span><span class="sxs-lookup"><span data-stu-id="324d0-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="324d0-133">W obszarze **atrybuty rejestracji**, wybierz atrybut **Nazwa wyświetlana**.</span><span class="sxs-lookup"><span data-stu-id="324d0-133">Under **Sign-up attributes**, select the attribute **Display name**.</span></span>  <span data-ttu-id="324d0-134">Możesz wybrać także inne atrybuty.</span><span class="sxs-lookup"><span data-stu-id="324d0-134">You can select other attributes as well.</span></span>
* <span data-ttu-id="324d0-135">W obszarze **oświadczenia aplikacji**, wybierz oświadczenia **Nazwa wyświetlana** i **Identyfikatora obiektu użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="324d0-135">Under **Application claims**, select the claims **Display name** and **User's Object ID**.</span></span> <span data-ttu-id="324d0-136">Możesz wybrać także inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="324d0-136">You can select other claims as well.</span></span>
* <span data-ttu-id="324d0-137">Skopiować każdą utworzoną wartość **Nazwa** zasad.</span><span class="sxs-lookup"><span data-stu-id="324d0-137">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="324d0-138">Nazwę zasad jest prefiksem `b2c_1_` podczas zapisywania zasad.</span><span class="sxs-lookup"><span data-stu-id="324d0-138">Your policy name is prefixed with `b2c_1_` when you save the policy.</span></span>  <span data-ttu-id="324d0-139">Nazwa zasady jest potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="324d0-139">You need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="324d0-140">Po utworzeniu zasad będzie można rozpocząć tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="324d0-140">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="324d0-141">Pobierz przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="324d0-141">Download the sample code</span></span>
<span data-ttu-id="324d0-142">Firma Microsoft umieściła próbki pracy, który korzysta z usługi Azure AD B2C AppAuth [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="324d0-142">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="324d0-143">Można go pobrać i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="324d0-143">You can download the code and run it.</span></span> <span data-ttu-id="324d0-144">Aby używać dzierżawy usługi Azure AD B2C, postępuj zgodnie z instrukcjami [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="324d0-144">To use your own Azure AD B2C tenant, follow the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="324d0-145">W tym przykładzie został utworzony zgodnie z instrukcjami README przez [iOS AppAuth projektu w witrynie GitHub](https://github.com/openid/AppAuth-iOS).</span><span class="sxs-lookup"><span data-stu-id="324d0-145">This sample was created by following the README instructions by the [iOS AppAuth project on GitHub](https://github.com/openid/AppAuth-iOS).</span></span> <span data-ttu-id="324d0-146">Aby uzyskać więcej informacji na temat działania próbki i bibliotece odwoływać README AppAuth w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="324d0-146">For more details on how the sample and the library work, reference the AppAuth README on GitHub.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="324d0-147">Modyfikowanie aplikacji do użycia usługi Azure AD B2C z AppAuth</span><span class="sxs-lookup"><span data-stu-id="324d0-147">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="324d0-148">AppAuth obsługuje system iOS 7 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="324d0-148">AppAuth supports iOS 7 and above.</span></span>  <span data-ttu-id="324d0-149">Jednak do obsługi logowania społecznościowych Google, SFSafariViewController jest potrzebny co wymaga systemu iOS 9 lub nowszą.</span><span class="sxs-lookup"><span data-stu-id="324d0-149">However, to support social logins on Google, SFSafariViewController is needed which requires iOS 9 or higher.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="324d0-150">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="324d0-150">Configuration</span></span>

<span data-ttu-id="324d0-151">Komunikację można skonfigurować z usługi Azure AD B2C, określając punktu końcowego autoryzacji i punktu końcowego tokena identyfikatorów URI.</span><span class="sxs-lookup"><span data-stu-id="324d0-151">You can configure communication with Azure AD B2C by specifying both the authorization endpoint and token endpoint URIs.</span></span>  <span data-ttu-id="324d0-152">Aby wygenerować te identyfikatory URI, potrzebne są następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="324d0-152">To generate these URIs, you need the following information:</span></span>
* <span data-ttu-id="324d0-153">Identyfikator dzierżawcy (np. contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="324d0-153">Tenant ID (for example, contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="324d0-154">Nazwa zasady (na przykład B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="324d0-154">Policy name (for example, B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="324d0-155">Zastępując dzierżawcy można wygenerować identyfikatora URI punktu końcowego tokena\_identyfikator i zasady\_nazwy w następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="324d0-155">The token endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const tokenEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/token";
```

<span data-ttu-id="324d0-156">Zastępując dzierżawcy można wygenerować identyfikatora URI punktu końcowego autoryzacji\_identyfikator i zasady\_nazwy w następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="324d0-156">The authorization endpoint URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```objc
static NSString *const authorizationEndpoint = @"https://login.microsoftonline.com/te/<Tenant_ID>/<Policy_Name>/oauth2/v2.0/authorize";
```

<span data-ttu-id="324d0-157">Uruchom następujący kod, aby utworzyć obiekt AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="324d0-157">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```objc
OIDServiceConfiguration *configuration = 
    [[OIDServiceConfiguration alloc] initWithAuthorizationEndpoint:authorizationEndpoint tokenEndpoint:tokenEndpoint];
// now we are ready to perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="324d0-158">Autoryzowanie</span><span class="sxs-lookup"><span data-stu-id="324d0-158">Authorizing</span></span>

<span data-ttu-id="324d0-159">Po Konfigurowanie lub pobieranie konfiguracji usługi autoryzacji, można utworzyć żądania autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="324d0-159">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="324d0-160">Aby utworzyć żądanie, potrzebne są następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="324d0-160">To create the request, you need the following information:</span></span>  
* <span data-ttu-id="324d0-161">Identyfikator klienta (na przykład 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="324d0-161">Client ID (for example, 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="324d0-162">Identyfikator URI przekierowania z schematu niestandardowego (na przykład com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span><span class="sxs-lookup"><span data-stu-id="324d0-162">Redirect URI with a custom scheme (for example, com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect)</span></span>

<span data-ttu-id="324d0-163">Oba elementy powinny zostały zapisane, gdy użytkownik [rejestrowanie aplikacji](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="324d0-163">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

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

<span data-ttu-id="324d0-164">Aby skonfigurować aplikację do obsługi przekierowania do identyfikatora URI ze schematem niestandardowe, należy zaktualizować listę "Schematy adresów URL" w Twojej Info.pList:</span><span class="sxs-lookup"><span data-stu-id="324d0-164">To set up your application to handle the redirect to the URI with the custom scheme, you need to update the list of 'URL Schemes' in your Info.pList:</span></span>
* <span data-ttu-id="324d0-165">Otwórz Info.pList.</span><span class="sxs-lookup"><span data-stu-id="324d0-165">Open Info.pList.</span></span>
* <span data-ttu-id="324d0-166">Umieść kursor nad wiersza, takie jak "Kod typu systemu operacyjnego pakietu", a następnie kliknij przycisk \+ symbolu.</span><span class="sxs-lookup"><span data-stu-id="324d0-166">Hover over a row like 'Bundle OS Type Code' and click the \+ symbol.</span></span>
* <span data-ttu-id="324d0-167">Zmień nazwę nowego wiersza "Adres URL typy".</span><span class="sxs-lookup"><span data-stu-id="324d0-167">Rename the new row 'URL types'.</span></span>
* <span data-ttu-id="324d0-168">Kliknij strzałkę w lewo "Adres URL typy" Aby otworzyć drzewa.</span><span class="sxs-lookup"><span data-stu-id="324d0-168">Click the arrow to the left of 'URL types' to open the tree.</span></span>
* <span data-ttu-id="324d0-169">Kliknij strzałkę po lewej "elementu 0", aby otworzyć drzewa.</span><span class="sxs-lookup"><span data-stu-id="324d0-169">Click the arrow to the left of 'Item 0' to open the tree.</span></span>
* <span data-ttu-id="324d0-170">Zmień nazwę pierwszego elementu poniżej elementu 0 "Schematy adresów URL".</span><span class="sxs-lookup"><span data-stu-id="324d0-170">Rename first item underneath Item 0 to 'URL Schemes'.</span></span>
* <span data-ttu-id="324d0-171">Kliknij strzałkę w lewo "Schematy adresów URL", aby otworzyć drzewa.</span><span class="sxs-lookup"><span data-stu-id="324d0-171">Click the arrow to the left of 'URL Schemes' to open the tree.</span></span>
* <span data-ttu-id="324d0-172">W kolumnie 'Value' jest puste pole na lewo od elementu 0 poniżej "Schematy adresów URL".</span><span class="sxs-lookup"><span data-stu-id="324d0-172">In the 'Value' column, there is a blank field to the left of 'Item 0' underneath 'URL Schemes'.</span></span>  <span data-ttu-id="324d0-173">Wartość schemat unikatowy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="324d0-173">Set the value to your application's unique scheme.</span></span>  <span data-ttu-id="324d0-174">Wartość musi być zgodna używany w redirectURL podczas tworzenia obiektu OIDAuthorizationRequest schemat.</span><span class="sxs-lookup"><span data-stu-id="324d0-174">The value must match the scheme used in redirectURL when creating the OIDAuthorizationRequest object.</span></span>  <span data-ttu-id="324d0-175">W naszym przykładzie użyliśmy schemat "com.onmicrosoft.fabrikamb2c.exampleapp".</span><span class="sxs-lookup"><span data-stu-id="324d0-175">In our sample, we used the scheme 'com.onmicrosoft.fabrikamb2c.exampleapp'.</span></span>

<span data-ttu-id="324d0-176">Zapoznaj się [przewodnik AppAuth](https://openid.github.io/AppAuth-iOS/) na temat sposobu ukończenia resztę procesu.</span><span class="sxs-lookup"><span data-stu-id="324d0-176">Refer to the [AppAuth guide](https://openid.github.io/AppAuth-iOS/) on how to complete the rest of the process.</span></span> <span data-ttu-id="324d0-177">Jeśli potrzebujesz szybko rozpocząć pracę z aplikacją pracy, zapoznaj się [naszej próbki](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="324d0-177">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c).</span></span> <span data-ttu-id="324d0-178">Postępuj zgodnie z instrukcjami [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) wprowadzić konfigurację usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="324d0-178">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-ios-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="324d0-179">Firma Microsoft zawsze są otwarte na opinie i sugestie!</span><span class="sxs-lookup"><span data-stu-id="324d0-179">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="324d0-180">Jeśli masz trudności w tym temacie lub mają zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii na dole strony.</span><span class="sxs-lookup"><span data-stu-id="324d0-180">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="324d0-181">Funkcja żądań, dodaj je do [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="324d0-181">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
