---
title: "aaaAzure przykładowy skrypt programu PowerShell — tworzenie aplikacji sieci web i wdrażanie tooa kodu tymczasowej środowiska | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure — tworzenie aplikacji sieci web i wdrażanie tooa kodu tymczasowej środowiska"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="e5aa2-103">Tworzenie aplikacji sieci web i wdrażanie tooa kodu tymczasowej środowiska</span><span class="sxs-lookup"><span data-stu-id="e5aa2-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="e5aa2-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z gniazdem dodatkowe wdrożenia o nazwie "tymczasowe", a następnie wdraża toohello aplikacji przykładowej, "staging" miejsca.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="e5aa2-105">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e5aa2-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="e5aa2-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e5aa2-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="e5aa2-107">Clean up deployment</span></span> 

<span data-ttu-id="e5aa2-108">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="e5aa2-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="e5aa2-109">Script explanation</span></span>

<span data-ttu-id="e5aa2-110">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-110">This script uses hello following commands.</span></span> <span data-ttu-id="e5aa2-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e5aa2-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="e5aa2-112">Command</span></span> | <span data-ttu-id="e5aa2-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="e5aa2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e5aa2-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e5aa2-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e5aa2-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e5aa2-116">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e5aa2-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="e5aa2-117">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e5aa2-118">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e5aa2-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="e5aa2-119">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-119">Creates a web app.</span></span> |
| [<span data-ttu-id="e5aa2-120">Zestaw AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e5aa2-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="e5aa2-121">Modyfikuje jego warstwy cenowej toochange planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="e5aa2-122">Nowe AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="e5aa2-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="e5aa2-123">Tworzy miejsca wdrożenia dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="e5aa2-124">Zestaw AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="e5aa2-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="e5aa2-125">Modyfikuje zasobów w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="e5aa2-126">AzureRmWebAppSlot wymiany</span><span class="sxs-lookup"><span data-stu-id="e5aa2-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="e5aa2-127">Zamienia miejsce wdrożenia aplikacji sieci web w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="e5aa2-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e5aa2-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e5aa2-128">Next steps</span></span>

<span data-ttu-id="e5aa2-129">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e5aa2-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e5aa2-130">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e5aa2-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
