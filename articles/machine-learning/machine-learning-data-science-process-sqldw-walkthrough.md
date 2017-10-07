---
title: "Hello proces nauki danych zespołu w działaniu: przy użyciu usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="17084-103">Hello proces nauki danych zespołu w działaniu: przy użyciu magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="17084-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="17084-104">W tym samouczku, możemy opisano tworzenie i wdrażanie modelu uczenia maszynowego przy użyciu magazynu danych SQL (SQL DW) dla elementu dataset publicznie dostępnych — hello [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="17084-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="17084-105">model klasyfikacji binarnej Hello skonstruowany prognozuje czy poradę ma być stosowany w podróży i modele wieloklasowej klasyfikacji i regresji omówiono także które prognozowania hello dystrybucji dla kwoty Porada hello płatnej.</span><span class="sxs-lookup"><span data-stu-id="17084-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="17084-106">procedury Hello następuje hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) przepływu pracy.</span><span class="sxs-lookup"><span data-stu-id="17084-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="17084-107">Zostanie przedstawiony sposób toosetup środowisku nauki danych jak tooload hello danych do magazynu danych SQL i sposobie używania magazynu danych SQL lub notesu IPython tooexplore hello danych i odtwarzania funkcji toomodel.</span><span class="sxs-lookup"><span data-stu-id="17084-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="17084-108">Następnie zostanie przedstawiony sposób toobuild i wdrażanie modelu przy użyciu usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="17084-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="17084-109"><a name="dataset"></a>Witaj NYC taksówki rund w zestawie danych</span><span class="sxs-lookup"><span data-stu-id="17084-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="17084-110">Hello podróży taksówki NYC danych składa się z około 20GB skompresowanego plików CSV (~ 48GB nieskompresowane), rejestrowanie ponad milion 173 poszczególnych podróży i hello cen w klasie ekonomicznej płatnej w odniesieniu do każdej podróży.</span><span class="sxs-lookup"><span data-stu-id="17084-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="17084-111">Każdy rekord podróży zawiera hello odbiór i przyjmowania lokalizacje i godziny anonimowe hack numer licencji (sterownik) i hello numer Medalionu (taksówki jego unikatowy identyfikator).</span><span class="sxs-lookup"><span data-stu-id="17084-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="17084-112">Hello danych obejmuje wszystkie rund w roku hello 2013 i jest dostępne w powitania po dwóch zestawów danych dla każdego miesiąca:</span><span class="sxs-lookup"><span data-stu-id="17084-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="17084-113">Witaj **trip_data.csv** plik zawiera szczegóły podróży, takie jak liczba pasażerów, punkty odbiór i dropoff, czas trwania podróży i długość podróży.</span><span class="sxs-lookup"><span data-stu-id="17084-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="17084-114">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="17084-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="17084-115">Witaj **trip_fare.csv** pliku zawiera szczegółowe informacje o klasie hello za każdym razem, takie jak typ płatności, kwota taryfy przeciążenia i podatków, porady i przejazd i Suma hello płatnej.</span><span class="sxs-lookup"><span data-stu-id="17084-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="17084-116">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="17084-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="17084-117">Witaj **Unikatowy klucz** używane podróży toojoin\_danych i podróży\_taryfy składa się z hello następujące trzy pola:</span><span class="sxs-lookup"><span data-stu-id="17084-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="17084-118">Medalionu,</span><span class="sxs-lookup"><span data-stu-id="17084-118">medallion,</span></span>
* <span data-ttu-id="17084-119">Funkcja\_licencji i</span><span class="sxs-lookup"><span data-stu-id="17084-119">hack\_license and</span></span>
* <span data-ttu-id="17084-120">pobranie\_daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="17084-120">pickup\_datetime.</span></span>

## <span data-ttu-id="17084-121"><a name="mltasks"></a>Adres trzy typy zadań prognozowania</span><span class="sxs-lookup"><span data-stu-id="17084-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="17084-122">Firma Microsoft sformułować trzy problemów prognozowania oparte na powitania *Porada\_kwota* tooillustrate trzy rodzaje modelowania zadań:</span><span class="sxs-lookup"><span data-stu-id="17084-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="17084-123">**Klasyfikacji binarnej**: toopredict czy poradę został płatnej podróży, tj. *Porada\_kwota* większą niż $0 jest przykład dodatnią, podczas gdy *Porada\_kwota* $ 0 to przykład ujemna.</span><span class="sxs-lookup"><span data-stu-id="17084-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="17084-124">**Wieloklasowej klasyfikacji**: zakres hello toopredict porady uregulowaniu płatności hello podróży.</span><span class="sxs-lookup"><span data-stu-id="17084-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="17084-125">Możemy podzielić hello *Porada\_kwota* do pięciu bins lub klasy:</span><span class="sxs-lookup"><span data-stu-id="17084-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="17084-126">**Zadanie regresji**: toopredict hello ilość Porada płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="17084-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="17084-127"><a name="setup"></a>Konfigurowanie środowiska nauki danych Azure hello zaawansowana analityka</span><span class="sxs-lookup"><span data-stu-id="17084-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="17084-128">tooset Twojego środowiska nauki danych Azure, wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="17084-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="17084-129">**Utwórz własne konto magazynu obiektów blob platformy Azure**</span><span class="sxs-lookup"><span data-stu-id="17084-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="17084-130">Podczas obsługi administracyjnej magazynu obiektów blob platformy Azure, wybierz lokalizację geograficzną magazynu obiektów blob platformy Azure w lub możliwie najbliżej zbyt**południowo-środkowe stany**, czyli przechowywania hello taksówki NYC danych.</span><span class="sxs-lookup"><span data-stu-id="17084-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="17084-131">Witaj, dane zostaną skopiowane przy użyciu narzędzia AzCopy z hello publicznym kontenerze obiektów blob magazynu kontenera tooa na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="17084-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="17084-132">Witaj bliżej magazynu obiektów blob platformy Azure jest tooSouth środkowe stany USA, hello szybciej (krok 4) będzie można ukończyć tego zadania.</span><span class="sxs-lookup"><span data-stu-id="17084-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="17084-133">Konto magazynu Azure toocreate, hello wykonaj kroki opisane w [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="17084-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="17084-134">Być czy toomake uwagi o wartości hello następujące poświadczenia konta magazynu, które będą potrzebne w dalszej części tego przewodnika.</span><span class="sxs-lookup"><span data-stu-id="17084-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="17084-135">**Nazwa konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="17084-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="17084-136">**Klucz konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="17084-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="17084-137">**Nazwa kontenera** (które mają hello toobe danych przechowywanych w hello magazynu obiektów blob platformy Azure)</span><span class="sxs-lookup"><span data-stu-id="17084-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="17084-138">**Udostępnij wystąpienie magazynu danych SQL Azure.**</span><span class="sxs-lookup"><span data-stu-id="17084-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="17084-139">Postępuj zgodnie z dokumentacją hello na [Tworzenie usługi SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision wystąpienie usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="17084-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="17084-140">Upewnij się, odpowiednie notacji na powitania po poświadczeń magazynu danych SQL, które będą używane w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="17084-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="17084-141">**Nazwa serwera**: <server Name>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="17084-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="17084-142">**Nazwa SQLDW (baza danych)**</span><span class="sxs-lookup"><span data-stu-id="17084-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="17084-143">**Nazwa użytkownika**</span><span class="sxs-lookup"><span data-stu-id="17084-143">**Username**</span></span>
* <span data-ttu-id="17084-144">**Hasło**</span><span class="sxs-lookup"><span data-stu-id="17084-144">**Password**</span></span>

