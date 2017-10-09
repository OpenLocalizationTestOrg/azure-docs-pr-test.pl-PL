---
title: "Podręcznik programowania aaaSCP.NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse SCP.NET toocreate. Na podstawie NET topologii Storm do za pomocą Storm w usłudze HDInsight."
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a>Podręcznik programowania punkt połączenia usługi
Punkt połączenia usługi jest czasu rzeczywistego toobuild platformy, niezawodnych, spójne i wysoką wydajność przetwarzania danych aplikacji. Jest ona wbudowana nad [Apache Storm](http://storm.incubator.apache.org/) — systemu projektowania Wspólnot hello OSS przetwarzania strumienia. STORM jest zaprojektowana przez Nathan Marz i otwórz kwerendą źródłową Twitter. Jest przeprowadzana z zastosowaniem [Apache ZooKeeper](http://zookeeper.apache.org/), Apache innego projektu tooenable wysoce niezawodne koordynacji rozproszonego oraz zarządzanie stanem. 

Nie tylko projektu hello SCP systemie Storm w systemie Windows, ale również projekt hello dodany rozszerzenia i dostosowania dla ekosystemu Windows hello. rozszerzenia Hello to środowisko dewelopera .NET i bibliotek, hello modyfikacje obejmują wdrażania systemu Windows. 

Witaj rozszerzenie i dostosowanie odbywa się w taki sposób, że nie występują toofork hello OSS projektów i firma Microsoft może korzystać z ekosystemami pochodnej, rozszerzający Storm.

## <a name="processing-model"></a>Przetwarzanie modelu
dane Hello w punkt połączenia usługi jest modelowana jako ciągłe strumienie spójnych kolekcji. Zwykle krotek hello przepływać do niektórych kolejki najpierw, a następnie pobrana i przekształcenia przez hostowaną wewnątrz topologii Storm logiki biznesowej, koniec hello danych wyjściowych może być przekazywane w potoku jako system tooanother SCP krotek lub być zatwierdzone toostores rozproszonego systemu plików, takich jak lub bazy danych, takich jak SQL Server.

![Diagram kolejki zasilania tooprocessing danych, które źródeł danych magazynu danych](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

Topologia aplikacji Storm, definiuje Graf obliczeń. Każdy węzeł w topologii zawiera logikę przetwarzania i łącza między węzłami Oznaczanie przepływu danych. dane wejściowe tooinject węzłów Hello w topologii hello są nazywane elementach Spout, które mogą być używane toosequence hello danych. Witaj danych wejściowych może znajdować się w plików dzienników, transakcyjne bazy danych licznika wydajności systemu itp. hello węzłów z obu przepływów danych wejściowych i wyjściowych są nazywane elementów Bolt, które hello filtrowania rzeczywiste dane i wybór oraz agregacji.

Punkt połączenia usługi obsługuje starań w najmniej jednokrotne, a dokładnie — raz przetwarzania danych. W przypadku przesyłania strumieniowego przetwarzania aplikacji rozproszonej różne błędy może się tak zdarzyć podczas przetwarzania danych, takich jak awaria sieci, błąd maszyny lub błąd kodu użytkownika itd. Przetwarzanie w najmniej jednokrotne zapewnia wszystkie dane będą przetwarzane co najmniej raz przez powtarzanie automatycznie hello tych samych danych w przypadku błędu. Przetwarzanie w najmniej jednokrotne jest proste i niezawodne i odpowiada także w wielu aplikacjach. Jednak gdy aplikacji hello wymaga dokładnego zliczanie, na przykład w najmniej jednokrotne przetwarzania jest niewystarczająca ponieważ hello tych samych danych może potencjalnie być odtworzone w topologii aplikacji hello. W takim przypadku, dokładnie-po zaprojektowano przetwarzania toomake się, że wynik hello jest poprawna, nawet wtedy, gdy hello danych mogą być odtwarzany i przetwarzane wiele razy.

Punkt połączenia usługi umożliwia aplikacji procesu danych czasu rzeczywistego .NET deweloperzy toodevelop podczas hello wykorzystać maszyny wirtualnej Java (JVM) na podstawie Storm w obszarze okładce hello. Witaj .NET i JVM komunikują się za pośrednictwem lokalnego gniazda TCP. Zasadniczo każdego Spout/Bolt jest para procesu .net/Java, gdzie hello logikę użytkownika działa w procesie .net jako dodatek.

toobuild danych przetwarzania aplikacji na punkt połączenia usługi, kilka czynności:

* Projektowania i implementacji hello elementach Spout toopull danych z kolejki.
* Projektowanie i implementowanie tooprocess elementów Bolt hello danych wejściowych i Zapisz dane są przechowywane tooexternal, takie jak bazy danych.
* Projektowanie topologii hello, przesyłania, a następnie uruchom hello topologii. Witaj topologii definiuje wierzchołki i hello dane między hello wierzchołków. Punkt połączenia usługi otrzymuje hello topologii specyfikacji i wdrożyć ją na klaster Storm, w którym każdy wierzchołek jest uruchamiany w jednym węźle logiczne. Hello trybu failover i skalowanie będzie można wybrać ofertę z przez harmonogram zadań hello Storm.

Ten dokument będzie używać niektórych toowalk proste przykłady za pośrednictwem jak toobuild przetwarzania danych aplikacji przy użyciu połączenia usługi.

## <a name="scp-plugin-interface"></a>Interfejs wtyczki punkt połączenia usługi
Wtyczki punkt połączenia usługi (lub aplikacji) są autonomiczne plików exe, które można jednocześnie uruchomić w programie Visual Studio w fazie programowanie hello i być podłączane do potoku Storm powitania po wdrożeniu w środowisku produkcyjnym. Pisanie wtyczki hello punkt połączenia usługi jest po prostu hello taki sam jak zapisywania wszelkich innych standardowych aplikacji systemu Windows konsoli. Platforma SCP.NET deklaruje niektórych interfejs dla spout/bolt, i kod wtyczki użytkownika hello należy zaimplementować te interfejsy. głównym celem Hello ten projekt jest ten użytkownik hello można skupić się na ich własnych warunki biznesowe logiczne i pozostawienie toobe innych elementów, obsługiwane przez platformę SCP.NET.

Kod wtyczki użytkownika Hello powinny implementować jeden hello następujących typów interfejsów, zależy od tego, czy topologia hello jest transakcyjna lub nietransakcyjna i określa, czy składnik hello jest spout lub bolt.

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin jest hello wspólny interfejs dla wszystkich rodzajów wtyczek. Obecnie jest interfejsem zastępczego.

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout jest interfejs hello spout nietransakcyjnej.

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

Gdy `NextTuple()` jest nazywany hello C\# jeden lub więcej krotek można emitowanie kodu użytkownika. Jeśli nie ma nic tooemit, ta metoda powinna zwrócić bez emitowanie żadnych czynności. Należy zauważyć, że `NextTuple()`, `Ack()`, i `Fail()` są wszystkie wywoływane w pętli ścisłej w jednym wątku w języku C\# procesu. Jeśli nie ma żadnych tooemit krotek, jest uśpienia NextTuple uprzejmy toohave do krótkim czasie (na przykład 10 ms) tak, jak nie toowaste zbyt dużo Procesora.

`Ack()`i `Fail()` można wywołać tylko wtedy, gdy mechanizmu potwierdzenia jest włączone w specyfikacji pliku. Witaj `seqId` jest używane tooidentify spójnej kolekcji hello prześledzone lub nie powiodło się. Dlatego po włączeniu potwierdzenia w topologii nietransakcyjnej powitania po emitowanie funkcji powinny być używane w Spout:

    public abstract void Emit(string streamId, List<object> values, long seqId); 

Jeśli potwierdzenie nie jest obsługiwany w topologii nietransakcyjnej, hello `Ack()` i `Fail()` może pozostać puste funkcji.

Witaj `parms` parametry wejściowe w te funkcje są po prostu pusty słownik, są one zarezerwowane do użytku w przyszłości.

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt jest interfejs hello bolt nietransakcyjnej.

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

Po udostępnieniu nowej krotki hello `Execute()` funkcji zostanie wywołana tooprocess go.

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout jest interfejs hello spout transakcyjnych.

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

Podobnie jak ich nietransakcyjnej zaradczych strony `NextTx()`, `Ack()`, i `Fail()` są wszystkie wywoływane w pętli ścisłej w jednym wątku w języku C\# procesu. Jeśli nie ma żadnych tooemit danych, jest uprzejmy toohave `NextTx` uśpienia przez krótki czas (10 ms), nie toowaste zbyt dużo Procesora.

`NextTx()`jest nazywany toostart nowej transakcji, hello parametru out `seqId` jest używane tooidentify hello transakcję, która jest również używana w `Ack()` i `Fail()`. W `NextTx()`, użytkownik może emitować po stronie tooJava danych. Witaj danych będą przechowywane w dozorcy toosupport powtarzania. Ponieważ hello pojemność dozorcy jest bardzo ograniczona, użytkownika powinien tylko Emituj metadane, nie zbiorczego danych w spout transakcyjnych.

STORM będzie odtwarzana w transakcji automatycznie w przypadku niepowodzenia to `Fail()` nie powinna być wywoływana w przypadku normalnych. Ale jeśli punkt połączenia usługi można sprawdzić metadanych hello emitowane przez transakcyjne spout, może wywołać `Fail()` Jeśli hello metadanych jest nieprawidłowy.

Witaj `parms` parametry wejściowe w te funkcje są po prostu pusty słownik, są one zarezerwowane do użytku w przyszłości.

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt jest interfejsem powitania dla transakcyjnego bolt.

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`jest wywoływana po nowej krotki otrzymywanych hello bolt. `FinishBatch()`jest wywoływana po zakończeniu tej transakcji. Witaj `parms` parametru wejściowego jest zarezerwowany do użytku w przyszłości.

Topologia transakcyjne jest ważne pojęcia — `StormTxAttempt`. Składa się z dwóch pól `TxId` i `AttemptId`. `TxId`jest używana tooidentify określonej transakcji, a dla danej transakcji, może mieć wielu prób transakcji hello kończy się niepowodzeniem i jest odtwarzany. SCP.NET nowych będzie inny ISCPBatchBolt obiektu tooprocess każdego `StormTxAttempt`, po prostu jak czego Storm w języku Java po stronie. Celem Hello ten projekt jest toosupport przetwarzania transakcji równoległych. Użytkownika należy go przechowywać w uwadze który jeśli próba transakcji zostało zakończone, odpowiedni obiekt ISCPBatchBolt hello zostaną zniszczone i w ramach odzyskiwania pamięci.

## <a name="object-model"></a>Model obiektu
SCP.NET udostępnia prosty zestaw obiektów kluczy dla deweloperów tooprogram z. Są one **kontekstu**, **stan klientów**, i **SCPRuntime**. Będą one omówione w hello pozostałej części tej sekcji.

### <a name="context"></a>Kontekst
Kontekst udostępnia działającej aplikacji toohello środowiska. Każde wystąpienie ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) ma odpowiednie wystąpienia kontekstu. Hello funkcje udostępniane przez kontekst można podzielić na dwie części: statycznej części hello (1), który jest dostępny w hello całego C\# przetworzyć strony dynamicznej hello (2), który jest dostępny tylko dla określonego wystąpienia kontekstu hello.

### <a name="static-part"></a>Statycznej części
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger`podano w celu dziennika.

`pluginType`jest używany typ wtyczki hello tooindicate hello C\# procesu. Jeśli hello C\# proces jest uruchomiony w trybie lokalnym testu (bez Java), typ wtyczki hello jest `SCP_NET_LOCAL`.

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`podano tooget parametry konfiguracji po stronie Java. Witaj parametry są przekazywane z Java strony po C\# dodatek został zainicjowany. Witaj `Config` parametry są podzielone na dwie części: `stormConf` i `pluginConf`.

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`jest parametrów zdefiniowanych Storm i `pluginConf` jest hello parametrów zdefiniowanych przez punkt połączenia usługi. Na przykład:

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`są podane w kontekście topologii tooget hello jest najbardziej przydatny w przypadku składników z wielu równoległości. Oto przykład:

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a>Części dynamicznej
Witaj następujące interfejsy są istotne tooa niektórych wystąpienia kontekstu. wystąpienie kontekstu Hello jest tworzony przez platformę SCP.NET i przekazany kod użytkownika toohello:

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

Do obsługi potwierdzenia nietransakcyjnej spout podano hello następujące metody:

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

Dla obsługi potwierdzenia nietransakcyjnej bolt, należy go jawnie `Ack()` lub `Fail()` hello odebrała spójnej kolekcji. I podczas emitowania nowe spójnej kolekcji, należy także określić kotwice hello z hello nowej krotki. podano Hello następujące metody.

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>Stan klientów
`StateStore`udostępnia usługi metadanych, generowanie monotoniczna sekwencji i koordynacji bez oczekiwania. Abstrakcje wyższego poziomu współbieżności rozproszonej mogą być wbudowane w `StateStore`, w tym rozproszonej blokad, kolejek rozproszonych bariery i transakcji usługi.

Punkt połączenia usługi, aplikacje mogą używać hello `State` obiekt toopersist niektóre informacje w dozorcy, szczególnie w przypadku topologii transakcyjnych. Wykonywanie, dzięki czemu transakcyjne spout ulegnie awarii, uruchom ponownie może pobrać hello niezbędne informacje z dozorcy i uruchom ponownie hello potoku.

Witaj `StateStore` obiekt ma głównie tych metod:

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

Witaj `State` obiekt ma głównie tych metod:

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

Dla hello `Commit()` metody, gdy simpleMode ustawiono tootrue, po prostu usunie hello odpowiadającego ZNode w dozorcy. W przeciwnym razie spowoduje usunięcie hello bieżącego ZNode i dodanie nowego węzła w hello zatwierdzone\_ścieżki.

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime zapewnia hello następujących dwóch metod.

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`to środowisko uruchomieniowe hello SCP tooinitialize używane. W przypadku tej metody hello C\# procesu połączy toohello stronie Java i pobiera parametry konfiguracji i topologii kontekstu.

`LaunchPlugin()`jest używana tookick poza wiadomość hello przetwarzanie pętli. W tym pętli hello C\# wtyczki będą otrzymywać wiadomości formularza po stronie Java (w tym sygnały krotek i sterowania), a następnie podaj wiadomości powitania procesu, prawdopodobnie podczas wywoływania metody interfejsu hello przez kod użytkownika hello. wejściowy parametr metody Hello `LaunchPlugin()` jest delegata, który może zwracać obiekt, który implementuje interfejs ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

Dla ISCPBatchBolt, można pobrać `StormTxAttempt` z `parms`i przy jego użyciu toojudge czy jest próba powtórzony. Zwykle odbywa się na powitania zatwierdzania bolt i zostało to przedstawione w hello `HelloWorldTx` przykład.

Ogólnie rzecz biorąc hello wtyczek SCP może działać w dwóch trybach tutaj:

1. Tryb lokalnego testu: W tym trybie hello wtyczek punkt połączenia usługi (hello C\# kod użytkownika) uruchom w programie Visual Studio w fazie programowanie hello. `LocalContext`można w tym trybie, co zapewnia metody tooserialize hello wysyłanego krotek toolocal pliki i utworzyć ich kopię toomemory odczytu.
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. Tryb regularnych: W tym trybie wtyczek SCP hello będą uruchamiane przez proces java storm.
   
    Oto przykład uruchamiania SCP wtyczki:
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a>Topologia specyfikacja języka
Specyfikacja topologii punkt połączenia usługi jest domeny określonego języka dla zawierająca opis i Konfigurowanie topologii punkt połączenia usługi. Jest on oparty na jego Storm Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) i zostanie rozszerzony przez punkt połączenia usługi.

Specyfikacje topologii można przesłać bezpośrednio toostorm klastra wykonywania za pośrednictwem hello ***runspec*** polecenia.

SCP.NET ma Dodaj następujące funkcje toodefine hello transakcyjne topologii:

| **Nowe funkcje** | **Parametry** | **Opis** |
| --- | --- | --- |
| **TX topolopy** |Nazwa topologii<br />spout mapy<br />bolt mapy |Zdefiniuj transakcyjne topologii o nazwie topologii hello, &nbsp;spouts mapy definicji i hello elementów bolt definicji mapy |
| **spout-tx — punkt połączenia usługi** |exec — nazwa<br />argumentów<br />Pola |Zdefiniuj spout transakcyjnych. Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów***.<br /><br />Witaj ***pola*** jest hello pól danych wyjściowych dla spout |
| **punkt połączenia usługi tx partii bolt** |exec — nazwa<br />argumentów<br />Pola |Zdefiniuj transakcyjne Bolt partii. Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów.***<br /><br />Witaj pola jest hello pól danych wyjściowych dla bolt. |
| **punkt połączenia usługi tx-commit-bolt** |exec — nazwa<br />argumentów<br />Pola |Zdefiniuj transakcyjne Bolt zatwierdzający. Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów***.<br /><br />Witaj ***pola*** jest hello pól danych wyjściowych dla bolt |
| **nontx topolopy** |Nazwa topologii<br />spout mapy<br />bolt mapy |Zdefiniuj topologię nietransakcyjne o nazwie topologii hello,&nbsp; spouts mapy definicji i hello elementów bolt definicji mapy |
| **spout punkt połączenia usługi** |exec — nazwa<br />argumentów<br />Pola<br />parameters |Zdefiniuj spout nietransakcyjne. Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów***.<br /><br />Witaj ***pola*** jest hello pól danych wyjściowych dla spout<br /><br />Witaj ***parametry*** jest opcjonalny, przy jej użyciu toospecify niektóre parametry, takie jak "nontransactional.ack.enabled". |
| **bolt punkt połączenia usługi** |exec — nazwa<br />argumentów<br />Pola<br />parameters |Zdefiniuj nietransakcyjne Bolt. Zostanie uruchomiony aplikacji hello z ***nazwa exec*** przy użyciu ***argumentów***.<br /><br />Witaj ***pola*** jest hello pól danych wyjściowych dla bolt<br /><br />Witaj ***parametry*** jest opcjonalny, przy jej użyciu toospecify niektóre parametry, takie jak "nontransactional.ack.enabled". |

Wykonaj ma SCP.NET kluczy zdefiniowane słowa:

| **Słowa kluczowe** | **Opis** |
| --- | --- |
| **: Nazwa** |Zdefiniuj hello nazwa topologii |
| **: topologii** |Zdefiniuj hello topologię za pomocą hello powyżej funkcje i kompilacji w tych. |
| **: p** |Zdefiniuj hello równoległości wskazówkę dla każdego spout lub bolt. |
| **: config** |Zdefiniuj skonfigurować parametru lub aktualizacji hello istniejących |
| **: schematu** |Zdefiniuj hello schematu strumienia. |

I często używane parametry:

| **Parametr** | **Opis** |
| --- | --- |
| **"plugin.name"** |Nazwa pliku exe wtyczki hello C# |
| **"plugin.args"** |argumenty wtyczki |
| **"output.schema"** |Schemat danych wyjściowych |
| **"nontransactional.ack.enabled"** |Czy potwierdzenia jest włączone dla topologii nietransakcyjne |

polecenie runspec Hello zostaną wdrożone razem z bitów hello, użycie hello jest podobne:

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

Hello ***zasobów dir*** parametr jest opcjonalny, należy toospecify go, jeśli chcesz tooplug C\# aplikacji, a ten katalog będzie zawierać aplikacji hello hello zależności i konfiguracji.

Witaj ***ścieżki klasy*** parametr również jest opcjonalny. Jeśli plik specyfikacji hello zawiera Java Spout lub Bolt jest klasy Java hello toospecify używane.

## <a name="miscellaneous-features"></a>Różne funkcje
### <a name="input-and-output-schema-declaration"></a>Danych wejściowych i wyjściowych schematu deklaracji
Witaj użytkownika może emitować spójnej kolekcji w języku C\# przetwarzania, hello platformy potrzeb krotki hello tooserialize byte [] stronie tooJava transferu, i Storm będzie przenieść ten cele toohello spójnej kolekcji. W tym samym czasie w składniku podrzędne hello C\# proces będzie otrzymywać krotki powrotem po stronie java i przekształcić ją typów pierwotnego toohello przez platformę, wszystkie czynności są ukryte przez hello platformy.

toosupport hello serializacji i deserializacji kodu użytkownika musi toodeclare hello schemat hello wejścia i wyjścia.

Schemat wejścia/wyjścia strumienia Hello jest zdefiniowany jako słownik, klucz hello jest hello StreamId a hello hello typów kolumn hello. składnik Hello może mieć wielu strumieni zadeklarowany.

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


Obiekt kontekstu mamy hello dodano następujący interfejs API:

    public void DeclareComponentSchema(ComponentStreamSchema schema)

Kod użytkownika, należy się upewnić, krotek hello wysyłanego przestrzegać schematu hello zdefiniowane dla tego strumienia lub hello system zgłosi wyjątek czasu wykonywania.

### <a name="multi-stream-support"></a>Obsługa wielu strumienia
Użytkownika obsługuje SCP kodu tooemit lub odebrać z wielu różnych strumieni na powitania sam czas. Obsługa Hello odzwierciedla w obiekt kontekstu hello jako hello emitowanie metoda przyjmuje parametr ID opcjonalne strumienia.

Dodano dwie metody w hello obiekt SCP.NET kontekstu. Są one używane tooemit spójnej kolekcji lub krotek toospecify StreamId. Hello StreamId jest ciągiem i musi on toobe spójne w obu C\# i hello specyfikacji definicji topologii.

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

wyjątki czasu wykonywania spowoduje, że Hello emisji tooa nieistniejącego strumienia.

### <a name="fields-grouping"></a>Grupowanie pól
Witaj w kompilacji Grupowanie pól w Strom nie działa prawidłowo w SCP.NET. Na powitania po stronie serwera Proxy Java wszystkie typy danych pola hello są faktycznie byte [], a pola hello grupowanie używa hello byte [] obiektu skrótu kodu tooperform hello grupowania. Witaj byte [] obiektu skrótu jest adresem hello tego obiektu w pamięci. Dzięki grupowania hello będą nieprawidłowe dla dwóch bajtów [] obiektów hello tego udziału, same zawartości, ale nie hello tego samego adresu.

SCP.NET dodaje metodę grupowania dostosowane, i użyje zawartości hello hello byte [] toodo hello grupowania. W **SPEC** pliku przypomina hello składni:

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


Tutaj

1. "punkt połączenia usługi pola group" oznacza "Grupowania pola niestandardowe implementowane przez punkt połączenia usługi".
2. ": tx"lub":-tx" oznacza, że jeśli jest transakcyjna topologii. Potrzebujemy tych informacji, ponieważ hello początkowy indeks jest inna w tx a topologie-tx.
3. zestaw hashset identyfikatory pola, począwszy od 0 oznacza [0,1].

### <a name="hybrid-topology"></a>Topologia hybrydowego
natywny Hello Storm są zapisywane w języku Java. I SCP.Net rozszerzonego, jego tooenable naszych toowrite celne C\# kodu toohandle ich logiki biznesowej. Obsługujemy również hybrydowe topologie, która zawiera nie tylko C, ale\# elementów elementach spout/bolt, ale również elementów Java Spout/Bolt.

### <a name="specify-java-spoutbolt-in-spec-file"></a>Określ Java Spout/Bolt w specyfikacji pliku
W specyfikacji pliku "punkt połączenia usługi spout" i "punkt połączenia usługi bolt" można też Spouts Java toospecify używane i elementów Bolt, Oto przykład:

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

W tym miejscu `microsoft.scp.example.HybridTopology.Generator` jest nazwą hello hello Klasa Java Spout.

### <a name="specify-java-classpath-in-runspec-command"></a>Określ klasy Java w runSpec polecenia
Chcąc topologii toosubmit zawierające Java Spouts lub elementów Bolt, wymaga hello kompilacji toofirst Java Spouts lub elementów Bolt i Pobierz pliki Jar hello. Następnie należy określić klasy java hello, który zawiera pliki Jar hello podczas przesyłania topologii. Oto przykład:

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

W tym miejscu **przykłady\\HybridTopology\\java\\docelowej\\**  jest hello folder zawierający plik Jar Spout/Bolt Java hello.

### <a name="serialization-and-deserialization-between-java-and-c"></a>Serializacja i deserializacja między Java i C\
Nasze składnik SCP zawiera stronie Java i C\# po stronie. W kolejności toointeract z macierzystego Java elementach Spout/elementów Bolt, serializacji/deserializacji przeprowadza się między stronie Java i C\# po stronie, jak pokazano na powitania po wykresu.

![Diagram składnika java wysyłania składnika tooSCP wysyłania tooJava składnika](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Serializacja w stronie Java i deserializacji w języku C\# po stronie**
   
   Najpierw firma Microsoft udostępnia domyślną implementację do serializacji w języku Java po stronie i deserializacji w języku C\# po stronie. Witaj metoda serializacji w języku Java po stronie można określić w specyfikacji pliku:
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   Witaj metody deserializacji w języku C\# po stronie powinny być określone w języku C\# kod użytkownika:
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   Ta domyślna implementacja powinna obsługiwać większości przypadków, jeśli hello — typ danych nie jest zbyt złożony. W niektórych przypadkach albo ponieważ hello typie danych użytkownika jest zbyt złożony lub hello wydajności naszych Domyślna implementacja nie spełnia hello wymaganie użytkownika, użytkownik może wtyczki realizacji.
   
   Witaj serializować interfejsu w języku java po stronie jest zdefiniowany jako:
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   Witaj deserializacji interfejsu w języku C\# po stronie jest zdefiniowany jako:
   
   Interfejs publiczny ICustomizedInteropCSharpDeserializer
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **Serializacji w języku C\# po stronie i deserializacji w języku Java obok siebie**
   
   Witaj, metoda serializacji w języku C\# po stronie powinny być określone w języku C\# kod użytkownika:
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   Witaj metody deserializacji po stronie Java powinny być określone w specyfikacji pliku:
   
     (punkt połączenia usługi spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   Tutaj "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" jest nazwą hello Deserializator i "microsoft.scp.example.HybridTopology.Person" oznacza dane hello klasy docelowej hello jest deserializacji do.
   
   Użytkownik może również wtyczki realizacji c\# serializator i Deserializator Java. Jest to interfejs hello C\# serializator:
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   Jest to interfejs hello Deserializator Java:
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>Tryb punktu połączenia usługi hosta
W tym trybie użytkownika można skompilować tooDLL ich kody i korzystać SCPHost.exe dostarczonych przez punkt połączenia usługi toosubmit topologii. Witaj specyfikacji pliku wygląda następująco:

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

W tym miejscu `plugin.name` jest określony jako `SCPHost.exe` dostarczonych przez punkt połączenia usługi SDK. SCPHost.exe akceptującego dokładnie trzy parametry:

1. Witaj najpierw jeden jest hello nazwy biblioteki DLL, która jest `"HelloWorld.dll"` w tym przykładzie.
2. Witaj drugim jest hello nazwy klasy, która jest `"Scp.App.HelloWorld.Generator"` w tym przykładzie.
3. Witaj innej jedną jest hello nazwa publicznej metody statycznej, który może być wywołana tooget wystąpienia ISCPPlugin.

W trybie hosta kod użytkownika jest skompilowana jako biblioteki DLL i jest wywoływane przez platformę punkt połączenia usługi. Dlatego platformy punkt połączenia usługi można uzyskać pełną kontrolę nad hello całego przetwarzania logiki. Dlatego zalecamy naszych klientów toosubmit topologii w trybie hosta SCP ponieważ można uprościć środowisko programistyczne hello i przełączyć nam większą elastyczność i lepszą zgodność z poprzednimi wersjami oraz nowszych wersji.

## <a name="scp-programming-examples"></a>Przykłady programowania w języku punkt połączenia usługi
### <a name="helloworld"></a>HelloWorld
**HelloWorld** jest tooshow bardzo prosty przykład smak SCP.Net. Za pomocą topologii nietransakcyjnej i spout, nazywany **generator**i dwóch elementów bolt o nazwie **podziału** i **licznika**. Hello spout **generator** losowo spowoduje wygenerowanie zdań niektóre i wyemitować tych zdań zbyt**podziału**. Hello bolt **podziału** będzie podzielić toowords zdań hello i zbyt Emituj te słowa**licznika** bolt. Witaj bolt "licznika" używa wielu wystąpienie słownika toorecord hello każdego wyrazu.

Istnieją dwa pliki specyfikacji, **HelloWorld.spec** i **HelloWorld\_EnableAck.spec** w tym przykładzie. W hello C\# kodu, go można ustalić, czy potwierdzenia jest włączona pobierając hello pluginConf z strony Java.

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

Po włączeniu potwierdzenia w hello spout słownik jest używane toocache hello krotek, które nie zostały jeszcze prześledzone. Jeśli po wywołaniu Fail() hello krotki nie powiodło się zostaną odtworzone:

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a>HelloWorldTx
Witaj **HelloWorldTx** przykładzie pokazano, jak tooimplement transakcyjnych topologii. Ma on jeden spout o nazwie **generator**, partii elementów bolt o nazwie **partial-count**, i wywołuje bolt zatwierdzania **Suma liczba**. Istnieją również trzy pliki txt wstępnie utworzone: **DataSource0.txt**, **DataSource1.txt** i **DataSource2.txt**.

W każdej transakcji hello spout **generator** będzie losowo wybierz dwa pliki z hello wstępnie utworzone trzy pliki i emisji toohello nazwy pliku hello dwa **partial-count** bolt. Hello bolt **partial-count** najpierw pobrać nazwy pliku hello hello Odebrano spójnej kolekcji, a następnie otwórz hello plików i liczba hello liczbę słów w tym pliku, a ostatecznie Emituj toohello numer word hello **Suma liczba**bolt. Witaj **Suma liczba** bolt podsumowanie hello łączna liczba.

tooachieve **dokładnie raz** semantyki, hello zatwierdzania bolt **Suma liczba** muszą toojudge, czy jest powtórzonym transakcji. W tym przykładzie ma statycznym elementem członkowskim zmiennej:

    public static long lastCommittedTxId = -1; 

Po utworzeniu wystąpienia ISCPBatchBolt pobierze hello `txAttempt` z parametrów wejściowych:

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

Gdy `FinishBatch()` po wywołaniu hello `lastCommittedTxId` będzie aktualizacji, jeśli nie jest transakcją powtórzony.

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a>HybridTopology
Ta topologia zawiera elementów Spout Java i C\# Bolt. Używa ona hello domyślnej serializacji i deserializacji implementacji dostarczonych przez punkt połączenia usługi platformy. Użyj ref hello **HybridTopology.spec** w **przykłady\\HybridTopology** folder szczegółów specyfikacji pliku hello, i **SubmitTopology.bat** jak klasy Java toospecify.

### <a name="scphostdemo"></a>SCPHostDemo
W tym przykładzie jest hello taki sam jak HelloWorld w zasadzie. Witaj tylko różnica polega na kod użytkownika hello jest skompilowana jako biblioteki DLL, a topologia hello jest przesyłany za pomocą SCPHost.exe. Aby uzyskać dokładniejsze objaśnienie, zapoznaj się z sekcji hello ref "Punkt połączenia usługi hosta tryb".

## <a name="next-steps"></a>Następne kroki
Przykłady topologii Storm utworzone przy użyciu połączenia usługi zobacz następujące hello:

* [Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [Tworzenie wielu strumieni danych w topologii Storm C#](hdinsight-storm-twitter-trending.md)
* [Użyj usługi Power Bi toovisualize danych od topologii Storm](hdinsight-storm-power-bi-topology.md)
* [Przetwarzania danych czujnika vehicle z usługi Event Hubs za pomocą Storm w usłudze HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [Wyodrębniania, przekształcania i ładowania (ETL) z usługi Azure Event Hubs tooHBase](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [Korelowanie zdarzeń za pomocą Storm i bazy danych HBase w usłudze HDInsight](hdinsight-storm-correlation-topology.md)

