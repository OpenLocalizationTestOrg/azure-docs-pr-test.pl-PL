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
# <a name="machine-learning-integration-in-stream-analytics"></a>Maszyny Learning integracji usługi analiza strumienia
Analiza strumienia obsługuje funkcji zdefiniowanych przez użytkownika, które wywołują się punkty końcowe usługi Machine Learning tooAzure. Obsługa interfejsu API REST dla tej funkcji została szczegółowo opisana na powitania [biblioteki interfejsu API REST usługi analiza strumienia](https://msdn.microsoft.com/library/azure/dn835031.aspx). Ten artykuł zawiera dodatkowe informacje potrzebne do pomyślnego wykonania tej funkcji w Stream Analytics. Samouczek również została opublikowana i jest dostępny [tutaj](stream-analytics-machine-learning-integration-tutorial.md).

## <a name="overview-azure-machine-learning-terminology"></a>Omówienie: Usługa Azure Machine Learning terminologia
Microsoft Azure Machine Learning zapewnia narzędzia współpracy, przeciągnij i upuść, można użyć toobuild, testowania i wdrażania rozwiązań analizy predykcyjnej na podstawie danych. To narzędzie jest nazywany hello *Azure Machine Learning Studio*. Hello studio jest używany toointeract z hello zasobów uczenia maszynowego i łatwe tworzenie, testowanie i wykonywanie kolejnych iteracji projektu. Poniżej są tych zasobów i ich definicje.

* **Obszar roboczy**: hello *obszaru roboczego* jest kontenerem, który zawiera inne zasoby usługi Machine Learning razem w kontenerze zarządzania i kontroli.
* **Eksperymentu**: *eksperymenty* zostały utworzone przy użyciu zestawów danych służące tooutilize danych oraz uczenia modelu uczenia maszynowego.
* **Punkt końcowy**: *punkty końcowe* hello Azure Machine Learning funkcji tootake obiekt używany jako dane wejściowe, zastosuj modelu uczenia maszynowego określonego i zwraca scored danych wyjściowych.
* **Ocenianie usługi sieci Web**: A *oceniania webservice* jest kolekcją punktów końcowych, jak wspomniano powyżej.

Każdy punkt końcowy ma interfejsów API dla wykonywania wsadowego i wykonywania synchronicznego. Analiza strumienia używa synchronicznej. nosi nazwę określonej usługi Hello [żądania/odpowiedzi usługi](../machine-learning/machine-learning-consume-web-services.md) w studio uczenie maszynowe Azure.

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a>Zasobów niezbędnych do zadania usługi analiza strumienia uczenia maszynowego
Hello celów usługi analiza strumienia zadania przetwarzania punktu końcowego żądanie/odpowiedź [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md), i definicji struktury swagger są wszystkie niezbędne do pomyślnego wykonania. Analiza strumienia ma dodatkowe punktu końcowego, który konstruuje hello adres url punktu końcowego struktury swagger, wyszukuje hello interfejsu i zwraca domyślny użytkownik toohello definicji funkcji zdefiniowanej przez użytkownika.

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a>Konfigurowanie usługi analiza strumienia i funkcji zdefiniowanej przez użytkownika za pomocą interfejsu API REST uczenia maszynowego
Za pomocą interfejsów API REST można skonfigurować usługi Azure Machine języka toocall zadania. Witaj obejmuje następujące czynności:

1. Tworzenie zadania usługi Stream Analytics
2. Zdefiniuj dane wejściowe
3. Definiowanie danych wyjściowych
4. Tworzenie funkcji zdefiniowanej przez użytkownika (UDF)
5. Zapisu transformację Stream Analytics, że wywołania hello funkcji zdefiniowanej przez użytkownika
6. Uruchom zadanie hello

## <a name="creating-a-udf-with-basic-properties"></a>Tworzenie funkcji zdefiniowanej przez użytkownika za pomocą właściwości podstawowe
Na przykład powitania po przykładowy kod tworzy skalarne funkcji zdefiniowanej przez użytkownika o nazwie *newudf* który wiąże tooan końcowego uczenia maszynowego Azure. Należy pamiętać, że hello *punktu końcowego* (identyfikator URI usługi) można znaleźć na stronie pomocy hello interfejsu API hello wybrane usługi i hello *apiKey* można znaleźć na stronie głównej usług hello.

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

Przykład treści żądania:  

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

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a>Punkt końcowy RetrieveDefaultDefinition wywołanie domyślnego funkcji zdefiniowanej przez użytkownika
Raz hello szkielet funkcji zdefiniowanej przez użytkownika jest tworzona hello pełnej definicji hello funkcji zdefiniowanej przez użytkownika jest wymagana. punkt końcowy RetreiveDefaultDefinition Hello ułatwia rozpoczęcie hello definicji domyślnej dla funkcji skalarnych jest powiązane tooan końcowego uczenia maszynowego Azure. ładunek Hello poniżej wymaga definicji UDF domyślnej hello tooget dla funkcji skalarnych jest punkt końcowy usługi Azure Machine Learning tooan powiązane. Nie go określić hello rzeczywisty punkt końcowy, ponieważ już podano podczas żądania PUT. Analiza strumienia wywołuje punkt końcowy hello podany w żądaniu hello, jeśli podano jawnie. W przeciwnym razie używa hello jedną oryginalnie odwołuje się do. W tym miejscu hello ciągu pojedynczy parametr (zdania) i zwraca jedną output typu String, co oznacza etykietę "wskaźniki nastrojów klientów" hello zdanie to przyjmuje funkcji zdefiniowanej przez użytkownika.

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

Przykład treści żądania:  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

Przykładowe dane wyjściowe tego poszukać coś chcieliby poniżej.  

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

## <a name="patch-udf-with-hello-response"></a>Poprawka UDF hello odpowiedzi
Teraz hello funkcji zdefiniowanej przez użytkownika musi być poprawiono z poprzedniej odpowiedzi hello, jak pokazano poniżej.

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

Treść żądania (dane wyjściowe z RetrieveDefaultDefinition):

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

## <a name="implement-stream-analytics-transformation-toocall-hello-udf"></a>Wdrożenie usługi analiza strumienia transformacji toocall hello funkcji zdefiniowanej przez użytkownika
Teraz zapytanie hello funkcji zdefiniowanej przez użytkownika (w tym miejscu o nazwie scoreTweet) dla każdego zdarzenia wejściowe i zapisu odpowiedzi na te dane wyjściowe tooan zdarzeń.  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a>Uzyskiwanie pomocy
Aby uzyskać dalszą pomoc, skorzystaj z naszego [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)
