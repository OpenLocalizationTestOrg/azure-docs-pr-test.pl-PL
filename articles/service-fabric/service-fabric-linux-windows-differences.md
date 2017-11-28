---
title: "aaaAzure sieci szkieletowej usług różnice między systemami Linux i Windows | Dokumentacja firmy Microsoft"
description: "Różnice między hello Azure Service Fabric w wersji zapoznawczej w systemie Linux i sieci szkieletowej usług Azure w systemie Windows."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 7a16a440dfc8d9006e274f46951be1562e6f10d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a><span data-ttu-id="5c8ad-103">Różnice między usługą Service Fabric w systemie Linux (wersja zapoznawcza) i w systemie Windows (wersja ogólnie dostępna)</span><span class="sxs-lookup"><span data-stu-id="5c8ad-103">Differences between Service Fabric on Linux (preview) and Windows (generally available)</span></span>

<span data-ttu-id="5c8ad-104">Ponieważ usługa Service Fabric w systemie Linux jest w wersji zapoznawczej, pewne funkcje, które są obsługiwane w systemie Windows, nie są jeszcze obsługiwane w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="5c8ad-104">Since Service Fabric on Linux is a preview, there are some features that are supported on Windows, but not yet on Linux.</span></span> <span data-ttu-id="5c8ad-105">Po pewnym czasie zestawy funkcji hello będzie na parzystości, gdy sieć szkieletowa usług w systemie Linux stanie się ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="5c8ad-105">Eventually, hello feature sets will be at parity when Service Fabric on Linux becomes generally available.</span></span> <span data-ttu-id="5c8ad-106">Różnica między funkcjami będzie się zmniejszać wraz z udostępnianiem kolejnych wersji.</span><span class="sxs-lookup"><span data-stu-id="5c8ad-106">With upcoming releases, this feature gap will shrink.</span></span> <span data-ttu-id="5c8ad-107">Hello następujące różnice między dostępne wersje najnowszych hello (to znaczy między wersja 5.6 w systemach Windows i w wersji 5.5 w systemie Linux):</span><span class="sxs-lookup"><span data-stu-id="5c8ad-107">hello following differences exist between hello latest available releases (that is, between version 5.6 on Windows and version 5.5 on Linux):</span></span> 

* <span data-ttu-id="5c8ad-108">Niezawodne kolekcje (i niezawodne usługi stanowe)</span><span class="sxs-lookup"><span data-stu-id="5c8ad-108">Reliable Collections (and Reliable Stateful Services)</span></span> 
* <span data-ttu-id="5c8ad-109">Zwrotny serwer proxy</span><span class="sxs-lookup"><span data-stu-id="5c8ad-109">ReverseProxy</span></span> 
* <span data-ttu-id="5c8ad-110">Autonomiczny instalator</span><span class="sxs-lookup"><span data-stu-id="5c8ad-110">Standalone installer</span></span> 
* <span data-ttu-id="5c8ad-111">Weryfikacja schematu XML dla plików manifestu</span><span class="sxs-lookup"><span data-stu-id="5c8ad-111">XML schema validation for manifest files</span></span> 
* <span data-ttu-id="5c8ad-112">Przekierowywanie konsoli</span><span class="sxs-lookup"><span data-stu-id="5c8ad-112">Console redirection</span></span> 
* <span data-ttu-id="5c8ad-113">Witaj błędów Analysis Service (FAS)</span><span class="sxs-lookup"><span data-stu-id="5c8ad-113">hello Fault Analysis Service (FAS)</span></span>
* <span data-ttu-id="5c8ad-114">Narzędzie Docker Compose oraz sterowniki woluminów i rejestrowania dla kontenerów</span><span class="sxs-lookup"><span data-stu-id="5c8ad-114">Docker compose and volume and logging drivers for containers</span></span> 
* <span data-ttu-id="5c8ad-115">Nadzór nad zasobami dla kontenerów i usług</span><span class="sxs-lookup"><span data-stu-id="5c8ad-115">Resource governance for containers and services</span></span> 
* <span data-ttu-id="5c8ad-116">Usługa DNS</span><span class="sxs-lookup"><span data-stu-id="5c8ad-116">DNS service</span></span>
* <span data-ttu-id="5c8ad-117">Obsługa usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c8ad-117">Azure Active Directory support</span></span>
* <span data-ttu-id="5c8ad-118">Polecenia interfejsu wiersza polecenia będące odpowiednikami niektórych poleceń programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="5c8ad-118">CLI command equivalents of certain Powershell commands</span></span> 
* <span data-ttu-id="5c8ad-119">Tylko podzestaw poleceń programu Powershell, mogą być uruchamiane na klaster systemu Linux (jak rozwinięty w następnej sekcji hello).</span><span class="sxs-lookup"><span data-stu-id="5c8ad-119">Only a subset of Powershell commands can be run against a Linux cluster (as expanded in hello next section).</span></span>

