---
title: "aaaBuild i wdrażanie modelu uczenia maszynowego przy użyciu programu SQL Server na maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: Proces zaawansowane metody analizy i technologii w akcji
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="59a60-103">Hello proces nauki danych zespołu w działaniu: przy użyciu programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="59a60-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="59a60-104">W tym samouczku opisano proces hello tworzenie i wdrażanie modelu uczenia maszynowego przy użyciu programu SQL Server i zestawu danych publicznie dostępnych — Witaj [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="59a60-105">procedury Hello następuje nauki standardowych danych przepływu pracy: pozyskiwania i eksplorować dane hello, opracowywać learning toofacilitate funkcje, a następnie tworzenia i wdrażania modelu.</span><span class="sxs-lookup"><span data-stu-id="59a60-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="59a60-106"><a name="dataset"></a>Taksówki NYC podróży opis zestawu danych</span><span class="sxs-lookup"><span data-stu-id="59a60-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="59a60-107">Hello danych podróży taksówki NYC około 20GB skompresowanego plików CSV (~ 48GB nieskompresowane), składającej się z więcej niż 173 milionów poszczególnych podróży i hello cen w klasie ekonomicznej płatnej w odniesieniu do każdej podróży.</span><span class="sxs-lookup"><span data-stu-id="59a60-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="59a60-108">Każdy rekord podróży obejmuje hello odbiór i przyjmowania lokalizacji i czasu, numer licencji hack anonimowe (sterownik) i numer Medalionu (taksówki jego unikatowy identyfikator).</span><span class="sxs-lookup"><span data-stu-id="59a60-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="59a60-109">Hello danych obejmuje wszystkie rund w roku hello 2013 i jest dostępne w powitania po dwóch zestawów danych dla każdego miesiąca:</span><span class="sxs-lookup"><span data-stu-id="59a60-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="59a60-110">Witaj "trip_data" CSV zawiera szczegóły podróży, takie jak liczba pasażerów, pobranie i punkty dropoff czas trwania podróży i długość podróży.</span><span class="sxs-lookup"><span data-stu-id="59a60-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="59a60-111">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="59a60-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="59a60-112">Witaj "trip_fare" CSV zawiera szczegółowe informacje o klasie hello za każdym razem, takie jak typ płatności, kwota taryfy przeciążenia i podatków, porady i przejazd i Suma hello płatnej.</span><span class="sxs-lookup"><span data-stu-id="59a60-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="59a60-113">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="59a60-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="59a60-114">Hello unikatowy kluczy toojoin podróży\_danych i podróży\_taryfy składa się z pola hello: Medalionu, hack\_licencji i pobrania\_daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="59a60-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="59a60-115"><a name="mltasks"></a>Przykłady prognozowania zadań</span><span class="sxs-lookup"><span data-stu-id="59a60-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="59a60-116">Firma Microsoft będzie sformułować trzy problemów prognozowania oparte na powitania *Porada\_kwota*, to znaczy:</span><span class="sxs-lookup"><span data-stu-id="59a60-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="59a60-117">Klasyfikacji binarnej: prognozowania, czy etykietki został płatnej podróży, tj. *Porada\_kwota* większą niż $0 jest przykład dodatnią, podczas gdy *Porada\_kwota* $ 0 jest ujemny przykład.</span><span class="sxs-lookup"><span data-stu-id="59a60-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="59a60-118">Wieloklasowej klasyfikacji: zakres hello toopredict porady uregulowaniu płatności hello podróży.</span><span class="sxs-lookup"><span data-stu-id="59a60-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="59a60-119">Możemy podzielić hello *Porada\_kwota* do pięciu bins lub klasy:</span><span class="sxs-lookup"><span data-stu-id="59a60-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="59a60-120">Zadanie regresji: toopredict hello ilość Porada płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="59a60-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="59a60-121"><a name="setup"></a>Definiowanie środowiska nauki danych Azure hello zaawansowana analityka</span><span class="sxs-lookup"><span data-stu-id="59a60-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="59a60-122">Jak widać w hello [Planowanie środowiska Your](machine-learning-data-science-plan-your-environment.md) przewodnik, istnieje kilka opcji toowork z zestawem danych rund taksówki NYC hello na platformie Azure:</span><span class="sxs-lookup"><span data-stu-id="59a60-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="59a60-123">Praca z hello danych w obiektach blob Azure, a następnie modelu w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="59a60-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="59a60-124">Ładowanie danych hello do bazy danych programu SQL Server, a następnie modelu w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="59a60-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="59a60-125">W tym samouczku przedstawiono importowania zbiorczego równoległych hello tooa danych programu SQL Server, Eksploracja danych, funkcja inżynierii i w dół próbkowania przy użyciu programu SQL Server Management Studio, a także za pomocą notesu IPython.</span><span class="sxs-lookup"><span data-stu-id="59a60-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="59a60-126">[Przykładowe skrypty](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) i [notesów IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) są udostępniane w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="59a60-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="59a60-127">Przykładowe IPython notesu toowork hello danymi w obiektach blob Azure jest również dostępna w hello tej samej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="59a60-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="59a60-128">tooset Twojego środowiska nauki danych Azure:</span><span class="sxs-lookup"><span data-stu-id="59a60-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="59a60-129">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="59a60-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="59a60-130">Utwórz obszar roboczy usługi Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="59a60-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="59a60-131">[Udostępnianie danych maszyny wirtualnej nauki](machine-learning-data-science-setup-sql-server-virtual-machine.md), zapewniające programu SQL Server i serwer IPython notesu.</span><span class="sxs-lookup"><span data-stu-id="59a60-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="59a60-132">Hello przykładowe skrypty i notebooki IPython będzie maszyny wirtualnej nauki danych tooyour pobrane podczas procesu konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="59a60-133">Po zakończeniu hello skryptu poinstalacyjnego maszyny Wirtualnej, przykłady hello będą biblioteki dokumentów maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="59a60-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="59a60-134">Przykładowe skrypty:`C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="59a60-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="59a60-135">Przykładowe IPython notesów:`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="59a60-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="59a60-136">gdzie `<user_name>` jest nazwą logowania systemu Windows maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="59a60-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="59a60-137">Odnoszą się foldery próbki toohello jako **przykładowe skrypty** i **notesów IPython próbki**.</span><span class="sxs-lookup"><span data-stu-id="59a60-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="59a60-138">Na podstawie hello rozmiaru zestawu danych, lokalizacja źródła danych i hello wybranego celu Azure środowisko, w tym scenariuszu jest podobne zbyt[scenariusza \#5: dużego zestawu danych w lokalnych plikach, docelowa programu SQL Server w maszynie Wirtualnej platformy Azure](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="59a60-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="59a60-139"><a name="getdata"></a>Pobierz hello danych ze źródła publiczny</span><span class="sxs-lookup"><span data-stu-id="59a60-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="59a60-140">tooget hello [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych z lokalizacji publicznej, możesz użyć dowolnej z metod hello opisanego w [tooand przenoszenia danych z magazynu obiektów Blob Azure](machine-learning-data-science-move-azure-blob.md) toocopy hello tooyour danych nowej maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="59a60-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="59a60-141">dane hello toocopy przy użyciu narzędzia AzCopy:</span><span class="sxs-lookup"><span data-stu-id="59a60-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="59a60-142">Zaloguj się za tooyour maszyny wirtualnej (VM)</span><span class="sxs-lookup"><span data-stu-id="59a60-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="59a60-143">Utwórz nowy katalog dysku danych hello maszyny Wirtualnej (Uwaga: nie używaj hello tymczasowego dysk, który jest dostarczany z hello maszyny Wirtualnej jako dysk danych).</span><span class="sxs-lookup"><span data-stu-id="59a60-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="59a60-144">W oknie wiersza polecenia Uruchom hello następującego wiersza polecenia Azcopy, zastępując < path_to_data_folder > folderu danych utworzone w (2):</span><span class="sxs-lookup"><span data-stu-id="59a60-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="59a60-145">Po ukończeniu hello AzCopy łącznie 24 zip plików CSV (12 podczas podróży\_danych i 12 podczas podróży\_taryfy) powinny się znajdować w folderze danych hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="59a60-146">Rozpakowywanie plików hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="59a60-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="59a60-147">Uwaga hello folder, w którym są przechowywane jako nieskompresowane hello pliki.</span><span class="sxs-lookup"><span data-stu-id="59a60-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="59a60-148">Ten folder będzie hello tooas określonego < ścieżka\_do\_danych\_pliki\>.</span><span class="sxs-lookup"><span data-stu-id="59a60-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="59a60-149"><a name="dbload"></a>Zbiorcze importowanie danych do bazy danych serwera SQL</span><span class="sxs-lookup"><span data-stu-id="59a60-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="59a60-150">Witaj ładowania/transfer dużych ilości danych tooan SQL database i kolejne zapytania można poprawić wydajność przy użyciu *partycjonowane tabele i widoki*.</span><span class="sxs-lookup"><span data-stu-id="59a60-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="59a60-151">W tej sekcji możemy wykonaj instrukcje hello opisanego w [równoległych zbiorczego danych importu za pomocą SQL tabel partycji](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate nowe dane hello bazy danych i obciążenia do partycjonowane tabele równolegle.</span><span class="sxs-lookup"><span data-stu-id="59a60-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="59a60-152">Po zalogowaniu tooyour maszyny Wirtualnej, należy uruchomić **programu SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="59a60-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="59a60-153">Połącz przy użyciu uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="59a60-153">Connect using Windows Authentication.</span></span>
   
    ![Połącz SSMS][12]
3. <span data-ttu-id="59a60-155">Jeśli jeszcze nie masz zmienić tryb uwierzytelniania programu SQL Server hello i utworzyć nowego użytkownika logowania SQL, otwórz plik skryptu hello o nazwie **zmienić\_auth.sql** w hello **przykładowe skrypty** folderu.</span><span class="sxs-lookup"><span data-stu-id="59a60-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="59a60-156">Zmień hello domyślna nazwa użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="59a60-156">Change hello  default user name and password.</span></span> <span data-ttu-id="59a60-157">Kliknij przycisk **! Wykonanie** hello narzędzi toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="59a60-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![Uruchom skrypt][13]
4. <span data-ttu-id="59a60-159">Sprawdź i/lub zmienić hello domyślnej bazy danych i dziennika folderów tooensure nowo utworzony baz danych będą przechowywane na dysku danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="59a60-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="59a60-160">Hello obraz maszyny Wirtualnej programu SQL Server, który jest zoptymalizowany pod kątem obciążeń strumienia jest wstępnie skonfigurowana z dyskami danych i dziennika.</span><span class="sxs-lookup"><span data-stu-id="59a60-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="59a60-161">Jeśli maszyna wirtualna nie zawiera dysk z danymi i dodać nowe wirtualnych dysków twardych podczas hello procesu konfiguracji maszyny Wirtualnej, zmień hello domyślnych folderów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="59a60-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="59a60-162">Kliknij prawym przyciskiem myszy nazwę serwera SQL hello hello lewego panelu i kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="59a60-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![Właściwości serwera SQL][14]
   * <span data-ttu-id="59a60-164">Wybierz **ustawienia bazy danych** z hello **wybierz stronę** listy toohello lewej.</span><span class="sxs-lookup"><span data-stu-id="59a60-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="59a60-165">Sprawdź i/lub zmienić hello **bazy danych domyślne lokalizacje** toohello **dysku danych** lokalizacje wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="59a60-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="59a60-166">Jest to, gdzie nowe bazy danych znajdują się Jeśli utworzone za pomocą hello domyślne ustawienia lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="59a60-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![Domyślne ustawienia bazy danych SQL][15]  
5. <span data-ttu-id="59a60-168">toocreate nową bazę danych i zestaw grup plików toohold hello partycjonowane tabele, otwórz hello przykładowy skrypt **utworzyć\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="59a60-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="59a60-169">skrypt Hello spowoduje utworzenie nowej bazy danych o nazwie **TaxiNYC** i 12 grup plików w hello domyślnej lokalizacji danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="59a60-170">Każda grupa plików będą przechowywane miesiąc podróży\_danych i podróży\_taryfy danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="59a60-171">W razie potrzeby zmodyfikuj hello Nazwa bazy danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="59a60-172">Kliknij przycisk **! Wykonanie** toorun hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="59a60-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="59a60-173">Następnie należy utworzyć dwie tabele partycji, jeden dla podróży hello\_danych i drugi dla podróży hello\_klasie.</span><span class="sxs-lookup"><span data-stu-id="59a60-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="59a60-174">Otwórz hello przykładowy skrypt **utworzyć\_partycjonowanej\_table.sql**, który będzie:</span><span class="sxs-lookup"><span data-stu-id="59a60-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="59a60-175">Tworzenie partycji funkcji toosplit hello danych według miesięcy.</span><span class="sxs-lookup"><span data-stu-id="59a60-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="59a60-176">Utwórz toomap schematu partycji co miesiąc danych tooa innej grupy plików.</span><span class="sxs-lookup"><span data-stu-id="59a60-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="59a60-177">Utwórz dwa schemat partycji zamapowanych toohello partycjonowane tabele: **nyctaxi\_podróży** będą przechowywane podróży hello\_danych i **nyctaxi\_taryfy** będą przechowywane hello podróży \_taryfy danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="59a60-178">Kliknij przycisk **! Wykonanie** toorun hello skryptu i tworzenie tabel hello podzielona na partycje.</span><span class="sxs-lookup"><span data-stu-id="59a60-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="59a60-179">W hello **przykładowe skrypty** folderu, istnieją dwie przykładowe skrypty programu PowerShell dostarczane toodemonstrate Importy zbiorcze równoległych tabel serwera tooSQL danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="59a60-180">**Narzędzie BCP\_równoległych\_generic.ps1** jest skrypt rodzajowy tooparallel zbiorczego importowania danych do tabeli.</span><span class="sxs-lookup"><span data-stu-id="59a60-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="59a60-181">Modyfikuj tego skryptu tooset hello dane wejściowe i obiekt docelowy zmienne wskazane hello wiersze komentarzy w skrypcie hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="59a60-182">**Narzędzie BCP\_równoległych\_nyctaxi.ps1** jest wstępnie skonfigurowana wersja skrypt rodzajowy hello i mogą być używane tootooload obu tabel danych rund taksówki NYC hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="59a60-183">Powitania kliknij prawym przyciskiem myszy **bcp\_równoległych\_nyctaxi.ps1** kliknij nazwę skryptu wraz z **Edytuj** tooopen go w programie PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59a60-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="59a60-184">Hello Przejrzyj ustawienia zmiennych i modyfikować zgodnie z tooyour wybranej nazwie bazy danych, folderu danych wejściowych, folder docelowy dziennika i ścieżki toohello Przykładowy format plików **nyctaxi_trip.xml** i **nyctaxi\_ fare.XML** (w hello **przykładowe skrypty** folderu).</span><span class="sxs-lookup"><span data-stu-id="59a60-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![Zbiorczego importowania danych][16]
   
    <span data-ttu-id="59a60-186">Można również wybrać tryb uwierzytelniania hello, domyślnym jest uwierzytelnianie systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="59a60-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="59a60-187">Kliknij strzałkę hello zielony w hello toorun paska narzędzi.</span><span class="sxs-lookup"><span data-stu-id="59a60-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="59a60-188">skrypt Hello uruchomi 24 operacji importowania zbiorczego w 12 równoległe, dla każdej tabeli partycjonowanej.</span><span class="sxs-lookup"><span data-stu-id="59a60-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="59a60-189">Może monitorować postęp importowania danych hello, otwierając folder dane domyślnego programu SQL Server hello zgodnie z ustaleniami powyżej.</span><span class="sxs-lookup"><span data-stu-id="59a60-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="59a60-190">Raporty skrypt programu PowerShell Hello hello godziny rozpoczęcia i zakończenia.</span><span class="sxs-lookup"><span data-stu-id="59a60-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="59a60-191">Jeśli wszystkie masowe Importy ukończone, zgłaszane hello godzina zakończenia.</span><span class="sxs-lookup"><span data-stu-id="59a60-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="59a60-192">Sprawdź hello docelowego dziennika folderu tooverify, który importuje zbiorczego hello zostały pomyślnie, tj. żadne błędy nie zgłoszone w folderze dziennika docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="59a60-193">Baza danych jest teraz gotowe do eksploracji, funkcja inżynieryjne i innych czynności.</span><span class="sxs-lookup"><span data-stu-id="59a60-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="59a60-194">Ponieważ tabele hello są podzielone na partycje według toohello **podnoszenia\_datetime** pola zapytania, które obejmują **podnoszenia\_daty/godziny** warunków w hello  **GDZIE** klauzuli będą korzystać z hello schemat partycji.</span><span class="sxs-lookup"><span data-stu-id="59a60-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="59a60-195">W **programu SQL Server Management Studio**, Eksploruj hello podano przykładowy skrypt **próbki\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="59a60-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="59a60-196">toorun żadnego hello przykładowe zapytania, hello wyróżnienie zapytania wierszy a następnie kliknij przycisk **! Wykonanie** hello w pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="59a60-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="59a60-197">Hello rund taksówki NYC danych została załadowana w dwóch oddzielnych tabelach.</span><span class="sxs-lookup"><span data-stu-id="59a60-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="59a60-198">operacji łączenia tooimprove, zdecydowanie zaleca tooindex hello tabel.</span><span class="sxs-lookup"><span data-stu-id="59a60-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="59a60-199">Witaj przykładowy skrypt **utworzyć\_podzielonym na partycje\_index.sql** tworzy indeksy podzielone na partycje klucza złożonego sprzężenia hello **Medalionu, hack\_licencji i pobrania\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="59a60-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="59a60-200"><a name="dbexplore"></a>Eksploracja danych i inżynieria funkcji w programie SQL Server</span><span class="sxs-lookup"><span data-stu-id="59a60-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="59a60-201">Generowanie funkcji i eksploracja danych w tej sekcji zostaną wykonane przez uruchomienie zapytania SQL bezpośrednio w hello **programu SQL Server Management Studio** przy użyciu bazy danych programu SQL Server hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="59a60-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="59a60-202">Przykładowy skrypt o nazwie **próbki\_queries.sql** znajduje się w hello **przykładowe skrypty** folderu.</span><span class="sxs-lookup"><span data-stu-id="59a60-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="59a60-203">Zmodyfikować hello toochange hello bazy danych nazwa skryptu, jeśli jest inny niż domyślny hello: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="59a60-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="59a60-204">W tym ćwiczeniu zostaną wykonane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="59a60-204">In this exercise, we will:</span></span>

* <span data-ttu-id="59a60-205">Połącz za**programu SQL Server Management Studio** przy użyciu uwierzytelnianiu systemu Windows lub uwierzytelniania SQL i hello nazwa logowania SQL i hasło.</span><span class="sxs-lookup"><span data-stu-id="59a60-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="59a60-206">Eksplorowanie danych dystrybucji kilka pól w różnym czasie systemu windows.</span><span class="sxs-lookup"><span data-stu-id="59a60-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="59a60-207">Zbadaj jakości danych hello pól długości i szerokości geograficznej.</span><span class="sxs-lookup"><span data-stu-id="59a60-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="59a60-208">Generowanie etykiet klasyfikacji binarnej i wieloklasowej oparte na powitania **Porada\_kwota**.</span><span class="sxs-lookup"><span data-stu-id="59a60-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="59a60-209">Generowanie funkcji i obliczeń lub porównania odległości podróży.</span><span class="sxs-lookup"><span data-stu-id="59a60-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="59a60-210">Dołącz Witaj dwie tabele i Wyodrębnij losowej próbki, które będzie używane toobuild modeli.</span><span class="sxs-lookup"><span data-stu-id="59a60-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="59a60-211">Gdy są gotowe tooproceed tooAzure uczenia maszynowego, użytkownik może:</span><span class="sxs-lookup"><span data-stu-id="59a60-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="59a60-212">Zapisz hello końcowego SQL kwerendy tooextract i przykładowa hello danych i kopiowania i wklejania hello zapytanie bezpośrednio do [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning, lub</span><span class="sxs-lookup"><span data-stu-id="59a60-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="59a60-213">Utrwalić hello próbkowany i odtworzone danych planujesz toouse modelu Tworzenie nowej bazy danych tabeli i korzystanie z nowej tabeli hello w hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="59a60-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="59a60-214">W tej sekcji zapisze firma Microsoft hello końcowego tooextract i przykładowa hello dane zapytania.</span><span class="sxs-lookup"><span data-stu-id="59a60-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="59a60-215">Druga metoda Hello jest przedstawiona w hello [Eksploracja danych i funkcji inżynieryjnego w notesie IPython](#ipnb) sekcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="59a60-216">Szybkie weryfikacji hello liczby wierszy i kolumn w hello tabel wypełnione wcześniej za pomocą importowania zbiorczego równoległych</span><span class="sxs-lookup"><span data-stu-id="59a60-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="59a60-217">Eksploracja: Podróży dystrybucji przez Medalionu</span><span class="sxs-lookup"><span data-stu-id="59a60-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="59a60-218">W tym przykładzie identyfikuje hello Medalionu (taksówki numery) z więcej niż 100 rund w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="59a60-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="59a60-219">Zapytanie Hello korzystałby z hello na partycje tabeli dostępu, ponieważ należy przygotować przez schemat partycji hello **podnoszenia\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="59a60-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="59a60-220">Badania hello pełnego zestawu danych będzie również używać tabeli partycjonowanej hello i/lub indeksu skanowania.</span><span class="sxs-lookup"><span data-stu-id="59a60-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="59a60-221">Eksploracja: Podróży dystrybucji Medalionu i hack_license</span><span class="sxs-lookup"><span data-stu-id="59a60-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="59a60-222">Oceny jakości danych: Rekordy z geograficzne niepoprawne i/lub szerokość geograficzną Sprawdź</span><span class="sxs-lookup"><span data-stu-id="59a60-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="59a60-223">W tym przykładzie sprawdza, czy hello geograficzne i/lub szerokość geograficzną polach albo zawiera nieprawidłową wartość (stopni w radianach powinna należeć do zakresu od-90 do 90,) lub (0, 0) współrzędnych.</span><span class="sxs-lookup"><span data-stu-id="59a60-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="59a60-224">Eksploracja: Przechylony vs. Nie Przechylony rund dystrybucji</span><span class="sxs-lookup"><span data-stu-id="59a60-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="59a60-225">W tym przykładzie znajduje hello Liczba podróży, które zostały Przechylony a nie Przechylony w danym momencie okres (lub w hello pełnego zestawu danych jeśli obejmujące cały rok hello).</span><span class="sxs-lookup"><span data-stu-id="59a60-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="59a60-226">Tej dystrybucji odzwierciedla toobe dystrybucji binarne etykiety hello później użyć do modelowania klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="59a60-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="59a60-227">Eksploracja: Porada dystrybucji klasy/zakresu</span><span class="sxs-lookup"><span data-stu-id="59a60-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="59a60-228">W tym przykładzie oblicza dystrybucji hello Porada zakresów w danym momencie okres (lub w hello pełnego zestawu danych jeśli obejmujące cały rok hello).</span><span class="sxs-lookup"><span data-stu-id="59a60-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="59a60-229">Jest to dystrybucji hello hello etykiety klas, które będą później używane do modelowania wieloklasowej klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="59a60-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="59a60-230">Eksploracja: Obliczania i porównać odległość podróży</span><span class="sxs-lookup"><span data-stu-id="59a60-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="59a60-231">W tym przykładzie konwertuje hello odbiór i przyjmowania geograficzne i współrzędne geograficzne tooSQL punktów, oblicza odległość podróży hello przy użyciu różnicę punktów geograficzne SQL i zwraca losowej próbki hello wyniki do porównania.</span><span class="sxs-lookup"><span data-stu-id="59a60-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="59a60-232">przykład Witaj ogranicza wyniki hello toovalid koordynuje tylko przy użyciu objętych wcześniej hello danych jakości oceny zapytania.</span><span class="sxs-lookup"><span data-stu-id="59a60-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="59a60-233">Funkcja Engineering w zapytania SQL</span><span class="sxs-lookup"><span data-stu-id="59a60-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="59a60-234">Hello etykiety generowania geograficzne konwersji eksploracji zapytań i może być również używane toogenerate etykiety/funkcje przez usunięcie hello zliczania części.</span><span class="sxs-lookup"><span data-stu-id="59a60-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="59a60-235">Dodatkową cechą engineering SQL przykłady znajdują się w hello [Eksploracja danych i funkcji inżynieryjnego w notesie IPython](#ipnb) sekcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="59a60-236">Jest bardziej wydajne toorun hello funkcji generowania zapytania na powitania pełnego zestawu danych lub za pomocą zapytania SQL, które uruchomione bezpośrednio w wystąpieniu bazy danych programu SQL Server hello duży podzbiór.</span><span class="sxs-lookup"><span data-stu-id="59a60-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="59a60-237">Witaj zapytania mogą być wykonywane w **programu SQL Server Management Studio**, notesu IPython lub dowolnego narzędzia/Środowisko deweloperskie, które mogą uzyskiwać dostęp do hello bazy danych lokalnie lub zdalnie.</span><span class="sxs-lookup"><span data-stu-id="59a60-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="59a60-238">Przygotowywanie danych do konstruowania modelu</span><span class="sxs-lookup"><span data-stu-id="59a60-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="59a60-239">Witaj następujące zapytanie sprzęga hello **nyctaxi\_podróży** i **nyctaxi\_taryfy** tabel, generuje etykiety klasyfikacji binarnej **Przechylony**, etykiety klasyfikacji wielu klasy **Porada\_klasy**i wyodrębnia 1% losowej próbki z hello pełnego dołączonego do zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="59a60-240">To zapytanie może skopiować następnie wkleić bezpośrednio w hello [Azure Machine Learning Studio](https://studio.azureml.net) [i zaimportuj dane] [ import-data] modułu dla wprowadzanie danych bezpośrednio z bazy danych programu SQL Server hello wystąpienie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="59a60-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="59a60-241">Zapytanie Hello wyklucza rekordy z niepoprawne (0, 0) współrzędnych.</span><span class="sxs-lookup"><span data-stu-id="59a60-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="59a60-242"><a name="ipnb"></a>Eksploracja danych i funkcji inżynieryjne w notesie IPython</span><span class="sxs-lookup"><span data-stu-id="59a60-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="59a60-243">W tej sekcji zostaną wykonane Eksplorowanie danych oraz generowanie funkcji za pomocą zarówno Python, jak i SQL zapytań dotyczących bazy danych programu SQL Server hello utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="59a60-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="59a60-244">Przykładowe IPython Notes o nazwie **machine-Learning-data-science-process-sql-story.ipynb** znajduje się w hello **notesów IPython próbki** folderu.</span><span class="sxs-lookup"><span data-stu-id="59a60-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="59a60-245">Ten notes jest również dostępna w [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="59a60-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="59a60-246">Hello zalecane sekwencji podczas pracy z danymi big data jest hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="59a60-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="59a60-247">Odczyt w małej przykładowej hello danych do ramki danych w pamięci.</span><span class="sxs-lookup"><span data-stu-id="59a60-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="59a60-248">Wykonywanie niektórych wizualizacje i eksploracji przy użyciu danych hello próbkowane.</span><span class="sxs-lookup"><span data-stu-id="59a60-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="59a60-249">Wypróbuj engineering funkcji przy użyciu danych hello próbkowane.</span><span class="sxs-lookup"><span data-stu-id="59a60-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="59a60-250">Dla większych Eksploracja danych do manipulowania danymi i funkcji zespołu inżynieryjnego, użyj zapytania SQL tooissue Python bezpośrednio z bazy danych programu SQL Server hello w hello maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59a60-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="59a60-251">Zdecyduj, toouse rozmiar próbki hello do tworzenia modelu uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="59a60-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="59a60-252">Gdy gotowe tooAzure tooproceed uczenia maszynowego, użytkownik może:</span><span class="sxs-lookup"><span data-stu-id="59a60-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="59a60-253">Zapisz hello końcowego SQL kwerendy tooextract i przykładowa hello danych i kopiowania i wklejania hello zapytanie bezpośrednio do [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="59a60-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="59a60-254">Ta metoda jest przedstawiona w hello [tworzenia modeli w usłudze Azure Machine Learning](#mlmodel) sekcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="59a60-255">Zachować hello próbkowany i odtworzone dane planujesz toouse tworzenie w nowej tabeli bazy danych modelu, a następnie użyj nowej tabeli hello w hello [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="59a60-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="59a60-256">Witaj poniżej przedstawiono kilka Eksploracja danych, wizualizacji danych i funkcji inżynierii przykłady.</span><span class="sxs-lookup"><span data-stu-id="59a60-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="59a60-257">Więcej przykładów można znaleźć hello przykładowy SQL IPython Notes w hello **notesów IPython próbki** folderu.</span><span class="sxs-lookup"><span data-stu-id="59a60-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="59a60-258">Inicjowanie poświadczenia bazy danych</span><span class="sxs-lookup"><span data-stu-id="59a60-258">Initialize Database Credentials</span></span>
<span data-ttu-id="59a60-259">Inicjowanie ustawienia połączenia bazy danych w hello następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="59a60-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="59a60-260">Utwórz połączenie z bazą danych</span><span class="sxs-lookup"><span data-stu-id="59a60-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="59a60-261">Raport liczba wierszy i kolumn w tabeli nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="59a60-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="59a60-262">Całkowita liczba wierszy = 173179759</span><span class="sxs-lookup"><span data-stu-id="59a60-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="59a60-263">Łączna liczba kolumn = 14</span><span class="sxs-lookup"><span data-stu-id="59a60-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="59a60-264">Odczyt w przykładowych danych małych z hello bazy danych serwera SQL</span><span class="sxs-lookup"><span data-stu-id="59a60-264">Read-in a small data sample from hello SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="59a60-265">Czas tooread hello Przykładowa tabela jest 6.492000 sekund</span><span class="sxs-lookup"><span data-stu-id="59a60-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="59a60-266">Liczba wierszy i kolumn pobrać = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="59a60-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="59a60-267">Statystyki opisowe</span><span class="sxs-lookup"><span data-stu-id="59a60-267">Descriptive Statistics</span></span>
<span data-ttu-id="59a60-268">Są teraz gotowe tooexplore hello próbce danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="59a60-269">Możemy zaczynać się patrzeć Statystyki opisowe dla hello **podróży\_odległość** (lub innych) pola/pól:</span><span class="sxs-lookup"><span data-stu-id="59a60-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="59a60-270">Wizualizacji: Przykład kreślenia pola</span><span class="sxs-lookup"><span data-stu-id="59a60-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="59a60-271">Następnie przyjrzymy się hello skrzynkowy dla hello podróży odległość toovisualize hello quantiles</span><span class="sxs-lookup"><span data-stu-id="59a60-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Wykreślenia #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="59a60-273">Wizualizacji: Przykład kreślenia dystrybucji</span><span class="sxs-lookup"><span data-stu-id="59a60-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Wykreślenia #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="59a60-275">Wizualizacji: Pasek i powierzchni wiersza</span><span class="sxs-lookup"><span data-stu-id="59a60-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="59a60-276">W tym przykładzie firma Microsoft hello odległość podróży do pięciu bins bin i wizualizację hello binning wyników.</span><span class="sxs-lookup"><span data-stu-id="59a60-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="59a60-277">Firma Microsoft może wykreślenia hello powyżej dystrybucji bin na pasku lub wiersz kreślenia zgodnie z poniższymi instrukcjami</span><span class="sxs-lookup"><span data-stu-id="59a60-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Wykreślenia #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Wykreślenia #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="59a60-280">Wizualizacji: Przykład Scatterplot</span><span class="sxs-lookup"><span data-stu-id="59a60-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="59a60-281">Zostanie przedstawiony jest wykres punktowy między **podróży\_czasu\_w\_s** i **podróży\_odległość** toosee w przypadku dowolnego korelacji</span><span class="sxs-lookup"><span data-stu-id="59a60-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Wykreślenia #6][6]

<span data-ttu-id="59a60-283">Podobnie można sprawdzić hello relacji między **szybkość\_kod** i **podróży\_odległość**.</span><span class="sxs-lookup"><span data-stu-id="59a60-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Wykreślenia #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="59a60-285">Hello podrzędne próbkowania danych SQL</span><span class="sxs-lookup"><span data-stu-id="59a60-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="59a60-286">Podczas przygotowywania danych dla modelu kompilacji w [Azure Machine Learning Studio](https://studio.azureml.net), albo można wyłączyć na powitania **toouse zapytania SQL bezpośrednio w module importu danych hello** lub utrwalić hello odtwarzane i próbkowany danych w nowej tabeli, którego można użyć w hello [i zaimportuj dane] [ import-data] modułu przy użyciu prostego **wybierz * FROM < Twojej\_nowe\_tabeli\_name >**.</span><span class="sxs-lookup"><span data-stu-id="59a60-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="59a60-287">W tej sekcji, który zostanie utworzony nowy hello toohold tabeli próbkowany i odtwarzane danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="59a60-288">Przykład bezpośrednie kwerendy SQL dla tworzenia modelu znajduje się w hello [Eksploracja danych i funkcji inżynieryjnego w programie SQL Server](#dbexplore) sekcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="59a60-289">Utwórz przykładową tabelę i Wypełnij tabele sprzężone hello: % 1.</span><span class="sxs-lookup"><span data-stu-id="59a60-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="59a60-290">Jeśli istnieje porzucić pierwszej tabeli.</span><span class="sxs-lookup"><span data-stu-id="59a60-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="59a60-291">W tej sekcji możemy sprzężone tabele hello **nyctaxi\_podróży** i **nyctaxi\_taryfy**, Wyodrębnij losowej próbki 1%, a utrwalenia hello próbkowany danych w nowej nazwy tabeli  **nyctaxi\_jeden\_procent**:</span><span class="sxs-lookup"><span data-stu-id="59a60-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="59a60-292">Eksploracja danych za pomocą zapytań SQL w notesie IPython</span><span class="sxs-lookup"><span data-stu-id="59a60-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="59a60-293">W tej sekcji możemy Eksplorowanie danych dystrybucji przy użyciu hello danych próbkowany % 1, który jest utrwalona w nowej tabeli hello, utworzone powyżej.</span><span class="sxs-lookup"><span data-stu-id="59a60-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="59a60-294">Należy pamiętać, że podobne eksploracji może zostać wykonane przy użyciu oryginalnego tabel hello, opcjonalnie używając **TABLESAMPLE** toolimit hello eksploracji przykładowa lub ograniczając hello powoduje tooa danego okresu czasu przy użyciu hello **pobrania \_datetime** partycji, jak pokazano na powitania [Eksploracja danych i funkcji inżynieryjnego w programie SQL Server](#dbexplore) sekcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="59a60-295">Eksploracji: Codzienne dystrybucji rund</span><span class="sxs-lookup"><span data-stu-id="59a60-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="59a60-296">Eksploracja: Podróży dystrybucji na Medalionu</span><span class="sxs-lookup"><span data-stu-id="59a60-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="59a60-297">Generowanie funkcji za pomocą zapytań SQL w notesie IPython</span><span class="sxs-lookup"><span data-stu-id="59a60-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="59a60-298">W tej sekcji wygenerujemy nowe etykiety i funkcji bezpośrednio za pomocą zapytania SQL, na tabeli 1% hello utworzyliśmy hello w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="59a60-299">Generowanie etykiety: Generowanie etykiet — klasa</span><span class="sxs-lookup"><span data-stu-id="59a60-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="59a60-300">W hello poniższy przykład firma Microsoft generuje dwa zestawy toouse etykiety dla modelowania:</span><span class="sxs-lookup"><span data-stu-id="59a60-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="59a60-301">Binarny etykiety klasy **Przechylony** (przewidywania, jeśli będzie miał poradę)</span><span class="sxs-lookup"><span data-stu-id="59a60-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="59a60-302">Etykiety wieloklasowej **Porada\_klasy** (przewidywania bin Porada hello lub zakres)</span><span class="sxs-lookup"><span data-stu-id="59a60-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="59a60-303">Inżynieria funkcji: Liczba funkcje dla kolumny podzielone na kategorie</span><span class="sxs-lookup"><span data-stu-id="59a60-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="59a60-304">W tym przykładzie przekształca pole kategorii do pola liczbowego przez zamianę każdej kategorii hello liczba ich wystąpień hello danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="59a60-305">Funkcja Engineering: Bin funkcje dla kolumny liczbowe</span><span class="sxs-lookup"><span data-stu-id="59a60-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="59a60-306">W tym przykładzie przekształca pola numerycznego ciągłe na zakresy istniejących kategorii, tj., Przekształcanie pola numerycznego w pole kategorii.</span><span class="sxs-lookup"><span data-stu-id="59a60-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="59a60-307">Inżynieria funkcji: Wyodrębniania dziesiętną szerokości geograficznej/długości geograficznej lokalizacji funkcji</span><span class="sxs-lookup"><span data-stu-id="59a60-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="59a60-308">W tym przykładzie dzieli hello dziesiętną reprezentację szerokości geograficznej i/lub długość pola na wielu pól region z różnych szczegółowości takich, jak kraj, Miasto, miejscowość, blok itp. Należy pamiętać, że nowe pola geograficznie hello nie są mapowane tooactual lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="59a60-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="59a60-309">Informacje dotyczące mapowania lokalizacji geocode znajdują się w temacie [usług REST mapy usługi Bing](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="59a60-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="59a60-310">Sprawdź hello końcowego formę hello featurized tabeli</span><span class="sxs-lookup"><span data-stu-id="59a60-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="59a60-311">Firma Microsoft są teraz gotowe tooproceed toomodel tworzenia i wdrażania modelu w [usługi Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="59a60-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="59a60-312">dane Hello jest gotowy do żadnego z wymienionych wcześniej, to znaczy problemów prognozowania hello:</span><span class="sxs-lookup"><span data-stu-id="59a60-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="59a60-313">Klasyfikacji binarnej: toopredict czy poradę został płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="59a60-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="59a60-314">Wieloklasowej klasyfikacji: zakres hello toopredict porady płatnej, zgodnie z uprzednio zdefiniowanej klasy toohello.</span><span class="sxs-lookup"><span data-stu-id="59a60-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="59a60-315">Zadanie regresji: toopredict hello ilość Porada płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="59a60-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="59a60-316"><a name="mlmodel"></a>Tworzenie modeli w uczenie maszynowe Azure</span><span class="sxs-lookup"><span data-stu-id="59a60-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="59a60-317">toobegin hello modelowania ćwiczeniu logowania obszaru roboczego uczenia maszynowego Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="59a60-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="59a60-318">Jeśli jeszcze nie utworzono obszaru roboczego uczenia maszynowego, zobacz [Utwórz obszar roboczy usługi Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="59a60-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="59a60-319">wprowadzenie do usługi Azure Machine Learning tooget zobacz [co to jest Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="59a60-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="59a60-320">Zaloguj się za[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="59a60-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="59a60-321">Strona główna Studio Hello zawiera wiele informacji, wideo, samouczki, toohello łącza odwołania moduły i innych zasobów.</span><span class="sxs-lookup"><span data-stu-id="59a60-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="59a60-322">Aby uzyskać więcej informacji na temat usługi Azure Machine Learning, zapoznaj się hello [Centrum dokumentacji uczenia maszynowego Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="59a60-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="59a60-323">Eksperyment typowe szkolenia składa się z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="59a60-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="59a60-324">Utwórz **+ nowy** eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="59a60-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="59a60-325">Pobierz tooAzure danych hello uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="59a60-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="59a60-326">Wstępnie przetworzyć, transformacji i manipulować danymi hello, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="59a60-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="59a60-327">Generowanie funkcji zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="59a60-327">Generate features as needed.</span></span>
5. <span data-ttu-id="59a60-328">Podział danych hello na zestawy szkoleniowe / / sprawdzanie poprawności danych (lub mieć osobne zestawy danych dla każdego).</span><span class="sxs-lookup"><span data-stu-id="59a60-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="59a60-329">Wybierz co najmniej jeden z algorytmów w zależności od hello learning problem toosolve uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="59a60-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="59a60-330">Przykład klasyfikacji binarnej, wieloklasowej klasyfikacji, regresji.</span><span class="sxs-lookup"><span data-stu-id="59a60-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="59a60-331">Szkolenie co najmniej jednego modelu przy użyciu zestawu danych szkoleniowych hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="59a60-332">Wynik przy użyciu modeli przeszkolone hello weryfikacji hello w zestawie danych.</span><span class="sxs-lookup"><span data-stu-id="59a60-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="59a60-333">Należy ocenić hello modele toocompute hello odpowiednich metryki dla hello uczenia problem.</span><span class="sxs-lookup"><span data-stu-id="59a60-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="59a60-334">Dopasuj hello modele i wybierz hello najlepsze toodeploy modelu.</span><span class="sxs-lookup"><span data-stu-id="59a60-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="59a60-335">W tym ćwiczeniu mamy już przedstawione i odtwarzane hello danych w programie SQL Server i na tooingest rozmiar próbki hello w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="59a60-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="59a60-336">toobuild co najmniej jeden modeli prognozowania hello zdecydowaliśmy:</span><span class="sxs-lookup"><span data-stu-id="59a60-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="59a60-337">Pobierz tooAzure danych hello uczenia maszynowego przy użyciu hello [i zaimportuj dane] [ import-data] modułu dostępne w hello **danych wejściowych i wyjściowych** sekcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="59a60-338">Aby uzyskać więcej informacji, zobacz hello [i zaimportuj dane] [ import-data] strony odwołanie do modułu.</span><span class="sxs-lookup"><span data-stu-id="59a60-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Uczenie maszynowe Azure i zaimportuj dane][17]
2. <span data-ttu-id="59a60-340">Wybierz **bazy danych SQL Azure** jako hello **źródła danych** w hello **właściwości** panelu.</span><span class="sxs-lookup"><span data-stu-id="59a60-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="59a60-341">Wprowadź nazwę DNS bazy danych hello w hello **nazwę serwera bazy danych** pola.</span><span class="sxs-lookup"><span data-stu-id="59a60-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="59a60-342">Format:`tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="59a60-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="59a60-343">Wprowadź hello **Nazwa bazy danych** w hello odpowiednie pole.</span><span class="sxs-lookup"><span data-stu-id="59a60-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="59a60-344">Wprowadź hello **nazwa użytkownika SQL** w hello ** nazwa_serwera aqccount użytkownika i hasło hello w hello **hasło konta użytkownika serwera**.</span><span class="sxs-lookup"><span data-stu-id="59a60-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="59a60-345">Sprawdź **dowolny certyfikat serwera Zaakceptuj** opcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="59a60-346">W hello **zapytanie bazy danych** edytować obszaru tekstu, Wklej zapytanie hello wyciąg konieczne hello pola (w tym wszystkie pola obliczane takich jak etykiety hello) bazy danych i w dół przykłady hello danych toohello potrzeby próbkowania.</span><span class="sxs-lookup"><span data-stu-id="59a60-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="59a60-347">Przykład eksperyment klasyfikacji binarnej odczytywanie danych bezpośrednio z bazy danych programu SQL Server hello jest hello na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="59a60-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="59a60-348">Podobne eksperymenty można utworzyć dla wieloklasowej klasyfikacji i regresji problemów.</span><span class="sxs-lookup"><span data-stu-id="59a60-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure Machine Learning pociągu][10]

