---
title: "narzędzia sqlcmd SQL Data Warehouse tooAzure aaaConnect | Dokumentacja firmy Microsoft"
description: "Użyj [sqlcmd] [sqlcmd] narzędzie wiersza polecenia tooconnect tooand zapytania usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 6e2b69e5-4806-4e91-9ea1-e2b63bf28c46
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 0334df7b969da1966ba29c97f835a2dc9e383e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sqlcmd"></a>Połącz tooSQL hurtowni danych przy użyciu narzędzia sqlcmd
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Program Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

Użyj [sqlcmd] [ sqlcmd] tooand tooconnect narzędzia wiersza polecenia zapytań usługi Azure SQL Data Warehouse.  

## <a name="1-connect"></a>1. Połączenie
wprowadzenie tooget [sqlcmd][sqlcmd], otwórz wiersz polecenia hello i wprowadź **sqlcmd** następuje hello parametry połączenia bazy danych SQL Data Warehouse. Parametry połączenia Hello wymaga hello następujące parametry:

* **Serwer (-S):** serwera w formie hello `<`nazwy serwera`>`. database.windows.net
* **Baza danych (-d):** nazwa bazy danych.
* **Włącz cytowane identyfikatory (-I):** cytowane identyfikatory musi być wystąpieniem usługi SQL Data Warehouse tooa tooconnect włączone.

toouse uwierzytelniania programu SQL Server, należy tooadd hello nazwy użytkownika i hasła parametry:

* **Użytkownik (-U):** użytkownik serwera w formie hello `<`użytkownika`>`
* **Hasło (-P):** hasło skojarzone z hello użytkownika.

Na przykład ciąg połączenia może wyglądać hello następujące czynności:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

Azure Active Directory Integrated authentication toouse, należy tooadd hello Azure Active Directory parametry:

* **Uwierzytelnianie usługi Azure Active Directory (-G):** używaj usługi Azure Active Directory do uwierzytelniania

Na przykład ciąg połączenia może wyglądać hello następujące czynności:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> Należy zbyt[Włącz uwierzytelnianie usługi Azure Active Directory](sql-data-warehouse-authentication.md) tooauthenticate przy użyciu usługi Active Directory.
> 
> 

## <a name="2-query"></a>2. Zapytanie
Po połączeniu można wystawiać żadnych obsługiwane instrukcje języka Transact-SQL przed wystąpieniem hello.  W tym przykładzie zapytania są przesyłane w trybie interaktywnym.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

Pokazują powyższe przykłady dalej sposób wykonywania zapytań w trybie wsadowym przy użyciu opcji -Q hello lub przekazanie w potoku toosqlcmd Twojego SQL.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Następne kroki
Zobacz [dokumentacji narzędzia sqlcmd] [ sqlcmd] więcej informacji o szczegółowe informacje o hello opcje dostępne w przypadku użycia programu sqlcmd.

<!--Image references-->

<!--Article references-->

<!--MSDN references--> 
[sqlcmd]: https://msdn.microsoft.com/library/ms162773.aspx
[Azure portal]: https://portal.azure.com

<!--Other Web references-->
