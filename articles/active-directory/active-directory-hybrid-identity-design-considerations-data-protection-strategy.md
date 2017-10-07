---
title: "aaaAzure usługi Active Directory hybrydowego zagadnienia dotyczące projektowania tożsamości — Definiowanie strategii ochrony danych | Dokumentacja firmy Microsoft"
description: "Strategię ochrony danych hello będziesz definiować dla hybrydowych tożsamości rozwiązania toomeet hello wymagań biznesowych zdefiniowane."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: e76fd1f4-340a-492a-84d9-e05f3b7cc396
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 8fd7ab364a09de3b60293a4a1cbb6e0fa4a3295d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="define-data-protection-strategy-for-your-hybrid-identity-solution"></a>Definiowanie strategii ochrony danych dla rozwiązania z tożsamością hybrydową
W tym zadaniu dla hybrydowych tożsamości rozwiązania toomeet hello wymagań biznesowych zdefiniowane w będziesz definiować strategii ochrony danych hello:

* [Określenie wymagań dotyczących ochrony danych](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md)
* [Określenie wymagań dotyczących zarządzania zawartością](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)
* [Określenie wymagań dotyczących kontroli dostępu](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)
* [Określenie wymagań dotyczących odpowiedzi na zdarzenia](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="define-data-protection-options"></a>Zdefiniuj opcje ochrony danych
Opisane w [określenie wymagań synchronizacji katalogu](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md), Microsoft Azure AD mogą wykonywać synchronizację z z usług domenowych Active Directory (AD DS) znajdujących się na lokalnych. Integracja umożliwia organizacjom tooleverage usługi Azure AD tooverify poświadczeń użytkownika, gdy usiłują tooaccess zasobów firmy. Można to zrobić w obu przypadkach: dane na rest lokalnie i w chmurze hello.  Toodata dostępu w usłudze Azure AD wymaga uwierzytelnienia użytkownika za pośrednictwem usługi tokenu zabezpieczającego (STS).

Po uwierzytelnieniu hello nazwa główna użytkownika (UPN) jest do odczytu z tokenu uwierzytelniania hello i replikowane hello partycji i odpowiadającego kontenera jest określana toohello użytkownika domeny. Informacje dotyczące istnienia, włączona i roli użytkownika hello jest używany przez hello autoryzacji systemu toodetermine czy hello żądany dostęp toohello docelowej dzierżawy jest autoryzowany do tego użytkownika w tej sesji. Pewne akcje autoryzowanych (w szczególności utworzyć użytkownika, resetowanie hasła) Utwórz dziennik inspekcji, które mogą być używane przez dzierżawcę wysiłków zgodności toomanage administratora lub dochodzenia.

Przenoszenie danych z centrum danych lokalnych w magazynie Azure przez połączenie internetowe mogą nie być możliwe toodata woluminu, dostępnej przepustowości lub innych kwestii. Witaj [usługi Import/Eksport magazynu Azure](../storage/common/storage-import-export-service.md) zapewnia oparte na sprzęcie opcję dla wprowadzania do pobierania dużych ilości danych w magazynie obiektów blob. Umożliwia toosend [zaszyfrowane przez funkcję BitLocker](https://technet.microsoft.com/library/dn306081#BKMK_BL2012R2) dyski twarde bezpośrednio tooreturn dyski tooan centrum danych Azure gdzie operatorom chmury przekaże konta magazynu tooyour zawartość hello lub będą oni mogli pobrać tooyour Twojego danych Azure tooyou. Tylko dla zaszyfrowanych dysków uznane za zaakceptowane dla tego procesu (przy użyciu klucza funkcji BitLocker, generowane przez usługę hello się podczas instalacji zadania hello). klucza funkcji BitLocker Hello podano tooAzure oddzielnie, zapewniając poza pasmem klucza udostępniania.

Ponieważ przesyłanych danych może odbywać się w różnych scenariuszy, jest również odpowiedniego tooknow, który używa programu Microsoft Azure [sieci wirtualne](https://azure.microsoft.com/documentation/services/virtual-network/) ruchu dzierżawców tooisolate od siebie nawzajem stosowania środków, takich jak poziom hosta i gościa zapór, filtrowanie pakietów IP, port blokowania i punktów końcowych HTTPS. Jednak większość komunikacji wewnętrznej platformy Azure, w tym infrastruktury do infrastruktury i infrastruktury do klienta (lokalnego), również są szyfrowane. Inny scenariusz ważne jest komunikacja hello w centrach danych platformy Azure; Firma Microsoft zarządza tooassure sieci, maszyna wirtualna nie może spersonifikować lub podsłuchiwać hello adresu IP innego. Protokoły TLS/SSL jest używany podczas uzyskiwania dostępu do usługi Azure Storage lub baz danych lub połączenie tooCloud usług. W takim przypadku administrator klienta hello jest odpowiedzialny za uzyskiwanie certyfikatu TLS/SSL i wdrożeniem tootheir dzierżawy infrastruktury. Przenoszenie między maszynami wirtualnymi ruch danych w hello tego samego wdrożenia lub między dzierżawcami w ramach jednego wdrożenia za pośrednictwem sieci wirtualnej Microsoft Azure mogą być chronione przy użyciu protokołów szyfrowaną komunikację HTTPS, SSL/TLS lub innych użytkowników.

W zależności od tego, jak odpowiedzieć na pytania hello w [ustalenie wymagań dotyczących ochrony danych](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md), powinno być możliwe toodetermine jak chcesz tooprotect dane i jak może pomóc rozwiązania z tożsamością hybrydową hello na tym. Witaj tabeli przedstawiono opcje hello obsługiwany przez platformę Azure, które są dostępne dla każdego scenariusza ochrony danych.

| Opcje ochrony danych | Magazynowane w chmurze hello | W pozostałych lokalnymi | W drodze |
| --- | --- | --- | --- |
| Szyfrowanie dysków funkcją BitLocker |X |X | |
| Bazy danych programu SQL Server tooencrypt |X |X | |
| Szyfrowanie maszyny Wirtualnej do maszyny Wirtualnej | | |X |
| PROTOKÓŁ SSL/TLS | | |X |
| Sieć VPN | | |X |

> [!NOTE]
> Odczyt [zgodności przez funkcję](https://azure.microsoft.com/support/trust-center/services/) w [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) tooknow więcej o certyfikatach hello, które jest zgodne z każdej usługi Azure.
> Ponieważ hello opcje ochrony danych używa wielowarstwowych podejście, porównanie te opcje nie są stosowane dla tego zadania. Upewnij się, że są wykorzystuje wszystkie opcje dostępne dla każdego stanu, który będzie hello danych.
>
>

## <a name="define-content-management-options"></a>Zdefiniuj opcje zarządzania zawartością
Jedną z zalet przy użyciu usługi Azure AD toomanage hybrydowej infrastruktury tożsamości jest w pełni przezroczyste z perspektywy użytkownika końcowego hello hello procesu. Hello użytkownik spróbuje tooaccess zasobu udostępnionego, hello zasób wymaga uwierzytelnienia, hello użytkownik będzie miał toosend tooAzure żądania uwierzytelniania AD w kolejności tooobtain hello tokenu i uzyskiwać dostęp do zasobów hello. Całego procesu odbywa się w tle, bez interakcji z użytkownikiem. Możliwe jest również możliwe toogrant uprawnienia tooa [grupy](active-directory-manage-groups.md#getting-started-with-access-management) użytkowników w kolejności tooallow ich tooperform niektórych typowych akcji.

Organizacje, które są obawy dotyczące prywatności danych zwykle wymagają klasyfikacji danych dla ich rozwiązania. Jeśli ich bieżącej infrastruktury lokalnej jest już z klasyfikacji danych, jest możliwe tooleverage usługi Azure AD jako hello głównym repozytorium dla tożsamości użytkownika. Typowe narzędzia jest używane lokalnymi klasyfikacji danych jest nazywana [Data Classification Toolkit](https://msdn.microsoft.com/library/Hh204743.aspx) dla systemu Windows Server 2012 R2. To narzędzie może pomóc tooidentify, klasyfikować i chronić dane na serwerach plików w chmurze prywatnej. Możliwe jest również możliwe tooleverage hello [automatycznej klasyfikacji plików](https://technet.microsoft.com/library/hh831672.aspx) w systemie Windows Server 2012 tooaccomplish to.

Jeśli Twoja organizacja nie ma klasyfikacji danych w miejscu, ale wymaga tooprotect poufnych plików bez dodawania nowych serwerów lokalnych, może użyć Microsoft [usługi Azure Rights Management](https://technet.microsoft.com/library/JJ585026.aspx).  Usługa Azure RMS używa szyfrowania, tożsamości i autoryzacji toohelp zasady bezpiecznych plików i wiadomości e-mail i działa na wielu urządzeniach — telefonach, tablety i komputery. Ponieważ usługa Azure RMS to usługa w chmurze, nie istnieje potrzeba tooexplicitly konfigurowania relacji zaufania z innymi organizacjami przed udostępnieniem chronionej zawartości z nimi. Jeżeli korzystają już one usługi Office 365 lub katalogu usługi Azure AD, współpraca między organizacjami jest obsługiwana automatycznie. Możesz także zsynchronizować tylko katalogu hello atrybutów usługi Azure RMS wymaga toosupport wspólną tożsamością dla lokalnych kont usługi Active Directory przy użyciu usług Azure do synchronizacji Active Directory (AAD Sync) lub Azure AD Connect.

To ważna część zarządzania zawartością toounderstand, kto uzyskuje dostęp do zasobów, w związku z tym możliwość rejestrowania sformatowanego jest ważna w przypadku hello rozwiązania do zarządzania tożsamościami. Usługa Azure AD zapewnia dziennika ponad 30 dni, w tym:

* Zmiany w członkostwo roli (przykład: użytkownik dodał rolę administratora tooGlobal)
* Poświadczenia aktualizacji (przykład: zmiany hasła)
* Zarządzanie domenami (przykład: weryfikowanie domeny niestandardowej usuwania domeny)
* Dodawanie lub usuwanie aplikacji
* Zarządzanie użytkownikami (przykład: Dodawanie, usuwanie, aktualizowanie użytkownika)
* Dodawanie lub usuwanie licencji

> [!NOTE]
> Odczyt [zabezpieczeń firmy Microsoft Azure i zarządzanie dziennikiem inspekcji](http://download.microsoft.com/download/B/6/C/B6C0A98B-D34A-417C-826E-3EA28CDFC9DD/AzureSecurityandAuditLogManagement_11132014.pdf) tooknow więcej informacji na temat możliwości rejestrowania zdarzeń w systemie Azure.
> W zależności od tego, jak odpowiedzieć na pytania hello w [ustalić wymagania dotyczące zarządzania zawartością](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md), powinno być możliwe toodetermine sposób hello zawartości toobe zarządzane w rozwiązaniu tożsamości hybrydowej. Może być zintegrowany z usługą Azure AD są wszystkie opcje widoczne w tabeli 6, jest ważne toodefine, który jest bardziej odpowiednie do potrzeb biznesowych.
>
>

| Opcje zarządzania zawartością | Zalety | Wady |
| --- | --- | --- |
| Scentralizowanie lokalne (Active Directory Rights Management Server) |Pełną kontrolę nad infrastrukturą serwera hello odpowiedzialny za klasyfikacji danych hello <br> Wbudowane możliwości w systemie Windows Server, nie jest konieczne dodatkowe licencji lub subskrypcji <br> Można zintegrować z usługą Azure AD w scenariuszu hybrydowym <br> Obsługuje możliwości zarządzania (IRM) prawa informacji w usługach Online firmy Microsoft, takich jak Exchange Online i SharePoint Online, jak również usługi Office 365 <br> Obsługuje lokalne produkty serwerowe firmy Microsoft, takich jak Exchange Server, SharePoint Server i serwery plików, z systemem Windows Server i infrastrukturą klasyfikacji plików (FCI). |Nowszą, konserwacji (trzymać się aktualizacje, konfiguracji i potencjalne uaktualnienia), ponieważ IT jest właścicielem powitania serwera <br> Wymaga infrastruktury serwera lokalnego<br> Doesn'tleverage funkcji platformy Azure natywnie |
| Scentralizowanie w chmurze hello (Azure RMS) |Łatwiejsze toohello toomanage porównaniu rozwiązanie lokalnego <br> Może być zintegrowany z usługami AD DS w scenariuszu hybrydowym <br>  W pełni zintegrowana z usługą Azure AD <br> Nie wymaga serwera lokalnego w kolejności toodeploy hello usługi <br> Obsługuje lokalne produkty serwerowe firmy Microsoft, takich jak Exchange Server, SharePoint Server i serwery plików, z systemem Windows Server i klasyfikacji plików, infrastruktury (FCI) <br> IT, może mieć pełną kontrolę nad kluczem ich dzierżawy z funkcją BYOK. |Organizacja musi mieć subskrypcję chmury, która obsługuje usługę RMS <br> Organizacja musi mieć uwierzytelnianie użytkownika toosupport katalogu usługi Azure AD RMS |
| Hybrydowe (zintegrowana z usługi Azure RMS, lokalnymi Active Directory Rights Management Server) |W tym scenariuszu akumuluje zalety hello, scentralizowane lokalnie i w chmurze hello. |Organizacja musi mieć subskrypcję chmury, która obsługuje usługę RMS <br> Organizacja musi mieć uwierzytelnianie użytkownika toosupport katalogu usługi Azure AD RMS, <br> Wymaga połączenia między usługą w chmurze platformy Azure i lokalnej infrastruktury |

## <a name="define-access-control-options"></a>Zdefiniuj opcje kontroli dostępu
Dzięki wykorzystaniu hello uwierzytelniania, autoryzacji dostępu kontrolę i możliwości są dostępne w usłudze Azure AD będzie możliwe tooenable toouse Twojej firmy repozytorium tożsamości centralnej podczas stosowanie użytkowników i partnerów toouse rejestracji jednokrotnej (SSO), jak pokazano w hello na poniższej ilustracji:

![](./media/hybrid-id-design-considerations/centralized-management.png)

Scentralizowane zarządzanie i w pełni integracji z innych katalogów

Azure Active Directory zapewnia toothousands znak jednej aplikacji SaaS i lokalnej aplikacji sieci web. Przeczytaj hello [listę zgodności federacyjnych usługi Azure Active Directory: dostawcy tożsamości innych firm, które mogą być używane tooimplement logowanie jednokrotne](https://msdn.microsoft.com/library/azure/jj679342.aspx) artykułu, aby uzyskać więcej informacji o hello firm logowania jednokrotnego, które zostały przetestowane przez Firmy Microsoft. Ta funkcja umożliwia organizacji tooimplement różne scenariusze B2B przy zachowaniu kontroli nad hello zarządzania tożsamościami i dostępem. Jednak podczas procesu projektowania hello B2B jest metoda uwierzytelniania hello toounderstand ważne, która będzie używana przez partnera hello i sprawdź, czy ta metoda jest obsługiwana przez platformę Azure. Obecnie są obsługiwane przez usługę Azure AD:

* Security Assertion Markup Language (SAML)
* OAuth
* Protokół Kerberos
* Tokeny
* Certyfikaty

> [!NOTE]
> Przeczytaj [protokoły uwierzytelniania usługi Active Directory Azure](https://msdn.microsoft.com/library/azure/dn151124.aspx) tooknow bardziej szczegółowe informacje dotyczące każdego protokołu i jego możliwości na platformie Azure.
>
>

Korzystanie z obsługi hello Azure AD, biznesowa urządzeń, które aplikacje mogą używać hello tego samego łatwe usług Mobile Services uwierzytelniania środowisko tooallow pracowników toosign w swoich aplikacjach mobilnych przy użyciu poświadczeń firmowych usługi Active Directory. W przypadku tej funkcji usługi Azure AD jest obsługiwany jako dostawcy tożsamości w usłudze Mobile Services razem z hello innych dostawców tożsamości już obsługujemy, (w tym Accounts firmy Microsoft, identyfikator usługi Facebook, Google identyfikator i identyfikator Twitter). Jeśli hello lokalnie aplikacje używa hello poświadczeń użytkownika znajduje się w firmie hello AD DS, hello dostęp z partnerami i użytkowników pochodzących z chmury hello powinny być przezroczyste. Zarządzanie użytkownika aplikacji sieci web too(cloud-based) kontroli dostępu warunkowego, interfejsu API sieci web firmy Microsoft usługi w chmurze, 3 aplikacji SaaS stron i aplikacji natywnych (klientów urządzeń przenośnych) i korzystnie hello zabezpieczeń, inspekcje, raportowanie wszystko w jednym miejsce. Jest jednak zalecane toovalidate to w środowiskach nieprodukcyjnych lub z ograniczoną ilością użytkowników.

> [!TIP]
> jest ważne toomention, że usługi Azure AD nie ma zasad grupy ma usług AD DS. W kolejności tooenforce zasady dla urządzeń należy rozwiązania do zarządzania urządzeniami przenośnymi takich jak [Microsoft Intune](https://technet.microsoft.com/library/jj676587.aspx).
>
>

Po uwierzytelnieniu użytkownika hello przy użyciu usługi Azure AD, ważne jest tooevaluate hello poziom dostępu, który hello użytkownika było z niej. Witaj poziom dostępu hello użytkownika będzie mieć wobec zasobu może się różnić, podczas usługi Azure AD można dodawać warstwy zabezpieczeń przez kontrolowanie dostęp do zasobów toosome, musi należy również należy pamiętać, że zasobów hello, się również może mieć własną listę kontroli dostępu oddzielnie, takich jak hello kontroli dostępu do plików znajdujących się na serwerze plików. na poniższej ilustracji Hello zawiera podsumowanie hello poziomy kontroli dostępu, który może mieć w scenariuszu hybrydowym:

![](./media/hybrid-id-design-considerations/accesscontrol.png)

Każdy interakcji hello diagramie pokazano na rysunku x reprezentuje jeden scenariusz kontroli dostępu może być objętych przez usługę Azure AD. Poniżej są opis poszczególnych scenariuszy:

1. Tooapplications dostępu warunkowego, które są hostowane lokalnie: zarejestrowane urządzenia można używać z zasadami dostępu dla aplikacji, które są skonfigurowane toouse usług AD FS w systemie Windows Server 2012 R2. Aby uzyskać więcej informacji na temat konfigurowania lokalnego dostępu warunkowego, zobacz [Setting up On-premises Conditional Access using Azure Active Directory Device Registration](active-directory-conditional-access.md) (Konfigurowanie lokalnego dostępu warunkowego przy użyciu usługi Rejestracja urządzeń w usłudze Azure Active Directory).

2. Kontrola dostępu toohello portalu Azure: Azure umożliwia również kontroli dostępu toohello portalu przy użyciu kontroli dostępu opartej na rolach (RBAC)). Ta metoda umożliwia hello firmy toorestrict hello ilość czynności, które osoby mogą wykonać hello portalu Azure. Za pomocą portalu toohello dostępu toocontrol RBAC, Administratorzy IT można delegować dostępu za pomocą hello następujących metod zarządzania dostępu:

* Przypisanie oparte na grupach roli: można przypisać dostępu grup tooAzure AD, które można synchronizować z lokalnej usługi Active Directory. Dzięki temu tooleverage hello dotychczasowych inwestycji wprowadzone w narzędzi i procesów do zarządzania grupami organizacji. Umożliwia także funkcji zarządzania grupy delegowanego hello Azure AD Premium.
* Wykorzystywanie wbudowane role na platformie Azure: można użyć trzech ról — tooensure właściciela, współautora i czytnika, że użytkownicy i grupy mają uprawnienia toodo tylko hello zadania muszą toodo swoich zadań.
* Tooresources szczegółowego dostępu: można przypisać toousers ról i grup dla określonej subskrypcji, grupy zasobów lub pojedynczych zasobów platformy Azure, takich jak witryny sieci Web lub bazy danych. W ten sposób można upewnij się, że użytkownicy mają dostęp do zasobów hello tooall, które są im potrzebne i nie tooresources dostępu, że nie potrzebują oni toomanage.

> [!NOTE]
> Jeśli są tworzenia aplikacji i chcesz kontroli dostępu hello toocustomize dla nich, jest również możliwe toouse Azure AD ról aplikacji do autoryzacji. Przejrzyj to [przykład aplikacji sieci Web-RoleClaims-DotNet](https://github.com/AzureADSamples/WebApp-RoleClaims-DotNet) na temat toobuild Twojego toouse aplikacji tej możliwości.
>
>

3. Dostęp warunkowy dla aplikacji usługi Office 365 w usłudze Microsoft Intune: Administratorzy IT mogą aprowizować dostępu warunkowego urządzeń zasady toosecure zasobów firmowych, podczas gdy na powitania sam czas dzięki czemu pracownicy przetwarzający informacje hello tooaccess zgodnym urządzeniom usługi. Aby uzyskać więcej informacji, zobacz artykuł [Conditional Access Device Policies for Office 365 services](active-directory-conditional-access-device-policies.md) (Zasady dostępu warunkowego urządzeń dla usług Office 365).

4. Dostęp warunkowy dla aplikacji Saas: [ta funkcja](http://blogs.technet.com/b/ad/archive/2015/06/25/azure-ad-conditional-access-preview-update-more-apps-and-blocking-access-for-users-not-at-work.aspx) pozwala reguły dostępu do poszczególnych aplikacji usługi Multi-Factor authentication tooconfigure i hello możliwości tooblock dostęp dla użytkowników nie znajduje się w zaufanej sieci. Możesz zastosować hello uwierzytelnianie wieloskładnikowe reguły tooall użytkowników, którzy są przypisane toohello aplikacji lub tylko dla użytkowników z określonych grup zabezpieczeń. Użytkownicy mogą zostać wyłączone z hello wymagania dotyczące uwierzytelniania wieloskładnikowego, jeśli uzyskują dostęp do aplikacji hello z adresu IP tego w elemencie hello sieci organizacji.

Ponieważ hello opcje kontroli dostępu używa wielowarstwowych podejście, porównanie te opcje nie są stosowane dla tego zadania. Upewnij się, że są wykorzystuje wszystkie opcje dostępne dla każdego scenariusza wymagającego toocontrol dostęp do tooyour zasobów.

## <a name="define-incident-response-options"></a>Zdefiniuj opcje odpowiedzi na zdarzenia
Usługi Azure AD może pomóc tooidentity IT potencjalne zagrożenia bezpieczeństwa w środowisku hello przez monitorowanie aktywności użytkownika, dział IT może korzystać z usługi Azure AD dostęp i możliwość toogain widoczność hello integralności i bezpieczeństwa w organizacji katalogu raportów użycia. Dzięki tym informacjom administrator IT może lepiej określają, gdzie może znajdować się możliwe zagrożenia bezpieczeństwa, tak aby ich odpowiednio zaplanować toomitigate te zagrożenia.  [Subskrypcję usługi Azure AD Premium](active-directory-get-started-premium.md) ma zestaw raporty dotyczące zabezpieczeń, które można włączyć IT tooobtain te informacje. [Raporty usługi Azure AD](active-directory-view-access-usage-reports.md) są podzielone, jak pokazano poniżej:

* **Raporty anomalii**: zawierają logowania czy znaleziono toobe nietypowe zdarzenia. Naszym celem jest toomake należy pamiętać o tych działań oraz pozwalające użytkownikowi toobe toomake możliwe określenie, czy jest podejrzane zdarzenia.
* **Zintegrowane raport aplikacji**: zapewnia wgląd w sposób aplikacji w chmurze są używane w organizacji. Usługa Azure Active Directory oferuje integrację z tysiącami aplikacji w chmurze.
* **Raporty o błędach**: wskazują błędy, które mogą wystąpić podczas inicjowania obsługi administracyjnej kont tooexternal aplikacji.
* **Raporty dotyczące użytkownika**: wyświetlać urządzenia/symbol w dane o aktywności dla określonego użytkownika.
* **Dzienniki aktywności**: zawiera rekord wszystkich zdarzeń inspekcji w ramach hello w ostatnich 24 godzinach, ostatnich 7 dni lub ostatnie 30 dni, a także grupy działania zmiany i działanie resetowania i rejestracji hasła.

> [!TIP]
> Innego raportu, który może również pomóc hello reagowania na zdarzenia zespół pracujący nad przypadkiem jest hello [użytkownik mający poświadczenia ujawnione](http://blogs.technet.com/b/ad/archive/2015/06/15/azure-active-directory-premium-reporting-now-detects-leaked-credentials.aspx) raportu.  Ten raport wyświetla dopasowań między te listy ujawnione poświadczenia i dzierżawy.
>
>

Inne ważne wbudowane raporty w usłudze Azure AD, używany podczas analizy odpowiedzi na zdarzenia i są:

* **Aktywność resetowania haseł**: udostępnianie Witaj, Administratorze wgląd w sposób aktywnie resetowania hasła jest używana w organizacji hello.
* **Aktywność rejestracji resetowania haseł**: udostępnia szczegółowe informacje, do których użytkownicy zarejestrowali ich metod w celu resetowania haseł i metod, które zostały wybrane.
* **Grupa działań**: zawiera historię zmian toohello grupy (ex: użytkowników dodawanych lub usuwanych) który zostały zainicjowane w hello panelu dostępu.

Ponadto toohello podstawowe możliwości raportowania dostępnych w programie Azure AD Premium, które można wykorzystać w procesie dochodzenia reagowania na zdarzenia, dział IT może również wykorzystać raport dotyczący inspekcji tooobtain informacje takie jak:

* Zmiany w członkostwo roli (przykład: użytkownik dodał rolę administratora tooGlobal)
* Poświadczenia aktualizacji (przykład: zmiany hasła)
* Zarządzanie domenami (przykład: weryfikowanie domeny niestandardowej usuwania domeny)
* Dodawanie lub usuwanie aplikacji
* Zarządzanie użytkownikami (przykład: Dodawanie, usuwanie, aktualizowanie użytkownika)
* Dodawanie lub usuwanie licencji

Ponieważ opcje hello odpowiedzi na zdarzenia używa wielowarstwowych podejście, porównanie te opcje nie są stosowane dla tego zadania. Upewnij się, że są wykorzystuje wszystkie opcje dostępne dla każdego scenariusza wymagającego toouse możliwości raportowania usługi Azure AD jako część procesu odpowiedzi na zdarzenia w firmie.

## <a name="next-steps"></a>Następne kroki
[Określić zadań zarządzania tożsamości hybrydowej](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)

## <a name="see-also"></a>Zobacz też
[Omówienie zagadnień dotyczących projektowania](active-directory-hybrid-identity-design-considerations-overview.md)
