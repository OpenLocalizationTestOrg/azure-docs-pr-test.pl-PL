---
title: "Konfigurowanie klastra usługi Azure Service Fabric | Microsoft Docs"
description: "Szybki start — tworzenie klastra usługi Service Fabric z systemem Windows lub Linux na platformie Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: ec59450052b377412a28f7eaf55d1f1512b55195
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="64f7f-103">Tworzenie pierwszego klastra usługi Service Fabric na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="64f7f-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="64f7f-104">[Klaster usługi Service Fabric](service-fabric-deploy-anywhere.md) jest połączonym z siecią zestawem maszyn wirtualnych lub fizycznych, w którym wdraża się mikrousługi i nimi zarządza.</span><span class="sxs-lookup"><span data-stu-id="64f7f-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="64f7f-105">Niniejszy przewodnik Szybki start pomaga w utworzeniu klastra o pięciu węzłach, z systemem Windows lub Linux, za pośrednictwem środowiska [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) lub witryny [Azure Portal](http://portal.azure.com) w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="64f7f-105">This quickstart helps you to create a five-node cluster, running on either Windows or Linux, through the [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="64f7f-106">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="64f7f-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-the-azure-portal"></a><span data-ttu-id="64f7f-107">Korzystanie z witryny Azure Portal</span><span class="sxs-lookup"><span data-stu-id="64f7f-107">Use the Azure portal</span></span>

<span data-ttu-id="64f7f-108">Zaloguj się w witrynie Azure Portal pod adresem [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64f7f-108">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-the-cluster"></a><span data-ttu-id="64f7f-109">Tworzenie klastra</span><span class="sxs-lookup"><span data-stu-id="64f7f-109">Create the cluster</span></span>

1. <span data-ttu-id="64f7f-110">Kliknij przycisk **Nowy** znajdujący się w lewym górnym rogu witryny Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="64f7f-110">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>
2. <span data-ttu-id="64f7f-111">Wybierz pozycję **Compute** w bloku **Nowy**, a następnie wybierz opcję **Klaster usługi Service Fabric** w bloku **Compute**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-111">Select **Compute** from the **New** blade and then select **Service Fabric Cluster** from the **Compute** blade.</span></span>
3. <span data-ttu-id="64f7f-112">Uzupełnij formularz **Podstawy** usługi Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="64f7f-112">Fill out the Service Fabric **Basics** form.</span></span> <span data-ttu-id="64f7f-113">W sekcji **System operacyjny** wybierz wersję systemu Windows lub Linux, którego chcesz używać w węzłach klastra.</span><span class="sxs-lookup"><span data-stu-id="64f7f-113">For **Operating system**, select the version of Windows or Linux you want the cluster nodes to run.</span></span> <span data-ttu-id="64f7f-114">Nazwa użytkownika i hasło wprowadzone w tym miejscu są używane na potrzeby logowania się do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64f7f-114">The user name and password entered here is used to log in to the virtual machine.</span></span> <span data-ttu-id="64f7f-115">W obszarze **Grupa zasobów** utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="64f7f-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="64f7f-116">Grupa zasobów to logiczny kontener, w którym są tworzone i zbiorczo zarządzane zasoby platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="64f7f-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="64f7f-117">Po zakończeniu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-117">When complete, click **OK**.</span></span>

    ![Dane wyjściowe instalacji klastra][cluster-setup-basics]

4. <span data-ttu-id="64f7f-119">Uzupełnij formularz **Konfiguracja klastra**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-119">Fill out the **Cluster configuration** form.</span></span>  <span data-ttu-id="64f7f-120">Dla ustawienia **Liczba typów węzłów** wprowadź wartość „1”.</span><span class="sxs-lookup"><span data-stu-id="64f7f-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="64f7f-121">Wybierz pozycję **Typ węzła 1 (podstawowy)** i wypełnij formularz **Konfiguracja typu węzła**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-121">Select **Node type 1 (Primary)** and fill out the **Node type configuration** form.</span></span>  <span data-ttu-id="64f7f-122">Wprowadź nazwę typu węzła i dla pozycji [Warstwa trwałości](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) ustaw wartość „Brązowa”.</span><span class="sxs-lookup"><span data-stu-id="64f7f-122">Enter a node type name and set the [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) to "Bronze."</span></span>  <span data-ttu-id="64f7f-123">Wybierz rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="64f7f-123">Select a VM size.</span></span>

    <span data-ttu-id="64f7f-124">Typy węzłów definiują rozmiar maszyny wirtualnej, liczbę maszyn wirtualnych, niestandardowe punkty końcowe oraz inne ustawienia dla maszyn wirtualnych tego typu.</span><span class="sxs-lookup"><span data-stu-id="64f7f-124">Node types define the VM size, number of VMs, custom endpoints, and other settings for the VMs of that type.</span></span> <span data-ttu-id="64f7f-125">Każdy zdefiniowany typ węzła jest konfigurowany jako oddzielny zestaw skalowania maszyn wirtualnych, który jest używany do wdrażania maszyn wirtualnych i zarządzania nimi jako zestawem.</span><span class="sxs-lookup"><span data-stu-id="64f7f-125">Each node type defined is set up as a separate virtual machine scale set, which is used to deploy and managed virtual machines as a set.</span></span> <span data-ttu-id="64f7f-126">Każdy typ węzła może być niezależnie skalowany w górę lub w dół, może mieć różne zestawy otwartych portów i może mieć różne metryki pojemności.</span><span class="sxs-lookup"><span data-stu-id="64f7f-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="64f7f-127">Pierwszy lub główny typ węzła jest miejscem, w którym hostowane są usługi systemowe Service Fabric. Musi zawierać co najmniej pięć maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="64f7f-127">The first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="64f7f-128">W przypadku wszystkich wdrożeń produkcyjnych [planowanie pojemności](service-fabric-cluster-capacity.md) jest ważnym krokiem.</span><span class="sxs-lookup"><span data-stu-id="64f7f-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="64f7f-129">Niemniej w ramach tego przewodnika Szybki start nie uruchamiasz aplikacji, więc wybierz rozmiar maszyny wirtualnej *Standardowa DS1_v2*.</span><span class="sxs-lookup"><span data-stu-id="64f7f-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="64f7f-130">Wybierz wartość „Srebrna” dla [warstwy niezawodności](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) oraz ustaw początkową pojemność zestawu skalowania maszyn wirtualnych na 5.</span><span class="sxs-lookup"><span data-stu-id="64f7f-130">Select "Silver" for the [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="64f7f-131">Niestandardowe punkty końcowe otwierają porty w module równoważenia obciążenia platformy Azure, dzięki czemu możesz nawiązywać połączenie z aplikacjami uruchomionymi w klastrze.</span><span class="sxs-lookup"><span data-stu-id="64f7f-131">Custom endpoints open up ports in the Azure load balancer so that you can connect with applications running on the cluster.</span></span>  <span data-ttu-id="64f7f-132">Wprowadź „80, 8172”, aby otworzyć porty 80 i 8172.</span><span class="sxs-lookup"><span data-stu-id="64f7f-132">Enter "80, 8172" to open up ports 80 and 8172.</span></span>

    <span data-ttu-id="64f7f-133">Nie zaznaczaj pola wyboru **Skonfiguruj ustawienia zaawansowane**. Opcji tej używa się do dostosowywania punktów końcowych zarządzania protokołem TCP/HTTP, zakresem portów aplikacji, [ograniczeniami dotyczącymi umieszczania](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints) oraz [właściwościami pojemności](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="64f7f-133">Do not check the **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="64f7f-134">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-134">Select **OK**.</span></span>

6. <span data-ttu-id="64f7f-135">W formularzu **Konfigurowanie klastra** ustaw opcję **Diagnostyka** na wartość **Wł**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-135">In the **Cluster configuration** form, set **Diagnostics** to **On**.</span></span>  <span data-ttu-id="64f7f-136">W ramach tego przewodnika Szybki start nie musisz wprowadzać żadnych właściwości [ustawień sieci szkieletowej](service-fabric-cluster-fabric-settings.md).</span><span class="sxs-lookup"><span data-stu-id="64f7f-136">For this quickstart, you do not need to enter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="64f7f-137">W pozycji **Wersja sieci szkieletowej** wybierz tryb uaktualniania **Automatyczny**, dzięki czemu firma Microsoft będzie automatycznie aktualizować wersję kodu sieci szkieletowej obsługującego klaster.</span><span class="sxs-lookup"><span data-stu-id="64f7f-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates the version of the fabric code running the cluster.</span></span>  <span data-ttu-id="64f7f-138">Ustaw tryb **Ręczny**, jeśli chcesz [wybrać obsługiwaną wersję](service-fabric-cluster-upgrade.md) do uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="64f7f-138">Set the mode to **Manual** if you want to [choose a supported version](service-fabric-cluster-upgrade.md) to upgrade to.</span></span> 

    ![Konfiguracja typu węzła][node-type-config]

    <span data-ttu-id="64f7f-140">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-140">Select **OK**.</span></span>

7. <span data-ttu-id="64f7f-141">Uzupełnij formularz **Zabezpieczenia**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-141">Fill out the **Security** form.</span></span>  <span data-ttu-id="64f7f-142">W ramach tego przewodnika Szybki start wybierz opcję **Niezabezpieczony**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="64f7f-143">Niemniej zaleca się utworzenie zabezpieczonego klastra dla obciążeń produkcyjnych, ponieważ każda osoba może anonimowo połączyć się z niezabezpieczonym klastrem i przeprowadzić operacje związane z zarządzaniem.</span><span class="sxs-lookup"><span data-stu-id="64f7f-143">It is highly recommended to create a secure cluster for production workloads, however, since anyone can anonymously connect to an unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="64f7f-144">W usłudze Service Fabric używa się certyfikatów, aby zapewniać uwierzytelnianie i szyfrowanie w celu zabezpieczania różnych aspektów klastra i jego aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64f7f-144">Certificates are used in Service Fabric to provide authentication and encryption to secure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="64f7f-145">Aby uzyskać więcej informacji o sposobie wykorzystania certyfikatów w usłudze Service Fabric, zobacz [Scenariusze zabezpieczeń klastra usługi Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="64f7f-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="64f7f-146">Aby włączyć uwierzytelnianie użytkownika przy użyciu usługi Azure Active Directory lub skonfigurować certyfikaty dla zabezpieczeń aplikacji, [utwórz klaster z szablonu usługi Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="64f7f-146">To enable user authentication using Azure Active Directory or to set up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="64f7f-147">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-147">Select **OK**.</span></span>

8. <span data-ttu-id="64f7f-148">Przejrzyj podsumowanie.</span><span class="sxs-lookup"><span data-stu-id="64f7f-148">Review the summary.</span></span>  <span data-ttu-id="64f7f-149">Jeśli chcesz pobrać szablon usługi Resource Manager utworzony na podstawie wprowadzonych ustawień, wybierz opcję **Pobierz szablon i parametry**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-149">If you'd like to download a Resource Manager template built from the settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="64f7f-150">Wybierz opcję **Utwórz**, aby utworzyć klaster.</span><span class="sxs-lookup"><span data-stu-id="64f7f-150">Select **Create** to create the cluster.</span></span>

    <span data-ttu-id="64f7f-151">Możesz zobaczyć postępy tworzenia w powiadomieniach.</span><span class="sxs-lookup"><span data-stu-id="64f7f-151">You can see the creation progress in the notifications.</span></span> <span data-ttu-id="64f7f-152">(Kliknij ikonę „Dzwonka” w pobliżu paska stanu w prawym górnym rogu ekranu). Jeśli kliknięto opcję **Przypnij do tablicy startowej** podczas tworzenia klastra, zobaczysz pozycję **Wdrażanie klastra usługi Service Fabric** przypiętą do tablicy **Start**.</span><span class="sxs-lookup"><span data-stu-id="64f7f-152">(Click the "Bell" icon near the status bar at the upper right of your screen.) If you clicked **Pin to Startboard** while creating the cluster, you see **Deploying Service Fabric Cluster** pinned to the **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="64f7f-153">Wyświetlanie stanu klastra</span><span class="sxs-lookup"><span data-stu-id="64f7f-153">View cluster status</span></span>
<span data-ttu-id="64f7f-154">Po utworzeniu klastra możesz sprawdzić klaster w bloku **Przegląd** w portalu.</span><span class="sxs-lookup"><span data-stu-id="64f7f-154">Once your cluster is created, you can inspect your cluster in the **Overview** blade in the portal.</span></span> <span data-ttu-id="64f7f-155">Możesz teraz wyświetlić szczegóły klastra na pulpicie nawigacyjnym, w tym publiczny punkt końcowy klastra oraz link do narzędzia Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="64f7f-155">You can now see the details of your cluster in the dashboard, including the cluster's public endpoint and a link to Service Fabric Explorer.</span></span>

![Stan klastra][cluster-status]

### <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="64f7f-157">Wizualizowanie klastra za pomocą narzędzia Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="64f7f-157">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="64f7f-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) to odpowiednie narzędzie do wizualizowania klastra i zarządzania aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="64f7f-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="64f7f-159">Service Fabric Explorer jest usługą uruchamianą w klastrze.</span><span class="sxs-lookup"><span data-stu-id="64f7f-159">Service Fabric Explorer is a service that runs in the cluster.</span></span>  <span data-ttu-id="64f7f-160">Dostęp do tej usługi uzyskasz poprzez kliknięcie linku **Service Fabric Explorer** na stronie **Przegląd** klastra w portalu.</span><span class="sxs-lookup"><span data-stu-id="64f7f-160">Access it using a web browser by clicking the **Service Fabric Explorer** link of the cluster **Overview** page in the portal.</span></span>  <span data-ttu-id="64f7f-161">Możesz również wprowadzić jej adres bezpośrednio do przeglądarki: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="64f7f-161">You can also enter the address directly into the browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="64f7f-162">Pulpit nawigacyjny klastra zawiera omówienie klastra, w tym podsumowanie kondycji węzła i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64f7f-162">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="64f7f-163">Widok węzła przedstawia fizyczny układ klastra.</span><span class="sxs-lookup"><span data-stu-id="64f7f-163">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="64f7f-164">Dla danego węzła można sprawdzić, które aplikacje mają kod wdrożony w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="64f7f-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-to-the-cluster-using-powershell"></a><span data-ttu-id="64f7f-166">Nawiązywanie połączenia z klastrem przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="64f7f-166">Connect to the cluster using PowerShell</span></span>
<span data-ttu-id="64f7f-167">Sprawdź, czy klaster działa, nawiązując połączenie przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64f7f-167">Verify that the cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="64f7f-168">Moduł ServiceFabric programu PowerShell jest instalowany przy użyciu [Zestawu SDK usługi Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="64f7f-168">The ServiceFabric PowerShell module is installed with the [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="64f7f-169">Polecenie cmdlet [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) umożliwia ustanowienie połączenia z klastrem.</span><span class="sxs-lookup"><span data-stu-id="64f7f-169">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="64f7f-170">Inne przykłady łączenia z klastrem można znaleźć w temacie [Nawiązywanie połączenia z zabezpieczonym klastrem](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="64f7f-170">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="64f7f-171">Po nawiązaniu połączenia z klastrem użyj polecenia cmdlet [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps), aby wyświetlić listę węzłów w klastrze oraz informacje o stanie każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="64f7f-171">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="64f7f-172">Element **HealthState** powinien mieć wartość *OK* dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="64f7f-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-the-cluster"></a><span data-ttu-id="64f7f-173">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="64f7f-173">Remove the cluster</span></span>
<span data-ttu-id="64f7f-174">Klaster usługi Service Fabric składa się z innych zasobów platformy Azure poza samym zasobem klastra.</span><span class="sxs-lookup"><span data-stu-id="64f7f-174">A Service Fabric cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="64f7f-175">Dlatego też, aby całkowicie usunąć klaster usługi Service Fabric, musisz również usunąć wszystkie zasoby, z których się składa.</span><span class="sxs-lookup"><span data-stu-id="64f7f-175">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span> <span data-ttu-id="64f7f-176">Najprostszym sposobem na usunięcie klastra i wszystkich wykorzystywanych przez niego zasobów jest usunięcie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="64f7f-176">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> <span data-ttu-id="64f7f-177">Aby uzyskać informacje o innych sposobach usunięcia klastra lub usunięcia części (nie wszystkich) zasobów w grupie zasobów, zobacz [Usuwanie klastra](service-fabric-cluster-delete.md).</span><span class="sxs-lookup"><span data-stu-id="64f7f-177">For other ways to delete a cluster or to delete some (but not all) the resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="64f7f-178">Usuń grupę zasobów w witrynie Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="64f7f-178">Delete a resource group in the Azure portal:</span></span>
1. <span data-ttu-id="64f7f-179">Przejdź do klastra usługi Service Fabric, który chcesz usunąć.</span><span class="sxs-lookup"><span data-stu-id="64f7f-179">Navigate to the Service Fabric cluster you want to delete.</span></span>
2. <span data-ttu-id="64f7f-180">Kliknij nazwę **Grupy zasobów** na stronie podstawowych elementów klastra.</span><span class="sxs-lookup"><span data-stu-id="64f7f-180">Click the **Resource Group** name on the cluster essentials page.</span></span>
3. <span data-ttu-id="64f7f-181">Na stronie **Podstawowe elementy grupy zasobów** kliknij pozycję **Usuń grupę zasobów** i wykonaj instrukcje na tej stronie, aby zakończyć usuwanie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="64f7f-181">In the **Resource Group Essentials** page, click **Delete resource group** and follow the instructions on that page to complete the deletion of the resource group.</span></span>
    <span data-ttu-id="64f7f-182">![Usuwanie grupy zasobów][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="64f7f-182">![Delete the resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-to-deploy-a-secure-cluster"></a><span data-ttu-id="64f7f-183">Wdrażanie zabezpieczonego klastra przy użyciu modułu Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="64f7f-183">Use Azure Powershell to deploy a secure cluster</span></span>
1. <span data-ttu-id="64f7f-184">Pobierz na komputer [moduł Azure Powershell w wersji 4.0 lub nowszej](https://docs.microsoft.com/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="64f7f-184">Download the [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="64f7f-185">Otwórz okno programu Windows PowerShell i uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="64f7f-185">Open a Windows PowerShell window, Run the following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="64f7f-186">Powinny pojawić się dane wyjściowe podobne do następujących.</span><span class="sxs-lookup"><span data-stu-id="64f7f-186">You should see an output similar to the following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="64f7f-188">Zaloguj się do platformy Azure i wybierz subskrypcję, dla której chcesz utworzyć klaster.</span><span class="sxs-lookup"><span data-stu-id="64f7f-188">Login to Azure and Select the subscription to which you want to create the cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="64f7f-189">Uruchom następujące polecenie, aby utworzyć teraz zabezpieczony klaster.</span><span class="sxs-lookup"><span data-stu-id="64f7f-189">Run the following command to now create a secure cluster.</span></span> <span data-ttu-id="64f7f-190">Pamiętaj o dostosowaniu parametrów.</span><span class="sxs-lookup"><span data-stu-id="64f7f-190">Do not forget to customize the parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also the name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="64f7f-191">Wykonanie tego polecenia może potrwać od 10 do 30 minut. Na koniec powinny zostać wyświetlone dane wyjściowe podobne do następujących.</span><span class="sxs-lookup"><span data-stu-id="64f7f-191">The command can take anywhere from 10 minutes to 30 minutes to complete, at the end of it, you should get an output similar to the following.</span></span> <span data-ttu-id="64f7f-192">Dane wyjściowe zawierają informacje dotyczące certyfikatu, usługi KeyVault, do której został przekazany certyfikat, i folderu lokalnego, do którego został skopiowany.</span><span class="sxs-lookup"><span data-stu-id="64f7f-192">The output has information about the certificate, the KeyVault where it was uploaded to, and the local folder where the certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="64f7f-194">Skopiuj wszystkie dane wyjściowe i zapisz je w pliku tekstowym do przyszłego użycia.</span><span class="sxs-lookup"><span data-stu-id="64f7f-194">Copy the entire output and save to a text file as we need to refer to it.</span></span> <span data-ttu-id="64f7f-195">Zanotuj następujące informacje z danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="64f7f-195">Make a note of the following information from the output.</span></span> 

    - <span data-ttu-id="64f7f-196">**CertificateSavedLocalPath** : c:\mojecertyfikaty\mojklaster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="64f7f-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="64f7f-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="64f7f-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="64f7f-198">**ManagementEndpoint** : https://mojklaster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="64f7f-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="64f7f-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="64f7f-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-the-certificate-on-your-local-machine"></a><span data-ttu-id="64f7f-200">Instalowanie certyfikatu na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="64f7f-200">Install the certificate on your local machine</span></span>
  
<span data-ttu-id="64f7f-201">Aby połączyć się z klastrem, należy zainstalować certyfikat w magazynie osobistym bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="64f7f-201">To connect to the cluster, you need to install the certificate into the Personal (My) store of the current user.</span></span> 

<span data-ttu-id="64f7f-202">Uruchom następujące polecenie programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="64f7f-202">Run the following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\the name of the cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="64f7f-203">Teraz możesz przystąpić do nawiązywania połączenia z zabezpieczonym klastrem.</span><span class="sxs-lookup"><span data-stu-id="64f7f-203">You are now ready to connect to your secure cluster.</span></span>

### <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="64f7f-204">Nawiązywanie połączenia z zabezpieczonym klastrem</span><span class="sxs-lookup"><span data-stu-id="64f7f-204">Connect to a secure cluster</span></span> 

<span data-ttu-id="64f7f-205">Uruchom następujące polecenie programu PowerShell w celu nawiązania połączenia z zabezpieczonym klastrem.</span><span class="sxs-lookup"><span data-stu-id="64f7f-205">Run the following PowerShell command to connect to a secure cluster.</span></span> <span data-ttu-id="64f7f-206">Szczegóły certyfikatu muszą być zgodne z certyfikatem, który został użyty do skonfigurowania klastra.</span><span class="sxs-lookup"><span data-stu-id="64f7f-206">The certificate details must match a certificate that was used to set up the cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="64f7f-207">W poniższym przykładzie pokazano uzupełnione parametry:</span><span class="sxs-lookup"><span data-stu-id="64f7f-207">The following example shows the completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="64f7f-208">Uruchom następujące polecenie, aby sprawdzić poprawność połączenia i upewnić się, że klaster jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="64f7f-208">Run the following command to check that you are connected and the cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-to-your-cluster-from-visual-studio"></a><span data-ttu-id="64f7f-209">Publikowanie aplikacji w klastrze z poziomu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="64f7f-209">Publish your apps to your cluster from Visual Studio</span></span>

<span data-ttu-id="64f7f-210">Teraz po skonfigurowaniu klastra platformy Azure możesz opublikować w nim swoje aplikacje z poziomu programu Visual Studio. W tym celu wykonaj instrukcje zawarte w dokumencie [Publish to an cluster](service-fabric-publish-app-remote-cluster.md) (Publikowanie w klastrze).</span><span class="sxs-lookup"><span data-stu-id="64f7f-210">Now that you have set up an Azure cluster, you can publish your applications to it from Visual Studio by following the [Publish to an cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-the-cluster"></a><span data-ttu-id="64f7f-211">Usuwanie klastra</span><span class="sxs-lookup"><span data-stu-id="64f7f-211">Remove the cluster</span></span>
<span data-ttu-id="64f7f-212">Klaster składa się z innych zasobów platformy Azure poza samym zasobem klastra.</span><span class="sxs-lookup"><span data-stu-id="64f7f-212">A cluster is made up of other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="64f7f-213">Najprostszym sposobem na usunięcie klastra i wszystkich wykorzystywanych przez niego zasobów jest usunięcie grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="64f7f-213">The simplest way to delete the cluster and all the resources it consumes is to delete the resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="64f7f-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64f7f-214">Next steps</span></span>
<span data-ttu-id="64f7f-215">Teraz po skonfigurowaniu klastra programowania możesz spróbować wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="64f7f-215">Now that you have set up a development cluster, try the following:</span></span>
* [<span data-ttu-id="64f7f-216">Tworzenie zabezpieczonego klastra w portalu</span><span class="sxs-lookup"><span data-stu-id="64f7f-216">Create a secure cluster in the portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="64f7f-217">Tworzenie klastra na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="64f7f-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="64f7f-218">Wdrażanie aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="64f7f-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
