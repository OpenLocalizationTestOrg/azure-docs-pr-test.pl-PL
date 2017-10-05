---
title: "Utwórz zadanie WebJob platformy .NET w usłudze Azure App Service | Dokumentacja firmy Microsoft"
description: "Utwórz aplikację wielowarstwową przy użyciu platformy ASP.NET MVC i platformy Azure. Fronton jest uruchamiany w aplikacji sieci web w usłudze Azure App Service i Wstecz działa zakończenia jako zadanie WebJob. Aplikacja korzysta z programu Entity Framework, bazy danych SQL i kolejek usługi Azure storage i obiektów blob."
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
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="daee8-105">Tworzenie zadania WebJob .NET w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="daee8-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="daee8-106">Ten samouczek pokazuje, jak napisać kod dla prostą aplikację ASP.NET MVC 5 wielowarstwowej, która używa [zestaw SDK zadań Webjob](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="daee8-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="daee8-107">Celem [zestaw SDK zadań Webjob](websites-webjobs-resources.md) jest uprościć kod zapisu typowych zadań, które mogą wykonywać zadanie WebJob, takich jak przetwarzania obrazu, przetwarzanie kolejki, agregacja danych RSS, plików obsługi i wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="daee8-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="daee8-108">Zestaw SDK zadań Webjob ma wbudowane funkcje do pracy z usługą Azure Storage i usługi Service Bus, planowanie zadań i obsługa błędów i wielu innych typowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="daee8-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="daee8-109">Ponadto ona ma być rozszerzony, a istnieje [repozytorium typu open source dla rozszerzeń](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="daee8-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="daee8-110">Przykładowa aplikacja to reklamowa Tablica ogłoszeń.</span><span class="sxs-lookup"><span data-stu-id="daee8-110">The sample application is an advertising bulletin board.</span></span> <span data-ttu-id="daee8-111">Użytkownicy można przekazywać obrazy dla reklam i procesu zaplecza konwertuje obrazy miniatur.</span><span class="sxs-lookup"><span data-stu-id="daee8-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span></span> <span data-ttu-id="daee8-112">Na stronie listy ad miniatury, a na stronie Szczegóły ad pokazuje obrazu w pełnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="daee8-112">The ad list page shows the thumbnails, and the ad details page shows the full-size image.</span></span> <span data-ttu-id="daee8-113">Poniżej przedstawiono zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="daee8-113">Here's a screenshot:</span></span>

![Lista reklam](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="daee8-115">Ta przykładowa aplikacja działa z [kolejek Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) i [obiekty BLOB platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="daee8-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="daee8-116">Samouczek pokazuje, jak wdrożyć aplikację na [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) i [bazy danych SQL Azure](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="daee8-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="daee8-117"><a id="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="daee8-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="daee8-118">W tym samouczku założono, że wiesz, jak pracować z [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projekty w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daee8-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="daee8-119">Samouczek pierwotnie sformatowano dla programu Visual Studio 2013, ale może być używany z nowszej wersji programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daee8-119">The tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="daee8-120">Jeśli używasz programu Visual Studio 2015 lub 2017, zwróć uwagę, że przed uruchomieniem aplikacji lokalnie, należy zmienić `Data Source` część ciągu połączenia bazy danych LocalDB programu SQL Server w plikach Web.config i App.config z `Data Source=(localdb)\v11.0` do `Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="daee8-120">If you are using Visual Studio 2015 or 2017, make note that before you run the application locally, you must change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="daee8-121"><a name="note"></a>Musi mieć konto platformy Azure do ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="daee8-121"><a name="note"></a>You must have an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="daee8-122">Możesz [otworzyć bezpłatne konto platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): otrzymasz kredyt, że można użyć do wypróbowania płatnych usług Azure, a nawet po wyczerpaniu, można zachować konto i korzystać z bezpłatnych usług platformy Azure, takich jak witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="daee8-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use to try out paid Azure services, and even after they're used up, you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="daee8-123">Karta kredytowa nie zostanie obciążona, chyba że jawnie zmienisz ustawienia i poprosisz o jej obciążenie.</span><span class="sxs-lookup"><span data-stu-id="daee8-123">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
> * <span data-ttu-id="daee8-124">Możesz [aktywowania Azure miesięczne środki dla subskrybentów usługi Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): subskrypcji otrzymasz kredyt, co miesiąc, używanego programu płatnych usług Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="daee8-125">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="daee8-125">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="daee8-126">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="daee8-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="daee8-127"><a id="learn"></a>Dowiesz się</span><span class="sxs-lookup"><span data-stu-id="daee8-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="daee8-128">Samouczek przedstawia sposób wykonywania następujących zadań:</span><span class="sxs-lookup"><span data-stu-id="daee8-128">The tutorial shows how to do the following tasks:</span></span>

* <span data-ttu-id="daee8-129">Włącz komputer dla rozwoju platformy Azure przez zainstalowanie zestawu Azure SDK (tylko dla programu Visual Studio 2013 i użytkowników 2015).</span><span class="sxs-lookup"><span data-stu-id="daee8-129">Enable your machine for Azure development by installing the Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="daee8-130">Utwórz projekt aplikacji konsoli, która automatycznie wdraża jako zadanie WebJob platformy Azure, podczas wdrażania projektu sieci web skojarzony.</span><span class="sxs-lookup"><span data-stu-id="daee8-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span></span>
* <span data-ttu-id="daee8-131">Przetestuj zestaw SDK zadań Webjob wewnętrznej bazy danych lokalnie na komputerze dewelopera.</span><span class="sxs-lookup"><span data-stu-id="daee8-131">Test a WebJobs SDK backend locally on the development computer.</span></span>
* <span data-ttu-id="daee8-132">Publikowanie aplikacji z zapleczem zadania Webjob do aplikacji sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="daee8-132">Publish an application with a WebJobs backend to a web app in App Service.</span></span>
* <span data-ttu-id="daee8-133">Przekazywanie plików i zapisywanie ich w usłudze obiektów Blob platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-133">Upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="daee8-134">Używanie zestawu SDK zadań Webjob Azure do pracy z obiektów blob i kolejek usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="daee8-134">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="daee8-135"><a id="contosoads"></a>Architektura aplikacji</span><span class="sxs-lookup"><span data-stu-id="daee8-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="daee8-136">Przykładowa aplikacja korzysta z [wzorzec skoncentrowane kolejki pracy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) do obciążające pracy obciążające Procesor z tworzeniem miniatur do procesu zaplecza.</span><span class="sxs-lookup"><span data-stu-id="daee8-136">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span></span>

<span data-ttu-id="daee8-137">Aplikacja przechowuje reklamy w bazie danych SQL oraz tworzy tabele i uzyskuje dostęp do danych za pomocą funkcji Code First platformy Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="daee8-137">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="daee8-138">W przypadku każdej reklamy baza danych zawiera dwa adresy URL: jeden dla obrazu w pełnym rozmiarze i jeden do miniatury.</span><span class="sxs-lookup"><span data-stu-id="daee8-138">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span></span>

![Tabela reklam](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="daee8-140">Gdy użytkownik przesyła obraz, aplikacji sieci web zapisuje obraz w [obiektów blob platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), oraz informacje o reklamie są przechowywane w bazie danych przy użyciu adresu URL, który wskazuje obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="daee8-140">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="daee8-141">W tym samym czasie w kolejce platformy Azure jest zapisywany komunikat.</span><span class="sxs-lookup"><span data-stu-id="daee8-141">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="daee8-142">W ramach procesu zaplecza uruchomiony jako zadanie WebJob platformy Azure zestaw SDK zadań Webjob sonduje kolejki wiadomości.</span><span class="sxs-lookup"><span data-stu-id="daee8-142">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span></span> <span data-ttu-id="daee8-143">Gdy pojawi się nowy komunikat, zadania WebJob tworzy miniaturę obrazu i aktualizuje pole bazy danych adresu URL miniatury dla danej reklamy.</span><span class="sxs-lookup"><span data-stu-id="daee8-143">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="daee8-144">Poniżej przedstawiono diagram przedstawia interakcje między częściami aplikacji:</span><span class="sxs-lookup"><span data-stu-id="daee8-144">Here's a diagram that shows how the parts of the application interact:</span></span>

![Architektura aplikacji Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="daee8-146">Samouczek instrukcje dotyczą zestawu Azure SDK dla platformy .NET 2.7.1 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="daee8-146">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="daee8-147"><a id="storage"></a>Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="daee8-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="daee8-148">Konto magazynu platformy Azure udostępnia zasoby służące do przechowywania danych kolejek i obiektów blob w chmurze.</span><span class="sxs-lookup"><span data-stu-id="daee8-148">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span> <span data-ttu-id="daee8-149">Jest on używany również przez zestaw SDK zadań Webjob do przechowywania danych rejestrowania pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="daee8-149">It's also used by the WebJobs SDK to store logging data for the dashboard.</span></span>

<span data-ttu-id="daee8-150">W przypadku aplikacji rzeczywistych można zwykle utworzyć oddzielne konta dla danych aplikacji porównywanych z danymi rejestrowania oraz oddzielne konta dla danych testowych porównywanych z danymi produkcyjnymi.</span><span class="sxs-lookup"><span data-stu-id="daee8-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="daee8-151">W tym samouczku będzie używane tylko jedno konto.</span><span class="sxs-lookup"><span data-stu-id="daee8-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="daee8-152">Otwórz **Eksploratora serwera** okna w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daee8-152">Open the **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="daee8-153">Kliknij prawym przyciskiem myszy **Azure** węzeł, a następnie kliknij przycisk **nawiązywanie połączenia z subskrypcją platformy Microsoft Azure...** .</span><span class="sxs-lookup"><span data-stu-id="daee8-153">Right-click the **Azure** node, and then click **Connect to Microsoft Azure Subscription...**.</span></span>
   
   ![Nawiązywanie połączenia z usługą Azure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="daee8-155">Zaloguj się przy użyciu poświadczeń konta platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="daee8-156">Kliknij prawym przyciskiem myszy **magazynu** w obszarze węzła Azure, a następnie kliknij przycisk **Utwórz konto magazynu**.</span><span class="sxs-lookup"><span data-stu-id="daee8-156">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Tworzenie konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="daee8-158">W **Utwórz konto magazynu** okna dialogowego, wprowadź nazwę konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="daee8-158">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="daee8-159">Nazwa musi być muszą być unikatowe (inne konto magazynu platformy Azure mogą mieć takiej samej nazwy).</span><span class="sxs-lookup"><span data-stu-id="daee8-159">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="daee8-160">Jeśli wprowadzona nazwa jest już w użyciu, uzyskasz możliwość go zmienić.</span><span class="sxs-lookup"><span data-stu-id="daee8-160">If the name you enter is already in use, you'll get a chance to change it.</span></span>

    <span data-ttu-id="daee8-161">Adres URL, aby uzyskać dostęp do konta magazynu będzie *{nazwa}*. core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="daee8-161">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="daee8-162">Ustaw **Region lub grupę koligacji** listy rozwijanej do najbliższego regionu.</span><span class="sxs-lookup"><span data-stu-id="daee8-162">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="daee8-163">To ustawienie określa, w którym Centrum danych Azure będą obsługiwać Twoje konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="daee8-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="daee8-164">W tym samouczku wybór nie należy to znaczącej różnicy.</span><span class="sxs-lookup"><span data-stu-id="daee8-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="daee8-165">Jednak w przypadku aplikacji sieci web produkcji mają serwera sieci web i konta magazynu w tym samym regionie, aby zminimalizować opóźnienie i danych opłaty za wyjście.</span><span class="sxs-lookup"><span data-stu-id="daee8-165">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="daee8-166">Aplikacja sieci web (do którego należy utworzyć później) centrum danych powinien być możliwie jak najbardziej zbliżone do przeglądarki, aby zminimalizować czas oczekiwania na dostęp do aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="daee8-166">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span></span>
7. <span data-ttu-id="daee8-167">Z listy rozwijanej **Replikacja** wybierz wartość **Lokalnie nadmiarowy**.</span><span class="sxs-lookup"><span data-stu-id="daee8-167">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="daee8-168">Jeśli na koncie magazynu włączono replikację geograficzną, przechowywana zawartość jest replikowana do pomocniczego centrum danych. Pozwala to na przejście do trybu failover w tej lokalizacji w przypadku poważnej awarii w lokalizacji głównej.</span><span class="sxs-lookup"><span data-stu-id="daee8-168">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="daee8-169">Replikacja geograficzna może pociągnąć za sobą dodatkowe koszty.</span><span class="sxs-lookup"><span data-stu-id="daee8-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="daee8-170">W przypadku kont testowych i projektowych przeważnie nie chcesz płacić za replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="daee8-170">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="daee8-171">Aby uzyskać więcej informacji, zobacz temat dotyczący [tworzenia i usuwania konta magazynu oraz zarządzania nim](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="daee8-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="daee8-172">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="daee8-172">Click **Create**.</span></span>

    ![Nowe konto usługi Storage](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="daee8-174"><a id="download"></a>Pobierz aplikację</span><span class="sxs-lookup"><span data-stu-id="daee8-174"><a id="download"></a>Download the application</span></span>
1. <span data-ttu-id="daee8-175">Pobierz i rozpakuj [ukończone rozwiązanie](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="daee8-175">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="daee8-176">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daee8-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="daee8-177">Z **pliku** menu wybierz **Otwórz > Projekt/rozwiązanie**, przejdź do lokalizacji pobranego rozwiązania, a następnie otwórz plik rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="daee8-177">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="daee8-178">Naciśnij kombinację klawiszy CTRL+SHIFT+B w celu skompilowania rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="daee8-178">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="daee8-179">Domyślnie program Visual Studio automatycznie przywraca zawartość pakietu NuGet, która nie została uwzględniona w pliku *ZIP*.</span><span class="sxs-lookup"><span data-stu-id="daee8-179">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="daee8-180">Jeśli pakiety nie zostaną przywrócone, zainstaluj je ręcznie, przechodząc do **Zarządzaj pakietami NuGet dla rozwiązania** okno dialogowe i klikając **przywrócić** u góry po prawej stronie.</span><span class="sxs-lookup"><span data-stu-id="daee8-180">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="daee8-181">W **Eksploratora rozwiązań**, upewnij się, że **ContosoAdsWeb** został wybrany jako projekt startowy.</span><span class="sxs-lookup"><span data-stu-id="daee8-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span></span>

## <span data-ttu-id="daee8-182"><a id="configurestorage"></a>Konfigurowanie aplikacji w celu używania konta magazynu</span><span class="sxs-lookup"><span data-stu-id="daee8-182"><a id="configurestorage"></a>Configure the application to use your storage account</span></span>
1. <span data-ttu-id="daee8-183">Otwórz aplikację *Web.config* pliku w projekcie ContosoAdsWeb.</span><span class="sxs-lookup"><span data-stu-id="daee8-183">Open the application *Web.config* file in the ContosoAdsWeb project.</span></span>

    <span data-ttu-id="daee8-184">Plik zawiera parametry połączenia SQL i parametry połączenia magazynu Azure do pracy z obiektów blob i kolejek.</span><span class="sxs-lookup"><span data-stu-id="daee8-184">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="daee8-185">Parametry połączenia SQL wskazuje [programu SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) bazy danych.</span><span class="sxs-lookup"><span data-stu-id="daee8-185">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="daee8-186">Parametry połączenia magazynu jest przykład symbole zastępcze klucz nazwy i dostępu do konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="daee8-186">The storage connection string is an example that has placeholders for the storage account name and access key.</span></span> <span data-ttu-id="daee8-187">Będzie to zastąpić przy użyciu parametrów połączenia, nazwa i klucz konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="daee8-187">You'll replace this with a connection string that has the name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="daee8-188">Parametry połączenia magazynu nosi nazwę AzureWebJobsStorage, ponieważ jest to nazwa, który korzysta z zestawu SDK WebJobs domyślnie.</span><span class="sxs-lookup"><span data-stu-id="daee8-188">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span></span> <span data-ttu-id="daee8-189">Tej samej nazwie jest używany w tym miejscu, należy ustawić tylko jedną wartość ciągu połączenia w środowisku platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-189">The same name is used here so you have to set only one connection string value in the Azure environment.</span></span>
2. <span data-ttu-id="daee8-190">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy konto magazynu w obszarze **magazynu** węzeł, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="daee8-190">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span></span>

    ![Kliknij przycisk Właściwości konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="daee8-192">W **właściwości** okna, kliknij przycisk **klucze konta magazynu**, a następnie kliknij przycisk wielokropka.</span><span class="sxs-lookup"><span data-stu-id="daee8-192">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span></span>

    ![Klucze konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="daee8-194">Kopiuj **ciąg połączenia**.</span><span class="sxs-lookup"><span data-stu-id="daee8-194">Copy the **Connection String**.</span></span>

    ![Okno dialogowe klucze konta magazynu](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="daee8-196">Zastąp parametry połączenia magazynu w *Web.config* plik został skopiowany ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="daee8-196">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span></span> <span data-ttu-id="daee8-197">Upewnij się, że możesz zaznaczyć wszystko w cudzysłowach, ale bez cudzysłowów przed wklejeniem.</span><span class="sxs-lookup"><span data-stu-id="daee8-197">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span></span>
6. <span data-ttu-id="daee8-198">Otwórz *App.config* plik w projekcie ContosoAdsWebJob.</span><span class="sxs-lookup"><span data-stu-id="daee8-198">Open the *App.config* file in the ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="daee8-199">Ten plik zawiera dwa parametry połączenia magazynu, jeden dla danych aplikacji i jeden dla rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="daee8-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="daee8-200">Możesz użyć oddzielny magazyn kont dla danych aplikacji i rejestrowania i można użyć [konta wielu magazynu dla danych](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="daee8-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="daee8-201">W tym samouczku użyjesz konto jednego magazynu.</span><span class="sxs-lookup"><span data-stu-id="daee8-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="daee8-202">Parametry połączenia mają symbole zastępcze klucze konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="daee8-202">The connection strings have placeholders for the storage account keys.</span></span>

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

    <span data-ttu-id="daee8-203">Domyślnie zestaw SDK zadań Webjob szuka parametry połączenia o nazwie AzureWebJobsStorage i AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="daee8-203">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="daee8-204">Alternatywnie, można [magazynu parametrów połączenia, ale mają i przekaż go w jawnie na `JobHost` obiektu](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="daee8-204">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="daee8-205">Zastąp parametry połączenia magazynu przy użyciu parametrów połączenia, które wcześniej zostały skopiowane.</span><span class="sxs-lookup"><span data-stu-id="daee8-205">Replace both storage connection strings with the connection string you copied earlier.</span></span>
8. <span data-ttu-id="daee8-206">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="daee8-206">Save your changes.</span></span>

## <span data-ttu-id="daee8-207"><a id="run"></a>Uruchamianie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="daee8-207"><a id="run"></a>Run the application locally</span></span>
1. <span data-ttu-id="daee8-208">Aby rozpocząć frontonu sieci web aplikacji, naciśnij kombinację klawiszy CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="daee8-208">To start the web frontend of the application, press CTRL+F5.</span></span>

    <span data-ttu-id="daee8-209">W domyślnej przeglądarce otworzy się do strony głównej.</span><span class="sxs-lookup"><span data-stu-id="daee8-209">The default browser opens to the home page.</span></span> <span data-ttu-id="daee8-210">(Projekt sieci web jest uruchomiona, ponieważ zostały wprowadzone projekt startowy.)</span><span class="sxs-lookup"><span data-stu-id="daee8-210">(The web project runs because you've made it the startup project.)</span></span>

    ![Strona główna aplikacji contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="daee8-212">Można uruchomić zadania WebJob wewnętrznej bazy danych aplikacji, kliknij prawym przyciskiem myszy projekt ContosoAdsWebJob w **Eksploratora rozwiązań**, a następnie kliknij przycisk **debugowania** > **Start nowe wystąpienie**.</span><span class="sxs-lookup"><span data-stu-id="daee8-212">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="daee8-213">Okno aplikacji konsoli otwiera i wyświetla rejestrowanie komunikatów wskazujący, że obiekt JobHost zestawu SDK zadań Webjob został uruchomiony w trybie uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="daee8-213">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span></span>

    ![Okno aplikacji konsoli pokazujący, że działa wewnętrznej bazy danych](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="daee8-215">W przeglądarce, kliknij przycisk **tworzenia Ad**.</span><span class="sxs-lookup"><span data-stu-id="daee8-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="daee8-216">Wprowadź dane testowe, wybierz obraz do przekazania, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="daee8-216">Enter some test data, select an image to upload, and then click **Create**.</span></span>

    ![Tworzenie strony](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="daee8-218">Aplikacja przechodzi do strony indeksu, ale nie wyświetla miniatury nowej reklamy, ponieważ przetwarzanie nie zostało jeszcze przeprowadzone.</span><span class="sxs-lookup"><span data-stu-id="daee8-218">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="daee8-219">W tym samym czasie po krótkim okresie oczekiwania komunikat rejestrowania w oknie aplikacji konsoli Pokazuje, że komunikatu w kolejce został odebrany i został przetworzony.</span><span class="sxs-lookup"><span data-stu-id="daee8-219">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span></span>

    ![Okno aplikacji konsoli przedstawiający przetworzeniu komunikatu w kolejce](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="daee8-221">Po rejestrowanie komunikatów w oknie aplikacji konsoli, Odśwież stronę indeksu, aby zobaczyć miniaturę.</span><span class="sxs-lookup"><span data-stu-id="daee8-221">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span></span>

    ![Strona indeksu](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="daee8-223">Kliknij link **Details** (Szczegóły) obok reklamy, aby wyświetlić obraz w pełnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="daee8-223">Click **Details** for your ad to see the full-size image.</span></span>

    ![Strona szczegółów](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="daee8-225">Działała aplikacja na komputerze lokalnym i używa programu SQL Server, bazy danych znajdującej się na komputerze, ale działa w przypadku kolejek i obiektów blob w chmurze.</span><span class="sxs-lookup"><span data-stu-id="daee8-225">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span></span> <span data-ttu-id="daee8-226">W poniższej sekcji uruchomisz aplikację w chmurze przy użyciu bazy danych w chmurze, a także chmury obiekty BLOB i kolejki.</span><span class="sxs-lookup"><span data-stu-id="daee8-226">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="daee8-227"><a id="runincloud"></a>Uruchamianie aplikacji w chmurze</span><span class="sxs-lookup"><span data-stu-id="daee8-227"><a id="runincloud"></a>Run the application in the cloud</span></span>
<span data-ttu-id="daee8-228">Aby uruchomić aplikację w chmurze, należy wykonać następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="daee8-228">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="daee8-229">Wdrażanie w aplikacjach sieci Web.</span><span class="sxs-lookup"><span data-stu-id="daee8-229">Deploy to Web Apps.</span></span> <span data-ttu-id="daee8-230">Visual Studio automatycznie tworzy nową aplikację sieci web usługi aplikacji i wystąpienie bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="daee8-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="daee8-231">Konfigurowanie aplikacji sieci web do używania konta magazynu i bazy danych Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="daee8-231">Configure the web app to use your Azure SQL database and storage account.</span></span>

<span data-ttu-id="daee8-232">Po utworzeniu niektóre reklamy podczas uruchamiania w chmurze, zostanie wyświetlona pulpitu nawigacyjnego zestaw SDK zadań Webjob, aby zobaczyć zaawansowanej funkcji, które musi oferować monitorowania.</span><span class="sxs-lookup"><span data-stu-id="daee8-232">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span></span>

### <a name="deploy-to-web-apps"></a><span data-ttu-id="daee8-233">Wdrażanie w aplikacjach sieci Web</span><span class="sxs-lookup"><span data-stu-id="daee8-233">Deploy to Web Apps</span></span>

1. <span data-ttu-id="daee8-234">Zamknij przeglądarkę i okna aplikacji konsoli.</span><span class="sxs-lookup"><span data-stu-id="daee8-234">Close the browser and the console application window.</span></span>
2. <span data-ttu-id="daee8-235">Postępuj zgodnie z instrukcjami [publikowania na platformie Azure w usłudze SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sekcji.</span><span class="sxs-lookup"><span data-stu-id="daee8-235">Follow the steps in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="daee8-236">Po wykonaniu kroków wdrażania kontynuować wykonywanie kolejnych zadań w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="daee8-236">After you complete the steps for deploying, continue with the remaining tasks in this article.</span></span>

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="daee8-237">Konfigurowanie aplikacji sieci web do używania konta magazynu i bazy danych Azure SQL</span><span class="sxs-lookup"><span data-stu-id="daee8-237">Configure the web app to use your Azure SQL database and storage account</span></span>
<span data-ttu-id="daee8-238">Zabezpieczeń najlepszym rozwiązaniem jest [należy unikać umieszczania poufne informacje, takie jak parametry połączenia w plikach, które są przechowywane w repozytoriach kodów źródłowych](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="daee8-238">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="daee8-239">Platforma Azure udostępnia sposób, aby to zrobić: można ustawić parametry połączenia i inne wartości ustawienia w środowisku platformy Azure i interfejsy API konfiguracji ASP.NET automatyczne pobranie te wartości po uruchomieniu aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-239">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span></span> <span data-ttu-id="daee8-240">Te wartości zostaną ustawione na platformie Azure, używając **Eksploratora serwera**, portalu Azure, programu Windows PowerShell lub interfejsu wiersza polecenia i platform.</span><span class="sxs-lookup"><span data-stu-id="daee8-240">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span></span> <span data-ttu-id="daee8-241">Aby uzyskać więcej informacji, zobacz [jak ciągi aplikacji i pracy ciągów połączenia](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="daee8-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="daee8-242">W tej sekcji użyjesz **Eksploratora serwera** można ustawić wartości ciągu połączenia na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-242">In this section, you use **Server Explorer** to set connection string values in Azure.</span></span>

1. <span data-ttu-id="daee8-243">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy aplikację sieci web, w obszarze **Azure > App Service > {grupie zasobów}**, a następnie kliknij przycisk **ustawienia widoku**.</span><span class="sxs-lookup"><span data-stu-id="daee8-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="daee8-244">**Aplikacji sieci Web Azure** na zostanie otwarte okno **konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="daee8-244">The **Azure Web App** window opens on the **Configuration** tab.</span></span>
2. <span data-ttu-id="daee8-245">Zmień nazwę parametrów połączenia parametru DefaultConnection na nazwę wybraną podczas konfigurowania bazy danych SQL w [publikowania na platformie Azure w usłudze SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artykułu.</span><span class="sxs-lookup"><span data-stu-id="daee8-245">Change the name of the DefaultConnection connection string to the name you chose when you configured the SQL database in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="daee8-246">Ten ciąg połączenia tworzone automatycznie, podczas tworzenia aplikacji sieci web z skojarzonej bazy danych, więc ma już wartość ciągu połączenia na odpowiednie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-246">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span></span> <span data-ttu-id="daee8-247">Tylko nazwę chcesz zmienić do kodu poszukuje programu.</span><span class="sxs-lookup"><span data-stu-id="daee8-247">You're changing just the name to what your code is looking for.</span></span>
3. <span data-ttu-id="daee8-248">Dodaj dwa nowe parametry połączenia, o nazwie AzureWebJobsStorage i AzureWebJobsDashboard.</span><span class="sxs-lookup"><span data-stu-id="daee8-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="daee8-249">Ustaw typ bazy danych **niestandardowy**i ustaw wartość ciągu połączenia na tę samą wartość, który był wcześniej używany przez *Web.config* i *App.config* plików.</span><span class="sxs-lookup"><span data-stu-id="daee8-249">Set the database type to **Custom**, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span></span> <span data-ttu-id="daee8-250">(Upewnij się, zawierają ciąg całego połączenia, nie tylko klucz dostępu, a nie zawierają znaki cudzysłowu.)</span><span class="sxs-lookup"><span data-stu-id="daee8-250">(Be sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span></span>

    <span data-ttu-id="daee8-251">Te parametry połączenia są używane przez zestaw SDK zadań Webjob, jeden dla danych aplikacji i jeden do rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="daee8-251">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="daee8-252">Jak przedstawiono wcześniej, jeden dla danych aplikacji jest również używany przez kod frontonu sieci web.</span><span class="sxs-lookup"><span data-stu-id="daee8-252">As you saw earlier, the one for application data is also used by the web front-end code.</span></span>
4. <span data-ttu-id="daee8-253">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="daee8-253">Click **Save**.</span></span>

    ![Parametry połączenia w portalu Azure](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="daee8-255">W **Eksploratora serwera**, kliknij prawym przyciskiem myszy aplikację sieci web, a następnie kliknij przycisk **zatrzymać**.</span><span class="sxs-lookup"><span data-stu-id="daee8-255">In **Server Explorer**, right-click the web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="daee8-256">Po zatrzymaniu aplikacji sieci web, ponownie kliknij prawym przyciskiem myszy aplikację sieci web, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="daee8-256">After the web app stops, right-click the web app again, and then click **Start**.</span></span>

   <span data-ttu-id="daee8-257">Zadania WebJob jest uruchamiana automatycznie, gdy opublikujesz, ale zatrzymuje go po wprowadzeniu zmiany konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="daee8-257">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="daee8-258">Aby uruchomić go ponownie, można ponownie uruchomić aplikacji sieci web lub ponownego uruchomienia zadania WebJob w [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="daee8-258">To restart it, you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="daee8-259">Ogólnie zaleca się ponowne uruchomienie aplikacji sieci web po zmianie konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="daee8-259">It's generally recommended to restart the web app after a configuration change.</span></span>
7. <span data-ttu-id="daee8-260">Odśwież okno przeglądarki, które ma adres URL aplikacji sieci web na pasku adresu.</span><span class="sxs-lookup"><span data-stu-id="daee8-260">Refresh the browser window that has the web app URL in its address bar.</span></span>

    <span data-ttu-id="daee8-261">Zostanie wyświetlona strona główna.</span><span class="sxs-lookup"><span data-stu-id="daee8-261">The home page appears.</span></span>
8. <span data-ttu-id="daee8-262">Utwórz reklamę, jak w przypadku należy [lokalnego uruchomienia aplikacji](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="daee8-262">Create an ad, as you did when you [ran the application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="daee8-263">Pokazuje stronę indeksu bez miniatur na początku.</span><span class="sxs-lookup"><span data-stu-id="daee8-263">The Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="daee8-264">Odśwież stronę za kilka sekund i pojawi się miniatury.</span><span class="sxs-lookup"><span data-stu-id="daee8-264">Refresh the page after a few seconds and the thumbnail appears.</span></span>

   <span data-ttu-id="daee8-265">Jeśli nie ma miniatury, może być konieczne Zaczekaj minutę lub tak dla zadania WebJob do ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="daee8-265">If the thumbnail doesn't appear, you might have to wait a minute or so for the WebJob to restart.</span></span> <span data-ttu-id="daee8-266">Jeśli po chwili, nadal nie widzisz miniatury podczas odświeżania strony, zadania WebJob nie może być uruchomiony automatycznie.</span><span class="sxs-lookup"><span data-stu-id="daee8-266">If after a while, you still don't see the thumbnail when you refresh the page, the WebJob might not have started automatically.</span></span> <span data-ttu-id="daee8-267">W takim przypadku przejdź do **usługi aplikacji** bloku w [portalu Azure](https://portal.azure.com/), Znajdź aplikację sieci web, a następnie kliknij przycisk **Start**.</span><span class="sxs-lookup"><span data-stu-id="daee8-267">In that case, go to the **App Services** blade in the [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-the-webjobs-sdk-dashboard"></a><span data-ttu-id="daee8-268">Widok pulpitu nawigacyjnego zestaw SDK zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="daee8-268">View the WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="daee8-269">W [portalu Azure](https://portal.azure.com/), wybierz pozycję **blok App Services**Znajdź aplikację sieci web i zaznacz **Webjob**.</span><span class="sxs-lookup"><span data-stu-id="daee8-269">In the [Azure portal](https://portal.azure.com/), select the **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="daee8-270">Wybierz **dzienniki** kartę.</span><span class="sxs-lookup"><span data-stu-id="daee8-270">Select the **Logs** tab.</span></span>

    ![Karta dzienniki](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="daee8-272">Otwiera nową kartę przeglądarki do pulpitu nawigacyjnego, zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="daee8-272">A new browser tab opens to the WebJobs SDK dashboard.</span></span> <span data-ttu-id="daee8-273">Pulpit nawigacyjny pokazuje, że zadania WebJob działa i czy zawiera listę funkcji w kodzie, która wyzwoliła zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="daee8-273">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="daee8-274">Kliknij jedną z funkcji, aby wyświetlić szczegółowe informacje o jego wykonywania.</span><span class="sxs-lookup"><span data-stu-id="daee8-274">Click one of the functions to see details about its execution.</span></span>

    ![Zestaw SDK zadań Webjob pulpitu nawigacyjnego](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![Zestaw SDK zadań Webjob pulpitu nawigacyjnego](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="daee8-277">**Funkcja powtarzania** framework zestaw SDK zadań Webjob ponownie wywołać funkcji powoduje, że przycisk na tej stronie i daje możliwość zmiany danych, najpierw przekazany do funkcji.</span><span class="sxs-lookup"><span data-stu-id="daee8-277">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span></span>

> [!NOTE]
> <span data-ttu-id="daee8-278">Po zakończeniu testowania, rozważ usunięcie aplikacji sieci web, konta magazynu i wystąpienie bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="daee8-278">When you're finished testing, consider deleting the web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="daee8-279">Aplikacja sieci web jest bezpłatne, ale wystąpienie konta i bazy danych magazynu SQL Naliczanie opłat (chociaż, ze względu na mały rozmiar minimalny).</span><span class="sxs-lookup"><span data-stu-id="daee8-279">The web app is free, but the SQL storage account and database instance accrue charges (albeit, minimal due to the small size).</span></span> <span data-ttu-id="daee8-280">Ponadto pozostawienie uruchomieniu aplikacji sieci web, każda osoba, która znajdzie adres URL można tworzyć i wyświetlać reklamy.</span><span class="sxs-lookup"><span data-stu-id="daee8-280">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="daee8-281">Usuń aplikację sieci web</span><span class="sxs-lookup"><span data-stu-id="daee8-281">Delete your web app</span></span>
<span data-ttu-id="daee8-282">W portalu, przejdź do **usługi aplikacji** bloku, Znajdź i wybierz aplikację sieci web, a następnie kliknij **usunąć**.</span><span class="sxs-lookup"><span data-stu-id="daee8-282">In the portal, go to the **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="daee8-283">Jeśli chcesz tylko czasowo uniemożliwić innym użytkownikom uzyskiwanie dostępu do aplikacji sieci web, kliknij przycisk **zatrzymać** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="daee8-283">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span></span> <span data-ttu-id="daee8-284">W takim przypadku opłaty będą nadal naliczane dla konta magazynu i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="daee8-284">In that case, charges will continue to accrue for the SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="daee8-285">Usuwanie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="daee8-285">Delete your storage account</span></span>
<span data-ttu-id="daee8-286">Aby usunąć konta magazynu, zobacz [usuwania konta magazynu](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="daee8-286">To delete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="daee8-287">Usunięcie bazy danych</span><span class="sxs-lookup"><span data-stu-id="daee8-287">Delete your database</span></span>
<span data-ttu-id="daee8-288">Aby usunąć bazę danych SQL, zobacz [interfejsu API REST bazy danych SQL Azure](https://docs.microsoft.com/rest/api/sql/) dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="daee8-288">To delete your SQL database, see the [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="daee8-289"><a id="create"></a>Tworzenie aplikacji od początku</span><span class="sxs-lookup"><span data-stu-id="daee8-289"><a id="create"></a>Create the application from scratch</span></span>
<span data-ttu-id="daee8-290">W tej sekcji należy wykonać następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="daee8-290">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="daee8-291">Tworzenie rozwiązania Visual Studio z projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="daee8-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="daee8-292">Dodawanie projektu biblioteki klas dla danych warstwy dostępu, która jest udostępniana między frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="daee8-292">Add a class library project for the data access layer that is shared between the front end and back end.</span></span>
* <span data-ttu-id="daee8-293">Dodaj projekt aplikacji konsoli wewnętrznej bazy danych, z włączonym wdrażaniem zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="daee8-293">Add a Console Application project for the backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="daee8-294">Dodawanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="daee8-294">Add NuGet packages.</span></span>
* <span data-ttu-id="daee8-295">Ustawianie odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="daee8-295">Set project references.</span></span>
* <span data-ttu-id="daee8-296">Skopiuj pliki kodu i konfiguracji aplikacji z pobraną aplikację, którą doświadczenie z poprzedniej sekcji samouczka.</span><span class="sxs-lookup"><span data-stu-id="daee8-296">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span></span>
* <span data-ttu-id="daee8-297">Przejrzyj części kodu, współdziałające z obiekty BLOB platformy Azure i kolejek oraz zestaw SDK zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="daee8-297">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="daee8-298">Tworzenie rozwiązań programu Visual Studio z projektu sieci web i projektu biblioteki klas</span><span class="sxs-lookup"><span data-stu-id="daee8-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="daee8-299">W programie Visual Studio, wybierz **pliku** > **nowy** > **projektu**.</span><span class="sxs-lookup"><span data-stu-id="daee8-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="daee8-300">W **nowy projekt** okno dialogowe, wybierz **Visual C#** > **Web** > **aplikacji sieci Web platformy ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="daee8-300">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="daee8-301">Nazwij projekt ContosoAdsWeb, nazwa rozwiązania ContosoAdsWebJobsSDK (zmiana nazwy rozwiązania, jeśli umieścić go w tym samym folderze co pobranego rozwiązania), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="daee8-301">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span></span>

    ![Nowy projekt](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="daee8-303">W **nowej aplikacji sieci Web ASP.NET** okno dialogowe, wybierz szablon MVC, a następnie wybierz **Zmień uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="daee8-303">In the **New ASP.NET Web Application** dialog, choose the MVC template, and select **Change Authentication**.</span></span>

    ![Zmienianie uwierzytelniania](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="daee8-305">W **Zmień uwierzytelnianie** okno dialogowe, wybierz **bez uwierzytelniania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="daee8-305">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Bez uwierzytelniania](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="daee8-307">W **nowej aplikacji sieci Web ASP.NET** okna dialogowego, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="daee8-307">In the **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="daee8-308">Program Visual Studio tworzy rozwiązanie i projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="daee8-308">Visual Studio creates the solution and the web project.</span></span>
7. <span data-ttu-id="daee8-309">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy rozwiązanie (nie projekt) i wybierz **Dodaj** > **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="daee8-309">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="daee8-310">W **Dodawanie nowego projektu** okno dialogowe, wybierz **Visual C#** > **Windows Desktop klasycznego** > **biblioteki klas (.NET Framework)** szablonu.</span><span class="sxs-lookup"><span data-stu-id="daee8-310">In the **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="daee8-311">Nazwij projekt *ContosoAdsCommon*, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="daee8-311">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="daee8-312">Ten projekt będzie zawierać kontekst Entity Framework, jak i model danych, który będzie używany zarówno frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="daee8-312">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span></span> <span data-ttu-id="daee8-313">Alternatywnie można zdefiniować klasy związane z platformą EF w projekcie sieci web i odwoływać się do tego projektu z projektu zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="daee8-313">As an alternative, you could define the EF-related classes in the web project and reference that project from the WebJob project.</span></span> <span data-ttu-id="daee8-314">Ale następnie projektu zadania WebJob musi odwołania do zestawów sieci web, których nie potrzebuje.</span><span class="sxs-lookup"><span data-stu-id="daee8-314">But, then your WebJob project would have a reference to web assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="daee8-315">Dodaj projekt aplikacji konsoli z włączonym wdrażaniem zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="daee8-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="daee8-316">Kliknij prawym przyciskiem myszy projekt sieci web (nie rozwiązania lub projektu biblioteki klas), a następnie kliknij przycisk **Dodaj** > **nowy projekt zadania WebJob Azure**.</span><span class="sxs-lookup"><span data-stu-id="daee8-316">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Nowe zaznaczenie menu projektu zadania WebJob platformy Azure](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="daee8-318">W **dodać zadania WebJob Azure** okna dialogowego, wprowadź ContosoAdsWebJob jednocześnie jako **Nazwa projektu** i **Nazwa zadania WebJob**.</span><span class="sxs-lookup"><span data-stu-id="daee8-318">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span></span> <span data-ttu-id="daee8-319">Pozostaw **tryb uruchomienia zadania WebJob** ustawioną **Uruchom stale**.</span><span class="sxs-lookup"><span data-stu-id="daee8-319">Leave **WebJob run mode** set to **Run Continuously**.</span></span>
3. <span data-ttu-id="daee8-320">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="daee8-320">Click **OK**.</span></span>

   <span data-ttu-id="daee8-321">Program Visual Studio tworzy aplikacja Konsolowa, która jest skonfigurowana do wdrożenia jako zadanie WebJob zawsze, gdy wdrażanie projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="daee8-321">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span></span> <span data-ttu-id="daee8-322">W tym celu wykonać następujące zadania po utworzeniu projektu:</span><span class="sxs-lookup"><span data-stu-id="daee8-322">To do that, it performed the following tasks after creating the project:</span></span>

   * <span data-ttu-id="daee8-323">Dodaje *zadania webjob publikowania settings.json* plików w folderze właściwości projektu zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="daee8-323">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span></span>
   * <span data-ttu-id="daee8-324">Dodaje *list.json webjob* plików w folderze właściwości projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="daee8-324">Added a *webjobs-list.json* file in the web project Properties folder.</span></span>
   * <span data-ttu-id="daee8-325">Zainstalowany pakiet Microsoft.Web.WebJobs.Publish NuGet projektu zadania WebJob.</span><span class="sxs-lookup"><span data-stu-id="daee8-325">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span></span>

   <span data-ttu-id="daee8-326">Aby uzyskać więcej informacji na temat tych zmian, zobacz [wdrażanie zadań Webjob za pomocą programu Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="daee8-326">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="daee8-327">Dodawanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="daee8-327">Add NuGet packages</span></span>
<span data-ttu-id="daee8-328">Szablon nowego projektu dla projektu zadania WebJob automatycznie instaluje pakiet NuGet zestawu SDK zadań Webjob [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) i jego zależności.</span><span class="sxs-lookup"><span data-stu-id="daee8-328">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="daee8-329">Jedna z zależności zestawu SDK zadań Webjob, które jest instalowane automatycznie w projektu zadania WebJob jest biblioteka klienta magazynu Azure (SCL).</span><span class="sxs-lookup"><span data-stu-id="daee8-329">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="daee8-330">Jednak należy dodać go do projektu sieci web do pracy z obiektów blob i kolejek.</span><span class="sxs-lookup"><span data-stu-id="daee8-330">However, you need to add it to the web project to work with blobs and queues.</span></span>

1. <span data-ttu-id="daee8-331">Otwórz **Zarządzaj pakietami NuGet** okna dialogowego dla rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="daee8-331">Open the **Manage NuGet Packages** dialog for the solution.</span></span>
2. <span data-ttu-id="daee8-332">W okienku po lewej stronie wybierz **zainstalowane pakiety**.</span><span class="sxs-lookup"><span data-stu-id="daee8-332">In the left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="daee8-333">Znajdź *usługi Azure Storage* pakietu, a następnie kliknij przycisk **Zarządzaj**.</span><span class="sxs-lookup"><span data-stu-id="daee8-333">Find the *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="daee8-334">W **Wybierz projekty** wybierz **ContosoAdsWeb** pole wyboru, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="daee8-334">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="daee8-335">Wszystkie trzy projekty Użyj programu Entity Framework do pracy z danymi w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="daee8-335">All three projects use the Entity Framework to work with data in SQL Database.</span></span>
5. <span data-ttu-id="daee8-336">W okienku po lewej stronie wybierz **Online**.</span><span class="sxs-lookup"><span data-stu-id="daee8-336">In the left pane, select **Online**.</span></span>
6. <span data-ttu-id="daee8-337">Znajdź pakiet NuGet *EntityFramework*, a następnie zainstaluj go we wszystkich trzech projektach.</span><span class="sxs-lookup"><span data-stu-id="daee8-337">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="daee8-338">Ustawianie odwołań do projektu</span><span class="sxs-lookup"><span data-stu-id="daee8-338">Set project references</span></span>
<span data-ttu-id="daee8-339">Sieć web i projektów zadania WebJob pracy z bazy danych SQL, tak zarówno potrzebują odwołania do projektu ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="daee8-339">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="daee8-340">W projekcie ContosoAdsWeb ustaw odwołanie do projektu ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="daee8-340">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="daee8-341">(Kliknij prawym przyciskiem myszy projekt ContosoAdsWeb, a następnie kliknij przycisk **Dodaj** > **odwołania**.</span><span class="sxs-lookup"><span data-stu-id="daee8-341">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="daee8-342">W **Menedżera odwołań** okno dialogowe, wybierz opcję **projekty** > **rozwiązania** > **ContosoAdsCommon**, a następnie kliknij przycisk **OK**.)</span><span class="sxs-lookup"><span data-stu-id="daee8-342">In the **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="daee8-343">Projektu zadania WebJob musi odwołań do pracy z obrazami i uzyskać dostęp do parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="daee8-343">The WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="daee8-344">W projekcie ContosoAdsWebJob Ustaw odwołanie do `System.Drawing` i `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="daee8-344">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="daee8-345">Dodawanie plików kodu i konfiguracji</span><span class="sxs-lookup"><span data-stu-id="daee8-345">Add code and configuration files</span></span>
<span data-ttu-id="daee8-346">Nie są wyświetlane w tym samouczku jak [utworzyć przy użyciu funkcji szkieletów widoków i kontrolerów MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), jak do [pisania kodu programu Entity Framework, który współpracuje z baz danych programu SQL Server](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), lub [podstawy programowania asynchronicznego w programie ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="daee8-346">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="daee8-347">Tak, czy pozostaje zrobić to skopiować kod i konfiguracja pliki z pobranego rozwiązania do nowego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="daee8-347">So, all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="daee8-348">Po wykonaniu tej czynności, w poniższych sekcjach Pokaż i objaśnione części kodu.</span><span class="sxs-lookup"><span data-stu-id="daee8-348">After you do that, the following sections show and explain key parts of the code.</span></span>

<span data-ttu-id="daee8-349">Aby dodać pliki do projektu lub folderu, kliknij prawym przyciskiem myszy projekt lub folder, a następnie kliknij kolejno pozycje **Dodaj** > **Istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="daee8-349">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="daee8-350">Wybierz pliki, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="daee8-350">Select the files you want and click **Add**.</span></span> <span data-ttu-id="daee8-351">Jeśli pojawi się pytanie, czy chcesz zastąpić istniejące pliki, kliknij pozycję **Tak**.</span><span class="sxs-lookup"><span data-stu-id="daee8-351">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="daee8-352">W projekcie ContosoAdsCommon Usuń *Class1.cs* i Dodaj w jego miejsce następujące pliki z pobranego projektu.</span><span class="sxs-lookup"><span data-stu-id="daee8-352">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span></span>

   * <span data-ttu-id="daee8-353">*AD.CS*</span><span class="sxs-lookup"><span data-stu-id="daee8-353">*Ad.cs*</span></span>
   * <span data-ttu-id="daee8-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="daee8-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="daee8-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="daee8-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="daee8-356">W projekcie ContosoAdsWeb dodaj poniższe pliki z pobranego projektu.</span><span class="sxs-lookup"><span data-stu-id="daee8-356">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="daee8-357">*Plik Web.config*</span><span class="sxs-lookup"><span data-stu-id="daee8-357">*Web.config*</span></span>
   * <span data-ttu-id="daee8-358">*Global.asax.CS*</span><span class="sxs-lookup"><span data-stu-id="daee8-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="daee8-359">W *kontrolerów* folder: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="daee8-359">In the *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="daee8-360">W *Views\Shared* folder: *_Layout.cshtml* pliku</span><span class="sxs-lookup"><span data-stu-id="daee8-360">In the *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="daee8-361">W *Views\Home* folder: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="daee8-361">In the *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="daee8-362">W *Views\Ad* folder (najpierw utwórz folder): pięć *.cshtml* plików</span><span class="sxs-lookup"><span data-stu-id="daee8-362">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="daee8-363">W projekcie ContosoAdsWebJob należy dodać następujące pliki z pobranego projektu.</span><span class="sxs-lookup"><span data-stu-id="daee8-363">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="daee8-364">*App.config* (Zmień filtr typu plików, aby **wszystkie pliki**)</span><span class="sxs-lookup"><span data-stu-id="daee8-364">*App.config* (change the file type filter to **All Files**)</span></span>
   * <span data-ttu-id="daee8-365">*Plik program.CS*</span><span class="sxs-lookup"><span data-stu-id="daee8-365">*Program.cs*</span></span>
   * <span data-ttu-id="daee8-366">*Functions.CS*</span><span class="sxs-lookup"><span data-stu-id="daee8-366">*Functions.cs*</span></span>

<span data-ttu-id="daee8-367">Można teraz kompilacji, uruchamiania i wdrażania aplikacji, zgodnie z instrukcją wcześniej w samouczku.</span><span class="sxs-lookup"><span data-stu-id="daee8-367">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span></span> <span data-ttu-id="daee8-368">Przed tym, jednak zatrzymać zadania WebJob, że nadal działa w pierwszej wdrożonej w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="daee8-368">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span></span> <span data-ttu-id="daee8-369">W przeciwnym razie tego zadania WebJob będzie przetwarzać wiadomości w kolejce utworzony lokalnie lub za pomocą aplikacji uruchomionych w nowej aplikacji sieci web, ponieważ wszystkie korzystają z tego samego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="daee8-369">Otherwise, that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span></span>

## <span data-ttu-id="daee8-370"><a id="code"></a>Przegląd kodu aplikacji</span><span class="sxs-lookup"><span data-stu-id="daee8-370"><a id="code"></a>Review the application code</span></span>
<span data-ttu-id="daee8-371">W poniższych sekcjach opisano kod powiązany z pracą z zestawu SDK zadań Webjob i usługi Azure Storage obiekty BLOB i kolejki.</span><span class="sxs-lookup"><span data-stu-id="daee8-371">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="daee8-372">Dla kodu specyficzne dla zestawu SDK zadań Webjob, przejdź do [Program.cs i Functions.cs](#programcs) sekcje.</span><span class="sxs-lookup"><span data-stu-id="daee8-372">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="daee8-373">ContosoAdsCommon — Ad.cs</span><span class="sxs-lookup"><span data-stu-id="daee8-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="daee8-374">Plik Ad.cs definiuje wyliczenia związane z kategoriami reklam i klasą jednostki POCO dla informacji o reklamach.</span><span class="sxs-lookup"><span data-stu-id="daee8-374">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="daee8-375">ContosoAdsCommon — ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="daee8-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="daee8-376">Klasa ContosoAdsContext Określa, czy klasa Ad jest używany w kolekcji DbSet Entity Framework są przechowywane w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="daee8-376">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="daee8-377">Klasa ma dwa konstruktory.</span><span class="sxs-lookup"><span data-stu-id="daee8-377">The class has two constructors.</span></span> <span data-ttu-id="daee8-378">Pierwszy jest używany przez projekt sieci web i określa nazwę parametrów połączenia, które są przechowywane w pliku Web.config lub środowisko uruchomieniowe platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-378">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span></span> <span data-ttu-id="daee8-379">Drugi konstruktor umożliwia przekazywanie rzeczywistych parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="daee8-379">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="daee8-380">Są one wymagane projektu zadania WebJob ponieważ nie ma on pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="daee8-380">That is needed by the WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="daee8-381">Wcześniej przedstawiono lokalizację przechowywania tych parametrów połączenia. Dalej pokażemy, jak kod pobiera parametry połączenia podczas tworzenia wystąpień klasy DbContext.</span><span class="sxs-lookup"><span data-stu-id="daee8-381">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="daee8-382">ContosoAdsCommon — BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="daee8-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="daee8-383">`BlobInformation` Klasa jest używana do przechowywania informacji na temat obiekt blob obrazu w komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="daee8-383">The `BlobInformation` class is used to store information about an image blob in a queue message.</span></span>

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


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="daee8-384">ContosoAdsWeb — Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="daee8-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="daee8-385">Kod wywoływany z metody `Application_Start` umożliwia tworzenie kontenera obiektów blob *obrazów* i kolejki *obrazów*, jeśli jeszcze nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="daee8-385">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="daee8-386">Dzięki temu, że przy każdym uruchomieniu przy użyciu nowego konta magazynu, kolejka i kontener obiektów blob wymagane są tworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="daee8-386">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span></span>

<span data-ttu-id="daee8-387">Kod uzyskuje dostęp do konta magazynu przy użyciu parametrów połączenia magazynu z *Web.config* pliku lub środowisko uruchomieniowe platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-387">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="daee8-388">Następnie pobiera odwołanie do *obrazów* kontenera obiektów blob, tworzy kontener, jeśli jeszcze nie istnieje, i ustawia uprawnienia dostępu w obrębie nowego kontenera.</span><span class="sxs-lookup"><span data-stu-id="daee8-388">Then, it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="daee8-389">Domyślnie nowe kontenery Zezwalaj tylko klientom z poświadczeniami konta magazynu dostęp do obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="daee8-389">By default, new containers allow only clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="daee8-390">Aplikacja sieci web musi być publiczne, aby możliwe było wyświetlanie obrazów przy użyciu adresów URL wskazujących na obiekty BLOB obrazów obiekty BLOB.</span><span class="sxs-lookup"><span data-stu-id="daee8-390">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

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

<span data-ttu-id="daee8-391">Podobny kod pobiera odwołanie do *thumbnailrequest* kolejki i tworzy nową kolejkę.</span><span class="sxs-lookup"><span data-stu-id="daee8-391">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="daee8-392">W takim przypadku nie trzeba zmieniać uprawnień.</span><span class="sxs-lookup"><span data-stu-id="daee8-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="daee8-393">ContosoAdsWeb — _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="daee8-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="daee8-394">Plik *_Layout.cshtml* umożliwia ustawienie nazwy aplikacji w nagłówku i stopce oraz utworzenie wpisu menu „Ads”.</span><span class="sxs-lookup"><span data-stu-id="daee8-394">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="daee8-395">ContosoAdsWeb — Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="daee8-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="daee8-396">Plik *Views\Home\Index.cshtml* umożliwia wyświetlanie linków kategorii na stronie głównej.</span><span class="sxs-lookup"><span data-stu-id="daee8-396">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="daee8-397">Linki przekazują wartość całkowitą typu wyliczeniowego `Category` w zmiennej querystring na stronie indeksu reklam.</span><span class="sxs-lookup"><span data-stu-id="daee8-397">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="daee8-398">ContosoAdsWeb — AdController.cs</span><span class="sxs-lookup"><span data-stu-id="daee8-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="daee8-399">W pliku *AdController.cs* konstruktor wywołuje metodę `InitializeStorage` w celu utworzenia obiektów biblioteki klienta usługi Azure Storage, które będą dostarczać interfejs API do pracy z kolejkami i obiektami blob.</span><span class="sxs-lookup"><span data-stu-id="daee8-399">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="daee8-400">Następnie kod pobiera odwołanie do *obrazów* kontenera obiektów blob, jak przedstawiono wcześniej w *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="daee8-400">Then, the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="daee8-401">Podczas wykonywania, który, ustawia domyślną [zasady ponawiania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) odpowiednie dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="daee8-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="daee8-402">Domyślne zasady ponawiania wykładniczego wycofywania mogą powodować zawieszanie aplikacji sieci Web na czas dłuższy niż minuta w przypadku kolejnych prób i wystąpienia błędu przejściowego.</span><span class="sxs-lookup"><span data-stu-id="daee8-402">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="daee8-403">Zasady ponawiania określone w tym miejscu powodują oczekiwanie przez trzy sekundy po każdej próbie. Maksymalna liczba prób to trzy.</span><span class="sxs-lookup"><span data-stu-id="daee8-403">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="daee8-404">Podobny kod pobiera odwołanie do kolejki *obrazów*.</span><span class="sxs-lookup"><span data-stu-id="daee8-404">Similar code gets a reference to the *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="daee8-405">Większość kodu kontrolera jest typowa dla pracy z modelem danych platformy Entity Framework za pomocą klasy DbContext.</span><span class="sxs-lookup"><span data-stu-id="daee8-405">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="daee8-406">Wyjątkiem jest metoda HttpPost `Create`, która powoduje przekazanie pliku i zapisanie go w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="daee8-406">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="daee8-407">Integrator modelu udostępnia obiekt [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) w metodzie.</span><span class="sxs-lookup"><span data-stu-id="daee8-407">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="daee8-408">Jeśli użytkownik wybrał plik do przekazania, kod powoduje przekazanie pliku, zapisanie go w obiekcie blob i zaktualizowanie rekordu bazy danych Ad przy użyciu adresu URL, który wskazuje obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="daee8-408">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="daee8-409">Kod, który obsługuje przekazywanie, znajduje się w metodzie `UploadAndSaveBlobAsync`.</span><span class="sxs-lookup"><span data-stu-id="daee8-409">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="daee8-410">Powoduje on utworzenie nazwy identyfikatora GUID dla obiektu blob, przekazanie i zapisanie pliku oraz zwraca odwołanie do zapisanego obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="daee8-410">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

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

<span data-ttu-id="daee8-411">Po HttpPost `Create` metody obiektu blob i aktualizuje bazę danych, tworzy kolejki komunikatów w celu poinformowania procesu zaplecza, że obraz jest gotowy do konwersji na miniaturę.</span><span class="sxs-lookup"><span data-stu-id="daee8-411">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="daee8-412">Kod HttpPost `Edit` metoda jest podobny, z wyjątkiem tego, że jeśli użytkownik wybierze nowy plik obrazu, należy usunąć wszystkie obiekty BLOB, które już istnieją dla tej usługi ad.</span><span class="sxs-lookup"><span data-stu-id="daee8-412">The code for the HttpPost `Edit` method is similar, except that if the user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="daee8-413">Oto kod, który usuwania obiektów blob podczas usuwania reklamy:</span><span class="sxs-lookup"><span data-stu-id="daee8-413">Here is the code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="daee8-414">ContosoAdsWeb — Views\Ad\Index.cshtml i Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="daee8-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="daee8-415">*Index.cshtml* służy do wyświetlania miniatury z innymi danymi reklamy:</span><span class="sxs-lookup"><span data-stu-id="daee8-415">The *Index.cshtml* file displays thumbnails with the other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="daee8-416">*Details.cshtml* pliku wyświetla obrazu w pełnym rozmiarze:</span><span class="sxs-lookup"><span data-stu-id="daee8-416">The *Details.cshtml* file displays the full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="daee8-417">ContosoAdsWeb — Views\Ad\Create.cshtml i Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="daee8-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="daee8-418">Pliki *Create.cshtml* i *Edit.cshtml* określają kodowanie formularzy, które umożliwia kontrolerowi pobieranie obiektu `HttpPostedFileBase`.</span><span class="sxs-lookup"><span data-stu-id="daee8-418">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="daee8-419">Element `<input>` informuje przeglądarkę o konieczności udostępnienia okna dialogowego wyboru pliku.</span><span class="sxs-lookup"><span data-stu-id="daee8-419">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="daee8-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="daee8-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="daee8-421">Po uruchomieniu zadania WebJob, `Main` metoda wywołuje zestaw SDK zadań Webjob `JobHost.RunAndBlock` metody, aby rozpocząć wykonywanie wyzwalane funkcje w bieżącym wątku.</span><span class="sxs-lookup"><span data-stu-id="daee8-421">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="daee8-422"><a id="generatethumbnail"></a>Metoda GenerateThumbnail ContosoAdsWebJob - Functions.cs-</span><span class="sxs-lookup"><span data-stu-id="daee8-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="daee8-423">Zestaw SDK zadań Webjob wywołuje tę metodę w przypadku otrzymania komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="daee8-423">The WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="daee8-424">Metoda tworzy miniaturę i umieszcza miniatury adres URL w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="daee8-424">The method creates a thumbnail and puts the thumbnail URL in the database.</span></span>

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
            // be instantiated and disposed within the function.
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

* <span data-ttu-id="daee8-425">`QueueTrigger` Atrybut określa, że zestaw SDK zadań Webjob, aby wywołać tę metodę po odebraniu nowej wiadomości w kolejce thumbnailrequest.</span><span class="sxs-lookup"><span data-stu-id="daee8-425">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="daee8-426">`BlobInformation` Obiekt kolejki wiadomości jest automatycznie zdeserializowany do `blobInfo` parametru.</span><span class="sxs-lookup"><span data-stu-id="daee8-426">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span></span> <span data-ttu-id="daee8-427">Po zakończeniu działania metody komunikat z kolejki jest usuwana.</span><span class="sxs-lookup"><span data-stu-id="daee8-427">When the method completes, the queue message is deleted.</span></span> <span data-ttu-id="daee8-428">W przypadku niepowodzenia przed wykonaniem metody komunikatu w kolejce nie zostanie usunięta; Po wygaśnięciu dzierżawy 10-minutowych komunikat jest wydane do pobrania ponownie i przetworzyć.</span><span class="sxs-lookup"><span data-stu-id="daee8-428">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span></span> <span data-ttu-id="daee8-429">Ta sekwencja nie należy powtórzyć przez czas nieokreślony, jeśli komunikat zawsze powoduje zgłoszenie wyjątku.</span><span class="sxs-lookup"><span data-stu-id="daee8-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="daee8-430">Po 5 bez powodzenia próbuje przetworzyć komunikatu, wiadomość zostanie przeniesiona do kolejki o nazwie {queuename}-skażone.</span><span class="sxs-lookup"><span data-stu-id="daee8-430">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span></span> <span data-ttu-id="daee8-431">Maksymalna liczba prób jest konfigurowalne.</span><span class="sxs-lookup"><span data-stu-id="daee8-431">The maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="daee8-432">Dwa `Blob` atrybuty Podaj obiektów, które są powiązane z obiektów blob: jeden do istniejącego obiektu blob obrazu i jeden do nowego blob miniatury, w którym ta metoda tworzy.</span><span class="sxs-lookup"><span data-stu-id="daee8-432">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="daee8-433">Nazwy obiektów blob pochodzą z właściwości `BlobInformation` obiektu odebranego w wiadomości w kolejce (`BlobName` i `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="daee8-433">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="daee8-434">Aby uzyskać pełną funkcjonalność biblioteki klienta usługi Storage, można użyć `CloudBlockBlob` klasy do pracy z obiektami blob.</span><span class="sxs-lookup"><span data-stu-id="daee8-434">To get the full functionality of the Storage Client Library, you can use the `CloudBlockBlob` class to work with blobs.</span></span> <span data-ttu-id="daee8-435">Jeśli chcesz ponownie użyć kodu napisanego do pracy z `Stream` obiekty, można użyć `Stream` klasy.</span><span class="sxs-lookup"><span data-stu-id="daee8-435">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span></span>

<span data-ttu-id="daee8-436">Aby uzyskać więcej informacji na temat pisania funkcje programu wykorzystujące zestaw SDK zadań Webjob atrybutów zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="daee8-436">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span></span>

* [<span data-ttu-id="daee8-437">Jak używać usługi Azure Queue Storage z zestawem SDK usługi WebJobs</span><span class="sxs-lookup"><span data-stu-id="daee8-437">How to use Azure queue storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="daee8-438">Używanie usługi Azure Blob Storage z zestawem SDK zadań WebJob</span><span class="sxs-lookup"><span data-stu-id="daee8-438">How to use Azure blob storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="daee8-439">Jak używać usługi Azure Table Storage z zestawem SDK usługi WebJobs</span><span class="sxs-lookup"><span data-stu-id="daee8-439">How to use Azure table storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="daee8-440">Jak używać usługi Azure Service Bus z zestawem SDK usługi WebJobs</span><span class="sxs-lookup"><span data-stu-id="daee8-440">How to use Azure Service Bus with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="daee8-441">Jeśli aplikacja sieci web jest uruchomiony na wiele maszyn wirtualnych, wielu zadań Webjob będzie działać jednocześnie, a w niektórych przypadkach może to spowodować tych samych danych przetwarzana wiele razy.</span><span class="sxs-lookup"><span data-stu-id="daee8-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span></span> <span data-ttu-id="daee8-442">To nie jest problem, korzystając z wbudowanego kolejki, obiektów blob i wyzwalaczy usługi Service Bus.</span><span class="sxs-lookup"><span data-stu-id="daee8-442">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="daee8-443">Zestaw SDK gwarantuje, że funkcje będą przetwarzane tylko raz dla każdego komunikatu lub obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="daee8-443">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="daee8-444">Informacje o sposobie implementacji bezpiecznego zamknięcia, zobacz [łagodne zamykanie](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="daee8-444">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="daee8-445">Kod w `ConvertImageToThumbnailJPG` — metoda (tego nie pokazano) używa klas w `System.Drawing` przestrzeni nazw dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="daee8-445">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="daee8-446">Jednak klasy w tej przestrzeni nazw zostały zaprojektowane do użytku z aplikacją Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="daee8-446">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="daee8-447">Nie są one obsługiwane w usłudze systemu Windows lub programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="daee8-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="daee8-448">Aby uzyskać więcej informacji o opcjach przetwarzania obrazu, zobacz [Dynamiczne generowanie obrazu](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) i [Bezpośrednie zmienianie rozmiaru obrazu](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="daee8-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="daee8-449">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="daee8-449">Next steps</span></span>
<span data-ttu-id="daee8-450">W tym samouczku przedstawiono prostą aplikację wielowarstwową, która korzysta z zestawu SDK zadań Webjob dla przetwarzania wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="daee8-450">In this tutorial, you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span></span> <span data-ttu-id="daee8-451">Ta sekcja zawiera sugestie dotyczące dowiedzieć się więcej na temat aplikacje wielowarstwowe platformy ASP.NET i zadań Webjob.</span><span class="sxs-lookup"><span data-stu-id="daee8-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="daee8-452">Brak funkcji</span><span class="sxs-lookup"><span data-stu-id="daee8-452">Missing features</span></span>
<span data-ttu-id="daee8-453">Aplikacja została zachowana proste samouczek ułatwiający Rozpoczynanie pracy.</span><span class="sxs-lookup"><span data-stu-id="daee8-453">The application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="daee8-454">W aplikacji rzeczywistych można zaimplementować [iniekcji zależności](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) i [repozytorium i jednostki pracy wzorce](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), użyj [interfejs umożliwiający rejestrowanie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), użyj [migracje EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) do zarządzania zmianami modelu danych, a następnie użyj [elastyczności połączenia platformy EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) do zarządzania błędami sieci.</span><span class="sxs-lookup"><span data-stu-id="daee8-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="daee8-455">Skalowanie zadania Webjob</span><span class="sxs-lookup"><span data-stu-id="daee8-455">Scaling WebJobs</span></span>
<span data-ttu-id="daee8-456">Zadania Webjob uruchamiane w kontekście aplikacji sieci web i nie są skalowalne oddzielnie.</span><span class="sxs-lookup"><span data-stu-id="daee8-456">WebJobs run in the context of a web app and are not scalable separately.</span></span> <span data-ttu-id="daee8-457">Na przykład jeśli jedno wystąpienie aplikacji sieci web Standard, można mieć tylko jedno wystąpienie procesu tła uruchomiona, a niektóre zasoby serwera (procesora CPU, pamięć, itp.), które w przeciwnym razie będą dostępne do obsługi zawartości sieci web używa.</span><span class="sxs-lookup"><span data-stu-id="daee8-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span></span>

<span data-ttu-id="daee8-458">Jeśli ruch jest zależna od czasu dzień lub dzień tygodnia i przetwarzania wewnętrznej bazy danych należy poczekać, można zaplanować Twoje zadania Webjob do uruchomienia w czasie mniejszym natężeniu ruchu.</span><span class="sxs-lookup"><span data-stu-id="daee8-458">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span></span> <span data-ttu-id="daee8-459">Jeżeli obciążenie jest nadal za duża dla tego rozwiązania, w tym celu można uruchomić wewnętrznej bazy danych jako zadanie WebJob w aplikacji sieci web oddzielnych dedykowanych.</span><span class="sxs-lookup"><span data-stu-id="daee8-459">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="daee8-460">Aplikacja sieci web wewnętrznej bazy danych można następnie skalować niezależnie z aplikacji sieci web frontonu.</span><span class="sxs-lookup"><span data-stu-id="daee8-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="daee8-461">Aby uzyskać więcej informacji, zobacz [skalowanie zadania Webjob](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="daee8-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="daee8-462">Unikanie sieci web aplikacji limit czasu zamykania rozwijanych</span><span class="sxs-lookup"><span data-stu-id="daee8-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="daee8-463">Aby upewnić się, zawsze działają z zadań Webjob i uruchomione na wszystkich wystąpień aplikacji sieci web, należy włączyć [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) funkcji.</span><span class="sxs-lookup"><span data-stu-id="daee8-463">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="daee8-464">Przy użyciu zestawu SDK zadań Webjob poza zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="daee8-464">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="daee8-465">Program, który korzysta z zestawu SDK zadań Webjob nie ma do uruchamiania na platformie Azure w zadanie WebJob.</span><span class="sxs-lookup"><span data-stu-id="daee8-465">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span></span> <span data-ttu-id="daee8-466">Można uruchomić lokalnie i można również uruchomić w innych środowiskach, takich jak usługi w chmurze rola proces roboczy lub usługi systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="daee8-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="daee8-467">Jednak dostępne tylko zestaw SDK zadań Webjob pulpitu nawigacyjnego za pomocą aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="daee8-467">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="daee8-468">Do użycia pulpit nawigacyjny, należy połączyć aplikację sieci web do konta magazynu używane przez ustawienie parametrów połączenia AzureWebJobsDashboard **Konfiguruj** kartę klasycznego portalu.</span><span class="sxs-lookup"><span data-stu-id="daee8-468">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span></span> <span data-ttu-id="daee8-469">Można następnie uzyskać do pulpitu nawigacyjnego, korzystając z następującego adresu URL:</span><span class="sxs-lookup"><span data-stu-id="daee8-469">Then, you can get to the Dashboard by using the following URL:</span></span>

<span data-ttu-id="daee8-470">https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions</span><span class="sxs-lookup"><span data-stu-id="daee8-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="daee8-471">Aby uzyskać więcej informacji, zobacz [pobierania pulpitu nawigacyjnego dla wdrożenia lokalnego przy użyciu zestawu SDK zadań Webjob](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ale należy pamiętać, że widoczny jest stara nazwa ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="daee8-471">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="daee8-472">Więcej dokumentacji zadań Webjob</span><span class="sxs-lookup"><span data-stu-id="daee8-472">More WebJobs documentation</span></span>
<span data-ttu-id="daee8-473">Aby uzyskać więcej informacji, zobacz [zasoby dokumentacji zadań Webjob Azure](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="daee8-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
