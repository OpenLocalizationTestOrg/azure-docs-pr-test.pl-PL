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
ms.openlocfilehash: 18edabe267ec06c08074d7a7a6d71435cedc8489
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="cec8d-103">Usługi sieci Web Azure Machine Learning: wdrażanie i korzystanie</span><span class="sxs-lookup"><span data-stu-id="cec8d-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="cec8d-104">Azure Machine Learning umożliwia wdrażanie przepływów pracy i modele jako usługi sieci web usługi machine learning.</span><span class="sxs-lookup"><span data-stu-id="cec8d-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="cec8d-105">Wywoływanie modeli uczenia maszynowego z aplikacji przez Internet w celu prognoz w czasie rzeczywistym lub w trybie wsadowym można następnie te usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="cec8d-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span></span> <span data-ttu-id="cec8d-106">Ponieważ usługi sieci web RESTful, można ich wywołać z różnych języków programowania i platform, takich jak .NET i Java i z aplikacji, takich jak program Excel.</span><span class="sxs-lookup"><span data-stu-id="cec8d-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="cec8d-107">Następne sekcje zawierają łącza do wskazówki, kodu i dokumentacji, aby ułatwić rozpoczęcie.</span><span class="sxs-lookup"><span data-stu-id="cec8d-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="cec8d-108">Wdrażanie usługi internetowej</span><span class="sxs-lookup"><span data-stu-id="cec8d-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="cec8d-109">Za pomocą usługi Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="cec8d-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="cec8d-110">Usługa Machine Learning Studio i portalu usługi sieci Web Microsoft Azure Machine Learning ułatwiające wdrażanie i zarządzanie usługi sieci web bez konieczności pisania kodu.</span><span class="sxs-lookup"><span data-stu-id="cec8d-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="cec8d-111">Poniższe łącza zawierają ogólne informacje dotyczące sposobu wdrażania nową usługę sieci web:</span><span class="sxs-lookup"><span data-stu-id="cec8d-111">The following links provide general Information about how to deploy a new web service:</span></span>

