---
title: "aaaGet do korzystania z usług Azure Cloud Services i programu ASP.NET | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate aplikację wielowarstwową przy użyciu platformy ASP.NET MVC i platformy Azure. Aplikacja Hello jest uruchamiana w usługi w chmurze z rolą sieci web i roli proces roboczy. Używa platformy Entity Framework, bazy danych SQL Database oraz obiektów blob i kolejek usługi Azure Storage."
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="f72fb-105">Wprowadzenie do usług Azure Cloud Services i programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f72fb-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="f72fb-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="f72fb-106">Overview</span></span>
<span data-ttu-id="f72fb-107">Ten samouczek pokazuje, jak toocreate wielowarstwową aplikację .NET z frontonem ASP.NET MVC frontonu, a następnie wdrożyć go tooan [usługi w chmurze Azure](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="f72fb-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="f72fb-108">Aplikacja używa Hello [bazy danych SQL Azure](http://msdn.microsoft.com/library/azure/ee336279), hello [usługi obiektów Blob platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage)i hello [usługi kolejek platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="f72fb-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="f72fb-109">Możesz [pobrać projekt programu Visual Studio hello](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) z hello galerii kodu MSDN.</span><span class="sxs-lookup"><span data-stu-id="f72fb-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="f72fb-110">Witaj samouczek pokazuje, jak toobuild i uruchom hello aplikację lokalnie, jak toodeploy go tooAzure i hello uruchamiania w chmurze i w jaki sposób toobuild ją od podstaw.</span><span class="sxs-lookup"><span data-stu-id="f72fb-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="f72fb-111">Można rozpocząć od kompilowania aplikacji od początku i hello testu i wdrożyć kroki później, jeśli wolisz.</span><span class="sxs-lookup"><span data-stu-id="f72fb-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="f72fb-112">Aplikacja Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="f72fb-112">Contoso Ads application</span></span>
<span data-ttu-id="f72fb-113">Aplikacja Hello jest reklamowa Tablica ogłoszeń.</span><span class="sxs-lookup"><span data-stu-id="f72fb-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="f72fb-114">Aby utworzyć reklamę, użytkownicy muszą wpisać tekst i przesłać obraz.</span><span class="sxs-lookup"><span data-stu-id="f72fb-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="f72fb-115">Widzą listę reklam z miniaturami obrazów i będą mogli wyświetlać obrazu w pełnym rozmiarze hello wybranie ad toosee hello szczegóły.</span><span class="sxs-lookup"><span data-stu-id="f72fb-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![Lista reklam](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="f72fb-117">Aplikacja Hello używa hello [wzorzec skoncentrowane kolejki pracy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff obciążenia roboczego hello użycie Procesora CPU tworzenia procesu zaplecza tooa miniatur.</span><span class="sxs-lookup"><span data-stu-id="f72fb-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="f72fb-118">Architektura alternatywna: witryny sieci Web i zadania WebJob</span><span class="sxs-lookup"><span data-stu-id="f72fb-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="f72fb-119">Ten samouczek pokazuje, jak toorun frontonu i zaplecza na platformie Azure w chmurze usługi.</span><span class="sxs-lookup"><span data-stu-id="f72fb-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="f72fb-120">Alternatywą jest hello toorun frontonu w [witryny sieci Web Azure](/services/web-sites/) i użyj hello [Webjob](http://go.microsoft.com/fwlink/?LinkId=390226) funkcji (obecnie w wersji zapoznawczej) dla zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="f72fb-121">Samouczek korzystającym z zadań Webjob, zobacz [wprowadzenie hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f72fb-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="f72fb-122">Aby uzyskać informacji na temat sposobu toochoose hello usług najlepiej dopasować danego scenariusza, zobacz [porównanie witryn sieci Web platformy Azure, usługi w chmurze i maszyn wirtualnych](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="f72fb-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="f72fb-123">Zawartość</span><span class="sxs-lookup"><span data-stu-id="f72fb-123">What you'll learn</span></span>
* <span data-ttu-id="f72fb-124">Jak tooenable komputer dla rozwoju platformy Azure, instalując hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="f72fb-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="f72fb-125">Jak toocreate Visual Studio cloud projektu usługi z rolą sieci web platformy ASP.NET MVC i roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="f72fb-126">Jak tootest hello projekt usługi w chmurze lokalnie, przy użyciu emulatora magazynu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="f72fb-127">Jak toopublish hello chmury projektu tooan Azure usługa w chmurze i przetestować go przy użyciu konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="f72fb-128">Jak tooupload pliki i przechowywać je w usłudze Azure Blob hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="f72fb-129">Jak toouse hello usługi kolejek platformy Azure do komunikacji między warstwami.</span><span class="sxs-lookup"><span data-stu-id="f72fb-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f72fb-130">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f72fb-130">Prerequisites</span></span>
<span data-ttu-id="f72fb-131">Witaj samouczka przyjęto założenie, że rozumiesz [podstawowe pojęcia dotyczące usługi Azure cloud services](cloud-services-choose-me.md) takich jak *roli sieci web* i *roli procesu roboczego* terminologii.</span><span class="sxs-lookup"><span data-stu-id="f72fb-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="f72fb-132">Założono również, że wiesz, jak toowork z [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) lub [formularzy sieci Web](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projekty w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f72fb-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="f72fb-133">Hello Przykładowa aplikacja korzysta MVC, ale większość hello samouczka odnosi się także tooWeb formularzy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="f72fb-134">Można uruchomić aplikacji hello lokalnie bez subskrypcji platformy Azure, ale należy jedna chmura toohello aplikacji hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="f72fb-135">Jeśli nie masz konta, możesz [aktywować korzyści dla subskrybentów MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) lub [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="f72fb-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="f72fb-136">Hello instrukcje w samouczku dotyczą pracy z jednym z hello następujące produkty:</span><span class="sxs-lookup"><span data-stu-id="f72fb-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="f72fb-137">Program Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f72fb-137">Visual Studio 2013</span></span>
* <span data-ttu-id="f72fb-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="f72fb-138">Visual Studio 2015</span></span>
* <span data-ttu-id="f72fb-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="f72fb-139">Visual Studio 2017</span></span>

<span data-ttu-id="f72fb-140">Jeśli nie masz jeden z nich, Visual Studio może być zainstalowana automatycznie po zainstalowaniu hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="f72fb-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="f72fb-141">Architektura aplikacji</span><span class="sxs-lookup"><span data-stu-id="f72fb-141">Application architecture</span></span>
<span data-ttu-id="f72fb-142">Aplikacja Hello przechowuje reklamy w bazie danych SQL przy użyciu programu Entity Framework Code First toocreate hello tabel i uzyskiwanie dostępu do danych hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="f72fb-143">W przypadku każdej reklamy hello bazy danych magazynów dwa adresy URL: jeden dla hello obrazu w pełnym rozmiarze i jeden do miniatury hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![Tabela reklam](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="f72fb-145">Gdy użytkownik przesyła obraz, hello fronton uruchomiony w roli sieć web zapisuje obraz powitania w [obiektów blob platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), zawierający informacje ad hello w bazie danych hello adres URL, który wskazuje toohello obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="f72fb-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="f72fb-146">At hello sama godzina, zapisuje komunikat tooan kolejki systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="f72fb-147">Proces zaplecza uruchomiony w roli proces roboczy okresowo sonduje kolejkę hello nowych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f72fb-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="f72fb-148">Gdy pojawi się nowy komunikat, hello roli proces roboczy tworzy miniaturę obrazu i aktualizacje hello miniatur pole bazy danych adresu URL dla danej reklamy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="f72fb-149">Witaj Poniższy diagram przedstawia interakcje hello części aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Architektura aplikacji Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="f72fb-151">Pobieranie i uruchamianie rozwiązania hello ukończone</span><span class="sxs-lookup"><span data-stu-id="f72fb-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="f72fb-152">Pobierz i Rozpakuj hello [ukończone rozwiązanie](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="f72fb-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="f72fb-153">Uruchom program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f72fb-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="f72fb-154">Z hello **pliku** menu wybierz **Otwórz projekt**, przejdź toowhere pobranego rozwiązania hello, a następnie otwórz plik rozwiązania hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="f72fb-155">Naciśnij klawisze CTRL + SHIFT + B toobuild hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f72fb-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="f72fb-156">Domyślnie program Visual Studio automatycznie przywraca zawartość pakietu NuGet hello, która nie została uwzględniona w hello *.zip* pliku.</span><span class="sxs-lookup"><span data-stu-id="f72fb-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="f72fb-157">Jeśli hello pakiety nie zostaną przywrócone, zainstaluj je ręcznie, przechodząc toohello **Zarządzaj pakietami NuGet dla rozwiązania** okno dialogowe i klikając hello **przywrócić** przycisk na powitania w prawym górnym narożniku.</span><span class="sxs-lookup"><span data-stu-id="f72fb-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="f72fb-158">W **Eksploratora rozwiązań**, upewnij się, że **ContosoAdsCloudService** został wybrany jako projekt startowy hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="f72fb-159">Jeśli używasz programu Visual Studio 2015 lub nowszego, Zmień parametry połączenia SQL Server hello w aplikacji hello *Web.config* pliku hello projektu ContosoAdsWeb i w hello *ServiceConfiguration.Local.cscfg* pliku projektu ContosoAdsCloudService hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="f72fb-160">W każdym przypadku Zmień "(localdb) \v11.0" za "(localdb) \MSSQLLocalDB".</span><span class="sxs-lookup"><span data-stu-id="f72fb-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="f72fb-161">Naciśnij klawisze CTRL + F5 toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f72fb-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="f72fb-162">Po uruchomieniu projektu usługi w chmurze lokalnie, Visual Studio automatycznie wywołuje hello Azure *emulator obliczeń* i Azure *emulatora magazynu*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="f72fb-163">Witaj obliczeniowe emulatora używa roli sieci web hello toosimulate zasoby komputera i środowisk roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="f72fb-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="f72fb-164">Witaj emulator magazynu używa [programu SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) bazy danych magazynu w chmurze Azure toosimulate.</span><span class="sxs-lookup"><span data-stu-id="f72fb-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="f72fb-165">Witaj pierwszego uruchomienia projektu usługi w chmurze, czas minuty toostart emulatory hello w górę.</span><span class="sxs-lookup"><span data-stu-id="f72fb-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="f72fb-166">Po zakończeniu uruchamiania emulatora hello domyślnej przeglądarki powoduje otwarcie strony głównej aplikacji toohello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Architektura aplikacji Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="f72fb-168">Kliknij przycisk **Create an Ad** (Utwórz reklamę).</span><span class="sxs-lookup"><span data-stu-id="f72fb-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="f72fb-169">Wprowadź dane testowe i wybierz *.jpg* tooupload obrazu, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![Tworzenie strony](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="f72fb-171">Aplikacja Hello przechodzi toohello strony indeksu, ale nie wyświetla miniatury nowej reklamy hello, ponieważ przetwarzanie nie zostało jeszcze przeprowadzone.</span><span class="sxs-lookup"><span data-stu-id="f72fb-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="f72fb-172">Poczekaj chwilę, a następnie Odśwież hello indeksu strony toosee hello miniatur.</span><span class="sxs-lookup"><span data-stu-id="f72fb-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![Strona indeksu](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="f72fb-174">Kliknij przycisk **szczegóły** dla użytkownika ad toosee hello obrazu w pełnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="f72fb-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![Strona szczegółów](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="f72fb-176">Działała aplikacja hello całkowicie na komputerze lokalnym, bez połączenia toohello chmury.</span><span class="sxs-lookup"><span data-stu-id="f72fb-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="f72fb-177">Witaj emulator magazynu przechowuje hello kolejki i danych obiektów blob w bazie danych programu SQL Server Express LocalDB, a aplikacja hello przechowuje dane ad hello w innej bazie danych LocalDB.</span><span class="sxs-lookup"><span data-stu-id="f72fb-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="f72fb-178">Bazy danych Entity Framework Code First automatycznie utworzone hello ad hello pierwszej aplikacji sieci web hello nastąpiła tooaccess go.</span><span class="sxs-lookup"><span data-stu-id="f72fb-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="f72fb-179">W powitania po sekcji skonfigurujesz hello rozwiązania toouse zasobów w chmurze Azure dla kolejek, obiektów blob i bazy danych aplikacji hello po uruchomieniu na powitania chmury.</span><span class="sxs-lookup"><span data-stu-id="f72fb-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="f72fb-180">Jeśli poszukiwany toorun toocontinue lokalnie, ale użycia zasobów magazynu i bazy danych w chmurze, możesz to zrobić.</span><span class="sxs-lookup"><span data-stu-id="f72fb-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="f72fb-181">Jest to jedynie ustawienia parametrów połączenia — pokażemy, jak toodo.</span><span class="sxs-lookup"><span data-stu-id="f72fb-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="f72fb-182">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="f72fb-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="f72fb-183">Należy to zrobić hello następujące kroki toorun hello aplikacji w chmurze hello:</span><span class="sxs-lookup"><span data-stu-id="f72fb-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="f72fb-184">Utworzenie usługi w chmurze platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="f72fb-185">Utworzenie bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="f72fb-186">Utworzenie konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="f72fb-187">Skonfiguruj toouse rozwiązania hello bazy danych Azure SQL po uruchomieniu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="f72fb-188">Skonfiguruj toouse rozwiązania hello konta magazynu Azure po uruchomieniu na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="f72fb-189">Wdróż hello projektu tooyour usługi w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="f72fb-190">Tworzenie usługi w chmurze platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f72fb-190">Create an Azure cloud service</span></span>
<span data-ttu-id="f72fb-191">Usługi w chmurze Azure to aplikacja hello środowiska hello jest uruchamiana w.</span><span class="sxs-lookup"><span data-stu-id="f72fb-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="f72fb-192">W przeglądarce otwórz hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f72fb-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f72fb-193">Kliknij kolejno pozycje **Nowe > Obliczenia > Usługa w chmurze**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="f72fb-194">W hello DNS nazwy wejściowe wpisz prefiks adresu URL dla usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="f72fb-195">Ten adres URL ma toobe unikatowy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-195">This URL has toobe unique.</span></span>  <span data-ttu-id="f72fb-196">Zostanie wyświetlony komunikat o błędzie, jeśli prefiksu hello jest już używana.</span><span class="sxs-lookup"><span data-stu-id="f72fb-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="f72fb-197">Określ nową grupę zasobów dla usługi hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="f72fb-198">Kliknij przycisk **Utwórz nowy** , a następnie wpisz nazwę w hello zasobów wejściowych pole grupy, takie jak CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="f72fb-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="f72fb-199">Wybierz region hello miejscu aplikacji hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="f72fb-200">To pole określa centrum danych, w którym będzie hostowana usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f72fb-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="f72fb-201">W przypadku aplikacji produkcyjnej warto wybrać hello region najbliższy tooyour klientów.</span><span class="sxs-lookup"><span data-stu-id="f72fb-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="f72fb-202">W tym samouczku wybierz hello region najbliższy tooyou.</span><span class="sxs-lookup"><span data-stu-id="f72fb-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="f72fb-203">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-203">Click **Create**.</span></span>

    <span data-ttu-id="f72fb-204">W hello po obrazu tworzona jest hello CSvccontosoads.cloudapp.net adres URL usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f72fb-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![Nowa usługa w chmurze](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="f72fb-206">Tworzenie bazy danych SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f72fb-206">Create an Azure SQL database</span></span>
<span data-ttu-id="f72fb-207">Po uruchomieniu aplikacji hello w chmurze hello, będzie on używać bazy danych opartej na chmurze.</span><span class="sxs-lookup"><span data-stu-id="f72fb-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="f72fb-208">W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **nowy > baz danych > SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="f72fb-209">W hello **Nazwa bazy danych** wprowadź *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="f72fb-210">W hello **grupy zasobów**, kliknij przycisk **Użyj istniejącego** i grupy zasobów wybierz hello używane dla usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="f72fb-211">Na powitania po obrazu, kliknij **serwera — Skonfiguruj wymagane ustawienia** i **Utwórz nowy serwer**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Serwer toodatabase tunelu](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="f72fb-213">Alternatywnie Jeśli subskrypcja obejmuje już serwer, z listy rozwijanej hello można wybrać tego serwera.</span><span class="sxs-lookup"><span data-stu-id="f72fb-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="f72fb-214">W hello **nazwy serwera** wprowadź *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="f72fb-215">Wprowadź wartość **Nazwa logowania** i **Hasło** dla administratora.</span><span class="sxs-lookup"><span data-stu-id="f72fb-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="f72fb-216">W przypadku wybrania opcji **Utwórz nowy serwer** nie wprowadzasz w tym miejscu istniejącej nazwy i hasła.</span><span class="sxs-lookup"><span data-stu-id="f72fb-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="f72fb-217">Podajesz nową nazwę i hasło, że definiujesz teraz toouse później podczas uzyskiwania dostępu hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="f72fb-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="f72fb-218">W przypadku wybrania wcześniej utworzonego serwera zostanie wyświetlony monit dla hello hasła toohello konta użytkownika administracyjnego już utworzone.</span><span class="sxs-lookup"><span data-stu-id="f72fb-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="f72fb-219">Wybierz hello sam **lokalizacji** wybraną hello usłudze w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f72fb-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="f72fb-220">Jeśli usługa w chmurze hello i bazy danych są w różnych centrach danych (różnych regionach), zwiększy się opóźnienie i możesz będą naliczane opłaty dotyczące przepustowości poza centrum danych hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="f72fb-221">Przepustowość w centrum danych jest bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="f72fb-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="f72fb-222">Sprawdź **Zezwalaj usługom platformy azure tooaccess serwera**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="f72fb-223">Kliknij przycisk **wybierz** hello nowego serwera.</span><span class="sxs-lookup"><span data-stu-id="f72fb-223">Click **Select** for hello new server.</span></span>

    ![Nowy serwer usługi SQL Database](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="f72fb-225">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="f72fb-226">Tworzenie konta usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f72fb-226">Create an Azure storage account</span></span>
<span data-ttu-id="f72fb-227">Konto magazynu platformy Azure udostępnia zasoby do przechowywania danych kolejek i obiektów blob w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="f72fb-228">W rzeczywistych aplikacjach przeważnie tworzy się oddzielne konta dla danych aplikacji porównywanych z danymi rejestrowania oraz oddzielne konta dla danych testowych porównywanych z danymi produkcyjnymi.</span><span class="sxs-lookup"><span data-stu-id="f72fb-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="f72fb-229">W tym samouczku będzie używane tylko jedno konto.</span><span class="sxs-lookup"><span data-stu-id="f72fb-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="f72fb-230">W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **nowy > magazynu > Konto magazynu — obiekt blob, plików, tabeli, kolejki**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="f72fb-231">W hello **nazwa** wpisz prefiks adresu URL.</span><span class="sxs-lookup"><span data-stu-id="f72fb-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="f72fb-232">Ten prefiks i hello tekst wyświetlony w polu hello będzie konto magazynu tooyour unikatowy adres URL hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="f72fb-233">Jeśli hello prefiks został już użyty przez innego użytkownika, będziesz mieć toochoose inny prefiks.</span><span class="sxs-lookup"><span data-stu-id="f72fb-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="f72fb-234">Zestaw hello **modelu wdrażania** za*klasycznego*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="f72fb-235">Zestaw hello **replikacji** listy rozwijanej liście zbyt**magazyn lokalnie nadmiarowy**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="f72fb-236">Jeśli replikacja geograficzna jest włączona dla konta magazynu, hello przechowywana zawartość jest trybu failover tooenable dodatkowego centrum danych replikowanych tooa w przypadku poważnej awarii w lokalizacji głównej hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="f72fb-237">Replikacja geograficzna może pociągnąć za sobą dodatkowe koszty.</span><span class="sxs-lookup"><span data-stu-id="f72fb-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="f72fb-238">W przypadku kont testowych i programistycznych zwykle nie chcesz toopay za replikację geograficzną.</span><span class="sxs-lookup"><span data-stu-id="f72fb-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="f72fb-239">Aby uzyskać więcej informacji, zobacz temat dotyczący [tworzenia i usuwania konta magazynu oraz zarządzania nim](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="f72fb-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="f72fb-240">W hello **grupy zasobów**, kliknij przycisk **Użyj istniejącego** i grupy zasobów wybierz hello używane dla usługi w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="f72fb-241">Zestaw hello **lokalizacji** toohello listy rozwijanej region wybrany dla usługi w chmurze hello wcześniej.</span><span class="sxs-lookup"><span data-stu-id="f72fb-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="f72fb-242">Jeśli hello chmury usługi i konto magazynu są obsługiwane w różnych centrach danych (różnych regionach), zwiększy się opóźnienie i możesz będą naliczane opłaty dotyczące przepustowości poza centrum danych hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="f72fb-243">Przepustowość w centrum danych jest bezpłatna.</span><span class="sxs-lookup"><span data-stu-id="f72fb-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="f72fb-244">Grupy koligacji Azure udostępniają mechanizm toominimize hello odległości między zasobami w centrum danych, co może zmniejszyć opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="f72fb-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="f72fb-245">Ten samouczek nie korzysta z grup koligacji.</span><span class="sxs-lookup"><span data-stu-id="f72fb-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="f72fb-246">Aby uzyskać więcej informacji, zobacz [jak tooCreate koligacji grupy w usłudze Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="f72fb-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="f72fb-247">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-247">Click **Create**.</span></span>

    ![Nowe konto usługi Storage](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="f72fb-249">W obrazie hello utworzeniu konta magazynu z adresem URL hello `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="f72fb-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="f72fb-250">Skonfiguruj toouse rozwiązania hello bazy danych Azure SQL po uruchomieniu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f72fb-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="f72fb-251">Witaj projektu sieci web i hello projektu roli proces roboczy każdy ma własne parametry połączenia bazy danych, a każdy z nich musi bazy danych Azure SQL toohello toopoint po uruchomieniu aplikacji hello na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="f72fb-252">Użyjesz [przekształcenie pliku Web.config](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) dla roli sieci web hello i ustawienia środowiska usługi chmury hello roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="f72fb-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="f72fb-253">W tej sekcji i hello kolejnej sekcji poświadczenia są przechowywane w plikach projektu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="f72fb-254">[Nie należy przechowywać poufnych danych w publicznych repozytoriach kodów źródłowych](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="f72fb-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="f72fb-255">W projekcie ContosoAdsWeb hello Otwórz hello *Web.Release.config* pliku transformacji dla aplikacji hello *Web.config* pliku, Usuń blok komentarza hello, który zawiera `<connectionStrings>` i Wklej Witaj następującego kodu w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="f72fb-256">Pozostaw hello plik jest otwarty do edycji.</span><span class="sxs-lookup"><span data-stu-id="f72fb-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="f72fb-257">W hello [portalu Azure](https://portal.azure.com), kliknij przycisk **baz danych SQL** w okienku po lewej stronie powitania kliknij hello bazy danych utworzonej w ramach tego samouczka, a następnie kliknij **Pokaż parametry połączenia**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Pokazywanie parametrów połączeń](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="f72fb-259">Hello portal zawiera parametry połączeń oraz symbol zastępczy hello hasła.</span><span class="sxs-lookup"><span data-stu-id="f72fb-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![Parametry połączeń](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="f72fb-261">W hello *Web.Release.config* pliku przekształcenia, Usuń `{connectionstring}` i Wklej w jego miejscu hello parametrów połączenia ADO.NET z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="f72fb-262">W parametrach połączenia hello wklejonych w hello *Web.Release.config* pliku przekształcenia, Zastąp `{your_password_here}` z hello hasło utworzone dla hello nowej bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="f72fb-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="f72fb-263">Zapisz plik hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-263">Save hello file.</span></span>  
6. <span data-ttu-id="f72fb-264">Zaznacz i skopiuj parametry połączenia hello (bez hello znaki cudzysłowu otaczające) do użycia w hello następujące kroki dotyczące konfigurowania projektu roli proces roboczy hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="f72fb-265">W **Eksploratora rozwiązań**w obszarze **ról** w hello projekt usługi w chmurze, kliknij prawym przyciskiem myszy **ContosoAdsWorker** , a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Właściwości roli](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="f72fb-267">Kliknij przycisk hello **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="f72fb-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="f72fb-268">Zmień **konfiguracji usługi** za**chmury**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="f72fb-269">Wybierz hello **wartość** dla hello pole `ContosoAdsDbConnectionString` ustawienia, a następnie wklej parametry połączenia hello, które zostały skopiowane z poprzedniej sekcji samouczka hello hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![Parametry połączenia bazy danych dla roli Proces roboczy](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="f72fb-271">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="f72fb-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="f72fb-272">Skonfiguruj toouse rozwiązania hello konta magazynu Azure po uruchomieniu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f72fb-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="f72fb-273">Parametry połączenia konta magazynu platformy Azure dla projektu roli sieć web hello i projektu roli proces roboczy hello są przechowywane w ustawieniach środowiska w hello projekt usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f72fb-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="f72fb-274">Dla każdego projektu istnieje osobny zestaw ustawień toobe używane po uruchomieniu aplikacji hello lokalnie, a po uruchomieniu na platformie hello chmury.</span><span class="sxs-lookup"><span data-stu-id="f72fb-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="f72fb-275">Ustawienia środowiska chmury hello projektów ról sieć web i proces roboczy będzie aktualizowana.</span><span class="sxs-lookup"><span data-stu-id="f72fb-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="f72fb-276">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy **ContosoAdsWeb** w obszarze **ról** w hello **ContosoAdsCloudService** projektu, a następnie kliknij przycisk **Właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Właściwości roli](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="f72fb-278">Kliknij przycisk hello **ustawienia** kartę. W hello **konfiguracji usługi** listy rozwijanej wybierz pozycję **chmury**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Konfiguracja chmury](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="f72fb-280">Wybierz hello **StorageConnectionString** wpis, aby zobaczyć wielokropek (**... **) przycisk na prawym końcu wiersza hello hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="f72fb-281">Kliknij przycisk hello tooopen przycisk wielokropka hello **Tworzenie parametrów połączenia konta magazynu** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f72fb-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![Otwieranie okna Tworzenie parametrów połączenia](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="f72fb-283">W hello **utworzyć parametry połączenia magazynu** okno dialogowe, kliknij przycisk **subskrypcji**, wybierz konto magazynu hello, który został utworzony wcześniej, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="f72fb-284">Jeśli nie zalogowano się, zostanie wyświetlony monit o podanie poświadczeń konta systemu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Tworzenie parametrów połączenia usługi Storage](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="f72fb-286">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="f72fb-286">Save your changes.</span></span>
6. <span data-ttu-id="f72fb-287">Wykonaj hello same procedury, która została użyta w przypadku hello `StorageConnectionString` hello tooset ciąg połączenia `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` parametry połączenia.</span><span class="sxs-lookup"><span data-stu-id="f72fb-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="f72fb-288">Te parametry są używane do rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="f72fb-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="f72fb-289">Wykonaj hello same procedury, która została użyta w przypadku hello **ContosoAdsWeb** tooset roli parametry połączeń dla hello **ContosoAdsWorker** roli.</span><span class="sxs-lookup"><span data-stu-id="f72fb-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="f72fb-290">Nie zapomnij tooset **konfiguracji usługi** za**chmury**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="f72fb-291">ustawienia środowiska roli Hello skonfigurowane przy użyciu interfejsu użytkownika programu Visual Studio hello są przechowywane w hello następujące pliki w projekcie ContosoAdsCloudService hello:</span><span class="sxs-lookup"><span data-stu-id="f72fb-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="f72fb-292">*ServiceDefinition.csdef* — definiuje nazwy ustawień hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="f72fb-293">*ServiceConfiguration.Cloud.cscfg* — udostępnia wartości w przypadku uruchamiania aplikacji hello w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="f72fb-294">*ServiceConfiguration.Local.cscfg* — udostępnia wartości podczas uruchamiania aplikacji hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f72fb-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="f72fb-295">Na przykład hello ServiceDefinition.csdef zawiera następujące definicje hello:</span><span class="sxs-lookup"><span data-stu-id="f72fb-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="f72fb-296">I hello *ServiceConfiguration.Cloud.cscfg* plik zawiera wartości hello wprowadzone dla tych ustawień w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f72fb-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="f72fb-297">Witaj `<Instances>` ustawienie określa liczbę hello maszyn wirtualnych, które platforma Azure uruchomi proces roboczy hello kod roli na.</span><span class="sxs-lookup"><span data-stu-id="f72fb-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="f72fb-298">Witaj [następne kroki](#next-steps) sekcja zawiera linki toomore informacji na temat skalowania usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="f72fb-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="f72fb-299">Wdrażanie hello tooAzure projektu</span><span class="sxs-lookup"><span data-stu-id="f72fb-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="f72fb-300">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello **ContosoAdsCloudService** projekt w chmurze, a następnie wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Menu Publikowanie](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="f72fb-302">W hello **Zaloguj** krok hello **publikowanie aplikacji platformy Azure** kreatora, kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Krok Logowanie](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="f72fb-304">W hello **ustawienia** kroku kreatora powitania kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![Krok Ustawienia](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="f72fb-306">Witaj ustawienia domyślne w hello **zaawansowane** kartę są wystarczające w przypadku tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="f72fb-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="f72fb-307">Aby uzyskać informacje o karcie Zaawansowane hello, zobacz [Kreator publikowania aplikacji Azure](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="f72fb-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="f72fb-308">W hello **Podsumowanie** kroku, kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-308">In hello **Summary** step, click **Publish**.</span></span>

    ![Krok Podsumowanie](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="f72fb-310">Witaj **dziennika aktywności platformy Azure** w programie Visual Studio zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="f72fb-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="f72fb-311">Kliknij przycisk Szczegóły wdrożenia hello tooexpand ikona hello strzałki w prawo.</span><span class="sxs-lookup"><span data-stu-id="f72fb-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="f72fb-312">Witaj wdrażania może potrwać too5 minut lub więcej toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f72fb-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Okno Dziennik aktywności platformy Azure](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="f72fb-314">Po zakończeniu stan wdrożenia powitania kliknij hello **adres URL aplikacji sieci Web** toostart hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f72fb-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="f72fb-315">Teraz możesz przetestować aplikacji hello tworzenia, wyświetlając i edytując niektóre reklamy, tak jak po uruchomieniu aplikacji hello lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f72fb-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="f72fb-316">Po zakończeniu testowania Usuń lub Zatrzymaj hello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f72fb-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="f72fb-317">Nawet jeśli nie używasz usługi w chmurze hello, jest Naliczanie opłat, ponieważ zasoby maszyny wirtualnej są zastrzeżone dla niego.</span><span class="sxs-lookup"><span data-stu-id="f72fb-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="f72fb-318">Jeśli usługa będzie działać, każda osoba, która znajdzie adres URL, będzie mogła tworzyć i wyświetlać reklamy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="f72fb-319">W hello [portalu Azure](https://portal.azure.com), przejdź toohello **omówienie** dla usługi w chmurze, a następnie kliknij pozycję hello **usunąć** przycisk u góry hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="f72fb-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="f72fb-320">Wystarczy tootemporarily uniemożliwić innym użytkownikom dostęp do witryny hello, kliknij przycisk **zatrzymać** zamiast tego.</span><span class="sxs-lookup"><span data-stu-id="f72fb-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="f72fb-321">W takim przypadku opłaty będą nadal tooaccrue.</span><span class="sxs-lookup"><span data-stu-id="f72fb-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="f72fb-322">Po ich nie są już potrzebne, można wykonać podobne hello toodelete procedury konto magazynu i bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="f72fb-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="f72fb-323">Tworzenie aplikacji hello od początku</span><span class="sxs-lookup"><span data-stu-id="f72fb-323">Create hello application from scratch</span></span>
<span data-ttu-id="f72fb-324">Jeśli nie pobrano jeszcze [aplikacji hello ukończone](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), zrób to teraz.</span><span class="sxs-lookup"><span data-stu-id="f72fb-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="f72fb-325">Do nowego projektu hello będzie skopiuj pliki z projektu hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="f72fb-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="f72fb-326">Tworzenie aplikacji Contoso Ads hello obejmuje hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="f72fb-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="f72fb-327">Tworzenie rozwiązania usługi w chmurze w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f72fb-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="f72fb-328">Aktualizowanie i dodawanie pakietów NuGet.</span><span class="sxs-lookup"><span data-stu-id="f72fb-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="f72fb-329">Ustawianie odwołań do projektu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-329">Set project references.</span></span>
* <span data-ttu-id="f72fb-330">Konfigurowanie parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="f72fb-330">Configure connection strings.</span></span>
* <span data-ttu-id="f72fb-331">Dodawanie plików kodu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-331">Add code files.</span></span>

<span data-ttu-id="f72fb-332">Po utworzeniu hello rozwiązania można przejrzeć kod hello projektów usług toocloud unikatowy i obiekty BLOB platformy Azure i kolejki.</span><span class="sxs-lookup"><span data-stu-id="f72fb-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="f72fb-333">Tworzenie rozwiązania usługi w chmurze w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f72fb-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="f72fb-334">W programie Visual Studio, wybierz **nowy projekt** z hello **pliku** menu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="f72fb-335">W okienku po lewej stronie powitania hello **nowy projekt** okna dialogowego rozwiń **Visual C#** i wybierz polecenie **chmury** szablony, a następnie wybierz pozycję hello **usługi w chmurze Azure** szablonu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="f72fb-336">Nazwa projektu hello i rozwiązanie ContosoAdsCloudService, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Nowy projekt](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="f72fb-338">W hello **nową usługę w chmurze Azure** okno dialogowe Dodaj rolę sieci web i roli proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="f72fb-339">Nazwa hello rolę sieć web ContosoAdsWeb i nazwę hello roli proces roboczy ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="f72fb-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="f72fb-340">(Użyj ikony ołówka hello w hello w okienku po prawej stronie toochange hello domyślne nazwy ról hello.)</span><span class="sxs-lookup"><span data-stu-id="f72fb-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![Projekt nowej usługi w chmurze](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="f72fb-342">Po wyświetleniu hello **nowy projekt ASP.NET** okno dialogowe dla roli sieci web hello, wybierz szablon MVC hello, a następnie kliknij przycisk **Zmień uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![Zmienianie uwierzytelniania](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="f72fb-344">W hello **Zmień uwierzytelnianie** oknie dialogowym wybierz **bez uwierzytelniania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Bez uwierzytelniania](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="f72fb-346">W hello **nowy projekt ASP.NET** okna dialogowego, kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="f72fb-347">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy hello rozwiązanie (nie jeden z projektów hello) i wybierz **Dodaj — nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="f72fb-348">W hello **Dodawanie nowego projektu** okno dialogowe Wybierz **Windows** w obszarze **Visual C#** w lewym okienku hello, a następnie kliknij hello **biblioteki klas** szablon.</span><span class="sxs-lookup"><span data-stu-id="f72fb-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="f72fb-349">Nazwa projektu hello *ContosoAdsCommon*, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="f72fb-350">Należy tooreference hello Entity Framework kontekstu i hello modelu danych z projektów ról sieć web i proces roboczy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="f72fb-351">Alternatywnie można zdefiniować klasy związane z platformą EF hello w projekcie roli sieci web hello i odwoływać się do tego projektu z projektu roli proces roboczy hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="f72fb-352">Ale hello o innym podejściu, projektu roli proces roboczy musi zestawów tooweb odwołań, które nie należy go.</span><span class="sxs-lookup"><span data-stu-id="f72fb-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="f72fb-353">Aktualizowanie i dodawanie pakietów NuGet</span><span class="sxs-lookup"><span data-stu-id="f72fb-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="f72fb-354">Otwórz hello **Zarządzaj pakietami NuGet** okno dialogowe hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f72fb-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="f72fb-355">U góry hello okna hello, zaznacz pole wyboru **aktualizacje**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="f72fb-356">Wyszukaj hello *WindowsAzure.Storage* pakietu, a jeśli znajduje się liście hello, zaznacz go i wybierz tooupdate projektów sieci web i proces roboczy hello go, a następnie kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="f72fb-357">Biblioteka klienta usługi storage Hello jest aktualizowana częściej niż szablony projektów Visual Studio, dlatego często okazuje tej wersji hello w nowo utworzonego projektu toobe potrzeb, zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="f72fb-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="f72fb-358">U góry hello okna hello, zaznacz pole wyboru **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="f72fb-359">Znajdź hello *EntityFramework* NuGet pakietu, a następnie zainstaluj go we wszystkich trzech projektach.</span><span class="sxs-lookup"><span data-stu-id="f72fb-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="f72fb-360">Znajdź hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet pakietu, a następnie zainstaluj go w projekcie roli proces roboczy hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="f72fb-361">Ustawianie odwołań do projektu</span><span class="sxs-lookup"><span data-stu-id="f72fb-361">Set project references</span></span>
1. <span data-ttu-id="f72fb-362">W projekcie ContosoAdsWeb hello Ustaw odwołanie do projektu ContosoAdsCommon toohello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="f72fb-363">Kliknij prawym przyciskiem myszy projekt ContosoAdsWeb hello, a następnie kliknij przycisk **odwołania** - **Dodaj odwołania**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="f72fb-364">W hello **Menedżera odwołań** okno dialogowe, wybierz opcję **rozwiązanie — projekty** wybierz w okienku po lewej stronie powitania **ContosoAdsCommon**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="f72fb-365">W hello w projekcie ContosoAdsWorker Ustaw odwołanie do projektu Contosoadscommon toohello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="f72fb-366">Projekt ContosoAdsCommon będzie zawierać hello Entity Framework danych klasę kontekstu i model, które będą używane przez oba hello frontonu i zaplecza.</span><span class="sxs-lookup"><span data-stu-id="f72fb-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="f72fb-367">W projekcie ContosoAdsWorker hello Ustaw odwołanie za`System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="f72fb-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="f72fb-368">Ten zestaw jest używany przez toothumbnails obrazów tooconvert zaplecza hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="f72fb-369">Konfigurowanie parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="f72fb-369">Configure connection strings</span></span>
<span data-ttu-id="f72fb-370">W tej sekcji będziesz konfigurować parametry połączenia usługi Azure Storage i danych SQL na potrzeby testowania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="f72fb-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="f72fb-371">instrukcje dotyczące wdrażania Hello wcześniej w samouczku hello wyjaśniają, jak tooset hello połączenie ciągów dla uruchomienie hello aplikacji w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="f72fb-372">W projekcie ContosoAdsWeb hello, hello Otwórz plik Web.config i Wstaw następujący hello `connectionStrings` elementu po hello `configSections` elementu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="f72fb-373">Jeśli korzystasz z programu Visual Studio 2015 lub nowszego, zastąp element „v11.0” elementem „MSSQLLocalDB”.</span><span class="sxs-lookup"><span data-stu-id="f72fb-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="f72fb-374">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="f72fb-374">Save your changes.</span></span>
3. <span data-ttu-id="f72fb-375">W projekcie ContosoAdsCloudService hello, kliknij prawym przyciskiem myszy ContosoAdsWeb w obszarze **ról**, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Właściwości roli](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="f72fb-377">W hello **contosadsweb — [rola]** okna właściwości, kliknij przycisk hello **ustawienia** , a następnie kliknij pozycję **Dodaj ustawienie**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="f72fb-378">Pozostaw **konfiguracji usługi** ustawić także**wszystkie konfiguracje**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="f72fb-379">Dodaj ustawienie o nazwie *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="f72fb-380">Ustaw **typu** za*ConnectionString*i ustaw **wartość** za*UseDevelopmentStorage = true*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![Nowe parametry połączenia](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="f72fb-382">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="f72fb-382">Save your changes.</span></span>
7. <span data-ttu-id="f72fb-383">Wykonaj hello tej samej procedury tooadd parametry połączenia magazynu w właściwości roli ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="f72fb-384">Nadal w hello **ContosoAdsWorker — [rola]** okna właściwości, Dodaj inny ciąg połączenia:</span><span class="sxs-lookup"><span data-stu-id="f72fb-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="f72fb-385">Nazwa: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="f72fb-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="f72fb-386">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="f72fb-386">Type: String</span></span>
   * <span data-ttu-id="f72fb-387">Wartość: Wklej hello takie same parametry połączenia używane dla projektu roli sieć web hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="f72fb-388">(hello poniższy przykład dotyczy programu Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="f72fb-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="f72fb-389">Nie zapomnij hello toochange źródła danych, jeśli kopiujesz ten przykład i korzystasz z programu Visual Studio 2015 lub nowszego.)</span><span class="sxs-lookup"><span data-stu-id="f72fb-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="f72fb-390">Dodawanie plików kodu</span><span class="sxs-lookup"><span data-stu-id="f72fb-390">Add code files</span></span>
<span data-ttu-id="f72fb-391">W tej sekcji skopiujesz pliki kodu z rozwiązania hello pobrane do hello nowego rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="f72fb-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="f72fb-392">Witaj sekcje będzie Pokaż i objaśnione części tego kodu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="f72fb-393">pliki tooadd tooa projektu lub folderu, kliknij prawym przyciskiem myszy projekt hello lub folderu i kliknij przycisk **Dodaj** - **istniejący element**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="f72fb-394">Wybierz pliki hello, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="f72fb-395">Jeśli zostanie wyświetlone pytanie, czy tooreplace istniejące pliki, kliknij przycisk **tak**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="f72fb-396">W projekcie ContosoAdsCommon hello Usuń hello *Class1.cs* i Dodaj w jego miejscu hello *Ad.cs* i *ContosoAdscontext.cs* pobrane pliki z hello projektu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="f72fb-397">W projekcie ContosoAdsWeb hello Dodaj hello następujące pliki z projektu hello pobrane.</span><span class="sxs-lookup"><span data-stu-id="f72fb-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="f72fb-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="f72fb-399">W hello *Views\Shared* folder: * \_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="f72fb-400">W hello *Views\Home* folder: *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="f72fb-401">W hello *kontrolerów* folder: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="f72fb-402">W hello *Views\Ad* folder (najpierw utwórz hello folder): pięć *.cshtml* plików.</span><span class="sxs-lookup"><span data-stu-id="f72fb-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="f72fb-403">W projekcie ContosoAdsWorker hello Dodaj *WorkerRole.cs* z hello pobrany projekt.</span><span class="sxs-lookup"><span data-stu-id="f72fb-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="f72fb-404">Teraz możesz skompilować i uruchomić aplikację hello, zgodnie z instrukcjami podanymi wcześniej w samouczku hello, a aplikacja hello będzie używać lokalnej bazy danych i zasobów emulatora magazynu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="f72fb-405">Witaj poniższe sekcje zawierają opis kodu hello tooworking powiązane z hello środowiska platformy Azure, obiekty BLOB i kolejek.</span><span class="sxs-lookup"><span data-stu-id="f72fb-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="f72fb-406">W tym samouczku opisano, jak kontrolerów MVC toocreate i widoków przy użyciu funkcji szkieletów, jak toowrite kodu programu Entity Framework działające z baz danych programu SQL Server lub hello podstaw programowania asynchronicznego w programie ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="f72fb-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="f72fb-407">Aby uzyskać informacje dotyczące tych tematów zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="f72fb-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="f72fb-408">Wprowadzenie do programu MVC 5</span><span class="sxs-lookup"><span data-stu-id="f72fb-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="f72fb-409">Wprowadzenie do programów EF 6 i MVC 5</span><span class="sxs-lookup"><span data-stu-id="f72fb-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="f72fb-410">[Wprowadzenie tooasynchronous programowania w programie .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="f72fb-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="f72fb-411">ContosoAdsCommon — Ad.cs</span><span class="sxs-lookup"><span data-stu-id="f72fb-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="f72fb-412">Witaj plik Ad.cs definiuje wyliczenia związane z kategoriami reklam i klasą jednostki POCO dla informacji o reklamach.</span><span class="sxs-lookup"><span data-stu-id="f72fb-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="f72fb-413">ContosoAdsCommon — ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="f72fb-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="f72fb-414">Witaj klasa ContosoAdsContext Określa, czy klasa Ad hello jest używany w kolekcji DbSet Entity Framework będą przechowywane w bazie danych SQL.</span><span class="sxs-lookup"><span data-stu-id="f72fb-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
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
```

<span data-ttu-id="f72fb-415">Klasa Hello ma dwa konstruktory.</span><span class="sxs-lookup"><span data-stu-id="f72fb-415">hello class has two constructors.</span></span> <span data-ttu-id="f72fb-416">Witaj pierwszy z nich jest używany przez hello projektu sieci web i określa nazwę parametrów połączenia, które są przechowywane w pliku Web.config hello hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="f72fb-417">Witaj drugi Konstruktor umożliwia toopass w hello rzeczywistych parametrów połączenia używane przez projekt roli proces roboczy hello, ponieważ nie ma on pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="f72fb-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="f72fb-418">Wcześniej przedstawiono gdzie te parametry połączenia są przechowywane i pojawi się później, jak hello kod pobiera parametry połączenia hello podczas tworzenia wystąpień klasy DbContext hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="f72fb-419">ContosoAdsWeb — Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="f72fb-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="f72fb-420">Kod, który jest wywoływany z hello `Application_Start` metoda tworzy *obrazów* kontenera obiektów blob i *obrazów* kolejki, jeśli jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="f72fb-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="f72fb-421">Daje to pewność, że zawsze, gdy rozpoczynasz pracę przy użyciu nowego konta magazynu, czy przy użyciu emulatora magazynu hello na nowym komputerze, kolejka i kontener wymaganego obiektu blob hello zostaną utworzone automatycznie.</span><span class="sxs-lookup"><span data-stu-id="f72fb-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="f72fb-422">Witaj konta magazynu toohello kod pobiera dostępu przy użyciu parametrów połączenia magazynu hello z hello *.cscfg* pliku.</span><span class="sxs-lookup"><span data-stu-id="f72fb-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="f72fb-423">Następnie pobiera toohello odwołanie *obrazów* kontenera obiektów blob, tworzy kontener hello, jeśli jeszcze nie istnieje, i zestawów uprawnień dostępu na powitania nowy kontener.</span><span class="sxs-lookup"><span data-stu-id="f72fb-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="f72fb-424">Domyślnie nowe kontenery tylko zezwolić klientom z kontem magazynu obiektów blob tooaccess poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="f72fb-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="f72fb-425">Hello witryny sieci Web wymaga hello publicznego toobe obiektów blob, aby możliwe było wyświetlanie obrazów przy użyciu adresów URL tego obiekty BLOB obrazów toohello punktu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="f72fb-426">Podobny kod pobiera odwołanie toohello *obrazów* kolejki i tworzy nową kolejkę.</span><span class="sxs-lookup"><span data-stu-id="f72fb-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="f72fb-427">W takim przypadku nie trzeba zmieniać uprawnień.</span><span class="sxs-lookup"><span data-stu-id="f72fb-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="f72fb-428">ContosoAdsWeb — \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="f72fb-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="f72fb-429">Witaj *_Layout.cshtml* plik ustawia nazwę aplikacji hello w hello nagłówku i stopce oraz utworzenie wpisu menu "Ads".</span><span class="sxs-lookup"><span data-stu-id="f72fb-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="f72fb-430">ContosoAdsWeb — Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="f72fb-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="f72fb-431">Witaj *Views\Home\Index.cshtml* pliku wyświetla linków kategorii na stronie głównej hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="f72fb-432">Witaj linki przekazują wartość całkowitą hello hello `Category` wyliczenia na stronie indeksu reklam toohello zmiennej querystring.</span><span class="sxs-lookup"><span data-stu-id="f72fb-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="f72fb-433">ContosoAdsWeb — AdController.cs</span><span class="sxs-lookup"><span data-stu-id="f72fb-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="f72fb-434">W hello *AdController.cs* plik, hello wywołania konstruktora hello `InitializeStorage` — metoda toocreate biblioteki klienta magazynu Azure obiektów, które zapewniają interfejs API do pracy z obiektów blob i kolejek.</span><span class="sxs-lookup"><span data-stu-id="f72fb-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="f72fb-435">Następnie hello kod pobiera odwołanie toohello *obrazów* kontenera obiektów blob, jak przedstawiono wcześniej w *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="f72fb-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="f72fb-436">W tym czasie ustawiane są domyślne [zasady ponawiania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) odpowiednie dla aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f72fb-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="f72fb-437">zasady ponawiania wykładniczego wycofywania domyślne Hello mogą powodować zawieszanie aplikacji sieci web hello przez czas dłuższy niż minuta w przypadku kolejnych prób błędu przejściowego.</span><span class="sxs-lookup"><span data-stu-id="f72fb-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="f72fb-438">Witaj zasady ponawiania określone w tym miejscu czeka trzy sekundy po każdej się toothree prób.</span><span class="sxs-lookup"><span data-stu-id="f72fb-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="f72fb-439">Podobny kod pobiera odwołanie toohello *obrazów* kolejki.</span><span class="sxs-lookup"><span data-stu-id="f72fb-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="f72fb-440">Większość kodu kontrolera hello jest typowa dla pracy z modelem danych programu Entity Framework za pomocą klasy DbContext.</span><span class="sxs-lookup"><span data-stu-id="f72fb-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="f72fb-441">Wyjątkiem jest hello HttpPost `Create` metodę, która przekazuje plik i zapisuje je w magazynie obiektów blob.</span><span class="sxs-lookup"><span data-stu-id="f72fb-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="f72fb-442">udostępnia integratora modelu Hello [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) obiekt toohello metody.</span><span class="sxs-lookup"><span data-stu-id="f72fb-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="f72fb-443">Użytkownika hello zaznaczenie tooupload pliku, kod hello hello plik zostanie przesłany, zapisuje go w obiekcie blob i aktualizacji rekordu bazy danych Ad hello adres URL, który wskazuje obiekt blob toohello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="f72fb-444">Witaj kod hello przekazywania jest hello `UploadAndSaveBlobAsync` metody.</span><span class="sxs-lookup"><span data-stu-id="f72fb-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="f72fb-445">Tworzy nazwę identyfikatora GUID dla obiektu blob hello, przekazywanie i zapisuje plik hello i zwraca odwołanie do obiektu blob toohello zapisane.</span><span class="sxs-lookup"><span data-stu-id="f72fb-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

```csharp
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
```

<span data-ttu-id="f72fb-446">Po hello HttpPost `Create` metoda przekazuje obiekt blob i aktualizacje hello bazy danych, tworzy tooinform komunikat kolejki tego procesu zaplecza, że obraz jest gotowy do konwersji tooa miniatur.</span><span class="sxs-lookup"><span data-stu-id="f72fb-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="f72fb-447">Witaj kod hello HttpPost `Edit` metoda jest podobna z tą różnicą, że jeśli hello użytkownik wybierze nowy plik obrazu należy usunąć wszystkie obiekty BLOB, które już istnieją.</span><span class="sxs-lookup"><span data-stu-id="f72fb-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="f72fb-448">Witaj kolejnym przykładzie pokazano kod hello usuwania obiektów blob podczas usuwania reklamy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="f72fb-449">ContosoAdsWeb — Views\Ad\Index.cshtml i Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="f72fb-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="f72fb-450">Witaj *Index.cshtml* służy do wyświetlania miniatury z hello innymi danymi reklamy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="f72fb-451">Witaj *Details.cshtml* pliku wyświetla hello obrazu w pełnym rozmiarze.</span><span class="sxs-lookup"><span data-stu-id="f72fb-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="f72fb-452">ContosoAdsWeb — Views\Ad\Create.cshtml i Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="f72fb-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="f72fb-453">Witaj *Create.cshtml* i *Edit.cshtml* pliki określają kodowanie, że umożliwia hello hello tooget kontrolera formularza `HttpPostedFileBase` obiektu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="f72fb-454">`<input>` Informuje hello przeglądarki tooprovide okna dialogowego wyboru pliku.</span><span class="sxs-lookup"><span data-stu-id="f72fb-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="f72fb-455">ContosoAdsWorker — WorkerRole.cs — metoda OnStart</span><span class="sxs-lookup"><span data-stu-id="f72fb-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="f72fb-456">środowisko roli procesu roboczego platformy Azure Hello wywołuje hello `OnStart` metoda hello `WorkerRole` klasy, gdy rola proces roboczy hello jest wprowadzenie i wywołuje hello `Run` metodą podczas hello `OnStart` zakończeniu działania metody.</span><span class="sxs-lookup"><span data-stu-id="f72fb-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="f72fb-457">Witaj `OnStart` metoda pobiera parametry połączenia bazy danych hello z hello *.cscfg* i przekazuje je toohello klasy Entity Framework DbContext.</span><span class="sxs-lookup"><span data-stu-id="f72fb-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="f72fb-458">Dostawca SQLClient Hello jest używany domyślnie, więc hello dostawca nie ma toobe określony.</span><span class="sxs-lookup"><span data-stu-id="f72fb-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="f72fb-459">Po wykonaniu tej hello metoda pobiera odwołanie do konta magazynu toohello i tworzy hello kontenera obiektów blob i kolejki, jeśli nie istnieją.</span><span class="sxs-lookup"><span data-stu-id="f72fb-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="f72fb-460">Kod Hello tej jest podobne toowhat był już wyświetlany w roli sieci web hello `Application_Start` metody.</span><span class="sxs-lookup"><span data-stu-id="f72fb-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="f72fb-461">ContosoAdsWorker — WorkerRole.cs — metoda Run</span><span class="sxs-lookup"><span data-stu-id="f72fb-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="f72fb-462">Witaj `Run` metoda jest wywoływana, gdy hello `OnStart` metoda zakończy się inicjowanie.</span><span class="sxs-lookup"><span data-stu-id="f72fb-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="f72fb-463">Witaj metoda wykonuje nieskończoną pętlę, która oczekuje na nowe komunikaty w kolejce i przetwarza je po nadejściu.</span><span class="sxs-lookup"><span data-stu-id="f72fb-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="f72fb-464">Po każdej iteracji pętli hello Jeśli komunikatu w kolejce nie został znaleziony, hello program zostanie uśpiony na sekundę.</span><span class="sxs-lookup"><span data-stu-id="f72fb-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="f72fb-465">Zapobiega to ponoszenia nadmiernych kosztów Procesora czas i Magazyn transakcji hello roli procesu roboczego.</span><span class="sxs-lookup"><span data-stu-id="f72fb-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="f72fb-466">Witaj zespół doradczy klientów firmy Microsoft opowiada historię o deweloperze, który zapomniał tooinclude, wdrożyć tooproduction i wyjechał na urlop.</span><span class="sxs-lookup"><span data-stu-id="f72fb-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="f72fb-467">Gdy zorientował się ponownie, jego poniesione koszty były wyższe niż koszty urlopu hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="f72fb-468">Czasami zawartość komunikatu w kolejce hello powoduje błąd podczas przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="f72fb-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="f72fb-469">Ta metoda jest wywoływana *Trująca wiadomość*, a jeśli właśnie zarejestrowano błąd i ponownym uruchomieniu pętli hello można nieskończoność ponawiać próby tooprocess tej wiadomości.</span><span class="sxs-lookup"><span data-stu-id="f72fb-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="f72fb-470">W związku z tym hello blok catch zawiera if instrukcji, która sprawdza toosee ile razy aplikacja hello podjął tooprocess hello bieżącego komunikatu, a jeśli został on więcej niż 5 razy, wiadomość hello jest usuwane z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="f72fb-471">`ProcessQueueMessage` — ten element jest wywoływany po znalezieniu komunikatu w kolejce.</span><span class="sxs-lookup"><span data-stu-id="f72fb-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="f72fb-472">Ten kod odczytuje adres URL obrazu hello hello bazy danych tooget, konwertuje hello obrazu tooa miniatur, zapisuje miniaturę hello w obiekcie blob, aktualizuje bazę danych hello z adresem URL obiektu blob miniatury hello i usuwa komunikat z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="f72fb-473">Witaj kodu w hello `ConvertImageToThumbnailJPG` metoda używa klas w przestrzeni nazw System.Drawing powitania dla uproszczenia.</span><span class="sxs-lookup"><span data-stu-id="f72fb-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="f72fb-474">Jednak klasy hello w tej przestrzeni nazw zostały zaprojektowane do użytku z formularzy systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="f72fb-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="f72fb-475">Nie są one obsługiwane w usłudze systemu Windows lub programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f72fb-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="f72fb-476">Aby uzyskać więcej informacji o opcjach przetwarzania obrazu, zobacz [Dynamiczne generowanie obrazu](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) i [Bezpośrednie zmienianie rozmiaru obrazu](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span><span class="sxs-lookup"><span data-stu-id="f72fb-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="f72fb-477">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="f72fb-477">Troubleshooting</span></span>
<span data-ttu-id="f72fb-478">W przypadku, gdy coś nie działa podczas postępujesz zgodnie z instrukcjami hello w tym samouczku, poniżej przedstawiono niektóre typowe błędy i w jaki sposób tooresolve je.</span><span class="sxs-lookup"><span data-stu-id="f72fb-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="f72fb-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="f72fb-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="f72fb-480">Witaj `RoleEnvironment` obiektu jest dostarczany przez platformę Azure po uruchomieniu aplikacji na platformie Azure lub po uruchomieniu lokalnie przy użyciu emulatora obliczeń platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="f72fb-481">Jeśli ten błąd wystąpi, jeśli są uruchomione lokalnie, upewnij się, że ustawiono projektu ContosoAdsCloudService hello jako projekt startowy hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="f72fb-482">Konfiguruje hello toorun projektu przy użyciu emulatora obliczeń platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="f72fb-483">Jest jeden z elementów hello zastosowań aplikacji hello hello Azure RoleEnvironment dla wartości parametrów połączeń hello tooget, które są przechowywane w hello *.cscfg* pliki, więc inną przyczyną tego wyjątku jest Brak parametrów połączenia.</span><span class="sxs-lookup"><span data-stu-id="f72fb-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="f72fb-484">Upewnij się, utworzony hello ustawienie StorageConnectionString w chmurze i lokalnej w projekcie ContosoAdsWeb hello i utworzyć parametry połączenia dla obydwu konfiguracji w projekcie ContosoAdsWorker hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="f72fb-485">Jeśli chcesz **Znajdź wszystkie** wyszukiwania dla elementu StorageConnectionString w całym rozwiązaniu hello, powinny pojawić się on znaleziony 9 razy w 6 plikach.</span><span class="sxs-lookup"><span data-stu-id="f72fb-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="f72fb-486">Nie można zastąpić tooport xxx.</span><span class="sxs-lookup"><span data-stu-id="f72fb-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="f72fb-487">Nowy port poniżej minimalnej dozwolonej wartości 8080 dla protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="f72fb-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="f72fb-488">Spróbuj zmienić hello numeru portu używanego przez hello projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="f72fb-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="f72fb-489">Kliknij prawym przyciskiem myszy projekt ContosoAdsWeb hello, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="f72fb-490">Kliknij przycisk hello **Web** karcie, a następnie zmień numer portu hello w hello **adres Url projektu** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="f72fb-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="f72fb-491">Kolejny alternatywny sposób rozwiązania problemu hello Zobacz hello następujących sekcji.</span><span class="sxs-lookup"><span data-stu-id="f72fb-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="f72fb-492">Inne błędy po uruchomieniu w środowisku lokalnym</span><span class="sxs-lookup"><span data-stu-id="f72fb-492">Other errors when running locally</span></span>
<span data-ttu-id="f72fb-493">W chmurze nowego domyślnego projektów usług Użyj hello obliczeń platformy Azure emulator express toosimulate hello środowiska platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f72fb-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="f72fb-494">Jest to Uproszczona wersja hello pełnego emulatora obliczeń, a w niektórych warunkach hello pełnego emulatora będzie działać, gdy hello wersja ekspresowa nie.</span><span class="sxs-lookup"><span data-stu-id="f72fb-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="f72fb-495">toochange hello projektu toouse hello pełnego emulatora, kliknij prawym przyciskiem myszy projekt ContosoAdsCloudService hello, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f72fb-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="f72fb-496">W hello **właściwości** oknie kliknij hello **Web** , a następnie kliknij pozycję hello **użyj pełnego emulatora** przycisk radiowy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="f72fb-497">Kolejność aplikacji hello toorun z pełnego emulatora hello masz tooopen programu Visual Studio z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="f72fb-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f72fb-498">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f72fb-498">Next steps</span></span>
<span data-ttu-id="f72fb-499">Witaj aplikacja Contoso Ads została celowo uproszczona samouczek ułatwiający Rozpoczynanie pracy.</span><span class="sxs-lookup"><span data-stu-id="f72fb-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="f72fb-500">Na przykład nie implementuje [iniekcji zależności](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) lub hello [repozytorium i jednostki pracy wzorce](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), nie [używa interfejsu do rejestrowania](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), nie używa [ Migracje EF Code First](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) zmiany modelu danych toomanage lub [elastyczności połączenia platformy EF](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage przejściowe błędy sieciowe i tak dalej.</span><span class="sxs-lookup"><span data-stu-id="f72fb-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="f72fb-501">Poniżej przedstawiono niektóre przykładowe aplikacje usług chmury których zastosowano więcej praktyk kodowania rzeczywistych, w kolejności od mniej złożona toomore złożonych:</span><span class="sxs-lookup"><span data-stu-id="f72fb-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="f72fb-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="f72fb-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="f72fb-503">Podobna tooContoso Ads, ale z zaimplementowaną większą liczbą funkcji i więcej rzeczywistych praktyk kodowania.</span><span class="sxs-lookup"><span data-stu-id="f72fb-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="f72fb-504">[Wielowarstwowa aplikacja usługi w chmurze Azure z tabelami, kolejkami i obiektami blob](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="f72fb-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="f72fb-505">Obejmuje tabele usługi Azure Storage, a także obiekty blob i kolejki.</span><span class="sxs-lookup"><span data-stu-id="f72fb-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="f72fb-506">Oparty na starszej wersji hello Azure SDK dla platformy .NET, będą musieli niektórych toowork modyfikacje hello bieżącej wersji.</span><span class="sxs-lookup"><span data-stu-id="f72fb-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="f72fb-507">[Podstawy usługi w chmurze na platformie Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="f72fb-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="f72fb-508">Kompleksowy przykład przedstawiający szeroki zakres najlepszych rozwiązań tworzonych przez grupę Microsoft Patterns and Practices hello.</span><span class="sxs-lookup"><span data-stu-id="f72fb-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="f72fb-509">Aby uzyskać ogólne informacje o tworzeniu aplikacji hello chmury, zobacz [tworzenia rzeczywistych aplikacji w chmurze platformy Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="f72fb-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="f72fb-510">Dla tooAzure wideo z wprowadzeniem magazynu najlepszych rozwiązań i wzorców, zobacz [Microsoft Azure Storage — nowości nowy, najlepsze rozwiązania i wzorce](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="f72fb-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="f72fb-511">Aby uzyskać więcej informacji zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="f72fb-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="f72fb-512">Azure Cloud Services, część 1: wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="f72fb-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="f72fb-513">W jaki sposób toomanage usług w chmurze</span><span class="sxs-lookup"><span data-stu-id="f72fb-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="f72fb-514">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f72fb-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="f72fb-515">Jak dostawca usług chmury toochoose</span><span class="sxs-lookup"><span data-stu-id="f72fb-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
