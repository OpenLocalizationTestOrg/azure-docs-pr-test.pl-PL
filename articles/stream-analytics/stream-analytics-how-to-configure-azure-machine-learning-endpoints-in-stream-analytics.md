---
title: "Korzystanie z punktów końcowych usługi Azure Machine Learning w Stream Analytics | Dokumentacja firmy Microsoft"
description: "Funkcje zdefiniowane przez użytkownika język maszyny w analiza strumienia"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: d3a46190dd802bf31ea03ef38304d58e6e63b66d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="b4422-103">Maszyny Learning integracji usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="b4422-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="b4422-104">Analiza strumienia obsługuje funkcje zdefiniowane przez użytkownika, które wyróżnienia do punktów końcowych usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b4422-104">Stream Analytics supports user-defined functions that call out to Azure Machine Learning endpoints.</span></span> <span data-ttu-id="b4422-105">Obsługa interfejsu API REST dla tej funkcji została szczegółowo opisana w [biblioteki interfejsu API REST usługi analiza strumienia](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="b4422-105">REST API support for this feature is detailed in the [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="b4422-106">Ten artykuł zawiera dodatkowe informacje potrzebne do pomyślnego wykonania tej funkcji w Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="b4422-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="b4422-107">Samouczek również została opublikowana i jest dostępny [tutaj](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b4422-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="b4422-108">Omówienie: Usługa Azure Machine Learning terminologia</span><span class="sxs-lookup"><span data-stu-id="b4422-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="b4422-109">Microsoft Azure Machine Learning zapewnia narzędzia współpracy, przeciągnij i upuść, używanego do tworzenia, testowania i wdrażania rozwiązań analizy predykcyjnej na podstawie danych.</span><span class="sxs-lookup"><span data-stu-id="b4422-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="b4422-110">To narzędzie jest nazywany *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="b4422-110">This tool is called the *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="b4422-111">Studio służy do interakcji z zasobami uczenia maszynowego i łatwy sposób tworzenia, testowania i iterację projektu.</span><span class="sxs-lookup"><span data-stu-id="b4422-111">The studio is used to interact with the Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="b4422-112">Poniżej są tych zasobów i ich definicje.</span><span class="sxs-lookup"><span data-stu-id="b4422-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="b4422-113">**Obszar roboczy**: *obszaru roboczego* jest kontenerem, który zawiera inne zasoby usługi Machine Learning razem w kontenerze zarządzania i kontroli.</span><span class="sxs-lookup"><span data-stu-id="b4422-113">**Workspace**: The *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="b4422-114">**Eksperymentu**: *eksperymenty* są tworzone przez analityków danych, do korzystania z zestawów danych i uczenia modelu uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="b4422-114">**Experiment**: *Experiments* are created by data scientists to utilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="b4422-115">**Punkt końcowy**: *punkty końcowe* są Azure Machine Learning obiekt używany do wybranie funkcji jako dane wejściowe, modelu uczenia maszynowego określonego i zwraca scored danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="b4422-115">**Endpoint**: *Endpoints* are the Azure Machine Learning object used to take features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="b4422-116">**Ocenianie usługi sieci Web**: A *oceniania webservice* jest kolekcją punktów końcowych, jak wspomniano powyżej.</span><span class="sxs-lookup"><span data-stu-id="b4422-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="b4422-117">Każdy punkt końcowy ma interfejsów API dla wykonywania wsadowego i wykonywania synchronicznego.</span><span class="sxs-lookup"><span data-stu-id="b4422-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="b4422-118">Analiza strumienia używa synchronicznej.</span><span class="sxs-lookup"><span data-stu-id="b4422-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="b4422-119">Nosi nazwę określonej usługi [żądania/odpowiedzi usługi](../machine-learning/machine-learning-consume-web-services.md) w studio uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="b4422-119">The specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="b4422-120">Zasobów niezbędnych do zadania usługi analiza strumienia uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="b4422-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="b4422-121">Na potrzeby usługi analiza strumienia zadania przetwarzania punktu końcowego żądanie/odpowiedź [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), i definicji struktury swagger są wszystkie niezbędne do pomyślnego wykonania.</span><span class="sxs-lookup"><span data-stu-id="b4422-121">For the purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="b4422-122">Analiza strumienia ma dodatkowe punktu końcowego, który konstruuje adres url punktu końcowego struktury swagger, wyszukuje interfejsu i zwraca domyślną definicją funkcji zdefiniowanej przez użytkownika dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b4422-122">Stream Analytics has an additional endpoint that constructs the url for swagger endpoint, looks up the interface and returns a default UDF definition to the user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="b4422-123">Konfigurowanie usługi analiza strumienia i funkcji zdefiniowanej przez użytkownika za pomocą interfejsu API REST uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="b4422-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="b4422-124">Za pomocą interfejsów API REST można tak skonfigurować zadanie do wywołania funkcji Azure maszyny języka.</span><span class="sxs-lookup"><span data-stu-id="b4422-124">By using REST APIs you may configure your job to call Azure Machine Language functions.</span></span> <span data-ttu-id="b4422-125">Dostępne są następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b4422-125">The steps are as follows:</span></span>

1. <span data-ttu-id="b4422-126">Tworzenie zadania usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b4422-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="b4422-127">Zdefiniuj dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="b4422-127">Define an input</span></span>
3. <span data-ttu-id="b4422-128">Definiowanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="b4422-128">Define an output</span></span>
4. <span data-ttu-id="b4422-129">Tworzenie funkcji zdefiniowanej przez użytkownika (UDF)</span><span class="sxs-lookup"><span data-stu-id="b4422-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="b4422-130">Zapis transformację Stream Analytics, która wywołuje funkcję zdefiniowaną przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="b4422-130">Write a Stream Analytics transformation that calls the UDF</span></span>
6. <span data-ttu-id="b4422-131">Uruchom zadanie</span><span class="sxs-lookup"><span data-stu-id="b4422-131">Start the job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="b4422-132">Tworzenie funkcji zdefiniowanej przez użytkownika za pomocą właściwości podstawowe</span><span class="sxs-lookup"><span data-stu-id="b4422-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="b4422-133">Na przykład następujący przykładowy kod tworzy skalarne funkcji zdefiniowanej przez użytkownika o nazwie *newudf* wiąże punktu końcowego uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="b4422-133">As an example, the following sample code creates a scalar UDF named *newudf* that binds to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="b4422-134">Należy pamiętać, że *punktu końcowego* (identyfikator URI usługi) można znaleźć na stronie pomocy interfejsu API dla wybranych usług i *apiKey* można znaleźć na stronie głównej usług.</span><span class="sxs-lookup"><span data-stu-id="b4422-134">Note that the *endpoint* (service URI) can be found on the API help page for the chosen service and the *apiKey* can be found on the Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="b4422-135">Przykład treści żądania:</span><span class="sxs-lookup"><span data-stu-id="b4422-135">Example request body:</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="b4422-136">Punkt końcowy RetrieveDefaultDefinition wywołanie domyślnego funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="b4422-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="b4422-137">Utworzone szkielet UDF pełnej definicji funkcji zdefiniowanej przez użytkownika jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="b4422-137">Once the skeleton UDF is created the complete definition of the UDF is needed.</span></span> <span data-ttu-id="b4422-138">Punkt końcowy RetreiveDefaultDefinition ułatwia rozpoczęcie definicji domyślnej dla funkcji skalarnej powiązanej z punktem końcowym usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b4422-138">The RetreiveDefaultDefinition endpoint helps you get the default definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="b4422-139">Ładunek poniżej wymaga pobrania domyślnej definicji funkcji zdefiniowanej przez użytkownika dla funkcji skalarnej powiązanej z punktem końcowym usługi Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b4422-139">The payload below requires you to get the default UDF definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="b4422-140">Rzeczywisty punkt końcowy go nie określa, jak zostały już dostarczone podczas żądania PUT.</span><span class="sxs-lookup"><span data-stu-id="b4422-140">It doesn’t specify the actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="b4422-141">Analiza strumienia wywołuje podany w żądaniu, jeśli podano jawnie punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="b4422-141">Stream Analytics calls the endpoint provided in the request if it is provided explicitly.</span></span> <span data-ttu-id="b4422-142">W przeciwnym razie używa jednego oryginalnie odwołuje się do.</span><span class="sxs-lookup"><span data-stu-id="b4422-142">Otherwise it uses the one originally referenced.</span></span> <span data-ttu-id="b4422-143">W tym miejscu ma UDF ciągu pojedynczy parametr (zdania) i zwraca jeden wyjściowy typu ciąg, co oznacza etykietę "wskaźniki nastrojów klientów" zdanie to.</span><span class="sxs-lookup"><span data-stu-id="b4422-143">Here the UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates the “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="b4422-144">Przykład treści żądania:</span><span class="sxs-lookup"><span data-stu-id="b4422-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="b4422-145">Przykładowe dane wyjściowe tego poszukać coś chcieliby poniżej.</span><span class="sxs-lookup"><span data-stu-id="b4422-145">A sample output of this would look something like below.</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-the-response"></a><span data-ttu-id="b4422-146">Poprawka UDF z odpowiedzią</span><span class="sxs-lookup"><span data-stu-id="b4422-146">Patch UDF with the response</span></span>
<span data-ttu-id="b4422-147">Teraz UDF muszą poprawiono z poprzedniej odpowiedzi, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="b4422-147">Now the UDF must be patched with the previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="b4422-148">Treść żądania (dane wyjściowe z RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="b4422-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-to-call-the-udf"></a><span data-ttu-id="b4422-149">Wdrożenie usługi analiza strumienia transformacji wywołać funkcję zdefiniowaną przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="b4422-149">Implement Stream Analytics transformation to call the UDF</span></span>
<span data-ttu-id="b4422-150">Teraz zapytanie UDF (w tym miejscu o nazwie scoreTweet) dla każdego zdarzenia wejściowe i zapisać dane wyjściowe odpowiedzi dla tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="b4422-150">Now query the UDF (here named scoreTweet) for every input event and write a response for that event to an output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="b4422-151">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="b4422-151">Get help</span></span>
<span data-ttu-id="b4422-152">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="b4422-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4422-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4422-153">Next steps</span></span>
* [<span data-ttu-id="b4422-154">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b4422-154">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="b4422-155">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="b4422-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="b4422-156">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="b4422-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="b4422-157">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="b4422-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="b4422-158">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="b4422-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
