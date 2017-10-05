---
title: "Klaster HPC Pack dla programów Excel i SOA | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 63babd94fdab15217cfb0757e4cd6efe458a628d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="e0c07-103">Wprowadzenie do uruchamiania obciążeń programu Excel i SOA w klastrze HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e0c07-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="e0c07-104">W tym artykule przedstawiono sposób wdrażania klastra Microsoft HPC Pack 2012 R2 na maszynach wirtualnych Azure przy użyciu szablonu Azure Szybki Start lub opcjonalnie skrypt wdrażania środowiska Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0c07-104">This article shows you how to deploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="e0c07-105">Klaster używa przeznaczonych do uruchamiania programu Microsoft Excel lub obciążeń zorientowane na usługę architektura (SOA) HPC Pack obrazów maszyny Wirtualnej Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e0c07-105">The cluster uses Azure Marketplace VM images designed to run Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="e0c07-106">Klastra służy do uruchamiania usług SOA i HPC dla programu Excel z lokalnych komputera klienckiego.</span><span class="sxs-lookup"><span data-stu-id="e0c07-106">You can use the cluster to run Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="e0c07-107">Usługi HPC dla programu Excel obejmują odciążenia skoroszytu programu Excel i funkcje zdefiniowane przez użytkownika programu Excel lub funkcji UDF.</span><span class="sxs-lookup"><span data-stu-id="e0c07-107">The Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="e0c07-108">W tym artykule opiera się na funkcje, szablony i skryptów HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e0c07-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="e0c07-109">W tym scenariuszu nie jest obecnie obsługiwane w HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="e0c07-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e0c07-110">Na wysokim poziomie na poniższym diagramie przedstawiono klastra HPC Pack, że utworzono.</span><span class="sxs-lookup"><span data-stu-id="e0c07-110">At a high level, the following diagram shows the HPC Pack cluster you create.</span></span>

![Klaster HPC z węzłami uruchamiania obciążeń programu Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="e0c07-112">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e0c07-112">Prerequisites</span></span>
* <span data-ttu-id="e0c07-113">**Komputer kliencki** — potrzebny jest komputer klienta z systemem Windows do przesyłania zadań programu Excel i SOA próbki do klastra.</span><span class="sxs-lookup"><span data-stu-id="e0c07-113">**Client computer** - You need a Windows-based client computer to submit sample Excel and SOA jobs to the cluster.</span></span> <span data-ttu-id="e0c07-114">Należy również komputerem z systemem Windows do uruchomienia skryptu wdrażania klastra programu Azure PowerShell (w przypadku wybrania tej metody wdrażania).</span><span class="sxs-lookup"><span data-stu-id="e0c07-114">You also need a Windows computer to run the Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="e0c07-115">**Subskrypcja platformy Azure** — Jeśli nie masz subskrypcji platformy Azure, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/) w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="e0c07-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="e0c07-116">**Limit przydziału rdzeni** — należy zwiększyć limit przydziału rdzeni, zwłaszcza, jeśli wdrożono kilka węzłów klastra z wielordzeniowych rozmiarów maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e0c07-116">**Cores quota** - You might need to increase the quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="e0c07-117">Jeśli przy użyciu szablonu Azure szybkiego startu przydziału rdzeni w Menedżerze zasobów jest na region platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c07-117">If you are using an Azure quickstart template, the cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="e0c07-118">W takim przypadku należy zwiększyć ten przydział w określonym regionie.</span><span class="sxs-lookup"><span data-stu-id="e0c07-118">In that case, you might need to increase the quota in a specific region.</span></span> <span data-ttu-id="e0c07-119">Zobacz [limity subskrypcji platformy Azure, przydziały i ograniczenia](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="e0c07-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="e0c07-120">Aby zwiększyć przydział, [otwarcia żądania pomocy technicznej online klienta](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) bez dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="e0c07-120">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="e0c07-121">**Microsoft Office licencji** — Jeśli wdrażanie węzłów za pomocą obrazu maszyny Wirtualnej Marketplace HPC Pack 2012 R2 z programem Microsoft Excel, 30-dniowej wersji ewaluacyjnej programu Microsoft Excel Professional Plus 2013 zainstalowano obliczeń.</span><span class="sxs-lookup"><span data-stu-id="e0c07-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="e0c07-122">Po okresie ewaluacyjnym konieczne jest zapewnienie prawidłowej licencji Microsoft Office, aby aktywować programu Excel, aby kontynuować uruchamianie obciążeń.</span><span class="sxs-lookup"><span data-stu-id="e0c07-122">After the evaluation period, you need to provide a valid Microsoft Office license to activate Excel to continue to run workloads.</span></span> <span data-ttu-id="e0c07-123">Zobacz [aktywacji w programie Excel](#excel-activation) dalszej części tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="e0c07-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="e0c07-124">Krok 1.</span><span class="sxs-lookup"><span data-stu-id="e0c07-124">Step 1.</span></span> <span data-ttu-id="e0c07-125">Konfigurowanie klastra HPC Pack na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="e0c07-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="e0c07-126">Zostanie przedstawiony dwie opcje do skonfigurowania klastra HPC Pack 2012 R2: najpierw przy użyciu szablonu Azure Szybki Start i portalu Azure; i sekundę, za pomocą skryptu wdrażania programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0c07-126">We show two options to set up the HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and the Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="e0c07-127">Opcja 1.</span><span class="sxs-lookup"><span data-stu-id="e0c07-127">Option 1.</span></span> <span data-ttu-id="e0c07-128">Szablon szybkiego startu</span><span class="sxs-lookup"><span data-stu-id="e0c07-128">Use a quickstart template</span></span>
<span data-ttu-id="e0c07-129">Szablon Szybki Start Azure umożliwia szybkie wdrożenie klastra HPC Pack w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c07-129">Use an Azure quickstart template to quickly deploy an HPC Pack cluster in the Azure portal.</span></span> <span data-ttu-id="e0c07-130">Po otwarciu szablonu w portalu można uzyskać Interfejsu prostego, gdzie możesz wprowadzić ustawienia dla klastra.</span><span class="sxs-lookup"><span data-stu-id="e0c07-130">When you open the template in the portal, you get a simple UI where you enter the settings for your cluster.</span></span> <span data-ttu-id="e0c07-131">Poniżej przedstawiono kroki.</span><span class="sxs-lookup"><span data-stu-id="e0c07-131">Here are the steps.</span></span> 

