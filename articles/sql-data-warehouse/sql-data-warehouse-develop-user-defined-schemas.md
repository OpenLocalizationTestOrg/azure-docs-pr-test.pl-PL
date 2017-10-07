---
title: "Definicja aaaUser schematów w usłudze SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Porady dotyczące używania schematów języka Transact-SQL w usłudze Azure SQL Data Warehouse związane z opracowywaniem rozwiązań."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>Schematy zdefiniowane przez użytkownika w usłudze SQL Data Warehouse
Magazyny danych tradycyjnych często użycia osobnych baz danych toocreate granic aplikacji na podstawie obciążenia, domeny lub zabezpieczeń. Na przykład tradycyjnego magazynu danych programu SQL Server może obejmować tymczasowej bazy danych, bazy danych magazynu danych i niektóre bazy danych składnicy danych. W tej topologii każda baza danych działa jako obciążenia i granicy zabezpieczeń w architekturze hello.

Z kolei SQL Data Warehouse uruchamia obciążeniu magazynu danych całego hello w ramach jednej bazy danych. Sprzężenia między bazy danych nie są dozwolone. W związku z tym usługi SQL Data Warehouse oczekuje, że wszystkie tabele używane przez toobe magazynu hello przechowywane w hello jedną bazę danych.

> [!NOTE]
> Usługa SQL Data Warehouse nie obsługuje kwerend bazy danych dowolnego rodzaju. W rezultacie implementacji magazynu danych, korzystających z tego wzorca należy toobe zmian.
> 
> 

## <a name="recommendations"></a>Zalecenia
Są to zalecenia na konsolidację obciążeń, zabezpieczeń, domeny i funkcjonalności granice przy użyciu schematów zdefiniowane przez użytkownika

1. Użyj jednego toorun bazy danych SQL Data Warehouse obciążenie magazynu danych
2. Konsolidacja z istniejącego środowiska toouse jeden magazyn danych SQL bazy danych magazynu danych
3. Wykorzystywanie **schematów użytkownika** granic hello tooprovide implementowana przy użyciu baz danych.

Jeśli schematy zdefiniowane przez użytkownika nie zostały użyte wcześniej użytkownik ma pustego. Po prostu użyć hello starej nazwy bazy danych jako podstawa powitania dla Twojego schematów zdefiniowane przez użytkownika w bazie danych usługi SQL Data Warehouse hello.

Jeśli używasz już schematy masz kilka opcji:

1. Usuń nazwy schematu starszych hello i rozpocząć od nowa pracę
2. Zachowaj nazwy schematu starszych hello Nazwa tabeli toohello dla wstępnie oczekujące hello starszej wersji schematu
3. Zachować nazwy schematu starszych hello zaimplementowanie widoków za pośrednictwem tabeli hello w toore dodatkowe schematu — tworzenie hello starego struktury schematu.

> [!NOTE]
> Na pierwszej kontroli opcja 3 może się wydawać hello najbardziej atrakcyjnymi opcji. Jednak hello devil jest szczegółowo hello. Widoki są tylko do odczytu w magazynie danych SQL. Każda zmiana danych lub tabeli potrzebny toobe wykonane względem hello tabeli podstawowej. Opcja 3 wprowadza również warstwy widoków do systemu. Możesz toogive tego rozwagą dodatkowe Jeśli korzystasz już z widoków w architektury.
> 
> 

### <a name="examples"></a>Przykłady:
Implementowanie schematy zdefiniowane przez użytkownika na podstawie nazw bazy danych

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

Zachowaj starszej wersji schematu nazwy przez wstępnie oczekujące ich toohello nazwy tabeli. Użyj schematy hello obciążenia granicy.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

Zachowaj nazwy starszej wersji schematu przy użyciu widoków

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> Wszelkie zmiany w schemacie strategii musi Przegląd modelu zabezpieczeń hello hello bazy danych. W wielu przypadkach może być model zabezpieczeń hello stanie toosimplify, przypisując uprawnienia na poziomie schematu hello. Jeśli wymagane są uprawnienia bardziej szczegółowego można użyć ról bazy danych.
> 
> 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
