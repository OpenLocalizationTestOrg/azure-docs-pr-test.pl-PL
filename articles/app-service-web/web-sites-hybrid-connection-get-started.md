---
title: "Dostęp do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service"
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
ms.openlocfilehash: fbd22e6e285c5ddaef2a473671d4a06a97384b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="access-on-premises-resources-using-hybrid-connections-in-azure-app-service"></a><span data-ttu-id="2ab8e-103">Dostęp do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="2ab8e-103">Access on-premises resources using hybrid connections in Azure App Service</span></span>
<span data-ttu-id="2ab8e-104">Możesz połączyć aplikację usługi aplikacji Azure do dowolnego zasobu lokalnego, który korzysta z portu statycznego TCP, takich jak SQL Server, MySQL, interfejsów API sieci Web HTTP i większość niestandardowych usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-104">You can connect an Azure App Service app to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="2ab8e-105">W tym artykule przedstawiono sposób utworzyć połączenie hybrydowe między usługą aplikacji i lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-105">This article shows you how to create a hybrid connection between App Service and an on-premises SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="2ab8e-106">Aplikacje sieci Web część funkcji połączeń hybrydowych było możliwe jest dostępna tylko w [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2ab8e-106">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="2ab8e-107">Aby utworzyć połączenie w usługi BizTalk Services, zobacz [połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="2ab8e-107">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span> 
> 
> <span data-ttu-id="2ab8e-108">Ta zawartość dotyczy również Mobile Apps w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-108">This content also applies to Mobile Apps in Azure App Service.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2ab8e-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2ab8e-109">Prerequisites</span></span>
* <span data-ttu-id="2ab8e-110">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-110">An Azure subscription.</span></span> <span data-ttu-id="2ab8e-111">Aby uzyskać bezpłatną subskrypcję, zobacz [bezpłatnej wersji próbnej Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2ab8e-111">For a free subscription, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
  
    <span data-ttu-id="2ab8e-112">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-112">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2ab8e-113">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-113">No credit cards required; no commitments.</span></span>
* <span data-ttu-id="2ab8e-114">Aby użyć lokalnego programu SQL Server lub SQL Server Express bazy danych z połączenia hybrydowego, TCP/IP musi być włączona na portu statycznego.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-114">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="2ab8e-115">Przy użyciu domyślnego wystąpienia serwera SQL jest zalecane, ponieważ używa portu statycznego 1433.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-115">Using a default instance on SQL Server is recommended because it uses static port 1433.</span></span> <span data-ttu-id="2ab8e-116">Aby uzyskać informacje na temat instalowania i konfigurowania programu SQL Server Express do użycia z połączeń hybrydowych było możliwe, zobacz [Połącz z lokalnego serwera SQL z Azure witryny sieci web za pomocą połączeń hybrydowych](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="2ab8e-116">For information on installing and configuring SQL Server Express for use with hybrid connections, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span>
* <span data-ttu-id="2ab8e-117">Komputer, na którym instalowany agenta menedżera połączeń hybrydowych lokalnymi opisane w dalszej części tego artykułu:</span><span class="sxs-lookup"><span data-stu-id="2ab8e-117">The computer on which you install the on-premises Hybrid Connection Manager agent described later in this article:</span></span>
  
  * <span data-ttu-id="2ab8e-118">Musi mieć możliwość połączenia z platformą Azure za pośrednictwem portu 5671</span><span class="sxs-lookup"><span data-stu-id="2ab8e-118">Must be able to connect to Azure over port 5671</span></span>
  * <span data-ttu-id="2ab8e-119">Musi być możliwe nawiązanie łączności *hostname*:*numer_portu* zasobu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-119">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span> 

> [!NOTE]
> <span data-ttu-id="2ab8e-120">Kroki opisane w tym artykule założono, że używasz przeglądarki z komputera, który będzie hostem agenta połączenia hybrydowego lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-120">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>
> 
> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="2ab8e-121">Tworzenie aplikacji sieci web w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2ab8e-121">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="2ab8e-122">Jeśli utworzono już aplikację sieci web lub zaplecza aplikacji mobilnej w portalu Azure, który ma być używany na potrzeby tego samouczka, możesz przejść od razu do [Tworzenie połączenia hybrydowego i usługi BizTalk](#CreateHC) i uruchomić stamtąd.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-122">If you have already created a web app or Mobile App backend in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and start from there.</span></span>
> 
> 

1. <span data-ttu-id="2ab8e-123">W lewym górnym rogu [Azure Portal](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-123">In the upper left corner of the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web App**.</span></span>
   
    ![Nowa aplikacja sieci web][NewWebsite]
2. <span data-ttu-id="2ab8e-125">Na **aplikacji sieci Web** bloku, podaj adres URL i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-125">On the **Web app** blade, provide a URL and click **Create**.</span></span> 
   
    ![Nazwa witryny sieci Web][WebsiteCreationBlade]
3. <span data-ttu-id="2ab8e-127">Po kilku chwilach aplikacji sieci web jest tworzona i pojawia się jego bloku aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-127">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="2ab8e-128">Blok jest pionowo przewijanego pulpit nawigacyjny, który umożliwia zarządzanie witryną.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-128">The blade is a vertically scrollable dashboard that lets you manage your site.</span></span>
   
    ![Witryny sieci Web uruchomionej][WebSiteRunningBlade]
4. <span data-ttu-id="2ab8e-130">Aby sprawdzić, witryna jest na żywo, można kliknąć **Przeglądaj** ikonę, aby wyświetlić stronę domyślną.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-130">To verify the site is live, you can click the **Browse** icon to display the default page.</span></span>
   
    ![Kliknij przycisk Przeglądaj, aby wyświetlić aplikację sieci web][Browse]
   
    ![Domyślna strona aplikacji sieci web][DefaultWebSitePage]

<span data-ttu-id="2ab8e-133">Następnie utworzysz połączenie hybrydowe i usługa BizTalk aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-133">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="2ab8e-134">Tworzenie połączenia hybrydowego i usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="2ab8e-134">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="2ab8e-135">W bloku aplikacja sieci web kliknij **wszystkie ustawienia** > **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-135">In your web app blade click on **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Połączenia hybrydowe][CreateHCHCIcon]
2. <span data-ttu-id="2ab8e-137">W bloku połączeń hybrydowych, kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-137">On the Hybrid connections blade, click **Add**.</span></span>
   
    <!-- ![Add a hybrid connnection][CreateHCAddHC]
   -->
3. <span data-ttu-id="2ab8e-138">**Dodaj połączenie hybrydowe** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-138">The **Add a hybrid connection** blade opens.</span></span>  <span data-ttu-id="2ab8e-139">Ponieważ jest to pierwsze połączenie hybrydowe, **nowe połączenie hybrydowe** wyświetlana jest wartość i **Tworzenie połączenia hybrydowego** zostanie otwarty blok dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-139">Since this is your first hybrid connection, the **New hybrid connection** option is preselected, and the **Create hybrid connection** blade opens for you.</span></span>
   
    ![Tworzenie połączenia hybrydowego][TwinCreateHCBlades]
   
    <span data-ttu-id="2ab8e-141">Na **bloku połączenia hybrydowe Utwórz**:</span><span class="sxs-lookup"><span data-stu-id="2ab8e-141">On the **Create hybrid connection blade**:</span></span>
   
   * <span data-ttu-id="2ab8e-142">Aby uzyskać **nazwa**, podaj nazwę dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-142">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="2ab8e-143">Aby uzyskać **Hostname**, wprowadź nazwę komputera lokalnego, który obsługuje zasobu.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-143">For **Hostname**, enter the name of the on-premises computer that hosts your resource.</span></span>
   * <span data-ttu-id="2ab8e-144">Aby uzyskać **portu**, wprowadź numer portu używany zasób lokalną (1433 dla domyślnego wystąpienia programu SQL Server).</span><span class="sxs-lookup"><span data-stu-id="2ab8e-144">For **Port**, enter the port number that your on-premises resource uses (1433 for a SQL Server default instance).</span></span>
   * <span data-ttu-id="2ab8e-145">Kliknij przycisk **Biz Talk usługi**</span><span class="sxs-lookup"><span data-stu-id="2ab8e-145">Click **Biz Talk Service**</span></span>
4. <span data-ttu-id="2ab8e-146">**Utwórz usługę BizTalk** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-146">The **Create BizTalk Service** blade opens.</span></span> <span data-ttu-id="2ab8e-147">Wprowadź nazwę usługi BizTalk, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-147">Enter a name for the BizTalk service, and then click **OK**.</span></span>
   
    ![Utwórz usługę BizTalk][CreateHCCreateBTS]
   
    <span data-ttu-id="2ab8e-149">**Utwórz usługę BizTalk** bloku zamyka i nastąpi powrót do **Tworzenie połączenia hybrydowego** bloku.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-149">The **Create BizTalk Service** blade closes and you are returned to the **Create hybrid connection** blade.</span></span>
5. <span data-ttu-id="2ab8e-150">W bloku Utwórz hybrydowe połączenia, kliknij polecenie **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-150">On the Create hybrid connection blade, click **OK**.</span></span> 
   
    ![Kliknij przycisk OK][CreateBTScomplete]
6. <span data-ttu-id="2ab8e-152">Po zakończeniu tego procesu, obszar powiadomień, w portalu informuje o pomyślnie utworzono połączenie.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-152">When the process completes, the notifications area in the Portal informs you that the connection has been successfully created.</span></span>
   
    <!--- TODO
   
    Everything fails at this step. I can't create a BizTalk service in the dogfood portal. I switch to the classic portal
    (full portal) and created the BizTalk service but it doesn't seem to let you connnect them - When you finish the
    Create hybrid conn step, you get the following error
    Failed to create hybrid connection RelecIoudHC. The 
    resource type could not be found in the namespace 
    'Microsoft.BizTaIkServices for api version 2014-06-01'.
   
    The error indicates it couldn't find the type, not the instance.
    ![Success notification][CreateHCSuccessNotification]
    -->
7. <span data-ttu-id="2ab8e-153">W bloku aplikacja sieci web **połączeń hybrydowych** ikona teraz wskazuje, że utworzono połączenie hybrydowe 1.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-153">On the web app's blade, the **Hybrid connections** icon now shows that 1 hybrid connection has been created.</span></span>
   
    ![Połączenia hybrydowe jeden utworzone][CreateHCOneConnectionCreated]

<span data-ttu-id="2ab8e-155">W tym momencie została ukończona ważnym elementem infrastruktury połączenia hybrydowe w chmurze.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-155">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="2ab8e-156">Następnie utworzy odpowiedni element lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-156">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="2ab8e-157">Zainstaluj Menedżera połączeń hybrydowych lokalnego, aby nawiązać połączenie</span><span class="sxs-lookup"><span data-stu-id="2ab8e-157">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
1. <span data-ttu-id="2ab8e-158">W bloku aplikacja sieci web, kliknij przycisk **wszystkie ustawienia** > **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-158">On the web app's blade, click **All settings** > **Networking** > **Configure your hybrid connection endpoints**.</span></span> 
   
    ![Ikona połączenia hybrydowego][HCIcon]
2. <span data-ttu-id="2ab8e-160">Na **połączeń hybrydowych** bloku **stan** kolumny dla przedstawia ostatnio dodany punkt końcowy **niepołączone**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-160">On the **Hybrid connections** blade, the **Status** column for the recently added endpoint shows **Not connected**.</span></span> <span data-ttu-id="2ab8e-161">Kliknij połączenie, aby go skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-161">Click the connection to configure it.</span></span>
   
    ![Nie połączono][NotConnected]
   
    <span data-ttu-id="2ab8e-163">Zostanie otwarty blok połączeń hybrydowych.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-163">The Hybrid connection blade opens.</span></span>
   
    ![NotConnectedBlade][NotConnectedBlade]
3. <span data-ttu-id="2ab8e-165">W bloku, kliknij **konfiguracji odbiornika**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-165">On the blade, click **Listener Setup**.</span></span>
   
    ![Kliknij przycisk Ustawienia odbiornika][ClickListenerSetup]
4. <span data-ttu-id="2ab8e-167">**Właściwości połączenia hybrydowe** zostanie otwarty blok.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-167">The **Hybrid connection properties** blade opens.</span></span> <span data-ttu-id="2ab8e-168">W obszarze **Menedżera połączeń hybrydowych lokalnymi**, wybierz **kliknij tutaj, aby zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-168">Under **On-premises Hybrid Connection Manager**, choose **Click here to install**.</span></span>
   
    ![Kliknij tutaj, aby zainstalować][ClickToInstallHCM]
5. <span data-ttu-id="2ab8e-170">W oknie Uruchamianie aplikacji Ostrzeżenie zabezpieczeń wybierz **Uruchom** aby kontynuować.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-170">In the Application Run security warning dialog, choose **Run** to continue.</span></span>
   
    ![Wybierz polecenie Uruchom, aby kontynuować][ApplicationRunWarning]
6. <span data-ttu-id="2ab8e-172">W **Kontrola konta użytkownika** okno dialogowe, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-172">In the **User Account Control** dialog, choose **Yes**.</span></span>
   
   ![Wybierz opcję Tak][UAC]
7. <span data-ttu-id="2ab8e-174">Menedżera połączeń hybrydowych jest pobierane i instalowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-174">The Hybrid Connection Manager is downloaded and installed for you.</span></span> 
   
    ![Instalowanie][HCMInstalling]
8. <span data-ttu-id="2ab8e-176">Po zakończeniu instalacji kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-176">When the install completes, click **Close**.</span></span>
   
    ![Kliknij przycisk Zamknij][HCMInstallComplete]
   
    <span data-ttu-id="2ab8e-178">Na **połączeń hybrydowych** bloku **stan** zawiera obecnie kolumnę **połączony**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-178">On the **Hybrid connections** blade, the **Status** column now shows **Connected**.</span></span> 
   
    ![Stan połączenia][HCStatusConnected]

<span data-ttu-id="2ab8e-180">Teraz, infrastruktura hybrydowa połączenie zostanie zakończone, można utworzyć aplikacji hybrydowych, która korzysta z niego.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-180">Now that the hybrid connection infrastructure is complete, you can create a hybrid application that uses it.</span></span> 

> [!NOTE]
> <span data-ttu-id="2ab8e-181">Poniższe sekcje pokazują, jak użyć połączenie hybrydowe z projektu zaplecza .NET aplikacji mobilnej.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-181">The following sections show you how to use a hybrid connection with a Mobile Apps .NET backend project.</span></span>
> 
> 

## <a name="configure-the-mobile-app-net-backend-project-to-connect-to-the-sql-server-database"></a><span data-ttu-id="2ab8e-182">Konfigurowanie projektu zaplecza .NET aplikacji mobilnej do łączenia z bazą danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="2ab8e-182">Configure the Mobile App .NET backend project to connect to the SQL Server database</span></span>
<span data-ttu-id="2ab8e-183">W usłudze App Service Mobile Apps na platformie .NET projekt wewnętrznej bazy danych jest tylko aplikacji sieci web platformy ASP.NET z dodatkowe zestawu Mobile Apps SDK zainstalowany i zainicjować.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-183">In App Service, a Mobile Apps .NET backend project is just an ASP.NET web app with an additional Mobile Apps SDK installed and initialized.</span></span> <span data-ttu-id="2ab8e-184">Aby korzystać z aplikacji sieci web jako zaplecza aplikacji mobilnej, należy najpierw [pobierania i zainicjuj zaplecza Mobile Apps .NET SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span><span class="sxs-lookup"><span data-stu-id="2ab8e-184">To use your web app as a Mobile Apps backend, you must [download and initialize the Mobile Apps .NET backend SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#install-sdk).</span></span>  

<span data-ttu-id="2ab8e-185">Dla aplikacji mobilnych należy również określić parametry połączenia dla lokalnej bazy danych i modyfikować wewnętrznej bazy danych dla tego połączenia.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-185">For Mobile Apps, you also need to define a connection string for the on-premises database and modify the backend to use this connection.</span></span> 

1. <span data-ttu-id="2ab8e-186">W Eksploratorze rozwiązań w programie Visual Studio Otwórz plik Web.config dla zaplecza .NET aplikacji mobilnych, odszukaj **connectionStrings** Dodaj nowy wpis SqlClient podobnie do poniższego, która wskazuje na lokalną bazą danych programu SQL Server:</span><span class="sxs-lookup"><span data-stu-id="2ab8e-186">In Solution Explorer in Visual Studio, open the Web.config file for your Mobile App .NET backend, locate the **connectionStrings** section, add a new SqlClient entry like the following, which points to the on-premises SQL Server database:</span></span>
   
        <add name="OnPremisesDBConnection"
         connectionString="Data Source=OnPremisesServer,1433;
         Initial Catalog=OnPremisesDB;
         User ID=HybridConnectionLogin;
         Password=<**secure_password**>;
         MultipleActiveResultSets=True"
         providerName="System.Data.SqlClient" />
   
    <span data-ttu-id="2ab8e-187">Pamiętaj, aby zastąpić `<**secure_password**>` w tym ciągu z hasła utworzonego dla *HybridConnectionLogin*.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-187">Remember to replace `<**secure_password**>` in this string with the password you created for  *HybridConnectionLogin*.</span></span>
2. <span data-ttu-id="2ab8e-188">Kliknij przycisk **zapisać** w programie Visual Studio można zapisać pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-188">Click **Save** in Visual Studio to save the Web.config file.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="2ab8e-189">To ustawienie połączenia jest używany podczas uruchamiania komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-189">This connection setting is used when running on the local computer.</span></span> <span data-ttu-id="2ab8e-190">Podczas uruchamiania na platformie Azure, to ustawienie jest zastąpione przez ustawienie połączenia zdefiniowane w portalu.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-190">When running in Azure, this setting is overriden by the connection setting defined in the portal.</span></span>
   > 
   > 
3. <span data-ttu-id="2ab8e-191">Rozwiń węzeł **modele** folderu i Otwórz plik modelu danych kończy się *Context.cs*.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-191">Expand the **Models** folder and open the data model file, which ends in *Context.cs*.</span></span>
4. <span data-ttu-id="2ab8e-192">Modyfikowanie **DbContext** konstruktora wystąpienia, aby przekazać wartość `OnPremisesDBConnection` podstawy **DbContext** konstruktora, podobny do następującego fragmentu kodu:</span><span class="sxs-lookup"><span data-stu-id="2ab8e-192">Modify the **DbContext** instance constructor to pass the value `OnPremisesDBConnection` to the base **DbContext** constructor, similar to the following snippet:</span></span>
   
        public class hybridService1Context : DbContext
        {
            public hybridService1Context()
                : base("OnPremisesDBConnection")
            {
            }
        }
   
    <span data-ttu-id="2ab8e-193">Usługa będzie teraz używać nowego połączenia z bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-193">The service will now use the new connection to the SQL Server database.</span></span>

## <a name="update-the-mobile-app-backend-to-use-the-on-premises-connection-string"></a><span data-ttu-id="2ab8e-194">Zaktualizuj zaplecza aplikacji mobilnej do używania ciągu połączenia lokalnego</span><span class="sxs-lookup"><span data-stu-id="2ab8e-194">Update the Mobile App backend to use the on-premises connection string</span></span>
<span data-ttu-id="2ab8e-195">Następnie należy dodać ustawienie aplikacji dla tych nowych parametrów połączenia, dzięki czemu mogą być używane z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-195">Next, you need to add an app setting for this new connection string so that it can be used from Azure.</span></span>  

1. <span data-ttu-id="2ab8e-196">W [portalu Azure](https://portal.azure.com) w aplikacji mobilnej kodu zaplecza aplikacji sieci web kliknij **wszystkie ustawienia**, następnie **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-196">Back in the [Azure portal](https://portal.azure.com) in the web app backend code for your Mobile App, click **All settings**, then **Application settings**.</span></span>
2. <span data-ttu-id="2ab8e-197">W **ustawienia aplikacji w sieci Web** bloku, przewiń w dół do **parametry połączenia** i dodać nowe **programu SQL Server** parametrów połączenia o nazwie `OnPremisesDBConnection` o wartości podobnie jak `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-197">In the **Web app settings** blade, scroll down to **Connection strings** and add an new **SQL Server** connection string named `OnPremisesDBConnection` with a value like `Server=OnPremisesServer,1433;Database=OnPremisesDB;User ID=HybridConnectionsLogin;Password=<**secure_password**>`.</span></span>
   
    <span data-ttu-id="2ab8e-198">Zastąp `<**secure_password**>` z bezpiecznym hasłem lokalnej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-198">Replace `<**secure_password**>` with the secure password for your on-premises database.</span></span>
   
    ![Parametry połączenia dla lokalnej bazy danych](./media/web-sites-hybrid-connection-get-started/set-sql-server-database-connection.png)
3. <span data-ttu-id="2ab8e-200">Naciśnij klawisz **zapisać** zapisać hybrydowego połączenia i połączenia ciągu właśnie utworzony.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-200">Press **Save** to save the hybrid connection and connection string you just created.</span></span>

<span data-ttu-id="2ab8e-201">W tym momencie możesz ponownie opublikować projekt serwera i przetestować nowego połączenia z klientami istniejące aplikacje mobilne.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-201">At this point you can republish the server project and test the new connection with your existing Mobile Apps clients.</span></span> <span data-ttu-id="2ab8e-202">Dane będą odczytywane i zapisywane w lokalną bazą danych przy użyciu połączenia hybrydowego.</span><span class="sxs-lookup"><span data-stu-id="2ab8e-202">Data will be read from and written to the on-premises database using the hybrid connection.</span></span>

<a name="NextSteps"></a>

## <a name="next-steps"></a><span data-ttu-id="2ab8e-203">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2ab8e-203">Next Steps</span></span>
* <span data-ttu-id="2ab8e-204">Aby uzyskać informacje dotyczące tworzenia aplikacji sieci web ASP.NET, która używa połączenie hybrydowe, zobacz [Połącz z lokalnego serwera SQL z Azure witryny sieci web za pomocą połączeń hybrydowych](http://go.microsoft.com/fwlink/?LinkID=397979).</span><span class="sxs-lookup"><span data-stu-id="2ab8e-204">For information on creating an ASP.NET web application that uses a hybrid connection, see [Connect to an on-premises SQL Server from an Azure web site using Hybrid Connections](http://go.microsoft.com/fwlink/?LinkID=397979).</span></span> 

### <a name="additional-resources"></a><span data-ttu-id="2ab8e-205">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="2ab8e-205">Additional Resources</span></span>
[<span data-ttu-id="2ab8e-206">Omówienie połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="2ab8e-206">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="2ab8e-207">Dołączony Josha wprowadza połączeń hybrydowych (wideo z witryny Channel 9)</span><span class="sxs-lookup"><span data-stu-id="2ab8e-207">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="2ab8e-208">Witryna sieci web połączenia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="2ab8e-208">Hybrid Connections web site</span></span>](https://azure.microsoft.com/services/biztalk-services/)

[<span data-ttu-id="2ab8e-209">Usługi BizTalk Services: Karty Pulpit nawigacyjny, Monitor skali, konfigurowanie i połączenia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="2ab8e-209">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="2ab8e-210">Tworzenie hybrydowego rzeczywistych chmury chronionej za pomocą bezproblemowe przenośność aplikacji (Channel 9 wideo)</span><span class="sxs-lookup"><span data-stu-id="2ab8e-210">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="2ab8e-211">Nawiązywanie połączenia lokalnego serwera SQL z usług Azure Mobile Services za pomocą połączeń hybrydowych (wideo z witryny Channel 9)</span><span class="sxs-lookup"><span data-stu-id="2ab8e-211">Connect to an on-premises SQL Server from Azure Mobile Services using Hybrid Connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Series/Windows-Azure-Mobile-Services/Connect-to-an-on-premises-SQL-Server-from-Azure-Mobile-Services-using-Hybrid-Connections)

## <a name="whats-changed"></a><span data-ttu-id="2ab8e-212">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="2ab8e-212">What's changed</span></span>
* <span data-ttu-id="2ab8e-213">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="2ab8e-213">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

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
