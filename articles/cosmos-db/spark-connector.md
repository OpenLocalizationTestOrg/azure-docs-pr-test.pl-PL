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
# <a name="accelerate-real-time-big-data-analytics-with-hello-spark-tooazure-cosmos-db-connector"></a>Przyspieszenie w czasie rzeczywistym analizy danych big data w usłudze hello Spark tooAzure DB rozwiązania Cosmos łącznika

Witaj Spark tooAzure DB rozwiązania Cosmos łącznika umożliwia tooact bazy danych Azure rozwiązania Cosmos jako źródło danych wejściowych lub ujście danych wyjściowych zadań Apache Spark. Łączenie [Spark](http://spark.apache.org/) za[bazy danych Azure rozwiązania Cosmos](https://azure.microsoft.com/services/cosmos-db/) przyspiesza z możliwości toosolve szybko danych nauka problemy, których można użyć bazy danych Azure rozwiązania Cosmos tooquickly utrwalić zapytania na danych. Hello Spark tooAzure DB rozwiązania Cosmos łącznika wydajnie korzysta hello natywnego indeksy bazy danych rozwiązania Cosmos Azure zarządzanych. indeksy Hello włączyć można aktualizować kolumny wykonywać analizy i rozwijana wypychania predykat filtrowania pod kątem fast zmiany globalnie rozproszone dane, które należeć do zakresu od scenariuszy nauki i analiza toodata Internetu rzeczy (IoT).

Do pracy z Spark, GraphX oraz hello Gremlin graph API Azure DB rozwiązania Cosmos, zobacz [wykonywać analizy wykresu przy użyciu platformy Spark i Apache TinkerPop Gremlin](spark-connector-graph.md).

## <a name="download"></a>Do pobrania

Rozpoczęto tooget, Pobierz hello Spark tooAzure DB rozwiązania Cosmos connector (wersja zapoznawcza) z hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark/) repozytorium w witrynie GitHub.

## <a name="connector-components"></a>Łącznik składników

Łącznik Hello wykorzystuje hello następujące składniki:

