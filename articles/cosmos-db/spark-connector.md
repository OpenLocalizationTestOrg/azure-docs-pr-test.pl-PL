---
title: "aaaConnecting Apache Spark tooAzure DB rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Użyj tego samouczka toolearn o hello Azure Spark DB rozwiązania Cosmos łącznik, który pozwala tooconnect Apache Spark tooAzure DB rozwiązania Cosmos tooperform rozproszonych agregacji i danych nauki na powitania wielodostępne globalnie Rozproszony system bazy danych firmy Microsoft przeznaczoną dla hello chmury."
keywords: Platforma Apache spark
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: c4f46007-2606-4273-ab16-29d0e15c0736
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: denlee
ms.openlocfilehash: 70b496fc5ca8f65675f0224e749637f5d533c346
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="d9c5b-104">Przyspieszenie w czasie rzeczywistym analizy danych big data w usłudze hello Spark tooAzure DB rozwiązania Cosmos łącznika</span><span class="sxs-lookup"><span data-stu-id="d9c5b-104">Accelerate real-time big-data analytics with hello Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="d9c5b-105">Witaj Spark tooAzure DB rozwiązania Cosmos łącznika umożliwia tooact bazy danych Azure rozwiązania Cosmos jako źródło danych wejściowych lub ujście danych wyjściowych zadań Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-105">hello Spark tooAzure Cosmos DB connector enables Azure Cosmos DB tooact as an input source or output sink for Apache Spark jobs.</span></span> <span data-ttu-id="d9c5b-106">Łączenie [Spark](http://spark.apache.org/) za[bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) przyspiesza z możliwości toosolve szybko danych nauka problemy, których można użyć bazy danych Azure rozwiązania Cosmos tooquickly utrwalić zapytania na danych.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-106">Connecting [Spark](http://spark.apache.org/) too[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) accelerates your ability toosolve fast-moving data science problems where you can use Azure Cosmos DB tooquickly persist and query data.</span></span> <span data-ttu-id="d9c5b-107">Hello Spark tooAzure DB rozwiązania Cosmos łącznika wydajnie korzysta hello natywnego indeksy bazy danych rozwiązania Cosmos Azure zarządzanych.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-107">hello Spark tooAzure Cosmos DB connector efficiently utilizes hello native Azure Cosmos DB managed indexes.</span></span> <span data-ttu-id="d9c5b-108">indeksy Hello włączyć można aktualizować kolumny wykonywać analizy i rozwijana wypychania predykat filtrowania pod kątem fast zmiany globalnie rozproszone dane, które należeć do zakresu od scenariuszy nauki i analiza toodata Internetu rzeczy (IoT).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-108">hello indexes enable updateable columns when you perform analytics and push-down predicate filtering against fast-changing globally distributed data, which range from Internet of Things (IoT) toodata science and analytics scenarios.</span></span>

<span data-ttu-id="d9c5b-109">Do pracy z Spark, GraphX oraz hello Gremlin graph API Azure DB rozwiązania Cosmos, zobacz [wykonywać analizy wykresu przy użyciu platformy Spark i Apache TinkerPop Gremlin](spark-connector-graph.md).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-109">For working with Spark GraphX and hello Gremlin graph APIs of Azure Cosmos DB, see [Perform graph analytics using Spark and Apache TinkerPop Gremlin](spark-connector-graph.md).</span></span>

## <a name="download"></a><span data-ttu-id="d9c5b-110">Do pobrania</span><span class="sxs-lookup"><span data-stu-id="d9c5b-110">Download</span></span>

<span data-ttu-id="d9c5b-111">Rozpoczęto tooget, Pobierz hello Spark tooAzure DB rozwiązania Cosmos connector (wersja zapoznawcza) z hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repozytorium w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-111">tooget started, download hello Spark tooAzure Cosmos DB connector (preview) from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repository on GitHub.</span></span>

## <a name="connector-components"></a><span data-ttu-id="d9c5b-112">Łącznik składników</span><span class="sxs-lookup"><span data-stu-id="d9c5b-112">Connector components</span></span>

<span data-ttu-id="d9c5b-113">Łącznik Hello wykorzystuje hello następujące składniki:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-113">hello connector utilizes hello following components:</span></span>

* <span data-ttu-id="d9c5b-114">[Azure DB rozwiązania Cosmos](http://documentdb.com) umożliwia klientom tooprovision i elastycznie skalować zarówno przepływność i Magazyn przez dowolną liczbę regionów geograficznych.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-114">[Azure Cosmos DB](http://documentdb.com) enables customers tooprovision and elastically scale both throughput and storage across any number of geographical regions.</span></span> <span data-ttu-id="d9c5b-115">Witaj oferty usługi:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-115">hello service offers:</span></span>
   * <span data-ttu-id="d9c5b-116">Włącz klucz [dystrybucji globalnego](distribute-data-globally.md) i skalowanie w poziomie</span><span class="sxs-lookup"><span data-stu-id="d9c5b-116">Turn key [global distribution](distribute-data-globally.md) and horizontal scale</span></span>
   * <span data-ttu-id="d9c5b-117">Gwarantowane pojedynczą cyfrą opóźnienia na powitania 99-ty percentyl</span><span class="sxs-lookup"><span data-stu-id="d9c5b-117">Guaranteed single digit latencies at hello 99th percentile</span></span>
   * [<span data-ttu-id="d9c5b-118">Wiele modeli dobrze zdefiniowany spójności</span><span class="sxs-lookup"><span data-stu-id="d9c5b-118">Multiple well-defined consistency models</span></span>](consistency-levels.md)
   * <span data-ttu-id="d9c5b-119">Zagwarantować wysokiej dostępności z możliwości wielu</span><span class="sxs-lookup"><span data-stu-id="d9c5b-119">Guaranteed high availability with multi-homing capabilities</span></span>
   * <span data-ttu-id="d9c5b-120">Wszystkie funkcje bazują na branży, kompleksowe [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-120">All features are backed by industry-leading, comprehensive [service level agreements](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLAs).</span></span>

* <span data-ttu-id="d9c5b-121">[Platforma Apache Spark](http://spark.apache.org/) jest aparat przetwarzania zaawansowanych typu open source, która opiera się szybkości, łatwości użycia i zaawansowanych możliwości analitycznych.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-121">[Apache Spark](http://spark.apache.org/) is a powerful open source processing engine that's built around speed, ease of use, and sophisticated analytics.</span></span>

* <span data-ttu-id="d9c5b-122">[Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) tak, aby platforma Apache Spark w chmurze hello wdrożeń krytycznym można wdrożyć za pomocą [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-122">[Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) so that you can deploy Apache Spark in hello cloud for mission-critical deployments by using [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).</span></span>

<span data-ttu-id="d9c5b-123">Oficjalnie obsługiwane wersje:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-123">Officially supported versions:</span></span>

| <span data-ttu-id="d9c5b-124">Składnik</span><span class="sxs-lookup"><span data-stu-id="d9c5b-124">Component</span></span> | <span data-ttu-id="d9c5b-125">Wersja</span><span class="sxs-lookup"><span data-stu-id="d9c5b-125">Version</span></span> |
|---------|-------|
|<span data-ttu-id="d9c5b-126">Apache Spark</span><span class="sxs-lookup"><span data-stu-id="d9c5b-126">Apache Spark</span></span>|<span data-ttu-id="d9c5b-127">2.0+</span><span class="sxs-lookup"><span data-stu-id="d9c5b-127">2.0+</span></span>|
| <span data-ttu-id="d9c5b-128">Scala</span><span class="sxs-lookup"><span data-stu-id="d9c5b-128">Scala</span></span>| <span data-ttu-id="d9c5b-129">2.11</span><span class="sxs-lookup"><span data-stu-id="d9c5b-129">2.11</span></span>|
| <span data-ttu-id="d9c5b-130">Zestaw SDK Java usługi DocumentDB platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d9c5b-130">Azure DocumentDB Java SDK</span></span> | <span data-ttu-id="d9c5b-131">1.10.0</span><span class="sxs-lookup"><span data-stu-id="d9c5b-131">1.10.0</span></span> |

<span data-ttu-id="d9c5b-132">Ten artykuł pomaga uruchamiania niektórych proste przykłady za pomocą języka Python (za pośrednictwem pakiet pyDocumentDB) i hello Scala interfejsów.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-132">This article helps you run some simple samples by using Python (via pyDocumentDB) and hello Scala interfaces.</span></span>

<span data-ttu-id="d9c5b-133">Istnieją dwa podejścia tooconnect Apache Spark i bazy danych rozwiązania Cosmos Azure:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-133">There are two approaches tooconnect Apache Spark and Azure Cosmos DB:</span></span>
- <span data-ttu-id="d9c5b-134">Użyj pydocumentdb — za pośrednictwem hello [Azure SDK Python usługi DocumentDB](https://github.com/Azure/azure-documentdb-python).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-134">Use pyDocumentDB via hello [Azure DocumentDB Python SDK](https://github.com/Azure/azure-documentdb-python).</span></span>
- <span data-ttu-id="d9c5b-135">Tworzenie łącznika DB rozwiązania Cosmos tooAzure opartych na języku Java Spark przy użyciu hello [zestawu SDK Java usługi DocumentDB Azure](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-135">Create a Java-based Spark tooAzure Cosmos DB connector by utilizing hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

## <a name="pydocumentdb-implementation"></a><span data-ttu-id="d9c5b-136">Pakiet pyDocumentDB implementacji</span><span class="sxs-lookup"><span data-stu-id="d9c5b-136">pyDocumentDB implementation</span></span>
<span data-ttu-id="d9c5b-137">Bieżący Hello [pydocumentdb — zestaw SDK](https://github.com/Azure/azure-documentdb-python) umożliwia tooconnect Spark tooAzure DB rozwiązania Cosmos pokazane na powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-137">hello current [pyDocumentDB SDK](https://github.com/Azure/azure-documentdb-python) enables you tooconnect Spark tooAzure Cosmos DB as shown in hello following diagram:</span></span>

![Platforma Spark tooAzure DB rozwiązania Cosmos przepływ danych za pośrednictwem pydocumentdb — bazy danych](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a><span data-ttu-id="d9c5b-139">Przepływ danych hello pakiet pyDocumentDB implementacji</span><span class="sxs-lookup"><span data-stu-id="d9c5b-139">Data flow of hello pyDocumentDB implementation</span></span>

<span data-ttu-id="d9c5b-140">Przepływ danych Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-140">hello data flow is as follows:</span></span>

1. <span data-ttu-id="d9c5b-141">węzeł główny Spark Hello łączy toohello bazy danych Azure rozwiązania Cosmos bramy węzła za pośrednictwem pakiet pyDocumentDB.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-141">hello Spark master node connects toohello Azure Cosmos DB gateway node via pyDocumentDB.</span></span> <span data-ttu-id="d9c5b-142">Użytkownik określa tylko hello Spark i bazy danych Azure rozwiązania Cosmos połączenia.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-142">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="d9c5b-143">Połączenia toohello odpowiednich master i bramy węzły są przezroczyste toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-143">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="d9c5b-144">węzeł bramy Hello sprawia, że zapytanie hello Azure DB rozwiązania Cosmos gdzie hello później uruchamiana jest kwerenda dotycząca kolekcji hello partycji w hello węzły danych.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-144">hello gateway node makes hello query against Azure Cosmos DB where hello query subsequently runs against hello collection's partitions in hello data nodes.</span></span> <span data-ttu-id="d9c5b-145">Witaj odpowiedzi dla tych zapytań jest odesłał toohello węzeł bramy i że zestaw wyników jest zwracany węzła głównego toohello Spark.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-145">hello response for those queries is sent back toohello gateway node, and that result set is returned toohello Spark master node.</span></span>
3. <span data-ttu-id="d9c5b-146">Kolejne zapytania (na przykład przed Spark DataFrame) są wysyłane węzłów procesu roboczego Spark toohello do przetworzenia.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-146">Subsequent queries (for example, against a Spark DataFrame) are sent toohello Spark worker nodes for processing.</span></span>

<span data-ttu-id="d9c5b-147">Komunikacja między Spark i bazy danych Azure rozwiązania Cosmos jest ograniczona toohello węzła głównego Spark i bazy danych Azure rozwiązania Cosmos węzłów bramy.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-147">Communication between Spark and Azure Cosmos DB is limited toohello Spark master node and Azure Cosmos DB gateway nodes.</span></span>  <span data-ttu-id="d9c5b-148">zapytania Hello go tak szybko, jak warstwa transportu hello między tymi dwoma węzłami umożliwia.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-148">hello queries go as fast as hello transport layer between these two nodes allows.</span></span>

### <a name="install-pydocumentdb"></a><span data-ttu-id="d9c5b-149">Zainstaluj pakiet pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d9c5b-149">Install pyDocumentDB</span></span>
<span data-ttu-id="d9c5b-150">Można zainstalować pakiet pyDocumentDB w węźle sterowników za pomocą **pip**, na przykład:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-150">You can install pyDocumentDB on your driver node by using **pip**, for example:</span></span>

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a><span data-ttu-id="d9c5b-151">Połącz Spark tooAzure rozwiązania Cosmos bazy danych za pośrednictwem pakiet pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d9c5b-151">Connect Spark tooAzure Cosmos DB via pyDocumentDB</span></span>
<span data-ttu-id="d9c5b-152">Prostota Hello transportu komunikacji hello sprawia, że wykonanie zapytania z tooAzure Spark rozwiązania Cosmos bazy danych przy użyciu pakiet pyDocumentDB stosunkowo proste.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-152">hello simplicity of hello communication transport makes execution of a query from Spark tooAzure Cosmos DB by using pyDocumentDB relatively simple.</span></span>

<span data-ttu-id="d9c5b-153">Witaj następującego kodu fragment kodu przedstawia sposób pakiet pyDocumentDB toouse w kontekście Spark.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-153">hello following code snippet shows how toouse pyDocumentDB in a Spark context.</span></span>

```
# Import Necessary Libraries
import pydocumentdb
from pydocumentdb import document_client
from pydocumentdb import documents
import datetime

# Configuring hello connection policy (allowing for endpoint discovery)
connectionPolicy = documents.ConnectionPolicy()
connectionPolicy.EnableEndpointDiscovery
connectionPolicy.PreferredLocations = ["Central US", "East US 2", "Southeast Asia", "Western Europe","Canada Central"]


# Set keys tooconnect tooAzure Cosmos DB
masterKey = 'le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA=='
host = 'https://doctorwho.documents.azure.com:443/'
client = document_client.DocumentClient(host, {'masterKey': masterKey}, connectionPolicy)
```

<span data-ttu-id="d9c5b-154">Jak wspomniano w hello fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-154">As noted in hello code snippet:</span></span>

* <span data-ttu-id="d9c5b-155">Hello Azure rozwiązania Cosmos DB Python SDK (`pyDocumentDB`) zawiera hello hello wszystkie parametry połączenia to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-155">hello Azure Cosmos DB Python SDK (`pyDocumentDB`) contains hello all hello necessary connection parameters.</span></span> <span data-ttu-id="d9c5b-156">Na przykład hello preferowanych parametru lokalizacje wybierze hello odczytu repliki i priorytet zlecenia.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-156">For example, hello preferred locations parameter chooses hello read replica and priority order.</span></span>
*  <span data-ttu-id="d9c5b-157">Importowanie hello wymagane biblioteki i konfigurowanie sieci **umożliwia** i **hosta** toocreate hello Azure DB rozwiązania Cosmos *klienta* (**pydocumentdb.document_ Klient**).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-157">Import hello necessary libraries and configure your **masterKey** and **host** toocreate hello Azure Cosmos DB *client* (**pydocumentdb.document_client**).</span></span>


### <a name="execute-spark-queries-via-pydocumentdb"></a><span data-ttu-id="d9c5b-158">Wykonywanie zapytań Spark za pośrednictwem pakiet pyDocumentDB</span><span class="sxs-lookup"><span data-stu-id="d9c5b-158">Execute Spark Queries via pyDocumentDB</span></span>
<span data-ttu-id="d9c5b-159">Następujące przykłady Użyj hello bazy danych Azure rozwiązania Cosmos wystąpienia, który został utworzony w poprzedniej fragment hello przy użyciu hello Hello określone klucze tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-159">hello following examples use hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="d9c5b-160">Witaj poniższy fragment kodu łączy toohello **airports.codes** kolekcji koncie DoctorWho hello jako określony wcześniej i uruchamia kwerendy tooextract hello lotnisku miast w stanie Waszyngton.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-160">hello following code snippet connects toohello **airports.codes** collection in hello DoctorWho account as specified earlier and runs a query tooextract hello airport cities in Washington state.</span></span>

```
# Configure Database and Collections
databaseId = 'airports'
collectionId = 'codes'

# Configurations hello Azure Cosmos DB client will use tooconnect toohello database and collection
dbLink = 'dbs/' + databaseId
collLink = dbLink + '/colls/' + collectionId

# Set query parameter
querystr = "SELECT c.City FROM c WHERE c.State='WA'"

# Query documents
query = client.QueryDocuments(collLink, querystr, options=None, partition_key=None)

# Query for partitioned collections
# query = client.QueryDocuments(collLink, query, options= { 'enableCrossPartitionQuery': True }, partition_key=None)

# Push into list `elements`
elements = list(query)
```

<span data-ttu-id="d9c5b-161">Po wykonaniu zapytania hello za pośrednictwem **zapytania**, wynik hello jest **query_iterable. QueryIterable** czyli przekonwertowanego tooa Python listy.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-161">After hello query has been executed via **query**, hello result is a **query_iterable.QueryIterable** that is converted tooa Python list.</span></span> <span data-ttu-id="d9c5b-162">Listy Python można łatwo przekonwertowanego tooa Spark DataFrame przy użyciu hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-162">A Python list can be easily converted tooa Spark DataFrame by using hello following code:</span></span>

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a><span data-ttu-id="d9c5b-163">Dlaczego warto używać hello pakiet pyDocumentDB tooconnect Spark tooAzure rozwiązania Cosmos bazy danych?</span><span class="sxs-lookup"><span data-stu-id="d9c5b-163">Why use hello pyDocumentDB tooconnect Spark tooAzure Cosmos DB?</span></span>
<span data-ttu-id="d9c5b-164">Łączenie tooAzure Spark rozwiązania Cosmos DB przy użyciu pakiet pyDocumentDB jest zazwyczaj w scenariuszach, gdzie:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-164">Connecting Spark tooAzure Cosmos DB by using pyDocumentDB is typically for scenarios where:</span></span>

* <span data-ttu-id="d9c5b-165">Ma toouse języka Python.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-165">You want toouse Python.</span></span>
* <span data-ttu-id="d9c5b-166">Zwracany jest stosunkowo mały zestaw z bazy danych Azure rozwiązania Cosmos tooSpark wyników.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-166">You are returning a relatively small result set from Azure Cosmos DB tooSpark.</span></span> <span data-ttu-id="d9c5b-167">Należy pamiętać, że hello podstawowy zestaw danych z bazy danych rozwiązania Cosmos Azure może być dość duży.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-167">Note that hello underlying dataset in Azure Cosmos DB can be quite large.</span></span> <span data-ttu-id="d9c5b-168">Chcesz zastosować filtry, to znaczy uruchamiania filtrów predykatów źródła bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-168">You are applying filters, that is, running predicate filters, against your Azure Cosmos DB source.</span></span>  

## <a name="spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="d9c5b-169">Platforma Spark tooAzure łącznika DB rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="d9c5b-169">Spark tooAzure Cosmos DB connector</span></span>

<span data-ttu-id="d9c5b-170">Łącznik DB rozwiązania Cosmos tooAzure Spark Hello wykorzystuje hello [zestawu SDK Java usługi DocumentDB Azure](https://github.com/Azure/azure-documentdb-java) i przenosi dane między węzłami procesów roboczych hello Spark i bazy danych Azure rozwiązania Cosmos, jak pokazano w powitania po diagramu:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-170">hello Spark tooAzure Cosmos DB connector utilizes hello [Azure DocumentDB Java SDK](https://github.com/Azure/azure-documentdb-java) and moves data between hello Spark worker nodes and Azure Cosmos DB as shown in hello following diagram:</span></span>

![Przepływ danych w hello Spark tooAzure DB rozwiązania Cosmos łącznika](./media/spark-connector/spark-connector.png)

<span data-ttu-id="d9c5b-172">Przepływ danych Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-172">hello data flow is as follows:</span></span>

1. <span data-ttu-id="d9c5b-173">węzeł główny Spark Hello łączy toohello bazy danych Azure rozwiązania Cosmos bramy węzła tooobtain hello partycji mapy.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-173">hello Spark master node connects toohello Azure Cosmos DB gateway node tooobtain hello partition map.</span></span> <span data-ttu-id="d9c5b-174">Użytkownik określa tylko hello Spark i bazy danych Azure rozwiązania Cosmos połączenia.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-174">A user specifies only hello Spark and Azure Cosmos DB connections.</span></span> <span data-ttu-id="d9c5b-175">Połączenia toohello odpowiednich master i bramy węzły są przezroczyste toohello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-175">Connections toohello respective master and gateway nodes are transparent toohello user.</span></span>
2. <span data-ttu-id="d9c5b-176">Te informacje są dostarczane węzła głównego Spark toohello Wstecz.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-176">This information is provided back toohello Spark master node.</span></span>  <span data-ttu-id="d9c5b-177">W tym momencie powinna być stanie tooparse hello zapytania toodetermine hello partycji i ich lokalizacje w usłudze Azure DB rozwiązania Cosmos konieczność tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-177">At this point, you should be able tooparse hello query toodetermine hello partitions and their locations in Azure Cosmos DB that you need tooaccess.</span></span>
3. <span data-ttu-id="d9c5b-178">Te informacje są węzłami procesów roboczych Spark toohello przesyłane.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-178">This information is transmitted toohello Spark worker nodes.</span></span>
4. <span data-ttu-id="d9c5b-179">węzłów procesu roboczego Spark Hello połączyć partycji bazy danych Azure rozwiązania Cosmos toohello bezpośrednio tooextract hello danych i zwróć toohello danych hello partycje Spark węzłów procesu roboczego Spark hello.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-179">hello Spark worker nodes connect toohello Azure Cosmos DB partitions directly tooextract hello data and return hello data toohello Spark partitions in hello Spark worker nodes.</span></span>

<span data-ttu-id="d9c5b-180">Komunikacja między Spark i bazy danych Azure rozwiązania Cosmos jest znacznie szybsze ponieważ hello przenoszenia danych między węzłami procesów roboczych hello Spark i węzły danych bazy danych Azure rozwiązania Cosmos hello (partycje).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-180">Communication between Spark and Azure Cosmos DB is significantly faster because hello data movement is between hello Spark worker nodes and hello Azure Cosmos DB data nodes (partitions).</span></span>

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a><span data-ttu-id="d9c5b-181">Tworzenie łącznika DB rozwiązania Cosmos tooAzure Spark hello</span><span class="sxs-lookup"><span data-stu-id="d9c5b-181">Build hello Spark tooAzure Cosmos DB connector</span></span>
<span data-ttu-id="d9c5b-182">Obecnie hello łącznika projekt używa maven.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-182">Currently, hello connector project uses maven.</span></span> <span data-ttu-id="d9c5b-183">Łącznik hello toobuild bez zależności, możesz uruchomić:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-183">toobuild hello connector without dependencies, you can run:</span></span>
```
mvn clean package
```
<span data-ttu-id="d9c5b-184">Możesz również pobrać najnowsze wersje hello JAR hello z hello *zwalnia* folderu.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-184">You can also download hello latest versions of hello JAR from hello *releases* folder.</span></span>

### <a name="include-hello-azure-cosmos-db-spark-jar"></a><span data-ttu-id="d9c5b-185">Zawierają hello Azure rozwiązania Cosmos DB Spark JAR</span><span class="sxs-lookup"><span data-stu-id="d9c5b-185">Include hello Azure Cosmos DB Spark JAR</span></span>
<span data-ttu-id="d9c5b-186">Przed wykonaniem dowolny kod należy hello tooinclude JAR Spark DB Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-186">Before you execute any code, you need tooinclude hello Azure Cosmos DB Spark JAR.</span></span>  <span data-ttu-id="d9c5b-187">Jeśli używasz hello **spark powłoki**, a następnie mogą obejmować hello JAR przy użyciu hello **— słoików** opcji.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-187">If you are using hello **spark-shell**, then you can include hello JAR by using hello **--jars** option.</span></span>  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

<span data-ttu-id="d9c5b-188">Jeśli chcesz tooexecute hello JAR bez zależności, użyj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-188">If you want tooexecute hello JAR without dependencies, use hello following code:</span></span>

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

<span data-ttu-id="d9c5b-189">Jeśli używasz usługi notesu, takich jak Azure HDInsight Jupyter notebook usługi można użyć hello **spark magic** polecenia:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-189">If you are using a notebook service such as Azure HDInsight Jupyter notebook service, you can use hello **spark magic** commands:</span></span>

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

<span data-ttu-id="d9c5b-190">Hello **słoików** polecenie umożliwia tooinclude możesz Witaj dwie JARs, które są potrzebne dla **azure-cosmosdb-spark** (się i hello Azure SDK Java usługi DocumentDB) i wykluczyć **scala-odzwierciedlają** tak, aby nie zakłóca hello wywołuje Livy (notesu Jupyter > Livy > Spark).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-190">hello **jars** command enables you tooinclude hello two JARs that are needed for **azure-cosmosdb-spark** (itself and hello Azure DocumentDB Java SDK) and exclude **scala-reflect** so that it does not interfere with hello Livy calls (Jupyter notebook > Livy > Spark).</span></span>

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a><span data-ttu-id="d9c5b-191">Połącz Spark przy użyciu rozwiązania Cosmos DB tooAzure hello łącznika</span><span class="sxs-lookup"><span data-stu-id="d9c5b-191">Connect Spark tooAzure Cosmos DB using hello connector</span></span>
<span data-ttu-id="d9c5b-192">Chociaż transportu komunikacji hello jest nieco bardziej skomplikowane, wykonywanie zapytania z Spark tooAzure rozwiązania Cosmos DB za pomocą łącznika hello jest znacznie szybsze.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-192">Although hello communication transport is a little more complicated, executing a query from Spark tooAzure Cosmos DB by using hello connector is significantly faster.</span></span>

<span data-ttu-id="d9c5b-193">Witaj następującego fragmentu kodu pokazuje, jak toouse hello łącznika w kontekście Spark.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-193">hello following code snippet shows how toouse hello connector in a Spark context.</span></span>

```
// Import Necessary Libraries
import org.joda.time._
import org.joda.time.format._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Configure connection tooyour collection
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="d9c5b-194">Jak wspomniano w hello fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-194">As noted in hello code snippet:</span></span>

- <span data-ttu-id="d9c5b-195">**Azure — cosmosdb-spark** zawiera hello hello wszystkie parametry połączenia niezbędne, lokalizacje hello preferowany.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-195">**azure-cosmosdb-spark** contains hello all hello necessary connection parameters, which include hello preferred locations.</span></span> <span data-ttu-id="d9c5b-196">Można na przykład hello odczytu repliki i priorytet zlecenia.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-196">For example, you can choose hello read replica and priority order.</span></span>
- <span data-ttu-id="d9c5b-197">Po prostu zaimportować hello wymagane biblioteki i konfigurowanie umożliwia i hosta klienta bazy danych Azure rozwiązania Cosmos hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-197">Just import hello necessary libraries and configure your masterKey and host toocreate hello Azure Cosmos DB client.</span></span>

### <a name="execute-spark-queries-via-hello-connector"></a><span data-ttu-id="d9c5b-198">Wykonywanie zapytań Spark za pośrednictwem łącznika hello</span><span class="sxs-lookup"><span data-stu-id="d9c5b-198">Execute Spark queries via hello connector</span></span>

<span data-ttu-id="d9c5b-199">powitania po przykład używa hello bazy danych Azure rozwiązania Cosmos wystąpienia, który został utworzony w poprzedniej fragment hello przy użyciu hello określone klucze tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-199">hello following example uses hello Azure Cosmos DB instance that was created in hello previous snippet by using hello specified read-only keys.</span></span> <span data-ttu-id="d9c5b-200">Witaj poniższy fragment kodu łączy z kolekcji DepartureDelays.flights_pcoll toohello (w hello DoctorWho konto określone wcześniej) i uruchamia kwerendy tooextract hello opóźnienie informacji o lotach, które są wychodzących z Seattle.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-200">hello following code snippet connects toohello DepartureDelays.flights_pcoll collection (in hello DoctorWho account as specified earlier) and runs a query tooextract hello flight delay information of flights that are departing from Seattle.</span></span>

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a><span data-ttu-id="d9c5b-201">Dlaczego warto używać hello Spark tooAzure DB rozwiązania Cosmos łącznika wdrożenia?</span><span class="sxs-lookup"><span data-stu-id="d9c5b-201">Why use hello Spark tooAzure Cosmos DB connector implementation?</span></span>

<span data-ttu-id="d9c5b-202">Łączenie tooAzure Spark rozwiązania Cosmos DB za pomocą łącznika hello jest zwykle w scenariuszach, gdzie:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-202">Connecting Spark tooAzure Cosmos DB by using hello connector is typically for scenarios where:</span></span>

* <span data-ttu-id="d9c5b-203">Mają toouse Scala i zaktualizować je tooinclude otoki Python, zgodnie z opisem w [problem 3: przykłady i dodać Python otoki](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-203">You want toouse Scala and update it tooinclude a Python wrapper as noted in [Issue 3: Add Python wrapper and examples](https://github.com/Azure/azure-cosmosdb-spark/issues/3).</span></span>
* <span data-ttu-id="d9c5b-204">Masz dużą ilość danych tootransfer między Apache Spark i bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-204">You have a large amount of data tootransfer between Apache Spark and Azure Cosmos DB.</span></span>

<span data-ttu-id="d9c5b-205">toogive pomysł hello poprawę wydajności zapytań, zobaczysz hello [wiki zapytania uruchomień testów](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-205">toogive you an idea of hello query performance difference, see hello [Query Test Runs wiki](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).</span></span>

## <a name="distributed-aggregation-example"></a><span data-ttu-id="d9c5b-206">Przykład rozproszonej agregacji</span><span class="sxs-lookup"><span data-stu-id="d9c5b-206">Distributed aggregation example</span></span>
<span data-ttu-id="d9c5b-207">Ta sekcja zawiera przykłady związanych z wykonaniem rozproszonej agregacji i analiza za pomocą platformy Apache Spark i bazy danych Azure rozwiązania Cosmos ze sobą.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-207">This section provides some examples of how you can do distributed aggregations and analytics by using Apache Spark and Azure Cosmos DB together.</span></span> <span data-ttu-id="d9c5b-208">Azure DB rozwiązania Cosmos już obsługuje agregacji, które opisano w hello [planety agreguje skali z bazy danych Azure rozwiązania Cosmos blogu](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-208">Azure Cosmos DB already supports aggregations, which is discussed in hello [Planet scale aggregates with Azure Cosmos DB blog](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/).</span></span> <span data-ttu-id="d9c5b-209">Oto jak można przenieść je toohello obok poziomu z platformy Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-209">Here is how you can take it toohello next level with Apache Spark.</span></span>

<span data-ttu-id="d9c5b-210">Należy pamiętać, że są tych agregacji w toohello odwołania [Spark tooAzure łącznika DB rozwiązania Cosmos notesu](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-210">Note that these aggregations are in reference toohello [Spark tooAzure Cosmos DB Connector notebook](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).</span></span>

### <a name="connect-tooflights-sample-data"></a><span data-ttu-id="d9c5b-211">Połącz tooflights przykładowe dane</span><span class="sxs-lookup"><span data-stu-id="d9c5b-211">Connect tooflights sample data</span></span>
<span data-ttu-id="d9c5b-212">Te przykłady agregacji dostępu niektóre dane dotyczące wydajności transmitowane przechowywanego w naszym **DoctorWho** bazy danych z bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-212">These aggregation examples access some flight performance data that's stored in our **DoctorWho** Azure Cosmos DB database.</span></span> <span data-ttu-id="d9c5b-213">tooconnect tooit należy hello tooutilize następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-213">tooconnect tooit, you need tooutilize hello following code snippet:</span></span>

```
// Import Spark tooAzure Cosmos DB connector
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.config.Config

// Connect tooAzure Cosmos DB Database
val readConfig2 = Config(Map("Endpoint" -> "https://doctorwho.documents.azure.com:443/",
"Masterkey" -> "le1n99i1w5l7uvokJs3RT5ZAH8dc3ql7lx2CG0h0kK4lVWPkQnwpRLyAN0nwS1z4Cyd1lJgvGUfMWR3v8vkXKA==",
"Database" -> "DepartureDelays",
"preferredRegions" -> "Central US;East US 2;",
"Collection" -> "flights_pcoll",
"SamplingRatio" -> "1.0"))

// Create collection connection
val coll = spark.sqlContext.read.cosmosDB(readConfig2)
coll.createOrReplaceTempView("c")
```

<span data-ttu-id="d9c5b-214">Dzięki ta Wstawka kodu mamy także będzie toorun zapytania bazowego czy transferów hello odfiltrowanego zbioru danych z bazy danych Azure rozwiązania Cosmos tooSpark gdzie hello później można wykonać agreguje rozproszonych.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-214">With this snippet, we are also going toorun a base query that transfers hello filtered set of data from Azure Cosmos DB tooSpark where hello latter can perform distributed aggregates.</span></span> <span data-ttu-id="d9c5b-215">W takim przypadku prosimy w lotach, które odbiegają od Seattle (SEA).</span><span class="sxs-lookup"><span data-stu-id="d9c5b-215">In this case, we are asking for flights that depart from Seattle (SEA).</span></span>

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

<span data-ttu-id="d9c5b-216">Witaj następujące wyniki zostały wygenerowane przez uruchomienie zapytania hello z hello usługi notesu Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-216">hello following results were generated by running hello queries from hello Jupyter notebook service.</span></span>  <span data-ttu-id="d9c5b-217">Należy zauważyć, że wszystkie wstawki kodu hello tooany ogólny i nie dotyczą usługi.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-217">Note that all hello code snippets are generic and not specific tooany service.</span></span>

### <a name="running-limit-and-count-queries"></a><span data-ttu-id="d9c5b-218">LIMIT uruchomione i liczba zapytań</span><span class="sxs-lookup"><span data-stu-id="d9c5b-218">Running LIMIT and COUNT queries</span></span>
<span data-ttu-id="d9c5b-219">Tylko tak samo, jak jest używany tooin SQL/Spark SQL, teraz należy rozpocząć **LIMIT** zapytania:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-219">Just like you're used tooin SQL/Spark SQL, let's start off with a **LIMIT** query:</span></span>

![Spark LIMIT zapytania](./media/spark-connector/spark-sql-query.png)

<span data-ttu-id="d9c5b-221">Witaj dalej zapytanie jest szybkie i proste **liczba** zapytania:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-221">hello next query is a simple and fast **COUNT** query:</span></span>

![Liczba Spark zapytania](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a><span data-ttu-id="d9c5b-223">GROUP BY zapytania</span><span class="sxs-lookup"><span data-stu-id="d9c5b-223">GROUP BY query</span></span>
<span data-ttu-id="d9c5b-224">W tym zestawie dalej, można łatwo uruchomić **GROUP BY** zapytania względem naszego bazy danych Azure rozwiązania Cosmos bazy danych:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-224">In this next set, we can easily run **GROUP BY** queries against our Azure Cosmos DB database:</span></span>

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Platforma Spark Grupuj według wykresu zapytania](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a><span data-ttu-id="d9c5b-226">DISTINCT, ORDER BY zapytania</span><span class="sxs-lookup"><span data-stu-id="d9c5b-226">DISTINCT, ORDER BY query</span></span>
<span data-ttu-id="d9c5b-227">A Oto **DISTINCT, ORDER BY** zapytania:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-227">And here is a **DISTINCT, ORDER BY** query:</span></span>

![Platforma Spark Grupuj według wykresu zapytania](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a><span data-ttu-id="d9c5b-229">Kontynuować analizę danych transmitowane hello</span><span class="sxs-lookup"><span data-stu-id="d9c5b-229">Continue hello flight data analysis</span></span>
<span data-ttu-id="d9c5b-230">Program hello następujące przykładowe zapytania toocontinue analizy danych transmitowane hello:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-230">You can use hello following example queries toocontinue analysis of hello flight data:</span></span>

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a><span data-ttu-id="d9c5b-231">Najpopularniejsze 5 opóźnione miejsca docelowe (miejscowości) z Seattle</span><span class="sxs-lookup"><span data-stu-id="d9c5b-231">Top 5 delayed destinations (cities) departing from Seattle</span></span>
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Wykres opóźnienia top Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a><span data-ttu-id="d9c5b-233">Obliczenia średniej opóźnienia przez miast docelowych z Seattle</span><span class="sxs-lookup"><span data-stu-id="d9c5b-233">Calculate median delays by destination cities departing from Seattle</span></span>
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Wykres opóźnienia środkowej Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a><span data-ttu-id="d9c5b-235">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9c5b-235">Next steps</span></span>

<span data-ttu-id="d9c5b-236">Jeśli nie jest jeszcze pobrać hello Spark tooAzure DB rozwiązania Cosmos łącznika z hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) repozytorium GitHub i przejrzyj dodatkowe zasoby hello w repozytorium hello:</span><span class="sxs-lookup"><span data-stu-id="d9c5b-236">If you haven't already, download hello Spark tooAzure Cosmos DB connector from hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore hello additional resources in hello repo:</span></span>

* [<span data-ttu-id="d9c5b-237">Przykłady rozproszonej agregacji</span><span class="sxs-lookup"><span data-stu-id="d9c5b-237">Distributed Aggregations Examples</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="d9c5b-238">Przykładowe skrypty i notebooki</span><span class="sxs-lookup"><span data-stu-id="d9c5b-238">Sample Scripts and Notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

<span data-ttu-id="d9c5b-239">Można także tooreview hello [Apache Spark SQL, przewodnik zestawów danych i DataFrames](http://spark.apache.org/docs/latest/sql-programming-guide.html) i hello [Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d9c5b-239">You might also want tooreview hello [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and hello [Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) article.</span></span>
