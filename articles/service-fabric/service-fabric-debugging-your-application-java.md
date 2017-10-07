---
title: "aaaDebug aplikację usługi Azure Service Fabric w środowisku Eclipse | Dokumentacja firmy Microsoft"
description: "Zwiększyć hello niezawodność i wydajność usług przez opracowywania i debugowania ich w środowisku Eclipse na lokalny klaster projektowy."
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
ms.openlocfilehash: ab86254a5c312db40fd631746c89aab0bbb9d1a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-java-service-fabric-application-using-eclipse"></a><span data-ttu-id="cab5c-103">Debugowanie aplikacji Java sieci szkieletowej usług za pomocą programu Eclipse</span><span class="sxs-lookup"><span data-stu-id="cab5c-103">Debug your Java Service Fabric application using Eclipse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cab5c-104">Visual Studio/CSharp</span><span class="sxs-lookup"><span data-stu-id="cab5c-104">Visual Studio/CSharp</span></span>](service-fabric-debugging-your-application.md) 
> * [<span data-ttu-id="cab5c-105">Eclipse/Java</span><span class="sxs-lookup"><span data-stu-id="cab5c-105">Eclipse/Java</span></span>](service-fabric-debugging-your-application-java.md)
> 

1. <span data-ttu-id="cab5c-106">Uruchom lokalnego klastra projektowego, wykonując kroki hello w [konfigurowania środowiska deweloperskiego sieci szkieletowej usług](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cab5c-106">Start a local development cluster by following hello steps in [Setting up your Service Fabric development environment](service-fabric-get-started-linux.md).</span></span>

2. <span data-ttu-id="cab5c-107">Zaktualizuj entryPoint.sh hello usługi ma toodebug, tak aby był uruchamiany z parametrami zdalnego debugowania procesu java hello.</span><span class="sxs-lookup"><span data-stu-id="cab5c-107">Update entryPoint.sh of hello service you wish toodebug, so that it starts hello java process with remote debug parameters.</span></span> <span data-ttu-id="cab5c-108">Ten plik znajduje się w następującej lokalizacji hello: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span><span class="sxs-lookup"><span data-stu-id="cab5c-108">This file can be found at hello following location: ``ApplicationName\ServiceNamePkg\Code\entrypoint.sh``.</span></span> <span data-ttu-id="cab5c-109">Port 8001 jest ustawiony do debugowania w tym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="cab5c-109">Port 8001 is set for debugging in this example.</span></span>

    ```sh
    java -Xdebug -Xrunjdwp:transport=dt_socket,address=8001,server=y,suspend=y -Djava.library.path=$LD_LIBRARY_PATH -jar myapp.jar
    ```
3. <span data-ttu-id="cab5c-110">Zaktualizuj Manifest aplikacji hello ustawiając hello liczbę wystąpień lub hello liczbie repliki usługi hello, który jest debugowany too1.</span><span class="sxs-lookup"><span data-stu-id="cab5c-110">Update hello Application Manifest by setting hello instance count or hello replica count for hello service that is being debugged too1.</span></span> <span data-ttu-id="cab5c-111">To ustawienie pozwala uniknąć konfliktów hello port używany do debugowania.</span><span class="sxs-lookup"><span data-stu-id="cab5c-111">This setting avoids conflicts for hello port that is used for debugging.</span></span> <span data-ttu-id="cab5c-112">Na przykład w przypadku usług bezstanowych ustawić ``InstanceCount="1"`` i usługi stanowej hello zestaw docelowy i min repliki Ustaw rozmiary too1 w następujący sposób: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span><span class="sxs-lookup"><span data-stu-id="cab5c-112">For example, for stateless services, set ``InstanceCount="1"`` and for stateful services set hello target and min replica set sizes too1 as follows: `` TargetReplicaSetSize="1" MinReplicaSetSize="1"``.</span></span>

4. <span data-ttu-id="cab5c-113">Wdrażanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cab5c-113">Deploy hello application.</span></span>

5. <span data-ttu-id="cab5c-114">Hello Eclipse IDE, wybierz **Uruchom -> debugowanie konfiguracji -> zdalnego aplikacji Java i wprowadź właściwości połączenia** i ustaw właściwości hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="cab5c-114">In hello Eclipse IDE, select **Run -> Debug Configurations -> Remote Java Application and input connection properties** and set hello properties as follows:</span></span>

   ```
   Host: ipaddress
   Port: 8001
   ```
6.  <span data-ttu-id="cab5c-115">Ustaw punkty przerwania w punktach żądaną i debugowanie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cab5c-115">Set breakpoints at desired points and debug hello application.</span></span>

<span data-ttu-id="cab5c-116">Jeśli aplikacja hello uległa awarii, również można tooenable coredumps.</span><span class="sxs-lookup"><span data-stu-id="cab5c-116">If hello application is crashing, you may also want tooenable coredumps.</span></span> <span data-ttu-id="cab5c-117">Wykonanie ``ulimit -c`` w powłoce i zwraca 0, a następnie coredumps nie są włączone.</span><span class="sxs-lookup"><span data-stu-id="cab5c-117">Execute ``ulimit -c`` in a shell and if it returns 0, then coredumps are not enabled.</span></span> <span data-ttu-id="cab5c-118">tooenable nieograniczone coredumps wykonania hello następującego polecenia: ``ulimit -c unlimited``.</span><span class="sxs-lookup"><span data-stu-id="cab5c-118">tooenable unlimited coredumps, execute hello following command: ``ulimit -c unlimited``.</span></span> <span data-ttu-id="cab5c-119">Można również sprawdzić stan hello za pomocą polecenia hello ``ulimit -a``.</span><span class="sxs-lookup"><span data-stu-id="cab5c-119">You can also verify hello status using hello command ``ulimit -a``.</span></span>  <span data-ttu-id="cab5c-120">Jeśli potrzebujesz tooupdate hello coredump generowania ścieżka wykonywania ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span><span class="sxs-lookup"><span data-stu-id="cab5c-120">If you wanted tooupdate hello coredump generation path, execute ``echo '/tmp/core_%e.%p' | sudo tee /proc/sys/kernel/core_pattern``.</span></span> 

### <a name="next-steps"></a><span data-ttu-id="cab5c-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cab5c-121">Next steps</span></span>

* <span data-ttu-id="cab5c-122">[Zbieranie dzienników przy użyciu diagnostyki Azure Linux](service-fabric-diagnostics-how-to-setup-lad.md).</span><span class="sxs-lookup"><span data-stu-id="cab5c-122">[Collect logs using Linux Azure Diagnostics](service-fabric-diagnostics-how-to-setup-lad.md).</span></span>
* <span data-ttu-id="cab5c-123">[Monitorowanie i diagnozowania usług lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cab5c-123">[Monitor and diagnose services locally](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md).</span></span>
