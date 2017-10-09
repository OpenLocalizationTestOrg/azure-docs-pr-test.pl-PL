---
title: "dostępność aaaHigh Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak klastry usługi HDInsight poprawy niezawodności i dostępności przy użyciu dodatkowego węzła głównego. Dowiedz się, jak to ma wpływ na usługi Hadoop, takich jak Ambari i Hive, oraz jak tooindividually połączyć tooeach węzła głównego przy użyciu protokołu SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "Wysoka dostępność usługi hadoop"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a>Dostępność i niezawodność klastrów Hadoop w usłudze HDInsight

Klastry HDInsight zapewniają dwóch węzłów głównych tooincrease hello dostępność i niezawodność usług Hadoop i zadania uruchomione.

Hadoop osiąga wysokiej dostępności i niezawodności, replikowanie usług i danych w wielu węzłach w klastrze. Jednak standardowe podziału Hadoop zwykle mają tylko pojedynczego węzła głównego. Wszelkie awarii jednego węzła głównego hello może spowodować hello klastra toostop pracy. Usługa HDInsight zapewnia dostępność i niezawodność dwóch headnodes tooimprove Hadoop.

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="availability-and-reliability-of-nodes"></a>Dostępność i niezawodność węzłów

Węzły w klastrze usługi HDInsight są implementowane za pomocą usługi Azure Virtual Machines. Witaj poniższych sekcjach omówiono typy oddzielnego węzła hello używane z usługą HDInsight. 

> [!NOTE]
> Nie wszystkie typy węzłów są używane dla typu klastra. Na przykład typ klastra usługi Hadoop nie ma żadnych węzłów Nimbus. Aby uzyskać więcej informacji na węzłach używana przez typy klastrów usługi HDInsight, zobacz hello klastra typy część hello [utworzyć Linux opartych klastrów Hadoop w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) dokumentu.

### <a name="head-nodes"></a>HEAD węzłów

tooensure wysoką dostępność usług Hadoop, usługa HDInsight zapewnia dwóch węzłów głównych. Obu węzłów głównych są aktywne i działa w klastrze HDInsight hello jednocześnie. Niektóre usługi, takie jak system plików HDFS lub YARN, są tylko aktywne, w jednym węźle głównym w danym momencie. Inne usługi, takie jak serwera HiveServer2 lub na potrzeby magazynu metadanych Hive są aktywne w obu węzłów głównych w hello tym samym czasie.

Węzły HEAD (i inne węzły w usłudze HDInsight) ma wartość numeryczną jako część nazwy hosta hello hello węzła. Na przykład `hn0-CLUSTERNAME` lub `hn4-CLUSTERNAME`.

> [!IMPORTANT]
> Nie należy kojarzyć hello wartość liczbową z tego, czy węzeł jest podstawowy lub pomocniczy. wartość liczbowa Hello jest tylko obecny tooprovide unikatową nazwę dla każdego węzła.

### <a name="nimbus-nodes"></a>Węzły Nimbus

Węzły nimbus są dostępne z klastrami Storm. węzły Nimbus Hello zapewniają podobne funkcje toohello Hadoop JobTracker przy dystrybucji i monitorowania przetwarzania między węzłami procesów roboczych. HDInsight dostarcza dwóch węzłów Nimbus, w przypadku klastrów Storm

### <a name="zookeeper-nodes"></a>Węzły dozorcy

