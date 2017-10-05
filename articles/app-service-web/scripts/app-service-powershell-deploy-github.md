---
title: "Przykładowy skrypt programu PowerShell Azure — tworzenie aplikacji sieci web i wdrażanie kodu z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure — tworzenie aplikacji sieci web i wdrażanie kodu z usługi GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 1f7fc21dc12c334f5d347ae9918bd62945bede64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a>Tworzenie aplikacji sieci web i wdrażanie kodu z usługi GitHub

Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web z publicznego repozytorium GitHub (bez ciągłego wdrażania). Do wdrożenia usługi GitHub z ciągłego wdrażania, zobacz [utworzenia aplikacji sieci web z ciągłego wdrażania od GitHub](app-service-powershell-continuous-deployment-github.md).

W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](/powershell/azure/overview). Ponadto należy łącze do repozytorium GitHub, który zawiera kod aplikacji sieci web.

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[główne](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "tworzenie aplikacji sieci web i wdrażanie kodu z usługi GitHub")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Po uruchomieniu przykładowym skrypcie następującego polecenia można usunąć grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Nowe AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Nowe AzureRmAppServicePlan](/powershell/module/azurerm.websites/new-azurermappserviceplan) | Tworzy plan usługi App Service. |
| [Nowe AzureRmWebApp](/powershell/module/azurerm.websites/new-azurermwebapp) | Tworzy aplikację sieci web. |
| [Zestaw AzureRmResource](/powershell/module/azurerm.resources/set-azurermresource) | Modyfikuje zasobów w grupie zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Dodatkowe przykłady programu Powershell systemu Azure dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).
