---
title: "Przykładowy skrypt programu PowerShell Azure — monitorowanie aplikacji sieci web z dziennikami serwera sieci web | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 34a3dd318cb9896342fce870922ecd113b3ed08d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="c5bb7-103">Monitorowanie aplikacji sieci web z dziennikami serwera sieci web</span><span class="sxs-lookup"><span data-stu-id="c5bb7-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="c5bb7-104">W tym scenariuszu utworzysz grupy zasobów, plan usługi aplikacji, aplikacji sieci web i konfigurowanie aplikacji sieci web, aby włączyć dzienniki serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="c5bb7-105">Następnie pobierze pliki dzienników w celu przeglądu.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-105">You will then download the log files for review.</span></span>

<span data-ttu-id="c5bb7-106">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c5bb7-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="c5bb7-107">Sample script</span></span>

<span data-ttu-id="c5bb7-108">[!code-powershell[główne](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "monitorowania aplikacji sieci web z dziennikami serwera sieci web")]</span><span class="sxs-lookup"><span data-stu-id="c5bb7-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c5bb7-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c5bb7-109">Clean up deployment</span></span> 

<span data-ttu-id="c5bb7-110">Po uruchomieniu przykładowym skrypcie następującego polecenia można usunąć grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="c5bb7-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="c5bb7-111">Script explanation</span></span>

<span data-ttu-id="c5bb7-112">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-112">This script uses the following commands.</span></span> <span data-ttu-id="c5bb7-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c5bb7-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="c5bb7-114">Command</span></span> | <span data-ttu-id="c5bb7-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c5bb7-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c5bb7-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c5bb7-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c5bb7-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c5bb7-118">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c5bb7-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c5bb7-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c5bb7-120">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c5bb7-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c5bb7-121">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-121">Creates a web app.</span></span> |
| [<span data-ttu-id="c5bb7-122">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c5bb7-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="c5bb7-123">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-123">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="c5bb7-124">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="c5bb7-124">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="c5bb7-125">Pobiera metryki aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="c5bb7-125">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c5bb7-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5bb7-126">Next steps</span></span>

<span data-ttu-id="c5bb7-127">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c5bb7-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c5bb7-128">Dodatkowe przykłady programu Powershell systemu Azure dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c5bb7-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
