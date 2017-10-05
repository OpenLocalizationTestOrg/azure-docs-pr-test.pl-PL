---
title: "Połączenie z lokalnym programem SQL Server z aplikacji sieci web w usłudze Azure App Service przy użyciu połączeń hybrydowych"
description: "Tworzenie aplikacji sieci web w systemie Microsoft Azure i połącz go z lokalną bazą danych programu SQL Server"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 2b4e0539-1a0b-4aa1-8a69-b4b053c3b2e5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2016
ms.author: cephalin
ms.openlocfilehash: 12456ef3e2aecfa7a03cca97de2ff6ffd9602357
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-on-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="6e494-103">Połączenie z lokalnym programem SQL Server z aplikacji sieci web w usłudze Azure App Service przy użyciu połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="6e494-103">Connect to on-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="6e494-104">Nawiązanie połączenia hybrydowe [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) aplikacji sieci Web z lokalnymi zasobami, które użycia portu statycznego TCP.</span><span class="sxs-lookup"><span data-stu-id="6e494-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps to on-premises resources that use a static TCP port.</span></span> <span data-ttu-id="6e494-105">Obsługiwane zasoby obejmują programu Microsoft SQL Server, MySQL, interfejsy API protokołu HTTP sieci Web, usługi aplikacji i większość niestandardowych usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6e494-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="6e494-106">Z tego samouczka, dowiesz sposób tworzenia aplikacji sieci web usługi aplikacji w [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), połączenia z bazą danych programu SQL Server lokalne lokalnymi, przy użyciu nowych funkcji hybrydowych połączenia aplikacji sieci web, utworzyć prostą aplikację ASP.NET do użycia przez połączenie hybrydowe, a wdrożenie aplikacji w aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e494-106">In this tutorial, you will learn how to create an App Service web app in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect the web app to your local on-premises SQL Server database using the new Hybrid Connection feature, create a simple ASP.NET application that will use the hybrid connection, and deploy the application to the App Service web app.</span></span> <span data-ttu-id="6e494-107">Aplikacja sieci web ukończone na platformie Azure przechowuje poświadczenia użytkownika w bazie danych członkostwa, które jest używane lokalne.</span><span class="sxs-lookup"><span data-stu-id="6e494-107">The completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="6e494-108">W samouczku założono nie wcześniejszego doświadczenia w używaniu platformy Azure lub programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6e494-108">The tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="6e494-109">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="6e494-109">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="6e494-110">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="6e494-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="6e494-111">Aplikacje sieci Web część funkcji połączeń hybrydowych było możliwe jest dostępna tylko w [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6e494-111">The Web Apps portion of the Hybrid Connections feature is available only in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="6e494-112">Aby utworzyć połączenie w usługi BizTalk Services, zobacz [połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="6e494-112">To create a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="6e494-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6e494-113">Prerequisites</span></span>
<span data-ttu-id="6e494-114">Do ukończenia tego samouczka należy następujące produkty.</span><span class="sxs-lookup"><span data-stu-id="6e494-114">To complete this tutorial, you'll need the following products.</span></span> <span data-ttu-id="6e494-115">Dostępne są wszystkie w bezpłatnej wersji, aby rozpocząć tworzenie aplikacji dla platformy Azure i całkowicie bezpłatne.</span><span class="sxs-lookup"><span data-stu-id="6e494-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="6e494-116">**Subskrypcja platformy Azure** — w przypadku bezpłatnej subskrypcji, zobacz [bezpłatnej wersji próbnej Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6e494-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="6e494-117">**Visual Studio 2013** — Aby pobrać bezpłatną wersję próbną programu Visual Studio 2013, zobacz [programu Visual Studio pobiera](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="6e494-117">**Visual Studio 2013** - To download a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="6e494-118">Zainstaluj to przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="6e494-118">Install this before continuing.</span></span>
* <span data-ttu-id="6e494-119">**Program Microsoft .NET Framework 3.5 z dodatkiem Service Pack 1** — w przypadku systemu operacyjnego Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 lub Windows Server 2008 R2, możesz je włączyć, w Panelu sterowania > programy i funkcje > Włącz lub wyłącz funkcje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="6e494-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="6e494-120">W przeciwnym razie możesz pobrać go z [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="6e494-120">Otherwise, you can download it from the [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="6e494-121">**SQL Server 2014 Express with Tools** — Microsoft SQL Server Express bezpłatnie pobrać na [strona bazy danych platformy sieci Web Microsoft](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e494-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at the [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="6e494-122">Wybierz **Express** (nie LocalDB) wersji.</span><span class="sxs-lookup"><span data-stu-id="6e494-122">Choose the **Express** (not LocalDB) version.</span></span> <span data-ttu-id="6e494-123">**Express with Tools** wersja obejmuje program SQL Server Management Studio, który będzie używany w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="6e494-123">The **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="6e494-124">**SQL Server Management Studio Express** — jest on dołączony do programu SQL Server 2014 Express pobierania narzędzia wymienionych powyżej, ale jeśli musisz zainstalować oddzielnie, można pobrać i zainstalować go z [strony pobierania programu SQL Server Express](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e494-124">**SQL Server Management Studio Express** - This is included with the SQL Server 2014 Express with Tools download mentioned above, but if you need to install it separately, you can download and install it from the [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="6e494-125">Samouczka przyjęto założenie, że masz subskrypcję platformy Azure, zainstalowanego programu Visual Studio 2013 i czy masz zainstalowany lub włączony program .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="6e494-125">The tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="6e494-126">Samouczek przedstawia sposób instalowania programu SQL Server 2014 Express w konfiguracji, które działa dobrze z funkcją Azure połączeń hybrydowych (domyślnego wystąpienia z portu statycznego TCP).</span><span class="sxs-lookup"><span data-stu-id="6e494-126">The tutorial shows you how to install SQL Server 2014 Express in a configuration that works well with the Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="6e494-127">Przed rozpoczęciem tego samouczka, Pobierz program SQL Server 2014 Express with Tools z lokalizacji wymienionych powyżej, jeśli nie masz zainstalowanego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6e494-127">Before starting the tutorial, download SQL Server 2014 Express with Tools from the location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="6e494-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6e494-128">Notes</span></span>
<span data-ttu-id="6e494-129">Aby użyć lokalnego programu SQL Server lub SQL Server Express bazy danych z połączenia hybrydowego, TCP/IP musi być włączona na portu statycznego.</span><span class="sxs-lookup"><span data-stu-id="6e494-129">To use an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs to be enabled on a static port.</span></span> <span data-ttu-id="6e494-130">Domyślne wystąpienia w programie SQL Server używać portu statycznego 1433, nazwanych wystąpień nie.</span><span class="sxs-lookup"><span data-stu-id="6e494-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="6e494-131">Komputer, na którym należy zainstalować agenta menedżera połączeń hybrydowych lokalnie:</span><span class="sxs-lookup"><span data-stu-id="6e494-131">The computer on which you install the on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="6e494-132">Musi mieć łączność wychodząca Azure za pośrednictwem:</span><span class="sxs-lookup"><span data-stu-id="6e494-132">Must have outbound connectivity to Azure over:</span></span>

| <span data-ttu-id="6e494-133">Port</span><span class="sxs-lookup"><span data-stu-id="6e494-133">Port</span></span> | <span data-ttu-id="6e494-134">Dlaczego</span><span class="sxs-lookup"><span data-stu-id="6e494-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="6e494-135">80</span><span class="sxs-lookup"><span data-stu-id="6e494-135">80</span></span> |<span data-ttu-id="6e494-136">**Wymagane** dla portu HTTP dla certyfikatu weryfikacji i opcjonalnie łączności danych.</span><span class="sxs-lookup"><span data-stu-id="6e494-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="6e494-137">443</span><span class="sxs-lookup"><span data-stu-id="6e494-137">443</span></span> |<span data-ttu-id="6e494-138">**Opcjonalne** połączeń danych.</span><span class="sxs-lookup"><span data-stu-id="6e494-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="6e494-139">Jeśli łączność wychodząca 443 jest niedostępna, jest używany TCP port 80.</span><span class="sxs-lookup"><span data-stu-id="6e494-139">If outbound connectivity to 443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="6e494-140">5671 i 9352</span><span class="sxs-lookup"><span data-stu-id="6e494-140">5671 and 9352</span></span> |<span data-ttu-id="6e494-141">**Zalecane** , ale opcjonalne dla połączenia danych.</span><span class="sxs-lookup"><span data-stu-id="6e494-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="6e494-142">Należy pamiętać, że w tym trybie zwykle zapewnia wyższą przepływność.</span><span class="sxs-lookup"><span data-stu-id="6e494-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="6e494-143">Jeśli łączność wychodząca tych portów jest niedostępna, jest używany TCP port 443.</span><span class="sxs-lookup"><span data-stu-id="6e494-143">If outbound connectivity to these ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="6e494-144">Musi być możliwe nawiązanie łączności *hostname*:*numer_portu* zasobu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="6e494-144">Must be able to reach the *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="6e494-145">Kroki opisane w tym artykule założono, że używasz przeglądarki z komputera, który będzie hostem agenta połączenia hybrydowego lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="6e494-145">The steps in this article assume that you are using the browser from the computer that will host the on-premises hybrid connection agent.</span></span>

<span data-ttu-id="6e494-146">Jeśli masz już programu SQL Server zainstalowanego w konfiguracji i w środowisku, które spełnia warunki opisane powyżej, możesz przejść od razu i rozpoczynać [Utwórz bazę danych programu SQL Server lokalne](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="6e494-146">If you already have SQL Server installed in a configuration and in an environment that meets the conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="6e494-147">A.</span><span class="sxs-lookup"><span data-stu-id="6e494-147">A.</span></span> <span data-ttu-id="6e494-148">Instalowanie programu SQL Server Express, Włącz protokół TCP/IP i utworzyć lokalnej bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="6e494-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="6e494-149">W tej sekcji przedstawiono sposób instalowania programu SQL Server Express, Włącz protokół TCP/IP i utworzyć bazę danych, aby działały aplikacji sieci web przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6e494-149">This section shows you how to install SQL Server Express, enable TCP/IP, and create a database so that your web application will work with the Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="6e494-150">Zainstaluj program SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="6e494-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="6e494-151">Aby zainstalować program SQL Server Express, uruchom **SQLEXPRWT_x64_ENU.exe** lub **SQLEXPR_x86_ENU.exe** pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="6e494-151">To install SQL Server Express, run the **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="6e494-152">Zostanie wyświetlony Kreator Centrum instalacji programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6e494-152">The SQL Server Installation Center wizard appears.</span></span>
   
    ![Instalacja serwera SQL][SQLServerInstall]
2. <span data-ttu-id="6e494-154">Wybierz **nowy serwer SQL instalacji autonomicznej lub Dodaj funkcje do istniejącej instalacji**.</span><span class="sxs-lookup"><span data-stu-id="6e494-154">Choose **New SQL Server stand-alone installation or add features to an existing installation**.</span></span> <span data-ttu-id="6e494-155">Postępuj zgodnie z instrukcjami, przyjmuje opcje domyślne i ustawienia, aż do **Konfiguracja wystąpienia** strony.</span><span class="sxs-lookup"><span data-stu-id="6e494-155">Follow the instructions, accepting the default choices and settings, until you get to the **Instance Configuration** page.</span></span>
3. <span data-ttu-id="6e494-156">Na **Konfiguracja wystąpienia** wybierz pozycję **domyślnego wystąpienia**.</span><span class="sxs-lookup"><span data-stu-id="6e494-156">On the **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Wybierz wystąpienie domyślne][ChooseDefaultInstance]
   
    <span data-ttu-id="6e494-158">Domyślnie domyślnego wystąpienia programu SQL Server nasłuchuje żądań od klientów programu SQL Server na statycznych porcie 1433, czyli wymaga funkcji połączeń hybrydowych było możliwe.</span><span class="sxs-lookup"><span data-stu-id="6e494-158">By default, the default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what the Hybrid Connections feature requires.</span></span> <span data-ttu-id="6e494-159">Nazwane wystąpienia używać portów dynamicznych i UDP, które nie są obsługiwane przez połączeń hybrydowych było możliwe.</span><span class="sxs-lookup"><span data-stu-id="6e494-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="6e494-160">Zaakceptuj wartości domyślne na **konfiguracji serwera** strony.</span><span class="sxs-lookup"><span data-stu-id="6e494-160">Accept the defaults on the **Server Configuration** page.</span></span>
5. <span data-ttu-id="6e494-161">Na **Konfiguracja aparatu bazy danych** w obszarze **tryb uwierzytelniania**, wybierz **trybu mieszanego (uwierzytelnianie programu SQL Server i uwierzytelniania systemu Windows)**i podaj hasło.</span><span class="sxs-lookup"><span data-stu-id="6e494-161">On the **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Wybierz tryb mieszany][ChooseMixedMode]
   
    <span data-ttu-id="6e494-163">W tym samouczku będziesz używać uwierzytelniania programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6e494-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="6e494-164">Należy zapamiętać hasło, które zostaną podane, ponieważ będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="6e494-164">Be sure to remember the password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="6e494-165">Kroków opisanych w pozostałej części kreatora w celu ukończenia instalacji.</span><span class="sxs-lookup"><span data-stu-id="6e494-165">Step through the rest of the wizard to complete the installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="6e494-166">Włącz protokół TCP/IP</span><span class="sxs-lookup"><span data-stu-id="6e494-166">Enable TCP/IP</span></span>
<span data-ttu-id="6e494-167">Aby włączyć protokół TCP/IP, używasz programu SQL Server Configuration Manager, który został zainstalowany przed zainstalowaniem programu SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="6e494-167">To enable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="6e494-168">Postępuj zgodnie z instrukcjami [Włącz protokół dla programu SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="6e494-168">Follow the steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="6e494-169">Utwórz bazę danych programu SQL Server lokalne</span><span class="sxs-lookup"><span data-stu-id="6e494-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="6e494-170">Aplikacja sieci web programu Visual Studio wymaga Azure można uzyskać dostępu do bazy danych członkostwa.</span><span class="sxs-lookup"><span data-stu-id="6e494-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="6e494-171">Wymaga to bazy danych programu SQL Server lub SQL Server Express (nie LocalDB bazy danych, która domyślnie używa szablonu MVC), więc następnie utworzysz bazie danych członkostwa.</span><span class="sxs-lookup"><span data-stu-id="6e494-171">This requires a SQL Server or SQL Server Express database (not the LocalDB database that the MVC template uses by default), so you'll create the membership database next.</span></span>

1. <span data-ttu-id="6e494-172">W programu SQL Server Management Studio nawiąż połączenie z programem SQL Server został właśnie zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="6e494-172">In SQL Server Management Studio, connect to the SQL Server you just installed.</span></span> <span data-ttu-id="6e494-173">(Jeśli **Połącz z serwerem** okna dialogowego nie zostanie wyświetlone automatycznie, przejdź do **Eksplorator obiektów** w okienku po lewej stronie kliknij **Connect**, a następnie kliknij przycisk **aparatu bazy danych**.) ![Połączyć się z serwerem][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="6e494-173">(If the **Connect to Server** dialog does not appear automatically, navigate to **Object Explorer** in the left pane, click **Connect**, and then click **Database Engine**.) ![Connect to Server][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="6e494-174">Aby uzyskać **typ serwera**, wybierz **aparatu bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="6e494-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="6e494-175">Aby uzyskać **nazwy serwera**, można użyć **localhost** lub nazwę komputera, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="6e494-175">For **Server name**, you can use **localhost** or the name of the computer that you are using.</span></span> <span data-ttu-id="6e494-176">Wybierz **uwierzytelniania programu SQL Server**, a następnie zaloguj się za pomocą nazwy użytkownika i hasła, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="6e494-176">Choose **SQL Server authentication**, and then log in with the sa user name and the password that you created earlier.</span></span>
2. <span data-ttu-id="6e494-177">Aby utworzyć nową bazę danych przy użyciu programu SQL Server Management Studio, kliknij prawym przyciskiem myszy **baz danych** w Eksploratorze obiektów, a następnie kliknij przycisk **nową bazę danych**.</span><span class="sxs-lookup"><span data-stu-id="6e494-177">To create a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Utwórz nową bazę danych][SSMScreateNewDB]
3. <span data-ttu-id="6e494-179">W **nową bazę danych** okna dialogowego, wprowadź MembershipDB dla nazwy bazy danych, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e494-179">In the **New Database** dialog, enter MembershipDB for the database name, and then click **OK**.</span></span>
   
    ![Podaj nazwę bazy danych][SSMSprovideDBname]
   
    <span data-ttu-id="6e494-181">Należy pamiętać, że użytkownik nie wprowadzaj żadnych zmian w bazie danych w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="6e494-181">Note that you do not make any changes to the database at this point.</span></span> <span data-ttu-id="6e494-182">Informacje o członkostwie zostaną automatycznie później dodane przez aplikację sieci web po jej uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="6e494-182">The membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="6e494-183">W Eksploratorze obiektów po rozwinięciu **baz danych**, zobaczysz, że utworzono bazy danych członkostwa.</span><span class="sxs-lookup"><span data-stu-id="6e494-183">In Object Explorer, if you expand **Databases**, you will see that the membership database has been created.</span></span>
   
    ![MembershipDB utworzone][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="6e494-185">B.</span><span class="sxs-lookup"><span data-stu-id="6e494-185">B.</span></span> <span data-ttu-id="6e494-186">Tworzenie aplikacji sieci web w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6e494-186">Create a web app in the Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="6e494-187">Jeśli utworzono już aplikacji sieci web w portalu Azure, który ma być używany na potrzeby tego samouczka, możesz przejść od razu do [Tworzenie połączenia hybrydowego i usługi BizTalk](#CreateHC) i kontynuować stamtąd.</span><span class="sxs-lookup"><span data-stu-id="6e494-187">If you have already created a web app in the Azure Portal that you want to use for this tutorial, you can skip ahead to [Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="6e494-188">W [Azure Portal](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="6e494-188">In the [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Przycisk Nowy][New]
2. <span data-ttu-id="6e494-190">Konfigurowanie aplikacji sieci web, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6e494-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Nazwa witryny sieci Web][WebsiteCreationBlade]
3. <span data-ttu-id="6e494-192">Po kilku chwilach aplikacji sieci web jest tworzona i pojawia się jego bloku aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="6e494-192">After a few moments, the web app is created and its web app blade appears.</span></span> <span data-ttu-id="6e494-193">Blok jest pionowo przewijanego pulpit nawigacyjny, który umożliwia zarządzanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6e494-193">The blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Witryny sieci Web uruchomionej][WebSiteRunningBlade]
   
    <span data-ttu-id="6e494-195">Aby potwierdzić, aplikacji sieci web na żywo, można kliknąć **Przeglądaj** ikonę, aby wyświetlić stronę domyślną.</span><span class="sxs-lookup"><span data-stu-id="6e494-195">To verify the web app is live, you can click the **Browse** icon to display the default page.</span></span>

<span data-ttu-id="6e494-196">Następnie utworzysz połączenie hybrydowe i usługa BizTalk aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="6e494-196">Next, you will create a hybrid connection and a BizTalk service for the web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="6e494-197">C.</span><span class="sxs-lookup"><span data-stu-id="6e494-197">C.</span></span> <span data-ttu-id="6e494-198">Tworzenie połączenia hybrydowego i usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="6e494-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="6e494-199">Wstecz w portalu, przejdź do ustawień i kliknij przycisk **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.</span><span class="sxs-lookup"><span data-stu-id="6e494-199">Back in the Portal, go to settings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Połączenia hybrydowe][CreateHCHCIcon]
2. <span data-ttu-id="6e494-201">W bloku połączeń hybrydowych, kliknij **Dodaj** > **nowe połączenie hybrydowe**.</span><span class="sxs-lookup"><span data-stu-id="6e494-201">On the Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="6e494-202">Na **Tworzenie połączenia hybrydowego** bloku:</span><span class="sxs-lookup"><span data-stu-id="6e494-202">On the **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="6e494-203">Aby uzyskać **nazwa**, podaj nazwę dla połączenia.</span><span class="sxs-lookup"><span data-stu-id="6e494-203">For **Name**, provide a name for the connection.</span></span>
   * <span data-ttu-id="6e494-204">Aby uzyskać **Hostname**, wpisz nazwę komputera komputera-hosta programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6e494-204">For **Hostname**, enter the computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="6e494-205">Aby uzyskać **portu**, wprowadź 1433 (port domyślny dla programu SQL Server).</span><span class="sxs-lookup"><span data-stu-id="6e494-205">For **Port**, enter 1433 (the default port for SQL Server).</span></span>
   * <span data-ttu-id="6e494-206">Kliknij przycisk **usługi BizTalk** > **nową usługę BizTalk** , a następnie wprowadź nazwę usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="6e494-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for the BizTalk service.</span></span>
     
     ![Tworzenie połączenia hybrydowego][TwinCreateHCBlades]
4. <span data-ttu-id="6e494-208">Kliknij przycisk **OK** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="6e494-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="6e494-209">Po zakończeniu tego procesu, **powiadomienia** obszaru będzie flash zielona **Powodzenie** i **połączenia hybrydowego** bloku zostaną wyświetlone nowe połączenie hybrydowe o stanie jako **niepołączone**.</span><span class="sxs-lookup"><span data-stu-id="6e494-209">When the process completes, the **Notifications** area will flash a green **SUCCESS** and the **Hybrid connection** blade will show the new hybrid connection with the status as **Not connected**.</span></span>
   
    ![Połączenia hybrydowe jeden utworzone][CreateHCOneConnectionCreated]

<span data-ttu-id="6e494-211">W tym momencie została ukończona ważnym elementem infrastruktury połączenia hybrydowe w chmurze.</span><span class="sxs-lookup"><span data-stu-id="6e494-211">At this point, you have completed an important part of the cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="6e494-212">Następnie utworzy odpowiedni element lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="6e494-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-the-on-premises-hybrid-connection-manager-to-complete-the-connection"></a><span data-ttu-id="6e494-213">D.</span><span class="sxs-lookup"><span data-stu-id="6e494-213">D.</span></span> <span data-ttu-id="6e494-214">Zainstaluj Menedżera połączeń hybrydowych lokalnego, aby nawiązać połączenie</span><span class="sxs-lookup"><span data-stu-id="6e494-214">Install the on-premises Hybrid Connection Manager to complete the connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="6e494-215">Teraz, infrastruktura hybrydowa połączenie zostanie zakończone, spowoduje utworzenie aplikacji sieci web, która korzysta z niego.</span><span class="sxs-lookup"><span data-stu-id="6e494-215">Now that the hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-the-database-connection-string-and-run-the-project-locally"></a><span data-ttu-id="6e494-216">E.</span><span class="sxs-lookup"><span data-stu-id="6e494-216">E.</span></span> <span data-ttu-id="6e494-217">Tworzenie podstawowego projektu sieci web programu ASP.NET, Edytuj parametry połączenia bazy danych i uruchamianie projektu lokalnie</span><span class="sxs-lookup"><span data-stu-id="6e494-217">Create a basic ASP.NET web project, edit the database connection string, and run the project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="6e494-218">Tworzenie podstawowego projektu programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6e494-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="6e494-219">W programie Visual Studio na **pliku** menu, Utwórz nowy projekt:</span><span class="sxs-lookup"><span data-stu-id="6e494-219">In Visual Studio, on the **File** menu, create a new Project:</span></span>
   
    ![Nowy projekt programu Visual Studio][HCVSNewProject]
2. <span data-ttu-id="6e494-221">W **szablony** sekcji **nowy projekt** okno dialogowe, wybierz opcję **sieci Web** i wybierz polecenie **aplikacji sieci Web ASP.NET**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e494-221">In the **Templates** section of the **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Wybierz aplikację sieci Web ASP.NET][HCVSChooseASPNET]
3. <span data-ttu-id="6e494-223">W **nowy projekt ASP.NET** okno dialogowe, wybierz **MVC**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e494-223">In the **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Wybierz MVC][HCVSChooseMVC]
4. <span data-ttu-id="6e494-225">Po utworzeniu projektu, zostanie wyświetlona strona readme aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e494-225">When the project has been created, the application readme page appears.</span></span> <span data-ttu-id="6e494-226">Nie należy jeszcze uruchamiać projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="6e494-226">Do not run the web project yet.</span></span>
   
    ![Stronę Readme][HCVSReadmePage]

### <a name="edit-the-database-connection-string-for-the-application"></a><span data-ttu-id="6e494-228">Edytuj parametry połączenia bazy danych dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="6e494-228">Edit the database connection string for the application</span></span>
<span data-ttu-id="6e494-229">W tym kroku możesz edytować parametry połączenia, które informuje aplikacji, gdzie można znaleźć lokalnej bazy danych programu SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="6e494-229">In this step, you edit the connection string that tells your application where to find your local SQL Server Express database.</span></span> <span data-ttu-id="6e494-230">Parametry połączenia są w pliku Web.config aplikacji, który zawiera informacje o konfiguracji dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e494-230">The connection string is in the application's Web.config file, which contains configuration information for the application.</span></span>

> [!NOTE]
> <span data-ttu-id="6e494-231">Aby upewnić się, że aplikacja korzysta z bazy danych utworzonej w programu SQL Server Express, a nie do domyślnej programu Visual Studio LocalDB, ważne jest ukończenia tego kroku przed uruchomieniem projektu.</span><span class="sxs-lookup"><span data-stu-id="6e494-231">To ensure that your application uses the database that you created in SQL Server Express, and not the one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="6e494-232">W Eksploratorze rozwiązań kliknij dwukrotnie plik Web.config.</span><span class="sxs-lookup"><span data-stu-id="6e494-232">In Solution Explorer, double-click the Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="6e494-234">Edytuj **connectionStrings** sekcji, aby wskazywał bazy danych programu SQL Server na komputerze lokalnym, składni w następującym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="6e494-234">Edit the **connectionStrings** section to point to the SQL Server database on your local machine, following the syntax in the following example:</span></span>
   
    ![Parametry połączenia][HCVSConnectionString]
   
    <span data-ttu-id="6e494-236">Podczas tworzenia ciągu połączenia, należy pamiętać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6e494-236">When composing the connection string, keep in mind the following:</span></span>
   
   * <span data-ttu-id="6e494-237">Jeśli łączysz się z wystąpieniem nazwanym, a wystąpienia domyślnego (na przykład YourServer\SQLEXPRESS), należy skonfigurować program SQL Server do korzystania z portów statycznych.</span><span class="sxs-lookup"><span data-stu-id="6e494-237">If you are connecting to a named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server to use static ports.</span></span> <span data-ttu-id="6e494-238">Informacje dotyczące konfigurowania portów statycznych, zobacz [sposób konfigurowania programu SQL Server do nasłuchiwania na konkretnym porcie](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="6e494-238">For information on configuring static ports, see [How to configure SQL Server to listen on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="6e494-239">Domyślnie nazwane wystąpienia używają protokołów UDP i porty dynamiczne, które nie są obsługiwane przez połączeń hybrydowych było możliwe.</span><span class="sxs-lookup"><span data-stu-id="6e494-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="6e494-240">Zalecane jest, aby określić port (1433 domyślnie, jak pokazano w przykładzie) w parametrach połączenia, dzięki czemu użytkownik może upewnij się, że lokalny serwer SQL został włączony protokół TCP i używa poprawnego portu.</span><span class="sxs-lookup"><span data-stu-id="6e494-240">It is recommended that you specify the port (1433 by default, as shown in the example) on the connection string so that you can be sure that your local SQL Server has TCP enabled and is using the correct port.</span></span>
   * <span data-ttu-id="6e494-241">Pamiętaj, aby używać uwierzytelniania programu SQL Server do połączenia, określenie Identyfikatora użytkownika i hasła w ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="6e494-241">Remember to use SQL Server Authentication to connect, specifying the user ID and password in your connection string.</span></span>
3. <span data-ttu-id="6e494-242">Kliknij przycisk **zapisać** w programie Visual Studio można zapisać pliku Web.config.</span><span class="sxs-lookup"><span data-stu-id="6e494-242">Click **Save** in Visual Studio to save the Web.config file.</span></span>

### <a name="run-the-project-locally-and-register-a-new-user"></a><span data-ttu-id="6e494-243">Uruchamianie projektu lokalnie i zarejestrować nowego użytkownika</span><span class="sxs-lookup"><span data-stu-id="6e494-243">Run the project locally and register a new user</span></span>
1. <span data-ttu-id="6e494-244">Teraz Uruchom nowego projektu sieci web lokalnie, klikając przycisk przeglądania w obszarze debugowania.</span><span class="sxs-lookup"><span data-stu-id="6e494-244">Now, run your new web project locally by clicking the browse button under Debug.</span></span> <span data-ttu-id="6e494-245">W tym przykładzie użyto programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="6e494-245">This example uses Internet Explorer.</span></span>
   
    ![Uruchom projekt][HCVSRunProject]
2. <span data-ttu-id="6e494-247">W prawym górnym rogu domyślnej strony sieci web, wybierz polecenie **zarejestrować** zarejestrować nowe konto:</span><span class="sxs-lookup"><span data-stu-id="6e494-247">On the upper right of the default web page, choose **Register** to register a new account:</span></span>
   
    ![Zarejestruj nowe konto][HCVSRegisterLocally]
3. <span data-ttu-id="6e494-249">Wprowadź nazwę użytkownika i hasło:</span><span class="sxs-lookup"><span data-stu-id="6e494-249">Enter a user name and password:</span></span>
   
    ![Wprowadź nazwę użytkownika i hasło][HCVSCreateNewAccount]
   
    <span data-ttu-id="6e494-251">Powoduje to automatyczne utworzenie bazy danych na serwerze SQL lokalnej, która przechowuje informacje o członkostwie dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6e494-251">This automatically creates a database on your local SQL Server that holds the membership information for your application.</span></span> <span data-ttu-id="6e494-252">Jedną z tabel (**dbo. AspNetUsers**) blokad sieci web poświadczenia użytkownika aplikacji, takich jak te, które zostały wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="6e494-252">One of the tables (**dbo.AspNetUsers**) holds web app user credentials like the ones that you just entered.</span></span> <span data-ttu-id="6e494-253">Zobaczysz tej tabeli później w samouczku.</span><span class="sxs-lookup"><span data-stu-id="6e494-253">You will see this table later in the tutorial.</span></span>
4. <span data-ttu-id="6e494-254">Zamknij okno przeglądarki domyślnej strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="6e494-254">Close the browser window of the default web page.</span></span> <span data-ttu-id="6e494-255">Powoduje to zatrzymanie aplikacji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e494-255">This stops the application in Visual Studio.</span></span>

<span data-ttu-id="6e494-256">Teraz można przystąpić do następnego kroku, która umożliwia publikowanie aplikacji na platformie Azure i przetestować go.</span><span class="sxs-lookup"><span data-stu-id="6e494-256">You are now ready for the next step, which is to publish the application to Azure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-the-web-application-to-azure-and-test-it"></a><span data-ttu-id="6e494-257">F.</span><span class="sxs-lookup"><span data-stu-id="6e494-257">F.</span></span> <span data-ttu-id="6e494-258">Publikowanie aplikacji sieci web na platformie Azure i przetestować go</span><span class="sxs-lookup"><span data-stu-id="6e494-258">Publish the web application to Azure and test it</span></span>
<span data-ttu-id="6e494-259">Teraz będziesz opublikować aplikację do aplikacji sieci web usługi aplikacji, a następnie sprawdź go, aby sprawdzić, jak jest używane przez skonfigurowane wcześniej połączenie hybrydowe także łączenie aplikacji sieci web do bazy danych na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="6e494-259">Now, you'll publish your application to your App Service web app and then test it to see how the hybrid connection you configured earlier is being used to connect your web app to the database on your local machine.</span></span>

### <a name="publish-the-web-application"></a><span data-ttu-id="6e494-260">Publikowanie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="6e494-260">Publish the web application</span></span>
1. <span data-ttu-id="6e494-261">Można pobrać profilu publikowania dla aplikacji sieci web usługi aplikacji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6e494-261">You can download your publishing profile for the App Service web app in the Azure Portal.</span></span> <span data-ttu-id="6e494-262">W bloku aplikacja sieci web, kliknij przycisk **profilu publikowania Get**, a następnie zapisz plik na komputerze.</span><span class="sxs-lookup"><span data-stu-id="6e494-262">On the blade for your web app, click **Get publish profile**, and then save the file to your computer.</span></span>
   
    ![Pobieranie profilu publikowania][PortalDownloadPublishProfile]
   
    <span data-ttu-id="6e494-264">Zostanie następnie zaimportować ten plik do aplikacji sieci web programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e494-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="6e494-265">W programie Visual Studio, kliknij prawym przyciskiem myszy nazwę projektu w Eksploratorze rozwiązań i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="6e494-265">In Visual Studio, right-click the project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Wybierz publikowania][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="6e494-267">W **publikowanie w sieci Web** okna dialogowego na **profilu** , wybierz pozycję **importu**.</span><span class="sxs-lookup"><span data-stu-id="6e494-267">In the **Publish Web** dialog, on the **Profile** tab, choose **Import**.</span></span>
   
    ![Import][HCVSPublishWebDialogImport]
4. <span data-ttu-id="6e494-269">Przejdź do pobrany profil publikowania, zaznacz go, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e494-269">Browse to your downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Przejdź do profilu][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="6e494-271">Publikowanie informacji jest importowany i wyświetla na **połączenia** karcie okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6e494-271">Your publishing information is imported and displays on the **Connection** tab of the dialog.</span></span>
   
    ![Kliknij przycisk Publikuj][HCVSClickPublish]
   
    <span data-ttu-id="6e494-273">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="6e494-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="6e494-274">Po ukończeniu publikowania przeglądarki będzie uruchomić i pokazać teraz znanych aplikacji ASP.NET--z tą różnicą, że jest teraz na żywo w chmurze Azure!</span><span class="sxs-lookup"><span data-stu-id="6e494-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in the Azure cloud!</span></span>

<span data-ttu-id="6e494-275">Następnie użyje aplikacji sieci web na żywo aby zobaczyć jego połączenia hybrydowego, w akcji.</span><span class="sxs-lookup"><span data-stu-id="6e494-275">Next, you will use your live web application to see its Hybrid Connection in action.</span></span>

### <a name="test-the-completed-web-application-on-azure"></a><span data-ttu-id="6e494-276">Testowanie ukończonej aplikacji sieci web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6e494-276">Test the completed web application on Azure</span></span>
1. <span data-ttu-id="6e494-277">U góry po prawej stronie sieci web na platformie Azure, wybierz **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="6e494-277">On the top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Dziennik testu w][HCTestLogIn]
2. <span data-ttu-id="6e494-279">Aplikacja sieci web usługi aplikacji jest teraz połączenie bazy danych członkostwa aplikacji sieci web na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="6e494-279">Your App Service web app is now connected to your web application's membership database on your local machine.</span></span> <span data-ttu-id="6e494-280">Aby to sprawdzić, zaloguj się za pomocą tych samych poświadczeń, które wcześniej wprowadzony w lokalnej bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6e494-280">To verify this, log in with the same credentials that you entered in the local database earlier.</span></span>
   
    ![Witaj pozdrowienia][HCTestHelloContoso]
3. <span data-ttu-id="6e494-282">Dodatkowo sprawdź nowe połączenie hybrydowe, wylogować się z aplikacji sieci web platformy Azure i Zarejestruj się jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="6e494-282">To further test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="6e494-283">Podaj nową nazwę użytkownika i hasło, a następnie kliknij przycisk **zarejestrować**.</span><span class="sxs-lookup"><span data-stu-id="6e494-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test zarejestrować innego użytkownika][HCTestRegisterRelecloud]
4. <span data-ttu-id="6e494-285">Aby zweryfikować, że poświadczenia nowego użytkownika były przechowywane w lokalnej bazie danych za pośrednictwem połączenia hybrydowe, Otwórz program SQL Management Studio na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="6e494-285">To verify that the new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="6e494-286">W Eksploratorze obiektów rozwiń **MembershipDB** bazy danych, a następnie rozwiń **tabel**.</span><span class="sxs-lookup"><span data-stu-id="6e494-286">In Object Explorer, expand the **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="6e494-287">Kliknij prawym przyciskiem myszy **dbo. AspNetUsers** członkostwa tabeli i wybierz polecenie **zaznacz 1000 pierwszych wierszy** , aby wyświetlić wyniki.</span><span class="sxs-lookup"><span data-stu-id="6e494-287">Right-click the **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** to view the results.</span></span>
   
    ![Wyświetlenie wyników][HCTestSSMSTree]
5. <span data-ttu-id="6e494-289">Członkostwo w lokalnej tabeli teraz zawiera oba konta — ten, który został utworzony lokalnie, a ten, który został utworzony w chmurze Azure.</span><span class="sxs-lookup"><span data-stu-id="6e494-289">Your local membership table now shows both accounts - the one that you created locally, and the one that you created in the Azure cloud.</span></span> <span data-ttu-id="6e494-290">Ten, który został utworzony w chmurze zostały zapisane w lokalnej bazie danych za pomocą funkcji połączenie hybrydowe platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6e494-290">The one that you created in the cloud has been saved to your on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Zarejestrowani użytkownicy w lokalnej bazie danych][HCTestShowMemberDb]

<span data-ttu-id="6e494-292">Możesz teraz utworzeniu i wdrożeniu aplikacji sieci web ASP.NET, która używa połączenie hybrydowe między aplikacji sieci web w chmurze platformy Azure i lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6e494-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in the Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="6e494-293">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="6e494-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="6e494-294">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6e494-294">See Also</span></span>
[<span data-ttu-id="6e494-295">Omówienie połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="6e494-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="6e494-296">Dołączony Josha wprowadza połączeń hybrydowych (wideo z witryny Channel 9)</span><span class="sxs-lookup"><span data-stu-id="6e494-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="6e494-297">Omówienie połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="6e494-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="6e494-298">Usługi BizTalk Services: Karty Pulpit nawigacyjny, Monitor skali, konfigurowanie i połączenia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="6e494-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="6e494-299">Tworzenie hybrydowego rzeczywistych chmury chronionej za pomocą bezproblemowe przenośność aplikacji (Channel 9 wideo)</span><span class="sxs-lookup"><span data-stu-id="6e494-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="6e494-300">Dostęp do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6e494-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="6e494-301">Tożsamość platformy ASP.NET — omówienie</span><span class="sxs-lookup"><span data-stu-id="6e494-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

<!-- IMAGES -->
[SQLServerInstall]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A01SQLServerInstall.png
[ChooseDefaultInstance]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A02ChooseDefaultInstance.png
[ChooseMixedMode]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A03ChooseMixedMode.png
[SSMSConnectToServer]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A04SSMSConnectToServer.png
[SSMScreateNewDB]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A05SSMScreateNewDBlh.png
[SSMSprovideDBname]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A06SSMSprovideDBname.png
[SSMSMembershipDBCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/A07SSMSMembershipDBCreated.png
[New]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B01New.png
[NewWebsite]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B02NewWebsite.png
[WebsiteCreationBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B03WebsiteCreationBlade.png
[WebSiteRunningBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B04WebSiteRunningBlade.png
[Browse]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B05Browse.png
[DefaultWebSitePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/B06DefaultWebSitePage.png
[CreateHCHCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C01CreateHCHCIcon.png
[CreateHCAddHC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C02CreateHCAddHC.png
[TwinCreateHCBlades]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C03TwinCreateHCBlades.png
[CreateHCCreateBTS]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C04CreateHCCreateBTS.png
[CreateBTScomplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C05CreateBTScomplete.png
[CreateHCSuccessNotification]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C06CreateHCSuccessNotification.png
[CreateHCOneConnectionCreated]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/C07CreateHCOneConnectionCreated.png
[HCIcon]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D01HCIcon.png
[NotConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D02NotConnected.png
[NotConnectedBlade]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D03NotConnectedBlade.png
[ClickListenerSetup]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D04ClickListenerSetup.png
[ClickToInstallHCM]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D05ClickToInstallHCM.png
[ApplicationRunWarning]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D06ApplicationRunWarning.png
[UAC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D07UAC.png
[HCMInstalling]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D08HCMInstalling.png
[HCMInstallComplete]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D09HCMInstallComplete.png
[HCStatusConnected]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/D10HCStatusConnected.png
[HCVSNewProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E01HCVSNewProject.png
[HCVSChooseASPNET]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E02HCVSChooseASPNET.png
[HCVSChooseMVC]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E03HCVSChooseMVC.png
[HCVSReadmePage]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E04HCVSReadmePage.png
[HCVSChooseWebConfig]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E05HCVSChooseWebConfig.png
[HCVSConnectionString]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSConnectionString.png
[HCVSRunProject]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E06HCVSRunProject.png
[HCVSRegisterLocally]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E07HCVSRegisterLocally.png
[HCVSCreateNewAccount]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/E08HCVSCreateNewAccount.png
[PortalDownloadPublishProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F01PortalDownloadPublishProfile.png
[HCVSPublishProfileInDownloadsFolder]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F02HCVSPublishProfileInDownloadsFolder.png
[HCVSRightClickProjectSelectPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F03HCVSRightClickProjectSelectPublish.png
[HCVSPublishWebDialogImport]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F04HCVSPublishWebDialogImport.png
[HCVSBrowseToImportPubProfile]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F05HCVSBrowseToImportPubProfile.png
[HCVSClickPublish]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F06HCVSClickPublish.png
[HCTestLogIn]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F07HCTestLogIn.png
[HCTestHelloContoso]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F08HCTestHelloContoso.png
[HCTestRegisterRelecloud]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F09HCTestRegisterRelecloud.png
[HCTestSSMSTree]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F10HCTestSSMSTree.png
[HCTestShowMemberDb]:./media/web-sites-hybrid-connection-connect-on-premises-sql-server/F11HCTestShowMemberDb.png
