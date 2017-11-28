---
title: "aaaMonitor klastrów platformy Hadoop w usłudze HDInsight przy użyciu Ambari API - tekst hello Azure | Dokumentacja firmy Microsoft"
description: "Użyj hello Apache Ambari API do tworzenia, zarządzania i monitorowania klastrów platformy Hadoop. Operator intuicyjne narzędzia i interfejsy API Ukryj hello złożoność platformy Hadoop."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="afda1-104">Monitorowanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu Ambari API hello</span><span class="sxs-lookup"><span data-stu-id="afda1-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="afda1-105">Dowiedz się, jak toomonitor HDInsight clusters przy użyciu Ambari API.</span><span class="sxs-lookup"><span data-stu-id="afda1-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="afda1-106">Witaj informacje w tym artykule jest przeznaczone głównie dla klastrów usługi HDInsight opartej na systemie Windows, które udostępnia hello interfejsu API REST Ambari wersji tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="afda1-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="afda1-107">W klastrach opartych na systemie Linux, zobacz [klastry Hadoop zarządzanie przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="afda1-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="afda1-108">Co to jest Ambari?</span><span class="sxs-lookup"><span data-stu-id="afda1-108">What is Ambari?</span></span>
<span data-ttu-id="afda1-109">[Apache Ambari] [ ambari-home] służy do inicjowania obsługi, zarządzania i monitorowania klastrów platformy Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="afda1-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="afda1-110">Obejmuje intuicyjny zestaw narzędzi operatora oraz niezawodny zestaw interfejsów API, które neutralizują złożoność hello Hadoop, upraszczając działanie hello klastrów.</span><span class="sxs-lookup"><span data-stu-id="afda1-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="afda1-111">Aby uzyskać więcej informacji na temat hello interfejsów API, zobacz [Ambari API Reference][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="afda1-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="afda1-112">HDInsight aktualnie obsługuje tylko hello Ambari funkcji monitorowania.</span><span class="sxs-lookup"><span data-stu-id="afda1-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="afda1-113">Ambari API 1.0 jest obsługiwany przez klastry usługi HDInsight w wersji 3.0 i 2.1.</span><span class="sxs-lookup"><span data-stu-id="afda1-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="afda1-114">W tym artykule omówiono podczas uzyskiwania dostępu do interfejsów API Ambari klastrów usługi HDInsight w wersji 3.1 i 2.1.</span><span class="sxs-lookup"><span data-stu-id="afda1-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="afda1-115">Hello Najważniejsza różnica między hello dwa jest niektórych składników hello zostały zmienione z hello wprowadzenie nowych funkcji (na przykład powitania serwera historii zadań).</span><span class="sxs-lookup"><span data-stu-id="afda1-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="afda1-116">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="afda1-116">**Prerequisites**</span></span>

<span data-ttu-id="afda1-117">Przed rozpoczęciem tego samouczka, musi mieć hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="afda1-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="afda1-118">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="afda1-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="afda1-119">(Opcjonalnie) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="afda1-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="afda1-120">tooinstall, zobacz [cURL wersje i pliki do pobrania][curl-download].</span><span class="sxs-lookup"><span data-stu-id="afda1-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="afda1-121">Kiedy używać polecenia cURL hello w systemie Windows, użyj w podwójny cudzysłów zamiast pojedynczego cudzysłowu do wartości opcji hello.</span><span class="sxs-lookup"><span data-stu-id="afda1-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="afda1-122">**Klaster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="afda1-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="afda1-123">Aby uzyskać instrukcje dotyczące inicjowania obsługi klastra, zobacz [rozpocząć korzystanie z usługi HDInsight] [ hdinsight-get-started] lub [Obsługa administracyjna klastrów HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="afda1-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="afda1-124">Należy powitania po toogo danych samouczkiem hello:</span><span class="sxs-lookup"><span data-stu-id="afda1-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="afda1-125">Właściwości klastra</span><span class="sxs-lookup"><span data-stu-id="afda1-125">Cluster property</span></span> | <span data-ttu-id="afda1-126">Nazwa zmiennej platformy Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="afda1-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="afda1-127">Wartość</span><span class="sxs-lookup"><span data-stu-id="afda1-127">Value</span></span> | <span data-ttu-id="afda1-128">Opis</span><span class="sxs-lookup"><span data-stu-id="afda1-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="afda1-129">Nazwa klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="afda1-129">HDInsight cluster name</span></span> |<span data-ttu-id="afda1-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="afda1-130">$clusterName</span></span> | |<span data-ttu-id="afda1-131">Nazwa Hello z klastrem usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="afda1-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="afda1-132">Nazwa użytkownika klastra</span><span class="sxs-lookup"><span data-stu-id="afda1-132">Cluster username</span></span> |<span data-ttu-id="afda1-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="afda1-133">$clusterUsername</span></span> | |<span data-ttu-id="afda1-134">Określona nazwa użytkownika klastra podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="afda1-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="afda1-135">Hasło klastra</span><span class="sxs-lookup"><span data-stu-id="afda1-135">Cluster password</span></span> |<span data-ttu-id="afda1-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="afda1-136">$clusterPassword</span></span> | |<span data-ttu-id="afda1-137">Hasło użytkownika klastra.</span><span class="sxs-lookup"><span data-stu-id="afda1-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="afda1-138">Szybkie rozpoczęcie tworzenia</span><span class="sxs-lookup"><span data-stu-id="afda1-138">Jump-start</span></span>
<span data-ttu-id="afda1-139">Istnieje kilka sposobów klastrów usługi HDInsight toomonitor Ambari toouse.</span><span class="sxs-lookup"><span data-stu-id="afda1-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="afda1-140">**Korzystanie z programu Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="afda1-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="afda1-141">Witaj następującego skryptu programu Azure PowerShell pobiera informacje śledzenia zadań MapReduce hello *w klastrze HDInsight 3.5.*</span><span class="sxs-lookup"><span data-stu-id="afda1-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="afda1-142">Witaj Najważniejsza różnica polega na tym, że możemy pobierać te szczegóły usługi YARN hello (zamiast MapReduce).</span><span class="sxs-lookup"><span data-stu-id="afda1-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="afda1-143">Witaj następującego skryptu programu PowerShell pobiera informacje śledzenia zadań MapReduce hello *w klastrze HDInsight 2.1*:</span><span class="sxs-lookup"><span data-stu-id="afda1-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="afda1-144">dane wyjściowe Hello to:</span><span class="sxs-lookup"><span data-stu-id="afda1-144">hello output is:</span></span>

![Dane wyjściowe Jobtracker][img-jobtracker-output]

<span data-ttu-id="afda1-146">**Korzystanie z programu cURL**</span><span class="sxs-lookup"><span data-stu-id="afda1-146">**Use cURL**</span></span>

<span data-ttu-id="afda1-147">Witaj poniższy przykład pobiera informacje o klastrze przy użyciu cURL:</span><span class="sxs-lookup"><span data-stu-id="afda1-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="afda1-148">dane wyjściowe Hello to:</span><span class="sxs-lookup"><span data-stu-id="afda1-148">hello output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="afda1-149">**W wersji 2014-10-8 hello**:</span><span class="sxs-lookup"><span data-stu-id="afda1-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="afda1-150">Gdy przy użyciu Ambari hello punktu końcowego, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* pola Zwraca hello pełną nazwę domeny (FQDN) węzła hello zamiast hello nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="afda1-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="afda1-151">Przed wprowadzeniem 2014-10-8 hello, w tym przykładzie zwracane po prostu "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="afda1-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="afda1-152">Po wydaniu 2014-10-8 hello, możesz uzyskać hello FQDN "**headnode0. { Gt;. azurehdinsight.NET ClusterDNS} .net**", jak pokazano w poprzednim przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="afda1-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="afda1-153">Ta zmiana została scenariusze wymagane toofacilitate wdrożonym wiele typów klastra (na przykład HBase i Hadoop) w jedną sieć wirtualną (VNET).</span><span class="sxs-lookup"><span data-stu-id="afda1-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="afda1-154">Dzieje się tak, na przykład w przypadku używania bazy danych HBase jako platforma wewnętrzna dla platformy Hadoop.</span><span class="sxs-lookup"><span data-stu-id="afda1-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="afda1-155">Ambari API monitorowania</span><span class="sxs-lookup"><span data-stu-id="afda1-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="afda1-156">Witaj poniższej tabeli przedstawiono niektóre hello najbardziej typowe narzędzia Ambari monitorowania wywołań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="afda1-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="afda1-157">Aby uzyskać więcej informacji na temat hello interfejsu API, zobacz [Ambari API Reference][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="afda1-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="afda1-158">Wywołanie interfejsu API Monitora</span><span class="sxs-lookup"><span data-stu-id="afda1-158">Monitor API call</span></span> | <span data-ttu-id="afda1-159">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="afda1-159">URI</span></span> | <span data-ttu-id="afda1-160">Opis</span><span class="sxs-lookup"><span data-stu-id="afda1-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="afda1-161">Pobierz klastrów</span><span class="sxs-lookup"><span data-stu-id="afda1-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="afda1-162">Pobierz informacje o klastrze.</span><span class="sxs-lookup"><span data-stu-id="afda1-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="afda1-163">klastry usług, hosty</span><span class="sxs-lookup"><span data-stu-id="afda1-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="afda1-164">Pobierz usługi</span><span class="sxs-lookup"><span data-stu-id="afda1-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="afda1-165">Usługi obejmują: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="afda1-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="afda1-166">Pobierz informacje o usługach.</span><span class="sxs-lookup"><span data-stu-id="afda1-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="afda1-167">Pobierz składniki usługi</span><span class="sxs-lookup"><span data-stu-id="afda1-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="afda1-168">System plików HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="afda1-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="afda1-169">Pobierz informacje składnika.</span><span class="sxs-lookup"><span data-stu-id="afda1-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="afda1-170">ServiceComponentInfo, składniki hosta, metryki</span><span class="sxs-lookup"><span data-stu-id="afda1-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="afda1-171">Pobierz hostów</span><span class="sxs-lookup"><span data-stu-id="afda1-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="afda1-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="afda1-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="afda1-173">Pobierz informacje o hoście.</span><span class="sxs-lookup"><span data-stu-id="afda1-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="afda1-174">Pobieranie składników hosta</span><span class="sxs-lookup"><span data-stu-id="afda1-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="afda1-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="afda1-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="afda1-176">Pobierz informacje składnika hosta.</span><span class="sxs-lookup"><span data-stu-id="afda1-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="afda1-177">HostRoles, składników, hosta i metryki</span><span class="sxs-lookup"><span data-stu-id="afda1-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="afda1-178">Uzyskiwanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="afda1-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="afda1-179">Typy konfiguracji: lokacji podstawowej, lokacji systemu plików hdfs, mapred lokacji, lokacji gałęzi</span><span class="sxs-lookup"><span data-stu-id="afda1-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="afda1-180">Pobierz informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="afda1-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="afda1-181">Typy konfiguracji: lokacji podstawowej, lokacji systemu plików hdfs, mapred lokacji, lokacji gałęzi</span><span class="sxs-lookup"><span data-stu-id="afda1-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="afda1-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="afda1-182">Next Steps</span></span>
<span data-ttu-id="afda1-183">Teraz wiesz już, jak wywołuje Ambari API monitorowania toouse.</span><span class="sxs-lookup"><span data-stu-id="afda1-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="afda1-184">toolearn więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="afda1-184">toolearn more, see:</span></span>

* <span data-ttu-id="afda1-185">[Zarządzanie klastrami HDInsight przy użyciu hello portalu Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="afda1-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="afda1-186">[Zarządzanie klastrami HDInsight przy użyciu programu Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="afda1-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="afda1-187">[Zarządzanie klastrami HDInsight przy użyciu interfejsu wiersza polecenia][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="afda1-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="afda1-188">[Dokumentacja dotycząca usługi HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="afda1-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="afda1-189">[Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="afda1-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
