---
title: aaaPowerShell skryptu toodeploy klastra HPC systemu Linux | Dokumentacja firmy Microsoft
description: "Uruchom toodeploy skryptu środowiska PowerShell klastra Linux HPC Pack 2012 R2 w maszynach wirtualnych platformy Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 73041960-58d3-4ecf-9540-d7e1a612c467
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 885b03fa2fd604827dc388803fc21debab730979
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-high-performance-computing-hpc-cluster-with-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="eb9be-103">Tworzenie klastra wysokiej wydajności (HPC) systemu Linux przy użyciu skryptu wdrażania hello HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="eb9be-103">Create a Linux high-performance computing (HPC) cluster with hello HPC Pack IaaS deployment script</span></span>
<span data-ttu-id="eb9be-104">Uruchom hello HPC Pack IaaS wdrożenia programu PowerShell skryptu toodeploy całego klastra HPC Pack 2012 R2 dla systemu Linux obciążeń na maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="eb9be-104">Run hello HPC Pack IaaS deployment PowerShell script toodeploy a complete HPC Pack 2012 R2 cluster for Linux workloads in Azure virtual machines.</span></span> <span data-ttu-id="eb9be-105">Witaj klaster składa się z węzłem głównym przyłączonych do usługi Active Directory systemem Windows Server i Microsoft HPC Pack i węzły obliczeniowe, które Uruchom jedno z hello dystrybucje systemu Linux obsługiwane przez HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="eb9be-105">hello cluster consists of an Active Directory-joined head node running Windows Server and Microsoft HPC Pack, and compute nodes that run one of hello Linux distributions supported by HPC Pack.</span></span> <span data-ttu-id="eb9be-106">Jeśli chcesz toodeploy klastra HPC Pack w obciążeń Azure dla systemu Windows, zobacz [utworzyć klaster HPC systemu Windows hello skrypt wdrożenia HPC Pack IaaS](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eb9be-106">If you want toodeploy an HPC Pack cluster in Azure for Windows workloads, see [Create a Windows HPC cluster with hello HPC Pack IaaS deployment script](../../windows/classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="eb9be-107">Można również użyć toodeploy szablonu usługi Azure Resource Manager klastra HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="eb9be-107">You can also use an Azure Resource Manager template toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="eb9be-108">Na przykład zobacz [utworzyć klaster HPC z węzłami obliczeniowymi Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span><span class="sxs-lookup"><span data-stu-id="eb9be-108">For an example, see [Create an HPC cluster with Linux compute nodes](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/).</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="eb9be-109">Witaj skrypt programu PowerShell opisanych w tym artykule jest tworzony klaster Microsoft HPC Pack 2012 R2 na platformie Azure przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="eb9be-109">hello PowerShell script described in this article creates a Microsoft HPC Pack 2012 R2 cluster in Azure using hello classic deployment model.</span></span> <span data-ttu-id="eb9be-110">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="eb9be-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="eb9be-111">Ponadto skryptu hello opisane w tym artykule nie obsługuje HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="eb9be-111">In addition, hello script described in this article does not support HPC Pack 2016.</span></span>

[!INCLUDE [virtual-machines-common-classic-hpcpack-cluster-powershell-script](../../../../includes/virtual-machines-common-classic-hpcpack-cluster-powershell-script.md)]

## <a name="example-configuration-file"></a><span data-ttu-id="eb9be-112">Przykładowy plik konfiguracji</span><span class="sxs-lookup"><span data-stu-id="eb9be-112">Example configuration file</span></span>
<span data-ttu-id="eb9be-113">Witaj następującego pliku konfiguracji tworzy kontroler domeny i lasu domen i wdraża klastra HPC Pack, który ma jednego węzła głównego z lokalnych baz danych i węzły obliczeniowe Linux 10.</span><span class="sxs-lookup"><span data-stu-id="eb9be-113">hello following configuration file creates a domain controller and domain forest and deploys an HPC Pack cluster which has one head node with local databases and 10 Linux compute nodes.</span></span> <span data-ttu-id="eb9be-114">Wszystkie usługi w chmurze hello są tworzone bezpośrednio w lokalizacji Azja Wschodnia hello.</span><span class="sxs-lookup"><span data-stu-id="eb9be-114">All hello cloud services are created directly in hello East Asia location.</span></span> <span data-ttu-id="eb9be-115">Hello Linux węzły obliczeniowe są tworzone w dwóch usług w chmurze i dwóch kont magazynu (to znaczy *MyLnxCN 0001* do *MyLnxCN 0005* w *MyLnxCNService01* i *mylnxstorage01*, i *MyLnxCN 0006* do *MyLnxCN 0010* w *MyLnxCNService02* i *mylnxstorage02* ).</span><span class="sxs-lookup"><span data-stu-id="eb9be-115">hello Linux compute nodes are created in two cloud services and two storage accounts (that is, *MyLnxCN-0001* to *MyLnxCN-0005* in *MyLnxCNService01* and *mylnxstorage01*, and *MyLnxCN-0006* to *MyLnxCN-0010* in *MyLnxCNService02* and *mylnxstorage02*).</span></span> <span data-ttu-id="eb9be-116">węzły obliczeniowe Hello są tworzone na podstawie obrazu OpenLogic CentOS Linux w wersji 7.0.</span><span class="sxs-lookup"><span data-stu-id="eb9be-116">hello compute nodes are created from an OpenLogic CentOS version 7.0 Linux image.</span></span> 

<span data-ttu-id="eb9be-117">Zastąp wartości hello nazwy usługi oraz konta i nazwę subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="eb9be-117">Substitute your own values for your subscription name and hello account and service names.</span></span>

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
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>MyHeadNode</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>ExtraLarge</VMSize>
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>MyLnxCN-%0001%</VMNamePattern>
    <ServiceNamePattern>MyLnxCNService%01%</ServiceNamePattern>
    <MaxNodeCountPerService>5</MaxNodeCountPerService>
    <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
    <VMSize>Medium</VMSize>
    <NodeCount>10</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20150325 </ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```
## <a name="troubleshooting"></a><span data-ttu-id="eb9be-118">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="eb9be-118">Troubleshooting</span></span>
* <span data-ttu-id="eb9be-119">**Błąd "Sieci wirtualnej nie istnieje"**.</span><span class="sxs-lookup"><span data-stu-id="eb9be-119">**“VNet doesn’t exist” error**.</span></span> <span data-ttu-id="eb9be-120">Po uruchomieniu hello HPC Pack IaaS wdrożenia skryptu toodeploy wielu klastrów na platformie Azure jednocześnie w ramach jednej subskrypcji, co najmniej jednego wdrożenia może działać z powodu błędu hello "sieci wirtualnej *sieci wirtualnej\_nazwa* nie istnieje".</span><span class="sxs-lookup"><span data-stu-id="eb9be-120">If you run hello HPC Pack IaaS deployment script toodeploy multiple clusters in Azure concurrently under one subscription, one or more deployments may fail with hello error “VNet *VNet\_Name* doesn't exist”.</span></span>
  <span data-ttu-id="eb9be-121">Jeśli ten błąd występuje, uruchom ponownie skrypt hello wdrożenia hello nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="eb9be-121">If this error occurs, rerun hello script for hello failed deployment.</span></span>
* <span data-ttu-id="eb9be-122">**Problem podczas uzyskiwania dostępu do hello Internet z hello sieci wirtualnej platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="eb9be-122">**Problem accessing hello Internet from hello Azure virtual network**.</span></span> <span data-ttu-id="eb9be-123">Jeśli utworzysz klaster HPC Pack z nowego kontrolera domeny za pomocą skryptu wdrażania hello lub ręczne podwyższenie węzła głównego kontrolera toodomain maszyny Wirtualnej, mogą wystąpić problemy z połączeniem maszyn wirtualnych hello w toohello sieci wirtualnej platformy Azure hello Internet.</span><span class="sxs-lookup"><span data-stu-id="eb9be-123">If you create an HPC Pack cluster with a new domain controller by using hello deployment script, or you manually promote a head node VM toodomain controller, you may experience problems connecting hello VMs in hello Azure virtual network toohello Internet.</span></span> <span data-ttu-id="eb9be-124">Może to występować, jeśli usługa przesyłania dalej serwera DNS jest automatycznie konfigurowane na kontrolerze domeny hello, a usługi przesyłania dalej serwera DNS nie jest rozpoznawane poprawnie.</span><span class="sxs-lookup"><span data-stu-id="eb9be-124">This can occur if a forwarder DNS server is automatically configured on hello domain controller, and this forwarder DNS server doesn’t resolve properly.</span></span>
  
    <span data-ttu-id="eb9be-125">toowork rozwiązać ten problem, zaloguj się na kontrolerze domeny toohello i ustawienia konfiguracji usługi przesyłania dalej albo usuń hello lub skonfiguruj prawidłową usługę przesyłania dalej serwera DNS.</span><span class="sxs-lookup"><span data-stu-id="eb9be-125">toowork around this problem, log on toohello domain controller and either remove hello forwarder configuration setting or configure a valid forwarder DNS server.</span></span> <span data-ttu-id="eb9be-126">toodo, w Menedżerze serwera kliknij **narzędzia** > **DNS** tooopen Menedżera DNS, a następnie kliknij dwukrotnie **usług przesyłania dalej**.</span><span class="sxs-lookup"><span data-stu-id="eb9be-126">toodo this, in Server Manager click **Tools** > **DNS** tooopen DNS Manager, and then double-click **Forwarders**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb9be-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb9be-127">Next steps</span></span>
* <span data-ttu-id="eb9be-128">Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) uzyskać informacji o obsługiwanych dystrybucjach systemu Linux, przenoszenia danych i przesyłanie zadań tooan HPC Pack klastra z systemem Linux węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="eb9be-128">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for information about supported Linux distributions, moving data, and submitting jobs tooan HPC Pack cluster with Linux compute nodes.</span></span>
* <span data-ttu-id="eb9be-129">Samouczki hello skryptu toocreate klastra i uruchom obciążenia HPC systemu Linux zobacz:</span><span class="sxs-lookup"><span data-stu-id="eb9be-129">For tutorials that use hello script toocreate a cluster and run a Linux HPC workload, see:</span></span>
  * [<span data-ttu-id="eb9be-130">Uruchamianie NAMD z pakietem Microsoft HPC w węzłach obliczeń systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="eb9be-130">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
  * [<span data-ttu-id="eb9be-131">Uruchamianie OpenFOAM z pakietem Microsoft HPC w węzłach obliczeń systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="eb9be-131">Run OpenFOAM with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-openfoam.md)
  * [<span data-ttu-id="eb9be-132">Uruchomienie GWIAZDĘ — CCM + z pakietem Microsoft HPC w systemie Linux obliczeniowe węzłów na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="eb9be-132">Run STAR-CCM+ with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-starccm.md)

