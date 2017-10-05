---
title: "Konfigurowanie klastra autonomiczny sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować autonomiczny lub prywatnej klastra sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: 9885dce18dabac4a945dafd219e3ae190e34a83b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="a21a3-103">Ustawienia konfiguracji dla autonomicznych klastra systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a21a3-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="a21a3-104">W tym artykule opisano sposób konfigurowania autonomicznej usługi sieć szkieletowa klastra za pomocą ***pliku ClusterConfig.JSON*** pliku.</span><span class="sxs-lookup"><span data-stu-id="a21a3-104">This article describes how to configure a standalone Service Fabric cluster using the ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="a21a3-105">Ten plik służy do określ informacje, takie jak węzłów sieci szkieletowej usług i ich adresy IP, różne typy węzłów na klaster, konfiguracjach zabezpieczeń, a także topologii sieci pod względem błędów/uaktualnienia domen, dla klastra autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="a21a3-105">You can use this file to specify information such as the Service Fabric nodes and their IP addresses, different types of nodes on the cluster, the security configurations as well as the network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="a21a3-106">Gdy można [Pobierz autonomiczny pakiet sieci szkieletowej usług](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), na komputerze pracy są pobierane kilka przykładów pliku pliku ClusterConfig.JSON.</span><span class="sxs-lookup"><span data-stu-id="a21a3-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of the ClusterConfig.JSON file are downloaded to your work machine.</span></span> <span data-ttu-id="a21a3-107">Próbki o *DevCluster* w nazwach zawierają informacje pomocne podczas tworzenia klastra ze wszystkich trzech węzłów na tym samym komputerze, takich jak logicznej węzłów.</span><span class="sxs-lookup"><span data-stu-id="a21a3-107">The samples having *DevCluster* in their names will help you create a cluster with all three nodes on the same machine, like logical nodes.</span></span> <span data-ttu-id="a21a3-108">Poza tym przypadku co najmniej jeden węzeł może być oznaczona jako węzła podstawowego.</span><span class="sxs-lookup"><span data-stu-id="a21a3-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="a21a3-109">Ten klaster jest przydatne w środowisku projektowania lub testowym i nie jest obsługiwany jako klastra produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a21a3-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="a21a3-110">Próbki o *MultiMachine* w nazwach, pomoże utworzyć klaster jakości produkcyjnych z każdego węzła na osobnym komputerze.</span><span class="sxs-lookup"><span data-stu-id="a21a3-110">The samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="a21a3-111">*ClusterConfig.Unsecure.DevCluster.JSON* i *ClusterConfig.Unsecure.MultiMachine.JSON* pokazują, jak utworzyć odpowiednio niezabezpieczona testowym lub produkcyjnym klastra.</span><span class="sxs-lookup"><span data-stu-id="a21a3-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how to create an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="a21a3-112">*ClusterConfig.Windows.DevCluster.JSON* i *ClusterConfig.Windows.MultiMachine.JSON* pokazują, jak utworzyć klaster testowym lub produkcyjnym chronione za pomocą [zabezpieczenia systemu Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="a21a3-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how to create test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="a21a3-113">*ClusterConfig.X509.DevCluster.JSON* i *ClusterConfig.X509.MultiMachine.JSON* pokazują, jak utworzyć klaster testowym lub produkcyjnym chronione za pomocą [X509 zabezpieczeń oparte na certyfikatach](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="a21a3-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how to create test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="a21a3-114">Teraz zostanie omówione różnych części ***pliku ClusterConfig.JSON*** plików zgodnie z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="a21a3-114">Now we will examine the various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="a21a3-115">Konfiguracje klastrów ogólne</span><span class="sxs-lookup"><span data-stu-id="a21a3-115">General cluster configurations</span></span>
<span data-ttu-id="a21a3-116">Obejmuje określonej konfiguracji klastra szerokie, jak pokazano poniżej fragment kodu JSON.</span><span class="sxs-lookup"><span data-stu-id="a21a3-116">This covers the broad cluster specific configurations, as shown in the JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="a21a3-117">Może być dowolną przyjazną nazwę klastra sieci szkieletowej usług przez przypisanie go do **nazwa** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="a21a3-117">You can give any friendly name to your Service Fabric cluster by assigning it to the **name** variable.</span></span> <span data-ttu-id="a21a3-118">**ClusterConfigurationVersion** jest numer wersji klastra; należy zwiększyć jego każdorazowego uaktualnienia klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="a21a3-118">The **clusterConfigurationVersion** is the version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="a21a3-119">Jednak należy pozostawić **apiVersion** na wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="a21a3-119">You should however leave the **apiVersion** to the default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a><span data-ttu-id="a21a3-120">Węzły w klastrze</span><span class="sxs-lookup"><span data-stu-id="a21a3-120">Nodes on the cluster</span></span>
<span data-ttu-id="a21a3-121">Węzły w klastrze usługi sieć szkieletowa można skonfigurować przy użyciu **węzłów** sekcji jako poniższy fragment kodu przedstawia.</span><span class="sxs-lookup"><span data-stu-id="a21a3-121">You can configure the nodes on your Service Fabric cluster by using the **nodes** section, as the following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="a21a3-122">Klaster sieci szkieletowej usług musi zawierać co najmniej 3 węzłach.</span><span class="sxs-lookup"><span data-stu-id="a21a3-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="a21a3-123">Zgodnie z ustawień, można dodać więcej węzłów do tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a21a3-123">You can add more nodes to this section as per your setup.</span></span> <span data-ttu-id="a21a3-124">W poniższej tabeli opisano ustawienia konfiguracji dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="a21a3-124">The following table explains the configuration settings for each node.</span></span>

| <span data-ttu-id="a21a3-125">**Konfiguracja węzła**</span><span class="sxs-lookup"><span data-stu-id="a21a3-125">**Node configuration**</span></span> | <span data-ttu-id="a21a3-126">**Opis**</span><span class="sxs-lookup"><span data-stu-id="a21a3-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="a21a3-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="a21a3-127">nodeName</span></span> |<span data-ttu-id="a21a3-128">Można nadać dowolną przyjazną nazwę do węzła.</span><span class="sxs-lookup"><span data-stu-id="a21a3-128">You can give any friendly name to the node.</span></span> |
| <span data-ttu-id="a21a3-129">Adres IP</span><span class="sxs-lookup"><span data-stu-id="a21a3-129">iPAddress</span></span> |<span data-ttu-id="a21a3-130">Sprawdzić adres IP węzła, otwierając okno polecenia i wpisując `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="a21a3-130">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="a21a3-131">Zanotuj adres IPV4 i przypisz go do **iPAddress** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="a21a3-131">Note the IPV4 address and assign it to the **iPAddress** variable.</span></span> |
| <span data-ttu-id="a21a3-132">wartość nodetyperef równą</span><span class="sxs-lookup"><span data-stu-id="a21a3-132">nodeTypeRef</span></span> |<span data-ttu-id="a21a3-133">Każdy węzeł można przypisać typu innego węzła.</span><span class="sxs-lookup"><span data-stu-id="a21a3-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="a21a3-134">[Typy węzłów](#nodetypes) są zdefiniowane w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a21a3-134">The [node types](#nodetypes) are defined in the section below.</span></span> |
| <span data-ttu-id="a21a3-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="a21a3-135">faultDomain</span></span> |<span data-ttu-id="a21a3-136">Domen błędów umożliwiają administratorom klastra zdefiniuj węzłów fizycznych, które może zakończyć się niepowodzeniem w tym samym czasie, z powodu zależności fizycznej udostępnionego.</span><span class="sxs-lookup"><span data-stu-id="a21a3-136">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span></span> |
| <span data-ttu-id="a21a3-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="a21a3-137">upgradeDomain</span></span> |<span data-ttu-id="a21a3-138">Domen uaktualnienia opisano zestaw węzłów, które są wyłączone uaktualnienia sieci szkieletowej usług na o tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="a21a3-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span></span> <span data-ttu-id="a21a3-139">Możesz węzły, które można przypisać do uaktualnienia domen, ponieważ nie są ograniczone przez wszystkie fizyczne wymagania.</span><span class="sxs-lookup"><span data-stu-id="a21a3-139">You can choose which nodes to assign to which Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="a21a3-140">Właściwości klastra</span><span class="sxs-lookup"><span data-stu-id="a21a3-140">Cluster properties</span></span>
<span data-ttu-id="a21a3-141">**Właściwości** sekcji w pliku ClusterConfig.JSON jest używany do konfigurowania klastra w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="a21a3-141">The **properties** section in the ClusterConfig.JSON is used to configure the cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="a21a3-142">Niezawodność</span><span class="sxs-lookup"><span data-stu-id="a21a3-142">Reliability</span></span>
<span data-ttu-id="a21a3-143">Pojęcie **reliabilityLevel** definiuje liczbę replik lub wystąpień usług systemowych sieci szkieletowej usług, które można uruchamiać na głównej węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="a21a3-143">The concept of **reliabilityLevel** defines the number of replicas or instances of the Service Fabric system services that can run on the primary nodes of the cluster.</span></span> <span data-ttu-id="a21a3-144">Określa niezawodności tych usług i tym samym klastrze.</span><span class="sxs-lookup"><span data-stu-id="a21a3-144">It determines the reliability of these services and hence the cluster.</span></span> <span data-ttu-id="a21a3-145">Wartość jest obliczeniowa przez system podczas tworzenia i uaktualniania klastra.</span><span class="sxs-lookup"><span data-stu-id="a21a3-145">The value is calcuated by the system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="a21a3-146">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="a21a3-146">Diagnostics</span></span>
<span data-ttu-id="a21a3-147">**DiagnosticsStore** sekcji pozwala na skonfigurowanie parametrów, aby włączyć diagnostyki i rozwiązywania problemów z węzła lub awarii klastra, jak pokazano w poniższy fragment kodu.</span><span class="sxs-lookup"><span data-stu-id="a21a3-147">The **diagnosticsStore** section allows you to configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="a21a3-148">**Metadanych** znajduje się opis diagnostycznej klastra i można ustawić odpowiednią konfigurację.</span><span class="sxs-lookup"><span data-stu-id="a21a3-148">The **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="a21a3-149">Te zmienne pomocy zbierania ETW dzienniki śledzenia, zrzuty awaryjne także liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="a21a3-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="a21a3-150">Odczyt [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) i [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) dzienniki śledzenia Aby uzyskać więcej informacji dotyczących funkcji ETW.</span><span class="sxs-lookup"><span data-stu-id="a21a3-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="a21a3-151">Wszystkie dzienniki tym [awarii zrzuty](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) i [liczniki wydajności](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) może zostać skierowany do **connectionString** folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="a21a3-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed to the **connectionString** folder on your machine.</span></span> <span data-ttu-id="a21a3-152">Można również użyć *AzureStorage* do przechowywania diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="a21a3-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="a21a3-153">Poniżej znajduje się fragment próbki.</span><span class="sxs-lookup"><span data-stu-id="a21a3-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="a21a3-154">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="a21a3-154">Security</span></span>
<span data-ttu-id="a21a3-155">**Zabezpieczeń** sekcja jest niezbędne do bezpiecznego autonomicznej klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="a21a3-155">The **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="a21a3-156">Poniższy fragment kodu przedstawia części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a21a3-156">The following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="a21a3-157">**Metadanych** opis klastra bezpiecznego a może ustawić odpowiednią konfigurację.</span><span class="sxs-lookup"><span data-stu-id="a21a3-157">The **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="a21a3-158">**ClusterCredentialType** i **ServerCredentialType** określają typ zabezpieczeń, który będzie implementowany klastra oraz węzłów.</span><span class="sxs-lookup"><span data-stu-id="a21a3-158">The **ClusterCredentialType** and **ServerCredentialType** determine the type of security that the cluster and the nodes will implement.</span></span> <span data-ttu-id="a21a3-159">Mogą być ustawione jako *X509* zabezpieczeń oparte na certyfikatach lub *Windows* dla zabezpieczeń opartych na usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a21a3-159">They can be set to either *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="a21a3-160">Pozostała część **zabezpieczeń** sekcji będą oparte na typ zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a21a3-160">The rest of the **security** section will be based on the type of the security.</span></span> <span data-ttu-id="a21a3-161">Odczytu [zabezpieczenia oparte na certyfikaty w klastrze autonomiczny](service-fabric-windows-cluster-x509-security.md) lub [zabezpieczenia systemu Windows w klastrze autonomiczny](service-fabric-windows-cluster-windows-security.md) informacji dotyczących wypełniania reszty **zabezpieczeń** sekcja.</span><span class="sxs-lookup"><span data-stu-id="a21a3-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how to fill out the rest of the **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="a21a3-162">Typy węzłów</span><span class="sxs-lookup"><span data-stu-id="a21a3-162">Node Types</span></span>
<span data-ttu-id="a21a3-163">**Elementów NodeType** sekcja opisuje typ węzłów, które ma w klastrze.</span><span class="sxs-lookup"><span data-stu-id="a21a3-163">The **nodeTypes** section describes the type of the nodes that your cluster has.</span></span> <span data-ttu-id="a21a3-164">Należy określić typ co najmniej jeden węzeł klastra, jak pokazano w poniższy fragment.</span><span class="sxs-lookup"><span data-stu-id="a21a3-164">At least one node type must be specified for a cluster, as shown in the snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="a21a3-165">**Nazwa** jest przyjazną nazwę dla tego typu określonego węzła.</span><span class="sxs-lookup"><span data-stu-id="a21a3-165">The **name** is the friendly name for this particular node type.</span></span> <span data-ttu-id="a21a3-166">Aby utworzyć węzeł tego typu węzła, przypisz przyjazną nazwę, którą **wartość nodetyperef równą** zmiennej dla tego węzła, jak wspomniano [powyżej](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="a21a3-166">To create a node of this node type, assign its friendly name to the **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="a21a3-167">Zdefiniuj punkty końcowe połączenia, które będą używane dla każdego typu węzła.</span><span class="sxs-lookup"><span data-stu-id="a21a3-167">For each node type, define the connection endpoints that will be used.</span></span> <span data-ttu-id="a21a3-168">Można wybrać dowolny inny numer portu na te punkty końcowe połączenia, tak długo, jak nie powodują konfliktów z innymi punktami końcowymi w tym klastrze.</span><span class="sxs-lookup"><span data-stu-id="a21a3-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="a21a3-169">W klastrze z wieloma węzłami, będzie co najmniej jeden węzeł podstawowy (tj. **isPrimary** ustawioną *true*), w zależności od [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="a21a3-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set to *true*), depending on the [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="a21a3-170">Odczyt [zagadnienia związane z planowaniem pojemności klastra usługi sieć szkieletowa](service-fabric-cluster-capacity.md) uzyskać informacji o **elementów NodeType** i **reliabilityLevel**oraz określenie, jakie są podstawowego i typy węzłów innych niż podstawowe.</span><span class="sxs-lookup"><span data-stu-id="a21a3-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and to know what are primary and the non-primary node types.</span></span> 

#### <a name="endpoints-used-to-configure-the-node-types"></a><span data-ttu-id="a21a3-171">Punkty końcowe umożliwiają skonfigurowanie typy węzłów</span><span class="sxs-lookup"><span data-stu-id="a21a3-171">Endpoints used to configure the node types</span></span>
* <span data-ttu-id="a21a3-172">*clientConnectionEndpointPort* to port używany przez klienta, aby połączyć się z klastrem, podczas korzystania z interfejsów API klienta.</span><span class="sxs-lookup"><span data-stu-id="a21a3-172">*clientConnectionEndpointPort* is the port used by the client to connect to the cluster, when using the client APIs.</span></span> 
* <span data-ttu-id="a21a3-173">*clusterConnectionEndpointPort* jest port, na jaką węzły komunikują się ze sobą.</span><span class="sxs-lookup"><span data-stu-id="a21a3-173">*clusterConnectionEndpointPort* is the port at which the nodes communicate with each other.</span></span>
* <span data-ttu-id="a21a3-174">*leaseDriverEndpointPort* jest port używany przez sterownik dzierżawę klastra, aby sprawdzić, czy węzły są nadal aktywne.</span><span class="sxs-lookup"><span data-stu-id="a21a3-174">*leaseDriverEndpointPort* is the port used by the cluster lease driver to find out if the nodes are still active.</span></span> 
* <span data-ttu-id="a21a3-175">*serviceConnectionEndpointPort* jest port używany przez aplikacje i usługi wdrożone w węźle do komunikacji z klientem usługi sieć szkieletowa na dany węzeł.</span><span class="sxs-lookup"><span data-stu-id="a21a3-175">*serviceConnectionEndpointPort* is the port used by the applications and services deployed on a node, to communicate with the Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="a21a3-176">*httpGatewayEndpointPort* jest port używany przez Service Fabric Explorer, aby połączyć się z klastrem.</span><span class="sxs-lookup"><span data-stu-id="a21a3-176">*httpGatewayEndpointPort* is the port used by the Service Fabric Explorer to connect to the cluster.</span></span>
* <span data-ttu-id="a21a3-177">*ephemeralPorts* zastąpienia [dynamiczne porty używane przez system operacyjny](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="a21a3-177">*ephemeralPorts* override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="a21a3-178">Sieć szkieletowa usług użyje części tych portów aplikacji i pozostałe będą dostępne dla systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="a21a3-178">Service Fabric will use a part of these as application ports and the remaining will be available for the OS.</span></span> <span data-ttu-id="a21a3-179">On również przypisze ten zakres do istniejący zakres obecne w systemie operacyjnym, więc dla wszystkich celów, można użyć zakresów podany w przykładowych plików JSON.</span><span class="sxs-lookup"><span data-stu-id="a21a3-179">It will also map this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span></span> <span data-ttu-id="a21a3-180">Należy się upewnić, że różnica między początek i koniec portów jest co najmniej 255.</span><span class="sxs-lookup"><span data-stu-id="a21a3-180">You need to make sure that the difference between the start and the end ports is at least 255.</span></span> <span data-ttu-id="a21a3-181">Jeśli różnica jest zbyt niski, ponieważ ten zakres jest udostępniony w systemie operacyjnym, może wystąpiły konflikty.</span><span class="sxs-lookup"><span data-stu-id="a21a3-181">You may run into conflicts if this difference is too low, since this range is shared with the operating system.</span></span> <span data-ttu-id="a21a3-182">Zobacz skonfigurowany dynamicznego zakresu portów, uruchamiając `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="a21a3-182">See the configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="a21a3-183">*applicationPorts* portów, które będą używane przez aplikacje, sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="a21a3-183">*applicationPorts* are the ports that will be used by the Service Fabric applications.</span></span> <span data-ttu-id="a21a3-184">Zakres portów aplikacji powinien być wystarczająco duży, aby pokryć zapotrzebowanie punkt końcowy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a21a3-184">The application port range should be large enough to cover the endpoint requirement of your applications.</span></span> <span data-ttu-id="a21a3-185">Ten zakres powinien być wyłączne z dynamicznego zakresu portów na komputerze, tj. *ephemeralPorts* zakresu zgodnie z ustawieniami w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a21a3-185">This range should be exclusive from the dynamic port range on the machine, i.e. the *ephemeralPorts* range as set in the configuration.</span></span>  <span data-ttu-id="a21a3-186">Usługa sieci szkieletowej będą one używane przy każdym nowe porty są wymagane, a także zajmie się otwarcie tych portów zapory.</span><span class="sxs-lookup"><span data-stu-id="a21a3-186">Service Fabric will use these whenever new ports are required, as well as take care of opening the firewall for these ports.</span></span> 
* <span data-ttu-id="a21a3-187">*reverseProxyEndpointPort* jest punktem końcowym opcjonalne zwrotnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="a21a3-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="a21a3-188">Zobacz [serwera Proxy usługi sieci szkieletowej wstecznego](service-fabric-reverseproxy.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="a21a3-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="a21a3-189">Ustawienia dziennika</span><span class="sxs-lookup"><span data-stu-id="a21a3-189">Log Settings</span></span>
<span data-ttu-id="a21a3-190">**FabricSettings** sekcji pozwala ustawić katalogów głównych dla dzienników i danych sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="a21a3-190">The **fabricSettings** section allows you to set the root directories for the Service Fabric data and logs.</span></span> <span data-ttu-id="a21a3-191">Można dostosować te tylko podczas tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="a21a3-191">You can customize these only during the initial cluster creation.</span></span> <span data-ttu-id="a21a3-192">Poniżej znajduje się fragment próbki w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a21a3-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="a21a3-193">Firma Microsoft zaleca użycie dysku z systemem innym niż system operacyjny jako zmiennej FabricDataRoot i lokalizacji FabricLogRoot jako zapewnia niezawodność więcej względem systemu operacyjnego ulegnie awarii.</span><span class="sxs-lookup"><span data-stu-id="a21a3-193">We recommended using a non-OS drive as the FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="a21a3-194">Należy pamiętać, że jeśli możesz dostosować tylko główny danych, następnie głównego dziennika zostaną umieszczone jeden poziom w dół w katalogu głównym danych.</span><span class="sxs-lookup"><span data-stu-id="a21a3-194">Note that if you customize only the data root, then the log root will be placed one level below the data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="a21a3-195">Ustawienia usługi stanowej niezawodnej</span><span class="sxs-lookup"><span data-stu-id="a21a3-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="a21a3-196">**KtlLogger** sekcja umożliwia ustawienie globalne ustawienia konfiguracji dla usług niezawodne.</span><span class="sxs-lookup"><span data-stu-id="a21a3-196">The **KtlLogger** section allows you to set the global configuration settings for Reliable Services.</span></span> <span data-ttu-id="a21a3-197">Aby uzyskać więcej informacji na temat tych ustawień do odczytu [skonfigurować niezawodne usługi stanowej](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="a21a3-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="a21a3-198">W poniższym przykładzie pokazano, jak zmienić dziennika transakcji udostępnionego, który jest tworzony kopii wszystkie kolekcje niezawodnych usług stanowych.</span><span class="sxs-lookup"><span data-stu-id="a21a3-198">The example below shows how to change the the shared transaction log that gets created to back any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="a21a3-199">Dodatkowe funkcje</span><span class="sxs-lookup"><span data-stu-id="a21a3-199">Add-on features</span></span>
<span data-ttu-id="a21a3-200">Aby skonfigurować dodatkowe funkcje, apiVersion powinien być skonfigurowany jako "04-2017' lub nowszej, a addonFeatures należy skonfigurować:</span><span class="sxs-lookup"><span data-stu-id="a21a3-200">To configure add-on features, the apiVersion should be configured as '04-2017' or higher, and addonFeatures needs to be configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="a21a3-201">Obsługa kontenerów</span><span class="sxs-lookup"><span data-stu-id="a21a3-201">Container support</span></span>
<span data-ttu-id="a21a3-202">Aby włączyć obsługę kontenera systemu windows server kontenera i kontener autonomicznych klastrów funkcji hyper-v, funkcja dodatku "DnsService" musi być włączona.</span><span class="sxs-lookup"><span data-stu-id="a21a3-202">To enable container support for both windows server container and hyper-v container for standalone clusters, the 'DnsService' add-on feature needs to be enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a21a3-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a21a3-203">Next steps</span></span>
<span data-ttu-id="a21a3-204">Po utworzeniu pełny plik pliku ClusterConfig.JSON skonfigurowane zgodnie z autonomicznego Instalatora klastra, wykonując tego artykułu można wdrożyć klastra [tworzenia klastra usługi sieć szkieletowa autonomiczny](service-fabric-cluster-creation-for-windows-server.md) , a następnie przejdź do [ Wizualizowanie klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a21a3-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following the article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed to [visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

