---
title: aaaApache topologii Storm z programu Visual Studio i C# - Azure HDInsight | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate topologii Storm w języku C#. Utworzyć topologię, liczba proste programu word w Visual Studio za pomocą narzędzi Hadoop hello for Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a>Tworzenie topologii C# dla Apache Storm przy użyciu narzędzi Data Lake hello for Visual Studio

Dowiedz się, jak toocreate topologii Storm C# za pomocą usługi Azure Data Lake (Hadoop) z hello narzędzia dla programu Visual Studio. Ten dokument przeprowadzi Cię przez proces hello Tworzenie projektu Storm w Visual Studio, testowanie go lokalnie i wdrażania go tooan Apache Storm w klastrze usługi HDInsight Azure.

Możesz także dowiedzieć się, jak toocreate hybrydowe topologie, wykorzystujące składniki C# i Java.

> [!NOTE]
> Gdy hello kroków w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio, hello skompilowany projekt może mieć tooeither przesyłanego klastra z systemem Linux lub HDInsight opartych na systemie Windows. Topologie SCP.NET obsługują tylko opartych na systemie Linux klastrów utworzonych po 28 października 2016 roku.

Topologia toouse C# z opartą na systemie Linux klaster, należy zaktualizować hello pakietu Microsoft.SCP.Net.SDK NuGet używany przez tooversion Twojego projektu 0.10.0.6 lub nowszej. Hello wersję pakietu hello musi być również zgodna wersja główna hello Storm zainstalowany w usłudze HDInsight.

| Wersja usługi HDInsight | Wersja platformy STORM | Wersja SCP.NET | Domyślna wersja Mono |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| 3.3 |0.10.x |0.10.x.x</br>(tylko w usłudze HDInsight opartych na systemie Windows) | Nie dotyczy |
| 3.4 | 0.10.0.x | 0.10.0.x | 3.2.8 |
| 3,5 | 1.0.2.x | 1.0.0.x | 4.2.1 |
| 3.6 | 1.1.0.x | 1.0.0.x | 4.2.8 |

> [!IMPORTANT]
> Topologie języka C# w klastrach opartych na systemie Linux należy użyć .NET 4.5 i użyj Mono toorun na powitania klastra usługi HDInsight. Sprawdź [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/) dla potencjalnych niezgodności.

## <a name="install-visual-studio"></a>Instalacja programu Visual Studio

Topologie języka C# z SCP.NET można tworzyć przy użyciu jednej z hello następujące wersje programu Visual Studio:

* Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)

* Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)

* Program Visual Studio 2015 lub [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)

* Visual Studio 2017 (dowolna wersja)

## <a name="install-data-lake-tools-for-visual-studio"></a>Zainstaluj Data Lake tools dla programu Visual Studio

