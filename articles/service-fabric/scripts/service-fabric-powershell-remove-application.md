---
title: "aaaAzure przykładowym skrypcie programu PowerShell — Usuń aplikację z klastra | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell — Usuń aplikację z klastra usługi sieć szkieletowa usług."
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
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>Usuń aplikację z klastra sieci szkieletowej usług

Ten przykładowy skrypt usuwa uruchomione wystąpienie aplikacji sieci szkieletowej usług, wyrejestrowuje typ i wersja aplikacji z klastra hello i usuwa pakiet aplikacji hello z magazynu obrazu klastra hello.  Trwa usuwanie wystąpienia aplikacji hello spowoduje również usunięcie hello wszystkie uruchomione wystąpienia usługi skojarzoną z daną aplikacją. Dostosuj parametry hello zgodnie z potrzebami. 

W razie potrzeby Zainstaluj moduł programu PowerShell usługi Service Fabric hello z hello [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Usuń ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | Usuwa uruchomione wystąpienie aplikacji sieci szkieletowej usług z hello klastra.  |
| [Wyrejestruj ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | Wyrejestrowuje sieci szkieletowej usług typ i wersja aplikacji z hello klastra. |
| [Usuń ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | Usuwa pakiet aplikacji sieci szkieletowej usług z hello magazynu obrazów.|

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).
