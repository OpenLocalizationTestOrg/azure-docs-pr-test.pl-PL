---
title: "Usługa Azure Active Directory B2C: Dodawanie dostawcy usług Salesforce SAML za pomocą niestandardowych zasad | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o toocreate zasad niestandardowych usługi Azure Active Directory B2C i zarządzanie nimi."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d7f4143f-cd7c-4939-91a8-231a4104dc2c
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/11/2017
ms.author: parakhj
ms.openlocfilehash: f14c9d96980ff124110db7cfb58bf7cd81750b7c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="41250-103">Usługa Azure Active Directory B2C: Zaloguj się przy użyciu konta usług Salesforce za pośrednictwem SAML</span><span class="sxs-lookup"><span data-stu-id="41250-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="41250-104">W tym artykule opisano sposób toouse [zasady niestandardowe](active-directory-b2c-overview-custom.md) tooset się logowania użytkowników z określonych organizacji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="41250-104">This article shows you how toouse [custom policies](active-directory-b2c-overview-custom.md) tooset up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41250-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="41250-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="41250-106">Instalacja usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="41250-106">Azure AD B2C setup</span></span>

<span data-ttu-id="41250-107">Upewnij się, że zostały wykonane wszystkie kroki hello, przedstawiających sposób zbyt[wprowadzenie do zasad niestandardowych](active-directory-b2c-get-started-custom.md) w usłudze Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="41250-107">Ensure that you have completed all of hello steps that show you how too[get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="41250-108">Należą do nich:</span><span class="sxs-lookup"><span data-stu-id="41250-108">These include:</span></span>

* <span data-ttu-id="41250-109">Tworzenie dzierżawy usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41250-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="41250-110">Tworzenie aplikacji usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41250-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="41250-111">Zarejestruj dwie aplikacje aparatu zasad.</span><span class="sxs-lookup"><span data-stu-id="41250-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="41250-112">Konfigurowanie kluczy.</span><span class="sxs-lookup"><span data-stu-id="41250-112">Set up keys.</span></span>
* <span data-ttu-id="41250-113">Konfigurowanie hello początkowego pakietu.</span><span class="sxs-lookup"><span data-stu-id="41250-113">Set up hello starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="41250-114">Instalator usług SalesForce</span><span class="sxs-lookup"><span data-stu-id="41250-114">Salesforce setup</span></span>

<span data-ttu-id="41250-115">W tym artykule przyjęto założenie, jeszcze hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="41250-115">In this article, we assume that you have already done hello following:</span></span>

* <span data-ttu-id="41250-116">Konta konta usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="41250-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="41250-117">Możesz zarejestrować się w celu [bezpłatne konto Developer Edition](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="41250-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="41250-118">[Konfigurowanie domeny Moje](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) organizacji Salesforce.</span><span class="sxs-lookup"><span data-stu-id="41250-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="41250-119">Konfigurowanie usług Salesforce, umożliwiające użytkownikom można było wykonać Federację</span><span class="sxs-lookup"><span data-stu-id="41250-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="41250-120">toohelp usługi Azure AD B2C komunikować się z usług Salesforce, należy tooget hello Salesforce metadanych z adresu URL.</span><span class="sxs-lookup"><span data-stu-id="41250-120">toohelp Azure AD B2C communicate with Salesforce, you need tooget hello Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="41250-121">Konfigurowanie usług Salesforce jako dostawca tożsamości</span><span class="sxs-lookup"><span data-stu-id="41250-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="41250-122">W tym artykule przyjęto założenie, używane są [Salesforce Lightning środowisko](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="41250-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="41250-123">[Zaloguj się tooSalesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="41250-123">[Sign in tooSalesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="41250-124">Na powitania pozostałych menu, w obszarze **ustawienia**, rozwiń węzeł **tożsamości**, a następnie kliknij przycisk **dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="41250-124">On hello left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="41250-125">Kliknij przycisk **włączenia dostawcy tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="41250-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="41250-126">W obszarze **certyfikatu wybierz hello**, wybierz pozycję hello certyfikatów, które mają toocommunicate toouse Salesforce w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41250-126">Under **Select hello certificate**, select hello certificate you want Salesforce toouse toocommunicate with Azure AD B2C.</span></span> <span data-ttu-id="41250-127">(Możesz użyć hello domyślnego certyfikatu). Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="41250-127">(You can use hello default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="41250-128">Tworzenie połączonej aplikacji w usłudze Salesforce</span><span class="sxs-lookup"><span data-stu-id="41250-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="41250-129">Na powitania **dostawcy tożsamości** strony znajduje się zbyt**usługodawców**.</span><span class="sxs-lookup"><span data-stu-id="41250-129">On hello **Identity Provider** page, go too**Service Providers**.</span></span>
2. <span data-ttu-id="41250-130">Kliknij przycisk **usługodawców zostaną utworzone za pośrednictwem połączenia aplikacji. Kliknij tutaj.**</span><span class="sxs-lookup"><span data-stu-id="41250-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="41250-131">W obszarze **podstawowe informacje**, wprowadź wartości hello wymagane dla połączonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41250-131">Under **Basic Information**,  enter hello required values for your connected app.</span></span>
4. <span data-ttu-id="41250-132">W obszarze **ustawień aplikacji sieci Web**, wybierz pozycję hello **Włącz SAML** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="41250-132">Under **Web App Settings**, select hello **Enable SAML** check box.</span></span>
5. <span data-ttu-id="41250-133">W hello **identyfikator jednostki** wprowadź hello następującego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="41250-133">In hello **Entity ID** field, enter hello following URL.</span></span> <span data-ttu-id="41250-134">Upewnij się, czy zastąpić wartość hello `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="41250-134">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="41250-135">W hello **adres URL usługi ACS** wprowadź hello następującego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="41250-135">In hello **ACS URL** field, enter hello following URL.</span></span> <span data-ttu-id="41250-136">Upewnij się, czy zastąpić wartość hello `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="41250-136">Ensure that you replace hello value for `tenantName`.</span></span>
      ```
      https://login.microsoftonline.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="41250-137">Pozostaw hello wartości domyślne dla wszystkich innych ustawień.</span><span class="sxs-lookup"><span data-stu-id="41250-137">Leave hello default values for all other settings.</span></span>
8. <span data-ttu-id="41250-138">Przewiń toohello dolnej części listy hello, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="41250-138">Scroll toohello bottom of hello list, and then click **Save**.</span></span>

### <a name="get-hello-metadata-url"></a><span data-ttu-id="41250-139">Pobierz adres URL metadanych hello</span><span class="sxs-lookup"><span data-stu-id="41250-139">Get hello metadata URL</span></span>

1. <span data-ttu-id="41250-140">Na stronie Przegląd hello połączonych aplikacji, kliknij przycisk **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="41250-140">On hello overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="41250-141">Skopiuj wartość hello **punkt końcowy odnajdowania metadanych**, a następnie zapisz je.</span><span class="sxs-lookup"><span data-stu-id="41250-141">Copy hello value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="41250-142">Będzie on używany w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="41250-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-toofederate"></a><span data-ttu-id="41250-143">Konfigurowanie usług Salesforce toofederate użytkowników</span><span class="sxs-lookup"><span data-stu-id="41250-143">Set up Salesforce users toofederate</span></span>

1. <span data-ttu-id="41250-144">Na powitania **Zarządzaj** strony połączonych aplikacji, przejdź zbyt**profile**.</span><span class="sxs-lookup"><span data-stu-id="41250-144">On hello **Manage** page of your connected app, go too**Profiles**.</span></span>
2. <span data-ttu-id="41250-145">Kliknij przycisk **zarządzania profilami**.</span><span class="sxs-lookup"><span data-stu-id="41250-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="41250-146">Wybierz profile hello (lub grupom użytkowników), które mają toofederate z usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41250-146">Select hello profiles (or groups of users) that you want toofederate with Azure AD B2C.</span></span> <span data-ttu-id="41250-147">Administrator systemu, wybierz hello **administratorem** Sprawdź okno, tak aby można było wykonać Federację przy użyciu konta usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="41250-147">As a system administrator, select hello **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="41250-148">Generuj certyfikat podpisywania dla usługi Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="41250-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="41250-149">Żądania wysyłane toobe potrzeby tooSalesforce podpisanego przez usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41250-149">Requests sent tooSalesforce need toobe signed by Azure AD B2C.</span></span> <span data-ttu-id="41250-150">toogenerate certyfikatu podpisywania, Otwórz program Azure PowerShell, a następnie uruchom następujące polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="41250-150">toogenerate a signing certificate, open Azure PowerShell, and then run hello following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="41250-151">Upewnij się, należy zaktualizować hello dzierżawy nazwy i hasła w hello top dwa wiersze.</span><span class="sxs-lookup"><span data-stu-id="41250-151">Make sure that you update hello tenant name and password in hello top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-hello-saml-signing-certificate-tooazure-ad-b2c"></a><span data-ttu-id="41250-152">Dodaj hello SAML podpisywania certyfikatu tooAzure AD B2C</span><span class="sxs-lookup"><span data-stu-id="41250-152">Add hello SAML signing certificate tooAzure AD B2C</span></span>

<span data-ttu-id="41250-153">Przekaż hello dzierżawy usługi Azure AD B2C tooyour certyfikatu podpisywania:</span><span class="sxs-lookup"><span data-stu-id="41250-153">Upload hello signing certificate tooyour Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="41250-154">Przejdź dzierżawy tooyour usługi Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41250-154">Go tooyour Azure AD B2C tenant.</span></span> <span data-ttu-id="41250-155">Kliknij przycisk **ustawienia** > **Framework obsługi tożsamości** > **klucze zasad**.</span><span class="sxs-lookup"><span data-stu-id="41250-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="41250-156">Kliknij przycisk **+ Dodaj**, a następnie:</span><span class="sxs-lookup"><span data-stu-id="41250-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="41250-157">Kliknij przycisk **opcje** > **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="41250-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="41250-158">Wprowadź **nazwa** (na przykład SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="41250-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="41250-159">Prefiks Hello *B2C_1A_* zostanie automatycznie dodana nazwę toohello klucza.</span><span class="sxs-lookup"><span data-stu-id="41250-159">hello prefix *B2C_1A_* is automatically added toohello name of your key.</span></span>
    3. <span data-ttu-id="41250-160">tooselect certyfikat, wybierz opcję **przekazać formant pliku**.</span><span class="sxs-lookup"><span data-stu-id="41250-160">tooselect your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="41250-161">Wprowadź hasło certyfikatu hello ustawione w skrypcie programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="41250-161">Enter hello certificate's password that you set in hello PowerShell script.</span></span>
3. <span data-ttu-id="41250-162">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="41250-162">Click **Create**.</span></span>
4. <span data-ttu-id="41250-163">Sprawdź, czy utworzono klucz (na przykład B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="41250-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="41250-164">Zwróć uwagę na powitania Pełna nazwa (włącznie z *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="41250-164">Take note of hello full name (including *B2C_1A_*).</span></span> <span data-ttu-id="41250-165">Będzie można znaleźć klucza toothis później w zasadach hello.</span><span class="sxs-lookup"><span data-stu-id="41250-165">You will refer toothis key later in hello policy.</span></span>

## <a name="create-hello-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="41250-166">Utwórz hello Salesforce SAML dostawcy oświadczeń w zasadach podstawowej</span><span class="sxs-lookup"><span data-stu-id="41250-166">Create hello Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="41250-167">Należy toodefine Salesforce jako dostawcy oświadczeń, użytkownicy mogą zarejestrować się przy użyciu Salesforce.</span><span class="sxs-lookup"><span data-stu-id="41250-167">You need toodefine Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="41250-168">Innymi słowy należy punktu końcowego hello toospecify, który usługi Azure AD B2C będzie komunikować się z.</span><span class="sxs-lookup"><span data-stu-id="41250-168">In other words, you need toospecify hello endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="41250-169">punkt końcowy Hello będzie *podaj* zestaw *oświadczeń* używany tooverify, do którego określony użytkownik został uwierzytelniony w usłudze Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="41250-169">hello endpoint will *provide* a set of *claims* that Azure AD B2C uses tooverify that a specific user has authenticated.</span></span> <span data-ttu-id="41250-170">toodo, Dodaj `<ClaimsProvider>` dla usług Salesforce w hello rozszerzenia pliku zasad:</span><span class="sxs-lookup"><span data-stu-id="41250-170">toodo this, add a `<ClaimsProvider>` for Salesforce in hello extension file of your policy:</span></span>

1. <span data-ttu-id="41250-171">W katalogu roboczym otwórz plik rozszerzenia hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="41250-171">In your working directory, open hello extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="41250-172">Znajdź hello `<ClaimsProviders>` sekcji.</span><span class="sxs-lookup"><span data-stu-id="41250-172">Find hello `<ClaimsProviders>` section.</span></span> <span data-ttu-id="41250-173">Jeśli nie istnieje, utwórz je w węźle głównym hello.</span><span class="sxs-lookup"><span data-stu-id="41250-173">If it does not exist, create it under hello root node.</span></span>
3. <span data-ttu-id="41250-174">Dodaj nową `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="41250-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="externalIdp"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

<span data-ttu-id="41250-175">W obszarze hello `<ClaimsProvider>` węzła:</span><span class="sxs-lookup"><span data-stu-id="41250-175">Under hello `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="41250-176">Zmień wartość hello `<Domain>` tooa unikatowa wartość odróżniająca `<ClaimsProvider>` od innych dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="41250-176">Change hello value for `<Domain>` tooa unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="41250-177">Zaktualizuj wartość hello `<DisplayName>` tooa nazwę wyświetlaną hello dostawcy oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="41250-177">Update hello value for `<DisplayName>` tooa display name for hello claims provider.</span></span> <span data-ttu-id="41250-178">Ta wartość nie jest obecnie używana.</span><span class="sxs-lookup"><span data-stu-id="41250-178">Currently, this value is not used.</span></span>

### <a name="update-hello-technical-profile"></a><span data-ttu-id="41250-179">Aktualizuj profil techniczne hello</span><span class="sxs-lookup"><span data-stu-id="41250-179">Update hello technical profile</span></span>

<span data-ttu-id="41250-180">tooget tokenu SAML z usług Salesforce, zdefiniuj protokołów hello Azure AD B2C będzie używać toocommunicate z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="41250-180">tooget a SAML token from Salesforce, define hello protocols that Azure AD B2C will use toocommunicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="41250-181">To zrobić w hello `<TechnicalProfile>` elementu `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="41250-181">Do this in hello `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="41250-182">Aktualizacja Identyfikatora hello hello `<TechnicalProfile>` węzła.</span><span class="sxs-lookup"><span data-stu-id="41250-182">Update hello ID of hello `<TechnicalProfile>` node.</span></span> <span data-ttu-id="41250-183">Ten identyfikator jest używane toorefer toothis techniczne profil z innymi częściami hello zasad.</span><span class="sxs-lookup"><span data-stu-id="41250-183">This ID is used toorefer toothis technical profile from other parts of hello policy.</span></span>
2. <span data-ttu-id="41250-184">Zaktualizuj wartość hello `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="41250-184">Update hello value for `<DisplayName>`.</span></span> <span data-ttu-id="41250-185">Ta wartość jest wyświetlana na powitania przycisk Zarejestruj się na stronie logowania.</span><span class="sxs-lookup"><span data-stu-id="41250-185">This value is displayed on hello sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="41250-186">Zaktualizuj wartość hello `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="41250-186">Update hello value for `<Description>`.</span></span>
4. <span data-ttu-id="41250-187">Usługa SalesForce używa protokołu hello SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="41250-187">Salesforce uses hello SAML 2.0 protocol.</span></span> <span data-ttu-id="41250-188">Upewnij się, wartość tego hello `<Protocol>` jest **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="41250-188">Ensure that hello value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="41250-189">Aktualizacja hello `<Metadata>` części hello poprzedzających XML tooreflect hello ustawienia dla określonego konta usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="41250-189">Update hello `<Metadata>` section in hello preceding XML tooreflect hello settings for your specific Salesforce account.</span></span> <span data-ttu-id="41250-190">W hello XML zaktualizuj wartości metadanych hello:</span><span class="sxs-lookup"><span data-stu-id="41250-190">In hello XML, update hello metadata values:</span></span>

1. <span data-ttu-id="41250-191">Zaktualizuj wartość hello `<Item Key="PartnerEntity">` z hello Salesforce metadanych adresu URL skopiowanego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="41250-191">Update hello value of `<Item Key="PartnerEntity">` with hello Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="41250-192">Ma hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="41250-192">It has hello following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="41250-193">W hello `<CryptographicKeys>` sekcji aktualizacji hello wartość dla obu wystąpień `StorageReferenceId` toohello nazwa hello klucza certyfikatu podpisywania (na przykład B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="41250-193">In hello `<CryptographicKeys>` section, update hello value for both instances of `StorageReferenceId` toohello name of hello key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-hello-extension-file-for-verification"></a><span data-ttu-id="41250-194">Przekaż plik rozszerzenia hello do weryfikacji</span><span class="sxs-lookup"><span data-stu-id="41250-194">Upload hello extension file for verification</span></span>

<span data-ttu-id="41250-195">Zgodnie z zasadami został skonfigurowany tak, aby usługi Azure AD B2C wie jak toocommunicate z usług Salesforce.</span><span class="sxs-lookup"><span data-stu-id="41250-195">Your policy is now configured so that Azure AD B2C knows how toocommunicate with Salesforce.</span></span> <span data-ttu-id="41250-196">Spróbuj przekazać plik rozszerzenia hello zasad, czy nie ma żadnych problemów wykonanej do tej pory tooverify.</span><span class="sxs-lookup"><span data-stu-id="41250-196">Try uploading hello extension file of your policy, tooverify that there aren't any issues so far.</span></span> <span data-ttu-id="41250-197">tooupload hello rozszerzenia pliku zasad:</span><span class="sxs-lookup"><span data-stu-id="41250-197">tooupload hello extension file of your policy:</span></span>

1. <span data-ttu-id="41250-198">W dzierżawie usługi Azure AD B2C, przejdź do pozycji toohello **wszystkie zasady** bloku.</span><span class="sxs-lookup"><span data-stu-id="41250-198">In your Azure AD B2C tenant, go toohello **All Policies** blade.</span></span>
2. <span data-ttu-id="41250-199">Wybierz hello **zastąpić hello zasady, jeśli istnieje** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="41250-199">Select hello **Overwrite hello policy if it exists** check box.</span></span>
3. <span data-ttu-id="41250-200">Przekaż plik rozszerzenia hello (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="41250-200">Upload hello extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="41250-201">Upewnij się, że nie wystąpi niepowodzenie weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="41250-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-hello-salesforce-saml-claims-provider-tooa-user-journey"></a><span data-ttu-id="41250-202">Zarejestruj hello Salesforce SAML oświadczeń dostawcy tooa użytkownika podróży</span><span class="sxs-lookup"><span data-stu-id="41250-202">Register hello Salesforce SAML claims provider tooa user journey</span></span>

<span data-ttu-id="41250-203">Następnie dodaj hello tooone dostawca tożsamości Salesforce SAML podróży z użytkownika.</span><span class="sxs-lookup"><span data-stu-id="41250-203">Next, add hello Salesforce SAML identity provider tooone of your user journeys.</span></span> <span data-ttu-id="41250-204">W tym momencie hello dostawcy tożsamości nie został skonfigurowany, ale nie jest dostępna w żadnym z hello strony rejestracji i logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="41250-204">At this point, hello identity provider has been set up, but it’s not available on any of hello user sign-up or sign-in pages.</span></span> <span data-ttu-id="41250-205">tooadd hello tożsamości dostawcy tooa strony logowania, najpierw utwórz duplikatem istniejącej przebieg użytkownika szablonu.</span><span class="sxs-lookup"><span data-stu-id="41250-205">tooadd hello identity provider tooa sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="41250-206">Następnie należy zmodyfikować szablon hello, tak aby ma również dostawcy tożsamości usługi Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="41250-206">Then, modify hello template so that it also has hello Azure AD identity provider.</span></span>

1. <span data-ttu-id="41250-207">Otwórz plik podstawowy hello zasad (na przykład TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="41250-207">Open hello base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="41250-208">Znajdź hello `<UserJourneys>` elementu, a następnie hello kopii całego `<UserJourney>` wartość, tym Id = "SignUpOrSignIn".</span><span class="sxs-lookup"><span data-stu-id="41250-208">Find hello `<UserJourneys>` element, and then copy hello entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="41250-209">Otwórz plik rozszerzenia hello (na przykład TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="41250-209">Open hello extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="41250-210">Znajdź hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="41250-210">Find hello `<UserJourneys>` element.</span></span> <span data-ttu-id="41250-211">Jeśli hello element nie istnieje, utwórz je.</span><span class="sxs-lookup"><span data-stu-id="41250-211">If hello element doesn't exist, create one.</span></span>
4. <span data-ttu-id="41250-212">Wklej hello całego skopiowane `<UserJourney>` jako element podrzędny hello `<UserJourneys>` elementu.</span><span class="sxs-lookup"><span data-stu-id="41250-212">Paste hello entire copied `<UserJourney>` as a child of hello `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="41250-213">Zmień nazwę hello identyfikator nowego hello `<UserJourney>` (na przykład SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="41250-213">Rename hello ID of hello new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-hello-identity-provider-button"></a><span data-ttu-id="41250-214">Przycisk dostawcy tożsamości hello wyświetlania</span><span class="sxs-lookup"><span data-stu-id="41250-214">Display hello identity provider button</span></span>

<span data-ttu-id="41250-215">Witaj `<ClaimsProviderSelection>` element jest analogiczne tooan przycisk dostawcę tożsamości na stronie tworzenia konta lub logowania.</span><span class="sxs-lookup"><span data-stu-id="41250-215">hello `<ClaimsProviderSelection>` element is analogous tooan identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="41250-216">Dodając `<ClaimsProviderSelection>` elementu Salesforce, nowy przycisk jest wyświetlany, gdy użytkownik przejdzie do strony toothis.</span><span class="sxs-lookup"><span data-stu-id="41250-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes toothis page.</span></span> <span data-ttu-id="41250-217">przycisk dostawcy tożsamości hello toodisplay:</span><span class="sxs-lookup"><span data-stu-id="41250-217">toodisplay hello identity provider button:</span></span>

1. <span data-ttu-id="41250-218">W hello `<UserJourney>` utworzony, Znajdź hello `<OrchestrationStep>` z `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="41250-218">In hello `<UserJourney>` that you created, find hello `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="41250-219">Dodaj następujące XML hello:</span><span class="sxs-lookup"><span data-stu-id="41250-219">Add hello following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="41250-220">Ustaw `TargetClaimsExchangeId` tooa wartość logiczną.</span><span class="sxs-lookup"><span data-stu-id="41250-220">Set `TargetClaimsExchangeId` tooa logical value.</span></span> <span data-ttu-id="41250-221">Zaleca się następujące hello sam Konwencji jako innych (na przykład  *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="41250-221">We recommend following hello same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-hello-identity-provider-button-tooan-action"></a><span data-ttu-id="41250-222">Akcja tooan przycisku dostawcy tożsamości hello łącza</span><span class="sxs-lookup"><span data-stu-id="41250-222">Link hello identity provider button tooan action</span></span>

<span data-ttu-id="41250-223">Teraz, gdy masz przycisk dostawcy tożsamości w miejscu połączyć je tooan akcji.</span><span class="sxs-lookup"><span data-stu-id="41250-223">Now that you have an identity provider button in place, link it tooan action.</span></span> <span data-ttu-id="41250-224">W takim przypadku akcja hello jest dla usługi Azure AD B2C toocommunicate z tooreceive Salesforce tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="41250-224">In this case, hello action is for Azure AD B2C toocommunicate with Salesforce tooreceive a SAML token.</span></span> <span data-ttu-id="41250-225">Można to zrobić przez łączenie hello techniczne profilu dla użytkownika SAML Salesforce dostawcy oświadczeń:</span><span class="sxs-lookup"><span data-stu-id="41250-225">You can do this by linking hello technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="41250-226">W hello `<UserJourney>` węzła, Znajdź hello `<OrchestrationStep>` z `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="41250-226">In hello `<UserJourney>` node, find hello `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="41250-227">Dodaj następujące XML hello:</span><span class="sxs-lookup"><span data-stu-id="41250-227">Add hello following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="41250-228">Aktualizacja `Id` toohello samą wartość tego używanego wcześniej dla `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="41250-228">Update `Id` toohello same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="41250-229">Aktualizacja `TechnicalProfileReferenceId` toohello `Id` hello techniczne profilu utworzonego wcześniej (na przykład ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="41250-229">Update `TechnicalProfileReferenceId` toohello `Id` of hello technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-hello-updated-extension-file"></a><span data-ttu-id="41250-230">Przekaż hello zaktualizowane rozszerzenie pliku</span><span class="sxs-lookup"><span data-stu-id="41250-230">Upload hello updated extension file</span></span>

<span data-ttu-id="41250-231">Po zakończeniu modyfikowania hello rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="41250-231">You are done modifying hello extension file.</span></span> <span data-ttu-id="41250-232">Zapisz i przekazywanie tego pliku.</span><span class="sxs-lookup"><span data-stu-id="41250-232">Save and upload this file.</span></span> <span data-ttu-id="41250-233">Upewnij się, że wszystkie operacje sprawdzania poprawności powiodło się.</span><span class="sxs-lookup"><span data-stu-id="41250-233">Ensure that all validations succeed.</span></span>

### <a name="update-hello-relying-party-file"></a><span data-ttu-id="41250-234">Zaktualizuj hello jednostki uzależnionej strony plik</span><span class="sxs-lookup"><span data-stu-id="41250-234">Update hello relying party file</span></span>

<span data-ttu-id="41250-235">Następnie zaktualizuj hello jednostki uzależnionej strony (RP) pliku, który inicjuje przebieg użytkownika hello, utworzony:</span><span class="sxs-lookup"><span data-stu-id="41250-235">Next, update hello relying party (RP) file that initiates hello user journey that you created:</span></span>

1. <span data-ttu-id="41250-236">Utwórz kopię SignUpOrSignIn.xml w katalogu roboczym.</span><span class="sxs-lookup"><span data-stu-id="41250-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="41250-237">Następnie należy zmienić jego nazwę (na przykład SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="41250-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="41250-238">Nowy plik i aktualizacji hello hello Otwórz `PolicyId` atrybutu dla `<TrustFrameworkPolicy>` z unikatową wartość.</span><span class="sxs-lookup"><span data-stu-id="41250-238">Open hello new file and update hello `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="41250-239">Jest to nazwa hello zasady (na przykład SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="41250-239">This is hello name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="41250-240">Modyfikowanie hello `ReferenceId` atrybutu w `<DefaultUserJourney>` toomatch hello `Id` hello nowego użytkownika podróży utworzony (na przykład SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="41250-240">Modify hello `ReferenceId` attribute in `<DefaultUserJourney>` toomatch hello `Id` of hello new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="41250-241">Zapisz zmiany, a następnie przekaż plik hello.</span><span class="sxs-lookup"><span data-stu-id="41250-241">Save your changes, and then upload hello file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="41250-242">Testowanie i rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="41250-242">Test and troubleshoot</span></span>

<span data-ttu-id="41250-243">tootest hello niestandardowych zasad, które przekazanym właśnie, w hello portalu Azure, przejdź do bloku zasad toohello, a następnie kliknij **Uruchom teraz**.</span><span class="sxs-lookup"><span data-stu-id="41250-243">tootest hello custom policy that you just uploaded, in hello Azure portal, go toohello policy blade, and then click **Run now**.</span></span> <span data-ttu-id="41250-244">Jeśli nie powiedzie się, zobacz [Rozwiązywanie problemów dotyczących zasad niestandardowych](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="41250-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41250-245">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41250-245">Next steps</span></span>

<span data-ttu-id="41250-246">Wyrazić swoją opinię za[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="41250-246">Provide feedback too[AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