<span data-ttu-id="17084-145">**Zainstaluj program Visual Studio i SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="17084-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="17084-146">Aby uzyskać instrukcje, zobacz [instalacji programu Visual Studio 2015 i/lub program SSDT (SQL Server Data Tools) dla usługi SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="17084-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="17084-147">**Połącz tooyour magazynu danych SQL Azure z programem Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="17084-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="17084-148">Aby uzyskać instrukcje, zobacz kroki 1 i 2 w [tooAzure SQL Data Warehouse Uzyskuj dostęp do programu Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17084-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="17084-149">Uruchom hello następujące zapytanie SQL w bazie danych hello utworzonego w magazynie danych programu SQL (zamiast hello zapytania w kroku 3 hello połączyć tematu) zbyt**utworzyć klucz główny**.</span><span class="sxs-lookup"><span data-stu-id="17084-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="17084-150">**Tworzenie obszaru roboczego uczenia maszynowego Azure w ramach Twojej subskrypcji platformy Azure.**</span><span class="sxs-lookup"><span data-stu-id="17084-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="17084-151">Aby uzyskać instrukcje, zobacz [Utwórz obszar roboczy usługi Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="17084-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="17084-152"><a name="getdata"></a>Ładowanie danych hello do usługi SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="17084-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="17084-153">Otwórz konsolę polecenia programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17084-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="17084-154">Uruchom hello następujące polecenia programu PowerShell toodownload hello przykład SQL pliki skryptów, które firma Microsoft udostępnia użytkownikowi na GitHub tooa katalog lokalny, który określisz z parametrem hello *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="17084-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="17084-155">Można zmienić wartości parametru hello *- DestDir* tooany katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="17084-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="17084-156">Jeśli *- DestDir* nie istnieje, zostanie on utworzony przez hello skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17084-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="17084-157">Może być konieczne zbyt**Uruchom jako Administrator** podczas wykonywania następującego skryptu programu PowerShell, jeśli hello Twojej *DestDir* katalog musi tooit toocreate lub toowrite uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="17084-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="17084-158">Po pomyślnym wykonaniu bieżący katalog roboczy zmienia zbyt*- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="17084-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="17084-159">Powinno być możliwe toosee ekran, tak jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="17084-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="17084-160">W Twojej *- DestDir*, wykonać hello następującego skryptu programu PowerShell w trybie administratora:</span><span class="sxs-lookup"><span data-stu-id="17084-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="17084-161">Po uruchomieniu hello skrypt programu PowerShell dla powitania po raz pierwszy, użytkownik zostanie poproszony tooinput hello informacji z Twojego magazynu danych SQL Azure i konta magazynu obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="17084-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="17084-162">Po zakończeniu tego skryptu PowerShell uruchomiona powitania po raz pierwszy, poświadczenia hello wprowadzania można będzie został napisany pliku konfiguracji tooa SQLDW.conf w katalogu roboczym obecny hello.</span><span class="sxs-lookup"><span data-stu-id="17084-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="17084-163">Witaj przyszłych uruchamianie tego pliku skryptu programu PowerShell ma tooread opcji hello wszystkie niezbędne parametry z tego pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="17084-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="17084-164">Należy toochange niektórych parametrów można wybrać tooinput parametry hello na ekranie powitania na monit o usunięcie tego pliku konfiguracji i wprowadzanie wartości parametrów hello w lub wartości parametrów hello toochange, edytując plik SQLDW.conf hello w Twojej *- DestDir* katalogu.</span><span class="sxs-lookup"><span data-stu-id="17084-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="17084-165">W kolejności tooavoid schematu nazwa powoduje konflikt z tymi, które już istnieją w Twojej SQL DW Azure podczas odczytywania parametrów bezpośrednio z pliku SQLDW.conf hello 3-cyfrowy numer losowe zostanie dodany toohello nazwy schematu z pliku SQLDW.conf hello jako nazwę schematu domyślnego hello każdym uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="17084-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="17084-166">Witaj skrypt programu PowerShell może wyświetlenie monitu o nazwę schematu: można określić nazwę hello uznania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="17084-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="17084-167">To **skrypt programu PowerShell** pliku zakończeniu hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="17084-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="17084-168">**Pobiera i instaluje narzędzie AzCopy**, jeśli nie zainstalowano narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="17084-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
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
* <span data-ttu-id="17084-169">**Kopiuje dane tooyour prywatnego obiektu blob magazynu konta** z hello publicznego obiektu blob z narzędzia AzCopy</span><span class="sxs-lookup"><span data-stu-id="17084-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="17084-170">**Ładuje dane przy użyciu programu Polybase (wykonując LoadDataToSQLDW.sql) tooyour Azure SQL DW** z konta prywatnego obiektu blob magazynu z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="17084-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="17084-171">Tworzenie schematu</span><span class="sxs-lookup"><span data-stu-id="17084-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="17084-172">Tworzenie poświadczeń o zakresie bazy danych</span><span class="sxs-lookup"><span data-stu-id="17084-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="17084-173">Tworzenie zewnętrznego źródła danych dla obiektu blob magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="17084-173">Create an external data source for an Azure storage blob</span></span>
    
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
  * <span data-ttu-id="17084-174">Tworzenie zewnętrznego formatu pliku dla pliku csv.</span><span class="sxs-lookup"><span data-stu-id="17084-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="17084-175">Jest nieskompresowanych danych i pola są oddzielone znakiem hello znaku kreski pionowej.</span><span class="sxs-lookup"><span data-stu-id="17084-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
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
  * <span data-ttu-id="17084-176">Tworzenie zewnętrznego taryfy i tabele podróży dla zestawu danych taksówki NYC w magazynie obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="17084-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
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

    - <span data-ttu-id="17084-177">Ładowanie danych z tabel zewnętrznych w tooSQL magazynu obiektów blob platformy Azure magazynu danych</span><span class="sxs-lookup"><span data-stu-id="17084-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

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

    - <span data-ttu-id="17084-178">Utwórz tabelę danych przykładowych (NYCTaxi_Sample) i Wstaw tooit danych z wybranie zapytania SQL w tabelach podróży i taryfy hello.</span><span class="sxs-lookup"><span data-stu-id="17084-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="17084-179">(Niektóre kroki tego przewodnika wymaga toouse tej tabeli.)</span><span class="sxs-lookup"><span data-stu-id="17084-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

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

