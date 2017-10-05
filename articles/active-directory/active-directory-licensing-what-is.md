---
title: "Licencji użytkowników usługi Azure Active Directory w klasycznym portalu Azure | Dokumentacja firmy Microsoft"
description: "Opis licencjonowania usługi Microsoft Azure Active Directory, jak to działa, jak rozpocząć pracę i najlepszych rozwiązań, w tym usługi Office 365, Microsoft Intune i Azure Active Directory Premium i podstawowa wersje"
services: active-directory
keywords: "Licencjonowanie usługi Azure AD"
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d769e8c6-7581-43f5-a3b4-de4b1dca2344
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;H1Hack27Feb2017
ms.openlocfilehash: 9da5bb6987a9eb3398abe0d6066f1945620df9a4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-the-azure-classic-portal"></a>Co to jest Microsoft Azure Active Directory licencjonowania w klasycznym portalu Azure?

> [!div class="op_single_selector"]
> * [Pobierz instrukcje portalu Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Azure classic informacji portalu](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) jest tożsamość firmy Microsoft jako rozwiązanie Service (IDaaS) i platforma. Usługi Azure AD jest oferowany na kilka różnych wersji funkcjonalności i technicznych od wolne Azure AD, która jest dostępna w usłudze firmy Microsoft, takich jak usługi Office 365, Dynamics, Microsoft Intune i Azure (Azure AD nie generuje żadnych opłat za zużycie w tym trybie), do Azure Multi-Factor Authentication (MFA), a także wersje, takie jak Enterprise Mobility Suite (EMS), Azure AD Premium i podstawowe płatne Azure AD. Podobnie jak wiele innych usług Microsoft online services najbardziej Azure AD płatnej wersji są dostarczane za pośrednictwem uprawnień użytkownika, gdy znajdują się w usłudze Office 365, Microsoft Intune i Azure AD. W takich przypadkach zakupu usługi jest reprezentowana z jedną lub kilka subskrypcji, a każda subskrypcja zawiera wstępne zakupu liczbę licencji w dzierżawie. Uprawnienia użytkownika, uzyskuje się poprzez przypisanie licencji, tworzenie łącza między użytkownikiem i produktu, włączenie składniki usługi dla użytkownika, a korzystanie z jednego z przedpłaty licencji.

> [!IMPORTANT]
> Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule. Do przypisywania ról administratora w Centrum administracyjnym usługi Azure AD, zobacz [licencji użytkownika, jak i użytkowników w usłudze Azure AD](active-directory-licensing-get-started-azure-portal.md).

