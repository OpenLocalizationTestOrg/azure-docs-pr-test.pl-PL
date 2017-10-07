---
title: "aaaCreate usług BizTalk Azure w portalu Azure hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprovision lub Utwórz usług BizTalk Azure w hello portal Azure. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="cc84e-103">Tworzenie przy użyciu portalu Azure hello usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="cc84e-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="cc84e-104">toosign w toohello portalu Azure, należy konto platformy Azure i subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cc84e-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="cc84e-105">Jeśli nie masz konta, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="cc84e-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="cc84e-106">Zobacz [Bezpłatna wersja próbna platformy Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="cc84e-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="cc84e-107"><a name="CreateService"></a>Tworzenie usługi BizTalk</span><span class="sxs-lookup"><span data-stu-id="cc84e-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="cc84e-108">W zależności od hello wybór wersji nie wszystkie ustawienia usługi BizTalk mogą być dostępne.</span><span class="sxs-lookup"><span data-stu-id="cc84e-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="cc84e-109">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cc84e-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="cc84e-110">Witaj dolnym okienku nawigacji, wybierz **nowy**:</span><span class="sxs-lookup"><span data-stu-id="cc84e-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="cc84e-111">![Wybierz przycisk Nowy hello][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="cc84e-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="cc84e-112">Wybierz kolejno opcje **USŁUGI APLIKACJI** > **USŁUGA BIZTALK** > **TWORZENIE NIESTANDARDOWE**:</span><span class="sxs-lookup"><span data-stu-id="cc84e-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="cc84e-113">![Wybieranie kolejno opcji Usługa BizTalk i Tworzenie niestandardowe][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="cc84e-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="cc84e-114">Wprowadź ustawienia usługi BizTalk hello:</span><span class="sxs-lookup"><span data-stu-id="cc84e-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="cc84e-115"><strong>Nazwa usługi BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="cc84e-116">Można wprowadzić dowolną nazwę, ale musi ona być dokładna.</span><span class="sxs-lookup"><span data-stu-id="cc84e-116">You can enter any name but be specific.</span></span> <span data-ttu-id="cc84e-117">Oto niektóre przykłady:</span><span class="sxs-lookup"><span data-stu-id="cc84e-117">Some examples include:</span></span><br/><br/><span data-ttu-id="cc84e-118">
    <em>mojafirma</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="cc84e-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="cc84e-119">
    <em>mojafirmamojaaplikacja</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="cc84e-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="cc84e-120">
    <em>mojaaplikacja</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="cc84e-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="cc84e-121">". biztalk.windows.net" jest nazwą automatycznie dodawanych toohello możesz wprowadzić.</span><span class="sxs-lookup"><span data-stu-id="cc84e-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="cc84e-122">Spowoduje to utworzenie adresu URL, który jest używany tooaccess Twojego BizTalk usługi tak samo, jak <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="cc84e-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="cc84e-123"><strong>Wersja</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="cc84e-124">Jeśli w fazie testowania programowanie hello, wybierz polecenie <strong>Developer</strong>.</span><span class="sxs-lookup"><span data-stu-id="cc84e-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="cc84e-125">Na etapie produkcji hello, za pomocą hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">usługi BizTalk Services: wykres wersje</a> toodetermine Jeśli <strong>Premium</strong>, <strong>standardowe</strong>, lub <strong>Basic</strong>jest poprawny wybór powitania dla danego scenariusza biznesowego.</span><span class="sxs-lookup"><span data-stu-id="cc84e-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="cc84e-126"><strong>Region</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="cc84e-127">Wybierz usługę BizTalk hello toohost regionu geograficznego.</span><span class="sxs-lookup"><span data-stu-id="cc84e-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cc84e-128"><strong>Adres URL domeny</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="cc84e-129"><strong>Opcjonalnie</strong>.</span><span class="sxs-lookup"><span data-stu-id="cc84e-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="cc84e-130">Domyślnie adres URL domeny hello jest <em>YourBizTalkServiceName</em>. biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="cc84e-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="cc84e-131">Można również wprowadzić niestandardową nazwę domeny. </span><span class="sxs-lookup"><span data-stu-id="cc84e-131">A custom domain can also be entered.</span></span> <span data-ttu-id="cc84e-132">Na przykład jeśli domeną jest <em>contoso</em>, możesz wprowadzić:</span><span class="sxs-lookup"><span data-stu-id="cc84e-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="cc84e-133">
    <em>MojaFirma</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="cc84e-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="cc84e-134">
    <em>MojaFirmaMojaAplikacja</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="cc84e-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="cc84e-135">
    <em>MojaAplikacja</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="cc84e-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="cc84e-136">
    <em>NazwaUsługiBizTalk</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="cc84e-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="cc84e-137">Wybierz strzałkę dalej hello.</span><span class="sxs-lookup"><span data-stu-id="cc84e-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="cc84e-138">5.</span><span class="sxs-lookup"><span data-stu-id="cc84e-138">5.</span></span> <span data-ttu-id="cc84e-139">Wprowadź hello magazynu i ustawienia bazy danych:</span><span class="sxs-lookup"><span data-stu-id="cc84e-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="cc84e-140"><strong>Konto monitorowania/archiwizowania magazynu</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="cc84e-141">Wybierz istniejące konto magazynu lub utwórz nowe.</span><span class="sxs-lookup"><span data-stu-id="cc84e-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="cc84e-142">Jeśli utworzysz nowe konto magazynu, wprowadź hello <strong>nazwy konta magazynu</strong>.</span><span class="sxs-lookup"><span data-stu-id="cc84e-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cc84e-143"><strong>Baza danych śledzenia</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="cc84e-144">Jeśli używasz istniejącej bazy danych SQL Azure, nie można jej użyć w innej usłudze BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="cc84e-145">Należy hello nazwy logowania i hasła podanego podczas tworzenia tego serwera bazy danych SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="cc84e-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="cc84e-146"><strong>Porada</strong> Utwórz hello śledzenia bazę danych i konto magazynu monitorowania/archiwizacja w hello tego samego regionu hello usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="cc84e-147">Wybierz strzałkę dalej hello.</span><span class="sxs-lookup"><span data-stu-id="cc84e-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="cc84e-148">6.</span><span class="sxs-lookup"><span data-stu-id="cc84e-148">6.</span></span> <span data-ttu-id="cc84e-149">Wprowadź ustawienia bazy danych hello:</span><span class="sxs-lookup"><span data-stu-id="cc84e-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="cc84e-150"><strong>Nazwa</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="cc84e-151">Dostępna, gdy <strong>utworzenia nowego wystąpienia bazy danych SQL</strong> wybrano hello poprzedniego ekranu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="cc84e-152">Wprowadź toobe Nazwa bazy danych SQL, używane przez usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cc84e-153"><strong>Serwer</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="cc84e-154">Dostępna, gdy <strong>utworzenia nowego wystąpienia bazy danych SQL</strong> wybrano hello poprzedniego ekranu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="cc84e-155">Wybierz istniejący serwer bazy danych SQL lub utwórz nowy.</span><span class="sxs-lookup"><span data-stu-id="cc84e-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cc84e-156"><strong>Nazwa logowania do serwera</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="cc84e-157">Wprowadź nazwę użytkownika logowania hello.</span><span class="sxs-lookup"><span data-stu-id="cc84e-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cc84e-158"><strong>Hasło logowania do serwera</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="cc84e-159">Wprowadź hasło logowania hello.</span><span class="sxs-lookup"><span data-stu-id="cc84e-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="cc84e-160"><strong>Region</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="cc84e-161">Ustawienie dostępne, jeśli wybrano opcję <strong>Utwórz nowe wystąpienie bazy danych SQL</strong>.</span><span class="sxs-lookup"><span data-stu-id="cc84e-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="cc84e-162">Wybierz toohost regionu geograficznego hello bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="cc84e-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="cc84e-163">Wybierz hello znacznik wyboru toocomplete hello kreatora.</span><span class="sxs-lookup"><span data-stu-id="cc84e-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="cc84e-164">pojawi się ikona postępu Hello:</span><span class="sxs-lookup"><span data-stu-id="cc84e-164">hello progress icon appears:</span></span>  
