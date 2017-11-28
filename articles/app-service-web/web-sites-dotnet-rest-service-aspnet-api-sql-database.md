---
title: aaaCreate interfejsu API REST na platformie Azure z platformy ASP.NET i bazy danych SQL | Dokumentacja firmy Microsoft
description: "Samouczek który jest przedstawienie sposobu toodeploy aplikacji, która używa hello tooan ASP.NET Web API aplikacji sieci web platformy Azure przy użyciu programu Visual Studio."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
writer: Rick-Anderson
manager: erikre
editor: 
ms.assetid: f4916fc0-ea08-41f7-846b-73e41bc88149
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/29/2016
ms.author: riande
ms.openlocfilehash: 1ef45dd1582bfda367e53c39f863164422ad678b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="c4b73-103">Tworzenie usługi REST przy użyciu interfejsu API sieci Web platformy ASP.NET i bazy danych SQL w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c4b73-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="c4b73-104">Ten samouczek pokazuje, jak toodeploy platformy ASP.NET sieci web aplikacji tooan [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) za pomocą kreatora Publikowanie w sieci Web hello w Visual Studio 2013 lub Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="c4b73-104">This tutorial shows how toodeploy an ASP.NET web app tooan [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using hello Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="c4b73-105">Możesz otworzyć bezpłatne konto platformy Azure, a jeśli nie masz jeszcze programu Visual Studio 2013, hello SDK automatycznie instaluje program Visual Studio 2013 for Web Express.</span><span class="sxs-lookup"><span data-stu-id="c4b73-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, hello SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="c4b73-106">Dlatego możesz rozpocząć tworzenie dla platformy Azure i całkowicie bezpłatne.</span><span class="sxs-lookup"><span data-stu-id="c4b73-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="c4b73-107">Ten samouczek zakłada, że nie masz wcześniejszego doświadczenia korzysta z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b73-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="c4b73-108">Na wykonanie kroków tego samouczka, będziesz mieć aplikację sieci web proste górę i w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-108">On completing this tutorial, you'll have a simple web app up and running in hello cloud.</span></span>

<span data-ttu-id="c4b73-109">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="c4b73-109">You'll learn:</span></span>

* <span data-ttu-id="c4b73-110">Jak tooenable komputer dla rozwoju platformy Azure, instalując hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="c4b73-110">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="c4b73-111">Jak toocreate programu Visual Studio ASP.NET MVC 5 projektu, a następnie opublikuj ją tooan aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b73-111">How toocreate a Visual Studio ASP.NET MVC 5 project and publish it tooan Azure app.</span></span>
* <span data-ttu-id="c4b73-112">W jaki sposób toouse hello tooenable interfejsu API sieci Web platformy ASP.NET wywołuje interfejs API Restful.</span><span class="sxs-lookup"><span data-stu-id="c4b73-112">How toouse hello ASP.NET Web API tooenable Restful API calls.</span></span>
* <span data-ttu-id="c4b73-113">Jak toouse SQL bazy danych toostore danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b73-113">How toouse a SQL database toostore data in Azure.</span></span>
* <span data-ttu-id="c4b73-114">Jak aplikacja toopublish aktualizuje tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c4b73-114">How toopublish application updates tooAzure.</span></span>

<span data-ttu-id="c4b73-115">Będzie tworzenia aplikacji sieci web proste listy kontaktów, która jest oparty na programie ASP.NET MVC 5 i używa hello ADO.NET Entity Framework dla dostępu do bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses hello ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="c4b73-116">Witaj następującej ilustracji przedstawiono hello ukończone aplikacji:</span><span class="sxs-lookup"><span data-stu-id="c4b73-116">hello following illustration shows hello completed application:</span></span>

![Zrzut ekranu przedstawiający witryny sieci web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-hello-project"></a><span data-ttu-id="c4b73-118">Utwórz projekt hello</span><span class="sxs-lookup"><span data-stu-id="c4b73-118">Create hello project</span></span>
1. <span data-ttu-id="c4b73-119">Uruchom program Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="c4b73-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="c4b73-120">Z hello **pliku** kliknij menu **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-120">From hello **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="c4b73-121">W hello **nowy projekt** okna dialogowego rozwiń **Visual C#** i wybierz **Web** , a następnie wybierz **aplikacji sieci Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-121">In hello **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="c4b73-122">Nadaj nazwę aplikacji hello **ContactManager** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-122">Name hello application **ContactManager** and click **OK**.</span></span>
   
    ![Okno dialogowe Nowy projekt](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="c4b73-124">W hello **nowy projekt ASP.NET** okno dialogowe, wybierz opcję hello **MVC** szablonu, sprawdź **interfejsu API sieci Web** , a następnie kliknij przycisk **Zmień uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-124">In hello **New ASP.NET Project** dialog box, select hello **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="c4b73-125">W hello **Zmień uwierzytelnianie** okno dialogowe, kliknij przycisk **bez uwierzytelniania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-125">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Bez uwierzytelniania](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="c4b73-127">Witaj przykładowej aplikacji, które tworzysz, nie będziesz mieć funkcji, które wymagają toolog użytkowników w.</span><span class="sxs-lookup"><span data-stu-id="c4b73-127">hello sample application you're creating won't have features that require users toolog in.</span></span> <span data-ttu-id="c4b73-128">Aby uzyskać informacje na temat tooimplement funkcji uwierzytelniania i autoryzacji, zobacz hello [następne kroki](#nextsteps) sekcji na końcu hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c4b73-128">For information about how tooimplement authentication and authorization features, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
6. <span data-ttu-id="c4b73-129">W hello **nowy projekt ASP.NET** okno dialogowe, upewnij się, że hello **hosta w chmurze hello** jest zaznaczony, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-129">In hello **New ASP.NET Project** dialog box, make sure hello **Host in hello Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="c4b73-130">Jeśli tooAzure nie zostały wcześniej zalogowany, będzie zostanie wyświetlony monit o toosign w.</span><span class="sxs-lookup"><span data-stu-id="c4b73-130">If you have not previously signed in tooAzure, you will be prompted toosign in.</span></span>

1. <span data-ttu-id="c4b73-131">Kreator konfiguracji Hello sugeruje unikatową nazwę, na podstawie *ContactManager* (zobacz poniższy obraz powitania).</span><span class="sxs-lookup"><span data-stu-id="c4b73-131">hello configuration wizard will suggest a unique name based on *ContactManager* (see hello image below).</span></span> <span data-ttu-id="c4b73-132">Wybierz region w pobliżu.</span><span class="sxs-lookup"><span data-stu-id="c4b73-132">Select a region near you.</span></span> <span data-ttu-id="c4b73-133">Można użyć [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello najniższy centrum danych opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="c4b73-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") toofind hello lowest latency data center.</span></span> 
2. <span data-ttu-id="c4b73-134">Jeśli nie utworzono serwera bazy danych przed, wybierz **Utwórz nowy serwer**, wprowadź nazwę bazy danych użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="c4b73-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Konfigurowanie witryny sieci Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="c4b73-136">Jeśli masz serwer bazy danych, użyj tego toocreate nową bazę danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-136">If you have a database server, use that toocreate a new database.</span></span> <span data-ttu-id="c4b73-137">Serwery bazy danych są cenne zasobów i zwykle mają toocreate wielu baz danych na powitania tego samego serwera do badania i rozwój zamiast serwera bazy danych dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-137">Database servers are a precious resource, and you generally want toocreate multiple databases on hello same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="c4b73-138">Upewnij się, że witryn sieci web i bazy danych znajdują się w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="c4b73-138">Make sure your web site and database are in hello same region.</span></span>

![Konfigurowanie witryny sieci Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-hello-page-header-and-footer"></a><span data-ttu-id="c4b73-140">Ustaw hello nagłówku i stopce strony</span><span class="sxs-lookup"><span data-stu-id="c4b73-140">Set hello page header and footer</span></span>
1. <span data-ttu-id="c4b73-141">W **Eksploratora rozwiązań**, rozwiń węzeł hello *Views\Shared* folder i otwórz hello *_Layout.cshtml* pliku.</span><span class="sxs-lookup"><span data-stu-id="c4b73-141">In **Solution Explorer**, expand hello *Views\Shared* folder and open hello *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml w Eksploratorze rozwiązań][newapp004]
2. <span data-ttu-id="c4b73-143">Zamień zawartość hello hello *Views\Shared_Layout.cshtml* pliku z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="c4b73-143">Replace hello contents of hello *Views\Shared_Layout.cshtml* file with hello following code:</span></span>

        <!DOCTYPE html>
        <html lang="en">
        <head>
            <meta charset="utf-8" />
            <title>@ViewBag.Title - Contact Manager</title>
            <link href="~/favicon.ico" rel="shortcut icon" type="image/x-icon" />
            <meta name="viewport" content="width=device-width" />
            @Styles.Render("~/Content/css")
            @Scripts.Render("~/bundles/modernizr")
        </head>
        <body>
            <header>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p class="site-title">@Html.ActionLink("Contact Manager", "Index", "Home")</p>
                    </div>
                </div>
            </header>
            <div id="body">
                @RenderSection("featured", required: false)
                <section class="content-wrapper main-content clear-fix">
                    @RenderBody()
                </section>
            </div>
            <footer>
                <div class="content-wrapper">
                    <div class="float-left">
                        <p>&copy; @DateTime.Now.Year - Contact Manager</p>
                    </div>
                </div>
            </footer>
            @Scripts.Render("~/bundles/jquery")
            @RenderSection("scripts", required: false)
        </body>
        </html>

<span data-ttu-id="c4b73-144">znaczników Hello powyżej nazwy aplikacji hello zmiany z "Moja aplikacja ASP.NET" za "Skontaktuj się z menedżerem" która usuwa hello łącza zbyt**Home**, **o** i **skontaktuj się z**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-144">hello markup above changes hello app name from "My ASP.NET App" too"Contact Manager", and it removes hello links too**Home**, **About** and **Contact**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="c4b73-145">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="c4b73-145">Run hello application locally</span></span>
1. <span data-ttu-id="c4b73-146">Naciśnij klawisze CTRL + F5 toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4b73-146">Press CTRL+F5 toorun hello application.</span></span>
   <span data-ttu-id="c4b73-147">Strona główna aplikacji Hello pojawia się w hello domyślnej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="c4b73-147">hello application home page appears in hello default browser.</span></span>
    <span data-ttu-id="c4b73-148">![Strona główna tooDo listy](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="c4b73-148">![tooDo List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="c4b73-149">To wszystko, czego potrzebujesz toodo dla aplikacji hello toocreate teraz wdrożony tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c4b73-149">This is all you need toodo for now toocreate hello application that you'll deploy tooAzure.</span></span> <span data-ttu-id="c4b73-150">Będzie później dodać funkcji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-150">Later you'll add database functionality.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="c4b73-151">Wdrażanie tooAzure aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="c4b73-151">Deploy hello application tooAzure</span></span>
1. <span data-ttu-id="c4b73-152">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** i wybierz **publikowania** z menu kontekstowego hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-152">In Visual Studio, right-click hello project in **Solution Explorer** and select **Publish** from hello context menu.</span></span>
   
    ![Opublikuj w menu kontekstowego projektu][PublishVSSolution]
   
    <span data-ttu-id="c4b73-154">Witaj **publikowanie w sieci Web** zostanie otwarty Kreator.</span><span class="sxs-lookup"><span data-stu-id="c4b73-154">hello **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="c4b73-155">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-155">Click **Publish**.</span></span>

![Karta Ustawienia](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="c4b73-157">Visual Studio rozpoczyna proces hello kopiowania hello pliki toohello serwerem Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b73-157">Visual Studio begins hello process of copying hello files toohello Azure server.</span></span> <span data-ttu-id="c4b73-158">Witaj **dane wyjściowe** okna pokazuje, jakie akcje wdrażania zostały pobrane i raporty pomyślne zakończenie hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="c4b73-158">hello **Output** window shows what deployment actions were taken and reports successful completion of hello deployment.</span></span>

1. <span data-ttu-id="c4b73-159">Hello przeglądarka domyślna automatycznie otwiera toohello adres URL witryny hello wdrożone.</span><span class="sxs-lookup"><span data-stu-id="c4b73-159">hello default browser automatically opens toohello URL of hello deployed site.</span></span>
   
   <span data-ttu-id="c4b73-160">utworzoną aplikację Hello jest teraz uruchomiona w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-160">hello application you created is now running in hello cloud.</span></span>
   
   ![Strona główna listy tooDo działające na platformie Azure][rxz2]

## <a name="add-a-database-toohello-application"></a><span data-ttu-id="c4b73-162">Dodaj aplikację toohello bazy danych</span><span class="sxs-lookup"><span data-stu-id="c4b73-162">Add a database toohello application</span></span>
<span data-ttu-id="c4b73-163">Następnie będzie zaktualizować hello MVC aplikacji tooadd hello możliwości toodisplay i Aktualizuj kontakty i zapisania danych hello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-163">Next, you'll update hello MVC application tooadd hello ability toodisplay and update contacts and store hello data in a database.</span></span> <span data-ttu-id="c4b73-164">Aplikacja Hello hello Entity Framework toocreate hello w bazie danych i tooread i aktualizacji danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-164">hello application will use hello Entity Framework toocreate hello database and tooread and update data in hello database.</span></span>

### <a name="add-data-model-classes-for-hello-contacts"></a><span data-ttu-id="c4b73-165">Dodawanie klasy modelu danych hello kontaktów</span><span class="sxs-lookup"><span data-stu-id="c4b73-165">Add data model classes for hello contacts</span></span>
<span data-ttu-id="c4b73-166">Można rozpocząć od tworzenia modelu danych proste w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c4b73-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="c4b73-167">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy folder modeli hello, kliknij przycisk **Dodaj**, a następnie **klasy**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-167">In **Solution Explorer**, right-click hello Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Dodaj klasę w menu kontekstowym folderu modeli][adddb001]
2. <span data-ttu-id="c4b73-169">W hello **Dodaj nowy element** okno dialogowe, hello nazwę nowego pliku klasy *Contact.cs*, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-169">In hello **Add New Item** dialog box, name hello new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Dodaj nowy element — okno dialogowe][adddb002]
3. <span data-ttu-id="c4b73-171">Zastąp zawartość pliku Contacts.cs hello hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="c4b73-171">Replace hello contents of hello Contacts.cs file with hello following code.</span></span>
   
        using System.Globalization;
        namespace ContactManager.Models
        {
            public class Contact
               {
                public int ContactId { get; set; }
                public string Name { get; set; }
                public string Address { get; set; }
                public string City { get; set; }
                public string State { get; set; }
                public string Zip { get; set; }
                public string Email { get; set; }
                public string Twitter { get; set; }
                public string Self
                {
                    get { return string.Format(CultureInfo.CurrentCulture,
                         "api/contacts/{0}", this.ContactId); }
                    set { }
                }
            }
        }

<span data-ttu-id="c4b73-172">Witaj **skontaktuj się z** klasa definiuje hello dane, które będą przechowywane dla każdego kontakt, a także klucz podstawowy, wartość ContactID wymaganej przez hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-172">hello **Contact** class defines hello data that you will store for each contact, plus a primary key, ContactID, that is needed by hello database.</span></span> <span data-ttu-id="c4b73-173">Więcej informacji o modelach danych można znaleźć w hello [następne kroki](#nextsteps) sekcji na końcu hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c4b73-173">You can get more information about data models in hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-toowork-with-hello-contacts"></a><span data-ttu-id="c4b73-174">Tworzenie stron sieci web, umożliwiające toowork użytkowników aplikacji hello kontaktów</span><span class="sxs-lookup"><span data-stu-id="c4b73-174">Create web pages that enable app users toowork with hello contacts</span></span>
<span data-ttu-id="c4b73-175">Witaj funkcja szkieletów hello ASP.NET MVC można automatycznie generować kod, który wykonuje tworzenia, odczytu, aktualizacji i usuwania (CRUD).</span><span class="sxs-lookup"><span data-stu-id="c4b73-175">hello ASP.NET MVC hello scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-hello-data"></a><span data-ttu-id="c4b73-176">Dodawanie kontrolera i widoku hello danych</span><span class="sxs-lookup"><span data-stu-id="c4b73-176">Add a Controller and a view for hello data</span></span>
1. <span data-ttu-id="c4b73-177">W **Eksploratora rozwiązań**, rozwiń folder kontrolery hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-177">In **Solution Explorer**, expand hello Controllers folder.</span></span>
2. <span data-ttu-id="c4b73-178">Tworzenie projektu hello **(Ctrl + Shift + B)**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-178">Build hello project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="c4b73-179">(Należy utworzyć projekt hello przed przy użyciu mechanizmu szkieletów.)</span><span class="sxs-lookup"><span data-stu-id="c4b73-179">(You must build hello project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="c4b73-180">Kliknij prawym przyciskiem myszy folder kontrolery hello, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-180">Right-click hello Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Dodawanie kontrolera w menu kontekstowym folderu kontrolerów][addcode001]
4. <span data-ttu-id="c4b73-182">W hello **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC z widokami używający narzędzia Entity Framework** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-182">In hello **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Dodawanie kontrolera](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="c4b73-184">Ustaw nazwę kontrolera hello zbyt**HomeController**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-184">Set hello controller name too**HomeController**.</span></span> <span data-ttu-id="c4b73-185">Wybierz **skontaktuj się z** jako klasy modelu.</span><span class="sxs-lookup"><span data-stu-id="c4b73-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="c4b73-186">Kliknij przycisk hello **nowy kontekst danych** przycisk i zaakceptuj domyślną hello "ContactManager.Models.ContactManagerContext" hello **nowy typ kontekstu danych**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-186">Click hello **New data context** button and accept hello default "ContactManager.Models.ContactManagerContext" for hello **New data context type**.</span></span> <span data-ttu-id="c4b73-187">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-187">Click **Add**.</span></span>

    <span data-ttu-id="c4b73-188">Okno dialogowe zostanie wyświetlony monit: "plik o nazwie hello HomeController już kończy działanie.</span><span class="sxs-lookup"><span data-stu-id="c4b73-188">A dialog box will prompt you: "A file with hello name HomeController already exits.</span></span> <span data-ttu-id="c4b73-189">Czy chcesz, aby tooreplace go? ".</span><span class="sxs-lookup"><span data-stu-id="c4b73-189">Do you want tooreplace it?".</span></span> <span data-ttu-id="c4b73-190">Kliknij przycisk **Yes** (Tak).</span><span class="sxs-lookup"><span data-stu-id="c4b73-190">Click **Yes**.</span></span> <span data-ttu-id="c4b73-191">Firma Microsoft są zastępowanie hello Home kontrolera utworzony za pomocą hello nowy projekt.</span><span class="sxs-lookup"><span data-stu-id="c4b73-191">We are overwriting hello Home Controller that was created with hello new project.</span></span> <span data-ttu-id="c4b73-192">Używamy hello nowe narzędzia główne kontrolera do naszej listy kontaktów.</span><span class="sxs-lookup"><span data-stu-id="c4b73-192">We will use hello new Home Controller for our contact list.</span></span>

    <span data-ttu-id="c4b73-193">Program Visual Studio tworzy metod kontrolera oraz widoki dla operacji CRUD bazy danych dla **skontaktuj się z** obiektów.</span><span class="sxs-lookup"><span data-stu-id="c4b73-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-hello-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="c4b73-194">Włącz migracji, tworzenie hello bazy danych, Dodawanie przykładowych danych i inicjatora danych</span><span class="sxs-lookup"><span data-stu-id="c4b73-194">Enable Migrations, create hello database, add sample data and a data initializer</span></span>
<span data-ttu-id="c4b73-195">następne zadanie Hello jest tooenable hello [migracje Code First](http://curah.microsoft.com/55220) funkcji w kolejności toocreate hello w bazie danych oparte na modelu danych hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="c4b73-195">hello next task is tooenable hello [Code First Migrations](http://curah.microsoft.com/55220) feature in order toocreate hello database based on hello data model you created.</span></span>

1. <span data-ttu-id="c4b73-196">W hello **narzędzia** menu, wybierz opcję **Menedżer pakietów biblioteki** , a następnie **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-196">In hello **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Konsola Menedżera pakietów w menu Narzędzia][addcode008]
2. <span data-ttu-id="c4b73-198">W hello **Konsola Menedżera pakietów** okna, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c4b73-198">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="c4b73-199">Witaj **enable-migrations,** polecenie tworzy *migracje* folderu i jego umieszcza w tym folderze *Configuration.cs* plik można edytować tooconfigure migracji.</span><span class="sxs-lookup"><span data-stu-id="c4b73-199">hello **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit tooconfigure Migrations.</span></span> 
3. <span data-ttu-id="c4b73-200">W hello **Konsola Menedżera pakietów** okna, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c4b73-200">In hello **Package Manager Console** window, enter hello following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="c4b73-201">Witaj **początkowego dodać migracji** polecenie generuje klasę o nazwie  **&lt;date_stamp&gt;początkowej** tworzącą hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-201">hello **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates hello database.</span></span> <span data-ttu-id="c4b73-202">Witaj pierwszy parametr ( *początkowej* ) jest nazwą hello toocreate dowolnego i używany hello pliku.</span><span class="sxs-lookup"><span data-stu-id="c4b73-202">hello first parameter ( *Initial* ) is arbitrary and used toocreate hello name of hello file.</span></span> <span data-ttu-id="c4b73-203">Widać hello nowe klasy pliki w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-203">You can see hello new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="c4b73-204">W hello **początkowej** klasy, hello **się** metoda tworzy hello tabeli kontaktów i hello **dół** — metoda (używany, gdy tooreturn toohello poprzedniego stanu) porzuca go.</span><span class="sxs-lookup"><span data-stu-id="c4b73-204">In hello **Initial** class, hello **Up** method creates hello Contacts table, and hello **Down** method (used when you want tooreturn toohello previous state) drops it.</span></span>
4. <span data-ttu-id="c4b73-205">Otwórz hello *Migrations\Configuration.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="c4b73-205">Open hello *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="c4b73-206">Dodaj hello następujące obszary nazw.</span><span class="sxs-lookup"><span data-stu-id="c4b73-206">Add hello following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="c4b73-207">Zastąp hello *inicjatora* metody z hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="c4b73-207">Replace hello *Seed* method with hello following code:</span></span>
   
        protected override void Seed(ContactManager.Models.ContactManagerContext context)
        {
            context.Contacts.AddOrUpdate(p => p.Name,
               new Contact
               {
                   Name = "Debra Garcia",
                   Address = "1234 Main St",
                   City = "Redmond",
                   State = "WA",
                   Zip = "10999",
                   Email = "debra@example.com",
                   Twitter = "debra_example"
               },
                new Contact
                {
                    Name = "Thorsten Weinrich",
                    Address = "5678 1st Ave W",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "thorsten@example.com",
                    Twitter = "thorsten_example"
                },
                new Contact
                {
                    Name = "Yuhong Li",
                    Address = "9012 State st",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "yuhong@example.com",
                    Twitter = "yuhong_example"
                },
                new Contact
                {
                    Name = "Jon Orton",
                    Address = "3456 Maple St",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "jon@example.com",
                    Twitter = "jon_example"
                },
                new Contact
                {
                    Name = "Diliana Alexieva-Bosseva",
                    Address = "7890 2nd Ave E",
                    City = "Redmond",
                    State = "WA",
                    Zip = "10999",
                    Email = "diliana@example.com",
                    Twitter = "diliana_example"
                }
                );
        }
   
    <span data-ttu-id="c4b73-208">Powyższy kod zostanie zainicjowany bazy danych hello hello informacje kontaktowe.</span><span class="sxs-lookup"><span data-stu-id="c4b73-208">This code above will initialize hello database with hello contact information.</span></span> <span data-ttu-id="c4b73-209">Aby uzyskać więcej informacji na wstępne wypełnianie bazy danych hello, zobacz [bazami danych debugowanie Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="c4b73-209">For more information on seeding hello database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="c4b73-210">W hello **Konsola Menedżera pakietów** wprowadź polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="c4b73-210">In hello **Package Manager Console** enter hello command:</span></span>
   
        update-database
   
    ![Polecenia konsoli Menedżera pakietów][addcode009]
   
    <span data-ttu-id="c4b73-212">Witaj **update-database** uruchamia hello pierwszej migracji, który tworzy hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-212">hello **update-database** runs hello first migration which creates hello database.</span></span> <span data-ttu-id="c4b73-213">Domyślnie program hello baza danych została utworzona jako baza danych programu SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="c4b73-213">By default, hello database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="c4b73-214">Naciśnij klawisze CTRL + F5 toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4b73-214">Press CTRL+F5 toorun hello application.</span></span> 

<span data-ttu-id="c4b73-215">Aplikacja Hello zawiera hello inicjatora danych oraz edytowanie, szczegóły i Usuń linki.</span><span class="sxs-lookup"><span data-stu-id="c4b73-215">hello application shows hello seed data and provides edit, details and delete links.</span></span>

![Widok MVC danych][rxz3]

## <a name="edit-hello-view"></a><span data-ttu-id="c4b73-217">Edytuj hello widoku</span><span class="sxs-lookup"><span data-stu-id="c4b73-217">Edit hello View</span></span>
1. <span data-ttu-id="c4b73-218">Otwórz hello *Views\Home\Index.cshtml* pliku.</span><span class="sxs-lookup"><span data-stu-id="c4b73-218">Open hello *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="c4b73-219">W następnym kroku hello, możemy spowoduje zamianę znaczników hello wygenerowany kod, który używa [jQuery](http://jquery.com/) i [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="c4b73-219">In hello next step, we will replace hello generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="c4b73-220">Ten kod pobiera hello listy kontaktów z przy użyciu interfejsu API sieci web i JSON, a następnie hello wiązania skontaktuj się z toohello danych interfejsu użytkownika przy użyciu knockout.js.</span><span class="sxs-lookup"><span data-stu-id="c4b73-220">This new code retrieves hello list of contacts from using web API and JSON and then binds hello contact data toohello UI using knockout.js.</span></span> <span data-ttu-id="c4b73-221">Aby uzyskać więcej informacji, zobacz hello [następne kroki](#nextsteps) sekcji na końcu hello tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="c4b73-221">For more information, see hello [Next Steps](#nextsteps) section at hello end of this tutorial.</span></span> 
2. <span data-ttu-id="c4b73-222">Zastąp zawartość pliku hello hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="c4b73-222">Replace hello contents of hello file with hello following code.</span></span>
   
        @model IEnumerable<ContactManager.Models.Contact>
        @{
            ViewBag.Title = "Home";
        }
        @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                function ContactsViewModel() {
                    var self = this;
                    self.contacts = ko.observableArray([]);
                    self.addContact = function () {
                        $.post("api/contacts",
                            $("#addContact").serialize(),
                            function (value) {
                                self.contacts.push(value);
                            },
                            "json");
                    }
                    self.removeContact = function (contact) {
                        $.ajax({
                            type: "DELETE",
                            url: contact.Self,
                            success: function () {
                                self.contacts.remove(contact);
                            }
                        });
                    }
   
                    $.getJSON("api/contacts", function (data) {
                        self.contacts(data);
                    });
                }
                ko.applyBindings(new ContactsViewModel());    
        </script>
        }
        <ul id="contacts" data-bind="foreach: contacts">
            <li class="ui-widget-content ui-corner-all">
                <h1 data-bind="text: Name" class="ui-widget-header"></h1>
                <div><span data-bind="text: $data.Address || 'Address?'"></span></div>
                <div>
                    <span data-bind="text: $data.City || 'City?'"></span>,
                    <span data-bind="text: $data.State || 'State?'"></span>
                    <span data-bind="text: $data.Zip || 'Zip?'"></span>
                </div>
                <div data-bind="if: $data.Email"><a data-bind="attr: { href: 'mailto:' + Email }, text: Email"></a></div>
                <div data-bind="ifnot: $data.Email"><span>Email?</span></div>
                <div data-bind="if: $data.Twitter"><a data-bind="attr: { href: 'http://twitter.com/' + Twitter }, text: '@@' + Twitter"></a></div>
                <div data-bind="ifnot: $data.Twitter"><span>Twitter?</span></div>
                <p><a data-bind="attr: { href: Self }, click: $root.removeContact" class="removeContact ui-state-default ui-corner-all">Remove</a></p>
            </li>
        </ul>
        <form id="addContact" data-bind="submit: addContact">
            <fieldset>
                <legend>Add New Contact</legend>
                <ol>
                    <li>
                        <label for="Name">Name</label>
                        <input type="text" name="Name" />
                    </li>
                    <li>
                        <label for="Address">Address</label>
                        <input type="text" name="Address" >
                    </li>
                    <li>
                        <label for="City">City</label>
                        <input type="text" name="City" />
                    </li>
                    <li>
                        <label for="State">State</label>
                        <input type="text" name="State" />
                    </li>
                    <li>
                        <label for="Zip">Zip</label>
                        <input type="text" name="Zip" />
                    </li>
                    <li>
                        <label for="Email">E-mail</label>
                        <input type="text" name="Email" />
                    </li>
                    <li>
                        <label for="Twitter">Twitter</label>
                        <input type="text" name="Twitter" />
                    </li>
                </ol>
                <input type="submit" value="Add" />
            </fieldset>
        </form>
3. <span data-ttu-id="c4b73-223">Kliknij prawym przyciskiem myszy folder zawartości hello, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element...** .</span><span class="sxs-lookup"><span data-stu-id="c4b73-223">Right-click hello Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Dodaj arkusz stylów w menu kontekstowym folder zawartości][addcode005]
4. <span data-ttu-id="c4b73-225">W hello **Dodaj nowy element** okna dialogowego wprowadź **styl** w hello pole wyszukiwania prawy górny, a następnie wybierz **arkusz stylów**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-225">In hello **Add New Item** dialog box, enter **Style** in hello upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="c4b73-226">![Dodaj nowy element — okno dialogowe][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="c4b73-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="c4b73-227">Nazwa pliku hello *Contacts.css* i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-227">Name hello file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="c4b73-228">Zastąp zawartość pliku hello hello hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="c4b73-228">Replace hello contents of hello file with hello following code.</span></span>
   
        .column {
            float: left;
            width: 50%;
            padding: 0;
            margin: 5px 0;
        }
        form ol {
            list-style-type: none;
            padding: 0;
            margin: 0;
        }
        form li {
            padding: 1px;
            margin: 3px;
        }
        form input[type="text"] {
            width: 100%;
        }
        #addContact {
            width: 300px;
            float: left;
            width:30%;
        }
        #contacts {
            list-style-type: none;
            margin: 0;
            padding: 0;
            float:left;
            width: 70%;
        }
        #contacts li {
            margin: 3px 3px 3px 0;
            padding: 1px;
            float: left;
            width: 300px;
            text-align: center;
            background-image: none;
            background-color: #F5F5F5;
        }
        #contacts li h1
        {
            padding: 0;
            margin: 0;
            background-image: none;
            background-color: Orange;
            color: White;
            font-family: Trebuchet MS, Tahoma, Verdana, Arial, sans-serif;
        }
        .removeContact, .viewImage
        {
            padding: 3px;
            text-decoration: none;
        }
   
    <span data-ttu-id="c4b73-229">Układ hello, kolory i style używane w aplikacji kontaktów Menedżerze hello użyjemy tego arkusza stylów.</span><span class="sxs-lookup"><span data-stu-id="c4b73-229">We will use this style sheet for hello layout, colors and styles used in hello contact manager app.</span></span>
6. <span data-ttu-id="c4b73-230">Otwórz hello *App_Start\BundleConfig.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="c4b73-230">Open hello *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="c4b73-231">Dodaj następującego kodu tooregister hello hello [Knockout](http://knockoutjs.com/index.html "KO") wtyczki.</span><span class="sxs-lookup"><span data-stu-id="c4b73-231">Add hello following code tooregister hello [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="c4b73-232">Ten przykład przy użyciu odcinania toosimplify dynamiczne JavaScript kod obsługujący szablony ekranów powitalnych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-232">This sample using knockout toosimplify dynamic JavaScript code that handles hello screen templates.</span></span>
8. <span data-ttu-id="c4b73-233">Modyfikowanie hello zawartość/css wpis tooregister hello *contacts.css* arkusza stylów.</span><span class="sxs-lookup"><span data-stu-id="c4b73-233">Modify hello contents/css entry tooregister hello *contacts.css* style sheet.</span></span> <span data-ttu-id="c4b73-234">Zmień powitania po wierszu:</span><span class="sxs-lookup"><span data-stu-id="c4b73-234">Change hello following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="c4b73-235">Aby:</span><span class="sxs-lookup"><span data-stu-id="c4b73-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="c4b73-236">W konsoli Menedżera pakietów hello uruchom następujące polecenie tooinstall odcinania hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-236">In hello Package Manager Console, run hello following command tooinstall Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-hello-web-api-restful-interface"></a><span data-ttu-id="c4b73-237">Dodawanie kontrolera interfejsu Web API Restful hello</span><span class="sxs-lookup"><span data-stu-id="c4b73-237">Add a controller for hello Web API Restful interface</span></span>
1. <span data-ttu-id="c4b73-238">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy kontrolerów i kliknij przycisk **Dodaj** , a następnie **kontrolera...**</span><span class="sxs-lookup"><span data-stu-id="c4b73-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="c4b73-239">W hello **Dodawanie szkieletu** okna dialogowego wprowadź **Web Kontroler interfejsu API 2 z akcjami używający narzędzia Entity Framework** , a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-239">In hello **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Dodaj Kontroler interfejsu API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="c4b73-241">W hello **Dodaj kontroler** okna dialogowego wprowadź "ContactsController" jako nazwę kontrolera.</span><span class="sxs-lookup"><span data-stu-id="c4b73-241">In hello **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="c4b73-242">Wybierz "Kontaktu (ContactManager.Models)" dla hello **klasa modelu**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-242">Select "Contact (ContactManager.Models)" for hello **Model class**.</span></span>  <span data-ttu-id="c4b73-243">Należy zachować wartość domyślną hello na powitania **klasa kontekstu danych**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-243">Keep hello default value for hello **Data context class**.</span></span> 
4. <span data-ttu-id="c4b73-244">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-244">Click **Add**.</span></span>

### <a name="run-hello-application-locally"></a><span data-ttu-id="c4b73-245">Uruchamianie aplikacji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="c4b73-245">Run hello application locally</span></span>
1. <span data-ttu-id="c4b73-246">Naciśnij klawisze CTRL + F5 toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4b73-246">Press CTRL+F5 toorun hello application.</span></span>
   
    ![Strona indeksu][intro001]
2. <span data-ttu-id="c4b73-248">Wprowadź kontaktu, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="c4b73-249">Aplikacja Hello zwraca toohello strony głównej i wyświetla hello kontaktu, który został wprowadzony.</span><span class="sxs-lookup"><span data-stu-id="c4b73-249">hello app returns toohello home page and displays hello contact you entered.</span></span>
   
    ![Strona indeksu z elementów listy zadań do wykonania][addwebapi004]
3. <span data-ttu-id="c4b73-251">W przeglądarce hello Dołącz **/api/contacts** toohello adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c4b73-251">In hello browser, append **/api/contacts** toohello URL.</span></span>
   
    <span data-ttu-id="c4b73-252">adres URL wynikowy Hello będzie podobny http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="c4b73-252">hello resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="c4b73-253">RESTful Hello dodaniu interfejsu API sieci web zwraca hello przechowywane kontaktów.</span><span class="sxs-lookup"><span data-stu-id="c4b73-253">hello RESTful web API you added returns hello stored contacts.</span></span> <span data-ttu-id="c4b73-254">Firefox i Chrome wyświetli hello dane w formacie XML.</span><span class="sxs-lookup"><span data-stu-id="c4b73-254">Firefox and Chrome will display hello data in XML format.</span></span>
   
    ![Strona indeksu z elementów listy zadań do wykonania][rxFFchrome]

    <span data-ttu-id="c4b73-256">Programu Internet Explorer będzie monitować tooopen lub zapisywać kontaktów hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-256">IE will prompt you tooopen or save hello contacts.</span></span>

    ![Okno dialogowe zapisywania interfejsu API sieci Web][addwebapi006]


    <span data-ttu-id="c4b73-258">Można także otworzyć hello zwrócił kontakty w Notatniku lub w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="c4b73-258">You can open hello returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="c4b73-259">Te dane wyjściowe mogą być używane przez inną aplikację, takich jak przenośnych strony sieci web lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4b73-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Okno dialogowe zapisywania interfejsu API sieci Web][addwebapi007]

    <span data-ttu-id="c4b73-261">**Ostrzeżenie o zabezpieczeniach**: W tym momencie aplikacja jest niebezpieczne i narażone tooCSRF ataku.</span><span class="sxs-lookup"><span data-stu-id="c4b73-261">**Security Warning**: At this point, your application is insecure and vulnerable tooCSRF attack.</span></span> <span data-ttu-id="c4b73-262">Później w samouczku hello zostanie usunięty tę lukę w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="c4b73-262">Later in hello tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="c4b73-263">Aby uzyskać więcej informacji, zobacz [ataków interfejsu uniemożliwia Cross-Site żądania Międzywitrynowego (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="c4b73-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="c4b73-264">Dodawanie ochrony XSRF</span><span class="sxs-lookup"><span data-stu-id="c4b73-264">Add XSRF Protection</span></span>
<span data-ttu-id="c4b73-265">Sfałszowaniem żądania między witrynami (znanej także jako XSRF lub CSRF) jest atak wykorzystujący aplikacje obsługiwane w sieci web, zgodnie z którymi złośliwą witrynę sieci Web może mieć wpływ hello interakcji między przeglądarką klienta i witryny sieci Web ufa tej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="c4b73-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence hello interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="c4b73-266">Tego rodzaju ataki są możliwe, ponieważ przeglądarki sieci web wysyła tokeny uwierzytelniania automatycznie z każdej tooa żądania witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c4b73-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request tooa website.</span></span> <span data-ttu-id="c4b73-267">canonical przykład Witaj jest pliku cookie uwierzytelniania, takich jak ASP. Biletu uwierzytelniania formularzy w sieci.</span><span class="sxs-lookup"><span data-stu-id="c4b73-267">hello canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="c4b73-268">Jednak tego rodzaju ataki może być celem witryn sieci Web, którego użyć dowolnego mechanizmu uwierzytelniania trwałe (takich jak uwierzytelnianie systemu Windows, Basic i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="c4b73-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="c4b73-269">Atak XSRF różni się od ataku wyłudzaniem informacji.</span><span class="sxs-lookup"><span data-stu-id="c4b73-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="c4b73-270">Wyłudzania wymagają interakcji z ofiara hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-270">Phishing attacks require interaction from hello victim.</span></span> <span data-ttu-id="c4b73-271">Atak wyłudzaniem informacji złośliwą witrynę sieci Web będzie naśladować hello docelowa witryna sieci Web i ofiara hello jest fooled do ujawnienia atakująca toohello poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="c4b73-271">In a phishing attack, a malicious website will mimic hello target website, and hello victim is fooled into providing sensitive information toohello attacker.</span></span> <span data-ttu-id="c4b73-272">W atak XSRF nie ma często bez interakcji z ofiara hello niezbędne.</span><span class="sxs-lookup"><span data-stu-id="c4b73-272">In an XSRF attack, there is often no interaction necessary from hello victim.</span></span> <span data-ttu-id="c4b73-273">Zamiast osoba atakująca hello jest jednostki uzależnionej w przeglądarce hello są automatycznie wysyłane wszystkie odpowiednie pliki cookie toohello docelowej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="c4b73-273">Rather, hello attacker is relying on hello browser automatically sending all relevant cookies toohello destination website.</span></span>

<span data-ttu-id="c4b73-274">Aby uzyskać więcej informacji, zobacz hello [Otwórz projekt zabezpieczeń aplikacji sieci Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="c4b73-274">For more information, see hello [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="c4b73-275">W **Eksploratora rozwiązań**, prawy **ContactManager** projekt i kliknij przycisk **Dodaj** , a następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="c4b73-276">Nazwa pliku hello *ValidateHttpAntiForgeryTokenAttribute.cs* i Dodaj hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="c4b73-276">Name hello file *ValidateHttpAntiForgeryTokenAttribute.cs* and add hello following code:</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Net;
        using System.Net.Http;
        using System.Web.Helpers;
        using System.Web.Http.Controllers;
        using System.Web.Http.Filters;
        using System.Web.Mvc;
        namespace ContactManager.Filters
        {
            public class ValidateHttpAntiForgeryTokenAttribute : AuthorizationFilterAttribute
            {
                public override void OnAuthorization(HttpActionContext actionContext)
                {
                    HttpRequestMessage request = actionContext.ControllerContext.Request;
                    try
                    {
                        if (IsAjaxRequest(request))
                        {
                            ValidateRequestHeader(request);
                        }
                        else
                        {
                            AntiForgery.Validate();
                        }
                    }
                    catch (HttpAntiForgeryException e)
                    {
                        actionContext.Response = request.CreateErrorResponse(HttpStatusCode.Forbidden, e);
                    }
                }
                private bool IsAjaxRequest(HttpRequestMessage request)
                {
                    IEnumerable<string> xRequestedWithHeaders;
                    if (request.Headers.TryGetValues("X-Requested-With", out xRequestedWithHeaders))
                    {
                        string headerValue = xRequestedWithHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(headerValue))
                        {
                            return String.Equals(headerValue, "XMLHttpRequest", StringComparison.OrdinalIgnoreCase);
                        }
                    }
                    return false;
                }
                private void ValidateRequestHeader(HttpRequestMessage request)
                {
                    string cookieToken = String.Empty;
                    string formToken = String.Empty;
                    IEnumerable<string> tokenHeaders;
                    if (request.Headers.TryGetValues("RequestVerificationToken", out tokenHeaders))
                    {
                        string tokenValue = tokenHeaders.FirstOrDefault();
                        if (!String.IsNullOrEmpty(tokenValue))
                        {
                            string[] tokens = tokenValue.Split(':');
                            if (tokens.Length == 2)
                            {
                                cookieToken = tokens[0].Trim();
                                formToken = tokens[1].Trim();
                            }
                        }
                    }
                    AntiForgery.Validate(cookieToken, formToken);
                }
            }
        }
3. <span data-ttu-id="c4b73-277">Dodaj następujące hello *przy użyciu* toohello instrukcji umów kontrolera, dlatego należy toohello dostępu **[ValidateHttpAntiForgeryToken]** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="c4b73-277">Add hello following *using* statement toohello contracts controller so you have access toohello **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="c4b73-278">Dodaj hello **[ValidateHttpAntiForgeryToken]** atrybutu metody Post toohello hello **ContactsController** tooprotect z XSRF zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="c4b73-278">Add hello **[ValidateHttpAntiForgeryToken]** attribute toohello Post methods of hello **ContactsController** tooprotect it from XSRF threats.</span></span> <span data-ttu-id="c4b73-279">Spowoduje dodanie toohello "PutContact", "PostContact" i **DeleteContact** metody akcji.</span><span class="sxs-lookup"><span data-stu-id="c4b73-279">You will add it toohello "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="c4b73-280">Aktualizacja hello *skryptów* sekcji hello *Views\Home\Index.cshtml* pliku tooinclude kodu tooget hello XSRF tokenów.</span><span class="sxs-lookup"><span data-stu-id="c4b73-280">Update hello *Scripts* section of hello *Views\Home\Index.cshtml* file tooinclude code tooget hello XSRF tokens.</span></span>
   
         @section Scripts {
            @Scripts.Render("~/bundles/knockout")
            <script type="text/javascript">
                @functions{
                   public string TokenHeaderValue()
                   {
                      string cookieToken, formToken;
                      AntiForgery.GetTokens(null, out cookieToken, out formToken);
                      return cookieToken + ":" + formToken;                
                   }
                }
   
               function ContactsViewModel() {
                  var self = this;
                  self.contacts = ko.observableArray([]);
                  self.addContact = function () {
   
                     $.ajax({
                        type: "post",
                        url: "api/contacts",
                        data: $("#addContact").serialize(),
                        dataType: "json",
                        success: function (value) {
                           self.contacts.push(value);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
                     });
   
                  }
                  self.removeContact = function (contact) {
                     $.ajax({
                        type: "DELETE",
                        url: contact.Self,
                        success: function () {
                           self.contacts.remove(contact);
                        },
                        headers: {
                           'RequestVerificationToken': '@TokenHeaderValue()'
                        }
   
                     });
                  }
   
                  $.getJSON("api/contacts", function (data) {
                     self.contacts(data);
                  });
               }
               ko.applyBindings(new ContactsViewModel());
            </script>
         }

## <a name="publish-hello-application-update-tooazure-and-sql-database"></a><span data-ttu-id="c4b73-281">Publikowanie tooAzure aktualizacji aplikacji hello i bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="c4b73-281">Publish hello application update tooAzure and SQL Database</span></span>
<span data-ttu-id="c4b73-282">Aplikacja hello toopublish, powtórz procedury hello, a następnie wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c4b73-282">toopublish hello application, you repeat hello procedure you followed earlier.</span></span>

1. <span data-ttu-id="c4b73-283">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt hello i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-283">In **Solution Explorer**, right click hello project and select **Publish**.</span></span>
   
    ![Publikowanie][rxP]
2. <span data-ttu-id="c4b73-285">Kliknij przycisk hello **ustawienia** kartę.</span><span class="sxs-lookup"><span data-stu-id="c4b73-285">Click hello **Settings** tab.</span></span>
3. <span data-ttu-id="c4b73-286">W obszarze **ContactsManagerContext(ContactsManagerContext)**, kliknij hello **v** toochange ikona *ciąg połączenia zdalnego* toohello parametry połączenia dla hello kontaktu Baza danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-286">Under **ContactsManagerContext(ContactsManagerContext)**, click hello **v** icon toochange *Remote connection string* toohello connection string for hello contact database.</span></span> <span data-ttu-id="c4b73-287">Kliknij przycisk **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-287">Click **ContactDB**.</span></span>
   
    ![Ustawienia](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="c4b73-289">Sprawdź pola hello **wykonaj migracje Code First (wywoływane po uruchomieniu aplikacji)**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-289">Check hello box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="c4b73-290">Kliknij przycisk **dalej** , a następnie kliknij przycisk **Podgląd**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="c4b73-291">Visual Studio zostanie wyświetlona lista hello pliki, które zostaną dodane lub zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="c4b73-291">Visual Studio displays a list of hello files that will be added or updated.</span></span>
6. <span data-ttu-id="c4b73-292">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="c4b73-292">Click **Publish**.</span></span>
   <span data-ttu-id="c4b73-293">Po zakończeniu wdrażania hello hello przeglądarce zostanie otwarty toohello strony głównej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-293">After hello deployment completes, hello browser opens toohello home page of hello application.</span></span>
   
    ![Strona indeksu z żadnych kontaktów][intro001]
   
    <span data-ttu-id="c4b73-295">Hello Visual Studio publikuje parametry połączenia hello procesu automatycznie konfigurowane w hello wdrożone *Web.config* pliku toopoint toohello SQL w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="c4b73-295">hello Visual Studio publish process automatically configured hello connection string in hello deployed *Web.config* file toopoint toohello SQL database.</span></span> <span data-ttu-id="c4b73-296">On również skonfigurowany migracje Code First tooautomatically hello uaktualnienia bazy danych toohello najnowszej wersji hello pierwszej aplikacji hello w czasie uzyskuje dostęp do bazy danych powitania po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="c4b73-296">It also configured Code First Migrations tooautomatically upgrade hello database toohello latest version hello first time hello application accesses hello database after deployment.</span></span>
   
    <span data-ttu-id="c4b73-297">W wyniku tej konfiguracji Code First utworzył hello bazę danych, uruchamiając kod hello w hello **początkowej** klasy, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="c4b73-297">As a result of this configuration, Code First created hello database by running hello code in hello **Initial** class that you created earlier.</span></span> <span data-ttu-id="c4b73-298">Po wdrożeniu jak hello pierwszego czasu hello nastąpiła tooaccess hello bazy danych tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c4b73-298">It did this hello first time hello application tried tooaccess hello database after deployment.</span></span>
7. <span data-ttu-id="c4b73-299">Wprowadź kontaktu, jak w przypadku uruchomienia aplikacji hello lokalnie, tooverify, który wdrażania bazy danych zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="c4b73-299">Enter a contact as you did when you ran hello app locally, tooverify that database deployment succeeded.</span></span>

<span data-ttu-id="c4b73-300">Po wyświetleniu elementu hello wprowadzany jest zapisywana i pojawia się na stronie kontaktów Menedżerze hello wiadomo, że ma ona przechowywana w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="c4b73-300">When you see that hello item you enter is saved and appears on hello contact manager page, you know that it has been stored in hello database.</span></span>

![Strona indeksu z kontaktów][addwebapi004]

<span data-ttu-id="c4b73-302">Aplikacja Hello jest teraz uruchomiona w chmurze hello przy użyciu bazy danych SQL toostore jego dane.</span><span class="sxs-lookup"><span data-stu-id="c4b73-302">hello application is now running in hello cloud, using SQL Database toostore its data.</span></span> <span data-ttu-id="c4b73-303">Po zakończeniu testowania aplikacji hello na platformie Azure, należy ją usunąć.</span><span class="sxs-lookup"><span data-stu-id="c4b73-303">After you finish testing hello application in Azure, delete it.</span></span> <span data-ttu-id="c4b73-304">Aplikacja Hello jest publiczna i nie ma dostępu toolimit mechanizmu.</span><span class="sxs-lookup"><span data-stu-id="c4b73-304">hello application is public and doesn't have a mechanism toolimit access.</span></span>

> [!NOTE]
> <span data-ttu-id="c4b73-305">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="c4b73-305">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="c4b73-306">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="c4b73-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="c4b73-307">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c4b73-307">Next Steps</span></span>
<span data-ttu-id="c4b73-308">Inny sposób toostore danych w aplikacji Azure jest toouse magazynu Azure, przechowywanie danych nierelacyjnych w formie hello obiekty BLOB i tabelach.</span><span class="sxs-lookup"><span data-stu-id="c4b73-308">Another way toostore data in an Azure application is toouse Azure storage, which provide non-relational data storage in hello form of blobs and tables.</span></span> <span data-ttu-id="c4b73-309">Hello następujące linki udostępniają więcej informacji na interfejs API sieci Web, ASP.NET MVC i Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="c4b73-309">hello following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="c4b73-310">[Wprowadzenie do korzystania z programu Entity Framework za pomocą MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="c4b73-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="c4b73-311">Wprowadzenie do tooASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="c4b73-311">Intro tooASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="c4b73-312">Pierwszy ASP.NET interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="c4b73-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="c4b73-313">Debugowanie WAWS</span><span class="sxs-lookup"><span data-stu-id="c4b73-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="c4b73-314">Zapisał tego samouczka i hello przykładowej aplikacji [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) z pomocą Dykstra Tomasz i Dorrans Marcin (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="c4b73-314">This tutorial and hello sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="c4b73-315">Wystaw opinię, co Ci się podoba lub co chcesz toosee zwiększona, nie tylko o samouczek hello, sam, ale także o produktach hello, przedstawiają go.</span><span class="sxs-lookup"><span data-stu-id="c4b73-315">Please leave feedback on what you liked or what you would like toosee improved, not only about hello tutorial itself but also about hello products that it demonstrates.</span></span> <span data-ttu-id="c4b73-316">Twoja opinia pomoże nam priorytety ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="c4b73-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="c4b73-317">Dbamy szczególnie w ustaleniu odsetek znajduje się w więcej automatyzacji procesu hello Konfigurowanie i wdrażanie hello bazy danych członkostwa.</span><span class="sxs-lookup"><span data-stu-id="c4b73-317">We are especially interested in finding out how much interest there is in more automation for hello process of configuring and deploying hello membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="c4b73-318">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="c4b73-318">What's changed</span></span>
* <span data-ttu-id="c4b73-319">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c4b73-319">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles toohello Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update hello Membership Database]:#ppd2
[setupdbenv]: #bkmk_setupdevenv
[setupwindowsazureenv]: #bkmk_setupwindowsazure
[createapplication]: #bkmk_createmvc4app
[deployapp1]: #bkmk_deploytowindowsazure1
[adddb]: #bkmk_addadatabase
[addcontroller]: #bkmk_addcontroller
[addwebapi]: #bkmk_addwebapi
[deploy2]: #bkmk_deploydatabaseupdate

<!-- links -->
[EFCodeFirstMVCTutorial]: http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
[dbcontext-link]: http://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx


<!-- images-->
[rxE]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxE.png
[rxP]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxP.png
[rx22]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/
[rxb2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxb2.png
[rxz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz.png
[rxzz]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxzz.png
[rxz2]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz2.png
[rxz3]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz3.png
[rxStyle]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxStyle.png
[rxz4]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz4.png
[rxz44]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxz44.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxPrevDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPrevDB.png
[rxOverwrite]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxOverwrite.png
[rxPWS]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxPWS.png
[rxNewCtx]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxNewCtx.png
[rxAddApiController]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxAddApiController.png
[rxFFchrome]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxFFchrome.png
[intro001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobil-intro-finished-web-app.png
[rxCreateWSwithDB]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rxCreateWSwithDB.png
[setup007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-setup-azure-site-004.png
[setup009]: ../Media/dntutmobile-setup-azure-site-006.png
[newapp002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-002.png
[newapp004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-createapp-004.png
[firsdeploy007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-005.png
[firsdeploy009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-deploy1-publish-007.png
[adddb001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-001.png
[adddb002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-adddatabase-002.png
[addcode001]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-context-menu.png
[addcode002]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-controller-dialog.png
[addcode004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-index-context.png
[addcode005]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-add-contents-context-menu.png
[addcode007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-controller-modify-bundleconfig-context.png
[addcode008]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-menu.png
[addcode009]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-migrations-package-manager-console.png
[addwebapi004]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-added-contact.png
[addwebapi006]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-save-returned-contacts.png
[addwebapi007]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/dntutmobile-webapi-contacts-in-notepad.png
[Add XSRF Protection]: #xsrf
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[Add XSRF Protection]: #xsrf
[ImportPublishSettings]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishSettings.png
[ImportPublishProfile]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ImportPublishProfile.png
[PublishVSSolution]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/PublishVSSolution.png
[ValidateConnection]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/ValidateConnection.png
[WebPIAzureSdk20NetVS12]: ./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/WebPIAzureSdk20NetVS12.png
[prevent-csrf-attacks]: http://www.asp.net/web-api/overview/security/preventing-cross-site-request-forgery-(csrf)-attacks

