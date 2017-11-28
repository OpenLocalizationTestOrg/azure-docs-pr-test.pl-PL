---
title: "aaaSet się hybrydowego HPC Pack klastra na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Microsoft HPC Pack i Azure tooset Konfigurowanie mały, hybrydowego wysokiej wydajności przetwarzania danych (HPC) klastra"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="c921e-103">Skonfiguruj hybrydowych wysokiej wydajności obliczeniowej klastra (HPC) z pakietu Microsoft HPC Pack i węzłów obliczeń platformy Azure na żądanie</span><span class="sxs-lookup"><span data-stu-id="c921e-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="c921e-104">Za pomocą programu Microsoft HPC Pack 2012 R2 i Azure tooset wydajności małych, wysokiej hybrydowych, obliczeniowych klastra (HPC).</span><span class="sxs-lookup"><span data-stu-id="c921e-104">Use Microsoft HPC Pack 2012 R2 and Azure tooset up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="c921e-105">klaster Hello wyświetlane w tym artykule składa się z węzłem głównym HPC Pack lokalnymi i niektóre wyliczenia węzłów wdrażanie na żądanie w systemie Azure usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c921e-105">hello cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="c921e-106">Następnie możesz uruchomić zadania obliczeń na powitania hybrydowego klastra.</span><span class="sxs-lookup"><span data-stu-id="c921e-106">You can then run compute jobs on hello hybrid cluster.</span></span>

![Klaster HPC hybrydowego][Overview] 

<span data-ttu-id="c921e-108">Ten samouczek pokazuje, jednym z podejść jest czasami nazywany klastra "serii toohello chmury," toouse skalowalne, na żądanie zasobów Azure toorun obliczeniowych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c921e-108">This tutorial shows one approach, sometimes called cluster "burst toohello cloud," toouse scalable, on-demand Azure resources toorun compute-intensive applications.</span></span>

<span data-ttu-id="c921e-109">Ten samouczek zakłada nie doświadczenie z lub klastry obliczeniowe HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="c921e-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="c921e-110">Jest zamierzone toohelp tylko w przypadku wdrażania klastra obliczeniowego hybrydowego szybko w celach demonstracyjnych.</span><span class="sxs-lookup"><span data-stu-id="c921e-110">It is intended only toohelp you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="c921e-111">Zagadnienia i czynności toodeploy hybrydowego HPC Pack klastra na większą skalę w środowisku produkcyjnym lub toouse HPC Pack 2016, można znaleźć hello [szczegółowe wskazówki](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="c921e-111">For considerations and steps toodeploy a hybrid HPC Pack cluster at greater scale in a production environment, or toouse HPC Pack 2016, see hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="c921e-112">W innych sytuacjach pakietem HPC łącznie z automatycznego wdrażania klastra na maszynach wirtualnych Azure, zobacz [opcje klastra HPC z pakietem Microsoft HPC w systemie Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c921e-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c921e-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c921e-113">Prerequisites</span></span>
* <span data-ttu-id="c921e-114">**Subskrypcja platformy Azure** — Jeśli nie masz subskrypcji platformy Azure, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c921e-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="c921e-115">**Na komputerze lokalnym systemem Windows Server 2012 R2 lub Windows Server 2012** -używa tego komputera jako hello węzła głównego klastra HPC hello.</span><span class="sxs-lookup"><span data-stu-id="c921e-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as hello head node of hello HPC cluster.</span></span> <span data-ttu-id="c921e-116">Jeśli nie są już systemem Windows Server, musisz pobrać i zainstalować [wersji ewaluacyjnej](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="c921e-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="c921e-117">Witaj, komputer musi być tooan przyłączone do domeny usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c921e-117">hello computer must be joined tooan Active Directory domain.</span></span> <span data-ttu-id="c921e-118">Do celów testowych można skonfigurować hello węzła głównego komputer jako kontroler domeny.</span><span class="sxs-lookup"><span data-stu-id="c921e-118">For test purposes, you can configure hello head node computer as a domain controller.</span></span> <span data-ttu-id="c921e-119">tooadd hello roli serwera usług domenowych w usłudze Active Directory i promować hello węzła głównego komputer jako kontroler domeny, zobacz dokumentację hello systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c921e-119">tooadd hello Active Directory Domain Services server role and promote hello head node computer as a domain controller, see hello documentation for Windows Server.</span></span>
  * <span data-ttu-id="c921e-120">toosupport HPC Pack hello systemu operacyjnego musi być zainstalowany w jednej z tych językach: angielski, japoński lub angielski, chiński (uproszczony).</span><span class="sxs-lookup"><span data-stu-id="c921e-120">toosupport HPC Pack, hello operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="c921e-121">Sprawdź, czy krytycznych i ważne aktualizacje są instalowane.</span><span class="sxs-lookup"><span data-stu-id="c921e-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="c921e-122">**HPC Pack 2012 R2** - [Pobierz](http://go.microsoft.com/fwlink/p/?linkid=328024) hello pakiet instalacyjny dla hello najnowszej wersji bez opłat i skopiuj hello pliki toohello węzła głównego komputera.</span><span class="sxs-lookup"><span data-stu-id="c921e-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) hello installation package for hello latest version free of charge and copy hello files toohello head node computer.</span></span> <span data-ttu-id="c921e-123">Wybierz pliki instalacyjne w hello sam język jako instalacji systemu Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c921e-123">Choose installation files in hello same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="c921e-124">Jeśli chcesz toouse HPC Pack 2016 zamiast HPC Pack 2012 R2, są wymagane dodatkowe czynności konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="c921e-124">If you want toouse HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="c921e-125">Zobacz hello [szczegółowe wskazówki](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="c921e-125">See hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="c921e-126">**Konto domeny** — to konto musi mieć prawa administratora lokalnego na powitania tooinstall węzłem głównym HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="c921e-126">**Domain account** - This account must be configured with local Administrator permissions on hello head node tooinstall HPC Pack.</span></span>
