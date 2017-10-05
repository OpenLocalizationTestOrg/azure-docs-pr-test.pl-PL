---
title: Tworzenie interfejsu API REST na platformie Azure z bazy danych SQL i programu ASP.NET | Dokumentacja firmy Microsoft
description: "Samouczek opisujący sposób wdrażania aplikacji, która używa interfejsu API sieci Web platformy ASP.NET dla aplikacji sieci web platformy Azure przy użyciu programu Visual Studio."
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
ms.openlocfilehash: 64c18f2cfabbb7af6ffd89b4c2a9095fca1cf799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-rest-service-using-aspnet-web-api-and-sql-database-in-azure-app-service"></a><span data-ttu-id="0a352-103">Tworzenie usługi REST przy użyciu interfejsu API sieci Web platformy ASP.NET i bazy danych SQL w usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0a352-103">Create a REST service using ASP.NET Web API and SQL Database in Azure App Service</span></span>
<span data-ttu-id="0a352-104">Ten samouczek przedstawia sposób wdrażania aplikacji sieci web platformy ASP.NET do [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) za pomocą kreatora Publikowanie w sieci Web w programie Visual Studio 2013 lub Visual Studio 2013 Community Edition.</span><span class="sxs-lookup"><span data-stu-id="0a352-104">This tutorial shows how to deploy an ASP.NET web app to an [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) by using the Publish Web wizard in Visual Studio 2013 or Visual Studio 2013 Community Edition.</span></span> 

<span data-ttu-id="0a352-105">Możesz otworzyć bezpłatne konto platformy Azure, a jeśli nie masz jeszcze programu Visual Studio 2013, zestaw SDK automatycznie instaluje program Visual Studio 2013 for Web Express.</span><span class="sxs-lookup"><span data-stu-id="0a352-105">You can open an Azure account for free, and if you don't already have Visual Studio 2013, the SDK automatically installs Visual Studio 2013 for Web Express.</span></span> <span data-ttu-id="0a352-106">Dlatego możesz rozpocząć tworzenie dla platformy Azure i całkowicie bezpłatne.</span><span class="sxs-lookup"><span data-stu-id="0a352-106">So you can start developing for Azure entirely for free.</span></span>

<span data-ttu-id="0a352-107">Ten samouczek zakłada, że nie masz wcześniejszego doświadczenia korzysta z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0a352-107">This tutorial assumes that you have no prior experience using Azure.</span></span> <span data-ttu-id="0a352-108">Na wykonanie kroków tego samouczka, będziesz mieć aplikację sieci web proste się działającą w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0a352-108">On completing this tutorial, you'll have a simple web app up and running in the cloud.</span></span>

<span data-ttu-id="0a352-109">Dowiesz się:</span><span class="sxs-lookup"><span data-stu-id="0a352-109">You'll learn:</span></span>

* <span data-ttu-id="0a352-110">Jak umożliwić tworzenie aplikacji platformy Azure na komputerze przez zainstalowanie zestawu Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="0a352-110">How to enable your machine for Azure development by installing the Azure SDK.</span></span>
* <span data-ttu-id="0a352-111">Jak utworzyć projekt Visual Studio ASP.NET MVC 5 i opublikowania go w usłudze aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="0a352-111">How to create a Visual Studio ASP.NET MVC 5 project and publish it to an Azure app.</span></span>
* <span data-ttu-id="0a352-112">Jak użyć interfejsu API sieci Web platformy ASP.NET w celu włączenia wywołania interfejsu API Restful.</span><span class="sxs-lookup"><span data-stu-id="0a352-112">How to use the ASP.NET Web API to enable Restful API calls.</span></span>
* <span data-ttu-id="0a352-113">Jak używać bazy danych SQL do przechowywania danych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0a352-113">How to use a SQL database to store data in Azure.</span></span>
* <span data-ttu-id="0a352-114">Jak opublikować aktualizacje aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0a352-114">How to publish application updates to Azure.</span></span>

<span data-ttu-id="0a352-115">Proste listy kontaktów aplikacji sieci web, który jest oparty na programie ASP.NET MVC 5 i używa programu ADO.NET Entity Framework dla dostępu do bazy danych będzie kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0a352-115">You'll build a simple contact list web application that is built on ASP.NET MVC 5 and uses the ADO.NET Entity Framework for database access.</span></span> <span data-ttu-id="0a352-116">Poniższa ilustracja przedstawia gotową aplikację:</span><span class="sxs-lookup"><span data-stu-id="0a352-116">The following illustration shows the completed application:</span></span>

![Zrzut ekranu przedstawiający witryny sieci web][intro001]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

### <a name="create-the-project"></a><span data-ttu-id="0a352-118">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="0a352-118">Create the project</span></span>
1. <span data-ttu-id="0a352-119">Uruchom program Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="0a352-119">Start Visual Studio 2013.</span></span>
2. <span data-ttu-id="0a352-120">Z **pliku** kliknij menu **nowy projekt**.</span><span class="sxs-lookup"><span data-stu-id="0a352-120">From the **File** menu click **New Project**.</span></span>
3. <span data-ttu-id="0a352-121">W **nowy projekt** okna dialogowego rozwiń **Visual C#** i wybierz **Web** , a następnie wybierz **aplikacji sieci Web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="0a352-121">In the **New Project** dialog box, expand **Visual C#** and select **Web**  and then select **ASP.NET Web Application**.</span></span> <span data-ttu-id="0a352-122">Nazwa aplikacji **ContactManager** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a352-122">Name the application **ContactManager** and click **OK**.</span></span>
   
    ![Okno dialogowe Nowy projekt](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr4.png)
