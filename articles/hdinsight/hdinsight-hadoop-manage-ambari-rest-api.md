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
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-rest-api"></a><span data-ttu-id="f59cc-104">Zarządzanie klastrami usługi HDInsight przy użyciu interfejsu API REST Ambari hello</span><span class="sxs-lookup"><span data-stu-id="f59cc-104">Manage HDInsight clusters by using hello Ambari REST API</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="f59cc-105">Dowiedz się, jak toouse hello toomanage interfejsu API REST Ambari i monitorowanie klastrów platformy Hadoop w usłudze Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f59cc-105">Learn how toouse hello Ambari REST API toomanage and monitor Hadoop clusters in Azure HDInsight.</span></span>

<span data-ttu-id="f59cc-106">Apache Ambari upraszcza hello zarządzania i monitorowania klastrów platformy Hadoop, zapewniając łatwy toouse interfejsu użytkownika i REST interfejsu API sieci web.</span><span class="sxs-lookup"><span data-stu-id="f59cc-106">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="f59cc-107">Ambari znajduje się w klastrach HDInsight, które używają systemu operacyjnego Linux hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-107">Ambari is included on HDInsight clusters that use hello Linux operating system.</span></span> <span data-ttu-id="f59cc-108">Można używać narzędzia Ambari toomonitor hello klastra i wprowadzania zmian w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f59cc-108">You can use Ambari toomonitor hello cluster and make configuration changes.</span></span>

## <span data-ttu-id="f59cc-109"><a id="whatis"></a>Co to jest Ambari</span><span class="sxs-lookup"><span data-stu-id="f59cc-109"><a id="whatis"></a>What is Ambari</span></span>

