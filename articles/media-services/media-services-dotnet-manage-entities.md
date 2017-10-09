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
# <a name="managing-assets-and-related-entities-with-media-services-net-sdk"></a><span data-ttu-id="1522e-103">Zarządzanie zasobami i jednostek powiązanych z programem Media Services zestawu .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1522e-103">Managing Assets and Related Entities with Media Services .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1522e-104">.NET</span><span class="sxs-lookup"><span data-stu-id="1522e-104">.NET</span></span>](media-services-dotnet-manage-entities.md)
> * [<span data-ttu-id="1522e-105">REST</span><span class="sxs-lookup"><span data-stu-id="1522e-105">REST</span></span>](media-services-rest-manage-entities.md)
> 
> 

<span data-ttu-id="1522e-106">W tym temacie pokazano, jak toomanage usługi Azure Media Services jednostki z platformy .NET.</span><span class="sxs-lookup"><span data-stu-id="1522e-106">This topic shows how toomanage Azure Media Services entities with .NET.</span></span> 

>[!NOTE]
> <span data-ttu-id="1522e-107">Uruchamianie 1 kwietnia 2017 dowolnego rekordu zadania konta starsze niż 90 dni zostaną automatycznie usunięte, wraz z jego skojarzonych rekordów zadań, nawet jeśli hello całkowita liczba rekordów jest poniżej hello maksymalny limit przydziału.</span><span class="sxs-lookup"><span data-stu-id="1522e-107">Starting April 1, 2017, any Job record in your account older than 90 days will be automatically deleted, along with its associated Task records, even if hello total number of records is below hello maximum quota.</span></span> <span data-ttu-id="1522e-108">Na przykład na 1 kwietnia 2017 dowolnego rekordu zadania konta starsze niż 31 grudnia 2016 r., zostaną automatycznie usunięte.</span><span class="sxs-lookup"><span data-stu-id="1522e-108">For example, on April 1, 2017, any Job record in your account older than December 31, 2016, will be automatically deleted.</span></span> <span data-ttu-id="1522e-109">Jeśli potrzebujesz informacji zadania lub zadanie hello tooarchive, można użyć kodu hello opisanych w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="1522e-109">If you need tooarchive hello job/task information, you can use hello code described in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1522e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1522e-110">Prerequisites</span></span>

<span data-ttu-id="1522e-111">Konfigurowanie środowiska projektowego i wypełnić plik app.config hello o informacje dotyczące połączenia, zgodnie z opisem w [tworzenia usługi Media Services z platformą .NET](media-services-dotnet-how-to-use.md).</span><span class="sxs-lookup"><span data-stu-id="1522e-111">Set up your development environment and populate hello app.config file with connection information, as described in [Media Services development with .NET](media-services-dotnet-how-to-use.md).</span></span> 

## <a name="get-an-asset-reference"></a><span data-ttu-id="1522e-112">Pobierz odwołanie do zasobu</span><span class="sxs-lookup"><span data-stu-id="1522e-112">Get an Asset Reference</span></span>
<span data-ttu-id="1522e-113">Częstych zadań jest tooget odwołanie tooan istniejący zasób w usłudze Media Services.</span><span class="sxs-lookup"><span data-stu-id="1522e-113">A frequent task is tooget a reference tooan existing asset in Media Services.</span></span> <span data-ttu-id="1522e-114">Hello poniższy przykład kodu pokazuje, jak można uzyskać odwołania do zasobów z kolekcji zasobów hello na powitania serwera obiekt kontekstu, oparte na powitania identyfikatora zasobów następującego kodu przykładzie użyto Linq zapytania tooget tooan istniejących IAsset obiektu odwołania.</span><span class="sxs-lookup"><span data-stu-id="1522e-114">hello following code example shows how you can get an asset reference from hello Assets collection on hello server context object, based on an asset Id. hello following code example uses a Linq query tooget a reference tooan existing IAsset object.</span></span>

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

