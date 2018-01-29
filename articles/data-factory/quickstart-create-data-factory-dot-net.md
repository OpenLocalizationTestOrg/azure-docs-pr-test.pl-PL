---
title: "Tworzenie usługi Azure Data Factory przy użyciu platformy .NET | Microsoft Docs"
description: "Tworzenie usługi Azure Data Factory w celu skopiowania danych z jednej lokalizacji w usłudze Azure Blob Storage do innej lokalizacji w tej samej usłudze Blob Storage."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: 
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: b430f5932bcd54d5e2ab787fb6c4491b48dbc416
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 01/23/2018
---
# <a name="create-a-data-factory-and-pipeline-using-net-sdk"></a>Tworzenie fabryki danych i potoku przy użyciu zestawu SDK .NET
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Wersja 1 — ogólnie dostępna](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Wersja 2 — wersja zapoznawcza](quickstart-create-data-factory-dot-net.md)

Ten samouczek Szybki start opisuje sposób używania zestawu SDK .NET w celu utworzenia usługi Azure Data Factory. Potok tworzony w tej fabryce danych **kopiuje** dane z jednego folderu do innego folderu w usłudze Azure Blob Storage. Aby zapoznać się z samouczkiem dotyczącym **przekształcania** danych za pomocą usługi Azure Data Factory, zobacz [Tutorial: Transform data using Spark (Samouczek: Przekształcanie danych przy użyciu usługi Spark)](transform-data-using-spark.md). 

