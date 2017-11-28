---
title: aaaRetrain modelu uczenia maszynowego | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak aktualizacja i tooretrain modelu hello sieci Web usługi toouse hello nowo uczonego modelu w usłudze Azure Machine Learning."
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
ms.openlocfilehash: 342bb9954105339b4b634ff20968a64f4f9f750e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="f1683-103">Ponownie ucz modelu uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="f1683-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="f1683-104">W ramach procesu hello operationalization modeli uczenia maszyny w usłudze Azure Machine Learning modelu są uczone i zapisać.</span><span class="sxs-lookup"><span data-stu-id="f1683-104">As part of hello process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="f1683-105">Następnie należy go toocreate predicative usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f1683-105">You then use it toocreate a predicative Web service.</span></span> <span data-ttu-id="f1683-106">Hello usługi sieci Web mogą być następnie używane w witrynach sieci web, pulpity nawigacyjne i aplikacji mobilnych.</span><span class="sxs-lookup"><span data-stu-id="f1683-106">hello Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="f1683-107">Modele utworzone za pomocą uczenia maszynowego zwykle nie są statyczne.</span><span class="sxs-lookup"><span data-stu-id="f1683-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="f1683-108">Wraz ze wzrostem dostępności nowych danych lub po hello konsumenta hello interfejsu API modelu hello własnych danych musi toobe retrained.</span><span class="sxs-lookup"><span data-stu-id="f1683-108">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span> 

<span data-ttu-id="f1683-109">Ponownego trenowania może występować często.</span><span class="sxs-lookup"><span data-stu-id="f1683-109">Retraining may occur frequently.</span></span> <span data-ttu-id="f1683-110">Przy użyciu funkcji API ponownego trenowania programowe hello można programowo retrain hello modelu przy użyciu hello ponownego trenowania interfejsów API i aktualizacji hello usługi sieci Web z hello nowo trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="f1683-110">With hello Programmatic Retraining API feature, you can programmatically retrain hello model using hello Retraining APIs and update hello Web service with hello newly trained model.</span></span> 

<span data-ttu-id="f1683-111">Niniejszy dokument opisuje hello ponownego trenowania procesu i pokazuje, jak toouse hello ponownego trenowania interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="f1683-111">This document describes hello retraining process, and shows you how toouse hello Retraining APIs.</span></span>

## <a name="why-retrain-defining-hello-problem"></a><span data-ttu-id="f1683-112">Dlaczego ponownie ucz: Definiowanie hello problem</span><span class="sxs-lookup"><span data-stu-id="f1683-112">Why retrain: defining hello problem</span></span>
<span data-ttu-id="f1683-113">W ramach uczenia maszynowego hello szkolenia procesu model jest uczony przy użyciu zestawu danych.</span><span class="sxs-lookup"><span data-stu-id="f1683-113">As part of hello machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="f1683-114">Modele utworzone za pomocą uczenia maszynowego zwykle nie są statyczne.</span><span class="sxs-lookup"><span data-stu-id="f1683-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="f1683-115">Wraz ze wzrostem dostępności nowych danych lub po hello konsumenta hello interfejsu API modelu hello własnych danych musi toobe retrained.</span><span class="sxs-lookup"><span data-stu-id="f1683-115">As new data becomes available or when hello consumer of hello API has their own data hello model needs toobe retrained.</span></span>