## <a name="list-all-assets"></a><span data-ttu-id="1522e-115">Wyświetl listę wszystkich zasobów</span><span class="sxs-lookup"><span data-stu-id="1522e-115">List All Assets</span></span>
<span data-ttu-id="1522e-116">Wraz z rozwojem hello liczby zasobów, masz w magazynie, jest przydatne toolist zasobów.</span><span class="sxs-lookup"><span data-stu-id="1522e-116">As hello number of assets you have in storage grows, it is helpful toolist your assets.</span></span> <span data-ttu-id="1522e-117">Witaj poniższy przykład kodu pokazuje, jak tooiterate za pośrednictwem hello kolekcji zasobów na powitania serwera kontekstu obiektu.</span><span class="sxs-lookup"><span data-stu-id="1522e-117">hello following code example shows how tooiterate through hello Assets collection on hello server context object.</span></span> <span data-ttu-id="1522e-118">Z każdym zawartości przykładowy kod hello zapisuje także niektóre jego właściwości wartości toohello konsoli.</span><span class="sxs-lookup"><span data-stu-id="1522e-118">With each asset, hello code example also writes some of its property values toohello console.</span></span> <span data-ttu-id="1522e-119">Na przykład poszczególnych zasobów może zawierać wiele plików multimedialnych.</span><span class="sxs-lookup"><span data-stu-id="1522e-119">For example, each asset can contain many media files.</span></span> <span data-ttu-id="1522e-120">Przykładowy kod Hello zapisuje się wszystkie pliki skojarzone z każdym zasobów.</span><span class="sxs-lookup"><span data-stu-id="1522e-120">hello code example writes out all files associated with each asset.</span></span>

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

## <a name="get-a-job-reference"></a><span data-ttu-id="1522e-121">Pobierz odwołanie do zadania</span><span class="sxs-lookup"><span data-stu-id="1522e-121">Get a Job Reference</span></span>

<span data-ttu-id="1522e-122">Podczas pracy z przetwarzania zadań w kodzie usługi Media Services, często konieczne tooget przez odwołanie tooan istniejące zadanie na podstawie hello identyfikatora poniższy przykład kodu pokazuje sposób tooget tooan odwołania IJob obiekt z kolekcji zadań hello.</span><span class="sxs-lookup"><span data-stu-id="1522e-122">When you work with processing tasks in Media Services code, you often need tooget a reference tooan existing job based on an Id. hello following code example shows how tooget a reference tooan IJob object from hello Jobs collection.</span></span>

<span data-ttu-id="1522e-123">Może muszą tooget odwołanie do zadania, podczas uruchamiania długotrwałe zadania kodowania, a muszą stan zadania hello toocheck w wątku.</span><span class="sxs-lookup"><span data-stu-id="1522e-123">You may need tooget a job reference when starting a long-running encoding job, and need toocheck hello job status on a thread.</span></span> <span data-ttu-id="1522e-124">W takich sytuacjach po powrocie z metody hello wprowadzanych przez wątek należy tooretrieve zadania tooa odświeżyć odwołania.</span><span class="sxs-lookup"><span data-stu-id="1522e-124">In cases like this, when hello method returns from a thread, you need tooretrieve a refreshed reference tooa job.</span></span>

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

