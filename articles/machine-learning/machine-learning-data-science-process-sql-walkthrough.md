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
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a>Hello proces nauki danych zespołu w działaniu: przy użyciu programu SQL Server
W tym samouczku opisano proces hello tworzenie i wdrażanie modelu uczenia maszynowego przy użyciu programu SQL Server i zestawu danych publicznie dostępnych — Witaj [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych. procedury Hello następuje nauki standardowych danych przepływu pracy: pozyskiwania i eksplorować dane hello, opracowywać learning toofacilitate funkcje, a następnie tworzenia i wdrażania modelu.

## <a name="dataset"></a>Taksówki NYC podróży opis zestawu danych
Hello danych podróży taksówki NYC około 20GB skompresowanego plików CSV (~ 48GB nieskompresowane), składającej się z więcej niż 173 milionów poszczególnych podróży i hello cen w klasie ekonomicznej płatnej w odniesieniu do każdej podróży. Każdy rekord podróży obejmuje hello odbiór i przyjmowania lokalizacji i czasu, numer licencji hack anonimowe (sterownik) i numer Medalionu (taksówki jego unikatowy identyfikator). Hello danych obejmuje wszystkie rund w roku hello 2013 i jest dostępne w powitania po dwóch zestawów danych dla każdego miesiąca:

1. Witaj "trip_data" CSV zawiera szczegóły podróży, takie jak liczba pasażerów, pobranie i punkty dropoff czas trwania podróży i długość podróży. Poniżej przedstawiono kilka przykładowych rekordów:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. Witaj "trip_fare" CSV zawiera szczegółowe informacje o klasie hello za każdym razem, takie jak typ płatności, kwota taryfy przeciążenia i podatków, porady i przejazd i Suma hello płatnej. Poniżej przedstawiono kilka przykładowych rekordów:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Hello unikatowy kluczy toojoin podróży\_danych i podróży\_taryfy składa się z pola hello: Medalionu, hack\_licencji i pobrania\_daty/godziny.

## <a name="mltasks"></a>Przykłady prognozowania zadań
Firma Microsoft będzie sformułować trzy problemów prognozowania oparte na powitania *Porada\_kwota*, to znaczy:

1. Klasyfikacji binarnej: prognozowania, czy etykietki został płatnej podróży, tj. *Porada\_kwota* większą niż $0 jest przykład dodatnią, podczas gdy *Porada\_kwota* $ 0 jest ujemny przykład.
2. Wieloklasowej klasyfikacji: zakres hello toopredict porady uregulowaniu płatności hello podróży. Możemy podzielić hello *Porada\_kwota* do pięciu bins lub klasy:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. Zadanie regresji: toopredict hello ilość Porada płatnej w podróży.  

## <a name="setup"></a>Definiowanie środowiska nauki danych Azure hello zaawansowana analityka
Jak widać w hello [Planowanie środowiska Your](machine-learning-data-science-plan-your-environment.md) przewodnik, istnieje kilka opcji toowork z zestawem danych rund taksówki NYC hello na platformie Azure:

* Praca z hello danych w obiektach blob Azure, a następnie modelu w usłudze Azure Machine Learning
* Ładowanie danych hello do bazy danych programu SQL Server, a następnie modelu w usłudze Azure Machine Learning

W tym samouczku przedstawiono importowania zbiorczego równoległych hello tooa danych programu SQL Server, Eksploracja danych, funkcja inżynierii i w dół próbkowania przy użyciu programu SQL Server Management Studio, a także za pomocą notesu IPython. [Przykładowe skrypty](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) i [notesów IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) są udostępniane w witrynie GitHub. Przykładowe IPython notesu toowork hello danymi w obiektach blob Azure jest również dostępna w hello tej samej lokalizacji.

tooset Twojego środowiska nauki danych Azure:

1. [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md)
2. [Utwórz obszar roboczy usługi Azure Machine Learning](machine-learning-create-workspace.md)
3. [Udostępnianie danych maszyny wirtualnej nauki](machine-learning-data-science-setup-sql-server-virtual-machine.md), zapewniające programu SQL Server i serwer IPython notesu.
   
   > [!NOTE]
   > Hello przykładowe skrypty i notebooki IPython będzie maszyny wirtualnej nauki danych tooyour pobrane podczas procesu konfiguracji hello. Po zakończeniu hello skryptu poinstalacyjnego maszyny Wirtualnej, przykłady hello będą biblioteki dokumentów maszyny Wirtualnej:  
   > 
   > * Przykładowe skrypty:`C:\Users\<user_name>\Documents\Data Science Scripts`  
   > * Przykładowe IPython notesów:`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`  
   >   gdzie `<user_name>` jest nazwą logowania systemu Windows maszyny Wirtualnej. Odnoszą się foldery próbki toohello jako **przykładowe skrypty** i **notesów IPython próbki**.
   > 
   > 

Na podstawie hello rozmiaru zestawu danych, lokalizacja źródła danych i hello wybranego celu Azure środowisko, w tym scenariuszu jest podobne zbyt[scenariusza \#5: dużego zestawu danych w lokalnych plikach, docelowa programu SQL Server w maszynie Wirtualnej platformy Azure](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).

## <a name="getdata"></a>Pobierz hello danych ze źródła publiczny
tooget hello [rund taksówki NYC](http://www.andresmh.com/nyctaxitrips/) zestawu danych z lokalizacji publicznej, możesz użyć dowolnej z metod hello opisanego w [tooand przenoszenia danych z magazynu obiektów Blob Azure](machine-learning-data-science-move-azure-blob.md) toocopy hello tooyour danych nowej maszyny wirtualnej.

dane hello toocopy przy użyciu narzędzia AzCopy:

1. Zaloguj się za tooyour maszyny wirtualnej (VM)
2. Utwórz nowy katalog dysku danych hello maszyny Wirtualnej (Uwaga: nie używaj hello tymczasowego dysk, który jest dostarczany z hello maszyny Wirtualnej jako dysk danych).
3. W oknie wiersza polecenia Uruchom hello następującego wiersza polecenia Azcopy, zastępując < path_to_data_folder > folderu danych utworzone w (2):
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    Po ukończeniu hello AzCopy łącznie 24 zip plików CSV (12 podczas podróży\_danych i 12 podczas podróży\_taryfy) powinny się znajdować w folderze danych hello.
4. Rozpakowywanie plików hello pobrane. Uwaga hello folder, w którym są przechowywane jako nieskompresowane hello pliki. Ten folder będzie hello tooas określonego < ścieżka\_do\_danych\_pliki\>.

## <a name="dbload"></a>Zbiorcze importowanie danych do bazy danych serwera SQL
Witaj ładowania/transfer dużych ilości danych tooan SQL database i kolejne zapytania można poprawić wydajność przy użyciu *partycjonowane tabele i widoki*. W tej sekcji możemy wykonaj instrukcje hello opisanego w [równoległych zbiorczego danych importu za pomocą SQL tabel partycji](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate nowe dane hello bazy danych i obciążenia do partycjonowane tabele równolegle.

1. Po zalogowaniu tooyour maszyny Wirtualnej, należy uruchomić **programu SQL Server Management Studio**.
2. Połącz przy użyciu uwierzytelniania systemu Windows.
   
    ![Połącz SSMS][12]
3. Jeśli jeszcze nie masz zmienić tryb uwierzytelniania programu SQL Server hello i utworzyć nowego użytkownika logowania SQL, otwórz plik skryptu hello o nazwie **zmienić\_auth.sql** w hello **przykładowe skrypty** folderu. Zmień hello domyślna nazwa użytkownika i hasło. Kliknij przycisk **! Wykonanie** hello narzędzi toorun hello skryptu.
   
    ![Uruchom skrypt][13]
4. Sprawdź i/lub zmienić hello domyślnej bazy danych i dziennika folderów tooensure nowo utworzony baz danych będą przechowywane na dysku danych programu SQL Server. Hello obraz maszyny Wirtualnej programu SQL Server, który jest zoptymalizowany pod kątem obciążeń strumienia jest wstępnie skonfigurowana z dyskami danych i dziennika. Jeśli maszyna wirtualna nie zawiera dysk z danymi i dodać nowe wirtualnych dysków twardych podczas hello procesu konfiguracji maszyny Wirtualnej, zmień hello domyślnych folderów w następujący sposób:
   
   * Kliknij prawym przyciskiem myszy nazwę serwera SQL hello hello lewego panelu i kliknij przycisk **właściwości**.
     
       ![Właściwości serwera SQL][14]
   * Wybierz **ustawienia bazy danych** z hello **wybierz stronę** listy toohello lewej.
   * Sprawdź i/lub zmienić hello **bazy danych domyślne lokalizacje** toohello **dysku danych** lokalizacje wybranych przez użytkownika. Jest to, gdzie nowe bazy danych znajdują się Jeśli utworzone za pomocą hello domyślne ustawienia lokalizacji.
     
       ![Domyślne ustawienia bazy danych SQL][15]  
5. toocreate nową bazę danych i zestaw grup plików toohold hello partycjonowane tabele, otwórz hello przykładowy skrypt **utworzyć\_db\_default.sql**. skrypt Hello spowoduje utworzenie nowej bazy danych o nazwie **TaxiNYC** i 12 grup plików w hello domyślnej lokalizacji danych. Każda grupa plików będą przechowywane miesiąc podróży\_danych i podróży\_taryfy danych. W razie potrzeby zmodyfikuj hello Nazwa bazy danych. Kliknij przycisk **! Wykonanie** toorun hello skryptu.
6. Następnie należy utworzyć dwie tabele partycji, jeden dla podróży hello\_danych i drugi dla podróży hello\_klasie. Otwórz hello przykładowy skrypt **utworzyć\_partycjonowanej\_table.sql**, który będzie:
   
   * Tworzenie partycji funkcji toosplit hello danych według miesięcy.
   * Utwórz toomap schematu partycji co miesiąc danych tooa innej grupy plików.
   * Utwórz dwa schemat partycji zamapowanych toohello partycjonowane tabele: **nyctaxi\_podróży** będą przechowywane podróży hello\_danych i **nyctaxi\_taryfy** będą przechowywane hello podróży \_taryfy danych.
     
     Kliknij przycisk **! Wykonanie** toorun hello skryptu i tworzenie tabel hello podzielona na partycje.
7. W hello **przykładowe skrypty** folderu, istnieją dwie przykładowe skrypty programu PowerShell dostarczane toodemonstrate Importy zbiorcze równoległych tabel serwera tooSQL danych.
   
   * **Narzędzie BCP\_równoległych\_generic.ps1** jest skrypt rodzajowy tooparallel zbiorczego importowania danych do tabeli. Modyfikuj tego skryptu tooset hello dane wejściowe i obiekt docelowy zmienne wskazane hello wiersze komentarzy w skrypcie hello.
   * **Narzędzie BCP\_równoległych\_nyctaxi.ps1** jest wstępnie skonfigurowana wersja skrypt rodzajowy hello i mogą być używane tootooload obu tabel danych rund taksówki NYC hello.  
8. Powitania kliknij prawym przyciskiem myszy **bcp\_równoległych\_nyctaxi.ps1** kliknij nazwę skryptu wraz z **Edytuj** tooopen go w programie PowerShell. Hello Przejrzyj ustawienia zmiennych i modyfikować zgodnie z tooyour wybranej nazwie bazy danych, folderu danych wejściowych, folder docelowy dziennika i ścieżki toohello Przykładowy format plików **nyctaxi_trip.xml** i **nyctaxi\_ fare.XML** (w hello **przykładowe skrypty** folderu).
   
    ![Zbiorczego importowania danych][16]
   
    Można również wybrać tryb uwierzytelniania hello, domyślnym jest uwierzytelnianie systemu Windows. Kliknij strzałkę hello zielony w hello toorun paska narzędzi. skrypt Hello uruchomi 24 operacji importowania zbiorczego w 12 równoległe, dla każdej tabeli partycjonowanej. Może monitorować postęp importowania danych hello, otwierając folder dane domyślnego programu SQL Server hello zgodnie z ustaleniami powyżej.
9. Raporty skrypt programu PowerShell Hello hello godziny rozpoczęcia i zakończenia. Jeśli wszystkie masowe Importy ukończone, zgłaszane hello godzina zakończenia. Sprawdź hello docelowego dziennika folderu tooverify, który importuje zbiorczego hello zostały pomyślnie, tj. żadne błędy nie zgłoszone w folderze dziennika docelowym hello.
10. Baza danych jest teraz gotowe do eksploracji, funkcja inżynieryjne i innych czynności. Ponieważ tabele hello są podzielone na partycje według toohello **podnoszenia\_datetime** pola zapytania, które obejmują **podnoszenia\_daty/godziny** warunków w hello  **GDZIE** klauzuli będą korzystać z hello schemat partycji.
11. W **programu SQL Server Management Studio**, Eksploruj hello podano przykładowy skrypt **próbki\_queries.sql**. toorun żadnego hello przykładowe zapytania, hello wyróżnienie zapytania wierszy a następnie kliknij przycisk **! Wykonanie** hello w pasku narzędzi.
12. Hello rund taksówki NYC danych została załadowana w dwóch oddzielnych tabelach. operacji łączenia tooimprove, zdecydowanie zaleca tooindex hello tabel. Witaj przykładowy skrypt **utworzyć\_podzielonym na partycje\_index.sql** tworzy indeksy podzielone na partycje klucza złożonego sprzężenia hello **Medalionu, hack\_licencji i pobrania\_datetime**.

## <a name="dbexplore"></a>Eksploracja danych i inżynieria funkcji w programie SQL Server
Generowanie funkcji i eksploracja danych w tej sekcji zostaną wykonane przez uruchomienie zapytania SQL bezpośrednio w hello **programu SQL Server Management Studio** przy użyciu bazy danych programu SQL Server hello utworzony wcześniej. Przykładowy skrypt o nazwie **próbki\_queries.sql** znajduje się w hello **przykładowe skrypty** folderu. Zmodyfikować hello toochange hello bazy danych nazwa skryptu, jeśli jest inny niż domyślny hello: **TaxiNYC**.

W tym ćwiczeniu zostaną wykonane następujące czynności:

* Połącz za**programu SQL Server Management Studio** przy użyciu uwierzytelnianiu systemu Windows lub uwierzytelniania SQL i hello nazwa logowania SQL i hasło.
* Eksplorowanie danych dystrybucji kilka pól w różnym czasie systemu windows.
* Zbadaj jakości danych hello pól długości i szerokości geograficznej.
* Generowanie etykiet klasyfikacji binarnej i wieloklasowej oparte na powitania **Porada\_kwota**.
* Generowanie funkcji i obliczeń lub porównania odległości podróży.
* Dołącz Witaj dwie tabele i Wyodrębnij losowej próbki, które będzie używane toobuild modeli.

Gdy są gotowe tooproceed tooAzure uczenia maszynowego, użytkownik może:  

1. Zapisz hello końcowego SQL kwerendy tooextract i przykładowa hello danych i kopiowania i wklejania hello zapytanie bezpośrednio do [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning, lub
2. Utrwalić hello próbkowany i odtworzone danych planujesz toouse modelu Tworzenie nowej bazy danych tabeli i korzystanie z nowej tabeli hello w hello [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning.

W tej sekcji zapisze firma Microsoft hello końcowego tooextract i przykładowa hello dane zapytania. Druga metoda Hello jest przedstawiona w hello [Eksploracja danych i funkcji inżynieryjnego w notesie IPython](#ipnb) sekcji.

Szybkie weryfikacji hello liczby wierszy i kolumn w hello tabel wypełnione wcześniej za pomocą importowania zbiorczego równoległych

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a>Eksploracja: Podróży dystrybucji przez Medalionu
W tym przykładzie identyfikuje hello Medalionu (taksówki numery) z więcej niż 100 rund w danym okresie. Zapytanie Hello korzystałby z hello na partycje tabeli dostępu, ponieważ należy przygotować przez schemat partycji hello **podnoszenia\_datetime**. Badania hello pełnego zestawu danych będzie również używać tabeli partycjonowanej hello i/lub indeksu skanowania.

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Eksploracja: Podróży dystrybucji Medalionu i hack_license
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a>Oceny jakości danych: Rekordy z geograficzne niepoprawne i/lub szerokość geograficzną Sprawdź
W tym przykładzie sprawdza, czy hello geograficzne i/lub szerokość geograficzną polach albo zawiera nieprawidłową wartość (stopni w radianach powinna należeć do zakresu od-90 do 90,) lub (0, 0) współrzędnych.

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a>Eksploracja: Przechylony vs. Nie Przechylony rund dystrybucji
W tym przykładzie znajduje hello Liczba podróży, które zostały Przechylony a nie Przechylony w danym momencie okres (lub w hello pełnego zestawu danych jeśli obejmujące cały rok hello). Tej dystrybucji odzwierciedla toobe dystrybucji binarne etykiety hello później użyć do modelowania klasyfikacji binarnej.

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a>Eksploracja: Porada dystrybucji klasy/zakresu
W tym przykładzie oblicza dystrybucji hello Porada zakresów w danym momencie okres (lub w hello pełnego zestawu danych jeśli obejmujące cały rok hello). Jest to dystrybucji hello hello etykiety klas, które będą później używane do modelowania wieloklasowej klasyfikacji.

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

#### <a name="exploration-compute-and-compare-trip-distance"></a>Eksploracja: Obliczania i porównać odległość podróży
W tym przykładzie konwertuje hello odbiór i przyjmowania geograficzne i współrzędne geograficzne tooSQL punktów, oblicza odległość podróży hello przy użyciu różnicę punktów geograficzne SQL i zwraca losowej próbki hello wyniki do porównania. przykład Witaj ogranicza wyniki hello toovalid koordynuje tylko przy użyciu objętych wcześniej hello danych jakości oceny zapytania.

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

#### <a name="feature-engineering-in-sql-queries"></a>Funkcja Engineering w zapytania SQL
Hello etykiety generowania geograficzne konwersji eksploracji zapytań i może być również używane toogenerate etykiety/funkcje przez usunięcie hello zliczania części. Dodatkową cechą engineering SQL przykłady znajdują się w hello [Eksploracja danych i funkcji inżynieryjnego w notesie IPython](#ipnb) sekcji. Jest bardziej wydajne toorun hello funkcji generowania zapytania na powitania pełnego zestawu danych lub za pomocą zapytania SQL, które uruchomione bezpośrednio w wystąpieniu bazy danych programu SQL Server hello duży podzbiór. Witaj zapytania mogą być wykonywane w **programu SQL Server Management Studio**, notesu IPython lub dowolnego narzędzia/Środowisko deweloperskie, które mogą uzyskiwać dostęp do hello bazy danych lokalnie lub zdalnie.

#### <a name="preparing-data-for-model-building"></a>Przygotowywanie danych do konstruowania modelu
Witaj następujące zapytanie sprzęga hello **nyctaxi\_podróży** i **nyctaxi\_taryfy** tabel, generuje etykiety klasyfikacji binarnej **Przechylony**, etykiety klasyfikacji wielu klasy **Porada\_klasy**i wyodrębnia 1% losowej próbki z hello pełnego dołączonego do zestawu danych. To zapytanie może skopiować następnie wkleić bezpośrednio w hello [Azure Machine Learning Studio](https://studio.azureml.net) [i zaimportuj dane] [ import-data] modułu dla wprowadzanie danych bezpośrednio z bazy danych programu SQL Server hello wystąpienie na platformie Azure. Zapytanie Hello wyklucza rekordy z niepoprawne (0, 0) współrzędnych.

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


## <a name="ipnb"></a>Eksploracja danych i funkcji inżynieryjne w notesie IPython
W tej sekcji zostaną wykonane Eksplorowanie danych oraz generowanie funkcji za pomocą zarówno Python, jak i SQL zapytań dotyczących bazy danych programu SQL Server hello utworzony wcześniej. Przykładowe IPython Notes o nazwie **machine-Learning-data-science-process-sql-story.ipynb** znajduje się w hello **notesów IPython próbki** folderu. Ten notes jest również dostępna w [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).

Hello zalecane sekwencji podczas pracy z danymi big data jest hello następujące czynności:

* Odczyt w małej przykładowej hello danych do ramki danych w pamięci.
* Wykonywanie niektórych wizualizacje i eksploracji przy użyciu danych hello próbkowane.
* Wypróbuj engineering funkcji przy użyciu danych hello próbkowane.
* Dla większych Eksploracja danych do manipulowania danymi i funkcji zespołu inżynieryjnego, użyj zapytania SQL tooissue Python bezpośrednio z bazy danych programu SQL Server hello w hello maszyny Wirtualnej platformy Azure.
* Zdecyduj, toouse rozmiar próbki hello do tworzenia modelu uczenia maszynowego Azure.

Gdy gotowe tooAzure tooproceed uczenia maszynowego, użytkownik może:  

1. Zapisz hello końcowego SQL kwerendy tooextract i przykładowa hello danych i kopiowania i wklejania hello zapytanie bezpośrednio do [i zaimportuj dane] [ import-data] modułu w usłudze Azure Machine Learning. Ta metoda jest przedstawiona w hello [tworzenia modeli w usłudze Azure Machine Learning](#mlmodel) sekcji.    
2. Zachować hello próbkowany i odtworzone dane planujesz toouse tworzenie w nowej tabeli bazy danych modelu, a następnie użyj nowej tabeli hello w hello [i zaimportuj dane] [ import-data] modułu.

Witaj poniżej przedstawiono kilka Eksploracja danych, wizualizacji danych i funkcji inżynierii przykłady. Więcej przykładów można znaleźć hello przykładowy SQL IPython Notes w hello **notesów IPython próbki** folderu.

#### <a name="initialize-database-credentials"></a>Inicjowanie poświadczenia bazy danych
Inicjowanie ustawienia połączenia bazy danych w hello następujące zmienne:

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a>Utwórz połączenie z bazą danych
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a>Raport liczba wierszy i kolumn w tabeli nyctaxi_trip
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

* Całkowita liczba wierszy = 173179759  
* Łączna liczba kolumn = 14

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a>Odczyt w przykładowych danych małych z hello bazy danych serwera SQL
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

Czas tooread hello Przykładowa tabela jest 6.492000 sekund  
Liczba wierszy i kolumn pobrać = (84952, 21)

#### <a name="descriptive-statistics"></a>Statystyki opisowe
Są teraz gotowe tooexplore hello próbce danych. Możemy zaczynać się patrzeć Statystyki opisowe dla hello **podróży\_odległość** (lub innych) pola/pól:

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a>Wizualizacji: Przykład kreślenia pola
Następnie przyjrzymy się hello skrzynkowy dla hello podróży odległość toovisualize hello quantiles

    df1.boxplot(column='trip_distance',return_type='dict')

![Wykreślenia #1][1]

#### <a name="visualization-distribution-plot-example"></a>Wizualizacji: Przykład kreślenia dystrybucji
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Wykreślenia #2][2]

#### <a name="visualization-bar-and-line-plots"></a>Wizualizacji: Pasek i powierzchni wiersza
W tym przykładzie firma Microsoft hello odległość podróży do pięciu bins bin i wizualizację hello binning wyników.

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

Firma Microsoft może wykreślenia hello powyżej dystrybucji bin na pasku lub wiersz kreślenia zgodnie z poniższymi instrukcjami

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Wykreślenia #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Wykreślenia #4][4]

#### <a name="visualization-scatterplot-example"></a>Wizualizacji: Przykład Scatterplot
Zostanie przedstawiony jest wykres punktowy między **podróży\_czasu\_w\_s** i **podróży\_odległość** toosee w przypadku dowolnego korelacji

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Wykreślenia #6][6]

Podobnie można sprawdzić hello relacji między **szybkość\_kod** i **podróży\_odległość**.

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Wykreślenia #8][8]

### <a name="sub-sampling-hello-data-in-sql"></a>Hello podrzędne próbkowania danych SQL
Podczas przygotowywania danych dla modelu kompilacji w [Azure Machine Learning Studio](https://studio.azureml.net), albo można wyłączyć na powitania **toouse zapytania SQL bezpośrednio w module importu danych hello** lub utrwalić hello odtwarzane i próbkowany danych w nowej tabeli, którego można użyć w hello [i zaimportuj dane] [ import-data] modułu przy użyciu prostego **wybierz * FROM < Twojej\_nowe\_tabeli\_name >**.

W tej sekcji, który zostanie utworzony nowy hello toohold tabeli próbkowany i odtwarzane danych. Przykład bezpośrednie kwerendy SQL dla tworzenia modelu znajduje się w hello [Eksploracja danych i funkcji inżynieryjnego w programie SQL Server](#dbexplore) sekcji.

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a>Utwórz przykładową tabelę i Wypełnij tabele sprzężone hello: % 1. Jeśli istnieje porzucić pierwszej tabeli.
W tej sekcji możemy sprzężone tabele hello **nyctaxi\_podróży** i **nyctaxi\_taryfy**, Wyodrębnij losowej próbki 1%, a utrwalenia hello próbkowany danych w nowej nazwy tabeli  **nyctaxi\_jeden\_procent**:

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

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a>Eksploracja danych za pomocą zapytań SQL w notesie IPython
W tej sekcji możemy Eksplorowanie danych dystrybucji przy użyciu hello danych próbkowany % 1, który jest utrwalona w nowej tabeli hello, utworzone powyżej. Należy pamiętać, że podobne eksploracji może zostać wykonane przy użyciu oryginalnego tabel hello, opcjonalnie używając **TABLESAMPLE** toolimit hello eksploracji przykładowa lub ograniczając hello powoduje tooa danego okresu czasu przy użyciu hello **pobrania \_datetime** partycji, jak pokazano na powitania [Eksploracja danych i funkcji inżynieryjnego w programie SQL Server](#dbexplore) sekcji.

#### <a name="exploration-daily-distribution-of-trips"></a>Eksploracji: Codzienne dystrybucji rund
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a>Eksploracja: Podróży dystrybucji na Medalionu
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a>Generowanie funkcji za pomocą zapytań SQL w notesie IPython
W tej sekcji wygenerujemy nowe etykiety i funkcji bezpośrednio za pomocą zapytania SQL, na tabeli 1% hello utworzyliśmy hello w poprzedniej sekcji.

#### <a name="label-generation-generate-class-labels"></a>Generowanie etykiety: Generowanie etykiet — klasa
W hello poniższy przykład firma Microsoft generuje dwa zestawy toouse etykiety dla modelowania:

1. Binarny etykiety klasy **Przechylony** (przewidywania, jeśli będzie miał poradę)
2. Etykiety wieloklasowej **Porada\_klasy** (przewidywania bin Porada hello lub zakres)
   
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

#### <a name="feature-engineering-count-features-for-categorical-columns"></a>Inżynieria funkcji: Liczba funkcje dla kolumny podzielone na kategorie
W tym przykładzie przekształca pole kategorii do pola liczbowego przez zamianę każdej kategorii hello liczba ich wystąpień hello danych.

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

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a>Funkcja Engineering: Bin funkcje dla kolumny liczbowe
W tym przykładzie przekształca pola numerycznego ciągłe na zakresy istniejących kategorii, tj., Przekształcanie pola numerycznego w pole kategorii.

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

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a>Inżynieria funkcji: Wyodrębniania dziesiętną szerokości geograficznej/długości geograficznej lokalizacji funkcji
W tym przykładzie dzieli hello dziesiętną reprezentację szerokości geograficznej i/lub długość pola na wielu pól region z różnych szczegółowości takich, jak kraj, Miasto, miejscowość, blok itp. Należy pamiętać, że nowe pola geograficznie hello nie są mapowane tooactual lokalizacji. Informacje dotyczące mapowania lokalizacji geocode znajdują się w temacie [usług REST mapy usługi Bing](https://msdn.microsoft.com/library/ff701710.aspx).

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

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a>Sprawdź hello końcowego formę hello featurized tabeli
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

Firma Microsoft są teraz gotowe tooproceed toomodel tworzenia i wdrażania modelu w [usługi Azure Machine Learning](https://studio.azureml.net). dane Hello jest gotowy do żadnego z wymienionych wcześniej, to znaczy problemów prognozowania hello:

1. Klasyfikacji binarnej: toopredict czy poradę został płatnej w podróży.
2. Wieloklasowej klasyfikacji: zakres hello toopredict porady płatnej, zgodnie z uprzednio zdefiniowanej klasy toohello.
3. Zadanie regresji: toopredict hello ilość Porada płatnej w podróży.  

## <a name="mlmodel"></a>Tworzenie modeli w uczenie maszynowe Azure
toobegin hello modelowania ćwiczeniu logowania obszaru roboczego uczenia maszynowego Azure tooyour. Jeśli jeszcze nie utworzono obszaru roboczego uczenia maszynowego, zobacz [Utwórz obszar roboczy usługi Azure Machine Learning](machine-learning-create-workspace.md).

1. wprowadzenie do usługi Azure Machine Learning tooget zobacz [co to jest Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)
2. Zaloguj się za[Azure Machine Learning Studio](https://studio.azureml.net).
3. Strona główna Studio Hello zawiera wiele informacji, wideo, samouczki, toohello łącza odwołania moduły i innych zasobów. Aby uzyskać więcej informacji na temat usługi Azure Machine Learning, zapoznaj się hello [Centrum dokumentacji uczenia maszynowego Azure](https://azure.microsoft.com/documentation/services/machine-learning/).

Eksperyment typowe szkolenia składa się z następujących hello:

1. Utwórz **+ nowy** eksperymentu.
2. Pobierz tooAzure danych hello uczenia maszynowego.
3. Wstępnie przetworzyć, transformacji i manipulować danymi hello, zgodnie z potrzebami.
4. Generowanie funkcji zgodnie z potrzebami.
5. Podział danych hello na zestawy szkoleniowe / / sprawdzanie poprawności danych (lub mieć osobne zestawy danych dla każdego).
6. Wybierz co najmniej jeden z algorytmów w zależności od hello learning problem toosolve uczenia maszynowego. Przykład klasyfikacji binarnej, wieloklasowej klasyfikacji, regresji.
7. Szkolenie co najmniej jednego modelu przy użyciu zestawu danych szkoleniowych hello.
8. Wynik przy użyciu modeli przeszkolone hello weryfikacji hello w zestawie danych.
9. Należy ocenić hello modele toocompute hello odpowiednich metryki dla hello uczenia problem.
10. Dopasuj hello modele i wybierz hello najlepsze toodeploy modelu.

W tym ćwiczeniu mamy już przedstawione i odtwarzane hello danych w programie SQL Server i na tooingest rozmiar próbki hello w usłudze Azure Machine Learning. toobuild co najmniej jeden modeli prognozowania hello zdecydowaliśmy:

1. Pobierz tooAzure danych hello uczenia maszynowego przy użyciu hello [i zaimportuj dane] [ import-data] modułu dostępne w hello **danych wejściowych i wyjściowych** sekcji. Aby uzyskać więcej informacji, zobacz hello [i zaimportuj dane] [ import-data] strony odwołanie do modułu.
   
    ![Uczenie maszynowe Azure i zaimportuj dane][17]
2. Wybierz **bazy danych SQL Azure** jako hello **źródła danych** w hello **właściwości** panelu.
3. Wprowadź nazwę DNS bazy danych hello w hello **nazwę serwera bazy danych** pola. Format:`tcp:<your_virtual_machine_DNS_name>,1433`
4. Wprowadź hello **Nazwa bazy danych** w hello odpowiednie pole.
5. Wprowadź hello **nazwa użytkownika SQL** w hello ** nazwa_serwera aqccount użytkownika i hasło hello w hello **hasło konta użytkownika serwera**.
6. Sprawdź **dowolny certyfikat serwera Zaakceptuj** opcji.
7. W hello **zapytanie bazy danych** edytować obszaru tekstu, Wklej zapytanie hello wyciąg konieczne hello pola (w tym wszystkie pola obliczane takich jak etykiety hello) bazy danych i w dół przykłady hello danych toohello potrzeby próbkowania.

Przykład eksperyment klasyfikacji binarnej odczytywanie danych bezpośrednio z bazy danych programu SQL Server hello jest hello na poniższej ilustracji. Podobne eksperymenty można utworzyć dla wieloklasowej klasyfikacji i regresji problemów.

![Azure Machine Learning pociągu][10]

> [!IMPORTANT]
> W hello modelowania wyodrębniania danych i pobierania próbek zapytania przykłady podane w poprzednich sekcjach **wszystkich etykiet ćwiczeń modelowania hello trzech znajdują się w zapytaniu hello**. Ważnym krokiem (wymagane) w każdym hello modelowania ćwiczenia jest zbyt**wykluczyć** hello niepotrzebnych etykiety hello innych dwa problemy oraz wszelkie inne **target przecieki**. Dla przykład korzystając z klasyfikacji binarnej, za pomocą etykiety hello **Przechylony** i wykluczyć pola hello **Porada\_klasy**, **Porada\_kwota**, i **całkowita\_kwota**. Hello te ostatnie są kupowane przecieki docelowy one zakłada Porada hello.
> 
> tooexclude zbędne kolumny i/lub przecieki docelowych, można użyć hello [Select Columns in Dataset] [ select-columns] modułu lub hello [edytowanie metadanych] [ edit-metadata]. Aby uzyskać więcej informacji, zobacz [Select Columns in Dataset] [ select-columns] i [edytowanie metadanych] [ edit-metadata] odwołania stron.
> 
> 

## <a name="mldeploy"></a>Wdrażanie modeli w uczenie maszynowe Azure
Gdy model jest gotowy, łatwo można go wdrożyć jako usługę sieci web bezpośrednio z hello eksperymentu. Aby uzyskać więcej informacji na temat wdrażania usług sieci web uczenie maszynowe Azure, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

toodeploy nową usługę sieci web, musisz:

1. Tworzenie eksperymentu oceniania.
2. Wdrażanie usługi sieci web hello.

toocreate oceniania Poeksperymentuj z **Zakończono** szkolenia eksperyment, kliknij przycisk **utworzyć OCENIANIA EKSPERYMENTU** hello dolnym pasku akcji.

![Ocenianie przez usługę Azure][18]

Usługa Azure Machine Learning podejmie toocreate eksperyment oceniania na podstawie składników hello eksperyment uczenia hello. W szczególności będzie:

1. Zapisz hello uczonego modelu i usuwanie modułów uczenia modelu hello.
2. Zidentyfikuj logicznych **port wejściowy** toorepresent hello oczekiwano schemat danych wejściowych.
3. Zidentyfikuj logicznych **output portu** schematem wyjściowym toorepresent hello oczekiwanego sieci web usługi.

Po utworzeniu hello oceniania eksperymentu, przejrzyj go i dostosować zgodnie z potrzebami. Typowy korekty jest wejściowy zestaw danych tooreplace hello i/lub zapytanie z taki, który wyklucza pola etykiety, jak te nie będą dostępne, gdy jest wywoływana hello usługi. Istnieje również wprowadzenia hello o rozmiarze hello tooreduce dobrym rozwiązaniem tooa zestawu danych i/lub zapytania kilka rekordów, schemat danych wejściowych hello wystarczającego tooindicate. Port wyjściowy hello, jest typowe tooexclude wszystkie pola i zawierać wyłącznie hello **oceniane etykiety** i **wynik prawdopodobieństwa** w danych wyjściowych za pomocą hello hello [Select Columns in Dataset ] [ select-columns] modułu.

Przykładowe oceniania eksperymentu jest hello na poniższej ilustracji. Toodeploy, gdy będzie gotowe kliknij hello **OPUBLIKOWAĆ usługi sieci WEB** przycisk hello dolnym pasku akcji.

![Publikowanie uczenie maszynowe Azure][11]

toorecap, w tym samouczku wskazówki utworzono środowiska nauki danych Azure, pracy z zestawem danych publicznych dużych końca hello z toomodel pozyskiwania danych, uczenie i wdrażanie usługi sieci web uczenie maszynowe Azure.

### <a name="license-information"></a>Informacje o licencji
Ten przewodnik próbki i jego towarzyszące IPython notebook(s) i skrypty są udostępniane przez firmę Microsoft hello MIT licencji. Sprawdź plik LICENSE.txt hello w katalogu hello hello przykładowy kod w serwisie GitHub więcej szczegółów.

### <a name="references"></a>Dokumentacja
• [Andrés Monroy taksówki NYC rund stronę pobierania](http://www.andresmh.com/nyctaxitrips/)  
• [FOILing NYC taksówki podróży danych przez Krzysztof Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
• [Taksówki NYC i Limousine Komisji badań i statystyki](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

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