[Dozorcy](http://zookeeper.apache.org/) węzły są używane do wyboru wiodące głównego usługi na węzłach głównych. Są one również używane tooinsure czy usług, danych (proces roboczy) węzły i bram wiedzieć, który węzła głównego głównej usługi jest aktywna na. Domyślnie usługa HDInsight zapewnia trzy węzły dozorcy.

### <a name="worker-nodes"></a>Węzłów procesu roboczego

Węzłów procesu roboczego do wykonywania analizy danych rzeczywistych hello gdy zadanie jest toohello przesyłanego klastra. Jeśli węzłem procesu roboczego nie powiedzie się, hello zadanie, które zostało zostanie wykonana jest węzłem procesu roboczego tooanother zostało przesłane. Domyślnie HDInsight tworzy czterech węzłów procesu roboczego. Możesz zmienić ten numer toosuit potrzeb podczas i po utworzeniu klastra.

### <a name="edge-node"></a>Węzeł krawędzi

Węzeł krawędzi nie aktywnie uczestniczy w analizy danych w ramach klastra hello. Jest on używany przez programistów i analityków danych, podczas pracy z platformą Hadoop. życie węzła krawędzi Hello w hello tej samej sieci wirtualnej platformy Azure jako hello inne węzły w klastrze hello i można uzyskać dostęp do wszystkich innych węzłów. można użyć węzła krawędzi Hello bez konieczności przełączania zasoby zadań analizy i krytycznych usług Hadoop.

Serwer R w usłudze HDInsight jest obecnie hello tylko klastra typ, który zawiera węzeł krawędzi domyślnie. R Server w usłudze HDInsight, węzłem krawędzi hello jest używany kod testu R lokalnie w węźle hello przed przesłaniem go toohello klastra na potrzeby przetwarzania rozproszonego.

Informacje o korzystaniu z węzłem krawędzi z klastra o typie innym niż serwer R, zobacz hello [użycia węzłów krawędzi w usłudze HDInsight](hdinsight-apps-use-edge-node.md) dokumentu.

## <a name="accessing-hello-nodes"></a>Uzyskiwanie dostępu do węzłów hello

Klastra toohello dostępu za pośrednictwem hello podano internet za pośrednictwem bramy sieci publicznej. Dostęp jest ograniczony tooconnecting toohello głównymi węzłami i (jeśli istnieje) hello węzła krawędzi. Uruchomione w węzłach head hello tooservices dostępu nie odbywa się przez wiele węzłów głównych. Hello publicznego bramy trasy żądania toohello węzła głównego obsługującego hello żądanej usługi. Na przykład Ambari znajduje się obecnie na powitania drugiego węzła głównego, hello brama kieruje przychodzące żądania dla węzła toothat Ambari.

Dostęp za pośrednictwem bramy publicznego hello jest ograniczona tooport 443 (HTTPS), 22 i 23.

* Port __443__ jest używane tooaccess Ambari i innych sieci web interfejsu użytkownika lub hostowanych w węzłach głównych hello interfejsów API REST.

* Port __22__ jest używane tooaccess hello głównej węzła głównego lub węzłem krawędzi przy użyciu protokołu SSH.

* Port __23__ jest hello używane tooaccess drugiego węzła głównego przy użyciu protokołu SSH. Na przykład `ssh username@mycluster-ssh.azurehdinsight.net` łączy toohello głównej węzła głównego o nazwie klastra hello **mycluster**.

Aby uzyskać więcej informacji o korzystaniu z protokołu SSH, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.

### <a name="internal-fully-qualified-domain-names-fqdn"></a>Wewnętrzne w pełni kwalifikowanej nazwy domeny (FQDN)

Węzły w klastrze HDInsight ma wewnętrzny adres IP i nazwy FQDN, która jest możliwy tylko z hello klastra. Podczas uzyskiwania dostępu do usługi w klastrze hello przy użyciu hello wewnętrznej nazwy FQDN lub adres IP, należy używać narzędzia Ambari tooverify hello adres IP lub nazwa FQDN toouse podczas uzyskiwania dostępu do usługi hello.

Na przykład Witaj Oozie usługi można uruchomić tylko na jednym węźle głównym, a za pomocą hello `oozie` polecenia w sesji SSH wymaga hello adres URL toohello usługi. Ten adres URL można pobrać z Ambari przy użyciu hello następujące polecenie:

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

To polecenie zwraca wartość toohello podobne, następujące polecenie, które zawiera hello wewnętrznego adresu URL toouse z hello `oozie` polecenia:

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

Aby uzyskać więcej informacji na temat pracy z hello interfejsu API REST Ambari, zobacz [monitorować i zarządzać HDInsight przy użyciu interfejsu API REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).

### <a name="accessing-other-node-types"></a>Uzyskiwanie dostępu do innych typów węzła

Możesz połączyć toonodes, które są nie bezpośrednio dostępny przez hello internet przy użyciu następujących metod hello:

* **SSH**: po nawiązaniu połączenia z węzłem głównym tooa przy użyciu protokołu SSH, można użyć protokołu SSH z hello węzła głównego tooconnect tooother węzłów w klastrze hello. Aby uzyskać więcej informacji, zobacz hello [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) dokumentu.

* **Tunel SSH**: Jeśli potrzebujesz tooaccess usługi sieci web hostowanych na jednym z węzłów hello, które nie jest widoczne toohello internet, należy użyć tunelu SSH. Aby uzyskać więcej informacji, zobacz hello [tunelu SSH za pomocą usługi HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.

* **Sieć wirtualna platformy Azure**: Jeśli Twoje HDInsight klastra jest częścią sieci wirtualnej platformy Azure, dowolnego zasobu na hello sam sieci wirtualnej można uzyskać dostęp do wszystkich węzłów w klastrze hello. Aby uzyskać więcej informacji, zobacz hello [rozszerzyć HDInsight przy użyciu usługi Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) dokumentu.

## <a name="how-toocheck-on-a-service-status"></a>Jak toocheck stanu usługi

Stan hello toocheck usługi działające na powitania węzłów głównych Użyj hello Interfejsu sieci Web Ambari lub hello interfejsu API REST Ambari.

### <a name="ambari-web-ui"></a>Interfejs użytkownika sieci Web Ambari

Interfejs sieci Web Ambari Hello są widoczne w https://CLUSTERNAME.azurehdinsight.net. Zastąp **CLUSTERNAME** o nazwie hello klastra. Jeśli zostanie wyświetlony monit, wprowadź poświadczenia użytkownika hello HTTP dla klastra. Witaj domyślna nazwa użytkownika HTTP jest **admin** i hasło hello jest hello hasła podczas tworzenia klastra hello.

Nadejściu na stronie Ambari hello hello zainstalowane usługi są wyświetlane na powitania po lewej stronie powitania.

![Zainstalowane usługi](./media/hdinsight-high-availability-linux/services.png)

Istnieje szereg ikony wyświetlane dalej stan tooindicate usługi tooa. Wszystkie alerty dotyczące usługi tooa można wyświetlić przy użyciu hello **alerty** łącze u góry hello hello strony. Można wybrać więcej o tooview każdej usługi.

Strony usługi hello zawiera informacje na powitania stanu i konfiguracji poszczególnych usług, natomiast nie dostarcza informacji, na którym jest uruchomiona usługa hello węzła głównego na. tooview tej informacji, użyj hello **hostów** łącze u góry hello hello strony. Ta strona wyświetla hosty w klastrze hello, w tym hello węzłów głównych.

![listy hostów](./media/hdinsight-high-availability-linux/hosts.png)

Wybór łącza hello jednego z węzłów głównych hello Wyświetla hello usług i składników uruchomione w tym węźle.

![Stan składnika](./media/hdinsight-high-availability-linux/nodeservices.png)

Aby uzyskać więcej informacji na temat używania narzędzia Ambari, zobacz [monitorowanie i zarządzanie nimi przy użyciu interfejsu użytkownika sieci Web Ambari hello HDInsight](hdinsight-hadoop-manage-ambari.md).

### <a name="ambari-rest-api"></a>Interfejs API REST Ambari

Interfejs API REST Ambari Hello jest dostępna za pośrednictwem hello internet. Brama publicznego HDInsight Hello obsługuje routingu żądań toohello węzła głównego aktualnie obsługujący hello interfejsu API REST.

Możesz użyć następującego polecenia toocheck hello stanu usługi za pośrednictwem interfejsu API REST Ambari hello hello:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* Zastąp **hasło** z hasłem konta użytkownika (Administrator) hello HTTP.
* Zastąp **CLUSTERNAME** o nazwie hello hello klastra.
* Zastąp **SERVICENAME** o nazwie hello hello usługi ma stan hello toocheck.

Na przykład stan hello toocheck hello **HDFS** usługi w klastrze o nazwie **mycluster**, używając hasła **hasła**, należy użyć następującego polecenia hello:

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

odpowiedź Hello jest podobne toohello po JSON:

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

Witaj adresu URL informuje NAS czy hello usługa jest obecnie uruchomiona na węzła głównego o nazwie **hn0 CLUSTERNAME**.

Witaj stanu informuje NAS czy obecnie jest uruchomiona usługa hello, lub **uruchomiono**.

Jeśli nie wiesz, jakie usługi są zainstalowane na powitania klastra, można użyć hello następujące polecenia tooretrieve listy:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

Aby uzyskać więcej informacji na temat pracy z hello interfejsu API REST Ambari, zobacz [monitorować i zarządzać HDInsight przy użyciu interfejsu API REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).

#### <a name="service-components"></a>Składniki usługi

Usługi mogą obejmować składników, które mają stan hello toocheck indywidualnie. Na przykład system plików HDFS zawiera składnik NameNode hello. tooview informacji na temat składnika, polecenie hello będzie:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

Jeśli nie wiadomo, które składniki są dostarczane przez usługę, możesz użyć hello następujące polecenia tooretrieve listy:

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a>Jak tooaccess dzienniki na powitania węzłów głównych

### <a name="ssh"></a>SSH

Podczas węzła głównego tooa połączonych za pośrednictwem protokołu SSH, pliki dziennika można znaleźć w **/var/log**. Na przykład **/var/log/hadoop-yarn/yarn** zawiera dzienników YARN.

Każdego węzła głównego może mieć wpisy dziennika unikatowy, dlatego należy sprawdzić dzienniki hello na obu.

### <a name="sftp"></a>SFTP

Można także połączyć toohello węzła głównego przy użyciu hello SSH protokołu transferu plików lub Secure File Transfer Protocol (SFTP) i pobierania plików dziennika hello bezpośrednio.

Podobne toousing klienta SSH, łącząc toohello klastra, które należy podać hello SSH konto nazwy użytkownika i hello SSH adresu hello klastra. Na przykład `sftp username@mycluster-ssh.azurehdinsight.net`. Podaj hello hasło dla konta powitania po wyświetleniu monitu, lub Podaj klucz publiczny przy użyciu hello `-i` parametru.

Po nawiązaniu połączenia jest wyświetlana `sftp>` wiersza. Z wiersza polecenia, można zmienić katalogi, przekazywanie i pobieranie plików. Na przykład hello następujące polecenia Zmień katalogi toohello **/var/log/hadoop/hdfs** katalogu, a następnie Pobierz wszystkie pliki w katalogu hello.

    cd /var/log/hadoop/hdfs
    get *

Aby uzyskać listę dostępnych poleceń, wprowadź `help` na powitania `sftp>` wiersza.

> [!NOTE]
> Dostępne są także graficzne interfejsy, które pozwalają toovisualize hello systemu plików, gdy nawiązano połączenie przy użyciu protokołu SFTP. Na przykład [MobaXTerm](http://mobaxterm.mobatek.net/) pozwala systemu plików hello toobrowse za pomocą interfejsu tooWindows podobne Explorer.

### <a name="ambari"></a>Ambari

> [!NOTE]
> tooaccess dziennik plików przy użyciu Ambari, należy użyć tunelu SSH. Witaj interfejsów sieci web dla poszczególnych usług hello nie są widoczne publicznie na powitania Internet. Aby uzyskać informacje na temat używania tunelu SSH, zobacz hello [Użyj SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) dokumentu.

Z hello Interfejsu sieci Web Ambari wybierz usługę hello chcesz dzienniki tooview (na przykład YARN). Następnie użyj **szybkie linki** tooselect, które hello tooview węzła głównego w dziennikach.

![Przy użyciu szybkie linki tooview dzienniki](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a>Jak tooconfigure hello rozmiaru węzła

rozmiar Hello węzła można wybrać tylko podczas tworzenia klastra. Można znaleźć listę hello różne rozmiary maszyny Wirtualnej dla usługi HDInsight na powitania [cennikiem usługi HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

Podczas tworzenia klastra, można określić rozmiaru hello hello węzłów. Witaj następujące informacje znajdują się wskazówki dotyczące sposobu przy użyciu rozmiaru hello toospecify hello [portalu Azure][preview-portal], [programu Azure PowerShell][azure-powershell], i hello [interfejsu wiersza polecenia Azure][azure-cli]:

* **Azure portal**: podczas tworzenia klastra, można ustawić rozmiaru hello węzłów hello używane przez klaster hello:

    ![Obraz kreatora tworzenia klastra z węzła rozmiar zaznaczenia](./media/hdinsight-high-availability-linux/headnodesize.png)

* **Azure CLI**: korzystając z hello `azure hdinsight cluster create` polecenia, można ustawić rozmiaru hello hello head, proces roboczy i węzły dozorcy przy użyciu hello `--headNodeSize`, `--workerNodeSize`, i `--zookeeperNodeSize` parametrów.

* **Program Azure PowerShell**: korzystając z hello `New-AzureRmHDInsightCluster` polecenia cmdlet, można ustawić rozmiaru hello hello head, proces roboczy i węzły dozorcy przy użyciu hello `-HeadNodeVMSize`, `-WorkerNodeSize`, i `-ZookeeperNodeSize` parametrów.

## <a name="next-steps"></a>Następne kroki

Użyj powitania po toolearn łącza więcej informacji na temat rzeczy, o których wspomniano w tym dokumencie.

* [Dokumentacja REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [Instalowanie i konfigurowanie hello wiersza polecenia platformy Azure](../cli-install-nodejs.md)
* [Zainstaluj i skonfiguruj program Azure PowerShell](/powershell/azure/overview)
* [Zarządzanie HDInsight przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md)
* [Obsługa administracyjna klastrów HDInsight opartych na systemie Linux](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
