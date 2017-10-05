---
title: "Skrypt programu PowerShell Azure Przykładowe — wdrożenie aplikacji do klastra | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — wdrażanie aplikacji do klastra usługi sieć szkieletowa usług."
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
ms.openlocfilehash: 2863823205dbd70f63948ecd4af8898220fe1ff8
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a>Wdrażanie aplikacji do klastra sieci szkieletowej usług

Ten przykładowy skrypt umożliwia skopiowanie pakietu aplikacji do magazynu obrazu klastra, rejestruje typ aplikacji w klastrze i tworzy wystąpienie aplikacji na podstawie typu aplikacji.  Jeśli wszystkie domyślne usługi zostały zdefiniowane w manifeście aplikacji typu aplikacji docelowej, te usługi są tworzone w tym momencie. Dostosuj parametry zgodnie z potrzebami. 

Jeśli to konieczne, Zainstaluj moduł programu PowerShell usługi Service Fabric [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[główne](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "wdrażania aplikacji do klastra")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Po przykładowym skrypcie zostało uruchomione, skrypt w [usuwania aplikacji](service-fabric-powershell-remove-application.md) można usunąć wystąpienia aplikacji, wyrejestrowywanie typu aplikacji i usuwanie pakietu aplikacji w magazynie obrazów.

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Kopiowanie ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | Skopiuj pakiet aplikacji do magazynu obrazu klastra.  |
|[Rejestr ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| Rejestruje typ i wersja aplikacji w klastrze. |
|[Nowe ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| Tworzy aplikację z typ zarejestrowanych aplikacji. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).

Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).
