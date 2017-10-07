---
title: "aaaLoad terabajtów danych do usługi SQL Data Warehouse | Dokumentacja firmy Microsoft"
description: "Pokazuje, jak 1 TB danych mogą być ładowane do usługi Azure SQL Data Warehouse z fabryką danych Azure w obszarze 15 minut"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a>Ładowanie 1 TB do usługi Azure SQL Data Warehouse w obszarze 15 minut przy użyciu fabryki danych
[Usługa Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) oparte na chmurze, skalowalnych w poziomie bazy danych jest w stanie przetwarzanie bardzo dużych woluminów danych relacyjnych i nierelacyjnych.  Zbudowany w oparciu o architekturę masowego przetwarzania równoległego (MPP), usługa SQL Data Warehouse jest zoptymalizowana pod kątem obciążeń magazynu danych przedsiębiorstwa.  Zapewnia elastyczność hello elastyczność tooscale magazynu w chmurze i zasobów obliczeniowych niezależnie.

Wprowadzenie do korzystania z usługi Azure SQL Data Warehouse jest teraz łatwiejsze niż kiedykolwiek przy użyciu **fabryki danych Azure**.  Fabryka danych Azure to usługa integracji pełni zarządzanych danych oparte na chmurze, które mogą być używane toopopulate SQL Data Warehouse hello danych z istniejącego systemu i zapisywanie cenny czas podczas oceny usługi SQL Data Warehouse i budowania sieci analityka rozwiązania. Poniżej przedstawiono główne zalety hello ładowania danych do usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure:

* **Łatwe tooset się**: Kreator intuicyjne krok 5 z bez skryptu wymagane.
* **Obsługa magazynu danych sformatowanego**: wbudowaną obsługę bogaty zestaw lokalnymi i magazyny danych oparte na chmurze.
* **Bezpieczne i zgodne**: dane są przesyłane za pośrednictwem protokołu HTTPS lub ExpressRoute i zapewnia obecności usługi globalne dane nigdy nie przekracza granic geograficznych hello
* **Bezkonkurencyjne wydajności przy użyciu programu PolyBase** — przy użyciu programu Polybase jest hello najbardziej efektywny sposób toomove danych do usługi Azure SQL Data Warehouse. Hello przemieszczania funkcji obiektów blob można osiągnąć szybkości wysokie obciążenie ze wszystkich typów magazynów danych oprócz magazynu obiektów Blob platformy Azure, które hello aparat Polybase obsługuje domyślnie.

W tym artykule opisano sposób toouse kreatora kopiowania fabryki danych tooload 1 TB danych z magazynu obiektów Blob Azure do usługi Azure SQL Data Warehouse w obszarze 15 minut, w ponad 1,2 GB/s przepustowości.

Ten artykuł zawiera instrukcje krok po kroku przenoszenie danych do usługi Azure SQL Data Warehouse przy użyciu Kreatora kopiowania hello.

