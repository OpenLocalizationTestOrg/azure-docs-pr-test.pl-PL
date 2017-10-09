---
title: "aaaWhat jest dostęp do aplikacji i logowanie jednokrotne w usłudze Azure Active Directory? | Microsoft Docs"
description: "Za pomocą usługi Azure Active Directory tooenable pojedynczego logowania jednokrotnego tooall aplikacji sieci web i SaaS hello wymagające dla firm."
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 75d1a3fd-b3c5-4495-a5c8-c4c24145ff00
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curyand
ms.openlocfilehash: 429522cbd570ab27359c4630c5a6d7b25b692ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-application-access-and-single-sign-on-with-azure-active-directory"></a>Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?
Logowanie jednokrotne oznacza, że jest w stanie tooaccess wszystkich aplikacji hello i zasobów potrzebnych firm toodo, logując się tylko raz przy użyciu jednego konta użytkownika. Po zalogowaniu możesz uzyskać dostęp do wszystkich aplikacji hello należy nie jest wymagane tooauthenticate (np. Wpisz hasło) po raz drugi.

W wielu organizacjach opierają się na oprogramowania jako aplikacje usługi (SaaS), takich jak Office 365, pole i Salesforce na produktywność użytkownika końcowego. W przeszłości personel działu informatycznego musi tooindividually tworzenie i aktualizowanie kont użytkowników w każdej aplikacji SaaS, a użytkownicy mają tooremember hasła dla każdej aplikacji SaaS.

Azure Active Directory rozszerza w lokalnej usłudze Active Directory w chmurze hello włączenie toouse użytkowników podstawowego konta organizacyjnego toonot tylko logowania tootheir urządzeń przyłączonych do domeny i zasobów firmy, ale również wszystkich hello sieci web i aplikacji SaaS potrzebne do ich pracy.

Więc nie tylko użytkownicy nie mają toomanage wiele zestawów nazw użytkowników i hasła, aplikacjach dostępu mogą być automatycznie udostępniane lub usuwane oparty na ich elementy członkowskie grupy organizacji i ich stan jako pracowników. Usługa Azure Active Directory wprowadzono zabezpieczeń i formantami ładu dostępu, które umożliwiają możesz toocentrally zarządzanie dostępem użytkowników do aplikacji SaaS.

Usługi Azure AD umożliwia łatwą integrację toomany współczesnych popularnych aplikacji SaaS; Umożliwia zarządzanie tożsamościami i dostępem i umożliwia użytkownikom toosingle logowania jednokrotnego tooapplications bezpośrednio, lub odnajdywania i uruchamiania ich z portalu, takich jak usługi Office 365 lub hello panel dostępu usługi Azure AD.

Architektura Hello integracji hello składa się z hello następujących czterech głównych elementów:

* Logowanie jednokrotne umożliwia użytkownikom tooaccess aplikacji SaaS, ich oparte na swoje konta organizacyjne w usłudze Azure AD. Logowanie jednokrotne jest to, co umożliwia aplikacji tooan tooauthenticate użytkowników przy użyciu pojedynczego konta organizacyjnego.
* Inicjowanie obsługi użytkowników umożliwia użytkownika aprowizację i anulowanie obsługi do obiektu docelowego, który SaaS na podstawie zmian wprowadzonych w systemie Windows Server Active Directory i/lub Azure AD. Udostępnione konta jest toouse toobe autoryzowanych użytkowników aplikacji, co umożliwia po uwierzytelnienia za pośrednictwem rejestracji jednokrotnej.
* Umożliwia aplikacji scentralizowanego zarządzania dostępem w portalu zarządzania Azure hello pojedynczy punkt SaaS dostęp do aplikacji i zarządzania, z hello możliwości toodelegate aplikacji dostępu decyzji wprowadzania i zatwierdzeń tooanyone w organizacji hello
* Jednolite raportowanie i monitorowania aktywności użytkowników w usłudze Azure AD

