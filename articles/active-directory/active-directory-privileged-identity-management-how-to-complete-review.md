---
title: "toocomplete aaaHow Przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Po rozpoczęciu Przegląd dostępu w usłudze Azure AD Privileged Identity Management Dowiedz się jak toocomplete go i widoku hello wyników"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a>Jak toocomplete dostępu Przejrzyj w usłudze Azure AD Privileged Identity Management
Administratorzy ról uprzywilejowanych można przejrzeć uprzywilejowanego dostępu raz [przeglądu zabezpieczeń została uruchomiona](active-directory-privileged-identity-management-how-to-start-security-review.md). Azure AD Privileged Identity Management (PIM) będzie automatycznie wysyłać wiadomości e-mail monitowania użytkowników tooreview dostępu. Jeśli użytkownik nie pobrały wiadomości e-mail, możesz wysłać im instrukcje hello [jak tooperform zabezpieczeń Przejrzyj](active-directory-privileged-identity-management-how-to-perform-security-review.md).

Po umieszczeniu okresu przeglądu zabezpieczeń hello lub wszyscy użytkownicy hello zostało ukończone w ich własnym Przejrzyj, wykonaj kroki hello w tym przeglądzie hello toomanage artykułu i zobaczyć wyniki hello.

## <a name="manage-security-reviews"></a>Zarządzanie inspekcje zabezpieczeń
1. Przejdź toohello [portalu Azure](https://portal.azure.com/) i wybierz hello **Azure AD Privileged Identity Management** aplikacji na pulpicie nawigacyjnym.
2. Wybierz hello **dostępu przeglądami** sekcji hello pulpitu nawigacyjnego.
3. Wybierz hello Przegląd dostępu, które mają toomanage.

W bloku szczegółów Przegląd dostępu hello istnieją liczba opcji zarządzania przeglądu.

![Przyciski przeglądu dostępu PIM — zrzut ekranu][1]

### <a name="remind"></a>Przypomnij
Jeśli Przegląd dostępu jest skonfigurowana tak, aby użytkownicy hello Przejrzyj samodzielnie, hello **Przypomnij** przycisk wysyła powiadomienia. 

### <a name="stop"></a>Stop
Wszystkie przeglądy dostępu mają datę końcową, ale można użyć hello **zatrzymać** toofinish przycisk go wcześniej. Jeśli jeszcze nie zostały sprawdzone wszyscy użytkownicy tego czasu, nie będą tooafter może zatrzymać hello przeglądu. Nie można ponownie uruchomić przeglądu, po jest została zatrzymana.

### <a name="apply"></a>Składanie wniosku o przyjęcie do programu
Po zakończeniu przeglądu dostęp, albo ponieważ osiągnięto datę zakończenia hello lub go ręcznie, zatrzymana hello **Zastosuj** przycisk implementuje hello wyniku hello przeglądu. Jeśli w przeglądzie hello nastąpiła odmowa dostępu użytkownika, jest to krok hello spowoduje usunięcie przypisania roli.  

### <a name="export"></a>Eksportowanie
Jeśli chcesz ręcznie tooapply hello wyników przeglądu zabezpieczeń hello, możesz wyeksportować hello przeglądu. Witaj **wyeksportować** przycisk rozpocznie się pobieranie pliku CSV. Wyniki hello w programie Excel lub inne programy, które mają otwarte pliki CSV można zarządzać.

### <a name="delete"></a>Usuwanie
Jeśli nie jesteś zainteresowany hello przejrzyj wszelkie dodatkowe, usuń go. Witaj **usunąć** przycisk usuwa hello PIM aplikacji hello przeglądu.

> [!IMPORTANT]
> Zostanie nie wyświetlone ostrzeżenie, zanim nastąpi jego usunięcia, dlatego należy się, że toodelete, który sprawdzić. 

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
