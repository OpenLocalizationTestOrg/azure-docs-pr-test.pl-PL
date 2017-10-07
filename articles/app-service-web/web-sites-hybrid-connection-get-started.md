---
title: "aaaAccess zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service"
description: "Utwórz połączenie między aplikacji sieci web w usłudze Azure App Service i zasobu lokalnego, który używa portu TCP statycznego"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: a46ed26b-df8e-4fc3-8e05-2d002a6ee508
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2016
ms.author: cephalin
ms.openlocfilehash: de7c57b94f4bd6250a93757817178e8455daae4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="8f959-103">Dostęp do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="8f959-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="8f959-104">Można połączyć z usługi aplikacji Azure tooany lokalnymi zasób aplikacji używającej portu statycznego TCP, takich jak SQL Server, MySQL, interfejsów API sieci Web HTTP i większość niestandardowych usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="8f959-104">You can connect an Azure App Service app tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="8f959-105">W tym artykule opisano sposób toocreate połączenie hybrydowe między usługą aplikacji i lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f959-105">This article shows you how toocreate a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="8f959-106">Witaj aplikacje sieci Web część funkcji połączeń hybrydowych hello jest dostępna tylko w hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8f959-106">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="8f959-107">Zobacz toocreate połączenie usługi BizTalk Services [połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="8f959-107">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="8f959-108">Ta zawartość dotyczy również tooMobile aplikacji w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8f959-108">This content also applies tooMobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8f959-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8f959-109">Prerequisites</span></span>
* <span data-ttu-id="8f959-110">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8f959-110">An Azure subscription.</span></span> <span data-ttu-id="8f959-111">Aby uzyskać bezpłatną subskrypcję, zobacz [bezpłatnej wersji próbnej Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8f959-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="8f959-112">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="8f959-112">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8f959-113">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="8f959-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="8f959-114">toouse lokalnego programu SQL Server lub SQL Server Express bazy danych z połączenia hybrydowego TCP/IP musi toobe włączone portu statycznego.</span><span class="sxs-lookup"><span data-stu-id="8f959-114">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="8f959-115">Przy użyciu domyślnego wystąpienia serwera SQL jest zalecane, ponieważ używa portu statycznego 1433.</span><span class="sxs-lookup"><span data-stu-id="8f959-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="8f959-116">Aby uzyskać informacje na temat instalowania i konfigurowania programu SQL Server Express do użycia z połączeń hybrydowych było możliwe, zobacz [tooan połączenia lokalnego programu SQL Server z Azure witryny sieci web za pomocą połączeń hybrydowych](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="8f959-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="8f959-117">Witaj komputera, na którym jest instalowany agent Menedżera połączeń hybrydowych lokalne powitania opisane w dalszej części tego artykułu:</span><span class="sxs-lookup"><span data-stu-id="8f959-117">hello computer on which you install hello on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="8f959-118">Musi być możliwe tooconnect tooAzure za pośrednictwem portu 5671</span><span class="sxs-lookup"><span data-stu-id="8f959-118">Must be able tooconnect tooAzure over port 5671</span></span>
  * <span data-ttu-id="8f959-119">Musi być w stanie tooreach hello *hostname*:*numer_portu* zasobu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="8f959-119">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="8f959-120">Hello opisanych w tym artykule założono, że używasz przeglądarki hello z hello komputer, który będzie hostem agenta połączenia hybrydowego lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="8f959-120">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="8f959-121">Tworzenie aplikacji sieci web w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8f959-121">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="8f959-122">Jeśli utworzono już aplikację sieci web lub zaplecza aplikacji mobilnej w hello mają toouse w tym samouczku portalu Azure, możesz przejść od razu zbyt[Tworzenie połączenia hybrydowego i usługi BizTalk](#CreateHC) i uruchomić stamtąd.</span><span class="sxs-lookup"><span data-stu-id="8f959-122">If you have already created a web app or Mobile App backend in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="8f959-123">W hello lewego górnego rogu hello [Azure Portal](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="8f959-123">In hello upper left corner of hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Nowa aplikacja sieci web][NewWebsite]
2. <span data-ttu-id="8f959-125">Na powitania **aplikacji sieci Web** bloku, podaj adres URL i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8f959-125">On hello **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Nazwa witryny sieci Web][WebsiteCreationBlade]
3. <span data-ttu-id="8f959-127">Po kilku chwilach hello aplikacji sieci web jest tworzona i pojawia się jego bloku aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="8f959-127">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="8f959-128">Blok Hello jest pionowo przewijanego pulpit nawigacyjny, który umożliwia zarządzanie witryną.</span><span class="sxs-lookup"><span data-stu-id="8f959-128">hello blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Witryny sieci Web uruchomionej][WebSiteRunningBlade]
4. <span data-ttu-id="8f959-130">Witryna hello tooverify na żywo, można kliknąć hello **Przeglądaj** ikona toodisplay hello domyślnej strony.</span><span class="sxs-lookup"><span data-stu-id="8f959-130">tooverify hello site is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>
   
    ![Kliknij przycisk Przeglądaj toosee aplikacji sieci web][Browse]
   
    ![Domyślna strona aplikacji sieci web][DefaultWebSitePage]