* <span data-ttu-id="c921e-127">**Połączenie TCP na porcie 443** z hello tooAzure węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="c921e-127">**TCP connectivity on port 443** from hello head node tooAzure.</span></span>

## <a name="install-hpc-pack-on-hello-head-node"></a><span data-ttu-id="c921e-128">Zainstaluj pakiet HPC na powitania węzła głównego</span><span class="sxs-lookup"><span data-stu-id="c921e-128">Install HPC Pack on hello head node</span></span>
<span data-ttu-id="c921e-129">Microsoft HPC Pack należy najpierw zainstalować na komputerze lokalnym systemem Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c921e-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="c921e-130">Ten komputer staje się hello węzła głównego klastra hello.</span><span class="sxs-lookup"><span data-stu-id="c921e-130">This computer becomes hello head node of hello cluster.</span></span>

1. <span data-ttu-id="c921e-131">Zaloguj się na węzła głównego toohello przy użyciu konta domeny, które ma uprawnienia administratora lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c921e-131">Log on toohello head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="c921e-132">Uruchom Kreatora instalacji pakietu HPC hello uruchamiania programu Setup.exe z plików instalacyjnych hello HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="c921e-132">Start hello HPC Pack Installation Wizard by running Setup.exe from hello HPC Pack installation files.</span></span>

3. <span data-ttu-id="c921e-133">Na powitania **Instalator HPC Pack 2012 R2** kliknij **nowej instalacji lub Dodaj nowe funkcje tooan istniejącej instalacji**.</span><span class="sxs-lookup"><span data-stu-id="c921e-133">On hello **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features tooan existing installation**.</span></span>

    ![HPC Pack 2012 Instalatora][install_hpc1]

4. <span data-ttu-id="c921e-135">Na powitania **strony Umowy użytkownika oprogramowania Microsoft**, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c921e-135">On hello **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="c921e-136">Na powitania **Wybieranie typu instalacji** kliknij przycisk **utworzenie nowego klastra HPC, tworząc węzła głównego**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c921e-136">On hello **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="c921e-137">Kreator Hello działa wiele testów przed instalacją.</span><span class="sxs-lookup"><span data-stu-id="c921e-137">hello wizard runs several pre-installation tests.</span></span> <span data-ttu-id="c921e-138">Kliknij przycisk **dalej** na powitania **reguły instalacji** strony, jeśli wszystkie testy zostały zaliczone pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c921e-138">Click **Next** on hello **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="c921e-139">W przeciwnym razie Przejrzyj podane informacje hello i wprowadź niezbędne zmiany w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="c921e-139">Otherwise, review hello information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="c921e-140">Następnie uruchom ponownie testów hello lub jeśli niezbędne start Witaj ponownie Kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="c921e-140">Then run hello tests again or if necessary start hello Installation Wizard again.</span></span>
7. <span data-ttu-id="c921e-141">Na powitania **konfiguracji bazy danych HPC** upewnij się, że **Head, węzła** jest zaznaczone dla wszystkich baz danych HPC, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c921e-141">On hello **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![Konfiguracja bazy danych][install_hpc4]

