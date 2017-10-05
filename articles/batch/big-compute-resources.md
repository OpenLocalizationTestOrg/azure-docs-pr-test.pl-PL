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
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a>Duże obliczeniowe na platformie Azure: zasoby techniczne dla partii i przetwarzanie o wysokiej wydajności
Jest to przewodnik dotyczący zasobów technicznych uruchomienie programu równolegle na dużą skalę, partii i wysokiej wydajności (HPC) obciążeń na platformie Azure. Rozszerzenie pliku wsadowym istniejących lub HPC obciążeń w chmurze platformy Azure lub tworzenia nowych rozwiązań Big obliczeniowe przy użyciu usług zakresu Azure.

## <a name="solutions-options"></a>Opcje rozwiązania
Więcej informacji na temat opcji obliczeniowe duży na platformie Azure, a następnie wybierz odpowiednie podejście dla potrzeb obciążenia i biznesowych.

* [Rozwiązania partii i HPC](batch-hpc-solutions.md)
* [Wideo: Big obliczeniowych w chmurze za pomocą platformy Azure i HPC](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a>Azure Batch
[Wsadowe](https://azure.microsoft.com/services/batch/) jest usługą platformy, która ułatwia chmury Włącz obsługę systemu Linux i Windows aplikacji i uruchom zadania bez konfigurowania i zarządzania harmonogramu klastra i zadania. Integracja aplikacji klienta z partii zadań Azure za pomocą różnych języków, etap danych na platformie Azure, przy użyciu zestawu SDK, a tworzenie potoków wykonywania zadania.

* [Dokumentacja](https://azure.microsoft.com/documentation/services/batch/)
* [.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), i [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) dokumentacja interfejsu API
* [Biblioteka .NET zarządzania partii](https://msdn.microsoft.com/library/mt463120.aspx) odwołania
* Samouczki: Rozpoczynanie pracy z [biblioteki partii zadań Azure dla platformy .NET](batch-dotnet-get-started.md) i [Python partii klienta](batch-python-tutorial.md)
* [Forum usługi partia zadań](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [Filmy wideo partii](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a>Czy rozwiązania klastrów HPC
Wdrażanie dysku lub Rozszerz istniejącego klastra systemu Windows lub Linux HPC na platformie Azure, aby uruchomić intensywnych obciążeń obliczeniowych.  

### <a name="microsoft-hpc-pack"></a>Microsoft HPC Pack
HPC Pack jest bezpłatna rozwiązania HPC firmy Microsoft, oparty na technologii Microsoft Azure i Windows Server, umożliwiający uruchomienie systemu Windows i Linux HPC obciążeń.  

* [Pobierz pakiet HPC 2016](https://www.microsoft.com/download/details.aspx?id=54507)
* [Pobierz HPC Pack 2012 R2 z aktualizacją 3](https://www.microsoft.com/download/details.aspx?id=49922)
* [Dokumentacja](https://technet.microsoft.com/library/jj899572.aspx)
* Opcje klastra HPC Pack na platformie Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) i [systemu Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 
* [Serii do wystąpień procesu roboczego platformy Azure z pakietem HPC](https://technet.microsoft.com/library/gg481749.aspx)
* [Serii do partii zadań Azure z pakietem HPC](https://technet.microsoft.com/library/mt612877.aspx)
* [Forum systemu Windows HPC](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a>Rozwiązania klastra z systemem Linux i systemów operacyjnych
Wdrażanie klastrów HPC systemu Linux za pomocą tych szablonów platformy Azure.

* [Aż klastra SLURM](https://azure.microsoft.com/documentation/templates/slurm/) i [wpis w blogu](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)
* [Aż do momentu klastra](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [Obliczenia bazy danych siatki szablony z PBS Professional](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a>Magazyn HPC
* [Systemy plików równoległych HPC magazynu na platformie Azure](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [Intel chmury wersji oprogramowania połysk - Eval](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [BeeGFS w szablonie CentOS 7.2](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a>MPI firmy Microsoft
[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) to implementacja firmy Microsoft standardowy interfejs przekazywanie komunikatów umożliwiające tworzenie i uruchamianie aplikacji równoległych na platformie Windows.

* [Pobierz MS MPI](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [Odwołanie MS MPI](https://msdn.microsoft.com/library/dn473458.aspx)
* [MPI forum](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a>Wystąpienia intensywnie korzystające z mocy obliczeniowej
Azure oferuje [rozmiarów zakresu maszyn wirtualnych](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), takie jak [obliczeniowych H-series](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) wystąpień może nawiązywać połączenia z siecią wewnętrzną RDMA do uruchamiania obciążeń systemu Linux i Windows HPC. 

* [Konfigurowanie klastra Linux RDMA na uruchamianie aplikacji MPI](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Konfigurowanie klastra RDMA systemu Windows z pakietem Microsoft HPC do uruchamiania aplikacji MPI](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

W przypadku obciążeń intensywnie z procesora GPU, zapoznaj się z [rozmiary NC i wirtualizacją sieci](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).

## <a name="samples-and-demos"></a>Przykłady i pokazy
* [Przykłady kodu platformy Azure partii C# i języka Python](https://github.com/Azure/azure-batch-samples)
* [Partii stoczni](https://azure.github.io/batch-shipyard/) zestawu narzędzi w celu łatwiejszego wdrażania obciążeń Dockerized stylu partii do partii zadań Azure
* [doAzureParallel](http://www.github.com/Azure/doAzureParallel) pakietu języka R, rozszerzający partii zadań Azure
* [Przetestuj SUSE Linux Enterprise Server dla HPC](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a>Pokrewne usługi platformy Azure
* [Fabryka danych](https://azure.microsoft.com/documentation/services/data-factory/)
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/)
* [Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Zestawy skalowania maszyny wirtualnej](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [Cloud Services](https://azure.microsoft.com/documentation/services/cloud-services/)
* [App Service](https://azure.microsoft.com/documentation/services/app-service/)
* [Media Services](https://azure.microsoft.com/documentation/services/media-services/)
* [Funkcje](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a>Schematy architektury
* [Orchestration HPC i danych przy użyciu partii zadań Azure i fabryki danych Azure](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) oraz [artykułu](../data-factory/data-factory-data-processing-using-batch.md)

## <a name="industry-solutions"></a>Rozwiązania z branży
* [Bankowości i inwestycyjne rynkach](https://finance.azure.com/)
* [Symulacje zespołu inżynieryjnego](https://simulation.azure.com/) 

## <a name="customer-stories"></a>Historie klientów
* [ANEO](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [d3View](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [Instytut Ludwig raka badań](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [Microsoft Research](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [Milliman](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [Mitsubishi UFJ zabezpieczeń międzynarodowych](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [Schlumberger](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Wieże Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [UberCloud](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a>Następne kroki
* Najnowsze informacje można znaleźć na [blogu zespołu Microsoft HPC i usługi Batch](http://blogs.technet.com/b/windowshpc/) oraz [blogu platformy Azure](https://azure.microsoft.com/blog/tag/hpc/).
* Zobacz też [nowości w partii](https://azure.microsoft.com/updates/?service=batch) lub subskrybować [kanału informacyjnego RSS](https://azure.microsoft.com/updates/feed/?service=batch).

