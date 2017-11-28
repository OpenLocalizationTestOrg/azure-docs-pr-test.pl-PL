---
title: "aaaConnect tooon lokalnego programu SQL Server z aplikacji sieci web w usłudze Azure App Service przy użyciu połączeń hybrydowych"
description: "Tworzenie aplikacji sieci web w systemie Microsoft Azure i podłącz go tooan lokalną bazą danych programu SQL Server"
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
ms.openlocfilehash: 2e8f8f7e0b9733cfb0433697615faba4358c6023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooon-premises-sql-server-from-a-web-app-in-azure-app-service-using-hybrid-connections"></a><span data-ttu-id="9096c-103">Nawiązywanie połączenia lokalnego tooon programu SQL Server z aplikacji sieci web w usłudze Azure App Service przy użyciu połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="9096c-103">Connect tooon-premises SQL Server from a web app in Azure App Service using Hybrid Connections</span></span>
<span data-ttu-id="9096c-104">Nawiązanie połączenia hybrydowe [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) zasobów tooon lokalnych aplikacji sieci Web, które użycia portu statycznego TCP.</span><span class="sxs-lookup"><span data-stu-id="9096c-104">Hybrid Connections can connect [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps tooon-premises resources that use a static TCP port.</span></span> <span data-ttu-id="9096c-105">Obsługiwane zasoby obejmują programu Microsoft SQL Server, MySQL, interfejsy API protokołu HTTP sieci Web, usługi aplikacji i większość niestandardowych usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="9096c-105">Supported resources include Microsoft SQL Server, MySQL, HTTP Web APIs, App Service, and most custom Web Services.</span></span>

<span data-ttu-id="9096c-106">Z tego samouczka, dowiesz się, jak toocreate usługę aplikacji sieci web aplikacji w hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715)Połącz z hello sieci web aplikacji tooyour lokalnego lokalnej bazy danych SQL Server przy użyciu nowej funkcji połączenia hybrydowego hello, Utwórz prosty program ASP.NET Aplikacja, która będzie używać połączenia hybrydowego hello i wdróż toohello aplikacji hello aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9096c-106">In this tutorial, you will learn how toocreate an App Service web app in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), connect hello web app tooyour local on-premises SQL Server database using hello new Hybrid Connection feature, create a simple ASP.NET application that will use hello hybrid connection, and deploy hello application toohello App Service web app.</span></span> <span data-ttu-id="9096c-107">ukończyć powitalnych aplikacji sieci web na platformie Azure są przechowywane poświadczenia użytkownika w bazie danych członkostwa, które jest używane lokalne.</span><span class="sxs-lookup"><span data-stu-id="9096c-107">hello completed web app on Azure stores user credentials in a membership database that is on-premises.</span></span> <span data-ttu-id="9096c-108">Witaj samouczek zakłada nie wcześniejszego doświadczenia w używaniu platformy Azure lub programu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9096c-108">hello tutorial assumes no prior experience using Azure or ASP.NET.</span></span>

> [!NOTE]
> <span data-ttu-id="9096c-109">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="9096c-109">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="9096c-110">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="9096c-110">No credit cards required; no commitments.</span></span>
> 
> <span data-ttu-id="9096c-111">Witaj aplikacje sieci Web część funkcji połączeń hybrydowych hello jest dostępna tylko w hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9096c-111">hello Web Apps portion of hello Hybrid Connections feature is available only in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="9096c-112">Zobacz toocreate połączenie usługi BizTalk Services [połączeń hybrydowych](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span><span class="sxs-lookup"><span data-stu-id="9096c-112">toocreate a connection in BizTalk Services, see [Hybrid Connections](http://go.microsoft.com/fwlink/p/?LinkID=397274).</span></span>  
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9096c-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9096c-113">Prerequisites</span></span>
<span data-ttu-id="9096c-114">toocomplete tego samouczka będziesz potrzebować hello następujące produkty.</span><span class="sxs-lookup"><span data-stu-id="9096c-114">toocomplete this tutorial, you'll need hello following products.</span></span> <span data-ttu-id="9096c-115">Dostępne są wszystkie w bezpłatnej wersji, aby rozpocząć tworzenie aplikacji dla platformy Azure i całkowicie bezpłatne.</span><span class="sxs-lookup"><span data-stu-id="9096c-115">All are available in free versions, so you can start developing for Azure entirely for free.</span></span>

