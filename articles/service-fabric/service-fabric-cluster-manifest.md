---
title: "aaaConfigure autonomicznej klastra sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure z autonomicznej lub prywatnej klastra sieci szkieletowej usług."
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
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="e8fe2-103">Ustawienia konfiguracji dla autonomicznych klastra systemu Windows</span><span class="sxs-lookup"><span data-stu-id="e8fe2-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="e8fe2-104">W tym artykule opisano, jak hello tooconfigure using klastra usługi sieć szkieletowa autonomiczny ***pliku ClusterConfig.JSON*** pliku.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="e8fe2-105">Możesz użyć tych informacji toospecify plików takich jak hello węzłów sieci szkieletowej usług i ich adresy IP, różne typy węzłów w hello klastra, hello konfiguracji zabezpieczeń, a także topologii sieci hello pod względem błędów/uaktualnienia domen, dla Twojej autonomicznej klaster.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="e8fe2-106">Gdy możesz [Pobierz hello wersjach usługi sieć szkieletowa](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), kilka przykładów hello pliku ClusterConfig.JSON pliku są pobierane tooyour pracy maszyny.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="e8fe2-107">Witaj próbki o *DevCluster* w nazwach pomoże utworzyć klaster z wszystkie trzy węzły na hello komputera takie same, jak logicznej węzłów.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="e8fe2-108">Poza tym przypadku co najmniej jeden węzeł może być oznaczona jako węzła podstawowego.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="e8fe2-109">Ten klaster jest przydatne w środowisku projektowania lub testowym i nie jest obsługiwany jako klastra produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="e8fe2-110">Witaj próbki o *MultiMachine* w nazwach, pomoże utworzyć klaster jakości produkcyjnych z każdego węzła na osobnym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="e8fe2-111">*ClusterConfig.Unsecure.DevCluster.JSON* i *ClusterConfig.Unsecure.MultiMachine.JSON* Pokaż jak toocreate niezabezpieczona testu lub produkcji klastra odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="e8fe2-112">*ClusterConfig.Windows.DevCluster.JSON* i *ClusterConfig.Windows.MultiMachine.JSON* Pokaż jak toocreate testowym lub produkcyjnym klastra zabezpieczone za pomocą [zabezpieczenia systemu Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="e8fe2-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="e8fe2-113">*ClusterConfig.X509.DevCluster.JSON* i *ClusterConfig.X509.MultiMachine.JSON* Pokaż jak toocreate testowym lub produkcyjnym klastra zabezpieczone za pomocą [X509 zabezpieczeń oparte na certyfikatach](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="e8fe2-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="e8fe2-114">Teraz zostanie hello różnych części ***pliku ClusterConfig.JSON*** plików zgodnie z poniższymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="e8fe2-115">Konfiguracje klastrów ogólne</span><span class="sxs-lookup"><span data-stu-id="e8fe2-115">General cluster configurations</span></span>
<span data-ttu-id="e8fe2-116">Obejmuje to hello szerokie klastra określonej konfiguracji, jak pokazano w poniższy fragment hello JSON.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="e8fe2-117">Można nadać dowolnego klastra usługi sieć szkieletowa tooyour przyjaznej nazwy, przypisując toohello **nazwa** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="e8fe2-118">Witaj **clusterConfigurationVersion** jest numer wersji hello klastra; należy zwiększyć jego każdorazowego uaktualnienia klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="e8fe2-119">Jednak należy pozostawić hello **apiVersion** toohello wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="e8fe2-120">Węzły w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="e8fe2-120">Nodes on hello cluster</span></span>
<span data-ttu-id="e8fe2-121">Można skonfigurować hello węzłów w klastrze usługi sieć szkieletowa usług za pomocą hello **węzłów** sekcji jako powitania po fragment kodu przedstawia.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

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

<span data-ttu-id="e8fe2-122">Klaster sieci szkieletowej usług musi zawierać co najmniej 3 węzłach.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="e8fe2-123">Możesz dodać więcej węzłów toothis sekcji zgodnie z konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="e8fe2-124">Witaj w poniższej tabeli opisano hello ustawienia konfiguracji dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="e8fe2-125">**Konfiguracja węzła**</span><span class="sxs-lookup"><span data-stu-id="e8fe2-125">**Node configuration**</span></span> | <span data-ttu-id="e8fe2-126">**Opis**</span><span class="sxs-lookup"><span data-stu-id="e8fe2-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="e8fe2-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="e8fe2-127">nodeName</span></span> |<span data-ttu-id="e8fe2-128">Aby zapewnić dowolnego węzła toohello przyjazną nazwę.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="e8fe2-129">Adres IP</span><span class="sxs-lookup"><span data-stu-id="e8fe2-129">iPAddress</span></span> |<span data-ttu-id="e8fe2-130">Sprawdzić hello adres IP węzła, otwierając okno polecenia i wpisując `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="e8fe2-131">Zanotuj adres hello IPV4 i przypisać je toohello **iPAddress** zmiennej.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="e8fe2-132">wartość nodetyperef równą</span><span class="sxs-lookup"><span data-stu-id="e8fe2-132">nodeTypeRef</span></span> |<span data-ttu-id="e8fe2-133">Każdy węzeł można przypisać typu innego węzła.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="e8fe2-134">Witaj [typy węzłów](#nodetypes) są zdefiniowane w poniższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="e8fe2-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="e8fe2-135">faultDomain</span></span> |<span data-ttu-id="e8fe2-136">Błąd domen Włącz klastra Administratorzy toodefine hello węzłów fizycznych, które może zakończyć się niepowodzeniem na powitania takie same czasu powodu tooshared fizycznych zależności.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="e8fe2-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="e8fe2-137">upgradeDomain</span></span> |<span data-ttu-id="e8fe2-138">Domen uaktualnienia opisano zestaw węzłów, które są zamykane dla sieci szkieletowej usług uaktualnia na temat hello sam czas.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="e8fe2-139">Można które toowhich tooassign węzłów domen uaktualnienia, ponieważ nie są ograniczone przez wszystkie fizyczne wymagania.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="e8fe2-140">Właściwości klastra</span><span class="sxs-lookup"><span data-stu-id="e8fe2-140">Cluster properties</span></span>
<span data-ttu-id="e8fe2-141">Witaj **właściwości** sekcji w pliku ClusterConfig.JSON hello jest używany tooconfigure hello klastra w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="e8fe2-142">Niezawodność</span><span class="sxs-lookup"><span data-stu-id="e8fe2-142">Reliability</span></span>
<span data-ttu-id="e8fe2-143">pojęcie Hello **reliabilityLevel** definiuje hello liczby replik lub wystąpień hello usługi sieć szkieletowa systemu usług, które można uruchamiać na powitania głównej węzłów klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="e8fe2-144">Określa hello niezawodności tych usług, a więc hello klastra.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="e8fe2-145">wartość Hello jest obliczeniowa przez hello system w czasie tworzenia i uaktualniania klastra.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="e8fe2-146">Diagnostyka</span><span class="sxs-lookup"><span data-stu-id="e8fe2-146">Diagnostics</span></span>
<span data-ttu-id="e8fe2-147">Witaj **diagnosticsStore** sekcji pozwala tooconfigure parametry tooenable diagnostyki i rozwiązywania problemów z węzła lub awarii klastra, jak pokazano w hello następującego fragmentu.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="e8fe2-148">Witaj **metadanych** znajduje się opis diagnostycznej klastra i można ustawić odpowiednią konfigurację.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="e8fe2-149">Te zmienne pomocy zbierania ETW dzienniki śledzenia, zrzuty awaryjne także liczników wydajności.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="e8fe2-150">Odczyt [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) i [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) dzienniki śledzenia Aby uzyskać więcej informacji dotyczących funkcji ETW.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="e8fe2-151">Wszystkie dzienniki tym [awarii zrzuty](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) i [liczniki wydajności](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) może być ukierunkowanej toohello **connectionString** folderu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="e8fe2-152">Można również użyć *AzureStorage* do przechowywania diagnostyki.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="e8fe2-153">Poniżej znajduje się fragment próbki.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="e8fe2-154">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="e8fe2-154">Security</span></span>
<span data-ttu-id="e8fe2-155">Witaj **zabezpieczeń** sekcja jest niezbędne do bezpiecznego autonomicznej klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="e8fe2-156">powitania po fragment kodu przedstawia części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="e8fe2-157">Witaj **metadanych** opis klastra bezpiecznego a może ustawić odpowiednią konfigurację.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="e8fe2-158">Witaj **ClusterCredentialType** i **ServerCredentialType** ustalić typu hello zabezpieczeń, które wykona klaster hello i hello węzły.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="e8fe2-159">Mogą być ustawione tooeither *X509* zabezpieczeń oparte na certyfikatach lub *Windows* dla zabezpieczeń opartych na usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="e8fe2-160">Witaj rest hello **zabezpieczeń** sekcji będą oparte na typ hello hello zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="e8fe2-161">Odczyt [zabezpieczenia oparte na certyfikaty w klastrze autonomiczny](service-fabric-windows-cluster-x509-security.md) lub [zabezpieczenia systemu Windows w klastrze autonomiczny](service-fabric-windows-cluster-windows-security.md) Aby uzyskać informacje dotyczące sposobu toofill limit hello pozostałej części hello **zabezpieczeń**sekcji.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="e8fe2-162">Typy węzłów</span><span class="sxs-lookup"><span data-stu-id="e8fe2-162">Node Types</span></span>
<span data-ttu-id="e8fe2-163">Witaj **elementów NodeType** sekcja opisuje typ hello hello węzłów, które ma w klastrze.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="e8fe2-164">Należy określić typ co najmniej jeden węzeł klastra, jak pokazano w poniższy fragment hello.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

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

<span data-ttu-id="e8fe2-165">Witaj **nazwa** jest hello przyjazną nazwę dla tego typu określonego węzła.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="e8fe2-166">toocreate węzeł tego typu węzła przypisać jej toohello przyjazną nazwę **wartość nodetyperef równą** zmiennej dla tego węzła, jak wspomniano [powyżej](#clusternodes).</span><span class="sxs-lookup"><span data-stu-id="e8fe2-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="e8fe2-167">Dla każdego typu węzła punkty końcowe połączenia hello, które będą używane.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="e8fe2-168">Można wybrać dowolny inny numer portu na te punkty końcowe połączenia, tak długo, jak nie powodują konfliktów z innymi punktami końcowymi w tym klastrze.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="e8fe2-169">W klastrze z wieloma węzłami, będzie co najmniej jeden węzeł podstawowy (tj. **isPrimary** ustawić także*true*), w zależności od hello [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="e8fe2-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="e8fe2-170">Odczyt [zagadnienia związane z planowaniem pojemności klastra sieci szkieletowej usług](service-fabric-cluster-capacity.md) uzyskać informacji o **elementów NodeType** i **reliabilityLevel**i tooknow co to są podstawowego i hello typy węzłów innych niż podstawowe.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="e8fe2-171">Typy węzłów hello tooconfigure używane punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="e8fe2-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="e8fe2-172">*clientConnectionEndpointPort* hello port jest używany przez powitania klienta tooconnect toohello klastra, używając powitania klienta interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="e8fe2-173">*clusterConnectionEndpointPort* jest port hello jaką węzłów hello komunikują się ze sobą.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="e8fe2-174">*leaseDriverEndpointPort* hello port jest używany przez hello klastra dzierżawy sterownika toofind się, jeśli hello węzły są nadal aktywne.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="e8fe2-175">*serviceConnectionEndpointPort* jest hello port używany przez program hello aplikacje i usługi wdrożone w węźle toocommunicate z klientem usługi sieć szkieletowa hello na dany węzeł.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="e8fe2-176">*httpGatewayEndpointPort* hello port jest używany przez hello Service Fabric Explorer tooconnect toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="e8fe2-177">*ephemeralPorts* zastąpienia hello [dynamiczne porty używane przez system operacyjny hello](https://support.microsoft.com/kb/929851).</span><span class="sxs-lookup"><span data-stu-id="e8fe2-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="e8fe2-178">Sieć szkieletowa usług użyje części tych portów aplikacji i pozostałych hello będą dostępne dla hello systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="e8fe2-179">Zostanie również mapować tego zakresu toohello istniejącego zakresu w hello systemu operacyjnego, więc dla wszystkich celów, można użyć zakresów hello podany w hello przykładowych plików JSON.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="e8fe2-180">Należy toomake się, że hello różnica między początkową hello i porty końcowe hello jest co najmniej 255.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="e8fe2-181">Jeśli różnica jest zbyt niski, ponieważ ten zakres jest współużytkowany z systemu operacyjnego hello może wystąpiły konflikty.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="e8fe2-182">Zobacz zakres portów dynamicznych hello skonfigurowany, uruchamiając `netsh int ipv4 show dynamicport tcp`.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="e8fe2-183">*applicationPorts* hello portów, które będą używane przez aplikacje platformy Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="e8fe2-184">zakres portów aplikacji Hello powinien być wystarczająco duży toocover hello punktu końcowego wymagań aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="e8fe2-185">Ten zakres powinien być wyłączne z zakresu portów dynamicznych hello na powitania maszyny, tzn. hello *ephemeralPorts* zakresem określonym w konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="e8fe2-186">Usługa sieci szkieletowej będą one używane przy każdym nowe porty są wymagane, a także zajmie się otwarcie zapory powitania dla tych portów.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="e8fe2-187">*reverseProxyEndpointPort* jest punktem końcowym opcjonalne zwrotnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="e8fe2-188">Zobacz [serwera Proxy usługi sieci szkieletowej wstecznego](service-fabric-reverseproxy.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="e8fe2-189">Ustawienia dziennika</span><span class="sxs-lookup"><span data-stu-id="e8fe2-189">Log Settings</span></span>
<span data-ttu-id="e8fe2-190">Witaj **fabricSettings** sekcja umożliwia katalogi główne hello tooset hello sieci szkieletowej usług danych i dzienniki.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="e8fe2-191">Można dostosować te tylko podczas tworzenia klastra hello.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="e8fe2-192">Poniżej znajduje się fragment próbki w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="e8fe2-193">Zaleca się przy użyciu dysku z systemem innym niż systemu operacyjnego jako hello zmiennej FabricDataRoot i lokalizacji FabricLogRoot zapewnia niezawodność więcej względem awarii systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="e8fe2-194">Należy pamiętać, że jeśli możesz dostosować tylko hello danych głównych, następnie hello dziennika głównego zostaną umieszczone jeden poziom w dół hello danych głównych.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="e8fe2-195">Ustawienia usługi stanowej niezawodnej</span><span class="sxs-lookup"><span data-stu-id="e8fe2-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="e8fe2-196">Witaj **KtlLogger** sekcja umożliwia tooset hello globalne ustawienia konfiguracji dla usług niezawodne.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="e8fe2-197">Aby uzyskać więcej informacji na temat tych ustawień do odczytu [skonfigurować niezawodne usługi stanowej](service-fabric-reliable-services-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="e8fe2-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="e8fe2-198">w poniższym przykładzie Hello pokazuje, jak dziennika transakcji udostępnionego hello hello toochange, który pobiera utworzone tooback wszystkie kolekcje niezawodnych usług stanowych.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="e8fe2-199">Dodatkowe funkcje</span><span class="sxs-lookup"><span data-stu-id="e8fe2-199">Add-on features</span></span>
<span data-ttu-id="e8fe2-200">tooconfigure dodatkowe funkcje, hello apiVersion powinien być skonfigurowany jako "04-2017' lub nowszej, a addonFeatures musi toobe skonfigurowane:</span><span class="sxs-lookup"><span data-stu-id="e8fe2-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="e8fe2-201">Obsługa kontenerów</span><span class="sxs-lookup"><span data-stu-id="e8fe2-201">Container support</span></span>
<span data-ttu-id="e8fe2-202">tooenable kontenera obsługę systemu windows server kontenera i kontener autonomicznych klastrów funkcji hyper-v, funkcja dodatku "DnsService" hello musi toobe włączone.</span><span class="sxs-lookup"><span data-stu-id="e8fe2-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e8fe2-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8fe2-203">Next steps</span></span>
<span data-ttu-id="e8fe2-204">Po utworzeniu pełny plik pliku ClusterConfig.JSON skonfigurowane zgodnie z autonomicznego Instalatora klastra, można wdrożyć klaster w następującym artykule hello [tworzenia klastra usługi sieć szkieletowa autonomiczny](service-fabric-cluster-creation-for-windows-server.md) , a następnie kontynuować zbyt[wizualizacja klastra za pomocą Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e8fe2-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

