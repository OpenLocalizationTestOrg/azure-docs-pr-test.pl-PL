---
title: "Przykładowy skrypt programu PowerShell - aaaAzure połączyć konto magazynu tooa aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — Połącz konto magazynu tooa aplikacji sieci web"
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
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="f1fd1-103">Połącz z kontem magazynu tooa aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="f1fd1-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="f1fd1-104">W tym scenariuszu dowiesz się, jak toocreate konto usługi Azure storage i Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="f1fd1-105">Następnie zostanie Połącz hello magazynu konta toohello web app przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="f1fd1-106">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f1fd1-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f1fd1-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f1fd1-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="f1fd1-108">Clean up deployment</span></span> 

<span data-ttu-id="f1fd1-109">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f1fd1-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f1fd1-110">Script explanation</span></span>

<span data-ttu-id="f1fd1-111">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-111">This script uses hello following commands.</span></span> <span data-ttu-id="f1fd1-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f1fd1-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f1fd1-113">Command</span></span> | <span data-ttu-id="f1fd1-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f1fd1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f1fd1-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f1fd1-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f1fd1-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f1fd1-117">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f1fd1-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f1fd1-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f1fd1-119">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f1fd1-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f1fd1-120">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-120">Creates a web app.</span></span> |
| [<span data-ttu-id="f1fd1-121">Nowe AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="f1fd1-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="f1fd1-122">Tworzy konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="f1fd1-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="f1fd1-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="f1fd1-124">Pobiera hello klucze dostępu dla konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="f1fd1-125">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f1fd1-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="f1fd1-126">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="f1fd1-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f1fd1-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f1fd1-127">Next steps</span></span>

<span data-ttu-id="f1fd1-128">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1fd1-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f1fd1-129">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f1fd1-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
