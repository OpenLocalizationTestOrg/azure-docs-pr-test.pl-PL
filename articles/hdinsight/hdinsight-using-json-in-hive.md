---
title: "aaaAnalyze i JSON procesu dokumentów przy użyciu Hive w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse JSON dokumenty i analizować je przy użyciu Hive w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>Przetwarzanie i analizowanie dokumentów JSON przy użyciu Hive w usłudze HDInsight

Dowiedz się, jak tooprocess i analizować pliki w formacie JSON przy użyciu Hive w usłudze HDInsight. powitania po dokumentu JSON jest używana w samouczku hello:

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

Hello plików można znaleźć w folderze wasb://processjson@hditutorialdata.blob.core.windows.net/. Aby uzyskać więcej informacji na temat używania magazynu obiektów Blob platformy Azure z usługą HDInsight, zobacz [magazynu obiektów Blob platformy Azure zgodnego systemem plików HDFS Użyj z platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-use-blob-storage.md). Możesz skopiować hello pliku toohello domyślny kontener klastra.

W tym samouczku używa się konsoli Hive hello.  Instrukcje dotyczące otwierania konsoli Hive hello znajdują się [używanie Hive z usługą Hadoop w usłudze HDInsight przy użyciu pulpitu zdalnego](hdinsight-hadoop-use-hive-remote-desktop.md).

## <a name="flatten-json-documents"></a>Spłaszczanie dokumentów JSON
metody Hello wymienionych w następnej sekcji hello wymagają hello dokument JSON w jednym wierszu. Dlatego należy spłaszczanie ciągu tooa dokumentu JSON hello. Jeśli już właściwości jest spłaszczona dokumentu JSON, można pominąć ten krok i przejdź na dane JSON analizowanie proste toohello następnej sekcji.

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

Hello plik JSON raw znajduje się pod adresem  **wasb://processjson@hditutorialdata.blob.core.windows.net/** . Witaj *StudentsRaw* raw poprzedniego dokumentu JSON toohello wskazuje tabelę programu Hive.