<span data-ttu-id="f1683-116">W tych scenariuszach programowe interfejsu API zapewnia tooallow wygodny sposób możesz lub powitania klienta toocreate Twojego interfejsów API klienta, który może na podstawie jednorazowe lub regularne retrain hello modelu, używając własnych danych.</span><span class="sxs-lookup"><span data-stu-id="f1683-116">In these scenarios, a programmatic API provides a convenient way tooallow you or hello consumer of your APIs toocreate a client that can, on a one-time or regular basis, retrain hello model using their own data.</span></span> <span data-ttu-id="f1683-117">Następnie mogą ocenić wyniki hello ponownego trenowania i zaktualizować hello sieci Web usługi interfejsu API toouse hello nowo uczonego modelu.</span><span class="sxs-lookup"><span data-stu-id="f1683-117">They can then evaluate hello results of retraining, and update hello Web service API toouse hello newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="f1683-118">Jeśli masz istniejące eksperyment uczenia i usługi sieci Web nowego można toocheck się ponownego próbkowania predykcyjnej istniejącej sieci Web usługi zamiast następujące wskazówki hello wspomnianego hello następujących sekcji.</span><span class="sxs-lookup"><span data-stu-id="f1683-118">If you have an existing Training Experiment and New Web service, you may want toocheck out Retrain an existing Predictive Web service instead of following hello walkthrough mentioned in hello following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="f1683-119">Kompletny przepływ pracy</span><span class="sxs-lookup"><span data-stu-id="f1683-119">End-to-end workflow</span></span>
<span data-ttu-id="f1683-120">Witaj proces obejmuje następujące składniki hello: A eksperyment uczenia i eksperyment predykcyjny publikowane jako usługę sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f1683-120">hello process involves hello following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="f1683-121">tooenable ponownego trenowania uczonego modelu hello eksperyment uczenia musi zostać opublikowany jako usługę sieci Web, przy czym dane wyjściowe hello trenowanego modelu.</span><span class="sxs-lookup"><span data-stu-id="f1683-121">tooenable retraining of a trained model, hello Training Experiment must be published as a Web service with hello output of a trained model.</span></span> <span data-ttu-id="f1683-122">Dzięki temu model toohello dostępu do interfejsu API do ponownego trenowania.</span><span class="sxs-lookup"><span data-stu-id="f1683-122">This enables API access toohello model for retraining.</span></span> 

<span data-ttu-id="f1683-123">Witaj następujące kroki, zastosuj tooboth nowy i klasycznego usługami sieci Web:</span><span class="sxs-lookup"><span data-stu-id="f1683-123">hello following steps apply tooboth New and Classic Web services:</span></span>

<span data-ttu-id="f1683-124">Tworzenie początkowej usługi sieci Web predykcyjnej hello:</span><span class="sxs-lookup"><span data-stu-id="f1683-124">Create hello initial Predictive Web service:</span></span>

* <span data-ttu-id="f1683-125">Tworzenie eksperymentu szkolenia</span><span class="sxs-lookup"><span data-stu-id="f1683-125">Create a training experiment</span></span>
* <span data-ttu-id="f1683-126">Tworzenie eksperymentu predykcyjnej sieci web</span><span class="sxs-lookup"><span data-stu-id="f1683-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="f1683-127">Wdrażanie usługi sieci web predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="f1683-127">Deploy a predictive web service</span></span>

<span data-ttu-id="f1683-128">Ponownie ucz hello usługi sieci Web:</span><span class="sxs-lookup"><span data-stu-id="f1683-128">Retrain hello Web service:</span></span>

* <span data-ttu-id="f1683-129">Zaktualizuj tooallow eksperymentu uczenia do ponownego trenowania</span><span class="sxs-lookup"><span data-stu-id="f1683-129">Update training experiment tooallow for retraining</span></span>
* <span data-ttu-id="f1683-130">Wdrażanie hello ponownego trenowania usługi sieci web</span><span class="sxs-lookup"><span data-stu-id="f1683-130">Deploy hello retraining web service</span></span>
* <span data-ttu-id="f1683-131">Użyj hello usługi wykonywania wsadowego kodu tooretrain hello modelu</span><span class="sxs-lookup"><span data-stu-id="f1683-131">Use hello Batch Execution Service code tooretrain hello model</span></span>

