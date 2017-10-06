---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — Definiowanie strategii wdrażania tożsamości hybrydowej | Dokumentacja firmy Microsoft"
description: "Z kontroli dostępu warunkowego usługi Azure Active Directory sprawdza hello określonych warunków, można wybrać podczas uwierzytelniania użytkownika hello i przed zezwoleniem na dostęp toohello aplikacji. Gdy te warunki są spełnione, użytkownik hello uwierzytelniony i dozwolone dostępu toohello aplikacji."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: b92fa5a9-c04c-4692-b495-ff64d023792c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9ffca675d0c714392adfcbbc4dcfad12fccbac78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="define-a-hybrid-identity-adoption-strategy"></a>Definiowanie strategii wdrażania tożsamości hybrydowej
W tym zadaniu będziesz definiować dla hybrydowych tożsamości rozwiązania toomeet hello wymagań biznesowych, które zostały omówione w strategii wdrażania tożsamości hybrydowej hello:

* [Określanie potrzeb biznesowych](active-directory-hybrid-identity-design-considerations-business-needs.md)
* [Określenie wymagań synchronizacji katalogu](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)
* [Określić wymagania dotyczące uwierzytelniania wieloskładnikowego](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)

## <a name="define-business-needs-strategy"></a>Definiowanie strategii potrzeb biznesowych
pierwszym zadaniem Hello adresów określanie potrzeb biznesowych organizacji hello.  Może to być bardzo szeroki i zakres pełzanie może wystąpić, jeśli nie są dokładne.  Początek hello Zachowaj prostotę, ale tooplan dla projektu, który będzie pomieścić a ułatwienia zmian w przyszłości hello należy pamiętać o.  Niezależnie od tego, czy jest prostego projektu lub jeden bardzo złożonych Azure Active Directory jest hello pakietu Microsoft Identity platformy, która obsługuje usługi Office 365, Microsoft Online Services i aplikacjom obsługującym chmury.

## <a name="define-an-integration-strategy"></a>Definiowanie strategii integracji
Firma Microsoft udostępnia trzy scenariusze integracji głównego tożsamości w chmurze, tożsamości synchronizowane i tożsamości federacyjnych.  Należy zaplanować na przyjmowanie jedną z następujących strategii integracji.  Witaj strategii wybierz może różnić się i mogą obejmować hello decyzji w wybranie jednej, jakiego typu środowisko użytkownika ma tooprovide, czy masz niektórych z istniejącej infrastruktury hello już na miejscu i co to jest najbardziej ekonomiczne hello.  

![](./media/hybrid-id-design-considerations/integration-scenarios.png)

scenariusze Hello zdefiniowane w hello powyżej rysunek są następujące:

* **Tożsamości w chmurze**: są to tożsamości, które istnieją tylko w chmurze hello.  W przypadku hello Azure AD ich będzie znajdować się w katalogu usługi Azure AD.
* **Zsynchronizowane**: są to tożsamości, które są umiejscowione lokalnie i w chmurze hello.  Za pomocą usługi Azure AD Connect, użytkownicy są tworzone lub połączony z istniejących kont usługi Azure AD.  Witaj skrót hasła użytkownika są synchronizowane z hello lokalnego środowiska toohello chmury w tzw skrót hasła.  Synchronizowane przy użyciu jedno zastrzeżenie: hello jest, że wyłączenie użytkownika w środowisku lokalne powitania może potrwać zapasowej godzin too3 tooshow stan tego konta w usłudze Azure AD.  Jest to powodu toohello synchronizacji czasu interwału.
* **Federacyjna**: tymi tożsamościami istnieje lokalnie i w chmurze hello.  Za pomocą usługi Azure AD Connect, użytkownicy są tworzone lub połączony z istniejących kont usługi Azure AD.  

> [!NOTE]
> Aby uzyskać więcej informacji na temat opcji synchronizacji hello przeczytaj [integrowanie tożsamości lokalnych z usługą Azure Active Directory](connect/active-directory-aadconnect.md).
> 
> 

Witaj w poniższej tabeli pomogą w określeniu hello zalety i wady każdego z następujących strategii hello:

