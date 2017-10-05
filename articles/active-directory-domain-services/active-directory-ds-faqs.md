---
title: "Często zadawane pytania — Azure Active Directory Domain Services | Dokumentacja firmy Microsoft"
description: "Często zadawane pytania dotyczące usług domenowych Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 48731820-9e8c-4ec2-95e8-83dba1e58775
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: maheshu
ms.openlocfilehash: 7f3212350b1158cd51a34ee1b20a456a73d41672
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services: Często zadawane pytania (FAQ)
Ta strona zawiera odpowiedzi na często zadawane pytania dotyczące usługi Azure Active Directory Domain Services. Sprawdzanie wstecz do aktualizacji.

### <a name="troubleshooting-guide"></a>Przewodnik rozwiązywania problemów
Zobacz nasze [przewodnik rozwiązywania problemów](active-directory-ds-troubleshooting.md) rozwiązania typowych problemów napotykanych podczas konfigurowania lub administrowania usługami domenowymi Azure AD.

### <a name="configuration"></a>Konfiguracja
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Można utworzyć wiele domen z jednym katalogu usługi Azure AD?
Nie. Można utworzyć tylko jedną domeną obsługiwanych przez usługi domenowe Azure AD z jednym katalogu usługi Azure AD.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Można włączyć usługi domenowe Azure AD w sieci wirtualnej platformy Azure Resource Manager?
Nie. Usługi domenowe Azure AD można włączyć tylko w klasycznej sieci wirtualnej platformy Azure. Klasyczne sieci wirtualnej może nawiązać Menedżera zasobów sieci wirtualnej przy użyciu sieci wirtualnej komunikacji równorzędnej do korzystania z domeny zarządzanej w sieci wirtualnej Menedżera zasobów.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-to-authenticate-users-for-access-to-office-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>Można włączyć usługi domenowe Azure AD w federacyjnych Azure AD directory? Używać usług AD FS do uwierzytelniania użytkowników w celu uzyskania dostępu do usługi Office 365. Można włączyć usługi domenowe Azure AD dla katalogu?
Nie. Usługi domenowe Azure AD musi mieć dostęp do wartości skrótów haseł kont użytkowników, do uwierzytelniania użytkowników za pomocą protokołu NTLM lub Kerberos. W katalogu federacyjnych skrótów haseł nie są przechowywane w katalogu usługi Azure AD. W związku z tym usługi domenowe Azure AD nie działa z tych katalogów usługi Azure AD.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Czy można utworzyć usługi domenowe Azure AD dostępne w wielu sieci wirtualnych w mojej subskrypcji?
Sama usługa nie obsługuje bezpośrednio w tym scenariuszu. Usługi domenowe Azure AD jest dostępna w tylko jedną sieć wirtualną w czasie. Jednak należy skonfigurować połączenie między wieloma sieciami wirtualnymi do udostępnienia usług domenowych Azure AD do innych sieci wirtualnych. W tym artykule opisano sposób [połączyć sieci wirtualnych na platformie Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>Można włączyć usługi domenowe Azure AD przy użyciu programu PowerShell?
PowerShell/automatycznego wdrażania usług domenowych Azure AD nie jest obecnie dostępna.

#### <a name="is-azure-ad-domain-services-available-in-the-new-azure-portal"></a>Usługi domenowe Azure AD jest dostępne w portalu Azure?
Nie. Usługi domenowe Azure AD można skonfigurować tylko w [klasycznego portalu Azure](https://manage.windowsazure.com). Oczekuje się rozszerzyć obsługę [portalu Azure](https://portal.azure.com) w przyszłości.

#### <a name="can-i-add-domain-controllers-to-an-azure-ad-domain-services-managed-domain"></a>Kontrolery domeny można dodać do domeny zarządzanej usług domenowych Azure AD?
Nie. Domena udostępniane przez usługi domenowe Azure AD jest domeną zarządzaną. Nie trzeba było możliwe, konfigurowania i inaczej Zarządzanie kontrolerami domeny dla tej domeny — te działania zarządzania są obsługiwane jako usługa przez firmę Microsoft. W związku z tym nie można dodać dodatkowe kontrolery domeny (odczytu i zapisu lub tylko do odczytu) dla domeny zarządzanej.

### <a name="administration-and-operations"></a>Administracja i operacje
#### <a name="can-i-connect-to-the-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Można podłączyć do kontrolera domeny dla mojej domeny zarządzanej przy użyciu pulpitu zdalnego?
Nie. Nie masz uprawnień do łączenia się z kontrolerami domeny dla domeny zarządzanej za pośrednictwem pulpitu zdalnego. Członkowie grupy "Administratorzy kontrolera domeny usługi AAD" mogą administrować domeny zarządzanej przy użyciu narzędzi administracyjnych AD, takie jak Centrum administracji usługi Active Directory (ADAC) lub AD PowerShell. Te narzędzia są zainstalowane na serwerze systemu Windows przyłączone do domeny zarządzanej przy użyciu funkcji "Narzędzia administracji zdalnej serwera".

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-to-domain-join-machines-to-this-domain"></a>Czy włączono usługi domenowe Azure AD. Które konto użytkownika należy używać do domeny sprzężenia maszyn do tej domeny?
Elementy członkowskie grupy administracyjnej "Administratorzy kontrolera domeny usługi AAD" można maszyny przyłączania do domeny. Ponadto Członkowie tej grupy są przyznawane pulpitu dostęp zdalny do komputerów, na których został przyłączony do domeny.

#### <a name="do-i-have-domain-administrator-privileges-for-the-managed-domain-provided-by-azure-ad-domain-services"></a>Czy mają uprawnienia administratora domeny dla domeny zarządzanej udostępniane przez usługi domenowe Azure AD?
Nie. Nie udzielono uprawnienia administracyjne do domeny zarządzanej. Zarówno domeny administratora, jak i administratora przedsiębiorstwa uprawnienia nie są dostępne do użycia w ramach domeny. Istniejącego administratora domeny lub grupy administratora przedsiębiorstwa w katalogu usługi Azure AD również nie są przyznawane uprawnienia administratora domeny/przedsiębiorstwa w domenie.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Można zmodyfikować członkostwa grupy przy użyciu protokołu LDAP lub innych narzędzi administracyjnych AD w domenach zarządzanych?
Nie. Nie można zmodyfikować członkostwa w grupach w domenach obsługiwanych przez usługi domenowe Azure AD. To samo dotyczy atrybuty użytkownika. Można jednak zmienić atrybuty użytkownika lub członkostwa w grupach w usłudze Azure AD lub w domenie lokalnej. Takie zmiany są synchronizowane automatycznie w usługach domenowych Azure AD.

#### <a name="how-long-does-it-take-for-changes-i-make-to-my-azure-ad-directory-to-be-visible-in-my-managed-domain"></a>Jak długo trwa zmiany można wprowadzić w katalogu Moje usługi Azure AD mają być wyświetlane w mojej domeny zarządzanej?
Zmiany wprowadzone w katalogu usługi Azure AD przy użyciu interfejsu użytkownika programu Azure AD lub programu PowerShell są synchronizowane z domeny zarządzanej. Ten proces synchronizacji działa w tle. Po zakończeniu jednorazowe wstępna synchronizacja katalogu zwykle trwa około 20 minut, aby zmiany wprowadzone w usłudze Azure AD zostaną odzwierciedlone w domeny zarządzanej.

#### <a name="can-i-extend-the-schema-of-the-managed-domain-provided-by-azure-ad-domain-services"></a>Czy można rozszerzyć schemat domeny zarządzanej udostępniane przez usługi domenowe Azure AD?
Nie. Schemat jest zarządzany przez firmę Microsoft do domeny zarządzanej. Rozszerzenia schematu nie są obsługiwane przez usługi domenowe Azure AD.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>Można zmodyfikować lub dodać rekordy DNS w mojej domeny zarządzanej?
Tak. Członków grupy "Administratorzy kontrolera domeny usługi AAD" są przyznawane uprawnienia administratora DNS, do modyfikowania rekordów DNS w domenie zarządzanej. Do zarządzania DNS użyciem konsoli Menedżera DNS na komputerze z systemem Windows Server przyłączony do domeny zarządzanej. Przy użyciu konsoli Menedżera DNS, należy zainstalować "Narzędzia serwera DNS", który jest częścią funkcji opcjonalnych "Narzędzia administracji zdalnej serwera" na serwerze. Więcej informacji na temat [narzędzia do zarządzania, monitorowania i rozwiązywania problemów DNS](https://technet.microsoft.com/library/cc753579.aspx) jest dostępna w witrynie TechNet.

### <a name="billing-and-availability"></a>Rozliczeń i dostępności
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Jest usługą płatną usług domenowych Azure AD?
Tak. Aby uzyskać więcej informacji, odwiedź [stronę cennika](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-the-service"></a>Czy istnieje bezpłatna wersja próbna usługi?
Ta usługa znajduje się w bezpłatnej wersji próbnej platformy Azure. Możesz zarejestrować się w celu [w warstwie bezpłatna miesięczna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-to-use-azure-ad-domain-services"></a>W ramach Enterprise Mobility Suite (EMS) można uzyskać usług domenowych Azure AD? Należy Azure AD Premium do użycia usług domenowych Azure AD?
Nie. Usługi domenowe Azure AD jest płatność za rzeczywiste użycie usługi Azure i nie jest częścią pakietu EMS. Usługi domenowe Azure AD może być używany z wszystkie wersje usługi Azure AD (bezpłatne, podstawowe i, Premium). Opłaty są naliczane co godzinę, w zależności od użycia.

#### <a name="what-azure-regions-is-the-service-available-in"></a>Jakie regiony platformy Azure jest dostępna w usłudze?
Zapoznaj się [regionów platformy Azure](https://azure.microsoft.com/regions/#services/) stronę, aby wyświetlić listę regionów platformy Azure, gdy są dostępne usługi domenowe Azure AD.
