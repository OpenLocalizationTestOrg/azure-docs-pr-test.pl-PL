---
title: "aaaLicense użytkowników w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toolicense sobie i użytkownikom w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: f8b932bc-8b4f-42b5-a2d3-f2c076234a78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
custom: it-pro
ms.openlocfilehash: ae0bc030fa02b79d1dd01ca961b4e96e6b9c470d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-license-users-in-azure-active-directory"></a>Szybki Start: Licencji użytkowników w usłudze Azure Active Directory
Na podstawie licencji usługi Azure AD usług pracy aktywować subskrypcję usługi Azure Active Directory (Azure AD) w dzierżawie platformy Azure. Po hello subskrypcja jest aktywna, możliwości usługi są zarządzane przez administratorów usługi Azure AD i używane przez licencjonowanych użytkowników. Po zakupie pakietu Enterprise Mobility + Security, Azure AD Premium lub Azure AD podstawowa, dzierżawy jest aktualizowane hello subskrypcji, w tym okresie ważności i Przedpłata licencji. Informacje o Twoim subskrypcji, w tym hello liczba przydzielonych lub dostępnych licencji, jest dostępna za pośrednictwem hello Azure portalu w obszarze **usługi Azure Active Directory** przez otwarcie hello **licencji** kafelka. Witaj **licencji** bloku jest również hello najlepsze miejsce toomanage przypisaniami licencji.

Uzyskiwanie subskrypcji ma wszystkie potrzebne tooconfigure płatnej możliwości, ale nadal musi przypisywać licencje użytkowników dla płatnej usługi Azure AD płatnej funkcji. Każdy użytkownik, którzy powinni mieć dostęp do lub który odbywa się za pośrednictwem usługi Azure AD płatnej funkcji należy przypisać im licencję. Przypisanie licencji jest mapowanie między użytkownikiem i zakupionych usług, takich jak Azure AD Premium, Basic lub pakietu Enterprise Mobility + Security.

Można użyć [przypisanie licencji na podstawie grupy](active-directory-licensing-whatis-azure-portal.md) tooset reguł, takich jak hello poniżej:
* Wszyscy użytkownicy w katalogu automatycznie otrzymuje licencję
* Pobiera wszystkich osób mających stanowisko odpowiednie hello licencji
* Możesz delegować hello decyzji tooother menedżerów w organizacji hello (przy użyciu [grup samoobsługi](active-directory-accessmanagement-self-service-group-management.md))

> [!TIP]
> Szczegółowe omówienie toogroups przypisanie licencji, w tym zaawansowane scenariusze i usługi Office 365 licencjonowania scenariuszy, zobacz [Przypisz licencje toousers przez członkostwo w grupie w usłudze Azure Active Directory](active-directory-licensing-group-assignment-azure-portal.md).

## <a name="assign-licenses-toousers-and-groups"></a>Przypisz licencje toousers i grupy
Przy użyciu aktywnej subskrypcji, należy najpierw przypisać tooyourself licencji i Odśwież tooensure Twojego przeglądarki, widoczne wszystkie hello Oczekiwano funkcji dostępnych w ramach subskrypcji. Witaj następnym krokiem jest tooassign licencji toohello użytkowników, którzy potrzebują funkcji Azure AD toopaid dostępu. Licencje tooassign łatwo jest tooassign toogroups licencje użytkowników, a nie tooindividuals. Po przypisaniu licencji tooa grupy Wszyscy członkowie grupy przypisanych licencji. Jeśli użytkownicy są dodawane lub usuwane z grupy hello, odpowiednią licencję hello jest automatycznie przypisać lub usunąć. 

> [!NOTE]
> Pewnych usług firmy Microsoft nie są dostępne we wszystkich lokalizacjach. Zanim można przypisać licencję użytkownika tooa, hello administrator musi określić hello **lokalizacji użytkowania** właściwość hello użytkownika. Można ustawić tę właściwość w obszarze **użytkownika** &gt; **profilu** &gt; **ustawienia** w hello portalu Azure. Używając przypisanie do grupy licencji, każdy użytkownik nie określono lokalizacji użytkowania, której dziedziczy hello lokalizację katalogu hello.

tooassign licencji w obszarze **usługi Azure Active Directory** &gt; **licencji** &gt; **wszystkich produktów**, wybierz jeden lub więcej produktów, a następnie wybierz **Przypisać** na powitania paska poleceń.

![Wybierz tooassign licencji](media/license-users-groups/select-license-to-assign.png)

Można użyć hello **użytkowników i grup** wielu użytkowników lub grup lub usługi toodisable plany w produkcie hello toochoose bloku. Użyj pola wyszukiwania hello na najwyższym toosearch dla nazwy użytkowników i grup.

