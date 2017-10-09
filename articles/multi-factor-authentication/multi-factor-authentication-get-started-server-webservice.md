---
title: "Usługa sieci Web aplikacji mobilnej serwera usługi MFA aaaAzure | Dokumentacja firmy Microsoft"
description: "Aplikacja Microsoft Authenticator Hello udostępnia opcję dodatkowego uwierzytelniania poza pasmem.  Umożliwia on hello MFA serwera toouse wypychania powiadomień toousers."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 6c8d6fcc-70f4-4da4-9610-c76d66635b8b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 4175b68fcbf85ec3fd53d8edf4e07306c75a4c71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-mobile-app-authentication-with-azure-multi-factor-authentication-server"></a>Włączanie uwierzytelniania aplikacji mobilnych za pomocą serwera usługi Azure Multi-Factor Authentication

Aplikacja Microsoft Authenticator Hello udostępnia opcję dodatkowej weryfikacji poza pasmem. Zamiast wprowadzania do automatycznego połączenia telefonicznego lub SMS toohello użytkownika podczas logowania, uwierzytelnianie wieloskładnikowe Azure wypycha aplikacji Microsoft Authenticator toohello powiadomień na smartfonie lub tablecie hello użytkownika. powitania po prostu naciśnięciu **Sprawdź** (lub wprowadza numeru PIN i naciska "Uwierzytelnij") w hello toocomplete aplikacji zalogowania.

Korzystanie z aplikacji mobilnej w celu weryfikacji dwuetapowej jest preferowane, jeśli zasięg telefonu jest niestabilny. Jeśli używasz aplikacji hello jako generator tokenu OATH nie wymaga żadnych połączenia sieciowego lub internet.

W zależności od środowiska, może być usługi sieci web aplikacji mobilnej hello toodeploy na powitania tego samego serwera jako serwera usługi Azure Multi-Factor Authentication lub na innym serwerze skierowane do Internetu.

## <a name="requirements"></a>Wymagania

aplikacji Microsoft Authenticator hello toouse, następujące hello są wymagane hello aplikacji mogą się komunikować z usługą sieci Web aplikacji mobilnej:

