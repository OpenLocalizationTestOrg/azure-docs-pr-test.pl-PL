---
title: "aaaConnect tooAzure SQL Data Warehouse — SSMS | Dokumentacja firmy Microsoft"
description: "Użyj programu SQL Server Management Studio (SSMS) tooconnect tooand zapytania usługi Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: 
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 299e50b3-e68a-471c-8aee-b0b9874781bd
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: bcbaf7139d2e5183b388b8d58c015cf5ad726722
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="5e266-103">Połącz tooSQL magazynu danych z programu SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="5e266-103">Connect tooSQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5e266-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="5e266-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="5e266-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5e266-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="5e266-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5e266-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="5e266-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="5e266-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="5e266-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="5e266-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="5e266-109">Użyj programu SQL Server Management Studio (SSMS) tooconnect tooand zapytania usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="5e266-109">Use SQL Server Management Studio (SSMS) tooconnect tooand query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5e266-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5e266-110">Prerequisites</span></span>
<span data-ttu-id="5e266-111">toouse tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="5e266-111">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="5e266-112">Istniejący magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="5e266-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="5e266-113">Zobacz toocreate, [Tworzenie usługi SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="5e266-113">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="5e266-114">SQL Server Management Studio (SSMS) zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="5e266-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="5e266-115">[Zainstaluj narzędzia SSMS] [ Install SSMS] bezpłatnie, jeśli nie masz jeszcze go.</span><span class="sxs-lookup"><span data-stu-id="5e266-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="5e266-116">Witaj w pełni kwalifikowana nazwa serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="5e266-116">hello fully qualified SQL server name.</span></span> <span data-ttu-id="5e266-117">toofind tego, zobacz [połączyć tooSQL hurtowni danych][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="5e266-117">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="5e266-118">1. Połącz tooyour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5e266-118">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="5e266-119">Otwórz program SSMS.</span><span class="sxs-lookup"><span data-stu-id="5e266-119">Open SSMS.</span></span>
2. <span data-ttu-id="5e266-120">Otwórz Eksplorator obiektów.</span><span class="sxs-lookup"><span data-stu-id="5e266-120">Open Object Explorer.</span></span> <span data-ttu-id="5e266-121">toodo ten, wybierz **pliku** > **połączyć Eksplorator obiektów**.</span><span class="sxs-lookup"><span data-stu-id="5e266-121">toodo this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Eksplorator obiektów SQL Server][1]
3. <span data-ttu-id="5e266-123">Wypełnij pola hello hello Connect tooServer okna.</span><span class="sxs-lookup"><span data-stu-id="5e266-123">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Połącz tooServer][2]
   
   * <span data-ttu-id="5e266-125">**Nazwa serwera**.</span><span class="sxs-lookup"><span data-stu-id="5e266-125">**Server name**.</span></span> <span data-ttu-id="5e266-126">Wprowadź hello **nazwy serwera** wcześniej ustaloną.</span><span class="sxs-lookup"><span data-stu-id="5e266-126">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="5e266-127">**Uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="5e266-127">**Authentication**.</span></span> <span data-ttu-id="5e266-128">Wybierz opcję **Uwierzytelnianie na serwerze SQL Server** lub **Zintegrowane uwierzytelnianie usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e266-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="5e266-129">**Nazwa użytkownika** i **Hasło**.</span><span class="sxs-lookup"><span data-stu-id="5e266-129">**User Name** and **Password**.</span></span> <span data-ttu-id="5e266-130">Wprowadź nazwę użytkownika i hasło, jeżeli powyżej wybrano uwierzytelnianie na serwerze SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5e266-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="5e266-131">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="5e266-131">Click **Connect**.</span></span>
4. <span data-ttu-id="5e266-132">tooexplore, rozwiń węzeł serwera Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="5e266-132">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="5e266-133">Witaj baz danych skojarzonego z serwerem hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="5e266-133">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="5e266-134">Rozwiń węzeł AdventureWorksDW toosee hello tabele w przykładowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="5e266-134">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Poznawanie bazy danych AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="5e266-136">2. Uruchamianie przykładowego zapytania</span><span class="sxs-lookup"><span data-stu-id="5e266-136">2. Run a sample query</span></span>
<span data-ttu-id="5e266-137">Teraz, gdy połączenie zostało nawiązane tooyour bazy danych, napiszemy zapytanie.</span><span class="sxs-lookup"><span data-stu-id="5e266-137">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="5e266-138">Kliknij prawym przyciskiem myszy bazę danych w Eksploratorze obiektów SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5e266-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="5e266-139">Wybierz pozycję **Nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="5e266-139">Select **New Query**.</span></span> <span data-ttu-id="5e266-140">Otworzy się okno nowego zapytania.</span><span class="sxs-lookup"><span data-stu-id="5e266-140">A new query window opens.</span></span>
   
    ![Nowe zapytanie][4]
3. <span data-ttu-id="5e266-142">Skopiuj to zapytanie TSQL do okna zapytania hello:</span><span class="sxs-lookup"><span data-stu-id="5e266-142">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="5e266-143">Kwerenda hello.</span><span class="sxs-lookup"><span data-stu-id="5e266-143">Run hello query.</span></span> <span data-ttu-id="5e266-144">toodo tego, kliknij `Execute` lub hello Użyj następującego skrótu: `F5`.</span><span class="sxs-lookup"><span data-stu-id="5e266-144">toodo this, click `Execute` or use hello following shortcut: `F5`.</span></span>
   
    ![Uruchamianie zapytania][5]
5. <span data-ttu-id="5e266-146">Spójrz na powitania wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="5e266-146">Look at hello query results.</span></span> <span data-ttu-id="5e266-147">W tym przykładzie hello Tabela FactInternetSales ma 60398 wierszy.</span><span class="sxs-lookup"><span data-stu-id="5e266-147">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Wyniki zapytania][6]

## <a name="next-steps"></a><span data-ttu-id="5e266-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e266-149">Next steps</span></span>
<span data-ttu-id="5e266-150">Teraz, możesz łączyć i zapytania, spróbuj [wizualizacji danych hello z usługą Power BI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="5e266-150">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="5e266-151">tooconfigure środowiska pod kątem uwierzytelniania usługi Azure Active Directory, zobacz [uwierzytelniania tooSQL hurtowni danych][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="5e266-151">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

<!--Other-->
[Azure portal]: https://portal.azure.com
[Install SSMS]: https://msdn.microsoft.com/en-US/library/hh213248.aspx


<!--Image references-->

[1]: media/sql-data-warehouse-query-ssms/connect-object-explorer.png
[2]: media/sql-data-warehouse-query-ssms/connect-object-explorer1.png
[3]: media/sql-data-warehouse-query-ssms/explore-tables.png
[4]: media/sql-data-warehouse-query-ssms/new-query.png
[5]: media/sql-data-warehouse-query-ssms/execute-query.png
[6]: media/sql-data-warehouse-query-ssms/results.png
