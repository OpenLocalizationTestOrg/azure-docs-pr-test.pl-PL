---
title: "Przykładowy skrypt programu PowerShell - aaaAzure przypisać domeny niestandardowej aplikacji sieci web tooa | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - Przypisz aplikację sieci web tooa domeny niestandardowej"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="3b48f-103">Przypisz aplikację sieci web tooa domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="3b48f-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="3b48f-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie mapuje `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="3b48f-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="3b48f-105">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="3b48f-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="3b48f-106">Ponadto należy toohave dostępu tooyour domeny rejestratora na stronie konfiguracji DNS.</span><span class="sxs-lookup"><span data-stu-id="3b48f-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="3b48f-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="3b48f-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3b48f-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="3b48f-108">Clean up deployment</span></span> 

<span data-ttu-id="3b48f-109">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="3b48f-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="3b48f-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="3b48f-110">Script explanation</span></span>

<span data-ttu-id="3b48f-111">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="3b48f-111">This script uses hello following commands.</span></span> <span data-ttu-id="3b48f-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="3b48f-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3b48f-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="3b48f-113">Command</span></span> | <span data-ttu-id="3b48f-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="3b48f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3b48f-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3b48f-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3b48f-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="3b48f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3b48f-117">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3b48f-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="3b48f-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="3b48f-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="3b48f-119">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3b48f-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="3b48f-120">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="3b48f-120">Creates a web app.</span></span> |
| [<span data-ttu-id="3b48f-121">Zestaw AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="3b48f-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="3b48f-122">Modyfikuje jego warstwy cenowej toochange planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3b48f-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="3b48f-123">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="3b48f-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="3b48f-124">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="3b48f-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3b48f-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3b48f-125">Next steps</span></span>

<span data-ttu-id="3b48f-126">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3b48f-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3b48f-127">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3b48f-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
