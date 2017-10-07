---
title: "aaaAzure Zarządzanie zabezpieczeniami i monitorowanie — Przegląd | Dokumentacja firmy Microsoft"
description: " Platforma Azure udostępnia tooaid mechanizmy zabezpieczeń hello zarządzania i monitorowania usług w chmurze Azure i maszyn wirtualnych.  W tym artykule omówiono te podstawowe funkcje zabezpieczeń i usług. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 0026fa97bab7e15c9f8de6856b5075abe2288f61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a>Zabezpieczeń platformy Azure, zarządzania i monitorowania — omówienie
Platforma Azure udostępnia tooaid mechanizmy zabezpieczeń hello zarządzania i monitorowania usług w chmurze Azure i maszyn wirtualnych. W tym artykule omówiono te podstawowe funkcje zabezpieczeń i usług. Łącza podano tooarticles, który podać szczegóły każdego z nich, aby dowiedzieć się więcej.

bezpieczeństwo Hello usług w chmurze firmy Microsoft jest powiązanie i udostępnionych odpowiedzialność między Tobą a firmą Microsoft. Odpowiedzialność udostępnionego oznacza, że firmy Microsoft jest odpowiedzialny za hello Microsoft Azure i zabezpieczenia fizyczne centrów danych (przy użyciu ochrony zabezpieczeń, takich jak zablokowanym wskaźnika wejścia drzwi, ogrodzenia i osłony). Ponadto platforma Azure udostępnia silne poziomów zabezpieczeń chmurze w warstwie oprogramowania hello, spełniającej hello zabezpieczeń, prywatności i zgodności potrzeby jego wymagających klientów.

Jesteś właścicielem Twoje dane i tożsamości, odpowiedzialność hello ochrony je, hello zabezpieczeń zasobów lokalnych i zabezpieczeń hello składników chmury, nad którymi zarządzasz. Firma Microsoft dostarcza z toohelp kontrolek i funkcji zabezpieczeń ochrony danych i aplikacji. Twoje stopień odpowiedzialność za bezpieczeństwo jest oparty na typie hello usługi w chmurze.

powitania po wykresu zawiera podsumowanie saldo hello odpowiedzialności za firmę Microsoft, jak i powitania klienta.

![Wspólna odpowiedzialność][1]

Aby uzyskać bardziej zgłębić temat do zarządzania zabezpieczeniami, zobacz [Zarządzanie zabezpieczeniami na platformie Azure](azure-security-management.md).

Poniżej przedstawiono toobe funkcje podstawowe hello omówione w tym artykule:

* Kontrola dostępu oparta na rolach
* Oprogramowanie chroniące przed złośliwym kodem
* Multi-Factor Authentication
* ExpressRoute
* Bramy sieci wirtualnej
* Zarządzanie tożsamościami uprzywilejowanymi
* Ochrona tożsamości
* Security Center

## <a name="role-based-access-control"></a>Kontrola dostępu oparta na rolach
Kontrola dostępu oparta na rolach (RBAC) umożliwia precyzyjne zarządzanie dostępem do zasobów platformy Azure. Przy użyciu funkcji RBAC, można przyznać osób tylko hello takiego dostępu, że powinni tooperform swoich zadań.  RBAC ułatwia również upewnij się, że gdy osób pozostawia organizacji hello utracą tooresources dostęp w chmurze hello.

Więcej informacji:

