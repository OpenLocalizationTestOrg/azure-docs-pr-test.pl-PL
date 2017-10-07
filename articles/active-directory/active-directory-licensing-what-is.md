---
title: "Użytkownicy usługi Azure Active Directory aaaLicense hello klasycznego portalu Azure | Dokumentacja firmy Microsoft"
description: "Opis licencjonowania usługi Microsoft Azure Active Directory, jak to działa, sposób uruchamiania tooget i najlepszych rozwiązań, w tym usługi Office 365, Microsoft Intune i Azure Active Directory Premium i podstawowa wersje"
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
ms.openlocfilehash: 4d5f244cbee2ae37a30976f70b5d4f21c3516d90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-microsoft-azure-active-directory-licensing-in-hello-azure-classic-portal"></a>Co to jest Microsoft Azure Active Directory licencjonowania w hello klasycznego portalu Azure?

> [!div class="op_single_selector"]
> * [Pobierz instrukcje portalu Azure](active-directory-licensing-get-started-azure-portal.md)
> * [Azure classic informacji portalu](active-directory-licensing-what-is.md)
>
>

Azure Active Directory (Azure AD) jest tożsamość firmy Microsoft jako rozwiązanie Service (IDaaS) i platforma. Usługi Azure AD jest oferowany na kilka różnych wersji funkcjonalności i technicznych od wolne Azure AD, która jest dostępna w usłudze firmy Microsoft, takich jak usługi Office 365, Dynamics, Microsoft Intune i Azure (Azure AD nie generuje żadnych opłat za zużycie w tym trybie,) tooAzure AD płatnej usługi Azure Multi-Factor Authentication (MFA), a także wersje, takie jak Enterprise Mobility Suite (EMS), Azure AD Premium i Basic. Podobnie jak wiele innych usług Microsoft online services najbardziej Azure AD płatnej wersji są dostarczane za pośrednictwem uprawnień użytkownika, gdy znajdują się w usłudze Office 365, Microsoft Intune i Azure AD. W takich przypadkach zakupu usługi hello jest reprezentowana z jedną lub kilka subskrypcji, a każda subskrypcja zawiera wstępne zakupu liczbę licencji w dzierżawie. Uprawnienia użytkownika, uzyskuje się poprzez przypisanie licencji, tworzenia łącza użytkownika hello i hello produktu, włączanie hello składników usługi dla użytkownika hello i korzystanie z jednego z hello Przedpłata licencji.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Aby uzyskać jak tooassign ról administratorów w usłudze Azure AD Witaj, Administratorze Centrum, zobacz [licencji użytkownika, jak i użytkowników w usłudze Azure AD](active-directory-licensing-get-started-azure-portal.md).