> [!IMPORTANT]
> <span data-ttu-id="59a60-350">W hello modelowania wyodrębniania danych i pobierania próbek zapytania przykłady podane w poprzednich sekcjach **wszystkich etykiet ćwiczeń modelowania hello trzech znajdują się w zapytaniu hello**.</span><span class="sxs-lookup"><span data-stu-id="59a60-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="59a60-351">Ważnym krokiem (wymagane) w każdym hello modelowania ćwiczenia jest zbyt**wykluczyć** hello niepotrzebnych etykiety hello innych dwa problemy oraz wszelkie inne **target przecieki**.</span><span class="sxs-lookup"><span data-stu-id="59a60-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="59a60-352">Dla przykład korzystając z klasyfikacji binarnej, za pomocą etykiety hello **Przechylony** i wykluczyć pola hello **Porada\_klasy**, **Porada\_kwota**, i **całkowita\_kwota**.</span><span class="sxs-lookup"><span data-stu-id="59a60-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="59a60-353">Hello te ostatnie są kupowane przecieki docelowy one zakłada Porada hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="59a60-354">tooexclude zbędne kolumny i/lub przecieki docelowych, można użyć hello [Select Columns in Dataset] [ select-columns] modułu lub hello [edytowanie metadanych] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="59a60-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="59a60-355">Aby uzyskać więcej informacji, zobacz [Select Columns in Dataset] [ select-columns] i [edytowanie metadanych] [ edit-metadata] odwołania stron.</span><span class="sxs-lookup"><span data-stu-id="59a60-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="59a60-356"><a name="mldeploy"></a>Wdrażanie modeli w uczenie maszynowe Azure</span><span class="sxs-lookup"><span data-stu-id="59a60-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="59a60-357">Gdy model jest gotowy, łatwo można go wdrożyć jako usługę sieci web bezpośrednio z hello eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="59a60-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="59a60-358">Aby uzyskać więcej informacji na temat wdrażania usług sieci web uczenie maszynowe Azure, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="59a60-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="59a60-359">toodeploy nową usługę sieci web, musisz:</span><span class="sxs-lookup"><span data-stu-id="59a60-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="59a60-360">Tworzenie eksperymentu oceniania.</span><span class="sxs-lookup"><span data-stu-id="59a60-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="59a60-361">Wdrażanie usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-361">Deploy hello web service.</span></span>

