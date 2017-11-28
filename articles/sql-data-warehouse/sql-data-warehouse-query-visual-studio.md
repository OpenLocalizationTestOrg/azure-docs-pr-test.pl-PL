---
title: "aaaConnect tooAzure SQL Data Warehouse — VSTS | Dokumentacja firmy Microsoft"
description: "Tworzenie zapytań względem usługi SQL Data Warehouse przy użyciu programu Visual Studio."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: daace889-95e5-4826-b2fc-047eac9d6d95
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 10/31/2016
ms.author: anvang;barbkess
ms.openlocfilehash: 55eef4dff3e0647be5a735295bc89b43eb456079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-data-warehouse-with-visual-studio-and-ssdt"></a><span data-ttu-id="77941-103">Połączenie tooSQL magazynu danych z programu Visual Studio i narzędzi SSDT</span><span class="sxs-lookup"><span data-stu-id="77941-103">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77941-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="77941-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="77941-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="77941-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="77941-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77941-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="77941-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="77941-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="77941-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="77941-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="77941-109">Użyj programu Visual Studio tooquery Azure SQL Data Warehouse w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="77941-109">Use Visual Studio tooquery Azure SQL Data Warehouse in just a few minutes.</span></span> <span data-ttu-id="77941-110">Ta metoda używa hello rozszerzenia SQL Server Data Tools (SSDT) w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77941-110">This method uses hello SQL Server Data Tools (SSDT) extension in Visual Studio.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="77941-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="77941-111">Prerequisites</span></span>
<span data-ttu-id="77941-112">toouse tego samouczka należy:</span><span class="sxs-lookup"><span data-stu-id="77941-112">toouse this tutorial, you need:</span></span>

