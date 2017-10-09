---
title: "aaaMigrate z usługi HDInsight opartej na systemie Windows Azure na podstawie tooLinux HDInsight - | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomigrate z usługi HDInsight opartych na systemie Windows klastra tooa opartych na systemie Linux klaster usługi HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>Migracji z klastrze opartych na systemie Linux tooa klastra usługi HDInsight opartej na systemie Windows

Ten dokument zawiera szczegółowe informacje na powitania różnice między HDInsight w systemach Windows i Linux oraz wskazówki toomigrate istniejących obciążeń tooa opartych na systemie Linux klaster.

HDInsight opartych na systemie Windows zapewnia prosty sposób toouse Hadoop w chmurze hello, jednocześnie może być konieczne toomigrate tooa opartych na systemie Linux klaster. Na przykład tootake zaletą opartych na systemie Linux narzędzia i technologie, które są wymagane do rozwiązania. Wiele elementów w ekosystemie Hadoop hello są tworzone w systemach opartych na systemie Linux, a nie mogą być dostępne do użycia z usługą HDInsight z systemu Windows. Ponadto wiele książek, wideo i innych materiałów szkoleniowych założono, że korzystasz z systemu Linux podczas pracy z platformą Hadoop.

> [!NOTE]
> Klastry HDInsight użyć funkcji długoterminowej Ubuntu (LTS) jako system operacyjny hello hello węzłów w klastrze hello. Aby uzyskać informacje na powitania wersję Ubuntu dostępne z usługą HDInsight, oraz inne informacje na temat wersji składnika, zobacz [wersji składnika usługi HDInsight](hdinsight-component-versioning.md).

## <a name="migration-tasks"></a>Zadania migracji

Witaj ogólny przepływ pracy migracji ma następującą składnię.

