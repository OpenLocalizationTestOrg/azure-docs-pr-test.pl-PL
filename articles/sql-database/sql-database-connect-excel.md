---
title: "Łączenie programu Excel z bazą danych SQL Database | Microsoft Docs"
description: "Dowiedz się, jak połączyć program Microsoft Excel z bazą danych Azure SQL w chmurze. Importowanie danych do programu Excel, raportowanie i eksploracja danych."
services: sql-database
keywords: "łączenie programu excel z sql, importowanie danych do programu excel"
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 97344d7c0be38b3092a3224074d486b5bb984176
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-excel-to-an-azure-sql-database-and-create-a-report"></a><span data-ttu-id="b5609-105">Łączenie programu Excel z bazą danych Azure SQL i utworzyć raport</span><span class="sxs-lookup"><span data-stu-id="b5609-105">Connect Excel to an Azure SQL database and create a report</span></span>

<span data-ttu-id="b5609-106">Łączenie programu Excel z bazą danych SQL w chmurze i importowanie danych i tworzenie tabel i wykresów na podstawie wartości w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="b5609-106">Connect Excel to a SQL database in the cloud and import data and create tables and charts based on values in the database.</span></span> <span data-ttu-id="b5609-107">W tym samouczku skonfigurujesz połączenie między programem Excel i tabelą bazy danych, zapiszesz plik przechowujący dane oraz informacje o połączeniu dla programu Excel, a następnie utworzysz wykres przestawny z wartościami bazy danych.</span><span class="sxs-lookup"><span data-stu-id="b5609-107">In this tutorial you will set up the connection between Excel and a database table, save the file that stores data and the connection information for Excel, and then create a pivot chart from the database values.</span></span>

