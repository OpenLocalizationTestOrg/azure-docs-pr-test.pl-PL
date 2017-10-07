---
title: aaaConnect Excel tooSQL bazy danych | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconnect programu Microsoft Excel tooAzure SQL bazy danych w chmurze hello. Importowanie danych do programu Excel, raportowanie i eksploracja danych."
services: sql-database
keywords: "Łączenie programu excel toosql, zaimportuj tooexcel danych"
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
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a><span data-ttu-id="f5ad9-105">Połączenia bazy danych Azure SQL tooan programu Excel i tworzenie raportu</span><span class="sxs-lookup"><span data-stu-id="f5ad9-105">Connect Excel tooan Azure SQL database and create a report</span></span>

<span data-ttu-id="f5ad9-106">Połącz Excel tooa SQL database w chmurze hello i importowanie danych i tworzenie tabel i wykresów na podstawie wartości w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-106">Connect Excel tooa SQL database in hello cloud and import data and create tables and charts based on values in hello database.</span></span> <span data-ttu-id="f5ad9-107">W tym samouczku skonfigurujesz połączenie hello pomiędzy programami Excel i tabelą bazy danych Zapisz plik hello, która przechowuje dane i hello informacje o połączeniu dla programu Excel, a następnie utworzysz wykres przestawny z hello wartościami bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-107">In this tutorial you will set up hello connection between Excel and a database table, save hello file that stores data and hello connection information for Excel, and then create a pivot chart from hello database values.</span></span>

<span data-ttu-id="f5ad9-108">Przed rozpoczęciem pracy będziesz potrzebować bazy danych SQL na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-108">You'll need a SQL database in Azure before you get started.</span></span> <span data-ttu-id="f5ad9-109">Jeśli nie masz, zobacz [utworzyć pierwszą bazę danych SQL](sql-database-get-started-portal.md) tooget bazy danych z przykładowymi danymi do pracy w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-109">If you don't have one, see [Create your first SQL database](sql-database-get-started-portal.md) tooget a database with sample data up and running in a few minutes.</span></span> <span data-ttu-id="f5ad9-110">W tym artykule będzie importować przykładowe dane do programu Excel z tego artykułu, ale można wykonać podobne kroki z użyciem własnych danych.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-110">In this article, you'll import sample data into Excel from that article, but you can follow similar steps with your own data.</span></span>

