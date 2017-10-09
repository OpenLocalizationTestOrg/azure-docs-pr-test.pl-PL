---
title: "Zasoby aaaManaging i powiązanych jednostek z zestawu .NET SDK usługi multimediów"
description: "Dowiedz się, jak zasoby toomanage i powiązanych jednostek z hello SDK usługi Media Services dla platformy .NET."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 1bd8fd42-7306-463d-bfe5-f642802f1906
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: juliako
ms.openlocfilehash: 59a8543ffc6f7f30da2c67a6fcae09bc46da7a52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a>Zarządzanie zasobami i jednostek powiązanych z programem Media Services zestawu .NET SDK
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-manage-entities.md)
> * [REST](media-services-rest-manage-entities.md)
> 
> 

W tym temacie pokazano, jak toomanage usługi Azure Media Services jednostki z platformy .NET. 

>[!NOTE]
> Uruchamianie 1 kwietnia 2017 dowolnego rekordu zadania konta starsze niż 90 dni zostaną automatycznie usunięte, wraz z jego skojarzonych rekordów zadań, nawet jeśli hello całkowita liczba rekordów jest poniżej hello maksymalny limit przydziału. Na przykład na 1 kwietnia 2017 dowolnego rekordu zadania konta starsze niż 31 grudnia 2016 r., zostaną automatycznie usunięte. Jeśli potrzebujesz informacji zadania lub zadanie hello tooarchive, można użyć kodu hello opisanych w tym temacie.

## <a name="prerequisites"></a>Wymagania wstępne

Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md). 

## <a name="get-an-asset-reference"></a>Pobierz odwołanie do zasobu
Częstych zadań jest tooget odwołanie tooan istniejący zasób w usłudze Media Services. Hello poniższy przykład kodu pokazuje, jak można uzyskać odwołania do zasobów z kolekcji zasobów hello na powitania serwera obiekt kontekstu, oparte na powitania identyfikatora zasobów następującego kodu przykładzie użyto Linq zapytania tooget tooan istniejących IAsset obiektu odwołania.

    static IAsset GetAsset(string assetId)
    {
        // Use a LINQ Select query tooget an asset.
        var assetInstance =
            from a in _context.Assets
            where a.Id == assetId
            select a;
        // Reference hello asset as an IAsset.
        IAsset asset = assetInstance.FirstOrDefault();

        return asset;
    }

