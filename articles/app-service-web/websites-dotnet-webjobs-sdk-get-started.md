---
title: "aaaCreate zadanie WebJob platformy .NET w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Utwórz aplikację wielowarstwową przy użyciu platformy ASP.NET MVC i platformy Azure. Hello front end jest uruchamiany w aplikacji sieci web w usłudze Azure App Service i hello powrotem końcowy uruchomień jako zadanie WebJob. Aplikacja Hello korzysta z programu Entity Framework, bazy danych SQL i kolejek usługi Azure storage i obiektów blob."
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="d6487-105">Tworzenie zadania WebJob .NET w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="d6487-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="d6487-106">Ten samouczek pokazuje, jak kod toowrite prostą aplikację ASP.NET MVC 5 wielowarstwowej, która używa hello [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d6487-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="d6487-107">Witaj celem hello [zestaw SDK zadań Webjob](websites-webjobs-resources.md) jest kod hello toosimplify zapisu typowych zadań, które mogą wykonywać zadanie WebJob, takich jak przetwarzania obrazu, przetwarzanie kolejki, agregacja danych RSS, plików obsługi i wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="d6487-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="d6487-108">zestaw SDK zadań Webjob Hello ma wbudowane funkcje do pracy z usługą Azure Storage i usługi Service Bus, planowanie zadań i obsługa błędów i wielu innych typowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="d6487-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="d6487-109">Ponadto ma przeznaczona toobe rozszerzony i jest [repozytorium typu open source dla rozszerzeń](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="d6487-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="d6487-110">Witaj Przykładowa aplikacja to reklamowa Tablica ogłoszeń.</span><span class="sxs-lookup"><span data-stu-id="d6487-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="d6487-111">Użytkowników może przekazywać obrazy dla reklam i procesu zaplecza konwertuje hello toothumbnails obrazów.</span><span class="sxs-lookup"><span data-stu-id="d6487-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="d6487-112">Strona z listą ad Hello miniatury hello i strony szczegółów ad hello pokazuje hello obrazu w pełnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="d6487-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="d6487-113">Poniżej przedstawiono zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="d6487-113">Here's a screenshot:</span></span>

