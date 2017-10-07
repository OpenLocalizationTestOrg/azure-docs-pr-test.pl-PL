---
title: "możliwości techniczne zabezpieczeń aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat przetwarzania danych usług w chmurze zawierających szeroką gamę wystąpienia obliczeniowe i usług, które można skalować w górę i w dół automatycznie toomeet hello potrzeb aplikacji lub przedsiębiorstwa."
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/26/2017
ms.author: TomSh
ms.openlocfilehash: a0ef17883be54dab4cb6b597204f3197dc05c28c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-technical-capabilities"></a>Możliwości techniczne zabezpieczeń platformy Azure

informacje o tooassist aktualnych i potencjalnych klientów platformy Azure i wykorzystywać hello różnych funkcjach zabezpieczeń dostępnych w i otaczającego je hello platformy Azure, firma Microsoft opracowała serii oficjalne dokumenty, omówienie zabezpieczeń, najlepsze rozwiązania i Listy kontrolne. Tematy Hello zakresu pod względem szerokości i głębokość i są okresowo aktualizowane. Ten dokument jest częścią tej serii, zgodnie z opisem w poniższej sekcji abstrakcyjny hello. Więcej informacji na temat tej serii zabezpieczeń Azure można znaleźć pod adresem (URL).

## <a name="azure-platform"></a>Platforma Azure

