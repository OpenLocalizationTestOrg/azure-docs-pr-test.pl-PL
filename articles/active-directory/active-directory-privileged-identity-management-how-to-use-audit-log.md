---
title: "Dziennik inspekcji hello toouse aaaHow w usłudze Azure AD Privileged Identity Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dziennika inspekcji hello toouse hello Azure Privileged Identity Management rozszerzenia."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>Za pomocą dziennika inspekcji hello w PIM
Można użyć toosee dziennik inspekcji zarządzania tożsamości uprzywilejowanych (PIM) hello wszystkich przypisań użytkownika hello i aktywacji w danym okresie. Jeśli chcesz toosee hello inspekcji pełnej historii aktywności w dzierżawie, w tym administratora, użytkownika i działania synchronizacji, można użyć hello [raportów dotyczących dostępu i użycia usługi Azure Active Directory.](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>Przejdź toohello dziennik inspekcji
Z hello [portalu Azure](https://portal.azure.com) pulpitu nawigacyjnego, wybierz hello **Azure AD Privileged Identity Management** aplikacji. Z tego miejsca, uzyskać dostęp do dziennika inspekcji hello klikając **Zarządzanie ról uprzywilejowanych** > **Historia inspekcji** hello PIM w pulpicie nawigacyjnym.

## <a name="hello-audit-log-graph"></a>Wykres dziennika inspekcji Hello
W wykres liniowy służy hello inspekcji dziennika tooview hello łączna liczba aktywacji, max aktywacji dziennie i średnie aktywacji na dzień.  Można także filtrować dane hello przez rolę, jeśli istnieje więcej niż jednej roli w hello Historia inspekcji.

Użyj hello **czasu**, **akcji**, i **roli** przyciski toosort hello dziennika.

## <a name="hello-audit-log-list"></a>Lista dzienników inspekcji Hello
kolumny Hello hello na liście dziennika inspekcji są:

* **Obiekt żądający** — użytkownik hello wymagane uaktywnienie roli hello lub zmiany.  Jeśli jest "Systemu Azure" hello, sprawdź dziennik inspekcji Azure hello, aby uzyskać więcej informacji.
* **Użytkownik** -hello użytkownika, który jest uaktywnianie lub przypisaną rolę tooa.
* **Rola** -roli hello przypisane lub aktywowany przez użytkownika hello.
* **Akcja** — Witaj akcje wykonywane przez obiekt żądający hello. Może to obejmować przypisania, anulowaniu, aktywacji lub dezaktywacji.
* **Czas** — gdy akcja hello wystąpił.
* **Uzasadnienie** — Jeśli dowolny tekst została wprowadzona w polu Przyczyna hello podczas aktywacji, pojawi się tutaj.
* **Wygaśnięcie** — tylko istotne dla aktywacji ról.

## <a name="filter-hello-audit-log"></a>Dziennik inspekcji hello filtru
Można filtrować hello informacje, które zostaną wyświetlone w dzienniku inspekcji hello klikając hello **filtru** przycisku.  Witaj **bloku parametry wykresu aktualizacji** będą wyświetlane.

Po ustawieniu filtrów powitania kliknij **aktualizacji** toofilter hello danych w dzienniku hello.  Jeśli dane hello nie występuje od razu, Odśwież stronę hello.

### <a name="change-hello-date-range"></a>Zmień zakres dat hello
Użyj hello **dzisiaj**, **zeszłym tygodniu**, **ostatnim miesiącu**, lub **niestandardowy** przyciski przedział czasu hello toochange hello dziennika inspekcji.

Po wybraniu hello **niestandardowy** przycisku, będziesz mieć możliwość **z** Data i **do** Data toospecify pola zakres dat dla hello dziennika.  Możesz wprowadzić hello daty w formacie MM/DD/RRRR lub kliknięcie hello **kalendarza** ikonę i wybierz hello datę z kalendarza.

### <a name="change-hello-roles-included-in-hello-log"></a>Zmiany zawarte w dzienniku hello ról hello
Zaznaczenie lub usunięcie zaznaczenia hello **roli** wyboru dalej tooeach roli tooinclude lub wyklucz go z hello logowania.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

