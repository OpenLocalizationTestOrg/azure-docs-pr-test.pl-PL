---
title: "Przykładowy skrypt programu PowerShell - aaaAzure uaktualniania aplikacji usługi Service Fabric | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a>Uaktualnianie aplikacji sieci szkieletowej usług

Ten przykładowy skrypt uaktualnia uruchomionej usługi sieć szkieletowa usług aplikacji wystąpienia tooversion 1.3.0. skrypt Hello kopiuje hello nowego pakietu toohello klastra obrazu sklepu z aplikacjami, rejestruje typ aplikacji hello uruchamia monitorowanych uaktualnienia i stale sprawdza stan uaktualnienia hello aż do ukończenia uaktualnienia hello, lub wycofuje. Dostosuj parametry hello zgodnie z potrzebami. 

W razie potrzeby Zainstaluj moduł programu PowerShell usługi Service Fabric hello z hello [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | Pobiera wszystkich aplikacji hello w hello klastra sieci szkieletowej usług lub określonych aplikacji.  |
| [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | Pobiera stan hello uaktualniania aplikacji sieci szkieletowej usług. |
| [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | Pobiera typy aplikacji usługi sieć szkieletowa hello zarejestrowany w klastrze usługi sieć szkieletowa hello. |
| [Wyrejestruj ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Wyrejestrowuje typ aplikacji sieci szkieletowej usług.  |
| [Kopiowanie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Kopie przechowywania obrazu toohello pakietu sieci szkieletowej usług aplikacji.  |
| [Rejestr ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | Rejestruje typ aplikacji sieci szkieletowej usług. |
| [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | Uaktualnia wersję typu sieci szkieletowej usług aplikacji toohello określonej aplikacji. |


## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).
