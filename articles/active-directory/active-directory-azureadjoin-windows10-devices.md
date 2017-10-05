---
title: "W miejscu pracy przy użyciu urządzeń z systemem Windows 10 | Dokumentacja firmy Microsoft"
description: "Zapewnia użytkownikom migawkę możliwości i IT kontrastem różne sposoby urządzenia można zainicjować obsługi administracyjnej i używane w przedsiębiorstwie z systemem Windows 10."
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
ms.openlocfilehash: 451842f764898af65dd7300e8b48442d256cea7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>Przy użyciu urządzeń z systemem Windows 10 w miejscu pracy
Dotyczy: komputerów z systemem Windows 10

Windows 10 udostępnia trzy modele dla organizacji, które umożliwiają użytkownikom uzyskiwanie dostępu do zasobów roboczych w bezpieczny i wygodny sposób.

* **Azure Active Directory Join procesu** (Azure AD Join), dla pracowników, którzy uzyskują dostęp do zasobów, takich jak usługi Office 365 głównie w chmurze. Azure AD Join jest samoobsługi pracy inicjowania obsługi administracyjnej obsługi, który jest nowy w systemie Windows 10.
* **Przyłączanie do domeny**, w przypadku organizacji, które dokonały inwestycji w lokalnej aplikacji i zasobów. Przyłączanie do domeny oferuje lepszą obsługę w systemie Windows 10 w przypadku połączenia z usługą Azure AD.
* **Nowy uproszczone środowisko BYOD**dla użytkowników, którzy mają zostać dodane konto służbowe lub służbowe do systemu Windows i łatwo uzyskiwać dostęp do zasobów na urządzeniach osobistych.

W poniższej tabeli przedstawiono migawki funkcji dla użytkowników i administratorów IT, kontrastem różne sposoby urządzenia można zainicjować obsługi administracyjnej i używane w przedsiębiorstwie z systemem Windows 10:

|  | Przyłączanie do domeny | Azure AD Join | Urządzenie osobiste |
| --- | --- | --- | --- |
| Windows urządzenia logowania dla konta firmowego lub szkolnego. |Tak |Tak |Nie |
| Użytkownik single-sign-on (rejestracji jednokrotnej SSO) do aplikacji usługi Office 365 i Azure AD. Usługa rejestracji Jednokrotnej jest możliwość Zaloguj się tylko raz na dostęp do zasobów organizacji. |Tak |Tak |Tak |
| Użytkownik logowania jednokrotnego do aplikacji Kerberos/NTLM. |Tak |Ograniczone |Tak, za pośrednictwem sieci VPN |
| Silne autoryzacji i wygodne logowanie dla konta służbowego z Microsoft Passport i usługi Windows Hello. |Tak |Tak |Tak |
| Dostęp do przedsiębiorstwa Sklepu Windows przy użyciu konta służbowego, (a nie kontem Microsoft). |Tak |Tak |Tak |
| Zgodne Enterprise roaming ustawień użytkownika między urządzeniami przy użyciu konta służbowego. |Tak |Tak |Tak |
| Możliwość ograniczania dostępu do aplikacji organizacyjnych na urządzeniach, które są zgodne z zasadami organizacji urządzenia. |Tak |Tak |Tak |
| Użytkownik samoobsługi inicjowania obsługi urządzeń dla "pracy z dowolnego miejsca." |Nie |Tak |Tak |
| Zdolność do zarządzania urządzeniami. |Tak, za pomocą zasad grupy/SCCM |Tak |Tak |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>Dołącz urządzeń należących do pracy z usługi Azure AD Join i domeny w systemie Windows 10
Windows 10 udostępnia dwa sposoby urządzenia należące do pracy uzyskać dostęp do zasobów roboczych:

* Azure AD Join
* Przyłączanie do domeny
  
  Jednocześnie może być prawidłowe opcje w zależności od wymagań i potrzeb organizacji. W niektórych przypadkach organizacje mogą korzystać z włączeniem obu metod wdrażania.

## <a name="when-to-use-azure-active-directory-join"></a>Kiedy należy używać usługi Azure Active Directory Join
Azure AD Join jest nowa praca samoobsługi inicjowania obsługi administracyjnej doświadczenie w systemie Windows 10.  Jest on skierowany do pracowników, którzy uzyskują dostęp do zasobów roboczych, takich jak Office 365 głównie w chmurze. To lekkie sposób skonfigurować komputery, tablety i telefony dla przedsiębiorstwa. Urządzenia są zarządzane za pośrednictwem funkcji zarządzania urządzeniami przenośnymi za pomocą formantów spójne na platformach systemu Windows.

