---
title: "Skrypt programu PowerShell Azure przykładowe — ręcznie skalować aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — ręcznie skalować aplikacji sieci web"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="42d82-103">Ręcznie skalować aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="42d82-103">Scale a web app manually</span></span>

<span data-ttu-id="42d82-104">W tym scenariuszu przedstawiono tworzenie grupy zasobów, aplikacji sieci web i plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42d82-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="42d82-105">Zostanie następnie skalowanie planu usługi App Service z pojedynczym wystąpieniem do wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="42d82-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="42d82-106">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="42d82-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="42d82-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="42d82-107">Sample script</span></span>

<span data-ttu-id="42d82-108">[!code-powershell[główne](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "ręcznie skalować aplikacji sieci web")]</span><span class="sxs-lookup"><span data-stu-id="42d82-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="42d82-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="42d82-109">Clean up deployment</span></span> 

<span data-ttu-id="42d82-110">Po uruchomieniu przykładowym skrypcie następującego polecenia można usunąć grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="42d82-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="42d82-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="42d82-111">Script explanation</span></span>

<span data-ttu-id="42d82-112">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="42d82-112">This script uses the following commands.</span></span> <span data-ttu-id="42d82-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="42d82-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="42d82-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="42d82-114">Command</span></span> | <span data-ttu-id="42d82-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="42d82-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="42d82-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="42d82-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="42d82-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="42d82-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="42d82-118">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="42d82-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="42d82-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="42d82-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="42d82-120">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="42d82-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="42d82-121">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="42d82-121">Creates a web app.</span></span> |
| [<span data-ttu-id="42d82-122">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="42d82-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="42d82-123">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="42d82-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="42d82-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42d82-124">Next steps</span></span>

<span data-ttu-id="42d82-125">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="42d82-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="42d82-126">Dodatkowe przykłady programu Powershell systemu Azure dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="42d82-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
