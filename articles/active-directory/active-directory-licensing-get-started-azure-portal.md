---
title: "aaaGet wprowadzenie Licencjonowanie w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak Azure Active Directory działa Licencjonowanie, jak tooget pracę z najlepszych rozwiązań"
services: active-directory
keywords: "Licencjonowanie usługi Azure AD"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: H1Hack27Feb2017;it-pro
ms.openlocfilehash: 268dab806b8b959790341d630a0355c6a43871d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="license-yourself-and-your-users-in-azure-active-directory"></a>Licencja użytkownika, jak i użytkowników w usłudze Azure Active Directory

> [!div class="op_single_selector"]
> * [Instrukcje portalu Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Pobierz informacje dotyczące klasycznego Azure portalu](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) jest tożsamością jako rozwiązanie service (IDaaS) i platforma firmy Microsoft. Usługi Azure AD jest oferowana w wersjach usługi innej:

* Azure Active Directory wolny, która jest dostępna w usłudze firmy Microsoft, takich jak usługi Office 365, Dynamics, Microsoft Intune lub Azure. Usługi Azure AD nie generuje żadnych opłat za zużycie w tym trybie.

* Azure AD płatnej wersji, takich jak:
  - Enterprise Mobility + Security 
  - Azure AD Premium (P1 i P2)
  - Azure AD podstawowa
  - Azure Multi-Factor Authentication

Podobnie jak wiele innych usług Microsoft online services najbardziej Azure AD płatnej wersji są dostarczane za pośrednictwem uprawnień użytkownika, gdy znajdują się w usłudze Office 365, Microsoft Intune i Azure AD. W takich przypadkach zakupu usługi hello jest reprezentowany przez jedną lub kilka subskrypcji, a każda subskrypcja zawiera niektóre prepurchased licencji w dzierżawie. Uprawnienia użytkownika są realizowane za:

* Przypisywanie licencji. 
* Tworzenie połączenia między hello użytkownika i hello produktu.
* Włączanie składniki usługi hello hello użytkownika.
* Korzystanie z jednego z hello Przedpłata licencji.