>[!NOTE]
><span data-ttu-id="5c8ad-120">Przekierowywanie konsoli nie jest obsługiwane w klastrach produkcyjnych, nawet w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="5c8ad-120">Console redirection is not supported in production clusters, even on Windows.</span></span>

<span data-ttu-id="5c8ad-121">Narzędzia programistyczne używane w systemie Windows różnią się także od tych używanych w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="5c8ad-121">Development tooling is also different between Windows and Linux.</span></span> <span data-ttu-id="5c8ad-122">W systemie Windows można korzystać z narzędzi VisualStudio, Powershell, VSTS i ETW, a w systemie Linux z narzędzi Yeoman, Eclipse, Jenkins i LTTng.</span><span class="sxs-lookup"><span data-stu-id="5c8ad-122">VisualStudio, Powershell, VSTS, and ETW are used on Windows while Yeoman, Eclipse, Jenkins, and LTTng are used on Linux.</span></span>

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a><span data-ttu-id="5c8ad-123">Polecenia cmdlet programu PowerShell, które nie działają względem klastra usługi Service Fabric z systemem Linux</span><span class="sxs-lookup"><span data-stu-id="5c8ad-123">Powershell cmdlets that do not work against a Linux Service Fabric cluster</span></span>

* <span data-ttu-id="5c8ad-124">Invoke-ServiceFabricChaosTestScenario</span><span class="sxs-lookup"><span data-stu-id="5c8ad-124">Invoke-ServiceFabricChaosTestScenario</span></span>
* <span data-ttu-id="5c8ad-125">Invoke-ServiceFabricFailoverTestScenario</span><span class="sxs-lookup"><span data-stu-id="5c8ad-125">Invoke-ServiceFabricFailoverTestScenario</span></span>
* <span data-ttu-id="5c8ad-126">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="5c8ad-126">Invoke-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="5c8ad-127">Invoke-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="5c8ad-127">Invoke-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="5c8ad-128">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="5c8ad-128">Restart-ServiceFabricPartition</span></span>
* <span data-ttu-id="5c8ad-129">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="5c8ad-129">Start-ServiceFabricNode</span></span>
* <span data-ttu-id="5c8ad-130">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="5c8ad-130">Stop-ServiceFabricNode</span></span>
* <span data-ttu-id="5c8ad-131">Get-ServiceFabricImageStoreContent</span><span class="sxs-lookup"><span data-stu-id="5c8ad-131">Get-ServiceFabricImageStoreContent</span></span>
* <span data-ttu-id="5c8ad-132">Get-ServiceFabricChaosReport</span><span class="sxs-lookup"><span data-stu-id="5c8ad-132">Get-ServiceFabricChaosReport</span></span>
* <span data-ttu-id="5c8ad-133">Get-ServiceFabricNodeTransitionProgress</span><span class="sxs-lookup"><span data-stu-id="5c8ad-133">Get-ServiceFabricNodeTransitionProgress</span></span>
* <span data-ttu-id="5c8ad-134">Get-ServiceFabricPartitionDataLossProgress</span><span class="sxs-lookup"><span data-stu-id="5c8ad-134">Get-ServiceFabricPartitionDataLossProgress</span></span>
* <span data-ttu-id="5c8ad-135">Get-ServiceFabricPartitionQuorumLossProgress</span><span class="sxs-lookup"><span data-stu-id="5c8ad-135">Get-ServiceFabricPartitionQuorumLossProgress</span></span>
* <span data-ttu-id="5c8ad-136">Get-ServiceFabricPartitionRestartProgress</span><span class="sxs-lookup"><span data-stu-id="5c8ad-136">Get-ServiceFabricPartitionRestartProgress</span></span>
* <span data-ttu-id="5c8ad-137">Get-ServiceFabricTestCommandStatusList</span><span class="sxs-lookup"><span data-stu-id="5c8ad-137">Get-ServiceFabricTestCommandStatusList</span></span>
* <span data-ttu-id="5c8ad-138">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="5c8ad-138">Remove-ServiceFabricTestState</span></span>
* <span data-ttu-id="5c8ad-139">Start-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="5c8ad-139">Start-ServiceFabricChaos</span></span>
* <span data-ttu-id="5c8ad-140">Start-ServiceFabricNodeTransition</span><span class="sxs-lookup"><span data-stu-id="5c8ad-140">Start-ServiceFabricNodeTransition</span></span>
* <span data-ttu-id="5c8ad-141">Start-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="5c8ad-141">Start-ServiceFabricPartitionDataLoss</span></span>
* <span data-ttu-id="5c8ad-142">Start-ServiceFabricPartitionQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="5c8ad-142">Start-ServiceFabricPartitionQuorumLoss</span></span>
* <span data-ttu-id="5c8ad-143">Start-ServiceFabricPartitionRestart</span><span class="sxs-lookup"><span data-stu-id="5c8ad-143">Start-ServiceFabricPartitionRestart</span></span>
* <span data-ttu-id="5c8ad-144">Stop-ServiceFabricChaos</span><span class="sxs-lookup"><span data-stu-id="5c8ad-144">Stop-ServiceFabricChaos</span></span>
* <span data-ttu-id="5c8ad-145">Stop-ServiceFabricTestCommand</span><span class="sxs-lookup"><span data-stu-id="5c8ad-145">Stop-ServiceFabricTestCommand</span></span>
* <span data-ttu-id="5c8ad-146">Cmd</span><span class="sxs-lookup"><span data-stu-id="5c8ad-146">Cmd</span></span>
* <span data-ttu-id="5c8ad-147">Get-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c8ad-147">Get-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="5c8ad-148">Get-ServiceFabricClusterConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c8ad-148">Get-ServiceFabricClusterConfiguration</span></span>
* <span data-ttu-id="5c8ad-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span><span class="sxs-lookup"><span data-stu-id="5c8ad-149">Get-ServiceFabricClusterConfigurationUpgradeStatus</span></span>
* <span data-ttu-id="5c8ad-150">Get-ServiceFabricPackageDebugParameters</span><span class="sxs-lookup"><span data-stu-id="5c8ad-150">Get-ServiceFabricPackageDebugParameters</span></span>
* <span data-ttu-id="5c8ad-151">New-ServiceFabricPackageDebugParameter</span><span class="sxs-lookup"><span data-stu-id="5c8ad-151">New-ServiceFabricPackageDebugParameter</span></span>
* <span data-ttu-id="5c8ad-152">New-ServiceFabricPackageSharingPolicy</span><span class="sxs-lookup"><span data-stu-id="5c8ad-152">New-ServiceFabricPackageSharingPolicy</span></span>
* <span data-ttu-id="5c8ad-153">Add-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="5c8ad-153">Add-ServiceFabricNode</span></span>
* <span data-ttu-id="5c8ad-154">Copy-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="5c8ad-154">Copy-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="5c8ad-155">Get-ServiceFabricRuntimeSupportedVersion</span><span class="sxs-lookup"><span data-stu-id="5c8ad-155">Get-ServiceFabricRuntimeSupportedVersion</span></span>
* <span data-ttu-id="5c8ad-156">Get-ServiceFabricRuntimeUpgradeVersion</span><span class="sxs-lookup"><span data-stu-id="5c8ad-156">Get-ServiceFabricRuntimeUpgradeVersion</span></span>
* <span data-ttu-id="5c8ad-157">New-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="5c8ad-157">New-ServiceFabricCluster</span></span>
* <span data-ttu-id="5c8ad-158">New-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c8ad-158">New-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="5c8ad-159">Remove-ServiceFabricCluster</span><span class="sxs-lookup"><span data-stu-id="5c8ad-159">Remove-ServiceFabricCluster</span></span>
* <span data-ttu-id="5c8ad-160">Remove-ServiceFabricClusterPackage</span><span class="sxs-lookup"><span data-stu-id="5c8ad-160">Remove-ServiceFabricClusterPackage</span></span>
* <span data-ttu-id="5c8ad-161">Remove-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c8ad-161">Remove-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="5c8ad-162">Test-ServiceFabricClusterManifest</span><span class="sxs-lookup"><span data-stu-id="5c8ad-162">Test-ServiceFabricClusterManifest</span></span>
* <span data-ttu-id="5c8ad-163">Test-ServiceFabricConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c8ad-163">Test-ServiceFabricConfiguration</span></span>
* <span data-ttu-id="5c8ad-164">Update-ServiceFabricNodeConfiguration</span><span class="sxs-lookup"><span data-stu-id="5c8ad-164">Update-ServiceFabricNodeConfiguration</span></span>
* <span data-ttu-id="5c8ad-165">Approve-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="5c8ad-165">Approve-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="5c8ad-166">Complete-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="5c8ad-166">Complete-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="5c8ad-167">Get-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="5c8ad-167">Get-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="5c8ad-168">Invoke-ServiceFabricDecryptText</span><span class="sxs-lookup"><span data-stu-id="5c8ad-168">Invoke-ServiceFabricDecryptText</span></span>
* <span data-ttu-id="5c8ad-169">Invoke-ServiceFabricEncryptSecret</span><span class="sxs-lookup"><span data-stu-id="5c8ad-169">Invoke-ServiceFabricEncryptSecret</span></span>
* <span data-ttu-id="5c8ad-170">Invoke-ServiceFabricEncryptText</span><span class="sxs-lookup"><span data-stu-id="5c8ad-170">Invoke-ServiceFabricEncryptText</span></span>
* <span data-ttu-id="5c8ad-171">Invoke-ServiceFabricInfrastructureCommand</span><span class="sxs-lookup"><span data-stu-id="5c8ad-171">Invoke-ServiceFabricInfrastructureCommand</span></span>
* <span data-ttu-id="5c8ad-172">Invoke-ServiceFabricInfrastructureQuery</span><span class="sxs-lookup"><span data-stu-id="5c8ad-172">Invoke-ServiceFabricInfrastructureQuery</span></span>
* <span data-ttu-id="5c8ad-173">Remove-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="5c8ad-173">Remove-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="5c8ad-174">Start-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="5c8ad-174">Start-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="5c8ad-175">Stop-ServiceFabricRepairTask</span><span class="sxs-lookup"><span data-stu-id="5c8ad-175">Stop-ServiceFabricRepairTask</span></span>
* <span data-ttu-id="5c8ad-176">Update-ServiceFabricRepairTaskHealthPolicy</span><span class="sxs-lookup"><span data-stu-id="5c8ad-176">Update-ServiceFabricRepairTaskHealthPolicy</span></span>



