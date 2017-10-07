---
title: "Łączenie usługi Active Directory z usługą Azure Active Directory. | Microsoft Docs"
description: "Program Azure AD Connect umożliwia integrowanie katalogów lokalnych z usługą Azure Active Directory. Dzięki temu tooprovide wspólną tożsamością dla usługi Office 365, Azure i aplikacji SaaS zintegrowanych z usługą Azure AD."
keywords: "wprowadzenie tooAzure AD Connect, omówienie usługi Azure AD Connect, co to jest usługa Azure AD Connect, instalacji usługi active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>Integrowanie katalogów lokalnych z usługą Azure Active Directory
Program Azure AD Connect umożliwia integrowanie katalogów lokalnych z usługą Azure Active Directory. Dzięki temu tooprovide wspólną tożsamością dla użytkowników dla usługi Office 365, Azure i aplikacji SaaS zintegrowanych z usługą Azure AD. W tym temacie przedstawiono hello planowania, wdrażania i operacji kroków. Jest kolekcja łącza toohello Tematy pokrewne toothis obszaru.

> [!IMPORTANT]
> [Azure AD Connect jest hello najlepsze sposób tooconnect katalogu lokalnego z usługą Azure AD i Office 365. Jest to doskonały moment tooAzure tooupgrade AD Connect z systemu Windows synchronizacji Azure Active Directory (DirSync) lub Azure AD Sync, jak te narzędzia są teraz przestarzałe i osiągną wsparcie dla 13 kwietnia 2017 r.](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![Co to jest program Azure AD Connect](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>Dlaczego warto korzystać z programu Azure AD Connect
Zintegrowanie katalogów lokalnych z usługą Azure AD zwiększa produktywność użytkowników, zapewniając wspólną tożsamość na potrzeby dostępu do zasobów, zarówno lokalnych, jak i w chmurze. Użytkowników i organizacji można korzystać z następujących hello:

* Użytkownicy mogą korzystać z jednej tożsamości tooaccess lokalnej aplikacji i usług, takich jak Office 365 w chmurze.
* Pojedynczy tooprovide narzędzia obsługi łatwe wdrażanie synchronizacji i logowania.
* Udostępnia najnowsze możliwości powitania dla scenariuszy. Program Azure AD Connect zastępuje starsze wersje narzędzi do integracji tożsamości, takie jak DirSync i Azure AD Sync. Aby uzyskać więcej informacji, zobacz [Porównanie narzędzi do integracji katalogów tożsamości hybrydowej](../active-directory-hybrid-identity-design-considerations-tools-comparison.md).

### <a name="how-azure-ad-connect-works"></a>Jak działa program Azure AD Connect
Azure Active Directory Connect obejmuje trzy główne składniki: hello usługi synchronizacji, opcjonalny składnik usług federacyjnych Active Directory hello i hello składnik monitorowania o nazwie [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md) .

<center>![Stos programu Azure AD Connect](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* Synchronizacja — ten składnik odpowiada za tworzenie użytkowników, grup i innych obiektów. Jest również odpowiedzialny za zapewnienie, że informacje o tożsamości dla lokalnych użytkowników i grup jest zgodne z hello chmury.
* Usług AD FS - federacyjnego jest opcjonalnym składnikiem programu Azure AD Connect i mogą być używane tooconfigure środowisku hybrydowym przy użyciu lokalnej infrastruktury usług AD FS. Może być używany przez organizacje tooaddress złożone wdrożenia, takich jak jednokrotne w domenie, wymuszanie AD zasad logowania, a karta inteligentna lub 3 usługi MFA innych firm.
* Monitorowanie kondycji — program Azure AD Connect Health mógł zapewnia zaawansowane monitorowanie i udostępniać centralnej lokalizacji w hello Azure tooview portalu tego działania. Aby uzyskać więcej informacji, zobacz [Azure Active Directory Connect Health](../connect-health/active-directory-aadconnect-health.md).

## <a name="install-azure-ad-connect"></a>Instalowanie programu Azure AD Connect
Pobieranie hello Azure AD Connect można znaleźć na [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771).

| Rozwiązanie | Scenariusz |
| --- | --- |
| Przed rozpoczęciem — [Sprzęt i wymagania wstępne](active-directory-aadconnect-prerequisites.md) |<li>Kroki toocomplete przed rozpoczęciem tooinstall Azure AD Connect.</li> |
| [Ustawienia ekspresowe](active-directory-aadconnect-get-started-express.md) |<li>Jeśli masz AD z jednym lasem następnie to hello zaleca się toouse opcji.</li> <li>Użytkownika można zalogować się przy użyciu hello same hasła przy użyciu synchronizacji haseł.</li> |
| [Ustawienia dostosowane](active-directory-aadconnect-get-started-custom.md) |<li>Opcja używana, gdy masz większą liczbę lasów. Obsługuje wiele [topologii](active-directory-aadconnect-topologies.md) lokalnych.</li> <li>Możesz dostosować opcje logowania, takie jak usługi federacyjne AD FS lub inny dostawca tożsamości.</li> <li>Możesz dostosować funkcje synchronizacji, na przykład filtrowanie i zapisywanie zwrotne.</li> |
| [Uaktualnianie z narzędzia DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Używane, jeśli masz już działający serwer DirSync.</li> |
| [Uaktualnienie z narzędzia Azure AD Sync lub Azure AD Connect](active-directory-aadconnect-upgrade-previous-version.md) |<li>Istnieje kilka różnych metod do wyboru w zależności od preferencji.</li> |

[Po zakończeniu instalacji](active-directory-aadconnect-whats-next.md) należy sprawdzić jest działa zgodnie z oczekiwaniami i przypisać licencje toohello użytkowników.

### <a name="next-steps-tooinstall-azure-ad-connect"></a>Następne kroki tooInstall Azure AD Connect
|Temat |Link|  
| --- | --- |
|Pobieranie programu Azure AD Connect | [Pobieranie programu Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Instalowanie przy użyciu ustawień ekspresowych | [Ekspresowa instalacja programu Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Instalowanie przy użyciu ustawień dostosowanych | [Niestandardowa instalacja programu Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Uaktualnianie przy użyciu narzędzia DirSync | [Uaktualnianie z narzędzia Azure AD Sync (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Po instalacji | [Zweryfikuj instalację hello i przypisywanie licencji](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>Więcej informacji o instalowaniu programu Azure AD Connect
Należy także tooprepare dla [operacyjne](active-directory-aadconnectsync-operations.md) problemy. Może być toohave serwera gotowości, umożliwiającego łatwe przełączenie przypadku braku [po awarii](active-directory-aadconnectsync-operations.md#disaster-recovery). Jeśli planujesz częste toomake zmiany, należy również zaplanować [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode) serwera.

|Temat |Link|  
| --- | --- |
|Obsługiwane topologie | [Topologie obsługiwane w programie Azure AD Connect](active-directory-aadconnect-topologies.md)|
|Zagadnienia dotyczące projektowania | [Zagadnienia dotyczące projektowania przy korzystaniu z programu Azure AD Connect](active-directory-aadconnect-design-concepts.md)|
|Konta używane do instalacji | [Więcej informacji na temat poświadczeń i uprawnień dla programu Azure AD Connect](./active-directory-aadconnect-accounts-permissions.md)|
|Planowanie operacyjne | [Synchronizacja programu Azure AD Connect: zagadnienia i zadania operacyjne](active-directory-aadconnectsync-operations.md)|
|Opcje logowania użytkowników | [Opcje logowania użytkowników w programie Azure AD Connect](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>Konfigurowanie funkcji synchronizacji
Program Azure AD Connect zawiera szereg funkcji, które są domyślnie włączone lub które można włączyć opcjonalnie. Niektóre funkcje mogą wymagać wykonania dodatkowych czynności konfiguracyjnych w określonych scenariuszach i topologiach.

[Filtrowanie](active-directory-aadconnectsync-configure-filtering.md) jest używany, gdy toolimit obiekty, które są synchronizowane tooAzure AD. Domyślnie synchronizacja obejmuje wszystkich użytkowników, kontakty, grupy i komputery z systemem Windows 10. Możesz zmienić hello filtrowanie na podstawie domen, jednostek organizacyjnych lub atrybutów.

[Synchronizacja haseł](active-directory-aadconnectsync-implement-password-synchronization.md) synchronizuje hello skrótów haseł w usłudze Active Directory tooAzure AD. Witaj przez użytkownika końcowego można użyć hello tego samego hasła lokalnie i w chmurze hello, ale tylko nim zarządzać w jednej lokalizacji. Ponieważ używa lokalnej usługi Active Directory jako urząd hello, można również użyć własnych zasad haseł.

[Zapisywanie zwrotne haseł](../active-directory-passwords-getting-started.md) Zezwalaj toochange Twojego użytkowników i resetowania swoich haseł w chmurze hello i mają sieci lokalnych zasad haseł.

[Zapisywanie zwrotne urządzeń](active-directory-aadconnect-feature-device-writeback.md) umożliwi urządzeń zarejestrowanych w usłudze Azure AD toobe zapisywane tooon lokalnej usłudze Active Directory, dzięki mogą być używane dla dostępu warunkowego.

Witaj [Zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) funkcja jest domyślnie włączona i zabezpiecza katalogu w chmurze przed usunięciem dużej liczby elementów na powitania tym samym czasie. Domyślnie dozwolone jest usunięcie 500 elementów w jednym przebiegu. Możesz zmienić to ustawienie w zależności od wielkości organizacji.

[Automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md) jest domyślnie włączone w przypadku instalacji ustawień ekspresowych i zapewnia programu Azure AD Connect jest zawsze aktywna toodate z hello najnowszej wersji.

### <a name="next-steps-tooconfigure-sync-features"></a>Następny funkcji synchronizacji tooconfigure kroki
|Temat |Link|  
| --- | --- |
|Konfigurowanie filtrowania | [Synchronizacja programu Azure AD Connect: konfigurowanie filtrowania](active-directory-aadconnectsync-configure-filtering.md)|
|Synchronizacja haseł | [Synchronizacja programu Azure AD Connect: wdrażanie synchronizacji haseł](active-directory-aadconnectsync-implement-password-synchronization.md)|
|Zapisywanie zwrotne haseł | [Wprowadzenie do zarządzania hasłami](../active-directory-passwords-getting-started.md)|
|Zapisywanie zwrotne urządzeń | [Włączanie zapisywania zwrotnego urządzeń w programie Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md)|
|Zapobieganie przypadkowemu usuwaniu | [Synchronizacja programu Azure AD Connect: zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|Automatycznie uaktualnianie | [Azure AD Connect: automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>Dostosowywanie synchronizacji w programie Azure AD Connect
Synchronizacja programu Azure AD Connect ma konfigurację domyślną, która jest toowork przeznaczone dla większości klientów i topologii. Zawsze jednak mogą sytuacji, gdy hello domyślnej konfiguracji nie działa i musi zostać dostosowana. Jest obsługiwana toomake zmian zgodnie z opisem w tej sekcji i powiązanych tematach.

Jeśli nie masz doświadczenia z topologią synchronizacji przed mają toostart toounderstand hello podstawy i używanymi pojęciami przedstawionymi w hello hello [zagadnienia techniczne](active-directory-aadconnectsync-technical-concepts.md). Azure AD Connect jest ewolucji hello podstawie narzędzi MIIS2003, ILM2007 i FIM2010. Mimo że niektóre elementy są identyczne, wprowadzono także wiele zmian.

Witaj [domyślnej konfiguracji](active-directory-aadconnectsync-understanding-default-configuration.md) zakłada hello konfiguracji może być więcej niż jednego lasu. W takich topologiach obiekt użytkownika może być reprezentowany jako kontakt w innym lesie. Użytkownik Hello może także mieć połączoną skrzynkę pocztową w innym lesie zasobów. zachowanie Hello hello domyślna konfiguracja jest opisana w [użytkowników i kontaktów](active-directory-aadconnectsync-understanding-users-and-contacts.md).

Witaj model konfiguracji synchronizacji jest nazywany [aprowizacją deklaratywną](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md). Witaj zaawansowane przepływy atrybutów używają [funkcje](active-directory-aadconnectsync-functions-reference.md) tooexpress atrybutu przekształcenia. Można wyświetlić i sprawdzić hello całą konfigurację za pomocą narzędzi dostarczany razem z programem Azure AD Connect. Jeśli potrzebujesz toomake zmian konfiguracji, upewnij się, wykonaj hello [najlepsze rozwiązania](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) więc jest łatwiejsze tooadopt nowych wersji.

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>Następne kroki toocustomize usługi Azure AD Connect synchronizacji
|Temat |Link|  
| --- | --- |
|Wszystkie artykuły dotyczące synchronizacji programu Azure AD Connect | [Synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md)|
|Zagadnienia techniczne | [Synchronizacja programu Azure AD Connect: zagadnienia techniczne](active-directory-aadconnectsync-technical-concepts.md)|
|Opis hello domyślnej konfiguracji | [Synchronizacja programu Azure AD Connect: opis hello domyślnej konfiguracji](active-directory-aadconnectsync-understanding-default-configuration.md)|
|Opis użytkowników i kontaktów | [Synchronizacja programu Azure AD Connect: opis użytkowników i kontaktów](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|Aprowizacja deklaratywna | [Synchronizacja programu Azure AD Connect: wyjaśnienie wyrażeń związanych z aprowizacją deklaratywną](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|Zmienianie konfiguracji domyślnej hello | [Najlepsze rozwiązania dotyczące zmieniania konfiguracji domyślnej hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>Konfigurowanie funkcji federacyjnych
Usługi AD FS może być skonfigurowany toosupport [wielu domen](active-directory-aadconnect-multiple-domains.md). Przykładowo jeśli masz wiele domen najwyższego poziomu należy toouse dla Federacji.

Jeśli serwer usług AD FS nie został skonfigurowany tooautomatically Aktualizuj certyfikaty z usługi Azure AD lub użycie rozwiązania z systemem innym niż usługi AD FS, następnie otrzymasz powiadomienie, gdy masz zbyt[Aktualizuj certyfikaty,](active-directory-aadconnect-o365-certs.md).

### <a name="next-steps-tooconfigure-federation-features"></a>Następny funkcji federacyjnych tooconfigure kroki
|Temat |Link|  
| --- | --- |
|Wszystkie artykuły dotyczące usług AD FS | [Program Azure AD Connect a federacja](active-directory-aadconnectfed-whatis.md)|
|Konfigurowanie usług AD FS z poddomenami | [Obsługa wielu domen do federowania w usłudze Azure AD](active-directory-aadconnect-multiple-domains.md)|
|Zarządzanie farmą usług AD FS | [Dostosowywanie usług AD FS i zarządzanie nimi za pomocą programu Azure AD Connect](active-directory-aadconnect-federation-management.md)|
|Ręczne aktualizowanie certyfikatów federacji | [Odnawianie certyfikatów federacji dla usług Office 365 i Azure AD](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>Więcej informacji i materiały referencyjne
|Temat |Link|  
| --- | --- |
|Historia wersji | [Historia wersji](active-directory-aadconnect-version-history.md)|
|Porównanie narzędzi DirSync, Azure ADSync i Azure AD Connect | [Porównanie narzędzi do integracji katalogów](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Lista zgodności usługi Azure AD z usługami innymi niż AD FS | [Lista zgodności usługi Azure AD z usługami federacyjnymi](active-directory-aadconnect-federation-compatibility.md)|
|Konfigurowanie dostawcy tożsamości SAML 2.0|[Korzystanie z dostawcy tożsamości SAML 2.0 do celów rejestracji jednokrotnej](active-directory-aadconnect-federation-saml-idp.md)|
|Synchronizowane atrybuty | [Synchronizowane atrybuty](active-directory-aadconnectsync-attributes-synchronized.md)|
|Monitorowanie za pomocą narzędzia Azure AD Connect Health | [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md)|
|Często zadawane pytania | [Azure AD Connect — Często zadawane pytania](active-directory-aadconnect-faq.md)|

**Dodatkowe zasoby**

Konferencji Ignite 2015 prezentacji rozszerzania katalogów lokalnych toohello chmury.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

