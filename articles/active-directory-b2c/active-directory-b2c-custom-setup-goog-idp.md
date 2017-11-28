---
title: "Usługa Azure Active Directory B2C: Dodawanie Google + funkcję dostawcy tożsamości OAuth2 przy użyciu zasad niestandardowych"
description: "Przykładowe przy użyciu usługi Google + jako dostawca tożsamości za pomocą protokołu OAuth2"
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
ms.openlocfilehash: 4feff21979c9c3b3b12c7a1cae4db0121d1bd79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-add-google-as-an-oauth2-identity-provider-using-custom-policies"></a><span data-ttu-id="bfe5b-103">Usługa Azure Active Directory B2C: Dodawanie Google + funkcję dostawcy tożsamości OAuth2 przy użyciu zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="bfe5b-103">Azure Active Directory B2C: Add Google+ as an OAuth2 identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="bfe5b-104">W tym przewodniku przedstawiono sposób tooenable logowania użytkowników z konta Google + przy użyciu hello [niestandardowych zasad](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="bfe5b-104">This guide shows you how tooenable sign-in for users from Google+ account through hello use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfe5b-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bfe5b-105">Prerequisites</span></span>

<span data-ttu-id="bfe5b-106">Zakończenie hello etapami hello [wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-106">Complete hello steps in hello [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="bfe5b-107">Kroki te obejmują:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-107">These steps include:</span></span>

1.  <span data-ttu-id="bfe5b-108">Tworzenie aplikacji konto Google +.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-108">Creating a Google+ account application.</span></span>
2.  <span data-ttu-id="bfe5b-109">Dodawanie hello Google + konto aplikacji klucza tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bfe5b-109">Adding hello Google+ account application key tooAzure AD B2C</span></span>
3.  <span data-ttu-id="bfe5b-110">Dodawanie zasad tooa dostawcy oświadczeń</span><span class="sxs-lookup"><span data-stu-id="bfe5b-110">Adding claims provider tooa policy</span></span>
4.  <span data-ttu-id="bfe5b-111">Rejestrowanie hello Google + konto oświadczeń dostawcy tooa użytkownika podróży</span><span class="sxs-lookup"><span data-stu-id="bfe5b-111">Registering hello Google+ account claims provider tooa user journey</span></span>
5.  <span data-ttu-id="bfe5b-112">Przekazywanie hello tooan zasad usługi Azure AD B2C dzierżawy i przetestować go</span><span class="sxs-lookup"><span data-stu-id="bfe5b-112">Uploading hello policy tooan Azure AD B2C tenant and test it</span></span>

## <a name="create-a-google-account-application"></a><span data-ttu-id="bfe5b-113">Tworzenie aplikacji konto Google +</span><span class="sxs-lookup"><span data-stu-id="bfe5b-113">Create a Google+ account application</span></span>
<span data-ttu-id="bfe5b-114">toouse Google + jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji Google + i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-114">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="bfe5b-115">Możesz zarejestrować Google + aplikacją w tym miejscu: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span><span class="sxs-lookup"><span data-stu-id="bfe5b-115">You can register a Google+ application here: [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp)</span></span>

1.  <span data-ttu-id="bfe5b-116">Przejdź toohello [konsoli deweloperów Google](https://console.developers.google.com/) i zaloguj się przy użyciu poświadczeń konta Google +.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-116">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2.  <span data-ttu-id="bfe5b-117">Kliknij przycisk **Tworzenie projektu**, wprowadź **Nazwa projektu**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-117">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>

3.  <span data-ttu-id="bfe5b-118">Polecenie hello **menu projekty**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-118">Click on hello **Projects menu**.</span></span>

    ![Google + konto — wybierz projekt](media/active-directory-b2c-custom-setup-goog-idp/goog-add-new-app1.png)

4.  <span data-ttu-id="bfe5b-120">Polecenie hello  **+**  przycisku.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-120">Click on hello **+** button.</span></span>

    ![Google + konto — Utwórz nowy projekt](media/active-directory-b2c-custom-setup-goog-idp//goog-add-new-app2.png)

5.  <span data-ttu-id="bfe5b-122">Wprowadź **Nazwa projektu**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-122">Enter a **Project name**, and then click **Create**.</span></span>

    ![Google + konto — nowy projekt](media/active-directory-b2c-custom-setup-goog-idp//goog-app-name.png)

6.  <span data-ttu-id="bfe5b-124">Poczekaj, aż projekt hello jest gotowy, a następnie kliknij przycisk na powitania **menu projekty**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-124">Wait until hello project is ready and click on hello **Projects menu**.</span></span>

    ![Zaczekaj, aż nowy projekt jest gotowy toouse Google + konto-](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app1.png)

7.  <span data-ttu-id="bfe5b-126">Kliknij nazwę projektu.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-126">Click on your project name.</span></span>

    ![Google + konto - hello wybierz nowy projekt](media/active-directory-b2c-custom-setup-goog-idp//goog-select-app2.png)

8.  <span data-ttu-id="bfe5b-128">Kliknij przycisk **Menedżer interfejsu API** , a następnie kliknij przycisk **poświadczenia** w hello lewy pasek nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-128">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
9.  <span data-ttu-id="bfe5b-129">Kliknij przycisk hello **ekranu zgoda OAuth** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-129">Click hello **OAuth consent screen** tab at hello top.</span></span>

    ![Google + konto — Ustaw OAuth zgody ekranu](media/active-directory-b2c-custom-setup-goog-idp/goog-add-cred.png)

10.  <span data-ttu-id="bfe5b-131">Wybierz lub określ prawidłowe **adres E-mail**, podaj **nazwa produktu**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-131">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>

    ![Google + - poświadczeń aplikacji](media/active-directory-b2c-custom-setup-goog-idp/goog-consent-screen.png)

11.  <span data-ttu-id="bfe5b-133">Kliknij przycisk **nowe poświadczenia** , a następnie wybierz **identyfikator klienta OAuth**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-133">Click **New credentials** and then choose **OAuth client ID**.</span></span>

    ![Google + - Utwórz nowe poświadczenia aplikacji](media/active-directory-b2c-custom-setup-goog-idp/goog-add-oauth2-client-id.png)

12.  <span data-ttu-id="bfe5b-135">W obszarze **typu aplikacji**, wybierz pozycję **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-135">Under **Application type**, select **Web application**.</span></span>

    ![Google + — Wybieranie typu aplikacji](media/active-directory-b2c-custom-setup-goog-idp/goog-web-app.png)

13.  <span data-ttu-id="bfe5b-137">Podaj **nazwa** dla aplikacji, wprowadź `https://login.microsoftonline.com` w hello **źródeł autoryzowany JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **autoryzowanych przekierowania URI**pola.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-137">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="bfe5b-138">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="bfe5b-138">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="bfe5b-139">Witaj **{dzierżawa}** wartość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-139">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="bfe5b-140">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-140">Click **Create**.</span></span>

    ![Google + - zapewniają autoryzację JavaScript źródeł i Przekierowanie URI](media/active-directory-b2c-custom-setup-goog-idp/goog-create-client-id.png)

14.  <span data-ttu-id="bfe5b-142">Skopiuj wartości hello **identyfikator klienta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-142">Copy hello values of **Client Id** and **Client secret**.</span></span> <span data-ttu-id="bfe5b-143">Należy obu tooconfigure Google + funkcję dostawcy tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-143">You need both tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="bfe5b-144">**Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-144">**Client secret** is an important security credential.</span></span>

    ![Google + - wartości hello kopii klucza tajnego identyfikator i klienta klienta](media/active-directory-b2c-custom-setup-goog-idp/goog-client-secret.png)

## <a name="add-hello-google-account-application-key-tooazure-ad-b2c"></a><span data-ttu-id="bfe5b-146">Dodaj hello Google + konto aplikacji klucza tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="bfe5b-146">Add hello Google+ account application key tooAzure AD B2C</span></span>
<span data-ttu-id="bfe5b-147">Federacja z konta Google + wymaga klucz tajny klienta konta Google + tootrust usługi Azure AD B2C w imieniu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-147">Federation with Google+ accounts requires a client secret for Google+ account tootrust Azure AD B2C on behalf of hello application.</span></span> <span data-ttu-id="bfe5b-148">Należy toostore Twojego Google + klucz tajny aplikacji w dzierżawie usługi Azure AD B2C:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-148">You need toostore your Google+ application secret in Azure AD B2C tenant:</span></span>  

1.  <span data-ttu-id="bfe5b-149">Przejdź do dzierżawy usługi Azure AD B2C tooyour i wybierz **ustawieniami B2C** > **Framework obsługi tożsamości**</span><span class="sxs-lookup"><span data-stu-id="bfe5b-149">Go tooyour Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="bfe5b-150">Wybierz **zasad kluczy** klawiszy hello tooview dostępnych w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-150">Select **Policy Keys** tooview hello keys available in your tenant.</span></span>
3.  <span data-ttu-id="bfe5b-151">Kliknij przycisk **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-151">Click **+Add**.</span></span>
4.  <span data-ttu-id="bfe5b-152">Aby uzyskać **opcje**, użyj **ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-152">For **Options**, use **Manual**.</span></span>
5.  <span data-ttu-id="bfe5b-153">Aby uzyskać **nazwa**, użyj `GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-153">For **Name**, use `GoogleSecret`.</span></span>  
    <span data-ttu-id="bfe5b-154">Prefiks Hello `B2C_1A_` mogą być dodawane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-154">hello prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="bfe5b-155">W hello **klucz tajny** wprowadź klucz tajny aplikacji firmy Microsoft z https://apps.dev.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="bfe5b-155">In hello **Secret** box, enter your Microsoft application secret from https://apps.dev.microsoft.com</span></span>
7.  <span data-ttu-id="bfe5b-156">Aby uzyskać **użycie klucza**, użyj **podpisu**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-156">For **Key usage**, use **Signature**.</span></span>
8.  <span data-ttu-id="bfe5b-157">Kliknij przycisk **Utwórz**</span><span class="sxs-lookup"><span data-stu-id="bfe5b-157">Click **Create**</span></span>
9.  <span data-ttu-id="bfe5b-158">Upewnij się, że utworzono klucz hello `B2C_1A_GoogleSecret`.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-158">Confirm that you've created hello key `B2C_1A_GoogleSecret`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="bfe5b-159">Dodawanie dostawcy oświadczeń w zasadach rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="bfe5b-159">Add a claims provider in your extension policy</span></span>

<span data-ttu-id="bfe5b-160">Jeśli chcesz toosign użytkowników przy użyciu konta Google +, musisz mieć toodefine Google + konto jako dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-160">If you want users toosign in by using Google+ account, you need toodefine Google+ account as a claims provider.</span></span> <span data-ttu-id="bfe5b-161">Innymi słowy należy toospecify punktu końcowego, który komunikuje się usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-161">In other words, you need toospecify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="bfe5b-162">punkt końcowy Hello zawiera zestaw oświadczeń, które są używane przez usługi Azure AD B2C tooverify, który został uwierzytelniony określonego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-162">hello endpoint provides a set of claims that are used by Azure AD B2C tooverify that a specific user has authenticated.</span></span>

<span data-ttu-id="bfe5b-163">Zdefiniuj konto Google + jako dostawcy oświadczeń, dodając `<ClaimsProvider>` węzeł rozszerzenia pliku zasad:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-163">Define Google+ Account as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1.  <span data-ttu-id="bfe5b-164">Otwórz plik zasad rozszerzenia hello (TrustFrameworkExtensions.xml) z katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-164">Open hello extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="bfe5b-165">Jeśli potrzebujesz edytora XML [spróbuj Visual Studio Code](https://code.visualstudio.com/download), lekkie edytora i platform.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-165">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2.  <span data-ttu-id="bfe5b-166">Znajdź hello `<ClaimsProviders>` sekcji</span><span class="sxs-lookup"><span data-stu-id="bfe5b-166">Find hello `<ClaimsProviders>` section</span></span>
3.  <span data-ttu-id="bfe5b-167">Dodaj następujące fragment kodu XML w obszarze hello hello `ClaimsProviders` elementu i zastępowanie `client_id` wartość przy użyciu usługi Google + konto aplikacji Identyfikatora klienta przed zapisaniem pliku hello.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-167">Add hello following XML snippet under hello `ClaimsProviders` element and replace `client_id` value with your Google+ account application client ID before saving hello file.</span></span>  

```xml
<ClaimsProvider>
    <Domain>google.com</Domain>
    <DisplayName>Google</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Google-OAUTH">
        <DisplayName>Google</DisplayName>
        <Protocol Name="OAuth2" />
        <Metadata>
        <Item Key="ProviderName">google</Item>
        <Item Key="authorization_endpoint">https://accounts.google.com/o/oauth2/auth</Item>
        <Item Key="AccessTokenEndpoint">https://accounts.google.com/o/oauth2/token</Item>
        <Item Key="ClaimsEndpoint">https://www.googleapis.com/oauth2/v1/userinfo</Item>
        <Item Key="scope">email</Item>
        <Item Key="HttpBinding">POST</Item>
        <Item Key="UsePolicyInRedirectUri">0</Item>
        <Item Key="client_id">Your Google+ application ID</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="client_secret" StorageReferenceId="B2C_1A_GoogleSecret" />
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="id" />
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name" />
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name" />
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name" />
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="google.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication" />
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName" />
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName" />
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId" />
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId" />
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-SocialLogin" />
        <ErrorHandlers>
        <ErrorHandler>
            <ErrorResponseFormat>json</ErrorResponseFormat>
            <ResponseMatch>$[?(@@.error == 'invalid_grant')]</ResponseMatch>
            <Action>Reauthenticate</Action>
            <!--In case of authorization code used error, we don't want hello user tooselect his account again.-->
            <!--AdditionalRequestParameters Key="prompt">select_account</AdditionalRequestParameters-->
        </ErrorHandler>
        </ErrorHandlers>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-hello-google-account-claims-provider-toosign-up-or-sign-in-user-journey"></a><span data-ttu-id="bfe5b-168">Zarejestruj hello Google + konto oświadczeń dostawcy tooSign się lub zaloguj się w podróży użytkownika</span><span class="sxs-lookup"><span data-stu-id="bfe5b-168">Register hello Google+ account claims provider tooSign up or Sign in user journey</span></span>

<span data-ttu-id="bfe5b-169">Dostawca tożsamości Hello nie został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-169">hello identity provider has been set up.</span></span>  <span data-ttu-id="bfe5b-170">Jednak nie jest dostępna w żadnym hello konta-konta/logowania ekranów.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-170">However, it is not available in any of hello sign-up/sign-in screens.</span></span> <span data-ttu-id="bfe5b-171">Dodaj hello Google + konto tożsamości użytkownika dostawcy usług tooyour `SignUpOrSignIn` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-171">Add hello Google+ account identity provider tooyour user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="bfe5b-172">toomake ją, utworzymy duplikatem istniejącej przebieg użytkownika szablonu.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-172">toomake it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="bfe5b-173">Następnie dodaj hello Google + dostawcy tożsamości konta:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-173">Then we add hello Google+ account identity provider:</span></span>

>[!NOTE]
>
><span data-ttu-id="bfe5b-174">Jeśli został skopiowany hello `<UserJourneys>` elementu z pliku podstawowego zasad toohello rozszerzenie pliku (TrustFrameworkExtensions.xml), możesz pominąć toothis sekcję.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-174">If you copied hello `<UserJourneys>` element from base file of your policy toohello extension file (TrustFrameworkExtensions.xml), you can skip toothis section.</span></span>

1.  <span data-ttu-id="bfe5b-175">Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="bfe5b-175">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="bfe5b-176">Znajdź hello `<UserJourneys>` element kopiowania hello całej zawartości i `<UserJourneys>` węzła.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-176">Find hello `<UserJourneys>` element and copy hello entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="bfe5b-177">Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml) i Znajdź hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-177">Open hello extension file (for example, TrustFrameworkExtensions.xml) and find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="bfe5b-178">Jeśli hello element nie istnieje, dodaj je.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-178">If hello element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="bfe5b-179">Wklej zawartość całego hello `<UserJournesy>` węzła, który został skopiowany jako element podrzędny hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-179">Paste hello entire content of `<UserJournesy>` node that you copied as a child of hello `<UserJourneys>` element.</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="bfe5b-180">Przycisk hello wyświetlania</span><span class="sxs-lookup"><span data-stu-id="bfe5b-180">Display hello button</span></span>
<span data-ttu-id="bfe5b-181">Witaj `<ClaimsProviderSelections>` element definiuje listę hello opcje wyboru dostawcy oświadczeń i ich kolejność.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-181">hello `<ClaimsProviderSelections>` element defines hello list of claims provider selection options and their order.</span></span>  <span data-ttu-id="bfe5b-182">`<ClaimsProviderSelection>`element jest przycisku dostawcy tożsamości analogiczne tooan na stronie konta-konta/logowania.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-182">`<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="bfe5b-183">Jeśli dodasz `<ClaimsProviderSelection>` elementu dla konta Google + nowy przycisk zostaną wyświetlone po wyładowuje użytkownika na stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-183">If you add a `<ClaimsProviderSelection>` element for Google+ account, a new button shows up when a user lands on hello page.</span></span> <span data-ttu-id="bfe5b-184">tooadd tego elementu:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-184">tooadd this element:</span></span>

1.  <span data-ttu-id="bfe5b-185">Znajdź hello `<UserJourney>` węzła, który zawiera `Id="SignUpOrSignIn"` w podróży użytkownika hello, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-185">Find hello `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in hello user journey that you copied.</span></span>
2.  <span data-ttu-id="bfe5b-186">Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="bfe5b-186">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="bfe5b-187">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-187">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="bfe5b-188">Akcja tooan przycisku hello łącza</span><span class="sxs-lookup"><span data-stu-id="bfe5b-188">Link hello button tooan action</span></span>
<span data-ttu-id="bfe5b-189">Teraz, gdy masz przycisku w miejscu, należy toolink go tooan akcji.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-189">Now that you have a button in place, you need toolink it tooan action.</span></span> <span data-ttu-id="bfe5b-190">Akcja Hello jest dla usługi Azure AD B2C toocommunicate z tooreceive konto Google + w takim przypadku tokenu.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-190">hello action, in this case, is for Azure AD B2C toocommunicate with Google+ account tooreceive a token.</span></span>

1.  <span data-ttu-id="bfe5b-191">Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-191">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="bfe5b-192">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-192">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

>[!NOTE]
>
> * <span data-ttu-id="bfe5b-193">Upewnij się, hello `Id` ma takie same wartości jak hello `TargetClaimsExchangeId` w powyższej sekcji hello</span><span class="sxs-lookup"><span data-stu-id="bfe5b-193">Ensure hello `Id` has hello same value as that of `TargetClaimsExchangeId` in hello preceding section</span></span>
> * <span data-ttu-id="bfe5b-194">Upewnij się, `TechnicalProfileReferenceId` ustawiono Identyfikatora profilu techniczne toohello utworzonego wcześniej (Google-OAUTH).</span><span class="sxs-lookup"><span data-stu-id="bfe5b-194">Ensure `TechnicalProfileReferenceId` ID is set toohello technical profile you created earlier (Google-OAUTH).</span></span>

## <a name="upload-hello-policy-tooyour-tenant"></a><span data-ttu-id="bfe5b-195">Przekaż hello zasad tooyour dzierżawy</span><span class="sxs-lookup"><span data-stu-id="bfe5b-195">Upload hello policy tooyour tenant</span></span>
1.  <span data-ttu-id="bfe5b-196">W hello [portalu Azure](https://portal.azure.com), przejdź do hello [kontekstu dzierżawy usługi Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md)i otwórz hello **usługi Azure AD B2C** bloku.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-196">In hello [Azure portal](https://portal.azure.com), switch into hello [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open hello **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="bfe5b-197">Wybierz **Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-197">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="bfe5b-198">Otwórz hello **wszystkie zasady** bloku.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-198">Open hello **All Policies** blade.</span></span>
4.  <span data-ttu-id="bfe5b-199">Wybierz **przekazywać zasady**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-199">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="bfe5b-200">Sprawdź **zastąpić hello zasady, jeśli istnieje** pole.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-200">Check **Overwrite hello policy if it exists** box.</span></span>
6.  <span data-ttu-id="bfe5b-201">**Przekaż** TrustFrameworkExtensions.xml i upewnij się, że nie wystąpi niepowodzenie weryfikacji hello</span><span class="sxs-lookup"><span data-stu-id="bfe5b-201">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail hello validation</span></span>

## <a name="test-hello-custom-policy-by-using-run-now"></a><span data-ttu-id="bfe5b-202">Testowanie zasad niestandardowych hello przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="bfe5b-202">Test hello custom policy by using Run Now</span></span>
1.  <span data-ttu-id="bfe5b-203">Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-203">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>

    >[!NOTE]
    >
    >    <span data-ttu-id="bfe5b-204">**Uruchom teraz** wymaga co najmniej jedną aplikację toobe preregistered hello dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-204">**Run now** requires at least one application toobe preregistered on hello tenant.</span></span> 
    >    <span data-ttu-id="bfe5b-205">toolearn tooregister aplikacji, zobacz temat hello Azure AD B2C [wprowadzenie](active-directory-b2c-get-started.md) artykułu lub hello [Rejestracja aplikacji](active-directory-b2c-app-registration.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-205">toolearn how tooregister applications, see hello Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or hello [Application registration](active-directory-b2c-app-registration.md) article.</span></span>


2.  <span data-ttu-id="bfe5b-206">Otwórz **B2C_1A_signup_signin**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-206">Open **B2C_1A_signup_signin**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="bfe5b-207">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-207">Select **Run now**.</span></span>
3.  <span data-ttu-id="bfe5b-208">Powinno być możliwe toosign za pomocą konta Google +.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-208">You should be able toosign in using Google+ account.</span></span>

## <a name="optional-register-hello-google-account-claims-provider-tooprofile-edit-user-journey"></a><span data-ttu-id="bfe5b-209">[Opcjonalnie] Zarejestruj hello Google + konto oświadczeń dostawcy tooProfile Edycja użytkownika podróży</span><span class="sxs-lookup"><span data-stu-id="bfe5b-209">[Optional] Register hello Google+ account claims provider tooProfile-Edit user journey</span></span>
<span data-ttu-id="bfe5b-210">Możesz tooadd hello Google + konto dostawcy tożsamości również użytkownika tooyour `ProfileEdit` podróży użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-210">You may want tooadd hello Google+ account identity provider also tooyour user `ProfileEdit` user journey.</span></span> <span data-ttu-id="bfe5b-211">toomake ją, powtórz firma Microsoft hello ostatnie dwa kroki:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-211">toomake it available, we repeat hello last two steps:</span></span>

### <a name="display-hello-button"></a><span data-ttu-id="bfe5b-212">Przycisk hello wyświetlania</span><span class="sxs-lookup"><span data-stu-id="bfe5b-212">Display hello button</span></span>
1.  <span data-ttu-id="bfe5b-213">Otwórz plik rozszerzenia hello zasad (na przykład TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="bfe5b-213">Open hello extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="bfe5b-214">Znajdź hello `<UserJourney>` węzła, który zawiera `Id="ProfileEdit"` w podróży użytkownika hello, które zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-214">Find hello `<UserJourney>` node that includes `Id="ProfileEdit"` in hello user journey that you copied.</span></span>
3.  <span data-ttu-id="bfe5b-215">Zlokalizuj hello `<OrchestrationStep>` węzła, który zawiera`Order="1"`</span><span class="sxs-lookup"><span data-stu-id="bfe5b-215">Locate hello `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="bfe5b-216">Dodaj następujący fragment kodu XML w obszarze `<ClaimsProviderSelections>` węzła:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-216">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="GoogleExchange" />
```

### <a name="link-hello-button-tooan-action"></a><span data-ttu-id="bfe5b-217">Akcja tooan przycisku hello łącza</span><span class="sxs-lookup"><span data-stu-id="bfe5b-217">Link hello button tooan action</span></span>
1.  <span data-ttu-id="bfe5b-218">Znajdź hello `<OrchestrationStep>` zawierającą `Order="2"` w hello `<UserJourney>` węzła.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-218">Find hello `<OrchestrationStep>` that includes `Order="2"` in hello `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="bfe5b-219">Dodaj następujący fragment kodu XML w obszarze `<ClaimsExchanges>` węzła:</span><span class="sxs-lookup"><span data-stu-id="bfe5b-219">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="GoogleExchange" TechnicalProfileReferenceId="Google-OAUTH" />
```

### <a name="test-hello-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="bfe5b-220">Testowanie zasad niestandardowych edycji profilu hello przy użyciu Uruchom teraz</span><span class="sxs-lookup"><span data-stu-id="bfe5b-220">Test hello custom Profile-Edit policy by using Run Now</span></span>

1.  <span data-ttu-id="bfe5b-221">Otwórz **ustawienia usługi Azure AD B2C** i przejść za**Framework obsługi tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-221">Open **Azure AD B2C Settings** and go too**Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="bfe5b-222">Otwórz **B2C_1A_ProfileEdit**, hello jednostki uzależnionej zasady niestandardowe strony (RP), który został przekazany.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-222">Open **B2C_1A_ProfileEdit**, hello relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="bfe5b-223">Wybierz **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-223">Select **Run now**.</span></span>
3.  <span data-ttu-id="bfe5b-224">Powinno być możliwe toosign za pomocą konta Google +.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-224">You should be able toosign in using Google+ account.</span></span>

## <a name="download-hello-complete-policy-files"></a><span data-ttu-id="bfe5b-225">Pobierz pliki zasad pełną hello</span><span class="sxs-lookup"><span data-stu-id="bfe5b-225">Download hello complete policy files</span></span>
<span data-ttu-id="bfe5b-226">Opcjonalnie: Zaleca się tworzenie scenariusz przy użyciu własnych niestandardowych zasad plików po zakończeniu hello wprowadzenie zasady niestandardowe przeprowadzenie zamiast te przykładowe pliki.</span><span class="sxs-lookup"><span data-stu-id="bfe5b-226">Optional: We recommend you build your scenario using your own Custom policy files after completing hello Getting Started with Custom Policies walk through instead of using these sample files.</span></span>  [<span data-ttu-id="bfe5b-227">Przykładowe pliki zasad dla odwołania</span><span class="sxs-lookup"><span data-stu-id="bfe5b-227">Sample policy files for reference</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-goog-app)