<span data-ttu-id="8f959-133">Następnie utworzysz, połączenie hybrydowe i usługi BizTalk hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="8f959-133">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="8f959-134">Tworzenie połączenia hybrydowego i usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="8f959-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="8f959-135">W bloku aplikacja sieci web kliknij **wszystkie ustawienia** > **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.</span><span class="sxs-lookup"><span data-stu-id="8f959-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Połączenia hybrydowe][CreateHCHCIcon]
2. <span data-ttu-id="8f959-137">W bloku połączeń hybrydowych hello, kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="8f959-137">On hello Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="8f959-138">Witaj **Dodaj połączenie hybrydowe** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="8f959-138">hello **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="8f959-139">Ponieważ jest to pierwszy połączenia hybrydowe, hello **nowe połączenie hybrydowe** opcja wyświetlana jest wartość i hello **Tworzenie połączenia hybrydowego** zostanie otwarty blok dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="8f959-139">Since this is your first hybrid connection, hello **New hybrid connection** option is preselected, and hello **Create hybrid connection** blade opens for you.</span></span>
   
    ![Tworzenie połączenia hybrydowego][TwinCreateHCBlades]
   
    <span data-ttu-id="8f959-141">Na powitania **bloku połączenia hybrydowe Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="8f959-141">On hello **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="8f959-142">Aby uzyskać **nazwa**, podaj nazwę hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="8f959-142">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="8f959-143">Aby uzyskać **Hostname**, wprowadź nazwę hello hello na lokalnym komputerze, który obsługuje zasobu.</span><span class="sxs-lookup"><span data-stu-id="8f959-143">For **Hostname**, enter hello name of hello on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="8f959-144">Aby uzyskać **portu**, wprowadź numer portu hello używany zasób lokalną (1433 dla domyślnego wystąpienia programu SQL Server).</span><span class="sxs-lookup"><span data-stu-id="8f959-144">For **Port**, enter hello port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="8f959-145">Kliknij przycisk **Biz Talk usługi**</span><span class="sxs-lookup"><span data-stu-id="8f959-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="8f959-146">Witaj **Utwórz usługę BizTalk** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="8f959-146">hello **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="8f959-147">Wprowadź nazwę hello usługi BizTalk, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f959-147">Enter a name for hello BizTalk service, and then click **OK**.</span></span>
   
    ![Utwórz usługę BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="8f959-149">Witaj **Utwórz usługę BizTalk** bloku zamyka i są zwracane toohello **Tworzenie połączenia hybrydowego** bloku.</span><span class="sxs-lookup"><span data-stu-id="8f959-149">hello **Create BizTalk Service** blade closes and you are returned toohello **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="8f959-150">W bloku połączenia hybrydowe Utwórz hello, kliknij polecenie **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f959-150">On hello Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Kliknij przycisk OK][CreateBTScomplete]
6. <span data-ttu-id="8f959-152">Po zakończeniu procesu hello hello obszar powiadomień w hello portalu informuje o pomyślnie utworzono połączenie hello.</span><span class="sxs-lookup"><span data-stu-id="8f959-152">When hello process completes, hello notifications area in hello Portal informs you that hello connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in hello dogfood portal. I switch toohello classic portal
    (full portal) and created hello BizTalk service but it doesn't seem toolet you connnect them - When you finish the
    Create hybrid conn step, you get hello following error
    Failed toocreate hybrid connection RelecIoudHC. hello 
    resource type could not be found in hello namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    hello error indicates it couldn't find hello type, not hello instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="8f959-153">W bloku aplikacja sieci web hello hello **połączeń hybrydowych** ikona teraz wskazuje, że utworzono połączenie hybrydowe 1.</span><span class="sxs-lookup"><span data-stu-id="8f959-153">On hello web app's blade, hello **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Połączenia hybrydowe jeden utworzone][CreateHCOneConnectionCreated]

