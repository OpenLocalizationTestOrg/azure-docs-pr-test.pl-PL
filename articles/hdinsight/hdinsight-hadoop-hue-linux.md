---
title: "aaaHue z platformą Hadoop w klastrach opartych na systemie Linux usługi HDInsight - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall Hue w usłudze HDInsight clusters i korzystać z tunelowania tooHue żądań hello tooroute. Użyj magazynu toobrowse Hue, a następnie uruchom Hive i Pig."
keywords: HUE hadoop
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 9e57fcca-e26c-479d-a745-7b80a9290447
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: f086cbad2a90cc6903fbfccbf4a6be44f8999d07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-hue-on-hdinsight-hadoop-clusters"></a>Zainstalować i używać Hue w klastrach HDInsight Hadoop

Dowiedz się, jak tooinstall Hue w usłudze HDInsight clusters i korzystać z tunelowania tooHue żądań hello tooroute.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="what-is-hue"></a>Co to jest Hue?
HUE jest zestaw aplikacji sieci Web użycia toointeract przy użyciu funkcji klastra usługi Hadoop. Można używać magazynu hello toobrowse Hue skojarzony z klastrem usługi Hadoop (w przypadku klastrów usługi HDInsight hello WASB), uruchamiania zadań Hive i skryptów usługi Pig i tak dalej. Witaj następujące składniki są dostępne z instalacjami aplikacji Hue w klastrze usługi HDInsight Hadoop.

* Edytor Hive wosk pszczeli
* Pig
* Menedżer na potrzeby magazynu metadanych
* Oozie
* FileBrowser (która komunikuje tooWASB domyślny kontener)
* Zadanie przeglądarki

> [!WARNING]
> Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane i Microsoft Support będzie pomocy tooisolate i rozwiązać problemy toothese powiązane składniki.
>
> Niestandardowe składniki odbierania toohelp Obsługa uzasadnione ekonomicznie toofurther należy rozwiązać problem hello. Może to spowodować nad rozwiązaniem problemu hello lub proszenia tooengage dostępnych kanałów dla hello otwarty technologii źródła wykryto głębokie doświadczenia z tej technologii. Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/).
>
>

## <a name="install-hue-using-script-actions"></a>Instalowanie aplikacji Hue za pomocą akcji skryptu

tooinstall skryptu Hello Hue w klastrze usługi HDInsight opartej na systemie Linux jest dostępna w https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. Jako domyślnego magazynu, można użyć tego skryptu tooinstall Hue w klastrach z obiektów blob magazynu Azure (WASB) lub usługi Azure Data Lake Store.

Ta sekcja zawiera instrukcje dotyczące sposobu toouse hello skryptu podczas inicjowania obsługi administracyjnej hello klastra przy użyciu hello portalu Azure.

> [!NOTE]
> Program Azure PowerShell, hello Azure CLI, hello zestawu .NET SDK usługi HDInsight lub szablonów usługi Azure Resource Manager może być również używane tooapply akcji skryptu. Można także zastosować tooalready akcji skryptu działające klastry. Aby uzyskać więcej informacji, zobacz [Dostosowywanie klastrów usługi HDInsight z akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).
>
>

1. Uruchom inicjowania obsługi klastra za pomocą kroków hello w [Obsługa administracyjna klastrów HDInsight w systemie Linux](hdinsight-hadoop-provision-linux-clusters.md), kroków inicjowania obsługi administracyjnej.

   > [!NOTE]
   > Hue tooinstall w usłudze HDInsight clusters, hello headnode zalecany rozmiar jest co najmniej A4 (8 rdzenie, 14 GB pamięci RAM).
   >
   >
2. Na powitania **konfiguracji opcjonalnej** bloku, wybierz opcję **akcji skryptu**i podaj informacje dotyczące hello, jak pokazano poniżej:

    ![Podaj parametry akcji skryptu dla Hue](./media/hdinsight-hadoop-hue-linux/hue-script-action.png "Podaj parametry akcji skryptu dla Hue")

   * **Nazwa**: Wprowadź przyjazną nazwę dla hello akcji skryptu.
   * **Identyfikator URI skryptu**: https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
   * **HEAD**: Zaznaczenie tego pola wyboru
   * **Proces ROBOCZY**: to pole pozostanie puste.
   * **DOZORCY**: to pole pozostanie puste.
   * **Parametry**: to pole pozostanie puste.
