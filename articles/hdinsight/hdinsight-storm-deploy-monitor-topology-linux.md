---
title: "aaaDeploy i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toodeploy, monitorowanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Linux przy użyciu hello pulpit nawigacyjny Storm. Narzędzia usługi Hadoop dla programu Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>Wdrażanie i zarządzanie nimi topologii Apache Storm w usłudze HDInsight

Dowiedz się hello podstawowe informacje dotyczące zarządzania i monitorowania topologii Storm działających w Storm w klastrach HDInsight, w tym dokumencie.

> [!IMPORTANT]
> Witaj kroki opisane w tym artykule wymagają platformy Storm opartej na systemie Linux w klastrze usługi HDInsight. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows). 
>
> Aby uzyskać informacje dotyczące wdrażania i monitorowania topologii w usłudze HDInsight z systemu Windows, zobacz [wdrażanie i zarządzanie topologiami Apache Storm na HDInsight opartych na systemie Windows](hdinsight-storm-deploy-monitor-topology.md)


## <a name="prerequisites"></a>Wymagania wstępne

* **Platformy Storm opartej na systemie Linux w klastrze usługi HDInsight**: zobacz [wprowadzenie do Apache Storm w usłudze HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) instrukcje dotyczące tworzenia klastra

* (Opcjonalnie) **Znajomość protokołów SSH i SCP**: Aby uzyskać więcej informacji, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* (Opcjonalnie) **Programu visual Studio**: zestaw Azure SDK 2.5.1 lub nowszej i hello narzędzi Data Lake Tools dla programu Visual Studio. Aby uzyskać więcej informacji, zobacz [rozpoczęcie pracy przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    Jedna z hello następujące wersje programu Visual Studio:

  * Program Visual Studio 2012 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 z [aktualizacja 4](http://www.microsoft.com/download/details.aspx?id=44921) lub [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Program Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015 (dowolna wersja)

  * Visual Studio 2017 r (dowolna wersja). Narzędzia Data Lake Tools dla programu Visual Studio 2017 są instalowane jako część hello Azure obciążenia.

## <a name="submit-a-topology-visual-studio"></a>Przedstawia topologię: Visual Studio

Narzędzia HDInsight Hello mogą być używane toosubmit C# i hybrydowych topologii tooyour klaster Storm. Witaj, wykonaj czynności użyć przykładowej aplikacji. Informacji o tworzeniu własnych topologii za pomocą narzędzi HDInsight hello, zobacz [topologii opracowywania C# za pomocą hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

1. Jeśli hello najnowszą wersję narzędzia Data Lake hello nie jest już zainstalowany dla programu Visual Studio, zobacz [rozpoczęcie pracy przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    > [!NOTE]
    > Hello narzędzi Data Lake Tools dla programu Visual Studio były dawniej nazywane hello HDInsight Tools for Visual Studio.
    >
    > Narzędzia Data Lake Tools dla programu Visual Studio znajdują się w hello __obciążenia Azure__ dla programu Visual Studio 2017 r.

2. Otwórz program Visual Studio, wybierz **pliku** > **nowy** > **projektu**.

3. W hello **nowy projekt** okna dialogowego rozwiń **zainstalowana** > **szablony**, a następnie wybierz **HDInsight**. Wybierz z listy hello szablonów **próbki Storm**. U dołu hello hello — okno dialogowe wpisz nazwę aplikacji hello.

    ![Obraz](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **przesłać tooStorm w usłudze HDInsight**.

   > [!NOTE]
   > Jeśli zostanie wyświetlony monit, wprowadź poświadczenia logowania hello subskrypcji platformy Azure. Jeśli masz więcej niż jedną subskrypcję, zaloguj się za toohello, który zawiera Storm w klastrze usługi HDInsight.

5. Wybierz Storm w klastrze usługi HDInsight z hello **klaster Storm** listy rozwijanej, a następnie wybierz **przesyłania**. Można monitorować, czy przesyłanie hello działa prawidłowo, używając hello **dane wyjściowe** okna.

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>Przedstawia topologię: SSH i hello Storm polecenia

1. Użyj klastra usługi HDInsight toohello tooconnect SSH. Zastąp **USERNAME** hello nazwa logowania użytkownika SSH. Zastąp **CLUSTERNAME** z nazwą klastra usługi HDInsight:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Aby uzyskać więcej informacji na temat używania SSH tooconnect tooyour HDInsight klastra, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Użyj następującego polecenia toostart przykładową topologię hello:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    To polecenie uruchamia hello przykładową topologię WordCount na powitania klastra. Ta topologia losowego generowania zdań i hello liczby wystąpień poszczególnych wyrazów w zdaniach hello.

   > [!NOTE]
   > Podczas przesyłania topologii toohello klastra, należy najpierw skopiować plik jar hello zawierający hello klastra przed użyciem hello `storm` polecenia. toocopy hello pliku toohello klastra, można użyć hello `scp` polecenia. Na przykład: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > przykład Witaj WordCount i inne przykłady storm starter, znajdują się już w klastrze na `/usr/hdp/current/storm-client/contrib/storm-starter/`.

## <a name="submit-a-topology-programmatically"></a>Przedstawia topologię: programowe

TooStorm topologii, w usłudze HDInsight można wdrożyć programowo przy komunikacji z hello Nimbus usług hostowanych w klastrze. [https://github.com/Azure-Samples/hdinsight-Java-Deploy-STORM-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) przykładowego aplikacji w języku Java pokazano, jak toodeploy i uruchomić topologii za pośrednictwem hello usługi Nimbus.

## <a name="monitor-and-manage-visual-studio"></a>Monitorowanie i zarządzanie nimi: Visual Studio

Gdy topologii zostało pomyślnie przesłane za pomocą programu Visual Studio, hello **topologii Storm** widoku hello klastra jest wyświetlana. Wybierz topologię hello z hello listy tooview informacji na temat hello systemem topologii.

![monitor programu Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> Można również wyświetlić **topologii Storm** z **Eksploratora serwera** rozwijając **Azure** > **HDInsight**, a następnie prawym przyciskiem myszy klaster Storm w usłudze HDInsight i wybierając **topologii Storm widoku**.

Wybierz kształt hello hello spouts lub bolts tooview informacji dotyczących tych składników. Otwiera nowe okno dla każdego wybranego elementu.

### <a name="deactivate-and-reactivate"></a>Najpierw dezaktywować i ponowne uaktywnianie

Dezaktywowanie topologii wstrzymuje go dopóki zostanie przerwana lub ponownej aktywacji. tooperform te operacje, użyj hello __Dezaktywuj__ i __ponownie uaktywnić__ przyciski u góry hello hello __podsumowanie topologii__.

### <a name="rebalance"></a>Ponownie Zrównoważ

Ponowne równoważenie topologii umożliwia hello systemu toorevise hello równoległość topologii hello. Na przykład jeśli ma zmieniony tooadd klastra hello dodatkowych notatek, ponowne równoważenie umożliwia topologii toosee hello nowe węzły.

toorebalance topologii, użyj hello __Rebalance__ u góry hello hello __podsumowanie topologii__.

> [!WARNING]
> Ponowne równoważenie topologii najpierw dezaktywuje topologii hello ponownie dystrybuuje pracowników równomiernie między hello klastra, a następnie finally zwraca hello topologii toohello stanu sprzed ponowne równoważenie wystąpił. Tak topologii hello był aktywny, staje się aktywny ponownie. Jeśli została ona zdezaktywowana, pozostaje dezaktywowane.

### <a name="kill-a-topology"></a>Kasowanie topologii

Topologii STORM nadal działać do chwili zostały zatrzymane lub hello klastra zostanie usunięta. toostop topologii, użyj hello __Kill__ u góry hello hello __podsumowanie topologii__.

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>Monitorowanie i zarządzanie nimi: SSH i hello Storm polecenia

Witaj `storm` narzędzie umożliwia toowork z uruchomionymi topologiami z wiersza polecenia hello. Użyj `storm -h` pełną listę poleceń.

### <a name="list-topologies"></a>Topologie listy

Użyj następującego polecenia toolist hello wszystkich uruchomionych topologii:

    storm list

To polecenie zwraca informacje toohello podobne następującego tekstu:

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>Najpierw dezaktywować i ponowne uaktywnianie

Dezaktywowanie topologii wstrzymuje go dopóki zostanie przerwana lub ponownej aktywacji. Użyj następującego polecenia toodeactivate hello i Uaktywnij ponownie:

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>Kasowanie uruchomionej topologii

STORM topologii po uruchomieniu, nadal uruchomione aż do zatrzymania. toostop topologii, hello Użyj następującego polecenia:

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>Ponownie Zrównoważ

Ponowne równoważenie topologii umożliwia hello systemu toorevise hello równoległość topologii hello. Na przykład jeśli ma zmieniony tooadd klastra hello dodatkowych notatek, ponowne równoważenie umożliwia topologii toosee hello nowe węzły.

> [!WARNING]
> Ponowne równoważenie topologii najpierw dezaktywuje topologii hello ponownie dystrybuuje pracowników równomiernie między hello klastra, a następnie finally zwraca hello topologii toohello stanu sprzed ponowne równoważenie wystąpił. Tak topologii hello był aktywny, staje się aktywny ponownie. Jeśli została ona zdezaktywowana, pozostaje dezaktywowane.

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>Monitorowanie i zarządzanie nimi: Storm interfejsu użytkownika

Hello interfejsu użytkownika platformy Storm udostępnia interfejs sieci web do pracy z uruchomionymi topologiami i znajduje się w klastrze usługi HDInsight. Witaj tooview interfejsu użytkownika platformy Storm, użyj tooopen przeglądarki sieci web **https://CLUSTERNAME.azurehdinsight.net/stormui**, gdzie **CLUSTERNAME** jest hello nazwą klastra.

> [!NOTE]
> Jeśli pojawi się monit tooprovide nazwy użytkownika i hasła, wprowadź hello administratora klastra (admin) i hasło użyte podczas tworzenia klastra hello.

### <a name="main-page"></a>Strona główna

strony główne Hello hello interfejsu użytkownika platformy Storm udostępnia hello następujących informacji:

* **Podsumowanie klastra**: podstawowe informacje o hello klaster Storm.
* **Topologia podsumowania**: Lista uruchomionych topologii. Użyj hello łącza w tej sekcji tooview więcej informacji o określonych topologii.
* **Podsumowanie przełożonego**: informacje o przełożonego Storm hello.
* **Konfiguracja nimbus**: Konfiguracja Nimbus hello klastra.

### <a name="topology-summary"></a>Topologia podsumowania

Wybieranie łącza z hello **podsumowanie topologii** sekcja wyświetla następujące informacje o topologii hello hello:

* **Topologia podsumowania**: podstawowe informacje o topologii hello.
* **Akcje topologii**: Akcje zarządzania, które można wykonywać w odniesieniu do topologii hello.

  * **Aktywuj**: wznowienie przetwarzania dezaktywowanej topologii.
  * **Dezaktywuj**: wstrzymanie uruchomionej topologii.
  * **Rebalance**: można dostosować równoległość hello hello topologii. Po zmianie hello liczby węzłów w klastrze hello, należy przeprowadzić ponowne równoważenie uruchomionych topologii. Ta operacja pozwala hello topologii tooadjust równoległości toocompensate dla hello zwiększyć lub zmniejszyć liczbę węzłów w klastrze hello.

    Aby uzyskać więcej informacji, zobacz <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">opis hello równoległości topologii Storm</a>.
  * **Kasowanie**: kończy topologii Storm po hello określony limit czasu.
* **Statystyka topologii**: Statystyka topologii hello. tooset hello uzyskać hello pozostałe wpisy na stronie powitania, użyj łącza hello w hello **okna** kolumny.
* **Spouts**: hello elementach spout używane przez hello topologii. Użyj łączy hello w tej sekcji tooview więcej informacji na temat określonych elementach spout.
* **Bolts**: hello używane przez hello topologii elementów bolt. Użyj łączy hello w tej sekcji tooview więcej informacji na temat określonych elementów bolt.
* **Topologia konfiguracji**: hello konfiguracji topologii hello wybrane.

### <a name="spout-and-bolt-summary"></a>Spout i Bolt — podsumowanie

Wybieranie spout z hello **Spouts** lub **Bolts** sekcje Wyświetla hello następujących informacji o elemencie hello wybrane:

* **Składnik podsumowania**: podstawowe informacje o hello spout lub bolt.
* **Spout/Bolt stats**: Statystyka hello spout lub elementów bolt. tooset hello uzyskać hello pozostałe wpisy na stronie powitania, użyj łącza hello w hello **okna** kolumny.
* **Wprowadź statystykę** (tylko dla elementów bolt): informacje o hello strumienie używane przez hello bolt.
* **OUTPUT stats**: informacje o strumieni hello emitowane przez to spout ani dla elementów bolt.
* **Modułów**: informacje na temat wystąpień hello hello spout lub bolt. Wybierz hello **portu** wpis dla tooview określonego modułu wykonującego dziennika informacji diagnostycznych utworzone dla tego wystąpienia.
* **Błędy**: informacje o błędzie dla tego spout lub elementów bolt.

## <a name="monitor-and-manage-rest-api"></a>Monitorowanie i zarządzanie nimi: interfejsu API REST

Hello interfejsu użytkownika platformy Storm jest oparty na powitania interfejsu API REST, więc można wykonać podobne do zarządzania i monitorowania funkcji przy użyciu hello interfejsu API REST. Można użyć interfejsu API REST hello toocreate niestandardowych narzędzi do zarządzania i monitorowania topologii Storm.

Aby uzyskać więcej informacji, zobacz [interfejsu API REST interfejsu użytkownika Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html). Witaj następujące informacje są hello toousing określonego interfejsu API REST z systemu Apache Storm w usłudze HDInsight.

> [!IMPORTANT]
> Witaj interfejsu API REST Storm nie jest publicznie dostępna przez hello internet i muszą być dostępne za pomocą protokołu SSH tunelu toohello HDInsight węzła głównego klastra. Aby uzyskać informacje na temat tworzenia i używania tunelu SSH, zobacz [Użyj SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie i innych sieci web UI](hdinsight-linux-ambari-ssh-tunnel.md).

### <a name="base-uri"></a>Podstawowy identyfikator URI

Witaj podstawowy identyfikator URI dla hello interfejsu API REST w klastrach HDInsight opartych na systemie Linux jest dostępna na powitania węzła głównego w **https://HEADNODEFQDN:8744/api/v1/**. Nazwa domeny Hello węzła głównego hello jest generowany podczas tworzenia klastra i nie jest statyczne.

Hello pełną nazwę domeny (FQDN) dla węzła głównego klastra hello znajduje się na kilka różnych sposobów:

* **W sesji SSH**: Użyj polecenia hello `headnode -f` z klastra toohello sesji SSH.
* **Z sieci Ambari Web**: Wybierz **usług** od góry hello hello strony, następnie wybierz **Storm**. Z hello **Podsumowanie** wybierz opcję **serwera interfejsu użytkownika Storm**. Witaj FQDN węzła hello, który działa hello interfejsu użytkownika platformy Storm i interfejsu API REST jest u góry hello hello strony.
* **Z interfejsu API REST Ambari**: Użyj polecenia hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve informacji na temat hello węzła, który hello interfejsu użytkownika platformy Storm i interfejsu API REST są uruchomione na. Zastąp **hasło** o hasło administratora hello hello klastra. Zastąp **CLUSTERNAME** hello nazwą klastra. W odpowiedzi hello wpis "host_name" hello zawiera hello FQDN węzła hello.

### <a name="authentication"></a>Authentication

Toohello żądania interfejsu API REST muszą używać **uwierzytelnianie podstawowe**, więc użyć hello HDInsight klastra nazwę i hasło administratora.

> [!NOTE]
> Ponieważ uwierzytelnianie podstawowe jest wysyłany przy użyciu zwykłego tekstu, należy **zawsze** połączeń toosecure HTTPS za pomocą hello klastra.

### <a name="return-values"></a>Wartości zwracane

Informacje zwrócone z hello interfejsu API REST mogą być tylko można używać z wewnątrz klastra hello lub maszyn wirtualnych na hello tej samej sieci wirtualnej platformy Azure jako klaster hello. Na przykład nie jest dostępny z Internetu hello hello pełną nazwę domeny (FQDN) dla serwerów dozorcy zwracane.

## <a name="next-steps"></a>Następne kroki

Teraz, kiedy znasz już jak topologie toodeploy i monitorować za pomocą hello pulpit nawigacyjny Storm, Dowiedz się, jak za[topologie oparte na opracowanie Java za pomocą programu Maven](hdinsight-storm-develop-java-topology.md).

Aby uzyskać listę więcej przykładowe topologie, zobacz [przykładowe topologie dla systemu Storm w usłudze HDInsight](hdinsight-storm-example-topology.md).
