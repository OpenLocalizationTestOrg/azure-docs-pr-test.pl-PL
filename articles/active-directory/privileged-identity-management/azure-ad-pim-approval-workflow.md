---
title: "aaaAzure Privileged Identity Management przepływów pracy | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat przepływów pracy w zarządzania tożsamości uprzywilejowanych (PIM)"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>Zatwierdzenia (wersja zapoznawcza)

## <a name="overview"></a>Omówienie

Z zatwierdzenia Privileged Identity Management można skonfigurować role toorequire zatwierdzenia dla aktywacji i wybrać jednego lub wielu użytkowników lub grup tak delegowani osób zatwierdzających. Zachowaj jak odczytywania toolearn tooconfigure ról i wybierz osób zatwierdzających.

>[!NOTE]
Pamiętaj, ta funkcja jest nadal w rozwoju i mogą wystąpić błędy. Funkcje Hello, łącznie z tekstem i konwencje nazewnictwa mogą ulec zmianie, a nie należy traktować jako ostatecznego.


## <a name="key-terminology"></a>Kluczową terminologię

*Kwalifikujące się roli użytkownika* — kwalifikujących się roli użytkownik jest użytkownikiem w organizacji, któremu przypisano rolę tooan usługi Azure AD jako uprawniających (rola wymaga aktywacji).

*Delegowane osoba zatwierdzająca* — delegowanego osoba zatwierdzająca jest jednego lub wielu osób lub grup w ramach usługi Azure AD, odpowiedzialnych za zatwierdzanie żądań dla roli aktywacji.

## <a name="scenarios"></a>Scenariusze

Witaj prywatnej wersji zapoznawczej obsługuje hello następujące scenariusze:

**Jako uprzywilejowane roli administratora pararozaniliny można wykonywać następujące czynności:**

