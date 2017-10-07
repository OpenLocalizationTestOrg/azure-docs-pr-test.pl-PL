---
title: Magazyn danych Azure tooyour danych aaaUse Redgate tooload | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse Redgate danych platformy Studio scenariuszach dotyczących magazynów danych."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="73a5a-103">Ładowanie danych za pomocą usługi Data Platform Studio firmy Redgate</span><span class="sxs-lookup"><span data-stu-id="73a5a-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="73a5a-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="73a5a-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="73a5a-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="73a5a-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="73a5a-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="73a5a-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="73a5a-107">BCP</span><span class="sxs-lookup"><span data-stu-id="73a5a-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="73a5a-108">W tym samouczku przedstawiono sposób toouse [Studio platforma danych firmy Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/) (punktu dystrybucji) toomove danych z lokalnego programu SQL Server tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="73a5a-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="73a5a-109">Studio platformy danych stosuje poprawki zgodności najbardziej odpowiednia hello i optymalizacje, co powoduje hello najkrótszej tooget sposób pracy z usługą Magazyn danych SQL.</span><span class="sxs-lookup"><span data-stu-id="73a5a-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="73a5a-110">Firma [Redgate](http://www.red-gate.com) to wieloletni partner firmy Microsoft, który dostarcza różne narzędzia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="73a5a-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="73a5a-111">Ta funkcja w usłudze Data Platform Studio została udostępniona bezpłatnie do użytku komercyjnego i niekomercyjnego.</span><span class="sxs-lookup"><span data-stu-id="73a5a-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="73a5a-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="73a5a-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="73a5a-113">Tworzenie lub identyfikowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="73a5a-113">Create or identify resources</span></span>
<span data-ttu-id="73a5a-114">Przed rozpoczęciem tego samouczka należy toohave:</span><span class="sxs-lookup"><span data-stu-id="73a5a-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="73a5a-115">**lokalnej bazy danych SQL Server**: hello dane, które mają tooSQL tooimport magazyn danych wymaga toocome z lokalnego programu SQL Server (w wersji 2008 R2 lub nowszy).</span><span class="sxs-lookup"><span data-stu-id="73a5a-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="73a5a-116">Usługa Data Platform Studio nie może bezpośrednio importować danych z usługi Azure SQL Database ani z plików tekstowych.</span><span class="sxs-lookup"><span data-stu-id="73a5a-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="73a5a-117">**Konto usługi Azure Storage**: Studio platformy danych przygotuje hello danych w magazynie obiektów Blob Azure przed załadowaniem go do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="73a5a-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="73a5a-118">konta magazynu Hello muszą używać modelu wdrażania hello "Resource Manager" (wartość domyślna hello) zamiast modelu wdrażania "Klasycznym" hello.</span><span class="sxs-lookup"><span data-stu-id="73a5a-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="73a5a-119">Dowiedz się, jeśli nie masz konta magazynu, jak tooCreate konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="73a5a-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="73a5a-120">**Usługa SQL Data Warehouse**: w tym samouczku przenosi hello dane z lokalnymi tooSQL programu SQL Server magazynu danych, więc należy toohave magazynu danych w trybie online.</span><span class="sxs-lookup"><span data-stu-id="73a5a-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="73a5a-121">Jeśli nie masz już magazyn danych, Dowiedz się jak tooCreate magazyn danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="73a5a-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="73a5a-122">Lepsza wydajność, jeśli konto magazynu hello i magazynu danych hello są tworzone w hello sam region.</span><span class="sxs-lookup"><span data-stu-id="73a5a-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="73a5a-123">Krok 1: Zaloguj się tooData Studio platformy z Twoim kontem platformy Azure</span><span class="sxs-lookup"><span data-stu-id="73a5a-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="73a5a-124">Otwórz przeglądarkę sieci web i przejdź toohello [Studio platformy danych](https://www.dataplatformstudio.com/) witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="73a5a-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="73a5a-125">Logowania z hello tego samego konta Azure tego możesz używane toocreate hello magazynu konta i magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="73a5a-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="73a5a-126">Jeśli adres e-mail jest skojarzony z służbowy lub konto służbowe i konto Microsoft, należy się toochoose hello konta, które ma dostęp do zasobów tooyour.</span><span class="sxs-lookup"><span data-stu-id="73a5a-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="73a5a-127">Jeśli jest to pierwsza przy użyciu danych Studio platformy, są zadawane toomanage uprawnienia aplikacji hello toogrant zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="73a5a-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="73a5a-128">Krok 2: Uruchom Kreatora importu hello</span><span class="sxs-lookup"><span data-stu-id="73a5a-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="73a5a-129">Z hello ekranu głównego punktu dystrybucji wybierz hello importu tooAzure SQL Data Warehouse łącze toostart hello importu Kreator.</span><span class="sxs-lookup"><span data-stu-id="73a5a-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="73a5a-130">Krok 3: Instalowanie hello bramy Studio platformy danych</span><span class="sxs-lookup"><span data-stu-id="73a5a-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="73a5a-131">tooconnect tooyour lokalną bazą danych programu SQL Server, należy tooinstall hello bramy punktu dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="73a5a-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="73a5a-132">Brama Hello jest agenta klienta, który zapewnia dostęp tooyour w lokalnym środowisku, wyodrębnia dane hello i przekazanie jej tooyour konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="73a5a-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="73a5a-133">Dane nigdy nie przechodzą przez serwery firmy Redgate.</span><span class="sxs-lookup"><span data-stu-id="73a5a-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="73a5a-134">Witaj tooinstall bramy:</span><span class="sxs-lookup"><span data-stu-id="73a5a-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="73a5a-135">Kliknij przycisk hello **Tworzenie bramy** łącza</span><span class="sxs-lookup"><span data-stu-id="73a5a-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="73a5a-136">Pobierz i zainstaluj hello bramę, używając hello podana Instalatora</span><span class="sxs-lookup"><span data-stu-id="73a5a-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="73a5a-137">Witaj bramy można zainstalować na dowolnym komputerze z bazy danych SQL Server źródła toohello dostępu do sieci.</span><span class="sxs-lookup"><span data-stu-id="73a5a-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="73a5a-138">Uzyskuje dostęp do bazy danych programu SQL Server hello przy użyciu uwierzytelniania systemu Windows przy użyciu poświadczeń hello hello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="73a5a-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="73a5a-139">Po zakończeniu instalacji hello tooConnected zmiany stanu bramy i wybraniu dalej.</span><span class="sxs-lookup"><span data-stu-id="73a5a-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="73a5a-140">Krok 4: Zidentyfikować hello źródłowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="73a5a-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="73a5a-141">W hello *wprowadź nazwę serwera* pole tekstowe, wprowadź nazwę hello powitania serwera, który jest hostem bazy danych i wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="73a5a-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="73a5a-142">Następnie z menu rozwijanego hello, wybierz tooimport danych z bazy danych hello.</span><span class="sxs-lookup"><span data-stu-id="73a5a-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="73a5a-143">Punktu dystrybucji sprawdza hello wybranej bazy danych dla tooimport tabel.</span><span class="sxs-lookup"><span data-stu-id="73a5a-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="73a5a-144">Domyślnie punktu dystrybucji importuje wszystkie tabele hello hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="73a5a-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="73a5a-145">Można wybrać, lub Anuluj wybór tabel, rozwijając powitalne link wszystkie tabele.</span><span class="sxs-lookup"><span data-stu-id="73a5a-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="73a5a-146">Wybierz hello dalej przycisk toomove do przodu.</span><span class="sxs-lookup"><span data-stu-id="73a5a-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="73a5a-147">Krok 5: Wybierz konto magazynu toostage hello danych</span><span class="sxs-lookup"><span data-stu-id="73a5a-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="73a5a-148">Punktu dystrybucji wyświetla monit o podanie danych hello toostage lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="73a5a-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="73a5a-149">Wybierz istniejące konto magazynu z subskrypcji, a następnie wybierz przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="73a5a-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="73a5a-150">Punktu dystrybucji utworzy nowy kontener obiektów blob w hello wybranego konta magazynu i użyć różnych folderu dla każdej operacji importowania.</span><span class="sxs-lookup"><span data-stu-id="73a5a-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="73a5a-151">Krok 6. Wybieranie magazynu danych</span><span class="sxs-lookup"><span data-stu-id="73a5a-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="73a5a-152">Następnie należy wybrać online [magazyn danych SQL Azure](http://aka.ms/sqldw) bazy danych hello tooimport do.</span><span class="sxs-lookup"><span data-stu-id="73a5a-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="73a5a-153">Po wybraniu bazy danych należy tooenter hello poświadczenia tooconnect toohello bazy danych, a następnie wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="73a5a-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="73a5a-154">Punktu dystrybucji scala tabel danych źródłowych hello hello hurtowni danych.</span><span class="sxs-lookup"><span data-stu-id="73a5a-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="73a5a-155">Punktu dystrybucji wyświetlane jest ostrzeżenie, jeśli nazwa tabeli hello wymaga toooverwrite istniejące tabele w magazynie danych hello.</span><span class="sxs-lookup"><span data-stu-id="73a5a-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="73a5a-156">Można opcjonalnie usunąć istniejących obiektów w magazynie danych hello wg Usuń wszystkie istniejące obiekty przed rozpoczęciem importowania.</span><span class="sxs-lookup"><span data-stu-id="73a5a-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="73a5a-157">Krok 7: Importowanie danych hello</span><span class="sxs-lookup"><span data-stu-id="73a5a-157">Step 7: Import hello data</span></span>
<span data-ttu-id="73a5a-158">Punktu dystrybucji potwierdza chcieliby tooimport hello danych.</span><span class="sxs-lookup"><span data-stu-id="73a5a-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="73a5a-159">Po prostu kliknij importu danych hello toobegin przycisk hello rozpoczęcia importowania.</span><span class="sxs-lookup"><span data-stu-id="73a5a-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="73a5a-160">Punktu dystrybucji Wyświetla wizualizację pokazujący postęp hello wyodrębnianie i przekazywanie danych hello z hello postępu programu SQL Server i hello lokalne powitania importu do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="73a5a-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="73a5a-161">Po zakończeniu importowania hello punktu dystrybucji Wyświetla podsumowanie importu danych hello i raport o zmianach hello zgodności poprawek, które mogły zostać wykonane.</span><span class="sxs-lookup"><span data-stu-id="73a5a-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="73a5a-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="73a5a-162">Next steps</span></span>
<span data-ttu-id="73a5a-163">tooexplore danych w usłudze SQL Data Warehouse, Rozpocznij od wyświetlenia:</span><span class="sxs-lookup"><span data-stu-id="73a5a-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="73a5a-164">[Tworzenie zapytań względem usługi Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="73a5a-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="73a5a-165">[Wizualizacja danych przy użyciu usługi Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="73a5a-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="73a5a-166">więcej informacji na temat Studio platforma danych firmy Redgate toolearn:</span><span class="sxs-lookup"><span data-stu-id="73a5a-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="73a5a-167">Odwiedź stronę główną punktu dystrybucji hello</span><span class="sxs-lookup"><span data-stu-id="73a5a-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="73a5a-168">Obejrzyj pokaz usługi DPS w witrynie Channel9</span><span class="sxs-lookup"><span data-stu-id="73a5a-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="73a5a-169">Omówienie inne sposoby toomigrate i ładowania danych w usłudze SQL Data Warehouse zobacz:</span><span class="sxs-lookup"><span data-stu-id="73a5a-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="73a5a-170">[Migrowanie tooSQL Twojego rozwiązania magazynu danych][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="73a5a-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* [<span data-ttu-id="73a5a-171">Ładowanie danych do usługi Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="73a5a-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="73a5a-172">Aby uzyskać więcej porad programistycznych, zobacz hello [omówienie programowania w usłudze SQL Data Warehouse](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="73a5a-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
