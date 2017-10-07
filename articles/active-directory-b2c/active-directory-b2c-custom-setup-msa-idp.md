---
title: "Usługa Azure Active Directory B2C: Dodawanie konta Microsoft (MSA) jako dostawca tożsamości za pomocą zasad niestandardowych"
description: "Przykładowe za pomocą programu Microsoft jako dostawca tożsamości za pomocą protokołu OpenID Connect (OIDC)"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: 577ac612f69015e6790f2fa9f2cfb42c2b524b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-microsoft-account-msa-as-an-identity-provider-using-custom-policies"></a><span data-ttu-id="1880f-103">Usługa Azure Active Directory B2C: Dodawanie konta Microsoft (MSA) jako dostawca tożsamości za pomocą zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="1880f-103">Azure Active Directory B2C: Add Microsoft Account (MSA) as an identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="1880f-104">W tym artykule opisano sposób tooenable logowania użytkowników z konta Microsoft (MSA) przy użyciu hello [niestandardowych zasad](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="1880f-104">This article shows you how tooenable sign-in for users from Microsoft account (MSA) through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1880f-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1880f-105">Prerequisites</span></span>
<span data-ttu-id="1880f-106">Zakończenie hello etapami hello [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="1880f-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="1880f-107">Kroki te obejmują:</span><span class="sxs-lookup"><span data-stu-id="1880f-107">These steps include:</span></span>

1.  <span data-ttu-id="1880f-108">Tworzenie aplikacji konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1880f-108">Creating a Microsoft account application.</span></span>
2.  <span data-ttu-id="1880f-109">Dodawanie hello Microsoft konta aplikacji klucza tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="1880f-109">Adding hello Microsoft account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="1880f-110">Dodawanie zasad tooa dostawcy oświadczeń</span><span class="sxs-lookup"><span data-stu-id="1880f-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="1880f-111">Rejestrowanie hello Account Microsoft oświadczeń dostawcy tooa użytkownika podróży</span><span class="sxs-lookup"><span data-stu-id="1880f-111">Registering hello Microsoft Account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="1880f-112">Przekazywanie hello tooan zasad usługi Azure AD B2C dzierżawy i przetestować go</span><span class="sxs-lookup"><span data-stu-id="1880f-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="1880f-113">Tworzenie aplikacji konta Microsoft</span><span class="sxs-lookup"><span data-stu-id="1880f-113">Create a Microsoft account application</span></span>
<span data-ttu-id="1880f-114">toouse konta Microsoft, funkcję dostawcy tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji konta Microsoft i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="1880f-114">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="1880f-115">Musisz mieć konto Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1880f-115">You need a Microsoft account.</span></span> <span data-ttu-id="1880f-116">Jeśli nie masz, odwiedź stronę [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="1880f-116">If you don’t have one, visit [https://www.live.com/](https://www.live.com/).</span></span>

1.  <span data-ttu-id="1880f-117">Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) i zaloguj się przy użyciu poświadczeń konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1880f-117">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2.  <span data-ttu-id="1880f-118">Kliknij przycisk **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="1880f-118">Click **Add an app**.</span></span>

    ![Microsoft konta — Dodawanie aplikacji](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-new-app.png)

3.  <span data-ttu-id="1880f-120">Podaj **nazwa** dla aplikacji, **adres e-mail kontaktu**, usuń zaznaczenie pola wyboru **nas pomocy Rozpoczynanie pracy** i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1880f-120">Provide a **Name** for your application, **Contact email**, uncheck **Let us help you get started** and click **Create**.</span></span>

    ![Konto Microsoft - rejestrowania aplikacji](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-name.png)

4.  <span data-ttu-id="1880f-122">Skopiuj wartość hello **identyfikator aplikacji**. Należy go tooconfigure konto Microsoft jako dostawca tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="1880f-122">Copy hello value of **Application Id**. You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>

    ![Konto Microsoft - kopiowania hello wartość identyfikatora aplikacji](media/active-directory-b2c-custom-setup-ms-account-idp/msa-app-id.png)

5.  <span data-ttu-id="1880f-124">Polecenie **Dodaj platformy**</span><span class="sxs-lookup"><span data-stu-id="1880f-124">Click on **Add platform**</span></span>

    ![Microsoft konta — Dodawanie platformy](media/active-directory-b2c-custom-setup-ms-account-idp/msa-add-platform.png)

