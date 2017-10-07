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
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a>Hello proces nauki danych zespołu w działaniu: przy użyciu magazynu danych SQL
W tym samouczku, możemy opisano tworzenie i wdrażanie modelu uczenia maszynowego przy użyciu magazynu danych SQL (SQL DW) dla elementu dataset publicznie dostępnych — hello [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych. model klasyfikacji binarnej Hello skonstruowany prognozuje czy poradę ma być stosowany w podróży i modele wieloklasowej klasyfikacji i regresji omówiono także które prognozowania hello dystrybucji dla kwoty Porada hello płatnej.

procedury Hello następuje hello [zespołu danych nauki procesu (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) przepływu pracy. Zostanie przedstawiony sposób toosetup środowisku nauki danych jak tooload hello danych do magazynu danych SQL i sposobie używania magazynu danych SQL lub notesu IPython tooexplore hello danych i odtwarzania funkcji toomodel. Następnie zostanie przedstawiony sposób toobuild i wdrażanie modelu przy użyciu usługi Azure Machine Learning.

## <a name="dataset"></a>Witaj NYC taksówki rund w zestawie danych
Hello podróży taksówki NYC danych składa się z około 20GB skompresowanego plików CSV (~ 48GB nieskompresowane), rejestrowanie ponad milion 173 poszczególnych podróży i hello cen w klasie ekonomicznej płatnej w odniesieniu do każdej podróży. Każdy rekord podróży zawiera hello odbiór i przyjmowania lokalizacje i godziny anonimowe hack numer licencji (sterownik) i hello numer Medalionu (taksówki jego unikatowy identyfikator). Hello danych obejmuje wszystkie rund w roku hello 2013 i jest dostępne w powitania po dwóch zestawów danych dla każdego miesiąca:

1. Witaj **trip_data.csv** plik zawiera szczegóły podróży, takie jak liczba pasażerów, punkty odbiór i dropoff, czas trwania podróży i długość podróży. Poniżej przedstawiono kilka przykładowych rekordów:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Witaj **trip_fare.csv** pliku zawiera szczegółowe informacje o klasie hello za każdym razem, takie jak typ płatności, kwota taryfy przeciążenia i podatków, porady i przejazd i Suma hello płatnej. Poniżej przedstawiono kilka przykładowych rekordów:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Witaj **Unikatowy klucz** używane podróży toojoin\_danych i podróży\_taryfy składa się z hello następujące trzy pola:

* Medalionu,
* Funkcja\_licencji i
* pobranie\_daty/godziny.

## <a name="mltasks"></a>Adres trzy typy zadań prognozowania
Firma Microsoft sformułować trzy problemów prognozowania oparte na powitania *Porada\_kwota* tooillustrate trzy rodzaje modelowania zadań:

1. **Klasyfikacji binarnej**: toopredict czy poradę został płatnej podróży, tj. *Porada\_kwota* większą niż $0 jest przykład dodatnią, podczas gdy *Porada\_kwota* $ 0 to przykład ujemna.
2. **Wieloklasowej klasyfikacji**: zakres hello toopredict porady uregulowaniu płatności hello podróży. Możemy podzielić hello *Porada\_kwota* do pięciu bins lub klasy:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Zadanie regresji**: toopredict hello ilość Porada płatnej w podróży.  

## <a name="setup"></a>Konfigurowanie środowiska nauki danych Azure hello zaawansowana analityka
tooset Twojego środowiska nauki danych Azure, wykonaj następujące kroki.

**Utwórz własne konto magazynu obiektów blob platformy Azure**

* Podczas obsługi administracyjnej magazynu obiektów blob platformy Azure, wybierz lokalizację geograficzną magazynu obiektów blob platformy Azure w lub możliwie najbliżej zbyt**południowo-środkowe stany**, czyli przechowywania hello taksówki NYC danych. Witaj, dane zostaną skopiowane przy użyciu narzędzia AzCopy z hello publicznym kontenerze obiektów blob magazynu kontenera tooa na koncie magazynu. Witaj bliżej magazynu obiektów blob platformy Azure jest tooSouth środkowe stany USA, hello szybciej (krok 4) będzie można ukończyć tego zadania.
* Konto magazynu Azure toocreate, hello wykonaj kroki opisane w [kont magazynu Azure o](../storage/common/storage-create-storage-account.md). Być czy toomake uwagi o wartości hello następujące poświadczenia konta magazynu, które będą potrzebne w dalszej części tego przewodnika.
  
  * **Nazwa konta magazynu**
  * **Klucz konta magazynu**
  * **Nazwa kontenera** (które mają hello toobe danych przechowywanych w hello magazynu obiektów blob platformy Azure)

**Udostępnij wystąpienie magazynu danych SQL Azure.**
Postępuj zgodnie z dokumentacją hello na [Tworzenie usługi SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision wystąpienie usługi SQL Data Warehouse. Upewnij się, odpowiednie notacji na powitania po poświadczeń magazynu danych SQL, które będą używane w kolejnych krokach.

* **Nazwa serwera**: <server Name>. database.windows.net
* **Nazwa SQLDW (baza danych)**
* **Nazwa użytkownika**
* **Hasło**

**Zainstaluj program Visual Studio i SQL Server Data Tools.** Aby uzyskać instrukcje, zobacz [instalacji programu Visual Studio 2015 i/lub program SSDT (SQL Server Data Tools) dla usługi SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).

**Połącz tooyour magazynu danych SQL Azure z programem Visual Studio.** Aby uzyskać instrukcje, zobacz kroki 1 i 2 w [tooAzure SQL Data Warehouse Uzyskuj dostęp do programu Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).

> [!NOTE]
> Uruchom hello następujące zapytanie SQL w bazie danych hello utworzonego w magazynie danych programu SQL (zamiast hello zapytania w kroku 3 hello połączyć tematu) zbyt**utworzyć klucz główny**.
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

**Tworzenie obszaru roboczego uczenia maszynowego Azure w ramach Twojej subskrypcji platformy Azure.** Aby uzyskać instrukcje, zobacz [Utwórz obszar roboczy usługi Azure Machine Learning](machine-learning-create-workspace.md).

## <a name="getdata"></a>Ładowanie danych hello do usługi SQL Data Warehouse
Otwórz konsolę polecenia programu Windows PowerShell. Uruchom hello następujące polecenia programu PowerShell toodownload hello przykład SQL pliki skryptów, które firma Microsoft udostępnia użytkownikowi na GitHub tooa katalog lokalny, który określisz z parametrem hello *- DestDir*. Można zmienić wartości parametru hello *- DestDir* tooany katalogu lokalnego. Jeśli *- DestDir* nie istnieje, zostanie on utworzony przez hello skrypt programu PowerShell.

> [!NOTE]
> Może być konieczne zbyt**Uruchom jako Administrator** podczas wykonywania następującego skryptu programu PowerShell, jeśli hello Twojej *DestDir* katalog musi tooit toocreate lub toowrite uprawnień administratora.
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

Po pomyślnym wykonaniu bieżący katalog roboczy zmienia zbyt*- DestDir*. Powinno być możliwe toosee ekran, tak jak poniżej:

![][19]

W Twojej *- DestDir*, wykonać hello następującego skryptu programu PowerShell w trybie administratora:

    ./SQLDW_Data_Import.ps1

Po uruchomieniu hello skrypt programu PowerShell dla powitania po raz pierwszy, użytkownik zostanie poproszony tooinput hello informacji z Twojego magazynu danych SQL Azure i konta magazynu obiektów blob platformy Azure. Po zakończeniu tego skryptu PowerShell uruchomiona powitania po raz pierwszy, poświadczenia hello wprowadzania można będzie został napisany pliku konfiguracji tooa SQLDW.conf w katalogu roboczym obecny hello. Witaj przyszłych uruchamianie tego pliku skryptu programu PowerShell ma tooread opcji hello wszystkie niezbędne parametry z tego pliku konfiguracji. Należy toochange niektórych parametrów można wybrać tooinput parametry hello na ekranie powitania na monit o usunięcie tego pliku konfiguracji i wprowadzanie wartości parametrów hello w lub wartości parametrów hello toochange, edytując plik SQLDW.conf hello w Twojej *- DestDir* katalogu.

> [!NOTE]
> W kolejności tooavoid schematu nazwa powoduje konflikt z tymi, które już istnieją w Twojej SQL DW Azure podczas odczytywania parametrów bezpośrednio z pliku SQLDW.conf hello 3-cyfrowy numer losowe zostanie dodany toohello nazwy schematu z pliku SQLDW.conf hello jako nazwę schematu domyślnego hello każdym uruchomieniu. Witaj skrypt programu PowerShell może wyświetlenie monitu o nazwę schematu: można określić nazwę hello uznania użytkownika.
> 
> 

To **skrypt programu PowerShell** pliku zakończeniu hello następujące zadania:

* **Pobiera i instaluje narzędzie AzCopy**, jeśli nie zainstalowano narzędzia AzCopy
  
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
* **Kopiuje dane tooyour prywatnego obiektu blob magazynu konta** z hello publicznego obiektu blob z narzędzia AzCopy
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* **Ładuje dane przy użyciu programu Polybase (wykonując LoadDataToSQLDW.sql) tooyour Azure SQL DW** z konta prywatnego obiektu blob magazynu z hello następujące polecenia.
  
  * Tworzenie schematu
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * Tworzenie poświadczeń o zakresie bazy danych
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * Tworzenie zewnętrznego źródła danych dla obiektu blob magazynu Azure
    
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
  * Tworzenie zewnętrznego formatu pliku dla pliku csv. Jest nieskompresowanych danych i pola są oddzielone znakiem hello znaku kreski pionowej.
    
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
  * Tworzenie zewnętrznego taryfy i tabele podróży dla zestawu danych taksówki NYC w magazynie obiektów blob platformy Azure.
    
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

    - Ładowanie danych z tabel zewnętrznych w tooSQL magazynu obiektów blob platformy Azure magazynu danych

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

    - Utwórz tabelę danych przykładowych (NYCTaxi_Sample) i Wstaw tooit danych z wybranie zapytania SQL w tabelach podróży i taryfy hello. (Niektóre kroki tego przewodnika wymaga toouse tej tabeli.)

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

Lokalizacja geograficzna Hello kont magazynu ma wpływ na czas ładowania.

> [!NOTE]
> W zależności od hello lokalizację geograficzną konto magazynu obiektów blob prywatne, hello proces kopiowania danych z konta magazynu prywatnego tooyour publicznego obiektu blob może potrwać około 15 minut lub nawet dłużej który hello proces ładowania danych z konta magazynu tooyour Azure SQL DW może potrwać 20 minut lub dłużej.  
> 
> 

Konieczne będzie toodecide co zrobić, jeśli masz zduplikowanego źródła i pliki docelowe.

> [!NOTE]
> Jeśli toobe plików CSV hello skopiowane z konta magazynu prywatnego obiektu blob tooyour hello publicznego obiektu blob magazynu już istnieje w konto magazynu obiektów blob prywatne, AzCopy zapyta, czy ma toooverwrite je. Jeśli nie chcesz toooverwrite ich, wejściowych  **n**  po wyświetleniu monitu. Jeśli chcesz, aby toooverwrite **wszystkie** z nich, wprowadź **** po wyświetleniu monitu. Możesz również wpisać **y** CSV toooverwrite pliki pojedynczo.
> 
> 

![Wykreślenia #21][21]

Można użyć własnych danych. Jeśli do komputera lokalnego w aplikacji rzeczywistych danych, można nadal używać narzędzia AzCopy tooupload lokalnych danych tooyour prywatnego magazynu Azure blob storage. Wystarczy toochange hello **źródła** lokalizacji, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, w hello AzCopy polecenie hello PowerShell skryptu pliku toohello katalog lokalny, który zawiera dane.

> [!TIP]
> Jeśli dane są już w magazynie obiektów blob platformy Azure prywatnych w rzeczywistych aplikacji, można pominąć hello AzCopy kroku w hello skrypt programu PowerShell i przekazać bezpośrednio hello tooAzure danych magazynu danych SQL. Wymaga to, że dodatkowe edytuje z tootailor skryptu hello ją toohello format danych.
> 
> 

Ten skrypt programu Powershell również podłącza hello Azure SQL DW informacji do hello eksploracji przykładowe pliki danych SQLDW_Explorations.sql, SQLDW_Explorations.ipynb i SQLDW_Explorations_Scripts.py tak, aby te trzy pliki są gotowe toobe wypróbowane natychmiast Po zakończeniu hello skrypt programu PowerShell.

Po pomyślnym wykonaniu, zostanie wyświetlony ekran, takich jak poniżej:

![][20]

## <a name="dbexplore"></a>Eksploracja danych i funkcji inżynieryjne w usłudze Azure SQL Data Warehouse
W tej sekcji możemy wykonywać Generowanie funkcji i eksploracja danych przez wykonywanie zapytań SQL magazynu danych SQL Azure bezpośrednio przy użyciu **programu Visual Studio Tools danych**. Wszystkie zapytania SQL w tej sekcji znajdują się w hello przykładowy skrypt o nazwie *SQLDW_Explorations.sql*. Ten plik został już pobrany tooyour katalogu lokalnego za pomocą skryptu programu PowerShell hello. Można również pobrać go z [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql). Ale plik hello w serwisie GitHub nie ma informacji magazynu danych SQL Azure hello podłączony.

Połącz tooyour magazynu danych SQL Azure za pomocą programu Visual Studio o nazwie logowania SQL DW hello i hasła i otwarcie hello **Eksplorator obiektów SQL** tooconfirm hello w bazie danych i tabele zostały zaimportowane. Pobrać hello *SQLDW_Explorations.sql* pliku.

> [!NOTE]
> tooopen edytorze zapytań równoległych magazynu danych (PDW), użyj hello **nowe zapytanie** polecenia aż do Twojej PDW wybrano hello **Eksplorator obiektów SQL**. Witaj standardowego edytora zapytań SQL nie jest obsługiwany przez PDW.
> 
> 

W tym miejscu są dane typu hello eksploracji i funkcji generowania wykonywane w tej sekcji:

* Eksplorowanie danych dystrybucji kilka pól w różnym czasie systemu windows.
* Zbadaj jakości danych hello pól długości i szerokości geograficznej.
* Generowanie etykiet klasyfikacji binarnej i wieloklasowej oparte na powitania **Porada\_kwota**.
* Generowanie funkcji i obliczeń lub porównania odległości podróży.
* Dołącz Witaj dwie tabele i Wyodrębnij losowej próbki, które będzie używane toobuild modeli.

### <a name="data-import-verification"></a>Weryfikacja importu danych
Kwerendy te zapewniają szybki weryfikacji hello liczby wierszy i kolumn w powitalne zaimportować tabele wypełniać wcześniej przy użyciu zbiorczego równoległe w programie Polybase,

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

**Dane wyjściowe:** należy pobrać 173,179,759 wierszy i kolumn 14.

### <a name="exploration-trip-distribution-by-medallion"></a>Eksploracja: Podróży dystrybucji przez Medalionu
To przykładowe zapytanie identyfikuje medallions hello (taksówki numery) wykonanych więcej niż 100 rund w określonym przedziale czasu. Zapytanie Hello korzystałby z hello na partycje tabeli dostępu, ponieważ należy przygotować przez schemat partycji hello **podnoszenia\_datetime**. Badania hello pełnego zestawu danych będzie również używać tabeli partycjonowanej hello i/lub indeksu skanowania.

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

**Dane wyjściowe:** zapytań hello powinien zwraca tabelę z wierszami Określanie hello 13,369 medallions (taksówkach) i hello Liczba podróży zakończone przez nich 2013. Witaj ostatnia kolumna zawiera liczby hello hello liczby rund ukończone.

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Eksploracja: Podróży dystrybucji Medalionu i hack_license
W tym przykładzie identyfikuje hello medallions (taksówki cyfry) i hack_license cyfry (sterowniki) zakończona ponad 100 rund w określonym przedziale czasu.

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

**Dane wyjściowe:** zapytania hello powinien zwrócić tabelę z wierszami 13,369 określenie hello 13,369 samochodu/driver identyfikatorów, które ukończyły bardziej tego 100 rund w 2013. Witaj ostatnia kolumna zawiera liczby hello hello liczby rund ukończone.

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Ocena jakości danych: Weryfikuj rekordy z geograficzne niepoprawne i/lub szerokość geograficzną
W tym przykładzie sprawdza, czy hello geograficzne i/lub szerokość geograficzną polach albo zawiera nieprawidłową wartość (stopni w radianach powinna należeć do zakresu od-90 do 90,) lub (0, 0) współrzędnych.

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

**Dane wyjściowe:** hello zapytanie zwraca 837,467 podróży, które mają nieprawidłowe pola geograficzne i/lub szerokość geograficzną.

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Eksploracja: Przechylony a nie Przechylony rund dystrybucji
W tym przykładzie znajduje hello Liczba podróży, które zostały Przechylony a numer hello, które nie zostały Przechylony w określonym przedziale czasu (lub hello pełnego zestawu danych, jeśli obejmujące cały rok hello, jak jest skonfigurowana w tym miejscu). Tej dystrybucji odzwierciedla toobe dystrybucji binarne etykiety hello później użyć do modelowania klasyfikacji binarnej.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

**Dane wyjściowe:** hello zapytania należy następujące zwracany hello Porada częstotliwości hello roku 2013: 90,447,622 Przechylony i 82,264,709 Przechylony nie.

### <a name="exploration-tip-classrange-distribution"></a>Eksploracja: Porada klasy/zakres dystrybucji
W tym przykładzie oblicza dystrybucji hello Porada zakresów w danym momencie okres (lub w hello pełnego zestawu danych jeśli obejmujące cały rok hello). Jest to dystrybucji hello hello etykiety klas, które będą później używane do modelowania wieloklasowej klasyfikacji.

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

**Dane wyjściowe:**

| tip_class | tip_freq |
| --- | --- |
| 1 |82230915 |
| 2 |6198803 |
| 3 |1932223 |
| 0 |82264625 |
| 4 |85765 |

### <a name="exploration-compute-and-compare-trip-distance"></a>Eksploracja: Obliczania i porównać odległość podróży
W tym przykładzie konwertuje hello odbiór i przyjmowania geograficzne i współrzędne geograficzne tooSQL punktów, oblicza odległość podróży hello przy użyciu różnicę punktów geograficzne SQL i zwraca losowej próbki hello wyniki do porównania. przykład Witaj ogranicza wyniki hello toovalid koordynuje tylko przy użyciu objętych wcześniej hello danych jakości oceny zapytania.

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

### <a name="feature-engineering-using-sql-functions"></a>Funkcja engineering przy użyciu funkcji SQL
Czasami funkcje SQL mogą być wydajne opcję engineering funkcji. W tym przewodniku zdefiniowanego SQL funkcja toocalculate hello bezpośredniego odległości między lokalizacjami odbiór i dropoff hello. Możesz uruchomić hello następujące skrypty SQL w **programu Visual Studio Tools danych**.

Oto hello SQL skrypt, który definiuje funkcję odległość hello.

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

Oto przykład toocall funkcje toogenerate tej funkcji w zapytaniu SQL:

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

**Dane wyjściowe:** to zapytanie generuje tabeli (z 2,803,538 wierszy) z odbiór i dropoff długości i szerokości geograficzne i hello odpowiadająca odległości w milach bezpośrednie. Poniżej przedstawiono wyniki hello pierwsze 3 wiersze:

|  | pickup_latitude | pickup_longitude | dropoff_latitude | dropoff_longitude | DirectDistance |
| --- | --- | --- | --- | --- | --- |
| 1 |40.731804 |-74.001083 |40.736622 |-73.988953 |.7169601222 |
| 2 |40.715794 |-74,010635 |40.725338 |-74.00399 |.7448343721 |
| 3 |40.761456 |-73.999886 |40.766544 |-73.988228 |0.7037227967 |

### <a name="prepare-data-for-model-building"></a>Przygotowanie do tworzenia modelu danych
Witaj następujące zapytanie sprzęga hello **nyctaxi\_podróży** i **nyctaxi\_taryfy** tabel, generuje etykiety klasyfikacji binarnej **Przechylony**, etykiety klasyfikacji wielu klasy **Porada\_klasy**i wyodrębnia próbki z hello pełnego dołączonego do zestawu danych. próbkowanie Hello odbywa się przez pobranie podzbiór rund hello na podstawie czasu odbioru.  To zapytanie może skopiować następnie wkleić bezpośrednio w hello [Azure Machine Learning Studio](https://studio.azureml.net) [i zaimportuj dane] [ import-data] modułu dla wprowadzanie danych bezpośrednio z wystąpienia bazy danych SQL hello na platformie Azure. Zapytanie Hello wyklucza rekordy z niepoprawne (0, 0) współrzędnych.

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

Gdy są gotowe tooproceed tooAzure uczenia maszynowego, użytkownik może:  

1. Zapisz hello końcowego SQL kwerendy tooextract i przykładowa hello danych i kopiowania i wklejania hello zapytanie bezpośrednio do [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning, lub
2. Utrwalanie hello próbkowany i odtworzone danych planujesz toouse modelu tworzenie w nowej SQL DW tabeli i korzystanie z nowej tabeli hello w hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning. Witaj skrypt programu PowerShell w poprzednim kroku ma zostało to zrobione automatycznie. Możesz przeczytać bezpośrednio z tej tabeli w hello importowanie danych modułu.

## <a name="ipnb"></a>Eksploracja danych i funkcji inżynieryjne w notesie IPython
W tej sekcji zostaną wykonane Eksplorowanie danych oraz generowanie funkcji za pomocą obu Python i zapytań SQL hello SQL DW utworzony wcześniej. Przykładowe IPython Notes o nazwie **SQLDW_Explorations.ipynb** plik skryptu języka Python **SQLDW_Explorations_Scripts.py** zostały pobrane tooyour katalogu lokalnego. Są również dostępne na [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW). Te dwa pliki są identyczne w skryptach Python. plik skryptu języka Python Hello podano tooyou w przypadku, gdy nie masz serwera IPython notesu. Te dwa przykładowe Python plików zostały zaprojektowane pod **Python 2.7**.

Witaj potrzebnych informacji magazynu danych SQL Azure w przykładowym hello notesu IPython i hello Python komputera lokalnego tooyour pobranego pliku skryptu został podłączony za pomocą skryptu programu PowerShell hello wcześniej. Są one wykonywalny bez żadnych modyfikacji.

Jeśli obszar roboczy uczenie maszynowe Azure zostały już skonfigurowane, możesz bezpośrednio Przekaż przykładowe hello usługi uczenie maszynowe Azure IPython notesu toohello notesu IPython i jej uruchamianie. Poniżej przedstawiono hello kroki tooupload tooAzureML notesu IPython usługi:

1. Zaloguj się w tooyour uczenie maszynowe Azure w obszarze roboczym, kliknij przycisk "Studio" u góry hello, a następnie kliknij przycisk "Komputery przenośne", po lewej stronie powitania hello strony sieci web.
   
    ![Wykreślenia #22][22]
2. Kliknij "Nowy" hello lewym dolnym rogu strony sieci web hello i wybierz pozycję "Python 2". Następnie podaj nazwę notesu toohello i kliknij hello znacznik wyboru toocreate hello nowego pustego IPython notesu.
   
    ![Wykreślenia #23][23]
3. Kliknij symbol "Jupyter" hello na powitania lewym górnym rogu hello nowy notes IPython.
   
    ![Wykreślenia #24][24]
4. Przeciągnij i upuść hello próbki notesu IPython toohello **drzewa** z usługi uczenie maszynowe Azure IPython notesu, a następnie kliknij przycisk **przekazać**. Przykładowe hello notesu IPython zostaną przekazane toohello usługi uczenie maszynowe Azure IPython notesu.
   
    ![Wykreślenia #25][25]

W kolejności toorun hello przykładowe notesu IPython lub hello pliku skryptu języka Python, hello następujące pakiety Python niezbędne. Jeśli używasz usługi uczenie maszynowe Azure IPython notesu hello te pakiety zostały wstępnie zainstalowane.

    - pandas
    - numpy
    - matplotlib
    - pyodbc
    - PyTables

Hello zalecany sekwencji, podczas tworzenia zaawansowanych rozwiązań analitycznych na uczenie maszynowe Azure z dużej ilości danych jest hello następujące czynności:

* Odczyt w małej przykładowej hello danych do ramki danych w pamięci.
* Wykonywanie niektórych wizualizacje i eksploracji przy użyciu danych hello próbkowane.
* Wypróbuj engineering funkcji przy użyciu danych hello próbkowane.
* Dla większych Eksploracja danych do manipulowania danymi i funkcji zespołu inżynieryjnego, użyj zapytania SQL tooissue Python bezpośrednio przed hello magazynu danych SQL.
* Zdecyduj, toobe rozmiar próbki hello odpowiednie do konstruowania modelu uczenia maszynowego Azure.

Po Hello są kilka Eksploracja danych, wizualizacji danych i przykłady engineering funkcji. Więcej eksploracji danych można znaleźć w przykładowych hello notesu IPython i hello przykładowy plik skryptu języka Python.

### <a name="initialize-database-credentials"></a>Inicjowanie poświadczenia bazy danych
Inicjowanie ustawienia połączenia bazy danych w hello następujące zmienne:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a>Utwórz połączenie z bazą danych
Oto hello parametry połączenia, które tworzy hello połączenia toohello w bazie danych.

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Raport liczba wierszy i kolumn w tabeli < nyctaxi_trip >
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

* Całkowita liczba wierszy = 173179759  
* Łączna liczba kolumn = 14

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a>Raport liczba wierszy i kolumn w tabeli < nyctaxi_fare >
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

* Całkowita liczba wierszy = 173179759  
* Łączna liczba kolumn = 11

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a>Odczytaj w przykładowych danych małych z hello bazy danych magazynu danych SQL
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

Czas tooread hello Przykładowa tabela jest 14.096495 sekund.  
Liczba wierszy i kolumn pobrać = (1000, 21).

### <a name="descriptive-statistics"></a>Statystyki opisowe
Teraz wszystko jest gotowe tooexplore hello próbce danych. Możemy zaczynać się patrzeć statystykami opisowy dla hello **podróży\_odległość** (lub inne pola, możesz wybrać toospecify).

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a>Wizualizacji: Przykład kreślenia pola
Następnie przyjrzymy się hello skrzynkowy dla hello podróży odległość toovisualize hello quantiles.

    df1.boxplot(column='trip_distance',return_type='dict')

![Wykreślenia #1][1]

### <a name="visualization-distribution-plot-example"></a>Wizualizacji: Przykład kreślenia dystrybucji
Wykresy, które wizualizacji hello dystrybucji i histogram hello próbkowany odległości podróży.

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Wykreślenia #2][2]

### <a name="visualization-bar-and-line-plots"></a>Wizualizacja: Pasek i geograficzne wiersza
W tym przykładzie firma Microsoft hello odległość podróży do pięciu bins bin i wizualizację hello binning wyników.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Firma Microsoft wykreślenia hello powyżej dystrybucji bin na pasku lub wiersz kreślenia z:

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Wykreślenia #3][3]

i

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Wykreślenia #4][4]

### <a name="visualization-scatterplot-examples"></a>Wizualizacji: Przykłady Scatterplot
Zostanie przedstawiony jest wykres punktowy między **podróży\_czasu\_w\_s** i **podróży\_odległość** toosee w przypadku dowolnego korelacji

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Wykreślenia #6][6]

Podobnie można sprawdzić hello relacji między **szybkość\_kod** i **podróży\_odległość**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Wykreślenia #8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a>Eksploracja danych na próbki danych za pomocą zapytań SQL w notesie IPython
W tej sekcji możemy Eksplorowanie danych dystrybucji przy użyciu danych hello próbkowany, którym jest umieszczany w nowej tabeli hello, utworzone powyżej. Należy pamiętać, że podobne eksploracji może zostać wykonane przy użyciu oryginalnego tabel hello.

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a>Eksploracja: Raport liczba wierszy i kolumn w hello próbkowany tabeli
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a>Eksploracja: Przechylony nie zwracać dystrybucji
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a>Eksploracja: Porada klasy dystrybucji
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a>Eksploracja: Wykreślenia hello Porada dystrybucji przez klasę
    tip_class_dist['tip_freq'].plot(kind='bar')

![#26 kreślenia][26]

#### <a name="exploration-daily-distribution-of-trips"></a>Eksploracji: Codzienne dystrybucji rund
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Eksploracja: Podróży dystrybucji na Medalionu
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a>Eksploracja: Podróży dystrybucji przez Medalionu i hack licencji
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a>Eksploracja: Podróży czasu dystrybucji
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a>Eksploracja: Podróży odległość dystrybucji
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a>Eksploracji: Dystrybucja typ płatności
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Sprawdź hello końcowego formę hello featurized tabeli
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <a name="mlmodel"></a>Tworzenie modeli w usłudze Azure Machine Learning
Firma Microsoft są teraz gotowe tooproceed toomodel tworzenia i wdrażania modelu w [usługi Azure Machine Learning](https://studio.azureml.net). dane Hello jest gotowy toobe używana w żadnym hello prognozowania problemy wcześniej, to znaczy:

1. **Klasyfikacji binarnej**: toopredict czy poradę został płatnej w podróży.
2. **Wieloklasowej klasyfikacji**: zakres hello toopredict porady płatnej, zgodnie z uprzednio zdefiniowanej klasy toohello.
3. **Zadanie regresji**: toopredict hello ilość Porada płatnej w podróży.  

toobegin hello modelowania wykonywania, zaloguj się za tooyour **usługi Azure Machine Learning** obszaru roboczego. Jeśli jeszcze nie utworzono obszaru roboczego uczenia maszynowego, zobacz [Utwórz obszar roboczy usługi Azure ML](machine-learning-create-workspace.md).

1. wprowadzenie do usługi Azure Machine Learning tooget zobacz [co to jest Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)
2. Zaloguj się za[Azure Machine Learning Studio](https://studio.azureml.net).
3. Strona główna Studio Hello zawiera wiele informacji, wideo, samouczki, toohello łącza odwołania moduły i innych zasobów. Aby uzyskać więcej informacji na temat usługi Azure Machine Learning, zapoznaj się hello [Centrum dokumentacji uczenia maszynowego Azure](https://azure.microsoft.com/documentation/services/machine-learning/).

Eksperyment typowe szkolenia składa się z hello następujące kroki:

1. Utwórz **+ nowy** eksperymentu.
2. Pobierz dane hello do uczenia Maszynowego Azure.
3. Wstępnie przetworzyć, transformacji i manipulować danymi hello, zgodnie z potrzebami.
4. Generowanie funkcji zgodnie z potrzebami.
5. Podział danych hello na zestawy szkoleniowe / / sprawdzanie poprawności danych (lub mieć osobne zestawy danych dla każdego).
6. Wybierz co najmniej jeden z algorytmów w zależności od hello learning problem toosolve uczenia maszynowego. Przykład klasyfikacji binarnej, wieloklasowej klasyfikacji, regresji.
7. Szkolenie co najmniej jednego modelu przy użyciu zestawu danych szkoleniowych hello.
8. Wynik przy użyciu modeli przeszkolone hello weryfikacji hello w zestawie danych.
9. Należy ocenić hello modele toocompute hello odpowiednich metryki dla hello uczenia problem.
10. Dopasuj hello modele i wybierz hello najlepsze toodeploy modelu.

W tym ćwiczeniu firma Microsoft ma już przedstawione odtwarzane hello danych w usłudze SQL Data Warehouse i na tooingest rozmiar próbki hello w uczenie Maszynowe Azure. Oto hello procedury toobuild co najmniej jeden modeli prognozowania hello:

1. Pobierz dane hello do uczenia Maszynowego Azure przy użyciu hello [importowanie danych] [ import-data] modułu dostępne w hello **danych wejściowych i wyjściowych** sekcji. Aby uzyskać więcej informacji, zobacz hello [i zaimportuj dane] [ import-data] strony odwołanie do modułu.
   
    ![Uczenie Maszynowe Azure i zaimportuj dane][17]
2. Wybierz **bazy danych SQL Azure** jako hello **źródła danych** w hello **właściwości** panelu.
3. Wprowadź nazwę DNS bazy danych hello w hello **nazwę serwera bazy danych** pola. Format:`tcp:<your_virtual_machine_DNS_name>,1433`
4. Wprowadź hello **Nazwa bazy danych** w hello odpowiednie pole.
5. Wprowadź hello *nazwa użytkownika SQL* w hello **nazwę konta użytkownika serwera**i hello *hasło* w hello **hasło konta użytkownika serwera**.
6. Sprawdź hello **dowolny certyfikat serwera Zaakceptuj** opcji.
7. W hello **zapytanie bazy danych** edytować obszaru tekstu, Wklej zapytanie hello wyciąg konieczne hello pola (w tym wszystkie pola obliczane takich jak etykiety hello) bazy danych i w dół przykłady hello danych toohello potrzeby próbkowania.

Przykładem eksperyment klasyfikacji binarnej odczytywanie danych bezpośrednio z bazy danych usługi SQL Data Warehouse hello jest hello rysunku poniżej (Pamiętaj tooreplace hello tabeli nazwy nyctaxi_trip i nyctaxi_fare przez schemat hello nazwy i hello tabeli nazwy używane w sieci Przewodnik). Podobne eksperymenty można utworzyć dla wieloklasowej klasyfikacji i regresji problemów.

![Azure ML pociągu][10]

> [!IMPORTANT]
> W hello modelowania wyodrębniania danych i pobierania próbek zapytania przykłady podane w poprzednich sekcjach **wszystkich etykiet ćwiczeń modelowania hello trzech znajdują się w zapytaniu hello**. Ważnym krokiem (wymagane) w każdym hello modelowania ćwiczenia jest zbyt**wykluczyć** hello niepotrzebnych etykiety hello innych dwa problemy oraz wszelkie inne **target przecieki**. Na przykład, korzystając z klasyfikacji binarnej, użyj etykiety hello **Przechylony** i wykluczyć pola hello **Porada\_klasy**, **Porada\_kwota**, i **całkowita\_kwota**. Hello te ostatnie są kupowane przecieki docelowy one zakłada Porada hello.
> 
> tooexclude wszystkie zbędne kolumny lub przecieki docelowych, można użyć hello [Select Columns in Dataset] [ select-columns] modułu lub hello [edytowanie metadanych] [ edit-metadata]. Aby uzyskać więcej informacji, zobacz [Select Columns in Dataset] [ select-columns] i [edytowanie metadanych] [ edit-metadata] odwołania stron.
> 
> 

## <a name="mldeploy"></a>Wdrażanie modeli w usłudze Azure Machine Learning
Gdy model jest gotowy, łatwo można go wdrożyć jako usługę sieci web bezpośrednio z hello eksperymentu. Aby uzyskać więcej informacji na temat wdrażania usług sieci web uczenie Maszynowe Azure, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy nową usługę sieci web, musisz:

1. Tworzenie eksperymentu oceniania.
2. Wdrażanie usługi sieci web hello.

toocreate oceniania Poeksperymentuj z **Zakończono** szkolenia eksperyment, kliknij przycisk **utworzyć OCENIANIA EKSPERYMENTU** hello dolnym pasku akcji.

![Ocenianie przez usługę Azure][18]

Usługa Azure Machine Learning podejmie toocreate eksperyment oceniania na podstawie składników hello eksperyment uczenia hello. W szczególności będzie:

1. Zapisz hello uczonego modelu i usuwanie modułów uczenia modelu hello.
2. Zidentyfikuj logicznych **port wejściowy** toorepresent hello oczekiwano schemat danych wejściowych.
3. Zidentyfikuj logicznych **output portu** schematem wyjściowym toorepresent hello oczekiwanego sieci web usługi.

Po utworzeniu hello oceniania eksperymentu, zapoznaj się z nim i upewnij się, Dopasuj zależnie od potrzeb. Typowy korekty jest wejściowy zestaw danych tooreplace hello i/lub zapytanie z taki, który wyklucza pola etykiety, jak te nie będą dostępne, gdy jest wywoływana hello usługi. Istnieje również wprowadzenia hello o rozmiarze hello tooreduce dobrym rozwiązaniem tooa zestawu danych i/lub zapytania kilka rekordów, schemat danych wejściowych hello wystarczającego tooindicate. Port wyjściowy hello, jest typowe tooexclude wszystkie pola i zawierać wyłącznie hello **oceniane etykiety** i **wynik prawdopodobieństwa** w danych wyjściowych za pomocą hello hello [Select Columns in Dataset ] [ select-columns] modułu.

Przykładowe oceniania eksperymentu znajduje się w hello na poniższej ilustracji. Toodeploy, gdy będzie gotowe kliknij hello **OPUBLIKOWAĆ usługi sieci WEB** przycisk hello dolnym pasku akcji.

![Publikowanie Azure ML][11]

## <a name="summary"></a>Podsumowanie
toorecap co możemy to zostało zrobione w tym samouczku wskazówki, zostały utworzone środowisku nauki danych Azure doświadczenie z dużego zestawu danych publiczne, biorąc go za pośrednictwem hello proces nauki danych zespołu, wszystkie sposób hello szkolenia toomodel pozyskiwania danych, a następnie Wdrażanie toohello usługi sieci web uczenie maszynowe Azure.

### <a name="license-information"></a>Informacje o licencji
Ten przewodnik próbki i jego towarzyszące IPython notebook(s) i skrypty są udostępniane przez firmę Microsoft hello MIT licencji. Sprawdź plik LICENSE.txt hello w katalogu hello hello przykładowy kod w serwisie GitHub więcej szczegółów.

## <a name="references"></a>Dokumentacja
• [Andrés Monroy taksówki NYC rund stronę pobierania](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC taksówki podróży danych przez Krzysztof Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [Taksówki NYC i Limousine Komisji badań i statystyki](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

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