<span data-ttu-id="f5ad9-111">Potrzebna będzie również kopia programu Excel.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-111">You'll also need a copy of Excel.</span></span> <span data-ttu-id="f5ad9-112">W tym artykule wykorzystano program [Microsoft Excel 2016](https://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-112">This article uses [Microsoft Excel 2016](https://products.office.com/).</span></span>

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a><span data-ttu-id="f5ad9-113">Łączenie bazy danych SQL tooa programu Excel i tworzenie pliku odc</span><span class="sxs-lookup"><span data-stu-id="f5ad9-113">Connect Excel tooa SQL database and create an odc file</span></span>
1. <span data-ttu-id="f5ad9-114">bazy danych tooSQL programu Excel tooconnect, Otwórz program Excel, a następnie utwórz nowy skoroszyt lub Otwórz istniejący skoroszyt programu Excel.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-114">tooconnect Excel tooSQL database, open Excel and then create a new workbook or open an existing Excel workbook.</span></span>
2. <span data-ttu-id="f5ad9-115">Na pasku menu hello u góry strony hello powitania kliknij **danych**, kliknij przycisk **z innych źródeł**, a następnie kliknij przycisk **z programu SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-115">In hello menu bar at hello top of hello page click **Data**, click **From Other Sources**, and then click **From SQL Server**.</span></span>
   
   ![Wybierz źródło danych: Połącz program Excel tooSQL w bazie danych.](./media/sql-database-connect-excel/excel_data_source.png)
   
   <span data-ttu-id="f5ad9-117">zostanie otwarty Kreator połączenia danych Hello.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-117">hello Data Connection Wizard opens.</span></span>
3. <span data-ttu-id="f5ad9-118">W hello **połączyć tooDatabase serwera** okno dialogowe, hello typu bazy danych SQL **nazwy serwera** tooconnect tooin hello formularz <*servername* > **. database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-118">In hello **Connect tooDatabase Server** dialog box, type hello SQL Database **Server name** you want tooconnect tooin hello form <*servername*>**.database.windows.net**.</span></span> <span data-ttu-id="f5ad9-119">Na przykład **adworkserver.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-119">For example, **adworkserver.database.windows.net**.</span></span>
4. <span data-ttu-id="f5ad9-120">W obszarze **poświadczenia logowania**, kliknij przycisk **hello użyj następującej nazwy użytkownika i hasła**, typ hello **nazwy użytkownika** i **hasło** ustawione dla Witaj bazy danych programu SQL server podczas jego tworzenia, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-120">Under **Log on credentials**, click **Use hello following User Name and Password**, type hello **User Name** and **Password** you set up for hello SQL Database server when you created it, and then click **Next**.</span></span>
   
   ![Wpisz powitania serwera nazwę i poświadczenia logowania](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > <span data-ttu-id="f5ad9-122">W zależności od środowiska sieciowego może być możliwe tooconnect lub jeśli hello bazy danych programu SQL server nie zezwala na ruch z adresu IP klienta może spowodować utratę połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-122">Depending on your network environment, you may not be able tooconnect or you may lose hello connection if hello SQL Database server doesn't allow traffic from your client IP address.</span></span> <span data-ttu-id="f5ad9-123">Przejdź toohello [portalu Azure](https://portal.azure.com/), kliknij serwery SQL, kliknij serwer, kliknij ikonę Zapora w ustawieniach i Dodaj swój adres IP klienta.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-123">Go toohello [Azure portal](https://portal.azure.com/), click SQL servers, click your server, click firewall under settings and add your client IP address.</span></span> <span data-ttu-id="f5ad9-124">Zobacz [jak ustawienia zapory tooconfigure](sql-database-configure-firewall-settings.md) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-124">See [How tooconfigure firewall settings](sql-database-configure-firewall-settings.md) for details.</span></span>
   > 
   > 
5. <span data-ttu-id="f5ad9-125">W hello **wybierz bazę danych i tabeli** okno dialogowe, wybierz hello bazy danych, mają toowork z z listy hello, a następnie kliknij hello tabele lub widoki mają toowork z (Wybraliśmy **vGetAllCategories**), a następnie Kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-125">In hello **Select Database and Table** dialog, select hello database you want toowork with from hello list, and then click hello tables or views you want toowork with (we chose **vGetAllCategories**), and then click **Next**.</span></span>
   
    ![Wybierz bazę danych i tabelę.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    <span data-ttu-id="f5ad9-127">Witaj **zapisywanie pliku połączenia danych i kończenie** zostanie wyświetlone okno dialogowe, w którym należy podać informacje o pliku połączenia (*.odc) bazy danych pakietu Office hello, który korzysta z programu Excel.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-127">hello **Save Data Connection File and Finish** dialog box opens, where you provide information about hello Office database connection (*.odc) file that Excel uses.</span></span> <span data-ttu-id="f5ad9-128">Można pozostawić wartości domyślne hello lub dostosować ustawienia.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-128">You can leave hello defaults or customize your selections.</span></span>
6. <span data-ttu-id="f5ad9-129">Możesz pozostawić domyślne hello, ale hello Uwaga **nazwę pliku** w szczególności.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-129">You can leave hello defaults, but note hello **File Name** in particular.</span></span> <span data-ttu-id="f5ad9-130">A **opis**, **przyjazną nazwę**, i **słowa kluczowe do wyszukania** ułatwiają i innym użytkownikom, co w przypadku podłączania tooand odnaleźć hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-130">A **Description**, a **Friendly Name**, and **Search Keywords** help you and other users remember what you're connecting tooand find hello connection.</span></span> <span data-ttu-id="f5ad9-131">Kliknij przycisk **zawsze podejmować toouse te dane toorefresh pliku** Jeśli chcesz, aby przechowywane w pliku odc hello, więc można zaktualizować, gdy połączenie tooit, a następnie kliknij przycisk informacje o połączeniu **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-131">Click **Always attempt toouse this file toorefresh data** if you want connection information stored in hello odc file so it can update when you connect tooit, and then click **Finish**.</span></span>
   
    ![Zapisywanie pliku odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    <span data-ttu-id="f5ad9-133">Witaj **importowania danych** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-133">hello **Import data** dialog box appears.</span></span>

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a><span data-ttu-id="f5ad9-134">Importowanie danych hello do programu Excel i tworzenie wykresu przestawnego</span><span class="sxs-lookup"><span data-stu-id="f5ad9-134">Import hello data into Excel and create a pivot chart</span></span>
<span data-ttu-id="f5ad9-135">Teraz, gdy zostaną utworzone połączenie hello i hello utworzony plik z danych oraz informacje o połączeniu, czytasz tooimport hello danych.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-135">Now that you've established hello connection and created hello file with data and connection information, you're reading tooimport hello data.</span></span>

1. <span data-ttu-id="f5ad9-136">W hello **i zaimportuj dane** okna dialogowego, kliknij hello opcję prezentacji danych w arkuszu hello, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-136">In hello **Import Data** dialog, click hello option you want for presenting your data in hello worksheet and then click **OK**.</span></span> <span data-ttu-id="f5ad9-137">Wybrano **Wykres przestawny**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-137">We chose **PivotChart**.</span></span> <span data-ttu-id="f5ad9-138">Możesz również toocreate **nowy arkusz** lub zbyt**Dodaj ten tooa danych modelu danych**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-138">You can also choose toocreate a **New worksheet** or too**Add this data tooa Data Model**.</span></span> <span data-ttu-id="f5ad9-139">Więcej informacji o modelach danych można znaleźć w temacie [Tworzenie modelu danych w programie Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-139">For more information on Data Models, see [Create a data model in Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B).</span></span> <span data-ttu-id="f5ad9-140">Kliknij przycisk **właściwości** tooexplore informacji na temat hello pliku odc utworzone w hello poprzedniego kroku i toochoose opcje odświeżania danych hello.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-140">Click **Properties** tooexplore information about hello odc file you created in hello previous step and toochoose options for refreshing hello data.</span></span>
   
    ![Wybieranie formatu hello danych w programie Excel](./media/sql-database-connect-excel/import-data.png)
   
    <span data-ttu-id="f5ad9-142">Witaj arkusz zawiera teraz pustą tabelę przestawną i wykres.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-142">hello worksheet now has an empty pivot table and chart.</span></span>
2. <span data-ttu-id="f5ad9-143">W obszarze **pól tabeli przestawnej**, wybierz hello wszystkich pól wyboru dla hello pola mają tooview.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-143">Under **PivotTable Fields**, select all hello check-boxes for hello fields you want tooview.</span></span>
   
    ![Skonfiguruj raport bazy danych.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> <span data-ttu-id="f5ad9-145">Tooconnect innych Excel skoroszyty i arkusze toohello bazy danych, kliknij przycisk **danych**, kliknij przycisk **połączeń**, kliknij przycisk **Dodaj**, wybierz utworzone połączenie hello z listy hello, a następnie kliknij przycisk **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-145">If you want tooconnect other Excel workbooks and worksheets toohello database, click **Data**, click **Connections**, click **Add**, choose hello connection you created from hello list, and then click **Open**.</span></span>
> <span data-ttu-id="f5ad9-146">![Otwieranie połączenia z innego skoroszytu](./media/sql-database-connect-excel/open-from-another-workbook.png)</span><span class="sxs-lookup"><span data-stu-id="f5ad9-146">![Open a connection from another workbook](./media/sql-database-connect-excel/open-from-another-workbook.png)</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f5ad9-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f5ad9-147">Next steps</span></span>
* <span data-ttu-id="f5ad9-148">Dowiedz się, jak za[uzyskuj tooSQL bazy danych programu SQL Server Management Studio](sql-database-connect-query-ssms.md) zaawansowane zapytania i analizy.</span><span class="sxs-lookup"><span data-stu-id="f5ad9-148">Learn how too[Connect tooSQL Database with SQL Server Management Studio](sql-database-connect-query-ssms.md) for advanced querying and analysis.</span></span>
* <span data-ttu-id="f5ad9-149">Więcej informacji na temat zalet hello [pule elastyczne](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-149">Learn about hello benefits of [elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="f5ad9-150">Dowiedz się, jak za[tworzenia aplikacji sieci web, łączącego tooSQL bazy danych na powitania zaplecza](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f5ad9-150">Learn how too[create a web application that connects tooSQL Database on hello back-end](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span>