<span data-ttu-id="59a60-362">toocreate oceniania Poeksperymentuj z **Zakończono** szkolenia eksperyment, kliknij przycisk **utworzyć OCENIANIA EKSPERYMENTU** hello dolnym pasku akcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Ocenianie przez usługę Azure][18]

<span data-ttu-id="59a60-364">Usługa Azure Machine Learning podejmie toocreate eksperyment oceniania na podstawie składników hello eksperyment uczenia hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="59a60-365">W szczególności będzie:</span><span class="sxs-lookup"><span data-stu-id="59a60-365">In particular, it will:</span></span>

1. <span data-ttu-id="59a60-366">Zapisz hello uczonego modelu i usuwanie modułów uczenia modelu hello.</span><span class="sxs-lookup"><span data-stu-id="59a60-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="59a60-367">Zidentyfikuj logicznych **port wejściowy** toorepresent hello oczekiwano schemat danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="59a60-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="59a60-368">Zidentyfikuj logicznych **output portu** schematem wyjściowym toorepresent hello oczekiwanego sieci web usługi.</span><span class="sxs-lookup"><span data-stu-id="59a60-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="59a60-369">Po utworzeniu hello oceniania eksperymentu, przejrzyj go i dostosować zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="59a60-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="59a60-370">Typowy korekty jest wejściowy zestaw danych tooreplace hello i/lub zapytanie z taki, który wyklucza pola etykiety, jak te nie będą dostępne, gdy jest wywoływana hello usługi.</span><span class="sxs-lookup"><span data-stu-id="59a60-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="59a60-371">Istnieje również wprowadzenia hello o rozmiarze hello tooreduce dobrym rozwiązaniem tooa zestawu danych i/lub zapytania kilka rekordów, schemat danych wejściowych hello wystarczającego tooindicate.</span><span class="sxs-lookup"><span data-stu-id="59a60-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="59a60-372">Port wyjściowy hello, jest typowe tooexclude wszystkie pola i zawierać wyłącznie hello **oceniane etykiety** i **wynik prawdopodobieństwa** w danych wyjściowych za pomocą hello hello [Select Columns in Dataset ] [ select-columns] modułu.</span><span class="sxs-lookup"><span data-stu-id="59a60-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="59a60-373">Przykładowe oceniania eksperymentu jest hello na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="59a60-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="59a60-374">Toodeploy, gdy będzie gotowe kliknij hello **OPUBLIKOWAĆ usługi sieci WEB** przycisk hello dolnym pasku akcji.</span><span class="sxs-lookup"><span data-stu-id="59a60-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Publikowanie uczenie maszynowe Azure][11]

<span data-ttu-id="59a60-376">toorecap, w tym samouczku wskazówki utworzono środowiska nauki danych Azure, pracy z zestawem danych publicznych dużych końca hello z toomodel pozyskiwania danych, uczenie i wdrażanie usługi sieci web uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="59a60-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="59a60-377">Informacje o licencji</span><span class="sxs-lookup"><span data-stu-id="59a60-377">License Information</span></span>
<span data-ttu-id="59a60-378">Ten przewodnik próbki i jego towarzyszące IPython notebook(s) i skrypty są udostępniane przez firmę Microsoft hello MIT licencji.</span><span class="sxs-lookup"><span data-stu-id="59a60-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="59a60-379">Sprawdź plik LICENSE.txt hello w katalogu hello hello przykładowy kod w serwisie GitHub więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="59a60-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="59a60-380">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="59a60-380">References</span></span>
<span data-ttu-id="59a60-381">• [Andrés Monroy taksówki NYC rund stronę pobierania](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="59a60-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="59a60-382">• [FOILing NYC taksówki podróży danych przez Krzysztof Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="59a60-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="59a60-383">• [Taksówki NYC i Limousine Komisji badań i statystyki](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="59a60-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
