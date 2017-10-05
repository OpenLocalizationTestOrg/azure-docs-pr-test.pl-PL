---
title: Zasoby dla partii i HPC w chmurze Azure | Dokumentacja firmy Microsoft
description: "Zawiera listę zasobów technicznych uruchomienie programu równolegle na dużą skalę, partii i wysokiej wydajności obliczeniowej (HPC) obciążeń na platformie Azure."
services: batch, cloud-services, virtual-machines
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: 18be9f503b57117a7e8f5f0a4e9c93614cc7755b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="719eb-103">Duże obliczeniowe na platformie Azure: zasoby techniczne dla partii i przetwarzanie o wysokiej wydajności</span><span class="sxs-lookup"><span data-stu-id="719eb-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="719eb-104">Jest to przewodnik dotyczący zasobów technicznych uruchomienie programu równolegle na dużą skalę, partii i wysokiej wydajności (HPC) obciążeń na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="719eb-104">This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="719eb-105">Rozszerzenie pliku wsadowym istniejących lub HPC obciążeń w chmurze platformy Azure lub tworzenia nowych rozwiązań Big obliczeniowe przy użyciu usług zakresu Azure.</span><span class="sxs-lookup"><span data-stu-id="719eb-105">Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="719eb-106">Opcje rozwiązania</span><span class="sxs-lookup"><span data-stu-id="719eb-106">Solutions options</span></span>
<span data-ttu-id="719eb-107">Więcej informacji na temat opcji obliczeniowe duży na platformie Azure, a następnie wybierz odpowiednie podejście dla potrzeb obciążenia i biznesowych.</span><span class="sxs-lookup"><span data-stu-id="719eb-107">Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.</span></span>