8. <span data-ttu-id="c921e-143">Zaakceptuj domyślne na pozostałych stronach kreatora hello hello.</span><span class="sxs-lookup"><span data-stu-id="c921e-143">Accept default selections on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="c921e-144">Na powitania **zainstalować wymagane składniki** kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="c921e-144">On hello **Install Required Components** page, click **Install**.</span></span>
   
    ![Instalowanie][install_hpc6]

9. <span data-ttu-id="c921e-146">Po zakończeniu instalacji hello, usuń zaznaczenie pola wyboru **Uruchom Menedżera klastra HPC** , a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="c921e-146">After hello installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="c921e-147">(Można uruchomić Menedżera klastra HPC w kolejnym kroku.)</span><span class="sxs-lookup"><span data-stu-id="c921e-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Zakończ][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a><span data-ttu-id="c921e-149">Przygotowanie hello subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c921e-149">Prepare hello Azure subscription</span></span>
<span data-ttu-id="c921e-150">Wykonaj następujące kroki w hello hello [portalu Azure](https://portal.azure.com) z subskrypcją platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c921e-150">Perform hello following steps in hello [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="c921e-151">Po wykonaniu tych czynności można wdrożyć węzły platformy Azure z węzłem głównym lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="c921e-151">After completing these steps, you can deploy Azure nodes from hello on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="c921e-152">Również Zanotuj identyfikator subskrypcji platformy Azure, która jest potrzebna później.</span><span class="sxs-lookup"><span data-stu-id="c921e-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="c921e-153">Identyfikator hello w **subskrypcje** w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="c921e-153">Find hello ID in **Subscriptions** in hello portal.</span></span>
  > 

### <a name="upload-hello-default-management-certificate"></a><span data-ttu-id="c921e-154">Przekaż hello domyślnego certyfikatu zarządzania</span><span class="sxs-lookup"><span data-stu-id="c921e-154">Upload hello default management certificate</span></span>
<span data-ttu-id="c921e-155">HPC Pack instaluje certyfikat z podpisem własnym na powitania węzła głównego, nazywany hello domyślne Microsoft HPC Azure Management certyfikatu, który można przekazać jako certyfikat zarządzania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c921e-155">HPC Pack installs a self-signed certificate on hello head node, called hello Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="c921e-156">Ten certyfikat jest dostępne w celu testowania i weryfikacja koncepcji wdrożenia toosecure hello połączenie między hello węzła głównego i Azure.</span><span class="sxs-lookup"><span data-stu-id="c921e-156">This certificate is provided for testing and proof-of-concept deployments toosecure hello connection between hello head node and Azure.</span></span>

1. <span data-ttu-id="c921e-157">Z komputera z węzłem głównym hello, zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c921e-157">From hello head node computer, sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="c921e-158">Kliknij przycisk **subskrypcje** > *your_subscription_name*.</span><span class="sxs-lookup"><span data-stu-id="c921e-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="c921e-159">Kliknij przycisk **certyfikaty zarządzania** > **przekazać**.4.</span><span class="sxs-lookup"><span data-stu-id="c921e-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="c921e-160">Przejdź na powitania węzła głównego hello pliku C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="c921e-160">Browse on hello head node for hello file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="c921e-161">Następnie kliknij przycisk **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="c921e-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="c921e-162">Witaj **domyślne HPC Azure Management** certyfikatu jest widoczna na liście hello certyfikaty zarządzania.</span><span class="sxs-lookup"><span data-stu-id="c921e-162">hello **Default HPC Azure Management** certificate appears in hello list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="c921e-163">Tworzenie usługi w chmurze platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c921e-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="c921e-164">Aby uzyskać najlepszą wydajność, należy utworzyć w hello hello usługa w chmurze i hello konta magazynu (w kolejnym kroku) tym samym regionie geograficznym.</span><span class="sxs-lookup"><span data-stu-id="c921e-164">For best performance, create hello cloud service and hello storage account (in a later step) in hello same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="c921e-165">W portalu powitania kliknij **usługi (klasyczne) w chmurze** > **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c921e-165">In hello portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="c921e-166">Wpisz nazwę DNS usługi hello, wybierz grupę zasobów i lokalizację, a następnie kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c921e-166">Type a DNS name for hello service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="c921e-167">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c921e-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="c921e-168">W portalu powitania kliknij **kont magazynu (klasyczne)** > **+ Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c921e-168">In hello portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="c921e-169">Wpisz nazwę konta hello i wybierz hello **klasycznego** modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c921e-169">Type a name for hello account, and select hello **Classic** deployment model.</span></span>

3. <span data-ttu-id="c921e-170">Wybierz grupę zasobów i lokalizację i pozostaw innych ustawień na wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="c921e-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="c921e-171">Następnie kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="c921e-171">Then click **Create**.</span></span>

## <a name="configure-hello-head-node"></a><span data-ttu-id="c921e-172">Skonfiguruj hello węzła głównego</span><span class="sxs-lookup"><span data-stu-id="c921e-172">Configure hello head node</span></span>
<span data-ttu-id="c921e-173">Menedżer klastrów HPC toodeploy toouse węzły platformy Azure i zadania toosubmit najpierw wykonać pewne czynności konfiguracyjne wymagane klastra.</span><span class="sxs-lookup"><span data-stu-id="c921e-173">toouse HPC Cluster Manager toodeploy Azure nodes and toosubmit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="c921e-174">Na powitania węzła głównego Uruchom Menedżera klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="c921e-174">On hello head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="c921e-175">Jeśli hello **wybierz węzeł Head** zostanie wyświetlone okno dialogowe, kliknij przycisk **komputera lokalnego**.</span><span class="sxs-lookup"><span data-stu-id="c921e-175">If hello **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="c921e-176">Witaj **listy zadań do wykonania wdrożenia** pojawi się.</span><span class="sxs-lookup"><span data-stu-id="c921e-176">hello **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="c921e-177">W obszarze **wymagane zadania wdrażania**, kliknij przycisk **konfiguracji sieci**.</span><span class="sxs-lookup"><span data-stu-id="c921e-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Konfigurowanie sieci][config_hpc2]

3. <span data-ttu-id="c921e-179">Witaj Kreatora konfiguracji sieci wybierz **wszystkie węzły tylko w sieci przedsiębiorstwa** (topologia 5).</span><span class="sxs-lookup"><span data-stu-id="c921e-179">In hello Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="c921e-180">Ta konfiguracja sieci jest najprostsza w celach demonstracyjnych hello.</span><span class="sxs-lookup"><span data-stu-id="c921e-180">This network configuration is hello simplest for demonstration purposes.</span></span>
   
    ![Topologia 5][config_hpc3]
   
4. <span data-ttu-id="c921e-182">Kliknij przycisk **dalej** tooaccept domyślne wartości na pozostałych stronach kreatora hello hello.</span><span class="sxs-lookup"><span data-stu-id="c921e-182">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="c921e-183">Następnie na powitania **przeglądu** , kliknij pozycję **Konfiguruj** konfiguracji sieci hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c921e-183">Then, on hello **Review** tab, click **Configure** toocomplete hello network configuration.</span></span>

5. <span data-ttu-id="c921e-184">W hello **listy zadań do wykonania wdrożenia**, kliknij przycisk **poświadczenia instalacji**.</span><span class="sxs-lookup"><span data-stu-id="c921e-184">In hello **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="c921e-185">W hello **poświadczeń instalacji** okno dialogowe, wpisz hello poświadczenia konta domeny hello użytą tooinstall HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="c921e-185">In hello **Installation Credentials** dialog box, type hello credentials of hello domain account that you used tooinstall HPC Pack.</span></span> <span data-ttu-id="c921e-186">Następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c921e-186">Then click **OK**.</span></span> 
   
    ![Poświadczenia instalacji][config_hpc6]
   
7. <span data-ttu-id="c921e-188">W hello **listy zadań do wykonania wdrożenia**, kliknij przycisk **skonfigurować hello nazewnictwo nowe węzły**.</span><span class="sxs-lookup"><span data-stu-id="c921e-188">In hello **Deployment To-do List**, click **Configure hello naming of new nodes**.</span></span>

8. <span data-ttu-id="c921e-189">W hello **Określ węzeł nazwy serii** okna dialogowego Zaakceptuj domyślne hello nazwy serii i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c921e-189">In hello **Specify Node Naming Series** dialog box, accept hello default naming series and click **OK**.</span></span> <span data-ttu-id="c921e-190">Mimo że hello Azure węzły, które można dodać w tym samouczku są nazywane automatycznie, należy wykonać ten krok.</span><span class="sxs-lookup"><span data-stu-id="c921e-190">Complete this step even though hello Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Węzeł nazewnictwa][config_hpc8]
   
9. <span data-ttu-id="c921e-192">W hello **listy zadań do wykonania wdrożenia**, kliknij przycisk **Tworzenie szablonu węzła**.</span><span class="sxs-lookup"><span data-stu-id="c921e-192">In hello **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="c921e-193">Później w samouczku hello używasz hello węzła szablonu tooadd węzłów Azure toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="c921e-193">Later in hello tutorial, you use hello node template tooadd Azure nodes toohello cluster.</span></span>

10. <span data-ttu-id="c921e-194">W hello Kreator tworzenia szablonu węzła, wykonaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="c921e-194">In hello Create Node Template Wizard, do hello following:</span></span>
    
    <span data-ttu-id="c921e-195">a.</span><span class="sxs-lookup"><span data-stu-id="c921e-195">a.</span></span> <span data-ttu-id="c921e-196">Na powitania **wybierz typ szablonu węzła** kliknij przycisk **szablonu węzła w systemie Windows Azure**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c921e-196">On hello **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Szablon węzła][config_hpc10]
    
    <span data-ttu-id="c921e-198">b.</span><span class="sxs-lookup"><span data-stu-id="c921e-198">b.</span></span> <span data-ttu-id="c921e-199">Kliknij przycisk **dalej** tooaccept hello domyślna nazwa szablonu.</span><span class="sxs-lookup"><span data-stu-id="c921e-199">Click **Next** tooaccept hello default template name.</span></span>
    
    <span data-ttu-id="c921e-200">c.</span><span class="sxs-lookup"><span data-stu-id="c921e-200">c.</span></span> <span data-ttu-id="c921e-201">Na powitania **Podaj informacje o subskrypcji** wprowadź identyfikator subskrypcji platformy Azure (dostępne w danych konta platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="c921e-201">On hello **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="c921e-202">Następnie w **certyfikat zarządzania**, wyszukaj **domyślne Microsoft HPC Azure Management.**</span><span class="sxs-lookup"><span data-stu-id="c921e-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="c921e-203">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="c921e-203">Then click **Next**.</span></span>
    
    ![Szablon węzła][config_hpc12]
    
    <span data-ttu-id="c921e-205">d.</span><span class="sxs-lookup"><span data-stu-id="c921e-205">d.</span></span> <span data-ttu-id="c921e-206">Na powitania **Podaj informacje o usłudze** strony, usługa w chmurze wybierz hello i hello konta magazynu, który został utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="c921e-206">On hello **Provide Service Information** page, select hello cloud service and hello storage account that you created in a previous step.</span></span> <span data-ttu-id="c921e-207">Następnie kliknij przycisk **Next** (Dalej).</span><span class="sxs-lookup"><span data-stu-id="c921e-207">Then click **Next**.</span></span>
    
    ![Szablon węzła][config_hpc13]
    
    <span data-ttu-id="c921e-209">e.</span><span class="sxs-lookup"><span data-stu-id="c921e-209">e.</span></span> <span data-ttu-id="c921e-210">Kliknij przycisk **dalej** tooaccept domyślne wartości na pozostałych stronach kreatora hello hello.</span><span class="sxs-lookup"><span data-stu-id="c921e-210">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="c921e-211">Następnie na powitania **przeglądu** , kliknij pozycję **Utwórz** toocreate hello węzła szablonu.</span><span class="sxs-lookup"><span data-stu-id="c921e-211">Then, on hello **Review** tab, click **Create** toocreate hello node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c921e-212">Domyślnie hello Azure węzła szablon zawiera ustawienia toostart (udostępniania) i Zatrzymaj hello węzłów ręcznie, za pomocą Menedżera klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="c921e-212">By default, hello Azure node template includes settings for you toostart (provision) and stop hello nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="c921e-213">Opcjonalnie można skonfigurować toostart harmonogram i Zatrzymaj automatycznie hello węzły platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c921e-213">You can optionally configure a schedule toostart and stop hello Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a><span data-ttu-id="c921e-214">Dodaj klaster toohello węzły platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c921e-214">Add Azure nodes toohello cluster</span></span>
<span data-ttu-id="c921e-215">Teraz można używać hello węzła szablonu tooadd węzłów Azure toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="c921e-215">Now use hello node template tooadd Azure nodes toohello cluster.</span></span> <span data-ttu-id="c921e-216">Dodawanie hello węzłów toohello klastra są przechowywane informacje o ich konfiguracji, tak, aby uruchomić (zainicjować obsługi administracyjnej) je w dowolnym momencie hello w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c921e-216">Adding hello nodes toohello cluster stores their configuration information so that you can start (provision) them at any time in hello cloud service.</span></span> <span data-ttu-id="c921e-217">Subskrypcja tylko pobiera obciążony węzły platformy Azure po uruchomionych wystąpień hello hello w usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c921e-217">Your subscription only gets charged for Azure nodes after hello instances are running in hello cloud service.</span></span>

<span data-ttu-id="c921e-218">Wykonaj te kroki tooadd dwóch małych węzłów.</span><span class="sxs-lookup"><span data-stu-id="c921e-218">Follow these steps tooadd two Small nodes.</span></span>

1. <span data-ttu-id="c921e-219">W Menedżerze klastra HPC, kliknij przycisk **węzła zarządzania** (nazywane **zarządzanie zasobami** w bieżącej wersji pakietu HPC) > **Dodaj węzeł**.</span><span class="sxs-lookup"><span data-stu-id="c921e-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Dodaj węzeł][add_node1]

2. <span data-ttu-id="c921e-221">W hello Kreatora dodawania węzłów na powitania **wybierz metodę wdrożenia** kliknij przycisk **węzłów dodać systemu Windows Azure**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c921e-221">In hello Add Node Wizard, on hello **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Dodaj węzeł Azure][add_node1_1]

3. <span data-ttu-id="c921e-223">Na powitania **określ nowe węzły** strony, szablon Azure węzła hello wybierz wcześniej utworzony (o nazwie domyślnie **domyślny szablon AzureNode**).</span><span class="sxs-lookup"><span data-stu-id="c921e-223">On hello **Specify New Nodes** page, select hello Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="c921e-224">Następnie określ **2** węzłów rozmiar **małych**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="c921e-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Określ węzły][add_node2]
   
4. <span data-ttu-id="c921e-226">Na powitania **wykonywanie hello Kreatora dodawania węzłów** kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="c921e-226">On hello **Completing hello Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="c921e-227">Dwa węzły platformy Azure o nazwie **AzureCN 0001** i **AzureCN 0002**, zostaną wyświetlone w Menedżerze klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="c921e-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="c921e-228">Są w hello **wdrożone nie** stanu.</span><span class="sxs-lookup"><span data-stu-id="c921e-228">Both are in hello **Not-Deployed** state.</span></span>
   
    ![Dodanych węzłach][add_node3]

## <a name="start-hello-azure-nodes"></a><span data-ttu-id="c921e-230">Uruchom hello węzły platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c921e-230">Start hello Azure nodes</span></span>
<span data-ttu-id="c921e-231">Jeśli chcesz toouse hello klastra zasobów platformy Azure, użyj Menedżera klastra HPC toostart (zainicjować obsługi administracyjnej) hello Azure węzły i umieść je online.</span><span class="sxs-lookup"><span data-stu-id="c921e-231">When you want toouse hello cluster resources in Azure, use HPC Cluster Manager toostart (provision) hello Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="c921e-232">W Menedżerze klastra HPC, kliknij przycisk **węzła zarządzania** (nazywane **zarządzanie zasobami** w bieżącej wersji pakietu HPC), i wybierz hello węzły platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c921e-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select hello Azure nodes.</span></span>

2. <span data-ttu-id="c921e-233">Kliknij przycisk **Start**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c921e-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Uruchom węzłów][add_node4]
   
    <span data-ttu-id="c921e-235">węzły Hello przejście toohello **inicjowania obsługi administracyjnej** stanu.</span><span class="sxs-lookup"><span data-stu-id="c921e-235">hello nodes transition toohello **Provisioning** state.</span></span> <span data-ttu-id="c921e-236">Inicjowanie obsługi administracyjnej hello tootrack dziennika postęp obsługi administracyjnej hello widoku.</span><span class="sxs-lookup"><span data-stu-id="c921e-236">View hello provisioning log tootrack hello provisioning progress.</span></span>
   
    ![Zainicjuj obsługę węzłów][add_node6]

3. <span data-ttu-id="c921e-238">Po kilku minutach hello Azure węzły zakończyć inicjowanie obsługi i znajdują się w hello **Offline** stanu.</span><span class="sxs-lookup"><span data-stu-id="c921e-238">After a few minutes, hello Azure nodes finish provisioning and are in hello **Offline** state.</span></span> <span data-ttu-id="c921e-239">W tym stanie wystąpień roli hello są uruchomione, ale jeszcze nie może zaakceptować zadań klastra.</span><span class="sxs-lookup"><span data-stu-id="c921e-239">In this state, hello role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="c921e-240">tooconfirm, który hello wystąpień roli są uruchomione w hello portalu Azure, kliknij przycisk **usługi w chmurze (klasyczne)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="c921e-240">tooconfirm that hello role instances are running, in hello Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="c921e-241">Powinny pojawić się dwa **HpcWorkerRole** uruchomionych w usłudze hello wystąpień (węzłów).</span><span class="sxs-lookup"><span data-stu-id="c921e-241">You should see two **HpcWorkerRole** instances (nodes) running in hello service.</span></span> <span data-ttu-id="c921e-242">HPC Pack automatycznie wdraża dwa **HpcProxy** wystąpienia (rozmiar średnia liczba godzin) toohandle komunikacji między węzłem głównym hello i platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="c921e-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) toohandle communication between hello head node and Azure.</span></span>

   ![Uruchomione wystąpienia][view_instances1]

5. <span data-ttu-id="c921e-244">toorun online toobring hello Azure węzłów klastra, zadań, wybierz hello węzłów, kliknij prawym przyciskiem myszy, a następnie kliknij **przejdź do trybu Online**.</span><span class="sxs-lookup"><span data-stu-id="c921e-244">toobring hello Azure nodes online toorun cluster jobs, select hello nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Węzły w trybie offline][add_node7]
   
    <span data-ttu-id="c921e-246">Menedżer klastrów HPC wskazuje, że węzły hello są w hello **Online** stanu.</span><span class="sxs-lookup"><span data-stu-id="c921e-246">HPC Cluster Manager indicates that hello nodes are in hello **Online** state.</span></span>

