---
title: "aaaSet zapasowej autonomicznej klastra sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Utworzyć klaster autonomiczny programowanie z trzech węzłów uruchomionych na powitania tym samym komputerze. Po ukończeniu tej konfiguracji będzie gotowy toocreate klastrze z wieloma maszynami."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="60fd9-104">Tworzenie pierwszego autonomicznego klastra usługi Service Fabric</span><span class="sxs-lookup"><span data-stu-id="60fd9-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="60fd9-105">Można utworzyć klastra sieci szkieletowej usług autonomiczny żadnych maszyn wirtualnych lub komputerach z systemem Windows Server 2012 R2 lub Windows Server 2016, lokalnie lub w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="60fd9-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in hello cloud.</span></span> <span data-ttu-id="60fd9-106">Tego przewodnika Szybki Start pomaga toocreate klastra autonomiczny Programowanie w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="60fd9-106">This quickstart helps you toocreate a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="60fd9-107">Po zakończeniu na pojedynczym komputerze będzie dostępny klaster z trzema węzłami, do którego można wdrażać aplikacje.</span><span class="sxs-lookup"><span data-stu-id="60fd9-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="60fd9-108">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="60fd9-108">Before you begin</span></span>
<span data-ttu-id="60fd9-109">Usługa Service Fabric realizuje konfiguracji pakietu toocreate sieci szkieletowej usług autonomicznych klastrów.</span><span class="sxs-lookup"><span data-stu-id="60fd9-109">Service Fabric provides a setup package toocreate Service Fabric standalone clusters.</span></span>  <span data-ttu-id="60fd9-110">[Pobierz pakiet instalacyjny hello](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="60fd9-110">[Download hello setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="60fd9-111">Rozpakuj hello Instalatora tooa folderu pakietu na powitania komputer lub maszynę wirtualną których konfigurujesz hello tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="60fd9-111">Unzip hello setup package tooa folder on hello computer or virtual machine where you are setting up hello development cluster.</span></span>  <span data-ttu-id="60fd9-112">szczegółowy opis Hello zawartość pakietu instalacyjnego hello [tutaj](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="60fd9-112">hello contents of hello setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="60fd9-113">administrator klastra Hello wdrażania i konfigurowania klastra hello musi mieć uprawnienia administratora na komputerze hello.</span><span class="sxs-lookup"><span data-stu-id="60fd9-113">hello cluster administrator deploying and configuring hello cluster must have administrator privileges on hello computer.</span></span> <span data-ttu-id="60fd9-114">Usługi Service Fabric nie można zainstalować na kontrolerze domeny.</span><span class="sxs-lookup"><span data-stu-id="60fd9-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-hello-environment"></a><span data-ttu-id="60fd9-115">Sprawdź poprawność hello środowiska</span><span class="sxs-lookup"><span data-stu-id="60fd9-115">Validate hello environment</span></span>
<span data-ttu-id="60fd9-116">Witaj *TestConfiguration.ps1* skryptu w pakiecie autonomiczny hello jest używany jako najlepsze rozwiązania w zakresie analizator toovalidate czy klastra może zostać wdrożony w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="60fd9-116">hello *TestConfiguration.ps1* script in hello standalone package is used as a best practices analyzer toovalidate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="60fd9-117">[Przygotowanie do wdrożenia](service-fabric-cluster-standalone-deployment-preparation.md) list hello wymagania wstępne i wymagania środowiska.</span><span class="sxs-lookup"><span data-stu-id="60fd9-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists hello pre-requisites and environment requirements.</span></span> <span data-ttu-id="60fd9-118">Uruchom tooverify skryptu powitania po utworzeniu klastra projektowego hello:</span><span class="sxs-lookup"><span data-stu-id="60fd9-118">Run hello script tooverify if you can create hello development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a><span data-ttu-id="60fd9-119">Tworzenie klastra hello</span><span class="sxs-lookup"><span data-stu-id="60fd9-119">Create hello cluster</span></span>
<span data-ttu-id="60fd9-120">Kilka przykładowych plików konfiguracji klastra są zainstalowane z pakietu instalacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="60fd9-120">Several sample cluster configuration files are installed with hello setup package.</span></span> <span data-ttu-id="60fd9-121">*ClusterConfig.Unsecure.DevCluster.json* jest najprostsza konfiguracja klastra hello: niezabezpieczone, trzech węzłów klastra z systemem na pojedynczym komputerze.</span><span class="sxs-lookup"><span data-stu-id="60fd9-121">*ClusterConfig.Unsecure.DevCluster.json* is hello simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="60fd9-122">Inne pliki konfiguracji zawierają opis klastrów dla jednej lub wielu maszyn, zabezpieczonych za pomocą certyfikatów X.509 lub zabezpieczeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="60fd9-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="60fd9-123">Nie wymagają ustawienia konfiguracji domyślnej hello toomodify w tym samouczku, ale Przejrzyj hello pliku konfiguracji i zapoznać się z ustawieniami hello.</span><span class="sxs-lookup"><span data-stu-id="60fd9-123">You don't need toomodify any of hello default config settings for this tutorial, but look through hello config file and get familiar with hello settings.</span></span>  <span data-ttu-id="60fd9-124">Witaj **węzłów** sekcji opisano hello trzy węzły w klastrze hello: nazwa, adres IP, [typu węzła domeny błędów i domena uaktualnienia](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="60fd9-124">hello **nodes** section describes hello three nodes in hello cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="60fd9-125">Witaj **właściwości** sekcja definiuje hello [bezpieczeństwa, poziom niezawodności kolekcji diagnostyki i typy węzłów](service-fabric-cluster-manifest.md#cluster-properties) hello klastra.</span><span class="sxs-lookup"><span data-stu-id="60fd9-125">hello **properties** section defines hello [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for hello cluster.</span></span>

<span data-ttu-id="60fd9-126">Ten klaster jest niezabezpieczony.</span><span class="sxs-lookup"><span data-stu-id="60fd9-126">This cluster is unsecure.</span></span>  <span data-ttu-id="60fd9-127">Każda osoba może połączyć się z nim anonimowo i przeprowadzić operacje związane z zarządzaniem. Dlatego też klastry produkcyjne należy zawsze zabezpieczać przy użyciu certyfikatów X.509 lub zabezpieczeń systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="60fd9-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="60fd9-128">Zabezpieczeń jest skonfigurowany tylko w czasie tworzenia klastra i nie jest możliwe tooenable zabezpieczeń po utworzeniu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="60fd9-128">Security is only configured at cluster creation time and it is not possible tooenable security after hello cluster is created.</span></span>  <span data-ttu-id="60fd9-129">Odczyt [Secure klastra](service-fabric-cluster-security.md) toolearn więcej informacji na temat zabezpieczeń klastra sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="60fd9-129">Read [Secure a cluster](service-fabric-cluster-security.md) toolearn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="60fd9-130">toocreate hello programowanie trzech węzłów klastra, uruchom hello *CreateServiceFabricCluster.ps1* skryptu z sesji programu PowerShell administratora:</span><span class="sxs-lookup"><span data-stu-id="60fd9-130">toocreate hello three-node development cluster, run hello *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="60fd9-131">Pakiet środowiska uruchomieniowego platformy Service Fabric Hello jest automatycznie pobierane i instalowane w czasie tworzenia klastra.</span><span class="sxs-lookup"><span data-stu-id="60fd9-131">hello Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="60fd9-132">Połącz toohello klastra</span><span class="sxs-lookup"><span data-stu-id="60fd9-132">Connect toohello cluster</span></span>
<span data-ttu-id="60fd9-133">Klaster programowania z trzema węzłami został uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="60fd9-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="60fd9-134">Witaj modułu ServiceFabric programu PowerShell jest instalowany z hello środowiska wykonawczego.</span><span class="sxs-lookup"><span data-stu-id="60fd9-134">hello ServiceFabric PowerShell module is installed with hello runtime.</span></span>  <span data-ttu-id="60fd9-135">Można sprawdzić klastra hello jest uruchomiona z hello tym samym komputerze lub na komputerze zdalnym ze środowiskiem uruchomieniowym usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="60fd9-135">You can verify that hello cluster is running from hello same computer or from a remote computer with hello Service Fabric runtime.</span></span>  <span data-ttu-id="60fd9-136">Witaj [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) polecenia cmdlet ustanawia połączenie toohello klastra.</span><span class="sxs-lookup"><span data-stu-id="60fd9-136">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="60fd9-137">Zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md) inne przykłady łączącego tooa klastra.</span><span class="sxs-lookup"><span data-stu-id="60fd9-137">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="60fd9-138">Po łączącego toohello klastra, użyj hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay polecenia cmdlet listy węzłów w hello klastra oraz informacje o stanie dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="60fd9-138">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="60fd9-139">Element **HealthState** powinien mieć wartość *OK* dla każdego węzła.</span><span class="sxs-lookup"><span data-stu-id="60fd9-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="60fd9-140">Wizualizowanie klastra hello za pomocą Eksploratora usługi sieć szkieletowa</span><span class="sxs-lookup"><span data-stu-id="60fd9-140">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="60fd9-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) to odpowiednie narzędzie do wizualizowania klastra i zarządzania aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="60fd9-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="60fd9-142">Service Fabric Explorer to usługa, która działa w klastrze hello, otwieranego w przeglądarce za przechodząc[http://localhost: 19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="60fd9-142">Service Fabric Explorer is a service that runs in hello cluster, which you access using a browser by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="60fd9-143">pulpit nawigacyjny klastra Hello Omówienie klastra, w tym podsumowanie aplikacji i kondycji węzła.</span><span class="sxs-lookup"><span data-stu-id="60fd9-143">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="60fd9-144">Widok węzła Hello przedstawia hello fizycznego układu hello klastra.</span><span class="sxs-lookup"><span data-stu-id="60fd9-144">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="60fd9-145">Dla danego węzła można sprawdzić, które aplikacje mają kod wdrożony w tym węźle.</span><span class="sxs-lookup"><span data-stu-id="60fd9-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a><span data-ttu-id="60fd9-147">Usuń hello klastra</span><span class="sxs-lookup"><span data-stu-id="60fd9-147">Remove hello cluster</span></span>
<span data-ttu-id="60fd9-148">tooremove klastra, uruchom hello *RemoveServiceFabricCluster.ps1* skrypt programu PowerShell z folderu pakietu hello i przekazać w pliku konfiguracji JSON hello ścieżki toohello.</span><span class="sxs-lookup"><span data-stu-id="60fd9-148">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="60fd9-149">Opcjonalnie można określić lokalizację dziennika hello hello usuwania.</span><span class="sxs-lookup"><span data-stu-id="60fd9-149">You can optionally specify a location for hello log of hello deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="60fd9-150">tooremove hello środowiska uruchomieniowego platformy Service Fabric z hello komputera, uruchom hello następującego skryptu programu PowerShell z hello folderu pakietu.</span><span class="sxs-lookup"><span data-stu-id="60fd9-150">tooremove hello Service Fabric runtime from hello computer, run hello following PowerShell script from hello package folder.</span></span>

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="60fd9-151">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60fd9-151">Next steps</span></span>
<span data-ttu-id="60fd9-152">Po skonfigurowaniu klastra autonomiczny programowanie wypróbować hello następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="60fd9-152">Now that you have set up a development standalone cluster, try hello following articles:</span></span>
* <span data-ttu-id="60fd9-153">[Konfigurowanie autonomicznego klastra dla wielu maszyn](service-fabric-cluster-creation-for-windows-server.md) i włączanie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="60fd9-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="60fd9-154">Wdrażanie aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="60fd9-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
