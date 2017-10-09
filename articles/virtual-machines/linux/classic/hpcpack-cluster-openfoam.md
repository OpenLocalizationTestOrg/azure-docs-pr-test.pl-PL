---
title: aaaRun OpenFOAM pakietem HPC na maszynach wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Wdrażanie klastra Microsoft HPC Pack na platformie Azure, a następnie uruchom zadanie OpenFOAM na wielu węzłach obliczeniowych Linux przez sieć RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="ac065-103">Uruchamianie oprogramowania OpenFoam przy użyciu pakietu Microsoft HPC w węzłach RDMA systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ac065-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="ac065-104">W tym artykule przedstawiono jednokierunkowej toorun OpenFoam w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ac065-104">This article shows you one way toorun OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="ac065-105">W tym miejscu, w przypadku wdrażania klastra Microsoft HPC Pack z węzłami obliczeniowymi systemu Linux na platformie Azure i uruchom [OpenFoam](http://openfoam.com/) zadania z Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="ac065-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="ac065-106">Tak, aby węzły obliczeniowe hello komunikują się za pośrednictwem sieci Azure RDMA hello, można użyć z funkcją RDMA maszynach wirtualnych platformy Azure dla węzłów obliczeniowych hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-106">You can use RDMA-capable Azure VMs for hello compute nodes, so that hello compute nodes communicate over hello Azure RDMA network.</span></span> <span data-ttu-id="ac065-107">Inne toorun opcje OpenFoam na platformie Azure zawierają w pełni skonfigurowany komercyjnych obrazy dostępne w hello Marketplace, takie jak jego UberCloud [2.3 OpenFoam na CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)i uruchamianych [partii zadań Azure](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="ac065-107">Other options toorun OpenFoam in Azure include fully configured commercial images available in hello Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ac065-108">OpenFOAM (dla operacji Otwórz pole i manipulowania) to pakiet oprogramowania open source obliczeniową płynu dynamics (CFD), który jest powszechnie używany w inżynieryjne i naukowe w organizacjach użytku komercyjnego i academic.</span><span class="sxs-lookup"><span data-stu-id="ac065-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="ac065-109">Obejmuje narzędzia do meshing, szczególnie snappyHexMesh zrównoleglone mesher złożonych CAD mają geometrię oraz wstępne i przetwarzania końcowego.</span><span class="sxs-lookup"><span data-stu-id="ac065-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="ac065-110">Prawie wszystkie procesy wykonywane równolegle, włączanie użytkowników tootake pełne wykorzystanie sprzętu komputera za pośrednictwem interfejsu LINQ.</span><span class="sxs-lookup"><span data-stu-id="ac065-110">Almost all processes run in parallel, enabling users tootake full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="ac065-111">Microsoft HPC Pack udostępnia funkcje toorun HPC na dużą skalę i równoległych aplikacji, w tym aplikacji MPI w klastrach maszyny wirtualne Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ac065-111">Microsoft HPC Pack provides features toorun large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="ac065-112">HPC Pack obsługuje również uruchomione HPC systemu Linux węzła, maszyn wirtualnych wdrożonych w klastrze HPC Pack obliczeniowego aplikacji w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="ac065-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="ac065-113">Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) dla toousing wprowadzenie Linux obliczeniowe węzłów o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ac065-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction toousing Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="ac065-114">W tym artykule przedstawiono sposób toorun obciążenia Linux MPI bez HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ac065-114">This article illustrates how toorun a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="ac065-115">Zakłada się, że masz pewną znajomość z Administracja systemu Linux i systemem obciążeń MPI klastry z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="ac065-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="ac065-116">Jeśli używasz wersji MPI oraz OpenFOAM inny niż hello te wyświetlane w tym artykule, może być toomodify niektóre kroki instalacji i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ac065-116">If you use versions of MPI and OpenFOAM different from hello ones shown in this article, you might have toomodify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ac065-117">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ac065-117">Prerequisites</span></span>
* <span data-ttu-id="ac065-118">**Węzły obliczeniowe HPC Pack klastra z systemem Linux z funkcją RDMA** — wdrożenie klastra HPC Pack o rozmiarze A8, A9, H16r, lub H16rm Linux obliczeniowe węzłów za pomocą [szablonu usługi Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) lub [skrypt programu PowerShell Azure](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="ac065-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="ac065-119">Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) hello wymagania wstępne i kroki dla każdej opcji.</span><span class="sxs-lookup"><span data-stu-id="ac065-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="ac065-120">Jeśli wybierzesz hello opcji wdrażania skryptu programu PowerShell, zobacz hello przykładowy plik konfiguracyjny w hello przykładowych plików na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ac065-120">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="ac065-121">Użyj tej konfiguracji klastra HPC Pack toodeploy bazującej na platformie Azure składające się z węzłem głównym A8 systemu Windows Server 2012 R2 rozmiar i węzły obliczeniowe 2 rozmiar A8 SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="ac065-121">Use this configuration toodeploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="ac065-122">Zastąp wartości odpowiednie dla Twojej subskrypcji i usługi nazw.</span><span class="sxs-lookup"><span data-stu-id="ac065-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="ac065-123">**Tooknow dodatkowe elementy**</span><span class="sxs-lookup"><span data-stu-id="ac065-123">**Additional things tooknow**</span></span>
  
  * <span data-ttu-id="ac065-124">Dla systemu Linux RDMA sieci wymagań wstępnych na platformie Azure, zobacz [wysokiej wydajności obliczeniowe rozmiarów maszyn wirtualnych](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ac065-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="ac065-125">Użycie hello opcji wdrażania skryptu programu Powershell, należy wdrożyć wszystkie węzły obliczeniowe Linux hello w ramach połączenia sieciowego RDMA hello toouse usługi jednej chmury.</span><span class="sxs-lookup"><span data-stu-id="ac065-125">If you use hello Powershell script deployment option, deploy all hello Linux compute nodes within one cloud service toouse hello RDMA network connection.</span></span>
  * <span data-ttu-id="ac065-126">Po wdrożeniu hello węzłów Linux należy połączyć SSH tooperform wszelkie dodatkowe zadania administracyjne.</span><span class="sxs-lookup"><span data-stu-id="ac065-126">After deploying hello Linux nodes, connect by SSH tooperform any additional administrative tasks.</span></span> <span data-ttu-id="ac065-127">Znajdź szczegóły połączenia SSH powitania dla każdej maszyny Wirtualnej systemu Linux w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ac065-127">Find hello SSH connection details for each Linux VM in hello Azure portal.</span></span>  
* <span data-ttu-id="ac065-128">**Intel MPI** -toorun OpenFOAM na SLES 12 HPC obliczeniowe węzłów na platformie Azure, konieczne tooinstall hello Intel MPI biblioteki 5 runtime ze hello [lokacji Intel.com](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="ac065-128">**Intel MPI** - toorun OpenFOAM on SLES 12 HPC compute nodes in Azure, you need tooinstall hello Intel MPI Library 5 runtime from hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="ac065-129">(Intel MPI 5 jest preinstalowany na podstawie CentOS HPC obrazy).  W kolejnym kroku w razie potrzeby zainstaluj Intel MPI na systemie Linux węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="ac065-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="ac065-130">tooprepare dla tego kroku po zarejestrowaniu się Intel, łącza hello hello potwierdzenie e-mail toohello powiązane strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="ac065-130">tooprepare for this step, after you register with Intel, follow hello link in hello confirmation email toohello related web page.</span></span> <span data-ttu-id="ac065-131">Następnie hello kopiowania Pobierz łącze do pliku .tgz hello hello odpowiednią wersję Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="ac065-131">Then, copy hello download link for hello .tgz file for hello appropriate version of Intel MPI.</span></span> <span data-ttu-id="ac065-132">W tym artykule jest oparta na Intel MPI wersji 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="ac065-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="ac065-133">**OpenFOAM źródła pakietu** — Pobierz hello OpenFOAM źródła pakietu oprogramowania dla systemu Linux z hello [lokacji OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="ac065-133">**OpenFOAM Source Pack** - Download hello OpenFOAM Source Pack software for Linux from hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="ac065-134">Ten artykuł jest oparty na wersja źródła pakietu 2.3.1 dostępny do pobrania jako OpenFOAM 2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="ac065-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="ac065-135">Postępuj zgodnie z instrukcjami hello w dalszej części tego artykułu toounpack i skompiluj OpenFOAM na węzły obliczeniowe hello systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ac065-135">Follow hello instructions later in this article toounpack and compile OpenFOAM on hello Linux compute nodes.</span></span>
* <span data-ttu-id="ac065-136">**EnSight** (opcjonalnie) - toosee hello wyniki symulacji OpenFOAM, Pobierz i zainstaluj hello [EnSight](https://www.ceisoftware.com/download/) program wizualizacji i analizy.</span><span class="sxs-lookup"><span data-stu-id="ac065-136">**EnSight** (optional) - toosee hello results of your OpenFOAM simulation, download and install hello [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="ac065-137">Informacje licencyjne i pobierania znajdują się w lokacji EnSight hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-137">Licensing and download information are at hello EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="ac065-138">Konfigurowanie wzajemnego zaufania między węzły obliczeń</span><span class="sxs-lookup"><span data-stu-id="ac065-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="ac065-139">Uruchomienie zadania między węzłami na wielu węzłach Linux wymaga tootrust węzłów hello wzajemnie (przez **rsh** lub **ssh**).</span><span class="sxs-lookup"><span data-stu-id="ac065-139">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="ac065-140">Po utworzeniu klastra HPC Pack hello z hello Microsoft HPC Pack IaaS skrypt wdrożenia skryptu hello automatycznie konfiguruje stałe wzajemnego zaufania dla konta administratora hello, które określisz.</span><span class="sxs-lookup"><span data-stu-id="ac065-140">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="ac065-141">Dla użytkowników niebędących administratorami utworzonych w domenie hello klaster dostępne są tooset tymczasowego relacji wzajemnego zaufania między węzłami hello zadania został przydzielony toothem i zniszcz relacji powitania po zakończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-141">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem, and destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="ac065-142">tooestablish zaufania dla każdego użytkownika, podaj klastra toohello parę kluczy RSA, używającego HPC Pack hello relacji zaufania.</span><span class="sxs-lookup"><span data-stu-id="ac065-142">tooestablish trust for each user, provide an RSA key pair toohello cluster that HPC Pack uses for hello trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="ac065-143">Generowanie pary kluczy RSA</span><span class="sxs-lookup"><span data-stu-id="ac065-143">Generate an RSA key pair</span></span>
<span data-ttu-id="ac065-144">Łatwe toogenerate parę kluczy RSA, który zawiera klucz publiczny i klucz prywatny, uruchamiając hello Linux **ssh-keygen** polecenia.</span><span class="sxs-lookup"><span data-stu-id="ac065-144">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="ac065-145">Zaloguj się na tooa komputera z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="ac065-145">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="ac065-146">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="ac065-146">Run hello following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="ac065-147">Naciśnij klawisz **Enter** toouse hello domyślne ustawienia ukończenie hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="ac065-147">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="ac065-148">Nie należy wprowadzać hasło tutaj; Po wyświetleniu monitu o podanie hasła, wystarczy nacisnąć klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ac065-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generowanie pary kluczy RSA][keygen]
3. <span data-ttu-id="ac065-150">Zmień katalog ~/.ssh toohello katalogu.</span><span class="sxs-lookup"><span data-stu-id="ac065-150">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="ac065-151">Witaj klucz prywatny jest przechowywany w id_rsa i hello klucz publiczny w id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="ac065-151">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Klucze prywatne i publiczne][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="ac065-153">Dodaj klaster HPC Pack toohello pary kluczy hello</span><span class="sxs-lookup"><span data-stu-id="ac065-153">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="ac065-154">Należy pulpitu zdalnego połączenia tooyour węzła głównego z konta administratora HPC Pack (hello konta administratora, które można skonfigurować po uruchomieniu skryptu wdrażania hello).</span><span class="sxs-lookup"><span data-stu-id="ac065-154">Make a Remote Desktop connection tooyour head node with your HPC Pack administrator account (hello administrator account you set up when you ran hello deployment script).</span></span>
2. <span data-ttu-id="ac065-155">Używanie standardowych systemu Windows Server toocreate procedury konto użytkownika domeny w domenie usługi Active Directory hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ac065-155">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="ac065-156">Na przykład użyć hello użytkowników usługi Active Directory i narzędzia komputerów na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="ac065-156">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="ac065-157">Przykłady Hello w tym artykule przyjęto założenie, że utworzenie użytkownika domeny o nazwie hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="ac065-157">hello examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="ac065-158">Utwórz plik o nazwie C:\cred.xml i skopiuj hello RSA danych klucza do niego.</span><span class="sxs-lookup"><span data-stu-id="ac065-158">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="ac065-159">Przykładowy plik cred.xml znajduje się na końcu hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ac065-159">A sample cred.xml file is at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="ac065-160">Otwórz wiersz polecenia i wpisz następujące polecenia, które tooset hello poświadczenia danych dla konta hpclab\hpcuser hello hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-160">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="ac065-161">Użyj hello **extendeddata** toopass parametru hello nazwę pliku C:\cred.xml utworzony hello danych.</span><span class="sxs-lookup"><span data-stu-id="ac065-161">You use hello **extendeddata** parameter toopass hello name of C:\cred.xml file you created for hello key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="ac065-162">To polecenie zakończy się pomyślnie bez danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ac065-162">This command completes successfully without output.</span></span> <span data-ttu-id="ac065-163">Po ustawieniu hello poświadczeń dla kont użytkowników hello potrzebne toorun zadania, przechowuj plik cred.xml hello w bezpiecznej lokalizacji lub usuń go.</span><span class="sxs-lookup"><span data-stu-id="ac065-163">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="ac065-164">Wygenerowany hello parę kluczy RSA w jednym z węzłów z systemem Linux Pamiętaj klucze hello toodelete po zakończeniu korzystania z nich.</span><span class="sxs-lookup"><span data-stu-id="ac065-164">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="ac065-165">Jeśli HPC Pack znajdzie istniejący plik id_rsa lub plik id_rsa.pub, nie ustawia relacji wzajemnego zaufania.</span><span class="sxs-lookup"><span data-stu-id="ac065-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac065-166">Nie zaleca się uruchamiania zadania Linux jako administrator klastra w klastrze udostępniony, ponieważ przesłane przez administratora zadania działa w ramach konta głównego hello na powitania Linux węzłów.</span><span class="sxs-lookup"><span data-stu-id="ac065-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="ac065-167">Jednak zadanie przesłane przez użytkownika z systemem innym niż administrator uruchamia się przy użyciu lokalnego konta użytkownika systemu Linux hello takie same nazwy jako użytkownik zadania hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-167">However, a job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="ac065-168">W takim przypadku HPC Pack konfiguruje wzajemnego zaufania dla tego użytkownika w systemie Linux w węzłach hello przydzielone toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-168">In this case, HPC Pack sets up mutual trust for this Linux user across hello nodes allocated toohello job.</span></span> <span data-ttu-id="ac065-169">Przed uruchomieniem zadania hello można skonfigurować ręcznie na węzłach Linux hello użytkownika w systemie Linux hello lub HPC Pack hello użytkownika automatycznie tworzy po przesłaniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-169">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="ac065-170">Jeśli HPC Pack tworzy hello użytkownika, HPC Pack usuwa je po zakończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-170">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="ac065-171">zagrożenia bezpieczeństwa tooreduce, HPC Pack usuwa klucze powitania po zakończeniu zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-171">tooreduce security threats, HPC Pack removes hello keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="ac065-172">Konfigurowanie udziału plików dla węzłów systemu Linux</span><span class="sxs-lookup"><span data-stu-id="ac065-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="ac065-173">Teraz należy skonfigurować standardowe udziału SMB do folderu na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="ac065-173">Now set up a standard SMB share on a folder on hello head node.</span></span> <span data-ttu-id="ac065-174">tooallow hello Linux węzłów tooaccess pliki aplikacji za pomocą wspólnej ścieżki, hello instalacji węzłów Linux hello folderze udostępnionym.</span><span class="sxs-lookup"><span data-stu-id="ac065-174">tooallow hello Linux nodes tooaccess application files with a common path, mount hello shared folder on hello Linux nodes.</span></span> <span data-ttu-id="ac065-175">Jeśli chcesz, możesz użyć innego pliku opcji, takich jak udział plików Azure — zalecane dla wielu scenariuszy - lub udziału NFS do udostępniania.</span><span class="sxs-lookup"><span data-stu-id="ac065-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="ac065-176">Znajduje się w pliku hello udostępniania informacji i szczegółowy opis kroków w [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ac065-176">See hello file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="ac065-177">Utwórz folder na powitania węzła głównego i udostępnić go tooEveryone ustawiając uprawnienia odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="ac065-177">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="ac065-178">Na przykład udostępnić C:\OpenFOAM na powitania węzła głównego jako \\ \\SUSE12RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="ac065-178">For example, share C:\OpenFOAM on hello head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="ac065-179">W tym miejscu *SUSE12RDMA HN* jest nazwą hosta hello hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="ac065-179">Here, *SUSE12RDMA-HN* is hello host name of hello head node.</span></span>
2. <span data-ttu-id="ac065-180">Otwórz okno programu Windows PowerShell i uruchom hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ac065-180">Open a Windows PowerShell window and run hello following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="ac065-181">pierwsze polecenie Hello tworzy folder o nazwie /openfoam we wszystkich węzłach grupy LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-181">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="ac065-182">drugie polecenie Hello instaluje hello udostępnionego folderu //SUSE12RDMA-HN/OpenFOAM na węzłach Linux hello z dir_mode i file_mode too777 zestawu usługi bits.</span><span class="sxs-lookup"><span data-stu-id="ac065-182">hello second command mounts hello shared folder //SUSE12RDMA-HN/OpenFOAM on hello Linux nodes with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="ac065-183">Witaj *username* i *hasło* hello polecenia powinien być hello poświadczeń użytkownika na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="ac065-183">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="ac065-184">Witaj "\\`" symbol w hello drugie polecenie jest symbolem ucieczki dla środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac065-184">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="ac065-185">"\\`,"hello "oznacza, że" (przecinek znak) jest częścią polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-185">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="ac065-186">Zainstaluj MPI i OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="ac065-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="ac065-187">toorun OpenFOAM jako zadanie MPI sieci RDMA hello należy toocompile OpenFOAM z bibliotekami Intel MPI hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-187">toorun OpenFOAM as an MPI job on hello RDMA network, you need toocompile OpenFOAM with hello Intel MPI libraries.</span></span> 

<span data-ttu-id="ac065-188">Najpierw uruchom kilka **clusrun** polecenia tooinstall Intel MPI bibliotek (Jeśli nie jest jeszcze zainstalowany) i OpenFOAM na węzły systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ac065-188">First, run several **clusrun** commands tooinstall Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="ac065-189">Użyj hello węzła głównego udział wcześniej skonfigurowany plików instalacyjnych hello tooshare między węzłami Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-189">Use hello head node share configured previously tooshare hello installation files among hello Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac065-190">Te instalacji i kroki kompilacji to przykłady.</span><span class="sxs-lookup"><span data-stu-id="ac065-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="ac065-191">Należy pewna znajomość tooensure administracji systemu Linux czy kompilatory zależne i biblioteki są prawidłowo zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="ac065-191">You need some knowledge of Linux system administration tooensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="ac065-192">Może być konieczne toomodify niektórych zmiennych środowiskowych lub inne ustawienia dla Twojej wersji Intel MPI i OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="ac065-192">You might need toomodify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="ac065-193">Aby uzyskać więcej informacji, zobacz [Intel MPI biblioteki dla systemu Linux Przewodnik instalacji](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) i [OpenFOAM źródła pakietu instalacji](http://openfoam.org/download/2-3-1-source/) dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="ac065-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="ac065-194">Zainstaluj Intel MPI</span><span class="sxs-lookup"><span data-stu-id="ac065-194">Install Intel MPI</span></span>
<span data-ttu-id="ac065-195">Zapisz na powitania węzła głównego hello pobranego pakietu instalacyjnego MPI firmy Intel (l_mpi_p_5.0.3.048.tgz w tym przykładzie) w C:\OpenFoam, tak, aby węzły Linux hello mogą uzyskać dostęp do tego pliku z /openfoam.</span><span class="sxs-lookup"><span data-stu-id="ac065-195">Save hello downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="ac065-196">Następnie uruchom **clusrun** tooinstall Intel MPI biblioteki we wszystkich węzłach Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-196">Then run **clusrun** tooinstall Intel MPI library on all hello Linux nodes.</span></span>

1. <span data-ttu-id="ac065-197">następujące Hello poleceń pakietu instalacyjnego hello kopiowania i wyodrębnij go za/opt/intel w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="ac065-197">hello following commands copy hello installation package and extract it too/opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="ac065-198">tooinstall Intel MPI biblioteki w trybie dyskretnym, użyj pliku silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="ac065-198">tooinstall Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="ac065-199">Przykład można znaleźć w hello przykładowych plików na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ac065-199">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="ac065-200">Miejsce tego pliku w hello udostępnionego folderu /openfoam.</span><span class="sxs-lookup"><span data-stu-id="ac065-200">Place this file in hello shared folder /openfoam.</span></span> <span data-ttu-id="ac065-201">Aby uzyskać szczegółowe informacje o pliku silent.cfg hello, zobacz [Intel MPI biblioteki dla systemu Linux Przewodnik instalacji - instalacji dyskretnej](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="ac065-201">For details about hello silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="ac065-202">Upewnij się, że możesz zapisać plik silent.cfg jako plik tekstowy z systemem Linux zakończenia (tylko LF, nie CR LF) wierszy.</span><span class="sxs-lookup"><span data-stu-id="ac065-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="ac065-203">Ten krok zapewnia, że działa prawidłowo w węzłach Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-203">This step ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="ac065-204">Zainstaluj biblioteki MPI Intel w trybie dyskretnym.</span><span class="sxs-lookup"><span data-stu-id="ac065-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="ac065-205">Skonfiguruj MPI</span><span class="sxs-lookup"><span data-stu-id="ac065-205">Configure MPI</span></span>
<span data-ttu-id="ac065-206">Do testowania, należy dodać następujące wiersze toohello /etc/security/limits.conf na każdym z węzłów Linux hello hello:</span><span class="sxs-lookup"><span data-stu-id="ac065-206">For testing, you should add hello following lines toohello /etc/security/limits.conf on each of hello Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="ac065-207">Po zaktualizowaniu hello limits.conf pliku, należy ponownie uruchomić hello Linux węzłów.</span><span class="sxs-lookup"><span data-stu-id="ac065-207">Restart hello Linux nodes after you update hello limits.conf file.</span></span> <span data-ttu-id="ac065-208">Na przykład użyć następujących hello **clusrun** polecenia:</span><span class="sxs-lookup"><span data-stu-id="ac065-208">For example, use hello following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="ac065-209">Po ponownym uruchomieniu, upewnij się, że ten folder udostępniony hello jest zainstalowany jako /openfoam.</span><span class="sxs-lookup"><span data-stu-id="ac065-209">After restarting, ensure that hello shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="ac065-210">Kompilowanie i zainstalować OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="ac065-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="ac065-211">W węźle głównym hello należy zapisać hello pobranego pakietu instalacyjnego dla hello tooC:\OpenFoam OpenFOAM źródła pakietu (w tym przykładzie OpenFOAM-2.3.1.tgz), dzięki czemu hello Linux węzły mogą uzyskać dostęp do tego pliku z /openfoam.</span><span class="sxs-lookup"><span data-stu-id="ac065-211">Save hello downloaded installation package for hello OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) tooC:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="ac065-212">Następnie uruchom **clusrun** polecenia toocompile OpenFOAM na wszystkich hello węzłów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ac065-212">Then run **clusrun** commands toocompile OpenFOAM on all hello Linux nodes.</span></span>

1. <span data-ttu-id="ac065-213">Utwórz /opt/OpenFOAM folderu w każdym węźle Linux folderu toothis kopiowania hello źródła pakietu i wyodrębnij go brak.</span><span class="sxs-lookup"><span data-stu-id="ac065-213">Create a folder /opt/OpenFOAM on each Linux node, copy hello source package toothis folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="ac065-214">toocompile OpenFOAM z hello biblioteki MPI firmy Intel, należy najpierw skonfigurować niektóre zmienne środowiskowe Intel MPI i OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="ac065-214">toocompile OpenFOAM with hello Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="ac065-215">Użyj skryptu bash o nazwie settings.sh tooset hello zmiennych.</span><span class="sxs-lookup"><span data-stu-id="ac065-215">Use a bash script called settings.sh tooset hello variables.</span></span> <span data-ttu-id="ac065-216">Przykład można znaleźć w hello przykładowych plików na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="ac065-216">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="ac065-217">Umieść ten plik (zapisane przy użyciu zakończenia wierszy w systemie Linux) w hello udostępnionego folderu /openfoam.</span><span class="sxs-lookup"><span data-stu-id="ac065-217">Place this file (saved with Linux line endings) in hello shared folder /openfoam.</span></span> <span data-ttu-id="ac065-218">Ten plik zawiera także ustawienia hello MPI i OpenFOAM środowisk uruchomieniowych użycie nowszej toorun OpenFOAM zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-218">This file also contains settings for hello MPI and OpenFOAM runtimes that you use later toorun an OpenFOAM job.</span></span>
3. <span data-ttu-id="ac065-219">Instalowanie pakietów zależnych potrzebne toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="ac065-219">Install dependent packages needed toocompile OpenFOAM.</span></span> <span data-ttu-id="ac065-220">W zależności od dystrybucji systemu Linux należy najpierw tooadd repozytorium.</span><span class="sxs-lookup"><span data-stu-id="ac065-220">Depending on your Linux distribution, you might first need tooadd a repository.</span></span> <span data-ttu-id="ac065-221">Uruchom **clusrun** podobne toohello następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="ac065-221">Run **clusrun** commands similar toohello following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="ac065-222">W razie potrzeby SSH tooeach Linux węzła toorun hello polecenia tooconfirm, które działają prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="ac065-222">If necessary, SSH tooeach Linux node toorun hello commands tooconfirm that they run properly.</span></span>
4. <span data-ttu-id="ac065-223">Uruchom następujące polecenie toocompile OpenFOAM hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-223">Run hello following command toocompile OpenFOAM.</span></span> <span data-ttu-id="ac065-224">Proces kompilacji Hello przyjmuje niektórych toocomplete czasu i generuje dużą ilość danych wyjściowych toostandard informacji dziennika, należy więc hello **/ przeplatana** opcję przeplatana hello toodisplay w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="ac065-224">hello compilation process takes some time toocomplete and generates a large amount of log information toostandard output, so use hello **/interleaved** option toodisplay hello output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="ac065-225">Witaj "\\`" symbol w poleceniu hello jest symbolem ucieczki dla środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac065-225">hello “\\`” symbol in hello command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="ac065-226">"\\`&" oznacza hello "&" jest częścią polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-226">“\\`&” means hello “&” is a part of hello command.</span></span>
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a><span data-ttu-id="ac065-227">Przygotowanie zadania OpenFOAM toorun</span><span class="sxs-lookup"><span data-stu-id="ac065-227">Prepare toorun an OpenFOAM job</span></span>
<span data-ttu-id="ac065-228">Teraz get gotowe toorun zadań MPI wywołano sloshingTank3D, które jest jednym z przykładów OpenFoam hello, dwa węzły systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ac065-228">Now get ready toorun an MPI job called sloshingTank3D, which is one of hello OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-hello-runtime-environment"></a><span data-ttu-id="ac065-229">Konfigurowanie środowiska uruchomieniowego hello</span><span class="sxs-lookup"><span data-stu-id="ac065-229">Set up hello runtime environment</span></span>
<span data-ttu-id="ac065-230">tooset się środowiska wykonawcze hello MPI i OpenFOAM w węzłach Linux hello, uruchom następujące polecenie w oknie programu Windows PowerShell na powitania węzła głównego hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-230">tooset up hello runtime environments for MPI and OpenFOAM on hello Linux nodes, run hello following command in a Windows PowerShell window on hello head node.</span></span> <span data-ttu-id="ac065-231">(To polecenie jest prawidłowe w systemie SUSE Linux.)</span><span class="sxs-lookup"><span data-stu-id="ac065-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="ac065-232">Przygotowanie danych przykładowych</span><span class="sxs-lookup"><span data-stu-id="ac065-232">Prepare sample data</span></span>
<span data-ttu-id="ac065-233">Użyj hello węzła głównego udziału skonfigurowane wcześniej tooshare plików między węzłami Linux hello (zainstalowany jako /openfoam).</span><span class="sxs-lookup"><span data-stu-id="ac065-233">Use hello head node share you configured previously tooshare files among hello Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="ac065-234">Węzły obliczeniowe SSH tooone Twojego systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ac065-234">SSH tooone of your Linux compute nodes.</span></span>
2. <span data-ttu-id="ac065-235">Uruchom hello następujące polecenie tooset się środowisko uruchomieniowe OpenFOAM hello, jeśli jeszcze nie zostało to zrobione.</span><span class="sxs-lookup"><span data-stu-id="ac065-235">Run hello following command tooset up hello OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="ac065-236">Skopiuj folder udostępniony przykładowy toohello hello sloshingTank3D i przejdź tooit.</span><span class="sxs-lookup"><span data-stu-id="ac065-236">Copy hello sloshingTank3D sample toohello shared folder and navigate tooit.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="ac065-237">Użycie hello parametry domyślne tego przykładu, może potrwać dziesiątki toorun minut, dlatego może być toomodify niektórych toomake parametry szybsze wykonywanie.</span><span class="sxs-lookup"><span data-stu-id="ac065-237">When you use hello default parameters of this sample, it can take tens of minutes toorun, so you might want toomodify some parameters toomake it run faster.</span></span> <span data-ttu-id="ac065-238">Jeden prosty wybór jest toomodify hello czasu krok zmienne deltaT i writeInterval w pliku system/controlDict hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-238">One simple choice is toomodify hello time step variables deltaT and writeInterval in hello system/controlDict file.</span></span> <span data-ttu-id="ac065-239">Ten plik przechowuje wszystkie dane wejściowe dotyczące kontroli toohello czasu i odczytywania i zapisywania danych rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ac065-239">This file stores all input data relating toohello control of time and reading and writing solution data.</span></span> <span data-ttu-id="ac065-240">Na przykład można zmienić wartość hello deltaT z too0.5 0,05 i wartość hello writeInterval z 0,05 too0.5.</span><span class="sxs-lookup"><span data-stu-id="ac065-240">For example, you could change hello value of deltaT from 0.05 too0.5 and hello value of writeInterval from 0.05 too0.5.</span></span>
   
   ![Modyfikuj zmienne w kroku][step_variables]
5. <span data-ttu-id="ac065-242">Podaj odpowiednie wartości zmiennych hello w pliku system/decomposeParDict hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-242">Specify desired values for hello variables in hello system/decomposeParDict file.</span></span> <span data-ttu-id="ac065-243">W tym przykładzie użyto dwóch Linux węzłów każdego z 8 rdzeni, a więc Ustaw numberOfSubdomains too16 i n hierarchicalCoeffs too(1 1 16), co oznacza, że równolegle OpenFOAM z 16 procesów.</span><span class="sxs-lookup"><span data-stu-id="ac065-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains too16 and n of hierarchicalCoeffs too(1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="ac065-244">Aby uzyskać więcej informacji, zobacz [Podręcznik użytkownika OpenFOAM: 3.4 aplikacji działa równolegle](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span><span class="sxs-lookup"><span data-stu-id="ac065-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Rozłóż procesów][decompose]
6. <span data-ttu-id="ac065-246">Uruchom hello poniższych poleceń z hello sloshingTank3D katalogu tooprepare hello przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="ac065-246">Run hello following commands from hello sloshingTank3D directory tooprepare hello sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="ac065-247">W węźle głównym hello powinien pojawić się pliki danych przykładowych hello są kopiowane do C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="ac065-247">On hello head node, you should see hello sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="ac065-248">(C:\OpenFoam jest hello folderu udostępnionego na powitania węzła głównego).</span><span class="sxs-lookup"><span data-stu-id="ac065-248">(C:\OpenFoam is hello shared folder on hello head node.)</span></span>
   
   ![Pliki danych na powitania węzła głównego][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="ac065-250">Plik hosta dla mpirun</span><span class="sxs-lookup"><span data-stu-id="ac065-250">Host file for mpirun</span></span>
<span data-ttu-id="ac065-251">W tym kroku utwórz plik hostów (listy węzłów obliczeniowych) które hello **mpirun** polecenia zastosowań.</span><span class="sxs-lookup"><span data-stu-id="ac065-251">In this step, you create a host file (a list of compute nodes) which hello **mpirun** command uses.</span></span>

1. <span data-ttu-id="ac065-252">W jednym z węzłów Linux hello Utwórz plik o nazwie hostfile w obszarze /openfoam, więc ten plik jest osiągalny w /openfoam/hostfile we wszystkich węzłach systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="ac065-252">On one of hello Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="ac065-253">Zapis nazwy węzła Linux do tego pliku.</span><span class="sxs-lookup"><span data-stu-id="ac065-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="ac065-254">W tym przykładzie hello plik zawiera hello następujące nazwy:</span><span class="sxs-lookup"><span data-stu-id="ac065-254">In this example, hello file contains hello following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="ac065-255">Można też utworzyć ten plik na C:\OpenFoam\hostfile na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="ac065-255">You can also create this file at C:\OpenFoam\hostfile on hello head node.</span></span> <span data-ttu-id="ac065-256">Jeśli wybierzesz tę opcję, zapisz go jako plik tekstowy z systemem Linux zakończenia wierszy (tylko LF, nie CR LF).</span><span class="sxs-lookup"><span data-stu-id="ac065-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="ac065-257">Dzięki temu, że działa prawidłowo w węzłach Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-257">This ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="ac065-258">**Bash skryptu otoki**</span><span class="sxs-lookup"><span data-stu-id="ac065-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="ac065-259">Jeśli masz wiele węzłów systemu Linux i chcesz toorun Twojego zadania na tylko niektóre z nich, nie jest toouse dobrym rozwiązaniem, stałe hosta pliku, ponieważ nie wiadomo, węzły, które zostaną przydzielone tooyour zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-259">If you have many Linux nodes and you want your job toorun on only some of them, it’s not a good idea toouse a fixed host file, because you don’t know which nodes will be allocated tooyour job.</span></span> <span data-ttu-id="ac065-260">W takim przypadku zapisu otoka skryptu bash dla **mpirun** toocreate hello automatycznie pliku hosta.</span><span class="sxs-lookup"><span data-stu-id="ac065-260">In this case, write a bash script wrapper for **mpirun** toocreate hello host file automatically.</span></span> <span data-ttu-id="ac065-261">Można znaleźć przykład otoki skryptu bash o nazwie hpcimpirun.sh na końcu hello w tym artykule i zapisz go jako /openfoam/hpcimpirun.sh. Ten przykładowy skrypt hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ac065-261">You can find an example bash script wrapper called hpcimpirun.sh at hello end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does hello following:</span></span>
   
   1. <span data-ttu-id="ac065-262">Konfiguruje hello zmiennych środowiskowych dla **mpirun**i dodanie polecenia parametrów toorun hello MPI zadanie wywołujące za pośrednictwem sieci RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-262">Sets up hello environment variables for **mpirun**, and some addition command parameters toorun hello MPI job through hello RDMA network.</span></span> <span data-ttu-id="ac065-263">W takim przypadku ustawia hello następujące zmienne:</span><span class="sxs-lookup"><span data-stu-id="ac065-263">In this case, it sets hello following variables:</span></span>
      
      * <span data-ttu-id="ac065-264">I_MPI_FABRICS = shm:dapl</span><span class="sxs-lookup"><span data-stu-id="ac065-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="ac065-265">I_MPI_DAPL_PROVIDER = ib0-v2 — ustawienia</span><span class="sxs-lookup"><span data-stu-id="ac065-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="ac065-266">I_MPI_DYNAMIC_CONNECTION = 0</span><span class="sxs-lookup"><span data-stu-id="ac065-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="ac065-267">Tworzy plik hostów zgodnie z toohello $ zmiennej środowiskowej CCP_NODES_CORES, co jest ustawieniem węzłem głównym HPC powitania po aktywowaniu hello zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-267">Creates a host file according toohello environment variable $CCP_NODES_CORES, which is set by hello HPC head node when hello job is activated.</span></span>
      
      <span data-ttu-id="ac065-268">format Hello $CCP_NODES_CORES następujące tego wzorca:</span><span class="sxs-lookup"><span data-stu-id="ac065-268">hello format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="ac065-269">gdzie</span><span class="sxs-lookup"><span data-stu-id="ac065-269">where</span></span>
      
      * <span data-ttu-id="ac065-270">`<Number of nodes>`-toothis zadania przydzielone hello liczba węzłów.</span><span class="sxs-lookup"><span data-stu-id="ac065-270">`<Number of nodes>` - hello number of nodes allocated toothis job.</span></span>  
      * <span data-ttu-id="ac065-271">`<Name of node_n_...>`-toothis zadania przydzielone hello nazwę każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="ac065-271">`<Name of node_n_...>` - hello name of each node allocated toothis job.</span></span>
      * <span data-ttu-id="ac065-272">`<Cores of node_n_...>`-hello liczba rdzeni na powitania węzła toothis przydzielonego zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-272">`<Cores of node_n_...>` - hello number of cores on hello node allocated toothis job.</span></span>
      
      <span data-ttu-id="ac065-273">Na przykład jeśli zadanie hello wymaga dwóch węzłów toorun, $CCP_NODES_CORES jest podobny do</span><span class="sxs-lookup"><span data-stu-id="ac065-273">For example, if hello job needs two nodes toorun, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="ac065-274">Wywołania hello **mpirun** polecenie i dołącza dwa wiersza polecenia toohello parametrów.</span><span class="sxs-lookup"><span data-stu-id="ac065-274">Calls hello **mpirun** command and appends two parameters toohello command line.</span></span>
      
      * <span data-ttu-id="ac065-275">`--hostfile <hostfilepath>: <hostfilepath>`-tworzy ścieżki hello hello hosta pliku hello skryptu</span><span class="sxs-lookup"><span data-stu-id="ac065-275">`--hostfile <hostfilepath>: <hostfilepath>` - hello path of hello host file hello script creates</span></span>
      * <span data-ttu-id="ac065-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-zmienną środowiskową ustawione przez hello HPC Pack węzła głównego, który przechowuje hello liczba całkowita liczba rdzeni przydzielone toothis zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by hello HPC Pack head node, which stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="ac065-277">W takim przypadku określa hello liczbę procesów dla **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="ac065-277">In this case, it specifies hello number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="ac065-278">Prześlij zadanie OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="ac065-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="ac065-279">Teraz można przesłać zadania w Menedżerze klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="ac065-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="ac065-280">Należy toopass hello skryptu hpcimpirun.sh w wiersze polecenia hello niektórych hello zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-280">You need toopass hello script hpcimpirun.sh in hello command lines for some of hello job tasks.</span></span>

1. <span data-ttu-id="ac065-281">Połącz tooyour węzła głównego klastra i uruchom Menedżera klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="ac065-281">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="ac065-282">**W przystawce Zarządzanie zasobów**, upewnij się, że węzły obliczeniowe Linux hello w hello **Online** stanu.</span><span class="sxs-lookup"><span data-stu-id="ac065-282">**In Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="ac065-283">Jeśli nie, zaznacz je i kliknij przycisk **przejdź do trybu Online**.</span><span class="sxs-lookup"><span data-stu-id="ac065-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="ac065-284">W **zadania zarządzania**, kliknij przycisk **nowe zadanie**.</span><span class="sxs-lookup"><span data-stu-id="ac065-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="ac065-285">Wprowadź nazwę dla zadania, takie jak *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="ac065-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Szczegóły zadania][job_details]
5. <span data-ttu-id="ac065-287">W **zadania zasoby**, wybierz typ zasobu jako "Węzła" hello i ustaw hello Minimum too2.</span><span class="sxs-lookup"><span data-stu-id="ac065-287">In **Job resources**, choose hello type of resource as “Node” and set hello Minimum too2.</span></span> <span data-ttu-id="ac065-288">Ta konfiguracja uruchamia zadanie hello na dwa węzły Linux, z których każdy ma osiem rdzeni w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ac065-288">This configuration runs hello job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Zadanie zasobów][job_resources]
6. <span data-ttu-id="ac065-290">Kliknij przycisk **Edycja zadań** w hello nawigacji po lewej stronie, a następnie kliknij przycisk **Dodaj** tooadd zadania toohello zadań.</span><span class="sxs-lookup"><span data-stu-id="ac065-290">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span> <span data-ttu-id="ac065-291">Dodaj cztery zadania toohello zadania o hello następujące wiersze poleceń i ustawień.</span><span class="sxs-lookup"><span data-stu-id="ac065-291">Add four tasks toohello job with hello following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ac065-292">Uruchomiona `source /openfoam/settings.sh` konfiguruje hello OpenFOAM MPI środowiska wykonawczego środowiska i, więc każdy hello następujące zadania wywołuje przed hello OpenFOAM polecenia.</span><span class="sxs-lookup"><span data-stu-id="ac065-292">Running `source /openfoam/settings.sh` sets up hello OpenFOAM and MPI runtime environments, so each of hello following tasks calls it before hello OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="ac065-293">**Zadanie 1**.</span><span class="sxs-lookup"><span data-stu-id="ac065-293">**Task 1**.</span></span> <span data-ttu-id="ac065-294">Uruchom **decomposePar** toogenerate plików danych do uruchomienia **interDyMFoam** równolegle.</span><span class="sxs-lookup"><span data-stu-id="ac065-294">Run **decomposePar** toogenerate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="ac065-295">Przypisz jedno zadanie toohello węzła</span><span class="sxs-lookup"><span data-stu-id="ac065-295">Assign one node toohello task</span></span>
     * <span data-ttu-id="ac065-296">**Wiersz polecenia** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="ac065-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="ac065-297">**Katalog roboczy** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="ac065-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="ac065-298">Zobacz powitania po rysunku.</span><span class="sxs-lookup"><span data-stu-id="ac065-298">See hello following figure.</span></span> <span data-ttu-id="ac065-299">Podobnie można skonfigurować hello pozostałych zadań.</span><span class="sxs-lookup"><span data-stu-id="ac065-299">You configure hello remaining tasks similarly.</span></span>
     
     ![Szczegóły zadania 1][task_details1]
   * <span data-ttu-id="ac065-301">**Zadanie 2**.</span><span class="sxs-lookup"><span data-stu-id="ac065-301">**Task 2**.</span></span> <span data-ttu-id="ac065-302">Uruchom **interDyMFoam** w przykładowym hello toocompute równoległych.</span><span class="sxs-lookup"><span data-stu-id="ac065-302">Run **interDyMFoam** in parallel toocompute hello sample.</span></span>
     
     * <span data-ttu-id="ac065-303">Przypisz dwa węzły toohello zadań</span><span class="sxs-lookup"><span data-stu-id="ac065-303">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="ac065-304">**Wiersz polecenia** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="ac065-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="ac065-305">**Katalog roboczy** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="ac065-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="ac065-306">**Zadanie 3**.</span><span class="sxs-lookup"><span data-stu-id="ac065-306">**Task 3**.</span></span> <span data-ttu-id="ac065-307">Uruchom **reconstructPar** toomerge hello ustawia czas katalogów z każdego katalogu processor_N_ w pojedynczy zestaw.</span><span class="sxs-lookup"><span data-stu-id="ac065-307">Run **reconstructPar** toomerge hello sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="ac065-308">Przypisz jedno zadanie toohello węzła</span><span class="sxs-lookup"><span data-stu-id="ac065-308">Assign one node toohello task</span></span>
     * <span data-ttu-id="ac065-309">**Wiersz polecenia** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="ac065-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="ac065-310">**Katalog roboczy** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="ac065-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="ac065-311">**Zadanie 4**.</span><span class="sxs-lookup"><span data-stu-id="ac065-311">**Task 4**.</span></span> <span data-ttu-id="ac065-312">Uruchom **foamToEnsight** w tooconvert równoległych plików wyników OpenFOAM hello do EnSight formatowania i umieścić w katalogu o nazwie Ensight w przypadku katalogu hello hello EnSight pliki.</span><span class="sxs-lookup"><span data-stu-id="ac065-312">Run **foamToEnsight** in parallel tooconvert hello OpenFOAM result files into EnSight format and place hello EnSight files in a directory named Ensight in hello case directory.</span></span>
     
     * <span data-ttu-id="ac065-313">Przypisz dwa węzły toohello zadań</span><span class="sxs-lookup"><span data-stu-id="ac065-313">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="ac065-314">**Wiersz polecenia** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="ac065-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="ac065-315">**Katalog roboczy** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="ac065-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="ac065-316">Dodaj zależności toothese zadania rosnąco zadań.</span><span class="sxs-lookup"><span data-stu-id="ac065-316">Add dependencies toothese tasks in ascending task order.</span></span>
   
   ![Zależności zadań][task_dependencies]
8. <span data-ttu-id="ac065-318">Kliknij przycisk **przesyłania** toorun tego zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-318">Click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="ac065-319">Domyślnie HPC Pack przesyła zadanie hello jako konta zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ac065-319">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="ac065-320">Po kliknięciu **przesyłania**, może być wyświetlone okno dialogowe z monitem tooenter hello nazwę i hasło użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ac065-320">After you click **Submit**, you might see a dialog box prompting you tooenter hello user name and password.</span></span>
   
   ![Poświadczenia zadania][creds]
   
   <span data-ttu-id="ac065-322">W niektórych warunkach HPC Pack pamięta hello wejściowych przed i nie pokazuj tego okna dialogowego informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="ac065-322">Under some conditions, HPC Pack remembers hello user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="ac065-323">toomake HPC Pack ponownie wyświetlić, wprowadź hello następujące polecenie w wierszu polecenia, a następnie przesłać zadania hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-323">toomake HPC Pack show it again, enter hello following command at a Command prompt and then submit hello job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="ac065-324">pobiera zadanie Hello dziesiątki minut tooseveral godzin zgodnie z parametrów toohello, ustawione przez hello próbki.</span><span class="sxs-lookup"><span data-stu-id="ac065-324">hello job takes from tens of minutes tooseveral hours according toohello parameters you have set for hello sample.</span></span> <span data-ttu-id="ac065-325">Mapa cieplna hello jest widoczny hello zadania uruchomione w węzłach Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-325">In hello heat map, you see hello job running on hello Linux nodes.</span></span> 
   
   ![Mapa cieplna][heat_map]
   
   <span data-ttu-id="ac065-327">W każdym węźle osiem procesy są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="ac065-327">On each node, eight processes are started.</span></span>
   
   ![Procesy systemu Linux][linux_processes]
10. <span data-ttu-id="ac065-329">Po zakończeniu zadania hello, Znajdź foldery w C:\OpenFoam\sloshingTank3D i plików dzienników hello C:\OpenFoam hello wyniki zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-329">When hello job finishes, find hello job results in folders under C:\OpenFoam\sloshingTank3D, and hello log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="ac065-330">Wyświetl wyniki w EnSight</span><span class="sxs-lookup"><span data-stu-id="ac065-330">View results in EnSight</span></span>
<span data-ttu-id="ac065-331">Opcjonalnie użyj [EnSight](https://www.ceisoftware.com/) toovisualize i Analizuj wyniki hello hello OpenFOAM zadania.</span><span class="sxs-lookup"><span data-stu-id="ac065-331">Optionally use [EnSight](https://www.ceisoftware.com/) toovisualize and analyze hello results of hello OpenFOAM job.</span></span> <span data-ttu-id="ac065-332">Więcej informacji o wizualizacji i animacji EnSight, zobacz [przewodnik wideo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="ac065-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="ac065-333">Po zainstalowaniu EnSight na powitania węzła głównego, należy ją uruchomić.</span><span class="sxs-lookup"><span data-stu-id="ac065-333">After you install EnSight on hello head node, start it.</span></span>
2. <span data-ttu-id="ac065-334">Otwórz C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="ac065-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="ac065-335">Zostanie wyświetlony zbiornika w podglądzie hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-335">You see a tank in hello viewer.</span></span>
   
   ![Zbiornik w EnSight][tank]
3. <span data-ttu-id="ac065-337">Utwórz **Isosurface** z **internalMesh**, a następnie wybierz pozycję zmienna hello **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="ac065-337">Create an **Isosurface** from **internalMesh**, and then choose hello variable **alpha_water**.</span></span>
   
   ![Utwórz isosurface][isosurface]
4. <span data-ttu-id="ac065-339">Ustawianie koloru hello **Isosurface_part** utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-339">Set hello color for **Isosurface_part** created in hello previous step.</span></span> <span data-ttu-id="ac065-340">Na przykład ustawić go toowater niebieski.</span><span class="sxs-lookup"><span data-stu-id="ac065-340">For example, set it toowater blue.</span></span>
   
   ![Edytuj isosurface kolorów][isosurface_color]
5. <span data-ttu-id="ac065-342">Utwórz **woluminu Iso** z **ściany** wybierając **ściany** w hello **części** panelu i kliknij hello **Isosurfaces**  przycisk hello w pasku narzędzi.</span><span class="sxs-lookup"><span data-stu-id="ac065-342">Create an **Iso-volume** from **walls** by selecting **walls** in hello **Parts** panel and click hello **Isosurfaces** button in hello toolbar.</span></span>
6. <span data-ttu-id="ac065-343">Okno dialogowe hello, wybierz **typu** jako **Isovolume** i ustaw hello Min z **zakres Isovolume** too0.5.</span><span class="sxs-lookup"><span data-stu-id="ac065-343">In hello dialog box, select **Type** as **Isovolume** and set hello Min of **Isovolume range** too0.5.</span></span> <span data-ttu-id="ac065-344">toocreate hello isovolume, kliknij przycisk **Utwórz z zaznaczonych części**.</span><span class="sxs-lookup"><span data-stu-id="ac065-344">toocreate hello isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="ac065-345">Ustawianie koloru hello **Iso_volume_part** utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="ac065-345">Set hello color for **Iso_volume_part** created in hello previous step.</span></span> <span data-ttu-id="ac065-346">Na przykład ustawić limitu górnego toodeep niebieski.</span><span class="sxs-lookup"><span data-stu-id="ac065-346">For example, set it toodeep water blue.</span></span>
8. <span data-ttu-id="ac065-347">Ustawianie koloru hello **ściany**.</span><span class="sxs-lookup"><span data-stu-id="ac065-347">Set hello color for **walls**.</span></span> <span data-ttu-id="ac065-348">Na przykład ustawić go tootransparent białym znakiem.</span><span class="sxs-lookup"><span data-stu-id="ac065-348">For example, set it tootransparent white.</span></span>
9. <span data-ttu-id="ac065-349">Teraz kliknij **odtwarzanie** toosee hello wyniki hello symulacji.</span><span class="sxs-lookup"><span data-stu-id="ac065-349">Now click **Play** toosee hello results of hello simulation.</span></span>
   
    ![Wynik zbiornika][tank_result]

## <a name="sample-files"></a><span data-ttu-id="ac065-351">Przykładowe pliki</span><span class="sxs-lookup"><span data-stu-id="ac065-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="ac065-352">Przykładowy plik konfiguracyjny XML dla wdrożenia klastra za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac065-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="ac065-353">Przykładowy plik cred.xml</span><span class="sxs-lookup"><span data-stu-id="ac065-353">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a><span data-ttu-id="ac065-354">Przykładowe silent.cfg pliku tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="ac065-354">Sample silent.cfg file tooinstall MPI</span></span>
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="ac065-355">Przykładowy skrypt settings.sh</span><span class="sxs-lookup"><span data-stu-id="ac065-355">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="ac065-356">Przykładowy skrypt hpcimpirun.sh</span><span class="sxs-lookup"><span data-stu-id="ac065-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
