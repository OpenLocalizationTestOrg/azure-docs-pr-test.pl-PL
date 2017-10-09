---
title: "Brama zarządzania dla fabryki danych aaaData | Dokumentacja firmy Microsoft"
description: "Konfigurowanie danych toomove bramy danych między lokalnymi i hello chmury. Użyj bramy zarządzania danymi w fabryce danych Azure toomove danych."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="0daec-104">Brama zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="0daec-104">Data Management Gateway</span></span>
<span data-ttu-id="0daec-105">Brama zarządzania danymi Hello jest agent klienta, które muszą być zainstalowane w danych lokalnych środowiska toocopy między chmury i lokalnych magazynów danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-105">hello Data management gateway is a client agent that you must install in your on-premises environment toocopy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="0daec-106">Witaj danych lokalnych magazynów danych fabryka obsługuje są wymienione w hello [obsługiwanych źródeł danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats) sekcji.</span><span class="sxs-lookup"><span data-stu-id="0daec-106">hello on-premises data stores supported by Data Factory are listed in hello [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="0daec-107">W tym artykule uzupełnia wskazówki hello w hello [przenoszenie danych między lokalnymi i w chmurze magazyny danych](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0daec-107">This article complements hello walkthrough in hello [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="0daec-108">W przewodniku hello utworzysz potok, który korzysta z danych toomove bramy hello z tooan bazy danych programu SQL Server na lokalnych obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0daec-108">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span> <span data-ttu-id="0daec-109">Ten artykuł zawiera szczegółowe informacje szczegółowe na temat bramy zarządzania danymi hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-109">This article provides detailed in-depth information about hello data management gateway.</span></span> 

<span data-ttu-id="0daec-110">Możesz skalować w poziomie bramy zarządzania danymi hello bramy można skojarzyć wielu komputerach lokalnych.</span><span class="sxs-lookup"><span data-stu-id="0daec-110">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="0daec-111">Możesz skalować w górę zwiększając liczbę zadań przepływu danych, które można uruchomić jednocześnie w węźle.</span><span class="sxs-lookup"><span data-stu-id="0daec-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="0daec-112">Ta funkcja jest również dostępny do logicznego bramy z jednego węzła.</span><span class="sxs-lookup"><span data-stu-id="0daec-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="0daec-113">Zobacz [skalowanie brama zarządzania danymi w fabryce danych Azure](data-factory-data-management-gateway-high-availability-scalability.md) artykułu, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0daec-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="0daec-114">Obecnie brama obsługuje tylko działania kopiowania hello i działania procedury składowanej w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-114">Currently, gateway supports only hello copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="0daec-115">Nie jest możliwe toouse hello bramy z działań niestandardowych tooaccess lokalnych źródeł danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-115">It is not possible toouse hello gateway from a custom activity tooaccess on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="0daec-116">Omówienie</span><span class="sxs-lookup"><span data-stu-id="0daec-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="0daec-117">Funkcje bramy zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="0daec-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="0daec-118">Brama zarządzania danymi zapewnia hello następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="0daec-118">Data management gateway provides hello following capabilities:</span></span>

* <span data-ttu-id="0daec-119">Model lokalnych źródeł danych i źródeł danych w chmurze w hello tej samej fabryki danych i przenoszenia danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-119">Model on-premises data sources and cloud data sources within hello same data factory and move data.</span></span>
* <span data-ttu-id="0daec-120">Ma jednego okienka szkła monitorowania i zarządzania wgląd w stan bramy z hello strony fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-120">Have a single pane of glass for monitoring and management with visibility into gateway status from hello Data Factory page.</span></span>
* <span data-ttu-id="0daec-121">Zarządzanie bezpieczny dostęp do lokalnych tooon źródła danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-121">Manage access tooon-premises data sources securely.</span></span>
  * <span data-ttu-id="0daec-122">Zapora toocorporate konieczne żadne zmiany.</span><span class="sxs-lookup"><span data-stu-id="0daec-122">No changes required toocorporate firewall.</span></span> <span data-ttu-id="0daec-123">Brama podejmuje tylko połączeń wychodzących oparte na protokole HTTP tooopen internet.</span><span class="sxs-lookup"><span data-stu-id="0daec-123">Gateway only makes outbound HTTP-based connections tooopen internet.</span></span>
  * <span data-ttu-id="0daec-124">Szyfrowania poświadczeń dostępu do sieci lokalnych magazynów danych przy użyciu certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="0daec-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="0daec-125">Przenoszenie danych wydajnie — dane są przesyłane w równoległe, odpornych toointermittent problemy z siecią z logiki ponawiania próby automatycznego.</span><span class="sxs-lookup"><span data-stu-id="0daec-125">Move data efficiently – data is transferred in parallel, resilient toointermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="0daec-126">Polecenie przepływu i przepływu danych</span><span class="sxs-lookup"><span data-stu-id="0daec-126">Command flow and data flow</span></span>
<span data-ttu-id="0daec-127">Użycie danych toocopy działania kopiowania między lokalnymi i w chmurze, hello działanie używa danych tootransfer bramy z toocloud źródła danych lokalnie i na odwrót.</span><span class="sxs-lookup"><span data-stu-id="0daec-127">When you use a copy activity toocopy data between on-premises and cloud, hello activity uses a gateway tootransfer data from on-premises data source toocloud and vice versa.</span></span>

<span data-ttu-id="0daec-128">Poniżej przedstawiono przepływ danych wysokiego poziomu hello i podsumowanie kroków kopii danych bramy: ![przepływ danych przy użyciu bramy](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="0daec-128">Here is hello high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="0daec-129">Projektant danych tworzy bramy dla fabryki danych Azure przy użyciu albo hello [portalu Azure](https://portal.azure.com) lub [polecenia Cmdlet programu PowerShell](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="0daec-129">Data developer creates a gateway for an Azure Data Factory using either hello [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="0daec-130">Projektant danych tworzy połączonej usługi magazynu danych lokalnych za pośrednictwem bramy hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-130">Data developer creates a linked service for an on-premises data store by specifying hello gateway.</span></span> <span data-ttu-id="0daec-131">Jako część konfigurowania hello połączonej usługi, danych deweloperów używa typy uwierzytelniania toospecify hello poświadczenia ustawienia aplikacji i poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="0daec-131">As part of setting up hello linked service, data developer uses hello Setting Credentials application toospecify authentication types and credentials.</span></span>  <span data-ttu-id="0daec-132">Witaj ustawienie poświadczeń, których aplikacji w oknie dialogowym komunikuje się z danymi hello przechowywać tootest połączenia i hello toosave poświadczeń bramy.</span><span class="sxs-lookup"><span data-stu-id="0daec-132">hello Setting Credentials application dialog communicates with hello data store tootest connection and hello gateway toosave credentials.</span></span>
3. <span data-ttu-id="0daec-133">Brama szyfruje poświadczenia hello z certyfikatem hello skojarzone z bramą hello (dostarczonych przez dewelopera danych), przed zapisaniem hello poświadczeń w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-133">Gateway encrypts hello credentials with hello certificate associated with hello gateway (supplied by data developer), before saving hello credentials in hello cloud.</span></span>
4. <span data-ttu-id="0daec-134">Usługi fabryka danych komunikuje się z bramą hello do planowania i zarządzanie zadań za pośrednictwem kanału kontroli, który używa kolejki magistrali usług Azure udostępnionych.</span><span class="sxs-lookup"><span data-stu-id="0daec-134">Data Factory service communicates with hello gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="0daec-135">Gdy zadanie działania kopiowania musi toobe rozpoczęte, fabryki danych kolejkuje Żądanie hello wraz z informacjami o poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="0daec-135">When a copy activity job needs toobe kicked off, Data Factory queues hello request along with credential information.</span></span> <span data-ttu-id="0daec-136">Brama dotyczącego hello zadania po sondowania hello kolejki.</span><span class="sxs-lookup"><span data-stu-id="0daec-136">Gateway kicks off hello job after polling hello queue.</span></span>
5. <span data-ttu-id="0daec-137">Brama Hello odszyfrowuje hello poświadczeń z hello sam certyfikatu, a następnie łączy toohello z lokalnym magazynem danych o typie odpowiedniego uwierzytelnienia i poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="0daec-137">hello gateway decrypts hello credentials with hello same certificate and then connects toohello on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="0daec-138">Brama Hello kopiuje dane z magazynu w chmurze tooa lokalnego magazynu lub na odwrót w zależności od sposobu skonfigurowania hello działanie kopiowania w potoku danych hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-138">hello gateway copies data from an on-premises store tooa cloud storage, or vice versa depending on how hello Copy Activity is configured in hello data pipeline.</span></span> <span data-ttu-id="0daec-139">W tym kroku hello bramy komunikuje się bezpośrednio z usług magazynu w chmurze, takich jak magazyn obiektów Blob Azure za pośrednictwem bezpiecznego kanału (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="0daec-139">For this step, hello gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="0daec-140">Zagadnienia dotyczące korzystania z bramy</span><span class="sxs-lookup"><span data-stu-id="0daec-140">Considerations for using gateway</span></span>
* <span data-ttu-id="0daec-141">Pojedyncze wystąpienie bramy zarządzania danymi może służyć do wielu źródeł danych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="0daec-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="0daec-142">Jednak **pojedyncze wystąpienie bramy jest jeden fabryki danych Azure wiązanej tooonly** i nie mogą być udostępniane innym fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-142">However, **a single gateway instance is tied tooonly one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="0daec-143">Może mieć **tylko jedno wystąpienie bramy zarządzania danymi** zainstalowane na jednym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0daec-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="0daec-144">Załóżmy, masz dwie fabryki danych, które wymagają tooaccess lokalnych źródeł danych, należy tooinstall bramy na dwóch lokalnych komputerów.</span><span class="sxs-lookup"><span data-stu-id="0daec-144">Suppose, you have two data factories that need tooaccess on-premises data sources, you need tooinstall gateways on two on-premises computers.</span></span> <span data-ttu-id="0daec-145">Innymi słowy brama jest wiązana tooa danych specyficznych dla fabryki</span><span class="sxs-lookup"><span data-stu-id="0daec-145">In other words, a gateway is tied tooa specific data factory</span></span>
* <span data-ttu-id="0daec-146">Witaj **bramy nie jest konieczne toobe na powitania sam komputer jako źródło danych hello**.</span><span class="sxs-lookup"><span data-stu-id="0daec-146">hello **gateway does not need toobe on hello same machine as hello data source**.</span></span> <span data-ttu-id="0daec-147">Jednak o źródła danych toohello bliżej bramy skraca czas powitania dla źródła danych toohello tooconnect bramy hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-147">However, having gateway closer toohello data source reduces hello time for hello gateway tooconnect toohello data source.</span></span> <span data-ttu-id="0daec-148">Zalecamy zainstalowanie bramy hello na maszynie, która różni się od hello jednego źródła danych lokalnych hostów.</span><span class="sxs-lookup"><span data-stu-id="0daec-148">We recommend that you install hello gateway on a machine that is different from hello one that hosts on-premises data source.</span></span> <span data-ttu-id="0daec-149">Gdy hello bramy i źródła danych na różnych komputerach, hello bramy nie konkurować o zasoby z źródła danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-149">When hello gateway and data source are on different machines, hello gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="0daec-150">Może mieć **wielu bram na różnych komputerach łączenie toohello tego samego źródła danych lokalnych**.</span><span class="sxs-lookup"><span data-stu-id="0daec-150">You can have **multiple gateways on different machines connecting toohello same on-premises data source**.</span></span> <span data-ttu-id="0daec-151">Na przykład może mieć dwóch bram obsługująca fabryki dwóch danych, ale powitalne tego samego źródła danych lokalnych jest zarejestrowany w obu hello fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-151">For example, you may have two gateways serving two data factories but hello same on-premises data source is registered with both hello data factories.</span></span>
* <span data-ttu-id="0daec-152">Jeśli masz już bramy zainstalowanej na programu obsługi komputera **usługi Power BI** scenariuszu instalowanie **oddzielnej bramy dla fabryki danych Azure** na innym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0daec-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="0daec-153">Można używać bramy, nawet wtedy, gdy używasz **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="0daec-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="0daec-154">Traktuj źródła danych jako źródło danych lokalnych (który znajduje się za zaporą) nawet jeśli używasz **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="0daec-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="0daec-155">Użyj hello bramy tooestablish łączność między usługą hello i hello źródła danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-155">Use hello gateway tooestablish connectivity between hello service and hello data source.</span></span>
* <span data-ttu-id="0daec-156">Należy **Użyj bramy hello** nawet, jeśli magazyn danych hello jest w chmurze hello na **maszyny Wirtualnej Azure IaaS**.</span><span class="sxs-lookup"><span data-stu-id="0daec-156">You must **use hello gateway** even if hello data store is in hello cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="0daec-157">Instalacja</span><span class="sxs-lookup"><span data-stu-id="0daec-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="0daec-158">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0daec-158">Prerequisites</span></span>
* <span data-ttu-id="0daec-159">Witaj obsługiwane **systemu operacyjnego** wersje to Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="0daec-159">hello supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="0daec-160">Instalacja hello brama zarządzania danymi na kontrolerze domeny nie jest obecnie obsługiwana.</span><span class="sxs-lookup"><span data-stu-id="0daec-160">Installation of hello data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="0daec-161">.NET framework 4.5.1 lub nowszy jest wymagany.</span><span class="sxs-lookup"><span data-stu-id="0daec-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="0daec-162">Jeśli instalujesz bramę na komputerze z systemem Windows 7, zainstaluj program .NET Framework 4.5 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="0daec-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="0daec-163">Zobacz [wymagania systemowe programu .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="0daec-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="0daec-164">Witaj zalecane **konfiguracji** hello maszyna bramy jest co najmniej 2 GHz 4 rdzenie, 8 GB pamięci RAM i dysk 80 GB.</span><span class="sxs-lookup"><span data-stu-id="0daec-164">hello recommended **configuration** for hello gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="0daec-165">Hibernacja hello komputer hosta, hello bramy nie odpowiada toodata żądań.</span><span class="sxs-lookup"><span data-stu-id="0daec-165">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span> <span data-ttu-id="0daec-166">W związku z tym, skonfigurować odpowiednie **planu zasilania** na komputerze hello przed zainstalowaniem bramy hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-166">Therefore, configure an appropriate **power plan** on hello computer before installing hello gateway.</span></span> <span data-ttu-id="0daec-167">Jeśli maszyna hello jest skonfigurowany toohibernate, instalacja bramy hello monituje komunikat.</span><span class="sxs-lookup"><span data-stu-id="0daec-167">If hello machine is configured toohibernate, hello gateway installation prompts a message.</span></span>
* <span data-ttu-id="0daec-168">Musisz mieć uprawnienia administratora na powitania tooinstall maszyny i skonfigurować brama zarządzania danymi hello pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="0daec-168">You must be an administrator on hello machine tooinstall and configure hello data management gateway successfully.</span></span> <span data-ttu-id="0daec-169">Możesz dodać kolejnych użytkowników toohello **brama zarządzania danymi użytkowników** lokalnej grupy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0daec-169">You can add additional users toohello **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="0daec-170">Hello członkami tej grupy są hello stanie toouse **Menedżera konfiguracji bramy zarządzania danymi** narzędzie tooconfigure hello bramy.</span><span class="sxs-lookup"><span data-stu-id="0daec-170">hello members of this group are able toouse hello **Data Management Gateway Configuration Manager** tool tooconfigure hello gateway.</span></span>

<span data-ttu-id="0daec-171">Jak skopiować uruchomień działania wystąpić na określonej częstotliwości, hello użycia zasobów (procesora CPU, pamięci) na maszynie hello również następuje hello sam wzorca z szczytowe i czas bezczynności.</span><span class="sxs-lookup"><span data-stu-id="0daec-171">As copy activity runs happen on a specific frequency, hello resource usage (CPU, memory) on hello machine also follows hello same pattern with peak and idle times.</span></span> <span data-ttu-id="0daec-172">Wykorzystanie zasobów zależy również od silnie hello ilość danych, jest przenoszony.</span><span class="sxs-lookup"><span data-stu-id="0daec-172">Resource utilization also depends heavily on hello amount of data being moved.</span></span> <span data-ttu-id="0daec-173">W przypadku wielu kopii zadania w toku, zostanie wyświetlony użycia zasobów, do góry w godzinach szczytu.</span><span class="sxs-lookup"><span data-stu-id="0daec-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="0daec-174">Opcje instalacji</span><span class="sxs-lookup"><span data-stu-id="0daec-174">Installation options</span></span>
<span data-ttu-id="0daec-175">Brama zarządzania danymi można zainstalować w hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="0daec-175">Data management gateway can be installed in hello following ways:</span></span>

* <span data-ttu-id="0daec-176">Instalując pakiet Instalatora MSI ze hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="0daec-176">By downloading an MSI setup package from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="0daec-177">Witaj MSI może być również używane tooupgrade istniejących danych zarządzania bramy toohello najnowszej wersji, z ustawieniami wszystkie zachowane.</span><span class="sxs-lookup"><span data-stu-id="0daec-177">hello MSI can also be used tooupgrade existing data management gateway toohello latest version, with all settings preserved.</span></span>
* <span data-ttu-id="0daec-178">Klikając **pobieranie i instalowanie bramy danych** łącze w PODRĘCZNIKU instalacji lub **Zainstaluj bezpośrednio na tym komputerze** w obszarze Ustawienia EXPRESS.</span><span class="sxs-lookup"><span data-stu-id="0daec-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="0daec-179">Zobacz [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu, aby uzyskać instrukcje na temat używania instalacji ekspresowej.</span><span class="sxs-lookup"><span data-stu-id="0daec-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="0daec-180">krok wykonywany ręcznie Hello przyjmuje toohello Centrum pobierania.</span><span class="sxs-lookup"><span data-stu-id="0daec-180">hello manual step takes you toohello download center.</span></span>  <span data-ttu-id="0daec-181">Witaj instrukcje dotyczące pobierania i instalowania bramy hello z Centrum pobierania znajdują się w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-181">hello instructions for downloading and installing hello gateway from download center are in hello next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="0daec-182">Najlepsze rozwiązania dotyczące instalacji:</span><span class="sxs-lookup"><span data-stu-id="0daec-182">Installation best practices:</span></span>
1. <span data-ttu-id="0daec-183">Skonfiguruj planu zasilania na komputerze-hoście hello hello bramy, dzięki czemu hello maszyny nie hibernacji.</span><span class="sxs-lookup"><span data-stu-id="0daec-183">Configure power plan on hello host machine for hello gateway so that hello machine does not hibernate.</span></span> <span data-ttu-id="0daec-184">Hibernacja hello komputer hosta, hello bramy nie odpowiada toodata żądań.</span><span class="sxs-lookup"><span data-stu-id="0daec-184">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span>
2. <span data-ttu-id="0daec-185">Utwórz kopię zapasową certyfikatu hello skojarzone z bramą hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-185">Back up hello certificate associated with hello gateway.</span></span>

### <a name="install-hello-gateway-from-download-center"></a><span data-ttu-id="0daec-186">Zainstaluj bramę hello z Centrum pobierania</span><span class="sxs-lookup"><span data-stu-id="0daec-186">Install hello gateway from download center</span></span>
1. <span data-ttu-id="0daec-187">Przejdź za[stronę pobierania brama zarządzania danymi firmy Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="0daec-187">Navigate too[Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="0daec-188">Kliknij przycisk **Pobierz**, wybierz hello odpowiednią wersję (**32-bitowych** vs. **64-bitowych**) i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0daec-188">Click **Download**, select hello appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="0daec-189">Uruchom hello **MSI** bezpośrednio lub zapisać go tooyour dysku twardego i uruchom.</span><span class="sxs-lookup"><span data-stu-id="0daec-189">Run hello **MSI** directly or save it tooyour hard disk and run.</span></span>
4. <span data-ttu-id="0daec-190">Na powitania **powitalnej** wybierz pozycję **języka** kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0daec-190">On hello **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="0daec-191">**Zaakceptuj** hello umowę licencyjną użytkownika oprogramowania i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0daec-191">**Accept** hello End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="0daec-192">Wybierz **folderu** tooinstall hello bramy i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="0daec-192">Select **folder** tooinstall hello gateway and click **Next**.</span></span>
7. <span data-ttu-id="0daec-193">Na powitania **gotowe tooinstall** kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="0daec-193">On hello **Ready tooinstall** page, click **Install**.</span></span>
8. <span data-ttu-id="0daec-194">Kliknij przycisk **Zakończ** toocomplete instalacji.</span><span class="sxs-lookup"><span data-stu-id="0daec-194">Click **Finish** toocomplete installation.</span></span>
9. <span data-ttu-id="0daec-195">Pobierz klucz hello z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0daec-195">Get hello key from hello Azure portal.</span></span> <span data-ttu-id="0daec-196">Zobacz następną sekcję hello instrukcje krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="0daec-196">See hello next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="0daec-197">Na powitania **bramy rejestru** strony **Menedżera konfiguracji bramy zarządzania danymi** na komputerze, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0daec-197">On hello **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do hello following steps:</span></span>
    1. <span data-ttu-id="0daec-198">Wklej tekst hello hello klucza.</span><span class="sxs-lookup"><span data-stu-id="0daec-198">Paste hello key in hello text.</span></span>
    2. <span data-ttu-id="0daec-199">Opcjonalnie kliknij **klucz bramy Pokaż** toosee hello klucza tekstu.</span><span class="sxs-lookup"><span data-stu-id="0daec-199">Optionally, click **Show gateway key** toosee hello key text.</span></span>
    3. <span data-ttu-id="0daec-200">Kliknij przycisk **zarejestrować**.</span><span class="sxs-lookup"><span data-stu-id="0daec-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="0daec-201">Rejestrowanie bramy przy użyciu klucza</span><span class="sxs-lookup"><span data-stu-id="0daec-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a><span data-ttu-id="0daec-202">Jeśli nie zostało utworzone logicznej bramy w portalu hello</span><span class="sxs-lookup"><span data-stu-id="0daec-202">If you haven't already created a logical gateway in hello portal</span></span>
<span data-ttu-id="0daec-203">toocreate bramy w kluczu hello portalu i get hello z hello **Konfiguruj** strony, wykonaj kroki z wskazówki w hello [przenoszenie danych między lokalnymi i w chmurze](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0daec-203">toocreate a gateway in hello portal and get hello key from hello **Configure** page, Follow steps from walkthrough in hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a><span data-ttu-id="0daec-204">Jeśli brama logicznej hello zostały już utworzone w portalu hello</span><span class="sxs-lookup"><span data-stu-id="0daec-204">If you have already created hello logical gateway in hello portal</span></span>
1. <span data-ttu-id="0daec-205">W portalu Azure Przejdź toohello **fabryki danych** , a następnie kliknij przycisk **połączonych usług** kafelka.</span><span class="sxs-lookup"><span data-stu-id="0daec-205">In Azure portal, navigate toohello **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Strona fabryki danych](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="0daec-207">W hello **połączonych usług** strony logicznej wybierz hello **bramy** utworzone w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-207">In hello **Linked Services** page, select hello logical **gateway** you created in hello portal.</span></span>

    ![logiczne bramy](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="0daec-209">W hello **bramy danych** kliknij przycisk **pobieranie i instalowanie bramy danych**.</span><span class="sxs-lookup"><span data-stu-id="0daec-209">In hello **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Pobierz łącze w portalu hello](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="0daec-211">W hello **Konfiguruj** kliknij przycisk **ponowne tworzenie klucza**.</span><span class="sxs-lookup"><span data-stu-id="0daec-211">In hello **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="0daec-212">Kliknij przycisk Tak na komunikat ostrzegawczy powitania po odczytaniu jej starannie.</span><span class="sxs-lookup"><span data-stu-id="0daec-212">Click Yes on hello warning message after reading it carefully.</span></span>

    ![Ponowne tworzenie klucza](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="0daec-214">Kliknij przycisk Kopiuj dalej klucz toohello.</span><span class="sxs-lookup"><span data-stu-id="0daec-214">Click Copy button next toohello key.</span></span> <span data-ttu-id="0daec-215">klucz Hello jest skopiowany toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="0daec-215">hello key is copied toohello clipboard.</span></span>

    ![Kopiowanie klucza](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="0daec-217">Ikony systemowe na pasku zadań / powiadomienia</span><span class="sxs-lookup"><span data-stu-id="0daec-217">System tray icons/ notifications</span></span>
<span data-ttu-id="0daec-218">Witaj poniższej ilustracji przedstawiono niektóre hello ikony na pasku zadań, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="0daec-218">hello following image shows some of hello tray icons that you see.</span></span>

![ikony systemowe na pasku zadań](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="0daec-220">Jeśli Przenieś kursor nad komunikat ikona/powiadomień na pasku zadań systemu hello, zobaczysz szczegółowe informacje o stanie hello hello operacji bramy/aktualizacji w oknie podręcznym.</span><span class="sxs-lookup"><span data-stu-id="0daec-220">If you move cursor over hello system tray icon/notification message, you see details about hello state of hello gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="0daec-221">Porty i zapory</span><span class="sxs-lookup"><span data-stu-id="0daec-221">Ports and firewall</span></span>
<span data-ttu-id="0daec-222">Istnieją dwa zapory należy tooconsider: **firmowej zapory** uruchomiony na routerze centralnej hello organizacji hello i **zapory systemu Windows** skonfigurowany jako demon na komputerze lokalnym hello, gdzie hello Brama jest instalowana.</span><span class="sxs-lookup"><span data-stu-id="0daec-222">There are two firewalls you need tooconsider: **corporate firewall** running on hello central router of hello organization, and **Windows firewall** configured as a daemon on hello local machine where hello gateway is installed.</span></span>  

![zapory](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="0daec-224">Na poziomie firmowa zapora, należy skonfigurować hello następujące domeny i portów wychodzących:</span><span class="sxs-lookup"><span data-stu-id="0daec-224">At corporate firewall level, you need configure hello following domains and outbound ports:</span></span>

| <span data-ttu-id="0daec-225">Nazwy domen</span><span class="sxs-lookup"><span data-stu-id="0daec-225">Domain names</span></span> | <span data-ttu-id="0daec-226">Porty</span><span class="sxs-lookup"><span data-stu-id="0daec-226">Ports</span></span> | <span data-ttu-id="0daec-227">Opis</span><span class="sxs-lookup"><span data-stu-id="0daec-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0daec-228">*. servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="0daec-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="0daec-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="0daec-229">443, 80</span></span> |<span data-ttu-id="0daec-230">Używany do komunikacji z zapleczem usługi przenoszenia danych</span><span class="sxs-lookup"><span data-stu-id="0daec-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="0daec-231">*. core.windows.net</span><span class="sxs-lookup"><span data-stu-id="0daec-231">*.core.windows.net</span></span> |<span data-ttu-id="0daec-232">443</span><span class="sxs-lookup"><span data-stu-id="0daec-232">443</span></span> |<span data-ttu-id="0daec-233">Używany do kopiowania przejściowa przy użyciu obiektów Blob platformy Azure (jeśli jest skonfigurowane)</span><span class="sxs-lookup"><span data-stu-id="0daec-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="0daec-234">*. frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="0daec-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="0daec-235">443</span><span class="sxs-lookup"><span data-stu-id="0daec-235">443</span></span> |<span data-ttu-id="0daec-236">Używany do komunikacji z zapleczem usługi przenoszenia danych</span><span class="sxs-lookup"><span data-stu-id="0daec-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="0daec-237">Na poziomie zapory systemu Windows te porty wyjściowe zwykle są włączone.</span><span class="sxs-lookup"><span data-stu-id="0daec-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="0daec-238">Nie można skonfigurować portów i domen hello odpowiednio na maszynie bramy.</span><span class="sxs-lookup"><span data-stu-id="0daec-238">If not, you can configure hello domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="0daec-239">Na podstawie Twojego źródła / sink mogą mieć dodatkowe domeny toowhitelist i portów wychodzących w sieci firmowej/Zapora systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="0daec-239">Based on your source/ sinks, you may have toowhitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="0daec-240">Dla niektórych baz danych w chmurze (na przykład: [bazy danych SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [usługi Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), itd.), może być konieczne toowhitelist adres IP komputera bramy na ich konfiguracji zapory.</span><span class="sxs-lookup"><span data-stu-id="0daec-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need toowhitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a><span data-ttu-id="0daec-241">Kopiowanie danych z magazynu danych źródła danych magazynu tooa odbioru</span><span class="sxs-lookup"><span data-stu-id="0daec-241">Copy data from a source data store tooa sink data store</span></span>
<span data-ttu-id="0daec-242">Sprawdź, czy reguły zapory hello są włączone prawidłowo na powitania firmowej zapory, Zapora systemu Windows na komputerze bramy hello, i magazyn danych hello, sam.</span><span class="sxs-lookup"><span data-stu-id="0daec-242">Ensure that hello firewall rules are enabled properly on hello corporate firewall, Windows firewall on hello gateway machine, and hello data store itself.</span></span> <span data-ttu-id="0daec-243">Włączenie tych zasad umożliwia hello bramy tooconnect tooboth źródła i sink pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="0daec-243">Enabling these rules allows hello gateway tooconnect tooboth source and sink successfully.</span></span> <span data-ttu-id="0daec-244">Włącz reguły dla każdego magazynu danych, który jest używany w operacji kopiowania hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-244">Enable rules for each data store that is involved in hello copy operation.</span></span>

<span data-ttu-id="0daec-245">Na przykład toocopy z **ujścia danych bazy danych SQL Azure tooan magazynu lokalnego lub ujścia magazynu danych SQL Azure**, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0daec-245">For example, toocopy from **an on-premises data store tooan Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do hello following steps:</span></span>

* <span data-ttu-id="0daec-246">Zezwalaj na wychodzące **TCP** komunikację za pośrednictwem portu **1433** dla zapory systemu Windows i firmowej zapory.</span><span class="sxs-lookup"><span data-stu-id="0daec-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="0daec-247">Skonfiguruj ustawienia zapory hello Azure SQL tooadd hello adresu IP serwera hello bramy maszyny toohello listę dozwolonych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="0daec-247">Configure hello firewall settings of Azure SQL server tooadd hello IP address of hello gateway machine toohello list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="0daec-248">Jeśli Zapora nie zezwala na wychodzący port 1433, brama nie bezpośredni dostęp Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="0daec-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="0daec-249">W takim przypadku można użyć [przemieszczane kopiowania](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL bazy danych platformy Azure / SQL Azure DW.</span><span class="sxs-lookup"><span data-stu-id="0daec-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="0daec-250">W tym scenariuszu do przenoszenia danych hello są tylko wymagane HTTPS (port 443).</span><span class="sxs-lookup"><span data-stu-id="0daec-250">In this scenario, you would only require HTTPS (port 443) for hello data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="0daec-251">Zagadnienia dotyczące serwera proxy</span><span class="sxs-lookup"><span data-stu-id="0daec-251">Proxy server considerations</span></span>
<span data-ttu-id="0daec-252">Jeśli środowisko sieci firmowej używa serwera proxy serwera tooaccess hello internet, skonfigurować danych zarządzania bramy toouse odpowiednie ustawienia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="0daec-252">If your corporate network environment uses a proxy server tooaccess hello internet, configure data management gateway toouse appropriate proxy settings.</span></span> <span data-ttu-id="0daec-253">W fazie początkowe rejestracyjny hello można ustawić powitania serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="0daec-253">You can set hello proxy during hello initial registration phase.</span></span>

![Zestaw proxy podczas rejestracji](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="0daec-255">Brama używa powitania serwera proxy serwera tooconnect toohello chmury usługi.</span><span class="sxs-lookup"><span data-stu-id="0daec-255">Gateway uses hello proxy server tooconnect toohello cloud service.</span></span> <span data-ttu-id="0daec-256">Kliknij przycisk **zmiany** łącze podczas instalacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="0daec-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="0daec-257">Zobacz hello **ustawienie serwera proxy** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0daec-257">You see hello **proxy setting** dialog.</span></span>

![Zestaw serwera proxy przy użyciu Menedżera konfiguracji](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="0daec-259">Dostępne są trzy opcje konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="0daec-259">There are three configuration options:</span></span>

* <span data-ttu-id="0daec-260">**Nie używaj serwera proxy**: bramy nie używa jawnie żadnych usług toocloud tooconnect serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="0daec-260">**Do not use proxy**: Gateway does not explicitly use any proxy tooconnect toocloud services.</span></span>
* <span data-ttu-id="0daec-261">**Użyj serwera proxy systemu**: hello serwera proxy, ustawienie skonfigurowane w diahost.exe.config i diawp.exe.config używa bramy.  Jeśli żadnego serwera proxy jest skonfigurowany w diahost.exe.config i diawp.exe.config, nawiązanie połączenia bramy usługi toocloud bezpośrednio, bez przechodzenia przez serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="0daec-261">**Use system proxy**: Gateway uses hello proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span>
* <span data-ttu-id="0daec-262">**Użyć niestandardowego serwera proxy**: Konfigurowanie toouse ustawienia serwera proxy hello HTTP bramy, zamiast konfiguracje diahost.exe.config i diawp.exe.config.  Wymagane są adres i Port.</span><span class="sxs-lookup"><span data-stu-id="0daec-262">**Use custom proxy**: Configure hello HTTP proxy setting toouse for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="0daec-263">Nazwa użytkownika i hasło są opcjonalne, w zależności od ustawienia uwierzytelniania serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="0daec-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="0daec-264">Wszystkie ustawienia są zaszyfrowane za pomocą hello certyfikat poświadczeń bramy hello i przechowywane lokalnie na komputerze-hoście hello bramy.</span><span class="sxs-lookup"><span data-stu-id="0daec-264">All settings are encrypted with hello credential certificate of hello gateway and stored locally on hello gateway host machine.</span></span>

<span data-ttu-id="0daec-265">Brama zarządzania danymi Hello usługi hosta do automatycznego uruchomienia po zapisaniu hello zaktualizować ustawienia serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="0daec-265">hello data management gateway Host Service restarts automatically after you save hello updated proxy settings.</span></span>

<span data-ttu-id="0daec-266">Po brama została pomyślnie zarejestrowana, tooview lub zaktualizować ustawienia serwera proxy, należy użyć Menedżera konfiguracji bramy zarządzania danymi.</span><span class="sxs-lookup"><span data-stu-id="0daec-266">After gateway has been successfully registered, if you want tooview or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="0daec-267">Uruchom **Menedżera konfiguracji bramy zarządzania danymi**.</span><span class="sxs-lookup"><span data-stu-id="0daec-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="0daec-268">Przełącz toohello **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="0daec-268">Switch toohello **Settings** tab.</span></span>
3. <span data-ttu-id="0daec-269">Kliknij przycisk **zmiany** łącze w **serwer HTTP Proxy** hello toolaunch sekcji **ustawiony serwer Proxy HTTP** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0daec-269">Click **Change** link in **HTTP Proxy** section toolaunch hello **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="0daec-270">Po kliknięciu hello **dalej** przycisku, zobacz okno dialogowe ostrzeżenia pytania dla użytkownika ustawienia proxy hello toosave uprawnień i uruchom ponownie hello usługa hosta bramy.</span><span class="sxs-lookup"><span data-stu-id="0daec-270">After you click hello **Next** button, you see a warning dialog asking for your permission toosave hello proxy setting and restart hello Gateway Host Service.</span></span>

<span data-ttu-id="0daec-271">Można wyświetlać i aktualizować serwer proxy HTTP za pomocą narzędzia Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="0daec-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Zestaw serwera proxy przy użyciu Menedżera konfiguracji](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="0daec-273">Jeśli skonfigurowano serwer proxy z uwierzytelnianiem NTLM usługa hosta bramy jest uruchamiana hello konta domeny.</span><span class="sxs-lookup"><span data-stu-id="0daec-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under hello domain account.</span></span> <span data-ttu-id="0daec-274">Jeśli zmienisz hasło konta domeny hello później hello, pamiętaj tooupdate ustawienia konfiguracji dla usługi hello i odpowiednio uruchom go ponownie.</span><span class="sxs-lookup"><span data-stu-id="0daec-274">If you change hello password for hello domain account later, remember tooupdate configuration settings for hello service and restart it accordingly.</span></span> <span data-ttu-id="0daec-275">Ze względu na wymagania toothis zaleca się, że używasz domeny dedykowanego konta tooaccess powitania serwera proxy, który nie jest wymagane hasło hello tooupdate często.</span><span class="sxs-lookup"><span data-stu-id="0daec-275">Due toothis requirement, we suggest you use a dedicated domain account tooaccess hello proxy server that does not require you tooupdate hello password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="0daec-276">Skonfiguruj ustawienia serwera proxy</span><span class="sxs-lookup"><span data-stu-id="0daec-276">Configure proxy server settings</span></span>
<span data-ttu-id="0daec-277">W przypadku wybrania **użycia serwera proxy systemu** ustawienie serwera proxy hello HTTP, brama używa hello ustawienie serwera proxy w diahost.exe.config i diawp.exe.config.  Jeśli w diahost.exe.config i diawp.exe.config określono żadnego serwera proxy, nawiązanie połączenia bramy usługi toocloud bezpośrednio, bez przechodzenia przez serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="0daec-277">If you select **Use system proxy** setting for hello HTTP proxy, gateway uses hello proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span> <span data-ttu-id="0daec-278">Witaj Poniższa procedura zawiera instrukcje dotyczące aktualizacji hello diahost.exe.config pliku.</span><span class="sxs-lookup"><span data-stu-id="0daec-278">hello following procedure provides instructions for updating hello diahost.exe.config file.</span></span>  

1. <span data-ttu-id="0daec-279">W Eksploratorze plików tworzą kopię bezpieczne tooback C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared\diahost.exe.config hello oryginalnego pliku.</span><span class="sxs-lookup"><span data-stu-id="0daec-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback up hello original file.</span></span>
2. <span data-ttu-id="0daec-280">Uruchamianie Notepad.exe uruchomioną jako administrator, a następnie otwórz plik tekstowy "C:\Program Files\Microsoft danych zarządzania Gateway\2.0\Shared\diahost.exe.config. Hello domyślny znacznik można znaleźć system.net pokazane na powitania następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="0daec-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find hello default tag for system.net as shown in hello following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="0daec-281">Następnie można dodać szczegóły serwera proxy, jak pokazano w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="0daec-281">You can then add proxy server details as shown in hello following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="0daec-282">Dodatkowe właściwości są dozwolone wewnątrz hello proxy tag toospecify hello wymagane ustawienia, takie jak scriptLocation.</span><span class="sxs-lookup"><span data-stu-id="0daec-282">Additional properties are allowed inside hello proxy tag toospecify hello required settings like scriptLocation.</span></span> <span data-ttu-id="0daec-283">Odwołuje się zbyt[serwera proxy elementu (ustawienia sieciowe)](https://msdn.microsoft.com/library/sa91de1e.aspx) na składni.</span><span class="sxs-lookup"><span data-stu-id="0daec-283">Refer too[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="0daec-284">Zapisanie pliku konfiguracyjnego hello w hello oryginalnej lokalizacji, a następnie uruchom ponownie hello usługi hosta bramy zarządzania danymi, które przejmuje hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="0daec-284">Save hello configuration file into hello original location, then restart hello Data Management Gateway Host service, which picks up hello changes.</span></span> <span data-ttu-id="0daec-285">Usługa hello toorestart: użyj apletu usługi w Panelu sterowania hello, lub z hello **Menedżera konfiguracji bramy zarządzania danymi** > kliknij hello **Zatrzymaj usługę** przycisk, a następnie kliknij przycisk hello **Uruchomić usługę**.</span><span class="sxs-lookup"><span data-stu-id="0daec-285">toorestart hello service: use services applet from hello control panel, or from hello **Data Management Gateway Configuration Manager** > click hello **Stop Service** button, then click hello **Start Service**.</span></span> <span data-ttu-id="0daec-286">Jeśli hello usługa nie zostanie uruchomiona, istnieje prawdopodobieństwo, że dodano niepoprawną składnię tagu XML w pliku konfiguracyjnym aplikacji hello, który był edytowany.</span><span class="sxs-lookup"><span data-stu-id="0daec-286">If hello service does not start, it is likely that an incorrect XML tag syntax has been added into hello application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0daec-287">Nie zapomnij tooupdate **zarówno** diahost.exe.config i diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="0daec-287">Do not forget tooupdate **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="0daec-288">Ponadto punkty toothese, należy również toomake się, że w dozwolonych w firmie Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="0daec-288">In addition toothese points, you also need toomake sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="0daec-289">Witaj listę prawidłowych adresów IP firmy Microsoft Azure można pobrać z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="0daec-289">hello list of valid Microsoft Azure IP addresses can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="0daec-290">Symptomów zapory i serwera proxy problemów związanych z serwerami</span><span class="sxs-lookup"><span data-stu-id="0daec-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="0daec-291">Jeśli wystąpią toohello podobne błędy po takich, które prawdopodobnie ukończenia konfiguracji tooimproper hello zapory lub serwera proxy, która blokuje bramy z łączącego tooauthenticate fabryki tooData sam.</span><span class="sxs-lookup"><span data-stu-id="0daec-291">If you encounter errors similar toohello following ones, it is likely due tooimproper configuration of hello firewall or proxy server, which blocks gateway from connecting tooData Factory tooauthenticate itself.</span></span> <span data-ttu-id="0daec-292">Zobacz tooensure sekcji tooprevious Serwer zapory i serwera proxy są poprawnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="0daec-292">Refer tooprevious section tooensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="0daec-293">Podczas próby tooregister hello bramy otrzymasz hello następujący błąd: "klucz bramy hello tooregister nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="0daec-293">When you try tooregister hello gateway, you receive hello following error: "Failed tooregister hello gateway key.</span></span> <span data-ttu-id="0daec-294">Przed podjęciem ponownej próby klucz bramy hello tooregister, upewnij się, że powitalne brama zarządzania danymi jest w stanie połączenia i hello usługa hosta bramy zarządzania danymi została uruchomiona."</span><span class="sxs-lookup"><span data-stu-id="0daec-294">Before trying tooregister hello gateway key again, confirm that hello data management gateway is in a connected state and hello Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="0daec-295">Po otwarciu Menedżera konfiguracji zostanie wyświetlony stan jako "Rozłączono" lub "Łączenie."</span><span class="sxs-lookup"><span data-stu-id="0daec-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="0daec-296">Podczas przeglądania dzienników zdarzeń systemu Windows, w obszarze "Podglądu zdarzeń" > "I usługi Dzienniki aplikacji" > "Brama zarządzania danymi", można wyświetlić komunikaty o błędach, takich jak hello następujący błąd:`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="0daec-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as hello following error: `Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="0daec-297">Otwórz port 8050 na potrzeby szyfrowania poświadczeń</span><span class="sxs-lookup"><span data-stu-id="0daec-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="0daec-298">Hello **ustawienie poświadczeń** zastosowań aplikacji hello portu wejściowego **8050** toorelay poświadczenia toohello bramy podczas konfigurowania lokalnego połączonej usługi w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0daec-298">hello **Setting Credentials** application uses hello inbound port **8050** toorelay credentials toohello gateway when you set up an on-premises linked service in hello Azure portal.</span></span> <span data-ttu-id="0daec-299">Podczas instalacji bramy domyślnie instalacja bramy hello powoduje otwarcie go na komputerze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-299">During gateway setup, by default, hello gateway installation opens it on hello gateway machine.</span></span>

<span data-ttu-id="0daec-300">Jeśli używasz zapory innych firm, można ręcznie otwórz hello port 8050.</span><span class="sxs-lookup"><span data-stu-id="0daec-300">If you are using a third-party firewall, you can manually open hello port 8050.</span></span> <span data-ttu-id="0daec-301">Jeśli napotkasz problem zapory podczas instalacji bramy można spróbować użyć następującego polecenia tooinstall hello bramy bez konfigurowania zapory hello hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-301">If you run into firewall issue during gateway setup, you can try using hello following command tooinstall hello gateway without configuring hello firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="0daec-302">Jeśli wybierzesz nie tooopen hello portu 8050 na komputerze bramy hello używa mechanizmów innych niż z użyciem hello **ustawienie poświadczeń** poświadczeń magazynu danych tooconfigure aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0daec-302">If you choose not tooopen hello port 8050 on hello gateway machine, use mechanisms other than using hello **Setting Credentials** application tooconfigure data store credentials.</span></span> <span data-ttu-id="0daec-303">Na przykład można użyć [AzureRmDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0daec-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="0daec-304">Zobacz [ustawienie poświadczeń i zabezpieczeń](#set-credentials-and-securityy) sekcję na temat sposobu poświadczeń magazynu danych można ustawić.</span><span class="sxs-lookup"><span data-stu-id="0daec-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="0daec-305">Aktualizacja</span><span class="sxs-lookup"><span data-stu-id="0daec-305">Update</span></span>
<span data-ttu-id="0daec-306">Domyślnie gdy dostępna jest nowsza wersja bramy hello brama zarządzania danymi jest automatycznie aktualizowany.</span><span class="sxs-lookup"><span data-stu-id="0daec-306">By default, data management gateway is automatically updated when a newer version of hello gateway is available.</span></span> <span data-ttu-id="0daec-307">Hello bramy nie jest aktualizowana, aż wszystkie hello zaplanowane zadania są wykonywane.</span><span class="sxs-lookup"><span data-stu-id="0daec-307">hello gateway is not updated until all hello scheduled tasks are done.</span></span> <span data-ttu-id="0daec-308">Kolejne zadania są przetwarzane przez bramę hello aż do zakończenia operacji aktualizacji hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-308">No further tasks are processed by hello gateway until hello update operation is completed.</span></span> <span data-ttu-id="0daec-309">W przypadku niepowodzenia aktualizacji hello bramy jest przywracana toohello starą wersję.</span><span class="sxs-lookup"><span data-stu-id="0daec-309">If hello update fails, gateway is rolled back toohello old version.</span></span>

<span data-ttu-id="0daec-310">Zostanie wyświetlony hello zaplanowane czas aktualizacji w następujących miejscach hello:</span><span class="sxs-lookup"><span data-stu-id="0daec-310">You see hello scheduled update time in hello following places:</span></span>

* <span data-ttu-id="0daec-311">strony właściwości bramy Hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0daec-311">hello gateway properties page in hello Azure portal.</span></span>
* <span data-ttu-id="0daec-312">Strona główna hello Menedżera konfiguracji bramy zarządzania danymi</span><span class="sxs-lookup"><span data-stu-id="0daec-312">Home page of hello Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="0daec-313">Komunikat powiadomienia na pasku zadań systemu.</span><span class="sxs-lookup"><span data-stu-id="0daec-313">System tray notification message.</span></span>

<span data-ttu-id="0daec-314">na karcie Strona główna Hello hello Menedżera konfiguracji bramy zarządzania danymi Wyświetla harmonogram aktualizacji hello i hello ostatni czas hello bramy zostało zainstalowane zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="0daec-314">hello Home tab of hello Data Management Gateway Configuration Manager displays hello update schedule and hello last time hello gateway was installed/updated.</span></span>

![Aktualizacje harmonogramu](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="0daec-316">Można zainstalować aktualizację powitania od razu lub zaczekaj na powitania bramy toobe automatycznie zaktualizowany w momencie hello zaplanowane.</span><span class="sxs-lookup"><span data-stu-id="0daec-316">You can install hello update right away or wait for hello gateway toobe automatically updated at hello scheduled time.</span></span> <span data-ttu-id="0daec-317">Na przykład powitania po pokazuje obrazu hello komunikatu powiadomienia pokazanym w hello Menedżera konfiguracji bramy wraz z przycisku Aktualizuj powitania kliknij tooinstall go.</span><span class="sxs-lookup"><span data-stu-id="0daec-317">For example, hello following image shows you hello notification message shown in hello Gateway Configuration Manager along with hello Update button that you can click tooinstall it immediately.</span></span>

![Aktualizacja w DMG programu Configuration Manager](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="0daec-319">Hello komunikatu powiadomienia w hello na pasku zadań będzie wyglądać jak pokazano w powitania po obrazu:</span><span class="sxs-lookup"><span data-stu-id="0daec-319">hello notification message in hello system tray would look as shown in hello following image:</span></span>

![Komunikat na pasku zadań systemu](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="0daec-321">Możesz wyświetlić stan hello operacji aktualizacji (ręczne lub automatyczne) hello na pasku zadań.</span><span class="sxs-lookup"><span data-stu-id="0daec-321">You see hello status of update operation (manual or automatic) in hello system tray.</span></span> <span data-ttu-id="0daec-322">Po następnym uruchomieniu Menedżera konfiguracji bramy zostanie wyświetlony komunikat na pasek tej bramy hello powiadomień hello została zaktualizowana wraz z linkiem zbyt[co to jest nowy temat](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="0daec-322">When you launch Gateway Configuration Manager next time, you see a message on hello notification bar that hello gateway has been updated along with a link too[what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="toodisableenable-auto-update-feature"></a><span data-ttu-id="0daec-323">Włącz/toodisable funkcji automatycznej aktualizacji</span><span class="sxs-lookup"><span data-stu-id="0daec-323">toodisable/enable auto-update feature</span></span>
<span data-ttu-id="0daec-324">Użytkownik może Włącz/Wyłącz hello funkcja Aktualizacje automatyczne, wykonując następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0daec-324">You can disable/enable hello auto-update feature by doing hello following steps:</span></span>

<span data-ttu-id="0daec-325">[Dla jednego węzła bramy]</span><span class="sxs-lookup"><span data-stu-id="0daec-325">[For single node gateway]</span></span>
1. <span data-ttu-id="0daec-326">Uruchom program Windows PowerShell na komputerze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-326">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="0daec-327">Przełącz folderu C:\Program Files\Microsoft danych zarządzania Gateway\2.0\PowerShellScript toohello.</span><span class="sxs-lookup"><span data-stu-id="0daec-327">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="0daec-328">Witaj uruchom następujące polecenie tooturn hello automatycznej aktualizacji funkcji OFF (wyłączone).</span><span class="sxs-lookup"><span data-stu-id="0daec-328">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="0daec-329">tooturn je ponownie:</span><span class="sxs-lookup"><span data-stu-id="0daec-329">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="0daec-330">[[Wielowęzłowego wysoką dostępność i skalowalność bramy (wersja zapoznawcza)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="0daec-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="0daec-331">Uruchom program Windows PowerShell na komputerze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-331">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="0daec-332">Przełącz folderu C:\Program Files\Microsoft danych zarządzania Gateway\2.0\PowerShellScript toohello.</span><span class="sxs-lookup"><span data-stu-id="0daec-332">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="0daec-333">Witaj uruchom następujące polecenie tooturn hello automatycznej aktualizacji funkcji OFF (wyłączone).</span><span class="sxs-lookup"><span data-stu-id="0daec-333">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="0daec-334">Bramy o wysokiej dostępności funkcji (wersja zapoznawcza) wymagany jest dodatkowy param AuthKey.</span><span class="sxs-lookup"><span data-stu-id="0daec-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="0daec-335">tooturn je ponownie:</span><span class="sxs-lookup"><span data-stu-id="0daec-335">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="0daec-336">Jeśli dostęp do portalu hello na komputerze, który różni się od hello maszyna bramy, należy się upewnić że hello Menedżer poświadczeń aplikacji mogą się łączyć maszyna bramy toohello.</span><span class="sxs-lookup"><span data-stu-id="0daec-336">If you access hello portal from a machine that is different from hello gateway machine, you must make sure that hello Credentials Manager application can connect toohello gateway machine.</span></span> <span data-ttu-id="0daec-337">Jeśli aplikacja hello można nawiązać połączenia z hello maszyna bramy, jego nie zezwala tooset poświadczeń dla źródła danych hello i źródła danych toohello połączenia tootest.</span><span class="sxs-lookup"><span data-stu-id="0daec-337">If hello application cannot reach hello gateway machine, it does not allow you tooset credentials for hello data source and tootest connection toohello data source.</span></span>  

<span data-ttu-id="0daec-338">Jeśli używasz hello **ustawienie poświadczeń** aplikacji, hello portal szyfruje poświadczenia hello z hello certyfikatu podanego w hello **certyfikatu** kartę hello **bramy Menedżer konfiguracji** na komputerze bramy hello.</span><span class="sxs-lookup"><span data-stu-id="0daec-338">When you use hello **Setting Credentials** application, hello portal encrypts hello credentials with hello certificate specified in hello **Certificate** tab of hello **Gateway Configuration Manager** on hello gateway machine.</span></span>

<span data-ttu-id="0daec-339">Jeśli szukasz oparty na interfejsach API podejście do szyfrowania poświadczeń hello, możesz użyć hello [AzureRmDataFactoryEncryptValue nowy](https://msdn.microsoft.com/library/mt603802.aspx) poświadczenia tooencrypt polecenia cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0daec-339">If you are looking for an API-based approach for encrypting hello credentials, you can use hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt credentials.</span></span> <span data-ttu-id="0daec-340">polecenie cmdlet Hello używa certyfikatów hello, że brama jest skonfigurowany toouse tooencrypt hello poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="0daec-340">hello cmdlet uses hello certificate that gateway is configured toouse tooencrypt hello credentials.</span></span> <span data-ttu-id="0daec-341">Dodaj zaszyfrowane poświadczenia toohello **EncryptedCredential** element hello **connectionString** w hello JSON.</span><span class="sxs-lookup"><span data-stu-id="0daec-341">You add encrypted credentials toohello **EncryptedCredential** element of hello **connectionString** in hello JSON.</span></span> <span data-ttu-id="0daec-342">Użyj hello JSON z hello [AzureRmDataFactoryLinkedService nowy](https://msdn.microsoft.com/library/mt603647.aspx) polecenia cmdlet lub hello Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-342">You use hello JSON with hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in hello Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="0daec-343">Jest jednym z podejść więcej do ustawiania poświadczeń przy użyciu Edytor fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="0daec-344">W przypadku utworzenia programu SQL Server połączone usługi za pomocą edytora hello i należy wprowadzić poświadczenia w postaci zwykłego tekstu, hello poświadczenia są szyfrowane za pomocą certyfikatu, który jest właścicielem hello usługi fabryka danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-344">If you create a SQL Server linked service by using hello editor and you enter credentials in plain text, hello credentials are encrypted using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="0daec-345">Nie używa certyfikatów hello, że brama jest skonfigurowany toouse.</span><span class="sxs-lookup"><span data-stu-id="0daec-345">It does NOT use hello certificate that gateway is configured toouse.</span></span> <span data-ttu-id="0daec-346">Takie podejście może być nieco szybsze w niektórych przypadkach, jest mniej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="0daec-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="0daec-347">Dlatego zaleca się, należy wykonać takie podejście tylko na potrzeby tworzenia/testowania.</span><span class="sxs-lookup"><span data-stu-id="0daec-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="0daec-348">Polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0daec-348">PowerShell cmdlets</span></span>
<span data-ttu-id="0daec-349">W tej sekcji opisano sposób toocreate i zarejestrować bramę za pomocą poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0daec-349">This section describes how toocreate and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="0daec-350">Uruchom **programu Azure PowerShell** w trybie administratora.</span><span class="sxs-lookup"><span data-stu-id="0daec-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="0daec-351">Zaloguj się za tooyour konto platformy Azure, uruchamiając hello następujące polecenia i wprowadzić poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0daec-351">Log in tooyour Azure account by running hello following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="0daec-352">Użyj hello **AzureRmDataFactoryGateway nowy** toocreate polecenia cmdlet logicznej bramy w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0daec-352">Use hello **New-AzureRmDataFactoryGateway** cmdlet toocreate a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="0daec-353">**Przykład polecenia i dane wyjściowe**:</span><span class="sxs-lookup"><span data-stu-id="0daec-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="0daec-354">W programie Azure PowerShell przełącznika folderu toohello: **C:\Program Files\Microsoft danych zarządzania Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="0daec-354">In Azure PowerShell, switch toohello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="0daec-355">Uruchom **RegisterGateway.ps1** skojarzone ze zmienną lokalne powitania **$Key** pokazane na powitania następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="0daec-355">Run **RegisterGateway.ps1** associated with hello local variable **$Key** as shown in hello following command.</span></span> <span data-ttu-id="0daec-356">Ten skrypt rejestruje agenta klienta hello zainstalowanej na komputerze z bramą logicznej hello utworzone wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0daec-356">This script registers hello client agent installed on your machine with hello logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="0daec-357">Za pomocą parametru IsRegisterOnRemoteMachine hello można zarejestrować bramy hello na komputerze zdalnym.</span><span class="sxs-lookup"><span data-stu-id="0daec-357">You can register hello gateway on a remote machine by using hello IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="0daec-358">Przykład:</span><span class="sxs-lookup"><span data-stu-id="0daec-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="0daec-359">Można użyć hello **Get-AzureRmDataFactoryGateway** polecenia cmdlet tooget hello lista bram w fabryce danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-359">You can use hello **Get-AzureRmDataFactoryGateway** cmdlet tooget hello list of Gateways in your data factory.</span></span> <span data-ttu-id="0daec-360">Gdy hello **stan** pokazuje **online**, oznacza to, brama jest gotowy toouse.</span><span class="sxs-lookup"><span data-stu-id="0daec-360">When hello **Status** shows **online**, it means your gateway is ready toouse.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="0daec-361">Można usunąć bramy przy użyciu hello **AzureRmDataFactoryGateway Usuń** opis polecenia cmdlet i aktualizacji bramy przy użyciu hello **AzureRmDataFactoryGateway zestaw** polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0daec-361">You can remove a gateway using hello **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using hello **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="0daec-362">Składnię i inne szczegółowe informacje o tych poleceniach cmdlet zobacz odwołanie do polecenia Cmdlet fabryki danych.</span><span class="sxs-lookup"><span data-stu-id="0daec-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="0daec-363">Lista bram przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0daec-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="0daec-364">Usuń bramę przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="0daec-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="0daec-365">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0daec-365">Next steps</span></span>
* <span data-ttu-id="0daec-366">Zobacz [przenoszenie danych między lokalnymi i w chmurze magazyny danych](data-factory-move-data-between-onprem-and-cloud.md) artykułu.</span><span class="sxs-lookup"><span data-stu-id="0daec-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="0daec-367">W przewodniku hello utworzysz potok, który korzysta z danych toomove bramy hello z tooan bazy danych programu SQL Server na lokalnych obiektów blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0daec-367">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span>  
