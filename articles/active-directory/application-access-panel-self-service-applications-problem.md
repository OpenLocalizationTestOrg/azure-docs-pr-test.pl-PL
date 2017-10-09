---
title: "za pomocą dostępu do aplikacji Sklep internetowy aaaProblem | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z dostępem powiązanych aplikacji usługi tooself problemów"
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
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a>Problem za pomocą dostępu do aplikacji Sklep internetowy

Dostęp do aplikacji Sklep internetowy jest doskonałym sposobem tooallow użytkowników tooself — odnajdywanie aplikacji, opcjonalnie zezwolić na dostęp tooapprove grupy biznesowej hello toothose aplikacji. Możesz zezwolić hello biznesowa grupy toomanage hello poświadczeń przypisanych użytkowników toothose jednokrotnego hasła w aplikacji bezpośrednio w ich panele dostępu.

Zanim użytkownicy mogą odnajdować własnym aplikacji z ich panel dostępu, należy tooenable **dostęp do aplikacji Sklep internetowy** tooany aplikacji, że chcesz tooself użytkowników tooallow — odnajdywania i zażądać dostępu do.

## <a name="general-issues-toocheck-first"></a>Ogólne problemy toocheck najpierw

-   Upewnij się, że poprawnie skonfigurowano dostęp do aplikacji Sklep internetowy. Zobacz "Jak tooconfigure samoobsługi aplikacji dostępu".

-   Upewnij się, że została hello użytkownikowi lub grupie dostęp do aplikacji Sklep internetowy toorequest włączone.

-   Upewnij się, że hello odwiedzania hello odpowiednie miejsce dostępu do aplikacji Sklep internetowy. Użytkownicy mogą przechodzić tootheir [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk hello **+ Dodaj** przycisk toofind hello aplikacji toowhich włączono samoobsługi dostępu.

-   Jeśli dostęp do aplikacji Sklep internetowy niedawno został skonfigurowany, ponów toosign i wylogowywanie do panelu dostępu użytkownika hello po kilku minutach toosee Jeśli pojawiły hello zmian samoobsługi dostępu.

## <a name="how-tooconfigure-self-service-application-access"></a>Jak uzyskać dostęp do aplikacji Sklep internetowy tooconfigure

tooenable samoobsługi aplikacji dostępu tooan aplikacji, wykonaj poniższe kroki hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello tooenable samoobsługi dostępu toofrom hello listy.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **samoobsługi** z menu nawigacji po lewej stronie powitania aplikacji.

8.  tooenable dostęp do aplikacji Sklep internetowy dla tej aplikacji, Włącz hello **użytkownicy aplikacji toothis dostępu toorequest?** Przełącz zbyt**tak.**

9.  Następnie tooselect hello grupy toowhich użytkowników, którzy żądają dostępu do aplikacji toothis powinny zostać dodane, kliknij przycisk Dalej etykiety toohello hello selektora **toowhich grupy należy przypisać użytkownicy dodani?** i wybierz grupę.

10. **Opcjonalnie:** w razie potrzeby toorequire zatwierdzenia firm przed użytkownicy mogą uzyskiwać dostęp, należy ustawić hello **wymagają zatwierdzenia przed udzieleniem im dostępu do aplikacji toothis?** Przełącz zbyt**tak**.

11. **Opcjonalnie: dla aplikacji za pomocą hasła jednokrotnego na tylko** w razie potrzeby tooallow tych firm osób zatwierdzających toospecify hello haseł, które są wysyłane toothis aplikacji dla zatwierdzonych użytkowników ustawić hello **tooset osób zatwierdzających Zezwalaj hasła użytkownika dla tej aplikacji?**  Przełącz zbyt**tak**.

12. **Opcjonalnie:** toospecify hello biznesowe osoby zatwierdzające mogą tooapprove dostępu toothis aplikacji, kliknij przycisk Dalej etykiety toohello hello selektora **użytkowników, którzy mają tooapprove dostępu toothis aplikacji?** tooselect w górę too10 biznesowe poszczególnych osób zatwierdzających.

 >[!NOTE]
 > Grupy nie są obsługiwane.
 >
 >

13. **Opcjonalnie:** **dla aplikacji, które ujawnia ról**, jeśli chcesz, aby tooassign roli tooa zatwierdzonych użytkowników samoobsługi, kliknij przycisk Dalej toohello selektora hello **toowhich roli należy przypisać użytkowników na tym aplikacji?**  tooselect hello roli toowhich powinien być przypisany tych użytkowników.

14. Kliknij przycisk hello **zapisać** przycisk u góry hello hello toofinish bloku.

Po zakończeniu konfiguracji samoobsługi aplikacji, użytkownicy mogą przechodzić tootheir [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk hello **+ Dodaj** przycisk toofind hello aplikacji toowhich włączono Dostęp z samoobsługi. Osób zatwierdzających firm również wyświetlone powiadomienie w ich [panelu dostępu aplikacji](https://myapps.microsoft.com/). Można włączyć wiadomość e-mail z informacją, gdy użytkownik zażąda dostępu tooan aplikację, która wymaga zatwierdzenia. 

Te zatwierdzenia obsługuje pojedynczy przepływów pracy, co oznacza, że możesz określić wiele osób zatwierdzających, wszelkie jedna osoba zatwierdzająca może zatwierdzić dostęp toohello aplikacji.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Jeśli te kroki rozwiązywania problemów nie rozwiąże problemu hello 

Otwórz bilet pomocy technicznej z następujących informacji, jeśli jest dostępna hello:

-   Identyfikator błędu korelacji

-   Nazwa UPN (adres e-mail użytkownika)

-   Dla identyfikatora dzierżawcy

-   Typ przeglądarki

-   Strefa czasowa i przedziału czasu/czasu podczas błąd występuje

-   Ślady fiddler

## <a name="next-steps"></a>Następne kroki
[Konfigurowanie usługi Azure Active Directory do zarządzania grupami samoobsługi](active-directory-accessmanagement-self-service-group-management.md)