## <a name="run-a-command-across-hello-cluster"></a><span data-ttu-id="c921e-247">Uruchom polecenie w klastrze hello</span><span class="sxs-lookup"><span data-stu-id="c921e-247">Run a command across hello cluster</span></span>
<span data-ttu-id="c921e-248">toocheck hello instalacji, użyj hello HPC Pack **clusrun** toorun polecenia polecenie lub aplikacji na co najmniej jednym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="c921e-248">toocheck hello installation, use hello HPC Pack **clusrun** command toorun a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="c921e-249">Prosty przykład użyć **clusrun** konfiguracji IP hello tooget hello węzły platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c921e-249">As a simple example, use **clusrun** tooget hello IP configuration of hello Azure nodes.</span></span>

1. <span data-ttu-id="c921e-250">W węźle głównym hello Otwórz wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="c921e-250">On hello head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="c921e-251">Wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c921e-251">Type hello following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="c921e-252">Jeśli zostanie wyświetlony monit, wprowadź hasło administratora klastra.</span><span class="sxs-lookup"><span data-stu-id="c921e-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="c921e-253">Powinny pojawić się, że podobne toohello następujących danych wyjściowych polecenia.</span><span class="sxs-lookup"><span data-stu-id="c921e-253">You should see command output similar toohello following.</span></span>
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="c921e-255">Uruchom zadanie testowe</span><span class="sxs-lookup"><span data-stu-id="c921e-255">Run a test job</span></span>
<span data-ttu-id="c921e-256">Teraz przesłać zadanie testu, które działa w klastrze hybrydowego hello.</span><span class="sxs-lookup"><span data-stu-id="c921e-256">Now submit a test job that runs on hello hybrid cluster.</span></span> <span data-ttu-id="c921e-257">W tym przykładzie jest zadaniem proste parametrycznych (typ obliczenia leżą równoległe).</span><span class="sxs-lookup"><span data-stu-id="c921e-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="c921e-258">W tym przykładzie jest uruchamiany podzadania, które dodać tooitself całkowitą przy użyciu hello **ustawić /a** polecenia.</span><span class="sxs-lookup"><span data-stu-id="c921e-258">This example runs subtasks that add an integer tooitself by using hello **set /a** command.</span></span> <span data-ttu-id="c921e-259">Wszystkie węzły hello w klastrze hello współtworzenia podzadania hello toofinishing liczb całkowitych od 1 too100.</span><span class="sxs-lookup"><span data-stu-id="c921e-259">All hello nodes in hello cluster contribute toofinishing hello subtasks for integers from 1 too100.</span></span>