<span data-ttu-id="8f959-155">W tym momencie została ukończona ważnym elementem hello chmury hybrydowej połączenia infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="8f959-155">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="8f959-156">Następnie utworzy odpowiedni element lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="8f959-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="8f959-157">Zainstaluj hello lokalnego Menedżera połączeń hybrydowych toocomplete hello połączenia</span><span class="sxs-lookup"><span data-stu-id="8f959-157">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
1. <span data-ttu-id="8f959-158">W bloku aplikacja sieci web powitania kliknij **wszystkie ustawienia** > **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.</span><span class="sxs-lookup"><span data-stu-id="8f959-158">On hello web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Ikona połączenia hybrydowego][HCIcon]
2. <span data-ttu-id="8f959-160">Na powitania **połączeń hybrydowych** bloku, hello **stan** kolumny dla hello niedawno dodano punkt końcowy pokazuje **niepołączone**.</span><span class="sxs-lookup"><span data-stu-id="8f959-160">On hello **Hybrid connections** blade, hello **Status** column for hello recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="8f959-161">Kliknij przycisk tooconfigure połączenia hello go.</span><span class="sxs-lookup"><span data-stu-id="8f959-161">Click hello connection tooconfigure it.</span></span>
   
    ![Nie połączono][NotConnected]
   
    <span data-ttu-id="8f959-163">zostanie otwarty blok połączenia hybrydowe Hello.</span><span class="sxs-lookup"><span data-stu-id="8f959-163">hello Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="8f959-165">W bloku powitania kliknij **konfiguracji odbiornika**.</span><span class="sxs-lookup"><span data-stu-id="8f959-165">On hello blade, click **Listener Setup**.</span></span>
   
    ![Kliknij przycisk Ustawienia odbiornika][ClickListenerSetup]
4. <span data-ttu-id="8f959-167">Witaj **właściwości połączenia hybrydowe** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="8f959-167">hello **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="8f959-168">W obszarze **Menedżera połączeń hybrydowych lokalnymi**, wybierz **kliknij tutaj tooinstall**.</span><span class="sxs-lookup"><span data-stu-id="8f959-168">Under **On-premises Hybrid Connection Manager**, choose **Click here tooinstall**.</span></span>
   
    ![Kliknij tutaj tooinstall][ClickToInstallHCM]
5. <span data-ttu-id="8f959-170">Hello uruchamiać aplikacje zabezpieczeń okno dialogowe z ostrzeżeniem, wybierz **Uruchom** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="8f959-170">In hello Application Run security warning dialog, choose **Run** toocontinue.</span></span>
   
    ![Wybierz polecenie Uruchom toocontinue][ApplicationRunWarning]
6. <span data-ttu-id="8f959-172">W hello **Kontrola konta użytkownika** okno dialogowe, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="8f959-172">In hello **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Wybierz opcję Tak][UAC]
7. <span data-ttu-id="8f959-174">Menedżera połączeń hybrydowych Hello jest pobierane i instalowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="8f959-174">hello Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Instalowanie][HCMInstalling]
8. <span data-ttu-id="8f959-176">Po zakończeniu instalacji powitania kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="8f959-176">When hello install completes, click **Close**.</span></span>
   
    ![Kliknij przycisk Zamknij][HCMInstallComplete]
   
    <span data-ttu-id="8f959-178">Na powitania **połączeń hybrydowych** bloku, hello **stan** zawiera obecnie kolumnę **połączony**.</span><span class="sxs-lookup"><span data-stu-id="8f959-178">On hello **Hybrid connections** blade, hello **Status** column now shows **Connected**.</span></span> 
   
    ![Stan połączenia][HCStatusConnected]

