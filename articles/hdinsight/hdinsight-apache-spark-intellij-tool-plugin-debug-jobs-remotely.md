---
title: "aaaAzure Toolkit for IntelliJ — aplikacje debugowania zdalnego na Spark w usłudze HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak za pomocą narzędzi HDInsight w zestawie narzędzi Azure dla aplikacji debugowania tooremotely IntelliJ uruchamianych w klastrach HDInsight Spark za pośrednictwem sieci vpn."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 55fb454f-c7dc-46de-a978-e242e9a94f4c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ad67d23bf609d0a7afb38b2acb110062f8b27b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toodebug-applications-remotely-on-hdinsight-spark-through-vpn"></a>Użyj zestawu narzędzi platformy Azure dla aplikacji toodebug IntelliJ zdalnie w HDInsight Spark za pośrednictwem sieci VPN

Firma Microsoft zaleca sposób hello debugowania applicaltion spark zdalnie za pomocą ssh. Aby uzyskać instrukcje, zobacz [zdalne debugowanie aplikacji Spark w klastrze usługi HDInsight narzędzi Azure for IntelliJ za pośrednictwem protokołu SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

Ten artykuł zawiera wskazówki krok po kroku, jak toouse hello narzędzi HDInsight Tools w zestawie narzędzi Azure dla toosubmit IntelliJ zadania Spark w klastrze Spark w usłudze HDInsight i następnie Debuguj go zdalnie z komputera stacjonarnego. toodo tak, należy wykonać następujące kroki wysokiego poziomu hello:

1. Tworzenie sieci wirtualnej platformy Azure do lokacji lub punkt lokacja. kroki Hello w tym dokumencie Załóżmy, że sieć lokacja lokacja.
2. Tworzenie klastra Spark w usłudze Azure HDInsight, który jest częścią hello lokacja lokacja sieci wirtualnej platformy Azure.
3. Sprawdź łączność hello między hello headnode klastra i pulpitu.
4. Tworzenie aplikacji Scala w IntelliJ IDEA i skonfigurować go na potrzeby debugowania zdalnego.
5. Uruchom i debugowanie aplikacji hello.

## <a name="prerequisites"></a>Wymagania wstępne
* Subskrypcja platformy Azure. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Klaster Apache Spark w usłudze HDInsight. Aby uzyskać instrukcje, zobacz [klastrów utworzyć Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development kit. Możesz zainstalować ją z [tutaj](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* IntelliJ IDEA. W tym artykule używa wersji 2017.1. Możesz zainstalować ją z [tutaj](https://www.jetbrains.com/idea/download/).
* Narzędzia HDInsight Tools w Azure Toolkit for IntelliJ. Narzędzia HDInsight tools for IntelliJ są dostępne jako część hello Azure Toolkit for IntelliJ. Aby uzyskać instrukcje dotyczące sposobu tooinstall hello Azure zestawu narzędzi, zobacz [hello Instalowanie narzędzi Azure dla IntelliJ](../azure-toolkit-for-intellij-installation.md).
* Zaloguj się do Twojej subskrypcji platformy Azure z rozwiązaniem IntelliJ IDEA. Postępuj zgodnie z instrukcjami hello [tutaj](hdinsight-apache-spark-intellij-tool-plugin.md).
* Podczas uruchamiania aplikacji Spark Scala do zdalnego debugowania na komputerze z systemem Windows, może spowodować wyjątek, zgodnie z objaśnieniem w [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356) występuje powodu Brak tooa WinUtils.exe w systemie Windows. toowork uniknąć tego błędu, należy najpierw [Pobierz hello pliku wykonywalnego w tym miejscu](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa lokalizacji, takich jak **C:\WinUtils\bin**. Następnie należy dodać zmienną środowiskową **HADOOP_HOME** i ustaw wartość hello zmiennej hello zbyt**C\WinUtils**.

## <a name="step-1-create-an-azure-virtual-network"></a>Krok 1: Tworzenie sieci wirtualnej platformy Azure
Wykonaj instrukcje hello z hello poniżej toocreate łącza sieci wirtualnej platformy Azure, a następnie sprawdź łączność hello hello pulpitu i sieci wirtualnej platformy Azure.

* [Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja lokacja przy użyciu portalu Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)
* [Tworzenie sieci wirtualnej za pomocą połączenia sieci VPN lokacja lokacja za pomocą programu PowerShell](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md)
* [Skonfiguruj połączenie punkt lokacja tooa sieć wirtualną przy użyciu programu PowerShell](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)

## <a name="step-2-create-an-hdinsight-spark-cluster"></a>Krok 2: Tworzenie klastra Spark w usłudze HDInsight
Należy również utworzyć klaster Apache Spark w usłudze Azure HDInsight jest częścią hello Azure Virtual Network, który został utworzony. Użyj hello informacji dostępnych w [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md). W ramach konfiguracji opcjonalnej wybierz hello Azure Virtual Network, utworzony w poprzednim kroku hello.

## <a name="step-3-verify-hello-connectivity-between-hello-cluster-headnode-and-your-desktop"></a>Krok 3: Sprawdź łączność hello między hello headnode klastra i pulpitu
1. Pobierz adres IP hello hello headnode. Otwórz interfejs użytkownika narzędzia Ambari hello klastra. W bloku klastra powitania kliknij **pulpitu nawigacyjnego**.

    ![Znajdowanie adresu IP headnode](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/launch-ambari-ui.png)
2. Hello interfejsu użytkownika narzędzia Ambari, z hello prawym górnym rogu kliknij **hostów**.

    ![Znajdowanie adresu IP headnode](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/ambari-hosts.png)
3. Należy wyświetlić listę headnodes węzłów procesu roboczego i węzły dozorcy. Witaj headnodes ma hello **hn*** prefiks. Kliknij pierwszy headnode hello.

    ![Znajdowanie adresu IP headnode](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/cluster-headnodes.png)
4. U dołu strony hello, który zostanie otwarty z hello hello **Podsumowanie** polu adres IP hello kopiowania hello headnode i hello nazwy hosta.

    ![Znajdowanie adresu IP headnode](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/headnode-ip-address.png)
5. Obejmują hello adresu IP i nazwy hosta hello hello headnode toohello **hostów** pliku na komputerze hello, z którym chcesz toorun i zdalne debugowanie zadań Spark hello. Pozwoli to toocommunicate z headnode hello przy użyciu hello adresu IP, a także hello nazwy hosta.

   1. Otwórz program Notatnik z podwyższonym poziomem uprawnień. W menu Plik powitania kliknij **Otwórz** , a następnie przejdź toohello lokalizację pliku hosts hello. Na komputerze z systemem Windows jest `C:\Windows\System32\Drivers\etc\hosts`.
   2. Dodaj następujące toohello hello **hostów** pliku.

           # For headnode0
           192.xxx.xx.xx hn0-nitinp
           192.xxx.xx.xx hn0-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net

           # For headnode1
           192.xxx.xx.xx hn1-nitinp
           192.xxx.xx.xx hn1-nitinp.lhwwghjkpqejawpqbwcdyp3.gx.internal.cloudapp.net
6. Z komputera hello, który połączony toohello sieci wirtualnej platformy Azure, używanego przez klaster usługi HDInsight hello Sprawdź, czy można wykonać polecenie ping zarówno headnodes hello przy użyciu hello adresu IP, a także hello nazwy hosta.
7. SSH do hello headnode klastra przy użyciu instrukcji hello na [klastra usługi HDInsight tooan Połącz przy użyciu protokołu SSH](hdinsight-hadoop-linux-use-ssh-unix.md). Z headnode klastra hello Zbadaj hello adres IP komputera stacjonarnego hello. Należy przetestować połączenie tooboth hello adresy IP przypisane toohello komputer, dla połączenia sieciowego hello i hello innych dla hello sieci wirtualnej platformy Azure, która hello komputer jest połączony.
8. Powtórz kroki od hello na powitania również inne headnode.

## <a name="step-4-create-a-spark-scala-application-using-hello-hdinsight-tools-in-azure-toolkit-for-intellij-and-configure-it-for-remote-debugging"></a>Krok 4: Tworzenie aplikacji Spark Scala przy użyciu narzędzi HDInsight hello w zestawie narzędzi Azure for IntelliJ i skonfiguruj ją do zdalnego debugowania
1. Uruchom IntelliJ IDEA i Utwórz nowy projekt. W powitalne okno dialogowe Nowy projekt, wprowadź hello następujące opcje, a następnie kliknij przycisk **dalej**.

    ![Tworzenie aplikacji Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-hdi-scala-app.png)

   * W okienku po lewej stronie powitania, wybierz **HDInsight**.
   * W okienku po prawej stronie powitania, wybierz **Spark w usłudze HDInsight (Scala)**.
   * Kliknij przycisk **Dalej**.
2. W następnym oknie hello, podaj poniższe informacje projektu hello, a następnie kliknij przycisk **Zakończ**.  
   - Podaj nazwę projektu i lokalizacja projektu.
   - Dla **SDK projektu**, użyj języka Java 1.8 Java 1.7 spark 1.x klastra spark 2.x klastra.
   - Aby uzyskać **wersji Spark**, Kreator tworzenia projektu Scala integruje poprawnej wersji dla platformy Spark zestawy SDK i Scala. Jeśli hello klastra spark w wersji 2.0 niższe, wybierz spark 1.x. W przeciwnym razie należy wybrać spark2.x. W tym przykładzie użyto Spark2.0.2 (Scala 2.11.8).
       ![Tworzenie aplikacji Spark Scala](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-scala-project-details.png)
  
3. Projekt Spark Hello automatycznie utworzy artefaktu. toosee hello artefaktu, wykonaj następujące kroki.

   1. Z hello **pliku** menu, kliknij przycisk **struktury projektu**.
   2. W hello **struktury projektu** okno dialogowe, kliknij przycisk **artefakty** toosee hello domyślne artefaktu, który jest tworzony.
   ![Utwórz JAR](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/default-artifact.png)

      Można również tworzyć własne artefaktu bly kliknięcie hello  **+**  ikona wyróżnione powyższy obraz powitania.

4. Dodaj projekt tooyour biblioteki. tooadd biblioteki, kliknij prawym przyciskiem myszy nazwę projektu hello w drzewie projektu hello, a następnie kliknij przycisk **Otwórz ustawienia modułu**. W hello **struktury projektu** okno dialogowe, w okienku po lewej stronie powitania kliknij **biblioteki**, kliknij symbol hello (+), a następnie kliknij przycisk **z Maven**.

    ![Dodaj bibliotekę](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/add-library.png)

    W hello **pobrania biblioteki z repozytorium Maven** okna dialogowego, wyszukiwanie i dodać hello następujące biblioteki.

   * `org.scalatest:scalatest_2.10:2.2.1`
   * `org.apache.hadoop:hadoop-azure:2.7.1`
5. Kopiuj `yarn-site.xml` i `core-site.xml` z hello headnode klastra, a następnie dodaj go toohello projektu. Użyj hello następujące pliki hello toocopy poleceń. Można użyć [programów Cygwin](https://cygwin.com/install.html) toorun hello następujące `scp` polecenia toocopy hello plików z hello headnodes klastra.

        scp <ssh user name>@<headnode IP address or host name>://etc/hadoop/conf/core-site.xml .

    Ponieważ dodano już hello klastra headnode IP adres i nazwy hostów fo hello pliku hosts na pulpicie hello, możemy użyć hello **scp** poleceń w powitania po sposób.

        scp sshuser@hn0-nitinp:/etc/hadoop/conf/core-site.xml .
        scp sshuser@hn0-nitinp:/etc/hadoop/conf/yarn-site.xml .

    Dodaj projekt tooyour te pliki, kopiując je w obszarze hello **/src** folderu w drzewie z projektu, na przykład `<your project directory>\src`.
6. Aktualizacja hello `core-site.xml` hello toomake następujące zmiany.

   1. `core-site.xml`zawiera konta magazynu kluczy toohello hello szyfrowane skojarzony z klastrem hello. W hello `core-site.xml` dodania toohello projektu, Zastąp hello zaszyfrowanego klucza z kluczem przechowywania hello skojarzone z hello domyślne konto magazynu. Zobacz [zarządzanie kluczami dostępu do magazynu](../storage/common/storage-create-storage-account.md#manage-your-storage-account).

           <property>
                 <name>fs.azure.account.key.hdistoragecentral.blob.core.windows.net</name>
                 <value>access-key-associated-with-the-account</value>
           </property>
   2. Usuń następujące wpisy z hello hello `core-site.xml`.

           <property>
                 <name>fs.azure.account.keyprovider.hdistoragecentral.blob.core.windows.net</name>
                 <value>org.apache.hadoop.fs.azure.ShellDecryptionKeyProvider</value>
           </property>

           <property>
                 <name>fs.azure.shellkeyprovider.script</name>
                 <value>/usr/lib/python2.7/dist-packages/hdinsight_common/decrypt.sh</value>
           </property>

           <property>
                 <name>net.topology.script.file.name</name>
                 <value>/etc/hadoop/conf/topology_script.py</value>
           </property>
   3. Zapisz plik hello.
7. Dodawanie klasy głównym hello aplikacji. Z hello **Eksplorator projektów**, kliknij prawym przyciskiem myszy **src**, punktu zbyt**nowy**, a następnie kliknij przycisk **klasy Scala**.

    ![Dodaj kod źródłowy](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code.png)
8. W hello **Utwórz nową klasę Scala** okna dialogowego podaj nazwę, dla **rodzaj** wybierz **obiektu**, a następnie kliknij przycisk **OK**.

    ![Dodaj kod źródłowy](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/hdi-spark-scala-code-object.png)
9. W hello `MyClusterAppMain.scala` plików, Wklej hello następującego kodu. Ten kod tworzy hello Spark kontekstu i uruchamia `executeJob` metody z hello `SparkSample` obiektu.

        import org.apache.spark.{SparkConf, SparkContext}

        object SparkSampleMain {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkSample")
                                      .set("spark.hadoop.validateOutputSpecs", "false")
            val sc = new SparkContext(conf)

            SparkSample.executeJob(sc,
                                   "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
                                   "wasb:///HVACOut")
          }
        }

10. Powtórz kroki od 8 do 9 powyżej tooadd nowy obiekt Scala o nazwie `SparkSample`. Klasa toothis Dodaj hello następującego kodu. Ten kod odczytuje dane hello z hello HVAC.csv (dostępne na wszystkich klastrach HDInsight Spark), pobiera hello wiersze z tylko jedną cyfrę w kolumnie siódmego hello hello CSV i zapisuje dane wyjściowe hello zbyt**/HVACOut** w obszarze hello domyślne kontener magazynu hello klaster.

        import org.apache.spark.SparkContext

        object SparkSample {
         def executeJob (sc: SparkContext, input: String, output: String): Unit = {
           val rdd = sc.textFile(input)

           //find hello rows which have only one digit in hello 7th column in hello CSV
           val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)

           val s = sc.parallelize(rdd.take(5)).cartesian(rdd).count()
           println(s)

           rdd1.saveAsTextFile(output)
           //rdd1.collect().foreach(println)
         }
        }
11. Powtórz kroki od 8 do 9 powyżej tooadd nową klasę o nazwie `RemoteClusterDebugging`. Ta klasa implementuje hello struktury testowej Spark, która jest używana do debugowania aplikacji. Dodaj hello następującego kodu toohello `RemoteClusterDebugging` klasy.

        import org.apache.spark.{SparkConf, SparkContext}
        import org.scalatest.FunSuite

        class RemoteClusterDebugging extends FunSuite {

         test("Remote run") {
           val conf = new SparkConf().setAppName("SparkSample")
                                     .setMaster("yarn-client")
                                     .set("spark.yarn.am.extraJavaOptions", "-Dhdp.version=2.4")
                                     .set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")
                                     .setJars(Seq("""C:\workspace\IdeaProjects\MyClusterApp\out\artifacts\MyClusterApp_DefaultArtifact\default_artifact.jar"""))
                                     .set("spark.hadoop.validateOutputSpecs", "false")
           val sc = new SparkContext(conf)

           SparkSample.executeJob(sc,
             "wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv",
             "wasb:///HVACOut")
         }
        }

     Kilka ważnych rzeczy toonote tutaj:

   * Aby uzyskać `.set("spark.yarn.jar", "wasb:///hdp/apps/2.4.2.0-258/spark-assembly-1.6.1.2.4.2.0-258-hadoop2.7.1.2.4.2.0-258.jar")`, upewnij się, że hello zestawu Spark JAR jest dostępna w magazynie klastra hello w określonej ścieżce hello.
   * Aby uzyskać `setJars`, określ lokalizację hello, w której zostanie utworzona jar artefaktu hello. Zazwyczaj jest `<Your IntelliJ project directory>\out\<project name>_DefaultArtifact\default_artifact.jar`.
12. W hello `RemoteClusterDebugging` klasy, kliknij prawym przyciskiem myszy hello `test` — słowo kluczowe i wybierz **Tworzenie konfiguracji RemoteClusterDebugging**.

    ![Tworzenie konfiguracji zdalnej](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-remote-config.png)

13. Okno dialogowe hello, podaj nazwę dla konfiguracji hello, a następnie wybierz hello **Test rodzaj** jako **nazwa testu**. Pozostaw pozostałe wartości domyślne, kliknij przycisk **Zastosuj**, a następnie kliknij przycisk **OK**.

    ![Tworzenie konfiguracji zdalnej](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/provide-config-value.png)
14. Powinien zostać wyświetlony **zdalnego uruchom** konfiguracji listy rozwijanej na pasku menu hello.

    ![Tworzenie konfiguracji zdalnej](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/config-run.png)

## <a name="step-5-run-hello-application-in-debug-mode"></a>Krok 5: Uruchamianie aplikacji hello w trybie debugowania
1. Otwórz w projekcie IntelliJ IDEA `SparkSample.scala` i Utwórz rdd1 too'val z następnego punktu przerwania ". W menu podręczne hello tworzenia punkt przerwania, wybierz **wiersz w funkcji executeJob**.

    ![Dodawanie punktu przerwania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/create-breakpoint.png)
2. Kliknij hello **debugowania Uruchom** przycisku Dalej toohello **zdalnego uruchom** uruchomiona aplikacja hello toostart listy rozwijanej konfiguracji.

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-run-mode.png)
3. Podczas wykonywania programu hello osiągnie punkt przerwania hello, powinny być widoczne **debugera** w hello dolnym okienku.

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch.png)
4. Kliknij przycisk hello (**+**) tooadd ikona czujki, jak pokazano w poniższym obrazie hello.

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable.png)

    Tutaj, ponieważ aplikacja hello spowodowało przerwanie przed zmiennej hello `rdd1` został utworzony przy użyciu tego czujki możemy stwierdzić, jakie są hello 5 pierwszych wierszy w zmiennej hello `rdd`. Naciśnij klawisz **ENTER**.

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-add-watch-variable-value.png)

    Zobacz w powyższy obraz powitania jest, że w czasie wykonywania, można zbadać terrabytes danych i debugowania sposób realizowany Twojej aplikacji. Na przykład w danych wyjściowych hello pokazano powyższy obraz powitania widać tego hello pierwszy wiersz danych wyjściowych hello jest nagłówkiem. Na podstawie tych, można zmodyfikować wiersz kodu nagłówka hello tooskip Twojej aplikacji w razie potrzeby.
5. Możesz teraz kliknąć hello **Program Wznów** tooproceed ikonę z aplikacją, uruchom.

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-continue-run.png)
6. Jeśli aplikacja hello zakończy się pomyślnie, powinny pojawić się dane wyjściowe podobne do następujących hello.

    ![Uruchom hello program w trybie debugowania](./media/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely-through-vpn/debug-complete.png)