1. <span data-ttu-id="c921e-260">W Menedżerze klastra HPC, kliknij przycisk **zadania zarządzania** > **nowe zadanie parametrycznych odchylenia**.</span><span class="sxs-lookup"><span data-stu-id="c921e-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Nowe zadanie][test_job1]

2. <span data-ttu-id="c921e-262">W hello **nowe zadanie parametrycznych odchylenia** okna dialogowego, **wiersza polecenia**, typ `set /a *+*` (zastępowanie hello domyślnego wiersza polecenia wyświetlany).</span><span class="sxs-lookup"><span data-stu-id="c921e-262">In hello **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting hello default command line that appears).</span></span> <span data-ttu-id="c921e-263">Pozostaw wartości domyślne dla pozostałych ustawień hello, a następnie kliknij przycisk **przesyłania** toosubmit hello zadania.</span><span class="sxs-lookup"><span data-stu-id="c921e-263">Leave default values for hello remaining settings, and then click **Submit** toosubmit hello job.</span></span>
   
    ![Parametrycznych][param_sweep1]

3. <span data-ttu-id="c921e-265">Po zakończeniu zadania hello, kliknij dwukrotnie hello **Moje zadania odchylenia** zadania.</span><span class="sxs-lookup"><span data-stu-id="c921e-265">When hello job is finished, double-click hello **My Sweep Task** job.</span></span>

