---
title: "Usługi sieci Web uczenie Azure maszyny: Wdrażanie i zużycia | Dokumentacja firmy Microsoft"
description: "Zasoby umożliwiające wdrażanie i korzystanie z usług sieci web."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 539c2abb053a0f981be0374defe45cf4d96b740b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="198d0-103">Usługi sieci Web Azure Machine Learning: wdrażanie i korzystanie</span><span class="sxs-lookup"><span data-stu-id="198d0-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="198d0-104">Można użyć usługi Azure Machine Learning toodeploy uczenia maszynowego przepływów pracy i modele jako usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="198d0-104">You can use Azure Machine Learning toodeploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="198d0-105">Te usługi sieci web może następnie być modeli uczenia maszynowego hello toocall używanych z aplikacji za pośrednictwem hello Internet toodo prognoz w czasie rzeczywistym lub w trybie wsadowym.</span><span class="sxs-lookup"><span data-stu-id="198d0-105">These web services can then be used toocall hello machine-learning models from applications over hello Internet toodo predictions in real time or in batch mode.</span></span> <span data-ttu-id="198d0-106">Ponieważ hello usług sieci web RESTful, można ich wywołać z różnych języków programowania i platform, takich jak .NET i Java i z aplikacji, takich jak program Excel.</span><span class="sxs-lookup"><span data-stu-id="198d0-106">Because hello web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="198d0-107">Witaj dalej sekcjach znajdują się linki toowalkthroughs, kodu i toohelp dokumentacji ułatwią rozpoczęcie pracy.</span><span class="sxs-lookup"><span data-stu-id="198d0-107">hello next sections provide links toowalkthroughs, code, and documentation toohelp get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="198d0-108">Wdrażanie usługi internetowej</span><span class="sxs-lookup"><span data-stu-id="198d0-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="198d0-109">Za pomocą usługi Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="198d0-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="198d0-110">Witaj usługi sieci Web Microsoft Azure Machine Learning portal i usługa Machine Learning Studio ułatwiające wdrażanie i zarządzanie usługi sieci web bez konieczności pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="198d0-110">Machine Learning Studio and hello Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="198d0-111">Witaj poniższe linki udostępniają informacje ogólne o tym, jak toodeploy nową usługę sieci web:</span><span class="sxs-lookup"><span data-stu-id="198d0-111">hello following links provide general Information about how toodeploy a new web service:</span></span>

