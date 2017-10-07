---
title: "Azure DB rozwiązania Cosmos: Wykonywać analizy wykresu przy użyciu platformy Spark i Apache TinkerPop Gremlin | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera instrukcje dotyczące konfigurowania i uruchamiania wykres analizy i równolegle obliczeń w usłudze Azure DB rozwiązania Cosmos z platformy Spark i TinkerPop SparkGraphComputer."
services: cosmosdb
documentationcenter: 
author: khdang
manager: shireest
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: gremlin
ms.topic: article
ms.date: 06/05/2017
ms.author: khdang
ms.openlocfilehash: 0be5c9b12cdba4a428c809d00e1e68785a9ec1ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a>Azure DB rozwiązania Cosmos: Wykonywać analizy wykresu przy użyciu platformy Spark i Apache TinkerPop Gremlin

[Azure DB rozwiązania Cosmos](introduction.md) jest hello globalnie rozproszone i wiele modeli bazy danych usługi firmy Microsoft. Można tworzyć i kwerend dokumentu, klucza i wartości i wykres baz danych, które korzystają z możliwości globalnego dystrybucji i skalowania poziomego hello na podstawowe hello Azure DB rozwiązania Cosmos. Obciążenia graph (OLTP), które wykorzystują przetwarzania transakcji online obsługuje bazę danych systemu Azure rozwiązania Cosmos [Apache TinkerPop Gremlin](graph-introduction.md).

[Platforma Spark](http://spark.apache.org/) jest Apache Software Foundation projektu, który koncentruje się na przetwarzanie danych ogólnego przeznaczenia przetwarzania analitycznego online (OLAP). Platforma Spark zapewnia hybrydowych w pamięci/opartej na dysku rozproszonego przetwarzania danych modelu, który jest podobne toohello modelu MapReduce z Hadoop. Apache Spark w chmurze hello można wdrożyć za pomocą [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Połączenie bazy danych Azure rozwiązania Cosmos z Spark, możesz wykonać obciążeń zarówno OLTP i OLAP używania Gremlin. W tym artykule szybki start przedstawiono, jak toorun Gremlin zapytania względem bazy danych Azure rozwiązania Cosmos w klastrze usługi Azure HDInsight Spark.

## <a name="prerequisites"></a>Wymagania wstępne

Przed uruchomieniem tego przykładu, musi mieć hello następujące wymagania wstępne:
* Azure HDInsight Spark klastra 2.0
* JDK 1.8 + (Jeśli nie masz JDK, uruchom `apt-get install default-jdk`.)
* Maven (Jeśli nie masz Maven, uruchom `apt-get install maven`.)
* Subskrypcja platformy Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])

