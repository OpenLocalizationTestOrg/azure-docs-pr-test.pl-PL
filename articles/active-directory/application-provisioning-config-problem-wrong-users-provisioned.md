---
title: "aaaWrong zbiór użytkowników są udostępnione tooan usługi Azure AD galerii aplikacji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toofind się, dlaczego inny zestaw użytkowników są udostępniane tooan aplikacji niż te, które miały"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Nieprawidłowy zestaw użytkowników są udostępnione tooan usługi Azure AD galerii aplikacji

Użytkowników, którzy są udostępnione toohello aplikacji głównie wynikają z których użytkownicy i grupy zostały **przypisane** toohello aplikacji.

Jak korzystać z zasobów hello poniżej toolearn toocheck, którzy użytkownicy i grupy z przypisanym tooan aplikacji w usłudze Azure Active Directory.

## <a name="assign-a-user-directly-as-an-administrator"></a>Przypisywanie użytkownika bezpośrednio jako administrator

tooassign jednej lub kilku użytkowników aplikacji tooan bezpośrednio, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.

9.  Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.

10. Typ w hello **Pełna nazwa** lub **adres e-mail** użytkownika hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.

11. Umieść kursor nad hello **użytkownika** w tooreveal listy hello **wyboru**. Kliknij przycisk hello wyboru dalej toohello użytkownika profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.

12. **Opcjonalnie:** Jeśli chcesz zbyt**dodać więcej niż jednego użytkownika**, typu w innym **Pełna nazwa** lub **adres e-mail** do hello **wyszukiwania według nazwy lub adresu e-mail** polu wyszukiwania, a następnie kliknij przycisk tooadd wyboru hello toohello tego użytkownika **wybrane** listy.

13. Po wybraniu użytkowników, kliknij przycisk hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.

14. **Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** tooselect bloku roli użytkowników toohello tooassign wybrano.

15. Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybranych użytkowników.

Jeśli Inicjowanie obsługi administracyjnej jest skonfigurowana i uruchomiona już aplikację, nowi użytkownicy powinna być elastycznie tooan aplikacji w ciągu 10 minut. Sprawdź hello **dzienników inspekcji** szczegółowe informacje.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Przypisz grupę bezpośrednio tooan aplikacji jako administrator

tooassign jeden lub więcej grup tooan aplikacji bezpośrednio, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma tooassign listy hello toofrom użytkownika.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **użytkowników i grup** z menu nawigacji po lewej stronie powitania aplikacji.

8.  Kliknij przycisk hello **Dodaj** przycisk na powitania **użytkowników i grup** hello tooopen listy **Dodaj przydziału** bloku.

9.  Kliknij przycisk hello **użytkowników i grup** selektora z hello **Dodaj przydziału** bloku.

10. Typ w hello **grupy Pełna nazwa** grupy hello planuje się przypisanie do hello **wyszukiwanie według nazwy lub adresu e-mail** pola wyszukiwania.

11. Umieść kursor nad hello **grupy** w tooreveal listy hello **wyboru**. Kliknij przycisk hello wyboru dalej toohello grupy profilu zdjęcie lub logo tooadd Twojego toohello użytkownika **wybrane** listy.

12. **Opcjonalnie:** czy zbyt**dodać więcej niż jednej grupy**, typu w innym **grupy Pełna nazwa** do hello **wyszukiwanie według nazwy lub adresu e-mail** pole wyszukiwania, i kliknij przycisk tooadd wyboru hello toohello tej grupy **wybrane** listy.

13. Po wybraniu grup kliknij hello **wybierz** tooadd przycisk ich toohello listę użytkowników i grup toobe przypisane toohello aplikacji.

14. **Opcjonalnie:** kliknij hello **wybierz rolę** selektora w hello **Dodaj przydziału** grupach bloku tooselect toohello tooassign roli zostały wybrane.

15. Kliknij przycisk hello **przypisać** toohello aplikacji hello tooassign przycisk wybrane grupy.

Jeśli Inicjowanie obsługi administracyjnej jest skonfigurowana i uruchomiona już aplikację, nowi użytkownicy, zawarte w grupie hello powinny być elastycznie tooan aplikacji w ciągu 10 minut. Sprawdź hello **dzienników inspekcji** szczegółowe informacje.

>[!IMPORTANT]
>Inicjowanie obsługi administracyjnej hello Nazwa grupy i grupowania szczegółów w elementach członkowskich toohello dodanie, jeśli obsługiwane w przypadku niektórych aplikacji. Można włączyć lub wyłączyć tę funkcję przez włączenie lub wyłączenie hello **mapowania** dla obiektów grupy pokazano hello **inicjowania obsługi administracyjnej** kartę. 
>
>

Jeśli inicjowania obsługi grup jest włączona, upewnij się, że tooreview hello atrybutu mapowania tooensure odpowiednie pole jest używany przez hello "zgodnym z Identyfikatorem". Może to być nazwa wyświetlana hello lub e-mail aliasu, jak hello grupy i jej elementów członkowskich nie można zainicjować obsługi administracyjnej Jeśli hello zgodnej właściwości jest pusta lub nie wypełnione grupy w usłudze Azure AD.

## <a name="next-steps"></a>Następne kroki
[Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji za pomocą usługi Azure Active Directory](active-directory-saas-app-provisioning.md)
