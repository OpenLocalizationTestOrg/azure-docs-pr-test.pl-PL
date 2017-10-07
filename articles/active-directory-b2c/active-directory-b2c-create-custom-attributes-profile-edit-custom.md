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
# <a name="azure-active-directory-b2c-creating-and-using-custom-attributes-in-a-custom-profile-edit-policy"></a>Usługa Azure Active Directory B2C: Tworzenie i używanie niestandardowych atrybutów w profilu niestandardowego edytowanie zasad

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

W tym artykule Tworzenie niestandardowego atrybutu w katalogu usługi Azure AD B2C i jako oświadczenia niestandardowego w podróży użytkownika edycji profilu hello za pomocą tego nowego atrybutu.

## <a name="prerequisites"></a>Wymagania wstępne

Hello pełną kroki opisane w artykule hello [wprowadzenie zasady niestandardowe](active-directory-b2c-get-started-custom.md).

## <a name="use-custom-attributes-toocollect-information-about-your-customers-in-azure-active-directory-b2c-using-custom-policies"></a>Atrybuty niestandardowe toocollect informacje o klientach w usłudze Azure Active Directory B2C za pomocą zasad niestandardowych
Katalogu usługi Azure Active Directory (Azure AD) B2C jest dostarczany z wbudowanego zestawu atrybutów: podana imię, nazwisko, Miasto, kod pocztowy, userPrincipalName, itp.  Często konieczne toocreate własne atrybuty.  Na przykład:
* Aplikacja klienta uwzględniającym musi toopersist atrybut, taki jak "LoyaltyNumber."
* Dostawca tożsamości ma identyfikator unikatowy użytkownika, który musi zostać zapisany, takie jak "uniqueUserGUID"."
* Przebieg użytkownika niestandardowego wymaga toopersist hello stanu użytkownika, takie jak "migrationStatus."

Z usługi Azure AD B2C można rozszerzyć hello zestaw atrybutów przechowywanych dla każdego konta użytkownika. Może także odczytywać i zapisywać te atrybuty przy użyciu hello [interfejsu API usługi Azure AD Graph](active-directory-b2c-devquickstarts-graph-dotnet.md).

Właściwości rozszerzenia rozszerzenie schematu hello hello obiektów użytkownika w katalogu hello.  Właściwość rozszerzenia warunki Hello, atrybutu niestandardowego i oświadczenia niestandardowe odwoływać się toohello, które samo w kontekście hello tego artykułu i hello nazwa różni się w zależności od kontekstu hello (aplikacji, obiekt zasad).

Właściwości rozszerzenia mogą być rejestrowane tylko dla obiektu aplikacji, nawet jeśli dane mogą zawierać dla użytkownika. Właściwość Hello jest dołączona toohello aplikacji. obiekt aplikacji Hello musi być przyznany dostęp do zapisu tooregister właściwość rozszerzenia. Tooany pojedynczego obiektu można pisać 100 właściwości rozszerzenia (za pośrednictwem wszystkich typów i wszystkie aplikacje). Właściwości rozszerzenia są dodawane typ katalog docelowy toohello i staje się natychmiast dostępne w dzierżawie katalogu hello Azure AD B2C.
Usunięcie aplikacji hello są również usuwane te właściwości rozszerzenia wraz z danymi znajdującymi się w nich dla wszystkich użytkowników. Jeśli właściwość rozszerzenia są usuwane przez hello aplikacji, zostanie ono usunięte na powitania obiektów katalogu docelowego i hello wartości usunięte.

Właściwości rozszerzenia istnieją tylko w kontekście hello zarejestrowaną aplikację w dzierżawie powitalnych. Identyfikator obiektu Hello tej aplikacji muszą być zawarte w hello TechnicalProfile, który go używać.

>[!NOTE]
>katalog usługi Azure AD B2C Hello zwykle zawiera aplikację sieci Web o nazwie `b2c-extensions-app`.  Tę aplikację przede wszystkim jest używany przez zasady wbudowanych b2c hello hello oświadczeń niestandardowe utworzone przy użyciu hello portalu Azure.  Za pomocą tego rozszerzenia tooregister aplikacji do zasad niestandardowych b2c jest zalecane tylko dla użytkowników zaawansowanych.  Odpowiednie instrukcje znajdują się w sekcji kolejne kroki w tym artykule hello.


## <a name="creating-a-new-application-toostore-hello-extension-properties"></a>Tworzenie nowego toostore aplikacji hello — właściwości rozszerzenia

