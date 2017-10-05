---
title: "Węzły klastra skalowania automatycznego HPC Pack | Dokumentacja firmy Microsoft"
description: "Automatycznie zwiększyć lub zmniejszyć liczbę węzłów obliczeniowych klastra HPC Pack na platformie Azure"
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
ms.openlocfilehash: 0dc0d15c64d8951c3c457df73588c37418a3c8a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-grow-and-shrink-the-hpc-pack-cluster-resources-in-azure-according-to-the-cluster-workload"></a><span data-ttu-id="ca598-103">Automatycznie zwiększyć lub zmniejszyć zasobów klastra HPC Pack na platformie Azure zgodnie z obciążenie klastra</span><span class="sxs-lookup"><span data-stu-id="ca598-103">Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload</span></span>
<span data-ttu-id="ca598-104">Jeśli wdrażania platformy Azure "serii" węzłów w klastrze HPC Pack lub utworzyć klaster HPC Pack w maszynach wirtualnych platformy Azure, możesz sposób, aby automatycznie zwiększać i zmniejszać zasoby klastra, takie jak węzłów lub rdzeni w zależności od obciążenia w klastrze.</span><span class="sxs-lookup"><span data-stu-id="ca598-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink the cluster resources such as nodes or cores according to the workload on the cluster.</span></span> <span data-ttu-id="ca598-105">Skalowanie zasobów klastra w ten sposób pozwala na bardziej efektywnie korzystać z zasobów platformy Azure i kontrolę kosztów ich.</span><span class="sxs-lookup"><span data-stu-id="ca598-105">Scaling the cluster resources in this way allows you to use your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="ca598-106">W tym artykule opisano, że zasoby obliczeniowe dwie metody udostępniające HPC Pack skalowania automatycznego:</span><span class="sxs-lookup"><span data-stu-id="ca598-106">This article shows you two ways that HPC Pack provides to autoscale compute resources:</span></span>

* <span data-ttu-id="ca598-107">Właściwość klastra HPC Pack **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="ca598-107">The HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="ca598-108">**AzureAutoGrowShrink.ps1** skryptu środowiska PowerShell klastra HPC</span><span class="sxs-lookup"><span data-stu-id="ca598-108">The **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="ca598-109">Obecnie tylko automatycznie można zwiększyć lub zmniejszyć węzły obliczeniowe HPC Pack uruchomionych w systemie operacyjnym Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ca598-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-the-autogrowshrink-cluster-property"></a><span data-ttu-id="ca598-110">Ustaw właściwość AutoGrowShrink klastra</span><span class="sxs-lookup"><span data-stu-id="ca598-110">Set the AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="ca598-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ca598-111">Prerequisites</span></span>

