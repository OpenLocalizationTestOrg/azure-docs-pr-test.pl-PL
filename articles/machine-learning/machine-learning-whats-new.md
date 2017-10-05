---
title: What's new in Azure Machine Learning | Dokumentacja firmy Microsoft
description: "Nowe funkcje, które są dostępne w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: vDonGlover
manager: raymondl
editor: 
ms.assetid: ddc716ed-2615-4806-bf27-6c9a5662a7f2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/28/2017
ms.author: v-donglo
ms.openlocfilehash: 551b977b90612ddbfa1514a9c2358ebf8179c385
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="whats-new-in-azure-machine-learning"></a><span data-ttu-id="a52c6-103">Co nowego w usłudze Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a52c6-103">What's New in Azure Machine Learning</span></span>

### <a name="the-march-2017-release-of-microsoft-azure-machine-learning-updates-provides-the-following-feature"></a><span data-ttu-id="a52c6-104">Wersja 2017 marca aktualizacje Microsoft Azure Machine Learning zapewnia następującej funkcji:</span><span class="sxs-lookup"><span data-stu-id="a52c6-104">The March 2017 release of Microsoft Azure Machine Learning updates provides the following feature:</span></span>



* <span data-ttu-id="a52c6-105">Dedykowany pojemności dla usługi Azure Machine Learning BES zadań</span><span class="sxs-lookup"><span data-stu-id="a52c6-105">Dedicated Capacity for Azure Machine Learning BES Jobs</span></span>

    <span data-ttu-id="a52c6-106">Maszyny przetwarzania używa puli partii Learning [partii zadań Azure](../batch/batch-technical-overview.md) usługą skalowalnego zarządzany przez klienta dla usługi Azure Machine Learning partii wykonywania.</span><span class="sxs-lookup"><span data-stu-id="a52c6-106">Machine Learning Batch Pool processing uses the [Azure Batch](../batch/batch-technical-overview.md) service to provide customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="a52c6-107">Przetwarzanie wsadowe puli służy do tworzenia pul partii zadań Azure, na których przesyłania zadań wsadowych i je w sposób przewidywalne.</span><span class="sxs-lookup"><span data-stu-id="a52c6-107">Batch Pool processing allows you to create Azure Batch pools on which you can submit batch jobs and have them execute in a predictable manner.</span></span>

    <span data-ttu-id="a52c6-108">Aby uzyskać więcej informacji, zobacz [usługi partia zadań Azure Machine Learning zadań](machine-learning-dedicated-capacity-for-bes-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="a52c6-108">For more information, see [Azure Batch service for Machine Learning jobs](machine-learning-dedicated-capacity-for-bes-jobs.md).</span></span>


### <a name="the-august-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="a52c6-109">Wersja sierpnia 2016 Microsoft Azure Machine Learning aktualizacje zapewniają następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="a52c6-109">The August 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="a52c6-110">Teraz można zarządzać klasycznym usługi sieci Web w nowej [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/) portal, który zawiera w jednym miejscu, aby zarządzać wszystkimi aspektami usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a52c6-110">Classic Web services can now be managed in the new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>    
  * <span data-ttu-id="a52c6-111">Zapewniające usługi sieci web [statystyk użycia](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="a52c6-111">Which provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
  * <span data-ttu-id="a52c6-112">Upraszcza testowania wywołań Azure Machine Learning zdalnego żądania przy użyciu przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="a52c6-112">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
  * <span data-ttu-id="a52c6-113">Udostępnia nową stroną testową usługi wykonywania wsadowego z historią przesyłania przykładowych danych i zadania.</span><span class="sxs-lookup"><span data-stu-id="a52c6-113">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>
  * <span data-ttu-id="a52c6-114">Umożliwia łatwiejsze zarządzanie punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="a52c6-114">Provides easier endpoint management.</span></span>

### <a name="the-july-2016-release-of-microsoft-azure-machine-learning-updates-provide-the-following-features"></a><span data-ttu-id="a52c6-115">Wersja lipca 2016 aktualizacje Microsoft Azure Machine Learning zapewniają następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="a52c6-115">The July 2016 release of Microsoft Azure Machine Learning updates provide the following features:</span></span>
* <span data-ttu-id="a52c6-116">Usługi sieci Web są teraz zarządzane jako zasobów platformy Azure zarządzanych za pomocą [usługi Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) interfejsów, co zapewnia następujące udoskonalenia:</span><span class="sxs-lookup"><span data-stu-id="a52c6-116">Web services are now managed as Azure resources managed through [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) interfaces, allowing for the following enhancements:</span></span>
  * <span data-ttu-id="a52c6-117">Istnieją nowe [interfejsów API REST](https://msdn.microsoft.com/library/azure/Dn950030.aspx) wdrażania i zarządzania nimi Menedżera zasobów na podstawie usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a52c6-117">There are new [REST APIs](https://msdn.microsoft.com/library/azure/Dn950030.aspx) to deploy and manage your Resource Manager based Web services.</span></span>
  * <span data-ttu-id="a52c6-118">Jest dostępna nowa [usługi sieci Web Microsoft Azure Machine Learning](https://services.azureml.net/) portal, który zawiera w jednym miejscu, aby zarządzać wszystkimi aspektami usługi sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a52c6-118">There is a new [Microsoft Azure Machine Learning Web Services](https://services.azureml.net/) portal that provides one place to manage all aspects of your Web service.</span></span>
* <span data-ttu-id="a52c6-119">Umowa zawiera nowe interfejsy API wykorzystaniu dostawcy zasobów Menedżera zasobów dla usług sieci Web na podstawie modelu wdrażania usług sieci web subskrypcji, w przypadku korzystania z Menedżera zasobów.</span><span class="sxs-lookup"><span data-stu-id="a52c6-119">Incorporates a new subscription-based, multi-region web service deployment model using Resource Manager based APIs leveraging the Resource Manager Resource Provider for Web Services.</span></span>
* <span data-ttu-id="a52c6-120">Wprowadzono nowe [planów cenowych](https://azure.microsoft.com/pricing/details/machine-learning/) i planowanie możliwości zarządzania przy użyciu nowego planu odzyskiwania Menedżera zasobów dla rozliczeń.</span><span class="sxs-lookup"><span data-stu-id="a52c6-120">Introduces new [pricing plans](https://azure.microsoft.com/pricing/details/machine-learning/) and plan management capabilities using the new Resource Manager RP for Billing.</span></span>
  * <span data-ttu-id="a52c6-121">Możesz teraz [wdrażanie usługi sieci web na wiele regionów](machine-learning-how-to-deploy-to-multiple-regions.md) bez konieczności tworzenia subskrypcji w każdym regionie.</span><span class="sxs-lookup"><span data-stu-id="a52c6-121">You can now [deploy your web service to multiple regions](machine-learning-how-to-deploy-to-multiple-regions.md) without needing to create a subscription in each region.</span></span>
* <span data-ttu-id="a52c6-122">Usługa sieci web [statystyk użycia](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="a52c6-122">Provides web service [usage statistics](machine-learning-manage-new-webservice.md).</span></span>
* <span data-ttu-id="a52c6-123">Upraszcza testowania wywołań Azure Machine Learning zdalnego żądania przy użyciu przykładowych danych.</span><span class="sxs-lookup"><span data-stu-id="a52c6-123">Simplifies testing of Azure Machine Learning Remote-Request calls using sample data.</span></span>
* <span data-ttu-id="a52c6-124">Udostępnia nową stroną testową usługi wykonywania wsadowego z historią przesyłania przykładowych danych i zadania.</span><span class="sxs-lookup"><span data-stu-id="a52c6-124">Provides a new Batch Execution Service test page with sample data and job submission history.</span></span>

<span data-ttu-id="a52c6-125">Ponadto Machine Learning Studio została zaktualizowana, aby umożliwić Wdrażanie nowego modelu usług sieci Web, lub Kontynuuj wdrażanie klasycznego modelu usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="a52c6-125">In addition, the Machine Learning Studio has been updated to allow you to deploy to the new Web service model or continue to deploy to the classic Web service model.</span></span> 

