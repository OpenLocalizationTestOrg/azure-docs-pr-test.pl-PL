---
title: "Przykładowy skrypt programu PowerShell - aaaAzure powiązać niestandardowej aplikacji sieci web tooa certyfikatu SSL | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure — Bind niestandardowej aplikacji sieci web tooa certyfikat SSL"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="2356e-103">Powiąż niestandardowej aplikacji sieci web tooa certyfikat protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="2356e-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="2356e-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie powiązania certyfikatu SSL hello tooit nazwy domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="2356e-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="2356e-105">Jeśli to konieczne, zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2356e-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="2356e-106">Ponadto upewnij się, że:</span><span class="sxs-lookup"><span data-stu-id="2356e-106">Also, ensure that:</span></span>

- <span data-ttu-id="2356e-107">Utworzono połączenie z platformą Azure, za pomocą hello `az login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="2356e-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="2356e-108">Masz strony konfiguracji rejestratora dostępu tooyour domen DNS.</span><span class="sxs-lookup"><span data-stu-id="2356e-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="2356e-109">Masz prawidłowe. Plik PFX i jego hasło dla hello SSL certyfikatów można mają tooupload i ich powiązania.</span><span class="sxs-lookup"><span data-stu-id="2356e-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="2356e-110">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="2356e-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2356e-111">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="2356e-111">Clean up deployment</span></span> 

<span data-ttu-id="2356e-112">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="2356e-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="2356e-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="2356e-113">Script explanation</span></span>

<span data-ttu-id="2356e-114">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="2356e-114">This script uses hello following commands.</span></span> <span data-ttu-id="2356e-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="2356e-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2356e-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="2356e-116">Command</span></span> | <span data-ttu-id="2356e-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2356e-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2356e-118">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2356e-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2356e-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="2356e-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2356e-120">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="2356e-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="2356e-121">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="2356e-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2356e-122">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="2356e-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="2356e-123">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="2356e-123">Creates a web app.</span></span> |
| [<span data-ttu-id="2356e-124">Zestaw AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="2356e-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="2356e-125">Modyfikuje jego warstwy cenowej toochange planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2356e-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="2356e-126">Zestaw AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="2356e-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="2356e-127">Modyfikuje konfigurację aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="2356e-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="2356e-128">Nowe AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="2356e-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="2356e-129">Tworzy powiązanie certyfikatu SSL dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="2356e-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2356e-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2356e-130">Next steps</span></span>

<span data-ttu-id="2356e-131">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2356e-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2356e-132">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2356e-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