| Strategia | Zalety | Wady |
| --- | --- | --- |
| **Tożsamości w chmurze** |Łatwiejsze toomanage dla małych organizacji. <br> Nie jest potrzebny dodatkowy sprzęt na — lokalnym — bez tooinstall<br>Jeśli hello użytkownik opuści firmę hello łatwo wyłączone |Użytkownicy muszą toosign w przypadku uzyskiwania dostępu do obciążeń w chmurze hello <br> Hasła może lub nie może być hello takie same dla tożsamości w chmurze i lokalnie |
| **Zsynchronizowane** |Lokalnego hasła będzie uwierzytelnienia zarówno lokalnie oraz katalogi w chmurze <br>Łatwiejsze toomanage dla małych, średnich i dużych organizacji <br>Użytkownicy mogą mieć rejestracji jednokrotnej (SSO) dla niektórych zasobów <br> Metoda Microsoft preferowany do synchronizacji <br> Łatwiejsze toomanage |Niektórzy klienci mogą być zniechęcić toosynchronize ich katalogów z hello chmury powodu polecenie określonej firmy |
| **Federacyjna** |Użytkownicy mogą mieć rejestracji jednokrotnej (SSO) <br>Jeśli użytkownik zostanie zakończony, pozostawia hello konta można natychmiast wyłączone, a dostęp odwołać,<br> Obsługa zaawansowanych scenariuszy nie może być realizowane za pomocą synchronizacji |Więcej kroki toosetup i skonfigurować <br> Wyższy konserwacji <br> Może wymagać dodatkowego sprzętu hello STS infrastruktury <br> Może wymagać dodatkowego sprzętu tooinstall hello federacyjnego serwera. Dodatkowe oprogramowanie jest wymagany, jeśli jest używany przez usługi AD FS <br> Wymagaj szeroką gamę Instalatora dla logowania jednokrotnego <br> Krytyczne punktu awarii, jeśli serwer federacyjny hello jest wyłączony, użytkownicy nie będą mogli tooauthenticate |

### <a name="client-experience"></a>Środowisko pracy klienta
strategii Hello, którego używasz wyznaczają hello użytkownika logowania.  Witaj poniższe tabele zawierają się, że informacje o ich logowania oczekiwać co użytkownicy hello występują toobe.  Należy zauważyć, że nie wszyscy dostawcy tożsamości federacyjnych obsługuje logowania jednokrotnego we wszystkich scenariuszach.

**Aplikacje przyłączone domena, jak i prywatnych sieci**:

|  | Tożsamości synchronizowane | Tożsamości federacyjnych |
| --- | --- | --- |
| Przeglądarki sieci Web |Uwierzytelnianie oparte na formularzach |funkcji logowania jednokrotnego, czasami wymagany identyfikator organizacji toosupply |
| Outlook |Monit o podanie poświadczeń |Monit o podanie poświadczeń |
| Skype dla firm (Lync) |Monit o podanie poświadczeń |logowania jednokrotnego dla Lync, monitowanie o poświadczenia dla programu Exchange |
| SkyDrive Pro |Monit o podanie poświadczeń |Logowanie jednokrotne |
| Office Pro Plus subskrypcji |Monit o podanie poświadczeń |Logowanie jednokrotne |

**Zewnętrznych lub niezaufanych źródeł**:

|  | Tożsamości synchronizowane | Tożsamości federacyjnych |
| --- | --- | --- |
| Przeglądarki sieci Web |Uwierzytelnianie oparte na formularzach |Uwierzytelnianie oparte na formularzach |
| Outlook i Skype dla firm (Lync), Skydrive Pro subskrypcji pakietu Office |Monit o podanie poświadczeń |Monit o podanie poświadczeń |
| Program Exchange ActiveSync |Monit o podanie poświadczeń |logowania jednokrotnego dla Lync, monitowanie o poświadczenia dla programu Exchange |
| Aplikacje mobilne |Monit o podanie poświadczeń |Monit o podanie poświadczeń |

W przypadku podjęcia decyzji z zadanie 1, czy masz 3rd strony toouse będzie IdP lub mają jeden tooprovide federacji z usługą Azure AD, należy pamiętać o następujących hello toobe obsługiwane możliwości:

* Wszelkie dostawcy SAML 2.0, który jest zgodny z dla hello SP Lite profilu może obsługiwać uwierzytelnianie tooAzure AD i skojarzone aplikacje
* Obsługuje pasywnym uwierzytelnianie, która ułatwia tooOWA uwierzytelniania, SPO, itp.
* Klienci usługi Exchange Online mogą być obsługiwane za pośrednictwem hello SAML 2.0 rozszerzone klienta profilu (ECP)

Należy wziąć pod uwagę jakie funkcje przestaną być dostępne:

* Bez obsługi zaufania/federacyjnych w sieci Web spowoduje przerwanie wszystkich aktywnych klientów
  * Oznacza to, że nie klienta Lync, klient usługi OneDrive, subskrypcji pakietu Office, Office Mobile wcześniejsze tooOffice 2016
