---
title: "aaaMonitor oraz zarządzania platformy Hadoop za pomocą narzędzia Ambari API REST - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Ambari toomonitor i zarządzania klastrami Hadoop w usłudze Azure HDInsight. W tym dokumencie dowiesz się, jak klastrów hello toouse interfejsu API REST Ambari dołączone do usługi HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2400530f-92b3-47b7-aa48-875f028765ff
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 1866a77c8e402231bccbcfba7174253aca41339b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a>Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu API REST Ambari hello

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Dowiedz się, jak toouse hello toomanage interfejsu API REST Ambari i monitorowanie klastrów platformy Hadoop w usłudze Azure HDInsight.

Apache Ambari upraszcza hello zarządzania i monitorowania klastrów platformy Hadoop, zapewniając łatwy toouse interfejsu użytkownika i REST interfejsu API sieci web. Ambari znajduje się w klastrach HDInsight, które używają systemu operacyjnego Linux hello. Można używać narzędzia Ambari toomonitor hello klastra i wprowadzania zmian w konfiguracji.

## <a id="whatis"></a>Co to jest Ambari

[Apache Ambari](http://ambari.apache.org) udostępnia interfejs użytkownika, które mogą być używane tooprovision, zarządzanie i monitorowanie klastrów platformy Hadoop sieci web. Deweloperzy mogą integrować te możliwości w swoich aplikacjach przy użyciu hello [interfejsów API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Ambari jest udostępniana domyślnie z klastrami HDInsight opartych na systemie Linux.

## <a name="how-toouse-hello-ambari-rest-api"></a>Jak toouse hello interfejsu API REST Ambari

> [!IMPORTANT]
> Witaj informacje i przykłady w tym dokumencie wymagają klastra usługi HDInsight, który korzysta z systemu operacyjnego Linux. Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z usługą HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).

Przykłady Hello w tym dokumencie znajdują się zarówno hello Bourne powłoki (bash), jak i programu PowerShell. Witaj bash, który przykłady zostały przetestowane z GNU bash 4.3.11, ale powinien współpracować z innymi powłoki systemu Unix. Przykłady programu PowerShell Hello zostały przetestowane z programu PowerShell 5.0, ale powinien współpracować z programem PowerShell 3.0 lub nowszej.

Jeśli przy użyciu hello __powłoki Bourne__ (Bash), musi być zainstalowane następujące hello:

