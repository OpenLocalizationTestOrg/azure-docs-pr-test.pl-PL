---
title: "Proces nauki danych zespołu w działaniu: przy użyciu usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: Proces zaawansowane metody analizy i technologii w akcji
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: ce7de48af0f2f21576c66a962b88635a0f9f8333
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="9cd3e-103">Proces nauki danych zespołu w działaniu: przy użyciu magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="9cd3e-103">The Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="9cd3e-104">W tym samouczku, możemy opisano tworzenie i wdrażanie modelu uczenia maszynowego przy użyciu magazynu danych SQL (SQL DW) dla elementu dataset publicznie dostępnych — [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="9cd3e-105">Model klasyfikacji binarnej skonstruowany prognozuje czy poradę ma być stosowany w podróży i modele wieloklasowej klasyfikacji i regresji omówiono także które prognozowania dystrybucji dla kwoty Porada płatnej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-105">The binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict the distribution for the tip amounts paid.</span></span>

<span data-ttu-id="9cd3e-106">Wykonuje procedurę [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-106">The procedure follows the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="9cd3e-107">Firma Microsoft pokazują, jak skonfigurować środowisko analizy danych, jak załadować dane do magazynu danych SQL i sposobie używania magazynu danych SQL lub notesu IPython, aby eksplorować dane i odtwarzania funkcje do modelu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-107">We show how to setup a data science environment, how to load the data into SQL DW, and how use either SQL DW or an IPython Notebook to explore the data and engineer features to model.</span></span> <span data-ttu-id="9cd3e-108">Firma Microsoft następnie przedstawiono sposób tworzenia i wdrażania modelu przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-108">We then show how to build and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="9cd3e-109"><a name="dataset"></a>Zestaw danych rund taksówki NYC</span><span class="sxs-lookup"><span data-stu-id="9cd3e-109"><a name="dataset"></a>The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="9cd3e-110">Dane podróży taksówki NYC składa się z około 20GB skompresowanego plików CSV (~ 48GB nieskompresowane), rejestrowanie ponad milion 173 poszczególnych podróży i opłaty płatnej dla każdej podróży.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-110">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="9cd3e-111">Każdy rekord podróży obejmuje odbiór i przyjmowania lokalizacje i godziny, hack anonimowe (sterownik) numer licencji i numer Medalionu (taksówki jego unikatowy identyfikator).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-111">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="9cd3e-112">Dane obejmuje wszystkie rund w roku 2013 i jest dostępne w następujących dwóch zestawów danych dla każdego miesiąca:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="9cd3e-113">**Trip_data.csv** plik zawiera szczegóły podróży, takie jak liczba pasażerów, punkty odbiór i dropoff, czas trwania podróży i długość podróży.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-113">The **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="9cd3e-114">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="9cd3e-115">**Trip_fare.csv** pliku zawiera szczegółowe informacje o klasie za każdym razem, takie jak typ płatności, kwota taryfy, przeciążenia i podatków, porady i przejazd i sumy płatnej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-115">The **trip_fare.csv** file contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="9cd3e-116">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="9cd3e-117">**Unikatowy klucz** używane do przyłączania podróży\_danych i podróży\_taryfy składa się z trzech następujących pól:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-117">The **unique key** used to join trip\_data and trip\_fare is composed of the following three fields:</span></span>

* <span data-ttu-id="9cd3e-118">Medalionu,</span><span class="sxs-lookup"><span data-stu-id="9cd3e-118">medallion,</span></span>
* <span data-ttu-id="9cd3e-119">Funkcja\_licencji i</span><span class="sxs-lookup"><span data-stu-id="9cd3e-119">hack\_license and</span></span>
* <span data-ttu-id="9cd3e-120">pobranie\_daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-120">pickup\_datetime.</span></span>

## <span data-ttu-id="9cd3e-121"><a name="mltasks"></a>Adres trzy typy zadań prognozowania</span><span class="sxs-lookup"><span data-stu-id="9cd3e-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="9cd3e-122">Firma Microsoft sformułować trzy problemów prognozowania na podstawie *Porada\_kwota* ilustrujący trzy rodzaje modelowania zadań:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-122">We formulate three prediction problems based on the *tip\_amount* to illustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="9cd3e-123">**Klasyfikacji binarnej**: przewidywanie czy poradę został płatnej podróży, tj. *Porada\_kwota* większą niż $0 jest przykład dodatnią, podczas gdy *Porada\_kwota* $ 0 to przykład ujemna.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-123">**Binary classification**: To predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="9cd3e-124">**Wieloklasowej klasyfikacji**: przewidywanie zakres Porada uregulowaniu płatności podróży.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-124">**Multiclass classification**: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="9cd3e-125">Możemy podzielić *Porada\_kwota* do pięciu bins lub klasy:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="9cd3e-126">**Zadanie regresji**: przewidywanie ilość Porada płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-126">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="9cd3e-127"><a name="setup"></a>Konfigurowanie środowiska nauki danych Azure, zaawansowana analityka</span><span class="sxs-lookup"><span data-stu-id="9cd3e-127"><a name="setup"></a>Set up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="9cd3e-128">Aby skonfigurować środowisko nauki danych Azure, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-128">To set up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="9cd3e-129">**Utwórz własne konto magazynu obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="9cd3e-130">Podczas obsługi administracyjnej magazynu obiektów blob platformy Azure, wybierz lokalizację geograficzną magazynu obiektów blob platformy Azure w lub możliwie najbliżej do **południowo-środkowe stany**, czyli przechowywania danych taksówki NYC.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible to **South Central US**, which is where the NYC Taxi data is stored.</span></span> <span data-ttu-id="9cd3e-131">Dane zostaną skopiowane przy użyciu narzędzia AzCopy z publicznym kontenerze obiektów blob magazynu do kontenera na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-131">The data will be copied using AzCopy from the public blob storage container to a container in your own storage account.</span></span> <span data-ttu-id="9cd3e-132">Bliższe magazynu obiektów blob platformy Azure południowo-środkowe stany, tym szybciej będzie można ukończyć tego zadania (krok 4).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-132">The closer your Azure blob storage is to South Central US, the faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="9cd3e-133">Aby utworzyć konta magazynu Azure, wykonaj czynności podane w [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-133">To create your own Azure storage account, follow the steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="9cd3e-134">Należy pamiętać o wykonaniu uwagi dla wartości poniższych poświadczeń konta magazynu, ponieważ będą one potrzebne w dalszej części tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-134">Be sure to make notes on the values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="9cd3e-135">**Nazwa konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="9cd3e-136">**Klucz konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="9cd3e-137">**Nazwa kontenera** (które mają dane mają być przechowywane w magazynie obiektów blob Azure)</span><span class="sxs-lookup"><span data-stu-id="9cd3e-137">**Container Name** (which you want the data to be stored in the Azure blob storage)</span></span>

<span data-ttu-id="9cd3e-138">**Udostępnij wystąpienie magazynu danych SQL Azure.**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="9cd3e-139">Postępuj zgodnie z dokumentacją dostępną pod [Tworzenie usługi SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) do udostępnienia wystąpienia programu SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-139">Follow the documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) to provision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="9cd3e-140">Upewnij się, odpowiednie notacji na następujących poświadczeń magazynu danych SQL, które będą używane w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-140">Make sure that you make notations on the following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="9cd3e-141">**Nazwa serwera**: <server Name>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="9cd3e-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="9cd3e-142">**Nazwa SQLDW (baza danych)**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="9cd3e-143">**Nazwa użytkownika**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-143">**Username**</span></span>
* <span data-ttu-id="9cd3e-144">**Hasło**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-144">**Password**</span></span>

<span data-ttu-id="9cd3e-145">**Zainstaluj program Visual Studio i SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="9cd3e-146">Aby uzyskać instrukcje, zobacz [instalacji programu Visual Studio 2015 i/lub program SSDT (SQL Server Data Tools) dla usługi SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="9cd3e-147">**Połączyć się z magazynu danych Azure SQL z programem Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-147">**Connect to your Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="9cd3e-148">Aby uzyskać instrukcje, zobacz kroki 1 i 2 w [Połącz z magazynu danych SQL Azure z programem Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-148">For instructions, see steps 1 & 2 in [Connect to Azure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9cd3e-149">Uruchom następujące zapytanie SQL w bazie danych utworzonego w magazynie danych SQL (zamiast zapytania w kroku 3 w temacie connect) do **utworzyć klucz główny**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-149">Run the following SQL query on the database you created in your SQL Data Warehouse (instead of the query provided in step 3 of the connect topic,) to **create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try to create the master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If the master key exists, do nothing
    END CATCH;

<span data-ttu-id="9cd3e-150">**Tworzenie obszaru roboczego uczenia maszynowego Azure w ramach Twojej subskrypcji platformy Azure.**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="9cd3e-151">Aby uzyskać instrukcje, zobacz [Utwórz obszar roboczy usługi Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="9cd3e-152"><a name="getdata"></a>Ładowanie danych do magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="9cd3e-152"><a name="getdata"></a>Load the data into SQL Data Warehouse</span></span>
<span data-ttu-id="9cd3e-153">Otwórz konsolę polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="9cd3e-154">Uruchom program PowerShell następujące polecenia, aby pobrać przykład SQL skryptu pliki, które firma Microsoft udostępnia z Tobą w witrynie GitHub w lokalnym katalogu, który należy określić przy użyciu parametru *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-154">Run the following PowerShell commands to download the example SQL script files that we share with you on GitHub to a local directory that you specify with the parameter *-DestDir*.</span></span> <span data-ttu-id="9cd3e-155">Można zmienić wartości parametru *- DestDir* do dowolnego katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-155">You can change the value of parameter *-DestDir* to any local directory.</span></span> <span data-ttu-id="9cd3e-156">Jeśli *- DestDir* nie istnieje, zostanie on utworzony przez skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-156">If *-DestDir* does not exist, it will be created by the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="9cd3e-157">Konieczne może być **Uruchom jako Administrator** podczas wykonywania następującego skryptu programu PowerShell, jeśli Twoje *DestDir* katalogu wymaga uprawnień administratora do utworzenia lub do zapisu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-157">You might need to **Run as Administrator** when executing the following PowerShell script if your *DestDir* directory needs Administrator privilege to create or to write to it.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="9cd3e-158">Po pomyślnym wykonaniu bieżący katalog roboczy zmienia się na *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-158">After successful execution, your current working directory changes to *-DestDir*.</span></span> <span data-ttu-id="9cd3e-159">Można wyświetlić ekranu, takich jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-159">You should be able to see screen like below:</span></span>

![][19]

<span data-ttu-id="9cd3e-160">W Twojej *- DestDir*, uruchom następujący skrypt programu PowerShell w trybie administratora:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-160">In your *-DestDir*, execute the following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="9cd3e-161">Po uruchomieniu skryptu programu PowerShell po raz pierwszy, użytkownik jest proszony o podanie informacji z Twojego magazynu danych SQL Azure i konta magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-161">When the PowerShell script runs for the first time, you will be asked to input the information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="9cd3e-162">Po zakończeniu tego skryptu PowerShell uruchomiony po raz pierwszy, poświadczenia wprowadzania można będzie zapisano do pliku konfiguracyjnego SQLDW.conf istnieje katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-162">When this PowerShell script completes running for the first time, the credentials you input will have been written to a configuration file SQLDW.conf in the present working directory.</span></span> <span data-ttu-id="9cd3e-163">Przyszłych uruchamianie tego pliku skryptu programu PowerShell może odczytać wszystkich potrzebnych parametrów z tego pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-163">The future run of this PowerShell script file has the option to read all needed parameters from this configuration file.</span></span> <span data-ttu-id="9cd3e-164">Jeśli musisz zmienić niektóre parametry, można wybrać przez usunięcie tego pliku konfiguracji i wprowadzanie wartości parametrów w danych wejściowych parametrów na ekranie po wierszu lub zmiany wartości parametrów, edytując plik SQLDW.conf Twojego *- DestDir* katalogu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-164">If you need to change some parameters, you can choose to input the parameters on the screen upon prompt by deleting this configuration file and inputting the parameters values as prompted or to change the parameter values by editing the SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="9cd3e-165">Aby uniknąć konfliktów nazw schematu z tymi, które już istnieją w Twojej SQL DW Azure podczas odczytywania parametrów bezpośrednio z pliku SQLDW.conf, 3-cyfrowy numer losowe zostanie dodany do nazwy schematu z pliku SQLDW.conf jako domyślną nazwę schematu dla każdego przebiegu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-165">In order to avoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from the SQLDW.conf file, a 3-digit random number is added to the schema name from the SQLDW.conf file as the default schema name for each run.</span></span> <span data-ttu-id="9cd3e-166">Skrypt programu PowerShell może wyświetlenie monitu o nazwę schematu: należy określić nazwę w uznania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-166">The PowerShell script may prompt you for a schema name: the name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="9cd3e-167">To **skrypt programu PowerShell** plików wykonuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-167">This **PowerShell script** file completes the following tasks:</span></span>

* <span data-ttu-id="9cd3e-168">**Pobiera i instaluje narzędzie AzCopy**, jeśli nie zainstalowano narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="9cd3e-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="9cd3e-169">**Kopiuje dane na konto magazynu obiektów blob prywatnej** z publicznego obiektu blob z narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="9cd3e-169">**Copies data to your private blob storage account** from the public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob to yo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account to verify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob to your storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="9cd3e-170">**Ładuje dane przy użyciu programu Polybase (wykonując LoadDataToSQLDW.sql) do programu SQL DW Azure** z konta magazynu prywatnych obiektów blob za pomocą następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) to your Azure SQL DW** from your private blob storage account with the following commands.</span></span>
  
  * <span data-ttu-id="9cd3e-171">Tworzenie schematu</span><span class="sxs-lookup"><span data-stu-id="9cd3e-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="9cd3e-172">Tworzenie poświadczeń o zakresie bazy danych</span><span class="sxs-lookup"><span data-stu-id="9cd3e-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="9cd3e-173">Tworzenie zewnętrznego źródła danych dla obiektu blob magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="9cd3e-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="9cd3e-174">Tworzenie zewnętrznego formatu pliku dla pliku csv.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="9cd3e-175">Jest nieskompresowanych danych i pola są oddzielone znakiem kreski pionowej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-175">Data is uncompressed and fields are separated with the pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="9cd3e-176">Tworzenie zewnętrznego taryfy i tabele podróży dla zestawu danych taksówki NYC w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="9cd3e-177">Ładowanie danych z tabel zewnętrznych w magazynie obiektów blob Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9cd3e-177">Load data from external tables in Azure blob storage to SQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="9cd3e-178">Utwórz tabelę danych przykładowych (NYCTaxi_Sample) i wstawiania danych do niego z wybranie zapytania SQL w tabelach podróży i klasie.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-178">Create a sample data table (NYCTaxi_Sample) and insert data to it from selecting SQL queries on the trip and fare tables.</span></span> <span data-ttu-id="9cd3e-179">(Niektóre kroki tego przewodnika musi używać tej tabeli.)</span><span class="sxs-lookup"><span data-stu-id="9cd3e-179">(Some steps of this walkthrough needs to use this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="9cd3e-180">Lokalizacja geograficzna kont magazynu ma wpływ na czas ładowania.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-180">The geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="9cd3e-181">W zależności od lokalizacji geograficznej konto magazynu obiektów blob prywatne, proces kopiowania danych z publicznego obiektu blob na koncie magazynu prywatnego może zająć około 15 minut, a nawet dłużej, a proces ładowania danych z konta magazynu do platformy Azure Może to potrwać magazynu danych SQL 20 minut lub dłużej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-181">Depending on the geographical location of your private blob storage account, the process of copying data from a public blob to your private storage account can take about 15 minutes, or even longer,and the process of loading data from your storage account to your Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="9cd3e-182">Należy podjąć decyzję czego, jeśli masz zduplikowane pliki źródłowe i docelowe.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-182">You will have to decide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="9cd3e-183">Jeśli pliki CSV do skopiowania z magazynu publicznego obiektu blob na koncie magazynu prywatnego obiektu blob już istnieją w konto magazynu obiektów blob prywatne, AzCopy zapyta, czy chcesz je zastąpić.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-183">If the .csv files to be copied from the public blob storage to your private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want to overwrite them.</span></span> <span data-ttu-id="9cd3e-184">Jeśli nie chcesz je zastąpić, wprowadź  **n**  po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-184">If you do not want to overwrite them, input **n** when prompted.</span></span> <span data-ttu-id="9cd3e-185">Jeśli chcesz zastąpić **wszystkie** z nich, wprowadź **** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-185">If you want to overwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="9cd3e-186">Możesz również wpisać **y** indywidualnie zastąpić pliki CSV.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-186">You can also input **y** to overwrite .csv files individually.</span></span>
> 
> 

![Wykreślenia #21][21]

<span data-ttu-id="9cd3e-188">Można użyć własnych danych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-188">You can use your own data.</span></span> <span data-ttu-id="9cd3e-189">Jeśli do komputera lokalnego w aplikacji rzeczywistych danych, można nadal używać narzędzia AzCopy przekazywania danych lokalnych do magazynu obiektów blob platformy Azure prywatnych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy to upload on-premises data to your private Azure blob storage.</span></span> <span data-ttu-id="9cd3e-190">Musisz zmienić **źródła** lokalizacji, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, w poleceniu AzCopy pliku skryptu PowerShell do katalogu lokalnego, który zawiera dane.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-190">You only need to change the **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in the AzCopy command of the PowerShell script file to the local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="9cd3e-191">Jeśli danych jest już w magazynie obiektów blob platformy Azure prywatnych w rzeczywistych aplikacji, można pominąć krok AzCopy w skrypcie programu PowerShell i bezpośrednio przekazać dane do magazynu danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-191">If your data is already in your private Azure blob storage in your real life application, you can skip the AzCopy step in the PowerShell script and directly upload the data to Azure SQL DW.</span></span> <span data-ttu-id="9cd3e-192">Wymaga to dodatkowe zmiany skryptu, aby dopasować ją do formatu danych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-192">This will require additional edits of the script to tailor it to the format of your data.</span></span>
> 
> 

<span data-ttu-id="9cd3e-193">Ten skrypt programu Powershell również podłącza się w informacjach dotyczących magazynu danych SQL Azure do plików przykład Eksploracja danych SQLDW_Explorations.sql, SQLDW_Explorations.ipynb i SQLDW_Explorations_Scripts.py tak, aby te trzy pliki są gotowe do próby natychmiast po Wykonuje skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-193">This Powershell script also plugs in the Azure SQL DW information into the data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready to be tried out instantly after the PowerShell script completes.</span></span>

<span data-ttu-id="9cd3e-194">Po pomyślnym wykonaniu, zostanie wyświetlony ekran, takich jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="9cd3e-195"><a name="dbexplore"></a>Eksploracja danych i funkcji inżynieryjne w usłudze Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9cd3e-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="9cd3e-196">W tej sekcji możemy wykonywać Generowanie funkcji i eksploracja danych przez wykonywanie zapytań SQL magazynu danych SQL Azure bezpośrednio przy użyciu **programu Visual Studio Tools danych**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="9cd3e-197">Wszystkie zapytania SQL w tej sekcji znajdują się w przykładowy skrypt o nazwie *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-197">All SQL queries used in this section can be found in the sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="9cd3e-198">Ten plik została już pobrana do katalogu lokalnego za pomocą skryptu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-198">This file has already been downloaded to your local directory by the PowerShell script.</span></span> <span data-ttu-id="9cd3e-199">Można również pobrać go z [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="9cd3e-200">Ale plik w witrynie GitHub nie ma informacji magazynu danych SQL Azure z sieci.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-200">But the file in GitHub does not have the Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="9cd3e-201">Nawiązywanie połączenia z magazynu danych SQL Azure za pomocą programu Visual Studio przy użyciu magazynu danych SQL, nazwa logowania i hasła i otwarcie **Eksplorator obiektów SQL** o potwierdzenie bazy danych i tabele zostały zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-201">Connect to your Azure SQL DW using Visual Studio with the SQL DW login name and password and open up the **SQL Object Explorer** to confirm the database and tables have been imported.</span></span> <span data-ttu-id="9cd3e-202">Pobrać *SQLDW_Explorations.sql* pliku.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-202">Retrieve the *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="9cd3e-203">Aby otworzyć Edytor zapytań równoległych magazynu danych (PDW), użyj **nowe zapytanie** polecenia, a Twoje PDW wybrano w **Eksplorator obiektów SQL**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-203">To open a Parallel Data Warehouse (PDW) query editor, use the **New Query** command while your PDW is selected in the **SQL Object Explorer**.</span></span> <span data-ttu-id="9cd3e-204">Standardowy Edytor zapytań SQL nie jest obsługiwany przez PDW.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-204">The standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="9cd3e-205">Poniżej przedstawiono dane tego typu funkcji i eksploracja generowania wykonywane w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-205">Here are the type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="9cd3e-206">Eksplorowanie danych dystrybucji kilka pól w różnym czasie systemu windows.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="9cd3e-207">Zbadaj jakości danych pól długości i szerokości geograficznej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="9cd3e-208">Generowanie na podstawie etykiet klasyfikacji binarnej i wieloklasowej **Porada\_kwota**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="9cd3e-209">Generowanie funkcji i obliczeń lub porównania odległości podróży.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="9cd3e-210">Dołącz do dwóch tabel i wyodrębniać losowej próbki, która będzie służyć do tworzenia modeli.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="9cd3e-211">Weryfikacja importu danych</span><span class="sxs-lookup"><span data-stu-id="9cd3e-211">Data import verification</span></span>
<span data-ttu-id="9cd3e-212">Kwerendy te zapewniają szybki weryfikacji liczby wierszy i kolumn w tabelach wypełniać wcześniej przy użyciu zbiorczego równoległe w programie Polybase zaimportować,</span><span class="sxs-lookup"><span data-stu-id="9cd3e-212">These queries provide a quick verification of the number of rows and columns in the tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="9cd3e-213">**Dane wyjściowe:** należy pobrać 173,179,759 wierszy i kolumn 14.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="9cd3e-214">Eksploracja: Podróży dystrybucji przez Medalionu</span><span class="sxs-lookup"><span data-stu-id="9cd3e-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="9cd3e-215">To przykładowe zapytanie identyfikuje medallions (taksówki numery) wykonanych więcej niż 100 rund w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-215">This example query identifies the medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="9cd3e-216">Zapytanie będzie korzystać z dostępu do tabeli partycjonowanej ponieważ należy przygotować w schemacie partycji **podnoszenia\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-216">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="9cd3e-217">Wykonywanie zapytania pełnego zestawu danych umożliwiają użycie tabeli partycjonowanej i/lub indeksu skanowania.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-217">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="9cd3e-218">**Dane wyjściowe:** zapytania powinien zwrócić tabelę z wierszami 13,369 medallions (taksówkach) i Liczba podróży zakończone przez nich 2013.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-218">**Output:** The query should return a table with rows specifying the 13,369 medallions (taxis) and the number of trip completed by them in 2013.</span></span> <span data-ttu-id="9cd3e-219">Ostatnia kolumna zawiera Liczba rund ukończone.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-219">The last column contains the count of the number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="9cd3e-220">Eksploracja: Podróży dystrybucji Medalionu i hack_license</span><span class="sxs-lookup"><span data-stu-id="9cd3e-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="9cd3e-221">W tym przykładzie identyfikuje medallions (taksówki cyfry) i hack_license cyfry (sterowniki) zakończona ponad 100 rund w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-221">This example identifies the medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="9cd3e-222">**Dane wyjściowe:** zapytanie powinna zwrócić tabelę z wierszami 13,369 określenie 13,369 identyfikatory samochodu/driver, które zostały ukończone więcej czy 100 podróży w 2013.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-222">**Output:** The query should return a table with 13,369 rows specifying the 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="9cd3e-223">Ostatnia kolumna zawiera Liczba rund ukończone.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-223">The last column contains the count of the number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="9cd3e-224">Ocena jakości danych: Weryfikuj rekordy z geograficzne niepoprawne i/lub szerokość geograficzną</span><span class="sxs-lookup"><span data-stu-id="9cd3e-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="9cd3e-225">W tym przykładzie sprawdza, czy polach geograficzne i/lub szerokość geograficzną albo zawiera nieprawidłową wartość (stopni w radianach powinna należeć do zakresu od-90 do 90,) lub (0, 0) współrzędnych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-225">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="9cd3e-226">**Dane wyjściowe:** zapytanie zwraca 837,467 podróży, które mają nieprawidłowe pola geograficzne i/lub szerokość geograficzną.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-226">**Output:** The query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="9cd3e-227">Eksploracja: Przechylony a nie Przechylony rund dystrybucji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="9cd3e-228">W tym przykładzie znajduje się liczba podróży, które zostały Przechylony a liczba, które nie zostały Przechylony w określonym przedziale czasu (lub pełnego zestawu danych, jeśli obejmujące pełny rok, ponieważ jest skonfigurowana w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-228">This example finds the number of trips that were tipped vs. the number that were not tipped in a specified time period (or in the full dataset if covering the full year as it is set up here).</span></span> <span data-ttu-id="9cd3e-229">Tej dystrybucji odzwierciedla dystrybucji binarne etykiety później służący do modelowania klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-229">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="9cd3e-230">**Dane wyjściowe:** zapytanie powinna zwrócić następujące częstotliwości Porada roku 2013: 90,447,622 Przechylony i 82,264,709 Przechylony nie.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-230">**Output:** The query should return the following tip frequencies for the year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="9cd3e-231">Eksploracja: Porada klasy/zakres dystrybucji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="9cd3e-232">W tym przykładzie oblicza rozkład Porada zakresów w danym przedziale czasu (lub pełnego zestawu danych, jeśli obejmujące pełny rok).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-232">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="9cd3e-233">Jest to dystrybucji klasy etykiety, które zostanie później użyty do modelowania wieloklasowej klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-233">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="9cd3e-234">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="9cd3e-234">**Output:**</span></span>

| <span data-ttu-id="9cd3e-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="9cd3e-235">tip_class</span></span> | <span data-ttu-id="9cd3e-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="9cd3e-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="9cd3e-237">1</span><span class="sxs-lookup"><span data-stu-id="9cd3e-237">1</span></span> |<span data-ttu-id="9cd3e-238">82230915</span><span class="sxs-lookup"><span data-stu-id="9cd3e-238">82230915</span></span> |
| <span data-ttu-id="9cd3e-239">2</span><span class="sxs-lookup"><span data-stu-id="9cd3e-239">2</span></span> |<span data-ttu-id="9cd3e-240">6198803</span><span class="sxs-lookup"><span data-stu-id="9cd3e-240">6198803</span></span> |
| <span data-ttu-id="9cd3e-241">3</span><span class="sxs-lookup"><span data-stu-id="9cd3e-241">3</span></span> |<span data-ttu-id="9cd3e-242">1932223</span><span class="sxs-lookup"><span data-stu-id="9cd3e-242">1932223</span></span> |
| <span data-ttu-id="9cd3e-243">0</span><span class="sxs-lookup"><span data-stu-id="9cd3e-243">0</span></span> |<span data-ttu-id="9cd3e-244">82264625</span><span class="sxs-lookup"><span data-stu-id="9cd3e-244">82264625</span></span> |
| <span data-ttu-id="9cd3e-245">4</span><span class="sxs-lookup"><span data-stu-id="9cd3e-245">4</span></span> |<span data-ttu-id="9cd3e-246">85765</span><span class="sxs-lookup"><span data-stu-id="9cd3e-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="9cd3e-247">Eksploracja: Obliczania i porównać odległość podróży</span><span class="sxs-lookup"><span data-stu-id="9cd3e-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="9cd3e-248">W tym przykładzie konwertuje długość odbiór i przyjmowania i szerokości geograficznej lokalizacji SQL punkty, oblicza odległość podróży przy użyciu różnicę punktów geograficzne SQL i zwraca losowej próbki wyniki do porównania.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-248">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="9cd3e-249">Przykład ogranicza wyniki do prawidłowe współrzędne tylko przy użyciu zapytania oceny jakości danych objętych wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-249">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function to calculate the direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="9cd3e-250">Funkcja engineering przy użyciu funkcji SQL</span><span class="sxs-lookup"><span data-stu-id="9cd3e-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="9cd3e-251">Czasami funkcje SQL mogą być wydajne opcję engineering funkcji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="9cd3e-252">W tym przewodniku zdefiniowanego funkcji SQL, aby obliczyć bezpośredniego odległość między lokalizacjami odbiór i dropoff.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-252">In this walkthrough, we defined a SQL function to calculate the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="9cd3e-253">Można uruchomić następujące skrypty SQL w **programu Visual Studio Tools danych**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-253">You can run the following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="9cd3e-254">Poniżej przedstawiono skrypt SQL, który definiuje funkcję odległości.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-254">Here is the SQL script that defines the distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate the direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="9cd3e-255">Oto przykład, aby wywołać tę funkcję, aby wygenerować funkcji w zapytaniu SQL:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-255">Here is an example to call this function to generate features in your SQL query:</span></span>

    -- Sample query to call the function to create features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="9cd3e-256">**Dane wyjściowe:** to zapytanie generuje tabeli (z 2,803,538 wierszy) z odbiór i dropoff długości i szerokości geograficzne i odpowiadający mu bezpośrednie odległości w milach.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and the corresponding direct distances in miles.</span></span> <span data-ttu-id="9cd3e-257">Poniżej przedstawiono wyniki dla pierwsze 3 wiersze:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-257">Here are the results for first 3 rows:</span></span>

|  | <span data-ttu-id="9cd3e-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="9cd3e-258">pickup_latitude</span></span> | <span data-ttu-id="9cd3e-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="9cd3e-259">pickup_longitude</span></span> | <span data-ttu-id="9cd3e-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="9cd3e-260">dropoff_latitude</span></span> | <span data-ttu-id="9cd3e-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="9cd3e-261">dropoff_longitude</span></span> | <span data-ttu-id="9cd3e-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="9cd3e-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="9cd3e-263">1</span><span class="sxs-lookup"><span data-stu-id="9cd3e-263">1</span></span> |<span data-ttu-id="9cd3e-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="9cd3e-264">40.731804</span></span> |<span data-ttu-id="9cd3e-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="9cd3e-265">-74.001083</span></span> |<span data-ttu-id="9cd3e-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="9cd3e-266">40.736622</span></span> |<span data-ttu-id="9cd3e-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="9cd3e-267">-73.988953</span></span> |<span data-ttu-id="9cd3e-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="9cd3e-268">.7169601222</span></span> |
| <span data-ttu-id="9cd3e-269">2</span><span class="sxs-lookup"><span data-stu-id="9cd3e-269">2</span></span> |<span data-ttu-id="9cd3e-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="9cd3e-270">40.715794</span></span> |<span data-ttu-id="9cd3e-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="9cd3e-271">-74,010635</span></span> |<span data-ttu-id="9cd3e-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="9cd3e-272">40.725338</span></span> |<span data-ttu-id="9cd3e-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="9cd3e-273">-74.00399</span></span> |<span data-ttu-id="9cd3e-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="9cd3e-274">.7448343721</span></span> |
| <span data-ttu-id="9cd3e-275">3</span><span class="sxs-lookup"><span data-stu-id="9cd3e-275">3</span></span> |<span data-ttu-id="9cd3e-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="9cd3e-276">40.761456</span></span> |<span data-ttu-id="9cd3e-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="9cd3e-277">-73.999886</span></span> |<span data-ttu-id="9cd3e-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="9cd3e-278">40.766544</span></span> |<span data-ttu-id="9cd3e-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="9cd3e-279">-73.988228</span></span> |<span data-ttu-id="9cd3e-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="9cd3e-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="9cd3e-281">Przygotowanie do tworzenia modelu danych</span><span class="sxs-lookup"><span data-stu-id="9cd3e-281">Prepare data for model building</span></span>
<span data-ttu-id="9cd3e-282">Następujące zapytanie sprzęga **nyctaxi\_podróży** i **nyctaxi\_taryfy** tabel, generuje etykiety klasyfikacji binarnej **Przechylony**, etykiety klasyfikacji wielu klasy **Porada\_klasy**i wyodrębnia próbki z dołączonym do pełnego zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-282">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from the full joined dataset.</span></span> <span data-ttu-id="9cd3e-283">Próbki odbywa się przez pobranie podzbiór rund na podstawie czasu odbioru.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-283">The sampling is done by retrieving a subset of the trips based on pickup time.</span></span>  <span data-ttu-id="9cd3e-284">To zapytanie może skopiować następnie wkleić bezpośrednio w [Azure Machine Learning Studio](https://studio.azureml.net) [i zaimportuj dane] [ import-data] modułu dla wprowadzanie danych bezpośrednio z wystąpienia bazy danych SQL w Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-284">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL database instance in Azure.</span></span> <span data-ttu-id="9cd3e-285">Zapytanie nie obejmuje rekordy z niepoprawne (0, 0) współrzędnych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-285">The query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="9cd3e-286">Gdy wszystko będzie gotowe przejść do usługi Azure Machine Learning, użytkownik może:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-286">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="9cd3e-287">Zapisz końcowego zapytanie SQL do wyodrębnienia przykładowe dane i skopiuj i Wklej zapytanie bezpośrednio do [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning, lub</span><span class="sxs-lookup"><span data-stu-id="9cd3e-287">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="9cd3e-288">Zachować dane próbki i odtworzone będą używane dla modelu tworzenie w nowej tabeli magazynu danych SQL i użyj nowej tabeli w [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-288">Persist the sampled and engineered data you plan to use for model building in a new SQL DW table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="9cd3e-289">Skrypt programu PowerShell w poprzednim kroku ma zostało to zrobione automatycznie.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-289">The PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="9cd3e-290">Możesz przeczytać bezpośrednio z tej tabeli w module importu danych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-290">You can read directly from this table in the Import Data module.</span></span>

## <span data-ttu-id="9cd3e-291"><a name="ipnb"></a>Eksploracja danych i funkcji inżynieryjne w notesie IPython</span><span class="sxs-lookup"><span data-stu-id="9cd3e-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="9cd3e-292">W tej sekcji zostaną wykonane Eksplorowanie danych oraz generowanie funkcji za pomocą obu Python i zapytań SQL magazynu danych SQL utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL DW created earlier.</span></span> <span data-ttu-id="9cd3e-293">Przykładowe IPython Notes o nazwie **SQLDW_Explorations.ipynb** plik skryptu języka Python **SQLDW_Explorations_Scripts.py** zostały pobrane do lokalnego katalogu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded to your local directory.</span></span> <span data-ttu-id="9cd3e-294">Są również dostępne na [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="9cd3e-295">Te dwa pliki są identyczne w skryptach Python.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="9cd3e-296">Plik skryptu języka Python są dostępne w przypadku, gdy nie masz serwera IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-296">The Python script file is provided to you in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="9cd3e-297">Te dwa przykładowe Python plików zostały zaprojektowane pod **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="9cd3e-298">Potrzebnych informacji magazynu danych SQL Azure w próbce notesu IPython i plik skryptu języka Python pobrane na komputer lokalny został podłączony za pomocą skryptu programu PowerShell wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-298">The needed Azure SQL DW information in the sample IPython Notebook and the Python script file downloaded to your local machine has been plugged in by the PowerShell script previously.</span></span> <span data-ttu-id="9cd3e-299">Są one wykonywalny bez żadnych modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-299">They are executable without any modification.</span></span>

<span data-ttu-id="9cd3e-300">Jeśli obszar roboczy uczenie maszynowe Azure zostały już skonfigurowane, możesz bezpośrednio przekazać przykładowe notesu IPython do usługi uczenie maszynowe Azure IPython notesu i jej uruchamianie.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-300">If you have already set up an AzureML workspace, you can directly upload the sample IPython Notebook to the AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="9cd3e-301">Poniżej przedstawiono kroki, aby przekazać do usługi uczenie maszynowe Azure IPython notesu:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-301">Here are the steps to upload to AzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="9cd3e-302">Zaloguj się do swojego obszaru roboczego uczenie maszynowe Azure, kliknij przycisk "Studio" u góry, a następnie kliknij przycisk "Komputery przenośne", po lewej stronie strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-302">Log in to your AzureML workspace, click "Studio" at the top, and click "NOTEBOOKS" on the left side of the web page.</span></span>
   
    ![Wykreślenia #22][22]
2. <span data-ttu-id="9cd3e-304">Kliknij przycisk "Nowy" w lewym dolnym rogu strony sieci web, a następnie wybierz pozycję "Python 2".</span><span class="sxs-lookup"><span data-stu-id="9cd3e-304">Click "NEW" on the left bottom corner of the web page, and select "Python 2".</span></span> <span data-ttu-id="9cd3e-305">Następnie podaj nazwę z notesem i kliknij znacznik wyboru, aby utworzyć nowy notes IPython puste.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-305">Then, provide a name to the notebook and click the check mark to create the new blank IPython Notebook.</span></span>
   
    ![Wykreślenia #23][23]
3. <span data-ttu-id="9cd3e-307">Kliknij symbol "Jupyter" w lewym górnym rogu nowy notes IPython.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-307">Click the "Jupyter" symbol on the left top corner of the new IPython Notebook.</span></span>
   
    ![Wykreślenia #24][24]
4. <span data-ttu-id="9cd3e-309">Przeciągnij i upuść próbki notesu IPython do **drzewa** z usługi uczenie maszynowe Azure IPython notesu, a następnie kliknij przycisk **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-309">Drag and drop the sample IPython Notebook to the **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="9cd3e-310">Następnie próbki IPython notesu zostanie przekazany do usługi uczenie maszynowe Azure IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-310">Then, the sample IPython Notebook will be uploaded to the AzureML IPython Notebook service.</span></span>
   
    ![Wykreślenia #25][25]

<span data-ttu-id="9cd3e-312">Aby można było uruchomić przykładowy plik, Python następujące pakiety są wymagane skryptu notesu IPython lub Python.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-312">In order to run the sample IPython Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="9cd3e-313">Jeśli używasz usługi uczenie maszynowe Azure IPython notesu te pakiety zostały wstępnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-313">If you are using the AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="9cd3e-314">pandas</span><span class="sxs-lookup"><span data-stu-id="9cd3e-314">pandas</span></span>
    - <span data-ttu-id="9cd3e-315">numpy</span><span class="sxs-lookup"><span data-stu-id="9cd3e-315">numpy</span></span>
    - <span data-ttu-id="9cd3e-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="9cd3e-316">matplotlib</span></span>
    - <span data-ttu-id="9cd3e-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="9cd3e-317">pyodbc</span></span>
    - <span data-ttu-id="9cd3e-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="9cd3e-318">PyTables</span></span>

<span data-ttu-id="9cd3e-319">Zalecana kolejność podczas tworzenia zaawansowanych rozwiązań analitycznych na uczenie maszynowe Azure z dużej ilości danych jest następujący:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-319">The recommended sequence when building advanced analytical solutions on AzureML with large data is the following:</span></span>

* <span data-ttu-id="9cd3e-320">Odczyt w małych przykładowych danych do ramki danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-320">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="9cd3e-321">Wykonywanie niektórych wizualizacje i eksploracji przy użyciu próbki danych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-321">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="9cd3e-322">Wypróbuj engineering funkcji przy użyciu próbki danych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-322">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="9cd3e-323">Dla większych Eksploracja danych, do manipulowania danymi i inżynieria funkcji należy użyć Python do wysyłania zapytań SQL bezpośrednio z magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-323">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL DW.</span></span>
* <span data-ttu-id="9cd3e-324">Określ wielkość próbki się odpowiednie do konstruowania modelu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-324">Decide the sample size to be suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="9cd3e-325">Następujących typów to kilka Eksploracja danych, wizualizacji danych i funkcji inżynierii przykłady.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-325">The followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="9cd3e-326">Więcej eksploracji danych można znaleźć w przykładzie notesu IPython oraz przykładowy plik skryptu języka Python.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-326">More data explorations can be found in the sample IPython Notebook and the sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="9cd3e-327">Inicjowanie poświadczenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="9cd3e-327">Initialize database credentials</span></span>
<span data-ttu-id="9cd3e-328">Inicjowanie ustawienia połączenia bazy danych w następujących zmiennych:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-328">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="9cd3e-329">Utwórz połączenie z bazą danych</span><span class="sxs-lookup"><span data-stu-id="9cd3e-329">Create database connection</span></span>
<span data-ttu-id="9cd3e-330">Oto parametry połączenia, które tworzy połączenie z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-330">Here is the connection string that creates the connection to the database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="9cd3e-331">Raport liczba wierszy i kolumn w tabeli < nyctaxi_trip ></span><span class="sxs-lookup"><span data-stu-id="9cd3e-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="9cd3e-332">Całkowita liczba wierszy = 173179759</span><span class="sxs-lookup"><span data-stu-id="9cd3e-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="9cd3e-333">Łączna liczba kolumn = 14</span><span class="sxs-lookup"><span data-stu-id="9cd3e-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="9cd3e-334">Raport liczba wierszy i kolumn w tabeli < nyctaxi_fare ></span><span class="sxs-lookup"><span data-stu-id="9cd3e-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="9cd3e-335">Całkowita liczba wierszy = 173179759</span><span class="sxs-lookup"><span data-stu-id="9cd3e-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="9cd3e-336">Łączna liczba kolumn = 11</span><span class="sxs-lookup"><span data-stu-id="9cd3e-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-the-sql-data-warehouse-database"></a><span data-ttu-id="9cd3e-337">Odczyt w przykładowych małych danych z bazy danych magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="9cd3e-337">Read-in a small data sample from the SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="9cd3e-338">Czas odczytu Przykładowa tabela jest 14.096495 sekund.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-338">Time to read the sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="9cd3e-339">Liczba wierszy i kolumn pobrać = (1000, 21).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="9cd3e-340">Statystyki opisowe</span><span class="sxs-lookup"><span data-stu-id="9cd3e-340">Descriptive statistics</span></span>
<span data-ttu-id="9cd3e-341">Teraz można przystąpić do eksplorowania próbki danych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-341">Now you are ready to explore the sampled data.</span></span> <span data-ttu-id="9cd3e-342">Możemy zaczynać się patrzeć statystykami opisowy dla **podróży\_odległość** (lub innych pól samodzielnie określić).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-342">We start with looking at some descriptive statistics for the **trip\_distance** (or any other fields you choose to specify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="9cd3e-343">Wizualizacji: Przykład kreślenia pola</span><span class="sxs-lookup"><span data-stu-id="9cd3e-343">Visualization: Box plot example</span></span>
<span data-ttu-id="9cd3e-344">Następnie przyjrzymy się skrzynkowy odległość podróży do wizualizacji quantiles.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-344">Next we look at the box plot for the trip distance to visualize the quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Wykreślenia #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="9cd3e-346">Wizualizacji: Przykład kreślenia dystrybucji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="9cd3e-347">Wykresy, które wizualizacji dystrybucji i histogram odległości próbkowanych podróży.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-347">Plots that visualize the distribution and a histogram for the sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Wykreślenia #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="9cd3e-349">Wizualizacja: Pasek i geograficzne wiersza</span><span class="sxs-lookup"><span data-stu-id="9cd3e-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="9cd3e-350">W tym przykładzie mamy bin odległość podróży, w pojemnikach pięć i wizualizacja wyników binning.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-350">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="9cd3e-351">Firma Microsoft wykreślenia powyżej dystrybucji bin na pasku lub wiersz kreślenia z:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-351">We can plot the above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Wykreślenia #3][3]

<span data-ttu-id="9cd3e-353">i</span><span class="sxs-lookup"><span data-stu-id="9cd3e-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Wykreślenia #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="9cd3e-355">Wizualizacji: Przykłady Scatterplot</span><span class="sxs-lookup"><span data-stu-id="9cd3e-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="9cd3e-356">Zostanie przedstawiony jest wykres punktowy między **podróży\_czasu\_w\_s** i **podróży\_odległość** się czy ma żadnych korelacji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Wykreślenia #6][6]

<span data-ttu-id="9cd3e-358">Podobnie można sprawdzić relacji między **szybkość\_kod** i **podróży\_odległość**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-358">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Wykreślenia #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="9cd3e-360">Eksploracja danych na próbki danych za pomocą zapytań SQL w notesie IPython</span><span class="sxs-lookup"><span data-stu-id="9cd3e-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="9cd3e-361">W tej sekcji możemy Eksplorowanie danych dystrybucji przy użyciu próbki danych, który jest utrwalona w nowej tabeli utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-361">In this section, we explore data distributions using the sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="9cd3e-362">Należy pamiętać, że podobne eksploracji może zostać wykonane przy użyciu oryginalnego tabel.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-362">Note that similar explorations can be performed using the original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-the-sampled-table"></a><span data-ttu-id="9cd3e-363">Eksploracja: Raport liczba wierszy i kolumn w tabeli próbki</span><span class="sxs-lookup"><span data-stu-id="9cd3e-363">Exploration: Report number of rows and columns in the sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="9cd3e-364">Eksploracja: Przechylony nie zwracać dystrybucji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="9cd3e-365">Eksploracja: Porada klasy dystrybucji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-the-tip-distribution-by-class"></a><span data-ttu-id="9cd3e-366">Eksploracja: Wykreślenia dystrybucji Porada przez klasę</span><span class="sxs-lookup"><span data-stu-id="9cd3e-366">Exploration: Plot the tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![#26 kreślenia][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="9cd3e-368">Eksploracji: Codzienne dystrybucji rund</span><span class="sxs-lookup"><span data-stu-id="9cd3e-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="9cd3e-369">Eksploracja: Podróży dystrybucji na Medalionu</span><span class="sxs-lookup"><span data-stu-id="9cd3e-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="9cd3e-370">Eksploracja: Podróży dystrybucji przez Medalionu i hack licencji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="9cd3e-371">Eksploracja: Podróży czasu dystrybucji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="9cd3e-372">Eksploracja: Podróży odległość dystrybucji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="9cd3e-373">Eksploracji: Dystrybucja typ płatności</span><span class="sxs-lookup"><span data-stu-id="9cd3e-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="9cd3e-374">Sprawdź ostatecznej formie tabeli featurized</span><span class="sxs-lookup"><span data-stu-id="9cd3e-374">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="9cd3e-375"><a name="mlmodel"></a>Tworzenie modeli w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9cd3e-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="9cd3e-376">Firma Microsoft są teraz gotowe do przejścia do konstruowania modelu i wdrażania modelu w [usługi Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-376">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="9cd3e-377">Dane są gotowe do użycia w jednym z problemów prognozowania wymienionych wcześniej, to znaczy:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-377">The data is ready to be used in any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="9cd3e-378">**Klasyfikacji binarnej**: przewidywanie, czy etykietki został płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-378">**Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="9cd3e-379">**Wieloklasowej klasyfikacji**: przewidywanie zakres Porada płatną zgodnie z uprzednio zdefiniowanej klasy.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-379">**Multiclass classification**: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="9cd3e-380">**Zadanie regresji**: przewidywanie ilość Porada płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-380">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

<span data-ttu-id="9cd3e-381">Aby rozpocząć wykonywania modelowania, zaloguj się do Twojego **usługi Azure Machine Learning** obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-381">To begin the modeling exercise, log in to your **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="9cd3e-382">Jeśli jeszcze nie utworzono obszaru roboczego uczenia maszynowego, zobacz [Utwórz obszar roboczy usługi Azure ML](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="9cd3e-383">Aby zacząć korzystać z usługi Azure Machine Learning, zobacz [co to jest Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="9cd3e-383">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="9cd3e-384">Zaloguj się do [Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-384">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="9cd3e-385">Strona główna Studio zapewnia wiele informacji, wideo, samouczki, linki do odwołania moduły i innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-385">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="9cd3e-386">Aby uzyskać więcej informacji na temat usługi Azure Machine Learning, zapoznaj się [Centrum dokumentacji uczenia maszynowego Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-386">For more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="9cd3e-387">Eksperyment typowe szkolenia składa się z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-387">A typical training experiment consists of the following steps:</span></span>

1. <span data-ttu-id="9cd3e-388">Utwórz **+ nowy** eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="9cd3e-389">Pobierz dane do uczenia Maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-389">Get the data into Azure ML.</span></span>
3. <span data-ttu-id="9cd3e-390">Wstępnie przetworzyć, transformacji i manipulowanie danymi w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-390">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="9cd3e-391">Generowanie funkcji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-391">Generate features as needed.</span></span>
5. <span data-ttu-id="9cd3e-392">Podział danych na zestaw szkolenia / / sprawdzanie poprawności danych (lub mieć osobne zestawy danych dla każdego).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-392">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="9cd3e-393">Wybierz co najmniej jeden algorytmów uczenia maszynowego w zależności od problemu learning do rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-393">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="9cd3e-394">Przykład klasyfikacji binarnej, wieloklasowej klasyfikacji, regresji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="9cd3e-395">Szkolenie co najmniej jednego modelu przy użyciu zestawu danych szkoleniowych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-395">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="9cd3e-396">Wynik sprawdzania poprawności zestawu danych przy użyciu modeli przeszkolone.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-396">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="9cd3e-397">Należy ocenić modele obliczeniowe odpowiednich metryki learning problem.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-397">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="9cd3e-398">Prawidłowo dostrojenie modele i wybrać najlepsze modelu do wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-398">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="9cd3e-399">W tym ćwiczeniu firma Microsoft ma już przedstawione odtwarzane danych w usłudze SQL Data Warehouse i postanowiła na rozmiar próbki pozyskiwania w uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-399">In this exercise, we have already explored and engineered the data in SQL Data Warehouse, and decided on the sample size to ingest in Azure ML.</span></span> <span data-ttu-id="9cd3e-400">Poniżej przedstawiono procedurę, aby utworzyć co najmniej jeden modele predykcyjne:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-400">Here is the procedure to build one or more of the prediction models:</span></span>

1. <span data-ttu-id="9cd3e-401">Pobieranie danych do usługi Azure ML przy użyciu [i zaimportuj dane] [ import-data] modułu dostępne w **danych wejściowych i wyjściowych** sekcji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-401">Get the data into Azure ML using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="9cd3e-402">Aby uzyskać więcej informacji, zobacz [i zaimportuj dane] [ import-data] strony odwołanie do modułu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-402">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Uczenie Maszynowe Azure i zaimportuj dane][17]
2. <span data-ttu-id="9cd3e-404">Wybierz **bazy danych SQL Azure** jako **źródła danych** w **właściwości** panelu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-404">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="9cd3e-405">Wprowadź nazwę DNS bazy danych w **nazwę serwera bazy danych** pola.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-405">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="9cd3e-406">Format:`tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="9cd3e-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="9cd3e-407">Wprowadź **Nazwa bazy danych** w odpowiednie pole.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-407">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="9cd3e-408">Wprowadź *nazwa użytkownika SQL* w **nazwę konta użytkownika serwera**i *hasło* w **hasło konta użytkownika serwera**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-408">Enter the *SQL user name* in the **Server user account name**, and the *password* in the **Server user account password**.</span></span>
6. <span data-ttu-id="9cd3e-409">Sprawdź **dowolny certyfikat serwera Zaakceptuj** opcji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-409">Check the **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="9cd3e-410">W **zapytanie bazy danych** edytowania obszaru tekstu, Wklej zapytanie, które zwraca pola niezbędne bazy danych (w tym wszystkie pola obliczanej, takich jak etykiety) i w dół próbek danych do żądanego próbkowania.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-410">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="9cd3e-411">Przykład eksperyment klasyfikacji binarnej odczytywanie danych bezpośrednio z bazy danych usługi SQL Data Warehouse to na poniższej ilustracji (Pamiętaj zastąpić nyctaxi_trip nazwy tabeli i nyctaxi_fare przez nazwę schematu i nazwy tabeli używana w Twojej wskazówki).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-411">An example of a binary classification experiment reading data directly from the SQL Data Warehouse database is in the figure below (remember to replace the table names nyctaxi_trip and nyctaxi_fare by the schema name and the table names you used in your walkthrough).</span></span> <span data-ttu-id="9cd3e-412">Podobne eksperymenty można utworzyć dla wieloklasowej klasyfikacji i regresji problemów.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure ML pociągu][10]

> [!IMPORTANT]
> <span data-ttu-id="9cd3e-414">W danych modelowania wyodrębniania i pobierania próbek przykłady zapytania podane w poprzednich sekcjach, **wszystkich etykiet trzy ćwiczeń modelowania są uwzględnione w zapytaniu**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-414">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="9cd3e-415">Ważnym krokiem (wymagane) w każdym ćwiczeń modelowania jest **wykluczyć** niepotrzebne etykiety dla innych problemów oraz wszelkie inne **target przecieki**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-415">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="9cd3e-416">Na przykład, korzystając z klasyfikacji binarnej, użyj etykiety **Przechylony** i wykluczyć pola **Porada\_klasy**, **Porada\_kwota**i **całkowita\_kwota**.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-416">For example, when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="9cd3e-417">Są one przecieki docelowy one zakłada poradę płatnej.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-417">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="9cd3e-418">Aby wykluczyć wszystkie zbędne kolumny lub docelowe przecieki, możesz użyć [Select Columns in Dataset] [ select-columns] modułu lub [edytowanie metadanych][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="9cd3e-418">To exclude any unnecessary columns or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="9cd3e-419">Aby uzyskać więcej informacji, zobacz [Select Columns in Dataset] [ select-columns] i [edytowanie metadanych] [ edit-metadata] odwołania stron.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="9cd3e-420"><a name="mldeploy"></a>Wdrażanie modeli w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9cd3e-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="9cd3e-421">Gdy model jest gotowy, łatwo można go wdrożyć jako usługę sieci web bezpośrednio z eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-421">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="9cd3e-422">Aby uzyskać więcej informacji na temat wdrażania usług sieci web uczenie Maszynowe Azure, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="9cd3e-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="9cd3e-423">Aby wdrożyć nową usługę sieci web, musisz:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-423">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="9cd3e-424">Tworzenie eksperymentu oceniania.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="9cd3e-425">Wdrażanie usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-425">Deploy the web service.</span></span>

<span data-ttu-id="9cd3e-426">Aby utworzyć eksperyment oceniania z **zakończone** szkolenia eksperyment, kliknij przycisk **utworzyć OCENIANIA EKSPERYMENTU** na dolnym pasku akcji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-426">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Ocenianie przez usługę Azure][18]

<span data-ttu-id="9cd3e-428">Usługa Azure Machine Learning podejmie próbę utworzenia eksperyment oceniania na podstawie składników eksperyment uczenia.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-428">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="9cd3e-429">W szczególności będzie:</span><span class="sxs-lookup"><span data-stu-id="9cd3e-429">In particular, it will:</span></span>

1. <span data-ttu-id="9cd3e-430">Zapisania trenowanego modelu oraz usuwanie modułów uczenia modelu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-430">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="9cd3e-431">Zidentyfikuj logicznych **port wejściowy** do reprezentowania schematu oczekiwanych danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-431">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="9cd3e-432">Zidentyfikuj logicznych **output portu** do reprezentowania schemat danych wyjściowych usługi sieci web oczekiwanego.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-432">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="9cd3e-433">Podczas tworzenia eksperymentu oceniania, zapoznaj się z nim i upewnij się, Dopasuj zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-433">When the scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="9cd3e-434">Typowy korekty jest Zamień wejściowy zestaw danych i/lub zapytania taki, który wyklucza pola etykiety, jak te nie będą dostępne, gdy usługa jest wywoływana.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-434">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="9cd3e-435">Jest również dobrym rozwiązaniem, aby zmniejszyć rozmiar wejściowy zestaw danych i/lub kwerendy na kilka rekordów wystarczającego wskazująca schemat danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-435">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="9cd3e-436">Port wyjściowy jest wspólny dla wszystkich wejściowych Dołączanie i wykluczanie tylko **oceniane etykiety** i **wynik prawdopodobieństwa** w danych wyjściowych przy użyciu [Select Columns in Dataset] [ select-columns] modułu.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-436">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="9cd3e-437">Przykładowe oceniania eksperymentu znajduje się na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-437">A sample scoring experiment is provided in the figure below.</span></span> <span data-ttu-id="9cd3e-438">Gdy będzie gotowy do wdrożenia, kliknij przycisk **OPUBLIKOWAĆ usługi sieci WEB** na dolnym pasku akcji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-438">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Publikowanie Azure ML][11]

## <a name="summary"></a><span data-ttu-id="9cd3e-440">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="9cd3e-440">Summary</span></span>
<span data-ttu-id="9cd3e-441">Aby recap, co możemy to zostało zrobione w tym samouczku wskazówki, utworzono środowisku nauki danych Azure doświadczenie z dużego zestawu danych publicznych, dostarczanej przez proces nauki zespołu danych od pozyskiwania danych do uczenia modelu, a następnie do Wdrażanie usługi sieci web uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-441">To recap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through the Team Data Science Process, all the way from data acquisition to model training, and then to the deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="9cd3e-442">Informacje o licencji</span><span class="sxs-lookup"><span data-stu-id="9cd3e-442">License information</span></span>
<span data-ttu-id="9cd3e-443">Ten przewodnik próbki i jego towarzyszące IPython notebook(s) i skrypty są udostępniane przez firmę Microsoft w ramach licencji MIT.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="9cd3e-444">Sprawdź plik LICENSE.txt w katalogu przykładowy kod w witrynie GitHub, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="9cd3e-444">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="9cd3e-445">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="9cd3e-445">References</span></span>
<span data-ttu-id="9cd3e-446">• [Andrés Monroy taksówki NYC rund stronę pobierania](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="9cd3e-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="9cd3e-447">• [FOILing NYC taksówki podróży danych przez Krzysztof Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="9cd3e-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="9cd3e-448">• [Taksówki NYC i Limousine Komisji badań i statystyki](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="9cd3e-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
