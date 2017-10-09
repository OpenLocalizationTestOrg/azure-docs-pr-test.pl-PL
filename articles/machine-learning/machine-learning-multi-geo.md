---
title: dokumentacji pomocy geograficznie aaaMulti | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate obszaru roboczego i opublikować usługi sieci web w regionie Azure, inny niż hello Południowa centralnej Stanów Zjednoczonych (SCUS) region platformy Azure."
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
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a><span data-ttu-id="95f4a-103">Dokumentacja pomocy dotyczącej wielu regionów geograficznych</span><span class="sxs-lookup"><span data-stu-id="95f4a-103">Multi-Geo Help documentation</span></span>
<span data-ttu-id="95f4a-104">W tym artykule opisano, jak można utworzyć obszaru roboczego i opublikować usługi sieci web w różnych regionach platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="95f4a-104">This article describes how you can create a workspace and publish a web service in different Azure regions.</span></span>  <span data-ttu-id="95f4a-105">Witaj [produkty Azure według regionu strony](https://azure.microsoft.com/en-us/regions/services/) zawiera listę regionów, gdzie dostępna jest usługa Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="95f4a-105">hello [Azure Products by Region page](https://azure.microsoft.com/en-us/regions/services/) lists regions where Azure Machine Learning is available.</span></span>

## <a name="create-a-workspace"></a><span data-ttu-id="95f4a-106">Tworzenie obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="95f4a-106">Create a workspace</span></span>
1. <span data-ttu-id="95f4a-107">Zaloguj się toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="95f4a-107">Sign in toohello Azure Classic Portal.</span></span>
2. <span data-ttu-id="95f4a-108">Kliknij przycisk **+ nowy** > **usług danych** > **UCZENIA MASZYNOWEGO** > **szybkie tworzenie**.</span><span class="sxs-lookup"><span data-stu-id="95f4a-108">Click **+NEW** > **DATA SERVICES** > **MACHINE LEARNING** > **QUICK CREATE**.</span></span>  <span data-ttu-id="95f4a-109">W obszarze **lokalizacji** wybrać inny region, takich jak **Azja południowo-wschodnia**.</span><span class="sxs-lookup"><span data-stu-id="95f4a-109">Under **LOCATION** select another region, such as **Southeast Asia**.</span></span>
   <span data-ttu-id="95f4a-110">![Obraz pomocy Multi-geograficznie 1][1]</span><span class="sxs-lookup"><span data-stu-id="95f4a-110">![Multi-Geo Help image 1][1]</span></span>
3. <span data-ttu-id="95f4a-111">Wybierz obszar roboczy hello, a następnie kliknij przycisk **logowania tooML Studio**.</span><span class="sxs-lookup"><span data-stu-id="95f4a-111">Select hello workspace, and then click **Sign-in tooML Studio**.</span></span>
   <span data-ttu-id="95f4a-112">![Pomoc geograficznie wielu obraz 2][2]</span><span class="sxs-lookup"><span data-stu-id="95f4a-112">![Multi-Geo Help image 2][2]</span></span>
4. <span data-ttu-id="95f4a-113">Obszar roboczy jest teraz dostępna w innym regionie, w których można używać tak samo jak inne obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="95f4a-113">You now have a workspace in another region that you may use just like any other workspace.</span></span> <span data-ttu-id="95f4a-114">tooswitch między obszarów roboczych, zobacz toohello górnym rogu ekranu.</span><span class="sxs-lookup"><span data-stu-id="95f4a-114">tooswitch among your workspaces, look toohello upper right of your screen.</span></span> <span data-ttu-id="95f4a-115">Kliknij przycisk hello listy rozwijanej, wybierz hello regionu i hello następnie wybierz obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="95f4a-115">Click hello dropdown, select hello region, and then select hello workspace.</span></span> <span data-ttu-id="95f4a-116">Wszystko to toohello lokalnego obszaru roboczego region.</span><span class="sxs-lookup"><span data-stu-id="95f4a-116">Everything is local toohello workspace region.</span></span>  <span data-ttu-id="95f4a-117">Na przykład będzie wszystkich usług sieci web utworzony z obszaru roboczego w hello, w tym samym regionie hello w obszarze roboczym w której znajduje się.</span><span class="sxs-lookup"><span data-stu-id="95f4a-117">For example, all of your web services created from a workspace will be in hello same region hello workspace is located in.</span></span>
   <span data-ttu-id="95f4a-118">![Pomoc geograficznie wielu obrazu 3][3]</span><span class="sxs-lookup"><span data-stu-id="95f4a-118">![Multi-Geo Help image 3][3]</span></span>

## <a name="open-an-experiment-from-gallery"></a><span data-ttu-id="95f4a-119">Otworzyć eksperyment z galerii</span><span class="sxs-lookup"><span data-stu-id="95f4a-119">Open an experiment from Gallery</span></span>
<span data-ttu-id="95f4a-120">Po otwarciu doświadczenia z galerii można również wybrać regionu, którego chcesz doświadczenia hello toocopy.</span><span class="sxs-lookup"><span data-stu-id="95f4a-120">If you open an experiment from Gallery, you can also select which region you want toocopy hello experiment to.</span></span>

![Pomoc geograficznie wielu obrazu 4][4a]

## <a name="web-service-management"></a><span data-ttu-id="95f4a-122">Zarządzanie usługami sieci Web</span><span class="sxs-lookup"><span data-stu-id="95f4a-122">Web service management</span></span>
<span data-ttu-id="95f4a-123">tooprogrammatically zarządzania usługami sieci web, takich jak do ponownego trenowania, użyj adresu określonego regionu hello:</span><span class="sxs-lookup"><span data-stu-id="95f4a-123">tooprogrammatically manage web services, such as for retraining, use hello region-specific address:</span></span>

* <span data-ttu-id="95f4a-124">https://asiasoutheast.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="95f4a-124">https://asiasoutheast.management.azureml.net</span></span>
* <span data-ttu-id="95f4a-125">https://europewest.Management.azureml.NET</span><span class="sxs-lookup"><span data-stu-id="95f4a-125">https://europewest.management.azureml.net</span></span>

### <a name="things-toonote"></a><span data-ttu-id="95f4a-126">Toonote rzeczy</span><span class="sxs-lookup"><span data-stu-id="95f4a-126">Things toonote</span></span>
1. <span data-ttu-id="95f4a-127">Możesz skopiować tylko eksperymenty między obszarami roboczymi, które należą toohello tego samego regionu w ten sposób.</span><span class="sxs-lookup"><span data-stu-id="95f4a-127">You can only copy experiments between workspaces that belong toohello same region this way.</span></span> <span data-ttu-id="95f4a-128">Jeśli potrzebujesz toocopy eksperymentu w obszary robocze w różnych regionach, można użyć hello [PowerShell](http://aka.ms/amlps) polecenie commandlet [ *AmlExperiment kopii* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish który.</span><span class="sxs-lookup"><span data-stu-id="95f4a-128">If you need toocopy experiment across workspaces in different regions, you can use hello [PowerShell](http://aka.ms/amlps) commandlet [*Copy-AmlExperiment*](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish that.</span></span> <span data-ttu-id="95f4a-129">Inne obejście jest toopublish hello eksperymentu w galerii w trybie nieznajdujące się na liście, a następnie otwórz go w obszarze roboczym hello z hello inny region.</span><span class="sxs-lookup"><span data-stu-id="95f4a-129">Another workaround is toopublish hello experiment into Gallery in unlisted mode, then open it in hello workspace from hello other region.</span></span>
2. <span data-ttu-id="95f4a-130">Selektor region Hello Pokaż tylko obszarów roboczych do jednego regionu w czasie.</span><span class="sxs-lookup"><span data-stu-id="95f4a-130">hello region selector will only show workspaces for one region at a time.</span></span>  
3. <span data-ttu-id="95f4a-131">Obszar roboczy wolne lub obszar roboczy (anonimowe) dostępu dla gości zostanie utworzona i hostowanych w centralnej Południowe stany USA</span><span class="sxs-lookup"><span data-stu-id="95f4a-131">A free workspace or Guest Access (anonymous) workspace will be created and hosted in South Central U.S.</span></span>  
4. <span data-ttu-id="95f4a-132">Usługi sieci Web wdrożone z obszaru roboczego w Azji Południowo-Wschodnia będą również obsługiwane w Azji Południowo-Wschodnia.</span><span class="sxs-lookup"><span data-stu-id="95f4a-132">Web services deployed from a workspace in Southeast Asia will also be hosted in Southeast Asia.</span></span>  

## <a name="more-information"></a><span data-ttu-id="95f4a-133">Więcej informacji</span><span class="sxs-lookup"><span data-stu-id="95f4a-133">More information</span></span>
<span data-ttu-id="95f4a-134">Zadaj pytanie na powitania [forum usługi Azure Machine Learning](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span><span class="sxs-lookup"><span data-stu-id="95f4a-134">Ask a question on hello [Azure Machine Learning forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning).</span></span>

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
