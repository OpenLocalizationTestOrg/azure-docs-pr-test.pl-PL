---
title: "węzły klastra HPC Pack aaaAutoscale | Dokumentacja firmy Microsoft"
description: "Automatycznie zwiększyć lub zmniejszyć hello liczba węzłów obliczeniowych klastra HPC Pack na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="dd020-103">Automatycznie zwiększyć lub zmniejszyć zasobów klastra HPC Pack hello na platformie Azure, zgodnie z toohello obciążenie klastra</span><span class="sxs-lookup"><span data-stu-id="dd020-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="dd020-104">Jeśli wdrażania platformy Azure "serii" węzłów w klastrze HPC Pack lub utworzyć klaster HPC Pack w maszynach wirtualnych platformy Azure, możesz sposób, aby automatycznie zwiększać i zmniejszać zasoby klastra hello, takie jak węzłów lub rdzeni zgodnie z hello obciążenie klastra hello.</span><span class="sxs-lookup"><span data-stu-id="dd020-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="dd020-105">Skalowanie hello zasoby klastra w ten sposób umożliwia toouse zasobów platformy Azure wydajniej i kontrolę kosztów ich.</span><span class="sxs-lookup"><span data-stu-id="dd020-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="dd020-106">W tym artykule przedstawiono HPC Pack udostępnia zasoby obliczeniowe tooautoscale na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="dd020-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="dd020-107">Witaj właściwości klastra HPC Pack **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="dd020-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="dd020-108">Witaj **AzureAutoGrowShrink.ps1** skryptu środowiska PowerShell klastra HPC</span><span class="sxs-lookup"><span data-stu-id="dd020-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="dd020-109">Obecnie tylko automatycznie można zwiększyć lub zmniejszyć węzły obliczeniowe HPC Pack uruchomionych w systemie operacyjnym Windows Server.</span><span class="sxs-lookup"><span data-stu-id="dd020-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="dd020-110">Ustaw właściwość klastra AutoGrowShrink hello</span><span class="sxs-lookup"><span data-stu-id="dd020-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="dd020-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dd020-111">Prerequisites</span></span>

