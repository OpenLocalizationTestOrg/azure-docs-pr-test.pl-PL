---
title: "Pamięć aaaIn OLTP poprawia wydajności transakcji SQL | Dokumentacja firmy Microsoft"
description: "OLTP w pamięci przyjąć tooimprove transakcyjnych wydajności w istniejącej bazy danych SQL."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>Użyj OLTP w pamięci tooimprove wydajność aplikacji w bazie danych SQL
[OLTP w pamięci](sql-database-in-memory.md) może być wydajności hello tooimprove używane przetwarzanie transakcji, wprowadzanie danych i scenariusze przejściowej danych w [Premium](sql-database-service-tiers.md) baz danych SQL Azure bez zwiększania hello warstwę cenową. 

> [!NOTE] 
> Dowiedz się, jak [kworum podwaja obciążenia klucza bazy danych podczas opuszczania jednostek dtu w warstwie 70% z bazy danych SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)


Wykonaj te kroki tooadopt OLTP w pamięci w istniejącej bazie danych.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>Krok 1: Upewnij się, że w przypadku korzystania z bazy danych — warstwa Premium
OLTP w pamięci jest obsługiwana tylko w bazach danych Premium. W pamięci jest obsługiwany, jeśli hello zwrócony wynik 1 (nie 0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP* oznacza *Extreme przetwarzania transakcji*



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>Krok 2: Określenie tooIn toomigrate obiektów pamięci OLTP
Obejmuje narzędzia SSMS **omówienie analizy wydajności transakcji** raport, który można uruchomić na bazie danych z aktywnego obciążenia. Raport Hello identyfikuje tabele i procedury składowane, przeznaczone do migracji pamięci tooIn OLTP.

W programie SSMS toogenerate hello raportu:

* W hello **Eksplorator obiektów**, kliknij prawym przyciskiem myszy węzeł bazy danych.
* Kliknij przycisk **raporty** > **raportów standardowych** > **omówienie analizy wydajności transakcji**.

Aby uzyskać więcej informacji, zobacz [Określanie tabela lub przechowywane procedury powinny być przenoszone OLTP pamięci tooIn](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>Krok 3: Tworzenie testu można porównywać pod względem bazy danych
Załóżmy, że raport hello wskazuje bazy danych zawiera tabelę, która będzie korzystać z przekonwertować tabel zoptymalizowanych pod kątem pamięci tooa. Zaleca się najpierw przetestować wskazanie hello tooconfirm podczas testów.

Należy kopię bazy danych produkcyjnych. Witaj testu baza danych powinna być na powitania samym poziomie usług, warstwy jako baza danych w środowisku produkcyjnym.

tooease testowania, dostosować bazy danych testu w następujący sposób:

1. Połączenia bazy danych testów toohello przy użyciu narzędzia SSMS.
2. tooavoid wymagające hello opcji WITH (SNAPSHOT) w zapytaniach, należy ustawić opcję bazy danych hello, jak pokazano w powitania po instrukcji T-SQL:
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>Krok 4: Migrowanie tabel
Należy utworzyć i wypełnić kopię zoptymalizowanych pod kątem pamięci tabeli hello ma tootest. Można go utworzyć za pomocą:

* Witaj przydatną Kreator optymalizacji pamięci w programie SSMS.
* Ręczne T-SQL.

#### <a name="memory-optimization-wizard-in-ssms"></a>Kreator optymalizacji pamięci w programie SSMS
toouse tej opcji migracji:

1. Połączenie bazy danych testów toohello z SSMS.
2. W hello **Eksplorator obiektów**, kliknij prawym przyciskiem myszy na powitania tabeli, a następnie kliknij przycisk **Advisor optymalizacji pamięci**.
   
   * Witaj **Advisor optymalizacji pamięci tabeli** zostanie wyświetlony Kreator.
3. W Kreatorze powitania kliknij **weryfikacji migracji** (lub hello **dalej** przycisk) toosee, jeśli tabela hello ma jakiekolwiek nieobsługiwane funkcje, które nie są obsługiwane w tabelach zoptymalizowanych pod kątem pamięci. Aby uzyskać więcej informacji, zobacz:
   
   * Witaj *Lista kontrolna optymalizacji pamięci* w [Advisor optymalizacji pamięci](http://msdn.microsoft.com/library/dn284308.aspx).
   * [Konstrukcje języka Transact-SQL nie są obsługiwane przez OLTP w pamięci](http://msdn.microsoft.com/library/dn246937.aspx).
   * [Migrowanie OLTP pamięci tooIn](http://msdn.microsoft.com/library/dn247639.aspx).
4. Jeśli hello tabela nie zawiera nieobsługiwany funkcji, hello advisor może wykonywać hello rzeczywiste schematu i migracji danych dla Ciebie.

#### <a name="manual-t-sql"></a>Ręczne T-SQL
toouse tej opcji migracji:

1. Połączenia bazy danych testów tooyour przy użyciu narzędzia SSMS (lub podobny narzędzia).
2. Uzyskaj hello pełną skryptu T-SQL dla tabeli i jego indeksy.
   
   * W programie SSMS kliknij prawym przyciskiem myszy węzeł tabeli.
   * Kliknij przycisk **skryptu tabeli jako** > **utworzyć** > **okna nowej kwerendy**.
3. W oknie Skrypt hello, Dodaj WITH (MEMORY_OPTIMIZED = ON) toohello instrukcji CREATE TABLE.
4. Jeśli istnieje indeks KLASTROWANY, zmień go tooNONCLUSTERED.
5. Zmień nazwę istniejącej tabeli hello przy użyciu obiekt SP_RENAME.
6. Utworzenie hello nowe zoptymalizowanych pod kątem pamięci kopii tabeli hello, uruchamiając skrypt CREATE TABLE edytowany.
7. Kopiuj hello danych tooyour zoptymalizowanych pod kątem pamięci tabeli za pomocą INSERT... WYBIERZ * DO:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>Krok 5 (opcjonalny): Migrowanie procedury składowane
Witaj w pamięci funkcji można również zmodyfikować procedury składowanej zwiększonej wydajności.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Zagadnienia w procedurach składowanych skompilowanych w sposób macierzysty
Procedurę składowaną skompilowanych w sposób macierzysty musi mieć następujące opcje w jej klauzula T-SQL z hello:

* OPCJĘ WITH NATIVE_COMPILATION
* SCHEMABINDING: tabel znaczenie, które hello procedury składowanej nie może mieć ich definicje kolumn zmienione w dowolny sposób, które będą wpływać na powitania przechowywane procedury, chyba że porzucić hello przechowywane procedury.

Moduł macierzysty muszą używać jednej big [bloków ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) zarządzania transakcji. Brak role jawne BEGIN TRANSACTION lub ROLLBACK TRANSACTION. Jeśli kod wykryje naruszenie reguł biznesowych, może obsłużyć hello atomic blok z [THROW](http://msdn.microsoft.com/library/ee677615.aspx) instrukcji.

### <a name="typical-create-procedure-for-natively-compiled"></a>Typowy CREATE PROCEDURE dla skompilowanych w sposób macierzysty
Zazwyczaj toocreate hello T-SQL skompilowanych w sposób macierzysty procedury składowanej jest podobne toohello następującego szablonu:

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* W przypadku hello TRANSACTION_ISOLATION_LEVEL MIGAWKI jest hello najbardziej typowe wartości dla skompilowanych w sposób macierzysty hello przechowywanej procedury. Jednak podzbiór hello inne wartości są również obsługiwane:
  
  * REPEATABLE READ
  * MOŻLIWY DO SERIALIZACJI
* Witaj wartość języka musi być obecny w widoku sys.languages hello.

### <a name="how-toomigrate-a-stored-procedure"></a>Jak toomigrate procedury składowanej
kroki migracji Hello są:

1. Uzyskaj hello CREATE PROCEDURE skryptu toohello regularne interpretowany procedury składowanej.
2. Należy zmodyfikować jej nagłówka toomatch hello poprzedniego szablonu.
3. Należy upewnić się, czy procedury przechowywane hello kodu T-SQL korzysta z żadnych funkcji, które nie są obsługiwane dla procedur składowanych skompilowanych w sposób macierzysty. Implementowanie rozwiązania, w razie potrzeby.
   
   * Aby uzyskać więcej informacji, zobacz [problemy przy migracji dla natywnie skompilowany na procedur składowanych](http://msdn.microsoft.com/library/dn296678.aspx).
4. Zmień nazwę procedury składowanej starego hello przy użyciu obiekt SP_RENAME. Lub po prostu UPUSZCZANIA.
5. Uruchom skrypt edytowany Tworzenie procedury T-SQL.

## <a name="step-6-run-your-workload-in-test"></a>Krok 6: Uruchamianie obciążenia w teście
Uruchom obciążenia w sieci testowej bazy danych jest podobne obciążenia toohello działający w sieci produkcyjnej bazy danych. To powinno ujawnić, bardziej wydajne hello realizowane za korzystanie z funkcji w pamięci hello tabele i procedury składowane.

Atrybuty głównych obciążenia hello są:

* Liczba równoczesnych połączeń.
* Stosunek odczytu/zapisu.

tootailor i hello wykonywania testu obciążenia, należy rozważyć użycie hello ostress.exe przydatne narzędzie, które przedstawiono w [tutaj](sql-database-in-memory.md).

Opóźnienie sieci toominimize, uruchom test w hello tym samym regionie geograficznym Azure gdzie hello baza danych istnieje.

## <a name="step-7-post-implementation-monitoring"></a>Krok 7: Monitorowanie po wdrożeniu
Należy rozważyć monitorowanie wydajności hello skutków implementacjach użytkownika w pamięci w środowisku produkcyjnym:

* [Monitorowanie magazynu w pamięci](sql-database-in-memory-oltp-monitoring.md).
* [Monitorowanie usługi Azure SQL Database przy użyciu dynamicznych widoków zarządzania](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>Powiązane linki
* [(Optymalizacja w pamięci) OLTP w pamięci](http://msdn.microsoft.com/library/dn133186.aspx)
* [Wprowadzenie tooNatively skompilowanych procedur składowanych](http://msdn.microsoft.com/library/dn133184.aspx)
* [Klasyfikator optymalizacji pamięci](http://msdn.microsoft.com/library/dn284308.aspx)

