---
title: "Tworzenie aplikacji Azure — biznesowych przy użyciu uwierzytelniania usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak utworzyć aplikację programu ASP.NET MVC biznesowych — w usłudze aplikacji Azure, który przeprowadza uwierzytelnianie z usługą Azure Active Directory"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 6eadf0a521a32c5bc580908e4e4b7f4305e2bf7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a>Tworzenie aplikacji Azure — biznesowych przy użyciu uwierzytelniania usługi Azure Active Directory
W tym artykule przedstawiono sposób tworzenia aplikacji biznesowych programu .NET w [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) przy użyciu [uwierzytelniania / autoryzacji](../app-service/app-service-authentication-overview.md) funkcji. Przedstawiono również sposób użycia [interfejsu API usługi Azure Active Directory Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) danych katalogowych kwerendy w aplikacji.

Dzierżawy usługi Azure Active Directory, którego używasz, może być katalogu tylko do platformy Azure. Lub może być [synchronizowane z lokalnej usługi Active Directory](../active-directory/active-directory-aadconnect.md) można utworzyć jeden środowisko logowania dla pracowników, które są lokalne i zdalne. W tym artykule korzysta z domyślnego katalogu dla konta platformy Azure.

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a>Zostanie utworzona
Będzie utworzyć prostą aplikację Utwórz-odczytu-aktualizowania i usuwania (CRUD)-biznesowych w aplikacji usługi sieci Web aplikacji czy śledzi elementy robocze z następujących funkcji:

* Uwierzytelnia użytkowników w usłudze Azure Active Directory
* Wysyła zapytanie do katalogu użytkowników i grup za pomocą [interfejsu API usługi Azure Active Directory Graph](http://msdn.microsoft.com/library/azure/hh974476.aspx)
* Użyj programu ASP.NET MVC *bez uwierzytelniania* szablonu

Jeśli potrzebujesz kontroli dostępu opartej na rolach (RBAC) dla aplikacji biznesowych z platformy Azure, zobacz [następnego kroku](#next).

<a name="bkmk_need"></a>

## <a name="what-you-need"></a>Co jest potrzebne
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

Potrzebne do ukończenia tego samouczka:

* Dzierżawy usługi Azure Active Directory z użytkownikami w różnych grupach
* Uprawnienia do tworzenia aplikacji w ramach dzierżawy usługi Azure Active Directory
* Visual Studio 2013 Update 4 lub nowszy
* [Zestaw Azure SDK 2.8.1 lub nowszy](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a>Tworzenie i wdrażanie aplikacji sieci web na platformie Azure
1. W programie Visual Studio, kliknij przycisk **pliku** > **nowy** > **projektu**.
2. Wybierz **aplikacji sieci Web ASP.NET**, nazwę projektu i kliknij przycisk **OK**.
3. Wybierz **MVC** szablonu, następnie zmienić uwierzytelnianie, aby **bez uwierzytelniania**. Upewnij się, że **Hostuj w chmurze** jest zaznaczone, a następnie kliknij przycisk **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. W **Tworzenie usługi App Service** okna dialogowego, kliknij przycisk **Dodaj konto** (i następnie **Dodaj konto** na liście rozwijanej) logować się do konta platformy Azure.
5. Po zalogowaniu skonfigurować aplikację sieci web. Utwórz grupę zasobów i nowy plan usługi aplikacji, klikając odpowiednio **nowy** przycisku. Kliknij przycisk **Eksploruj dodatkowych usług Azure** aby kontynuować.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. W **usług** , kliknij pozycję  **+**  można dodać bazy danych SQL dla aplikacji. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. W **Konfigurowanie bazy danych SQL**, kliknij przycisk **nowy** można utworzyć wystąpienia programu SQL Server.
8. W **Konfiguruj serwer SQL**, skonfiguruj wystąpienia programu SQL Server. Następnie kliknij przycisk **OK**, **OK**, i **Utwórz** można rozpocząć poza tworzenie aplikacji na platformie Azure.
9. W **działanie usługi Azure App Service**, zobacz temat po zakończeniu tworzenia aplikacji. Kliknij przycisk  **publikowania &lt;* appname*> do tej aplikacji sieci Web teraz **, następnie kliknij przycisk **publikowania**. 
   
    Po zakończeniu pracy programu Visual Studio otworzy Opublikuj aplikację w przeglądarce. 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a>Konfigurowanie uwierzytelniania i katalog dostępu
1. Zaloguj się do witryny [Azure Portal](https://portal.azure.com).
2. Z menu po lewej stronie kliknij **usługi aplikacji** > **&lt;*appname*> ** > **uwierzytelniania / autoryzacji**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. Włącz uwierzytelnianie usługi Azure Active Directory, klikając **na** > **usługi Azure Active Directory** > **Express**  >   **OK**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. Kliknij przycisk **zapisać** na pasku poleceń.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    Ustawienia uwierzytelniania są zapisane pomyślnie, spróbuj przejść do aplikacji ponownie w przeglądarce. Domyślnych ustawień wymusić uwierzytelnianie na całej aplikacji. Jeśli użytkownik nie jest już zalogowany, nastąpi przekierowanie do ekranu logowania. Po zalogowaniu, zapoznaj się aplikacji zabezpieczonej przez protokół HTTPS. Następnie należy włączyć dostęp do danych katalogu. 
5. Przejdź do [klasyczny portal](https://manage.windowsazure.com).
6. Z menu po lewej stronie kliknij **usługi Active Directory** > **katalog domyślny** > **aplikacji**  >   **&lt;* appname*> **.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    To jest aplikacja usługi Azure Active Directory, usługi aplikacji utworzony dla Ciebie umożliwia autoryzację / funkcji uwierzytelniania.
7. Kliknij przycisk **użytkowników** i **grup** aby upewnić się, że niektórych użytkowników i grup w katalogu. Jeśli nie, należy utworzyć kilka użytkowników testowych i grup.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. Kliknij przycisk **Konfiguruj** konfigurowania tej aplikacji.
9. Przewiń w dół do **klucze** sekcji, a następnie dodaj klucz wybierając czas trwania. Następnie kliknij przycisk **delegowane uprawnienia** i wybierz **odczytuj dane katalogu**. 
   Kliknij pozycję **Zapisz**.
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. Po zapisaniu ustawień przewiń z powrotem do **klucze** sekcji, a następnie kliknij przycisk **kopiowania** przycisk, aby skopiować klucz klienta. 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > Jeśli opuścisz tę stronę teraz, nie będzie można uzyskać dostępu do tego klucza klienta kiedykolwiek ponownie.
    > 
    > 
11. Następnie należy skonfigurować aplikację sieci web przy użyciu tego klucza. Zaloguj się do [Eksploratora zasobów Azure](https://resources.azure.com) z Twoim kontem platformy Azure.
12. W górnej części strony kliknij **odczytu/zapisu** do wprowadzania zmian w Eksploratora zasobów Azure.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. Znalezienie ustawień uwierzytelniania dla aplikacji, znajdujący się w subskrypcji >  **&lt;* Nazwa subskrypcji*> ** > **resourceGroups**  >   **&lt;* resourcegroupname*> ** > **dostawców** > **Microsoft.Web**  >  **witryny** > **&lt;*appname*> ** > **config**  >  **authsettings**.
14. Kliknij pozycję **Edytuj**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. W okienku edycji zestawu `clientSecret` i `additionalLoginParams` właściwości w następujący sposób.
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. Kliknij przycisk **Put** u góry, aby przesłać zmiany.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. Teraz, aby sprawdzić, czy masz token autoryzacji do dostępu do usługi Azure Active Directory interfejsu API programu Graph, przejdź do  **https://&lt;*appname*>.azurewebsites.net/.auth/me** w przeglądarce . Jeśli skonfigurowano wszystko poprawnie, powinny pojawić się `access_token` w odpowiedzi JSON.
    
    `~/.auth/me` Ścieżki adresu URL jest zarządzana przez aplikację usługi uwierzytelniania / autoryzacji, które pozwalają na wszystkie informacje dotyczące sesji uwierzytelnionych. Aby uzyskać więcej informacji, zobacz [uwierzytelnianie i autoryzację w usłudze Azure App Service](../app-service/app-service-authentication-overview.md).
    
    > [!NOTE]
    > `access_token` Ma okres ważności. Jednak aplikacja usługi uwierzytelniania / autoryzacji zawiera token odświeżania funkcji z `~/.auth/refresh`. Aby uzyskać więcej informacji dotyczących sposobu jego używania, zobacz [sklepu z aplikacjami usługi tokenu](https://cgillum.tech/2016/03/07/app-service-token-store/).
    > 
    > 

Następnie zostanie Zrób coś, które są przydatne w przypadku danych katalogu.

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a>Dodawanie do aplikacji biznesowych — funkcja
Można teraz utworzyć prosty śledzenia elementów roboczych CRUD.  

1. W folderze ~\Models, Utwórz plik klasy o nazwie WorkItem.cs i Zastąp `public class WorkItem {...}` następującym kodem:
   
     przy użyciu System.ComponentModel.DataAnnotations;
   
     Klasa publiczna {elementu pracy
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     }
   
     Wyliczenie publiczne WorkItemStatus {
   
         Open,
         Investigating,
         Resolved,
         Closed
     }
2. Skompiluj projekt, aby udostępnić nowe modelu dla logiki szkieletów w programie Visual Studio.
3. Dodaj nowy element szkieletu `WorkItemsController` do folderu ~\Controllers (kliknij prawym przyciskiem myszy **kontrolerów**, wskaż polecenie **Dodaj**i wybierz **nowy element szkieletu**). 
4. Wybierz **kontroler MVC 5 z widokami używający narzędzia Entity Framework** i kliknij przycisk **Dodaj**.
5. Wybierz model, który zostanie utworzony, a następnie kliknij przycisk  **+**  , a następnie **Dodaj** dodać kontekstu danych, a następnie kliknij przycisk **Dodaj**.
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. W ~\Views\WorkItems\Create.cshtml (element automatycznie szkieletu), Znajdź `Html.BeginForm` metody pomocniczej i wprowadź następujące zmiany wyróżnione:  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   Należy pamiętać, że `token` i `tenant` są używane przez `AadPicker` obiektu w celu wykonywania wywołań interfejsu API usługi Azure Active Directory Graph. Należy dodać `AadPicker` później.     
   
   > [!NOTE]
   > Równie dobrze Ci `token` i `tenant` po stronie klienta z `~/.auth/me`, ale ten będzie wywołanie dodatkowego serwera. Na przykład:
   > 
   > $.ajax ({typ danych: "json", adres url: "/.auth/me", powodzenia: funkcji (dane) {var token = danych [0] .access_token; var dzierżawy = .find .user_claims danych [0] (c = > c.typ === "http://schemas.microsoft.com/identity/claims/tenantid") .val;}});
   > 
   > 
7. Wprowadzenie identycznych zmian z ~ \Views\WorkItems\Edit.cshtml.
8. `AadPicker` Obiektu jest zdefiniowana w skrypcie, który należy dodać do projektu. Kliknij prawym przyciskiem myszy ~\Scripts folder, wskaż pozycję **Dodaj**i kliknij przycisk **plik JavaScript**. Typ `AadPickerLibrary` nazwę pliku i kliknij **OK**.
9. Skopiuj zawartość z [tutaj](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) do ~ \Scripts\AadPickerLibrary.js.
   
   W skrypcie `AadPicker` obiektu wywołania [interfejsu API usługi Azure Active Directory Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) wyszukiwania dla użytkowników i grup zgodnych danych wejściowych.  
10. Używa również ~\Scripts\AadPickerLibrary.js [widget autouzupełniania interfejsu użytkownika jQuery](https://jqueryui.com/autocomplete/). Dlatego należy dodać do projektu interfejsu użytkownika jQuery. Kliknij prawym przyciskiem myszy projekt w, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
11. W Menedżerze pakietów NuGet, kliknij przycisk Przeglądaj, typ **interfejsu użytkownika jquery** na pasku wyszukiwania, a następnie kliknij polecenie **jQuery.UI.Combined**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. W okienku po prawej stronie kliknij **zainstalować**, następnie kliknij przycisk **OK** aby kontynuować.
13. Otwórz ~\App_Start\BundleConfig.cs i wprowadź następujące zmiany wyróżnione:  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    Istnieje więcej sposobów wydajności zarządzanie plikami JavaScript i CSS w aplikacji. Jednak dla uproszczenia możesz po prostu zacząć potwierdzeń na pakiety, które są ładowane z każdego widoku.
14. Ponadto w ~ \Global.asax, Dodaj następujący wiersz kodu w `Application_Start()` metody. `Ctrl`+`.`na każdym nazewnictwa błędów rozpoznawania nazw, aby go rozwiązać.
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > Należy ten wiersz kodu, ponieważ korzysta z domyślnego szablonu MVC <code>[ValidateAntiForgeryToken]</code> decoration w przypadku niektórych działań. Ze względu na zachowanie opisanego przez [Allen firmy Brock](https://twitter.com/BrockLAllen) w [MVC 4, AntiForgeryToken i oświadczeń](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) Twojego HTTP POST może zakończyć się niepowodzeniem sprawdzania poprawności tokenu zabezpieczającego przed sfałszowaniem, ponieważ:
    > 
    > * Usługa Azure Active Directory nie wysyła http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, co jest wymagane domyślnie przez token zabezpieczający przed sfałszowaniem.
    > * Jeśli usługi Azure Active Directory jest katalogiem zsynchronizowane z usługami AD FS, zaufania usług AD FS domyślnie nie wysyła oświadczeń http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider albo, mimo że można ręcznie skonfigurować usługi AD FS, aby wysłać oświadczenie.
    > 
    > `ClaimTypes.NameIdentifies`Określa oświadczenie `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, której zapewnić usługi Azure Active Directory.  
    > 
    > 
15. Teraz Opublikuj zmiany. Kliknij prawym przyciskiem myszy projekt i kliknij przycisk **publikowania**.
16. Kliknij przycisk **ustawienia**, należy upewnić się, parametry połączenia z bazą danych SQL, wybierz **aktualizacji bazy danych** wprowadzania zmian schematu dla modelu, a następnie kliknij przycisk **publikowania**.
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. W przeglądarce przejdź do https://&lt;*appname*>.azurewebsites.net/workitems, a następnie kliknij przycisk **Utwórz nowy**.
18. Kliknij **AssignedToName** pole. Powinna zostać wyświetlona użytkowników i grup z dzierżawy usługi Azure Active Directory na liście rozwijanej. Wpisz, aby filtrować lub użyj `Up` lub `Down` klucza, lub kliknij, aby wybrać użytkownika lub grupę. 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. Kliknij przycisk **Utwórz** Aby zapisać zmiany. Następnie kliknij przycisk **Edytuj** na element roboczy utworzony, aby przyjrzeć się zachowaniu tego samego.

Gratulacje teraz używasz aplikacji biznesowych z platformy Azure z dostępem do katalogu! Istnieje wiele można zrobić za pomocą interfejsu API programu Graph. Zobacz [dokumentacja interfejsu API Azure AD Graph](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).

<a name="next"></a>

## <a name="next-step"></a>Następny krok
Jeśli potrzebujesz kontroli dostępu opartej na rolach (RBAC) dla aplikacji biznesowych z platformy azure, zobacz [aplikacji sieci Web-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) przykładowe przez zespół usługi Azure Active Directory. Przedstawiono sposób Włącz role w aplikacji usługi Azure Active Directory, a następnie zezwolić użytkownikom `[Authorize]` decoration.

Jeśli aplikacji biznesowych — musi mieć dostęp do danych lokalnych, zobacz [dostępu do zasobów lokalnych za pomocą połączeń hybrydowych w usłudze Azure App Service](web-sites-hybrid-connection-get-started.md).

<a name="bkmk_resources"></a>

## <a name="further-resources"></a>Dodatkowe zasoby
* [Uwierzytelnianie i autoryzację w usłudze Azure App Service](../app-service/app-service-authentication-overview.md)
* [Uwierzytelniania za pomocą lokalnej usługi Active Directory w aplikacji Azure](web-sites-authentication-authorization.md)
* [Tworzenie aplikacji biznesowych z uwierzytelniania usług AD FS na platformie Azure](web-sites-dotnet-lob-application-adfs.md)
* [Uwierzytelnianie usługi aplikacji i Azure AD Graph API](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [Microsoft Azure Active Directory przykłady i dokumentacja](https://github.com/AzureADSamples)
* [Usługa Azure Active Directory obsługiwane tokeny i oświadczenia](http://msdn.microsoft.com/library/azure/dn195587.aspx)
