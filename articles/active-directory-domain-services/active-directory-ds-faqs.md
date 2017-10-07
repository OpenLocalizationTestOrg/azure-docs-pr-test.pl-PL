---
title: "aaaFAQs — Azure Active Directory Domain Services | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 42a6d659f6408bf694cb2aa6ec24bff7a76b0565
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-domain-services-frequently-asked-questions-faqs"></a>Azure Active Directory Domain Services: Często zadawane pytania (FAQ)
Ta strona zawiera odpowiedzi na często zadawane pytania dotyczące hello Azure Active Directory Domain Services. Sprawdzanie wstecz do aktualizacji.

### <a name="troubleshooting-guide"></a>Przewodnik rozwiązywania problemów
Zobacz tooour [przewodnik rozwiązywania problemów](active-directory-ds-troubleshooting.md) rozwiązań problemów toocommon wystąpił podczas konfigurowania lub administrowania usługami domenowymi Azure AD.

### <a name="configuration"></a>Konfiguracja
#### <a name="can-i-create-multiple-domains-for-a-single-azure-ad-directory"></a>Można utworzyć wiele domen z jednym katalogu usługi Azure AD?
Nie. Można utworzyć tylko jedną domeną obsługiwanych przez usługi domenowe Azure AD z jednym katalogu usługi Azure AD.  

#### <a name="can-i-enable-azure-ad-domain-services-in-an-azure-resource-manager-virtual-network"></a>Można włączyć usługi domenowe Azure AD w sieci wirtualnej platformy Azure Resource Manager?
Nie. Usługi domenowe Azure AD można włączyć tylko w klasycznej sieci wirtualnej platformy Azure. Możesz połączyć hello klasycznej sieci wirtualnej tooa Menedżera zasobów sieci wirtualnej przy użyciu sieci wirtualnej komunikacji równorzędnej toouse domeny zarządzanej w sieci wirtualnej Menedżera zasobów.

#### <a name="can-i-enable-azure-ad-domain-services-in-a-federated-azure-ad-directory-i-use-adfs-tooauthenticate-users-for-access-toooffice-365-can-i-enable-azure-ad-domain-services-for-this-directory"></a>Można włączyć usługi domenowe Azure AD w federacyjnych Azure AD directory? Użytkownicy tooauthenticate usług AD FS za pomocą uzyskać dostęp tooOffice 365. Można włączyć usługi domenowe Azure AD dla katalogu?
Nie. Usługi domenowe Azure AD musi uzyskiwać dostęp do toohello skrótów haseł kont użytkowników, użytkownicy tooauthenticate za pomocą protokołu NTLM lub Kerberos. W katalogu federacyjnych skrótów haseł nie są przechowywane w katalogu usługi Azure AD hello. W związku z tym usługi domenowe Azure AD nie działa z tych katalogów usługi Azure AD.

#### <a name="can-i-make-azure-ad-domain-services-available-in-multiple-virtual-networks-within-my-subscription"></a>Czy można utworzyć usługi domenowe Azure AD dostępne w wielu sieci wirtualnych w mojej subskrypcji?
sama usługa Hello nie obsługuje bezpośrednio w tym scenariuszu. Usługi domenowe Azure AD jest dostępna w tylko jedną sieć wirtualną w czasie. Jednak należy skonfigurować połączenie między wieloma sieciami wirtualnymi tooexpose usług domenowych Azure AD tooother sieciami wirtualnymi. W tym artykule opisano sposób [połączyć sieci wirtualnych na platformie Azure](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).

#### <a name="can-i-enable-azure-ad-domain-services-using-powershell"></a>Można włączyć usługi domenowe Azure AD przy użyciu programu PowerShell?
PowerShell/automatycznego wdrażania usług domenowych Azure AD nie jest obecnie dostępna.