> [!TIP]
> <span data-ttu-id="e0c07-132">Należy użyć [szablonu portalu Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) tworzącą podobne klastra specjalnie dla obciążeń programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="e0c07-133">Spośród następujących kroków różnić się nieznacznie.</span><span class="sxs-lookup"><span data-stu-id="e0c07-133">The steps differ slightly from the following.</span></span>
> 
> 

1. <span data-ttu-id="e0c07-134">Odwiedź stronę [strony szablonu tworzenia klastrów HPC w serwisie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="e0c07-134">Visit the [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="e0c07-135">Jeśli chcesz, przejrzyj informacje dotyczące szablonu i kod źródłowy.</span><span class="sxs-lookup"><span data-stu-id="e0c07-135">If you want, review information about the template and the source code.</span></span>
2. <span data-ttu-id="e0c07-136">Kliknij przycisk **wdrażanie na platformie Azure** rozpocząć wdrażanie przy użyciu szablonu w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c07-136">Click **Deploy to Azure** to start a deployment with the template in the Azure portal.</span></span>
   
   ![Wdrażanie szablonu na platformie Azure][github]
3. <span data-ttu-id="e0c07-138">W portalu wykonaj następujące kroki, aby wprowadzić parametry szablonu klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="e0c07-138">In the portal, follow these steps to enter the parameters for the HPC cluster template.</span></span>
   
   <span data-ttu-id="e0c07-139">a.</span><span class="sxs-lookup"><span data-stu-id="e0c07-139">a.</span></span> <span data-ttu-id="e0c07-140">Na **parametry** strony, wprowadź lub zmień wartości parametrów szablonu.</span><span class="sxs-lookup"><span data-stu-id="e0c07-140">On the **Parameters** page, enter or modify values for the template parameters.</span></span> <span data-ttu-id="e0c07-141">(Kliknij ikonę obok każdego ustawienia, aby uzyskać pomoc.) W poniższym ekranie przedstawiono przykładowe wartości.</span><span class="sxs-lookup"><span data-stu-id="e0c07-141">(Click the icon next to each setting for help information.) Sample values are shown in the following screen.</span></span> <span data-ttu-id="e0c07-142">W tym przykładzie jest tworzony klaster o nazwie *hpc01* w *hpc.local* węzły obliczeniowe domeny składające się z węzła głównego i 2.</span><span class="sxs-lookup"><span data-stu-id="e0c07-142">This example creates a cluster named *hpc01* in the *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="e0c07-143">Węzły obliczeniowe są tworzone na podstawie obrazu HPC Pack VM, który zawiera program Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-143">The compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Wprowadź parametry][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="e0c07-145">Maszyna wirtualna jest utworzona automatycznie z węzłem głównym [najnowsze obrazu z witryny Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) HPC Pack 2012 R2 w systemie Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="e0c07-145">The head node VM is created automatically from the [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="e0c07-146">Obecnie obraz jest oparty na HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="e0c07-146">Currently the image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="e0c07-147">Maszyny wirtualne z węzła obliczeń są tworzone na podstawie najnowszej obraz rodziny węzła obliczeń wybranych.</span><span class="sxs-lookup"><span data-stu-id="e0c07-147">Compute node VMs are created from the latest image of the selected compute node family.</span></span> <span data-ttu-id="e0c07-148">Wybierz **ComputeNodeWithExcel** opcji dla najnowszego pakietu HPC obliczeniowe obrazu węzła, który obejmuje wersji ewaluacyjnej programu Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="e0c07-148">Select the **ComputeNodeWithExcel** option for the latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="e0c07-149">Aby wdrożyć klaster ogólne SOA sesji lub Odciążanie UDF programu Excel, wybierz **ComputeNode** opcji (bez programu Excel zainstalowane).</span><span class="sxs-lookup"><span data-stu-id="e0c07-149">To deploy a cluster for general SOA sessions or for Excel UDF offloading, choose the **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="e0c07-150">b.</span><span class="sxs-lookup"><span data-stu-id="e0c07-150">b.</span></span> <span data-ttu-id="e0c07-151">Wybierz subskrypcję.</span><span class="sxs-lookup"><span data-stu-id="e0c07-151">Choose the subscription.</span></span>
   
   <span data-ttu-id="e0c07-152">c.</span><span class="sxs-lookup"><span data-stu-id="e0c07-152">c.</span></span> <span data-ttu-id="e0c07-153">Tworzenie grupy zasobów klastra, takich jak *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="e0c07-153">Create a resource group for the cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="e0c07-154">d.</span><span class="sxs-lookup"><span data-stu-id="e0c07-154">d.</span></span> <span data-ttu-id="e0c07-155">Wybierz lokalizację dla grupy zasobów, takich jak środkowe stany USA.</span><span class="sxs-lookup"><span data-stu-id="e0c07-155">Choose a location for the resource group, such as Central US.</span></span>
   
   <span data-ttu-id="e0c07-156">e.</span><span class="sxs-lookup"><span data-stu-id="e0c07-156">e.</span></span> <span data-ttu-id="e0c07-157">Na **postanowienia prawne** Przejrzyj postanowienia.</span><span class="sxs-lookup"><span data-stu-id="e0c07-157">On the **Legal terms** page, review the terms.</span></span> <span data-ttu-id="e0c07-158">Jeśli akceptujesz, kliknij przycisk **zakupu**.</span><span class="sxs-lookup"><span data-stu-id="e0c07-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="e0c07-159">Następnie, po zakończeniu ustawienie wartości dla szablonu, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e0c07-159">Then, when you are finished setting the values for the template, click **Create**.</span></span>
4. <span data-ttu-id="e0c07-160">Po zakończeniu wdrożenia (zwykle trwa około 30 minut), eksportowania pliku certyfikatu klastra z węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="e0c07-160">When the deployment completes (it typically takes around 30 minutes), export the cluster certificate file from the cluster head node.</span></span> <span data-ttu-id="e0c07-161">W kolejnym kroku należy zaimportować ten publiczny certyfikat na komputerze klienckim, aby zapewnić uwierzytelnianie po stronie serwera dla bezpiecznego powiązania protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e0c07-161">In a later step, you import this public certificate on the client computer to provide the server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="e0c07-162">a.</span><span class="sxs-lookup"><span data-stu-id="e0c07-162">a.</span></span> <span data-ttu-id="e0c07-163">W portalu Azure, przejdź do pulpitu nawigacyjnego, wybierz węzła głównego, a następnie kliknij przycisk **Connect** w górnej części strony, aby połączyć się przy użyciu pulpitu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="e0c07-163">In the Azure portal, go to the dashboard, select the head node, and click **Connect** at the top of the page to connect using Remote Desktop.</span></span>
   
    <!-- ![Connect to the head node][connect] -->
   
   <span data-ttu-id="e0c07-164">b.</span><span class="sxs-lookup"><span data-stu-id="e0c07-164">b.</span></span> <span data-ttu-id="e0c07-165">Użyj standardowych procedur w Menedżerze certyfikatów, aby wyeksportować certyfikat węzła głównego (znajdujący się w obszarze Cert: \LocalMachine\My) bez klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="e0c07-165">Use standard procedures in Certificate Manager to export the head node certificate (located under Cert:\LocalMachine\My) without the private key.</span></span> <span data-ttu-id="e0c07-166">W tym przykładzie należy wyeksportować *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="e0c07-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Eksportowanie certyfikatu][cert]

### <a name="option-2-use-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="e0c07-168">Opcja 2.</span><span class="sxs-lookup"><span data-stu-id="e0c07-168">Option 2.</span></span> <span data-ttu-id="e0c07-169">Użyj skryptu HPC Pack IaaS wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e0c07-169">Use the HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="e0c07-170">Skrypt wdrożenia HPC Pack IaaS umożliwia innym elastyczne wdrożenie klastra HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="e0c07-170">The HPC Pack IaaS deployment script provides another versatile way to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="e0c07-171">Tworzy klaster w klasycznym modelu wdrażania, podczas gdy szablon korzysta z modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0c07-171">It creates a cluster in the classic deployment model, whereas the template uses the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e0c07-172">Ponadto skryptu jest zgodny z subskrypcją w usłudze Azure globalne lub chińskiej wersji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c07-172">Also, the script is compatible with a subscription in either the Azure Global or Azure China service.</span></span>

<span data-ttu-id="e0c07-173">**Dodatkowe wymagania wstępne**</span><span class="sxs-lookup"><span data-stu-id="e0c07-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="e0c07-174">**Program Azure PowerShell** - [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) (wersja 0.8.10 lub nowszego) na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="e0c07-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="e0c07-175">**Skrypt wdrożenia HPC Pack IaaS** — Pobierz i Rozpakuj najnowszej wersji skryptu z [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="e0c07-175">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="e0c07-176">Sprawdź wersję skryptu, uruchamiając `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="e0c07-176">Check the version of the script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="e0c07-177">Ten artykuł jest oparty na wersji 4.5.0 lub nowszej skryptu.</span><span class="sxs-lookup"><span data-stu-id="e0c07-177">This article is based on version 4.5.0 or later of the script.</span></span>

<span data-ttu-id="e0c07-178">**Utwórz plik konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="e0c07-178">**Create the configuration file**</span></span>

 <span data-ttu-id="e0c07-179">Skrypt wdrażania HPC Pack IaaS używa pliku konfiguracji XML jako dane wejściowe, który opisuje infrastruktura klastra HPC.</span><span class="sxs-lookup"><span data-stu-id="e0c07-179">The HPC Pack IaaS deployment script uses an XML configuration file as input that describes the infrastructure of the HPC cluster.</span></span> <span data-ttu-id="e0c07-180">Aby wdrożyć klaster składa się z węzłem głównym i 18 węzły obliczeniowe utworzone na podstawie obrazu węzła obliczeń, który zawiera program Microsoft Excel, Zastąp wartości w danym środowisku, w poniższym przykładowym pliku konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e0c07-180">To deploy a cluster consisting of a head node and 18 compute nodes created from the compute node image that includes Microsoft Excel, substitute values for your environment into the following sample configuration file.</span></span> <span data-ttu-id="e0c07-181">Aby uzyskać więcej informacji o pliku konfiguracji, zobacz plik Manual.rtf w folderze skryptów i [utworzyć klaster HPC z skrypt wdrożenia HPC Pack IaaS](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0c07-181">For more information about the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="e0c07-182">**Uwagi dotyczące pliku konfiguracji**</span><span class="sxs-lookup"><span data-stu-id="e0c07-182">**Notes about the configuration file**</span></span>

* <span data-ttu-id="e0c07-183">**VMName** węzła głównego **musi** być taka sama jak **ServiceName**, lub zadań SOA nie udało się uruchomić.</span><span class="sxs-lookup"><span data-stu-id="e0c07-183">The **VMName** of the head node **MUST** be the same as the **ServiceName**, or SOA jobs fail to run.</span></span>
* <span data-ttu-id="e0c07-184">Upewnij się, że możesz określić **EnableWebPortal** tak, aby certyfikat węzła głównego jest generowany i wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="e0c07-184">Make sure you specify **EnableWebPortal** so that the head node certificate is generated and exported.</span></span>
* <span data-ttu-id="e0c07-185">Plik Określa skryptu środowiska PowerShell po konfiguracji PostConfig.ps1 działającą z węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="e0c07-185">The file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on the head node.</span></span> <span data-ttu-id="e0c07-186">Poniższy przykładowy skrypt umożliwia skonfigurowanie parametrów połączenia magazynu Azure, usuwa rolę węzła obliczeń z węzła głównego i oferuje wszystkie węzły w tryb online, gdy są one wdrażane.</span><span class="sxs-lookup"><span data-stu-id="e0c07-186">THe following sample script configures the Azure storage connection string, removes the compute node role from the head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add the HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set the Azure storage connection string for the cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove the compute node role for head node to make sure the Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in the deployment including the head node and compute nodes, which should match the number specified in the XML configuration file
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

<span data-ttu-id="e0c07-187">**Uruchom skrypt**</span><span class="sxs-lookup"><span data-stu-id="e0c07-187">**Run the script**</span></span>

1. <span data-ttu-id="e0c07-188">Otwórz konsolę programu PowerShell na komputerze klienckim jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e0c07-188">Open the PowerShell console on the client computer as an administrator.</span></span>
2. <span data-ttu-id="e0c07-189">Zmień katalog na folder skryptów (E:\IaaSClusterScript w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="e0c07-189">Change directory to the script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="e0c07-190">Aby wdrożyć klaster HPC Pack, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="e0c07-190">To deploy the HPC Pack cluster, run the following command.</span></span> <span data-ttu-id="e0c07-191">W tym przykładzie przyjęto założenie, że plik konfiguracji znajduje się w E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="e0c07-191">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="e0c07-192">Uruchamia skrypt wdrożenia HPC Pack przez pewien czas.</span><span class="sxs-lookup"><span data-stu-id="e0c07-192">The HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="e0c07-193">Jedyną operacją, której ten skrypt wykonuje się wyeksportować i Pobierz certyfikat klastra i zapisz go w folderze dokumenty bieżącego użytkownika na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="e0c07-193">One thing the script does is to export and download the cluster certificate and save it in the current user’s Documents folder on the client computer.</span></span> <span data-ttu-id="e0c07-194">Skrypt generuje komunikat podobny do następującego.</span><span class="sxs-lookup"><span data-stu-id="e0c07-194">The script generates a message similar to the following.</span></span> <span data-ttu-id="e0c07-195">W poniższym kroku należy zaimportować certyfikat w magazynie odpowiedni certyfikat.</span><span class="sxs-lookup"><span data-stu-id="e0c07-195">In a following step, you import the certificate in the appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import the following certificate in the Trusted Root Certification Authorities certificate store on the computer where you are submitting job or accessing the HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="e0c07-196">Krok 2.</span><span class="sxs-lookup"><span data-stu-id="e0c07-196">Step 2.</span></span> <span data-ttu-id="e0c07-197">Odciążanie skoroszytów programu Excel i uruchamiania funkcji UDF z klienta lokalnego</span><span class="sxs-lookup"><span data-stu-id="e0c07-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="e0c07-198">Aktywacja programu Excel</span><span class="sxs-lookup"><span data-stu-id="e0c07-198">Excel activation</span></span>
<span data-ttu-id="e0c07-199">W przypadku używania obrazu maszyny Wirtualnej ComputeNodeWithExcel dla obciążeń produkcyjnych, musisz podać prawidłowy klucz licencji Microsoft Office do aktywacji programu Excel w węzłach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="e0c07-199">When using the ComputeNodeWithExcel VM image for production workloads, you need to provide a valid Microsoft Office license key to activate Excel on the compute nodes.</span></span> <span data-ttu-id="e0c07-200">W przeciwnym razie wersję ewaluacyjną programu Excel wygasa po 30 dniach, a systemem skoroszytów programu Excel zakończy się niepowodzeniem z COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="e0c07-200">Otherwise, the evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with the COMException (0x800AC472).</span></span> 

<span data-ttu-id="e0c07-201">Można licencjonowania programu Excel o 30 dni oceny czasu: Zaloguj się do węzła głównego i clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` na Excel wszystkie węzły za pomocą Menedżera klastra HPC obliczeniowe.</span><span class="sxs-lookup"><span data-stu-id="e0c07-201">You can rearm Excel for another 30 days of evaluation time: Log on to the head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="e0c07-202">Można rearm maksymalnie dwa razy.</span><span class="sxs-lookup"><span data-stu-id="e0c07-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="e0c07-203">Po tym należy podać prawidłowy klucz licencji pakietu Office.</span><span class="sxs-lookup"><span data-stu-id="e0c07-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="e0c07-204">Pakiet Office Professional Plus 2013 zainstalować w obrazie maszyny Wirtualnej to wersja woluminu z ogólnym woluminu licencji klucza (GVLK).</span><span class="sxs-lookup"><span data-stu-id="e0c07-204">The Office Professional Plus 2013 installed on the VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="e0c07-205">Możesz to zrobić za pomocą usługi zarządzania kluczami (KMS) / aktywację opartą na usłudze (AD BA) lub klucza aktywacji wielokrotnej (MAK).</span><span class="sxs-lookup"><span data-stu-id="e0c07-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="e0c07-206">Aby korzystać z usługi KMS/AD-BA, użyj istniejącego serwera usługi KMS, lub skonfigurować nową przy użyciu pakietu Microsoft Office 2013 woluminu licencji.</span><span class="sxs-lookup"><span data-stu-id="e0c07-206">To use KMS/AD-BA, use an existing KMS server or set up a new one by using the Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="e0c07-207">(Jeśli chcesz, skonfigurować serwer w węźle głównym). Następnie Aktywuj klucz hosta usługi KMS za pośrednictwem telefonu lub Internetu.</span><span class="sxs-lookup"><span data-stu-id="e0c07-207">(If you want to, set up the server on the head node.) Then, activate the KMS host key via the Internet or telephone.</span></span> <span data-ttu-id="e0c07-208">Następnie clusrun `ospp.vbs` Ustaw serwer usługi KMS i portu i aktywowanie pakietu Office na wszystkie węzły obliczeniowe programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-208">Then clusrun `ospp.vbs` to set the KMS server and port and activate Office on all the Excel compute nodes.</span></span> 

    * <span data-ttu-id="e0c07-209">Aby za pomocą klucza MAK, pierwszy clusrun `ospp.vbs` wprowadzić klucz i aktywować wszystkie węzły za pośrednictwem Internetu lub telefonu obliczeniowe programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-209">To use MAK, first clusrun `ospp.vbs` to input the key and then activate all the Excel compute nodes via the Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="e0c07-210">Nie można używać Retail kluczami produktów Office Professional Plus 2013 z tego obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0c07-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="e0c07-211">Jeśli masz prawidłowe klucze i nośnik instalacyjny dla wersji pakietu Office lub programu Excel innych niż ta wersja woluminu Office Professional Plus 2013 możesz ich użyć.</span><span class="sxs-lookup"><span data-stu-id="e0c07-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="e0c07-212">Najpierw Odinstaluj tę wersję woluminu i zainstaluj wersję, do której masz.</span><span class="sxs-lookup"><span data-stu-id="e0c07-212">First uninstall this volume edition and install the edition that you have.</span></span> <span data-ttu-id="e0c07-213">Ponownie węźle obliczeń programu Excel, można przechwycić jako dostosowanego obrazu maszyny Wirtualnej do użycia w ramach wdrożenia na dużą skalę.</span><span class="sxs-lookup"><span data-stu-id="e0c07-213">The reinstalled Excel compute node can be captured as a customized VM image to use in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="e0c07-214">Odciążanie skoroszytów programu Excel</span><span class="sxs-lookup"><span data-stu-id="e0c07-214">Offload Excel workbooks</span></span>
<span data-ttu-id="e0c07-215">Wykonaj następujące kroki w celu odciążenia skoroszytu programu Excel, aby został uruchomiony w klastrze HPC Pack na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c07-215">Follow these steps to offload an Excel workbook so that it runs on the HPC Pack cluster in Azure.</span></span> <span data-ttu-id="e0c07-216">Aby to zrobić, musi mieć programu Excel 2010 lub 2013 już zainstalowana na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="e0c07-216">To do this, you must have Excel 2010 or 2013 already installed on the client computer.</span></span>

1. <span data-ttu-id="e0c07-217">Użyj jednej z opcji w kroku 1, aby wdrożyć klaster HPC Pack z programu Excel obliczeniowe obrazu węzła.</span><span class="sxs-lookup"><span data-stu-id="e0c07-217">Use one of the options in Step 1 to deploy an HPC Pack cluster with the Excel compute node image.</span></span> <span data-ttu-id="e0c07-218">Uzyskaj klastra pliku certyfikatu (.cer) i nazwy klastra użytkownika i hasła.</span><span class="sxs-lookup"><span data-stu-id="e0c07-218">Obtain the cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="e0c07-219">Na komputerze klienckim należy zaimportować certyfikat do klastra, w obszarze Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="e0c07-219">On the client computer, import the cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="e0c07-220">Upewnij się, że zainstalowano programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-220">Make sure Excel is installed.</span></span> <span data-ttu-id="e0c07-221">Utwórz plik Excel.exe.config z następującą zawartość w tym samym folderze co Excel.exe na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="e0c07-221">Create an Excel.exe.config file with the following contents in the same folder as Excel.exe on the client computer.</span></span> <span data-ttu-id="e0c07-222">Ten krok zapewnia, że dodatek HPC Pack 2012 R2 Excel COM załadowaniu.</span><span class="sxs-lookup"><span data-stu-id="e0c07-222">This step ensures that the HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="e0c07-223">Konfigurowanie klienta umożliwiają przesyłanie zadań do klastra HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="e0c07-223">Set up the client to submit jobs to the HPC Pack cluster.</span></span> <span data-ttu-id="e0c07-224">Jedną z opcji jest pobranie pełnego [instalacji HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) i zainstaluj klienta HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="e0c07-224">One option is to download the full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install the HPC Pack client.</span></span> <span data-ttu-id="e0c07-225">Można również pobrać i zainstalować [narzędzi klienta HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) i odpowiednie Visual C++ 2010 redistributable dla tego komputera ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555) ).</span><span class="sxs-lookup"><span data-stu-id="e0c07-225">Alternatively, download and install the [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and the appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="e0c07-226">W tym przykładzie używamy próbki skoroszytu programu Excel o nazwie ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="e0c07-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="e0c07-227">Można go pobrać [tutaj](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="e0c07-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="e0c07-228">Skopiuj skoroszytu programu Excel do folderu roboczego, takich jak D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="e0c07-228">Copy the Excel workbook to a working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="e0c07-229">Otwórz skoroszyt programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-229">Open the Excel workbook.</span></span> <span data-ttu-id="e0c07-230">Na **opracowanie** wstążki, kliknij przycisk **dodatki COM** i upewnij się, że dodatek HPC Pack Excel COM został załadowany pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="e0c07-230">On the **Develop** ribbon, click **COM Add-Ins** and confirm that the HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Dodatek dla pakietu HPC programu Excel][addin]
8. <span data-ttu-id="e0c07-232">Edytuj makro VBA HPCControlMacros w programie Excel, zmieniając komentarze wierszy, jak pokazano w poniższym skrypcie.</span><span class="sxs-lookup"><span data-stu-id="e0c07-232">Edit the VBA macro HPCControlMacros in Excel by changing the commented lines as shown in the following script.</span></span> <span data-ttu-id="e0c07-233">Zastąp wartości odpowiednich dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="e0c07-233">Substitute appropriate values for your environment.</span></span>
   
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
9. <span data-ttu-id="e0c07-235">Skopiuj skoroszytu programu Excel do katalogu przekazywania, takich jak D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="e0c07-235">Copy the Excel workbook to an upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="e0c07-236">Ten katalog jest określony w stałej HPC_DependsFiles w makrze VBA.</span><span class="sxs-lookup"><span data-stu-id="e0c07-236">This directory is specified in the HPC_DependsFiles constant in the VBA macro.</span></span>
10. <span data-ttu-id="e0c07-237">Aby uruchomić skoroszytu w klastrze na platformie Azure, kliknij przycisk **klastra** przycisk w arkuszu.</span><span class="sxs-lookup"><span data-stu-id="e0c07-237">To run the workbook on the cluster in Azure, click the **Cluster** button on the worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="e0c07-238">Uruchom funkcje UDF programu Excel</span><span class="sxs-lookup"><span data-stu-id="e0c07-238">Run Excel UDFs</span></span>
<span data-ttu-id="e0c07-239">Aby uruchomić plikami UDF programu Excel, wykonaj poprzednie kroki 1 – 3, aby skonfigurować komputer kliencki.</span><span class="sxs-lookup"><span data-stu-id="e0c07-239">To run Excel UDFs, follow the preceding steps 1 – 3 to set up the client computer.</span></span> <span data-ttu-id="e0c07-240">Dla funkcji UDF programu Excel nie trzeba zainstalowaną na węzłach obliczeniowych aplikacją programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-240">For Excel UDFs, you don't need to have the Excel application installed on compute nodes.</span></span> <span data-ttu-id="e0c07-241">Tak gdy węzły obliczeniowe tworzenia klastra, można wybrać zwykłym obliczeniowe obrazu węzła zamiast obrazu węzła obliczeń przy użyciu programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of the compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="e0c07-242">Istnieje limit 34 znaków w programie Excel 2010 i 2013 — okno dialogowe łącznik klastra.</span><span class="sxs-lookup"><span data-stu-id="e0c07-242">There is a 34 character limit in the Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="e0c07-243">To okno dialogowe służy do określania klastra funkcji UDF.</span><span class="sxs-lookup"><span data-stu-id="e0c07-243">You use this dialog box to specify the cluster that runs the UDFs.</span></span> <span data-ttu-id="e0c07-244">Jeśli klaster Pełna nazwa jest dłuższa (na przykład hpcexcelhn01.southeastasia.cloudapp.azure.com), nie mieści się w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="e0c07-244">If the full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in the dialog box.</span></span> <span data-ttu-id="e0c07-245">Należy ustawić zmiennej dla komputera, takich jak *CCP_IAASHN* z wartością nazwy klastra długo.</span><span class="sxs-lookup"><span data-stu-id="e0c07-245">The workaround is to set a machine-wide variable such as *CCP_IAASHN* with the value of the long cluster name.</span></span> <span data-ttu-id="e0c07-246">Następnie wprowadź *CCP_IAASHN %* w oknie dialogowym nazwy węzła głównego klastra.</span><span class="sxs-lookup"><span data-stu-id="e0c07-246">Then, enter *%CCP_IAASHN%* in the dialog box as the cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="e0c07-247">Po pomyślnym wdrożeniu klastra, kontynuuj następujące kroki, aby uruchomić przykładowe wbudowanych UDF programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-247">After the cluster is successfully deployed, continue with the following steps to run a sample built-in Excel UDF.</span></span> <span data-ttu-id="e0c07-248">Dostosowane plikami UDF programu Excel, zobacz te [zasobów](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) tworzenie XLL i wdrożyć je w klastrze IaaS.</span><span class="sxs-lookup"><span data-stu-id="e0c07-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) to build the XLLs and deploy them on the IaaS cluster.</span></span>

1. <span data-ttu-id="e0c07-249">Otwórz nowy skoroszyt programu Excel.</span><span class="sxs-lookup"><span data-stu-id="e0c07-249">Open a new Excel workbook.</span></span> <span data-ttu-id="e0c07-250">Na **opracowanie** wstążki, kliknij przycisk **Add-Ins**.</span><span class="sxs-lookup"><span data-stu-id="e0c07-250">On the **Develop** ribbon, click **Add-Ins**.</span></span> <span data-ttu-id="e0c07-251">Następnie w oknie dialogowym kliknij **Przeglądaj**, przejdź do folderu %CCP_HOME%Bin\XLL32 i wybierz przykład ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="e0c07-251">Then, in the dialog box, click **Browse**, navigate to the %CCP_HOME%Bin\XLL32 folder, and select the sample ClusterUDF32.xll.</span></span> <span data-ttu-id="e0c07-252">Jeśli ClusterUDF32 nie istnieje na komputerze klienckim, skopiuj go w folderze %CCP_HOME%Bin\XLL32 na węzła głównego.</span><span class="sxs-lookup"><span data-stu-id="e0c07-252">If the ClusterUDF32 doesn't exist on the client machine, copy it from the %CCP_HOME%Bin\XLL32 folder on the head node.</span></span>
   
   ![Wybierz funkcję zdefiniowaną przez użytkownika][udf]
2. <span data-ttu-id="e0c07-254">Kliknij przycisk **pliku** > **opcje** > **zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="e0c07-254">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="e0c07-255">W obszarze **formuły**, sprawdź **Zezwalaj na uruchamianie klastra obliczeniowego funkcji XLL użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="e0c07-255">Under **Formulas**, check **Allow user-defined XLL functions to run a compute cluster**.</span></span> <span data-ttu-id="e0c07-256">Następnie kliknij przycisk **opcje** , a następnie wprowadź nazwę klastra pełna w **nazwy węzła głównego klastra**.</span><span class="sxs-lookup"><span data-stu-id="e0c07-256">Then click **Options** and enter the full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="e0c07-257">(Jak zanotowane wcześniej to pole wejściowe jest ograniczona do 34 znaków, tak długo nazwa_klastra może nie mieści się.</span><span class="sxs-lookup"><span data-stu-id="e0c07-257">(As noted previously this input box is limited to 34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="e0c07-258">Można użyć zmiennej dla komputera, w tym miejscu dla nazwy klastra długie.)</span><span class="sxs-lookup"><span data-stu-id="e0c07-258">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Skonfiguruj funkcję zdefiniowaną przez użytkownika][options]
3. <span data-ttu-id="e0c07-260">Aby uruchomić obliczania funkcji zdefiniowanej przez użytkownika w klastrze, kliknij komórkę z =XllGetComputerNameC() wartości, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="e0c07-260">To run the UDF calculation on the cluster, click the cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="e0c07-261">Funkcja po prostu pobiera nazwę węzła obliczeń, na którym jest uruchomiony funkcję zdefiniowaną przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e0c07-261">The function simply retrieves the name of the compute node on which the UDF runs.</span></span> <span data-ttu-id="e0c07-262">Dla pierwszego uruchomienia okno dialogowe poświadczeń monituje o podanie nazwy użytkownika i hasła do nawiązania połączenia klastra IaaS.</span><span class="sxs-lookup"><span data-stu-id="e0c07-262">For the first run, a credentials dialog box prompts for the username and password to connect to the IaaS cluster.</span></span>
   
   ![Uruchamianie funkcji zdefiniowanej przez użytkownika][run]
   
   <span data-ttu-id="e0c07-264">W przypadku wielu komórek do obliczenia, naciśnij klawisz Ctrl-Alt-Shift + F9, aby uruchomić obliczenia na wszystkie komórki.</span><span class="sxs-lookup"><span data-stu-id="e0c07-264">When there are many cells to calculate, press Alt-Shift-Ctrl + F9 to run the calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="e0c07-265">Krok 3.</span><span class="sxs-lookup"><span data-stu-id="e0c07-265">Step 3.</span></span> <span data-ttu-id="e0c07-266">Uruchom obciążenia SOA z klienta lokalnego</span><span class="sxs-lookup"><span data-stu-id="e0c07-266">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="e0c07-267">Aby uruchomić ogólne SOA aplikacji w klastrze HPC Pack IaaS, należy najpierw użyć jednej z metod w kroku 1 do wdrożenia klastra.</span><span class="sxs-lookup"><span data-stu-id="e0c07-267">To run general SOA applications on the HPC Pack IaaS cluster, first use one of the methods in Step 1 to deploy the cluster.</span></span> <span data-ttu-id="e0c07-268">Określ ogólnego obliczeniowe obrazu węzła w tym przypadku, ponieważ nie ma potrzeby programu Excel w węzłach obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="e0c07-268">Specify a generic compute node image in this case, because you do not need Excel on the compute nodes.</span></span> <span data-ttu-id="e0c07-269">Następnie wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="e0c07-269">Then follow these steps.</span></span>

1. <span data-ttu-id="e0c07-270">Po pobraniu certyfikatu klastra, należy zaimportować go na komputerze klienckim w obszarze Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="e0c07-270">After retrieving the cluster certificate, import it on the client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="e0c07-271">Zainstaluj [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) i [narzędzi klienta HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="e0c07-271">Install the [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="e0c07-272">Te narzędzia umożliwiają tworzenie i uruchamianie aplikacji klienckich SOA.</span><span class="sxs-lookup"><span data-stu-id="e0c07-272">These tools enable you to develop and run SOA client applications.</span></span>
3. <span data-ttu-id="e0c07-273">Pobierz HelloWorldR2 [przykładowy kod](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="e0c07-273">Download the HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="e0c07-274">Otwórz HelloWorldR2.sln w Visual Studio 2010 lub 2012.</span><span class="sxs-lookup"><span data-stu-id="e0c07-274">Open the HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="e0c07-275">(Ten przykład nie jest obecnie zgodny z nowszej wersji programu Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="e0c07-275">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="e0c07-276">Tworzenie pierwszej kompilacji projektu EchoService.</span><span class="sxs-lookup"><span data-stu-id="e0c07-276">Build the EchoService project first.</span></span> <span data-ttu-id="e0c07-277">Następnie Wdróż usługę klastra IaaS w taki sam sposób wdrożyć w klastrze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="e0c07-277">Then, deploy the service to the IaaS cluster in the same way you deploy to an on-premises cluster.</span></span> <span data-ttu-id="e0c07-278">Aby uzyskać szczegółowe instrukcje Zobacz Readme.doc w HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="e0c07-278">For detailed steps, see the Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="e0c07-279">Modyfikowanie i tworzenie HellWorldR2 i inne projekty, zgodnie z opisem w poniższej sekcji, można wygenerować aplikacje klienckie SOA uruchamianych w klastrze IaaS platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e0c07-279">Modify and build the HellWorldR2 and other projects as described in the following section to generate the SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="e0c07-280">Używaj wiązania Http z kolejką usługi Azure storage</span><span class="sxs-lookup"><span data-stu-id="e0c07-280">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="e0c07-281">Umożliwia powiązanie Http z kolejką usługi Azure storage, należy wprowadzić kilka zmian w przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="e0c07-281">To use Http binding with an Azure storage queue, make a few changes to the sample code.</span></span>

* <span data-ttu-id="e0c07-282">Aktualizacja nazwy klastra.</span><span class="sxs-lookup"><span data-stu-id="e0c07-282">Update the cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="e0c07-283">Opcjonalnie użyj domyślnej TransportScheme w SessionStartInfo lub jawnie ustaw HTTP.</span><span class="sxs-lookup"><span data-stu-id="e0c07-283">Optionally, use the default TransportScheme in SessionStartInfo or explicitly set it to Http.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="e0c07-284">Użyj domyślnego powiązania dla BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="e0c07-284">Use default binding for the BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="e0c07-285">Ani nie ustawiaj jawnie użycie klasy basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="e0c07-285">Or set explicitly using the basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="e0c07-286">Opcjonalnie można ustawić flagi UseAzureQueue na wartość true w SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="e0c07-286">Optionally, set the UseAzureQueue flag to true in SessionStartInfo.</span></span> <span data-ttu-id="e0c07-287">Jeśli nie jest ustawiona, zostanie ustawiona wartość true, domyślnie, gdy nazwa klastra ma sufiksy domen platformy Azure i TransportScheme Http.</span><span class="sxs-lookup"><span data-stu-id="e0c07-287">If not set, it will be set to true by default when the cluster name has Azure domain suffixes and the TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="e0c07-288">Używaj wiązania Http bez kolejki magazynu Azure</span><span class="sxs-lookup"><span data-stu-id="e0c07-288">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="e0c07-289">Aby jawnie używaj wiązania Http bez kolejki magazynu Azure, należy ustawić flagę UseAzureQueue false w SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="e0c07-289">To use Http binding without an Azure storage queue, explicitly set the UseAzureQueue flag to false in the SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="e0c07-290">Użyj NetTcp powiązania</span><span class="sxs-lookup"><span data-stu-id="e0c07-290">Use NetTcp binding</span></span>
<span data-ttu-id="e0c07-291">Aby użyć NetTcp powiązania, konfiguracja jest podobny do nawiązywania połączenia z lokalnego klastra.</span><span class="sxs-lookup"><span data-stu-id="e0c07-291">To use NetTcp binding, the configuration is similar to connecting to an on-premises cluster.</span></span> <span data-ttu-id="e0c07-292">Należy otworzyć kilka punktów końcowych w węźle głównym maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e0c07-292">You need to open a few endpoints on the head node VM.</span></span> <span data-ttu-id="e0c07-293">Jeśli skrypt wdrożenia HPC Pack IaaS jest używany do tworzenia klastra, na przykład ustawić punkty końcowe w portalu Azure w następujący sposób.</span><span class="sxs-lookup"><span data-stu-id="e0c07-293">If you used the HPC Pack IaaS deployment script to create the cluster, for example, set the endpoints in the Azure portal as follows.</span></span>

1. <span data-ttu-id="e0c07-294">Zatrzymaj maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e0c07-294">Stop the VM.</span></span>
2. <span data-ttu-id="e0c07-295">Dodaj porty TCP 9090, 9087, 9091, Broker 9094 w sesji, odpowiednio Broker pracownik i usługi danych</span><span class="sxs-lookup"><span data-stu-id="e0c07-295">Add the TCP ports 9090, 9087, 9091, 9094 for the Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Konfigurowanie punktów końcowych][endpoint-new-portal]
3. <span data-ttu-id="e0c07-297">Uruchom maszynę Wirtualną.</span><span class="sxs-lookup"><span data-stu-id="e0c07-297">Start the VM.</span></span>

<span data-ttu-id="e0c07-298">Aplikacja kliencka SOA nie wymagają żadnych zmian, z wyjątkiem zmiana nazwy head pełnej nazwy klastra IaaS.</span><span class="sxs-lookup"><span data-stu-id="e0c07-298">The SOA client application requires no changes except altering the head name to the IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0c07-299">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e0c07-299">Next steps</span></span>
* <span data-ttu-id="e0c07-300">Zobacz [tych zasobów](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) uzyskać więcej informacji dotyczących uruchamiania obciążeń programu Excel z HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="e0c07-300">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="e0c07-301">Zobacz [Zarządzanie SOA usług Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) szczegółowe informacje na temat wdrażania i zarządzania usługami SOA pakietem HPC.</span><span class="sxs-lookup"><span data-stu-id="e0c07-301">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

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
