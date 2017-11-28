---
title: Dokumentacji pomocy Multi-geograficznie | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak utworzyć obszaru roboczego i opublikować usługi sieci web w regionie Azure różne od Południowe Stany Zjednoczone centralnej (SCUS) region platformy Azure."
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 32f80863308c00c32b1496bb92d39a7ae7d0cc6f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="6f3e0-103">Dokumentacja pomocy dotyczącej wielu regionów geograficznych</span><span class="sxs-lookup"><span data-stu-id="6f3e0-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="6f3e0-104">W tym artykule opisano, jak można utworzyć obszaru roboczego i opublikować usługi sieci web w różnych regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="6f3e0-105">[Produkty Azure według regionu strony](https://azure.microsoft.com/en-us/regions/services/) zawiera listę regionów, gdzie dostępna jest usługa Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-105">The [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="6f3e0-106">Tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="6f3e0-106">Create a workspace</span></span>
1. <span data-ttu-id="6f3e0-107">Zaloguj się do klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-107">Sign in to the Azure Classic Portal.</span></span>
2. <span data-ttu-id="6f3e0-108">Kliknij przycisk **+ nowy** > **usług danych** > **UCZENIA MASZYNOWEGO** > **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="6f3e0-109">W obszarze **lokalizacji** wybrać inny region, takich jak **Azja południowo-wschodnia**.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="6f3e0-110">![Obraz pomocy Multi-geograficznie 1][1]</span><span class="sxs-lookup"><span data-stu-id="6f3e0-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="6f3e0-111">Wybierz obszar roboczy, a następnie kliknij przycisk **zalogować się do ML Studio**.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-111">Select the workspace, and then click **Sign-in to ML Studio**.</span></span>
   <span data-ttu-id="6f3e0-112">![Pomoc geograficznie wielu obraz 2][2]</span><span class="sxs-lookup"><span data-stu-id="6f3e0-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="6f3e0-113">Obszar roboczy jest teraz dostępna w innym regionie, w których można używać tak samo jak inne obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="6f3e0-114">Aby przełączyć między obszarów roboczych, poszukaj do prawego górnego rogu ekranu.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-114">To switch among your workspaces, look to the upper right of your screen.</span></span> <span data-ttu-id="6f3e0-115">Kliknij listę rozwijaną, wybierz region, a następnie wybierz obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-115">Click the dropdown, select the region, and then select the workspace.</span></span> <span data-ttu-id="6f3e0-116">Wszystko jest lokalny dla obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-116">Everything is local to the workspace region.</span></span>  <span data-ttu-id="6f3e0-117">Na przykład wszystkich usług sieci web utworzony z obszaru roboczego będzie, w tym samym regionie, w obszarze roboczym w której znajduje się.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-117">For example, all of your web services created from a workspace will be in the same region the workspace is located in.</span></span>
   <span data-ttu-id="6f3e0-118">![Pomoc geograficznie wielu obrazu 3][3]</span><span class="sxs-lookup"><span data-stu-id="6f3e0-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="6f3e0-119">Otworzyć eksperyment z galerii</span><span class="sxs-lookup"><span data-stu-id="6f3e0-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="6f3e0-120">Po otwarciu doświadczenia z galerii, możesz wybrać regionu, którego chcesz skopiować do eksperymentu.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-120">If you open an experiment from Gallery, you can also select which region you want to copy the experiment to.</span></span>

![Pomoc geograficznie wielu obrazu 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="6f3e0-122">Zarządzanie usługami sieci Web</span><span class="sxs-lookup"><span data-stu-id="6f3e0-122">Web service management</span></span>
<span data-ttu-id="6f3e0-123">Do programowego zarządzania usług sieci web, takich jak do ponownego trenowania, użyj adresu określonego regionu:</span><span class="sxs-lookup"><span data-stu-id="6f3e0-123">To programmatically manage web services, such as for retraining, use the region-specific address:</span></span>

* <span data-ttu-id="6f3e0-124">https://asiasoutheast.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="6f3e0-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="6f3e0-125">https://europewest.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="6f3e0-125">https://europewest.management.azureml.net</span></span>

### <a name="things-to-note"></a><span data-ttu-id="6f3e0-126">Rzeczy do uwzględnienia</span><span class="sxs-lookup"><span data-stu-id="6f3e0-126">Things to note</span></span>
1. <span data-ttu-id="6f3e0-127">Możesz skopiować tylko eksperymenty między obszarami roboczymi, które należą do tego samego regionu w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-127">You can only copy experiments between workspaces that belong to the same region this way.</span></span> <span data-ttu-id="6f3e0-128">Jeśli trzeba skopiować eksperymentu w obszary robocze w różnych regionach, można użyć [PowerShell](http://aka.ms/amlps) polecenie commandlet [ *AmlExperiment kopii* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) znajdują się.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-128">If you need to copy experiment across workspaces in different regions, you can use the [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) to accomplish that.</span></span> <span data-ttu-id="6f3e0-129">Inne obejście jest opublikowanie eksperymentu w galerii w trybie nieznajdujące się na liście, otwórz go w obszarze roboczym z innego regionu.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-129">Another workaround is to publish the experiment into Gallery in unlisted mode, then open it in the workspace from the other region.</span></span>
2. <span data-ttu-id="6f3e0-130">Selektor region Pokaż tylko obszarów roboczych do jednego regionu w czasie.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-130">The region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="6f3e0-131">Obszar roboczy wolne lub obszar roboczy (anonimowe) dostępu dla gości zostanie utworzona i hostowanych w centralnej Południowe stany USA</span><span class="sxs-lookup"><span data-stu-id="6f3e0-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="6f3e0-132">Usługi sieci Web wdrożone z obszaru roboczego w Azji Południowo-Wschodnia będą również obsługiwane w Azji Południowo-Wschodnia.</span><span class="sxs-lookup"><span data-stu-id="6f3e0-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="6f3e0-133">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="6f3e0-133">More information</span></span>
<span data-ttu-id="6f3e0-134">Zadaj pytanie na [forum usługi Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="6f3e0-134">Ask a question on the [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
