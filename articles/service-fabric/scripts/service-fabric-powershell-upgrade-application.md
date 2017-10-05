---
title: "Przykładowy skrypt programu PowerShell Azure - uaktualniania aplikacji usługi Service Fabric | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell — uaktualnienie aplikacji sieci szkieletowej usług."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 454849f82ddb23ddb9d71459f86e3cf5a1589254
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Uaktualnianie aplikacji sieci szkieletowej usług

Ten przykładowy skrypt uaktualnia uruchomione wystąpienie aplikacji sieci szkieletowej usług do wersji 1.3.0. Skrypt kopiuje nowy pakiet aplikacji do magazynu obrazu klastra, rejestruje typ aplikacji, rozpoczyna się uaktualnienie monitorowanych i stale sprawdza stan uaktualnienia, aż do uaktualnienia ukończenia lub wycofuje. Dostosuj parametry zgodnie z potrzebami. 

Jeśli to konieczne, Zainstaluj moduł programu PowerShell usługi Service Fabric [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[główne](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "uaktualnianie aplikacji")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Pobiera wszystkie aplikacje w klastrze usługi sieć szkieletowa usług lub określonych aplikacji.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Pobiera stan uaktualniania aplikacji sieci szkieletowej usług. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Pobiera typy aplikacji usługi sieć szkieletowa zarejestrowany w klastrze usługi sieć szkieletowa usług. |
| [Wyrejestruj ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Wyrejestrowuje typ aplikacji sieci szkieletowej usług.  |
| [Kopiowanie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Kopiuje pakiet aplikacji usługi sieci szkieletowej magazynu obrazów.  |
| [Rejestr ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Rejestruje typ aplikacji sieci szkieletowej usług. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Uaktualnia aplikacji usługi Service Fabric, do wersji typu określonej aplikacji. |


## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).
