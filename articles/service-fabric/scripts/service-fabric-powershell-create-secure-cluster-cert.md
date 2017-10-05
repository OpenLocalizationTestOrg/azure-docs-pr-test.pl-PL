---
title: "Skrypt programu PowerShell Azure przykładowe — Tworzenie klastra sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Tworzenie klastra sieci szkieletowej usług."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 7cbeb3da695af3815ba660f9cc2e3388abb6f87d
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-service-fabric-cluster"></a>Tworzenie klastra sieci szkieletowej usług

Ten przykładowy skrypt tworzy klaster sieci szkieletowej usług pięcioma węzłami klastra zabezpieczone za pomocą certyfikatu X.509.  Polecenie tworzy certyfikat z podpisem własnym i przekazuje go do nowego magazynu kluczy. Certyfikat jest również kopiowany do katalogu lokalnego.  Ustaw *-OS* parametr, aby wybrać wersję systemu Windows lub Linux, działającą w węzłach klastra.  Dostosuj parametry zgodnie z potrzebami.

W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](/powershell/azure/overview) , a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure. 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[główne](../../../powershell_scripts/service-fabric/create-secure-cluster/create-secure-cluster.ps1 "Tworzenie klastra sieci szkieletowej usług")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Po uruchomieniu przykładowym skrypcie następującego polecenia można usunąć grupy zasobów klastra i wszystkie powiązane zasoby.

```powershell
$groupname="mysfclustergroup"
Remove-AzureRmResourceGroup -Name $groupname -Force
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmServiceFabricCluster](/powershell/module/azurerm.servicefabric/New-AzureRmServiceFabricCluster) | Tworzy nowy klaster sieci szkieletowej usług. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Dodatkowe przykłady programu Azure Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).
