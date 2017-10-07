---
title: "aaaManagement v1.x zestawu .NET SDK dla usługi Azure Stream Analytics | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d205c388880e3d9c2ca5df218f4b68abac8c9780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-hello-azure-stream-analytics-api-for-net"></a><span data-ttu-id="e695b-106">Zarządzanie zestawu .NET SDK v1.x: Ustawianie i za pomocą zadania uruchamiania analizy hello interfejsu API usługi analiza strumienia Azure dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="e695b-106">Management .NET SDK v1.x: Set up and run analytics jobs using hello Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="e695b-107">Dowiedz się, jak tooset się oraz zadań wykonywania analizy przy użyciu interfejsu API usługi analiza strumienia hello dla platformy .NET przy użyciu zestawu .NET SDK zarządzania hello.</span><span class="sxs-lookup"><span data-stu-id="e695b-107">Learn how tooset up and run analytics jobs using hello Stream Analytics API for .NET using hello Management .NET SDK.</span></span> <span data-ttu-id="e695b-108">Konfigurowanie projektu, Utwórz wejściowymi i wyjściowymi źródeł, transformacji i rozpocząć i zatrzymać zadania.</span><span class="sxs-lookup"><span data-stu-id="e695b-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="e695b-109">Dla Twojego zadania usługi analiza może przesyłać strumieniowo dane z magazynu obiektów Blob lub Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="e695b-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="e695b-110">Zobacz hello [zarządzania dokumentacji dla hello interfejsu API usługi analiza strumienia dla platformy .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="e695b-110">See hello [management reference documentation for hello Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="e695b-111">Usługa Azure Stream Analytics to w pełni zarządzana usługa dostarczanie przetwarzania małych opóźnieniach, wysokiej dostępności, skalowalności, złożonych zdarzeń za pośrednictwem przesyłania strumieniowego danych w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="e695b-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="e695b-112">Analiza strumienia umożliwia tooset klientów w górę przesyłania strumieniowego strumienie danych tooanalyze zadań oraz pozwala toodrive niemal analiz w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="e695b-112">Stream Analytics enables customers tooset up streaming jobs tooanalyze data streams, and allows them toodrive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="e695b-113">Przykładowy kod w tym artykule nadal używa starszego (1.x) wersja zestawu .NET SDK usługi Azure Stream Analytics zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e695b-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="e695b-114">Przykładowy kod przy użyciu hello zaktualizowanej wersji zestawu SDK, zobacz [hello Użyj zestawu SDK .NET zarządzania dla usługi Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span><span class="sxs-lookup"><span data-stu-id="e695b-114">For sample code using hello up-to-date SDK version, please see [Use hello Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e695b-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e695b-115">Prerequisites</span></span>
<span data-ttu-id="e695b-116">Przed rozpoczęciem tego artykułu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="e695b-116">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="e695b-117">Zainstaluj program Visual Studio 2017 lub 2015.</span><span class="sxs-lookup"><span data-stu-id="e695b-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="e695b-118">Pobierz i zainstaluj [zestawu Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e695b-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="e695b-119">Utwórz grupy zasobów platformy Azure w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="e695b-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="e695b-120">Witaj poniżej znajduje się przykładowy skrypt programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="e695b-120">hello following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="e695b-121">Informacje programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="e695b-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in tooyour Azure account
        Add-AzureAccount

        # Select hello Azure subscription you want toouse toocreate hello resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered toohello subscription, remove hello remark symbol (#) toorun hello Register-AzureRMProvider cmdlet tooregister hello provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="e695b-122">Konfigurowanie źródła danych wejściowych i wyjściowych toouse docelowej.</span><span class="sxs-lookup"><span data-stu-id="e695b-122">Set up an input source and output target toouse.</span></span> <span data-ttu-id="e695b-123">Dodatkowe instrukcje można znaleźć [dodać dane wejściowe](stream-analytics-add-inputs.md) tooset się przykładowe dane wejściowe i [dodać danych wyjściowych](stream-analytics-add-outputs.md) tooset się przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="e695b-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) tooset up a sample input and [Add Outputs](stream-analytics-add-outputs.md) tooset up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="e695b-124">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="e695b-124">Set up a project</span></span>
<span data-ttu-id="e695b-125">toocreate zadania usługi Analiza użycia hello interfejsu API usługi analiza strumienia dla platformy .NET, należy najpierw skonfigurować projektu.</span><span class="sxs-lookup"><span data-stu-id="e695b-125">toocreate an analytics job use hello Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="e695b-126">Utwórz aplikację konsolową programu Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="e695b-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="e695b-127">W konsoli Menedżera pakietów hello hello uruchom następujące polecenia pakietów NuGet hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="e695b-127">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="e695b-128">Witaj najpierw jedna jest hello zestawu .NET SDK usługi Azure Stream Analytics zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e695b-128">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="e695b-129">Witaj drugim jest powitania klienta usługi Azure Active Directory, który będzie używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e695b-129">hello second one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="e695b-130">Dodaj następujące hello **appSettings** pliku App.config toohello sekcji:</span><span class="sxs-lookup"><span data-stu-id="e695b-130">Add hello following **appSettings** section toohello App.config file:</span></span>
   
        <appSettings>
          <!--CSM Prod related values-->
          <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
          <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
          <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
          <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
          <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
          <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION" />
          <add key="ActiveDirectoryTenantId" value="YOU TENANT ID" />
        </appSettings>

    <span data-ttu-id="e695b-131">Zastąp wartości **SubscriptionId** i **ActiveDirectoryTenantId** identyfikatorami z usługi Azure subskrypcji i dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="e695b-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="e695b-132">Te wartości można uzyskać, uruchamiając następujące polecenia cmdlet programu Azure PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="e695b-132">You can get these values by running hello following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="e695b-133">Dodaj następujące odwołania w pliku .csproj hello:</span><span class="sxs-lookup"><span data-stu-id="e695b-133">Add hello following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="e695b-134">Dodaj następujące hello **przy użyciu** instrukcje toohello pliku źródłowego (Program.cs) w projekcie hello:</span><span class="sxs-lookup"><span data-stu-id="e695b-134">Add hello following **using** statements toohello source file (Program.cs) in hello project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="e695b-135">Dodaj metodę pomocnika uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="e695b-135">Add an authentication helper method:</span></span>

   ```   
   private static async Task<string> GetAuthorizationHeader()
   {
       var context = new AuthenticationContext(
           ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
           ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);

        AuthenticationResult result = await context.AcquireTokenASync(
           resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
           clientId: ConfigurationManager.AppSettings["AsaClientId"],
           redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
           promptBehavior: PromptBehavior.Always);

        if (result != null)
            return result.AccessToken;

       throw new InvalidOperationException("Failed tooacquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="e695b-136">Tworzenie klienta zarządzania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e695b-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="e695b-137">A **StreamAnalyticsManagementClient** obiektu umożliwia toomanage hello zadania i hello zadania składniki, takie jak dane wejściowe, dane wyjściowe i przekształcania.</span><span class="sxs-lookup"><span data-stu-id="e695b-137">A **StreamAnalyticsManagementClient** object allows you toomanage hello job and hello job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="e695b-138">Dodaj następującego kodu toohello początku hello hello **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="e695b-138">Add hello following code toohello beginning of hello **Main** method:</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";
    string streamAnalyticsInputName = "<YOUR JOB INPUT NAME>";
    string streamAnalyticsOutputName = "<YOUR JOB OUTPUT NAME>";
    string streamAnalyticsTransformationName = "<YOUR JOB TRANSFORMATION NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
        ConfigurationManager.AppSettings["SubscriptionId"],
        GetAuthorizationHeader().Result);

    // Create Stream Analytics management client
    StreamAnalyticsManagementClient client = new StreamAnalyticsManagementClient(aadTokenCredentials);

<span data-ttu-id="e695b-139">Witaj **resourceGroupName** wartość zmiennej powinna być taka sama jak nazwa hello zasobu hello grupy utworzone lub pobrać wymagane wstępnie kroki hello hello.</span><span class="sxs-lookup"><span data-stu-id="e695b-139">hello **resourceGroupName** variable's value should be hello same as hello name of hello resource group you created or picked in hello prerequisite steps.</span></span>

<span data-ttu-id="e695b-140">tooautomate hello poświadczeń prezentacji aspekt tworzenia zadania, można znaleźć zbyt[uwierzytelniania nazwy głównej usługi z usługą Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="e695b-140">tooautomate hello credential presentation aspect of job creation, refer too[Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="e695b-141">Witaj pozostałe sekcje w tym artykule przyjęto, że ten kod zostało początku hello hello **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="e695b-141">hello remaining sections of this article assume that this code is at hello beginning of hello **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="e695b-142">Tworzenie zadania usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="e695b-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="e695b-143">Witaj poniższy kod tworzy zadanie usługi analiza strumienia, w grupie zasobów hello zdefiniowanej przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e695b-143">hello following code creates a Stream Analytics job under hello resource group that you have defined.</span></span> <span data-ttu-id="e695b-144">Zadanie toohello danych wejściowych, wyjściowych i przekształcenie zostaną dodane później.</span><span class="sxs-lookup"><span data-stu-id="e695b-144">You will add an input, output, and transformation toohello job later.</span></span>

    // Create a Stream Analytics job
    JobCreateOrUpdateParameters jobCreateParameters = new JobCreateOrUpdateParameters()
    {
        Job = new Job()
        {
            Name = streamAnalyticsJobName,
            Location = "<LOCATION>",
            Properties = new JobProperties()
            {
                EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Adjust,
                Sku = new Sku()
                {
                    Name = "Standard"
                }
            }
        }
    };

    JobCreateOrUpdateResponse jobCreateResponse = client.StreamingJobs.CreateOrUpdate(resourceGroupName, jobCreateParameters);


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="e695b-145">Utwórz źródło danych wejściowych analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e695b-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="e695b-146">Witaj poniższy kod tworzy Stream Analytics źródło danych wejściowych typu źródła danych wejściowych obiektu blob hello i serializacji woluminów CSV.</span><span class="sxs-lookup"><span data-stu-id="e695b-146">hello following code creates a Stream Analytics input source with hello blob input source type and CSV serialization.</span></span> <span data-ttu-id="e695b-147">Użyj toocreate źródło wejścia Centrum zdarzeń, **EventHubStreamInputDataSource** zamiast **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="e695b-147">toocreate an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="e695b-148">Podobnie można dostosować hello serializacji typu hello źródła danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="e695b-148">Similarly, you can customize hello serialization type of hello input source.</span></span>

    // Create a Stream Analytics input source
    InputCreateOrUpdateParameters jobInputCreateParameters = new InputCreateOrUpdateParameters()
    {
        Input = new Input()
        {
            Name = streamAnalyticsInputName,
            Properties = new StreamInputProperties()
            {
                Serialization = new CsvSerialization
                {
                    Properties = new CsvSerializationProperties
                    {
                        Encoding = "UTF8",
                        FieldDelimiter = ","
                    }
                },
                DataSource = new BlobStreamInputDataSource
                {
                    Properties = new BlobStreamInputDataSourceProperties
                    {
                        StorageAccounts = new StorageAccount[]
                        {
                            new StorageAccount()
                            {
                                AccountName = "<YOUR STORAGE ACCOUNT NAME>",
                                AccountKey = "<YOUR STORAGE ACCOUNT KEY>"
                            }
                        },
                        Container = "samples",
                        PathPattern = ""
                    }
                }
            }
        }
    };

    InputCreateOrUpdateResponse inputCreateResponse =
        client.Inputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobInputCreateParameters);

<span data-ttu-id="e695b-149">Źródeł danych wejściowych z magazynu obiektów Blob lub Centrum zdarzeń są wiązanej tooa określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="e695b-149">Input sources, whether from Blob storage or an event hub, are tied tooa specific job.</span></span> <span data-ttu-id="e695b-150">toouse hello tego samego źródła danych wejściowych dla różnych zadań, należy wywołać metodę hello ponownie i określenia innej nazwy zadania.</span><span class="sxs-lookup"><span data-stu-id="e695b-150">toouse hello same input source for different jobs, you must call hello method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="e695b-151">Testowanie usługi Stream Analytics źródło danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="e695b-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="e695b-152">Witaj **TestConnection** testy metody czy zadanie usługi Stream Analytics hello jest możliwe tooconnect toohello wejściowych źródłowego, jak również inne aspekty toohello określonych danych wejściowych typu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="e695b-152">hello **TestConnection** method tests whether hello Stream Analytics job is able tooconnect toohello input source as well as other aspects specific toohello input source type.</span></span> <span data-ttu-id="e695b-153">Na przykład w hello źródło wejścia obiektów blob utworzony w poprzednim kroku, metoda hello sprawdzi, czy nazwa konta magazynu hello i pary kluczy może być toohello tooconnect używane konto magazynu także Sprawdź, czy istnieje hello określonego kontenera.</span><span class="sxs-lookup"><span data-stu-id="e695b-153">For example, in hello blob input source you created in an earlier step, hello method will check that hello Storage account name and key pair can be used tooconnect toohello Storage account as well as check that hello specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="e695b-154">Utworzyć cel usługi analiza strumienia wyjściowego</span><span class="sxs-lookup"><span data-stu-id="e695b-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="e695b-155">Tworzenie obiektu docelowego dane wyjściowe jest bardzo podobne toocreating Stream Analytics źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="e695b-155">Creating an output target is very similar toocreating a Stream Analytics input source.</span></span> <span data-ttu-id="e695b-156">Podobnie jak źródeł danych wejściowych docelowe dla danych wyjściowych są tooa wiązanej określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="e695b-156">Like input sources, output targets are tied tooa specific job.</span></span> <span data-ttu-id="e695b-157">toouse hello tej samej wartości docelowej danych wyjściowych dla różnych zadań, należy wywołać metodę hello ponownie i określenia innej nazwy zadania.</span><span class="sxs-lookup"><span data-stu-id="e695b-157">toouse hello same output target for different jobs, you must call hello method again and specify a different job name.</span></span>

<span data-ttu-id="e695b-158">Witaj następującego kodu tworzy obiekt docelowy danych wyjściowych (baza danych Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="e695b-158">hello following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="e695b-159">Można dostosować hello dane wyjściowe docelowy typ danych i/lub typu serializacji.</span><span class="sxs-lookup"><span data-stu-id="e695b-159">You can customize hello output target's data type and/or serialization type.</span></span>

    // Create a Stream Analytics output target
    OutputCreateOrUpdateParameters jobOutputCreateParameters = new OutputCreateOrUpdateParameters()
    {
        Output = new Output()
        {
            Name = streamAnalyticsOutputName,
            Properties = new OutputProperties()
            {
                DataSource = new SqlAzureOutputDataSource()
                {
                    Properties = new SqlAzureOutputDataSourceProperties()
                    {
                        Server = "<YOUR DATABASE SERVER NAME>",
                        Database = "<YOUR DATABASE NAME>",
                        User = "<YOUR DATABASE LOGIN>",
                        Password = "<YOUR DATABASE LOGIN PASSWORD>",
                        Table = "<YOUR DATABASE TABLE NAME>"
                    }
                }
            }
        }
    };

    OutputCreateOrUpdateResponse outputCreateResponse =
        client.Outputs.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, jobOutputCreateParameters);

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="e695b-160">Testowanie elementu docelowego danych wyjściowych usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e695b-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="e695b-161">Docelowy danych wyjściowych usługi analiza strumienia ma również hello **TestConnection** metody do testowania połączenia.</span><span class="sxs-lookup"><span data-stu-id="e695b-161">A Stream Analytics output target also has hello **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="e695b-162">Utworzyć transformację analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e695b-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="e695b-163">Witaj poniższy kod tworzy transformację Stream Analytics z zapytaniem hello "Wybierz * z danych wejściowych" i określa jedną jednostkę przesyłania strumieniowego tooallocate zadania usługi analiza strumienia hello.</span><span class="sxs-lookup"><span data-stu-id="e695b-163">hello following code creates a Stream Analytics transformation with hello query "select * from Input" and specifies tooallocate one streaming unit for hello Stream Analytics job.</span></span> <span data-ttu-id="e695b-164">Aby uzyskać więcej informacji dotyczących dostosowywania jednostki przesyłania strumieniowego, zobacz [zadania usługi analiza strumienia Azure skali](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="e695b-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

    // Create a Stream Analytics transformation
    TransformationCreateOrUpdateParameters transformationCreateParameters = new TransformationCreateOrUpdateParameters()
    {
        Transformation = new Transformation()
        {
            Name = streamAnalyticsTransformationName,
            Properties = new TransformationProperties()
            {
                StreamingUnits = 1,
                Query = "select * from Input"
            }
        }
    };

    var transformationCreateResp =
        client.Transformations.CreateOrUpdate(resourceGroupName, streamAnalyticsJobName, transformationCreateParameters);

<span data-ttu-id="e695b-165">Podobnie jak dane wejściowe i wyjściowe transformację jest również wiązanej toohello określone zadanie usługi Stream Analytics została utworzona w obszarze.</span><span class="sxs-lookup"><span data-stu-id="e695b-165">Like input and output, a transformation is also tied toohello specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="e695b-166">Uruchom zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e695b-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="e695b-167">Po utworzeniu zadania usługi analiza strumienia i jego input(s) wyjściami i przekształcenie, można uruchomić zadania hello hello wywoływania **Start** metody.</span><span class="sxs-lookup"><span data-stu-id="e695b-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start hello job by calling hello **Start** method.</span></span>

<span data-ttu-id="e695b-168">Zadanie usługi Stream Analytics rozpoczyna się Hello następującego przykładowego kodu z danych wyjściowych niestandardowego początkowy czas zestaw tooDecember 12, 2012, 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="e695b-168">hello following sample code starts a Stream Analytics job with a custom output start time set tooDecember 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="e695b-169">Zatrzymaj zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e695b-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="e695b-170">Uruchomione zadania Stream Analytics można zatrzymać za hello wywoływania **zatrzymać** metody.</span><span class="sxs-lookup"><span data-stu-id="e695b-170">You can stop a running Stream Analytics job by calling hello **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="e695b-171">Usuń zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e695b-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="e695b-172">Witaj **usunąć** metoda usuwa hello zadania, a także hello bazowy podrzędne zasobów, w tym input(s) wyjściami i przekształcenie hello zadania.</span><span class="sxs-lookup"><span data-stu-id="e695b-172">hello **Delete** method will delete hello job as well as hello underlying sub-resources, including input(s), output(s), and transformation of hello job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="e695b-173">Uzyskiwanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="e695b-173">Get support</span></span>
<span data-ttu-id="e695b-174">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="e695b-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e695b-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e695b-175">Next steps</span></span>
<span data-ttu-id="e695b-176">Zostały rozpoznane podstawy hello przy użyciu toocreate zestawu .NET SDK i uruchom zadania usługi analiza.</span><span class="sxs-lookup"><span data-stu-id="e695b-176">You've learned hello basics of using a .NET SDK toocreate and run analytics jobs.</span></span> <span data-ttu-id="e695b-177">toolearn więcej, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="e695b-177">toolearn more, see hello following:</span></span>

* [<span data-ttu-id="e695b-178">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="e695b-178">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="e695b-179">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="e695b-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="e695b-180">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="e695b-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="e695b-181">[Azure Stream Analytics Management zestawu .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="e695b-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="e695b-182">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="e695b-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="e695b-183">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="e695b-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