## <a name="how-does-single-sign-on-with-azure-active-directory-work"></a>Jak działa logowanie jednokrotne z usługą Azure Active Directory?
Po "loguje" tooan aplikację użytkownika, komputery przechodzą przez proces uwierzytelniania gdy są one wymagane tooprove, w którym się znajdują, który mówią, że są one. Bez rejestracji jednokrotnej, jest to zazwyczaj wykonywane przez wprowadzenie hasła, które są przechowywane w aplikacji hello i użytkownik hello jest tooknow wymagane hasło.

Usługi Azure AD obsługuje trzy różne sposoby toosign w tooapplications:

* **Federacyjne logowanie jednokrotne** umożliwia aplikacji tooredirect tooAzure AD do uwierzytelniania użytkowników zamiast monitowanie o własnego hasła. Jest to obsługiwane w przypadku aplikacji obsługa protokołów, takich jak SAML 2.0, WS-Federation lub OpenID Connect, i jest hello najszerszym tryb rejestracji jednokrotnej.
* **Oparte na hasłach rejestracji jednokrotnej** umożliwia bezpiecznego magazynu haseł aplikacji i powtarzania przy użyciu rozszerzenia przeglądarki sieci web lub aplikacji mobilnej. Wykorzystuje hello istniejącego procesu logowania dostarczone przez aplikację hello, ale umożliwia hasła administratora toomanage hello i nie wymagają hello użytkownika tooknow hello hasła.
* **Istniejące rejestracji jednokrotnej** włącza wszystkie istniejące rejestracji jednokrotnej, który został skonfigurowany do aplikacji hello, ale umożliwia te aplikacje toohello toobe połączone usługi Office 365 lub portale panel dostępu usługi Azure AD, a także umożliwia tooleverage usługi Azure AD dodatkowe raporty w usłudze Azure AD, gdy istnieje uruchamiania aplikacji hello.

Gdy użytkownik ma uwierzytelnienie przy użyciu aplikacji, muszą toohave rekord konta zainicjowane w aplikacji hello, która określa, że aplikacja hello gdzie istnieje uprawnienia i poziom dostępu są wewnątrz aplikacji hello. Witaj inicjowania obsługi administracyjnej z tego konta można albo automatycznie są wykonywane, lub może być wykonywane ręcznie przez administratora przed hello użytkownik ma możliwość dostępu rejestracji jednokrotnej.

 Więcej informacji na temat pojedynczego logowania jednokrotnego trybów i Inicjowanie obsługi poniżej.

### <a name="federated-single-sign-on"></a>Federacyjne logowanie jednokrotne
Federacyjne logowanie jednokrotne umożliwia logowania jednokrotnego hello użytkownicy w Twojej organizacji toobe, zostanie automatycznie zalogowany aplikacji SaaS innych firm tooa przez usługę Azure AD przy użyciu hello informacje o koncie użytkownika z usługi Azure AD.

W tym scenariuszu po możesz już zostały zarejestrowane w usłudze Azure Active Directory, a użytkownik chce tooaccess zasoby, które są kontrolowane przez innych firm aplikacji SaaS, federacyjnego eliminuje potrzebę hello toobe użytkownika, ponownie uwierzytelnieni.

Usługi Azure AD mogą obsługiwać federacyjne logowanie jednokrotne z aplikacjami, które obsługują hello SAML 2.0, WS-Federation, lub OpenID connect protokołów.

Zobacz też: [zarządzanie certyfikatami dla federacyjnych rejestracji jednokrotnej](active-directory-sso-certs.md)

### <a name="password-based-single-sign-on"></a>Oparte na hasłach rejestracji jednokrotnej
Konfigurowanie opartego na hasłach logowania jednokrotnego pozwala użytkownikom hello w Twojej organizacji toobe, zostanie automatycznie zalogowany aplikacji SaaS innych firm tooa przez usługę Azure AD przy użyciu informacji o koncie użytkownika hello z aplikacji SaaS hello innych firm. Po włączeniu tej funkcji usługi Azure AD zbiera i bezpiecznie przechowuje informacje o koncie użytkownika hello i hello powiązane hasło.

