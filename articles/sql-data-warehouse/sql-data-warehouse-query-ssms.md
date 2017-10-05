---
title: "Połączyć się z magazynem danych Azure SQL - SSMS | Dokumentacja firmy Microsoft"
description: "Użyj programu SQL Server Management Studio (SSMS) do nawiązania połączenia i wykonywać zapytania usługi Azure SQL Data Warehouse."
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
ms.openlocfilehash: 207fb9fd861c66039fbde89681aed3df3a2f4021
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-sql-data-warehouse-with-sql-server-management-studio-ssms"></a><span data-ttu-id="71a02-103">Nawiązać połączenia SQL Data Warehouse przy użyciu programu SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="71a02-103">Connect to SQL Data Warehouse with SQL Server Management Studio (SSMS)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="71a02-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="71a02-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="71a02-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="71a02-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="71a02-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71a02-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="71a02-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="71a02-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="71a02-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="71a02-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="71a02-109">Użyj programu SQL Server Management Studio (SSMS) do nawiązania połączenia i wykonywać zapytania usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="71a02-109">Use SQL Server Management Studio (SSMS) to connect to and query Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="71a02-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="71a02-110">Prerequisites</span></span>
<span data-ttu-id="71a02-111">Aby użyć tego samouczka, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="71a02-111">To use this tutorial, you need:</span></span>

