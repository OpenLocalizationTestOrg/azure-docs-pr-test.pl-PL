---
title: "Tworzenie serwera usług Azure Analysis Services przy użyciu programu PowerShell | Microsoft Docs"
description: "Dowiedz się, jak utworzyć serwer usług Azure Analysis Services przy użyciu programu PowerShell"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/01/2017
ms.author: owend
ms.custom: mvc
ms.openlocfilehash: cb42fd3ed51364cf478848cc51ebbb2f175e96d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="01c4f-103">Tworzenie serwera usług Azure Analysis Services przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="01c4f-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="01c4f-104">Ten przewodnik Szybki start opisano, jak utworzyć serwer usług Azure Analysis Services przy użyciu programu PowerShell z poziomu wiersza polecenia w [grupie zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="01c4f-104">This quickstart describes using PowerShell from the command line to create an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="01c4f-105">Dla tego zadania jest wymagany moduł Azure PowerShell w wersji 4.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="01c4f-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="01c4f-106">Aby dowiedzieć się, jaka wersja jest używana, uruchom polecenie ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="01c4f-106">To find the version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="01c4f-107">Aby przeprowadzić instalację lub uaktualnienie, zobacz [Instalowanie modułu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="01c4f-107">To install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="01c4f-108">Utworzenie serwera może skutkować powstaniem nowej usługi płatnej.</span><span class="sxs-lookup"><span data-stu-id="01c4f-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="01c4f-109">Aby dowiedzieć się więcej, zobacz [cennik usług Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="01c4f-109">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01c4f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="01c4f-110">Prerequisites</span></span>
<span data-ttu-id="01c4f-111">Aby ukończyć ten przewodnik Szybki Start, musisz spełnić następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="01c4f-111">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="01c4f-112">**Subskrypcja platformy Azure**: odwiedź stronę [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/offers/ms-azr-0044p/), aby utworzyć konto.</span><span class="sxs-lookup"><span data-stu-id="01c4f-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="01c4f-113">**Azure Active Directory**: subskrypcja musi być skojarzona z dzierżawą usługi Azure Active Directory i musisz mieć konto w tym katalogu.</span><span class="sxs-lookup"><span data-stu-id="01c4f-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="01c4f-114">Aby dowiedzieć się więcej, zobacz [Authentication and user permissions (Uwierzytelnianie i uprawnienia użytkownika)](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="01c4f-114">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="01c4f-115">Importowanie modułu AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="01c4f-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="01c4f-116">Aby utworzyć serwer w ramach subskrypcji, należy użyć modułu składnika [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices).</span><span class="sxs-lookup"><span data-stu-id="01c4f-116">To create a server in your subscription, you use the [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="01c4f-117">Załaduj moduł AzureRm.AnalysisServices w sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01c4f-117">Load the AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-to-azure"></a><span data-ttu-id="01c4f-118">Logowanie do platformy Azure</span><span class="sxs-lookup"><span data-stu-id="01c4f-118">Sign in to Azure</span></span>

<span data-ttu-id="01c4f-119">Zaloguj się do subskrypcji platformy Azure przy użyciu polecenia [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount).</span><span class="sxs-lookup"><span data-stu-id="01c4f-119">Sign in to your Azure subscription by using the [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="01c4f-120">Postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.</span><span class="sxs-lookup"><span data-stu-id="01c4f-120">Follow the on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="01c4f-121">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="01c4f-121">Create a resource group</span></span>
 
<span data-ttu-id="01c4f-122">[Grupa zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="01c4f-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="01c4f-123">Podczas tworzenia serwera musisz podać grupę zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="01c4f-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="01c4f-124">Jeśli nie masz jeszcze grupy zasobów, możesz ją utworzyć teraz przy użyciu polecenia [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="01c4f-124">If you do not already have a resource group, you can create a new one by using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="01c4f-125">Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie `myResourceGroup` w regionie Zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="01c4f-125">The following example creates a resource group named `myResourceGroup` in the West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="01c4f-126">Tworzenie serwera</span><span class="sxs-lookup"><span data-stu-id="01c4f-126">Create a server</span></span>

<span data-ttu-id="01c4f-127">Utwórz nowy serwer przy użyciu polecenia [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="01c4f-127">Create a new server by using the [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="01c4f-128">W poniższym przykładzie utworzono serwer o nazwie myServer w grupie myResourceGroup w regionie Zachodnie stany USA w warstwie D1 i określono użytkownika philipc@adventureworks.com jako administratora serwera.</span><span class="sxs-lookup"><span data-stu-id="01c4f-128">The following example creates a server named myServer in myResourceGroup, in the West US region, at the D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="01c4f-129">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="01c4f-129">Clean up resources</span></span>

<span data-ttu-id="01c4f-130">Możesz usunąć serwer z subskrypcji przy użyciu polecenia [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver).</span><span class="sxs-lookup"><span data-stu-id="01c4f-130">You can remove the server from your subscription by using the [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="01c4f-131">Jeśli będziesz korzystać z innych przewodników Szybki start i samouczków w tej kolekcji, nie usuwaj serwera.</span><span class="sxs-lookup"><span data-stu-id="01c4f-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="01c4f-132">Poniższy przykład obejmuje usuwanie serwera utworzonego w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="01c4f-132">The following example removes the server created in the previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="01c4f-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="01c4f-133">Next steps</span></span>
<span data-ttu-id="01c4f-134">[Zarządzanie usługami Azure Analysis Services przy użyciu programu PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="01c4f-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="01c4f-135">[Wdrażanie modelu w programie SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="01c4f-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="01c4f-136">Create a model in Azure portal (preview) (Tworzenie modelu w wersji zapoznawczej witryny Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="01c4f-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)