4. <span data-ttu-id="c921e-266">Kliknij przycisk **zadania widoku**, a następnie kliknij przycisk podzadanie tooview hello obliczane dane wyjściowe z tym samym poziomie.</span><span class="sxs-lookup"><span data-stu-id="c921e-266">Click **View Tasks**, and then click a subtask tooview hello calculated output of that subtask.</span></span>
   
    ![Wyniki zadań][view_job361]

5. <span data-ttu-id="c921e-268">Kliknij toosee, który węzeł wykonać obliczenie hello na tym samym poziomie **przydzielone węzłów**.</span><span class="sxs-lookup"><span data-stu-id="c921e-268">toosee which node performed hello calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="c921e-269">(Klastra mogą być wyświetlane nazwy innego węzła).</span><span class="sxs-lookup"><span data-stu-id="c921e-269">(Your cluster might show a different node name.)</span></span>
   
    ![Wyniki zadań][view_job362]

## <a name="stop-hello-azure-nodes"></a><span data-ttu-id="c921e-271">Zatrzymaj hello węzły platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c921e-271">Stop hello Azure nodes</span></span>
<span data-ttu-id="c921e-272">Po wypróbowanie hello klastra, należy zatrzymać hello Azure węzłów tooavoid niepotrzebnych opłat tooyour konta.</span><span class="sxs-lookup"><span data-stu-id="c921e-272">After you try out hello cluster, stop hello Azure nodes tooavoid unnecessary charges tooyour account.</span></span> <span data-ttu-id="c921e-273">Ten krok zatrzymuje usługę w chmurze hello i usuwa hello wystąpień roli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c921e-273">This step stops hello cloud service and removes hello Azure role instances.</span></span>

