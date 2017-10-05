---
title: "Zarządzanie .NET v1.x zestawu SDK dla usługi Azure Stream Analytics | Dokumentacja firmy Microsoft"
description: "Rozpoczynanie pracy z Stream Analytics Management .NET SDK. Dowiedz się, jak skonfigurować i uruchomić zadania usługi analiza. Utwórz projekt, wejść, wyjść i przekształcenia."
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
ms.openlocfilehash: c75322ba53a447b8529023482945051caaf61bb2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="management-net-sdk-v1x-set-up-and-run-analytics-jobs-using-the-azure-stream-analytics-api-for-net"></a><span data-ttu-id="c1407-106">Zarządzanie zestawu .NET SDK v1.x: Ustaw Konfigurowanie i uruchamianie zadania usługi analiza przy użyciu interfejsu API usługi analiza strumienia Azure dla platformy .NET</span><span class="sxs-lookup"><span data-stu-id="c1407-106">Management .NET SDK v1.x: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>
<span data-ttu-id="c1407-107">Dowiedz się, jak skonfigurować i uruchomić zadania usługi analiza dla platformy .NET przy użyciu zestawu .NET SDK zarządzania przy użyciu interfejsu API usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="c1407-107">Learn how to set up and run analytics jobs using the Stream Analytics API for .NET using the Management .NET SDK.</span></span> <span data-ttu-id="c1407-108">Konfigurowanie projektu, Utwórz wejściowymi i wyjściowymi źródeł, transformacji i rozpocząć i zatrzymać zadania.</span><span class="sxs-lookup"><span data-stu-id="c1407-108">Set up a project, create input and output sources, transformations, and start and stop jobs.</span></span> <span data-ttu-id="c1407-109">Dla Twojego zadania usługi analiza może przesyłać strumieniowo dane z magazynu obiektów Blob lub Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="c1407-109">For your analytics jobs, you can stream data from Blob storage or from an event hub.</span></span>