4. <span data-ttu-id="0a352-124">W **nowy projekt ASP.NET** okno dialogowe, wybierz opcję **MVC** szablonu, sprawdź **interfejsu API sieci Web** , a następnie kliknij przycisk **Zmień uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="0a352-124">In the **New ASP.NET Project** dialog box, select the **MVC** template, check **Web API** and then click **Change Authentication**.</span></span>
5. <span data-ttu-id="0a352-125">W oknie dialogowym **Zmienianie uwierzytelniania** kliknij pozycję **Bez uwierzytelniania**, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a352-125">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span>
   
    ![Bez uwierzytelniania](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/GS13noauth.png)
   
    <span data-ttu-id="0a352-127">Przykładowej aplikacji, które tworzysz, nie będziesz mieć funkcji, które wymagają użytkownikom logować się.</span><span class="sxs-lookup"><span data-stu-id="0a352-127">The sample application you're creating won't have features that require users to log in.</span></span> <span data-ttu-id="0a352-128">Aby uzyskać informacje dotyczące sposobu implementowania funkcji uwierzytelniania i autoryzacji, zobacz [następne kroki](#nextsteps) sekcji na końcu tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="0a352-128">For information about how to implement authentication and authorization features, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
6. <span data-ttu-id="0a352-129">W **nowy projekt ASP.NET** okna dialogowego upewnij się, **Hostuj w chmurze** jest zaznaczony, a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a352-129">In the **New ASP.NET Project** dialog box, make sure the **Host in the Cloud** is checked and click **OK**.</span></span>

<span data-ttu-id="0a352-130">Jeśli użytkownik ma nie wcześniej zalogowany na platformie Azure, pojawi się monit do logowania.</span><span class="sxs-lookup"><span data-stu-id="0a352-130">If you have not previously signed in to Azure, you will be prompted to sign in.</span></span>

1. <span data-ttu-id="0a352-131">Kreator konfiguracji sugeruje unikatową nazwę, na podstawie *ContactManager* (zobacz obraz poniżej).</span><span class="sxs-lookup"><span data-stu-id="0a352-131">The configuration wizard will suggest a unique name based on *ContactManager* (see the image below).</span></span> <span data-ttu-id="0a352-132">Wybierz region w pobliżu.</span><span class="sxs-lookup"><span data-stu-id="0a352-132">Select a region near you.</span></span> <span data-ttu-id="0a352-133">Można użyć [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") można znaleźć Centrum danych najniższym opóźnieniu.</span><span class="sxs-lookup"><span data-stu-id="0a352-133">You can use [azurespeed.com](http://www.azurespeed.com/ "AzureSpeed.com") to find the lowest latency data center.</span></span> 
2. <span data-ttu-id="0a352-134">Jeśli nie utworzono serwera bazy danych przed, wybierz **Utwórz nowy serwer**, wprowadź nazwę bazy danych użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="0a352-134">If you haven't created a database server before, select **Create new server**, enter a database user name and password.</span></span>
   
    ![Konfigurowanie witryny sieci Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configAz.PNG)

<span data-ttu-id="0a352-136">Jeśli masz serwer bazy danych, użycie w celu utworzenia nowej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-136">If you have a database server, use that to create a new database.</span></span> <span data-ttu-id="0a352-137">Serwery bazy danych są cenne zasobów i zazwyczaj chcesz utworzyć wiele baz danych na tym samym serwerze do badania i rozwój zamiast serwera bazy danych dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-137">Database servers are a precious resource, and you generally want to create multiple databases on the same server for testing and development rather than creating a database server per database.</span></span> <span data-ttu-id="0a352-138">Upewnij się, że witryna sieci web i bazy danych są w tym samym regionie.</span><span class="sxs-lookup"><span data-stu-id="0a352-138">Make sure your web site and database are in the same region.</span></span>

![Konfigurowanie witryny sieci Web Azure](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/configWithDB.PNG)

### <a name="set-the-page-header-and-footer"></a><span data-ttu-id="0a352-140">Ustaw w nagłówku i stopce strony</span><span class="sxs-lookup"><span data-stu-id="0a352-140">Set the page header and footer</span></span>
1. <span data-ttu-id="0a352-141">W **Eksploratora rozwiązań**, rozwiń węzeł *Views\Shared* folderu i Otwórz *_Layout.cshtml* pliku.</span><span class="sxs-lookup"><span data-stu-id="0a352-141">In **Solution Explorer**, expand the *Views\Shared* folder and open the *_Layout.cshtml* file.</span></span>
   
    ![_Layout.cshtml w Eksploratorze rozwiązań][newapp004]
2. <span data-ttu-id="0a352-143">Zastąp zawartość *Views\Shared_Layout.cshtml* pliku następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="0a352-143">Replace the contents of the *Views\Shared_Layout.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="0a352-144">Powyżej znaczników zmienia nazwę aplikacji z "Moja aplikacja ASP.NET" na "Skontaktuj się z menedżerem" i spowoduje usunięcie łącza do **Home**, **o** i **skontaktuj się z**.</span><span class="sxs-lookup"><span data-stu-id="0a352-144">The markup above changes the app name from "My ASP.NET App" to "Contact Manager", and it removes the links to **Home**, **About** and **Contact**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="0a352-145">Uruchamianie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="0a352-145">Run the application locally</span></span>
1. <span data-ttu-id="0a352-146">Naciśnij klawisze CTRL+F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="0a352-146">Press CTRL+F5 to run the application.</span></span>
   <span data-ttu-id="0a352-147">Strona główna aplikacji jest wyświetlana w domyślnej przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="0a352-147">The application home page appears in the default browser.</span></span>
    <span data-ttu-id="0a352-148">![Do wykonania strony głównej](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span><span class="sxs-lookup"><span data-stu-id="0a352-148">![To Do List home page](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rr5.png)</span></span>

<span data-ttu-id="0a352-149">Wszystko co należy zrobić to teraz utworzyć aplikację, która będzie wdrażanie na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="0a352-149">This is all you need to do for now to create the application that you'll deploy to Azure.</span></span> <span data-ttu-id="0a352-150">Będzie później dodać funkcji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-150">Later you'll add database functionality.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="0a352-151">Wdrażanie aplikacji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="0a352-151">Deploy the application to Azure</span></span>
1. <span data-ttu-id="0a352-152">W programie Visual Studio, kliknij prawym przyciskiem myszy projekt w **Eksploratora rozwiązań** i wybierz **publikowania** z menu kontekstowego.</span><span class="sxs-lookup"><span data-stu-id="0a352-152">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
   
    ![Opublikuj w menu kontekstowego projektu][PublishVSSolution]
   
    <span data-ttu-id="0a352-154">**Publikowanie w sieci Web** zostanie otwarty Kreator.</span><span class="sxs-lookup"><span data-stu-id="0a352-154">The **Publish Web** wizard opens.</span></span>
2. <span data-ttu-id="0a352-155">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="0a352-155">Click **Publish**.</span></span>

![Karta Ustawienia](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/pw.png)

<span data-ttu-id="0a352-157">Visual Studio rozpoczyna proces kopiowania plików na serwer platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0a352-157">Visual Studio begins the process of copying the files to the Azure server.</span></span> <span data-ttu-id="0a352-158">**Dane wyjściowe** okna pokazuje, jakie akcje wdrażania zostały pobrane i raporty pomyślnego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="0a352-158">The **Output** window shows what deployment actions were taken and reports successful completion of the deployment.</span></span>

1. <span data-ttu-id="0a352-159">Przeglądarka domyślna automatycznie otwiera adres URL wdrożonej lokacji.</span><span class="sxs-lookup"><span data-stu-id="0a352-159">The default browser automatically opens to the URL of the deployed site.</span></span>
   
   <span data-ttu-id="0a352-160">Utworzoną aplikację jest teraz uruchomiona w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0a352-160">The application you created is now running in the cloud.</span></span>
   
   ![Do strony głównej listy wykonania działające na platformie Azure][rxz2]

## <a name="add-a-database-to-the-application"></a><span data-ttu-id="0a352-162">Dodaj bazę danych do aplikacji</span><span class="sxs-lookup"><span data-stu-id="0a352-162">Add a database to the application</span></span>
<span data-ttu-id="0a352-163">Następnie będzie aktualizowana aplikacji MVC, aby dodać możliwości, aby wyświetlić i zaktualizować kontaktów i przechowywanie danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-163">Next, you'll update the MVC application to add the ability to display and update contacts and store the data in a database.</span></span> <span data-ttu-id="0a352-164">Aplikacja będzie korzystać z programu Entity Framework, można utworzyć bazy danych i na odczytywanie i aktualizowanie danych w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-164">The application will use the Entity Framework to create the database and to read and update data in the database.</span></span>

### <a name="add-data-model-classes-for-the-contacts"></a><span data-ttu-id="0a352-165">Dodawanie klasy modelu danych dla kontaktów</span><span class="sxs-lookup"><span data-stu-id="0a352-165">Add data model classes for the contacts</span></span>
<span data-ttu-id="0a352-166">Można rozpocząć od tworzenia modelu danych proste w kodzie.</span><span class="sxs-lookup"><span data-stu-id="0a352-166">You begin by creating a simple data model in code.</span></span>

1. <span data-ttu-id="0a352-167">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy folder modeli, kliknij przycisk **Dodaj**, a następnie **klasy**.</span><span class="sxs-lookup"><span data-stu-id="0a352-167">In **Solution Explorer**, right-click the Models folder, click **Add**, and then **Class**.</span></span>
   
    ![Dodaj klasę w menu kontekstowym folderu modeli][adddb001]
2. <span data-ttu-id="0a352-169">W **Dodaj nowy element** okno dialogowe, nazwę nowego pliku klasy *Contact.cs*, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a352-169">In the **Add New Item** dialog box, name the new class file *Contact.cs*, and then click **Add**.</span></span>
   
    ![Dodaj nowy element — okno dialogowe][adddb002]
3. <span data-ttu-id="0a352-171">Zastąp zawartość pliku Contacts.cs następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="0a352-171">Replace the contents of the Contacts.cs file with the following code.</span></span>
   
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

<span data-ttu-id="0a352-172">**Skontaktuj się z** klasa definiuje dane, które będą przechowywane dla każdego kontakt, a także klucz podstawowy, wartość ContactID, który jest wymagany przez bazę danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-172">The **Contact** class defines the data that you will store for each contact, plus a primary key, ContactID, that is needed by the database.</span></span> <span data-ttu-id="0a352-173">Możesz uzyskać więcej informacji o modelach danych w [następne kroki](#nextsteps) sekcji na końcu tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="0a352-173">You can get more information about data models in the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span>

### <a name="create-web-pages-that-enable-app-users-to-work-with-the-contacts"></a><span data-ttu-id="0a352-174">Tworzenie stron sieci web, które umożliwiają użytkownikom aplikacji do pracy z kontaktów</span><span class="sxs-lookup"><span data-stu-id="0a352-174">Create web pages that enable app users to work with the contacts</span></span>
<span data-ttu-id="0a352-175">ASP.NET MVC funkcja szkieletów może automatycznie generować kod, który wykonuje tworzenia, odczytu, aktualizacji i usuwania (CRUD).</span><span class="sxs-lookup"><span data-stu-id="0a352-175">The ASP.NET MVC the scaffolding feature can automatically generate code that performs create, read, update, and delete (CRUD) actions.</span></span>

## <a name="add-a-controller-and-a-view-for-the-data"></a><span data-ttu-id="0a352-176">Dodawanie kontrolera i widoku danych</span><span class="sxs-lookup"><span data-stu-id="0a352-176">Add a Controller and a view for the data</span></span>
1. <span data-ttu-id="0a352-177">W **Eksploratora rozwiązań**, rozwiń folder kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="0a352-177">In **Solution Explorer**, expand the Controllers folder.</span></span>
2. <span data-ttu-id="0a352-178">Skompiluj projekt **(Ctrl + Shift + B)**.</span><span class="sxs-lookup"><span data-stu-id="0a352-178">Build the project **(Ctrl+Shift+B)**.</span></span> <span data-ttu-id="0a352-179">(Aby można było używać mechanizmu szkieletów musi skompilować projekt).</span><span class="sxs-lookup"><span data-stu-id="0a352-179">(You must build the project before using scaffolding mechanism.)</span></span> 
3. <span data-ttu-id="0a352-180">Kliknij prawym przyciskiem myszy folder kontrolery, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="0a352-180">Right-click the Controllers folder and click **Add**, and then click **Controller**.</span></span>
   
    ![Dodawanie kontrolera w menu kontekstowym folderu kontrolerów][addcode001]
4. <span data-ttu-id="0a352-182">W **Dodawanie szkieletu** okno dialogowe, wybierz opcję **kontroler MVC z widokami używający narzędzia Entity Framework** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a352-182">In the **Add Scaffold** dialog box, select **MVC Controller with views, using Entity Framework** and click **Add**.</span></span>
   
   ![Dodawanie kontrolera](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rrAC.png)
5. <span data-ttu-id="0a352-184">Ustaw nazwę kontrolera **HomeController**.</span><span class="sxs-lookup"><span data-stu-id="0a352-184">Set the controller name to **HomeController**.</span></span> <span data-ttu-id="0a352-185">Wybierz **skontaktuj się z** jako klasy modelu.</span><span class="sxs-lookup"><span data-stu-id="0a352-185">Select **Contact** as your model class.</span></span> <span data-ttu-id="0a352-186">Kliknij przycisk **nowy kontekst danych** przycisk i zaakceptuj wartość domyślną "ContactManager.Models.ContactManagerContext" dla **nowy typ kontekstu danych**.</span><span class="sxs-lookup"><span data-stu-id="0a352-186">Click the **New data context** button and accept the default "ContactManager.Models.ContactManagerContext" for the **New data context type**.</span></span> <span data-ttu-id="0a352-187">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a352-187">Click **Add**.</span></span>

    <span data-ttu-id="0a352-188">Okno dialogowe zostanie wyświetlony monit: "plik o nazwie HomeController już kończy działanie.</span><span class="sxs-lookup"><span data-stu-id="0a352-188">A dialog box will prompt you: "A file with the name HomeController already exits.</span></span> <span data-ttu-id="0a352-189">Czy chcesz go zastąpić? ".</span><span class="sxs-lookup"><span data-stu-id="0a352-189">Do you want to replace it?".</span></span> <span data-ttu-id="0a352-190">Kliknij przycisk **Yes** (Tak).</span><span class="sxs-lookup"><span data-stu-id="0a352-190">Click **Yes**.</span></span> <span data-ttu-id="0a352-191">Firma Microsoft są Zastępowanie kontrolera Narzędzia główne, który został utworzony nowy projekt.</span><span class="sxs-lookup"><span data-stu-id="0a352-191">We are overwriting the Home Controller that was created with the new project.</span></span> <span data-ttu-id="0a352-192">Firma Microsoft będzie używać nowego kontrolera Home naszej listy kontaktów.</span><span class="sxs-lookup"><span data-stu-id="0a352-192">We will use the new Home Controller for our contact list.</span></span>

    <span data-ttu-id="0a352-193">Program Visual Studio tworzy metod kontrolera oraz widoki dla operacji CRUD bazy danych dla **skontaktuj się z** obiektów.</span><span class="sxs-lookup"><span data-stu-id="0a352-193">Visual Studio creates controller methods and views for CRUD database operations for **Contact** objects.</span></span>

## <a name="enable-migrations-create-the-database-add-sample-data-and-a-data-initializer"></a><span data-ttu-id="0a352-194">Włącz migracji, utworzyć bazę danych, Dodawanie przykładowych danych i inicjatora danych</span><span class="sxs-lookup"><span data-stu-id="0a352-194">Enable Migrations, create the database, add sample data and a data initializer</span></span>
<span data-ttu-id="0a352-195">Następne zadanie jest umożliwienie [migracje Code First](http://curah.microsoft.com/55220) funkcji, aby można było utworzyć bazę danych opartą na modelu danych został utworzony.</span><span class="sxs-lookup"><span data-stu-id="0a352-195">The next task is to enable the [Code First Migrations](http://curah.microsoft.com/55220) feature in order to create the database based on the data model you created.</span></span>

1. <span data-ttu-id="0a352-196">W **narzędzia** menu, wybierz opcję **Menedżer pakietów biblioteki** , a następnie **Konsola Menedżera pakietów**.</span><span class="sxs-lookup"><span data-stu-id="0a352-196">In the **Tools** menu, select **Library Package Manager** and then **Package Manager Console**.</span></span>
   
    ![Konsola Menedżera pakietów w menu Narzędzia][addcode008]
2. <span data-ttu-id="0a352-198">W **Konsola Menedżera pakietów** okna, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="0a352-198">In the **Package Manager Console** window, enter the following command:</span></span>
   
        enable-migrations 
   
    <span data-ttu-id="0a352-199">**Enable-migrations,** polecenie tworzy *migracje* folderu i jego umieszcza w tym folderze *Configuration.cs* pliku, który można edytować w celu konfigurowania migracji.</span><span class="sxs-lookup"><span data-stu-id="0a352-199">The **enable-migrations** command creates a *Migrations* folder and it puts in that folder a *Configuration.cs* file that you can edit to configure Migrations.</span></span> 
3. <span data-ttu-id="0a352-200">W **Konsola Menedżera pakietów** okna, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="0a352-200">In the **Package Manager Console** window, enter the following command:</span></span>
   
        add-migration Initial
   
    <span data-ttu-id="0a352-201">**Początkowego dodać migracji** polecenie generuje klasę o nazwie  **&lt;date_stamp&gt;początkowej** tworzącą bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-201">The **add-migration Initial** command generates a class named **&lt;date_stamp&gt;Initial** that creates the database.</span></span> <span data-ttu-id="0a352-202">Pierwszy parametr ( *początkowej* ) jest dowolnego i używany do tworzenia nazwy pliku.</span><span class="sxs-lookup"><span data-stu-id="0a352-202">The first parameter ( *Initial* ) is arbitrary and used to create the name of the file.</span></span> <span data-ttu-id="0a352-203">Widać nowe pliki klasy w **Eksploratora rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="0a352-203">You can see the new class files in **Solution Explorer**.</span></span>
   
    <span data-ttu-id="0a352-204">W **początkowej** klasy **się** metoda tworzy tabeli kontaktów i **dół** — metoda (używane, jeśli chcesz powrócić do poprzedniego stanu) porzuca go.</span><span class="sxs-lookup"><span data-stu-id="0a352-204">In the **Initial** class, the **Up** method creates the Contacts table, and the **Down** method (used when you want to return to the previous state) drops it.</span></span>
4. <span data-ttu-id="0a352-205">Otwórz *Migrations\Configuration.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="0a352-205">Open the *Migrations\Configuration.cs* file.</span></span> 
5. <span data-ttu-id="0a352-206">Dodaj następujących przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="0a352-206">Add the following namespaces.</span></span> 
   
         using ContactManager.Models;
6. <span data-ttu-id="0a352-207">Zastąp *inicjatora* metodę z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="0a352-207">Replace the *Seed* method with the following code:</span></span>
   
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
   
    <span data-ttu-id="0a352-208">Powyższy kod zostanie zainicjowany bazy danych o informacje kontaktowe.</span><span class="sxs-lookup"><span data-stu-id="0a352-208">This code above will initialize the database with the contact information.</span></span> <span data-ttu-id="0a352-209">Aby uzyskać więcej informacji dotyczących wstępnego wypełniania bazy danych, zobacz [bazami danych debugowanie Entity Framework (EF)](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a352-209">For more information on seeding the database, see [Debugging Entity Framework (EF) DBs](http://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx).</span></span>
7. <span data-ttu-id="0a352-210">W **Konsola Menedżera pakietów** wprowadź polecenie:</span><span class="sxs-lookup"><span data-stu-id="0a352-210">In the **Package Manager Console** enter the command:</span></span>
   
        update-database
   
    ![Polecenia konsoli Menedżera pakietów][addcode009]
   
    <span data-ttu-id="0a352-212">**Update-database** uruchamia pierwszej migracji, które utworzy bazę danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-212">The **update-database** runs the first migration which creates the database.</span></span> <span data-ttu-id="0a352-213">Domyślnie baza danych została utworzona jako baza danych programu SQL Server Express LocalDB.</span><span class="sxs-lookup"><span data-stu-id="0a352-213">By default, the database is created as a SQL Server Express LocalDB database.</span></span>
8. <span data-ttu-id="0a352-214">Naciśnij klawisze CTRL+F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="0a352-214">Press CTRL+F5 to run the application.</span></span> 

<span data-ttu-id="0a352-215">Aplikacja zawiera dane inicjatora i łącza edycji, szczegóły i delete.</span><span class="sxs-lookup"><span data-stu-id="0a352-215">The application shows the seed data and provides edit, details and delete links.</span></span>

![Widok MVC danych][rxz3]

## <a name="edit-the-view"></a><span data-ttu-id="0a352-217">Edytuj widok</span><span class="sxs-lookup"><span data-stu-id="0a352-217">Edit the View</span></span>
1. <span data-ttu-id="0a352-218">Otwórz *Views\Home\Index.cshtml* pliku.</span><span class="sxs-lookup"><span data-stu-id="0a352-218">Open the *Views\Home\Index.cshtml* file.</span></span> <span data-ttu-id="0a352-219">W następnym kroku możemy spowoduje zamianę znaczników wygenerowanego kodu korzystającego z [jQuery](http://jquery.com/) i [Knockout.js](http://knockoutjs.com/).</span><span class="sxs-lookup"><span data-stu-id="0a352-219">In the next step, we will replace the generated markup with code that uses [jQuery](http://jquery.com/) and [Knockout.js](http://knockoutjs.com/).</span></span> <span data-ttu-id="0a352-220">Ten kod pobiera listy kontaktów z przy użyciu interfejsu API sieci web i JSON i czym wiąże się z działem dane do interfejsu użytkownika przy użyciu knockout.js.</span><span class="sxs-lookup"><span data-stu-id="0a352-220">This new code retrieves the list of contacts from using web API and JSON and then binds the contact data to the UI using knockout.js.</span></span> <span data-ttu-id="0a352-221">Aby uzyskać więcej informacji, zobacz [następne kroki](#nextsteps) sekcji na końcu tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="0a352-221">For more information, see the [Next Steps](#nextsteps) section at the end of this tutorial.</span></span> 
2. <span data-ttu-id="0a352-222">Zastąp zawartość pliku następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="0a352-222">Replace the contents of the file with the following code.</span></span>
   
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
3. <span data-ttu-id="0a352-223">Kliknij prawym przyciskiem myszy folder zawartości, a następnie kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element...** .</span><span class="sxs-lookup"><span data-stu-id="0a352-223">Right-click the Content folder and click **Add**, and then click **New Item...**.</span></span>
   
    ![Dodaj arkusz stylów w menu kontekstowym folder zawartości][addcode005]
4. <span data-ttu-id="0a352-225">W **Dodaj nowy element** okna dialogowego wprowadź **styl** w prawym górnym w polu wyszukiwania, a następnie wybierz **arkusz stylów**.</span><span class="sxs-lookup"><span data-stu-id="0a352-225">In the **Add New Item** dialog box, enter **Style** in the upper right search box and then select **Style Sheet**.</span></span>
    <span data-ttu-id="0a352-226">![Dodaj nowy element — okno dialogowe][rxStyle]</span><span class="sxs-lookup"><span data-stu-id="0a352-226">![Add New Item dialog box][rxStyle]</span></span>
5. <span data-ttu-id="0a352-227">Nadaj nazwę plikowi *Contacts.css* i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a352-227">Name the file *Contacts.css* and click **Add**.</span></span> <span data-ttu-id="0a352-228">Zastąp zawartość pliku następującym kodem.</span><span class="sxs-lookup"><span data-stu-id="0a352-228">Replace the contents of the file with the following code.</span></span>
   
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
   
    <span data-ttu-id="0a352-229">Układ, kolory i style używane w aplikacji kontaktów Menedżerze użyjemy tego arkusza stylów.</span><span class="sxs-lookup"><span data-stu-id="0a352-229">We will use this style sheet for the layout, colors and styles used in the contact manager app.</span></span>
6. <span data-ttu-id="0a352-230">Otwórz *App_Start\BundleConfig.cs* pliku.</span><span class="sxs-lookup"><span data-stu-id="0a352-230">Open the *App_Start\BundleConfig.cs* file.</span></span>
7. <span data-ttu-id="0a352-231">Dodaj następujący kod, aby zarejestrować [Knockout](http://knockoutjs.com/index.html "KO") wtyczki.</span><span class="sxs-lookup"><span data-stu-id="0a352-231">Add the following code to register the [Knockout](http://knockoutjs.com/index.html "KO") plugin.</span></span>
   
        bundles.Add(new ScriptBundle("~/bundles/knockout").Include(
                    "~/Scripts/knockout-{version}.js"));
    <span data-ttu-id="0a352-232">Ten przykład przy użyciu odcinania uprościć dynamiczny kod JavaScript, który obsługuje szablony ekranu.</span><span class="sxs-lookup"><span data-stu-id="0a352-232">This sample using knockout to simplify dynamic JavaScript code that handles the screen templates.</span></span>
8. <span data-ttu-id="0a352-233">Zmodyfikuj wpis zawartość/css, aby zarejestrować *contacts.css* arkusza stylów.</span><span class="sxs-lookup"><span data-stu-id="0a352-233">Modify the contents/css entry to register the *contacts.css* style sheet.</span></span> <span data-ttu-id="0a352-234">Zmień następujący wiersz:</span><span class="sxs-lookup"><span data-stu-id="0a352-234">Change the following line:</span></span>
   
                 bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/site.css"));
   <span data-ttu-id="0a352-235">Aby:</span><span class="sxs-lookup"><span data-stu-id="0a352-235">To:</span></span>
   
        bundles.Add(new StyleBundle("~/Content/css").Include(
                   "~/Content/bootstrap.css",
                   "~/Content/contacts.css",
                   "~/Content/site.css"));
9. <span data-ttu-id="0a352-236">W konsoli Menedżera pakietów uruchom następujące polecenie, aby zainstalować odcinania.</span><span class="sxs-lookup"><span data-stu-id="0a352-236">In the Package Manager Console, run the following command to install Knockout.</span></span>
   
        Install-Package knockoutjs

## <a name="add-a-controller-for-the-web-api-restful-interface"></a><span data-ttu-id="0a352-237">Dodawanie kontrolera dla interfejsu sieci Web interfejsu API Restful.</span><span class="sxs-lookup"><span data-stu-id="0a352-237">Add a controller for the Web API Restful interface</span></span>
1. <span data-ttu-id="0a352-238">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy kontrolerów i kliknij przycisk **Dodaj** , a następnie **kontrolera...**</span><span class="sxs-lookup"><span data-stu-id="0a352-238">In **Solution Explorer**, right-click Controllers and click **Add** and then **Controller....**</span></span> 
2. <span data-ttu-id="0a352-239">W **Dodawanie szkieletu** okna dialogowego wprowadź **Web Kontroler interfejsu API 2 z akcjami używający narzędzia Entity Framework** , a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a352-239">In the **Add Scaffold** dialog box, enter **Web API 2 Controller with actions, using Entity Framework** and then click **Add**.</span></span>
   
    ![Dodaj Kontroler interfejsu API](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt1.png)
3. <span data-ttu-id="0a352-241">W **Dodaj kontroler** okna dialogowego wprowadź "ContactsController" jako nazwę kontrolera.</span><span class="sxs-lookup"><span data-stu-id="0a352-241">In the **Add Controller** dialog box, enter "ContactsController" as your controller name.</span></span> <span data-ttu-id="0a352-242">Wybierz "Kontaktu (ContactManager.Models)" dla **klasa modelu**.</span><span class="sxs-lookup"><span data-stu-id="0a352-242">Select "Contact (ContactManager.Models)" for the **Model class**.</span></span>  <span data-ttu-id="0a352-243">Należy zachować wartość domyślną dla **klasa kontekstu danych**.</span><span class="sxs-lookup"><span data-stu-id="0a352-243">Keep the default value for the **Data context class**.</span></span> 
4. <span data-ttu-id="0a352-244">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a352-244">Click **Add**.</span></span>

### <a name="run-the-application-locally"></a><span data-ttu-id="0a352-245">Uruchamianie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="0a352-245">Run the application locally</span></span>
1. <span data-ttu-id="0a352-246">Naciśnij klawisze CTRL+F5, aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="0a352-246">Press CTRL+F5 to run the application.</span></span>
   
    ![Strona indeksu][intro001]
2. <span data-ttu-id="0a352-248">Wprowadź kontaktu, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="0a352-248">Enter a contact and click **Add**.</span></span> <span data-ttu-id="0a352-249">Aplikacja zwraca do strony głównej i wyświetla kontaktu, który został wprowadzony.</span><span class="sxs-lookup"><span data-stu-id="0a352-249">The app returns to the home page and displays the contact you entered.</span></span>
   
    ![Strona indeksu z elementów listy zadań do wykonania][addwebapi004]
3. <span data-ttu-id="0a352-251">W przeglądarce, dołącz **/api/contacts** do adresu URL.</span><span class="sxs-lookup"><span data-stu-id="0a352-251">In the browser, append **/api/contacts** to the URL.</span></span>
   
    <span data-ttu-id="0a352-252">Adres URL wynikowy będzie podobny http://localhost:1234/api/contacts.</span><span class="sxs-lookup"><span data-stu-id="0a352-252">The resulting URL will resemble http://localhost:1234/api/contacts.</span></span> <span data-ttu-id="0a352-253">RESTful interfejsu API sieci web dodano zwraca przechowywanych kontaktów.</span><span class="sxs-lookup"><span data-stu-id="0a352-253">The RESTful web API you added returns the stored contacts.</span></span> <span data-ttu-id="0a352-254">Firefox i Chrome będą wyświetlane dane w formacie XML.</span><span class="sxs-lookup"><span data-stu-id="0a352-254">Firefox and Chrome will display the data in XML format.</span></span>
   
    ![Strona indeksu z elementów listy zadań do wykonania][rxFFchrome]

    <span data-ttu-id="0a352-256">IE spowoduje wyświetlenie monitu o otworzyć lub zapisać kontaktów.</span><span class="sxs-lookup"><span data-stu-id="0a352-256">IE will prompt you to open or save the contacts.</span></span>

    ![Okno dialogowe zapisywania interfejsu API sieci Web][addwebapi006]


    <span data-ttu-id="0a352-258">Możesz otworzyć zwrócony kontakty w Notatniku lub w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="0a352-258">You can open the returned contacts in notepad or a browser.</span></span>

    <span data-ttu-id="0a352-259">Te dane wyjściowe mogą być używane przez inną aplikację, takich jak przenośnych strony sieci web lub aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a352-259">This output can be consumed by another application such as mobile web page or application.</span></span>

    ![Okno dialogowe zapisywania interfejsu API sieci Web][addwebapi007]

    <span data-ttu-id="0a352-261">**Ostrzeżenie o zabezpieczeniach**: W tym momencie aplikacja jest niebezpieczne i narażone na atak CSRF.</span><span class="sxs-lookup"><span data-stu-id="0a352-261">**Security Warning**: At this point, your application is insecure and vulnerable to CSRF attack.</span></span> <span data-ttu-id="0a352-262">W dalszej części tego samouczka zostanie usunięty tę lukę w zabezpieczeniach.</span><span class="sxs-lookup"><span data-stu-id="0a352-262">Later in the tutorial we will remove this vulnerability.</span></span> <span data-ttu-id="0a352-263">Aby uzyskać więcej informacji, zobacz [ataków interfejsu uniemożliwia Cross-Site żądania Międzywitrynowego (CSRF)][prevent-csrf-attacks].</span><span class="sxs-lookup"><span data-stu-id="0a352-263">For more information see [Preventing Cross-Site Request Forgery (CSRF) Attacks][prevent-csrf-attacks].</span></span>
## <a name="add-xsrf-protection"></a><span data-ttu-id="0a352-264">Dodawanie ochrony XSRF</span><span class="sxs-lookup"><span data-stu-id="0a352-264">Add XSRF Protection</span></span>
<span data-ttu-id="0a352-265">Sfałszowaniem żądania między witrynami (znanej także jako XSRF lub CSRF) jest atak wykorzystujący aplikacje obsługiwane w sieci web, zgodnie z którymi złośliwą witrynę sieci Web może mieć wpływ interakcji między przeglądarką klienta i witryny sieci Web ufa tej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="0a352-265">Cross-site request forgery (also known as XSRF or CSRF) is an attack against web-hosted applications whereby a malicious website can influence the interaction between a client browser and a website trusted by that browser.</span></span> <span data-ttu-id="0a352-266">Tego rodzaju ataki są możliwe, ponieważ przeglądarki sieci web wysyła tokeny uwierzytelniania automatycznie z każdym żądaniem do witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0a352-266">These attacks are made possible because web browsers will send authentication tokens automatically with every request to a website.</span></span> <span data-ttu-id="0a352-267">Canonical przykładem jest pliku cookie uwierzytelniania, takich jak ASP. Biletu uwierzytelniania formularzy w sieci.</span><span class="sxs-lookup"><span data-stu-id="0a352-267">The canonical example is an authentication cookie, such as ASP.NET's Forms Authentication ticket.</span></span> <span data-ttu-id="0a352-268">Jednak tego rodzaju ataki może być celem witryn sieci Web, którego użyć dowolnego mechanizmu uwierzytelniania trwałe (takich jak uwierzytelnianie systemu Windows, Basic i tak dalej).</span><span class="sxs-lookup"><span data-stu-id="0a352-268">However, websites which use any persistent authentication mechanism (such as Windows Authentication, Basic, and so forth) can be targeted by these attacks.</span></span>

<span data-ttu-id="0a352-269">Atak XSRF różni się od ataku wyłudzaniem informacji.</span><span class="sxs-lookup"><span data-stu-id="0a352-269">An XSRF attack is distinct from a phishing attack.</span></span> <span data-ttu-id="0a352-270">Wyłudzania wymagają interakcji z ofiary.</span><span class="sxs-lookup"><span data-stu-id="0a352-270">Phishing attacks require interaction from the victim.</span></span> <span data-ttu-id="0a352-271">Atak phishing złośliwą witrynę sieci Web będzie naśladować docelowa witryna sieci Web i ofiary jest fooled na dostarczanie informacji poufnych dla osoby atakującej.</span><span class="sxs-lookup"><span data-stu-id="0a352-271">In a phishing attack, a malicious website will mimic the target website, and the victim is fooled into providing sensitive information to the attacker.</span></span> <span data-ttu-id="0a352-272">W atak XSRF nie ma często bez interakcji z ofiary niezbędne.</span><span class="sxs-lookup"><span data-stu-id="0a352-272">In an XSRF attack, there is often no interaction necessary from the victim.</span></span> <span data-ttu-id="0a352-273">Osoba atakująca jest raczej jednostki uzależnionej w przeglądarce, wszystkie odpowiednie pliki cookie są automatycznie wysyłane do docelowej witryny sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0a352-273">Rather, the attacker is relying on the browser automatically sending all relevant cookies to the destination website.</span></span>

<span data-ttu-id="0a352-274">Aby uzyskać więcej informacji, zobacz [Otwórz projekt zabezpieczeń aplikacji sieci Web](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span><span class="sxs-lookup"><span data-stu-id="0a352-274">For more information, see the [Open Web Application Security Project](https://www.owasp.org/index.php/Main_Page) (OWASP) [XSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_\(CSRF\)).</span></span>

1. <span data-ttu-id="0a352-275">W **Eksploratora rozwiązań**, prawy **ContactManager** projekt i kliknij przycisk **Dodaj** , a następnie kliknij przycisk **klasy**.</span><span class="sxs-lookup"><span data-stu-id="0a352-275">In **Solution Explorer**, right **ContactManager** project and click **Add** and then click **Class**.</span></span>
2. <span data-ttu-id="0a352-276">Nadaj nazwę plikowi *ValidateHttpAntiForgeryTokenAttribute.cs* i Dodaj następujący kod:</span><span class="sxs-lookup"><span data-stu-id="0a352-276">Name the file *ValidateHttpAntiForgeryTokenAttribute.cs* and add the following code:</span></span>
   
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
3. <span data-ttu-id="0a352-277">Dodaj następujące *przy użyciu* instrukcji do kontrolera kontrakty, musisz mieć dostęp do **[ValidateHttpAntiForgeryToken]** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0a352-277">Add the following *using* statement to the contracts controller so you have access to the **[ValidateHttpAntiForgeryToken]** attribute.</span></span>
   
        using ContactManager.Filters;
4. <span data-ttu-id="0a352-278">Dodaj **[ValidateHttpAntiForgeryToken]** atrybut do metody Post **ContactsController** do ochrony przed zagrożeniami XSRF.</span><span class="sxs-lookup"><span data-stu-id="0a352-278">Add the **[ValidateHttpAntiForgeryToken]** attribute to the Post methods of the **ContactsController** to protect it from XSRF threats.</span></span> <span data-ttu-id="0a352-279">Doda do "PutContact", "PostContact" i **DeleteContact** metody akcji.</span><span class="sxs-lookup"><span data-stu-id="0a352-279">You will add it to the "PutContact",  "PostContact" and **DeleteContact** action methods.</span></span>
   
        [ValidateHttpAntiForgeryToken]
            public IHttpActionResult PutContact(int id, Contact contact)
            {
5. <span data-ttu-id="0a352-280">Aktualizacja *skryptów* sekcji *Views\Home\Index.cshtml* pliku, aby uwzględnić kod w celu uzyskania XSRF tokenów.</span><span class="sxs-lookup"><span data-stu-id="0a352-280">Update the *Scripts* section of the *Views\Home\Index.cshtml* file to include code to get the XSRF tokens.</span></span>
   
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

## <a name="publish-the-application-update-to-azure-and-sql-database"></a><span data-ttu-id="0a352-281">Publikowanie aktualizacji aplikacji na platformie Azure oraz bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="0a352-281">Publish the application update to Azure and SQL Database</span></span>
<span data-ttu-id="0a352-282">Aby opublikować aplikację, możesz Powtórz procedurę, które zostały wykonane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0a352-282">To publish the application, you repeat the procedure you followed earlier.</span></span>

1. <span data-ttu-id="0a352-283">W **Eksploratora rozwiązań**, kliknij prawym przyciskiem myszy projekt i wybierz **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="0a352-283">In **Solution Explorer**, right click the project and select **Publish**.</span></span>
   
    ![Publikowanie][rxP]
2. <span data-ttu-id="0a352-285">Kliknij kartę **Ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="0a352-285">Click the **Settings** tab.</span></span>
3. <span data-ttu-id="0a352-286">W obszarze **ContactsManagerContext(ContactsManagerContext)**, kliknij przycisk **v** ikonę, aby zmienić *ciąg połączenia zdalnego* w parametrach połączenia dla bazy danych kontaktowych.</span><span class="sxs-lookup"><span data-stu-id="0a352-286">Under **ContactsManagerContext(ContactsManagerContext)**, click the **v** icon to change *Remote connection string* to the connection string for the contact database.</span></span> <span data-ttu-id="0a352-287">Kliknij przycisk **ContactDB**.</span><span class="sxs-lookup"><span data-stu-id="0a352-287">Click **ContactDB**.</span></span>
   
    ![Ustawienia](./media/web-sites-dotnet-rest-service-aspnet-api-sql-database/rt5.png)
4. <span data-ttu-id="0a352-289">Pole wyboru dla **wykonaj migracje Code First (wywoływane po uruchomieniu aplikacji)**.</span><span class="sxs-lookup"><span data-stu-id="0a352-289">Check the box for **Execute Code First Migrations (runs on application start)**.</span></span>
5. <span data-ttu-id="0a352-290">Kliknij przycisk **dalej** , a następnie kliknij przycisk **Podgląd**.</span><span class="sxs-lookup"><span data-stu-id="0a352-290">Click **Next** and then click **Preview**.</span></span> <span data-ttu-id="0a352-291">Visual Studio zostanie wyświetlona lista plików, które zostaną dodane lub zaktualizowane.</span><span class="sxs-lookup"><span data-stu-id="0a352-291">Visual Studio displays a list of the files that will be added or updated.</span></span>
6. <span data-ttu-id="0a352-292">Kliknij przycisk **Opublikuj**.</span><span class="sxs-lookup"><span data-stu-id="0a352-292">Click **Publish**.</span></span>
   <span data-ttu-id="0a352-293">Po zakończeniu wdrożenia, przeglądarka otworzy się do strony głównej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0a352-293">After the deployment completes, the browser opens to the home page of the application.</span></span>
   
    ![Strona indeksu z żadnych kontaktów][intro001]
   
    <span data-ttu-id="0a352-295">Visual Studio automatycznie publikowania procesu skonfigurowanych parametrów połączenia w wdrożone *Web.config* pliku do punktu z bazą danych SQL.</span><span class="sxs-lookup"><span data-stu-id="0a352-295">The Visual Studio publish process automatically configured the connection string in the deployed *Web.config* file to point to the SQL database.</span></span> <span data-ttu-id="0a352-296">On również skonfigurowany migracje Code First automatycznie przy pierwszym aplikacja uzyskuje dostęp do bazy danych po wdrożeniu uaktualnienie do najnowszej wersji bazy danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-296">It also configured Code First Migrations to automatically upgrade the database to the latest version the first time the application accesses the database after deployment.</span></span>
   
    <span data-ttu-id="0a352-297">W wyniku tej konfiguracji Code First baza danych utworzona uruchamiając kod na **początkowej** klasy, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="0a352-297">As a result of this configuration, Code First created the database by running the code in the **Initial** class that you created earlier.</span></span> <span data-ttu-id="0a352-298">Jak to aplikacja próbowała dostęp do bazy danych po wdrożeniu po raz pierwszy.</span><span class="sxs-lookup"><span data-stu-id="0a352-298">It did this the first time the application tried to access the database after deployment.</span></span>
7. <span data-ttu-id="0a352-299">Wprowadź kontaktu, tak jak po uruchomieniu aplikacji lokalnie, aby sprawdzić, czy wdrożenie bazy danych zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="0a352-299">Enter a contact as you did when you ran the app locally, to verify that database deployment succeeded.</span></span>

<span data-ttu-id="0a352-300">Gdy pojawi się, że element, który możesz wprowadzić jest zapisywana i jest wyświetlany na stronie kontaktów Menedżerze, wiadomo, że ma ona przechowywana w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-300">When you see that the item you enter is saved and appears on the contact manager page, you know that it has been stored in the database.</span></span>

![Strona indeksu z kontaktów][addwebapi004]

<span data-ttu-id="0a352-302">Aplikacja jest teraz uruchomiona w chmurze przy użyciu bazy danych SQL do przechowywania danych.</span><span class="sxs-lookup"><span data-stu-id="0a352-302">The application is now running in the cloud, using SQL Database to store its data.</span></span> <span data-ttu-id="0a352-303">Po zakończeniu testowania aplikacji na platformie Azure, należy ją usunąć.</span><span class="sxs-lookup"><span data-stu-id="0a352-303">After you finish testing the application in Azure, delete it.</span></span> <span data-ttu-id="0a352-304">Aplikacja nie jest publiczny i nie ma mechanizmu, aby ograniczyć dostęp.</span><span class="sxs-lookup"><span data-stu-id="0a352-304">The application is public and doesn't have a mechanism to limit access.</span></span>

> [!NOTE]
> <span data-ttu-id="0a352-305">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="0a352-305">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0a352-306">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="0a352-306">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0a352-307">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0a352-307">Next Steps</span></span>
<span data-ttu-id="0a352-308">Inny sposób przechowywania danych w aplikacji Azure jest użycie magazynu Azure, które zapewniają magazynu danych nierelacyjnych w formie obiektów blob i tabelach.</span><span class="sxs-lookup"><span data-stu-id="0a352-308">Another way to store data in an Azure application is to use Azure storage, which provide non-relational data storage in the form of blobs and tables.</span></span> <span data-ttu-id="0a352-309">Poniższe linki udostępniają więcej informacji na interfejs API sieci Web, ASP.NET MVC i Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="0a352-309">The following links provide more information on Web API, ASP.NET MVC and Window Azure.</span></span>

* <span data-ttu-id="0a352-310">[Wprowadzenie do korzystania z programu Entity Framework za pomocą MVC][EFCodeFirstMVCTutorial]</span><span class="sxs-lookup"><span data-stu-id="0a352-310">[Getting Started with Entity Framework using MVC][EFCodeFirstMVCTutorial]</span></span>
* [<span data-ttu-id="0a352-311">Wprowadzenie do platformy ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="0a352-311">Intro to ASP.NET MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="0a352-312">Pierwszy ASP.NET interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="0a352-312">Your First ASP.NET Web API</span></span>](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api)
* [<span data-ttu-id="0a352-313">Debugowanie WAWS</span><span class="sxs-lookup"><span data-stu-id="0a352-313">Debugging WAWS</span></span>](web-sites-dotnet-troubleshoot-visual-studio.md)

<span data-ttu-id="0a352-314">W tym samouczku i przykładowa aplikacja została napisana przy [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [ @RickAndMSFT ](https://twitter.com/RickAndMSFT)) z pomocą Dykstra Tomasz i Dorrans Marcin (Twitter [ @blowdart ](https://twitter.com/blowdart)).</span><span class="sxs-lookup"><span data-stu-id="0a352-314">This tutorial and the sample application was written by [Rick Anderson](http://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](https://twitter.com/RickAndMSFT)) with assistance from Tom Dykstra and Barry Dorrans (Twitter [@blowdart](https://twitter.com/blowdart)).</span></span> 

<span data-ttu-id="0a352-315">Sprawdź Wystaw opinię, co Ci się podoba lub chcesz zobaczyć zwiększona, nie tylko o samouczka sam, ale także o produktach, które pokazuje go.</span><span class="sxs-lookup"><span data-stu-id="0a352-315">Please leave feedback on what you liked or what you would like to see improved, not only about the tutorial itself but also about the products that it demonstrates.</span></span> <span data-ttu-id="0a352-316">Twoja opinia pomoże nam priorytety ulepszenia.</span><span class="sxs-lookup"><span data-stu-id="0a352-316">Your feedback will help us prioritize improvements.</span></span> <span data-ttu-id="0a352-317">Dbamy szczególnie w ustaleniu odsetek istnieje więcej automatyzacji procesu, konfigurowanie i wdrażanie bazy danych członkostwa.</span><span class="sxs-lookup"><span data-stu-id="0a352-317">We are especially interested in finding out how much interest there is in more automation for the process of configuring and deploying the membership database.</span></span> 

## <a name="whats-changed"></a><span data-ttu-id="0a352-318">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="0a352-318">What's changed</span></span>
* <span data-ttu-id="0a352-319">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="0a352-319">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- bookmarks -->
[Add an OAuth Provider]: #addOauth
[Add Roles to the Membership Database]:#mbrDB
[Create a Data Deployment Script]:#ppd
[Update the Membership Database]:#ppd2
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