<span data-ttu-id="8f959-180">Po zakończeniu tego połączenia infrastruktura hybrydowa hello można utworzyć aplikacji hybrydowych, która korzysta z niego.</span><span class="sxs-lookup"><span data-stu-id="8f959-180">Now that hello hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="8f959-181">Hello następnych sekcjach opisano sposób toouse połączenie hybrydowe z projektu zaplecza .NET aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="8f959-181">hello following sections show you how toouse a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-hello-mobile-app-net-backend-project-tooconnect-toohello-sql-server-database"></a><span data-ttu-id="8f959-182">Skonfiguruj hello Mobile aplikacji .NET w wewnętrznej bazie danych projektu tooconnect toohello bazy danych SQL Server</span><span class="sxs-lookup"><span data-stu-id="8f959-182">Configure hello Mobile App .NET backend project tooconnect toohello SQL Server database</span></span>
<span data-ttu-id="8f959-183">W usłudze App Service Mobile Apps na platformie .NET projekt wewnętrznej bazy danych jest tylko aplikacji sieci web platformy ASP.NET z dodatkowe zestawu Mobile Apps SDK zainstalowany i zainicjować.</span><span class="sxs-lookup"><span data-stu-id="8f959-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="8f959-184">toouse aplikacji sieci web jako zaplecza aplikacji mobilnej musi [pobierania i zainicjuj hello zaplecza Mobile Apps .NET SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="8f959-184">toouse your web app as a Mobile Apps backend, you must [download and initialize hello Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="8f959-185">Dla aplikacji mobilnych także muszą toodefine ciąg połączenia dla bazy danych lokalne powitania i zmodyfikować hello toouse wewnętrznej bazy danych to połączenie.</span><span class="sxs-lookup"><span data-stu-id="8f959-185">For Mobile Apps, you also need toodefine a connection string for hello on-premises database and modify hello backend toouse this connection.</span></span> 

1. <span data-ttu-id="8f959-186">W Eksploratorze rozwiązań w programie Visual Studio, hello Otwórz plik Web.config dla zaplecza .NET aplikacji mobilnych, Znajdź hello **connectionStrings** Dodaj nowy wpis SqlClient jak hello poniższe polecenie, które toohello punktów lokalnej SQL Serwer bazy danych:</span><span class="sxs-lookup"><span data-stu-id="8f959-186">In Solution Explorer in Visual Studio, open hello Web.config file for your Mobile App .NET backend, locate hello **connectionStrings** section, add a new SqlClient entry like hello following, which points toohello on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="8f959-187">Należy pamiętać, tooreplace `<**secure_password**>` w tym ciągu z hello hasło utworzone dla *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="8f959-187">Remember tooreplace `<**secure_password**>` in this string with hello password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="8f959-188">Kliknij przycisk **zapisać** w pliku Web.config hello toosave programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f959-188">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8f959-189">To ustawienie połączenia jest używany podczas uruchamiania komputera lokalnego hello.</span><span class="sxs-lookup"><span data-stu-id="8f959-189">This connection setting is used when running on hello local computer.</span></span> <span data-ttu-id="8f959-190">Podczas uruchamiania na platformie Azure, to ustawienie jest zastąpione przez ustawienie połączenia hello zdefiniowane w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="8f959-190">When running in Azure, this setting is overriden by hello connection setting defined in hello portal.</span></span>
   > 
   > 
3. <span data-ttu-id="8f959-191">Rozwiń węzeł hello **modele** folderu i pliku modelu danych otwórz hello, która kończy się *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="8f959-191">Expand hello **Models** folder and open hello data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="8f959-192">Modyfikowanie hello **DbContext** toopass konstruktora wystąpienia hello wartość `OnPremisesDBConnection` toohello podstawowej **DbContext** konstruktora, podobne toohello po fragment kodu:</span><span class="sxs-lookup"><span data-stu-id="8f959-192">Modify hello **DbContext** instance constructor toopass hello value `OnPremisesDBConnection` toohello base **DbContext** constructor, similar toohello following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="8f959-193">Usługa Hello użyje teraz hello nowego połączenia toohello bazy danych SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8f959-193">hello service will now use hello new connection toohello SQL Server database.</span></span>

