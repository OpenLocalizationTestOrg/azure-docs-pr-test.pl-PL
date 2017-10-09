---
title: "potoki danych aaaCreate przy użyciu zestawu Azure .NET SDK | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprogrammatically tworzenia, monitorowania i zarządzania fabryki danych Azure przy użyciu zestawu SDK fabryki danych."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a>Tworzenie, monitorowanie i zarządzanie przy użyciu zestawu SDK .NET usługi Azure Data Factory fabryki danych Azure
## <a name="overview"></a>Omówienie
Tworzenie, monitorowanie i zarządzanie fabryki danych Azure, programowo przy użyciu zestawu .NET SDK fabryki danych. Ten artykuł zawiera wskazówki, które możesz wykonać toocreate przykładowej aplikacji konsoli .NET, które tworzy i monitoruje fabryki danych. 

> [!NOTE]
> W tym artykule nie opisano wszystkich hello interfejs API .NET fabryki danych. Zobacz [dokumentacja interfejsu API platformy .NET fabryki danych](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) dla pełna dokumentacja interfejsu API platformy .NET dla fabryki danych. 

## <a name="prerequisites"></a>Wymagania wstępne
* Program Visual Studio w wersji 2012, 2013 lub 2015.
* Pobierz i zainstaluj [zestawu Azure .NET SDK](http://azure.microsoft.com/downloads/).
* Azure PowerShell. Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykuł tooinstall programu Azure PowerShell na komputerze. Korzystając z programu Azure PowerShell toocreate aplikację usługi Azure Active Directory.

### <a name="create-an-application-in-azure-active-directory"></a>Tworzenie aplikacji w usłudze Azure Active Directory
Tworzenie aplikacji usługi Azure Active Directory, tworzenie nazwy głównej usługi dla aplikacji hello i przypisać je toohello **współautora fabryki danych** roli.

1. Uruchom program **PowerShell**.
2. Uruchom następujące polecenie hello, a następnie wprowadź hello nazwy użytkownika i hasła, użyj toosign w toohello portalu Azure.

    ```PowerShell
    Login-AzureRmAccount
    ```
3. Uruchom następujące polecenie tooview hello wszystkie subskrypcje powitania dla tego konta.

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. Uruchom następujące polecenie tooselect hello subskrypcję, która ma toowork z hello. Zastąp  **&lt;NameOfAzureSubscription** &gt; o nazwie hello subskrypcji platformy Azure.

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > Należy zanotować **SubscriptionId** i **TenantId** z hello dane wyjściowe tego polecenia.

5. Tworzenie grupy zasobów platformy Azure o nazwie **ADFTutorialResourceGroup** , uruchamiając następujące polecenie w środowiska PowerShell hello hello.

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    Jeśli hello grupy zasobów już istnieje, określić czy tooupdate go (Y) lub zachować go jako (N).

    Jeśli używasz innej grupie zasobów, należy toouse hello Nazwa grupy zasobów, zamiast ADFTutorialResourceGroup w tym samouczku.
6. Utwórz aplikację usługi Azure Active Directory.

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    Jeśli zostanie wyświetlony następujący błąd hello, określ inny adres URL, a następnie ponownie uruchom polecenie hello.
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. Utwórz hello nazwy głównej usługi AD.

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. Dodaj toohello główna usługi **współautora fabryki danych** roli.

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. Pobierz identyfikator aplikacji hello

    ```PowerShell
    $azureAdApplication 
    ```
    Zanotuj identyfikator aplikacji hello (identyfikator aplikacji applicationID) z hello danych wyjściowych.

Po wykonaniu tych kroków powinny być dostępne cztery następujące wartości:

* Identyfikator dzierżawy
* Identyfikator subskrypcji
* Identyfikator aplikacji
* Hasło (określone w poleceniu pierwszy hello)

## <a name="walkthrough"></a>Przewodnik
W przewodniku hello tworzenie fabryki danych z potok, który zawiera działanie kopiowania. Witaj działanie kopiowania kopiuje dane z folderu w folderze tooanother magazynu obiektów blob platformy Azure w hello sam magazynu obiektów blob. 

Witaj działanie kopiowania wykonuje hello przenoszenia danych w fabryce danych Azure. działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności. Zobacz [działań przepływu danych](data-factory-data-movement-activities.md) artykułu szczegółowe informacje o hello działanie kopiowania.

1. Za pomocą programu Visual Studio 2012/2013/2015 utwórz aplikację konsolową .NET C#.
   1. Uruchom program **Visual Studio** 2012/2013/2015.
   2. Kliknij przycisk **pliku**, punktu zbyt**nowy**i kliknij przycisk **projektu**.
   3. Rozwiń węzeł **Szablony** i wybierz opcję **Visual C#**. W tym przewodniku stosowany jest język C#, ale można użyć dowolnego języka platformy .NET.
   4. Wybierz **aplikacji konsoli** z hello listy typów projektu na powitania prawo.
   5. Wprowadź **DataFactoryAPITestApp** dla hello nazwy.
   6. Wybierz **C:\ADFGetStarted** dla hello lokalizacji.
   7. Kliknij przycisk **OK** toocreate hello projektu.
2. Kliknij przycisk **narzędzia**, punktu zbyt**Menedżera pakietów NuGet**i kliknij przycisk **Konsola Menedżera pakietów**.
3. W hello **Konsola Menedżera pakietów**, hello następujące kroki:
   1. Uruchom hello następujące polecenia tooinstall fabryki danych pakietu:`Install-Package Microsoft.Azure.Management.DataFactories`
   2. Uruchom hello następującego pakietu usługi Azure Active Directory tooinstall polecenia (należy użyć interfejsu API usługi Active Directory w kodzie hello):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`
4. Zamień zawartość hello **App.config** plik w projekcie hello z hello następującej zawartości: 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. W pliku App.Config hello, zaktualizuj wartości  **&lt;identyfikator aplikacji&gt;**,  **&lt;hasło&gt;**,  **&lt; Identyfikator subskrypcji&gt;**, i  **&lt;Identyfikatorem dzierżawy&gt;**  z własne wartości.
6. Dodaj następujące hello **przy użyciu** toohello instrukcje **Program.cs** plik w projekcie hello.

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. Dodaj hello następującego kodu, który tworzy wystąpienie **DataPipelineManagementClient** toohello klasy **Main** metody. Ten obiekt toocreate są używane fabryki danych, połączonej usługi, wejściowych i wyjściowych zestawów danych i potoku. Można również użyć tego obiektu wycinków toomonitor zestawu danych w czasie wykonywania.

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Zastąp wartość hello **resourceGroupName** o nazwie hello grupy zasobów platformy Azure. Można utworzyć grupy zasobów przy użyciu hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) polecenia cmdlet.
   >
   > Zaktualizuj nazwę hello danych fabryki (dataFactoryName) toobe unikatowy. Nazwa fabryki danych hello musi być globalnie unikatowa. Artykuł [Data Factory — Naming Rules](data-factory-naming-rules.md) (Fabryka danych — zasady nazewnictwa) zawiera zasady nazewnictwa artefaktów usługi Fabryka danych.
7. Dodaj następującego kodu, który tworzy hello **fabryki danych** toohello **Main** metody.

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. Dodaj następującego kodu, który tworzy hello **połączonej usługi magazynu Azure** toohello **Main** metody.

   > [!IMPORTANT]
   > Zastąp wartości **storageaccountname** i **accountkey** nazwą konta usługi Azure Storage oraz jego kluczem.

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. Dodaj hello następującego kodu, który tworzy **zestawów danych wejściowych i wyjściowych** toohello **Main** metody.

    Witaj **FolderPath** dla hello blob danych wejściowych jest ustawiony za**adftutorial /** gdzie **adftutorial** jest nazwą hello hello kontenera w magazynie obiektów blob. Ten kontener nie istnieje w magazynie obiektów blob platformy Azure, utworzyć kontener o tej nazwie: **adftutorial** i przekazać kontener toohello pliku tekstowego.

    Hello FolderPath dla hello output ustawiono obiektu blob: **adftutorial/apifactoryoutput / {Slice}** gdzie **wycinka** jest hello na podstawie dynamicznie obliczona wartość **SliceStart**(uruchomienie Data i godzina każdy wycinek).

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. Dodaj hello poniższy kod, który **tworzy i włącza potoku** toohello **Main** metody. Ten potok zawiera działanie **CopyActivity**, które pobiera element **BlobSource** jako źródło i **BlobSink** jako ujście.

    Witaj działanie kopiowania wykonuje hello przenoszenia danych w fabryce danych Azure. działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności. Zobacz [działań przepływu danych](data-factory-data-movement-activities.md) artykułu szczegółowe informacje o hello działanie kopiowania.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. Dodaj hello następującego kodu toohello **Main** metody tooget hello stan wycinek danych hello wyjściowy zestaw danych. Istnieje tylko jeden wycinek oczekiwany w tym przykładzie.

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. **(opcjonalnie)**  Dodaj hello poniższy kod tooget Uruchom szczegóły toohello wycinek danych **Main** metody.

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. Dodaj następujące metody pomocnika używany przez hello hello **Main** toohello metody **Program** klasy. Ta metoda powoduje okno dialogowe umożliwiające podaj **nazwy użytkownika** i **hasło** Użyj toolog w portalu tooAzure.

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. W Eksploratorze rozwiązań hello, rozwiń projekt hello: **DataFactoryAPITestApp**, kliknij prawym przyciskiem myszy **odwołania**i kliknij przycisk **Dodaj odwołanie**. Zaznacz pole wyboru dla `System.Configuration` zestawu i kliknij przycisk **OK**.
15. Tworzenie aplikacji konsoli hello. Kliknij przycisk **kompilacji** w hello menu i kliknij przycisk **Kompiluj rozwiązanie**.
16. Upewnij się, że istnieje co najmniej jeden plik w kontenerze adftutorial hello w magazynie obiektów blob platformy Azure. W przeciwnym razie utwórz Emp.txt plik w programie Notatnik z powitania po zawartości i przekaż go toohello adftutorial kontenera.

    ```
    John, Doe
    Jane, Doe
    ```
17. Uruchom przykładowe hello klikając **debugowania** -> **Rozpocznij debugowanie** menu hello. Po wyświetleniu hello **pierwsze uruchomienie szczegóły wycinka danych**, zaczekaj kilka minut, a następnie naciśnij klawisz **ENTER**.
18. Użyj hello tooverify portalu Azure w tej fabryce danych hello **APITutorialFactory** jest tworzony z następującego artefakty hello:
    * Połączona usługa: **AzureStorageLinkedService**
    * Zestaw danych: **DatasetBlobSource** i **DatasetBlobDestination**.
    * Potok: **PipelineBlobSample**
19. Sprawdź, czy plik wyjściowy jest utworzony w hello **apifactoryoutput** folderu w hello **adftutorial** kontenera.

## <a name="get-a-list-of-failed-data-slices"></a>Pobierz listę wycinków danych nie powiodło się 

```csharp
// Parse hello resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a>Następne kroki
Zobacz poniższy przykład do utworzenia potoku przy użyciu zestawu .NET SDK, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure hello: 

- [Tworzenie potoku toocopy danych z magazynu obiektów Blob tooSQL bazy danych](data-factory-copy-activity-tutorial-using-dotnet-api.md)
