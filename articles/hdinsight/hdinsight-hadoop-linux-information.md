---
title: "aaaTips dotyczące korzystania z usługi Hadoop w usłudze HDInsight opartych na systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Implementacja porady dotyczące korzystania z klastrów opartych na systemie Linux usługą HDInsight (Hadoop) w znanym środowisku Linux uruchomionych w hello chmury Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c41c611c-5798-4c14-81cc-bed1e26b5609
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: a555622605079c9beae88ece872042e36d540c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="information-about-using-hdinsight-on-linux"></a>Informacje dotyczące korzystania z usługi HDInsight w systemie Linux

Azure klastry HDInsight zapewniają Hadoop w znanym środowisku Linux uruchomionych w hello chmury Azure. Dla większości zadań powinny działać dokładnie w żadnej instalacji platformy Hadoop w systemie Linux. Ten dokument uwidacznia poznać konkretne różnice, które należy zwrócić uwagę.

> [!IMPORTANT]
> Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="prerequisites"></a>Wymagania wstępne

Wiele z hello kroków w tym dokumencie za pomocą hello następujące narzędzia, które może być konieczne toobe zainstalowanych w systemie.

* [cURL](https://curl.haxx.se/) -używać toocommunicate z usług sieci web
* [jq](https://stedolan.github.io/jq/) -używanych dokumentów JSON tooparse
* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) (wersja zapoznawcza) — używane tooremotely zarządzania usługami platformy Azure

## <a name="users"></a>Użytkownicy

O ile [przyłączonych do domeny](hdinsight-domain-joined-introduction.md), należy rozważyć HDInsight **pojedynczego użytkownika** systemu. Jednego konta użytkownika SSH jest utworzony z klastrem hello, z poziomu uprawnień administratora. Można utworzyć dodatkowych kont SSH, ale ma także klastra toohello dostępu administratora.

Domeny w usłudze HDInsight obsługuje wielu użytkowników i bardziej szczegółowe ustawienia uprawnień i ról. Aby uzyskać więcej informacji, zobacz [przyłączonych do domeny zarządzania w usłudze hdinsight](hdinsight-domain-joined-manage.md).

## <a name="domain-names"></a>Nazwy domen

Witaj w pełni kwalifikowana toouse nazwa FQDN domeny podczas łączenia z hello jest internet toohello klastra  **&lt;clustername >. azurehdinsight.net** lub (tylko SSH)  **&lt;clustername-ssh >. azurehdinsight.net**.

Wewnętrznie każdy węzeł w klastrze hello ma nazwę, która jest przypisywana podczas konfiguracji klastra. nazwy klastrów hello toofind, zobacz hello **hostów** strony na powitania Interfejsu sieci Web Ambari. Można także użyć powitania po tooreturn listę hostów z interfejsu API REST Ambari hello:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts" | jq '.items[].Hosts.host_name'

Zastąp **hasło** hasłem hello hello konta administratora, i **CLUSTERNAME** o nazwie hello klastra. To polecenie zwraca dokument JSON, który zawiera listę hello hosty w klastrze hello. Jq jest używane tooextract hello `host_name` wartość elementu dla każdego hosta.

Jeśli potrzebujesz toofind hello nazwa węzła powitania dla określonej usługi, można badać Ambari dla tego składnika. Na przykład hostów hello toofind dla węzła nazw systemu plików HDFS hello, użyj hello następujące polecenie:

    curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/NAMENODE" | jq '.host_components[].HostRoles.host_name'

To polecenie zwraca dokument JSON opisujący hello usługi, a następnie jq wysunięcie tylko hello `host_name` wartość hello hostów.

## <a name="remote-access-tooservices"></a>Tooservices dostępu zdalnego

* **Ambari (sieć web)** -https://&lt;clustername >. azurehdinsight.net

    Uwierzytelnianie przy użyciu hello klastra administrator użytkownika i hasło, a następnie zaloguj tooAmbari.

    Uwierzytelnianie w postaci zwykłego tekstu — zawsze użycie protokołu HTTPS toohelp upewnij się, że połączenie hello jest bezpieczne.

    > [!IMPORTANT]
    > Część sieci web hello UI dostępne za pośrednictwem narzędzia Ambari uzyskiwać dostęp do węzłów przy użyciu nazwy domeny wewnętrznej. Domeny wewnętrznej nazwy nie są publicznie dostępna przez hello internet. Błędy "nie można odnaleźć serwera" może zostać wyświetlony podczas próby tooaccess niektóre funkcje za pośrednictwem hello Internet.
    >
    > toouse hello pełną funkcjonalność hello Ambari web UI, użyj SSH tunelu tooproxy web ruchu toohello węzła głównego klastra. Zobacz [Użyj SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie i innych sieci web UI](hdinsight-linux-ambari-ssh-tunnel.md)

* **Ambari (REST)** -https://&lt;clustername >.azurehdinsight.net/ambari

    > [!NOTE]
    > Uwierzytelnianie przy użyciu hello klastra administrator użytkownika i hasła.
    >
    > Uwierzytelnianie w postaci zwykłego tekstu — zawsze użycie protokołu HTTPS toohelp upewnij się, że połączenie hello jest bezpieczne.

* **WebHCat (Templeton)** -https://&lt;clustername >.azurehdinsight.net/templeton

    > [!NOTE]
    > Uwierzytelnianie przy użyciu hello klastra administrator użytkownika i hasła.
    >
    > Uwierzytelnianie w postaci zwykłego tekstu — zawsze użycie protokołu HTTPS toohelp upewnij się, że połączenie hello jest bezpieczne.

* **SSH** - &lt;clustername >-ssh.azurehdinsight.net port 22 i 23. Port 22 jest podstawowy headnode toohello tooconnect używane podczas 23 jest używane tooconnect toohello dodatkowej. Aby uzyskać więcej informacji o węzłach głównych hello, zobacz [dostępność i niezawodność Hadoop clusters w usłudze HDInsight](hdinsight-high-availability-linux.md).

    > [!NOTE]
    > Dostępne są tylko hello głównymi węzłami klastra za pośrednictwem protokołu SSH z komputera klienta. Po nawiązaniu połączenia można następnie dostępu hello węzłów procesu roboczego przy użyciu protokołu SSH z headnode.

## <a name="file-locations"></a>Lokalizacje plików

Pliki związane z platformą Hadoop znajduje się w węzłach klastra hello w `/usr/hdp`. Ten katalog zawiera Witaj podkatalogi następujące:

* **2.2.4.9-1**: Nazwa katalogu hello jest wersja hello hello platformie Hortonworks Data Platform używane przez usługi HDInsight. numer Hello w klastrze może być inny niż hello jedną wymienione w tym miejscu.
* **bieżący**: ten katalog zawiera toosubdirectories łącza w obszarze hello **2.2.4.9-1** katalogu. Ten katalog istnieje, dzięki czemu nie trzeba numer wersji hello tooremember.

Przykładowe dane i pliki JAR znajduje się na rozproszonego systemu plików Hadoop w `/example` i`/HdiSamples`

## <a name="hdfs-azure-storage-and-data-lake-store"></a>System plików HDFS, magazynu Azure i usługi Data Lake Store

W większości dystrybucji Hadoop system plików HDFS nie jest obsługiwana przez magazynu lokalnego na maszynach hello hello klastra. Korzystanie z magazynu lokalnego może być kosztowne rozwiązania oparte na chmurze gdzie są naliczane co godzinę lub za minutę dla zasobów obliczeniowych.

HDInsight używa obiekty BLOB w magazynie Azure albo usługi Azure Data Lake Store jako hello domyślny magazyn. Te usługi zawierają hello następujące korzyści:

* Tanie magazynu długoterminowego
* Ułatwienia dostępu z usług zewnętrznych, takich jak witryny sieci Web, plik przekazywania/Pobierz narzędzia różnych zestawów SDK języka i przeglądarki sieci web

> [!WARNING]
> HDInsight obsługuje tylko __ogólnego przeznaczenia__ konta usługi Azure Storage. Nie obsługuje obecnie hello __magazynu obiektów Blob__ typ konta.

Konto usługi Azure Storage można utrzymanie too4.75 TB, chociaż poszczególne obiekty BLOB (lub pliki z punktu widzenia HDInsight) może jedynie zwiększenie too195 GB. Azure Data Lake Store może zwiększyć się dynamicznie toohold bilionów pliki, z poszczególnych plików przekracza petabajt. Aby uzyskać więcej informacji, zobacz [obiekty BLOB opis](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs) i [usługi Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).

Korzystając z usługi Azure Storage lub Data Lake Store, nie masz toodo jakieś szczególne HDInsight tooaccess hello danych. Na przykład następujące polecenie hello listę plików hello `/example/data` folderu niezależnie od tego, czy jest on przechowywany w magazynie Azure lub usługi Data Lake Store:

    hdfs dfs -ls /example/data

### <a name="uri-and-scheme"></a>Identyfikator URI i schematu

Niektóre polecenia może wymagać toospecify hello schematu jako część hello URI podczas uzyskiwania dostępu do pliku. Na przykład hello składnik systemu plików HDFS Storm wymaga toospecify hello schematu. Korzystając z innych niż domyślne magazynu dodany jako klaster toohello magazynu "dodatkowe", należy zawsze używać hello schematu jako część hello identyfikatora URI.

Korzystając z __usługi Azure Storage__, użyj jednej z następującego schematy identyfikatorów URI hello:

* `wasb:///`: Dostęp do magazynu domyślnego przy użyciu nieszyfrowanego komunikacji.

* `wasbs:///`: Dostęp do magazynu domyślnego za pomocą szyfrowaną komunikację.  Schemat wasbs Hello jest obsługiwana tylko z usługi HDInsight w wersji 3,6 i jego nowszych wersjach.

* `wasb://<container-name>@<account-name>.blob.core.windows.net/`: Używany podczas komunikacji z kontem magazynu innych niż domyślne. Na przykład, jeśli użytkownik ma konto dodatkowego miejsca do magazynowania lub podczas uzyskiwania dostępu do danych przechowywane na koncie magazynu publicznie.

Korzystając z __usługi Data Lake Store__, użyj jednej z następującego schematy identyfikatorów URI hello:

* `adl:///`: Dostęp hello domyślne usługi Data Lake Store hello klastra.

* `adl://<storage-name>.azuredatalakestore.net/`: Używany podczas komunikacji z innych niż domyślne Data Lake Store. Również tooaccess danych znajdujących się poza katalogiem głównym hello z klastrem usługi HDInsight.

> [!IMPORTANT]
> Podczas korzystania z usługi Data Lake Store jako hello domyślny magazyn dla usługi HDInsight, należy określić ścieżkę w ramach toouse magazynu hello jako główny hello magazynu usługi HDInsight. Witaj domyślna ścieżka to `/clusters/<cluster-name>/`.
>
> Korzystając z `/` lub `adl:///` tooaccess danych, użytkownik ma dostęp tylko do danych przechowywanych w katalogu głównym hello (na przykład `/clusters/<cluster-name>/`) hello klastra. dane tooaccess dowolne miejsce w magazynie hello, użyj hello `adl://<storage-name>.azuredatalakestore.net/` format.

### <a name="what-storage-is-hello-cluster-using"></a>Jakie magazynu jest hello klastra przy użyciu

Ambari tooretrieve hello domyślnej magazynu konfiguracji można użyć hello klastra. Użyj następujących hello polecenia przy użyciu programu curl informacje o konfiguracji systemu plików HDFS tooretrieve i filtrować za pomocą [jq](https://stedolan.github.io/jq/):

```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'```

> [!NOTE]
> To polecenie zwróci hello pierwszy serwer toohello zastosowano konfigurację (`service_config_version=1`), który zawiera te informacje. Toolist może być konieczne wszystkie wersje konfiguracji toofind hello najnowszy numer.

To polecenie zwraca wartość toohello podobne, następujące identyfikatory URI:

* `wasb://<container-name>@<account-name>.blob.core.windows.net`Jeśli przy użyciu konta usługi Azure Storage.

    Hello nazwa konta jest hello nazwę konta usługi Azure Storage hello, gdy nazwa kontenera hello jest hello kontenera obiektów blob to główny hello hello magazynu klastra.

* `adl://home`Jeśli przy użyciu usługi Azure Data Lake Store. Nazwa usługi Data Lake Store hello tooget, hello używana po wywołaniu REST:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'```

    To polecenie zwraca następujące nazwy hosta hello: `<data-lake-store-account-name>.azuredatalakestore.net`.

    katalog hello tooget w magazynie hello, który jest głównym powitania dla usługi HDInsight, hello używana po wywołaniu REST:

    ```curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'```

    To polecenie zwraca ścieżkę toohello podobne, ze ścieżką: `/clusters/<hdinsight-cluster-name>/`.

Można również znaleźć informacje o magazynu hello hello portalu Azure przy użyciu hello następujące kroki:

1. W hello [portalu Azure](https://portal.azure.com/), wybierz z klastrem usługi HDInsight.

2. Z hello **właściwości** zaznacz **kont magazynu**. Hello magazynu dla klastra hello są informacje.

### <a name="how-do-i-access-files-from-outside-hdinsight"></a>Jak dostęp do plików z poza HDInsight

Istnieją różne sposoby tooaccess danych z hello poza klastrem usługi HDInsight. Witaj poniżej przedstawiono kilka tooutilities łącza i zestawy SDK, które mogą być używane toowork z danymi:

Jeśli przy użyciu __usługi Azure Storage__, zobacz następujące łącza sposób, że można uzyskać dostępu do danych hello:

* [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2): polecenia interfejsu wiersza polecenia do pracy z platformą Azure. Po zainstalowaniu należy użyć hello `az storage` polecenia, aby uzyskać pomoc na temat używania magazynu, lub `az storage blob` poleceń specyficznych dla obiekt blob.
* [blobxfer.PY](https://github.com/Azure/azure-batch-samples/tree/master/Python/Storage): skryptu python do pracy z obiektami BLOB w usłudze Azure Storage.
* Różne zestawy SDK:

    * [Java](https://github.com/Azure/azure-sdk-for-java)
    * [Node.js](https://github.com/Azure/azure-sdk-for-node)
    * [PHP](https://github.com/Azure/azure-sdk-for-php)
    * [Python](https://github.com/Azure/azure-sdk-for-python)
    * [Ruby](https://github.com/Azure/azure-sdk-for-ruby)
    * [.NET](https://github.com/Azure/azure-sdk-for-net)
    * [Interfejs API REST magazynu](https://msdn.microsoft.com/library/azure/dd135733.aspx)

Jeśli przy użyciu __Azure Data Lake Store__, zobacz następujące łącza sposób, że można uzyskać dostępu do danych hello:

* [Przeglądarki sieci Web](../data-lake-store/data-lake-store-get-started-portal.md)
* [PowerShell](../data-lake-store/data-lake-store-get-started-powershell.md)
* [Interfejs wiersza polecenia platformy Azure 2.0](../data-lake-store/data-lake-store-get-started-cli-2.0.md)
* [Interfejsu API REST WebHDFS](../data-lake-store/data-lake-store-get-started-rest-api.md)
* [Narzędzia Data Lake Tools dla programu Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504)
* [.NET](../data-lake-store/data-lake-store-get-started-net-sdk.md)
* [Java](../data-lake-store/data-lake-store-get-started-java-sdk.md)
* [Python](../data-lake-store/data-lake-store-get-started-python.md)

## <a name="scaling"></a>Skalowanie klastra

Skalowanie funkcji klastra Hello umożliwia toodynamically zmiany hello liczba węzłów danych używane przez klaster. Można wykonywać operacje skalowania podczas innych zadań lub procesów są uruchomione w klastrze.

Witaj różne typy klastrów dotyczy skalowanie w następujący sposób:

* **Hadoop**: podczas skalowania hello liczby węzłów w klastrze, niektóre usługi hello w klastrze hello ponownego uruchomienia. Skalowanie operacji może spowodować zadania uruchomione lub oczekujące toofail na zakończenie hello hello operacji skalowania. Po zakończeniu operacji hello można przesłać ponownie hello zadania.
* **HBase**: serwery regionalne są automatycznie rozmieszczana za kilka minut po zakończeniu operacji skalowania hello. serwery regionalne saldo toomanually, użyj hello następujące kroki:

    1. Połącz toohello klastra usługi HDInsight przy użyciu protokołu SSH. Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

    2. Użyj następującego powłoki HBase hello toostart hello:

            hbase shell

    3. Po załadowaniu hello powłoki HBase, użyj hello następujące serwery regionalne toomanually saldo hello:

            balancer

* **STORM**: należy przeprowadzić ponowne równoważenie wszelkie uruchomione topologie Storm, po wykonaniu operacji skalowania. Ponowne równoważenie pozwala hello topologii tooreadjust równoległości ustawień na podstawie nowych liczby węzłów w klastrze hello hello. toorebalance uruchomionymi topologiami, użyj jednej z hello następujące opcje:

    * **SSH**: połączenia serwera toohello i użyj hello następujące polecenie toorebalance topologii:

            storm rebalance TOPOLOGYNAME

        Można również określić parametry toooverride hello równoległości wskazówek pierwotnie podał hello topologii. Na przykład `storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10` Rekonfiguruj hello procesów roboczych too5 topologii, 3 z modułów wykonujących dla składnika niebieski spout hello i 10 modułów hello żółty bolt składnika.

    * **Interfejsu użytkownika STORM**: Użyj hello następujące czynności toorebalance topologii za pomocą hello interfejsu użytkownika platformy Storm.

        1. Otwórz **https://CLUSTERNAME.azurehdinsight.net/stormui** w przeglądarce sieci web, gdzie CLUSTERNAME jest nazwą hello klastra Storm. Jeśli zostanie wyświetlony monit, wprowadź nazwę administratora (Administrator) klastra usługi HDInsight hello i hasło określone podczas tworzenia klastra hello.
        2. Wybierz topologię hello ma toorebalance, następnie wybierz opcję hello **Rebalance** przycisku. Wprowadź opóźnienie hello, przed wykonaniem operacji Zrównoważ hello.

Aby uzyskać szczegółowe informacje na temat skalowania z klastrem usługi HDInsight zobacz:

* [Zarządzanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu hello portalu Azure](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [Zarządzanie klastrami Hadoop w usłudze HDInsight przy użyciu programu Azure PowerShell](hdinsight-administer-use-command-line.md#scale-clusters)

## <a name="how-do-i-install-hue-or-other-hadoop-component"></a>Jak zainstalować Hue (lub innych składników Hadoop)?

HDInsight to zarządzana usługa. Jeśli Azure wykryje problem z klastrem hello, może usunąć hello awarii węzła i tworzenia tooreplace węzła go. Jeśli musisz ręcznie zainstalować rzeczy w klastrze hello, ich nie są zachowywane podczas tej operacji. Zamiast tego należy użyć [akcji skryptu HDInsight](hdinsight-hadoop-customize-cluster.md). Akcja skryptu można hello toomake używane następujące zmiany:

* Instalowanie i konfigurowanie usługi lub witryny sieci web, takich jak Spark lub Hue.
* Zainstaluj i skonfiguruj składnik, który wymaga zmian konfiguracji na wielu węzłach w klastrze hello. Na przykład zmienna wymagane środowisko, tworzenie katalog rejestrowania i utworzenie pliku konfiguracji.

Akcje skryptu to skrypty Bash. Hello skrypty uruchamiane podczas inicjowania obsługi klastra i można tooinstall używane i konfiguracji dodatkowych składników w klastrze hello. Przykładowe skrypty są dostępne do zainstalowania hello następujące składniki:

* [HUE](hdinsight-hadoop-hue-linux.md)
* [Giraph](hdinsight-hadoop-giraph-install-linux.md)
* [Solr](hdinsight-hadoop-solr-install-linux.md)

Informacje na temat tworzenia własnych akcji skryptu można znaleźć w temacie [Script Action development with HDInsight](hdinsight-hadoop-script-actions-linux.md) (Tworzenie akcji skryptu za pomocą usługi HDInsight).

### <a name="jar-files"></a>Pliki JAR

Niektóre technologie Hadoop znajdują się pliki jar niezależne, które zawierają funkcje używane w ramach zadania MapReduce, lub z wewnątrz Pig lub Hive. Gdy mogą być instalowane za pomocą akcji skryptu, one często nie wymaga żadnej konfiguracji i może być przekazana toohello klastra po zainicjowaniu obsługi administracyjnej i używać bezpośrednio. Jeśli chcesz się, że składnik hello toomake przeżyje ponownym hello klastra, można przechowywać plik jar hello w hello domyślny magazyn dla klastra (WASB lub ADL).

Na przykład, jeśli chcesz, aby toouse hello najnowszą wersję [DataFu](http://datafu.incubator.apache.org/), możesz pobrać jar zawierający projekt hello i przekaż go toohello klastra usługi HDInsight. Następnie wykonaj hello DataFu dokumentacji na temat toouse jej Pig lub Hive.

> [!IMPORTANT]
> Niektóre składniki są pliki jar autonomiczny znajdują się z usługą HDInsight, ale nie znajdują się w ścieżce hello. Jeśli szukasz określonego składnika program hello toosearch wykonaj dla niego w klastrze:
>
> ```find / -name *componentname*.jar 2>/dev/null```
>
> To polecenie zwraca ścieżkę hello pliki jar dopasowania.

toouse innej wersji składnika, wersja hello przekazywania konieczne i korzystać z niego w zadaniach.

> [!WARNING]
> Składniki dostarczony z klastrem usługi HDInsight hello są w pełni obsługiwane i Microsoft Support pomaga tooisolate i rozwiązać problemy toothese powiązane składniki.
>
> Niestandardowe składniki odbierania toohelp Obsługa uzasadnione ekonomicznie toofurther należy rozwiązać problem hello. Może to spowodować nad rozwiązaniem problemu hello lub proszenia tooengage dostępnych kanałów dla hello otwarty technologii źródła wykryto głębokie doświadczenia z tej technologii. Na przykład istnieje wiele witryn społeczności, które mogą być używane, takie jak: [forum MSDN dla usługi HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Projekty Apache mieć witryny projektu na [http://apache.org](http://apache.org), na przykład: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).

## <a name="next-steps"></a>Następne kroki

* [Migrowanie z usługi HDInsight opartych na systemie Windows, na podstawie tooLinux](hdinsight-migrate-from-windows-to-linux.md)
* [Korzystanie z programu Hive z usługą HDInsight](hdinsight-use-hive.md)
* [Korzystanie z języka Pig z usługą HDInsight](hdinsight-use-pig.md)
* [Korzystanie z zadań MapReduce z usługą HDInsight](hdinsight-use-mapreduce.md)
