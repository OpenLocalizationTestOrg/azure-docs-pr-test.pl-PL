---
title: "Uruchomienie GWIAZDĘ — CCM + pakietem HPC na maszynach wirtualnych systemu Linux | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: b45fcfb981287035da02fda62eaf5f9436ec2379
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="run-star-ccm-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="f68f9-103">Uruchomienie GWIAZDĘ — CCM + z pakietem Microsoft HPC na Linux RDMA klaster na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f68f9-103">Run STAR-CCM+ with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="f68f9-104">W tym artykule przedstawiono sposób wdrażania klastra Microsoft HPC Pack na platformie Azure i uruchom [GWIAZDKĘ CD adapco-CCM +](http://www.cd-adapco.com/products/star-ccm%C2%AE) zadania na wielu węzłach obliczeniowych Linux, które są wzajemnie InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="f68f9-104">This article shows you how to deploy a Microsoft HPC Pack cluster on Azure and run a [CD-adapco STAR-CCM+](http://www.cd-adapco.com/products/star-ccm%C2%AE) job on multiple Linux compute nodes that are interconnected with InfiniBand.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f68f9-105">Microsoft HPC Pack udostępnia funkcje, aby obsługiwał różne HPC na dużą skalę i równoległych aplikacji, w tym aplikacji MPI w klastrach maszyny wirtualne Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f68f9-105">Microsoft HPC Pack provides features to run a variety of large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="f68f9-106">HPC Pack również umożliwia uruchamianie aplikacji HPC systemu Linux na węźle obliczeń maszyn wirtualnych systemu Linux, które zostały wdrożone w klastrze HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="f68f9-106">HPC Pack also supports running Linux HPC applications on Linux compute-node VMs that are deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="f68f9-107">Aby obejrzeć wprowadzenie do pomocą Linux węzły obliczeniowe HPC Pack zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="f68f9-107">For an introduction to using Linux compute nodes with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="set-up-an-hpc-pack-cluster"></a><span data-ttu-id="f68f9-108">Konfigurowanie klastra HPC Pack</span><span class="sxs-lookup"><span data-stu-id="f68f9-108">Set up an HPC Pack cluster</span></span>
<span data-ttu-id="f68f9-109">Pobierz skrypty wdrażania HPC Pack IaaS z [Centrum pobierania](https://www.microsoft.com/en-us/download/details.aspx?id=44949) i wyodrębnić je lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f68f9-109">Download the HPC Pack IaaS deployment scripts from the [Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=44949) and extract them locally.</span></span>

<span data-ttu-id="f68f9-110">Program Azure PowerShell jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="f68f9-110">Azure PowerShell is a prerequisite.</span></span> <span data-ttu-id="f68f9-111">Jeśli nie skonfigurowano programu PowerShell na komputerze lokalnym, przeczytaj artykuł na temat [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f68f9-111">If PowerShell is not configured on your local machine, please read the article [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="f68f9-112">W momencie pisania tego dokumentu obrazy systemu Linux z portalu Azure Marketplace, (zawierający sterowniki InfiniBand dla platformy Azure) są SLES 12, CentOS 6.5 i CentOS 7.1.</span><span class="sxs-lookup"><span data-stu-id="f68f9-112">At the time of this writing, the Linux images from the Azure Marketplace (which contains the InfiniBand drivers for Azure) are for SLES 12, CentOS 6.5, and CentOS 7.1.</span></span> <span data-ttu-id="f68f9-113">W tym artykule jest na podstawie użycia SLES 12.</span><span class="sxs-lookup"><span data-stu-id="f68f9-113">This article is based on the usage of SLES 12.</span></span> <span data-ttu-id="f68f9-114">Aby pobrać nazwy wszystkich obrazów systemu Linux, które obsługują HPC w witrynie Marketplace, można uruchomić następujące polecenie programu PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f68f9-114">To retrieve the name of all Linux images that support HPC in the Marketplace, you can run the following PowerShell command:</span></span>

```
    get-azurevmimage | ?{$_.ImageName.Contains("hpc") -and $_.OS -eq "Linux" }
```

<span data-ttu-id="f68f9-115">Wyświetla dane wyjściowe, lokalizacji, w których te obrazy są dostępne i nazwa obrazu (**Nazwa_obrazu**) do użycia w szablonie wdrożenia później.</span><span class="sxs-lookup"><span data-stu-id="f68f9-115">The output lists the location in which these images are available and the image name (**ImageName**) to be used in the deployment template later.</span></span>

<span data-ttu-id="f68f9-116">Przed wdrożeniem klastra, masz do utworzenia pliku szablonu wdrożenia HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="f68f9-116">Before you deploy the cluster, you have to build an HPC Pack deployment template file.</span></span> <span data-ttu-id="f68f9-117">Ponieważ firma Microsoft docelowych małych klastra, węzłem głównym zostanie kontrolera domeny i hosta lokalnego bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="f68f9-117">Because we're targeting a small cluster, the head node will be the domain controller and host a local SQL database.</span></span>

<span data-ttu-id="f68f9-118">Następujący szablon będzie wdrażanie węzła głównego, Utwórz plik XML o nazwie **MyCluster.xml**i Zastąp wartości **SubscriptionId**, **StorageAccount**,  **Lokalizacja**, **VMName**, i **ServiceName** z Twoimi zmianami.</span><span class="sxs-lookup"><span data-stu-id="f68f9-118">The following template will deploy such a head node, create an XML file named **MyCluster.xml**, and replace the values of **SubscriptionId**, **StorageAccount**, **Location**, **VMName**, and **ServiceName** with yours.</span></span>

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

<span data-ttu-id="f68f9-119">Rozpocznij tworzenie węzłem head za pomocą polecenia programu PowerShell w wiersza polecenia o podniesionych uprawnieniach:</span><span class="sxs-lookup"><span data-stu-id="f68f9-119">Start the head-node creation by running the PowerShell command in an elevated command prompt:</span></span>

```
    .\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml
```

<span data-ttu-id="f68f9-120">Po upływie 20-30 minut zapewne zechcesz węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="f68f9-120">After 20 to 30 minutes, the head node should be ready.</span></span> <span data-ttu-id="f68f9-121">Można połączyć się go w portalu Azure, klikając **Connect** ikona maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f68f9-121">You can connect to it from the Azure portal by clicking the **Connect** icon of the virtual machine.</span></span>

<span data-ttu-id="f68f9-122">Po pewnym czasie może być konieczne napraw usługę przesyłania dalej DNS.</span><span class="sxs-lookup"><span data-stu-id="f68f9-122">You might eventually have to fix the DNS forwarder.</span></span> <span data-ttu-id="f68f9-123">Aby to zrobić, uruchom Menedżera DNS.</span><span class="sxs-lookup"><span data-stu-id="f68f9-123">To do so, start DNS Manager.</span></span>

1. <span data-ttu-id="f68f9-124">Kliknij prawym przyciskiem myszy nazwę serwera w Menedżerze DNS, wybierz **właściwości**, a następnie kliknij przycisk **usług przesyłania dalej** kartę.</span><span class="sxs-lookup"><span data-stu-id="f68f9-124">Right-click the server name in DNS Manager, select **Properties**, and then click the **Forwarders** tab.</span></span>
2. <span data-ttu-id="f68f9-125">Kliknij przycisk **Edytuj** przycisk, aby usunąć wszystkie usługi przesyłania dalej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f68f9-125">Click the **Edit** button to remove any forwarders, and then click **OK**.</span></span>
3. <span data-ttu-id="f68f9-126">Upewnij się, że **Użyj wskazówek dotyczących serwerów głównych, jeśli są dostępne nie usług przesyłania dalej** pole wyboru jest zaznaczone, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f68f9-126">Make sure that the **Use root hints if no forwarders are available** check box is selected, and then click **OK**.</span></span>

## <a name="set-up-linux-compute-nodes"></a><span data-ttu-id="f68f9-127">Konfigurowanie węzłów obliczeniowych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="f68f9-127">Set up Linux compute nodes</span></span>
<span data-ttu-id="f68f9-128">Możesz wdrożyć węzły obliczeniowe systemu Linux przy użyciu tego samego szablonu wdrażania, która pozwala utworzyć węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="f68f9-128">You deploy the Linux compute nodes by using the same deployment template that you used to create the head node.</span></span>

<span data-ttu-id="f68f9-129">Skopiuj plik **MyCluster.xml** z komputera lokalnego do węzła głównego i aktualizacja **NodeCount** tag o liczbie węzłów, które mają zostać wdrożone (< = 20).</span><span class="sxs-lookup"><span data-stu-id="f68f9-129">Copy the file **MyCluster.xml** from your local machine to the head node, and update the **NodeCount** tag with the number of nodes that you want to deploy (<=20).</span></span> <span data-ttu-id="f68f9-130">Należy zachować ostrożność ma za mało dostępnych rdzeni limitu Azure, ponieważ każde wystąpienie A9 będą korzystać z 16 rdzeni w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f68f9-130">Be careful to have enough available cores in your Azure quota, because each A9 instance will consume 16 cores in your subscription.</span></span> <span data-ttu-id="f68f9-131">Jeśli chcesz użyć więcej maszyn wirtualnych w tej samej budżetu, można użyć wystąpienia A8 (8 rdzeni) zamiast A9.</span><span class="sxs-lookup"><span data-stu-id="f68f9-131">You can use A8 instances (8 cores) instead of A9 if you want to use more VMs in the same budget.</span></span>

<span data-ttu-id="f68f9-132">W węźle głównym skopiuj HPC Pack IaaS skryptów wdrażania.</span><span class="sxs-lookup"><span data-stu-id="f68f9-132">On the head node, copy the HPC Pack IaaS deployment scripts.</span></span>

<span data-ttu-id="f68f9-133">Uruchom następujące polecenia programu PowerShell systemu Azure w wiersza polecenia o podniesionych uprawnieniach:</span><span class="sxs-lookup"><span data-stu-id="f68f9-133">Run the following Azure PowerShell commands in an elevated command prompt:</span></span>

1. <span data-ttu-id="f68f9-134">Uruchom **Add-AzureAccount** nawiązać połączenia z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f68f9-134">Run **Add-AzureAccount** to connect to your Azure subscription.</span></span>
2. <span data-ttu-id="f68f9-135">Jeśli masz wiele subskrypcji, uruchom **Get AzureSubscription** wyświetlić je.</span><span class="sxs-lookup"><span data-stu-id="f68f9-135">If you have multiple subscriptions, run **Get-AzureSubscription** to list them.</span></span>
3. <span data-ttu-id="f68f9-136">Wartość domyślna subskrypcja, uruchamiając **xxxx wybierz AzureSubscription — Nazwa subskrypcji — domyślna** polecenia.</span><span class="sxs-lookup"><span data-stu-id="f68f9-136">Set a default subscription by running the **Select-AzureSubscription -SubscriptionName xxxx -Default** command.</span></span>
4. <span data-ttu-id="f68f9-137">Uruchom **.\New-HPCIaaSCluster.ps1 - ConfigFile MyCluster.xml** rozpocząć wdrażanie węzły obliczeniowe systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f68f9-137">Run **.\New-HPCIaaSCluster.ps1 -ConfigFile MyCluster.xml** to start deploying Linux compute nodes.</span></span>
   
   ![Wdrażanie węzła HEAD w akcji][hndeploy]

<span data-ttu-id="f68f9-139">Otwórz narzędzie Menedżer klastra HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="f68f9-139">Open the HPC Pack Cluster Manager tool.</span></span> <span data-ttu-id="f68f9-140">Po kilku minutach węzły obliczeniowe Linux regularnie pojawi się lista węzły klastra obliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="f68f9-140">After few minutes, Linux compute nodes will regularly appear in list of cluster compute nodes.</span></span> <span data-ttu-id="f68f9-141">W trybie klasycznym wdrażania maszyn wirtualnych IaaS są tworzone po kolei.</span><span class="sxs-lookup"><span data-stu-id="f68f9-141">With the classic deployment mode, IaaS VMs are created sequentially.</span></span> <span data-ttu-id="f68f9-142">Dlatego jeśli ważne jest liczba węzłów, pobieranie wszystkie wdrożone może zająć znaczną ilość czasu.</span><span class="sxs-lookup"><span data-stu-id="f68f9-142">So if the number of nodes is important, getting them all deployed can take a significant amount of time.</span></span>

![Linux węzłów w Menedżerze klastra HPC Pack][clustermanager]

<span data-ttu-id="f68f9-144">Teraz wszystkie węzły są gotowe do działania w klastrze, czy ustawienia dodatkowej infrastruktury, aby się upewnić.</span><span class="sxs-lookup"><span data-stu-id="f68f9-144">Now that all nodes are up and running in the cluster, there are additional infrastructure settings to make.</span></span>

## <a name="set-up-an-azure-file-share-for-windows-and-linux-nodes"></a><span data-ttu-id="f68f9-145">Konfigurowanie udziału plików platformy Azure dla systemu Windows i Linux węzłów</span><span class="sxs-lookup"><span data-stu-id="f68f9-145">Set up an Azure File share for Windows and Linux nodes</span></span>
<span data-ttu-id="f68f9-146">Usługa Azure plików służy do przechowywania plików danych, pakiety aplikacji i skryptów.</span><span class="sxs-lookup"><span data-stu-id="f68f9-146">You can use the Azure File service to store scripts, application packages, and data files.</span></span> <span data-ttu-id="f68f9-147">Plików na platformę Azure zapewnia możliwości CIFS u góry magazynu obiektów Blob platformy Azure jako magazynu trwałego.</span><span class="sxs-lookup"><span data-stu-id="f68f9-147">Azure File provides CIFS capabilities on top of Azure Blob storage as a persistent store.</span></span> <span data-ttu-id="f68f9-148">Należy pamiętać, że nie jest to najbardziej skalowalne rozwiązanie, ale jest to najprostsza i nie wymaga dedykowanych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="f68f9-148">Be aware that this is not the most scalable solution, but it is the simplest one and doesn’t require dedicated VMs.</span></span>

<span data-ttu-id="f68f9-149">Tworzenie udziału plików platformy Azure zgodnie z instrukcjami w artykule [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="f68f9-149">Create an Azure File share by following the instructions in the article [Get started with Azure File storage on Windows](../../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>

<span data-ttu-id="f68f9-150">Zachowaj nazwę konta magazynu jako **saname**, nazwa udziału plików jako **sharename**i klucz konta magazynu jako **sakey**.</span><span class="sxs-lookup"><span data-stu-id="f68f9-150">Keep the name of your storage account as **saname**, the file share name as **sharename**, and the storage account key as **sakey**.</span></span>

### <a name="mount-the-azure-file-share-on-the-head-node"></a><span data-ttu-id="f68f9-151">Instalowanie udziału plików Azure w węźle głównym</span><span class="sxs-lookup"><span data-stu-id="f68f9-151">Mount the Azure File share on the head node</span></span>
<span data-ttu-id="f68f9-152">Otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie, aby zapisać poświadczenia w magazynie komputera lokalnego:</span><span class="sxs-lookup"><span data-stu-id="f68f9-152">Open an elevated command prompt and run the following command to store the credentials in the local machine vault:</span></span>

```
    cmdkey /add:<saname>.file.core.windows.net /user:<saname> /pass:<sakey>
```

<span data-ttu-id="f68f9-153">Następnie Aby zainstalować udział plików Azure, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="f68f9-153">Then, to mount the Azure File share, run:</span></span>

```
    net use Z: \\<saname>.file.core.windows.net\<sharename> /persistent:yes
```

### <a name="mount-the-azure-file-share-on-linux-compute-nodes"></a><span data-ttu-id="f68f9-154">Instalowanie udziału plików Azure w węzłach obliczeniowych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="f68f9-154">Mount the Azure File share on Linux compute nodes</span></span>
<span data-ttu-id="f68f9-155">Jeden przydatne narzędzie dołączoną HPC Pack to narzędzie clusrun.</span><span class="sxs-lookup"><span data-stu-id="f68f9-155">One useful tool that comes with HPC Pack is the clusrun tool.</span></span> <span data-ttu-id="f68f9-156">To narzędzie wiersza polecenia umożliwia jednoczesną tego samego polecenia na zestaw węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="f68f9-156">You can use this command-line tool to run the same command simultaneously on a set of compute nodes.</span></span> <span data-ttu-id="f68f9-157">W tym przypadku służy do udziałów plików Azure i utrwala go przetrwać ponowne uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="f68f9-157">In our case, it's used to mount the Azure File share and persist it to survive reboots.</span></span>
<span data-ttu-id="f68f9-158">W podniesionego wiersza poleceń w węźle głównym uruchom następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="f68f9-158">In an elevated command prompt on the head node, run the following commands.</span></span>

<span data-ttu-id="f68f9-159">Aby utworzyć katalog instalacji:</span><span class="sxs-lookup"><span data-stu-id="f68f9-159">To create the mount directory:</span></span>

```
    clusrun /nodegroup:LinuxNodes mkdir -p /hpcdata
```

<span data-ttu-id="f68f9-160">Aby zainstalować udział plików Azure:</span><span class="sxs-lookup"><span data-stu-id="f68f9-160">To mount the Azure File share:</span></span>

```
    clusrun /nodegroup:LinuxNodes mount -t cifs //<saname>.file.core.windows.net/<sharename> /hpcdata -o vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777
```

<span data-ttu-id="f68f9-161">Aby zachować udziału instalacji:</span><span class="sxs-lookup"><span data-stu-id="f68f9-161">To persist the mount share:</span></span>

```
    clusrun /nodegroup:LinuxNodes "echo //<saname>.file.core.windows.net/<sharename> /hpcdata cifs vers=2.1,username=<saname>,password='<sakey>',dir_mode=0777,file_mode=0777 >> /etc/fstab"
```

## <a name="install-star-ccm"></a><span data-ttu-id="f68f9-162">Zainstaluj GWIAZDKĘ — CCM +</span><span class="sxs-lookup"><span data-stu-id="f68f9-162">Install STAR-CCM+</span></span>
<span data-ttu-id="f68f9-163">Azure wystąpień maszyna wirtualna A8 i A9 świadczenie obsługi InfiniBand i funkcji RDMA.</span><span class="sxs-lookup"><span data-stu-id="f68f9-163">Azure VM instances A8 and A9 provide InfiniBand support and RDMA capabilities.</span></span> <span data-ttu-id="f68f9-164">Sterowniki jądra, które włączają te funkcje są dostępne dla systemu Windows Server 2012 R2, SUSE 12 CentOS 6.5 i CentOS 7.1 obrazów w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f68f9-164">The kernel drivers that enable those capabilities are available for Windows Server 2012 R2, SUSE 12, CentOS 6.5, and CentOS 7.1 images in the Azure Marketplace.</span></span> <span data-ttu-id="f68f9-165">Microsoft MPI i MPI firmy Intel (wersji 5.x) są dwie biblioteki MPI, które obsługują te sterowniki w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="f68f9-165">Microsoft MPI and Intel MPI (release 5.x) are the two MPI libraries that support those drivers in Azure.</span></span>

<span data-ttu-id="f68f9-166">GWIAZDKĘ CD adapco — CCM + wersji 11.x i później jest powiązane z wersją Intel MPI 5.x, więc InfiniBand obsługę Azure jest dołączony.</span><span class="sxs-lookup"><span data-stu-id="f68f9-166">CD-adapco STAR-CCM+ release 11.x and later is bundled with Intel MPI version 5.x, so InfiniBand support for Azure is included.</span></span>

<span data-ttu-id="f68f9-167">Pobierz Linux64 GWIAZDKĘ — CCM + pakietu z [CD adapco portal](https://steve.cd-adapco.com).</span><span class="sxs-lookup"><span data-stu-id="f68f9-167">Get the Linux64 STAR-CCM+ package from the [CD-adapco portal](https://steve.cd-adapco.com).</span></span> <span data-ttu-id="f68f9-168">W naszym przykładzie użyliśmy wersji 11.02.010 w mieszanych dokładności.</span><span class="sxs-lookup"><span data-stu-id="f68f9-168">In our case, we used version 11.02.010 in mixed precision.</span></span>

<span data-ttu-id="f68f9-169">W węźle głównym w **/hpcdata** plików Azure udostępnić, utworzyć skrypt powłoki o nazwie **setupstarccm.sh** o następującej zawartości.</span><span class="sxs-lookup"><span data-stu-id="f68f9-169">On the head node, in the **/hpcdata** Azure File share, create a shell script named **setupstarccm.sh** with the following content.</span></span> <span data-ttu-id="f68f9-170">Ten skrypt będzie uruchamiany w każdym węźle obliczeń, aby skonfigurować GWIAZDKĘ — CCM + lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f68f9-170">This script will be run on each compute node to set up STAR-CCM+ locally.</span></span>

#### <a name="sample-setupstarcmsh-script"></a><span data-ttu-id="f68f9-171">Przykładowy skrypt setupstarcm.sh</span><span class="sxs-lookup"><span data-stu-id="f68f9-171">Sample setupstarcm.sh script</span></span>
```
    #!/bin/bash
    # setupstarcm.sh to set up STAR-CCM+ locally

    # Create the CD-adapco main directory
    mkdir -p /opt/CD-adapco

    # Copy the STAR-CCM package from the file share to the local directory
    cp /hpcdata/StarCCM/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz /opt/CD-adapco/

    # Extract the package
    tar -xzf /opt/CD-adapco/STAR-CCM+11.02.010_01_linux-x86_64.tar.gz -C /opt/CD-adapco/

    # Start a silent installation of STAR-CCM without the FLEXlm component
    /opt/CD-adapco/starccm+_11.02.010/STAR-CCM+11.02.010_01_linux-x86_64-2.5_gnu4.8.bin -i silent -DCOMPUTE_NODE=true -DNODOC=true -DINSTALLFLEX=false

    # Update memory limits
    echo "*               hard    memlock         unlimited" >> /etc/security/limits.conf
    echo "*               soft    memlock         unlimited" >> /etc/security/limits.conf
```
<span data-ttu-id="f68f9-172">Teraz, aby skonfigurować GWIAZDKĘ — CCM + na wszystkich systemu Linux węzły obliczeniowe, otwórz wiersz polecenia z podwyższonym poziomem uprawnień i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f68f9-172">Now, to set up STAR-CCM+ on all your Linux compute nodes, open an elevated command prompt and run the following command:</span></span>

```
    clusrun /nodegroup:LinuxNodes bash /hpcdata/setupstarccm.sh
```

<span data-ttu-id="f68f9-173">Po uruchomieniu polecenia można monitorować użycie procesora CPU za pomocą Mapa cieplna z Menedżera klastra.</span><span class="sxs-lookup"><span data-stu-id="f68f9-173">While the command is running, you can monitor the CPU usage by using the heat map of Cluster Manager.</span></span> <span data-ttu-id="f68f9-174">Po kilku minutach wszystkie węzły powinny zostać poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="f68f9-174">After few minutes, all nodes should be correctly set up.</span></span>

## <a name="run-star-ccm-jobs"></a><span data-ttu-id="f68f9-175">Uruchomienie GWIAZDĘ — CCM + zadania</span><span class="sxs-lookup"><span data-stu-id="f68f9-175">Run STAR-CCM+ jobs</span></span>
<span data-ttu-id="f68f9-176">HPC Pack służy do jego możliwości harmonogram zadania uruchomienie GWIAZDĘ — CCM + zadania.</span><span class="sxs-lookup"><span data-stu-id="f68f9-176">HPC Pack is used for its job scheduler capabilities in order to run STAR-CCM+ jobs.</span></span> <span data-ttu-id="f68f9-177">Aby to zrobić, potrzebujemy obsługę kilku skryptów, które są używane do uruchamiania zadania i uruchomienie GWIAZDĘ — CCM +.</span><span class="sxs-lookup"><span data-stu-id="f68f9-177">To do so, we need the support of a few scripts that are used to start the job and run STAR-CCM+.</span></span> <span data-ttu-id="f68f9-178">Dane wejściowe pozostaje w udziale plików Azure pierwszy dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="f68f9-178">The input data is kept on the Azure File share first for simplicity.</span></span>

<span data-ttu-id="f68f9-179">Poniższy skrypt programu PowerShell jest używany do kolejki GWIAZDY — CCM + zadania.</span><span class="sxs-lookup"><span data-stu-id="f68f9-179">The following PowerShell script is used to queue a STAR-CCM+ job.</span></span> <span data-ttu-id="f68f9-180">Trwa trzech argumentów:</span><span class="sxs-lookup"><span data-stu-id="f68f9-180">It takes three arguments:</span></span>

* <span data-ttu-id="f68f9-181">Nazwa modelu</span><span class="sxs-lookup"><span data-stu-id="f68f9-181">The model name</span></span>
* <span data-ttu-id="f68f9-182">Liczba węzłów do użycia</span><span class="sxs-lookup"><span data-stu-id="f68f9-182">The number of nodes to be used</span></span>
* <span data-ttu-id="f68f9-183">Liczba rdzeni w każdym węźle ma być używany</span><span class="sxs-lookup"><span data-stu-id="f68f9-183">The number of cores on each node to be used</span></span>

<span data-ttu-id="f68f9-184">Ponieważ GWIAZDKĘ — CCM + wpisać przepustowości pamięci jest lepiej jest użyć mniejszej liczby rdzeni w jednym węzłów obliczeniowych i dodać nowe węzły.</span><span class="sxs-lookup"><span data-stu-id="f68f9-184">Because STAR-CCM+ can fill the memory bandwidth, it's usually better to use fewer cores per compute nodes and add new nodes.</span></span> <span data-ttu-id="f68f9-185">Dokładna liczba rdzeni w jednym węźle zależy od rodziny procesorów i szybkość połączenia.</span><span class="sxs-lookup"><span data-stu-id="f68f9-185">The exact number of cores per node will depend on the processor family and the interconnect speed.</span></span>

<span data-ttu-id="f68f9-186">Węzły są przydzielane wyłącznie dla zadania i nie może być współużytkowana z innymi zadaniami.</span><span class="sxs-lookup"><span data-stu-id="f68f9-186">The nodes are allocated exclusively for the job and can’t be shared with other jobs.</span></span> <span data-ttu-id="f68f9-187">Zadanie nie jest uruchomiona jako zadanie MPI bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="f68f9-187">The job is not started as an MPI job directly.</span></span> <span data-ttu-id="f68f9-188">**Runstarccm.sh** skrypt powłoki rozpocznie uruchamiania MPI.</span><span class="sxs-lookup"><span data-stu-id="f68f9-188">The **runstarccm.sh** shell script will start the MPI launcher.</span></span>

<span data-ttu-id="f68f9-189">Wejściowy modelu i **runstarccm.sh** skryptu są przechowywane w **/hpcdata** udziału, który został wcześniej zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="f68f9-189">The input model and the **runstarccm.sh** script are stored in the **/hpcdata** share that was previously mounted.</span></span>

<span data-ttu-id="f68f9-190">Pliki dziennika są nazywane z Identyfikatorem zadania i są przechowywane w **udziału /hpcdata**, wraz z GWIAZDY — CCM + plików wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="f68f9-190">Log files are named with the job ID and are stored in the **/hpcdata share**, along with the STAR-CCM+ output files.</span></span>

#### <a name="sample-submitstarccmjobps1-script"></a><span data-ttu-id="f68f9-191">Przykładowy skrypt SubmitStarccmJob.ps1</span><span class="sxs-lookup"><span data-stu-id="f68f9-191">Sample SubmitStarccmJob.ps1 script</span></span>
```
    Add-PSSnapin Microsoft.HPC -ErrorAction silentlycontinue
    $scheduler="headnodename"
    $modelName=$args[0]
    $nbCoresPerNode=$args[2]
    $nbNodes=$args[1]

    #---------------------------------------------------------------------------------------------------------
    # Create a new job; this will give us the job ID that's used to identify the name of the uploaded package in Azure
    #
    $job = New-HpcJob -Name "$modelName $nbNodes $nbCoresPerNode" -Scheduler $scheduler -NumNodes $nbNodes -NodeGroups "LinuxNodes" -FailOnTaskFailure $true -Exclusive $true
    $jobId = [String]$job.Id

    #---------------------------------------------------------------------------------------------------------
    # Submit the job     
    $workdir =  "/hpcdata"
    $execName = "$nbCoresPerNode runner.java $modelName.sim"

    $job | Add-HpcTask -Scheduler $scheduler -Name "Compute" -stdout "$jobId.log" -stderr "$jobId.err" -Rerunnable $false -NumNodes $nbNodes -Command "runstarccm.sh $execName" -WorkDir "$workdir"


    Submit-HpcJob -Job $job -Scheduler $scheduler
```
<span data-ttu-id="f68f9-192">Zastąp **runner.java** z Twojej preferowanych GWIAZDKĄ — CCM + Java modelu uruchamiania i rejestrowanie kodu.</span><span class="sxs-lookup"><span data-stu-id="f68f9-192">Replace **runner.java** with your preferred STAR-CCM+ Java model launcher and logging code.</span></span>

#### <a name="sample-runstarccmsh-script"></a><span data-ttu-id="f68f9-193">Przykładowy skrypt runstarccm.sh</span><span class="sxs-lookup"><span data-stu-id="f68f9-193">Sample runstarccm.sh script</span></span>
```
    #!/bin/bash
    echo "start"
    # The path of this script
    SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
    echo ${SCRIPT_PATH}
    # Set the mpirun runtime environment
    export CDLMD_LICENSE_FILE=1999@flex.cd-adapco.com

    # mpirun command
    STARCCM=/opt/CD-adapco/STAR-CCM+11.02.010/star/bin/starccm+

    # Get node information from ENVs
    NODESCORES=(${CCP_NODES_CORES})
    COUNT=${#NODESCORES[@]}
    NBCORESPERNODE=$1

    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$
    echo ${NODELIST_PATH}

    # Get every node name and write into the hostfile file
    I=1
    NBNODES=0
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
        let "NBNODES=${NBNODES}+1"
    done
    let "NBCORES=${NBNODES}*${NBCORESPERNODE}"

    # Run STAR-CCM with the hostfile argument
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

<span data-ttu-id="f68f9-194">W naszym teście użyliśmy token licencji zasilania na żądanie.</span><span class="sxs-lookup"><span data-stu-id="f68f9-194">In our test, we used a Power-On-Demand license token.</span></span> <span data-ttu-id="f68f9-195">Token, należy ustawić **$CDLMD_LICENSE_FILE** zmienną środowiskową  **1999@flex.cd-adapco.com**  i klucz w **- podkey** opcji wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="f68f9-195">For that token, you have to set the **$CDLMD_LICENSE_FILE** environment variable to **1999@flex.cd-adapco.com** and the key in the **-podkey** option of the command line.</span></span>

<span data-ttu-id="f68f9-196">Po zainicjowaniu niektórych skrypt wyodrębnia — od **$CCP_NODES_CORES** zmienne środowiskowe tego pakietu HPC ustawiane — Lista węzłów do tworzenia hostfile, używającej uruchamiania MPI.</span><span class="sxs-lookup"><span data-stu-id="f68f9-196">After some initialization, the script extracts--from the **$CCP_NODES_CORES** environment variables that HPC Pack set--the list of nodes to build a hostfile that the MPI launcher uses.</span></span> <span data-ttu-id="f68f9-197">Ta hostfile będzie zawierać listę nazw węzła obliczeń, które są używane do zadania, nazwa jeden na wiersz.</span><span class="sxs-lookup"><span data-stu-id="f68f9-197">This hostfile will contain the list of compute node names that are used for the job, one name per line.</span></span>

<span data-ttu-id="f68f9-198">Format **$CCP_NODES_CORES** następuje tego wzorca:</span><span class="sxs-lookup"><span data-stu-id="f68f9-198">The format of **$CCP_NODES_CORES** follows this pattern:</span></span>

```
<Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
```

<span data-ttu-id="f68f9-199">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="f68f9-199">Where:</span></span>

* <span data-ttu-id="f68f9-200">`<Number of nodes>`jest to liczba węzłów przydzielone do tego zadania.</span><span class="sxs-lookup"><span data-stu-id="f68f9-200">`<Number of nodes>` is the number of nodes allocated to this job.</span></span>
* <span data-ttu-id="f68f9-201">`<Name of node_n_...>`to nazwa każdego węzła przydzielone do tego zadania.</span><span class="sxs-lookup"><span data-stu-id="f68f9-201">`<Name of node_n_...>` is the name of each node allocated to this job.</span></span>
* <span data-ttu-id="f68f9-202">`<Cores of node_n_...>`jest to liczba rdzeni w węźle przydzielone do tego zadania.</span><span class="sxs-lookup"><span data-stu-id="f68f9-202">`<Cores of node_n_...>` is the number of cores on the node allocated to this job.</span></span>

<span data-ttu-id="f68f9-203">Liczba rdzeni (**$NBCORES**) jest obliczana na podstawie liczby węzłów (**$NBNODES**) i liczba rdzeni przypadająca na węzeł (podać jako parametr **$NBCORESPERNODE**).</span><span class="sxs-lookup"><span data-stu-id="f68f9-203">The number of cores (**$NBCORES**) is also calculated based on the number of nodes (**$NBNODES**) and the number of cores per node (provided as parameter **$NBCORESPERNODE**).</span></span>

<span data-ttu-id="f68f9-204">Dla opcji MPI te, które są używane z Intel MPI na platformie Azure są:</span><span class="sxs-lookup"><span data-stu-id="f68f9-204">For the MPI options, the ones that are used with Intel MPI on Azure are:</span></span>

* <span data-ttu-id="f68f9-205">`-mpi intel`Aby określić Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="f68f9-205">`-mpi intel` to specify Intel MPI.</span></span>
* <span data-ttu-id="f68f9-206">`-fabric UDAPL`do korzystania z poleceń Azure InfiniBand.</span><span class="sxs-lookup"><span data-stu-id="f68f9-206">`-fabric UDAPL` to use Azure InfiniBand verbs.</span></span>
* <span data-ttu-id="f68f9-207">`-cpubind bandwidth,v`w celu zoptymalizowania przepustowości dla MPI z GWIAZDKĄ — CCM +.</span><span class="sxs-lookup"><span data-stu-id="f68f9-207">`-cpubind bandwidth,v` to optimize bandwidth for MPI with STAR-CCM+.</span></span>
* <span data-ttu-id="f68f9-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"`Aby pracować z Azure InfiniBand MPI Intel i ustawić wymaganej liczby rdzeni w jednym węźle.</span><span class="sxs-lookup"><span data-stu-id="f68f9-208">`-mppflags "-ppn $NBCORESPERNODE -genv I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -genv I_MPI_DAPL_UD=0 -genv I_MPI_DYNAMIC_CONNECTION=0"` to make Intel MPI work with Azure InfiniBand, and to set the required number of cores per node.</span></span>
* <span data-ttu-id="f68f9-209">`-batch`Aby uruchomić GWIAZDKĘ — CCM + w trybie wsadowym z bez interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f68f9-209">`-batch` to start STAR-CCM+ in batch mode with no UI.</span></span>

<span data-ttu-id="f68f9-210">Na koniec można uruchomić zadania, upewnij się, że węzły są gotowe do działania i są w trybie online w Menedżerze klastra.</span><span class="sxs-lookup"><span data-stu-id="f68f9-210">Finally, to start a job, make sure that your nodes are up and running and are online in Cluster Manager.</span></span> <span data-ttu-id="f68f9-211">Następnie w wierszu polecenia programu PowerShell, uruchom to:</span><span class="sxs-lookup"><span data-stu-id="f68f9-211">Then from a PowerShell command prompt, run this:</span></span>

```
    .\ SubmitStarccmJob.ps1 <model> <nbNodes> <nbCoresPerNode>
```

## <a name="stop-nodes"></a><span data-ttu-id="f68f9-212">Zatrzymaj węzłów</span><span class="sxs-lookup"><span data-stu-id="f68f9-212">Stop nodes</span></span>
<span data-ttu-id="f68f9-213">Później po wykonaniu tych testów, służy następujące polecenia środowiska PowerShell klastra HPC Pack do zatrzymywania i uruchamiania węzłów:</span><span class="sxs-lookup"><span data-stu-id="f68f9-213">Later on, after you're done with your tests, you can use the following HPC Pack PowerShell commands to stop and start nodes:</span></span>

```
    Stop-HPCIaaSNode.ps1 -Name <prefix>-00*
    Start-HPCIaaSNode.ps1 -Name <prefix>-00*
```

## <a name="next-steps"></a><span data-ttu-id="f68f9-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f68f9-214">Next steps</span></span>
<span data-ttu-id="f68f9-215">Spróbuj uruchomić inne obciążenia systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f68f9-215">Try running other Linux workloads.</span></span> <span data-ttu-id="f68f9-216">Na przykład zobacz:</span><span class="sxs-lookup"><span data-stu-id="f68f9-216">For example, see:</span></span>

* [<span data-ttu-id="f68f9-217">Uruchamianie NAMD z pakietem Microsoft HPC w węzłach obliczeń systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f68f9-217">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>](hpcpack-cluster-namd.md)
* [<span data-ttu-id="f68f9-218">Uruchom OpenFOAM z pakietem Microsoft HPC w klastrze RDMA systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f68f9-218">Run OpenFOAM with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>](hpcpack-cluster-openfoam.md)

<!--Image references-->
[hndeploy]:media/hpcpack-cluster-starccm/hndeploy.png
[clustermanager]:media/hpcpack-cluster-starccm/ClusterManager.png
