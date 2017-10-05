---
title: "Skrypt programu PowerShell Azure przykładowe — łączenie aplikacji sieci web z konta magazynu | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — łączenie aplikacji sieci web z konta magazynu"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 481f3efdb1cbbeba328183da7e320c7e5b819b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="22317-103">Łączenie aplikacji sieci web z konta magazynu</span><span class="sxs-lookup"><span data-stu-id="22317-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="22317-104">W tym scenariuszu dowiesz się, jak utworzyć konto magazynu platformy Azure i aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="22317-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="22317-105">Następnie połączy konta magazynu do aplikacji sieci web, przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="22317-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="22317-106">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="22317-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="22317-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="22317-107">Sample script</span></span>

<span data-ttu-id="22317-108">[!code-powershell[główne](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "łączenie aplikacji sieci web z konta magazynu")]</span><span class="sxs-lookup"><span data-stu-id="22317-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="22317-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="22317-109">Clean up deployment</span></span> 

<span data-ttu-id="22317-110">Po uruchomieniu przykładowym skrypcie następującego polecenia można usunąć grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="22317-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="22317-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="22317-111">Script explanation</span></span>

<span data-ttu-id="22317-112">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="22317-112">This script uses the following commands.</span></span> <span data-ttu-id="22317-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="22317-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="22317-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="22317-114">Command</span></span> | <span data-ttu-id="22317-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="22317-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="22317-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="22317-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="22317-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="22317-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="22317-118">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="22317-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="22317-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="22317-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="22317-120">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="22317-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="22317-121">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="22317-121">Creates a web app.</span></span> |
| [<span data-ttu-id="22317-122">Nowe AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="22317-122">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="22317-123">Tworzy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="22317-123">Creates a Storage account.</span></span> |
| [<span data-ttu-id="22317-124">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="22317-124">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="22317-125">Pobiera klucze dostępu dla konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="22317-125">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="22317-126">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="22317-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="22317-127">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="22317-127">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="22317-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22317-128">Next steps</span></span>

<span data-ttu-id="22317-129">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22317-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="22317-130">Dodatkowe przykłady programu Powershell systemu Azure dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="22317-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