Witaj *StudentsOneLine* tabelę programu Hive przechowuje dane hello w hello HDInsight domyślnego systemu plików w obszarze hello */json/uczniów lubstudentów/* ścieżki.

Instrukcja INSERT Hello wypełnia hello StudentOneLine tabelę z danymi JSON hello spłaszczona.

Instrukcja SELECT Hello zwracają tylko jeden wiersz.

Poniżej przedstawiono dane wyjściowe hello instrukcji SELECT hello:

![Spłaszczanie hello dokumentu JSON.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>Analizowanie dokumentów JSON w gałęzi
Gałąź zawiera trzy różne mechanizmy toorun zapytania dotyczące dokumentów JSON:

* Użyj hello GET\_JSON\_obiektu funkcji zdefiniowanej przez użytkownika (funkcji zdefiniowanej przez użytkownika)
* Użyj hello JSON_TUPLE funkcji zdefiniowanej przez użytkownika
* Użyj niestandardowych SerDe
* zapisu własnej funkcji zdefiniowanej przez użytkownika za pomocą języka Python lub innych języków. Zobacz [w tym artykule] [ hdinsight-python] uruchamiania kodu języka Python z gałęzi.

### <a name="use-hello-getjsonobject-udf"></a>Użyj hello GET\_JSON_OBJECT funkcji zdefiniowanej przez użytkownika
Gałąź zapewnia wbudowanej funkcji zdefiniowanej przez użytkownika o nazwie [, Pobierz obiekt json](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), które można wykonywać zapytań JSON w czasie wykonywania. Ta metoda przyjmuje dwa argumenty — Witaj nazwę tabeli i nazwę metody, która ma hello spłaszczoną JSON hello i dokumentów JSON pola, które należy przeanalizować toobe. Przyjrzyjmy się toosee przykład działania tej funkcji zdefiniowanej przez użytkownika.

Pobierz hello imię i nazwisko dla użytkowników

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

Poniżej przedstawiono dane wyjściowe hello podczas uruchamiania tego zapytania w oknie konsoli.

![get_json_object funkcji zdefiniowanej przez użytkownika][image-hdi-hivejson-getjsonobject]

Istnieje kilka ograniczeń hello get-json_object funkcji zdefiniowanej przez użytkownika.

* Ponieważ każde pole w zapytaniu hello wymaga ponownej analizy hello zapytania, wpływa to na wydajność hello.
* Pobierz\_JSON_OBJECT() zwraca reprezentację ciągu hello tablicy. tooconvert tej tablicy tooa Hive tablicy ma tooreplace wyrażeń regularnych toouse hello nawiasów kwadratowych "[" i "]", a następnie również wywołania podział tooget hello tablicy.

Jest to, dlaczego hello Hive wiki zaleca korzystanie z json_tuple.  

### <a name="use-hello-jsontuple-udf"></a>Użyj hello JSON_TUPLE funkcji zdefiniowanej przez użytkownika
Inny UDF udostępniane przez Hive jest wywoływana [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), który wykonuje lepszym rozwiązaniem niż [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object). Ta metoda przyjmuje zestaw kluczy i ciągu JSON i zwraca spójną kolekcję wartości przy użyciu jednej funkcji. Hello następujące zapytanie zwraca identyfikator uczniów hello i klasy hello z dokumentu JSON hello:

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

dane wyjściowe Hello tego skryptu w konsoli Hive hello:

![json_tuple funkcji zdefiniowanej przez użytkownika][image-hdi-hivejson-jsontuple]

JSON\_KROTKI używa hello [penetracji widoku](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) składni w gałęzi, dzięki czemu json\_toocreate krotki wirtualnego tabelę, stosując hello UDT funkcja tooeach wiersza oryginalnej tabeli hello.  Użyj złożonych JSONs być zbyt trudno obsługiwać ze względu na powitania powtarzany PENETRACJI widoku. Ponadto JSON_TUPLE nie może obsłużyć JSONs zagnieżdżonych.

### <a name="use-custom-serde"></a>Użyj niestandardowych SerDe
SerDe hello najlepszym wyborem do analizowania zagnieżdżonej dokumentów JSON, pozwala schematu JSON hello toodefine i użyj hello schematu tooparse hello dokumentów. W tym samouczku, użyj jednej z hello SerDe bardziej popularne, który został opracowany przez [Roberto Congiu](https://github.com/rcongiu).

**toouse hello SerDe niestandardowe:**

1. Zainstaluj [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR). Wybierz wersję systemu Windows X64 hello hello JDK, jeśli ma toobe przy użyciu wdrażania systemu Windows hello usługi hdinsight
   
   > [!WARNING]
   > JDK 1.8 nie działa z tym SerDe.
   > 
   > 
   
    Po zakończeniu instalacji hello, Dodaj nową zmienną środowiskową użytkownika:
   
   1. Otwórz **widoku Zaawansowane ustawienia systemu** z ekranu Windows hello.
   2. Kliknij przycisk **zmiennych środowiskowych**.  
   3. Dodaj nową **JAVA_HOME** zbyt wskazuje zmiennej środowiskowej**C:\Program Files\Java\jdk1.7.0_55** lub wszędzie tam, gdzie jest zainstalowana z JDK.
      
      ![Definiowanie konfiguracji poprawne wartości dla JDK][image-hdi-hivejson-jdk]
2. Zainstaluj [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    Dodaj ścieżkę tooyour folder bin hello przechodząc tooControl panelu--> Edytuj zmienne systemowe hello zmiennych środowiskowych Twojego konta. Witaj Poniższy zrzut ekranu pokazuje jak toodo to.
   
    ![Konfigurowanie Maven][image-hdi-hivejson-maven]
3. Klonowanie hello projektu z [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) witryny github. Można to zrobić, klikając przycisk "Pobierz Zip" hello, jak pokazano w powitania po zrzut ekranu.
   
    ![Klonowanie hello projektu][image-hdi-hivejson-serde]

4: Przejdź toohello folder, gdzie został pobrany tego pakietu, a następnie wpisz "mvn pakietu". Ten należy utworzyć hello jar niezbędne pliki, które można następnie skopiować za pośrednictwem toohello klastra.

5: folder docelowy toohello go w folderze głównym hello której pobrano pakiet hello. Przekaż hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar pliku toohead węzłów klastra. Zazwyczaj umieścić go w folderze binarne hive hello: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin lub podobny.

6: hello wiersza hive, wpisz "Dodaj jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar". Ponieważ w moim przypadku hello jar znajduje się w folderze C:\apps\dist\hive-0.13.x\bin hello, można bezpośrednio dodać jar hello o nazwie hello, jak pokazano:

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Dodanie JAR tooyour projektu][image-hdi-hivejson-addjar]

Teraz wszystko jest gotowe toouse hello SerDe toorun zapytań dotyczących dokumentów JSON hello.

Po instrukcji Hello tworzy tabelę z określonego schematu:

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

toolist hello imię i nazwisko student hello

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

Oto hello wyniku hello Hive konsoli.

![Zapytanie SerDe 1][image-hdi-hivejson-serde_query1]

Suma hello toocalculate wyniki hello dokumentu JSON

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

Hello poprzedzających używa zapytania [rozłożyć penetracji widoku](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello tablicy wyników, dzięki czemu mogą być sumowane.

Poniżej przedstawiono dane wyjściowe konsoli Hive hello hello.

![Zapytanie SerDe 2][image-hdi-hivejson-serde_query2]

toofind, które tematy danego uczniów ma przyznane więcej niż 80 punkty:

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

Hello poprzedniego zapytanie zwraca tablicę gałęzi, w odróżnieniu od get\_json\_obiektu, który zwraca wartość typu ciąg.

![Zapytanie SerDe 3][image-hdi-hivejson-serde_query3]

Jeśli chcesz, aby tooskil nieprawidłowo sformatowany kod JSON, a następnie jako hello wyjaśniono w [strona typu wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) z tym SerDe można osiągnąć który wpisując hello następującego kodu:  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>Podsumowanie
Podsumowując typ hello operatora JSON w gałęzi, którą można wybrać zależy od danego scenariusza. Jeśli proste dokument JSON i masz tylko jedną toolook pola — możesz wybrać get Hive UDF hello toouse\_json\_obiektu. Jeśli masz więcej niż jednego klucza toolook, można użyć json_tuple. Jeśli masz zagnieżdżonych dokumentu, należy używać hello JSON SerDe.

## <a name="next-steps"></a>Następne kroki

Aby uzyskać inne pokrewne artykuły zobacz

* [Używanie Hive i HiveQL z usługą Hadoop w HDInsight tooanalyze przykładowego pliku Apache log4j](hdinsight-use-hive.md)
* [Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Analizowanie danych Twitter przy użyciu Hive w usłudze HDInsight](hdinsight-analyze-twitter-data.md)
* [Uruchomienie zadania usługi Hadoop przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
