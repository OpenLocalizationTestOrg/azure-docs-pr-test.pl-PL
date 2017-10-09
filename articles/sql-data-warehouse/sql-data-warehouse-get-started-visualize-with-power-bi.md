---
title: "aaaVisualize danych magazynu danych SQL za pomocą Power BI | Microsoft Azure"
description: "Wizualizacja danych usługi SQL Data Warehouse przy użyciu usługi Power BI"
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: d7fb89d1-da1d-4788-a111-68d0e3fda799
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: 0425cf5abe7bc001b2a41df4d09bf5f2e42527e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-data-with-power-bi"></a><span data-ttu-id="acaed-103">Wizualizacja danych przy użyciu usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="acaed-103">Visualize data with Power BI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="acaed-104">Power BI</span><span class="sxs-lookup"><span data-stu-id="acaed-104">Power BI</span></span>](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [<span data-ttu-id="acaed-105">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="acaed-105">Azure Machine Learning</span></span>](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [<span data-ttu-id="acaed-106">Program Visual Studio</span><span class="sxs-lookup"><span data-stu-id="acaed-106">Visual Studio</span></span>](sql-data-warehouse-query-visual-studio.md)
> * [<span data-ttu-id="acaed-107">sqlcmd</span><span class="sxs-lookup"><span data-stu-id="acaed-107">sqlcmd</span></span>](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [<span data-ttu-id="acaed-108">SSMS</span><span class="sxs-lookup"><span data-stu-id="acaed-108">SSMS</span></span>](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="acaed-109">W tym samouczku przedstawiono sposób toouse usługi Power BI tooconnect tooSQL magazynu danych oraz tworzenia podstawowych wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="acaed-109">This tutorial shows you how toouse Power BI tooconnect tooSQL Data Warehouse and create a few basic visualizations.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Data-Warehouse-Sample-Data-and-PowerBI/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="acaed-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="acaed-110">Prerequisites</span></span>
<span data-ttu-id="acaed-111">toostep opisanych w tym samouczku, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="acaed-111">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="acaed-112">Magazyn danych SQL są wstępnie załadowane z bazą danych AdventureWorksDW hello.</span><span class="sxs-lookup"><span data-stu-id="acaed-112">A SQL Data Warehouse pre-loaded with hello AdventureWorksDW database.</span></span> <span data-ttu-id="acaed-113">tooprovision tego, zobacz [Tworzenie usługi SQL Data Warehouse] [ Create a SQL Data Warehouse] i wybierz polecenie tooload hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="acaed-113">tooprovision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose tooload hello sample data.</span></span> <span data-ttu-id="acaed-114">Jeśli masz już magazyn danych, ale bez przykładowych danych, możesz [ręcznie załadować przykładowe dane][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="acaed-114">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-connect-tooyour-database"></a><span data-ttu-id="acaed-115">1. Połącz tooyour bazy danych</span><span class="sxs-lookup"><span data-stu-id="acaed-115">1. Connect tooyour database</span></span>
<span data-ttu-id="acaed-116">tooopen usługi Power BI i Połącz z bazą danych AdventureWorksDW tooyour:</span><span class="sxs-lookup"><span data-stu-id="acaed-116">tooopen Power BI and connect tooyour AdventureWorksDW database:</span></span>

1. <span data-ttu-id="acaed-117">Zaloguj się na powitania [portalu Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="acaed-117">Sign into hello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="acaed-118">Kliknij pozycję **Bazy danych SQL** i wybierz bazę danych AdventureWorks usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="acaed-118">Click **SQL databases** and choose your AdventureWorks SQL Data Warehouse database.</span></span>
   
    ![Znajdowanie bazy danych][1]
3. <span data-ttu-id="acaed-120">Kliknij przycisk "Otwórz w usłudze Power BI" hello.</span><span class="sxs-lookup"><span data-stu-id="acaed-120">Click hello 'Open in Power BI' button.</span></span>
   
    ![Przycisk usługi Power BI][2]
4. <span data-ttu-id="acaed-122">Powinna zostać wyświetlona strona połączenia SQL Data Warehouse hello wyświetlanie adres sieci web bazy danych.</span><span class="sxs-lookup"><span data-stu-id="acaed-122">You should now see hello SQL Data Warehouse connection page displaying your database web address.</span></span> <span data-ttu-id="acaed-123">Kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="acaed-123">Click next.</span></span>
   
    ![Połączenie z usługą Power BI][3]
5. <span data-ttu-id="acaed-125">Wprowadź nazwę użytkownika serwera Azure SQL i hasło i będzie bazy danych magazynu danych SQL tooyour pełni połączonych.</span><span class="sxs-lookup"><span data-stu-id="acaed-125">Enter your Azure SQL server username and password and you will be fully connected tooyour SQL Data Warehouse database.</span></span>
   
    ![Logowanie w usłudze Power BI][4]
6. <span data-ttu-id="acaed-127">Po zalogowaniu się do usługi Power BI, kliknij przycisk hello zestaw danych AdventureWorksDW w lewym bloku hello.</span><span class="sxs-lookup"><span data-stu-id="acaed-127">Once you have signed into Power BI, click hello AdventureWorksDW dataset on hello left blade.</span></span> <span data-ttu-id="acaed-128">Spowoduje to otwarcie hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="acaed-128">This will open hello database.</span></span>
   
    ![Otwieranie bazy danych AdventureWorksDW w usłudze Power BI][5]

## <a name="2-create-a-report"></a><span data-ttu-id="acaed-130">2. Tworzenie raportu</span><span class="sxs-lookup"><span data-stu-id="acaed-130">2. Create a report</span></span>
<span data-ttu-id="acaed-131">Użytkownik jest teraz gotowy toouse usługi Power BI tooanalyze przykładowe dane AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="acaed-131">You are now ready toouse Power BI tooanalyze your AdventureWorksDW sample data.</span></span> <span data-ttu-id="acaed-132">Analiza hello tooperform, AdventureWorksDW ma widok o nazwie widoku AggregateSales.</span><span class="sxs-lookup"><span data-stu-id="acaed-132">tooperform hello analysis, AdventureWorksDW has a view called AggregateSales.</span></span> <span data-ttu-id="acaed-133">Ten widok zawiera kilka hello kluczowych metryk do analizowania sprzedaży firmy hello hello.</span><span class="sxs-lookup"><span data-stu-id="acaed-133">This view contains a few of hello key metrics for analyzing hello sales of hello company.</span></span>

1. <span data-ttu-id="acaed-134">toocreate mapę kwot sprzedaży, zgodnie z toopostal kodu, w okienku pól po prawej stronie powitania kliknij hello widoku AggregateSales widoku tooexpand go.</span><span class="sxs-lookup"><span data-stu-id="acaed-134">toocreate a map of sales amount according toopostal code, in hello right-hand fields pane, click hello AggregateSales view tooexpand it.</span></span> <span data-ttu-id="acaed-135">Kliknij przycisk hello KodPocztowy i kwoty sprzedaży tooselect kolumn je.</span><span class="sxs-lookup"><span data-stu-id="acaed-135">Click hello PostalCode and SalesAmount columns tooselect them.</span></span>
   
    ![Wybór widoku AggregateSales w usłudze Power BI][6]
   
    <span data-ttu-id="acaed-137">Usługa Power BI automatycznie rozpoznaje dane geograficzne i umieszcza je na mapie.</span><span class="sxs-lookup"><span data-stu-id="acaed-137">Power BI automatically recognizes this is geographic data and put it in a map for you.</span></span>
   
    ![Mapa w usłudze Power BI][7]
2. <span data-ttu-id="acaed-139">W tym kroku zostanie utworzony wykres słupkowy przedstawiający kwotę sprzedaży w odniesieniu do dochodu klienta.</span><span class="sxs-lookup"><span data-stu-id="acaed-139">This step creates a bar graph that shows amount of sales per customer income.</span></span> <span data-ttu-id="acaed-140">toocreate to przejdź toohello widoku AggregateSales widok rozszerzony.</span><span class="sxs-lookup"><span data-stu-id="acaed-140">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="acaed-141">Kliknij pole kwoty sprzedaży hello.</span><span class="sxs-lookup"><span data-stu-id="acaed-141">Click hello SalesAmount field.</span></span> <span data-ttu-id="acaed-142">Przeciągnij hello dochód klienta pola toohello lewo i upuść ją na osi.</span><span class="sxs-lookup"><span data-stu-id="acaed-142">Drag hello Customer Income field toohello left and drop it into Axis.</span></span>
   
    ![Wybór osi w usłudze Power BI][8]
   
    <span data-ttu-id="acaed-144">Przenieśliśmy wykres słupkowy hello na lewą hello.</span><span class="sxs-lookup"><span data-stu-id="acaed-144">We moved hello bar chart over hello left.</span></span>
   
    ![Wykres słupkowy w usłudze Power BI][9]
3. <span data-ttu-id="acaed-146">W tym kroku utworzymy wykres liniowy, który przedstawia kwoty sprzedaży według dat zamówienia.</span><span class="sxs-lookup"><span data-stu-id="acaed-146">This step creates a line chart that shows sales amount per order date.</span></span> <span data-ttu-id="acaed-147">toocreate to przejdź toohello widoku AggregateSales widok rozszerzony.</span><span class="sxs-lookup"><span data-stu-id="acaed-147">toocreate this go toohello expanded AggregateSales view.</span></span> <span data-ttu-id="acaed-148">Kliknij pola SalesAmount (Kwota sprzedaży) i OrderDate (Data zamówienia).</span><span class="sxs-lookup"><span data-stu-id="acaed-148">Click SalesAmount and OrderDate.</span></span> <span data-ttu-id="acaed-149">W kolumnie wizualizacje powitania kliknij ikonę wykres liniowy hello; jest to pierwsza ikona hello w hello drugim wierszu w obszarze wizualizacji.</span><span class="sxs-lookup"><span data-stu-id="acaed-149">In hello Visualizations column click hello Line Chart icon; this is hello first icon in hello second line under visualizations.</span></span>
   
    ![Wybór wykresu liniowego w usłudze Power BI][10]
   
    <span data-ttu-id="acaed-151">Masz teraz raport wyświetlający trzy różne wizualizacje danych hello.</span><span class="sxs-lookup"><span data-stu-id="acaed-151">You now have a report that shows three different visualizations of hello data.</span></span>
   
    ![Wykres liniowy w usłudze Power BI][11]

<span data-ttu-id="acaed-153">W dowolnym momencie możesz kliknąć menu **Plik** i wybrać polecenie **Zapisz**, aby zapisać postęp.</span><span class="sxs-lookup"><span data-stu-id="acaed-153">You can save your progress at any time by clicking **File** and selecting **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="acaed-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="acaed-154">Next steps</span></span>
<span data-ttu-id="acaed-155">Teraz, gdy firma Microsoft została podana możesz niektórych toowarm czasu hello przykładowych danych, zobacz temat jak zbyt[opracowanie][develop], [załadować][load], lub [ Migrowanie][migrate].</span><span class="sxs-lookup"><span data-stu-id="acaed-155">Now that we've given you some time toowarm up with hello sample data, see how too[develop][develop], [load][load], or [migrate][migrate].</span></span> <span data-ttu-id="acaed-156">Lub Spójrz na powitania [witryny sieci Web usługi Power BI][Power BI website].</span><span class="sxs-lookup"><span data-stu-id="acaed-156">Or take a look at hello [Power BI website][Power BI website].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-find-database.png
[2]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-button.png
[3]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-connect-to-azure.png
[4]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-sign-in.png
[5]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-open-adventureworks.png
[6]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-aggregatesales.png
[7]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-map.png
[8]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-chooseaxis.png
[9]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-bar.png
[10]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-prepare-line.png
[11]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-line.png
[12]: media/sql-data-warehouse-get-started-visualize-with-power-bi/pbi-save.png

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[connecting tooSQL Data Warehouse]: sql-data-warehouse-integrate-power-bi.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md

<!--Other-->
[Azure portal]: https://portal.azure.com/
[Power BI website]: http://www.powerbi.com/