![Ikona postępu zostanie wyświetlona po ukończeniu][ProgressComplete]

<span data-ttu-id="cc84e-166">Po zakończeniu hello Azure usługi BizTalk został utworzony i gotowa do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc84e-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="cc84e-167">Witaj domyślne ustawienia są wystarczające.</span><span class="sxs-lookup"><span data-stu-id="cc84e-167">hello default settings are sufficient.</span></span> <span data-ttu-id="cc84e-168">Ustawienia domyślne hello toochange, wybierz opcję **usługi BIZTALK SERVICES** w lewym okienku nawigacji hello, a następnie wybierz usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="cc84e-169">Dodatkowe ustawienia są wyświetlane na powitania [karty Pulpit nawigacyjny, Monitor i skali](biztalk-dashboard-monitor-scale-tabs.md) u góry hello.</span><span class="sxs-lookup"><span data-stu-id="cc84e-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="cc84e-170">W zależności od stanu hello hello usługi BizTalk ma niektórych operacji, które nie może zostać zakończona.</span><span class="sxs-lookup"><span data-stu-id="cc84e-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="cc84e-171">Lista te operacje, przejść za[wykresu stanu usługi BizTalk](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="cc84e-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="cc84e-172">Kroki po zainicjowaniu obsługi</span><span class="sxs-lookup"><span data-stu-id="cc84e-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="cc84e-173">Zainstaluj certyfikat hello na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="cc84e-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="cc84e-174">Dodanie certyfikatu gotowego do produkcji</span><span class="sxs-lookup"><span data-stu-id="cc84e-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="cc84e-175">Pobierz hello kontroli dostępu w przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="cc84e-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="cc84e-176"><a name="InstallCert"></a>Zainstaluj certyfikat hello na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="cc84e-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="cc84e-177">W ramach inicjowania obsługi usługi BizTalk zostaje utworzony certyfikat z podpisem własnym, skojarzony z subskrypcją usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="cc84e-178">Należy pobrać tego certyfikatu i zainstalować na komputerach, z których możesz wdrażania aplikacji usługi BizTalk lub wysyłać wiadomości tooa punktu końcowego usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="cc84e-179">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cc84e-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="cc84e-180">Wybierz **usługi BIZTALK SERVICES** w lewym okienku nawigacji hello, a następnie wybierz subskrypcję usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="cc84e-181">Wybierz hello **pulpitu nawigacyjnego** kartę.</span><span class="sxs-lookup"><span data-stu-id="cc84e-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="cc84e-182">Wybierz opcję **Pobierz certyfikat SSL**:</span><span class="sxs-lookup"><span data-stu-id="cc84e-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="cc84e-183">![Modyfikowanie certyfikatu SSL][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="cc84e-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="cc84e-184">Kliknij dwukrotnie certyfikat hello i uruchom za pośrednictwem hello kreatora tooinstall hello certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="cc84e-185">Upewnij się, że konieczne jest zainstalowanie certyfikatu hello w obszarze hello **zaufane główne urzędy certyfikacji** przechowywania.</span><span class="sxs-lookup"><span data-stu-id="cc84e-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="cc84e-186"><a name="AddCert"></a>Dodanie certyfikatu gotowego do produkcji</span><span class="sxs-lookup"><span data-stu-id="cc84e-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="cc84e-187">Witaj certyfikatu z podpisem własnym, który jest tworzony automatycznie podczas tworzenia usługi BizTalk Services jest przeznaczony do użytku w środowiskach programistycznych tylko.</span><span class="sxs-lookup"><span data-stu-id="cc84e-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="cc84e-188">Na potrzeby scenariuszy produkcyjnych zastąp go certyfikatem gotowym do produkcji.</span><span class="sxs-lookup"><span data-stu-id="cc84e-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="cc84e-189">Na powitania **pulpitu nawigacyjnego** wybierz opcję **certyfikat SSL aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="cc84e-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="cc84e-190">Przeglądaj tooyour prywatny certyfikatu SSL (*CertificateName*pfx) zawierającą nazwę usługi BizTalk, wprowadź hasło hello, a następnie kliknij znacznik wyboru hello.</span><span class="sxs-lookup"><span data-stu-id="cc84e-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="cc84e-191"><a name="ACS"></a>Pobierz hello kontroli dostępu w przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="cc84e-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="cc84e-192">Zaloguj się toohello [portalu Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cc84e-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="cc84e-193">Wybierz **usługi BIZTALK SERVICES** w lewym okienku nawigacji hello, a następnie wybierz usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="cc84e-194">Na pasku zadań hello, wybierz **informacje o połączeniu**:</span><span class="sxs-lookup"><span data-stu-id="cc84e-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="cc84e-195">![Wybieranie opcji Informacje o połączeniu][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="cc84e-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="cc84e-196">Skopiuj hello wartości kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="cc84e-197">Podczas wdrażania projektu usługi BizTalk w programie Visual Studio należy wprowadzić obszar nazw kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="cc84e-198">Witaj kontroli dostępu w przestrzeni nazw jest tworzony automatycznie dla usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="cc84e-199">można używać wartości kontroli dostępu Hello z dowolnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc84e-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="cc84e-200">Po utworzeniu usługi BizTalk Azure tej przestrzeni nazw kontroli dostępu określa hello uwierzytelniania z wdrożeniem usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="cc84e-201">Wybierz toochange hello subskrypcji lub zarządzania hello przestrzeni nazw, **usługi ACTIVE DIRECTORY** w hello w lewym okienku nawigacji, a następnie wybierz obszar nazw.</span><span class="sxs-lookup"><span data-stu-id="cc84e-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="cc84e-202">pasek zadań Hello listą dostępnych opcji.</span><span class="sxs-lookup"><span data-stu-id="cc84e-202">hello task bar lists your options.</span></span>

<span data-ttu-id="cc84e-203">Kliknięcie przycisku **Zarządzaj** otwiera hello portalu zarządzania kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="cc84e-204">W portalu zarządzania kontroli dostępu hello, hello używa usługi BizTalk **tożsamości usługi**:</span><span class="sxs-lookup"><span data-stu-id="cc84e-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="cc84e-205">![Tożsamości usługi ACS w hello portalu zarządzania kontroli dostępu][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="cc84e-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="cc84e-206">Witaj tożsamość usługi kontroli dostępu jest zestaw poświadczeń, które umożliwia aplikacji lub tooauthenticate klientów bezpośrednio z kontroli dostępu i otrzymujących token.</span><span class="sxs-lookup"><span data-stu-id="cc84e-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cc84e-207">Witaj usługi BizTalk używa **właściciela** hello domyślnej usługi tożsamości i hello **hasło** wartość.</span><span class="sxs-lookup"><span data-stu-id="cc84e-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="cc84e-208">Jeśli używasz wartość klucza symetrycznego hello zamiast hello wartość hasła hello następujący błąd może wystąpić.</span><span class="sxs-lookup"><span data-stu-id="cc84e-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="cc84e-209">*Nie można połączyć konto usługi zarządzania kontroli dostępu toohello z hello określone poświadczenia*</span><span class="sxs-lookup"><span data-stu-id="cc84e-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="cc84e-210">Niektóre wskazówki i zalecenia znajdują się w artykule [Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) (Zarządzanie obszarem nazw ACS).</span><span class="sxs-lookup"><span data-stu-id="cc84e-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="cc84e-211">Wyjaśniono wymagania</span><span class="sxs-lookup"><span data-stu-id="cc84e-211">Requirements explained</span></span>
<span data-ttu-id="cc84e-212">Te wymagania nie dotyczą toohello bezpłatna wersja.</span><span class="sxs-lookup"><span data-stu-id="cc84e-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="cc84e-213"><strong>Co jest potrzebne</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="cc84e-214"><strong>Do czego służy</strong></span><span class="sxs-lookup"><span data-stu-id="cc84e-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="cc84e-215">Subskrypcja platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cc84e-215">Azure subscription</span></span></td>
<td><span data-ttu-id="cc84e-216">Subskrypcja Hello Określa, kto Zaloguj toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cc84e-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="cc84e-217">Właściciel konta Hello tworzy subskrypcję hello w <a HREF="https://account.windowsazure.com/Subscriptions"> subskrypcji platformy Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="cc84e-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="cc84e-218">Witaj konto platformy Azure może mieć wiele subskrypcji i mogą być zarządzane przez każdy, kto jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="cc84e-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="cc84e-219">Na przykład z właścicielem konta Azure tworzy subskrypcję o nazwie <em>BizTalkServiceSubscription</em> i zapewnia hello Administratorzy BizTalk w obrębie firmy (na przykład ContosoBTSAdmins@live.com) dostęp toothis subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="cc84e-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="cc84e-220">W tym scenariuszu Administratorzy BizTalk hello Zaloguj toohello portalu Azure i ma pełny Administrator prawa tooall hello hostowanej usługi w subskrypcji hello, w tym usług BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="cc84e-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="cc84e-221">Administratorzy BizTalk Hello nie są hello posiadaczy konto platformy Azure i w związku z tym nie ma informacji dotyczących rozliczeń tooany dostępu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="cc84e-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Zarządzanie subskrypcjami i kont magazynu w hello portalu Azure</a> zawiera więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="cc84e-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="cc84e-223">Usługa Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="cc84e-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="cc84e-224">Przechowuje hello tabel, widoków i procedur składowanych używane przez usługi BizTalk, w tym dane śledzenia hello hello.</span><span class="sxs-lookup"><span data-stu-id="cc84e-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="cc84e-225">Podczas tworzenia usługi BizTalk można użyć istniejącego serwera Azure SQL Server, bazy danych SQL Azure lub automatycznie utworzyć nowy serwer bądź nową bazę danych.</span><span class="sxs-lookup"><span data-stu-id="cc84e-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="cc84e-226">automatycznie skonfigurowano Hello skalowania bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="cc84e-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="cc84e-227">Zazwyczaj Skala domyślna hello jest wystarczająca dla usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="cc84e-228">Zmiana skali hello ma wpływ na cennik.</span><span class="sxs-lookup"><span data-stu-id="cc84e-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="cc84e-229">Zobacz artykuł <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
 (Konta i rozliczenia w bazie danych SQL Azure)</span><span class="sxs-lookup"><span data-stu-id="cc84e-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="cc84e-230">
<strong>Uwagi</strong>
</span><span class="sxs-lookup"><span data-stu-id="cc84e-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="cc84e-231">Po utworzeniu nowego serwera Azure SQL Server i bazy danych usługi Azure zostaną automatycznie włączone.</span><span class="sxs-lookup"><span data-stu-id="cc84e-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="cc84e-232">Usługi BizTalk Hello wymaga usług Azure można włączyć.</span><span class="sxs-lookup"><span data-stu-id="cc84e-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="cc84e-233">Jeśli tworzysz nową bazę danych SQL Azure na istniejącym serwerze SQL Azure hello reguły zapory powitania serwera nie są zmieniane.</span><span class="sxs-lookup"><span data-stu-id="cc84e-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="cc84e-234">W związku z tym jest możliwe, innych usług Azure nie są dozwolone baz danych serwera toohello dostępu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="cc84e-235">Przestrzeń nazw kontroli dostępu Azure</span><span class="sxs-lookup"><span data-stu-id="cc84e-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="cc84e-236">Uwierzytelnia za pomocą usługi Azure BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="cc84e-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="cc84e-237">Podczas wdrażania projektu usługi BizTalk w programie Visual Studio należy wprowadzić obszar nazw kontroli dostępu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="cc84e-238">Witaj kontroli dostępu w przestrzeni nazw jest tworzony automatycznie podczas tworzenia usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="cc84e-239">Konto usługi Azure Storage</span><span class="sxs-lookup"><span data-stu-id="cc84e-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="cc84e-240">Zapewnia dostęp do tootables, obiekty BLOB i kolejki używane przez użytkownika usługi BizTalk toosave powitania po:</span><span class="sxs-lookup"><span data-stu-id="cc84e-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="cc84e-241">Ten monitor hello usługi BizTalk plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="cc84e-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="cc84e-242">monitorowanie danych wyjściowych Hello jest wyświetlany na powitania **monitorowanie** kartę w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="cc84e-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="cc84e-243">Podczas tworzenia X12 lub AS2 umowę pomiędzy partnerami, można włączyć właściwości wiadomości powitania Archiwizacja funkcji toostore.</span><span class="sxs-lookup"><span data-stu-id="cc84e-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="cc84e-244">Te dane są zapisywane w hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="cc84e-245">Podczas tworzenia usługi BizTalk można użyć istniejącego konta usługi Storage lub automatycznie utworzyć nowe.</span><span class="sxs-lookup"><span data-stu-id="cc84e-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="cc84e-246">Witaj domyślne ustawienia przechowywania są wystarczające dla usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="cc84e-247">Podczas tworzenia konta usługi Storage następuje automatyczne utworzenie klucza podstawowego i klucza pomocniczego.</span><span class="sxs-lookup"><span data-stu-id="cc84e-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="cc84e-248">Te klucze kontroli dostępu tooyour konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="cc84e-249">Usługi BizTalk Hello automatycznie używa hello klucza podstawowego.</span><span class="sxs-lookup"><span data-stu-id="cc84e-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="cc84e-250">Więcej informacji znajduje się w artykule <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a>.</span><span class="sxs-lookup"><span data-stu-id="cc84e-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="cc84e-251">Prywatny certyfikat SSL</span><span class="sxs-lookup"><span data-stu-id="cc84e-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="cc84e-252">Po utworzeniu usługi Azure BizTalk Services zostaje również utworzony adres URL HTTPS zawierający nazwę usługi BizTalk.</span><span class="sxs-lookup"><span data-stu-id="cc84e-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="cc84e-253">Ten adres URL jest automatycznie skonfigurowana toouse tylko do tworzenia certyfikatu z podpisem własnym.</span><span class="sxs-lookup"><span data-stu-id="cc84e-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="cc84e-254">Do produkcji potrzebny jest prywatny certyfikat SSL.</span><span class="sxs-lookup"><span data-stu-id="cc84e-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="cc84e-255">
<strong>Ważne informacje dotyczące certyfikatów SSL</strong>

</span><span class="sxs-lookup"><span data-stu-id="cc84e-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="cc84e-256">Data wygaśnięcia certyfikatu Hello musi być mniejsza niż 5 lat.</span><span class="sxs-lookup"><span data-stu-id="cc84e-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="cc84e-257">Wszystkie certyfikaty prywatne wymagają hasła.</span><span class="sxs-lookup"><span data-stu-id="cc84e-257">All private certificates require a password.</span></span> <span data-ttu-id="cc84e-258">Zapamiętaj to hasło i udostępnij je swoim administratorom.</span><span class="sxs-lookup"><span data-stu-id="cc84e-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="cc84e-259">Certyfikaty z podpisem własnym są używane w środowisku testowania/programowania.</span><span class="sxs-lookup"><span data-stu-id="cc84e-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="cc84e-260">Podczas korzystania z certyfikatów z podpisem własnym, zaimportuj hello certyfikatu tooyour osobistym magazynie certyfikatów i hello magazynu certyfikatów zaufanych głównych urzędów certyfikacji.</span><span class="sxs-lookup"><span data-stu-id="cc84e-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="cc84e-261">Podczas wysyłania urzędu certyfikacji tooyour żądania certyfikatu hello produkcji, należy podać hello następujące właściwości certyfikatu:</span><span class="sxs-lookup"><span data-stu-id="cc84e-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="cc84e-262"><strong>Ulepszone użycie klucza</strong>: usługa Azure BizTalk Services wymaga przynajmniej uwierzytelniania przez serwer.</span><span class="sxs-lookup"><span data-stu-id="cc84e-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="cc84e-263"><strong>Nazwa pospolita</strong>: Wprowadź hello pełną nazwę domeny (FQDN) adres URL usługi BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="cc84e-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="cc84e-264">Zobacz temat <a HREF="#CreateService">Create a BizTalk Service</a> (Tworzenie usługi BizTalk) w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="cc84e-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="cc84e-265">Po utworzeniu hello usługi BizTalk można dodać nowe lub inny certyfikat.</span><span class="sxs-lookup"><span data-stu-id="cc84e-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="cc84e-266">Połączenia hybrydowe</span><span class="sxs-lookup"><span data-stu-id="cc84e-266">Hybrid Connections</span></span>
<span data-ttu-id="cc84e-267">Podczas tworzenia usługi BizTalk Azure hello **połączeń hybrydowych** karta jest dostępna:</span><span class="sxs-lookup"><span data-stu-id="cc84e-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![Karta Połączenia hybrydowe][HybridConnectionTab]

<span data-ttu-id="cc84e-269">Połączenia hybrydowe są używane tooconnect Azure witryny sieci Web lub usługą Azure mobile Services tooany lokalnych zasobów, która używa portu TCP statycznego, takich jak SQL Server, MySQL, interfejsy API protokołu HTTP sieci Web, usług Mobile Services i większość niestandardowych usług sieci Web.</span><span class="sxs-lookup"><span data-stu-id="cc84e-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="cc84e-270">Połączenia hybrydowe i hello usługę BizTalk karty są różne.</span><span class="sxs-lookup"><span data-stu-id="cc84e-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="cc84e-271">Hello Usługa karty BizTalk jest używane tooconnect usług BizTalk Azure tooan lokalnego Linia biznesowych (LOB) systemu.</span><span class="sxs-lookup"><span data-stu-id="cc84e-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="cc84e-272">Zobacz [połączeń hybrydowych](integration-hybrid-connection-overview.md) toolearn więcej, w tym tworzenie i zarządzanie nimi połączeń hybrydowych było możliwe.</span><span class="sxs-lookup"><span data-stu-id="cc84e-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc84e-273">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cc84e-273">Next steps</span></span>
<span data-ttu-id="cc84e-274">Teraz, gdy jest tworzony usługi BizTalk, zapoznaj się z różnych hello [usługi BizTalk Services: karty Pulpit nawigacyjny, Monitor i skali](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="cc84e-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="cc84e-275">Usługa BizTalk jest gotowa dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cc84e-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="cc84e-276">toostart tworzenia aplikacji, przejdź do zbyt[usług BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="cc84e-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="cc84e-277">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="cc84e-277">See also</span></span>
* [<span data-ttu-id="cc84e-278">BizTalk Services: Editions Chart (Usługa BizTalk Services: zestawienie wersji)</span><span class="sxs-lookup"><span data-stu-id="cc84e-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="cc84e-279">BizTalk Services: State Chart (Usługa BizTalk Services: tabela stanów)</span><span class="sxs-lookup"><span data-stu-id="cc84e-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="cc84e-280">BizTalk Services: Backup and Restore (Usługa BizTalk Services: tworzenie kopii zapasowej i przywracanie)</span><span class="sxs-lookup"><span data-stu-id="cc84e-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="cc84e-281">BizTalk Services: Throttling (Usługa BizTalk Services: ograniczanie przepływności)</span><span class="sxs-lookup"><span data-stu-id="cc84e-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="cc84e-282">BizTalk Services: Issuer Name and Issuer Key (Usługa BizTalk Services: nazwa i klucz wydawcy)</span><span class="sxs-lookup"><span data-stu-id="cc84e-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="cc84e-283">Jak mogę uruchomić przy użyciu hello Azure zestawu SDK usługi BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="cc84e-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="cc84e-284">Połączenia hybrydowe</span><span class="sxs-lookup"><span data-stu-id="cc84e-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