1. Otwórz sesję przeglądania i przejdź toohello [Azure porta](https://portal.azure.com) i zaloguj się przy użyciu poświadczeń administracyjnych serwera hello mają tooconfigure katalogu usługi B2C.
1. Kliknij przycisk **usługi Azure Active Directory** w menu nawigacji po lewej stronie powitania. Toofind ją, wybierając więcej usług może być konieczne >.
1. Wybierz **rejestracji aplikacji** i kliknij przycisk **nowej rejestracji aplikacji**
1. Zapewniają następujące hello zalecane wpisy:
  * Określ nazwę dla aplikacji sieci web hello: **aplikacji sieci Web-GraphAPI-DirectoryExtensions**
  * Typ aplikacji: aplikacja/interfejs API sieci Web
  * URL:https://{tenantName}.onmicrosoft.com/WebApp-GraphAPI-DirectoryExtensions logowania jednokrotnego
1. Wybierz ** utworzyć. Pomyślne zakończenie pojawia się w hello **powiadomienia**
1. Wybierz aplikację sieci web hello nowo utworzony: **aplikacji sieci Web-GraphAPI-DirectoryExtensions**
1. Wybierz ustawienia: **wymagane uprawnienia**
1. Wybierz interfejs API **usługi Active Directory systemu Windows**
1. Należy zaznaczyć uprawnienia aplikacji: **Odczyt i zapis danych katalogu**, i **Zapisz**
1. Wybierz **udzielić uprawnień** i Potwierdź **tak**.
1. Skopiuj tooyour Schowka i Zapisz hello poniższych identyfikatorów z aplikacji sieci Web-GraphAPI-DirectoryExtensions > Ustawienia > Właściwości >
*  **Identyfikator aplikacji** . Przykład:`103ee0e6-f92d-4183-b576-8c3739027780`
* **Obiekt o identyfikatorze**. Przykład:`80d8296a-da0a-49ee-b6ab-fd232aa45201`



## <a name="modifying-your-custom-policy-tooadd-hello-applicationobjectid"></a>Modyfikowanie hello tooadd Twojego zasad niestandardowych ApplicationObjectId

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
>Witaj <TechnicalProfile Id="AAD-Common"> jest określony tooas "typowe", ponieważ jego elementy są uwzględnione w i użyć ponownie w wszystkich hello Azure Active Directory TechnicalProfiles przy użyciu elementu hello:`<IncludeTechnicalProfile ReferenceId="AAD-Common" />`

>[!NOTE]
>Podczas hello TechnicalProfile zapisuje dla właściwości rozszerzenia toohello nowo utworzony czasu hello pierwszy, może wystąpić błąd jednorazowego.  Właściwość rozszerzenia Hello jest tworzony hello jest używany po raz pierwszy.  

## <a name="using-hello-new-extension-property--custom-attribute-in-a-user-journey"></a>Za pomocą hello nowe rozszerzenie właściwości / atrybutu niestandardowego w podróży użytkownika


1. Otwórz hello jednostki uzależnionej Party(RP) pliku, który opisuje zasady edytować przebieg użytkownika.  Jeśli uruchamiasz, może być wskazane toodownload swoją wersję już skonfigurowany hello RP PolicyEdit pliku bezpośrednio z hello Azure B2C niestandardowych zasad części hello portalu Azure.  Alternatywnie można otworzyć pliku XML z folderu magazynu.
2. Dodawanie oświadczenia niestandardowego `loyaltyId`.  Dodając niestandardowe hello oświadczeń w hello `<RelyingParty>` elementu, jest przekazywana jako parametr toohello UserJourney TechnicalProfiles i uwzględnione w tokenie hello aplikacji hello.
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
3. Dodaj plik zasad oświadczeń definicji toohello rozszerzenia `TrustFrameworkExtensions.xml` wewnątrz hello `<ClaimsSchema>` element, jak pokazano.
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
4. Dodaj hello oświadczeń sam plik podstawowy zasad toohello definicji `TrustFrameworkBase.xml`.  
>Dodawanie `ClaimType` definicji w jednocześnie hello typu podstawowego, jak i plik rozszerzenia hello zwykle nie jest konieczne, jednak ponieważ następne kroki hello doda hello extension_loyaltyId tooTechnicalProfiles w pliku podstawowego hello, modułu sprawdzania poprawności hello zasad spowoduje odrzucenie hello przekazywania Witaj pliku bazowego bez niego.
>Może to być przydatne tootrace hello wykonywania hello podróży użytkownika o nazwie "ProfileEdit" w pliku TrustFrameworkBase.xml hello.  Wyszukaj użytkownika obejmuje hello hello takie same nazwy w edytorze i sprawdź, czy aranżacji krok 5 wywołuje hello TechnicalProfileReferenceID = "SelfAsserted ProfileUpdate".  Wyszukiwanie i sprawdzić samodzielnie tego toofamiliarize TechnicalProfile z przepływem hello.
5. Dodaj loyaltyId zgodnie z oświadczeń przychodzących i wychodzących w hello TechnicalProfile "SelfAsserted ProfileUpdate"
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
6. Dodaj oświadczenie TechnicalProfile "AAD UserWriteProfileUsingObjectId" toopersist hello wartości oświadczenia hello we właściwości rozszerzenia hello, hello bieżącego użytkownika w katalogu hello.
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
7. Dodaj oświadczenie TechnicalProfile "AAD UserReadUsingObjectId" tooread hello wartości atrybutu rozszerzenia hello za każdym razem, gdy użytkownik loguje. Dotychczas hello TechnicalProfiles zostały zmienione w przepływie hello tylko kont lokalnych.  Razie nowy atrybut hello w przepływie hello konta społecznego/federacyjnych inny zestaw TechnicalProfiles musi toobe zmienione. Zobacz następne kroki.

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
>Hello IncludeTechnicalProfile element dodaje wszystkie elementy hello AAD typowe toothis TechnicalProfile.

## <a name="test-hello-custom-policy-using-run-now"></a>Zasady niestandardowe hello testu przy użyciu "opcji Uruchom teraz"
1. Otwórz hello **bloku usługi Azure AD B2C** i przejdź zbyt**tożsamości środowiska Framework > zasady niestandardowe**.
1. Wybierz zasady niestandardowe hello, który został przekazany, a następnie kliknij przycisk hello **Uruchom teraz** przycisku.
1. Powinno być możliwe toosign przy użyciu adresu e-mail.

token identyfikatora Hello odesłał tooyour aplikacji zawiera nową właściwość rozszerzenia hello jako oświadczenia niestandardowego poprzedzony extension_loyaltyId. Zobacz przykład.

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

## <a name="next-steps"></a>Następne kroki

Dodaj hello nowe oświadczenie toohello przepływów społecznościowych konta logowania, zmieniając hello TechnicalProfiles na liście. Te dwie TechnicalProfiles są używane przez toowrite logowania do konta społecznego/federacyjnych i odczytywania danych użytkowników hello przy użyciu hello alternativeSecurityId hello lokalizatora hello obiektu user.
```
  <TechnicalProfile Id="AAD-UserWriteUsingAlternativeSecurityId">

  <TechnicalProfile Id="AAD-UserReadUsingAlternativeSecurityId">
```

Przy użyciu hello takie same atrybuty rozszerzenia między zasadami wbudowanych i niestandardowych.
Po dodaniu atrybuty rozszerzenia (alias atrybutów niestandardowych) za pośrednictwem portalu środowisko hello te atrybuty są rejestrowane przy użyciu hello ** b2c rozszerzeń aplikacji w każdej dzierżawy b2c.  toouse te atrybuty rozszerzenia w zasadach niestandardowych:
1. W ramach dzierżawy usługi b2c w portal.azure.com Przejdź zbyt**usługi Azure Active Directory** i wybierz **rejestracji aplikacji**
2. Znajdź użytkownika **b2c rozszerzeń aplikacji** i wybierz ją
3. W obszarze "Essentials" hello rekordu **identyfikator aplikacji** i hello **identyfikator obiektu:**
4. Należy uwzględnić je w metadanych programu AAD typowe techniczne profilu podobnie jak w następujący sposób:

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

spójności tookeep hello doświadczenie w portalu, Utwórz te atrybuty przy użyciu interfejsu użytkownika portalu hello *przed* używane w niestandardowych zasad.  Podczas tworzenia atrybutu "ActivationStatus" w portalu hello, użytkownik musi odwoływać się tooit w następujący sposób:

```
extension_ActivationStatus in hello custom policy
extension_<app-guid>_ActivationStatus via hello Graph API.
```


## <a name="reference"></a>Dokumentacja

* A **techniczne profilu (TP)** jest typem elementu, który można traktować jako *funkcja* definiuje nazwę punktu końcowego, jego metadanych, protokół, a szczegóły hello exchange oświadczenia, które hello tożsamości Należy wykonać czynności Framework.  Gdy to *funkcja* jest wywoływana w kroku aranżacji lub z innego TechnicalProfile, hello InputClaims i OutputClaims są udostępniane jako parametry przez obiekt wywołujący hello.


* Pełna oczyszczania we właściwościach rozszerzenia, zobacz artykuł hello [rozszerzenia SCHEMATU katalogu | POJĘCIA DOTYCZĄCE INTERFEJSU API PROGRAMU GRAPH](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions)

>[!NOTE]
>Atrybuty rozszerzenia interfejsu API programu Graph są nazywane przy użyciu konwencji hello `extension_ApplicationObjectID_attributename`. Zasady niestandardowe można znaleźć atrybuty tooextensions jako extension_attributename, w związku z tym pominięcie hello ApplicationObjectId w hello XML
