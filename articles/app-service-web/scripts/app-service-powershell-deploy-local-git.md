---
title: "aaaAzure przykładowy skrypt programu PowerShell — tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="43a16-103">Tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="43a16-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="43a16-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web w lokalnym repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="43a16-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="43a16-105">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="43a16-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="43a16-106">Kod aplikacji musi ponadto toobe zatwierdzone do lokalnego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="43a16-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="43a16-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="43a16-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="43a16-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="43a16-108">Clean up deployment</span></span> 

<span data-ttu-id="43a16-109">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="43a16-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="43a16-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="43a16-110">Script explanation</span></span>

<span data-ttu-id="43a16-111">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="43a16-111">This script uses hello following commands.</span></span> <span data-ttu-id="43a16-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="43a16-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="43a16-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="43a16-113">Command</span></span> | <span data-ttu-id="43a16-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="43a16-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="43a16-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="43a16-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="43a16-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="43a16-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="43a16-117">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="43a16-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="43a16-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="43a16-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="43a16-119">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="43a16-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="43a16-120">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="43a16-120">Creates a web app.</span></span> |
| [<span data-ttu-id="43a16-121">Zestaw AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="43a16-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="43a16-122">Modyfikuje zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="43a16-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="43a16-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="43a16-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="43a16-124">Pobierz profil publikowania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="43a16-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="43a16-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="43a16-125">Next steps</span></span>

<span data-ttu-id="43a16-126">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43a16-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="43a16-127">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="43a16-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