6.  <span data-ttu-id="1880f-126">Z listy platformy hello wybierz **Web**.</span><span class="sxs-lookup"><span data-stu-id="1880f-126">From hello platform list, choose **Web**.</span></span>

    ![Konto Microsoft — z listy platformy hello wybierz sieci Web](media/active-directory-b2c-custom-setup-ms-account-idp/msa-web.png)

7.  <span data-ttu-id="1880f-128">Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **identyfikator URI przekierowania** pola.</span><span class="sxs-lookup"><span data-stu-id="1880f-128">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="1880f-129">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="1880f-129">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>

    ![Konto Microsoft — zestaw adresów URL przekierowania.](media/active-directory-b2c-custom-setup-ms-account-idp/msa-redirect-url.png)

8.  <span data-ttu-id="1880f-131">Polecenie **wygenerować nowe hasło** w obszarze hello **klucze tajne aplikacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1880f-131">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="1880f-132">Skopiuj nowe hasło hello wyświetlany na ekranie.</span><span class="sxs-lookup"><span data-stu-id="1880f-132">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="1880f-133">Należy go tooconfigure konto Microsoft jako dostawca tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="1880f-133">You need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="1880f-134">To hasło jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1880f-134">This password is an important security credential.</span></span>

    ![Microsoft konta — wygenerować nowe hasło](media/active-directory-b2c-custom-setup-ms-account-idp/msa-generate-new-password.png)

    ![Konto Microsoft - kopiowania hello nowe hasło](media/active-directory-b2c-custom-setup-ms-account-idp/msa-new-password.png)

9.  <span data-ttu-id="1880f-137">Witaj opcję **Obsługa zestaw Live SDK** w obszarze hello **zaawansowane opcje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1880f-137">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="1880f-138">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1880f-138">Click **Save**.</span></span>

    ![Konto Microsoft — Obsługa zestaw Live SDK](media/active-directory-b2c-custom-setup-ms-account-idp/msa-live-sdk-support.png)

## <a name="add-hello-microsoft-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="1880f-140">Dodaj hello Microsoft konta aplikacji klucza tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="1880f-140">Add hello Microsoft account application key tooAzure AD B2C</span></span>
<span data-ttu-id="1880f-141">Federacja z kontami Microsoft wymaga klucza tajnego klienta tootrust konta Microsoft Azure AD B2C w imieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1880f-141">Federation with Microsoft accounts requires a client secret for Microsoft account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="1880f-142">Należy toostore Twojego secert aplikacji konta Microsoft, w dzierżawie usługi Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="1880f-142">You need toostore your Microsoft account application secert in Azure AD B2C tenant:</span></span>   

