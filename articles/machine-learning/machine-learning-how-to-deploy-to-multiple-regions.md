---
title: "Jak wdrożyć usługę sieci Web w wielu regionach | Dokumentacja firmy Microsoft"
description: "Kroki wdrażania (Kopiuj) nową usługę sieci Web do innych regionów."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: cgronlun
ms.assetid: 36c60411-f2db-4ee2-9b66-b1f1d77a8f44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 3895537bbca72e687838ff5013c291dfee3be707
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-web-service-to-multiple-regions"></a><span data-ttu-id="68e9b-103">Wdrażanie usługi sieci Web do wielu regionów</span><span class="sxs-lookup"><span data-stu-id="68e9b-103">How to deploy a Web Service to multiple regions</span></span>
<span data-ttu-id="68e9b-104">Usługi sieci Web platformy Azure umożliwiają łatwe wdrażanie usługi sieci web do wielu regionach, bez konieczności wielu subskrypcji lub obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="68e9b-104">The New Azure Web Services allow you to easily deploy a web service to multiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="68e9b-105">Cennik to region określonych, dlatego należy zdefiniować plan rozliczeniowy dla każdego regionu, w którym będą wdrażać usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="68e9b-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy the web service.</span></span>

## <a name="to-create-a-plan-in-another-region"></a><span data-ttu-id="68e9b-106">Aby utworzyć plan w innym regionie</span><span class="sxs-lookup"><span data-stu-id="68e9b-106">To create a plan in another region</span></span>
1. <span data-ttu-id="68e9b-107">Zaloguj się do [platformy Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="68e9b-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="68e9b-108">Kliknij przycisk **plany** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="68e9b-108">Click the **Plans** menu option.</span></span>
3. <span data-ttu-id="68e9b-109">W planie za pośrednictwem widoku strony, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-109">On the Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="68e9b-110">Z **subskrypcji** listy rozwijanej wybierz subskrypcję, w której będą znajdować się nowy plan.</span><span class="sxs-lookup"><span data-stu-id="68e9b-110">From the **Subscription** dropdown, select the subscription in which the new plan will reside.</span></span>
5. <span data-ttu-id="68e9b-111">Z **Region** listy rozwijanej wybierz region nowego planu.</span><span class="sxs-lookup"><span data-stu-id="68e9b-111">From the **Region** dropdown, select a region for the new plan.</span></span> <span data-ttu-id="68e9b-112">Zostaną wyświetlone opcje planowania dla wybranego regionu **opcje planowania** części strony.</span><span class="sxs-lookup"><span data-stu-id="68e9b-112">The Plan Options for the selected region will display in the **Plan Options** section of the page.</span></span>
6. <span data-ttu-id="68e9b-113">Z **grupy zasobów** listy rozwijanej wybierz zasób grupy planu.</span><span class="sxs-lookup"><span data-stu-id="68e9b-113">From the **Resource Group** dropdown, select a resource group for the plan.</span></span> <span data-ttu-id="68e9b-114">Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68e9b-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="68e9b-115">W **Nazwa planu** wpisz nazwę planu.</span><span class="sxs-lookup"><span data-stu-id="68e9b-115">In **Plan Name** type the name of the plan.</span></span>
8. <span data-ttu-id="68e9b-116">W obszarze **opcje planu**, kliknij przycisk rozliczeń poziom nowego planu.</span><span class="sxs-lookup"><span data-stu-id="68e9b-116">Under **Plan Options**, click the billing level for the new plan.</span></span>
9. <span data-ttu-id="68e9b-117">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-117">Click **Create**.</span></span>

## <a name="deploying-the-web-service-to-another-region"></a><span data-ttu-id="68e9b-118">Wdrażanie usługi sieci web do innego regionu</span><span class="sxs-lookup"><span data-stu-id="68e9b-118">Deploying the web service to another region</span></span>
1. <span data-ttu-id="68e9b-119">Kliknij przycisk **usług sieci Web** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="68e9b-119">Click the **Web Services** menu option.</span></span>
2. <span data-ttu-id="68e9b-120">Wybierz usługę sieci Web jest wdrażany z nowego regionu.</span><span class="sxs-lookup"><span data-stu-id="68e9b-120">Select the Web Service you are deploying to a new region.</span></span>
3. <span data-ttu-id="68e9b-121">Kliknij przycisk **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-121">Click **Copy**.</span></span>
4. <span data-ttu-id="68e9b-122">W **nazwę usługi sieci Web**, wpisz nową nazwę dla usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="68e9b-122">In **Web Service Name**, type a new name for the web service.</span></span>
5. <span data-ttu-id="68e9b-123">W **sieci Web opisu usługi**, wpisz opis usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="68e9b-123">In **Web service description**, type a description for the web service.</span></span>
6. <span data-ttu-id="68e9b-124">Z **subskrypcji** listy rozwijanej wybierz subskrypcję, w której będą znajdować się nową usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="68e9b-124">From the **Subscription** dropdown, select the subscription in which the new web service will reside.</span></span>
7. <span data-ttu-id="68e9b-125">Z **grupy zasobów** listy rozwijanej wybierz zasób grupy dla usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="68e9b-125">From the **Resource Group** dropdown, select a resource group for the web service.</span></span> <span data-ttu-id="68e9b-126">Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="68e9b-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="68e9b-127">Z **Region** listy rozwijanej wybierz region, w której chcesz wdrożyć usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="68e9b-127">From the **Region** dropdown, select the region in which to deploy the web service.</span></span>
9. <span data-ttu-id="68e9b-128">Z **konta magazynu** konta listy rozwijanej wybierz magazynu do przechowywania usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="68e9b-128">From the **Storage account** dropdown, select a storage account in which to store the web service.</span></span>
10. <span data-ttu-id="68e9b-129">Z **planu cen** listy rozwijanej wybierz plan w regionie wybranej w kroku 8.</span><span class="sxs-lookup"><span data-stu-id="68e9b-129">From the **Price Plan** dropdown, select a plan in the region you selected in step 8.</span></span>
11. <span data-ttu-id="68e9b-130">Kliknij przycisk **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="68e9b-130">Click **Copy**.</span></span>