> [!NOTE]
> Ten artykuł dotyczy wersji 2 usługi Data Factory, która jest obecnie dostępna w wersji zapoznawczej. Jeśli używasz dostępnej ogólnie wersji 1 usługi Data Factory, zobacz artykuł z [wprowadzeniem do usługi Data Factory w wersji 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
>
> Ten artykuł nie zawiera szczegółowego wprowadzenia do usługi Data Factory. Aby zapoznać się z wprowadzeniem do usługi Azure Data Factory, zobacz [Wprowadzenie do usługi Azure Data Factory](introduction.md).

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

## <a name="prerequisites"></a>Wymagania wstępne

### <a name="azure-subscription"></a>Subskrypcja platformy Azure
Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne](https://azure.microsoft.com/free/) konto.

### <a name="azure-roles"></a>Role platformy Azure
Aby utworzyć wystąpienia usługi Data Factory, konto użytkownika używane do logowania się na platformie Azure musi być członkiem roli **współautora** lub **właściciela** albo **administratorem** subskrypcji platformy Azure. W witrynie Azure Portal kliknij swoją **nazwę użytkownika** w prawym górnym rogu i wybierz pozycję **Uprawnienia**, aby wyświetlić uprawnienia, które masz w subskrypcji. Jeśli masz dostęp do wielu subskrypcji, wybierz odpowiednią subskrypcję. Aby uzyskać przykładowe instrukcje dotyczące dodawania użytkownika do roli, zobacz artykuł [Dodawanie ról](../billing/billing-add-change-azure-subscription-administrator.md).

### <a name="azure-storage-account"></a>Konto usługi Azure Storage
W tym samouczku Szybki start używasz konta usługi Azure Storage ogólnego przeznaczenia (w szczególności usługi Blob Storage) jako **źródłowego** i **docelowego** magazynu danych. Jeśli nie masz konta usługi Azure Storage ogólnego przeznaczenia, zobacz [Tworzenie konta magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account), aby uzyskać informacje o jego tworzeniu. 

#### <a name="get-storage-account-name-and-account-key"></a>Pobieranie nazwy konta i klucza konta magazynu
W tym samouczku Szybki start używasz nazwy i klucza konta magazynu platformy Azure. Poniższa procedura obejmuje kroki pobierania nazwy i konta klucza magazynu. 

1. Otwórz przeglądarkę internetową i przejdź do witryny [Azure Portal](https://portal.azure.com). Zaloguj się za pomocą nazwy użytkownika i hasła platformy Azure. 
2. Kliknij pozycję **Więcej usług >** w menu po lewej stronie, odfiltruj przy użyciu słowa kluczowego **Storage** i wybierz pozycję **Konta usługi Storage**.

    ![Wyszukiwanie konta magazynu](media/quickstart-create-data-factory-dot-net/search-storage-account.png)
3. Na liście kont magazynu odfiltruj konto magazynu (w razie potrzeby), a następnie wybierz **swoje konto magazynu**. 
4. Na stronie **Konto magazynu** wybierz pozycję **Klucze dostępu**.

    ![Pobieranie nazwy i klucza konta magazynu](media/quickstart-create-data-factory-dot-net/storage-account-name-key.png)
5. Skopiuj wartości pól **Nazwa konta magazynu** i **klucz1** do schowka. Wklej je do Notatnika lub innego edytora i zapisz plik.  

#### <a name="create-input-folder-and-files"></a>Tworzenie plików i folderu wejściowego
W tej sekcji utworzysz kontener obiektów blob o nazwie **adftutorial** w usłudze Azure Blob Storage. Następnie utwórz folder o nazwie **input** w kontenerze i przekaż przykładowy plik do folderu input. 

1. Na stronie **Konto magazynu** przełącz się do widoku **Przegląd**, a następnie kliknij pozycję **Obiekty blob**. 

    ![Wybieranie opcji Obiekty blob](media/quickstart-create-data-factory-dot-net/select-blobs.png)
2. Na stronie **Usługa Blob** kliknij pozycję **+ Kontener** na pasku narzędzi. 

    ![Przycisk dodawania kontenera](media/quickstart-create-data-factory-dot-net/add-container-button.png)    
3. W oknie dialogowym **Nowy kontener** wprowadź jako nazwę **adftutorial**, a następnie kliknij przycisk **OK**. 

    ![Wprowadzanie nazwy kontenera](media/quickstart-create-data-factory-dot-net/new-container-dialog.png)
4. Kliknij pozycję **adftutorial** na liście kontenerów. 

    ![Wybieranie kontenera](media/quickstart-create-data-factory-dot-net/select-adftutorial-container.png)
1. Na stronie **Kontener** kliknij pozycję **Przekaż** na pasku narzędzi.  

    ![Przycisk Przekaż](media/quickstart-create-data-factory-dot-net/upload-toolbar-button.png)
6. Na stronie **Przekaż obiekt blob** kliknij pozycję **Zaawansowane**.

    ![Klikanie linku Zaawansowane](media/quickstart-create-data-factory-dot-net/upload-blob-advanced.png)
7. Uruchom program **Notatnik** i utwórz plik o nazwie **emp.txt** z następującą zawartością: zapisz go w folderze **c:\ADFv2QuickStartPSH**: (utwórz folder **ADFv2QuickStartPSH**, jeśli jeszcze nie istnieje).
    
    ```
    John, Doe
    Jane, Doe
    ```    
8. W witrynie Azure Portal na stronie **Przekazywanie obiektu blob** wyszukaj i wybierz plik **emp.txt** dla pola **Pliki**. 
9. Wprowadź wartość **input** jako wartość pola **Przekaż do folderu**. 

    ![Ustawienia przekazywania obiektu blob](media/quickstart-create-data-factory-dot-net/upload-blob-settings.png)    
10. Upewnij się, że wybrano folder **input** i plik **emp.txt**, a następnie kliknij przycisk **Przekaż**.
11. Na liście powinien pojawić się plik **emp.txt** i stan przekazywania. 
12. Zamknij stronę **Przekazywanie obiektu blob**, klikając przycisk **X** w rogu strony. 

    ![Zamykanie strony przekazywania obiektu blob](media/quickstart-create-data-factory-dot-net/close-upload-blob.png)
1. Zachowaj otwartą stronę **kontenera**. Będzie ona używana do weryfikowania danych wyjściowych na końcu tego samouczka Szybki start.

### <a name="visual-studio"></a>Visual Studio
W przewodniku w tym artykule jest używany program Visual Studio 2017. Możesz też użyć programu Visual Studio 2013 lub 2015.

### <a name="azure-net-sdk"></a>Zestaw Azure .NET SDK
Pobierz i zainstaluj zestaw [Azure .NET SDK](http://azure.microsoft.com/downloads/) na maszynie.

### <a name="create-an-application-in-azure-active-directory"></a>Tworzenie aplikacji w usłudze Azure Active Directory
Postępuj zgodnie z instrukcjami przedstawionymi w [tym artykule](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application), aby wykonać następujące zadania: 

1. **Utworzenie aplikacji usługi Azure Active Directory**. Utwórz aplikację w usłudze Azure Active Directory reprezentującą aplikację platformy .NET tworzoną w tym samouczku. W przypadku adresu URL logowania możesz podać fikcyjny adres URL, jak pokazano w artykule (`https://contoso.org/exampleapp`).
2. Pobierz **identyfikator aplikacji** i **klucz uwierzytelniania****, postępując zgodnie z instrukcjami przedstawionymi w sekcji **Pobieranie identyfikatora aplikacji i klucza uwierzytelniania** w artykule. Zanotuj te wartości, których użyjesz w dalszej części tego samouczka. 
3. Pobierz **identyfikator dzierżawy**, postępując zgodnie z instrukcjami przedstawionymi w sekcji **Pobieranie identyfikatora dzierżawy** w artykule. Zanotuj tę wartość. 
4. Przypisz aplikację do roli **Współautor** na poziomie subskrypcji, aby aplikacja mogła tworzyć fabryki danych w ramach subskrypcji. Postępuj zgodnie z instrukcjami przedstawionymi w sekcji **Przypisywanie aplikacji do roli** w artykule. 

## <a name="create-a-visual-studio-project"></a>Tworzenie projektu programu Visual Studio

Za pomocą programu Visual Studio 2013/2015/2017 utwórz aplikację konsolową .NET C#.

1. Uruchom program **Visual Studio**.
2. Kliknij pozycję **Plik**, wskaż polecenie **Nowy** i kliknij pozycję **Projekt**.
3. Wybierz pozycję **Visual C#** -> **Aplikacja konsolowa (.NET Framework)** z listy typów projektów po prawej stronie. Wymagana jest platforma .NET w wersji 4.5.2 lub nowszej.
4. Wprowadź **ADFv2QuickStart** w polu nazwy.
5. Kliknij przycisk **OK**, aby utworzyć projekt.

## <a name="install-nuget-packages"></a>Instalowanie pakietów NuGet

1. Kliknij pozycję **Narzędzia** -> **Menedżer pakietów NuGet** -> **Konsola menedżera pakietów**.
2. W oknie **Konsola menedżera pakietów** uruchom następujące polecenia, aby zainstalować pakiety:

    ```
    Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
    Install-Package Microsoft.Azure.Management.ResourceManager -Prerelease
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory

    ```

## <a name="create-a-data-factory-client"></a>Tworzenie klienta fabryki danych

1. Otwórz plik **Program.cs**, a następnie dołącz poniższe instrukcje, aby dodać odwołania do przestrzeni nazw.

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using Microsoft.Rest;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.DataFactory;
    using Microsoft.Azure.Management.DataFactory.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    ```

2. Dodaj do metody **Main** następujący kod, który określa zmienne. Zastąp symbole zastępcze własnymi wartościami. Obecnie usługa Data Factory w wersji 2 umożliwia tworzenie fabryk danych tylko w regionach Wschodnie stany USA, Wschodnie stany USA 2 i Europa Zachodnia. Magazyny danych (Azure Storage, Azure SQL Database itp.) i jednostki obliczeniowe (HDInsight itp.) używane przez fabrykę danych mogą mieścić się w innych regionach.

    ```csharp
    // Set variables
    string tenantID = "<your tenant ID>";
    string applicationId = "<your application ID>";
    string authenticationKey = "<your authentication key for the application>";
    string subscriptionId = "<your subscription ID where the data factory resides>";
    string resourceGroup = "<your resource group where the data factory resides>";
    string region = "East US 2";
    string dataFactoryName = "<specify the name of data factory to create. It must be globally unique.>";
    string storageAccount = "<your storage account name to copy data>";
    string storageKey = "<your storage account key>";
    // specify the container and input folder from which all files need to be copied to the output folder. 
    string inputBlobPath = "<the path to existing blob(s) to copy data from, e.g. containername/foldername>";
    //specify the contains and output folder where the files are copied
    string outputBlobPath = "<the blob path to copy data to, e.g. containername/foldername>";

    string storageLinkedServiceName = "AzureStorageLinkedService";  // name of the Azure Storage linked service
    string blobDatasetName = "BlobDataset";             // name of the blob dataset
    string pipelineName = "Adfv2QuickStartPipeline";    // name of the pipeline
    ```

3. Dodaj do metody **Main** poniższy kod, który tworzy wystąpienie klasy **DataFactoryManagementClient**. Ten obiekt jest używany do tworzenia fabryki danych, połączonej usługi, zestawów danych i potoku. Umożliwia on również monitorowanie szczegółów uruchomienia potoku.

    ```csharp
    // Authenticate and create a data factory management client
    var context = new AuthenticationContext("https://login.windows.net/" + tenantID);
    ClientCredential cc = new ClientCredential(applicationId, authenticationKey);
    AuthenticationResult result = context.AcquireTokenAsync("https://management.azure.com/", cc).Result;
    ServiceClientCredentials cred = new TokenCredentials(result.AccessToken);
    var client = new DataFactoryManagementClient(cred) { SubscriptionId = subscriptionId };
    ```

## <a name="create-a-data-factory"></a>Tworzenie fabryki danych

Dodaj do metody **Main** poniższy kod, który tworzy **fabrykę danych**. 

```csharp
// Create a data factory
Console.WriteLine("Creating data factory " + dataFactoryName + "...");
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
Console.WriteLine(SafeJsonConvert.SerializeObject(dataFactory, client.SerializationSettings));

while (client.Factories.Get(resourceGroup, dataFactoryName).ProvisioningState == "PendingCreation")
{
    System.Threading.Thread.Sleep(1000);
}
```

## <a name="create-a-linked-service"></a>Tworzenie usługi połączonej

Dodaj do metody **Main** poniższy kod, który tworzy **połączoną usługę Azure Storage**.

Połączone usługi tworzy się w fabryce danych w celu połączenia magazynów danych i usług obliczeniowych z fabryką danych. W tym samouczku Szybki start musisz utworzyć tylko jedną połączoną usługę Azure Storage zarówno dla źródła kopii, jak i ujścia magazynu o nazwie „AzureStorageLinkedService” w przykładzie.

```csharp
// Create an Azure Storage linked service
Console.WriteLine("Creating linked service " + storageLinkedServiceName + "...");

LinkedServiceResource storageLinkedService = new LinkedServiceResource(
    new AzureStorageLinkedService
    {
        ConnectionString = new SecureString("DefaultEndpointsProtocol=https;AccountName=" + storageAccount + ";AccountKey=" + storageKey)
    }
);
client.LinkedServices.CreateOrUpdate(resourceGroup, dataFactoryName, storageLinkedServiceName, storageLinkedService);
Console.WriteLine(SafeJsonConvert.SerializeObject(storageLinkedService, client.SerializationSettings));
```

## <a name="create-a-dataset"></a>Tworzenie zestawu danych

Dodaj do metody **Main** poniższy kod, który tworzy **zestaw danych obiektu blob platformy Azure**.

Zdefiniuj zestaw danych, który reprezentuje dane do skopiowania ze źródła do ujścia. W tym przykładzie ten zestaw danych obiektu blob odwołuje się do połączonej usługi Azure Storage utworzonej w poprzednim kroku. Zestaw danych przyjmuje parametr, którego wartość jest ustawiana w działaniu wykorzystującym zestaw danych. Parametr służy do tworzenia wartości „folderPath” wskazującej miejsce, gdzie znajdują się/są przechowywane dane.

```csharp
// Create a Azure Blob dataset
Console.WriteLine("Creating dataset " + blobDatasetName + "...");
DatasetResource blobDataset = new DatasetResource(
    new AzureBlobDataset
    {
        LinkedServiceName = new LinkedServiceReference
        {
            ReferenceName = storageLinkedServiceName
        },
        FolderPath = new Expression { Value = "@{dataset().path}" },
        Parameters = new Dictionary<string, ParameterSpecification>
        {
            { "path", new ParameterSpecification { Type = ParameterType.String } }

        }
    }
);
client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, blobDatasetName, blobDataset);
Console.WriteLine(SafeJsonConvert.SerializeObject(blobDataset, client.SerializationSettings));
```

## <a name="create-a-pipeline"></a>Tworzenie potoku

Dodaj do metody **Main** poniższy kod, który tworzy **potok z działaniem kopiowania**.

W niniejszym przykładzie ten potok zawiera jedno działanie i pobiera dwa parametry — ścieżkę wejściowego obiektu blob i ścieżkę wyjściowego obiektu blob. Wartości tych parametrów są ustawiane w chwili wyzwolenia/uruchomienia potoku. Działanie kopiowania dotyczy tego samego zestawu danych obiektu blob, który został utworzony w poprzednim kroku jako wejście i wyjście. W przypadku użycia zestawu danych jako zestawu danych wejściowych określana jest ścieżka wejściowa. Natomiast w przypadku użycia zestawu danych jako zestawu danych wyjściowych określana jest ścieżka wyjściowa. 

```csharp
// Create a pipeline with a copy activity
Console.WriteLine("Creating pipeline " + pipelineName + "...");
PipelineResource pipeline = new PipelineResource
{
    Parameters = new Dictionary<string, ParameterSpecification>
    {
        { "inputPath", new ParameterSpecification { Type = ParameterType.String } },
        { "outputPath", new ParameterSpecification { Type = ParameterType.String } }
    },
    Activities = new List<Activity>
    {
        new CopyActivity
        {
            Name = "CopyFromBlobToBlob",
            Inputs = new List<DatasetReference>
            {
                new DatasetReference()
                {
                    ReferenceName = blobDatasetName,
                    Parameters = new Dictionary<string, object>
                    {
                        { "path", "@pipeline().parameters.inputPath" }
                    }
                }
            },
            Outputs = new List<DatasetReference>
            {
                new DatasetReference
                {
                    ReferenceName = blobDatasetName,
                    Parameters = new Dictionary<string, object>
                    {
                        { "path", "@pipeline().parameters.outputPath" }
                    }
                }
            },
            Source = new BlobSource { },
            Sink = new BlobSink { }
        }
    }
};
client.Pipelines.CreateOrUpdate(resourceGroup, dataFactoryName, pipelineName, pipeline);
Console.WriteLine(SafeJsonConvert.SerializeObject(pipeline, client.SerializationSettings));
```

## <a name="create-a-pipeline-run"></a>Tworzenie uruchomienia potoku

Dodaj do metody **Main** poniższy kod, który **wyzwala uruchomienie potoku**.

Ten kod ustawia też wartości parametrów **inputPath** i **outputPath** określonych w potoku za pomocą rzeczywistych wartości ścieżek źródła i ujścia obiektu blob.

```csharp
// Create a pipeline run
Console.WriteLine("Creating pipeline run...");
Dictionary<string, object> parameters = new Dictionary<string, object>
{
    { "inputPath", inputBlobPath },
    { "outputPath", outputBlobPath }
};
CreateRunResponse runResponse = client.Pipelines.CreateRunWithHttpMessagesAsync(resourceGroup, dataFactoryName, pipelineName, parameters).Result.Body;
Console.WriteLine("Pipeline run ID: " + runResponse.RunId);
```

## <a name="monitor-a-pipeline-run"></a>Monitorowanie uruchomienia potoku

1. Dodaj do metody **Main** poniższy kod, aby stale sprawdzać stan do momentu zakończenia kopiowania danych.

    ```csharp
    // Monitor the pipeline run
    Console.WriteLine("Checking pipeline run status...");
    PipelineRun pipelineRun;
    while (true)
    {
        pipelineRun = client.PipelineRuns.Get(resourceGroup, dataFactoryName, runResponse.RunId);
        Console.WriteLine("Status: " + pipelineRun.Status);
        if (pipelineRun.Status == "InProgress")
            System.Threading.Thread.Sleep(15000);
        else
            break;
    }
    ```

2. Dodaj do metody **Main** poniższy kod, który pobiera szczegóły uruchomienia działania kopiowania, na przykład rozmiar odczytanych/zapisanych danych.

    ```csharp
    // Check the copy activity run details
    Console.WriteLine("Checking copy activity run details...");
   
    List<ActivityRun> activityRuns = client.ActivityRuns.ListByPipelineRun(
    resourceGroup, dataFactoryName, runResponse.RunId, DateTime.UtcNow.AddMinutes(-10), DateTime.UtcNow.AddMinutes(10)).ToList(); 
    if (pipelineRun.Status == "Succeeded")
        Console.WriteLine(activityRuns.First().Output);
    else
        Console.WriteLine(activityRuns.First().Error);
    Console.WriteLine("\nPress any key to exit...");
    Console.ReadKey();
    ```

## <a name="run-the-code"></a>Uruchamianie kodu

Skompiluj i uruchom aplikację, a następnie zweryfikuj wykonywanie potoku.

Konsola wypisuje postęp tworzenia fabryki danych, połączonej usługi, zestawów danych, potoku i uruchomienia potoku. Następnie sprawdza stan uruchomienia potoku. Poczekaj na wyświetlenie szczegółów uruchomienia działania kopiowania z rozmiarem odczytanych/zapisanych danych. Następnie sprawdź przy użyciu narzędzi, takich jak [eksplorator usługi Azure Storage](https://azure.microsoft.com/features/storage-explorer/), czy obiekty blob zostały skopiowane do lokalizacji „outputBlobPath” z lokalizacji „inputBlobPath”, jak określono w zmiennych.

### <a name="sample-output"></a>Przykładowe dane wyjściowe: 
```json
Creating data factory SPv2Factory0907...
{
  "identity": {
    "type": "SystemAssigned"
  },
  "location": "East US"
}
Creating linked service AzureStorageLinkedService...
{
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": {
        "value": "DefaultEndpointsProtocol=https;AccountName=<storageAccountName>;AccountKey=<storageAccountKey>",
        "type": "SecureString"
      }
    }
  }
}
Creating dataset BlobDataset...
{
  "properties": {
    "type": "AzureBlob",
    "typeProperties": {
      "folderPath": {
        "value": "@{dataset().path}",
        "type": "Expression"
      }
    },
    "linkedServiceName": {
      "referenceName": "AzureStorageLinkedService",
      "type": "LinkedServiceReference"
    },
    "parameters": {
      "path": {
        "type": "String"
      }
    }
  }
}
Creating pipeline Adfv2QuickStartPipeline...
{
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
        "inputs": [
          {
            "referenceName": "BlobDataset",
            "parameters": {
              "path": "@pipeline().parameters.inputPath"
            },
            "type": "DatasetReference"
          }
        ],
        "outputs": [
          {
            "referenceName": "BlobDataset",
            "parameters": {
              "path": "@pipeline().parameters.outputPath"
            },
            "type": "DatasetReference"
          }
        ],
        "name": "CopyFromBlobToBlob"
      }
    ],
    "parameters": {
      "inputPath": {
        "type": "String"
      },
      "outputPath": {
        "type": "String"
      }
    }
  }
}
Creating pipeline run...
Pipeline run ID: 308d222d-3858-48b1-9e66-acd921feaa09
Checking pipeline run status...
Status: InProgress
Status: InProgress
Checking copy activity run details...
{
    "dataRead": 331452208,
    "dataWritten": 331452208,
    "copyDuration": 23,
    "throughput": 14073.209,
    "errors": [],
    "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (West US)",
    "usedCloudDataMovementUnits": 2,
    "billedDuration": 23
}

