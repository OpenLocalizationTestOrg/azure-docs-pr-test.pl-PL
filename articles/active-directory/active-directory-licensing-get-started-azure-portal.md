---
title: "Rozpoczynanie pracy z Licencjonowanie w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak Azure Active Directory działa Licencjonowanie, jak rozpocząć pracę z najlepszymi rozwiązaniami"
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
ms.openlocfilehash: 6fa7cbbc452861870136482aa320d268e78fe3d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
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

Podobnie jak wiele innych usług Microsoft online services najbardziej Azure AD płatnej wersji są dostarczane za pośrednictwem uprawnień użytkownika, gdy znajdują się w usłudze Office 365, Microsoft Intune i Azure AD. W takich przypadkach zakupu usługi jest reprezentowany przez jedną lub kilka subskrypcji, a każda subskrypcja zawiera niektóre prepurchased licencji w dzierżawie. Uprawnienia użytkownika są realizowane za:

* Przypisywanie licencji. 
* Utworzenie łącza między użytkownikiem i produkt.
* Włączanie składników usługi dla użytkownika.
* Korzystanie z jednego z przedpłaty licencji.

[Wypróbuj teraz usługi Azure AD Premium.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

Zawiera ogólne omówienie możliwości usługi Azure AD dla [co to jest usługa Azure AD?](active-directory-whatis.md). Aby uzyskać więcej informacji, zobacz nasze [strony umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/active-directory/v1_0/).

> [!NOTE]
> Z subskrypcji platformy Azure umożliwiają tworzenie zasobów Azure i zamapowania ich formy płatności. Nie ma żadnych liczby licencji skojarzone z subskrypcją. Przyznaj użytkownikowi uprawnienia do działania na zasobów platformy Azure są mapowane do subskrypcji, są skojarzone z subskrypcją i mogą zarządzać zasobami subskrypcji.

## <a name="how-does-azure-active-directory-licensing-work"></a>Jak działa Licencjonowanie usługi Azure Active Directory?

Na podstawie licencji usługi Azure AD usług pracy przez aktywowania subskrypcji w dzierżawie usługi Azure AD. Po subskrypcja jest aktywna, możliwości usługi są zarządzane przez administratorów usługi Azure AD i używane przez licencjonowanych użytkowników.

### <a name="manage-subscription-information"></a>Zarządzanie informacjami o subskrypcji

Po zakupie pakietu Enterprise Mobility + Security, Azure AD Premium lub Azure AD podstawowa dzierżawy jest aktualizowana subskrypcji, takie jak jego okresu ważności i przedpłaty licencji. Informacje o Twojej subskrypcji, wraz z liczbą przydzielonych lub dostępnych licencji, jest dostępna za pośrednictwem portalu Azure: w obszarze **usługi Azure Active Directory**, otwórz **licencji** kafelka dla określonego katalogu. **Licencji** bloku jest również najlepszym miejscem, aby zarządzać przypisaniami licencji.

Każda subskrypcja składa się z co najmniej jeden planów usług, takich jak Azure AD, uwierzytelnianie wieloskładnikowe, Intune, usługi Exchange Online lub SharePoint Online.  Zarządzanie licencjami usługi Azure AD jest *nie* wymaga poziomu planu usług zarządzania. Usługi Office 365 różni się, ponieważ opiera się na ten tryb konfiguracji zaawansowanej, aby zarządzać dostępem do usług uwzględnione. Usługi Azure AD zależy od użytkowanego konfigurację, aby włączyć funkcje i zarządzanie nimi indywidualnych uprawnień.

> [!IMPORTANT]
> Usługi Azure AD Premium, Azure AD podstawowa i Enterprise Mobility + Security subskrypcje są ograniczone do ich elastycznie katalogu/dzierżawców. Subskrypcji nie można podzielić między katalogami lub umożliwia uprawniają użytkowników w innych katalogach. Przenoszenie subskrypcji między katalogami jest możliwe, ale wymaga przesłanie biletu pomocy technicznej lub anulowanie i odkupu dla bezpośrednie zakupów.
>
> Gdy usługi Azure AD lub pakietu Enterprise Mobility + Security jest zakupione w ramach subskrypcji usługi licencjonowania zbiorowego, a gdy Umowa obejmuje innych usług Online firmy Microsoft (na przykład usługi Office 365), aktywacja odbywa się automatycznie. 

### <a name="assign-licenses"></a>Przypisywanie licencji

Uzyskiwanie subskrypcji ma wszystkie informacje wymagane do konfigurowania płatnej możliwości, ale nadal należy rozesłać licencji dla usługi Azure AD płatnej funkcji dla użytkowników. Każdy użytkownik, który muszą mieć dostęp do lub który odbywa się za pośrednictwem usługi Azure AD płatnej funkcji należy przypisać licencję. Przypisanie licencji jest mapowanie między użytkownikiem i zakupionych usług, takich jak Azure AD Premium, Basic lub pakietu Enterprise Mobility + Security.


Zarządzanie, którzy użytkownicy w katalogu powinien mieć licencję można osiągnąć przez: 

* Przypisywanie licencji do grup w [portalu Azure](active-directory-licensing-whatis-azure-portal.md).
* Przypisywanie licencji bezpośrednio do użytkowników za pomocą portalu, programu PowerShell lub interfejsów API. 

W przypadku przypisywania licencji do grupy, wszyscy członkowie grupy przypisanych licencji. Jeśli użytkownicy są dodawane lub usuwane z grupy, odpowiednie licencji jest przypisany lub usunięty. Przypisanie do grupy mogą wykorzystywać wszystkie dostępne i umożliwiają zarządzanie grupami i jest ona zgodna z grupy przypisywania do aplikacji.

Można użyć [przypisanie licencji na podstawie grupy](active-directory-licensing-whatis-azure-portal.md) do konfigurowania reguł, takich jak następujące:
* Wszyscy użytkownicy w katalogu automatycznie otrzymuje licencję
* Każdy z tytułem odpowiednie zadanie pobiera licencji
* Możesz delegować decyzja o innych menedżerów w organizacji (przy użyciu [grup samoobsługi](active-directory-accessmanagement-self-service-group-management.md))

Szczegółowe omówienie przypisania licencji do grup, zobacz zaawansowanych scenariuszy i usługi Office 365 licencjonowania scenariuszy, w tym [przypisać licencje do użytkowników na podstawie członkostwa w grupie w usłudze Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="get-started-with-azure-ad-licensing"></a>Rozpoczynanie pracy z licencją Azure AD

Wprowadzenie do korzystania z usługi Azure AD jest bardzo proste. Zawsze można utworzyć katalogu jako część skorzystania [Azure bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p/).

Następujące najlepsze rozwiązania pozwala zagwarantować, że dzierżawy jest zgodne z innymi usługami firmy Microsoft, które mogą korzystać i cele usługi:

- Jeśli korzystasz już z organizacyjnej usług firmy Microsoft, masz już dzierżawę usługi Azure AD. Warto użyć tej samej dzierżawy dla innych usług, umożliwiając zarządzanie tożsamościami core, w tym inicjowania obsługi administracyjnej i hybrydowych rejestracji jednokrotnej (SSO), można używać w usługach. Z logowania jednokrotnego użytkownikom korzystać z zaawansowanych funkcji w usługach. Jeśli zdecydujesz się kupić subskrypcję usługi Azure AD płatnej usługi dla pracowników, firma Microsoft zaleca w związku z tym ponownie użyć tej samej dzierżawy.

- Firma Microsoft zaleca, użyj nowej dzierżawy w portalu Azure, jeśli jest planowane:
  - Użyj usługi Azure AD na inny zestaw użytkowników (takich jak partnerów lub klientów).
  - Oceny usługi Azure AD w izolacji od usługi produkcji.
  - Konfigurowanie środowiska izolowanego dla usług.

  Nowy katalog jest tworzona przy użyciu konta jako użytkownik zewnętrzny z uprawnieniami administratora globalnego. Po zalogowaniu się do portalu Azure w odniesieniu do tego konta, możesz wyświetlić tej dzierżawy i dostęp do wszystkich zadań administracyjnych.

> [!NOTE]
> Usługi Azure AD obsługuje gościa "Użytkownicy", które konta użytkowników w dzierżawie usługi Azure AD, które zostały utworzone za pomocą konta Microsoft lub tożsamości usługi Azure AD z innego dzierżawcę. Portalu administracyjnego usługi Office 365 nie obsługuje obecnie tych użytkowników. Gości z konta Microsoft nie będą mogli uzyskać dostępu do portalu administracyjnego usługi Office 365, podczas gości z innymi dzierżawcami usługi Azure AD są ignorowane. W drugim przypadku tylko lokalne konto użytkownika, w usłudze Azure AD lub dzierżawy usługi Office 365, której użytkownik został pierwotnie utworzony, nie jest dostępna.

### <a name="select-one-or-more-license-trials"></a>Wybierz co najmniej jeden prób licencji

Można aktywować usługi Azure AD Premium lub pakietu Enterprise Mobility + zabezpieczeń subskrypcji wersji próbnej w obszarze **usługi Azure Active Directory** &gt; **szybki start**.

![Wybierz z wersji próbnej licencji](media/active-directory-licensing-get-started-azure-portal/select-a-license-trial.png)

Są dostępne w wersji próbnej licencji **licencji** bloku.

### <a name="assign-licenses-to-users-and-groups"></a>Przypisywanie licencji do użytkowników i grup

Po subskrypcja jest aktywna, należy przypisać licencję do siebie. Następnie odśwież przeglądarkę, aby upewnić się, że pojawia się do wszystkich funkcji. Następnym krokiem jest, aby przypisać licencje do użytkowników, którzy potrzebują dostępu do płatnej funkcje usługi Azure AD. Zgodnie z opisem w [przypisać licencje](#assign-licenses), co jest prosty sposób na przypisywanie licencji do identyfikowania grupy reprezentująca odbiorców i przypisać licencję do niego. W ten sposób użytkownicy, którzy są dodawane lub usuwane z grupy jego cyklem zostały przypisane lub usunięte z licencji, odpowiednio.

> [!NOTE]
> Pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach. Zanim można przypisać licencję do użytkownika, administrator musi określić **lokalizacji użytkowania** właściwości dla użytkownika. Można ustawić tę właściwość w obszarze **użytkownika** &gt; **profilu** &gt; **ustawienia** w portalu Azure. Używając przypisanie do grupy licencji, każdy użytkownik nie określono lokalizacji użytkowania, której dziedziczy lokalizację katalogu.

Aby przypisać licencję, w obszarze **usługi Azure Active Directory** &gt; **licencji** &gt; **wszystkie produkty**, wybierz jeden lub więcej produktów, a następnie wybierz **przypisać** na pasku poleceń.

![Wybierz licencji do przypisania](media/active-directory-licensing-get-started-azure-portal/select-license-to-assign.png)

Można użyć **użytkowników i grup** bloku, aby wybrać wielu użytkowników lub grup lub wyłącz planów usług w ramach produktu. Użyj pola wyszukiwania w górnej części do wyszukania nazwy użytkowników i grup.

![Wybierz użytkownika lub grupy do przypisania licencji](media/active-directory-licensing-get-started-azure-portal/select-user-for-license-assignment.png)

W przypadku przypisywania licencji do grupy, może upłynąć pewien czas, zanim wszyscy użytkownicy dziedziczą licencji, w zależności od liczby użytkowników w grupie. Można sprawdzić stan przetwarzania na **grupy** bloku, w obszarze **licencji** kafelka.

![Stan przypisania licencji](media/active-directory-licensing-get-started-azure-portal/license-assignment-status.png)

Przypisanie błędy mogą wystąpić podczas przypisanie licencji usługi Azure AD, ale są stosunkowo rzadko podczas zarządzania usługi Azure AD i Enterprise Mobility + Security produktów. Potencjalne błędy przydziału są ograniczone do:
- Konflikt przypisania: gdy użytkownik został już wcześniej przypisany licencji, która jest niezgodna z bieżącej licencji. W takim przypadku Przypisywanie nowej licencji wymaga usunięcia bieżącego.
- Przekroczono dostępnych licencji: gdy liczbę użytkowników w grupach przypisanej przekracza dostępne licencje, stan przypisania użytkownika odzwierciedla awarii można przypisać ze względu na Brak licencji.

#### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure licencjonowania współpracy B2B usługi AD

Współpraca B2B umożliwia zaprosić użytkowników gościa do dzierżawy usługi Azure AD w celu zapewnienia dostępu do usługi Azure AD i dowolnych zasobów platformy Azure mają być dostępne.  

Jest bezpłatna dla zapraszanie B2B użytkowników i przypisywanie ich do aplikacji w usłudze Azure AD. Do 10 aplikacji według użytkownika gościa i 3 podstawowe raporty są także bezpłatna dla użytkowników współpracy B2B. Jeśli użytkownika gościa zawiera wszystkie odpowiednie licencje przypisane w dzierżawie usługi Azure AD partnera, będą one licencjonowane w należy do Ciebie również.

Nie jest to wymagane, ale jeśli chcesz zapewnić dostęp do płatnej funkcje usługi Azure AD, muszą mieć licencję tych gości B2B z odpowiednimi licencjami usługi Azure AD. Zapraszanie dzierżawcy z usługą Azure AD, płatną licencję współpracy B2B prawa użytkownika można przypisać dodatkowym użytkownikom pięć gościa zaproszenie do dzierżawy. Scenariusze i informacje, zobacz [współpracy B2B licencjonowania wskazówki](active-directory-b2b-licensing.md).

### <a name="view-assigned-licenses"></a>Wyświetl przypisane licencje

Widok podsumowania przypisane i dostępnych licencji zostanie wyświetlona w obszarze **usługi Azure Active Directory** &gt; **licencji** &gt; **wszystkie produkty**.

![Licencja wyświetlania podsumowania](media/active-directory-licensing-get-started-azure-portal/view-license-summary.png)

Szczegółową listę przypisanych użytkowników i grup jest dostępna po wybraniu określonego produktu. **Licencjonowanych użytkowników** lista zawiera wszystkich użytkowników, w obecnie korzystających z licencji i czy została przypisana licencja bezpośrednio do użytkownika lub jeśli zostało ono odziedziczone po grupie.

![Wyświetl szczegóły licencji](media/active-directory-licensing-get-started-azure-portal/view-license-detail.png)

Podobnie **grup licencji** lista zawiera wszystkich grup, do których zostały przypisane licencje. Wybierz użytkownika lub grupę, aby otworzyć **licencji** bloku, który zawiera wszystkie licencje przypisane do tego obiektu.

### <a name="remove-a-license"></a>Usunąć licencję

Aby usunąć licencję, przejdź do użytkownika lub grupy, a następnie otwórz **licencji** kafelka. Wybierz licencji, a następnie kliknij przycisk **Usuń**.

![Usunąć licencję](media/active-directory-licensing-get-started-azure-portal/remove-license.png)

Nie można bezpośrednio usunąć dziedziczone przez użytkownika z grupy licencji. Zamiast tego Usuń użytkownika z grupy, z którego są dziedziczone licencji.

### <a name="extend-trials"></a>Rozszerzenie wersji próbnych

Wersja próbna rozszerzenia dla klientów są dostępne jako samoobsługowego tworzenia konta za pośrednictwem portalu usługi Office 365. Administrator klienta można przejść do portalu usługi Office (dostępu zależy od uprawnień do portalu usługi Office) i wybierz wersję próbną usługi Azure AD Premium. Kliknięcie przycisku **przedłużyć okres próbny** łącze spowoduje uruchomienie procesu rozszerzenia. Karty kredytowej jest wymagany, ale nie jest pobierana.

![Przedłużyć okres próbny w portalu Azure](media/active-directory-licensing-get-started-azure-portal/extend-trial-beginning.png)

## <a name="next-steps"></a>Następne kroki

Aby dowiedzieć się więcej o zaawansowanych scenariuszy zarządzania licencji za pomocą grup, przeczytaj artykuł na temat [przypisywaniu licencji do grupy](active-directory-licensing-group-assignment-azure-portal.md).

Poniżej przedstawiono informacje o konfigurowaniu i korzystanie z innych funkcji Azure AD płatnej:

* [Samoobsługowe Resetowanie hasła](active-directory-manage-passwords.md)
* [Samoobsługowe zarządzanie grupami](active-directory-accessmanagement-self-service-group-management.md)
* [Program Azure AD Connect health](active-directory-aadconnect-health.md)
* [Uwierzytelnianie wieloskładnikowe platformy Azure](../multi-factor-authentication/multi-factor-authentication.md)
* [Bezpośrednie zakupu licencji Azure AD Premium](http://aka.ms/buyaadp)
