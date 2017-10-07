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
# <a name="create-a-line-of-business-azure-app-with-ad-fs-authentication"></a>Tworzenie aplikacji Azure — biznesowych uwierzytelniania usług AD FS
W tym artykule opisano sposób toocreate ASP.NET MVC — biznesowych aplikacji w [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md) przy użyciu lokalnej [Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx) jako hello dostawcy tożsamości. W tym scenariuszu można pracować, podczas ma toocreate aplikacji biznesowych — w usłudze Azure App Service, ale Twoja organizacja wymaga katalogu toobe dane przechowywane na miejscu.

> [!NOTE]
> Omówienie hello opcje uwierzytelniania i autoryzacji różnych organizacji dla usługi Azure App Service, zobacz [Uwierzytelnij z lokalnej usługi Active Directory w aplikacji Azure](web-sites-authentication-authorization.md).
> 
> 

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Zostanie utworzona
Utworzysz podstawowej aplikacji ASP.NET w aplikacji sieci Web usługi aplikacji Azure z hello następujące funkcje:

* Uwierzytelnia użytkowników w usługach AD FS
* Używa `[Authorize]` tooauthorize użytkownicy dla różnych działań
* Statycznie dla debugowania w programie Visual Studio i publikowania aplikacji sieci Web usługi tooApp (Konfigurowanie raz, debugowania i opublikować w dowolnym momencie)  

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Co jest potrzebne
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Po toocomplete muszą hello w tym samouczku:

* Lokalnego wdrożenia usług AD FS (end-to-end przewodnik laboratorium testowego hello używane w tym samouczku, zobacz [laboratorium testowego: STS autonomiczny z usługami AD FS w maszynie Wirtualnej platformy Azure (dla testu tylko)](https://blogs.msdn.microsoft.com/cephalin/2014/12/21/test-lab-standalone-sts-with-ad-fs-in-azure-vm-for-test-only/))
* Uprawnienia toocreate zaufania jednostek uzależnionych w zarządzanie usługami AD FS
* Visual Studio 2013 Update 4 lub nowszy
* [Zestaw Azure SDK 2.8.1](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) lub nowszy

<a name="bkmk_sample"></a>

## <a name="use-sample-application-for-line-of-business-template"></a>Użyj przykładowej aplikacji biznesowych z szablonu
Witaj przykładowej aplikacji w tym samouczku [aplikacji sieci Web-WSFederation-DotNet)](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet), jest tworzony przez zespół usługi Azure Active Directory hello. Ponieważ usługi AD FS obsługuje usługi WS-Federation, można użyć jej jako szablonu toocreate--aplikacji biznesowych z łatwością. Ma hello następujące funkcje:

* Używa [WS-Federation](http://msdn.microsoft.com/library/bb498017.aspx) tooauthenticate z lokalnego wdrożenia usług AD FS
* Funkcjonalność logowania się i wylogowania
* Używa [Microsoft.Owin](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana) (zamiast Windows Identity Foundation), który jest hello przyszłych programu ASP.NET i tooset znacznie prostsza do uwierzytelniania i autoryzacji niż WIF

<a name="bkmk_setup"></a>

## <a name="set-up-hello-sample-application"></a>Konfigurowanie hello przykładowej aplikacji
1. Klonuj lub pobrać hello przykładowe rozwiązanie [aplikacji sieci Web-WSFederation-DotNet](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet) tooyour katalogu lokalnego.
   
   > [!NOTE]
   > Witaj instrukcje [README.md](https://github.com/AzureADSamples/WebApp-WSFederation-DotNet/blob/master/README.md) przedstawia sposób tooset się hello aplikację w usłudze Azure Active Directory. Jednak w tym samouczku, skonfigurować ją z usługami AD FS, dlatego zamiast tego należy wykonać kroki hello tutaj.
   > 
   > 
2. Otwórz rozwiązanie hello, a następnie otwórz Controllers\AccountController.cs w hello **Eksploratora rozwiązań**.
   
   Zobaczysz, że kod powitania po prostu wystawia użytkownika hello tooauthenticate żądania uwierzytelniania za pomocą protokołu WS-Federation. Wszystkie uwierzytelniania jest skonfigurowany w App_Start\Startup.Auth.cs.
3. Otwórz App_Start\Startup.Auth.cs. W hello `ConfigureAuth` metody, linia hello Uwaga:
   
       app.UseWsFederationAuthentication(
           new WsFederationAuthenticationOptions
           {
               Wtrealm = realm,
               MetadataAddress = metadata                                      
           });
   
   Witaj świecie OWIN ta Wstawka kodu jest w rzeczywistości hello systemu od zera, minimalna należy tooconfigure WS-Federation uwierzytelniania. Jest znacznie łatwiejsze i bardziej elegancki niż WIF, gdzie Web.config jest wprowadzonym za pomocą XML na całym hello miejsce. Witaj informacje potrzebne jest hello uzależnionej (RP) tylko identyfikator i hello adres URL pliku metadanych usługi AD FS. Oto przykład:
   
   * Identyfikator planu odzyskiwania:`https://contoso.com/MyLOBApp`
   * Adres metadanych:`http://adfs.contoso.com/FederationMetadata/2007-06/FederationMetadata.xml`
4. W App_Start\Startup.Auth.cs Zmień następujące definicje statyczny ciąg hello:  
   
   <pre class="prettyprint">
   private static string realm = ConfigurationManager.AppSettings["ida:<mark>RPIdentifier</mark>"];
   <mark><del>private static string aadInstance = ConfigurationManager.AppSettings["ida:AADInstance"];</del></mark>
   <mark><del>private static string tenant = ConfigurationManager.AppSettings["ida:Tenant"];</del></mark>
   <mark><del>private static string metadata = string.Format("{0}/{1}/federationmetadata/2007-06/federationmetadata.xml", aadInstance, tenant);</del></mark>
   <mark>private static string metadata = string.Format("https://{0}/federationmetadata/2007-06/federationmetadata.xml", ConfigurationManager.AppSettings["ida:ADFS"]);</mark>
   
   <mark><del>string authority = String.Format(CultureInfo.InvariantCulture, aadInstance, tenant);</del></mark>
   </pre>
5. Teraz wprowadzić hello odpowiednie zmiany w pliku Web.config. Otwórz plik Web.config hello i zmodyfikuj następujące ustawienia aplikacji hello:  
   
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
   
   Wypełnij hello wartości klucza w zależności od używanego środowiska odpowiednich.
6. Tworzenie toomake aplikacji hello się, że nie ma żadnych błędów.

To już wszystko. Teraz hello Przykładowa aplikacja jest gotowa toowork z usługami AD FS. Nadal potrzebujesz tooconfigure zaufania planu odzyskiwania z tej aplikacji w usługach AD FS później.

<a name="bkmk_deploy"></a>

## <a name="deploy-hello-sample-application-tooazure-app-service-web-apps"></a>Wdrażanie hello przykładowej aplikacji tooAzure aplikacji usługi sieci Web aplikacji
W tym miejscu publikowania aplikacji sieci web tooa aplikacji hello w aplikacji usługi sieci Web aplikacji przy jednoczesnym zachowaniu hello debugowania środowiska. Należy pamiętać, że chcesz zacząć aplikacji hello toopublish przed ma zaufanie planu odzyskiwania z usługami AD FS, więc uwierzytelniania nadal nie działa jeszcze. Jednak jeśli chcesz go teraz program może URL aplikacji sieci web hello później używania tooconfigure hello RP zaufania.

1. Kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/01-publish-website.png)
2. Wybierz **usługi Microsoft Azure App Service**.
3. Jeżeli nie zarejestrujesz w tooAzure, kliknij przycisk **logowania** używanie konta Microsoft hello toosign Twojej subskrypcji platformy Azure w.
4. Po zalogowaniu kliknij **nowy** toocreate aplikacji sieci web.
5. Wypełnij wszystkie wymagane pola. Zamierzasz tooconnect tooon lokalne dane później, dlatego nie należy tworzyć bazy danych dla tej aplikacji sieci web.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/02-create-website.png)
6. Kliknij przycisk **Utwórz**. Po utworzeniu aplikacji sieci web hello okna dialogowego publikowanie w sieci Web hello jest otwarty.
7. W **docelowy adres URL**, zmień **http** za**https**. Skopiuj hello cały adres URL tooa Edytor tekstu do późniejszego użycia. Następnie kliknij przycisk **publikowania**.
   
    ![](./media/web-sites-dotnet-lob-application-adfs/03-destination-url.png)
8. W programie Visual Studio Otwórz **Web.Release.config** w projekcie. Wstaw powitania po XML na powitania `<configuration>` tagu i Zastąp wartości klucza hello adres URL aplikacji sieci web publikowania.  
   
   <pre class="prettyprint">
   &lt;appSettings&gt;
   &lt;add key="ida:RPIdentifier" value="<mark>[e.g. https://mylobapp.azurewebsites.net/]</mark>" xdt:Transform="SetAttributes" xdt:Locator="Match(key)" /&gt;
   &lt;/appSettings&gt;</pre>

Gdy wszystko będzie gotowe, ma dwa identyfikatory RP skonfigurowane w projekcie, jeden dla danego środowiska debugowania w programie Visual Studio i jeden dla hello opublikowane aplikacji sieci web na platformie Azure. Zaufanie RP zostanie skonfigurowany dla każdego z dwóch środowisk hello w usługach AD FS. Podczas debugowania, ustawienia aplikacji hello w pliku Web.config są używane toomake Twojego **debugowania** konfiguracji pracy z usługami AD FS. Jeśli jest publikowany (domyślnie hello **wersji** konfiguracji został opublikowany), przekazaniu przekształcone Web.config zawiera zmiany w ustawieniach aplikacji hello w Web.Release.config.

Jeśli chcesz tooattach hello opublikowana aplikacja sieci web debugera Azure toohello (tj. musisz przekazać symboli debugowania kodu w hello opublikowana aplikacja sieci web), można utworzyć klonu hello debugowania konfiguracji platformy Azure, debugowanie, ale z własnego niestandardowego pliku Web.config przekształcenie ( np. Web.AzureDebug.config) używający ustawień aplikacji hello z Web.Release.config. Dzięki temu można toomaintain konfiguracji statycznej hello różnych środowiskach.

<a name="bkmk_rptrusts"></a>

## <a name="configure-relying-party-trusts-in-ad-fs-management"></a>Konfigurowanie relacji zaufania w zarządzanie usługami AD FS
Teraz należy tooconfigure zaufania RP do zarządzania usługami AD FS można było użyć przykładowej aplikacji i faktycznie uwierzytelniania za pomocą usług AD FS. Konieczne będzie tooset się dwa oddzielne zaufania planu odzyskiwania, jeden dla danego środowiska debugowania i jeden dla aplikacji opublikowanych w sieci web.

> [!NOTE]
> Upewnij się, czy Powtórz hello następujące kroki dla obu tych środowisk.
> 
> 

1. Na serwerze usług AD FS Zaloguj się przy użyciu poświadczeń, które mają management rights tooAD FS.
2. Otwórz przystawkę zarządzania usługami AD FS. Kliknij prawym przyciskiem myszy **AD FS\Trusted Relationships\Relying uzależnionych** i wybierz **dodać zaufanie jednostki uzależnionej**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/1-add-rptrust.png)
3. W hello **wybierz źródło danych** wybierz **ręcznie wprowadź dane dotyczące jednostki uzależnionej hello**. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/2-enter-rp-manually.png)
4. W hello **Określanie nazwy wyświetlanej** , wpisz nazwę wyświetlaną dla aplikacji hello i kliknij przycisk **dalej**.
5. W hello **wybierz protokół** kliknij przycisk **dalej**.
6. W hello **Konfigurowanie certyfikatu** kliknij przycisk **dalej**.
   
   > [!NOTE]
   > Ponieważ powinien być używany protokół HTTPS już, zaszyfrowanych tokenów są opcjonalne. Jeśli na pewno tooencrypt tokenów z usług AD FS na tej stronie, musisz również dodać logikę odszyfrowywania tokenu w kodzie. Aby uzyskać więcej informacji, zobacz [ręczne konfigurowanie oprogramowania pośredniczącego OWIN WS-Federation i akceptowanie szyfrowane tokenów](http://chris.59north.com/post/2014/08/21/Manually-configuring-OWIN-WS-Federation-middleware-and-accepting-encrypted-tokens.aspx).
   > 
   > 
7. Przed przejściem do następnego kroku hello należy jednej informacji z projektu programu Visual Studio. We właściwościach projektu hello, należy zwrócić uwagę hello **adres URL protokołu SSL** aplikacji hello. 
   
   ![](./media/web-sites-dotnet-lob-application-adfs/3-ssl-url.png)
8. Zarządzanie usługami AD FS, w hello w **Konfigurowanie adresu URL** strony hello **jednostki uzależnionej strony Kreatora dodawania relacji zaufania**, wybierz pozycję **Włącz obsługę protokołu WS-Federation Passive hello** i Wpisz hello SSL adres URL projektu programu Visual Studio, zanotowaną w poprzednim kroku hello. Następnie kliknij przycisk **Dalej**.
   
   ![](./media/web-sites-dotnet-lob-application-adfs/4-configure-url.png)
   
   > [!NOTE]
   > Adres URL określa, gdzie toosend powitania klienta po uwierzytelnieniu zakończy się pomyślnie. W środowisku debugowania hello powinna być <code>https://localhost:&lt;port&gt;/</code>. Dla hello opublikowana aplikacja sieci web należy go adres URL aplikacji sieci web hello.
   > 
   > 
9. W hello **skonfiguruj identyfikatory** , sprawdź, czy projekt SSL adres URL jest już wyświetlane i kliknij przycisk **dalej**. Kliknij przycisk **dalej** wszystkie hello sposób toohello koniec hello kreatora bez ustawienia domyślne.
   
   > [!NOTE]
   > App_Start\Startup.Auth.cs projektu programu Visual Studio, ten identyfikator jest dopasowywana wartość hello <code>WsFederationAuthenticationOptions.Wtrealm</code> podczas uwierzytelniania federacyjnego. Domyślnie adres URL aplikacji hello z poprzedniego kroku hello jest dodawany jako identyfikator planu odzyskiwania.
   > 
   > 
10. Konfigurowanie w usługach AD FS hello RP aplikacji dla projektu zostało zakończone. Następnie należy skonfigurować ten toosend aplikacji hello oświadczenia wymagane przez aplikację. Witaj **Edycja reguł oświadczeń** okna dialogowego jest domyślnie otwierany automatycznie na końcu hello hello kreatora, aby natychmiast rozpocząć. Skonfigurujmy hello co najmniej następujących oświadczeń (ze schematami w nawiasach):
    
    * Nazwa (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name) — używane przez program ASP.NET toohydrate `User.Identity.Name`.
    * Użytkownika nazwy głównej (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn) - używany toouniquely identyfikowania użytkowników w organizacji hello.
    * Członkostwa w grupach jako role (http://schemas.microsoft.com/ws/2008/06/identity/claims/role) — może być używany z `[Authorize(Roles="role1, role2,...")]` tooauthorize decoration kontrolerów/akcji. W rzeczywistości to rozwiązanie może nie być hello większości wydajności do autoryzacji ról. Użytkownicy AD należą toohundreds grup zabezpieczeń, staje się setki oświadczeń roli z tokenu SAML hello. Informacje o innym podejściu jest toosend jedną rolę warunkowo oświadczeń w zależności od użytkownika hello członkostwa w określonej grupie. Jednak firma Microsoft będzie Zachowaj prostotę w tym samouczku.
    * Nazwa Identyfikatora (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier) — może służyć do weryfikacji zabezpieczający przed sfałszowaniem. Aby uzyskać więcej informacji na temat działania toomake go z weryfikacją zabezpieczający przed sfałszowaniem, zobacz hello **Dodawanie funkcji z biznesowych** sekcji [tworzenie aplikacji Azure — biznesowych przy użyciu uwierzytelniania usługi Azure Active Directory ](web-sites-dotnet-lob-application-azure-ad.md#bkmk_crud).
    
    > [!NOTE]
    > Witaj oświadczeń typów konieczność tooconfigure aplikacji zależy od potrzeb aplikacji. Witaj lista oświadczeń obsługiwane przez aplikacje usługi Azure Active Directory (tzn. RP zaufania), na przykład, zobacz [obsługiwany Token i typy oświadczeń](http://msdn.microsoft.com/library/azure/dn195587.aspx).
    > 
    > 
11. W oknie dialogowym Edycja reguł oświadczeń powitania kliknij **Dodaj regułę**.
12. Skonfigurować oświadczenia nazwy UPN i roli hello, jak pokazano w hello zrzut ekranu, a następnie kliknij przycisk **Zakończ**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/5-ldap-claims.png)
    
    Następnie należy utworzyć przejściowej nazwę Identyfikatora oświadczenia, wykonując kroki hello przedstawiona w [nazwy identyfikatorów potwierdzenia SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
13. Kliknij przycisk **Dodaj regułę** ponownie.
14. Wybierz **wysyłanie oświadczeń przy użyciu reguły niestandardowej** i kliknij przycisk **dalej**.
15. Wklej hello następujące reguły języka na powitania **reguły niestandardowej** okno, nazwa reguły hello **na identyfikator sesji** i kliknij przycisk **Zakończ**.  
    
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
    
    Niestandardowe reguły powinna wyglądać tego zrzutu ekranu:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/6-per-session-identifier.png)
16. Kliknij przycisk **Dodaj regułę** ponownie.
17. Wybierz **Przekształcanie oświadczenia przychodzącego** i kliknij przycisk **dalej**.
18. Skonfiguruj regułę hello, jak pokazano na zrzucie ekranu pokazano hello (przy użyciu typu oświadczenia hello utworzone w regule niestandardowej hello), a następnie kliknij przycisk **Zakończ**.
    
    ![](./media/web-sites-dotnet-lob-application-adfs/7-transient-name-id.png)
    
    Aby uzyskać szczegółowe informacje dotyczące kroków hello hello przejściowej oświadczenia Identyfikatora nazwy, zobacz [nazwy identyfikatorów potwierdzenia SAML](http://blogs.msdn.com/b/card/archive/2010/02/17/name-identifiers-in-saml-assertions.aspx).
19. Kliknij przycisk **Zastosuj** w hello **Edycja reguł oświadczeń** okna dialogowego. Powinna ona wyglądać tak jak powitania po zrzut ekranu:
    
    ![](./media/web-sites-dotnet-lob-application-adfs/8-all-claim-rules.png)
    
    > [!NOTE]
    > Ponownie upewnij się, powtórz te kroki dla debugowania środowiska i opublikowana aplikacja sieci web.
    > 
    > 

<a name="bkmk_test"></a>

## <a name="test-federated-authentication-for-your-application"></a>Uwierzytelnianie Sfederowane testu dla aplikacji
Możesz są gotowe tootest aplikacji logiki uwierzytelniania dla usług AD FS. W moich środowiska laboratoryjnego usług AD FS masz użytkownika testowego, w której należy grupa testowa tooa w usłudze Active Directory (AD).

![](./media/web-sites-dotnet-lob-application-adfs/10-test-user-and-group.png)

Uwierzytelnianie tootest w debugerze hello, wystarczy toodo teraz jest typu `F5`. Jeśli chcesz tootest uwierzytelniania w hello opublikowana aplikacja sieci web, przejdź toohello adresu URL.

Po załadowaniu hello aplikacji sieci web, kliknij przycisk **logowania**. Należy teraz pobrać albo okna dialogowego lub hello logowania strony logowania obsługiwanych przez usługi AD FS, w zależności od metody uwierzytelniania hello wybranej przez usługi AD FS. Oto, co pojawia się w programie Internet Explorer 11.

![](./media/web-sites-dotnet-lob-application-adfs/9-test-debugging.png)

Po zalogowaniu użytkownika w domenie hello AD hello AD FS wdrożenia powinna zostać wyświetlona strona główna hello ponownie, podając **Hello, <User Name>!** w hello rogu. Oto, co pojawia się.

![](./media/web-sites-dotnet-lob-application-adfs/11-test-debugging-success.png)

Do tej pory zostały zakończone powodzeniem w następujące sposoby hello:

* Aplikacja została osiągnięta pomyślnie usług AD FS i pasującym identyfikatorem planu odzyskiwania znajduje się w hello bazy danych usług AD FS
* Usługi AD FS pomyślnie uwierzytelnił użytkownika AD i Przekierowanie kopii aplikacji toohello strony głównej
* Usługi AD FS jako nazwa hello został pomyślnie wysłany oświadczenia aplikacji tooyour (http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name), wskazywany przez fakt hello hello użytkownika nazwa jest wyświetlana w hello rogu. 

Jeśli brakuje oświadczenia nazwy hello czy przejrzane **Hello,!**. Jeśli przyjrzymy się Views\Shared\_LoginPartial.cshtml, okaże się, że używa `User.Identity.Name` nazwy użytkownika hello toodisplay. Jak wspomniano wcześniej, jeśli nazwa hello oświadczeń z hello uwierzytelniony użytkownik jest dostępna w tokenie SAML hello, ASP.NET hydrates tej właściwości z nią. toosee, który hello wszystkich oświadczeń, które są wysyłane przez usługę AD FS, umieść punkt przerwania w Controllers\HomeController.cs, w hello metody akcji indeksu. Po uwierzytelnieniu użytkownika hello sprawdzić hello `System.Security.Claims.Current.Claims` kolekcji.

![](./media/web-sites-dotnet-lob-application-adfs/12-test-debugging-all-claims.png) 

<a name="bkmk_authorize"></a>

## <a name="authorize-users-for-specific-controllers-or-actions"></a>Autoryzowanie użytkowników do określonego kontrolerów lub akcji
Ponieważ członkostwa w grupie jako oświadczenia roli wprowadzono w konfiguracji relacji zaufania planu odzyskiwania, można je teraz użyć bezpośrednio w hello `[Authorize(Roles="...")]` decoration dla kontrolerów i akcji. W aplikacji biznesowych z wzorem hello Utwórz-odczytu-aktualizowania i usuwania (CRUD) można autoryzować tooaccess określonych ról każdej akcji. Teraz zostanie tylko wypróbować tę funkcję na powitania istniejącego kontrolera głównej.

1. Otwórz Controllers\HomeController.cs.
2. Dekoracji hello `About` i `Contact` toohello podobne metod akcji następującego kodu, za pomocą członkostwa grupy zabezpieczeń, które ma uwierzytelnionego użytkownika.  
   
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
   
    Ponieważ dodano **użytkownika testowego** za**grupa testowa** w mojej środowiska laboratoryjnego usług AD FS, będzie używać autoryzacji tootest grupę testową na `About`. Dla `Contact`, I przetestujesz, w przypadku ujemna hello **Administratorzy domeny**, toowhich **użytkownika testu** nie należy.
3. Uruchom debuger hello, wpisując `F5` i zaloguj się, a następnie kliknij przycisk **o**. Powinny teraz być przeglądane hello `~/About/Index` strony pomyślnie, jeśli Twoje uwierzytelniony użytkownik jest autoryzowany dla tej akcji.
4. Teraz kliknij **skontaktuj się z**, co w przypadku mojej powinien nie zezwalają na **użytkownika testowego** hello akcji. Przeglądarka hello jest jednak przekierowanego tooAD FS, który ostatecznie pokazuje ten komunikat:
   
    ![](./media/web-sites-dotnet-lob-application-adfs/13-authorize-adfs-error.png)
   
    Sprawdzenie tego błędu w Podglądzie zdarzeń na powitania serwera usług AD FS pojawić się komunikat o wyjątku:  
   
    <pre class="prettyprint">
    Microsoft.IdentityServer.Web.InvalidRequestException: MSIS7042: <mark>hello same client browser session has made '6' requests in hello last '11' seconds.</mark> Contact your administrator for details.
       at Microsoft.IdentityServer.Web.Protocols.PassiveProtocolHandler.UpdateLoopDetectionCookie(WrappedHttpListenerContext context)
       at Microsoft.IdentityServer.Web.Protocols.WSFederation.WSFederationProtocolHandler.SendSignInResponse(WSFederationContext context, MSISSignInResponse response)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.ProcessProtocolRequest(ProtocolContext protocolContext, PassiveProtocolHandler protocolHandler)
       at Microsoft.IdentityServer.Web.PassiveProtocolListener.OnGetContext(WrappedHttpListenerContext context)
    </pre>
   
    Hello przyczyn tego błędu domyślnie MVC zwracanych jest 401 nieautoryzowane Jeśli nie masz uprawnień ról użytkownika. Powoduje ponowne uwierzytelnianie żądania tooyour dostawcy tożsamości (AD FS). Ponieważ użytkownik hello jest już uwierzytelniony, usługi AD FS zwraca toohello tej samej stronie, która następnie wystawia 401 innego, tworzenie pętli przekierowania. Zostanie zastąpione przez klasy AuthorizeAttribute `HandleUnauthorizedRequest` metody za pomocą prostego logiki tooshow coś, co ma sens zamiast kontynuowanie hello przekierowania pętli.
5. Utwórz plik w projekcie hello AuthorizeAttribute.cs i Wklej hello następującego kodu do niego.
   
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
   
    Hello zastąpić wysyła kodu HTTP 403 (Dostęp zabroniony) w przypadkach, uwierzytelnionym, ale nieautoryzowanego zamiast protokołu HTTP 401 (bez autoryzacji).
6. Uruchom debuger hello ponownie, podając `F5`. Kliknięcie przycisku **skontaktuj się z** pojawi się komunikat o błędzie większą przyjazność (, choć nieatrakcyjnych):
   
    ![](./media/web-sites-dotnet-lob-application-adfs/14-unauthorized-forbidden.png)
7. Ponownie opublikować tooAzure aplikacji hello aplikacji usługi sieci Web aplikacji i przetestowania hello zachowanie hello działającej aplikacji.

<a name="bkmk_data"></a>

## <a name="connect-tooon-premises-data"></a>Połącz dane lokalne tooon
Powód byłaby wskazana tooimplement aplikacji biznesowych z z usługami AD FS a usługą Azure Active Directory jest problemów ze zgodnością z utrzymywaniem organizacji danych lokalnego. Może to także oznaczać aplikacji sieci web na platformie Azure muszą dostępu lokalnych baz danych, ponieważ nie są dozwolone toouse [bazy danych SQL](/services/sql-database/) hello warstwy danych dla aplikacji sieci web.

Aplikacje sieci Web usługi aplikacji platformy Azure obsługuje dostęp do lokalnych baz danych, dwa podejścia: [połączeń hybrydowych](../biztalk-services/integration-hybrid-connection-overview.md) i [sieci wirtualnych](web-sites-integrate-with-vnet.md). Aby uzyskać więcej informacji, zobacz [integracji przy użyciu sieci Wirtualnej i połączeń hybrydowych z aplikacjami sieci Web usługi aplikacji Azure](https://azure.microsoft.com/blog/2014/10/30/using-vnet-or-hybrid-conn-with-websites/).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Dodatkowe zasoby
* [Uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure](web-sites-authentication-authorization.md)
* [Tworzenie aplikacji Azure — biznesowych przy użyciu uwierzytelniania usługi Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md)
* [Użyj hello opcji uwierzytelniania lokalnego organizacji (ADFS) z platformy ASP.NET w programie Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/)
* [Migrowanie tooKatana VS2013 WIF z dla projektu sieci Web](http://www.cloudidentity.com/blog/2014/09/15/MIGRATE-A-VS2013-WEB-PROJECT-FROM-WIF-TO-KATANA/)
* [Omówienie usług Active Directory Federation Services](http://technet.microsoft.com/library/hh831502.aspx)
* [Specyfikacja WS-Federation 1.1](http://download.boulder.ibm.com/ibmdl/pub/software/dw/specs/ws-fed/WS-Federation-V1-1B.pdf?S_TACT=105AGX04&S_CMP=LP)

