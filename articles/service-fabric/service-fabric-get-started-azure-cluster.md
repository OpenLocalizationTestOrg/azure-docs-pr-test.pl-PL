---
title: "aaaSet zapasowej klastra usługi sieć szkieletowa usług Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="78e1f-103">Tworzenie pierwszego klastra usługi Service Fabric na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="78e1f-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="78e1f-104">[Klaster usługi Service Fabric](service-fabric-deploy-anywhere.md) jest połączonym z siecią zestawem maszyn wirtualnych lub fizycznych, w którym wdraża się mikrousługi i nimi zarządza.</span><span class="sxs-lookup"><span data-stu-id="78e1f-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="78e1f-105">Ta opcja szybkiego startu pomaga toocreate pięcioma węzłami klastra, systemem Windows lub Linux, za pośrednictwem hello [programu Azure PowerShell](https://msdn.microsoft.com/library/dn135248) lub [portalu Azure](http://portal.azure.com) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="78e1f-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="78e1f-106">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="78e1f-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="78e1f-107">Użyj hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="78e1f-107">Use hello Azure portal</span></span>

<span data-ttu-id="78e1f-108">Zaloguj się za toohello portalu Azure w [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78e1f-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="78e1f-109">Tworzenie klastra hello</span><span class="sxs-lookup"><span data-stu-id="78e1f-109">Create hello cluster</span></span>

1. <span data-ttu-id="78e1f-110">Kliknij przycisk hello **nowy** znaleziono przycisku na powitania lewym górnym rogu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="78e1f-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="78e1f-111">Wybierz **obliczeniowe** z hello **nowy** bloku, a następnie wybierz **klastra sieci szkieletowej usług** z hello **obliczeniowe** bloku.</span><span class="sxs-lookup"><span data-stu-id="78e1f-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="78e1f-112">Wypełnianie hello sieci szkieletowej usług **podstawy** formularza.</span><span class="sxs-lookup"><span data-stu-id="78e1f-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="78e1f-113">Dla **systemu operacyjnego**, wybierz pozycję hello wersji systemu Windows lub Linux ma hello toorun węzłów klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="78e1f-114">Hello nazwy użytkownika i hasła wprowadzonego w tym miejscu jest używane toolog toohello maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="78e1f-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="78e1f-115">W obszarze **Grupa zasobów** utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="78e1f-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="78e1f-116">Grupa zasobów to logiczny kontener, w którym są tworzone i zbiorczo zarządzane zasoby platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="78e1f-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="78e1f-117">Po zakończeniu kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78e1f-117">When complete, click **OK**.</span></span>

    ![Dane wyjściowe instalacji klastra][cluster-setup-basics]

4. <span data-ttu-id="78e1f-119">Wypełnianie hello **konfiguracji klastra** formularza.</span><span class="sxs-lookup"><span data-stu-id="78e1f-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="78e1f-120">Dla ustawienia **Liczba typów węzłów** wprowadź wartość „1”.</span><span class="sxs-lookup"><span data-stu-id="78e1f-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="78e1f-121">Wybierz **typu węzła 1 (podstawowe)** i wypełnianie hello **konfiguracji typu węzła** formularza.</span><span class="sxs-lookup"><span data-stu-id="78e1f-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="78e1f-122">Wprowadź nazwę typu węzła i ustaw hello [warstwa trwałości](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) zbyt "brązową."</span><span class="sxs-lookup"><span data-stu-id="78e1f-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="78e1f-123">Wybierz rozmiar maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="78e1f-123">Select a VM size.</span></span>

    <span data-ttu-id="78e1f-124">Typy węzłów zdefiniuj hello rozmiar maszyny Wirtualnej, liczbę maszyn wirtualnych, niestandardowe punkty końcowe, oraz inne ustawienia hello maszyny wirtualne tego typu.</span><span class="sxs-lookup"><span data-stu-id="78e1f-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="78e1f-125">Każdy typ węzła zdefiniowany jest skonfigurowany jako zestaw skali oddzielnej maszynie wirtualnej, który jest zarządzanych maszyn wirtualnych i toodeploy używane jako zestaw.</span><span class="sxs-lookup"><span data-stu-id="78e1f-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="78e1f-126">Każdy typ węzła może być niezależnie skalowany w górę lub w dół, może mieć różne zestawy otwartych portów i może mieć różne metryki pojemności.</span><span class="sxs-lookup"><span data-stu-id="78e1f-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="78e1f-127">Hello pierwszy lub podstawowego, typ węzła jest którym usługi sieć szkieletowa usług systemowych są obsługiwane i musi mieć co najmniej pięć maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="78e1f-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="78e1f-128">W przypadku wszystkich wdrożeń produkcyjnych [planowanie pojemności](service-fabric-cluster-capacity.md) jest ważnym krokiem.</span><span class="sxs-lookup"><span data-stu-id="78e1f-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="78e1f-129">Niemniej w ramach tego przewodnika Szybki start nie uruchamiasz aplikacji, więc wybierz rozmiar maszyny wirtualnej *Standardowa DS1_v2*.</span><span class="sxs-lookup"><span data-stu-id="78e1f-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="78e1f-130">Wybierz "Srebrna" hello [warstwa niezawodności](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) i pojemność wynoszącą 5 zestawu skalowania maszyny wirtualnej początkowej.</span><span class="sxs-lookup"><span data-stu-id="78e1f-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="78e1f-131">Niestandardowe punkty końcowe otwarcie portów w usłudze równoważenia obciążenia Azure hello, dzięki czemu można połączyć z aplikacji działających na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="78e1f-132">Wprowadź "80, 8172" tooopen się porty 80 i 8172.</span><span class="sxs-lookup"><span data-stu-id="78e1f-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="78e1f-133">Nie sprawdzaj hello **Skonfiguruj ustawienia zaawansowane** okno, który służy do dostosowywania końcowych zarządzania TCP/HTTP, zakresy portów aplikacji, [ograniczenia umieszczania](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), i [pojemności właściwości](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="78e1f-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="78e1f-134">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78e1f-134">Select **OK**.</span></span>

6. <span data-ttu-id="78e1f-135">W hello **konfiguracji klastra** formularza, ustaw **diagnostyki** za**na**.</span><span class="sxs-lookup"><span data-stu-id="78e1f-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="78e1f-136">Dla tego przewodnika Szybki Start, nie trzeba tooenter any [sieci szkieletowej ustawienie](service-fabric-cluster-fabric-settings.md) właściwości.</span><span class="sxs-lookup"><span data-stu-id="78e1f-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="78e1f-137">W **wersja platformy Fabric**, wybierz pozycję **automatyczne** tryb uaktualniania, tak aby firma Microsoft automatycznie aktualizuje hello wersja kodu sieci szkieletowej hello uruchomionego hello klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="78e1f-138">Ustaw tryb hello zbyt**ręcznego** Jeśli zbyt[Wybierz obsługiwaną wersję](service-fabric-cluster-upgrade.md) tooupgrade do.</span><span class="sxs-lookup"><span data-stu-id="78e1f-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![Konfiguracja typu węzła][node-type-config]

    <span data-ttu-id="78e1f-140">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78e1f-140">Select **OK**.</span></span>

7. <span data-ttu-id="78e1f-141">Wypełnianie hello **zabezpieczeń** formularza.</span><span class="sxs-lookup"><span data-stu-id="78e1f-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="78e1f-142">W ramach tego przewodnika Szybki start wybierz opcję **Niezabezpieczony**.</span><span class="sxs-lookup"><span data-stu-id="78e1f-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="78e1f-143">Jest zdecydowanie zalecane toocreate bezpiecznego klastra w przypadku obciążeń produkcyjnych, jednak ponieważ każdy anonimowo połączyć tooan niezabezpieczone klaster i wykonywać operacje zarządzania.</span><span class="sxs-lookup"><span data-stu-id="78e1f-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="78e1f-144">Certyfikaty są używane w sieci szkieletowej usług tooprovide uwierzytelnianie i szyfrowanie toosecure różnych aspektów klastra i jego zastosowań.</span><span class="sxs-lookup"><span data-stu-id="78e1f-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="78e1f-145">Aby uzyskać więcej informacji o sposobie wykorzystania certyfikatów w usłudze Service Fabric, zobacz [Scenariusze zabezpieczeń klastra usługi Service Fabric](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="78e1f-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="78e1f-146">Uwierzytelnianie użytkownika tooenable za pomocą usługi Azure Active Directory lub tooset zapasowych certyfikatów zabezpieczeń aplikacji [Tworzenie klastra z szablonem usługi Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="78e1f-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="78e1f-147">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="78e1f-147">Select **OK**.</span></span>

8. <span data-ttu-id="78e1f-148">Witaj Przejrzyj podsumowania.</span><span class="sxs-lookup"><span data-stu-id="78e1f-148">Review hello summary.</span></span>  <span data-ttu-id="78e1f-149">Jeśli chcesz toodownload szablonem usługi Resource Manager zbudowane na podstawie ustawień hello wprowadzona, wybierz **Pobierz szablon i parametry**.</span><span class="sxs-lookup"><span data-stu-id="78e1f-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="78e1f-150">Wybierz **Utwórz** toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="78e1f-151">Postęp tworzenia hello w powiadomieniach hello jest widoczny.</span><span class="sxs-lookup"><span data-stu-id="78e1f-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="78e1f-152">(Kliknij ikonę dzwonka"hello" w pobliżu pasek stanu hello na powitania górnym rogu ekranu). Jeśli kliknięto **tooStartboard numeru Pin** podczas tworzenia klastra hello, zobacz **wdrażanie klastra sieci szkieletowej usług** przypięty toohello **Start** tablicy.</span><span class="sxs-lookup"><span data-stu-id="78e1f-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="78e1f-153">Wyświetlanie stanu klastra</span><span class="sxs-lookup"><span data-stu-id="78e1f-153">View cluster status</span></span>
<span data-ttu-id="78e1f-154">Po utworzeniu klastra można sprawdzić klastra w hello **omówienie** bloku w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="78e1f-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="78e1f-155">Możesz teraz przeglądać szczegóły hello klastra na pulpicie nawigacyjnym hello, w tym klastrze hello publiczny punkt końcowy i tooService łącze Eksploratora sieci szkieletowej.</span><span class="sxs-lookup"><span data-stu-id="78e1f-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![Stan klastra][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="78e1f-157">Wizualizowanie klastra hello za pomocą Eksploratora usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="78e1f-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="78e1f-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) to odpowiednie narzędzie do wizualizowania klastra i zarządzania aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="78e1f-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="78e1f-159">Service Fabric Explorer to usługa, która działa w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="78e1f-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="78e1f-160">Dostęp za pomocą przeglądarki sieci web, klikając hello **Service Fabric Explorer** łącze klastra hello **omówienie** w portalu hello na stronie.</span><span class="sxs-lookup"><span data-stu-id="78e1f-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="78e1f-161">Można również wprowadzić adres hello bezpośrednio w przeglądarce hello: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="78e1f-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="78e1f-162">pulpit nawigacyjny klastra Hello Omówienie klastra, w tym podsumowanie aplikacji i kondycji węzła.</span><span class="sxs-lookup"><span data-stu-id="78e1f-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="78e1f-163">Widok węzła Hello przedstawia hello fizycznego układu hello klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="78e1f-164">Dla danego węzła można sprawdzić, które aplikacje mają kod wdrożony w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="78e1f-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="78e1f-166">Połącz toohello klastra przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="78e1f-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="78e1f-167">Sprawdź, czy w tym klastrze hello jest uruchomiona, nawiązując połączenie za pomocą programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78e1f-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="78e1f-168">Witaj modułu ServiceFabric programu PowerShell jest instalowany z hello [zestawu SDK usług sieci szkieletowej](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="78e1f-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="78e1f-169">Witaj [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet ustanawia połączenie toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="78e1f-170">Zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md) inne przykłady łączącego tooa klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="78e1f-171">Po łączącego toohello klastra, użyj hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay polecenia cmdlet listy węzłów w hello klastra oraz informacje o stanie dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="78e1f-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="78e1f-172">Element **HealthState** powinien mieć wartość *OK* dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="78e1f-172">**HealthState** should be *OK* for each node.</span></span>

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

### <a name="remove-hello-cluster"></a><span data-ttu-id="78e1f-173">Usuń hello klastra</span><span class="sxs-lookup"><span data-stu-id="78e1f-173">Remove hello cluster</span></span>
<span data-ttu-id="78e1f-174">Klastra usługi sieć szkieletowa składa się z innych zasobów platformy Azure oprócz zasobu klastra toohello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="78e1f-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="78e1f-175">Dlatego toocompletely Usuwanie klastra sieci szkieletowej usług należy również toodelete hello wszystkie zasoby, które składa się z.</span><span class="sxs-lookup"><span data-stu-id="78e1f-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="78e1f-176">Hello najprostszy sposób toodelete hello klaster i wszystkie zużywanych zasobach hello jest grupa zasobów hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="78e1f-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="78e1f-177">Dla innych toodelete sposoby klaster lub toodelete zasobów hello niektóre (ale nie wszystkie) w grupie zasobów, zobacz [usunąć klaster](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="78e1f-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="78e1f-178">Usuń grupę zasobów w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="78e1f-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="78e1f-179">Przejdź toohello klastra sieci szkieletowej usług ma toodelete.</span><span class="sxs-lookup"><span data-stu-id="78e1f-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="78e1f-180">Kliknij przycisk hello **grupy zasobów** nazwa strony essentials hello klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="78e1f-181">W hello **Essentials grupy zasobów** kliknij przycisk **Usuń grupę zasobów** i wykonać instrukcje hello usunięcie hello toocomplete strony tego hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="78e1f-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="78e1f-182">![Usuń grupę zasobów hello][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="78e1f-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="78e1f-183">Użyj programu Azure Powershell toodeploy bezpiecznego klastra</span><span class="sxs-lookup"><span data-stu-id="78e1f-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="78e1f-184">Pobierz hello [programu Azure Powershell modułu w wersji 4.0 lub nowszej](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="78e1f-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="78e1f-185">Otwórz okno programu Windows PowerShell, hello uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="78e1f-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="78e1f-186">Powinny zostać wyświetlone następujące dane wyjściowe podobne toohello.</span><span class="sxs-lookup"><span data-stu-id="78e1f-186">You should see an output similar toohello following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="78e1f-188">TooAzure logowania i wybierz hello toowhich subskrypcji ma toocreate hello klastra</span><span class="sxs-lookup"><span data-stu-id="78e1f-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="78e1f-189">Hello uruchom następujące polecenie toonow tworzenia bezpiecznego klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="78e1f-190">Nie zapomnij toocustomize hello parametrów.</span><span class="sxs-lookup"><span data-stu-id="78e1f-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="78e1f-191">polecenie Hello może potrwać od 10 minut too30 minut toocomplete na końcu hello go, należy pobrać następujące dane wyjściowe podobne toohello.</span><span class="sxs-lookup"><span data-stu-id="78e1f-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="78e1f-192">dane wyjściowe Hello zawiera informacje o certyfikacie hello, hello KeyVault, w którym został przekazany, i hello folder lokalny, w którym certyfikat hello jest kopiowany.</span><span class="sxs-lookup"><span data-stu-id="78e1f-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="78e1f-194">Kopiuj dane wyjściowe całego hello i Zapisz plik tekstowy tooa jako potrzebujemy toorefer tooit.</span><span class="sxs-lookup"><span data-stu-id="78e1f-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="78e1f-195">Zanotuj hello następujących informacji w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="78e1f-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="78e1f-196">**CertificateSavedLocalPath** : c:\mojecertyfikaty\mojklaster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="78e1f-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="78e1f-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="78e1f-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="78e1f-198">**ManagementEndpoint** : https://mojklaster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="78e1f-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="78e1f-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="78e1f-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="78e1f-200">Zainstaluj certyfikat hello na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="78e1f-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="78e1f-201">tooconnect toohello klastra, potrzebujesz tooinstall hello certyfikatu do magazynu osobistego (Mój) hello hello bieżącego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="78e1f-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="78e1f-202">Uruchom hello następującego środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="78e1f-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="78e1f-203">Wszystko jest teraz gotowy tooconnect tooyour bezpiecznego klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="78e1f-204">Połącz tooa bezpiecznego klastra</span><span class="sxs-lookup"><span data-stu-id="78e1f-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="78e1f-205">Uruchom powitania po klastra bezpiecznego tooa tooconnect polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="78e1f-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="78e1f-206">Szczegóły certyfikatu Hello musi odpowiadać certyfikatu, który był używany tooset zapasowej hello klastra.</span><span class="sxs-lookup"><span data-stu-id="78e1f-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="78e1f-207">powitania po hello przedstawiono przykład ukończone parametry:</span><span class="sxs-lookup"><span data-stu-id="78e1f-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="78e1f-208">Uruchom hello następujące polecenia toocheck, że komputer jest połączony i hello klastra jest w dobrej kondycji.</span><span class="sxs-lookup"><span data-stu-id="78e1f-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="78e1f-209">Publikowanie aplikacji tooyour klastra w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="78e1f-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="78e1f-210">Teraz, gdy zdefiniowano klastra platformy Azure możesz opublikować tooit Twojej aplikacji w programie Visual Studio przez następujące hello [klastra tooan publikowania](service-fabric-publish-app-remote-cluster.md) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="78e1f-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="78e1f-211">Usuń hello klastra</span><span class="sxs-lookup"><span data-stu-id="78e1f-211">Remove hello cluster</span></span>
<span data-ttu-id="78e1f-212">Klaster składa się z innych zasobów platformy Azure oprócz zasobu klastra toohello samej siebie.</span><span class="sxs-lookup"><span data-stu-id="78e1f-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="78e1f-213">Hello najprostszy sposób toodelete hello klaster i wszystkie zużywanych zasobach hello jest grupa zasobów hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="78e1f-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="78e1f-214">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="78e1f-214">Next steps</span></span>
<span data-ttu-id="78e1f-215">Po skonfigurowaniu klastra projektowego wypróbować hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="78e1f-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="78e1f-216">Tworzenie bezpiecznej klastra w portalu hello</span><span class="sxs-lookup"><span data-stu-id="78e1f-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="78e1f-217">Tworzenie klastra na podstawie szablonu</span><span class="sxs-lookup"><span data-stu-id="78e1f-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="78e1f-218">Wdrażanie aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="78e1f-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
