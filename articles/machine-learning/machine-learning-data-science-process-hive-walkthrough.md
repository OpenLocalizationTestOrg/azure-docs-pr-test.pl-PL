---
title: "dane aaaExplore usługi Hadoop klastra i tworzenia modeli w usłudze Azure Machine Learning | Dokumentacja firmy Microsoft"
description: "Za pomocą hello proces nauki danych zespołu scenariusz end-to-end wykorzystujących usługi HDInsight Hadoop klastra toobuild i wdrożenia modelu za pomocą publicznie dostępnych zestawu danych."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="081eb-103">Hello proces nauki danych zespołu w działaniu: klastrów użycia usługi Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="081eb-103">hello Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="081eb-104">W tym przewodniku używamy hello [zespołu danych nauki procesu (TDSP)](data-science-process-overview.md) w scenariuszu end-to-end przy użyciu [klastra usługi Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, Eksploruj i funkcji danych odtwarzania z hello publicznie dostępne [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych i toodown przykładowe dane hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-104">In this walkthrough, we use hello [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore and feature engineer data from hello publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and toodown sample hello data.</span></span> <span data-ttu-id="081eb-105">Modele danych hello są tworzone z usługi Azure Machine Learning toohandle binarnej i wieloklasowej klasyfikacji i regresji predykcyjnej zadania.</span><span class="sxs-lookup"><span data-stu-id="081eb-105">Models of hello data are built with Azure Machine Learning toohandle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="081eb-106">Aby uzyskać wskazówki, który pokazuje, jak toohandle większy zestaw danych (1 terabajt) podobny scenariusz za pomocą usługi HDInsight Hadoop clusters do przetwarzania danych, zobacz [zespołu danych nauki proces — za pomocą usługi Azure HDInsight klastrów platformy Hadoop w zestawie danych 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="081eb-106">For a walkthrough that shows how toohandle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="081eb-107">Jest również możliwe toouse hello tooaccomplish notesu IPython zadań wskazówki przedstawioną hello przy użyciu zestawu hello 1 TB danych.</span><span class="sxs-lookup"><span data-stu-id="081eb-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented hello walkthrough using hello 1 TB dataset.</span></span> <span data-ttu-id="081eb-108">Użytkownicy, którzy będą jak tootry takie podejście powinni skontaktować hello [wskazówki Criteo za pomocą połączenia ODBC programu Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tematu.</span><span class="sxs-lookup"><span data-stu-id="081eb-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="081eb-109"><a name="dataset"></a>Opis elementu Dataset rund taksówki NYC</span><span class="sxs-lookup"><span data-stu-id="081eb-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="081eb-110">Hello danych podróży taksówki NYC około 20GB skompresowanego wartości rozdzielanych przecinkami (CSV) plików (~ 48GB nieskompresowane), składającej się z więcej niż 173 milionów poszczególnych podróży i hello cen w klasie ekonomicznej płatnej w odniesieniu do każdej podróży.</span><span class="sxs-lookup"><span data-stu-id="081eb-110">hello NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="081eb-111">Każdy rekord podróży obejmuje hello odbiór i przyjmowania lokalizacji i czasu, numer licencji hack anonimowe (sterownik) i numer Medalionu (taksówki jego unikatowy identyfikator).</span><span class="sxs-lookup"><span data-stu-id="081eb-111">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="081eb-112">Hello danych obejmuje wszystkie rund w roku hello 2013 i jest dostępne w powitania po dwóch zestawów danych dla każdego miesiąca:</span><span class="sxs-lookup"><span data-stu-id="081eb-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="081eb-113">pliki CSV "trip_data" Hello zawierają szczegóły podróży, takie jak liczba pasażerów, pobranie i punkty dropoff czas trwania podróży i długość podróży.</span><span class="sxs-lookup"><span data-stu-id="081eb-113">hello 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="081eb-114">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="081eb-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="081eb-115">pliki CSV "trip_fare" Hello zawierają szczegółowe informacje o klasie hello za każdym razem, takie jak typ płatności, kwota taryfy przeciążenia i podatków, porady i przejazd i Suma hello płatnej.</span><span class="sxs-lookup"><span data-stu-id="081eb-115">hello 'trip_fare' CSV files contain details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="081eb-116">Poniżej przedstawiono kilka przykładowych rekordów:</span><span class="sxs-lookup"><span data-stu-id="081eb-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="081eb-117">Hello unikatowy kluczy toojoin podróży\_danych i podróży\_taryfy składa się z pola hello: Medalionu, hack\_licencji i pobrania\_daty/godziny.</span><span class="sxs-lookup"><span data-stu-id="081eb-117">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="081eb-118">tooget wszystkie hello szczegóły odpowiednich tooa określonego podróży, jest wystarczające toojoin z trzech kluczy: "Medalionu" hello "hack\_licencji" i "podnoszenia\_datetime".</span><span class="sxs-lookup"><span data-stu-id="081eb-118">tooget all of hello details relevant tooa particular trip, it is sufficient toojoin with three keys: hello "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="081eb-119">Firma Microsoft opisano niektóre szczegółowe dane hello, gdy są przechowywane ich do tabele programu Hive wkrótce.</span><span class="sxs-lookup"><span data-stu-id="081eb-119">We describe some more details of hello data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="081eb-120"><a name="mltasks"></a>Przykłady prognozowania zadań</span><span class="sxs-lookup"><span data-stu-id="081eb-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="081eb-121">Gdy zbliża się data, określania hello rodzaj prognoz, które chcesz toomake oparte na analizie jego pomaga wyjaśnienia hello zadań w procesie należy tooinclude.</span><span class="sxs-lookup"><span data-stu-id="081eb-121">When approaching data, determining hello kind of predictions you want toomake based on its analysis helps clarify hello tasks that you will need tooinclude in your process.</span></span>
<span data-ttu-id="081eb-122">Poniżej przedstawiono trzy przykłady problemów prognozowania, które można rozwiązać w ramach tego przewodnika, w której skład opiera się na powitania *Porada\_kwota*:</span><span class="sxs-lookup"><span data-stu-id="081eb-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on hello *tip\_amount*:</span></span>

1. <span data-ttu-id="081eb-123">**Klasyfikacji binarnej**: prognozowania, czy etykietki został płatnej podróży, tj. *Porada\_kwota* większą niż $0 jest przykład dodatnią, podczas gdy *Porada\_kwota* $ 0 jest ujemny przykład.</span><span class="sxs-lookup"><span data-stu-id="081eb-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="081eb-124">**Wieloklasowej klasyfikacji**: zakres hello toopredict kwot Porada uregulowaniu płatności hello podróży.</span><span class="sxs-lookup"><span data-stu-id="081eb-124">**Multiclass classification**: toopredict hello range of tip amounts paid for hello trip.</span></span> <span data-ttu-id="081eb-125">Możemy podzielić hello *Porada\_kwota* do pięciu bins lub klasy:</span><span class="sxs-lookup"><span data-stu-id="081eb-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="081eb-126">**Zadanie regresji**: toopredict hello ilość Porada hello płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="081eb-126">**Regression task**: toopredict hello amount of hello tip paid for a trip.</span></span>  

## <span data-ttu-id="081eb-127"><a name="setup"></a>Konfigurowanie klastra usługi HDInsight Hadoop zaawansowana analityka</span><span class="sxs-lookup"><span data-stu-id="081eb-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-128">Jest to zazwyczaj **Admin** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="081eb-129">Można skonfigurować środowiska platformy Azure zaawansowana analityka używającego klastra usługi HDInsight w trzy kroki:</span><span class="sxs-lookup"><span data-stu-id="081eb-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="081eb-130">[Utwórz konto magazynu](../storage/common/storage-create-storage-account.md): to konto magazynu jest używany do przechowywania danych w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="081eb-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="081eb-131">dane Hello używane w klastrach HDInsight również znajdują się tutaj.</span><span class="sxs-lookup"><span data-stu-id="081eb-131">hello data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="081eb-132">[Dostosowywanie Azure HDInsight Hadoop clusters dla hello zaawansowane procesu analizy i technologii](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="081eb-132">[Customize Azure HDInsight Hadoop clusters for hello Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="081eb-133">Spowoduje to utworzenie Azure HDInsight Hadoop, klaster z 64-bitowych Anaconda Python 2.7 zainstalowane we wszystkich węzłach.</span><span class="sxs-lookup"><span data-stu-id="081eb-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="081eb-134">Istnieją dwa tooremember ważne czynności podczas dostosowywania z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="081eb-134">There are two important steps tooremember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="081eb-135">Należy pamiętać, konta magazynu hello toolink utworzonego w kroku 1 z klastrem usługi HDInsight, podczas jej tworzenia.</span><span class="sxs-lookup"><span data-stu-id="081eb-135">Remember toolink hello storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="081eb-136">To konto magazynu jest tooaccess używane dane, które są przetwarzane w ramach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-136">This storage account is used tooaccess data that is processed within hello cluster.</span></span>
   * <span data-ttu-id="081eb-137">Po utworzeniu klastra hello włączyć dostęp zdalny toohello węzła głównego klastra hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-137">After hello cluster is created, enable Remote Access toohello head node of hello cluster.</span></span> <span data-ttu-id="081eb-138">Przejdź toohello **konfiguracji** i kliknij polecenie **Włącz zdalne**.</span><span class="sxs-lookup"><span data-stu-id="081eb-138">Navigate toohello **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="081eb-139">Ten krok określa hello poświadczenia użytkownika używane do logowania zdalnego.</span><span class="sxs-lookup"><span data-stu-id="081eb-139">This step specifies hello user credentials used for remote login.</span></span>
3. <span data-ttu-id="081eb-140">[Utwórz obszar roboczy usługi Azure Machine Learning](machine-learning-create-workspace.md): modeli uczenia maszynowego toobuild używane jest to Azure Machine Learning obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="081eb-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used toobuild machine learning models.</span></span> <span data-ttu-id="081eb-141">To zadanie zostanie rozwiązana po zakończeniu Eksploracja danych początkowych i w dół próbkowania przy użyciu hello klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="081eb-141">This task is addressed after completing an initial data exploration and down sampling using hello HDInsight cluster.</span></span>

## <span data-ttu-id="081eb-142"><a name="getdata"></a>Pobierz dane hello ze źródła publiczny</span><span class="sxs-lookup"><span data-stu-id="081eb-142"><a name="getdata"></a>Get hello data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-143">Jest to zazwyczaj **Admin** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="081eb-144">tooget hello [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych z lokalizacji publicznej, możesz użyć dowolnej z metod hello opisanego w [tooand przenoszenia danych z magazynu obiektów Blob Azure](machine-learning-data-science-move-azure-blob.md) toocopy hello danych tooyour maszyny.</span><span class="sxs-lookup"><span data-stu-id="081eb-144">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour machine.</span></span>

<span data-ttu-id="081eb-145">Opisano sposób użycia narzędzia AzCopy tootransfer hello pliki zawierający dane.</span><span class="sxs-lookup"><span data-stu-id="081eb-145">Here we describe how use AzCopy tootransfer hello files containing data.</span></span> <span data-ttu-id="081eb-146">toodownload i zainstaluj narzędzie AzCopy postępuj zgodnie z instrukcjami hello w [wprowadzenie hello wiersza polecenia Azcopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="081eb-146">toodownload and install AzCopy follow hello instructions at [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="081eb-147">Z poziomu okna wiersza polecenia wystawiać hello następujące polecenia narzędzia AzCopy, zastępując *< path_to_data_folder >* z hello docelowej lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="081eb-147">From a Command Prompt window, issue hello following AzCopy commands, replacing *<path_to_data_folder>* with hello desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="081eb-148">Po zakończeniu kopiowania hello łącznie 24 plików zip znajdują się w folderze danych hello wybrany.</span><span class="sxs-lookup"><span data-stu-id="081eb-148">When hello copy completes, a total of 24 zipped files are in hello data folder chosen.</span></span> <span data-ttu-id="081eb-149">Rozpakuj hello pobrane pliki toohello tym samym katalogu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="081eb-149">Unzip hello downloaded files toohello same directory on your local machine.</span></span> <span data-ttu-id="081eb-150">Zanotuj folder hello, w którym znajdują się pliki hello nieskompresowane.</span><span class="sxs-lookup"><span data-stu-id="081eb-150">Make a note of hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="081eb-151">Ten folder będzie hello określonego tooas *< ścieżka\_do\_unzipped_data\_pliki\>*  jest poniżej.</span><span class="sxs-lookup"><span data-stu-id="081eb-151">This folder will be referred tooas hello *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="081eb-152"><a name="upload"></a>Przekaż hello toohello domyślny kontener danych klastra usługi Azure HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="081eb-152"><a name="upload"></a>Upload hello data toohello default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-153">Jest to zazwyczaj **Admin** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="081eb-154">W hello następujące polecenia narzędzia AzCopy, Zastąp hello następujące parametry hello rzeczywiste wartości, które określono podczas tworzenia klastra usługi Hadoop hello i rozpakować hello plików danych.</span><span class="sxs-lookup"><span data-stu-id="081eb-154">In hello following AzCopy commands, replace hello following parameters with hello actual values that you specified when creating hello Hadoop cluster and unzipping hello data files.</span></span>

* <span data-ttu-id="081eb-155">***&#60; path_to_data_folder >*** katalogu hello (wraz ze ścieżką) na komputerze zawierają hello rozpakowane pliki danych</span><span class="sxs-lookup"><span data-stu-id="081eb-155">***&#60;path_to_data_folder>*** hello directory (along with path) on your machine that contain hello unzipped data files</span></span>  
* <span data-ttu-id="081eb-156">***&#60; nazwa konta magazynu z klastra usługi Hadoop >*** hello konta magazynu skojarzone z klastrem usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="081eb-156">***&#60;storage account name of Hadoop cluster>*** hello storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="081eb-157">***&#60; domyślny kontener klastra usługi Hadoop >*** hello domyślny kontener używane przez klaster.</span><span class="sxs-lookup"><span data-stu-id="081eb-157">***&#60;default container of Hadoop cluster>*** hello default container used by your cluster.</span></span> <span data-ttu-id="081eb-158">Zanotuj nazwę tego hello domyślnych hello kontenera jest zwykle hello takie same nazwy jako hello samego klastra.</span><span class="sxs-lookup"><span data-stu-id="081eb-158">Note that hello name of hello default container is usually hello same name as hello cluster itself.</span></span> <span data-ttu-id="081eb-159">Na przykład jeśli hello klastra jest nazywany "abc123.azurehdinsight.net", hello domyślny kontener jest abc123.</span><span class="sxs-lookup"><span data-stu-id="081eb-159">For example, if hello cluster is called "abc123.azurehdinsight.net", hello default container is abc123.</span></span>
* <span data-ttu-id="081eb-160">***&#60; klucz konta magazynu >*** hello klucza dla konta magazynu hello używane przez klaster</span><span class="sxs-lookup"><span data-stu-id="081eb-160">***&#60;storage account key>*** hello key for hello storage account used by your cluster</span></span>

<span data-ttu-id="081eb-161">Z wiersza polecenia lub okno programu Windows PowerShell na tym komputerze uruchom hello następujące dwa polecenia AzCopy.</span><span class="sxs-lookup"><span data-stu-id="081eb-161">From a Command Prompt or a Windows PowerShell window in your machine, run hello following two AzCopy commands.</span></span>

<span data-ttu-id="081eb-162">To polecenie przekazuje dane podróży hello zbyt***nyctaxitripraw*** katalogu w kontenerze domyślna hello hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="081eb-162">This command uploads hello trip data too***nyctaxitripraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="081eb-163">To polecenie przekazuje dane taryfy hello zbyt***nyctaxifareraw*** katalogu w kontenerze domyślna hello hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="081eb-163">This command uploads hello fare data too***nyctaxifareraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="081eb-164">Hello danych powinna się teraz w magazynie obiektów Blob Azure i gotowe toobe używane w ramach klastra usługi HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-164">hello data should now in Azure Blob Storage and ready toobe consumed within hello HDInsight cluster.</span></span>

## <span data-ttu-id="081eb-165"><a name="#download-hql-files"></a>Zaloguj się do hello węzła głównego klastra usługi Hadoop i i przygotować do analizy danych poznawcze</span><span class="sxs-lookup"><span data-stu-id="081eb-165"><a name="#download-hql-files"></a>Log into hello head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-166">Jest to zazwyczaj **Admin** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="081eb-167">tooaccess hello węzła głównego klastra hello do analizy danych poznawcze i w dół próbkowania hello danych, wykonaj procedurę hello opisane w temacie [hello dostępu Head węzeł z klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="081eb-167">tooaccess hello head node of hello cluster for exploratory data analysis and down sampling of hello data, follow hello procedure outlined in [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="081eb-168">W tym przewodniku używamy głównie zapytań w [Hive](https://hive.apache.org/), język zapytań SQL przypominającej, tooperform eksploracji wstępne dane.</span><span class="sxs-lookup"><span data-stu-id="081eb-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, tooperform preliminary data explorations.</span></span> <span data-ttu-id="081eb-169">zapytań programu Hive Hello są przechowywane w plikach .hql.</span><span class="sxs-lookup"><span data-stu-id="081eb-169">hello Hive queries are stored in .hql files.</span></span> <span data-ttu-id="081eb-170">Firma Microsoft następnie wyłącza przykładowe to toobe danych używana w usłudze Azure Machine Learning przeznaczone do budowania modeli.</span><span class="sxs-lookup"><span data-stu-id="081eb-170">We then down sample this data toobe used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="081eb-171">tooprepare hello klastra do analizy danych poznawcze, możemy Pobierz hello .hql pliki zawierające hello odpowiednie skrypty Hive z [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa lokalnego katalogu (C:\temp) na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="081eb-171">tooprepare hello cluster for exploratory data analysis, we download hello .hql files containing hello relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa local directory (C:\temp) on hello head node.</span></span> <span data-ttu-id="081eb-172">toodo, otwórz hello **wiersza polecenia** z poziomu hello węzłem głównym hello klastra i problem hello następujące dwa polecenia:</span><span class="sxs-lookup"><span data-stu-id="081eb-172">toodo this, open hello **Command Prompt** from within hello head node of hello cluster and issue hello following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="081eb-173">Te dwa polecenia pobierze wszystkie pliki .hql potrzebne w tym katalogu lokalnego toohello wskazówki ***C:\temp &#92;*** w hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="081eb-173">These two commands will download all .hql files needed in this walkthrough toohello local directory ***C:\temp&#92;*** in hello head node.</span></span>

## <span data-ttu-id="081eb-174"><a name="#hive-db-tables"></a>Utwórz gałąź bazy danych i tabele partycjonowane według miesięcy</span><span class="sxs-lookup"><span data-stu-id="081eb-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-175">Jest to zazwyczaj **Admin** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="081eb-176">Firma Microsoft są teraz gotowe toocreate tabele programu Hive dla naszego zestawu danych taksówki NYC.</span><span class="sxs-lookup"><span data-stu-id="081eb-176">We are now ready toocreate Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="081eb-177">Witaj węzła głównego klastra usługi Hadoop hello, otwórz hello ***wiersza polecenia platformy Hadoop*** na hello pulpitu hello węzła głównego, a następnie wprowadź katalog Hive hello wprowadzając polecenie hello</span><span class="sxs-lookup"><span data-stu-id="081eb-177">In hello head node of hello Hadoop cluster, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="081eb-178">**Uruchom wszystkie polecenia gałęzi w tym przewodniku z hello powyżej Hive bin / directory wiersza. To zajmie się wszelkie problemy, ścieżka automatycznie. Używane hello pojęcia "Hive katalogu wiersza", "bin gałęzi / wiersza katalogu" i "wiersza polecenia usługi Hadoop" zamiennie w tym przewodniku.**</span><span class="sxs-lookup"><span data-stu-id="081eb-178">**Run all Hive commands in this walkthrough from hello above Hive bin/ directory prompt. This will take care of any path issues automatically. We use hello terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="081eb-179">Hello gałęzi katalogu w wierszu polecenia programu wprowadź następujące polecenie w wierszu polecenia Hadoop hello węzła głównego toosubmit hello Hive zapytania toocreate gałąź bazy danych i tabele hello:</span><span class="sxs-lookup"><span data-stu-id="081eb-179">From hello Hive directory prompt, enter hello following command in Hadoop Command Line of hello head node toosubmit hello Hive query toocreate Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="081eb-180">Oto hello zawartość hello ***C:\temp\sample\_hive\_utworzyć\_db\_i\_tables.hql*** pliku, który tworzy gałąź bazy danych ***nyctaxidb *** i tabele ***podróży*** i ***taryfy***.</span><span class="sxs-lookup"><span data-stu-id="081eb-180">Here is hello content of hello ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

<span data-ttu-id="081eb-181">Ten skrypt Hive tworzy dwie tabele:</span><span class="sxs-lookup"><span data-stu-id="081eb-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="081eb-182">Tabela "podróży" Hello zawiera szczegóły podróży każdego jazdy (Szczegóły sterownika, czasu odbioru, odległość podróży i razy)</span><span class="sxs-lookup"><span data-stu-id="081eb-182">hello "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="081eb-183">Tabela "opłata" Hello zawiera szczegóły taryfy (kwota taryfy, kwota poradę, przejazd i opłaty).</span><span class="sxs-lookup"><span data-stu-id="081eb-183">hello "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="081eb-184">Jeśli konieczne uzyskania dodatkowej pomocy w tych procedurach lub mają tooinvestigate tych alternatywnych, zobacz sekcję hello [zapytań Hive przesłać bezpośrednio z hello wiersza polecenia usługi Hadoop ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="081eb-184">If you need any additional assistance with these procedures or want tooinvestigate alternative ones, see hello section [Submit Hive queries directly from hello Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="081eb-185"><a name="#load-data"></a>Załaduj dane tooHive tabel, partycji</span><span class="sxs-lookup"><span data-stu-id="081eb-185"><a name="#load-data"></a>Load Data tooHive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-186">Jest to zazwyczaj **Admin** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="081eb-187">dataset taksówki Hello NYC ma fizycznych partycjonowania według miesięcy, której używamy tooenable krótszy czas przetwarzania i zapytania.</span><span class="sxs-lookup"><span data-stu-id="081eb-187">hello NYC taxi dataset has a natural partitioning by month, which we use tooenable faster processing and query times.</span></span> <span data-ttu-id="081eb-188">Witaj poniższe polecenia programu PowerShell (wystawiony na podstawie hello gałęzi katalogu przy użyciu hello **wiersza polecenia platformy Hadoop**) załadować danych toohello "podróży" i "opłata" tabele programu Hive podzielona na partycje według miesięcy.</span><span class="sxs-lookup"><span data-stu-id="081eb-188">hello PowerShell commands below (issued from hello Hive directory using hello **Hadoop Command Line**) load data toohello "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="081eb-189">Hello *próbki\_hive\_załadować\_danych\_przez\_partitions.hql* plik zawiera następujące hello **ZAŁADOWAĆ** poleceń.</span><span class="sxs-lookup"><span data-stu-id="081eb-189">hello *sample\_hive\_load\_data\_by\_partitions.hql* file contains hello following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="081eb-190">Należy pamiętać, że liczba zapytań programu Hive używanej w tym miejscu w procesu eksploracji hello są związane z jednej partycji lub tylko kilka partycji.</span><span class="sxs-lookup"><span data-stu-id="081eb-190">Note that a number of Hive queries we use here in hello exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="081eb-191">Jednak te zapytania może zostać uruchomione przez cały danych hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-191">But these queries could be run across hello entire data.</span></span>

### <span data-ttu-id="081eb-192"><a name="#show-db"></a>Pokaż baz danych w hello klastra usługi HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="081eb-192"><a name="#show-db"></a>Show databases in hello HDInsight Hadoop cluster</span></span>
<span data-ttu-id="081eb-193">tooshow baz hello danych utworzonych w klastrze usługi HDInsight Hadoop w oknie wiersza polecenia platformy Hadoop hello, uruchom następujące polecenie w wierszu polecenia Hadoop hello:</span><span class="sxs-lookup"><span data-stu-id="081eb-193">tooshow hello databases created in HDInsight Hadoop cluster inside hello Hadoop Command Line window, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="081eb-194"><a name="#show-tables"></a>Pokaż tabele programu Hive hello w bazie danych nyctaxidb hello</span><span class="sxs-lookup"><span data-stu-id="081eb-194"><a name="#show-tables"></a>Show hello Hive tables in hello nyctaxidb database</span></span>
<span data-ttu-id="081eb-195">tabele hello tooshow hello nyctaxidb bazy danych, uruchom następujące polecenie w wierszu polecenia Hadoop hello:</span><span class="sxs-lookup"><span data-stu-id="081eb-195">tooshow hello tables in hello nyctaxidb database, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="081eb-196">Możemy potwierdzić, że tabele hello są dzielone wydając polecenie hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="081eb-196">We can confirm that hello tables are partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="081eb-197">Witaj oczekuje się, że dane wyjściowe są wyświetlane poniżej:</span><span class="sxs-lookup"><span data-stu-id="081eb-197">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

<span data-ttu-id="081eb-198">Podobnie możemy upewnij się, że ta tabela taryfy hello jest podzielona na partycje wydając polecenie hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="081eb-198">Similarly, we can ensure that hello fare table is partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="081eb-199">Witaj oczekuje się, że dane wyjściowe są wyświetlane poniżej:</span><span class="sxs-lookup"><span data-stu-id="081eb-199">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <span data-ttu-id="081eb-200"><a name="#explore-hive"></a>Eksploracja danych i funkcji inżynieryjne w gałęzi</span><span class="sxs-lookup"><span data-stu-id="081eb-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-201">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-202">Witaj Eksploracja danych i funkcji engineering zadania hello dane ładowane do hello tabele programu Hive można osiągnąć za pomocą zapytań Hive.</span><span class="sxs-lookup"><span data-stu-id="081eb-202">hello data exploration and feature engineering tasks for hello data loaded into hello Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="081eb-203">Poniżej przedstawiono przykłady takich zadań, że firma Microsoft przeprowadzi użytkownika przez proces w tej sekcji:</span><span class="sxs-lookup"><span data-stu-id="081eb-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="081eb-204">Wyświetl hello top 10 rekordów w obu tabel.</span><span class="sxs-lookup"><span data-stu-id="081eb-204">View hello top 10 records in both tables.</span></span>
* <span data-ttu-id="081eb-205">Eksplorowanie danych dystrybucji kilka pól w różnym czasie systemu windows.</span><span class="sxs-lookup"><span data-stu-id="081eb-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="081eb-206">Zbadaj jakości danych hello pól długości i szerokości geograficznej.</span><span class="sxs-lookup"><span data-stu-id="081eb-206">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="081eb-207">Generowanie etykiet klasyfikacji binarnej i wieloklasowej oparte na powitania **Porada\_kwota**.</span><span class="sxs-lookup"><span data-stu-id="081eb-207">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="081eb-208">Generowanie funkcji przez obliczeniowych hello bezpośredniego podróży odległości.</span><span class="sxs-lookup"><span data-stu-id="081eb-208">Generate features by computing hello direct trip distances.</span></span>

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a><span data-ttu-id="081eb-209">Eksploracja: Wyświetlanie hello top 10 rekordów w podróży tabeli</span><span class="sxs-lookup"><span data-stu-id="081eb-209">Exploration: View hello top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-210">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-211">jakie dane hello wygląda toosee, omówione 10 rekordy z każdej tabeli.</span><span class="sxs-lookup"><span data-stu-id="081eb-211">toosee what hello data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="081eb-212">Uruchom hello oddzielnie następujące dwa zapytania z wiersza katalogu Hive hello hello Hadoop wiersza polecenia konsoli tooinspect hello rekordów.</span><span class="sxs-lookup"><span data-stu-id="081eb-212">Run hello following two queries separately from hello Hive directory prompt in hello Hadoop Command Line console tooinspect hello records.</span></span>

<span data-ttu-id="081eb-213">tooget hello top 10 rekordów w tabeli hello "podróży" z hello pierwszy miesiąc:</span><span class="sxs-lookup"><span data-stu-id="081eb-213">tooget hello top 10 records in hello table "trip" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="081eb-214">tooget hello top 10 rekordów w tabeli hello "opłata" z hello miesiąca:</span><span class="sxs-lookup"><span data-stu-id="081eb-214">tooget hello top 10 records in hello table "fare" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="081eb-215">Często jest przydatne toosave hello rekordów tooa pliku w celu wyświetlenia wygodne.</span><span class="sxs-lookup"><span data-stu-id="081eb-215">It is often useful toosave hello records tooa file for convenient viewing.</span></span> <span data-ttu-id="081eb-216">Niewielkie zmiany toohello powyżej zapytania rozwiązanie to:</span><span class="sxs-lookup"><span data-stu-id="081eb-216">A small change toohello above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a><span data-ttu-id="081eb-217">Eksploracja: Wyświetl hello liczby rekordów w każdej partycji 12 hello</span><span class="sxs-lookup"><span data-stu-id="081eb-217">Exploration: View hello number of records in each of hello 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-218">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-219">Odsetek jest hello jak hello liczby rund różni się w roku kalendarzowym hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-219">Of interest is hello how hello number of trips varies during hello calendar year.</span></span> <span data-ttu-id="081eb-220">Grupowanie według miesięcy pozwala nam toosee wygląda tej dystrybucji rund.</span><span class="sxs-lookup"><span data-stu-id="081eb-220">Grouping by month allows us toosee what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="081eb-221">Daje hello danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="081eb-221">This gives us hello output :</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

<span data-ttu-id="081eb-222">W tym miejscu hello pierwszej kolumny hello miesiąc a hello jest drugi hello liczby rund w danym miesiącu.</span><span class="sxs-lookup"><span data-stu-id="081eb-222">Here, hello first column is hello month and hello second is hello number of trips for that month.</span></span>

<span data-ttu-id="081eb-223">Firma Microsoft zliczanie hello całkowita liczba rekordów w naszym zestawie danych podróży wysyłając hello następujące polecenie w wierszu hello gałęzi katalogu.</span><span class="sxs-lookup"><span data-stu-id="081eb-223">We can also count hello total number of records in our trip data set by issuing hello following command at hello Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="081eb-224">Daje to:</span><span class="sxs-lookup"><span data-stu-id="081eb-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="081eb-225">Za pomocą polecenia toothose podobne wyświetlane dla zestawu danych w podróży hello, firma Microsoft może wystawiać zapytań programu Hive z wiersza katalogu Hive hello hello taryfy zestawu danych toovalidate hello liczby rekordów.</span><span class="sxs-lookup"><span data-stu-id="081eb-225">Using commands similar toothose shown for hello trip data set, we can issue Hive queries from hello Hive directory prompt for hello fare data set toovalidate hello number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="081eb-226">Daje hello danych wyjściowych:</span><span class="sxs-lookup"><span data-stu-id="081eb-226">This gives us hello output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

<span data-ttu-id="081eb-227">Należy pamiętać, że hello dokładnie takie same numery rund miesięcznie jest zwracany w obu zestawach danych.</span><span class="sxs-lookup"><span data-stu-id="081eb-227">Note that hello exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="081eb-228">Zapewnia to pierwsze sprawdzenie hello tego powitalne danych został załadowany poprawnie.</span><span class="sxs-lookup"><span data-stu-id="081eb-228">This provides hello first validation that hello data has been loaded correctly.</span></span>

<span data-ttu-id="081eb-229">Zliczanie hello całkowita liczba rekordów w zestawie danych taryfy hello może odbywać się przy użyciu polecenia hello poniżej w wierszu katalogu Hive hello:</span><span class="sxs-lookup"><span data-stu-id="081eb-229">Counting hello total number of records in hello fare data set can be done using hello command below from hello Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="081eb-230">Daje to:</span><span class="sxs-lookup"><span data-stu-id="081eb-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="081eb-231">Całkowita liczba rekordów z obu tabel Hello jest również hello tego samego.</span><span class="sxs-lookup"><span data-stu-id="081eb-231">hello total number of records in both tables is also hello same.</span></span> <span data-ttu-id="081eb-232">Zapewnia to drugi sprawdzania poprawności tego powitalne danych został załadowany poprawnie.</span><span class="sxs-lookup"><span data-stu-id="081eb-232">This provides a second validation that hello data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="081eb-233">Eksploracja: Podróży dystrybucji przez Medalionu</span><span class="sxs-lookup"><span data-stu-id="081eb-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-234">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-235">W tym przykładzie identyfikuje hello Medalionu (taksówki numery) z więcej niż 100 rund w danym okresie.</span><span class="sxs-lookup"><span data-stu-id="081eb-235">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="081eb-236">Hello zapytania korzyści z hello na partycje dostępu do tabel, ponieważ należy przygotować przez zmienną partycji hello **miesiąca**.</span><span class="sxs-lookup"><span data-stu-id="081eb-236">hello query benefits from hello partitioned table access since it is conditioned by hello partition variable **month**.</span></span> <span data-ttu-id="081eb-237">Witaj wyniki zapytania są zapisywane queryoutput.tsv pliku lokalnego tooa `C:\temp` na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="081eb-237">hello query results are written tooa local file queryoutput.tsv in `C:\temp` on hello head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="081eb-238">Oto zawartość hello *próbki\_hive\_podróży\_liczba\_przez\_medallion.hql* pliku inspekcji.</span><span class="sxs-lookup"><span data-stu-id="081eb-238">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="081eb-239">Medalionu Hello w zestawie danych taksówki NYC hello identyfikuje unikatowy pliku cab.</span><span class="sxs-lookup"><span data-stu-id="081eb-239">hello medallion in hello NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="081eb-240">Firma Microsoft można określić, które pliki cab są "zajęte" pytając, które z nich wprowadzone więcej niż określoną liczbę rund w określonym przedziale czasu.</span><span class="sxs-lookup"><span data-stu-id="081eb-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="081eb-241">Witaj poniższy przykład identyfikuje pliki cab, wprowadzone w więcej niż stu rund w hello pierwszych trzech miesięcy i zapisuje hello zapytania tooa lokalnego pliku wyników C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="081eb-241">hello following example identifies cabs that made more than a hundred trips in hello first three months, and saves hello query results tooa local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="081eb-242">Oto zawartość hello *próbki\_hive\_podróży\_liczba\_przez\_medallion.hql* pliku inspekcji.</span><span class="sxs-lookup"><span data-stu-id="081eb-242">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="081eb-243">Z hello gałęzi katalogu wierszu poniższego polecenia hello problemu:</span><span class="sxs-lookup"><span data-stu-id="081eb-243">From hello Hive directory prompt, issue hello command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="081eb-244">Eksploracja: Podróży dystrybucji Medalionu i hack_license</span><span class="sxs-lookup"><span data-stu-id="081eb-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-245">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-246">Podczas eksplorowania zestawu danych, chcemy często tooexamine hello liczbę wystąpień co grupy wartości.</span><span class="sxs-lookup"><span data-stu-id="081eb-246">When exploring a dataset, we frequently want tooexamine hello number of co-occurences of groups of values.</span></span> <span data-ttu-id="081eb-247">W tej sekcji przedstawiono przykładową jak toodo dla plików cab i sterowników.</span><span class="sxs-lookup"><span data-stu-id="081eb-247">This section provide an example of how toodo this for cabs and drivers.</span></span>

<span data-ttu-id="081eb-248">Witaj *próbki\_hive\_podróży\_liczba\_przez\_Medalionu\_license.hql* grup plików danych taryfy hello "Medalionu" i "hack_license" i zwraca liczbę każdej kombinacji.</span><span class="sxs-lookup"><span data-stu-id="081eb-248">hello *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups hello fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="081eb-249">Poniżej przedstawiono jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="081eb-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="081eb-250">Ta kwerenda zwraca kombinacji określony sterownik, uporządkowanych malejąco liczby rund i cab.</span><span class="sxs-lookup"><span data-stu-id="081eb-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="081eb-251">Z hello Hive wiersza katalogu, uruchom:</span><span class="sxs-lookup"><span data-stu-id="081eb-251">From hello Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="081eb-252">wyniki zapytania Hello są zapisywane w pliku lokalnego tooa C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="081eb-252">hello query results are written tooa local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="081eb-253">Eksploracja: Oceny jakości danych przez wyszukiwanie rekordów nieprawidłowa długość i szerokość geograficzna</span><span class="sxs-lookup"><span data-stu-id="081eb-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-254">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-255">Typowe celem analizy danych poznawcze jest tooweed się rekordy nieprawidłowe lub uszkodzone.</span><span class="sxs-lookup"><span data-stu-id="081eb-255">A common objective of exploratory data analysis is tooweed out invalid or bad records.</span></span> <span data-ttu-id="081eb-256">Witaj przykładzie w tej sekcji określa, czy albo hello pola współrzędnych geograficznych zawierać wartości do tej pory spoza hello NYC obszaru.</span><span class="sxs-lookup"><span data-stu-id="081eb-256">hello example in this section determines whether either hello longitude or latitude fields contain a value far outside hello NYC area.</span></span> <span data-ttu-id="081eb-257">Ponieważ istnieje prawdopodobieństwo, że takie rekordów mają wartości błędne współrzędne geograficzne, chcemy tooeliminate je z żadnych danych toobe używany do modelowania.</span><span class="sxs-lookup"><span data-stu-id="081eb-257">Since it is likely that such records have an erroneous longitude-latitude values, we want tooeliminate them from any data that is toobe used for modeling.</span></span>

<span data-ttu-id="081eb-258">Oto zawartość hello *próbki\_hive\_jakości\_assessment.hql* pliku inspekcji.</span><span class="sxs-lookup"><span data-stu-id="081eb-258">Here is hello content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="081eb-259">Z hello Hive wiersza katalogu, uruchom:</span><span class="sxs-lookup"><span data-stu-id="081eb-259">From hello Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="081eb-260">Witaj *-S* hello wydruk ekranu stan zadania Hive mapy/Zmniejsz hello pomija argument zawarte w tym poleceniu.</span><span class="sxs-lookup"><span data-stu-id="081eb-260">hello *-S* argument included in this command suppresses hello status screen printout of hello Hive Map/Reduce jobs.</span></span> <span data-ttu-id="081eb-261">Jest to przydatne, ponieważ sprawia, że hello ekranu drukowanie hello Hive wyników zapytania bardziej czytelne.</span><span class="sxs-lookup"><span data-stu-id="081eb-261">This is useful because it makes hello screen print of hello Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="081eb-262">Eksploracja: Binarny klasy dystrybucje podróży porad</span><span class="sxs-lookup"><span data-stu-id="081eb-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-263">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-264">Opisane w hello problemu klasyfikacji binarnej hello [przykłady zadań prognozowania](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sekcji, czy etykietki został podany lub nie jest przydatne tooknow.</span><span class="sxs-lookup"><span data-stu-id="081eb-264">For hello binary classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful tooknow whether a tip was given or not.</span></span> <span data-ttu-id="081eb-265">Tej dystrybucji porady jest plikiem binarnym:</span><span class="sxs-lookup"><span data-stu-id="081eb-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="081eb-266">Porada podane (klasy 1, porada\_ilość > $0)</span><span class="sxs-lookup"><span data-stu-id="081eb-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="081eb-267">Brak porady (klasa 0, porada\_kwota = $0).</span><span class="sxs-lookup"><span data-stu-id="081eb-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="081eb-268">Witaj *próbki\_hive\_Przechylony\_frequencies.hql* pliku pokazano poniżej robi to.</span><span class="sxs-lookup"><span data-stu-id="081eb-268">hello *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="081eb-269">Z hello Hive wiersza katalogu, uruchom:</span><span class="sxs-lookup"><span data-stu-id="081eb-269">From hello Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a><span data-ttu-id="081eb-270">Eksploracja: Klasa dystrybucje w ustawieniu wieloklasowej hello</span><span class="sxs-lookup"><span data-stu-id="081eb-270">Exploration: Class distributions in hello multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-271">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-272">Witaj wieloklasowej klasyfikacji problemu opisane w hello [przykłady zadań prognozowania](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sekcji ten zestaw danych również jest przydatna tooa klasyfikacji fizycznych gdzie chcielibyśmy toopredict hello ilość porady hello podane.</span><span class="sxs-lookup"><span data-stu-id="081eb-272">For hello multiclass classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself tooa natural classification where we would like toopredict hello amount of hello tips given.</span></span> <span data-ttu-id="081eb-273">Możemy użyć bins toodefine Porada zakresów w zapytaniu hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-273">We can use bins toodefine tip ranges in hello query.</span></span> <span data-ttu-id="081eb-274">tooget hello dystrybucji klasy dla hello różnych zakresów poradę, używamy hello *próbki\_hive\_Porada\_zakres\_frequencies.hql* pliku.</span><span class="sxs-lookup"><span data-stu-id="081eb-274">tooget hello class distributions for hello various tip ranges, we use hello *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="081eb-275">Poniżej przedstawiono jego zawartość.</span><span class="sxs-lookup"><span data-stu-id="081eb-275">Below are its contents.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

<span data-ttu-id="081eb-276">Uruchom następujące polecenie z wiersza polecenia platformy Hadoop konsoli hello:</span><span class="sxs-lookup"><span data-stu-id="081eb-276">Run hello following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="081eb-277">Eksploracji: Bezpośrednie odległość między dwiema lokalizacjami współrzędne geograficzne obliczeniowe</span><span class="sxs-lookup"><span data-stu-id="081eb-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-278">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-279">O miary odległości bezpośredniego hello pozwala nam toofind limit hello rozbieżność między nim a hello rzeczywiste rzeczy przed wyjazdem odległości.</span><span class="sxs-lookup"><span data-stu-id="081eb-279">Having a measure of hello direct distance allows us toofind out hello discrepancy between it and hello actual trip distance.</span></span> <span data-ttu-id="081eb-280">Ta funkcja możemy Motywuj przez wskazujące, że osób może być mniejsza prawdopodobnie tootip, jeśli ich dowiedzieć się, że sterownik hello celowo trwało ich drogą znacznie dłużej.</span><span class="sxs-lookup"><span data-stu-id="081eb-280">We motivate this feature by pointing out that a passenger might be less likely tootip if they figure out that hello driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="081eb-281">toosee hello porównanie odległość rzeczywiste podróży i hello [odległość Haversine](http://en.wikipedia.org/wiki/Haversine_formula) między dwoma punktami współrzędne geograficzne (hello "koła" wielkiego) używamy funkcje trygonometryczne hello dostępne w gałęzi, w związku z tym:</span><span class="sxs-lookup"><span data-stu-id="081eb-281">toosee hello comparison between actual trip distance and hello [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (hello "great circle" distance), we use hello trigonometric functions available within Hive, thus :</span></span>

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

<span data-ttu-id="081eb-282">W powyższym zapytaniu hello R jest hello promień hello Earth w milach i pi jest tooradians przekonwertowany.</span><span class="sxs-lookup"><span data-stu-id="081eb-282">In hello query above, R is hello radius of hello Earth in miles, and pi is converted tooradians.</span></span> <span data-ttu-id="081eb-283">Należy zauważyć, że punkty współrzędne geograficzne hello wartości "filtrowane" tooremove daleko od hello NYC obszaru.</span><span class="sxs-lookup"><span data-stu-id="081eb-283">Note that hello longitude-latitude points are "filtered" tooremove values that are far from hello NYC area.</span></span>

<span data-ttu-id="081eb-284">W takim przypadku możemy zapisać naszych wyników tooa katalog o nazwie "queryoutputdir".</span><span class="sxs-lookup"><span data-stu-id="081eb-284">In this case, we write our results tooa directory called "queryoutputdir".</span></span> <span data-ttu-id="081eb-285">Witaj sekwencji poleceń pokazano poniżej najpierw tworzy ten katalog wyjściowy, a następnie uruchamia polecenie gałęzi hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-285">hello sequence of commands shown below first creates this output directory, and then runs hello Hive command.</span></span>

<span data-ttu-id="081eb-286">Z hello Hive wiersza katalogu, uruchom:</span><span class="sxs-lookup"><span data-stu-id="081eb-286">From hello Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="081eb-287">Witaj wyniki zapytania są zapisywane obiektów blob too9 Azure ***queryoutputdir/000000\_0*** za ***queryoutputdir/000008\_0*** w kontenerze domyślna hello hello klastra usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="081eb-287">hello query results are written too9 Azure blobs ***queryoutputdir/000000\_0*** too ***queryoutputdir/000008\_0*** under hello default container of hello Hadoop cluster.</span></span>

<span data-ttu-id="081eb-288">rozmiar hello toosee hello poszczególne obiekty BLOB, przeprowadzana hello następujące polecenie w wierszu katalogu Hive hello:</span><span class="sxs-lookup"><span data-stu-id="081eb-288">toosee hello size of hello individual blobs, we run hello following command from hello Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="081eb-289">toosee hello zawartość określonego pliku, powiedz 000000\_0, używamy jego Hadoop `copyToLocal` poleceń, w związku z tym.</span><span class="sxs-lookup"><span data-stu-id="081eb-289">toosee hello contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="081eb-290">`copyToLocal`może być bardzo wolno dla dużych plików, a nie jest zalecane używanie z nimi.</span><span class="sxs-lookup"><span data-stu-id="081eb-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="081eb-291">Zaletą tych danych znajdują się w obiekcie blob Azure jest, że firma Microsoft może Eksplorowanie danych hello w ramach usługi Azure Machine Learning przy użyciu hello [i zaimportuj dane] [ import-data] modułu.</span><span class="sxs-lookup"><span data-stu-id="081eb-291">A key advantage of having this data reside in an Azure blob is that we may explore hello data within Azure Machine Learning using hello [Import Data][import-data] module.</span></span>

## <span data-ttu-id="081eb-292"><a name="#downsample"></a>Przykładowe modele danych i kompilacji w usłudze Azure Machine Learning w dół</span><span class="sxs-lookup"><span data-stu-id="081eb-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="081eb-293">Jest to zazwyczaj **naukowca danych** zadań.</span><span class="sxs-lookup"><span data-stu-id="081eb-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="081eb-294">Po faza analizy danych poznawcze hello możemy teraz gotowy toodown przykładowe hello dane przeznaczone do budowania modeli w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="081eb-294">After hello exploratory data analysis phase, we are now ready toodown sample hello data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="081eb-295">W tej sekcji zostanie przedstawiony sposób toouse gałąź zapytania toodown przykładowych hello danych, który następnie jest dostępny z hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="081eb-295">In this section, we show how toouse a Hive query toodown sample hello data, which is then accessed from hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-hello-data"></a><span data-ttu-id="081eb-296">Próbkowanie danych hello w dół</span><span class="sxs-lookup"><span data-stu-id="081eb-296">Down sampling hello data</span></span>
<span data-ttu-id="081eb-297">Istnieją dwa kroki tej procedury.</span><span class="sxs-lookup"><span data-stu-id="081eb-297">There are two steps in this procedure.</span></span> <span data-ttu-id="081eb-298">Najpierw dołączyć firma Microsoft hello **nyctaxidb.trip** i **nyctaxidb.fare** tabel w trzech kluczy, które znajdują się we wszystkich rekordach: "Medalionu", "hack\_licencji", i "podnoszenia\_datetime".</span><span class="sxs-lookup"><span data-stu-id="081eb-298">First we join hello **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="081eb-299">Następnie możemy wygenerować etykiety klasyfikacji binarnej **Przechylony** i etykiety klasyfikacji wielu klasy **Porada\_klasy**.</span><span class="sxs-lookup"><span data-stu-id="081eb-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="081eb-300">toobe toouse stanie hello dół próbki danych bezpośrednio z hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning jest konieczne toostore wyniki hello hello powyżej wewnętrznej tabeli Hive tooan zapytania.</span><span class="sxs-lookup"><span data-stu-id="081eb-300">toobe able toouse hello down sampled data directly from hello [Import Data][import-data] module in Azure Machine Learning, it is necessary toostore hello results of hello above query tooan internal Hive table.</span></span> <span data-ttu-id="081eb-301">W poniżej możemy utworzyć wewnętrznej tabeli Hive i wypełnić zawartością z hello przyłączone i w dół próbki danych.</span><span class="sxs-lookup"><span data-stu-id="081eb-301">In what follows, we create an internal Hive table and populate its contents with hello joined and down sampled data.</span></span>

<span data-ttu-id="081eb-302">Witaj zapytania stosuje standardowe funkcje Hive bezpośrednio toogenerate hello godzinę dnia, tygodnia w roku, dzień tygodnia (1 zawiera poniedziałek i 7 zawiera niedziela) z hello "podnoszenia\_datetime" pola i hello bezpośredniego odległość między hello odbiór i dropoff lokalizacje.</span><span class="sxs-lookup"><span data-stu-id="081eb-302">hello query applies standard Hive functions directly toogenerate hello hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from hello "pickup\_datetime" field,  and hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="081eb-303">Użytkownicy mogą odwoływać się za[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) pełną listę funkcji.</span><span class="sxs-lookup"><span data-stu-id="081eb-303">Users can refer too[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="081eb-304">Witaj zapytania, a następnie danych hello próbek w dół, aby hello wyniki zapytania można umieścić w hello Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="081eb-304">hello query then down samples hello data so that hello query results can fit into hello Azure Machine Learning Studio.</span></span> <span data-ttu-id="081eb-305">Tylko około 1% hello oryginalnego zestawu danych jest importowany do hello Studio.</span><span class="sxs-lookup"><span data-stu-id="081eb-305">Only about 1% of hello original dataset is imported into hello Studio.</span></span>

<span data-ttu-id="081eb-306">Poniżej przedstawiono zawartość hello *próbki\_hive\_przygotowanie\_dla\_aml\_full.hql* pliku, który przygotowuje danych do tworzenia w usłudze Azure Machine Learning model.</span><span class="sxs-lookup"><span data-stu-id="081eb-306">Below are hello contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

<span data-ttu-id="081eb-307">Monituj toorun tego zapytania z katalogu Hive hello:</span><span class="sxs-lookup"><span data-stu-id="081eb-307">toorun this query, from hello Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="081eb-308">Teraz mamy wewnętrznej tabeli "nyctaxidb.nyctaxi_downsampled_dataset", który można uzyskać dostęp za pomocą hello [i zaimportuj dane] [ import-data] modułu na podstawie usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="081eb-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using hello [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="081eb-309">Ponadto firma Microsoft może używać tego elementu dataset do budowania modeli uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="081eb-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a><span data-ttu-id="081eb-310">Używaj modułu i zaimportuj dane hello w hello tooaccess uczenie maszynowe Azure w dół próbki danych</span><span class="sxs-lookup"><span data-stu-id="081eb-310">Use hello Import Data module in Azure Machine Learning tooaccess hello down sampled data</span></span>
<span data-ttu-id="081eb-311">Jako wymagania wstępne dotyczące wysyłania zapytań Hive w hello [i zaimportuj dane] [ import-data] moduł usługi Azure Machine Learning, potrzebujemy dostęp do obszaru roboczego uczenia maszynowego Azure tooan i dostęp do poświadczeń toohello hello klaster i jego skojarzone konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="081eb-311">As prerequisites for issuing Hive queries in hello [Import Data][import-data] module of Azure Machine Learning, we need access tooan Azure Machine Learning workspace and access toohello credentials of hello cluster and its associated storage account.</span></span>

<span data-ttu-id="081eb-312">Niektóre szczegóły na powitania [i zaimportuj dane] [ import-data] modułu i hello tooinput parametry:</span><span class="sxs-lookup"><span data-stu-id="081eb-312">Some details on hello [Import Data][import-data] module and hello parameters tooinput :</span></span>

<span data-ttu-id="081eb-313">**Identyfikator URI serwera HCatalog**: Jeśli nazwa klastra hello jest abc123, to po prostu: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="081eb-313">**HCatalog server URI**: If hello cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="081eb-314">**Nazwa konta użytkownika Hadoop** : nazwa użytkownika hello wybrany dla klastra hello (**nie** nazwa użytkownika dostępu zdalnego hello)</span><span class="sxs-lookup"><span data-stu-id="081eb-314">**Hadoop user account name** : hello user name chosen for hello cluster (**not** hello remote access user name)</span></span>

<span data-ttu-id="081eb-315">**Hasło konta ser Hadoop** : hasło hello wybrany dla klastra hello (**nie** hello hasła dostępu zdalnego)</span><span class="sxs-lookup"><span data-stu-id="081eb-315">**Hadoop ser account password** : hello password chosen for hello cluster (**not** hello remote access password)</span></span>

<span data-ttu-id="081eb-316">**Lokalizacja danych wyjściowych** : to jest wybierany toobe Azure.</span><span class="sxs-lookup"><span data-stu-id="081eb-316">**Location of output data** : This is chosen toobe Azure.</span></span>

<span data-ttu-id="081eb-317">**Nazwa konta magazynu Azure** : Nazwa hello domyślnego konta magazynu skojarzone z klastrem hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-317">**Azure storage account name** : Name of hello default storage account associated with hello cluster.</span></span>

<span data-ttu-id="081eb-318">**Nazwa kontenera Azure** : to jest nazwa kontenera domyślnego hello hello klastra i jest zwykle hello takie same jak nazwa klastra hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-318">**Azure container name** : This is hello default container name for hello cluster, and is typically hello same as hello cluster name.</span></span> <span data-ttu-id="081eb-319">W przypadku klastra o nazwie "abc123" jest po prostu abc123.</span><span class="sxs-lookup"><span data-stu-id="081eb-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="081eb-320">**Tabeli Życzymy tooquery przy użyciu hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning musi być wewnętrznej tabeli.**</span><span class="sxs-lookup"><span data-stu-id="081eb-320">**Any table we wish tooquery using hello [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="081eb-321">Porada na określenie, czy tabela T w bazie danych D.db wewnętrznej tabeli ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="081eb-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="081eb-322">Z hello gałęzi katalogu wierszu polecenia hello problemu:</span><span class="sxs-lookup"><span data-stu-id="081eb-322">From hello Hive directory prompt, issue hello command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="081eb-323">Jeśli zostanie wprowadzony hello jest wewnętrzna tabela, jego zawartość musi wskazywać tutaj.</span><span class="sxs-lookup"><span data-stu-id="081eb-323">If hello table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="081eb-324">Inny sposób toodetermine czy tabeli wewnętrznej tabeli jest hello toouse Eksploratora usługi Storage platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="081eb-324">Another way toodetermine whether a table is an internal table is toouse hello Azure Storage Explorer.</span></span> <span data-ttu-id="081eb-325">Użyj jej nazwa kontenera domyślnego toohello toonavigate hello klastra, a następnie Filtruj według nazwy tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-325">Use it toonavigate toohello default container name of hello cluster, and then filter by hello table name.</span></span> <span data-ttu-id="081eb-326">Jeśli tabela hello i jego zawartość występuje, to potwierdzenie jest wewnętrznej tabeli.</span><span class="sxs-lookup"><span data-stu-id="081eb-326">If hello table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="081eb-327">W tym miejscu jest migawką hello zapytań Hive i hello [i zaimportuj dane] [ import-data] modułu:</span><span class="sxs-lookup"><span data-stu-id="081eb-327">Here is a snapshot of hello Hive query and hello [Import Data][import-data] module:</span></span>

![Zapytanie hive dla modułu importowanie danych](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="081eb-329">Od naszej próbki danych znajduje się w kontenerze domyślna hello dół, hello wynikowe zapytanie Hive z usługi Azure Machine Learning jest bardzo prosty i jest tylko "Wybierz * z nyctaxidb.nyctaxi\_próbkowane w dół\_danych".</span><span class="sxs-lookup"><span data-stu-id="081eb-329">Note that since our down sampled data resides in hello default container, hello resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="081eb-330">zestaw danych Hello teraz może być używany jako punkt początkowy dla budowania modeli uczenia maszynowego hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-330">hello dataset may now be used as hello starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="081eb-331"><a name="mlmodel"></a>Tworzenie modeli w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="081eb-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="081eb-332">Możemy teraz stanie tooproceed toomodel tworzenia i wdrażania modelu w [usługi Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="081eb-332">We are now able tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="081eb-333">dane Hello jest gotowy do nas toouse w rozwiązywaniu problemów prognozowania hello określonych powyżej:</span><span class="sxs-lookup"><span data-stu-id="081eb-333">hello data is ready for us toouse in addressing hello prediction problems identified above:</span></span>

<span data-ttu-id="081eb-334">**1. Klasyfikacji binarnej**: toopredict czy poradę został płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="081eb-334">**1. Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="081eb-335">**Uczeń używane:** Regresja logistyczna Two-class</span><span class="sxs-lookup"><span data-stu-id="081eb-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="081eb-336">a.</span><span class="sxs-lookup"><span data-stu-id="081eb-336">a.</span></span> <span data-ttu-id="081eb-337">W przypadku tego problemu naszą etykietę docelowego (lub klasy) jest "Przechylony".</span><span class="sxs-lookup"><span data-stu-id="081eb-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="081eb-338">Nasze oryginalnego zestawu danych próbkowania w dół ma kilka kolumn, które są przecieki docelowych do tego eksperymentu klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="081eb-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="081eb-339">W szczególności: Porada\_klasy, porada\_kwota i całkowitej\_ilość ujawniania informacji na temat hello etykiety docelowej, która nie jest dostępny na czas testowania.</span><span class="sxs-lookup"><span data-stu-id="081eb-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="081eb-340">Firma Microsoft Usuń te kolumny z brany pod uwagę przy użyciu hello [Select Columns in Dataset] [ select-columns] modułu.</span><span class="sxs-lookup"><span data-stu-id="081eb-340">We remove these columns from consideration using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="081eb-341">migawki Hello poniżej zawiera naszych toopredict eksperymentu czy poradę został płatnej dla danego podróży.</span><span class="sxs-lookup"><span data-stu-id="081eb-341">hello snapshot below shows our experiment toopredict whether or not a tip was paid for a given trip.</span></span>

![Migawki eksperymentu](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="081eb-343">b.</span><span class="sxs-lookup"><span data-stu-id="081eb-343">b.</span></span> <span data-ttu-id="081eb-344">W tym eksperymencie naszych dystrybucje etykiety docelowego zostały około 1:1.</span><span class="sxs-lookup"><span data-stu-id="081eb-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="081eb-345">migawki Hello poniżej przedstawia dystrybucji hello etykiet klasy Porada hello problemu klasyfikacji binarnej.</span><span class="sxs-lookup"><span data-stu-id="081eb-345">hello snapshot below shows hello distribution of tip class labels for hello binary classification problem.</span></span>

![Dystrybucji Porada etykiet — klasa](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="081eb-347">W związku z tym możemy uzyskać AUC 0.987, jak pokazano na poniższej ilustracji hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-347">As a result, we obtain an AUC of 0.987 as shown in hello figure below.</span></span>

![Wartość AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="081eb-349">**2. Wieloklasowej klasyfikacji**: zakres hello toopredict kwot Porada uregulowaniu płatności hello podróży, za pomocą hello wcześniej zdefiniowany klasy.</span><span class="sxs-lookup"><span data-stu-id="081eb-349">**2. Multiclass classification**: toopredict hello range of tip amounts paid for hello trip, using hello previously defined classes.</span></span>

<span data-ttu-id="081eb-350">**Uczeń używane:** Wieloklasowej Regresja logistyczna</span><span class="sxs-lookup"><span data-stu-id="081eb-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="081eb-351">a.</span><span class="sxs-lookup"><span data-stu-id="081eb-351">a.</span></span> <span data-ttu-id="081eb-352">W przypadku tego problemu jest naszą etykietę docelowego (lub klasy) "Porada\_klasy" może to zająć jednej z pięciu wartości (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="081eb-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="081eb-353">Jak w przypadku klasyfikacji binarnej hello mamy kilka kolumn, które są przecieki docelowych do tego eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="081eb-353">As in hello binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="081eb-354">W szczególności: Przechylony, porada\_łączna kwota\_ilość ujawniania informacji na temat hello etykiety docelowej, która nie jest dostępny na czas testowania.</span><span class="sxs-lookup"><span data-stu-id="081eb-354">In particular : tipped, tip\_amount, total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="081eb-355">Firma Microsoft Usuń te kolumny za pomocą hello [Select Columns in Dataset] [ select-columns] modułu.</span><span class="sxs-lookup"><span data-stu-id="081eb-355">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="081eb-356">Hello migawki poniżej przedstawia naszych toopredict eksperymentu, w których bin Porada jest prawdopodobnie toofall (klasa 0: Porada = $0, 1 — klasa: Porada > $0 i Porada < = $5, klasy 2: Porada > $5 i Porada < = $10 klasy 3: Porada > $10 i Porada < = $20 Klasa 4: Porada > $20)</span><span class="sxs-lookup"><span data-stu-id="081eb-356">hello snapshot below shows our experiment toopredict in which bin a tip is likely toofall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Migawki eksperymentu](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="081eb-358">Teraz Pokaż się wygląd naszego dystrybucji klasy rzeczywiste testu.</span><span class="sxs-lookup"><span data-stu-id="081eb-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="081eb-359">Widzimy, że klasa 0 i 1 klasy są powszechnie znane, hello innych klas są rzadko.</span><span class="sxs-lookup"><span data-stu-id="081eb-359">We see that while Class 0 and Class 1 are prevalent, hello other classes are rare.</span></span>

![Testowanie dystrybucji — klasa](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="081eb-361">b.</span><span class="sxs-lookup"><span data-stu-id="081eb-361">b.</span></span> <span data-ttu-id="081eb-362">W tym eksperymencie używamy toolook macierzy pomyłek w naszym dokładności przewidywania.</span><span class="sxs-lookup"><span data-stu-id="081eb-362">For this experiment, we use a confusion matrix toolook at our prediction accuracies.</span></span> <span data-ttu-id="081eb-363">Jest to pokazane poniżej.</span><span class="sxs-lookup"><span data-stu-id="081eb-363">This is shown below.</span></span>

![Macierz pomyłek](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="081eb-365">Należy pamiętać, że naszych dokładności klasy w klasach powszechnie hello jest bardzo dobre, hello modelu, które nie są dobrym zadanie "learning" w klasach rzadkich hello.</span><span class="sxs-lookup"><span data-stu-id="081eb-365">Note that while our class accuracies on hello prevalent classes is quite good, hello model does not do a good job of "learning" on hello rarer classes.</span></span>

<span data-ttu-id="081eb-366">**3. Zadanie regresji**: toopredict hello ilość Porada płatnej w podróży.</span><span class="sxs-lookup"><span data-stu-id="081eb-366">**3. Regression task**: toopredict hello amount of tip paid for a trip.</span></span>

<span data-ttu-id="081eb-367">**Uczeń używane:** Boosted drzewa decyzyjnego</span><span class="sxs-lookup"><span data-stu-id="081eb-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="081eb-368">a.</span><span class="sxs-lookup"><span data-stu-id="081eb-368">a.</span></span> <span data-ttu-id="081eb-369">W przypadku tego problemu jest naszą etykietę docelowego (lub klasy) "Porada\_kwota".</span><span class="sxs-lookup"><span data-stu-id="081eb-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="081eb-370">Nasze przecieki docelowego w tym przypadku są: Przechylony, porada\_klasy całkowita\_kwota; te zmienne ujawnienie informacji na temat kwota Porada hello jest zazwyczaj niedostępna na czas testowania.</span><span class="sxs-lookup"><span data-stu-id="081eb-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about hello tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="081eb-371">Firma Microsoft Usuń te kolumny za pomocą hello [Select Columns in Dataset] [ select-columns] modułu.</span><span class="sxs-lookup"><span data-stu-id="081eb-371">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="081eb-372">belows migawki Hello przedstawiający kwotę hello toopredict eksperymentu naszych hello podane poradę.</span><span class="sxs-lookup"><span data-stu-id="081eb-372">hello snapshot belows shows our experiment toopredict hello amount of hello given tip.</span></span>

![Migawki eksperymentu](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="081eb-374">b.</span><span class="sxs-lookup"><span data-stu-id="081eb-374">b.</span></span> <span data-ttu-id="081eb-375">W przypadku problemów regresji mierzymy hello dokładności przewidywania naszych analizując hello kwadrat błąd prognoz hello, hello współczynnik determinacji i Witaj, takich jak.</span><span class="sxs-lookup"><span data-stu-id="081eb-375">For regression problems, we measure hello accuracies of our prediction by looking at hello squared error in hello predictions, hello coefficient of determination, and hello like.</span></span> <span data-ttu-id="081eb-376">Zostanie przedstawiony je poniżej.</span><span class="sxs-lookup"><span data-stu-id="081eb-376">We show these below.</span></span>

![Statystyki prognozowania](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="081eb-378">Widzimy o hello współczynnik determinacji jest 0.709, podejrzeń około 71% wariancję hello tłumaczy naszych współczynników modelu.</span><span class="sxs-lookup"><span data-stu-id="081eb-378">We see that about hello coefficient of determination is 0.709, implying about 71% of hello variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="081eb-379">więcej informacji na temat usługi Azure Machine Learning toolearn i w jaki sposób tooaccess i użyj go, zobacz zbyt[co to jest Machine Learning?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="081eb-379">toolearn more about Azure Machine Learning and how tooaccess and use it, please refer too[What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="081eb-380">Zasób przydatne do odtwarzania z licznych eksperymenty uczenia maszynowego w usłudze Azure Machine Learning to hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="081eb-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="081eb-381">Galeria Hello obejmuje gamy eksperymenty i zapewnia kompleksowy wprowadzenia hello zakres możliwości usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="081eb-381">hello Gallery covers a gamut of experiments and provides a thorough introduction into hello range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="081eb-382">Informacje o licencji</span><span class="sxs-lookup"><span data-stu-id="081eb-382">License Information</span></span>
<span data-ttu-id="081eb-383">Ten przewodnik próbki i jego towarzyszący skrypty są udostępniane przez firmę Microsoft hello MIT licencji.</span><span class="sxs-lookup"><span data-stu-id="081eb-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="081eb-384">Sprawdź plik LICENSE.txt hello w katalogu hello hello przykładowy kod w serwisie GitHub więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="081eb-384">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="081eb-385">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="081eb-385">References</span></span>
<span data-ttu-id="081eb-386">• [Andrés Monroy taksówki NYC rund stronę pobierania](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="081eb-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="081eb-387">• [FOILing NYC taksówki podróży danych przez Krzysztof Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="081eb-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="081eb-388">• [Taksówki NYC i Limousine Komisji badań i statystyki](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="081eb-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