* <span data-ttu-id="dd020-112">**HPC Pack 2012 R2 Update 2 lub nowszym klastra** -hello węzła głównego klastra może być wdrożona lokalnie lub w maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dd020-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="dd020-113">Zobacz [Konfigurowanie klastra hybrydowego pakietem HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget pracę z węzłem głównym lokalnymi i węzły platformy Azure "serii".</span><span class="sxs-lookup"><span data-stu-id="dd020-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="dd020-114">Zobacz hello [skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md) tooquickly wdrożenie klastra HPC Pack w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dd020-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="dd020-115">**W przypadku klastra z węzła głównego na platformie Azure (modelu wdrażania usługi Resource Manager)** — począwszy od HPC Pack 2016 certyfikatów uwierzytelniania w aplikacji usługi Azure Active Directory służy do automatycznie powiększania i zmniejszanie rozmiaru klastra maszyny wirtualne wdrażane za pomocą Usługa Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dd020-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="dd020-116">Konfigurowanie certyfikatu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="dd020-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="dd020-117">Po wdrożeniu klastra łączyć węzła głównego tooone pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="dd020-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="dd020-118">Przekaż hello węzła głównego tooeach certyfikatu (format PFX z kluczem prywatnym) i zainstaluj tooCert:\LocalMachine\My i Cert: \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="dd020-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="dd020-119">Uruchom program Azure PowerShell jako administrator i uruchom następujące polecenia w jednym węźle głównym hello:</span><span class="sxs-lookup"><span data-stu-id="dd020-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="dd020-120">Jeśli konto użytkownika należy do więcej niż jednej dzierżawy usługi Azure Active Directory lub subskrypcji platformy Azure, można uruchomić następujące hello polecenia tooselect hello poprawne dzierżawy i subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="dd020-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="dd020-121">Uruchom następujące polecenie tooview hello hello aktualnie wybrane dzierżawy i subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="dd020-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="dd020-122">Uruchom hello następującego skryptu</span><span class="sxs-lookup"><span data-stu-id="dd020-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="dd020-123">gdzie</span><span class="sxs-lookup"><span data-stu-id="dd020-123">where</span></span>

    <span data-ttu-id="dd020-124">**Nazwa wyświetlana** — Nazwa wyświetlana Azure aktywnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dd020-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="dd020-125">Jeśli aplikacja hello nie istnieje, jest tworzony w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dd020-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="dd020-126">**Strona główna** — strona główna hello aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="dd020-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="dd020-127">Można skonfigurować zastępczego adresu URL, tak jak hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="dd020-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="dd020-128">**IdentifierUri** — identyfikator aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="dd020-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="dd020-129">Można skonfigurować zastępczego adresu URL, tak jak hello poprzedzających przykład.</span><span class="sxs-lookup"><span data-stu-id="dd020-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="dd020-130">**CertificateThumbprint** — odcisk palca certyfikatu hello zainstalowany na powitania węzła głównego w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="dd020-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="dd020-131">**TenantId** -Identyfikatorem usługi Azure Active Directory dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="dd020-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="dd020-132">Hello identyfikator dzierżawcy można pobrać z portalu usługi Azure Active Directory hello **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="dd020-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="dd020-133">Aby uzyskać więcej informacji o **ConfigARMAutoGrowShrinkCert.ps1**Uruchom `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="dd020-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="dd020-134">**W przypadku klastra z węzła głównego na platformie Azure (klasycznego modelu wdrażania)** — Jeśli używasz hello HPC Pack IaaS wdrożenia skryptu toocreate hello klastra hello klasycznego modelu wdrażania, Włącz hello **AutoGrowShrink** klastra Właściwość przez ustawienie opcji AutoGrowShrink hello w pliku konfiguracyjnym hello klastra.</span><span class="sxs-lookup"><span data-stu-id="dd020-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="dd020-135">Aby uzyskać więcej informacji, zobacz dokumentację hello, towarzyszące hello [pobieranie skryptu](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="dd020-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="dd020-136">Można również włączyć hello **AutoGrowShrink** właściwości klastra po wdrożeniu klastra hello przy użyciu środowiska PowerShell klastra HPC polecenia opisane w następujących sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="dd020-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="dd020-137">tooprepare tego, pierwszy hello pełną następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="dd020-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="dd020-138">Skonfiguruj certyfikat zarządzania platformy Azure na powitania węzła głównego i w hello subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dd020-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="dd020-139">W przypadku testowego wdrożenia można użyć hello domyślne Microsoft HPC Azure certyfikatu z podpisem własnym instalujący na powitania węzłem głównym HPC Pack a następnie przekaż tooyour tego certyfikatu subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dd020-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="dd020-140">Dla opcji i procedury, zobacz hello [wskazówki w bibliotece TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd020-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="dd020-141">Uruchom **regedit** na powitania węzła głównego, przejdź tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo i Dodaj wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="dd020-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="dd020-142">Ustaw nazwę wartości hello zbyt "Odcisk palca" i wartości danych toohello odcisk palca certyfikatu hello w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="dd020-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="dd020-143">Właściwość AutoGrowShrink hello tooset polecenia środowiska PowerShell klastra HPC</span><span class="sxs-lookup"><span data-stu-id="dd020-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="dd020-144">Poniżej przedstawiono tooset polecenia środowiska PowerShell klastra HPC próbki **AutoGrowShrink** i tootune jego zachowanie w przypadku dodatkowych parametrów.</span><span class="sxs-lookup"><span data-stu-id="dd020-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="dd020-145">Zobacz [parametry AutoGrowShrink](#AutoGrowShrink-parameters) dalszej części tego artykułu hello pełną listę ustawień.</span><span class="sxs-lookup"><span data-stu-id="dd020-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="dd020-146">toorun tych poleceń, uruchom program HPC PowerShell na powitania węzła głównego klastra jako administrator.</span><span class="sxs-lookup"><span data-stu-id="dd020-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="dd020-147">**Witaj tooenable AutoGrowShrink właściwości**</span><span class="sxs-lookup"><span data-stu-id="dd020-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="dd020-148">**Witaj toodisable AutoGrowShrink właściwości**</span><span class="sxs-lookup"><span data-stu-id="dd020-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="dd020-149">**Witaj toochange Zwiększ interwał w minutach**</span><span class="sxs-lookup"><span data-stu-id="dd020-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="dd020-150">**Witaj toochange Zmniejszanie interwału w minutach**</span><span class="sxs-lookup"><span data-stu-id="dd020-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="dd020-151">**tooview hello bieżącej konfiguracji AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="dd020-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="dd020-152">**tooexclude węzeł grupy z AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="dd020-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="dd020-153">Ten parametr jest obsługiwane począwszy od HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="dd020-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="dd020-154">Parametry AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="dd020-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="dd020-155">Witaj poniżej przedstawiono AutoGrowShrink parametry, które można modyfikować za pomocą hello **HpcClusterProperty zestaw** polecenia.</span><span class="sxs-lookup"><span data-stu-id="dd020-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="dd020-156">**EnableGrowShrink** — przełącznik tooenable lub wyłącz hello **AutoGrowShrink** właściwości.</span><span class="sxs-lookup"><span data-stu-id="dd020-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="dd020-157">**ParamSweepTasksPerCore** — liczba parametrów zadania toogrow jednego rdzenia.</span><span class="sxs-lookup"><span data-stu-id="dd020-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="dd020-158">Domyślnie Hello jest toogrow jednego rdzenia poszczególnych zadań.</span><span class="sxs-lookup"><span data-stu-id="dd020-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="dd020-159">Zmiany HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** za**TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="dd020-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="dd020-160">Jest oparty na typie zasobów zadania hello, a węzeł, gniazda lub core.</span><span class="sxs-lookup"><span data-stu-id="dd020-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="dd020-161">**GrowThreshold** — próg umieszczonych w kolejce zadań tootrigger automatycznego przyrostu.</span><span class="sxs-lookup"><span data-stu-id="dd020-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="dd020-162">Witaj domyślna to 1, co oznacza, że jeśli istnieją 1 lub więcej zadań w hello stanu umieszczonych w kolejce, automatycznie rozszerzaj węzłów.</span><span class="sxs-lookup"><span data-stu-id="dd020-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="dd020-163">**GrowInterval** — interwał w minutach tootrigger automatycznego przyrostu.</span><span class="sxs-lookup"><span data-stu-id="dd020-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="dd020-164">Witaj domyślny interwał wynosi 5 minut.</span><span class="sxs-lookup"><span data-stu-id="dd020-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="dd020-165">**ShrinkInterval** — interwał w minutach tootrigger automatyczne zmniejszanie.</span><span class="sxs-lookup"><span data-stu-id="dd020-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="dd020-166">Witaj domyślny interwał wynosi 5 minut. |</span><span class="sxs-lookup"><span data-stu-id="dd020-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="dd020-167">**ShrinkIdleTimes** — liczba węzłów hello tooindicate tooshrink ciągłego kontroli są w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="dd020-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="dd020-168">Witaj domyślna to 3 razy.</span><span class="sxs-lookup"><span data-stu-id="dd020-168">hello default is 3 times.</span></span> <span data-ttu-id="dd020-169">Na przykład, jeśli hello **ShrinkInterval** wynosi 5 minut, HPC Pack sprawdza, czy węzeł hello jest w stanie bezczynności co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="dd020-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="dd020-170">Jeśli węzły hello są w stanie bezczynności hello po 3 ciągłego sprawdza (15 minut), HPC Pack zmniejsza tego węzła.</span><span class="sxs-lookup"><span data-stu-id="dd020-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="dd020-171">**ExtraNodesGrowRatio** -procent dodatkowe węzły toogrow zadań komunikat interfejsu (Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="dd020-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="dd020-172">Witaj, wartość domyślna to 1, co oznacza, że HPC Pack rozwoju węzłów % 1 dla zadań MPI.</span><span class="sxs-lookup"><span data-stu-id="dd020-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="dd020-173">**GrowByMin** -przełącznika tooindicate, czy zasady automatycznego przyrostu hello opiera się na powitania zasobów minimalne wymagane hello zadania.</span><span class="sxs-lookup"><span data-stu-id="dd020-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="dd020-174">Domyślna Hello to false, co oznacza, że HPC Pack rozwoju węzłów zadań na podstawie zasobów maksymalną hello wymagane hello zadań.</span><span class="sxs-lookup"><span data-stu-id="dd020-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="dd020-175">**SoaJobGrowThreshold** — próg przychodzące SOA żądań tootrigger hello automatycznego wzrostu procesu.</span><span class="sxs-lookup"><span data-stu-id="dd020-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="dd020-176">Wartość domyślna Hello jest 50000.</span><span class="sxs-lookup"><span data-stu-id="dd020-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="dd020-177">Ten parametr jest obsługiwana, począwszy od HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="dd020-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="dd020-178">**SoaRequestsPerCore** — liczba SOA przychodzących żądań toogrow jednego rdzenia.</span><span class="sxs-lookup"><span data-stu-id="dd020-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="dd020-179">Wartość domyślna Hello jest 20000.</span><span class="sxs-lookup"><span data-stu-id="dd020-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="dd020-180">Ten parametr jest obsługiwana, począwszy od HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="dd020-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="dd020-181">**ExcludeNodeGroups** — węzły w hello określone grupy węzła automatycznie zwiększyć lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="dd020-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="dd020-182">Ten parametr jest obsługiwana, począwszy od HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="dd020-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="dd020-183">Przykład MPI</span><span class="sxs-lookup"><span data-stu-id="dd020-183">MPI example</span></span>
<span data-ttu-id="dd020-184">Domyślnie HPC Pack rozwoju 1% dodatkowe węzły zadań MPI (**ExtraNodesGrowRatio** ustawiono too1).</span><span class="sxs-lookup"><span data-stu-id="dd020-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="dd020-185">Przyczyna Hello jest MPI może wymagać wielu węzłów, czy hello zadanie można uruchomić tylko po zakończeniu wszystkich węzłów.</span><span class="sxs-lookup"><span data-stu-id="dd020-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="dd020-186">Po uruchomieniu węzłów Azure czasami jeden węzeł może być konieczne więcej czasu toostart niż inne, powodując inne węzły toobe bezczynności podczas oczekiwania na tym tooget węzła gotowe.</span><span class="sxs-lookup"><span data-stu-id="dd020-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="dd020-187">Powiększając dodatkowe węzły, HPC Pack skraca czas oczekiwania tego zasobu i potencjalnie zapisuje kosztów.</span><span class="sxs-lookup"><span data-stu-id="dd020-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="dd020-188">Procent hello tooincrease dodatkowe węzły zadań MPI (na przykład too10%), uruchom polecenie podobne do</span><span class="sxs-lookup"><span data-stu-id="dd020-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="dd020-189">Przykład SOA</span><span class="sxs-lookup"><span data-stu-id="dd020-189">SOA example</span></span>
<span data-ttu-id="dd020-190">Domyślnie **SoaJobGrowThreshold** ustawiono too50000 i **SoaRequestsPerCore** ustawiono too200000.</span><span class="sxs-lookup"><span data-stu-id="dd020-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="dd020-191">Jeśli prześlesz jedno zadanie SOA z żądaniami 70000 istnieje jedno zadanie w kolejce i żądania przychodzące są 70000.</span><span class="sxs-lookup"><span data-stu-id="dd020-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="dd020-192">W takim przypadku HPC Pack rozwoju 1 rdzeń hello w kolejce zadań i żądań przychodzących, rozwoju (70000 50000) / podstawowe 20000 = 1, dlatego w łącznie rozwoju 2 rdzeni dla tego zadania SOA.</span><span class="sxs-lookup"><span data-stu-id="dd020-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="dd020-193">Uruchom skrypt AzureAutoGrowShrink.ps1 hello</span><span class="sxs-lookup"><span data-stu-id="dd020-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="dd020-194">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dd020-194">Prerequisites</span></span>

* <span data-ttu-id="dd020-195">**HPC Pack 2012 R2 Update 1 lub nowszym klastra** — Witaj **AzureAutoGrowShrink.ps1** skryptów jest zainstalowany w hello % CCP_HOME % bin folder.</span><span class="sxs-lookup"><span data-stu-id="dd020-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="dd020-196">Witaj węzła głównego klastra może być wdrożona lokalnie lub w maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dd020-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="dd020-197">Zobacz [Konfigurowanie klastra hybrydowego pakietem HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget pracę z węzłem głównym lokalnymi i węzły platformy Azure "serii".</span><span class="sxs-lookup"><span data-stu-id="dd020-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="dd020-198">Zobacz hello [skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md) tooquickly wdrożenie klastra HPC Pack w maszynach wirtualnych platformy Azure lub użyj [szablonie Szybki Start Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="dd020-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="dd020-199">**Program Azure PowerShell 1.4.0** -skryptu hello zależy od obecnie tę konkretną wersję programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dd020-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="dd020-200">**Dla klastra przy użyciu platformy Azure serii węzłów** — Uruchom skrypt hello na komputerze klienckim, na których zainstalowano pakiet HPC lub na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="dd020-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="dd020-201">Jeśli uruchomiona na komputerze klienckim, upewnij się, ustaw hello zmiennej $env: węzła głównego toohello toopoint CCP_SCHEDULER.</span><span class="sxs-lookup"><span data-stu-id="dd020-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="dd020-202">musi zostać dodany Hello Azure "serii" węzłów klastra toohello, ale hello stan wdrożonych nie mogą być.</span><span class="sxs-lookup"><span data-stu-id="dd020-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="dd020-203">**Dla klastra wdrożone w maszynach wirtualnych platformy Azure (modelu wdrażania usługi Resource Manager)** -klastra z maszyn wirtualnych Azure wdrożone w modelu wdrażania usługi Resource Manager hello skrypt hello obsługuje dwie metody uwierzytelniania systemu Azure: Zaloguj tooyour konto platformy Azure skrypt hello toorun zawsze (uruchamiając `Login-AzureRmAccount`, lub skonfigurować tooauthenticate główna usługi przy użyciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="dd020-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="dd020-204">HPC Pack zawiera skrypt hello **ConfigARMAutoGrowShrinkCert.ps** toocreate nazwy głównej usługi o certyfikat.</span><span class="sxs-lookup"><span data-stu-id="dd020-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="dd020-205">Witaj skrypt tworzy aplikację usługi Azure Active Directory (Azure AD) i nazwy głównej usługi i przypisuje nazwy głównej usługi toohello roli współautora hello.</span><span class="sxs-lookup"><span data-stu-id="dd020-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="dd020-206">skrypt hello toorun, uruchom program Azure PowerShell jako administrator i uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="dd020-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="dd020-207">Aby uzyskać więcej informacji o **ConfigARMAutoGrowShrinkCert.ps1**Uruchom `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span><span class="sxs-lookup"><span data-stu-id="dd020-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="dd020-208">**Dla klastra wdrożone w maszynach wirtualnych platformy Azure (klasycznego modelu wdrażania)** — Uruchom skrypt hello na powitania węzła głównego maszyny Wirtualnej, ponieważ zależy on od hello **Start HpcIaaSNode.ps1** i **Stop-HpcIaaSNode.ps1**skrypty, które są zainstalowane na.</span><span class="sxs-lookup"><span data-stu-id="dd020-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="dd020-209">Ponadto te skrypty wymagają certyfikatu zarządzania platformy Azure lub plik ustawień publikowania (zobacz [Zarządzaj węzłów obliczeniowych w HPC Pack klastra w systemie Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="dd020-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="dd020-210">Upewnij się, wszystkie hello obliczeniowe węzła maszyny wirtualne, konieczne są już dodane toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="dd020-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="dd020-211">Mogą być hello zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="dd020-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="dd020-212">Składnia</span><span class="sxs-lookup"><span data-stu-id="dd020-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="dd020-213">Parametry</span><span class="sxs-lookup"><span data-stu-id="dd020-213">Parameters</span></span>
* <span data-ttu-id="dd020-214">**NodeTemplates** -nazwy hello węzeł Szablony toodefine hello zakres hello toogrow węzłów i zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="dd020-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="dd020-215">Jeśli nie zostanie określony (hello wartość domyślna to @()), wszystkie węzły w hello **AzureNodes** węzła grupy są w zakres podczas **NodeType** ma wartość AzureNodes, a wszystkie węzły w hello **ComputeNodes** węzła grupy są w przypadku zakres **NodeType** ma wartość ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="dd020-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="dd020-216">**JobTemplates** -nazwy hello zadania szablonów toodefine hello zakres hello toogrow węzłów.</span><span class="sxs-lookup"><span data-stu-id="dd020-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="dd020-217">**Typ NodeType** — Witaj typu węzła toogrow i zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="dd020-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="dd020-218">Obsługiwane są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="dd020-218">Supported values are:</span></span>

  * <span data-ttu-id="dd020-219">**AzureNodes** — w przypadku Azure PaaS (serii) węzły w lokalnej lub w klastrze IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dd020-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="dd020-220">**ComputeNodes** — dla węzła obliczeniowego maszyn wirtualnych tylko w klastrze IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dd020-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="dd020-221">**NumOfQueuedJobsPerNodeToGrow** -liczbę zadań umieszczonych w kolejce wymagane toogrow jeden węzeł.</span><span class="sxs-lookup"><span data-stu-id="dd020-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="dd020-222">**NumOfQueuedJobsToGrowThreshold** -hello próg liczbę zadań umieszczonych w kolejce toostart hello wzrostu procesu.</span><span class="sxs-lookup"><span data-stu-id="dd020-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="dd020-223">**NumOfActiveQueuedTasksPerNodeToGrow** -hello liczba aktywnych zadań w kolejce wymagane toogrow jeden węzeł.</span><span class="sxs-lookup"><span data-stu-id="dd020-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="dd020-224">Jeśli **NumOfQueuedJobsPerNodeToGrow** zostanie podana wartość większą niż 0, ten parametr jest ignorowany.</span><span class="sxs-lookup"><span data-stu-id="dd020-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="dd020-225">**NumOfActiveQueuedTasksToGrowThreshold** -hello Próg liczby aktywnych zadań w kolejce toostart hello wzrostu procesu.</span><span class="sxs-lookup"><span data-stu-id="dd020-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="dd020-226">**NumOfInitialNodesToGrow** — Witaj początkowa minimalna liczba węzłów toogrow, jeśli wszystkie węzły hello w zakresie są **wdrożone nie** lub **zatrzymane (Deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="dd020-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="dd020-227">**GrowCheckIntervalMins** -hello interwał w minutach od sprawdza toogrow.</span><span class="sxs-lookup"><span data-stu-id="dd020-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="dd020-228">**ShrinkCheckIntervalMins** -hello interwał w minutach od sprawdza tooshrink.</span><span class="sxs-lookup"><span data-stu-id="dd020-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="dd020-229">**ShrinkCheckIdleTimes** — Witaj liczby sprawdzeń ciągłego zmniejszania (rozdzielone **ShrinkCheckIntervalMins**) tooindicate hello węzły są w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="dd020-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="dd020-230">**UseLastConfigurations** — Witaj poprzedniej konfiguracji zapisane w pliku argumentu hello.</span><span class="sxs-lookup"><span data-stu-id="dd020-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="dd020-231">**ArgFile**— Witaj nazwa toosave plik używany argument hello i hello konfiguracje toorun hello skrypt aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="dd020-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="dd020-232">**LogFilePrefix** -hello prefiks nazwy pliku dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="dd020-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="dd020-233">Można określić ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="dd020-233">You can specify a path.</span></span> <span data-ttu-id="dd020-234">Domyślnie dziennik hello jest zapisywane toohello bieżący katalog roboczy.</span><span class="sxs-lookup"><span data-stu-id="dd020-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="dd020-235">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="dd020-235">Example 1</span></span>
<span data-ttu-id="dd020-236">Witaj poniższy przykład umożliwia skonfigurowanie hello Azure serii węzłów z toogrow domyślny szablon AzureNode i zmniejsza się automatycznie.</span><span class="sxs-lookup"><span data-stu-id="dd020-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="dd020-237">Jeśli wszystkie węzły są początkowo w hello **wdrożone nie** stanu, są uruchamiane co najmniej 3 węzłach.</span><span class="sxs-lookup"><span data-stu-id="dd020-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="dd020-238">Jeśli hello liczbę zadań umieszczonych w kolejce przekroczy 8, skrypt hello rozpoczyna węzłów aż do ich liczba przekracza stosunek hello umieszczonych w kolejce zadań do **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="dd020-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="dd020-239">Jeśli węzeł zostanie znaleziony toobe bezczynności 3 kolejne czas bezczynności, zostanie zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="dd020-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="dd020-240">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="dd020-240">Example 2</span></span>
<span data-ttu-id="dd020-241">Witaj poniższy przykład umożliwia skonfigurowanie hello Azure obliczeniowe węzła maszyny wirtualne wdrażane z hello domyślny szablon ComputeNode toogrow i zmniejsza się automatycznie.</span><span class="sxs-lookup"><span data-stu-id="dd020-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="dd020-242">zadania Hello konfigurowane za pomocą szablonu zadania domyślne hello zdefiniować zakres hello obciążenia w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="dd020-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="dd020-243">Jeśli wszystkie węzły hello są początkowo zatrzymana, są uruchamiane co najmniej 5 węzłów.</span><span class="sxs-lookup"><span data-stu-id="dd020-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="dd020-244">Jeśli hello liczba aktywnych zadań w kolejce przekroczy 15, skrypt hello rozpoczyna węzłów aż do ich liczba przekracza hello stosunek aktywne zadania w kolejce za**NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="dd020-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="dd020-245">Jeśli węzeł zostanie znaleziony toobe bezczynności 10 kolejnych czas bezczynności, zostanie zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="dd020-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
