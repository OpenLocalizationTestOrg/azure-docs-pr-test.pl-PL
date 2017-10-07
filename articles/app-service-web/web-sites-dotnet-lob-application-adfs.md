---
title: "aaaCreate aplikacji Azure — biznesowych, z uwierzytelniania usług AD FS | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate w aplikacji biznesowych — w usłudze Azure App Service, który przeprowadza uwierzytelnianie z lokalnej usługi STS. Ten samouczek jest przeznaczony dla usług AD FS jako hello lokalnej usługi STS."
services: app-service\web
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: 0fa9f7a1-37bd-4d11-845f-aeff6fc9e4ca
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: cfd6f14837642fbf58ca5da9dee72db69cd5ab7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a><span data-ttu-id="ae4eb-104">Tworzenie aplikacji Azure — biznesowych uwierzytelniania usług AD FS</span><span class="sxs-lookup"><span data-stu-id="ae4eb-104">Create a line-of-business Azure app with AD FS authentication</span></span>
<span data-ttu-id="ae4eb-105">W tym artykule opisano sposób toocreate ASP.NET MVC — biznesowych aplikacji w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) przy użyciu lokalnej [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) jako hello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-105">This article shows you how toocreate an ASP.NET MVC line-of-business application in [Azure App Service](../app-service/app-service-value-prop-what-is.md) using an on-premises [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) as hello identity provider.</span></span> <span data-ttu-id="ae4eb-106">W tym scenariuszu można pracować, podczas ma toocreate aplikacji biznesowych — w usłudze Azure App Service, ale Twoja organizacja wymaga katalogu toobe dane przechowywane na miejscu.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-106">This scenario can work when you want toocreate line-of-business applications in Azure App Service but your organization requires directory data toobe stored on-site.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4eb-107">Omówienie hello opcje uwierzytelniania i autoryzacji różnych organizacji dla usługi Azure App Service, zobacz [Uwierzytelnij z lokalnej usługi Active Directory w aplikacji Azure](web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-107">For an overview of hello different enterprise authentication and authorization options for Azure App Service, see [Authenticate with on-premises Active Directory in your Azure app](web-sites-authentication-authorization.md).</span></span>
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="ae4eb-108">Zostanie utworzona</span><span class="sxs-lookup"><span data-stu-id="ae4eb-108">What you will build</span></span>
<span data-ttu-id="ae4eb-109">Utworzysz podstawowej aplikacji ASP.NET w aplikacji sieci Web usługi aplikacji Azure z hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-109">You will build a basic ASP.NET application in Azure App Service Web Apps with hello following features:</span></span>

* <span data-ttu-id="ae4eb-110">Uwierzytelnia użytkowników w usługach AD FS</span><span class="sxs-lookup"><span data-stu-id="ae4eb-110">Authenticates users against AD FS</span></span>
* <span data-ttu-id="ae4eb-111">Używa `[Authorize]` tooauthorize użytkownicy dla różnych działań</span><span class="sxs-lookup"><span data-stu-id="ae4eb-111">Uses `[Authorize]` tooauthorize users for different actions</span></span>
* <span data-ttu-id="ae4eb-112">Statycznie dla debugowania w programie Visual Studio i publikowania aplikacji sieci Web usługi tooApp (Konfigurowanie raz, debugowania i opublikować w dowolnym momencie)</span><span class="sxs-lookup"><span data-stu-id="ae4eb-112">Static configuration for both debugging in Visual Studio and publishing tooApp Service Web Apps (configure once, debug and publish anytime)</span></span>  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="ae4eb-113">Co jest potrzebne</span><span class="sxs-lookup"><span data-stu-id="ae4eb-113">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="ae4eb-114">Po toocomplete muszą hello w tym samouczku:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-114">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="ae4eb-115">Lokalnego wdrożenia usług AD FS (end-to-end przewodnik laboratorium testowego hello używane w tym samouczku, zobacz [laboratorium testowego: STS autonomiczny z usługami AD FS w maszynie Wirtualnej platformy Azure (dla testu tylko)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span><span class="sxs-lookup"><span data-stu-id="ae4eb-115">An on-premises AD FS deployment (for an end-to-end walkthrough of hello test lab used in this tutorial, see [Test Lab: Standalone STS with AD FS in Azure VM (for test only)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))</span></span>
* <span data-ttu-id="ae4eb-116">Uprawnienia toocreate zaufania jednostek uzależnionych w zarządzanie usługami AD FS</span><span class="sxs-lookup"><span data-stu-id="ae4eb-116">Permissions toocreate relying party trusts in AD FS Management</span></span>
* <span data-ttu-id="ae4eb-117">Visual Studio 2013 Update 4 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="ae4eb-117">Visual Studio 2013 Update 4 or later</span></span>
* <span data-ttu-id="ae4eb-118">[Zestaw Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) lub nowszy</span><span class="sxs-lookup"><span data-stu-id="ae4eb-118">[Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) or later</span></span>

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a><span data-ttu-id="ae4eb-119">Użyj przykładowej aplikacji biznesowych z szablonu</span><span class="sxs-lookup"><span data-stu-id="ae4eb-119">Use sample application for line-of-business template</span></span>
<span data-ttu-id="ae4eb-120">Witaj przykładowej aplikacji w tym samouczku [aplikacji sieci Web-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), jest tworzony przez zespół usługi Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-120">hello sample application in this tutorial, [WebApp-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), is created by hello Azure Active Directory team.</span></span> <span data-ttu-id="ae4eb-121">Ponieważ usługi AD FS obsługuje usługi WS-Federation, można użyć jej jako szablonu toocreate--aplikacji biznesowych z łatwością.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-121">Since AD FS supports WS-Federation, you can use it as a template toocreate line-of-business applications with ease.</span></span> <span data-ttu-id="ae4eb-122">Ma hello następujące funkcje:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-122">It has hello following features:</span></span>