[Wypróbuj usługę Azure AD premium.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Portalu administracyjnego usługi Azure AD jest częścią klasycznego portalu Azure. Podczas gdy przy użyciu usługi Azure AD nie wymagają żadnych Azure zakupów, uzyskiwanie dostępu do tego portalu wymaga aktywną subskrypcją platformy Azure lub [subskrypcji wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

Zawiera ogólne omówienie możliwości usługi Azure AD dla [co to jest usługa Azure AD](active-directory-whatis.md).
[Dowiedz się więcej na temat poziomów usług Azure AD](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Subskrypcje platformy Azure płatności zgodnie z rzeczywistym są różne: podczas również reprezentowane w katalogu, te subskrypcje umożliwiają tworzenie zasobów Azure i zamapowania ich na formy płatności. W tym przypadku są nie liczby licencji skojarzone z subskrypcją. Skojarzeń użytkowników z subskrypcją dostęp użytkowników do zarządzania zasobami subskrypcji, uzyskuje się poprzez przyznania im uprawnień do działania na zasobów platformy Azure są mapowane do subskrypcji.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Jak działa Licencjonowanie usługi Azure AD?
(W oparciu o uprawnieniach) na podstawie licencji usługi Azure AD usług pracy przez aktywowania subskrypcji w dzierżawie usługi katalogowej/usługi Azure AD. Gdy subskrypcja jest aktywna możliwości usługi można zarządzane przez administratorów usługi katalogowej/i używane przez licencjonowanych użytkowników.

Katalog materiałów szkoleniowych Enterprise Mobility Suite, Azure AD Premium lub usługi Azure AD podstawowa, zostaje zaktualizowany z subskrypcją, w tym jego okresu ważności i przedpłaty licencji. Informacje o Twojej subskrypcji, w tym stan, następne zdarzenie cyklu życia i liczbę licencji przypisanych lub dostępna jest dostępna za pośrednictwem klasycznego portalu Azure na karcie licencji dla określonego katalogu. Dotyczy to również najlepszym miejscem, aby zarządzać przypisaniami licencji.

Każda subskrypcja składa się z co najmniej jeden plan usługi każdego mapowania dołączone poziom funkcjonalności usługi typu; na przykład usługi Azure AD, Azure MFA, Microsoft Intune, usługi Exchange Online lub SharePoint Online. Zarządzanie licencjami usługi Azure AD nie wymaga zarządzania poziomem usługi planu. Różni się to od usługi Office 365, która opiera się na ten tryb konfiguracji zaawansowanej, aby zarządzać dostępem do usług uwzględnione. W konfiguracji usługi, aby włączyć funkcje i zarządzać nimi indywidualnych uprawnień zależy od usługi Azure AD.

Ogólnie rzecz biorąc informacji o subskrypcji usługi Azure AD jest zarządzana za pośrednictwem klasycznego portalu Azure, na karcie licencji dla określonego katalogu. Subskrypcje platformy Azure AD, z wyjątkiem usługi Azure AD Premium, nie są wyświetlane w portalu usługi Office.

> [!IMPORTANT]
> Azure AD Premium i Basic, a także subskrypcji pakietu Enterprise Mobility Suite, są ograniczone do ich elastycznie katalogu/dzierżawy. Subskrypcji nie można podzielić między katalogami lub umożliwia uprawniają użytkowników w innych katalogach. Przenoszenie subskrypcji między katalogami jest możliwe, ale wymaga przesłanie biletu pomocy technicznej lub anulowania i ponownego zakupu w przypadku bezpośrednich zakupów.
>
> Przy zakupie usługi Azure AD lub pakietu Enterprise Mobility Suite za pośrednictwem licencjonowania zbiorowego aktywacji subskrypcji nastąpi automatycznie, gdy Umowa obejmuje innych usług Online firmy Microsoft, np. Office 365.
>
>

Płatnej usługi Azure AD funkcji span szerokość katalogu. Przykłady:

* Na podstawie grupy przypisywania do aplikacji, która jest włączona w obszarze określonej aplikacji, którym zarządzasz.
* Zaawansowane i możliwości zarządzania grupami samoobsługi dostępnych w obszarze Konfiguracja katalogu lub określonej grupy.
* Raporty dotyczące zabezpieczeń w warstwie Premium są na karcie raportowanie
* Rozwiązanie cloud discovery aplikacji zostaną wyświetlone w portalu Azure w ramach tożsamości.

### <a name="assigning-licenses"></a>Przypisywanie licencji
Podczas uzyskiwania subskrypcji jest wszystkie informacje wymagane do konfigurowania płatnej możliwości, za pomocą usługi Azure AD płatnej funkcji wymaga dystrybucji licencji do prawej osób. Ogólnie rzecz biorąc każdy użytkownik, który muszą mieć dostęp do lub który odbywa się za pośrednictwem usługi Azure AD płatnej funkcji należy przypisać licencję. Przypisanie licencji jest mapowanie między użytkownikiem i zakupionych usług, takich jak Azure AD Premium, podstawowa lub pakietu Enterprise Mobility Suite.

Zarządzanie, którzy użytkownicy w katalogu powinien mieć licencję jest proste. Można wykonywać, przez przypisanie do grupy można utworzyć przypisania zasady przy użyciu portalu administracyjnego usługi Azure AD lub przypisywaniu licencji bezpośrednio do prawej fizycznych za pośrednictwem portalu, programu PowerShell lub interfejsów API. Podczas przypisywania licencji do grupy, wszyscy członkowie grupy będą przypisanej licencji. Jeśli użytkownicy są dodawane lub usuwane z grupy, będzie można przypisać lub usunąć odpowiednią licencję. Przypisanie do grupy mogą wykorzystywać wszystkie dostępne i umożliwiają zarządzanie grupami i jest zgodny z grupy przypisywania do aplikacji. W ten sposób można Ustaw reguły w taki sposób, że wszyscy użytkownicy w katalogu są automatycznie przypisywane, upewnij się, że wszyscy z tytułem odpowiednie zadanie ma licencję lub nawet delegować decyzja o innych menedżerów w organizacji.

Za pomocą przypisania na podstawie grupy licencji każdy użytkownik, Brak lokalizacji użytkowania będzie dziedziczyć na lokalizację katalogu podczas przypisywania. Tej lokalizacji można zmienić w dowolnym momencie przez administratora. W przypadkach, w których automatycznego przypisania nie powiodło się z powodu błędu informacje o użytkowniku w obszarze typu licencji odpowiada tego stanu.

## <a name="getting-started-with-azure-ad-licensing"></a>Wprowadzenie do licencjonowania usługi Azure AD
Wprowadzenie do korzystania z usługi Azure AD jest proste. zawsze można utworzyć katalogu w ramach konta do bezpłatnej wersji próbnej platformy Azure. [Dowiedz się więcej o rejestracji jako organizacja](sign-up-organization.md). Następujące czynności mogą pomóc upewnij się, że katalog najlepiej jest zgodne z innych usług firmy Microsoft mogą korzystać z lub planowane jest użycie i cele w uzyskaniu usługi.

Poniżej przedstawiono kilka najlepszych rozwiązań:

* Jeśli korzystasz już z organizacyjnej usług firmy Microsoft, masz już katalog usługi Azure AD. W takim przypadku można nadal używał tego samego katalogu dla innych usług, umożliwiając zarządzanie identity core, w tym inicjowania obsługi administracyjnej oraz w hybrydowych logowania jednokrotnego, mogą zostać użyte przez usługi. Użytkownicy będą mieli środowisko logowania jednokrotnego i będą korzystać z bardziej rozbudowane możliwości w usługach. Jeśli zdecydujesz się kupić subskrypcję usługi Azure AD płatnej usługi dla pracowników, firma Microsoft zaleca w związku z tym używany ten sam katalog w tym celu.
* Jeśli planujesz używać usługi Azure AD na inny zestaw użytkowników (partnerów, klientów i tak dalej), lub jeśli chcesz ocenić usługi Azure AD, a chcesz to zrobić w izolacji usługi produkcji lub jeśli chcesz skonfigurować środowisko piaskownicy y naszych usług, firma Microsoft zaleca, najpierw utwórz nowy katalog za pośrednictwem klasycznego portalu Azure, Azure. [Dowiedz się więcej na temat tworzenia nowego katalogu usługi Azure AD w klasycznym portalu Azure](active-directory-licensing-directory-independence.md). Nowy katalog zostanie utworzona przy użyciu konta jako użytkownik zewnętrzny z uprawnieniami administratora globalnego. Po zalogowaniu się do klasycznego portalu Azure z tym kontem, można wyświetlić tego katalogu i dostęp do wszystkich zadań administracyjnych w katalogu. Firma Microsoft zaleca, Utwórz konto lokalne z odpowiednimi uprawnieniami do zarządzania innymi usługami firmy Microsoft, (te nie jest dostępna za pośrednictwem klasycznego portalu Azure). [Dowiedz się więcej na temat tworzenia kont użytkowników w usłudze Azure AD](active-directory-create-users.md).

> [!NOTE]
> Usługi Azure AD obsługuje "użytkowników zewnętrznych", które są konta użytkowników w wystąpieniu usługi Azure AD, które zostały utworzone przy użyciu konta Microsoft (MSA) lub tożsamości usługi Azure AD z innego katalogu. Są nam zajęty rozszerzanie tej możliwości do wszystkich usług firmy Microsoft w organizacji, teraz te konta nie są obsługiwane w niektórych usług doświadczeń; na przykład portalu administracyjnego usługi Office 365 aktualnie nie obsługuje tych użytkowników. W związku z tym użytkownicy zewnętrzni z konta Microsoft nie będzie na dostęp do portalu administracyjnego usługi Office 365, gdy użytkownicy zewnętrzni z innych katalogów usługi Azure AD zostaną zignorowane. W drugim przypadku tylko lokalne konto użytkownika, programu Azure AD lub katalogu usługi Office 365, w której użytkownik został pierwotnie utworzony, będą dostępne za pośrednictwem funkcji.
>
>

Jak wskazano, usługa Azure AD ma różne wersje płatną. Te wersje są niektóre niewielkie różnice w ich dostępności zakupu:

| Product (Produkt) | UMOWA EA/LICENCJONOWANIA ZBIOROWEGO | Otwarty | CSP | Prawa do używania MPN | Bezpośrednie zakupu | Wersja próbna |
| --- | --- | --- | --- | --- | --- | --- |
| Pakiet Enterprise Mobility Suite |X |X |X |X | |X |
| Usługa Azure AD — wersja Premium |X |X |X | |X |X |
| Azure AD podstawowa |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Wybierz co najmniej jeden prób licencji
 We wszystkich przypadkach możesz aktywować subskrypcję wersji próbnej usługi Azure AD Premium lub pakietu Enterprise Mobility Suite przez wybranie określonych wersji próbnej, wybrany na karcie licencji w katalogu. Każda wersja próbna zawiera subskrypcji 30-dniowej ze 100 licencji.

![Planów licencja próbna usługi Azure Active Directory](./media/active-directory-licensing-what-is/trial_plans.png)

![Plany licencjonowania wersji próbnej pakietu Enterprise Mobility Suite](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Licencja próbna aktywnych planów](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Przypisywanie licencji
Gdy subskrypcja jest aktywna, należy przypisać licencję do siebie i Odśwież przeglądarkę, aby upewnić się, że jest wyświetlany, wszystkie funkcje. Następnym krokiem jest, aby przypisać licencje do użytkowników, którzy będą musieli dostępu lub zostać uwzględnione w płatną funkcje usługi Azure AD. Jak wspomniano powyżej w "Przypisywanie licencji" najlepszym sposobem, w tym celu jest identyfikator grupy reprezentująca odbiorców i przypisz je do licencji; w ten sposób użytkownicy, którzy są dodawane lub usuwane z grupy jego cyklem zostaną przypisane do lub usunięte z licencji.

Aby przypisać licencję do grupy lub poszczególnych użytkowników, wybierz plan licencji chcesz przypisać i kliknij przycisk **przypisać** na pasku poleceń.

![Licencja próbna aktywnych planów](./media/active-directory-licensing-what-is/assign_licenses.png)

Gdy w oknie dialogowym przydział dla wybranego planu, można wybrać użytkowników i dodanie ich do **przypisać** kolumnę po prawej stronie. Można strony za pomocą listy użytkownika lub Wyszukaj szkła konkretne osoby za pomocą wyszukiwania w górnej części prawej strony siatki użytkownika. Aby przypisać grupy, wybierz "Grupy" z **Pokaż** menu, a następnie kliknij przycisk wyboru po prawej stronie, aby odświeżyć przydziałów, które są wyświetlane.

![Przypisywanie licencji do grup](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

Teraz można przeszukiwać lub strony przy użyciu grup i dodaj je do **przypisać** kolumny w taki sam sposób. Służy to do przypisywania kombinację użytkowników i grup w ramach jednej operacji. Aby dokończyć przypisanie, kliknij przycisk wyboru w prawym dolnym rogu strony.

![Wiadomość o postępie przypisania licencji](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Po przypisaniu grupy jej elementów członkowskich dziedziczą licencji w ciągu 30 minut, ale zazwyczaj w ciągu 1 – 2 minuty.

Przypisanie błędy mogą wystąpić podczas przypisanie licencji usługi Azure AD, ale są stosunkowo rzadko. Potencjalne błędy przydziału są ograniczone do:

* Konflikt przypisania — Jeśli użytkownik został już wcześniej przypisany licencji, która jest niezgodna z bieżącej licencji. W takim przypadku przypisanie nowej licencji wymaga usunięcia poprzedniego.
* Przekroczono dostępnych licencji — dostępnych licencji, przekracza liczbę użytkowników w grupach przypisany stan przypisania użytkowników zostaną one zastosowane awarii można przypisać ze względu na Brak licencji.

### <a name="view-assigned-licenses"></a>Wyświetl przypisane licencje
Widok podsumowania przypisane licencje zdarzeń cyklu życia subskrypcji dostępne przypisanej i dalej w tym są wyświetlane na **licencji** kartę.

![Wskazuje liczbę przypisane licencje](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Szczegółową listę przypisanych użytkowników i grup, w tym stan przypisania i ścieżki (bezpośrednio lub dziedziczone z co najmniej jedną grupę) jest dostępna podczas nawigowania do planu licencjonowania.

![Wyświetlanie szczegółów licencji przypisanych do planu licencjonowania](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

Usuwanie licencji jest tak proste, jak przypisywania do nich. Jeśli bezpośrednio są przypisane do użytkownika lub grupy przypisanej licencji można usunąć, wybierając typ licencji, wybranie opcji **Usuń**, Dodawanie użytkownika lub grupę do listy Usuń i potwierdzenie akcji. Alternatywnie można Otwórz typ licencji, wybierz określonego użytkownika lub grupy i wybierz **Usuń** na pasku poleceń. Aby zakończyć dziedziczenie użytkownika z grupy licencji, po prostu usuń użytkownika z grupy.

### <a name="extending-trials"></a>Rozszerzanie prób
Wersja próbna rozszerzenia dla klientów są dostępne jako samoobsługowego portalu usługi Office 365. Administrator klienta można przejść do [portalu Office](https://portal.office.com/#Billing) (dostępu zależy od uprawnień do portalu usługi Office) i wybierz wersję próbną usługi Azure AD Premium. Kliknij przycisk **przedłużyć okres próbny** łącze i postępuj zgodnie z instrukcjami. Musisz wprowadzić karty kredytowej, ale nie zostanie obciążona.

![Rozszerzenie wersji próbnej licencji w portalu usługi Office](./media/active-directory-licensing-what-is/extend_license_trial.png)

Klientów można również poprosić o przedłużenie okresu próbnego po przesłaniu żądania pomocy technicznej. Administrator klienta można przejść do portalu usługi Office 365 [strony pomocy technicznej](http://aka.ms/extendAADtrial) (dostępu zależy od uprawnień dla strony Obsługa pakietu Office). Na tej stronie wybierz pozycję "Subskrypcje i wersji próbnych" w funkcji i "Wersja próbna pytań" w obszarze objaw. Na koniec wprowadź informacje na temat okoliczności

![Rozszerzenie wersji próbnej licencji przy użyciu żądania obsługi](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Następne kroki
Można teraz gotowe do skonfigurowania i korzystać z niektórych funkcji Azure AD Premium.

* [Samoobsługowe Resetowanie hasła](active-directory-manage-passwords.md)
* [Samoobsługowe zarządzanie grupami](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect kondycji](active-directory-aadconnect-health.md)
* [Przypisanie do grupy aplikacji](active-directory-manage-groups.md)
* [Uwierzytelnianie wieloskładnikowe platformy Azure](../multi-factor-authentication/multi-factor-authentication.md)
* [Bezpośrednie zakupu licencji Azure AD Premium](http://aka.ms/buyaadp)