3. U dołu hello hello **akcji skryptu**, użyj hello **wybierz** przycisk toosave hello konfiguracji. Na koniec użyj hello **wybierz** u dołu hello hello **konfiguracji opcjonalnej** bloku toosave hello konfiguracji opcjonalnej informacji.
4. Kontynuuj, inicjowania obsługi klastra hello zgodnie z opisem w [Obsługa administracyjna klastrów HDInsight w systemie Linux](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="use-hue-with-hdinsight-clusters"></a>Użyj Hue z klastrami usługi HDInsight

Tunelowanie SSH jest hello tylko tooaccess sposób Hue w klastrze hello, gdy jest uruchomiona. Tunelowanie za pośrednictwem SSH umożliwia toogo ruchu hello bezpośrednio headnode toohello z hello klastra, gdzie odcienia, który jest uruchomiony. Po zakończeniu hello klastra podczas inicjowania obsługi administracyjnej, należy użyć hello następujące kroki toouse Hue w klastrze HDInsight Linux.

> [!NOTE]
> Zaleca się przy użyciu instrukcji hello toofollow Firefox przeglądarki sieci web, które zostały poniżej.
>
>

1. Użyj informacji hello w [Użyj SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie i innych interfejs sieci web](hdinsight-linux-ambari-ssh-tunnel.md) toocreate SSH tunelowania z klastrem usługi HDInsight toohello systemu klienta, a następnie skonfiguruj z sieci Web przeglądarce toouse hello SSH tunelu jako serwer proxy.

2. Po utworzeniu tunelu SSH i skonfigurowany ruchu tooproxy przeglądarki przy jego użyciu, należy znaleźć nazwy hosta hello hello głównej węzła głównego. Można to zrobić, łącząc toohello klastra przy użyciu protokołu SSH na port 22. Na przykład `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net` gdzie **USERNAME** to nazwa użytkownika SSH i **CLUSTERNAME** jest hello nazwą klastra.

    Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Po nawiązaniu połączenia użyj następującego polecenia tooobtain hello pełni kwalifikowaną nazwę domeny głównej headnode hello hello:

        hostname -f

    Spowoduje to zwrócenie nazwa podobne toohello po:

        hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

    Jest hello nazwy hosta headnode głównej hello, gdzie znajduje się hello Hue witryny sieci Web.
4. Użyj hello przeglądarki tooopen hello Hue portal u http://HOSTNAME:8888. Zamień nazwę hello uzyskanych w poprzednim kroku hello nazwy hosta.

   > [!NOTE]
   > Podczas logowania na powitania po raz pierwszy, będzie zostanie wyświetlony monit o toocreate toolog konta w portalu Hue toohello. poświadczenia Hello, określone w tym miejscu będzie ograniczona toohello portalu i nie są powiązane toohello administratora lub poświadczeń SSH, określone podczas udostępniania hello klastra.
   >
   >

    ![Portalu Hue toohello logowania](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-login.png "Określ poświadczenia dla portalu Hue")

### <a name="run-a-hive-query"></a>Uruchomienie zapytania programu Hive
1. Z portalu Hue hello, kliknij przycisk **edytory zapytania**, a następnie kliknij przycisk **Hive** Edytor Hive hello tooopen.

    ![Korzystanie z programu Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-use-hive.png "korzystanie z programu Hive")
2. Na powitania **Assist** , w obszarze **bazy danych**, powinny pojawić się **hivesampletable**. Jest to Przykładowa tabela, który jest dostarczany z wszystkich klastrów Hadoop w usłudze HDInsight. Wprowadź przykładowe zapytanie w okienku po prawej stronie powitania i wyświetlane hello na powitania **wyniki** karcie w okienku hello poniżej, jak pokazano w hello Przechwytywanie ekranu.

    ![Uruchamianie zapytań Hive](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-hive-query.png "zapytanie Hive Uruchom")

    Można również użyć hello **wykresu** karcie toosee wizualną reprezentację hello wynik.

### <a name="browse-hello-cluster-storage"></a>Przeglądaj hello magazynu klastra
1. Z portalu Hue hello, kliknij przycisk **przeglądarka plików** w hello prawym górnym rogu paska menu hello.
2. Domyślnie hello pliku przeglądarce zostanie otwarty na powitania **/użytkownik/Myuser.pds** katalogu. Kliknij przycisk hello ukośnik bezpośrednio poprzedzający hello katalogu użytkownika w katalogu głównym toohello toogo ścieżki hello hello kontenera magazynu systemu Azure skojarzony z klastrem hello.

    ![Użyj pliku przeglądarki](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-file-browser.png "używana przeglądarka plików")
3. Kliknij prawym przyciskiem myszy plik lub folder toosee hello dostępne operacje. Użyj hello **przekazać** przycisku na powitania rogu tooupload pliki toohello bieżącego katalogu. Użyj hello **nowy** przycisk toocreate nowych plików lub katalogów.

> [!NOTE]
> Przeglądarka plików Hue Hello można wyświetlić tylko zawartość hello hello domyślnego kontenera skojarzonego z klastrem usługi HDInsight hello. Wszelkie dodatkowe miejsce do magazynowania kont/kontenerów, które mogą być skojarzone z klastrem hello nie będzie dostępna przy użyciu przeglądarki plików hello. Jednak dodatkowe kontenery hello skojarzony z klastrem hello zawsze będzie dostępna dla zadań Hive hello. Na przykład wprowadź polecenie hello `dfs -ls wasb://newcontainer@mystore.blob.core.windows.net` w edytorze Hive hello, można wyświetlić zawartość hello również dodatkowe kontenerów. W tym poleceniu **newcontainer** nie jest hello domyślnego kontenera skojarzonego z klastrem.
>
>

## <a name="important-considerations"></a>Ważne uwagi
1. Hue tooinstall skryptu używanego Hello instaluje je tylko na powitania headnode głównej hello klastra.

2. Podczas instalacji aktualizacji konfiguracji hello ponownego uruchomienia wielu usług Hadoop (HDFS, YARN, MR2, Oozie). Po zakończeniu działania skryptu hello, instalowanie aplikacji Hue, może upłynąć trochę czasu, zanim inne toostart usługi Hadoop. To może wpłynąć na wydajność aplikacji Hue w początkowo. Po uruchomić wszystkie usługi odcienia, który będzie pełną funkcjonalność.
3. HUE nie rozpoznaje Tez zadania, czyli hello domyślne bieżącej gałęzi. Jeśli chcesz toouse MapReduce jako hello aparat wykonywania Hive, aktualizacja hello toouse skryptu hello następujące polecenie w skrypcie:

        set hive.execution.engine=mr;

4. Dzięki klastry z systemem Linux mogą mieć scenariusz, w którym usługi są uruchomione na headnode głównej hello podczas hello Resource Manager mogą być wykonywane na powitania dodatkowej. Takiej sytuacji może spowodować błędy (pokazana poniżej), korzystając z Hue tooview szczegóły zadania uruchomione w klastrze hello. Jednak po ukończeniu zadania hello można przeglądać szczegóły zadania hello.

   ![Błąd portalu Hue](./media/hdinsight-hadoop-hue-linux/hdinsight-hue-portal-error.png "błąd portalu Hue")

   Jest to termin tooa znany problem. Jako obejście należy zmodyfikować Ambari, tak aby hello active Resource Manager również działa na powitania headnode podstawowego.
5. HUE rozumie WebHDFS, podczas gdy klastry usługi HDInsight przy użyciu usługi Azure Storage `wasb://`. Tak hello skryptu niestandardowego używane z akcji skryptu instaluje WebWasb, czyli mówić tooWASB usługę zgodny z WebHDFS. Tak, mimo że portalu Hue hello mówi systemu plików HDFS w miejscach (takich jak, gdy mysz przesuwa się nad hello **przeglądarka plików**), powinny być rozumiane jako WASB.

## <a name="next-steps"></a>Następne kroki
* [Zainstaluj Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install-linux.md). Użyj tooinstall dostosowywania klastra, który Giraph na platformie Hadoop w HDInsight clusters. Giraph pozwala wykres tooperform przetwarzania przy użyciu platformy Hadoop i może służyć z usługą Azure HDInsight.
* [Zainstaluj Solr w klastrach HDInsight](hdinsight-hadoop-solr-install-linux.md). Użyj tooinstall dostosowywania klastra, który Solr na platformie Hadoop w HDInsight clusters. Solr umożliwia operacji wyszukiwania zaawansowanego tooperform na przechowywanych danych.
* [Zainstalować język R w klastrach HDInsight](hdinsight-hadoop-r-scripts-linux.md). Użyj klastra dostosowania tooinstall R w klastrach HDInsight Hadoop. R jest open source języka i środowiska do statystycznego przetwarzania danych. Zapewnia on setki wbudowanych funkcji statystycznych i własnej język programowania, łączącą aspekty funkcjonalne i zorientowanym obiektowo programowania. Umożliwia także rozbudowane funkcje graficzne.

[powershell-install-configure]: install-configure-powershell-linux.md
[hdinsight-provision]: hdinsight-provision-clusters-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
