---
title: "aaaSigning przerzucania klucza w usłudze Azure AD | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono hello podpisywania Przerzucanie klucza najlepsze rozwiązania dotyczące usługi Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Podpisywanie przerzucania kluczy w usłudze Azure Active Directory
W tym temacie opisano, co należy tooknow o hello kluczy publicznych, które są używane w tokenach zabezpieczających toosign usługi Azure Active Directory (Azure AD). Jest ważne toonote, że te przerzucania kluczy w regularnych odstępach czasu i w razie zagrożenia, może być przerzuceniem natychmiast. Wszystkie aplikacje, które używają usługi Azure AD powinna być stanie tooprogrammatically dojście hello Przerzucanie klucza procesu lub ustanowić proces okresowej ręczne przerzucania. Kontynuuj czytanie toounderstand, jak działa hello klucze, jak tooassess hello wpływ hello przerzucania tooyour aplikacji i jak tooupdate aplikacji lub ustanawiania okresowe przerzucania ręczne Przerzucanie klucza toohandle procesu, jeśli to konieczne.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Omówienie kluczy podpisywania w usłudze Azure AD
Usługi Azure AD wykorzystuje kryptografię klucza publicznego w oparciu branżowych standardów tooestablish zaufania między sobą i hello aplikacje, które go używają. W praktyce działa to hello w następujący sposób: klucz podpisujący, który składa się z pary kluczy publicznych i prywatnych używa usługi Azure AD. Po zalogowaniu użytkownika tooan aplikacji, która używa usługi Azure AD do uwierzytelniania usługi Azure AD tworzy token zabezpieczający, który zawiera informacje o użytkowniku hello. Token ten jest podpisany przez usługę Azure AD przy użyciu jego klucz prywatny, przed wysłaniem wstecz toohello aplikacji. tooverify, który hello token jest prawidłowy i faktycznie zdalnych z usługi Azure AD, aplikacja hello zweryfikować podpisu tokenu hello przy użyciu klucza publicznego hello udostępnianych przez usługi Azure AD, który jest zawarty w dzierżawie powitalnych [OpenID Connect dokument](http://openid.net/specs/openid-connect-discovery-1_0.html) lub SAML/WS-Fed [dokument metadanych usług federacyjnych](active-directory-federation-metadata.md).

Ze względów bezpieczeństwa klucza przedstawia w regularnych odstępach czasu, a w przypadku hello awaryjnego podpisywania usługi Azure AD może być przerzuceniem natychmiast. Każda aplikacja, która integruje się z usługą Azure AD powinna być przygotowana toohandle zdarzeń przerzucania klucza nie niezależnie od tego, jak często występuje. Jeśli nie, a aplikacja próbuje toouse hello wygasłe tooverify klucza podpisu tokenu, hello logowania żądanie zakończy się niepowodzeniem.

Istnieje więcej niż jeden prawidłowy klucz dostępnych w dokumencie odnajdywania OpenID Connect hello i hello dokument metadanych usług federacyjnych. Aplikacja powinna być przygotowana toouse klawiszy hello określone w hello dokumentu, ponieważ jeden klucz mogła zostać wycofana wkrótce innego mogą być zastąpienia i tak dalej.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>Jak tooassess, jeśli będzie mieć wpływ na aplikację i jakie toodo informacji na ten temat
Jak aplikacja obsługuje Przerzucanie klucza zależy od zmienne, takie jak typ hello aplikacji lub użyto jakiego protokołu tożsamości i biblioteki. Poniższe rozdziały zawierają Hello oceny, czy hello najbardziej typowych aplikacji ma wpływ na powitania przerzucania kluczy i wytyczne dotyczące sposobu tooupdate hello automatycznego przerzucania toosupport aplikacji lub ręcznie zaktualizować hello klucza.

* [Aplikacja Native client aplikacji dostęp do zasobów](#nativeclient)
* [Aplikacje sieci Web / interfejsów API uzyskiwania dostępu do zasobów](#webclient)
* [Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzony za pomocą usługi aplikacji Azure](#appservices)
* [Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET OWIN OpenID Connect, WS-Fed lub WindowsAzureActiveDirectoryBearerAuthentication oprogramowania pośredniczącego](#owin)
* [Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET Core OpenID Connect lub JwtBearerAuthentication oprogramowania pośredniczącego](#owincore)
* [Aplikacje sieci Web / interfejsy API ochrony zasobów za pomocą modułu passport-azure-ad Node.js](#passport)
* [Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzone za pomocą programu Visual Studio 2015 lub Visual Studio 2017 r.](#vs2015)
* [Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2013](#vs2013)
* [Interfejsy API sieci Web ochrona zasobów i utworzone za pomocą programu Visual Studio 2013](#vs2013_webapi)
* [Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2012](#vs2012)
* [Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2010, o 2008 przy użyciu programu Windows Identity Foundation](#vs2010)
* [Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu dowolnego inne biblioteki lub ręcznie implementacją hello obsługiwane protokoły](#other)

Niniejsze wskazówki **nie** dotyczy:

* Aplikacje dodane z usługi Azure AD galerii aplikacji (w tym niestandardowe) mają oddzielne wytyczne z kluczami toosigning zakresie. [Więcej informacji.](../active-directory-sso-certs.md)
* Lokalne aplikacje opublikowane za pośrednictwem serwera proxy aplikacji nie ma tooworry klucze podpisywania.

### <a name="nativeclient"></a>Aplikacja Native client aplikacji dostęp do zasobów
Aplikacje, które uzyskują dostęp tylko do zasobów (tj. Microsoft Graph, KeyVault, interfejsu API programu Outlook i inne APIs firmy Microsoft) zwykle tylko uzyskania tokenu i przekazują toohello właściciela zasobów. Biorąc pod uwagę, że nie są one chronione żadnych zasobów, nie kontrolują hello token i dlatego nie ma potrzeby tooensure, który jest poprawnie podpisany.

Aplikacje klienckie natywnego, czy desktop lub mobile, do tej kategorii i w związku z tym nie dotyczy hello przerzucania.

### <a name="webclient"></a>Aplikacje sieci Web / interfejsów API uzyskiwania dostępu do zasobów
Aplikacje, które uzyskują dostęp tylko do zasobów (tj. Microsoft Graph, KeyVault, interfejsu API programu Outlook i inne APIs firmy Microsoft) zwykle tylko uzyskania tokenu i przekazują toohello właściciela zasobów. Biorąc pod uwagę, że nie są one chronione żadnych zasobów, nie kontrolują hello token i dlatego nie ma potrzeby tooensure, który jest poprawnie podpisany.

Aplikacje sieci Web i interfejsów API używanym hello przepływu tylko do aplikacji sieci web (poświadczenia klienta / certyfikatu klienta), do tej kategorii i w związku z tym nie dotyczy hello przerzucania.

### <a name="appservices"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzony za pomocą usługi aplikacji Azure
Usługa Azure App Service Authentication / automatycznie funkcjonalność autoryzacji (EasyAuth) Przerzucanie klucza toohandle niezbędne logiki hello ma już.

### <a name="owin"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET OWIN OpenID Connect, WS-Fed lub WindowsAzureActiveDirectoryBearerAuthentication oprogramowania pośredniczącego
Jeśli aplikacja używa hello .NET OWIN OpenID Connect, WS-Fed lub WindowsAzureActiveDirectoryBearerAuthentication oprogramowanie pośredniczące, jest już Przerzucanie klucza toohandle niezbędne logiki hello automatycznie.

Można potwierdzić, że aplikacja używa żadnego z nich polega na wyszukiwaniu żadnego z następujących fragmentów w pliku Startup.cs lub Startup.Auth.cs aplikacji hello

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu platformy .NET Core OpenID Connect lub JwtBearerAuthentication oprogramowania pośredniczącego
Jeśli aplikacja używa hello .NET Core OWIN OpenID Connect lub JwtBearerAuthentication oprogramowanie pośredniczące, jest już Przerzucanie klucza toohandle niezbędne logiki hello automatycznie.

Można potwierdzić, że aplikacja używa żadnego z nich polega na wyszukiwaniu żadnego z następujących fragmentów w pliku Startup.cs lub Startup.Auth.cs aplikacji hello

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów za pomocą modułu passport-azure-ad Node.js
Jeśli aplikacja używa modułu passport-ad Node.js hello, jest już Przerzucanie klucza toohandle niezbędne logiki hello automatycznie.

Sprawdź, czy aplikacja usługi passport-ad przez wyszukiwanie hello następującego fragmentu kodu w aplikacji app.js

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów i utworzone za pomocą programu Visual Studio 2015 lub Visual Studio 2017 r.
Jeśli aplikacja została skompilowana przy użyciu szablonu aplikacji sieci web w programie Visual Studio 2015 lub Visual Studio 2017 i wybrano **konta służbowego i pracy** z hello **Zmień uwierzytelnianie** menu ono już ma Przerzucanie klucza toohandle niezbędne logiki hello automatycznie. Tę logikę osadzone w oprogramowaniu pośredniczącym OWIN OpenID Connect hello, pobiera i przechowuje klucze hello z hello OpenID Connect dokument i okresowo odświeża je.

Uwierzytelniania tooyour rozwiązanie zostało dodane ręcznie, aplikacja może nie mieć hello logiki niezbędne przerzucania klucza. Konieczne będzie toowrite ją samodzielnie lub hello wykonaj kroki opisane w temacie [aplikacji sieci Web / interfejsów API przy użyciu innych biblioteki lub ręcznie implementacją hello obsługiwane protokoły.](#other).

### <a name="vs2013"></a>Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2013
Jeśli aplikacja została skompilowana przy użyciu szablonu aplikacji sieci web w programie Visual Studio 2013 i wybrano **konta organizacyjne** z hello **Zmień uwierzytelnianie** menu ma już potrzeby hello Logika toohandle klucza przerzucania automatycznie. Istotą takiej logiki przechowuje unikatowy identyfikator organizacji i hello podpisywania kluczowych informacji w dwóch tabelach bazy danych skojarzony z projektem hello. Parametry połączenia hello hello bazy danych można znaleźć w pliku Web.config hello projektu.

Uwierzytelniania tooyour rozwiązanie zostało dodane ręcznie, aplikacja może nie mieć hello logiki niezbędne przerzucania klucza. Konieczne będzie toowrite ją samodzielnie lub hello wykonaj kroki opisane w temacie [aplikacji sieci Web / interfejsów API przy użyciu innych biblioteki lub ręcznie implementacją hello obsługiwane protokoły.](#other).

następujące kroki Hello pomoże Ci Sprawdź, czy logiki hello działa prawidłowo w aplikacji.

1. W programie Visual Studio 2013, otwórz rozwiązanie hello, a następnie kliknij na powitania **Eksploratora serwera** karty w oknie prawym hello.
2. Rozwiń węzeł **połączenia danych**, **połączenia DefaultConnection**, a następnie **tabel**. Zlokalizuj hello **IssuingAuthorityKeys** tabeli, kliknij go prawym przyciskiem myszy, a następnie kliknij przycisk **Pokaż dane tabeli**.
3. W hello **IssuingAuthorityKeys** tabeli, będzie istnieć co najmniej jeden wiersz, co odpowiada wartości odcisku palca toohello hello klucza. Usuń wszystkie wiersze w tabeli hello.
4. Kliknij prawym przyciskiem myszy hello **dzierżaw** tabeli, a następnie kliknij przycisk **Pokaż dane tabeli**.
5. W hello **dzierżawców** tabeli, będzie istnieć co najmniej jeden wiersz, co odpowiada identyfikator dzierżawy unikatowy katalog tooa. Usuń wszystkie wiersze w tabeli hello. Jeśli nie usuniesz hello wierszy w obu hello **dzierżawców** tabeli i **IssuingAuthorityKeys** tabeli, wystąpi błąd w czasie wykonywania.
6. Tworzenie i uruchamianie aplikacji hello. Po zarejestrowaniu się na koncie tooyour, można zatrzymać aplikacji hello.
7. Zwraca toohello **Eksploratora serwera** i przyjrzyj się wartości hello hello **IssuingAuthorityKeys** i **dzierżawców** tabeli. Można zauważyć, że zostały one automatycznie zapełnienia hello odpowiednich informacji z hello dokument metadanych usług federacyjnych.

### <a name="vs2013"></a>Interfejsy API sieci Web ochrona zasobów i utworzone za pomocą programu Visual Studio 2013
Jeśli utworzono aplikacji interfejsu API sieci web w programie Visual Studio 2013, przy użyciu szablonu interfejsu API sieci Web hello, a następnie wybrać **konta organizacyjne** z hello **Zmień uwierzytelnianie** menu, możesz już mieć hello niezbędne logikę w aplikacji.

Jeśli ręcznie skonfigurowano uwierzytelnianie, wykonaj instrukcje hello poniżej toolearn jak tooconfigure Twojego tooautomatically interfejsu API sieci Web zaktualizować informacje klucza.

Hello poniższy fragment kodu pokazano, jak hello najnowsze kluczy z dokument metadanych usług federacyjnych hello tooget, a następnie użyj hello [programu obsługi tokenów JWT](https://msdn.microsoft.com/library/dn205065.aspx) toovalidate hello tokenu. fragment kodu Hello przyjęto założenie, użyje własne buforowanie mechanizm utrwalanie przyszłych toovalidate klucza hello tokenów z usługi Azure AD, czy jest w bazy danych, w pliku konfiguracji lub w innym miejscu.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>Aplikacje sieci Web, ochrona zasobów i utworzone za pomocą programu Visual Studio 2012
Jeśli aplikacja został utworzony w programie Visual Studio 2012, prawdopodobnie użyto hello tożsamości i tooconfigure narzędzia dostępu do aplikacji. Jest również prawdopodobne, że używasz hello [sprawdzania poprawności wystawcy nazwa rejestru (VINR)](https://msdn.microsoft.com/library/dn205067.aspx). Witaj VINR jest odpowiedzialny za konserwację informacji o zaufanych dostawców tożsamości (Azure AD) i hello klucze toovalidate tokeny wystawione przez nich. Witaj VINR ułatwia też łatwo tooautomatically aktualizacji hello klucza informacje przechowywane w pliku Web.config pobierając hello najnowsze dokument metadanych usług federacyjnych skojarzone z katalogiem sprawdzania, czy konfiguracja hello jest najnowsza wersja hello nieaktualny dokument i aktualizowania hello toouse hello nowy klucz aplikacji odpowiednio do potrzeb.

Jeśli utworzono aplikację za pomocą przykłady kodu hello lub wskazówki z dokumentacją dostarczoną przez firmę Microsoft hello logiki Przerzucanie klucza jest już uwzględniony w projekcie. Można zauważyć, że poniższy kod hello już istnieje w projekcie. Jeśli aplikacja nie ma już tę logikę, wykonaj kroki hello poniżej tooadd i tooverify, który działa prawidłowo.

1. W **Eksploratora rozwiązań**, Dodaj toohello odwołanie **System.IdentityModel** zestawu dla hello odpowiedni projekt.
2. Otwórz hello **Global.asax.cs** i dodaj następujące hello dyrektyw using:
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. Dodaj następujące metody toohello hello **Global.asax.cs** pliku:
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Wywołanie hello **RefreshValidationSettings()** metoda hello **Application_Start()** metody w **Global.asax.cs** pokazany:
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

Po wykonaniu tych kroków hello najnowsze informacje z hello dokument metadanych usług federacyjnych, w tym klucze najnowszą hello zostaną zaktualizowane pliku Web.config aplikacji. Ta aktualizacja nastąpi za każdym razem, gdy puli aplikacji jest odtwarzana w usługach IIS; Domyślnie usługi IIS jest ustawienie aplikacji toorecycle co 29 godzin.

Wykonaj kroki hello poniżej tooverify, czy działa hello logiki przerzucania klucza.

1. Po upewnieniu się, że aplikacja korzysta z kodu hello powyżej, otwórz hello **Web.config** pliku i przechodzić toohello  **<issuerNameRegistry>**  bloku, w szczególności wyszukiwanie powitania po kilku wierszy:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. W hello  **<add thumbprint=””>**  Zmień ustawienie wartości odcisku palca hello przez zamianę dowolny znak inny. Zapisz hello **Web.config** pliku.
3. Tworzenie aplikacji hello, a następnie ją uruchom. Jeśli można ukończyć procesu logowania hello, aplikacja jest pomyślnie aktualizowanie klucza hello pobierając hello wymaganych informacji z dokument metadanych usług federacyjnych w Twoim katalogu. Jeśli występują problemy dotyczące logowania, upewnij się, hello zmian w aplikacji są poprawne, odczytując hello [dodanie jednokrotne tooYour aplikacji sieci Web przy użyciu usługi Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) tematu lub pobieranie i zapoznanie się powitania po przykładowym kodzie: [ Chmury wielodostępne aplikacji dla usługi Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### <a name="vs2010"></a>Aplikacje sieci Web ochrona zasobów i utworzone za pomocą programu Visual Studio 2008 lub 2010 i .NET 3.5 w wersji 1.0 systemu Windows Identity Foundation (WIF)
Jeśli utworzono aplikację na WIF v1.0 nie ma nie podana mechanizmu odświeżania tooautomatically toouse konfiguracji aplikacji nowy klucz.

* *Najprostszym sposobem* użyj narzędzi FedUtil hello objęte hello WIF zestaw SDK, który można pobrać najnowszą wersję dokumentu metadanych hello i zaktualizowanie konfiguracji.
* Aktualizacja Twojego too.NET aplikacji 4.5, w tym hello najnowszej wersji WIF znajduje się w przestrzeni nazw systemu hello. Następnie można użyć hello [sprawdzania poprawności wystawcy nazwa rejestru (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform aktualizacje automatyczne konfiguracji aplikacji hello.
* Wykonaj ręcznie przerzucania zgodnie z instrukcjami hello na końcu hello Niniejsze wytyczne.

Instrukcje toouse hello FedUtil tooupdate konfiguracji:

1. Sprawdź, czy masz hello WIF 1.0 SDK zainstalowany na komputerze deweloperskim dla programu Visual Studio 2008 lub 2010. Możesz [go pobrać stąd](https://www.microsoft.com/en-us/download/details.aspx?id=4451) Jeśli nie został jeszcze zainstalowany go.
2. W programie Visual Studio Otwórz rozwiązanie hello, a następnie kliknij prawym przyciskiem myszy projekt dotyczy hello i wybierz **aktualizacji metadanych Federacji**. Jeśli ta opcja nie jest dostępna, FedUtil i/lub hello WIF 1.0 SDK nie został zainstalowany.
3. W wierszu hello wybierz **aktualizacji** toobegin aktualizowania metadanych federacji. Jeśli masz środowisko serwera toohello dostępu do których aplikacja hello jest obsługiwana, można używać w FedUtil [harmonogram aktualizacji automatycznych metadanych](https://msdn.microsoft.com/library/ee517272.aspx).
4. Kliknij przycisk **Zakończ** proces aktualizacji hello toocomplete.

### <a name="other"></a>Aplikacje sieci Web / interfejsy API ochrony zasobów przy użyciu dowolnego inne biblioteki lub ręcznie implementacją hello obsługiwane protokoły
Jeśli używasz niektóre inne biblioteki lub ręcznie zaimplementowana żadnego hello obsługiwanych protokołów, będziesz potrzebować tooreview hello biblioteki lub tooensure Twojego wdrożenia, który hello klucza jest pobierana z hello OpenID Connect dokument lub hello Dokument metadanych usług federacyjnych. Jednym ze sposobów toocheck dla tego jest toodo w kodzie lub kod biblioteki hello Wyszukaj wszystkie wywołania tooeither hello OpenID dokument lub hello dokument metadanych usług federacyjnych.

Jeśli klucz jest magazynowana gdzieś lub zapisane na stałe w aplikacji, możesz ręcznie pobrać klucz hello i zaktualizuj odpowiednio przez wykonuje ręczne przerzucania zgodnie z instrukcjami hello na końcu hello Niniejsze wytyczne. **Zdecydowanie zaleca się, że zwiększenia Twojej aplikacji toosupport automatycznego przerzucania** przy użyciu dowolnego hello zbliża konspektu w tym artykule tooavoid przyszłych zakłóceń i obciążenie, jeśli usługi Azure AD zwiększa jego przerzucania okresach lub ma awaryjnego przerzucania poza pasmem.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>Jak tootest Twojego toodetermine aplikacji, jeśli będzie mieć wpływ na
Można sprawdzić, czy aplikacja obsługuje automatyczne Przerzucanie klucza, pobierając hello skryptów i instrukcjami hello w [to repozytorium GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>Jak tooperform ręczne przerzucania, jeśli użytkownik aplikacji nie obsługuje automatycznego przerzucania
Jeśli aplikacja obsługuje **nie** obsługują automatyczne przerzucanie, w związku z tym należy tooestablish procesu, który okresowo podpisywania monitory usługi Azure AD kluczy i wykonuje ręczne przerzucania. [To repozytorium GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) zawiera instrukcje i skrypty toodo to.

