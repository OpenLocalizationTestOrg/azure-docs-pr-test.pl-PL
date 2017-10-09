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
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a><span data-ttu-id="2189d-103">Przetwarzanie i analizowanie dokumentów JSON przy użyciu Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="2189d-103">Process and analyze JSON documents using Hive in HDInsight</span></span>

<span data-ttu-id="2189d-104">Dowiedz się, jak tooprocess i analizować pliki w formacie JSON przy użyciu Hive w usłudze HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2189d-104">Learn how tooprocess and analyze JSON files using Hive in HDInsight.</span></span> <span data-ttu-id="2189d-105">powitania po dokumentu JSON jest używana w samouczku hello:</span><span class="sxs-lookup"><span data-stu-id="2189d-105">hello following JSON document is used in hello tutorial:</span></span>

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

<span data-ttu-id="2189d-106">Hello plików można znaleźć w folderze wasb://processjson@hditutorialdata.blob.core.windows.net/.</span><span class="sxs-lookup"><span data-stu-id="2189d-106">hello file can be found at wasb://processjson@hditutorialdata.blob.core.windows.net/.</span></span> <span data-ttu-id="2189d-107">Aby uzyskać więcej informacji na temat używania magazynu obiektów Blob platformy Azure z usługą HDInsight, zobacz [magazynu obiektów Blob platformy Azure zgodnego systemem plików HDFS Użyj z platformą Hadoop w usłudze HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="2189d-107">For more information on using Azure Blob storage with HDInsight, see [Use HDFS-compatible Azure Blob storage with Hadoop in HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="2189d-108">Możesz skopiować hello pliku toohello domyślny kontener klastra.</span><span class="sxs-lookup"><span data-stu-id="2189d-108">You can copy hello file toohello default container of your cluster.</span></span>

