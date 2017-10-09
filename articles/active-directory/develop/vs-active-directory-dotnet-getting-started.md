---
title: aaaGet Started with Azure AD w projektach Visual Studio MVC | Dokumentacja firmy Microsoft
description: "Sposób uruchamiania przy użyciu usługi Azure Active Directory w projektach MVC po połączeniu tooor Tworzenie usługi Azure AD przy użyciu programu Visual Studio tooget połączone usługi"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1c8b6a58-5144-4965-a905-625b9ee7b22b
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 807824dd6e4e57e443f8a7322cf2e5326384316d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-and-visual-studio-connected-services-mvc-projects"></a><span data-ttu-id="b238a-103">Wprowadzenie do korzystania z usługi Azure Active Directory i programu Visual Studio połączone usługi (projektów MVC)</span><span class="sxs-lookup"><span data-stu-id="b238a-103">Getting Started with Azure Active Directory and Visual Studio connected services (MVC Projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b238a-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="b238a-104">Getting Started</span></span>](vs-active-directory-dotnet-getting-started.md)
> * [<span data-ttu-id="b238a-105">Co się stało</span><span class="sxs-lookup"><span data-stu-id="b238a-105">What Happened</span></span>](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a><span data-ttu-id="b238a-106">Wymaganie uwierzytelniania tooaccess kontrolerów</span><span class="sxs-lookup"><span data-stu-id="b238a-106">Requiring authentication tooaccess controllers</span></span>
<span data-ttu-id="b238a-107">Wszystkie kontrolery w projekcie zostały adorned z hello **autoryzacji** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="b238a-107">All controllers in your project were adorned with hello **Authorize** attribute.</span></span> <span data-ttu-id="b238a-108">Ten atrybut wymaga hello toobe użytkownik uwierzytelniony przed uzyskaniem dostępu do tych kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="b238a-108">This attribute requires hello user toobe authenticated before accessing these controllers.</span></span> <span data-ttu-id="b238a-109">toobe kontrolera hello tooallow dostęp anonimowo, Usuń ten atrybut z hello kontrolera.</span><span class="sxs-lookup"><span data-stu-id="b238a-109">tooallow hello controller toobe accessed anonymously, remove this attribute from hello controller.</span></span> <span data-ttu-id="b238a-110">Uprawnienia hello tooset na bardziej szczegółowym poziomie, można zastosować hello atrybutu tooeach metodę, która wymaga autoryzacji zamiast stosować go toohello klasy kontrolera.</span><span class="sxs-lookup"><span data-stu-id="b238a-110">If you want tooset hello permissions at a more granular level, apply hello attribute tooeach method that requires authorization instead of applying it toohello controller class.</span></span>

## <a name="adding-signin--signout-controls"></a><span data-ttu-id="b238a-111">Dodawanie SignIn / SignOut kontrolki</span><span class="sxs-lookup"><span data-stu-id="b238a-111">Adding SignIn / SignOut Controls</span></span>
<span data-ttu-id="b238a-112">hello tooadd SignIn/SignOut kontrolki widoku tooyour, możesz użyć hello **_LoginPartial.cshtml** widoku częściowego tooadd hello funkcji tooone widoków.</span><span class="sxs-lookup"><span data-stu-id="b238a-112">tooadd hello SignIn/SignOut controls tooyour view, you can use hello **_LoginPartial.cshtml** partial view tooadd hello functionality tooone of your views.</span></span> <span data-ttu-id="b238a-113">Oto przykład hello funkcji toohello dodano standardu **_Layout.cshtml** widoku.</span><span class="sxs-lookup"><span data-stu-id="b238a-113">Here is an example of hello functionality added toohello standard **_Layout.cshtml** view.</span></span> <span data-ttu-id="b238a-114">(Uwaga hello ostatni element div hello zwinięte pasek nawigacyjny klasy):</span><span class="sxs-lookup"><span data-stu-id="b238a-114">(Note hello last element in hello div with class navbar-collapse):</span></span>

<pre>
    &lt;!DOCTYPE html&gt; 
     &lt;html&gt; 
     &lt;head&gt; 
         &lt;meta charset="utf-8" /&gt; 
        &lt;meta name="viewport" content="width=device-width, initial-scale=1.0"&gt; 
        &lt;title&gt;@ViewBag.Title - My ASP.NET Application&lt;/title&gt; 
        @Styles.Render("~/Content/css") 
        @Scripts.Render("~/bundles/modernizr") 
    &lt;/head&gt; 
    &lt;body&gt; 
        &lt;div class="navbar navbar-inverse navbar-fixed-top"&gt; 
            &lt;div class="container"&gt; 
                &lt;div class="navbar-header"&gt; 
                    &lt;button type="button" class="navbar-toggle" data-toggle="collapse" data-target=".navbar-collapse"&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                        &lt;span class="icon-bar"&gt;&lt;/span&gt; 
                    &lt;/button&gt; 
                    @Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" }) 
                &lt;/div&gt; 
                &lt;div class="navbar-collapse collapse"&gt; 
                    &lt;ul class="nav navbar-nav"&gt; 
                        &lt;li&gt;@Html.ActionLink("Home", "Index", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("About", "About", "Home")&lt;/li&gt; 
                        &lt;li&gt;@Html.ActionLink("Contact", "Contact", "Home")&lt;/li&gt; 
                    &lt;/ul&gt; 
                    <span style="background-color:yellow">@Html.Partial("_LoginPartial")</span> 
                &lt;/div&gt; 
            &lt;/div&gt; 
        &lt;/div&gt; 
        &lt;div class="container body-content"&gt; 
            @RenderBody() 
            &lt;hr /&gt; 
            &lt;footer&gt; 
                &lt;p&gt;&amp;copy; @DateTime.Now.Year - My ASP.NET Application&lt;/p&gt; 
            &lt;/footer&gt; 
        &lt;/div&gt; 
        @Scripts.Render("~/bundles/jquery") 
        @Scripts.Render("~/bundles/bootstrap") 
        @RenderSection("scripts", required: false) 
    &lt;/body&gt; 
    &lt;/html&gt;
</pre>

## <a name="next-steps"></a><span data-ttu-id="b238a-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b238a-115">Next steps</span></span>
- [<span data-ttu-id="b238a-116">Dowiedz się więcej o usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b238a-116">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/) 

