---
title: "Zarządzanie grupami baz danych Azure SQL | Dokumentacja firmy Microsoft"
description: "Przeprowadzenie tworzenie i zarządzanie elastycznej zadania."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: d30cc74778e0b36dd632c2f040ce80d1ca8af5a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a>Tworzenie i zarządzanie nimi skalowanej baz danych SQL Azure za pomocą zadania elastyczne (wersja zapoznawcza)


**Zadania elastyczne bazy danych** uprościć zarządzanie grupy baz danych, wykonując operacje administracyjne, takie jak zmiany schematu, Zarządzanie poświadczeniami, aktualizacje danych odwołania, gromadzenia danych wydajności lub telemetrii dzierżawy (klienta) Kolekcja. Zadania elastyczne bazy danych jest obecnie dostępna za pośrednictwem portalu Azure i poleceń cmdlet programu PowerShell. Niemniej jednak Azure powierzchni portalu zmniejszony ograniczone do wykonania dla wszystkich baz danych w funkcji [puli elastycznej (wersja zapoznawcza)](sql-database-elastic-pool.md). Dostęp do dodatkowych funkcji i wykonywanie skryptów między grupą baz danych w tym niestandardowy kolekcji lub fragmentacji Ustaw (utworzony za pomocą [biblioteki klienta elastycznej bazy danych](sql-database-elastic-scale-introduction.md)), zobacz [tworzenie i zarządzanie nimi zadania przy użyciu programu PowerShell](sql-database-elastic-jobs-powershell.md). Aby uzyskać więcej informacji o zadaniach, zobacz [omówienie zadania elastycznej bazy danych](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure. Bezpłatnej wersji próbnej, zobacz [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* Puli elastycznej. Zobacz [o pule elastyczne](sql-database-elastic-pool.md).
* Instalacja składników usługi zadania elastycznej bazy danych. Zobacz [instalowania usługi zadania elastycznej bazy danych](sql-database-elastic-jobs-service-installation.md).

## <a name="creating-jobs"></a>Tworzenie zadania
1. Przy użyciu [portalu Azure](https://portal.azure.com), z istniejącej elastycznej puli baz danych zadania, kliknij przycisk **Utwórz zadanie**.
2. Wpisz nazwę użytkownika i hasło administratora bazy danych (utworzone podczas instalacji zadania) dla bazy danych kontroli zadania (magazynu metadanych dla zadania).
   
    ![Nazwa zadania, wpisz lub Wklej w kodzie i kliknij przycisk Uruchom][1]
3. W **Utwórz zadanie** bloku, wpisz nazwę zadania.
4. Wpisz nazwę użytkownika i hasło, aby połączyć się z docelowymi bazami danych z wystarczającymi uprawnieniami do pomyślnego wykonania skryptów.
5. Wklej lub typ skryptu T-SQL.
6. Kliknij przycisk **zapisać** , a następnie kliknij przycisk **Uruchom**.
   
    ![Tworzenie zadań i uruchom][5]

## <a name="run-idempotent-jobs"></a>Uruchamianie zadań idempotentności
Po uruchomieniu skryptu na podstawie zestawu baz danych, należy się upewnić, że skrypt jest idempotentności. Oznacza to, że skryptu musi być można uruchamiać wielokrotnie, nawet jeśli go nie powiodło się przed niekompletna. Na przykład, jeśli skrypt zakończy się niepowodzeniem, zadanie będzie automatycznie ponawiana dopóki próba powiedzie się (w granicach, jako retry logiki ostatecznie przestaną ponawianie próby). Sposób, w tym celu jest użycie klauzuli "Jeśli ISTNIEJE" i usunąć wszystkie znalezione wystąpienia przed utworzeniem nowego obiektu. Przykładem jest następujący:

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

Alternatywnie można użyć klauzuli "Jeśli nie ISTNIEJE" przed utworzeniem nowego wystąpienia:

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

Ten skrypt aktualizacji następnie tabeli utworzone wcześniej.

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a>Sprawdzanie stanu zadania
Po rozpoczęciu zadania, można sprawdzić jego postępu.

1. Na stronie puli elastycznej kliknij **zarządzać zadaniami**.
   
    ![Kliknij pozycję "Zarządzaj zadania"][2]
2. Kliknij nazwę () zadania. **Stan** może być "Ukończone" lub "Nie powiodło się." Szczegóły zadania zostaną wyświetlone (b) z jego datę i godzinę tworzenia i uruchamiania. Listy (c) poniżej się, że będzie wyświetlany postęp skryptu dla każdej bazy danych w puli, podając jego szczegóły daty i godziny.
   
    ![Zakończono zadania sprawdzania][3]

## <a name="checking-failed-jobs"></a>Sprawdzanie zadania zakończone niepowodzeniem
Jeśli zadanie nie powiedzie się, można znaleźć w dzienniku wykonywania. Kliknij nazwę zadania nie powiodło się, aby wyświetlić jego szczegóły.

![Sprawdź zadanie zakończone niepowodzeniem][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


