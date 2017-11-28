---
title: "Usługa Azure Active Directory B2C: Dodawanie własnych zasad toocustom atrybutów i używanie w edycji profilu | Dokumentacja firmy Microsoft"
description: "Przewodnik dotyczący przy użyciu właściwości rozszerzenia, atrybuty niestandardowe, w tym ich z hello interfejsu użytkownika"
services: active-directory-b2c
documentationcenter: 
author: rojasja
manager: krassk
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 8cc9c6a38d7652797ba54a3e02078ac2bf4a693b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a><span data-ttu-id="2ec31-103">Usługa Azure Active Directory B2C: Tworzenie i używanie niestandardowych atrybutów w profilu niestandardowego edytowanie zasad</span><span class="sxs-lookup"><span data-stu-id="2ec31-103">Azure Active Directory B2C: Creating and using custom attributes in a custom profile edit policy</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="2ec31-104">W tym artykule Tworzenie niestandardowego atrybutu w katalogu usługi Azure AD B2C i jako oświadczenia niestandardowego w podróży użytkownika edycji profilu hello za pomocą tego nowego atrybutu.</span><span class="sxs-lookup"><span data-stu-id="2ec31-104">In this article, you create a custom attribute in your Azure AD B2C directory and use this new attribute as a custom claim in hello profile edit user journey.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ec31-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2ec31-105">Prerequisites</span></span>

