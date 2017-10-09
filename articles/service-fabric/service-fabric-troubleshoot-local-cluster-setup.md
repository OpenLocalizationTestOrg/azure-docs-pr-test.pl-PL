---
title: "aaaTroubleshoot ustawienia lokalnego klastra usługi sieć szkieletowa | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="91e56-103">Rozwiązywanie problemów z konfiguracji klastra lokalnego rozwoju</span><span class="sxs-lookup"><span data-stu-id="91e56-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="91e56-104">Jeśli napotkasz problem podczas interakcji z lokalnym klastrem programowanie sieć szkieletowa usług Azure, przejrzyj powitania po sugestie dotyczące potencjalne rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="91e56-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="91e56-105">Błędy instalacji klastra</span><span class="sxs-lookup"><span data-stu-id="91e56-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="91e56-106">Nie można wyczyścić dzienniki sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="91e56-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="91e56-107">Problem</span><span class="sxs-lookup"><span data-stu-id="91e56-107">Problem</span></span>
<span data-ttu-id="91e56-108">Podczas uruchamiania skryptu DevClusterSetup hello, zostanie wyświetlony błąd w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="91e56-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="91e56-109">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="91e56-109">Solution</span></span>
<span data-ttu-id="91e56-110">Zamknij bieżące okno programu PowerShell hello i otworzyć nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="91e56-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="91e56-111">Teraz powinno być możliwe toosuccessfully Uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="91e56-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="91e56-112">Liczba błędów połączenia klastra</span><span class="sxs-lookup"><span data-stu-id="91e56-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="91e56-113">Polecenia cmdlet programu PowerShell usługi Service Fabric nie są rozpoznawane w programie Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="91e56-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="91e56-114">Problem</span><span class="sxs-lookup"><span data-stu-id="91e56-114">Problem</span></span>
<span data-ttu-id="91e56-115">Jeśli spróbujesz toorun żadnego hello poleceń cmdlet programu PowerShell usługi Service Fabric, takich jak `Connect-ServiceFabricCluster` w oknie programu PowerShell usługi Azure jej nie powiedzie się, informujący o tym, to polecenie cmdlet hello nie został rozpoznany.</span><span class="sxs-lookup"><span data-stu-id="91e56-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="91e56-116">Witaj przyczyną tego błędu jest używany hello 32-bitowa wersja programu Windows PowerShell (nawet na 64-bitowe wersje systemu operacyjnego), programu Azure PowerShell hello poleceń cmdlet usługi sieć szkieletowa tylko pracy w środowiskach 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="91e56-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="91e56-117">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="91e56-117">Solution</span></span>
<span data-ttu-id="91e56-118">Zawsze uruchamiaj polecenia cmdlet usługi sieć szkieletowa bezpośrednio z programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="91e56-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="91e56-119">Hello najnowszą wersję programu Azure PowerShell nie tworzy specjalne skrót, więc nie powinno to nastąpić.</span><span class="sxs-lookup"><span data-stu-id="91e56-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="91e56-120">Wyjątek inicjowania typu</span><span class="sxs-lookup"><span data-stu-id="91e56-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="91e56-121">Problem</span><span class="sxs-lookup"><span data-stu-id="91e56-121">Problem</span></span>
<span data-ttu-id="91e56-122">Podczas łączenia z toohello klastra w programie PowerShell zostanie wyświetlony błąd hello typeinitializationexception — System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="91e56-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="91e56-123">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="91e56-123">Solution</span></span>
<span data-ttu-id="91e56-124">Podczas instalacji nie ustawiono poprawnie zmiennej path.</span><span class="sxs-lookup"><span data-stu-id="91e56-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="91e56-125">Wyloguj się z systemem Windows i zaloguj się ponownie.</span><span class="sxs-lookup"><span data-stu-id="91e56-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="91e56-126">Spowoduje to odświeżenie ścieżki.</span><span class="sxs-lookup"><span data-stu-id="91e56-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="91e56-127">Połączenia klastra kończy się niepowodzeniem z "Obiekt jest zamknięty"</span><span class="sxs-lookup"><span data-stu-id="91e56-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="91e56-128">Problem</span><span class="sxs-lookup"><span data-stu-id="91e56-128">Problem</span></span>
<span data-ttu-id="91e56-129">Wywołanie tooConnect-ServiceFabricCluster zakończy się niepowodzeniem z powodu błędu w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="91e56-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="91e56-130">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="91e56-130">Solution</span></span>
<span data-ttu-id="91e56-131">Zamknij bieżące okno programu PowerShell hello i otworzyć nowe okno programu PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="91e56-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="91e56-132">Teraz powinno być możliwe połączenie toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="91e56-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="91e56-133">Wyjątek odmowa połączenia sieci szkieletowej</span><span class="sxs-lookup"><span data-stu-id="91e56-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="91e56-134">Problem</span><span class="sxs-lookup"><span data-stu-id="91e56-134">Problem</span></span>
<span data-ttu-id="91e56-135">Podczas debugowania w programie Visual Studio, otrzymasz komunikat o błędzie FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="91e56-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="91e56-136">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="91e56-136">Solution</span></span>
<span data-ttu-id="91e56-137">Ten błąd zazwyczaj występuje podczas toostart procesu hosta usługi ręcznie, zamiast stosowanie toostart środowiska uruchomieniowego platformy Service Fabric hello go.</span><span class="sxs-lookup"><span data-stu-id="91e56-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="91e56-138">Upewnij się, że nie masz żadnych projektów usług Ustaw jako projekty startowe w rozwiązaniu.</span><span class="sxs-lookup"><span data-stu-id="91e56-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="91e56-139">Tylko projekty aplikacji sieci szkieletowej usług powinna być ustawiona jako projekty startowe.</span><span class="sxs-lookup"><span data-stu-id="91e56-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="91e56-140">Jeśli po zakończeniu instalacji, klaster lokalny rozpoczyna toobehave nieprawidłowo, można zresetować go przy użyciu aplikacji na pasku zadań systemu Menedżera klastra lokalnego hello.</span><span class="sxs-lookup"><span data-stu-id="91e56-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="91e56-141">Spowoduje to usunięcie hello istniejącego klastra i skonfigurować nowy.</span><span class="sxs-lookup"><span data-stu-id="91e56-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="91e56-142">Należy pamiętać, że wszystkie wdrożone aplikacje i skojarzone dane zostaną usunięte.</span><span class="sxs-lookup"><span data-stu-id="91e56-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="91e56-143">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91e56-143">Next steps</span></span>
* [<span data-ttu-id="91e56-144">Omówienie i rozwiązywanie problemów klastra za pomocą raportów o kondycji systemu</span><span class="sxs-lookup"><span data-stu-id="91e56-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="91e56-145">Wizualizowanie klastra przy użyciu narzędzia Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="91e56-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