* [Blog zespołu usługi Active Directory na RBAC](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [Kontrola dostępu oparta na rolach na platformie Azure](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a>Oprogramowanie chroniące przed złośliwym kodem
Przy użyciu platformy Azure można użyć ochrony przed złośliwym oprogramowaniem z dostawców głównych zabezpieczeń, takich jak Microsoft, firmy Symantec, Trend Micro, McAfee i Kaspersky toohelp ochrony maszyn wirtualnych z złośliwych plików, adware i innymi zagrożeniami.

Microsoft Antimalware oferuje hello tooinstall możliwości agenta ochrony przed złośliwym kodem dla ról PaaS i maszyny wirtualne. W oparciu o System Center Endpoint Protection, ta funkcja przełącza sprawdzonych lokalnymi chmury toohello technologii zabezpieczeń.

Oferujemy również głęboką integrację dla trendu [głębokie zabezpieczeń](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ i [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ produktów hello platformy Azure. DeepSecurity to rozwiązanie w zakresie oprogramowania antywirusowego i SecureCloud to rozwiązanie do szyfrowania. DeepSecurity jest wdrażany wewnątrz maszyn wirtualnych przy użyciu modelu rozszerzenia. Przy użyciu interfejsu użytkownika portalu hello i programu PowerShell, można wybrać toouse DeepSecurity wewnątrz nowych maszyn wirtualnych, które są jest uruchomione lub istniejących maszyn wirtualnych, które są już wdrożone.

Symantec ochrony punktu końcowego (wrz) jest również obsługiwany na platformie Azure. Dzięki integracji portalu klientów można określić, czy mają one toouse wrz w maszynie Wirtualnej. WRZ można zainstalować na zupełnie nowej maszyny Wirtualnej za pośrednictwem portalu Azure hello lub można ją zainstalować na istniejącej maszyny Wirtualnej przy użyciu programu PowerShell.

Więcej informacji:

* [Wdrażanie rozwiązań do ochrony przed złośliwym kodem na maszynach wirtualnych platformy Azure](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [Ochrony przed złośliwym oprogramowaniem firmy Microsoft dla usług w chmurze Azure i maszyn wirtualnych](azure-security-antimalware.md)
* [Jak tooinstall i skonfigurować Trend Micro głębokie zabezpieczeń jako usługa na maszynie Wirtualnej systemu Windows](../virtual-machines/windows/classic/install-trend.md)
* [Jak tooinstall i skonfigurować Symantec Endpoint Protection na maszynie Wirtualnej systemu Windows](../virtual-machines/windows/classic/install-symantec.md)
* [Nowe opcje ochrony przed złośliwym kodem ochrony maszyn wirtualnych platformy Azure — McAfee programu Endpoint Protection](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a>Multi-Factor Authentication
Usługa Azure Multi-Factor authentication (MFA) jest metoda uwierzytelniania, która wymaga użycia hello więcej niż jednej metody weryfikacji i dodaje kluczową drugą warstwę logowania toouser zabezpieczeń i transakcji. MFA ułatwia zabezpieczenie dostępu toodata i aplikacje spełniając zapotrzebowanie na prosty proces logowania. Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji — połączenie telefoniczne, wiadomość tekstowa lub aplikacja mobilna weryfikacji lub powiadamiania o kodzie i innych firm tokenów OATH.

Więcej informacji:

* [Multi-Factor Authentication](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [Co to jest usługa Multi-Factor Authentication platformy Azure?](../multi-factor-authentication/multi-factor-authentication.md)
* [Jak działa usługa Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a>ExpressRoute
Microsoft Azure ExpressRoute pozwala rozszerzyć sieci lokalnej na powitania firmy Microsoft w chmurze za pośrednictwem dedykowanego połączenia prywatne w ramach dostawcy łączności. Z usługi ExpressRoute można ustanowić połączenia usług chmury tooMicrosoft, takich jak Microsoft Azure, Office 365 i CRM Online. Połączenie może być z sieci typu dowolna-dowolna (IP VPN), sieci Ethernet typu punkt-punkt lub przy użyciu łączności obejmującej wiele połączeń wirtualnych przez dostawcę połączenia w ramach infrastruktury współlokacji. Połączenia ExpressRoute nie został przekroczony hello publicznej sieci Internet. Dzięki toooffer połączeń ExpressRoute więcej niezawodności, szybkości szybsze niższe opóźnienia i lepsze zabezpieczenia niż typowe połączenia za pośrednictwem Internetu hello.

Więcej informacji:

* [Opis techniczny ExpressRoute](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a>Bramy sieci wirtualnej
Bramy sieci VPN, nazywany również bramy sieci wirtualnej Azure, są używane toosend ruchu sieciowego między sieciami wirtualnymi i lokalizacji lokalnej. Są one również używane toosend ruchu między wieloma sieciami wirtualnymi w obrębie platformy Azure (VNet-VNet).  Bramy sieci VPN zapewniają łączność bezpiecznego między lokalizacjami platformy Azure i infrastruktury.

Więcej informacji:

* [Temat bram sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [Przegląd zabezpieczeń sieci platformy Azure](security-network-overview.md)

## <a name="privileged-identity-management"></a>Privileged Identity Management
Czasami użytkownicy muszą toocarry operacje uprzywilejowane w zasobów platformy Azure lub innych aplikacji SaaS. Często oznacza to, organizacje mają toogive ich stałe uprzywilejowanego dostępu w usłudze Azure Active Directory (Azure AD). Jest to zagrożenie bezpieczeństwa rosnącym zasobów hostowanych w chmurze, ponieważ organizacje wystarczająco nie można monitorować, co robią tych użytkowników z ich uprzywilejowanego dostępu.
Ponadto w przypadku złamania zabezpieczeń konta użytkownika z dostępem uprzywilejowanym tego naruszenia co może mieć wpływ na ogólną zabezpieczeń chmury. Azure AD Privileged Identity Management pomaga tooresolve to ryzyko przez co zmniejsza czas ekspozycji hello uprawnień i zwiększając wydajność wgląd w użycie.  

Zarządzanie tożsamościami uprzywilejowanymi wprowadzono pojęcie hello tymczasowego administratora dla roli lub "just in time" uprawnienia dostępu administratora, który jest użytkownik, który musi toocomplete procesu aktywacji dla danego przypisaną rolę. Witaj procesu aktywacji hello przypisania roli tooa użytkownika hello w usłudze Azure AD z nieaktywnych tooactive w określonym przedziale czasu takich jak ośmiu godzin.

Więcej informacji:

* [Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md)
* [Wprowadzenie do usługi Azure AD Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a>Identity Protection
Ochronę tożsamości w usłudze Azure Active Directory (AD) zapewnia skonsolidowanego widoku podejrzanych działań logowania i potencjalnych luk w zabezpieczeniach toohelp ochronę firmy. Identity Protection wykrywa podejrzane działania dla użytkowników i tożsamości uprzywilejowanych (Administrator), oparte na sygnały jak ataków siłowych ujawnione poświadczenia i logowania z nieznanych lokalizacji i zainfekowanych urządzeń.

Zapewniając powiadomień i zalecanych czynności naprawczych, Identity Protection pomaga toomitigate zagrożeń w czasie rzeczywistym. Ważność ryzyka użytkownika jest obliczana i można skonfigurować zasady oparte na ryzyko tooautomatically pomocy zabezpieczenie dostępu do aplikacji przed zagrożeniami w przyszłości.

Więcej informacji:

* [Ochronę tożsamości usługi Azure Active Directory](../active-directory/active-directory-identityprotection.md)
* [Kanał 9: Usługi Azure AD i Pokaż tożsamości: Podgląd ochrony tożsamości](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a>Security Center
Centrum zabezpieczeń Azure pomaga zapobiec, wykrywania i reagowania toothreats i zapewnia zwiększyć widoczność i kontrolę nad, hello zabezpieczeń zasobów platformy Azure. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

Centrum zabezpieczeń ułatwia optymalizacji i monitorować hello zabezpieczeń zasobów platformy Azure przez:

* Umożliwiając toodefine zasady dla zasobów subskrypcji platformy Azure zgodnie z tooyour zabezpieczeń firmy użytkownika wymaga oraz hello typem aplikacji oraz poufności hello danych w każdej subskrypcji.
* Monitorowanie stanu hello Azure maszyn wirtualnych, sieci i aplikacji.
* Udostępnia listę priorytety alerty zabezpieczeń, między innymi alertów ze zintegrowanych partnera zbadać rozwiązania, wraz z informacjami hello należy tooquickly i zalecenia dotyczące tooremediate atak.

Więcej informacji:

* [Wprowadzenie tooAzure Centrum zabezpieczeń](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png