* <span data-ttu-id="ca598-112">**HPC Pack 2012 R2 Update 2 lub nowszym klastra** -węzła głównego klastra może być wdrożona lokalnie lub w maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca598-112">**HPC Pack 2012 R2 Update 2 or later cluster** - The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="ca598-113">Zobacz [Konfigurowanie klastra hybrydowego pakietem HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) rozpocząć pracę z węzłem głównym lokalnymi i węzły platformy Azure "serii".</span><span class="sxs-lookup"><span data-stu-id="ca598-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="ca598-114">Zobacz [skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md) można szybko wdrożyć klaster HPC Pack w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca598-114">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="ca598-115">**W przypadku klastra z węzła głównego na platformie Azure (modelu wdrażania usługi Resource Manager)** — począwszy od HPC Pack 2016 certyfikatów uwierzytelniania w aplikacji usługi Azure Active Directory służy do automatycznie powiększania i zmniejszanie rozmiaru klastra maszyny wirtualne wdrażane za pomocą Usługa Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ca598-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="ca598-116">Konfigurowanie certyfikatu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="ca598-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="ca598-117">Po wdrożeniu klastra przez pulpit zdalny połączyć się z jednego węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="ca598-117">After cluster deployment, connect by Remote Desktop to one head node.</span></span>

  2. <span data-ttu-id="ca598-118">Przekaż certyfikat (format PFX z kluczem prywatnym) do każdego węzła głównego i zainstaluj Cert: \LocalMachine\My i Cert: \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="ca598-118">Upload the certificate (PFX format with private key) to each head node and install to Cert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="ca598-119">Uruchom program Azure PowerShell jako administrator i uruchom następujące polecenia w jednym węźle głównym:</span><span class="sxs-lookup"><span data-stu-id="ca598-119">Start Azure PowerShell as an administrator and run the following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="ca598-120">Jeśli konto użytkownika należy do więcej niż jednej dzierżawy usługi Azure Active Directory lub subskrypcji platformy Azure, można uruchomić następujące polecenie, aby wybrać poprawny dzierżawy i subskrypcję:</span><span class="sxs-lookup"><span data-stu-id="ca598-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run the following command to select the correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="ca598-121">Uruchom następujące polecenie, aby wyświetlić aktualnie wybranej dzierżawy i subskrypcji:</span><span class="sxs-lookup"><span data-stu-id="ca598-121">Run the following command to view the currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="ca598-122">Uruchom poniższy skrypt</span><span class="sxs-lookup"><span data-stu-id="ca598-122">Run the following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="ca598-123">gdzie</span><span class="sxs-lookup"><span data-stu-id="ca598-123">where</span></span>

    <span data-ttu-id="ca598-124">**Nazwa wyświetlana** — Nazwa wyświetlana Azure aktywnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca598-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="ca598-125">Jeśli aplikacja nie istnieje, jest tworzony w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ca598-125">If the application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="ca598-126">**Strona główna** — strona główna aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca598-126">**HomePage** - The home page of the application.</span></span> <span data-ttu-id="ca598-127">Można skonfigurować zastępczego adresu URL, tak jak w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ca598-127">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="ca598-128">**IdentifierUri** — identyfikator aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ca598-128">**IdentifierUri** - Identifier of the application.</span></span> <span data-ttu-id="ca598-129">Można skonfigurować zastępczego adresu URL, tak jak w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="ca598-129">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="ca598-130">**CertificateThumbprint** — odcisk palca certyfikatu został zainstalowany w węźle głównym w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="ca598-130">**CertificateThumbprint** - Thumbprint of the certificate you installed on the head node in Step 1.</span></span>

    <span data-ttu-id="ca598-131">**TenantId** -Identyfikatorem usługi Azure Active Directory dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="ca598-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="ca598-132">Identyfikator dzierżawcy można pobrać z portalu usługi Azure Active Directory **właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="ca598-132">You can get the Tenant ID from the Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="ca598-133">Aby uzyskać więcej informacji o **ConfigARMAutoGrowShrinkCert.ps1**Uruchom `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="ca598-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="ca598-134">**W przypadku klastra z węzła głównego na platformie Azure (klasycznego modelu wdrażania)** — Jeśli używasz skryptu wdrażania HPC Pack IaaS do tworzenia klastra w klasycznym modelu wdrożenia, Włącz **AutoGrowShrink** klastra właściwości przez ustawienie opcji AutoGrowShrink w pliku konfiguracji klastra.</span><span class="sxs-lookup"><span data-stu-id="ca598-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use the HPC Pack IaaS deployment script to create the cluster in the classic deployment model, enable the **AutoGrowShrink** cluster property by setting the AutoGrowShrink option in the cluster configuration file.</span></span> <span data-ttu-id="ca598-135">Aby uzyskać więcej informacji, zobacz towarzyszące dokumentacji [pobieranie skryptu](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="ca598-135">For details, see the documentation accompanying the [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="ca598-136">Można również włączyć **AutoGrowShrink** klastra właściwości po wdrożeniu klastra za pomocą poleceń środowiska PowerShell klastra HPC opisane w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ca598-136">Alternatively, enable the **AutoGrowShrink** cluster property after you deploy the cluster by using HPC PowerShell commands described in the following section.</span></span> <span data-ttu-id="ca598-137">Aby przygotować się do tego, najpierw należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ca598-137">To prepare for this, first complete the following steps:</span></span>

  1. <span data-ttu-id="ca598-138">W węźle głównym i w subskrypcji platformy Azure, należy skonfigurować certyfikat zarządzania platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca598-138">Configure an Azure management certificate on the head node and in the Azure subscription.</span></span> <span data-ttu-id="ca598-139">W przypadku wdrożenia testu Użyj domyślnej Microsoft HPC Azure certyfikatu z podpisem własnym instalujący w węźle głównym HPC Pack i następnie przekaż certyfikat do subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca598-139">For a test deployment, you can use the Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on the head node, and then upload that certificate to your Azure subscription.</span></span> <span data-ttu-id="ca598-140">Dla opcji i procedury, zobacz [wskazówki w bibliotece TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca598-140">For options and steps, see the [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="ca598-141">Uruchom **regedit** w węźle głównym, przejdź do HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo i Dodaj wartość ciągu.</span><span class="sxs-lookup"><span data-stu-id="ca598-141">Run **regedit** on the head node, go to HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="ca598-142">Ustaw nazwę wartości "Odcisk palca", a wartość danych odcisk palca certyfikatu w kroku 1.</span><span class="sxs-lookup"><span data-stu-id="ca598-142">Set the Value name to “ThumbPrint”, and Value data to the thumbprint of the certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-to-set-the-autogrowshrink-property"></a><span data-ttu-id="ca598-143">Polecenia środowiska PowerShell klastra HPC, aby ustawić właściwość AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="ca598-143">HPC PowerShell commands to set the AutoGrowShrink property</span></span>
<span data-ttu-id="ca598-144">Poniżej przedstawiono przykładowe polecenia środowiska PowerShell klastra HPC, aby ustawić **AutoGrowShrink** i dostosować jego zachowanie w przypadku dodatkowych parametrów.</span><span class="sxs-lookup"><span data-stu-id="ca598-144">Following are sample HPC PowerShell commands to set **AutoGrowShrink** and to tune its behavior with additional parameters.</span></span> <span data-ttu-id="ca598-145">Zobacz [parametry AutoGrowShrink](#AutoGrowShrink-parameters) opisaną w tym artykule, aby uzyskać pełną listę ustawień.</span><span class="sxs-lookup"><span data-stu-id="ca598-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for the complete list of settings.</span></span>

<span data-ttu-id="ca598-146">Aby uruchomić te polecenia, uruchom program HPC PowerShell na węzła głównego klastra jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ca598-146">To run these commands, start HPC PowerShell on the cluster head node as an administrator.</span></span>

<span data-ttu-id="ca598-147">**Aby włączyć właściwość AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="ca598-147">**To enable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="ca598-148">**Aby wyłączyć właściwość AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="ca598-148">**To disable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="ca598-149">**Aby zmienić interwał wzrostu w minutach**</span><span class="sxs-lookup"><span data-stu-id="ca598-149">**To change the grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="ca598-150">**Aby zmienić interwał zmniejszania w minutach**</span><span class="sxs-lookup"><span data-stu-id="ca598-150">**To change the shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="ca598-151">**Aby wyświetlić bieżącą konfigurację AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="ca598-151">**To view the current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="ca598-152">**Aby wykluczyć węzeł grupy z AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="ca598-152">**To exclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="ca598-153">Ten parametr jest obsługiwane począwszy od HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="ca598-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="ca598-154">Parametry AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="ca598-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="ca598-155">Poniżej przedstawiono AutoGrowShrink parametry, które można modyfikować za pomocą **HpcClusterProperty zestaw** polecenia.</span><span class="sxs-lookup"><span data-stu-id="ca598-155">The following are AutoGrowShrink parameters that you can modify by using the **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="ca598-156">**EnableGrowShrink** — przełącznik, aby włączyć lub wyłączyć **AutoGrowShrink** właściwości.</span><span class="sxs-lookup"><span data-stu-id="ca598-156">**EnableGrowShrink** - Switch to enable or disable the **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="ca598-157">**ParamSweepTasksPerCore** — liczba zadań parametrycznych rośnie jednego rdzenia.</span><span class="sxs-lookup"><span data-stu-id="ca598-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks to grow one core.</span></span> <span data-ttu-id="ca598-158">Wartość domyślna to zwiększa jednego rdzenia poszczególnych zadań.</span><span class="sxs-lookup"><span data-stu-id="ca598-158">The default is to grow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ca598-159">Zmiany HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** do **TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="ca598-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** to **TasksPerResourceUnit**.</span></span> <span data-ttu-id="ca598-160">Jest oparty na typie zasobów zadania, a węzeł, gniazda lub core.</span><span class="sxs-lookup"><span data-stu-id="ca598-160">It is based on the job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="ca598-161">**GrowThreshold** — próg umieszczonych w kolejce zadań do wyzwalania automatycznego przyrostu.</span><span class="sxs-lookup"><span data-stu-id="ca598-161">**GrowThreshold** - Threshold of queued tasks to trigger automatic growth.</span></span> <span data-ttu-id="ca598-162">Wartość domyślna to 1, co oznacza, że jeśli 1 lub więcej zadań, znajduje się w stanie umieszczonych w kolejce, automatycznie rozszerzaj węzłów.</span><span class="sxs-lookup"><span data-stu-id="ca598-162">The default is 1, which means that if there are 1 or more tasks in the queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="ca598-163">**GrowInterval** — interwał w minutach, aby wyzwolić automatyczne zwiększanie rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="ca598-163">**GrowInterval** - Interval in minutes to trigger automatic growth.</span></span> <span data-ttu-id="ca598-164">Domyślny interwał wynosi 5 minut.</span><span class="sxs-lookup"><span data-stu-id="ca598-164">The default interval is 5 minutes.</span></span>
* <span data-ttu-id="ca598-165">**ShrinkInterval** — interwał w minutach, aby wyzwolić automatyczne zmniejszanie.</span><span class="sxs-lookup"><span data-stu-id="ca598-165">**ShrinkInterval** - Interval in minutes to trigger automatic shrinking.</span></span> <span data-ttu-id="ca598-166">Domyślny interwał wynosi 5 minut. |</span><span class="sxs-lookup"><span data-stu-id="ca598-166">The default interval is 5 minutes.|</span></span>
* <span data-ttu-id="ca598-167">**ShrinkIdleTimes** — liczba ciągłego kontroli Zmniejszaj, aby wskazać węzły są w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="ca598-167">**ShrinkIdleTimes** - Number of continuous checks to shrink to indicate the nodes are idle.</span></span> <span data-ttu-id="ca598-168">Wartość domyślna to 3 razy.</span><span class="sxs-lookup"><span data-stu-id="ca598-168">The default is 3 times.</span></span> <span data-ttu-id="ca598-169">Na przykład jeśli **ShrinkInterval** wynosi 5 minut, HPC Pack sprawdza, czy węzeł jest w stanie bezczynności co 5 minut.</span><span class="sxs-lookup"><span data-stu-id="ca598-169">For example, if the **ShrinkInterval** is 5 minutes, HPC Pack checks whether the node is idle every 5 minutes.</span></span> <span data-ttu-id="ca598-170">Jeśli węzły są w stanie bezczynności, po 3 ciągłego sprawdza (15 minut), HPC Pack zmniejsza tego węzła.</span><span class="sxs-lookup"><span data-stu-id="ca598-170">If the nodes are in the idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="ca598-171">**ExtraNodesGrowRatio** -procent dodatkowe węzły do zwiększenia zadań komunikat interfejsu (Passing Interface).</span><span class="sxs-lookup"><span data-stu-id="ca598-171">**ExtraNodesGrowRatio** - Additional percentage of nodes to grow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="ca598-172">Wartość domyślna to 1, co oznacza, że HPC Pack rozwoju węzłów % 1 dla zadań MPI.</span><span class="sxs-lookup"><span data-stu-id="ca598-172">The default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="ca598-173">**GrowByMin** — przełącznik, aby wskazać, czy zasady automatycznego przyrostu jest oparta na zasoby minimalne wymagane dla zadania.</span><span class="sxs-lookup"><span data-stu-id="ca598-173">**GrowByMin** - Switch to indicate whether the autogrow policy is based on the minimum resources required for the job.</span></span> <span data-ttu-id="ca598-174">Wartość domyślna to false, co oznacza, że HPC Pack rozwoju węzłów dla zadania w oparciu o maksymalnej zasoby wymagane do zadania.</span><span class="sxs-lookup"><span data-stu-id="ca598-174">The default is false, which means that HPC Pack grows nodes for jobs based on the maximum resources required for the jobs.</span></span>
* <span data-ttu-id="ca598-175">**SoaJobGrowThreshold** — próg przychodzących żądań SOA do wyzwalania automatycznego wzrostu procesu.</span><span class="sxs-lookup"><span data-stu-id="ca598-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests to trigger the automatic grow process.</span></span> <span data-ttu-id="ca598-176">Wartość domyślna to 50000.</span><span class="sxs-lookup"><span data-stu-id="ca598-176">The default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ca598-177">Ten parametr jest obsługiwana, począwszy od HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="ca598-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="ca598-178">**SoaRequestsPerCore** — liczba SOA przychodzących żądań do zwiększenia jednego rdzenia.</span><span class="sxs-lookup"><span data-stu-id="ca598-178">**SoaRequestsPerCore** -Number of incoming SOA requests to grow one core.</span></span> <span data-ttu-id="ca598-179">Wartość domyślna to 20000.</span><span class="sxs-lookup"><span data-stu-id="ca598-179">The default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="ca598-180">Ten parametr jest obsługiwana, począwszy od HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="ca598-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="ca598-181">**ExcludeNodeGroups** — węzły w grupach określony węzeł nie automatycznie zwiększyć lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="ca598-181">**ExcludeNodeGroups** – Nodes in the specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ca598-182">Ten parametr jest obsługiwana, począwszy od HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="ca598-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="ca598-183">Przykład MPI</span><span class="sxs-lookup"><span data-stu-id="ca598-183">MPI example</span></span>
<span data-ttu-id="ca598-184">Domyślnie HPC Pack rozwoju 1% dodatkowe węzły zadań MPI (**ExtraNodesGrowRatio** jest ustawiona na 1).</span><span class="sxs-lookup"><span data-stu-id="ca598-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set to 1).</span></span> <span data-ttu-id="ca598-185">Dzieje się tak MPI może wymagać wielu węzłów, czy zadanie można uruchomić tylko, gdy wszystkie węzły są gotowe.</span><span class="sxs-lookup"><span data-stu-id="ca598-185">The reason is that MPI may require multiple nodes, and the job can only run when all nodes are ready.</span></span> <span data-ttu-id="ca598-186">Po uruchomieniu węzłów Azure czasami jeden węzeł może być konieczne dłuższego czasu, aby rozpocząć od innych, powodując inne węzły ze stanu bezczynności podczas oczekiwania na tym węźle w celu przygotowania.</span><span class="sxs-lookup"><span data-stu-id="ca598-186">When Azure starts nodes, occasionally one node might need more time to start than others, causing other nodes to be idle while waiting for that node to get ready.</span></span> <span data-ttu-id="ca598-187">Powiększając dodatkowe węzły, HPC Pack skraca czas oczekiwania tego zasobu i potencjalnie zapisuje kosztów.</span><span class="sxs-lookup"><span data-stu-id="ca598-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="ca598-188">Aby zwiększyć stopień dodatkowe węzły zadań MPI (na przykład do 10%), uruchom polecenie podobne do</span><span class="sxs-lookup"><span data-stu-id="ca598-188">To increase the percentage of extra nodes for MPI jobs (for example, to 10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="ca598-189">Przykład SOA</span><span class="sxs-lookup"><span data-stu-id="ca598-189">SOA example</span></span>
<span data-ttu-id="ca598-190">Domyślnie **SoaJobGrowThreshold** ustawiono 50000 i **SoaRequestsPerCore** ustawiono 200000.</span><span class="sxs-lookup"><span data-stu-id="ca598-190">By default, **SoaJobGrowThreshold** is set to 50000 and **SoaRequestsPerCore** is set to 200000.</span></span> <span data-ttu-id="ca598-191">Jeśli prześlesz jedno zadanie SOA z żądaniami 70000 istnieje jedno zadanie w kolejce i żądania przychodzące są 70000.</span><span class="sxs-lookup"><span data-stu-id="ca598-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="ca598-192">W takim przypadku HPC Pack rozwoju 1 rdzeń umieszczonych w kolejce zadań i żądań przychodzących, rozwoju (70000 50000) / podstawowe 20000 = 1, dlatego w łącznie rozwoju 2 rdzeni dla tego zadania SOA.</span><span class="sxs-lookup"><span data-stu-id="ca598-192">In this case HPC Pack grows 1 core for the queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-the-azureautogrowshrinkps1-script"></a><span data-ttu-id="ca598-193">Uruchom skrypt AzureAutoGrowShrink.ps1</span><span class="sxs-lookup"><span data-stu-id="ca598-193">Run the AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="ca598-194">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ca598-194">Prerequisites</span></span>

* <span data-ttu-id="ca598-195">**HPC Pack 2012 R2 Update 1 lub nowszym klastra** - **AzureAutoGrowShrink.ps1** skryptów jest zainstalowany w folderze % CCP_HOME % bin.</span><span class="sxs-lookup"><span data-stu-id="ca598-195">**HPC Pack 2012 R2 Update 1 or later cluster** - The **AzureAutoGrowShrink.ps1** script is installed in the %CCP_HOME%bin folder.</span></span> <span data-ttu-id="ca598-196">Węzła głównego klastra może być wdrożona lokalnie lub w maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca598-196">The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="ca598-197">Zobacz [Konfigurowanie klastra hybrydowego pakietem HPC](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) rozpocząć pracę z węzłem głównym lokalnymi i węzły platformy Azure "serii".</span><span class="sxs-lookup"><span data-stu-id="ca598-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="ca598-198">Zobacz [skrypt wdrożenia HPC Pack IaaS](hpcpack-cluster-powershell-script.md) szybkie wdrożenie klastra HPC Pack w maszynach wirtualnych platformy Azure lub użyj [szablonie Szybki Start Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="ca598-198">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="ca598-199">**Program Azure PowerShell 1.4.0** -skrypt zależy od obecnie tę konkretną wersję programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ca598-199">**Azure PowerShell 1.4.0** - The script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="ca598-200">**Dla klastra przy użyciu platformy Azure serii węzłów** -uruchomić skrypt na komputerze klienckim, na których zainstalowano pakiet HPC lub w węźle głównym.</span><span class="sxs-lookup"><span data-stu-id="ca598-200">**For a cluster with Azure burst nodes** - Run the script on a client computer where HPC Pack is installed, or on the head node.</span></span> <span data-ttu-id="ca598-201">Jeśli uruchomiony na komputerze klienckim, upewnij się, że ustawienia zmiennej $env: CCP_SCHEDULER, aby wskazywał węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="ca598-201">If running on a client computer, ensure that you set the variable $env:CCP_SCHEDULER to point to the head node.</span></span> <span data-ttu-id="ca598-202">Węzły platformy Azure "serii" musi zostać dodany do klastra, ale mogą być w stanie wdrożyć nie.</span><span class="sxs-lookup"><span data-stu-id="ca598-202">The Azure “burst” nodes must be added to the cluster, but they may be in the Not-Deployed state.</span></span>
* <span data-ttu-id="ca598-203">**Dla klastra wdrożone w maszynach wirtualnych platformy Azure (modelu wdrażania usługi Resource Manager)** — dla klastra Azure maszyn wirtualnych wdrożonych w modelu wdrażania usługi Resource Manager, skrypt obsługuje dwie metody uwierzytelniania systemu Azure: Zaloguj się do konta platformy Azure, aby uruchomić skrypt zawsze (uruchamiając `Login-AzureRmAccount`, lub skonfiguruj nazwę główną usługi do uwierzytelniania przy użyciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ca598-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in the Resource Manager deployment model, the script supports two methods for Azure authentication: sign in to your Azure account to run the script every time (by running `Login-AzureRmAccount`, or configure a service principal to authenticate with a certificate.</span></span> <span data-ttu-id="ca598-204">HPC Pack dostarcza skrypt **ConfigARMAutoGrowShrinkCert.ps** można utworzyć nazwy głównej usługi o certyfikat.</span><span class="sxs-lookup"><span data-stu-id="ca598-204">HPC Pack provides the script **ConfigARMAutoGrowShrinkCert.ps** to create a service principal with certificate.</span></span> <span data-ttu-id="ca598-205">Skrypt tworzy aplikację usługi Azure Active Directory (Azure AD) i nazwy głównej usługi i przypisanie roli współautora do nazwy głównej usługi.</span><span class="sxs-lookup"><span data-stu-id="ca598-205">The script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns the Contributor role to the service principal.</span></span> <span data-ttu-id="ca598-206">Aby uruchomić skrypt, uruchom program Azure PowerShell jako administrator i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="ca598-206">To run the script, start Azure PowerShell  as administrator and run the following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="ca598-207">Aby uzyskać więcej informacji o **ConfigARMAutoGrowShrinkCert.ps1**Uruchom `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span><span class="sxs-lookup"><span data-stu-id="ca598-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="ca598-208">**Dla klastra wdrożone w maszynach wirtualnych platformy Azure (klasycznego modelu wdrażania)** — Uruchom skrypt w węźle głównym maszyny Wirtualnej, ponieważ zależy on od **Start HpcIaaSNode.ps1** i **Stop-HpcIaaSNode.ps1** skrypty, które są zainstalowane na.</span><span class="sxs-lookup"><span data-stu-id="ca598-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run the script on the head node VM, because it depends on the **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="ca598-209">Ponadto te skrypty wymagają certyfikatu zarządzania platformy Azure lub plik ustawień publikowania (zobacz [Zarządzaj węzłów obliczeniowych w HPC Pack klastra w systemie Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="ca598-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="ca598-210">Sprawdź, czy wszystkie węźle obliczeń maszyny wirtualne, konieczne są już dodane do klastra.</span><span class="sxs-lookup"><span data-stu-id="ca598-210">Make sure all the compute node VMs you need are already added to the cluster.</span></span> <span data-ttu-id="ca598-211">Mogą być w stanie zatrzymania.</span><span class="sxs-lookup"><span data-stu-id="ca598-211">They may be in the Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="ca598-212">Składnia</span><span class="sxs-lookup"><span data-stu-id="ca598-212">Syntax</span></span>
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
### <a name="parameters"></a><span data-ttu-id="ca598-213">Parametry</span><span class="sxs-lookup"><span data-stu-id="ca598-213">Parameters</span></span>
* <span data-ttu-id="ca598-214">**NodeTemplates** -nazwy szablonów węzła do zdefiniowania zakresu dla węzłów zwiększyć lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="ca598-214">**NodeTemplates** - Names of the node templates to define the scope for the nodes to grow and shrink.</span></span> <span data-ttu-id="ca598-215">Jeśli nie zostanie określony (wartość domyślna to @()), wszystkie węzły w **AzureNodes** węzła grupy są w zakres podczas **NodeType** ma wartość AzureNodes i we wszystkich węzłach w **ComputeNodes**węzeł grupy są w przypadku zakres **NodeType** ma wartość ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="ca598-215">If not specified (the default value is @()), all nodes in the **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in the **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="ca598-216">**JobTemplates** -nazwy szablonów zadań do zdefiniowania zakresu dla węzłów rośnie.</span><span class="sxs-lookup"><span data-stu-id="ca598-216">**JobTemplates** - Names of the job templates to define the scope for the nodes to grow.</span></span>
* <span data-ttu-id="ca598-217">**Typ NodeType** — typ węzeł, aby zwiększyć lub zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="ca598-217">**NodeType** - The type of node to grow and shrink.</span></span> <span data-ttu-id="ca598-218">Obsługiwane są następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="ca598-218">Supported values are:</span></span>

  * <span data-ttu-id="ca598-219">**AzureNodes** — w przypadku Azure PaaS (serii) węzły w lokalnej lub w klastrze IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca598-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="ca598-220">**ComputeNodes** — dla węzła obliczeniowego maszyn wirtualnych tylko w klastrze IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca598-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="ca598-221">**NumOfQueuedJobsPerNodeToGrow** -liczbę zadań umieszczonych w kolejce wymagane do zwiększenia jeden węzeł.</span><span class="sxs-lookup"><span data-stu-id="ca598-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required to grow one node.</span></span>
* <span data-ttu-id="ca598-222">**NumOfQueuedJobsToGrowThreshold** — próg liczbę zadań umieszczonych w kolejce do uruchomienia procesu wzrostu.</span><span class="sxs-lookup"><span data-stu-id="ca598-222">**NumOfQueuedJobsToGrowThreshold** - The threshold number of queued jobs to start the grow process.</span></span>
* <span data-ttu-id="ca598-223">**NumOfActiveQueuedTasksPerNodeToGrow** — liczba aktywnych w kolejce zadania wymagane do zwiększenia jeden węzeł.</span><span class="sxs-lookup"><span data-stu-id="ca598-223">**NumOfActiveQueuedTasksPerNodeToGrow** - The number of active queued tasks required to grow one node.</span></span> <span data-ttu-id="ca598-224">Jeśli **NumOfQueuedJobsPerNodeToGrow** zostanie podana wartość większą niż 0, ten parametr jest ignorowany.</span><span class="sxs-lookup"><span data-stu-id="ca598-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="ca598-225">**NumOfActiveQueuedTasksToGrowThreshold** — próg liczba aktywnych zadań w kolejce do uruchomienia procesu wzrostu.</span><span class="sxs-lookup"><span data-stu-id="ca598-225">**NumOfActiveQueuedTasksToGrowThreshold** - The threshold number of active queued tasks to start the grow process.</span></span>
* <span data-ttu-id="ca598-226">**NumOfInitialNodesToGrow** -początkowej minimalną liczbę węzłów do powiększania, jeśli wszystkie węzły w zakresie są **wdrożone nie** lub **zatrzymane (Deallocated)**.</span><span class="sxs-lookup"><span data-stu-id="ca598-226">**NumOfInitialNodesToGrow** - The initial minimum number of nodes to grow if all the nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="ca598-227">**GrowCheckIntervalMins** — interwał w minutach pomiędzy kontrole zwiększa się.</span><span class="sxs-lookup"><span data-stu-id="ca598-227">**GrowCheckIntervalMins** - The interval in minutes between checks to grow.</span></span>
* <span data-ttu-id="ca598-228">**ShrinkCheckIntervalMins** — interwał w minutach, między każdym sprawdzeniem, aby zmniejszyć.</span><span class="sxs-lookup"><span data-stu-id="ca598-228">**ShrinkCheckIntervalMins** - The interval in minutes between checks to shrink.</span></span>
* <span data-ttu-id="ca598-229">**ShrinkCheckIdleTimes** -kontroli zmniejszyć liczbę ciągłego (rozdzielone **ShrinkCheckIntervalMins**) wskazująca węzły są w stanie bezczynności.</span><span class="sxs-lookup"><span data-stu-id="ca598-229">**ShrinkCheckIdleTimes** - The number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) to indicate the nodes are idle.</span></span>
* <span data-ttu-id="ca598-230">**UseLastConfigurations** -powyższych konfiguracjach zapisane w pliku argumentu.</span><span class="sxs-lookup"><span data-stu-id="ca598-230">**UseLastConfigurations** - The previous configurations saved in the argument file.</span></span>
* <span data-ttu-id="ca598-231">**ArgFile**-nazwa pliku argumentu używany do zapisywania i aktualizowania konfiguracji, aby uruchomić skrypt.</span><span class="sxs-lookup"><span data-stu-id="ca598-231">**ArgFile**- The name of the argument file used to save and update the configurations to run the script.</span></span>
* <span data-ttu-id="ca598-232">**LogFilePrefix** — prefiks nazwy pliku dziennika.</span><span class="sxs-lookup"><span data-stu-id="ca598-232">**LogFilePrefix** - The prefix name of the log file.</span></span> <span data-ttu-id="ca598-233">Można określić ścieżkę.</span><span class="sxs-lookup"><span data-stu-id="ca598-233">You can specify a path.</span></span> <span data-ttu-id="ca598-234">Domyślnie dziennik jest zapisywany do bieżącego katalogu roboczego.</span><span class="sxs-lookup"><span data-stu-id="ca598-234">By default the log is written to the current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="ca598-235">Przykład 1</span><span class="sxs-lookup"><span data-stu-id="ca598-235">Example 1</span></span>
<span data-ttu-id="ca598-236">Poniższy przykład umożliwia skonfigurowanie węzłów Azure serii wdrożone z szablonem AzureNode domyślne, aby zwiększyć lub zmniejszyć automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ca598-236">The following example configures the Azure burst nodes deployed with the Default AzureNode Template to grow and shrink automatically.</span></span> <span data-ttu-id="ca598-237">Jeśli wszystkie węzły są początkowo w **wdrożone nie** stanu, są uruchamiane co najmniej 3 węzłach.</span><span class="sxs-lookup"><span data-stu-id="ca598-237">If all the nodes are initially in the **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="ca598-238">Jeśli liczba zadań w kolejce przekroczy 8, skrypt rozpoczyna węzłów aż do ich liczba przekracza stosunek zadania w kolejce **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="ca598-238">If the number of queued jobs exceeds 8, the script starts nodes until their number exceeds the ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="ca598-239">Jeśli węzeł zostanie znaleziony ze stanu bezczynności w 3 razy bezczynny, jest zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="ca598-239">If a node is found to be idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="ca598-240">Przykład 2</span><span class="sxs-lookup"><span data-stu-id="ca598-240">Example 2</span></span>
<span data-ttu-id="ca598-241">Poniższy przykład umożliwia skonfigurowanie maszyn wirtualnych wdrożonych przy użyciu szablonu ComputeNode domyślne, aby zwiększyć lub zmniejszyć automatycznie węzeł obliczeń platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ca598-241">The following example configures the Azure compute node VMs deployed with the Default ComputeNode Template to grow and shrink automatically.</span></span>
<span data-ttu-id="ca598-242">Zadania konfigurowane przez domyślny szablon zadania zdefiniować zakres obciążenia w klastrze.</span><span class="sxs-lookup"><span data-stu-id="ca598-242">The jobs configured by the Default job template define the scope of the workload on the cluster.</span></span> <span data-ttu-id="ca598-243">Jeśli wszystkie węzły są początkowo zatrzymana, są uruchamiane co najmniej 5 węzłów.</span><span class="sxs-lookup"><span data-stu-id="ca598-243">If all the nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="ca598-244">Jeśli liczba aktywnych zadań w kolejce przekroczy 15, uruchamia skrypt węzłów aż do ich liczba przekracza stosunek liczby aktywnych zadań w kolejce do **NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="ca598-244">If the number of active queued tasks exceeds 15, the script starts nodes until their number exceeds the ratio of active queued tasks to **NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="ca598-245">Jeśli węzeł zostanie znaleziony ze stanu bezczynności 10 kolejnych czas bezczynności, zostanie zatrzymana.</span><span class="sxs-lookup"><span data-stu-id="ca598-245">If a node is found to be idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