## <a name="list-all-assets"></a>Wyświetl listę wszystkich zasobów
Wraz z rozwojem hello liczby zasobów, masz w magazynie, jest przydatne toolist zasobów. Witaj poniższy przykład kodu pokazuje, jak tooiterate za pośrednictwem hello kolekcji zasobów na powitania serwera kontekstu obiektu. Z każdym zawartości przykładowy kod hello zapisuje także niektóre jego właściwości wartości toohello konsoli. Na przykład poszczególnych zasobów może zawierać wiele plików multimedialnych. Przykładowy kod Hello zapisuje się wszystkie pliki skojarzone z każdym zasobów.

    static void ListAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IAsset asset in _context.Assets)
        {
            // Display hello collection of assets.
            builder.AppendLine("");
            builder.AppendLine("******ASSET******");
            builder.AppendLine("Asset ID: " + asset.Id);
            builder.AppendLine("Name: " + asset.Name);
            builder.AppendLine("==============");
            builder.AppendLine("******ASSET FILES******");

            // Display hello files associated with each asset. 
            foreach (IAssetFile fileItem in asset.AssetFiles)
            {
                builder.AppendLine("Name: " + fileItem.Name);
                builder.AppendLine("Size: " + fileItem.ContentFileSize);
                builder.AppendLine("==============");
            }
        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="get-a-job-reference"></a>Pobierz odwołanie do zadania

Podczas pracy z przetwarzania zadań w kodzie usługi Media Services, często konieczne tooget przez odwołanie tooan istniejące zadanie na podstawie hello identyfikatora poniższy przykład kodu pokazuje sposób tooget tooan odwołania IJob obiekt z kolekcji zadań hello.

Może muszą tooget odwołanie do zadania, podczas uruchamiania długotrwałe zadania kodowania, a muszą stan zadania hello toocheck w wątku. W takich sytuacjach po powrocie z metody hello wprowadzanych przez wątek należy tooretrieve zadania tooa odświeżyć odwołania.

    static IJob GetJob(string jobId)
    {
        // Use a Linq select query tooget an updated 
        // reference by Id. 
        var jobInstance =
            from j in _context.Jobs
            where j.Id == jobId
            select j;
        // Return hello job reference as an Ijob. 
        IJob job = jobInstance.FirstOrDefault();

        return job;
    }

## <a name="list-jobs-and-assets"></a>Lista zadań i zasoby
Ważnym zadaniem powiązane jest toolist zasobów z ich skojarzone zadania w usłudze Media Services. Witaj poniższy przykład kodu pokazuje sposób toolist każdego obiektu IJob, następnie dla każdego zadania, jego wartość właściwości o hello zadania, wszystkie powiązane zadania, wejściowego wszystkie zasoby i wszystkie zasoby w danych wyjściowych. Kod Hello w tym przykładzie może być przydatne w przypadku wielu innych zadań. Na przykład jeśli chcesz toolist hello dane wyjściowe zasobów z co najmniej jednego zadania kodowania, które został przeprowadzony wcześniej ten kod pokazuje, jak tooaccess hello output zasoby. Jeśli masz zawartości wyjściowej tooan odwołanie hello zawartości tooother użytkowników lub aplikacji można następnie dostarczać ją pobrać lub udostępniając adresów URL. 

Aby uzyskać więcej informacji na temat opcji dostarczania zasoby, zobacz [dostarczania zasobów z hello SDK usługi Media Services dla platformy .NET](media-services-deliver-streaming-content.md).

    // List all jobs on hello server, and for each job, also list 
    // all tasks, all input assets, all output assets.

    static void ListJobsAndAssets()
    {
        string waitMessage = "Building hello list. This may take a few "
            + "seconds tooa few minutes depending on how many assets "
            + "you have."
            + Environment.NewLine + Environment.NewLine
            + "Please wait..."
            + Environment.NewLine;
        Console.Write(waitMessage);

        // Create a Stringbuilder toostore hello list that we build. 
        StringBuilder builder = new StringBuilder();

        foreach (IJob job in _context.Jobs)
        {
            // Display hello collection of jobs on hello server.
            builder.AppendLine("");
            builder.AppendLine("******JOB*******");
            builder.AppendLine("Job ID: " + job.Id);
            builder.AppendLine("Name: " + job.Name);
            builder.AppendLine("State: " + job.State);
            builder.AppendLine("Order: " + job.Priority);
            builder.AppendLine("==============");


            // For each job, display hello associated tasks (a job  
            // has one or more tasks). 
            builder.AppendLine("******TASKS*******");
            foreach (ITask task in job.Tasks)
            {
                builder.AppendLine("Task Id: " + task.Id);
                builder.AppendLine("Name: " + task.Name);
                builder.AppendLine("Progress: " + task.Progress);
                builder.AppendLine("Configuration: " + task.Configuration);
                if (task.ErrorDetails != null)
                {
                    builder.AppendLine("Error: " + task.ErrorDetails);
                }
                builder.AppendLine("==============");
            }

            // For each job, display hello list of input media assets.
            builder.AppendLine("******JOB INPUT MEDIA ASSETS*******");
            foreach (IAsset inputAsset in job.InputMediaAssets)
            {

                if (inputAsset != null)
                {
                    builder.AppendLine("Input Asset Id: " + inputAsset.Id);
                    builder.AppendLine("Name: " + inputAsset.Name);
                    builder.AppendLine("==============");
                }
            }

            // For each job, display hello list of output media assets.
            builder.AppendLine("******JOB OUTPUT MEDIA ASSETS*******");
            foreach (IAsset theAsset in job.OutputMediaAssets)
            {
                if (theAsset != null)
                {
                    builder.AppendLine("Output Asset Id: " + theAsset.Id);
                    builder.AppendLine("Name: " + theAsset.Name);
                    builder.AppendLine("==============");
                }
            }

        }

        // Display output in console.
        Console.Write(builder.ToString());
    }

## <a name="list-all-access-policies"></a>Wyświetl listę wszystkich zasad dostępu
W usłudze Media Services można zdefiniować zasadę dostępu zasobów lub jego pliki. Zasady dostępu definiuje uprawnienia hello plik lub zasób (typ dostępu i czas trwania hello). W kodzie usługi Media Services zwykle zdefiniować zasadę dostępu przez utworzenie obiektu IAccessPolicy i kojarzenie go z istniejących zasobów. Następnie można utworzyć obiektu ILocator, który pozwala dostarczyć tooassets bezpośredni dostęp do usług Media Services. Projekt programu Visual Studio Hello dołączona ta seria dokumentacja zawiera kilka przykładów kodu, które pokazują, jak toocreate i przypisz dostępu do zasady i lokalizatorów tooassets.

Witaj, jak po przedstawia przykładowy kod toolist wszystkie zasady dostępu na powitania serwera i pokazuje typ hello uprawnień związanych z każdym. Zasady dostępu w innym tooview wygodny sposób jest toolist wszystkie obiekty ILocator na powitania serwera, a następnie dla każdego lokalizatora można wyświetlić listę jego zasad dostępu skojarzonych za pomocą jego właściwość AccessPolicy.

    static void ListAllPolicies()
    {
        foreach (IAccessPolicy policy in _context.AccessPolicies)
        {
            Console.WriteLine("");
            Console.WriteLine("Name:  " + policy.Name);
            Console.WriteLine("ID:  " + policy.Id);
            Console.WriteLine("Permissions: " + policy.Permissions);
            Console.WriteLine("==============");

        }
    }
    
## <a name="limit-access-policies"></a>Limit zasad dostępu 

>[!NOTE]
> Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy). Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie). 

