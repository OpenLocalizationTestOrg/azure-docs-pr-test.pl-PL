---
title: "Rozwiązywanie problemów z ustawienia lokalnego klastra usługi sieć szkieletowa | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano zestaw sugestie dotyczące rozwiązywania problemów z lokalnego klastra projektowego"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: aa393f884b564cee81fcf75cc2eff895efea9471
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="b4647-103">Rozwiązywanie problemów z konfiguracji klastra lokalnego rozwoju</span><span class="sxs-lookup"><span data-stu-id="b4647-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="b4647-104">Jeśli napotkasz problem podczas interakcji z lokalnym klastrem programowanie sieć szkieletowa usług Azure, przejrzyj poniższe sugestie potencjalnych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="b4647-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review the following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="b4647-105">Błędy instalacji klastra</span><span class="sxs-lookup"><span data-stu-id="b4647-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="b4647-106">Nie można wyczyścić dzienniki sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="b4647-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="b4647-107">Problem</span><span class="sxs-lookup"><span data-stu-id="b4647-107">Problem</span></span>
<span data-ttu-id="b4647-108">Podczas uruchamiania skryptu DevClusterSetup, zostanie wyświetlony błąd w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b4647-108">While running the DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held to items in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="b4647-109">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="b4647-109">Solution</span></span>
<span data-ttu-id="b4647-110">Zamknij bieżące okno programu PowerShell i otworzyć nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b4647-110">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="b4647-111">Teraz można pomyślnie uruchomić skryptu.</span><span class="sxs-lookup"><span data-stu-id="b4647-111">You should now be able to successfully run the script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="b4647-112">Liczba błędów połączenia klastra</span><span class="sxs-lookup"><span data-stu-id="b4647-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="b4647-113">Polecenia cmdlet programu PowerShell usługi Service Fabric nie są rozpoznawane w programie Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4647-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="b4647-114">Problem</span><span class="sxs-lookup"><span data-stu-id="b4647-114">Problem</span></span>
<span data-ttu-id="b4647-115">Jeśli zostanie podjęta próba uruchomienia dowolnych poleceniach cmdlet programu PowerShell usługi Service Fabric, takich jak `Connect-ServiceFabricCluster` w oknie programu PowerShell usługi Azure jej nie powiedzie się, informujący o tym, że polecenie cmdlet nie została rozpoznana.</span><span class="sxs-lookup"><span data-stu-id="b4647-115">If you try to run any of the Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that the cmdlet is not recognized.</span></span> <span data-ttu-id="b4647-116">Przyczyną jest używany 32-bitowej wersji środowiska Windows PowerShell (nawet na 64-bitowe wersje systemu operacyjnego), programu Azure PowerShell poleceń cmdlet usługi sieć szkieletowa tylko pracy w środowiskach 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="b4647-116">The reason for this is that Azure PowerShell uses the 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas the Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="b4647-117">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="b4647-117">Solution</span></span>
<span data-ttu-id="b4647-118">Zawsze uruchamiaj polecenia cmdlet usługi sieć szkieletowa bezpośrednio z programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b4647-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="b4647-119">Najnowszą wersję programu Azure PowerShell nie tworzy specjalne skrót, więc nie powinno to nastąpić.</span><span class="sxs-lookup"><span data-stu-id="b4647-119">The latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="b4647-120">Wyjątek inicjowania typu</span><span class="sxs-lookup"><span data-stu-id="b4647-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="b4647-121">Problem</span><span class="sxs-lookup"><span data-stu-id="b4647-121">Problem</span></span>
<span data-ttu-id="b4647-122">Podczas łączenia z klastrem w programie PowerShell zostanie wyświetlony błąd typeinitializationexception — System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="b4647-122">When you are connecting to the cluster in PowerShell, you see the error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="b4647-123">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="b4647-123">Solution</span></span>
<span data-ttu-id="b4647-124">Podczas instalacji nie ustawiono poprawnie zmiennej path.</span><span class="sxs-lookup"><span data-stu-id="b4647-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="b4647-125">Wyloguj się z systemem Windows i zaloguj się ponownie.</span><span class="sxs-lookup"><span data-stu-id="b4647-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="b4647-126">Spowoduje to odświeżenie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="b4647-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="b4647-127">Połączenia klastra kończy się niepowodzeniem z "Obiekt jest zamknięty"</span><span class="sxs-lookup"><span data-stu-id="b4647-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="b4647-128">Problem</span><span class="sxs-lookup"><span data-stu-id="b4647-128">Problem</span></span>
<span data-ttu-id="b4647-129">Wywołanie Connect-ServiceFabricCluster zakończy się niepowodzeniem z powodu błędu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="b4647-129">A call to Connect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : The object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="b4647-130">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="b4647-130">Solution</span></span>
<span data-ttu-id="b4647-131">Zamknij bieżące okno programu PowerShell i otworzyć nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b4647-131">Close the current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="b4647-132">Teraz można nawiązywać połączeń.</span><span class="sxs-lookup"><span data-stu-id="b4647-132">You should now be able to successfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="b4647-133">Wyjątek odmowa połączenia sieci szkieletowej</span><span class="sxs-lookup"><span data-stu-id="b4647-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="b4647-134">Problem</span><span class="sxs-lookup"><span data-stu-id="b4647-134">Problem</span></span>
<span data-ttu-id="b4647-135">Podczas debugowania w programie Visual Studio, otrzymasz komunikat o błędzie FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="b4647-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="b4647-136">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="b4647-136">Solution</span></span>
<span data-ttu-id="b4647-137">Ten błąd występuje zazwyczaj, gdy użytkownik próbuje uruchomić proces hosta usługi ręcznie, zamiast stosowanie środowiska uruchomieniowego platformy Service Fabric ją uruchomić za.</span><span class="sxs-lookup"><span data-stu-id="b4647-137">This error usually occurs when you try to start a service host process manually, rather than allowing the Service Fabric runtime to start it for you.</span></span>

<span data-ttu-id="b4647-138">Upewnij się, że nie masz żadnych projektów usług Ustaw jako projekty startowe w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="b4647-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="b4647-139">Tylko projekty aplikacji sieci szkieletowej usług powinna być ustawiona jako projekty startowe.</span><span class="sxs-lookup"><span data-stu-id="b4647-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="b4647-140">Jeśli po zakończeniu instalacji, lokalnego klastra zaczyna działać nieprawidłowo, można zresetować go przy użyciu aplikacji na pasku zadań systemu Menedżera klastra lokalnego.</span><span class="sxs-lookup"><span data-stu-id="b4647-140">If, following setup, your local cluster begins to behave abnormally, you can reset it using the local cluster manager system tray application.</span></span> <span data-ttu-id="b4647-141">Spowoduje to usunięcie istniejącego klastra i skonfigurować nowy.</span><span class="sxs-lookup"><span data-stu-id="b4647-141">This removes the existing cluster and set up a new one.</span></span> <span data-ttu-id="b4647-142">Należy pamiętać, że wszystkie wdrożone aplikacje i skojarzone dane zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="b4647-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b4647-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4647-143">Next steps</span></span>
* [<span data-ttu-id="b4647-144">Omówienie i rozwiązywanie problemów klastra za pomocą raportów o kondycji systemu</span><span class="sxs-lookup"><span data-stu-id="b4647-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="b4647-145">Wizualizowanie klastra przy użyciu narzędzia Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="b4647-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

