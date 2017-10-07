---
title: "potoki danych predykcyjnej aaaCreate przy użyciu fabryki danych Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate utworzyć predykcyjnej potoki przy użyciu fabryki danych Azure i usługi Azure Machine Learning"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 943210c28b1696e299ff9b7cc96369b95f182354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a>Tworzenie potoków predykcyjnej przy użyciu usługi Azure Machine Learning i fabryki danych Azure

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Działanie gałęzi](data-factory-hive-activity.md) 
> * [Działanie pig](data-factory-pig-activity.md)
> * [Działania MapReduce](data-factory-map-reduce.md)
> * [Działaniu przesyłania strumieniowego usługi Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Działanie Spark](data-factory-spark.md)
> * [Działanie wykonywania wsadowego w usłudze Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Działania aktualizowania zasobów w usłudze Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Działania procedur składowanych](data-factory-stored-proc-activity.md)
> * [Działania języka U-SQL usługi Data Lake Analytics](data-factory-usql-activity.md)
> * [Działania niestandardowe .NET](data-factory-use-custom-activities.md)

## <a name="introduction"></a>Wprowadzenie

### <a name="azure-machine-learning"></a>Azure Machine Learning
[Usługa Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) umożliwia toobuild możesz, testowania i wdrażania rozwiązań analizy predykcyjnej. Z wysokiego poziomu punktu widzenia można to zrobić w trzy kroki:

1. **Tworzenie eksperymentu uczenia**. W tym kroku są wykonywane przy użyciu hello Azure ML Studio. Witaj ML studio to środowisko visual programowanie zespołowe używanie tootrain i testowanie modelu analizy predykcyjnej przy użyciu danych szkoleniowych.
2. **Przekonwertuj go eksperyment predykcyjny tooa**. Po modelu po zapoznaniu z istniejącymi danymi i są gotowe toouse go tooscore nowe dane, Przygotuj i usprawnić eksperymentu wyników.
3. **Go wdrożyć jako usługę sieci web**. Możesz opublikować oceniania eksperymentu jako usługi sieci web platformy Azure. Można wysyłać modelu tooyour danych za pomocą tego punktu końcowego usługi sieci web i odbierać prognoz wyniku z modelu hello.  

### <a name="azure-data-factory"></a>Azure Data Factory
Fabryka danych jest usługa integracji danych opartych na chmurze, która organizuje i zautomatyzować hello **przepływu** i **przekształcania** danych. Można utworzyć integracji danych rozwiązania przy użyciu fabryki danych Azure, które można pozyskiwania danych z różnych baz danych, proces/transformacji danych hello i publikowanie magazyny danych toohello hello wynik danych.

Usługi fabryka danych pozwala toocreate potoki danych, które Przenieś i przekształcania danych, a następnie uruchom potoki hello zgodnie z zaplanowanym harmonogramem (co godzinę, codziennie, co tydzień, itp.). Ponadto zapewnia elementy powiązane hello toodisplay zaawansowane wizualizacje i zależności między Twojej potoki danych i monitorowania sieci potoki danych z problemów znaleźć tooeasily pojedynczego ujednoliconego podglądu, a ustawienia alertów monitorowania.

Zobacz [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) i [kompilacji swój pierwszy potok](data-factory-build-your-first-pipeline.md) tooquickly artykuły wprowadzenie hello usługi fabryka danych Azure.

### <a name="data-factory-and-machine-learning-together"></a>Fabryki danych i jednocześnie uczenia maszynowego
Azure umożliwia fabryki danych tooeasily możesz utworzyć potoki, które używają opublikowanych [usługi Azure Machine Learning] [ azure-machine-learning] usługi analizy predykcyjnej sieci web. Przy użyciu hello **działanie wykonywania wsadowego** w potoku fabryki danych Azure, można wywołać usługi Azure ML web toomake operacje przewidywania dla usługi na powitania danych w partii. Zobacz [uczenie Maszynowe Azure wywoływania usługi sieci web przy użyciu hello działanie wykonywania wsadowego](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) sekcji, aby uzyskać szczegółowe informacje.

