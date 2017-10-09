---
title: "aaaSecurity najlepsze rozwiązania dotyczące uwierzytelniania Wieloskładnikowego | Dokumentacja firmy Microsoft"
description: "Ten dokument zawiera najlepsze rozwiązania w zakresie obsługi za pomocą usługi Azure MFA z kontami usługi Azure"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7f18c2592764878b842d81783b321a05f29ee3d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a>Najlepsze rozwiązania dotyczące korzystania z usługi Azure Multi-Factor Authentication z konta usługi Azure AD

Weryfikacja dwuetapowa to wybór hello preferowane w przypadku większości organizacji, które mają tooenhance procesu uwierzytelniania. Usługa Azure Multi-Factor Authentication (MFA) pomaga firm, które spełnia ich wymagania dotyczące zabezpieczeń i zgodności, zapewniając prostych środowiska logowania dla użytkowników. W tym artykule przedstawiono kilka wskazówek, które należy wziąć pod uwagę podczas planowania hello przyjęcia usługi Azure MFA.

## <a name="deploy-azure-mfa-in-hello-cloud"></a>Wdrażanie usługi Azure MFA w chmurze hello

Istnieją dwa sposoby tooenable usługi Azure MFA dla wszystkich użytkowników.

* Kupowanie licencji dla każdego użytkownika (albo usługi Azure MFA, Azure AD Premium lub Enterprise Mobility + Security)
* Tworzenie dostawcy uwierzytelniania wieloskładnikowego i płatności dla poszczególnych użytkowników lub uwierzytelnienia

