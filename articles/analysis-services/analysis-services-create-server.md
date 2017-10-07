---
title: "aaaCreate serwerem usług Analysis Services na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wystąpienie toocreate serwerem usług Analysis Services na platformie Azure."
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
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a><span data-ttu-id="070ba-103">Tworzenie serwera usług Azure Analysis Services w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="070ba-103">Create an Azure Analysis Services server in Azure portal</span></span>
<span data-ttu-id="070ba-104">W tym artykule przedstawiono tworzenie zasobu serwera usług Analysis Services w ramach subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="070ba-104">This article walks you through creating an Analysis Services server resource in your Azure subscription.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="070ba-105">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="070ba-105">Before you begin</span></span>
<span data-ttu-id="070ba-106">toocomplete tego przewodnika Szybki Start, należy:</span><span class="sxs-lookup"><span data-stu-id="070ba-106">toocomplete this quickstart, you need:</span></span>

* <span data-ttu-id="070ba-107">**Subskrypcja platformy Azure**: odwiedź [bezpłatnej wersji próbnej Azure](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate konta.</span><span class="sxs-lookup"><span data-stu-id="070ba-107">**Azure subscription**: Visit [Azure Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) toocreate an account.</span></span>
* <span data-ttu-id="070ba-108">**Usługa Azure Active Directory**: subskrypcji musi być skojarzony z dzierżawy usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="070ba-108">**Azure Active Directory**: Your subscription must be associated with an Azure Active Directory tenant.</span></span> <span data-ttu-id="070ba-109">I należy toobe zalogowany tooAzure przy użyciu konta w tej usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="070ba-109">And, you need toobe signed in tooAzure with an account in that Azure Active Directory.</span></span> <span data-ttu-id="070ba-110">Konta Microsoft nie są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="070ba-110">Microsoft accounts are not supported.</span></span> <span data-ttu-id="070ba-111">toolearn więcej, zobacz [uprawnienia do uwierzytelniania i użytkownik](analysis-services-manage-users.md).</span><span class="sxs-lookup"><span data-stu-id="070ba-111">toolearn more, see [Authentication and user permissions](analysis-services-manage-users.md).</span></span>
* <span data-ttu-id="070ba-112">**Grupa zasobów**: Użyj masz już grupę zasobów lub [Utwórz nową](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="070ba-112">**Resource group**: Use a resource group you already have or [create a new one](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="070ba-113">Utworzenie serwera może skutkować powstaniem nowej usługi płatnej.</span><span class="sxs-lookup"><span data-stu-id="070ba-113">Creating a server might result in a new billable service.</span></span> <span data-ttu-id="070ba-114">toolearn więcej, zobacz [cennik usług Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="070ba-114">toolearn more, see [Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a><span data-ttu-id="070ba-115">toocreate serwera w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="070ba-115">toocreate a server in Azure portal</span></span>
1. <span data-ttu-id="070ba-116">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="070ba-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="070ba-117">Kliknij przycisk **+ nowy** > **dane i analiza** > **usług Analysis Services**.</span><span class="sxs-lookup"><span data-stu-id="070ba-117">Click **+ New** > **Data + analytics** > **Analysis Services**.</span></span>
3. <span data-ttu-id="070ba-118">W hello **usług Analysis Services** bloku, wypełnij pola hello wymagane, a następnie naciśnij klawisz **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="070ba-118">In hello **Analysis Services** blade, fill in hello required fields, and then press **Create**.</span></span>
   
    ![Tworzenie serwera](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * <span data-ttu-id="070ba-120">**Nazwa serwera**: wpisz unikatową nazwę używaną tooreference powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="070ba-120">**Server name**: Type a unique name used tooreference hello server.</span></span>
   * <span data-ttu-id="070ba-121">**Subskrypcja**: Wybierz subskrypcję hello rachunków tego serwera do.</span><span class="sxs-lookup"><span data-stu-id="070ba-121">**Subscription**: Select hello subscription this server bills to.</span></span>
   * <span data-ttu-id="070ba-122">**Grupa zasobów**: kontenery są zaprojektowane toohelp zarządzanie kolekcją zasobów systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="070ba-122">**Resource group**: These containers are designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="070ba-123">toolearn więcej, zobacz [grup zasobów](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="070ba-123">toolearn more, see [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="070ba-124">**Lokalizacja**: hostów lokalizację centrum danych Azure to hello serwera.</span><span class="sxs-lookup"><span data-stu-id="070ba-124">**Location**: This Azure datacenter location hosts hello server.</span></span> <span data-ttu-id="070ba-125">Wybierz lokalizację najbliżej największy bazy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="070ba-125">Choose a location nearest your largest user base.</span></span>
   * <span data-ttu-id="070ba-126">**Warstwa cenowa**: Wybierz warstwę cenową.</span><span class="sxs-lookup"><span data-stu-id="070ba-126">**Pricing tier**: Select a pricing tier.</span></span> <span data-ttu-id="070ba-127">Modele tabelaryczne zapasowej too400 GB są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="070ba-127">Tabular models up too400 GB are supported.</span></span> <span data-ttu-id="070ba-128">toolearn więcej, zobacz [cennik usług Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).</span><span class="sxs-lookup"><span data-stu-id="070ba-128">toolearn more, see [Azure Analysis Services pricing](https://azure.microsoft.com/pricing/details/analysis-services/).</span></span>
4. <span data-ttu-id="070ba-129">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="070ba-129">Click **Create**.</span></span>

<span data-ttu-id="070ba-130">Utwórz potrzebuje zazwyczaj w obszarze chwilę. często tylko kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="070ba-130">Create usually takes under a minute; often just a few seconds.</span></span> <span data-ttu-id="070ba-131">W przypadku wybrania **dodać tooPortal**, przejdź toosee portalu tooyour nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="070ba-131">If you selected **Add tooPortal**, navigate tooyour portal toosee your new server.</span></span> <span data-ttu-id="070ba-132">Lub zbyt Przejdź**więcej usług** > **usług Analysis Services** toosee, jeśli serwer jest gotowy.</span><span class="sxs-lookup"><span data-stu-id="070ba-132">Or, navigate too**More services** > **Analysis Services** toosee if your server is ready.</span></span>

 ![Pulpit nawigacyjny](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a><span data-ttu-id="070ba-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="070ba-134">Next steps</span></span>
<span data-ttu-id="070ba-135">Po utworzeniu serwera, możesz [wdrożenia modelu](analysis-services-deploy.md) tooit za pomocą narzędzi SSDT lub z narzędzia SSMS.</span><span class="sxs-lookup"><span data-stu-id="070ba-135">Once you've created your server, you can [deploy a model](analysis-services-deploy.md) tooit by using SSDT or with SSMS.</span></span>

<span data-ttu-id="070ba-136">Jeśli model wdrażania serwera tooyour łączy tooon lokalnych źródeł danych, należy tooinstall [bramy danych lokalnych](analysis-services-gateway.md) na komputerze w sieci.</span><span class="sxs-lookup"><span data-stu-id="070ba-136">If a model you deploy tooyour server connects tooon-premises data sources, you need tooinstall an [On-premises data gateway](analysis-services-gateway.md) on a computer in your network.</span></span>

