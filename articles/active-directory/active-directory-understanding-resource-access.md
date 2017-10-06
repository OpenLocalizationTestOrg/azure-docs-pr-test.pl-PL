---
title: "aaaUnderstanding dostęp do zasobów na platformie Azure | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano pojęcia dotyczące korzystania z subskrypcji dostęp do zasobów toocontrol dla administratorów w hello pełnej wersji portalu Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: 174f1706-b959-4230-9a75-bf651227ebf6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 06b9c4166bdea849faae67cae3146c6c278deb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-resource-access-in-azure"></a>Opis dostęp do zasobów na platformie Azure
> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Witaj Azure portal udostępnia [kontroli dostępu opartej na rolach](role-based-access-control-configure.md) tak zasobów platformy Azure można zarządzać dokładniej.
> 
> 

W październiku 2013 r. hello klasycznego portalu Azure i interfejsów API usługi Service Management zostały zintegrowane z usługą Azure Active Directory w kolejności toolay hello przygotowuje poprawę środowiska użytkownika hello zarządzania zasobami tooAzure dostępu. Azure Active Directory zawiera już dużą możliwości, takie jak zarządzanie użytkownikami, synchronizacja katalogu lokalnego uwierzytelniania wieloskładnikowego i kontroli dostępu aplikacji. Oczywiście te powinny również dostępne do zarządzania zasobami Azure ogólnego.

Kontrola dostępu na platformie Azure rozpoczyna się z punktu widzenia rozliczeń. Witaj właściciela konta platformy Azure, dostęp, przechodząc na stronę hello [Centrum konta platformy Azure](https://account.windowsazure.com/subscriptions), jest hello konta administratora (AA). Subskrypcje są kontener rozliczeń, ale również działają jako granic zabezpieczeń: Każda subskrypcja ma usługi administratora kto dodawania, usuwania i modyfikowania zasobów platformy Azure w ramach tej subskrypcji przy użyciu hello [klasycznego portalu Azure](https://manage.windowsazure.com/). SA domyślne Hello nowej subskrypcji jest hello AA, ale hello AA można zmienić hello SA w hello Centrum konta platformy Azure.

<br><br>![Konta platformy Azure][1]

Subskrypcje mają również skojarzenie z katalogiem. katalog Hello definiuje zestaw użytkowników. Mogą to być użytkownicy z hello pracy lub nauki, który utworzył katalog hello lub można je użytkowników zewnętrznych (to znaczy Accounts firmy Microsoft). Subskrypcje są dostępne dla podzbioru użytkowników katalogu, na których został przypisany jako usługi administratora lub administratora współpracującego (CA); Witaj tylko wyjątek to, że dla starszych powodów Accounts firmy Microsoft (dawniej identyfikator Windows Live ID) można przypisać jako administratora systemu lub urzędu certyfikacji nie jest obecny w katalogu hello.

<br><br>![Kontrola dostępu na platformie Azure][2]

Funkcje hello klasycznego portalu Azure umożliwia SAs, które są podpisane za pomocą katalogu hello toochange Account Microsoft skojarzonego z subskrypcją za pomocą hello **Edytuj katalog** na powitania **Subskrypcje** strony **ustawienia**. Należy pamiętać, że ta operacja ma wpływ na powitania kontroli dostępu subskrypcji.

> [!NOTE]
> Witaj **Edytuj katalog** poleceń w hello Azure classic portal nie jest dostępne toousers, który jest zalogowany przy użyciu lub konto służbowe, ponieważ te konta można zalogować się tylko toohello katalogu toowhich należą.
> 
> 

<br><br>![Przepływu logowania użytkownika prostego][3]

W przypadku prostego powitania organizacji (na przykład Contoso) wymusić rozliczeń i kontrola dostępu między hello sam zestaw subskrypcji. Katalog hello jest skojarzony toosubscriptions, które należą do jednego konta platformy Azure. Po toohello pomyślnego logowania klasycznego portalu Azure użytkownicy widzą dwie kolekcje zasobów (kolor pomarańczowy hello poprzedniej ilustracji przedstawiono):

* Katalogi Jeśli istnieje ich konta użytkownika (powierzając jej ich konserwację lub dodany jako obcego podmiotu zabezpieczeń). Należy pamiętać, że tego katalogu hello używane do logowania nie jest toothis odpowiednich obliczeń, więc katalogi są zawsze wyświetlane niezależnie od tego, w którym się zalogowano.
* Zasoby, które są częścią subskrypcji skojarzonych z katalogu hello używanego do logowania i które hello użytkownika ma dostęp do (gdy są SA lub urząd certyfikacji).

<br><br>![Użytkownik z wieloma subskrypcjami i katalogami][4]

Użytkownicy z subskrypcjami w wielu katalogach mają hello możliwości tooswitch hello bieżący kontekst hello klasycznego portalu Azure za pomocą hello filtr subskrypcji. W obszarze obejmuje hello powoduje to w innym katalogu tooa oddzielne logowania, ale odbywa się bezproblemowo przy użyciu rejestracji jednokrotnej (SSO).

Operacje, takie jak przeniesienie zasobów między subskrypcjami może być trudniejsza w wyniku tego widoku jednego katalogu subskrypcji. przeniesienia zasobu hello tooperform, może być konieczne toofirst Użyj hello **Edytuj katalog** polecenia na stronie subskrypcji hello **ustawienia** tooassociate hello subskrypcje toohello tym samym katalogu .

## <a name="next-steps"></a>Następne kroki
* więcej informacji o toolearn, toochange Administratorzy subskrypcji platformy Azure, zobacz temat [jak tooadd lub zmień role administratora platformy Azure](../billing/billing-add-change-azure-subscription-administrator.md)
* Aby uzyskać więcej informacji dotyczących powiązań tooyour subskrypcji platformy Azure w usłudze Azure Active Directory, zobacz [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](active-directory-how-subscriptions-associated-directory.md)
* Aby uzyskać więcej informacji na temat ról tooassign w usłudze Azure AD, zobacz [przypisywanie ról administratorów w usłudze Azure Active Directory](active-directory-assign-admin-roles.md)

<!--Image references-->
[1]: ./media/active-directory-understanding-resource-access/IC707931.png
[2]: ./media/active-directory-understanding-resource-access/IC707932.png
[3]: ./media/active-directory-understanding-resource-access/IC707933.png
[4]: ./media/active-directory-understanding-resource-access/IC707934.png
