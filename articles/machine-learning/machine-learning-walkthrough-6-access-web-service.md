---
title: "Krok 6: Dostęp do usługi Machine Learning Web | Dokumentacja firmy Microsoft"
description: "Krok 6 opracowanie wskazówki rozwiązanie predykcyjne: dostęp do usługi sieci Web Azure Machine Learning active."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a65c89a-40ab-4673-8dd8-8eee0a150e3b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: d309f6c4749a80c81859b693a2bd5927e8fe0e54
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-step-6-access-the-azure-machine-learning-web-service"></a><span data-ttu-id="97e09-103">Przewodnik, krok 6. Dostęp do usługi sieci Web Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="97e09-103">Walkthrough Step 6: Access the Azure Machine Learning web service</span></span>

<span data-ttu-id="97e09-104">Jest to ostatni krok wskazówki, [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="97e09-104">This is the last step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="97e09-105">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="97e09-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="97e09-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="97e09-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="97e09-107">Tworzenie nowego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="97e09-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="97e09-108">Nauczanie i ocena modeli</span><span class="sxs-lookup"><span data-stu-id="97e09-108">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="97e09-109">Wdrażanie usługi sieci Web</span><span class="sxs-lookup"><span data-stu-id="97e09-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="97e09-110">**Dostęp do usługi sieci Web**</span><span class="sxs-lookup"><span data-stu-id="97e09-110">**Access the Web service**</span></span>

- - -
<span data-ttu-id="97e09-111">Usługi sieci web, która używa modelu prognozowania ryzyko kredytowe wdrożyliśmy w poprzednim kroku, w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="97e09-111">In the previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="97e09-112">Teraz użytkownicy mogą wysyłać dane do niego i otrzymywania wyników.</span><span class="sxs-lookup"><span data-stu-id="97e09-112">Now users are able to send data to it and receive results.</span></span> 

<span data-ttu-id="97e09-113">Usługa sieci Web jest usługą sieci web platformy Azure, która umożliwia odbieranie i zwrócić dane przy użyciu interfejsów API REST w jeden z dwóch sposobów:</span><span class="sxs-lookup"><span data-stu-id="97e09-113">The Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="97e09-114">**Żądanie/odpowiedź** — użytkownik wysyła co najmniej jeden wiersz danych środki do usługi przy użyciu protokołu HTTP, a usługa odpowiada z jednego lub więcej zestawów wyników.</span><span class="sxs-lookup"><span data-stu-id="97e09-114">**Request/Response** - The user sends one or more rows of credit data to the service by using an HTTP protocol, and the service responds with one or more sets of results.</span></span>
* <span data-ttu-id="97e09-115">**Wykonywanie wsadowe** — użytkownik przechowuje jednego lub większej liczby wierszy danych środki na platformie Azure blob, a następnie wysyła lokalizacji obiektu blob do usługi.</span><span class="sxs-lookup"><span data-stu-id="97e09-115">**Batch Execution** - The user stores one or more rows of credit data in an Azure blob and then sends the blob location to the service.</span></span> <span data-ttu-id="97e09-116">Usługa wyników wszystkich wierszy danych w blob danych wejściowych, przechowuje wyniki w innym obiekcie blob i zwraca adres URL tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="97e09-116">The service scores all the rows of data in the input blob, stores the results in another blob, and returns the URL of that container.</span></span>  

<span data-ttu-id="97e09-117">Jest najszybszym i Najprostszym sposobem uzyskania dostępu do usługi sieci web klasycznego za pośrednictwem [aplikacji sieci Web usługi Azure ML żądanie-odpowiedź](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) lub [szablonu aplikacji sieci Web Azure ML partii wykonywania usługi](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="97e09-117">The quickest and easiest way to access a Classic web service is through the [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="97e09-118">Te szablony aplikacji sieci web można utworzyć aplikacji sieci web niestandardowego, który zna usługi sieci web dane wejściowe i co zwróci.</span><span class="sxs-lookup"><span data-stu-id="97e09-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="97e09-119">Wszystko, co należy zrobić to zapewniają dostęp do danych i usługi sieci web, a reszta szablonu.</span><span class="sxs-lookup"><span data-stu-id="97e09-119">All you need to do is provide access to your web service and data, and the template does the rest.</span></span>

<span data-ttu-id="97e09-120">Aby uzyskać więcej informacji na temat używania szablonów aplikacji sieci web, zobacz [korzystać z usługi Azure Machine Learning w sieci Web przy użyciu szablonu aplikacji sieci web](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="97e09-120">For more information on using the web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="97e09-121">Można również zaprojektować aplikacji niestandardowej do uzyskania dostępu do usługi sieci web przy użyciu kodu starter dostarczany w R, C# i języki programowania Python.</span><span class="sxs-lookup"><span data-stu-id="97e09-121">You can also develop a custom application to access the web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="97e09-122">Można znaleźć szczegółowe informacje w [jak korzystać z usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="97e09-122">You can find complete details in [How to consume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