**Użyj usługi Azure AD Join dla żadnej z następujących powodów**:

* Chcesz włączyć samoobsługowe inicjowania obsługi urządzeń dla pracowników w podróży.
* Urządzenia przenośne należące do pracy, takich jak tablety i telefony można udostępnić użytkownikom.
* Chcesz zarządzać zbioru użytkowników w usłudze Azure AD, a nie w usłudze Active Directory, takie jak okresach pracownicy, wykonawcy lub studentów.
* Chcesz podać łącząca możliwości do pracowników w biurach oddziałów zdalnego z infrastruktury lokalnej ograniczone.
* Nie masz lokalnej usługi Active Directory.

Niektóre organizacje zastosuje Azure AD Join jako podstawową metodą wdrażania urządzenia należące do pracy, szczególnie jako migracji większości lub wszystkich ich zasobów w chmurze. Hybrydowe organizacji z usługi Active Directory i Azure AD można również wdrożyć jednej metody lub innym w zależności od użytkowników lub działów.

Regionach służbowe i wyższych, na przykład może zarządzać personelu w usłudze Active Directory i studentów w usłudze Azure AD. Niektóre firmy może być zarządzania zdalnego oddziałów lub działów sprzedaży w usłudze Azure AD. Zarówno program Azure AD Join, jak i metody sprzężenia domeny może służyć w obrębie organizacji hybrydowego. Azure AD Join można doskonałe uzupełnienie przyłączenie do domeny do wdrażania urządzeń w środowisku pracy.

**Jeśli jest zwykle dostęp do zasobów firmy za pośrednictwem chmury, organizacja może dodatkowe korzyści obejmują Jeśli**:

* Możesz usunąć zależności na lokalnej infrastruktury tożsamości.
* Model wdrażania urządzeń, można uprościć pobierania od rozwiązań do obsługi obrazów, zezwalając Konfiguracja samoobsługi.
* Zarządzanie urządzeniami przenośnymi umożliwia zarządzanie wszystkimi urządzeniami na różnych platformach.