* <span data-ttu-id="9096c-116">**Subskrypcja platformy Azure** — w przypadku bezpłatnej subskrypcji, zobacz [bezpłatnej wersji próbnej Azure](/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9096c-116">**Azure subscription** - For a free subscription, see [Azure Free Trial](/pricing/free-trial/).</span></span>
* <span data-ttu-id="9096c-117">**Visual Studio 2013** -toodownload bezpłatną wersję próbną programu Visual Studio 2013, zobacz [programu Visual Studio pobiera](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span><span class="sxs-lookup"><span data-stu-id="9096c-117">**Visual Studio 2013** - toodownload a free trial version of Visual Studio 2013, see [Visual Studio Downloads](http://www.visualstudio.com/downloads/download-visual-studio-vs).</span></span> <span data-ttu-id="9096c-118">Zainstaluj to przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="9096c-118">Install this before continuing.</span></span>
* <span data-ttu-id="9096c-119">**Program Microsoft .NET Framework 3.5 z dodatkiem Service Pack 1** — w przypadku systemu operacyjnego Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7 lub Windows Server 2008 R2, możesz je włączyć, w Panelu sterowania > programy i funkcje > Włącz lub wyłącz funkcje systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="9096c-119">**Microsoft .NET Framework 3.5 Service Pack 1** - If your operating system is Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows 7, or Windows Server 2008 R2, you can enable this in Control Panel > Programs and Features > Turn Windows features on or off.</span></span> <span data-ttu-id="9096c-120">W przeciwnym razie można go pobrać z hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span><span class="sxs-lookup"><span data-stu-id="9096c-120">Otherwise, you can download it from hello [Microsoft Download Center](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=22).</span></span>
* <span data-ttu-id="9096c-121">**SQL Server 2014 Express with Tools** — Microsoft SQL Server Express bezpłatnie pobrać na powitania [strona bazy danych platformy sieci Web Microsoft](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="9096c-121">**SQL Server 2014 Express with Tools** - download Microsoft SQL Server Express for free at hello [Microsoft Web Platform Database page](http://www.microsoft.com/web/platform/database.aspx).</span></span> <span data-ttu-id="9096c-122">Wybierz hello **Express** (nie LocalDB) wersji.</span><span class="sxs-lookup"><span data-stu-id="9096c-122">Choose hello **Express** (not LocalDB) version.</span></span> <span data-ttu-id="9096c-123">Witaj **Express with Tools** wersja obejmuje program SQL Server Management Studio, który będzie używany w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="9096c-123">hello **Express with Tools** version includes SQL Server Management Studio, which you will use in this tutorial.</span></span>
* <span data-ttu-id="9096c-124">**SQL Server Management Studio Express** — jest on dołączony do programu SQL Server 2014 Express hello pobierania narzędzia wymienionych powyżej, ale jeśli potrzebujesz tooinstall go oddzielnie, można pobrać i zainstalować go z hello [programu SQL Server Express strona pobierania](http://www.microsoft.com/web/platform/database.aspx).</span><span class="sxs-lookup"><span data-stu-id="9096c-124">**SQL Server Management Studio Express** - This is included with hello SQL Server 2014 Express with Tools download mentioned above, but if you need tooinstall it separately, you can download and install it from hello [SQL Server Express download page](http://www.microsoft.com/web/platform/database.aspx).</span></span>

<span data-ttu-id="9096c-125">Hello samouczku założono, że masz subskrypcję platformy Azure, zainstalowanego programu Visual Studio 2013 i czy masz zainstalowany lub włączony program .NET Framework 3.5.</span><span class="sxs-lookup"><span data-stu-id="9096c-125">hello tutorial assumes that you have an Azure subscription, that you have installed Visual Studio 2013, and that you have installed or enabled .NET Framework 3.5.</span></span> <span data-ttu-id="9096c-126">Witaj samouczek pokazuje, jak tooinstall programu SQL Server 2014 Express w konfiguracji, które działa dobrze w przypadku połączeń hybrydowych hello Azure funkcji (domyślnego wystąpienia z portu statycznego TCP).</span><span class="sxs-lookup"><span data-stu-id="9096c-126">hello tutorial shows you how tooinstall SQL Server 2014 Express in a configuration that works well with hello Azure Hybrid Connections feature (a default instance with a static TCP port).</span></span> <span data-ttu-id="9096c-127">Przed rozpoczęciem samouczka hello, Pobierz program SQL Server 2014 Express with Tools z lokalizacji hello wymienione powyżej, jeśli nie masz zainstalowanego programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9096c-127">Before starting hello tutorial, download SQL Server 2014 Express with Tools from hello location mentioned above if you do not have SQL Server installed.</span></span>

### <a name="notes"></a><span data-ttu-id="9096c-128">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9096c-128">Notes</span></span>
<span data-ttu-id="9096c-129">toouse lokalnego programu SQL Server lub SQL Server Express bazy danych z połączenia hybrydowego TCP/IP musi toobe włączone portu statycznego.</span><span class="sxs-lookup"><span data-stu-id="9096c-129">toouse an on-premises SQL Server or SQL Server Express database with a hybrid connection, TCP/IP needs toobe enabled on a static port.</span></span> <span data-ttu-id="9096c-130">Domyślne wystąpienia w programie SQL Server używać portu statycznego 1433, nazwanych wystąpień nie.</span><span class="sxs-lookup"><span data-stu-id="9096c-130">Default instances on SQL Server use static port 1433, whereas named instances do not.</span></span>

<span data-ttu-id="9096c-131">Hello komputera, na którym należy zainstalować agenta menedżera połączeń hybrydowych lokalne powitania:</span><span class="sxs-lookup"><span data-stu-id="9096c-131">hello computer on which you install hello on-premises Hybrid Connection Manager agent:</span></span>

* <span data-ttu-id="9096c-132">Musi mieć łączność wychodząca tooAzure przez:</span><span class="sxs-lookup"><span data-stu-id="9096c-132">Must have outbound connectivity tooAzure over:</span></span>

| <span data-ttu-id="9096c-133">Port</span><span class="sxs-lookup"><span data-stu-id="9096c-133">Port</span></span> | <span data-ttu-id="9096c-134">Dlaczego</span><span class="sxs-lookup"><span data-stu-id="9096c-134">Why</span></span> |
| --- | --- |
| <span data-ttu-id="9096c-135">80</span><span class="sxs-lookup"><span data-stu-id="9096c-135">80</span></span> |<span data-ttu-id="9096c-136">**Wymagane** dla portu HTTP dla certyfikatu weryfikacji i opcjonalnie łączności danych.</span><span class="sxs-lookup"><span data-stu-id="9096c-136">**Required** for HTTP port for certificate validation and optionally for data connectivity.</span></span> |
| <span data-ttu-id="9096c-137">443</span><span class="sxs-lookup"><span data-stu-id="9096c-137">443</span></span> |<span data-ttu-id="9096c-138">**Opcjonalne** połączeń danych.</span><span class="sxs-lookup"><span data-stu-id="9096c-138">**Optional** for data connectivity.</span></span> <span data-ttu-id="9096c-139">Jeśli too443 łączność wychodząca jest niedostępna, jest używany TCP port 80.</span><span class="sxs-lookup"><span data-stu-id="9096c-139">If outbound connectivity too443 is unavailable, TCP port 80 is used.</span></span> |
| <span data-ttu-id="9096c-140">5671 i 9352</span><span class="sxs-lookup"><span data-stu-id="9096c-140">5671 and 9352</span></span> |<span data-ttu-id="9096c-141">**Zalecane** , ale opcjonalne dla połączenia danych.</span><span class="sxs-lookup"><span data-stu-id="9096c-141">**Recommended** but Optional for data connectivity.</span></span> <span data-ttu-id="9096c-142">Należy pamiętać, że w tym trybie zwykle zapewnia wyższą przepływność.</span><span class="sxs-lookup"><span data-stu-id="9096c-142">Note this mode usually yields higher throughput.</span></span> <span data-ttu-id="9096c-143">Jeśli porty toothese łączność wychodząca jest niedostępna, jest używany TCP port 443.</span><span class="sxs-lookup"><span data-stu-id="9096c-143">If outbound connectivity toothese ports is unavailable, TCP port 443 is used.</span></span> |

* <span data-ttu-id="9096c-144">Musi być w stanie tooreach hello *hostname*:*numer_portu* zasobu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="9096c-144">Must be able tooreach hello *hostname*:*portnumber* of your on-premises resource.</span></span>

<span data-ttu-id="9096c-145">Hello opisanych w tym artykule założono, że używasz przeglądarki hello z hello komputer, który będzie hostem agenta połączenia hybrydowego lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="9096c-145">hello steps in this article assume that you are using hello browser from hello computer that will host hello on-premises hybrid connection agent.</span></span>

<span data-ttu-id="9096c-146">Jeśli masz już programu SQL Server zainstalowanego w konfiguracji i w środowisku, które spełnia warunki hello opisane powyżej, możesz przejść od razu i rozpoczynać [Utwórz bazę danych programu SQL Server lokalne](#CreateSQLDB).</span><span class="sxs-lookup"><span data-stu-id="9096c-146">If you already have SQL Server installed in a configuration and in an environment that meets hello conditions described above, you can skip ahead and start with [Create a SQL Server database on-premises](#CreateSQLDB).</span></span>

<a name="InstallSQL"></a>

## <a name="a-install-sql-server-express-enable-tcpip-and-create-a-sql-server-database-on-premises"></a><span data-ttu-id="9096c-147">A.</span><span class="sxs-lookup"><span data-stu-id="9096c-147">A.</span></span> <span data-ttu-id="9096c-148">Instalowanie programu SQL Server Express, Włącz protokół TCP/IP i utworzyć lokalnej bazy danych programu SQL Server</span><span class="sxs-lookup"><span data-stu-id="9096c-148">Install SQL Server Express, enable TCP/IP, and create a SQL Server database on-premises</span></span>
<span data-ttu-id="9096c-149">W tej sekcji przedstawiono sposób tooinstall programu SQL Server Express, Włącz protokół TCP/IP i utworzyć bazę danych tak, aby aplikacja sieci web będzie działać z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9096c-149">This section shows you how tooinstall SQL Server Express, enable TCP/IP, and create a database so that your web application will work with hello Azure Portal.</span></span>

### <a name="install-sql-server-express"></a><span data-ttu-id="9096c-150">Zainstaluj program SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="9096c-150">Install SQL Server Express</span></span>
1. <span data-ttu-id="9096c-151">tooinstall programu SQL Server Express, uruchom hello **SQLEXPRWT_x64_ENU.exe** lub **SQLEXPR_x86_ENU.exe** pobranego pliku.</span><span class="sxs-lookup"><span data-stu-id="9096c-151">tooinstall SQL Server Express, run hello **SQLEXPRWT_x64_ENU.exe** or **SQLEXPR_x86_ENU.exe** file that you downloaded.</span></span> <span data-ttu-id="9096c-152">zostanie wyświetlony Kreator Centrum instalacji programu SQL Server Hello.</span><span class="sxs-lookup"><span data-stu-id="9096c-152">hello SQL Server Installation Center wizard appears.</span></span>
   
    ![Instalacja serwera SQL][SQLServerInstall]
2. <span data-ttu-id="9096c-154">Wybierz **nowy serwer SQL instalacji autonomicznej lub Dodaj funkcje tooan istniejącej instalacji**.</span><span class="sxs-lookup"><span data-stu-id="9096c-154">Choose **New SQL Server stand-alone installation or add features tooan existing installation**.</span></span> <span data-ttu-id="9096c-155">Wykonaj instrukcje hello, akceptując hello opcje domyślne i ustawienia, do momentu uzyskania toohello **Konfiguracja wystąpienia** strony.</span><span class="sxs-lookup"><span data-stu-id="9096c-155">Follow hello instructions, accepting hello default choices and settings, until you get toohello **Instance Configuration** page.</span></span>
3. <span data-ttu-id="9096c-156">Na powitania **Konfiguracja wystąpienia** wybierz pozycję **domyślnego wystąpienia**.</span><span class="sxs-lookup"><span data-stu-id="9096c-156">On hello **Instance Configuration** page, choose **Default instance**.</span></span>
   
    ![Wybierz wystąpienie domyślne][ChooseDefaultInstance]
   
    <span data-ttu-id="9096c-158">Domyślnie hello domyślnego wystąpienia programu SQL Server nasłuchuje żądań od klientów programu SQL Server na statycznych porcie 1433, czyli jakie hello funkcja wymaga połączeń hybrydowych.</span><span class="sxs-lookup"><span data-stu-id="9096c-158">By default, hello default instance of SQL Server listens for requests from SQL Server clients on static port 1433, which is what hello Hybrid Connections feature requires.</span></span> <span data-ttu-id="9096c-159">Nazwane wystąpienia używać portów dynamicznych i UDP, które nie są obsługiwane przez połączeń hybrydowych było możliwe.</span><span class="sxs-lookup"><span data-stu-id="9096c-159">Named instances use dynamic ports and UDP, which are not supported by Hybrid Connections.</span></span>
4. <span data-ttu-id="9096c-160">Zaakceptuj ustawienia domyślne hello na powitania **konfiguracji serwera** strony.</span><span class="sxs-lookup"><span data-stu-id="9096c-160">Accept hello defaults on hello **Server Configuration** page.</span></span>
5. <span data-ttu-id="9096c-161">Na powitania **Konfiguracja aparatu bazy danych** w obszarze **tryb uwierzytelniania**, wybierz **trybu mieszanego (uwierzytelnianie programu SQL Server i uwierzytelniania systemu Windows)**i podaj hasło.</span><span class="sxs-lookup"><span data-stu-id="9096c-161">On hello **Database Engine Configuration** page, under **Authentication Mode**, choose **Mixed Mode (SQL Server authentication and Windows authentication)**, and provide a password.</span></span>
   
    ![Wybierz tryb mieszany][ChooseMixedMode]
   
    <span data-ttu-id="9096c-163">W tym samouczku będziesz używać uwierzytelniania programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9096c-163">In this tutorial, you will be using SQL Server authentication.</span></span> <span data-ttu-id="9096c-164">Należy się tooremember hello hasła, ponieważ będzie potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="9096c-164">Be sure tooremember hello password that you provide, because you will need it later.</span></span>
6. <span data-ttu-id="9096c-165">Przejrzyj kroki hello reszty hello kreatora toocomplete hello instalacji.</span><span class="sxs-lookup"><span data-stu-id="9096c-165">Step through hello rest of hello wizard toocomplete hello installation.</span></span>

### <a name="enable-tcpip"></a><span data-ttu-id="9096c-166">Włącz protokół TCP/IP</span><span class="sxs-lookup"><span data-stu-id="9096c-166">Enable TCP/IP</span></span>
<span data-ttu-id="9096c-167">tooenable TCP/IP użyjesz programu SQL Server Configuration Manager, który został zainstalowany przed zainstalowaniem programu SQL Server Express.</span><span class="sxs-lookup"><span data-stu-id="9096c-167">tooenable TCP/IP, you will use SQL Server Configuration Manager, which was installed when you installed SQL Server Express.</span></span> <span data-ttu-id="9096c-168">Wykonaj kroki hello w [Włącz protokół dla programu SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) przed kontynuowaniem.</span><span class="sxs-lookup"><span data-stu-id="9096c-168">Follow hello steps in [Enable TCP/IP Network Protocol for SQL Server](http://technet.microsoft.com/library/hh231672%28v=sql.110%29.aspx) before continuing.</span></span>

<a name="CreateSQLDB"></a>

### <a name="create-a-sql-server-database-on-premises"></a><span data-ttu-id="9096c-169">Utwórz bazę danych programu SQL Server lokalne</span><span class="sxs-lookup"><span data-stu-id="9096c-169">Create a SQL Server database on-premises</span></span>
<span data-ttu-id="9096c-170">Aplikacja sieci web programu Visual Studio wymaga Azure można uzyskać dostępu do bazy danych członkostwa.</span><span class="sxs-lookup"><span data-stu-id="9096c-170">Your Visual Studio web application requires a membership database that can be accessed by Azure.</span></span> <span data-ttu-id="9096c-171">Wymaga to bazy danych programu SQL Server lub SQL Server Express (nie hello bazie danych LocalDB który hello używa szablonu MVC domyślnie), więc następnie utworzysz hello członkostwa w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="9096c-171">This requires a SQL Server or SQL Server Express database (not hello LocalDB database that hello MVC template uses by default), so you'll create hello membership database next.</span></span>

1. <span data-ttu-id="9096c-172">W programu SQL Server Management Studio połącz toohello programu SQL Server został właśnie zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="9096c-172">In SQL Server Management Studio, connect toohello SQL Server you just installed.</span></span> <span data-ttu-id="9096c-173">(Jeśli hello **połączyć tooServer** okna dialogowego nie zostanie wyświetlone automatycznie, przejdź do zbyt**Eksplorator obiektów** w okienku po lewej stronie powitania kliknij **Connect**, a następnie kliknij przycisk **Bazy danych aparatu**.) ![Połącz tooServer][SSMSConnectToServer]</span><span class="sxs-lookup"><span data-stu-id="9096c-173">(If hello **Connect tooServer** dialog does not appear automatically, navigate too**Object Explorer** in hello left pane, click **Connect**, and then click **Database Engine**.) ![Connect tooServer][SSMSConnectToServer]</span></span>
   
    <span data-ttu-id="9096c-174">Aby uzyskać **typ serwera**, wybierz **aparatu bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="9096c-174">For **Server type**, choose **Database Engine**.</span></span> <span data-ttu-id="9096c-175">Dla **nazwy serwera**, można użyć **localhost** lub nazwa hello hello komputera, którego używasz.</span><span class="sxs-lookup"><span data-stu-id="9096c-175">For **Server name**, you can use **localhost** or hello name of hello computer that you are using.</span></span> <span data-ttu-id="9096c-176">Wybierz **uwierzytelniania programu SQL Server**, a następnie zaloguj się za pomocą hello nazwy użytkownika i hasła hello, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="9096c-176">Choose **SQL Server authentication**, and then log in with hello sa user name and hello password that you created earlier.</span></span>
2. <span data-ttu-id="9096c-177">Kliknij prawym przyciskiem myszy nową bazę danych przy użyciu programu SQL Server Management Studio, toocreate **baz danych** w Eksploratorze obiektów, a następnie kliknij przycisk **nową bazę danych**.</span><span class="sxs-lookup"><span data-stu-id="9096c-177">toocreate a new database by using SQL Server Management Studio, right-click **Databases** in Object Explorer, and then click **New Database**.</span></span>
   
    ![Utwórz nową bazę danych][SSMScreateNewDB]
3. <span data-ttu-id="9096c-179">W hello **nową bazę danych** okna dialogowego, wprowadź MembershipDB hello nazwy bazy danych, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9096c-179">In hello **New Database** dialog, enter MembershipDB for hello database name, and then click **OK**.</span></span>
   
    ![Podaj nazwę bazy danych][SSMSprovideDBname]
   
    <span data-ttu-id="9096c-181">Należy pamiętać, że nie wprowadzisz wszystkie bazy danych toohello zmiany w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="9096c-181">Note that you do not make any changes toohello database at this point.</span></span> <span data-ttu-id="9096c-182">informacje o członkostwie w Hello zostaną automatycznie później dodane przez aplikację sieci web po uruchomieniu.</span><span class="sxs-lookup"><span data-stu-id="9096c-182">hello membership information will be added automatically later by your web application when you run it.</span></span>
4. <span data-ttu-id="9096c-183">W Eksploratorze obiektów po rozwinięciu **baz danych**, zobaczysz tej bazy danych członkostwa hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="9096c-183">In Object Explorer, if you expand **Databases**, you will see that hello membership database has been created.</span></span>
   
    ![MembershipDB utworzone][SSMSMembershipDBCreated]

<a name="CreateSite"></a>

## <a name="b-create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="9096c-185">B.</span><span class="sxs-lookup"><span data-stu-id="9096c-185">B.</span></span> <span data-ttu-id="9096c-186">Tworzenie aplikacji sieci web w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9096c-186">Create a web app in hello Azure Portal</span></span>
> [!NOTE]
> <span data-ttu-id="9096c-187">Jeśli utworzono już aplikacji sieci web w hello mają toouse w tym samouczku portalu Azure, możesz przejść od razu zbyt[Tworzenie połączenia hybrydowego i usługi BizTalk](#CreateHC) i kontynuować stamtąd.</span><span class="sxs-lookup"><span data-stu-id="9096c-187">If you have already created a web app in hello Azure Portal that you want toouse for this tutorial, you can skip ahead too[Create a Hybrid Connection and a BizTalk Service](#CreateHC) and continue from there.</span></span>
> 
> 

1. <span data-ttu-id="9096c-188">W hello [Azure Portal](https://portal.azure.com), kliknij przycisk **nowy** > **sieci Web i mobilność** > **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="9096c-188">In hello [Azure Portal](https://portal.azure.com), click **New** > **Web + Mobile** > **Web app**.</span></span>
   
    ![Przycisk Nowy][New]
2. <span data-ttu-id="9096c-190">Konfigurowanie aplikacji sieci web, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9096c-190">Configure your web app, and then click **Create**.</span></span>
   
    ![Nazwa witryny sieci Web][WebsiteCreationBlade]
3. <span data-ttu-id="9096c-192">Po kilku chwilach hello aplikacji sieci web jest tworzona i pojawia się jego bloku aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="9096c-192">After a few moments, hello web app is created and its web app blade appears.</span></span> <span data-ttu-id="9096c-193">Blok Hello jest pionowo przewijanego pulpit nawigacyjny, który umożliwia zarządzanie aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9096c-193">hello blade is a vertically scrollable dashboard that lets you manage your web app.</span></span>
   
    ![Witryny sieci Web uruchomionej][WebSiteRunningBlade]
   
    <span data-ttu-id="9096c-195">Aplikacja sieci web hello tooverify jest na żywo, można kliknąć hello **Przeglądaj** ikona toodisplay hello domyślnej strony.</span><span class="sxs-lookup"><span data-stu-id="9096c-195">tooverify hello web app is live, you can click hello **Browse** icon toodisplay hello default page.</span></span>

<span data-ttu-id="9096c-196">Następnie utworzysz, połączenie hybrydowe i usługi BizTalk hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="9096c-196">Next, you will create a hybrid connection and a BizTalk service for hello web app.</span></span>

<a name="CreateHC"></a>

## <a name="c-create-a-hybrid-connection-and-a-biztalk-service"></a><span data-ttu-id="9096c-197">C.</span><span class="sxs-lookup"><span data-stu-id="9096c-197">C.</span></span> <span data-ttu-id="9096c-198">Tworzenie połączenia hybrydowego i usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="9096c-198">Create a Hybrid Connection and a BizTalk Service</span></span>
1. <span data-ttu-id="9096c-199">Wstecz w hello portalu, przejdź do pozycji toosettings i kliknij przycisk **sieci** > **skonfiguruj punkty końcowe połączenia hybrydowego**.</span><span class="sxs-lookup"><span data-stu-id="9096c-199">Back in hello Portal, go toosettings and click **Networking** > **Configure your hybrid connection endpoints**.</span></span>
   
    ![Połączenia hybrydowe][CreateHCHCIcon]
2. <span data-ttu-id="9096c-201">W bloku połączeń hybrydowych hello, kliknij **Dodaj** > **nowe połączenie hybrydowe**.</span><span class="sxs-lookup"><span data-stu-id="9096c-201">On hello Hybrid connections blade, click **Add** > **New hybrid connection**.</span></span>
3. <span data-ttu-id="9096c-202">Na powitania **Tworzenie połączenia hybrydowego** bloku:</span><span class="sxs-lookup"><span data-stu-id="9096c-202">On hello **Create hybrid connection** blade:</span></span>
   
   * <span data-ttu-id="9096c-203">Aby uzyskać **nazwa**, podaj nazwę hello połączenia.</span><span class="sxs-lookup"><span data-stu-id="9096c-203">For **Name**, provide a name for hello connection.</span></span>
   * <span data-ttu-id="9096c-204">Aby uzyskać **Hostname**, wpisz nazwę komputera hello komputera-hosta programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9096c-204">For **Hostname**, enter hello computer name of your SQL Server host computer.</span></span>
   * <span data-ttu-id="9096c-205">Aby uzyskać **portu**, wprowadź 1433 (hello domyślny port dla programu SQL Server).</span><span class="sxs-lookup"><span data-stu-id="9096c-205">For **Port**, enter 1433 (hello default port for SQL Server).</span></span>
   * <span data-ttu-id="9096c-206">Kliknij przycisk **usługi BizTalk** > **nową usługę BizTalk** , a następnie wprowadź nazwę hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="9096c-206">Click **BizTalk Service** > **New BizTalk Service** and enter a name for hello BizTalk service.</span></span>
     
     ![Tworzenie połączenia hybrydowego][TwinCreateHCBlades]
4. <span data-ttu-id="9096c-208">Kliknij przycisk **OK** dwa razy.</span><span class="sxs-lookup"><span data-stu-id="9096c-208">Click **OK** twice.</span></span>
   
    <span data-ttu-id="9096c-209">Gdy hello zakończeniu procesu hello **powiadomienia** obszaru będzie flash zielona **Powodzenie** i hello **połączenia hybrydowego** bloku wyświetli hello nowe połączenie hybrydowe z Witaj statusu **niepołączone**.</span><span class="sxs-lookup"><span data-stu-id="9096c-209">When hello process completes, hello **Notifications** area will flash a green **SUCCESS** and hello **Hybrid connection** blade will show hello new hybrid connection with hello status as **Not connected**.</span></span>
   
    ![Połączenia hybrydowe jeden utworzone][CreateHCOneConnectionCreated]

<span data-ttu-id="9096c-211">W tym momencie została ukończona ważnym elementem hello chmury hybrydowej połączenia infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="9096c-211">At this point, you have completed an important part of hello cloud hybrid connection infrastructure.</span></span> <span data-ttu-id="9096c-212">Następnie utworzy odpowiedni element lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="9096c-212">Next, you will create a corresponding on-premises piece.</span></span>

<a name="InstallHCM"></a>

## <a name="d-install-hello-on-premises-hybrid-connection-manager-toocomplete-hello-connection"></a><span data-ttu-id="9096c-213">D.</span><span class="sxs-lookup"><span data-stu-id="9096c-213">D.</span></span> <span data-ttu-id="9096c-214">Zainstaluj hello lokalnego Menedżera połączeń hybrydowych toocomplete hello połączenia</span><span class="sxs-lookup"><span data-stu-id="9096c-214">Install hello on-premises Hybrid Connection Manager toocomplete hello connection</span></span>
[!INCLUDE [app-service-hybrid-connections-manager-install](../../includes/app-service-hybrid-connections-manager-install.md)]

<span data-ttu-id="9096c-215">Po zakończeniu tego połączenia infrastruktura hybrydowa hello spowoduje utworzenie aplikacji sieci web, która korzysta z niego.</span><span class="sxs-lookup"><span data-stu-id="9096c-215">Now that hello hybrid connection infrastructure is complete, you will create a web application that uses it.</span></span>

<a name="CreateASPNET"></a>

## <a name="e-create-a-basic-aspnet-web-project-edit-hello-database-connection-string-and-run-hello-project-locally"></a><span data-ttu-id="9096c-216">E.</span><span class="sxs-lookup"><span data-stu-id="9096c-216">E.</span></span> <span data-ttu-id="9096c-217">Utworzyć podstawowy projekt sieci web ASP.NET, Edytuj parametry połączenia bazy danych hello i uruchomić projekt hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="9096c-217">Create a basic ASP.NET web project, edit hello database connection string, and run hello project locally</span></span>
### <a name="create-a-basic-aspnet-project"></a><span data-ttu-id="9096c-218">Tworzenie podstawowego projektu programu ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9096c-218">Create a basic ASP.NET project</span></span>
1. <span data-ttu-id="9096c-219">W programie Visual Studio na powitania **pliku** menu, Utwórz nowy projekt:</span><span class="sxs-lookup"><span data-stu-id="9096c-219">In Visual Studio, on hello **File** menu, create a new Project:</span></span>
   
    ![Nowy projekt programu Visual Studio][HCVSNewProject]
2. <span data-ttu-id="9096c-221">W hello **szablony** sekcji hello **nowy projekt** okno dialogowe, wybierz opcję **sieci Web** i wybierz polecenie **aplikacji sieci Web ASP.NET**, a następnie kliknij przycisk  **OK**.</span><span class="sxs-lookup"><span data-stu-id="9096c-221">In hello **Templates** section of hello **New Project** dialog, select **Web** and choose **ASP.NET Web Application**, and then click **OK**.</span></span>
   
    ![Wybierz aplikację sieci Web ASP.NET][HCVSChooseASPNET]
3. <span data-ttu-id="9096c-223">W hello **nowy projekt ASP.NET** okno dialogowe, wybierz **MVC**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9096c-223">In hello **New ASP.NET Project** dialog, choose **MVC**, and then click **OK**.</span></span>
   
    ![Wybierz MVC][HCVSChooseMVC]
4. <span data-ttu-id="9096c-225">Po utworzeniu projektu hello, zostanie wyświetlona strona readme aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9096c-225">When hello project has been created, hello application readme page appears.</span></span> <span data-ttu-id="9096c-226">Nie należy jeszcze uruchamiać hello projektu sieci web.</span><span class="sxs-lookup"><span data-stu-id="9096c-226">Do not run hello web project yet.</span></span>
   
    ![Stronę Readme][HCVSReadmePage]

### <a name="edit-hello-database-connection-string-for-hello-application"></a><span data-ttu-id="9096c-228">Edytuj parametry połączenia bazy danych hello aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="9096c-228">Edit hello database connection string for hello application</span></span>
<span data-ttu-id="9096c-229">W tym kroku, Edytuj parametry połączenia hello informujący o posiadanych aplikacji gdzie toofind Twojego lokalny program SQL Server Express bazy danych.</span><span class="sxs-lookup"><span data-stu-id="9096c-229">In this step, you edit hello connection string that tells your application where toofind your local SQL Server Express database.</span></span> <span data-ttu-id="9096c-230">Parametry połączenia Hello są w pliku Web.config aplikacji hello, który zawiera informacje dotyczące konfiguracji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9096c-230">hello connection string is in hello application's Web.config file, which contains configuration information for hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="9096c-231">tooensure używanych przez aplikację hello bazy danych, utworzony w programu SQL Server Express, a nie hello jedną domyślnej programu Visual Studio LocalDB, ważne jest ukończenia tego kroku przed uruchomieniem projektu.</span><span class="sxs-lookup"><span data-stu-id="9096c-231">tooensure that your application uses hello database that you created in SQL Server Express, and not hello one in Visual Studio's default LocalDB, it is important that you complete this step before running your project.</span></span>
> 
> 

1. <span data-ttu-id="9096c-232">W Eksploratorze rozwiązań kliknij dwukrotnie plik Web.config hello.</span><span class="sxs-lookup"><span data-stu-id="9096c-232">In Solution Explorer, double-click hello Web.config file.</span></span>
   
    ![Web.config][HCVSChooseWebConfig]
2. <span data-ttu-id="9096c-234">Edytuj hello **connectionStrings** bazy danych programu SQL Server toohello toopoint sekcji na komputerze lokalnym, składni hello w hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="9096c-234">Edit hello **connectionStrings** section toopoint toohello SQL Server database on your local machine, following hello syntax in hello following example:</span></span>
   
    ![Parametry połączenia][HCVSConnectionString]
   
    <span data-ttu-id="9096c-236">Tworząc hello parametry połączenia, należy uwzględnić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="9096c-236">When composing hello connection string, keep in mind hello following:</span></span>
   
   * <span data-ttu-id="9096c-237">Jeśli łączysz tooa nazwanego wystąpienia, a nie wystąpienia domyślnego (na przykład YourServer\SQLEXPRESS), należy skonfigurować porty statycznych toouse programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9096c-237">If you are connecting tooa named instance instead of a default instance (for example, YourServer\SQLEXPRESS), you must configure your SQL Server toouse static ports.</span></span> <span data-ttu-id="9096c-238">Informacje dotyczące konfigurowania portów statycznych, zobacz [jak tooconfigure toolisten programu SQL Server na określonym porcie](http://support.microsoft.com/kb/823938).</span><span class="sxs-lookup"><span data-stu-id="9096c-238">For information on configuring static ports, see [How tooconfigure SQL Server toolisten on a specific port](http://support.microsoft.com/kb/823938).</span></span> <span data-ttu-id="9096c-239">Domyślnie nazwane wystąpienia używają protokołów UDP i porty dynamiczne, które nie są obsługiwane przez połączeń hybrydowych było możliwe.</span><span class="sxs-lookup"><span data-stu-id="9096c-239">By default, named instances use UDP and dynamic ports, which are not supported by Hybrid Connections.</span></span>
   * <span data-ttu-id="9096c-240">Zaleca się, że podajesz hello portu (1433 domyślnie, jak pokazano w przykładzie hello) na powitania parametry połączenia, dzięki czemu można mieć pewność, że lokalny serwer SQL został włączony protokół TCP i korzysta z poprawnego portu hello.</span><span class="sxs-lookup"><span data-stu-id="9096c-240">It is recommended that you specify hello port (1433 by default, as shown in hello example) on hello connection string so that you can be sure that your local SQL Server has TCP enabled and is using hello correct port.</span></span>
   * <span data-ttu-id="9096c-241">Należy pamiętać, tooconnect uwierzytelniania programu SQL Server toouse, określając hello identyfikator użytkownika i hasło w ciągu połączenia.</span><span class="sxs-lookup"><span data-stu-id="9096c-241">Remember toouse SQL Server Authentication tooconnect, specifying hello user ID and password in your connection string.</span></span>
3. <span data-ttu-id="9096c-242">Kliknij przycisk **zapisać** w pliku Web.config hello toosave programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9096c-242">Click **Save** in Visual Studio toosave hello Web.config file.</span></span>

### <a name="run-hello-project-locally-and-register-a-new-user"></a><span data-ttu-id="9096c-243">Uruchom projekt hello lokalnie i zarejestrować nowego użytkownika</span><span class="sxs-lookup"><span data-stu-id="9096c-243">Run hello project locally and register a new user</span></span>
1. <span data-ttu-id="9096c-244">Teraz Uruchom nowego projektu sieci web lokalnie przez kliknięcie przycisku Przeglądaj hello w obszarze debugowania.</span><span class="sxs-lookup"><span data-stu-id="9096c-244">Now, run your new web project locally by clicking hello browse button under Debug.</span></span> <span data-ttu-id="9096c-245">W tym przykładzie użyto programu Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="9096c-245">This example uses Internet Explorer.</span></span>
   
    ![Uruchom projekt][HCVSRunProject]
2. <span data-ttu-id="9096c-247">Na powitania prawym górnym rogu hello domyślnej strony sieci web, wybierz **zarejestrować** tooregister nowe konto:</span><span class="sxs-lookup"><span data-stu-id="9096c-247">On hello upper right of hello default web page, choose **Register** tooregister a new account:</span></span>
   
    ![Zarejestruj nowe konto][HCVSRegisterLocally]
3. <span data-ttu-id="9096c-249">Wprowadź nazwę użytkownika i hasło:</span><span class="sxs-lookup"><span data-stu-id="9096c-249">Enter a user name and password:</span></span>
   
    ![Wprowadź nazwę użytkownika i hasło][HCVSCreateNewAccount]
   
    <span data-ttu-id="9096c-251">Powoduje to automatyczne utworzenie bazy danych na serwerze SQL lokalne powitania informacje członkostwa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9096c-251">This automatically creates a database on your local SQL Server that holds hello membership information for your application.</span></span> <span data-ttu-id="9096c-252">Jedną z tabel hello (**dbo. AspNetUsers**) poświadczenia użytkownika aplikacji, takich jak te, które zostały wprowadzone hello sieci web blokad.</span><span class="sxs-lookup"><span data-stu-id="9096c-252">One of hello tables (**dbo.AspNetUsers**) holds web app user credentials like hello ones that you just entered.</span></span> <span data-ttu-id="9096c-253">Później w samouczku hello, pojawi się w tej tabeli.</span><span class="sxs-lookup"><span data-stu-id="9096c-253">You will see this table later in hello tutorial.</span></span>
4. <span data-ttu-id="9096c-254">Zamknij okno przeglądarki hello hello domyślnej strony sieci web.</span><span class="sxs-lookup"><span data-stu-id="9096c-254">Close hello browser window of hello default web page.</span></span> <span data-ttu-id="9096c-255">Powoduje to zatrzymanie aplikacji hello w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9096c-255">This stops hello application in Visual Studio.</span></span>

<span data-ttu-id="9096c-256">Są teraz gotowe do następnego kroku hello, czyli tooAzure aplikacji hello toopublish i przetestować go.</span><span class="sxs-lookup"><span data-stu-id="9096c-256">You are now ready for hello next step, which is toopublish hello application tooAzure and test it.</span></span>

<a name="PubNTest"></a>

## <a name="f-publish-hello-web-application-tooazure-and-test-it"></a><span data-ttu-id="9096c-257">F.</span><span class="sxs-lookup"><span data-stu-id="9096c-257">F.</span></span> <span data-ttu-id="9096c-258">Publikowanie tooAzure aplikacji sieci web hello i przetestować go</span><span class="sxs-lookup"><span data-stu-id="9096c-258">Publish hello web application tooAzure and test it</span></span>
<span data-ttu-id="9096c-259">Teraz, należy opublikować Twojej aplikacji tooyour aplikacji sieci web usługi aplikacji i przetestowanie toosee jak jest połączenie hybrydowe hello skonfigurowane wcześniej są używane tooconnect bazy danych toohello aplikacji sieci web na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="9096c-259">Now, you'll publish your application tooyour App Service web app and then test it toosee how hello hybrid connection you configured earlier is being used tooconnect your web app toohello database on your local machine.</span></span>

### <a name="publish-hello-web-application"></a><span data-ttu-id="9096c-260">Publikowanie aplikacji sieci web hello</span><span class="sxs-lookup"><span data-stu-id="9096c-260">Publish hello web application</span></span>
1. <span data-ttu-id="9096c-261">Można pobrać profilu publikowania dla aplikacji sieci web usługi aplikacji w portalu Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="9096c-261">You can download your publishing profile for hello App Service web app in hello Azure Portal.</span></span> <span data-ttu-id="9096c-262">Na powitania bloku aplikacji sieci web, kliknij przycisk **Get profilu publikowania**, a następnie zapisz hello pliku tooyour komputera.</span><span class="sxs-lookup"><span data-stu-id="9096c-262">On hello blade for your web app, click **Get publish profile**, and then save hello file tooyour computer.</span></span>
   
    ![Pobieranie profilu publikowania][PortalDownloadPublishProfile]
   
    <span data-ttu-id="9096c-264">Zostanie następnie zaimportować ten plik do aplikacji sieci web programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9096c-264">Next, you will import this file into your Visual Studio web application.</span></span>
2. <span data-ttu-id="9096c-265">W programie Visual Studio, kliknij prawym przyciskiem myszy nazwę projektu hello w Eksploratorze rozwiązań i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="9096c-265">In Visual Studio, right-click hello project name in Solution Explorer and select **Publish**.</span></span>
   
    ![Wybierz publikowania][HCVSRightClickProjectSelectPublish]
3. <span data-ttu-id="9096c-267">W hello **publikowanie w sieci Web** okna dialogowego na powitania **profilu** , wybierz pozycję **importu**.</span><span class="sxs-lookup"><span data-stu-id="9096c-267">In hello **Publish Web** dialog, on hello **Profile** tab, choose **Import**.</span></span>
   
    ![Import][HCVSPublishWebDialogImport]
4. <span data-ttu-id="9096c-269">Przeglądaj tooyour pobrany profil publikowania, zaznacz go, a następnie kliknij **OK**.</span><span class="sxs-lookup"><span data-stu-id="9096c-269">Browse tooyour downloaded publishing profile, select it, and then click **OK**.</span></span>
   
    ![Przeglądaj tooprofile][HCVSBrowseToImportPubProfile]
5. <span data-ttu-id="9096c-271">Publikowanie informacji jest importowany i wyświetla na powitania **połączenia** kartę hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9096c-271">Your publishing information is imported and displays on hello **Connection** tab of hello dialog.</span></span>
   
    ![Kliknij przycisk Publikuj][HCVSClickPublish]
   
    <span data-ttu-id="9096c-273">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="9096c-273">Click **Publish**.</span></span>
   
    <span data-ttu-id="9096c-274">Po ukończeniu publikowania przeglądarki będzie uruchomić i pokazać teraz znanych aplikacji ASP.NET--z tą różnicą, że jest teraz na żywo w hello chmury Azure!</span><span class="sxs-lookup"><span data-stu-id="9096c-274">When publishing completes, your browser will launch and show your now familiar ASP.NET application -- except that now it is live in hello Azure cloud!</span></span>

<span data-ttu-id="9096c-275">Następnie użyjesz toosee aplikacji sieci web na żywo połączenie hybrydowe w akcji.</span><span class="sxs-lookup"><span data-stu-id="9096c-275">Next, you will use your live web application toosee its Hybrid Connection in action.</span></span>

### <a name="test-hello-completed-web-application-on-azure"></a><span data-ttu-id="9096c-276">Test hello ukończone aplikacji sieci web na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9096c-276">Test hello completed web application on Azure</span></span>
1. <span data-ttu-id="9096c-277">U góry powitania po prawej stronie sieci web na platformie Azure, wybierz **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="9096c-277">On hello top right of your web page on Azure, choose **Log in**.</span></span>
   
    ![Dziennik testu w][HCTestLogIn]
2. <span data-ttu-id="9096c-279">Usługi aplikacji, których aplikacja sieci web jest teraz połączona bazy danych członkostwa aplikacji sieci web tooyour na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="9096c-279">Your App Service web app is now connected tooyour web application's membership database on your local machine.</span></span> <span data-ttu-id="9096c-280">tooverify, zaloguj się przy użyciu tych samych poświadczeń, które należy wprowadzić w lokalne powitania bazy danych wcześniej hello.</span><span class="sxs-lookup"><span data-stu-id="9096c-280">tooverify this, log in with hello same credentials that you entered in hello local database earlier.</span></span>
   
    ![Witaj pozdrowienia][HCTestHelloContoso]
3. <span data-ttu-id="9096c-282">toofurther przetestuj nowe połączenie hybrydowe, wylogować się z aplikacji sieci web platformy Azure i Zarejestruj się jako inny użytkownik.</span><span class="sxs-lookup"><span data-stu-id="9096c-282">toofurther test your new hybrid connection, log off of your Azure web application and register as another user.</span></span> <span data-ttu-id="9096c-283">Podaj nową nazwę użytkownika i hasło, a następnie kliknij przycisk **zarejestrować**.</span><span class="sxs-lookup"><span data-stu-id="9096c-283">Provide a new user name and password, and then click **Register**.</span></span>
   
    ![Test zarejestrować innego użytkownika][HCTestRegisterRelecloud]
4. <span data-ttu-id="9096c-285">tooverify hello nowe poświadczenia użytkownika były przechowywane w lokalnej bazie danych za pośrednictwem połączenia hybrydowe, Otwórz program SQL Management Studio na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="9096c-285">tooverify that hello new user's credentials have been stored in your local database through your hybrid connection, open SQL Management Studio on your local computer.</span></span> <span data-ttu-id="9096c-286">W Eksploratorze obiektów rozwiń hello **MembershipDB** bazy danych, a następnie rozwiń **tabel**.</span><span class="sxs-lookup"><span data-stu-id="9096c-286">In Object Explorer, expand hello **MembershipDB** database, and then expand **Tables**.</span></span> <span data-ttu-id="9096c-287">Kliknij prawym przyciskiem myszy hello **dbo. AspNetUsers** członkostwa tabeli i wybierz polecenie **zaznacz 1000 pierwszych wierszy** tooview hello wyników.</span><span class="sxs-lookup"><span data-stu-id="9096c-287">Right-click hello **dbo.AspNetUsers** membership table and choose **Select Top 1000 Rows** tooview hello results.</span></span>
   
    ![Wyświetl wyniki hello][HCTestSSMSTree]
5. <span data-ttu-id="9096c-289">Członkostwo w lokalnej tabeli teraz zawiera oba konta — Witaj, został utworzony lokalnie i hello został utworzony w hello chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="9096c-289">Your local membership table now shows both accounts - hello one that you created locally, and hello one that you created in hello Azure cloud.</span></span> <span data-ttu-id="9096c-290">Witaj, został utworzony w chmurze hello został zapisany tooyour lokalną bazą danych za pomocą funkcji połączenie hybrydowe platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9096c-290">hello one that you created in hello cloud has been saved tooyour on-premises database through Azure's Hybrid Connection feature.</span></span>
   
    ![Zarejestrowani użytkownicy w lokalnej bazie danych][HCTestShowMemberDb]

<span data-ttu-id="9096c-292">Możesz teraz utworzeniu i wdrożeniu aplikacji sieci web ASP.NET, która używa połączenie hybrydowe między aplikacji sieci web w hello chmury Azure i lokalną bazą danych programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9096c-292">You have now created and deployed an ASP.NET web application that uses a hybrid connection between a web app in hello Azure cloud and an on-premises SQL Server database.</span></span> <span data-ttu-id="9096c-293">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="9096c-293">Congratulations!</span></span>

## <a name="see-also"></a><span data-ttu-id="9096c-294">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="9096c-294">See Also</span></span>
[<span data-ttu-id="9096c-295">Omówienie połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="9096c-295">Hybrid Connections overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=397274)

[<span data-ttu-id="9096c-296">Dołączony Josha wprowadza połączeń hybrydowych (wideo z witryny Channel 9)</span><span class="sxs-lookup"><span data-stu-id="9096c-296">Josh Twist introduces hybrid connections (Channel 9 video)</span></span>](http://channel9.msdn.com/Shows/Azure-Friday/Josh-Twist-introduces-hybrid-connections)

[<span data-ttu-id="9096c-297">Omówienie połączeń hybrydowych</span><span class="sxs-lookup"><span data-stu-id="9096c-297">Hybrid Connections overview</span></span>](/services/biztalk-services/)

[<span data-ttu-id="9096c-298">Usługi BizTalk Services: Karty Pulpit nawigacyjny, Monitor skali, konfigurowanie i połączenia hybrydowego</span><span class="sxs-lookup"><span data-stu-id="9096c-298">BizTalk Services: Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>](../biztalk-services/biztalk-dashboard-monitor-scale-tabs.md)

[<span data-ttu-id="9096c-299">Tworzenie hybrydowego rzeczywistych chmury chronionej za pomocą bezproblemowe przenośność aplikacji (Channel 9 wideo)</span><span class="sxs-lookup"><span data-stu-id="9096c-299">Building a Real-World Hybrid Cloud with Seamless Application Portability (Channel 9 video)</span></span>](http://channel9.msdn.com/events/TechEd/NorthAmerica/2014/DCIM-B323#fbid=)

[<span data-ttu-id="9096c-300">Dostęp do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9096c-300">Access on-premises resources using hybrid connections in Azure App Service</span></span>](web-sites-hybrid-connection-get-started.md)

[<span data-ttu-id="9096c-301">Tożsamość platformy ASP.NET — omówienie</span><span class="sxs-lookup"><span data-stu-id="9096c-301">ASP.NET Identity Overview</span></span>](http://www.asp.net/identity)

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