Press any key to exit...
```

## <a name="verify-the-output"></a>Sprawdzanie danych wyjściowych
Potok automatycznie tworzy folder wyjściowy w kontenerze obiektów blob adftutorial. Następnie kopiuje plik emp.txt z folderu wejściowego do folderu wyjściowego. 

1. W witrynie Azure Portal na stronie kontenera **adftutorial** kliknij przycisk **Odśwież**, aby wyświetlić folder wyjściowy. 
    
    ![Odświeżanie](media/quickstart-create-data-factory-dot-net/output-refresh.png)
2. Kliknij folder **dane wyjściowe** na liście folderów. 
2. Upewnij się, że plik **emp.txt** jest kopiowany do folderu wyjściowego. 

    ![Odświeżanie](media/quickstart-create-data-factory-dot-net/output-file.png)

## <a name="clean-up-resources"></a>Oczyszczanie zasobów
Aby programowo usunąć fabrykę danych, dodaj następujące wiersze kodu do programu: 

```csharp
            Console.WriteLine("Deleting the data factory");
            client.Factories.Delete(resourceGroup, dataFactoryName);
```

## <a name="next-steps"></a>Następne kroki
Potok w tym przykładzie kopiuje dane z jednej lokalizacji do innej lokalizacji w usłudze Azure Blob Storage. Zapoznaj się z [samouczkami](tutorial-copy-data-dot-net.md), aby dowiedzieć się więcej o korzystaniu z usługi Data Factory w dalszych scenariuszach. 
