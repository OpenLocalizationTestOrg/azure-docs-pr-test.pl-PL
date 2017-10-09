---
title: "Programowanie akcji aaaScript z usługą HDInsight opartą na systemie Linux - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Bash skrypty toocustomize opartych na systemie Linux klastrów usługi HDInsight. Hello funkcji Akcja skryptu HDInsight umożliwia skrypty toorun podczas lub po utworzeniu klastra. Skrypty można toochange używanych ustawień konfiguracji klastra lub zainstalować dodatkowe oprogramowanie."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>Tworzenie akcji skryptu za pomocą usługi HDInsight

Dowiedz się, jak użyciu klastra usługi HDInsight Bash toocustomize skryptów. Akcje skryptu to sposób toocustomize HDInsight podczas lub po utworzeniu klastra.

> [!IMPORTANT]
> kroki Hello w tym dokumencie wymagają klastra usługi HDInsight, który używa systemu Linux. Linux jest hello tylko system operacyjny używany w usłudze HDInsight w wersji 3.4 lub nowszej. Aby uzyskać więcej informacji, zobacz sekcję [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Wycofanie usługi HDInsight w systemie Windows).

## <a name="what-are-script-actions"></a>Co to są akcji skryptu

Akcje skryptu to skrypty Bash, które Azure działa na zmiany konfiguracji toomake węzłów klastra hello ani instalować oprogramowania. Akcja skryptu jest wykonywany jako główny i zapewnia pełny dostęp węzłów klastra toohello praw.

Akcje skryptu można zastosować za pośrednictwem hello następujące metody:

| Użyj tej metody tooapply skryptu... | Tworzenie klastra podczas... | W klastrze uruchomione... |
| --- |:---:|:---:|
| Azure Portal |✓ |✓ |
| Azure PowerShell |✓ |✓ |
| Interfejs wiersza polecenia platformy Azure |&nbsp; |✓ |
| Zestaw SDK dla platformy .NET usługi HDInsight |✓ |✓ |
| Szablonu usługi Azure Resource Manager |✓ |&nbsp; |

Aby uzyskać więcej informacji na za pomocą akcji skryptu tooapply tych metod, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Najlepsze rozwiązania dotyczące tworzenia skryptów

Podczas opracowywania niestandardowego skryptu dla klastra usługi HDInsight są kilka tookeep najlepszych praktyk pamiętać:

