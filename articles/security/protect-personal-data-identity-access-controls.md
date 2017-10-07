---
title: "dane osobowe aaaProtect z Azure formanty tożsamościami i dostępem | Dokumentacja firmy Microsoft"
description: "Przy użyciu Azure toohelp formanty tożsamościami i dostępem chronić dane osobowe użytkownika"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 3132c2af25f86662668e5b555eab1d81de7f2e6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-and-multi-factor-authentication-protect-personal-data-with-identity-and-access-controls"></a>Azure Active Directory i uwierzytelniania wieloskładnikowego: ochrony danych osobowych z formantami tożsamościami i dostępem

Ten artykuł zawiera informacje i procedury, można użyć danych osobowych tooprotect przy użyciu usługi i funkcje zabezpieczeń uwierzytelniania usługi Azure Active Directory i usługi Multi-Factor.

## <a name="scenario"></a>Scenariusz

Firma rejs dużych, siedzibą w Stanach Zjednoczonych hello, rozwija trasy toooffer jego operacji w Śródziemnego hello, Adriatyku i Bałtyckiego mórz, jak również hello brytyjskich. toosupport tych działań uzyskała mniejszych rejs wiersze na podstawie we Włoszech Niemczech, Dania i hello Zjednoczone Królestwo 

Witaj firma korzysta z danych firmowych toostore Microsoft Azure w chmurze hello. Dotyczy to również dane osobowe, takich jak nazwy, adresy, numery telefonów i informacje o karcie kredytowej z jej klientów globalnych. Zawiera także tradycyjnych informacje kadr, takie jak adresy, numery telefonów, numery identyfikacyjne podatku i medyczne informacje dotyczące pracowników firmy we wszystkich lokalizacjach. wiersz rejs Hello zachowuje również dużej bazy danych elementów członkowskich programu osób trzecich i lojalność zawierający dane osobowe tootrack relacje z bieżących i starszych klientów.

Pracownikom firmy dostępu hello sieci z biurach zdalnych i agentów podróży hello firmy znajdujących się wokół Witaj świecie mają dostęp do zasobów firmowych toosome.

## <a name="problem-statement"></a>Opis problemu

Hello firmy muszą chronić prywatność hello danych osobowych pracowników i klientów przed atakami znalezienia dostępu toogain tożsamości toouse naruszenia zabezpieczeń. One także sprawdzić toopersonal tego dostępu, które dane przez autoryzowanych użytkowników jest ograniczony tylko do tych wymagających toodo swoich zadań.

## <a name="company-goal"></a>Celem firmy