Aby uzyskać informacje na temat tooset zapasowej klastra Spark w usłudze HDInsight Azure, zobacz [klastrów inicjowania obsługi usługi HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

## <a name="create-an-azure-cosmos-db-database-account"></a>Tworzenie konta bazy danych Azure DB rozwiązania Cosmos

Najpierw utwórz konto bazy danych z interfejsu API programu Graph hello hello następujący:

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Dodawanie kolekcji

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a>Pobierz Apache TinkerPop

Pobierz Apache TinkerPop hello następujący:

1. Zdalne toohello węzła głównego klastra usługi HDInsight hello `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.

2. Klonowanie kodu źródłowego TinkerPop3 hello, skompiluj go lokalnie i zainstalować ją w pamięci podręcznej tooMaven.

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. Instalowanie wtyczki Spark Gremlin hello 

    a. Hello instalacji dodatku plug-in hello jest obsługiwana przez moszcz. Wypełnij hello repozytoriów informacji gronowego, aby mógł pobrać hello wtyczki i jego zależności. 

      Utwórz plik konfiguracji winogronowego hello, jeśli nie jest obecny w `~/.groovy/grapeConfig.xml`. Użyj hello następujące ustawienia:

    ```xml
    <ivysettings>
    <settings defaultResolver="downloadGrapes"/>
    <resolvers>
        <chain name="downloadGrapes">
        <filesystem name="cachedGrapes">
            <ivy pattern="${user.home}/.groovy/grapes/[organisation]/[module]/ivy-[revision].xml"/>
            <artifact pattern="${user.home}/.groovy/grapes/[organisation]/[module]/[type]s/[artifact]-[revision].[ext]"/>
        </filesystem>
        <ibiblio name="codehaus" root="http://repository.codehaus.org/" m2compatible="true"/>
        <ibiblio name="central" root="http://central.maven.org/maven2/" m2compatible="true"/>
        <ibiblio name="jitpack" root="https://jitpack.io" m2compatible="true"/>
        <ibiblio name="java.net2" root="http://download.java.net/maven/2/" m2compatible="true"/>
        <ibiblio name="apache-snapshots" root="http://repository.apache.org/snapshots/" m2compatible="true"/>
        <ibiblio name="local" root="file:${user.home}/.m2/repository/" m2compatible="true"/>
        </chain>
    </resolvers>
    </ivysettings>
    ``` 

    b. Uruchom konsolę Gremlin `bin/gremlin.sh`.
        
    c. Instalowanie wtyczki Spark Gremlin hello z wersją 3.3.0-SNAPSHOT, które zostały utworzone w poprzednich krokach hello:

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart hello console toouse [tinkerpop.spark]
    gremlin> :q
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :plugin use tinkerpop.spark
    ==>tinkerpop.spark activated
    ```

4. Sprawdź, czy toosee `Hadoop-Gremlin` jest aktywowany przy `:plugin list`. Wyłącz ten dodatek, ponieważ jego może zakłócać hello Spark Gremlin wtyczki `:plugin unuse tinkerpop.hadoop`.

## <a name="prepare-tinkerpop3-dependencies"></a>Przygotowanie TinkerPop3 zależności

Gdy TinkerPop3 jest utworzony w poprzednim kroku hello, proces hello również pobierane wszystkie zależności jar Spark i Hadoop w katalogu docelowym hello. Użyj słoików hello, które są wstępnie zainstalowane z HDI i ściągnąć dodatkowe zależności tylko niezbędne.

1. Katalog docelowy Gremlin konsoli przejdź toohello na `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`. 

2. Przenieś wszystkie słoików w obszarze `ext/` za`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.

3. Usuń wszystkie jar biblioteki w obszarze `lib/` czy hello nie znajdują się one listy:

    ```bash
    # TinkerPop3
    gremlin-console-3.3.0-SNAPSHOT.jar
    gremlin-core-3.3.0-SNAPSHOT.jar       
    gremlin-groovy-3.3.0-SNAPSHOT.jar     
    gremlin-shaded-3.3.0-SNAPSHOT.jar     
    hadoop-gremlin-3.3.0-SNAPSHOT.jar     
    spark-gremlin-3.3.0-SNAPSHOT.jar      
    tinkergraph-gremlin-3.3.0-SNAPSHOT.jar

    # Gremlin depedencies
    asm-3.2.jar                                
    avro-1.7.4.jar                             
    caffeine-2.3.1.jar                         
    cglib-2.2.1-v20090111.jar                  
    gbench-0.4.3-groovy-2.4.jar                
    gprof-0.3.1-groovy-2.4.jar                 
    groovy-2.4.9-indy.jar                      
    groovy-2.4.9.jar                           
    groovy-console-2.4.9.jar                   
    groovy-groovysh-2.4.9-indy.jar             
    groovy-json-2.4.9-indy.jar                 
    groovy-jsr223-2.4.9-indy.jar               
    groovy-sql-2.4.9-indy.jar                  
    groovy-swing-2.4.9.jar                     
    groovy-templates-2.4.9.jar                 
    groovy-xml-2.4.9.jar                       
    hadoop-yarn-server-nodemanager-2.7.2.jar   
    hppc-0.7.1.jar                             
    javatuples-1.2.jar                         
    jaxb-impl-2.2.3-1.jar                      
    jbcrypt-0.4.jar                            
    jcabi-log-0.14.jar                         
    jcabi-manifests-1.1.jar                    
    jersey-core-1.9.jar                        
    jersey-guice-1.9.jar                       
    jersey-json-1.9.jar                        
    jettison-1.1.jar                           
    scalatest_2.11-2.2.6.jar                   
    servlet-api-2.5.jar                        
    snakeyaml-1.15.jar                         
    unused-1.0.0.jar                           
    xml-apis-1.3.04.jar                        
    ```

## <a name="get-hello-azure-cosmos-db-spark-connector"></a>Pobierz hello łącznika usługi Azure Spark DB rozwiązania Cosmos

1. Pobierz łącznik usługi Azure Spark DB rozwiązania Cosmos hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` i rozwiązania Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` z [łącznika usługi Azure rozwiązania Cosmos DB Spark w usłudze GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).

2. Alternatywnie można utworzyć ją lokalnie. Ponieważ hello najnowszą wersję Spark Gremlin został skompilowany z Spark 1.6.1 i nie jest zgodny z Spark pkt 2.0.2, który jest obecnie używana w łączniku Spark DB rozwiązania Cosmos Azure hello, możesz skompilować hello najnowsze TinkerPop3 kodu i ręcznie zainstalować słoików hello. Witaj, po:

    a. Klonowanie hello łącznika usługi Azure Spark DB rozwiązania Cosmos.

    b. Tworzenie TinkerPop3 (już wykonane w poprzednich krokach). Zainstaluj wszystkie słoików TinkerPop 3.3.0-SNAPSHOT lokalnie.

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    c. Aktualizacja `tinkerpop.version` `azure-documentdb-spark/pom.xml` zbyt`3.3.0-SNAPSHOT`.
    
    d. Kompiluj z Maven. Witaj słoików potrzebne są umieszczane w `target` i `target/alternateLocation`.

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. Hello kopiowania wcześniej wymienionymi słoików tooa lokalnego katalogu ~ / azure-documentdb-spark:

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a>Dystrybuuj węzłów procesu roboczego Spark hello zależności toohello 

1. Ponieważ hello przekształcania danych wykresu jest zależna od TinkerPop3, musisz przeprowadzić dystrybucję hello związane z węzłami procesów roboczych Spark tooall zależności.

2. Hello kopiowania wymienione wcześniej Gremlin zależności, hello jar łącznika CosmosDB Spark i węzłów procesu roboczego zestawu Java SDK CosmosDB toohello następujący hello:

    a. Skopiuj wszystkie słoików hello do `~/azure-documentdb-spark`.

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    b. Pobierz hello listę wszystkich węzłów procesu roboczego Spark, które można znaleźć na pulpicie nawigacyjnym Ambari, w hello `Spark2 Clients` liście hello `Spark2` sekcji.

    c. Skopiuj ten katalog tooeach hello węzłów.

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a>Ustawianie zmiennych środowiskowych hello

1. Znaleźć wersji HDP hello hello klastra Spark. To nazwa katalogu hello w obszarze `/usr/hdp/` (na przykład 2.5.4.2-7).

2. Ustaw hdp.version dla wszystkich węzłów. Na pulpicie nawigacyjnym Ambari, przejdź za**sekcji YARN** > **Configs** > **zaawansowane**, a następnie hello następujące: 
 
    a. W `Custom yarn-site`, Dodaj nową właściwość `hdp.version` o wartości hello wersja HDP hello na powitania węzła głównego. 
     
    b. Zapisz konfiguracje hello. Wystąpiły ostrzeżenia, które można zignorować. 
     
    c. Ponownie uruchom usługi hello YARN oraz Oozie, jak wskazują hello ikony powiadomień.

3. Zestaw hello następujące zmienne środowiskowe w węźle głównym hello (Zastąp wartości hello zależnie od potrzeb):

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a>Przygotowanie hello wykres konfiguracji

1. Utwórz plik konfiguracji zawierający hello parametry połączenia bazy danych rozwiązania Cosmos Azure Spark ustawienia i umieszcza je w `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.

    ```
    gremlin.graph=org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph
    gremlin.hadoop.jarsInDistributedCache=true
    gremlin.hadoop.defaultGraphComputer=org.apache.tinkerpop.gremlin.spark.process.computer.SparkGraphComputer

    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    gremlin.hadoop.graphWriter=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBOutputRDD

    ####################################
    # SparkGraphComputer Configuration #
    ####################################
    spark.master=yarn
    spark.executor.memory=3g
    spark.executor.instances=6
    spark.serializer=org.apache.spark.serializer.KryoSerializer
    spark.kryo.registrator=org.apache.tinkerpop.gremlin.spark.structure.io.gryo.GryoRegistrator
    gremlin.spark.persistContext=true

    # Classpath for hello driver and executors
    spark.driver.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    spark.executor.extraClassPath=/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    
    ######################################
    # DocumentDB Spark connector         #
    ######################################
    spark.documentdb.connectionMode=Gateway
    spark.documentdb.schema_samplingratio=1.0
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    spark.documentdb.preferredRegions=FILLIN
    ```

2. Aktualizacja hello `spark.driver.extraClassPath` i `spark.executor.extraClassPath` tooinclude katalogu hello słoików hello, rozproszonych w poprzednim kroku hello, w tym przypadku `/home/sshuser/azure-documentdb-spark/*`.

3. Podaj poniższe informacje dla bazy danych Azure rozwiązania Cosmos hello:

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a>Ładowanie hello TinkerPop wykresu, a następnie zapisz tooAzure DB rozwiązania Cosmos
toodemonstrate jak toopersist wykres do bazy danych z rozwiązania Cosmos platformy Azure, w tym przykładzie używa hello TinkerPop wstępnie zdefiniowane TinkerPop nowoczesnych wykresu. Wykres Hello są przechowywane w formacie Kryo i jest dostępny w repozytorium TinkerPop hello.

1. Ponieważ Gremlin działają w trybie YARN, należy udostępnić dane wykresu hello w hello systemu plików usługi Hadoop. Użyj następujących hello polecenia toomake katalogu i kopiowania pliku wykres lokalne powitania do niego. 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. Tymczasowo zaktualizować hello `gremlin-spark.properties` pliku toouse `GryoInputFormat` tooread hello wykresu. Również wskazywać `inputLocation` jako katalog hello tworzenia, tak jak poniżej hello:

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. Uruchom konsolę Gremlin, a następnie utwórz powitania po obliczeń kroki toopersist toohello skonfigurowane bazy danych Azure rozwiązania Cosmos funkcji zbierania danych:  

    a. Utwórz wykres hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.

    b. Użyj SparkGraphComputer do zapisu `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[gryoinputformat->documentdboutputrdd]
    gremlin> hg = graph.
                compute(SparkGraphComputer.class).
                result(GraphComputer.ResultGraph.NEW).
                persist(GraphComputer.Persist.EDGES).
                program(TraversalVertexProgram.build().
                    traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)), "gremlin-groovy", "g.V()").
                    create(graph)).
                submit().
                get() 
    ==>result[hadoopgraph[documentdbinputrdd->documentdboutputrdd],memory[size:1]]
    ```

4. W Eksploratorze danych możesz sprawdzić, czy ten powitalne dane zostały utrwalone tooAzure DB rozwiązania Cosmos.

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a>Załadować hello wykres z bazy danych Azure rozwiązania Cosmos i uruchamianie zapytań Gremlin

1. Wykres hello tooload, Edytuj `gremlin-spark.properties` tooset `graphReader` zbyt`DocumentDBInputRDD`:

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. Wykres hello obciążenia, przenoszenie danych hello, a następnie uruchom zapytania Gremlin z nim hello następujący:

    a. Uruchom hello konsoli Gremlin `bin/gremlin.sh`.

    b. Utwórz wykres hello z konfiguracją hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.

    c. Utwórz przechodzenie wykres z SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.

    d. Uruchom powitania po Gremlin wykres zapytania:

    ```bash
    gremlin> graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")
    ==>hadoopgraph[documentdbinputrdd->documentdboutputrdd]
    gremlin> g = graph.traversal().withComputer(SparkGraphComputer)
    ==>graphtraversalsource[hadoopgraph[documentdbinputrdd->documentdboutputrdd], sparkgraphcomputer]
    gremlin> g.V().count()
    ==>6
    gremlin> g.E().count()
    ==>6
    gremlin> g.V(1).out().values('name')
    ==>josh
    ==>vadas
    ==>lop
    gremlin> g.V().hasLabel('person').coalesce(values('nickname'), values('name'))
    ==>josh
    ==>peter
    ==>vadas
    ==>marko
    gremlin> g.V().hasLabel('person').
            choose(values('name')).
                option('marko', values('age')).
                option('josh', values('name')).
                option('vadas', valueMap()).
                option('peter', label())
    ==>josh
    ==>person
    ==>[name:[vadas],age:[27]]
    ==>29
    ```

> [!NOTE]
> toosee bardziej szczegółowe rejestrowanie, Ustaw poziom dziennika hello w `conf/log4j-console.properties` tooa pełniejsze poziom.
>

## <a name="next-steps"></a>Następne kroki

W tym artykule szybki start kiedy znasz już jak toowork z wykresach przez połączenie bazy danych Azure rozwiązania Cosmos i Spark.

> [!div class="nextstepaction"]