## <a name="seealso"></a>Zobacz też
* [Przegląd: platforma Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demonstracja
* Utwórz projekt Scala (klip wideo): [tworzenie aplikacji Spark Scala](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Debugowanie zdalne (klip wideo): [użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie w klastrze usługi HDInsight](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scenariusze
* [Platforma Spark i analiza biznesowa: interakcyjna analiza danych na platformie Spark w usłudze HDInsight z użyciem narzędzi do analizy biznesowej](hdinsight-apache-spark-use-bi-tools.md)
* [Platforma Spark i usługa Machine Learning: korzystanie z platformy Spark w usłudze HDInsight do analizy temperatury w budynku z użyciem danych HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Platforma Spark przy użyciu Machine Learning: Korzystanie z platformy Spark w wyników inspekcji żywności toopredict HDInsight](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Przesyłanie strumieniowe Spark: korzystanie z platformy Spark w usłudze HDInsight do tworzenia aplikacji do przesyłania strumieniowego w czasie rzeczywistym](hdinsight-apache-spark-eventhub-streaming.md)
* [Analiza dzienników witryny sieci Web na platformie Spark w usłudze HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Tworzenie i uruchamianie aplikacji
* [Tworzenie autonomicznych aplikacji przy użyciu języka Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Zdalne uruchamianie zadań w klastrze Spark przy użyciu programu Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Narzędzia i rozszerzenia
* [Użycie narzędzi HDInsight w zestawie narzędzi Azure IntelliJ toocreate i przesyłanie aplikacji Spark Scala](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Użyj narzędzi Azure dla aplikacji Spark toodebug IntelliJ zdalnie za pośrednictwem SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Użyj narzędzia HDInsight Tools for IntelliJ z Hortonworks piaskownicy](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Użyj narzędzia HDInsight Tools w zestawie narzędzi Azure dla programu Eclipse toocreate Spark aplikacji](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Korzystanie z notesów Zeppelin w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Jądra dostępne dla notesu Jupyter w klastrze Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Korzystanie z zewnętrznych pakietów z notesami Jupyter](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Instalacja oprogramowania Jupyter na komputerze i połącz tooan klastra Spark w usłudze HDInsight](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Zarządzanie zasobami
* [Zarządzanie zasobami hello klastra Apache Spark w usłudze Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Śledzenie i debugowanie zadań uruchamianych w klastrze Apache Spark w usłudze HDInsight](hdinsight-apache-spark-job-debugging.md)