<span data-ttu-id="f1683-132">Aby uzyskać wskazówki hello w poprzednich krokach, zobacz [Retrain Machine Learning programowo modele](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="f1683-132">For a walkthrough of hello preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="f1683-133">toodeploy nową usługę sieci web, należy posiadać odpowiednie uprawnienia w hello toowhich subskrypcji możesz wdrażanie usługi sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="f1683-133">toodeploy a New web service you must have sufficient permissions in hello subscription toowhich you deploying hello web service.</span></span> <span data-ttu-id="f1683-134">Aby uzyskać więcej informacji, zobacz [zarządzania usługi sieci Web przy użyciu portalu usługi sieci Web systemu Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="f1683-134">For more information see, [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="f1683-135">Jeśli wdrożono klasycznym usługi sieci Web:</span><span class="sxs-lookup"><span data-stu-id="f1683-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="f1683-136">Utwórz nowy punkt końcowy na powitania usługi sieci Web predykcyjnej</span><span class="sxs-lookup"><span data-stu-id="f1683-136">Create a new Endpoint on hello Predictive Web service</span></span>
* <span data-ttu-id="f1683-137">Pobierz adres URL poprawki hello i kod</span><span class="sxs-lookup"><span data-stu-id="f1683-137">Get hello PATCH URL and code</span></span>
* <span data-ttu-id="f1683-138">Użyj hello poprawka adresu URL toopoint hello nowy punkt końcowy na powitania retrained modelu</span><span class="sxs-lookup"><span data-stu-id="f1683-138">Use hello PATCH URL toopoint hello new Endpoint at hello retrained model</span></span> 

<span data-ttu-id="f1683-139">Aby uzyskać wskazówki hello w poprzednich krokach, zobacz [Retrain usługi sieci Web klasycznego](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f1683-139">For a walkthrough of hello preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="f1683-140">Jeśli wystąpiły problemy podczas ponownego trenowania usługi sieci Web klasycznego, zobacz [Rozwiązywanie problemów z hello ponownego trenowania usługi sieci Web Azure Machine Learning klasycznego](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="f1683-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting hello retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="f1683-141">Jeśli wdrożono usługę sieci Web nowe:</span><span class="sxs-lookup"><span data-stu-id="f1683-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="f1683-142">Zaloguj się tooyour konta usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f1683-142">Sign in tooyour Azure Resource Manager account</span></span>
* <span data-ttu-id="f1683-143">Pobierz definicję usługi sieci Web hello</span><span class="sxs-lookup"><span data-stu-id="f1683-143">Get hello Web service definition</span></span>
* <span data-ttu-id="f1683-144">Eksportuj hello definicji usługi sieci Web w formacie JSON</span><span class="sxs-lookup"><span data-stu-id="f1683-144">Export hello Web Service Definition as JSON</span></span>
* <span data-ttu-id="f1683-145">Zaktualizuj toohello odwołanie hello `ilearner` obiektu blob w hello JSON</span><span class="sxs-lookup"><span data-stu-id="f1683-145">Update hello reference toohello `ilearner` blob in hello JSON</span></span>
* <span data-ttu-id="f1683-146">Importowanie hello JSON do definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="f1683-146">Import hello JSON into a Web Service Definition</span></span>
* <span data-ttu-id="f1683-147">Usługi sieci Web hello aktualizacji z nowej definicji usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="f1683-147">Update hello Web service with new Web Service Definition</span></span>

<span data-ttu-id="f1683-148">Aby uzyskać wskazówki hello w poprzednich krokach, zobacz [Retrain usługi nowej sieci Web przy użyciu poleceń cmdlet programu PowerShell do zarządzania Machine Learning hello](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f1683-148">For a walkthrough of hello preceding steps, see [Retrain a New Web service using hello Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="f1683-149">Witaj proces konfigurowania ponownego trenowania dla usługi sieci Web klasycznego obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f1683-149">hello process for setting up retraining for a Classic Web service involves hello following steps:</span></span>

![Omówienie procesu ponownego trenowania][1]

<span data-ttu-id="f1683-151">Konfigurowanie ponownego trenowania dla usługi sieci Web nowy proces Hello obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f1683-151">hello process for setting up retraining for a New Web service involves hello following steps:</span></span>

![Omówienie procesu ponownego trenowania][7]

## <a name="other-resources"></a><span data-ttu-id="f1683-153">Inne zasoby</span><span class="sxs-lookup"><span data-stu-id="f1683-153">Other Resources</span></span>
* [<span data-ttu-id="f1683-154">Modele ponownego trenowania i aktualizowania usługi Azure Machine Learning z fabryką danych Azure</span><span class="sxs-lookup"><span data-stu-id="f1683-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="f1683-155">Tworzenie wielu modeli uczenia maszynowego i sieci web punktów końcowych usługi z doświadczenia przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1683-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="f1683-156">Witaj [AML ponownego trenowania modeli przy użyciu interfejsów API](https://www.youtube.com/watch?v=wwjglA8xllg) wideo pokazuje, jak modeli uczenia maszynowego tooretrain utworzone w usłudze Azure Machine Learning przy użyciu hello ponownego trenowania interfejsów API i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1683-156">hello [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how tooretrain Machine Learning models created in Azure Machine Learning using hello Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: ./media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png

