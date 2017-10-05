---
title: "Monitorowanie klastrów platformy Hadoop w usłudze HDInsight przy użyciu interfejsu API Ambari - Azure | Dokumentacja firmy Microsoft"
description: "Przy użyciu interfejsów API Apache Ambari do tworzenia, zarządzania i monitorowania klastrów platformy Hadoop. Operator intuicyjne narzędzia i interfejsy API neutralizują złożoność platformy Hadoop."
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
ms.openlocfilehash: b6fc2098027690eb76b69b1427f0e9541b8a7a69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-the-ambari-api"></a><span data-ttu-id="3a2b2-104">Zarządzanie klastrami Hadoop w usłudze HDInsight przy użyciu interfejsów API systemu Ambari</span><span class="sxs-lookup"><span data-stu-id="3a2b2-104">Monitor Hadoop clusters in HDInsight using the Ambari API</span></span>
<span data-ttu-id="3a2b2-105">Informacje o sposobie monitorowania klastrów usługi HDInsight przy użyciu Ambari API.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-105">Learn how to monitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="3a2b2-106">Informacje przedstawione w tym artykule jest głównie do klastrów usługi HDInsight opartej na systemie Windows, które udostępnia wersji interfejsu API REST Ambari tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-106">The information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of the Ambari REST API.</span></span> <span data-ttu-id="3a2b2-107">W klastrach opartych na systemie Linux, zobacz [klastry Hadoop zarządzanie przy użyciu narzędzia Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="3a2b2-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="3a2b2-108">Co to jest Ambari?</span><span class="sxs-lookup"><span data-stu-id="3a2b2-108">What is Ambari?</span></span>
<span data-ttu-id="3a2b2-109">[Apache Ambari] [ ambari-home] służy do inicjowania obsługi, zarządzania i monitorowania klastrów platformy Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="3a2b2-110">Obejmuje intuicyjny zestaw narzędzi operatora oraz niezawodny zestaw interfejsów API, które neutralizują złożoność platformy Hadoop, upraszczając działanie klastrów.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide the complexity of Hadoop, simplifying the operation of clusters.</span></span> <span data-ttu-id="3a2b2-111">Aby uzyskać więcej informacji na temat interfejsów API, zobacz [Ambari API Reference][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="3a2b2-111">For more information about the APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="3a2b2-112">HDInsight aktualnie obsługuje tylko funkcja monitorowania Ambari.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-112">HDInsight currently supports only the Ambari monitoring feature.</span></span> <span data-ttu-id="3a2b2-113">Ambari API 1.0 jest obsługiwany przez klastry usługi HDInsight w wersji 3.0 i 2.1.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="3a2b2-114">W tym artykule omówiono podczas uzyskiwania dostępu do interfejsów API Ambari klastrów usługi HDInsight w wersji 3.1 i 2.1.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="3a2b2-115">Najważniejsza różnica między nimi jest niektóre składniki zostały zmienione wraz z wprowadzeniem nowych możliwości (na przykład serwer historii zadań).</span><span class="sxs-lookup"><span data-stu-id="3a2b2-115">The key difference between the two is that some of the components have changed with the introduction of new capabilities (such as the Job History Server).</span></span> 

<span data-ttu-id="3a2b2-116">**Wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="3a2b2-116">**Prerequisites**</span></span>

<span data-ttu-id="3a2b2-117">Przed przystąpieniem do wykonywania kroków opisanych w tym samouczku musisz mieć poniższe:</span><span class="sxs-lookup"><span data-stu-id="3a2b2-117">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="3a2b2-118">**Stacja robocza z programem Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="3a2b2-119">(Opcjonalnie) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="3a2b2-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="3a2b2-120">Aby go zainstalować, zobacz [cURL wersje i pliki do pobrania][curl-download].</span><span class="sxs-lookup"><span data-stu-id="3a2b2-120">To install it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3a2b2-121">Kiedy używać polecenia cURL w systemie Windows, użyj w podwójny cudzysłów zamiast pojedynczego cudzysłowu do wartości opcji.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-121">When use the cURL command in Windows, use double-quotation marks instead of single-quotation marks for the option values.</span></span>
  > 
  > 
* <span data-ttu-id="3a2b2-122">**Klaster Azure HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="3a2b2-123">Aby uzyskać instrukcje dotyczące inicjowania obsługi klastra, zobacz [rozpocząć korzystanie z usługi HDInsight] [ hdinsight-get-started] lub [Obsługa administracyjna klastrów HDInsight][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="3a2b2-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="3a2b2-124">Potrzebne są następujące dane do wykonywania kroków samouczka:</span><span class="sxs-lookup"><span data-stu-id="3a2b2-124">You need the following data to go through the tutorial:</span></span>
  
  | <span data-ttu-id="3a2b2-125">Właściwości klastra</span><span class="sxs-lookup"><span data-stu-id="3a2b2-125">Cluster property</span></span> | <span data-ttu-id="3a2b2-126">Nazwa zmiennej platformy Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3a2b2-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="3a2b2-127">Wartość</span><span class="sxs-lookup"><span data-stu-id="3a2b2-127">Value</span></span> | <span data-ttu-id="3a2b2-128">Opis</span><span class="sxs-lookup"><span data-stu-id="3a2b2-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="3a2b2-129">Nazwa klastra usługi HDInsight</span><span class="sxs-lookup"><span data-stu-id="3a2b2-129">HDInsight cluster name</span></span> |<span data-ttu-id="3a2b2-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="3a2b2-130">$clusterName</span></span> | |<span data-ttu-id="3a2b2-131">Nazwa klastra usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-131">The name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="3a2b2-132">Nazwa użytkownika klastra</span><span class="sxs-lookup"><span data-stu-id="3a2b2-132">Cluster username</span></span> |<span data-ttu-id="3a2b2-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="3a2b2-133">$clusterUsername</span></span> | |<span data-ttu-id="3a2b2-134">Określona nazwa użytkownika klastra podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-134">Cluster user name specified when the cluster was created.</span></span> |
  |   <span data-ttu-id="3a2b2-135">Hasło klastra</span><span class="sxs-lookup"><span data-stu-id="3a2b2-135">Cluster password</span></span> |<span data-ttu-id="3a2b2-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="3a2b2-136">$clusterPassword</span></span> | |<span data-ttu-id="3a2b2-137">Hasło użytkownika klastra.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="3a2b2-138">Szybkie rozpoczęcie tworzenia</span><span class="sxs-lookup"><span data-stu-id="3a2b2-138">Jump-start</span></span>
<span data-ttu-id="3a2b2-139">Istnieje kilka sposobów, aby używać narzędzia Ambari do monitorowania klastrów usługi HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-139">There are several ways to use Ambari to monitor HDInsight clusters.</span></span>

<span data-ttu-id="3a2b2-140">**Korzystanie z programu Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3a2b2-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="3a2b2-141">Poniższy skrypt programu PowerShell Azure pobiera informacji o śledzeniu zadania MapReduce *w klastrze HDInsight 3.5.*</span><span class="sxs-lookup"><span data-stu-id="3a2b2-141">The following Azure PowerShell script gets the MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="3a2b2-142">Najważniejsza różnica polega na tym, że możemy pobierać te szczegóły usługi YARN (zamiast MapReduce).</span><span class="sxs-lookup"><span data-stu-id="3a2b2-142">The key difference is that we pull these details from the YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="3a2b2-143">Poniższy skrypt programu PowerShell pobiera informacji o śledzeniu zadania MapReduce *w klastrze HDInsight 2.1*:</span><span class="sxs-lookup"><span data-stu-id="3a2b2-143">The following PowerShell script gets the MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="3a2b2-144">Wynik jest:</span><span class="sxs-lookup"><span data-stu-id="3a2b2-144">The output is:</span></span>

![Dane wyjściowe Jobtracker][img-jobtracker-output]

<span data-ttu-id="3a2b2-146">**Korzystanie z programu cURL**</span><span class="sxs-lookup"><span data-stu-id="3a2b2-146">**Use cURL**</span></span>

<span data-ttu-id="3a2b2-147">Poniższy przykład pobiera informacje o klastrze przy użyciu cURL:</span><span class="sxs-lookup"><span data-stu-id="3a2b2-147">The following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="3a2b2-148">Wynik jest:</span><span class="sxs-lookup"><span data-stu-id="3a2b2-148">The output is:</span></span>

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

<span data-ttu-id="3a2b2-149">**W wersji 2014-10-8**:</span><span class="sxs-lookup"><span data-stu-id="3a2b2-149">**For the 10/8/2014 release**:</span></span>

<span data-ttu-id="3a2b2-150">Korzystając z punktu końcowego Ambari "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", *host_name* pola Zwraca pełną nazwę domeny (FQDN) węzła zamiast nazwy hosta.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-150">When using the Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", the *host_name* field returns the fully qualified domain name (FQDN) of the node instead of the host name.</span></span> <span data-ttu-id="3a2b2-151">Przed wprowadzeniem 2014-10-8, w tym przykładzie zwracane po prostu "**headnode0**".</span><span class="sxs-lookup"><span data-stu-id="3a2b2-151">Before the 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="3a2b2-152">Po wydaniu 2014-10-8, możesz uzyskać nazwę FQDN "**headnode0. { Gt;. azurehdinsight.NET ClusterDNS} .net**", jak pokazano w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-152">After the 10/8/2014 release, you get the FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in the previous example.</span></span> <span data-ttu-id="3a2b2-153">Ta zmiana została wymagane do ułatwienia scenariuszy, w którym można wdrożyć wiele typów klastra (na przykład HBase i Hadoop) w jedną sieć wirtualną (VNET).</span><span class="sxs-lookup"><span data-stu-id="3a2b2-153">This change was required to facilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="3a2b2-154">Dzieje się tak, na przykład w przypadku używania bazy danych HBase jako platforma wewnętrzna dla platformy Hadoop.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="3a2b2-155">Ambari API monitorowania</span><span class="sxs-lookup"><span data-stu-id="3a2b2-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="3a2b2-156">W poniższej tabeli wymieniono niektóre z najczęściej Ambari monitorowania wywołań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-156">The following table lists some of the most common Ambari monitoring API calls.</span></span> <span data-ttu-id="3a2b2-157">Aby uzyskać więcej informacji na temat interfejsu API, zobacz [Ambari API Reference][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="3a2b2-157">For more information about the API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="3a2b2-158">Wywołanie interfejsu API Monitora</span><span class="sxs-lookup"><span data-stu-id="3a2b2-158">Monitor API call</span></span> | <span data-ttu-id="3a2b2-159">IDENTYFIKATOR URI</span><span class="sxs-lookup"><span data-stu-id="3a2b2-159">URI</span></span> | <span data-ttu-id="3a2b2-160">Opis</span><span class="sxs-lookup"><span data-stu-id="3a2b2-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a2b2-161">Pobierz klastrów</span><span class="sxs-lookup"><span data-stu-id="3a2b2-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="3a2b2-162">Pobierz informacje o klastrze.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="3a2b2-163">klastry usług, hosty</span><span class="sxs-lookup"><span data-stu-id="3a2b2-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="3a2b2-164">Pobierz usługi</span><span class="sxs-lookup"><span data-stu-id="3a2b2-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="3a2b2-165">Usługi obejmują: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="3a2b2-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="3a2b2-166">Pobierz informacje o usługach.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="3a2b2-167">Pobierz składniki usługi</span><span class="sxs-lookup"><span data-stu-id="3a2b2-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="3a2b2-168">System plików HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="3a2b2-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="3a2b2-169">Pobierz informacje składnika.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="3a2b2-170">ServiceComponentInfo, składniki hosta, metryki</span><span class="sxs-lookup"><span data-stu-id="3a2b2-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="3a2b2-171">Pobierz hostów</span><span class="sxs-lookup"><span data-stu-id="3a2b2-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="3a2b2-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="3a2b2-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="3a2b2-173">Pobierz informacje o hoście.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="3a2b2-174">Pobieranie składników hosta</span><span class="sxs-lookup"><span data-stu-id="3a2b2-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="3a2b2-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="3a2b2-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="3a2b2-176">Pobierz informacje składnika hosta.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="3a2b2-177">HostRoles, składników, hosta i metryki</span><span class="sxs-lookup"><span data-stu-id="3a2b2-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="3a2b2-178">Uzyskiwanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="3a2b2-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="3a2b2-179">Typy konfiguracji: lokacji podstawowej, lokacji systemu plików hdfs, mapred lokacji, lokacji gałęzi</span><span class="sxs-lookup"><span data-stu-id="3a2b2-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="3a2b2-180">Pobierz informacje o konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="3a2b2-181">Typy konfiguracji: lokacji podstawowej, lokacji systemu plików hdfs, mapred lokacji, lokacji gałęzi</span><span class="sxs-lookup"><span data-stu-id="3a2b2-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3a2b2-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3a2b2-182">Next Steps</span></span>
<span data-ttu-id="3a2b2-183">Teraz ma pokazaliśmy, jak używać narzędzia Ambari monitorowania wywołań interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3a2b2-183">Now you have learned how to use Ambari monitoring API calls.</span></span> <span data-ttu-id="3a2b2-184">Aby dowiedzieć się więcej, zobacz:</span><span class="sxs-lookup"><span data-stu-id="3a2b2-184">To learn more, see:</span></span>

* <span data-ttu-id="3a2b2-185">[Zarządzanie klastrami HDInsight przy użyciu portalu Azure][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="3a2b2-185">[Manage HDInsight clusters using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="3a2b2-186">[Zarządzanie klastrami HDInsight przy użyciu programu Azure PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="3a2b2-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="3a2b2-187">[Zarządzanie klastrami HDInsight przy użyciu interfejsu wiersza polecenia][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="3a2b2-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="3a2b2-188">[Dokumentacja dotycząca usługi HDInsight][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="3a2b2-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="3a2b2-189">[Rozpoczynanie pracy z usługą HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="3a2b2-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

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
