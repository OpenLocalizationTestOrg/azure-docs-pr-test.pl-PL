---
title: "Przypisanie aplikacji samoobsługi tooconfigure aaaHow | Dokumentacja firmy Microsoft"
description: "Włączanie samoobsługi aplikacji dostępu tooallow użytkowników toofind własne aplikacje"
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
ms.openlocfilehash: d25a0146c4c8cebf9c2ae8c516f094a8eccb4570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-self-service-application-assignment"></a>Jak tooconfigure samoobsługi aplikacji przypisania

Zanim użytkownicy mogą odnajdować własnym aplikacji z ich panel dostępu, należy tooenable **dostęp do aplikacji Sklep internetowy** tooany aplikacji, że chcesz tooself użytkowników tooallow — odnajdywania i zażądać dostępu do.

Ta funkcja jest to doskonały sposób toosave czas i pieniądze jako grupa IT i zdecydowanie zaleca się jako część wdrożenia nowoczesnych aplikacji w usłudze Azure Active Directory.

Za pomocą tej funkcji, można:

-   Zezwala użytkownikom na własnym odnajdywanie aplikacji hello [panelu dostępu aplikacji](https://myapps.microsoft.com/) bez bothering hello IT grupy.

-   Dodaj tych użytkowników tooa wstępnie skonfigurowane grupy, aby zobaczyć, kto żąda dostępu, usunięcie dostępu i zarządzanie rolami hello przypisane toothem.

-   Opcjonalnie dopuszczają zatwierdzająca firm żądań dostępu do aplikacji tooapprove hello grupa IT nie ma.

-   Opcjonalnie skonfiguruj się too10 osób, które może zatwierdzić dostęp toothis aplikacji.

-   Opcjonalnie Zezwalaj zatwierdzająca firm tooset hello hasła użytkownicy ci mogą używać toosign w aplikacji toohello z hello firm zatwierdzająca [panelu dostępu aplikacji](https://myapps.microsoft.com/).

-   Opcjonalnie automatycznie przypisywać bezpośrednio roli aplikacji tooan przypisanych użytkowników samoobsługi.

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a>Włączanie samoobsługi aplikacji dostępu tooallow użytkowników toofind własne aplikacje

Dostęp do aplikacji Sklep internetowy jest doskonałym sposobem tooallow użytkowników tooself — odnajdywanie aplikacji, opcjonalnie zezwolić na dostęp tooapprove grupy biznesowej hello toothose aplikacji. Możesz zezwolić hello biznesowa grupy toomanage hello poświadczeń przypisanych użytkowników toothose jednokrotnego hasła w aplikacji bezpośrednio w ich panele dostępu.

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
   >Grupy nie są obsługiwane.
   >
   >

13. **Opcjonalnie:** **dla aplikacji, które ujawnia ról**, jeśli chcesz, aby tooassign roli tooa zatwierdzonych użytkowników samoobsługi, kliknij przycisk Dalej toohello selektora hello **toowhich roli należy przypisać użytkowników na tym aplikacji?**  tooselect hello roli toowhich powinien być przypisany tych użytkowników.

14. Kliknij przycisk hello **zapisać** przycisk u góry hello hello toofinish bloku.

Po zakończeniu konfiguracji samoobsługi aplikacji, użytkownicy mogą przechodzić tootheir [panelu dostępu aplikacji](https://myapps.microsoft.com/) i kliknij przycisk hello **+ Dodaj** przycisk toofind hello aplikacji toowhich włączono Dostęp z samoobsługi. Osób zatwierdzających firm również wyświetlone powiadomienie w ich [panelu dostępu aplikacji](https://myapps.microsoft.com/). Można włączyć wiadomość e-mail z informacją, gdy użytkownik zażąda dostępu tooan aplikację, która wymaga zatwierdzenia. 

Te zatwierdzenia obsługuje pojedynczy przepływów pracy, co oznacza, że jeśli określisz wiele osób zatwierdzających żadnych jedna osoba zatwierdzająca może aplikacji toohello dostęp osoby zatwierdzającej.

## <a name="next-steps"></a>Następne kroki
[Konfigurowanie usługi Azure Active Directory do zarządzania grupami samoobsługi](active-directory-accessmanagement-self-service-group-management.md)
