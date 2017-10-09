---
title: "Krok 6: Dostęp do usługi Machine Learning Web hello | Dokumentacja firmy Microsoft"
description: "Krok 6 hello opracowanie wskazówki rozwiązanie predykcyjne: dostęp do usługi sieci Web Azure Machine Learning active."
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
ms.openlocfilehash: 211de0294092c6a6b5e6eb608d5d3b88107674c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-step-6-access-hello-azure-machine-learning-web-service"></a><span data-ttu-id="63732-103">Wskazówki krok 6: Hello dostępu do usługi sieci web uczenie maszynowe Azure</span><span class="sxs-lookup"><span data-stu-id="63732-103">Walkthrough Step 6: Access hello Azure Machine Learning web service</span></span>

<span data-ttu-id="63732-104">Jest to ostatni krok wskazówki hello hello [tworzenie rozwiązania analizy predykcyjnej w usłudze Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="63732-104">This is hello last step of hello walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="63732-105">Tworzenie obszaru roboczego usługi Machine Learning</span><span class="sxs-lookup"><span data-stu-id="63732-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="63732-106">Przekazywanie istniejących danych</span><span class="sxs-lookup"><span data-stu-id="63732-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="63732-107">Tworzenie nowego eksperymentu</span><span class="sxs-lookup"><span data-stu-id="63732-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="63732-108">Nauczanie i Ewaluacja modeli hello</span><span class="sxs-lookup"><span data-stu-id="63732-108">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="63732-109">Wdrażanie usługi sieci Web hello</span><span class="sxs-lookup"><span data-stu-id="63732-109">Deploy hello Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. <span data-ttu-id="63732-110">**Witaj dostępu do usługi sieci Web**</span><span class="sxs-lookup"><span data-stu-id="63732-110">**Access hello Web service**</span></span>

- - -
<span data-ttu-id="63732-111">Usługi sieci web, która używa modelu prognozowania ryzyko kredytowe wdrożyliśmy w poprzednim kroku hello w tym przewodniku.</span><span class="sxs-lookup"><span data-stu-id="63732-111">In hello previous step in this walkthrough we deployed a web service that uses our credit risk prediction model.</span></span> <span data-ttu-id="63732-112">Teraz użytkownicy są w stanie toosend tooit danych i otrzymywać wyniki.</span><span class="sxs-lookup"><span data-stu-id="63732-112">Now users are able toosend data tooit and receive results.</span></span> 

<span data-ttu-id="63732-113">Hello usługi sieci Web jest usługą sieci web platformy Azure, która umożliwia odbieranie i zwrócić dane przy użyciu interfejsów API REST w jeden z dwóch sposobów:</span><span class="sxs-lookup"><span data-stu-id="63732-113">hello Web service is an Azure web service that can receive and return data using REST APIs in one of two ways:</span></span>  

* <span data-ttu-id="63732-114">**Żądanie/odpowiedź** — hello użytkownik wysyła jeden lub więcej wierszy toohello danych środki usługi za pomocą protokołu HTTP i hello odpowiada usługi z jednego lub więcej zestawów wyników.</span><span class="sxs-lookup"><span data-stu-id="63732-114">**Request/Response** - hello user sends one or more rows of credit data toohello service by using an HTTP protocol, and hello service responds with one or more sets of results.</span></span>
* <span data-ttu-id="63732-115">**Wykonywanie wsadowe** — użytkownik hello przechowuje jednego lub większej liczby wierszy danych środki na platformie Azure blob, a następnie wysyła usługi toohello lokalizacji obiektu blob hello.</span><span class="sxs-lookup"><span data-stu-id="63732-115">**Batch Execution** - hello user stores one or more rows of credit data in an Azure blob and then sends hello blob location toohello service.</span></span> <span data-ttu-id="63732-116">wyniki Hello usługi, które hello wszystkich wierszy danych w hello blob danych wejściowych, magazyny hello wyniki w innym obiekcie blob i zwraca hello adres URL tego kontenera.</span><span class="sxs-lookup"><span data-stu-id="63732-116">hello service scores all hello rows of data in hello input blob, stores hello results in another blob, and returns hello URL of that container.</span></span>  

<span data-ttu-id="63732-117">Witaj tooaccess najszybszym i Najprostszym sposobem jest klasycznym usługi sieci web za pośrednictwem hello [aplikacji sieci Web usługi Azure ML żądanie-odpowiedź](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) lub [szablonu aplikacji sieci Web Azure ML partii wykonywania usługi](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span><span class="sxs-lookup"><span data-stu-id="63732-117">hello quickest and easiest way tooaccess a Classic web service is through hello [Azure ML Request-Response Service Web App](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlaspnettemplateforrrs/) or [Azure ML Batch Execution Service Web App Template](https://azure.microsoft.com/marketplace/partners/microsoft/azuremlbeswebapptemplate/).</span></span>

<span data-ttu-id="63732-118">Te szablony aplikacji sieci web można utworzyć aplikacji sieci web niestandardowego, który zna usługi sieci web dane wejściowe i co zwróci.</span><span class="sxs-lookup"><span data-stu-id="63732-118">These web app templates can build a custom web app that knows your web service's input data and what it will return.</span></span> <span data-ttu-id="63732-119">Toodo wystarczy zapewnienia usługi sieci web tooyour dostępu i danych, a szablon hello hello rest.</span><span class="sxs-lookup"><span data-stu-id="63732-119">All you need toodo is provide access tooyour web service and data, and hello template does hello rest.</span></span>

<span data-ttu-id="63732-120">Aby uzyskać więcej informacji na temat używania szablonów aplikacji sieci web hello zobacz [korzystać z usługi Azure Machine Learning w sieci Web przy użyciu szablonu aplikacji sieci web](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="63732-120">For more information on using hello web app templates, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>

<span data-ttu-id="63732-121">Można również zaprojektować niestandardową aplikację tooaccess hello usługi sieci web przy użyciu kodu starter dostarczany w R, C# i języków programowania Python.</span><span class="sxs-lookup"><span data-stu-id="63732-121">You can also develop a custom application tooaccess hello web service using starter code provided for you in R, C#, and Python programming languages.</span></span>

<span data-ttu-id="63732-122">Można znaleźć szczegółowe informacje w [jak tooconsume usługi sieci Web Azure Machine Learning](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="63732-122">You can find complete details in [How tooconsume an Azure Machine Learning Web service](machine-learning-consume-web-services.md).</span></span>