1.  <span data-ttu-id="1880f-143">Przejdź do dzierżawy usługi Azure AD B2C tooyour i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości**</span><span class="sxs-lookup"><span data-stu-id="1880f-143">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="1880f-144">Wybierz **zasad kluczy** klawiszy hello tooview dostępnych w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="1880f-144">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="1880f-145">Kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="1880f-145">Click **+Add**.</span></span>
4.  <span data-ttu-id="1880f-146">Aby uzyskać **opcje**, użyj **ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="1880f-146">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="1880f-147">Aby uzyskać **nazwa**, użyj `MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="1880f-147">For **Name**, use `MSASecret`.</span></span>  
    <span data-ttu-id="1880f-148">Prefiks Hello `B2C_1A_` mogą być dodawane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="1880f-148">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="1880f-149">W hello **klucz tajny** wprowadź klucz tajny aplikacji firmy Microsoft z https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="1880f-149">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="1880f-150">Aby uzyskać **użycie klucza**, użyj **podpisu**.</span><span class="sxs-lookup"><span data-stu-id="1880f-150">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="1880f-151">Kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="1880f-151">Click **Create**</span></span>
9.  <span data-ttu-id="1880f-152">Upewnij się, że utworzono klucz hello `B2C_1A_MSASecret`.</span><span class="sxs-lookup"><span data-stu-id="1880f-152">Confirm that you've created hello key `B2C_1A_MSASecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="1880f-153">Dodawanie dostawcy oświadczeń w zasadach rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="1880f-153">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="1880f-154">Jeśli chcesz toosign użytkowników przy użyciu Account firmy Microsoft, należy toodefine Account Microsoft jako dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="1880f-154">If you want users toosign in by using Microsoft Account, you need toodefine Microsoft Account as a claims provider.</span></span> <span data-ttu-id="1880f-155">Innymi słowy należy toospecify punktu końcowego, który komunikuje się usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="1880f-155">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="1880f-156">punkt końcowy Hello zawiera zestaw oświadczeń, które są używane przez usługi Azure AD B2C tooverify, który został uwierzytelniony określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1880f-156">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="1880f-157">Zdefiniuj Account Microsoft jako dostawcy oświadczeń, dodając `<ClaimsProvider>` węzeł rozszerzenia pliku zasad:</span><span class="sxs-lookup"><span data-stu-id="1880f-157">Define Microsoft Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="1880f-158">Otwórz plik zasad rozszerzenia hello (TrustFrameworkExtensions.xml) z katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="1880f-158">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="1880f-159">Jeśli potrzebujesz edytora XML [spróbuj Visual Studio Code](https://code.visualstudio.com/download), lekkie edytora i platform.</span><span class="sxs-lookup"><span data-stu-id="1880f-159">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="1880f-160">Znajdź hello `<ClaimsProviders>` sekcji</span><span class="sxs-lookup"><span data-stu-id="1880f-160">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="1880f-161">Dodaj następujący fragment kodu XML w obszarze hello `ClaimsProviders` elementu:</span><span class="sxs-lookup"><span data-stu-id="1880f-161">Add following XML snippet under hello `ClaimsProviders` element:</span></span>

    ```xml
<ClaimsProvider>
    <Domain>live.com</Domain>
    <DisplayName>Microsoft Account</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="MSA-OIDC">
        <DisplayName>Microsoft Account</DisplayName>
        <Protocol Name="OpenIdConnect" />
        <Metadata>
        <Item Key="ProviderName">https://login.live.com</Item>
        <Item Key="METADATA">https://login.live.com/.well-known/openid-configuration</Item>
        <Item Key="response_types">code</Item>
        <Item Key="response_mode">form_post</Item>
        <Item Key="scope">openid profile email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Microsoft application client id</Item>
        </Metadata>
    <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_MSASecret" />
    </CryptographicKeys>
    <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="live.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="sub" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="email" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

4.  <span data-ttu-id="1880f-162">Zastąp `client_id` wartości identyfikatora klienta aplikacji Account firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="1880f-162">Replace `client_id` value with your Microsoft Account application client Id</span></span>

5.  <span data-ttu-id="1880f-163">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="1880f-163">Save hello file.</span></span>

## <a name="register-hello-microsoft-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="1880f-164">Zarejestruj hello Account Microsoft oświadczeń dostawcy tooSign się lub logowanie przebieg użytkownika</span><span class="sxs-lookup"><span data-stu-id="1880f-164">Register hello Microsoft Account claims provider tooSign up or Sign-in user journey</span></span>

<span data-ttu-id="1880f-165">W tym momencie hello dostawcy tożsamości nie został skonfigurowany, ale nie jest dostępna w żadnym hello konta-konta/logowania ekranów.</span><span class="sxs-lookup"><span data-stu-id="1880f-165">At this point, hello identity provider has been set up, but it’s not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="1880f-166">Teraz należy użytkownika tooyour dostawcy tożsamości Account Microsoft hello tooadd `SignUpOrSignIn` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1880f-166">Now you need tooadd hello Microsoft Account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="1880f-167">toomake ją, utworzymy duplikatem istniejącej przebieg użytkownika szablonu.</span><span class="sxs-lookup"><span data-stu-id="1880f-167">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="1880f-168">Następnie dodaj dostawcy tożsamości Account Microsoft hello:</span><span class="sxs-lookup"><span data-stu-id="1880f-168">Then we add hello Microsoft Account identity provider:</span></span>

> [!NOTE]
>
><span data-ttu-id="1880f-169">Jeśli został wcześniej skopiowany hello `<UserJourneys>` elementu z pliku podstawowego pliku rozszerzenia zasad toohello `TrustFrameworkExtensions.xml`, toothis sekcję można pominąć.</span><span class="sxs-lookup"><span data-stu-id="1880f-169">If you previously copied hello `<UserJourneys>` element from base file of your policy toohello extension file `TrustFrameworkExtensions.xml`, you can skip toothis section.</span></span>

1.  <span data-ttu-id="1880f-170">Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="1880f-170">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="1880f-171">Znajdź hello `<UserJourneys>` element kopiowania hello całej zawartości i `<UserJourneys>` węzła.</span><span class="sxs-lookup"><span data-stu-id="1880f-171">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="1880f-172">Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml) i Znajdź hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="1880f-172">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="1880f-173">Jeśli hello element nie istnieje, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="1880f-173">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="1880f-174">Wklej zawartość całego hello `<UserJournesy>` węzła, który został skopiowany jako element podrzędny hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="1880f-174">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="1880f-175">Przycisk hello wyświetlania</span><span class="sxs-lookup"><span data-stu-id="1880f-175">Display hello button</span></span>
<span data-ttu-id="1880f-176">Witaj `<ClaimsProviderSelections>` element definiuje listę hello opcje wyboru dostawcy oświadczeń i ich kolejność.</span><span class="sxs-lookup"><span data-stu-id="1880f-176">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="1880f-177">`<ClaimsProviderSelection>`element jest przycisku dostawcy tożsamości analogiczne tooan na stronie konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="1880f-177">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="1880f-178">Jeśli dodasz `<ClaimsProviderSelection>` elementu dla konta Microsoft, nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="1880f-178">If you add a `<ClaimsProviderSelection>` element for Microsoft account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="1880f-179">tooadd tego elementu:</span><span class="sxs-lookup"><span data-stu-id="1880f-179">tooadd this element:</span></span>

1.  <span data-ttu-id="1880f-180">Znajdź hello `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"` w podróży użytkownika hello, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="1880f-180">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="1880f-181">Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="1880f-181">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="1880f-182">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="1880f-182">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="1880f-183">Akcja tooan przycisku hello łącza</span><span class="sxs-lookup"><span data-stu-id="1880f-183">Link hello button tooan action</span></span>
<span data-ttu-id="1880f-184">Teraz, gdy masz przycisku w miejscu, należy toolink go tooan akcji.</span><span class="sxs-lookup"><span data-stu-id="1880f-184">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="1880f-185">Akcja Hello jest dla usługi Azure AD B2C toocommunicate z tooreceive Account Microsoft w tym przypadku tokenu.</span><span class="sxs-lookup"><span data-stu-id="1880f-185">hello action, in this case, is for Azure AD B2C toocommunicate with Microsoft Account tooreceive a token.</span></span> <span data-ttu-id="1880f-186">Link akcji tooan przycisk hello przez łączenie hello techniczne profilu dla dostawcy oświadczeń Account Microsoft:</span><span class="sxs-lookup"><span data-stu-id="1880f-186">Link hello button tooan action by linking hello technical profile for your Microsoft Account claims provider:</span></span>