[Wypróbuj teraz usługi Azure AD Premium.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Zawiera ogólne omówienie możliwości usługi Azure AD dla [co to jest usługa Azure AD?](active-directory-whatis.md). Aby uzyskać więcej informacji, zobacz nasze [strony umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Z subskrypcji platformy Azure umożliwiają tworzenie zasobów Azure, a następnie odwzorować je tooyour formy płatności. Nie ma żadnych liczby licencji skojarzone z subskrypcją hello. Przyznanie subskrypcji toohello zmapowana toooperate uprawnień użytkownika, na zasobów platformy Azure, są skojarzone z subskrypcją hello i mogą zarządzać zasobami subskrypcji.

## <a name="how-does-azure-active-directory-licensing-work"></a>Jak działa Licencjonowanie usługi Azure Active Directory?

Na podstawie licencji usługi Azure AD usług pracy przez aktywowania subskrypcji w dzierżawie usługi Azure AD. Po hello subskrypcja jest aktywna, możliwości usługi hello są zarządzane przez administratorów usługi Azure AD i używane przez licencjonowanych użytkowników.

### <a name="manage-subscription-information"></a>Zarządzanie informacjami o subskrypcji

Po zakupie pakietu Enterprise Mobility + Security, Azure AD Premium lub Azure AD podstawowa, dzierżawy jest aktualizowane hello subskrypcji, w tym okresie ważności i Przedpłata licencji. Informacji o subskrypcji, w tym hello liczby przydzielonych lub dostępnych licencji, jest dostępna za pośrednictwem portalu Azure hello: w obszarze **usługi Azure Active Directory**, otwórz hello **licencji** kafelku hello określony katalog. Witaj **licencji** bloku jest również hello najlepsze miejsce toomanage przypisaniami licencji.

Każda subskrypcja składa się z co najmniej jeden planów usług, takich jak Azure AD, uwierzytelnianie wieloskładnikowe, Intune, usługi Exchange Online lub SharePoint Online.  Zarządzanie licencjami usługi Azure AD jest *nie* wymaga poziomu planu usług zarządzania. Usługi Office 365 różni się, ponieważ zależy od tej usługi tooincluded konfiguracji zaawansowanej tryb toomanage dostępu. Usługi Azure AD zależy od konfiguracji użytkowanych tooenable funkcje i zarządzaj nimi indywidualnych uprawnień.

> [!IMPORTANT]
> Usługi Azure AD Premium, Azure AD podstawowa i Enterprise Mobility + Security subskrypcje są dzierżawy directory zamkniętej tootheir udostępnione. Nie można podzielić subskrypcje między katalogami lub użytkownicy tooentitle używane w innych katalogach. Przenoszenie subskrypcji między katalogami jest możliwe, ale wymaga przesłanie biletu pomocy technicznej lub anulowanie i odkupu dla bezpośrednie zakupów.
>
> Gdy usługi Azure AD lub pakietu Enterprise Mobility + Security jest zakupione w ramach subskrypcji usługi licencjonowania zbiorowego, a kiedy umowy hello obejmuje innych usług Online firmy Microsoft (na przykład usługi Office 365), aktywacja odbywa się automatycznie. 

### <a name="assign-licenses"></a>Przypisywanie licencji

Chociaż jest potrzebne wszystkie tooconfigure płatnej możliwości uzyskiwanie subskrypcji, możesz nadal dystrybuować licencji dla usługi Azure AD płatnej toousers funkcji. Każdy użytkownik, który powinien mieć tooor dostępu, która jest zarządzana za pomocą usługi Azure AD płatnej funkcji należy przypisać licencję. Przypisanie licencji jest mapowanie między użytkownikiem i zakupionych usług, takich jak Azure AD Premium, Basic lub pakietu Enterprise Mobility + Security.


Zarządzanie, którzy użytkownicy w katalogu powinien mieć licencję można osiągnąć przez: 

* Przypisywanie licencje toogroups w hello [portalu Azure](active-directory-licensing-whatis-azure-portal.md).
* Przypisywanie bezpośrednio licencje toousers hello portalu, programu PowerShell lub interfejsów API. 

W przypadku przypisywania licencji tooa grupy, wszyscy członkowie grupy przypisanych licencji. Jeśli użytkownicy są dodawane lub usuwane z grupy hello, odpowiednią licencję hello jest przypisany lub usunięty. Przypisanie do grupy mogą korzystać z dowolnej grupy zarządzania dostępne tooyou i jest ona zgodna z tooapplications przypisywania na podstawie grupy.

Można użyć [przypisanie licencji na podstawie grupy](active-directory-licensing-whatis-azure-portal.md) tooset reguł, takich jak hello poniżej:
* Wszyscy użytkownicy w katalogu automatycznie otrzymuje licencję
* Pobiera wszystkich osób mających stanowisko odpowiednie hello licencji
* Możesz delegować hello decyzji tooother menedżerów w organizacji hello (przy użyciu [grup samoobsługi](active-directory-accessmanagement-self-service-group-management.md))

Szczegółowe omówienie toogroups przypisanie licencji, w tym zaawansowane scenariusze i usługi Office 365 licencjonowania scenariuszy, zobacz [Przypisz licencje toousers przez członkostwo w grupie w usłudze Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Rozpoczynanie pracy z licencją Azure AD

Wprowadzenie do korzystania z usługi Azure AD jest bardzo proste. Zawsze można utworzyć katalogu jako część skorzystania [Azure bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p/).

Hello następujące najlepsze rozwiązania pozwala zagwarantować, że dzierżawy jest zgodne z innymi usługami firmy Microsoft, które mogą korzystać i cele usługi hello:

- Jeśli korzystasz już z hello organizacyjnej usług firmy Microsoft, masz już dzierżawę usługi Azure AD. Jest przydatne toouse powitalne takie same dzierżawy dla innych usług, dzięki czemu Zarządzanie tożsamościami core, w tym inicjowania obsługi administracyjnej i hybrydowych rejestracji jednokrotnej (SSO), można używać w usługach hello. Z logowania jednokrotnego użytkownikom korzystać z zaawansowanych funkcji hello w usługach hello. W związku z tym Jeśli zdecydujesz toobuy usługę Azure AD płatnej dla pracowników, zaleca się używanie hello sam dzierżawy ponownie.

- Zalecane jest użycie nowej dzierżawy w hello portalu Azure, jeśli jest planowane:
  - Użyj usługi Azure AD na inny zestaw użytkowników (takich jak partnerów lub klientów).
  - Oceny usługi Azure AD w izolacji od usługi produkcji.
  - Konfigurowanie środowiska izolowanego dla usług.

  Nowy katalog Hello jest tworzona przy użyciu konta jako zewnętrzne użytkownika z uprawnieniami administratora globalnego. Po zarejestrowaniu się w portalu Azure z tym kontem toohello, możesz wyświetlić tej dzierżawy i dostęp do wszystkich zadań administracyjnych.

> [!NOTE]
> Usługi Azure AD obsługuje gościa "Użytkownicy", które konta użytkowników w dzierżawie usługi Azure AD, które zostały utworzone za pomocą konta Microsoft lub tożsamości usługi Azure AD z innego dzierżawcę. portalu administracyjnego usługi Office 365 Hello nie obsługuje obecnie tych użytkowników. Goście z konta Microsoft nie są portalu administracyjnego usługi Office 365 hello tooaccess stanie na wszystkich podczas gości z innymi dzierżawcami usługi Azure AD są ignorowane. W drugim przypadku hello tylko hello lokalnego konta użytkownika w hello Azure AD lub dzierżawy usługi Office 365, której użytkownik hello pierwotnie został utworzony, nie jest dostępna.

### <a name="select-one-or-more-license-trials"></a>Wybierz co najmniej jeden prób licencji

Można aktywować usługi Azure AD Premium lub pakietu Enterprise Mobility + zabezpieczeń subskrypcji wersji próbnej w obszarze **usługi Azure Active Directory** &gt; **szybki start**.

![Wybierz z wersji próbnej licencji](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Na powitania dostępnych licencji wersji próbnej **licencji** bloku.

### <a name="assign-licenses-toousers-and-groups"></a>Przypisz licencje toousers i grupy

Po hello subskrypcja jest aktywna, należy przypisać tooyourself licencji. Następnie Odśwież tooensure przeglądarki hello wyświetlenie wszystkich funkcji hello. Witaj następnym krokiem jest tooassign licencji toohello użytkowników, którzy potrzebują funkcji Azure AD toopaid dostępu. Zgodnie z opisem w [przypisać licencje](#assign-licenses), jeden łatwy sposób tooassign licencji jest tooidentify hello grupy reprezentująca hello potrzeby odbiorców i przypisz hello tooit licencji. W ten sposób użytkownicy, którzy są dodawane lub usuwane z grupy hello jego cyklem zostały przypisane lub usunięte z licencji hello odpowiednio.

> [!NOTE]
> Pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach. Zanim można przypisać licencję użytkownika tooa, hello administrator musi określić hello **lokalizacji użytkowania** właściwość hello użytkownika. Można ustawić tę właściwość w obszarze **użytkownika** &gt; **profilu** &gt; **ustawienia** w hello portalu Azure. Używając przypisanie do grupy licencji, każdy użytkownik nie określono lokalizacji użytkowania, której dziedziczy hello lokalizację katalogu hello.

tooassign licencji w obszarze **usługi Azure Active Directory** &gt; **licencji** &gt; **wszystkich produktów**, wybierz jeden lub więcej produktów, a następnie wybierz **Przypisać** na powitania paska poleceń.

![Wybierz tooassign licencji](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

Można użyć hello **użytkowników i grup** wielu użytkowników lub grup lub usługi toodisable plany w produkcie hello toochoose bloku. Użyj pola wyszukiwania hello na najwyższym toosearch dla nazwy użytkowników i grup.

![Wybierz użytkownika lub grupy do przypisania licencji](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

W przypadku przypisywania tooa grupę licencji, może upłynąć pewien czas, zanim hello licencji, w zależności od hello liczbę użytkowników w grupie hello dziedziczą wszystkich użytkowników. Istnieje możliwość sprawdzenia stanu przetwarzania hello na powitania **grupy** bloku, w obszarze hello **licencji** kafelka.

![Stan przypisania licencji](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Przypisanie błędy mogą wystąpić podczas przypisanie licencji usługi Azure AD, ale są stosunkowo rzadko podczas zarządzania usługi Azure AD i Enterprise Mobility + Security produktów. Potencjalne błędy przydziału są ograniczone do:
- Konflikt przypisania: Jeśli użytkownik został już wcześniej przypisany licencji, która jest niezgodna z bieżącej licencji hello. W takim przypadku przypisanie hello nowej licencji wymaga usuwanie hello bieżący.
- Przekroczono dostępnych licencji: hello liczbę użytkowników w grupach przypisanej przekroczenia hello dostępnych licencji użytkownika stanu przypisania odzwierciedla tooassign awarii, ze względu toomissing licencji.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure licencjonowania współpracy B2B usługi AD

Współpraca B2B pozwala tooinvite gości do usług tooAzure AD dostępu tooprovide dzierżawy usługi Azure AD i dowolnych zasobów platformy Azure mają być dostępne.  

Jest bezpłatna dla zapraszanie B2B użytkowników i przypisywania do nich tooan aplikacji w usłudze Azure AD. Zapasowej too10 aplikacji dla gościa użytkownika i 3 podstawowe raporty są również bezpłatna dla użytkowników współpracy B2B. Jeśli użytkownika gościa zawiera wszystkie odpowiednie licencje przypisane w dzierżawie usługi Azure AD hello partnera, będą one licencjonowane w należy do Ciebie również.

Nie jest to wymagane, ale jeśli chcesz, aby funkcje usługi Azure AD toopaid dostępu tooprovide, muszą mieć licencję tych gości B2B z odpowiednimi licencjami usługi Azure AD. Zapraszanie dzierżawy z usługi Azure AD z płatnej licencji można przypisać prawa użytkownika współpracy B2B tooan pięć dodatkowych gości zaproszenie toohello dzierżawy. Scenariusze i informacje, zobacz [współpracy B2B licencjonowania wskazówki](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Wyświetl przypisane licencje

Widok podsumowania przypisane i dostępnych licencji zostanie wyświetlona w obszarze **usługi Azure Active Directory** &gt; **licencji** &gt; **wszystkie produkty**.

![Licencja wyświetlania podsumowania](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Szczegółową listę przypisanych użytkowników i grup jest dostępna po wybraniu określonego produktu. Witaj **licencjonowanych użytkowników** lista zawiera wszystkich użytkowników, w obecnie korzystających z licencji i czy licencji hello przypisano bezpośrednio toohello użytkownika lub jeśli zostało ono odziedziczone po grupie.

![Wyświetl szczegóły licencji](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

Podobnie, hello **grup licencji** lista zawiera wszystkich grup licencji toowhich zostały przypisane. Wybierz użytkownika lub grupę hello tooopen **licencji** bloku, który zawiera wszystkie licencje przypisać toothat obiektu.

### <a name="remove-a-license"></a>Usunąć licencję

tooremove licencji, przejdź toohello użytkownika lub grupę, a następnie otwórz hello **licencji** kafelka. Wybierz hello licencji, a następnie kliknij przycisk **Usuń**.

![Usunąć licencję](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Nie można bezpośrednio usunąć dziedziczone przez hello użytkownika z grupy licencji. Zamiast tego należy usunąć hello użytkownika z grupy hello, z którego są dziedziczone hello licencji.

### <a name="extend-trials"></a>Rozszerzenie wersji próbnych

Wersja próbna rozszerzenia dla klientów są dostępne jako samoobsługowego tworzenia konta za pośrednictwem portalu hello usługi Office 365. Administrator klienta można przejść toohello portalu usługi Office (dostępu zależy od uprawnień do portalu usługi Office hello) i wybierz hello Azure AD Premium w wersji próbnej. Kliknięcie przycisku hello **przedłużyć okres próbny** łącze spowoduje uruchomienie procesu rozszerzenia hello. Karty kredytowej jest wymagany, ale nie jest pobierana.

![Przedłużyć okres próbny w hello portalu Azure](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Następne kroki

więcej informacji o toolearn zaawansowanych scenariuszy zarządzania licencji za pomocą grup, przeczytaj artykuł hello [przypisywanie licencji tooa grupy](active-directory-licensing-group-assignment-azure-portal.md).

Poniżej przedstawiono informacje na temat tooconfigure i używanie innych usługi Azure AD płatnej funkcje:

* [Samoobsługowe Resetowanie hasła](active-directory-manage-passwords.md)
* [Samoobsługowe zarządzanie grupami](active-directory-accessmanagement-self-service-group-management.md)
* [Program Azure AD Connect health](active-directory-aadconnect-health.md)
* [Uwierzytelnianie wieloskładnikowe platformy Azure](../multi-factor-authentication/multi-factor-authentication.md)
* [Bezpośrednie zakupu licencji Azure AD Premium](http://aka.ms/buyaadp)
