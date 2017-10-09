---
title: "punkty końcowe usługi Azure Machine Learning aaaUse w Stream Analytics | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 013b841ee85b1e0b6d8139a9ba0dde88fc3f8ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="f2467-103">Maszyny Learning integracji usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="f2467-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="f2467-104">Analiza strumienia obsługuje funkcji zdefiniowanych przez użytkownika, które wywołują się punkty końcowe usługi Machine Learning tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f2467-104">Stream Analytics supports user-defined functions that call out tooAzure Machine Learning endpoints.</span></span> <span data-ttu-id="f2467-105">Obsługa interfejsu API REST dla tej funkcji została szczegółowo opisana na powitania [biblioteki interfejsu API REST usługi analiza strumienia](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2467-105">REST API support for this feature is detailed in hello [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="f2467-106">Ten artykuł zawiera dodatkowe informacje potrzebne do pomyślnego wykonania tej funkcji w Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="f2467-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="f2467-107">Samouczek również została opublikowana i jest dostępny [tutaj](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="f2467-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="f2467-108">Omówienie: Usługa Azure Machine Learning terminologia</span><span class="sxs-lookup"><span data-stu-id="f2467-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="f2467-109">Microsoft Azure Machine Learning zapewnia narzędzia współpracy, przeciągnij i upuść, można użyć toobuild, testowania i wdrażania rozwiązań analizy predykcyjnej na podstawie danych.</span><span class="sxs-lookup"><span data-stu-id="f2467-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use toobuild, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="f2467-110">To narzędzie jest nazywany hello *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="f2467-110">This tool is called hello *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="f2467-111">Hello studio jest używany toointeract z hello zasobów uczenia maszynowego i łatwe tworzenie, testowanie i wykonywanie kolejnych iteracji projektu.</span><span class="sxs-lookup"><span data-stu-id="f2467-111">hello studio is used toointeract with hello Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="f2467-112">Poniżej są tych zasobów i ich definicje.</span><span class="sxs-lookup"><span data-stu-id="f2467-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="f2467-113">**Obszar roboczy**: hello *obszaru roboczego* jest kontenerem, który zawiera inne zasoby usługi Machine Learning razem w kontenerze zarządzania i kontroli.</span><span class="sxs-lookup"><span data-stu-id="f2467-113">**Workspace**: hello *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="f2467-114">**Eksperymentu**: *eksperymenty* zostały utworzone przy użyciu zestawów danych służące tooutilize danych oraz uczenia modelu uczenia maszynowego.</span><span class="sxs-lookup"><span data-stu-id="f2467-114">**Experiment**: *Experiments* are created by data scientists tooutilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="f2467-115">**Punkt końcowy**: *punkty końcowe* hello Azure Machine Learning funkcji tootake obiekt używany jako dane wejściowe, zastosuj modelu uczenia maszynowego określonego i zwraca scored danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="f2467-115">**Endpoint**: *Endpoints* are hello Azure Machine Learning object used tootake features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="f2467-116">**Ocenianie usługi sieci Web**: A *oceniania webservice* jest kolekcją punktów końcowych, jak wspomniano powyżej.</span><span class="sxs-lookup"><span data-stu-id="f2467-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="f2467-117">Każdy punkt końcowy ma interfejsów API dla wykonywania wsadowego i wykonywania synchronicznego.</span><span class="sxs-lookup"><span data-stu-id="f2467-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="f2467-118">Analiza strumienia używa synchronicznej.</span><span class="sxs-lookup"><span data-stu-id="f2467-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="f2467-119">nosi nazwę określonej usługi Hello [żądania/odpowiedzi usługi](../machine-learning/machine-learning-consume-web-services.md) w studio uczenie maszynowe Azure.</span><span class="sxs-lookup"><span data-stu-id="f2467-119">hello specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="f2467-120">Zasobów niezbędnych do zadania usługi analiza strumienia uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="f2467-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="f2467-121">Hello celów usługi analiza strumienia zadania przetwarzania punktu końcowego żądanie/odpowiedź [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), i definicji struktury swagger są wszystkie niezbędne do pomyślnego wykonania.</span><span class="sxs-lookup"><span data-stu-id="f2467-121">For hello purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="f2467-122">Analiza strumienia ma dodatkowe punktu końcowego, który konstruuje hello adres url punktu końcowego struktury swagger, wyszukuje hello interfejsu i zwraca domyślny użytkownik toohello definicji funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2467-122">Stream Analytics has an additional endpoint that constructs hello url for swagger endpoint, looks up hello interface and returns a default UDF definition toohello user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="f2467-123">Konfigurowanie usługi analiza strumienia i funkcji zdefiniowanej przez użytkownika za pomocą interfejsu API REST uczenia maszynowego</span><span class="sxs-lookup"><span data-stu-id="f2467-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="f2467-124">Za pomocą interfejsów API REST można skonfigurować usługi Azure Machine języka toocall zadania.</span><span class="sxs-lookup"><span data-stu-id="f2467-124">By using REST APIs you may configure your job toocall Azure Machine Language functions.</span></span> <span data-ttu-id="f2467-125">Witaj obejmuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f2467-125">hello steps are as follows:</span></span>

1. <span data-ttu-id="f2467-126">Tworzenie zadania usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f2467-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="f2467-127">Zdefiniuj dane wejściowe</span><span class="sxs-lookup"><span data-stu-id="f2467-127">Define an input</span></span>
3. <span data-ttu-id="f2467-128">Definiowanie danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="f2467-128">Define an output</span></span>
4. <span data-ttu-id="f2467-129">Tworzenie funkcji zdefiniowanej przez użytkownika (UDF)</span><span class="sxs-lookup"><span data-stu-id="f2467-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="f2467-130">Zapisu transformację Stream Analytics, że wywołania hello funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="f2467-130">Write a Stream Analytics transformation that calls hello UDF</span></span>
6. <span data-ttu-id="f2467-131">Uruchom zadanie hello</span><span class="sxs-lookup"><span data-stu-id="f2467-131">Start hello job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="f2467-132">Tworzenie funkcji zdefiniowanej przez użytkownika za pomocą właściwości podstawowe</span><span class="sxs-lookup"><span data-stu-id="f2467-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="f2467-133">Na przykład powitania po przykładowy kod tworzy skalarne funkcji zdefiniowanej przez użytkownika o nazwie *newudf* który wiąże tooan końcowego uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="f2467-133">As an example, hello following sample code creates a scalar UDF named *newudf* that binds tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="f2467-134">Należy pamiętać, że hello *punktu końcowego* (identyfikator URI usługi) można znaleźć na stronie pomocy hello interfejsu API hello wybrane usługi i hello *apiKey* można znaleźć na stronie głównej usług hello.</span><span class="sxs-lookup"><span data-stu-id="f2467-134">Note that hello *endpoint* (service URI) can be found on hello API help page for hello chosen service and hello *apiKey* can be found on hello Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="f2467-135">Przykład treści żądania:</span><span class="sxs-lookup"><span data-stu-id="f2467-135">Example request body:</span></span>  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="f2467-136">Punkt końcowy RetrieveDefaultDefinition wywołanie domyślnego funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="f2467-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="f2467-137">Raz hello szkielet funkcji zdefiniowanej przez użytkownika jest tworzona hello pełnej definicji hello funkcji zdefiniowanej przez użytkownika jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="f2467-137">Once hello skeleton UDF is created hello complete definition of hello UDF is needed.</span></span> <span data-ttu-id="f2467-138">punkt końcowy RetreiveDefaultDefinition Hello ułatwia rozpoczęcie hello definicji domyślnej dla funkcji skalarnych jest powiązane tooan końcowego uczenia maszynowego Azure.</span><span class="sxs-lookup"><span data-stu-id="f2467-138">hello RetreiveDefaultDefinition endpoint helps you get hello default definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="f2467-139">ładunek Hello poniżej wymaga definicji UDF domyślnej hello tooget dla funkcji skalarnych jest punkt końcowy usługi Azure Machine Learning tooan powiązane.</span><span class="sxs-lookup"><span data-stu-id="f2467-139">hello payload below requires you tooget hello default UDF definition for a scalar function that is bound tooan Azure Machine Learning endpoint.</span></span> <span data-ttu-id="f2467-140">Nie go określić hello rzeczywisty punkt końcowy, ponieważ już podano podczas żądania PUT.</span><span class="sxs-lookup"><span data-stu-id="f2467-140">It doesn’t specify hello actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="f2467-141">Analiza strumienia wywołuje punkt końcowy hello podany w żądaniu hello, jeśli podano jawnie.</span><span class="sxs-lookup"><span data-stu-id="f2467-141">Stream Analytics calls hello endpoint provided in hello request if it is provided explicitly.</span></span> <span data-ttu-id="f2467-142">W przeciwnym razie używa hello jedną oryginalnie odwołuje się do.</span><span class="sxs-lookup"><span data-stu-id="f2467-142">Otherwise it uses hello one originally referenced.</span></span> <span data-ttu-id="f2467-143">W tym miejscu hello ciągu pojedynczy parametr (zdania) i zwraca jedną output typu String, co oznacza etykietę "wskaźniki nastrojów klientów" hello zdanie to przyjmuje funkcji zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="f2467-143">Here hello UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates hello “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="f2467-144">Przykład treści żądania:</span><span class="sxs-lookup"><span data-stu-id="f2467-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="f2467-145">Przykładowe dane wyjściowe tego poszukać coś chcieliby poniżej.</span><span class="sxs-lookup"><span data-stu-id="f2467-145">A sample output of this would look something like below.</span></span>  

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

## <a name="patch-udf-with-hello-response"></a><span data-ttu-id="f2467-146">Poprawka UDF hello odpowiedzi</span><span class="sxs-lookup"><span data-stu-id="f2467-146">Patch UDF with hello response</span></span>
<span data-ttu-id="f2467-147">Teraz hello funkcji zdefiniowanej przez użytkownika musi być poprawiono z poprzedniej odpowiedzi hello, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="f2467-147">Now hello UDF must be patched with hello previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="f2467-148">Treść żądania (dane wyjściowe z RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="f2467-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

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

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a><span data-ttu-id="f2467-149">Wdrożenie usługi analiza strumienia transformacji toocall hello funkcji zdefiniowanej przez użytkownika</span><span class="sxs-lookup"><span data-stu-id="f2467-149">Implement Stream Analytics transformation toocall hello UDF</span></span>
<span data-ttu-id="f2467-150">Teraz zapytanie hello funkcji zdefiniowanej przez użytkownika (w tym miejscu o nazwie scoreTweet) dla każdego zdarzenia wejściowe i zapisu odpowiedzi na te dane wyjściowe tooan zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="f2467-150">Now query hello UDF (here named scoreTweet) for every input event and write a response for that event tooan output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="f2467-151">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="f2467-151">Get help</span></span>
<span data-ttu-id="f2467-152">Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f2467-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2467-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2467-153">Next steps</span></span>
* [<span data-ttu-id="f2467-154">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="f2467-154">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f2467-155">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f2467-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f2467-156">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f2467-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f2467-157">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f2467-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f2467-158">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f2467-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