<span data-ttu-id="2ec31-106">Hello pełną kroki opisane w artykule hello [wprowadzenie zasady niestandardowe](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="2ec31-106">Complete hello steps in hello article [Getting Started with Custom Policies](active-directory-b2c-get-started-custom.md).</span></span>

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a><span data-ttu-id="2ec31-107">Atrybuty niestandardowe toocollect informacje o klientach w usłudze Azure Active Directory B2C za pomocą zasad niestandardowych</span><span class="sxs-lookup"><span data-stu-id="2ec31-107">Use custom attributes toocollect information about your customers in Azure Active Directory B2C using custom policies</span></span>
<span data-ttu-id="2ec31-108">Katalogu usługi Azure Active Directory (Azure AD) B2C jest dostarczany z wbudowanego zestawu atrybutów: podana imię, nazwisko, Miasto, kod pocztowy, userPrincipalName, itp.  Często konieczne toocreate własne atrybuty.</span><span class="sxs-lookup"><span data-stu-id="2ec31-108">Your Azure Active Directory (Azure AD) B2C directory comes with a built-in set of attributes: Given Name, Surname, City, Postal Code, userPrincipalName, etc.  You often need toocreate your own attributes.</span></span>  <span data-ttu-id="2ec31-109">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="2ec31-109">For example:</span></span>
* <span data-ttu-id="2ec31-110">Aplikacja klienta uwzględniającym musi toopersist atrybut, taki jak "LoyaltyNumber."</span><span class="sxs-lookup"><span data-stu-id="2ec31-110">A customer-facing application needs toopersist an attribute such as "LoyaltyNumber."</span></span>
* <span data-ttu-id="2ec31-111">Dostawca tożsamości ma identyfikator unikatowy użytkownika, który musi zostać zapisany, takie jak "uniqueUserGUID"."</span><span class="sxs-lookup"><span data-stu-id="2ec31-111">An identity provider has a unique user identifier that must be saved such as "uniqueUserGUID.""</span></span>
* <span data-ttu-id="2ec31-112">Przebieg użytkownika niestandardowego wymaga toopersist hello stanu użytkownika, takie jak "migrationStatus."</span><span class="sxs-lookup"><span data-stu-id="2ec31-112">A custom user journey needs toopersist hello state of user such as "migrationStatus."</span></span>

<span data-ttu-id="2ec31-113">Z usługi Azure AD B2C można rozszerzyć hello zestaw atrybutów przechowywanych dla każdego konta użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2ec31-113">With Azure AD B2C, you can extend hello set of attributes stored on each user account.</span></span> <span data-ttu-id="2ec31-114">Może także odczytywać i zapisywać te atrybuty przy użyciu hello [interfejsu API usługi Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2ec31-114">You can also read and write these attributes by using hello [Azure AD Graph API](active-directory-b2c-devquickstarts-graph-dotnet.md).</span></span>

<span data-ttu-id="2ec31-115">Właściwości rozszerzenia rozszerzenie schematu hello hello obiektów użytkownika w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="2ec31-115">Extension properties extend hello schema of hello user objects in hello directory.</span></span>  <span data-ttu-id="2ec31-116">Właściwość rozszerzenia warunki Hello, atrybutu niestandardowego i oświadczenia niestandardowe odwoływać się toohello, które samo w kontekście hello tego artykułu i hello nazwa różni się w zależności od kontekstu hello (aplikacji, obiekt zasad).</span><span class="sxs-lookup"><span data-stu-id="2ec31-116">hello terms extension property, custom attribute and custom claim refer toohello same thing in hello context of this article and hello name varies depending on hello context (application, object, policy).</span></span>

<span data-ttu-id="2ec31-117">Właściwości rozszerzenia mogą być rejestrowane tylko dla obiektu aplikacji, nawet jeśli dane mogą zawierać dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2ec31-117">Extension properties can only be registered on an Application object even though they may contain data for a User.</span></span> <span data-ttu-id="2ec31-118">Właściwość Hello jest dołączona toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2ec31-118">hello property is attached toohello application.</span></span> <span data-ttu-id="2ec31-119">obiekt aplikacji Hello musi być przyznany dostęp do zapisu tooregister właściwość rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="2ec31-119">hello Application object must be granted write access tooregister an extension property.</span></span> <span data-ttu-id="2ec31-120">Tooany pojedynczego obiektu można pisać 100 właściwości rozszerzenia (za pośrednictwem wszystkich typów i wszystkie aplikacje).</span><span class="sxs-lookup"><span data-stu-id="2ec31-120">100 Extension properties (across ALL types and ALL applications) can be written tooany single object.</span></span> <span data-ttu-id="2ec31-121">Właściwości rozszerzenia są dodawane typ katalog docelowy toohello i staje się natychmiast dostępne w dzierżawie katalogu hello Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="2ec31-121">Extension properties are added toohello target directory type and becomes immediately accessible in hello Azure AD B2C directory tenant.</span></span>
<span data-ttu-id="2ec31-122">Usunięcie aplikacji hello są również usuwane te właściwości rozszerzenia wraz z danymi znajdującymi się w nich dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2ec31-122">If hello application is deleted, those Extension properties along with any data contained in them for all users are also removed.</span></span> <span data-ttu-id="2ec31-123">Jeśli właściwość rozszerzenia są usuwane przez hello aplikacji, zostanie ono usunięte na powitania obiektów katalogu docelowego i hello wartości usunięte.</span><span class="sxs-lookup"><span data-stu-id="2ec31-123">If an extension property is deleted by hello Application, it is removed on hello target directory objects, and hello values deleted.</span></span>

<span data-ttu-id="2ec31-124">Właściwości rozszerzenia istnieją tylko w kontekście hello zarejestrowaną aplikację w dzierżawie powitalnych.</span><span class="sxs-lookup"><span data-stu-id="2ec31-124">Extension properties exist only in hello context of a registered  Application in hello tenant.</span></span> <span data-ttu-id="2ec31-125">Identyfikator obiektu Hello tej aplikacji muszą być zawarte w hello TechnicalProfile, który go używać.</span><span class="sxs-lookup"><span data-stu-id="2ec31-125">hello object id of that Application must be included in hello TechnicalProfile that use it.</span></span>

>[!NOTE]
><span data-ttu-id="2ec31-126">katalog usługi Azure AD B2C Hello zwykle zawiera aplikację sieci Web o nazwie `b2c-extensions-app`.</span><span class="sxs-lookup"><span data-stu-id="2ec31-126">hello Azure AD B2C directory typically includes a Web App named `b2c-extensions-app`.</span></span>  <span data-ttu-id="2ec31-127">Tę aplikację przede wszystkim jest używany przez zasady wbudowanych b2c hello hello oświadczeń niestandardowe utworzone przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec31-127">This application is primarily used by hello b2c built-in  policies for hello custom claims created via hello Azure portal.</span></span>  <span data-ttu-id="2ec31-128">Za pomocą tego rozszerzenia tooregister aplikacji do zasad niestandardowych b2c jest zalecane tylko dla użytkowników zaawansowanych.</span><span class="sxs-lookup"><span data-stu-id="2ec31-128">Using this application tooregister extensions for b2c custom policies is recommended only for advanced users.</span></span>  <span data-ttu-id="2ec31-129">Odpowiednie instrukcje znajdują się w sekcji kolejne kroki w tym artykule hello.</span><span class="sxs-lookup"><span data-stu-id="2ec31-129">Instructions for this are included in hello Next Steps section in this article.</span></span>


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a><span data-ttu-id="2ec31-130">Tworzenie nowego toostore aplikacji hello — właściwości rozszerzenia</span><span class="sxs-lookup"><span data-stu-id="2ec31-130">Creating a new application toostore hello extension properties</span></span>

1. <span data-ttu-id="2ec31-131">Otwórz sesję przeglądania i przejdź toohello [Azure porta](https://portal.azure.com) i zaloguj się przy użyciu poświadczeń administracyjnych serwera hello mają tooconfigure katalogu usługi B2C.</span><span class="sxs-lookup"><span data-stu-id="2ec31-131">Open a browsing session and navigate toohello [Azure porta](https://portal.azure.com) and sign in with administrative credentials of hello B2C Directory you wish tooconfigure.</span></span>
1. <span data-ttu-id="2ec31-132">Kliknij przycisk **usługi Azure Active Directory** w menu nawigacji po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="2ec31-132">Click **Azure Active Directory** on hello left navigation menu.</span></span> <span data-ttu-id="2ec31-133">Toofind ją, wybierając więcej usług może być konieczne >.</span><span class="sxs-lookup"><span data-stu-id="2ec31-133">You may need toofind it by selecting More services>.</span></span>
1. <span data-ttu-id="2ec31-134">Wybierz **rejestracji aplikacji** i kliknij przycisk **nowej rejestracji aplikacji**</span><span class="sxs-lookup"><span data-stu-id="2ec31-134">Select **App registrations** and click **New application registration**</span></span>
1. <span data-ttu-id="2ec31-135">Zapewniają następujące hello zalecane wpisy:</span><span class="sxs-lookup"><span data-stu-id="2ec31-135">Provide hello following recommended entries:</span></span>
  * <span data-ttu-id="2ec31-136">Określ nazwę dla aplikacji sieci web hello: **aplikacji sieci Web-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="2ec31-136">Specify a name for hello web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
  * <span data-ttu-id="2ec31-137">Typ aplikacji: aplikacja/interfejs API sieci Web</span><span class="sxs-lookup"><span data-stu-id="2ec31-137">Application type: Web app/API</span></span>
  * <span data-ttu-id="2ec31-138">URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="2ec31-138">Sign-on URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions</span></span>
1. <span data-ttu-id="2ec31-139">Wybierz ** utworzyć.</span><span class="sxs-lookup"><span data-stu-id="2ec31-139">Select **Create.</span></span> <span data-ttu-id="2ec31-140">Pomyślne zakończenie pojawia się w hello **powiadomienia**</span><span class="sxs-lookup"><span data-stu-id="2ec31-140">Successful completion appears in hello **notifications**</span></span>
1. <span data-ttu-id="2ec31-141">Wybierz aplikację sieci web hello nowo utworzony: **aplikacji sieci Web-GraphAPI-DirectoryExtensions**</span><span class="sxs-lookup"><span data-stu-id="2ec31-141">Select hello newly created web application: **WebApp-GraphAPI-DirectoryExtensions**</span></span>
1. <span data-ttu-id="2ec31-142">Wybierz ustawienia: **wymagane uprawnienia**</span><span class="sxs-lookup"><span data-stu-id="2ec31-142">Select Settings: **Required permissions**</span></span>
1. <span data-ttu-id="2ec31-143">Wybierz interfejs API **usługi Active Directory systemu Windows**</span><span class="sxs-lookup"><span data-stu-id="2ec31-143">Select API **Windows Active Directory**</span></span>
1. <span data-ttu-id="2ec31-144">Należy zaznaczyć uprawnienia aplikacji: **Odczyt i zapis danych katalogu**, i **Zapisz**</span><span class="sxs-lookup"><span data-stu-id="2ec31-144">Place a checkmark in Application Permissions: **Read and write directory data**, and **Save**</span></span>
1. <span data-ttu-id="2ec31-145">Wybierz **udzielić uprawnień** i Potwierdź **tak**.</span><span class="sxs-lookup"><span data-stu-id="2ec31-145">Choose **Grant permissions** and confirm **Yes**.</span></span>
1. <span data-ttu-id="2ec31-146">Skopiuj tooyour Schowka i Zapisz hello poniższych identyfikatorów z aplikacji sieci Web-GraphAPI-DirectoryExtensions > Ustawienia > Właściwości ></span><span class="sxs-lookup"><span data-stu-id="2ec31-146">Copy tooyour clipboard and save hello following identifiers from WebApp-GraphAPI-DirectoryExtensions>Settings>Properties></span></span>
*  <span data-ttu-id="2ec31-147">**Identyfikator aplikacji** .</span><span class="sxs-lookup"><span data-stu-id="2ec31-147">**Application ID** .</span></span> <span data-ttu-id="2ec31-148">Przykład:`103ee0e6-f92d-4183-b576-8c3739027780`</span><span class="sxs-lookup"><span data-stu-id="2ec31-148">Example: `103ee0e6-f92d-4183-b576-8c3739027780`</span></span>
* <span data-ttu-id="2ec31-149">**Obiekt o identyfikatorze**.</span><span class="sxs-lookup"><span data-stu-id="2ec31-149">**Object ID**.</span></span> <span data-ttu-id="2ec31-150">Przykład:`80d8296a-da0a-49ee-b6ab-fd232aa45201`</span><span class="sxs-lookup"><span data-stu-id="2ec31-150">Example: `80d8296a-da0a-49ee-b6ab-fd232aa45201`</span></span>



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a><span data-ttu-id="2ec31-151">Modyfikowanie hello tooadd Twojego zasad niestandardowych ApplicationObjectId</span><span class="sxs-lookup"><span data-stu-id="2ec31-151">Modifying your custom policy tooadd hello ApplicationObjectId</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item>
                <Item Key="ClientId">insert appId here</Item>
              </Metadata>
            <!-- End of changes -->
              <CryptographicKeys>
                <Key Id="issuer_secret" StorageReferenceId="TokenSigningKeyContainer" />
              </CryptographicKeys>
              <IncludeInSso>false</IncludeInSso>
              <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop" />
            </TechnicalProfile>
        </ClaimsProvider>
    </ClaimsProviders>
```

>[!NOTE]
><span data-ttu-id="2ec31-152">Witaj <TechnicalProfile Id="AAD-Common"> jest określony tooas "typowe", ponieważ jego elementy są uwzględnione w i użyć ponownie w wszystkich hello Azure Active Directory TechnicalProfiles przy użyciu elementu hello:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span><span class="sxs-lookup"><span data-stu-id="2ec31-152">hello <TechnicalProfile Id="AAD-Common"> is referred tooas "common" because its elements are included in and reused in all hello Azure Active Directory TechnicalProfiles by using hello element: `<IncludeTechnicalProfile ReferenceId="AAD-Common" />`</span></span>

>[!NOTE]
><span data-ttu-id="2ec31-153">Podczas hello TechnicalProfile zapisuje dla właściwości rozszerzenia toohello nowo utworzony czasu hello pierwszy, może wystąpić błąd jednorazowego.</span><span class="sxs-lookup"><span data-stu-id="2ec31-153">When hello TechnicalProfile writes for hello first time toohello newly created extension property, you may experience a one-time error.</span></span>  <span data-ttu-id="2ec31-154">Właściwość rozszerzenia Hello jest tworzony hello jest używany po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="2ec31-154">hello extension property is created hello first time it is used.</span></span>  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a><span data-ttu-id="2ec31-155">Za pomocą hello nowe rozszerzenie właściwości / atrybutu niestandardowego w podróży użytkownika</span><span class="sxs-lookup"><span data-stu-id="2ec31-155">Using hello new extension property / custom attribute in a user journey</span></span>


1. <span data-ttu-id="2ec31-156">Otwórz hello jednostki uzależnionej Party(RP) pliku, który opisuje zasady edytować przebieg użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2ec31-156">Open hello Relying Party(RP) file that describes your policy edit user journey.</span></span>  <span data-ttu-id="2ec31-157">Jeśli uruchamiasz, może być wskazane toodownload swoją wersję już skonfigurowany hello RP PolicyEdit pliku bezpośrednio z hello Azure B2C niestandardowych zasad części hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2ec31-157">If you are starting out, it may be advisable toodownload your already configured version of hello RP-PolicyEdit file directly from hello Azure B2C Custom Policy section in hello Azure portal.</span></span>  <span data-ttu-id="2ec31-158">Alternatywnie można otworzyć pliku XML z folderu magazynu.</span><span class="sxs-lookup"><span data-stu-id="2ec31-158">Alternatively, open your XML file from your storage folder.</span></span>
2. <span data-ttu-id="2ec31-159">Dodawanie oświadczenia niestandardowego `loyaltyId`.</span><span class="sxs-lookup"><span data-stu-id="2ec31-159">Add a custom claim `loyaltyId`.</span></span>  <span data-ttu-id="2ec31-160">Dodając niestandardowe hello oświadczeń w hello `<RelyingParty>` elementu, jest przekazywana jako parametr toohello UserJourney TechnicalProfiles i uwzględnione w tokenie hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="2ec31-160">By including hello custom claim in hello `<RelyingParty>` element, it is passed as a parameter toohello UserJourney TechnicalProfiles and included in hello token for hello application.</span></span>
```xml
<RelyingParty>
   <DefaultUserJourney ReferenceId="ProfileEdit" />
   <TechnicalProfile Id="PolicyProfile">
     <DisplayName>PolicyProfile</DisplayName>
     <Protocol Name="OpenIdConnect" />
     <OutputClaims>
       <OutputClaim ClaimTypeReferenceId="objectId" PartnerClaimType="sub"/>
       <OutputClaim ClaimTypeReferenceId="city" />

       <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />

     </OutputClaims>
     <SubjectNamingInfo ClaimType="sub" />
   </TechnicalProfile>
 </RelyingParty>
 ```
3. <span data-ttu-id="2ec31-161">Dodaj plik zasad oświadczeń definicji toohello rozszerzenia `TrustFrameworkExtensions.xml` wewnątrz hello `<ClaimsSchema>` element, jak pokazano.</span><span class="sxs-lookup"><span data-stu-id="2ec31-161">Add a claim definition toohello Extension policy file  `TrustFrameworkExtensions.xml` inside hello `<ClaimsSchema>` element as shown.</span></span>
```xml
<ClaimsSchema>
        <ClaimType Id="extension_loyaltyId">
            <DisplayName>Loyalty Identification Tag</DisplayName>
            <DataType>string</DataType>
            <UserHelpText>Your loyalty number from your membership card</UserHelpText>
            <UserInputType>TextBox</UserInputType>
        </ClaimType>
</ClaimsSchema>
```
4. <span data-ttu-id="2ec31-162">Dodaj hello oświadczeń sam plik podstawowy zasad toohello definicji `TrustFrameworkBase.xml`.</span><span class="sxs-lookup"><span data-stu-id="2ec31-162">Add hello same claim definition toohello Base policy file `TrustFrameworkBase.xml`.</span></span>  
><span data-ttu-id="2ec31-163">Dodawanie `ClaimType` definicji w jednocześnie hello typu podstawowego, jak i plik rozszerzenia hello zwykle nie jest konieczne, jednak ponieważ następne kroki hello doda hello extension_loyaltyId tooTechnicalProfiles w pliku podstawowego hello, modułu sprawdzania poprawności hello zasad spowoduje odrzucenie hello przekazywania Witaj pliku bazowego bez niego.</span><span class="sxs-lookup"><span data-stu-id="2ec31-163">Adding a `ClaimType` definition in both hello base and hello extensions file is normally not necessary, however since hello next steps will add hello extension_loyaltyId tooTechnicalProfiles in hello Base file, hello policy validator will reject hello upload of hello base file without it.</span></span>
><span data-ttu-id="2ec31-164">Może to być przydatne tootrace hello wykonywania hello podróży użytkownika o nazwie "ProfileEdit" w pliku TrustFrameworkBase.xml hello.</span><span class="sxs-lookup"><span data-stu-id="2ec31-164">It may be useful tootrace hello execution of hello user journey named "ProfileEdit" in hello TrustFrameworkBase.xml file.</span></span>  <span data-ttu-id="2ec31-165">Wyszukaj użytkownika obejmuje hello hello takie same nazwy w edytorze i sprawdź, czy aranżacji krok 5 wywołuje hello TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".</span><span class="sxs-lookup"><span data-stu-id="2ec31-165">Search for hello user journey of hello same name in your editor and observe that Orchestration Step 5 invokes hello TechnicalProfileReferenceID="SelfAsserted-ProfileUpdate".</span></span>  <span data-ttu-id="2ec31-166">Wyszukiwanie i sprawdzić samodzielnie tego toofamiliarize TechnicalProfile z przepływem hello.</span><span class="sxs-lookup"><span data-stu-id="2ec31-166">Search and inspect this TechnicalProfile toofamiliarize yourself with hello flow.</span></span>
5. <span data-ttu-id="2ec31-167">Dodaj loyaltyId zgodnie z oświadczeń przychodzących i wychodzących w hello TechnicalProfile "SelfAsserted ProfileUpdate"</span><span class="sxs-lookup"><span data-stu-id="2ec31-167">Add loyaltyId as input and output claim in hello TechnicalProfile "SelfAsserted-ProfileUpdate"</span></span>
```xml
<TechnicalProfile Id="SelfAsserted-ProfileUpdate">
          <DisplayName>User ID signup</DisplayName>
          <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.SelfAssertedAttributeProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
          <Metadata>
            <Item Key="ContentDefinitionReferenceId">api.selfasserted.profileupdate</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>

            <InputClaim ClaimTypeReferenceId="alternativeSecurityId" />
            <InputClaim ClaimTypeReferenceId="userPrincipalName" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <InputClaim ClaimTypeReferenceId="givenName" />
            <InputClaim ClaimTypeReferenceId="surname" />
            <InputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </InputClaims>
          <OutputClaims>
            <!-- Required claims -->
            <OutputClaim ClaimTypeReferenceId="executed-SelfAsserted-Input" DefaultValue="true" />

            <!-- Optional claims. These claims are collected from hello user and can be modified. Any claim added here should be updated in the
                 ValidationTechnicalProfile referenced below so it can be written toodirectory after being updateed by hello user, i.e. AAD-UserWriteProfileUsingObjectId. -->
            <OutputClaim ClaimTypeReferenceId="givenName" />
            <OutputClaim ClaimTypeReferenceId="surname" />
            <OutputClaim ClaimTypeReferenceId="extension_loyaltyId"/>
          </OutputClaims>
          <ValidationTechnicalProfiles>
            <ValidationTechnicalProfile ReferenceId="AAD-UserWriteProfileUsingObjectId" />
          </ValidationTechnicalProfiles>
        </TechnicalProfile>
```
6. <span data-ttu-id="2ec31-168">Dodaj oświadczenie TechnicalProfile "AAD UserWriteProfileUsingObjectId" toopersist hello wartości oświadczenia hello we właściwości rozszerzenia hello, hello bieżącego użytkownika w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="2ec31-168">Add claim in TechnicalProfile "AAD-UserWriteProfileUsingObjectId" toopersist hello value of hello claim in hello extension property, for hello current user in hello directory.</span></span>
```xml
<TechnicalProfile Id="AAD-UserWriteProfileUsingObjectId">
          <Metadata>
            <Item Key="Operation">Write</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalAlreadyExists">false</Item>
            <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
          </Metadata>
          <IncludeInSso>false</IncludeInSso>
          <InputClaims>
            <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
          </InputClaims>
          <PersistedClaims>
            <!-- Required claims -->
            <PersistedClaim ClaimTypeReferenceId="objectId" />

            <!-- Optional claims -->
            <PersistedClaim ClaimTypeReferenceId="givenName" />
            <PersistedClaim ClaimTypeReferenceId="surname" />
            <PersistedClaim ClaimTypeReferenceId="extension_loyaltyId" />

          </PersistedClaims>
          <IncludeTechnicalProfile ReferenceId="AAD-Common" />
        </TechnicalProfile>
```
7. <span data-ttu-id="2ec31-169">Dodaj oświadczenie TechnicalProfile "AAD UserReadUsingObjectId" tooread hello wartości atrybutu rozszerzenia hello za każdym razem, gdy użytkownik loguje.</span><span class="sxs-lookup"><span data-stu-id="2ec31-169">Add claim in TechnicalProfile "AAD-UserReadUsingObjectId" tooread hello value of hello extension attribute every time a user logs in.</span></span> <span data-ttu-id="2ec31-170">Dotychczas hello TechnicalProfiles zostały zmienione w przepływie hello tylko kont lokalnych.</span><span class="sxs-lookup"><span data-stu-id="2ec31-170">Thus far hello TechnicalProfiles have been changed in hello flow of local accounts only.</span></span>  <span data-ttu-id="2ec31-171">Razie nowy atrybut hello w przepływie hello konta społecznego/federacyjnych inny zestaw TechnicalProfiles musi toobe zmienione.</span><span class="sxs-lookup"><span data-stu-id="2ec31-171">If hello new attribute is desired in hello flow of a social/federated account, a different set of TechnicalProfiles needs toobe changed.</span></span> <span data-ttu-id="2ec31-172">Zobacz następne kroki.</span><span class="sxs-lookup"><span data-stu-id="2ec31-172">See Next Steps.</span></span>

```xml
<!-- hello following technical profile is used tooread data after user authenticates. -->
     <TechnicalProfile Id="AAD-UserReadUsingObjectId">
       <Metadata>
         <Item Key="Operation">Read</Item>
         <Item Key="RaiseErrorIfClaimsPrincipalDoesNotExist">true</Item>
       </Metadata>
       <IncludeInSso>false</IncludeInSso>
       <InputClaims>
         <InputClaim ClaimTypeReferenceId="objectId" Required="true" />
       </InputClaims>
       <OutputClaims>
         <!-- Optional claims -->
         <OutputClaim ClaimTypeReferenceId="signInNames.emailAddress" />
         <OutputClaim ClaimTypeReferenceId="displayName" />
         <OutputClaim ClaimTypeReferenceId="otherMails" />
         <OutputClaim ClaimTypeReferenceId="givenName" />
         <OutputClaim ClaimTypeReferenceId="surname" />
         <OutputClaim ClaimTypeReferenceId="extension_loyaltyId" />
       </OutputClaims>
       <IncludeTechnicalProfile ReferenceId="AAD-Common" />
     </TechnicalProfile>
```


>[!IMPORTANT]
><span data-ttu-id="2ec31-173">Hello IncludeTechnicalProfile element dodaje wszystkie elementy hello AAD typowe toothis TechnicalProfile.</span><span class="sxs-lookup"><span data-stu-id="2ec31-173">hello IncludeTechnicalProfile element adds all hello elements of AAD-Common toothis TechnicalProfile.</span></span>

## <a name="test-hello-custom-policy-using-run-now"></a><span data-ttu-id="2ec31-174">Zasady niestandardowe hello testu przy użyciu "opcji Uruchom teraz"</span><span class="sxs-lookup"><span data-stu-id="2ec31-174">Test hello custom policy using "Run Now"</span></span>
1. <span data-ttu-id="2ec31-175">Otwórz hello **bloku usługi Azure AD B2C** i przejdź zbyt**tożsamości środowiska Framework > zasady niestandardowe**.</span><span class="sxs-lookup"><span data-stu-id="2ec31-175">Open hello **Azure AD B2C Blade** and navigate too**Identity Experience Framework > Custom policies**.</span></span>
1. <span data-ttu-id="2ec31-176">Wybierz zasady niestandardowe hello, który został przekazany, a następnie kliknij przycisk hello **Uruchom teraz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="2ec31-176">Select hello custom policy that you uploaded, and click hello **Run now** button.</span></span>
1. <span data-ttu-id="2ec31-177">Powinno być możliwe toosign przy użyciu adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="2ec31-177">You should be able toosign up using an email address.</span></span>

<span data-ttu-id="2ec31-178">token identyfikatora Hello odesłał tooyour aplikacji zawiera nową właściwość rozszerzenia hello jako oświadczenia niestandardowego poprzedzony extension_loyaltyId.</span><span class="sxs-lookup"><span data-stu-id="2ec31-178">hello  id token sent back tooyour application includes hello new extension property as a custom claim preceded by extension_loyaltyId.</span></span> <span data-ttu-id="2ec31-179">Zobacz przykład.</span><span class="sxs-lookup"><span data-stu-id="2ec31-179">See example.</span></span>

```
{
  "exp": 1493585187,
  "nbf": 1493581587,
  "ver": "1.0",
  "iss": "https://login.microsoftonline.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
  "sub": "a58e7c6c-7535-4074-93da-b0023fbaf3ac",
  "aud": "4e87c1dd-e5f5-4ac8-8368-bc6a98751b8b",
  "acr": "b2c_1a_trustframeworkprofileedit",
  "nonce": "defaultNonce",
  "iat": 1493581587,
  "auth_time": 1493581587,
  "extension_loyaltyId": "abc",
  "city": "Redmond"
}
```

## <a name="next-steps"></a><span data-ttu-id="2ec31-180">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2ec31-180">Next steps</span></span>

<span data-ttu-id="2ec31-181">Dodaj hello nowe oświadczenie toohello przepływów społecznościowych konta logowania, zmieniając hello TechnicalProfiles na liście.</span><span class="sxs-lookup"><span data-stu-id="2ec31-181">Add hello new claim toohello flows for social account logins by changing hello TechnicalProfiles listed.</span></span> <span data-ttu-id="2ec31-182">Te dwie TechnicalProfiles są używane przez toowrite logowania do konta społecznego/federacyjnych i odczytywania danych użytkowników hello przy użyciu hello alternativeSecurityId hello lokalizatora hello obiektu user.</span><span class="sxs-lookup"><span data-stu-id="2ec31-182">These two TechnicalProfiles are used by social/federated account logins toowrite and read hello user data using hello alternativeSecurityId as hello locator of hello user object.</span></span>
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

<span data-ttu-id="2ec31-183">Przy użyciu hello takie same atrybuty rozszerzenia między zasadami wbudowanych i niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="2ec31-183">Using hello same extension attributes between built-in and custom policies.</span></span>
<span data-ttu-id="2ec31-184">Po dodaniu atrybuty rozszerzenia (alias atrybutów niestandardowych) za pośrednictwem portalu środowisko hello te atrybuty są rejestrowane przy użyciu hello ** b2c rozszerzeń aplikacji w każdej dzierżawy b2c.</span><span class="sxs-lookup"><span data-stu-id="2ec31-184">When you add extension attributes (aka custom attributes) via hello portal experience, those attributes are registered using hello **b2c-extensions-app that exists in every b2c tenant.</span></span>  <span data-ttu-id="2ec31-185">toouse te atrybuty rozszerzenia w zasadach niestandardowych:</span><span class="sxs-lookup"><span data-stu-id="2ec31-185">toouse these extension attributes in your custom policy:</span></span>
1. <span data-ttu-id="2ec31-186">W ramach dzierżawy usługi b2c w portal.azure.com Przejdź zbyt**usługi Azure Active Directory** i wybierz **rejestracji aplikacji**</span><span class="sxs-lookup"><span data-stu-id="2ec31-186">Within your b2c tenant in portal.azure.com, navigate too**Azure Active Directory** and select **App registrations**</span></span>
2. <span data-ttu-id="2ec31-187">Znajdź użytkownika **b2c rozszerzeń aplikacji** i wybierz ją</span><span class="sxs-lookup"><span data-stu-id="2ec31-187">Find your **b2c-extensions-app** and select it</span></span>
3. <span data-ttu-id="2ec31-188">W obszarze "Essentials" hello rekordu **identyfikator aplikacji** i hello **identyfikator obiektu:**</span><span class="sxs-lookup"><span data-stu-id="2ec31-188">Under 'Essentials' record hello **Application ID** and hello **Object ID**</span></span>
4. <span data-ttu-id="2ec31-189">Należy uwzględnić je w metadanych programu AAD typowe techniczne profilu podobnie jak w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2ec31-189">Include them in your AAD-Common Technical profile metadata like as follows:</span></span>

```xml
    <ClaimsProviders>
        <ClaimsProvider>
              <DisplayName>Azure Active Directory</DisplayName>
            <TechnicalProfile Id="AAD-Common">
              <DisplayName>Azure Active Directory</DisplayName>
              <Protocol Name="Proprietary" Handler="Web.TPEngine.Providers.AzureActiveDirectoryProvider, Web.TPEngine, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />
              <!-- Provide objectId and appId before using extension properties. -->
              <Metadata>
                <Item Key="ApplicationObjectId">insert objectId here</Item> <!-- This is hello "Object ID" from hello "b2c-extensions-app"-->
                <Item Key="ClientId">insert appId here</Item> <!--This is hello "Application ID" from hello "b2c-extensions-app"-->
              </Metadata>
```

<span data-ttu-id="2ec31-190">spójności tookeep hello doświadczenie w portalu, Utwórz te atrybuty przy użyciu interfejsu użytkownika portalu hello *przed* używane w niestandardowych zasad.</span><span class="sxs-lookup"><span data-stu-id="2ec31-190">tookeep consistency with hello portal experience, create these attributes using hello portal UI *before* you use them in your custom policies.</span></span>  <span data-ttu-id="2ec31-191">Podczas tworzenia atrybutu "ActivationStatus" w portalu hello, użytkownik musi odwoływać się tooit w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2ec31-191">When you create an attribute "ActivationStatus" in hello portal, you must refer tooit as follows:</span></span>

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a><span data-ttu-id="2ec31-192">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="2ec31-192">Reference</span></span>

* <span data-ttu-id="2ec31-193">A **techniczne profilu (TP)** jest typem elementu, który można traktować jako *funkcja* definiuje nazwę punktu końcowego, jego metadanych, protokół, a szczegóły hello exchange oświadczenia, które hello tożsamości Należy wykonać czynności Framework.</span><span class="sxs-lookup"><span data-stu-id="2ec31-193">A **Technical Profile (TP)** is an element type that can be thought of as a *function* that defines an endpoint’s name, its metadata, its protocol, and details hello exchange of claims that hello Identity Experience Framework should perform.</span></span>  <span data-ttu-id="2ec31-194">Gdy to *funkcja* jest wywoływana w kroku aranżacji lub z innego TechnicalProfile, hello InputClaims i OutputClaims są udostępniane jako parametry przez obiekt wywołujący hello.</span><span class="sxs-lookup"><span data-stu-id="2ec31-194">When this *function* is called in an orchestration step or from another TechnicalProfile, hello InputClaims and OutputClaims are provided as parameters by hello caller.</span></span>


* <span data-ttu-id="2ec31-195">Pełna oczyszczania we właściwościach rozszerzenia, zobacz artykuł hello [rozszerzenia SCHEMATU katalogu | POJĘCIA DOTYCZĄCE INTERFEJSU API PROGRAMU GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span><span class="sxs-lookup"><span data-stu-id="2ec31-195">For full treatment on extension properties, see hello article [DIRECTORY SCHEMA EXTENSIONS | GRAPH API CONCEPTS](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)</span></span>

>[!NOTE]
><span data-ttu-id="2ec31-196">Atrybuty rozszerzenia interfejsu API programu Graph są nazywane przy użyciu konwencji hello `extension_ApplicationObjectID_attributename`.</span><span class="sxs-lookup"><span data-stu-id="2ec31-196">Extension attributes in Graph API are named using hello convention `extension_ApplicationObjectID_attributename`.</span></span> <span data-ttu-id="2ec31-197">Zasady niestandardowe można znaleźć atrybuty tooextensions jako extension_attributename, w związku z tym pominięcie hello ApplicationObjectId w hello XML</span><span class="sxs-lookup"><span data-stu-id="2ec31-197">Custom policies refer tooextensions attributes as extension_attributename, thus omitting hello ApplicationObjectId in hello XML</span></span>