* [cURL](http://curl.haxx.se/): cURL to narzędzie, które mogą być używane toowork z interfejsów API REST z wiersza polecenia hello. W tym dokumencie jest używana toocommunicate z hello interfejsu API REST Ambari.

Czy przy użyciu Bash lub programu PowerShell, musi również mieć [jq](https://stedolan.github.io/jq/) zainstalowane. Jq jest narzędziem do pracy z dokumentów JSON. Jest on używany w **wszystkie** hello przykłady Bash i **jeden** hello przykładów programu PowerShell.

### <a name="base-uri-for-ambari-rest-api"></a>Podstawowy identyfikator URI dla Ambari Rest API

Witaj podstawowy identyfikator URI dla hello Ambari API REST w usłudze HDInsight jest https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, gdzie **CLUSTERNAME** jest hello nazwą klastra.

> [!IMPORTANT]
> Gdy w pełni kwalifikowana nazwa klastra hello w hello części nazwy (FQDN) domeny hello identyfikatora URI (CLUSTERNAME.azurehdinsight.net) nie uwzględnia wielkości liter, inne zdarzenia w hello identyfikatora URI jest rozróżniana wielkość liter. Na przykład, jeśli klaster o nazwie `MyCluster`, następujące hello są prawidłowymi identyfikatorami URI:
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> następujące Hello identyfikatorów URI zwrócony błąd, ponieważ nie jest hello hello drugie wystąpienie nazwy hello Popraw case.
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a>Authentication

Połączenie tooAmbari w usłudze HDInsight wymaga protokołu HTTPS. Nazwa konta administratora hello Użyj (domyślnej hello jest **admin**) i hasło podane podczas tworzenia klastra.

## <a name="examples-authentication-and-parsing-json"></a>Przykłady: Uwierzytelnianie i analizowania JSON

Witaj następujące przykłady pokazują, jak toomake żądanie GET względem hello podstawowy interfejs API REST Ambari:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> Witaj Bash przykłady w tym dokumencie upewnij hello następujące założenia:
>
> * Nazwa logowania Hello klastra hello jest wartość domyślna hello `admin`.
> * `$PASSWORD`zawiera hasło hello hello polecenia logowania usługi HDInsight. Tę wartość można ustawić za pomocą `PASSWORD='mypassword'`.
> * `$CLUSTERNAME`zawiera nazwę hello hello klastra. Tę wartość można ustawić za pomocą`set CLUSTERNAME='clustername'`

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> Przykłady z programu PowerShell Hello w tym dokumencie upewnij hello następujące założenia:
>
> * `$creds`jest obiekt poświadczeń, który zawiera hello admin logowania i hasło dla hello klastra. Tę wartość można ustawić za pomocą `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` i podawania poświadczeń powitania po wyświetleniu monitu.
> * `$clusterName`jest ciąg znaków zawierający nazwę hello hello klastra. Tę wartość można ustawić za pomocą `$clusterName="clustername"`.

Oba przykłady zwracają dokument JSON, który rozpoczyna się od informacji toohello podobnie poniższy przykład:

```json
{
"href" : "http://10.0.0.10:8080/api/v1/clusters/CLUSTERNAME",
"Clusters" : {
    "cluster_id" : 2,
    "cluster_name" : "CLUSTERNAME",
    "health_report" : {
    "Host/stale_config" : 0,
    "Host/maintenance_state" : 0,
    "Host/host_state/HEALTHY" : 7,
    "Host/host_state/UNHEALTHY" : 0,
    "Host/host_state/HEARTBEAT_LOST" : 0,
    "Host/host_state/INIT" : 0,
    "Host/host_status/HEALTHY" : 7,
    "Host/host_status/UNHEALTHY" : 0,
    "Host/host_status/UNKNOWN" : 0,
    "Host/host_status/ALERT" : 0
    ...
```

### <a name="parsing-json-data"></a>Analizowanie danych JSON

Witaj poniższym przykładzie użyto `jq` tooparse hello JSON odpowiedzi dokumentu i wyświetlenie tylko hello `health_report` informacji z hello wyników.

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

PowerShell 3.0 i wyższe zapewnia hello `ConvertFrom-Json` polecenia cmdlet, który konwertuje hello dokument JSON na obiekt, który jest łatwiejsze toowork z z programu PowerShell. Witaj poniższym przykładzie użyto `ConvertFrom-Json` hello tylko toodisplay `health_report` informacji z hello wyników.

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> Podczas gdy większość przykłady w tym dokumencie `ConvertFrom-Json` hello toodisplay elementów z dokumentu odpowiedzi hello, [Ambari aktualizacji konfiguracji](#example-update-ambari-configuration) przykładzie użyto jq. Jq jest używany w tym tooconstruct przykład nowego szablonu z hello JSON odpowiedzi dokumentu.

Pełną dokumentację hello interfejsu API REST, zobacz [Ambari API odwołanie V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a>Przykład: Pobieranie hello FQDN węzłów klastra

Podczas pracy z usługą HDInsight, może być konieczne tooknow hello pełną nazwę domeny (FQDN) węzła klastra. Możesz łatwo pobierać hello nazwy FQDN dla hello różnych węzłach klastra hello przy użyciu hello następujące przykłady:

* **Wszystkie węzły**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" \
    | jq '.items[].Hosts.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.Hosts.host_name
    ```

* **HEAD węzłów**

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HDFS/components/NAMENODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/NAMENODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Węzłów procesu roboczego**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/HDFS/components/DATANODE" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HDFS/components/DATANODE" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

* **Węzły dozorcy**

    ```bash
    curl -u admin:PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" \
    | jq '.host_components[].HostRoles.host_name'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.host_components.HostRoles.host_name
    ```

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a>Przykład: Pobieranie hello wewnętrzny adres IP z węzłów klastra

> [!IMPORTANT]
> adresy IP Hello zwrócony przez hello przykłady w tej sekcji są nie bezpośrednio dostępny przez hello internet. Tylko są one dostępne w ramach sieci wirtualnej platformy Azure, zawierającą klaster usługi HDInsight hello hello.
>
> Aby uzyskać więcej informacji na temat pracy z usługi HDInsight i sieci wirtualnych, zobacz [możliwości rozszerzania HDInsight przy użyciu niestandardowych sieci wirtualnej Azure](hdinsight-extend-hadoop-virtual-network.md).

adres IP hello toofind, musisz znać hello wewnętrzny pełni kwalifikowaną nazwę domeny (FQDN) hello węzły klastra. Po utworzeniu hello nazwy FQDN, możesz uzyskać adres IP hello hello hosta. Hello następujące przykłady najpierw wyszukać Ambari hello FQDN wszystkich węzłów hosta hello, a następnie wyszukać Ambari hello adres IP każdego hosta.

```bash
for HOSTNAME in $(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts" | jq -r '.items[].Hosts.host_name')
do
    IP=$(curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/hosts/$HOSTNAME" | jq -r '.Hosts.ip')
  echo "$HOSTNAME <--> $IP"
done
```

```powershell
$uri = "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/hosts"
$resp = Invoke-WebRequest -Uri $uri -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
foreach($item in $respObj.items) {
    $hostName = [string]$item.Hosts.host_name
    $hostInfoResp = Invoke-WebRequest -Uri "$uri/$hostName" `
        -Credential $creds
    $hostInfoObj = ConvertFrom-Json $hostInfoResp 
    $hostIp = $hostInfoObj.Hosts.ip
    "$hostName <--> $hostIp"
}
```

## <a name="example-get-hello-default-storage"></a>Przykład: Pobieranie hello domyślnego magazynu

Podczas tworzenia klastra usługi HDInsight, musisz użyć konta magazynu Azure lub usługi Data Lake Store jako hello domyślny magazyn dla klastra hello. Można użyć narzędzia Ambari tooretrieve na te informacje po utworzeniu klastra hello. Na przykład, jeśli chcesz tooread/zapisu danych toohello kontenera poza HDInsight.

Witaj następujące przykłady pobrać hello domyślnej konfiguracji magazynu klastra hello:

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
| jq '.items[].configurations[].properties["fs.defaultFS"] | select(. != null)'
```

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.items.configurations.properties.'fs.defaultFS'
```

> [!IMPORTANT]
> Te przykłady zwracać hello pierwszy serwer toohello zastosowano konfigurację (`service_config_version=1`) zawierającą te informacje. Po pobraniu wartość, która została zmodyfikowana po utworzeniu klastra może muszą wersji konfiguracji hello toolist i pobierania hello najnowszy numer.

Wartość zwracana Hello jest podobne tooone z hello następujące przykłady:

* `wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Ta wartość wskazuje, że klastra hello używa konta usługi Azure Storage do magazynu domyślnego. Witaj `ACCOUNTNAME` wartość jest nazwą hello hello konta magazynu. Witaj `CONTAINER` części jest nazwą hello hello kontenera obiektów blob na koncie magazynu hello. kontener Hello jest głównym hello hello systemu plików HDFS zgodne magazynu dla klastra hello.

* `adl://home`-Ta wartość wskazuje, że klastra hello używa usługi Azure Data Lake Store dla domyślnego magazynu.

    Witaj toofind nazwy konta usługi Data Lake Store, użyj hello następujące przykłady:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.hostname"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.hostname'
    ```

    Hello wartości zwracanej przypomina zbyt`ACCOUNTNAME.azuredatalakestore.net`, gdzie `ACCOUNTNAME` jest nazwą hello hello konta usługi Data Lake Store.

    katalog hello toofind w ramach usługi Data Lake Store zawiera hello magazynu dla klastra hello, użyj hello następujące przykłady:

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations/service_config_versions?service_name=HDFS&service_config_version=1" \
    | jq '.items[].configurations[].properties["dfs.adls.home.mountpoint"] | select(. != null)'
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations/service_config_versions?service_name=HDFS&service_config_version=1" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.items.configurations.properties.'dfs.adls.home.mountpoint'
    ```

    Hello wartości zwracanej przypomina zbyt`/clusters/CLUSTERNAME/`. Ta wartość jest ścieżki w ramach hello konta usługi Data Lake Store. Ta ścieżka jest głównym hello hello system plików zgodny system plików HDFS hello klastra. 

> [!NOTE]
> Witaj `Get-AzureRmHDInsightCluster` udostępniane przez polecenia cmdlet [programu Azure PowerShell](/powershell/azure/overview) również zwraca hello informacji magazynu dla klastra hello.


## <a name="example-get-configuration"></a>Przykład: Get konfiguracji

1. Pobierz hello konfiguracje, które są dostępne dla klastra.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    W tym przykładzie zwraca dokument JSON zawierający bieżącą konfigurację hello (identyfikowane przez hello *tag* wartość) dla składników hello zainstalowany w klastrze hello. Witaj poniższy przykład zawiera fragment hello dane zwrócone w wyniku typ klastra Spark.
   
   ```json
   "spark-metrics-properties" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-fairscheduler" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   },
   "spark-thrift-sparkconf" : {
       "tag" : "INITIAL",
       "user" : "admin",
       "version" : 1
   }
   ```

2. Uzyskiwanie konfiguracji hello hello składnika, który chcesz. Poniższy przykład, Zastąp w hello `INITIAL` z hello tag wartość zwracana z hello poprzedniego żądania.

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    W tym przykładzie zwraca dokument JSON zawierający bieżącą konfigurację hello hello `core-site` składnika.

## <a name="example-update-configuration"></a>Przykład: Aktualizacji konfiguracji

1. Pobierz bieżącą konfigurację hello, której Ambari są przechowywane jako hello "żądaną konfiguracją":

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    W tym przykładzie zwraca dokument JSON zawierający bieżącą konfigurację hello (identyfikowane przez hello *tag* wartość) dla składników hello zainstalowany w klastrze hello. Witaj poniższy przykład zawiera fragment hello dane zwrócone w wyniku typ klastra Spark.
   
    ```json
    "spark-metrics-properties" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-fairscheduler" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    },
    "spark-thrift-sparkconf" : {
        "tag" : "INITIAL",
        "user" : "admin",
        "version" : 1
    }
    ```
   
    Z tej listy muszą toocopy hello nazwy składnika hello (na przykład **spark\_thrift\_sparkconf** i hello **tag** wartość.

2. Pobieranie hello konfigurację dla składnika hello i tag przy użyciu hello następującego polecenia:
   
    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=spark-thrift-sparkconf&tag=INITIAL" \
    | jq --arg newtag $(echo version$(date +%s%N)) '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    ```powershell
    $epoch = Get-Date -Year 1970 -Month 1 -Day 1 -Hour 0 -Minute 0 -Second 0
    $now = Get-Date
    $unixTimeStamp = [math]::truncate($now.ToUniversalTime().Subtract($epoch).TotalMilliSeconds)
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=spark-thrift-sparkconf&tag=INITIAL" `
        -Credential $creds
    $resp.Content | jq --arg newtag "version$unixTimeStamp" '.items[] | del(.href, .version, .Config) | .tag |= $newtag | {"Clusters": {"desired_config": .}}' > newconfig.json
    ```

    > [!NOTE]
    > Zastąp **spark-thrift-sparkconf** i **początkowej** składnika hello i tag, który ma tooretrieve hello konfiguracji.
   
    Jq jest używane tooturn hello dane pobierane z usługi HDInsight do nowego szablonu konfiguracji. W szczególności te przykłady wykonaj hello następujące akcje:
   
    * Tworzy unikatową wartość zawierające ciąg hello "version" i hello daty, który jest przechowywany w `newtag`.

    * Tworzy głównego dokumentu do hello nowe wymaganą konfiguracją.

    * Pobiera hello zawartość hello `.items[]` tablicy i dodanie go w obszarze hello **desired_config** elementu.

    * Usuwa hello `href`, `version`, i `Config` elementy, jak te elementy nie są wymagane toosubmit nowej konfiguracji.

    * Dodaje `tag` element o wartości `version#################`. część numeryczna Hello jest oparta na powitania bieżącą datę. Każdej konfiguracji musi mieć unikatowy tag.
     
    Na koniec są zapisywane dane hello toohello `newconfig.json` dokumentu. Struktura dokumentu Hello powinna zostać wyświetlona toohello podobnie poniższy przykład:
     
     ```json
    {
        "Clusters": {
            "desired_config": {
            "tag": "version1459260185774265400",
            "type": "spark-thrift-sparkconf",
            "properties": {
                ....
            },
            "properties_attributes": {
                ....
            }
        }
    }
    ```

3. Otwórz hello `newconfig.json` dokument i zmodyfikować dodać wartości w hello `properties` obiektu. Witaj następujące zmiany przykład Witaj wartość `"spark.yarn.am.memory"` z `"1g"` zbyt`"3g"`. Dodano również `"spark.kryoserializer.buffer.max"` o wartości `"256m"`.
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    Zapisz plik hello, po zakończeniu wprowadzania zmian.

4. Użyj następującego polecenia toosubmit hello aktualizacji konfiguracji tooAmbari hello.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" -X PUT -d @newconfig.json "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
    ```

    ```powershell
    $newConfig = Get-Content .\newconfig.json
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body $newConfig
    $resp.Content
    ```
   
    Te polecenia przesłać zawartość hello hello **newconfig.json** plików w klastrze toohello hello nowych Konfiguracja żądanego. Żądanie hello zwraca dokumentu JSON. Witaj **versionTag** element w tym dokumencie powinna być zgodna wersja hello przesłane i hello **configs** obiekt zawiera zmiany konfiguracji hello żądanego.

### <a name="example-restart-a-service-component"></a>Przykład: Ponowne uruchomienie składnika usługi

W tym momencie można spojrzeć na powitania interfejsu użytkownika sieci web Ambari, hello usługę platformy Spark wskazuje, że wymaga ona toobe po ponownym uruchomieniu hello nowej konfiguracji zostały wprowadzone. Użyj hello następujące kroki toorestart hello usługi.

1. Użyj powitania po tooenable trybu konserwacji dla hello usługę platformy Spark:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning on maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"ON"}}}'
    $resp.Content
    ```
   
    Te polecenia Wyślij serwer toohello dokumentów JSON, który powoduje włączenie trybu konserwacji. Aby sprawdzić, usługa hello jest teraz w trybie konserwacji przy użyciu hello następujące żądania:
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK" \
    | jq .ServiceInfo.maintenance_state
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK2" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.ServiceInfo.maintenance_state
    ```
   
    Witaj zwracana wartość jest `ON`.

2. Następnie użyj powitania po tooturn poza hello usługi:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"INSTALLED"}}}'
    $resp.Content
    ```
    
    odpowiedź Hello jest toohello podobnie poniższy przykład:
   
    ```json
    {
        "href" : "http://10.0.0.18:8080/api/v1/clusters/CLUSTERNAME/requests/29",
        "Requests" : {
            "id" : 29,
            "status" : "Accepted"
        }
    }
    ```
    
    > [!IMPORTANT]
    > Witaj `href` wartość zwrócona przez ten identyfikator URI jest używany wewnętrzny adres IP hello hello węzła klastra. toouse części hello "10.0.0.18:8080" z poziomu zewnętrznej hello klastra, Zamień hello nazwę FQDN klastra hello. 
    
    następujące polecenia Hello pobrać stanu hello hello żądania:

    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/requests/29" \
    | jq .Requests.request_status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/requests/29" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.Requests.request_status
    ```

    Odpowiedź `COMPLETED` wskazuje hello żądanie zostało ukończone.

3. Po ukończeniu poprzedniego żądania hello, użyj powitania po toostart hello usługi.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```
   
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo":{"context":"_PARSE_.STOP.SPARK","operation_level":{"level":"SERVICE","cluster_name":"CLUSTERNAME","service_name":"SPARK"}},"Body":{"ServiceInfo":{"state":"STARTED"}}}'
    ```
    Usługa Hello jest teraz, używając hello nowej konfiguracji.

4. Na koniec użyj powitania po tooturn Wyłącz tryb konserwacji.
   
    ```bash
    curl -u admin:$PASSWORD -sS -H "X-Requested-By: ambari" \
    -X PUT -d '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}' \
    "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/SPARK"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/SPARK" `
        -Credential $creds `
        -Method PUT `
        -Headers @{"X-Requested-By" = "ambari"} `
        -Body '{"RequestInfo": {"context": "turning off maintenance mode for SPARK"},"Body": {"ServiceInfo": {"maintenance_state":"OFF"}}}'
    ```

## <a name="next-steps"></a>Następne kroki

Pełną dokumentację hello interfejsu API REST, zobacz [Ambari API odwołanie V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