* [Azure DB rozwiązania Cosmos](http://documentdb.com) umożliwia klientom tooprovision i elastycznie skalować zarówno przepływność i Magazyn przez dowolną liczbę regionów geograficznych. Witaj oferty usługi:
   * Włącz klucz [dystrybucji globalnego](distribute-data-globally.md) i skalowanie w poziomie
   * Gwarantowane pojedynczą cyfrą opóźnienia na powitania 99-ty percentyl
   * [Wiele modeli dobrze zdefiniowany spójności](consistency-levels.md)
   * Zagwarantować wysokiej dostępności z możliwości wielu
   * Wszystkie funkcje bazują na branży, kompleksowe [umowy dotyczące poziomu usług](https://azure.microsoft.com/support/legal/sla/cosmos-db) (SLA).

* [Platforma Apache Spark](http://spark.apache.org/) jest aparat przetwarzania zaawansowanych typu open source, która opiera się szybkości, łatwości użycia i zaawansowanych możliwości analitycznych.

* [Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) tak, aby platforma Apache Spark w chmurze hello wdrożeń krytycznym można wdrożyć za pomocą [Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/).

Oficjalnie obsługiwane wersje:

| Składnik | Wersja |
|---------|-------|
|Apache Spark|2.0+|
| Scala| 2.11|
| Zestaw SDK Java usługi DocumentDB platformy Azure | 1.10.0 |

Ten artykuł pomaga uruchamiania niektórych proste przykłady za pomocą języka Python (za pośrednictwem pakiet pyDocumentDB) i hello Scala interfejsów.

Istnieją dwa podejścia tooconnect Apache Spark i bazy danych rozwiązania Cosmos Azure:
- Użyj pydocumentdb — za pośrednictwem hello [Azure SDK Python usługi DocumentDB](https://github.com/Azure/azure-documentdb-python).
- Tworzenie łącznika DB rozwiązania Cosmos tooAzure opartych na języku Java Spark przy użyciu hello [zestawu SDK Java usługi DocumentDB Azure](https://github.com/Azure/azure-documentdb-java).

## <a name="pydocumentdb-implementation"></a>Pakiet pyDocumentDB implementacji
Bieżący Hello [pydocumentdb — zestaw SDK](https://github.com/Azure/azure-documentdb-python) umożliwia tooconnect Spark tooAzure DB rozwiązania Cosmos pokazane na powitania po diagramu:

![Platforma Spark tooAzure DB rozwiązania Cosmos przepływ danych za pośrednictwem pydocumentdb — bazy danych](./media/spark-connector/spark-pydocumentdb.png)


### <a name="data-flow-of-hello-pydocumentdb-implementation"></a>Przepływ danych hello pakiet pyDocumentDB implementacji

Przepływ danych Hello jest następujący:

1. węzeł główny Spark Hello łączy toohello bazy danych Azure rozwiązania Cosmos bramy węzła za pośrednictwem pakiet pyDocumentDB. Użytkownik określa tylko hello Spark i bazy danych Azure rozwiązania Cosmos połączenia. Połączenia toohello odpowiednich master i bramy węzły są przezroczyste toohello użytkownika.
2. węzeł bramy Hello sprawia, że zapytanie hello Azure DB rozwiązania Cosmos gdzie hello później uruchamiana jest kwerenda dotycząca kolekcji hello partycji w hello węzły danych. Witaj odpowiedzi dla tych zapytań jest odesłał toohello węzeł bramy i że zestaw wyników jest zwracany węzła głównego toohello Spark.
3. Kolejne zapytania (na przykład przed Spark DataFrame) są wysyłane węzłów procesu roboczego Spark toohello do przetworzenia.

Komunikacja między Spark i bazy danych Azure rozwiązania Cosmos jest ograniczona toohello węzła głównego Spark i bazy danych Azure rozwiązania Cosmos węzłów bramy.  zapytania Hello go tak szybko, jak warstwa transportu hello między tymi dwoma węzłami umożliwia.

### <a name="install-pydocumentdb"></a>Zainstaluj pakiet pyDocumentDB
Można zainstalować pakiet pyDocumentDB w węźle sterowników za pomocą **pip**, na przykład:

```
pip install pyDocumentDB
```


### <a name="connect-spark-tooazure-cosmos-db-via-pydocumentdb"></a>Połącz Spark tooAzure rozwiązania Cosmos bazy danych za pośrednictwem pakiet pyDocumentDB
Prostota Hello transportu komunikacji hello sprawia, że wykonanie zapytania z tooAzure Spark rozwiązania Cosmos bazy danych przy użyciu pakiet pyDocumentDB stosunkowo proste.

Witaj następującego kodu fragment kodu przedstawia sposób pakiet pyDocumentDB toouse w kontekście Spark.

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

Jak wspomniano w hello fragment kodu:

* Hello Azure rozwiązania Cosmos DB Python SDK (`pyDocumentDB`) zawiera hello hello wszystkie parametry połączenia to konieczne. Na przykład hello preferowanych parametru lokalizacje wybierze hello odczytu repliki i priorytet zlecenia.
*  Importowanie hello wymagane biblioteki i konfigurowanie sieci **umożliwia** i **hosta** toocreate hello Azure DB rozwiązania Cosmos *klienta* (**pydocumentdb.document_ Klient**).


### <a name="execute-spark-queries-via-pydocumentdb"></a>Wykonywanie zapytań Spark za pośrednictwem pakiet pyDocumentDB
Następujące przykłady Użyj hello bazy danych Azure rozwiązania Cosmos wystąpienia, który został utworzony w poprzedniej fragment hello przy użyciu hello Hello określone klucze tylko do odczytu. Witaj poniższy fragment kodu łączy toohello **airports.codes** kolekcji koncie DoctorWho hello jako określony wcześniej i uruchamia kwerendy tooextract hello lotnisku miast w stanie Waszyngton.

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

Po wykonaniu zapytania hello za pośrednictwem **zapytania**, wynik hello jest **query_iterable. QueryIterable** czyli przekonwertowanego tooa Python listy. Listy Python można łatwo przekonwertowanego tooa Spark DataFrame przy użyciu hello następującego kodu:

```
# Create `df` Spark DataFrame from `elements` Python list
df = spark.createDataFrame(elements)
```

### <a name="why-use-hello-pydocumentdb-tooconnect-spark-tooazure-cosmos-db"></a>Dlaczego warto używać hello pakiet pyDocumentDB tooconnect Spark tooAzure rozwiązania Cosmos bazy danych?
Łączenie tooAzure Spark rozwiązania Cosmos DB przy użyciu pakiet pyDocumentDB jest zazwyczaj w scenariuszach, gdzie:

* Ma toouse języka Python.
* Zwracany jest stosunkowo mały zestaw z bazy danych Azure rozwiązania Cosmos tooSpark wyników. Należy pamiętać, że hello podstawowy zestaw danych z bazy danych rozwiązania Cosmos Azure może być dość duży. Chcesz zastosować filtry, to znaczy uruchamiania filtrów predykatów źródła bazy danych Azure rozwiązania Cosmos.  

## <a name="spark-tooazure-cosmos-db-connector"></a>Platforma Spark tooAzure łącznika DB rozwiązania Cosmos

Łącznik DB rozwiązania Cosmos tooAzure Spark Hello wykorzystuje hello [zestawu SDK Java usługi DocumentDB Azure](https://github.com/Azure/azure-documentdb-java) i przenosi dane między węzłami procesów roboczych hello Spark i bazy danych Azure rozwiązania Cosmos, jak pokazano w powitania po diagramu:

![Przepływ danych w hello Spark tooAzure DB rozwiązania Cosmos łącznika](./media/spark-connector/spark-connector.png)

Przepływ danych Hello jest następujący:

1. węzeł główny Spark Hello łączy toohello bazy danych Azure rozwiązania Cosmos bramy węzła tooobtain hello partycji mapy. Użytkownik określa tylko hello Spark i bazy danych Azure rozwiązania Cosmos połączenia. Połączenia toohello odpowiednich master i bramy węzły są przezroczyste toohello użytkownika.
2. Te informacje są dostarczane węzła głównego Spark toohello Wstecz.  W tym momencie powinna być stanie tooparse hello zapytania toodetermine hello partycji i ich lokalizacje w usłudze Azure DB rozwiązania Cosmos konieczność tooaccess.
3. Te informacje są węzłami procesów roboczych Spark toohello przesyłane.
4. węzłów procesu roboczego Spark Hello połączyć partycji bazy danych Azure rozwiązania Cosmos toohello bezpośrednio tooextract hello danych i zwróć toohello danych hello partycje Spark węzłów procesu roboczego Spark hello.

Komunikacja między Spark i bazy danych Azure rozwiązania Cosmos jest znacznie szybsze ponieważ hello przenoszenia danych między węzłami procesów roboczych hello Spark i węzły danych bazy danych Azure rozwiązania Cosmos hello (partycje).

### <a name="build-hello-spark-tooazure-cosmos-db-connector"></a>Tworzenie łącznika DB rozwiązania Cosmos tooAzure Spark hello
Obecnie hello łącznika projekt używa maven. Łącznik hello toobuild bez zależności, możesz uruchomić:
```
mvn clean package
```
Możesz również pobrać najnowsze wersje hello JAR hello z hello *zwalnia* folderu.

### <a name="include-hello-azure-cosmos-db-spark-jar"></a>Zawierają hello Azure rozwiązania Cosmos DB Spark JAR
Przed wykonaniem dowolny kod należy hello tooinclude JAR Spark DB Azure rozwiązania Cosmos.  Jeśli używasz hello **spark powłoki**, a następnie mogą obejmować hello JAR przy użyciu hello **— słoików** opcji.  

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3-jar-with-dependencies.jar
```

Jeśli chcesz tooexecute hello JAR bez zależności, użyj hello następującego kodu:

```
spark-shell --master $master --jars /$location/azure-cosmosdb-spark-0.0.3.jar,/$location/azure-documentdb-1.10.0.jar
```

Jeśli używasz usługi notesu, takich jak Azure HDInsight Jupyter notebook usługi można użyć hello **spark magic** polecenia:

```
%%configure
{ "jars": ["wasb:///example/jars/azure-documentdb-1.10.0.jar","wasb:///example/jars/azure-cosmosdb-spark-0.0.3.jar"],
  "conf": {
    "spark.jars.excludes": "org.scala-lang:scala-reflect"
   }
}
```

Hello **słoików** polecenie umożliwia tooinclude możesz Witaj dwie JARs, które są potrzebne dla **azure-cosmosdb-spark** (się i hello Azure SDK Java usługi DocumentDB) i wykluczyć **scala-odzwierciedlają** tak, aby nie zakłóca hello wywołuje Livy (notesu Jupyter > Livy > Spark).

### <a name="connect-spark-tooazure-cosmos-db-using-hello-connector"></a>Połącz Spark przy użyciu rozwiązania Cosmos DB tooAzure hello łącznika
Chociaż transportu komunikacji hello jest nieco bardziej skomplikowane, wykonywanie zapytania z Spark tooAzure rozwiązania Cosmos DB za pomocą łącznika hello jest znacznie szybsze.

Witaj następującego fragmentu kodu pokazuje, jak toouse hello łącznika w kontekście Spark.

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

Jak wspomniano w hello fragment kodu:

- **Azure — cosmosdb-spark** zawiera hello hello wszystkie parametry połączenia niezbędne, lokalizacje hello preferowany. Można na przykład hello odczytu repliki i priorytet zlecenia.
- Po prostu zaimportować hello wymagane biblioteki i konfigurowanie umożliwia i hosta klienta bazy danych Azure rozwiązania Cosmos hello toocreate.

### <a name="execute-spark-queries-via-hello-connector"></a>Wykonywanie zapytań Spark za pośrednictwem łącznika hello

powitania po przykład używa hello bazy danych Azure rozwiązania Cosmos wystąpienia, który został utworzony w poprzedniej fragment hello przy użyciu hello określone klucze tylko do odczytu. Witaj poniższy fragment kodu łączy z kolekcji DepartureDelays.flights_pcoll toohello (w hello DoctorWho konto określone wcześniej) i uruchamia kwerendy tooextract hello opóźnienie informacji o lotach, które są wychodzących z Seattle.

```
// Queries
var query = "SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'"
val df = spark.sql(query)

// Run DF query (count)
df.count()

// Run DF query (show)
df.show()
```

### <a name="why-use-hello-spark-tooazure-cosmos-db-connector-implementation"></a>Dlaczego warto używać hello Spark tooAzure DB rozwiązania Cosmos łącznika wdrożenia?

Łączenie tooAzure Spark rozwiązania Cosmos DB za pomocą łącznika hello jest zwykle w scenariuszach, gdzie:

* Mają toouse Scala i zaktualizować je tooinclude otoki Python, zgodnie z opisem w [problem 3: przykłady i dodać Python otoki](https://github.com/Azure/azure-cosmosdb-spark/issues/3).
* Masz dużą ilość danych tootransfer między Apache Spark i bazy danych Azure rozwiązania Cosmos.

toogive pomysł hello poprawę wydajności zapytań, zobaczysz hello [wiki zapytania uruchomień testów](https://github.com/Azure/azure-cosmosdb-spark/wiki/Query-Test-Runs).

## <a name="distributed-aggregation-example"></a>Przykład rozproszonej agregacji
Ta sekcja zawiera przykłady związanych z wykonaniem rozproszonej agregacji i analiza za pomocą platformy Apache Spark i bazy danych Azure rozwiązania Cosmos ze sobą. Azure DB rozwiązania Cosmos już obsługuje agregacji, które opisano w hello [planety agreguje skali z bazy danych Azure rozwiązania Cosmos blogu](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/). Oto jak można przenieść je toohello obok poziomu z platformy Apache Spark.

Należy pamiętać, że są tych agregacji w toohello odwołania [Spark tooAzure łącznika DB rozwiązania Cosmos notesu](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/notebooks/Spark-to-CosmosDB_Connector.ipynb).

### <a name="connect-tooflights-sample-data"></a>Połącz tooflights przykładowe dane
Te przykłady agregacji dostępu niektóre dane dotyczące wydajności transmitowane przechowywanego w naszym **DoctorWho** bazy danych z bazy danych Azure rozwiązania Cosmos. tooconnect tooit należy hello tooutilize następującego fragmentu kodu:

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

Dzięki ta Wstawka kodu mamy także będzie toorun zapytania bazowego czy transferów hello odfiltrowanego zbioru danych z bazy danych Azure rozwiązania Cosmos tooSpark gdzie hello później można wykonać agreguje rozproszonych. W takim przypadku prosimy w lotach, które odbiegają od Seattle (SEA).

```
// Run, get row count, and time query
val originSEA = spark.sql("SELECT c.date, c.delay, c.distance, c.origin, c.destination FROM c WHERE c.origin = 'SEA'")
originSEA.createOrReplaceTempView("originSEA")
```

Witaj następujące wyniki zostały wygenerowane przez uruchomienie zapytania hello z hello usługi notesu Jupyter.  Należy zauważyć, że wszystkie wstawki kodu hello tooany ogólny i nie dotyczą usługi.

### <a name="running-limit-and-count-queries"></a>LIMIT uruchomione i liczba zapytań
Tylko tak samo, jak jest używany tooin SQL/Spark SQL, teraz należy rozpocząć **LIMIT** zapytania:

![Spark LIMIT zapytania](./media/spark-connector/spark-sql-query.png)

Witaj dalej zapytanie jest szybkie i proste **liczba** zapytania:

![Liczba Spark zapytania](./media/spark-connector/spark-count-query.png)

### <a name="group-by-query"></a>GROUP BY zapytania
W tym zestawie dalej, można łatwo uruchomić **GROUP BY** zapytania względem naszego bazy danych Azure rozwiązania Cosmos bazy danych:

```
select destination, sum(delay) as TotalDelays
from originSEA
group by destination
order by sum(delay) desc limit 10
```

![Platforma Spark Grupuj według wykresu zapytania](./media/spark-connector/group-by-query-graph.png)

### <a name="distinct-order-by-query"></a>DISTINCT, ORDER BY zapytania
A Oto **DISTINCT, ORDER BY** zapytania:

![Platforma Spark Grupuj według wykresu zapytania](./media/spark-connector/order-by-query.png)

### <a name="continue-hello-flight-data-analysis"></a>Kontynuować analizę danych transmitowane hello
Program hello następujące przykładowe zapytania toocontinue analizy danych transmitowane hello:

#### <a name="top-5-delayed-destinations-cities-departing-from-seattle"></a>Najpopularniejsze 5 opóźnione miejsca docelowe (miejscowości) z Seattle
```
select destination, sum(delay)
from originSEA
where delay < 0
group by destination
order by sum(delay) limit 5
```
![Wykres opóźnienia top Spark](./media/spark-connector/top-delays-graph.png)


#### <a name="calculate-median-delays-by-destination-cities-departing-from-seattle"></a>Obliczenia średniej opóźnienia przez miast docelowych z Seattle
```
select destination, percentile_approx(delay, 0.5) as median_delay
from originSEA
where delay < 0
group by destination
order by percentile_approx(delay, 0.5)
```

![Wykres opóźnienia środkowej Spark](./media/spark-connector/median-delays-graph.png)

## <a name="next-steps"></a>Następne kroki

Jeśli nie jest jeszcze pobrać hello Spark tooAzure DB rozwiązania Cosmos łącznika z hello [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) repozytorium GitHub i przejrzyj dodatkowe zasoby hello w repozytorium hello:

* [Przykłady rozproszonej agregacji](https://github.com/Azure/azure-cosmosdb-spark/wiki/Aggregations-Examples)
* [Przykładowe skrypty i notebooki](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)

Można także tooreview hello [Apache Spark SQL, przewodnik zestawów danych i DataFrames](http://spark.apache.org/docs/latest/sql-programming-guide.html) i hello [Apache Spark w usłudze Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md) artykułu.
