---
title: "toostart aaaHow Przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate dostępu Przejrzyj dla uprzywilejowanymi tożsamościami przy hello aplikacji Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
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
ms.openlocfilehash: 24feac307f77c69b5d68d6ae0623dbcb52416b01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostart-an-access-review-in-azure-ad-privileged-identity-management"></a>Jak toostart dostępu Przejrzyj w usłudze Azure AD Privileged Identity Management
Przypisania ról nieodświeżone "", gdy użytkownicy mają uprzywilejowany dostęp, które nie wymagają już. W kolejności tooreduce hello ryzyka związanego z tych przypisań ról starych ról uprzywilejowanych powinni regularnie sprawdzić hello ról, które użytkownicy mają prawo. W tym dokumencie opisano kroki hello uruchamiania Przegląd dostępu w usłudze Azure AD Privileged Identity Management (PIM).

## <a name="start-an-access-review"></a>Rozpocząć Przegląd dostępu
> [!NOTE]
> Jeśli nie dodano hello pulpit nawigacyjny tooyour aplikacji dla usługi PIM w hello portalu Azure, zobacz kroki hello w [wprowadzenie do korzystania z usługi Azure Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md)
> 
> 

Z usługi PIM hello aplikacji strony głównej istnieją trzy sposoby toostart Przegląd dostępu:

* **Dostęp do przeglądu** > **Dodaj**
* **Role** > **przeglądu** przycisku
* Wybierz hello konkretnej roli toobe usunięci z listy ról hello > **przeglądu** przycisku

Po kliknięciu hello **Przejrzyj** przycisk hello **rozpocząć Przegląd dostępu** zostanie wyświetlony blok. W tym bloku jest będzie tooconfigure hello recenzowania o nazwie i limit czasu, wybraniu tooreview roli i zdecydować, kto będzie wykonywać hello przeglądu.

![Przegląd dostępu — zrzut ekranu Start][1]

### <a name="configure-hello-review"></a>Skonfiguruj hello przeglądu
Przejrzyj dostępu toocreate należy tooname go i Ustaw daty początkową i końcową.

![Skonfiguruj przeglądu — zrzut ekranu][2]

Należy hello długość hello Przejrzyj wystarczająco długi dla toocomplete użytkowników. Jeśli zakończy się wcześniejsza niż data zakończenia hello, można zawsze zatrzymać przeglądu hello wcześniej.

### <a name="choose-a-role-tooreview"></a>Wybierz tooreview roli
Każdego przeglądu koncentruje się na tylko jedną rolę. Jeśli nie został uruchomiony Przegląd dostępu hello bloku konkretnej roli, należy toochoose roli teraz.

1. Przejdź do zbyt**Przejrzyj członkostwo roli**
   
    ![Przejrzyj członkostwo roli — zrzut ekranu][3]
2. Wybierz jedną rolę z listy hello.

### <a name="decide-who-will-perform-hello-review"></a>Zdecyduj, który przeprowadzi hello przeglądu
Dostępne są trzy opcje umożliwiające wykonywanie przeglądu. Można przypisać toosomeone przeglądu hello else toocomplete, możesz zrobić to samodzielnie lub może mieć każdy użytkownik, Przejrzyj swoje własne dostępu.

1. Przejdź do zbyt**wybierz osób dokonujących przeglądu**
   
    ![Wybierz osoby dokonujące przeglądu — zrzut ekranu][4]
2. Wybierz jedną z opcji hello:
   
   * **Wybierz osoby dokonującej przeglądu**: Użyj tej opcji, jeśli nie wiesz, który musi mieć dostęp. Po wybraniu tej opcji można przypisać właściciela zasobów tooa przeglądu hello lub toocomplete menedżera grupy.
   * **ME**: przydatne w przypadku toopreview jak dostępu przegląda pracy lub w imieniu osoby, które nie mają tooreview.
   * **Elementy członkowskie, zapoznaj się**: za pomocą przeglądu użytkowników hello toohave opcji własnych przypisań ról.

### <a name="start-hello-review"></a>Rozpocząć Przegląd hello
Na koniec należy toorequire opcji hello użytkowników podać przyczynę, jeśli udzielają dostępu. Jeśli chcesz dodać opis hello przeglądu, a następnie wybierz **Start**.

Upewnij się, że poinformować użytkowników, wiadomo, że jest przegląd dostępu oczekiwanie na ich i wyświetlić je [jak tooperform dostępu Przejrzyj](active-directory-privileged-identity-management-how-to-perform-security-review.md).

## <a name="manage-hello-access-review"></a>Zarządzanie hello Przegląd dostępu
Możesz śledzić postępy hello w recenzentów hello zakończenia ich oceny w hello Azure AD PIM pulpitu nawigacyjnego, w hello dostępu przegląda sekcji. Brak praw dostępu zostaną zmienione w katalogu hello do [zakończeniu Przejrzyj hello](active-directory-privileged-identity-management-how-to-complete-review.md).

Okresu przeglądu hello toocomplete użytkownicy mogą Przypomnij ich przeglądu, lub przejrzyj hello stop wczesne przed dostępem hello przegląda sekcji.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="pim-table-of-contents"></a>PIM spis treści
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_start_review.png
[2]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_configure.png
[3]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_role.png
[4]: ./media/active-directory-privileged-identity-management-how-to-start-security-review/PIM_review_reviewers.png
