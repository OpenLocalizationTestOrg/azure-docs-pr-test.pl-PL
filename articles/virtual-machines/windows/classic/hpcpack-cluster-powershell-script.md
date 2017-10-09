---
title: klaster HPC systemu Windows toodeploy skrypt aaaPowerShell | Dokumentacja firmy Microsoft
description: "Uruchom toodeploy skryptu środowiska PowerShell klastra systemu Windows HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 286b2be8-2533-40df-b02a-26156b1f1133
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 10ce1e9bc4e98954b955549bd72aaaf6106c69fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="eb2ac-103">Tworzenie klastra wysokiej wydajności (HPC) systemu Windows przy użyciu skryptu wdrażania hello HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="eb2ac-103">Create a Windows high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="eb2ac-104">Uruchom hello HPC Pack IaaS wdrożenia programu PowerShell skryptu toodeploy całego klastra HPC Pack 2012 R2 dla obciążeń systemu Windows na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Windows workloads in Azure virtual machines.</span></span> <span data-ttu-id="eb2ac-105">Witaj klaster składa się z węzłem głównym przyłączonych do usługi Active Directory systemem Windows Server i Microsoft HPC Pack i zasoby, które określisz obliczeniowe dodatkowe okna.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and additional Windows compute resources you specify.</span></span> <span data-ttu-id="eb2ac-106">Jeśli dla obciążeń systemu Linux toodeploy klastra HPC Pack na platformie Azure, zobacz [utworzyć klaster HPC systemu Linux hello skrypt wdrożenia HPC Pack IaaS](../../linux/classic/hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="eb2ac-106">If you want toodeploy an HPC Pack cluster in Azure for Linux workloads, see [Create a Linux HPC cluster with hello HPC Pack IaaS deployment script](../../linux/classic/hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="eb2ac-107">Można również użyć toodeploy szablonu usługi Azure Resource Manager klastra HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="eb2ac-108">Przykłady można znaleźć [utworzyć klaster HPC](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) i [utworzyć klaster HPC z obrazem węzła niestandardowego obliczania](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span><span class="sxs-lookup"><span data-stu-id="eb2ac-108">For examples, see [Create an HPC cluster](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/) and [Create an HPC cluster with a custom compute node image](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-custom-image/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="eb2ac-109">Witaj skrypt programu PowerShell opisanych w tym artykule jest tworzony klaster Microsoft HPC Pack 2012 R2 na platformie Azure przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="eb2ac-110">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="eb2ac-111">Ponadto skryptu hello opisane w tym artykule nie obsługuje HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-files"></a><span data-ttu-id="eb2ac-112">Przykładowe pliki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="eb2ac-112">Example configuration files</span></span>
<span data-ttu-id="eb2ac-113">W hello następujące przykłady, należy zastąpić własne wartości dla Twojego identyfikatora subskrypcji lub nazwy i nazwy usługi oraz konta hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-113">In hello following examples, substitute your own values for your subscription Id or name and hello account and service names.</span></span>

### <a name="example-1"></a><span data-ttu-id="eb2ac-114">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="eb2ac-114">Example 1</span></span>
<span data-ttu-id="eb2ac-115">Witaj następującego pliku konfiguracji wdraża klaster HPC Pack węzła głównego z lokalnych baz danych i systemem operacyjnym Windows Server 2012 R2 hello pięć węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-115">hello following configuration file deploys an HPC Pack cluster that has a head node with local databases and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="eb2ac-116">Wszystkie usługi w chmurze hello są tworzone bezpośrednio w hello lokalizacji zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-116">All hello cloud services are created directly in hello West US location.</span></span> <span data-ttu-id="eb2ac-117">węzła głównego Hello działa jako kontroler domeny w lesie domeny hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-117">hello head node acts as domain controller of hello domain forest.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionId>08701940-C02E-452F-B0B1-39D50119F267</SubscriptionId>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%1000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>5</NodeCount>
    <OSVersion>WindowsServer2012R2</OSVersion>
  </ComputeNodes>
</IaaSClusterConfig>
```

### <a name="example-2"></a><span data-ttu-id="eb2ac-118">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="eb2ac-118">Example 2</span></span>
<span data-ttu-id="eb2ac-119">Witaj następującego pliku konfiguracji wdraża klaster HPC Pack w istniejącym lesie domeny.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-119">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="eb2ac-120">klaster Hello ma 1 węzła głównego z lokalnych baz danych i 12 obliczeniowe węzłów o hello zastosować rozszerzenia BGInfo maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-120">hello cluster has 1 head node with local databases and 12 compute nodes with hello BGInfo VM extension applied.</span></span>
<span data-ttu-id="eb2ac-121">Automatyczne instalowanie aktualizacji systemu Windows jest wyłączona dla wszystkich hello maszyn wirtualnych w lesie domeny hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-121">Automatic installation of Windows updates is disabled for all hello VMs in hello domain forest.</span></span> <span data-ttu-id="eb2ac-122">Wszystkie usługi w chmurze hello są tworzone bezpośrednio w lokalizacji Azja Wschodnia.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-122">All hello cloud services are created directly in the East Asia location.</span></span> <span data-ttu-id="eb2ac-123">węzły obliczeniowe Hello są tworzone trzy usługi w chmurze i kont magazynu trzy: *MyHPCCN 0001* za*MyHPCCN 0005* w *MyHPCCNService01* i  *mycnstorage01*; *MyHPCCN 0006* za*MyHPCCN0010* w *MyHPCCNService02* i *mycnstorage02*; i  *MyHPCCN-0011* za*MyHPCCN 0012* w *MyHPCCNService03* i *mycnstorage03*).</span><span class="sxs-lookup"><span data-stu-id="eb2ac-123">hello compute nodes are created in three cloud services and three storage accounts: *MyHPCCN-0001* too*MyHPCCN-0005* in *MyHPCCNService01* and *mycnstorage01*; *MyHPCCN-0006* too*MyHPCCN0010* in *MyHPCCNService02* and *mycnstorage02*; and *MyHPCCN-0011* too*MyHPCCN-0012* in *MyHPCCNService03* and *mycnstorage03*).</span></span> <span data-ttu-id="eb2ac-124">węzły obliczeniowe Hello są tworzone na podstawie istniejącego obrazu prywatnej przechwytywane z węzła obliczeń.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-124">hello compute nodes are created from an existing private image captured from a compute node.</span></span> <span data-ttu-id="eb2ac-125">Witaj automatycznie zwiększyć lub zmniejszyć włączono usługę z domyślnymi zwiększyć lub zmniejszyć odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-125">hello auto grow and shrink service is enabled with default grow and shrink intervals.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>MyDCServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>Large</VMSize>
      </DomainController>
     <NoWindowsAutoUpdate />
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
  </Certificates>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0001%</VMNamePattern>
<ServiceNamePattern>MyHPCCNService%01%</ServiceNamePattern>
<MaxNodeCountPerService>5</MaxNodeCountPerService>
<StorageAccountNamePattern>mycnstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>12</NodeCount>
    <ImageName HPCPackInstalled=”true”>MyHPCComputeNodeImage</ImageName>
    <VMExtensions>
       <VMExtension>
          <ExtensionName>BGInfo</ExtensionName>
          <Publisher>Microsoft.Compute</Publisher>
          <Version>1.*</Version>
       </VMExtension>
    </VMExtensions>
  </ComputeNodes>
  <AutoGrowShrink>
    <CertificateId>1</CertificateId>
  </AutoGrowShrink>
</IaaSClusterConfig>

```

### <a name="example-3"></a><span data-ttu-id="eb2ac-126">Przykład 3</span><span class="sxs-lookup"><span data-stu-id="eb2ac-126">Example 3</span></span>
<span data-ttu-id="eb2ac-127">Witaj następującego pliku konfiguracji wdraża klaster HPC Pack w istniejącym lesie domeny.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-127">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="eb2ac-128">Witaj klastra zawiera jednego węzła głównego, jeden serwer bazy danych z dysku danych 500 GB, dwa węzły brokera zainstalowano system operacyjny Windows Server 2012 R2 hello oraz systemem operacyjnym Windows Server 2012 R2 hello pięć węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-128">hello cluster contains one head node, one database server with a 500 GB data disk, two broker nodes running hello Windows Server 2012 R2 operating system, and five compute nodes running hello Windows Server 2012 R2 operating system.</span></span> <span data-ttu-id="eb2ac-129">usługi w chmurze MyHPCCNService jest tworzony w grupie koligacji hello Hello *MyIBAffinityGroup*, a hello innych usług w chmurze są tworzone w grupie koligacji hello *MyAffinityGroup*.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-129">hello cloud service MyHPCCNService is created in hello affinity group *MyIBAffinityGroup*, and hello other cloud services are created in hello affinity group *MyAffinityGroup*.</span></span> <span data-ttu-id="eb2ac-130">Witaj HPC interfejsu API REST harmonogramu dla zadania i portalu internetowego HPC są włączone na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-130">hello HPC Job Scheduler REST API and HPC web portal are enabled on hello head node.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>    
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>NewRemoteDB</DBOption>
    <DBVersion>SQLServer2014_Enterprise</DBVersion>
    <DBServer>
      <VMName>MyDBServer</VMName>
      <ServiceName>MyHPCService</ServiceName>
      <VMSize>ExtraLarge</VMSize>
      <DataDiskSizeInGB>500</DataDiskSizeInGB>
    </DBServer>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>MyHPCCN-%0000%</VMNamePattern>
    <ServiceName>MyHPCCNService</ServiceName>
    <VMSize>A8</VMSize>
<NodeCount>5</NodeCount>
<AffinityGroup>MyIBAffinityGroup</AffinityGroup>
  </ComputeNodes>
  <BrokerNodes>
    <VMNamePattern>MyHPCBN-%0000%</VMNamePattern>
    <ServiceName>MyHPCBNService</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>2</NodeCount>
  </BrokerNodes>
</IaaSClusterConfig>
```



### <a name="example-4"></a><span data-ttu-id="eb2ac-131">Przykład 4</span><span class="sxs-lookup"><span data-stu-id="eb2ac-131">Example 4</span></span>
<span data-ttu-id="eb2ac-132">Witaj następującego pliku konfiguracji wdraża klaster HPC Pack w istniejącym lesie domeny.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-132">hello following configuration file deploys an HPC Pack cluster in an existing domain forest.</span></span> <span data-ttu-id="eb2ac-133">klaster Hello ma dwa węzła głównego z lokalnych baz danych, są tworzone dwa szablony Azure węzła i dla szablonu węzła Azure są tworzone trzy węzły Azure średni rozmiar *AzureTemplate1*.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-133">hello cluster has two head node with local databases, two Azure node templates are created, and three size Medium Azure nodes are created for Azure node template *AzureTemplate1*.</span></span> <span data-ttu-id="eb2ac-134">Plik skryptu działa na powitania węzła głównego po skonfigurowaniu hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-134">A script file runs on hello head node after hello head node is configured.</span></span>

```Xml
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
  <AffinityGroup>MyAffinityGroup</AffinityGroup>
  <Location>East Asia</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>ExistingDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
<VMSize>ExtraLarge</VMSize>
    <PostConfigScript>c:\MyHNPostActions.ps1</PostConfigScript>
  </HeadNode>
  <Certificates>
    <Certificate>
      <Id>1</Id>
      <PfxFile>d:\mytestcert1.pfx</PfxFile>
      <Password>MyPsw!!2</Password>
    </Certificate>
    <Certificate>
      <Id>2</Id>
      <PfxFile>d:\mytestcert2.pfx</PfxFile>
    </Certificate>    
  </Certificates>
  <AzureBurst>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate1</TemplateName>
      <SubscriptionId>bb9252ba-831f-4c9d-ae14-9a38e6da8ee4</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc1</ServiceName>
      <StorageAccount>myteststorage1</StorageAccount>
      <NodeCount>3</NodeCount>
      <RoleSize>Medium</RoleSize>
    </AzureNodeTemplate>
    <AzureNodeTemplate>
      <TemplateName>AzureTemplate2</TemplateName>
      <SubscriptionId>ad4b9f9f-05f2-4c74-a83f-f2eb73000e0b</SubscriptionId>
      <CertificateId>1</CertificateId>
      <ServiceName>mytestsvc2</ServiceName>
      <StorageAccount>myteststorage2</StorageAccount>
      <Proxy>
        <UsesStaticProxyCount>false</UsesStaticProxyCount>     
        <ProxyRatio>100</ProxyRatio>
        <ProxyRatioBase>400</ProxyRatioBase>
      </Proxy>
      <OSVersion>WindowsServer2012</OSVersion>
    </AzureNodeTemplate>
  </AzureBurst>
</IaaSClusterConfig>
```

## <a name="troubleshooting"></a><span data-ttu-id="eb2ac-135">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="eb2ac-135">Troubleshooting</span></span>
* <span data-ttu-id="eb2ac-136">**Błąd "Sieci wirtualnej nie istnieje"** — Jeśli uruchomisz toodeploy skryptu hello wielu klastrów na platformie Azure jednocześnie w ramach jednej subskrypcji, co najmniej jednego wdrożenia może działać z powodu błędu hello "sieci wirtualnej *sieci wirtualnej\_nazwa* nie istnieje".</span><span class="sxs-lookup"><span data-stu-id="eb2ac-136">**“VNet doesn’t exist” error** - If you run hello script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="eb2ac-137">Jeśli ten błąd występuje, uruchom skrypt hello ponownie dla wdrożenia hello nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-137">If this error occurs, run hello script again for hello failed deployment.</span></span>
* <span data-ttu-id="eb2ac-138">**Problem podczas uzyskiwania dostępu do hello Internet z hello sieci wirtualnej platformy Azure** — Jeśli utworzyć klaster z nowego kontrolera domeny za pomocą skryptu wdrażania hello, lub ręcznie podwyższyć poziom kontrolera toodomain wirtualna węzła głównego, mogą wystąpić problemy Łączenie hello maszyn wirtualnych toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-138">**Problem accessing hello Internet from hello Azure virtual network** - If you create a cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs toohello Internet.</span></span> <span data-ttu-id="eb2ac-139">Ten problem może wystąpić, jeśli usługa przesyłania dalej serwera DNS jest automatycznie konfigurowane na kontrolerze domeny hello, a usługi przesyłania dalej serwera DNS nie jest rozpoznawane poprawnie.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-139">This problem can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="eb2ac-140">toowork rozwiązać ten problem, zaloguj się na kontrolerze domeny toohello i ustawienia konfiguracji usługi przesyłania dalej albo usuń hello lub skonfiguruj prawidłową usługę przesyłania dalej serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-140">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="eb2ac-141">tooconfigure to ustawienie, w Menedżerze serwera kliknij **narzędzia** >
    **DNS** tooopen Menedżera DNS, a następnie kliknij dwukrotnie **usług przesyłania dalej**.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-141">tooconfigure this setting, in Server Manager click **Tools** >
    **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>
* <span data-ttu-id="eb2ac-142">**Problem z dostępem do sieci RDMA z maszyn wirtualnych obliczeniowych** — Jeśli Dodawanie obliczeń do systemu Windows Server lub węzeł brokera rozmiar maszyn wirtualnych przy użyciu z funkcją RDMA, takich jak A8 i A9, mogą wystąpić problemy z połączeniem tych maszyn wirtualnych toohello RDMA aplikacji sieci.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-142">**Problem accessing RDMA network from compute-intensive VMs** - If you add Windows Server compute or broker node VMs using an RDMA-capable size such as A8 or A9, you may experience problems connecting those VMs toohello RDMA application network.</span></span> <span data-ttu-id="eb2ac-143">Jedną z przyczyn się, że ten problem występuje, to jeśli hello HpcVmDrivers rozszerzenia nie jest zainstalowany prawidłowo po dodaniu klastra toohello hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-143">One reason this problem occurs is if hello HpcVmDrivers extension is not properly installed when hello VMs are added toohello cluster.</span></span> <span data-ttu-id="eb2ac-144">Na przykład rozszerzenie mogła zostać zablokowana na powitania stan instalacji.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-144">For example, the extension might be stuck in hello installing state.</span></span>
  
    <span data-ttu-id="eb2ac-145">toowork rozwiązać ten problem, pierwszy stan rozszerzenia hello na maszynach wirtualnych hello hello wyboru.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-145">toowork around this problem, first check hello state of hello extension in hello VMs.</span></span> <span data-ttu-id="eb2ac-146">Jeśli nie zainstalowano poprawnie rozszerzenia hello, spróbuj usunąć hello węzłów z klastra HPC hello, a następnie ponownie Dodaj hello węzłów.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-146">If hello extension is not properly installed, try removing hello nodes from hello HPC cluster and then add hello nodes again.</span></span> <span data-ttu-id="eb2ac-147">Na przykład można dodać węzła obliczeniowego maszyn wirtualnych, uruchamiając skrypt HpcIaaSNode.ps1 Dodaj hello na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-147">For example, you can add compute node VMs by running hello Add-HpcIaaSNode.ps1 script on hello head node.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb2ac-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb2ac-148">Next steps</span></span>
* <span data-ttu-id="eb2ac-149">Spróbuj uruchomić test obciążenia w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-149">Try running a test workload on hello cluster.</span></span> <span data-ttu-id="eb2ac-150">Na przykład zobacz hello HPC Pack [Wprowadzenie — przewodnik](https://technet.microsoft.com/library/jj884144).</span><span class="sxs-lookup"><span data-stu-id="eb2ac-150">For an example, see hello HPC Pack [getting started guide](https://technet.microsoft.com/library/jj884144).</span></span>
* <span data-ttu-id="eb2ac-151">Dla hello samouczek tooscript wdrażanie klastra i uruchom obciążenia HPC, zobacz [wprowadzenie do klastra HPC Pack w obciążeń programu Excel i SOA Azure toorun](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb2ac-151">For a tutorial tooscript hello cluster deployment and run an HPC workload, see [Get started with an HPC Pack cluster in Azure toorun Excel and SOA workloads](../../virtual-machines-windows-excel-cluster-hpcpack.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="eb2ac-152">Spróbuj toostart narzędzia HPC Pack, Zatrzymaj, Dodaj i usuń węzły obliczeniowe z klastra, którą utworzysz.</span><span class="sxs-lookup"><span data-stu-id="eb2ac-152">Try HPC Pack's tools toostart, stop, add, and remove compute nodes from a cluster you create.</span></span> <span data-ttu-id="eb2ac-153">Zobacz [Zarządzaj węzłów obliczeniowych w HPC Pack klastra w systemie Azure](hpcpack-cluster-node-manage.md).</span><span class="sxs-lookup"><span data-stu-id="eb2ac-153">See [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md).</span></span>
* <span data-ttu-id="eb2ac-154">tooget Konfigurowanie klastra toohello zadania toosubmit z komputera lokalnego, zobacz [klastra HPC przesyłania zadań na lokalnym komputerze tooan HPC Pack na platformie Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb2ac-154">tooget set up toosubmit jobs toohello cluster from a local computer, see [Submit HPC jobs from an on-premises computer tooan HPC Pack cluster in Azure](../../virtual-machines-windows-hpcpack-cluster-submit-jobs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