[Wypróbuj usługę Azure AD premium.](https://portal.office.com/Signup/Signup.aspx?OfferId=01824d11-5ad8-447f-8523-666b0848b381&ali=1#0)

> [!NOTE]
> Portalu administracyjnego usługi Azure AD jest częścią hello klasycznego portalu Azure. Podczas gdy przy użyciu usługi Azure AD nie wymagają żadnych Azure zakupów, uzyskiwanie dostępu do tego portalu wymaga aktywną subskrypcją platformy Azure lub [subskrypcji wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

Zawiera ogólne omówienie możliwości usługi Azure AD dla [co to jest usługa Azure AD](active-directory-whatis.md).
[Dowiedz się więcej na temat poziomów usług Azure AD](https://azure.microsoft.com/support/legal/sla/)

> [!NOTE]
> Subskrypcje platformy Azure płatności zgodnie z rzeczywistym są różne: również reprezentowane w katalogu, te subskrypcje umożliwiają tworzenie zasobów Azure i zamapowania ich tooyour formy płatności. W tym przypadku są liczbami licencji, nie skojarzone z subskrypcją hello. Skojarzeń użytkowników z subskrypcją hello, hello użytkownicy uzyskują dostęp do zasobów subskrypcji toomanaging, uzyskuje się poprzez przyznania im toooperate uprawnienia subskrypcji toohello mapowane zasobów platformy Azure.
>
>

## <a name="how-does-azure-ad-licensing-work"></a>Jak działa Licencjonowanie usługi Azure AD?
(W oparciu o uprawnieniach) na podstawie licencji usługi Azure AD usług pracy przez aktywowania subskrypcji w dzierżawie usługi katalogowej/usługi Azure AD. Po hello subskrypcja jest aktywna hello możliwości usługi można zarządzane przez administratorów usługi katalogowej/i używane przez licencjonowanych użytkowników.

Gdy zakupu lub uaktywnianie Enterprise Mobility Suite, Azure AD Premium i Azure AD podstawowa, katalog jest aktualizowane hello subskrypcji, w tym okresie ważności i Przedpłata licencji. Informacje o Twojej subskrypcji, w tym stan, następne zdarzenie cyklu życia i hello liczbę licencji przypisanych lub dostępna jest dostępna za pośrednictwem hello klasycznego portalu Azure hello karcie licencji dla określonego katalogu hello. To jest również toomanage miejsce toobest przypisaniami licencji.

Każda subskrypcja składa się z co najmniej jeden plan usługi, każdy hello mapowania uwzględnione poziom funkcjonalności typu usługi hello; na przykład usługi Azure AD, Azure MFA, Microsoft Intune, usługi Exchange Online lub SharePoint Online. Zarządzanie licencjami usługi Azure AD nie wymaga zarządzania poziomem usługi planu. Różni się to od usługi Office 365, która zależy od tej usługi tooincluded konfiguracji zaawansowanej tryb toomanage dostępu. Usługi Azure AD zależy od w konfiguracji usługi, funkcji tooenable i zarządzaj nimi indywidualnych uprawnień.

Ogólnie rzecz biorąc informacji o subskrypcji usługi Azure AD jest zarządzana za pośrednictwem klasycznego portalu Azure hello karcie licencji dla określonego katalogu hello hello. Subskrypcje platformy Azure AD, z wyjątkiem hello Azure AD Premium nie są wyświetlane w portalu Office hello.

> [!IMPORTANT]
> Azure AD Premium i Basic, a także subskrypcji pakietu Enterprise Mobility Suite, są dzierżawy directory zamkniętej tootheir udostępniane. Nie można podzielić subskrypcje między katalogami lub użytkownicy tooentitle używane w innych katalogach. Przenoszenie subskrypcji między katalogami jest możliwe, ale wymaga przesłanie biletu pomocy technicznej lub anulowania i ponownego zakupu w przypadku hello bezpośrednich zakupów.
>
> Przy zakupie usługi Azure AD lub pakietu Enterprise Mobility Suite za pośrednictwem licencjonowania zbiorowego aktywacji subskrypcji nastąpi automatycznie, gdy Umowa hello obejmuje innych usług Online firmy Microsoft, np. Office 365.
>
>

Płatnej szerokość zakresu hello katalogu hello funkcje usługi Azure AD. Przykłady:

* Tooapplications przypisywania na podstawie grupy jest włączona w obszarze określonej aplikacji hello, którym zarządzasz.
* Zaawansowane i możliwości zarządzania grupami samoobsługi dostępnych w obszarze Konfiguracja katalogu hello lub hello określonej grupy.
* Raporty dotyczące zabezpieczeń w warstwie Premium są na karcie raportowanie hello
* Rozwiązanie cloud discovery aplikacji zostaną wyświetlone w hello portalu Azure w ramach tożsamości.

### <a name="assigning-licenses"></a>Przypisywanie licencji
Podczas uzyskiwania subskrypcji jest potrzebne wszystkie tooconfigure płatnej możliwości, za pomocą usługi Azure AD płatnej funkcji wymaga dystrybucja osób prawo toohello licencji. Ogólnie rzecz biorąc każdy użytkownik, który powinien mieć tooor dostępu, która jest zarządzana za pomocą usługi Azure AD płatnej funkcji należy przypisać licencję. Przypisanie licencji jest mapowanie między użytkownikiem i zakupionych usług, takich jak Azure AD Premium, podstawowa lub pakietu Enterprise Mobility Suite.

Zarządzanie, którzy użytkownicy w katalogu powinien mieć licencję jest proste. Można zrobić, przypisując toocreate grupy tooa przypisania zasady przy użyciu portalu administracyjnego usługi Azure AD hello lub bezpośrednio przypisać licencje toohello prawo fizycznych za pośrednictwem portalu, programu PowerShell lub interfejsów API. Podczas przypisywania licencji tooa grupy, wszyscy członkowie grupy będą przypisanej licencji. Jeśli użytkownicy są dodawane lub usuwane z grupy hello one odpowiednią licencję hello przypisanej lub usunięty. Przypisanie do grupy mogą korzystać z dowolnej grupy zarządzania dostępne tooyou i jest zgodny z tooapplications przypisywania na podstawie grupy. W ten sposób można Ustaw reguły w taki sposób, że wszyscy użytkownicy w katalogu są automatycznie przypisywane, sprawdź, czy wszyscy z odpowiednią hello stanowisko ma licencję lub nawet delegować hello decyzji tooother menedżerów w organizacji hello.

Za pomocą przypisania na podstawie grupy licencji każdy użytkownik, Brak lokalizacji użytkowania będzie dziedziczyć lokalizację katalogu hello podczas przypisywania. W dowolnym momencie przez administratora hello można zmienić tej lokalizacji. W przypadkach, gdy hello automatycznego przypisania nie powiodła z powodu tooerror, informacje o użytkowniku hello w obszarze czy typ licencji odpowiada tym stanie.

## <a name="getting-started-with-azure-ad-licensing"></a>Wprowadzenie do licencjonowania usługi Azure AD
Wprowadzenie do korzystania z usługi Azure AD jest proste. zawsze można utworzyć katalogu w ramach konta tooa podczas bezpłatna wersja próbna platformy Azure. [Dowiedz się więcej o rejestracji jako organizacja](sign-up-organization.md). Witaj poniżej mogą pomóc w upewnij się, że katalogu najlepiej jest zgodne z innymi usługami firmy Microsoft mogą korzystać z lub planowanych tooconsume i cele w uzyskaniu hello usługi.

Poniżej przedstawiono kilka najlepszych rozwiązań:

* Jeśli korzystasz już z organizacyjnej usług firmy Microsoft, masz już katalog usługi Azure AD. W takim przypadku należy kontynuować toouse hello tym samym katalogu dla innych usług, dzięki czemu zarządzanie identity core, w tym inicjowania obsługi administracyjnej oraz w hybrydowych logowania jednokrotnego, mogą zostać użyte w usługach hello. Użytkownicy będą mieli środowisko logowania jednokrotnego i będą korzystać z bardziej rozbudowane możliwości w usługach hello. W związku z tym Jeśli zdecydujesz się toobuy usługi Azure AD płatnej usługi dla pracowników, firma Microsoft zaleca się używanie tego samego katalogu toodo Witaj, to.
* Jeśli planujesz toouse usługi Azure AD na inny zestaw użytkowników (partnerów, klientów i tak dalej), lub jeśli chcesz usług tooevaluate usługi Azure AD i chcesz toodo w izolacji usługi produkcji, lub jeśli szukasz toosetup środowisko piaskownicy dla usług firma Microsoft zaleca, najpierw utwórz nowy katalog za pośrednictwem klasycznego portalu Azure, Azure hello. [Dowiedz się więcej na temat tworzenia nowego katalogu usługi Azure AD w hello klasycznego portalu Azure](active-directory-licensing-directory-independence.md). Nowy katalog Hello zostanie utworzona przy użyciu konta jako użytkownik zewnętrzny z uprawnieniami administratora globalnego. Po zarejestrowaniu toohello klasycznego Azure portalu z tego konta można zostanie stanie toosee tego katalogu i dostęp do wszystkich zadań administracyjnych w katalogu. Firma Microsoft zaleca utworzenie lokalnego konta z odpowiednimi uprawnieniami toomanage innych usług firmy Microsoft, (te nie jest dostępna za pośrednictwem hello klasyczny portal Azure). [Dowiedz się więcej na temat tworzenia kont użytkowników w usłudze Azure AD](active-directory-create-users.md).

> [!NOTE]
> Usługi Azure AD obsługuje "użytkowników zewnętrznych", które są konta użytkowników w wystąpieniu usługi Azure AD, które zostały utworzone przy użyciu konta Microsoft (MSA) lub tożsamości usługi Azure AD z innego katalogu. Są nam zajęty rozszerzanie tej możliwości do wszystkich usług firmy Microsoft w organizacji, teraz te konta nie są obsługiwane w niektórych usług hello doświadczeń; na przykład portalu administracyjnego usługi Office 365 hello aktualnie nie obsługuje tych użytkowników. W związku z tym użytkownicy zewnętrzni z kontami Microsoft nie będzie portalu administracyjnego usługi Office 365 hello tooaccess stanie na wszystkich podczas użytkowników zewnętrznych z innych katalogów usługi Azure AD zostaną zignorowane. W drugim przypadku hello, jedynym użytkownikiem hello konta lokalnego, hello Azure AD lub usługi Office 365 katalogu, w którym użytkownik hello pierwotnie został utworzony, jest dostępny za pośrednictwem funkcji.
>
>

Jak wskazano, usługa Azure AD ma różne wersje płatną. Te wersje są niektóre niewielkie różnice w ich dostępności zakupu:

| Product (Produkt) | UMOWA EA/LICENCJONOWANIA ZBIOROWEGO | Otwarty | CSP | Prawa do używania MPN | Bezpośrednie zakupu | Wersja próbna |
| --- | --- | --- | --- | --- | --- | --- |
| Pakiet Enterprise Mobility Suite |X |X |X |X | |X |
| Usługa Azure AD — wersja Premium |X |X |X | |X |X |
| Azure AD podstawowa |X |X |X |X |<br /> |<br /> |

### <a name="select-one-or-more-license-trials"></a>Wybierz co najmniej jeden prób licencji
 We wszystkich przypadkach można aktywować subskrypcję wersji próbnej usługi Azure AD Premium lub pakietu Enterprise Mobility Suite, wybierając hello określonych wersji próbnej, wybrany na karcie licencji hello w katalogu. Każda wersja próbna zawiera subskrypcji 30-dniowej ze 100 licencji.

![Planów licencja próbna usługi Azure Active Directory](./media/active-directory-licensing-what-is/trial_plans.png)

![Plany licencjonowania wersji próbnej pakietu Enterprise Mobility Suite](./media/active-directory-licensing-what-is/EMS_trial_plan.png)

![Licencja próbna aktywnych planów](./media/active-directory-licensing-what-is/active_license_trials.png)

### <a name="assign-licenses"></a>Przypisywanie licencji
Po hello subskrypcja jest aktywna, należy przypisać tooyourself licencji i Odśwież tooensure przeglądarki hello pojawia się wszystkie funkcje. Witaj następnym krokiem jest licencji tooassign toohello użytkowników, którzy będą potrzebne tooaccess lub je uwzględnić w płatną funkcje usługi Azure AD. Jak wspomniano powyżej w "Przypisywanie licencji," hello najlepsze sposób toodo to jest tooidentify hello grupy reprezentujący hello potrzeby odbiorców i przypisz mu licencji toohello; w ten sposób użytkownicy, którzy są dodawane lub usuwane z grupy hello jego cyklem zostanie przypisany tooor usunięte z hello licencji.

tooassign grupy tooa licencji lub poszczególnych użytkowników, wybierz opcję hello planu licencjonowania chcesz tooassign i kliknij przycisk **przypisać** na powitania paska poleceń.

![Licencja próbna aktywnych planów](./media/active-directory-licensing-what-is/assign_licenses.png)

Gdy w oknie dialogowym hello przypisania dla wybranego planu hello, można wybrać użytkowników i dodawanie ich toohello **przypisać** kolumny na powitania prawo. Możesz przeglądania listy użytkowników hello lub wyszukaj konkretne osoby za pomocą wyszukiwania hello szkła na powitania górnego prawego hello użytkownika siatki. grupy tooassign wybierać "Grupy" hello **Pokaż** menu a następnie kliknij przycisk wyboru hello hello prawo toorefresh hello przydziałów, które są wyświetlane.

![Przypisywanie licencji toogroups](./media/active-directory-licensing-what-is/assign_licenses_to_groups.png)

Teraz można przeszukiwać lub za pośrednictwem grupy i dodać je toohello **przypisać** kolumny w hello tak samo. Można użyć tych tooassign kombinację użytkowników i grup w ramach jednej operacji. toocomplete hello procesu przypisania, kliknij przycisk wyboru hello hello prawym dolnym rogu strony hello.

![Wiadomość o postępie przypisania licencji](./media/active-directory-licensing-what-is/license_assignment_progress_message.png)

Po przypisaniu grupy jej elementów członkowskich dziedziczą hello licencji w ciągu 30 minut, ale zazwyczaj w ciągu 1 – 2 minuty.

Przypisanie błędy mogą wystąpić podczas przypisanie licencji usługi Azure AD, ale są stosunkowo rzadko. Potencjalne błędy przydziału są ograniczone do:

* Konflikt przypisania — Jeśli użytkownik został wcześniej przypisanej licencji jest niezgodna z hello bieżącej licencji. W takim przypadku przypisanie hello nowej licencji będzie wymagać usuwanie hello poprzedniego.
* Przekroczono dostępnych licencji - hello liczbę użytkowników w grupach przypisanej przekracza dostępne licencje użytkowników hello stanu przypisania zostaną one zastosowane tooassign awarii, ze względu toomissing licencji.

### <a name="view-assigned-licenses"></a>Wyświetl przypisane licencje
Widok podsumowania przypisane licencje zdarzeń cyklu życia subskrypcji dostępne przypisanej i dalej w tym są wyświetlane na powitania **licencji** kartę.

![Widok hello liczba przypisane licencje](./media/active-directory-licensing-what-is/view_assigned_licenses.png)

Szczegółową listę przypisanych użytkowników i grup, w tym stan przypisania i ścieżki (bezpośrednio lub dziedziczone z co najmniej jedną grupę) jest dostępna podczas nawigowania do planu licencjonowania.

![Wyświetlanie szczegółów licencji przypisanych do planu licencjonowania](./media/active-directory-licensing-what-is/assigned_licenses_detail.png)

Usuwanie licencji jest tak proste, jak przypisywania do nich. Jeśli przypisanej bezpośrednio hello użytkownika lub grupy przypisanej licencji hello można usunąć, wybierając typ licencji hello, wybranie opcji **Usuń**, dodawanie hello użytkownika lub grupy toohello Usuń listę i potwierdzenie hello akcji. Alternatywnie można otworzyć typu licencji, wybierz hello określonego użytkownika lub grupy i wybierz **Usuń** na powitania paska poleceń. tooend dziedziczenia użytkownika licencji z grupy, po prostu usuń hello użytkownika z grupy hello.

### <a name="extending-trials"></a>Rozszerzanie prób
Wersja próbna rozszerzenia dla klientów są dostępne jako samoobsługowego portalu hello usługi Office 365. Administrator klienta można przechodzić toohello [portalu Office](https://portal.office.com/#Billing) (dostępu zależy od uprawnień do portalu usługi Office hello) i wybierz wersję próbną usługi Azure AD Premium. Kliknij przycisk hello **przedłużyć okres próbny** łącze i wykonaj instrukcje hello. Konieczne będzie tooenter karty kredytowej, ale nie zostanie obciążona.

![Rozszerzenie wersji próbnej licencji w portalu Office hello](./media/active-directory-licensing-what-is/extend_license_trial.png)

Klientów można również poprosić o przedłużenie okresu próbnego po przesłaniu żądania pomocy technicznej. Administrator klienta można przechodzić portalu usługi Office 365 toohello [strony pomocy technicznej](http://aka.ms/extendAADtrial) (dostępu zależy od uprawnień dla strony Obsługa Office hello). Na tej stronie wybierz pozycję "Subskrypcje i wersji próbnych" w funkcji i "Wersja próbna pytań" w obszarze objaw. Na koniec wprowadzić informacje o warunkach hello

![Rozszerzenie wersji próbnej licencji przy użyciu żądania obsługi](./media/active-directory-licensing-what-is/alternate_office_aad_trial_extension.png)

## <a name="next-steps"></a>Następne kroki
Teraz możesz być gotowe tooconfigure i korzystać z niektórych funkcji Azure AD Premium.

* [Samoobsługowe Resetowanie hasła](active-directory-manage-passwords.md)
* [Samoobsługowe zarządzanie grupami](active-directory-accessmanagement-self-service-group-management.md)
* [Azure AD Connect kondycji](active-directory-aadconnect-health.md)
* [Tooapplications przypisania grupy](active-directory-manage-groups.md)
* [Uwierzytelnianie wieloskładnikowe platformy Azure](../multi-factor-authentication/multi-factor-authentication.md)
* [Bezpośrednie zakupu licencji Azure AD Premium](http://aka.ms/buyaadp)
