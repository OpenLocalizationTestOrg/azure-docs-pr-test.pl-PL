---
title: "aaaCreate serwerem usług Azure Analysis Services przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Azure Analysis Services serwera przy użyciu programu PowerShell"
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
ms.openlocfilehash: 269b78983410f773d47c4cea34d6d353b19f9e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-by-using-powershell"></a><span data-ttu-id="cb2da-103">Tworzenie serwera usług Azure Analysis Services przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb2da-103">Create an Azure Analysis Services server by using PowerShell</span></span>

<span data-ttu-id="cb2da-104">Tego przewodnika Szybki Start zawiera opis korzystania ze środowiska PowerShell z toocreate wiersza polecenia hello serwerem usług Azure Analysis Services w [grupy zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cb2da-104">This quickstart describes using PowerShell from hello command line toocreate an Azure Analysis Services server in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in your Azure subscription.</span></span>

<span data-ttu-id="cb2da-105">Dla tego zadania jest wymagany moduł Azure PowerShell w wersji 4.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cb2da-105">This task requires Azure PowerShell module version 4.0 or later.</span></span> <span data-ttu-id="cb2da-106">Wersja hello toofind, uruchom ` Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="cb2da-106">toofind hello version, run ` Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="cb2da-107">tooinstall lub uaktualniania, zobacz [modułu instalacji programu Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="cb2da-107">tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 

> [!NOTE]
> <span data-ttu-id="cb2da-108">Utworzenie serwera może skutkować powstaniem nowej usługi płatnej.</span><span class="sxs-lookup"><span data-stu-id="cb2da-108">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="cb2da-109">toolearn więcej, zobacz [cennik usług Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="cb2da-109">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb2da-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cb2da-110">Prerequisites</span></span>
<span data-ttu-id="cb2da-111">toocomplete tego przewodnika Szybki Start, należy:</span><span class="sxs-lookup"><span data-stu-id="cb2da-111">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="cb2da-112">**Subskrypcja platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate konta.</span><span class="sxs-lookup"><span data-stu-id="cb2da-112">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="cb2da-113">**Azure Active Directory**: subskrypcja musi być skojarzona z dzierżawą usługi Azure Active Directory i musisz mieć konto w tym katalogu.</span><span class="sxs-lookup"><span data-stu-id="cb2da-113">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant and you must have an account in that directory.</span></span> <span data-ttu-id="cb2da-114">toolearn więcej, zobacz [uprawnienia do uwierzytelniania i użytkownik](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="cb2da-114">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>

## <a name="import-azurermanalysisservices-module"></a><span data-ttu-id="cb2da-115">Importowanie modułu AzureRm.AnalysisServices</span><span class="sxs-lookup"><span data-stu-id="cb2da-115">Import AzureRm.AnalysisServices module</span></span>
<span data-ttu-id="cb2da-116">toocreate serwera w ramach subskrypcji, użyj hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices) składnika modułu.</span><span class="sxs-lookup"><span data-stu-id="cb2da-116">toocreate a server in your subscription, you use hello [AzureRM.AnalysisServices](https://www.powershellgallery.com/packages/AzureRM.AnalysisServices)  component module.</span></span> <span data-ttu-id="cb2da-117">Załaduj moduł AzureRm.AnalysisServices hello do sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cb2da-117">Load hello AzureRm.AnalysisServices module into your PowerShell session.</span></span>

```powershell
Import-Module AzureRM.AnalysisServices
```

## <a name="sign-in-tooazure"></a><span data-ttu-id="cb2da-118">Zaloguj się tooAzure</span><span class="sxs-lookup"><span data-stu-id="cb2da-118">Sign in tooAzure</span></span>

<span data-ttu-id="cb2da-119">Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) polecenia.</span><span class="sxs-lookup"><span data-stu-id="cb2da-119">Sign in tooyour Azure subscription by using hello [Add-AzureRmAccount](/powershell/module/azurerm.profile/add-azurermaccount) command.</span></span> <span data-ttu-id="cb2da-120">Wykonaj hello wyświetlanymi instrukcjami.</span><span class="sxs-lookup"><span data-stu-id="cb2da-120">Follow hello on-screen directions.</span></span>

```powershell
Add-AzureRmAccount
```

## <a name="create-a-resource-group"></a><span data-ttu-id="cb2da-121">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="cb2da-121">Create a resource group</span></span>
 
<span data-ttu-id="cb2da-122">[Grupa zasobów platformy Azure](../azure-resource-manager/resource-group-overview.md) to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi w formie grupy.</span><span class="sxs-lookup"><span data-stu-id="cb2da-122">An [Azure resource group](../azure-resource-manager/resource-group-overview.md) is a logical container where Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="cb2da-123">Podczas tworzenia serwera musisz podać grupę zasobów w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cb2da-123">When you create your server, you must specify a resource group in your subscription.</span></span> <span data-ttu-id="cb2da-124">Jeśli nie masz już grupę zasobów, można utworzyć nową przy użyciu hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia.</span><span class="sxs-lookup"><span data-stu-id="cb2da-124">If you do not already have a resource group, you can create a new one by using hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="cb2da-125">Witaj poniższy przykład tworzy grupę zasobów o nazwie `myResourceGroup` hello regionu zachodnie stany USA.</span><span class="sxs-lookup"><span data-stu-id="cb2da-125">hello following example creates a resource group named `myResourceGroup` in hello West US region.</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "West US"
```

## <a name="create-a-server"></a><span data-ttu-id="cb2da-126">Tworzenie serwera</span><span class="sxs-lookup"><span data-stu-id="cb2da-126">Create a server</span></span>

<span data-ttu-id="cb2da-127">Tworzenie nowego serwera przy użyciu hello [AzureRmAnalysisServicesServer nowy](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) polecenia.</span><span class="sxs-lookup"><span data-stu-id="cb2da-127">Create a new server by using hello [New-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="cb2da-128">Witaj poniższy przykład tworzy serwer o nazwie MójSerwer w myResourceGroup w hello regionu zachodnie stany USA, w warstwie hello D1 i określa philipc@adventureworks.com jako administrator serwera.</span><span class="sxs-lookup"><span data-stu-id="cb2da-128">hello following example creates a server named myServer in myResourceGroup, in hello West US region, at hello D1 tier, and specifies philipc@adventureworks.com as a server administrator.</span></span>

```powershell
New-AzureRmAnalysisServicesServer -ResourceGroupName "myResourceGroup" -Name "myServer" -Location West US -Sku D1 -Administrator "philipc@adventure-works.com"
```

## <a name="clean-up-resources"></a><span data-ttu-id="cb2da-129">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="cb2da-129">Clean up resources</span></span>

<span data-ttu-id="cb2da-130">Można usunąć serwera hello z subskrypcji przy użyciu hello [AzureRmAnalysisServicesServer Usuń](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) polecenia.</span><span class="sxs-lookup"><span data-stu-id="cb2da-130">You can remove hello server from your subscription by using hello [Remove-AzureRmAnalysisServicesServer](/powershell/module/azurerm.analysisservices/new-azurermanalysisservicesserver) command.</span></span> <span data-ttu-id="cb2da-131">Jeśli będziesz korzystać z innych przewodników Szybki start i samouczków w tej kolekcji, nie usuwaj serwera.</span><span class="sxs-lookup"><span data-stu-id="cb2da-131">If you continue with other quickstarts and tutorials in this collection, do not remove your server.</span></span> <span data-ttu-id="cb2da-132">Witaj poniższy przykład umożliwia usunięcie serwera hello utworzony w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="cb2da-132">hello following example removes hello server created in hello previous step.</span></span>


```powershell
Remove-AzureRmAnalysisServicesServer -Name "myServer" -ResourceGroupName "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="cb2da-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cb2da-133">Next steps</span></span>
<span data-ttu-id="cb2da-134">[Zarządzanie usługami Azure Analysis Services przy użyciu programu PowerShell](analysis-services-powershell.md) </span><span class="sxs-lookup"><span data-stu-id="cb2da-134">[Manage Azure Analysis Services with PowerShell](analysis-services-powershell.md) </span></span>  
<span data-ttu-id="cb2da-135">[Wdrażanie modelu w programie SSDT](analysis-services-deploy.md) </span><span class="sxs-lookup"><span data-stu-id="cb2da-135">[Deploy a model from SSDT](analysis-services-deploy.md) </span></span>  
[<span data-ttu-id="cb2da-136">Create a model in Azure portal (preview) (Tworzenie modelu w wersji zapoznawczej witryny Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="cb2da-136">Create a model in Azure portal</span></span>](analysis-services-create-model-portal.md)