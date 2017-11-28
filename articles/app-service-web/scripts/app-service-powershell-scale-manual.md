---
title: "Przykładowy skrypt programu PowerShell - aaaAzure skalowanie aplikacji sieci web ręcznie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="64ebf-103">Ręcznie skalować aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="64ebf-103">Scale a web app manually</span></span>

<span data-ttu-id="64ebf-104">W tym scenariuszu dowiesz się toocreate grupę zasobów aplikacji sieci web i plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="64ebf-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="64ebf-105">Następnie będzie skalować hello planu usługi App Service z wystąpień toomultiple pojedynczego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="64ebf-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="64ebf-106">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="64ebf-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="64ebf-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="64ebf-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="64ebf-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="64ebf-108">Clean up deployment</span></span> 

<span data-ttu-id="64ebf-109">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="64ebf-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="64ebf-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="64ebf-110">Script explanation</span></span>

<span data-ttu-id="64ebf-111">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="64ebf-111">This script uses hello following commands.</span></span> <span data-ttu-id="64ebf-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="64ebf-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="64ebf-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="64ebf-113">Command</span></span> | <span data-ttu-id="64ebf-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="64ebf-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="64ebf-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="64ebf-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="64ebf-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="64ebf-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="64ebf-117">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="64ebf-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="64ebf-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="64ebf-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="64ebf-119">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="64ebf-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="64ebf-120">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="64ebf-120">Creates a web app.</span></span> |
| [<span data-ttu-id="64ebf-121">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="64ebf-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="64ebf-122">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="64ebf-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="64ebf-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="64ebf-123">Next steps</span></span>

<span data-ttu-id="64ebf-124">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="64ebf-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="64ebf-125">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="64ebf-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