<span data-ttu-id="c1407-110">Zobacz [zarządzania dokumentacji interfejsu API usługi analiza strumienia dla platformy .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1407-110">See the [management reference documentation for the Stream Analytics API for .NET](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>

<span data-ttu-id="c1407-111">Usługa Azure Stream Analytics to w pełni zarządzana usługa dostarczanie przetwarzania małych opóźnieniach, wysokiej dostępności, skalowalności, złożonych zdarzeń za pośrednictwem przesyłania strumieniowego danych w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c1407-111">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable, complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="c1407-112">Analiza strumienia umożliwia klientom ustawianie zadań przesyłania strumieniowego do analizowania strumieni danych oraz pozwala na dysku w pobliżu analiz w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="c1407-112">Stream Analytics enables customers to set up streaming jobs to analyze data streams, and allows them to drive near real-time analytics.</span></span>  

> [!NOTE]
> <span data-ttu-id="c1407-113">Przykładowy kod w tym artykule nadal używa starszego (1.x) wersja zestawu .NET SDK usługi Azure Stream Analytics zarządzania.</span><span class="sxs-lookup"><span data-stu-id="c1407-113">Sample code in this article still uses legacy (1.x) version of Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="c1407-114">Przykładowy kod za pomocą zaktualizowanej wersji zestawu SDK, zobacz [używanie zestawu SDK .NET zarządzania dla usługi Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span><span class="sxs-lookup"><span data-stu-id="c1407-114">For sample code using the up-to-date SDK version, please see [Use the Management .NET SDK for Stream Analytics](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-dotnet-management-sdk).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1407-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c1407-115">Prerequisites</span></span>
<span data-ttu-id="c1407-116">Przed rozpoczęciem korzystania z informacji zawartych w tym artykule należy dysponować następującymi elementami:</span><span class="sxs-lookup"><span data-stu-id="c1407-116">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="c1407-117">Zainstaluj program Visual Studio 2017 lub 2015.</span><span class="sxs-lookup"><span data-stu-id="c1407-117">Install Visual Studio 2017 or 2015.</span></span>
* <span data-ttu-id="c1407-118">Pobierz i zainstaluj [zestawu Azure .NET SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c1407-118">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="c1407-119">Utwórz grupy zasobów platformy Azure w ramach subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c1407-119">Create an Azure Resource Group in your subscription.</span></span> <span data-ttu-id="c1407-120">Poniżej przedstawiono przykładowy skrypt programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="c1407-120">The following is a sample Azure PowerShell script.</span></span> <span data-ttu-id="c1407-121">Informacje programu Azure PowerShell, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview);</span><span class="sxs-lookup"><span data-stu-id="c1407-121">For Azure PowerShell information, see [Install and configure Azure PowerShell](/powershell/azure/overview);</span></span>  

        # Log in to your Azure account
        Add-AzureAccount

        # Select the Azure subscription you want to use to create the resource group
        Select-AzureSubscription -SubscriptionName <subscription name>

            # If Stream Analytics has not been registered to the subscription, remove the remark symbol (#) to run the Register-AzureRMProvider cmdlet to register the provider namespace
            #Register-AzureRMProvider -Force -ProviderNamespace 'Microsoft.StreamAnalytics'

        # Create an Azure resource group
        New-AzureResourceGroup -Name <YOUR RESOURCE GROUP NAME> -Location <LOCATION>


* <span data-ttu-id="c1407-122">Skonfiguruj źródło danych wejściowych i docelowego dane wyjściowe do użycia.</span><span class="sxs-lookup"><span data-stu-id="c1407-122">Set up an input source and output target to use.</span></span> <span data-ttu-id="c1407-123">Dodatkowe instrukcje można znaleźć [dodać dane wejściowe](stream-analytics-add-inputs.md) skonfigurować przykładowe dane wejściowe i [dodać danych wyjściowych](stream-analytics-add-outputs.md) skonfigurować przykładowe dane wyjściowe.</span><span class="sxs-lookup"><span data-stu-id="c1407-123">For further instructions see [Add Inputs](stream-analytics-add-inputs.md) to set up a sample input and [Add Outputs](stream-analytics-add-outputs.md) to set up a sample output.</span></span>

## <a name="set-up-a-project"></a><span data-ttu-id="c1407-124">Konfigurowanie projektu</span><span class="sxs-lookup"><span data-stu-id="c1407-124">Set up a project</span></span>
<span data-ttu-id="c1407-125">Aby utworzyć zadania usługi analiza, należy użyć interfejsu API usługi analiza strumienia dla platformy .NET, należy najpierw skonfigurować projektu.</span><span class="sxs-lookup"><span data-stu-id="c1407-125">To create an analytics job use the Stream Analytics API for .NET, first set up your project.</span></span>

1. <span data-ttu-id="c1407-126">Utwórz aplikację konsolową programu Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="c1407-126">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="c1407-127">W konsoli Menedżera pakietów uruchom następujące polecenia można zainstalować pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="c1407-127">In the Package Manager Console, run the following commands to install the NuGet packages.</span></span> <span data-ttu-id="c1407-128">Pierwsza z nich jest Azure Stream Analytics Management .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="c1407-128">The first one is the Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="c1407-129">Drugim jest klienta usługi Azure Active Directory, który będzie używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="c1407-129">The second one is the Azure Active Directory client that will be used for authentication.</span></span>
   
        Install-Package Microsoft.Azure.Management.StreamAnalytics -Version 1.8.3
        Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.28.4
3. <span data-ttu-id="c1407-130">Dodaj następujące **appSettings** sekcji w pliku App.config:</span><span class="sxs-lookup"><span data-stu-id="c1407-130">Add the following **appSettings** section to the App.config file:</span></span>
   
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

    <span data-ttu-id="c1407-131">Zastąp wartości **SubscriptionId** i **ActiveDirectoryTenantId** identyfikatorami z usługi Azure subskrypcji i dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="c1407-131">Replace values for **SubscriptionId** and **ActiveDirectoryTenantId** with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="c1407-132">Te wartości można uzyskać, uruchamiając następujące polecenie cmdlet programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c1407-132">You can get these values by running the following Azure PowerShell cmdlet:</span></span>

        Get-AzureAccount

4. <span data-ttu-id="c1407-133">Dodaj następujące informacje w pliku .csproj:</span><span class="sxs-lookup"><span data-stu-id="c1407-133">Add the following reference in your .csproj file:</span></span>

        <Reference Include="System.Configuration" />

1. <span data-ttu-id="c1407-134">Dodaj następujące **przy użyciu** instrukcje do pliku źródłowego (Program.cs) w projekcie:</span><span class="sxs-lookup"><span data-stu-id="c1407-134">Add the following **using** statements to the source file (Program.cs) in the project:</span></span>
   
        using System;
        using System.Configuration;
        using System.Threading.Tasks;
        
        using Microsoft.Azure;
        using Microsoft.Azure.Management.StreamAnalytics;
        using Microsoft.Azure.Management.StreamAnalytics.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
2. <span data-ttu-id="c1407-135">Dodaj metodę pomocnika uwierzytelniania:</span><span class="sxs-lookup"><span data-stu-id="c1407-135">Add an authentication helper method:</span></span>

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

       throw new InvalidOperationException("Failed to acquire token");
   }
   ```  

## <a name="create-a-stream-analytics-management-client"></a><span data-ttu-id="c1407-136">Tworzenie klienta zarządzania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="c1407-136">Create a Stream Analytics management client</span></span>
<span data-ttu-id="c1407-137">A **StreamAnalyticsManagementClient** obiektu umożliwia zarządzanie zadania i składniki zadania, takie jak dane wejściowe, dane wyjściowe i przekształcania.</span><span class="sxs-lookup"><span data-stu-id="c1407-137">A **StreamAnalyticsManagementClient** object allows you to manage the job and the job components, such as input, output, and transformation.</span></span>

<span data-ttu-id="c1407-138">Dodaj następujący kod na początku **Main** metody:</span><span class="sxs-lookup"><span data-stu-id="c1407-138">Add the following code to the beginning of the **Main** method:</span></span>

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

<span data-ttu-id="c1407-139">**ResourceGroupName** wartość zmiennej powinna być taka sama jak nazwa grupy zasobów został utworzony lub pobrać wstępnie wymagane kroki.</span><span class="sxs-lookup"><span data-stu-id="c1407-139">The **resourceGroupName** variable's value should be the same as the name of the resource group you created or picked in the prerequisite steps.</span></span>

<span data-ttu-id="c1407-140">Aby zautomatyzować aspekt prezentacji poświadczenie tworzenia zadania, należy zapoznać się [uwierzytelniania nazwy głównej usługi z usługą Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="c1407-140">To automate the credential presentation aspect of job creation, refer to [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

<span data-ttu-id="c1407-141">Pozostałe sekcje w tym artykule założono, że ten kod jest na początku **Main** metody.</span><span class="sxs-lookup"><span data-stu-id="c1407-141">The remaining sections of this article assume that this code is at the beginning of the **Main** method.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="c1407-142">Tworzenie zadania usługi Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c1407-142">Create a Stream Analytics job</span></span>
<span data-ttu-id="c1407-143">Poniższy kod tworzy zadanie usługi analiza strumienia w grupie zasobów, który został zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="c1407-143">The following code creates a Stream Analytics job under the resource group that you have defined.</span></span> <span data-ttu-id="c1407-144">Zadania zostaną później dodane z danych wejściowych, wyjściowych i przekształcenie.</span><span class="sxs-lookup"><span data-stu-id="c1407-144">You will add an input, output, and transformation to the job later.</span></span>

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


## <a name="create-a-stream-analytics-input-source"></a><span data-ttu-id="c1407-145">Utwórz źródło danych wejściowych analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="c1407-145">Create a Stream Analytics input source</span></span>
<span data-ttu-id="c1407-146">Poniższy kod tworzy Stream Analytics źródło danych wejściowych typu źródła danych wejściowych obiektu blob i serializacji woluminów CSV.</span><span class="sxs-lookup"><span data-stu-id="c1407-146">The following code creates a Stream Analytics input source with the blob input source type and CSV serialization.</span></span> <span data-ttu-id="c1407-147">Aby utworzyć źródło wejścia Centrum zdarzeń, użyj **EventHubStreamInputDataSource** zamiast **BlobStreamInputDataSource**.</span><span class="sxs-lookup"><span data-stu-id="c1407-147">To create an event hub input source, use **EventHubStreamInputDataSource** instead of **BlobStreamInputDataSource**.</span></span> <span data-ttu-id="c1407-148">Podobnie można dostosować serializację typu źródła danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c1407-148">Similarly, you can customize the serialization type of the input source.</span></span>

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

<span data-ttu-id="c1407-149">Źródeł danych wejściowych z magazynu obiektów Blob lub Centrum zdarzeń są powiązane z konkretnym zadaniu.</span><span class="sxs-lookup"><span data-stu-id="c1407-149">Input sources, whether from Blob storage or an event hub, are tied to a specific job.</span></span> <span data-ttu-id="c1407-150">Aby użyć tego samego źródła danych wejściowych dla różnych zadań, należy ponownie wywołać metodę i określenia innej nazwy zadania.</span><span class="sxs-lookup"><span data-stu-id="c1407-150">To use the same input source for different jobs, you must call the method again and specify a different job name.</span></span>

## <a name="test-a-stream-analytics-input-source"></a><span data-ttu-id="c1407-151">Testowanie usługi Stream Analytics źródło danych wejściowych</span><span class="sxs-lookup"><span data-stu-id="c1407-151">Test a Stream Analytics input source</span></span>
<span data-ttu-id="c1407-152">**TestConnection** metoda sprawdza, czy zadanie usługi Stream Analytics jest w stanie połączyć się źródło danych wejściowych, jak również inne aspekty specyficzne dla typu źródła danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c1407-152">The **TestConnection** method tests whether the Stream Analytics job is able to connect to the input source as well as other aspects specific to the input source type.</span></span> <span data-ttu-id="c1407-153">Na przykład w źródło wejścia obiektów blob, utworzony w poprzednim kroku, metoda sprawdza, czy para klucza i nazwy konta magazynu może służyć do nawiązania połączenia z kontem magazynu, a także Sprawdź, czy istnieje określony kontener.</span><span class="sxs-lookup"><span data-stu-id="c1407-153">For example, in the blob input source you created in an earlier step, the method will check that the Storage account name and key pair can be used to connect to the Storage account as well as check that the specified container exists.</span></span>

    // Test input source connection
    DataSourceTestConnectionResponse inputTestResponse =
        client.Inputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsInputName);

## <a name="create-a-stream-analytics-output-target"></a><span data-ttu-id="c1407-154">Utworzyć cel usługi analiza strumienia wyjściowego</span><span class="sxs-lookup"><span data-stu-id="c1407-154">Create a Stream Analytics output target</span></span>
<span data-ttu-id="c1407-155">Tworzenie obiektu docelowego dane wyjściowe jest bardzo podobny do tworzenia usługi Stream Analytics źródło danych wejściowych.</span><span class="sxs-lookup"><span data-stu-id="c1407-155">Creating an output target is very similar to creating a Stream Analytics input source.</span></span> <span data-ttu-id="c1407-156">Jak źródeł danych wejściowych powiązane są elementy docelowe danych wyjściowych do określonego zadania.</span><span class="sxs-lookup"><span data-stu-id="c1407-156">Like input sources, output targets are tied to a specific job.</span></span> <span data-ttu-id="c1407-157">Aby użyć tej samej wartości docelowej danych wyjściowych dla różnych zadań, należy ponownie wywołać metodę i określenia innej nazwy zadania.</span><span class="sxs-lookup"><span data-stu-id="c1407-157">To use the same output target for different jobs, you must call the method again and specify a different job name.</span></span>

<span data-ttu-id="c1407-158">Poniższy kod tworzy obiekt docelowy danych wyjściowych (baza danych Azure SQL).</span><span class="sxs-lookup"><span data-stu-id="c1407-158">The following code creates an output target (Azure SQL database).</span></span> <span data-ttu-id="c1407-159">Można dostosować w danych wyjściowych elementu docelowego typu danych i/lub typu serializacji.</span><span class="sxs-lookup"><span data-stu-id="c1407-159">You can customize the output target's data type and/or serialization type.</span></span>

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

## <a name="test-a-stream-analytics-output-target"></a><span data-ttu-id="c1407-160">Testowanie elementu docelowego danych wyjściowych usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="c1407-160">Test a Stream Analytics output target</span></span>
<span data-ttu-id="c1407-161">Ma również elementu docelowego danych wyjściowych Stream Analytics **TestConnection** metody do testowania połączenia.</span><span class="sxs-lookup"><span data-stu-id="c1407-161">A Stream Analytics output target also has the **TestConnection** method for testing connections.</span></span>

    // Test output target connection
    DataSourceTestConnectionResponse outputTestResponse =
        client.Outputs.TestConnection(resourceGroupName, streamAnalyticsJobName, streamAnalyticsOutputName);

## <a name="create-a-stream-analytics-transformation"></a><span data-ttu-id="c1407-162">Utworzyć transformację analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="c1407-162">Create a Stream Analytics transformation</span></span>
<span data-ttu-id="c1407-163">Poniższy kod tworzy transformację Stream Analytics z zapytaniem "Wybierz * z danych wejściowych" i określa przydzielić jedną jednostkę przesyłania strumieniowego zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="c1407-163">The following code creates a Stream Analytics transformation with the query "select * from Input" and specifies to allocate one streaming unit for the Stream Analytics job.</span></span> <span data-ttu-id="c1407-164">Aby uzyskać więcej informacji dotyczących dostosowywania jednostki przesyłania strumieniowego, zobacz [zadania usługi analiza strumienia Azure skali](stream-analytics-scale-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="c1407-164">For more information on adjusting streaming units, see [Scale Azure Stream Analytics jobs](stream-analytics-scale-jobs.md).</span></span>

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

<span data-ttu-id="c1407-165">Podobnie jak dane wejściowe i wyjściowe transformację jest też powiązany z danego zadania Stream Analytics, został on utworzony w obszarze.</span><span class="sxs-lookup"><span data-stu-id="c1407-165">Like input and output, a transformation is also tied to the specific Stream Analytics job it was created under.</span></span>

## <a name="start-a-stream-analytics-job"></a><span data-ttu-id="c1407-166">Uruchom zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="c1407-166">Start a Stream Analytics job</span></span>
<span data-ttu-id="c1407-167">Po utworzeniu zadania usługi analiza strumienia i jego input(s) wyjściami i przekształcenie, można uruchomić zadanie, wywołując **Start** metody.</span><span class="sxs-lookup"><span data-stu-id="c1407-167">After creating a Stream Analytics job and its input(s), output(s), and transformation, you can start the job by calling the **Start** method.</span></span>

<span data-ttu-id="c1407-168">Poniższy przykładowy kod uruchamia zadania usługi analiza strumienia danych wyjściowych niestandardowego czas rozpoczęcia ustawioną 12 grudnia 2012 12:12:12 UTC:</span><span class="sxs-lookup"><span data-stu-id="c1407-168">The following sample code starts a Stream Analytics job with a custom output start time set to December 12, 2012, 12:12:12 UTC:</span></span>

    // Start a Stream Analytics job
    JobStartParameters jobStartParameters = new JobStartParameters
    {
        OutputStartMode = OutputStartMode.CustomTime,
        OutputStartTime = new DateTime(2012, 12, 12, 0, 0, 0, DateTimeKind.Utc)
    };

    LongRunningOperationResponse jobStartResponse = client.StreamingJobs.Start(resourceGroupName, streamAnalyticsJobName, jobStartParameters);

## <a name="stop-a-stream-analytics-job"></a><span data-ttu-id="c1407-169">Zatrzymaj zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="c1407-169">Stop a Stream Analytics job</span></span>
<span data-ttu-id="c1407-170">Można zatrzymać uruchomione zadanie usługi Stream Analytics wywołując **zatrzymać** metody.</span><span class="sxs-lookup"><span data-stu-id="c1407-170">You can stop a running Stream Analytics job by calling the **Stop** method.</span></span>

    // Stop a Stream Analytics job
    LongRunningOperationResponse jobStopResponse = client.StreamingJobs.Stop(resourceGroupName, streamAnalyticsJobName);

## <a name="delete-a-stream-analytics-job"></a><span data-ttu-id="c1407-171">Usuń zadanie usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="c1407-171">Delete a Stream Analytics job</span></span>
<span data-ttu-id="c1407-172">**Usunąć** metoda usuwa zadanie, a także podrzędne zasobów, w tym input(s), wyjściami i przekształcenie zadania.</span><span class="sxs-lookup"><span data-stu-id="c1407-172">The **Delete** method will delete the job as well as the underlying sub-resources, including input(s), output(s), and transformation of the job.</span></span>

    // Delete a Stream Analytics job
    LongRunningOperationResponse jobDeleteResponse = client.StreamingJobs.Delete(resourceGroupName, streamAnalyticsJobName);

## <a name="get-support"></a><span data-ttu-id="c1407-173">Uzyskiwanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="c1407-173">Get support</span></span>
<span data-ttu-id="c1407-174">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="c1407-174">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1407-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c1407-175">Next steps</span></span>
<span data-ttu-id="c1407-176">Znasz już podstawy przy użyciu zestawu .NET SDK do tworzenia i uruchamiania zadania usługi analiza.</span><span class="sxs-lookup"><span data-stu-id="c1407-176">You've learned the basics of using a .NET SDK to create and run analytics jobs.</span></span> <span data-ttu-id="c1407-177">Aby dowiedzieć się więcej, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="c1407-177">To learn more, see the following:</span></span>

* [<span data-ttu-id="c1407-178">Wprowadzenie do usługi Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c1407-178">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c1407-179">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="c1407-179">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c1407-180">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="c1407-180">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* <span data-ttu-id="c1407-181">[Azure Stream Analytics Management zestawu .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span><span class="sxs-lookup"><span data-stu-id="c1407-181">[Azure Stream Analytics Management .NET SDK](https://msdn.microsoft.com/library/azure/dn889315.aspx).</span></span>
* [<span data-ttu-id="c1407-182">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="c1407-182">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c1407-183">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="c1407-183">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

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
