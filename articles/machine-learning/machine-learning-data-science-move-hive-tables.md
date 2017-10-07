---
title: "aaaCreate Hive tabel i ładowanie danych z magazynu obiektów Blob platformy Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie tabel programu Hive i załadować dane w tabelach toohive obiektów blob"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>Tworzenie tabel programu Hive i ładowanie danych z magazynu obiektów Blob Azure
W tym temacie przedstawiono ogólne zapytań Hive, które Tworzenie tabel programu Hive i ładowanie danych z magazynu obiektów blob platformy Azure. Instrukcje dostępne są również na partycje tabele programu Hive i przy użyciu hello zoptymalizowanych pod kątem wiersza kolumnowy (ORC) formatowania tooimprove kwerendy wydajności.

To **menu** łączy tootopics, które opisują sposób tooingest danych w środowisku docelowym, gdzie hello dane mogą być przechowywane i przetwarzane podczas hello zespołu danych nauki procesu (TDSP).

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>Wymagania wstępne
W tym artykule przyjęto założenie, że masz:

* Utworzone konto magazynu platformy Azure. Aby uzyskać instrukcje, zobacz [kont magazynu Azure o](../storage/common/storage-create-storage-account.md).
* Zainicjowano obsługę administracyjną dostosowane klastra usługi Hadoop z hello usługi HDInsight.  Aby uzyskać instrukcje, zobacz [dostosować Azure HDInsight Hadoop clusters zaawansowana analityka](machine-learning-data-science-customize-hadoop-cluster.md).
* Klastra toohello włączone dostępu zdalnego, zalogowany i otworzyć konsolę wiersza polecenia hello Hadoop. Aby uzyskać instrukcje, zobacz [hello dostępu Head węzeł z klastra usługi Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="upload-data-tooazure-blob-storage"></a>Przekazywanie danych tooAzure obiektu blob magazynu
Jeśli utworzono maszynę wirtualną platformy Azure, wykonując instrukcje hello podane w [Konfigurowanie maszyny wirtualnej platformy Azure, zaawansowana analityka](machine-learning-data-science-setup-virtual-machine.md), ten plik skryptu powinien być pobrany toohello *C:\\ Użytkownicy\\\<nazwy użytkownika\>\\dokumenty\\skryptów nauki danych* katalogu hello maszyny wirtualnej. Te zapytania Hive wymagają tylko należy podłączyć własny schemat danych i konfiguracji magazynu obiektów blob platformy Azure w toobe odpowiednich pól hello jest gotowy do przesłania.

Przyjęto założenie, że dane hello tabele programu Hive są w **nieskompresowanych** tabelarycznej i że hello dane zostały przekazane toohello domyślne (lub tooan dodatkowe) kontenera konta magazynu hello używane przez klaster Hadoop hello.

Jeśli chcesz, aby toopractice na powitania **NYC taksówki podróży danych**, musisz:

* **Pobierz** hello 24 [danych podróży taksówki NYC](http://www.andresmh.com/nyctaxitrips) plików (12 pliki podróży i pliki taryfy 12),
* **Rozpakuj** wszystkie pliki w pliki CSV, a następnie
* **Przekaż** ich toohello domyślne lub odpowiedniego kontenera hello kontem magazynu platformy Azure, który został utworzony przez hello procedury opisane w hello [dostosować Azure HDInsight Hadoop clusters zaawansowane procesu analizy i technologii ](machine-learning-data-science-customize-hadoop-cluster.md) tematu. Witaj procesu tooupload hello CSV pliki toohello domyślnego kontenera na koncie magazynu hello znajduje się na tym [strony](machine-learning-data-science-process-hive-walkthrough.md#upload).

## <a name="submit"></a>Jak toosubmit zapytań programu Hive
Można przesłać zapytań programu hive za pomocą:

1. [Wysyłanie zapytań programu Hive za pomocą wiersza polecenia platformy Hadoop w headnode klastra usługi Hadoop](#headnode)
2. [Wysyłanie zapytań programu Hive z hello Edytor Hive](#hive-editor)
3. [Wysyłanie zapytań programu Hive z poleceń programu PowerShell Azure](#ps)

Zapytania hive są przypominającego SQL. Jeśli znasz SQL, może się okazać hello [Hive arkusza Cheat użytkowników SQL](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf) przydatne.

Podczas składania zapytań programu Hive, można też kontrolować hello miejsce docelowe danych wyjściowych hello z zapytań programu Hive, czy jest na powitania ekranu lub tooa pliku lokalnego dla węzła głównego hello lub tooan obiektów blob platformy Azure.

### <a name="headnode"></a> 1. Wysyłanie zapytań programu Hive za pomocą wiersza polecenia platformy Hadoop w headnode klastra usługi Hadoop
Jeśli hello Hive zapytanie jest złożony, przesłanie bezpośrednio w hello węzła głównego klastra usługi Hadoop hello zwykle prowadzi Włącz toofaster wokół niż przesłania go w edytorze Hive lub skryptów programu Azure PowerShell.

Zaloguj się za toohello węzła głównego klastra usługi Hadoop hello, otwórz hello wiersza polecenia usługi Hadoop na pulpicie hello hello węzła głównego i wprowadź polecenie `cd %hive_home%\bin`.

Masz zapytań programu Hive toosubmit trzy sposoby w hello Hadoop wiersza polecenia:

* bezpośrednio
* przy użyciu plików .hql
* z hello Hive konsoli poleceń

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>Wysyłanie zapytań programu Hive bezpośrednio w Hadoop wiersza polecenia.
Możesz uruchomić polecenie, takie jak `hive -e "<your hive query>;` toosubmit prostych zapytań programu Hive bezpośrednio w Hadoop wiersza polecenia. Oto przykład, gdy zawiera pole hello red hello polecenia, który przesyła zapytanie Hive hello i hello zielone pole zawiera hello dane wyjściowe zapytań Hive hello.

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>Wysyłanie zapytań programu Hive w plikach .hql
Jeśli zapytanie Hive hello jest bardziej skomplikowany i ma wiele wierszy, edytowanie zapytań w wierszu polecenia lub konsoli poleceń gałęzi nie jest praktyczne. Alternatywą jest toouse edytora tekstu, w węźle głównym hello hello Hadoop klastra toosave hello zapytań programu Hive w pliku .hql w katalogu lokalnym hello węzła głównego. Następnie hello zapytanie Hive w pliku .hql hello można przesłać za pomocą hello `-f` argument w następujący sposób:

    hive -f "<path toohello .hql file>"

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**Pomiń postępu stan ekranu drukowania zapytań Hive**

Domyślnie po wysłaniu zapytania Hive w wierszu polecenia Hadoop hello postęp zadania mapy/Zmniejsz hello jest drukowany na ekranie. toosuppress hello drukowania ekran postępu zadania mapy/Zmniejsz hello, można użyć argumentu `-S` ("S" wielkimi literami) w hello wiersza polecenia w następujący sposób:

    hive -S -f "<path toohello .hql file>"
.    -S -e hive "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>Wysyłanie zapytań programu Hive z konsoli poleceń Hive.
Można również najpierw wprowadzić konsoli poleceń hello Hive, uruchamiając polecenie `hive` w wierszu polecenia Hadoop, a następnie wysyłanie zapytań programu Hive z konsoli poleceń Hive. Oto przykład. W tym przykładzie hello dwa pola czerwone wyróżnienie hello polecenia używane tooenter hello Hive konsoli poleceń i hello przesłane w konsoli polecenie gałęzi odpowiednio zapytanie Hive. wyróżnione hello dane wyjściowe zapytań Hive hello Hello zielony.

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

Witaj w poprzednich przykładach output bezpośrednio wyników zapytania Hive hello na ekranie. Można również napisać pliku lokalnego tooa dane wyjściowe hello na powitania węzła głównego lub tooan obiektów blob platformy Azure. Następnie należy użyć innych narzędzi toofurther analizować dane wyjściowe hello zapytań programu Hive.

**Dane wyjściowe pliku lokalnego tooa wyników zapytania Hive.**
toooutput Hive zapytania wyniki tooa katalogu lokalnego na powitania węzła głównego, masz zapytanie Hive hello toosubmit w hello wiersza polecenia platformy Hadoop w następujący sposób:

    hive -e "<hive query>" > <local path in hello head node>

W hello poniższy przykład, dane wyjściowe hello zapytania Hive są zapisywane do pliku `hivequeryoutput.txt` w katalogu `C:\apps\temp`.

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**Dane wyjściowe tooan wyników zapytania Hive obiektów blob platformy Azure**

Można również output hello Hive zapytania wyniki tooan obiektów blob platformy Azure w kontenerze domyślna hello hello klastra usługi Hadoop. Zapytanie Hive Hello tego przebiega następująco:

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

W hello poniższy przykład, dane wyjściowe hello zapytania Hive są zapisywane katalogu obiektu blob tooa `queryoutputdir` w kontenerze domyślna hello hello klastra usługi Hadoop. W tym miejscu wystarczy tylko nazwę katalogu hello tooprovide, bez hello nazwa obiektu blob. Zostanie zgłoszony błąd, jeśli zostaną podane nazwy usługi directory i obiektów blob, takich jak `wasb:///queryoutputdir/queryoutput.txt`.

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

Po otwarciu hello domyślny kontener hello klastra platformy Hadoop za pomocą Eksploratora usługi Storage Azure widać hello dane wyjściowe zapytań Hive hello pokazane na powitania po rysunku. Możesz zastosować hello blob hello pobrać tooonly filtru (wyróżniony przez czerwonym prostokątem) z określonej litery w nazwach.

![Tworzenie obszaru roboczego](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2. Wysyłanie zapytań programu Hive z hello Edytor Hive
Umożliwia także hello zapytania konsoli (Edytor Hive), wprowadzając adres URL w postaci hello *https://&#60; Nazwa klastra Hadoop >.azurehdinsight.net/Home/HiveEditor* w przeglądarce sieci web. Musi być zalogowany Zobacz hello tej konsoli i dlatego potrzebne są poświadczenia klastra usługi Hadoop.

### <a name="ps"></a> 3. Wysyłanie zapytań programu Hive z poleceń programu PowerShell Azure
Umożliwia także zapytań Hive toosubmit środowiska PowerShell. Aby uzyskać instrukcje, zobacz [zadania Hive przesyłania przy użyciu programu PowerShell](../hdinsight/hdinsight-hadoop-use-hive-powershell.md).

## <a name="create-tables"></a>Utwórz gałąź bazy danych i tabel
Witaj zapytań programu Hive są udostępniane w hello [repozytorium GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql) i może zostać pobrany z tego miejsca.

Oto zapytanie Hive hello utworzona tabela programu Hive.

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

Poniżej przedstawiono opisy hello hello pola, które muszą tooplug w i inne konfiguracje:

* **&#60; Nazwa bazy danych >**: Nazwa hello hello bazy danych, które mają toocreate. Jeśli chcesz toouse hello domyślna baza danych, hello zapytania *tworzenie bazy danych...*  można pominąć.
* **&#60; Nazwa tabeli >**: hello Nazwa tabeli hello, które mają toocreate w hello określonej bazy danych. Toouse hello domyślna baza danych należy hello tabeli mogą być bezpośrednio przywoływane przez *&#60; Nazwa tabeli >* bez &#60; Nazwa bazy danych >.
* **&#60; separator pola >**: hello separatora, ograniczającego pól w toobe pliku danych hello przekazać toohello tabelę programu Hive.
* **&#60; linii separatora >**: hello separatora, ograniczającego wierszy w pliku danych hello.
* **&#60; lokalizacja magazynu >**: hello danych hello toosave lokalizacji magazynu platformy Azure z tabele programu Hive. Jeśli nie określisz *lokalizacji &#60; lokalizacja magazynu >*, hello bazy danych i hello tabele są przechowywane w *gałęzi/magazynu/* katalogu w kontenerze domyślna hello hello klastra gałąź domyślną. Lokalizacja magazynu hello toospecify należy hello lokalizacji magazynu ma toobe w kontenerze domyślna hello hello bazy danych i tabele. Tej lokalizacji jest określane jako lokalizacji względnej toohello domyślny kontener hello klastra w formacie hello toobe *"wasb: / / / &#60; katalogu 1 > /"* lub *"wasb: lokalizacje &#60; katalogu 1 > / &#60; katalog 2 > / "*itp. Po wykonaniu zapytania hello hello względną katalogi są tworzone w ramach hello domyślnego kontenera.
* **TBLPROPERTIES("SKIP.Header.line.Count"="1")**: Jeśli plik danych hello ma wiersz nagłówka, masz tooadd tej właściwości **na końcu hello** z hello *Utwórz tabelę* zapytania. W przeciwnym razie wiersz nagłówka hello jest ładowany jako tabelę toohello rekordów. Jeśli plik danych hello nie ma wiersz nagłówka, w zapytaniu hello można pominąć tej konfiguracji.

## <a name="load-data"></a>Tabele tooHive danych obciążenia
Oto hello zapytania Hive, który ładuje dane do tabeli programu Hive.

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; ścieżka tooblob dane >**: w przypadku tabeli Hive toohello toobe przekazany plik hello obiektów blob w kontenerze domyślna hello z hello klastra usługi HDInsight Hadoop, hello *&#60; ścieżka tooblob dane >* powinna mieć format hello *"wasb: / / / &#60; katalog, w tym kontenerze > / &#60; nazwa pliku obiektu blob >"*. Witaj pliku blob może być również w dodatkowych kontenera hello klastra usługi HDInsight Hadoop. W takim przypadku *&#60; ścieżka tooblob dane >* powinna mieć format hello *"wasb: / / &#60; nazwa kontenera > @&#60; nazwa konta magazynu >.blob.core.windows.net/ &#60; nazwa pliku obiektu blob >"*.

  > [!NOTE]
  > Hello obiektu blob danych toobe przekazać tooHive tabela ma toobe w domyślnej hello lub dodatkowego kontenera hello konta magazynu dla klastra usługi Hadoop hello. W przeciwnym razie hello *danych obciążenia* działanie nie powiodło się Strona skarżąca, że nie ma dostępu do danych hello.
  >
  >

## <a name="partition-orc"></a>Tematy zaawansowane: podzielona na partycje tabeli i magazynu danych gałęzi w formacie ORC
W przypadku dużych danych hello partycjonowania tabeli hello jest korzystne dla zapytań, które potrzebują tylko tooscan kilka partycji tabeli hello. Na przykład jest uzasadnione toopartition hello dziennika danych witryny sieci web według daty.

W dodatku toopartitioning Hive tabel, jest również przydatne toostore hello Hive dane w formacie zoptymalizowanych pod kątem wiersza kolumnowy (ORC) hello. Aby uzyskać więcej informacji na ORC formatowania, zobacz <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">plików ORC przy użyciu zwiększa wydajność podczas czytania, zapisywania i przetwarzania danych Hive</a>.

### <a name="partitioned-table"></a>Tabeli partycjonowanej
Oto zapytanie Hive hello tworzy tabeli partycjonowanej i ładuje dane do niego.

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

Podczas wykonywania zapytania partycjonowane tabele, zaleca się tooadd hello partycji warunku w hello **początku** z hello `where` skuteczności hello wyszukiwanie znacznie zwiększa klauzuli jako to.

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>Przechowywanie danych gałęzi w formacie ORC
Nie można bezpośrednio ładowanie danych z magazynu obiektów blob do gałęzi tabel, które są przechowywane w formacie ORC hello. Poniżej przedstawiono kroki hello tooHive tabel są przechowywane w formacie ORC obiektów blob tego hello należy tootake tooload danych z platformy Azure.

Tworzenie tabeli zewnętrznej **TEXTFILE AS PRZECHOWYWANE** i ładowanie danych z tabeli toohello magazynu obiektów blob.

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

Tworzenie wewnętrznej tabeli z hello tego samego schematu jako hello tabeli zewnętrznej w kroku 1, z hello sam ogranicznik pola i przechowywać hello Hive dane w formacie ORC hello.

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

Wybierz dane z tabeli zewnętrznej hello w kroku 1 i Wstaw do tabeli ORC hello

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> Jeśli tabela TEXTFILE hello *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli zewnętrznej textfile >* zawiera partycje, w KROKU 3 hello `SELECT * FROM <database name>.<external textfile table name>` polecenia wybiera hello zmiennej partycji pola w hello zwrócony zestawu danych. Wstawienie go w hello *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >* nie powiedzie się, ponieważ *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >* nie ma hello partycji zmiennej jako pole w hello schemat tabeli. W takim przypadku należy toobe pól select hello toospecifically dodaje zbyt*&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >* w następujący sposób:
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

Jest bezpieczne toodrop hello *&#60; Nazwa tabeli zewnętrznej textfile >* po użyciu hello następującego zapytania po wszystkich danych został wstawiony do *&#60; Nazwa bazy danych >. &#60; Nazwa tabeli ORC >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

Po wykonaniu tej procedury, powinien mieć tabelę z danymi w toouse gotowy hello ORC format.  
