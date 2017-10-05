---
title: "Skrypt programu PowerShell Azure przykładowe — tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od GitHub | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: fc594a94bb64ceb88370be8617036a73402ade4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="d625f-103">Tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od GitHub</span><span class="sxs-lookup"><span data-stu-id="d625f-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="d625f-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie konfiguruje ciągłego wdrażania od repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="d625f-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="d625f-105">GitHub wdrożenia bez ciągłego wdrażania, zobacz [tworzenie aplikacji sieci web i wdrażanie kodu z usługi GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="d625f-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="d625f-106">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d625f-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="d625f-107">Ponadto upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="d625f-107">Also, ensure that:</span></span>

- <span data-ttu-id="d625f-108">Utworzono połączenie z platformą Azure za pomocą `az login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d625f-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="d625f-109">Kod aplikacji znajduje się w publicznym lub prywatnym repozytorium GitHub, którego jesteś właścicielem.</span><span class="sxs-lookup"><span data-stu-id="d625f-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="d625f-110">Masz [utworzony token dostępu na koncie usługi GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="d625f-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="d625f-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d625f-111">Sample script</span></span>

<span data-ttu-id="d625f-112">[!code-powershell[główne](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "utworzenia aplikacji sieci web z ciągłego wdrażania od GitHub")]</span><span class="sxs-lookup"><span data-stu-id="d625f-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d625f-113">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d625f-113">Clean up deployment</span></span> 

<span data-ttu-id="d625f-114">Po uruchomieniu przykładowym skrypcie następującego polecenia można usunąć grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="d625f-114">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d625f-115">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d625f-115">Script explanation</span></span>

<span data-ttu-id="d625f-116">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="d625f-116">This script uses the following commands.</span></span> <span data-ttu-id="d625f-117">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="d625f-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d625f-118">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d625f-118">Command</span></span> | <span data-ttu-id="d625f-119">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d625f-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d625f-120">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d625f-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d625f-121">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="d625f-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d625f-122">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d625f-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d625f-123">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="d625f-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d625f-124">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d625f-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d625f-125">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="d625f-125">Creates a web app.</span></span> |
| [<span data-ttu-id="d625f-126">Zestaw AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="d625f-126">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="d625f-127">Modyfikuje zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="d625f-127">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d625f-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d625f-128">Next steps</span></span>

<span data-ttu-id="d625f-129">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d625f-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d625f-130">Dodatkowe przykłady programu Powershell systemu Azure dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d625f-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