#### <a name="is-azure-ad-domain-services-available-in-hello-new-azure-portal"></a>Usługi domenowe Azure AD jest dostępna w hello nowego portalu Azure?
Nie. Usługi domenowe Azure AD można skonfigurować tylko w hello [klasycznego portalu Azure](https://manage.windowsazure.com). Oczekujemy tooextend obsługę hello [portalu Azure](https://portal.azure.com) w przyszłości hello.

#### <a name="can-i-add-domain-controllers-tooan-azure-ad-domain-services-managed-domain"></a>Można dodać domeny zarządzanej usług domenowych Azure AD tooan kontrolery domeny?
Nie. Domena Hello udostępniane przez usługi domenowe Azure AD jest domeną zarządzaną. Nie trzeba tooprovision, skonfiguruj lub w przeciwnym razie Zarządzanie kontrolerami domeny dla tej domeny - management, te działania są dostępne jako usługa przez firmę Microsoft. W związku z tym nie można dodać dodatkowe kontrolery domeny (odczytu i zapisu lub tylko do odczytu) dla domeny zarządzanej hello.

### <a name="administration-and-operations"></a>Administracja i operacje
#### <a name="can-i-connect-toohello-domain-controller-for-my-managed-domain-using-remote-desktop"></a>Dla mojej domeny zarządzanej przy użyciu pulpitu zdalnego można łączyć toohello kontrolera domeny?
Nie. Nie masz uprawnień tooconnect toodomain kontrolery hello zarządzane za pośrednictwem pulpitu zdalnego. Członkowie grupy "Administratorzy kontrolera domeny usługi AAD" hello mogą administrować hello domeny zarządzanej przy użyciu narzędzi administracyjnych AD, takie jak hello Centrum administracji usługi Active Directory (ADAC) lub AD PowerShell. Te narzędzia są zainstalowane przy użyciu hello "Narzędzia administracji zdalnej serwera" funkcji na serwerze z systemem Windows przyłączonych do domeny zarządzanej toohello.

#### <a name="ive-enabled-azure-ad-domain-services-what-user-account-do-i-use-toodomain-join-machines-toothis-domain"></a>Czy włączono usługi domenowe Azure AD. Jakiego konta użytkownika domeny toothis maszyny sprzężenia toodomain należy używać?
Członkowie grupy administracyjne hello "Administratorzy kontrolera domeny usługi AAD" mogą maszyny przyłączania do domeny. Ponadto Członkowie tej grupy są przyznawane toomachines dostępu do pulpitu zdalnego, które zostały toohello przyłączone do domeny.

#### <a name="do-i-have-domain-administrator-privileges-for-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Czy mają uprawnienia administratora domeny dla domeny zarządzanej hello udostępniane przez usługi domenowe Azure AD?
Nie. Nie udzielono uprawnienia administracyjne na powitania domeny zarządzanej. Zarówno domeny administratora, jak i administratora przedsiębiorstwa uprawnienia nie są dostępne dla toouse w domenie hello. Istniejącego administratora domeny lub grupy administratora przedsiębiorstwa w katalogu usługi Azure AD również nie są przyznawane uprawnienia administratora domeny/enterprise na powitania domeny.

#### <a name="can-i-modify-group-memberships-using-ldap-or-other-ad-administrative-tools-on-managed-domains"></a>Można zmodyfikować członkostwa grupy przy użyciu protokołu LDAP lub innych narzędzi administracyjnych AD w domenach zarządzanych?
Nie. Nie można zmodyfikować członkostwa w grupach w domenach obsługiwanych przez usługi domenowe Azure AD. Witaj, który dotyczy dla atrybutów użytkownika. Można jednak zmienić atrybuty użytkownika lub członkostwa w grupach w usłudze Azure AD lub w domenie lokalnej. Zmiany te są automatycznie synchronizowane tooAzure AD usług domenowych w usłudze.

#### <a name="how-long-does-it-take-for-changes-i-make-toomy-azure-ad-directory-toobe-visible-in-my-managed-domain"></a>Jak długo trwa zmian I uwidocznić toomy usługi Azure AD directory toobe w mojej domeny zarządzanej?
Zmiany wprowadzone w katalogu usługi Azure AD przy użyciu hello interfejsu użytkownika programu Azure AD lub programu PowerShell są synchronizowane tooyour domeny zarządzanej. Ten proces synchronizacji działa w tle hello. Po zakończeniu hello jednorazowego wstępnej synchronizacji katalogu on zwykle trwa około 20 minut, aby zmiany wprowadzone w usłudze Azure AD toobe odzwierciedlone w domeny zarządzanej.

#### <a name="can-i-extend-hello-schema-of-hello-managed-domain-provided-by-azure-ad-domain-services"></a>Czy można rozszerzyć schemat hello hello domeny zarządzanej udostępniane przez usługi domenowe Azure AD?
Nie. Schemat Hello jest zarządzany przez firmę Microsoft do domeny zarządzanej hello. Rozszerzenia schematu nie są obsługiwane przez usługi domenowe Azure AD.

#### <a name="can-i-modify-or-add-dns-records-in-my-managed-domain"></a>Można zmodyfikować lub dodać rekordy DNS w mojej domeny zarządzanej?
Tak. Członkowie grupy hello "Administratorzy kontrolera domeny usługi AAD" są przyznawane uprawnienia administratora DNS toomodify rekordy DNS w domenie zarządzanej hello. Ich za pomocą konsoli Menedżera DNS hello na maszynie uruchomionego systemu Windows Server toohello przyłączone do domeny zarządzanej, toomanage DNS. Witaj toouse konsoli Menedżera DNS, zainstaluj "Narzędzia serwera DNS", która jest częścią opcjonalna funkcja "Narzędzia administracji zdalnej serwera" hello na powitania serwera. Więcej informacji na temat [narzędzia do zarządzania, monitorowania i rozwiązywania problemów DNS](https://technet.microsoft.com/library/cc753579.aspx) jest dostępna w witrynie TechNet.

### <a name="billing-and-availability"></a>Rozliczeń i dostępności
#### <a name="is-azure-ad-domain-services-a-paid-service"></a>Jest usługą płatną usług domenowych Azure AD?
Tak. Aby uzyskać więcej informacji, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/active-directory-ds/).

#### <a name="is-there-a-free-trial-for-hello-service"></a>Czy istnieje bezpłatna wersja próbna usługi hello?
Ta usługa jest objęta hello bezpłatna wersja próbna platformy Azure. Możesz zarejestrować się w celu [w warstwie bezpłatna miesięczna wersja próbna systemu Azure](https://azure.microsoft.com/pricing/free-trial/).

#### <a name="can-i-get-azure-ad-domain-services-as-part-of-enterprise-mobility-suite-ems-do-i-need-azure-ad-premium-toouse-azure-ad-domain-services"></a>W ramach Enterprise Mobility Suite (EMS) można uzyskać usług domenowych Azure AD? Należy usług domenowych Azure AD Premium toouse usługi Azure AD?
Nie. Usługi domenowe Azure AD jest płatność za rzeczywiste użycie usługi Azure i nie jest częścią pakietu EMS. Usługi domenowe Azure AD może być używany z wszystkie wersje usługi Azure AD (bezpłatne, podstawowe i, Premium). Opłaty są naliczane co godzinę, w zależności od użycia.

#### <a name="what-azure-regions-is-hello-service-available-in"></a>Jakie regiony platformy Azure jest dostępna w hello usługi?
Zobacz toohello [regionów platformy Azure](https://azure.microsoft.com/regions/#services/) toosee strony listę hello regiony platformy Azure, w którym są dostępne usługi domenowe Azure AD.