* <span data-ttu-id="71a02-112">Istniejący magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="71a02-112">An existing SQL data warehouse.</span></span> <span data-ttu-id="71a02-113">Aby go utworzyć, zobacz artykuł [Tworzenie bazy danych w usłudze SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="71a02-113">To create one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="71a02-114">SQL Server Management Studio (SSMS) zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="71a02-114">SQL Server Management Studio (SSMS) installed.</span></span> <span data-ttu-id="71a02-115">[Zainstaluj narzędzia SSMS] [ Install SSMS] bezpłatnie, jeśli nie masz jeszcze go.</span><span class="sxs-lookup"><span data-stu-id="71a02-115">[Install SSMS][Install SSMS] for free if you don't already have it.</span></span>
* <span data-ttu-id="71a02-116">W pełni kwalifikowana nazwa serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="71a02-116">The fully qualified SQL server name.</span></span> <span data-ttu-id="71a02-117">Aby ją znaleźć, zobacz [Nawiązywanie połączenia z usługą SQL Data Warehouse][Connect to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="71a02-117">To find this, see [Connect to SQL Data Warehouse][Connect to SQL Data Warehouse].</span></span>

## <a name="1-connect-to-your-sql-data-warehouse"></a><span data-ttu-id="71a02-118">1. Nawiązywanie połączenia z usługą SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="71a02-118">1. Connect to your SQL Data Warehouse</span></span>
1. <span data-ttu-id="71a02-119">Otwórz program SSMS.</span><span class="sxs-lookup"><span data-stu-id="71a02-119">Open SSMS.</span></span>
2. <span data-ttu-id="71a02-120">Otwórz Eksplorator obiektów.</span><span class="sxs-lookup"><span data-stu-id="71a02-120">Open Object Explorer.</span></span> <span data-ttu-id="71a02-121">Aby to zrobić, wybierz **pliku** > **połączyć Eksplorator obiektów**.</span><span class="sxs-lookup"><span data-stu-id="71a02-121">To do this, select **File** > **Connect Object Explorer**.</span></span>
   
    ![Eksplorator obiektów SQL Server][1]
3. <span data-ttu-id="71a02-123">Wypełnij pola w oknie łączenia z serwerem.</span><span class="sxs-lookup"><span data-stu-id="71a02-123">Fill in the fields in the Connect to Server window.</span></span>
   
    ![Łączenie z serwerem][2]
   
   * <span data-ttu-id="71a02-125">**Nazwa serwera**.</span><span class="sxs-lookup"><span data-stu-id="71a02-125">**Server name**.</span></span> <span data-ttu-id="71a02-126">Wprowadź wcześniej ustaloną **nazwę serwera**.</span><span class="sxs-lookup"><span data-stu-id="71a02-126">Enter the **server name** previously identified.</span></span>
   * <span data-ttu-id="71a02-127">**Uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="71a02-127">**Authentication**.</span></span> <span data-ttu-id="71a02-128">Wybierz opcję **Uwierzytelnianie na serwerze SQL Server** lub **Zintegrowane uwierzytelnianie usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71a02-128">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="71a02-129">**Nazwa użytkownika** i **Hasło**.</span><span class="sxs-lookup"><span data-stu-id="71a02-129">**User Name** and **Password**.</span></span> <span data-ttu-id="71a02-130">Wprowadź nazwę użytkownika i hasło, jeżeli powyżej wybrano uwierzytelnianie na serwerze SQL Server.</span><span class="sxs-lookup"><span data-stu-id="71a02-130">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="71a02-131">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="71a02-131">Click **Connect**.</span></span>
4. <span data-ttu-id="71a02-132">W celach poznawczych rozwiń węzeł serwera Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="71a02-132">To explore, expand your Azure SQL server.</span></span> <span data-ttu-id="71a02-133">Możesz przejrzeć skojarzone z serwerem bazy danych.</span><span class="sxs-lookup"><span data-stu-id="71a02-133">You can view the databases associated with the server.</span></span> <span data-ttu-id="71a02-134">Rozwiń węzeł AdventureWorksDW, aby zobaczyć tabele w przykładowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="71a02-134">Expand AdventureWorksDW to see the tables in your sample database.</span></span>
   
    ![Poznawanie bazy danych AdventureWorksDW][3]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="71a02-136">2. Uruchamianie przykładowego zapytania</span><span class="sxs-lookup"><span data-stu-id="71a02-136">2. Run a sample query</span></span>
<span data-ttu-id="71a02-137">Teraz, po nawiązaniu połączenia z bazą danych, napiszemy zapytanie.</span><span class="sxs-lookup"><span data-stu-id="71a02-137">Now that a connection has been established to your database, let's write a query.</span></span>

1. <span data-ttu-id="71a02-138">Kliknij prawym przyciskiem myszy bazę danych w Eksploratorze obiektów SQL Server.</span><span class="sxs-lookup"><span data-stu-id="71a02-138">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="71a02-139">Wybierz pozycję **Nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="71a02-139">Select **New Query**.</span></span> <span data-ttu-id="71a02-140">Otworzy się okno nowego zapytania.</span><span class="sxs-lookup"><span data-stu-id="71a02-140">A new query window opens.</span></span>
   
    ![Nowe zapytanie][4]
3. <span data-ttu-id="71a02-142">Skopiuj to zapytanie TSQL do okna zapytania:</span><span class="sxs-lookup"><span data-stu-id="71a02-142">Copy this TSQL query into the query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="71a02-143">Uruchom zapytanie.</span><span class="sxs-lookup"><span data-stu-id="71a02-143">Run the query.</span></span> <span data-ttu-id="71a02-144">Aby to zrobić, kliknij przycisk `Execute` lub użyj następującego skrótu: `F5`.</span><span class="sxs-lookup"><span data-stu-id="71a02-144">To do this, click `Execute` or use the following shortcut: `F5`.</span></span>
   
    ![Uruchamianie zapytania][5]
5. <span data-ttu-id="71a02-146">Przejrzyj wyniki zapytania.</span><span class="sxs-lookup"><span data-stu-id="71a02-146">Look at the query results.</span></span> <span data-ttu-id="71a02-147">W tym przykładzie tabela FactInternetSales ma 60398 wierszy.</span><span class="sxs-lookup"><span data-stu-id="71a02-147">In this example, the FactInternetSales table has 60398 rows.</span></span>
   
    ![Wyniki zapytania][6]

## <a name="next-steps"></a><span data-ttu-id="71a02-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71a02-149">Next steps</span></span>
<span data-ttu-id="71a02-150">Teraz, kiedy umiesz nawiązywać połączenia i wykonywać zapytania, spróbuj wykonać [wizualizację danych przy użyciu usługi Power BI][visualizing the data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="71a02-150">Now that you can connect and query, try [visualizing the data with PowerBI][visualizing the data with PowerBI].</span></span>

<span data-ttu-id="71a02-151">Aby skonfigurować środowisko do uwierzytelniania usługi Azure Active Directory, zobacz artykuł [Uwierzytelnianie w usłudze SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="71a02-151">To configure your environment for Azure Active Directory authentication, see [Authenticate to SQL Data Warehouse][Authenticate to SQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect to SQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Authenticate to SQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing the data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md 

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
