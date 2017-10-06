---
title: "urządzenia aaaUsing systemu Windows 10 w miejscu pracy | Dokumentacja firmy Microsoft"
description: "Zapewnia użytkownikom migawkę możliwości i IT kontrastem hello różne sposoby urządzenia można zainicjować obsługi administracyjnej i używane w przedsiębiorstwie z systemem Windows 10."
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: 94ccc8fd-b17b-4fda-8d56-9d87aa37a9f9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 8767e1649ced8737d20875f425c24198dcaa7f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Przy użyciu urządzeń z systemem Windows 10 w miejscu pracy
Dotyczy: komputerów z systemem Windows 10

Windows 10 udostępnia trzy modele dla organizacji, które umożliwiają użytkownikom tooaccess pracy zasobów w sposób bezpieczny i wygodny.

* **Azure Active Directory Join procesu** (Azure AD Join), dla pracowników, którzy uzyskują dostęp do zasobów, takich jak usługi Office 365 głównie w chmurze hello. Azure AD Join jest samoobsługi pracy inicjowania obsługi administracyjnej obsługi, który jest nowy w systemie Windows 10.
* **Przyłączanie do domeny**, w przypadku organizacji, które dokonały inwestycji w lokalnej aplikacji i zasobów. Przyłączanie do domeny oferuje lepszą obsługę w systemie Windows 10 w przypadku połączenia tooAzure AD.
* **Nowy uproszczone środowisko BYOD**, konta użytkowników, którzy chcą tooadd pracy lub szkołą tooWindows i łatwo uzyskiwać dostęp do zasobów na urządzeniach osobistych.

Witaj poniższej tabeli przedstawiono migawki funkcji dla użytkowników i administratorów IT, kontrastem hello różne sposoby urządzenia można zainicjować obsługi administracyjnej i używane w przedsiębiorstwie z systemem Windows 10:

|  | Przyłączanie do domeny | Azure AD Join | Urządzenie osobiste |
| --- | --- | --- | --- |
| Windows urządzenia logowania dla konta firmowego lub szkolnego. |Tak |Tak |Nie |
| Użytkownik-jednokrotnej (SSO) tooOffice 365 i aplikacji usługi Azure AD. Usługa rejestracji Jednokrotnej jest toosign możliwości hello w tylko raz tooaccess zasobów organizacji. |Tak |Tak |Tak |
| Aplikacje tooKerberos/NTLM logowania jednokrotnego użytkowników. |Tak |Ograniczone |Tak, za pośrednictwem sieci VPN |
| Silne autoryzacji i wygodne logowanie dla konta służbowego z Microsoft Passport i usługi Windows Hello. |Tak |Tak |Tak |
| Dostęp do Sklepu Windows tooenterprise przy użyciu konta służbowego, (a nie kontem Microsoft). |Tak |Tak |Tak |
| Zgodne Enterprise roaming ustawień użytkownika między urządzeniami przy użyciu konta służbowego. |Tak |Tak |Tak |
| Witaj możliwości toorestrict dostępu tooorganizational aplikacji toodevices, które są zgodne z zasadami organizacji urządzenia. |Tak |Tak |Tak |
| Użytkownik samoobsługi inicjowania obsługi urządzeń dla "pracy z dowolnego miejsca." |Nie |Tak |Tak |
| Możliwość toomanage urządzenia. |Tak, za pomocą zasad grupy/SCCM |Tak |Tak |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Dołącz urządzeń należących do pracy z usługi Azure AD Join i domeny w systemie Windows 10
Windows 10 udostępnia dwa sposoby zasobów roboczych tooaccess urządzenia należące do pracy:

* Azure AD Join
* Przyłączanie do domeny
  
  Jednocześnie może być prawidłowe opcje w zależności od wymagań i potrzeb organizacji. W niektórych przypadkach organizacje mogą korzystać z włączeniem obu metod wdrażania.

## <a name="when-toouse-azure-active-directory-join"></a>Gdy toouse usługi Azure Active Directory Join
Azure AD Join jest nowa praca samoobsługi inicjowania obsługi administracyjnej doświadczenie w systemie Windows 10.  Jest on skierowany do pracowników, którzy uzyskują dostęp do zasobów roboczych, takich jak Office 365 głównie w chmurze hello. Jest tooconfigure sposób lekkie komputery, tablety i telefony hello przedsiębiorstwa. Urządzenia są zarządzane za pośrednictwem funkcji zarządzania urządzeniami przenośnymi za pomocą formantów spójne na platformach systemu Windows.

