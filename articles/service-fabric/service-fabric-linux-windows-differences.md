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
# <a name="differences-between-service-fabric-on-linux-preview-and-windows-generally-available"></a>Różnice między usługą Service Fabric w systemie Linux (wersja zapoznawcza) i w systemie Windows (wersja ogólnie dostępna)

Ponieważ usługa Service Fabric w systemie Linux jest w wersji zapoznawczej, pewne funkcje, które są obsługiwane w systemie Windows, nie są jeszcze obsługiwane w systemie Linux. Po pewnym czasie zestawy funkcji hello będzie na parzystości, gdy sieć szkieletowa usług w systemie Linux stanie się ogólnie dostępna. Różnica między funkcjami będzie się zmniejszać wraz z udostępnianiem kolejnych wersji. Hello następujące różnice między dostępne wersje najnowszych hello (to znaczy między wersja 5.6 w systemach Windows i w wersji 5.5 w systemie Linux): 

* Niezawodne kolekcje (i niezawodne usługi stanowe) 
* Zwrotny serwer proxy 
* Autonomiczny instalator 
* Weryfikacja schematu XML dla plików manifestu 
* Przekierowywanie konsoli 
* Witaj błędów Analysis Service (FAS)
* Narzędzie Docker Compose oraz sterowniki woluminów i rejestrowania dla kontenerów 
* Nadzór nad zasobami dla kontenerów i usług 
* Usługa DNS
* Obsługa usługi Azure Active Directory
* Polecenia interfejsu wiersza polecenia będące odpowiednikami niektórych poleceń programu PowerShell 
* Tylko podzestaw poleceń programu Powershell, mogą być uruchamiane na klaster systemu Linux (jak rozwinięty w następnej sekcji hello).

>[!NOTE]
>Przekierowywanie konsoli nie jest obsługiwane w klastrach produkcyjnych, nawet w systemie Windows.

Narzędzia programistyczne używane w systemie Windows różnią się także od tych używanych w systemie Linux. W systemie Windows można korzystać z narzędzi VisualStudio, Powershell, VSTS i ETW, a w systemie Linux z narzędzi Yeoman, Eclipse, Jenkins i LTTng.

## <a name="powershell-cmdlets-that-do-not-work-against-a-linux-service-fabric-cluster"></a>Polecenia cmdlet programu PowerShell, które nie działają względem klastra usługi Service Fabric z systemem Linux

* Invoke-ServiceFabricChaosTestScenario
* Invoke-ServiceFabricFailoverTestScenario
* Invoke-ServiceFabricPartitionDataLoss
* Invoke-ServiceFabricPartitionQuorumLoss
* Restart-ServiceFabricPartition
* Start-ServiceFabricNode
* Stop-ServiceFabricNode
* Get-ServiceFabricImageStoreContent
* Get-ServiceFabricChaosReport
* Get-ServiceFabricNodeTransitionProgress
* Get-ServiceFabricPartitionDataLossProgress
* Get-ServiceFabricPartitionQuorumLossProgress
* Get-ServiceFabricPartitionRestartProgress
* Get-ServiceFabricTestCommandStatusList
* Remove-ServiceFabricTestState
* Start-ServiceFabricChaos
* Start-ServiceFabricNodeTransition
* Start-ServiceFabricPartitionDataLoss
* Start-ServiceFabricPartitionQuorumLoss
* Start-ServiceFabricPartitionRestart
* Stop-ServiceFabricChaos
* Stop-ServiceFabricTestCommand
* Cmd
* Get-ServiceFabricNodeConfiguration
* Get-ServiceFabricClusterConfiguration
* Get-ServiceFabricClusterConfigurationUpgradeStatus
* Get-ServiceFabricPackageDebugParameters
* New-ServiceFabricPackageDebugParameter
* New-ServiceFabricPackageSharingPolicy
* Add-ServiceFabricNode
* Copy-ServiceFabricClusterPackage
* Get-ServiceFabricRuntimeSupportedVersion
* Get-ServiceFabricRuntimeUpgradeVersion
* New-ServiceFabricCluster
* New-ServiceFabricNodeConfiguration
* Remove-ServiceFabricCluster
* Remove-ServiceFabricClusterPackage
* Remove-ServiceFabricNodeConfiguration
* Test-ServiceFabricClusterManifest
* Test-ServiceFabricConfiguration
* Update-ServiceFabricNodeConfiguration
* Approve-ServiceFabricRepairTask
* Complete-ServiceFabricRepairTask
* Get-ServiceFabricRepairTask
* Invoke-ServiceFabricDecryptText
* Invoke-ServiceFabricEncryptSecret
* Invoke-ServiceFabricEncryptText
* Invoke-ServiceFabricInfrastructureCommand
* Invoke-ServiceFabricInfrastructureQuery
* Remove-ServiceFabricRepairTask
* Start-ServiceFabricRepairTask
* Stop-ServiceFabricRepairTask
* Update-ServiceFabricRepairTaskHealthPolicy



## <a name="next-steps"></a>Następne kroki
* [Przygotowywanie środowiska projektowego w systemie Linux](service-fabric-get-started-linux.md)
* [Przygotowywanie środowiska projektowego w systemie OSX](service-fabric-get-started-mac.md)
* [Create and deploy your first Service Fabric Java application on Linux using Yeoman](service-fabric-create-your-first-linux-application-with-java.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu programu Yeoman)
* [Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse](service-fabric-get-started-eclipse.md) (Tworzenie i wdrażanie pierwszej aplikacji Java usługi Service Fabric w systemie Linux przy użyciu wtyczki usługi Service Fabric dla środowiska Eclipse)
* [Create your first CSharp application on Linux](service-fabric-create-your-first-linux-application-with-csharp.md) (Tworzenie pierwszej aplikacji CSharp w systemie Linux)
* [Użyj aplikacji hello toomanage usługi sieci szkieletowej interfejsu wiersza polecenia](service-fabric-application-lifecycle-sfctl.md)
