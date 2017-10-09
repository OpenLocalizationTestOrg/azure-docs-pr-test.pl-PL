---
title: aaaRestore pojedynczej tabeli z kopii zapasowej bazy danych SQL Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toorestore pojedynczej tabeli z kopii zapasowej bazy danych SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a>Jak toorestore pojedynczej tabeli z kopii zapasowej bazy danych SQL Azure
Może wystąpić sytuacja, w którym przypadkowo zmodyfikowano niektóre dane w bazie danych SQL, a teraz ma toorecover hello pojedynczej tabeli dotyczy. W tym artykule opisano, jak toorestore pojedynczej tabeli w bazie danych z jednego z hello bazy danych SQL [automatycznego tworzenia kopii zapasowych](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a>Czynności przygotowujące: Zmień nazwę tabeli hello i przywrócenie kopii bazy danych hello
1. Zidentyfikuj hello tabeli, które mają tooreplace hello przywrócić kopię bazy danych Azure SQL. Użyj programu Microsoft SQL Management Studio toorename hello tabeli. Na przykład zmienić nazwę tabeli hello jako &lt;nazwy tabeli&gt;_old.
   
   > [!NOTE]
   > tooavoid blokowane, upewnij się, że nic się nie uruchomione na powitania tabeli, która jest zmieniana. Jeśli wystąpią problemy, upewnij się, że wykonać tę procedurę w oknie obsługi.
   >

2. Przywróć kopię zapasową punktu tooa bazy danych w czasie, które mają toorecover toousing hello [punkt-In_Time przywrócić](sql-database-recovery-using-backups.md#point-in-time-restore) czynności.
   
   > [!NOTE]
   > Nazwa Hello hello przywrócona baza danych będzie w hello DBName + format sygnatury czasowej; na przykład **Adventureworks2012_2016-01-01T22-12Z**. Ten krok nie zastąpienie nazwy istniejącej bazy danych hello na powitania serwera. Jest to miara bezpieczeństwa i jest on przeznaczony tooallow tooverify hello przywrócone bazy danych, aby usunąć ich bieżącej bazy danych i Zmień nazwę bazy danych hello przywrócone do użytku produkcyjnego.
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a>Kopiowanie tabeli hello z hello przywrócić bazy danych przy użyciu narzędzia do migracji bazy danych SQL hello

1. Pobierz i zainstaluj hello [Kreatora migracji bazy danych SQL](https://sqlazuremw.codeplex.com).
2. Hello otwórz Kreator migracji bazy danych SQL, na powitania **wybierz proces** wybierz **bazy danych w obszarze Analizuj/migracji**, a następnie kliknij przycisk **dalej**.

   ![Kreator migracji bazy danych SQL — wybierz procesu](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. W hello **połączyć tooServer** okna dialogowego należy zastosować hello następujące ustawienia:

   * Nazwa serwera: **Your SQL server**
   * Uwierzytelnianie: **uwierzytelniania programu SQL Server**
   * Nazwa użytkownika: **logowanie**
   * Hasło: **hasła**
   * Baza danych: **bazy danych Master (listę wszystkich baz danych)**
   
   > [!NOTE]
   > Domyślnie hello kreator zapisuje informacje logowania. Jeśli nie chcesz jej, wybierz **zapomnij informacje logowania**.
   >
   
     ![Migracja bazy danych SQL kreatora — wybierz źródło — krok 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. W hello **wybierz źródło** okno dialogowe, nazwa bazy danych wybierz hello przywrócone z hello **czynności przygotowujące** sekcji jako źródła, a następnie kliknij przycisk **dalej**.
   
    ![Migracja bazy danych SQL kreatora — wybierz źródło — krok 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. W hello **wybierz obiekty** okno dialogowe, wybierz opcję hello **określonych obiektów bazy danych wybierz** opcji, a następnie wybierz table(or tables) hello czy chcesz, aby serwer docelowy toohello toomigrate.
   ![Kreator migracji bazy danych SQL — Wybieranie obiektów](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. Na powitania **Podsumowanie Kreatora skryptu** kliknij przycisk **tak** monit o czy wszystko jest gotowe toogenerate skryptu SQL. Istnieje również opcja hello toosave hello skryptu TSQL do późniejszego użycia.
   ![Kreator migracji bazy danych SQL — Podsumowanie Kreatora skryptu](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. Na powitania **podsumowania wyników** kliknij przycisk **dalej**.
   ![Kreator migracji bazy danych SQL — podsumowanie wyników](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. Na powitania **ustawienia połączenia z serwerem docelowym** kliknij przycisk **połączyć tooServer**, a następnie wprowadź szczegóły hello w następujący sposób:
   
   * **Nazwa serwera**: wystąpienie serwera docelowego
   * **Uwierzytelnianie**: **uwierzytelniania programu SQL Server**. Wprowadź poświadczenia logowania.
   * **Baza danych**: **bazy danych Master (listę wszystkich baz danych)**. Ta opcja wyświetla listę wszystkich hello baz danych na serwerze docelowym hello.
     
     ![Kreator migracji bazy danych SQL — Skonfiguruj połączenie z serwera docelowego](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Kliknij przycisk **Connect**, wybierz docelową bazę danych hello, tabela hello toomove, a następnie kliknij przycisk **dalej**. To powinno zostać zakończone uruchomienie skryptu hello wcześniej wygenerowany i powinien pojawić się hello nowo przenieść tabeli skopiowanych toohello docelowej bazy danych.

## <a name="verification-step"></a>Krok weryfikacji

- Zapytania i przetestować toomake tabeli hello nowo skopiowany pewność, że dane hello jest prawidłowa. Po potwierdzeniu, musisz porzucić hello zmienić nazwy tabeli formularza **czynności przygotowujące** sekcji. (na przykład &lt;nazwy tabeli&gt;_old).

## <a name="next-steps"></a>Następne kroki
[Automatyczne kopie zapasowe bazy danych SQL](sql-database-automated-backups.md)

