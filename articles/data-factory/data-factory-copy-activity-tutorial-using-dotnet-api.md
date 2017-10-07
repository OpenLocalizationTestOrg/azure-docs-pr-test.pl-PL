---
title: "Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu interfejsu API .NET | Microsoft Docs"
description: "Ten samouczek zawiera instrukcje tworzenia potoku usługi Azure Data Factory za pomocą działania kopiowania przy użyciu interfejsu API .NET."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a>Samouczek: tworzenie potoku za pomocą działania kopiowania przy użyciu interfejsu API .NET
> [!div class="op_single_selector"]
> * [Przegląd i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Kreator kopiowania](data-factory-copy-data-wizard-tutorial.md)
> * [Witryna Azure Portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Program Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [Program PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Szablon usługi Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [Interfejs API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [Interfejs API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)

W tym artykule dowiesz się, jak toouse [interfejs API .NET](https://portal.azure.com) toocreate fabryki danych z potok, który kopiuje dane z bazy danych Azure SQL tooan magazynu obiektów blob platformy Azure. Jeśli nowy tooAzure fabryki danych, zapoznaj się z artykułem hello [tooAzure wprowadzenie fabryki danych](data-factory-introduction.md) artykuł przed wykonaniem tego samouczka.   

W tym samouczku opisano tworzenie potoku z jednym działaniem (Działanie kopiowania). działanie kopiowania Hello kopiuje dane z magazynu danych obsługiwanych ujścia magazynu tooa obsługiwane dane. Aby zapoznać się z listą magazynów danych obsługiwanych jako źródła i ujścia, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). działanie Hello jest obsługiwany przez ogólnie dostępna usługa, która można skopiować dane między różnych magazynach danych w sposób bezpieczny, niezawodny i skalowalności. Aby uzyskać więcej informacji na temat hello działanie kopiowania, zobacz [działań przepływu danych](data-factory-data-movement-activities.md).

Potok może obejmować więcej niż jedno działanie. I tworzenia łańcucha dwa działania (Uruchom jedno działanie po drugim), ustawiając hello wyjściowy zestaw danych z jednego działania jako hello wejściowy zestaw danych z hello innych działań. Aby uzyskać więcej informacji, zobacz sekcję dotyczącą [wielu działań w potoku](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline). 

> [!NOTE] 
> Aby zapoznać się z pełną dokumentacją dotyczącą interfejsu API .NET usługi Data Factory, zobacz [dokumentację interfejsu API .NET usługi Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).
> 
> Witaj potoku danych w tym samouczku kopiuje dane z magazynu danych źródła danych magazynu tooa docelowego. Samouczek na temat danych tootransform przy użyciu fabryki danych Azure, zobacz [samouczek: Tworzenie danych tootransform potoku, przy użyciu klastra usługi Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Wymagania wstępne
* Przejdź przez [samouczek omówienie i wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget omówienie samouczek hello i pełne hello **wymagań wstępnych** czynności.
* Program Visual Studio w wersji 2012, 2013 lub 2015.
* Pobierz i zainstaluj zestaw [SDK .NET Azure](http://azure.microsoft.com/downloads/).
* Azure PowerShell. Postępuj zgodnie z instrukcjami wyświetlanymi w [jak tooinstall i konfigurowanie programu Azure PowerShell](../powershell-install-configure.md) artykuł tooinstall programu Azure PowerShell na komputerze. Korzystając z programu Azure PowerShell toocreate aplikację usługi Azure Active Directory.

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
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
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
4. Dodaj następujące hello **appSetttings** toohello sekcji **App.config** pliku. Te ustawienia są używane przez metodę pomocniczą hello: **GetAuthorizationHeader**.

    Zastąp wartości **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** i **&lt;tenant ID&gt;** własnymi wartościami.

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

5. Dodaj następujące hello **przy użyciu** instrukcje toohello pliku źródłowego (Program.cs) w projekcie hello.

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
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > Zastąp wartość hello **resourceGroupName** o nazwie hello grupy zasobów platformy Azure.
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

    Fabryka danych może obejmować jeden lub wiele potoków. Potok może obejmować jedno lub wiele działań. Na przykład toocopy działanie kopiowania danych z magazynu danych docelowy tooa źródłowego i HDInsight Hive działania toorun tootransform skryptu Hive wejściowe dane wyjściowe tooproduct danych. Zacznijmy od utworzenia hello fabryki danych w tym kroku.
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

    Połączone usługi są tworzone w toolink fabryki danych dane są przechowywane i obliczeniowe fabryki danych toohello usług. W tym samouczku nie przedstawiono korzystania z żadnych usług obliczeniowych, takich jak Azure HDInsight czy Azure Data Lake Analytics. Zostają użyte dwa magazyny danych typu Azure Storage (źródło) i Azure SQL Database (lokalizacja docelowa). 

    W związku z tym tworzy się dwie połączone usługi o nazwie AzureStorageLinkedService i AzureSqlLinkedService typu: AzureStorage i AzureSqlDatabase.  

    Witaj AzureStorageLinkedService łączy fabrykę danych toohello konta magazynu platformy Azure. To konto magazynu jest hello jedną w którym utworzono kontener i hello dane przekazane jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
9. Dodaj hello następującego kodu, który tworzy **Azure SQL połączona usługa** toohello **Main** metody.

   > [!IMPORTANT]
   > Zastąp wartości **servername**, **databasename**, **username** oraz **password** nazwą serwera SQL Azure, nazwą bazy danych, nazwą użytkownika i hasłem.

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    AzureSqlLinkedService łączy fabrykę danych toohello bazy danych Azure SQL. dane Hello, który jest skopiowany z magazynu obiektów blob hello są przechowywane w tej bazie danych. Utworzono hello pustych elementów tabeli w tej bazie danych jako część [wymagania wstępne](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
10. Dodaj hello następującego kodu, który tworzy **zestawów danych wejściowych i wyjściowych** toohello **Main** metody.

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    W poprzednim kroku hello utworzono toolink połączone usługi konta magazynu Azure i fabryki danych tooyour bazy danych Azure SQL. W tym kroku należy zdefiniować dwa zestawy danych o nazwie InputDataset i OutputDataset reprezentujące danych wejściowych i wyjściowych danych przechowywanych w magazynach danych hello odwołuje się AzureStorageLinkedService i AzureSqlLinkedService odpowiednio.

    Hello Azure połączoną usługą magazynu określa parametry połączenia hello, która używa usługi fabryka danych w czasie wykonywania tooconnect tooyour kontem magazynu platformy Azure. I zestawu danych wejściowych obiektu blob hello (InputDataset) określa hello kontenera i folderu hello, który zawiera hello danych wejściowych.  

    Podobnie hello usługi baza danych SQL Azure połączone określa hello parametry połączenia, które korzysta z usługi fabryka danych w czasie wykonywania tooconnect tooyour — bazy danych Azure SQL. I hello danych wyjściowych SQL tabeli dataset (OututDataset) określa hello tabeli w hello bazy danych toowhich powitalne dane z magazynu obiektów blob hello są kopiowane.

    W tym kroku utworzysz zestaw danych o nazwie InputDataset, który wskazuje plik obiektu blob tooa (emp.txt) w folderze głównym hello kontenera obiektów blob (adftutorial) w hello reprezentowany przez hello AzureStorageLinkedService połączone usługi Magazyn Azure. Brak określić wartość dla nazwy pliku hello (lub Pomiń je), danych z wszystkich obiektów blob w folderze wejściowych hello są skopiowanych toohello docelowego. W tym samouczku należy określić wartość dla hello fileName.    

    W tym kroku tworzony jest wyjściowy zestaw danych o nazwie **OutputDataset**. Ten zestaw danych wskazuje tooa tabeli SQL w bazie danych Azure SQL hello reprezentowany przez **AzureSqlLinkedService**.
11. Dodaj hello poniższy kod, który **tworzy i włącza potoku** toohello **Main** metody. W tym kroku opisano tworzenie potoku za pomocą **działania kopiowania**, w którym parametr **InputDataset** jest używany jako dane wejściowe, a parametr **OutputDataset** jako dane wyjściowe.

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    Należy zwrócić uwagę hello następujące punkty:
   
    - W sekcji działania hello jest tylko jedno działanie którego **typu** ustawiono zbyt**kopiowania**. Aby uzyskać więcej informacji o działaniu kopiowania hello, zobacz [działań przepływu danych](data-factory-data-movement-activities.md). W rozwiązaniach usługi Data Factory można również użyć [działań dotyczących przekształcania danych](data-factory-data-transformation-activities.md).
    - Dane wejściowe dla działania hello jest ustawiony za**InputDataset** i danych wyjściowych dla działania hello jest ustawiony za**OutputDataset**. 
    - W hello **typeProperties** sekcji **BlobSource** jest określony jako typ źródła hello i **SqlSink** jest określony jako typ ujścia hello. Aby uzyskać pełną listę obsługiwanych przez działanie kopiowania hello jako źródła i wychwytywanie magazyny danych, zobacz [obsługiwane magazyny danych](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn jak przechowywać toouse określonych danych obsługiwane jako źródło/ujście, kliknij łącze hello hello tabeli.  
   
    Wyjściowy zestaw danych jest obecnie, jakie dysków hello harmonogramu. W tym samouczku wyjściowy zestaw danych jest skonfigurowane tooproduce wycinek godzinę. potok Hello ma czas rozpoczęcia i godzina zakończenia, będące w ciągu jednego dnia od siebie, który wynosi 24 godziny. W związku z tym 24 wycinków wyjściowy zestaw danych są produkowane przez hello potoku.
12. Dodaj hello następującego kodu toohello **Main** metody tooget hello stan wycinek danych hello wyjściowy zestaw danych. W tym przykładzie oczekiwany jest tylko wycinek.

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

13. Dodaj poniższe informacje tooget uruchomić kod dla toohello wycinek danych hello **Main** metody.

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
            }
        );

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

14. Dodaj następujące metody pomocnika używany przez hello hello **Main** toohello metody **Program** klasy.

    > [!NOTE] 
    > Podczas kopiowania i wklejania hello następującego kodu, upewnij się, że hello skopiowanych kod jest w hello sam poziom jako hello metody Main.

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

15. W Eksploratorze rozwiązań hello rozwiń hello projektu (DataFactoryAPITestApp), kliknij prawym przyciskiem myszy **odwołania**i kliknij przycisk **Dodaj odwołanie**. Zaznacz pole wyboru zestawu **System.Configuration**. i kliknij przycisk **OK**.
16. Tworzenie aplikacji konsoli hello. Kliknij przycisk **kompilacji** w hello menu i kliknij przycisk **Kompiluj rozwiązanie**.
17. Upewnij się, że istnieje co najmniej jeden plik w hello **adftutorial** kontenera w magazynie obiektów blob platformy Azure. Jeśli nie, należy utworzyć **Emp.txt** pliku w Notatniku z powitania po zawartości i przekaż go toohello adftutorial kontenera.

    ```
    John, Doe
    Jane, Doe
    ```
18. Uruchom przykładowe hello klikając **debugowania** -> **Rozpocznij debugowanie** menu hello. Po wyświetleniu hello **pierwsze uruchomienie szczegóły wycinka danych**, zaczekaj kilka minut, a następnie naciśnij klawisz **ENTER**.
19. Użyj hello tooverify portalu Azure w tej fabryce danych hello **APITutorialFactory** jest tworzony z następującego artefakty hello:
   * Połączona usługa: **LinkedService_AzureStorage**
   * Zestaw danych: **InputDataset** i **OutputDataset**.
   * Potok: **PipelineBlobSample**
20. Sprawdź, czy hello dwa rekordy pracowników są tworzone w hello **pustych elementów** tabeli w hello określona baza danych Azure SQL.

## <a name="next-steps"></a>Następne kroki
Aby zapoznać się z pełną dokumentacją dotyczącą interfejsu API .NET usługi Data Factory, zobacz [dokumentację interfejsu API .NET usługi Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).

W tym samouczku użyto magazynu obiektów blob platformy Azure jako magazynu danych źródła oraz bazy danych SQL na platformie Azure jako magazynu danych docelowych w operacji kopiowania. Witaj Poniższa tabela zawiera listę magazynów danych obsługiwane jako źródeł i miejsc docelowych przez działanie kopiowania hello: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn o jak magazyn danych toocopy z danych, kliknij łącze hello hello magazynu danych w tabeli hello.