## <a name="update-hello-mobile-app-backend-toouse-hello-on-premises-connection-string"></a><span data-ttu-id="8f959-194">Zaktualizować parametry połączenia lokalne powitania toouse hello aplikacji mobilnej wewnętrznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="8f959-194">Update hello Mobile App backend toouse hello on-premises connection string</span></span>
<span data-ttu-id="8f959-195">Następnie należy tooadd ustawienia aplikacji dla tych nowych parametrów połączenia, dzięki czemu mogą być używane z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8f959-195">Next, you need tooadd an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="8f959-196">Po powrocie do hello [portalu Azure](https://portal.azure.com) w wewnętrznej bazy danych aplikacji kod hello sieci web aplikacji mobilnej kliknij **wszystkie ustawienia**, następnie **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="8f959-196">Back in hello [Azure portal](https://portal.azure.com) in hello web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="8f959-197">W hello **ustawienia aplikacji w sieci Web** bloku, przewiń w dół za**parametry połączenia** i dodać nowe **programu SQL Server** parametrów połączenia o nazwie `OnPremisesDBConnection` o wartości podobnie jak `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="8f959-197">In hello **Web app settings** blade, scroll down too**Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="8f959-198">Zastąp `<**secure_password**>` z bezpiecznym hasłem hello lokalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="8f959-198">Replace `<**secure_password**>` with hello secure password for your on-premises database.</span></span>
   
    ![Parametry połączenia dla lokalnej bazy danych](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="8f959-200">Naciśnij klawisz **zapisać** połączenia hybrydowego hello toosave i parametry połączenia utworzony.</span><span class="sxs-lookup"><span data-stu-id="8f959-200">Press **Save** toosave hello hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="8f959-201">W tym momencie możesz ponownie opublikować projekt serwera hello i przetestować hello nowego połączenia z istniejących klientów Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="8f959-201">At this point you can republish hello server project and test hello new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="8f959-202">Dane będą odczytywane i zapisywane toohello lokalną bazą danych przy użyciu połączenia hybrydowego hello.</span><span class="sxs-lookup"><span data-stu-id="8f959-202">Data will be read from and written toohello on-premises database using hello hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="8f959-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8f959-203">Next Steps</span></span>
* <span data-ttu-id="8f959-204">Aby uzyskać informacje dotyczące tworzenia aplikacji sieci web ASP.NET, która używa połączenie hybrydowe, zobacz [tooan połączenia lokalnego programu SQL Server z Azure witryny sieci web za pomocą połączeń hybrydowych](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="8f959-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect tooan on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="8f959-205">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8f959-205">Additional Resources</span></span>
[<span data-ttu-id="8f959-206">Omówienie połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="8f959-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="8f959-207">Dołączony Josha wprowadza połączeń hybrydowych (wideo z witryny Channel 9)</span><span class="sxs-lookup"><span data-stu-id="8f959-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="8f959-208">Witryna sieci web połączenia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="8f959-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="8f959-209">Usługi BizTalk Services: Karty Pulpit nawigacyjny, Monitor skali, konfigurowanie i połączenia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="8f959-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="8f959-210">Tworzenie hybrydowego rzeczywistych chmury chronionej za pomocą bezproblemowe przenośność aplikacji (Channel 9 wideo)</span><span class="sxs-lookup"><span data-stu-id="8f959-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="8f959-211">Połącz tooan lokalnego programu SQL Server z usługi Azure Mobile Services za pomocą połączeń hybrydowych (wideo z witryny Channel 9)</span><span class="sxs-lookup"><span data-stu-id="8f959-211">Connect tooan on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="8f959-212">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="8f959-212">What's changed</span></span>
* <span data-ttu-id="8f959-213">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8f959-213">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[New]:./media/web-sites-hybrid-connection-get-started/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-get-started/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-get-started/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-get-started/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-get-started/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-get-started/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-get-started/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-get-started/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-get-started/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-get-started/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-get-started/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-get-started/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-get-started/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-get-started/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-get-started/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-get-started/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-get-started/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-get-started/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-get-started/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-get-started/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-get-started/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-get-started/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-get-started/D10HCStatusConnected.png