<span data-ttu-id="17084-180">Lokalizacja geograficzna Hello kont magazynu ma wpływ na czas ładowania.</span><span class="sxs-lookup"><span data-stu-id="17084-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="17084-181">W zależności od hello lokalizację geograficzną konto magazynu obiektów blob prywatne, hello proces kopiowania danych z konta magazynu prywatnego tooyour publicznego obiektu blob może potrwać około 15 minut lub nawet dłużej który hello proces ładowania danych z konta magazynu tooyour Azure SQL DW może potrwać 20 minut lub dłużej.</span><span class="sxs-lookup"><span data-stu-id="17084-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="17084-182">Konieczne będzie toodecide co zrobić, jeśli masz zduplikowanego źródła i pliki docelowe.</span><span class="sxs-lookup"><span data-stu-id="17084-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="17084-183">Jeśli toobe plików CSV hello skopiowane z konta magazynu prywatnego obiektu blob tooyour hello publicznego obiektu blob magazynu już istnieje w konto magazynu obiektów blob prywatne, AzCopy zapyta, czy ma toooverwrite je.</span><span class="sxs-lookup"><span data-stu-id="17084-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="17084-184">Jeśli nie chcesz toooverwrite ich, wejściowych  **n**  po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="17084-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="17084-185">Jeśli chcesz, aby toooverwrite **wszystkie** z nich, wprowadź **** po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="17084-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="17084-186">Możesz również wpisać **y** CSV toooverwrite pliki pojedynczo.</span><span class="sxs-lookup"><span data-stu-id="17084-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![Wykreślenia #21][21]

<span data-ttu-id="17084-188">Można użyć własnych danych.</span><span class="sxs-lookup"><span data-stu-id="17084-188">You can use your own data.</span></span> <span data-ttu-id="17084-189">Jeśli do komputera lokalnego w aplikacji rzeczywistych danych, można nadal używać narzędzia AzCopy tooupload lokalnych danych tooyour prywatnego magazynu Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="17084-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="17084-190">Wystarczy toochange hello **źródła** lokalizacji, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, w hello AzCopy polecenie hello PowerShell skryptu pliku toohello katalog lokalny, który zawiera dane.</span><span class="sxs-lookup"><span data-stu-id="17084-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="17084-191">Jeśli dane są już w magazynie obiektów blob platformy Azure prywatnych w rzeczywistych aplikacji, można pominąć hello AzCopy kroku w hello skrypt programu PowerShell i przekazać bezpośrednio hello tooAzure danych magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="17084-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="17084-192">Wymaga to, że dodatkowe edytuje z tootailor skryptu hello ją toohello format danych.</span><span class="sxs-lookup"><span data-stu-id="17084-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="17084-193">Ten skrypt programu Powershell również podłącza hello Azure SQL DW informacji do hello eksploracji przykładowe pliki danych SQLDW_Explorations.sql, SQLDW_Explorations.ipynb i SQLDW_Explorations_Scripts.py tak, aby te trzy pliki są gotowe toobe wypróbowane natychmiast Po zakończeniu hello skrypt programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17084-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="17084-194">Po pomyślnym wykonaniu, zostanie wyświetlony ekran, takich jak poniżej:</span><span class="sxs-lookup"><span data-stu-id="17084-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="17084-195"><a name="dbexplore"></a>Eksploracja danych i funkcji inżynieryjne w usłudze Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="17084-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="17084-196">W tej sekcji możemy wykonywać Generowanie funkcji i eksploracja danych przez wykonywanie zapytań SQL magazynu danych SQL Azure bezpośrednio przy użyciu **programu Visual Studio Tools danych**.</span><span class="sxs-lookup"><span data-stu-id="17084-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="17084-197">Wszystkie zapytania SQL w tej sekcji znajdują się w hello przykładowy skrypt o nazwie *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="17084-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="17084-198">Ten plik został już pobrany tooyour katalogu lokalnego za pomocą skryptu programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="17084-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="17084-199">Można również pobrać go z [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="17084-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="17084-200">Ale plik hello w serwisie GitHub nie ma informacji magazynu danych SQL Azure hello podłączony.</span><span class="sxs-lookup"><span data-stu-id="17084-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="17084-201">Połącz tooyour magazynu danych SQL Azure za pomocą programu Visual Studio o nazwie logowania SQL DW hello i hasła i otwarcie hello **Eksplorator obiektów SQL** tooconfirm hello w bazie danych i tabele zostały zaimportowane.</span><span class="sxs-lookup"><span data-stu-id="17084-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="17084-202">Pobrać hello *SQLDW_Explorations.sql* pliku.</span><span class="sxs-lookup"><span data-stu-id="17084-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="17084-203">tooopen edytorze zapytań równoległych magazynu danych (PDW), użyj hello **nowe zapytanie** polecenia aż do Twojej PDW wybrano hello **Eksplorator obiektów SQL**.</span><span class="sxs-lookup"><span data-stu-id="17084-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="17084-204">Witaj standardowego edytora zapytań SQL nie jest obsługiwany przez PDW.</span><span class="sxs-lookup"><span data-stu-id="17084-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="17084-205">W tym miejscu są dane typu hello eksploracji i funkcji generowania wykonywane w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="17084-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="17084-206">Eksplorowanie danych dystrybucji kilka pól w różnym czasie systemu windows.</span><span class="sxs-lookup"><span data-stu-id="17084-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="17084-207">Zbadaj jakości danych hello pól długości i szerokości geograficznej.</span><span class="sxs-lookup"><span data-stu-id="17084-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="17084-208">Generowanie etykiet klasyfikacji binarnej i wieloklasowej oparte na powitania **Porada\_kwota**.</span><span class="sxs-lookup"><span data-stu-id="17084-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="17084-209">Generowanie funkcji i obliczeń lub porównania odległości podróży.</span><span class="sxs-lookup"><span data-stu-id="17084-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="17084-210">Dołącz Witaj dwie tabele i Wyodrębnij losowej próbki, które będzie używane toobuild modeli.</span><span class="sxs-lookup"><span data-stu-id="17084-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="17084-211">Weryfikacja importu danych</span><span class="sxs-lookup"><span data-stu-id="17084-211">Data import verification</span></span>
<span data-ttu-id="17084-212">Kwerendy te zapewniają szybki weryfikacji hello liczby wierszy i kolumn w powitalne zaimportować tabele wypełniać wcześniej przy użyciu zbiorczego równoległe w programie Polybase,</span><span class="sxs-lookup"><span data-stu-id="17084-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="17084-213">**Dane wyjściowe:** należy pobrać 173,179,759 wierszy i kolumn 14.</span><span class="sxs-lookup"><span data-stu-id="17084-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="17084-214">Eksploracja: Podróży dystrybucji przez Medalionu</span><span class="sxs-lookup"><span data-stu-id="17084-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="17084-215">To przykładowe zapytanie identyfikuje medallions hello (taksówki numery) wykonanych więcej niż 100 rund w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="17084-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="17084-216">Zapytanie Hello korzystałby z hello na partycje tabeli dostępu, ponieważ należy przygotować przez schemat partycji hello **podnoszenia\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="17084-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="17084-217">Badania hello pełnego zestawu danych będzie również używać tabeli partycjonowanej hello i/lub indeksu skanowania.</span><span class="sxs-lookup"><span data-stu-id="17084-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="17084-218">**Dane wyjściowe:** zapytań hello powinien zwraca tabelę z wierszami Określanie hello 13,369 medallions (taksówkach) i hello Liczba podróży zakończone przez nich 2013.</span><span class="sxs-lookup"><span data-stu-id="17084-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="17084-219">Witaj ostatnia kolumna zawiera liczby hello hello liczby rund ukończone.</span><span class="sxs-lookup"><span data-stu-id="17084-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="17084-220">Eksploracja: Podróży dystrybucji Medalionu i hack_license</span><span class="sxs-lookup"><span data-stu-id="17084-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="17084-221">W tym przykładzie identyfikuje hello medallions (taksówki cyfry) i hack_license cyfry (sterowniki) zakończona ponad 100 rund w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="17084-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="17084-222">**Dane wyjściowe:** zapytania hello powinien zwrócić tabelę z wierszami 13,369 określenie hello 13,369 samochodu/driver identyfikatorów, które ukończyły bardziej tego 100 rund w 2013.</span><span class="sxs-lookup"><span data-stu-id="17084-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="17084-223">Witaj ostatnia kolumna zawiera liczby hello hello liczby rund ukończone.</span><span class="sxs-lookup"><span data-stu-id="17084-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="17084-224">Ocena jakości danych: Weryfikuj rekordy z geograficzne niepoprawne i/lub szerokość geograficzną</span><span class="sxs-lookup"><span data-stu-id="17084-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="17084-225">W tym przykładzie sprawdza, czy hello geograficzne i/lub szerokość geograficzną polach albo zawiera nieprawidłową wartość (stopni w radianach powinna należeć do zakresu od-90 do 90,) lub (0, 0) współrzędnych.</span><span class="sxs-lookup"><span data-stu-id="17084-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="17084-226">**Dane wyjściowe:** hello zapytanie zwraca 837,467 podróży, które mają nieprawidłowe pola geograficzne i/lub szerokość geograficzną.</span><span class="sxs-lookup"><span data-stu-id="17084-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="17084-227">Eksploracja: Przechylony a nie Przechylony rund dystrybucji</span><span class="sxs-lookup"><span data-stu-id="17084-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="17084-228">W tym przykładzie znajduje hello Liczba podróży, które zostały Przechylony a numer hello, które nie zostały Przechylony w określonym przedziale czasu (lub hello pełnego zestawu danych, jeśli obejmujące cały rok hello, jak jest skonfigurowana w tym miejscu).</span><span class="sxs-lookup"><span data-stu-id="17084-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="17084-229">Tej dystrybucji odzwierciedla toobe dystrybucji binarne etykiety hello później użyć do modelowania klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="17084-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="17084-230">**Dane wyjściowe:** hello zapytania należy następujące zwracany hello Porada częstotliwości hello roku 2013: 90,447,622 Przechylony i 82,264,709 Przechylony nie.</span><span class="sxs-lookup"><span data-stu-id="17084-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="17084-231">Eksploracja: Porada klasy/zakres dystrybucji</span><span class="sxs-lookup"><span data-stu-id="17084-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="17084-232">W tym przykładzie oblicza dystrybucji hello Porada zakresów w danym momencie okres (lub w hello pełnego zestawu danych jeśli obejmujące cały rok hello).</span><span class="sxs-lookup"><span data-stu-id="17084-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="17084-233">Jest to dystrybucji hello hello etykiety klas, które będą później używane do modelowania wieloklasowej klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="17084-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

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

