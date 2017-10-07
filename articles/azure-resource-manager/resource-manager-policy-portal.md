---
title: "portal aaaAzure zasady zasobów | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse toocreate portalu Azure Resource Manager zasad i zarządzania nimi. Zasady można stosować na powitania grupy zasobów lub subskrypcji."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a>Użyj tooassign portalu Azure i zarządzanie zasadami zasobów
Witaj portalu Azure umożliwia możesz tooassign zasady tooresource grup zasobów i subskrypcje. Interfejs użytkownika Hello umożliwia łatwe tooselect hello zasad mają tooassign i podaj wartości parametrów dla tej zasady toocustomize hello ustawienia zasad. 

tooassign zasad za pośrednictwem portalu hello definicji zasad hello musi już istnieć w ramach subskrypcji. Subskrypcja obejmuje kilka definicje wbudowanych zasad, które są gotowe do momentu tooassign tooresource grupy lub subskrypcji. Widzisz tych zasad wbudowanych i niestandardowych zasad, które zdefiniowano przy użyciu zasad portalu tooassign hello. Wprowadzenie toopolicies i jak toodefine dostosowane zasady, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).

Zasady są dziedziczone przez wszystkie zasoby podrzędne. Jeśli zasady są stosowane tooa grupy zasobów, jest odpowiednie tooall hello zasobów w danej grupie zasobów. W tym artykule określenie hello **zakres** odwołuje się toohello grupy zasobów lub subskrypcji, która jest przypisana hello zasad. 

Zasady są oceniane podczas tworzenia i aktualizowania zasobów (PUT i poprawka operacji).

## <a name="assign-a-policy"></a>Przypisać zasady

1. tooassign tooeither zasad grupy zasobów lub subskrypcji, należy wybrać odpowiednie grupy zasobów lub subskrypcji. W ustawieniach hello wybierz **zasad**.

   ![Wybieranie zasad](./media/resource-manager-policy-portal/select-policies.png)

2. Wybierz przypisanie zasad dla tego zakresu toocreate **Dodaj przypisanie**.

   ![Dodaj przypisania](./media/resource-manager-policy-portal/add-assignment.png)

3. Wybierz zasady hello ma tooassign. Nawet jeśli nie dodano żadnych subskrypcji tooyour definicje zasad, zobacz się hello wbudowanych zasad, które są dostępne do przypisania. Zasady te wbudowane obejmują wiele typowych scenariuszy.

   ![Wybierz definicję](./media/resource-manager-policy-portal/select-definition.png)

4. Po wybraniu zasad, zobacz opis zasad hello i wszelkie parametry dla tej zasady. Na przykład hello poniższy obraz przedstawia hello **dozwolone lokalizacje** parametr, który jest wymagany dla hello zasadę, która ogranicza hello dostępnych lokalizacji.

   ![Pokaż parametry](./media/resource-manager-policy-portal/show-parameters.png)

5. Za pomocą interfejsu użytkownika hello wybierz hello toospecify wartości dla parametrów zasad hello (na przykład hello lokalizacje, które mogą być używane do wdrożenia).

   ![Wybierz wartości parametrów](./media/resource-manager-policy-portal/select-parameters.png)

6. Podaj wartości hello innych parametrów. zakres Hello zostanie automatycznie przypisany oparte na powitania bloku, wybranych podczas uruchamiania hello przypisania zasad. Po zakończeniu wybierz przycisk **OK**.

   ![Zdefiniuj parametry](./media/resource-manager-policy-portal/define-parameters.png)

  Przypisaniu zasad hello toohello określony zakres.

## <a name="view-policy-assignments"></a>Wyświetl przypisania zasad

Po przypisaniu zasad, zobacz liście hello zasad dla tego zakresu. Witaj **szczegóły** karta zawiera podsumowanie hello przypisania zasad.

![Pokaż szczegóły](./media/resource-manager-policy-portal/show-details.png)

Witaj **zasada przypisania** karcie są wyświetlane hello JSON dla definicji zasad hello.

![Pokaż reguły przypisania](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a>Zmień istniejące przypisania zasad

toochange zasady, wybierz **edytować przypisanie** lub **usunąć**

![edytowanie lub usuwanie przypisania](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a>Przypisanie zasad niestandardowych

Jeśli zasady niestandardowe zdefiniowane w ramach subskrypcji, te zasady są dostępne do przypisania w ramach hello portalu. Te zasady są poprzedzone znakiem **[Custom]**

![zasady niestandardowe](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a>Następne kroki
* toolearn o składni JSON hello do definiowania zasad, zobacz [Przegląd zasad zasobów](resource-manager-policy.md).
* Aby uzyskać wskazówki dotyczące użycia tooeffectively Menedżera zasobów przedsiębiorstwa Zarządzaj subskrypcjami, zobacz [szkieletu Azure enterprise — ładu przetestowanego subskrypcji](resource-manager-subscription-governance.md).
* Schemat zasad Hello jest opublikowana w [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json). 