Aby uzyskać więcej informacji na temat usługi Azure AD Join, zobacz [rozszerzanie funkcji chmury na urządzeniach z systemem Windows 10 za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="when-to-use-domain-join-or-keep-using-it"></a>Kiedy należy używać sprzężenia domeny (lub Zachowaj korzystania z niego)
W ostatnich latach 15 w wielu organizacjach użyto przyłączenie do domeny do łączenia urządzeń w pracy. Umożliwia użytkownikom zalogowanie się na urządzeniach z siecią firmową usługi Active Directory lub konta służbowego. Przyłączanie do domeny umożliwia również IT, aby centralnie i w pełni zarządzać tymi urządzeniami. Organizacje zwykle są oparte na metodach obrazu, aby zainicjować obsługę administracyjną urządzeń i często używają programu System Center Configuration Manager (SCCM) lub zasad grupy (GP) do zarządzania nimi.

**Przedsiębiorstwa należy używać sprzężenia domeny (lub zachować przy jego użyciu) dla dowolnego z następujących powodów**:

* Masz aplikacji Win32 wdrożonych na tych urządzeniach, które używają protokołu NTLM/Kerberos.
* Wymagane jest zasad grupy lub SCCM/DCM do zarządzania urządzeniami.
* Chcesz nadal używać do konfigurowania urządzeń pracowników rozwiązań do obsługi obrazów.

**Przyłączanie do domeny w systemie Windows 10 zapewnia również następujące korzyści podczas połączenia z usługą Azure AD**:

* Silne uwierzytelnianie powiązane z urządzenia i wygodne logowanie dla konta służbowego z Microsoft Passport i usługi Windows Hello.
* Dostęp do przedsiębiorstwa Sklepu Windows dla urządzeń używających pracy lub szkołą kont (nie wymagane konto Microsoft).
* Zgodne Enterprise roaming ustawień użytkownika na urządzeniach korzystających z konta służbowe (nie wymagane konto Microsoft).
* Możliwość ograniczania dostępu do aplikacji organizacyjnych na urządzeniach, które są zgodne z zasadami organizacji urządzenia.

Aby uzyskać więcej informacji na temat usługi Azure AD Join, zobacz [rozszerzanie funkcji chmury na urządzeniach z systemem Windows 10 za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-overview.md).

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>Włącz dołączenie urządzeń osobistych w pracy lub nauki
Na potrzeby obsługi BYOD w przedsiębiorstwie, Windows 10 zapewnia możliwość dodawania konta firmowego lub szkolnego do jego komputera, tabletu lub telefonu. Po użytkownik dodaje konto służbowe, urządzenie jest zarejestrowane w usłudze Azure AD i opcjonalnie zarejestrowane w systemie zarządzania urządzeniami przenośnymi, skonfigurowanego w organizacji. Katalog wyświetli te urządzenia jako "Zarejestrowanej" vs. "Połączone usługi azure AD". Administratorzy IT można stosować różne zasady na podstawie tych informacji, zapewniając jaśniejszy touch na urządzeniach osobistych niż na urządzenia należące do pracy w razie potrzeby.

Użytkownicy mogą dodać konta służbowego do swoich urządzeń osobistych bardzo wygodny sposób. Mogą one to robić przy uzyskiwaniu dostępu do aplikacji pracy po raz pierwszy lub ich można to zrobić ręcznie za pomocą menu Ustawienia. To konto będzie zapewnienia logowania jednokrotnego do zasobów organizacji.

Aby uzyskać więcej informacji na temat usługi Azure AD Join, zobacz [łączenie urządzeń przyłączonych do domeny do usługi Azure AD dla systemu Windows 10 napotyka](active-directory-azureadjoin-devices-group-policy.md).

## <a name="enable-domain-join-or-azure-ad-join"></a>Włącz przyłączenie do domeny lub Azure AD Join
Wszystkie metody opisanych wcześniej (przyłączenie do domeny, Dołącz do programu Azure AD i Dodaj konto służbowe) mają punktów wejścia w środowisko użytkownika systemu Windows 10. Jednak wymaga administratora IT włączyć funkcję w infrastrukturze przed środowisko będzie działać.

## <a name="requirements-for-deploying-azure-ad-join"></a>Wymagania dotyczące wdrażania usługi Azure AD Join
Do wdrożenia usługi Azure AD Join dla każdego zestawu użytkowników są potrzebne następujące elementy:

* Subskrypcja usługi Azure AD.
* Subskrypcja usługi Azure AD Premium, takie jak urządzenie przenośne zarządzania autorejestrowania, jeśli potrzebujesz więcej możliwości.
* Zarządzanie urządzeniami przenośnymi — na przykład subskrypcję Microsoft Intune, zarządzanie urządzeniami przenośnymi dla usługi Office 365 lub dowolnego partnera dostawców zarządzania urządzeniami przenośnymi, które integracji z usługą Azure AD. (Zobacz [sekcji często zadawanych PYTAŃ](#frequently-asked-questions) pod koniec w tym artykule, aby uzyskać więcej informacji).

Jeśli Twoje urządzenia hybrydowych, zaleca się wdrożenie usługi Azure AD Connect, aby rozszerzyć katalog lokalny z usługą Azure AD.

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>Wymagania dotyczące korzystania z usługi Azure AD przy użyciu przyłączania do domeny
Przyłączanie do domeny w dalszym ciągu działać jako zawsze ma. Jednak aby uzyskać korzyści usługi Azure AD są potrzebne następujące:

* Subskrypcja usługi Azure AD.
* Wdrażanie programu Azure AD Connect, aby rozszerzyć katalog lokalny z usługą Azure AD.
* Zasada, która umożliwia urządzeń przyłączonych do domeny dostęp warunkowy do usługi Azure AD.
* Zasada, która umożliwia uzyskanie dostępu do urządzenia "przyłączonych do domeny", jeśli chcesz można było ograniczyć dostęp dla niektórych urządzeń.
* System Center Configuration Manager wersji 1509 Technical Preview, aby włączyć zasady wymagające ze zgodnych urządzeń. (Zobacz dokumentację w witrynie TechNet i wpisie w blogu).

Aby uzyskać więcej informacji dotyczących przyłączania do domeny w systemie Windows 10, zobacz [łączenie urządzeń przyłączonych do domeny do usługi Azure AD dla systemu Windows 10 napotyka](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>Wymagania dotyczące korzystania z modelu BYOD i "Dodaj konto służbowe"
Aby włączyć "Przynieś własne urządzenie" (BYOD) z konta służbowego, należy spełnić następujące warunki:

* Subskrypcja usługi Azure AD.
* Subskrypcja usługi Azure AD Premium, takie jak urządzenie przenośne zarządzania autorejestrowania, jeśli potrzebujesz więcej możliwości.

## <a name="requirements-for-using-microsoft-passport"></a>Wymagania dotyczące usługi Microsoft Passport
Aby włączyć Microsoft Passport, potrzebne następujące elementy:

* Infrastruktury kluczy publicznych (PKI) do obsługi uwierzytelniania opartego na certyfikatach, który używa programu Microsoft Passport.
* Subskrypcję usługi Intune do obsługi uwierzytelniania opartego na certyfikatach, który korzysta z konta służbowego i Microsoft Passport for Azure AD Join.
* System Center Configuration Manager wersji 1509 Technical Preview (zobacz dokumentację w witrynie TechNet i wpisie w blogu) do obsługi uwierzytelniania opartego na certyfikatach, używanego przez Microsoft Passport do przyłączania do domeny.
* Zasady dotyczące włączania Microsoft Passport w organizacji.

Alternatywą wobec przy użyciu infrastruktury kluczy publicznych można włączyć opartego na kluczach Microsoft Passport w następujący sposób:

* Wdrożenie kontrolerów domeny dla systemu Windows Server 2016 "Produkcyjnej wersji zapoznawczej 1" (nie ma potrzeby poziomów funkcjonalności domeny lub lasu; kilka kontrolerów domeny do użycia nadmiarowość, który wystarczy każdej lokacji usługi Active Directory).
* Ustawienie zasad umożliwia Microsoft Passport w organizacji.

Aby uzyskać więcej informacji o Microsoft Passport i usługi Windows Hello w systemie Windows 10 zobacz < link-to-MS-Passport-and-Windows-Hello-document >.

## <a name="frequently-asked-questions"></a>Często zadawane pytania
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>Partner produktów zarządzania urządzeniami przenośnymi można zintegrować z usługą Azure AD?
Następujące produkty dostawcy integracji z usługą Azure AD ujednoliconego rejestracji i dostępu warunkowego w systemie Windows 10:

* AirWatch VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* SOTI lokalnego zarządzania urządzeniami przenośnymi
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Dołącz co o pracy w systemie Windows 10?
Dołącz do miejsca pracy została użyta Windows 8.1 można włączyć model BYOD. W systemie Windows 10 BYOD za pomocą apletu "Dodaj służbowy lub konta służbowego" jest włączona, jak opisano wcześniej w tym dokumencie. Dla organizacji, które nie integracji zarządzania ich urządzeniami przenośnymi z usługą Azure AD, użytkownicy mogą rejestrować urządzenia do zarządzania ręcznie za pośrednictwem **ustawienia** > **kont** > **dostęp z miejsca pracy**.

### <a name="can-users-connect-their-microsoft-account-to-their-domain-account-in-windows-10"></a>Użytkownicy mogą łączyć swoje konta Microsoft swojego konta domeny w systemie Windows 10?
Nie w systemie Windows 10. W Windows 8.1 użytkownicy urządzeń przyłączonych do domeny można "connect" swojego konta Microsoft (na przykład usługi Hotmail, Live, Outlook, Xbox, itp.) do swojego konta domeny, aby umożliwić korzystanie niektóre z takich jak usługa rejestracji Jednokrotnej usługi Live, korzystanie ze Sklepu Windows i przenoszenie ustawień między urządzeniami. W systemie Windows 10 konta Microsoft "Połącz" funkcjonalność została wycofana. Użytkownik może dodać co najmniej jedno konto Microsoft jako dodatkowych kont w celu włączenia funkcji logowania jednokrotnego do klienta usług takich jak Sklep Windows. Jest to wykonywane w **ustawienia** > **kont** > **konta**.

Użytkownicy uaktualniających oprogramowanie z urządzeń, Windows 8.1 przyłączonych do domeny, i która została swojego konta Microsoft połączone, automatycznie otrzymują połączonych dodany do listy dodatkowych kont, których używają konta Microsoft.

## <a name="additional-information"></a>Dodatkowe informacje
* [System Windows 10 dla przedsiębiorstw: sposoby używania urządzenia do pracy](active-directory-azureadjoin-windows10-devices-overview.md)
* [Rozszerzanie możliwości chmury dla urządzeń z systemem Windows 10 za pomocą usługi Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md)
* [Dowiedz się więcej na temat scenariuszy użycia funkcji Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Łączenie urządzeń przyłączonych do domeny z usługą Azure AD w celu korzystania z możliwości systemu Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Konfigurowanie funkcji Azure AD Join](active-directory-azureadjoin-setup.md)