<span data-ttu-id="f59cc-110">[Apache Ambari](http://ambari.apache.org) udostępnia interfejs użytkownika, które mogą być używane tooprovision, zarządzanie i monitorowanie klastrów platformy Hadoop sieci web.</span><span class="sxs-lookup"><span data-stu-id="f59cc-110">[Apache Ambari](http://ambari.apache.org) provides web UI that can be used tooprovision, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="f59cc-111">Deweloperzy mogą integrować te możliwości w swoich aplikacjach przy użyciu hello [interfejsów API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="f59cc-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="f59cc-112">Ambari jest udostępniana domyślnie z klastrami HDInsight opartych na systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="f59cc-112">Ambari is provided by default with Linux-based HDInsight clusters.</span></span>

## <a name="how-toouse-hello-ambari-rest-api"></a><span data-ttu-id="f59cc-113">Jak toouse hello interfejsu API REST Ambari</span><span class="sxs-lookup"><span data-stu-id="f59cc-113">How toouse hello Ambari REST API</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f59cc-114">Witaj informacje i przykłady w tym dokumencie wymagają klastra usługi HDInsight, który korzysta z systemu operacyjnego Linux.</span><span class="sxs-lookup"><span data-stu-id="f59cc-114">hello information and examples in this document require an HDInsight cluster that uses Linux operating system.</span></span> <span data-ttu-id="f59cc-115">Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z usługą HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f59cc-115">For more information, see [Get started with HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

<span data-ttu-id="f59cc-116">Przykłady Hello w tym dokumencie znajdują się zarówno hello Bourne powłoki (bash), jak i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f59cc-116">hello examples in this document are provided for both hello Bourne shell (bash) and PowerShell.</span></span> <span data-ttu-id="f59cc-117">Witaj bash, który przykłady zostały przetestowane z GNU bash 4.3.11, ale powinien współpracować z innymi powłoki systemu Unix.</span><span class="sxs-lookup"><span data-stu-id="f59cc-117">hello bash examples were tested with GNU bash 4.3.11, but should work with other Unix shells.</span></span> <span data-ttu-id="f59cc-118">Przykłady programu PowerShell Hello zostały przetestowane z programu PowerShell 5.0, ale powinien współpracować z programem PowerShell 3.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f59cc-118">hello PowerShell examples were tested with PowerShell 5.0, but should work with PowerShell 3.0 or higher.</span></span>

<span data-ttu-id="f59cc-119">Jeśli przy użyciu hello __powłoki Bourne__ (Bash), musi być zainstalowane następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f59cc-119">If using hello __Bourne shell__ (Bash), you must have hello following installed:</span></span>

* <span data-ttu-id="f59cc-120">[cURL](http://curl.haxx.se/): cURL to narzędzie, które mogą być używane toowork z interfejsów API REST z wiersza polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-120">[cURL](http://curl.haxx.se/): cURL is a utility that can be used toowork with REST APIs from hello command line.</span></span> <span data-ttu-id="f59cc-121">W tym dokumencie jest używana toocommunicate z hello interfejsu API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="f59cc-121">In this document, it is used toocommunicate with hello Ambari REST API.</span></span>

<span data-ttu-id="f59cc-122">Czy przy użyciu Bash lub programu PowerShell, musi również mieć [jq](https://stedolan.github.io/jq/) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="f59cc-122">Whether using Bash or PowerShell, you must also have [jq](https://stedolan.github.io/jq/) installed.</span></span> <span data-ttu-id="f59cc-123">Jq jest narzędziem do pracy z dokumentów JSON.</span><span class="sxs-lookup"><span data-stu-id="f59cc-123">Jq is a utility for working with JSON documents.</span></span> <span data-ttu-id="f59cc-124">Jest on używany w **wszystkie** hello przykłady Bash i **jeden** hello przykładów programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f59cc-124">It is used in **all** hello Bash examples, and **one** of hello PowerShell examples.</span></span>

### <a name="base-uri-for-ambari-rest-api"></a><span data-ttu-id="f59cc-125">Podstawowy identyfikator URI dla Ambari Rest API</span><span class="sxs-lookup"><span data-stu-id="f59cc-125">Base URI for Ambari Rest API</span></span>

<span data-ttu-id="f59cc-126">Witaj podstawowy identyfikator URI dla hello Ambari API REST w usłudze HDInsight jest https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, gdzie **CLUSTERNAME** jest hello nazwą klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-126">hello base URI for hello Ambari REST API on HDInsight is https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f59cc-127">Gdy w pełni kwalifikowana nazwa klastra hello w hello części nazwy (FQDN) domeny hello identyfikatora URI (CLUSTERNAME.azurehdinsight.net) nie uwzględnia wielkości liter, inne zdarzenia w hello identyfikatora URI jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="f59cc-127">While hello cluster name in hello fully qualified domain name (FQDN) part of hello URI (CLUSTERNAME.azurehdinsight.net) is case-insensitive, other occurrences in hello URI are case-sensitive.</span></span> <span data-ttu-id="f59cc-128">Na przykład, jeśli klaster o nazwie `MyCluster`, następujące hello są prawidłowymi identyfikatorami URI:</span><span class="sxs-lookup"><span data-stu-id="f59cc-128">For example, if your cluster is named `MyCluster`, hello following are valid URIs:</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/MyCluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/MyCluster`
> 
> <span data-ttu-id="f59cc-129">następujące Hello identyfikatorów URI zwrócony błąd, ponieważ nie jest hello hello drugie wystąpienie nazwy hello Popraw case.</span><span class="sxs-lookup"><span data-stu-id="f59cc-129">hello following URIs return an error because hello second occurrence of hello name is not hello correct case.</span></span>
> 
> `https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster`
>
> `https://MyCluster.azurehdinsight.net/api/v1/clusters/mycluster`

### <a name="authentication"></a><span data-ttu-id="f59cc-130">Authentication</span><span class="sxs-lookup"><span data-stu-id="f59cc-130">Authentication</span></span>

<span data-ttu-id="f59cc-131">Połączenie tooAmbari w usłudze HDInsight wymaga protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f59cc-131">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="f59cc-132">Nazwa konta administratora hello Użyj (domyślnej hello jest **admin**) i hasło podane podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-132">Use hello admin account name (hello default is **admin**) and password you provided during cluster creation.</span></span>

## <a name="examples-authentication-and-parsing-json"></a><span data-ttu-id="f59cc-133">Przykłady: Uwierzytelnianie i analizowania JSON</span><span class="sxs-lookup"><span data-stu-id="f59cc-133">Examples: Authentication and parsing JSON</span></span>

<span data-ttu-id="f59cc-134">Witaj następujące przykłady pokazują, jak toomake żądanie GET względem hello podstawowy interfejs API REST Ambari:</span><span class="sxs-lookup"><span data-stu-id="f59cc-134">hello following examples demonstrate how toomake a GET request against hello base Ambari REST API:</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME"
```

> [!IMPORTANT]
> <span data-ttu-id="f59cc-135">Witaj Bash przykłady w tym dokumencie upewnij hello następujące założenia:</span><span class="sxs-lookup"><span data-stu-id="f59cc-135">hello Bash examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="f59cc-136">Nazwa logowania Hello klastra hello jest wartość domyślna hello `admin`.</span><span class="sxs-lookup"><span data-stu-id="f59cc-136">hello login name for hello cluster is hello default value of `admin`.</span></span>
> * <span data-ttu-id="f59cc-137">`$PASSWORD`zawiera hasło hello hello polecenia logowania usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f59cc-137">`$PASSWORD` contains hello password for hello HDInsight login command.</span></span> <span data-ttu-id="f59cc-138">Tę wartość można ustawić za pomocą `PASSWORD='mypassword'`.</span><span class="sxs-lookup"><span data-stu-id="f59cc-138">You can set this value by using `PASSWORD='mypassword'`.</span></span>
> * <span data-ttu-id="f59cc-139">`$CLUSTERNAME`zawiera nazwę hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-139">`$CLUSTERNAME` contains hello name of hello cluster.</span></span> <span data-ttu-id="f59cc-140">Tę wartość można ustawić za pomocą`set CLUSTERNAME='clustername'`</span><span class="sxs-lookup"><span data-stu-id="f59cc-140">You can set this value by using `set CLUSTERNAME='clustername'`</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$resp.Content
```

> [!IMPORTANT]
> <span data-ttu-id="f59cc-141">Przykłady z programu PowerShell Hello w tym dokumencie upewnij hello następujące założenia:</span><span class="sxs-lookup"><span data-stu-id="f59cc-141">hello PowerShell examples in this document make hello following assumptions:</span></span>
>
> * <span data-ttu-id="f59cc-142">`$creds`jest obiekt poświadczeń, który zawiera hello admin logowania i hasło dla hello klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-142">`$creds` is a credential object that contains hello admin login and password for hello cluster.</span></span> <span data-ttu-id="f59cc-143">Tę wartość można ustawić za pomocą `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` i podawania poświadczeń powitania po wyświetleniu monitu.</span><span class="sxs-lookup"><span data-stu-id="f59cc-143">You can set this value by using `$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"` and providing hello credentials when prompted.</span></span>
> * <span data-ttu-id="f59cc-144">`$clusterName`jest ciąg znaków zawierający nazwę hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-144">`$clusterName` is a string that contains hello name of hello cluster.</span></span> <span data-ttu-id="f59cc-145">Tę wartość można ustawić za pomocą `$clusterName="clustername"`.</span><span class="sxs-lookup"><span data-stu-id="f59cc-145">You can set this value by using `$clusterName="clustername"`.</span></span>

<span data-ttu-id="f59cc-146">Oba przykłady zwracają dokument JSON, który rozpoczyna się od informacji toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f59cc-146">Both examples return a JSON document that begins with information similar toohello following example:</span></span>

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

### <a name="parsing-json-data"></a><span data-ttu-id="f59cc-147">Analizowanie danych JSON</span><span class="sxs-lookup"><span data-stu-id="f59cc-147">Parsing JSON data</span></span>

<span data-ttu-id="f59cc-148">Witaj poniższym przykładzie użyto `jq` tooparse hello JSON odpowiedzi dokumentu i wyświetlenie tylko hello `health_report` informacji z hello wyników.</span><span class="sxs-lookup"><span data-stu-id="f59cc-148">hello following example uses `jq` tooparse hello JSON response document and display only hello `health_report` information from hello results.</span></span>

```bash
curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME" \
| jq '.Clusters.health_report'
```

<span data-ttu-id="f59cc-149">PowerShell 3.0 i wyższe zapewnia hello `ConvertFrom-Json` polecenia cmdlet, który konwertuje hello dokument JSON na obiekt, który jest łatwiejsze toowork z z programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f59cc-149">PowerShell 3.0 and higher provides hello `ConvertFrom-Json` cmdlet, which converts hello JSON document into an object that is easier toowork with from PowerShell.</span></span> <span data-ttu-id="f59cc-150">Witaj poniższym przykładzie użyto `ConvertFrom-Json` hello tylko toodisplay `health_report` informacji z hello wyników.</span><span class="sxs-lookup"><span data-stu-id="f59cc-150">hello following example uses `ConvertFrom-Json` toodisplay only hello `health_report` information from hello results.</span></span>

```powershell
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$respObj.Clusters.health_report
```

> [!NOTE]
> <span data-ttu-id="f59cc-151">Podczas gdy większość przykłady w tym dokumencie `ConvertFrom-Json` hello toodisplay elementów z dokumentu odpowiedzi hello, [Ambari aktualizacji konfiguracji](#example-update-ambari-configuration) przykładzie użyto jq.</span><span class="sxs-lookup"><span data-stu-id="f59cc-151">While most examples in this document use `ConvertFrom-Json` toodisplay elements from hello response document, hello [Update Ambari configuration](#example-update-ambari-configuration) example uses jq.</span></span> <span data-ttu-id="f59cc-152">Jq jest używany w tym tooconstruct przykład nowego szablonu z hello JSON odpowiedzi dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f59cc-152">Jq is used in this example tooconstruct a new template from hello JSON response document.</span></span>

<span data-ttu-id="f59cc-153">Pełną dokumentację hello interfejsu API REST, zobacz [Ambari API odwołanie V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="f59cc-153">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

## <a name="example-get-hello-fqdn-of-cluster-nodes"></a><span data-ttu-id="f59cc-154">Przykład: Pobieranie hello FQDN węzłów klastra</span><span class="sxs-lookup"><span data-stu-id="f59cc-154">Example: Get hello FQDN of cluster nodes</span></span>

<span data-ttu-id="f59cc-155">Podczas pracy z usługą HDInsight, może być konieczne tooknow hello pełną nazwę domeny (FQDN) węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-155">When working with HDInsight, you may need tooknow hello fully qualified domain name (FQDN) of a cluster node.</span></span> <span data-ttu-id="f59cc-156">Możesz łatwo pobierać hello nazwy FQDN dla hello różnych węzłach klastra hello przy użyciu hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="f59cc-156">You can easily retrieve hello FQDN for hello various nodes in hello cluster using hello following examples:</span></span>

* <span data-ttu-id="f59cc-157">**Wszystkie węzły**</span><span class="sxs-lookup"><span data-stu-id="f59cc-157">**All nodes**</span></span>

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

* <span data-ttu-id="f59cc-158">**HEAD węzłów**</span><span class="sxs-lookup"><span data-stu-id="f59cc-158">**Head nodes**</span></span>

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

* <span data-ttu-id="f59cc-159">**Węzłów procesu roboczego**</span><span class="sxs-lookup"><span data-stu-id="f59cc-159">**Worker nodes**</span></span>

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

* <span data-ttu-id="f59cc-160">**Węzły dozorcy**</span><span class="sxs-lookup"><span data-stu-id="f59cc-160">**Zookeeper nodes**</span></span>

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

## <a name="example-get-hello-internal-ip-address-of-cluster-nodes"></a><span data-ttu-id="f59cc-161">Przykład: Pobieranie hello wewnętrzny adres IP z węzłów klastra</span><span class="sxs-lookup"><span data-stu-id="f59cc-161">Example: Get hello internal IP address of cluster nodes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f59cc-162">adresy IP Hello zwrócony przez hello przykłady w tej sekcji są nie bezpośrednio dostępny przez hello internet.</span><span class="sxs-lookup"><span data-stu-id="f59cc-162">hello IP addresses returned by hello examples in this section are not directly accessible over hello internet.</span></span> <span data-ttu-id="f59cc-163">Tylko są one dostępne w ramach sieci wirtualnej platformy Azure, zawierającą klaster usługi HDInsight hello hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-163">They are only accessible within hello Azure Virtual Network that contains hello HDInsight cluster.</span></span>
>
> <span data-ttu-id="f59cc-164">Aby uzyskać więcej informacji na temat pracy z usługi HDInsight i sieci wirtualnych, zobacz [możliwości rozszerzania HDInsight przy użyciu niestandardowych sieci wirtualnej Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="f59cc-164">For more information on working with HDInsight and virtual networks, see [Extend HDInsight capabilities by using a custom Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md).</span></span>

<span data-ttu-id="f59cc-165">adres IP hello toofind, musisz znać hello wewnętrzny pełni kwalifikowaną nazwę domeny (FQDN) hello węzły klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-165">toofind hello IP address, you must know hello internal fully qualified domain name (FQDN) of hello cluster nodes.</span></span> <span data-ttu-id="f59cc-166">Po utworzeniu hello nazwy FQDN, możesz uzyskać adres IP hello hello hosta.</span><span class="sxs-lookup"><span data-stu-id="f59cc-166">Once you have hello FQDN, you can then get hello IP address of hello host.</span></span> <span data-ttu-id="f59cc-167">Hello następujące przykłady najpierw wyszukać Ambari hello FQDN wszystkich węzłów hosta hello, a następnie wyszukać Ambari hello adres IP każdego hosta.</span><span class="sxs-lookup"><span data-stu-id="f59cc-167">hello following examples first query Ambari for hello FQDN of all hello host nodes, then query Ambari for hello IP address of each host.</span></span>

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

## <a name="example-get-hello-default-storage"></a><span data-ttu-id="f59cc-168">Przykład: Pobieranie hello domyślnego magazynu</span><span class="sxs-lookup"><span data-stu-id="f59cc-168">Example: Get hello default storage</span></span>

<span data-ttu-id="f59cc-169">Podczas tworzenia klastra usługi HDInsight, musisz użyć konta magazynu Azure lub usługi Data Lake Store jako hello domyślny magazyn dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-169">When you create an HDInsight cluster, you must use an Azure Storage Account or Data Lake Store as hello default storage for hello cluster.</span></span> <span data-ttu-id="f59cc-170">Można użyć narzędzia Ambari tooretrieve na te informacje po utworzeniu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-170">You can use Ambari tooretrieve this information after hello cluster has been created.</span></span> <span data-ttu-id="f59cc-171">Na przykład, jeśli chcesz tooread/zapisu danych toohello kontenera poza HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f59cc-171">For example, if you want tooread/write data toohello container outside HDInsight.</span></span>

<span data-ttu-id="f59cc-172">Witaj następujące przykłady pobrać hello domyślnej konfiguracji magazynu klastra hello:</span><span class="sxs-lookup"><span data-stu-id="f59cc-172">hello following examples retrieve hello default storage configuration from hello cluster:</span></span>

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
> <span data-ttu-id="f59cc-173">Te przykłady zwracać hello pierwszy serwer toohello zastosowano konfigurację (`service_config_version=1`) zawierającą te informacje.</span><span class="sxs-lookup"><span data-stu-id="f59cc-173">These examples return hello first configuration applied toohello server (`service_config_version=1`) which contains this information.</span></span> <span data-ttu-id="f59cc-174">Po pobraniu wartość, która została zmodyfikowana po utworzeniu klastra może muszą wersji konfiguracji hello toolist i pobierania hello najnowszy numer.</span><span class="sxs-lookup"><span data-stu-id="f59cc-174">If you retrieve a value that has been modified after cluster creation, you may need toolist hello configuration versions and retrieve hello latest one.</span></span>

<span data-ttu-id="f59cc-175">Wartość zwracana Hello jest podobne tooone z hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="f59cc-175">hello return value is similar tooone of hello following examples:</span></span>

* <span data-ttu-id="f59cc-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net`-Ta wartość wskazuje, że klastra hello używa konta usługi Azure Storage do magazynu domyślnego.</span><span class="sxs-lookup"><span data-stu-id="f59cc-176">`wasb://CONTAINER@ACCOUNTNAME.blob.core.windows.net` - This value indicates that hello cluster is using an Azure Storage account for default storage.</span></span> <span data-ttu-id="f59cc-177">Witaj `ACCOUNTNAME` wartość jest nazwą hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="f59cc-177">hello `ACCOUNTNAME` value is hello name of hello storage account.</span></span> <span data-ttu-id="f59cc-178">Witaj `CONTAINER` części jest nazwą hello hello kontenera obiektów blob na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-178">hello `CONTAINER` portion is hello name of hello blob container in hello storage account.</span></span> <span data-ttu-id="f59cc-179">kontener Hello jest głównym hello hello systemu plików HDFS zgodne magazynu dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-179">hello container is hello root of hello HDFS compatible storage for hello cluster.</span></span>

* <span data-ttu-id="f59cc-180">`adl://home`-Ta wartość wskazuje, że klastra hello używa usługi Azure Data Lake Store dla domyślnego magazynu.</span><span class="sxs-lookup"><span data-stu-id="f59cc-180">`adl://home` - This value indicates that hello cluster is using an Azure Data Lake Store for default storage.</span></span>

    <span data-ttu-id="f59cc-181">Witaj toofind nazwy konta usługi Data Lake Store, użyj hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="f59cc-181">toofind hello Data Lake Store account name, use hello following examples:</span></span>

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

    <span data-ttu-id="f59cc-182">Hello wartości zwracanej przypomina zbyt`ACCOUNTNAME.azuredatalakestore.net`, gdzie `ACCOUNTNAME` jest nazwą hello hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f59cc-182">hello return value is similar too`ACCOUNTNAME.azuredatalakestore.net`, where `ACCOUNTNAME` is hello name of hello Data Lake Store account.</span></span>

    <span data-ttu-id="f59cc-183">katalog hello toofind w ramach usługi Data Lake Store zawiera hello magazynu dla klastra hello, użyj hello następujące przykłady:</span><span class="sxs-lookup"><span data-stu-id="f59cc-183">toofind hello directory within Data Lake Store that contains hello storage for hello cluster, use hello following examples:</span></span>

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

    <span data-ttu-id="f59cc-184">Hello wartości zwracanej przypomina zbyt`/clusters/CLUSTERNAME/`.</span><span class="sxs-lookup"><span data-stu-id="f59cc-184">hello return value is similar too`/clusters/CLUSTERNAME/`.</span></span> <span data-ttu-id="f59cc-185">Ta wartość jest ścieżki w ramach hello konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f59cc-185">This value is a path within hello Data Lake Store account.</span></span> <span data-ttu-id="f59cc-186">Ta ścieżka jest głównym hello hello system plików zgodny system plików HDFS hello klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-186">This path is hello root of hello HDFS compatible file system for hello cluster.</span></span> 

> [!NOTE]
> <span data-ttu-id="f59cc-187">Witaj `Get-AzureRmHDInsightCluster` udostępniane przez polecenia cmdlet [programu Azure PowerShell](/powershell/azure/overview) również zwraca hello informacji magazynu dla klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-187">hello `Get-AzureRmHDInsightCluster` cmdlet provided by [Azure PowerShell](/powershell/azure/overview) also returns hello storage information for hello cluster.</span></span>


## <a name="example-get-configuration"></a><span data-ttu-id="f59cc-188">Przykład: Get konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f59cc-188">Example: Get configuration</span></span>

1. <span data-ttu-id="f59cc-189">Pobierz hello konfiguracje, które są dostępne dla klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-189">Get hello configurations that are available for your cluster.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    $respObj = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    $respObj.Content
    ```

    <span data-ttu-id="f59cc-190">W tym przykładzie zwraca dokument JSON zawierający bieżącą konfigurację hello (identyfikowane przez hello *tag* wartość) dla składników hello zainstalowany w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-190">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="f59cc-191">Witaj poniższy przykład zawiera fragment hello dane zwrócone w wyniku typ klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="f59cc-191">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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

2. <span data-ttu-id="f59cc-192">Uzyskiwanie konfiguracji hello hello składnika, który chcesz.</span><span class="sxs-lookup"><span data-stu-id="f59cc-192">Get hello configuration for hello component that you are interested in.</span></span> <span data-ttu-id="f59cc-193">Poniższy przykład, Zastąp w hello `INITIAL` z hello tag wartość zwracana z hello poprzedniego żądania.</span><span class="sxs-lookup"><span data-stu-id="f59cc-193">In hello following example, replace `INITIAL` with hello tag value returned from hello previous request.</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/configurations?type=core-site&tag=INITIAL"
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/configurations?type=core-site&tag=INITIAL" `
        -Credential $creds
    $resp.Content
    ```

    <span data-ttu-id="f59cc-194">W tym przykładzie zwraca dokument JSON zawierający bieżącą konfigurację hello hello `core-site` składnika.</span><span class="sxs-lookup"><span data-stu-id="f59cc-194">This example returns a JSON document containing hello current configuration for hello `core-site` component.</span></span>

## <a name="example-update-configuration"></a><span data-ttu-id="f59cc-195">Przykład: Aktualizacji konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f59cc-195">Example: Update configuration</span></span>

1. <span data-ttu-id="f59cc-196">Pobierz bieżącą konfigurację hello, której Ambari są przechowywane jako hello "żądaną konfiguracją":</span><span class="sxs-lookup"><span data-stu-id="f59cc-196">Get hello current configuration, which Ambari stores as hello "desired configuration":</span></span>

    ```bash
    curl -u admin:$PASSWORD -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME?fields=Clusters/desired_configs"
    ```

    ```powershell
    Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName`?fields=Clusters/desired_configs" `
        -Credential $creds
    ```

    <span data-ttu-id="f59cc-197">W tym przykładzie zwraca dokument JSON zawierający bieżącą konfigurację hello (identyfikowane przez hello *tag* wartość) dla składników hello zainstalowany w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-197">This example returns a JSON document containing hello current configuration (identified by hello *tag* value) for hello components installed on hello cluster.</span></span> <span data-ttu-id="f59cc-198">Witaj poniższy przykład zawiera fragment hello dane zwrócone w wyniku typ klastra Spark.</span><span class="sxs-lookup"><span data-stu-id="f59cc-198">hello following example is an excerpt from hello data returned from a Spark cluster type.</span></span>
   
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
   
    <span data-ttu-id="f59cc-199">Z tej listy muszą toocopy hello nazwy składnika hello (na przykład **spark\_thrift\_sparkconf** i hello **tag** wartość.</span><span class="sxs-lookup"><span data-stu-id="f59cc-199">From this list, you need toocopy hello name of hello component (for example, **spark\_thrift\_sparkconf** and hello **tag** value.</span></span>

2. <span data-ttu-id="f59cc-200">Pobieranie hello konfigurację dla składnika hello i tag przy użyciu hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f59cc-200">Retrieve hello configuration for hello component and tag by using hello following commands:</span></span>
   
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
    > <span data-ttu-id="f59cc-201">Zastąp **spark-thrift-sparkconf** i **początkowej** składnika hello i tag, który ma tooretrieve hello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f59cc-201">Replace **spark-thrift-sparkconf** and **INITIAL** with hello component and tag that you want tooretrieve hello configuration for.</span></span>
   
    <span data-ttu-id="f59cc-202">Jq jest używane tooturn hello dane pobierane z usługi HDInsight do nowego szablonu konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f59cc-202">Jq is used tooturn hello data retrieved from HDInsight into a new configuration template.</span></span> <span data-ttu-id="f59cc-203">W szczególności te przykłady wykonaj hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="f59cc-203">Specifically, these examples perform hello following actions:</span></span>
   
    * <span data-ttu-id="f59cc-204">Tworzy unikatową wartość zawierające ciąg hello "version" i hello daty, który jest przechowywany w `newtag`.</span><span class="sxs-lookup"><span data-stu-id="f59cc-204">Creates a unique value containing hello string "version" and hello date, which is stored in `newtag`.</span></span>

    * <span data-ttu-id="f59cc-205">Tworzy głównego dokumentu do hello nowe wymaganą konfiguracją.</span><span class="sxs-lookup"><span data-stu-id="f59cc-205">Creates a root document for hello new desired configuration.</span></span>

    * <span data-ttu-id="f59cc-206">Pobiera hello zawartość hello `.items[]` tablicy i dodanie go w obszarze hello **desired_config** elementu.</span><span class="sxs-lookup"><span data-stu-id="f59cc-206">Gets hello contents of hello `.items[]` array and adds it under hello **desired_config** element.</span></span>

    * <span data-ttu-id="f59cc-207">Usuwa hello `href`, `version`, i `Config` elementy, jak te elementy nie są wymagane toosubmit nowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f59cc-207">Deletes hello `href`, `version`, and `Config` elements, as these elements aren't needed toosubmit a new configuration.</span></span>

    * <span data-ttu-id="f59cc-208">Dodaje `tag` element o wartości `version#################`.</span><span class="sxs-lookup"><span data-stu-id="f59cc-208">Adds a `tag` element with a value of `version#################`.</span></span> <span data-ttu-id="f59cc-209">część numeryczna Hello jest oparta na powitania bieżącą datę.</span><span class="sxs-lookup"><span data-stu-id="f59cc-209">hello numeric portion is based on hello current date.</span></span> <span data-ttu-id="f59cc-210">Każdej konfiguracji musi mieć unikatowy tag.</span><span class="sxs-lookup"><span data-stu-id="f59cc-210">Each configuration must have a unique tag.</span></span>
     
    <span data-ttu-id="f59cc-211">Na koniec są zapisywane dane hello toohello `newconfig.json` dokumentu.</span><span class="sxs-lookup"><span data-stu-id="f59cc-211">Finally, hello data is saved toohello `newconfig.json` document.</span></span> <span data-ttu-id="f59cc-212">Struktura dokumentu Hello powinna zostać wyświetlona toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f59cc-212">hello document structure should appear similar toohello following example:</span></span>
     
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

3. <span data-ttu-id="f59cc-213">Otwórz hello `newconfig.json` dokument i zmodyfikować dodać wartości w hello `properties` obiektu.</span><span class="sxs-lookup"><span data-stu-id="f59cc-213">Open hello `newconfig.json` document and modify/add values in hello `properties` object.</span></span> <span data-ttu-id="f59cc-214">Witaj następujące zmiany przykład Witaj wartość `"spark.yarn.am.memory"` z `"1g"` zbyt`"3g"`.</span><span class="sxs-lookup"><span data-stu-id="f59cc-214">hello following example changes hello value of `"spark.yarn.am.memory"` from `"1g"` too`"3g"`.</span></span> <span data-ttu-id="f59cc-215">Dodano również `"spark.kryoserializer.buffer.max"` o wartości `"256m"`.</span><span class="sxs-lookup"><span data-stu-id="f59cc-215">It also adds `"spark.kryoserializer.buffer.max"` with a value of `"256m"`.</span></span>
   
        "spark.yarn.am.memory": "3g",
        "spark.kyroserializer.buffer.max": "256m",
   
    <span data-ttu-id="f59cc-216">Zapisz plik hello, po zakończeniu wprowadzania zmian.</span><span class="sxs-lookup"><span data-stu-id="f59cc-216">Save hello file once you are done making modifications.</span></span>

4. <span data-ttu-id="f59cc-217">Użyj następującego polecenia toosubmit hello aktualizacji konfiguracji tooAmbari hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-217">Use hello following commands toosubmit hello updated configuration tooAmbari.</span></span>
   
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
   
    <span data-ttu-id="f59cc-218">Te polecenia przesłać zawartość hello hello **newconfig.json** plików w klastrze toohello hello nowych Konfiguracja żądanego.</span><span class="sxs-lookup"><span data-stu-id="f59cc-218">These commands submit hello contents of hello **newconfig.json** file toohello cluster as hello new desired configuration.</span></span> <span data-ttu-id="f59cc-219">Żądanie hello zwraca dokumentu JSON.</span><span class="sxs-lookup"><span data-stu-id="f59cc-219">hello request returns a JSON document.</span></span> <span data-ttu-id="f59cc-220">Witaj **versionTag** element w tym dokumencie powinna być zgodna wersja hello przesłane i hello **configs** obiekt zawiera zmiany konfiguracji hello żądanego.</span><span class="sxs-lookup"><span data-stu-id="f59cc-220">hello **versionTag** element in this document should match hello version you submitted, and hello **configs** object contains hello configuration changes you requested.</span></span>

### <a name="example-restart-a-service-component"></a><span data-ttu-id="f59cc-221">Przykład: Ponowne uruchomienie składnika usługi</span><span class="sxs-lookup"><span data-stu-id="f59cc-221">Example: Restart a service component</span></span>

<span data-ttu-id="f59cc-222">W tym momencie można spojrzeć na powitania interfejsu użytkownika sieci web Ambari, hello usługę platformy Spark wskazuje, że wymaga ona toobe po ponownym uruchomieniu hello nowej konfiguracji zostały wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="f59cc-222">At this point, if you look at hello Ambari web UI, hello Spark service indicates that it needs toobe restarted before hello new configuration can take effect.</span></span> <span data-ttu-id="f59cc-223">Użyj hello następujące kroki toorestart hello usługi.</span><span class="sxs-lookup"><span data-stu-id="f59cc-223">Use hello following steps toorestart hello service.</span></span>

1. <span data-ttu-id="f59cc-224">Użyj powitania po tooenable trybu konserwacji dla hello usługę platformy Spark:</span><span class="sxs-lookup"><span data-stu-id="f59cc-224">Use hello following tooenable maintenance mode for hello Spark service:</span></span>

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
   
    <span data-ttu-id="f59cc-225">Te polecenia Wyślij serwer toohello dokumentów JSON, który powoduje włączenie trybu konserwacji.</span><span class="sxs-lookup"><span data-stu-id="f59cc-225">These commands send a JSON document toohello server that turns on maintenance mode.</span></span> <span data-ttu-id="f59cc-226">Aby sprawdzić, usługa hello jest teraz w trybie konserwacji przy użyciu hello następujące żądania:</span><span class="sxs-lookup"><span data-stu-id="f59cc-226">You can verify that hello service is now in maintenance mode using hello following request:</span></span>
   
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
   
    <span data-ttu-id="f59cc-227">Witaj zwracana wartość jest `ON`.</span><span class="sxs-lookup"><span data-stu-id="f59cc-227">hello return value is `ON`.</span></span>

2. <span data-ttu-id="f59cc-228">Następnie użyj powitania po tooturn poza hello usługi:</span><span class="sxs-lookup"><span data-stu-id="f59cc-228">Next, use hello following tooturn off hello service:</span></span>

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
    
    <span data-ttu-id="f59cc-229">odpowiedź Hello jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="f59cc-229">hello response is similar toohello following example:</span></span>
   
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
    > <span data-ttu-id="f59cc-230">Witaj `href` wartość zwrócona przez ten identyfikator URI jest używany wewnętrzny adres IP hello hello węzła klastra.</span><span class="sxs-lookup"><span data-stu-id="f59cc-230">hello `href` value returned by this URI is using hello internal IP address of hello cluster node.</span></span> <span data-ttu-id="f59cc-231">toouse części hello "10.0.0.18:8080" z poziomu zewnętrznej hello klastra, Zamień hello nazwę FQDN klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f59cc-231">toouse it from outside hello cluster, replace hello \`10.0.0.18:8080' portion with hello FQDN of hello cluster.</span></span> 
    
    <span data-ttu-id="f59cc-232">następujące polecenia Hello pobrać stanu hello hello żądania:</span><span class="sxs-lookup"><span data-stu-id="f59cc-232">hello following commands retrieve hello status of hello request:</span></span>

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

    <span data-ttu-id="f59cc-233">Odpowiedź `COMPLETED` wskazuje hello żądanie zostało ukończone.</span><span class="sxs-lookup"><span data-stu-id="f59cc-233">A response of `COMPLETED` indicates that hello request has finished.</span></span>

3. <span data-ttu-id="f59cc-234">Po ukończeniu poprzedniego żądania hello, użyj powitania po toostart hello usługi.</span><span class="sxs-lookup"><span data-stu-id="f59cc-234">Once hello previous request completes, use hello following toostart hello service.</span></span>
   
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
    <span data-ttu-id="f59cc-235">Usługa Hello jest teraz, używając hello nowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f59cc-235">hello service is now using hello new configuration.</span></span>

4. <span data-ttu-id="f59cc-236">Na koniec użyj powitania po tooturn Wyłącz tryb konserwacji.</span><span class="sxs-lookup"><span data-stu-id="f59cc-236">Finally, use hello following tooturn off maintenance mode.</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="f59cc-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f59cc-237">Next steps</span></span>

<span data-ttu-id="f59cc-238">Pełną dokumentację hello interfejsu API REST, zobacz [Ambari API odwołanie V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="f59cc-238">For a complete reference of hello REST API, see [Ambari API Reference V1](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