![Lista reklam](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="d6487-115">Ta przykładowa aplikacja działa z [kolejek Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) i [obiekty BLOB platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="d6487-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="d6487-116">Witaj samouczek pokazuje, jak toodeploy hello aplikacji zbyt[usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) i [bazy danych SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="d6487-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="d6487-117"><a id="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d6487-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="d6487-118">Witaj samouczka przyjęto założenie, że wiesz, jak toowork z [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projekty w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6487-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="d6487-119">Samouczek Hello pierwotnie sformatowano dla programu Visual Studio 2013, ale może być używany z nowszej wersji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6487-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="d6487-120">Jeśli używasz programu Visual Studio 2015 lub 2017, zwróć uwagę, że przed uruchomieniem aplikacji hello lokalnie, należy zmienić hello `Data Source` częścią hello parametry połączenia bazy danych LocalDB programu SQL Server w plikach Web.config i App.config hello z `Data Source=(localdb)\v11.0` zbyt`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="d6487-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="d6487-121"><a name="note"></a>W tym samouczku musi mieć toocomplete konto platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="d6487-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="d6487-122">Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): otrzymasz kredyt, że można użyć tootry limit płatnej usług Azure, a nawet po wyczerpaniu, można zachować hello konto i korzystać z bezpłatnych usług platformy Azure, takich jak witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="d6487-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="d6487-123">Karty kredytowej nigdy nie zostanie obciążona, chyba że jawnie zmienić ustawienia i poproś toobe obciążona.</span><span class="sxs-lookup"><span data-stu-id="d6487-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="d6487-124">Możesz [aktywowania Azure miesięczne środki dla subskrybentów usługi Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.</span><span class="sxs-lookup"><span data-stu-id="d6487-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="d6487-125">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="d6487-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="d6487-126">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="d6487-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="d6487-127"><a id="learn"></a>Dowiesz się</span><span class="sxs-lookup"><span data-stu-id="d6487-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="d6487-128">Witaj samouczek pokazuje, jak hello toodo następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="d6487-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="d6487-129">Włącz komputer dla rozwoju platformy Azure, instalując hello zestawu SDK platformy Azure (tylko dla programu Visual Studio 2013 i użytkowników 2015).</span><span class="sxs-lookup"><span data-stu-id="d6487-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="d6487-130">Utwórz projekt aplikacji konsoli, która automatycznie wdraża jako zadanie WebJob platformy Azure, podczas wdrażania projektu sieci web skojarzony hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="d6487-131">Przetestuj zestaw SDK zadań Webjob wewnętrznej bazy danych lokalnie na komputerze dewelopera hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="d6487-132">Publikowanie aplikacji z aplikacją sieci web tooa zadań Webjob wewnętrznej bazy danych w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="d6487-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="d6487-133">Przekazywanie plików i przechowywania ich w hello usługi obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6487-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="d6487-134">Za pomocą hello Azure WebJobs SDK toowork obiektów blob i kolejek usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d6487-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="d6487-135"><a id="contosoads"></a>Architektura aplikacji</span><span class="sxs-lookup"><span data-stu-id="d6487-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="d6487-136">Witaj Przykładowa aplikacja korzysta hello [wzorzec skoncentrowane kolejki pracy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff obciążenia roboczego hello użycie Procesora CPU tworzenia miniatur tooa wewnętrznej bazy danych procesu.</span><span class="sxs-lookup"><span data-stu-id="d6487-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="d6487-137">Aplikacja Hello przechowuje reklamy w bazie danych SQL przy użyciu programu Entity Framework Code First toocreate hello tabel i uzyskiwanie dostępu do danych hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="d6487-138">W przypadku każdej reklamy baza danych hello zawiera dwa adresy URL: jeden dla hello obrazu w pełnym rozmiarze i jeden dla hello miniatur.</span><span class="sxs-lookup"><span data-stu-id="d6487-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![Tabela reklam](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="d6487-140">Gdy użytkownik przesyła obraz, hello aplikacji sieci web zapisuje obraz powitania w [obiektów blob platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), zawierający informacje ad hello w bazie danych hello adres URL, który wskazuje toohello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d6487-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="d6487-141">At hello sama godzina, zapisuje komunikat tooan kolejki systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="d6487-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="d6487-142">W ramach procesu zaplecza uruchomiony jako zadanie WebJob platformy Azure hello zestaw SDK zadań Webjob sonduje hello kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="d6487-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="d6487-143">Gdy pojawi się nowy komunikat, hello zadania WebJob tworzy miniaturę obrazu i aktualizacje hello miniatur pole bazy danych adresu URL dla danej reklamy.</span><span class="sxs-lookup"><span data-stu-id="d6487-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="d6487-144">Poniżej przedstawiono diagram pokazujący sposób interakcji hello części aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="d6487-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Architektura aplikacji Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="d6487-146">instrukcje w samouczku dotyczą Hello zastosować tooAzure zestawu SDK dla platformy .NET 2.7.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="d6487-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="d6487-147"><a id="storage"></a>Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="d6487-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="d6487-148">Konto magazynu platformy Azure udostępnia zasoby do przechowywania danych kolejek i obiektów blob w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="d6487-149">Jest on również używany przez hello dane rejestrowania toostore zestaw SDK zadań Webjob dla pulpitu nawigacyjnego hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="d6487-150">W przypadku aplikacji rzeczywistych można zwykle utworzyć oddzielne konta dla danych aplikacji porównywanych z danymi rejestrowania oraz oddzielne konta dla danych testowych porównywanych z danymi produkcyjnymi.</span><span class="sxs-lookup"><span data-stu-id="d6487-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="d6487-151">W tym samouczku będzie używane tylko jedno konto.</span><span class="sxs-lookup"><span data-stu-id="d6487-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="d6487-152">Otwórz hello **Eksploratora serwera** okna w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6487-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="d6487-153">Kliknij prawym przyciskiem myszy hello **Azure** węzeł, a następnie kliknij przycisk **połączyć tooMicrosoft subskrypcji platformy Azure...** .</span><span class="sxs-lookup"><span data-stu-id="d6487-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![Połącz tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="d6487-155">Zaloguj się przy użyciu poświadczeń konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6487-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="d6487-156">Kliknij prawym przyciskiem myszy **magazynu** w obszarze hello Azure węzeł, a następnie kliknij przycisk **Utwórz konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="d6487-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Tworzenie konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="d6487-158">W hello **Utwórz konto magazynu** okna dialogowego, wprowadź nazwę konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="d6487-159">Nazwa Hello musi być muszą być unikatowe (inne konto magazynu platformy Azure może mieć hello tej samej nazwy).</span><span class="sxs-lookup"><span data-stu-id="d6487-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="d6487-160">Jeśli wprowadzona nazwa hello jest już używana, otrzymasz toochange szansy go.</span><span class="sxs-lookup"><span data-stu-id="d6487-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="d6487-161">Witaj tooaccess adres URL konta magazynu będzie *{nazwa}*. core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d6487-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="d6487-162">Zestaw hello **Region lub grupę koligacji** tooyou najbliższy region toohello listy rozwijanej.</span><span class="sxs-lookup"><span data-stu-id="d6487-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="d6487-163">To ustawienie określa, w którym Centrum danych Azure będą obsługiwać Twoje konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6487-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="d6487-164">W tym samouczku wybór nie należy to znaczącej różnicy.</span><span class="sxs-lookup"><span data-stu-id="d6487-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="d6487-165">Jednak w przypadku aplikacji sieci web produkcji ma serwera sieci web i toobe konta magazynu, korzystając z hello tego samego regionu toominimize opóźnienia i danych wyjściowych opłat.</span><span class="sxs-lookup"><span data-stu-id="d6487-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="d6487-166">Aplikacja sieci web Hello (co należy utworzyć później) powinna być centrum danych, jak to możliwe przeglądarki toohello uzyskiwanie dostępu do aplikacji sieci web hello w kolejności toominimize opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="d6487-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="d6487-167">Zestaw hello **replikacji** listy rozwijanej liście zbyt**magazyn lokalnie nadmiarowy**.</span><span class="sxs-lookup"><span data-stu-id="d6487-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="d6487-168">Jeśli replikacja geograficzna jest włączona dla konta magazynu, hello przechowywana zawartość jest lokalizacji tooenable dodatkowego centrum danych replikowanych tooa toothat trybu failover w przypadku poważnej awarii w lokalizacji głównej hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="d6487-169">Replikacja geograficzna może pociągnąć za sobą dodatkowe koszty.</span><span class="sxs-lookup"><span data-stu-id="d6487-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="d6487-170">W przypadku kont testowych i programistycznych zwykle nie chcesz toopay za replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="d6487-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="d6487-171">Aby uzyskać więcej informacji, zobacz temat dotyczący [tworzenia i usuwania konta magazynu oraz zarządzania nim](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d6487-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="d6487-172">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d6487-172">Click **Create**.</span></span>

    ![Nowe konto usługi Storage](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="d6487-174"><a id="download"></a>Pobieranie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="d6487-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="d6487-175">Pobierz i Rozpakuj hello [ukończone rozwiązanie](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="d6487-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="d6487-176">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6487-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="d6487-177">Z hello **pliku** menu wybierz **Otwórz > Projekt/rozwiązanie**, przejdź toowhere pobranego rozwiązania hello, a następnie otwórz plik rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="d6487-178">Naciśnij klawisze CTRL + SHIFT + B toobuild hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d6487-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="d6487-179">Domyślnie program Visual Studio automatycznie przywraca zawartość pakietu NuGet hello, która nie została uwzględniona w hello *.zip* pliku.</span><span class="sxs-lookup"><span data-stu-id="d6487-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="d6487-180">Jeśli hello pakiety nie zostaną przywrócone, zainstaluj je ręcznie, przechodząc toohello **Zarządzaj pakietami NuGet dla rozwiązania** okno dialogowe i klikając hello **przywrócić** przycisk na powitania w prawym górnym narożniku.</span><span class="sxs-lookup"><span data-stu-id="d6487-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="d6487-181">W **Eksploratora rozwiązań**, upewnij się, że **ContosoAdsWeb** został wybrany jako projekt startowy hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="d6487-182"><a id="configurestorage"></a>Skonfiguruj toouse aplikacji hello konta magazynu</span><span class="sxs-lookup"><span data-stu-id="d6487-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="d6487-183">Otwórz aplikację hello *Web.config* plik w projekcie ContosoAdsWeb hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="d6487-184">Plik Hello zawiera parametry połączenia SQL i parametry połączenia magazynu Azure do pracy z obiektów blob i kolejek.</span><span class="sxs-lookup"><span data-stu-id="d6487-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="d6487-185">Witaj parametrów połączenia SQL punkty tooa [programu SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6487-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="d6487-186">Parametry połączenia magazynu Hello jest przykład symbole zastępcze hello magazynu konta nazwy i klucza dostępu.</span><span class="sxs-lookup"><span data-stu-id="d6487-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="d6487-187">Będzie to Zastąp z parametrów połączenia, które ma hello nazwy i klucza konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6487-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="d6487-188">Parametry połączenia magazynu Hello nosi nazwę AzureWebJobsStorage ponieważ jest to hello nazwa hello, używanych przez zestaw SDK zadań Webjob domyślnie.</span><span class="sxs-lookup"><span data-stu-id="d6487-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="d6487-189">Witaj, tej samej nazwy jest używana w tym miejscu, więc wartość ciągu tylko jedno połączenie tooset hello środowiska platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6487-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="d6487-190">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy konto magazynu w obszarze hello **magazynu** węzeł, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="d6487-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![Kliknij przycisk Właściwości konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="d6487-192">W hello **właściwości** okna, kliknij przycisk **klucze konta magazynu**, a następnie kliknij przycisk wielokropka hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![Klucze konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="d6487-194">Kopiuj hello **ciąg połączenia**.</span><span class="sxs-lookup"><span data-stu-id="d6487-194">Copy hello **Connection String**.</span></span>

    ![Okno dialogowe klucze konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="d6487-196">Zastąp parametry połączenia magazynu hello w hello *Web.config* pliku przy użyciu parametrów połączenia hello został skopiowany.</span><span class="sxs-lookup"><span data-stu-id="d6487-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="d6487-197">Upewnij się, że zaznaczono wszystkie elementy wewnątrz cudzysłowów hello, ale bez znaków cudzysłowu hello przed wklejeniem.</span><span class="sxs-lookup"><span data-stu-id="d6487-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="d6487-198">Otwórz hello *App.config* plik w projekcie ContosoAdsWebJob hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="d6487-199">Ten plik zawiera dwa parametry połączenia magazynu, jeden dla danych aplikacji i jeden dla rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="d6487-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="d6487-200">Możesz użyć oddzielny magazyn kont dla danych aplikacji i rejestrowania i można użyć [konta wielu magazynu dla danych](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="d6487-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="d6487-201">W tym samouczku użyjesz konto jednego magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6487-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="d6487-202">Parametry połączenia Hello ma symbole zastępcze klucze konta magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-202">hello connection strings have placeholders for hello storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="d6487-203">Domyślnie parametry połączenia o nazwie AzureWebJobsStorage i AzureWebJobsDashboard szuka hello zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="d6487-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="d6487-204">Alternatywnie, można [przechowywanie parametrów połączenia hello, jednak mają i przekazać go w jawnie toohello `JobHost` obiektu](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="d6487-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="d6487-205">Zastąp parametry połączenia magazynu hello parametry połączenia, które wcześniej zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="d6487-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="d6487-206">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="d6487-206">Save your changes.</span></span>

## <span data-ttu-id="d6487-207"><a id="run"></a>Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="d6487-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="d6487-208">toostart hello sieci web frontonu aplikacji hello, naciśnij kombinację klawiszy CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="d6487-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="d6487-209">Witaj domyślnej przeglądarce otworzy toohello strony głównej.</span><span class="sxs-lookup"><span data-stu-id="d6487-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="d6487-210">(hello projektu sieci web jest uruchamiana, ponieważ wprowadzono go hello projekt startowy.)</span><span class="sxs-lookup"><span data-stu-id="d6487-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Strona główna aplikacji contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="d6487-212">toostart hello zadania WebJob zaplecza aplikacji hello, kliknij prawym przyciskiem myszy projekt ContosoAdsWebJob hello w **Eksploratora rozwiązań**, a następnie kliknij przycisk **debugowania** > **Start nowe wystąpienie** .</span><span class="sxs-lookup"><span data-stu-id="d6487-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="d6487-213">Okno aplikacji konsoli otwiera i wyświetla rejestrowanie komunikatów wskazujący, że obiekt JobHost zestawu SDK zadań Webjob hello rozpoczęto toorun.</span><span class="sxs-lookup"><span data-stu-id="d6487-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![Okno aplikacji konsoli przedstawiający tego hello wewnętrznej bazy danych jest uruchomiona.](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="d6487-215">W przeglądarce, kliknij przycisk **tworzenia Ad**.</span><span class="sxs-lookup"><span data-stu-id="d6487-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="d6487-216">Wprowadź dane testowe wybierz tooupload obrazu, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d6487-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![Tworzenie strony](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="d6487-218">Aplikacja Hello przechodzi toohello strony indeksu, ale nie wyświetla miniatury nowej reklamy hello, ponieważ przetwarzanie nie zostało jeszcze przeprowadzone.</span><span class="sxs-lookup"><span data-stu-id="d6487-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="d6487-219">W tym samym czasie po krótkim okresie oczekiwania komunikat rejestrowania w oknie aplikacji hello konsoli Pokazuje, że komunikatu w kolejce został odebrany i został przetworzony.</span><span class="sxs-lookup"><span data-stu-id="d6487-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![Okno aplikacji konsoli przedstawiający przetworzeniu komunikatu w kolejce](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="d6487-221">Po hello rejestrowanie komunikatów w oknie aplikacji hello konsoli zostanie wyświetlony, Odśwież hello indeksu strony toosee hello miniatur.</span><span class="sxs-lookup"><span data-stu-id="d6487-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![Strona indeksu](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="d6487-223">Kliknij przycisk **szczegóły** dla użytkownika ad toosee hello obrazu w pełnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="d6487-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![Strona szczegółów](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="d6487-225">Działała aplikacja hello na komputerze lokalnym i używa programu SQL Server, bazy danych znajdującej się na komputerze, ale działa w przypadku kolejek i obiektów blob w hello chmury.</span><span class="sxs-lookup"><span data-stu-id="d6487-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="d6487-226">W następujących sekcji hello uruchomisz aplikacji hello w chmurze hello przy użyciu bazy danych w chmurze, a także chmury obiekty BLOB i kolejki.</span><span class="sxs-lookup"><span data-stu-id="d6487-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="d6487-227"><a id="runincloud"></a>Uruchamianie aplikacji hello w chmurze hello</span><span class="sxs-lookup"><span data-stu-id="d6487-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="d6487-228">Należy to zrobić hello następujące kroki toorun hello aplikacji w chmurze hello:</span><span class="sxs-lookup"><span data-stu-id="d6487-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="d6487-229">Wdrażanie aplikacji tooWeb.</span><span class="sxs-lookup"><span data-stu-id="d6487-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="d6487-230">Visual Studio automatycznie tworzy nową aplikację sieci web usługi aplikacji i wystąpienie bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d6487-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="d6487-231">Skonfiguruj toouse aplikacji sieci web hello konta magazynu i bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="d6487-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="d6487-232">Po utworzeniu niektóre reklamy podczas uruchamiania w chmurze hello, zostanie wyświetlona hello rozbudowane funkcje ma toooffer hello toosee pulpitu nawigacyjnego zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="d6487-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="d6487-233">Wdrażanie aplikacji tooWeb</span><span class="sxs-lookup"><span data-stu-id="d6487-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="d6487-234">Zamknij przeglądarkę hello i okna aplikacji hello konsoli.</span><span class="sxs-lookup"><span data-stu-id="d6487-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="d6487-235">Wykonaj kroki hello hello [publikowania tooAzure z bazy danych SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d6487-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="d6487-236">Po wykonaniu kroków hello wdrażania, kontynuuj hello pozostałych zadań w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="d6487-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="d6487-237">Skonfiguruj toouse aplikacji sieci web hello konta magazynu i bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="d6487-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="d6487-238">Ze względów bezpieczeństwa jest zbyt[należy unikać umieszczania poufne informacje, takie jak parametry połączenia w plikach, które są przechowywane w repozytoriach kodów źródłowych](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="d6487-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="d6487-239">Platforma Azure udostępnia toodo sposób: można ustawić parametry połączenia i inne wartości ustawień, które znajdują się w hello środowiska platformy Azure i interfejsy API konfiguracji ASP.NET automatyczne pobranie te wartości po uruchomieniu aplikacji hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d6487-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="d6487-240">Te wartości zostaną ustawione na platformie Azure, używając **Eksploratora serwera**, hello portalu Azure, programu Windows PowerShell lub hello międzyplatformowego interfejsu wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="d6487-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="d6487-241">Aby uzyskać więcej informacji, zobacz [jak ciągi aplikacji i pracy ciągów połączenia](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="d6487-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="d6487-242">W tej sekcji użyjesz **Eksploratora serwera** tooset wartości parametrów połączeń na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d6487-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="d6487-243">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy aplikację sieci web, w obszarze **Azure > App Service > {grupie zasobów}**, a następnie kliknij przycisk **ustawienia widoku**.</span><span class="sxs-lookup"><span data-stu-id="d6487-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="d6487-244">Witaj **aplikacji sieci Web Azure** na powitania zostanie otwarte okno **konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="d6487-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="d6487-245">Zmień nazwę hello hello połączenia DefaultConnection połączenia ciąg toohello nazwy wybrania podczas konfigurowania bazy danych SQL hello w hello [publikowania tooAzure z bazy danych SQL](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artykułu.</span><span class="sxs-lookup"><span data-stu-id="d6487-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="d6487-246">Podczas tworzenia aplikacji sieci web hello skojarzona baza danych, ma już wartość ciągu połączenia na odpowiednie hello Azure automatycznie utworzone te parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="d6487-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="d6487-247">Zmieniasz właśnie toowhat nazwa hello, który potrzebuje kodu.</span><span class="sxs-lookup"><span data-stu-id="d6487-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="d6487-248">Dodaj dwa nowe parametry połączenia, o nazwie AzureWebJobsStorage i AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="d6487-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="d6487-249">Ustaw typ bazy danych hello zbyt**niestandardowy**i samą wartość, należy wcześniej używane dla hello zestaw hello połączenia ciągu wartości toohello *Web.config* i *App.config* plików.</span><span class="sxs-lookup"><span data-stu-id="d6487-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="d6487-250">(Upewnij się, obejmują hello całego połączenia ciągu, nie tylko klucz dostępu hello i nie zawierają znaki cudzysłowu hello.)</span><span class="sxs-lookup"><span data-stu-id="d6487-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="d6487-251">Te parametry połączenia są używane przez hello zestaw SDK zadań Webjob, jeden dla danych aplikacji i jeden dla rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="d6487-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="d6487-252">Jak przedstawiono wcześniej, hello, jeden dla danych aplikacji jest również używany przez kod frontonu sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="d6487-253">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d6487-253">Click **Save**.</span></span>

    ![Parametry połączenia w portalu Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="d6487-255">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy hello aplikacji sieci web, a następnie kliknij przycisk **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="d6487-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="d6487-256">Po zatrzymaniu hello aplikacji sieci web, ponownie kliknij prawym przyciskiem myszy hello aplikacji sieci web, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="d6487-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="d6487-257">Hello zadania WebJob jest uruchamiana automatycznie, gdy opublikujesz, ale zatrzymuje go po wprowadzeniu zmiany konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d6487-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="d6487-258">toorestart, możesz ponownie uruchomić aplikacji sieci web hello, lub uruchom ponownie zadanie WebJob hello w hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="d6487-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="d6487-259">Aplikacja sieci web hello toorestart ogólnie zalecane jest po zmianie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d6487-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="d6487-260">Odśwież okno przeglądarki hello zawierający adres URL aplikacji sieci web hello na jego pasku adresu.</span><span class="sxs-lookup"><span data-stu-id="d6487-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="d6487-261">zostanie wyświetlona strona główna Hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-261">hello home page appears.</span></span>
8. <span data-ttu-id="d6487-262">Utwórz reklamę, jak w przypadku należy [uruchomiono lokalnie aplikacji hello](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="d6487-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="d6487-263">Strona indeksu Hello pokazuje bez miniatur na początku.</span><span class="sxs-lookup"><span data-stu-id="d6487-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="d6487-264">Odśwież stronę powitania po kilku sekundach i hello miniatur zostanie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="d6487-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="d6487-265">Jeśli nie ma miniatury hello, może być toowait minuty hello toorestart zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="d6487-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="d6487-266">Jeśli po chwili, nadal nie widać miniatur powitania po odświeżeniu strony hello, hello zadania WebJob może nie został uruchomiony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d6487-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="d6487-267">W takim przypadku przejdź toohello **usługi aplikacji** bloku w hello [portalu Azure](https://portal.azure.com/), Znajdź aplikację sieci web, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="d6487-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="d6487-268">Witaj widoku pulpitu nawigacyjnego zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="d6487-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="d6487-269">W hello [portalu Azure](https://portal.azure.com/), wybierz pozycję hello **blok App Services**Znajdź aplikację sieci web i zaznacz **Webjob**.</span><span class="sxs-lookup"><span data-stu-id="d6487-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="d6487-270">Wybierz hello **dzienniki** kartę.</span><span class="sxs-lookup"><span data-stu-id="d6487-270">Select hello **Logs** tab.</span></span>

    ![Karta dzienniki](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="d6487-272">Na nowej karcie przeglądarki zostanie otwarty toohello zestaw SDK zadań Webjob pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="d6487-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="d6487-273">pulpit nawigacyjny Hello zawiera ten hello zadania WebJob działa i jest to lista funkcji w kodzie tego hello wyzwolenia przez zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="d6487-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="d6487-274">Kliknij jeden z hello funkcje toosee szczegóły jego wykonywania.</span><span class="sxs-lookup"><span data-stu-id="d6487-274">Click one of hello functions toosee details about its execution.</span></span>

    ![Zestaw SDK zadań Webjob pulpitu nawigacyjnego](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Zestaw SDK zadań Webjob pulpitu nawigacyjnego](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="d6487-277">Witaj **funkcja powtarzania** przycisk powoduje, że zestaw SDK zadań Webjob hello framework toocall hello funkcja ponownie i udostępnia funkcję toohello szansy toochange hello danych przekazanych najpierw.</span><span class="sxs-lookup"><span data-stu-id="d6487-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="d6487-278">Po zakończeniu testowania, rozważ usunięcie aplikacji sieci web hello, konta magazynu i wystąpienie bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d6487-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="d6487-279">Aplikacja sieci web Hello jest bezpłatne, ale hello konta magazynu SQL i wystąpienie bazy danych Naliczanie opłat (aczkolwiek, minimalna powodu toohello mały rozmiar).</span><span class="sxs-lookup"><span data-stu-id="d6487-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="d6487-280">Ponadto pozostawienie hello aplikacji sieci web, każda osoba, która znajdzie adres URL można tworzyć i wyświetlać reklamy.</span><span class="sxs-lookup"><span data-stu-id="d6487-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="d6487-281">Usuń aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="d6487-281">Delete your web app</span></span>
<span data-ttu-id="d6487-282">W portalu hello Przejdź toohello **usługi aplikacji** bloku, Znajdź i wybierz aplikację sieci web, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="d6487-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="d6487-283">Wystarczy tootemporarily uniemożliwić innym użytkownikom dostęp do aplikacji sieci web hello, kliknij przycisk **zatrzymać** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="d6487-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="d6487-284">W takim przypadku opłaty będą nadal tooaccrue dla hello bazy danych SQL i konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6487-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="d6487-285">Usuwanie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="d6487-285">Delete your storage account</span></span>
<span data-ttu-id="d6487-286">toodelete Twojego konta magazynu, zobacz [usuwania konta magazynu](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d6487-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="d6487-287">Usunięcie bazy danych</span><span class="sxs-lookup"><span data-stu-id="d6487-287">Delete your database</span></span>
<span data-ttu-id="d6487-288">toodelete Twojego SQL bazy danych, zobacz hello [interfejsu API REST bazy danych SQL Azure](https://docs.microsoft.com/rest/api/sql/) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d6487-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="d6487-289"><a id="create"></a>Tworzenie aplikacji hello od początku</span><span class="sxs-lookup"><span data-stu-id="d6487-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="d6487-290">W tej sekcji należy wykonać hello następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="d6487-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="d6487-291">Tworzenie rozwiązania Visual Studio z projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6487-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="d6487-292">Dodawanie projektu biblioteki klas danych hello warstwy dostępu, która jest udostępniana między hello frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d6487-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="d6487-293">Dodaj projekt aplikacji konsoli hello wewnętrznej bazy danych, z włączonym wdrażaniem zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="d6487-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="d6487-294">Dodawanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="d6487-294">Add NuGet packages.</span></span>
* <span data-ttu-id="d6487-295">Ustawianie odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="d6487-295">Set project references.</span></span>
* <span data-ttu-id="d6487-296">Skopiuj pliki kodu i konfiguracji aplikacji z aplikacji hello pobrane, który pracuje z hello w poprzedniej sekcji samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="d6487-297">Przejrzyj hello hello istotnych częściach kodu pracy z kolejkami i obiekty BLOB platformy Azure i hello zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="d6487-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="d6487-298">Tworzenie rozwiązań programu Visual Studio z projektu sieci web i projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="d6487-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="d6487-299">W programie Visual Studio, wybierz **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="d6487-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="d6487-300">W hello **nowy projekt** okno dialogowe, wybierz **Visual C#** > **Web** > **aplikacji sieci Web platformy ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="d6487-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="d6487-301">Nazwa hello projekt ContosoAdsWeb, nazwa rozwiązania hello ContosoAdsWebJobsSDK (zmienić nazwy rozwiązania hello, jeśli chcesz umieścić go w hello tym samym folderze co hello pobrane rozwiązanie), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6487-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![Nowy projekt](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="d6487-303">W hello **nowej aplikacji sieci Web ASP.NET** okno dialogowe, wybierz szablon MVC hello, a następnie wybierz **Zmień uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="d6487-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![Zmienianie uwierzytelniania](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="d6487-305">W hello **Zmień uwierzytelnianie** okno dialogowe, wybierz **bez uwierzytelniania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6487-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Bez uwierzytelniania](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="d6487-307">W hello **nowej aplikacji sieci Web ASP.NET** okna dialogowego, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6487-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="d6487-308">Program Visual Studio tworzy rozwiązanie hello i hello projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6487-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="d6487-309">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy rozwiązanie hello (nie projekt hello) i wybierz **Dodaj** > **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="d6487-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="d6487-310">W hello **Dodawanie nowego projektu** okno dialogowe, wybierz **Visual C#** > **Windows Desktop klasycznego** > **klasy biblioteki (.NET Framework)** szablonu.</span><span class="sxs-lookup"><span data-stu-id="d6487-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="d6487-311">Nazwa projektu hello *ContosoAdsCommon*, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6487-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="d6487-312">Ten projekt będzie zawierał hello kontekstu programu Entity Framework i hello modelu danych, które zarówno hello frontonu i użyje zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d6487-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="d6487-313">Alternatywnie można zdefiniować klasy związane z platformą EF hello w hello projektu sieci web i odwoływać się do tego projektu z projektu zadania WebJob hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="d6487-314">Ale następnie projektu zadania WebJob musi zestawów tooweb odwołań, których nie potrzebuje.</span><span class="sxs-lookup"><span data-stu-id="d6487-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="d6487-315">Dodaj projekt aplikacji konsoli z włączonym wdrażaniem zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="d6487-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="d6487-316">Kliknij prawym przyciskiem myszy projekt sieci web hello (nie hello rozwiązania lub projektu biblioteki klas hello), a następnie kliknij przycisk **Dodaj** > **nowy projekt zadania WebJob Azure**.</span><span class="sxs-lookup"><span data-stu-id="d6487-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Nowe zaznaczenie menu projektu zadania WebJob platformy Azure](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="d6487-318">W hello **dodać zadania WebJob Azure** okna dialogowego, wprowadź ContosoAdsWebJob jako zarówno hello **Nazwa projektu** i hello **Nazwa zadania WebJob**.</span><span class="sxs-lookup"><span data-stu-id="d6487-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="d6487-319">Pozostaw **tryb uruchomienia zadania WebJob** ustawić także**Uruchom stale**.</span><span class="sxs-lookup"><span data-stu-id="d6487-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="d6487-320">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6487-320">Click **OK**.</span></span>

   <span data-ttu-id="d6487-321">Program Visual Studio tworzy aplikacja Konsolowa, która jest skonfigurowana toodeploy jako zadanie WebJob zawsze, gdy wdrażanie projektu sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="d6487-322">toodo, jego wykonanie hello następujące zadania po utworzeniu projektu hello:</span><span class="sxs-lookup"><span data-stu-id="d6487-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="d6487-323">Dodaje *zadania webjob publikowania settings.json* plików w folderze właściwości projektu zadania WebJob hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="d6487-324">Dodaje *list.json webjob* plików w folderze właściwości projektu sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="d6487-325">Zainstalowany pakiet Microsoft.Web.WebJobs.Publish NuGet hello w hello projektu zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="d6487-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="d6487-326">Aby uzyskać więcej informacji na temat tych zmian, zobacz [jak toodeploy zadań Webjob za pomocą programu Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="d6487-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="d6487-327">Dodawanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="d6487-327">Add NuGet packages</span></span>
<span data-ttu-id="d6487-328">Witaj nowy projekt szablonu projektu zadania WebJob automatycznie instaluje pakiet NuGet zestawu SDK zadań Webjob hello [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="d6487-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="d6487-329">Jeden z hello jest zestaw SDK zadań Webjob zależności, które jest instalowane automatycznie w projektu zadania WebJob hello hello Azure magazynu klienta biblioteki (SCL).</span><span class="sxs-lookup"><span data-stu-id="d6487-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="d6487-330">Jednak należy tooadd go toowork projektu sieci web toohello z obiektów blob i kolejek.</span><span class="sxs-lookup"><span data-stu-id="d6487-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="d6487-331">Otwórz hello **Zarządzaj pakietami NuGet** okna dialogowego hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d6487-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="d6487-332">Wybierz w okienku po lewej stronie powitania **zainstalowane pakiety**.</span><span class="sxs-lookup"><span data-stu-id="d6487-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="d6487-333">Znajdź hello *usługi Azure Storage* pakietu, a następnie kliknij przycisk **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="d6487-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="d6487-334">W hello **Wybierz projekty** okno, wybierz hello **ContosoAdsWeb** pole wyboru, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6487-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="d6487-335">Wszystkie trzy projekty za pomocą toowork Entity Framework hello danych w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d6487-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="d6487-336">Wybierz w okienku po lewej stronie powitania **Online**.</span><span class="sxs-lookup"><span data-stu-id="d6487-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="d6487-337">Znajdź hello *EntityFramework* NuGet pakietu, a następnie zainstaluj go we wszystkich trzech projektach.</span><span class="sxs-lookup"><span data-stu-id="d6487-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="d6487-338">Ustawianie odwołań do projektu</span><span class="sxs-lookup"><span data-stu-id="d6487-338">Set project references</span></span>
<span data-ttu-id="d6487-339">Sieć web i projektów zadania WebJob pracy z hello bazy danych SQL, tak zarówno wymagane odwołanie do projektu ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="d6487-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="d6487-340">W projekcie ContosoAdsWeb hello Ustaw odwołanie do projektu ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="d6487-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="d6487-341">(Kliknij prawym przyciskiem myszy projekt ContosoAdsWeb hello, a następnie kliknij przycisk **Dodaj** > **odwołania**.</span><span class="sxs-lookup"><span data-stu-id="d6487-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="d6487-342">W hello **Menedżera odwołań** okno dialogowe, wybierz opcję **projekty** > **rozwiązania** > **ContosoAdsCommon**, a następnie kliknij przycisk **OK**.)</span><span class="sxs-lookup"><span data-stu-id="d6487-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="d6487-343">Witaj projektu zadania WebJob musi odwołania do pracy z obrazami i uzyskać dostęp do parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="d6487-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="d6487-344">W projekcie ContosoAdsWebJob hello Ustaw odwołanie za`System.Drawing` i `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="d6487-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="d6487-345">Dodawanie plików kodu i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="d6487-345">Add code and configuration files</span></span>
<span data-ttu-id="d6487-346">W tym samouczku nie pokazuje sposób zbyt[utworzyć przy użyciu funkcji szkieletów widoków i kontrolerów MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), jak za[pisania kodu programu Entity Framework, który współpracuje z baz danych programu SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), lub [hello podstawy Programowanie w programie ASP.NET 4.5 asynchroniczne](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="d6487-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="d6487-347">Tak, czy pozostaje toodo jest kopiowania kodu i plików konfiguracji z rozwiązania hello pobrane do hello nowego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="d6487-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="d6487-348">Po wykonaniu tej czynności, hello sekcje Pokaż i objaśnione części hello kodu.</span><span class="sxs-lookup"><span data-stu-id="d6487-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="d6487-349">pliki tooadd tooa projektu lub folderu, kliknij prawym przyciskiem myszy projekt hello lub folderu i kliknij przycisk **Dodaj** > **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="d6487-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="d6487-350">Wybierz hello pliki chcesz i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d6487-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="d6487-351">Jeśli zostanie wyświetlone pytanie, czy tooreplace istniejące pliki, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="d6487-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="d6487-352">W projekcie ContosoAdsCommon hello Usuń hello *Class1.cs* i Dodaj w jego hello miejsce następujące pliki z projektu hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="d6487-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="d6487-353">*AD.CS*</span><span class="sxs-lookup"><span data-stu-id="d6487-353">*Ad.cs*</span></span>
   * <span data-ttu-id="d6487-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="d6487-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="d6487-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="d6487-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="d6487-356">W projekcie ContosoAdsWeb hello Dodaj hello następujące pliki z projektu hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="d6487-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="d6487-357">*Plik Web.config*</span><span class="sxs-lookup"><span data-stu-id="d6487-357">*Web.config*</span></span>
   * <span data-ttu-id="d6487-358">*Global.asax.CS*</span><span class="sxs-lookup"><span data-stu-id="d6487-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="d6487-359">W hello *kontrolerów* folder: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="d6487-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="d6487-360">W hello *Views\Shared* folder: *_Layout.cshtml* pliku</span><span class="sxs-lookup"><span data-stu-id="d6487-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="d6487-361">W hello *Views\Home* folder: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="d6487-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="d6487-362">W hello *Views\Ad* folder (najpierw utwórz hello folder): pięć *.cshtml* plików</span><span class="sxs-lookup"><span data-stu-id="d6487-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="d6487-363">W projekcie ContosoAdsWebJob hello Dodaj hello następujące pliki z projektu hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="d6487-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="d6487-364">*App.config* (Zmień filtr typu pliku hello zbyt**wszystkie pliki**)</span><span class="sxs-lookup"><span data-stu-id="d6487-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="d6487-365">*Plik program.CS*</span><span class="sxs-lookup"><span data-stu-id="d6487-365">*Program.cs*</span></span>
   * <span data-ttu-id="d6487-366">*Functions.CS*</span><span class="sxs-lookup"><span data-stu-id="d6487-366">*Functions.cs*</span></span>

<span data-ttu-id="d6487-367">Można teraz utworzyć, uruchamiania i wdrażania aplikacji hello zgodnie z instrukcjami podanymi wcześniej w samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="d6487-368">Przed tym, jednak zatrzymać hello zadania WebJob, który jest nadal uruchomione w hello pierwszej aplikacji sieci web wdrożonej w.</span><span class="sxs-lookup"><span data-stu-id="d6487-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="d6487-369">W przeciwnym razie wartość tego zadania WebJob będzie przetwarzać komunikaty z kolejki utworzony lokalnie lub przez hello uruchomieniu aplikacji w nowej aplikacji sieci web, ponieważ wszystkie przy użyciu hello sam konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6487-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="d6487-370"><a id="code"></a>Kod aplikacji hello przeglądu</span><span class="sxs-lookup"><span data-stu-id="d6487-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="d6487-371">Witaj poniższe sekcje zawierają opis kodu hello związane z tooworking z hello zestaw SDK zadań Webjob i obiektów blob magazynu Azure i kolejek.</span><span class="sxs-lookup"><span data-stu-id="d6487-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="d6487-372">Dla hello kodu toohello określonego zestawu SDK zadań Webjob, przejdź toohello [Program.cs i Functions.cs](#programcs) sekcje.</span><span class="sxs-lookup"><span data-stu-id="d6487-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="d6487-373">ContosoAdsCommon — Ad.cs</span><span class="sxs-lookup"><span data-stu-id="d6487-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="d6487-374">Witaj plik Ad.cs definiuje wyliczenia związane z kategoriami reklam i klasą jednostki POCO dla informacji o reklamach.</span><span class="sxs-lookup"><span data-stu-id="d6487-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="d6487-375">ContosoAdsCommon — ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="d6487-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="d6487-376">Witaj klasa ContosoAdsContext Określa, czy klasa Ad hello jest używany w kolekcji DbSet Entity Framework są przechowywane w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="d6487-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

<span data-ttu-id="d6487-377">Klasa Hello ma dwa konstruktory.</span><span class="sxs-lookup"><span data-stu-id="d6487-377">hello class has two constructors.</span></span> <span data-ttu-id="d6487-378">najpierw Hello jest używany przez hello projektu sieci web i określa nazwę parametrów połączenia, które są przechowywane w pliku Web.config hello lub środowisko uruchomieniowe Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="d6487-379">Witaj drugi Konstruktor umożliwia toopass w hello rzeczywistych parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="d6487-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="d6487-380">Są one wymagane projektu zadania WebJob hello ponieważ nie ma on pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="d6487-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="d6487-381">Wcześniej przedstawiono gdzie te parametry połączenia są przechowywane i pojawi się później, jak hello kod pobiera parametry połączenia hello podczas tworzenia wystąpień klasy DbContext hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="d6487-382">ContosoAdsCommon — BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="d6487-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="d6487-383">Witaj `BlobInformation` klasa jest używana toostore informacji na temat obiekt blob obrazu w komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="d6487-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="d6487-384">ContosoAdsWeb — Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="d6487-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="d6487-385">Kod, który jest wywoływany z hello `Application_Start` metoda tworzy *obrazów* kontenera obiektów blob i *obrazów* kolejki, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="d6487-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="d6487-386">Dzięki temu, że przy każdym uruchomieniu przy użyciu nowego konta magazynu, hello wymagane, kolejka i kontener obiektów blob są tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d6487-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="d6487-387">Witaj konta magazynu toohello kod pobiera dostępu przy użyciu parametrów połączenia magazynu hello z hello *Web.config* pliku lub środowisko uruchomieniowe platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6487-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="d6487-388">Następnie pobiera toohello odwołanie *obrazów* kontenera obiektów blob, tworzy kontener hello, jeśli jeszcze nie istnieje, i zestawów uprawnień dostępu na powitania nowy kontener.</span><span class="sxs-lookup"><span data-stu-id="d6487-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="d6487-389">Domyślnie nowe kontenery Zezwalaj tylko klientów z obiektów blob tooaccess poświadczeń konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="d6487-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="d6487-390">Hello aplikacji sieci web wymaga hello publicznego toobe obiektów blob, aby możliwe było wyświetlanie obrazów przy użyciu adresów URL tego obiekty BLOB obrazów toohello punktu.</span><span class="sxs-lookup"><span data-stu-id="d6487-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="d6487-391">Podobny kod pobiera odwołanie toohello *thumbnailrequest* kolejki i tworzy nową kolejkę.</span><span class="sxs-lookup"><span data-stu-id="d6487-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="d6487-392">W takim przypadku nie trzeba zmieniać uprawnień.</span><span class="sxs-lookup"><span data-stu-id="d6487-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="d6487-393">ContosoAdsWeb — _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="d6487-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="d6487-394">Witaj *_Layout.cshtml* plik ustawia nazwę aplikacji hello w hello nagłówku i stopce oraz utworzenie wpisu menu "Ads".</span><span class="sxs-lookup"><span data-stu-id="d6487-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="d6487-395">ContosoAdsWeb — Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="d6487-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="d6487-396">Witaj *Views\Home\Index.cshtml* pliku wyświetla linków kategorii na stronie głównej hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="d6487-397">Witaj linki przekazują wartość całkowitą hello hello `Category` wyliczenia na stronie indeksu reklam toohello zmiennej querystring.</span><span class="sxs-lookup"><span data-stu-id="d6487-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="d6487-398">ContosoAdsWeb — AdController.cs</span><span class="sxs-lookup"><span data-stu-id="d6487-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="d6487-399">W hello *AdController.cs* plik, hello wywołania konstruktora hello `InitializeStorage` — metoda toocreate biblioteki klienta magazynu Azure obiektów, które zapewniają interfejs API do pracy z obiektów blob i kolejek.</span><span class="sxs-lookup"><span data-stu-id="d6487-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="d6487-400">Następnie kod hello pobiera toohello odwołanie *obrazów* kontenera obiektów blob, jak przedstawiono wcześniej w *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="d6487-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="d6487-401">Podczas wykonywania, który, ustawia domyślną [zasady ponawiania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) odpowiednie dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="d6487-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="d6487-402">zasady ponawiania wykładniczego wycofywania domyślne Hello mogą powodować zawieszanie aplikacji sieci web hello przez czas dłuższy niż minuta w przypadku kolejnych prób błędu przejściowego.</span><span class="sxs-lookup"><span data-stu-id="d6487-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="d6487-403">Witaj zasady ponawiania określone w tym miejscu czeka trzy sekundy po każdej się toothree prób.</span><span class="sxs-lookup"><span data-stu-id="d6487-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="d6487-404">Podobny kod pobiera odwołanie toohello *obrazów* kolejki.</span><span class="sxs-lookup"><span data-stu-id="d6487-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="d6487-405">Większość kodu kontrolera hello jest typowa dla pracy z modelem danych programu Entity Framework za pomocą klasy DbContext.</span><span class="sxs-lookup"><span data-stu-id="d6487-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="d6487-406">Wyjątkiem jest hello HttpPost `Create` metodę, która przekazuje plik i zapisuje je w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="d6487-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="d6487-407">udostępnia integratora modelu Hello [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) obiekt toohello metody.</span><span class="sxs-lookup"><span data-stu-id="d6487-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="d6487-408">Użytkownika hello zaznaczenie tooupload pliku, kod hello hello plik zostanie przesłany, zapisuje go w obiekcie blob i aktualizacji rekordu bazy danych Ad hello adres URL, który wskazuje obiekt blob toohello.</span><span class="sxs-lookup"><span data-stu-id="d6487-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="d6487-409">Witaj kod hello przekazywania jest hello `UploadAndSaveBlobAsync` metody.</span><span class="sxs-lookup"><span data-stu-id="d6487-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="d6487-410">Tworzy nazwę identyfikatora GUID dla obiektu blob hello, przekazywanie i zapisuje plik hello i zwraca odwołanie do obiektu blob toohello zapisane.</span><span class="sxs-lookup"><span data-stu-id="d6487-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

<span data-ttu-id="d6487-411">Po hello HttpPost `Create` metoda przekazuje obiekt blob i aktualizacje hello bazy danych, tworzy kolejki wiadomości tooinform hello zaplecza proces że obraz jest gotowy do konwersji tooa miniatur.</span><span class="sxs-lookup"><span data-stu-id="d6487-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="d6487-412">Witaj kod hello HttpPost `Edit` metoda jest podobny, z wyjątkiem tego, że jeśli hello użytkownik wybierze nowy plik obrazu, należy usunąć wszystkie obiekty BLOB, które już istnieją dla tej usługi ad.</span><span class="sxs-lookup"><span data-stu-id="d6487-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="d6487-413">Oto kod hello usuwania obiektów blob podczas usuwania reklamy:</span><span class="sxs-lookup"><span data-stu-id="d6487-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="d6487-414">ContosoAdsWeb — Views\Ad\Index.cshtml i Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="d6487-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="d6487-415">Witaj *Index.cshtml* służy do wyświetlania miniatury z hello innymi danymi reklamy:</span><span class="sxs-lookup"><span data-stu-id="d6487-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="d6487-416">Witaj *Details.cshtml* pliku wyświetla obrazu w pełnym rozmiarze hello:</span><span class="sxs-lookup"><span data-stu-id="d6487-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="d6487-417">ContosoAdsWeb — Views\Ad\Create.cshtml i Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="d6487-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="d6487-418">Witaj *Create.cshtml* i *Edit.cshtml* pliki określają kodowanie, że umożliwia hello hello tooget kontrolera formularza `HttpPostedFileBase` obiektu.</span><span class="sxs-lookup"><span data-stu-id="d6487-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="d6487-419">`<input>` Informuje hello przeglądarki tooprovide okna dialogowego wyboru pliku.</span><span class="sxs-lookup"><span data-stu-id="d6487-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="d6487-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="d6487-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="d6487-421">Gdy hello uruchamia zadania WebJob hello `Main` wywołania metody hello zestaw SDK zadań Webjob `JobHost.RunAndBlock` wykonywania toobegin metody funkcji wyzwalanych na powitania bieżącego wątku.</span><span class="sxs-lookup"><span data-stu-id="d6487-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="d6487-422"><a id="generatethumbnail"></a>Metoda GenerateThumbnail ContosoAdsWebJob - Functions.cs-</span><span class="sxs-lookup"><span data-stu-id="d6487-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="d6487-423">zestaw SDK zadań Webjob Hello wywołuje tę metodę po odebraniu komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="d6487-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="d6487-424">Metoda Hello tworzy miniaturę i naraża hello miniatur adres URL w hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6487-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within hello function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="d6487-425">Witaj `QueueTrigger` atrybutu kieruje hello toocall zestaw SDK zadań Webjob tę metodę po odebraniu nowej wiadomości w kolejce thumbnailrequest hello.</span><span class="sxs-lookup"><span data-stu-id="d6487-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="d6487-426">Witaj `BlobInformation` obiekt hello kolejki wiadomości jest automatycznie zdeserializowany do hello `blobInfo` parametru.</span><span class="sxs-lookup"><span data-stu-id="d6487-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="d6487-427">Po ukończeniu metody hello, komunikatu w kolejce hello jest usuwana.</span><span class="sxs-lookup"><span data-stu-id="d6487-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="d6487-428">W przypadku niepowodzenia przed wykonaniem metody hello hello kolejka komunikatów nie zostanie usunięta; Po wygaśnięciu dzierżawy 10-minutowych wiadomość hello jest wydanych toobe pobrana ponownie i przetwarzane.</span><span class="sxs-lookup"><span data-stu-id="d6487-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="d6487-429">Ta sekwencja nie należy powtórzyć przez czas nieokreślony, jeśli komunikat zawsze powoduje zgłoszenie wyjątku.</span><span class="sxs-lookup"><span data-stu-id="d6487-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="d6487-430">Po 5 nieudanych próbach tooprocess wiadomości, wiadomość hello jest przeniesionego tooa kolejki o nazwie {queuename}-skażone.</span><span class="sxs-lookup"><span data-stu-id="d6487-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="d6487-431">konfiguruje się Hello maksymalną liczbę prób.</span><span class="sxs-lookup"><span data-stu-id="d6487-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="d6487-432">Witaj dwie `Blob` atrybuty Podaj obiektów, które są powiązane tooblobs: jeden toohello istniejący obiekt blob obrazu i jeden tooa nowego obiektu blob miniatury tworzącą hello metody.</span><span class="sxs-lookup"><span data-stu-id="d6487-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="d6487-433">Nazwy obiektów blob pochodzą z właściwości hello `BlobInformation` obiektu otrzymane w wiadomości powitania kolejki (`BlobName` i `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="d6487-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="d6487-434">tooget hello pełną funkcjonalność hello biblioteki klienta usługi Storage, można użyć hello `CloudBlockBlob` toowork klasy z obiektami blob.</span><span class="sxs-lookup"><span data-stu-id="d6487-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="d6487-435">Jeśli chcesz, aby tooreuse kod, który został zapisany toowork z `Stream` obiekty, można użyć hello `Stream` klasy.</span><span class="sxs-lookup"><span data-stu-id="d6487-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="d6487-436">Aby uzyskać więcej informacji na temat sposobu toowrite funkcje, które używane są atrybuty zestaw SDK zadań Webjob, zobacz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="d6487-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="d6487-437">Jak toouse Azure kolejki magazynu z hello zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="d6487-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="d6487-438">Jak toouse Azure blob magazynu z hello zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="d6487-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="d6487-439">Jak toouse Azure tabeli magazynu z hello zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="d6487-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="d6487-440">W jaki sposób toouse usługa Azure Service Bus z hello zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="d6487-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="d6487-441">Jeśli aplikacja sieci web jest uruchomiony na wiele maszyn wirtualnych, wielu zadań Webjob będzie działać jednocześnie, a w niektórych przypadkach może to spowodować hello sam danych przetwarzana wiele razy.</span><span class="sxs-lookup"><span data-stu-id="d6487-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="d6487-442">Nie jest problem użycie hello wbudowanych kolejki, obiektów blob i wyzwalaczy usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="d6487-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="d6487-443">Hello SDK gwarantuje, że funkcje będą przetwarzane tylko raz dla każdego komunikatu lub obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="d6487-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="d6487-444">Aby uzyskać informacje na temat łagodne zamykanie tooimplement, zobacz [łagodne zamykanie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="d6487-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="d6487-445">Witaj kodu w hello `ConvertImageToThumbnailJPG` — metoda (tego nie pokazano) używa klas w hello `System.Drawing` przestrzeni nazw dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="d6487-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="d6487-446">Jednak klasy hello w tej przestrzeni nazw zostały zaprojektowane do użytku z formularzy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6487-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="d6487-447">Nie są one obsługiwane w usłudze systemu Windows lub programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d6487-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="d6487-448">Aby uzyskać więcej informacji o opcjach przetwarzania obrazu, zobacz [Dynamiczne generowanie obrazu](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) i [Bezpośrednie zmienianie rozmiaru obrazu](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="d6487-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="d6487-449">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d6487-449">Next steps</span></span>
<span data-ttu-id="d6487-450">W tym samouczku przedstawiono prostą aplikację wielowarstwową, która używa hello zestaw SDK zadań Webjob dla przetwarzania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="d6487-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="d6487-451">Ta sekcja zawiera sugestie dotyczące dowiedzieć się więcej na temat aplikacje wielowarstwowe platformy ASP.NET i zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="d6487-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="d6487-452">Brak funkcji</span><span class="sxs-lookup"><span data-stu-id="d6487-452">Missing features</span></span>
<span data-ttu-id="d6487-453">Aplikacja Hello została zachowana proste samouczek ułatwiający Rozpoczynanie pracy.</span><span class="sxs-lookup"><span data-stu-id="d6487-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="d6487-454">W aplikacji rzeczywistych można zaimplementować [iniekcji zależności](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) i hello [repozytorium i jednostki pracy wzorce](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), użyj [interfejs umożliwiający rejestrowanie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), użyj [ Migracje EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage danych modelu zmian i użyj [elastyczności połączenia platformy EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage przejściowe błędy sieciowym.</span><span class="sxs-lookup"><span data-stu-id="d6487-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="d6487-455">Skalowanie zadania Webjob</span><span class="sxs-lookup"><span data-stu-id="d6487-455">Scaling WebJobs</span></span>
<span data-ttu-id="d6487-456">Zadania Webjob są uruchamiane w kontekście hello aplikacji sieci web i nie są skalowalne oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="d6487-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="d6487-457">Na przykład jeśli jedno wystąpienie aplikacji sieci web Standard, można mieć tylko jedno wystąpienie procesu tła uruchomiona, a niektóre zasoby serwera hello (procesora CPU, pamięć, itp.), które w przeciwnym razie będą dostępne tooserve zawartości sieci web używa.</span><span class="sxs-lookup"><span data-stu-id="d6487-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="d6487-458">Jeśli ruch jest zależna od czasu dzień lub dzień tygodnia i czy zaplecza hello przetwarzania należy poczekać toodo, toorun Twojego zadań Webjob można zaplanować w czasie mniejszym natężeniu ruchu.</span><span class="sxs-lookup"><span data-stu-id="d6487-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="d6487-459">Jeśli obciążenie hello nadal jest za duża dla tego rozwiązania, w tym celu można uruchomić hello wewnętrznej bazy danych jako zadanie WebJob w aplikacji sieci web oddzielnych dedykowanych.</span><span class="sxs-lookup"><span data-stu-id="d6487-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="d6487-460">Aplikacja sieci web wewnętrznej bazy danych można następnie skalować niezależnie z aplikacji sieci web frontonu.</span><span class="sxs-lookup"><span data-stu-id="d6487-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="d6487-461">Aby uzyskać więcej informacji, zobacz [skalowanie zadania Webjob](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="d6487-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="d6487-462">Unikanie sieci web aplikacji limit czasu zamykania rozwijanych</span><span class="sxs-lookup"><span data-stu-id="d6487-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="d6487-463">czy toomake Twojego zadań Webjob zawsze są uruchomione i uruchomione na wszystkich wystąpień aplikacji sieci web, masz tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) funkcji.</span><span class="sxs-lookup"><span data-stu-id="d6487-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="d6487-464">Przy użyciu hello zestaw SDK zadań Webjob poza zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="d6487-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="d6487-465">Program, który używa hello zestaw SDK zadań Webjob nie ma toorun na platformie Azure w zadanie WebJob.</span><span class="sxs-lookup"><span data-stu-id="d6487-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="d6487-466">Można uruchomić lokalnie i można również uruchomić w innych środowiskach, takich jak usługi w chmurze rola proces roboczy lub usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="d6487-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="d6487-467">Jednak dostępne tylko hello zestaw SDK zadań Webjob pulpitu nawigacyjnego za pomocą aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d6487-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="d6487-468">pulpit nawigacyjny hello toouse masz tooconnect hello sieci web aplikacji toohello konto magazynu używane przez ustawienie parametrów połączenia AzureWebJobsDashboard hello na powitania **Konfiguruj** kartę hello klasycznego portalu.</span><span class="sxs-lookup"><span data-stu-id="d6487-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="d6487-469">Następnie można uzyskać toohello pulpitu nawigacyjnego za pomocą hello następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="d6487-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="d6487-470">https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions</span><span class="sxs-lookup"><span data-stu-id="d6487-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="d6487-471">Aby uzyskać więcej informacji, zobacz [pobierania pulpitu nawigacyjnego lokalnego środowiska deweloperskiego przy użyciu zestawu SDK zadań Webjob hello](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ale należy pamiętać, że widoczny jest stara nazwa ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="d6487-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="d6487-472">Więcej dokumentacji zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="d6487-472">More WebJobs documentation</span></span>
<span data-ttu-id="d6487-473">Aby uzyskać więcej informacji, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="d6487-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
