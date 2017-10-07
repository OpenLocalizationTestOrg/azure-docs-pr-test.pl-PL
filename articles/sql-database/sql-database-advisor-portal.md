---
title: "zalecenia wydajności aaaApply — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Można użyć hello toofind portalu Azure wydajności zaleceń, które można zoptymalizować wydajność bazy danych SQL Azure lub toocorrect niektórych problem wskazany w obciążenie."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>Znajdź i stosować zalecenia wydajności

Można użyć hello toofind portalu Azure wydajności zaleceń, które można zoptymalizować wydajność bazy danych SQL Azure lub toocorrect niektórych problem wskazany w obciążenie. **Zalecenie wydajności** strony w portalu Azure umożliwia toofind hello najlepsze rekomendacje na potencjalnego wpływu na ich podstawie. 

## <a name="viewing-recommendations"></a>Przeglądanie zaleceniami

tooview i stosować zalecenia dotyczące wydajności, należy hello poprawne [kontroli dostępu opartej na rolach](../active-directory/role-based-access-control-what-is.md) uprawnienia na platformie Azure. **Czytnik**, **Współautor bazy danych SQL** zalecenia tooview wymagane są uprawnienia i **właściciela**, **Współautor bazy danych SQL** uprawnienia są wymagane tooexecute wszystkie akcje; Utwórz lub Porzuć indeksy i anulowanie tworzenia indeksu.

Użyj hello następujące zalecenia dotyczące wydajności toofind kroki w portalu Azure:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Przejdź za**więcej usług** > **baz danych**i wybierz bazę danych.
3. Przejdź za**wydajności zalecenie** tooview dostępne zalecenia dotyczące hello wybranej bazy danych.

Zalecenia dotyczące wydajności są shonw w hello tabeli podobne toohello przedstawionego na następującej ilustracji hello:

![Zalecenia](./media/sql-database-advisor-portal/recommendations.png)

Zalecenia są sortowane według ich potencjalny wpływ na wydajność w hello następujące kategorie:

| Wpływ | Opis |
|:--- |:--- |
| Wysoka |Duże znaczenie zalecenia powinien zapewnić hello najbardziej znaczący wpływ na wydajność. |
| Medium |Średni wpływ zalecenia należy zwiększyć wydajność, ale nie w znacznym stopniu. |
| Niska |Niski wpływ zalecenia należy zapewnić lepszą wydajność niż bez, ale ulepszenia może być niewielka. |


> [!NOTE]
> Baza danych SQL Azure wymaga działania toomonitor co najmniej dzień w kolejności tooidentify kilka zaleceń. Hello bazy danych SQL Azure łatwiej można zoptymalizować wzorców spójne zapytania nie może uzyskać losowe spotty seria działań. Jeśli zalecenia nie są dostępne corrently, hello **wydajności zalecenie** strona zawiera komunikat wyjaśniający, dlaczego.
> 

Można również wyświetlić stan hello hello historyczne operacje. Wybierz toosee zalecenia lub stan więcej szczegółów.

Oto przykład "Create index" zalecenia w hello portalu Azure.

