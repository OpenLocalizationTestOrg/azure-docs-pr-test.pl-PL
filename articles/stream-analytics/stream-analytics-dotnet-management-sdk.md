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
# <a name="management-net-sdk-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="24dfd-106">Zarządzanie zestawu .NET SDK: Konfigurowanie i uruchamianie zadania usługi analiza dla platformy .NET przy użyciu interfejsu API usługi Azure Stream Analytics hello</span><span class="sxs-lookup"><span data-stu-id="24dfd-106">Management .NET SDK: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="24dfd-107">Dowiedz się, jak tooset się oraz zadań wykonywania analizy przy użyciu interfejsu API usługi analiza strumienia hello dla platformy .NET przy użyciu zestawu .NET SDK zarządzania hello.</span><span class="sxs-lookup"><span data-stu-id="24dfd-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="24dfd-108">Konfigurowanie projektu, Utwórz wejściowymi i wyjściowymi źródeł, transformacji i rozpocząć i zatrzymać zadania.</span><span class="sxs-lookup"><span data-stu-id="24dfd-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="24dfd-109">Dla Twojego zadania usługi analiza może przesyłać strumieniowo dane z magazynu obiektów Blob lub Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="24dfd-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="24dfd-110">Zobacz hello [zarządzania dokumentacji dla hello interfejsu API usługi analiza strumienia dla platformy .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="24dfd-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="24dfd-111">Usługa Azure Stream Analytics to w pełni zarządzana usługa dostarczanie przetwarzania małych opóźnieniach, wysokiej dostępności, skalowalności, złożonych zdarzeń za pośrednictwem przesyłania strumieniowego danych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="24dfd-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="24dfd-112">Analiza strumienia umożliwia tooset klientów w górę przesyłania strumieniowego strumienie danych tooanalyze zadań oraz pozwala toodrive niemal analiz w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="24dfd-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="24dfd-113">Witaj przykładowy kod w tym artykule zostały zaktualizowane z zestawu .NET SDK usługi Azure Stream Analytics zarządzania v2.x wersją.</span><span class="sxs-lookup"><span data-stu-id="24dfd-113">We have updated hello sample code in this article with Azure Stream Analytics Management .NET SDK v2.x version.</span></span> <span data-ttu-id="24dfd-114">Przykładowy kod przy użyciu hello użycia wersja zestawu SDK lagecy (1.x), można znaleźć pod adresem [v1.x zestawu .NET SDK zarządzania hello na użytek Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span><span class="sxs-lookup"><span data-stu-id="24dfd-114">For sample code using hello uses lagecy (1.x) SDK version, please see [Use hello Management .NET SDK v1.x for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk-v1).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24dfd-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="24dfd-115">Prerequisites</span></span>
<span data-ttu-id="24dfd-116">Przed rozpoczęciem tego artykułu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="24dfd-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="24dfd-117">Zainstaluj program Visual Studio 2017 lub 2015.</span><span class="sxs-lookup"><span data-stu-id="24dfd-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="24dfd-118">Pobierz i zainstaluj [zestawu Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="24dfd-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="24dfd-119">Utwórz grupy zasobów platformy Azure w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="24dfd-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="24dfd-120">Witaj poniżej znajduje się przykładowy skrypt programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="24dfd-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="24dfd-121">Informacje programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="24dfd-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="24dfd-122">Konfigurowanie źródła danych wejściowych i wyjściowych toouse docelowej.</span><span class="sxs-lookup"><span data-stu-id="24dfd-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="24dfd-123">Dodatkowe instrukcje można znaleźć [dodać dane wejściowe](stream-analytics-add-inputs.md) tooset się przykładowe dane wejściowe i [dodać danych wyjściowych](stream-analytics-add-outputs.md) tooset się przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="24dfd-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="24dfd-124">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="24dfd-124">Set up a project</span></span>
<span data-ttu-id="24dfd-125">toocreate zadania usługi Analiza użycia hello interfejsu API usługi analiza strumienia dla platformy .NET, należy najpierw skonfigurować projektu.</span><span class="sxs-lookup"><span data-stu-id="24dfd-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="24dfd-126">Utwórz aplikację konsolową programu Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="24dfd-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="24dfd-127">W konsoli Menedżera pakietów hello hello uruchom następujące polecenia pakietów NuGet hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="24dfd-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="24dfd-128">Witaj najpierw jedna jest hello zestawu .NET SDK usługi Azure Stream Analytics zarządzania.</span><span class="sxs-lookup"><span data-stu-id="24dfd-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="24dfd-129">Witaj drugim jest do uwierzytelniania klienta usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="24dfd-129">hello second one is for Azure client authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 2.0.0
        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Version 2.3.1
3. <span data-ttu-id="24dfd-130">Dodaj następujące hello **appSettings** pliku App.config toohello sekcji:</span><span class="sxs-lookup"><span data-stu-id="24dfd-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <add key="ClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR SUBSCRIPTION ID" />
          <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
        </appSettings>

    <span data-ttu-id="24dfd-131">Zastąp wartości **SubscriptionId** i **ActiveDirectoryTenantId** identyfikatorami z usługi Azure subskrypcji i dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="24dfd-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="24dfd-132">Te wartości można uzyskać, uruchamiając następujące polecenia cmdlet programu Azure PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="24dfd-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="24dfd-133">Dodaj następujące odwołania w pliku .csproj hello:</span><span class="sxs-lookup"><span data-stu-id="24dfd-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

5. <span data-ttu-id="24dfd-134">Dodaj następujące hello **przy użyciu** instrukcje toohello pliku źródłowego (Program.cs) w projekcie hello:</span><span class="sxs-lookup"><span data-stu-id="24dfd-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Configuration;
        using System.Threading;
        using System.Threading.Tasks;
        
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Rest;
6. <span data-ttu-id="24dfd-135">Dodaj metodę pomocnika uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="24dfd-135">Add an authentication helper method:</span></span>

   ```
   private static async Task<ServiceClientCredentials> GetCredentials()
   {
       var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(ConfigurationManager.AppSettings["ClientId"], new Uri("urn:ietf:wg:oauth:2.0:oob"));
       ServiceClientCredentials credentials = await UserTokenProvider.LoginWithPromptAsync(ConfigurationManager.AppSettings["ActiveDirectoryTenantId"], activeDirectoryClientSettings);
       
       return credentials;
    }
   ```

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="24dfd-136">Tworzenie klienta zarządzania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="24dfd-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="24dfd-137">A **StreamAnalyticsManagementClient** obiektu umożliwia toomanage hello zadania i hello zadania składniki, takie jak dane wejściowe, dane wyjściowe i przekształcania.</span><span class="sxs-lookup"><span data-stu-id="24dfd-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="24dfd-138">Dodaj następującego kodu toohello początku hello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="24dfd-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

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

<span data-ttu-id="24dfd-139">Witaj **resourceGroupName** wartość zmiennej powinna być taka sama jak nazwa hello zasobu hello grupy utworzone lub pobrać wymagane wstępnie kroki hello hello.</span><span class="sxs-lookup"><span data-stu-id="24dfd-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="24dfd-140">tooautomate hello poświadczeń prezentacji aspekt tworzenia zadania, można znaleźć zbyt[uwierzytelniania nazwy głównej usługi z usługą Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="24dfd-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="24dfd-141">Witaj pozostałe sekcje w tym artykule przyjęto, że ten kod zostało początku hello hello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="24dfd-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="24dfd-142">Tworzenie zadania usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="24dfd-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="24dfd-143">Witaj poniższy kod tworzy zadanie usługi analiza strumienia, w grupie zasobów hello zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24dfd-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="24dfd-144">Zadanie toohello danych wejściowych, wyjściowych i przekształcenie zostaną dodane później.</span><span class="sxs-lookup"><span data-stu-id="24dfd-144">You will add an input, output, and transformation toohello job later.</span></span>

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

## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="24dfd-145">Utwórz źródło danych wejściowych analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="24dfd-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="24dfd-146">Witaj poniższy kod tworzy Stream Analytics źródło danych wejściowych typu źródła danych wejściowych obiektu blob hello i serializacji woluminów CSV.</span><span class="sxs-lookup"><span data-stu-id="24dfd-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="24dfd-147">Użyj toocreate źródło wejścia Centrum zdarzeń, **EventHubStreamInputDataSource** zamiast **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="24dfd-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="24dfd-148">Podobnie można dostosować hello serializacji typu hello źródła danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="24dfd-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

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

<span data-ttu-id="24dfd-149">Źródeł danych wejściowych z magazynu obiektów Blob lub Centrum zdarzeń są wiązanej tooa określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="24dfd-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="24dfd-150">toouse hello tego samego źródła danych wejściowych dla różnych zadań, należy wywołać metodę hello ponownie i określenia innej nazwy zadania.</span><span class="sxs-lookup"><span data-stu-id="24dfd-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="24dfd-151">Testowanie usługi Stream Analytics źródło danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="24dfd-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="24dfd-152">Witaj **TestConnection** testy metody czy zadanie usługi Stream Analytics hello jest możliwe tooconnect toohello wejściowych źródłowego, jak również inne aspekty toohello określonych danych wejściowych typu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="24dfd-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="24dfd-153">Na przykład w hello źródło wejścia obiektów blob utworzony w poprzednim kroku, metoda hello sprawdzi, czy nazwa konta magazynu hello i pary kluczy może być toohello tooconnect używane konto magazynu także Sprawdź, czy istnieje hello określonego kontenera.</span><span class="sxs-lookup"><span data-stu-id="24dfd-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

   ```
   // Test hello connection toohello input
   ResourceTestStatus testInputResult = streamAnalyticsManagementClient.Inputs.Test(resourceGroupName, streamingJobName, inputName);
   ```

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="24dfd-154">Utworzyć cel usługi analiza strumienia wyjściowego</span><span class="sxs-lookup"><span data-stu-id="24dfd-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="24dfd-155">Tworzenie obiektu docelowego dane wyjściowe jest bardzo podobne toocreating Stream Analytics źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="24dfd-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="24dfd-156">Podobnie jak źródeł danych wejściowych docelowe dla danych wyjściowych są tooa wiązanej określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="24dfd-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="24dfd-157">toouse hello tej samej wartości docelowej danych wyjściowych dla różnych zadań, należy wywołać metodę hello ponownie i określenia innej nazwy zadania.</span><span class="sxs-lookup"><span data-stu-id="24dfd-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="24dfd-158">Witaj następującego kodu tworzy obiekt docelowy danych wyjściowych (baza danych Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="24dfd-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="24dfd-159">Można dostosować hello dane wyjściowe docelowy typ danych i/lub typu serializacji.</span><span class="sxs-lookup"><span data-stu-id="24dfd-159">You can customize hello output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="24dfd-160">Testowanie elementu docelowego danych wyjściowych usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="24dfd-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="24dfd-161">Docelowy danych wyjściowych usługi analiza strumienia ma również hello **TestConnection** metody do testowania połączenia.</span><span class="sxs-lookup"><span data-stu-id="24dfd-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

   ```
   // Test hello connection toohello output
   ResourceTestStatus testOutputResult = streamAnalyticsManagementClient.Outputs.Test(resourceGroupName, streamingJobName, outputName);
   ```

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="24dfd-162">Utworzyć transformację analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="24dfd-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="24dfd-163">Witaj poniższy kod tworzy transformację Stream Analytics z zapytaniem hello "Wybierz * z danych wejściowych" i określa jedną jednostkę przesyłania strumieniowego tooallocate zadania usługi analiza strumienia hello.</span><span class="sxs-lookup"><span data-stu-id="24dfd-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="24dfd-164">Aby uzyskać więcej informacji dotyczących dostosowywania jednostki przesyłania strumieniowego, zobacz [zadania usługi analiza strumienia Azure skali](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="24dfd-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

   ```
   // Create a transformation
   Transformation transformation = new Transformation()
   {
       Query = "Select Id, Name from <your input name>", // '<your input name>' should be replaced with hello value you put for hello 'inputName' variable above or in a previous step
       StreamingUnits = 1
   };
   Transformation createTransformationResult = streamAnalyticsManagementClient.Transformations.CreateOrReplace(transformation, resourceGroupName, streamingJobName, transformationName);
   ```

<span data-ttu-id="24dfd-165">Podobnie jak dane wejściowe i wyjściowe transformację jest również wiązanej toohello określone zadanie usługi Stream Analytics została utworzona w obszarze.</span><span class="sxs-lookup"><span data-stu-id="24dfd-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="24dfd-166">Uruchom zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="24dfd-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="24dfd-167">Po utworzeniu zadania usługi analiza strumienia i jego input(s) wyjściami i przekształcenie, można uruchomić zadania hello hello wywoływania **Start** metody.</span><span class="sxs-lookup"><span data-stu-id="24dfd-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="24dfd-168">Zadanie usługi Stream Analytics rozpoczyna się Hello następującego przykładowego kodu z danych wyjściowych niestandardowego początkowy czas zestaw tooDecember 12, 2012, 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="24dfd-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

   ```
   // Start a streaming job
   StartStreamingJobParameters startStreamingJobParameters = new StartStreamingJobParameters()
   {
       OutputStartMode = OutputStartMode.CustomTime,
       OutputStartTime = new DateTime(2012, 12, 12, 12, 12, 12, DateTimeKind.Utc)
   };
   streamAnalyticsManagementClient.StreamingJobs.Start(resourceGroupName, streamingJobName, startStreamingJobParameters);
   ```

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="24dfd-169">Zatrzymaj zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="24dfd-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="24dfd-170">Uruchomione zadania Stream Analytics można zatrzymać za hello wywoływania **zatrzymać** metody.</span><span class="sxs-lookup"><span data-stu-id="24dfd-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

   ```
   // Stop a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Stop(resourceGroupName, streamingJobName);
   ```

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="24dfd-171">Usuń zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="24dfd-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="24dfd-172">Witaj **usunąć** metoda usuwa hello zadania, a także hello bazowy podrzędne zasobów, w tym input(s) wyjściami i przekształcenie hello zadania.</span><span class="sxs-lookup"><span data-stu-id="24dfd-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

   ```
   // Delete a streaming job
   streamAnalyticsManagementClient.StreamingJobs.Delete(resourceGroupName, streamingJobName);
   ```

## <a name="get-support"></a><span data-ttu-id="24dfd-173">Uzyskiwanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="24dfd-173">Get support</span></span>
<span data-ttu-id="24dfd-174">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="24dfd-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="24dfd-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="24dfd-175">Next steps</span></span>
<span data-ttu-id="24dfd-176">Zostały rozpoznane podstawy hello przy użyciu toocreate zestawu .NET SDK i uruchom zadania usługi analiza.</span><span class="sxs-lookup"><span data-stu-id="24dfd-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="24dfd-177">toolearn więcej, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="24dfd-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="24dfd-178">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="24dfd-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="24dfd-179">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="24dfd-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="24dfd-180">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="24dfd-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="24dfd-181">[Azure Stream Analytics Management zestawu .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="24dfd-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="24dfd-182">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="24dfd-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="24dfd-183">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="24dfd-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