![Wybierz użytkownika lub grupy do przypisania licencji](media/license-users-groups/select-user-for-license-assignment.png)

Po przypisaniu licencji tooa grupy może potrwać pewien czas, zanim wszyscy użytkownicy dziedziczą hello licencji, w zależności od wielkości hello hello grupy. Istnieje możliwość sprawdzenia stanu przetwarzania hello na powitania **grupy** bloku, w obszarze hello **licencji** kafelka.

![Stan przypisania licencji](media/license-users-groups/license-assignment-status.png)

Przypisanie błędy mogą wystąpić podczas przypisanie licencji usługi Azure AD, ale są stosunkowo rzadko podczas zarządzania usługi Azure AD i Enterprise Mobility + Security produktów. Potencjalne błędy przydziału są ograniczone do:
- Konflikt przypisania: Jeśli użytkownik został już wcześniej przypisany licencji, która jest niezgodna z bieżącej licencji hello. W takim przypadku przypisanie hello nowej licencji wymaga usuwanie hello bieżący.
- Przekroczono dostępnych licencji: hello liczbę użytkowników w grupach przypisanej przekroczenia hello dostępnych licencji użytkownika stanu przypisania odzwierciedla tooassign awarii, ze względu toomissing licencji.

### <a name="azure-ad-b2b-collaboration-licensing"></a>Azure licencjonowania współpracy B2B usługi AD

Współpraca B2B pozwala tooinvite gości do usług tooAzure AD dostępu tooprovide dzierżawy usługi Azure AD i dowolnych zasobów platformy Azure mają być dostępne.  

Jest bezpłatna dla zapraszanie B2B użytkowników i przypisywania do nich tooan aplikacji w usłudze Azure AD. Zapasowej too10 aplikacji dla gościa użytkownika i 3 podstawowe raporty są również bezpłatna dla użytkowników współpracy B2B. Jeśli użytkownika gościa zawiera wszystkie odpowiednie licencje przypisane w dzierżawie usługi Azure AD hello partnera, będą one licencjonowane w należy do Ciebie również.

Nie jest to wymagane, ale jeśli chcesz, aby funkcje usługi Azure AD toopaid dostępu tooprovide, muszą mieć licencję tych gości B2B z odpowiednimi licencjami usługi Azure AD. Zapraszanie dzierżawy z usługi Azure AD z płatnej licencji można przypisać prawa użytkownika współpracy B2B tooan pięć dodatkowych gości zaproszenie toohello dzierżawy. Scenariusze i informacje, zobacz [współpracy B2B licencjonowania wskazówki](active-directory-b2b-licensing.md).

## <a name="view-assigned-licenses"></a>Wyświetl przypisane licencje

Widok podsumowania przypisane i dostępnych licencji zostanie wyświetlona w obszarze **usługi Azure Active Directory** &gt; **licencji** &gt; **wszystkie produkty**.

![Licencja wyświetlania podsumowania](media/license-users-groups/view-license-summary.png)

Szczegółową listę przypisanych użytkowników i grup jest dostępna po wybraniu określonego produktu. Witaj **licencjonowanych użytkowników** lista zawiera wszystkich użytkowników, w obecnie korzystających z licencji i czy licencji hello przypisano bezpośrednio toohello użytkownika lub jeśli zostało ono odziedziczone po grupie.

![Wyświetl szczegóły licencji](media/license-users-groups/view-license-detail.png)

Podobnie, hello **grup licencji** lista zawiera wszystkich grup licencji toowhich zostały przypisane. Wybierz użytkownika lub grupę hello tooopen **licencji** bloku, który zawiera wszystkie licencje przypisać toothat obiektu.

## <a name="remove-a-license"></a>Usunąć licencję

tooremove licencji, przejdź toohello użytkownika lub grupę, a następnie otwórz hello **licencji** kafelka. Wybierz hello licencji, a następnie kliknij przycisk **Usuń**.

![Usunąć licencję](media/license-users-groups/remove-license.png)

Nie można bezpośrednio usunąć dziedziczone przez hello użytkownika z grupy licencji. Zamiast tego należy usunąć hello użytkownika z grupy hello, z którego są dziedziczone hello licencji.


## <a name="next-steps"></a>Następne kroki
W tym szybkiego startu kiedy znasz już jak tooassign licencje toousers i grupy w katalogu usługi Azure AD. 

Można użyć poniższych przypisania licencji subskrypcji tooconfigure łącze w usłudze Azure AD z portalu Azure hello hello.

> [!div class="nextstepaction"]
> [Przypisywanie licencji usługi Azure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/LicensesMenuBlade/Overview) 