## <a name="list-jobs-and-assets"></a><span data-ttu-id="1522e-125">Lista zadań i zasoby</span><span class="sxs-lookup"><span data-stu-id="1522e-125">List Jobs and Assets</span></span>
<span data-ttu-id="1522e-126">Ważnym zadaniem powiązane jest toolist zasobów z ich skojarzone zadania w usłudze Media Services.</span><span class="sxs-lookup"><span data-stu-id="1522e-126">An important related task is toolist assets with their associated job in Media Services.</span></span> <span data-ttu-id="1522e-127">Witaj poniższy przykład kodu pokazuje sposób toolist każdego obiektu IJob, następnie dla każdego zadania, jego wartość właściwości o hello zadania, wszystkie powiązane zadania, wejściowego wszystkie zasoby i wszystkie zasoby w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="1522e-127">hello following code example shows you how toolist each IJob object, and then for each job, it displays properties about hello job, all related tasks, all input assets, and all output assets.</span></span> <span data-ttu-id="1522e-128">Kod Hello w tym przykładzie może być przydatne w przypadku wielu innych zadań.</span><span class="sxs-lookup"><span data-stu-id="1522e-128">hello code in this example can be useful for numerous other tasks.</span></span> <span data-ttu-id="1522e-129">Na przykład jeśli chcesz toolist hello dane wyjściowe zasobów z co najmniej jednego zadania kodowania, które został przeprowadzony wcześniej ten kod pokazuje, jak tooaccess hello output zasoby.</span><span class="sxs-lookup"><span data-stu-id="1522e-129">For example, if you want toolist hello output assets from one or more encoding jobs that you ran previously, this code shows how tooaccess hello output assets.</span></span> <span data-ttu-id="1522e-130">Jeśli masz zawartości wyjściowej tooan odwołanie hello zawartości tooother użytkowników lub aplikacji można następnie dostarczać ją pobrać lub udostępniając adresów URL.</span><span class="sxs-lookup"><span data-stu-id="1522e-130">When you have a reference tooan output asset, you can then deliver hello content tooother users or applications by downloading it, or providing URLs.</span></span> 

