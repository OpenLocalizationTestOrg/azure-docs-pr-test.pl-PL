---
title: "aaaAzure przykładowy skrypt programu PowerShell — monitorowanie aplikacji sieci web z dziennikami serwera sieci web | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure — monitorowanie aplikacji sieci web z dziennikami serwera sieci web"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: efaae1e19f5153e33d1f5d5decadb9f6c4649f8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="07778-103">Monitorowanie aplikacji sieci web z dziennikami serwera sieci web</span><span class="sxs-lookup"><span data-stu-id="07778-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="07778-104">W tym scenariuszu utworzysz grupy zasobów, plan usługi aplikacji, aplikacji sieci web i konfigurowanie aplikacji sieci web hello tooenable dzienniki serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="07778-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="07778-105">Następnie pobierze pliki dziennika hello do przeglądu.</span><span class="sxs-lookup"><span data-stu-id="07778-105">You will then download hello log files for review.</span></span>

<span data-ttu-id="07778-106">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="07778-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="07778-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="07778-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]

## <a name="clean-up-deployment"></a><span data-ttu-id="07778-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="07778-108">Clean up deployment</span></span> 

<span data-ttu-id="07778-109">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="07778-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="07778-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="07778-110">Script explanation</span></span>

<span data-ttu-id="07778-111">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="07778-111">This script uses hello following commands.</span></span> <span data-ttu-id="07778-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="07778-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="07778-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="07778-113">Command</span></span> | <span data-ttu-id="07778-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="07778-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="07778-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="07778-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="07778-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="07778-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="07778-117">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="07778-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="07778-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="07778-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="07778-119">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="07778-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="07778-120">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="07778-120">Creates a web app.</span></span> |
| [<span data-ttu-id="07778-121">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="07778-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="07778-122">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="07778-122">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="07778-123">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="07778-123">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="07778-124">Pobiera metryki aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="07778-124">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="07778-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="07778-125">Next steps</span></span>

<span data-ttu-id="07778-126">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07778-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="07778-127">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="07778-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