1.  <span data-ttu-id="1880f-187">Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="1880f-187">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="1880f-188">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="1880f-188">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

> [!NOTE]
>
>   * <span data-ttu-id="1880f-189">Upewnij się, hello `Id` ma takie same wartości jak hello `TargetClaimsExchangeId` w powyższej sekcji hello</span><span class="sxs-lookup"><span data-stu-id="1880f-189">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
>   * <span data-ttu-id="1880f-190">Upewnij się, `TechnicalProfileReferenceId` ustawiono Identyfikatora profilu techniczne toohello utworzonego wcześniej (MSA-OIDC).</span><span class="sxs-lookup"><span data-stu-id="1880f-190">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (MSA-OIDC).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="1880f-191">Przekaż hello zasad tooyour dzierżawy</span><span class="sxs-lookup"><span data-stu-id="1880f-191">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="1880f-192">W hello [portalu Azure](https://portal.azure.com), przejdź do hello [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)i otwórz hello **usługi Azure AD B2C** bloku.</span><span class="sxs-lookup"><span data-stu-id="1880f-192">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="1880f-193">Wybierz **Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="1880f-193">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="1880f-194">Otwórz hello **wszystkie zasady** bloku.</span><span class="sxs-lookup"><span data-stu-id="1880f-194">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="1880f-195">Wybierz **przekazywać zasady**.</span><span class="sxs-lookup"><span data-stu-id="1880f-195">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="1880f-196">Sprawdź **zastąpić hello zasady, jeśli istnieje** pole.</span><span class="sxs-lookup"><span data-stu-id="1880f-196">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="1880f-197">**Przekaż** TrustFrameworkExtensions.xml i upewnij się, że nie wystąpi niepowodzenie weryfikacji hello</span><span class="sxs-lookup"><span data-stu-id="1880f-197">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="1880f-198">Testowanie zasad niestandardowych hello przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="1880f-198">Test hello custom policy by using Run Now</span></span>

1.  <span data-ttu-id="1880f-199">Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="1880f-199">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
> [!NOTE]
>
><span data-ttu-id="1880f-200">**Uruchom teraz** wymaga co najmniej jedną aplikację toobe preregistered hello dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="1880f-200">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> <span data-ttu-id="1880f-201">toolearn tooregister aplikacji, zobacz temat hello Azure AD B2C [wprowadzenie](active-directory-b2c-get-started.md) artykułu lub hello [Rejestracja aplikacji](active-directory-b2c-app-registration.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="1880f-201">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>
2.  <span data-ttu-id="1880f-202">Otwórz **B2C_1A_signup_signin**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="1880f-202">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="1880f-203">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="1880f-203">Select **Run now**.</span></span>
3.  <span data-ttu-id="1880f-204">Powinno być możliwe toosign za pomocą konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1880f-204">You should be able toosign in using Microsoft account.</span></span>

## <a name="optional-register-hello-microsoft-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="1880f-205">[Opcjonalnie] Zarejestruj hello Account Microsoft oświadczeń dostawcy tooProfile Edycja użytkownika podróży</span><span class="sxs-lookup"><span data-stu-id="1880f-205">[Optional] Register hello Microsoft Account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="1880f-206">Możesz dostawcy tożsamości Account Microsoft hello tooadd również użytkownika tooyour `ProfileEdit` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1880f-206">You may want tooadd hello Microsoft Account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="1880f-207">toomake ją, powtórz firma Microsoft hello ostatnie dwa kroki:</span><span class="sxs-lookup"><span data-stu-id="1880f-207">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="1880f-208">Przycisk hello wyświetlania</span><span class="sxs-lookup"><span data-stu-id="1880f-208">Display hello button</span></span>
1.  <span data-ttu-id="1880f-209">Otwórz plik rozszerzenia hello zasad (na przykład TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="1880f-209">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="1880f-210">Znajdź hello `<UserJourney>` węzła, który zawiera `Id="ProfileEdit"` w podróży użytkownika hello, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="1880f-210">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="1880f-211">Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="1880f-211">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="1880f-212">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="1880f-212">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="MSAExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="1880f-213">Akcja tooan przycisku hello łącza</span><span class="sxs-lookup"><span data-stu-id="1880f-213">Link hello button tooan action</span></span>
1.  <span data-ttu-id="1880f-214">Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="1880f-214">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="1880f-215">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="1880f-215">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="MSAExchange" TechnicalProfileReferenceId="MSA-OIDC" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="1880f-216">Testowanie zasad niestandardowych edycji profilu hello przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="1880f-216">Test hello custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="1880f-217">Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="1880f-217">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="1880f-218">Otwórz **B2C_1A_ProfileEdit**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="1880f-218">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="1880f-219">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="1880f-219">Select **Run now**.</span></span>
3.  <span data-ttu-id="1880f-220">Powinno być możliwe toosign za pomocą konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1880f-220">You should be able toosign in using Microsoft account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="1880f-221">Pobierz pliki zasad pełną hello</span><span class="sxs-lookup"><span data-stu-id="1880f-221">Download hello complete policy files</span></span>
<span data-ttu-id="1880f-222">Opcjonalnie: Zaleca się tworzenie scenariusz przy użyciu własnych niestandardowych zasad plików po zakończeniu hello wprowadzenie zasady niestandardowe przeprowadzenie zamiast te przykładowe pliki.</span><span class="sxs-lookup"><span data-stu-id="1880f-222">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="1880f-223">Przykładowe pliki zasad dla odwołania</span><span class="sxs-lookup"><span data-stu-id="1880f-223">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-msa-app)