> [!NOTE]
>  Aby uzyskać ogólne informacje o możliwościach fabryki danych podczas przenoszenia danych do/z usługi Azure SQL Data Warehouse, zobacz [przenieść tooand danych z usługi Azure SQL Data Warehouse przy użyciu fabryki danych Azure](data-factory-azure-sql-data-warehouse-connector.md) artykułu.
>
> Można również tworzyć przy użyciu portalu Azure, programu Visual Studio, programu PowerShell, potoki itp. Zobacz [samouczek: kopiowanie danych z tooAzure obiektów Blob platformy Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Przewodnik Szybki z instrukcje krok po kroku dotyczące korzystania z hello działanie kopiowania w fabryce danych Azure.  
>
>

## <a name="prerequisites"></a>Wymagania wstępne
* Azure Blob Storage: tego eksperymentu używa magazynu obiektów Blob Azure (GRS) do przechowywania TPC-H testowych w zestawie danych.  Dowiedz się, jeśli nie masz konta magazynu platformy Azure, [jak toocreate konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* [TPC-H](http://www.tpc.org/tpch/) danych: zamierzamy toouse TPC-H, jak hello zestawu danych testowych.  toodo, że należy toouse `dbgen` z zestawu narzędzi TPC-H, który pomaga Generowanie hello zestawu danych.  Albo można pobrać kodu źródłowego dla `dbgen` z [narzędzia TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) i skompiluj go samodzielnie lub danych binarnych skompilowanych hello pobierania z [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).  Uruchom dbgen.exe hello następujące polecenia toogenerate pliku prostego 1 TB dla `lineitem` tabeli rozpowszechniania przez 10 plików:

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * …
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    Teraz hello kopii wygenerowanych plików tooAzure obiektów Blob.  Odwołuje się zbyt[przenieść tooand danych z lokalnego systemu plików przy użyciu fabryki danych Azure](data-factory-onprem-file-system-connector.md) jak toodo który przy użyciu kopii ADF.    
* Usługa Azure SQL Data Warehouse: tego eksperymentu ładuje dane do magazynu danych SQL Azure utworzonych za pomocą dwu 6000

    Odwołuje się zbyt[Utwórz magazyn danych SQL Azure](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) szczegółowe informacje dotyczące sposobu toocreate SQL Data Warehouse bazy danych.  tooget hello najlepsze możliwe obciążenie wydajności do usługi SQL Data Warehouse przy użyciu programu Polybase, możemy wybierz maksymalną liczbę jednostek magazynu danych (dwu) dozwolone w ustawieniu wydajności hello, czyli 6000 jednostek dwu.

  > [!NOTE]
  > Podczas ładowania z obiektów Blob platformy Azure, ładowanie wydajności danych hello jest wprost proporcjonalny toohello liczby jednostek dwu Skonfiguruj na powitania SQL Data Warehouse:
  >
  > Ładowanie 1 TB do 1000 DWU usługa SQL Data Warehouse uwzględnia 87 minut (przepływność ~ 200 MB/s) podczas ładowania 1 TB 2000 DWU usługa SQL Data Warehouse przyjmuje 46 minut (przepływność ~ 380 MB/s) podczas ładowania 1 TB w 6000 DWU usługa SQL Data Warehouse trwa 14 minut (przepływność ~1.2 GB/s)
  >
  >

    toocreate SQL Data Warehouse z dwu 6000, przesuń suwak wydajności hello wszystkich toohello sposób powitania po prawej:

    ![Suwak wydajności](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    Dla istniejącej bazy danych nie jest skonfigurowany z dwu 6000 można go skalować przy użyciu portalu Azure.  Przejdź toohello bazy danych, w portalu Azure, a nie **skali** przycisku na powitania **omówienie** panelu pokazano powitania po obrazu:

    ![Przycisk skali](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    Kliknij przycisk hello **skali** następujące hello tooopen przycisk panelu, przesuń suwak hello toohello maksymalną wartość i kliknij **Zapisz** przycisku.

    ![Okno dialogowe skalowania](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    Tego eksperymentu ładuje dane do usługi Azure SQL Data Warehouse przy użyciu `xlargerc` klasy zasobów.

    tooachieve najlepsze możliwe przepływności, kopii musi toobe wykonywane przy użyciu użytkownika usługi SQL Data Warehouse należącego zbyt`xlargerc` klasy zasobów.  Dowiedz się, jak toodo który wykonując [zmienić przykład klasy zasobów użytkownika](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).  
* Tworzenie schematu tabeli docelowej w bazie danych Azure SQL Data Warehouse, uruchamiając powitania po instrukcji DDL:

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
Dzięki wstępnie wymagane kroki hello ukończone mamy teraz działanie kopiowania hello tooconfigure gotowe za pomocą Kreatora kopiowania hello.

## <a name="launch-copy-wizard"></a>Uruchamianie Kreatora kopiowania
1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **+ nowy** hello lewym górnym rogu kliknij **analizy i analiza**i kliknij przycisk **fabryki danych**.
3. W hello **nowa fabryka danych** bloku:

   1. Wprowadź **LoadIntoSQLDWDataFactory** dla hello **nazwa**.
       Nazwa fabryki danych Azure hello Hello musi być globalnie unikatowe. Jeśli wystąpi błąd hello: **nazwa fabryki danych "LoadIntoSQLDWDataFactory" nie jest dostępna**, Zmień nazwę hello hello fabryki danych (na przykład yournameLoadIntoSQLDWDataFactory) i spróbuj ponownie utworzyć. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.  
   2. Wybierz swoją **subskrypcję** platformy Azure.
   3. Dla grupy zasobów wykonaj jedną z hello następujące kroki:
      1. Wybierz **Użyj istniejącego** tooselect istniejącą grupę zasobów.
      2. Wybierz **Utwórz nowy** tooenter nazwę grupy zasobów.
   4. Wybierz **lokalizacji** hello fabryki danych.
   5. Wybierz **toodashboard numeru Pin** pole wyboru u dołu hello hello bloku.  
   6. Kliknij przycisk **Utwórz**.
4. Po zakończeniu tworzenia hello Zobacz hello **fabryki danych** bloku, jak pokazano w powitania po obrazu:

   ![Strona główna fabryki danych](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. Na stronie głównej fabryki danych powitania kliknij hello **skopiować dane** Kafelek toolaunch **kreatora kopiowania**.

   > [!NOTE]
   > Jeśli widzisz tej przeglądarki sieci web hello jest zablokowany na "Autoryzowanie...", wyłącz/Usuń zaznaczenie pola wyboru **zablokować pliki cookie innych firm, a dane lokacji** ustawienie (lub) schowaj włączone i utworzyć wyjątek **login.microsoftonline.com**, a następnie spróbuj ponownie uruchomić Kreatora hello.
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a>Krok 1: Skonfiguruj harmonogram ładowanie danych
pierwszym krokiem Hello są dane hello tooconfigure ładowania harmonogramu.  

W hello **właściwości** strony:

1. Wprowadź **CopyFromBlobToAzureSqlDataWarehouse** dla **Nazwa zadania**
2. Wybierz **uruchom raz teraz** opcji.   
3. Kliknij przycisk **Dalej**.  

    ![Kreator kopiowania — strona właściwości](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a>Krok 2: Konfigurowanie źródła
Ten przedstawia sekcji hello kroki tooconfigure hello źródła: obiektów Blob platformy Azure zawierającą hello TPC 1 TB-H pozycji plików.

1. Wybierz hello **magazyn obiektów Blob Azure** danych hello przechowywania, a następnie kliknij przycisk **dalej**.

    ![Kreator kopiowania — wybierz źródło strony](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. Wypełnij hello informacje o połączeniu dla hello konta magazynu obiektów Blob platformy Azure, a następnie kliknij przycisk **dalej**.

    ![Kreator kopiowania — informacje o źródle połączenia](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. Wybierz hello **folderu** hello TPC-H wiersza zawierającego element plików, a następnie kliknij przycisk **dalej**.

    ![Kreator kopiowania — wybierz folder wejściowy](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. Po kliknięciu **dalej**, ustawienia formatu pliku hello są wykrywane automatycznie.  Sprawdź toomake się, że jest ogranicznik tej kolumny ' | 'zamiast przecinkami domyślne hello",".  Kliknij przycisk **dalej** po przejrzeniu hello danych.

    ![Kreator kopiowania — ustawienia format pliku](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a>Krok 3: Konfigurowanie docelowej
W tej sekcji przedstawiono, jak tooconfigure hello docelowego: `lineitem` tabeli w bazie danych Azure SQL Data Warehouse hello.

1. Wybierz **magazyn danych SQL Azure** jako miejsce docelowe hello przechowywania, a następnie kliknij przycisk **dalej**.

    ![Kreator kopiowania — wybierz miejsce docelowe magazynu danych](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. Wypełnij hello informacje o połączeniu dla usługi Azure SQL Data Warehouse.  Upewnij się, że Określ hello użytkownika, który jest członkiem roli hello `xlargerc` (zobacz hello **wymagania wstępne** sekcji, aby uzyskać szczegółowe instrukcje) i kliknij przycisk **dalej**.

    ![Kreator kopiowania — informacje o połączeniu docelowego](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. Wybierz tabelę docelową hello i kliknij przycisk **dalej**.

    ![Kreator kopiowania — strona mapowania tabeli](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. Na stronie mapowania schematu, nie zaznaczaj opcji "Zastosować mapowanie kolumn" wyboru i kliknij przycisk **dalej**.

## <a name="step-4-performance-settings"></a>Krok 4: Ustawienia wydajności

**Zezwalaj na polybase** jest domyślnie zaznaczone.  Kliknij przycisk **Dalej**.

![Kreator kopiowania — strona mapowanie schematu](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a>Krok 5: Wdrażanie i monitorowanie wyników obciążenia
1. Kliknij przycisk **Zakończ** toodeploy przycisku.

    ![Kreator kopiowania — strona podsumowania](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. Po zakończeniu wdrażania powitania kliknij `Click here toomonitor copy pipeline` kopiowania hello toomonitor Uruchom postępu. Potok kopiowania hello wybierz utworzony w hello **okien działania** listy.

    ![Kreator kopiowania — strona podsumowania](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    Możesz wyświetlić szczegóły uruchomienia w hello kopiowania hello **działania okna Eksploratora** hello prawym panelu, w tym ilość danych hello odczytywane źródła i zapisywane na docelowy, czas trwania i średniej przepływności hello hello Uruchom.

    Jak widać na powitania po zrzut ekranu, kopiowanie 1 TB danych z magazynu obiektów Blob Azure do usługi SQL Data Warehouse trwało 14 minut, efektywnie uzyskanie 1,22 przepływności GB/s!

    ![Kreator kopiowania — okno dialogowe zakończyło się pomyślnie](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a>Najlepsze praktyki
Poniżej przedstawiono kilka najlepszych rozwiązań dotyczących bazy danych Azure SQL Data Warehouse:

* Używanie większych klasy zasobu, podczas ładowania do KLASTROWANEGO INDEKSU magazynu kolumn.
* Dla bardziej wydajne sprzężeń należy wziąć pod uwagę przy użyciu skrótu dystrybucji przez wybierz kolumnę, zamiast domyślnej round dystrybucji działania okrężnego.
* Szybsze szybkości obciążenia należy wziąć pod uwagę przy użyciu sterty przejściowej danych.
* Tworzenie statystyk po zakończeniu ładowania magazyn danych SQL Azure.

Zobacz [najlepsze rozwiązania dotyczące usługi Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) szczegółowe informacje.

## <a name="next-steps"></a>Następne kroki
* [Kreator kopiowania fabryki danych](data-factory-copy-wizard.md) — w tym artykule przedstawiono szczegóły hello kreatora kopiowania.
* [Skopiuj wydajności działania i dostrajania przewodnik](data-factory-copy-activity-performance.md) — ten artykuł zawiera hello pomiarów wydajności i dostrajania przewodnik.
