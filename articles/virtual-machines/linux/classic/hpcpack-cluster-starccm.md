---
title: "aaaRun GWIAZDKĘ — CCM + pakietem HPC na maszynach wirtualnych systemu Linux | Dokumentacja firmy Microsoft"
description: "Wdrażanie klastra Microsoft HPC Pack na platformie Azure i uruchomienie GWIAZDĘ — CCM + zadania w systemie Linux w wielu węzłach obliczeniowych przez sieć RDMA."
services: virtual-machines-linux
documentationcenter: 
author: xpillons
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 75523406-d268-4623-ac3e-811c7b74de4b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 09/13/2016
ms.author: xpillons
ms.openlocfilehash: 8265013cb295f53d6d4354ab2f100ef20d9f4c8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="dfdaf-103">Uruchomienie GWIAZDĘ — CCM + z pakietem Microsoft HPC na Linux RDMA klaster na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="dfdaf-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="dfdaf-104">W tym artykule opisano, jak toodeploy Microsoft HPC Pack klastra na platformie Azure i uruchom [GWIAZDKĘ CD adapco-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) zadania na wielu węzłach obliczeniowych Linux, które są wzajemnie InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-104">This article shows you how toodeploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="dfdaf-105">Microsoft HPC Pack udostępnia funkcje toorun różnych HPC na dużą skalę i równoległych aplikacji, w tym aplikacji MPI w klastrach maszyny wirtualne Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-105">Microsoft HPC Pack provides features toorun a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="dfdaf-106">HPC Pack również umożliwia uruchamianie aplikacji HPC systemu Linux na węźle obliczeń maszyn wirtualnych systemu Linux, które zostały wdrożone w klastrze HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="dfdaf-107">Aby toousing wprowadzenie Linux obliczeniowe węzłów z pakietem HPC, zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-107">For an introduction toousing Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="dfdaf-108">Konfigurowanie klastra HPC Pack</span><span class="sxs-lookup"><span data-stu-id="dfdaf-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="dfdaf-109">Pobierz skrypty wdrażania HPC Pack IaaS hello z hello [Centrum pobierania](https://www.microsoft.com/en-us/download/details.aspx?id=44949) i wyodrębnić je lokalnie.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-109">Download hello HPC Pack IaaS deployment scripts from hello [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="dfdaf-110">Program Azure PowerShell jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="dfdaf-111">Jeśli nie skonfigurowano programu PowerShell na komputerze lokalnym, przeczytaj artykuł hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-111">If PowerShell is not configured on your local machine, please read hello article [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="dfdaf-112">W chwili hello pisania tego dokumentu hello Linux obrazów z hello Azure Marketplace, (zawierający sterowniki InfiniBand hello Azure) są SLES 12, CentOS 6.5 i CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-112">At hello time of this writing, hello Linux images from hello Azure Marketplace (which contains hello InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="dfdaf-113">W tym artykule jest oparta na użycie hello SLES 12.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-113">This article is based on hello usage of SLES 12.</span></span> <span data-ttu-id="dfdaf-114">Nazwa hello tooretrieve wszystkie obrazy systemu Linux obsługujących HPC w hello Marketplace, możesz uruchomić hello następującego polecenia programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-114">tooretrieve hello name of all Linux images that support HPC in hello Marketplace, you can run hello following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="dfdaf-115">dane wyjściowe Hello wymieniono hello lokalizacji, w którym te obrazy są dostępne i hello nazwa obrazu (**Nazwa_obrazu**) toobe używany w szablonie wdrożenia hello później.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-115">hello output lists hello location in which these images are available and hello image name (**ImageName**) toobe used in hello deployment template later.</span></span>

<span data-ttu-id="dfdaf-116">Przed wdrożeniem klastra hello masz toobuild pliku HPC Pack wdrażania szablonu.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-116">Before you deploy hello cluster, you have toobuild an HPC Pack deployment template file.</span></span> <span data-ttu-id="dfdaf-117">Ponieważ firma Microsoft docelowych małych klastra, węzłem głównym hello zostanie hello kontrolera domeny i hosta lokalnego bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-117">Because we're targeting a small cluster, hello head node will be hello domain controller and host a local SQL database.</span></span>

<span data-ttu-id="dfdaf-118">Witaj następujący szablon będzie wdrażanie węzła głównego, Utwórz plik XML o nazwie **MyCluster.xml**i Zastąp wartości hello **SubscriptionId**, **StorageAccount**,  **Lokalizacja**, **VMName**, i **ServiceName** z Twoimi zmianami.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-118">hello following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace hello values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <IaaSClusterConfig>
      <Subscription>
        <SubscriptionId>99999999-9999-9999-9999-999999999999</SubscriptionId>
        <StorageAccount>mystorageaccount</StorageAccount>
      </Subscription>
      <Location>North Europe</Location>
      <VNet>
        <VNetName>hpcvnetne</VNetName>
        <SubnetName>subnet-hpc</SubnetName>
      </VNet>
      <Domain>
        <DCOption>HeadNodeAsDC</DCOption>
        <DomainFQDN>hpc.local</DomainFQDN>
      </Domain>
      <Database>
        <DBOption>LocalDB</DBOption>
      </Database>
      <HeadNode>
        <VMName>myhpchn</VMName>
        <ServiceName>myhpchn</ServiceName>
        <VMSize>Standard_D4</VMSize>
      </HeadNode>
      <LinuxComputeNodes>
        <VMNamePattern>lnxcn-%0001%</VMNamePattern>
        <ServiceNamePattern>mylnxcn%01%</ServiceNamePattern>
        <MaxNodeCountPerService>20</MaxNodeCountPerService>
        <StorageAccountNamePattern>mylnxstorage%01%</StorageAccountNamePattern>
        <VMSize>A9</VMSize>
        <NodeCount>0</NodeCount>
        <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
      </LinuxComputeNodes>
    </IaaSClusterConfig>

<span data-ttu-id="dfdaf-119">Rozpocznij tworzenie węzłem head hello uruchamiając hello polecenia programu PowerShell z wiersza polecenia o podniesionych uprawnieniach:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-119">Start hello head-node creation by running hello PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="dfdaf-120">Po upływie 20 minut too30 węzłem głównym hello powinno być gotowe.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-120">After 20 too30 minutes, hello head node should be ready.</span></span> <span data-ttu-id="dfdaf-121">Możesz połączyć tooit z hello portalu Azure, klikając hello **Connect** ikona hello maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-121">You can connect tooit from hello Azure portal by clicking hello **Connect** icon of hello virtual machine.</span></span>

<span data-ttu-id="dfdaf-122">Po pewnym czasie może być toofix hello DNS usługa przesyłania dalej.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-122">You might eventually have toofix hello DNS forwarder.</span></span> <span data-ttu-id="dfdaf-123">toodo tak, uruchom Menedżera DNS.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-123">toodo so, start DNS Manager.</span></span>

1. <span data-ttu-id="dfdaf-124">Nazwa serwera powitania kliknij prawym przyciskiem myszy w Menedżerze DNS, wybierz **właściwości**, a następnie kliknij przycisk hello **usług przesyłania dalej** kartę.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-124">Right-click hello server name in DNS Manager, select **Properties**, and then click hello **Forwarders** tab.</span></span>
2. <span data-ttu-id="dfdaf-125">Kliknij przycisk hello **Edytuj** przycisk tooremove żadnych usług przesyłania dalej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-125">Click hello **Edit** button tooremove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="dfdaf-126">Upewnij się, że hello **Użyj wskazówek dotyczących serwerów głównych, jeśli są dostępne nie usług przesyłania dalej** pole wyboru jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-126">Make sure that hello **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="dfdaf-127">Konfigurowanie węzłów obliczeniowych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="dfdaf-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="dfdaf-128">Możesz wdrożyć węzły obliczeniowe hello systemu Linux przy użyciu hello tego samego szablonu wdrożenia użytą węzła głównego hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-128">You deploy hello Linux compute nodes by using hello same deployment template that you used toocreate hello head node.</span></span>

<span data-ttu-id="dfdaf-129">Kopiuj plik hello **MyCluster.xml** z węzłem głównym toohello komputera lokalnego, a aktualizacja hello **NodeCount** oznaczanie numerami hello węzłów, które mają toodeploy (< = 20).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-129">Copy hello file **MyCluster.xml** from your local machine toohello head node, and update hello **NodeCount** tag with hello number of nodes that you want toodeploy (<=20).</span></span> <span data-ttu-id="dfdaf-130">Można dokładne toohave za mało dostępnych rdzeni limitu Azure, ponieważ każde wystąpienie A9 będą korzystać z 16 rdzeni w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-130">Be careful toohave enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="dfdaf-131">Można użyć wystąpienia A8 (8 rdzeni) zamiast A9, jeśli chcesz toouse więcej maszyn wirtualnych w hello samego budżetu.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-131">You can use A8 instances (8 cores) instead of A9 if you want toouse more VMs in hello same budget.</span></span>

<span data-ttu-id="dfdaf-132">W węźle głównym hello skopiuj skryptów wdrażania hello HPC Pack IaaS.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-132">On hello head node, copy hello HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="dfdaf-133">Uruchom następujące polecenia programu PowerShell systemu Azure w wiersza polecenia o podniesionych uprawnieniach hello:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-133">Run hello following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="dfdaf-134">Uruchom **Add-AzureAccount** tooyour tooconnect subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-134">Run **Add-AzureAccount** tooconnect tooyour Azure subscription.</span></span>
2. <span data-ttu-id="dfdaf-135">Jeśli masz wiele subskrypcji, uruchom **Get-AzureSubscription** toolist je.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-135">If you have multiple subscriptions, run **Get-AzureSubscription** toolist them.</span></span>
3. <span data-ttu-id="dfdaf-136">Wartość domyślna subskrypcja, uruchamiając hello **xxxx wybierz AzureSubscription — Nazwa subskrypcji — domyślna** polecenia.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-136">Set a default subscription by running hello **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="dfdaf-137">Uruchom **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** toostart wdrażania węzłów obliczeniowych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** toostart deploying Linux compute nodes.</span></span>
   
   ![Wdrażanie węzła HEAD w akcji][hndeploy]

<span data-ttu-id="dfdaf-139">Otwórz narzędzie Menedżer klastra HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-139">Open hello HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="dfdaf-140">Po kilku minutach węzły obliczeniowe Linux regularnie pojawi się lista węzły klastra obliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="dfdaf-141">W trybie klasycznym wdrożenia hello maszyn wirtualnych IaaS są tworzone po kolei.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-141">With hello classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="dfdaf-142">Tak hello liczba węzłów jest ważne, pobieranie wszystkie wdrożone może zająć dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-142">So if hello number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Linux węzłów w Menedżerze klastra HPC Pack][clustermanager]

<span data-ttu-id="dfdaf-144">Teraz, wszystkie węzły są gotowe do działania w klastrze hello, istnieją toomake ustawień dodatkowej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-144">Now that all nodes are up and running in hello cluster, there are additional infrastructure settings toomake.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="dfdaf-145">Konfigurowanie udziału plików platformy Azure dla systemu Windows i Linux węzłów</span><span class="sxs-lookup"><span data-stu-id="dfdaf-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="dfdaf-146">Można użyć skryptów toostore usługi plików Azure hello, pakiety aplikacji i plików danych.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-146">You can use hello Azure File service toostore scripts, application packages, and data files.</span></span> <span data-ttu-id="dfdaf-147">Plików na platformę Azure zapewnia możliwości CIFS u góry magazynu obiektów Blob platformy Azure jako magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="dfdaf-148">Należy pamiętać, że nie jest to najbardziej skalowalne rozwiązanie hello, ale jest hello jeden najprostszym i nie wymaga dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-148">Be aware that this is not hello most scalable solution, but it is hello simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="dfdaf-149">Tworzenie udziału plików Azure, wykonując następujące instrukcje hello w artykule hello [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-149">Create an Azure File share by following hello instructions in hello article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="dfdaf-150">Zachowaj hello nazwę konta magazynu jako **saname**, nazwa udziału plików hello jako **sharename**i klucz konta magazynu hello jako **sakey**.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-150">Keep hello name of your storage account as **saname**, hello file share name as **sharename**, and hello storage account key as **sakey**.</span></span>

### <a name="mount-hello-azure-file-share-on-hello-head-node"></a><span data-ttu-id="dfdaf-151">Instalowanie udziału plików Azure hello na powitania węzła głównego</span><span class="sxs-lookup"><span data-stu-id="dfdaf-151">Mount hello Azure File share on hello head node</span></span>
<span data-ttu-id="dfdaf-152">Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie toostore hello poświadczeń w magazynie komputera lokalnego hello hello:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-152">Open an elevated command prompt and run hello following command toostore hello credentials in hello local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="dfdaf-153">Następnie toomount hello Azure udziału plików, uruchom:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-153">Then, toomount hello Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-hello-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="dfdaf-154">Instalowanie udziału plików Azure hello na węzły obliczeniowe systemu Linux</span><span class="sxs-lookup"><span data-stu-id="dfdaf-154">Mount hello Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="dfdaf-155">Jeden przydatne narzędzie dołączoną HPC Pack to narzędzie clusrun hello.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-155">One useful tool that comes with HPC Pack is hello clusrun tool.</span></span> <span data-ttu-id="dfdaf-156">To narzędzie wiersza polecenia toorun hello, same polecenia można użyć jednocześnie na zestaw węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-156">You can use this command-line tool toorun hello same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="dfdaf-157">W tym przypadku został użyty udział plików Azure hello toomount i utrwalić go toosurvive jest uruchamiany ponownie.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-157">In our case, it's used toomount hello Azure File share and persist it toosurvive reboots.</span></span>
<span data-ttu-id="dfdaf-158">W podniesionego wiersza poleceń na powitania węzła głównego uruchom następujące polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-158">In an elevated command prompt on hello head node, run hello following commands.</span></span>

<span data-ttu-id="dfdaf-159">katalog instalacji hello toocreate:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-159">toocreate hello mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="dfdaf-160">Witaj toomount udziału plików platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-160">toomount hello Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="dfdaf-161">toopersist hello instalacji udziału:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-161">toopersist hello mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="dfdaf-162">Zainstaluj GWIAZDKĘ — CCM +</span><span class="sxs-lookup"><span data-stu-id="dfdaf-162">Install STAR-CCM+</span></span>
<span data-ttu-id="dfdaf-163">Azure wystąpień maszyna wirtualna A8 i A9 świadczenie obsługi InfiniBand i funkcji RDMA.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="dfdaf-164">Hello jądra sterowniki, które włączają te funkcje są dostępne dla systemu Windows Server 2012 R2, SUSE 12 CentOS 6.5 i CentOS 7.1 obrazów w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-164">hello kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in hello Azure Marketplace.</span></span> <span data-ttu-id="dfdaf-165">Microsoft MPI i MPI firmy Intel (wersji 5.x) są Witaj dwie MPI bibliotek, które obsługują te sterowniki na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-165">Microsoft MPI and Intel MPI (release 5.x) are hello two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="dfdaf-166">GWIAZDKĘ CD adapco — CCM + wersji 11.x i później jest powiązane z wersją Intel MPI 5.x, więc InfiniBand obsługę Azure jest dołączony.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="dfdaf-167">Pobierz hello Linux64 GWIAZDKĘ — CCM + pakietu z hello [CD adapco portal](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-167">Get hello Linux64 STAR-CCM+ package from hello [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="dfdaf-168">W naszym przykładzie użyliśmy wersji 11.02.010 w mieszanych dokładności.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="dfdaf-169">Na powitania węzła głównego w hello **/hpcdata** plików Azure udostępnić, utworzyć skrypt powłoki o nazwie **setupstarccm.sh** z powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-169">On hello head node, in hello **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with hello following content.</span></span> <span data-ttu-id="dfdaf-170">Ten skrypt będzie uruchamiany na każdym tooset węzła obliczeń się GWIAZDKĄ — CCM + lokalnie.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-170">This script will be run on each compute node tooset up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="dfdaf-171">Przykładowy skrypt setupstarcm.sh</span><span class="sxs-lookup"><span data-stu-id="dfdaf-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh tooset up STAR-CCM+ locally

    # Create hello CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy hello STAR-CCM package from hello file share toohello local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract hello package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without hello FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="dfdaf-172">Teraz, tooset się GWIAZDKĄ — CCM + na wszystkich systemu Linux węzły obliczeniowe, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-172">Now, tooset up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run hello following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="dfdaf-173">Polecenie hello jest uruchomiona, można monitorować użycie procesora CPU hello za pomocą hello Mapa cieplna z Menedżera klastra.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-173">While hello command is running, you can monitor hello CPU usage by using hello heat map of Cluster Manager.</span></span> <span data-ttu-id="dfdaf-174">Po kilku minutach wszystkie węzły powinny zostać poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="dfdaf-175">Uruchomienie GWIAZDĘ — CCM + zadania</span><span class="sxs-lookup"><span data-stu-id="dfdaf-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="dfdaf-176">HPC Pack służy do jego możliwości harmonogramu zadań w kolejności toorun GWIAZDKĘ — CCM + zadania.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-176">HPC Pack is used for its job scheduler capabilities in order toorun STAR-CCM+ jobs.</span></span> <span data-ttu-id="dfdaf-177">toodo tak, należy hello obsługę kilku skrypty, które są używane toostart hello zadania i uruchomienie GWIAZDĘ — CCM +.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-177">toodo so, we need hello support of a few scripts that are used toostart hello job and run STAR-CCM+.</span></span> <span data-ttu-id="dfdaf-178">dane wejściowe Hello pozostaje w udziale plików Azure hello pierwszy dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-178">hello input data is kept on hello Azure File share first for simplicity.</span></span>

<span data-ttu-id="dfdaf-179">Witaj następującego skryptu programu PowerShell jest używane tooqueue GWIAZDY — CCM + zadania.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-179">hello following PowerShell script is used tooqueue a STAR-CCM+ job.</span></span> <span data-ttu-id="dfdaf-180">Trwa trzech argumentów:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-180">It takes three arguments:</span></span>

* <span data-ttu-id="dfdaf-181">Nazwa modelu Hello</span><span class="sxs-lookup"><span data-stu-id="dfdaf-181">hello model name</span></span>
* <span data-ttu-id="dfdaf-182">Witaj liczba węzłów toobe używane</span><span class="sxs-lookup"><span data-stu-id="dfdaf-182">hello number of nodes toobe used</span></span>
* <span data-ttu-id="dfdaf-183">Witaj liczba rdzeni w każdej toobe węzła używane</span><span class="sxs-lookup"><span data-stu-id="dfdaf-183">hello number of cores on each node toobe used</span></span>

<span data-ttu-id="dfdaf-184">Ponieważ GWIAZDKĘ — CCM + wpisać hello pamięci przepustowość, jego zazwyczaj lepiej toouse mniej rdzenie na węzłach obliczeniowych i Dodaj nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-184">Because STAR-CCM+ can fill hello memory bandwidth, it's usually better toouse fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="dfdaf-185">Witaj dokładna liczba rdzeni przypadająca na węzeł będzie zależeć od hello Rodzina procesorów i szybkość między połączeniami wzajemnymi hello.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-185">hello exact number of cores per node will depend on hello processor family and hello interconnect speed.</span></span>

<span data-ttu-id="dfdaf-186">węzły Hello są przydzielane wyłącznie dla zadania hello i nie może być współużytkowana z innymi zadaniami.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-186">hello nodes are allocated exclusively for hello job and can’t be shared with other jobs.</span></span> <span data-ttu-id="dfdaf-187">Witaj zadania nie jest uruchomiona jako zadanie MPI bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-187">hello job is not started as an MPI job directly.</span></span> <span data-ttu-id="dfdaf-188">Witaj **runstarccm.sh** skrypt powłoki rozpocznie hello MPI uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-188">hello **runstarccm.sh** shell script will start hello MPI launcher.</span></span>

<span data-ttu-id="dfdaf-189">Hello danych wejściowych, model i hello **runstarccm.sh** skryptu są przechowywane w hello **/hpcdata** udziału, który został wcześniej zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-189">hello input model and hello **runstarccm.sh** script are stored in hello **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="dfdaf-190">Pliki dziennika są nazywane hello zadania o identyfikatorze i są przechowywane w hello **udziału /hpcdata**, wraz z hello GWIAZDKĘ — CCM + plików wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-190">Log files are named with hello job ID and are stored in hello **/hpcdata share**, along with hello STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="dfdaf-191">Przykładowy skrypt SubmitStarccmJob.ps1</span><span class="sxs-lookup"><span data-stu-id="dfdaf-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us hello job ID that's used tooidentify hello name of hello uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit hello job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="dfdaf-192">Zastąp **runner.java** z Twojej preferowanych GWIAZDKĄ — CCM + Java modelu uruchamiania i rejestrowanie kodu.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="dfdaf-193">Przykładowy skrypt runstarccm.sh</span><span class="sxs-lookup"><span data-stu-id="dfdaf-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # hello path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set hello mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into hello hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with hello hostfile argument
    #  
    ${STARCCM} -np ${NBCORES} -machinefile ${NODELIST_PATH} \
        -power -podkey "<yourkey>" -rsh ssh \
        -mpi intel -fabric UDAPL -cpubind bandwidth,v \
        -mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0" \
        -batch $2 $3
    RTNSTS=$?
    rm -f ${NODELIST_PATH}

    exit ${RTNSTS}
```

<span data-ttu-id="dfdaf-194">W naszym teście użyliśmy token licencji zasilania na żądanie.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="dfdaf-195">Dla tego tokenu masz tooset hello **$CDLMD_LICENSE_FILE** zmiennej środowiskowej zbyt **1999@flex.cd-adapco.com**  i klucz hello w hello **- podkey** opcji wiersza polecenia hello .</span><span class="sxs-lookup"><span data-stu-id="dfdaf-195">For that token, you have tooset hello **$CDLMD_LICENSE_FILE** environment variable too**1999@flex.cd-adapco.com** and hello key in hello **-podkey** option of hello command line.</span></span>

<span data-ttu-id="dfdaf-196">Po zainicjowaniu niektórych skryptu hello wyodrębnia — z hello **$CCP_NODES_CORES** zmienne środowiskowe, które HPC Pack — Witaj listy węzłów toobuild używa hostfile, który hello uruchamiania MPI.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-196">After some initialization, hello script extracts--from hello **$CCP_NODES_CORES** environment variables that HPC Pack set--hello list of nodes toobuild a hostfile that hello MPI launcher uses.</span></span> <span data-ttu-id="dfdaf-197">Ta hostfile będzie zawierać hello listę nazw węzła obliczeń, które są używane do hello zadania, nazwa jeden na wiersz.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-197">This hostfile will contain hello list of compute node names that are used for hello job, one name per line.</span></span>

<span data-ttu-id="dfdaf-198">Hello format **$CCP_NODES_CORES** następuje tego wzorca:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-198">hello format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="dfdaf-199">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-199">Where:</span></span>

* <span data-ttu-id="dfdaf-200">`<Number of nodes>`jest hello liczba węzłów przydzielone toothis zadania.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-200">`<Number of nodes>` is hello number of nodes allocated toothis job.</span></span>
* <span data-ttu-id="dfdaf-201">`<Name of node_n_...>`jest nazwą hello każdego węzła przydzielone toothis zadania.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-201">`<Name of node_n_...>` is hello name of each node allocated toothis job.</span></span>
* <span data-ttu-id="dfdaf-202">`<Cores of node_n_...>`jest hello liczba rdzeni w węźle hello przydzielone toothis zadania.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-202">`<Cores of node_n_...>` is hello number of cores on hello node allocated toothis job.</span></span>

<span data-ttu-id="dfdaf-203">Witaj liczby rdzeni (**$NBCORES**) jest również obliczeniowej hello na podstawie liczby węzłów (**$NBNODES**) i hello liczba rdzeni przypadająca na węzeł (podać jako parametr **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="dfdaf-203">hello number of cores (**$NBCORES**) is also calculated based on hello number of nodes (**$NBNODES**) and hello number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="dfdaf-204">Opcje MPI hello hello te, które są używane z Intel MPI na platformie Azure są:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-204">For hello MPI options, hello ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="dfdaf-205">`-mpi intel`toospecify Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-205">`-mpi intel` toospecify Intel MPI.</span></span>
* <span data-ttu-id="dfdaf-206">`-fabric UDAPL`toouse Azure InfiniBand zleceń.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-206">`-fabric UDAPL` toouse Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="dfdaf-207">`-cpubind bandwidth,v`przepustowość toooptimize MPI z GWIAZDKĄ — CCM +.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-207">`-cpubind bandwidth,v` toooptimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="dfdaf-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`toomake Intel MPI współpracować Azure InfiniBand i tooset hello wymagana liczba rdzeni przypadająca na węzeł.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` toomake Intel MPI work with Azure InfiniBand, and tooset hello required number of cores per node.</span></span>
* <span data-ttu-id="dfdaf-209">`-batch`toostart GWIAZDKĘ — CCM + w trybie wsadowym z bez interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-209">`-batch` toostart STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="dfdaf-210">Na koniec toostart zadania, upewnij się, że węzły są gotowe do działania i są w trybie online w Menedżerze klastra.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-210">Finally, toostart a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="dfdaf-211">Następnie w wierszu polecenia programu PowerShell, uruchom to:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="dfdaf-212">Zatrzymaj węzłów</span><span class="sxs-lookup"><span data-stu-id="dfdaf-212">Stop nodes</span></span>
<span data-ttu-id="dfdaf-213">Później po wykonaniu tych testów, można użyć następującego toostop polecenia środowiska PowerShell klastra HPC Pack hello i rozpocząć węzłów:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-213">Later on, after you're done with your tests, you can use hello following HPC Pack PowerShell commands toostop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="dfdaf-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dfdaf-214">Next steps</span></span>
<span data-ttu-id="dfdaf-215">Spróbuj uruchomić inne obciążenia systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="dfdaf-215">Try running other Linux workloads.</span></span> <span data-ttu-id="dfdaf-216">Na przykład zobacz:</span><span class="sxs-lookup"><span data-stu-id="dfdaf-216">For example, see:</span></span>

* [<span data-ttu-id="dfdaf-217">Uruchamianie NAMD z pakietem Microsoft HPC w węzłach obliczeń systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="dfdaf-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="dfdaf-218">Uruchom OpenFOAM z pakietem Microsoft HPC w klastrze RDMA systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="dfdaf-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