* Przejście uwierzytelniania toopassive Office pozwolą toosupport czysty SAML 2.0 IdPs, ale obsługa nadal będzie na podstawie klienta przez klienta

> [!NOTE]
> Dla hello hello artykułu http://aka.ms/ssoproviders odczytać najnowsze listy.
> 
> 

## <a name="define-synchronization-strategy"></a>Definiowanie strategii synchronizacji
To zadanie będzie definiował hello narzędzia, które będą używane toosynchronize hello organizacji danych lokalnych w chmurze toohello i co należy używać topologii.  Ponieważ większość organizacji używa usługi Active Directory, informacji o korzystaniu z usługi Azure AD Connect tooaddress hello pytania powyżej podano niektóre szczegółowe.  W środowiskach, które nie ma usługi Active Directory ma informacji o korzystaniu z programu FIM 2010 R2 lub toohelp MIM 2016 planowanie tej strategii.  Jednak przyszłych wersjach programu Azure AD Connect będzie obsługiwać katalogów LDAP, więc w zależności od osi czasu, te informacje mogą być w stanie tooassist.

### <a name="synchronization-tools"></a>Narzędzia do synchronizacji
Latach hello kilka narzędzi synchronizacji ma istniał i używane dla różnych scenariuszy.  Azure AD Connect jest obecnie hello Przejdź tootool z rozwiązaniem w przypadku wszystkich obsługiwanych scenariuszy.  AAD Sync DirSync są nadal wokół i może nawet występować w danym środowisku teraz. 

> [!NOTE]
> Aby hello najnowsze informacje dotyczące hello obsługiwane możliwości narzędzia, przeczytaj [porównanie narzędzi integracji katalogów](active-directory-hybrid-identity-design-considerations-tools-comparison.md) artykułu.  
> 
> 

### <a name="supported-topologies"></a>Obsługiwane topologie
Podczas definiowania strategii synchronizacji, należy określić topologię hello, która jest używana. W zależności od hello informacje, które zostało ustalone w kroku 2, można określić, która topologia jest hello prawidłowego toouse jeden. Witaj pojedynczy las, pojedynczy topologii usługi Azure AD hello najbardziej typowe i składa się z jednego lasu usługi Active Directory i jedno wystąpienie usługi Azure AD.  To jest używane w większości scenariuszy hello toobe i jest hello oczekiwano topologii w przypadku przy użyciu usługi Azure AD Connect Express instalacji, jak pokazano na poniższej ilustracji hello.

![](./media/hybrid-id-design-considerations/single-forest.png)Pojedynczy las scenariusz jest często stosowane w organizacjach dużych i małych nawet toohave wielu lasów, jak pokazano na rysunku 5.

> [!NOTE]
> Aby uzyskać więcej informacji na temat hello różnych lokalnymi i topologii usługi Azure AD z synchronizacji Azure AD Connect, przeczytaj artykuł hello [topologii dla usługi Azure AD Connect](connect/active-directory-aadconnect-topologies.md).
> 
> 

![](./media/hybrid-id-design-considerations/multi-forest.png) 

Scenariusza obejmującego wiele lasów

Jeżeli przypadek hello następnie hello kilku forest jednym topologii usługi Azure AD należy rozważyć, jeśli hello są spełnione następujące warunki:

* Użytkownicy mają tylko 1 tożsamości we wszystkich lasach — Witaj, który unikatowo identyfikuje użytkowników poniższej sekcji opisano to bardziej szczegółowo.
* Witaj, użytkownik jest uwierzytelniany toohello lesie, w którym znajduje się ich tożsamości
* UPN i zakotwiczenie źródła (niezmienialnego identyfikatora) będą pochodzić z tego lasu
* Wszystkich lasach są dostępne przy użyciu usługi Azure AD Connect — oznacza to toobe przyłączone do domeny, nie jest konieczne, a jeśli ułatwia to można umieścić w strefie DMZ.
* Użytkowników ma tylko jedną skrzynkę pocztową
* Hello lasu, który hostuje skrzynki pocztowej użytkownika ma hello najlepszą jakość danych dla atrybutów widoczne w hello globalne listy adresów (GAL) programu Exchange
* Jeśli na powitania użytkownika jest nie skrzynki pocztowej, a następnie dowolnym lesie mogą być używane toocontribute te wartości
* Jeśli masz połączoną skrzynkę pocztową, występuje także innego konta w toosign innego lasu używane w.

