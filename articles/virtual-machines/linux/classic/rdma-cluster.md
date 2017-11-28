---
title: aaaSet zapasowe Linux RDMA klastra toorun MPI aplikacji | Dokumentacja firmy Microsoft
description: Tworzenie klastra rozmiar toouse H16r H16mr, A8 i A9 maszyn wirtualnych systemu Linux hello Azure RDMA sieci toorun MPI aplikacji
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 01834bad-c8e6-48a3-b066-7f1719047dd2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: danlep
ms.openlocfilehash: 3199317a37b095e80718d6724954687d30aea3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-linux-rdma-cluster-toorun-mpi-applications"></a><span data-ttu-id="afe9e-103">Skonfiguruj aplikacje MPI toorun Linux RDMA klastra</span><span class="sxs-lookup"><span data-stu-id="afe9e-103">Set up a Linux RDMA cluster toorun MPI applications</span></span>
<span data-ttu-id="afe9e-104">Dowiedz się, jak klastra tooset się RDMA systemu Linux na platformie Azure z [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun równoległych aplikacji komunikat interfejsu (Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="afe9e-104">Learn how tooset up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toorun parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="afe9e-105">W tym artykule przedstawiono kroki tooprepare toorun obrazu HPC systemu Linux Intel MPI w klastrze.</span><span class="sxs-lookup"><span data-stu-id="afe9e-105">This article provides steps tooprepare a Linux HPC image toorun Intel MPI on a cluster.</span></span> <span data-ttu-id="afe9e-106">Po przygotowaniu można wdrożyć klaster maszyn wirtualnych przy użyciu tego obrazu i jeden rozmiary maszyny Wirtualnej platformy Azure z funkcją RDMA hello (obecnie H16r H16mr, A8 i A9).</span><span class="sxs-lookup"><span data-stu-id="afe9e-106">After preparation, you deploy a cluster of VMs using this image and one of hello RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="afe9e-107">Użyj hello klastra toorun MPI aplikacji, które skutecznie komunikacji za pośrednictwem małe opóźnienia, wysokiej przepustowości sieci na podstawie zdalnego bezpośredniego dostępu do pamięci technologii (RDMA).</span><span class="sxs-lookup"><span data-stu-id="afe9e-107">Use hello cluster toorun MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afe9e-108">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager](../../../resource-manager-deployment-model.md) i klasycznym.</span><span class="sxs-lookup"><span data-stu-id="afe9e-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="afe9e-109">W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="afe9e-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="afe9e-110">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="afe9e-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="afe9e-111">Opcje wdrażania klastra</span><span class="sxs-lookup"><span data-stu-id="afe9e-111">Cluster deployment options</span></span>
<span data-ttu-id="afe9e-112">Poniżej przedstawiono metod toocreate klastra Linux RDMA z lub bez harmonogramu zadań.</span><span class="sxs-lookup"><span data-stu-id="afe9e-112">Following are methods you can use toocreate a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="afe9e-113">**Skrypty interfejsu wiersza polecenia platformy Azure**: jak pokazano w dalszej części tego artykułu, należy użyć hello [interfejsu wiersza polecenia platformy Azure](../../../cli-install-nodejs.md) (CLI) tooscript hello wdrożenia klastra maszyn wirtualnych z funkcją RDMA.</span><span class="sxs-lookup"><span data-stu-id="afe9e-113">**Azure CLI scripts**: As shown later in this article, use hello [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="afe9e-114">Hello interfejsu wiersza polecenia w trybie usługi zarządzania tworzy hello węzły klastra kolejno w hello klasycznego modelu wdrażania, tak wiele węzłów obliczeniowych wdrażanie może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="afe9e-114">hello CLI in Service Management mode creates hello cluster nodes serially in hello classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="afe9e-115">tooenable hello połączenia sieciowego RDMA, gdy używasz hello klasycznego modelu wdrażania, wdrażanie maszyn wirtualnych hello w hello sama usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="afe9e-115">tooenable hello RDMA network connection when you use hello classic deployment model, deploy hello VMs in hello same cloud service.</span></span>
* <span data-ttu-id="afe9e-116">**Szablony usługi Azure Resource Manager**: umożliwia także hello Resource Manager deployment model toodeploy klastra maszyny wirtualne z funkcją RDMA, który łączy sieciowych RDMA toohello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-116">**Azure Resource Manager templates**: You can also use hello Resource Manager deployment model toodeploy a cluster of RDMA-capable VMs that connects toohello RDMA network.</span></span> <span data-ttu-id="afe9e-117">Możesz [utworzyć własny szablon](../../../resource-group-authoring-templates.md), lub sprawdź hello [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/) zamieszczone przez Microsoft lub hello społeczności toodeploy hello rozwiązanie ma szablonów.</span><span class="sxs-lookup"><span data-stu-id="afe9e-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or hello community toodeploy hello solution you want.</span></span> <span data-ttu-id="afe9e-118">Szablony Menedżera zasobów zapewniają toodeploy szybki i niezawodny sposób klaster systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="afe9e-118">Resource Manager templates can provide a fast and reliable way toodeploy a Linux cluster.</span></span> <span data-ttu-id="afe9e-119">Witaj tooenable połączenia sieciowego RDMA, korzystając z modelu wdrażania usługi Resource Manager hello, wdrażanie maszyn wirtualnych hello w hello tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="afe9e-119">tooenable hello RDMA network connection when you use hello Resource Manager deployment model, deploy hello VMs in hello same availability set.</span></span>
* <span data-ttu-id="afe9e-120">**HPC Pack**: Tworzenie klastra Microsoft HPC Pack na platformie Azure i Dodaj węzły obliczeniowe z funkcją RDMA, systemem obsługiwanych Linux tooaccess hello RDMA sieci dystrybucji.</span><span class="sxs-lookup"><span data-stu-id="afe9e-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution tooaccess hello RDMA network.</span></span> <span data-ttu-id="afe9e-121">Aby uzyskać więcej informacji, zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="afe9e-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-hello-classic-model"></a><span data-ttu-id="afe9e-122">Przykładowe wdrożenie kroki w klasycznym modelu hello</span><span class="sxs-lookup"><span data-stu-id="afe9e-122">Sample deployment steps in hello classic model</span></span>
<span data-ttu-id="afe9e-123">Witaj poniższej procedurze pokazano, jak dostosować go toouse hello Azure CLI toodeploy maszyny Wirtualnej HPC z dodatkiem SP1 SUSE Linux Enterprise Server (SLES) 12 z hello Azure Marketplace i utworzyć niestandardowy obraz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afe9e-123">hello following steps show how toouse hello Azure CLI toodeploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from hello Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="afe9e-124">Następnie można użyć wdrożenia hello tooscript obrazu hello klastra maszyn wirtualnych z funkcją RDMA.</span><span class="sxs-lookup"><span data-stu-id="afe9e-124">Then you can use hello image tooscript hello deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="afe9e-125">Użyj podobne kroki toodeploy, klaster maszyn wirtualnych z funkcją RDMA oparta na podstawie CentOS HPC obrazów w hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="afe9e-125">Use similar steps toodeploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in hello Azure Marketplace.</span></span> <span data-ttu-id="afe9e-126">Niektóre kroki różnić się nieznacznie, jak podano.</span><span class="sxs-lookup"><span data-stu-id="afe9e-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="afe9e-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="afe9e-127">Prerequisites</span></span>
* <span data-ttu-id="afe9e-128">**Komputer kliencki**: należy Mac, Linux lub Windows klienta komputera toocommunicate z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afe9e-128">**Client computer**: You need a Mac, Linux, or Windows client computer toocommunicate with Azure.</span></span> <span data-ttu-id="afe9e-129">Tych krokach przyjęto założenie, że używasz klienta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="afe9e-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="afe9e-130">**Subskrypcja platformy Azure**: Jeśli nie masz subskrypcji, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="afe9e-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="afe9e-131">W przypadku dużych klastrów rozważ z subskrypcji lub inne opcje zakupu.</span><span class="sxs-lookup"><span data-stu-id="afe9e-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="afe9e-132">**Dostępność rozmiar maszyny Wirtualnej**: hello po wystąpieniu rozmiary są funkcją RDMA: H16r, H16mr A8 i A9.</span><span class="sxs-lookup"><span data-stu-id="afe9e-132">**VM size availability**: hello following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="afe9e-133">Sprawdź [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/) dostępności w regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afe9e-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="afe9e-134">**Limit przydziału rdzeni**: może być konieczne tooincrease hello przydziału rdzeni toodeploy klastrów obliczeniowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afe9e-134">**Cores quota**: You might need tooincrease hello quota of cores toodeploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="afe9e-135">Na przykład należy co najmniej 128 rdzeni Chcąc VMs A9 toodeploy 8, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="afe9e-135">For example, you need at least 128 cores if you want toodeploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="afe9e-136">Subskrypcji może również ograniczać hello liczba rdzeni, którą można wdrożyć w niektórych rodzin rozmiar maszyny Wirtualnej, włączając hello H-series.</span><span class="sxs-lookup"><span data-stu-id="afe9e-136">Your subscription might also limit hello number of cores you can deploy in certain VM size families, including hello H-series.</span></span> <span data-ttu-id="afe9e-137">Zwiększ limit przydziału toorequest [otwarcia żądania pomocy technicznej online klienta](../../../azure-supportability/how-to-create-azure-support-request.md) bez dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="afe9e-137">toorequest a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="afe9e-138">**Azure CLI**: [zainstalować](../../../cli-install-nodejs.md) hello wiersza polecenia platformy Azure i [połączyć tooyour subskrypcji platformy Azure](../../../xplat-cli-connect.md) z komputera klienckiego hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) hello Azure CLI and [connect tooyour Azure subscription](../../../xplat-cli-connect.md) from hello client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="afe9e-139">Zapewnij SLES 12 SP1 HPC maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="afe9e-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="afe9e-140">Po zalogowaniu się tooAzure z hello wiersza polecenia platformy Azure, uruchom `azure config list` tooconfirm, który hello danych wyjściowych zawiera trybie zarządzania usługami.</span><span class="sxs-lookup"><span data-stu-id="afe9e-140">After signing in tooAzure with hello Azure CLI, run `azure config list` tooconfirm that hello output shows Service Management mode.</span></span> <span data-ttu-id="afe9e-141">Jeśli nie, należy ustawić tryb hello, uruchamiając poniższe polecenie:</span><span class="sxs-lookup"><span data-stu-id="afe9e-141">If it does not, set hello mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="afe9e-142">Wpisz następujące toolist hello wszystkie subskrypcje hello są autoryzowane toouse:</span><span class="sxs-lookup"><span data-stu-id="afe9e-142">Type hello following toolist all hello subscriptions you are authorized toouse:</span></span>

    azure account list

<span data-ttu-id="afe9e-143">bieżącej subskrypcji active Hello jest oznaczone symbolem `Current` ustawić także`true`.</span><span class="sxs-lookup"><span data-stu-id="afe9e-143">hello current active subscription is identified with `Current` set too`true`.</span></span> <span data-ttu-id="afe9e-144">Jeśli ta subskrypcja nie jest hello jeden klaster hello toocreate toouse, Ustaw identyfikator subskrypcji odpowiednie hello jako aktywną subskrypcją hello:</span><span class="sxs-lookup"><span data-stu-id="afe9e-144">If this subscription isn't hello one you want toouse toocreate hello cluster, set hello appropriate subscription ID as hello active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="afe9e-145">toosee hello publicznie dostępnych obrazów SLES 12 SP1 HPC na platformie Azure, uruchom polecenie, takie jak powitania po, zakładając, że obsługuje środowisko z powłoki **grep**:</span><span class="sxs-lookup"><span data-stu-id="afe9e-145">toosee hello publicly available SLES 12 SP1 HPC images in Azure, run a command like hello following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="afe9e-146">Zapewnij z funkcją RDMA maszyny Wirtualnej z obrazu systemu SLES 12 SP1 HPC, uruchamiając polecenie, takie jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="afe9e-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like hello following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="afe9e-147">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="afe9e-147">Where:</span></span>

* <span data-ttu-id="afe9e-148">Witaj rozmiaru (A9 w tym przykładzie) jest jednym z funkcją RDMA hello rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afe9e-148">hello size (A9 in this example) is one of hello RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="afe9e-149">numer Hello do portu zewnętrznego SSH (22 w tym przykładzie jest hello domyślne SSH) jest dowolny prawidłowy numer portu.</span><span class="sxs-lookup"><span data-stu-id="afe9e-149">hello external SSH port number (22 in this example, which is hello SSH default) is any valid port number.</span></span> <span data-ttu-id="afe9e-150">numer portu SSH wewnętrzny Hello ustawiono too22.</span><span class="sxs-lookup"><span data-stu-id="afe9e-150">hello internal SSH port number is set too22.</span></span>
* <span data-ttu-id="afe9e-151">Nową usługę w chmurze jest tworzony w hello określony na podstawie lokalizacji hello region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afe9e-151">A new cloud service is created in hello Azure region specified by hello location.</span></span> <span data-ttu-id="afe9e-152">Określ lokalizację, w których hello maszyny Wirtualnej jest dostępna rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="afe9e-152">Specify a location in which hello VM size you choose is available.</span></span>
* <span data-ttu-id="afe9e-153">Obsługa SUSE priorytet (która wiąże się z dodatkowych opłat) Nazwa obrazu hello SLES 12 SP1 aktualnie może być jedną z tych dwóch opcji:</span><span class="sxs-lookup"><span data-stu-id="afe9e-153">For SUSE priority support (which incurs additional charges), hello SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-hello-vm"></a><span data-ttu-id="afe9e-154">Dostosowywanie hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="afe9e-154">Customize hello VM</span></span>
<span data-ttu-id="afe9e-155">Po zakończeniu inicjowania obsługi administracyjnej hello wirtualna toohello SSH maszyny Wirtualnej za pomocą hello zewnętrzny adres IP maszyny Wirtualnej (lub nazwa DNS) i hello numer portu zewnętrznego skonfigurowany, a następnie dostosować go.</span><span class="sxs-lookup"><span data-stu-id="afe9e-155">After hello VM finishes provisioning, SSH toohello VM by using hello VM's external IP address (or DNS name) and hello external port number you configured, and then customize it.</span></span> <span data-ttu-id="afe9e-156">Aby uzyskać informacje dotyczące połączenia, zobacz [jak toolog na tooa maszyny wirtualnej z systemem Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="afe9e-156">For connection details, see [How toolog on tooa virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="afe9e-157">Przeprowadź polecenia hello użytkownika, którego skonfigurowane na powitania maszyny Wirtualnej, chyba że wymagane toocomplete krokiem jest dostęp do konta root.</span><span class="sxs-lookup"><span data-stu-id="afe9e-157">Perform commands as hello user you configured on hello VM, unless root access is required toocomplete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="afe9e-158">Microsoft Azure nie zapewnia dostęp do konta root tooLinux maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="afe9e-158">Microsoft Azure does not provide root access tooLinux VMs.</span></span> <span data-ttu-id="afe9e-159">dostęp administracyjny toogain podczas połączenia jako toohello użytkownika maszyny Wirtualnej, Uruchom polecenia przy użyciu `sudo`.</span><span class="sxs-lookup"><span data-stu-id="afe9e-159">toogain administrative access when connected as a user toohello VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="afe9e-160">**Aktualizacje**: Zainstaluj aktualizacje za pomocą zypper.</span><span class="sxs-lookup"><span data-stu-id="afe9e-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="afe9e-161">Można także tooinstall narzędzia systemu plików NFS.</span><span class="sxs-lookup"><span data-stu-id="afe9e-161">You might also want tooinstall NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="afe9e-162">SLES 12 SP1 HPC maszynie wirtualnej firma Microsoft zaleca, nie zostaną zastosowane aktualizacje jądra, które mogą powodować problemy hello Linux RDMA sterowniki.</span><span class="sxs-lookup"><span data-stu-id="afe9e-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with hello Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="afe9e-163">**Intel MPI**: ukończy instalację hello Intel MPI na powitania wirtualna HPC systemu SLES 12 z dodatkiem SP1, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="afe9e-163">**Intel MPI**: Complete hello installation of Intel MPI on hello SLES 12 SP1 HPC VM by running hello following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="afe9e-164">**Zablokować pamięci**: MPI kody toolock hello pamięci dostępnej dla funkcji RDMA, dodać lub zmienić hello następujące ustawienia w pliku /etc/security/limits.conf hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-164">**Lock memory**: For MPI codes toolock hello memory available for RDMA, add or change hello following settings in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="afe9e-165">Należy głównego tooedit dostępu do tego pliku.</span><span class="sxs-lookup"><span data-stu-id="afe9e-165">You need root access tooedit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="afe9e-166">Do celów testowych można również ustawić memlock toounlimited.</span><span class="sxs-lookup"><span data-stu-id="afe9e-166">For testing purposes, you can also set memlock toounlimited.</span></span> <span data-ttu-id="afe9e-167">Na przykład: `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="afe9e-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="afe9e-168">Aby uzyskać więcej informacji, zobacz [znaną metody ustawienie zablokowane rozmiar pamięci](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="afe9e-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="afe9e-169">**Klucze SSH dla maszyn wirtualnych SLES**: generowanie SSH klucze tooestablish zaufania dla tego konta użytkownika między hello obliczeniowe węzłów w klastrze SLES hello podczas uruchamiania zadań MPI.</span><span class="sxs-lookup"><span data-stu-id="afe9e-169">**SSH keys for SLES VMs**: Generate SSH keys tooestablish trust for your user account among hello compute nodes in hello SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="afe9e-170">Jeśli wdrożono maszynę Wirtualną na podstawie CentOS HPC, nie należy wykonać ten krok.</span><span class="sxs-lookup"><span data-stu-id="afe9e-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="afe9e-171">Zobacz instrukcje w dalszej części tego artykułu tooset passwordless SSH relacji zaufania między węzłami klastra powitania po przechwyceniu hello obrazu i wdrożenie klastra hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-171">See instructions later in this article tooset up passwordless SSH trust among hello cluster nodes after you capture hello image and deploy hello cluster.</span></span>

    <span data-ttu-id="afe9e-172">kluczy SSH toocreate, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-172">toocreate SSH keys, run hello following command.</span></span> <span data-ttu-id="afe9e-173">Po wyświetleniu monitu o wprowadzenie danych, wybierz **Enter** toogenerate hello kluczy w lokalizacji domyślnej hello bez ustawienia hasła.</span><span class="sxs-lookup"><span data-stu-id="afe9e-173">When you are prompted for input, select **Enter** toogenerate hello keys in hello default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="afe9e-174">Dołącz plik authorized_keys toohello klucza publicznego hello znane kluczy publicznych.</span><span class="sxs-lookup"><span data-stu-id="afe9e-174">Append hello public key toohello authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="afe9e-175">W katalogu ~/.ssh hello Edytuj lub Utwórz hello pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="afe9e-175">In hello ~/.ssh directory, edit or create hello config file.</span></span> <span data-ttu-id="afe9e-176">Podaj zakres adresów IP hello hello sieci prywatnej czy planujesz toouse na platformie Azure (10.32.0.0/16 w tym przykładzie):</span><span class="sxs-lookup"><span data-stu-id="afe9e-176">Provide hello IP address range of hello private network that you plan toouse in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="afe9e-177">Alternatywnie listy adres IP sieci prywatnej hello każdej maszyny Wirtualnej w klastrze w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="afe9e-177">Alternatively, list hello private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="afe9e-178">Konfigurowanie `StrictHostKeyChecking no` można utworzyć potencjalne zagrożenie dla bezpieczeństwa, jeśli nie określono określonego adresu IP lub zakresu.</span><span class="sxs-lookup"><span data-stu-id="afe9e-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="afe9e-179">**Aplikacje**: Zainstaluj wszystkie aplikacje muszą lub wykonywać inne dostosowania, przed przechwyceniem obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-179">**Applications**: Install any applications you need or perform other customizations before you capture hello image.</span></span>

### <a name="capture-hello-image"></a><span data-ttu-id="afe9e-180">Przechwyć obraz powitania</span><span class="sxs-lookup"><span data-stu-id="afe9e-180">Capture hello image</span></span>
<span data-ttu-id="afe9e-181">Obraz powitania toocapture, najpierw uruchom następujące polecenie na powitania maszyny Wirtualnej systemu Linux hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-181">toocapture hello image, first run hello following command on hello Linux VM.</span></span> <span data-ttu-id="afe9e-182">To polecenie deprovisions hello maszyny Wirtualnej, ale przechowuje konta użytkowników i kluczy SSH, które zostały zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="afe9e-182">This command deprovisions hello VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="afe9e-183">Z komputera klienta Uruchom powitania po obraz powitania toocapture polecenia wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afe9e-183">From your client computer, run hello following Azure CLI commands toocapture hello image.</span></span> <span data-ttu-id="afe9e-184">Aby uzyskać więcej informacji, zobacz [jak toocapture klasyczne maszyny wirtualnej systemu Linux jako obrazu](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="afe9e-184">For more information, see [How toocapture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="afe9e-185">Po uruchomieniu tych poleceń hello obrazu maszyny Wirtualnej są przechwytywane do użycia i hello maszyna wirtualna zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="afe9e-185">After you run these commands, hello VM image is captured for your use and hello VM is deleted.</span></span> <span data-ttu-id="afe9e-186">Teraz masz z niestandardowego obrazu toodeploy gotowy klaster.</span><span class="sxs-lookup"><span data-stu-id="afe9e-186">Now you have your custom image ready toodeploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-hello-image"></a><span data-ttu-id="afe9e-187">Wdrażanie klastra z obrazem hello</span><span class="sxs-lookup"><span data-stu-id="afe9e-187">Deploy a cluster with hello image</span></span>
<span data-ttu-id="afe9e-188">Modyfikowanie hello następującego skryptu Bash z odpowiednimi wartościami dla środowiska i uruchom go z komputera klienckiego.</span><span class="sxs-lookup"><span data-stu-id="afe9e-188">Modify hello following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="afe9e-189">Ponieważ Azure wdraża hello maszyn wirtualnych, pojedynczo w hello klasycznego modelu wdrażania, zajmuje kilka minut toodeploy hello osiem A9 maszyn wirtualnych sugerowane w tym skrypcie.</span><span class="sxs-lookup"><span data-stu-id="afe9e-189">Because Azure deploys hello VMs serially in hello classic deployment model, it takes a few minutes toodeploy hello eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script toocreate a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where hello VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All hello compute-intensive instances need toobe in hello same cloud service for Linux RDMA toowork across InfiniBand.
# Note: hello current maximum number of VMs in a cloud service is 50. If you need tooprovision more than 50 VMs in hello same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want tooturn off external ports and use only internal ports toocommunicate between compute nodes via port 22, don’t use this option. Since port numbers up too10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 toocluster18. Specify your captured image in <image-name>. Specify hello username and password you used when creating hello SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment tooprovision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="afe9e-190">Zagadnienia dotyczące klastra CentOS HPC</span><span class="sxs-lookup"><span data-stu-id="afe9e-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="afe9e-191">Tooset zapasowej klastra na podstawie jednej z obrazów na podstawie CentOS HPC hello w hello Azure Marketplace zamiast SLES 12 dla HPC, należy wykonać czynności ogólne hello w powyższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-191">If you want tooset up a cluster based on one of hello CentOS-based HPC images in hello Azure Marketplace instead of SLES 12 for HPC, follow hello general steps in hello preceding section.</span></span> <span data-ttu-id="afe9e-192">Należy zwrócić uwagę hello następujące różnice, podczas udostępniania i konfigurowania hello maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="afe9e-192">Note hello following differences when you provision and configure hello VM:</span></span>

- <span data-ttu-id="afe9e-193">Intel MPI jest już zainstalowana na maszynie Wirtualnej z obrazu na podstawie CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="afe9e-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="afe9e-194">Ustawienia pamięci blokady są już dodana w pliku /etc/security/limits.conf hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="afe9e-194">Lock memory settings are already added in hello VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="afe9e-195">Generuje klucze SSH na powitania udostępnieniem maszyny Wirtualnej do przechwycenia.</span><span class="sxs-lookup"><span data-stu-id="afe9e-195">Do not generate SSH keys on hello VM you provision for capture.</span></span> <span data-ttu-id="afe9e-196">Zamiast tego zaleca się skonfigurowanie uwierzytelniania użytkownika po wdrożeniu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-196">Instead, we recommend setting up user-based authentication after you deploy hello cluster.</span></span> <span data-ttu-id="afe9e-197">Aby uzyskać więcej informacji zobacz hello następujących sekcji.</span><span class="sxs-lookup"><span data-stu-id="afe9e-197">For more information, see hello following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-hello-cluster"></a><span data-ttu-id="afe9e-198">Konfigurowanie passwordless zaufania SSH w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="afe9e-198">Set up passwordless SSH trust on hello cluster</span></span>
<span data-ttu-id="afe9e-199">W klastrze HPC na podstawie CentOS, istnieją dwie metody do ustanawiania relacji zaufania między węzłami obliczeniowymi hello: uwierzytelnianie oparte na hoście i uwierzytelnianie oparte na użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="afe9e-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between hello compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="afe9e-200">Uwierzytelnianie oparte na hoście wykracza poza zakres tego artykułu hello i zazwyczaj muszą być wykonywane przez rozszerzenia skryptów podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="afe9e-200">Host-based authentication is outside of hello scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="afe9e-201">Uwierzytelnianie użytkownika jest wygodną metodą ustanawiania relacji zaufania po wdrożeniu i wymaga generowania hello i udostępniania kluczy SSH między hello obliczeniowe węzłów w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-201">User-based authentication is convenient for establishing trust after deployment and requires hello generation and sharing of SSH keys among hello compute nodes in hello cluster.</span></span> <span data-ttu-id="afe9e-202">Ta metoda jest często nazywana passwordless logowania SSH i jest wymagany w przypadku uruchamiania zadań MPI.</span><span class="sxs-lookup"><span data-stu-id="afe9e-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="afe9e-203">Przykładowy skrypt przyczyniły się od społeczności hello jest dostępna w [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable łatwe użytkownika uwierzytelniania w klastrze HPC na podstawie CentOS.</span><span class="sxs-lookup"><span data-stu-id="afe9e-203">A sample script contributed from hello community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) tooenable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="afe9e-204">Pobranie i użycie tego skryptu za pomocą hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="afe9e-204">Download and use this script by using hello following steps.</span></span> <span data-ttu-id="afe9e-205">Można również zmodyfikować tego skryptu lub użyć inne metody tooestablish passwordless SSH uwierzytelniania między węzły obliczeń hello klastra.</span><span class="sxs-lookup"><span data-stu-id="afe9e-205">You can also modify this script or use any other method tooestablish passwordless SSH authentication between hello cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="afe9e-206">skrypt hello toorun, należy tooknow hello prefiks dla podsieci adresów IP.</span><span class="sxs-lookup"><span data-stu-id="afe9e-206">toorun hello script, you need tooknow hello prefix for your subnet IP addresses.</span></span> <span data-ttu-id="afe9e-207">Pobierz hello prefiksu, uruchamiając następujące polecenie w jednym z węzłów klastra hello hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-207">Get hello prefix by running hello following command on one of hello cluster nodes.</span></span> <span data-ttu-id="afe9e-208">Dane wyjściowe powinny wyglądać podobnie 10.1.3.5 i prefiks hello jest hello 10.1.3 części.</span><span class="sxs-lookup"><span data-stu-id="afe9e-208">Your output should look something like 10.1.3.5, and hello prefix is hello 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="afe9e-209">Teraz uruchom skrypt hello przy użyciu trzech parametrów: Nazwa pospolita użytkownika hello na powitania węzły obliczeniowe, hello wspólne hasło dla tego użytkownika na powitania węzły obliczeniowe i prefiksu podsieci hello, który został zwrócony z hello poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="afe9e-209">Now run hello script using three parameters: hello common user name on hello compute nodes, hello common password for that user on hello compute nodes, and hello subnet prefix that was returned from hello previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="afe9e-210">Ten skrypt hello następujące:</span><span class="sxs-lookup"><span data-stu-id="afe9e-210">This script does hello following:</span></span>

* <span data-ttu-id="afe9e-211">Tworzy katalog na powitania węzła hosta o nazwie .ssh, co jest niezbędne do logowania passwordless.</span><span class="sxs-lookup"><span data-stu-id="afe9e-211">Creates a directory on hello host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="afe9e-212">Tworzy plik konfiguracji w katalogu .ssh hello, która sprawia, że logowanie tooallow passwordless logowania z dowolnego węzła w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-212">Creates a configuration file in hello .ssh directory that instructs passwordless login tooallow login from any node in hello cluster.</span></span>
* <span data-ttu-id="afe9e-213">Tworzy pliki zawierające hello nazwy węzła i węzła adresów IP dla wszystkich węzłów hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="afe9e-213">Creates files containing hello node names and node IP addresses for all hello nodes in hello cluster.</span></span> <span data-ttu-id="afe9e-214">Te pliki są pozostawiane po uruchomieniu skryptu hello do wykorzystania w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="afe9e-214">These files are left after hello script is run for later reference.</span></span>
* <span data-ttu-id="afe9e-215">Tworzy prywatne i publiczne pary kluczy dla każdego węzła klastra (w tym hello węzła hosta) oraz wpisy w pliku authorized_keys hello.</span><span class="sxs-lookup"><span data-stu-id="afe9e-215">Creates a private and public key pair for each cluster node (including hello host node) and creates entries in hello authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="afe9e-216">Uruchomienie tego skryptu można utworzyć potencjalne zagrożenie dla bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="afe9e-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="afe9e-217">Upewnij się, że hello informacje o kluczu publicznym w ~/.ssh nie będzie on rozpowszechniany.</span><span class="sxs-lookup"><span data-stu-id="afe9e-217">Ensure that hello public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="afe9e-218">Skonfiguruj Intel MPI</span><span class="sxs-lookup"><span data-stu-id="afe9e-218">Configure Intel MPI</span></span>
<span data-ttu-id="afe9e-219">aplikacje MPI toorun na RDMA systemu Linux platformy Azure, należy tooconfigure niektórych tooIntel określonych zmiennych MPI środowiska.</span><span class="sxs-lookup"><span data-stu-id="afe9e-219">toorun MPI applications on Azure Linux RDMA, you need tooconfigure certain environment variables specific tooIntel MPI.</span></span> <span data-ttu-id="afe9e-220">Oto przykładowe Bash skryptu tooconfigure hello zmienne potrzebne toorun aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afe9e-220">Here is a sample Bash script tooconfigure hello variables needed toorun an application.</span></span> <span data-ttu-id="afe9e-221">Zmień hello toompivars.sh ścieżki instalacji programu Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="afe9e-221">Change hello path toompivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting hello variable tooshm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line toorun hello job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path toohello application exe> <arguments specific toohello application>

#end
```

<span data-ttu-id="afe9e-222">Witaj format pliku hosta hello ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="afe9e-222">hello format of hello host file is as follows.</span></span> <span data-ttu-id="afe9e-223">Dodaj jeden wiersz dla każdego węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="afe9e-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="afe9e-224">Określ prywatnych adresów IP z sieci wirtualnej hello nie zostały zdefiniowane wcześniej, a nie nazw DNS.</span><span class="sxs-lookup"><span data-stu-id="afe9e-224">Specify private IP addresses from hello virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="afe9e-225">Na przykład dla dwa hosty z adresami IP 10.32.0.1 i 10.32.0.2 hello plik zawiera następujące hello:</span><span class="sxs-lookup"><span data-stu-id="afe9e-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, hello file contains hello following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="afe9e-226">Uruchom MPI na podstawowe dwa węzły klastra</span><span class="sxs-lookup"><span data-stu-id="afe9e-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="afe9e-227">Jeśli jeszcze tego nie zrobiono, najpierw skonfigurować środowisko hello do Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="afe9e-227">If you haven't already done so, first set up hello environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="afe9e-228">Uruchom polecenie MPI</span><span class="sxs-lookup"><span data-stu-id="afe9e-228">Run an MPI command</span></span>
<span data-ttu-id="afe9e-229">Uruchom polecenie MPI na jednym z hello tooshow węzły obliczeniowe, MPI jest poprawnie zainstalowany i może komunikować się między co najmniej dwóch węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="afe9e-229">Run an MPI command on one of hello compute nodes tooshow that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="afe9e-230">następujące Hello **mpirun** polecenia uruchamiane hello **hostname** na dwa węzły.</span><span class="sxs-lookup"><span data-stu-id="afe9e-230">hello following **mpirun** command runs hello **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="afe9e-231">Dane wyjściowe powinny zawierać nazw hello wszystkich węzłów hello, które przekazany jako dane wejściowe dla `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="afe9e-231">Your output should list hello names of all hello nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="afe9e-232">Na przykład **mpirun** polecenie z dwoma węzłami zwraca dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="afe9e-232">For example, an **mpirun** command with two nodes returns output like hello following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="afe9e-233">Uruchamianie testów porównawczych MPI</span><span class="sxs-lookup"><span data-stu-id="afe9e-233">Run an MPI benchmark</span></span>
<span data-ttu-id="afe9e-234">następujące polecenie Intel MPI Hello uruchamia pingpong testu porównawczego tooverify hello konfiguracji i połączeń toohello RDMA sieć klastra.</span><span class="sxs-lookup"><span data-stu-id="afe9e-234">hello following Intel MPI command runs a pingpong benchmark tooverify hello cluster configuration and connection toohello RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="afe9e-235">Powinny zostać wyświetlone dane wyjściowe podobne do następujących hello w klastrze pracy z dwoma węzłami.</span><span class="sxs-lookup"><span data-stu-id="afe9e-235">On a working cluster with two nodes, you should see output like hello following.</span></span> <span data-ttu-id="afe9e-236">W sieci Azure RDMA hello oczekiwany czas oczekiwania na poziomie lub poniżej 3 mikrosekundach dla rozmiary wiadomości w górę too512 bajtów.</span><span class="sxs-lookup"><span data-stu-id="afe9e-236">On hello Azure RDMA network, expect latency at or below 3 microseconds for message sizes up too512 bytes.</span></span>

```
#------------------------------------------------------------
#    Intel (R) MPI Benchmarks 4.0 Update 1, MPI-1 part
#------------------------------------------------------------
# Date                  : Fri Jul 17 23:16:46 2015
# Machine               : x86_64
# System                : Linux
# Release               : 3.12.39-44-default
# Version               : #5 SMP Thu Jun 25 22:45:24 UTC 2015
# MPI Version           : 3.0
# MPI Thread Environment:
# New default behavior from Version 3.2 on:
# hello number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected toobe exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through hello flag => -time

# Calling sequence was:
# /opt/intel/impi_latest/bin64/IMB-MPI1 pingpong
# Minimum message length in bytes:   0
# Maximum message length in bytes:   4194304
#
# MPI_Datatype                   :   MPI_BYTE
# MPI_Datatype for reductions    :   MPI_FLOAT
# MPI_Op                         :   MPI_SUM
#
#
# List of Benchmarks toorun:
# PingPong
#---------------------------------------------------
# Benchmarking PingPong
# #processes = 2
#---------------------------------------------------
       #bytes #repetitions      t[usec]   Mbytes/sec
            0         1000         2.23         0.00
            1         1000         2.26         0.42
            2         1000         2.26         0.85
            4         1000         2.26         1.69
            8         1000         2.26         3.38
           16         1000         2.36         6.45
           32         1000         2.57        11.89
           64         1000         2.36        25.81
          128         1000         2.64        46.19
          256         1000         2.73        89.30
          512         1000         3.09       157.99
         1024         1000         3.60       271.53
         2048         1000         4.46       437.57
         4096         1000         6.11       639.23
         8192         1000         7.49      1043.47
        16384         1000         9.76      1600.76
        32768         1000        14.98      2085.77
        65536          640        25.99      2405.08
       131072          320        50.68      2466.64
       262144          160        80.62      3101.01
       524288           80       145.86      3427.91
      1048576           40       279.06      3583.42
      2097152           20       543.37      3680.71
      4194304           10      1082.94      3693.63

# All processes entering MPI_Finalize

```



## <a name="next-steps"></a><span data-ttu-id="afe9e-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="afe9e-237">Next steps</span></span>
* <span data-ttu-id="afe9e-238">Wdrażanie i uruchamianie sieci MPI Linux aplikacji w klastrze systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="afe9e-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="afe9e-239">Zobacz hello [dokumentację biblioteki MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) wskazówki dotyczące Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="afe9e-239">See hello [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="afe9e-240">Spróbuj [szablon szybkiego startu](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate połysk Intel klastra przy użyciu obrazu na podstawie CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="afe9e-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) toocreate an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="afe9e-241">Aby uzyskać więcej informacji, zobacz [wdrażanie Intel chmury Edition dla połysk w systemie Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="afe9e-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