**Użyj usługi Azure AD Join dla żadnej z następujących powodów**:

* Ma tooenable hello samoobsługi inicjowania obsługi urządzeń dla pracowników na powitania go.
* Urządzenia przenośne należące do pracy, takich jak tablety i telefony można udostępnić użytkownikom.
* Ma toomanage zbioru użytkowników w usłudze Azure AD, a nie w usłudze Active Directory, takie jak okresach pracownicy, wykonawcy lub studentów.
* Ma tooprovide łącząca tooworkers możliwości w biurach oddziałów zdalnego z infrastruktury lokalnej ograniczone.
* Nie masz lokalnej usługi Active Directory.

Niektóre organizacje zastosuje Azure AD Join jako hello podstawowy sposób toodeploy pracy urządzeń należących do firmy, szczególnie jako migrowania większości lub wszystkich ich zasobów toohello chmury. Hybrydowe organizacji z usługi Active Directory i Azure AD można również wybrać jedną metodę toodeploy lub innej w zależności od użytkowników hello lub działów.

Regionach służbowe i wyższych, na przykład może zarządzać personelu w usłudze Active Directory i studentów w usłudze Azure AD. Niektóre firmy może być toomanage zdalnego oddziałów lub działów sprzedaży w usłudze Azure AD. Zarówno program Azure AD Join, jak i metody sprzężenia domeny może służyć w obrębie organizacji hybrydowego. Azure AD Join można sprzężenia toodomain dużą dopełnienia dotyczące wdrażania urządzeń w środowisku pracy.

**W przypadku hello zwykle uzyskują dostęp do zasobów tooenterprise za pośrednictwem chmury hello, organizacja może dodatkowe korzyści obejmują Jeśli**:

* Możesz usunąć zależności na lokalnej infrastruktury tożsamości.
* Model wdrażania urządzeń, można uprościć pobierania od rozwiązań do obsługi obrazów, zezwalając Konfiguracja samoobsługi.
* Toomanage zarządzania urządzeniami przenośnymi można użyć wszystkich urządzeń na różnych platformach.

Aby uzyskać więcej informacji na temat usługi Azure AD Join, zobacz [rozszerzanie możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join chmury](active-directory-azureadjoin-overview.md).

## <a name="when-toouse-domain-join-or-keep-using-it"></a>Gdy przyłączanie do domeny toouse (lub jej korzystać)
Dla hello ostatnich 15 lat, w wielu organizacjach użyto domeny sprzężenia tooconnect pracy urządzenia. Umożliwia ona użytkownikom toosign tootheir urządzenia z usługą Active Directory ich pracy lub szkołą kont. Przyłączanie do domeny umożliwia również IT toocentrally i pełni zarządzać tymi urządzeniami. Organizacje są zwykle oparte na imaging metody tooprovision urządzeń i często używają toomanage System Center Configuration Manager (SCCM) lub zasad grupy (GP) je.

**Przedsiębiorstwa należy używać sprzężenia domeny (lub zachować przy jego użyciu) dla dowolnego z następujących powodów**:

* Masz urządzeń toothese wdrożonej aplikacji Win32, korzystających z protokołu NTLM/Kerberos.
* Wymagane jest urządzeń toomanage zasad grupy lub SCCM/DCM.
* Chcesz toocontinue toouse obrazowania rozwiązań tooconfigure urządzenia dla pracowników.

**Przyłączanie do domeny w systemie Windows 10 zapewnia również hello następujące korzyści podczas połączenia tooAzure AD**:

* Silne uwierzytelnianie powiązane z urządzenia i wygodne logowanie dla konta służbowego z Microsoft Passport i usługi Windows Hello.
* Dostęp do przedsiębiorstwa toohello Sklepu Windows dla urządzeń używających pracy lub szkołą kont (nie wymagane konto Microsoft).
* Zgodne Enterprise roaming ustawień użytkownika na urządzeniach korzystających z konta służbowe (nie wymagane konto Microsoft).
* Witaj możliwości toorestrict dostępu tooorganizational aplikacji toodevices, które są zgodne z zasadami organizacji urządzenia.

