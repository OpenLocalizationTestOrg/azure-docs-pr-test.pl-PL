---
title: "aaaHPC pakiet klastra dla programów Excel i SOA | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do uruchamiania dużych obciążeń programu Excel i SOA w klastrze HPC Pack na platformie Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="16df3-103">Wprowadzenie do uruchamiania obciążeń programu Excel i SOA w klastrze HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="16df3-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="16df3-104">W tym artykule opisano, jak toodeploy Microsoft HPC Pack 2012 R2 klastra na maszynach wirtualnych platformy Azure przy użyciu szablonu Azure Szybki Start lub opcjonalnie skrypt wdrażania środowiska Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16df3-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="16df3-105">klaster Hello używa toorun zaprojektowane obrazów maszyny Wirtualnej Azure Marketplace programu Microsoft Excel lub obciążeń zorientowane na usługę architektura (SOA) pakietem HPC.</span><span class="sxs-lookup"><span data-stu-id="16df3-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="16df3-106">Można użyć hello toorun klastra HPC dla programu Excel i usługi SOA z lokalnych komputera klienckiego.</span><span class="sxs-lookup"><span data-stu-id="16df3-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="16df3-107">usługi HPC dla programu Excel Hello obejmują odciążenia skoroszytu programu Excel i funkcje zdefiniowane przez użytkownika programu Excel lub funkcji UDF.</span><span class="sxs-lookup"><span data-stu-id="16df3-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="16df3-108">W tym artykule opiera się na funkcje, szablony i skryptów HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="16df3-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="16df3-109">W tym scenariuszu nie jest obecnie obsługiwane w HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="16df3-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="16df3-110">Na wysokim poziomie hello Poniższy diagram przedstawia klastra HPC Pack hello utworzony.</span><span class="sxs-lookup"><span data-stu-id="16df3-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![Klaster HPC z węzłami uruchamiania obciążeń programu Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="16df3-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16df3-112">Prerequisites</span></span>
* <span data-ttu-id="16df3-113">**Komputer kliencki** — możesz potrzebować klienta z systemem Windows komputera toosubmit próbki programu Excel i SOA zadania toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="16df3-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="16df3-114">Należy również Windows hello toorun komputera skrypt wdrożenia klastra programu Azure PowerShell (w przypadku wybrania tej metody wdrażania).</span><span class="sxs-lookup"><span data-stu-id="16df3-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="16df3-115">**Subskrypcja platformy Azure** — Jeśli nie masz subskrypcji platformy Azure, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="16df3-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="16df3-116">**Limit przydziału rdzeni** — może być konieczne tooincrease hello przydziału rdzeni, zwłaszcza, jeśli wdrożono kilka węzłów klastra z wielordzeniowych rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="16df3-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="16df3-117">Jeśli przy użyciu szablonu Azure szybkiego startu przydziału rdzeni hello w Menedżerze zasobów jest na region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16df3-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="16df3-118">W takim przypadku należy tooincrease hello przydziału w określonym regionie.</span><span class="sxs-lookup"><span data-stu-id="16df3-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="16df3-119">Zobacz [limity subskrypcji platformy Azure, przydziały i ograniczenia](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="16df3-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="16df3-120">limit przydziału, tooincrease [otwarcia żądania pomocy technicznej online klienta](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) bez dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="16df3-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="16df3-121">**Microsoft Office licencji** — Jeśli wdrażanie węzłów za pomocą obrazu maszyny Wirtualnej Marketplace HPC Pack 2012 R2 z programem Microsoft Excel, 30-dniowej wersji ewaluacyjnej programu Microsoft Excel Professional Plus 2013 zainstalowano obliczeń.</span><span class="sxs-lookup"><span data-stu-id="16df3-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="16df3-122">Po zakończeniu okresu próbnego hello wymagane tooprovide prawidłowy Microsoft Office licencji tooactivate Excel toocontinue toorun obciążeń.</span><span class="sxs-lookup"><span data-stu-id="16df3-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="16df3-123">Zobacz [aktywacji w programie Excel](#excel-activation) dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="16df3-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="16df3-124">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="16df3-124">Step 1.</span></span> <span data-ttu-id="16df3-125">Konfigurowanie klastra HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="16df3-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="16df3-126">Zostanie przedstawiony dwie opcje tooset zapasowej hello klastra HPC Pack 2012 R2: najpierw przy użyciu szablonu Azure Szybki Start i hello portal Azure. i sekundę, za pomocą skryptu wdrażania programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16df3-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="16df3-127">Opcja 1.</span><span class="sxs-lookup"><span data-stu-id="16df3-127">Option 1.</span></span> <span data-ttu-id="16df3-128">Szablon szybkiego startu</span><span class="sxs-lookup"><span data-stu-id="16df3-128">Use a quickstart template</span></span>
<span data-ttu-id="16df3-129">Użyj tooquickly szablonów Szybki Start Azure wdrożenie klastra HPC Pack w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="16df3-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="16df3-130">Po otwarciu szablonu hello w portalu hello, możesz uzyskać Interfejsu prostego, gdzie możesz wprowadzić ustawienia powitania dla klastra.</span><span class="sxs-lookup"><span data-stu-id="16df3-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="16df3-131">Poniżej przedstawiono kroki hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="16df3-132">Należy użyć [szablonu portalu Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) tworzącą podobne klastra specjalnie dla obciążeń programu Excel.</span><span class="sxs-lookup"><span data-stu-id="16df3-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="16df3-133">kroki Hello różnić się nieznacznie od następującego hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="16df3-134">Odwiedź hello [strony szablonu tworzenia klastrów HPC w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="16df3-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="16df3-135">Jeśli chcesz, przejrzyj informacje dotyczące szablonu hello i hello kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="16df3-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="16df3-136">Kliknij przycisk **wdrażanie tooAzure** toostart wdrożenia z szablonem hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="16df3-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![Wdrażanie szablonu tooAzure][github]
3. <span data-ttu-id="16df3-138">W portalu hello wykonaj te kroki tooenter hello parametry szablonu klastra HPC hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="16df3-139">a.</span><span class="sxs-lookup"><span data-stu-id="16df3-139">a.</span></span> <span data-ttu-id="16df3-140">Na powitania **parametry** strony, wprowadź lub zmień wartości parametrów szablonu hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="16df3-141">(Kliknij hello ikona dalej tooeach ustawienie informacji pomocy.) W powitania po ekranie przedstawiono przykładowe wartości.</span><span class="sxs-lookup"><span data-stu-id="16df3-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="16df3-142">W tym przykładzie jest tworzony klaster o nazwie *hpc01* w hello *hpc.local* węzły obliczeniowe domeny składające się z węzła głównego i 2.</span><span class="sxs-lookup"><span data-stu-id="16df3-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="16df3-143">węzły obliczeniowe Hello są tworzone na podstawie obrazu HPC Pack VM, który zawiera program Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="16df3-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Wprowadź parametry][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="16df3-145">Witaj węzła głównego maszyny Wirtualnej jest tworzona automatycznie na podstawie hello [najnowsze obrazu z witryny Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) HPC Pack 2012 R2 w systemie Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="16df3-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="16df3-146">Obecnie hello obraz jest oparty na HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="16df3-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="16df3-147">Maszyny wirtualne z węzła obliczeń są tworzone na podstawie obrazu najnowsze hello rodziny węzła obliczeń hello wybrane.</span><span class="sxs-lookup"><span data-stu-id="16df3-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="16df3-148">Wybierz hello **ComputeNodeWithExcel** opcję hello najnowsze HPC Pack obliczeń węzła obrazu zawierającego wersji ewaluacyjnej programu Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="16df3-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="16df3-149">toodeploy klastra dla sesji SOA ogólne lub włączenie odciążania UDF programu Excel, wybierz hello **ComputeNode** opcji (bez programu Excel zainstalowane).</span><span class="sxs-lookup"><span data-stu-id="16df3-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="16df3-150">b.</span><span class="sxs-lookup"><span data-stu-id="16df3-150">b.</span></span> <span data-ttu-id="16df3-151">Wybierz subskrypcję hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="16df3-152">c.</span><span class="sxs-lookup"><span data-stu-id="16df3-152">c.</span></span> <span data-ttu-id="16df3-153">Tworzenie grupy zasobów klastra hello, takich jak *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="16df3-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="16df3-154">d.</span><span class="sxs-lookup"><span data-stu-id="16df3-154">d.</span></span> <span data-ttu-id="16df3-155">Wybierz lokalizację dla grupy zasobów hello, takich jak środkowe stany USA.</span><span class="sxs-lookup"><span data-stu-id="16df3-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="16df3-156">e.</span><span class="sxs-lookup"><span data-stu-id="16df3-156">e.</span></span> <span data-ttu-id="16df3-157">Na powitania **postanowienia prawne** Przejrzyj postanowienia hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="16df3-158">Jeśli akceptujesz, kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="16df3-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="16df3-159">Następnie kliknij przycisk po zakończeniu ustawienie hello wartości dla szablonu hello **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="16df3-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="16df3-160">Po zakończeniu wdrażania hello (zwykle trwa około 30 minut), wyeksportować plik certyfikatu hello klastra z węzła głównego klastra hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="16df3-161">W kolejnym kroku należy zaimportować ten publiczny certyfikat na powitania uwierzytelnianie komputera klienckiego tooprovide powitania po stronie serwera dla bezpiecznego powiązania protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="16df3-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="16df3-162">a.</span><span class="sxs-lookup"><span data-stu-id="16df3-162">a.</span></span> <span data-ttu-id="16df3-163">W hello portalu Azure, przejdź do pozycji toohello pulpitu nawigacyjnego, wybierz hello węzła głównego i kliknij przycisk **Connect** u góry hello hello tooconnect strony przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="16df3-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="16df3-164">b.</span><span class="sxs-lookup"><span data-stu-id="16df3-164">b.</span></span> <span data-ttu-id="16df3-165">Użyj standardowych procedur w certyfikacie węzła głównego hello tooexport Menedżer certyfikatów (znajdujący się w obszarze Cert: \LocalMachine\My) bez klucza prywatnego hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="16df3-166">W tym przykładzie należy wyeksportować *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="16df3-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Wyeksportuj certyfikat hello][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="16df3-168">Opcja 2.</span><span class="sxs-lookup"><span data-stu-id="16df3-168">Option 2.</span></span> <span data-ttu-id="16df3-169">Użyj skryptu HPC Pack IaaS wdrożenia hello</span><span class="sxs-lookup"><span data-stu-id="16df3-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="16df3-170">Hello skrypt wdrożenia HPC Pack IaaS zawiera inny sposób elastyczne toodeploy klastra HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="16df3-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="16df3-171">Tworzy klaster w hello klasycznego modelu wdrażania, podczas gdy szablon hello używa modelu wdrażania usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="16df3-172">Ponadto hello skryptu jest zgodny z subskrypcji w hello Azure globalnych lub usługi chińskiej wersji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16df3-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="16df3-173">**Dodatkowe wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="16df3-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="16df3-174">**Program Azure PowerShell** - [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) (wersja 0.8.10 lub nowszego) na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="16df3-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="16df3-175">**Skrypt wdrożenia HPC Pack IaaS** — Pobierz i Rozpakuj hello najnowszą wersję hello skryptu z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="16df3-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="16df3-176">Sprawdź wersję hello skryptu hello uruchamiając `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="16df3-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="16df3-177">Ten artykuł jest oparty na wersji 4.5.0 lub nowszej hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="16df3-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="16df3-178">**Utwórz plik konfiguracji hello**</span><span class="sxs-lookup"><span data-stu-id="16df3-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="16df3-179">Witaj skrypt wdrożenia HPC Pack IaaS używa pliku konfiguracji XML jako dane wejściowe, który opisuje hello infrastruktura klastra HPC hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="16df3-180">toodeploy klaster składa się z węzłem głównym i 18 obliczeniowe węzłów tworzonych z obrazu węzła obliczeń hello, zawierający program Microsoft Excel, Zastąp wartości dla danego środowiska na powitania następującego przykładowego pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16df3-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="16df3-181">Aby uzyskać więcej informacji na temat hello pliku konfiguracji, zobacz hello Manual.rtf plik w folderze skryptów hello i [utworzyć klaster HPC z hello skrypt wdrożenia HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16df3-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="16df3-182">**Uwagi dotyczące hello pliku konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="16df3-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="16df3-183">Witaj **VMName** węzła głównego hello **musi** można hello takie same jak hello **ServiceName**, lub toorun niepowodzeniem zadań SOA.</span><span class="sxs-lookup"><span data-stu-id="16df3-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="16df3-184">Upewnij się, że możesz określić **EnableWebPortal** tak, aby hello węzła głównego certyfikatu jest generowane i eksportować.</span><span class="sxs-lookup"><span data-stu-id="16df3-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="16df3-185">Plik Hello określa skryptu środowiska PowerShell po konfiguracji PostConfig.ps1 uruchamianego na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="16df3-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="16df3-186">Hello następującego przykładowego skryptu konfiguruje parametry połączenia magazynu Azure hello usuwa rolę węzła obliczeń hello z węzłem głównym hello i oferuje wszystkie węzły w tryb online, gdy są one wdrażane.</span><span class="sxs-lookup"><span data-stu-id="16df3-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="16df3-187">**Uruchom skrypt hello**</span><span class="sxs-lookup"><span data-stu-id="16df3-187">**Run hello script**</span></span>

1. <span data-ttu-id="16df3-188">Otwórz konsolę programu PowerShell hello na komputerze klienckim hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="16df3-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="16df3-189">Zmień folder skryptu toohello katalogu (E:\IaaSClusterScript w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="16df3-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="16df3-190">toodeploy hello HPC Pack klastra, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="16df3-191">W tym przykładzie przyjęto założenie, że ten plik konfiguracji hello znajduje się w E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="16df3-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="16df3-192">Uruchamia Hello skrypt wdrożenia HPC Pack przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="16df3-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="16df3-193">Jeden element hello skrypt wykonuje jest tooexport i Pobierz certyfikat klastra hello i zapisz go w folderze dokumenty hello bieżącego użytkownika na komputerze klienckim hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="16df3-194">Witaj skrypt generuje następujące toohello podobne wiadomości.</span><span class="sxs-lookup"><span data-stu-id="16df3-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="16df3-195">W poniższym kroku należy zaimportować certyfikat hello w magazynie certyfikatów odpowiednich hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="16df3-196">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="16df3-196">Step 2.</span></span> <span data-ttu-id="16df3-197">Odciążanie skoroszytów programu Excel i uruchamiania funkcji UDF z klienta lokalnego</span><span class="sxs-lookup"><span data-stu-id="16df3-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="16df3-198">Aktywacja programu Excel</span><span class="sxs-lookup"><span data-stu-id="16df3-198">Excel activation</span></span>
<span data-ttu-id="16df3-199">W przypadku używania hello obrazu maszyny Wirtualnej ComputeNodeWithExcel dla obciążeń produkcyjnych, należy tooprovide prawidłowy Microsoft Office licencji klucza tooactivate programu Excel na powitania węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="16df3-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="16df3-200">W przeciwnym razie hello wersję ewaluacyjną programu Excel wygasa po 30 dniach, a systemem skoroszytów programu Excel zakończy się niepowodzeniem z hello COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="16df3-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="16df3-201">Można licencjonowania programu Excel o 30 dni oceny czasu: Zaloguj się na toohello węzła głównego i clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` na Excel wszystkie węzły za pomocą Menedżera klastra HPC obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="16df3-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="16df3-202">Można rearm maksymalnie dwa razy.</span><span class="sxs-lookup"><span data-stu-id="16df3-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="16df3-203">Po tym należy podać prawidłowy klucz licencji pakietu Office.</span><span class="sxs-lookup"><span data-stu-id="16df3-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="16df3-204">Witaj, Office Professional Plus 2013 zainstalować w obrazie maszyny Wirtualnej hello to wersja woluminu z ogólnym woluminu licencji klucza (GVLK).</span><span class="sxs-lookup"><span data-stu-id="16df3-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="16df3-205">Możesz to zrobić za pomocą usługi zarządzania kluczami (KMS) / aktywację opartą na usłudze (AD BA) lub klucza aktywacji wielokrotnej (MAK).</span><span class="sxs-lookup"><span data-stu-id="16df3-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="16df3-206">toouse usługi KMS/AD-BA, użyj istniejącego serwera usługi KMS lub skonfiguruj nową przy użyciu hello pakietu Microsoft Office 2013 woluminu licencji.</span><span class="sxs-lookup"><span data-stu-id="16df3-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="16df3-207">(Jeśli chcesz, skonfigurowanie powitania serwera na powitania węzła głównego.) Następnie Aktywuj klucz hosta usługi KMS hello za pośrednictwem hello Internetu lub telefonicznie.</span><span class="sxs-lookup"><span data-stu-id="16df3-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="16df3-208">Następnie clusrun `ospp.vbs` tooset hello serwera usługi KMS oraz port i aktywowanie pakietu Office na wszystkie węzły obliczeniowe programu Excel hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="16df3-209">toouse klucza MAK, pierwszy clusrun `ospp.vbs` tooinput hello klucza, a następnie uaktywnić wszystkie węzły obliczeniowe programu Excel hello za pośrednictwem hello Internetu lub telefonicznie.</span><span class="sxs-lookup"><span data-stu-id="16df3-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="16df3-210">Nie można używać Retail kluczami produktów Office Professional Plus 2013 z tego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="16df3-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="16df3-211">Jeśli masz prawidłowe klucze i nośnik instalacyjny dla wersji pakietu Office lub programu Excel innych niż ta wersja woluminu Office Professional Plus 2013 możesz ich użyć.</span><span class="sxs-lookup"><span data-stu-id="16df3-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="16df3-212">Najpierw Odinstaluj tę wersję woluminu i zainstalować hello wersji.</span><span class="sxs-lookup"><span data-stu-id="16df3-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="16df3-213">Witaj ponownie zainstalowana jako dostosowane toouse obrazu maszyny Wirtualnej w ramach wdrożenia na dużą skalę, można przechwycić węźle obliczeń programu Excel.</span><span class="sxs-lookup"><span data-stu-id="16df3-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="16df3-214">Odciążanie skoroszytów programu Excel</span><span class="sxs-lookup"><span data-stu-id="16df3-214">Offload Excel workbooks</span></span>
<span data-ttu-id="16df3-215">Wykonaj te kroki toooffload skoroszytu programu Excel, aby został uruchomiony w klastrze HPC Pack hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="16df3-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="16df3-216">toodo, musi mieć programu Excel 2010 lub 2013 już zainstalowana na komputerze klienckim hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="16df3-217">Użyj jednej z opcji hello w kroku 1 toodeploy klastra HPC Pack z hello Excel obliczeniowe obrazu węzła.</span><span class="sxs-lookup"><span data-stu-id="16df3-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="16df3-218">Uzyskaj hello klastra-plik certyfikatu (.cer) i klaster nazwy użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="16df3-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="16df3-219">Na komputerze klienckim hello zaimportuj certyfikat klastra hello w obszarze Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="16df3-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="16df3-220">Upewnij się, że zainstalowano programu Excel.</span><span class="sxs-lookup"><span data-stu-id="16df3-220">Make sure Excel is installed.</span></span> <span data-ttu-id="16df3-221">Utwórz plik Excel.exe.config z hello zawartości w powitania po tym samym folderze co Excel.exe na komputerze klienckim hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="16df3-222">Ten krok zapewnia, że załadowaniu tego hello — w modelu COM HPC Pack 2012 R2 programu Excel.</span><span class="sxs-lookup"><span data-stu-id="16df3-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="16df3-223">Konfigurowanie powitania klienta toosubmit zadania toohello HPC Pack klastra.</span><span class="sxs-lookup"><span data-stu-id="16df3-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="16df3-224">Jedną z opcji jest pełna hello toodownload [instalacji HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) i zainstalować powitania klienta HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="16df3-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="16df3-225">Można również pobrać i zainstalować hello [narzędzi klienta HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) i hello odpowiednie Visual C++ 2010 redistributable dla tego komputera ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="16df3-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="16df3-226">W tym przykładzie używamy próbki skoroszytu programu Excel o nazwie ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="16df3-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="16df3-227">Można go pobrać [tutaj](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="16df3-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="16df3-228">Skopiuj folder roboczy tooa skoroszytu programu Excel hello takich jak D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="16df3-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="16df3-229">Otwórz skoroszyt programu Excel hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-229">Open hello Excel workbook.</span></span> <span data-ttu-id="16df3-230">Na powitania **opracowanie** wstążki, kliknij przycisk **dodatki COM** i upewnij się, że hello dodatek HPC Pack Excel COM została pomyślnie załadowana.</span><span class="sxs-lookup"><span data-stu-id="16df3-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Dodatek dla pakietu HPC programu Excel][addin]
8. <span data-ttu-id="16df3-232">Edycji hello VBA makro HPCControlMacros w programie Excel, zmieniając hello oznaczone jako wierszy, jak pokazano w hello następującego skryptu.</span><span class="sxs-lookup"><span data-stu-id="16df3-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="16df3-233">Zastąp wartości odpowiednich dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="16df3-233">Substitute appropriate values for your environment.</span></span>
   
   ![Makra programu Excel dla pakietu HPC][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="16df3-235">Skopiuj katalog skoroszytu programu Excel hello przekazywania tooan takich jak D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="16df3-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="16df3-236">Ten katalog jest określony w stałej HPC_DependsFiles hello w makrze VBA hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="16df3-237">toorun hello skoroszytu w klastrze hello na platformie Azure, kliknij przycisk hello **klastra** przycisk hello arkusza.</span><span class="sxs-lookup"><span data-stu-id="16df3-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="16df3-238">Uruchom funkcje UDF programu Excel</span><span class="sxs-lookup"><span data-stu-id="16df3-238">Run Excel UDFs</span></span>
<span data-ttu-id="16df3-239">toorun plikami UDF programu Excel, wykonaj hello w poprzednich krokach 1 – 3 tooset powitania klienta komputera.</span><span class="sxs-lookup"><span data-stu-id="16df3-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="16df3-240">Dla funkcji UDF programu Excel nie potrzebujesz aplikacji Excel hello toohave zainstalowanej na węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="16df3-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="16df3-241">Tak, gdy węzły obliczeniowe tworzenia klastra, można wybrać obrazu węzła obliczeń normalne, zamiast hello obliczeniowe obrazu węzła przy użyciu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="16df3-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="16df3-242">Istnieje limit 34 znak w hello programu Excel 2010 i 2013 — okno dialogowe łącznik klastra.</span><span class="sxs-lookup"><span data-stu-id="16df3-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="16df3-243">Możesz użyć tego okna dialogowego pole toospecify hello klastra, który uruchamia hello funkcji UDF.</span><span class="sxs-lookup"><span data-stu-id="16df3-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="16df3-244">Jeśli nazwa klastra pełne hello jest dłuższy (na przykład hpcexcelhn01.southeastasia.cloudapp.azure.com), nie mieści się w oknie dialogowym hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="16df3-245">Witaj obejściem jest tooset zmiennej dla komputera, takich jak *CCP_IAASHN* z wartością hello hello klastra długie nazwy.</span><span class="sxs-lookup"><span data-stu-id="16df3-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="16df3-246">Następnie wprowadź *CCP_IAASHN %* w oknie dialogowym hello jako nazwa węzła głównego klastra hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="16df3-247">Po pomyślnym wdrożeniu klastra hello kontynuować hello następujące kroki toorun wbudowaną próbki UDF programu Excel.</span><span class="sxs-lookup"><span data-stu-id="16df3-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="16df3-248">Dostosowane plikami UDF programu Excel, zobacz te [zasobów](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLL i wdrożyć je w klastrze IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="16df3-249">Otwórz nowy skoroszyt programu Excel.</span><span class="sxs-lookup"><span data-stu-id="16df3-249">Open a new Excel workbook.</span></span> <span data-ttu-id="16df3-250">Na powitania **opracowanie** wstążki, kliknij przycisk **Add-Ins**. Następnie w oknie hello, kliknij przycisk **Przeglądaj**, przejdź do folderu %CCP_HOME%Bin\XLL32 toohello i wybierz próbki hello ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="16df3-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="16df3-251">Jeśli hello ClusterUDF32 nie istnieje na komputerze klienckim hello, skopiuj go w folderze %CCP_HOME%Bin\XLL32 hello na powitania węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="16df3-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Wybierz hello funkcji zdefiniowanej przez użytkownika][udf]
2. <span data-ttu-id="16df3-253">Kliknij przycisk **pliku** > **opcje** > **zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="16df3-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="16df3-254">W obszarze **formuły**, sprawdź **Zezwalaj użytkownika toorun funkcje XLL klastra obliczeniowego**.</span><span class="sxs-lookup"><span data-stu-id="16df3-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="16df3-255">Następnie kliknij przycisk **opcje** , a następnie wprowadź nazwę klastra pełne hello w **nazwy węzła głównego klastra**.</span><span class="sxs-lookup"><span data-stu-id="16df3-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="16df3-256">(Jakie zostały zanotowane wcześniej to pole wejściowe to ograniczona too34 znaków, tak długo nazwa_klastra może nie mieści się.</span><span class="sxs-lookup"><span data-stu-id="16df3-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="16df3-257">Można użyć zmiennej dla komputera, w tym miejscu dla nazwy klastra długie.)</span><span class="sxs-lookup"><span data-stu-id="16df3-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Skonfiguruj hello funkcji zdefiniowanej przez użytkownika][options]
3. <span data-ttu-id="16df3-259">toorun hello obliczania funkcji zdefiniowanej przez użytkownika w klastrze powitania kliknij komórkę hello z =XllGetComputerNameC() wartość i naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="16df3-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="16df3-260">Funkcja powitania po prostu pobiera nazwę hello hello węźle obliczeń, w których hello uruchamia funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="16df3-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="16df3-261">Dla pierwszego uruchomienia hello okno dialogowe poświadczeń wyświetli monit o hello nazwy użytkownika i hasła tooconnect toohello IaaS klastra.</span><span class="sxs-lookup"><span data-stu-id="16df3-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![Uruchamianie funkcji zdefiniowanej przez użytkownika][run]
   
   <span data-ttu-id="16df3-263">W przypadku wielu komórek toocalculate klawisz Ctrl-Alt-Shift + F9 toorun hello obliczeń na wszystkie komórki.</span><span class="sxs-lookup"><span data-stu-id="16df3-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="16df3-264">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="16df3-264">Step 3.</span></span> <span data-ttu-id="16df3-265">Uruchom obciążenia SOA z klienta lokalnego</span><span class="sxs-lookup"><span data-stu-id="16df3-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="16df3-266">toorun ogólne SOA aplikacji w klastrze HPC Pack IaaS hello, należy najpierw użyć jednej z metod hello w kroku 1 toodeploy hello klastra.</span><span class="sxs-lookup"><span data-stu-id="16df3-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="16df3-267">W takim przypadku Określ obrazu węzła obliczeń ogólnego, ponieważ nie ma potrzeby Excel na powitania węzłów obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="16df3-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="16df3-268">Następnie wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="16df3-268">Then follow these steps.</span></span>

1. <span data-ttu-id="16df3-269">Po pobraniu hello klastra certyfikatu, należy zaimportować go na komputerze klienckim hello w obszarze Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="16df3-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="16df3-270">Zainstaluj hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) i [narzędzi klienta HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="16df3-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="16df3-271">Te narzędzia umożliwiają toodevelop i uruchamianie aplikacji klienckich SOA.</span><span class="sxs-lookup"><span data-stu-id="16df3-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="16df3-272">Pobierz hello HelloWorldR2 [przykładowy kod](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="16df3-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="16df3-273">Otwórz hello HelloWorldR2.sln w Visual Studio 2010 lub 2012.</span><span class="sxs-lookup"><span data-stu-id="16df3-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="16df3-274">(Ten przykład nie jest obecnie zgodny z nowszej wersji programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="16df3-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="16df3-275">Tworzenie pierwszej kompilacji projektu EchoService hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-275">Build hello EchoService project first.</span></span> <span data-ttu-id="16df3-276">Następnie Wdróż hello usługi toohello IaaS klastra w hello taki sam sposób wdrażania tooan lokalnego klastra.</span><span class="sxs-lookup"><span data-stu-id="16df3-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="16df3-277">Aby uzyskać szczegółowe instrukcje Zobacz hello Readme.doc w HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="16df3-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="16df3-278">Modyfikowanie i tworzenie hello HellWorldR2 i inne projekty, zgodnie z opisem w powitania po sekcji toogenerate hello SOA aplikacji klienckich działających w klastrze IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="16df3-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="16df3-279">Używaj wiązania Http z kolejką usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="16df3-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="16df3-280">Wiązanie Http toouse z kolejką usługi Azure storage zmiany kilka toohello przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="16df3-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="16df3-281">Nazwa klastra hello aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="16df3-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="16df3-282">Opcjonalnie użyj domyślnej hello TransportScheme w SessionStartInfo lub jawnie ustaw tooHttp.</span><span class="sxs-lookup"><span data-stu-id="16df3-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="16df3-283">Użyj domyślnego powiązania dla hello BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="16df3-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="16df3-284">Ani nie ustawiaj jawnie użycie klasy basicHttpBinding hello.</span><span class="sxs-lookup"><span data-stu-id="16df3-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="16df3-285">Opcjonalnie można ustawić hello UseAzureQueue flagi tootrue w SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="16df3-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="16df3-286">Jeśli nie jest zestawem, zostanie ustawiona tootrue domyślnie gdy nazwa klastra hello sufiksy domen platformy Azure i hello TransportScheme jest protokół Http.</span><span class="sxs-lookup"><span data-stu-id="16df3-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="16df3-287">Używaj wiązania Http bez kolejki magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="16df3-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="16df3-288">Wiązanie Http toouse bez kolejki magazynu Azure, jawnie ustaw hello UseAzureQueue flagi toofalse w hello SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="16df3-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="16df3-289">Użyj NetTcp powiązania</span><span class="sxs-lookup"><span data-stu-id="16df3-289">Use NetTcp binding</span></span>
<span data-ttu-id="16df3-290">toouse NetTcp powiązanie, konfiguracja hello jest podobne tooconnecting tooan lokalnego klastra.</span><span class="sxs-lookup"><span data-stu-id="16df3-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="16df3-291">Należy tooopen kilka punktów końcowych na powitania węzła głównego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="16df3-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="16df3-292">Jeśli używasz hello HPC Pack IaaS wdrożenia skryptu toocreate hello klastra, na przykład punkty końcowe hello zestawu w hello portalu Azure w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="16df3-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="16df3-293">Zatrzymaj hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="16df3-293">Stop hello VM.</span></span>
2. <span data-ttu-id="16df3-294">Dodaj porty TCP hello 9090, 9087, 9091, Broker 9094 dla hello sesji, odpowiednio Broker pracownik i usługi danych</span><span class="sxs-lookup"><span data-stu-id="16df3-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Konfigurowanie punktów końcowych][endpoint-new-portal]
3. <span data-ttu-id="16df3-296">Uruchom hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="16df3-296">Start hello VM.</span></span>

<span data-ttu-id="16df3-297">Witaj aplikacji klienckiej SOA nie wymagają żadnych zmian, z wyjątkiem zmiany hello head toohello IaaS klastra Pełna nazwa.</span><span class="sxs-lookup"><span data-stu-id="16df3-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16df3-298">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16df3-298">Next steps</span></span>
* <span data-ttu-id="16df3-299">Zobacz [tych zasobów](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) uzyskać więcej informacji dotyczących uruchamiania obciążeń programu Excel z HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="16df3-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="16df3-300">Zobacz [Zarządzanie SOA usług Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) szczegółowe informacje na temat wdrażania i zarządzania usługami SOA pakietem HPC.</span><span class="sxs-lookup"><span data-stu-id="16df3-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
