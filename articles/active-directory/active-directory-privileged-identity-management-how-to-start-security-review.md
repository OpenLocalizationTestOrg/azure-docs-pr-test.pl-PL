---
title: "Jak rozpocząć Przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć Przegląd dostępu uprzywilejowanego tożsamości z aplikacji Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: 3e52b731-55f4-4c8a-ba87-9fd34033f52f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: f57a32ca1914d18540289ebb05421a7ae9618094
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="how-to-start-an-access-review-in-azure-ad-privileged-identity-management"></a>Jak rozpocząć Przegląd dostępu w usłudze Azure AD Privileged Identity Management
Przypisania ról nieodświeżone "", gdy użytkownicy mają uprzywilejowany dostęp, które nie wymagają już. W celu zmniejszenia ryzyka związanego z tych przypisań ról starych, ról uprzywilejowanych powinni regularnie sprawdzić ról, którym przyznano użytkowników. W tym dokumencie opisano kroki dotyczące uruchomienia Przegląd dostępu w usłudze Azure AD Privileged Identity Management (PIM).

## <a name="start-an-access-review"></a>Rozpocząć Przegląd dostępu
> [!NOTE]
> Jeśli nie dodano aplikacji PIM do pulpitu nawigacyjnego w portalu Azure, zobacz kroki w [wprowadzenie do korzystania z usługi Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Na stronie głównej aplikacji PIM istnieją trzy sposoby uruchamiania Przegląd dostępu:

* **Dostęp do przeglądu** > **Dodaj**
* **Role** > **przeglądu** przycisku
* Wybierz określoną rolę, należy sprawdzić na liście ról > **przeglądu** przycisku

Po kliknięciu **Przejrzyj** przycisku **rozpocząć Przegląd dostępu** zostanie wyświetlony blok. W tym bloku użytkownik chce skonfigurować przeglądu przy użyciu nazwy i limit czasu, wybierz rolę, aby przejrzeć i zdecydować, kto będzie wykonywać przeglądu.

![Przegląd dostępu — zrzut ekranu Start][1]

### <a name="configure-the-review"></a>Skonfiguruj przeglądu
Aby utworzyć Przegląd dostępu, należy nadaj jej nazwę i ustawiania datę początkową i końcową.

![Skonfiguruj przeglądu — zrzut ekranu][2]

Należy długość przeglądu wystarczająco długo, użytkowników ją zakończyć. Jeśli zakończy się wcześniejsza od daty zakończenia, można zawsze zatrzymać przeglądu wcześniej.

### <a name="choose-a-role-to-review"></a>Wybierz rolę do przeglądu
Każdego przeglądu koncentruje się na tylko jedną rolę. Chyba, że przegląd dostępu został uruchomiony z bloku konkretnej roli, należy wybrać rolę teraz.

1. Przejdź do **Przejrzyj członkostwo roli**
   
    ![Przejrzyj członkostwo roli — zrzut ekranu][3]
2. Wybierz jedną rolę z listy.

### <a name="decide-who-will-perform-the-review"></a>Zdecyduj, który przeprowadzi przeglądu
Dostępne są trzy opcje umożliwiające wykonywanie przeglądu. Przegląd można przypisać do innej osoby, aby zakończyć, możesz zrobić to samodzielnie lub może mieć każdy użytkownik, Przejrzyj swoje własne dostępu.

1. Przejdź do **wybierz osób dokonujących przeglądu**
   
    ![Wybierz osoby dokonujące przeglądu — zrzut ekranu][4]
2. Wybierz jedną z opcji:
   
   * **Wybierz osoby dokonującej przeglądu**: Użyj tej opcji, jeśli nie wiesz, który musi mieć dostęp. Po wybraniu tej opcji można przypisać do właściciela zasobów lub menedżera grupy do ukończenia przeglądu.
   * **ME**: przydatne, jeśli chcesz obejrzeć, jak program access sprawdza pracy lub aby przejrzeć w imieniu osoby, które nie.
   * **Elementy członkowskie, zapoznaj się**: Użyj tej opcji, aby przejrzeć swoje własne przypisań ról użytkowników.

### <a name="start-the-review"></a>Uruchom przeglądu
Na koniec masz opcję, aby wymagać podania użytkowników przyczynę Jeśli udzielają dostępu. Jeśli chcesz dodać opis przeglądu, a następnie wybierz **Start**.

Upewnij się, że poinformować użytkowników, wiadomo, że jest przegląd dostępu oczekiwanie na ich i wyświetlić je [jak przeprowadzić przegląd dostępu](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-the-access-review"></a>Zarządzanie Przegląd dostępu
Postęp można śledzić w recenzentów zakończenia ich przeglądami na pulpicie nawigacyjnym usługi Azure AD PIM w sekcji przeglądami dostęp. Brak praw dostępu zostaną zmienione w katalogu do [zakończeniu przeglądu](active-directory-privileged-identity-management-how-to-complete-review.md).

Aż do okresu przeglądu Przypomnij użytkowników przeprowadzenie ich przeglądu, lub Zatrzymaj przeglądu wcześniej w sekcji przeglądami dostępu.

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="pim-table-of-contents"></a>PIM spis treści
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