tooinstall Data Lake tools dla programu Visual Studio, wykonaj kroki hello w [rozpocząć korzystanie z usługi Data Lake tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a name="install-java"></a>Instalowanie języka Java

Podczas przesyłania topologii Storm z programu Visual Studio SCP.NET generuje plik zip, który zawiera hello topologii i zależności. Java jest używane toocreate te Kompresuj pliki, ponieważ używa ona formatu, który jest bardziej zgodne z opartą na systemie Linux klastrów.

1. Zainstaluj hello Java Developer Kit (JDK) 7 lub nowszego środowiska deweloperskiego. Możesz uzyskać hello JDK Oracle z [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Można również użyć [innych dystrybucje Java](http://openjdk.java.net/).

2. Witaj `JAVA_HOME` środowiska zmiennej musi toohello punktu katalog, który zawiera Java.

3. Witaj `PATH` zmiennej środowiskowej musi zawierać hello `%JAVA_HOME%\bin` katalogu.

Program hello C# console application tooverify że Java i hello JDK są prawidłowo zainstalowane następujące:

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a>Szablony STORM

Witaj usługi Data Lake tools dla Visual Studio zawierają hello następujące szablony:

| Typ projektu | Pokazuje |
| --- | --- |
| Aplikacja STORM |Pusty projekt topologii Storm. |
| Przykładowy składnik zapisywania usługi Azure SQL STORM |Jak tooAzure toowrite bazy danych SQL. |
| Przykładowe czytnika rozwiązania Cosmos Azure DB STORM |Jak tooread z bazy danych usługi Azure rozwiązania Cosmos. |
| Przykładowy składnik zapisywania rozwiązania Cosmos Azure DB STORM |Jak tooAzure toowrite DB rozwiązania Cosmos. |
| Przykładowe czytnika EventHub STORM |Jak tooread z usługi Azure Event Hubs. |
| Przykładowy składnik zapisywania EventHub STORM |Jak tooAzure toowrite usługi Event Hubs. |
| Przykładowe bazy danych HBase czytnika STORM |Jak tooread z bazy danych HBase w usłudze HDInsight klastrów. |
| Przykładowe bazy danych HBase zapisywania STORM |Jak klastrów tooHBase toowrite w usłudze HDInsight. |
| Przykład hybrydowego STORM |Jak toouse składnika Java. |
| Przykładowe STORM |Topologii liczby podstawowych programu word. |

> [!WARNING]
> Nie wszystkie szablony będzie działać z opartą na systemie Linux usługą HDInsight. Pakiety Nuget służące przez hello szablony mogą być niezgodne z Mono. Sprawdź hello [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/) dokumentów i użyj hello [analizator przenośność .NET](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potencjalne problemy.

W hello kroków w tym dokumencie należy użyć hello Podstawowa aplikacja Storm projektu typu toocreate topologii.

### <a name="hbase-templates-notes"></a>Informacje o szablonach HBase

Hello czytnika HBase i szablony zapisywania użyć hello interfejsu API REST HBase, nie hello HBase interfejsu API języka Java, toocommunicate z bazy danych HBase w klastrze usługi HDInsight.

### <a name="eventhub-templates-notes"></a>Informacje o szablonach EventHub

> [!IMPORTANT]
> Witaj opartych na języku Java EventHub spout składnika dołączonego hello czytnika EventHub szablonu nie może działać z systemu Storm w usłudze HDInsight w wersji 3.5 lub nowszej. Zaktualizowana wersja tego składnika jest dostępna w [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).

Aby przykładową topologię, która używa tej składnika i współpracuje z systemu Storm w usłudze HDInsight 3.5, zobacz [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

## <a name="create-a-c-topology"></a>Tworzenie topologii C#

1. Otwórz program Visual Studio, wybierz **pliku** > **nowy**, a następnie wybierz **projektu**.

2. Z hello **nowy projekt** okna, rozwiń węzeł **zainstalowana** > **szablony**i wybierz **usługi Azure Data Lake**. Wybierz z listy hello szablonów **aplikacji Storm**. U dołu hello hello ekranu, wprowadź **WordCount** jako nazwa hello aplikacji hello.

    ![Zrzut ekranu nowego projektu okna](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. Po utworzeniu projektu hello powinny mieć hello następujące pliki:

   * **Plik program.cs**: plik definiuje hello topologii dla projektu. Domyślnie zostanie utworzona domyślną topologię, która składa się z jednego spout i jeden bolt.

   * **Spout.cs**: spout przykład, który emituje liczb losowych.

   * **Bolt.cs**: przykład bolt, który śledzi liczbę elementów emitowane przez hello spout.

     Podczas tworzenia projektu hello NuGet pobieranie najnowszych hello [pakietu SCP.NET](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a>Spout hello wdrożenie

1. Otwórz **Spout.cs**. Elementach spout są używane tooread danych w topologii z zewnętrznego źródła. główne składniki powitania dla spout są:

   * **NextTuple**: wywoływane przez Storm, gdy elementy spout hello jest dozwolone tooemit krotek nowe.

   * **Potwierdzenia** (tylko w przypadku topologii transakcyjnych): obsługuje inicjowane przez inne składniki w topologii hello krotek wysyłane z hello spout potwierdzeń. Potwierdzeniem krotka umożliwia spout hello wiedzieć, że jej został pomyślnie przetworzony przez składniki podrzędne.

   * **Niepowodzenie** (tylko w przypadku topologii transakcyjnych): obsługuje krotek, które są niepowodzenie przetwarzania innych składników w topologii hello. Implementacja metody niepowodzenie umożliwia toore-Emituj hello spójnej kolekcji, dzięki czemu mogą być przetwarzane ponownie.

2. Zamień zawartość hello hello **Spout** klasy z hello następującego tekstu. Ta spout losowo emituje zdania na powitania topologii.

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a>Bolts hello wdrożenie

1. Usunięcie istniejących hello **Bolt.cs** plik z projektu hello.

2. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **Dodaj** > **nowy element**. Wybierz z listy hello **Storm Bolt**, a następnie wprowadź **Splitter.cs** jako nazwa hello. Powtórz ten proces toocreate, drugi bolt o nazwie **Counter.cs**.

   * **Splitter.cs**: implementuje elementu bolt, który dzieli zdania na poszczególnych wyrazów i emituje nowego strumienia słów.

   * **Counter.cs**: implementuje elementu bolt, który zlicza każdego wyrazu i emituje nowego strumienia słów i liczby powitania dla każdego wyrazu.

     > [!NOTE]
     > Tych elementów bolt odczytu i zapisu toostreams, ale można również użyć bolt toocommunicate ze źródeł, takich jak bazy danych lub usługi.

3. Otwórz **Splitter.cs**. Domyślnie ma tylko jedną metodę: **Execute**. Witaj metody Execute jest wywoływane, gdy hello bolt odbiera tuple do przetwarzania. W tym miejscu możesz przeczytać i przetwarzania przychodzących krotek i Emituj krotek wychodzących.

4. Zamień zawartość hello hello **podziału** klasy z hello następującego kodu:

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. Otwórz **Counter.cs**i Zastąp zawartość klasy hello hello następujące czynności:

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a>Zdefiniuj topologię hello

Elementach spout i elementów bolt są rozmieszczone na wykresie, który definiuje sposób hello dane przepływają między składnikami. Ta topologia wykres hello jest następujący:

![Diagram przedstawiający sposób rozmieszczenia elementów](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

Zdania są emitowane z hello spout i są rozproszone tooinstances z hello podziału bolt. bolt podziału Hello dzieli hello zdań w wyrazy, które są rozproszone toohello licznika bolt.

Ponieważ wyrazów jest przechowywanych lokalnie w wystąpienia licznika hello, chcemy się upewnić, że określone wyrazy przepływ toohello toomake tego samego wystąpienia bolt licznika. Każde wystąpienie przechowuje informacje o słów. Ponieważ bolt podziału hello przechowuje bez stanu, rzeczywiście nie ma znaczenia, którego wystąpienia podziału hello otrzymuje zdanie, które.

Otwórz **Program.cs**. Metoda ważne Hello jest **GetTopologyBuilder**, które jest używane toodefine hello topologię, która jest przesyłany tooStorm. Zamień zawartość hello **GetTopologyBuilder** z powitania po topologii hello tooimplement kodu opisanych powyżej:

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a>Przedstawia topologię hello

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **przesłać tooStorm w usłudze HDInsight**.

   > [!NOTE]
   > Jeśli zostanie wyświetlony monit, wprowadź poświadczenia hello subskrypcji platformy Azure. Jeśli masz więcej niż jedną subskrypcję, zaloguj się toohello, który zawiera Storm w klastrze usługi HDInsight.

2. Wybierz Storm w klastrze usługi HDInsight z hello **klaster Storm** listy rozwijanej, a następnie wybierz **przesyłania**. Można monitorować, jeśli przesyłanie hello działa prawidłowo, używając hello **dane wyjściowe** okna.

3. Gdy topologia hello został pomyślnie przesłany, hello **topologii Storm** dla klastra hello powinna zostać wyświetlona. Wybierz hello **WordCount** topologii z hello listy tooview informacji na temat hello systemem topologii.

   > [!NOTE]
   > Można również wyświetlić **topologii Storm** z **Eksploratora serwera**. Rozwiń węzeł **Azure** > **HDInsight**, kliknij prawym przyciskiem myszy klaster Storm w usłudze HDInsight, a następnie wybierz **topologii Storm widoku**.

    tooview informacji o składnikach hello topologii hello, kliknij dwukrotnie składnik hello hello diagramie.

4. Z hello **podsumowanie topologii** wyświetlić, kliknij przycisk **Kill** toostop hello topologii.

   > [!NOTE]
   > Topologii STORM nadal toorun, dopóki nie zostaną one wyłączone lub klaster hello jest usunięty.

## <a name="transactional-topology"></a>Topologia transakcyjne

Topologia poprzedniej Hello jest nietransakcyjnej. składniki Hello w topologii hello implementuje funkcje tooreplaying wiadomości. Na przykład transakcyjne topologii Utwórz projekt i wybierz **próbki Storm** jako hello typu projektu.

Topologie transakcyjne zaimplementować powitania po toosupport powtarzania danych:

* **Buforowanie metadanych**: hello spout muszą być przechowywane metadane dotyczące danych hello wysyłanego, dzięki czemu hello danych można je pobrać i wysyłanego ponownie, jeśli wystąpi błąd. Ponieważ hello danych emitowanych przez próbki hello jest mały, hello danych pierwotnych dla każdej krotki są przechowywane w słowniku powtarzania.

* **Potwierdzenia**: każdego bolt w topologii hello można wywołać `this.ctx.Ack(tuple)` tooacknowledge, że pomyślnie przetworzył spójnych kolekcji. Witaj w przypadku wszystkich elementów bolt prześledzone hello krotki, `Ack` wywoływana jest metoda hello spout. Witaj `Ack` metody umożliwia hello spout tooremove danych, który był buforowany powtarzania.

* **Niepowodzenie**: każdego bolt można wywołać `this.ctx.Fail(tuple)` tooindicate przetwarzanie nie powiodło się dla spójnych kolekcji. Błąd Hello propaguje toohello `Fail` metody spout hello, w którym krotki hello można odtworzyć za pomocą buforowanych metadanych.

* **Identyfikator sekwencji**: podczas emitowania krotka, można określić identyfikator unikatowy ciąg. Ta wartość określa krotki hello przetwarzania powtórzeń (Ack i błędów). Na przykład Witaj spout w hello **próbki Storm** projekt używa następujących hello podczas emitowania danych:

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    Ten kod emituje krotka zawiera zdanie toohello domyślny strumień, z identyfikatorem sekwencji hello zawarte w **lastSeqId**. Na przykład **lastSeqId** jest zwiększany dla każdego krotki wysyłanego.

Jak pokazano w hello **próbki Storm** projektu, czy składnik jest transakcyjna można ustawić w czasie wykonywania na podstawie konfiguracji.

## <a name="hybrid-topology-with-c-and-java"></a>Hybrydowych topologii C# i Java

Umożliwia także Data Lake tools dla Visual Studio toocreate hybrydowe topologie, gdzie są niektóre składniki C#, a niektóre Java.

Na przykład topologii hybrydowego Utwórz projekt i wybierz **przykład hybrydowego Storm**. Ten typ przykładowych pokazano hello następujące pojęcia:

* **Java spout** i **C# bolt**: zdefiniowanych w **HybridTopology_javaSpout_csharpBolt**.

    * Transakcyjne wersja jest zdefiniowany w **HybridTopologyTx_javaSpout_csharpBolt**.

* **C# spout** i **Java bolt**: zdefiniowanych w **HybridTopology_csharpSpout_javaBolt**.

    * Transakcyjne wersja jest zdefiniowany w **HybridTopologyTx_csharpSpout_javaBolt**.

  > [!NOTE]
  > Ta wersja również pokazuje, jak toouse Clojure kodu z pliku tekstowego jako składnik Java.


tooswitch hello topologię, która jest używana po przesłaniu hello projektu, po prostu przenieść hello `[Active(true)]` topologii toohello instrukcji ma toouse, przed przesłaniem go toohello klastra.

> [!NOTE]
> Wszystkie pliki hello Java, które są wymagane są dostarczane jako część tego projektu w hello **JavaDependency** folderu.

Podczas tworzenia i przesyłania topologii hybrydowe, należy wziąć pod uwagę następujące hello:

* Należy użyć **JavaComponentConstructor** toocreate wystąpienia hello Klasa Java spout lub bolt.

* Należy używać **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON obiektów danych tooserialize do lub wychodzący składniki Java za pomocą języka Java.

* Podczas przesyłania hello topologii toohello serwera, należy użyć hello **dodatkowe konfiguracje** hello toospecify opcji **ścieżki plików Java**. Określona ścieżka Hello powinna być hello katalog, który zawiera pliki JAR hello, które zawierają klas Java.

### <a name="azure-event-hubs"></a>Azure Event Hubs

Wersja SCP.NET 0.9.4.203 wprowadza nowe klasy i metody specjalnie z myślą o pracy z hello spout Centrum zdarzeń (Java spout, służącą do odczytywania z usługi Event Hubs). Po utworzeniu topologię, która używa spout Centrum zdarzeń Użyj hello następujące metody:

* **EventHubSpoutConfig** klasy: tworzy obiekt zawierający konfigurację hello hello spout składnika.

* **TopologyBuilder.SetEventHubSpout** metody: dodaje hello Centrum zdarzeń spout składnika toohello topologii.

> [!NOTE]
> Możesz nadal korzystać hello **CustomizedInteropJSONSerializer** tooserialize dane generowane przez hello spout.

## <a id="configurationmanager"></a>Użyj program Configuration Manager

Nie używaj **ConfigurationManager** wartości konfiguracji tooretrieve z elementów bolt i spout składników. W ten sposób może spowodować wyjątek pustego wskaźnika. Zamiast tego hello konfiguracji projektu jest przekazywany do topologii Storm hello jako pary kluczy i wartości w kontekście topologii hello. Każdego składnika, który korzysta z wartości konfiguracji musi pobrać je z kontekstu hello podczas inicjowania.

Witaj poniższy kod przedstawia sposób tooretrieve te wartości:

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

Jeśli używasz `Get` tooreturn metody instancję składnika, należy upewnić się, czy przekazaniem zarówno hello `Context` i `Dictionary<string, Object>` Konstruktor toohello parametrów. Witaj przykładem jest podstawowy `Get` metodę, która poprawnie przekazuje te wartości:

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a>Jak tooupdate SCP.NET

Najnowsze wersje SCP.NET obsługuje uaktualnienie pakietu przez pakiet NuGet. Dostępna jest nowa aktualizacja, pojawi się powiadomienie uaktualnienia. Sprawdź toomanually do uaktualnienia, wykonaj następujące kroki:

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **Zarządzaj pakietami NuGet**.

2. Wybierz z Menedżera pakietów hello, **aktualizacje**. Czy jest dostępna aktualizacja, są one dostępne. Kliknij przycisk **aktualizacji** dla tooinstall pakietu hello go.

> [!IMPORTANT]
> Jeśli projekt został utworzony przy użyciu starszej wersji SCP.NET, który nie używa NuGet, należy wykonać hello następujące kroki tooupdate tooa nowszej wersji:
>
> 1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **Zarządzaj pakietami NuGet**.
> 2. Przy użyciu hello **wyszukiwania** pola, Wyszukaj, a następnie dodaj **Microsoft.SCP.Net.SDK** toohello projektu.

## <a name="troubleshoot-common-issues-with-topologies"></a>Rozwiązywanie typowych problemów z topologii

### <a name="null-pointer-exceptions"></a>Wyjątki wskaźnika o wartości null

Gdy używasz topologii C# z klastrem usługi HDInsight opartej na systemie Linux, blokowania i spout składników, które używają **ConfigurationManager** tooread ustawienia konfiguracji w czasie wykonywania mogą zwracać wyjątki wskaźnika o wartości null.

Hello konfiguracji projektu jest przekazywany do topologii Storm hello jako pary kluczy i wartości w kontekście topologii hello. Można go pobrać z hello słownika obiektu, który jest przekazywany tooyour składniki, gdy są one inicjowane.

Aby uzyskać więcej informacji, zobacz hello [ConfigurationManager](#configurationmanager) sekcji tego dokumentu.

### <a name="systemtypeloadexception"></a>System.TypeLoadException

Jeśli używasz topologii C# z klastrem usługi HDInsight opartej na systemie Linux, możesz napotkać hello następujący błąd:

    System.TypeLoadException: Failure has occurred while loading a type.

Ten błąd występuje podczas używania pliku binarnego, który nie jest zgodny z wersją .NET, który obsługuje Mono hello.

W przypadku klastrów usługi HDInsight opartej na systemie Linux upewnij się, że projekt korzysta z plików binarnych skompilowanego dla platformy .NET 4.5.

### <a name="test-a-topology-locally"></a>Testowanie topologii lokalnie

Chociaż jest łatwe toodeploy klastra tooa topologii, w niektórych przypadkach może być konieczne tootest topologii lokalnie. Następujące kroki toorun hello i testów hello przykładową topologię w tym samouczku lokalnie w środowisku projektowania.

> [!WARNING]
> Testowanie lokalnym działa tylko dla basic, C# — tylko topologii. Nie można użyć lokalnego testowanie pod kątem hybrydowe topologie lub topologie, wykorzystujące wiele strumieni.

1. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **właściwości**. We właściwościach projektu hello, zmień hello **Output typu** za**aplikacji konsoli**.

    ![Zrzut ekranu przedstawiający właściwości projektu z wyróżnionym typem danych wyjściowych](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > Pamiętaj toochange hello **Output typu** za tworzenie kopii**biblioteki klas** przed wdrożeniem hello topologii tooa klastra.

2. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello, a następnie wybierz **Dodaj** > **nowy element**. Wybierz **klasy**, a następnie wprowadź **LocalTest.cs** jako nazwa klasy hello. Na koniec kliknij **Dodaj**.

3. Otwórz **LocalTest.cs**i dodaj następujące hello **przy użyciu** instrukcji u góry hello:

    ```csharp
    using Microsoft.SCP;
    ```

4. Użyj hello poniższy kod jako zawartość hello hello **LocalTest** klasy:

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    Zająć tooread moment, za pośrednictwem hello komentarze w kodzie. Ten kod zawiera **LocalContext** toorun hello składników w hello Środowisko deweloperskie, a będzie się powtarzał hello strumienia danych między plikami tootext składników na lokalnym dysku hello.

1. Otwórz **Program.cs**i dodaj następujące toohello hello **Main** metody:

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. Zapisz zmiany hello, a następnie kliknij przycisk **F5** lub wybierz **debugowania** > **Rozpocznij debugowanie** toostart hello projektu. Okno konsoli powinna wyświetlane i rejestrowania stanu hello testów postępu. Gdy **testy zakończone** pojawia się, naciśnij klawisz w dowolnym oknie hello tooclose klucza.

3. Użyj **Eksploratora Windows** toolocate hello katalog, który zawiera projekt. Na przykład: **C:\Users\<your_user_name > \Documents\Visual 2013\Projects\WordCount\WordCount w Studio**. W tym katalogu, otwórz **Bin**, a następnie kliknij przycisk **debugowania**. Powinny pojawić się hello plików tekstowych, które zostały utworzone podczas testów hello: sentences.txt, counter.txt i splitter.txt. Otwórz każdy plik tekstowy i sprawdzić hello danych.

   > [!NOTE]
   > Ciąg danych będzie nadal występował jako tablica wartości dziesiętnych w tych plikach. Na przykład \[[97,103,111]] w hello **splitter.txt** pliku jest słowem hello *i*.

> [!NOTE]
> Należy się hello tooset **typ projektu** kopii za**biblioteki klas** przed wdrożeniem tooa Storm w klastrze usługi HDInsight.

### <a name="log-information"></a>Informacje w Dzienniku

Można łatwo rejestrowanie informacji z składniki topologii sieci, za pomocą `Context.Logger`. Na przykład następujące hello tworzy wpis informacyjny w dzienniku:

```csharp
Context.Logger.Info("Component started");
```

Zarejestrowane informacje mogą być wyświetlane z hello **dziennik usługi Hadoop**, który znajduje się w **Eksploratora serwera**. Rozwiń pozycję powitania dla Storm w klastrze usługi HDInsight, a następnie rozwiń **dziennik usługi Hadoop**. Na koniec wybierz tooview pliku dziennika hello.

> [!NOTE]
> Witaj dzienniki są przechowywane w hello kontem magazynu platformy Azure, który jest używany przez klaster. Dzienniki hello tooview w programie Visual Studio, musisz zalogować się toohello subskrypcji platformy Azure, który jest właścicielem konta magazynu hello.

### <a name="view-error-information"></a>Wyświetl informacje o błędzie

błędy tooview, które wystąpiły w uruchomionej topologii, użyj hello następujące kroki:

1. Z **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello Storm w klastrze usługi HDInsight i wybierz **topologii Storm widoku**.

2. Dla hello **Spout** i **Bolts**, hello **ostatniego błędu** kolumna zawiera informacje na temat hello ostatniego błędu.

3. Wybierz hello **Spout identyfikator** lub **identyfikator Bolt** hello składnika, który zawiera błąd na liście. Na stronie szczegółów hello jest błąd wyświetlania, dodatkowe informacje są wymienione w hello **błędy** sekcji u dołu hello hello strony.

4. tooobtain więcej informacji, wybierz opcję **portu** z hello **modułów** sekcji hello strony, toosee hello Storm procesu roboczego w dzienniku hello ostatnich kilka minut.

### <a name="errors-submitting-topologies"></a>Błędy przesyłania topologii

Jeśli wystąpią błędy przesyłania tooHDInsight topologii hello składników po stronie serwera, które obsługi przesyłania topologii w klastrze usługi HDInsight można znaleźć dzienników. tooretrieve te dzienniki, użyj hello następujące polecenie w wierszu polecenia:

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

Zastąp __sshuser__ z hello konta użytkownika SSH hello klastra. Zastąp __clustername__ o nazwie hello hello klastra usługi HDInsight. Aby uzyskać więcej informacji na temat używania `scp` i `ssh` z usługą HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Przesyłanie może zakończyć się niepowodzeniem kilka przyczyn:

* JDK nie jest zainstalowany lub nie znajduje się w ścieżce hello.
* Wymagane zależności Java nie znajdują się w hello przesyłania.
* Niezgodne zależności.
* Zduplikowane nazwy topologii.

Jeśli hello `hdinsight-scpwebapi.out` dziennik zawiera `FileNotFoundException`, może to być spowodowane hello następujące warunki:

* Witaj JDK nie jest w ścieżce hello na powitania Środowisko deweloperskie. Sprawdź, że hello JDK jest zainstalowany w hello Środowisko deweloperskie, który `%JAVA_HOME%/bin` znajduje się w ścieżce hello.
* Brak zależności Java. Upewnij się, że łącznie z plikami wymagane JAR jako część hello przesyłania.

## <a name="next-steps"></a>Następne kroki

Na przykład przetwarzania danych z usługi Event Hubs, zobacz [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).

Na przykład topologii C#, która dzieli strumienia danych na wiele strumieni zobacz [przykład C# Storm](https://github.com/Blackmist/csharp-storm-example).

Zobacz więcej informacji o tworzeniu topologie języka C#, toodiscover [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).

Więcej sposobów toowork z usługą HDInsight i więcej Storm na próbkach HDInsight Zobacz hello następujące dokumenty:

**SCP.NET firmy Microsoft**

* [Podręcznik programowania punkt połączenia usługi](hdinsight-storm-scp-programming-guide.md)

**Apache Storm w usłudze HDInsight**

* [Wdrażanie i monitorowanie topologii z systemu Apache Storm w usłudze HDInsight](hdinsight-storm-deploy-monitor-topology.md)
* [Przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)

**Apache Hadoop w usłudze HDInsight**

* [Korzystanie z programu Hive z usługą Hadoop w usłudze HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą Hadoop w usłudze HDInsight](hdinsight-use-pig.md)
* [Używanie MapReduce z usługą Hadoop w usłudze HDInsight](hdinsight-use-mapreduce.md)

**Bazy danych Apache HBase w usłudze HDInsight**

* [Wprowadzenie do korzystania z bazy danych HBase w usłudze HDInsight](hdinsight-hbase-tutorial-get-started.md)
