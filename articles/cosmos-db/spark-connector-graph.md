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
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="07178-103">Azure DB rozwiązania Cosmos: Wykonywać analizy wykresu przy użyciu platformy Spark i Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="07178-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="07178-104">[Azure DB rozwiązania Cosmos](introduction.md) jest hello globalnie rozproszone i wiele modeli bazy danych usługi firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="07178-104">[Azure Cosmos DB](introduction.md) is hello globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="07178-105">Można tworzyć i kwerend dokumentu, klucza i wartości i wykres baz danych, które korzystają z możliwości globalnego dystrybucji i skalowania poziomego hello na podstawowe hello Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="07178-105">You can create and query document, key/value, and graph databases, all of which benefit from hello global-distribution and horizontal-scale capabilities at hello core of Azure Cosmos DB.</span></span> <span data-ttu-id="07178-106">Obciążenia graph (OLTP), które wykorzystują przetwarzania transakcji online obsługuje bazę danych systemu Azure rozwiązania Cosmos [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="07178-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="07178-107">[Platforma Spark](http://spark.apache.org/) jest Apache Software Foundation projektu, który koncentruje się na przetwarzanie danych ogólnego przeznaczenia przetwarzania analitycznego online (OLAP).</span><span class="sxs-lookup"><span data-stu-id="07178-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="07178-108">Platforma Spark zapewnia hybrydowych w pamięci/opartej na dysku rozproszonego przetwarzania danych modelu, który jest podobne toohello modelu MapReduce z Hadoop.</span><span class="sxs-lookup"><span data-stu-id="07178-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar toohello Hadoop MapReduce model.</span></span> <span data-ttu-id="07178-109">Apache Spark w chmurze hello można wdrożyć za pomocą [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="07178-109">You can deploy Apache Spark in hello cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="07178-110">Połączenie bazy danych Azure rozwiązania Cosmos z Spark, możesz wykonać obciążeń zarówno OLTP i OLAP używania Gremlin.</span><span class="sxs-lookup"><span data-stu-id="07178-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="07178-111">W tym artykule szybki start przedstawiono, jak toorun Gremlin zapytania względem bazy danych Azure rozwiązania Cosmos w klastrze usługi Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="07178-111">This quick-start article demonstrates how toorun Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07178-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="07178-112">Prerequisites</span></span>

<span data-ttu-id="07178-113">Przed uruchomieniem tego przykładu, musi mieć hello następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="07178-113">Before you can run this sample, you must have hello following prerequisites:</span></span>
* <span data-ttu-id="07178-114">Azure HDInsight Spark klastra 2.0</span><span class="sxs-lookup"><span data-stu-id="07178-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="07178-115">JDK 1.8 + (Jeśli nie masz JDK, uruchom `apt-get install default-jdk`.)</span><span class="sxs-lookup"><span data-stu-id="07178-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="07178-116">Maven (Jeśli nie masz Maven, uruchom `apt-get install maven`.)</span><span class="sxs-lookup"><span data-stu-id="07178-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="07178-117">Subskrypcja platformy Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="07178-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="07178-118">Aby uzyskać informacje na temat tooset zapasowej klastra Spark w usłudze HDInsight Azure, zobacz [klastrów inicjowania obsługi usługi HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="07178-118">For information about how tooset up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="07178-119">Tworzenie konta bazy danych Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="07178-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="07178-120">Najpierw utwórz konto bazy danych z interfejsu API programu Graph hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="07178-120">First, create a database account with hello Graph API by doing hello following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="07178-121">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="07178-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="07178-122">Pobierz Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="07178-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="07178-123">Pobierz Apache TinkerPop hello następujący:</span><span class="sxs-lookup"><span data-stu-id="07178-123">Get Apache TinkerPop by doing hello following:</span></span>

1. <span data-ttu-id="07178-124">Zdalne toohello węzła głównego klastra usługi HDInsight hello `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="07178-124">Remote toohello master node of hello HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="07178-125">Klonowanie kodu źródłowego TinkerPop3 hello, skompiluj go lokalnie i zainstalować ją w pamięci podręcznej tooMaven.</span><span class="sxs-lookup"><span data-stu-id="07178-125">Clone hello TinkerPop3 source code, build it locally, and install it tooMaven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="07178-126">Instalowanie wtyczki Spark Gremlin hello</span><span class="sxs-lookup"><span data-stu-id="07178-126">Install hello Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="07178-127">a.</span><span class="sxs-lookup"><span data-stu-id="07178-127">a.</span></span> <span data-ttu-id="07178-128">Hello instalacji dodatku plug-in hello jest obsługiwana przez moszcz.</span><span class="sxs-lookup"><span data-stu-id="07178-128">hello installation of hello plug-in is handled by Grape.</span></span> <span data-ttu-id="07178-129">Wypełnij hello repozytoriów informacji gronowego, aby mógł pobrać hello wtyczki i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="07178-129">Populate hello repositories information for Grape so it can download hello plug-in and its dependencies.</span></span> 

      <span data-ttu-id="07178-130">Utwórz plik konfiguracji winogronowego hello, jeśli nie jest obecny w `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="07178-130">Create hello grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="07178-131">Użyj hello następujące ustawienia:</span><span class="sxs-lookup"><span data-stu-id="07178-131">Use hello following settings:</span></span>

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

    <span data-ttu-id="07178-132">b.</span><span class="sxs-lookup"><span data-stu-id="07178-132">b.</span></span> <span data-ttu-id="07178-133">Uruchom konsolę Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="07178-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="07178-134">c.</span><span class="sxs-lookup"><span data-stu-id="07178-134">c.</span></span> <span data-ttu-id="07178-135">Instalowanie wtyczki Spark Gremlin hello z wersją 3.3.0-SNAPSHOT, które zostały utworzone w poprzednich krokach hello:</span><span class="sxs-lookup"><span data-stu-id="07178-135">Install hello Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in hello previous steps:</span></span>

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

4. <span data-ttu-id="07178-136">Sprawdź, czy toosee `Hadoop-Gremlin` jest aktywowany przy `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="07178-136">Check toosee whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="07178-137">Wyłącz ten dodatek, ponieważ jego może zakłócać hello Spark Gremlin wtyczki `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="07178-137">Disable this plug-in, because it could interfere with hello Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="07178-138">Przygotowanie TinkerPop3 zależności</span><span class="sxs-lookup"><span data-stu-id="07178-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="07178-139">Gdy TinkerPop3 jest utworzony w poprzednim kroku hello, proces hello również pobierane wszystkie zależności jar Spark i Hadoop w katalogu docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="07178-139">When you built TinkerPop3 in hello previous step, hello process also pulled all jar dependencies for Spark and Hadoop in hello target directory.</span></span> <span data-ttu-id="07178-140">Użyj słoików hello, które są wstępnie zainstalowane z HDI i ściągnąć dodatkowe zależności tylko niezbędne.</span><span class="sxs-lookup"><span data-stu-id="07178-140">Use hello jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="07178-141">Katalog docelowy Gremlin konsoli przejdź toohello na `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="07178-141">Go toohello Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="07178-142">Przenieś wszystkie słoików w obszarze `ext/` za`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="07178-142">Move all jars under `ext/` too`lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="07178-143">Usuń wszystkie jar biblioteki w obszarze `lib/` czy hello nie znajdują się one listy:</span><span class="sxs-lookup"><span data-stu-id="07178-143">Remove all jar libraries under `lib/` that are not in hello following list:</span></span>

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

## <a name="get-hello-azure-cosmos-db-spark-connector"></a><span data-ttu-id="07178-144">Pobierz hello łącznika usługi Azure Spark DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="07178-144">Get hello Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="07178-145">Pobierz łącznik usługi Azure Spark DB rozwiązania Cosmos hello `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` i rozwiązania Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` z [łącznika usługi Azure rozwiązania Cosmos DB Spark w usłudze GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="07178-145">Get hello Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="07178-146">Alternatywnie można utworzyć ją lokalnie.</span><span class="sxs-lookup"><span data-stu-id="07178-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="07178-147">Ponieważ hello najnowszą wersję Spark Gremlin został skompilowany z Spark 1.6.1 i nie jest zgodny z Spark pkt 2.0.2, który jest obecnie używana w łączniku Spark DB rozwiązania Cosmos Azure hello, możesz skompilować hello najnowsze TinkerPop3 kodu i ręcznie zainstalować słoików hello.</span><span class="sxs-lookup"><span data-stu-id="07178-147">Because hello latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in hello Azure Cosmos DB Spark connector, you can build hello latest TinkerPop3 code and install hello jars manually.</span></span> <span data-ttu-id="07178-148">Witaj, po:</span><span class="sxs-lookup"><span data-stu-id="07178-148">Do hello following:</span></span>

    <span data-ttu-id="07178-149">a.</span><span class="sxs-lookup"><span data-stu-id="07178-149">a.</span></span> <span data-ttu-id="07178-150">Klonowanie hello łącznika usługi Azure Spark DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="07178-150">Clone hello Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="07178-151">b.</span><span class="sxs-lookup"><span data-stu-id="07178-151">b.</span></span> <span data-ttu-id="07178-152">Tworzenie TinkerPop3 (już wykonane w poprzednich krokach).</span><span class="sxs-lookup"><span data-stu-id="07178-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="07178-153">Zainstaluj wszystkie słoików TinkerPop 3.3.0-SNAPSHOT lokalnie.</span><span class="sxs-lookup"><span data-stu-id="07178-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="07178-154">c.</span><span class="sxs-lookup"><span data-stu-id="07178-154">c.</span></span> <span data-ttu-id="07178-155">Aktualizacja `tinkerpop.version` `azure-documentdb-spark/pom.xml` zbyt`3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="07178-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` too`3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="07178-156">d.</span><span class="sxs-lookup"><span data-stu-id="07178-156">d.</span></span> <span data-ttu-id="07178-157">Kompiluj z Maven.</span><span class="sxs-lookup"><span data-stu-id="07178-157">Build with Maven.</span></span> <span data-ttu-id="07178-158">Witaj słoików potrzebne są umieszczane w `target` i `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="07178-158">hello needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="07178-159">Hello kopiowania wcześniej wymienionymi słoików tooa lokalnego katalogu ~ / azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="07178-159">Copy hello previously mentioned jars tooa local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-hello-dependencies-toohello-spark-worker-nodes"></a><span data-ttu-id="07178-160">Dystrybuuj węzłów procesu roboczego Spark hello zależności toohello</span><span class="sxs-lookup"><span data-stu-id="07178-160">Distribute hello dependencies toohello Spark worker nodes</span></span> 

1. <span data-ttu-id="07178-161">Ponieważ hello przekształcania danych wykresu jest zależna od TinkerPop3, musisz przeprowadzić dystrybucję hello związane z węzłami procesów roboczych Spark tooall zależności.</span><span class="sxs-lookup"><span data-stu-id="07178-161">Because hello transformation of graph data depends on TinkerPop3, you must distribute hello related dependencies tooall Spark worker nodes.</span></span>

2. <span data-ttu-id="07178-162">Hello kopiowania wymienione wcześniej Gremlin zależności, hello jar łącznika CosmosDB Spark i węzłów procesu roboczego zestawu Java SDK CosmosDB toohello następujący hello:</span><span class="sxs-lookup"><span data-stu-id="07178-162">Copy hello previously mentioned Gremlin dependencies, hello CosmosDB Spark connector jar, and CosmosDB Java SDK toohello worker nodes by doing hello following:</span></span>

    <span data-ttu-id="07178-163">a.</span><span class="sxs-lookup"><span data-stu-id="07178-163">a.</span></span> <span data-ttu-id="07178-164">Skopiuj wszystkie słoików hello do `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="07178-164">Copy all hello jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="07178-165">b.</span><span class="sxs-lookup"><span data-stu-id="07178-165">b.</span></span> <span data-ttu-id="07178-166">Pobierz hello listę wszystkich węzłów procesu roboczego Spark, które można znaleźć na pulpicie nawigacyjnym Ambari, w hello `Spark2 Clients` liście hello `Spark2` sekcji.</span><span class="sxs-lookup"><span data-stu-id="07178-166">Get hello list of all Spark worker nodes, which you can find on Ambari Dashboard, in hello `Spark2 Clients` list in hello `Spark2` section.</span></span>

    <span data-ttu-id="07178-167">c.</span><span class="sxs-lookup"><span data-stu-id="07178-167">c.</span></span> <span data-ttu-id="07178-168">Skopiuj ten katalog tooeach hello węzłów.</span><span class="sxs-lookup"><span data-stu-id="07178-168">Copy that directory tooeach of hello nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-hello-environment-variables"></a><span data-ttu-id="07178-169">Ustawianie zmiennych środowiskowych hello</span><span class="sxs-lookup"><span data-stu-id="07178-169">Set up hello environment variables</span></span>

1. <span data-ttu-id="07178-170">Znaleźć wersji HDP hello hello klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="07178-170">Find hello HDP version of hello Spark cluster.</span></span> <span data-ttu-id="07178-171">To nazwa katalogu hello w obszarze `/usr/hdp/` (na przykład 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="07178-171">It is hello directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="07178-172">Ustaw hdp.version dla wszystkich węzłów.</span><span class="sxs-lookup"><span data-stu-id="07178-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="07178-173">Na pulpicie nawigacyjnym Ambari, przejdź za**sekcji YARN** > **Configs** > **zaawansowane**, a następnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="07178-173">In Ambari Dashboard, go too**YARN section** > **Configs** > **Advanced**, and then do hello following:</span></span> 
 
    <span data-ttu-id="07178-174">a.</span><span class="sxs-lookup"><span data-stu-id="07178-174">a.</span></span> <span data-ttu-id="07178-175">W `Custom yarn-site`, Dodaj nową właściwość `hdp.version` o wartości hello wersja HDP hello na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="07178-175">In `Custom yarn-site`, add a new property `hdp.version` with hello value of hello HDP version on hello master node.</span></span> 
     
    <span data-ttu-id="07178-176">b.</span><span class="sxs-lookup"><span data-stu-id="07178-176">b.</span></span> <span data-ttu-id="07178-177">Zapisz konfiguracje hello.</span><span class="sxs-lookup"><span data-stu-id="07178-177">Save hello configurations.</span></span> <span data-ttu-id="07178-178">Wystąpiły ostrzeżenia, które można zignorować.</span><span class="sxs-lookup"><span data-stu-id="07178-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="07178-179">c.</span><span class="sxs-lookup"><span data-stu-id="07178-179">c.</span></span> <span data-ttu-id="07178-180">Ponownie uruchom usługi hello YARN oraz Oozie, jak wskazują hello ikony powiadomień.</span><span class="sxs-lookup"><span data-stu-id="07178-180">Restart hello YARN and Oozie services as hello notification icons indicate.</span></span>

3. <span data-ttu-id="07178-181">Zestaw hello następujące zmienne środowiskowe w węźle głównym hello (Zastąp wartości hello zależnie od potrzeb):</span><span class="sxs-lookup"><span data-stu-id="07178-181">Set hello following environment variables on hello master node (replace hello values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-hello-graph-configuration"></a><span data-ttu-id="07178-182">Przygotowanie hello wykres konfiguracji</span><span class="sxs-lookup"><span data-stu-id="07178-182">Prepare hello graph configuration</span></span>

1. <span data-ttu-id="07178-183">Utwórz plik konfiguracji zawierający hello parametry połączenia bazy danych rozwiązania Cosmos Azure Spark ustawienia i umieszcza je w `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="07178-183">Create a configuration file with hello Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

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

2. <span data-ttu-id="07178-184">Aktualizacja hello `spark.driver.extraClassPath` i `spark.executor.extraClassPath` tooinclude katalogu hello słoików hello, rozproszonych w poprzednim kroku hello, w tym przypadku `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="07178-184">Update hello `spark.driver.extraClassPath` and `spark.executor.extraClassPath` tooinclude hello directory of hello jars that you distributed in hello previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="07178-185">Podaj poniższe informacje dla bazy danych Azure rozwiązania Cosmos hello:</span><span class="sxs-lookup"><span data-stu-id="07178-185">Provide hello following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-hello-tinkerpop-graph-and-save-it-tooazure-cosmos-db"></a><span data-ttu-id="07178-186">Ładowanie hello TinkerPop wykresu, a następnie zapisz tooAzure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="07178-186">Load hello TinkerPop graph, and save it tooAzure Cosmos DB</span></span>
<span data-ttu-id="07178-187">toodemonstrate jak toopersist wykres do bazy danych z rozwiązania Cosmos platformy Azure, w tym przykładzie używa hello TinkerPop wstępnie zdefiniowane TinkerPop nowoczesnych wykresu.</span><span class="sxs-lookup"><span data-stu-id="07178-187">toodemonstrate how toopersist a graph into Azure Cosmos DB, this example uses hello TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="07178-188">Wykres Hello są przechowywane w formacie Kryo i jest dostępny w repozytorium TinkerPop hello.</span><span class="sxs-lookup"><span data-stu-id="07178-188">hello graph is stored in Kryo format, and it's provided in hello TinkerPop repository.</span></span>

1. <span data-ttu-id="07178-189">Ponieważ Gremlin działają w trybie YARN, należy udostępnić dane wykresu hello w hello systemu plików usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="07178-189">Because you are running Gremlin in YARN mode, you must make hello graph data available in hello Hadoop file system.</span></span> <span data-ttu-id="07178-190">Użyj następujących hello polecenia toomake katalogu i kopiowania pliku wykres lokalne powitania do niego.</span><span class="sxs-lookup"><span data-stu-id="07178-190">Use hello following commands toomake a directory and copy hello local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="07178-191">Tymczasowo zaktualizować hello `gremlin-spark.properties` pliku toouse `GryoInputFormat` tooread hello wykresu.</span><span class="sxs-lookup"><span data-stu-id="07178-191">Temporarily update hello `gremlin-spark.properties` file toouse `GryoInputFormat` tooread hello graph.</span></span> <span data-ttu-id="07178-192">Również wskazywać `inputLocation` jako katalog hello tworzenia, tak jak poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="07178-192">Also indicate `inputLocation` as hello directory you create, as in hello following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="07178-193">Uruchom konsolę Gremlin, a następnie utwórz powitania po obliczeń kroki toopersist toohello skonfigurowane bazy danych Azure rozwiązania Cosmos funkcji zbierania danych:</span><span class="sxs-lookup"><span data-stu-id="07178-193">Start Gremlin Console, and then create hello following computation steps toopersist data toohello configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="07178-194">a.</span><span class="sxs-lookup"><span data-stu-id="07178-194">a.</span></span> <span data-ttu-id="07178-195">Utwórz wykres hello `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="07178-195">Create hello graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="07178-196">b.</span><span class="sxs-lookup"><span data-stu-id="07178-196">b.</span></span> <span data-ttu-id="07178-197">Użyj SparkGraphComputer do zapisu `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="07178-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

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

4. <span data-ttu-id="07178-198">W Eksploratorze danych możesz sprawdzić, czy ten powitalne dane zostały utrwalone tooAzure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="07178-198">From Data Explorer, you can verify that hello data has been persisted tooAzure Cosmos DB.</span></span>

## <a name="load-hello-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="07178-199">Załadować hello wykres z bazy danych Azure rozwiązania Cosmos i uruchamianie zapytań Gremlin</span><span class="sxs-lookup"><span data-stu-id="07178-199">Load hello graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="07178-200">Wykres hello tooload, Edytuj `gremlin-spark.properties` tooset `graphReader` zbyt`DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="07178-200">tooload hello graph, edit `gremlin-spark.properties` tooset `graphReader` too`DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="07178-201">Wykres hello obciążenia, przenoszenie danych hello, a następnie uruchom zapytania Gremlin z nim hello następujący:</span><span class="sxs-lookup"><span data-stu-id="07178-201">Load hello graph, traverse hello data, and run Gremlin queries with it by doing hello following:</span></span>

    <span data-ttu-id="07178-202">a.</span><span class="sxs-lookup"><span data-stu-id="07178-202">a.</span></span> <span data-ttu-id="07178-203">Uruchom hello konsoli Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="07178-203">Start hello Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="07178-204">b.</span><span class="sxs-lookup"><span data-stu-id="07178-204">b.</span></span> <span data-ttu-id="07178-205">Utwórz wykres hello z konfiguracją hello `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="07178-205">Create hello graph with hello configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="07178-206">c.</span><span class="sxs-lookup"><span data-stu-id="07178-206">c.</span></span> <span data-ttu-id="07178-207">Utwórz przechodzenie wykres z SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="07178-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="07178-208">d.</span><span class="sxs-lookup"><span data-stu-id="07178-208">d.</span></span> <span data-ttu-id="07178-209">Uruchom powitania po Gremlin wykres zapytania:</span><span class="sxs-lookup"><span data-stu-id="07178-209">Run hello following Gremlin graph queries:</span></span>

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
> <span data-ttu-id="07178-210">toosee bardziej szczegółowe rejestrowanie, Ustaw poziom dziennika hello w `conf/log4j-console.properties` tooa pełniejsze poziom.</span><span class="sxs-lookup"><span data-stu-id="07178-210">toosee more detailed logging, set hello log level in `conf/log4j-console.properties` tooa more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="07178-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07178-211">Next steps</span></span>

<span data-ttu-id="07178-212">W tym artykule szybki start kiedy znasz już jak toowork z wykresach przez połączenie bazy danych Azure rozwiązania Cosmos i Spark.</span><span class="sxs-lookup"><span data-stu-id="07178-212">In this quick-start article, you've learned how toowork with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
