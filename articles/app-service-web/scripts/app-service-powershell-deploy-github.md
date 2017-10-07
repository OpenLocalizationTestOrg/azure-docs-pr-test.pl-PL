---
title: "aaaAzure przykładowy skrypt programu PowerShell — tworzenie aplikacji sieci web i wdrażanie kodu z serwisu GitHub | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 9a28f9cb01b71c86fa0a3f1d0a6761fc3d45d43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="d57ae-103">Tworzenie aplikacji sieci web i wdrażanie kodu z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="d57ae-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="d57ae-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web z publicznego repozytorium GitHub (bez ciągłego wdrażania).</span><span class="sxs-lookup"><span data-stu-id="d57ae-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="d57ae-105">Do wdrożenia usługi GitHub z ciągłego wdrażania, zobacz [utworzenia aplikacji sieci web z ciągłego wdrażania od GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="d57ae-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="d57ae-106">Jeśli to konieczne, zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d57ae-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="d57ae-107">Ponadto należy zawierający kodu aplikacji sieci web hello repozytorium tooGitHub łącza.</span><span class="sxs-lookup"><span data-stu-id="d57ae-107">Also, you need a link tooGitHub repository that contains hello web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d57ae-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d57ae-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d57ae-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d57ae-109">Clean up deployment</span></span> 

<span data-ttu-id="d57ae-110">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="d57ae-110">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d57ae-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d57ae-111">Script explanation</span></span>

<span data-ttu-id="d57ae-112">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="d57ae-112">This script uses hello following commands.</span></span> <span data-ttu-id="d57ae-113">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d57ae-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d57ae-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d57ae-114">Command</span></span> | <span data-ttu-id="d57ae-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d57ae-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d57ae-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d57ae-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d57ae-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d57ae-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d57ae-118">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d57ae-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d57ae-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="d57ae-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d57ae-120">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d57ae-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d57ae-121">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="d57ae-121">Creates a web app.</span></span> |
| [<span data-ttu-id="d57ae-122">Zestaw AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="d57ae-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="d57ae-123">Modyfikuje zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="d57ae-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d57ae-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d57ae-124">Next steps</span></span>

<span data-ttu-id="d57ae-125">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d57ae-125">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d57ae-126">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d57ae-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