[Microsoft Azure](https://azure.microsoft.com/overview/what-is-azure/) platformy w chmurze składa się z infrastrukturą i usług aplikacji, z usług zintegrowanych danych i zaawansowane metody analizy i narzędzia deweloperskie i usług, obsługiwana w danych firmy Microsoft w chmurze publicznej centrów. Klienci używać platformy Azure dla wiele różnych możliwości i scenariusze z podstawowych obliczeniowych, sieci i magazynu, sieci web i toomobile aplikacji usług, toofull scenariusze chmury, takich jak Internet rzeczy i może być używany z technologiami typu open source i wdrożony jako hybrydowe w chmurze lub umieszczony w obrębie centrum danych klienta. Platforma Azure udostępnia technologii w chmurze jako bloków konstrukcyjnych toohelp firmy ograniczenia kosztów, innowacji szybko i aktywne zarządzanie systemami. Podczas tworzenia lub migracji dostawcy chmury tooa zasoby IT są zależne tooprotect możliwości organizacji w aplikacji i danych za pomocą usługi hello i formanty hello zapewniają bezpieczeństwo hello toomanage zasobów opartych na chmurze.

Microsoft Azure to hello tylko chmury obliczeniowej dostawcy, który zapewnia platformę aplikacji bezpiecznego, spójne i infrastruktury jako usługi dla zespołów toowork w ramach ich skillsets inną chmurę i poziomy złożoność projektu, zintegrowanych danych usługi i analitycznych odkrywanie analizy danych wszędzie tam, gdzie istnieje, przez firmę Microsoft, jak i platform firmy Microsoft, otwórz struktur i narzędzi, zapewniając wyboru do integracji z lokalnymi również wdrażanie usług w chmurze Azure w chmurze lokalnych centrów danych. W ramach hello zaufane firmy Microsoft w chmurze klienci polegać na platformie Azure dla branży zabezpieczeń, zgodności, prywatności i niezawodność sieci przeważająca hello osób, partnerzy i organizacji toosupport procesy w chmurze hello.

Microsoft Azure możesz:

- Przyspieszenie innowacji hello chmury.

- Decyzje biznesowe zasilania i aplikacji z informacjami.

- Za darmo tworzenie i wdrażanie dowolnego miejsca.

- Ochrona firmy.

## <a name="scope"></a>Zakres

Witaj centralny punkt tego dokumentu dotyczy funkcji zabezpieczeń i funkcji pomocniczych — podstawowe składniki Microsoft Azure, czyli [magazyn Microsoft Azure](https://docs.microsoft.com/azure/storage/storage-introduction), [baz danych SQL Azure Microsoft](https://docs.microsoft.com/azure/sql-database/), [Modelu maszyny wirtualnej Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/  )i narzędzi hello, jak i zarządzać nim wszystkie infrastruktury. Ten dokument skupić się na tooyou dostępne technicznych Microsoft Azure jako klienci toofulfil ich rolę w ochronie hello zabezpieczenia i prywatność ich danych.

opis tego modelu udostępnionego odpowiedzialność znaczenie Hello jest istotne dla klientów, którzy są przenoszone toohello chmury. Dostawcy chmury oferują znaczące korzyści dla zabezpieczeń i zgodności, ale te zalety zwalnia powitania klienta z ochrony swoich użytkowników, aplikacji i ofert usług.

Rozwiązania IaaS powitania klienta jest odpowiedzialny lub odpowiada udostępnionego do zabezpieczania i zarządzania nimi hello systemu operacyjnego, konfigurację sieci, aplikacji, tożsamości, klientów i danych.  Tworzenie rozwiązań PaaS w wdrożenia IaaS, hello klient nadal odpowiada lub ma wspólnej odpowiedzialności za zabezpieczania i zarządzanie aplikacjami, tożsamości, klientów i danych. Rozwiązania SaaS, Nonetheless, klient hello nadal toobe odpowiedzialny. One zapewnić, że dane są poprawnie klasyfikowane, i mają toomanage odpowiedzialność ich użytkowników i urządzeń punktu końcowego.

Ten dokument nie daje szczegółowy pokrycia dowolnego hello powiązane składniki platformy Microsoft Azure, takich jak witryny sieci Web platformy Azure, Azure Active Directory, HDInsight, Media Services i innych usług, które są warstwie nad hello podstawowe składniki. Mimo że podano minimalny poziom informacje ogólne, czytników uznaje, że znasz podstawowe pojęcia Azure zgodnie z opisem w inne odwołania obsługiwane przez firmę Microsoft i zawarte w łączy w tym oficjalnym dokumencie.


## <a name="available-security-technical-capabilities-toofulfil-user-customer-responsibility---big-picture"></a>Odpowiedzialność użytkownika (klienta) zabezpieczeń dostępne możliwości techniczne toofulfil - duży obraz

Microsoft Azure oferuje usługi, które mogą pomóc klientom spełnia hello zabezpieczeń, prywatności i zgodności potrzeb. Witaj, stosując obraz, który pomaga opisano różne usługi platformy Azure dostępne dla użytkowników toobuild infrastruktury aplikacji bezpieczne i zgodne oparte na standardach.

![Techniczne obraz Big możliwości dostępnych zabezpieczeń](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig1.png)

## <a name="manage-and-control-identity-and-user-access-protect"></a>Zarządzanie i sterowanie tożsamości i dostęp użytkownika (Chroń)

Azure pomaga chronić biznesowych i danych osobowych przez włączenie możesz toomanage tożsamości użytkownika i poświadczeń i kontroli dostępu.

### <a name="azure-active-directory"></a>Usługa Azure active directory

Pomocy firmy Microsoft tożsamościami i dostępem zarządzania rozwiązań IT ochronę tooapplications dostępu i zasobów na powitania firmowym centrum danych i w chmurze hello włączenie dodatkowe poziomy sprawdzania poprawności, takich jak uwierzytelnianie wieloskładnikowe i warunkowe zasady dostępu. Monitorowania podejrzanych działań przez zaawansowane zabezpieczenia raportowania, inspekcji i alerty, pomaga ograniczyć potencjalne problemy. [Azure Active Directory Premium](https://docs.microsoft.com/azure/active-directory/active-directory-editions) zapewnia toothousands znak pojedynczego aplikacji w chmurze (SaaS) i uruchom lokalnie aplikacje tooweb dostępu.

Korzyści w zakresie zabezpieczeń dla usługi Azure Active Directory (AD) obejmują możliwość hello:

- Utwórz i Zarządzaj jednej tożsamości dla każdego użytkownika w przedsiębiorstwie hybrydowego Synchronizacja użytkowników, grup i urządzeń.

- Podaj dostępu rejestracji jednokrotnej tooyour aplikacji, w tym tysięcy wstępnie zintegrowanych aplikacji SaaS.

- Włącz zabezpieczenia dostępu do aplikacji, wymuszając uwierzytelnianie wieloskładnikowe opartych na regułach, które zarówno lokalnie i aplikacji w chmurze.

- Lokalne tooon bezpieczny dostęp zdalny należy sieci web aplikacji za pośrednictwem serwera Proxy aplikacji usługi Azure AD.

[Portal usługi Azure active directory](http://aad.portal.azure.com/) jest dostępna części portalu azure. Z tego pulpitu nawigacyjnego zapoznaj się z omówieniem stanu hello organizacji i Poznaj łatwe zarządzanie hello katalogu, użytkowników lub dostęp do aplikacji.

![Usługa Azure active directory](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig2.png)

Poniżej są podstawowe możliwości zarządzania tożsamość platformy Azure:

- Logowanie jednokrotne

- Uwierzytelnianie wieloskładnikowe

- Monitorowanie zabezpieczeń, alertów i raportów na podstawie learning maszyny

- Zarządzanie tożsamościami i dostępem klientów

- Rejestracja urządzenia

- Zarządzanie tożsamościami uprzywilejowanymi

- Ochrona tożsamości

#### <a name="single-sign-on"></a>Logowanie jednokrotne

[Logowanie jednokrotne (SSO)](https://azure.microsoft.com/documentation/videos/overview-of-single-sign-on/) oznacza, że jest w stanie tooaccess wszystkich aplikacji hello i zasobów potrzebnych firm toodo, logując się tylko raz przy użyciu jednego konta użytkownika. Po zalogowaniu może uzyskiwać dostęp do wszystkich aplikacji hello należy nie jest wymagane tooauthenticate (na przykład wpisz hasło) po raz drugi.

W wielu organizacjach opierają się na oprogramowania jako aplikacje usługi (SaaS), takich jak Office 365, pole i Salesforce na produktywność użytkownika końcowego. W przeszłości tooindividually potrzebne personelu IT tworzenie i aktualizowanie kont użytkowników w każdej aplikacji SaaS, a użytkownicy mieli tooremember hasła dla każdej aplikacji SaaS.

[Usługi Azure AD rozszerza w lokalnej usłudze Active Directory w chmurze hello](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis), włączanie toouse użytkownikom ich podstawowej organizacji konta logowania tylko toonot tootheir urządzeń przyłączonych do domeny i zasobów firmy, ale również wszystkich hello sieci web i aplikacji SaaS potrzebne do ich pracy.

Nie tylko użytkownicy bez toomanage wiele zestawów nazwy użytkowników i hasła, dostęp do aplikacji mogą być automatycznie udostępnione lub cofnąć elastycznie na podstawie grupy organizacyjne i ich stan jako pracownika. [Usługi Azure AD wprowadza formanty Zarządzanie zabezpieczeniami i dostępem](https://docs.microsoft.com/azure/active-directory/active-directory-sso-integrate-saas-apps) pozwalające toocentrally zarządzanie dostępem użytkowników do aplikacji SaaS.

#### <a name="multi-factor-authentication"></a>Uwierzytelnianie wieloskładnikowe

[Usługa Azure Multi-Factor authentication (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication) jest metoda uwierzytelniania, która wymaga użycia hello więcej niż jednej metody weryfikacji i dodaje kluczową drugą warstwę logowania toouser zabezpieczeń i transakcji. [MFA ułatwia zabezpieczenie](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-how-it-works) dostęp do toodata i aplikacji, spełniając zapotrzebowanie na prosty proces logowania. Zapewnia silne uwierzytelnianie za pomocą różnych opcji weryfikacji — połączenie telefoniczne, wiadomość tekstowa lub aplikacja mobilna weryfikacji lub powiadamiania o kodzie i innych firm tokenów OAuth.

#### <a name="security-monitoring-alerts-and-machine-learning-based-reports"></a>Monitorowanie zabezpieczeń, alertów i raportów na podstawie learning maszyny

Monitorowanie zabezpieczeń i alertów i machine learning raportów na podstawie identyfikujące niespójne wzorce dostępu ułatwia ochronę firmy. Umożliwia dostęp do usługi Azure Active Directory i użycia raporty toogain widoczność hello integralności i bezpieczeństwa w katalogu organizacji. Dzięki tym informacjom administratora katalogu można lepiej określić, gdzie może znajdować się możliwe zagrożenia bezpieczeństwa, tak aby ich odpowiednio zaplanować toomitigate te zagrożenia.

Witaj klasycznego portalu Azure lub za pośrednictwem [portalu usługi Azure Active directory](http://aad.portal.azure.com/), [raporty](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) są podzielone na powitania następujące sposoby:

- Raporty anomalii — zawierają logowania czy znaleziono toobe nietypowe zdarzenia. Naszym celem jest toomake należy pamiętać o tych działań oraz pozwalające użytkownikowi toobe stanie toodecide o tym, czy jest podejrzane zdarzenia.

- Raporty aplikacji zintegrowanego — wgląd w sposób aplikacji w chmurze są używane w organizacji. Usługa Azure Active Directory oferuje integrację z tysiącami aplikacji w chmurze.

- Raporty o błędach — wskazują błędy, które mogą wystąpić podczas inicjowania obsługi administracyjnej kont tooexternal aplikacji.

- Raporty dotyczące użytkownika — wyświetlać urządzenia/symbol w dane o aktywności dla określonego użytkownika.

- Dzienniki aktywności — zawiera rekord wszystkich zdarzeń inspekcji w ramach hello ostatnich 24 godzinach, ostatnie 7 dni, lub ostatnich 30 dni i grupy działania zmiany oraz działania resetowania i rejestracji hasła.

#### <a name="consumer-identity-and-access-management"></a>Zarządzanie tożsamościami i dostępem klientów

[Usługa Azure Active Directory B2C](https://azure.microsoft.com/services/active-directory-b2c/) jest tożsamość wysokiej dostępności, globalnych, zarządzanie usługą w aplikacjach użytkownika która może obsłużyć toohundreds milionów tożsamości. Można ją łatwo integrować z platformami mobilnymi i platformami sieci Web. Użytkownicy mogą logować tooall aplikacji za pomocą środowiska można dostosować przy użyciu istniejących kont społecznościowych lub tworząc nowe poświadczenia.

W hello przeszłości deweloperzy aplikacji, którzy chciał zbyt[i zalogują się konsumentów](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview) w swoich aplikacjach, musieli napisać własny kod. I musieli korzystać z lokalnych baz danych lub systemów toostore nazwy użytkowników i hasła. Usługa Azure Active Directory B2C oferuje organizacji lepszą sposób toointegrate zarządzania tożsamością użytkowników do aplikacji za pomocą hello bezpiecznej, spełniającej standardy platformy i dużego zestawu rozszerzalnych zasad.

Gdy używasz usługi Azure Active Directory B2C użytkownicy mogą rejestrować dla aplikacji, przy użyciu istniejących kont społecznościowych (Facebook, Google, Amazon, LinkedIn) lub tworząc nowe poświadczenia (adres e-mail i hasło lub nazwa użytkownika i hasło).

Rejestracja urządzenia

[Rejestracja urządzenia w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) podstawę hello jest oparta na urządzeniach [dostępu warunkowego](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-device-registration-overview) scenariuszy. Po zarejestrowaniu urządzenia rejestracji urządzeń usługi Azure Active Directory zapewnia hello urządzenia przy użyciu tożsamości, który jest używany tooauthenticate hello urządzenia po zalogowaniu użytkownika hello. urządzenie Hello uwierzytelniony i atrybuty hello hello urządzenia, można następnie tooenforce używane zasady dostępu warunkowego dla aplikacji, które znajdują się w chmurze hello i lokalnych.

W połączeniu z [zarządzania urządzeniami przenośnymi (MDM)](https://www.microsoft.com/itshowcase/Article/Content/588/Mobile-device-management-at-Microsoft) rozwiązania, takie jak usługi Intune, atrybuty urządzenia hello w usłudze Azure Active Directory są aktualizowane przy użyciu dodatkowych informacji o urządzeniu hello. Dzięki temu można toocreate zasady dostępu warunkowego, które wymuszają dostęp z urządzeń toomeet standardy zabezpieczeń i zgodności.

#### <a name="privileged-identity-management"></a>Zarządzanie tożsamościami uprzywilejowanymi

[Azure Active Directory (AD) Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure) umożliwia zarządzanie, sterowanie i monitorowanie tożsamości uprzywilejowanych oraz dostęp tooresources w usłudze Azure AD, jak również inne usługi online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune.

Czasami użytkownicy muszą toocarry operacje uprzywilejowane w zasobów platformy Azure lub usługi Office 365 lub innych aplikacji SaaS. Często oznacza to, organizacje mają toogive ich stałe uprzywilejowanego dostępu w usłudze Azure AD. Jest to zagrożenie bezpieczeństwa rosnącym zasobów hostowanych w chmurze, ponieważ organizacje wystarczająco nie można monitorować, co robią tych użytkowników, używając swoich uprawnień administratora. Ponadto w przypadku złamania zabezpieczeń konta użytkownika z dostępem uprzywilejowanym tego naruszenia co może mieć wpływ na ich ogólne bezpieczeństwo chmury. Azure AD Privileged Identity Management pomaga tooresolve to ryzyko.

Azure AD Privileged Identity Management umożliwia:

- Zobacz użytkowników, którzy są administratorami usługi Azure AD

- Włącz na żądanie "just in time" tooMicrosoft dostępu administracyjnego usług Online, takich jak Office 365 i Intune

- Uzyskaj raporty dotyczące historii dostępu administratora i zmian w przypisaniach administratora

- Uzyskiwanie alertów dotyczących ról uprzywilejowanych tooa dostępu

#### <a name="identity-protection"></a>Ochrona tożsamości

[Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection) to usługa zabezpieczeń, która udostępnia skonsolidowany wgląd w zdarzenia o podwyższonym ryzyku i potencjalnych luk w zabezpieczeniach wpływających na tożsamości organizacji. Identity Protection korzysta z możliwości wykrywania anomalii istniejących Azure usługi Active Directory (dostępne za pośrednictwem usługi Azure AD nietypowe działanie raportów) i wprowadza nowe typy zdarzeń ryzyka, które można wykrywania anomalii w czasie rzeczywistym.

## <a name="secured-resource-access-in-azure"></a>Dostęp do zabezpieczonych zasobów na platformie Azure

Kontrola dostępu na platformie Azure rozpoczyna się z punktu widzenia rozliczeń. Witaj właściciela konta platformy Azure, dostęp, przechodząc na stronę hello [Centrum konta platformy Azure](https://account.windowsazure.com/subscriptions), jest hello konta administratora (AA). Subskrypcje są kontener rozliczeń, ale również działają jako granic zabezpieczeń: Każda subskrypcja ma usługi administratora kto dodawania, usuwania i modyfikowania zasobów platformy Azure w ramach tej subskrypcji przy użyciu hello [klasycznego portalu Azure](https://manage.windowsazure.com/). SA domyślne Hello nowej subskrypcji jest hello AA, ale hello AA można zmienić hello SA w hello Centrum konta platformy Azure.

![Dostęp do zabezpieczonych zasobów na platformie Azure](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig3.png)

Subskrypcje mają również skojarzenie z katalogiem. katalog Hello definiuje zestaw użytkowników. Mogą to być użytkownicy z hello pracy lub nauki, który utworzył katalog hello, lub mogą być użytkownicy zewnętrzni (to znaczy Accounts firmy Microsoft). Subskrypcje są dostępne dla podzbioru użytkowników katalogu, na których został przypisany jako usługi administratora lub administratora współpracującego (CA); Witaj tylko wyjątek to, że dla starszych powodów Accounts firmy Microsoft (dawniej identyfikator Windows Live ID) można przypisać jako administratora systemu lub urzędu certyfikacji nie jest obecny w katalogu hello.

Nastawionych zabezpieczeń skoncentrować się nadanie uprawnień dokładne hello potrzebnych im pracowników. Za dużo uprawnienia mogą uwidaczniać tooattackers konta. Za mało uprawnienia oznacza, że pracownicy nie można pobrać ich pracować wydajnie. [Azure opartej na rolach kontroli dostępu (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is) pomaga rozwiązać ten problem, oferując precyzyjne zarządzanie dostępem dla platformy Azure.

![Dostęp do zabezpieczonych zasobów ](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig4.png)

Przy użyciu funkcji RBAC, można rozdzielenie obowiązków w obrębie organizacji i udzielić tylko hello ilość toousers dostępu do potrzebnych tooperform swoich zadań. Zamiast nadanie każdy nieograniczonych uprawnień w Twojej subskrypcji platformy Azure lub zasobów, można zezwolić tylko pewne akcje. Na przykład użyj RBAC toolet jednego pracownika zarządzania maszynami wirtualnymi w ramach subskrypcji, podczas gdy inny można zarządzać baz danych SQL w ramach hello takie same subskrypcji.

![Dostęp do zasobów zabezpieczonych w Azure(RBAC)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig5.png)

## <a name="azure-data-security-and-encryption-protect"></a>Bezpieczeństwo danych platformy Azure i szyfrowania (Ochrona)

Jeden z ochrony toodata klucze hello w chmurze hello jest księgowanie hello możliwe stany, w których może wystąpić danych oraz kontrolki są dostępne dla tego stanu. Bezpieczeństwo danych platformy Azure i szyfrowania hello zaleceniach się wokół hello następujące stany danych.

- W pozostałych: W tym wszystkie informacje, które typy, statycznie występujących na nośnik fizyczny, kontenerów i obiektów magazynu można go magnetyczne lub optyczne dysku.

- Podczas przesyłania: Podczas transferu danych między składnikami, lokalizacji lub programy, takie jak sieci hello przez usługi service bus (z toocloud lokalnie i na odwrót, łącznie z połączeń hybrydowych, takich jak usługi ExpressRoute), lub w trakcie operacji We/Wy proces, jego jest traktować jako w ruchu.

### <a name="encryption--rest"></a>Szyfrowanie @ rest

tooachieve szyfrowanie przechowywanych hello następującego:

Obsługuje co najmniej jeden z hello zalecane modeli szyfrowania szczegółowo w hello następujące dane tooencrypt tabeli.

| Modele szyfrowania |  |  |  |
| ----------------  | ----------------- | ----------------- | --------------- |
| Szyfrowanie serwera | Szyfrowanie serwera | Szyfrowanie serwera | Szyfrowanie klienta
| Przy użyciu usługi zarządzane klucze szyfrowania po stronie serwera | W usłudze Azure Key Vault za pomocą Customer-Managed klucze szyfrowania po stronie serwera | Przy użyciu lokalnego klienta zarządzane klucze szyfrowania po stronie serwera |
| • Azure dostawcy zasobów operacji hello szyfrowania i odszyfrowywania <br> • Firma Microsoft zarządza hello kluczy <br>• Chmury pełna funkcjonalność | • Azure dostawcy zasobów operacji hello szyfrowania i odszyfrowywania<br>• Klient kontroluje klucze za pomocą usługi Azure Key Vault<br>• Chmury pełna funkcjonalność | • Azure dostawcy zasobów operacji hello szyfrowania i odszyfrowywania <br>• Klient kontroluje klucze lokalnego <br> • Chmury pełna funkcjonalność| • Usług azure nie widzi odszyfrowane dane <br>• Klienci przechowywać klucze lokalnie lub w innych secure magazynów. Klucze nie są dostępne tooAzure usług <br>• Zmniejszona funkcji chmury|

### <a name="enabling-encryption-at-rest"></a>Włączenie szyfrowania magazynowane

**Zidentyfikuj wszystkie lokalizacje magazyny danych**

Celem Hello szyfrowanie magazynowanych jest tooencrypt wszystkie dane. Dzięki temu eliminuje możliwość hello Brak ważnych danych lub wszystkich lokalizacji utrwalonych. Wyświetla wszystkie dane przechowywane przez aplikację. 

> [!Note] 
> Nie tylko "application data" lub "dane osobowe", ale żadnych danych związanych z tym tooapplication konta metadanych (mapowania subskrypcji, informacje kontraktu danych osobowych).

Należy wziąć pod uwagę, jakie są przechowywane są przy użyciu toostore danych. Na przykład:

- Magazynu zewnętrznego (na przykład SQL Azure, bazie danych dokumentów, HDInsights, Data Lake, itp.)

- Magazyn tymczasowy (żadnych lokalnej pamięci podręcznej zawierającego dane dzierżawcy)

- W pamięci podręcznej (mogą znajdować się w pliku stronicowania hello.)

### <a name="leverage-hello-existing-encryption-at-rest-support-in-azure"></a>Korzystać z szyfrowania istniejących hello w witrynie pomocy technicznej rest na platformie Azure

Dla każdego używanego sklepu wykorzystać hello istniejących szyfrowania w witrynie pomocy technicznej Rest.

- Magazyn Azure: Zobacz [szyfrowanie usługi Magazyn Azure dla danych magazynowanych](https://docs.microsoft.com/azure/storage/storage-service-encryption),

- Usługi SQL Azure: Zobacz [przezroczystego szyfrowania danych (funkcji TDE), zawsze zaszyfrowane programu SQL](https://msdn.microsoft.com/library/mt163865.aspx)

- Na dysku magazynu maszyny Wirtualnej & lokalny ([szyfrowania dysków Azure](https://docs.microsoft.com/azure/security/azure-security-disk-encryption))

Dla maszyny Wirtualnej i lokalny magazyn dyskowy Użyj szyfrowania dysków Azure w przypadku, gdy obsługiwane:

IaaS

Usługi z maszyn wirtualnych IaaS (Windows lub Linux) powinny używać [szyfrowania dysków Azure](https://microsoft.sharepoint.com/teams/AzureSecurityCompliance/Security/SitePages/Azure%20Disk%20Encryption.aspx) tooencrypt woluminy zawierające dane klienta.

PaaS w wersji 2

Usługi uruchomione na PaaS v2 korzystania z usługi sieć szkieletowa można używać szyfrowania dysków Azure dla zestawu skalowania maszyn wirtualnych [VMSS] tooencrypt ich maszyny wirtualne w wersji 2 PaaS.

PaaS v1

Szyfrowanie dysków Azure aktualnie nie jest obsługiwane na PaaS v1. W związku z tym należy użyć aplikacji poziom szyfrowania tooencrypt istniejących danych w stanie spoczynku.  Obejmuje, ale nie jest ograniczona do danych aplikacji, plików tymczasowych, dzienniki i zrzuty awaryjne.

Większość usług mają podejmować próbę tooleverage hello szyfrowania dostawcy zasobów magazynu. Niektóre usługi mają toodo jawne szyfrowania, na przykład żadnego utrwalonego materiału klucza (certyfikaty, głównego / wzorca kluczy) musi być przechowywany w magazynie kluczy.

Jeśli szyfrowanie po stronie serwera za pomocą kluczy zarządzany przez klienta musi toobe sposób powitania klienta tooget hello klucza toous. Witaj obsługiwane i zalecane toodo sposób dzięki integracji z magazynu kluczy Azure (AKV). W takim przypadku klientów, można dodać i zarządzać swoimi kluczami w usłudze Azure Key Vault. Klienta można dowiedzieć się jak toouse AKV za pośrednictwem [wprowadzenie do korzystania z usługi Key Vault](http://go.microsoft.com/fwlink/?linkid=521402).

toointegrate z usługi Azure Key Vault, należy dodać kodu toorequest klucza z AKV, gdy są potrzebne do odszyfrowywania.

- Zobacz [usługi Azure Key Vault — krok po kroku](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/) informacji na temat toointegrate z AKV.

Obsługuje klientów zarządzanych kluczy, należy najpierw tooprovide UX na powitania klienta toospecify które toouse magazynu kluczy (lub identyfikator URI magazynu kluczy).

Jak szyfrowanie magazynowanych obejmuje hello szyfrowania danych hosta, infrastruktury i dzierżawcy, utraty hello kluczy hello ukończenia lub niepowodzenia toosystem złośliwych działań może oznaczać wszystkich hello zaszyfrowane dane zostaną utracone. W związku z tym jest krytyczny, że szyfrowania rozwiązania Rest ma odzyskiwania po awarii kompleksowe wątek błędów toosystem odporne i złośliwych działań.

Usług, które implementuje szyfrowanie magazynowanych zwykle są nadal podatne toohello kluczy szyfrowania lub danych pozostaje w postaci niezaszyfrowanej na powitania dysku hosta (na przykład w hello pliku strony hello hosta systemu operacyjnego.) W związku z tym usługi należy zapewnić, że hello woluminu hosta dla swoich usług są szyfrowane. toofacilitate tego zespołu obliczeń włączył hello wdrożenia szyfrowania hosta, który używa [funkcji Bitlocker](https://technet.microsoft.com/library/dn306081.aspx) NKP i rozszerzenia toohello DCM agent i usługi tooencrypt hello woluminu hosta.

Większość usług są implementowane na maszynach wirtualnych Azure standard. Tych usług należy uzyskać [szyfrowania hosta](https://docs.microsoft.com/azure/security/azure-security-disk-encryption) automatycznie podczas obliczeń włączy ją. Dla usług uruchomionych w obliczeń zarządzane klastry hosta szyfrowanie jest włączane automatycznie, zgodnie z systemu Windows Server 2016 jest wdrażana.

### <a name="encryption-in-transit"></a>Szyfrowanie podczas przesyłania danych

Ochrona danych podczas przesyłania powinien być integralną część strategii ochrony danych. Ponieważ dane są przenoszone i z powrotem w wielu lokalizacjach, ogólne zalecenie hello jest zawsze używaj danych tooexchange protokołów SSL/TLS w różnych lokalizacjach. W niektórych sytuacjach może być tooisolate hello całej komunikacji kanału między lokalnymi i w chmurze infrastruktury przy użyciu wirtualnej sieci prywatnej (VPN).

Przenoszenie między lokalną infrastrukturą i Azure danych należy rozważyć odpowiednie zabezpieczenia, takie jak HTTPS lub sieci VPN.

Dla organizacji, które wymagają dostępu toosecure z wielu stacjach roboczych znajdujących się lokalnie tooAzure, użyj [Azure VPN lokacja lokacja](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-site-to-site-create).

Dla organizacji, które wymagają dostępu toosecure z jednej stacji roboczej znajdujących się lokalnie tooAzure, użyj [punkt-lokacja sieci VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-point-to-site-create).

Większych zestawów danych można przenieść za pośrednictwem dedykowanej o dużej szybkości łącza sieci WAN takich jak [ExpressRoute](https://azure.microsoft.com/services/expressroute/). Jeśli wybierzesz toouse ExpressRoute, można również szyfrowanie danych hello przy użyciu poziomu aplikacji hello [SSL/TLS](https://support.microsoft.com/kb/257591) lub innymi protokołami zapewnia dodatkową ochronę.

Jeśli użytkownik korzysta z usługi Azure Storage za pomocą portalu Azure hello, wszystkich transakcji jest realizowana za pośrednictwem protokołu HTTPS. [Interfejs API REST magazynu](https://msdn.microsoft.com/library/azure/dd179355.aspx) za pośrednictwem protokołu HTTPS może być również używane toointeract z [usługi Azure Storage](https://azure.microsoft.com/services/storage/) i [bazy danych SQL Azure](https://azure.microsoft.com/services/sql-database/).

Organizacje, które nie są przesyłane dane tooprotect są bardziej narażony na [ataków man-in--middle](https://technet.microsoft.com/library/gg195821.aspx), [podsłuchiwaniu](https://technet.microsoft.com/library/gg195641.aspx)i przejęcie kontroli sesji. Tego rodzaju ataki może być pierwszym krokiem hello w uzyskiwaniu dostępu do danych tooconfidential.

Możesz można dowiedzieć się więcej o sieci VPN platformy Azure opcja od przeczytania artykułu hello [planowania i projektowania dla bramy sieci VPN](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-plan-design).

### <a name="enforce-file-level-data-encryption"></a>Wymuszanie szyfrowania danych na poziomie plików

[Usługa Azure RMS](https://technet.microsoft.com/library/jj585026.aspx) toohelp zasad szyfrowania, tożsamości i autoryzacji używa Zabezpieczanie plików i wiadomości e-mail. Usługa Azure RMS działa na wielu urządzeniach — telefonach, tablety i komputery, aby chronić w obrębie organizacji i poza organizacją. Ta funkcja jest możliwa, ponieważ usługa Azure RMS dodaje poziom ochrony, który pozostaje hello danych, nawet wtedy, gdy opuszczą teren organizacji.

Gdy używasz usługi Azure RMS tooprotect plików za pomocą branżowego standardu kryptografii pełnej obsługi [FIPS 140-2](http://csrc.nist.gov/groups/STM/cmvp/standards.html). Podczas ochrony danych należy korzystać z usługi Azure RMS, masz hello gwarantują, że ochrona powitalnych pozostanie z plikiem hello, nawet jeśli jest skopiowany toostorage, który nie jest pod kontrolą hello IT, takich jak Usługa magazynu w chmurze. Hello sam występuje w przypadku plików udostępnianych za pośrednictwem poczty e-mail, hello plik jest chroniony jako załącznik tooan wiadomość e-mail, jak z instrukcjami tooopen hello chronionego załącznika.
Podczas planowania wdrożenia usługi Azure RMS firma Microsoft zaleca hello następujące czynności:

- Zainstaluj hello [aplikacji RMS sharing](https://technet.microsoft.com/library/dn339006.aspx). Ta aplikacja jest zintegrowany z pakietu Office aplikacji przez zainstalowanie pakietu Office dodatek tak, aby użytkownikom ochronę plików bezpośrednio.

- Skonfiguruj aplikacje i toosupport usług Azure RMS

- Utwórz [szablonów niestandardowych](https://technet.microsoft.com/library/dn642472.aspx) która odzwierciedla wymagania firmy. Na przykład: szablon do górnej poufne dane, które powinny być stosowane w wszystkich ściśle tajne związane z wiadomości e-mail.

Organizacje, które są słabe na [klasyfikacji danych](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) i ochrona plików może być bardziej narażony wycieku toodata. Bez ochrony prawidłowego pliku organizacji nie będą mogli tooobtain informacje biznesowe, monitorowanie nadużyć należy również uniemożliwić toofiles nieautoryzowanym dostępem.

> [!Note]
> Dodatkowe informacje na temat usługi Azure RMS od przeczytania artykułu hello [wprowadzenie do korzystania z usługi Azure Rights Management](https://technet.microsoft.com/library/jj585016.aspx).

## <a name="secure-your-application-protect"></a>Zabezpieczanie aplikacji (Ochrona)
Azure jest odpowiedzialny za bezpieczeństwo infrastruktury hello i platformy, która aplikacja działa na, ale jest toosecure Twojego odpowiedzialność samej aplikacji. Innymi słowy, należy toodevelop, wdrażania i zarządzania kod aplikacji i zawartości w bezpieczny sposób. W przeciwnym razie z kodu aplikacji lub zawartość nadal można toothreats narażone.

### <a name="web-application-firewall-waf"></a>Zapora aplikacji sieci Web
[Zapora aplikacji sieci Web (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) jest funkcją [brama aplikacji w](https://docs.microsoft.com/azure/application-gateway/application-gateway-introduction) zapewnia scentralizowane ochrony aplikacji sieci web z najczęściej luki w zabezpieczeniach i luk w zabezpieczeniach.

Zapora aplikacji sieci Web jest na podstawie reguł z hello [zestawów reguł core OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 lub 2.2.9. Aplikacje sieci Web coraz częściej stają się obiektami złośliwych ataków wykorzystujących znane luki w zabezpieczeniach. Typowe te luki w zabezpieczeniach ataki, skryptów krzyżowych ataków tooname kilka. Zapobieganie takich ataków w kodzie aplikacji może być trudne i może wymagać rygorystyczne konserwacji, monitorowanie w wielu warstw Topologia aplikacji hello i stosowanie poprawek. Zapora aplikacji sieci web scentralizowane ułatwia zarządzanie zabezpieczeniami znacznie prostsza i zapewnia lepsze zapewnienia administratorom tooapplication przed zagrożeniami lub wtargnięcia. Rozwiązanie zapory aplikacji sieci Web można reagować zagrożeniem bezpieczeństwa tooa szybsze przez stosowanie poprawek znane luki w zabezpieczeniach w centralnej lokalizacji i zabezpieczanie wszystkich aplikacji sieci web indywidualnych. Brama aplikacji w włączona jest Zapora aplikacji sieci web przekonwertowanego tooa można łatwo istniejącej bramy aplikacji.

Niektóre hello zapory aplikacji sieci web, która chroni przed znanych luk w sieci web obejmuje:

- Ochrona przed atakami polegającymi na iniekcji SQL

- Ochrona przed atakami z użyciem skryptów wykorzystywanych w obrębie wielu witryn

- Częste ataki w ramach sieci Web polegające na iniekcji poleceń, przemycaniu żądań HTTP, rozdzielaniu odpowiedzi HTTP i zdalnym dołączaniu plików

- Ochrona przed naruszeniami protokołu HTTP

- Ochrona przed nieprawidłowościami protokołu HTTP, takimi jak brakujące powiązania agenta i użytkownika hosta oraz akceptowanie nagłówków

- Zapobieganie atakom z użyciem robotów, przeszukiwarek i skanerów

- Wykrycie typowych błędów konfiguracji aplikacji (czyli Apache usług IIS, itp.)

> [!Note]
> Aby bardziej szczegółową listę reguł i ich ochrony, zobacz następujące hello [podstawowe zestawy reguł](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview#core-rule-sets):

Platforma Azure oferuje również kilka toohelp łatwy w użyciu funkcji zabezpieczania ruchu przychodzącego i wychodzącego dla aplikacji. Azure umożliwia klientom zabezpieczyć ich kodu aplikacji przez zapewnienie zewnętrznie dostępne również tooscan funkcji luk w zabezpieczeniach aplikacji sieci web.

- [Zabezpieczenia aplikacji sieci web przy użyciu różne metody uwierzytelniania i autoryzacji](https://docs.microsoft.com/azure/app-service-web/web-sites-authentication-authorization)

    - [Konfiguracja uwierzytelniania aplikacji usługi Azure Active Directory](https://azure.microsoft.com/blog/azure-websites-authentication-authorization/)


- [Bezpieczny ruch tooyour aplikacji przez włączenie Transport Layer Security (TLS/SSL) - HTTPS](https://docs.microsoft.com/azure/app-service-web/web-sites-configure-ssl-certificate)

    - [Wymuś cały ruch przychodzący za pośrednictwem połączenia HTTPS](http://microsoftazurewebsitescheatsheet.info/)

  - [Włącz zabezpieczenie Transport ograniczeniami (HSTS)](http://microsoftazurewebsitescheatsheet.info/#enable-http-strict-transport-security-hsts)


- [Ograniczanie dostępu do aplikacji tooyour według adresu IP klienta](http://microsoftazurewebsitescheatsheet.info/#filtering-traffic-by-ip)

- [Ograniczenie dostępu do aplikacji tooyour przez zachowanie klienta - częstotliwość żądania i współbieżność](http://microsoftazurewebsitescheatsheet.info/#dynamic-ip-restrictions)

- [Skanowanie kodu aplikacji sieci web dla luk w zabezpieczeniach za pomocą skanowania przy użyciu usługi Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/)

- [Konfigurowanie protokołu TLS wzajemnego uwierzytelniania toorequire klienta certyfikaty tooconnect tooyour sieci web aplikacji](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth)

- [Skonfiguruj certyfikat klienta do użycia z Twojej aplikacji toosecurely łączenie zasobów tooexternal](https://azure.microsoft.com/blog/using-certificates-in-azure-websites-applications/)

- [Usuń narzędzia tooavoid nagłówki standardowe serwera z odcisków aplikacji](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/)

- [Bezpieczne łączenie aplikacji z zasobami w sieci prywatnej przy użyciu sieci VPN typu punkt-lokacja](https://docs.microsoft.com/azure/app-service-web/web-sites-integrate-with-vnet)

- [Bezpieczne łączenie z zasobami w sieci prywatnej przy użyciu połączeń hybrydowych aplikacji](https://docs.microsoft.com/azure/app-service-web/web-sites-hybrid-connection-get-started)

Azure korzysta z usługi aplikacji hello tego samego rozwiązania chroniące przed złośliwym kodem przez usług Azure Cloud Services i maszyny wirtualne. toolearn więcej na ten temat można znaleźć tooour [dokumentacji ochrony przed złośliwym kodem](https://docs.microsoft.com/azure/security/azure-security-antimalware).

## <a name="secure-your-network-protect"></a>Zabezpieczenia sieci (Ochrona)
Microsoft Azure obejmuje niezawodne toosupport infrastruktury sieci, aplikacji i wymaganiami dotyczącymi łączności usługi. Łączność sieciowa będzie możliwe między zasobami znajdującymi się na platformie Azure, między lokalnymi i Azure hostowanej zasobów oraz tooand z hello Internet i Azure.

Witaj [infrastruktury sieci platformy Azure](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-networking-guidelines) umożliwia toosecurely możesz połączyć zasoby platformy Azure tooeach innych z [sieci wirtualnych (sieci wirtualne)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview). Sieci wirtualnej jest reprezentację sieci w chmurze hello. Sieci wirtualnej jest logiczną izolacją hello chmury Azure w wersji dedykowanej sieci tooyour subskrypcji. Możesz połączyć sieci lokalnej tooyour sieci wirtualnych.

![Zabezpieczenia sieci (Ochrona)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig6.png)

Jeśli potrzebujesz kontroli dostępu na poziomie sieci podstawowej (oparte na adres i hello TCP lub UDP protokołów IP), a następnie można użyć [grup zabezpieczeń sieci](https://docs.microsoft.com/azure/virtual-network/virtual-networks-nsg). Grupy zabezpieczeń sieci (NSG) jest filtrowanie Zapora podstawowa pakietów stanowe i umożliwia toocontrol dostępu na podstawie [5-elementowej](https://www.techopedia.com/definition/28190/5-tuple).

Sieć platformy Azure obsługuje zachowania routingu hello toocustomize możliwości hello ruchu w sieci dla sieci wirtualne platformy Azure. Można to zrobić przez skonfigurowanie [trasy zdefiniowane przez użytkownika](https://docs.microsoft.com/azure/virtual-network/virtual-networks-udr-overview) na platformie Azure.

[Wymuszone tunelowanie](https://www.petri.com/azure-forced-tunneling) jest mechanizm służy tooensure, że usługi nie są dozwolone tooinitiate toodevices połączenia na powitania Internet.

Obsługuje platformy Azure w wersji dedykowanej sieci lokalnej tooyour łączności łącza sieci WAN i sieci wirtualnej platformy Azure z [ExpressRoute](https://docs.microsoft.com/azure/expressroute/expressroute-introduction). Powiązanie Hello Azure i witryny sieci Web używa dedykowanego połączenia nie przechodzi przez hello publicznej sieci Internet. Jeśli aplikacja Azure jest uruchomiona w wielu centrach danych, możesz użyć [usługi Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview) tooroute żądania od użytkowników inteligentnie między wystąpieniami aplikacji hello. Można również przekierować tooservices ruchu nie działa na platformie Azure, jeśli są one dostępne z hello Internet.

## <a name="virtual-machine-security-protect"></a>Zabezpieczeń maszyny wirtualnej (Ochrona)

[Maszyny wirtualne platformy Azure](https://docs.microsoft.com/azure/virtual-machines/) umożliwia wdrażanie szeroką gamę rozwiązań opartych na przetwarzaniu w sposób elastyczne. Dzięki obsłudze rozwiązań Microsoft Windows, Linux, Microsoft SQL Server, Oracle, IBM i SAP oraz usługi BizTalk Services na platformie Azure możesz wdrożyć dowolne obciążenie w dowolnym języku i w prawie każdym systemie operacyjnym.

Przy użyciu platformy Azure, można użyć [ochrony przed złośliwym oprogramowaniem](https://docs.microsoft.com/azure/security/azure-security-antimalware) od dostawców zabezpieczeń, takich jak Microsoft, firmy Symantec, Trend Micro i Kaspersky tooprotect maszyn wirtualnych z złośliwych plików, adware i innymi zagrożeniami.

Antimalware firmy Microsoft dla usług Azure Cloud Services i maszyn wirtualnych jest możliwość ochrony w czasie rzeczywistym, która pomaga w identyfikacji i usuwania wirusy, programy szpiegujące lub inne złośliwe oprogramowanie. Microsoft Antimalware udostępnia można skonfigurować alerty, gdy znane tooinstall prób złośliwego lub niechcianego oprogramowania, się lub uruchomić w systemie Azure.

[Kopia zapasowa Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) jest skalowalna, która chroni dane aplikacji z zero inwestycji kapitału i minimalne kosztów operacyjnych. Błędy aplikacji mogą powodować uszkodzenia danych, a błędy użytkowników — usterki aplikacji. Kopia zapasowa Azure maszynach wirtualnych z systemem Windows i Linux są chronione.

[Usługa Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview) pomaga organizowania replikacji, trybu failover i odzyskiwania obciążeń i aplikacji, tak aby były dostępne z lokalizacji dodatkowej jeśli spadnie do lokalizacji głównej.

## <a name="ensure-compliance-cloud-services-due-diligence-checklist-protect"></a>Zapewnianie zgodności: usługi powodu starannością listy kontrolnej w chmurze (Ochrona)

Microsoft opracowała [hello Lista kontrolna starannością na chmurze usługi](https://aka.ms/cloudchecklist.download) organizacji toohelp stosowny starannością jako uznają chmury toohello przenoszenia. Zapewnia to struktura dla organizacji, rozmiar i typ — prywatnej firmy i organizacje sektora publicznego, w tym dla instytucji rządowych na wszystkich poziomach oraz organizacjom — tooidentify ich wydajności, usługi Zarządzanie danymi i cele ładu i wymagania. Dzięki temu są toocompare hello oferowanych przez różnych dostawców usługi w chmurze ostatecznie stanowiący podstawę hello umowy usługi chmury.

Lista kontrolna Hello zapewniają strukturę, która wyrównuje klauzuli przez klauzulę o nowy standard międzynarodowych umów usługi chmury, ISO/IEC 19086. Ten standard udostępnia zestaw połączonych uwag dotyczących organizacji toohelp ich podejmowania decyzji o przyjęciu chmury i utworzyć podstawą typowe porównanie ofert usług w chmurze.

Lista kontrolna Hello zamienia chmury toohello dokładnie sprawdzonych i doświadczonych przenoszenia, podając wskazówki strukturalnych i podejście spójne i powtarzalnej Wybieranie dostawcy usług w chmurze.

Wdrożenia chmury nie jest już po prostu decyzji technologii. Ponieważ lista kontrolna wymagania touch na wszystkie aspekty organizacji, służą tooconvene wszystkich kluczy wewnętrzny-podejmujące — Witaj CIO i CISO, a także prawnych, ryzyka specjalistom ds. zarządzania, nabywania i zgodności. Powoduje to zwiększenie wydajności hello hello proces podejmowania decyzji i podstaw decyzji w dźwięk uzasadnienie, co zmniejsza prawdopodobieństwo hello tooadoption nieprzewidzianego roadblocks.

Ponadto hello Lista kontrolna:

- Udostępnia tematy dyskusji klucza dla decydentów początku hello hello chmury przyjęcia procesu.

- Obsługuje dokładnego firm dyskusjach na temat wykonawcze i cele w organizacji hello prywatności, dane osobowe (dane osobowe) i bezpieczeństwo danych.

- Pomaga organizacjom Zidentyfikuj potencjalne problemy, które mogą wpłynąć na projekt w chmurze.

- Zapewnia spójny zestaw pytań z hello samych warunków, definicje, metryki i materiałów dla każdego dostawcy, proces hello toosimplify porównanie ofert od dostawcy usług w innej chmurze.

## <a name="azure-infrastructure-and-application-security-validation-detect"></a>Azure walidacji infrastruktury i aplikacji (wykrywa)

[Azure bezpieczeństwa operacyjnego](https://docs.microsoft.com/azure/security/azure-operational-security) odwołuje się toohello usług, kontrolek i toousers dostępnych funkcji ochrony danych, aplikacji i innych zasobów na platformie Microsoft Azure.

![Sprawdzanie poprawności zabezpieczeń (wykrywa)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig7.png)

Azure bezpieczeństwa operacyjnego w oparciu framework, która będzie zawierała wiedzę hello za pośrednictwem różnych funkcji, które są unikatowe tooMicrosoft, w tym hello Microsoft Security Development Lifecycle (SDL), hello Centrum odpowiedź zabezpieczeń firmy Microsoft Program i głębokie świadomości hello bezpieczeństwa zagrożeń.

### <a name="microsoft-operations-management-suiteoms"></a>Microsoft operations management suite(OMS)

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) jest hello IT rozwiązania do zarządzania hello chmura hybrydowa. Użyte bez parametrów lub tooextend, który zapewnia istniejącego wdrożenia programu System Center, OMS hello maksymalną elastyczność i kontrola zarządzania infrastruktury w chmurze.

![Microsoft operations management suite(OMS)](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig8.png)

Dzięki OMS mogą zarządzać wystąpienie w żadną chmurą, tym lokalnymi, Azure AWS, Windows Server, Linux, VMware i OpenStack, na niższe koszty niż konkurencyjnych rozwiązania. Skompilowany dla Witaj świecie pierwszy chmury, OMS oferuje nowe toomanaging podejście przedsiębiorstwie hello najszybsze i najbardziej ekonomiczny sposób toomeet nowych transakcji będzie wymagał i uwzględnić nowe obciążenia, aplikacji i środowisk chmury.

### <a name="log-analytics"></a>Log Analytics

Usługa [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) umożliwia monitorowanie pakietu OMS przez zbieranie danych z zarządzanych zasobów w centralnym repozytorium. Te dane mogą obejmować zdarzeń, danych wydajności lub niestandardowe dane przekazane za pośrednictwem hello interfejsu API. Po zebraniu danych, danych hello jest dostępna dla alertów, analizy i eksportowanie.

![Log Analytics](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig9.png)

Ta metoda umożliwia tooconsolidate danych z różnych źródeł, więc można połączyć dane z usługami Azure z istniejącą lokalnego środowiska. Oddziela również wyraźnie hello zbierania danych hello hello akcję podejmowaną w odniesieniu do danych tak, aby wszystkie akcje są dostępne tooall rodzajów danych z.

### <a name="azure-security-center"></a>Centrum zabezpieczeń Azure

[Centrum zabezpieczeń Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) pomaga zapobiegania, wykrywania i odpowie toothreats lepszy wgląd w i kontroli nad hello zabezpieczeń zasobów platformy Azure. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

Centrum zabezpieczeń analizuje stan zabezpieczeń hello z zasobów platformy Azure tooidentify potencjalnych luk w zabezpieczeniach. Lista zaleceń prowadzi użytkownika przez proces konfigurowania wymaganych elementów sterujących hello.

Przykłady:

- Inicjowanie obsługi ochrony przed złośliwym kodem toohelp identyfikacji i usuwania złośliwego oprogramowania

- Konfigurowanie sieci zabezpieczeń grup i reguł toocontrol ruchu tooVMs

- Inicjowanie obsługi administracyjnej zapór aplikacji sieci web toohelp chronić przed atakami, które odnoszą się do aplikacji sieci web

- Wdrażanie brakujących aktualizacji systemu

- Modyfikowanie konfiguracji systemu operacyjnego, które nie odpowiadają hello zalecanych planów bazowych

Centrum zabezpieczeń automatycznie gromadzi, analizuje i integruje dane dzienników z zasobów platformy Azure, hello sieci i rozwiązań partnerskich, takich jak programy ochrony przed złośliwym oprogramowaniem i zapory. Po wykryciu zagrożenia tworzony jest alert zabezpieczeń. Przykłady obejmują wykrywanie:

- Złamany maszyny wirtualnej komunikowania się ze znanymi złośliwymi adresami IP

- Zaawansowanego złośliwego oprogramowania wykrytego za pomocą funkcji raportowania błędów systemu Windows

- Ataków siłowych wobec maszyn wirtualnych

- Alerty zabezpieczeń ze zintegrowanych programów chroniących przed złośliwym oprogramowaniem i zapór

### <a name="azure-monitor"></a>Monitor systemu Azure

[Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview) zawiera tooinformation wskaźniki dotyczące określonych typów zasobów. Zapewnia ona wizualizacji, zapytania, routingu, alerty, automatyczne skalowanie i automatyzacji na dane zarówno z hello infrastruktury platformy Azure (dziennik) i każdego pojedynczego zasobu platformy Azure (dzienników diagnostycznych).

Aplikacje w chmurze są złożonych z wielu części ruchu. Monitorowania udostępnia tooensure danych, która aplikacja pozostaje w górę i uruchomiona w dobrej kondycji. Pomaga również należy toostave wyłączone potencjalne problemy lub Rozwiązywanie problemów z przeszłości te.

![Azure monitor](media/azure-security-technical-capabilities/azure-security-technical-capabilities-fig10.png) Ponadto można użyć monitorowania danych toogain szczegółowych informacji o aplikacji. Wiedzy może pomóc tooimprove wydajność aplikacji lub utrzymania lub automatyzować czynności, które w przeciwnym razie wymagają ręcznej interwencji.

Inspekcja zabezpieczeń sieci jest niezbędne do wykrycia luk w zabezpieczeniach sieci i zapewniania zgodności z przepisami ładu modelu i zabezpieczeń IT. Z widokiem grupy zabezpieczeń możesz można pobrać hello skonfigurowane reguły grupy zabezpieczeń sieci i zabezpieczeń, a także hello reguły efektywnym elementem systemu zabezpieczeń. Z listą hello zasady zastosowane należy określić się, że są otwarte porty hello i ss luki w zabezpieczeniach sieci.

### <a name="network-watcher"></a>Obserwatora sieciowego

[Monitor sieci](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) to regionalnych usługa, która umożliwia toomonitor i diagnozowanie warunki na poziomie sieci w, do i z platformy Azure. Diagnostyka sieci i narzędzi wizualizacji dostępnych z obserwatora sieciowego pomagają zrozumieć, diagnozowanie i uzyskać informacje na temat technologii sieci tooyour na platformie Azure. Ta usługa obejmuje przechwytywania pakietów, następnego przeskoku, przepływ IP Sprawdź widok grupy zabezpieczeń, dzienniki przepływu NSG. Scenariusz poziomu monitorowania udostępnia widok tooend zakończenia zasobów sieciowych w monitorowania zasobów sieciowych tooindividual kontrastu.

### <a name="storage-analytics"></a>Analityka magazynu

[Analityka magazynu](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) może przechowywać metryki, które zawierają zagregowane transakcji statystyk i pojemności dane dotyczące usługi Magazyn tooa żądań. Transakcje są raportowane zarówno na poziomie operacji hello interfejsu API, a także na poziomie usługi magazynu hello i pojemności jest zgłaszany na poziomie usługi hello magazynu. Dane metryk można wykorzystania usługi magazynu używanych tooanalyze, diagnozowanie problemów z żądania wysyłane przed hello usługi magazynu i tooimprove hello wydajności aplikacji korzystających z usługi.

### <a name="application-insights"></a>Usługa Application insights

[Usługa Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) jest rozszerzalną usługę zarządzania wydajności aplikacji (APM) dla deweloperów sieci web na wielu platformach. Użyj go toomonitor aplikacji sieci web na żywo. Usługa automatycznie wykryje nieprawidłowości w zakresie wydajności. Obejmuje on analytics zaawansowanych narzędzi toohelp diagnozować problemy i toounderstand co użytkownicy wykonać za pomocą aplikacji. Zaprojektowano go toohelp stale zwiększyć wydajność i użyteczność. Działa w przypadku aplikacji na różnych platformach w tym .NET, Node.js i J2EE obsługiwanego lokalnie lub w chmurze hello. Integruje się z procesu opracowywania oprogramowania, a ma tooa punktów połączenia różnych narzędzi programistycznych.

Monitoruje ona:

- **Liczby żądań, czasy reakcji i współczynniki błędów** — dowiedz się, które strony są najbardziej popularne, o jakiej porze dnia i gdzie są Twoi użytkownicy. Zobacz, które strony działają najlepiej. Jeśli Twoje czasy odpowiedzi i częstotliwości awarii są duże, gdy jest więcej żądań, być może masz problem z zasobami.

- **Współczynniki zależności, czasy reakcji i współczynniki błędów** — dowiedz się, czy usługi zewnętrzne nie spowalniają pracy.

- **Wyjątki** — analizowania statystyk zagregowane hello, lub wybierz określone wystąpienia i przejść do szczegółów w hello ślad stosu i powiązane żądań. Są zgłaszane zarówno wyjątki serwera, jak i przeglądarki.

- **Wydajność ładowania i wyświetleń stron** — zgłoszona przez przeglądarki użytkowników.

- **Wywołania AJAX ze stron sieci web** -szybkość, czas reakcji i awariami.

- **Liczba użytkowników i sesji.**

- **Liczniki wydajności** z serwerów systemu Windows lub Linux, takie jak użycie procesora CPU, pamięci i sieci.

- **Diagnostyka hosta** z platformy Docker lub Azure.

- **Diagnostyczne dzienniki śledzenia** z Twojej aplikacji — dzięki temu możesz skorelować zdarzenia śledzenia z żądaniami.

- **Niestandardowe zdarzenia i metryki** napisać samodzielnie w kodzie powitania klienta lub serwera, tootrack zdarzenia biznesowe, takie jak towarów sprzedanych lub gry won.
Hello infrastruktura aplikacji zwykle obejmuje wiele składników — może być maszynę wirtualną, konta magazynu i sieci wirtualnej lub aplikacji sieci web, bazy danych, serwer bazy danych i 3 usług firm. Te składniki nie są widoczne jako osobne jednostki, tylko jako powiązane i zależne od siebie nawzajem części jednej całości. Mają toodeploy, zarządzanie i monitorowanie ich jako grupa. [Usługa Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) pozwala toowork z zasobami hello w rozwiązaniu jako grupa.

Można wdrożyć, zaktualizować lub usunąć wszystkie zasoby powitania dla danego rozwiązania w jednej, skoordynowanej operacji. Wdrażanie wykonuje się przy użyciu szablonu, którego można następnie używać w różnych środowiskach (testowanie, etap przejściowy i produkcja). Usługa Resource Manager zapewnia zabezpieczeń, inspekcji i znakowanie toohelp funkcje zarządzania zasobami po wdrożeniu.

**Zalety Hello za pomocą Menedżera zasobów**

Usługa Resource Manager zapewnia kilka korzyści:

- Można wdrożyć, zarządzanie i monitorowanie wszystkich zasobów hello do rozwiązania jako grupy zamiast obsługiwania zasobów pojedynczo.

- Można wielokrotnie wdrażania rozwiązania w całym cyklu programistycznym hello i mieć pewność, zasoby są wdrażane w spójnym stanie.

- Możliwość zarządzania infrastrukturą przy użyciu szablonów deklaratywnych zamiast skryptów.

- Można zdefiniować hello zależności między zasobami, aby wdrażać je w odpowiedniej kolejności hello.

- Można zastosować usług tooall kontroli dostępu w grupie zasobów, ponieważ na platformie zarządzania hello natywnej integracji funkcji kontroli dostępu opartej na rolach (RBAC).

- Możliwość dodawania tagów tooresources toologically organizowanie wszystkie zasoby hello w ramach subskrypcji.

- Można również uprościć rozliczenia w organizacji, wyświetlając kosztów dla grupy zasobów udostępnianie hello na tym samym tagiem.

> [!Note]
> Menedżer zasobów udostępnia nowe toodeploy sposób rozwiązań i zarządzania nimi. Jeśli używasz hello wcześniejszego modelu wdrożenia i mają toolearn o zmianach hello, zobacz [wdrożenia Understanding Resource Manager oraz wdrażania klasycznego](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-deployment-model).

## <a name="next-steps"></a>Następne kroki

Dowiedz się więcej o zabezpieczeń, odczytując niektóre nasze tematy szczegółowe zabezpieczeń:

- [Inspekcja i rejestrowanie](https://www.microsoft.com/en-us/trustcenter/security/auditingandlogging)

- [Wzrost cyberprzestępczości](https://www.microsoft.com/en-us/trustcenter/security/cybercrime)

- [Projektowanie i bezpieczeństwa operacyjnego](https://www.microsoft.com/en-us/trustcenter/security/designopsecurity)

- [Szyfrowanie](https://www.microsoft.com/en-us/trustcenter/security/encryption)

- [Zarządzanie tożsamościami i dostępem](https://www.microsoft.com/en-us/trustcenter/security/identity)

- [Bezpieczeństwo sieci](https://www.microsoft.com/en-us/trustcenter/security/networksecurity)

- [Zarządzanie zagrożeniami](https://www.microsoft.com/en-us/trustcenter/security/threatmanagement)