* [<span data-ttu-id="719eb-108">Rozwiązania partii i HPC</span><span class="sxs-lookup"><span data-stu-id="719eb-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="719eb-109">Wideo: Big obliczeniowych w chmurze za pomocą platformy Azure i HPC</span><span class="sxs-lookup"><span data-stu-id="719eb-109">Video: Big Compute in the cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="719eb-110">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="719eb-110">Azure Batch</span></span>
<span data-ttu-id="719eb-111">[Wsadowe](https://azure.microsoft.com/services/batch/) jest usługą platformy, która ułatwia chmury Włącz obsługę systemu Linux i Windows aplikacji i uruchom zadania bez konfigurowania i zarządzania harmonogramu klastra i zadania.</span><span class="sxs-lookup"><span data-stu-id="719eb-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="719eb-112">Integracja aplikacji klienta z partii zadań Azure za pomocą różnych języków, etap danych na platformie Azure, przy użyciu zestawu SDK, a tworzenie potoków wykonywania zadania.</span><span class="sxs-lookup"><span data-stu-id="719eb-112">Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="719eb-113">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="719eb-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="719eb-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), i [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) dokumentacja interfejsu API</span><span class="sxs-lookup"><span data-stu-id="719eb-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="719eb-115">[Biblioteka .NET zarządzania partii](https://msdn.microsoft.com/library/mt463120.aspx) odwołania</span><span class="sxs-lookup"><span data-stu-id="719eb-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="719eb-116">Samouczki: Rozpoczynanie pracy z [biblioteki partii zadań Azure dla platformy .NET](batch-dotnet-get-started.md) i [Python partii klienta](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="719eb-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="719eb-117">Forum usługi partia zadań</span><span class="sxs-lookup"><span data-stu-id="719eb-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="719eb-118">Filmy wideo partii</span><span class="sxs-lookup"><span data-stu-id="719eb-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="719eb-119">Czy rozwiązania klastrów HPC</span><span class="sxs-lookup"><span data-stu-id="719eb-119">HPC cluster solutions</span></span>
<span data-ttu-id="719eb-120">Wdrażanie dysku lub Rozszerz istniejącego klastra systemu Windows lub Linux HPC na platformie Azure, aby uruchomić intensywnych obciążeń obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="719eb-120">Deploy or extend your existing Windows or Linux HPC cluster to Azure to run your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="719eb-121">Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="719eb-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="719eb-122">HPC Pack jest bezpłatna rozwiązania HPC firmy Microsoft, oparty na technologii Microsoft Azure i Windows Server, umożliwiający uruchomienie systemu Windows i Linux HPC obciążeń.</span><span class="sxs-lookup"><span data-stu-id="719eb-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="719eb-123">Pobierz pakiet HPC 2016</span><span class="sxs-lookup"><span data-stu-id="719eb-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="719eb-124">Pobierz HPC Pack 2012 R2 z aktualizacją 3</span><span class="sxs-lookup"><span data-stu-id="719eb-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="719eb-125">Dokumentacja</span><span class="sxs-lookup"><span data-stu-id="719eb-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="719eb-126">Opcje klastra HPC Pack na platformie Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) i [systemu Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="719eb-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="719eb-127">Serii do wystąpień procesu roboczego platformy Azure z pakietem HPC</span><span class="sxs-lookup"><span data-stu-id="719eb-127">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="719eb-128">Serii do partii zadań Azure z pakietem HPC</span><span class="sxs-lookup"><span data-stu-id="719eb-128">Burst to Azure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="719eb-129">Forum systemu Windows HPC</span><span class="sxs-lookup"><span data-stu-id="719eb-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="719eb-130">Rozwiązania klastra z systemem Linux i systemów operacyjnych</span><span class="sxs-lookup"><span data-stu-id="719eb-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="719eb-131">Wdrażanie klastrów HPC systemu Linux za pomocą tych szablonów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="719eb-131">Use these Azure templates to deploy Linux HPC clusters.</span></span>

* <span data-ttu-id="719eb-132">[Aż klastra SLURM](https://azure.microsoft.com/documentation/templates/slurm/) i [wpis w blogu](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="719eb-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="719eb-133">Aż do momentu klastra</span><span class="sxs-lookup"><span data-stu-id="719eb-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="719eb-134">Obliczenia bazy danych siatki szablony z PBS Professional</span><span class="sxs-lookup"><span data-stu-id="719eb-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="719eb-135">Magazyn HPC</span><span class="sxs-lookup"><span data-stu-id="719eb-135">HPC storage</span></span>
* [<span data-ttu-id="719eb-136">Systemy plików równoległych HPC magazynu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="719eb-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="719eb-137">Intel chmury wersji oprogramowania połysk - Eval</span><span class="sxs-lookup"><span data-stu-id="719eb-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="719eb-138">BeeGFS w szablonie CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="719eb-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="719eb-139">MPI firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="719eb-139">Microsoft MPI</span></span>
<span data-ttu-id="719eb-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) to implementacja firmy Microsoft standardowy interfejs przekazywanie komunikatów umożliwiające tworzenie i uruchamianie aplikacji równoległych na platformie Windows.</span><span class="sxs-lookup"><span data-stu-id="719eb-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.</span></span>

* [<span data-ttu-id="719eb-141">Pobierz MS MPI</span><span class="sxs-lookup"><span data-stu-id="719eb-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="719eb-142">Odwołanie MS MPI</span><span class="sxs-lookup"><span data-stu-id="719eb-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="719eb-143">MPI forum</span><span class="sxs-lookup"><span data-stu-id="719eb-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="719eb-144">Wystąpienia intensywnie korzystające z mocy obliczeniowej</span><span class="sxs-lookup"><span data-stu-id="719eb-144">Compute-intensive instances</span></span>
<span data-ttu-id="719eb-145">Azure oferuje [rozmiarów zakresu maszyn wirtualnych](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), takie jak [obliczeniowych H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) wystąpień może nawiązywać połączenia z siecią wewnętrzną RDMA do uruchamiania obciążeń systemu Linux i Windows HPC.</span><span class="sxs-lookup"><span data-stu-id="719eb-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting to a back-end RDMA network, to run your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="719eb-146">Konfigurowanie klastra Linux RDMA na uruchamianie aplikacji MPI</span><span class="sxs-lookup"><span data-stu-id="719eb-146">Set up a Linux RDMA cluster to run MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="719eb-147">Konfigurowanie klastra RDMA systemu Windows z pakietem Microsoft HPC do uruchamiania aplikacji MPI</span><span class="sxs-lookup"><span data-stu-id="719eb-147">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="719eb-148">W przypadku obciążeń intensywnie z procesora GPU, zapoznaj się z [rozmiary NC i wirtualizacją sieci](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span><span class="sxs-lookup"><span data-stu-id="719eb-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="719eb-149">Przykłady i pokazy</span><span class="sxs-lookup"><span data-stu-id="719eb-149">Samples and demos</span></span>
* [<span data-ttu-id="719eb-150">Przykłady kodu platformy Azure partii C# i języka Python</span><span class="sxs-lookup"><span data-stu-id="719eb-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="719eb-151">[Partii stoczni](https://azure.github.io/batch-shipyard/) zestawu narzędzi w celu łatwiejszego wdrażania obciążeń Dockerized stylu partii do partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="719eb-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch</span></span>
* <span data-ttu-id="719eb-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) pakietu języka R, rozszerzający partii zadań Azure</span><span class="sxs-lookup"><span data-stu-id="719eb-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="719eb-153">Przetestuj SUSE Linux Enterprise Server dla HPC</span><span class="sxs-lookup"><span data-stu-id="719eb-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="719eb-154">Pokrewne usługi platformy Azure</span><span class="sxs-lookup"><span data-stu-id="719eb-154">Related Azure services</span></span>
* [<span data-ttu-id="719eb-155">Fabryka danych</span><span class="sxs-lookup"><span data-stu-id="719eb-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="719eb-156">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="719eb-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="719eb-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="719eb-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="719eb-158">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="719eb-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="719eb-159">Zestawy skalowania maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="719eb-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="719eb-160">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="719eb-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="719eb-161">App Service</span><span class="sxs-lookup"><span data-stu-id="719eb-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="719eb-162">Media Services</span><span class="sxs-lookup"><span data-stu-id="719eb-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="719eb-163">Funkcje</span><span class="sxs-lookup"><span data-stu-id="719eb-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="719eb-164">Schematy architektury</span><span class="sxs-lookup"><span data-stu-id="719eb-164">Architecture blueprints</span></span>
* <span data-ttu-id="719eb-165">[Orchestration HPC i danych przy użyciu partii zadań Azure i fabryki danych Azure](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) oraz [artykułu](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="719eb-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="719eb-166">Rozwiązania z branży</span><span class="sxs-lookup"><span data-stu-id="719eb-166">Industry solutions</span></span>
* [<span data-ttu-id="719eb-167">Bankowości i inwestycyjne rynkach</span><span class="sxs-lookup"><span data-stu-id="719eb-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="719eb-168">Symulacje zespołu inżynieryjnego</span><span class="sxs-lookup"><span data-stu-id="719eb-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="719eb-169">Historie klientów</span><span class="sxs-lookup"><span data-stu-id="719eb-169">Customer stories</span></span>
* [<span data-ttu-id="719eb-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="719eb-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="719eb-171">d3View</span><span class="sxs-lookup"><span data-stu-id="719eb-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="719eb-172">Instytut Ludwig raka badań</span><span class="sxs-lookup"><span data-stu-id="719eb-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="719eb-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="719eb-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="719eb-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="719eb-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="719eb-175">Mitsubishi UFJ zabezpieczeń międzynarodowych</span><span class="sxs-lookup"><span data-stu-id="719eb-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="719eb-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="719eb-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="719eb-177">Wieże Watson</span><span class="sxs-lookup"><span data-stu-id="719eb-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="719eb-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="719eb-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="719eb-179">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="719eb-179">Next steps</span></span>
* <span data-ttu-id="719eb-180">Najnowsze informacje można znaleźć na [blogu zespołu Microsoft HPC i usługi Batch](http://blogs.technet.com/b/windowshpc/) oraz [blogu platformy Azure](https://azure.microsoft.com/blog/tag/hpc/).</span><span class="sxs-lookup"><span data-stu-id="719eb-180">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="719eb-181">Zobacz też [nowości w partii](https://azure.microsoft.com/updates/?service=batch) lub subskrybować [kanału informacyjnego RSS](https://azure.microsoft.com/updates/feed/?service=batch).</span><span class="sxs-lookup"><span data-stu-id="719eb-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

