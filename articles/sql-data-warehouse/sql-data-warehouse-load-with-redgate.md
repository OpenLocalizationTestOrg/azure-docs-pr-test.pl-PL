---
title: "Ładowanie danych do magazynu danych platformy Azure za pomocą usługi firmy Redgate | Microsoft Docs"
description: "Dowiedz się, jak używać usługi Data Platform Studio firmy Redgate na potrzeby scenariuszy magazynowania danych."
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
ms.openlocfilehash: a38b237d5bfc0450c1ca79b53a5784dbb9bf8602
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="09028-103">Ładowanie danych za pomocą usługi Data Platform Studio firmy Redgate</span><span class="sxs-lookup"><span data-stu-id="09028-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="09028-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="09028-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="09028-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="09028-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="09028-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="09028-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="09028-107">BCP</span><span class="sxs-lookup"><span data-stu-id="09028-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="09028-108">W tym samouczku pokazano, w jaki sposób używać usługi [Data Platform Studio (DPS) firmy Redgate](http://www.red-gate.com/products/azure-development/data-platform-studio/), aby przenieść dane z lokalnego programu SQL Server do usługi Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="09028-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premises SQL Server to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="09028-109">Usługa Data Platform Studio stosuje najbardziej odpowiednie poprawki zgodności i optymalizacje, więc stanowi najszybszy sposób na rozpoczęcie pracy z usługą SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="09028-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="09028-110">Firma [Redgate](http://www.red-gate.com) to wieloletni partner firmy Microsoft, który dostarcza różne narzędzia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="09028-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="09028-111">Ta funkcja w usłudze Data Platform Studio została udostępniona bezpłatnie do użytku komercyjnego i niekomercyjnego.</span><span class="sxs-lookup"><span data-stu-id="09028-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="09028-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="09028-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="09028-113">Tworzenie lub identyfikowanie zasobów</span><span class="sxs-lookup"><span data-stu-id="09028-113">Create or identify resources</span></span>
<span data-ttu-id="09028-114">Przed rozpoczęciem tego samouczka trzeba mieć następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="09028-114">Before starting this tutorial, you need to have:</span></span>

* <span data-ttu-id="09028-115">**lokalna baza danych programu SQL Server**: dane do zaimportowania do usługi SQL Data Warehouse muszą pochodzić z lokalnego programu SQL Server (wersja 2008 R2 lub nowsza).</span><span class="sxs-lookup"><span data-stu-id="09028-115">**on-premises SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="09028-116">Usługa Data Platform Studio nie może bezpośrednio importować danych z usługi Azure SQL Database ani z plików tekstowych.</span><span class="sxs-lookup"><span data-stu-id="09028-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="09028-117">**Konto usługi Azure Storage**: usługa Data Platform Studio przygotowuje dane w usłudze Azure Blob Storage przed załadowaniem ich do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="09028-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="09028-118">Konto magazynu musi używać modelu wdrażania usługi Resource Manager (domyślnie), a nie klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="09028-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span></span> <span data-ttu-id="09028-119">Jeśli nie masz jeszcze konta magazynu, dowiedz się, jak je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="09028-119">If you don't have a storage account, learn how to Create a storage account.</span></span> 
* <span data-ttu-id="09028-120">**Magazyn danych usługi SQL Data Warehouse**: w tym samouczku znajdują się informacje dotyczące przenoszenia danych z lokalnego programu SQL Server do usługi SQL Data Warehouse, więc magazyn danych musi być w trybie online.</span><span class="sxs-lookup"><span data-stu-id="09028-120">**SQL Data Warehouse**: This tutorial moves the data from on-premises SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span></span> <span data-ttu-id="09028-121">Jeśli nie masz jeszcze magazynu danych, dowiedz się, jak utworzyć magazyn danych usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="09028-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="09028-122">Można zwiększyć wydajność, jeśli konto magazynu i magazyn danych zostaną utworzone w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="09028-122">Performance is improved if the storage account and the data warehouse are created in the same region.</span></span>
> 
> 

## <a name="step-1-sign-in-to-data-platform-studio-with-your-azure-account"></a><span data-ttu-id="09028-123">Krok 1. Logowanie się do usługi Data Platform Studio za pomocą konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="09028-123">Step 1: Sign in to Data Platform Studio with your Azure account</span></span>
<span data-ttu-id="09028-124">Otwórz przeglądarkę sieci Web i przejdź do witryny sieci Web usługi [Data Platform Studio](https://www.dataplatformstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="09028-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="09028-125">Zaloguj się przy użyciu tego samego konta platformy Azure, które zostało użyte do utworzenia konta magazynu i magazynu danych.</span><span class="sxs-lookup"><span data-stu-id="09028-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span></span> <span data-ttu-id="09028-126">Jeśli Twój adres e-mail jest skojarzony zarówno z kontem służbowym, jak i kontem Microsoft, upewnij się, że wybrane zostało konto, które ma dostęp do zasobów.</span><span class="sxs-lookup"><span data-stu-id="09028-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span></span>

> [!NOTE]
> <span data-ttu-id="09028-127">Jeśli używasz usługi Data Platform Studio pierwszy raz, zostanie wyświetlona prośba o nadanie aplikacji uprawnień do zarządzania zasobami platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="09028-127">If this is your first time using Data Platform Studio, you are asked to grant the application permission to manage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-the-import-wizard"></a><span data-ttu-id="09028-128">Krok 2. Uruchamianie kreatora importu</span><span class="sxs-lookup"><span data-stu-id="09028-128">Step 2: Start the Import Wizard</span></span>
<span data-ttu-id="09028-129">Z poziomu ekranu głównego usługi DPS wybierz link Import to Azure SQL Data Warehouse (Importuj do usługi Azure SQL Data Warehouse), aby uruchomić kreatora importu.</span><span class="sxs-lookup"><span data-stu-id="09028-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span></span>

![][1]

## <a name="step-3-install-the-data-platform-studio-gateway"></a><span data-ttu-id="09028-130">Krok 3. Instalowanie bramy usługi Data Platform Studio</span><span class="sxs-lookup"><span data-stu-id="09028-130">Step 3: Install the Data Platform Studio Gateway</span></span>
<span data-ttu-id="09028-131">Aby nawiązać połączenie z lokalną bazą danych programu SQL Server, należy zainstalować bramę usługi DPS.</span><span class="sxs-lookup"><span data-stu-id="09028-131">To connect to your on-premises SQL Server database, you need to install the DPS Gateway.</span></span> <span data-ttu-id="09028-132">Brama to agent klienta, który zapewnia dostęp do środowiska lokalnego, wyodrębnia dane i przekazuje je do używanego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="09028-132">The gateway is a client agent that provides access to your on-premises environment, extracts the data, and uploads it to your storage account.</span></span> <span data-ttu-id="09028-133">Dane nigdy nie przechodzą przez serwery firmy Redgate.</span><span class="sxs-lookup"><span data-stu-id="09028-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="09028-134">Aby zainstalować bramę:</span><span class="sxs-lookup"><span data-stu-id="09028-134">To install the Gateway:</span></span>

1. <span data-ttu-id="09028-135">Kliknij link **Create Gateway** (Utwórz bramę)</span><span class="sxs-lookup"><span data-stu-id="09028-135">Click the **Create Gateway** link</span></span>
2. <span data-ttu-id="09028-136">Pobierz i zainstaluj bramę przy użyciu udostępnionego instalatora</span><span class="sxs-lookup"><span data-stu-id="09028-136">Download and install the Gateway using the provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="09028-137">Bramę można zainstalować na dowolnej maszynie z dostępem sieciowym do źródłowej bazy danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="09028-137">The Gateway can be installed on any machine with network access to the source SQL Server database.</span></span> <span data-ttu-id="09028-138">Uzyskuje ona dostęp do bazy danych programu SQL Server przy użyciu uwierzytelniania systemu Windows i poświadczeń bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="09028-138">It accesses the SQL Server database using Windows authentication with the credentials of the current user.</span></span>
> 
> 

<span data-ttu-id="09028-139">Po zainstalowaniu stan bramy zmienia się na wartość Connected (Połączona) i możliwe jest wybranie pozycji Next (Dalej).</span><span class="sxs-lookup"><span data-stu-id="09028-139">Once installed, the Gateway status changes to Connected and you can select Next.</span></span>

## <a name="step-4-identify-the-source-database"></a><span data-ttu-id="09028-140">Krok 4. Identyfikacja źródłowej bazy danych</span><span class="sxs-lookup"><span data-stu-id="09028-140">Step 4: Identify the source database</span></span>
<span data-ttu-id="09028-141">W polu tekstowym *Enter Server Name* (Wprowadź nazwę serwera) wprowadź nazwę serwera, na którym znajduje się baza danych, a następnie wybierz przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="09028-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span></span> <span data-ttu-id="09028-142">Następnie z menu rozwijanego wybierz bazę danych, z której chcesz zaimportować dane.</span><span class="sxs-lookup"><span data-stu-id="09028-142">Then, from the drop-down menu, select the database you want to import data from.</span></span>

![][3]

<span data-ttu-id="09028-143">Usługa DPS sprawdza wybraną bazę danych pod kątem tabel do zaimportowania.</span><span class="sxs-lookup"><span data-stu-id="09028-143">DPS inspects the selected database for tables to import.</span></span> <span data-ttu-id="09028-144">Domyślnie usługa DPS importuje wszystkie tabele znajdujące się w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="09028-144">By default, DPS imports all the tables in the database.</span></span> <span data-ttu-id="09028-145">Tabele można wybrać lub anulować ich wybór, rozwijając link All Tables (Wszystkie tabele).</span><span class="sxs-lookup"><span data-stu-id="09028-145">You can select or deselect tables by expanding the All Tables link.</span></span> <span data-ttu-id="09028-146">Wybierz przycisk Next (Dalej), aby przejść dalej.</span><span class="sxs-lookup"><span data-stu-id="09028-146">Select the Next button to move forward.</span></span>

## <a name="step-5-choose-a-storage-account-to-stage-the-data"></a><span data-ttu-id="09028-147">Krok 5. Wybieranie konta magazynu do przygotowania danych</span><span class="sxs-lookup"><span data-stu-id="09028-147">Step 5: Choose a storage account to stage the data</span></span>
<span data-ttu-id="09028-148">Usługa DPS wyświetla monit o lokalizację, w której mają zostać przygotowane dane.</span><span class="sxs-lookup"><span data-stu-id="09028-148">DPS prompts you for a location to stage the data.</span></span> <span data-ttu-id="09028-149">Wybierz istniejące konto magazynu z subskrypcji, a następnie wybierz przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="09028-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="09028-150">Usługa DPS utworzy nowy kontener obiektów blob na wybranym koncie magazynu i użyje oddzielnego folderu dla każdego importu.</span><span class="sxs-lookup"><span data-stu-id="09028-150">DPS will create a new blob container in the chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="09028-151">Krok 6. Wybieranie magazynu danych</span><span class="sxs-lookup"><span data-stu-id="09028-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="09028-152">Następnie wybierz bazę danych usługi [Azure SQL Data Warehouse](http://aka.ms/sqldw) w trybie online, do której zostaną zaimportowane dane.</span><span class="sxs-lookup"><span data-stu-id="09028-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span></span> <span data-ttu-id="09028-153">Po wybraniu bazy danych wprowadź poświadczenia, aby nawiązać połączenie z bazą danych. Następnie wybierz przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="09028-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="09028-154">Usługa DPS scala tabele danych źródłowych w magazyn danych.</span><span class="sxs-lookup"><span data-stu-id="09028-154">DPS merges the source data tables into the data warehouse.</span></span> <span data-ttu-id="09028-155">Usługa DPS wyświetli ostrzeżenie, jeśli ze względu na nazwę tabeli wymagane jest zastąpienie istniejących tabel w magazynie danych.</span><span class="sxs-lookup"><span data-stu-id="09028-155">DPS warns you if the table name requires it to overwrite existing tables in the data warehouse.</span></span> <span data-ttu-id="09028-156">Opcjonalnie można usunąć dowolne istniejące obiekty w magazynie danych, zaznaczając pole wyboru Delete all existing objects (Usuń wszystkie zaznaczone obiekty) przed zaimportowaniem.</span><span class="sxs-lookup"><span data-stu-id="09028-156">You may optionally delete any existing objects in the data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-the-data"></a><span data-ttu-id="09028-157">Krok 7. Importowanie danych</span><span class="sxs-lookup"><span data-stu-id="09028-157">Step 7: Import the data</span></span>
<span data-ttu-id="09028-158">Usługa DPS wyświetla potwierdzenie, czy dane mają zostać zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="09028-158">DPS confirms that you would like to import the data.</span></span> <span data-ttu-id="09028-159">Po prostu kliknij przycisk Start import (Rozpocznij import), aby rozpocząć import danych.</span><span class="sxs-lookup"><span data-stu-id="09028-159">Simply click the Start import button to begin the data import.</span></span>

![][6]

<span data-ttu-id="09028-160">Usługa DPS wyświetla wizualizację, która przedstawia postęp pobierania i przekazywania danych z lokalnego programu SQL Server i postęp importowania do usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="09028-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premises SQL Server and the progress of the import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="09028-161">Po ukończeniu importowania usługa DPS wyświetla podsumowanie importu danych i raport zmian poprawek zgodności, które zostały wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="09028-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="09028-162">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="09028-162">Next steps</span></span>
<span data-ttu-id="09028-163">Aby eksplorować dane w usłudze SQL Data Warehouse, należy rozpocząć od zapoznania się z następującymi tematami:</span><span class="sxs-lookup"><span data-stu-id="09028-163">To explore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="09028-164">[Tworzenie zapytań względem usługi Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="09028-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="09028-165">[Wizualizacja danych przy użyciu usługi Power BI][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="09028-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="09028-166">Aby dowiedzieć się więcej o usłudze Data Platform Studio firmy Redgate:</span><span class="sxs-lookup"><span data-stu-id="09028-166">To learn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="09028-167">Odwiedź stronę główną usługi DPS</span><span class="sxs-lookup"><span data-stu-id="09028-167">Visit the DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="09028-168">Obejrzyj pokaz usługi DPS w witrynie Channel9</span><span class="sxs-lookup"><span data-stu-id="09028-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="09028-169">Aby uzyskać przegląd innych sposobów migracji i ładowania danych w usłudze SQL Data Warehouse, zobacz:</span><span class="sxs-lookup"><span data-stu-id="09028-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="09028-170">[Migracja rozwiązania do usługi SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="09028-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span></span>
* [<span data-ttu-id="09028-171">Ładowanie danych do usługi Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="09028-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="09028-172">Aby uzyskać więcej porad programistycznych, zobacz [Omówienie programowania w usłudze SQL Data Warehouse](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="09028-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

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
[Migrate your solution to SQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
