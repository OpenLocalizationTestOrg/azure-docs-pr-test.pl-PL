---
title: Ponownie ucz modelu uczenia maszynowego | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak ponownie ucz modelu i usługi sieci Web, aby użyć nowo uczonego modelu w usłudze Azure Machine Learning aktualizacji."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: f86c2bc41dd7ff0bc31454a56b84d136dc7d026c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="93578-103">Ponownie ucz modelu uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="93578-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="93578-104">W ramach procesu operationalization modeli uczenia maszyny w usłudze Azure Machine Learning modelu są uczone i zapisać.</span><span class="sxs-lookup"><span data-stu-id="93578-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="93578-105">Następnie należy go utworzyć predicative usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="93578-105">You then use it to create a predicative Web service.</span></span> <span data-ttu-id="93578-106">Usługi sieci Web mogą być następnie używane w witrynach sieci web, pulpity nawigacyjne i aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="93578-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="93578-107">Modele utworzone za pomocą uczenia maszynowego zwykle nie są statyczne.</span><span class="sxs-lookup"><span data-stu-id="93578-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="93578-108">Wraz ze wzrostem dostępności nowych danych lub gdy konsumenta interfejsu API ma własne dane modelu musi być retrained.</span><span class="sxs-lookup"><span data-stu-id="93578-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> 

<span data-ttu-id="93578-109">Ponownego trenowania może występować często.</span><span class="sxs-lookup"><span data-stu-id="93578-109">Retraining may occur frequently.</span></span> <span data-ttu-id="93578-110">Z funkcją programowe ponownego trenowania interfejsu API można programowo retrain modelu przy użyciu interfejsów API ponownego trenowania i aktualizować usługi sieci Web z nowo trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="93578-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span></span> 

<span data-ttu-id="93578-111">Tym dokumencie opisano proces ponownego trenowania i przedstawiono sposób użycia interfejsów API ponownego trenowania.</span><span class="sxs-lookup"><span data-stu-id="93578-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span></span>

## <a name="why-retrain-defining-the-problem"></a><span data-ttu-id="93578-112">Dlaczego ponownie ucz: Definiowanie problemu</span><span class="sxs-lookup"><span data-stu-id="93578-112">Why retrain: defining the problem</span></span>
<span data-ttu-id="93578-113">W ramach procesu szkolenia uczenia maszynowego model jest uczony przy użyciu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="93578-113">As part of the machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="93578-114">Modele utworzone za pomocą uczenia maszynowego zwykle nie są statyczne.</span><span class="sxs-lookup"><span data-stu-id="93578-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="93578-115">Wraz ze wzrostem dostępności nowych danych lub gdy konsumenta interfejsu API ma własne dane modelu musi być retrained.</span><span class="sxs-lookup"><span data-stu-id="93578-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span>

<span data-ttu-id="93578-116">W tych scenariuszach Programistyczny interfejs API udostępnia wygodny sposób pozwalającej użytkownikowi lub konsumenta swoje interfejsy API do tworzenia klienta, który może na podstawie jednorazowe lub regularne retrain modelu przy użyciu własnych danych.</span><span class="sxs-lookup"><span data-stu-id="93578-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span></span> <span data-ttu-id="93578-117">Następnie mogą oceniać wyniki ponownego trenowania i aktualizacji interfejsu API usługi sieci Web, aby użyć nowo trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="93578-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="93578-118">Jeśli masz istniejące eksperyment uczenia i usługi sieci Web nowego można wyewidencjonować ponownego próbkowania istniejącej usługi sieci Web predykcyjnej zamiast następujące wskazówki wymienionych w poniższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="93578-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="93578-119">End-to-end przepływu pracy</span><span class="sxs-lookup"><span data-stu-id="93578-119">End-to-end workflow</span></span>
<span data-ttu-id="93578-120">Ten proces obejmuje następujące składniki: A eksperyment uczenia i eksperyment predykcyjny publikowane jako usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="93578-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="93578-121">Aby włączyć ponownego trenowania trenowanego modelu, eksperyment uczenia musi zostać opublikowany jako usługę sieci Web, przy czym dane wyjściowe trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="93578-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span></span> <span data-ttu-id="93578-122">Dzięki temu dostęp API do modelu do ponownego trenowania.</span><span class="sxs-lookup"><span data-stu-id="93578-122">This enables API access to the model for retraining.</span></span> 

<span data-ttu-id="93578-123">Poniższe kroki dotyczą zarówno nowe, jak i klasycznych sieci Web usług:</span><span class="sxs-lookup"><span data-stu-id="93578-123">The following steps apply to both New and Classic Web services:</span></span>

<span data-ttu-id="93578-124">Tworzenie początkowej usługi sieci Web predykcyjnej:</span><span class="sxs-lookup"><span data-stu-id="93578-124">Create the initial Predictive Web service:</span></span>

* <span data-ttu-id="93578-125">Tworzenie eksperymentu szkolenia</span><span class="sxs-lookup"><span data-stu-id="93578-125">Create a training experiment</span></span>
* <span data-ttu-id="93578-126">Tworzenie eksperymentu predykcyjnej sieci web</span><span class="sxs-lookup"><span data-stu-id="93578-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="93578-127">Wdrażanie usługi sieci web predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="93578-127">Deploy a predictive web service</span></span>

