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
ms.openlocfilehash: 27c4d945e418b130c68cfde845571eb93658101e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-perform-graph-analytics-by-using-spark-and-apache-tinkerpop-gremlin"></a><span data-ttu-id="eedd1-103">Azure DB rozwiązania Cosmos: Wykonywać analizy wykresu przy użyciu platformy Spark i Apache TinkerPop Gremlin</span><span class="sxs-lookup"><span data-stu-id="eedd1-103">Azure Cosmos DB: Perform graph analytics by using Spark and Apache TinkerPop Gremlin</span></span>

<span data-ttu-id="eedd1-104">[Azure DB rozwiązania Cosmos](introduction.md) globalnie rozproszone i wiele modeli bazy danych usługi firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eedd1-104">[Azure Cosmos DB](introduction.md) is the globally distributed, multi-model database service from Microsoft.</span></span> <span data-ttu-id="eedd1-105">Można tworzyć i kwerend dokumentu, klucza i wartości i wykres baz danych, które korzystają z możliwości globalnego dystrybucji i skalowania poziomego Fundament bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eedd1-105">You can create and query document, key/value, and graph databases, all of which benefit from the global-distribution and horizontal-scale capabilities at the core of Azure Cosmos DB.</span></span> <span data-ttu-id="eedd1-106">Obciążenia graph (OLTP), które wykorzystują przetwarzania transakcji online obsługuje bazę danych systemu Azure rozwiązania Cosmos [Apache TinkerPop Gremlin](graph-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eedd1-106">Azure Cosmos DB supports online transaction processing (OLTP) graph workloads that use [Apache TinkerPop Gremlin](graph-introduction.md).</span></span>

<span data-ttu-id="eedd1-107">[Platforma Spark](http://spark.apache.org/) jest Apache Software Foundation projektu, który koncentruje się na przetwarzanie danych ogólnego przeznaczenia przetwarzania analitycznego online (OLAP).</span><span class="sxs-lookup"><span data-stu-id="eedd1-107">[Spark](http://spark.apache.org/) is an Apache Software Foundation project that's focused on general-purpose online analytical processing (OLAP) data processing.</span></span> <span data-ttu-id="eedd1-108">Spark zapewnia hybrydowych w pamięci/opartej na dysku rozproszonego przetwarzania danych model podobny do modelu MapReduce z Hadoop.</span><span class="sxs-lookup"><span data-stu-id="eedd1-108">Spark provides a hybrid in-memory/disk-based distributed computing model that is similar to the Hadoop MapReduce model.</span></span> <span data-ttu-id="eedd1-109">Apache Spark w chmurze można wdrożyć za pomocą [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="eedd1-109">You can deploy Apache Spark in the cloud by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="eedd1-110">Połączenie bazy danych Azure rozwiązania Cosmos z Spark, możesz wykonać obciążeń zarówno OLTP i OLAP używania Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eedd1-110">By combining Azure Cosmos DB and Spark, you can perform both OLTP and OLAP workloads when you use Gremlin.</span></span> <span data-ttu-id="eedd1-111">W tym artykule szybki start przedstawiono sposób wykonywania kwerend Gremlin do bazy danych Azure rozwiązania Cosmos w klastrze usługi Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="eedd1-111">This quick-start article demonstrates how to run Gremlin queries against Azure Cosmos DB on an Azure HDInsight Spark cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eedd1-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eedd1-112">Prerequisites</span></span>

<span data-ttu-id="eedd1-113">Przed uruchomieniem tego przykładu muszą być spełnione następujące wymagania wstępne:</span><span class="sxs-lookup"><span data-stu-id="eedd1-113">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="eedd1-114">Azure HDInsight Spark klastra 2.0</span><span class="sxs-lookup"><span data-stu-id="eedd1-114">Azure HDInsight Spark cluster 2.0</span></span>
* <span data-ttu-id="eedd1-115">JDK 1.8 + (Jeśli nie masz JDK, uruchom `apt-get install default-jdk`.)</span><span class="sxs-lookup"><span data-stu-id="eedd1-115">JDK 1.8+ (If you don't have JDK, run `apt-get install default-jdk`.)</span></span>
* <span data-ttu-id="eedd1-116">Maven (Jeśli nie masz Maven, uruchom `apt-get install maven`.)</span><span class="sxs-lookup"><span data-stu-id="eedd1-116">Maven (If you don't have Maven, run `apt-get install maven`.)</span></span>
* <span data-ttu-id="eedd1-117">Subskrypcja platformy Azure ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span><span class="sxs-lookup"><span data-stu-id="eedd1-117">An Azure subscription ([!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)])</span></span>

<span data-ttu-id="eedd1-118">Aby uzyskać informacje o sposobie konfigurowania klastra Spark w usłudze HDInsight Azure, zobacz [klastrów inicjowania obsługi usługi HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="eedd1-118">For information about how to set up an Azure HDInsight Spark cluster, see [Provisioning HDInsight clusters](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="create-an-azure-cosmos-db-database-account"></a><span data-ttu-id="eedd1-119">Tworzenie konta bazy danych Azure DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="eedd1-119">Create an Azure Cosmos DB database account</span></span>

<span data-ttu-id="eedd1-120">Najpierw utwórz konto bazy danych z interfejsu API programu Graph, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eedd1-120">First, create a database account with the Graph API by doing the following:</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="eedd1-121">Dodawanie kolekcji</span><span class="sxs-lookup"><span data-stu-id="eedd1-121">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="get-apache-tinkerpop"></a><span data-ttu-id="eedd1-122">Pobierz Apache TinkerPop</span><span class="sxs-lookup"><span data-stu-id="eedd1-122">Get Apache TinkerPop</span></span>

<span data-ttu-id="eedd1-123">Pobierz Apache TinkerPop, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eedd1-123">Get Apache TinkerPop by doing the following:</span></span>

1. <span data-ttu-id="eedd1-124">Zdalny do węzła głównego klastra usługi HDInsight `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-124">Remote to the master node of the HDInsight cluster `ssh tinkerpop3-cosmosdb-demo-ssh.azurehdinsight.net`.</span></span>

2. <span data-ttu-id="eedd1-125">Klonowanie kodu źródłowego TinkerPop3, skompiluj go lokalnie i zainstaluj go w pamięci podręcznej Maven.</span><span class="sxs-lookup"><span data-stu-id="eedd1-125">Clone the TinkerPop3 source code, build it locally, and install it to Maven cache.</span></span>

    ```bash
    git clone https://github.com/apache/tinkerpop.git
    cd tinkerpop
    mvn clean install
    ```

3. <span data-ttu-id="eedd1-126">Zainstaluj Spark Gremlin wtyczki</span><span class="sxs-lookup"><span data-stu-id="eedd1-126">Install the Spark-Gremlin plug-in</span></span> 

    <span data-ttu-id="eedd1-127">a.</span><span class="sxs-lookup"><span data-stu-id="eedd1-127">a.</span></span> <span data-ttu-id="eedd1-128">Instalacja dodatku jest obsługiwany przez moszcz.</span><span class="sxs-lookup"><span data-stu-id="eedd1-128">The installation of the plug-in is handled by Grape.</span></span> <span data-ttu-id="eedd1-129">Wypełnij informacje repozytoria gronowego, można pobrać wtyczki i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="eedd1-129">Populate the repositories information for Grape so it can download the plug-in and its dependencies.</span></span> 

      <span data-ttu-id="eedd1-130">Utwórz plik konfiguracji winogronowego, jeśli nie jest obecny w `~/.groovy/grapeConfig.xml`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-130">Create the grape configuration file if it's not present at `~/.groovy/grapeConfig.xml`.</span></span> <span data-ttu-id="eedd1-131">Użyj następujących ustawień:</span><span class="sxs-lookup"><span data-stu-id="eedd1-131">Use the following settings:</span></span>

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

    <span data-ttu-id="eedd1-132">b.</span><span class="sxs-lookup"><span data-stu-id="eedd1-132">b.</span></span> <span data-ttu-id="eedd1-133">Uruchom konsolę Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-133">Start Gremlin console `bin/gremlin.sh`.</span></span>
        
    <span data-ttu-id="eedd1-134">c.</span><span class="sxs-lookup"><span data-stu-id="eedd1-134">c.</span></span> <span data-ttu-id="eedd1-135">Zainstaluj Spark Gremlin wtyczki z wersją 3.3.0-SNAPSHOT, które zostały utworzone w poprzednich krokach:</span><span class="sxs-lookup"><span data-stu-id="eedd1-135">Install the Spark-Gremlin plug-in with version 3.3.0-SNAPSHOT, which you built in the previous steps:</span></span>

    ```bash
    $ bin/gremlin.sh

            \,,,/
            (o o)
    -----oOOo-(3)-oOOo-----
    plugin activated: tinkerpop.server
    plugin activated: tinkerpop.utilities
    plugin activated: tinkerpop.tinkergraph
    gremlin> :install org.apache.tinkerpop spark-gremlin 3.3.0-SNAPSHOT
    ==>loaded: [org.apache.tinkerpop, spark-gremlin, 3.3.0-SNAPSHOT] - restart the console to use [tinkerpop.spark]
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

4. <span data-ttu-id="eedd1-136">Sprawdź, czy `Hadoop-Gremlin` jest aktywowany przy `:plugin list`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-136">Check to see whether `Hadoop-Gremlin` is activated with `:plugin list`.</span></span> <span data-ttu-id="eedd1-137">Wyłącz ten dodatek, ponieważ może zakłócać Spark Gremlin wtyczki `:plugin unuse tinkerpop.hadoop`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-137">Disable this plug-in, because it could interfere with the Spark-Gremlin plug-in `:plugin unuse tinkerpop.hadoop`.</span></span>

## <a name="prepare-tinkerpop3-dependencies"></a><span data-ttu-id="eedd1-138">Przygotowanie TinkerPop3 zależności</span><span class="sxs-lookup"><span data-stu-id="eedd1-138">Prepare TinkerPop3 dependencies</span></span>

<span data-ttu-id="eedd1-139">Gdy TinkerPop3 jest utworzony w poprzednim kroku, proces również pobierane wszystkie zależności jar dla platformy Spark i Hadoop w katalogu docelowym.</span><span class="sxs-lookup"><span data-stu-id="eedd1-139">When you built TinkerPop3 in the previous step, the process also pulled all jar dependencies for Spark and Hadoop in the target directory.</span></span> <span data-ttu-id="eedd1-140">Użyj słoików, które są wstępnie zainstalowane z HDI i ściągnąć dodatkowe zależności tylko niezbędne.</span><span class="sxs-lookup"><span data-stu-id="eedd1-140">Use the jars that are pre-installed with HDI, and pull in additional dependencies only as necessary.</span></span>

1. <span data-ttu-id="eedd1-141">Przejdź do katalogu docelowego konsoli Gremlin na `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-141">Go to the Gremlin Console target directory at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone`.</span></span> 

2. <span data-ttu-id="eedd1-142">Przenieś wszystkie słoików w obszarze `ext/` do `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-142">Move all jars under `ext/` to `lib/`: `find ext/ -name '*.jar' -exec mv {} lib/ \;`.</span></span>

3. <span data-ttu-id="eedd1-143">Usuń wszystkie jar biblioteki w obszarze `lib/` nie znajdują się w następującej listy:</span><span class="sxs-lookup"><span data-stu-id="eedd1-143">Remove all jar libraries under `lib/` that are not in the following list:</span></span>

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

## <a name="get-the-azure-cosmos-db-spark-connector"></a><span data-ttu-id="eedd1-144">Pobierz łącznik usługi Azure Spark DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="eedd1-144">Get the Azure Cosmos DB Spark connector</span></span>

1. <span data-ttu-id="eedd1-145">Pobierz łącznik usługi Azure Spark DB rozwiązania Cosmos `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` i rozwiązania Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` z [łącznika usługi Azure rozwiązania Cosmos DB Spark w usłudze GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span><span class="sxs-lookup"><span data-stu-id="eedd1-145">Get the Azure Cosmos DB Spark connector `azure-documentdb-spark-0.0.3-SNAPSHOT.jar` and Cosmos DB Java SDK `azure-documentdb-1.10.0.jar` from [Azure Cosmos DB Spark Connector on GitHub](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark-0.0.3_2.0.2_2.11).</span></span>

2. <span data-ttu-id="eedd1-146">Alternatywnie można utworzyć ją lokalnie.</span><span class="sxs-lookup"><span data-stu-id="eedd1-146">Alternatively, you can build it locally.</span></span> <span data-ttu-id="eedd1-147">Ponieważ najnowsza wersja Spark Gremlin został skompilowany z Spark 1.6.1 i nie jest zgodny z Spark pkt 2.0.2, który jest obecnie używana w łączniku Spark DB rozwiązania Cosmos Azure, możesz skompilować kod TinkerPop3 najnowsze i ręcznie zainstalować słoików.</span><span class="sxs-lookup"><span data-stu-id="eedd1-147">Because the latest version of Spark-Gremlin was built with Spark 1.6.1 and is not compatible with Spark 2.0.2, which is currently used in the Azure Cosmos DB Spark connector, you can build the latest TinkerPop3 code and install the jars manually.</span></span> <span data-ttu-id="eedd1-148">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eedd1-148">Do the following:</span></span>

    <span data-ttu-id="eedd1-149">a.</span><span class="sxs-lookup"><span data-stu-id="eedd1-149">a.</span></span> <span data-ttu-id="eedd1-150">Klonowanie łącznika usługi Azure Spark DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eedd1-150">Clone the Azure Cosmos DB Spark connector.</span></span>

    <span data-ttu-id="eedd1-151">b.</span><span class="sxs-lookup"><span data-stu-id="eedd1-151">b.</span></span> <span data-ttu-id="eedd1-152">Tworzenie TinkerPop3 (już wykonane w poprzednich krokach).</span><span class="sxs-lookup"><span data-stu-id="eedd1-152">Build TinkerPop3 (already done in previous steps).</span></span> <span data-ttu-id="eedd1-153">Zainstaluj wszystkie słoików TinkerPop 3.3.0-SNAPSHOT lokalnie.</span><span class="sxs-lookup"><span data-stu-id="eedd1-153">Install all TinkerPop 3.3.0-SNAPSHOT jars locally.</span></span>

    ```bash
    mvn install:install-file -Dfile="gremlin-core-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-core -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar
    mvn install:install-file -Dfile="gremlin-groovy-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-groovy -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="gremlin-shaded-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=gremlin-shaded -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="hadoop-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=hadoop-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="spark-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=spark-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    mvn install:install-file -Dfile="tinkergraph-gremlin-3.3.0-SNAPSHOT.jar" -DgroupId=org.apache.tinkerpop -DartifactId=tinkergraph-gremlin -Dversion=3.3.0-SNAPSHOT -Dpackaging=jar`
    ```

    <span data-ttu-id="eedd1-154">c.</span><span class="sxs-lookup"><span data-stu-id="eedd1-154">c.</span></span> <span data-ttu-id="eedd1-155">Aktualizacja `tinkerpop.version` `azure-documentdb-spark/pom.xml` do `3.3.0-SNAPSHOT`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-155">Update `tinkerpop.version` `azure-documentdb-spark/pom.xml` to `3.3.0-SNAPSHOT`.</span></span>
    
    <span data-ttu-id="eedd1-156">d.</span><span class="sxs-lookup"><span data-stu-id="eedd1-156">d.</span></span> <span data-ttu-id="eedd1-157">Kompiluj z Maven.</span><span class="sxs-lookup"><span data-stu-id="eedd1-157">Build with Maven.</span></span> <span data-ttu-id="eedd1-158">Słoików potrzebne są umieszczane w `target` i `target/alternateLocation`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-158">The needed jars are placed in `target` and `target/alternateLocation`.</span></span>

    ```bash
    git clone https://github.com/Azure/azure-cosmosdb-spark.git
    cd azure-documentdb-spark
    mvn clean package
    ```

3. <span data-ttu-id="eedd1-159">Skopiuj słoików wymienione wcześniej w lokalnym katalogu na ~ / azure-documentdb-spark:</span><span class="sxs-lookup"><span data-stu-id="eedd1-159">Copy the previously mentioned jars to a local directory at ~/azure-documentdb-spark:</span></span>

    ```bash
    $ azure-documentdb-spark:
    mkdir ~/azure-documentdb-spark
    cp target/azure-documentdb-spark-0.0.3-SNAPSHOT.jar ~/azure-documentdb-spark
    cp target/alternateLocation/azure-documentdb-1.10.0.jar ~/azure-documentdb-spark
    ```

## <a name="distribute-the-dependencies-to-the-spark-worker-nodes"></a><span data-ttu-id="eedd1-160">Dystrybuuj zależności z węzłami procesu roboczego Spark</span><span class="sxs-lookup"><span data-stu-id="eedd1-160">Distribute the dependencies to the Spark worker nodes</span></span> 

1. <span data-ttu-id="eedd1-161">Ponieważ przekształcania danych wykresu jest zależna od TinkerPop3, musisz przeprowadzić dystrybucję powiązane zależności do wszystkich węzłów procesu roboczego platformy Spark.</span><span class="sxs-lookup"><span data-stu-id="eedd1-161">Because the transformation of graph data depends on TinkerPop3, you must distribute the related dependencies to all Spark worker nodes.</span></span>

2. <span data-ttu-id="eedd1-162">Skopiuj wymienione wcześniej zależności Gremlin, CosmosDB Spark jar łącznika i zestawu SDK Java CosmosDB do węzłów procesu roboczego w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="eedd1-162">Copy the previously mentioned Gremlin dependencies, the CosmosDB Spark connector jar, and CosmosDB Java SDK to the worker nodes by doing the following:</span></span>

    <span data-ttu-id="eedd1-163">a.</span><span class="sxs-lookup"><span data-stu-id="eedd1-163">a.</span></span> <span data-ttu-id="eedd1-164">Skopiuj wszystkie słoików do `~/azure-documentdb-spark`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-164">Copy all the jars into `~/azure-documentdb-spark`.</span></span>

    ```bash
    $ /home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone:
    cp lib/* ~/azure-documentdb-spark
    ```

    <span data-ttu-id="eedd1-165">b.</span><span class="sxs-lookup"><span data-stu-id="eedd1-165">b.</span></span> <span data-ttu-id="eedd1-166">Pobierz listę wszystkich węzłów procesu roboczego Spark, które można znaleźć na pulpicie nawigacyjnym Ambari, w `Spark2 Clients` na liście `Spark2` sekcji.</span><span class="sxs-lookup"><span data-stu-id="eedd1-166">Get the list of all Spark worker nodes, which you can find on Ambari Dashboard, in the `Spark2 Clients` list in the `Spark2` section.</span></span>

    <span data-ttu-id="eedd1-167">c.</span><span class="sxs-lookup"><span data-stu-id="eedd1-167">c.</span></span> <span data-ttu-id="eedd1-168">Kopiowanie katalogu do każdego z węzłów.</span><span class="sxs-lookup"><span data-stu-id="eedd1-168">Copy that directory to each of the nodes.</span></span>

    ```bash
    scp -r ~/azure-documentdb-spark sshuser@wn0-cosmos:/home/sshuser
    scp -r ~/azure-documentdb-spark sshuser@wn1-cosmos:/home/sshuser
    ...
    ```
    
## <a name="set-up-the-environment-variables"></a><span data-ttu-id="eedd1-169">Ustawianie zmiennych środowiskowych</span><span class="sxs-lookup"><span data-stu-id="eedd1-169">Set up the environment variables</span></span>

1. <span data-ttu-id="eedd1-170">Znajdź wersję HDP klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="eedd1-170">Find the HDP version of the Spark cluster.</span></span> <span data-ttu-id="eedd1-171">Jest to nazwa katalogu, w obszarze `/usr/hdp/` (na przykład 2.5.4.2-7).</span><span class="sxs-lookup"><span data-stu-id="eedd1-171">It is the directory name under `/usr/hdp/` (for example, 2.5.4.2-7).</span></span>

2. <span data-ttu-id="eedd1-172">Ustaw hdp.version dla wszystkich węzłów.</span><span class="sxs-lookup"><span data-stu-id="eedd1-172">Set hdp.version for all nodes.</span></span> <span data-ttu-id="eedd1-173">Na pulpicie nawigacyjnym Ambari, przejdź do **sekcji YARN** > **Configs** > **zaawansowane**, a następnie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eedd1-173">In Ambari Dashboard, go to **YARN section** > **Configs** > **Advanced**, and then do the following:</span></span> 
 
    <span data-ttu-id="eedd1-174">a.</span><span class="sxs-lookup"><span data-stu-id="eedd1-174">a.</span></span> <span data-ttu-id="eedd1-175">W `Custom yarn-site`, Dodaj nową właściwość `hdp.version` o wartości wersji HDP w węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="eedd1-175">In `Custom yarn-site`, add a new property `hdp.version` with the value of the HDP version on the master node.</span></span> 
     
    <span data-ttu-id="eedd1-176">b.</span><span class="sxs-lookup"><span data-stu-id="eedd1-176">b.</span></span> <span data-ttu-id="eedd1-177">Zapisz konfiguracje.</span><span class="sxs-lookup"><span data-stu-id="eedd1-177">Save the configurations.</span></span> <span data-ttu-id="eedd1-178">Wystąpiły ostrzeżenia, które można zignorować.</span><span class="sxs-lookup"><span data-stu-id="eedd1-178">There are warnings, which you can ignore.</span></span> 
     
    <span data-ttu-id="eedd1-179">c.</span><span class="sxs-lookup"><span data-stu-id="eedd1-179">c.</span></span> <span data-ttu-id="eedd1-180">Uruchom ponownie usługi YARN i Oozie, jak wskazują ikony powiadomień.</span><span class="sxs-lookup"><span data-stu-id="eedd1-180">Restart the YARN and Oozie services as the notification icons indicate.</span></span>

3. <span data-ttu-id="eedd1-181">Ustaw następujące zmienne środowiskowe w węźle głównym (Zastąp wartości zależnie od potrzeb):</span><span class="sxs-lookup"><span data-stu-id="eedd1-181">Set the following environment variables on the master node (replace the values as appropriate):</span></span>

    ```bash
    export HADOOP_GREMLIN_LIBS=/home/sshuser/tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/ext/spark-gremlin/lib
    export CLASSPATH=$CLASSPATH:$HADOOP_CONF_DIR:/usr/hdp/current/spark2-client/jars/*:/home/sshuser/azure-documentdb-spark/*
    export HDP_VERSION=2.5.4.2-7
    export HADOOP_HOME=${HADOOP_HOME:-/usr/hdp/current/hadoop-client}
    ```

## <a name="prepare-the-graph-configuration"></a><span data-ttu-id="eedd1-182">Przygotowanie konfiguracji wykresu</span><span class="sxs-lookup"><span data-stu-id="eedd1-182">Prepare the graph configuration</span></span>

1. <span data-ttu-id="eedd1-183">Utwórz plik konfiguracji z ustawieniami Spark i parametry połączenia bazy danych Azure rozwiązania Cosmos i umieszcza je w `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-183">Create a configuration file with the Azure Cosmos DB connection parameters and Spark settings, and put it at `tinkerpop/gremlin-console/target/apache-tinkerpop-gremlin-console-3.3.0-SNAPSHOT-standalone/conf/hadoop/gremlin-spark.properties`.</span></span>

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

    # Classpath for the driver and executors
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

2. <span data-ttu-id="eedd1-184">Aktualizacja `spark.driver.extraClassPath` i `spark.executor.extraClassPath` można dołączyć podanego katalogu słoików, rozproszonych w poprzednim kroku, w tym przypadku `/home/sshuser/azure-documentdb-spark/*`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-184">Update the `spark.driver.extraClassPath` and `spark.executor.extraClassPath` to include the directory of the jars that you distributed in the previous step, in this case `/home/sshuser/azure-documentdb-spark/*`.</span></span>

3. <span data-ttu-id="eedd1-185">Dla bazy danych rozwiązania Cosmos platformy Azure, należy podać następujące dane:</span><span class="sxs-lookup"><span data-stu-id="eedd1-185">Provide the following details for Azure Cosmos DB:</span></span>

    ```
    spark.documentdb.Endpoint=https://FILLIN.documents.azure.com:443/
    spark.documentdb.Masterkey=FILLIN
    spark.documentdb.Database=FILLIN
    spark.documentdb.Collection=FILLIN
    # Optional
    #spark.documentdb.preferredRegions=West\ US;West\ US\ 2
    ```
   
## <a name="load-the-tinkerpop-graph-and-save-it-to-azure-cosmos-db"></a><span data-ttu-id="eedd1-186">Załadować wykresu TinkerPop i zapisać go do bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="eedd1-186">Load the TinkerPop graph, and save it to Azure Cosmos DB</span></span>
<span data-ttu-id="eedd1-187">Aby zademonstrować sposób utrwalić wykres do bazy danych z rozwiązania Cosmos platformy Azure, w tym przykładzie używa TinkerPop wstępnie zdefiniowane TinkerPop nowoczesnych wykresu.</span><span class="sxs-lookup"><span data-stu-id="eedd1-187">To demonstrate how to persist a graph into Azure Cosmos DB, this example uses the TinkerPop predefined TinkerPop modern graph.</span></span> <span data-ttu-id="eedd1-188">Wykres są przechowywane w formacie Kryo i jest dostępny w repozytorium TinkerPop.</span><span class="sxs-lookup"><span data-stu-id="eedd1-188">The graph is stored in Kryo format, and it's provided in the TinkerPop repository.</span></span>

1. <span data-ttu-id="eedd1-189">Ponieważ Gremlin działają w trybie YARN, należy udostępnić dane wykresu w systemie plików usługi Hadoop.</span><span class="sxs-lookup"><span data-stu-id="eedd1-189">Because you are running Gremlin in YARN mode, you must make the graph data available in the Hadoop file system.</span></span> <span data-ttu-id="eedd1-190">Użyj następujących poleceń, aby udostępnić katalogu i skopiuj do niego pliku lokalnego wykresu.</span><span class="sxs-lookup"><span data-stu-id="eedd1-190">Use the following commands to make a directory and copy the local graph file into it.</span></span> 

    ```bash
    $ tinkerpop:
    hadoop fs -mkdir /graphData
    hadoop fs -copyFromLocal ~/tinkerpop/data/tinkerpop-modern.kryo /graphData/tinkerpop-modern.kryo
    ```

2. <span data-ttu-id="eedd1-191">Tymczasowo zaktualizować `gremlin-spark.properties` plik `GryoInputFormat` do odczytu na wykresie.</span><span class="sxs-lookup"><span data-stu-id="eedd1-191">Temporarily update the `gremlin-spark.properties` file to use `GryoInputFormat` to read the graph.</span></span> <span data-ttu-id="eedd1-192">Również wskazywać `inputLocation` jako katalog można utworzyć, co przedstawiono poniżej:</span><span class="sxs-lookup"><span data-stu-id="eedd1-192">Also indicate `inputLocation` as the directory you create, as in the following:</span></span>

    ```
    gremlin.hadoop.graphReader=org.apache.tinkerpop.gremlin.hadoop.structure.io.gryo.GryoInputFormat
    gremlin.hadoop.inputLocation=/graphData/tinkerpop-modern.kryo
    ```

3. <span data-ttu-id="eedd1-193">Uruchom konsolę Gremlin, a następnie utwórz następujące kroki obliczeń do utrwalenia danych do skonfigurowanej kolekcji bazy danych rozwiązania Cosmos Azure:</span><span class="sxs-lookup"><span data-stu-id="eedd1-193">Start Gremlin Console, and then create the following computation steps to persist data to the configured Azure Cosmos DB collection:</span></span>  

    <span data-ttu-id="eedd1-194">a.</span><span class="sxs-lookup"><span data-stu-id="eedd1-194">a.</span></span> <span data-ttu-id="eedd1-195">Utwórz wykres `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-195">Create the graph `graph = GraphFactory.open("conf/hadoop/gremlin-spark.properties")`.</span></span>

    <span data-ttu-id="eedd1-196">b.</span><span class="sxs-lookup"><span data-stu-id="eedd1-196">b.</span></span> <span data-ttu-id="eedd1-197">Użyj SparkGraphComputer do zapisu `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-197">Use SparkGraphComputer for writing `graph.compute(SparkGraphComputer.class).result(GraphComputer.ResultGraph.NEW).persist(GraphComputer.Persist.EDGES).program(TraversalVertexProgram.build().traversal(graph.traversal().withComputer(Computer.compute(SparkGraphComputer.class)),"gremlin-groovy","g.V()").create(graph)).submit().get()`.</span></span>

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

4. <span data-ttu-id="eedd1-198">Z poziomu Eksploratora danych można sprawdzić utrwalone dane do bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="eedd1-198">From Data Explorer, you can verify that the data has been persisted to Azure Cosmos DB.</span></span>

## <a name="load-the-graph-from-azure-cosmos-db-and-run-gremlin-queries"></a><span data-ttu-id="eedd1-199">Ładowanie wykres z bazy danych Azure rozwiązania Cosmos i uruchamiać zapytania Gremlin</span><span class="sxs-lookup"><span data-stu-id="eedd1-199">Load the graph from Azure Cosmos DB, and run Gremlin queries</span></span>

1. <span data-ttu-id="eedd1-200">Aby załadować wykresu, należy edytować `gremlin-spark.properties` można ustawić `graphReader` do `DocumentDBInputRDD`:</span><span class="sxs-lookup"><span data-stu-id="eedd1-200">To load the graph, edit `gremlin-spark.properties` to set `graphReader` to `DocumentDBInputRDD`:</span></span>

    ```
    gremlin.hadoop.graphReader=com.microsoft.azure.documentdb.spark.gremlin.DocumentDBInputRDD
    ```

2. <span data-ttu-id="eedd1-201">Załadować wykresu, przechodzenie przez dane i uruchamiać zapytania Gremlin z nim, wykonując następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eedd1-201">Load the graph, traverse the data, and run Gremlin queries with it by doing the following:</span></span>

    <span data-ttu-id="eedd1-202">a.</span><span class="sxs-lookup"><span data-stu-id="eedd1-202">a.</span></span> <span data-ttu-id="eedd1-203">Uruchom konsolę Gremlin `bin/gremlin.sh`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-203">Start the Gremlin Console `bin/gremlin.sh`.</span></span>

    <span data-ttu-id="eedd1-204">b.</span><span class="sxs-lookup"><span data-stu-id="eedd1-204">b.</span></span> <span data-ttu-id="eedd1-205">Utwórz wykres z konfiguracją `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-205">Create the graph with the configuration `graph = GraphFactory.open('conf/hadoop/gremlin-spark.properties')`.</span></span>

    <span data-ttu-id="eedd1-206">c.</span><span class="sxs-lookup"><span data-stu-id="eedd1-206">c.</span></span> <span data-ttu-id="eedd1-207">Utwórz przechodzenie wykres z SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span><span class="sxs-lookup"><span data-stu-id="eedd1-207">Create a graph traversal with SparkGraphComputer `g = graph.traversal().withComputer(SparkGraphComputer)`.</span></span>

    <span data-ttu-id="eedd1-208">d.</span><span class="sxs-lookup"><span data-stu-id="eedd1-208">d.</span></span> <span data-ttu-id="eedd1-209">Uruchom następujące kwerendy wykres Gremlin:</span><span class="sxs-lookup"><span data-stu-id="eedd1-209">Run the following Gremlin graph queries:</span></span>

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
> <span data-ttu-id="eedd1-210">Aby wyświetlić bardziej szczegółowe rejestrowanie, należy ustawić dziennika w `conf/log4j-console.properties` na pełniejsze poziom.</span><span class="sxs-lookup"><span data-stu-id="eedd1-210">To see more detailed logging, set the log level in `conf/log4j-console.properties` to a more verbose level.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="eedd1-211">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eedd1-211">Next steps</span></span>

<span data-ttu-id="eedd1-212">W tym artykule szybki start kiedy znasz już sposób pracy z wykresy przez połączenie bazy danych Azure rozwiązania Cosmos i Spark.</span><span class="sxs-lookup"><span data-stu-id="eedd1-212">In this quick-start article, you've learned how to work with graphs by combining Azure Cosmos DB and Spark.</span></span>

> [!div class="nextstepaction"]