![Tworzenie indeksu](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>Zalecenia dotyczące stosowania
Baza danych SQL Azure umożliwia pełną kontrolę nad jak zalecenia są włączone, przy użyciu dowolnego hello następujące trzy opcje: 

* Zastosuj poszczególne zalecenia co naraz.
* Włącz hello automatycznego dostrajania tooautomatically stosować zalecenia.
* tooimplement zalecenie uruchomić ręcznie, hello zalecane skryptu T-SQL bazy danych.

Wybierz wszystkie zalecenia tooview jego szczegóły, a następnie kliknij przycisk **wyświetlić skryptu** tooreview hello szczegółowe dane dotyczące sposobu tworzenia hello zalecenia.

Witaj bazy danych pozostaje w trybie online, gdy zastosowano zalecenie hello — przy użyciu zalecenie wydajności lub automatycznego dostrajania nigdy nie ma bazy danych w trybie offline.

### <a name="apply-an-individual-recommendation"></a>Zastosuj poszczególne zalecenia.
Można przeczytaj i zaakceptuj zalecenia jednym naraz.

1. Na powitania **zalecenia** bloku, wybierz zalecenia.
2. Na powitania **szczegóły** kliknij bloku **Zastosuj** przycisku.
   
    ![Zastosuj zalecenia](./media/sql-database-advisor-portal/apply.png)

Zalecenie wybrane zostaną zastosowane na powitania bazy danych.

### <a name="removing-recommendations-from-hello-list"></a>Usuwanie z listy hello zalecenia
Jeśli lista zaleceń zawiera elementy, które mają tooremove z listy hello, można odrzucić hello zalecenia:

1. Wybierz zalecenie liście hello **zalecenia** tooopen hello szczegóły.
2. Kliknij przycisk **odrzucić** na powitania **szczegóły** bloku.

W razie potrzeby można dodać odrzucone elementy kopii toohello **zalecenia** listy:

1. Na powitania **zalecenia** kliknij bloku **widoku odrzucone**.
2. Zaznacz element odrzuconych tooview listy hello jego szczegóły.
3. Opcjonalnie kliknij **Cofnij odrzucić** tooadd hello indeksu wstecz toohello główną listę **zalecenia**.


### <a name="enable-automatic-tuning"></a>Włączanie automatycznego dostrajania
Można ustawić hello bazy danych SQL Azure tooimplement zalecenia automatycznie. Zgodnie z zaleceniami staną się dostępne automatycznie zostaną one zastosowane. Jako wszystkie zalecenia zarządza hello usługi, jeśli hello wpływ na wydajność jest ujemny hello zalecenie zostaną cofnięte.

1. Na powitania **zalecenia** bloku, kliknij przycisk **automatyzacja**:
   
    ![Ustawienia usługi Advisor](./media/sql-database-advisor-portal/settings.png)
2. Wybierz akcje tooautomate:
   
    ![Zalecane indeksy](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>Ręcznie uruchom hello zalecane skryptu T-SQL
Wybierz każde zalecenie, a następnie kliknij przycisk **Wyświetl skrypt**. Uruchom ten skrypt bazy danych toomanually zastosować zalecenie hello.

*Indeksy, które są wykonywane ręcznie nie są monitorowane i weryfikowane pod kątem wpływu na wydajność przez usługę hello* , zaleca się monitorowanie tych indeksów po utworzeniu tooverify one zapewniają większą wydajność i dostosować lub usuń je, jeśli niezbędne. Aby uzyskać więcej informacji o tworzeniu indeksów, zobacz [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).

### <a name="canceling-recommendations"></a>Anulowanie zalecenia
Zalecenia, które znajdują się w **oczekujące**, **weryfikacji**, lub **Powodzenie** stanu mogą zostać anulowane. Zalecenia dotyczące ze stanem **Executing** nie można anulować.

1. Wybierz zalecenie hello **dostrajanie historii** hello tooopen obszaru **szczegóły zalecenia** bloku.
2. Kliknij przycisk **anulować** tooabort hello proces stosowania hello zalecenia.

## <a name="monitoring-operations"></a>Operacje monitorowania
Zalecamy stosowanie może odbywa się natychmiast. Hello portal zawiera szczegółowe informacje dotyczące stanu hello zalecenia. Witaj poniżej przedstawiono możliwe stany, które można indeksu w:

| Stan | Opis |
|:--- |:--- |
| Oczekujące |Zastosuj zalecenie polecenie zostało odebrane i jest zaplanowane do uruchomienia. |
| Wykonywanie |zalecenie Hello jest stosowany. |
| Weryfikowanie |Zalecenie zostało pomyślnie zastosowane i usługi hello jest pomiaru hello korzyści. |
| Powodzenie |Zalecenie zostało pomyślnie zastosowane i zostały zmierzone korzyści. |
| Błąd |Wystąpił błąd podczas procesu hello stosowania hello zalecenia. Może to być przejściowy problem lub toohello zmiany schematu tabeli i hello skryptu nie jest już prawidłowy. |
| Przywracanie |zalecenie Hello została zastosowana, ale został uznany za z systemem innym niż wydajność i zostanie automatycznie przywrócony. |
| Przywrócono |zalecenie Hello została przywrócona. |

Kliknij w trakcie zalecenie toosee listy hello więcej szczegółów:

![Zalecane indeksy](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>Przywrócenie zalecenia
Jeśli użyto hello wydajności zalecenia tooapply hello zalecenie (co oznacza, że nie został ręcznie uruchomiony skryptu hello T-SQL) automatycznie zostanie przywrócona jego przypadku ich znalezienia hello wydajności wpływ toobe ujemna. Przyczyny po prostu chcesz toorevert zalecenia należy hello następujące czynności:

1. Wybierz zalecenie pomyślnie zastosowane w hello **dostrajanie historii** obszaru.
2. Kliknij przycisk **Przywróć** na powitania **szczegóły zalecenia** bloku.

![Zalecane indeksy](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>Wpływ na wydajność monitorowania zalecenia dotyczące indeksu
Po pomyślnie zostały zaimplementowane zalecenia (obecnie indeksu operacji i parametryzacja zapytań zalecenia tylko) możesz kliknąć **szczegółowe informacje o zapytań** na powitania zalecenie szczegóły blok tooopen [zapytania Szczegółowe informacje o wydajności](sql-database-query-performance.md) zobaczyć wpływ na wydajność hello top zapytań.

![Wpływ na wydajność monitora](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>Podsumowanie
Baza danych SQL Azure zawiera zalecenia dotyczące poprawy wydajności bazy danych SQL. Zapewniając skryptów T-SQL, a także osoby i pełni — automatyczne, otrzymasz przydatne pomocy w optymalizacji bazy danych i ostatecznie poprawę wydajności zapytań.

## <a name="next-steps"></a>Następne kroki
Monitorowanie zalecenia i kontynuować tooapply ich toorefine wydajności. Obciążeń bazy danych są dynamiczne i zmienianie w sposób ciągły. Baza danych SQL Azure będzie kontynuować toomonitor i podano zalecenia, które może potencjalnie podnieść wydajność bazy danych. 

* Zobacz [automatycznego dostrajania](sql-database-automatic-tuning.md) hello toolearn więcej na temat automatycznego dostrajania w bazie danych SQL Azure.
* Zobacz [zaleceń](sql-database-advisor.md) omówienie zaleceń wydajności bazy danych SQL Azure.
* Zobacz [szczegółowe informacje o wydajności zapytań](sql-database-query-performance.md) toolearn o wyświetlaniu hello wpływ na wydajność kwerend top.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Magazyn zapytań](https://msdn.microsoft.com/library/dn817826.aspx)
* [TWORZENIE INDEKSU](https://msdn.microsoft.com/library/ms188783.aspx)
* [Kontrola dostępu oparta na rolach](../active-directory/role-based-access-control-what-is.md)

