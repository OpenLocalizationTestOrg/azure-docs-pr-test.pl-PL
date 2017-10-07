---
title: "aaaAzure przykładowy skrypt programu PowerShell — wdrożenie aplikacji tooa klastra | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — wdrażanie klastra usługi sieć szkieletowa tooa aplikacji."
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>Wdrażanie klastra usługi sieć szkieletowa tooa aplikacji

Ten przykładowy skrypt kopiuje pakiet tooa klastra obrazu sklepu z aplikacjami, rejestruje typ aplikacji hello w klastrze hello i tworzy wystąpienie aplikacji na podstawie typu aplikacji hello.  Jeśli wszystkie domyślne usługi zostały zdefiniowane w manifeście aplikacji hello typu aplikacji docelowej hello, te usługi są tworzone w tym momencie. Dostosuj parametry hello zgodnie z potrzebami. 

W razie potrzeby Zainstaluj moduł programu PowerShell usługi Service Fabric hello z hello [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Po uruchomieniu przykładowym skrypcie hello hello skryptu w [usuwania aplikacji](service-fabric-powershell-remove-application.md) można instancji aplikacji hello tooremove używane, wyrejestrowywanie typu aplikacji hello i usunąć pakiet aplikacji hello z hello magazynu obrazów.

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Kopiowanie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Skopiuj pakiet toohello klastra obrazu sklepu z aplikacjami.  |
|[Rejestr ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Rejestruje typ i wersja aplikacji w klastrze hello. |
|[Nowe ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Tworzy aplikację z typ zarejestrowanych aplikacji. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).