Na przykład można utworzyć zestawu ogólnych zasad z hello następującego kodu, który można uruchomić tylko raz w aplikacji. Możesz zalogować się plik dziennika tooa identyfikatorów do późniejszego użytku:

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

Następnie należy użyć hello istniejących identyfikatorów w kodzie następująco:

    const string policy1YearId = "nb:pid:UUID:2a4f0104-51a9-4078-ae26-c730f88d35cf";


    // Get hello standard policy for 1 year read only
    var tempPolicyId = from b in _context.AccessPolicies
                       where b.Id == policy1YearId
                       select b;
    IAccessPolicy policy1Year = tempPolicyId.FirstOrDefault();

    // Get hello existing asset
    var tempAsset = from a in _context.Assets
                where a.Id == assetID
                select a;
    IAsset asset = tempAsset.SingleOrDefault();

    ILocator originLocator = _context.Locators.CreateLocator(LocatorType.OnDemandOrigin, asset,
        policy1Year,
        DateTime.UtcNow.AddMinutes(-5));
    Console.WriteLine("hello locator base path is " + originLocator.BaseUri.ToString());

## <a name="list-all-locators"></a>Wyświetl listę wszystkich lokalizatorów
Lokalizator jest adres URL, który zawiera tooaccess bezpośrednią ścieżkę zasób, wraz z zasobów toohello uprawnienia określone przez zasady dostępu skojarzony Lokalizator hello. Każdy zasobów może mieć kolekcji ILocator obiektów skojarzonych z nim na jego właściwość lokalizatorów. Witaj kontekstu serwera ma również lokalizatorów kolekcję, która zawiera wszystkie lokalizatorów.

Witaj Poniższy przykładowy kod zawiera listę wszystkich lokalizatorów na powitania serwera. Dla każdego lokalizatora pokazuje hello identyfikator hello powiązanych zasobów i zasad dostępu. Wyświetla typ hello uprawnienia, datę wygaśnięcia hello i hello pełną ścieżkę toohello zasobów.

Należy pamiętać, że zasób lokalizatora ścieżki tooan tylko podstawowy adres URL toohello zasób. toocreate, które pliki tooindividual bezpośrednią ścieżkę, w którym użytkownik lub aplikacja może przejść do kodu, należy dodać hello określonego pliku ścieżka toohello lokalizatora ścieżki. Aby uzyskać więcej informacji na temat toodo tego, zobacz temat hello [dostarczania zasobów z hello SDK usługi Media Services dla platformy .NET](media-services-deliver-streaming-content.md).

    static void ListAllLocators()
    {
        foreach (ILocator locator in _context.Locators)
        {
            Console.WriteLine("***********");
            Console.WriteLine("Locator Id: " + locator.Id);
            Console.WriteLine("Locator asset Id: " + locator.AssetId);
            Console.WriteLine("Locator access policy Id: " + locator.AccessPolicyId);
            Console.WriteLine("Access policy permissions: " + locator.AccessPolicy.Permissions);
            Console.WriteLine("Locator expiration: " + locator.ExpirationDateTime);
            // hello locator path is hello base or parent path (with included permissions) tooaccess  
            // hello media content of an asset. toocreate a full URL tooa specific media file, take 
            // hello locator path and then append a file name and info as needed.  
            Console.WriteLine("Locator base path: " + locator.Path);
            Console.WriteLine("");
        }
    }