<span data-ttu-id="b5609-108">Przed rozpoczęciem pracy będziesz potrzebować bazy danych SQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b5609-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="b5609-109">Jeśli jej nie masz, zobacz artykuł [Create your first SQL database](sql-database-get-started-portal.md) (Tworzenie pierwszej bazy danych SQL), aby w ciągu kilku minut uzyskać gotową do pracy bazę danych z przykładowymi danymi.</span><span class="sxs-lookup"><span data-stu-id="b5609-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) to get a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="b5609-110">W tym artykule będzie importować przykładowe dane do programu Excel z tego artykułu, ale można wykonać podobne kroki z użyciem własnych danych.</span><span class="sxs-lookup"><span data-stu-id="b5609-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="b5609-111">Potrzebna będzie również kopia programu Excel.</span><span class="sxs-lookup"><span data-stu-id="b5609-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="b5609-112">W tym artykule wykorzystano program [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="b5609-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-to-a-sql-database-and-create-an-odc-file"></a><span data-ttu-id="b5609-113">Łączenie programu Excel z bazą danych SQL i tworzenie pliku odc</span><span class="sxs-lookup"><span data-stu-id="b5609-113">Connect Excel to a SQL database and create an odc file</span></span>
1. <span data-ttu-id="b5609-114">Aby połączyć program Excel z bazą danych SQL, otwórz program Excel, a następnie utwórz nowy skoroszyt lub otwórz istniejący skoroszyt programu Excel.</span><span class="sxs-lookup"><span data-stu-id="b5609-114">To connect Excel to SQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="b5609-115">Na pasku menu w górnej części strony kliknij kartę **Dane**, kliknij przycisk **Z innych źródeł**, a następnie kliknij pozycję **Z programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="b5609-115">In the menu bar at the top of the page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Wybór źródła danych: połącz program Excel z bazą danych SQL.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="b5609-117">Zostanie otwarty Kreator połączenia danych.</span><span class="sxs-lookup"><span data-stu-id="b5609-117">The Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="b5609-118">W oknie dialogowym **Łączenie z serwerem bazy danych** wpisz **nazwę serwera** usługi SQL Database, z którym chcesz nawiązać połączenie w następującej formie: <*nazwaserwera*>**. database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="b5609-118">In the **Connect to Database Server** dialog box, type the SQL Database **Server name** you want to connect to in the form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="b5609-119">Na przykład **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="b5609-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="b5609-120">W obszarze **Poświadczenia logowania** kliknij opcję **Użyj następującej nazwy użytkownika i hasła**, wpisz **nazwę użytkownika** i **hasło** skonfigurowane dla serwera usługi SQL Database podczas jego tworzenia, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="b5609-120">Under **Log on credentials**, click **Use the following User Name and Password**, type the **User Name** and **Password** you set up for the SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Wpisywanie nazwy serwera i poświadczeń logowania](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="b5609-122">W zależności od środowiska sieciowego może nie być możliwe nawiązanie połączenia lub można utracić połączenie, jeśli serwer usługi SQL Database nie zezwala na ruch z adresu IP klienta.</span><span class="sxs-lookup"><span data-stu-id="b5609-122">Depending on your network environment, you may not be able to connect or you may lose the connection if the SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="b5609-123">Przejdź do witryny [Azure Portal](https://portal.azure.com/), kliknij serwery SQL, kliknij serwer, którego używasz, kliknij zaporę systemu w ustawieniach i dodaj swój adres IP klienta.</span><span class="sxs-lookup"><span data-stu-id="b5609-123">Go to the [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="b5609-124">Aby uzyskać szczegółowe informacje, zobacz artykuł [How to configure firewall settings](sql-database-configure-firewall-settings.md) (Jak skonfigurować ustawienia zapory).</span><span class="sxs-lookup"><span data-stu-id="b5609-124">See [How to configure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="b5609-125">W oknie dialogowym **Wybór bazy danych i tabeli** wybierz z listy bazę danych, której chcesz używać, kliknij tabele lub widoki, których chcesz używać (wybrano **vGetAllCategories**), a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="b5609-125">In the **Select Database and Table** dialog, select the database you want to work with from the list, and then click the tables or views you want to work with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Wybierz bazę danych i tabelę.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="b5609-127">Zostanie otwarte okno dialogowe **Zapisywanie pliku połączenia danych i kończenie**, w którym należy podać informacje o pliku połączenia bazy danych pakietu Office (*.odc), z którego korzysta program Excel.</span><span class="sxs-lookup"><span data-stu-id="b5609-127">The **Save Data Connection File and Finish** dialog box opens, where you provide information about the Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="b5609-128">Można pozostawić wartości domyślne lub dostosować ustawienia.</span><span class="sxs-lookup"><span data-stu-id="b5609-128">You can leave the defaults or customize your selections.</span></span>
6. <span data-ttu-id="b5609-129">Wartości domyślne możesz pozostawić bez zmian, zwróć jednak uwagę na pole **Nazwa pliku**.</span><span class="sxs-lookup"><span data-stu-id="b5609-129">You can leave the defaults, but note the **File Name** in particular.</span></span> <span data-ttu-id="b5609-130">**Opis**, **Przyjazna nazwa** i **Słowa kluczowe** przypominają zarówno Tobie, jak i innym użytkownikom, jakie połączenie ma zostać nawiązane, oraz ułatwiają znalezienie połączenia.</span><span class="sxs-lookup"><span data-stu-id="b5609-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting to and find the connection.</span></span> <span data-ttu-id="b5609-131">Kliknij opcję **Zawsze próbuj używać tego pliku w celu odświeżenia danych**, jeśli chcesz, aby informacje o połączeniu były przechowywane w pliku odc i używane w celu aktualizacji danych podczas nawiązywania połączenia, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="b5609-131">Click **Always attempt to use this file to refresh data** if you want connection information stored in the odc file so it can update when you connect to it, and then click **Finish**.</span></span>
   
    ![Zapisywanie pliku odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="b5609-133">Zostanie otwarte okno dialogowe **Importowanie danych**.</span><span class="sxs-lookup"><span data-stu-id="b5609-133">The **Import data** dialog box appears.</span></span>

## <a name="import-the-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="b5609-134">Importowanie danych do programu Excel i tworzenie wykresu przestawnego</span><span class="sxs-lookup"><span data-stu-id="b5609-134">Import the data into Excel and create a pivot chart</span></span>
<span data-ttu-id="b5609-135">Po nawiązaniu połączenia i utworzeniu pliku zawierającego dane oraz informacje o połączeniu należy zapoznać się z wskazówkami na temat importowania danych.</span><span class="sxs-lookup"><span data-stu-id="b5609-135">Now that you've established the connection and created the file with data and connection information, you're reading to import the data.</span></span>

1. <span data-ttu-id="b5609-136">W oknie dialogowym **Importowanie danych** kliknij opcję prezentacji danych w arkuszu, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5609-136">In the **Import Data** dialog, click the option you want for presenting your data in the worksheet and then click **OK**.</span></span> <span data-ttu-id="b5609-137">Wybrano **Wykres przestawny**.</span><span class="sxs-lookup"><span data-stu-id="b5609-137">We chose **PivotChart**.</span></span> <span data-ttu-id="b5609-138">Można również utworzyć **Nowy arkusz** lub wybrać opcję **Dodaj te dane do modelu danych**.</span><span class="sxs-lookup"><span data-stu-id="b5609-138">You can also choose to create a **New worksheet** or to **Add this data to a Data Model**.</span></span> <span data-ttu-id="b5609-139">Więcej informacji o modelach danych można znaleźć w temacie [Tworzenie modelu danych w programie Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="b5609-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="b5609-140">Kliknij przycisk **Właściwości**, aby zapoznać się z informacjami o pliku odc utworzonym w poprzednim kroku i wybrać opcje odświeżania danych.</span><span class="sxs-lookup"><span data-stu-id="b5609-140">Click **Properties** to explore information about the odc file you created in the previous step and to choose options for refreshing the data.</span></span>
   
    ![Wybieranie formatu danych w programie Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="b5609-142">Arkusz zawiera teraz pustą tabelę przestawną i wykres.</span><span class="sxs-lookup"><span data-stu-id="b5609-142">The worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="b5609-143">W obszarze **Pola tabeli przestawnej** zaznacz wszystkie pola wyboru dla pól do wyświetlenia.</span><span class="sxs-lookup"><span data-stu-id="b5609-143">Under **PivotTable Fields**, select all the check-boxes for the fields you want to view.</span></span>
   
    ![Skonfiguruj raport bazy danych.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="b5609-145">Aby połączyć inne skoroszyty i arkusze programu Excel z bazą danych, kliknij kartę **Dane**, następnie kliknij przycisk **Połączenia** oraz przycisk **Dodaj**, wybierz z listy utworzone połączenie, a następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="b5609-145">If you want to connect other Excel workbooks and worksheets to the database, click **Data**, click **Connections**, click **Add**, choose the connection you created from the list, and then click **Open**.</span></span>
> <span data-ttu-id="b5609-146">![Otwieranie połączenia z innego skoroszytu](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="b5609-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b5609-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b5609-147">Next steps</span></span>
* <span data-ttu-id="b5609-148">Aby wykonywać zaawansowane zapytania i analizy, zobacz temat [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) (Nawiązywanie połączenia z usługą SQL Database za pomocą programu SQL Server Management Studio).</span><span class="sxs-lookup"><span data-stu-id="b5609-148">Learn how to [Connect to SQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="b5609-149">Dowiedz się, jakie zalety mają [pule elastyczne](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="b5609-149">Learn about the benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="b5609-150">Dowiedz się, jak [utworzyć aplikację sieci Web, która łączy się z bazą danych SQL Database zaplecza](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b5609-150">Learn how to [create a web application that connects to SQL Database on the back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