* [Docelowa wersja platformy Hadoop hello](#bPS1)
* [Witaj docelowej wersji systemu operacyjnego](#bps10)
* [Znajdują się stabilne łączy tooscript zasoby](#bPS2)
* [Użyj wstępnie skompilowanym zasobów](#bPS4)
* [Upewnij się, że hello klastra dostosowywania skryptu jest idempotentności](#bPS3)
* [Zapewni to wysoką dostępność hello architektury klastra](#bPS5)
* [Konfigurowanie magazynu obiektów Blob platformy Azure toouse niestandardowych składników hello](#bPS6)
* [Zapis tooSTDOUT informacji i STDERR.](#bPS7)
* [Zapisz pliki jako ASCII z końców LF](#bps8)
* [Użyj toorecover logiki ponownych prób w przypadku błędów przejściowych](#bps9)

> [!IMPORTANT]
> Akcje skryptu musi zostać zakończone w ciągu 60 minut lub hello proces zakończy się niepowodzeniem. Podczas inicjowania obsługi węzła, hello skrypt jest uruchamiany równocześnie z innymi procesami instalacji i konfiguracji. Konkurowanie o zasoby, takie jak czas lub sieci przepustowości Procesora może powodować hello skryptu tootake dłużej toofinish niż w środowisku projektowania.

### <a name="bPS1"></a>Docelowa wersja platformy Hadoop hello

Różne wersje HDInsight korzystają z różnych wersji usług Hadoop i zainstalowanych składników. Jeśli skrypt oczekuje określoną wersję usługi lub składnika, skrypt hello należy używać tylko z wersją hello HDInsight zawierającym hello wymagane składniki. Informacje można znaleźć w wersji składników dołączone do usługi HDInsight przy użyciu hello [przechowywanie wersji składnika usługi HDInsight](hdinsight-component-versioning.md) dokumentu.

### <a name="bps10"></a>Docelowa wersja hello systemu operacyjnego

HDInsight opartych na systemie Linux jest oparta na powitania dystrybucji Ubuntu Linux. Różnych wersji usługi hdinsight korzystają z różnych wersji systemu Ubuntu, która może zmienić sposób działania skryptu. Na przykład HDInsight 3.4 i starsze wersje są oparte na wersji Ubuntu, które używają Upstart. Wersja 3.5 jest oparta na 16.04 Ubuntu, który używa Systemd. Systemd i Upstart zależne inne polecenia, aby skrypt powinien być zapisywany toowork zarówno.

Inna ważna różnica między HDInsight 3.4 i 3.5 jest to, że `JAVA_HOME` teraz punkty tooJava 8.

Wersja systemu operacyjnego hello można sprawdzić za pomocą `lsb_release`. Witaj poniższy kod przedstawia sposób toodetermine Jeśli hello skryptu systemem Ubuntu 14 lub 16:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

Można znaleźć hello pełne skrypt, który zawiera te wstawki na https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.

Wersję hello Ubuntu, który jest używany przez usługi HDInsight, zobacz hello [składnika usługi HDInsight w wersji](hdinsight-component-versioning.md) dokumentu.

toounderstand hello różnice między Systemd i Upstart, zobacz [Systemd dla użytkowników Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Znajdują się stabilne łączy tooscript zasoby

Witaj skrypt i skojarzonych zasobów musi być dostępna przez cały okres istnienia hello hello klastra. Te zasoby są wymagane, jeśli zostaną dodane nowe węzły klastra toohello podczas operacji skalowania.

Witaj, najlepszym rozwiązaniem jest toodownload i zarchiwizowanie wszystkich na koncie magazynu Azure w ramach subskrypcji.

> [!IMPORTANT]
> Konto magazynu Hello używane musi być hello domyślne konto magazynu dla klastra hello lub kontener publiczne, tylko do odczytu na inne konto magazynu.

Na przykład przykłady hello obsługiwane przez firmę Microsoft są przechowywane w hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) konta magazynu. Jest obsługiwana przez zespół usługi HDInsight hello kontener publiczne, tylko do odczytu.

### <a name="bPS4"></a>Użyj wstępnie skompilowanym zasobów

tooreduce hello czasu zajmuje toorun hello skryptu, uniknąć operacji kompilowane zasobów z kodu źródłowego. Na przykład wstępnie skompilować zasobów i zapisanie ich w obiekcie blob konta usługi Azure Storage w hello tego samego centrum danych, w usłudze HDInsight.

### <a name="bPS3"></a>Upewnij się, że hello klastra dostosowywania skryptu jest idempotentności

Skrypty musi być idempotentności. Jeśli hello skrypt jest uruchamiany wiele razy, powinien on zwrócić hello sam stan zawsze toohello klastra.

Na przykład skrypt, który modyfikuje pliki konfiguracji nie dodać zduplikowanych wpisów, gdy uruchomiono wiele razy.

### <a name="bPS5"></a>Zapewni to wysoką dostępność hello architektury klastra

Klastry HDInsight opartych na systemie Linux zapewniają dwa węzły head, które są aktywne w ramach klastra hello, a akcji skryptu, uruchom na obu węzłów. Jeżeli hello składniki, które można zainstalować tylko jednego węzła głównego, nie należy instalować na obu węzłów głównych hello składników.

> [!IMPORTANT]
> Usługi w ramach usługi HDInsight są zaprojektowane toofail za pośrednictwem, między dwoma węzłami head hello, zgodnie z potrzebami. Ta funkcja nie jest przedłużana toocustom składniki zainstalowane za pomocą akcji skryptu. Jeśli potrzebujesz wysokiej dostępności dla niestandardowych składników, musisz zaimplementować własny mechanizm pracy awaryjnej.

### <a name="bPS6"></a>Konfigurowanie magazynu obiektów Blob platformy Azure toouse niestandardowych składników hello

Składniki, które można zainstalować w klastrze hello może mieć konfigurację domyślną, która korzysta z magazynu systemu Distributed plików Hadoop (HDFS). HDInsight używa magazynu Azure lub usługi Data Lake Store jako hello domyślny magazyn. Podaj zarówno systemu plików zgodny system plików HDFS, który będzie się powtarzać danych, nawet jeśli klaster hello jest usunięty. Może być konieczne składniki tooconfigure zainstalować toouse WASB lub ADL zamiast systemu plików HDFS.

Dla większości operacji nie trzeba toospecify hello w systemie plików. Na przykład następujące hello kopiuje plik giraph-examples.jar hello z hello pliku lokalnego systemu toocluster magazynu:

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

W tym przykładzie hello `hdfs` polecenie niewidocznie używa magazynu klastra hello domyślne. Dla niektórych operacji może być konieczne hello toospecify identyfikatora URI. Na przykład `adl:///example/jars` dla usługi Data Lake Store lub `wasb:///example/jars` usługi Azure Storage.

### <a name="bPS7"></a>Zapis tooSTDOUT informacji i STDERR.

HDInsight rejestruje dane wyjściowe skryptu jest zapisywane tooSTDOUT i STDERR. Można wyświetlić te informacje przy użyciu hello Ambari web UI.

> [!NOTE]
> Ambari jest dostępna tylko jeśli hello klaster został utworzony pomyślnie. Jeśli używasz akcji skryptu podczas tworzenia klastra i utworzenie kończy się niepowodzeniem, zobacz hello Rozwiązywanie problemów z sekcji [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) dotyczące innych metod uzyskiwania dostępu do zarejestrowane informacje.

Większość narzędzi i pakiety instalacyjne już zapisu tooSTDOUT informacji i STDERR, jednak może być tooadd dodatkowe rejestrowanie. toosend tekst tooSTDOUT, użyj `echo`. Na przykład:

```bash
echo "Getting ready tooinstall Foo"
```

Domyślnie `echo` wysyła hello tooSTDOUT ciągu. toodirect go tooSTDERR, Dodaj `>&2` przed `echo`. Na przykład:

```bash
>&2 echo "An error occurred installing Foo"
```

To przekierowuje informacje zapisane zamiast tooSTDERR tooSTDOUT (2). Aby uzyskać więcej informacji dotyczących przekierowania we/wy, zobacz [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Aby uzyskać więcej informacji o wyświetlaniu informacji zarejestrowanych przez akcje skryptu, zobacz [HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a>Zapisz pliki jako ASCII z końców LF

Skrypty powłoki systemowej powinny być przechowywane w formacie ASCII, liniami został przerwany przez wysuwu wiersza. Pliki, które są przechowywane w formacie UTF-8, lub użyj CRLF jako zakończenie wiersza hello może zakończyć się niepowodzeniem z hello następujący błąd:

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>Użyj toorecover logiki ponownych prób w przypadku błędów przejściowych

Podczas pobierania plików, instalowanie pakietów przy użyciu stanie get lub innych działań, których dane są przesyłane za pośrednictwem hello internet, akcja hello może zakończyć się niepowodzeniem ze względu na błędy łączności sieciowej tootransient. Na przykład zasób zdalny hello, które komunikują się z może być w procesie hello niepowodzenie nad węzłem kopii zapasowej tooa.

toomake tootransient odporność błędy skryptu, można implementację logiki ponawiania próby. powitania po funkcja pokazano, jak Logika ponawiania próby tooimplement. Ponowną operacji hello trzy razy przed niepowodzeniem.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

Witaj poniższe przykłady pokazują, jak toouse tej funkcji.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>Metody pomocnicze dla niestandardowych skryptów

Metody pomocnicze akcji skryptu są narzędzia, które można użyć podczas pisania skryptów niestandardowych. Te metody są zawarte w[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) skryptu. Użyj następującego toodownload hello i używać ich jako część skryptu:

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

powitania po pomocników dostępne do użycia w skrypcie:

| Użycie pomocnika | Opis |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Pobiera plik z hello źródła identyfikatora URI toohello określona ścieżka pliku. Domyślnie go nie zastępuj istniejącego pliku. |
| `untar_file TARFILE DESTDIR` |Wyodrębnia plik tar (przy użyciu `-xf`) toohello katalogu docelowego. |
| `test_is_headnode` |Jeśli został uruchomiony na węzła głównego klastra zwracany 1; w przeciwnym razie wartość 0. |
| `test_is_datanode` |W przypadku hello bieżący węzeł jest węzłem danych (proces roboczy), zwraca 1; w przeciwnym razie wartość 0. |
| `test_is_first_datanode` |W przypadku bieżącego węzła hello jest pierwsze dane hello (proces roboczy) węzła (o nazwie workernode0) zwraca 1; w przeciwnym razie wartość 0. |
| `get_headnodes` |Zwraca nazwę FQDN hello hello headnodes hello klastra. Nazwy są rozdzielone przecinkami. Ciąg pusty jest zwracana w przypadku błędu. |
| `get_primary_headnode` |Pobiera nazwę FQDN hello hello headnode podstawowego. Ciąg pusty jest zwracana w przypadku błędu. |
| `get_secondary_headnode` |Pobiera nazwę FQDN hello hello headnode dodatkowej. Ciąg pusty jest zwracana w przypadku błędu. |
| `get_primary_headnode_number` |Pobiera sufiks numeryczny hello z hello headnode podstawowego. Ciąg pusty jest zwracana w przypadku błędu. |
| `get_secondary_headnode_number` |Pobiera sufiks numeryczny hello z hello headnode dodatkowej. Ciąg pusty jest zwracana w przypadku błędu. |

## <a name="commonusage"></a>Wspólne wzorce użycia

Ta sekcja zawiera wskazówki dotyczące implementowania niektóre hello typowe wzorce użycia, które możesz napotkać podczas pisania skryptu niestandardowego.

### <a name="passing-parameters-tooa-script"></a>Przekazywanie parametrów tooa skryptu

W niektórych przypadkach skrypt może wymagać parametrów. Na przykład mogą być potrzebne hasło administratora hello hello klastra, korzystając z interfejsu API REST Ambari hello.

Parametry przekazywane do skryptu toohello są określane jako *parametrów pozycyjnych*i są przydzielane za`$1` dla pierwszego parametru hello `$2` dla hello drugi i tak w przypadku. `$0`zawiera nazwę hello hello sam skrypt.

Wartości przekazane jako parametry skryptu toohello powinna zostać ujęta w pojedynczym cudzysłowie ('). Daje to gwarancję, że hello przekazana wartość jest traktowany jako literału.

### <a name="setting-environment-variables"></a>Ustawianie zmiennych środowiskowych

Ustawienie zmiennej środowiskowej jest wykonywane przez hello następującej instrukcji:

    VARIABLENAME=value

Gdzie NAZWA_ZMIENNEJ to nazwa hello hello zmiennej. Użycie zmiennej, hello tooaccess `$VARIABLENAME`. Na przykład tooassign dla wartości dostarczonej przez parametrów pozycyjnych jako zmienną środowiskową o nazwie HASŁA, należy użyć następującej instrukcji hello:

    PASSWORD=$1

Dostęp do informacji toohello można następnie użyć `$PASSWORD`.

Zmienne środowiskowe w hello skrypt istnieje tylko w zakresie hello hello skryptu. W niektórych przypadkach może być konieczne tooadd zmiennych środowiskowych całego systemu, które pozostają po zakończeniu działania skryptu hello. zmienne środowiskowe systemowe tooadd, Dodaj zmienną hello zbyt`/etc/environment`. Na przykład dodaje powitania po instrukcji `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Gdzie są przechowywane niestandardowe skrypty hello toolocations dostępu

Skrypty używane toocustomize klastra musi toobe przechowywane w jednej z następujących lokalizacji hello:

* __Konta magazynu Azure__ skojarzonego z klastrem hello.

* __Konta magazynu dodatkowe__ skojarzony z klastrem hello.

* A __publicznie można odczytać identyfikatora URI__. Na przykład adres URL toodata przechowywane na OneDrive, Dropbox lub innych plików usługi hosta.

* __Konta usługi Azure Data Lake Store__ skojarzonego z klastrem usługi HDInsight hello. Aby uzyskać więcej informacji na temat używania usługi Azure Data Lake Store z usługą HDInsight, zobacz [tworzenia klastra usługi HDInsight z usługą Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    > [!NOTE]
    > Hello usługi głównej HDInsight używa tooaccess Data Lake — Magazyn musi mieć dostęp do odczytu toohello skryptu.

Zasoby używane przez skrypt hello również musi być publicznie dostępny.

Przechowywanie plików hello w koncie magazynu Azure lub usługi Azure Data Lake Store zapewnia szybki dostęp, jako zarówno w ramach hello sieć platformy Azure.

> [!NOTE]
> w zależności od używanej usługi hello różni się Hello skryptu hello tooreference formatu identyfikatora URI. Dla konta magazynu skojarzone z klastrem usługi HDInsight hello, użyj `wasb://` lub `wasbs://`. Identyfikatory URI publicznie do odczytu, użyj `http://` lub `https://`. Data Lake Store, użyj `adl://`.

### <a name="checking-hello-operating-system-version"></a>Sprawdzanie wersji systemu operacyjnego hello

Różne wersje HDInsight korzystają z określonych wersji systemu Ubuntu. Może to być różnice między systemami Operacyjnymi, które muszą sprawdzaj w skrypcie. Na przykład może być konieczne tooinstall pliku binarnego, który jest wersja wiązanej toohello Ubuntu.

toocheck wersji hello systemu operacyjnego, użyj `lsb_release`. Na przykład hello następującego skryptu pokazano, jak tooreference tar określonego pliku w zależności od wersji systemu operacyjnego hello:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>Lista kontrolna wdrażania akcji skryptu

Poniżej przedstawiono kroki hello Wybraliśmy podczas przygotowywania toodeploy te skrypty:

* Umieść hello pliki, które zawierają hello niestandardowych skryptów w miejscu, który jest dostępny dla węzłów klastra hello podczas wdrażania. Na przykład hello domyślny magazyn dla klastra hello. Pliki mogą być również przechowywane w publicznie do odczytu usług hostingu.
* Sprawdź, czy skrypt hello impotent. Dzięki temu toobe skryptu hello wykonywane wiele razy na powitania sam węzeł.
* Użyj pliku tymczasowego katalogu /tmp tookeep hello pobrane pliki używane przez skrypty hello i następnie wyczyść je po wykonaniu skryptów.
* Jeśli ustawienia na poziomie systemu operacyjnego lub plików konfiguracyjnych usługi Hadoop są zmieniane, możesz toorestart usługi HDInsight.

## <a name="runScriptAction"></a>Jak toorun akcji skryptu

Można użyć skryptu akcje toocustomize klastrów usługi HDInsight przy użyciu hello następujące metody:

* Azure Portal
* Azure PowerShell
* Szablony usługi Azure Resource Manager
* Witaj zestawu .NET SDK usługi HDInsight.

Aby uzyskać więcej informacji na temat używania każdej z metod, zobacz [jak toouse skryptu akcji](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Przykłady niestandardowych skryptów

Firma Microsoft udostępnia przykładowe skrypty tooinstall składników w klastrze usługi HDInsight. Zobacz następujące łącza więcej akcji skryptu przykład hello.

* [Zainstalować i używać Hue w klastrach HDInsight](hdinsight-hadoop-hue-linux.md)
* [Zainstalować i używać Solr w klastrach HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Zainstalować i używać Giraph w klastrach HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Zainstaluj lub Uaktualnij Mono w klastrach HDInsight](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>Rozwiązywanie problemów

błędy, które mogą wystąpić podczas za pomocą skryptów, które zostały opracowane są następujące Hello:

**Błąd**: `$'\r': command not found`. Czasami następuje `syntax error: unexpected end of file`.

*Przyczyna*: ten błąd występuje, gdy hello wierszy w skrypcie kończyć CRLF. Systemy UNIX oczekiwać tylko LF jako hello koniec wiersza.

Ten problem najczęściej występuje, gdy hello skrypt został utworzony w środowisku Windows CRLF jest linii Kończenie dla wielu edytory tekstów w systemie Windows.

*Rozdzielczość*: Jeśli jest to opcja w edytorze tekstu, wybierz format systemu Unix lub LF dla hello zakończenia wiersza. Można także użyć następujących poleceń na Unix systemu toochange hello CRLF tooan LF hello:

> [!NOTE]
> Witaj poniższe polecenia są w przybliżeniu powinny one zmieniać tooLF zakończenia wiersza CRLF hello. Wybierz jedną oparte na powitania narzędzi dostępnych w systemie.

| Polecenie | Uwagi |
| --- | --- |
| `unix2dos -b INFILE` |kopii zapasowej oryginalnego pliku Hello z. Rozszerzeniem BAK |
| `tr -d '\r' < INFILE > OUTFILE` |PLIKWYJŚCIOWY zawiera wersję z tylko LF zakończenia |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Modyfikuje plik hello bezpośrednio |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |PLIKWYJŚCIOWY zawiera wersję z tylko LF zakończenia. |

**Błąd**: `line 1: #!/usr/bin/env: No such file or directory`.

*Przyczyna*: ten błąd występuje, gdy hello skrypt został zapisany jako UTF-8 z znacznik kolejności bajtów (BOM).

*Rozdzielczość*: hello Zapisz albo jako ASCII lub UTF-8 bez BOM. Można także użyć następującego polecenia w systemie Linux lub Unix systemu toocreate pliku bez hello BOM hello:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Zastąp `INFILE` hello plik zawierający hello BOM. `OUTFILE`powinien być nową nazwę pliku, zawierającego hello skryptu bez hello BOM.

## <a name="seeAlso"></a>Następne kroki

* Dowiedz się, jak za[HDInsight dostosować klastry za pomocą akcji skryptu](hdinsight-hadoop-customize-cluster-linux.md)
* Użyj hello [odwołania do zestawu SDK .NET usługi HDInsight](https://msdn.microsoft.com/library/mt271028.aspx) toolearn więcej informacji na temat tworzenia aplikacji .NET, które zarządzają HDInsight
* Użyj hello [interfejsu API REST usługi HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn jak klastrów akcje zarządzania tooperform toouse REST w usłudze HDInsight.