Celem firmy Hello jest tooensure, że dostęp do danych toopersonal ścisłą kontrolę. Istotne jest, że tożsamości użytkowników mających dostęp do danych toopersonal być chronione przez silnego uwierzytelniania. Zasady [najniższych uprawnień] (https://en.wikipedia.org/wiki/Principle_of_least_privilege) musi odbywać się tak, że istnieje tylko poziom hello potrzebują dostępu i nie więcej.

## <a name="solutions"></a>Rozwiązania

Microsoft Azure udostępnia narzędzia do zarządzania tożsamościami i dostępem toohelp firm kontrolować, kto może tooresources dostępu, które zawierają dane osobowe.

### <a name="azure-active-directory"></a>Usługa Azure Active Directory

[Usługa Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) (AAD) zarządza tożsamości i kontroluje dostęp tooAzure, jak również innych lokalnych i innych zasobów w chmurze, danych i aplikacji. [Azure Active Directory Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access) pomaga Azure Administratorzy toominimize hello liczbę użytkowników, którzy mają dostęp toocertain informacje, takie jak dane osobowe. Pozwala toodiscover, ograniczenia i monitorowanie tożsamości uprzywilejowanych i ich tooresources i tooassign tymczasowe, just in Time (JIT) prawa administracyjne tooeligible użytkowników dostępu. Zapewnia wgląd w tych, którzy mają uprawnienia administracyjne w usłudze AAD.

Witaj działania związane ze stosowaniem AAD PIM obejmują:

- Włączanie katalogu Privileged Identity Management

- Przy użyciu Privileged Identity Management admin pulpit nawigacyjny toosee ważne informacje w skrócie

- Zarządzanie tożsamościami hello uprzywilejowany (Administratorzy) przez dodanie lub usunięcie roli tooeach stałych lub kwalifikujących się Administratorzy

- Konfigurowanie ustawień aktywacji roli hello

- Aktywacja ról

- Przeglądanie roli działania

#### <a name="how-do-i-enable-aad-pim"></a>Jak włączyć AAD PIM?

przy użyciu usługi PIM dla katalogu, toostart hello następujące:

1. Zaloguj się toohello portalu Azure jako administrator globalny katalogu.

2. Jeśli Twoja organizacja ma więcej niż jeden katalog, w hello prawym górnym rogu hello portalu Azure wybierz nazwy użytkownika. Wybierz katalog hello, w którym będziesz używać usługi Azure AD Privileged Identity Management.

3. Wybierz **więcej usług** i użyj hello **filtru** toosearch pole tekstowe dla usługi Azure AD Privileged Identity Management.

4. Sprawdź **toodashboard numeru Pin** , a następnie kliknij przycisk **Utwórz**. Otwiera Hello aplikacji Privileged Identity Management.

Po skonfigurowaniu usługi Azure AD Privileged Identity Management, zobacz blok nawigacji hello przy każdym otwarciu aplikacji hello.

![](media/protect-personal-data-identity-access-controls/azure-pim.png)

Aby uzyskać więcej informacji oraz instrukcje dotyczące wprowadzenie do korzystania z usługi PIM w usłudze AAD, zobacz [uruchomić przy użyciu usługi Azure AD Privileged Identity Management.](https://docs.microsoft.com/active-directory/active-directory-privileged-identity-management-getting-started)

### <a name="azure-role-based-access-control"></a>Kontrola dostępu oparta na rolach na platformie Azure

[Kontrola dostępu oparta na rolach Azure](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) (RBAC) ułatwia administratorom Azure, zarządzanie zasobami tooAzure dostępu przez włączenie hello przyznawania dostępu na podstawie użytkownika hello przypisanej roli. Możesz rozdzielenie obowiązków w zespole i udzielić tylko hello ilość toousers dostępu, grup i aplikacji, że powinni tooperform swoich zadań.

Dostępu na podstawie roli może zostać przydzielony toousers przy użyciu hello portalu Azure, narzędzi wiersza polecenia platformy Azure lub interfejsów API zarządzania platformy Azure.

Aby uzyskać więcej informacji dotyczących podstaw Azure RBAC, zobacz [wprowadzenie opartej na rolach kontrola dostępu w hello portalu Azure.](https://docs.microsoft.com/active-directory/role-based-access-control-what-is)

#### <a name="how-do-i-manage-azure-rbac-with-powershell"></a>Jak zarządzać Azure RBAC przy użyciu programu PowerShell?

Możesz użyć toomanage poleceń cmdlet programu PowerShell Azure RBAC, w tym hello następujące zadania związane z zarządzaniem:

- Lista ról

- Zobacz, kto ma dostęp

- Udzielanie dostępu

- Usuń dostęp

- Tworzenie niestandardowej roli zabezpieczeń

- Pobierz akcji dla dostawcy zasobów

- Modyfikowanie niestandardowej roli zabezpieczeń

- Usunięcia niestandardowej roli zabezpieczeń

- Lista ról niestandardowych

Aby uzyskać instrukcje dotyczące toomanage Azure RBAC przy użyciu programu PowerShell, zobacz temat [opartej na rolach Zarządzanie dostępu przy użyciu programu Azure PowerShell](https://docs.microsoft.com/azure/active-directory/role-based-access-control-manage-access-powershell).

### <a name="azure-multi-factor-authentication"></a>Azure Multi-Factor Authentication

[Usługa Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/) (MFA) jest rozwiązaniem weryfikacji dwuetapowej, która ułatwia zabezpieczenie dostępu toodata i aplikacje, jednocześnie spełniając zapotrzebowanie na prosty proces logowania. Oferuje ona silne uwierzytelnianie za pośrednictwem różnych metod weryfikacji, w tym weryfikacji w trakcie rozmowy telefonicznej albo przy użyciu wiadomości SMS lub aplikacji mobilnej.

toodeploy MFA w hello chmury Azure należy toofirst ją włączyć, a następnie Włącz weryfikację dwuetapową dla użytkowników.

#### <a name="how-do-i-enable-azure-toouse-mfa"></a>Jak włączyć Azure toouse MFA?

Jeśli użytkownicy mają licencje, które obejmują usługi Azure Multi-Factor Authentication, nie ma nic konieczność tooturn toodo na usługę Azure MFA. W przeciwnym razie należy toocreate dostawcy uwierzytelniania wieloskładnikowego w katalogu. toodo, wykonaj następujące kroki:

1. Wybierz **usługi Active Directory** w hello klasycznego portalu Azure (zalogowany jako administrator).

2. Wybierz **dostawców uwierzytelniania wieloskładnikowego.**

3. Wybierz **nowy** , a następnie w obszarze **usługi aplikacji** wybierz **dostawcy uwierzytelniania wieloskładnikowego.**

4. Wybierz **szybkie tworzenie.**

5. Wypełnij pole Nazwa hello i wybierz model użycia (dla uwierzytelniania lub każdego włączonego użytkownika).

6. Wybierz katalog, z którego hello jest skojarzony dostawca usługi MFA.

7. Kliknij przycisk hello **Utwórz** przycisku.

![](media/protect-personal-data-identity-access-controls/quick-create.png)

Aby uzyskać dodatkowe instrukcje na temat toomanage dostawcy uwierzytelniania wieloskładnikowego, zobacz [wprowadzenie do korzystania z dostawcy usługi Azure Multi-Factor Authentication.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-auth-provider)

#### <a name="how-do-i-turn-on-two-step-verification-for-users"></a>Jak włączyć weryfikację dwuetapową dla użytkowników?

Można wymusić weryfikacji dwuetapowej dla wszystkich logowania lub weryfikacji dwuetapowej toorequire zasady dostępu warunkowego można utworzyć tylko wtedy, gdy określone warunki są spełnione.

Włączanie usługi Azure MFA, zmieniając stanów użytkownika jest hello tradycyjne podejście, wymagająca weryfikacji dwuetapowej. Wszyscy użytkownicy hello, które można włączyć będą mieć hello tooperform sam wymóg włączono weryfikację dwuetapową, za każdym razem zalogują się w. Włączenie użytkownik zastępuje wszystkie zasady dostępu warunkowego, które mogą mieć wpływ na tego użytkownika.

Włączanie usługi Azure MFA z zasad dostępu warunkowego jest bardziej elastyczne podejście wymagająca weryfikacji dwuetapowej. Można utworzyć zasady dostępu warunkowego, które dotyczą toogroups, a także poszczególnych użytkowników. O wysokim ryzyku grup można przydzielić więcej ograniczeń, niż niskiego ryzyka grup lub weryfikacji dwuetapowej mogą być wymagane tylko dla aplikacji w chmurze o wysokim ryzyku i pomijana dla nich niskiego ryzyka. Dostęp warunkowy jest jednak płatnych funkcji usługi Azure Active Directory.

tooenable MFA przez zmianę stanu użytkownika hello następujące:

1. Zaloguj się toohello portalu Azure jako administrator.
2. Przejdź za**usługi Azure Active Directory \> użytkowników i grup \> wszyscy użytkownicy**.
3. Wybierz **uwierzytelnianie wieloskładnikowe**.
4. Znajdź użytkownika hello mają tooenable dla usługi Azure MFA. Może być konieczne toochange hello widoku u góry hello.
5. Sprawdź nazwę hello pole dalej toohello użytkownika.
6. W prawo, w obszarze Szybkie kroki hello, wybierz polecenie **włączyć**.

   ![](media/protect-personal-data-identity-access-controls/quick-create.png)

7. Potwierdź wybór w oknie podręcznym hello, który zostanie otwarty.  Użytkownicy, dla których włączono uwierzytelnianie wieloskładnikowe zostanie wyświetlony monit tooregister hello następnym razem zalogują się w.

tooenable usługi Azure MFA za pomocą zasad dostępu warunkowego hello następujące:

1. Zaloguj się toohello portalu Azure jako administrator.

2. Przejdź za**usługi Azure Active Directory \> dostępu warunkowego**.

3. Wybierz **nowe zasady**.

4. W obszarze **przypisania**, wybierz pozycję **użytkowników i grup**. Użyj hello **Include** i **wykluczyć** toospecify, którzy użytkownicy i grupy będą zarządzane przez zasady hello karty.

5. W obszarze **przypisania**, wybierz pozycję **aplikacji w chmurze.** Wybierz zbyt**obejmują wszystkie aplikacje w chmurze**.
6.  W obszarze **dostęp do formantów**, wybierz pozycję **Grant**. Wybierz **wymusić uwierzytelnianie wieloskładnikowe**.
7.  Włącz **Włącz zasady** za**na** , a następnie wybierz **zapisać**.

Aby uzyskać informacje dotyczące sposobu tooset ustawienia usługi Azure MFA tooconfigure zapasowej alertów oszustwa, utworzyć jednorazowe obejście, użycia niestandardowe wiadomości głosowe, skonfiguruj buforowania, określ listę zaufanych adresów IP, tworzenie haseł aplikacji, Włącz zapamiętywanie MFA dla urządzeń, które ufają użytkowników, a następnie wybierz metody weryfikacji, zobacz [Konfigurowanie ustawień uwierzytelnianie wieloskładnikowe Azure.](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-whats-next)

## <a name="next-steps"></a>Następne kroki

- [Zabezpieczanie uprzywilejowanego dostępu w usłudze Azure AD](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/active-directory-securing-privileged-access)

- [Często zadawane pytania dotyczące usługi Azure Multi-Factor Authentication](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-faq)

- [Oparta na rolach kontrola dostępu do rozwiązywania problemów](https://docs.microsoft.com/azure/active-directory/role-based-access-control-troubleshooting)

- [Ochronę tożsamości usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)