## <a name="enumerating-through-large-collections-of-entities"></a>Wyliczanie za pośrednictwem dużych kolekcjach jednostek
Podczas wykonywania zapytania jednostek, istnieje limit 1000 jednostek zwracane w tym samym czasie, ponieważ publiczny v2 REST ogranicza wyniki too1000 wyników zapytania. Należy toouse Skip i Take podczas wyliczania dużych kolekcjach jednostek. 

Witaj następujących funkcji pętlę wszystkie zadania hello w hello podać konta usługi Media Services. Usługa Media Services zwraca 1000 zadań w kolekcji zadań. Funkcja Hello sprawia, że użycie Skip i zająć się, że toomake który wyliczane są wszystkie zadania (w przypadku, gdy masz więcej niż 1000 zadania konta).

    static void ProcessJobs()
    {
        try
        {

            int skipSize = 0;
            int batchSize = 1000;
            int currentBatch = 0;

            while (true)
            {
                // Loop through all Jobs (1000 at a time) in hello Media Services account
                IQueryable _jobsCollectionQuery = _context.Jobs.Skip(skipSize).Take(batchSize);
                foreach (IJob job in _jobsCollectionQuery)
                {
                    currentBatch++;
                    Console.WriteLine("Processing Job Id:" + job.Id);
                }

                if (currentBatch == batchSize)
                {
                    skipSize += batchSize;
                    currentBatch = 0;
                }
                else
                {
                    break;
                }
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }

## <a name="delete-an-asset"></a>Usuń zasób
Poniższy przykład Hello Usuwa zasób.

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a>Usuwanie zadania
toodelete zadanie, musisz sprawdzić hello stan zadania hello wskazane hello stanu właściwości. Zadania, które zostały zakończone lub anulowane mogą zostać usunięte podczas zadania, które znajdują się w niektórych innych stanów, np. w kolejce, według harmonogramu lub przetwarzania, należy najpierw anulować, a następnie można go usunąć.

Witaj Poniższy przykładowy kod przedstawia metoda usuwania zadania sprawdzania stany zadań, a następnie usuwając podczas hello stanu zostało zakończone lub anulowane. Ten kod jest zależny od hello poprzedniej sekcji, w tym temacie pobierania zadania tooa odwołanie: odwołać zadania.

    static void DeleteJob(string jobId)
    {
        bool jobDeleted = false;

        while (!jobDeleted)
        {
            // Get an updated job reference.  
            IJob job = GetJob(jobId);

            // Check and handle various possible job states. You can 
            // only delete a job whose state is Finished, Error, or Canceled.   
            // You can cancel jobs that are Queued, Scheduled, or Processing,  
            // and then delete after they are canceled.
            switch (job.State)
            {
                case JobState.Finished:
                case JobState.Canceled:
                case JobState.Error:
                    // Job errors should already be logged by polling or event 
                    // handling methods such as CheckJobProgress or StateChanged.
                    // You can also call job.DeleteAsync toodo async deletes.
                    job.Delete();
                    Console.WriteLine("Job has been deleted.");
                    jobDeleted = true;
                    break;
                case JobState.Canceling:
                    Console.WriteLine("Job is cancelling and will be deleted "
                        + "when finished.");
                    Console.WriteLine("Wait while job finishes canceling...");
                    Thread.Sleep(5000);
                    break;
                case JobState.Queued:
                case JobState.Scheduled:
                case JobState.Processing:
                    job.Cancel();
                    Console.WriteLine("Job is scheduled or processing and will "
                        + "be deleted.");
                    break;
                default:
                    break;
            }

        }
    }


## <a name="delete-an-access-policy"></a>Usunięcie zasad dostępu
Witaj Poniższy przykładowy kod przedstawia sposób tooget zasady dostępu tooan odwołania na podstawie zasad Id, a następnie toodelete hello zasad.

    static void DeleteAccessPolicy(string existingPolicyId)
    {
        // toodelete a specific access policy, get a reference toohello policy.  
        // based on hello policy Id passed toohello method.
        var policyInstance =
                from p in _context.AccessPolicies
                where p.Id == existingPolicyId
                select p;
        IAccessPolicy policy = policyInstance.FirstOrDefault();

        policy.Delete();

    }



## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