* Korzystanie z serwera usługi Azure Multi-Factor Authentication w wersji 6.0 lub nowszej.
* Zainstalowanie usługi sieci Web aplikacji mobilnej na dostępnym z Internetu serwerze sieci Web z uruchomionymi usługami Microsoft® [Internet Information Services (IIS) w wersji 7.x lub nowszej](http://www.iis.net/).
* Pozycję ASP.NET v4.0.30319 jest zainstalowany, zarejestrowane i ustaw tooAllowed
* Wymagane usługi ról obejmują usługę ASP.NET oraz usługę zgodności z metabazą usług IIS 6.
* Udostępnienie usługi sieci Web aplikacji mobilnej za pośrednictwem publicznego adresu URL.
* Zabezpieczenie usługi sieci Web aplikacji mobilnej za pomocą certyfikatu SSL.
* Zainstaluj hello Azure Multi-Factor Authentication Web Service SDK w usługach IIS 7.x lub nowszej na powitania **tym samym serwerze co powitania serwera usługi Azure Multi-Factor Authentication**
* Hello Azure Multi-Factor Authentication Web Service SDK jest zabezpieczony za pomocą certyfikatu SSL.
* Usługa sieci Web aplikacji mobilnej można połączyć toohello Azure Multi-Factor Authentication Web Service SDK za pośrednictwem protokołu SSL
* Mobile App Web Service może uwierzytelnić toohello usługi Web Service SDK usługi Azure MFA przy użyciu poświadczeń konta usługi, który jest członkiem grupy zabezpieczeń "Administratorzy aplikacji PhoneFactor" hello hello. Tego konta usługi i grupy istnieje w usłudze Active Directory, jeśli powitania serwera usługi Azure Multi-Factor Authentication znajduje się na serwerze przyłączonym do domeny. Na powitania serwera usługi Azure Multi-Factor Authentication istnieje lokalnie tego konta usługi i grupy, ponieważ nie jest tooa przyłączone do domeny.

## <a name="install-hello-mobile-app-web-service"></a>Instalowanie usługi sieci web aplikacji mobilnej hello

Przed zainstalowaniem usługi sieci web aplikacji mobilnej hello, należy pamiętać o hello poniższe informacje:

* Musisz mieć konto usługi będą częścią grupy „PhoneFactor Admins”. To konto może być taki sam, jak jeden hello używane do instalacji portalu użytkowników hello hello.
* Jest przydatne tooopen przeglądarki sieci web na serwerze sieci web internetowy hello i przejdź do adresu URL toohello hello zestawu SDK usług sieci Web, wprowadzony w pliku web.config hello. Jeśli hello przeglądarki może pomyślnie uzyskać toohello usługi sieci web, jego powinien monit o poświadczenia. Wprowadź hello użytkownika i hasło, które zostały wprowadzone w pliku web.config hello dokładnie w takiej postaci, w jakiej występuje w pliku hello. Upewnij się, że nie są wyświetlane żadne ostrzeżenia ani błędy dotyczące certyfikatów.
* Zwrotnego serwera proxy lub zapory jest obecne przed serwera sieci web hello Mobile App Web Service, wykonywanie SSL Odciążanie można edytować pliku web.config hello Mobile App Web Service, dzięki czemu hello Mobile App Web Service może używać protokołu http zamiast https. Protokół SSL jest nadal wymagana od hello proxy zapory odwrotnego toohello aplikacji mobilnej. Dodaj hello następującego klucza toohello \<appSettings\> sekcji:

        <add key="SSL_REQUIRED" value="false"/>

### <a name="install-hello-web-service-sdk"></a>Instalowanie zestawu SDK usług sieci web hello

W każdym z tych scenariuszy, jeśli hello Azure Multi-Factor Authentication Web Service SDK jest **nie** już zainstalowane na powitania serwera usługi Azure Multi-Factor Authentication (MFA), pełny hello kroków poniżej.

1. Otwórz program hello aplikacji serwer Multi-Factor Authentication.
2. Przejdź toohello **zestawu SDK usług sieci Web** i wybierz **Zainstaluj usługę Web Service SDK**.
3. Zainstaluj pełną hello przy użyciu wartości domyślnych hello, chyba że potrzebne toochange ich jakiegoś powodu.
4. Powiązania witryny toohello certyfikatu SSL w usługach IIS.

Jeśli masz pytania dotyczące konfigurowania certyfikatu SSL na serwerze IIS, zobacz artykuł hello [jak tooSet zabezpieczeń SSL w usługach IIS](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Witaj zestawu SDK usług sieci Web musi być zabezpieczona za pomocą certyfikatu SSL. W tym celu wystarczy certyfikat z podpisem własnym. Zaimportuj certyfikat hello w magazynie "Zaufane główne urzędy certyfikacji" hello hello konta komputera lokalnego na serwerze sieci web portalu użytkowników hello, tak, aby podczas inicjowania połączenia SSL hello zaufany certyfikat.

![Ustawienia konfiguracji serwera usługi MFA — zestaw SDK usługi internetowej](./media/multi-factor-authentication-get-started-server-webservice/sdk.png)

### <a name="install-hello-service"></a>Zainstaluj usługę hello

1. **Na powitania serwera usługi MFA**, Przeglądaj toohello ścieżki instalacji.
2. Przejdź toohello folder powitania serwera usługi Azure MFA w przypadku domyślnego zainstalowanych hello jest **uwierzytelnianie wieloskładnikowe Files\Azure C:\Program**.
3. Zlokalizuj plik instalacyjny hello **MultiFactorAuthenticationMobileAppWebServiceSetup64**. Jeśli serwer hello jest **nie** internetowy, kopiowania hello instalacji pliku toohello internetowy serwer.
4. Jeśli hello jest serwer usługi MFA **nie** toohello przełącznika internetowy **internetowy serwer**.
5. Uruchom hello **MultiFactorAuthenticationMobileAppWebServiceSetup64** instalowanie plików jako administrator, zmień hello lokacji, w razie potrzeby i zmienić hello wirtualnej katalogu tooa krótką nazwę, jeśli chcesz.
6. Po przeprowadzeniu instalacji hello zakończenia, Przeglądaj zbyt**C:\inetpub\wwwroot\MultiFactorAuthMobileAppWebService** (lub odpowiedniego katalogu na podstawie nazwy katalogu wirtualnego hello) i edytowania pliku Web.Config hello.

   * Znajdź klucz hello **"Wartość pozycji WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** i zmienić **wartość = ""** za**wartość = "Domena\użytkownik"** domena\nazwa użytkownika w przypadku konta usługi, który jest częścią Grupy "Administratorzy aplikacji PhoneFactor".
   * Znajdź klucz hello **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** i zmienić **wartość = ""** za**wartość = "Password"** gdzie hasło jest hasło hello hello usługi Wprowadzona w poprzednim wierszu hello konta.
   * Znajdź hello **pfMobile aplikacji sieci Web Service_pfwssdk_PfWsSdk** ustawienie i zmień wartość hello z **http://localhost:4898/PfWsSdk.asmx** toohello adres URL zestawu SDK usługi sieci Web (przykład: https://mfa.contoso.com/ MultiFactorAuthWebServiceSdk/PfWsSdk.asmx).
   * Zapisz plik Web.Config hello i zamknij Notatnik.

   > [!NOTE]
   > Ponieważ protokół SSL jest używany dla tego połączenia, należy wskazać hello zestawu SDK usług sieci Web przez **pełną nazwę domeny (FQDN)** i **nie adres IP**. Hello certyfikat SSL czy zostały wystawione dla hello nazwy FQDN i hello adres URL używany musi odpowiadać hello nazwa hello certyfikatu.

7. Witaj witryny sieci Web, który Mobile App Web Service została zainstalowana w nie ma już powiązany z publicznie podpisany certyfikat, zainstaluj certyfikat hello na powitania serwera, otwórz Menedżera usług IIS i powiązać hello certyfikatu toohello witryny sieci Web.
8. Otwórz przeglądarkę sieci web za pomocą dowolnego komputera i adres URL toohello zainstalowaną Mobile App Web Service nawigacji (przykład: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService). Upewnij się, że nie są wyświetlane żadne ostrzeżenia ani błędy dotyczące certyfikatów.

## <a name="configure-hello-mobile-app-settings-in-hello-azure-multi-factor-authentication-server"></a>Skonfiguruj ustawienia aplikacji mobilnej hello na powitania serwera usługi Azure Multi-Factor Authentication

Usługa sieci web aplikacji mobilnej hello jest zainstalowana, trzeba tooconfigure powitania serwera usługi Azure Multi-Factor Authentication toowork hello Portal.

1. W konsoli serwera Multi-Factor Authentication hello kliknij ikonę Portal użytkowników hello. Sprawdź ich metod uwierzytelniania, jeśli użytkownicy mogą toocontrol **aplikacji mobilnej** na karcie Ustawienia hello, w obszarze **użytkownicy metody tooselect**. Bez ta funkcja jest włączona, użytkownicy końcowi są wymagane toocontact proces aktywacji toocomplete działu pomocy technicznej dla hello aplikacji mobilnej.
2. Sprawdź hello **Zezwalaj tooactivate użytkowników aplikacji mobilnej** pole.
3. Sprawdź hello **Zezwalaj na rejestrowanie użytkowników** pole.
4. Kliknij przycisk hello **aplikacji mobilnej** ikony.
5. Wprowadź adres URL hello używany z hello katalogu wirtualnego, który został utworzony podczas instalowania MultiFactorAuthenticationMobileAppWebServiceSetup64 (przykład: https://mfa.contoso.com/MultiFactorAuthMobileAppWebService/) w polu hello  **Adres URL usługi sieci Web aplikacji mobilnej:**.
6. Wypełnij hello **nazwa konta** pole z hello toodisplay nazwy firmy lub organizacji w aplikacji mobilnej powitania dla tego konta.
   ![Ustawienia aplikacji mobilnej konfiguracji serwera usługi MFA](./media/multi-factor-authentication-get-started-server-webservice/mobile.png)

## <a name="next-steps"></a>Następne kroki

- [Zaawansowane scenariusze obejmujące usługę Azure Multi-Factor Authentication i sieci VPN innych firm](multi-factor-authentication-advanced-vpn-configurations.md).