<span data-ttu-id="17084-234">**Dane wyjściowe:**</span><span class="sxs-lookup"><span data-stu-id="17084-234">**Output:**</span></span>

| <span data-ttu-id="17084-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="17084-235">tip_class</span></span> | <span data-ttu-id="17084-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="17084-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="17084-237">1</span><span class="sxs-lookup"><span data-stu-id="17084-237">1</span></span> |<span data-ttu-id="17084-238">82230915</span><span class="sxs-lookup"><span data-stu-id="17084-238">82230915</span></span> |
| <span data-ttu-id="17084-239">2</span><span class="sxs-lookup"><span data-stu-id="17084-239">2</span></span> |<span data-ttu-id="17084-240">6198803</span><span class="sxs-lookup"><span data-stu-id="17084-240">6198803</span></span> |
| <span data-ttu-id="17084-241">3</span><span class="sxs-lookup"><span data-stu-id="17084-241">3</span></span> |<span data-ttu-id="17084-242">1932223</span><span class="sxs-lookup"><span data-stu-id="17084-242">1932223</span></span> |
| <span data-ttu-id="17084-243">0</span><span class="sxs-lookup"><span data-stu-id="17084-243">0</span></span> |<span data-ttu-id="17084-244">82264625</span><span class="sxs-lookup"><span data-stu-id="17084-244">82264625</span></span> |
| <span data-ttu-id="17084-245">4</span><span class="sxs-lookup"><span data-stu-id="17084-245">4</span></span> |<span data-ttu-id="17084-246">85765</span><span class="sxs-lookup"><span data-stu-id="17084-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="17084-247">Eksploracja: Obliczania i porównać odległość podróży</span><span class="sxs-lookup"><span data-stu-id="17084-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="17084-248">W tym przykładzie konwertuje hello odbiór i przyjmowania geograficzne i współrzędne geograficzne tooSQL punktów, oblicza odległość podróży hello przy użyciu różnicę punktów geograficzne SQL i zwraca losowej próbki hello wyniki do porównania.</span><span class="sxs-lookup"><span data-stu-id="17084-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="17084-249">przykład Witaj ogranicza wyniki hello toovalid koordynuje tylko przy użyciu objętych wcześniej hello danych jakości oceny zapytania.</span><span class="sxs-lookup"><span data-stu-id="17084-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
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

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="17084-250">Funkcja engineering przy użyciu funkcji SQL</span><span class="sxs-lookup"><span data-stu-id="17084-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="17084-251">Czasami funkcje SQL mogą być wydajne opcję engineering funkcji.</span><span class="sxs-lookup"><span data-stu-id="17084-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="17084-252">W tym przewodniku zdefiniowanego SQL funkcja toocalculate hello bezpośredniego odległości między lokalizacjami odbiór i dropoff hello.</span><span class="sxs-lookup"><span data-stu-id="17084-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="17084-253">Możesz uruchomić hello następujące skrypty SQL w **programu Visual Studio Tools danych**.</span><span class="sxs-lookup"><span data-stu-id="17084-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="17084-254">Oto hello SQL skrypt, który definiuje funkcję odległość hello.</span><span class="sxs-lookup"><span data-stu-id="17084-254">Here is hello SQL script that defines hello distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="17084-255">Oto przykład toocall funkcje toogenerate tej funkcji w zapytaniu SQL:</span><span class="sxs-lookup"><span data-stu-id="17084-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="17084-256">**Dane wyjściowe:** to zapytanie generuje tabeli (z 2,803,538 wierszy) z odbiór i dropoff długości i szerokości geograficzne i hello odpowiadająca odległości w milach bezpośrednie.</span><span class="sxs-lookup"><span data-stu-id="17084-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="17084-257">Poniżej przedstawiono wyniki hello pierwsze 3 wiersze:</span><span class="sxs-lookup"><span data-stu-id="17084-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="17084-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="17084-258">pickup_latitude</span></span> | <span data-ttu-id="17084-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="17084-259">pickup_longitude</span></span> | <span data-ttu-id="17084-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="17084-260">dropoff_latitude</span></span> | <span data-ttu-id="17084-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="17084-261">dropoff_longitude</span></span> | <span data-ttu-id="17084-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="17084-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="17084-263">1</span><span class="sxs-lookup"><span data-stu-id="17084-263">1</span></span> |<span data-ttu-id="17084-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="17084-264">40.731804</span></span> |<span data-ttu-id="17084-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="17084-265">-74.001083</span></span> |<span data-ttu-id="17084-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="17084-266">40.736622</span></span> |<span data-ttu-id="17084-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="17084-267">-73.988953</span></span> |<span data-ttu-id="17084-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="17084-268">.7169601222</span></span> |
| <span data-ttu-id="17084-269">2</span><span class="sxs-lookup"><span data-stu-id="17084-269">2</span></span> |<span data-ttu-id="17084-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="17084-270">40.715794</span></span> |<span data-ttu-id="17084-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="17084-271">-74,010635</span></span> |<span data-ttu-id="17084-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="17084-272">40.725338</span></span> |<span data-ttu-id="17084-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="17084-273">-74.00399</span></span> |<span data-ttu-id="17084-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="17084-274">.7448343721</span></span> |
| <span data-ttu-id="17084-275">3</span><span class="sxs-lookup"><span data-stu-id="17084-275">3</span></span> |<span data-ttu-id="17084-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="17084-276">40.761456</span></span> |<span data-ttu-id="17084-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="17084-277">-73.999886</span></span> |<span data-ttu-id="17084-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="17084-278">40.766544</span></span> |<span data-ttu-id="17084-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="17084-279">-73.988228</span></span> |<span data-ttu-id="17084-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="17084-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="17084-281">Przygotowanie do tworzenia modelu danych</span><span class="sxs-lookup"><span data-stu-id="17084-281">Prepare data for model building</span></span>
<span data-ttu-id="17084-282">Witaj następujące zapytanie sprzęga hello **nyctaxi\_podróży** i **nyctaxi\_taryfy** tabel, generuje etykiety klasyfikacji binarnej **Przechylony**, etykiety klasyfikacji wielu klasy **Porada\_klasy**i wyodrębnia próbki z hello pełnego dołączonego do zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="17084-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="17084-283">próbkowanie Hello odbywa się przez pobranie podzbiór rund hello na podstawie czasu odbioru.</span><span class="sxs-lookup"><span data-stu-id="17084-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="17084-284">To zapytanie może skopiować następnie wkleić bezpośrednio w hello [Azure Machine Learning Studio](https://studio.azureml.net) [i zaimportuj dane] [ import-data] modułu dla wprowadzanie danych bezpośrednio z wystąpienia bazy danych SQL hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="17084-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="17084-285">Zapytanie Hello wyklucza rekordy z niepoprawne (0, 0) współrzędnych.</span><span class="sxs-lookup"><span data-stu-id="17084-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

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

<span data-ttu-id="17084-286">Gdy są gotowe tooproceed tooAzure uczenia maszynowego, użytkownik może:</span><span class="sxs-lookup"><span data-stu-id="17084-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="17084-287">Zapisz hello końcowego SQL kwerendy tooextract i przykładowa hello danych i kopiowania i wklejania hello zapytanie bezpośrednio do [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning, lub</span><span class="sxs-lookup"><span data-stu-id="17084-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="17084-288">Utrwalanie hello próbkowany i odtworzone danych planujesz toouse modelu tworzenie w nowej SQL DW tabeli i korzystanie z nowej tabeli hello w hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="17084-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="17084-289">Witaj skrypt programu PowerShell w poprzednim kroku ma zostało to zrobione automatycznie.</span><span class="sxs-lookup"><span data-stu-id="17084-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="17084-290">Możesz przeczytać bezpośrednio z tej tabeli w hello importowanie danych modułu.</span><span class="sxs-lookup"><span data-stu-id="17084-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="17084-291"><a name="ipnb"></a>Eksploracja danych i funkcji inżynieryjne w notesie IPython</span><span class="sxs-lookup"><span data-stu-id="17084-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="17084-292">W tej sekcji zostaną wykonane Eksplorowanie danych oraz generowanie funkcji za pomocą obu Python i zapytań SQL hello SQL DW utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="17084-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="17084-293">Przykładowe IPython Notes o nazwie **SQLDW_Explorations.ipynb** plik skryptu języka Python **SQLDW_Explorations_Scripts.py** zostały pobrane tooyour katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="17084-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="17084-294">Są również dostępne na [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="17084-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="17084-295">Te dwa pliki są identyczne w skryptach Python.</span><span class="sxs-lookup"><span data-stu-id="17084-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="17084-296">plik skryptu języka Python Hello podano tooyou w przypadku, gdy nie masz serwera IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="17084-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="17084-297">Te dwa przykładowe Python plików zostały zaprojektowane pod **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="17084-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="17084-298">Witaj potrzebnych informacji magazynu danych SQL Azure w przykładowym hello notesu IPython i hello Python komputera lokalnego tooyour pobranego pliku skryptu został podłączony za pomocą skryptu programu PowerShell hello wcześniej.</span><span class="sxs-lookup"><span data-stu-id="17084-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="17084-299">Są one wykonywalny bez żadnych modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="17084-299">They are executable without any modification.</span></span>

<span data-ttu-id="17084-300">Jeśli obszar roboczy uczenie maszynowe Azure zostały już skonfigurowane, możesz bezpośrednio Przekaż przykładowe hello usługi uczenie maszynowe Azure IPython notesu toohello notesu IPython i jej uruchamianie.</span><span class="sxs-lookup"><span data-stu-id="17084-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="17084-301">Poniżej przedstawiono hello kroki tooupload tooAzureML notesu IPython usługi:</span><span class="sxs-lookup"><span data-stu-id="17084-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="17084-302">Zaloguj się w tooyour uczenie maszynowe Azure w obszarze roboczym, kliknij przycisk "Studio" u góry hello, a następnie kliknij przycisk "Komputery przenośne", po lewej stronie powitania hello strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="17084-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![Wykreślenia #22][22]
2. <span data-ttu-id="17084-304">Kliknij "Nowy" hello lewym dolnym rogu strony sieci web hello i wybierz pozycję "Python 2".</span><span class="sxs-lookup"><span data-stu-id="17084-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="17084-305">Następnie podaj nazwę notesu toohello i kliknij hello znacznik wyboru toocreate hello nowego pustego IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="17084-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![Wykreślenia #23][23]
3. <span data-ttu-id="17084-307">Kliknij symbol "Jupyter" hello na powitania lewym górnym rogu hello nowy notes IPython.</span><span class="sxs-lookup"><span data-stu-id="17084-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![Wykreślenia #24][24]
4. <span data-ttu-id="17084-309">Przeciągnij i upuść hello próbki notesu IPython toohello **drzewa** z usługi uczenie maszynowe Azure IPython notesu, a następnie kliknij przycisk **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="17084-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="17084-310">Przykładowe hello notesu IPython zostaną przekazane toohello usługi uczenie maszynowe Azure IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="17084-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![Wykreślenia #25][25]

<span data-ttu-id="17084-312">W kolejności toorun hello przykładowe notesu IPython lub hello pliku skryptu języka Python, hello następujące pakiety Python niezbędne.</span><span class="sxs-lookup"><span data-stu-id="17084-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="17084-313">Jeśli używasz usługi uczenie maszynowe Azure IPython notesu hello te pakiety zostały wstępnie zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="17084-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="17084-314">pandas</span><span class="sxs-lookup"><span data-stu-id="17084-314">pandas</span></span>
    - <span data-ttu-id="17084-315">numpy</span><span class="sxs-lookup"><span data-stu-id="17084-315">numpy</span></span>
    - <span data-ttu-id="17084-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="17084-316">matplotlib</span></span>
    - <span data-ttu-id="17084-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="17084-317">pyodbc</span></span>
    - <span data-ttu-id="17084-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="17084-318">PyTables</span></span>

<span data-ttu-id="17084-319">Hello zalecany sekwencji, podczas tworzenia zaawansowanych rozwiązań analitycznych na uczenie maszynowe Azure z dużej ilości danych jest hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="17084-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="17084-320">Odczyt w małej przykładowej hello danych do ramki danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="17084-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="17084-321">Wykonywanie niektórych wizualizacje i eksploracji przy użyciu danych hello próbkowane.</span><span class="sxs-lookup"><span data-stu-id="17084-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="17084-322">Wypróbuj engineering funkcji przy użyciu danych hello próbkowane.</span><span class="sxs-lookup"><span data-stu-id="17084-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="17084-323">Dla większych Eksploracja danych do manipulowania danymi i funkcji zespołu inżynieryjnego, użyj zapytania SQL tooissue Python bezpośrednio przed hello magazynu danych SQL.</span><span class="sxs-lookup"><span data-stu-id="17084-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="17084-324">Zdecyduj, toobe rozmiar próbki hello odpowiednie do konstruowania modelu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="17084-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="17084-325">Po Hello są kilka Eksploracja danych, wizualizacji danych i przykłady engineering funkcji.</span><span class="sxs-lookup"><span data-stu-id="17084-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="17084-326">Więcej eksploracji danych można znaleźć w przykładowych hello notesu IPython i hello przykładowy plik skryptu języka Python.</span><span class="sxs-lookup"><span data-stu-id="17084-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="17084-327">Inicjowanie poświadczenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="17084-327">Initialize database credentials</span></span>
<span data-ttu-id="17084-328">Inicjowanie ustawienia połączenia bazy danych w hello następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="17084-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="17084-329">Utwórz połączenie z bazą danych</span><span class="sxs-lookup"><span data-stu-id="17084-329">Create database connection</span></span>
<span data-ttu-id="17084-330">Oto hello parametry połączenia, które tworzy hello połączenia toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="17084-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="17084-331">Raport liczba wierszy i kolumn w tabeli < nyctaxi_trip ></span><span class="sxs-lookup"><span data-stu-id="17084-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
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

* <span data-ttu-id="17084-332">Całkowita liczba wierszy = 173179759</span><span class="sxs-lookup"><span data-stu-id="17084-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="17084-333">Łączna liczba kolumn = 14</span><span class="sxs-lookup"><span data-stu-id="17084-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="17084-334">Raport liczba wierszy i kolumn w tabeli < nyctaxi_fare ></span><span class="sxs-lookup"><span data-stu-id="17084-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
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

* <span data-ttu-id="17084-335">Całkowita liczba wierszy = 173179759</span><span class="sxs-lookup"><span data-stu-id="17084-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="17084-336">Łączna liczba kolumn = 11</span><span class="sxs-lookup"><span data-stu-id="17084-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="17084-337">Odczytaj w przykładowych danych małych z hello bazy danych magazynu danych SQL</span><span class="sxs-lookup"><span data-stu-id="17084-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
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
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="17084-338">Czas tooread hello Przykładowa tabela jest 14.096495 sekund.</span><span class="sxs-lookup"><span data-stu-id="17084-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="17084-339">Liczba wierszy i kolumn pobrać = (1000, 21).</span><span class="sxs-lookup"><span data-stu-id="17084-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="17084-340">Statystyki opisowe</span><span class="sxs-lookup"><span data-stu-id="17084-340">Descriptive statistics</span></span>
<span data-ttu-id="17084-341">Teraz wszystko jest gotowe tooexplore hello próbce danych.</span><span class="sxs-lookup"><span data-stu-id="17084-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="17084-342">Możemy zaczynać się patrzeć statystykami opisowy dla hello **podróży\_odległość** (lub inne pola, możesz wybrać toospecify).</span><span class="sxs-lookup"><span data-stu-id="17084-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="17084-343">Wizualizacji: Przykład kreślenia pola</span><span class="sxs-lookup"><span data-stu-id="17084-343">Visualization: Box plot example</span></span>
<span data-ttu-id="17084-344">Następnie przyjrzymy się hello skrzynkowy dla hello podróży odległość toovisualize hello quantiles.</span><span class="sxs-lookup"><span data-stu-id="17084-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Wykreślenia #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="17084-346">Wizualizacji: Przykład kreślenia dystrybucji</span><span class="sxs-lookup"><span data-stu-id="17084-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="17084-347">Wykresy, które wizualizacji hello dystrybucji i histogram hello próbkowany odległości podróży.</span><span class="sxs-lookup"><span data-stu-id="17084-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Wykreślenia #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="17084-349">Wizualizacja: Pasek i geograficzne wiersza</span><span class="sxs-lookup"><span data-stu-id="17084-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="17084-350">W tym przykładzie firma Microsoft hello odległość podróży do pięciu bins bin i wizualizację hello binning wyników.</span><span class="sxs-lookup"><span data-stu-id="17084-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="17084-351">Firma Microsoft wykreślenia hello powyżej dystrybucji bin na pasku lub wiersz kreślenia z:</span><span class="sxs-lookup"><span data-stu-id="17084-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Wykreślenia #3][3]

<span data-ttu-id="17084-353">i</span><span class="sxs-lookup"><span data-stu-id="17084-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Wykreślenia #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="17084-355">Wizualizacji: Przykłady Scatterplot</span><span class="sxs-lookup"><span data-stu-id="17084-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="17084-356">Zostanie przedstawiony jest wykres punktowy między **podróży\_czasu\_w\_s** i **podróży\_odległość** toosee w przypadku dowolnego korelacji</span><span class="sxs-lookup"><span data-stu-id="17084-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Wykreślenia #6][6]

<span data-ttu-id="17084-358">Podobnie można sprawdzić hello relacji między **szybkość\_kod** i **podróży\_odległość**.</span><span class="sxs-lookup"><span data-stu-id="17084-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Wykreślenia #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="17084-360">Eksploracja danych na próbki danych za pomocą zapytań SQL w notesie IPython</span><span class="sxs-lookup"><span data-stu-id="17084-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="17084-361">W tej sekcji możemy Eksplorowanie danych dystrybucji przy użyciu danych hello próbkowany, którym jest umieszczany w nowej tabeli hello, utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="17084-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="17084-362">Należy pamiętać, że podobne eksploracji może zostać wykonane przy użyciu oryginalnego tabel hello.</span><span class="sxs-lookup"><span data-stu-id="17084-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="17084-363">Eksploracja: Raport liczba wierszy i kolumn w hello próbkowany tabeli</span><span class="sxs-lookup"><span data-stu-id="17084-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="17084-364">Eksploracja: Przechylony nie zwracać dystrybucji</span><span class="sxs-lookup"><span data-stu-id="17084-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="17084-365">Eksploracja: Porada klasy dystrybucji</span><span class="sxs-lookup"><span data-stu-id="17084-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="17084-366">Eksploracja: Wykreślenia hello Porada dystrybucji przez klasę</span><span class="sxs-lookup"><span data-stu-id="17084-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![#26 kreślenia][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="17084-368">Eksploracji: Codzienne dystrybucji rund</span><span class="sxs-lookup"><span data-stu-id="17084-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="17084-369">Eksploracja: Podróży dystrybucji na Medalionu</span><span class="sxs-lookup"><span data-stu-id="17084-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="17084-370">Eksploracja: Podróży dystrybucji przez Medalionu i hack licencji</span><span class="sxs-lookup"><span data-stu-id="17084-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="17084-371">Eksploracja: Podróży czasu dystrybucji</span><span class="sxs-lookup"><span data-stu-id="17084-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="17084-372">Eksploracja: Podróży odległość dystrybucji</span><span class="sxs-lookup"><span data-stu-id="17084-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="17084-373">Eksploracji: Dystrybucja typ płatności</span><span class="sxs-lookup"><span data-stu-id="17084-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="17084-374">Sprawdź hello końcowego formę hello featurized tabeli</span><span class="sxs-lookup"><span data-stu-id="17084-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="17084-375"><a name="mlmodel"></a>Tworzenie modeli w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="17084-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="17084-376">Firma Microsoft są teraz gotowe tooproceed toomodel tworzenia i wdrażania modelu w [usługi Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="17084-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="17084-377">dane Hello jest gotowy toobe używana w żadnym hello prognozowania problemy wcześniej, to znaczy:</span><span class="sxs-lookup"><span data-stu-id="17084-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="17084-378">**Klasyfikacji binarnej**: toopredict czy poradę został płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="17084-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="17084-379">**Wieloklasowej klasyfikacji**: zakres hello toopredict porady płatnej, zgodnie z uprzednio zdefiniowanej klasy toohello.</span><span class="sxs-lookup"><span data-stu-id="17084-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="17084-380">**Zadanie regresji**: toopredict hello ilość Porada płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="17084-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="17084-381">toobegin hello modelowania wykonywania, zaloguj się za tooyour **usługi Azure Machine Learning** obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="17084-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="17084-382">Jeśli jeszcze nie utworzono obszaru roboczego uczenia maszynowego, zobacz [Utwórz obszar roboczy usługi Azure ML](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="17084-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="17084-383">wprowadzenie do usługi Azure Machine Learning tooget zobacz [co to jest Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="17084-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="17084-384">Zaloguj się za[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="17084-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="17084-385">Strona główna Studio Hello zawiera wiele informacji, wideo, samouczki, toohello łącza odwołania moduły i innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="17084-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="17084-386">Aby uzyskać więcej informacji na temat usługi Azure Machine Learning, zapoznaj się hello [Centrum dokumentacji uczenia maszynowego Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="17084-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="17084-387">Eksperyment typowe szkolenia składa się z hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="17084-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="17084-388">Utwórz **+ nowy** eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="17084-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="17084-389">Pobierz dane hello do uczenia Maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="17084-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="17084-390">Wstępnie przetworzyć, transformacji i manipulować danymi hello, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="17084-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="17084-391">Generowanie funkcji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="17084-391">Generate features as needed.</span></span>
5. <span data-ttu-id="17084-392">Podział danych hello na zestawy szkoleniowe / / sprawdzanie poprawności danych (lub mieć osobne zestawy danych dla każdego).</span><span class="sxs-lookup"><span data-stu-id="17084-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="17084-393">Wybierz co najmniej jeden z algorytmów w zależności od hello learning problem toosolve uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="17084-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="17084-394">Przykład klasyfikacji binarnej, wieloklasowej klasyfikacji, regresji.</span><span class="sxs-lookup"><span data-stu-id="17084-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="17084-395">Szkolenie co najmniej jednego modelu przy użyciu zestawu danych szkoleniowych hello.</span><span class="sxs-lookup"><span data-stu-id="17084-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="17084-396">Wynik przy użyciu modeli przeszkolone hello weryfikacji hello w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="17084-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="17084-397">Należy ocenić hello modele toocompute hello odpowiednich metryki dla hello uczenia problem.</span><span class="sxs-lookup"><span data-stu-id="17084-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="17084-398">Dopasuj hello modele i wybierz hello najlepsze toodeploy modelu.</span><span class="sxs-lookup"><span data-stu-id="17084-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="17084-399">W tym ćwiczeniu firma Microsoft ma już przedstawione odtwarzane hello danych w usłudze SQL Data Warehouse i na tooingest rozmiar próbki hello w uczenie Maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="17084-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="17084-400">Oto hello procedury toobuild co najmniej jeden modeli prognozowania hello:</span><span class="sxs-lookup"><span data-stu-id="17084-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="17084-401">Pobierz dane hello do uczenia Maszynowego Azure przy użyciu hello [importowanie danych] [ import-data] modułu dostępne w hello **danych wejściowych i wyjściowych** sekcji.</span><span class="sxs-lookup"><span data-stu-id="17084-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="17084-402">Aby uzyskać więcej informacji, zobacz hello [i zaimportuj dane] [ import-data] strony odwołanie do modułu.</span><span class="sxs-lookup"><span data-stu-id="17084-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Uczenie Maszynowe Azure i zaimportuj dane][17]
2. <span data-ttu-id="17084-404">Wybierz **bazy danych SQL Azure** jako hello **źródła danych** w hello **właściwości** panelu.</span><span class="sxs-lookup"><span data-stu-id="17084-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="17084-405">Wprowadź nazwę DNS bazy danych hello w hello **nazwę serwera bazy danych** pola.</span><span class="sxs-lookup"><span data-stu-id="17084-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="17084-406">Format:`tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="17084-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="17084-407">Wprowadź hello **Nazwa bazy danych** w hello odpowiednie pole.</span><span class="sxs-lookup"><span data-stu-id="17084-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="17084-408">Wprowadź hello *nazwa użytkownika SQL* w hello **nazwę konta użytkownika serwera**i hello *hasło* w hello **hasło konta użytkownika serwera**.</span><span class="sxs-lookup"><span data-stu-id="17084-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="17084-409">Sprawdź hello **dowolny certyfikat serwera Zaakceptuj** opcji.</span><span class="sxs-lookup"><span data-stu-id="17084-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="17084-410">W hello **zapytanie bazy danych** edytować obszaru tekstu, Wklej zapytanie hello wyciąg konieczne hello pola (w tym wszystkie pola obliczane takich jak etykiety hello) bazy danych i w dół przykłady hello danych toohello potrzeby próbkowania.</span><span class="sxs-lookup"><span data-stu-id="17084-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="17084-411">Przykładem eksperyment klasyfikacji binarnej odczytywanie danych bezpośrednio z bazy danych usługi SQL Data Warehouse hello jest hello rysunku poniżej (Pamiętaj tooreplace hello tabeli nazwy nyctaxi_trip i nyctaxi_fare przez schemat hello nazwy i hello tabeli nazwy używane w sieci Przewodnik).</span><span class="sxs-lookup"><span data-stu-id="17084-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="17084-412">Podobne eksperymenty można utworzyć dla wieloklasowej klasyfikacji i regresji problemów.</span><span class="sxs-lookup"><span data-stu-id="17084-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure ML pociągu][10]

> [!IMPORTANT]
> <span data-ttu-id="17084-414">W hello modelowania wyodrębniania danych i pobierania próbek zapytania przykłady podane w poprzednich sekcjach **wszystkich etykiet ćwiczeń modelowania hello trzech znajdują się w zapytaniu hello**.</span><span class="sxs-lookup"><span data-stu-id="17084-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="17084-415">Ważnym krokiem (wymagane) w każdym hello modelowania ćwiczenia jest zbyt**wykluczyć** hello niepotrzebnych etykiety hello innych dwa problemy oraz wszelkie inne **target przecieki**.</span><span class="sxs-lookup"><span data-stu-id="17084-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="17084-416">Na przykład, korzystając z klasyfikacji binarnej, użyj etykiety hello **Przechylony** i wykluczyć pola hello **Porada\_klasy**, **Porada\_kwota**, i **całkowita\_kwota**.</span><span class="sxs-lookup"><span data-stu-id="17084-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="17084-417">Hello te ostatnie są kupowane przecieki docelowy one zakłada Porada hello.</span><span class="sxs-lookup"><span data-stu-id="17084-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="17084-418">tooexclude wszystkie zbędne kolumny lub przecieki docelowych, można użyć hello [Select Columns in Dataset] [ select-columns] modułu lub hello [edytowanie metadanych] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="17084-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="17084-419">Aby uzyskać więcej informacji, zobacz [Select Columns in Dataset] [ select-columns] i [edytowanie metadanych] [ edit-metadata] odwołania stron.</span><span class="sxs-lookup"><span data-stu-id="17084-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="17084-420"><a name="mldeploy"></a>Wdrażanie modeli w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="17084-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="17084-421">Gdy model jest gotowy, łatwo można go wdrożyć jako usługę sieci web bezpośrednio z hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="17084-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="17084-422">Aby uzyskać więcej informacji na temat wdrażania usług sieci web uczenie Maszynowe Azure, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="17084-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="17084-423">toodeploy nową usługę sieci web, musisz:</span><span class="sxs-lookup"><span data-stu-id="17084-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="17084-424">Tworzenie eksperymentu oceniania.</span><span class="sxs-lookup"><span data-stu-id="17084-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="17084-425">Wdrażanie usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="17084-425">Deploy hello web service.</span></span>

<span data-ttu-id="17084-426">toocreate oceniania Poeksperymentuj z **Zakończono** szkolenia eksperyment, kliknij przycisk **utworzyć OCENIANIA EKSPERYMENTU** hello dolnym pasku akcji.</span><span class="sxs-lookup"><span data-stu-id="17084-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Ocenianie przez usługę Azure][18]

<span data-ttu-id="17084-428">Usługa Azure Machine Learning podejmie toocreate eksperyment oceniania na podstawie składników hello eksperyment uczenia hello.</span><span class="sxs-lookup"><span data-stu-id="17084-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="17084-429">W szczególności będzie:</span><span class="sxs-lookup"><span data-stu-id="17084-429">In particular, it will:</span></span>

1. <span data-ttu-id="17084-430">Zapisz hello uczonego modelu i usuwanie modułów uczenia modelu hello.</span><span class="sxs-lookup"><span data-stu-id="17084-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="17084-431">Zidentyfikuj logicznych **port wejściowy** toorepresent hello oczekiwano schemat danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="17084-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="17084-432">Zidentyfikuj logicznych **output portu** schematem wyjściowym toorepresent hello oczekiwanego sieci web usługi.</span><span class="sxs-lookup"><span data-stu-id="17084-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="17084-433">Po utworzeniu hello oceniania eksperymentu, zapoznaj się z nim i upewnij się, Dopasuj zależnie od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="17084-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="17084-434">Typowy korekty jest wejściowy zestaw danych tooreplace hello i/lub zapytanie z taki, który wyklucza pola etykiety, jak te nie będą dostępne, gdy jest wywoływana hello usługi.</span><span class="sxs-lookup"><span data-stu-id="17084-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="17084-435">Istnieje również wprowadzenia hello o rozmiarze hello tooreduce dobrym rozwiązaniem tooa zestawu danych i/lub zapytania kilka rekordów, schemat danych wejściowych hello wystarczającego tooindicate.</span><span class="sxs-lookup"><span data-stu-id="17084-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="17084-436">Port wyjściowy hello, jest typowe tooexclude wszystkie pola i zawierać wyłącznie hello **oceniane etykiety** i **wynik prawdopodobieństwa** w danych wyjściowych za pomocą hello hello [Select Columns in Dataset ] [ select-columns] modułu.</span><span class="sxs-lookup"><span data-stu-id="17084-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="17084-437">Przykładowe oceniania eksperymentu znajduje się w hello na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="17084-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="17084-438">Toodeploy, gdy będzie gotowe kliknij hello **OPUBLIKOWAĆ usługi sieci WEB** przycisk hello dolnym pasku akcji.</span><span class="sxs-lookup"><span data-stu-id="17084-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Publikowanie Azure ML][11]

## <a name="summary"></a><span data-ttu-id="17084-440">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="17084-440">Summary</span></span>
<span data-ttu-id="17084-441">toorecap co możemy to zostało zrobione w tym samouczku wskazówki, zostały utworzone środowisku nauki danych Azure doświadczenie z dużego zestawu danych publiczne, biorąc go za pośrednictwem hello proces nauki danych zespołu, wszystkie sposób hello szkolenia toomodel pozyskiwania danych, a następnie Wdrażanie toohello usługi sieci web uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="17084-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="17084-442">Informacje o licencji</span><span class="sxs-lookup"><span data-stu-id="17084-442">License information</span></span>
<span data-ttu-id="17084-443">Ten przewodnik próbki i jego towarzyszące IPython notebook(s) i skrypty są udostępniane przez firmę Microsoft hello MIT licencji.</span><span class="sxs-lookup"><span data-stu-id="17084-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="17084-444">Sprawdź plik LICENSE.txt hello w katalogu hello hello przykładowy kod w serwisie GitHub więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="17084-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="17084-445">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="17084-445">References</span></span>
<span data-ttu-id="17084-446">• [Andrés Monroy taksówki NYC rund stronę pobierania](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="17084-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="17084-447">• [FOILing NYC taksówki podróży danych przez Krzysztof Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="17084-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="17084-448">• [Taksówki NYC i Limousine Komisji badań i statystyki](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="17084-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