* <span data-ttu-id="198d0-112">Omówienie toodeploy nową usługę sieci web, opartą na usłudze Azure Resource Manager, zobacz temat [wdrożenie nowej usługi sieci web](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="198d0-112">For an overview about how toodeploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="198d0-113">Aby uzyskać wskazówki dotyczące toodeploy usługi sieci web, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="198d0-113">For a walkthrough about how toodeploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="198d0-114">Aby uzyskać pełny przewodnik o tym, jak toocreate i wdrażania usługi sieci web, zobacz [wskazówki krok 1: tworzenie obszaru roboczego uczenia maszynowego](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="198d0-114">For a full walkthrough about how toocreate and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="198d0-115">Aby uzyskać szczegółowe przykłady, które wdrażanie usługi sieci web zobacz:</span><span class="sxs-lookup"><span data-stu-id="198d0-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="198d0-116">Wskazówki krok 5: Wdrażanie usługi sieci web Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="198d0-116">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="198d0-117">Jak toodeploy sieci web usługi toomultiple regionów</span><span class="sxs-lookup"><span data-stu-id="198d0-117">How toodeploy a web service toomultiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="198d0-118">Z dostawcy zasobów usługi sieci web API (interfejsów API usługi Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="198d0-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="198d0-119">dostawcy zasobów usługi Azure Machine Learning Hello usług sieci web umożliwia wdrażanie i zarządzanie usługami sieci web przy użyciu wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="198d0-119">hello Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="198d0-120">Aby uzyskać więcej informacji, zobacz [maszyny Learning Web Service (REST)](/rest/api/machinelearning/index) odwołania.</span><span class="sxs-lookup"><span data-stu-id="198d0-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="198d0-121">Polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="198d0-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="198d0-122">Dostawca zasobów usługi Azure Machine Learning dla usług sieci web umożliwia wdrażanie i zarządzanie usługami sieci web przy użyciu poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="198d0-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="198d0-123">toouse hello poleceń cmdlet, musi pierwszy raz logujesz się tooyour konto platformy Azure w środowisku PowerShell hello przy użyciu hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="198d0-123">toouse hello cmdlets, you must first sign in tooyour Azure account from within hello PowerShell environment by using hello [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="198d0-124">Jeśli użytkownik nie zna jak toocall PowerShell poleceń, które są oparte na Menedżera zasobów, zobacz [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="198d0-124">If you are unfamiliar with how toocall PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="198d0-125">tooexport Twojego predykcyjnej eksperymentu, użyj [ten przykładowy kod](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="198d0-125">tooexport your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="198d0-126">Po utworzeniu pliku .exe hello z kodu hello można wpisać:</span><span class="sxs-lookup"><span data-stu-id="198d0-126">After you create hello .exe file from hello code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="198d0-127">Uruchomienie aplikacji hello tworzy JSON szablonu usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="198d0-127">Running hello application creates a web service JSON template.</span></span> <span data-ttu-id="198d0-128">toouse hello szablonu toodeploy usługi sieci web, należy dodać hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="198d0-128">toouse hello template toodeploy a web service, you must add hello following information:</span></span>

* <span data-ttu-id="198d0-129">Nazwa konta magazynu i klucz</span><span class="sxs-lookup"><span data-stu-id="198d0-129">Storage account name and key</span></span>

    <span data-ttu-id="198d0-130">Możesz pobrać ze strony hello albo nazwę konta magazynu hello i klucz [portalu Azure](https://portal.azure.com/) lub hello [klasycznego portalu Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="198d0-130">You can get hello storage account name and key from either hello [Azure portal](https://portal.azure.com/) or hello [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="198d0-131">Identyfikator planu zobowiązań</span><span class="sxs-lookup"><span data-stu-id="198d0-131">Commitment plan ID</span></span>

    <span data-ttu-id="198d0-132">Identyfikator planu hello można uzyskać z hello [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu, rejestrując się i klikając nazwę planu.</span><span class="sxs-lookup"><span data-stu-id="198d0-132">You can get hello plan ID from hello [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="198d0-133">Dodaj je toohello JSON szablonu jako elementy podrzędne hello *właściwości* węzeł hello sam poziom jako hello *MachineLearningWorkspace* węzła.</span><span class="sxs-lookup"><span data-stu-id="198d0-133">Add them toohello JSON template as children of hello *Properties* node at hello same level as hello *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="198d0-134">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="198d0-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="198d0-135">Zobacz następujące artykuły hello i przykładowy kod, aby uzyskać dodatkowe szczegóły:</span><span class="sxs-lookup"><span data-stu-id="198d0-135">See hello following articles and sample code for additional details:</span></span>

* <span data-ttu-id="198d0-136">[Polecenia cmdlet systemu Azure Learning maszyny](https://msdn.microsoft.com/library/azure/mt767952.aspx) odwołania w witrynie MSDN</span><span class="sxs-lookup"><span data-stu-id="198d0-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="198d0-137">Przykładowe [wskazówki](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="198d0-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-hello-web-services"></a><span data-ttu-id="198d0-138">Stosowanie hello usług sieci web</span><span class="sxs-lookup"><span data-stu-id="198d0-138">Consume hello web services</span></span>
### <a name="from-hello-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="198d0-139">Z hello Azure Machine Learning usług interfejsie użytkownika sieci Web (testowanie)</span><span class="sxs-lookup"><span data-stu-id="198d0-139">From hello Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="198d0-140">Można przetestować usługi sieci web z portalu usługi sieci Web systemu Azure Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="198d0-140">You can test your web service from hello Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="198d0-141">Dotyczy to również testowania hello żądań i odpowiedzi usługi (RR) i interfejsy usługę wykonywania wsadowego (BES).</span><span class="sxs-lookup"><span data-stu-id="198d0-141">This includes testing hello Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="198d0-142">Wdrażanie nowej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="198d0-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="198d0-143">Wdrażanie usługi sieci web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="198d0-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="198d0-144">Wskazówki krok 5: Wdrażanie usługi sieci web Azure Machine Learning hello</span><span class="sxs-lookup"><span data-stu-id="198d0-144">Walkthrough Step 5: Deploy hello Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="198d0-145">Z programu Excel</span><span class="sxs-lookup"><span data-stu-id="198d0-145">From Excel</span></span>
<span data-ttu-id="198d0-146">Można pobrać szablonu programu Excel, który wykorzystuje hello usługi sieci web:</span><span class="sxs-lookup"><span data-stu-id="198d0-146">You can download an Excel template that consumes hello web service:</span></span>

* [<span data-ttu-id="198d0-147">Korzystanie z usługi sieci web uczenie maszynowe Azure z programu Excel</span><span class="sxs-lookup"><span data-stu-id="198d0-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="198d0-148">Dodatek programu Excel do usługi sieci Web systemu Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="198d0-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="198d0-149">W kliencie opartego na interfejsie REST</span><span class="sxs-lookup"><span data-stu-id="198d0-149">From a REST-based client</span></span>
<span data-ttu-id="198d0-150">Usługi sieci Web uczenie w usłudze Azure Machine są interfejsy API RESTful.</span><span class="sxs-lookup"><span data-stu-id="198d0-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="198d0-151">Będzie można korzystać z poniższych interfejsów API z różnych platform, takich jak .NET, Python, R, Java, hello itp. **Consume** stronę usługi sieci web na powitania [portal usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net) ma próbki Kod, który może pomóc rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="198d0-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. hello **Consume** page for your web service on hello [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="198d0-152">Aby uzyskać więcej informacji, zobacz [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="198d0-152">For more information, see [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
