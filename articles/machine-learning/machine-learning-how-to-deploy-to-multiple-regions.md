---
title: "toodeploy aaaHow usługi sieci Web regionów toomultiple | Dokumentacja firmy Microsoft"
description: "Kroki toodeploy (Kopiuj) regionów tooother nową usługę sieci Web."
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
ms.openlocfilehash: 21fcdb96f118c60ed98b60b1b2df833766c7c8bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-web-service-toomultiple-regions"></a><span data-ttu-id="44d53-103">Jak toodeploy usługi sieci Web toomultiple regionów</span><span class="sxs-lookup"><span data-stu-id="44d53-103">How toodeploy a Web Service toomultiple regions</span></span>
<span data-ttu-id="44d53-104">Hello nowych usług sieci Web Azure pozwala tooeasily wdrażanie regiony toomultiple usługi sieci web bez konieczności wielu subskrypcji lub obszarów roboczych.</span><span class="sxs-lookup"><span data-stu-id="44d53-104">hello New Azure Web Services allow you tooeasily deploy a web service toomultiple regions without needing multiple subscriptions or workspaces.</span></span> 

<span data-ttu-id="44d53-105">Cennik jest określone, dlatego należy zdefiniować plan rozliczeniowy dla każdego regionu, w którym zostanie wdrożona usługa sieci web hello regionu.</span><span class="sxs-lookup"><span data-stu-id="44d53-105">Pricing is region specific, therefore you must define a billing plan for each region in which you will deploy hello web service.</span></span>

## <a name="toocreate-a-plan-in-another-region"></a><span data-ttu-id="44d53-106">toocreate planu w innym regionie</span><span class="sxs-lookup"><span data-stu-id="44d53-106">toocreate a plan in another region</span></span>
1. <span data-ttu-id="44d53-107">Zaloguj się do [platformy Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="44d53-107">Sign into [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/).</span></span>
2. <span data-ttu-id="44d53-108">Kliknij przycisk hello **plany** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="44d53-108">Click hello **Plans** menu option.</span></span>
3. <span data-ttu-id="44d53-109">W planie hello za pośrednictwem widoku strony, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="44d53-109">On hello Plans over view page, click **New**.</span></span>
4. <span data-ttu-id="44d53-110">Z hello **subskrypcji** listy rozwijanej wybierz hello subskrypcji w hello, które będą znajdować się nowy plan.</span><span class="sxs-lookup"><span data-stu-id="44d53-110">From hello **Subscription** dropdown, select hello subscription in which hello new plan will reside.</span></span>
5. <span data-ttu-id="44d53-111">Z hello **Region** listy rozwijanej wybierz region hello nowego planu.</span><span class="sxs-lookup"><span data-stu-id="44d53-111">From hello **Region** dropdown, select a region for hello new plan.</span></span> <span data-ttu-id="44d53-112">Witaj opcje planowania dla wybranego regionu hello będą wyświetlane na powitania **opcje planowania** sekcji hello strony.</span><span class="sxs-lookup"><span data-stu-id="44d53-112">hello Plan Options for hello selected region will display in hello **Plan Options** section of hello page.</span></span>
6. <span data-ttu-id="44d53-113">Z hello **grupy zasobów** listy rozwijanej wybierz zasób grupy hello planu.</span><span class="sxs-lookup"><span data-stu-id="44d53-113">From hello **Resource Group** dropdown, select a resource group for hello plan.</span></span> <span data-ttu-id="44d53-114">Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44d53-114">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
7. <span data-ttu-id="44d53-115">W **Nazwa planu** Nazwa typu hello hello planu.</span><span class="sxs-lookup"><span data-stu-id="44d53-115">In **Plan Name** type hello name of hello plan.</span></span>
8. <span data-ttu-id="44d53-116">W obszarze **opcje planu**, kliknij przycisk Poziom rozliczeń hello hello nowego planu.</span><span class="sxs-lookup"><span data-stu-id="44d53-116">Under **Plan Options**, click hello billing level for hello new plan.</span></span>
9. <span data-ttu-id="44d53-117">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="44d53-117">Click **Create**.</span></span>

## <a name="deploying-hello-web-service-tooanother-region"></a><span data-ttu-id="44d53-118">Wdrażanie region tooanother usługi sieci web hello</span><span class="sxs-lookup"><span data-stu-id="44d53-118">Deploying hello web service tooanother region</span></span>
1. <span data-ttu-id="44d53-119">Kliknij przycisk hello **usług sieci Web** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="44d53-119">Click hello **Web Services** menu option.</span></span>
2. <span data-ttu-id="44d53-120">Wybierz hello wdrażasz nowego regionu tooa usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="44d53-120">Select hello Web Service you are deploying tooa new region.</span></span>
3. <span data-ttu-id="44d53-121">Kliknij przycisk **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="44d53-121">Click **Copy**.</span></span>
4. <span data-ttu-id="44d53-122">W **nazwę usługi sieci Web**, wpisz nową nazwę dla usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="44d53-122">In **Web Service Name**, type a new name for hello web service.</span></span>
5. <span data-ttu-id="44d53-123">W **sieci Web opisu usługi**, wpisz opis hello usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="44d53-123">In **Web service description**, type a description for hello web service.</span></span>
6. <span data-ttu-id="44d53-124">Z hello **subskrypcji** listy rozwijanej wybierz hello subskrypcji, w których hello nową usługę sieci web będzie znajdować się.</span><span class="sxs-lookup"><span data-stu-id="44d53-124">From hello **Subscription** dropdown, select hello subscription in which hello new web service will reside.</span></span>
7. <span data-ttu-id="44d53-125">Z hello **grupy zasobów** listy rozwijanej wybierz zasób grupy dla usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="44d53-125">From hello **Resource Group** dropdown, select a resource group for hello web service.</span></span> <span data-ttu-id="44d53-126">Aby uzyskać więcej informacji na temat grup zasobów, zobacz [Omówienie usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44d53-126">From more information on resource groups, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
8. <span data-ttu-id="44d53-127">Z hello **Region** listy rozwijanej wybierz hello region usługi sieci web, która hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="44d53-127">From hello **Region** dropdown, select hello region in which toodeploy hello web service.</span></span>
9. <span data-ttu-id="44d53-128">Z hello **konta magazynu** listy rozwijanej, wybierz konto magazynu, w którym hello toostore usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="44d53-128">From hello **Storage account** dropdown, select a storage account in which toostore hello web service.</span></span>
10. <span data-ttu-id="44d53-129">Z hello **planu cen** listy rozwijanej wybierz plan w regionie hello wybranej w kroku 8.</span><span class="sxs-lookup"><span data-stu-id="44d53-129">From hello **Price Plan** dropdown, select a plan in hello region you selected in step 8.</span></span>
11. <span data-ttu-id="44d53-130">Kliknij przycisk **kopiowania**.</span><span class="sxs-lookup"><span data-stu-id="44d53-130">Click **Copy**.</span></span>

