---
title: "aaaManagement zestawu .NET SDK dla usługi Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z Stream Analytics Management .NET SDK. Dowiedz się, jak tooset Konfigurowanie i uruchamianie zadania usługi analiza. Utwórz projekt, wejść, wyjść i przekształcenia."
keywords: .NET SDK, analizy interfejsu API
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5e93de87-0c6f-4f4b-be98-08d63f832897
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/06/2017
ms.author: jeffstok
ms.openlocfilehash: 507c11938bc5bf2249a2e41f6bcc076db8ead3f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a>Zarządzanie zestawu .NET SDK: Konfigurowanie i uruchamianie zadania usługi analiza dla platformy .NET przy użyciu interfejsu API usługi Azure Stream Analytics hello
Dowiedz się, jak tooset się oraz zadań wykonywania analizy przy użyciu interfejsu API usługi analiza strumienia hello dla platformy .NET przy użyciu zestawu .NET SDK zarządzania hello. Konfigurowanie projektu, Utwórz wejściowymi i wyjściowymi źródeł, transformacji i rozpocząć i zatrzymać zadania. Dla Twojego zadania usługi analiza może przesyłać strumieniowo dane z magazynu obiektów Blob lub Centrum zdarzeń.

Zobacz hello [zarządzania dokumentacji dla hello interfejsu API usługi analiza strumienia dla platformy .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).

Usługa Azure Stream Analytics to w pełni zarządzana usługa dostarczanie przetwarzania małych opóźnieniach, wysokiej dostępności, skalowalności, złożonych zdarzeń za pośrednictwem przesyłania strumieniowego danych w chmurze hello. Analiza strumienia umożliwia tooset klientów w górę przesyłania strumieniowego strumienie danych tooanalyze zadań oraz pozwala toodrive niemal analiz w czasie rzeczywistym.  

