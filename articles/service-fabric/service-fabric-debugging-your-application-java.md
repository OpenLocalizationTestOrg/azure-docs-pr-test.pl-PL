---
title: "Debugowanie aplikacji sieci szkieletowej usług Azure w programie Eclipse | Dokumentacja firmy Microsoft"
description: "Zwiększyć niezawodność i wydajność usługi poprzez opracowywania i debugowania ich w środowisku Eclipse na lokalny klaster projektowy."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: f3bcee3794de35005bd387ecfae7e6707f3cb5ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="e50db-103">Debugowanie aplikacji Java sieci szkieletowej usług za pomocą programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="e50db-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e50db-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="e50db-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="e50db-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="e50db-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="e50db-106">Uruchom lokalny klaster projektowy, wykonując kroki opisane w [konfigurowania środowiska deweloperskiego sieci szkieletowej usług](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e50db-106">Start a local development cluster by following the steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="e50db-107">Zaktualizuj entryPoint.sh usługi, którą chcesz debugować, tak aby był uruchamiany z parametrami zdalnego debugowania procesu java.</span><span class="sxs-lookup"><span data-stu-id="e50db-107">Update entryPoint.sh of the service you wish to debug, so that it starts the java process with remote debug parameters.</span></span> <span data-ttu-id="e50db-108">Ten plik znajduje się w następującej lokalizacji: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="e50db-108">This file can be found at the following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="e50db-109">Port 8001 jest ustawiony do debugowania w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="e50db-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="e50db-110">Zaktualizuj Manifest aplikacji, ustawiając liczbę wystąpień lub liczby replik dla usługi, która jest debugowany 1.</span><span class="sxs-lookup"><span data-stu-id="e50db-110">Update the Application Manifest by setting the instance count or the replica count for the service that is being debugged to 1.</span></span> <span data-ttu-id="e50db-111">To ustawienie pozwala uniknąć konfliktów port, który jest używany do debugowania.</span><span class="sxs-lookup"><span data-stu-id="e50db-111">This setting avoids conflicts for the port that is used for debugging.</span></span> <span data-ttu-id="e50db-112">Na przykład w przypadku usług bezstanowych ustawić ``InstanceCount="1"`` i dla stanowych usług zestawu docelowego i min zestawu replik rozmiary 1 w następujący sposób: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="e50db-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set the target and min replica set sizes to 1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="e50db-113">Wdrażanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e50db-113">Deploy the application.</span></span>

5. <span data-ttu-id="e50db-114">W środowisku IDE programu Eclipse wybierz **Uruchom -> debugowanie konfiguracji -> zdalnego aplikacji Java i wprowadź właściwości połączenia** i ustaw właściwości w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e50db-114">In the Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set the properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="e50db-115">Ustaw punkty przerwania w punktach żądaną i debugowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e50db-115">Set breakpoints at desired points and debug the application.</span></span>

<span data-ttu-id="e50db-116">Jeśli awarii aplikacji można również włączyć coredumps.</span><span class="sxs-lookup"><span data-stu-id="e50db-116">If the application is crashing, you may also want to enable coredumps.</span></span> <span data-ttu-id="e50db-117">Wykonanie ``ulimit -c`` w powłoce i zwraca 0, a następnie coredumps nie są włączone.</span><span class="sxs-lookup"><span data-stu-id="e50db-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="e50db-118">Aby włączyć nieograniczone coredumps, uruchom następujące polecenie: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="e50db-118">To enable unlimited coredumps, execute the following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="e50db-119">Można również sprawdzić stan za pomocą polecenia ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="e50db-119">You can also verify the status using the command ``ulimit -a``.</span></span>  <span data-ttu-id="e50db-120">Jeśli chcesz zaktualizować ścieżkę generowania coredump wykonania ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="e50db-120">If you wanted to update the coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="e50db-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e50db-121">Next steps</span></span>

* <span data-ttu-id="e50db-122">[Zbieranie dzienników przy użyciu diagnostyki Azure Linux](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="e50db-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="e50db-123">[Monitorowanie i diagnozowania usług lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e50db-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
