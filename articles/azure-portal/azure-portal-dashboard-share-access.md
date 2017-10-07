---
title: "aaaShare Azure pulpity nawigacyjne portalu przy użyciu RBAC | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak hello tooshare a pulpitu nawigacyjnego w portalu Azure przy użyciu kontroli dostępu opartej na rolach."
services: azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 8908a6ce-ae0c-4f60-a0c9-b3acfe823365
ms.service: multiple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2016
ms.author: tomfitz
ms.openlocfilehash: b12f9f8582596ee14aa8bfdfb4772cc139e3bf45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="share-azure-dashboards-by-using-role-based-access-control"></a>Udostępnianie pulpitów nawigacyjnych Azure przy użyciu kontroli dostępu opartej na rolach
Po skonfigurowaniu pulpitu nawigacyjnego, można ją opublikować i udostępnić go innym użytkownikom w organizacji. Zezwól innym tooview pulpitu nawigacyjnego za pomocą usługi Azure [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-configure.md). Przypisanie użytkownika lub grupy użytkowników tooa roli, a ta rola definiuje, czy tym użytkownikom można wyświetlać lub modyfikować opublikowane pulpitu nawigacyjnego hello. 

Wszystkie opublikowane pulpity nawigacyjne są zaimplementowane jako zasobów platformy Azure, co oznacza istnieje jako elementy można zarządzać w ramach subskrypcji i znajdują się w grupie zasobów.  Z perspektywy kontroli dostępu pulpity nawigacyjne są nie różni się od innych zasobów, takich jak maszyny wirtualnej lub konto magazynu.

> [!TIP]
> Poszczególne Kafelki na pulpicie nawigacyjnym hello wymusić własne wymagania dotyczące kontroli dostępu na podstawie hello zasobów, które są one wyświetlane.  W związku z tym można zaprojektować pulpit nawigacyjny, który jest współużytkowany szeroko przy zapewnieniu ochrony danych hello na poszczególnych Kafelki.
> 
> 

## <a name="understanding-access-control-for-dashboards"></a>Opis kontroli dostępu dla pulpitów nawigacyjnych
Z opartej na rolach kontroli dostępu (RBAC), można przypisać tooroles użytkowników na trzy różne poziomy zakresu:

* subskrypcja
* grupa zasobów
* Zasobów

przypisane uprawnienia Hello są dziedziczone z subskrypcji w dół toohello zasobów. pulpit nawigacyjny opublikowanych Hello jest zasobem. W związku z tym może już istnieć tooroles użytkownicy przypisani hello subskrypcji, która działa także dla hello opublikowanych pulpitu nawigacyjnego. 

Oto przykład.  Załóżmy, że masz subskrypcję platformy Azure i różnych członkowie zespołu są przypisane role hello **właściciela**, **współautora**, lub **czytnika** hello subskrypcji. Użytkownicy, którzy są właściciele i Współautorzy są możliwe toolist, widok, Utwórz, modyfikować lub usuwać pulpitów nawigacyjnych w ramach subskrypcji hello.  Użytkownicy, którzy są czytników są możliwe toolist i wyświetlanie pulpitów nawigacyjnych, ale nie można je modyfikować lub usuwać.  Użytkownikom z dostępem do czytnika są opublikowane pulpitu nawigacyjnego można toomake edycje lokalne tooa (takich jak podczas rozwiązywania problemu), ale nie jest nie jest w stanie toopublish serwera zapasowego toohello tych zmian.  Dysponują toomake opcji hello prywatnej kopii hello pulpitu nawigacyjnego dla siebie

Jednak można także przypisać uprawnienia grupy zasobów toohello, zawierającą kilka pulpity nawigacyjne lub tooan pojedynczego pulpitu nawigacyjnego. Na przykład może zdecydować, że grupy użytkowników powinny mieć ograniczone uprawnienia między hello subskrypcji, ale większa nawigacyjnym określonego tooa dostępu. Możesz przypisać rolę tooa tych użytkowników dla tego pulpitu nawigacyjnego. 

