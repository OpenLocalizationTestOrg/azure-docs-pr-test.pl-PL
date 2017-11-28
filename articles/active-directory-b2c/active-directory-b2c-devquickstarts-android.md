---
title: "Usługa Azure Active Directory B2C: Pobierania tokenu przy użyciu aplikacji systemu Android | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate aplikację systemu Android, który korzysta z tożsamości użytkowników usługi Azure Active Directory B2C toomanage AppAuth i uwierzytelnianie użytkowników."
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
ms.openlocfilehash: 0236398673115a34951f035cb1e73e89417abf86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-sign-in-using-an-android-application"></a><span data-ttu-id="a0a7c-103">Usługa Azure AD B2C: Zaloguj się przy użyciu aplikacji systemu Android</span><span class="sxs-lookup"><span data-stu-id="a0a7c-103">Azure AD B2C: Sign-in using an Android application</span></span>

<span data-ttu-id="a0a7c-104">korzysta z platformą tożsamości Microsoft Hello Otwórz standardy, takie jak OAuth2 i OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="a0a7c-105">Dzięki temu deweloperzy mogą tooleverage żadnej biblioteki życzą toointegrate z naszych usług.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-105">This allows developers tooleverage any library they wish toointegrate with our services.</span></span> <span data-ttu-id="a0a7c-106">Deweloperzy tooaid przy użyciu platformy z innych bibliotek, możemy napisanych kilka wskazówki, takich jak ta toodemonstrate jeden sposób tooconfigure 3 bibliotek tooconnect toohello Microsoft tożsamość platformy firmy.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-106">tooaid developers in using our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure 3rd party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="a0a7c-107">Większość bibliotek, które implementują [specyfikację RFC6749 OAuth2 hello](https://tools.ietf.org/html/rfc6749) będą mogli tooconnect toohello pakietu Microsoft Identity platformy.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) will be able tooconnect toohello Microsoft Identity platform.</span></span>

> [!WARNING]
> <span data-ttu-id="a0a7c-108">Firma Microsoft zapewnia poprawki dla 3rd strony biblioteki i nie przeprowadził Przegląd tych bibliotek.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-108">Microsoft does not provide fixes for 3rd party libraries and has not done a review of those libraries.</span></span> <span data-ttu-id="a0a7c-109">W tym przykładzie używa 3 biblioteki firmy o nazwie AppAuth, które zostały przetestowane zgodność w podstawowe scenariusze z hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-109">This sample is using a 3rd party library called AppAuth that has been tested for compatibility in basic scenarios with hello Azure AD B2C.</span></span> <span data-ttu-id="a0a7c-110">Problemy i żądania funkcji powinny być projekt open source ukierunkowanej toohello biblioteki.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-110">Issues and feature requests should be directed toohello library's open-source project.</span></span> <span data-ttu-id="a0a7c-111">Zobacz [w tym artykule](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-111">Please see [this article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-libraries) for more information.</span></span>  
>
>

<span data-ttu-id="a0a7c-112">W przypadku nowych tooOAuth2 lub OpenID Connect znacznie to przykładowa konfiguracja może nie mieć wiele tooyou znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-112">If you're new tooOAuth2 or OpenID Connect much of this sample configuration may not make much sense tooyou.</span></span> <span data-ttu-id="a0a7c-113">Firma Microsoft zaleca, Obejrzyj krótkie [Omówienie protokołu hello mamy już opisanych tutaj](active-directory-b2c-reference-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-113">We recommend you look at a brief [overview of hello protocol we've documented here](active-directory-b2c-reference-protocols.md).</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="a0a7c-114">Tworzenie katalogu usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="a0a7c-114">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="a0a7c-115">Przed rozpoczęciem korzystania z usługi Azure AD B2C należy utworzyć katalog lub dzierżawę.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-115">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span> <span data-ttu-id="a0a7c-116">Katalog jest kontenerem dla wszystkich użytkowników, aplikacji, grup i innych elementów.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-116">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="a0a7c-117">Jeśli jeszcze go nie masz, [utwórz katalog usługi B2C](active-directory-b2c-get-started.md), zanim przejdziesz dalej.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-117">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="a0a7c-118">Tworzenie aplikacji</span><span class="sxs-lookup"><span data-stu-id="a0a7c-118">Create an application</span></span>

<span data-ttu-id="a0a7c-119">Następnie należy toocreate aplikację w katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-119">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="a0a7c-120">Dzięki temu informacji usługi Azure AD, że wymaga ona toocommunicate bezpiecznie z aplikacją.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-120">This gives Azure AD information that it needs toocommunicate securely with your app.</span></span> <span data-ttu-id="a0a7c-121">toocreate aplikacji mobilnej, wykonaj [tych instrukcji](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-121">toocreate a mobile app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="a0a7c-122">Należy pamiętać o wykonaniu następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="a0a7c-122">Be sure to:</span></span>

* <span data-ttu-id="a0a7c-123">Obejmują **Native Client** w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-123">Include a **Native Client** in hello application.</span></span>
* <span data-ttu-id="a0a7c-124">Kopiuj hello **identyfikator aplikacji** czyli przypisanej tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-124">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="a0a7c-125">Będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-125">You will need this later.</span></span>
* <span data-ttu-id="a0a7c-126">Konfigurowanie klienta natywnego **identyfikator URI przekierowania** (np. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-126">Set up a native client **Redirect URI** (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauth/redirect).</span></span> <span data-ttu-id="a0a7c-127">On również będzie później potrzebny.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-127">You will also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="a0a7c-128">Tworzenie zasad</span><span class="sxs-lookup"><span data-stu-id="a0a7c-128">Create your policies</span></span>

<span data-ttu-id="a0a7c-129">W usłudze Azure AD B2C każde działanie użytkownika jest definiowane przy użyciu [zasad](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-129">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="a0a7c-130">Ta aplikacja zawiera jeden obsługi tożsamości: połączone logowania i rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-130">This app contains one identity experience: a combined sign-in and sign-up.</span></span> <span data-ttu-id="a0a7c-131">Należy toocreate te zasady, zgodnie z opisem w [artykule o zasadach](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-131">You need toocreate this policy, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="a0a7c-132">Po utworzeniu hello zasad należy koniecznie:</span><span class="sxs-lookup"><span data-stu-id="a0a7c-132">When you create hello policy, be sure to:</span></span>

* <span data-ttu-id="a0a7c-133">Wybierz hello **Nazwa wyświetlana** jako atrybut rejestracji w zasadach.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-133">Choose hello **Display name** as a sign-up attribute in your policy.</span></span>
* <span data-ttu-id="a0a7c-134">Wybierz hello **Nazwa wyświetlana** i **obiektu o identyfikatorze** oświadczenia aplikacji we wszystkich zasadach.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-134">Choose hello **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="a0a7c-135">Można również wybrać inne oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-135">You can choose other claims as well.</span></span>
* <span data-ttu-id="a0a7c-136">Kopiuj hello **nazwa** poszczególnych zasad po jego utworzeniu.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-136">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="a0a7c-137">Powinien on mieć prefiks hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-137">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="a0a7c-138">Nazwa zasad hello będą potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-138">You'll need hello policy name later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="a0a7c-139">Po utworzeniu zasad, wszystko jest gotowe toobuild aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-139">After you have created your policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-sample-code"></a><span data-ttu-id="a0a7c-140">Pobierz hello przykładowy kod</span><span class="sxs-lookup"><span data-stu-id="a0a7c-140">Download hello sample code</span></span>

<span data-ttu-id="a0a7c-141">Firma Microsoft umieściła próbki pracy, który korzysta z usługi Azure AD B2C AppAuth [w serwisie GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-141">We have provided a working sample that uses AppAuth with Azure AD B2C [on GitHub](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="a0a7c-142">Można pobrać kodu hello i uruchom go.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-142">You can download hello code and run it.</span></span> <span data-ttu-id="a0a7c-143">Możesz szybko rozpocząć pracę z własną aplikację przy użyciu konfigurację usługi Azure AD B2C, wykonując następujące instrukcje hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-143">You can quickly get started with your own app using your own Azure AD B2C configuration by following hello instructions in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md).</span></span>

<span data-ttu-id="a0a7c-144">przykład Hello jest modyfikacji próbki hello dostarczonych przez [AppAuth](https://openid.github.io/AppAuth-Android/).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-144">hello sample is a modification of hello sample provided by [AppAuth](https://openid.github.io/AppAuth-Android/).</span></span> <span data-ttu-id="a0a7c-145">Odwiedź ich toolearn strony więcej informacji na temat AppAuth i ich funkcje.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-145">Please visit their page toolearn more about AppAuth and its features.</span></span>

## <a name="modifying-your-app-toouse-azure-ad-b2c-with-appauth"></a><span data-ttu-id="a0a7c-146">Modyfikowanie toouse Twojej aplikacji usługi Azure AD B2C z AppAuth</span><span class="sxs-lookup"><span data-stu-id="a0a7c-146">Modifying your app toouse Azure AD B2C with AppAuth</span></span>

> [!NOTE]
> <span data-ttu-id="a0a7c-147">AppAuth obsługuje 16 interfejsu API systemu Android (Jellybean) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-147">AppAuth supports Android API 16 (Jellybean) and above.</span></span> <span data-ttu-id="a0a7c-148">Firma Microsoft zaleca używanie 23 interfejsu API i powyżej.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-148">We recommend using API 23 and above.</span></span>
>

### <a name="configuration"></a><span data-ttu-id="a0a7c-149">Konfiguracja</span><span class="sxs-lookup"><span data-stu-id="a0a7c-149">Configuration</span></span>

<span data-ttu-id="a0a7c-150">Komunikację z usługą Azure AD B2C można skonfigurować albo odnajdywania hello określania identyfikatora URI lub podając zarówno punktu końcowego autoryzacji hello, jak i punktu końcowego tokena identyfikatorów URI.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-150">You can configure communication with Azure AD B2C by either specifying hello discovery URI or by specifying both hello authorization endpoint and token endpoint URIs.</span></span> <span data-ttu-id="a0a7c-151">W obu przypadkach należy hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="a0a7c-151">In either case, you will need hello following information:</span></span>

* <span data-ttu-id="a0a7c-152">Identyfikator dzierżawcy (np. contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="a0a7c-152">Tenant ID (e.g. contoso.onmicrosoft.com)</span></span>
* <span data-ttu-id="a0a7c-153">Nazwa zasad (np. B2C\_1\_SignUpIn)</span><span class="sxs-lookup"><span data-stu-id="a0a7c-153">Policy name (e.g. B2C\_1\_SignUpIn)</span></span>

<span data-ttu-id="a0a7c-154">Jeśli wybierzesz tooautomatically odnajdywanie hello autoryzacji i tokena punktu końcowego identyfikatory URI, konieczne będą informacje toofetch z odnajdywania hello identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-154">If you choose tooautomatically discover hello authorization and token endpoint URIs, you will need toofetch information from hello discovery URI.</span></span> <span data-ttu-id="a0a7c-155">Hello odnajdywania, zastępując hello dzierżawcy można wygenerować identyfikatora URI\_identyfikator i hello zasad\_nazwy w hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="a0a7c-155">hello discovery URI can be generated by replacing hello Tenant\_ID and hello Policy\_Name in hello following URL:</span></span>

```java
String mDiscoveryURI = "https://login.microsoftonline.com/<Tenant_ID>/v2.0/.well-known/openid-configuration?p=<Policy_Name>";
```

<span data-ttu-id="a0a7c-156">Można następnie uzyskać hello autoryzacji i tokena punktu końcowego identyfikatorów URI i utworzenia obiektu AuthorizationServiceConfiguration, uruchamiając następujące hello:</span><span class="sxs-lookup"><span data-stu-id="a0a7c-156">You can then acquire hello authorization and token endpoint URIs and create an AuthorizationServiceConfiguration object by running hello following:</span></span>

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
            Log.w(TAG, "Failed tooretrieve configuration for " + issuerUri, ex);
        } else {
            // service configuration retrieved, proceed tooauthorization...
        }
      }
  });
```

<span data-ttu-id="a0a7c-157">Zamiast używać odnajdywania tooobtain hello autoryzacji i tokena punktu końcowego identyfikatory URI, można również określić je jawnie przez zastąpienie hello dzierżawy\_identyfikator i hello zasad\_nazwą w hello URL poniżej:</span><span class="sxs-lookup"><span data-stu-id="a0a7c-157">Instead of using discovery tooobtain hello authorization and token endpoint URIs, you can also specify them explicitly by replacing hello Tenant\_ID and hello Policy\_Name in hello URL's below:</span></span>

```java
String mAuthEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/authorize?p=<Policy_Name>";

String mTokenEndpoint = "https://login.microsoftonline.com/<Tenant_ID>/oauth2/v2.0/token?p=<Policy_Name>";
```

<span data-ttu-id="a0a7c-158">Uruchom hello poniższy kod toocreate obiektu AuthorizationServiceConfiguration:</span><span class="sxs-lookup"><span data-stu-id="a0a7c-158">Run hello following code toocreate your AuthorizationServiceConfiguration object:</span></span>

```java
AuthorizationServiceConfiguration config =
        new AuthorizationServiceConfiguration(name, mAuthEndpoint, mTokenEndpoint);

// perform hello auth request...
```

### <a name="authorizing"></a><span data-ttu-id="a0a7c-159">Autoryzowanie</span><span class="sxs-lookup"><span data-stu-id="a0a7c-159">Authorizing</span></span>

<span data-ttu-id="a0a7c-160">Po Konfigurowanie lub pobieranie konfiguracji usługi autoryzacji, można utworzyć żądania autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-160">After configuring or retrieving an authorization service configuration, an authorization request can be constructed.</span></span> <span data-ttu-id="a0a7c-161">Witaj toocreate żądania, konieczne będzie hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="a0a7c-161">toocreate hello request, you will need hello following information:</span></span>

* <span data-ttu-id="a0a7c-162">Identyfikator klienta (np. 00000000-0000-0000-0000-000000000000)</span><span class="sxs-lookup"><span data-stu-id="a0a7c-162">Client ID (e.g. 00000000-0000-0000-0000-000000000000)</span></span>
* <span data-ttu-id="a0a7c-163">Identyfikator URI przekierowania z schematu niestandardowego (np. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span><span class="sxs-lookup"><span data-stu-id="a0a7c-163">Redirect URI with a custom scheme (e.g. com.onmicrosoft.fabrikamb2c.exampleapp://oauthredirect)</span></span>

<span data-ttu-id="a0a7c-164">Oba elementy powinny zostały zapisane, gdy użytkownik [rejestrowanie aplikacji](#create-an-application).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-164">Both items should have been saved when you were [registering your app](#create-an-application).</span></span>

```java
AuthorizationRequest req = new AuthorizationRequest.Builder(
    config,
    clientId,
    ResponseTypeValues.CODE,
    redirectUri)
    .build();
```

<span data-ttu-id="a0a7c-165">Zobacz toohello [przewodnik AppAuth](https://openid.github.io/AppAuth-Android/) w sposób toocomplete hello resztę procesu hello.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-165">Please refer toohello [AppAuth guide](https://openid.github.io/AppAuth-Android/) on how toocomplete hello rest of hello process.</span></span> <span data-ttu-id="a0a7c-166">Jeśli potrzebujesz tooquickly rozpocząć pracę z aplikacją pracy, zapoznaj się z [naszej próbki](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-166">If you need tooquickly get started with a working app, check out [our sample](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c).</span></span> <span data-ttu-id="a0a7c-167">Wykonaj kroki hello hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter konfigurację usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-167">Follow hello steps in hello [README.md](https://github.com/Azure-Samples/active-directory-android-native-appauth-b2c/blob/master/README.md) tooenter your own Azure AD B2C configuration.</span></span>

<span data-ttu-id="a0a7c-168">Jesteśmy zawsze toofeedback otwarte i sugestie!</span><span class="sxs-lookup"><span data-stu-id="a0a7c-168">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="a0a7c-169">Jeśli masz trudności w tym temacie lub mają zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="a0a7c-169">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="a0a7c-170">Funkcja żądań, dodaj ich zbyt[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="a0a7c-170">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>