* <span data-ttu-id="77941-113">Istniejący magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="77941-113">An existing SQL data warehouse.</span></span> <span data-ttu-id="77941-114">Zobacz toocreate, [Tworzenie usługi SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="77941-114">toocreate one, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>
* <span data-ttu-id="77941-115">Rozszerzenie SSDT dla programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="77941-115">SSDT for Visual Studio.</span></span> <span data-ttu-id="77941-116">Jeśli masz program Visual Studio, prawdopodobnie masz też to rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="77941-116">If you have Visual Studio, you probably already have this.</span></span> <span data-ttu-id="77941-117">Aby uzyskać instrukcje instalacji i informacje na temat dostępnych opcji, zobacz artykuł [Instalowanie programu Visual Studio i narzędzi SSDT][Installing Visual Studio and SSDT].</span><span class="sxs-lookup"><span data-stu-id="77941-117">For installation instructions and options, see [Installing Visual Studio and SSDT][Installing Visual Studio and SSDT].</span></span>
* <span data-ttu-id="77941-118">Witaj w pełni kwalifikowana nazwa serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="77941-118">hello fully qualified SQL server name.</span></span> <span data-ttu-id="77941-119">toofind tego, zobacz [połączyć tooSQL hurtowni danych][Connect tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="77941-119">toofind this, see [Connect tooSQL Data Warehouse][Connect tooSQL Data Warehouse].</span></span>

## <a name="1-connect-tooyour-sql-data-warehouse"></a><span data-ttu-id="77941-120">1. Połącz tooyour SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="77941-120">1. Connect tooyour SQL Data Warehouse</span></span>
1. <span data-ttu-id="77941-121">Otwórz program Visual Studio 2013 lub 2015.</span><span class="sxs-lookup"><span data-stu-id="77941-121">Open Visual Studio 2013 or 2015.</span></span>
2. <span data-ttu-id="77941-122">Otwórz Eksplorator obiektów SQL Server.</span><span class="sxs-lookup"><span data-stu-id="77941-122">Open SQL Server Object Explorer.</span></span> <span data-ttu-id="77941-123">toodo ten, wybierz **widoku** > **Eksplorator obiektów SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="77941-123">toodo this, select **View** > **SQL Server Object Explorer**.</span></span>
   
    ![Eksplorator obiektów SQL Server][1]
3. <span data-ttu-id="77941-125">Kliknij przycisk hello **dodawania serwera SQL** ikony.</span><span class="sxs-lookup"><span data-stu-id="77941-125">Click hello **Add SQL Server** icon.</span></span>
   
    ![Dodawanie serwera SQL][2]
4. <span data-ttu-id="77941-127">Wypełnij pola hello hello Connect tooServer okna.</span><span class="sxs-lookup"><span data-stu-id="77941-127">Fill in hello fields in hello Connect tooServer window.</span></span>
   
    ![Połącz tooServer][3]
   
   * <span data-ttu-id="77941-129">**Nazwa serwera**.</span><span class="sxs-lookup"><span data-stu-id="77941-129">**Server name**.</span></span> <span data-ttu-id="77941-130">Wprowadź hello **nazwy serwera** wcześniej ustaloną.</span><span class="sxs-lookup"><span data-stu-id="77941-130">Enter hello **server name** previously identified.</span></span>
   * <span data-ttu-id="77941-131">**Uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="77941-131">**Authentication**.</span></span> <span data-ttu-id="77941-132">Wybierz opcję **Uwierzytelnianie na serwerze SQL Server** lub **Zintegrowane uwierzytelnianie usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="77941-132">Select **SQL Server Authentication** or **Active Directory Integrated Authentication**.</span></span>
   * <span data-ttu-id="77941-133">**Nazwa użytkownika** i **Hasło**.</span><span class="sxs-lookup"><span data-stu-id="77941-133">**User Name** and **Password**.</span></span> <span data-ttu-id="77941-134">Wprowadź nazwę użytkownika i hasło, jeżeli powyżej wybrano uwierzytelnianie na serwerze SQL Server.</span><span class="sxs-lookup"><span data-stu-id="77941-134">Enter user name and password if SQL Server Authentication was selected above.</span></span>
   * <span data-ttu-id="77941-135">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="77941-135">Click **Connect**.</span></span>
5. <span data-ttu-id="77941-136">tooexplore, rozwiń węzeł serwera Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="77941-136">tooexplore, expand your Azure SQL server.</span></span> <span data-ttu-id="77941-137">Witaj baz danych skojarzonego z serwerem hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="77941-137">You can view hello databases associated with hello server.</span></span> <span data-ttu-id="77941-138">Rozwiń węzeł AdventureWorksDW toosee hello tabele w przykładowej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="77941-138">Expand AdventureWorksDW toosee hello tables in your sample database.</span></span>
   
    ![Poznawanie bazy danych AdventureWorksDW][4]

## <a name="2-run-a-sample-query"></a><span data-ttu-id="77941-140">2. Uruchamianie przykładowego zapytania</span><span class="sxs-lookup"><span data-stu-id="77941-140">2. Run a sample query</span></span>
<span data-ttu-id="77941-141">Teraz, gdy połączenie zostało nawiązane tooyour bazy danych, napiszemy zapytanie.</span><span class="sxs-lookup"><span data-stu-id="77941-141">Now that a connection has been established tooyour database, let's write a query.</span></span>

1. <span data-ttu-id="77941-142">Kliknij prawym przyciskiem myszy bazę danych w Eksploratorze obiektów SQL Server.</span><span class="sxs-lookup"><span data-stu-id="77941-142">Right-click your database in SQL Server Object Explorer.</span></span>
2. <span data-ttu-id="77941-143">Wybierz pozycję **Nowe zapytanie**.</span><span class="sxs-lookup"><span data-stu-id="77941-143">Select **New Query**.</span></span> <span data-ttu-id="77941-144">Otworzy się okno nowego zapytania.</span><span class="sxs-lookup"><span data-stu-id="77941-144">A new query window opens.</span></span>
   
    ![Nowe zapytanie][5]
3. <span data-ttu-id="77941-146">Skopiuj to zapytanie TSQL do okna zapytania hello:</span><span class="sxs-lookup"><span data-stu-id="77941-146">Copy this TSQL query into hello query window:</span></span>
   
    ```sql
    SELECT COUNT(*) FROM dbo.FactInternetSales;
    ```
4. <span data-ttu-id="77941-147">Kwerenda hello.</span><span class="sxs-lookup"><span data-stu-id="77941-147">Run hello query.</span></span> <span data-ttu-id="77941-148">toodo, hello zieloną strzałkę lub użyj następującego skrótu hello: `CTRL` + `SHIFT` + `E`.</span><span class="sxs-lookup"><span data-stu-id="77941-148">toodo this, click hello green arrow or use hello following shortcut: `CTRL`+`SHIFT`+`E`.</span></span>
   
    ![Uruchamianie zapytania][6]
5. <span data-ttu-id="77941-150">Spójrz na powitania wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="77941-150">Look at hello query results.</span></span> <span data-ttu-id="77941-151">W tym przykładzie hello Tabela FactInternetSales ma 60398 wierszy.</span><span class="sxs-lookup"><span data-stu-id="77941-151">In this example, hello FactInternetSales table has 60398 rows.</span></span>
   
    ![Wyniki zapytania][7]

## <a name="next-steps"></a><span data-ttu-id="77941-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="77941-153">Next steps</span></span>
<span data-ttu-id="77941-154">Teraz, możesz łączyć i zapytania, spróbuj [wizualizacji danych hello z usługą Power BI][visualizing hello data with PowerBI].</span><span class="sxs-lookup"><span data-stu-id="77941-154">Now that you can connect and query, try [visualizing hello data with PowerBI][visualizing hello data with PowerBI].</span></span>

<span data-ttu-id="77941-155">tooconfigure środowiska pod kątem uwierzytelniania usługi Azure Active Directory, zobacz [uwierzytelniania tooSQL hurtowni danych][Authenticate tooSQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="77941-155">tooconfigure your environment for Azure Active Directory authentication, see [Authenticate tooSQL Data Warehouse][Authenticate tooSQL Data Warehouse].</span></span>

<!--Arcticles-->
[Connect tooSQL Data Warehouse]: sql-data-warehouse-connect-overview.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[Authenticate tooSQL Data Warehouse]: sql-data-warehouse-authentication.md
[visualizing hello data with PowerBI]: sql-data-warehouse-get-started-visualize-with-power-bi.md  

<!--Other-->
[Azure portal]: https://portal.azure.com

<!--Image references-->

[1]: media/sql-data-warehouse-query-visual-studio/open-ssdt.png
[2]: media/sql-data-warehouse-query-visual-studio/add-server.png
[3]: media/sql-data-warehouse-query-visual-studio/connection-dialog.png
[4]: media/sql-data-warehouse-query-visual-studio/explore-sample.png
[5]: media/sql-data-warehouse-query-visual-studio/new-query2.png
[6]: media/sql-data-warehouse-query-visual-studio/run-query.png
[7]: media/sql-data-warehouse-query-visual-studio/query-results.png