Usługi Azure AD można obsługiwać opartego na hasłach jednokrotnego żadnych chmurowych aplikacji, który ma oparty na języku HTML strony logowania. Za pomocą wtyczki przeglądarki niestandardowych, automatyzuje logowania użytkownika hello w procesie za pośrednictwem bezpiecznego pobierania poświadczeń aplikacji, takich jak hello nazwy użytkownika i hasła hello z katalogu hello AAD i wejścia stronę logowania aplikacji hello te poświadczenia w imieniu użytkownika hello. Istnieją dwa przypadki użycia:

1. **Administrator zarządza poświadczeniami** — Administratorzy mogą tworzyć i zarządzać poświadczeń aplikacji i przypisać te poświadczenia toousers lub grupy, które muszą uzyskać dostęp do aplikacji toohello. W takich przypadkach hello użytkownika końcowego nie potrzebuje tooknow hello poświadczeń, ale nadal uzyska dostępu rejestracji jednokrotnej toohello aplikacji po prostu, klikając go w ich panelu dostępu lub przy użyciu podanego łącza. Dzięki temu zarówno zarządzania cyklem życia hello poświadczeń administratora hello, a także wygody dla użytkowników końcowych, zgodnie z którymi nie wymagają tooremember lub zarządzać hasłami specyficzny dla aplikacji. poświadczenia Hello są zaciemniona z hello użytkownika końcowego podczas automatycznego logowania hello w procesie; jednak znajdują się pod względem technicznym wykrywalny przez użytkownika hello za pomocą debugowania sieci web narzędzia, a użytkownicy i Administratorzy, należy wykonać bezpośrednio przez użytkownika hello przedstawiono hello tych samych zasad zabezpieczeń tak, jakby hello poświadczeń. Poświadczenia administratora są bardzo przydatne podczas tworzenia konta dostępu, który jest współużytkowane przez wielu użytkowników, takich jak mediami społecznościowymi lub aplikacji do udostępniania dokumentu.
2. **Użytkownik zarządza poświadczeniami** — Administratorzy mogą przypisywać aplikacji tooend użytkowników lub grup i Zezwalaj tooenter użytkownicy końcowi hello poświadczeń bezpośrednio na uzyskiwanie dostępu do aplikacji hello na powitania po raz pierwszy w ich panelu dostępu. Spowoduje to utworzenie udogodnienie dla użytkowników końcowych, zgodnie z którymi toocontinually nie muszą wprowadzać haseł specyficzny dla aplikacji hello każdej próbie dostępu aplikacji hello. Ten przypadek użycia mogą służyć jako wykonywania krokowego zarządzania skalnej tooadministrative hello poświadczeń, zgodnie z którymi hello administrator może skonfigurować nowe poświadczenia dla aplikacji hello w przyszłości bez zmieniania aplikacji hello dostępu środowisko użytkownika końcowego hello.

W obu przypadkach poświadczenia są przechowywane w zaszyfrowanej stanu w katalogu hello i tylko są przekazywane za pośrednictwem protokołu HTTPS podczas procesu hello automatycznego logowania. Za pomocą opartego na hasłach rejestracji jednokrotnej na, usługi Azure AD oferuje wygodny dostępu rozwiązania do zarządzania tożsamościami dla aplikacji, które nie są w stanie obsłużyć protokoły federacji.

Na podstawie hasła logowania jednokrotnego opiera się na przeglądarce rozszerzenia toosecurely pobrać hello aplikacji i użytkownika określone informacje z usługi Azure AD i zastosować je toohello usługi. Większość aplikacji SaaS innych firm, które są obsługiwane przez usługę Azure AD obsługuje tę funkcję.

Logowanie Jednokrotne opartego na hasłach można przeglądarki hello przez użytkownika końcowego:

* Internet Explorer 8, 9, 10, 11 — w systemie Windows 7 lub nowszy (Zobacz też [Podręcznik wdrażania programu Internet Explorer rozszerzenia](active-directory-saas-ie-group-policy.md))
* Chrome — W systemie Windows 7 lub nowszy oraz System MacOS x lub nowszych
* Firefox 26.0 lub później — w systemie Windows XP z dodatkiem SP2 lub nowszy oraz w systemie Mac OS X 10,6 lub nowszy

