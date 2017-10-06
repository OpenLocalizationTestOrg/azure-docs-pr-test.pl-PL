---
title: "Azure AD Connect: Należy użyć dostawcy SAML 2.0 tożsamości na logowanie jednokrotne na | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano, za pomocą protokołu SAML 2.0 zgodne Idp na logowanie jednokrotne na."
services: active-directory
author: billmath
manager: femila
ms.custom: it-pro
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f9653dc44fb284a9b3c1988f623c33f27ae148cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
#  <a name="use-a-saml-20-identity-provider-idp-for-single-sign-on"></a>W systemie dostawcy SAML 2.0 tożsamości (IdP) dla funkcji logowania jednokrotnego

Ten temat zawiera informacje przy użyciu SAML 2.0 zgodnego profilu SP Lite podstawie dostawcy tożsamości hello preferowane zabezpieczeń usługi tokenów (STS) / dostawcy tożsamości. Jest to przydatne, gdy masz już katalog użytkownika i hasła przechowywane lokalnie, które mogą uzyskać dostęp za pomocą SAML 2.0. Ten katalog istniejącego użytkownika może służyć do logowania jednokrotnego tooOffice 365 i innych zasobów platformy Azure zabezpieczonej przez usługi AD. Hello SAML 2.0 SP-Lite profilu jest oparta na powitania powszechnie używane tooprovide standardowe tożsamości Assertion Markup języka SAML (Security) federacyjnego logowania jednokrotnego i framework wymiany atrybutu.

>[!NOTE]
>Listę firm 3 Idps, które zostały przetestowane do użycia z usługą Azure AD, zobacz hello [listę zgodności federacyjnych usługi Azure AD](active-directory-aadconnect-federation-compatibility.md)

Z sieci odpowiednio skonfigurowanego SAML 2.0 profilu opartego na IdP, firma Microsoft zapewnia to środowisko logowania jako hello integracji usługi w chmurze firmy Microsoft, takich jak Office 365. Produkty innych firm są dostawców tożsamości SAML 2.0 i dlatego firma Microsoft nie zapewnia obsługi hello wdrażania, konfiguracji, najlepszych rozwiązań dotyczących ich rozwiązywania. Raz prawidłowo skonfigurowane, hello integracji z hello SAML 2.0 przy użyciu narzędzia Analizator łączności do firmy Microsoft, opisany bardziej szczegółowo poniżej hello można przetestować dla właściwej konfiguracji dostawcy tożsamości. Aby uzyskać więcej informacji na temat dostawcy tożsamości oparte na profilu SAML 2.0 SP-Lite poproś hello organizacji, która ją podać.

>[!IMPORTANT]
>Tylko ograniczony zestaw klientów są dostępne w tym scenariuszu logowania z dostawców tożsamości SAML 2.0, w tym:

>- Oparte na sieci Web klientów, takie jak program Outlook Web Access i usługi SharePoint Online
- Klienci bogate w wiadomości e-mail, korzystających z uwierzytelniania podstawowego i obsługiwanych metoda dostępu do programu Exchange, takich jak IMAP, POP, ActiveSync, MAPI, itp. (hello punktu końcowego jest wymagana toobe wdrożony protokół klienta rozszerzony), w tym:
    - Program Microsoft Outlook 2010/Outlook 2013/Outlook 2016, Apple iPhone (różne wersje systemu iOS)
    - Różnych urządzeń systemu Google Android
    - Windows Phone 7, Windows Phone 7.8 i Windows Phone 8.0
    - Klient poczty systemu Windows 8 i Windows 8.1 klienta poczty E-mail
    - Klient poczty systemu Windows 10

Wszystkich pozostałych klientów nie są dostępne w tym scenariuszu logowania u dostawcy tożsamości SAML 2.0. Na przykład klient pulpitu hello Lync 2010 nie jest toologin możliwe do użytku hello u dostawcy tożsamości SAML 2.0 skonfigurowany do logowania jednokrotnego.

## <a name="azure-ad-saml-20-protocol-requirements"></a>Wymagania protokołu usługi Azure AD SAML 2.0
Ten temat zawiera szczegółowe wymagania dla protokołu hello i wiadomości formatowania, że Twój dostawca tożsamości SAML 2.0 musi implementować toofederate z usługi Azure AD tooenable logowania jednokrotnego tooone lub więcej usług chmurowych firmy Microsoft (takich jak Office 365). Witaj SAML 2.0 jednostki uzależnionej (SP STS) dla usługi w chmurze firmy Microsoft w tym scenariuszu jest usługi Azure AD.