## <a name="next-steps"></a><span data-ttu-id="5c8ad-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5c8ad-177">Next steps</span></span>
* [<span data-ttu-id="5c8ad-178">Przygotowywanie środowiska projektowego w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="5c8ad-178">Prepare your development environment on Linux</span></span>](service-fabric-get-started-linux.md)
* [<span data-ttu-id="5c8ad-179">Przygotowywanie środowiska projektowego w systemie OSX</span><span class="sxs-lookup"><span data-stu-id="5c8ad-179">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* <span data-ttu-id="5c8ad-180">[Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu programu Yeoman)</span><span class="sxs-lookup"><span data-stu-id="5c8ad-180">[Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md)</span></span>
* <span data-ttu-id="5c8ad-181">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu wtyczki usługi Service Fabric dla środowiska Eclipse)</span><span class="sxs-lookup"><span data-stu-id="5c8ad-181">[Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md)</span></span>
* <span data-ttu-id="5c8ad-182">[Create your first CSharp application on Linux](service-fabric-create-your-first-linux-application-with-csharp.md) (Tworzenie pierwszej aplikacji CSharp w systemie Linux)</span><span class="sxs-lookup"><span data-stu-id="5c8ad-182">[Create your first CSharp application on Linux](service-fabric-create-your-first-linux-application-with-csharp.md)</span></span>
* [<span data-ttu-id="5c8ad-183">Użyj aplikacji hello toomanage usługi sieci szkieletowej interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="5c8ad-183">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