### <a name="licenses"></a>Licencje
![PAKIET EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

Jeśli masz Azure AD Premium lub pakietu Enterprise Mobility + Security licencji, masz już usługi Azure MFA. Twoja organizacja nie wymaga cokolwiek dodatkowe tooextend hello dwuetapowej weryfikacji możliwości tooall użytkowników. Wystarczy tooassign tooa licencji użytkownika, a następnie włączyć uwierzytelnianie wieloskładnikowe.

Podczas konfigurowania uwierzytelniania wieloskładnikowego, należy wziąć pod uwagę następujące wskazówki hello:

* Nie należy tworzyć dostawcę uwierzytelniania wieloskładnikowego na uwierzytelniania. Jeśli to zrobisz, może się okazać płatności weryfikacji żądań od użytkowników, którzy już mają licencje.
* Jeśli nie masz wystarczającą liczbę licencji dla wszystkich użytkowników, można utworzyć użytkownika dostawcy uwierzytelniania wieloskładnikowego toocover hello reszty Twojej organizacji. 
* Azure AD Connect jest tylko wymagane, jeśli synchronizacji w lokalnym środowisku usługi Active Directory z katalogu usługi Azure AD. Jeśli używasz katalog usługi Azure AD, która nie jest zsynchronizowany z lokalnego wystąpienia usługi Active Directory, nie trzeba Azure AD Connect.

### <a name="multi-factor-auth-provider"></a>Dostawca uwierzytelniania MFA
![Dostawca uwierzytelniania MFA](./media/multi-factor-authentication-security-best-practices/authprovider.png)

Jeśli nie masz licencji, które obejmują usługi Azure MFA, można utworzyć dostawcy uwierzytelniania MFA. 

Podczas tworzenia hello dostawca usługi MFA, należy tooselect katalogu i należy wziąć pod uwagę hello poniższe informacje:

* Nie trzeba toocreate katalogu usługi Azure AD dostawca uwierzytelniania MFA, ale uzyskać więcej funkcji z jednym. Witaj, następujące funkcje są włączone po skojarzeniu hello dostawca usługi MFA z katalogu usługi Azure AD:  
  * Rozszerzanie tooall weryfikacji dwuetapowej użytkowników  
  * Oferują dodatkowe funkcje, takie jak portal zarządzania hello, niestandardowe pozdrowienia i raporty z administratorów globalnych.
* Po zsynchronizowaniu w lokalnym środowisku usługi Active Directory z katalogiem Azure AD, należy narzędzia DirSync i AAD Sync. Jeśli używasz katalog usługi Azure AD, która nie jest zsynchronizowany z lokalnego wystąpienia usługi Active Directory, nie trzeba narzędzia DirSync i AAD Sync.
* Wybierz model zużycie hello, najlepiej pasujące do firmy. Po wybraniu hello użycia modelu nie można go zmienić. są dwa modele Hello:
  * Na uwierzytelniania: można opłaty za każdy weryfikacji. Ten model należy użyć, jeśli włączono weryfikację dwuetapową dla każdego, który uzyskuje dostęp do niektórych aplikacji, a nie dla konkretnych użytkowników.
  * Każdego włączonego użytkownika: użytkownik opłaty za każdy użytkownik, który można włączyć usługi Azure MFA. Ten model użycia w przypadku niektórych użytkowników z usługi Azure AD Premium lub pakietu Enterprise Mobility Suite licencji, a niektóre bez.

### <a name="supportability"></a>Możliwości obsługi
Ponieważ większość użytkowników są przystosowane toousing tooauthenticate tylko hasła, ważne jest, że firmy powoduje świadomości tooall użytkowników dotyczące tego procesu. Tego pogłębianie wiedzy na temat zmniejszyć hello prawdopodobieństwo, że użytkownicy wywołać dział pomocy technicznej tooMFA powiązane drobne problemy. Istnieją sytuacje, w których czasowo wyłączyć uwierzytelnianie wieloskładnikowe jest konieczne. Użyj hello następujące wytyczne toounderstand jak toohandle tych scenariuszy:

* Szkolenie gdzie hello użytkownik może zalogować ponieważ hello aplikacji mobilnej lub telefon nie odbiera powiadomienia lub połączeń telefonicznych scenariuszy toohandle personelu pomocy technicznej. Pomoc techniczna może [włączyć jednorazowe obejście](multi-factor-authentication-whats-next.md#one-time-bypass) tooallow tooauthenticate użytkownika jeden raz, pomijając"" weryfikacji dwuetapowej. Witaj obejście jest tymczasowe i wygasa po określonym czasie.
* Należy wziąć pod uwagę hello [możliwości zaufanych adresów IP](multi-factor-authentication-whats-next.md#trusted-ips) w usługi Azure MFA jako weryfikacji dwuetapowej toominimize sposób. Przy użyciu tej funkcji Administratorzy dzierżawy zarządzane lub federacyjnych można pominąć weryfikacji dwuetapowej dla użytkowników, którzy są logujący się z firmy hello lokalny intranet. Funkcje Hello są dostępne dla dzierżaw usługi Azure AD, którzy mają licencje usługi Azure AD Premium, Enterprise Mobility Suite lub Azure Multi-Factor Authentication.

## <a name="best-practices-for-an-on-premises-deployment"></a>Najlepsze rozwiązania dotyczące wdrożenia lokalnego
Jeśli firma zdecydowała tooleverage tooenable własnej infrastruktury usługi MFA, należy toodeploy lokalne serwera usługi Azure Multi-Factor Authentication. składniki serwera usługi MFA Hello są pokazane w powitania po diagramu:

![Domyślne składniki serwera usługi MFA: konsoli, aparatu synchronizacji, portalu zarządzania usługą w chmurze](./media/multi-factor-authentication-security-best-practices/server.png) \*nie jest instalowany domyślnie \** zainstalowany, lecz nie jest włączona domyślnie

Azure aplikacji serwer Multi-Factor Authentication można zabezpieczyć chmury zasobów lokalnych i w zasoby przy użyciu federacji. Musisz mieć usług AD FS i jego Sfederowanych z dzierżawy usługi Azure AD.
Podczas konfigurowania serwera Multi-Factor Authentication, należy wziąć pod uwagę hello poniższe informacje:

* Jeśli to zabezpieczania zasobów usługi Azure AD przy użyciu usługi Active Directory Federation Services (AD FS), a następnie hello pierwszym krokiem weryfikacji jest wykonywane lokalnie za pomocą usług AD FS. drugi etap Hello jest realizowany lokalnie przy zachowaniu hello oświadczeń.
* Nie masz tooinstall powitania serwera usługi Azure Multi-Factor Authentication serwera federacyjnego usług AD FS. Jednak hello karty uwierzytelniania wieloskładnikowego usług AD FS musi być zainstalowany w systemie Windows Server 2012 R2 uruchomionymi usługami AD FS. Można zainstalować serwera hello na innym komputerze, tak długo, jak jest obsługiwana wersja i oddzielnego instalowania adaptera ADFS hello AD na serwerze federacyjnym usług AD FS. 
* Kreator instalacji usługi Multi-Factor Authentication AD FS karty Hello tworzy grupę zabezpieczeń o nazwie PhoneFactor Admins w usłudze Active Directory, a następnie dodaje grupę toothis kont usługi AD FS. Sprawdź, czy hello grupy PhoneFactor Admins został utworzony na kontrolerze domeny i konta usługi hello AD FS jest członkiem tej grupy. W razie potrzeby dodaj hello usług AD FS usługi konta toohello grupy PhoneFactor Admins na kontrolerze domeny ręcznie.

### <a name="user-portal"></a>Portal użytkowników
portal użytkowników Hello umożliwia funkcji samoobsługi i zapewnia pełny zestaw możliwości administrowania użytkownika. Działa on w witrynie sieci web usług Internet Information Server (IIS). Użyj następujących wytycznych tooconfigure hello tego składnika:

* Korzystanie z usług IIS 6 lub nowszego
* Zainstaluj i zarejestruj ASP.NET v2.0.507207
* Upewnij się, że ten serwer można wdrożyć w sieci obwodowej

### <a name="app-passwords"></a>Hasła aplikacji
Jeśli Twoja organizacja jest Sfederowane dla rejestracji Jednokrotnej z usługą Azure AD i ma toobe przy użyciu usługi Azure MFA, następnie należy pamiętać o hello poniższe informacje:

* hasła aplikacji Hello jest weryfikowany przez usługę Azure AD i w związku z tym pomija federacji. Federacyjnej jest używana tylko podczas konfigurowania haseł aplikacji.
* Dla użytkowników federacyjnych (SSO) hasła są przechowywane w hello identyfikatora organizacyjnego. Jeśli hello użytkownik opuści firmę hello, że informacje o identyfikatorze tooflow tooorganizational przy użyciu narzędzia DirSync. Wyłączenie/usunięcie konta może trwać toothree toosync godzin, które opóźnienie wyłączenia/usunięcia hasła aplikacji w usłudze Azure AD.
* Ustawienia lokalnej kontroli dostępu klienta nie są uznawane przez hasło aplikacji.
* Możliwość rejestrowania/inspekcji nie lokalnego uwierzytelniania jest dostępna dla hasła aplikacji.
* Niektóre zaawansowane architektury projekty mogą wymagać przy użyciu kombinacji organizacji nazwy użytkownika i hasła i haseł aplikacji, gdy z klientami, w zależności od tego, gdzie uwierzytelniania przy użyciu weryfikacji dwuetapowej. Dla klientów, którzy uwierzytelniania względem infrastruktury lokalnej użyje organizacyjnej nazwy użytkownika i hasła. Dla klientów, którzy uwierzytelniania usługi Azure AD należy użyć hasła aplikacji hello.
* Domyślnie użytkownicy nie mogą tworzyć hasła aplikacji. Hasła aplikacji toocreate użytkowników tooallow, należy wybrać hello **Zezwalaj toosign hasła aplikacji toocreate użytkowników w aplikacjach korzystających z przeglądarki** opcji.

## <a name="additional-considerations"></a>Dodatkowe uwagi
Użyj tej listy, aby uzyskać dodatkowe informacje i wskazówki dotyczące każdego składnika, który jest wdrożony na lokalnym:

- Konfigurowanie usługi Multi-Factor Authentication w usługach [Active Directory Federation Services](multi-factor-authentication-get-started-adfs.md).
- Instalowanie i konfigurowanie serwera usługi Azure MFA z hello [uwierzytelnianie usługi RADIUS](multi-factor-authentication-get-started-server-radius.md).
- Instalowanie i konfigurowanie serwera usługi Azure MFA z hello [uwierzytelniania usług IIS](multi-factor-authentication-get-started-server-iis.md).
- Instalowanie i konfigurowanie serwera usługi Azure MFA z hello [uwierzytelniania systemu Windows](multi-factor-authentication-get-started-server-windows.md).
- Instalowanie i konfigurowanie serwera usługi Azure MFA z hello [uwierzytelniania LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Instalowanie i konfigurowanie serwera usługi Azure MFA z hello [bramy usług pulpitu zdalnego i Azure przy użyciu usługi RADIUS serwera Multi-Factor Authentication](multi-factor-authentication-get-started-server-rdg.md).
- Instalowanie i Konfigurowanie synchronizacji między powitania serwera usługi Azure MFA i [usługi Active Directory systemu Windows Server](multi-factor-authentication-get-started-server-dirint.md).
- [Wdrażanie hello Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).
- [Zaawansowana konfiguracja sieci VPN z uwierzytelnianiem wieloskładnikowym Azure](multi-factor-authentication-advanced-vpn-configurations.md) dla urządzenia Cisco ASA, Citrix Netscaler i Juniper/Pulse Secure VPN przy użyciu protokołu LDAP lub serwera RADIUS.

## <a name="next-steps"></a>Następne kroki
Chociaż ten artykuł zawiera opis najlepsze rozwiązania dla usługi Azure MFA, istnieją inne zasoby, które można również użyć podczas planowania wdrożenia usługi MFA. Hello lista poniżej zawiera niektóre klucza artykuły, które mogą pomóc w trakcie tego procesu:

* [Raporty w uwierzytelnianie wieloskładnikowe platformy Azure](multi-factor-authentication-manage-reports.md)
* [środowisko rejestracji weryfikacji dwuetapowej Hello](multi-factor-authentication-end-user-first-time.md)
* [Uwierzytelnianie wieloskładnikowe platformy Azure — często zadawane pytania](multi-factor-authentication-faq.md)