Aby uzyskać więcej informacji na temat usługi Azure AD Join, zobacz [rozszerzanie możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join chmury](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>Włącz dołączenie urządzeń osobistych w pracy lub nauki
toosupport BYOD w hello enterprise, Windows 10 zapewnia hello użytkownika hello możliwości tooadd pracy lub komputerze tootheir konto służbowe, tabletu lub telefonu. Po hello użytkownik dodaje służbowy lub konto służbowe, hello urządzenie jest zarejestrowane w usłudze Azure AD i opcjonalnie zarejestrowane w systemie zarządzania urządzeniami przenośnymi hello skonfigurowanego hello organizacji. katalog Hello wyświetli te urządzenia jako "Zarejestrowanej" vs. "Połączone usługi azure AD". Administratorzy IT można stosować różne zasady na podstawie tych informacji, zapewniając jaśniejszy touch na urządzeniach osobistych niż na urządzenia należące do pracy w razie potrzeby.

Użytkownicy można dodać służbowego lub szkolnego konta tootheir osobiste urządzenie bardzo wygodny sposób. Mogą one to robić przy uzyskiwaniu dostępu do aplikacji pracy dla powitania po raz pierwszy lub ich można to zrobić ręcznie za pomocą menu Ustawienia hello. To konto będzie dostarczała zasoby tooorganizational logowania jednokrotnego.

Aby uzyskać więcej informacji na temat usługi Azure AD Join, zobacz [połączyć tooAzure urządzeń przyłączonych do domeny AD dla systemu Windows 10 napotyka](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Włącz przyłączenie do domeny lub Azure AD Join
Wszystkie metody opisanych wcześniej (przyłączenie do domeny, Dołącz do programu Azure AD i Dodaj konto służbowe) mają punktów wejścia w środowisku użytkownika hello systemu Windows 10. Jednak wymaga funkcji hello IT administrator tooenable w infrastrukturze hello przed hello środowisko będzie działać.

## <a name="requirements-for-deploying-azure-ad-join"></a>Wymagania dotyczące wdrażania usługi Azure AD Join
toodeploy Azure AD Join dla każdego zestawu użytkowników należy hello następujące:

* Subskrypcja usługi Azure AD.
* Subskrypcja usługi Azure AD Premium, takie jak urządzenie przenośne zarządzania autorejestrowania, jeśli potrzebujesz więcej możliwości.
* Zarządzanie urządzeniami przenośnymi — na przykład subskrypcję Microsoft Intune, zarządzanie urządzeniami przenośnymi dla usługi Office 365 lub dowolnego dostawców zarządzania urządzeniami przenośnymi partnera hello, które integrują się z usługą Azure AD. (Zobacz hello [sekcji często zadawanych PYTAŃ](#frequently-asked-questions) zbliża się koniec hello w tym artykule, aby uzyskać więcej informacji).

Jeśli Twoje urządzenia hybrydowych, zaleca się wdrożenie usługi Azure AD Connect tooextend hello lokalnego katalogu tooAzure AD.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Wymagania dotyczące korzystania z usługi Azure AD przy użyciu przyłączania do domeny
Przyłączanie do domeny nadal toowork jako zawsze ma. Jednak tooget korzyści hello Azure AD będą potrzebne hello następujące:

* Subskrypcja usługi Azure AD.
* Wdrażanie usługi Azure AD Connect tooextend hello lokalnego katalogu tooAzure AD.
* Zasada, która umożliwia tooAzure dostępu warunkowego toohave urządzeń przyłączonych do domeny AD.
* Zasada, która zezwala na dostęp urządzeń zbyt "przyłączonych do domeny" Jeśli chcesz toobe toorestrict stanie dostępu dla niektórych urządzeń.
* System Center Configuration Manager wersji 1509 Technical Preview, tooenable zasady wymagające ze zgodnych urządzeń. (Zobacz hello dokumentację w witrynie TechNet i wpis w blogu).

Aby uzyskać więcej informacji dotyczących przyłączania do domeny w systemie Windows 10, zobacz [połączyć tooAzure urządzeń przyłączonych do domeny AD dla napotyka systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>Wymagania dotyczące korzystania z modelu BYOD i "Dodaj konto służbowe"
tooenable "Przynieś własne urządzenie" (BYOD) z konta służbowego, potrzebujesz następujących hello:

* Subskrypcja usługi Azure AD.
* Subskrypcja usługi Azure AD Premium, takie jak urządzenie przenośne zarządzania autorejestrowania, jeśli potrzebujesz więcej możliwości.

## <a name="requirements-for-using-microsoft-passport"></a>Wymagania dotyczące usługi Microsoft Passport
tooenable Microsoft Passport, potrzebne są następujące hello:

* Infrastruktury kluczy publicznych (PKI) do obsługi uwierzytelniania opartego na certyfikatach, który używa programu Microsoft Passport.
* Subskrypcję usługi Intune do obsługi uwierzytelniania opartego na certyfikatach, który korzysta z konta służbowego i Microsoft Passport for Azure AD Join.
* System Center Configuration Manager wersji 1509 Technical Preview (zobacz hello dokumentację w witrynie TechNet i wpis w blogu) do obsługi uwierzytelniania opartego na certyfikatach, używanego przez Microsoft Passport do przyłączania do domeny.
* Zasady dotyczące włączania Microsoft Passport w organizacji hello.

Jako alternatywne toousing infrastruktury kluczy publicznych można włączyć opartego na kluczach Microsoft Passport, wykonując następujące hello:

* Wdrożenie kontrolerów domeny dla systemu Windows Server 2016 "Produkcyjnej wersji zapoznawczej 1" (nie ma potrzeby poziomów funkcjonalności domeny lub lasu; kilka kontrolerów domeny do użycia nadmiarowość, który wystarczy każdej lokacji usługi Active Directory).
* Ustaw zasady tooenable Microsoft Passport w organizacji hello.

Aby uzyskać więcej informacji o Microsoft Passport i usługi Windows Hello w systemie Windows 10 zobacz < link-to-MS-Passport-and-Windows-Hello-document >.

## <a name="frequently-asked-questions"></a>Często zadawane pytania
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Partner produktów zarządzania urządzeniami przenośnymi można zintegrować z usługą Azure AD?
Witaj następujące produkty dostawcy integracji z usługą Azure AD ujednoliconego rejestracji i dostępu warunkowego w systemie Windows 10:

* AirWatch VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* SOTI lokalnego zarządzania urządzeniami przenośnymi
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Dołącz co o pracy w systemie Windows 10?
Dołącz do miejsca pracy została użyta tooenable Windows 8.1 BYOD. W systemie Windows 10 BYOD za pomocą apletu "Dodaj służbowy lub konta służbowego" jest włączona, jak opisano wcześniej w tym dokumencie. Dla organizacji, które nie integracji zarządzania ich urządzeniami przenośnymi z usługą Azure AD, użytkownicy mogą rejestrować urządzenia hello do zarządzania ręcznie za pośrednictwem **ustawienia** > **kont**  >  **Dostęp z miejsca pracy**.

### <a name="can-users-connect-their-microsoft-account-tootheir-domain-account-in-windows-10"></a>Można to robić konta domeny tootheir konta Microsoft w systemie Windows 10?
Nie w systemie Windows 10. W Windows 8.1 użytkownicy urządzeń przyłączonych do domeny można "connect" ich tooenable konta domeny tootheir Microsoft konta (na przykład usługi Hotmail, Live, Outlook, Xbox, itp.) niektóre funkcje takie jak logowania jednokrotnego tooLive usługi, użyj hello Sklepu Windows i przenoszenie Ustawienia użytkownika między urządzeniami. W systemie Windows 10 hello konta Microsoft "Połącz" funkcjonalność została wycofana. Witaj użytkownik może dodać co najmniej jedno konto Microsoft jako dodatkowych kont tooenable logowania jednokrotnego tooconsumer usług, takich jak hello Sklepu Windows. Jest to wykonywane w **ustawienia** > **kont** > **konta**.

Użytkownicy uaktualniających oprogramowanie z urządzeń, Windows 8.1 przyłączonych do domeny, a który miał swojego konta Microsoft połączone, zostanie automatycznie połączone konta Microsoft dodano toohello listę dodatkowych kont, których używają.

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw hello: sposoby toouse urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie chmury możliwości tooWindows 10 urządzeniami za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny tooAzure AD dla systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