-   [Włącz zatwierdzenia dla określonych ról](#enable-approval-for-specific-roles)

-   [Określ żądań tooapprove osoba zatwierdzająca użytkowników i/lub grup](#specify-approver-users-and/or-groups-to-approve-requests)

-   [Wyświetl historię żądań i zatwierdzania dla wszystkich ról uprzywilejowanych](#view-request-and-approval-history-for-all-privileged-roles)

**Wyznaczone osoby zatwierdzającej można:**

-   [Wyświetlanie oczekujących zatwierdzeń (liczba żądań)](#view-pending-approvals-requests)

-   [Zatwierdzanie lub odrzucanie żądań w celu podniesienia roli (pojedynczego i/lub masowo)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [Podaj uzasadnienie dla moich lub odrzuceniu](#provide-justification-for-my-approval/rejection) 

**Kwalifikujące się roli użytkownika może:**

-   [żądanie aktywacji roli, która wymaga zatwierdzenia](#request-activation-of-a-role-that-requires-approval)

-   [Wyświetlanie stanu hello tooactivate Twojego żądania](#view-the-status-of-your-request-to-activate)

-   [wykonać zadanie w usłudze Azure AD, jeśli Aktywacja została zatwierdzona](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a>Nawigacji

Zaktualizowaliśmy hello nawigacji toosupport zatwierdzenia

![](media/azure-ad-pim-approval-workflow/image001.png)

Witaj domyślna strona docelowa zawiera tooinformation najwygodniejszy dostęp o PIM i hello Nowa dokumentacja zatwierdzenia.

![](media/azure-ad-pim-approval-workflow/image002.png)

Dodaliśmy również nową sekcję dla wszystkich użytkowników PIM, "Moje Historia inspekcji". W tym miejscu można znaleźć wszystkie hello informacje istotne tooyour tożsamości. W tym wszystkie swoje żądania oczekujące i ukończone, wszelkich decyzji, których dokonano hello żądań, które należy rozwiązać i wszystkich poprzednich aktywacji roli w jednej lokalizacji.

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>Włącz zatwierdzenia dla określonych ról

tooenable zatwierdzenia dla konkretnej roli, najpierw wybierz role katalogu z hello nawigacji po lewej stronie.

![](media/azure-ad-pim-approval-workflow/image004.png)

Znajdź i wybierz ustawienia w hello nawigacji po lewej stronie ról katalogu

![](media/azure-ad-pim-approval-workflow/image006.png)

Wybierz role uprzywilejowane:

![](media/azure-ad-pim-approval-workflow/image009.png)

Zaznacz pole wyboru "Włącz" w hello wymagają zatwierdzenia sekcji:

![](media/azure-ad-pim-approval-workflow/image011.png)

Po włączeniu bloku hello rozwinie hello tooshow poniższe informacje:

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
Jeśli nie określono żadnych osób zatwierdzających, hello PRA(s) stają się osoby zatwierdzające domyślne hello. PRA(s) może być wymagane tooapprove aktywacji wszystkie żądania dla tej roli.

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>Określ żądań tooapprove osoba zatwierdzająca użytkowników i/lub grup

zatwierdzenie toodelegate, kliknij opcję hello zbyt "Wybierz osób zatwierdzających":

![](media/azure-ad-pim-approval-workflow/image015.png)

Podczas ładowania bloku wybierz osób zatwierdzających hello może wyszukać określonego użytkownika lub grupy za pomocą hello pasek wyszukiwania w górnej hello lub wybrać z listy wstępnie wypełnione hello, a następnie kliknij "Wybierz" po zakończeniu:

![](media/azure-ad-pim-approval-workflow/image017.png)

Uwaga: Można wybrać wielu użytkowników lub grup w czasie.

Wybór pojawi się w wybranej listy hello, jak pokazano poniżej:

![](media/azure-ad-pim-approval-workflow/image019.png)

tooremove osoba zatwierdzająca, wystarczy kliknąć hello Usuń przycisku Dalej tootheir nazwę.

tooadd dodatkowe osób zatwierdzających, proces hello powtarzania.

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>Wyświetl historię żądań i zatwierdzania dla wszystkich ról uprzywilejowanych

Historia żądania i zatwierdzania tooview dla wszystkich ról uprzywilejowanych, wybierz Historia inspekcji z pulpitu nawigacyjnego hello:

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
Sortowanie danych hello przez akcję i wyszukaj "Zatwierdzone aktywacji"

### <a name="view-pending-approvals-requests"></a>Wyświetlanie oczekujących zatwierdzeń (liczba żądań)

Zatwierdzającą delegowanego będzie otrzymywał powiadomienia e-mail, kiedy żądanie oczekuje na zatwierdzenie. tooview te żądania w portalu usługi PIM hello, na karcie Wybierz hello "oczekujących żądań zatwierdzenia" Pulpit nawigacyjny (w nawigacji nowe hello) w hello lewym pasku nawigacyjnym.

![](media/azure-ad-pim-approval-workflow/image023.png)

Z tego miejsca zobaczysz listę żądania w oczekiwaniu na zatwierdzenie:

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>Zatwierdzanie lub odrzucanie żądań w celu podniesienia roli (pojedynczego i/lub masowo)

Wybierz hello żądania ma tooapprove lub odmowy i kliknij przycisk hello w pasku akcji, który odpowiada decyzji:

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>Podaj uzasadnienie dla moich lub odrzuceniu

Będzie to Otwórz nowe tooapprove bloku lub odrzucanie jednocześnie wiele żądań. Wprowadź uzasadnienie decyzji, i kliknij przycisk Zatwierdź (lub Odmów) hello lub bloku hello:

![](media/azure-ad-pim-approval-workflow/image029.png)

Po zakończeniu procesu żądania hello hello symbolu stanu będzie odzwierciedlać wprowadzone decyzji (w tym przykładzie decyzji hello jest zatwierdzić):

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>Żądania aktywacji roli, która wymaga zatwierdzenia

Żądanie aktywacji roli, który wymaga zatwierdzenia można zainicjować z hello starego PIM nawigacji lub hello nowe nawigacji, jako proces hello roli aktywacji pozostaje hello takie same. Po prostu wybierz rolę z listy hello ról do aktywacji:

![](media/azure-ad-pim-approval-workflow/image033.png)

Jeśli ról uprzywilejowanych wymaga uwierzytelniania wieloskładnikowego, zostanie wyświetlony monit przeprowadzenie tego zadania:

![](media/azure-ad-pim-approval-workflow/image035.png)

Po jego zakończeniu, kliknij przycisk Aktywuj i uzasadnić (jeśli jest to wymagane):

![](media/azure-ad-pim-approval-workflow/image037.png)

obiektu żądającego Hello pojawią się, że powiadomienie, które hello żądania oczekuje na zatwierdzenie:

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>Wyświetlanie stanu hello tooactivate Twojego żądania

Wyświetlanie stanu hello tooactivate oczekujące żądania musi być dostępny z nowego nawigacji. Z hello paska nawigacji po lewej stronie wybierz kartę "Moje żądania" hello:

![](media/azure-ad-pim-approval-workflow/image041.png)

Stan żądania Hello zbyt domyślne "Oczekujące", ale może przełączyć toosee wszystkie lub odrzucone żądania.

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>Wykonać zadanie w usłudze Azure AD, jeśli Aktywacja została zatwierdzona

Po zatwierdzeniu żądania hello rola hello jest aktywna i może kontynuować pracę, która wymaga tej roli.

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>Następne kroki

Twoja opinia jest przydatna toous. Wyślij komentarze wolnego tooshare lub opinii z nami tutaj!
