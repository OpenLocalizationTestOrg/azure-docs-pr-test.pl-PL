---
title: "Usługa Azure Active Directory B2C: Pobierania tokenu przy użyciu aplikacji systemu Android | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób tworzenia aplikacji systemu Android AppAuth z usługi Azure Active Directory B2C jest używana do zarządzania tożsamościami użytkowników i uwierzytelniania użytkowników."
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: d00947c3-dcaa-4cb3-8c2e-d94e0746d8b2
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 03/06/2017
ms.author: parakhj
ms.openlocfilehash: cd4b8048245be49ea79bcb1b364f2f99c56f8291
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="1cb8b-103">Usługa Azure AD B2C: Zaloguj się przy użyciu aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="1cb8b-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="1cb8b-104">Platforma Microsoft Identity korzysta z otwartych standardów, takich jak OAuth2 i OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-104">The Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="1cb8b-105">Umożliwia to deweloperom korzystanie z każdej biblioteki, którą chcą zintegrować z naszymi usługami.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-105">This allows developers to leverage any library they wish to integrate with our services.</span></span> <span data-ttu-id="1cb8b-106">Aby pomóc deweloperom przy użyciu platformy z innych bibliotek, możemy napisanych kilka wskazówki podobny do pokazują, jak skonfigurować 3 bibliotek strona nawiązać połączenia z platformą tożsamości Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-106">To aid developers in using our platform with other libraries, we've written a few walkthroughs like this one to demonstrate how to configure 3rd party libraries to connect to the Microsoft identity platform.</span></span> <span data-ttu-id="1cb8b-107">Z platformą Microsoft Identity może łączyć się większość bibliotek implementujących [specyfikację RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-107">Most libraries that implement [the RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able to connect to the Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="1cb8b-108">Firma Microsoft zapewnia poprawki dla 3rd strony biblioteki i nie przeprowadził Przegląd tych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="1cb8b-109">W tym przykładzie używa 3 biblioteki firmy o nazwie AppAuth, które zostały przetestowane na zgodność w podstawowe scenariusze w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with the Azure AD B2C.</span></span> <span data-ttu-id="1cb8b-110">Problemy i żądania funkcji powinny być kierowane do biblioteki projektu open source.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-110">Issues and feature requests should be directed to the library's open-source project.</span></span> <span data-ttu-id="1cb8b-111">Zobacz [w tym artykule](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="1cb8b-112">Jeśli dopiero rozpoczynasz korzystanie ze standardu OAuth2 lub OpenID Connect, spora część tej przykładowej konfiguracji może być dla Ciebie niezrozumiała.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-112">If you're new to OAuth2 or OpenID Connect much of this sample configuration may not make much sense to you.</span></span> <span data-ttu-id="1cb8b-113">Zalecamy zapoznanie się z [krótkim omówieniem protokołu w tej dokumentacji](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-113">We recommend you look at a brief [overview of the protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="1cb8b-114">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="1cb8b-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="1cb8b-115">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="1cb8b-116">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="1cb8b-117">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="1cb8b-118">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="1cb8b-118">Create an application</span></span>

<span data-ttu-id="1cb8b-119">Następnie musisz utworzyć aplikację w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-119">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="1cb8b-120">Dzięki temu do usługi Azure AD będą przekazywane informacje wymagane do bezpiecznego komunikowania się z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-120">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="1cb8b-121">Aby utworzyć aplikacji mobilnej, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-121">To create a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="1cb8b-122">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="1cb8b-122">Be sure to:</span></span>

* <span data-ttu-id="1cb8b-123">Obejmują **Native Client** w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-123">Include a **Native Client** in the application.</span></span>
* <span data-ttu-id="1cb8b-124">Skopiuj **Identyfikator aplikacji** przypisany do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-124">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="1cb8b-125">Będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-125">You will need this later.</span></span>
* <span data-ttu-id="1cb8b-126">Konfigurowanie klienta natywnego **identyfikator URI przekierowania** (np. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="1cb8b-127">On również będzie później potrzebny.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="1cb8b-128">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="1cb8b-128">Create your policies</span></span>

<span data-ttu-id="1cb8b-129">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="1cb8b-130">Ta aplikacja zawiera jeden obsługi tożsamości: połączone logowania i rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="1cb8b-131">Należy utworzyć te zasady, zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-131">You need to create this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="1cb8b-132">Podczas tworzenia zasad należy:</span><span class="sxs-lookup"><span data-stu-id="1cb8b-132">When you create the policy, be sure to:</span></span>

* <span data-ttu-id="1cb8b-133">Wybierz **Nazwa wyświetlana** jako atrybut rejestracji w zasadach.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-133">Choose the **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="1cb8b-134">Wybrać oświadczenia aplikacji **Nazwa wyświetlana** oraz **Identyfikator obiektu** we wszystkich zasadach.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-134">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="1cb8b-135">Można również wybrać inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="1cb8b-136">Skopiować każdą utworzoną wartość **Nazwa** zasad.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-136">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="1cb8b-137">Powinny zawierać prefiks `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-137">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="1cb8b-138">Nazwa zasad będzie potrzebna później.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-138">You'll need the policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="1cb8b-139">Po utworzeniu zasad będzie można rozpocząć tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-139">After you have created your policies, you're ready to build your app.</span></span>

## <a name="download-the-sample-code"></a><span data-ttu-id="1cb8b-140">Pobierz przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="1cb8b-140">Download the sample code</span></span>

<span data-ttu-id="1cb8b-141">Firma Microsoft umieściła próbki pracy, który korzysta z usługi Azure AD B2C AppAuth [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="1cb8b-142">Można go pobrać i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-142">You can download the code and run it.</span></span> <span data-ttu-id="1cb8b-143">Możesz szybko rozpocząć pracę z własną aplikację przy użyciu konfiguracji usługi Azure AD B2C, postępując zgodnie z instrukcjami w [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following the instructions in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="1cb8b-144">Próbka jest modyfikacji próbki dostarczonych przez [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-144">The sample is a modification of the sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="1cb8b-145">Odwiedź ich strony, aby dowiedzieć się więcej o AppAuth i ich funkcje.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-145">Please visit their page to learn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-to-use-azure-ad-b2c-with-appauth"></a><span data-ttu-id="1cb8b-146">Modyfikowanie aplikacji do użycia usługi Azure AD B2C z AppAuth</span><span class="sxs-lookup"><span data-stu-id="1cb8b-146">Modifying your app to use Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="1cb8b-147">AppAuth obsługuje 16 interfejsu API systemu Android (Jellybean) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="1cb8b-148">Firma Microsoft zaleca używanie 23 interfejsu API i powyżej.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="1cb8b-149">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="1cb8b-149">Configuration</span></span>

<span data-ttu-id="1cb8b-150">Komunikację można skonfigurować z usługi Azure AD B2C, określając odnajdywania identyfikatora URI lub określając punktu końcowego autoryzacji i punktu końcowego tokena identyfikatorów URI.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-150">You can configure communication with Azure AD B2C by either specifying the discovery URI or by specifying both the authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="1cb8b-151">W obu przypadkach należy następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="1cb8b-151">In either case, you will need the following information:</span></span>

* <span data-ttu-id="1cb8b-152">Identyfikator dzierżawcy (np. contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="1cb8b-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="1cb8b-153">Nazwa zasad (np. B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="1cb8b-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="1cb8b-154">Jeśli wybierzesz opcję automatycznego wykrywania autoryzacji i tokena punktu końcowego identyfikatory URI, konieczne będzie pobranie informacji dotyczących odnajdywania identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-154">If you choose to automatically discover the authorization and token endpoint URIs, you will need to fetch information from the discovery URI.</span></span> <span data-ttu-id="1cb8b-155">Odnajdywania, zastępując dzierżawcy można wygenerować identyfikatora URI\_identyfikator i zasady\_nazwy w następujący adres URL:</span><span class="sxs-lookup"><span data-stu-id="1cb8b-155">The discovery URI can be generated by replacing the Tenant\_ID and the Policy\_Name in the following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="1cb8b-156">Można uzyskać autoryzacji i tokena punktu końcowego identyfikatorów URI i utworzenia obiektu AuthorizationServiceConfiguration, uruchamiając następujące:</span><span class="sxs-lookup"><span data-stu-id="1cb8b-156">You can then acquire the authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running the following:</span></span>

```java
final Uri issuerUri = Uri.parse(mDiscoveryURI);
AuthorizationServiceConfiguration config;

AuthorizationServiceConfiguration.fetchFromIssuer(
    issuerUri,
    new RetrieveConfigurationCallback() {
      @Override public void onFetchConfigurationCompleted(
          @Nullable AuthorizationServiceConfiguration serviceConfiguration,
          @Nullable AuthorizationException ex) {
        if (ex != null) {
            Log.w(TAG, "Failed to retrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed to authorization...
        }
      }
  });
```

<span data-ttu-id="1cb8b-157">Zamiast używać odnajdywania uzyskanie autoryzacji i tokena punktu końcowego identyfikatory URI, można również określić je jawnie przez zastąpienie dzierżawcy\_identyfikator i zasady\_nazwą w adresie URL poniżej:</span><span class="sxs-lookup"><span data-stu-id="1cb8b-157">Instead of using discovery to obtain the authorization and token endpoint URIs, you can also specify them explicitly by replacing the Tenant\_ID and the Policy\_Name in the URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="1cb8b-158">Uruchom następujący kod, aby utworzyć obiekt AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="1cb8b-158">Run the following code to create your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform the auth request...
```

### <a name="authorizing"></a><span data-ttu-id="1cb8b-159">Autoryzowanie</span><span class="sxs-lookup"><span data-stu-id="1cb8b-159">Authorizing</span></span>

<span data-ttu-id="1cb8b-160">Po Konfigurowanie lub pobieranie konfiguracji usługi autoryzacji, można utworzyć żądania autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="1cb8b-161">Aby utworzyć żądanie, są potrzebne następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="1cb8b-161">To create the request, you will need the following information:</span></span>

* <span data-ttu-id="1cb8b-162">Identyfikator klienta (np. 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="1cb8b-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="1cb8b-163">Identyfikator URI przekierowania z schematu niestandardowego (np. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="1cb8b-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="1cb8b-164">Oba elementy powinny zostały zapisane, gdy użytkownik [rejestrowanie aplikacji](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="1cb8b-165">Zapoznaj się z [przewodnik AppAuth](https://openid.github.io/AppAuth-Android/) na temat sposobu ukończenia resztę procesu.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-165">Please refer to the [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how to complete the rest of the process.</span></span> <span data-ttu-id="1cb8b-166">Jeśli potrzebujesz szybko rozpocząć pracę z aplikacją pracy, zapoznaj się [naszej próbki](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-166">If you need to quickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="1cb8b-167">Postępuj zgodnie z instrukcjami [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) wprowadzić konfigurację usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-167">Follow the steps in the [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) to enter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="1cb8b-168">Firma Microsoft zawsze są otwarte na opinie i sugestie!</span><span class="sxs-lookup"><span data-stu-id="1cb8b-168">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="1cb8b-169">Jeśli masz trudności w tym temacie lub mają zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii na dole strony.</span><span class="sxs-lookup"><span data-stu-id="1cb8b-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="1cb8b-170">Funkcja żądań, dodaj je do [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="1cb8b-170">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