<span data-ttu-id="1522e-131">Aby uzyskać więcej informacji na temat opcji dostarczania zasoby, zobacz [dostarczania zasobów z hello SDK usługi Media Services dla platformy .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="1522e-131">For more information on options for delivering assets, see [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="list-all-access-policies"></a><span data-ttu-id="1522e-132">Wyświetl listę wszystkich zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="1522e-132">List all Access Policies</span></span>
<span data-ttu-id="1522e-133">W usłudze Media Services można zdefiniować zasadę dostępu zasobów lub jego pliki.</span><span class="sxs-lookup"><span data-stu-id="1522e-133">In Media Services, you can define an access policy on an asset or its files.</span></span> <span data-ttu-id="1522e-134">Zasady dostępu definiuje uprawnienia hello plik lub zasób (typ dostępu i czas trwania hello).</span><span class="sxs-lookup"><span data-stu-id="1522e-134">An access policy defines hello permissions for a file or an asset (what type of access, and hello duration).</span></span> <span data-ttu-id="1522e-135">W kodzie usługi Media Services zwykle zdefiniować zasadę dostępu przez utworzenie obiektu IAccessPolicy i kojarzenie go z istniejących zasobów.</span><span class="sxs-lookup"><span data-stu-id="1522e-135">In your Media Services code, you typically define an access policy by creating an IAccessPolicy object and then associating it with an existing asset.</span></span> <span data-ttu-id="1522e-136">Następnie można utworzyć obiektu ILocator, który pozwala dostarczyć tooassets bezpośredni dostęp do usług Media Services.</span><span class="sxs-lookup"><span data-stu-id="1522e-136">Then you create a ILocator object, which lets you provide direct access tooassets in Media Services.</span></span> <span data-ttu-id="1522e-137">Projekt programu Visual Studio Hello dołączona ta seria dokumentacja zawiera kilka przykładów kodu, które pokazują, jak toocreate i przypisz dostępu do zasady i lokalizatorów tooassets.</span><span class="sxs-lookup"><span data-stu-id="1522e-137">hello Visual Studio project that accompanies this documentation series contains several code examples that show how toocreate and assign access policies and locators tooassets.</span></span>

<span data-ttu-id="1522e-138">Witaj, jak po przedstawia przykładowy kod toolist wszystkie zasady dostępu na powitania serwera i pokazuje typ hello uprawnień związanych z każdym.</span><span class="sxs-lookup"><span data-stu-id="1522e-138">hello following code example shows how toolist all access policies on hello server, and shows hello type of permissions associated with each.</span></span> <span data-ttu-id="1522e-139">Zasady dostępu w innym tooview wygodny sposób jest toolist wszystkie obiekty ILocator na powitania serwera, a następnie dla każdego lokalizatora można wyświetlić listę jego zasad dostępu skojarzonych za pomocą jego właściwość AccessPolicy.</span><span class="sxs-lookup"><span data-stu-id="1522e-139">Another useful way tooview access policies is toolist all ILocator objects on hello server, and then for each locator, you can list its associated access policy by using its AccessPolicy property.</span></span>

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
    
## <a name="limit-access-policies"></a><span data-ttu-id="1522e-140">Limit zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="1522e-140">Limit Access Policies</span></span> 

>[!NOTE]
> <span data-ttu-id="1522e-141">Limit różnych zasad usługi AMS wynosi 1 000 000 (na przykład zasad lokalizatorów lub ContentKeyAuthorizationPolicy).</span><span class="sxs-lookup"><span data-stu-id="1522e-141">There is a limit of 1,000,000 policies for different AMS policies (for example, for Locator policy or ContentKeyAuthorizationPolicy).</span></span> <span data-ttu-id="1522e-142">Należy używać hello tym samym identyfikatorze zasad, jeśli używasz zawsze hello sam dni / dostęp uprawnień, na przykład zasady dla lokalizatorów, które są przeznaczone tooremain w miejscu przez długi czas (zasady — przekazywanie).</span><span class="sxs-lookup"><span data-stu-id="1522e-142">You should use hello same policy ID if you are always using hello same days / access permissions, for example, policies for locators that are intended tooremain in place for a long time (non-upload policies).</span></span> 

<span data-ttu-id="1522e-143">Na przykład można utworzyć zestawu ogólnych zasad z hello następującego kodu, który można uruchomić tylko raz w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1522e-143">For example, you can create a generic set of policies with hello following code that would only run one time in your application.</span></span> <span data-ttu-id="1522e-144">Możesz zalogować się plik dziennika tooa identyfikatorów do późniejszego użytku:</span><span class="sxs-lookup"><span data-stu-id="1522e-144">You can log IDs tooa log file for later use:</span></span>

    double year = 365.25;
    double week = 7;
    IAccessPolicy policyYear = _context.AccessPolicies.Create("One Year", TimeSpan.FromDays(year), AccessPermissions.Read);
    IAccessPolicy policy100Year = _context.AccessPolicies.Create("Hundred Years", TimeSpan.FromDays(year * 100), AccessPermissions.Read);
    IAccessPolicy policyWeek = _context.AccessPolicies.Create("One Week", TimeSpan.FromDays(week), AccessPermissions.Read);

    Console.WriteLine("One year policy ID is: " + policyYear.Id);
    Console.WriteLine("100 year policy ID is: " + policy100Year.Id);
    Console.WriteLine("One week policy ID is: " + policyWeek.Id);

<span data-ttu-id="1522e-145">Następnie należy użyć hello istniejących identyfikatorów w kodzie następująco:</span><span class="sxs-lookup"><span data-stu-id="1522e-145">Then, you can use hello existing IDs in your code like this:</span></span>

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

## <a name="list-all-locators"></a><span data-ttu-id="1522e-146">Wyświetl listę wszystkich lokalizatorów</span><span class="sxs-lookup"><span data-stu-id="1522e-146">List All Locators</span></span>
<span data-ttu-id="1522e-147">Lokalizator jest adres URL, który zawiera tooaccess bezpośrednią ścieżkę zasób, wraz z zasobów toohello uprawnienia określone przez zasady dostępu skojarzony Lokalizator hello.</span><span class="sxs-lookup"><span data-stu-id="1522e-147">A locator is a URL that provides a direct path tooaccess an asset, along with permissions toohello asset as defined by hello locator's associated access policy.</span></span> <span data-ttu-id="1522e-148">Każdy zasobów może mieć kolekcji ILocator obiektów skojarzonych z nim na jego właściwość lokalizatorów.</span><span class="sxs-lookup"><span data-stu-id="1522e-148">Each asset can have a collection of ILocator objects associated with it on its Locators property.</span></span> <span data-ttu-id="1522e-149">Witaj kontekstu serwera ma również lokalizatorów kolekcję, która zawiera wszystkie lokalizatorów.</span><span class="sxs-lookup"><span data-stu-id="1522e-149">hello server context also has a Locators collection that contains all locators.</span></span>

<span data-ttu-id="1522e-150">Witaj Poniższy przykładowy kod zawiera listę wszystkich lokalizatorów na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="1522e-150">hello following code example lists all locators on hello server.</span></span> <span data-ttu-id="1522e-151">Dla każdego lokalizatora pokazuje hello identyfikator hello powiązanych zasobów i zasad dostępu.</span><span class="sxs-lookup"><span data-stu-id="1522e-151">For each locator, it shows hello Id for hello related asset and access policy.</span></span> <span data-ttu-id="1522e-152">Wyświetla typ hello uprawnienia, datę wygaśnięcia hello i hello pełną ścieżkę toohello zasobów.</span><span class="sxs-lookup"><span data-stu-id="1522e-152">It also displays hello type of permissions, hello expiration date, and hello full path toohello asset.</span></span>

<span data-ttu-id="1522e-153">Należy pamiętać, że zasób lokalizatora ścieżki tooan tylko podstawowy adres URL toohello zasób.</span><span class="sxs-lookup"><span data-stu-id="1522e-153">Note that a locator path tooan asset is only a base URL toohello asset.</span></span> <span data-ttu-id="1522e-154">toocreate, które pliki tooindividual bezpośrednią ścieżkę, w którym użytkownik lub aplikacja może przejść do kodu, należy dodać hello określonego pliku ścieżka toohello lokalizatora ścieżki.</span><span class="sxs-lookup"><span data-stu-id="1522e-154">toocreate a direct path tooindividual files that a user or application could browse to, your code must add hello specific file path toohello locator path.</span></span> <span data-ttu-id="1522e-155">Aby uzyskać więcej informacji na temat toodo tego, zobacz temat hello [dostarczania zasobów z hello SDK usługi Media Services dla platformy .NET](media-services-deliver-streaming-content.md).</span><span class="sxs-lookup"><span data-stu-id="1522e-155">For more information on how toodo this, see hello topic [Deliver Assets with hello Media Services SDK for .NET](media-services-deliver-streaming-content.md).</span></span>

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

## <a name="enumerating-through-large-collections-of-entities"></a><span data-ttu-id="1522e-156">Wyliczanie za pośrednictwem dużych kolekcjach jednostek</span><span class="sxs-lookup"><span data-stu-id="1522e-156">Enumerating through large collections of entities</span></span>
<span data-ttu-id="1522e-157">Podczas wykonywania zapytania jednostek, istnieje limit 1000 jednostek zwracane w tym samym czasie, ponieważ publiczny v2 REST ogranicza wyniki too1000 wyników zapytania.</span><span class="sxs-lookup"><span data-stu-id="1522e-157">When querying entities, there is a limit of 1000 entities returned at one time because public REST v2 limits query results too1000 results.</span></span> <span data-ttu-id="1522e-158">Należy toouse Skip i Take podczas wyliczania dużych kolekcjach jednostek.</span><span class="sxs-lookup"><span data-stu-id="1522e-158">You need toouse Skip and Take when enumerating through large collections of entities.</span></span> 

<span data-ttu-id="1522e-159">Witaj następujących funkcji pętlę wszystkie zadania hello w hello podać konta usługi Media Services.</span><span class="sxs-lookup"><span data-stu-id="1522e-159">hello following function loops through all hello jobs in hello provided Media Services Account.</span></span> <span data-ttu-id="1522e-160">Usługa Media Services zwraca 1000 zadań w kolekcji zadań.</span><span class="sxs-lookup"><span data-stu-id="1522e-160">Media Services returns 1000 jobs in Jobs Collection.</span></span> <span data-ttu-id="1522e-161">Funkcja Hello sprawia, że użycie Skip i zająć się, że toomake który wyliczane są wszystkie zadania (w przypadku, gdy masz więcej niż 1000 zadania konta).</span><span class="sxs-lookup"><span data-stu-id="1522e-161">hello function makes use of Skip and Take toomake sure that all jobs are enumerated (in case you have more than 1000 jobs in your account).</span></span>

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

## <a name="delete-an-asset"></a><span data-ttu-id="1522e-162">Usuń zasób</span><span class="sxs-lookup"><span data-stu-id="1522e-162">Delete an Asset</span></span>
<span data-ttu-id="1522e-163">Poniższy przykład Hello Usuwa zasób.</span><span class="sxs-lookup"><span data-stu-id="1522e-163">hello following example deletes an asset.</span></span>

    static void DeleteAsset( IAsset asset)
    {
        // delete hello asset
        asset.Delete();

        // Verify asset deletion
        if (GetAsset(asset.Id) == null)
            Console.WriteLine("Deleted hello Asset");

    }

## <a name="delete-a-job"></a><span data-ttu-id="1522e-164">Usuwanie zadania</span><span class="sxs-lookup"><span data-stu-id="1522e-164">Delete a Job</span></span>
<span data-ttu-id="1522e-165">toodelete zadanie, musisz sprawdzić hello stan zadania hello wskazane hello stanu właściwości.</span><span class="sxs-lookup"><span data-stu-id="1522e-165">toodelete a job, you must check hello state of hello job as indicated in hello State property.</span></span> <span data-ttu-id="1522e-166">Zadania, które zostały zakończone lub anulowane mogą zostać usunięte podczas zadania, które znajdują się w niektórych innych stanów, np. w kolejce, według harmonogramu lub przetwarzania, należy najpierw anulować, a następnie można go usunąć.</span><span class="sxs-lookup"><span data-stu-id="1522e-166">Jobs that are finished or canceled can be deleted, while jobs that are in certain other states, such as queued, scheduled, or processing, must be canceled first, and then they can be deleted.</span></span>

<span data-ttu-id="1522e-167">Witaj Poniższy przykładowy kod przedstawia metoda usuwania zadania sprawdzania stany zadań, a następnie usuwając podczas hello stanu zostało zakończone lub anulowane.</span><span class="sxs-lookup"><span data-stu-id="1522e-167">hello following code example shows a method for deleting a job by checking job states and then deleting when hello state is finished or canceled.</span></span> <span data-ttu-id="1522e-168">Ten kod jest zależny od hello poprzedniej sekcji, w tym temacie pobierania zadania tooa odwołanie: odwołać zadania.</span><span class="sxs-lookup"><span data-stu-id="1522e-168">This code depends on hello previous section in this topic for getting a reference tooa job: Get a job reference.</span></span>

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


## <a name="delete-an-access-policy"></a><span data-ttu-id="1522e-169">Usunięcie zasad dostępu</span><span class="sxs-lookup"><span data-stu-id="1522e-169">Delete an Access Policy</span></span>
<span data-ttu-id="1522e-170">Witaj Poniższy przykładowy kod przedstawia sposób tooget zasady dostępu tooan odwołania na podstawie zasad Id, a następnie toodelete hello zasad.</span><span class="sxs-lookup"><span data-stu-id="1522e-170">hello following code example shows how tooget a reference tooan access policy based on a policy Id, and then toodelete hello policy.</span></span>

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



## <a name="media-services-learning-paths"></a><span data-ttu-id="1522e-171">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="1522e-171">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="1522e-172">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="1522e-172">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