<span data-ttu-id="2189d-109">W tym samouczku używa się konsoli Hive hello.</span><span class="sxs-lookup"><span data-stu-id="2189d-109">In this tutorial, you use hello Hive console.</span></span>  <span data-ttu-id="2189d-110">Instrukcje dotyczące otwierania konsoli Hive hello znajdują się [używanie Hive z usługą Hadoop w usłudze HDInsight przy użyciu pulpitu zdalnego](hdinsight-hadoop-use-hive-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="2189d-110">For instructions of opening hello Hive console, see [Use Hive with Hadoop on HDInsight with Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md).</span></span>

## <a name="flatten-json-documents"></a><span data-ttu-id="2189d-111">Spłaszczanie dokumentów JSON</span><span class="sxs-lookup"><span data-stu-id="2189d-111">Flatten JSON documents</span></span>
<span data-ttu-id="2189d-112">metody Hello wymienionych w następnej sekcji hello wymagają hello dokument JSON w jednym wierszu.</span><span class="sxs-lookup"><span data-stu-id="2189d-112">hello methods listed in hello next section require hello JSON document in a single row.</span></span> <span data-ttu-id="2189d-113">Dlatego należy spłaszczanie ciągu tooa dokumentu JSON hello.</span><span class="sxs-lookup"><span data-stu-id="2189d-113">So you must flatten hello JSON document tooa string.</span></span> <span data-ttu-id="2189d-114">Jeśli już właściwości jest spłaszczona dokumentu JSON, można pominąć ten krok i przejdź na dane JSON analizowanie proste toohello następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="2189d-114">If your JSON document is already flattened, you can skip this step and go straight toohello next section on Analyzing JSON data.</span></span>

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

<span data-ttu-id="2189d-115">Hello plik JSON raw znajduje się pod adresem  **wasb://processjson@hditutorialdata.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="2189d-115">hello raw JSON file is located at **wasb://processjson@hditutorialdata.blob.core.windows.net/**.</span></span> <span data-ttu-id="2189d-116">Witaj *StudentsRaw* raw poprzedniego dokumentu JSON toohello wskazuje tabelę programu Hive.</span><span class="sxs-lookup"><span data-stu-id="2189d-116">hello *StudentsRaw* Hive table points toohello raw unflattened JSON document.</span></span>

<span data-ttu-id="2189d-117">Witaj *StudentsOneLine* tabelę programu Hive przechowuje dane hello w hello HDInsight domyślnego systemu plików w obszarze hello */json/uczniów lubstudentów/* ścieżki.</span><span class="sxs-lookup"><span data-stu-id="2189d-117">hello *StudentsOneLine* Hive table stores hello data in hello HDInsight default file system under hello */json/students/* path.</span></span>

<span data-ttu-id="2189d-118">Instrukcja INSERT Hello wypełnia hello StudentOneLine tabelę z danymi JSON hello spłaszczona.</span><span class="sxs-lookup"><span data-stu-id="2189d-118">hello INSERT statement populates hello StudentOneLine table with hello flattened JSON data.</span></span>

<span data-ttu-id="2189d-119">Instrukcja SELECT Hello zwracają tylko jeden wiersz.</span><span class="sxs-lookup"><span data-stu-id="2189d-119">hello SELECT statement shall only return one row.</span></span>

<span data-ttu-id="2189d-120">Poniżej przedstawiono dane wyjściowe hello instrukcji SELECT hello:</span><span class="sxs-lookup"><span data-stu-id="2189d-120">Here is hello output of hello SELECT statement:</span></span>

![Spłaszczanie hello dokumentu JSON.][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a><span data-ttu-id="2189d-122">Analizowanie dokumentów JSON w gałęzi</span><span class="sxs-lookup"><span data-stu-id="2189d-122">Analyze JSON documents in Hive</span></span>
<span data-ttu-id="2189d-123">Gałąź zawiera trzy różne mechanizmy toorun zapytania dotyczące dokumentów JSON:</span><span class="sxs-lookup"><span data-stu-id="2189d-123">Hive provides three different mechanisms toorun queries on JSON documents:</span></span>

* <span data-ttu-id="2189d-124">Użyj hello GET\_JSON\_obiektu funkcji zdefiniowanej przez użytkownika (funkcji zdefiniowanej przez użytkownika)</span><span class="sxs-lookup"><span data-stu-id="2189d-124">use hello GET\_JSON\_OBJECT UDF (User-defined function)</span></span>
* <span data-ttu-id="2189d-125">Użyj hello JSON_TUPLE funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="2189d-125">use hello JSON_TUPLE UDF</span></span>
* <span data-ttu-id="2189d-126">Użyj niestandardowych SerDe</span><span class="sxs-lookup"><span data-stu-id="2189d-126">use custom SerDe</span></span>
* <span data-ttu-id="2189d-127">zapisu własnej funkcji zdefiniowanej przez użytkownika za pomocą języka Python lub innych języków.</span><span class="sxs-lookup"><span data-stu-id="2189d-127">write you own UDF using Python or other languages.</span></span> <span data-ttu-id="2189d-128">Zobacz [w tym artykule] [ hdinsight-python] uruchamiania kodu języka Python z gałęzi.</span><span class="sxs-lookup"><span data-stu-id="2189d-128">See [this article][hdinsight-python] on running your own Python code with Hive.</span></span>

### <a name="use-hello-getjsonobject-udf"></a><span data-ttu-id="2189d-129">Użyj hello GET\_JSON_OBJECT funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="2189d-129">Use hello GET\_JSON_OBJECT UDF</span></span>
<span data-ttu-id="2189d-130">Gałąź zapewnia wbudowanej funkcji zdefiniowanej przez użytkownika o nazwie [, Pobierz obiekt json](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), które można wykonywać zapytań JSON w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="2189d-130">Hive provides a built-in UDF called [get json object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object), which can perform JSON querying during run time.</span></span> <span data-ttu-id="2189d-131">Ta metoda przyjmuje dwa argumenty — Witaj nazwę tabeli i nazwę metody, która ma hello spłaszczoną JSON hello i dokumentów JSON pola, które należy przeanalizować toobe.</span><span class="sxs-lookup"><span data-stu-id="2189d-131">This method takes two arguments – hello table name and method name, which has hello flattened JSON document and hello JSON field that needs toobe parsed.</span></span> <span data-ttu-id="2189d-132">Przyjrzyjmy się toosee przykład działania tej funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2189d-132">Let’s look at an example toosee how this UDF works.</span></span>

<span data-ttu-id="2189d-133">Pobierz hello imię i nazwisko dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="2189d-133">Get hello first name and last name for each student</span></span>

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

<span data-ttu-id="2189d-134">Poniżej przedstawiono dane wyjściowe hello podczas uruchamiania tego zapytania w oknie konsoli.</span><span class="sxs-lookup"><span data-stu-id="2189d-134">Here is hello output when running this query in console window.</span></span>

![get_json_object funkcji zdefiniowanej przez użytkownika][image-hdi-hivejson-getjsonobject]

<span data-ttu-id="2189d-136">Istnieje kilka ograniczeń hello get-json_object funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2189d-136">There are a few limitations of hello get-json_object UDF.</span></span>

* <span data-ttu-id="2189d-137">Ponieważ każde pole w zapytaniu hello wymaga ponownej analizy hello zapytania, wpływa to na wydajność hello.</span><span class="sxs-lookup"><span data-stu-id="2189d-137">Because each field in hello query requires reparsing hello query, it affects hello performance.</span></span>
* <span data-ttu-id="2189d-138">Pobierz\_JSON_OBJECT() zwraca reprezentację ciągu hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="2189d-138">GET\_JSON_OBJECT() returns hello string representation of an array.</span></span> <span data-ttu-id="2189d-139">tooconvert tej tablicy tooa Hive tablicy ma tooreplace wyrażeń regularnych toouse hello nawiasów kwadratowych "[" i "]", a następnie również wywołania podział tooget hello tablicy.</span><span class="sxs-lookup"><span data-stu-id="2189d-139">tooconvert this array tooa Hive array, you have toouse regular expressions tooreplace hello square brackets ‘[‘ and ‘]’ and then also call split tooget hello array.</span></span>

<span data-ttu-id="2189d-140">Jest to, dlaczego hello Hive wiki zaleca korzystanie z json_tuple.</span><span class="sxs-lookup"><span data-stu-id="2189d-140">This is why hello Hive wiki recommends using json_tuple.</span></span>  

### <a name="use-hello-jsontuple-udf"></a><span data-ttu-id="2189d-141">Użyj hello JSON_TUPLE funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="2189d-141">Use hello JSON_TUPLE UDF</span></span>
<span data-ttu-id="2189d-142">Inny UDF udostępniane przez Hive jest wywoływana [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), który wykonuje lepszym rozwiązaniem niż [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span><span class="sxs-lookup"><span data-stu-id="2189d-142">Another UDF provided by Hive is called [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple), which performs better than [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object).</span></span> <span data-ttu-id="2189d-143">Ta metoda przyjmuje zestaw kluczy i ciągu JSON i zwraca spójną kolekcję wartości przy użyciu jednej funkcji.</span><span class="sxs-lookup"><span data-stu-id="2189d-143">This method takes a set of keys and a JSON string, and returns a tuple of values using one function.</span></span> <span data-ttu-id="2189d-144">Hello następujące zapytanie zwraca identyfikator uczniów hello i klasy hello z dokumentu JSON hello:</span><span class="sxs-lookup"><span data-stu-id="2189d-144">hello following query returns hello student id and hello grade from hello JSON document:</span></span>

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

<span data-ttu-id="2189d-145">dane wyjściowe Hello tego skryptu w konsoli Hive hello:</span><span class="sxs-lookup"><span data-stu-id="2189d-145">hello output of this script in hello Hive console:</span></span>

![json_tuple funkcji zdefiniowanej przez użytkownika][image-hdi-hivejson-jsontuple]

<span data-ttu-id="2189d-147">JSON\_KROTKI używa hello [penetracji widoku](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) składni w gałęzi, dzięki czemu json\_toocreate krotki wirtualnego tabelę, stosując hello UDT funkcja tooeach wiersza oryginalnej tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="2189d-147">JSON\_TUPLE uses hello [lateral view](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) syntax in Hive, which allows json\_tuple toocreate a virtual table by applying hello UDT function tooeach row of hello original table.</span></span>  <span data-ttu-id="2189d-148">Użyj złożonych JSONs być zbyt trudno obsługiwać ze względu na powitania powtarzany PENETRACJI widoku.</span><span class="sxs-lookup"><span data-stu-id="2189d-148">Complex JSONs become too unwieldy because of hello repeated use of LATERAL VIEW.</span></span> <span data-ttu-id="2189d-149">Ponadto JSON_TUPLE nie może obsłużyć JSONs zagnieżdżonych.</span><span class="sxs-lookup"><span data-stu-id="2189d-149">Furthermore, JSON_TUPLE cannot handle nested JSONs.</span></span>

### <a name="use-custom-serde"></a><span data-ttu-id="2189d-150">Użyj niestandardowych SerDe</span><span class="sxs-lookup"><span data-stu-id="2189d-150">Use custom SerDe</span></span>
<span data-ttu-id="2189d-151">SerDe hello najlepszym wyborem do analizowania zagnieżdżonej dokumentów JSON, pozwala schematu JSON hello toodefine i użyj hello schematu tooparse hello dokumentów.</span><span class="sxs-lookup"><span data-stu-id="2189d-151">SerDe is hello best choice for parsing nested JSON documents, it allows you toodefine hello JSON schema, and use hello schema tooparse hello documents.</span></span> <span data-ttu-id="2189d-152">W tym samouczku, użyj jednej z hello SerDe bardziej popularne, który został opracowany przez [Roberto Congiu](https://github.com/rcongiu).</span><span class="sxs-lookup"><span data-stu-id="2189d-152">In this tutorial, you use one of hello more popular SerDe that has been developed by [Roberto Congiu](https://github.com/rcongiu).</span></span>

<span data-ttu-id="2189d-153">**toouse hello SerDe niestandardowe:**</span><span class="sxs-lookup"><span data-stu-id="2189d-153">**toouse hello custom SerDe:**</span></span>

1. <span data-ttu-id="2189d-154">Zainstaluj [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span><span class="sxs-lookup"><span data-stu-id="2189d-154">Install [Java SE Development Kit 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR).</span></span> <span data-ttu-id="2189d-155">Wybierz wersję systemu Windows X64 hello hello JDK, jeśli ma toobe przy użyciu wdrażania systemu Windows hello usługi hdinsight</span><span class="sxs-lookup"><span data-stu-id="2189d-155">Choose hello Windows X64 version of hello JDK if you are going toobe using hello Windows deployment of HDInsight</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="2189d-156">JDK 1.8 nie działa z tym SerDe.</span><span class="sxs-lookup"><span data-stu-id="2189d-156">JDK 1.8 doesn't work with this SerDe.</span></span>
   > 
   > 
   
    <span data-ttu-id="2189d-157">Po zakończeniu instalacji hello, Dodaj nową zmienną środowiskową użytkownika:</span><span class="sxs-lookup"><span data-stu-id="2189d-157">After hello installation is completed, add a new user environment variable:</span></span>
   
   1. <span data-ttu-id="2189d-158">Otwórz **widoku Zaawansowane ustawienia systemu** z ekranu Windows hello.</span><span class="sxs-lookup"><span data-stu-id="2189d-158">Open **View advanced system settings** from hello Windows screen.</span></span>
   2. <span data-ttu-id="2189d-159">Kliknij przycisk **zmiennych środowiskowych**.</span><span class="sxs-lookup"><span data-stu-id="2189d-159">Click **Environment Variables**.</span></span>  
   3. <span data-ttu-id="2189d-160">Dodaj nową **JAVA_HOME** zbyt wskazuje zmiennej środowiskowej**C:\Program Files\Java\jdk1.7.0_55** lub wszędzie tam, gdzie jest zainstalowana z JDK.</span><span class="sxs-lookup"><span data-stu-id="2189d-160">Add a new **JAVA_HOME** environment variable is pointing too**C:\Program Files\Java\jdk1.7.0_55** or wherever your JDK is installed.</span></span>
      
      ![Definiowanie konfiguracji poprawne wartości dla JDK][image-hdi-hivejson-jdk]
2. <span data-ttu-id="2189d-162">Zainstaluj [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span><span class="sxs-lookup"><span data-stu-id="2189d-162">Install [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)</span></span>
   
    <span data-ttu-id="2189d-163">Dodaj ścieżkę tooyour folder bin hello przechodząc tooControl panelu--> Edytuj zmienne systemowe hello zmiennych środowiskowych Twojego konta.</span><span class="sxs-lookup"><span data-stu-id="2189d-163">Add hello bin folder tooyour path by going tooControl Panel-->Edit hello System Variables for your account Environment variables.</span></span> <span data-ttu-id="2189d-164">Witaj Poniższy zrzut ekranu pokazuje jak toodo to.</span><span class="sxs-lookup"><span data-stu-id="2189d-164">hello following screenshot shows you how toodo this.</span></span>
   
    ![Konfigurowanie Maven][image-hdi-hivejson-maven]
3. <span data-ttu-id="2189d-166">Klonowanie hello projektu z [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) witryny github.</span><span class="sxs-lookup"><span data-stu-id="2189d-166">Clone hello project from [Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github site.</span></span> <span data-ttu-id="2189d-167">Można to zrobić, klikając przycisk "Pobierz Zip" hello, jak pokazano w powitania po zrzut ekranu.</span><span class="sxs-lookup"><span data-stu-id="2189d-167">You can do this by clicking on hello “Download Zip” button as shown in hello following screenshot.</span></span>
   
    ![Klonowanie hello projektu][image-hdi-hivejson-serde]

<span data-ttu-id="2189d-169">4: Przejdź toohello folder, gdzie został pobrany tego pakietu, a następnie wpisz "mvn pakietu".</span><span class="sxs-lookup"><span data-stu-id="2189d-169">4: Go toohello folder where you have downloaded this package and then type “mvn package”.</span></span> <span data-ttu-id="2189d-170">Ten należy utworzyć hello jar niezbędne pliki, które można następnie skopiować za pośrednictwem toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="2189d-170">This should create hello necessary jar files that you can then copy over toohello cluster.</span></span>

<span data-ttu-id="2189d-171">5: folder docelowy toohello go w folderze głównym hello której pobrano pakiet hello.</span><span class="sxs-lookup"><span data-stu-id="2189d-171">5: Go toohello target folder under hello root folder where you downloaded hello package.</span></span> <span data-ttu-id="2189d-172">Przekaż hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar pliku toohead węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="2189d-172">Upload hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar file toohead-node of your cluster.</span></span> <span data-ttu-id="2189d-173">Zazwyczaj umieścić go w folderze binarne hive hello: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin lub podobny.</span><span class="sxs-lookup"><span data-stu-id="2189d-173">I usually put it under hello hive binary folder: C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin or something similar.</span></span>

<span data-ttu-id="2189d-174">6: hello wiersza hive, wpisz "Dodaj jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar".</span><span class="sxs-lookup"><span data-stu-id="2189d-174">6: In hello hive prompt, type “add jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar”.</span></span> <span data-ttu-id="2189d-175">Ponieważ w moim przypadku hello jar znajduje się w folderze C:\apps\dist\hive-0.13.x\bin hello, można bezpośrednio dodać jar hello o nazwie hello, jak pokazano:</span><span class="sxs-lookup"><span data-stu-id="2189d-175">Since in my case, hello jar is in hello C:\apps\dist\hive-0.13.x\bin folder, I can directly add hello jar with hello name as shown:</span></span>

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![Dodanie JAR tooyour projektu][image-hdi-hivejson-addjar]

<span data-ttu-id="2189d-177">Teraz wszystko jest gotowe toouse hello SerDe toorun zapytań dotyczących dokumentów JSON hello.</span><span class="sxs-lookup"><span data-stu-id="2189d-177">Now, you are ready toouse hello SerDe toorun queries against hello JSON document.</span></span>

<span data-ttu-id="2189d-178">Po instrukcji Hello tworzy tabelę z określonego schematu:</span><span class="sxs-lookup"><span data-stu-id="2189d-178">hello following statement creates a table with a defined schema:</span></span>

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

<span data-ttu-id="2189d-179">toolist hello imię i nazwisko student hello</span><span class="sxs-lookup"><span data-stu-id="2189d-179">toolist hello first name and last name of hello student</span></span>

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

<span data-ttu-id="2189d-180">Oto hello wyniku hello Hive konsoli.</span><span class="sxs-lookup"><span data-stu-id="2189d-180">Here is hello result from hello Hive console.</span></span>

![Zapytanie SerDe 1][image-hdi-hivejson-serde_query1]

<span data-ttu-id="2189d-182">Suma hello toocalculate wyniki hello dokumentu JSON</span><span class="sxs-lookup"><span data-stu-id="2189d-182">toocalculate hello sum of scores of hello JSON document</span></span>

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

<span data-ttu-id="2189d-183">Hello poprzedzających używa zapytania [rozłożyć penetracji widoku](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello tablicy wyników, dzięki czemu mogą być sumowane.</span><span class="sxs-lookup"><span data-stu-id="2189d-183">hello preceding query uses [lateral view explode](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView) UDF tooexpand hello array of scores so that they can be summed.</span></span>

<span data-ttu-id="2189d-184">Poniżej przedstawiono dane wyjściowe konsoli Hive hello hello.</span><span class="sxs-lookup"><span data-stu-id="2189d-184">Here is hello output from hello Hive console.</span></span>

![Zapytanie SerDe 2][image-hdi-hivejson-serde_query2]

<span data-ttu-id="2189d-186">toofind, które tematy danego uczniów ma przyznane więcej niż 80 punkty:</span><span class="sxs-lookup"><span data-stu-id="2189d-186">toofind which subjects a given student has scored more than 80 points:</span></span>

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

<span data-ttu-id="2189d-187">Hello poprzedniego zapytanie zwraca tablicę gałęzi, w odróżnieniu od get\_json\_obiektu, który zwraca wartość typu ciąg.</span><span class="sxs-lookup"><span data-stu-id="2189d-187">hello preceding query returns a Hive array unlike get\_json\_object, which returns a string.</span></span>

![Zapytanie SerDe 3][image-hdi-hivejson-serde_query3]

<span data-ttu-id="2189d-189">Jeśli chcesz, aby tooskil nieprawidłowo sformatowany kod JSON, a następnie jako hello wyjaśniono w [strona typu wiki](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) z tym SerDe można osiągnąć który wpisując hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="2189d-189">If you want tooskil malformed JSON, then as explained in hello [wiki page](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) of this SerDe you can achieve that by typing hello following code:</span></span>  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a><span data-ttu-id="2189d-190">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="2189d-190">Summary</span></span>
<span data-ttu-id="2189d-191">Podsumowując typ hello operatora JSON w gałęzi, którą można wybrać zależy od danego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="2189d-191">In conclusion, hello type of JSON operator in Hive that you choose depends on your scenario.</span></span> <span data-ttu-id="2189d-192">Jeśli proste dokument JSON i masz tylko jedną toolook pola — możesz wybrać get Hive UDF hello toouse\_json\_obiektu.</span><span class="sxs-lookup"><span data-stu-id="2189d-192">If you have a simple JSON document and you only have one field toolook up on – you can choose toouse hello Hive UDF get\_json\_object.</span></span> <span data-ttu-id="2189d-193">Jeśli masz więcej niż jednego klucza toolook, można użyć json_tuple.</span><span class="sxs-lookup"><span data-stu-id="2189d-193">If you have more than one key toolook up on, then you can use json_tuple.</span></span> <span data-ttu-id="2189d-194">Jeśli masz zagnieżdżonych dokumentu, należy używać hello JSON SerDe.</span><span class="sxs-lookup"><span data-stu-id="2189d-194">If you have a nested document, then you should use hello JSON SerDe.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2189d-195">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2189d-195">Next steps</span></span>

<span data-ttu-id="2189d-196">Aby uzyskać inne pokrewne artykuły zobacz</span><span class="sxs-lookup"><span data-stu-id="2189d-196">For other related articles, see</span></span>

* [<span data-ttu-id="2189d-197">Używanie Hive i HiveQL z usługą Hadoop w HDInsight tooanalyze przykładowego pliku Apache log4j</span><span class="sxs-lookup"><span data-stu-id="2189d-197">Use Hive and HiveQL with Hadoop in HDInsight tooanalyze a sample Apache log4j file</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="2189d-198">Analizowanie danych opóźnienie transmitowane przy użyciu usługi Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="2189d-198">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="2189d-199">Analizowanie danych Twitter przy użyciu Hive w usłudze HDInsight</span><span class="sxs-lookup"><span data-stu-id="2189d-199">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="2189d-200">Uruchomienie zadania usługi Hadoop przy użyciu bazy danych rozwiązania Cosmos Azure i usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="2189d-200">Run a Hadoop job using Azure Cosmos DB and HDInsight</span></span>](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

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