Wraz z upływem czasu hello modeli predykcyjnych w eksperymentach oceniania uczenia Maszynowego Azure hello muszą toobe retrained przy użyciu nowych baz danych wejściowych. Model usługi uczenie Maszynowe Azure z potoku fabryki danych można ponownie ucz, wykonując następujące kroki hello:

1. Opublikuj eksperyment uczenia hello (eksperyment predykcyjny nie) jako usługę sieci web. Należy wykonać ten krok w hello Azure ML Studio, tak jak tooexpose eksperyment predykcyjny jako usługę sieci web w poprzednim scenariuszu hello.
2. Użyj hello działanie wykonywania wsadowego usługi Azure ML tooinvoke hello usługę sieci web eksperyment uczenia hello. Zasadniczo można użyć hello tooinvoke działanie wykonywania wsadowego usługi uczenie Maszynowe Azure zarówno uczenie usługi sieci web i oceniania usługi sieci web.

Po wykonaniu ponownego trenowania zaktualizuj hello oceniania usługi sieci web (eksperyment predykcyjny udostępniony jako usługa sieci web) z hello nowo uczonego modelu przy użyciu hello **działanie aktualizacji zasobu usługi Azure ML**. Zobacz [aktualizowanie modeli przy użyciu działanie aktualizacji zasobu](data-factory-azure-ml-update-resource-activity.md) artykułu, aby uzyskać szczegółowe informacje.

## <a name="invoking-a-web-service-using-batch-execution-activity"></a>Wywoływanie usługi sieci web przy użyciu działanie wykonywania wsadowego
Przenoszenie danych tooorchestrate fabryki danych Azure i przetwarzania, a następnie wykonaj wykonywania wsadowego usługi za pomocą usługi Azure Machine Learning. Poniżej przedstawiono kroki najwyższego poziomu hello:

1. Tworzenie usługi Azure Machine Learning połączone. Należy hello następujące wartości:

   1. **Identyfikator URI żądania** dla hello API wykonywania wsadowego. Hello przez identyfikator URI żądania można znaleźć, klikając hello **BATCH EXECUTION** łącze na stronie usługi sieci web hello.
   2. **Klucz interfejsu API** dla hello opublikowane usługi sieci web uczenie maszynowe Azure. Klucz interfejsu API hello można znaleźć, klikając hello usługi sieci web, które zostały opublikowane.
   3. Użyj hello **AzureMLBatchExecution** działania.

      ![Pulpit nawigacyjny uczenia maszynowego](./media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Identyfikator URI partii](./media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-toodata-in-azure-blob-storage"></a>Scenariusz: Eksperymentów przy użyciu sieci Web usługi wejść/wyjść odwołujące się toodata w magazynie obiektów Blob Azure
W tym scenariuszu hello usługi sieci Web Azure Machine Learning sprawia, że prognoz przy użyciu danych z pliku w magazynie obiektów blob platformy Azure i przechowuje wyniki prognozowania hello w magazynie obiektów blob hello. Witaj następujące JSON definiuje potoku fabryki danych do działania AzureMLBatchExecution. działanie Hello ma hello dataset **DecisionTreeInputBlob** jako dane wejściowe i **DecisionTreeResultBlob** jako dane wyjściowe hello. Witaj **DecisionTreeInputBlob** jest przekazywany jako usługi sieci web toohello wejściowych przez przy użyciu hello **WebServiceInputActivity** właściwości JSON. Witaj **DecisionTreeResultBlob** jest przekazywany jako usługi sieci Web dane wyjściowe toohello przez przy użyciu hello **webServiceOutputs** właściwości JSON.  

> [!IMPORTANT]
> Jeśli usługa sieci web hello przyjmuje wielu danych wejściowych, użyj hello **webServiceInputs** zamiast za pomocą właściwości **WebServiceInputActivity**. Zobacz hello [usługi sieci Web wymaga wielu nakładów](#web-service-requires-multiple-inputs) sekcji, na przykład za pomocą właściwości webServiceInputs hello.
>
> Zestawy danych, które odwołują się hello **WebServiceInputActivity**/**webServiceInputs** i **webServiceOutputs** właściwości (w  **typeProperties**) również muszą być zawarte w hello działania **dane wejściowe** i **generuje**.
>
> W eksperymencie uczenie Maszynowe Azure wprowadzania usługi sieci web i porty wyjścia i parametry globalne mają nazwy domyślnej ("input1", "input2"), które można dostosować. nazwy Hello, używane w przypadku webServiceInputs, webServiceOutputs i ustawienia globalParameters musi dokładnie odpowiadać hello nazw hello eksperymenty. Ładunek żądania próbki hello można wyświetlić na stronie pomocy wykonywania wsadowego hello mapowanie hello oczekiwano tooverify punktu końcowego uczenia Maszynowego Azure.
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> Tylko wejściami i wyjściami hello AzureMLBatchExecution działania mogą być przekazywane jako parametry toohello usługi sieci Web. Na przykład hello powyżej fragment kodu JSON, DecisionTreeInputBlob jest wejściowych toohello AzureMLBatchExecution działalność, która jest przekazywany jako wejściowych toohello usługi sieci Web za pomocą parametru WebServiceInputActivity.   
>
>

### <a name="example"></a>Przykład
Ten przykład używa usługi Azure Storage toohold zarówno hello danych wejściowych i wyjściowych.

Firma Microsoft zaleca zapoznanie hello [kompilacji swój pierwszy potok z fabryką danych] [ adf-build-1st-pipeline] samouczka przed rozpoczęciem tego przykładu. W tym przykładzie, należy użyć hello Edytor fabryki danych toocreate fabryki danych artefakty (połączone usługi, zestawy danych, potoku).   

1. Utwórz **połączona usługa** dla Twojego **usługi Azure Storage**. Witaj plików wejściowych i wyjściowych znajdują się w różnych kont magazynu, należy najpierw dwóch połączonych usług. Oto przykład JSON:

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. Utwórz hello **wejściowych** fabryki danych Azure **zestawu danych**. W odróżnieniu od niektórych innych fabryki danych zestawów danych, te zestawy danych musi zawierać zarówno **folderPath** i **fileName** wartości. Można użyć partycjonowania toocause każdej partii tooprocess wykonywania (każdy wycinek danych) lub utworzyć unikatowe dane wejściowe i plików wyjściowych. Może być konieczne tooinclude hello tootransform niektóre działania nadrzędnego danych wejściowych w formacie pliku CSV hello i umieścić go w hello konta magazynu dla każdego wycinka. W takim przypadku nie obejmuje hello **zewnętrznych** i **externalData** ustawienia w powitania po przykład oraz DecisionTreeInputBlob Twojego będą hello wyjściowy zestaw danych z innego działania.

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    Plik wejściowy csv musi mieć wiersz nagłówka kolumny hello. Jeśli używasz hello **działanie kopiowania** toocreate/przeniesienia hello csv do magazynu obiektów blob hello, należy ustawić właściwość obiektu sink hello **blobWriterAddHeader** za**true**. Na przykład:

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    Jeśli plik csv hello nie ma wiersz nagłówka hello, mogą pojawić się hello następujący błąd: **błąd w działaniu: Wystąpił błąd podczas odczytywania ciągu. Nieoczekiwany token: metodzie StartObject. Ścieżka ', wiersz 1, umieść 1**.
3. Utwórz hello **dane wyjściowe** fabryki danych Azure **zestawu danych**. W tym przykładzie użyto partycjonowania toocreate ścieżka wyjściowa unikatowy dla każdego wykonania wycinka. Bez hello partycje, działanie hello zastąpiłaby hello pliku.

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. Utwórz **połączona usługa** typu: **AzureMLLinkedService**, zapewniając klucza hello interfejsu API i modelu adres URL wykonywania wsadowego.

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. Na koniec tworzenie potoku nadrzędnym **AzureMLBatchExecution** działania. W czasie wykonywania potoku wykonuje hello następujące kroki:

   1. Pobiera lokalizację pliku wejściowego hello hello z zestawów danych wejściowych.
   2. Wywołuje wykonywania wsadowego usługi uczenie maszynowe Azure hello interfejsu API
   3. Kopie hello wykonanie partii danych wyjściowych toohello blob podane w zestawie danych wyjściowych.

      > [!NOTE]
      > Działanie AzureMLBatchExecution może mieć zero lub więcej wejściami i wyjściami jeden lub więcej.
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      Zarówno **start** i **zakończenia** dat i godzin musi być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Na przykład: 2014-10-14T16:32:41Z. Witaj **zakończenia** czasu jest opcjonalna. Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin.**" potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości. Szczegółowe informacje dotyczące właściwości kodu JSON znajdują się w artykule [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) (Dokumentacja dotycząca skryptów JSON).

      > [!NOTE]
      > Określenie danych wejściowych dla działania AzureMLBatchExecution hello jest opcjonalne.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-toorefer-toodata-in-various-storages"></a>Scenariusz: Eksperymentów przy użyciu modułów odczytywania/zapisywania toorefer toodata w różnych miejsc
Inny typowy scenariusz, podczas tworzenia eksperymenty uczenie Maszynowe Azure jest toouse składników zapisywania i odczytywania modułów. Moduł czytnika Hello jest tooload używane dane do eksperymentu, a moduł zapisywania hello jest toosave danych z eksperymentów. Szczegółowe informacje na temat składników zapisywania i odczytywania modułów, zobacz [czytnika](https://msdn.microsoft.com/library/azure/dn905997.aspx) i [zapisywania](https://msdn.microsoft.com/library/azure/dn905984.aspx) tematy w bibliotece MSDN.     

Korzystając z hello składników zapisywania i odczytywania modułów, jest dobrym rozwiązaniem toouse parametr usługi sieci Web dla każdej właściwości w tych modułów odczytywania/zapisywania. Te parametry sieci web umożliwiają tooconfigure hello wartości w czasie wykonywania. Na przykład można utworzyć eksperyment przy użyciu modułu reader używa usługi Azure SQL Database: XXX.database.windows.net. Po wdrożeniu usługi sieci web hello ma konsumentów hello tooenable toospecify usługi sieci web hello o nazwie YYY.database.windows.net innego serwera SQL Azure. Tooallow parametr usługi sieci Web można użyć tego toobe wartość skonfigurowana.

> [!NOTE]
> Usługi sieci Web w danych wejściowych i wyjściowych różnią się od parametry usługi sieci Web. Pierwszy scenariusz hello już wspomniano, jak dane wejściowe i wyjściowe można określić dla usługi sieci Web uczenie Maszynowe Azure. W tym scenariuszu należy przekazać parametry usługi sieci Web, które odpowiadają tooproperties odczytywania/zapisywania modułów.
>
>

Przyjrzyjmy się scenariusz użycia parametry usługi sieci Web. Masz wdrożonej usługi sieci web uczenie maszynowe Azure używającej tooread moduł czytnika danych z jednego źródła danych hello obsługiwane przez usługi Azure Machine Learning (na przykład: baza danych SQL Azure). Po wykonaniu hello wsadowe hello wyniki są zapisywane za pomocą modułu zapisywania (baza danych SQL Azure).  Nie sieci web usługi wejściami i wyjściami są definiowane w hello eksperymentów. W takim przypadku firma Microsoft zaleca, aby skonfigurować parametry usługi sieci web odpowiednich hello składników zapisywania i odczytywania modułów. Taka konfiguracja pozwala hello odczytywania/zapisywania skonfigurowane podczas używania działania AzureMLBatchExecution hello toobe modułów. Określ parametry usługi sieci Web w hello **globalParameters** sekcji w działaniu hello JSON w następujący sposób.

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

Można również użyć [funkcji fabryki danych](data-factory-functions-variables.md) do przekazywania wartości hello parametry usługi sieci Web, jak pokazano w hello poniższy przykład:

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Parametry usługi sieci Web Hello jest rozróżniana wielkość liter, dlatego upewnij się, czy nazwy hello, które określisz w działaniu hello JSON pasują hello te udostępniane przez hello usługi sieci Web.
>
>

### <a name="using-a-reader-module-tooread-data-from-multiple-files-in-azure-blob"></a>Przy użyciu tooread moduł czytnika danych z wielu plików w obiekcie Blob Azure
Dane big data potoków z działania, takie jak Pig i Hive można utworzyć jeden lub więcej plików wyjściowych bez rozszerzeń. Na przykład po określeniu tabelę zewnętrzną Hive hello danych dla tabeli zewnętrznej Hive hello można przechowywane w magazynu obiektów blob platformy Azure z powitania po 000000_0 nazwy. Moduł czytnika hello w tooread eksperymentu korzystanie z wielu plików i używać ich na potrzeby prognoz.

Korzystając z hello czytnika modułu w eksperymencie usługi Azure Machine Learning, obiektów Blob platformy Azure można określić jako dane wejściowe. pliki Hello w hello magazynu obiektów blob platformy Azure mogą być pliki wyjściowe hello (przykład: 000000_0) który są produkowane przez Pig i Hive skryptu uruchomionego w usłudze HDInsight. Witaj moduł czytnika pozwala tooread plików (nie rozszerzenia) przez skonfigurowanie hello **toocontainer ścieżki, w katalogu/obiektów blob**. Hello **toocontainer ścieżki** punktów toohello kontenera i **katalogu/obiektów blob** punktów toofolder zawierający pliki hello, jak pokazano w powitania po obrazu. Hello gwiazdka oznacza to, \*) **Określa, że hello wszystkie pliki w hello kontenera lub folder (oznacza to, aggregateddata/rocznie danych = miesiąc-2014-6 /\*)** są odczytywane w ramach eksperymentu hello.

![Właściwości obiektów Blob platformy Azure](./media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a>Przykład
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a>W potoku z działania AzureMLBatchExecution o parametry usługi sieci Web

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

W hello powyżej przykład JSON:

* Azure Machine Learning w sieci Web usługi używa czytnika i zapisywania danych tooread/zapisu dla modułu z wdrożonych Hello / tooan bazy danych SQL Azure. Ta usługa sieci Web udostępnia następujące cztery parametry hello: Nazwa serwera, nazwa bazy danych, nazwę konta użytkownika serwera i hasło konta użytkownika serwera bazy danych.  
* Zarówno **start** i **zakończenia** dat i godzin musi być w [formacie ISO](http://en.wikipedia.org/wiki/ISO_8601). Na przykład: 2014-10-14T16:32:41Z. Witaj **zakończenia** czasu jest opcjonalna. Jeśli nie określisz wartości hello **zakończenia** właściwości, jest on obliczany jako "**start + 48 godzin.**" potok hello toorun przez czas nieokreślony, określ **9999-09-09** jako wartość hello hello **zakończenia** właściwości. Szczegółowe informacje dotyczące właściwości kodu JSON znajdują się w artykule [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) (Dokumentacja dotycząca skryptów JSON).

### <a name="other-scenarios"></a>Inne scenariusze
#### <a name="web-service-requires-multiple-inputs"></a>Usługa sieci Web wymaga wielu danych wejściowych
Jeśli usługa sieci web hello przyjmuje wielu danych wejściowych, użyj hello **webServiceInputs** zamiast za pomocą właściwości **WebServiceInputActivity**. Zestawy danych, które odwołują się hello **webServiceInputs** również muszą być zawarte w hello działania **dane wejściowe**.

W eksperymencie uczenie Maszynowe Azure wprowadzania usługi sieci web i porty wyjścia i parametry globalne mają nazwy domyślnej ("input1", "input2"), które można dostosować. nazwy Hello, używane w przypadku webServiceInputs, webServiceOutputs i ustawienia globalParameters musi dokładnie odpowiadać hello nazw hello eksperymenty. Ładunek żądania próbki hello można wyświetlić na stronie pomocy wykonywania wsadowego hello mapowanie hello oczekiwano tooverify punktu końcowego uczenia Maszynowego Azure.

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a>Usługa sieci Web nie wymaga danych wejściowych
Azure ML wsadowe wykonywanie usług sieci web może być używane toorun przepływów pracy, na przykład R lub Python skrypty, które nie mogą wymagać wszystkie dane wejściowe. Lub eksperymentu hello mogą być skonfigurowane przy użyciu modułu nie ujawnia żadnych GlobalParameters czytniku. W takim przypadku hello AzureMLBatchExecution działania zostanie skonfigurowany w następujący sposób:

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a>Usługa sieci Web nie wymaga danych wejściowych/wyjściowych
Witaj usługi sieci web wykonywania wsadowego uczenie Maszynowe Azure może nie mieć żadnych danych wyjściowych z usługą sieci Web skonfigurowana. W tym przykładzie nie istnieje usługi sieci Web w danych wejściowych lub wyjściowych, ani nie skonfigurowano żadnych GlobalParameters. Nadal jest wyjściem skonfigurowane w działaniu hello, się, ale nie zostanie podany jako webServiceOutput.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-hello-activity-runs-only-when-other-activities-have-succeeded"></a>Czytników używa usługi sieci Web i zapisywania i hello działania działa tylko wtedy, gdy inne działania zakończyło się pomyślnie
Hello Azure ML web składników zapisywania i odczytywania modułów usługi może być skonfigurowany toorun z lub bez żadnych GlobalParameters. Można jednak, że usługa tooembed wywołuje w potoku, która używa usługi hello tooinvoke zależności zestawu danych tylko wtedy, gdy niektóre nadrzędnego przetwarzanie zostało zakończone. Po zakończeniu wykonywania wsadowego usługi hello przy użyciu tej metody, można również uruchomić innych działań. W takim przypadku można wyrazić hello zależności za pomocą działania wejściach i wyjściach, bez nazw ich jako usługi sieci Web wejściowych i wyjściowych.

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

Witaj **takeaways** są:

* Jeśli punkt końcowy eksperyment używa WebServiceInputActivity: jest reprezentowana przez zestaw danych obiektów blob i znajduje się w danych wejściowych działania hello i hello WebServiceInputActivity właściwość. W przeciwnym razie hello WebServiceInputActivity właściwość została pominięta.
* Jeśli punkt końcowy eksperyment używa webServiceOutput(s): są reprezentowane przez zestawy danych obiektów blob i zawarte w danych wyjściowych działania hello oraz we właściwości webServiceOutputs hello. generuje Hello działania i webServiceOutputs są mapowane według nazwy hello każdego danych wyjściowych w eksperymencie hello. W przeciwnym razie wartość właściwości webServiceOutputs hello jest pomijany.
* Jeśli punkt końcowy eksperyment przedstawia globalParameter(s), otrzymują one we właściwości globalParameters działania hello jako pary kluczy, wartość. W przeciwnym razie wartość właściwości globalParameters hello jest pomijany. Witaj kluczy jest rozróżniana wielkość liter. [Funkcje fabryki danych Azure](data-factory-functions-variables.md) mogą być używane w hello wartości.
* Dodatkowe zestawy danych może być zawarta w właściwości wejściami i wyjściami hello działania, bez przywoływane w hello typeProperties działania. Te zestawy danych będą zarządzały sposobem wykonania przy użyciu zależności wycinka, ale w przeciwnym razie są ignorowane przez hello AzureMLBatchExecution działania.


## <a name="updating-models-using-update-resource-activity"></a>Aktualizowanie modeli przy użyciu działanie aktualizacji zasobu
Po wykonaniu ponownego trenowania zaktualizuj hello oceniania usługi sieci web (eksperyment predykcyjny udostępniony jako usługa sieci web) z hello nowo uczonego modelu przy użyciu hello **działanie aktualizacji zasobu usługi Azure ML**. Zobacz [aktualizowanie modeli przy użyciu działanie aktualizacji zasobu](data-factory-azure-ml-update-resource-activity.md) artykułu, aby uzyskać szczegółowe informacje.

### <a name="reader-and-writer-modules"></a>Czytnik i modułów zapisywania
Typowy scenariusz użycia parametrów usługi sieci Web jest używanie hello czytników SQL Azure i zapisywania. Moduł czytnika Hello jest tooload używane dane do eksperymentu z usług zarządzania danych poza Azure Machine Learning Studio. Moduł zapisywania Hello jest toosave danych z eksperymentów do usługi zarządzania danych poza Azure Machine Learning Studio.  

Aby uzyskać więcej informacji o SQL Azure/obiektów Blob Azure odczytywania/zapisywania, zobacz [czytnika](https://msdn.microsoft.com/library/azure/dn905997.aspx) i [zapisywania](https://msdn.microsoft.com/library/azure/dn905984.aspx) tematy w bibliotece MSDN. przykład Witaj w poprzedniej sekcji hello używane hello obiektów Blob platformy Azure i zapisu obiektów Blob platformy Azure. W tej sekcji omówiono przy użyciu czytnik Azure SQL i składnika zapisywania usługi Azure SQL.

## <a name="frequently-asked-questions"></a>Często zadawane pytania
**Pytanie:** mam wiele plików, które są generowane przez mój potoki danych big data. Toowork działania AzureMLBatchExecution hello można używać we wszystkich plikach hello?

**Odpowiedź:** tak. Zobacz hello **przy użyciu tooread moduł czytnika danych z wielu plików w obiekcie Blob Azure** sekcji, aby uzyskać szczegółowe informacje.

## <a name="azure-ml-batch-scoring-activity"></a>Działanie oceniania partii zadań Azure ML
Jeśli używasz hello **AzureMLBatchScoring** toointegrate działania przy użyciu usługi Azure Machine Learning, firma Microsoft zaleca się używanie hello najnowsza wersja **AzureMLBatchExecution** działania.

Witaj działania AzureMLBatchExecution została wprowadzona w hello sierpnia 2015 wersji zestawu Azure SDK i programu Azure PowerShell.

Jeśli chcesz toocontinue przy użyciu działania AzureMLBatchScoring hello nadal odczytu za pomocą tej sekcji.  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a>Wsadowe ocenianie przez ML działanie Azure przy użyciu usługi Azure Storage dla wejścia/wyjścia

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a>Parametry usługi sieci Web
Dodaj toospecify wartości parametrów usługi sieci Web, **typeProperties** toohello sekcji **AzureMLBatchScoringActivty** sekcji w potoku hello JSON, jak pokazano w hello poniższy przykład:

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
Można również użyć [funkcji fabryki danych](data-factory-functions-variables.md) do przekazywania wartości hello parametry usługi sieci Web, jak pokazano w hello poniższy przykład:

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> Parametry usługi sieci Web Hello jest rozróżniana wielkość liter, dlatego upewnij się, czy nazwy hello, które określisz w działaniu hello JSON pasują hello te udostępniane przez hello usługi sieci Web.
>
>

## <a name="see-also"></a>Zobacz też
* [Azure wpis w blogu: wprowadzenie do fabryki danych Azure i usługi Azure Machine Learning](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/