1. <span data-ttu-id="c921e-274">W Menedżerze klastra HPC w **węzła zarządzania** (nazywane **zarządzanie zasobami** w poprzednich wersjach programu HPC Pack), wybierz oba węzły platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c921e-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="c921e-275">Następnie kliknij przycisk **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="c921e-275">Then, click **Stop**.</span></span>
   
    ![Zatrzymaj węzłów][stop_node1]

2. <span data-ttu-id="c921e-277">W hello **zatrzymania systemu Windows Azure węzłów** okno dialogowe, kliknij przycisk **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="c921e-277">In hello **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="c921e-278">węzły Hello przejście toohello **zatrzymywanie** stanu.</span><span class="sxs-lookup"><span data-stu-id="c921e-278">hello nodes transition toohello **Stopping** state.</span></span> <span data-ttu-id="c921e-279">Po upływie kilku minut, Menedżer klastra HPC pokazuje, czy węzły hello są **wdrożone nie**.</span><span class="sxs-lookup"><span data-stu-id="c921e-279">After a few minutes, HPC Cluster Manager shows that hello nodes are **Not-Deployed**.</span></span>
   
    ![Węzły Niewdrożone][stop_node4]

4. <span data-ttu-id="c921e-281">tooconfirm, który hello wystąpień roli nie jest już uruchomiony na platformie Azure w hello Azure portalu, kliknij przycisk **usługi (klasyczne) w chmurze** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="c921e-281">tooconfirm that hello role instances are no longer running in Azure, in hello Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="c921e-282">Brak wystąpień są wdrażane w środowisku produkcyjnym hello.</span><span class="sxs-lookup"><span data-stu-id="c921e-282">No instances are deployed in hello production environment.</span></span> 
   
    <span data-ttu-id="c921e-283">Na tym kończy się hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="c921e-283">This completes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c921e-284">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c921e-284">Next steps</span></span>
* <span data-ttu-id="c921e-285">Eksploruj dokumentacji hello [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="c921e-285">Explore hello documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="c921e-286">Zobacz tooset się hybrydowe wdrożenie klastra HPC Pack na większą skalę [serii tooAzure wystąpień roli procesu roboczego z pakietem Microsoft HPC](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="c921e-286">tooset up a hybrid HPC Pack cluster deployment at greater scale, see [Burst tooAzure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="c921e-287">Inne sposoby toocreate klastra HPC Pack na platformie Azure, w tym za pomocą szablonów usługi Azure Resource Manager dla [opcje klastra HPC z pakietem Microsoft HPC w systemie Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c921e-287">For other ways toocreate an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
