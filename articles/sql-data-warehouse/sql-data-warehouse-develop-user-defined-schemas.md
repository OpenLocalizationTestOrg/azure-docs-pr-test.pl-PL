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
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="8bdd3-103">Schematy zdefiniowane przez użytkownika w usłudze SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8bdd3-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="8bdd3-104">Magazyny danych tradycyjnych często użycia osobnych baz danych toocreate granic aplikacji na podstawie obciążenia, domeny lub zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="8bdd3-105">Na przykład tradycyjnego magazynu danych programu SQL Server może obejmować tymczasowej bazy danych, bazy danych magazynu danych i niektóre bazy danych składnicy danych.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="8bdd3-106">W tej topologii każda baza danych działa jako obciążenia i granicy zabezpieczeń w architekturze hello.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="8bdd3-107">Z kolei SQL Data Warehouse uruchamia obciążeniu magazynu danych całego hello w ramach jednej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="8bdd3-108">Sprzężenia między bazy danych nie są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="8bdd3-109">W związku z tym usługi SQL Data Warehouse oczekuje, że wszystkie tabele używane przez toobe magazynu hello przechowywane w hello jedną bazę danych.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="8bdd3-110">Usługa SQL Data Warehouse nie obsługuje kwerend bazy danych dowolnego rodzaju.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="8bdd3-111">W rezultacie implementacji magazynu danych, korzystających z tego wzorca należy toobe zmian.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="8bdd3-112">Zalecenia</span><span class="sxs-lookup"><span data-stu-id="8bdd3-112">Recommendations</span></span>
<span data-ttu-id="8bdd3-113">Są to zalecenia na konsolidację obciążeń, zabezpieczeń, domeny i funkcjonalności granice przy użyciu schematów zdefiniowane przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="8bdd3-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="8bdd3-114">Użyj jednego toorun bazy danych SQL Data Warehouse obciążenie magazynu danych</span><span class="sxs-lookup"><span data-stu-id="8bdd3-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="8bdd3-115">Konsolidacja z istniejącego środowiska toouse jeden magazyn danych SQL bazy danych magazynu danych</span><span class="sxs-lookup"><span data-stu-id="8bdd3-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="8bdd3-116">Wykorzystywanie **schematów użytkownika** granic hello tooprovide implementowana przy użyciu baz danych.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="8bdd3-117">Jeśli schematy zdefiniowane przez użytkownika nie zostały użyte wcześniej użytkownik ma pustego.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="8bdd3-118">Po prostu użyć hello starej nazwy bazy danych jako podstawa powitania dla Twojego schematów zdefiniowane przez użytkownika w bazie danych usługi SQL Data Warehouse hello.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="8bdd3-119">Jeśli używasz już schematy masz kilka opcji:</span><span class="sxs-lookup"><span data-stu-id="8bdd3-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="8bdd3-120">Usuń nazwy schematu starszych hello i rozpocząć od nowa pracę</span><span class="sxs-lookup"><span data-stu-id="8bdd3-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="8bdd3-121">Zachowaj nazwy schematu starszych hello Nazwa tabeli toohello dla wstępnie oczekujące hello starszej wersji schematu</span><span class="sxs-lookup"><span data-stu-id="8bdd3-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="8bdd3-122">Zachować nazwy schematu starszych hello zaimplementowanie widoków za pośrednictwem tabeli hello w toore dodatkowe schematu — tworzenie hello starego struktury schematu.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="8bdd3-123">Na pierwszej kontroli opcja 3 może się wydawać hello najbardziej atrakcyjnymi opcji.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="8bdd3-124">Jednak hello devil jest szczegółowo hello.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="8bdd3-125">Widoki są tylko do odczytu w magazynie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="8bdd3-126">Każda zmiana danych lub tabeli potrzebny toobe wykonane względem hello tabeli podstawowej.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="8bdd3-127">Opcja 3 wprowadza również warstwy widoków do systemu.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="8bdd3-128">Możesz toogive tego rozwagą dodatkowe Jeśli korzystasz już z widoków w architektury.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="8bdd3-129">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="8bdd3-129">Examples:</span></span>
<span data-ttu-id="8bdd3-130">Implementowanie schematy zdefiniowane przez użytkownika na podstawie nazw bazy danych</span><span class="sxs-lookup"><span data-stu-id="8bdd3-130">Implement user-defined schemas based on database names</span></span>

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

<span data-ttu-id="8bdd3-131">Zachowaj starszej wersji schematu nazwy przez wstępnie oczekujące ich toohello nazwy tabeli.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="8bdd3-132">Użyj schematy hello obciążenia granicy.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-132">Use schemas for hello workload boundary.</span></span>

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

<span data-ttu-id="8bdd3-133">Zachowaj nazwy starszej wersji schematu przy użyciu widoków</span><span class="sxs-lookup"><span data-stu-id="8bdd3-133">Retain legacy schema names using views</span></span>

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
> <span data-ttu-id="8bdd3-134">Wszelkie zmiany w schemacie strategii musi Przegląd modelu zabezpieczeń hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="8bdd3-135">W wielu przypadkach może być model zabezpieczeń hello stanie toosimplify, przypisując uprawnienia na poziomie schematu hello.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="8bdd3-136">Jeśli wymagane są uprawnienia bardziej szczegółowego można użyć ról bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8bdd3-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8bdd3-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8bdd3-137">Next steps</span></span>
<span data-ttu-id="8bdd3-138">Aby uzyskać więcej porad programistycznych, zobacz [omówienie tworzenia][development overview].</span><span class="sxs-lookup"><span data-stu-id="8bdd3-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