> [!NOTE]
> Witaj przykładowy kod w tym artykule zostały zaktualizowane z zestawu .NET SDK usługi Azure Stream Analytics zarządzania v2.x wersją. Przykładowy kod przy użyciu hello użycia wersja zestawu SDK lagecy (1.x), można znaleźć pod adresem [v1.x zestawu .NET SDK zarządzania hello na użytek Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* Zainstaluj program Visual Studio 2017 lub 2015.
* Pobierz i zainstaluj [zestawu Azure .NET SDK](https://azure.microsoft.com/downloads/).
* Utwórz grupy zasobów platformy Azure w ramach subskrypcji. Witaj poniżej znajduje się przykładowy skrypt programu PowerShell systemu Azure. Informacje programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview);  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* Konfigurowanie źródła danych wejściowych i wyjściowych toouse docelowej. Dodatkowe instrukcje można znaleźć [dodać dane wejściowe](stream-analytics-add-inputs.md) tooset się przykładowe dane wejściowe i [dodać danych wyjściowych](stream-analytics-add-outputs.md) tooset się przykładowe dane wyjściowe.

## <a name="set-up-a-project"></a>Konfigurowanie projektu
toocreate zadania usługi Analiza użycia hello interfejsu API usługi analiza strumienia dla platformy .NET, należy najpierw skonfigurować projektu.

1. Utwórz aplikację konsolową programu Visual Studio C# .NET.
2. W konsoli Menedżera pakietów hello hello uruchom następujące polecenia pakietów NuGet hello tooinstall. Witaj najpierw jedna jest hello zestawu .NET SDK usługi Azure Stream Analytics zarządzania. Witaj drugim jest do uwierzytelniania klienta usługi Azure.
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. Dodaj następujące hello **appSettings** pliku App.config toohello sekcji:
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    Zastąp wartości **SubscriptionId** i **ActiveDirectoryTenantId** identyfikatorami z usługi Azure subskrypcji i dzierżawcy. Te wartości można uzyskać, uruchamiając następujące polecenia cmdlet programu Azure PowerShell hello:

        Get-AzureAccount

4. Dodaj następujące odwołania w pliku .csproj hello:

        <Reference Include="System.Configuration" />

5. Dodaj następujące hello **przy użyciu** instrukcje toohello pliku źródłowego (Program.cs) w projekcie hello:
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. Dodaj metodę pomocnika uwierzytelniania:

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a>Tworzenie klienta zarządzania usługi analiza strumienia
A **StreamAnalyticsManagementClient** obiektu umożliwia toomanage hello zadania i hello zadania składniki, takie jak dane wejściowe, dane wyjściowe i przekształcania.

Dodaj następującego kodu toohello początku hello hello **Main** metody:

   ```
    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamingJobName = "<YOUR STREAMING JOB NAME>";
    string inputName = "<YOUR JOB INPUT NAME>";
    string transformationName = "<YOUR JOB TRANSFORMATION NAME>";
    string outputName = "<YOUR JOB OUTPUT NAME>";
    
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    
    // Get credentials
    ServiceClientCredentials credentials = GetCredentials().Result;
    
    // Create Stream Analytics management client
    StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
    {
        SubscriptionId = ConfigurationManager.AppSettings["SubscriptionId"]
    };
   ```

Witaj **resourceGroupName** wartość zmiennej powinna być taka sama jak nazwa hello zasobu hello grupy utworzone lub pobrać wymagane wstępnie kroki hello hello.

tooautomate hello poświadczeń prezentacji aspekt tworzenia zadania, można znaleźć zbyt[uwierzytelniania nazwy głównej usługi z usługą Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Witaj pozostałe sekcje w tym artykule przyjęto, że ten kod zostało początku hello hello **Main** metody.

## <a name="create-a-stream-analytics-job"></a>Tworzenie zadania usługi Stream Analytics
Witaj poniższy kod tworzy zadanie usługi analiza strumienia, w grupie zasobów hello zdefiniowanej przez użytkownika. Zadanie toohello danych wejściowych, wyjściowych i przekształcenie zostaną dodane później.

   ```
   // Create a streaming job
   StreamingJob streamingJob = new StreamingJob()
   {
       Tags = new Dictionary<string, string>()
       {
           { "Origin", ".NET SDK" },
           { "ReasonCreated", "Getting started tutorial" }
       },
       Location = "West US",
       EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
       EventsOutOfOrderMaxDelayInSeconds = 5,
       EventsLateArrivalMaxDelayInSeconds = 16,
       OutputErrorPolicy = OutputErrorPolicy.Drop,
       DataLocale = "en-US",
       CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
       Sku = new Sku()
       {
           Name = SkuName.Standard
       }
   };
   StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
   ```

## <a name="create-a-stream-analytics-input-source"></a>Utwórz źródło danych wejściowych analiza strumienia
Witaj poniższy kod tworzy Stream Analytics źródło danych wejściowych typu źródła danych wejściowych obiektu blob hello i serializacji woluminów CSV. Użyj toocreate źródło wejścia Centrum zdarzeń, **EventHubStreamInputDataSource** zamiast **BlobStreamInputDataSource**. Podobnie można dostosować hello serializacji typu hello źródła danych wejściowych.

   ```
   // Create an input
   StorageAccount storageAccount = new StorageAccount()
   {
       AccountName = "<YOUR STORAGE ACCOUNT NAME>",
       AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
   };
   Input input = new Input()
   {
       Properties = new StreamInputProperties()
       {
           Serialization = new CsvSerialization()
           {
               FieldDelimiter = ",",
               Encoding = Encoding.UTF8
           },
           Datasource = new BlobStreamInputDataSource()
           {
               StorageAccounts = new[] { storageAccount },
               Container = "<YOUR STORAGE BLOB CONTAINER>",
               PathPattern = "{date}/{time}",
               DateFormat = "yyyy/MM/dd",
               TimeFormat = "HH",
               SourcePartitionCount = 16
           }
       }
   };
   Input createInputResult = streamAnalyticsManagementClient.Inputs.CreateOrReplace(input, resourceGroupName, streamingJobName, inputName);
   ```

Źródeł danych wejściowych z magazynu obiektów Blob lub Centrum zdarzeń są wiązanej tooa określonego zadania. toouse hello tego samego źródła danych wejściowych dla różnych zadań, należy wywołać metodę hello ponownie i określenia innej nazwy zadania.

## <a name="test-a-stream-analytics-input-source"></a>Testowanie usługi Stream Analytics źródło danych wejściowych
Witaj **TestConnection** testy metody czy zadanie usługi Stream Analytics hello jest możliwe tooconnect toohello wejściowych źródłowego, jak również inne aspekty toohello określonych danych wejściowych typu źródłowego. Na przykład w hello źródło wejścia obiektów blob utworzony w poprzednim kroku, metoda hello sprawdzi, czy nazwa konta magazynu hello i pary kluczy może być toohello tooconnect używane konto magazynu także Sprawdź, czy istnieje hello określonego kontenera.

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a>Utworzyć cel usługi analiza strumienia wyjściowego
Tworzenie obiektu docelowego dane wyjściowe jest bardzo podobne toocreating Stream Analytics źródło danych wejściowych. Podobnie jak źródeł danych wejściowych docelowe dla danych wyjściowych są tooa wiązanej określonego zadania. toouse hello tej samej wartości docelowej danych wyjściowych dla różnych zadań, należy wywołać metodę hello ponownie i określenia innej nazwy zadania.

Witaj następującego kodu tworzy obiekt docelowy danych wyjściowych (baza danych Azure SQL). Można dostosować hello dane wyjściowe docelowy typ danych i/lub typu serializacji.

   ```
   // Create an output
   Output output = new Output()
   {
       Datasource = new AzureSqlDatabaseOutputDataSource()
       {
           Server = "<YOUR DATABASE SERVER NAME>",
           Database = "<YOUR DATABASE NAME>",
           User = "<YOUR DATABASE LOGIN>",
           Password = "<YOUR DATABASE LOGIN PASSWORD>",
           Table = "<YOUR DATABASE TABLE NAME>"
       }
   };
   Output createOutputResult = streamAnalyticsManagementClient.Outputs.CreateOrReplace(output, resourceGroupName, streamingJobName, outputName);
   ```

## <a name="test-a-stream-analytics-output-target"></a>Testowanie elementu docelowego danych wyjściowych usługi analiza strumienia
Docelowy danych wyjściowych usługi analiza strumienia ma również hello **TestConnection** metody do testowania połączenia.

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a>Utworzyć transformację analiza strumienia
Witaj poniższy kod tworzy transformację Stream Analytics z zapytaniem hello "Wybierz * z danych wejściowych" i określa jedną jednostkę przesyłania strumieniowego tooallocate zadania usługi analiza strumienia hello. Aby uzyskać więcej informacji dotyczących dostosowywania jednostki przesyłania strumieniowego, zobacz [zadania usługi analiza strumienia Azure skali](stream-analytics-scale-jobs.md).

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

Podobnie jak dane wejściowe i wyjściowe transformację jest również wiązanej toohello określone zadanie usługi Stream Analytics została utworzona w obszarze.

## <a name="start-a-stream-analytics-job"></a>Uruchom zadanie usługi analiza strumienia
Po utworzeniu zadania usługi analiza strumienia i jego input(s) wyjściami i przekształcenie, można uruchomić zadania hello hello wywoływania **Start** metody.

Zadanie usługi Stream Analytics rozpoczyna się Hello następującego przykładowego kodu z danych wyjściowych niestandardowego początkowy czas zestaw tooDecember 12, 2012, 12:12:12 UTC:

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a>Zatrzymaj zadanie usługi analiza strumienia
Uruchomione zadania Stream Analytics można zatrzymać za hello wywoływania **zatrzymać** metody.

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a>Usuń zadanie usługi analiza strumienia
Witaj **usunąć** metoda usuwa hello zadania, a także hello bazowy podrzędne zasobów, w tym input(s) wyjściami i przekształcenie hello zadania.

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a>Uzyskiwanie pomocy technicznej
Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki
Zostały rozpoznane podstawy hello przy użyciu toocreate zestawu .NET SDK i uruchom zadania usługi analiza. toolearn więcej, zobacz następujące hello:

* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Management zestawu .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->
[5]: ./media/markdown-template-for-new-articles/octocats.png
[6]: ./media/markdown-template-for-new-articles/pretty49.png
[7]: ./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[azure.blob.storage]: http://azure.microsoft.com/documentation/services/storage/
[azure.blob.storage.use]: http://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-blobs/

[azure.event.hubs]: http://azure.microsoft.com/services/event-hubs/
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.forum]: http://go.microsoft.com/fwlink/?LinkId=512151

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.developer.guide]: stream-analytics-developer-guide.md
[stream.analytics.scale.jobs]: stream-analytics-scale-jobs.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301