> [!NOTE]
> Obiekty, które istnieją w swoich lokalnych i w chmurze hello "połączenie" za pośrednictwem Unikatowy identyfikator. W kontekście hello synchronizacji katalogów ten unikatowy identyfikator jest hello tooas określonego SourceAnchor. W kontekście hello z logowania jednokrotnego to hello tooas określono nazwę ImmutableId. [Zagadnienia dotyczące projektowania programu Azure AD Connect](connect/active-directory-aadconnect-design-concepts.md#sourceanchor) więcej uwagi dotyczące użycia hello elementu SourceAnchor.
> 
> 

Jeśli masz więcej niż jedno konto active lub więcej niż jedną skrzynkę pocztową hello powyżej nie są spełnione, Azure AD Connect wybierz jedną i Ignoruj hello innych.  Jeśli istnieje łącze skrzynek pocztowych, ale żadne inne konto, tych kont nie będzie eksportowany tooAzure AD i że użytkownik nie będzie członkiem żadnej grupy.  To różni się od sposobu był hello poza z narzędzia DirSync i jest zamierzone toobetter obsługi tych scenariuszy obejmujących wiele lasów. Hello rysunku poniżej przedstawiono scenariusza obejmującego wiele lasów.

![](./media/hybrid-id-design-considerations/multiforest-multipleAzureAD.png) 

**Obejmującego wiele lasów wielu scenariusza usługi Azure AD**

Zaleca się, że toohave jest tylko jeden katalog w usłudze Azure AD dla organizacji, ale obsługuje ona relację 1:1 jest przechowywane między serwerem synchronizacji Azure AD Connect i katalog usługi Azure AD.  Dla każdego wystąpienia usługi Azure AD konieczne będzie instalacji programu Azure AD Connect.  Ponadto usługi Azure AD, zgodnie z projektem jest izolowana i użytkowników w jednym wystąpieniu usługi Azure AD nie będą mogli toosee użytkowników w innym wystąpieniu.

Możliwe jest i obsługiwanych tooconnect, jeden lokalne wystąpienie usługi Active Directory katalogów usługi Azure AD toomultiple pokazane na poniższej ilustracji hello:

![](./media/hybrid-id-design-considerations/single-forest-flitering.png) 

**Scenariusz filtrowania pojedynczego lasu**

W kolejności toodo tego hello musi być spełnione następujące warunki:

* Serwery synchronizacji usługi Azure AD Connect musi być skonfigurowana do filtrowania, każdy z nich ma wykluczają się wzajemnie zestaw obiektów.  To zrobić, na przykład przez zakresu każdego serwera tooa określonej domeny lub jednostki Organizacyjnej.
* Domena DNS mogą być rejestrowane tylko w jednym katalogu usługi Azure AD, dlatego hello nazwy UPN użytkowników hello w hello lokalnej usługi AD, należy użyć oddzielnych przestrzenie nazw
* Użytkownicy w jednym wystąpieniu usługi Azure AD będą tylko użytkownicy mogli toosee z ich wystąpienia.  One nie będą mieć użytkownicy mogli toosee hello innych wystąpień
* Tylko jeden z katalogów hello Azure AD można włączyć Exchange hybrydowe z hello lokalnej usługi AD
* Wzajemne wyłączności ma również zastosowanie toowrite Wstecz.  Dzięki temu niektórych funkcji zapisywania zwrotnego nie są obsługiwane z tej topologii, ponieważ te założono konfiguracji pojedynczym lokalnym.  Obejmuje to:
  * Grupuj zapisu z konfiguracji domyślnej
  * Zapisywanie zwrotne urządzeń

Należy pamiętać, że następujący hello nie jest obsługiwane i nie powinna być wybrana jako implementacji:

* Nie jest obsługiwane toohave wielu serwerów synchronizacji Azure AD Connect łączenie toohello usługi Azure AD w tym samym katalogu, nawet jeśli są skonfigurowane toosynchronize wykluczają się wzajemnie zestaw obiektów
* Jest on nieobsługiwany toosync hello samych katalogach toomultiple usługi Azure AD użytkownika. 
* Możliwe jest również nieobsługiwany toomake zmiana konfiguracji użytkowników toomake w jednym tooappear usługi Azure AD jako kontaktuje się w innym katalogu usługi Azure AD. 
* Możliwe jest również nieobsługiwany toomodify Azure AD Connect synchronizacji tooconnect toomultiple usługi Azure AD katalogów.
* Katalogów usługi Azure AD są zgodne z założeniami samodzielnie. Taka konfiguracja hello nieobsługiwany toochange danych tooread synchronizacji Azure AD Connect z innego katalogu usługi Azure AD w toobuild próba typowe i ujednoliconego usługi GAL między katalogami hello jest. Jest również użytkownikom tooexport nieobsługiwany kontaktuje się tooanother lokalnej usłudze AD za pomocą synchronizacji usługi Azure AD Connect.

> [!NOTE]
> Jeśli Twoja organizacja ogranicza komputerów w sieci łączenie toohello Internet, w tym artykule wymieniono hello endpoints (nazw FQDN, IPv4 i zakresy adresów IPv6), które należy uwzględnić w Twojej wychodzącego Zezwalaj, list i Internet Explorer Zaufane witryny programu tooensure komputery klienckie komputery pomyślnie można korzystać z usługi Office 365. Aby uzyskać więcej informacji, przeczytaj [zakresów adresów IP i URL usługi Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US).
> 
> 

## <a name="define-multi-factor-authentication-strategy"></a>Definiowanie strategii uwierzytelniania wieloskładnikowego
W ramach tego zadania, który będzie definiował hello toouse strategii uwierzytelniania wieloskładnikowego.  Uwierzytelnianie wieloskładnikowe platformy Azure jest dostarczany w dwóch różnych wersji.  Jedną jest oparty na chmurze i lokalne za pomocą serwera usługi Azure MFA hello jest hello innych.  Oparte na ocenie hello, powyżej, które można określić, które rozwiązanie jest hello właściwy dla strategii.  Użyj hello tabelę poniżej toodetermine, który projekt opcję najlepiej spełniać wymagania dotyczące zabezpieczeń firmy:

Opcje projektu wieloskładnikowego:

| Toosecure zasobów | Uwierzytelniania MFA w chmurze hello | Lokalna usługa MFA |
| --- | --- | --- |
| Aplikacje firmy Microsoft |Tak |Tak |
| Aplikacji SaaS w galerii aplikacji hello |Tak |Tak |
| Aplikacje usług IIS opublikowane za pośrednictwem serwera proxy aplikacji usługi Azure AD |Tak |Tak |
| Aplikacji programu IIS nie są publikowane w powitania serwera Proxy aplikacji usługi Azure AD |Brak |Tak |
| Dostępu zdalnego sieci VPN, Brama usług pulpitu zdalnego |Brak |Tak |

Nawet jeśli użytkownik może mieć rozliczenia na rozwiązanie dla strategii, należy nadal oceny hello toouse z powyższych, na którym znajdują się użytkownicy.  Może to spowodować hello toochange rozwiązania.  Użyj tabeli hello poniżej tooassist możesz określania to:

| Lokalizacja użytkownika | Opcja preferowane rozwiązanie |
| --- | --- |
| Usługa Azure Active Directory |Multi-FactorAuthentication w chmurze hello |
| Usługa Azure AD i lokalna usługa AD przy użyciu federacji z usługami AD FS |Zarówno |
| Usługi Azure AD i lokalnymi AD za pomocą usługi Azure AD Connect nie synchronizacji haseł |Zarówno |
| Usługi Azure AD i lokalnymi za pomocą usługi Azure AD Connect z synchronizacją haseł |Zarówno |
| Lokalne usługi AD |Serwer Multi-Factor Authentication |

> [!NOTE]
> Należy również upewnić, że hello uwierzytelnianie wieloskładnikowe projektowania opcja obsługuje hello funkcje, które są wymagane dla projektu.  Aby uzyskać więcej informacji, przeczytaj [wybierz rozwiązanie z zakresu zabezpieczeń wieloskładnikowego hello](../multi-factor-authentication/multi-factor-authentication-get-started.md#what-am-i-trying-to-secure).
> 
> 

## <a name="multi-factor-auth-provider"></a>Dostawca uwierzytelniania MFA
Usługa Multi-Factor authentication jest dostępna domyślnie dla administratorów globalnych dzierżawiących usługę Azure Active Directory. Jednak jeśli chcesz tooextend tooall uwierzytelnianie wieloskładnikowe dla użytkowników lub mają tooyour Administratorzy globalni toobe tootake mogli korzystać funkcje, takie jak hello portalu zarządzania, niestandardowe pozdrowienia oraz raportów, następnie należy kupić i skonfigurować Dostawca usługi Multi-Factor Authentication.

> [!NOTE]
> Należy również upewnić, że hello uwierzytelnianie wieloskładnikowe projektowania opcja obsługuje hello funkcje, które są wymagane dla projektu. 
> 
> 

## <a name="next-steps"></a>Następne kroki
[Określenie wymagań dotyczących ochrony danych](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)

