---
title: "zdarzenia aaaProcess z centrów zdarzeń z systemu Storm - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprocess dane z usługi Azure Event Hubs w topologii Storm C# utworzone w programie Visual Studio przy użyciu hello narzędzi HDInsight tools dla programu Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>Zdarzenia procesu z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (C#)

Dowiedz się, jak toowork z usługą Azure Event Hubs z systemu Apache Storm w usłudze HDInsight. Ten dokument używa C# Storm topologii tooread i zapisu danych z centrów Evbent

> [!NOTE]
> Wersja języka Java tego projektu, dla [przetwarzać zdarzeń z usługi Azure Event Hubs z systemu Storm w usłudze HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="scpnet"></a>SCP.NET

kroki Hello w tym dokumencie Użyj SCP.NET, pakietu NuGet, który ułatwia topologie łatwe toocreate C# i składniki do użycia z systemu Storm w usłudze HDInsight.

> [!IMPORTANT]
> Gdy hello kroków w tym dokumencie zależą od środowiska projektowego systemu Windows w programie Visual Studio, hello skompilowany projekt może być przesłane tooa Storm w klastrze usługi HDInsight, który używa systemu Linux. Topologie SCP.NET obsługują tylko opartych na systemie Linux klastrów utworzonych po 28 października 2016 roku.

HDInsight 3.4 i większa topologie Mono toorun C# Użyj. przykład Witaj używane w tym dokumencie współpracuje z 3,6 HDInsight. Jeśli planujesz tworzenie własnych rozwiązań .NET dla usługi HDInsight, sprawdź hello [Mono zgodności](http://www.mono-project.com/docs/about-mono/compatibility/) dokument dla potencjalnych niezgodności.

### <a name="cluster-versioning"></a>Przechowywanie wersji klastra

Witaj używanego dla projektu pakietu Microsoft.SCP.Net.SDK NuGet musi odpowiadać wersji głównych hello Storm zainstalowany w usłudze HDInsight. HDInsight w wersji 3.5 i 3,6 używać systemu Storm 1.x, dlatego należy użyć 1.0.x.x wersji SCP.NET z tych klastrach.

> [!IMPORTANT]
> przykład Witaj w tym dokumencie oczekuje HDInsight w wersji 3.5 lub 3,6 klastra.
>
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

Topologie języka C# muszą również wskazywać .NET 4.5.

## <a name="how-toowork-with-event-hubs"></a>Jak toowork z usługą Event Hubs

Firma Microsoft udostępnia zestaw składników Java, które mogą być używane toocommunicate z usługą Event Hubs od topologii Storm. Można znaleźć pliku archiwum (JAR) Java hello, który zawiera 3,6 HDInsight zgodna wersja tych składników na [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

> [!IMPORTANT]
> Gdy składniki hello są napisane w języku Java, łatwo można je od topologii C#.

następujące składniki Hello są używane w tym przykładzie:

* __EventHubSpout__: odczytuje dane z usługi Event Hubs.
* __EventHubBolt__: zapisuje dane tooEvent koncentratorów.
* __EventHubSpoutConfig__: tooconfigure EventHubSpout używane.
* __EventHubBoltConfig__: tooconfigure EventHubBolt używane.

### <a name="example-spout-usage"></a>Przykład użycia spout

SCP.NET udostępnia metody do dodawania EventHubSpout tooyour topologii. Te metody umożliwiają łatwiejsze tooadd spout niż przy użyciu metody rodzajowe hello do dodawania składnika Java. Witaj poniższym przykładzie pokazano, jak hello toocreate spout za pomocą __SetEventHubSpout__ i **EventHubSpoutConfig** metody udostępniane przez SCP.NET:

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

Witaj w poprzednim przykładzie tworzy nowy składnik spout o nazwie __EventHubSpout__i skonfiguruje je toocommunicate z Centrum zdarzeń. Wskazówka równoległości Hello składnika hello jest ustawiana toohello liczby partycji w Centrum zdarzeń hello. To ustawienie umożliwia Storm toocreate wystąpienia składnika powitania dla każdej partycji.

### <a name="example-bolt-usage"></a>Przykład użycia bolt

Użyj hello **JavaComponmentConstructor** toocreate metody wystąpienia hello bolt. Witaj poniższym przykładzie pokazano, jak toocreate i skonfiguruj nowe wystąpienie klasy hello **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> W tym przykładzie użyto wyrażenia Clojure przekazany jako ciąg, zamiast **JavaComponentConstructor** toocreate **EventHubBoltConfig**, tak jak na przykład Witaj spout. Każda metoda działa. Użyj metody hello tak najlepsze tooyou.

## <a name="download-hello-completed-project"></a>Pobierz ukończyć powitalnych projektu

Możesz pobrać pełną wersję utworzonego w ramach tego samouczka z projektu hello [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub). Jednak nadal potrzebujesz tooprovide ustawienia konfiguracji, wykonując kroki hello w tym samouczku.

### <a name="prerequisites"></a>Wymagania wstępne

* [Systemu Apache Storm w klastrze usługi HDInsight w wersji 3.5 lub 3,6](hdinsight-apache-storm-tutorial-get-started.md).

    > [!WARNING]
    > przykład Witaj używane w tym dokumencie wymaga Storm w usłudze HDInsight w wersji 3.5 lub 3,6. Nie działa ze starszymi wersjami usługi hdinsight, zmiany nazwy klasy toobreaking ukończenia. Wersja tego przykładu, która współdziała z klastrami starsze, dla [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).

* [Centrum zdarzeń Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* Witaj [zestawu Azure .NET SDK](http://azure.microsoft.com/downloads/).

* Witaj [narzędzia HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Java JDK 1.8 lub nowszego środowiska deweloperskiego. Pobieranie JDK są dostępne z [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

  * Witaj **JAVA_HOME** środowiska zmiennej musi toohello punktu katalog, który zawiera Java.
  * Witaj **%JAVA_HOME%/bin** katalog musi znajdować się w ścieżce hello.

## <a name="download-hello-event-hubs-components"></a>Pobierz hello składniki usługi Event Hubs

Hello pobierania centrów zdarzeń spout i zablokowanie składnika z [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

Utwórz katalog o nazwie `eventhubspout`i Zapisz plik hello do katalogu hello.

## <a name="configure-event-hubs"></a>Konfigurowanie usługi Event Hubs

Centra zdarzeń to hello źródła danych w tym przykładzie. Użyj informacji hello w sekcji "Tworzenie Centrum zdarzeń" hello z [Rozpoczynanie pracy z usługą Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

1. Po utworzeniu Centrum zdarzeń hello wyświetlić hello **EventHub** bloku w hello Azure portalu i wybierz pozycję **zasady dostępu współużytkowanego**. Wybierz **+ Dodaj** hello tooadd następujące zasady:

   | Nazwa | Uprawnienia |
   | --- | --- |
   | Składnik zapisywania |Send |
   | Czytnik |Nasłuchiwanie |

    ![Zrzut ekranu udziału dostępu zasady okna](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. Wybierz hello **czytnika** i **zapisywania** zasad. Skopiuj i Zapisz hello wartość klucza podstawowego dla obu zasad, jak te wartości są używane później.

## <a name="configure-hello-eventhubwriter"></a>Skonfiguruj hello EventHubWriter

1. Jeśli hello najnowszą wersję narzędzi HDInsight hello nie jest już zainstalowany dla programu Visual Studio, zobacz [rozpocząć korzystanie z narzędzia HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Pobierz hello rozwiązania z [eventhub storm hybrydowy](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

3. W hello **EventHubWriter** projektu, otwórz hello **App.config** pliku. Użyj informacji hello z Centrum zdarzeń hello skonfigurowane wcześniej toofill hello wartości hello następujące klucze:

   | Klucz | Wartość |
   | --- | --- |
   | EventHubPolicyName |Moduł zapisujący (jeśli użyto inną nazwę dla zasad hello o *wysyłania* uprawnień, zamiast tego użyj.) |
   | EventHubPolicyKey |klucz Hello hello zapisywania zasad. |
   | EventHubNamespace |Witaj przestrzeni nazw, która zawiera Centrum zdarzeń. |
   | EventHubName |Nazwę Centrum zdarzeń. |
   | EventHubPartitionCount |Witaj liczbę partycji w Centrum zdarzeń. |

4. Zapisz i zamknij hello **App.config** pliku.

## <a name="configure-hello-eventhubreader"></a>Skonfiguruj hello EventHubReader

1. Otwórz hello **EventHubReader** projektu.

2. Otwórz hello **App.config** pliku hello **EventHubReader**. Użyj informacji hello z Centrum zdarzeń hello skonfigurowane wcześniej toofill hello wartości hello następujące klucze:

   | Klucz | Wartość |
   | --- | --- |
   | EventHubPolicyName |Czytnik (Jeśli używasz inną nazwę dla zasad hello o *nasłuchiwania* uprawnień, zamiast tego użyj.) |
   | EventHubPolicyKey |klucz Hello hello czytnika zasad. |
   | EventHubNamespace |Witaj przestrzeni nazw, która zawiera Centrum zdarzeń. |
   | EventHubName |Nazwę Centrum zdarzeń. |
   | EventHubPartitionCount |Witaj liczbę partycji w Centrum zdarzeń. |

3. Zapisz i zamknij hello **App.config** pliku.

## <a name="deploy-hello-topologies"></a>Wdrażanie topologii hello

1. Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **EventHubReader** projekt i wybierz **przesłać tooStorm w usłudze HDInsight**.

    ![Zrzut ekranu z Eksplorator rozwiązań z tooStorm przesyłania w usłudze HDInsight wyróżnione](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. Na powitania **przesyłania topologii** okno dialogowe, wybierz użytkownika **klaster Storm**. Rozwiń węzeł **dodatkowe konfiguracje**, wybierz pozycję **ścieżki plików Java**, wybierz pozycję **...** i hello wybierz katalog, który zawiera plik JAR hello pobranego wcześniej. Na koniec kliknij **przesyłania**.

    ![Zrzut ekranu przedstawia topologię — okno dialogowe](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. Po przesłaniu topologii hello hello **podglądu topologii Storm** pojawi się. tooview informacji o topologii hello, wybierz hello **EventHubReader** topologię. w okienku po lewej stronie powitania.

    ![Zrzut ekranu przedstawiający podgląd topologie Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. Z **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **EventHubWriter** projekt i wybierz **przesłać tooStorm w usłudze HDInsight**.

5. Na powitania **przesyłania topologii** okno dialogowe, wybierz użytkownika **klaster Storm**. Rozwiń węzeł **dodatkowe konfiguracje**, wybierz pozycję **ścieżki plików Java**, wybierz pozycję **...** , i hello wybierz katalog, który zawiera plik JAR hello pobranego wcześniej. Na koniec kliknij **przesyłania**.

6. Po przesłaniu hello topologii, Odśwież listę topologii hello w hello **podglądu topologii Storm** tooverify obu topologiach uruchomionych w klastrze hello.

7. W **podglądu topologii Storm**, wybierz pozycję hello **EventHubReader** topologii.

8. Podsumowanie hello bolt składnika hello tooopen kliknij dwukrotnie hello **LogBolt** składnika hello diagramie.

9. W hello **modułów** sekcji, wybierz jeden z linków hello hello **portu** kolumny. Spowoduje to wyświetlenie informacji zarejestrowanych przez składnik hello. informacje o Hello rejestrowane są podobne toohello następującego tekstu:

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>Zatrzymywanie topologii hello

topologie hello toostop, wybierz każdej topologii w hello **podglądu topologii Storm**, następnie kliknij przycisk **Kill**.

![Zrzut ekranu z Storm topologii podglądu, z wyróżnionym przyciskiem Kill](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Usuwanie klastra

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Następne kroki

W tym dokumencie uzyskanych jak toouse hello Java centra zdarzeń spout i zablokowanie z toowork topologii C#, w danych w usłudze Azure Event Hubs. toolearn więcej informacji na temat tworzenia topologie języka C#, zobacz następujące hello:

* [Tworzenie topologii C# dla Apache Storm w usłudze HDInsight przy użyciu programu Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Podręcznik programowania punkt połączenia usługi](hdinsight-storm-scp-programming-guide.md)
* [Przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md)
