---
title: "Tworzenie serwera usług Analysis Services na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć wystąpienie serwera usług Analysis Services na platformie Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 95b367e7cd74405088190c1fe19cf92990759d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="9e06e-103">Tworzenie serwera usług Azure Analysis Services w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9e06e-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="9e06e-104">W tym artykule przedstawiono tworzenie zasobu serwera usług Analysis Services w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9e06e-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9e06e-105">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="9e06e-105">Before you begin</span></span>
<span data-ttu-id="9e06e-106">Aby ukończyć ten przewodnik Szybki Start, musisz spełnić następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="9e06e-106">To complete this quickstart, you need:</span></span>

* <span data-ttu-id="9e06e-107">**Subskrypcja platformy Azure**: odwiedź stronę [bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/offers/ms-azr-0044p/), aby utworzyć konto.</span><span class="sxs-lookup"><span data-stu-id="9e06e-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) to create an account.</span></span>
* <span data-ttu-id="9e06e-108">**Usługa Azure Active Directory**: subskrypcji musi być skojarzony z dzierżawy usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e06e-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="9e06e-109">A, musisz być zalogowany na platformie Azure przy użyciu konta w tej usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e06e-109">And, you need to be signed in to Azure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="9e06e-110">Konta Microsoft nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="9e06e-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="9e06e-111">Aby dowiedzieć się więcej, zobacz [Authentication and user permissions (Uwierzytelnianie i uprawnienia użytkownika)](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="9e06e-111">To learn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="9e06e-112">**Grupa zasobów**: Użyj masz już grupę zasobów lub [Utwórz nową](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e06e-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9e06e-113">Utworzenie serwera może skutkować powstaniem nowej usługi płatnej.</span><span class="sxs-lookup"><span data-stu-id="9e06e-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="9e06e-114">Aby dowiedzieć się więcej, zobacz [cennik usług Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="9e06e-114">To learn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="to-create-a-server-in-azure-portal"></a><span data-ttu-id="9e06e-115">Aby utworzyć serwer w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9e06e-115">To create a server in Azure portal</span></span>
1. <span data-ttu-id="9e06e-116">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9e06e-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="9e06e-117">Kliknij przycisk **+ nowy** > **dane i analiza** > **usług Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="9e06e-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="9e06e-118">W **usług Analysis Services** bloku, wypełnij wymagane pola, a następnie naciśnij klawisz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9e06e-118">In the **Analysis Services** blade, fill in the required fields, and then press **Create**.</span></span>
   
    ![Tworzenie serwera](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="9e06e-120">**Nazwa serwera**: wpisz unikatową nazwę używany do serwera.</span><span class="sxs-lookup"><span data-stu-id="9e06e-120">**Server name**: Type a unique name used to reference the server.</span></span>
   * <span data-ttu-id="9e06e-121">**Subskrypcja**: Wybierz subskrypcję rachunków tego serwera do.</span><span class="sxs-lookup"><span data-stu-id="9e06e-121">**Subscription**: Select the subscription this server bills to.</span></span>
   * <span data-ttu-id="9e06e-122">**Grupa zasobów**: zaprojektowano kontenery ułatwiające zarządzanie kolekcją zasobów systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="9e06e-122">**Resource group**: These containers are designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="9e06e-123">Aby dowiedzieć się więcej, zobacz [grup zasobów](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e06e-123">To learn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="9e06e-124">**Lokalizacja**: Lokalizacja centrum danych Azure ten obsługuje serwer.</span><span class="sxs-lookup"><span data-stu-id="9e06e-124">**Location**: This Azure datacenter location hosts the server.</span></span> <span data-ttu-id="9e06e-125">Wybierz lokalizację najbliżej największy bazy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9e06e-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="9e06e-126">**Warstwa cenowa**: Wybierz warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="9e06e-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="9e06e-127">Maksymalnie 400 GB modele tabelaryczne są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="9e06e-127">Tabular models up to 400 GB are supported.</span></span> <span data-ttu-id="9e06e-128">Aby dowiedzieć się więcej, zobacz [cennik usług Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="9e06e-128">To learn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="9e06e-129">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9e06e-129">Click **Create**.</span></span>

<span data-ttu-id="9e06e-130">Utwórz potrzebuje zazwyczaj w obszarze chwilę. często tylko kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="9e06e-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="9e06e-131">W przypadku wybrania **dodać do portalu**, przejdź do portalu w taki sposób, aby wyświetlić nowy serwer.</span><span class="sxs-lookup"><span data-stu-id="9e06e-131">If you selected **Add to Portal**, navigate to your portal to see your new server.</span></span> <span data-ttu-id="9e06e-132">Lub przejdź do **więcej usług** > **usług Analysis Services** czy serwer jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="9e06e-132">Or, navigate to **More services** > **Analysis Services** to see if your server is ready.</span></span>

 ![Pulpit nawigacyjny](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="9e06e-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9e06e-134">Next steps</span></span>
<span data-ttu-id="9e06e-135">Po utworzeniu serwera, możesz [wdrożenia modelu](analysis-services-deploy.md) do niej przy użyciu narzędzi SSDT lub SSMS.</span><span class="sxs-lookup"><span data-stu-id="9e06e-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) to it by using SSDT or with SSMS.</span></span>

<span data-ttu-id="9e06e-136">Jeśli model wdrażania na serwerze nawiązuje połączenie z lokalnych źródeł danych, musisz zainstalować [bramy danych lokalnych](analysis-services-gateway.md) na komputerze w sieci.</span><span class="sxs-lookup"><span data-stu-id="9e06e-136">If a model you deploy to your server connects to on-premises data sources, you need to install an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