![Diagram przepływu pracy migracji](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. Przeczytaj toounderstand zmiany, które mogą być wymagane podczas migracji istniejącego przepływu pracy, zadania, itp. tooa opartych na systemie Linux klaster każdej sekcji tego dokumentu.

2. Tworzenie klastra opartych na systemie Linux jako środowiska gwarancji testu/jakości. Aby uzyskać więcej informacji o tworzeniu klastra opartych na systemie Linux, zobacz [opartych na systemie Linux z tworzenia klastrów w usłudze HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Kopia istniejącego zadania, źródła danych i wychwytywanie toohello nowego środowiska.

4. Sprawdzania poprawności testowania toomake się upewnić, że zadaniach działać zgodnie z oczekiwaniami w nowym klastrze hello.

Po upewnieniu się, że wszystko działa zgodnie z oczekiwaniami, należy zaplanować przestój hello migracji. Podczas tego przestojów wykonaj hello następujące akcje:

1. Utwórz kopię zapasową przejściowej dane przechowywane lokalnie na hello węzłów klastra. Jeśli na przykład dane przechowywane bezpośrednio na węzła głównego.

2. Usuwanie klastra z systemem Windows hello.

3. Tworzenie klastra opartych na systemie Linux przy użyciu hello sam domyślny magazyn danych, który hello klastra systemu Windows używane. Hello opartych na systemie Linux klastrów mogą kontynuować pracę z istniejących danych produkcyjnych.

4. Importuj wszystkie przejściowej dane kopii zapasowej.

5. Uruchom zadania/Kontynuuj przetwarzania przy użyciu hello nowego klastra.

### <a name="copy-data-toohello-test-environment"></a>Skopiuj środowisko testowe toohello danych

Istnieje wiele metod toocopy hello danych i zadań, jednak hello dwa omówione w tej sekcji są hello najprostszym metody toodirectly Przenieś pliki tooa klastra testowego.

#### <a name="hdfs-copy"></a>System plików HDFS kopiowania

Użyj poniższych kroków toocopy danych z klastra testowego toohello klastra produkcyjnego hello hello. Kroki przy użyciu hello `hdfs dfs` narzędzia, która jest zawarta w usłudze HDInsight.

1. Informacje hello magazynu konto i domyślny kontener dla istniejącego klastra. Poniższy przykład Hello używa PowerShell tooretrieve tych informacji:

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. toocreate środowiska testowego, wykonaj kroki hello hello klastrów z systemem Linux utworzyć w dokumencie usługi HDInsight. Przed rozpoczęciem tworzenia klastra hello i zamiast tego wybrać **konfiguracji opcjonalnej**.

3. W bloku konfiguracji opcjonalnej hello, wybierz **połączonych kontach magazynu**.

4. Wybierz **Dodaj klucz magazynu**, a po wyświetleniu monitu wybierz hello konta magazynu, który został zwrócony przez hello skrypt programu PowerShell w kroku 1. Kliknij przycisk **wybierz** w każdym bloku. Na koniec Utwórz klaster hello.

5. Po utworzeniu klastra hello łączyć się przy użyciu tooit **SSH.** Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

6. W sesji SSH hello Użyj hello następujące polecenia toocopy pliki z hello połączone magazynu konta toohello nowe domyślne konto magazynu. Zastąp kontenera hello kontenera informacje zwracane przez programu PowerShell. Zastąp __konta__ nazwą konta hello. Zastąp toodata ścieżka hello hello ścieżki tooa danych pliku.

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > Jeśli hello struktury katalogów, zawierający dane hello nie istnieje w środowisku testowym hello, można utworzyć za pomocą następującego polecenia hello:

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    Witaj `-p` przełącznik umożliwia tworzenie hello wszystkie katalogi w ścieżce hello.

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>Bezpośrednie kopiowania między obiekty BLOB w usłudze Azure Storage

Alternatywnie możesz toouse hello `Start-AzureStorageBlobCopy` obiekty BLOB toocopy polecenia cmdlet programu Azure PowerShell między kontami magazynu poza usługą HDInsight. Aby uzyskać więcej informacji, zobacz hello jak toomanage sekcji obiektów blob Azure przy użyciu programu Azure PowerShell z usługą Azure Storage.

## <a name="client-side-technologies"></a>Technologie po stronie klienta

Technologie po stronie klienta, takich jak [poleceń cmdlet programu Azure PowerShell](/powershell/azureps-cmdlets-docs), [interfejsu wiersza polecenia Azure](../cli-install-nodejs.md), lub hello [zestawu .NET SDK dla platformy Hadoop](https://hadoopsdk.codeplex.com/) kontynuować toowork opartych na systemie Linux klastrów. Technologie te są zależne od REST interfejsów API, które są takie same hello obu typów klastra systemu operacyjnego.

## <a name="server-side-technologies"></a>Technologie serwerowe

Witaj w poniższej tabeli znajdują się wskazówki dotyczące migrowania składniki po stronie serwera, które są specyficzne dla systemu Windows.

| Jeśli używasz tej technologii... | Wykonanie tej czynności... |
| --- | --- |
| **PowerShell** (skrypty po stronie serwera, w tym akcji skryptu używane podczas tworzenia klastra) |Ponownego zapisywania jako skrypty Bash. Dla akcji skryptu, zobacz [systemem Linux dostosować usługi HDInsight za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md) i [skryptu programowanie akcji dla usługi HDInsight opartej na systemie Linux](hdinsight-hadoop-script-actions-linux.md). |
| **Azure CLI** (skrypty po stronie serwera) |Chociaż hello wiersza polecenia platformy Azure jest dostępna w systemie Linux, go nie są zainstalowane w głównymi węzłami klastra usługi HDInsight hello. Aby uzyskać więcej informacji na temat instalowania hello wiersza polecenia platformy Azure, zobacz [wprowadzenie Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli). |
| **Składniki platformy .NET** |.NET jest obsługiwana w HDInsight opartych na systemie Linux za pomocą [Mono](https://mono-project.com). Aby uzyskać więcej informacji, zobacz [rozwiązań .NET migracji usługi HDInsight opartej na tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md). |
| **Składniki Win32 lub innych technologii systemu Windows** |Wskazówki dotyczące zależy od składnika hello lub technologii. Może być możliwe toofind wersji, która jest zgodna z systemem Linux lub może muszą toofind alternatywne rozwiązanie lub przepisywania tego składnika. |

> [!IMPORTANT]
> Zarządzanie HDInsight Hello zestawu SDK nie jest całkowicie zgodnej z Mono. Nie należy używać jako część rozwiązania wdrożone toohello klastra usługi HDInsight w tej chwili.

## <a name="cluster-creation"></a>Tworzenie klastra

Ta sekcja zawiera informacje na temat różnic w tworzenia klastra.

### <a name="ssh-user"></a>SSH użytkownika

Klastry usługi HDInsight opartej na systemie Linux Użyj hello **Secure Shell (SSH)** protokołu tooprovide dostępu zdalnego toohello węzłach. W przeciwieństwie do klastrów z systemem Windows dla pulpitu zdalnego większość klientów SSH nie udostępniają graficznego użytkowników. Zamiast tego klientów SSH podać wiersz polecenia, który umożliwia toorun poleceń w klastrze hello. Niektórzy klienci (takich jak [MobaXterm](http://mobaxterm.mobatek.net/)) podaj przeglądarką system plików graficznych w wierszu polecenia zdalnego dodanie tooa.

Podczas tworzenia klastra, należy określić użytkownika SSH i albo **hasło** lub **certyfikatu klucza publicznego** do uwierzytelniania.

Zalecamy używanie certyfikatu klucza publicznego, ponieważ jest bezpieczniejsza niż używanie hasła. Uwierzytelnianie certyfikatu polega na generowanie podpisem pary kluczy publiczny/prywatny, a następnie podając hello klucza publicznego, podczas tworzenia klastra hello. Podczas łączenia z serwerem toohello przy użyciu protokołu SSH, klucza prywatnego hello na powitania klienta zawiera uwierzytelniania dla połączenia hello.

Aby uzyskać więcej informacji, zobacz [Używanie protokołu SSH w usłudze HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

### <a name="cluster-customization"></a>Dostosowywanie klastra

**Akcje skryptu** używane z opartą na systemie Linux klastrów musi być napisana w skrypcie Bash. Chociaż akcji skryptu mogą być używane podczas tworzenia klastra, opartych na systemie Linux klastrów można je również dostosowania tooperform używane po skonfigurowaniu klastra i uruchomiona. Aby uzyskać więcej informacji, zobacz [systemem Linux dostosować usługi HDInsight za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md) i [skryptu programowanie akcji dla usługi HDInsight opartej na systemie Linux](hdinsight-hadoop-script-actions-linux.md).

Jest inna funkcja dostosowywania **bootstrap**. W przypadku klastrów systemu Windows ta funkcja umożliwia lokalizacji hello toospecify dodatkowych bibliotek do użycia z gałęzi. Po utworzeniu klastra biblioteki te są automatycznie dostępne do użycia z zapytań programu Hive bez toouse potrzeby hello `ADD JAR`.

Funkcja ładowania początkowego Hello opartych na systemie Linux klastrów nie udostępnia tę funkcję. Zamiast tego należy użyć akcji skryptu w [dodać Hive bibliotek podczas tworzenia klastra](hdinsight-hadoop-add-hive-libraries.md).

### <a name="virtual-networks"></a>Sieci wirtualne

HDInsight opartych na systemie Windows klastrów działać tylko w przypadku klasycznych sieci wirtualnych, podczas gdy klastrów usługi HDInsight opartych na systemie Linux wymagają sieci wirtualnych Menedżera zasobów. Jeśli masz zasoby w sieci wirtualnej klasycznego hello klastra usługi HDInsight Linux musi nawiązać połączenie, zobacz [łączenie tooa klasycznej sieci wirtualnej sieci wirtualnych Menedżera zasobów](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).

Aby uzyskać więcej informacji dotyczących wymagań konfiguracyjnych dotyczących przy użyciu sieci wirtualnych Azure z usługą HDInsight, zobacz [możliwości rozszerzania HDInsight przy użyciu sieci wirtualnej](hdinsight-extend-hadoop-virtual-network.md).

## <a name="management-and-monitoring"></a>Zarządzanie i monitorowanie

Wiele hello web UI użyto z HDInsight opartych na systemie Windows, takich jak Historia zadań lub Yarn interfejsu użytkownika, są dostępne za pośrednictwem narzędzia Ambari. Ponadto hello widoku Hive narzędzia Ambari zapewnia toorun sposób zapytań Hive przy użyciu przeglądarki sieci web. Hello Interfejsu sieci Web Ambari jest dostępna w klastrach opartych na systemie Linux na https://CLUSTERNAME.azurehdinsight.net.

Aby uzyskać więcej informacji na temat pracy z narzędzia Ambari Zobacz hello w następujących dokumentach:

* [Ambari Web](hdinsight-hadoop-manage-ambari.md)
* [Interfejs API REST Ambari](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Alerty Ambari

Ambari ma system alertów można ustalić o potencjalnych problemach z klastrem hello. Alerty są wyświetlane jako czerwony lub żółty wpisów w hello Interfejsu sieci Web Ambari, jednak może również pobierać za pośrednictwem hello interfejsu API REST.

> [!IMPORTANT]
> Alerty Ambari wskazują, że istnieje *może* to stanowić problem, nie czy nie *jest* problem. Na przykład otrzymasz alert, że nie można uzyskać dostępu do serwera HiveServer2, mimo że można do niego dostęp normalnie.
>
> Wiele alertów są zaimplementowane jako określonych odstępach czasu zapytań dotyczących usługi i oczekują odpowiedzi w określonym przedziale czasu. Tak hello alert nie musi oznaczać, że hello usługa działa, po prostu, że nie zwróciło wyników w okresie hello oczekiwano.

Należy ocenić, czy alert występuje od dłuższego czasu lub odzwierciedla problemów użytkownika, które zostały zgłoszone przed wykonaniem akcji na nim.

## <a name="file-system-locations"></a>Lokalizacje w systemie plików

Witaj system plików klastra systemu Linux jest rozmieszczona inaczej niż klastrów usługi HDInsight opartych na systemie Windows. Użyj hello następujące pliki toofind często używane w tabeli.

| Potrzebuję toofind... | Jest on umieszczony... |
| --- | --- |
| Konfiguracja |`/etc`. Na przykład: `/etc/hadoop/conf/core-site.xml` |
| Pliki dziennika |`/var/logs` |
| Hortonworks Data Platform (HDP) |`/usr/hdp`. Istnieją dwa katalogi znajduje się w tym miejscu jest bieżąca wersja HDP hello i `current`. Witaj `current` katalog zawiera toofiles łącza symbolicznego i znajdującego się w katalogu numer wersji hello katalogów. Witaj `current` katalogu została podana jako wygodny sposób uzyskiwania dostępu do plików HDP od zmiany numeru wersji hello jako hello HDP wersja jest aktualizowana. |
| hadoop streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

Ogólnie rzecz biorąc Jeśli znasz nazwę hello hello pliku można użyć następującego polecenia ze ścieżki plików hello toofind sesji SSH hello:

    find / -name FILENAME 2>/dev/null

Można również użyć symboli wieloznacznych, z nazwą pliku hello. Na przykład `find / -name *streaming*.jar 2>/dev/null` zwraca pliki jar, które zawierają hello word strumienia, jako część nazwy pliku hello hello tooany ścieżki.

## <a name="hive-pig-and-mapreduce"></a>Hive, Pig i MapReduce

Pig i MapReduce obciążeń są podobne w klastrach opartych na systemie Linux. Jednak klastrów usługi HDInsight opartych na systemie Linux mogą być tworzone przy użyciu nowszej wersji platformy Hadoop, Hive i Pig. Te różnice wersji może spowodować zmiany w sposób istniejących funkcji rozwiązania. Aby uzyskać więcej informacji na powitania wersji składników zawartych z usługą HDInsight, zobacz [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md).

HDInsight opartych na systemie Linux nie zapewnia funkcje pulpitu zdalnego. Zamiast tego można użyć SSH tooremotely połączyć toohello głównymi węzłami klastra. Aby uzyskać więcej informacji zobacz hello w następujących dokumentach:

* [Korzystanie z programu Hive przy użyciu protokołu SSH](hdinsight-hadoop-use-hive-ssh.md)
* [Korzystanie z języka Pig przy użyciu protokołu SSH](hdinsight-hadoop-use-pig-ssh.md)
* [Korzystać z usługi MapReduce przy użyciu protokołu SSH](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> Jeśli używasz zewnętrznego potrzeby magazynu metadanych Hive, przed użyciem go z opartą na systemie Linux usługą HDInsight należy kopię zapasową hello potrzeby magazynu metadanych. HDInsight opartych na systemie Linux jest dostępna z nowszymi wersjami programu Hive, który może mieć niezgodności z magazyny utworzone we wcześniejszych wersjach.

powitania po wykresu znajdują się wskazówki dotyczące migracji obciążeń Hive.

| Na podstawie systemu Windows, używać... | Na opartych na systemie Linux... |
| --- | --- |
| **Edytor hive** |[Widok hive narzędzia Ambari](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Tez hello domyślnego wykonywania aparatu opartych na systemie Linux klastrów, więc hello set — instrukcja nie jest już potrzebne. |
| C# zdefiniowane przez użytkownika funkcji | Uzyskać informacji dotyczących sprawdzania poprawności składniki C# z opartą na systemie Linux usługą HDInsight, zobacz [rozwiązań .NET migracji usługi HDInsight opartej na tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| Pliki CMD lub skryptów na powitania serwera wywołany jako część zadania Hive |Użyj skrypty powłoki systemowej |
| `hive`polecenie z pulpitu zdalnego |Użyj [Beeline](hdinsight-hadoop-use-hive-beeline.md) lub [Hive w sesji SSH](hdinsight-hadoop-use-hive-ssh.md) |

### <a name="pig"></a>Pig

| Na podstawie systemu Windows, używać... | Na opartych na systemie Linux... |
| --- | --- |
| C# zdefiniowane przez użytkownika funkcji | Uzyskać informacji dotyczących sprawdzania poprawności składniki C# z opartą na systemie Linux usługą HDInsight, zobacz [rozwiązań .NET migracji usługi HDInsight opartej na tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| Pliki CMD lub skryptów na powitania serwera wywołany jako część zadania Pig |Użyj skrypty powłoki systemowej |

### <a name="mapreduce"></a>MapReduce

| Na podstawie systemu Windows, używać... | Na opartych na systemie Linux... |
| --- | --- |
| C# mapowania i reduktor składników | Uzyskać informacji dotyczących sprawdzania poprawności składniki C# z opartą na systemie Linux usługą HDInsight, zobacz [rozwiązań .NET migracji usługi HDInsight opartej na tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| Pliki CMD lub skryptów na powitania serwera wywołany jako część zadania Hive |Użyj skrypty powłoki systemowej |

## <a name="oozie"></a>Oozie

> [!IMPORTANT]
> Jeśli używasz zewnętrznego potrzeby magazynu metadanych Oozie, przed użyciem go z usługi HDInsight opartej na systemie Linux należy kopię zapasową hello potrzeby magazynu metadanych. HDInsight opartych na systemie Linux jest dostępna z nowszymi wersjami programu Oozie, który może mieć niezgodności z magazyny utworzone we wcześniejszych wersjach.

Przepływy pracy Oozie umożliwiają akcji powłoki. Działania powłoki hello domyślną powłokę przy użyciu poleceń wiersza polecenia toorun systemu operacyjnego hello. Jeśli masz Oozie przepływy pracy, które opierają się na powitania powłoki systemu Windows muszą zmodyfikować hello toorely przepływów pracy w środowisku powłoki systemu Linux hello (Bash). Aby uzyskać więcej informacji o używaniu akcje powłoki z Oozie zobacz [rozszerzenie akcji powłoki Oozie](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html).

Jeśli masz Oozie przepływy pracy, które opierają się na aplikacji C# wywołane przez akcje powłoki, należy sprawdzić te aplikacje w środowisku systemu Linux. Aby uzyskać więcej informacji, zobacz [rozwiązań .NET migracji usługi HDInsight opartej na tooLinux](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="storm"></a>Storm

| Na podstawie systemu Windows, używać... | Na opartych na systemie Linux... |
| --- | --- |
| Pulpit nawigacyjny STORM |pulpit nawigacyjny Storm Hello jest niedostępna. Zobacz [topologie wdrażania i zarządzania Storm w usłudze HDInsight z systemem Linux](hdinsight-storm-deploy-monitor-topology-linux.md) dla metody toosubmit topologie |
| STORM interfejsu użytkownika |Witaj interfejsu użytkownika platformy Storm jest dostępne pod adresem https://CLUSTERNAME.azurehdinsight.net/stormui |
| Visual Studio toocreate, wdrażanie i zarządzanie nimi C# i hybrydowych topologii |Visual Studio może być używane toocreate, wdrażania i zarządzania języka C# (SCP.NET) lub hybrydowe topologie na Storm opartej na systemie Linux w klastrach HDInsight utworzone po 10/28/2016. |

## <a name="hbase"></a>HBase

W klastrach opartych na systemie Linux, hello znode nadrzędnej bazy danych hbase jest `/hbase-unsecure`. Ustaw tę wartość w konfiguracji hello aplikacje klienta Java korzystających z natywnego interfejsu API języka Java HBase.

Zobacz [tworzenia aplikacji opartych na języku Java HBase](hdinsight-hbase-build-java-maven.md) dla klienta przykład ustawiający tę wartość.

## <a name="spark"></a>platforma Spark

Klastry Spark były dostępne w klastrach z systemem Windows w wersji zapoznawczej. Spark GA jest dostępna tylko w klastrach opartych na systemie Linux. Brak nie ścieżki migracji z klastra Spark opartych na systemie Linux wersji tooa klastra Spark opartych na systemie Windows w wersji zapoznawczej.

## <a name="known-issues"></a>Znane problemy

### <a name="azure-data-factory-custom-net-activities"></a>Azure fabryki danych niestandardowych działań platformy .NET

Azure fabryki danych niestandardowych działań platformy .NET nie są obecnie obsługiwane w klastrach HDInsight opartych na systemie Linux. Zamiast tego należy użyć jednej z hello następujące metody tooimplement niestandardowych działań w ramach planowaną ADF.

* Wykonanie działań platformy .NET w puli partii zadań Azure. W sekcji hello partii zadań Azure Użyj połączone usługi [skorzystać z działań niestandardowych w potoku fabryki danych Azure](../data-factory/data-factory-use-custom-activities.md)
* Implementuje hello działania jako działania MapReduce. Aby uzyskać więcej informacji, zobacz [wywołania programy MapReduce z fabryki danych](../data-factory/data-factory-map-reduce.md).

### <a name="line-endings"></a>Zakończenia wierszy

Ogólnie rzecz biorąc zakończenia wierszy na komputerach z systemem Windows użyj CRLF, podczas gdy LF systemów opartych na systemie Linux. Tworzy, czy oczekiwane dane z końców CRLF, może być konieczne toomodify toowork producenci i konsumenci hello z hello LF wiersza końcowego.

Na przykład usługi HDInsight w klastrze z systemem Windows przy użyciu programu Azure PowerShell tooquery zwraca dane z CRLF. Witaj tego samego zapytania z klastrem opartych na systemie Linux zwraca wysuwu wiersza. Jeśli hello wiersza końcowego powoduje, że problem z Twojej solutuion przed przeprowadzeniem migracji należy przetestować toosee tooa opartych na systemie Linux klaster.

Jeśli masz skrypty, które są wykonywane bezpośrednio na węzłach klastra Linux hello, zawsze należy używać LF jako hello zakończenia linii. Jeśli używasz CRLF, mogą zostać wyświetlone błędy podczas uruchamiania skryptów hello na klastrze z systemem Linux.

Jeśli znasz hello skrypty nie zawierają ciągi zawierające osadzonych znaków powrotu Karetki, można zbiorczo zakończenia wierszy hello zmiany przy użyciu jednej z następujących metod hello:

* **Przed przekazaniem klastra toohello**: hello Użyj poniższych zakończenia wierszy hello toochange instrukcje programu PowerShell z CRLF tooLF przed przekazaniem hello skryptu toohello klastra.

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **Po przekazaniu klastra toohello**: Użyj hello następujące polecenie z toohello sesji SSH opartych na systemie Linux klaster toomodify hello skryptu.

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się, jak toocreate opartych na systemie Linux klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md)
* [Użyj SSH tooconnect tooHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
* [Zarządzanie klastrem opartych na systemie Linux przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md)
