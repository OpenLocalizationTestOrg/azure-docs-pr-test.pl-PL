---
title: "Przykładowy skrypt programu PowerShell - przekazywania plików tooa aplikacji sieci web za pomocą protokołu FTP aaaAzure | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - przekazywania plików tooa aplikacji sieci web za pomocą protokołu FTP"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="76d4f-103">Przekaż aplikację sieci web tooa plików za pomocą protokołu FTP</span><span class="sxs-lookup"><span data-stu-id="76d4f-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="76d4f-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web za pomocą protokołu FTP (za pośrednictwem [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="76d4f-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="76d4f-105">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="76d4f-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="76d4f-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="76d4f-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="76d4f-107">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="76d4f-107">Clean up deployment</span></span> 

<span data-ttu-id="76d4f-108">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="76d4f-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="76d4f-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="76d4f-109">Script explanation</span></span>

<span data-ttu-id="76d4f-110">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="76d4f-110">This script uses hello following commands.</span></span> <span data-ttu-id="76d4f-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="76d4f-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="76d4f-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="76d4f-112">Command</span></span> | <span data-ttu-id="76d4f-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="76d4f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="76d4f-114">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="76d4f-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="76d4f-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="76d4f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="76d4f-116">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="76d4f-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="76d4f-117">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="76d4f-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="76d4f-118">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="76d4f-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="76d4f-119">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="76d4f-119">Creates a web app.</span></span> |
| [<span data-ttu-id="76d4f-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="76d4f-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="76d4f-121">Pobierz profil publikowania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="76d4f-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="76d4f-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="76d4f-122">Next steps</span></span>

<span data-ttu-id="76d4f-123">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="76d4f-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="76d4f-124">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="76d4f-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