## <a name="publish-dashboard"></a>Publikowanie pulpitu nawigacyjnego
Załóżmy, że zakończono konfigurowanie pulpitu nawigacyjnego mają tooshare z grupą Użytkownicy w Twojej subskrypcji. Poniższe kroki Hello przedstawiać dostosowane grupę o nazwie menedżerów magazynu, ale niezależnie od chcesz można nazwę grupy. Aby uzyskać informacje o tworzeniu grupy usługi Active Directory i dodawanie użytkowników toothat grupy, zobacz [Zarządzanie grupami w usłudze Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

1. Na pulpicie nawigacyjnym hello, wybierz **udziału**.
   
     ![Wybierz udział](./media/azure-portal-dashboard-share-access/select-share.png)
2. Przed udzieleniem im dostępu, należy opublikować hello pulpitu nawigacyjnego. Domyślnie hello pulpitu nawigacyjnego zostaną opublikowane tooa grupy zasobów o nazwie **pulpity nawigacyjne**. Wybierz **publikowania**.
   
     ![publish](./media/azure-portal-dashboard-share-access/publish.png)

Pulpit nawigacyjny zostały opublikowane. Jeśli hello uprawnienia dziedziczone z subskrypcji hello są odpowiednie, nie trzeba toodo niczego więcej. Inni użytkownicy w organizacji zostanie stanie tooaccess i zmodyfikować pulpitu nawigacyjnego hello na podstawie ich ról poziomu subskrypcji. Jednak w tym samouczku teraz przypisać grupę użytkowników tooa roli dla tego pulpitu nawigacyjnego.

## <a name="assign-access-tooa-dashboard"></a>Przypisz pulpitu nawigacyjnego tooa dostępu
1. Po opublikowaniu hello pulpitu nawigacyjnego, wybierz **Zarządzanie użytkownikami**.
   
     ![zarządzanie użytkownikami](./media/azure-portal-dashboard-share-access/manage-users.png)
2. Zostanie wyświetlona lista istniejących użytkowników, które już przypisano rolę do tego pulpitu nawigacyjnego. Listę istniejących użytkowników mogą być inne niż obraz powitania poniżej. Prawdopodobnie przydziały hello są dziedziczone z hello subskrypcji. tooadd nowego użytkownika lub grupę, wybierz **Dodaj**.
   
     ![Dodaj użytkownika](./media/azure-portal-dashboard-share-access/existing-users.png)
3. Wybierz rolę hello, którą reprezentuje uprawnienia hello chcesz toogrant. Na przykład wybierz **współautora**.
   
     ![Wybierz rolę](./media/azure-portal-dashboard-share-access/select-role.png)
4. Wybierz hello użytkownika lub grupy, że chcesz tooassign toohello roli. Jeśli nie ma hello użytkownika lub grupę, których szukasz liście hello, użyj pola wyszukiwania hello. Z listy dostępnych grup będzie zależeć od hello grup, które zostały utworzone w usłudze Active Directory.
   
     ![Wybierz użytkownika](./media/azure-portal-dashboard-share-access/select-user.png) 
5. Po zakończeniu dodawania użytkowników lub grup, wybierz **OK**. 
6. nowe przypisanie Hello jest dodawana toohello listy użytkowników. Zwróć uwagę, że jego **dostępu** jest wymienione jako **przypisane** zamiast **dziedziczonych**.
   
     ![przypisane role](./media/azure-portal-dashboard-share-access/assigned-roles.png)

## <a name="next-steps"></a>Następne kroki
* Aby uzyskać listę ról, zobacz [RBAC: role wbudowane](../active-directory/role-based-access-built-in-roles.md).
* toolearn dotyczących zarządzania zasobami, zobacz [zasobów Azure zarządzania za pośrednictwem portalu](resource-group-portal.md).

