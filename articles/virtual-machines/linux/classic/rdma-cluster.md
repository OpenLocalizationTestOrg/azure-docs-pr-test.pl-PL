---
title: Konfigurowanie klastra Linux RDMA na uruchamianie aplikacji MPI | Dokumentacja firmy Microsoft
description: "Tworzenie klastra Linux rozmiaru H16r H16mr, A8 i A9 maszyn wirtualnych do używania w sieci Azure RDMA do uruchamiania aplikacji MPI"
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
ms.openlocfilehash: 4b2ceb64b1737918458f6d5c692fc2bfbc0f12ed
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-a-linux-rdma-cluster-to-run-mpi-applications"></a><span data-ttu-id="9cade-103">Konfigurowanie klastra RDMA systemu Linux na potrzeby uruchamiania aplikacji MPI</span><span class="sxs-lookup"><span data-stu-id="9cade-103">Set up a Linux RDMA cluster to run MPI applications</span></span>
<span data-ttu-id="9cade-104">Dowiedz się, jak skonfigurować klaster RDMA systemu Linux na platformie Azure z [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) na uruchamianie równoległe aplikacji komunikat interfejsu (Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="9cade-104">Learn how to set up a Linux RDMA cluster in Azure with [High performance compute VM sizes](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to run parallel Message Passing Interface (MPI) applications.</span></span> <span data-ttu-id="9cade-105">Ten artykuł zawiera kroki, aby przygotować obraz HPC systemu Linux, aby uruchomić Intel MPI w klastrze.</span><span class="sxs-lookup"><span data-stu-id="9cade-105">This article provides steps to prepare a Linux HPC image to run Intel MPI on a cluster.</span></span> <span data-ttu-id="9cade-106">Po przygotowaniu można wdrożyć klaster maszyn wirtualnych przy użyciu tego obrazu i jeden rozmiary maszyny Wirtualnej platformy Azure z funkcją RDMA (obecnie H16r H16mr, A8 i A9).</span><span class="sxs-lookup"><span data-stu-id="9cade-106">After preparation, you deploy a cluster of VMs using this image and one of the RDMA-capable Azure VM sizes (currently H16r, H16mr, A8, or A9).</span></span> <span data-ttu-id="9cade-107">Klaster umożliwia uruchamianie aplikacji MPI wydajne komunikowanie się przez sieć małym opóźnieniu i dużej przepustowości oparte na technologii dostępu (do pamięci RDMA) zdalnego pamięci.</span><span class="sxs-lookup"><span data-stu-id="9cade-107">Use the cluster to run MPI applications that communicate efficiently over a low-latency, high-throughput network based on remote direct memory access (RDMA) technology.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cade-108">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager](../../../resource-manager-deployment-model.md) i klasycznym.</span><span class="sxs-lookup"><span data-stu-id="9cade-108">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="9cade-109">Ten artykuł dotyczy klasycznego modelu wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="9cade-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="9cade-110">Firma Microsoft zaleca, aby w przypadku większości nowych wdrożeń korzystać z modelu opartego na programie Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9cade-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

## <a name="cluster-deployment-options"></a><span data-ttu-id="9cade-111">Opcje wdrażania klastra</span><span class="sxs-lookup"><span data-stu-id="9cade-111">Cluster deployment options</span></span>
<span data-ttu-id="9cade-112">Poniżej przedstawiono metody można użyć do utworzenia klastra Linux RDMA z lub bez harmonogramu zadań.</span><span class="sxs-lookup"><span data-stu-id="9cade-112">Following are methods you can use to create a Linux RDMA cluster with or without a job scheduler.</span></span>

* <span data-ttu-id="9cade-113">**Skrypty interfejsu wiersza polecenia platformy Azure**: jak pokazano w dalszej części tego artykułu, użyj [interfejsu wiersza polecenia platformy Azure](../../../cli-install-nodejs.md) (CLI) do skryptu wdrażania klastra maszyn wirtualnych z funkcją RDMA.</span><span class="sxs-lookup"><span data-stu-id="9cade-113">**Azure CLI scripts**: As shown later in this article, use the [Azure command-line interface](../../../cli-install-nodejs.md) (CLI) to script the deployment of a cluster of RDMA-capable VMs.</span></span> <span data-ttu-id="9cade-114">Interfejsu wiersza polecenia w trybie zarządzania usługami tworzy węzłów klastra szeregowo w klasycznym modelu wdrożenia, więc wdrażania wielu węzłów obliczeniowych może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="9cade-114">The CLI in Service Management mode creates the cluster nodes serially in the classic deployment model, so deploying many compute nodes might take several minutes.</span></span> <span data-ttu-id="9cade-115">Aby włączyć połączenia sieciowego RDMA, korzystając z klasycznym modelu wdrożenia, należy wdrożyć maszyn wirtualnych w tej samej usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="9cade-115">To enable the RDMA network connection when you use the classic deployment model, deploy the VMs in the same cloud service.</span></span>
* <span data-ttu-id="9cade-116">**Szablony usługi Azure Resource Manager**: umożliwia także modelu wdrażania usługi Resource Manager można wdrożyć klaster maszyn wirtualnych z funkcją RDMA, który łączy się z siecią RDMA.</span><span class="sxs-lookup"><span data-stu-id="9cade-116">**Azure Resource Manager templates**: You can also use the Resource Manager deployment model to deploy a cluster of RDMA-capable VMs that connects to the RDMA network.</span></span> <span data-ttu-id="9cade-117">Możesz [utworzyć własny szablon](../../../resource-group-authoring-templates.md), lub sprawdź [szablonów Szybki Start Azure](https://azure.microsoft.com/documentation/templates/) zamieszczone przez firmę Microsoft lub społeczności, aby wdrożyć rozwiązanie ma szablonów.</span><span class="sxs-lookup"><span data-stu-id="9cade-117">You can [create your own template](../../../resource-group-authoring-templates.md), or check the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/) for templates contributed by Microsoft or the community to deploy the solution you want.</span></span> <span data-ttu-id="9cade-118">Szablony Menedżera zasobów zapewniają szybki i niezawodny sposób wdrożyć klaster systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9cade-118">Resource Manager templates can provide a fast and reliable way to deploy a Linux cluster.</span></span> <span data-ttu-id="9cade-119">Aby włączyć połączenia sieciowego RDMA, korzystając z modelu wdrażania usługi Resource Manager, należy wdrożyć maszyn wirtualnych w tym samym zestawie dostępności.</span><span class="sxs-lookup"><span data-stu-id="9cade-119">To enable the RDMA network connection when you use the Resource Manager deployment model, deploy the VMs in the same availability set.</span></span>
* <span data-ttu-id="9cade-120">**HPC Pack**: Tworzenie klastra Microsoft HPC Pack na platformie Azure i Dodaj węzły obliczeniowe z funkcją RDMA, systemem obsługiwanych dystrybucji systemu Linux na dostęp do sieci RDMA.</span><span class="sxs-lookup"><span data-stu-id="9cade-120">**HPC Pack**: Create a Microsoft HPC Pack cluster in Azure and add RDMA-capable compute nodes that run a supported Linux distribution to access the RDMA network.</span></span> <span data-ttu-id="9cade-121">Aby uzyskać więcej informacji, zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="9cade-121">For more information, see [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md).</span></span>

## <a name="sample-deployment-steps-in-the-classic-model"></a><span data-ttu-id="9cade-122">Przykładowe wdrożenie kroki w klasycznym modelu.</span><span class="sxs-lookup"><span data-stu-id="9cade-122">Sample deployment steps in the classic model</span></span>
<span data-ttu-id="9cade-123">Poniższe kroki pokazują, jak wdrożyć maszynę Wirtualną HPC z dodatkiem SP1 SUSE Linux Enterprise Server (SLES) 12 z portalu Azure Marketplace, dostosować go i utworzyć niestandardowy obraz maszyny Wirtualnej za pomocą wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cade-123">The following steps show how to use the Azure CLI to deploy a SUSE Linux Enterprise Server (SLES) 12 SP1 HPC VM from the Azure Marketplace, customize it, and create a custom VM image.</span></span> <span data-ttu-id="9cade-124">Następnie można użyć obrazu do skryptu wdrażania klastra maszyn wirtualnych z funkcją RDMA.</span><span class="sxs-lookup"><span data-stu-id="9cade-124">Then you can use the image to script the deployment of a cluster of RDMA-capable VMs.</span></span>

> [!TIP]
> <span data-ttu-id="9cade-125">Podobne kroki umożliwiają wdrożenie klastra maszyn wirtualnych z funkcją RDMA, oparte na podstawie CentOS HPC obrazów w portalu Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="9cade-125">Use similar steps to deploy a cluster of RDMA-capable VMs based on CentOS-based HPC images in the Azure Marketplace.</span></span> <span data-ttu-id="9cade-126">Niektóre kroki różnić się nieznacznie, jak podano.</span><span class="sxs-lookup"><span data-stu-id="9cade-126">Some steps differ slightly, as noted.</span></span> 
>
>

### <a name="prerequisites"></a><span data-ttu-id="9cade-127">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9cade-127">Prerequisites</span></span>
* <span data-ttu-id="9cade-128">**Komputer kliencki**: wymagany jest komputer klienta Mac, Linux lub Windows do komunikowania się z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="9cade-128">**Client computer**: You need a Mac, Linux, or Windows client computer to communicate with Azure.</span></span> <span data-ttu-id="9cade-129">Tych krokach przyjęto założenie, że używasz klienta systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9cade-129">These steps assume you are using a Linux client.</span></span>
* <span data-ttu-id="9cade-130">**Subskrypcja platformy Azure**: Jeśli nie masz subskrypcji, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="9cade-130">**Azure subscription**: If you don't have a subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span> <span data-ttu-id="9cade-131">W przypadku dużych klastrów rozważ z subskrypcji lub inne opcje zakupu.</span><span class="sxs-lookup"><span data-stu-id="9cade-131">For larger clusters, consider a pay-as-you-go subscription or other purchase options.</span></span>
* <span data-ttu-id="9cade-132">**Dostępność rozmiar maszyny Wirtualnej**: następujące rozmiary wystąpienia są funkcją RDMA: H16r, H16mr A8 i A9.</span><span class="sxs-lookup"><span data-stu-id="9cade-132">**VM size availability**: The following instance sizes are RDMA capable: H16r, H16mr, A8, and A9.</span></span> <span data-ttu-id="9cade-133">Sprawdź [produkty, które są dostępne w regionie](https://azure.microsoft.com/regions/services/) dostępności w regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9cade-133">Check [Products available by region](https://azure.microsoft.com/regions/services/) for availability in Azure regions.</span></span>
* <span data-ttu-id="9cade-134">**Limit przydziału rdzeni**: może być konieczne zwiększyć limit przydziału rdzeni do wdrożenia klastrów obliczeniowych maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="9cade-134">**Cores quota**: You might need to increase the quota of cores to deploy a cluster of compute-intensive VMs.</span></span> <span data-ttu-id="9cade-135">Na przykład należy co najmniej 128 rdzeni. Jeśli chcesz wdrożyć 8 A9 maszyn wirtualnych, jak pokazano w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="9cade-135">For example, you need at least 128 cores if you want to deploy 8 A9 VMs as shown in this article.</span></span> <span data-ttu-id="9cade-136">Subskrypcją również może ograniczyć liczbę rdzeni, którą można wdrożyć w niektórych rodzin rozmiar maszyny Wirtualnej, w tym serię H.</span><span class="sxs-lookup"><span data-stu-id="9cade-136">Your subscription might also limit the number of cores you can deploy in certain VM size families, including the H-series.</span></span> <span data-ttu-id="9cade-137">Aby zażądać zwiększenia limitu przydziału [otwarcia żądania pomocy technicznej online klienta](../../../azure-supportability/how-to-create-azure-support-request.md) bez dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="9cade-137">To request a quota increase, [open an online customer support request](../../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
* <span data-ttu-id="9cade-138">**Azure CLI**: [zainstalować](../../../cli-install-nodejs.md) wiersza polecenia platformy Azure i [nawiązać połączenia z subskrypcją platformy Azure](../../../xplat-cli-connect.md) z komputera klienckiego.</span><span class="sxs-lookup"><span data-stu-id="9cade-138">**Azure CLI**: [Install](../../../cli-install-nodejs.md) the Azure CLI and [connect to your Azure subscription](../../../xplat-cli-connect.md) from the client computer.</span></span>

### <a name="provision-an-sles-12-sp1-hpc-vm"></a><span data-ttu-id="9cade-139">Zapewnij SLES 12 SP1 HPC maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9cade-139">Provision an SLES 12 SP1 HPC VM</span></span>
<span data-ttu-id="9cade-140">Po zalogowaniu się na platformie Azure przy użyciu wiersza polecenia platformy Azure, uruchom `azure config list` aby upewnić się, że dane wyjściowe zawierają tryb usługi zarządzania.</span><span class="sxs-lookup"><span data-stu-id="9cade-140">After signing in to Azure with the Azure CLI, run `azure config list` to confirm that the output shows Service Management mode.</span></span> <span data-ttu-id="9cade-141">Jeśli nie, należy ustawić tryb uruchamiając poniższe polecenie:</span><span class="sxs-lookup"><span data-stu-id="9cade-141">If it does not, set the mode by running this command:</span></span>

    azure config mode asm


<span data-ttu-id="9cade-142">Wpisz następujące polecenie, aby wyświetlić wszystkie subskrypcje, które są autoryzowane do używania:</span><span class="sxs-lookup"><span data-stu-id="9cade-142">Type the following to list all the subscriptions you are authorized to use:</span></span>

    azure account list

<span data-ttu-id="9cade-143">Jest identyfikowane bieżącej subskrypcji active `Current` ustawioną `true`.</span><span class="sxs-lookup"><span data-stu-id="9cade-143">The current active subscription is identified with `Current` set to `true`.</span></span> <span data-ttu-id="9cade-144">Jeśli ta subskrypcja nie jest ten, który ma być używany do tworzenia klastra, Ustaw identyfikator subskrypcji odpowiednie jako aktywną subskrypcją:</span><span class="sxs-lookup"><span data-stu-id="9cade-144">If this subscription isn't the one you want to use to create the cluster, set the appropriate subscription ID as the active subscription:</span></span>

    azure account set <subscription-Id>

<span data-ttu-id="9cade-145">Aby wyświetlić publicznie dostępnych obrazów SLES 12 SP1 HPC na platformie Azure, uruchom polecenie podobne do poniższych, zakładając, że obsługuje środowisko z powłoki **grep**:</span><span class="sxs-lookup"><span data-stu-id="9cade-145">To see the publicly available SLES 12 SP1 HPC images in Azure, run a command like the following, assuming your shell environment supports **grep**:</span></span>

    azure vm image list | grep "suse.*hpc"

<span data-ttu-id="9cade-146">Zapewnij z funkcją RDMA maszyny Wirtualnej z obrazu systemu SLES 12 SP1 HPC, uruchamiając polecenie podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="9cade-146">Provision an RDMA-capable VM with a SLES 12 SP1 HPC image by running a command like the following:</span></span>

    azure vm create -g <username> -p <password> -c <cloud-service-name> -l <location> -z A9 -n <vm-name> -e 22 b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824

<span data-ttu-id="9cade-147">Gdzie:</span><span class="sxs-lookup"><span data-stu-id="9cade-147">Where:</span></span>

* <span data-ttu-id="9cade-148">Rozmiar (A9 w tym przykładzie) jest jednym z rozmiary maszyny Wirtualnej z funkcją RDMA.</span><span class="sxs-lookup"><span data-stu-id="9cade-148">The size (A9 in this example) is one of the RDMA-capable VM sizes.</span></span>
* <span data-ttu-id="9cade-149">Zewnętrzny numer portu SSH (22 w tym przykładzie, która jest domyślnie SSH) jest dowolny prawidłowy numer portu.</span><span class="sxs-lookup"><span data-stu-id="9cade-149">The external SSH port number (22 in this example, which is the SSH default) is any valid port number.</span></span> <span data-ttu-id="9cade-150">Wewnętrzny numer portu SSH wynosi 22.</span><span class="sxs-lookup"><span data-stu-id="9cade-150">The internal SSH port number is set to 22.</span></span>
* <span data-ttu-id="9cade-151">Nową usługę w chmurze jest tworzony w regionie Azure, określony przez lokalizację.</span><span class="sxs-lookup"><span data-stu-id="9cade-151">A new cloud service is created in the Azure region specified by the location.</span></span> <span data-ttu-id="9cade-152">Określ lokalizację, w której znajduje się wybrany rozmiar maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9cade-152">Specify a location in which the VM size you choose is available.</span></span>
* <span data-ttu-id="9cade-153">Obsługa SUSE priorytet (która wiąże się z dodatkowych opłat) Nazwa obrazu z dodatkiem SP1 SLES 12 aktualnie może być jedną z tych dwóch opcji:</span><span class="sxs-lookup"><span data-stu-id="9cade-153">For SUSE priority support (which incurs additional charges), the SLES 12 SP1 image name currently can be one of these two options:</span></span> 

 `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-v20160824`

  `b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-sp1-hpc-priority-v20160824`


### <a name="customize-the-vm"></a><span data-ttu-id="9cade-154">Dostosowywanie maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="9cade-154">Customize the VM</span></span>
<span data-ttu-id="9cade-155">Gdy maszyna wirtualna zakończy, udostępniania SSH z maszyną Wirtualną za pomocą zewnętrznego adresu IP maszyny Wirtualnej (lub nazwa DNS) i portu zewnętrznego numeru skonfigurowany, a następnie dostosować go.</span><span class="sxs-lookup"><span data-stu-id="9cade-155">After the VM finishes provisioning, SSH to the VM by using the VM's external IP address (or DNS name) and the external port number you configured, and then customize it.</span></span> <span data-ttu-id="9cade-156">Aby uzyskać informacje dotyczące połączenia, zobacz [jak zalogować się do maszyny wirtualnej z systemem Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9cade-156">For connection details, see [How to log on to a virtual machine running Linux](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9cade-157">Przeprowadź poleceń użytkownika, które zostały skonfigurowane na Maszynie wirtualnej, chyba że do ukończenia krok jest wymagany dostęp do konta root.</span><span class="sxs-lookup"><span data-stu-id="9cade-157">Perform commands as the user you configured on the VM, unless root access is required to complete a step.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cade-158">Microsoft Azure nie zapewnia dostęp do konta root do maszyn wirtualnych systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9cade-158">Microsoft Azure does not provide root access to Linux VMs.</span></span> <span data-ttu-id="9cade-159">Aby uzyskać dostęp administracyjny podczas połączenia jako użytkownik z maszyną wirtualną, Uruchom polecenia przy użyciu `sudo`.</span><span class="sxs-lookup"><span data-stu-id="9cade-159">To gain administrative access when connected as a user to the VM, run commands by using `sudo`.</span></span>
>
>

* <span data-ttu-id="9cade-160">**Aktualizacje**: Zainstaluj aktualizacje za pomocą zypper.</span><span class="sxs-lookup"><span data-stu-id="9cade-160">**Updates**: Install updates by using zypper.</span></span> <span data-ttu-id="9cade-161">Można także zainstalować narzędzia systemu plików NFS.</span><span class="sxs-lookup"><span data-stu-id="9cade-161">You might also want to install NFS utilities.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9cade-162">SLES 12 SP1 HPC maszynie wirtualnej zalecamy nie stosowanie aktualizacji jądra, które mogą powodować problemy z protokołem RDMA Linux sterowniki.</span><span class="sxs-lookup"><span data-stu-id="9cade-162">In a SLES 12 SP1 HPC VM, we recommend that you don't apply kernel updates, which can cause issues with the Linux RDMA drivers.</span></span>
  >
  >
* <span data-ttu-id="9cade-163">**Intel MPI**: zakończenie instalacji MPI Intel na maszynie Wirtualnej HPC SLES 12 z dodatkiem SP1, uruchamiając następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9cade-163">**Intel MPI**: Complete the installation of Intel MPI on the SLES 12 SP1 HPC VM by running the following command:</span></span>

        sudo rpm -v -i --nodeps /opt/intelMPI/intel_mpi_packages/*.rpm
* <span data-ttu-id="9cade-164">**Zablokować pamięci**: kodów dla MPI zablokować dostępnej pamięci dla funkcji RDMA, dodać lub zmienić poniższe ustawienia w pliku /etc/security/limits.conf.</span><span class="sxs-lookup"><span data-stu-id="9cade-164">**Lock memory**: For MPI codes to lock the memory available for RDMA, add or change the following settings in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="9cade-165">Należy głównego dostępu do edytowania tego pliku.</span><span class="sxs-lookup"><span data-stu-id="9cade-165">You need root access to edit this file.</span></span>

    ```
    <User or group name> hard    memlock <memory required for your application in KB>

    <User or group name> soft    memlock <memory required for your application in KB>
    ```

  > [!NOTE]
  > <span data-ttu-id="9cade-166">Do celów testowych można również ustawić memlock na nieograniczony.</span><span class="sxs-lookup"><span data-stu-id="9cade-166">For testing purposes, you can also set memlock to unlimited.</span></span> <span data-ttu-id="9cade-167">Na przykład: `<User or group name>    hard    memlock unlimited`.</span><span class="sxs-lookup"><span data-stu-id="9cade-167">For example: `<User or group name>    hard    memlock unlimited`.</span></span> <span data-ttu-id="9cade-168">Aby uzyskać więcej informacji, zobacz [znaną metody ustawienie zablokowane rozmiar pamięci](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span><span class="sxs-lookup"><span data-stu-id="9cade-168">For more information, see [Best known methods for setting locked memory size](https://software.intel.com/en-us/blogs/2014/12/16/best-known-methods-for-setting-locked-memory-size).</span></span>
  >
  >
* <span data-ttu-id="9cade-169">**Klucze SSH dla maszyn wirtualnych SLES**: klucze Generowanie SSH do ustanawiania relacji zaufania dla konta użytkownika między węzłami obliczeniowymi w SLES klastra podczas uruchamiania zadań MPI.</span><span class="sxs-lookup"><span data-stu-id="9cade-169">**SSH keys for SLES VMs**: Generate SSH keys to establish trust for your user account among the compute nodes in the SLES cluster when running MPI jobs.</span></span> <span data-ttu-id="9cade-170">Jeśli wdrożono maszynę Wirtualną na podstawie CentOS HPC, nie należy wykonać ten krok.</span><span class="sxs-lookup"><span data-stu-id="9cade-170">If you deployed a CentOS-based HPC VM, don't follow this step.</span></span> <span data-ttu-id="9cade-171">Zobacz instrukcje w dalszej części tego artykułu można ustawić passwordless SSH relacji zaufania między węzłami klastra po przechwyceniu obrazu i wdrożenie klastra.</span><span class="sxs-lookup"><span data-stu-id="9cade-171">See instructions later in this article to set up passwordless SSH trust among the cluster nodes after you capture the image and deploy the cluster.</span></span>

    <span data-ttu-id="9cade-172">Do tworzenia kluczy SSH, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="9cade-172">To create SSH keys, run the following command.</span></span> <span data-ttu-id="9cade-173">Po wyświetleniu monitu o wprowadzenie danych, wybierz **Enter** do generowania kluczy w domyślnej lokalizacji bez ustawienia hasła.</span><span class="sxs-lookup"><span data-stu-id="9cade-173">When you are prompted for input, select **Enter** to generate the keys in the default location without setting a password.</span></span>

        ssh-keygen

    <span data-ttu-id="9cade-174">Dołącz klucz publiczny do pliku authorized_keys znane kluczy publicznych.</span><span class="sxs-lookup"><span data-stu-id="9cade-174">Append the public key to the authorized_keys file for known public keys.</span></span>

        cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

    <span data-ttu-id="9cade-175">W katalogu ~/.ssh edycji lub tworzenia pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9cade-175">In the ~/.ssh directory, edit or create the config file.</span></span> <span data-ttu-id="9cade-176">Podaj zakres adresów IP w sieci prywatnej, które będą używane na platformie Azure (10.32.0.0/16 w tym przykładzie):</span><span class="sxs-lookup"><span data-stu-id="9cade-176">Provide the IP address range of the private network that you plan to use in Azure (10.32.0.0/16 in this example):</span></span>

        host 10.32.0.*
        StrictHostKeyChecking no

    <span data-ttu-id="9cade-177">Alternatywnie listy adres IP sieci prywatnej każdej maszyny Wirtualnej w klastrze w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9cade-177">Alternatively, list the private network IP address of each VM in your cluster as follows:</span></span>

    ```
    host 10.32.0.1
     StrictHostKeyChecking no
    host 10.32.0.2
     StrictHostKeyChecking no
    host 10.32.0.3
     StrictHostKeyChecking no
    ```

  > [!NOTE]
  > <span data-ttu-id="9cade-178">Konfigurowanie `StrictHostKeyChecking no` można utworzyć potencjalne zagrożenie dla bezpieczeństwa, jeśli nie określono określonego adresu IP lub zakresu.</span><span class="sxs-lookup"><span data-stu-id="9cade-178">Configuring `StrictHostKeyChecking no` can create a potential security risk when a specific IP address or range is not specified.</span></span>
  >
  >
* <span data-ttu-id="9cade-179">**Aplikacje**: Zainstaluj wszystkie aplikacje muszą lub wykonywać inne dostosowania, przed przechwyceniem obrazu.</span><span class="sxs-lookup"><span data-stu-id="9cade-179">**Applications**: Install any applications you need or perform other customizations before you capture the image.</span></span>

### <a name="capture-the-image"></a><span data-ttu-id="9cade-180">Przechwycenie obrazu</span><span class="sxs-lookup"><span data-stu-id="9cade-180">Capture the image</span></span>
<span data-ttu-id="9cade-181">Aby przechwycić obraz, uruchom następujące polecenie w maszyny Wirtualnej systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9cade-181">To capture the image, first run the following command on the Linux VM.</span></span> <span data-ttu-id="9cade-182">To polecenie deprovisions maszyny Wirtualnej, ale przechowuje konta użytkowników i kluczy SSH, które zostały zdefiniowane.</span><span class="sxs-lookup"><span data-stu-id="9cade-182">This command deprovisions the VM but maintains user accounts and SSH keys that you set up.</span></span>

```
sudo waagent -deprovision
```

<span data-ttu-id="9cade-183">Z komputera klienta uruchom następujące polecenia interfejsu wiersza polecenia Azure, aby przechwycić obraz.</span><span class="sxs-lookup"><span data-stu-id="9cade-183">From your client computer, run the following Azure CLI commands to capture the image.</span></span> <span data-ttu-id="9cade-184">Aby uzyskać więcej informacji, zobacz [Przechwytywanie klasycznej maszyny wirtualnej systemu Linux jako obrazu](capture-image.md).</span><span class="sxs-lookup"><span data-stu-id="9cade-184">For more information, see [How to capture a classic Linux virtual machine as an image](capture-image.md).</span></span>  

```
azure vm shutdown <vm-name>

azure vm capture -t <vm-name> <image-name>

```

<span data-ttu-id="9cade-185">Po uruchomieniu tych poleceń obrazu maszyny Wirtualnej są przechwytywane do użycia, a maszyna wirtualna jest usuwana.</span><span class="sxs-lookup"><span data-stu-id="9cade-185">After you run these commands, the VM image is captured for your use and the VM is deleted.</span></span> <span data-ttu-id="9cade-186">Masz teraz gotowy do wdrożenia klastra obraz niestandardowy.</span><span class="sxs-lookup"><span data-stu-id="9cade-186">Now you have your custom image ready to deploy a cluster.</span></span>

### <a name="deploy-a-cluster-with-the-image"></a><span data-ttu-id="9cade-187">Wdrażanie klastra przy użyciu obrazu</span><span class="sxs-lookup"><span data-stu-id="9cade-187">Deploy a cluster with the image</span></span>
<span data-ttu-id="9cade-188">Zmodyfikuj następujący skrypt Bash z odpowiednimi wartościami dla środowiska i uruchom go z komputera klienckiego.</span><span class="sxs-lookup"><span data-stu-id="9cade-188">Modify the following Bash script with appropriate values for your environment and run it from your client computer.</span></span> <span data-ttu-id="9cade-189">Ponieważ Azure wdraża szeregowo w klasycznym modelu wdrażania maszyn wirtualnych, zajmuje kilka minut, aby wdrożyć osiem maszyn wirtualnych A9 sugerowane w tym skrypcie.</span><span class="sxs-lookup"><span data-stu-id="9cade-189">Because Azure deploys the VMs serially in the classic deployment model, it takes a few minutes to deploy the eight A9 VMs suggested in this script.</span></span>

```
#!/bin/bash -x
# Script to create a compute cluster without a scheduler in a VNet in Azure
# Create a custom private network in Azure
# Replace 10.32.0.0 with your virtual network address space
# Replace <network-name> with your network identifier
# Replace "West US" with an Azure region where the VM size is available
# See Azure Pricing pages for prices and availability of compute-intensive VMs

azure network vnet create -l "West US" -e 10.32.0.0 -i 16 <network-name>

# Create a cloud service. All the compute-intensive instances need to be in the same cloud service for Linux RDMA to work across InfiniBand.
# Note: The current maximum number of VMs in a cloud service is 50. If you need to provision more than 50 VMs in the same cloud service in your cluster, contact Azure Support.

azure service create <cloud-service-name> --location "West US" –s <subscription-ID>

# Define a prefix naming scheme for compute nodes, e.g., cluster11, cluster12, etc.

vmname=cluster

# Define a prefix for external port numbers. If you want to turn off external ports and use only internal ports to communicate between compute nodes via port 22, don’t use this option. Since port numbers up to 10000 are reserved, use numbers after 10000. Leave external port on for rank 0 and head node.

portnumber=101

# In this cluster there will be 8 size A9 nodes, named cluster11 to cluster18. Specify your captured image in <image-name>. Specify the username and password you used when creating the SSH keys.

for (( i=11; i<19; i++ )); do
        azure vm create -g <username> -p <password> -c <cloud-service-name> -z A9 -n $vmname$i -e $portnumber$i -w <network-name> -b Subnet-1 <image-name>
done

# Save this script with a name like makecluster.sh and run it in your shell environment to provision your cluster
```

## <a name="considerations-for-a-centos-hpc-cluster"></a><span data-ttu-id="9cade-190">Zagadnienia dotyczące klastra CentOS HPC</span><span class="sxs-lookup"><span data-stu-id="9cade-190">Considerations for a CentOS HPC cluster</span></span>
<span data-ttu-id="9cade-191">Aby skonfigurować klaster oparty na jednym z obrazów na podstawie CentOS HPC w portalu Azure Marketplace zamiast SLES 12 dla HPC, wykonaj ogólne kroki opisane w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="9cade-191">If you want to set up a cluster based on one of the CentOS-based HPC images in the Azure Marketplace instead of SLES 12 for HPC, follow the general steps in the preceding section.</span></span> <span data-ttu-id="9cade-192">Podczas udostępniania i konfigurowania maszyny Wirtualnej, należy uwzględnić następujące różnice:</span><span class="sxs-lookup"><span data-stu-id="9cade-192">Note the following differences when you provision and configure the VM:</span></span>

- <span data-ttu-id="9cade-193">Intel MPI jest już zainstalowana na maszynie Wirtualnej z obrazu na podstawie CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="9cade-193">Intel MPI is already installed on a VM provisioned from a CentOS-based HPC image.</span></span>
- <span data-ttu-id="9cade-194">Ustawienia pamięci blokady są już dodana w pliku /etc/security/limits.conf maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="9cade-194">Lock memory settings are already added in the VM's /etc/security/limits.conf file.</span></span>
- <span data-ttu-id="9cade-195">Nie generują kluczy SSH na maszynie Wirtualnej, należy udostępnić do przechwycenia.</span><span class="sxs-lookup"><span data-stu-id="9cade-195">Do not generate SSH keys on the VM you provision for capture.</span></span> <span data-ttu-id="9cade-196">Zamiast tego zaleca się skonfigurowanie uwierzytelniania użytkownika po wdrożeniu klastra.</span><span class="sxs-lookup"><span data-stu-id="9cade-196">Instead, we recommend setting up user-based authentication after you deploy the cluster.</span></span> <span data-ttu-id="9cade-197">Aby uzyskać więcej informacji zobacz sekcję poniżej.</span><span class="sxs-lookup"><span data-stu-id="9cade-197">For more information, see the following section.</span></span>  

### <a name="set-up-passwordless-ssh-trust-on-the-cluster"></a><span data-ttu-id="9cade-198">Konfigurowanie passwordless zaufania SSH w klastrze</span><span class="sxs-lookup"><span data-stu-id="9cade-198">Set up passwordless SSH trust on the cluster</span></span>
<span data-ttu-id="9cade-199">W klastrze HPC na podstawie CentOS, istnieją dwie metody do ustanawiania relacji zaufania między węzły obliczeniowe: uwierzytelnianie oparte na hoście i uwierzytelnianie oparte na użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="9cade-199">On a CentOS-based HPC cluster, there are two methods for establishing trust between the compute nodes: host-based authentication and user-based authentication.</span></span> <span data-ttu-id="9cade-200">Uwierzytelnianie oparte na hoście, wykracza poza zakres tego artykułu i zazwyczaj muszą być wykonywane przez rozszerzenia skryptów podczas wdrażania.</span><span class="sxs-lookup"><span data-stu-id="9cade-200">Host-based authentication is outside of the scope of this article and generally must be done through an extension script during deployment.</span></span> <span data-ttu-id="9cade-201">Uwierzytelnianie użytkownika jest wygodną metodą ustanawiania relacji zaufania po wdrożeniu i wymaga tworzenia i udostępniania kluczy SSH między węzłami obliczeniowymi w klastrze.</span><span class="sxs-lookup"><span data-stu-id="9cade-201">User-based authentication is convenient for establishing trust after deployment and requires the generation and sharing of SSH keys among the compute nodes in the cluster.</span></span> <span data-ttu-id="9cade-202">Ta metoda jest często nazywana passwordless logowania SSH i jest wymagany w przypadku uruchamiania zadań MPI.</span><span class="sxs-lookup"><span data-stu-id="9cade-202">This method is commonly known as passwordless SSH login and is required when running MPI jobs.</span></span>

<span data-ttu-id="9cade-203">Przykładowy skrypt zamieszczone przez społeczność jest dostępna w [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) do włączenia uwierzytelniania użytkownika łatwy w klastrze HPC na podstawie CentOS.</span><span class="sxs-lookup"><span data-stu-id="9cade-203">A sample script contributed from the community is available on [GitHub](https://github.com/tanewill/utils/blob/master/user_authentication.sh) to enable easy user authentication on a CentOS-based HPC cluster.</span></span> <span data-ttu-id="9cade-204">Pobranie i użycie tego skryptu za pomocą poniższych kroków.</span><span class="sxs-lookup"><span data-stu-id="9cade-204">Download and use this script by using the following steps.</span></span> <span data-ttu-id="9cade-205">Można również zmodyfikować tego skryptu lub użyć innej metody do ustanawiania passwordless uwierzytelniania SSH między węzłami klastra obliczeniowego.</span><span class="sxs-lookup"><span data-stu-id="9cade-205">You can also modify this script or use any other method to establish passwordless SSH authentication between the cluster compute nodes.</span></span>

    wget https://raw.githubusercontent.com/tanewill/utils/master/ user_authentication.sh

<span data-ttu-id="9cade-206">Aby uruchomić skrypt, musisz znać prefiks podsieci adresów IP.</span><span class="sxs-lookup"><span data-stu-id="9cade-206">To run the script, you need to know the prefix for your subnet IP addresses.</span></span> <span data-ttu-id="9cade-207">Pobierz prefiks, uruchamiając następujące polecenie w jednym z węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="9cade-207">Get the prefix by running the following command on one of the cluster nodes.</span></span> <span data-ttu-id="9cade-208">Dane wyjściowe powinny wyglądać podobnie 10.1.3.5 i prefiks jest 10.1.3 części.</span><span class="sxs-lookup"><span data-stu-id="9cade-208">Your output should look something like 10.1.3.5, and the prefix is the 10.1.3 portion.</span></span>

    ifconfig eth0 | grep -w inet | awk '{print $2}'

<span data-ttu-id="9cade-209">Teraz uruchom skrypt przy użyciu trzech parametrów: Nazwa pospolita użytkownika w węzłach obliczeniowych, wspólnego hasła dla tego użytkownika w węzłach obliczeniowych i prefiks podsieci zwrócony przez poprzednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="9cade-209">Now run the script using three parameters: the common user name on the compute nodes, the common password for that user on the compute nodes, and the subnet prefix that was returned from the previous command.</span></span>

    ./user_authentication.sh <myusername> <mypassword> 10.1.3

<span data-ttu-id="9cade-210">Ten skrypt wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9cade-210">This script does the following:</span></span>

* <span data-ttu-id="9cade-211">Tworzy katalog o nazwie .ssh, co jest niezbędne do logowania passwordless węzła hosta.</span><span class="sxs-lookup"><span data-stu-id="9cade-211">Creates a directory on the host node named .ssh, which is required for passwordless login.</span></span>
* <span data-ttu-id="9cade-212">Tworzy plik konfiguracji w katalogu .ssh, która sprawia, że passwordless logowania, aby umożliwić logowanie z dowolnego węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="9cade-212">Creates a configuration file in the .ssh directory that instructs passwordless login to allow login from any node in the cluster.</span></span>
* <span data-ttu-id="9cade-213">Tworzy pliki zawierające nazwy węzła i węzła adresów IP dla wszystkich węzłów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="9cade-213">Creates files containing the node names and node IP addresses for all the nodes in the cluster.</span></span> <span data-ttu-id="9cade-214">Te pliki są pozostawiane po uruchomieniu skryptu do wykorzystania w późniejszym czasie.</span><span class="sxs-lookup"><span data-stu-id="9cade-214">These files are left after the script is run for later reference.</span></span>
* <span data-ttu-id="9cade-215">Tworzy prywatne i publiczne pary kluczy dla każdego węzła klastra (w tym węzła hosta) oraz wpisy w pliku authorized_keys.</span><span class="sxs-lookup"><span data-stu-id="9cade-215">Creates a private and public key pair for each cluster node (including the host node) and creates entries in the authorized_keys file.</span></span>

> [!WARNING]
> <span data-ttu-id="9cade-216">Uruchomienie tego skryptu można utworzyć potencjalne zagrożenie dla bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="9cade-216">Running this script can create a potential security risk.</span></span> <span data-ttu-id="9cade-217">Upewnij się, że informacje o kluczu publicznym w ~/.ssh nie będzie on rozpowszechniany.</span><span class="sxs-lookup"><span data-stu-id="9cade-217">Ensure that the public key information in ~/.ssh is not distributed.</span></span>
>
>

## <a name="configure-intel-mpi"></a><span data-ttu-id="9cade-218">Skonfiguruj Intel MPI</span><span class="sxs-lookup"><span data-stu-id="9cade-218">Configure Intel MPI</span></span>
<span data-ttu-id="9cade-219">Aby uruchomić aplikacje MPI RDMA systemu Linux platformy Azure, należy skonfigurować niektóre zmienne środowiskowe specyficzne dla firmy Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="9cade-219">To run MPI applications on Azure Linux RDMA, you need to configure certain environment variables specific to Intel MPI.</span></span> <span data-ttu-id="9cade-220">Poniżej przedstawiono przykładowy skrypt Bash, aby skonfigurować zmienne potrzebne do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9cade-220">Here is a sample Bash script to configure the variables needed to run an application.</span></span> <span data-ttu-id="9cade-221">Zmień ścieżkę, aby mpivars.sh zgodnie z potrzebami dla tej instalacji Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="9cade-221">Change the path to mpivars.sh as needed for your installation of Intel MPI.</span></span>

```
#!/bin/bash -x

# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh

export I_MPI_FABRICS=shm:dapl

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB
# Setting the variable to shm:dapl gives best performance for some applications
# If your application doesn’t take advantage of shared memory and MPI together, then set only dapl

export I_MPI_DAPL_PROVIDER=ofa-v2-ib0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

export I_MPI_DYNAMIC_CONNECTION=0

# THIS IS A MANDATORY ENVIRONMENT VARIABLE AND MUST BE SET BEFORE RUNNING ANY JOB

# Command line to run the job

mpirun -n <number-of-cores> -ppn <core-per-node> -hostfile <hostfilename>  /path <path to the application exe> <arguments specific to the application>

#end
```

<span data-ttu-id="9cade-222">Format pliku hosta ma następującą składnię.</span><span class="sxs-lookup"><span data-stu-id="9cade-222">The format of the host file is as follows.</span></span> <span data-ttu-id="9cade-223">Dodaj jeden wiersz dla każdego węzła w klastrze.</span><span class="sxs-lookup"><span data-stu-id="9cade-223">Add one line for each node in your cluster.</span></span> <span data-ttu-id="9cade-224">Określ prywatnych adresów IP z sieci wirtualnej nie zostały zdefiniowane wcześniej, a nie nazw DNS.</span><span class="sxs-lookup"><span data-stu-id="9cade-224">Specify private IP addresses from the virtual network defined earlier, not DNS names.</span></span> <span data-ttu-id="9cade-225">Na przykład dla dwa hosty z adresami IP 10.32.0.1 i 10.32.0.2, plik zawiera następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9cade-225">For example, for two hosts with IP addresses 10.32.0.1 and 10.32.0.2, the file contains the following:</span></span>

```
10.32.0.1:16
10.32.0.2:16
```

## <a name="run-mpi-on-a-basic-two-node-cluster"></a><span data-ttu-id="9cade-226">Uruchom MPI na podstawowe dwa węzły klastra</span><span class="sxs-lookup"><span data-stu-id="9cade-226">Run MPI on a basic two-node cluster</span></span>
<span data-ttu-id="9cade-227">Jeśli jeszcze tego nie zrobiono, najpierw skonfigurować środowisko dla Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="9cade-227">If you haven't already done so, first set up the environment for Intel MPI.</span></span>

```
# For a SLES 12 SP1 HPC cluster

source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh

# For a CentOS-based HPC cluster

# source /opt/intel/impi/5.1.3.181/bin64/mpivars.sh
```

### <a name="run-an-mpi-command"></a><span data-ttu-id="9cade-228">Uruchom polecenie MPI</span><span class="sxs-lookup"><span data-stu-id="9cade-228">Run an MPI command</span></span>
<span data-ttu-id="9cade-229">Uruchom polecenie MPI na jednym z węzłów obliczeniowych do wskazują, że MPI jest poprawnie zainstalowany i może komunikować się między co najmniej się, że dwa węzły obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="9cade-229">Run an MPI command on one of the compute nodes to show that MPI is installed properly and can communicate between at least two compute nodes.</span></span> <span data-ttu-id="9cade-230">Następujące **mpirun** polecenia **hostname** na dwa węzły.</span><span class="sxs-lookup"><span data-stu-id="9cade-230">The following **mpirun** command runs the **hostname** command on two nodes.</span></span>

```
mpirun -ppn 1 -n 2 -hosts <host1>,<host2> -env I_MPI_FABRICS=shm:dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 hostname
```
<span data-ttu-id="9cade-231">Dane wyjściowe powinny zawierać nazw wszystkie węzły, które przekazany jako dane wejściowe dla `-hosts`.</span><span class="sxs-lookup"><span data-stu-id="9cade-231">Your output should list the names of all the nodes that you passed as input for `-hosts`.</span></span> <span data-ttu-id="9cade-232">Na przykład **mpirun** polecenie z dwoma węzłami zwraca dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="9cade-232">For example, an **mpirun** command with two nodes returns output like the following:</span></span>

```
cluster11
cluster12
```

### <a name="run-an-mpi-benchmark"></a><span data-ttu-id="9cade-233">Uruchamianie testów porównawczych MPI</span><span class="sxs-lookup"><span data-stu-id="9cade-233">Run an MPI benchmark</span></span>
<span data-ttu-id="9cade-234">Następujące polecenie Intel MPI uruchamia testu pingpong, aby sprawdzić konfigurację klastra i połączenie z siecią RDMA.</span><span class="sxs-lookup"><span data-stu-id="9cade-234">The following Intel MPI command runs a pingpong benchmark to verify the cluster configuration and connection to the RDMA network.</span></span>

```
mpirun -hosts <host1>,<host2> -ppn 1 -n 2 -env I_MPI_FABRICS=dapl -env I_MPI_DAPL_PROVIDER=ofa-v2-ib0 -env I_MPI_DYNAMIC_CONNECTION=0 IMB-MPI1 pingpong
```

<span data-ttu-id="9cade-235">W klastrze pracy z dwoma węzłami powinny zostać wyświetlone dane wyjściowe podobne do następujących.</span><span class="sxs-lookup"><span data-stu-id="9cade-235">On a working cluster with two nodes, you should see output like the following.</span></span> <span data-ttu-id="9cade-236">W sieci Azure RDMA oczekuje się, że czas oczekiwania na poziomie lub poniżej 3 mikrosekundach wiadomości rozmiary maksymalnie 512 bajtów.</span><span class="sxs-lookup"><span data-stu-id="9cade-236">On the Azure RDMA network, expect latency at or below 3 microseconds for message sizes up to 512 bytes.</span></span>

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
# the number of iterations per message size is cut down
# dynamically when a certain run time (per message size sample)
# is expected to be exceeded. Time limit is defined by variable
# "SECS_PER_SAMPLE" (=> IMB_settings.h)
# or through the flag => -time

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
# List of Benchmarks to run:
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



## <a name="next-steps"></a><span data-ttu-id="9cade-237">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9cade-237">Next steps</span></span>
* <span data-ttu-id="9cade-238">Wdrażanie i uruchamianie sieci MPI Linux aplikacji w klastrze systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9cade-238">Deploy and run your Linux MPI applications on your Linux cluster.</span></span>
* <span data-ttu-id="9cade-239">Zobacz [dokumentację biblioteki MPI Intel](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) wskazówki dotyczące Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="9cade-239">See the [Intel MPI Library documentation](https://software.intel.com/en-us/articles/intel-mpi-library-documentation/) for guidance on Intel MPI.</span></span>
* <span data-ttu-id="9cade-240">Spróbuj [szablon szybkiego startu](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) do utworzenia klastra połysk Intel przy użyciu obrazu na podstawie CentOS HPC.</span><span class="sxs-lookup"><span data-stu-id="9cade-240">Try a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/intel-lustre-clients-on-centos) to create an Intel Lustre cluster by using a CentOS-based HPC image.</span></span> <span data-ttu-id="9cade-241">Aby uzyskać więcej informacji, zobacz [wdrażanie Intel chmury Edition dla połysk w systemie Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span><span class="sxs-lookup"><span data-stu-id="9cade-241">For details, see [Deploying Intel Cloud Edition for Lustre on Microsoft Azure](https://blogs.msdn.microsoft.com/arsen/2015/10/29/deploying-intel-cloud-edition-for-lustre-on-microsoft-azure/).</span></span>