**Uwaga:** hello opartego na hasłach logowania jednokrotnego rozszerzenia staną się dostępne Edge w systemie Windows 10, gdy staną się również obsługiwany rozszerzenia przeglądarki Edge.

### <a name="existing-single-sign-on"></a>Istniejące rejestracji jednokrotnej
Podczas konfigurowania rejestracji jednokrotnej dla aplikacji, hello portalu zarządzania Azure udostępnia trzecia opcja z "istniejącej rejestracji jednokrotnej". Ta opcja po prostu umożliwia hello administrator toocreate aplikacji tooan łącza i umieść ją na powitania panel dostępu dla wybranych użytkowników.

Na przykład jeśli istnieje, że aplikacja, która jest skonfigurowana tooauthenticate użytkowników przy użyciu Active Directory Federation Services 2.0, administrator może użyć hello "istniejącej rejestracji jednokrotnej" opcja toocreate tooit łącza na powitania panelu dostępu. Gdy użytkownicy uzyskują dostęp do łącza hello, ich uwierzytelniania przy użyciu Active Directory Federation Services 2.0, lub niezależnie od jednego logowania jednokrotnego rozwiązania jest zapewniana przez aplikację hello.

### <a name="user-provisioning"></a>Inicjowanie obsługi użytkowników
Wybierz aplikacje usługi Azure AD umożliwia automatyczne użytkownika aprowizację i anulowanie obsługi kont w innych firm aplikacji SaaS z wewnątrz hello portalu zarządzania Azure, przy użyciu informacji o tożsamości systemu Windows Server Active Directory lub Azure AD. Gdy użytkownik otrzymuje uprawnienia w usłudze Azure AD dla jednej z tych aplikacji, konta mogą być automatycznie tworzone (udostępnione) w celu hello aplikacji SaaS.

Po usunięciu użytkownika lub ich informacje zmian w usłudze Azure AD, te zmiany są również odzwierciedlane w hello aplikacji SaaS. Oznacza to, że zarządzanie cyklem życia tożsamości automatyczne konfigurowanie umożliwia administratorom toocontrol i podaj zautomatyzowaną aprowizację i anulowanie obsługi z poziomu aplikacji SaaS. W usłudze Azure AD ta Automatyzacja zarządzania cyklem życia tożsamości jest włączana przez Inicjowanie obsługi użytkowników.

toolearn więcej, zobacz [tooSaaS automatyczne Inicjowanie obsługi użytkowników i anulowania zastrzeżenia aplikacji](active-directory-saas-app-provisioning.md)

## <a name="get-started-with-hello-azure-ad-application-gallery"></a>Rozpoczynanie pracy z galerią aplikacji usługi Azure AD hello
Rozpoczęto gotowe tooget? toodeploy rejestracji jednokrotnej między usługą Azure AD i aplikacji SaaS, które organizacja używa, postępuj zgodnie z poniższymi wskazówkami.

### <a name="using-hello-azure-ad-application-gallery"></a>Za pomocą galerii aplikacji hello Azure AD
Witaj [galerii aplikacji programu Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/) zawiera listę aplikacji, które są znane toosupport formularza rejestracji jednokrotnej z usługą Azure Active Directory.

![][1]

Poniżej przedstawiono kilka wskazówek do znajdowania aplikacji przez jakie funkcje, które obsługują:

* Usługi Azure AD obsługuje automatyczną aprowizację i anulowanie obsługi dla wszystkich aplikacji "Proponowanym" w hello [galerii aplikacji programu Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/).
* Wykaz aplikacji federacyjnych w szczególności obsługiwać federacyjnym logowaniem jednokrotnym przy użyciu protokołu, takich jak SAML, WS-Federation, lub OpenID Connect można znaleźć [tutaj](http://social.technet.microsoft.com/wiki/contents/articles/20235.azure-active-directory-application-gallery-federated-saas-apps.aspx).

Po znalezieniu aplikacji, można rozpocząć hello krok po kroku instrukcje przedstawione w galerii aplikacji hello i w tooenable portalu zarządzania Azure hello logowanie jednokrotne.

### <a name="application-not-in-hello-gallery"></a>Aplikacji nie znajduje się w galerii hello?
Jeśli aplikacja nie zostanie znaleziony w galerii aplikacji usługi Azure AD hello, masz następujące opcje:

* **Dodaj nieznajdujące się na liście aplikacji są za pomocą** -Użyj kategorię niestandardową hello w galerii aplikacji hello w portalu zarządzania platformy Azure hello — tooconnect nieznajdujące się na liście aplikacji korzystających z Twojej organizacji. Możesz dodać dowolnej aplikacji, który obsługuje SAML 2.0 jako aplikacji federacyjnych lub dowolnej aplikacji, która jest oparty na języku HTML strony logowania jako aplikację hasło logowania jednokrotnego. Aby uzyskać więcej informacji, zobacz ten artykuł w [Dodawanie własnych aplikacji](active-directory-saas-custom-apps.md).
* **Dodaj własną aplikację, tworzysz** — Jeśli korzystasz z aplikacji hello samodzielnie, jest zgodna z wytycznymi hello w hello Azure AD developer dokumentacji tooimplement federacyjnego logowania jednokrotnego lub inicjowanie obsługi przy użyciu hello interfejsu API programu graph usługi Azure AD. Aby uzyskać więcej informacji zobacz następujące zasoby:
  
  * [Scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md)
  * [https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet](https://github.com/AzureADSamples/WebApp-WebAPI-MultiTenant-OpenIdConnect-DotNet)
  * [https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore](https://github.com/AzureADSamples/NativeClient-WebAPI-MultiTenant-WindowsStore)
* **Żądanie integracji aplikacji** -żądania pomocy technicznej dla aplikacji hello należy za pomocą hello [forum opinii usługi Azure AD](https://feedback.azure.com/forums/169401-azure-active-directory/).

### <a name="using-hello-azure-management-portal"></a>Za pomocą portalu zarządzania Azure hello
Hello rozszerzenie usługi Active Directory można użyć w hello Azure Management Portal tooconfigure hello aplikacji rejestracji jednokrotnej. Pierwszym krokiem należy tooselect katalog z sekcji usługi Active Directory w portalu hello hello:

![][2]

toomanage aplikacji SaaS innych firm, można przełączyć na kartę aplikacji hello hello wybrany katalog. Ten widok umożliwia administratorom:

* Dodaj nowe aplikacje z galerii Azure AD hello, a także aplikacje, które tworzysz
* Usuń zintegrowanych aplikacji
* Zarządzanie aplikacjami hello, które już zostały zintegrowana

Typowe zadania administracyjne dla aplikacji SaaS innych firm są:

* Włączanie rejestracji jednokrotnej z usługą Azure AD przy użyciu hasła logowania jednokrotnego lub, jeśli jest dostępna dla docelowej hello SaaS, Federacyjna usługa rejestracji Jednokrotnej
* Opcjonalnie włączenie użytkownika inicjowania obsługi administracyjnej dla użytkownika aprowizację i anulowanie obsługi (Zarządzanie cyklem życia tożsamości)
* Dla aplikacji, których inicjowanie obsługi użytkowników jest włączone, Wybieranie użytkowników, którzy mają dostęp do aplikacji toothat

Do galerii aplikacji, które obsługują federacyjnego logowania jednokrotnego Konfiguracja zwykle wymaga tooprovide dodatkowe ustawienia konfiguracji, takich jak certyfikaty i toocreate metadanych federacyjnych relacji zaufania między hello aplikacji innych firm i Azure AD. Kreator konfiguracji Hello przedstawiono szczegóły hello i udostępnia użytkownikowi łatwy dostęp toohello dane specyficzne dla aplikacji SaaS i instrukcje.

W przypadku aplikacji galerii zapewniające obsługę użytkowników wymaga możesz toogive usługi Azure AD uprawnienia toomanage kont użytkownika w aplikacji SaaS hello. Co najmniej należy tooprovide poświadczeń usługi Azure AD powinien używać podczas uwierzytelniania za pośrednictwem toohello aplikacji docelowej. Określa, czy ustawienia dodatkowe czynności konfiguracyjne należy toobe podane zależy od wymagań hello aplikacji hello.

## <a name="deploying-azure-ad-integrated-applications-toousers"></a>Wdrażanie usługi Azure AD zintegrowane aplikacje toousers
Usługa Azure AD zapewnia różne sposoby dostosowania toodeploy aplikacji tooend — użytkownicy w Twojej organizacji:

* Panel dostępu usługi Azure AD
* Uruchamianie aplikacji usługi Office 365
* Aplikacje toofederated bezpośredniego logowania jednokrotnego
* Toofederated głębokiego łącza, oparte na hasłach lub istniejących aplikacjach

Które metody wybierzesz toodeploy w organizacji jest uznania.

### <a name="azure-ad-access-panel"></a>Panel dostępu usługi Azure AD
Witaj panelu dostępu pod https://myapps.microsoft.com jest portal sieci web, który umożliwia użytkownikowi końcowemu za pomocą konta organizacyjnego w usłudze Azure Active Directory tooview i uruchamiania toowhich aplikacji opartych na chmurze, które zostały one udzielony dostęp przez hello Azure AD Administrator. Jeśli jesteś użytkownika końcowego z [Azure Active Directory Premium](https://azure.microsoft.com/pricing/details/active-directory/), można również korzystać z funkcji zarządzania grupami samoobsługi za pośrednictwem hello panelu dostępu.

![][3]

Witaj Panel dostępu jest oddzielony od hello portalu zarządzania Azure i nie wymaga toohave użytkownicy subskrypcji platformy Azure lub subskrypcji usługi Office 365.

Aby uzyskać więcej informacji na panelu dostępu hello Azure AD, zobacz hello [panelu dostępu toohello wprowadzenie](active-directory-saas-access-panel-introduction.md).

### <a name="office-365-application-launcher"></a>Uruchamianie aplikacji usługi Office 365
Aplikacje przypisane toousers za pośrednictwem usługi Azure AD dla organizacji, które zostały wdrożone usługi Office 365, również pojawi się w portalu usługi Office 365 hello https://portal.office.com/myapps. To ułatwia wygodne dla użytkowników w organizacji toolaunch swoje aplikacje bez potrzeby toouse drugi portalu i hello zaleca aplikacji Uruchamianie rozwiązania dla organizacji przy użyciu usługi Office 365.

![][4]

Aby uzyskać więcej informacji na temat uruchamiania aplikacji hello usługi Office 365, zobacz [mają aplikacji są wyświetlane na ekranie uruchamiania aplikacji hello usługi Office 365](https://msdn.microsoft.com/office/office365/howto/connect-your-app-to-o365-app-launcher).

### <a name="direct-sign-on-toofederated-apps"></a>Aplikacje toofederated bezpośredniego logowania jednokrotnego
Większość aplikacji federacyjnych obsługuje SAML 2.0 i WS-Federation, OpenID Połącz również możliwość hello pomocy technicznej dla użytkowników toostart w aplikacji hello, a następnie Pobierz zalogowany za pomocą usługi Azure AD przez automatyczne przekierowanie lub klikając łącze toosign w. Jest to nazywane dostawcy usług-inicjowane logowania jednokrotnego i najbardziej aplikacji federacyjnych w galerii aplikacji hello Azure AD obsługuje to (zobacz dokumentację hello połączone z aplikacji hello Kreatora konfiguracji rejestracji jednokrotnej w portalu zarządzania Azure powitalnych dla szczegółowe informacje).

![][5]

### <a name="direct-sign-on-links-for-federated-password-based-or-existing-apps"></a>Linki bezpośrednie logowania jednokrotnego do aplikacji federacyjnych, opartych na hasłach lub istniejących
Usługi Azure AD obsługuje również pojedynczego logowania jednokrotnego linki bezpośrednie tooindividual aplikacje, które obsługują opartego na hasłach rejestracji jednokrotnej, istniejące rejestracji jednokrotnej i dowolnej formy federacyjnego logowania jednokrotnego.

Te linki mają specjalnie co adresów URL, które wysyłania do użytkownika za pośrednictwem hello Azure AD logowania procesu dla określonej aplikacji bez konieczności użytkownika hello uruchomić je z panelu dostępu hello Azure AD lub usługi Office 365. Te pojedynczy znak na adresy URL można znaleźć w karty Pulpit nawigacyjny hello wszystkie wstępnie zintegrowanych aplikacji w hello sekcji usługi Active Directory hello portalu zarządzania Azure, jak pokazano na poniższym zrzucie ekranu hello.

![][6]

Te linki mogą zostać skopiowane i wklejone żądanych aplikacji toohello wybrane łącze tooprovide logowania. Może to być w wiadomości e-mail lub w żadnych niestandardowych portalu sieci web skonfigurowanego użytkownika dostępu do aplikacji. Oto przykład usługi Azure AD bezpośredniego pojedynczy adres URL logowania dla usługi Twitter:

`https://myapps.microsoft.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Podobne specyficzne dla tooorganization adresy URL hello panel dostępu, można dostosować ten adres URL, dodając co hello active lub zweryfikowanych domen dla katalogu po hello myapps.microsoft.com domeny. Gwarantuje to, że wszelkie znakowanie organizacji jest ładowany natychmiast na stronę logowania w hello bez konieczności tooenter najpierw swój identyfikator użytkownika użytkownika hello:

`https://myapps.microsoft.com/contosobuild.com/signin/Twitter/230848d52c8745d4b05a60d29a40fced`

Uwierzytelniony użytkownik klika w jednej z poniższych linków, specyficzne dla aplikacji, ich najpierw Zobacz ich organizacyjnej strony logowania (przy założeniu, że ich nie jest już zalogowany), a po zalogowaniu są przekierowane tootheir aplikacji bez uprzedniego zatrzymywania na powitania panelu dostępu. Jeśli użytkownik hello brakuje wymagania wstępne, że tooaccess hello aplikacji, takie jak rozszerzenie przeglądarki opartego na hasłach jednokrotnego hello, hello link monitują hello użytkownika tooinstall hello Brak rozszerzenia. adres URL łącza Hello również pozostaje stała, w przypadku zmiany hello pojedynczego logowania jednokrotnego konfiguracji hello aplikacji.

Te linki Użyj hello tego samego mechanizmy kontroli dostępu jako hello dostępu panelu i Office 365, a tylko do tych użytkowników lub grup, którym przypisano toohello aplikacji w portalu zarządzania Azure hello jest w stanie toosuccessfully uwierzytelniania. Jednak każdy użytkownik, który nie ma autoryzacji zobaczą komunikat z informacjami o tym, że nie przyznano dostęp i podano łącza tooload hello dostępu panelu tooview dostępnych aplikacji dla których mają dostęp.

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory](active-directory-saas-tutorial-list.md)
* [Znajdowanie niezatwierdzona aplikacji w chmurze z usługi Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md)
* [Wprowadzenie tooManaging tooApps dostępu](active-directory-managing-access-to-apps.md)
* [Porównanie funkcji zarządzania w usłudze Azure AD tożsamości zewnętrznych](active-directory-b2b-compare-external-identities.md)

<!--Image references-->
[1]: ./media/active-directory-appssoaccess-whatis/onlineappgallery.png
[2]: ./media/active-directory-appssoaccess-whatis/azuremgmtportal.png
[3]: ./media/active-directory-appssoaccess-whatis/accesspanel.png
[4]: ./media/active-directory-appssoaccess-whatis/officeapphub.png
[5]: ./media/active-directory-appssoaccess-whatis/workdaymobile.png
[6]: ./media/active-directory-appssoaccess-whatis/deeplink.png
