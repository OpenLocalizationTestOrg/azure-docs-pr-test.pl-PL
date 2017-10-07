---
title: "aaaAzure tożsamościami i dostępem najlepszych rozwiązań dotyczących zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera zestaw najlepsze rozwiązania w zakresie zarządzania tożsamościami i kontroli dostępu przy użyciu wbudowanych funkcji platformy Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 07d8e8a8-47e8-447c-9c06-3a88d2713bc1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/30/2017
ms.author: yurid
ms.openlocfilehash: af07dfda84758b9124641078ac8f696f725f2bf1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-identity-management-and-access-control-security-best-practices"></a>Azure Zarządzanie tożsamościami i dostępem kontrolować najlepszych rozwiązań dotyczących zabezpieczeń
Wiele należy wziąć pod uwagę toobe hello nowych granic warstwy tożsamości zabezpieczeń przejęcia tej roli z punktu widzenia skoncentrowane sieci tradycyjnych hello. Ten rozwój hello pivot głównej uwagi bezpieczeństwa i inwestycje pochodzą z hello na fakt, że strefy sieci stały się coraz bardziej porowaty i obrony ten obwód nie może być skuteczne raz były rozwinięcie wcześniejsze toohello [BYOD](http://aka.ms/byodcg) urządzeń i aplikacji w chmurze.

W tym artykule omówiono kolekcja zarządzania tożsamość platformy Azure i najlepsze rozwiązania zabezpieczeń kontroli dostępu. Następujące najlepsze rozwiązania są uzyskiwane z wiemy z doświadczenia z [usługi Azure AD](../active-directory/active-directory-whatis.md) i doświadczenia hello klientów, takich jak samodzielnie.

Dla każdego ze względów wyjaśniamy:

* Jakie hello najlepszym rozwiązaniem jest
* Dlaczego chcesz tooenable tej najlepsze praktyki
* Co może wynikać hello tooenable hello najlepszym rozwiązaniem w przeciwnym przypadku
* Najlepszym rozwiązaniem toohello możliwe alternatywy
* Jak można znaleźć tooenable hello najlepsze praktyki

Ta tożsamość platformy Azure zarządzania i dostęp kontroli zabezpieczeń, najlepsze rozwiązania dotyczące na podstawie opinii konsensu i funkcji platformy Azure i zestawy funkcji istniejących w chwili hello, który został zapisany w tym artykule. Opinie i technologie ulegną zmianom i będą w tym artykule zaktualizowane na tooreflect regularnie tych zmian.

Tożsamość platformy Azure zarządzania i dostęp do sterowania najlepsze rozwiązania omówione w tym artykule obejmują:

* Scentralizowane zarządzanie tożsamościami
* Włącz logowanie jednokrotne (SSO)
* Wdrażanie zarządzania hasłami
* Wymusić uwierzytelnianie wieloskładnikowe (MFA) dla użytkowników
* Kontrola dostępu (RBAC) oparta na rolach użycia
* Lokalizacje kontroli, gdy zasoby są tworzone za pomocą Menedżera zasobów
* Przewodnik deweloperów tooleverage tożsamości możliwości dla aplikacji SaaS
* Aktywne monitorowanie dla podejrzanych działań

## <a name="centralize-your-identity-management"></a>Scentralizowane zarządzanie tożsamościami
Jeden ważnym krokiem do zabezpieczania tożsamości jest tooensure IT mogą zarządzać kontami z jednej lokalizacji pojedynczego, o której utworzono to konto. Większość hello hello przedsiębiorstw IT organizacji będzie miał ich kontem podstawowym katalogu lokalnego, gdy chmury hybrydowej znajdują się na powitania wzrostu i ważne jest zrozumienie sposobu toointegrate lokalne i katalogi w chmurze i podaj nie zakłóca pracy użytkownika końcowego toohello.

tooaccomplish to [tożsamość hybrydowa](../active-directory/active-directory-hybrid-identity-design-considerations-overview.md) scenariuszu zaleca się dwie opcje:

* Synchronizacji katalogu lokalnego z katalogiem chmury, za pomocą programu Azure AD Connect
* Utworzenie federacji tożsamości lokalnych z katalogu chmurze przy użyciu [Active Directory Federation Services](https://msdn.microsoft.com/library/bb897402.aspx) (AD FS)

Organizacje, które nie są toointegrate, który może wystąpić tożsamości lokalnych z ich tożsamość w chmurze zwiększyć administracyjne obciążenie w zarządzanie kontami, co zwiększa prawdopodobieństwo hello błędów i naruszeń zabezpieczeń.

Więcej informacji o synchronizacji usługi Azure AD, przeczytaj artykuł hello [integrowanie tożsamości lokalnych z usługą Azure Active Directory](../active-directory/active-directory-aadconnect.md).

## <a name="enable-single-sign-on-sso"></a>Włącz logowanie jednokrotne (SSO)
Jeśli masz wiele katalogów toomanage staje się on administracyjne problem nie tylko w przypadku IT, ale także dla użytkowników końcowych, które będą miały tooremember wiele haseł. Za pomocą [logowania jednokrotnego](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) będzie zapewnić użytkownikom możliwość hello hello Użyj sam zestaw poświadczeń toosign w i uzyskiwać dostęp do zasobów hello, których potrzebują, bez względu na to w przypadku tego zasobu znajdujących się lokalnie lub w chmurze hello.

Użyj logowania jednokrotnego tooenable użytkowników tooaccess ich [aplikacji SaaS](../active-directory/active-directory-appssoaccess-whatis.md) oparte na swoje konta organizacyjne w usłudze Azure AD. Ma to zastosowanie nie tylko dla aplikacji SaaS firmy Microsoft, ale także inne aplikacje, takie jak [usługi Google Apps](../active-directory/active-directory-saas-google-apps-tutorial.md) i [Salesforce](../active-directory/active-directory-saas-salesforce-tutorial.md). Aplikacja może być skonfigurowany toouse usługi Azure AD jako [tożsamość oparta na SAML](../active-directory/fundamentals-identity.md) dostawcy. Jako formant zabezpieczeń usługi Azure AD nie będzie wystawiać token, dzięki czemu toosign do aplikacji hello jeśli przyznano im dostęp przy użyciu usługi Azure AD. Możesz udzielić dostępu bezpośrednio lub za pośrednictwem grupy są członkami.

> [!NOTE]
> Hello decyzji toouse logowania jednokrotnego zostanie wpływ na sposób integracji katalogu lokalnego z katalogiem w chmurze. Chcąc logowania jednokrotnego, konieczne będzie toouse Federacji, ponieważ udostępni jedynie synchronizacji katalogów [tego samego środowiska logowania jednokrotnego](../active-directory/active-directory-aadconnect.md).
>
>

Organizacje, które nie wymuszają logowania jednokrotnego dla swoich użytkowników i aplikacje są bardziej narażona tooscenarios gdzie użytkownicy będą mieć wiele haseł, które bezpośrednio zwiększa prawdopodobieństwo hello użytkowników ponowne użycie hasła lub przy użyciu słabe hasła.

Możesz można dowiedzieć się więcej o rejestracji Jednokrotnej programu Azure AD od przeczytania artykułu hello [zarządzania usług AD FS i dostosowywania z programem Azure AD Connect](../active-directory/active-directory-aadconnect-federation-management.md).

## <a name="deploy-password-management"></a>Wdrażanie zarządzania hasłami
W scenariuszach, w którym masz wielu dzierżawców lub użytkownicy tooenable zbyt[zresetować swoje hasła](../active-directory/active-directory-passwords-update-your-own-password.md), należy użyć zabezpieczeń odpowiednich zasad tooprevent nadużycia jest. Na platformie Azure można wykorzystać funkcję resetowania hasła samoobsługi hello i dostosować toomeet opcje zabezpieczeń hello wymagań biznesowych.

Jest szczególnie ważne tooobtain opinie od tych użytkowników i Dowiedz się ze swoimi doświadczeniami podczas tooperform następujące kroki. W oparciu o te funkcje, opracowania planu toomitigate potencjalne problemy, które mogą wystąpić podczas wdrażania hello większej grupy. Zalecane jest również, że używasz hello [raport aktywności rejestracji resetowania haseł](../active-directory/active-directory-passwords-get-insights.md) toomonitor hello użytkowników, którzy rejestracji.

Organizacje, które mają hasło tooavoid zmiany wywołań obsługi, ale należy włączać tooreset użytkowników swoje hasła są bardziej narażony tooa wyższe wywołania woluminu toohello działu powodu toopassword problemów. W organizacjach z wieloma dzierżawcami konieczne jest wdrożenie tego typu możliwości, a następnie włączyć funkcję resetowania w granicach zabezpieczeń, które zostały określone w zasadach zabezpieczeń hello hasła tooperform użytkowników.

Dowiedz się więcej o Resetowanie hasła przy czytania artykułu hello [wdrażanie Zarządzanie hasłami oraz szkolenie użytkowników toouse go](../active-directory/active-directory-passwords-best-practices.md).

## <a name="enforce-multi-factor-authentication-mfa-for-users"></a>Wymusić uwierzytelnianie wieloskładnikowe (MFA) dla użytkowników
Dla organizacji, które muszą toobe zgodny ze standardami branżowymi, takich jak [PCI DSS w wersji 3.2](http://blog.pcisecuritystandards.org/preparing-for-pci-dss-32), uwierzytelnianie wieloskładnikowe jest musi mieć możliwość uwierzytelniania użytkowników. Poza jest zgodny ze standardami branżowymi, wymuszając uwierzytelnianie wieloskładnikowe tooauthenticate użytkowników może również pomóc typ kradzieży poświadczeń organizacji toomitigate ataku, takich jak [Pass--Hash (PtH)](http://aka.ms/PtHPaper).

Włączanie usługi Azure MFA dla użytkowników, dodajesz drugą warstwę logowania toouser zabezpieczeń i transakcji. W takim przypadku transakcji może uzyskiwać dostęp do dokumentu znajdującego się na serwerze plików lub w trybie Online programu SharePoint. Usługa Azure MFA pomaga również IT tooreduce hello prawdopodobieństwo, że przejęciem poświadczeń tooorganization dostępu do danych.

Na przykład: Wymuszanie usługi Azure MFA dla użytkowników i skonfigurować toouse Rozmowa telefoniczna lub wiadomości tekstowej jako weryfikacji. Naruszenie poświadczenia użytkownika hello atakująca hello nie być możliwe tooaccess dowolnego zasobu, ponieważ on nie będą miały dostępu toouser telefonu. Organizacje, które nie należy dodawać dodatkowych warstw ochrony tożsamości są bardziej narażony na atak kradzieży poświadczeń, co może prowadzić do naruszenia toodata.

Jeden alternatywą dla organizacji, które mają kontroli cały proces uwierzytelniania hello tookeep lokalnej jest toouse [serwera usługi Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-server.md), nazywany również lokalne usługi MFA. Za pomocą tej metody, będą mogli tooenforce uwierzytelnianie wieloskładnikowe, przy zachowaniu hello MFA serwera lokalnego.

Aby uzyskać więcej informacji dotyczących usługi Azure MFA, przeczytaj artykuł hello [wprowadzenie do korzystania z usługi Azure Multi-Factor Authentication w chmurze hello](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

## <a name="use-role-based-access-control-rbac"></a>Kontrola dostępu (RBAC) oparta na rolach użycia
Ograniczanie dostępu oparte na powitania [muszą tooknow](https://en.wikipedia.org/wiki/Need_to_know) i [najniższych uprawnień](https://en.wikipedia.org/wiki/Principle_of_least_privilege) jest zasad bezpieczeństwa dla firm, które chcą tooenforce zasad zabezpieczeń dla dostępu do danych. Azure opartej na rolach kontroli dostępu (RBAC) może być używane tooassign toousers uprawnienia, grup i aplikacji w zakresie niektórych. Witaj zakres przypisania roli może być pojedynczego zasobu, grupy zasobów lub subskrypcji.

Można wykorzystać [wbudowane RBAC](../active-directory/role-based-access-built-in-roles.md) role w programie Azure tooassign toousers uprawnienia. Należy rozważyć użycie *współautora konta magazynu* dla operatorów chmury, które wymagają konta magazynu toomanage i *klasycznego współautora konta magazynu* roli toomanage klasycznych kont magazynu. Operatorom chmury, które musi toomanage maszyn wirtualnych i konto magazynu, należy rozważyć dodanie ich zbyt*Współautor·maszyny·wirtualnej* roli.

Organizacje, które nie wymusić kontrolę dostępu danych dzięki wykorzystaniu możliwości, takie jak RBAC może nadanie więcej uprawnień niż niezbędne tootheir użytkowników. Może to spowodować naruszenie toodata przez umożliwienia użytkownikom dostępu typów toocertain danych (np. duże znaczenie biznesowe), które nie mają one w miejscu pierwszego hello.

Użytkownik może dowiedzieć się więcej o Azure RBAC od przeczytania artykułu hello [kontroli dostępu](../active-directory/role-based-access-control-configure.md).

## <a name="control-locations-where-resources-are-created-using-resource-manager"></a>Lokalizacje kontroli, gdy zasoby są tworzone za pomocą Menedżera zasobów
Włączenie zadań tooperform operatory chmurze podczas uniemożliwia zasady dzielenia potrzebne toomanage zasobów organizacji jest bardzo ważne. Organizacje, które mają lokalizacje hello toocontrol, gdy zasoby są tworzone twarde powinny kodu tych lokalizacjach.

tooachieve, organizacje mogą tworzyć zasady zabezpieczeń, które zawierają definicje, które opisują akcje hello lub zasobów, które nie są specjalnie. Można przypisać te definicje zasad w zakresie hello potrzebne, takich jak hello subskrypcji, grupy zasobów lub pojedynczych zasobów.

> [!NOTE]
> to jest nie hello takie same jak RBAC, faktycznie wykorzystuje RBAC tooauthenticate hello użytkowników, którzy mają uprawnienia toocreate tych zasobów.
>
>

Wykorzystywanie [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) toocreate niestandardowych zasad również w scenariuszach, w którym hello organizacja chce tooallow operacje tylko gdy hello Centrum kosztów odpowiedniego jest skojarzony; w przeciwnym razie będzie odmawiał hello żądania.

Organizacje, które nie są kontrolowanie sposobu tworzenia zasobów są bardziej narażony toousers, który może nadużyć usługi hello tworząc więcej zasobów niż jest to wymagane. Wzmacnianie ochrony procesu tworzenia zasobu hello jest ważnym krokiem toosecure scenariusza z wieloma dzierżawcami.

Dowiedz się więcej na temat tworzenia zasad za pomocą Menedżera zasobów Azure, przeczytaj artykuł hello [zasady toomanage zasobów i kontroli dostępu](../azure-resource-manager/resource-manager-policy.md).

## <a name="guide-developers-tooleverage-identity-capabilities-for-saas-apps"></a>Przewodnik deweloperów tooleverage tożsamości możliwości dla aplikacji SaaS
Tożsamość użytkownika będzie można użyć w wielu scenariuszach, gdy użytkownicy uzyskują dostęp do [aplikacji SaaS](https://azure.microsoft.com/marketplace/active-directory/all/) którego można zintegrować z lokalnymi lub katalogu w chmurze. Najpierw i, zalecane jest deweloperom użycie toodevelop bezpiecznego metodologii tych aplikacji, takich jak [Microsoft Security Development Lifecycle (SDL)](https://www.microsoft.com/sdl/default.aspx). Usługi Azure AD upraszcza uwierzytelniania dla deweloperów, podając tożsamości jako usługa, obsługuje protokoły przemysłowe oraz protokoły takich jak [OAuth 2.0](http://oauth.net/2/) i [OpenID Connect](http://openid.net/connect/), a także typu open source biblioteki dla różnych platform.

Upewnij się, że tooregister dowolnej aplikacji, która outsources tooAzure uwierzytelniania AD, jest to procedura obowiązkowe. to powód Hello jest, ponieważ usługi Azure AD musi toocoordinate hello komunikacji z aplikacją hello, gdy obsługa logowania jednokrotnego (SSO) lub wymiana tokenów. Hello sesja wygasa po upływie okresu istnienia hello hello token wystawiony przez usługę Azure AD. Zawsze należy ocenić, jeśli aplikacja powinna używać tej chwili lub ten czas można skrócić. Zmniejszenie hello okresu istnienia może działać jako miary zabezpieczeń, która wymusi toosign użytkowników wychodzących na podstawie w okresie braku aktywności.

Organizacje, które nie wymuszają tożsamości kontrola tooaccess aplikacji nie deweloperów na i jak toosecurely integracji aplikacji z ich tożsamości systemu zarządzania może być bardziej narażony toocredential kradzieży rodzaj ataku, takich jak [słabe uwierzytelnianie i sesji zarządzania opisane w otwartych sieci Web aplikacji zabezpieczeń projektu (OWASP) pierwszych 10](https://www.owasp.org/index.php/OWASP_Top_Ten_Cheat_Sheet).

Użytkownik może dowiedzieć się więcej o scenariusze uwierzytelniania dla aplikacji SaaS odczytując [scenariusze uwierzytelniania dla usługi Azure AD](../active-directory/active-directory-authentication-scenarios.md).

## <a name="actively-monitor-for-suspicious-activities"></a>Aktywne monitorowanie dla podejrzanych działań
Zgodnie z zbyt[raport naruszenia danych 2016 Verizon](http://www.verizonenterprise.com/verizon-insights-lab/dbir/2016/), przejęcie poświadczeń są nadal prowadzić hello i staje się jedną z najbardziej dochodowe firm powitania dla przez przestępców. Dlatego jest ważne toohave system monitor aktywnej tożsamości w miejscu, które można szybko wykrywać podejrzane działania i wywoływać alert dla dalszego postępowania. Usługa Azure AD ma dwa główne możliwości, które pomaga organizacjom monitorować ich tożsamości: Azure AD Premium [raporty anomalii](../active-directory/active-directory-view-access-usage-reports.md) i Azure AD [ochronę tożsamości](../active-directory/active-directory-identityprotection.md) możliwości.

Upewnij się, że toouse hello anomalii raporty tooidentify prób toosign w [bez śledzone](../active-directory/active-directory-reporting-sign-ins-from-unknown-sources.md), [siłowych](../active-directory/active-directory-reporting-sign-ins-after-multiple-failures.md) ataków określonego konta, toosign prób w wielu lokalizacjach, zaloguj się z [zainfekowanych urządzeń](../active-directory/active-directory-reporting-sign-ins-from-possibly-infected-devices.md) i podejrzane adresy IP. Należy pamiętać, że są one raportów. Innymi słowy musi mieć procesy i procedury umieścić toorun Administratorzy IT te raporty na codziennie hello lub na żądanie (zazwyczaj w scenariuszu odpowiedzi na zdarzenia).

Z kolei usługi Azure AD identity protection jest aktywnego monitorowania systemu i będzie Flaga hello ryzyka bieżącego na jego własnej pulpitu nawigacyjnego. Oprócz, otrzymasz również dzienne podsumowanie powiadomienia pocztą e-mail. Firma Microsoft zaleca, aby dostosować poziom ryzyka hello zgodnie z wymaganiami biznesowymi tooyour. Hello poziom ryzyka dla zdarzenia ryzyka będzie wskazywać ważność hello hello ryzyka zdarzenia (wysoki, średni lub niski). poziom ryzyka Hello ułatwia użytkownikom ochronę tożsamości priorytety hello akcje, które muszą podjąć tooreduce hello ryzyka tootheir organizacji.

Organizacje, które aktywnie nie monitorowania systemów tożsamości się ryzyko naruszenia zabezpieczeń poświadczeń użytkownika. Bez wiedzy, która podejrzanych działań są zbyt umieść przy użyciu tych poświadczeń, organizacje nie będzie możliwe toomitigate tego rodzaju zagrożenia.
Możesz można dowiedzieć się więcej o ochronę tożsamości Azure odczytując [Azure Active Directory Identity Protection](../active-directory/active-directory-identityprotection.md).