<span data-ttu-id="93578-128">Ponownie ucz usługi sieci Web:</span><span class="sxs-lookup"><span data-stu-id="93578-128">Retrain the Web service:</span></span>

* <span data-ttu-id="93578-129">Eksperyment uczenia aktualizacji, aby umożliwić ponownego trenowania</span><span class="sxs-lookup"><span data-stu-id="93578-129">Update training experiment to allow for retraining</span></span>
* <span data-ttu-id="93578-130">Wdrażanie ponownego trenowania usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="93578-130">Deploy the retraining web service</span></span>
* <span data-ttu-id="93578-131">Ponownie ucz modelu za pomocą kodu usługi wykonywania wsadowego</span><span class="sxs-lookup"><span data-stu-id="93578-131">Use the Batch Execution Service code to retrain the model</span></span>

<span data-ttu-id="93578-132">Aby uzyskać wskazówki poprzednich kroków, zobacz [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="93578-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="93578-133">Aby wdrożyć nową usługę sieci web musi masz wystarczające uprawnienia do subskrypcji, do którego należy wdrożyć usługę sieci web.</span><span class="sxs-lookup"><span data-stu-id="93578-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="93578-134">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="93578-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="93578-135">Jeśli wdrożono klasycznym usługi sieci Web:</span><span class="sxs-lookup"><span data-stu-id="93578-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="93578-136">Utwórz nowy punkt końcowy usługi sieci Web predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="93578-136">Create a new Endpoint on the Predictive Web service</span></span>
* <span data-ttu-id="93578-137">Pobierz adres URL poprawki i kod</span><span class="sxs-lookup"><span data-stu-id="93578-137">Get the PATCH URL and code</span></span>
* <span data-ttu-id="93578-138">Użyj adresu URL PATCH, aby wskazywały nowy punkt końcowy na retrained modelu</span><span class="sxs-lookup"><span data-stu-id="93578-138">Use the PATCH URL to point the new Endpoint at the retrained model</span></span> 

<span data-ttu-id="93578-139">Aby uzyskać wskazówki poprzednich kroków, zobacz [Retrain usługi sieci Web klasycznego](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="93578-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="93578-140">Jeśli wystąpiły problemy podczas ponownego trenowania usługi sieci Web klasycznego, zobacz [Rozwiązywanie problemów z ponownego trenowania usługi sieci Web Azure Machine Learning klasycznego](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="93578-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="93578-141">Jeśli wdrożono usługę sieci Web nowe:</span><span class="sxs-lookup"><span data-stu-id="93578-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="93578-142">Zaloguj się do konta usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="93578-142">Sign in to your Azure Resource Manager account</span></span>
* <span data-ttu-id="93578-143">Pobierz definicję usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="93578-143">Get the Web service definition</span></span>
* <span data-ttu-id="93578-144">Eksportowanie definicji usługi sieci Web w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="93578-144">Export the Web Service Definition as JSON</span></span>
* <span data-ttu-id="93578-145">Aktualizacja odwołania do `ilearner` obiektu blob w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="93578-145">Update the reference to the `ilearner` blob in the JSON</span></span>
* <span data-ttu-id="93578-146">Zaimportuj dane JSON do definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="93578-146">Import the JSON into a Web Service Definition</span></span>
* <span data-ttu-id="93578-147">Aktualizacja usługi sieci Web z nowego definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="93578-147">Update the Web service with new Web Service Definition</span></span>

<span data-ttu-id="93578-148">Aby uzyskać wskazówki poprzednich kroków, zobacz [Retrain usługi nowej sieci Web przy użyciu poleceń cmdlet programu PowerShell do zarządzania Machine Learning](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="93578-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="93578-149">Proces konfigurowania ponownego trenowania dla usługi sieci Web klasycznego obejmuje następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="93578-149">The process for setting up retraining for a Classic Web service involves the following steps:</span></span>

![Omówienie procesu ponownego trenowania][1]

<span data-ttu-id="93578-151">Proces konfigurowania ponownego trenowania dla usługi sieci Web nowego obejmuje następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="93578-151">The process for setting up retraining for a New Web service involves the following steps:</span></span>

![Omówienie procesu ponownego trenowania][7]

## <a name="other-resources"></a><span data-ttu-id="93578-153">Inne zasoby</span><span class="sxs-lookup"><span data-stu-id="93578-153">Other Resources</span></span>
* [<span data-ttu-id="93578-154">Modele ponownego trenowania i aktualizowania usługi Azure Machine Learning z fabryką danych Azure</span><span class="sxs-lookup"><span data-stu-id="93578-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="93578-155">Tworzenie wielu modeli uczenia maszynowego i sieci web punktów końcowych usługi z doświadczenia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="93578-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="93578-156">[AML ponownego trenowania modeli przy użyciu interfejsów API](https://www.youtube.com/watch?v=wwjglA8xllg) wideo pokazuje, jak ponownie ucz modele uczenia maszynowego utworzone w usłudze Azure Machine Learning przy użyciu ponownego trenowania interfejsów API i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93578-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

