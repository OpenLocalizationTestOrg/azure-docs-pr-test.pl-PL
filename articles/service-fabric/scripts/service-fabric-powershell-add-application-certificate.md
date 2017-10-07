---
title: "aaaAzure przykładowy skrypt programu PowerShell — Dodawanie aplikacji cert tooa klastra | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Dodaj klaster sieci szkieletowej usług tooa aplikacji certyfikatu."
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
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>Dodaj klaster sieci szkieletowej usług tooa certyfikat aplikacji

Ten przykładowy skrypt tworzy certyfikat z podpisem własnym w hello określonej usługi Azure key vault i instaluje je tooall węzłów klastra usługi sieć szkieletowa hello. certyfikat Hello pobiera również tooa folderu lokalnego. Hello nazwę certyfikatu pobrane hello jest hello taka sama jak nazwa hello hello certyfikatu w magazynie kluczy hello. Dostosuj parametry hello zgodnie z potrzebami.

Jeśli to konieczne, zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview) , a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure. 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następującego polecenia: każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Dodaj AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | Dodaj wchodzących w skład klastra hello zestawu skalowania maszyn wirtualnych toohello certyfikatu w usłudze nowej aplikacji.  |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Dodatkowe przykłady programu Azure Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).
