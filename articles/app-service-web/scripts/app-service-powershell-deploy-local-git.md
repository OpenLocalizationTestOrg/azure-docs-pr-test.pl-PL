---
title: "Przykładowy skrypt programu PowerShell Azure — tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure — tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 855b8c643bf2a742e763bda2e2c21c6a86331aac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="60586-103">Tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="60586-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="60586-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web w lokalnym repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="60586-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="60586-105">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="60586-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="60586-106">Kod aplikacji musi ponadto zadeklarowane w lokalnym repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="60586-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="60586-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="60586-107">Sample script</span></span>

<span data-ttu-id="60586-108">[!code-powershell[główne](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git")]</span><span class="sxs-lookup"><span data-stu-id="60586-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="60586-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="60586-109">Clean up deployment</span></span> 

<span data-ttu-id="60586-110">Po uruchomieniu przykładowym skrypcie następującego polecenia można usunąć grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="60586-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="60586-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="60586-111">Script explanation</span></span>

<span data-ttu-id="60586-112">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="60586-112">This script uses the following commands.</span></span> <span data-ttu-id="60586-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="60586-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="60586-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="60586-114">Command</span></span> | <span data-ttu-id="60586-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="60586-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="60586-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="60586-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="60586-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="60586-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="60586-118">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="60586-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="60586-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="60586-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="60586-120">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="60586-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="60586-121">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="60586-121">Creates a web app.</span></span> |
| [<span data-ttu-id="60586-122">Zestaw AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="60586-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="60586-123">Modyfikuje zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="60586-123">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="60586-124">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="60586-124">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="60586-125">Pobierz profil publikowania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="60586-125">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="60586-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60586-126">Next steps</span></span>

<span data-ttu-id="60586-127">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="60586-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="60586-128">Dodatkowe przykłady programu Powershell systemu Azure dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="60586-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