* <span data-ttu-id="ae4eb-123">Używa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate z lokalnego wdrożenia usług AD FS</span><span class="sxs-lookup"><span data-stu-id="ae4eb-123">Uses [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate with an on-premises AD FS deployment</span></span>
* <span data-ttu-id="ae4eb-124">Funkcjonalność logowania się i wylogowania</span><span class="sxs-lookup"><span data-stu-id="ae4eb-124">Sign-in and sign-out functionality</span></span>
* <span data-ttu-id="ae4eb-125">Używa [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (zamiast Windows Identity Foundation), który jest hello przyszłych programu ASP.NET i tooset znacznie prostsza do uwierzytelniania i autoryzacji niż WIF</span><span class="sxs-lookup"><span data-stu-id="ae4eb-125">Uses [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (instead of Windows Identity Foundation), which is hello future of ASP.NET and much simpler tooset up for authentication and authorization than WIF</span></span>

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a><span data-ttu-id="ae4eb-126">Konfigurowanie hello przykładowej aplikacji</span><span class="sxs-lookup"><span data-stu-id="ae4eb-126">Set up hello sample application</span></span>
1. <span data-ttu-id="ae4eb-127">Klonuj lub pobrać hello przykładowe rozwiązanie [aplikacji sieci Web-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour katalogu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-127">Clone or download hello sample solution at [WebApp-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour local directory.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ae4eb-128">Witaj instrukcje [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) przedstawia sposób tooset się hello aplikację w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-128">hello instructions at [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) show you how tooset up hello application with Azure Active Directory.</span></span> <span data-ttu-id="ae4eb-129">Jednak w tym samouczku, skonfigurować ją z usługami AD FS, dlatego zamiast tego należy wykonać kroki hello tutaj.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-129">But in this tutorial, you set it up with AD FS, so follow hello steps here instead.</span></span>
   > 
   > 
2. <span data-ttu-id="ae4eb-130">Otwórz rozwiązanie hello, a następnie otwórz Controllers\AccountController.cs w hello **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-130">Open hello solution, and then open Controllers\AccountController.cs in hello **Solution Explorer**.</span></span>
   
   <span data-ttu-id="ae4eb-131">Zobaczysz, że kod powitania po prostu wystawia użytkownika hello tooauthenticate żądania uwierzytelniania za pomocą protokołu WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-131">You will see that hello code simply issues an authentication challenge tooauthenticate hello user using WS-Federation.</span></span> <span data-ttu-id="ae4eb-132">Wszystkie uwierzytelniania jest skonfigurowany w App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-132">All authentication is configured in App_Start\Startup.Auth.cs.</span></span>
3. <span data-ttu-id="ae4eb-133">Otwórz App_Start\Startup.Auth.cs.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-133">Open App_Start\Startup.Auth.cs.</span></span> <span data-ttu-id="ae4eb-134">W hello `ConfigureAuth` metody, linia hello Uwaga:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-134">In hello `ConfigureAuth` method, note hello line:</span></span>
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   <span data-ttu-id="ae4eb-135">Witaj świecie OWIN ta Wstawka kodu jest w rzeczywistości hello systemu od zera, minimalna należy tooconfigure WS-Federation uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-135">In hello OWIN world, this snippet is really hello bare minimum you need tooconfigure WS-Federation authentication.</span></span> <span data-ttu-id="ae4eb-136">Jest znacznie łatwiejsze i bardziej elegancki niż WIF, gdzie Web.config jest wprowadzonym za pomocą XML na całym hello miejsce.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-136">It is much simpler and more elegant than WIF, where Web.config is injected with XML all over hello place.</span></span> <span data-ttu-id="ae4eb-137">Witaj informacje potrzebne jest hello uzależnionej (RP) tylko identyfikator i hello adres URL pliku metadanych usługi AD FS.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-137">hello only information you need is hello relying party's (RP) identifier and hello URL of your AD FS service's metadata file.</span></span> <span data-ttu-id="ae4eb-138">Oto przykład:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-138">Here's an example:</span></span>
   
   * <span data-ttu-id="ae4eb-139">Identyfikator planu odzyskiwania:`https://contoso.com/MyLOBApp`</span><span class="sxs-lookup"><span data-stu-id="ae4eb-139">RP identifier: `https://contoso.com/MyLOBApp`</span></span>
   * <span data-ttu-id="ae4eb-140">Adres metadanych:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span><span class="sxs-lookup"><span data-stu-id="ae4eb-140">Metadata address: `http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`</span></span>
4. <span data-ttu-id="ae4eb-141">W App_Start\Startup.Auth.cs Zmień następujące definicje statyczny ciąg hello:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-141">In App_Start\Startup.Auth.cs, change hello following static string definitions:</span></span>  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. <span data-ttu-id="ae4eb-142">Teraz wprowadzić hello odpowiednie zmiany w pliku Web.config. Otwórz plik Web.config hello i zmodyfikuj następujące ustawienia aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-142">Now, make hello corresponding changes in Web.config. Open hello Web.config and modify hello following app settings:</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="webpages:Version" value="3.0.0.0" /&gt;
   &lt;add key="webpages:Enabled" value="false" /&gt;
   &lt;add key="ClientValidationEnabled" value="true" /&gt;
   &lt;add key="UnobtrusiveJavaScriptEnabled" value="true" /&gt;
   <mark><del>&lt;add key="ida:Wtrealm" value="[Enter hello App ID URI of WebApp-WSFederation-DotNet https://contoso.onmicrosoft.com/WebApp-WSFederation-DotNet]" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:AADInstance" value="https://login.microsoftonline.com" /&gt;</del></mark>
   <mark><del>&lt;add key="ida:Tenant" value="[Enter tenant name, e.g. contoso.onmicrosoft.com]" /&gt;</del></mark>
   <mark>&lt;add key="ida:RPIdentifier" value="[Enter hello relying party identifier as configured in AD FS, e.g. https://localhost:44320/]" /&gt;</mark>
   <mark>&lt;add key="ida:ADFS" value="[Enter hello FQDN of AD FS service, e.g. adfs.contoso.com]" /&gt;</mark>
   
   &lt;/appSettings&gt;
   </pre>
   
   <span data-ttu-id="ae4eb-143">Wypełnij hello wartości klucza w zależności od używanego środowiska odpowiednich.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-143">Fill in hello key values based on your respective environment.</span></span>
6. <span data-ttu-id="ae4eb-144">Tworzenie toomake aplikacji hello się, że nie ma żadnych błędów.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-144">Build hello application toomake sure there are no errors.</span></span>

<span data-ttu-id="ae4eb-145">To już wszystko.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-145">That's it.</span></span> <span data-ttu-id="ae4eb-146">Teraz hello Przykładowa aplikacja jest gotowa toowork z usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-146">Now hello sample application is ready toowork with AD FS.</span></span> <span data-ttu-id="ae4eb-147">Nadal potrzebujesz tooconfigure zaufania planu odzyskiwania z tej aplikacji w usługach AD FS później.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-147">You still need tooconfigure an RP trust with this application in AD FS later.</span></span>

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a><span data-ttu-id="ae4eb-148">Wdrażanie hello przykładowej aplikacji tooAzure aplikacji usługi sieci Web aplikacji</span><span class="sxs-lookup"><span data-stu-id="ae4eb-148">Deploy hello sample application tooAzure App Service Web Apps</span></span>
<span data-ttu-id="ae4eb-149">W tym miejscu publikowania aplikacji sieci web tooa aplikacji hello w aplikacji usługi sieci Web aplikacji przy jednoczesnym zachowaniu hello debugowania środowiska.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-149">Here, you publish hello application tooa web app in App Service Web Apps while preserving hello debug environment.</span></span> <span data-ttu-id="ae4eb-150">Należy pamiętać, że chcesz zacząć aplikacji hello toopublish przed ma zaufanie planu odzyskiwania z usługami AD FS, więc uwierzytelniania nadal nie działa jeszcze.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-150">Note that you're going toopublish hello application before it has an RP trust with AD FS, so authentication still doesn't work yet.</span></span> <span data-ttu-id="ae4eb-151">Jednak jeśli chcesz go teraz program może URL aplikacji sieci web hello później używania tooconfigure hello RP zaufania.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-151">However, if you do it now you can have hello web app URL that you can use tooconfigure hello RP trust later.</span></span>

1. <span data-ttu-id="ae4eb-152">Kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-152">Right-click your project and select **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. <span data-ttu-id="ae4eb-153">Wybierz **usługi Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-153">Select **Microsoft Azure App Service**.</span></span>
3. <span data-ttu-id="ae4eb-154">Jeżeli nie zarejestrujesz w tooAzure, kliknij przycisk **logowania** używanie konta Microsoft hello toosign Twojej subskrypcji platformy Azure w.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-154">If you haven't signed in tooAzure, click **Sign In** and use hello Microsoft account for your Azure subscription toosign in.</span></span>
4. <span data-ttu-id="ae4eb-155">Po zalogowaniu kliknij **nowy** toocreate aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-155">Once signed in, click **New** toocreate a web app.</span></span>
5. <span data-ttu-id="ae4eb-156">Wypełnij wszystkie wymagane pola.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-156">Fill in all required fields.</span></span> <span data-ttu-id="ae4eb-157">Zamierzasz tooconnect tooon lokalne dane później, dlatego nie należy tworzyć bazy danych dla tej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-157">You are going tooconnect tooon-premises data later, so don't create a database for this web app.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. <span data-ttu-id="ae4eb-158">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-158">Click **Create**.</span></span> <span data-ttu-id="ae4eb-159">Po utworzeniu aplikacji sieci web hello okna dialogowego publikowanie w sieci Web hello jest otwarty.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-159">Once hello web app is created, hello Publish Web dialog is opened.</span></span>
7. <span data-ttu-id="ae4eb-160">W **docelowy adres URL**, zmień **http** za**https**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-160">In **Destination URL**, change **http** too**https**.</span></span> <span data-ttu-id="ae4eb-161">Skopiuj hello cały adres URL tooa Edytor tekstu do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-161">Copy hello entire URL tooa text editor for later use.</span></span> <span data-ttu-id="ae4eb-162">Następnie kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-162">Then, click **Publish**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. <span data-ttu-id="ae4eb-163">W programie Visual Studio Otwórz **Web.Release.config** w projekcie.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-163">In Visual Studio, open **Web.Release.config** in your project.</span></span> <span data-ttu-id="ae4eb-164">Wstaw powitania po XML na powitania `<configuration>` tagu i Zastąp wartości klucza hello adres URL aplikacji sieci web publikowania.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-164">Insert hello following XML into hello `<configuration>` tag, and replace hello key value with your publish web app's URL.</span></span>  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

<span data-ttu-id="ae4eb-165">Gdy wszystko będzie gotowe, ma dwa identyfikatory RP skonfigurowane w projekcie, jeden dla danego środowiska debugowania w programie Visual Studio i jeden dla hello opublikowane aplikacji sieci web na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-165">When you're done, you have two RP identifiers configured in your project, one for your debug environment in Visual Studio, and one for hello published web app in Azure.</span></span> <span data-ttu-id="ae4eb-166">Zaufanie RP zostanie skonfigurowany dla każdego z dwóch środowisk hello w usługach AD FS.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-166">You will set up an RP trust for each of hello two environments in AD FS.</span></span> <span data-ttu-id="ae4eb-167">Podczas debugowania, ustawienia aplikacji hello w pliku Web.config są używane toomake Twojego **debugowania** konfiguracji pracy z usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-167">During debugging, hello app settings in Web.config are used toomake your **Debug** configuration work with AD FS.</span></span> <span data-ttu-id="ae4eb-168">Jeśli jest publikowany (domyślnie hello **wersji** konfiguracji został opublikowany), przekazaniu przekształcone Web.config zawiera zmiany w ustawieniach aplikacji hello w Web.Release.config.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-168">When it's published (by default, hello **Release** configuration is published), a transformed Web.config is uploaded that incorporates hello app setting changes in Web.Release.config.</span></span>

<span data-ttu-id="ae4eb-169">Jeśli chcesz tooattach hello opublikowana aplikacja sieci web debugera Azure toohello (tj. musisz przekazać symboli debugowania kodu w hello opublikowana aplikacja sieci web), można utworzyć klonu hello debugowania konfiguracji platformy Azure, debugowanie, ale z własnego niestandardowego pliku Web.config przekształcenie ( np. Web.AzureDebug.config) używający ustawień aplikacji hello z Web.Release.config. Dzięki temu można toomaintain konfiguracji statycznej hello różnych środowiskach.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-169">If you want tooattach hello published web app in Azure toohello debugger (i.e. you must upload debug symbols of your code in hello published web app), you can create a clone of hello Debug configuration for Azure debugging, but with its own custom Web.config transform (e.g. Web.AzureDebug.config) that uses hello app settings from Web.Release.config. This allows you toomaintain a static configuration across hello different environments.</span></span>

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a><span data-ttu-id="ae4eb-170">Konfigurowanie relacji zaufania w zarządzanie usługami AD FS</span><span class="sxs-lookup"><span data-stu-id="ae4eb-170">Configure relying party trusts in AD FS Management</span></span>
<span data-ttu-id="ae4eb-171">Teraz należy tooconfigure zaufania RP do zarządzania usługami AD FS można było użyć przykładowej aplikacji i faktycznie uwierzytelniania za pomocą usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-171">Now you need tooconfigure an RP trust in AD FS Management before you can use your sample application and actually authenticate with AD FS.</span></span> <span data-ttu-id="ae4eb-172">Konieczne będzie tooset się dwa oddzielne zaufania planu odzyskiwania, jeden dla danego środowiska debugowania i jeden dla aplikacji opublikowanych w sieci web.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-172">You will need tooset up two separate RP trusts, one for your debug environment and one for your published web app.</span></span>

> [!NOTE]
> <span data-ttu-id="ae4eb-173">Upewnij się, czy Powtórz hello następujące kroki dla obu tych środowisk.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-173">Make sure that you repeat hello following steps for both of your environments.</span></span>
> 
> 

1. <span data-ttu-id="ae4eb-174">Na serwerze usług AD FS Zaloguj się przy użyciu poświadczeń, które mają management rights tooAD FS.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-174">On your AD FS server, log in with credentials that have management rights tooAD FS.</span></span>
2. <span data-ttu-id="ae4eb-175">Otwórz przystawkę zarządzania usługami AD FS.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-175">Open AD FS Management.</span></span> <span data-ttu-id="ae4eb-176">Kliknij prawym przyciskiem myszy **AD FS\Trusted Relationships\Relying uzależnionych** i wybierz **dodać zaufanie jednostki uzależnionej**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-176">Right-click **AD FS\Trusted Relationships\Relying Party Trusts** and select **Add Relying Party Trust**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. <span data-ttu-id="ae4eb-177">W hello **wybierz źródło danych** wybierz **ręcznie wprowadź dane dotyczące jednostki uzależnionej hello**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-177">In hello **Select Data Source** page, select **Enter data about hello relying party manually**.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. <span data-ttu-id="ae4eb-178">W hello **Określanie nazwy wyświetlanej** , wpisz nazwę wyświetlaną dla aplikacji hello i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-178">In hello **Specify Display Name** page, type a display name for hello application and click **Next**.</span></span>
5. <span data-ttu-id="ae4eb-179">W hello **wybierz protokół** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-179">In hello **Choose Protocol** page, click **Next**.</span></span>
6. <span data-ttu-id="ae4eb-180">W hello **Konfigurowanie certyfikatu** kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-180">In hello **Configure Certificate** page, click **Next**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ae4eb-181">Ponieważ powinien być używany protokół HTTPS już, zaszyfrowanych tokenów są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-181">Since you should be using HTTPS already, encrypted tokens are optional.</span></span> <span data-ttu-id="ae4eb-182">Jeśli na pewno tooencrypt tokenów z usług AD FS na tej stronie, musisz również dodać logikę odszyfrowywania tokenu w kodzie.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-182">If you really want tooencrypt tokens from AD FS on this page, you must also add token-decrypting logic in your code.</span></span> <span data-ttu-id="ae4eb-183">Aby uzyskać więcej informacji, zobacz [ręczne konfigurowanie oprogramowania pośredniczącego OWIN WS-Federation i akceptowanie szyfrowane tokenów](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-183">For more information, see [Manually configuring OWIN WS-Federation middleware and accepting encrypted tokens](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).</span></span>
   > 
   > 
7. <span data-ttu-id="ae4eb-184">Przed przejściem do następnego kroku hello należy jednej informacji z projektu programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-184">Before you move onto hello next step, you need one piece of information from your Visual Studio project.</span></span> <span data-ttu-id="ae4eb-185">We właściwościach projektu hello, należy zwrócić uwagę hello **adres URL protokołu SSL** aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-185">In hello project properties, note hello **SSL URL** of hello application.</span></span> 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. <span data-ttu-id="ae4eb-186">Zarządzanie usługami AD FS, w hello w **Konfigurowanie adresu URL** strony hello **jednostki uzależnionej strony Kreatora dodawania relacji zaufania**, wybierz pozycję **Włącz obsługę protokołu WS-Federation Passive hello** i Wpisz hello SSL adres URL projektu programu Visual Studio, zanotowaną w poprzednim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-186">Back in AD FS Management, in hello **Configure URL** page of hello **Add Relying Party Trust Wizard**, select **Enable support for hello WS-Federation Passive protocol** and type in hello SSL URL of your Visual Studio project that you noted in hello previous step.</span></span> <span data-ttu-id="ae4eb-187">Następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-187">Then, click **Next**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > <span data-ttu-id="ae4eb-188">Adres URL określa, gdzie toosend powitania klienta po uwierzytelnieniu zakończy się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-188">URL specifies where toosend hello client after authentication succeeds.</span></span> <span data-ttu-id="ae4eb-189">W środowisku debugowania hello powinna być <code>https://localhost:&lt;port&gt;/</code>.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-189">For hello debug environment, it should be <code>https://localhost:&lt;port&gt;/</code>.</span></span> <span data-ttu-id="ae4eb-190">Dla hello opublikowana aplikacja sieci web należy go adres URL aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-190">For hello published web app, it should be hello web app URL.</span></span>
   > 
   > 
9. <span data-ttu-id="ae4eb-191">W hello **skonfiguruj identyfikatory** , sprawdź, czy projekt SSL adres URL jest już wyświetlane i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-191">In hello **Configure Identifiers** page, verify that your project SSL URL is already listed and click **Next**.</span></span> <span data-ttu-id="ae4eb-192">Kliknij przycisk **dalej** wszystkie hello sposób toohello koniec hello kreatora bez ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-192">Click **Next** all hello way toohello end of hello wizard with default selections.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ae4eb-193">App_Start\Startup.Auth.cs projektu programu Visual Studio, ten identyfikator jest dopasowywana wartość hello <code>WsFederationAuthenticationOptions.Wtrealm</code> podczas uwierzytelniania federacyjnego.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-193">In App_Start\Startup.Auth.cs of your Visual Studio project, this identifier is matched against hello value of <code>WsFederationAuthenticationOptions.Wtrealm</code> during federated authentication.</span></span> <span data-ttu-id="ae4eb-194">Domyślnie adres URL aplikacji hello z poprzedniego kroku hello jest dodawany jako identyfikator planu odzyskiwania.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-194">By default, hello application's URL from hello previous step is added as an RP identifier.</span></span>
   > 
   > 
10. <span data-ttu-id="ae4eb-195">Konfigurowanie w usługach AD FS hello RP aplikacji dla projektu zostało zakończone.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-195">You have now finished configuring hello RP application for your project in AD FS.</span></span> <span data-ttu-id="ae4eb-196">Następnie należy skonfigurować ten toosend aplikacji hello oświadczenia wymagane przez aplikację.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-196">Next, you configure this application toosend hello claims needed by your application.</span></span> <span data-ttu-id="ae4eb-197">Witaj **Edycja reguł oświadczeń** okna dialogowego jest domyślnie otwierany automatycznie na końcu hello hello kreatora, aby natychmiast rozpocząć.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-197">hello **Edit Claim Rules** dialog is opened by default for you at hello end of hello wizard so you can start immediately.</span></span> <span data-ttu-id="ae4eb-198">Skonfigurujmy hello co najmniej następujących oświadczeń (ze schematami w nawiasach):</span><span class="sxs-lookup"><span data-stu-id="ae4eb-198">Let's configure at least hello following claims (with schemas in parentheses):</span></span>
    
    * <span data-ttu-id="ae4eb-199">Nazwa (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) — używane przez program ASP.NET toohydrate `User.Identity.Name`.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-199">Name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) - used by ASP.NET toohydrate `User.Identity.Name`.</span></span>
    * <span data-ttu-id="ae4eb-200">Użytkownika nazwy głównej (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - używany toouniquely identyfikowania użytkowników w organizacji hello.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-200">User principal name (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - used toouniquely identify users in hello organization.</span></span>
    * <span data-ttu-id="ae4eb-201">Członkostwa w grupach jako role (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) — może być używany z `[Authorize(Roles="role1, role2,...")]` tooauthorize decoration kontrolerów/akcji.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-201">Group memberships as roles (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) - can be used with `[Authorize(Roles="role1, role2,...")]` decoration tooauthorize controllers/actions.</span></span> <span data-ttu-id="ae4eb-202">W rzeczywistości to rozwiązanie może nie być hello większości wydajności do autoryzacji ról.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-202">In reality, this approach may not be hello most performant for role authorization.</span></span> <span data-ttu-id="ae4eb-203">Użytkownicy AD należą toohundreds grup zabezpieczeń, staje się setki oświadczeń roli z tokenu SAML hello.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-203">If your AD users belong toohundreds of security groups, they become hundreds of role claims in hello SAML token.</span></span> <span data-ttu-id="ae4eb-204">Informacje o innym podejściu jest toosend jedną rolę warunkowo oświadczeń w zależności od użytkownika hello członkostwa w określonej grupie.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-204">An alternative approach is toosend a single role claim conditionally depending on hello user's membership in a particular group.</span></span> <span data-ttu-id="ae4eb-205">Jednak firma Microsoft będzie Zachowaj prostotę w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-205">However, we'll keep it simple for this tutorial.</span></span>
    * <span data-ttu-id="ae4eb-206">Nazwa Identyfikatora (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) — może służyć do weryfikacji zabezpieczający przed sfałszowaniem.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-206">Name ID (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) - can be used for anti-forgery validation.</span></span> <span data-ttu-id="ae4eb-207">Aby uzyskać więcej informacji na temat działania toomake go z weryfikacją zabezpieczający przed sfałszowaniem, zobacz hello **Dodawanie funkcji z biznesowych** sekcji [tworzenie aplikacji Azure — biznesowych przy użyciu uwierzytelniania usługi Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-207">For more information on how toomake it work with anti-forgery validation, see hello **Add line-of-business functionality** section of [Create a line-of-business Azure app with Azure Active Directory authentication](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ae4eb-208">Witaj oświadczeń typów konieczność tooconfigure aplikacji zależy od potrzeb aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-208">hello claim types you need tooconfigure for your application is determined by your application's needs.</span></span> <span data-ttu-id="ae4eb-209">Witaj lista oświadczeń obsługiwane przez aplikacje usługi Azure Active Directory (tzn. RP zaufania), na przykład, zobacz [obsługiwany Token i typy oświadczeń](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-209">For hello list of claims supported by Azure Active Directory applications (i.e. RP trusts), for example, see [Supported Token and Claim Types](http://msdn.microsoft.com/library/azure/dn195587.aspx).</span></span>
    > 
    > 
11. <span data-ttu-id="ae4eb-210">W oknie dialogowym Edycja reguł oświadczeń powitania kliknij **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-210">In hello Edit Claim Rules dialog, click **Add Rule**.</span></span>
12. <span data-ttu-id="ae4eb-211">Skonfigurować oświadczenia nazwy UPN i roli hello, jak pokazano w hello zrzut ekranu, a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-211">Configure hello name, UPN, and role claims as shown in hello screenshot and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    <span data-ttu-id="ae4eb-212">Następnie należy utworzyć przejściowej nazwę Identyfikatora oświadczenia, wykonując kroki hello przedstawiona w [nazwy identyfikatorów potwierdzenia SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-212">Next, you create a transient name ID claim using hello steps demonstrated in [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
13. <span data-ttu-id="ae4eb-213">Kliknij przycisk **Dodaj regułę** ponownie.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-213">Click **Add Rule** again.</span></span>
14. <span data-ttu-id="ae4eb-214">Wybierz **wysyłanie oświadczeń przy użyciu reguły niestandardowej** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-214">Select **Send Claims Using a Custom Rule** and click **Next**.</span></span>
15. <span data-ttu-id="ae4eb-215">Wklej hello następujące reguły języka na powitania **reguły niestandardowej** okno, nazwa reguły hello **na identyfikator sesji** i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-215">Paste hello following rule language into hello **Custom rule** box, name hello rule **Per Session Identifier** and click **Finish**.</span></span>  
    
    <pre class="prettyprint">
    c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"] &amp;&amp;
    c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationinstant"]
     => add(
         store = "_OpaqueIdStore",
         types = ("<mark>http://contoso.com/internal/sessionid</mark>"),
         query = "{0};{1};{2};{3};{4}",
         param = "useEntropy",
         param = c1.Value,
         param = c1.OriginalIssuer,
         param = "",
         param = c2.Value);
    </pre>
    
    <span data-ttu-id="ae4eb-216">Niestandardowe reguły powinna wyglądać tego zrzutu ekranu:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-216">Your custom rule should look like this screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. <span data-ttu-id="ae4eb-217">Kliknij przycisk **Dodaj regułę** ponownie.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-217">Click **Add Rule** again.</span></span>
17. <span data-ttu-id="ae4eb-218">Wybierz **Przekształcanie oświadczenia przychodzącego** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-218">Select **Transform an Incoming Claim** and click **Next**.</span></span>
18. <span data-ttu-id="ae4eb-219">Skonfiguruj regułę hello, jak pokazano na zrzucie ekranu pokazano hello (przy użyciu typu oświadczenia hello utworzone w regule niestandardowej hello), a następnie kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-219">Configure hello rule as shown in hello screenshot (using hello claim type you created in hello custom rule) and click **Finish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    <span data-ttu-id="ae4eb-220">Aby uzyskać szczegółowe informacje dotyczące kroków hello hello przejściowej oświadczenia Identyfikatora nazwy, zobacz [nazwy identyfikatorów potwierdzenia SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-220">For detailed information on hello steps for hello transient Name ID claim, see [Name Identifiers in SAML assertions](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).</span></span>
19. <span data-ttu-id="ae4eb-221">Kliknij przycisk **Zastosuj** w hello **Edycja reguł oświadczeń** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-221">Click **Apply** in hello **Edit Claim Rules** dialog.</span></span> <span data-ttu-id="ae4eb-222">Powinna ona wyglądać tak jak powitania po zrzut ekranu:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-222">It should now look like hello following screenshot:</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > <span data-ttu-id="ae4eb-223">Ponownie upewnij się, powtórz te kroki dla debugowania środowiska i opublikowana aplikacja sieci web.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-223">Again, make sure that you repeat these steps for both your debug environment and published web app.</span></span>
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a><span data-ttu-id="ae4eb-224">Uwierzytelnianie Sfederowane testu dla aplikacji</span><span class="sxs-lookup"><span data-stu-id="ae4eb-224">Test federated authentication for your application</span></span>
<span data-ttu-id="ae4eb-225">Możesz są gotowe tootest aplikacji logiki uwierzytelniania dla usług AD FS.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-225">You are ready tootest your application's authentication logic against AD FS.</span></span> <span data-ttu-id="ae4eb-226">W moich środowiska laboratoryjnego usług AD FS masz użytkownika testowego, w której należy grupa testowa tooa w usłudze Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-226">In my AD FS lab environment, I have a test user that belongs tooa test group in Active Directory (AD).</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

<span data-ttu-id="ae4eb-227">Uwierzytelnianie tootest w debugerze hello, wystarczy toodo teraz jest typu `F5`.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-227">tootest authentication in hello debugger, all you need toodo now is type `F5`.</span></span> <span data-ttu-id="ae4eb-228">Jeśli chcesz tootest uwierzytelniania w hello opublikowana aplikacja sieci web, przejdź toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-228">If you want tootest authentication in hello published web app, navigate toohello URL.</span></span>

<span data-ttu-id="ae4eb-229">Po załadowaniu hello aplikacji sieci web, kliknij przycisk **logowania**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-229">After hello web application loads, click **Sign In**.</span></span> <span data-ttu-id="ae4eb-230">Należy teraz pobrać albo okna dialogowego lub hello logowania strony logowania obsługiwanych przez usługi AD FS, w zależności od metody uwierzytelniania hello wybranej przez usługi AD FS.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-230">You should now get either a login dialog or hello login page served by AD FS, depending on hello authentication method chosen by AD FS.</span></span> <span data-ttu-id="ae4eb-231">Oto, co pojawia się w programie Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-231">Here's what I get in Internet Explorer 11.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

<span data-ttu-id="ae4eb-232">Po zalogowaniu użytkownika w domenie hello AD hello AD FS wdrożenia powinna zostać wyświetlona strona główna hello ponownie, podając **Hello, <User Name>!**</span><span class="sxs-lookup"><span data-stu-id="ae4eb-232">Once you log in with a user in hello AD domain of hello AD FS deployment, you should now see hello homepage again with **Hello, <User Name>!**</span></span> <span data-ttu-id="ae4eb-233">w hello rogu.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-233">in hello corner.</span></span> <span data-ttu-id="ae4eb-234">Oto, co pojawia się.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-234">Here's what I get.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

<span data-ttu-id="ae4eb-235">Do tej pory zostały zakończone powodzeniem w następujące sposoby hello:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-235">So far, you've succeeded in hello following ways:</span></span>

* <span data-ttu-id="ae4eb-236">Aplikacja została osiągnięta pomyślnie usług AD FS i pasującym identyfikatorem planu odzyskiwania znajduje się w hello bazy danych usług AD FS</span><span class="sxs-lookup"><span data-stu-id="ae4eb-236">Your application has successfully reached AD FS and a matching RP identifier is found in hello AD FS database</span></span>
* <span data-ttu-id="ae4eb-237">Usługi AD FS pomyślnie uwierzytelnił użytkownika AD i Przekierowanie kopii aplikacji toohello strony głównej</span><span class="sxs-lookup"><span data-stu-id="ae4eb-237">AD FS has successfully authenticated an AD user and redirect you back toohello application's homepage</span></span>
* <span data-ttu-id="ae4eb-238">Usługi AD FS jako nazwa hello został pomyślnie wysłany oświadczenia aplikacji tooyour (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name), wskazywany przez fakt hello hello użytkownika nazwa jest wyświetlana w hello rogu.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-238">AD FS as successfully sent hello name claim (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) tooyour application, as indicated by hello fact that hello user name is displayed in hello corner.</span></span> 

<span data-ttu-id="ae4eb-239">Jeśli brakuje oświadczenia nazwy hello czy przejrzane **Hello,!**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-239">If hello name claim is missing, you would have seen **Hello, !**.</span></span> <span data-ttu-id="ae4eb-240">Jeśli przyjrzymy się Views\Shared\_LoginPartial.cshtml, okaże się, że używa `User.Identity.Name` nazwy użytkownika hello toodisplay.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-240">If you look at Views\Shared\_LoginPartial.cshtml, you find that it uses `User.Identity.Name` toodisplay hello user name.</span></span> <span data-ttu-id="ae4eb-241">Jak wspomniano wcześniej, jeśli nazwa hello oświadczeń z hello uwierzytelniony użytkownik jest dostępna w tokenie SAML hello, ASP.NET hydrates tej właściwości z nią.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-241">As mentioned previously, if hello name claim of hello authenticated user is available in hello SAML token, ASP.NET hydrates this property with it.</span></span> <span data-ttu-id="ae4eb-242">toosee, który hello wszystkich oświadczeń, które są wysyłane przez usługę AD FS, umieść punkt przerwania w Controllers\HomeController.cs, w hello metody akcji indeksu.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-242">toosee all hello claims that are sent by AD FS, put a breakpoint in Controllers\HomeController.cs, in hello Index action method.</span></span> <span data-ttu-id="ae4eb-243">Po uwierzytelnieniu użytkownika hello sprawdzić hello `System.Security.Claims.Current.Claims` kolekcji.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-243">After hello user is authenticated, inspect hello `System.Security.Claims.Current.Claims` collection.</span></span>

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a><span data-ttu-id="ae4eb-244">Autoryzowanie użytkowników do określonego kontrolerów lub akcji</span><span class="sxs-lookup"><span data-stu-id="ae4eb-244">Authorize users for specific controllers or actions</span></span>
<span data-ttu-id="ae4eb-245">Ponieważ członkostwa w grupie jako oświadczenia roli wprowadzono w konfiguracji relacji zaufania planu odzyskiwania, można je teraz użyć bezpośrednio w hello `[Authorize(Roles="...")]` decoration dla kontrolerów i akcji.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-245">Since you have included group memberships as role claims in your RP trust configuration, you can now use them directly in hello `[Authorize(Roles="...")]` decoration for controllers and actions.</span></span> <span data-ttu-id="ae4eb-246">W aplikacji biznesowych z wzorem hello Utwórz-odczytu-aktualizowania i usuwania (CRUD) można autoryzować tooaccess określonych ról każdej akcji.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-246">In a line-of-business application with hello Create-Read-Update-Delete (CRUD) pattern, you can authorize specific roles tooaccess each action.</span></span> <span data-ttu-id="ae4eb-247">Teraz zostanie tylko wypróbować tę funkcję na powitania istniejącego kontrolera głównej.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-247">For now, you will just try out this feature on hello existing Home controller.</span></span>

1. <span data-ttu-id="ae4eb-248">Otwórz Controllers\HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-248">Open Controllers\HomeController.cs.</span></span>
2. <span data-ttu-id="ae4eb-249">Dekoracji hello `About` i `Contact` toohello podobne metod akcji następującego kodu, za pomocą członkostwa grupy zabezpieczeń, które ma uwierzytelnionego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-249">Decorate hello `About` and `Contact` action methods similar toohello following code, using security group memberships that your authenticated user has.</span></span>  
   
    <pre class="prettyprint">
    <mark>[Authorize(Roles="Test Group")]</mark>
    public ActionResult About()
    {
        ViewBag.Message = "Your application description page.";
   
        return View();
    }
   
    <mark>[Authorize(Roles="Domain Admins")]</mark>
    public ActionResult Contact()
    {
        ViewBag.Message = "Your contact page.";
   
        return View();
    }
    </pre>
   
    <span data-ttu-id="ae4eb-250">Ponieważ dodano **użytkownika testowego** za**grupa testowa** w mojej środowiska laboratoryjnego usług AD FS, będzie używać autoryzacji tootest grupę testową na `About`.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-250">Since I added **Test User** too**Test Group** in my AD FS lab environment, I'll use Test Group tootest authorization on `About`.</span></span> <span data-ttu-id="ae4eb-251">Dla `Contact`, I przetestujesz, w przypadku ujemna hello **Administratorzy domeny**, toowhich **użytkownika testu** nie należy.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-251">For `Contact`, I'll test hello negative case of **Domain Admins**, toowhich **Test User** doesn't belong.</span></span>
3. <span data-ttu-id="ae4eb-252">Uruchom debuger hello, wpisując `F5` i zaloguj się, a następnie kliknij przycisk **o**.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-252">Start hello debugger by typing `F5` and sign in, then click **About**.</span></span> <span data-ttu-id="ae4eb-253">Powinny teraz być przeglądane hello `~/About/Index` strony pomyślnie, jeśli Twoje uwierzytelniony użytkownik jest autoryzowany dla tej akcji.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-253">You should now be viewing hello `~/About/Index` page successfully, if your authenticated user is authorized for that action.</span></span>
4. <span data-ttu-id="ae4eb-254">Teraz kliknij **skontaktuj się z**, co w przypadku mojej powinien nie zezwalają na **użytkownika testowego** hello akcji.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-254">Now click **Contact**, which in my case should not authorize **Test User** for hello action.</span></span> <span data-ttu-id="ae4eb-255">Przeglądarka hello jest jednak przekierowanego tooAD FS, który ostatecznie pokazuje ten komunikat:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-255">However, hello browser is redirected tooAD FS, which eventually shows this message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    <span data-ttu-id="ae4eb-256">Sprawdzenie tego błędu w Podglądzie zdarzeń na powitania serwera usług AD FS pojawić się komunikat o wyjątku:</span><span class="sxs-lookup"><span data-stu-id="ae4eb-256">If you investigate this error in Event Viewer on hello AD FS server, you see this exception message:</span></span>  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    <span data-ttu-id="ae4eb-257">Hello przyczyn tego błędu domyślnie MVC zwracanych jest 401 nieautoryzowane Jeśli nie masz uprawnień ról użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-257">hello reason for this error is that by default, MVC returns a 401 Unauthorized when a user's roles are not authorized.</span></span> <span data-ttu-id="ae4eb-258">Powoduje ponowne uwierzytelnianie żądania tooyour dostawcy tożsamości (AD FS).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-258">This triggers a reauthentication request tooyour identity provider (AD FS).</span></span> <span data-ttu-id="ae4eb-259">Ponieważ użytkownik hello jest już uwierzytelniony, usługi AD FS zwraca toohello tej samej stronie, która następnie wystawia 401 innego, tworzenie pętli przekierowania.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-259">Since hello user is already authenticated, AD FS returns toohello same page, which then issues another 401, creating a redirect loop.</span></span> <span data-ttu-id="ae4eb-260">Zostanie zastąpione przez klasy AuthorizeAttribute `HandleUnauthorizedRequest` metody za pomocą prostego logiki tooshow coś, co ma sens zamiast kontynuowanie hello przekierowania pętli.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-260">You will override AuthorizeAttribute's `HandleUnauthorizedRequest` method with simple logic tooshow something that makes sense instead of continuing hello redirect loop.</span></span>
5. <span data-ttu-id="ae4eb-261">Utwórz plik w projekcie hello AuthorizeAttribute.cs i Wklej hello następującego kodu do niego.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-261">Create a file in hello project called AuthorizeAttribute.cs, and paste hello following code into it.</span></span>
   
        using System;
        using System.Web.Mvc;
        using System.Web.Routing;
   
        namespace WebApp_WSFederation_DotNet
        {
            [AttributeUsage(AttributeTargets.Class | AttributeTargets.Method, Inherited = true, AllowMultiple = true)]
            public class AuthorizeAttribute : System.Web.Mvc.AuthorizeAttribute
            {
                protected override void HandleUnauthorizedRequest(AuthorizationContext filterContext)
                {
                    if (filterContext.HttpContext.Request.IsAuthenticated)
                    {
                        filterContext.Result = new System.Web.Mvc.HttpStatusCodeResult((int)System.Net.HttpStatusCode.Forbidden);
                    }
                    else
                    {
                        base.HandleUnauthorizedRequest(filterContext);
                    }
                }
            }
        }
   
    <span data-ttu-id="ae4eb-262">Hello zastąpić wysyła kodu HTTP 403 (Dostęp zabroniony) w przypadkach, uwierzytelnionym, ale nieautoryzowanego zamiast protokołu HTTP 401 (bez autoryzacji).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-262">hello override code sends an HTTP 403 (Forbidden) instead of HTTP 401 (Unauthorized) in  authenticated but unauthorized cases.</span></span>
6. <span data-ttu-id="ae4eb-263">Uruchom debuger hello ponownie, podając `F5`.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-263">Run hello debugger again with `F5`.</span></span> <span data-ttu-id="ae4eb-264">Kliknięcie przycisku **skontaktuj się z** pojawi się komunikat o błędzie większą przyjazność (, choć nieatrakcyjnych):</span><span class="sxs-lookup"><span data-stu-id="ae4eb-264">Clicking **Contact** now shows a more informative (albeit unattractive) error message:</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. <span data-ttu-id="ae4eb-265">Ponownie opublikować tooAzure aplikacji hello aplikacji usługi sieci Web aplikacji i przetestowania hello zachowanie hello działającej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-265">Publish hello application tooAzure App Service Web Apps again, and test hello behavior of hello live application.</span></span>

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a><span data-ttu-id="ae4eb-266">Połącz dane lokalne tooon</span><span class="sxs-lookup"><span data-stu-id="ae4eb-266">Connect tooon-premises data</span></span>
<span data-ttu-id="ae4eb-267">Powód byłaby wskazana tooimplement aplikacji biznesowych z z usługami AD FS a usługą Azure Active Directory jest problemów ze zgodnością z utrzymywaniem organizacji danych lokalnego.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-267">A reason that you would want tooimplement your line-of-business application with AD FS instead of Azure Active Directory is compliance issues with keeping organization data off-premise.</span></span> <span data-ttu-id="ae4eb-268">Może to także oznaczać aplikacji sieci web na platformie Azure muszą dostępu lokalnych baz danych, ponieważ nie są dozwolone toouse [bazy danych SQL](/services/sql-database/) hello warstwy danych dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="ae4eb-268">This may also mean that your web app in Azure must access on-premises databases, since you are not allowed toouse [SQL Database](/services/sql-database/) as hello data tier for your web apps.</span></span>

<span data-ttu-id="ae4eb-269">Aplikacje sieci Web usługi aplikacji platformy Azure obsługuje dostęp do lokalnych baz danych, dwa podejścia: [połączeń hybrydowych](../biztalk-services/integration-hybrid-connection-overview.md) i [sieci wirtualnych](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-269">Azure App Service Web Apps supports accessing on-premises databases with two approaches: [Hybrid Connections](../biztalk-services/integration-hybrid-connection-overview.md) and [Virtual Networks](web-sites-integrate-with-vnet.md).</span></span> <span data-ttu-id="ae4eb-270">Aby uzyskać więcej informacji, zobacz [integracji przy użyciu sieci Wirtualnej i połączeń hybrydowych z aplikacjami sieci Web usługi aplikacji Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span><span class="sxs-lookup"><span data-stu-id="ae4eb-270">For more information, see [Using VNET integration and Hybrid connections with Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="ae4eb-271">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ae4eb-271">Further resources</span></span>
* [<span data-ttu-id="ae4eb-272">Uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="ae4eb-272">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="ae4eb-273">Tworzenie aplikacji Azure — biznesowych przy użyciu uwierzytelniania usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae4eb-273">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>](web-sites-dotnet-lob-application-azure-ad.md)
* [<span data-ttu-id="ae4eb-274">Użyj hello opcji uwierzytelniania lokalnego organizacji (ADFS) z platformy ASP.NET w programie Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ae4eb-274">Use hello On-Premises Organizational Authentication Option (ADFS) With ASP.NET in Visual Studio 2013</span></span>](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [<span data-ttu-id="ae4eb-275">Migrowanie tooKatana VS2013 WIF z dla projektu sieci Web</span><span class="sxs-lookup"><span data-stu-id="ae4eb-275">Migrate a VS2013 Web Project From WIF tooKatana</span></span>](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [<span data-ttu-id="ae4eb-276">Omówienie usług Active Directory Federation Services</span><span class="sxs-lookup"><span data-stu-id="ae4eb-276">Active Directory Federation Services Overview</span></span>](http://technet.microsoft.com/library/hh831502.aspx)
* [<span data-ttu-id="ae4eb-277">Specyfikacja WS-Federation 1.1</span><span class="sxs-lookup"><span data-stu-id="ae4eb-277">WS-Federation 1.1 specification</span></span>](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