Zalecane jest, upewnij się z SAML 2.0 komunikaty wyjściowe dostawcy tożsamości jest podobne toohello podano przykładowe dane śledzenia jak to możliwe. Należy także użyć wartości atrybutów określonych z metadanych usługi Azure AD hello dostarczone w miarę możliwości. Po przejściu wszystkiego wiadomości dane wyjściowe można przetestować z hello analizatora łączności firmy Microsoft zgodnie z poniższym opisem.

metadane Hello Azure AD można pobrać spod tego adresu URL: [https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml](http://https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml).
Dla klientów w Chinach przy użyciu hello Chin konkretnego wystąpienia usługi Office 365, można użyć hello następującego punktu końcowego federacyjnej: [https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml](https://nexus.partner.microsoftonline-p.cn/federationmetadata/saml20/federationmetadata.xml).

## <a name="saml-protocol-requirements"></a>Wymagania dotyczące protokołu SAML
Ta sekcja zawiera szczegółowy opis sposobu pary komunikatów żądań i odpowiedzi hello opracować w kolejności toohelp możesz tooformat wiadomości poprawnie.

Usługi Azure AD może być skonfigurowany toowork z dostawców tożsamości, korzystających z profilu SAML 2.0 SP Lite hello z niektórych wymagań wymienione poniżej. Przykładowe SAML żądań i odpowiedzi wiadomości powitania wraz z zautomatyzowanej oraz ręcznej testowania można pracować tooachieve współdziałania z usługą Azure AD.

## <a name="signature-block-requirements"></a>Wymagania dotyczące blok podpisu
W ramach hello odpowiedzi SAML wiadomość hello podpisu węzła zawiera informacje o hello podpisu cyfrowego wiadomości powitania. Blok podpisu Hello ma hello następujące wymagania:

1. sam węzeł potwierdzenia Hello muszą być podpisane.
2.  Algorytm RSA sha1 Hello musi być używany jako Metoda DigestMethod hello. Inne algorytmy podpisu cyfrowego nie są akceptowane.
   `<ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>`
3.  Możesz również uaktywnić hello dokumentu XML. 
4.  Algorytm przekształcania Hello musi pasuje do wartości hello w hello następujące przykładowe:`<ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
       <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>`
9.  Hello algorytm elementu SignatureMethod musi odpowiadać hello następujące przykładowe:`<ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>`

## <a name="supported-bindings"></a>Obsługiwane powiązania
Powiązania są transportu hello związane z nimi parametry komunikacji, które są wymagane. Witaj, następujące wymagania zastosowania toohello powiązania

1. HTTPS jest wymagane hello transportu.
2.  Usługi Azure AD będzie wymagać HTTP POST składania tokenu podczas logowania
3.  Usługi Azure AD będą używane HTTP POST dla dostawcy tożsamości toohello żądania uwierzytelniania hello i przekierowanie dla dostawcy tożsamości toohello hello wylogowywania wiadomości.

## <a name="required-attributes"></a>Wymaganych atrybutów
Ta tabela zawiera wymagania dotyczące określonych atrybutów w wiadomości powitania SAML 2.0.
 
|Atrybut|Opis|
| ----- | ----- |
|NameID|wartość Hello potwierdzenie musi hello w taki sam jak nazwę ImmutableID użytkownika hello Azure AD. Może okazać się too64 znaków alfanumerycznych. Musi być zakodowany bezpieczne znaków innych niż HTML, na przykład znak "+" jest wyświetlany jako ".2B".|
|IDPEmail|Witaj główną nazwę użytkownika (UPN) jest wymieniony w hello SAML element z hello nazw IDPEmail to jest odpowiedź UserPrincipalName hello użytkownika (UPN) w usłudze Azure AD/Office 365. Witaj głównej nazwy użytkownika jest format adresu e-mail. Wartość nazwy UPN w usłudze Office 365 (Azure Active Directory) dla systemu Windows.|
|Wystawcy|Jest to wymagane toobe identyfikatora URI hello dostawcy tożsamości. Witaj wystawca z wiadomości powitania przykładowych nie należy używać ponownie. Jeśli masz wiele domen najwyższego poziomu w powitalne dzierżaw usługi Azure AD Twojego wystawcy muszą być zgodne hello określony identyfikator URI ustawienie skonfigurowane w każdej domenie.|

>[!IMPORTANT]
>Obecnie usługa Azure AD obsługuje hello czynności NameID Format URI SAML 2.0:urn:oasis:names:tc:SAML:2.0:nameid — format: trwałych.

## <a name="sample-saml-request-and-response-messages"></a>Przykładowe komunikaty żądań i odpowiedzi SAML
Exchange logowania jednokrotnego wiadomość hello przedstawiono para komunikatów żądań i odpowiedzi.
To jest przykładowy komunikat żądania, który jest wysyłany z dostawca tożsamości SAML 2.0 próbki tooa usługi Azure AD. Dostawca tożsamości SAML 2.0 próbki Hello jest Active Directory Federation Services (AD FS) skonfigurowany toouse protokołu SAML-P. Testowania współdziałania również została ukończona z innych dostawców tożsamości SAML 2.0.

    `<samlp:AuthnRequest xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_7171b0b2-19f2-4ba2-8f94-24b5e56b7f1e" IssueInstant="2014-01-30T16:18:35Z" Version="2.0" AssertionConsumerServiceIndex="0" >
    <saml:Issuer>urn:federation:MicrosoftOnline</saml:Issuer>
    <samlp:NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
    </samlp:AuthnRequest>`

To jest przykładowy komunikat odpowiedzi, który jest wysyłany z hello próbki SAML 2.0 zgodne tożsamości dostawcy tooAzure AD / usługi Office 365.

    `<samlp:Response ID="_592c022f-e85e-4d23-b55b-9141c95cd2a5" Version="2.0" IssueInstant="2014-01-31T15:36:31.357Z" Destination="https://login.microsoftonline.com/login.srf" Consent="urn:oasis:names:tc:SAML:2.0:consent:unspecified" InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
    <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
    </samlp:Status>
    <Assertion ID="_7e3c1bcd-f180-4f78-83e1-7680920793aa" IssueInstant="2014-01-31T15:36:31.279Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>http://WS2012R2-0.contoso.com/adfs/services/trust</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      <ds:SignedInfo>
        <ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
        <ds:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1" />
        <ds:Reference URI="#_7e3c1bcd-f180-4f78-83e1-7680920793aa">
          <ds:Transforms>
            <ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature" />
            <ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#" />
          </ds:Transforms>
          <ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1" />
          <ds:DigestValue>CBn/5YqbheaJP425c0pHva9PhNY=</ds:DigestValue>
        </ds:Reference>
      </ds:SignedInfo>
      <ds:SignatureValue>TciWMyHW2ZODrh/2xrvp5ggmcHBFEd9vrp6DYXp+hZWJzmXMmzwmwS8KNRJKy8H7XqBsdELA1Msqi8I3TmWdnoIRfM/ZAyUppo8suMu6Zw+boE32hoQRnX9EWN/f0vH6zA/YKTzrjca6JQ8gAV1ErwvRWDpyMcwdYCiWALv9ScbkAcebOE1s1JctZ5RBXggdZWrYi72X+I4i6WgyZcIGai/rZ4v2otoWAEHS0y1yh1qT7NDPpl/McDaTGkNU6C+8VfjD78DrUXEcAfKvPgKlKrOMZnD1lCGsViimGY+LSuIdY45MLmyaa5UT4KWph6dA==</ds:SignatureValue>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <ds:X509Data>
          <ds:X509Certificate>MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyhBREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDTE1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9ybWVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/+3ZWxd9T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEMb2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcCAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvyJOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBySx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==</ds:X509Certificate>
        </ds:X509Data>
      </KeyInfo>
    </ds:Signature>
    <Subject>
      <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent">ABCDEG1234567890</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="_049917a6-1183-42fd-a190-1d2cbaf9b144" NotOnOrAfter="2014-01-31T15:41:31.357Z" Recipient="https://login.microsoftonline.com/login.srf" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2014-01-31T15:36:31.263Z" NotOnOrAfter="2014-01-31T16:36:31.263Z">
      <AudienceRestriction>
        <Audience>urn:federation:MicrosoftOnline</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="IDPEmail">
        <AttributeValue>administrator@contoso.com</AttributeValue>
      </Attribute>
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2014-01-31T15:36:30.200Z" SessionIndex="_7e3c1bcd-f180-4f78-83e1-7680920793aa">
      <AuthnContext>
        <AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:PasswordProtectedTransport</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
    </Assertion>
    </samlp:Response>`

## <a name="configure-your-saml-20-compliant-identity-provider"></a>Konfigurowanie dostawcy tożsamości zgodne SAML 2.0
Ten temat zawiera wskazówki dotyczące sposobu tooconfigure toofederate dostawca tożsamości SAML 2.0, tak tooone dostępu rejestracji jednokrotnej tooenable usługi Azure AD lub więcej firmy Microsoft w chmurze usług (takich jak Office 365) przy użyciu protokołu hello SAML 2.0. Witaj SAML 2.0 jednostki zależnej dla usługi w chmurze firmy Microsoft w tym scenariuszu jest usługi Azure AD.

## <a name="add-azure-ad-metadata"></a>Dodawanie metadanych usługi Azure AD
Twój dostawca tożsamości SAML 2.0 musi tooinformation tooadhere dotyczące jednostki uzależnionej hello Azure AD. Usługi Azure AD publikuje metadane na https://nexus.microsoftonline-p.com/federationmetadata/saml20/federationmetadata.xml.

Zalecane jest zawsze Importowanie metadanych hello najnowsze usługi Azure AD podczas konfigurowania Twój dostawca tożsamości SAML 2.0. Należy pamiętać, że usługi Azure AD nie odczytać metadanych z hello dostawcy tożsamości.

## <a name="add-azure-ad-as-a-relying-party"></a>Dodaj usługi Azure AD jako jednostki uzależnionej
Masz tooenable komunikacji między dostawca tożsamości SAML 2.0 i usługi Azure AD. Ta konfiguracja będzie zależało od dostawcy określonego tożsamości i należy zapoznać się toodocumentation dla niego. Można zwykle ustawić hello jednostki uzależnionej strony identyfikator toohello taki sam jak identyfikator jednostki hello z metadanych hello Azure AD.

>[!NOTE]
>Sprawdź zegara hello na serwerze dostawcy tożsamości SAML 2.0 jest synchronizowane tooan dokładnego źródła czasu. Czas zegara niedokładne może spowodować toofail logowania federacyjnego.

## <a name="install-windows-powershell-for-sign-on-with-saml-20-identity-provider"></a>Zainstaluj środowisko Windows PowerShell dla logowania jednokrotnego z dostawca tożsamości SAML 2.0
Po skonfigurowaniu dostawcy tożsamości SAML 2.0 do użytku z logowania jednokrotnego w usłudze Azure AD, hello następnym krokiem jest toodownload i zainstaluj hello Azure Active Directory modułu dla środowiska Windows PowerShell. Po zakończeniu instalacji będzie używać tych poleceń cmdlet tooconfigure domen usługi Azure AD jako Sfederowanych domen.

Hello Azure Active Directory modułu dla środowiska Windows PowerShell jest pobierania zarządzania danych organizacji w usłudze Azure AD. Ten moduł instaluje zestaw tooWindows poleceń cmdlet programu PowerShell; Uruchom te polecenia cmdlet tooset się tooAzure dostępu rejestracji jednokrotnej AD i z kolei tooall hello w chmurze usługi, które subskrybujesz. Aby uzyskać instrukcje dotyczące sposobu toodownload i zainstaluj hello poleceń cmdlet, zobacz [http://technet.microsoft.com/library/jj151815.aspx](http://technet.microsoft.com/library/jj151815.aspx)

## <a name="set-up-a-trust-between-your-saml-identity-provider-and-azure-ad"></a>Konfigurowanie relacji zaufania między dostawca tożsamości SAML i usługa Azure AD
Przed rozpoczęciem konfigurowania Federacji dla domeny usługi Azure AD, trzeba dla niego skonfigurować własną domenę niestandardową. Nie można sfederować domeny domyślnej hello zapewnianej przez firmę Microsoft. Domena domyślna Hello firmy Microsoft kończy się wyrazem "onmicrosoft.com".
Zostanie uruchomieniu serii poleceń cmdlet w tooadd interfejsu wiersza polecenia programu Windows PowerShell hello lub przekonwertować domen dla logowania jednokrotnego.

Każdej domeny usługi Azure Active Directory, która ma toofederate przy użyciu dostawcy tożsamości SAML 2.0 musi być dodany jako pojedynczą domenę logowania jednokrotnego lub przekonwertowanego toobe pojedynczą domenę logowania jednokrotnego od standardowej w domenę. Dodawanie lub Przekształcanie domeny ustanawia relację zaufania między dostawca tożsamości SAML 2.0 i usługi Azure AD.

Witaj Poniższa procedura przeprowadzi Cię przez Konwertowanie istniejącej domeny standardowe tooa domeny federacyjnej przy użyciu SAML 2.0 SP-Lite. Należy pamiętać, że domeny mogą wystąpić awaria, który ma wpływ na użytkowników w górę too2 godzin po wykonaniu tego kroku.

## <a name="configuring-a-domain-in-your-azure-ad-directory-for-federation"></a>Skonfigurowanie domeny w usłudze Azure AD Directory dla Federacji


1. Połącz tooyour katalog usługi Azure AD jako administrator dzierżawy: MsolService połączenia.
2.  Skonfiguruj żądane federacyjnym toouse domeny usługi Office 365 z SAML 2.0:`$dom = "contoso.com" $BrandName - "Sample SAML 2.0 IDP" $LogOnUrl = "https://WS2012R2-0.contoso.com/passiveLogon" $LogOffUrl = "https://WS2012R2-0.contoso.com/passiveLogOff" $ecpUrl = "https://WS2012R2-0.contoso.com/PAOS" $MyURI = "urn:uri:MySamlp2IDP" $MySigningCert = @" MIIC7jCCAdagAwIBAgIQRrjsbFPaXIlOG3GTv50fkjANBgkqhkiG9w0BAQsFADAzMTEwLwYDVQQDEyh BREZTIFNpZ25pbmcgLSBXUzIwMTJSMi0wLnN3aW5mb3JtZXIuY29tMB4XDTE0MDEyMDE1MTY0MFoXDT E1MDEyMDE1MTY0MFowMzExMC8GA1UEAxMoQURGUyBTaWduaW5nIC0gV1MyMDEyUjItMC5zd2luZm9yb WVyLmNvbTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAKe+rLVmXy1QwCwZwqgbbp1/kupQ VcjKuKLitVDbssFyqbDTjP7WRjlVMWAHBI3kgNT7oE362Gf2WMJFf1b0HcrsgLin7daRXpq4Qi6OA57 sW1YFMj3sqyuTP0eZV3S4+ZbDVob6amsZIdIwxaLP9Zfywg2bLsGnVldB0+XKedZwDbCLCVg+3ZWxd9 T/jV0hpLIIWr+LCOHqq8n8beJvlivgLmDJo8f+EITnAxWcsJUvVai/35AhHCUq9tc9sqMp5PWtabAEM b2AU72/QlX/72D2/NbGQq1BWYbqUpgpCZ2nSgvlWDHlCiUo//UGsvfox01kjTFlmqQInsJVfRxF5AcC AwEAATANBgkqhkiG9w0BAQsFAAOCAQEAi8c6C4zaTEc7aQiUgvnGQgCbMZbhUXXLGRpjvFLKaQzkwa9 eq7WLJibcSNyGXBa/SfT5wJgsm3TPKgSehGAOTirhcqHheZyvBObAScY7GOT+u9pVYp6raFrc7ez3c+ CGHeV/tNvy1hJNs12FYH4X+ZCNFIT9tprieR25NCdi5SWUbPZL0tVzJsHc1y92b2M2FxqRDohxQgJvy JOpcg2mSBzZZIkvDg7gfPSUXHVS1MQs0RHSbwq/XdQocUUhl9/e/YWCbNNxlM84BxFsBUok1dH/gzBy Sx+Fc8zYi7cOq9yaBT3RLT6cGmFGVYZJW4FyhPZOCLVNsLlnPQcX3dDg9A==" "@ $uri = "http://WS2012R2-0.contoso.com/adfs/services/trust" $Protocol = "SAMLP" Set-MsolDomainAuthentication -DomainName $dom -FederationBrandName $dom -Authentication Federated -PassiveLogOnUri $MyURI -ActiveLogOnUri $ecpUrl -SigningCertificate $MySigningCert -IssuerUri $uri -LogOffUri $url -PreferredAuthenticationProtocol $Protocol` 

3.  Możesz uzyskać hello ciąg kodowany w standardzie base64 certyfikatu z pliku metadanych IDP podpisywania. Dostarczono przykładem tej lokalizacji, ale mogą się nieznacznie różnić w implementacji.

    `<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol"> <KeyDescriptor use="signing"> <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#"> <X509Data> <X509Certificate>MIIC5jCCAc6gAwIBAgIQLnaxUPzay6ZJsC8HVv/QfTANBgkqhkiG9w0BAQsFADAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwHhcNMTMxMTA0MTgxMzMyWhcNMTQxMTA0MTgxMzMyWjAvMS0wKwYDVQQDEyRBREZTIFNpZ25pbmcgLSBmcy50ZWNobGFiY2VudHJhbC5vcmcwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQCwMdVLTr5YTSRp+ccbSpuuFeXMfABD9mVCi2wtkRwC30TIyPdORz642MkurdxdPCWjwgJ0HW6TvXwcO9afH3OC5V//wEGDoNcI8PV4enCzTYFe/h//w51uqyv48Fbb3lEXs+aVl8155OAj2sO9IX64OJWKey82GQWK3g7LfhWWpp17j5bKpSd9DBH5pvrV+Q1ESU3mx71TEOvikHGCZYitEPywNeVMLRKrevdWI3FAhFjcCSO6nWDiMqCqiTDYOURXIcHVYTSof1YotkJ4tG6mP5Kpjzd4VQvnR7Pjb47nhIYG6iZ3mR1F85Ns9+hBWukQWNN2hcD/uGdPXhpdMVpBAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAK7h7jF7wPzhZ1dPl4e+XMAr8I7TNbhgEU3+oxKyW/IioQbvZVw1mYVCbGq9Rsw4KE06eSMybqHln3w5EeBbLS0MEkApqHY+p68iRpguqa+W7UHKXXQVgPMCpqxMFKonX6VlSQOR64FgpBme2uG+LJ8reTgypEKspQIN0WvtPWmiq4zAwBp08hAacgv868c0MM4WbOYU0rzMIR6Q+ceGVRImlCwZ5b7XKp4mJZ9hlaRjeuyVrDuzBkzROSurX1OXoci08yJvhbtiBJLf3uPOJHrhjKRwIt2TnzS9ElgFZlJiDIA26Athe73n43CT0af2IG6yC7e6sK4L3NEXJrwwUZk=</X509Certificate> </X509Data> </KeyInfo> </KeyDescriptor>` 

Aby uzyskać więcej informacji na temat "Set-MsolDomainAuthentication", zobacz: [http://technet.microsoft.com/library/dn194112.aspx](http://technet.microsoft.com/library/dn194112.aspx).

>[!NOTE]
>Należy uruchomić Użyj "$ecpUrl"https://WS2012R2-0.contoso.com/PAOS"=" tylko wtedy, gdy rozszerzenie ECP skonfigurowane dla dostawcy tożsamości. Klienci usługi Exchange Online, z wyjątkiem aplikacji sieci Web programu Outlook (OWA) polegać na ogłoszenie na podstawie aktywnego punktu końcowego. Jeśli z SAML 2.0 STS implementuje aktywny punkt końcowy podobne tooShibboleth w implementacji ECP aktywnego punktu końcowego może być możliwe w dla tych klientów zaawansowanych toointeract z hello usługą Exchange Online.

Po skonfigurowano federacyjnego można przełączać za "niefederacyjnych" (lub "zarządzany"), jednak ta zmiana zajmuje toocomplete godziny tootwo i wymaga przypisywanie nowe hasła losowego chmury opartej na tooeach logowania użytkownika. Ponowne włączenie zbyt "zarządzany" może być wymagane w niektórych scenariuszach tooreset wystąpił błąd w ustawieniach. Aby uzyskać więcej informacji o konwersji domeny Zobacz: [http://msdn.microsoft.com/library/windowsazure/dn194122.aspx](http://msdn.microsoft.com/library/windowsazure/dn194122.aspx).

## <a name="provision-user-principals-tooazure-ad--office-365"></a>Zapewnij tooAzure podmiotów zabezpieczeń użytkownika AD / usługi Office 365
Zanim można uwierzytelnić użytkownika tooOffice użytkowników 365 należy udostępnić usługi Azure AD z użytkownikiem, który oświadczeń podmiotów zabezpieczeń, które odpowiadają toohello potwierdzenia w hello SAML 2.0. Jeśli te podmioty użytkownika nie są znane z wyprzedzeniem tooAzure AD następnie one nie może służyć do federacyjnego logowania. Azure AD Connect lub środowiska Windows PowerShell może być używane tooprovision podmiotów użytkownika.

Azure AD Connect mogą być używane tooprovision podmiotów tooyour domen w katalogu Azure AD z hello lokalnej usługi Active Directory. Aby uzyskać szczegółowe informacje, zobacz [integrację katalogów lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

Programu Windows PowerShell może być również używane tooautomate Dodawanie nowych użytkowników tooAzure AD a toosynchronize zmienia się z katalogiem lokalnym hello. Witaj toouse poleceń cmdlet programu Windows PowerShell, należy pobrać hello [Azure Active Directory modułów](https://docs.microsoft.com/powershell/azure/install-adv2?view=azureadps-2.0).

W tej procedurze pokazano sposób tooadd tooAzure pojedynczego użytkownika AD.


1. Połącz tooyour katalog usługi Azure AD jako administrator dzierżawy: MsolService połączenia.
2.  Utwórz nowy podmiot użytkownika:` New-MsolUser
        -UserPrincipalName elwoodf1@contoso.com
        -ImmutableId ABCDEFG1234567890
        -DisplayName "Elwood Folk"
        -FirstName Elwood 
        -LastName Folk 
        -AlternateEmailAddresses "Elwood.Folk@contoso.com" 
        -LicenseAssignment "samlp2test:ENTERPRISEPACK" 
        -UsageLocation "US" ` 

Aby uzyskać więcej informacji na temat wyboru "New-MsolUser", [http://technet.microsoft.com/library/dn194096.aspx](http://technet.microsoft.com/library/dn194096.aspx)

>[!NOTE]
>Witaj "UserPrinciplName", wartość musi odpowiadać wartości hello zostanie wysłana do "IDPEmail" oświadczenia SAML 2.0 i hello "Nazwę ImmutableID", wartość musi odpowiadać wartości hello wysyłane potwierdzenia Twojej "NameID".

## <a name="verify-single-sign-on-with-your-saml-20-idp"></a>Sprawdź rejestracji jednokrotnej z dostawców tożsamości użytkownika SAML 2.0
Jako hello administrator przed Sprawdź i zarządzanie rejestracji jednokrotnej (również o nazwie tożsamości federacyjnych), przejrzyj informacje hello i wykonaj kroki hello w hello następujące artykuły tooset się rejestracji jednokrotnej z SAML 2.0 SP-Lite dostawcy tożsamości oparte na:


1.  Należy przejrzeć hello wymagania protokołu usługi Azure AD SAML 2.0
2.  Skonfigurowano dostawcy tożsamości SAML 2.0
3.  Zainstaluj środowisko Windows PowerShell dla rejestracji jednokrotnej z dostawca tożsamości SAML 2.0
4.  Konfigurowanie relacji zaufania między dostawca tożsamości SAML 2.0 i usługi Azure AD
5.  Zainicjowano obsługę administracyjną tooAzure podmiotu zabezpieczeń użytkowników usługi Active Directory (Office 365) znane testu za pomocą środowiska Windows PowerShell lub Azure AD Connect.
6.  Konfigurowanie przy użyciu synchronizacji katalogu [Azure AD Connect](active-directory-aadconnect.md).

Po skonfigurowaniu logowania jednokrotnego SAML 2.0 SP-Lite na podstawie dostawcy tożsamości, należy sprawdzić, czy działa prawidłowo.

>[!NOTE]
>Po przekonwertowaniu domeny, zamiast dodawania co może potrwać tooset godziny too24 się rejestracji jednokrotnej.
Przed sprawdzisz logowanie jednokrotne, należy zakończyć konfigurowanie synchronizacji usługi Active Directory, zsynchronizuj swoje katalogi i Aktywuj zsynchronizowanych użytkowników.

### <a name="use-hello-tool-tooverify-that-single-sign-on-has-been-set-up-correctly"></a>Użyj hello narzędzia tooverify, że logowanie jednokrotne nie został skonfigurowany poprawnie
tooverify tej rejestracji jednokrotnej nie został skonfigurowany prawidłowo, można dokonać powitania po tooconfirm procedury są możliwe toosign toohello w usłudze w chmurze przy użyciu poświadczeń firmowych.

Firma Microsoft udostępnia narzędzia, których można używać tootest Twojego SAML 2.0 na podstawie dostawcy tożsamości. Przed uruchomieniem hello testu narzędzia należy skonfigurować toofederate dzierżawy usługi Azure AD przy pomocy dostawcy tożsamości.

>[!NOTE]
>Witaj analizatora łączności wymaga programu Internet Explorer 10 lub nowszej.



1. Pobieranie hello analizatora łączności z [https://testconnectivity.microsoft.com/?tabid=Client](https://testconnectivity.microsoft.com/?tabid=Client).
2.  Kliknij przycisk Zainstaluj teraz toobegin pobieranie i instalowanie narzędzia hello.
3.  Wybierz opcję "Nie może skonfigurować federacji z usługi Office 365, Azure lub innych usług używających usługi Azure Active Directory".
4.  Po pobraniu narzędzia hello i uruchomiona, pojawi się okno diagnostyki łączności hello. Narzędzie Hello będzie krokowo testowania połączenia federacji.
5.  Hello analizatora łączności będzie dostawców tożsamości użytkownika SAML 2.0 dla toologon można otworzyć, wprowadź poświadczenia hello hello głównej nazwy użytkownika podczas testowania: ![SAML](media/active-directory-aadconnect-federation-saml-idp/saml1.png)
6.  Na powitania federacyjnego testu w oknie rejestrowania dla dzierżawy usługi Azure AD hello, który jest skonfigurowany toobe Sfederowane przy użyciu dostawcy tożsamości SAML 2.0 należy wprowadzić nazwę konta i hasło. Narzędzie Hello podejmie toosign w użyciu tych poświadczeń i szczegółowe wyniki testów wykonanych podczas próby logowania hello zostanie podana jako dane wyjściowe.
![SAML](media/active-directory-aadconnect-federation-saml-idp/saml2.png)
7. To okno zawiera nieudanych wyników testów. Kliknięcie przeglądu szczegółowe wyniki są wyświetlane informacje o wynikach powitania dla każdego testu, która została wykonana. Można także zapisać hello toodisk wyniki w kolejności tooshare je.
 
>[!NOTE]
>Witaj analizatora łączności również testów Active Federacji przy użyciu hello WS *-protokołów opartych na i ECP/PAOS. Jeśli nie używasz te można zignorować hello następujący błąd: testowanie hello przepływu logowania Active przy użyciu dostawcy tożsamości federacyjnej Active w punkcie końcowym.

### <a name="manually-verify-that-single-sign-on-has-been-set-up-correctly"></a>Ręcznie Sprawdź, czy tej rejestracji jednokrotnej nie został skonfigurowany poprawnie
Weryfikacja ręczna udostępnia dodatkowe kroki, które należy wykonać tooensure, czy dostawca tożsamości SAML 2.0 działa prawidłowo w wielu scenariuszach.
tooverify, że logowanie jednokrotne nie został skonfigurowany prawidłowo, wykonaj następujące czynności hello kroki:


1. Na komputerze przyłączonym do domeny Zaloguj się przy użyciu hello logowania sama nazwa używana dla poświadczenia firmowe, usługa w chmurze tooyour.
2.  Kliknij wewnątrz pola hasła hello. Jeśli logowanie jednokrotne jest skonfigurowany, hello pole hasło będzie przyciemnione i zobaczą następującą wiadomości powitania: "wszystko jest teraz wymagane toosign w na <your company>."
3.  Kliknij przycisk hello Zaloguj się na stronie <your company> łącza. Jeśli jesteś stanie toosign w następnie logowania jednokrotnego nie został skonfigurowany.

## <a name="next-steps"></a>Następne kroki


- [Dostosowywanie z programem Azure AD Connect i zarządzania w usłudze Active Directory Federation Services](active-directory-aadconnect-federation-management.md)
- [Lista zgodności usługi Azure AD z usługami federacyjnymi](active-directory-aadconnect-federation-compatibility.md)
- [Instalacja niestandardowa programu Azure AD Connect](active-directory-aadconnect-get-started-custom.md)
