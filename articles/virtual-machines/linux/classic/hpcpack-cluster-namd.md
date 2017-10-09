---
title: aaaNAMD z pakietem Microsoft HPC na maszynach wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Wdrażanie klastra Microsoft HPC Pack na platformie Azure i uruchom symulacji NAMD z charmrun na wielu węzłach obliczeniowych systemu Linux"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="14024-103">Uruchamianie oprogramowania NAMD przy użyciu pakietu Microsoft HPC w węzłach obliczeniowych systemu Linux na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="14024-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="14024-104">W tym artykule przedstawiono jednokierunkowej toorun Linux wysokiej wydajności (HPC) obciążenia na maszynach wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="14024-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="14024-105">W tym miejscu można skonfigurować [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) klaster na platformie Azure z węzłami obliczeniowymi systemu Linux i uruchamianie [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate symulacji i wizualizację struktury hello dużych biomolekularnych systemu.</span><span class="sxs-lookup"><span data-stu-id="14024-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="14024-106">**NAMD** (dla programu Dynamics molekularnej Nanoscale) jest pakiet równoległych dynamics molekularnej przeznaczone do symulacji wysokiej wydajności dużych biomolekularnych systemów zawierający się toomillions atomami.</span><span class="sxs-lookup"><span data-stu-id="14024-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="14024-107">Przykładami tych systemów wirusy, komórki struktury i białek duże.</span><span class="sxs-lookup"><span data-stu-id="14024-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="14024-108">NAMD skaluje toohundreds rdzeniami dla typowych symulacje i toomore niż 500 000 rdzeniami dla symulacje największy hello.</span><span class="sxs-lookup"><span data-stu-id="14024-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="14024-109">**Microsoft HPC Pack** udostępnia funkcje toorun HPC na dużą skalę i aplikacje równoległe w klastrach komputerów lokalnych lub maszyn wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="14024-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="14024-110">Pierwotnie opracowany jako rozwiązaniem w przypadku obciążeń HPC systemu Windows HPC Pack obsługuje teraz aplikacje HPC systemu Linux w systemie Linux obliczeniowe węzła maszyn wirtualnych wdrożonych w klastrze HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="14024-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="14024-111">Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) wprowadzenie.</span><span class="sxs-lookup"><span data-stu-id="14024-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="14024-112">Dla innych opcji toorun HPC systemu Linux obciążeń na platformie Azure, zobacz [zasobów technicznych partii i wysoką wydajność pracy](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="14024-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14024-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="14024-113">Prerequisites</span></span>
* <span data-ttu-id="14024-114">**Węzły obliczeniowe HPC Pack klastra z systemem Linux** — wdrożenie klastra HPC Pack z węzłami obliczeniowymi systemu Linux na platformie Azure przy użyciu [szablonu usługi Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) lub [skrypt programu PowerShell Azure](hpcpack-cluster-powershell-script.md) .</span><span class="sxs-lookup"><span data-stu-id="14024-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="14024-115">Zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md) hello wymagania wstępne i kroki dla każdej opcji.</span><span class="sxs-lookup"><span data-stu-id="14024-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="14024-116">Jeśli wybierzesz hello opcji wdrażania skryptu programu PowerShell, zobacz hello przykładowy plik konfiguracyjny w hello przykładowych plików na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="14024-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="14024-117">Ten plik służy do konfigurowania klastra bazujących na platformie Azure HPC Pack składające się z węzłem głównym systemu Windows Server 2012 R2 i cztery węzły obliczeniowe 6.6 CentOS duży rozmiar.</span><span class="sxs-lookup"><span data-stu-id="14024-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="14024-118">Ten plik należy dostosować zgodnie z wymaganiami środowiska.</span><span class="sxs-lookup"><span data-stu-id="14024-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="14024-119">**Pliki oprogramowania i samouczek NAMD** — Pobierz NAMD oprogramowania dla systemu Linux z hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) lokacji (rejestracja wymagane).</span><span class="sxs-lookup"><span data-stu-id="14024-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="14024-120">W tym artykule jest oparta na NAMD wersji 2.10 i używa hello [Linux-x86_64 (64-bit Intel/AMD z Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archiwum.</span><span class="sxs-lookup"><span data-stu-id="14024-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="14024-121">Również pobrać hello [plików samouczka NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="14024-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="14024-122">Pobieranie Hello są pliki tar i trzeba plików systemu Windows hello tooextract narzędzia na powitania węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="14024-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="14024-123">tooextract hello pliki, wykonaj instrukcje hello w dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="14024-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="14024-124">**VMD** (opcjonalnie) — toosee hello wyników zadania NAMD, Pobierz i zainstaluj program molekularnej wizualizacji hello [VMD](http://www.ks.uiuc.edu/Research/vmd/) na wybranym komputerze.</span><span class="sxs-lookup"><span data-stu-id="14024-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="14024-125">Bieżąca wersja Hello jest 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="14024-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="14024-126">Zobacz hello VMD Pobierz tooget lokacji uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="14024-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="14024-127">Konfigurowanie wzajemnego zaufania między węzły obliczeń</span><span class="sxs-lookup"><span data-stu-id="14024-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="14024-128">Uruchomienie zadania między węzłami na wielu węzłach Linux wymaga tootrust węzłów hello wzajemnie (przez **rsh** lub **ssh**).</span><span class="sxs-lookup"><span data-stu-id="14024-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="14024-129">Po utworzeniu klastra HPC Pack hello z hello Microsoft HPC Pack IaaS skrypt wdrożenia skryptu hello automatycznie konfiguruje stałe wzajemnego zaufania dla konta administratora hello, które określisz.</span><span class="sxs-lookup"><span data-stu-id="14024-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="14024-130">Dla użytkowników niebędących administratorami utworzonych w domenie hello klastra masz tooset tymczasowego relacji wzajemnego zaufania między węzłami hello gdy zadanie jest przydzielany toothem.</span><span class="sxs-lookup"><span data-stu-id="14024-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="14024-131">Następnie należy zniszczyć hello relacji po zakończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="14024-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="14024-132">toodo to dla każdego użytkownika, podaj klastra toohello parę kluczy RSA które HPC Pack korzysta z relacji zaufania hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="14024-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="14024-133">Postępuj zgodnie z instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="14024-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="14024-134">Generowanie pary kluczy RSA</span><span class="sxs-lookup"><span data-stu-id="14024-134">Generate an RSA key pair</span></span>
<span data-ttu-id="14024-135">Łatwe toogenerate parę kluczy RSA, który zawiera klucz publiczny i klucz prywatny, uruchamiając hello Linux **ssh-keygen** polecenia.</span><span class="sxs-lookup"><span data-stu-id="14024-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="14024-136">Zaloguj się na tooa komputera z systemem Linux.</span><span class="sxs-lookup"><span data-stu-id="14024-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="14024-137">Uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="14024-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="14024-138">Naciśnij klawisz **Enter** toouse hello domyślne ustawienia ukończenie hello polecenia.</span><span class="sxs-lookup"><span data-stu-id="14024-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="14024-139">Nie należy wprowadzać hasło tutaj; Po wyświetleniu monitu o podanie hasła, wystarczy nacisnąć klawisz **Enter**.</span><span class="sxs-lookup"><span data-stu-id="14024-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Generowanie pary kluczy RSA][keygen]
3. <span data-ttu-id="14024-141">Zmień katalog ~/.ssh toohello katalogu.</span><span class="sxs-lookup"><span data-stu-id="14024-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="14024-142">Witaj klucz prywatny jest przechowywany w id_rsa i hello klucz publiczny w id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="14024-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Klucze prywatne i publiczne][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="14024-144">Dodaj klaster HPC Pack toohello pary kluczy hello</span><span class="sxs-lookup"><span data-stu-id="14024-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="14024-145">[Połącz przez pulpit zdalny](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello węzła głównego maszynę Wirtualną przy użyciu hello poświadczeń domeny podana podczas wdrażania klastra hello (na przykład hpc\clusteradmin).</span><span class="sxs-lookup"><span data-stu-id="14024-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="14024-146">Witaj klastra można zarządzać z węzła głównego hello.</span><span class="sxs-lookup"><span data-stu-id="14024-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="14024-147">Używanie standardowych systemu Windows Server toocreate procedury konto użytkownika domeny w domenie usługi Active Directory hello klastra.</span><span class="sxs-lookup"><span data-stu-id="14024-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="14024-148">Na przykład użyć hello użytkowników usługi Active Directory i narzędzia komputerów na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="14024-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="14024-149">Przykłady Hello w tym artykule przyjęto założenie, że utworzenie użytkownika domeny o nazwie hpcuser w domenie hpclab hello (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="14024-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="14024-150">Dodawanie hello domeny użytkownika toohello HPC Pack klastra jako użytkownika klastra.</span><span class="sxs-lookup"><span data-stu-id="14024-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="14024-151">Aby uzyskać instrukcje, zobacz [Dodaj lub usuń użytkowników klastra](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="14024-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="14024-152">Utwórz plik o nazwie C:\cred.xml i skopiuj hello RSA danych klucza do niego.</span><span class="sxs-lookup"><span data-stu-id="14024-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="14024-153">Przykład można znaleźć w hello przykładowych plików na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="14024-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="14024-154">Otwórz wiersz polecenia i wpisz następujące polecenia, które tooset hello poświadczenia danych dla konta hpclab\hpcuser hello hello.</span><span class="sxs-lookup"><span data-stu-id="14024-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="14024-155">Użyj hello **extendeddata** toopass parametru hello nazwę pliku C:\cred.xml hello utworzony hello danych.</span><span class="sxs-lookup"><span data-stu-id="14024-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="14024-156">To polecenie zakończy się pomyślnie bez danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="14024-156">This command completes successfully without output.</span></span> <span data-ttu-id="14024-157">Po ustawieniu hello poświadczeń dla kont użytkowników hello potrzebne toorun zadania, przechowuj plik cred.xml hello w bezpiecznej lokalizacji lub usuń go.</span><span class="sxs-lookup"><span data-stu-id="14024-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="14024-158">Wygenerowany hello parę kluczy RSA w jednym z węzłów z systemem Linux Pamiętaj klucze hello toodelete po zakończeniu korzystania z nich.</span><span class="sxs-lookup"><span data-stu-id="14024-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="14024-159">HPC Pack nie konfiguruje wzajemnego zaufania w przypadku odnalezienia istniejącego pliku id_rsa lub id_rsa.pub pliku.</span><span class="sxs-lookup"><span data-stu-id="14024-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="14024-160">Nie zaleca się uruchamiania zadania Linux jako administrator klastra w klastrze udostępniony, ponieważ przesłane przez administratora zadania działa w ramach konta głównego hello na powitania Linux węzłów.</span><span class="sxs-lookup"><span data-stu-id="14024-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="14024-161">Zadania zostało przesłane przez użytkownika bez uprawnień administratora jest uruchamiany przy użyciu lokalnego konta użytkownika systemu Linux, hello takie same nazwy jako hello zadania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="14024-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="14024-162">W takim przypadku HPC Pack konfiguruje wzajemnego zaufania dla tego użytkownika w systemie Linux we wszystkich węzłach hello przydzielone toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="14024-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="14024-163">Przed uruchomieniem zadania hello można skonfigurować ręcznie na węzłach Linux hello użytkownika w systemie Linux hello lub HPC Pack hello użytkownika automatycznie tworzy po przesłaniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="14024-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="14024-164">Jeśli HPC Pack tworzy hello użytkownika, HPC Pack usuwa je po zakończeniu zadania hello.</span><span class="sxs-lookup"><span data-stu-id="14024-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="14024-165">tooreduce zagrożeniem bezpieczeństwa, powitalne klucze są usuwane po zakończeniu zadania hello na węzłach hello.</span><span class="sxs-lookup"><span data-stu-id="14024-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="14024-166">Konfigurowanie udziału plików dla węzłów systemu Linux</span><span class="sxs-lookup"><span data-stu-id="14024-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="14024-167">Teraz skonfigurować udział plików SMB i instalacji hello folderu udostępnionego na wszystkie Linux węzłów tooallow hello Linux węzłów tooaccess NAMD pliki z wspólnej ścieżki.</span><span class="sxs-lookup"><span data-stu-id="14024-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="14024-168">Poniżej przedstawiono kroki toomount folderu udostępnionego na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="14024-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="14024-169">Takie jak CentOS 6.6 dystrybucji, które aktualnie nie obsługują usługę Azure plików hello udział jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="14024-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="14024-170">Jeśli węzły Linux obsługują udziału plików platformy Azure, zobacz [jak toouse magazyn plików Azure z systemem Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="14024-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="14024-171">W przypadku pliku dodatkowe opcje udostępniania pakietem HPC, zobacz [wprowadzenie węzły obliczeniowe systemu Linux w klastrze HPC Pack na platformie Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="14024-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="14024-172">Utwórz folder na powitania węzła głównego i udostępnić go tooEveryone ustawiając uprawnienia odczytu/zapisu.</span><span class="sxs-lookup"><span data-stu-id="14024-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="14024-173">W tym przykładzie \\ \\CentOS66HN\Namd jest nazwą hello hello folderu, gdzie CentOS66HN jest nazwą hosta hello hello węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="14024-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="14024-174">Utwórz podfolder o nazwie namd2 w folderze udostępnionym hello.</span><span class="sxs-lookup"><span data-stu-id="14024-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="14024-175">W namd2 należy utworzyć inny podfolder o nazwie namdsample.</span><span class="sxs-lookup"><span data-stu-id="14024-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="14024-176">Wyodrębnij pliki NAMD hello w folderze hello przy użyciu wersji systemu Windows z **tar** lub innego narzędzia systemu Windows, który operuje na archiwa tar.</span><span class="sxs-lookup"><span data-stu-id="14024-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="14024-177">Wyodrębnij hello NAMD tar archiwum zbyt\\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="14024-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="14024-178">Wyodrębnij pliki samouczka hello w obszarze \\ \\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="14024-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="14024-179">Otwórz okno programu Windows PowerShell i uruchom następujące polecenia toomount hello folderu udostępnionego na węzłach Linux hello hello.</span><span class="sxs-lookup"><span data-stu-id="14024-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="14024-180">pierwsze polecenie Hello tworzy folder o nazwie /namd2 we wszystkich węzłach grupy LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="14024-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="14024-181">drugie polecenie Hello instaluje hello udostępnionego folderu //CentOS66HN/Namd/namd2 na powitania folder o dir_mode i file_mode too777 zestawu usługi bits.</span><span class="sxs-lookup"><span data-stu-id="14024-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="14024-182">Witaj *username* i *hasło* hello polecenia powinien być hello poświadczeń użytkownika na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="14024-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="14024-183">Witaj "\\`" symbol w hello drugie polecenie jest symbolem ucieczki dla środowiska PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14024-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="14024-184">"\\`,"hello "oznacza, że" (przecinek znak) jest częścią polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="14024-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="14024-185">Utwórz zadanie NAMD toorun skryptu Bash</span><span class="sxs-lookup"><span data-stu-id="14024-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="14024-186">Zadanie NAMD musi *wstawienia* plik **charmrun** toodetermine hello liczba węzłów toouse podczas uruchamiania procesów NAMD.</span><span class="sxs-lookup"><span data-stu-id="14024-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="14024-187">Możesz użyć skryptu Bash, który generuje plik wstawienia hello i uruchamia **charmrun** z tym plikiem wstawienia.</span><span class="sxs-lookup"><span data-stu-id="14024-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="14024-188">Następnie można przesłać zadania NAMD w Menedżer klastra HPC, który wywołuje ten skrypt.</span><span class="sxs-lookup"><span data-stu-id="14024-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="14024-189">Za pomocą dowolnego edytora tekstu, utworzyć skrypt Bash w hello /namd2 folderu zawierającego pliki programów NAMD hello i nadaj mu nazwę hpccharmrun.sh. W przypadku szybkiego Weryfikacja koncepcji, skopiuj hello skrypt hpccharmrun.sh podana na końcu hello w tym artykule i przejść za[przesłać zadania NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="14024-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="14024-190">Zapisz skrypt jako plik tekstowy z systemem Linux zakończenia (tylko LF, nie CR LF) wierszy.</span><span class="sxs-lookup"><span data-stu-id="14024-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="14024-191">Dzięki temu, że działa prawidłowo w węzłach Linux hello.</span><span class="sxs-lookup"><span data-stu-id="14024-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="14024-192">Poniżej przedstawiono szczegółowe informacje o czego ten skrypt bash.</span><span class="sxs-lookup"><span data-stu-id="14024-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="14024-193">Zdefiniuj niektóre zmienne.</span><span class="sxs-lookup"><span data-stu-id="14024-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="14024-194">Pobierz informacje węzła z hello zmiennych środowiskowych.</span><span class="sxs-lookup"><span data-stu-id="14024-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="14024-195">$NODESCORES przechowuje listę słów podziału z $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="14024-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="14024-196">$COUNT jest rozmiarem hello $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="14024-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="14024-197">format Hello zmiennej CCP_NODES_CORES $ hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="14024-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="14024-198">Ta zmienna wymieniono hello łączna liczba węzłów, nazwy węzła i liczba rdzeni w każdym węźle przydzielonych toohello zadania.</span><span class="sxs-lookup"><span data-stu-id="14024-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="14024-199">Na przykład jeśli zadanie hello musi 10 toorun rdzeni, wartość hello $CCP_NODES_CORES jest podobny do:</span><span class="sxs-lookup"><span data-stu-id="14024-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="14024-200">Jeśli nie ustawiono zmiennej CCP_NODES_CORES $ hello, uruchom **charmrun** bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="14024-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="14024-201">(Ten może występować tylko po uruchomieniu tego skryptu bezpośrednio na węzły systemu Linux.)</span><span class="sxs-lookup"><span data-stu-id="14024-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="14024-202">Lub Utwórz plik wstawienia **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="14024-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="14024-203">Uruchom **charmrun** z plikiem wstawienia hello, Pobierz stanu powrotu, a następnie usuń plik wstawienia hello na końcu hello.</span><span class="sxs-lookup"><span data-stu-id="14024-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="14024-204">${CCP_NUMCPUS} jest ustawiony przez węzłem głównym HPC Pack hello innej zmiennej środowiskowej.</span><span class="sxs-lookup"><span data-stu-id="14024-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="14024-205">Przechowuje hello liczba całkowita liczba rdzeni przydzielone toothis zadania.</span><span class="sxs-lookup"><span data-stu-id="14024-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="14024-206">Będziemy używać go toospecify hello liczba procesów charmrun.</span><span class="sxs-lookup"><span data-stu-id="14024-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="14024-207">Wyjście z hello **charmrun** stan powrotu.</span><span class="sxs-lookup"><span data-stu-id="14024-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="14024-208">Poniżej przedstawiono informacje hello w pliku wstawienia hello, w którym skrypt hello generuje:</span><span class="sxs-lookup"><span data-stu-id="14024-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="14024-209">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="14024-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="14024-210">Prześlij zadanie NAMD</span><span class="sxs-lookup"><span data-stu-id="14024-210">Submit a NAMD job</span></span>
<span data-ttu-id="14024-211">Teraz wszystko jest gotowe toosubmit NAMD zadania w Menedżerze klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="14024-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="14024-212">Połącz tooyour węzła głównego klastra i uruchom Menedżera klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="14024-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="14024-213">W **zarządzanie zasobami**, upewnij się, że węzły obliczeniowe Linux hello w hello **Online** stanu.</span><span class="sxs-lookup"><span data-stu-id="14024-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="14024-214">Jeśli nie, zaznacz je i kliknij przycisk **przejdź do trybu Online**.</span><span class="sxs-lookup"><span data-stu-id="14024-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="14024-215">W **zadania zarządzania**, kliknij przycisk **nowe zadanie**.</span><span class="sxs-lookup"><span data-stu-id="14024-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="14024-216">Wprowadź nazwę dla zadania, takie jak *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="14024-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Nowe zadanie HPC][namd_job]
5. <span data-ttu-id="14024-218">Na powitania **szczegóły zadania** w obszarze **zasobów zadania**, wybierz typ hello zasobu jako **węzła** i zestaw hello **Minimum** too3.</span><span class="sxs-lookup"><span data-stu-id="14024-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="14024-219">, możemy uruchomić zadania hello na trzy węzły systemu Linux i każdy węzeł ma cztery rdzenie.</span><span class="sxs-lookup"><span data-stu-id="14024-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![Zadanie zasobów][job_resources]
6. <span data-ttu-id="14024-221">Kliknij przycisk **Edycja zadań** w hello nawigacji po lewej stronie, a następnie kliknij przycisk **Dodaj** tooadd zadania toohello zadań.</span><span class="sxs-lookup"><span data-stu-id="14024-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="14024-222">Na powitania **szczegółów zadań i Przekierowanie We/Wy** strony hello ustaw następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="14024-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="14024-223">**Wiersz polecenia**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="14024-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="14024-224">Witaj poprzedniego wiersza polecenia jest jednego polecenia bez podziałów wierszy.</span><span class="sxs-lookup"><span data-stu-id="14024-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="14024-225">W wielu wierszach, w obszarze jest zawijana tooappear **wiersza polecenia**.</span><span class="sxs-lookup"><span data-stu-id="14024-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="14024-226">**Katalog roboczy** -/namd2</span><span class="sxs-lookup"><span data-stu-id="14024-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="14024-227">**Co najmniej** — 3</span><span class="sxs-lookup"><span data-stu-id="14024-227">**Minimum** - 3</span></span>
     
     ![Szczegóły zadania][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="14024-229">W tym miejscu ustawić katalogu roboczego hello ponieważ **charmrun** próbuje toonavigate toohello tego samego katalogu roboczego w każdym węźle.</span><span class="sxs-lookup"><span data-stu-id="14024-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="14024-230">Jeśli nie ustawiono katalogu roboczego hello, HPC Pack uruchamia polecenie hello w losowo wybranej nazwie folder utworzony w jednym z węzłów Linux hello.</span><span class="sxs-lookup"><span data-stu-id="14024-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="14024-231">Powoduje to hello następujący błąd na powitania innych węzłów: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid ten problem, określ ścieżkę folderu, które są dostępne przez wszystkie węzły hello katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="14024-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="14024-232">Kliknij przycisk **OK** , a następnie kliknij przycisk **przesyłania** toorun tego zadania.</span><span class="sxs-lookup"><span data-stu-id="14024-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="14024-233">Domyślnie HPC Pack przesyła zadanie hello jako konta zalogowanego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="14024-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="14024-234">Okno dialogowe może monitować tooenter hello nazwę i hasło użytkownika po kliknięciu **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="14024-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![Poświadczenia zadania][creds]
   
   <span data-ttu-id="14024-236">W niektórych warunkach HPC Pack pamięta hello wejściowych przed i nie pokazuj tego okna dialogowego informacje o użytkowniku.</span><span class="sxs-lookup"><span data-stu-id="14024-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="14024-237">toomake HPC Pack ponownie wyświetlić, wprowadź hello następujące polecenie w wierszu polecenia, a następnie przesłać zadania hello.</span><span class="sxs-lookup"><span data-stu-id="14024-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="14024-238">zadanie Hello zajmuje kilka minut toofinish.</span><span class="sxs-lookup"><span data-stu-id="14024-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="14024-239">Znajdź dziennik zadań hello na \\ <headnodeName>pliki wyjściowe \Namd\namd2\namd2_hpccharmrun.log i hello \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="14024-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="14024-240">Opcjonalnie można uruchomić VMD tooview wyniki zadania.</span><span class="sxs-lookup"><span data-stu-id="14024-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="14024-241">kroki Hello do wizualizacji pliki wyjściowe NAMD hello (w tym przypadku związku białka ubiquitin, w zakresie limitu górnego) są poza zakres tego artykułu hello.</span><span class="sxs-lookup"><span data-stu-id="14024-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="14024-242">Zobacz [samouczek NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="14024-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Wyniki zadania][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="14024-244">Przykładowe pliki</span><span class="sxs-lookup"><span data-stu-id="14024-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="14024-245">Przykładowy plik konfiguracyjny XML dla wdrożenia klastra za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="14024-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="14024-246">Przykładowy plik cred.xml</span><span class="sxs-lookup"><span data-stu-id="14024-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="14024-247">Przykładowy skrypt hpccharmrun.sh</span><span class="sxs-lookup"><span data-stu-id="14024-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