* <span data-ttu-id="cec8d-112">Aby uzyskać ogólne informacje o sposobie wdrażania nową usługę sieci web, która jest oparta na usłudze Azure Resource Manager, zobacz [wdrożenie nowej usługi sieci web](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="cec8d-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="cec8d-113">Aby uzyskać wskazówki dotyczące wdrażania usługi sieci web, zobacz [wdrażanie usługi sieci web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="cec8d-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="cec8d-114">Aby pełna wskazówki dotyczące sposobu tworzenia i wdrażania usługi sieci web, zobacz [wskazówki krok 1: tworzenie obszaru roboczego uczenia maszynowego](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="cec8d-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="cec8d-115">Aby uzyskać szczegółowe przykłady, które wdrażanie usługi sieci web zobacz:</span><span class="sxs-lookup"><span data-stu-id="cec8d-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="cec8d-116">Wskazówki krok 5: Wdrażanie usługi sieci web uczenie maszynowe Azure</span><span class="sxs-lookup"><span data-stu-id="cec8d-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="cec8d-117">Jak wdrożyć usługę sieci web w wielu regionach</span><span class="sxs-lookup"><span data-stu-id="cec8d-117">How to deploy a web service to multiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="cec8d-118">Z dostawcy zasobów usługi sieci web API (interfejsów API usługi Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="cec8d-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="cec8d-119">Dostawcy zasobów usługi Azure Machine Learning dla usług sieci web umożliwia wdrażanie i zarządzanie usługami sieci web przy użyciu wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="cec8d-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="cec8d-120">Aby uzyskać więcej informacji, zobacz [maszyny Learning Web Service (REST)](/rest/api/machinelearning/index) odwołania.</span><span class="sxs-lookup"><span data-stu-id="cec8d-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="cec8d-121">Polecenia cmdlet programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="cec8d-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="cec8d-122">Dostawca zasobów usługi Azure Machine Learning dla usług sieci web umożliwia wdrażanie i zarządzanie usługami sieci web przy użyciu poleceń cmdlet programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cec8d-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="cec8d-123">Aby używać poleceń cmdlet, należy najpierw zalogować się do konta z platformy Azure w środowisku PowerShell przy użyciu [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cec8d-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="cec8d-124">Jeśli znasz sposób wywoływania polecenia programu PowerShell, które są oparte na Resource Manager, zobacz temat [przy użyciu programu Azure PowerShell z usługą Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="cec8d-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="cec8d-125">Aby wyeksportować predykcyjnej eksperymentu, należy użyć [ten przykładowy kod](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="cec8d-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="cec8d-126">Po utworzeniu pliku .exe z kodu można wpisać:</span><span class="sxs-lookup"><span data-stu-id="cec8d-126">After you create the .exe file from the code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="cec8d-127">Uruchamianie aplikacji powoduje utworzenie szablonu JSON usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="cec8d-127">Running the application creates a web service JSON template.</span></span> <span data-ttu-id="cec8d-128">Aby użyć szablonu, aby wdrożyć usługę sieci web, należy dodać następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="cec8d-128">To use the template to deploy a web service, you must add the following information:</span></span>

* <span data-ttu-id="cec8d-129">Nazwa konta magazynu i klucz</span><span class="sxs-lookup"><span data-stu-id="cec8d-129">Storage account name and key</span></span>

    <span data-ttu-id="cec8d-130">Nazwa konta magazynu i klucza można uzyskać z dowolnej [portalu Azure](https://portal.azure.com/) lub [klasycznego portalu Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="cec8d-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="cec8d-131">Identyfikator planu zobowiązań</span><span class="sxs-lookup"><span data-stu-id="cec8d-131">Commitment plan ID</span></span>

    <span data-ttu-id="cec8d-132">Otrzymasz identyfikator planu z [usługi sieci Web systemu Azure Machine Learning](https://services.azureml.net) portalu, rejestrując się i klikając nazwę planu.</span><span class="sxs-lookup"><span data-stu-id="cec8d-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="cec8d-133">Dodaj je do formatu JSON szablonu jako elementy podrzędne *właściwości* węzłów na tym samym poziomie jako *MachineLearningWorkspace* węzła.</span><span class="sxs-lookup"><span data-stu-id="cec8d-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="cec8d-134">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="cec8d-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="cec8d-135">Zobacz następujące artykuły i przykładowy kod, aby uzyskać dodatkowe szczegóły:</span><span class="sxs-lookup"><span data-stu-id="cec8d-135">See the following articles and sample code for additional details:</span></span>

* <span data-ttu-id="cec8d-136">[Polecenia cmdlet systemu Azure Learning maszyny](https://msdn.microsoft.com/library/azure/mt767952.aspx) odwołania w witrynie MSDN</span><span class="sxs-lookup"><span data-stu-id="cec8d-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="cec8d-137">Przykładowe [wskazówki](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) w witrynie GitHub</span><span class="sxs-lookup"><span data-stu-id="cec8d-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-the-web-services"></a><span data-ttu-id="cec8d-138">Korzystanie z usług sieci web</span><span class="sxs-lookup"><span data-stu-id="cec8d-138">Consume the web services</span></span>
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="cec8d-139">Z usług sieci Web Azure Machine Learning interfejsu użytkownika (testowanie)</span><span class="sxs-lookup"><span data-stu-id="cec8d-139">From the Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="cec8d-140">Można przetestować usługi sieci web z portalu usługi sieci Web systemu Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="cec8d-140">You can test your web service from the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="cec8d-141">Dotyczy to również testowania usługi żądań i odpowiedzi (RR) i interfejsy usługę wykonywania wsadowego (BES).</span><span class="sxs-lookup"><span data-stu-id="cec8d-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="cec8d-142">Wdrażanie nowej usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="cec8d-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="cec8d-143">Wdrażanie usługi sieci web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cec8d-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="cec8d-144">Wskazówki krok 5: Wdrażanie usługi sieci web uczenie maszynowe Azure</span><span class="sxs-lookup"><span data-stu-id="cec8d-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="cec8d-145">Z programu Excel</span><span class="sxs-lookup"><span data-stu-id="cec8d-145">From Excel</span></span>
<span data-ttu-id="cec8d-146">Można pobrać szablonu programu Excel, który wykorzystuje usługę sieci web:</span><span class="sxs-lookup"><span data-stu-id="cec8d-146">You can download an Excel template that consumes the web service:</span></span>

* [<span data-ttu-id="cec8d-147">Korzystanie z usługi sieci web uczenie maszynowe Azure z programu Excel</span><span class="sxs-lookup"><span data-stu-id="cec8d-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="cec8d-148">Dodatek programu Excel do usługi sieci Web systemu Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cec8d-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="cec8d-149">W kliencie opartego na interfejsie REST</span><span class="sxs-lookup"><span data-stu-id="cec8d-149">From a REST-based client</span></span>
<span data-ttu-id="cec8d-150">Usługi sieci Web uczenie w usłudze Azure Machine są interfejsy API RESTful.</span><span class="sxs-lookup"><span data-stu-id="cec8d-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="cec8d-151">Będzie można korzystać z poniższych interfejsów API z różnych platform, takich jak .NET, Python, R, Java, itp. **Consume** strony usługi sieci web na [portal usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net) zawiera przykładowy kod, który może pomóc Ci rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="cec8d-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="cec8d-152">Aby uzyskać więcej informacji, zobacz [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md) (Jak korzystać z usługi internetowej Azure Machine Learning).</span><span class="sxs-lookup"><span data-stu-id="cec8d-152">For more information, see [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>
