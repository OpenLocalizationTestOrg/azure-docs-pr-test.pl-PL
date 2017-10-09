---
title: "aaaProtect interfejsu API sieci Web wewnętrznej bazy danych z usługi Azure Active Directory i zarządzanie interfejsami API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooprotect interfejsu API sieci Web wewnętrznej bazy danych z usługi Azure Active Directory i zarządzanie interfejsami API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: f856ff03-64a1-4548-9ec4-c0ec4cc1600f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: f4b323034354aa09579c643bade47257fbf1e5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooprotect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="3eb9b-103">Jak tooprotect interfejsu API sieci Web wewnętrznej bazy danych z usługi Azure Active Directory i zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="3eb9b-103">How tooprotect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="3eb9b-104">Witaj, po wideo pokazuje, jak toobuild zaplecza interfejsu API sieci Web i chronić go z usługą Azure Active Directory i zarządzanie interfejsami API przy użyciu protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-104">hello following video shows how toobuild a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="3eb9b-105">Ten artykuł zawiera omówienie i dodatkowe informacje dotyczące hello kroki hello wideo.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-105">This article provides an overview and additional information for hello steps in hello video.</span></span> <span data-ttu-id="3eb9b-106">To 24 minutę wideo pokazuje, jak do:</span><span class="sxs-lookup"><span data-stu-id="3eb9b-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="3eb9b-107">Tworzenie zaplecza interfejsu API sieci Web i zabezpiecz ją przy użyciu usługi AAD — począwszy od 1:30</span><span class="sxs-lookup"><span data-stu-id="3eb9b-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="3eb9b-108">Importowanie hello API zarządzanie interfejsami API — począwszy od 7:10</span><span class="sxs-lookup"><span data-stu-id="3eb9b-108">Import hello API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="3eb9b-109">Skonfiguruj hello Developer portal toocall hello interfejsu API — począwszy od 9:09</span><span class="sxs-lookup"><span data-stu-id="3eb9b-109">Configure hello Developer portal toocall hello API - starting at 9:09</span></span>
* <span data-ttu-id="3eb9b-110">Konfigurowanie aplikacji komputerowych hello toocall interfejsu API — począwszy od 18:08</span><span class="sxs-lookup"><span data-stu-id="3eb9b-110">Configure a desktop application toocall hello API - starting at 18:08</span></span>
* <span data-ttu-id="3eb9b-111">Skonfiguruj toopre zasady sprawdzania poprawności tokenu JWT-autoryzować żądania — począwszy od 20:47</span><span class="sxs-lookup"><span data-stu-id="3eb9b-111">Configure a JWT validation policy toopre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="3eb9b-112">Utwórz katalog usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb9b-112">Create an Azure AD directory</span></span>
<span data-ttu-id="3eb9b-113">toosecure kopii interfejsu API sieci Web przy użyciu usługi Azure Active Directory, musisz najpierw mieć dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-113">toosecure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="3eb9b-114">W tym wideo dzierżawa o nazwie **APIMDemo** jest używany.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="3eb9b-115">toocreate dzierżawę usługi AAD logowania toohello [klasycznego portalu Azure](https://manage.windowsazure.com) i kliknij przycisk **nowy**->**usługi aplikacji**->**Active Katalog**->**katalogu**->**Utwórz niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-115">toocreate an AAD tenant, sign-in toohello [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Usługa Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="3eb9b-117">W tym przykładzie katalog o nazwie **APIMDemo** jest tworzony z domyślnej domeny o nazwie **DemoAPIM.onmicrosoft.com**. Ten katalog jest używany w całym hello wideo.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**. This directory is used throughout hello video.</span></span>

![Usługa Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="3eb9b-119">Tworzenie usługi interfejsu API sieci Web zabezpieczonych przez usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3eb9b-119">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="3eb9b-120">W tym kroku zaplecza interfejsu API sieci Web jest tworzony przy użyciu programu Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-120">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="3eb9b-121">W tym kroku hello wideo rozpoczyna się od 1:30.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-121">This step of hello video starts at 1:30.</span></span> <span data-ttu-id="3eb9b-122">toocreate projektu zaplecza interfejsu API sieci Web w programie Visual Studio kliknij **pliku**->**nowy**->**projektu**i wybierz polecenie **sieci Web ASP.NET Aplikacja** z hello **Web** listy szablonów.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-122">toocreate Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from hello **Web** templates list.</span></span> <span data-ttu-id="3eb9b-123">W tym wideo hello projektu o nazwie **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-123">In this video hello project is named **APIMAADDemo**.</span></span> <span data-ttu-id="3eb9b-124">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-124">Click **OK** toocreate hello project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="3eb9b-126">Kliknij przycisk **interfejsu API sieci Web** z hello **wybierz listę szablonów** toocreate projekt interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-126">Click **Web API** from hello **Select a template list** toocreate a Web API project.</span></span> <span data-ttu-id="3eb9b-127">Kliknij tooconfigure uwierzytelniania katalogu Azure **Zmień uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-127">tooconfigure Azure Directory Authentication click **Change Authentication**.</span></span>

![Nowy projekt][api-management-new-project]

<span data-ttu-id="3eb9b-129">Kliknij przycisk **konta organizacyjne**, a następnie określ hello **domeny** dzierżawy usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-129">Click **Organizational Accounts**, and specify hello **Domain** of your AAD tenant.</span></span> <span data-ttu-id="3eb9b-130">W tym hello przykład domena jest **DemoAPIM.onmicrosoft.com**. hello domeny katalogu można je uzyskać z hello **domen** katalogu.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-130">In this example hello domain is **DemoAPIM.onmicrosoft.com**. hello domain of your directory can be obtained from hello **Domains** tab of your directory.</span></span>

![Domeny][api-management-aad-domains]

<span data-ttu-id="3eb9b-132">Skonfiguruj ustawienia hello potrzebne w hello **Zmień uwierzytelnianie** okno dialogowe i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-132">Configure hello desired settings in hello **Change Authentication** dialog box and click **OK**.</span></span>

![Zmienianie uwierzytelniania][api-management-change-authentication]

<span data-ttu-id="3eb9b-134">Po kliknięciu **OK** programu Visual Studio będzie podejmować tooregister do aplikacji z katalogu usługi Azure AD i może być zostanie wyświetlony monit o toosign w przez program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-134">When you click **OK** Visual Studio will attempt tooregister your application with your Azure AD directory and you may be prompted toosign in by Visual Studio.</span></span> <span data-ttu-id="3eb9b-135">Zaloguj się przy użyciu konta administracyjnego dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-135">Sign in using an administrative account for your directory.</span></span>

![Zaloguj się tooVisual w Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="3eb9b-137">tooconfigure pole tego projektu jako hello wyboru interfejsu API sieci Web Azure **Host w chmurze hello** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-137">tooconfigure this project as an Azure Web API check hello box for **Host in hello cloud** and then click **OK**.</span></span>

![Nowy projekt][api-management-new-project-cloud]

<span data-ttu-id="3eb9b-139">Zostanie wyświetlony monit o toosign w tooAzure może być, a następnie można skonfigurować hello aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-139">You may be prompted toosign in tooAzure, and then you can configure hello Web App.</span></span>

![Konfigurowanie][api-management-configure-web-app]

<span data-ttu-id="3eb9b-141">W tym przykładzie nowy **planu usługi aplikacji** o nazwie **APIMAADDemo** jest określona.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-141">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="3eb9b-142">Kliknij przycisk **OK** tooconfigure hello aplikacji sieci Web i Utwórz projekt hello.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-142">Click **OK** tooconfigure hello Web App and create hello project.</span></span>

## <a name="add-hello-code-toohello-web-api-project"></a><span data-ttu-id="3eb9b-143">Dodaj projekt interfejsu API sieci Web toohello kodu hello</span><span class="sxs-lookup"><span data-stu-id="3eb9b-143">Add hello code toohello Web API project</span></span>
<span data-ttu-id="3eb9b-144">następnym krokiem Hello wideo hello dodaje hello kodu toohello interfejsu API sieci Web projektu.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-144">hello next step in hello video adds hello code toohello Web API project.</span></span> <span data-ttu-id="3eb9b-145">Ten krok zostanie uruchomiony na 4:35.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-145">This step starts at 4:35.</span></span>

<span data-ttu-id="3eb9b-146">Witaj interfejsu API sieci Web w tym przykładzie implementuje Kalkulator podstawowe usługi przy użyciu modelu i kontrolera.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-146">hello Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="3eb9b-147">Kliknij prawym przyciskiem myszy tooadd hello model dla usługi hello, **modele** w **Eksploratora rozwiązań** i wybierz polecenie **Dodaj**, **klasy**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-147">tooadd hello model for hello service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="3eb9b-148">Nazwa klasy hello `CalcInput` i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-148">Name hello class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="3eb9b-149">Dodaj następujące hello `using` instrukcji toohello początku hello `CalcInput.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-149">Add hello following `using` statement toohello top of hello `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="3eb9b-150">Zastąp hello wygenerowane klasy hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-150">Replace hello generated class with hello following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="3eb9b-151">Kliknij prawym przyciskiem myszy **kontrolerów** w **Eksploratora rozwiązań** i wybierz polecenie **Dodaj**->**kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-151">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="3eb9b-152">Wybierz **kontrolera 2 interfejsu API sieci Web — pusty** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-152">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="3eb9b-153">Typ **CalcController** dla hello kontrolera nazwę, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-153">Type **CalcController** for hello Controller name and click **Add**.</span></span>

![Dodawanie kontrolera][api-management-add-controller]

<span data-ttu-id="3eb9b-155">Dodaj następujące hello `using` instrukcji toohello początku hello `CalcController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-155">Add hello following `using` statement toohello top of hello `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="3eb9b-156">Zastąp hello wygenerowane klasy kontrolera hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-156">Replace hello generated controller class with hello following code.</span></span> <span data-ttu-id="3eb9b-157">Ten kod implementuje hello `Add`, `Subtract`, `Multiply`, i `Divide` operacji hello podstawowe Kalkulator interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-157">This code implements hello `Add`, `Subtract`, `Multiply`, and `Divide` operations of hello Basic Calculator API.</span></span>

```c#
[Authorize]
public class CalcController : ApiController
{
    [Route("api/add")]
    [HttpGet]
    public HttpResponseMessage GetSum([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a + b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/sub")]
    [HttpGet]
    public HttpResponseMessage GetDiff([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a - b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/mul")]
    [HttpGet]
    public HttpResponseMessage GetProduct([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a * b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }

    [Route("api/div")]
    [HttpGet]
    public HttpResponseMessage GetDiv([FromUri]int a, [FromUri]int b)
    {
        string xml = string.Format("<result><value>{0}</value><broughtToYouBy>Azure API Management - http://azure.microsoft.com/apim/ </broughtToYouBy></result>", a / b);
        HttpResponseMessage response = Request.CreateResponse();
        response.Content = new StringContent(xml, System.Text.Encoding.UTF8, "application/xml");
        return response;
    }
}
```

<span data-ttu-id="3eb9b-158">Naciśnij klawisz **F6** toobuild i sprawdź hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-158">Press **F6** toobuild and verify hello solution.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="3eb9b-159">Publikowanie hello tooAzure projektu</span><span class="sxs-lookup"><span data-stu-id="3eb9b-159">Publish hello project tooAzure</span></span>
<span data-ttu-id="3eb9b-160">W ten krok hello Visual Studio projektu jest tooAzure opublikowane.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-160">In this step hello Visual Studio project is published tooAzure.</span></span> <span data-ttu-id="3eb9b-161">W tym kroku hello wideo rozpoczyna się od 5:45.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-161">This step of hello video starts at 5:45.</span></span>

<span data-ttu-id="3eb9b-162">toopublish hello tooAzure projektu, kliknij prawym przyciskiem myszy hello **APIMAADDemo** projekt w programie Visual Studio i wybierz pozycję **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-162">toopublish hello project tooAzure, right-click hello **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="3eb9b-163">Zachowaj ustawienia domyślne hello w hello **publikowanie w sieci Web** okno dialogowe i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-163">Keep hello default settings in hello **Publish Web** dialog box and click **Publish**.</span></span>

![Publikowanie w sieci Web][api-management-web-publish]

## <a name="grant-permissions-toohello-azure-ad-backend-service-application"></a><span data-ttu-id="3eb9b-165">Przyznaj uprawnienia aplikacji usługi wewnętrznej bazy danych toohello usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3eb9b-165">Grant permissions toohello Azure AD backend service application</span></span>
<span data-ttu-id="3eb9b-166">Nowa aplikacja hello usługi wewnętrznej bazy danych jest tworzony w katalogu usługi Azure AD w ramach konfigurowania hello i proces publikowania projektu interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-166">A new application for hello backend service is created in your Azure AD directory as part of hello configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="3eb9b-167">W tym kroku hello wideo zaczynając od 6:13 uprawnienia są przyznawane toohello interfejsu API sieci Web zaplecza.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-167">In this step of hello video, starting at 6:13, permissions are granted toohello Web API backend.</span></span>

![Aplikacja][api-management-aad-backend-app]

<span data-ttu-id="3eb9b-169">Kliknij nazwę hello hello aplikacji tooconfigure hello wymagane uprawnienia.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-169">Click hello name of hello application tooconfigure hello required permissions.</span></span> <span data-ttu-id="3eb9b-170">Przejdź toohello **Konfiguruj** i przewiń w dół toohello **uprawnienia aplikacji tooother** sekcji.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-170">Navigate toohello **Configure** tab and scroll down toohello **permissions tooother applications** section.</span></span> <span data-ttu-id="3eb9b-171">Kliknij przycisk hello **uprawnienia aplikacji** listy rozwijanej obok **Windows** **usługi Azure Active Directory**, sprawdź pole hello **odczytuj dane katalogu**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-171">Click hello **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check hello box for **Read directory data**, and click **Save**.</span></span>

![Dodaj uprawnienia][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="3eb9b-173">Jeśli **Windows** **usługi Azure Active Directory** jest niewymienione w obszarze uprawnienia tooother aplikacji, kliknij przycisk **dodać aplikację** i dodaj go z listy hello.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-173">If **Windows** **Azure Active Directory** is not listed under permissions tooother applications, click **Add application** and add it from hello list.</span></span>
> 
> 

<span data-ttu-id="3eb9b-174">Zanotuj hello **identyfikator URI aplikacji** do użycia w kolejnym kroku po skonfigurowaniu aplikacji usługi Azure AD do portalu dla deweloperów usługi API Management hello.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-174">Make a note of hello **App Id URI** for use in a subsequent step when an Azure AD application is configured for hello API Management developer portal.</span></span>

![Identyfikator URI. Identyfikator aplikacji][api-management-aad-sso-uri]

## <a name="import-hello-web-api-into-api-management"></a><span data-ttu-id="3eb9b-176">Importowanie hello interfejsu API sieci Web do zarządzania interfejsem API</span><span class="sxs-lookup"><span data-stu-id="3eb9b-176">Import hello Web API into API Management</span></span>
<span data-ttu-id="3eb9b-177">Interfejsy API są skonfigurowane z hello interfejsu API wydawcy portalu, który jest dostępny za pośrednictwem hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-177">APIs are configured from hello API publisher portal, which is accessed through hello Azure Portal.</span></span> <span data-ttu-id="3eb9b-178">tooreach, kliknij przycisk **wydawcy portalu** z paska narzędzi hello usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-178">tooreach it, click **Publisher portal** from hello toolbar of your API Management service.</span></span> <span data-ttu-id="3eb9b-179">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [pierwszy interfejs API zarządzania] [ Manage your first API] samouczka.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-179">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Manage your first API][Manage your first API] tutorial.</span></span>

![Portal wydawcy][api-management-management-console]

<span data-ttu-id="3eb9b-181">Operacje mogą być [ręcznie dodawać tooAPIs](api-management-howto-add-operations.md), lub mogą być importowane.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-181">Operations can be [added tooAPIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="3eb9b-182">W tym wideo operacje są importowane w formacie struktury Swagger, zaczynając od 6:40.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-182">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="3eb9b-183">Utwórz plik o nazwie `calcapi.json` o następującej zawartości i zapisaniu tooyour komputera.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-183">Create a file named `calcapi.json` with following contents and save it tooyour computer.</span></span> <span data-ttu-id="3eb9b-184">Upewnij się, że hello `host` atrybut wskazuje tooyour interfejsu API sieci Web zaplecza.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-184">Ensure that hello `host` attribute points tooyour Web API backend.</span></span> <span data-ttu-id="3eb9b-185">W tym przykładzie `"host": "apimaaddemo.azurewebsites.net"` jest używany.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-185">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

```json
{
  "swagger": "2.0",
  "info": {
    "title": "Calculator",
    "description": "Arithmetics over HTTP!",
    "version": "1.0"
  },
  "host": "apimaaddemo.azurewebsites.net",
  "basePath": "/api",
  "schemes": [
    "http"
  ],
  "paths": {
    "/add?a={a}&b={b}": {
      "get": {
        "description": "Responds with a sum of two numbers.",
        "operationId": "Add two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>51</code>.",
            "required": true,
            "type": "string",
            "default": "51",
            "enum": [
              "51"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>49</code>.",
            "required": true,
            "type": "string",
            "default": "49",
            "enum": [
              "49"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/sub?a={a}&b={b}": {
      "get": {
        "description": "Responds with a difference between two numbers.",
        "operationId": "Subtract two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>50</code>.",
            "required": true,
            "type": "string",
            "default": "50",
            "enum": [
              "50"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/div?a={a}&b={b}": {
      "get": {
        "description": "Responds with a quotient of two numbers.",
        "operationId": "Divide two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>100</code>.",
            "required": true,
            "type": "string",
            "default": "100",
            "enum": [
              "100"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          }
        ],
        "responses": { }
      }
    },
    "/mul?a={a}&b={b}": {
      "get": {
        "description": "Responds with a product of two numbers.",
        "operationId": "Multiply two integers",
        "parameters": [
          {
            "name": "a",
            "in": "query",
            "description": "First operand. Default value is <code>20</code>.",
            "required": true,
            "type": "string",
            "default": "20",
            "enum": [
              "20"
            ]
          },
          {
            "name": "b",
            "in": "query",
            "description": "Second operand. Default value is <code>5</code>.",
            "required": true,
            "type": "string",
            "default": "5",
            "enum": [
              "5"
            ]
          }
        ],
        "responses": { }
      }
    }
  }
}
```

<span data-ttu-id="3eb9b-186">Kalkulator hello tooimport interfejsu API, kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **Import API**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-186">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Przycisk do importowania interfejsu API][api-management-import-api]

<span data-ttu-id="3eb9b-188">Wykonaj następujące kroki tooconfigure hello Kalkulator API hello.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-188">Perform hello following steps tooconfigure hello calculator API.</span></span>

1. <span data-ttu-id="3eb9b-189">Kliknij przycisk **z pliku**, Przeglądaj toohello `calculator.json` można zapisać pliku, a następnie kliknij przycisk hello **Swagger** przycisk radiowy.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-189">Click **From file**, browse toohello `calculator.json` file you saved, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="3eb9b-190">Typ **obliczenia** do hello **sufiks adresu URL interfejsu API sieci Web** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-190">Type **calc** into hello **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="3eb9b-191">Kliknij hello **produktów (opcjonalnie)** polu i wybierz polecenie **Starter**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-191">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="3eb9b-192">Kliknij przycisk **zapisać** hello tooimport interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-192">Click **Save** tooimport hello API.</span></span>

![Dodawanie nowego interfejsu API][api-management-import-new-api]

<span data-ttu-id="3eb9b-194">Po zaimportowaniu hello API hello strony podsumowania dla interfejsu API hello jest wyświetlana w hello wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-194">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

## <a name="call-hello-api-unsuccessfully-from-hello-developer-portal"></a><span data-ttu-id="3eb9b-195">Wywołanie interfejsu API hello niepomyślnie z portalu dla deweloperów hello</span><span class="sxs-lookup"><span data-stu-id="3eb9b-195">Call hello API unsuccessfully from hello developer portal</span></span>
<span data-ttu-id="3eb9b-196">W tym momencie hello interfejsu API został zaimportowany do interfejsu API zarządzania, ale nie można jeszcze można wywołać pomyślnie z portalu dla deweloperów hello ponieważ hello usługi wewnętrznej bazy danych jest chroniony za pomocą uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-196">At this point, hello API has been imported into API Management, but cannot yet be called successfully from hello developer portal because hello backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="3eb9b-197">To jest przedstawiona w hello wideo, zaczynając od 7:40 przy użyciu hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-197">This is demonstrated in hello video starting at 7:40 using hello following steps.</span></span>

<span data-ttu-id="3eb9b-198">Kliknij przycisk **portalu dla deweloperów** z hello prawym górnym rogu strony hello wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-198">Click **Developer portal** from hello top-right side of hello publisher portal.</span></span>

![Portal dla deweloperów][api-management-developer-portal-menu]

<span data-ttu-id="3eb9b-200">Kliknij przycisk **interfejsów API** i kliknij przycisk hello **Kalkulator** interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-200">Click **APIs** and click hello **Calculator** API.</span></span>

![Portal dla deweloperów][api-management-dev-portal-apis]

<span data-ttu-id="3eb9b-202">Kliknij przycisk **wypróbuj**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-202">Click **Try it**.</span></span>

![Wypróbuj][api-management-dev-portal-try-it]

<span data-ttu-id="3eb9b-204">Kliknij przycisk **wysyłania** i zwróć uwagę na stan odpowiedzi hello **401 nieautoryzowane**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-204">Click **Send** and note hello response status of **401 Unauthorized**.</span></span>

![Send][api-management-dev-portal-send-401]

<span data-ttu-id="3eb9b-206">Hello żądania nie ma autoryzacji, ponieważ interfejs API zaplecza hello jest chroniony przez usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-206">hello request is unauthorized because hello backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="3eb9b-207">Przed wywołaniem metody interfejsu API hello pomyślnie portalu dla deweloperów hello musi być deweloperzy tooauthorize skonfigurowany przy użyciu protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-207">Before successfully calling hello API hello developer portal must be configured tooauthorize developers using OAuth 2.0.</span></span> <span data-ttu-id="3eb9b-208">Ten proces jest opisany w hello następujące sekcje.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-208">This process is described in hello following sections.</span></span>

## <a name="register-hello-developer-portal-as-an-aad-application"></a><span data-ttu-id="3eb9b-209">Zarejestruj portalu dla deweloperów hello jako aplikację AAD</span><span class="sxs-lookup"><span data-stu-id="3eb9b-209">Register hello developer portal as an AAD application</span></span>
<span data-ttu-id="3eb9b-210">Witaj pierwszym etapem konfigurowania deweloperzy tooauthorize portalu deweloperów hello przy użyciu protokołu OAuth 2.0 jest portalu dla deweloperów hello tooregister jako aplikację AAD.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-210">hello first step in configuring hello developer portal tooauthorize developers using OAuth 2.0 is tooregister hello developer portal as an AAD application.</span></span> <span data-ttu-id="3eb9b-211">Jest to wykazać, zaczynając od 8:27 hello wideo.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-211">This is demonstrated starting at 8:27 in hello video.</span></span>

<span data-ttu-id="3eb9b-212">Przejdź dzierżawy toohello usługi Azure AD z pierwszym krokiem hello ten film, w tym przykładzie **APIMDemo** i przejdź toohello **aplikacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-212">Navigate toohello Azure AD tenant from hello first step of this video, in this example **APIMDemo** and navigate toohello **Applications** tab.</span></span>

![Nowa aplikacja][api-management-aad-new-application-devportal]

<span data-ttu-id="3eb9b-214">Kliknij przycisk hello **Dodaj** przycisk toocreate nową aplikację usługi Azure Active Directory, a następnie wybierz pozycję **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-214">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Nowa aplikacja][api-management-new-aad-application-menu]

<span data-ttu-id="3eb9b-216">Wybierz **sieci Web, aplikacji i/lub interfejs API sieci Web**, wprowadź nazwę i kliknij strzałkę dalej hello.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-216">Choose **Web application and/or Web API**, enter a name, and click hello next arrow.</span></span> <span data-ttu-id="3eb9b-217">W tym przykładzie **APIMDeveloperPortal** jest używany.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-217">In this example **APIMDeveloperPortal** is used.</span></span>

![Nowa aplikacja][api-management-aad-new-application-devportal-1]

<span data-ttu-id="3eb9b-219">Aby uzyskać **adres URL logowania** wprowadź adres URL hello usługi API Management i Dołącz `/signin`.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-219">For **Sign-on URL** enter hello URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="3eb9b-220">W tym przykładzie `https://contoso5.portal.azure-api.net/signin` jest używany.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-220">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="3eb9b-221">Aby uzyskać **adres URL identyfikatora aplikacji** wprowadź adres URL hello usługi API Management i Dołącz niektóre unikatowe znaki.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-221">For **App Id URL** enter hello URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="3eb9b-222">Mogą to być wszystkie odpowiednie znaki w tym przykładzie `https://contoso5.portal.azure-api.net/dp` jest używany.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-222">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="3eb9b-223">Gdy potrzebne hello **właściwości aplikacji** są skonfigurowane, kliknij przycisk hello znacznik wyboru toocreate hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-223">When hello  desired **App properties** are configured, click hello check mark toocreate hello application.</span></span>

![Nowa aplikacja][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="3eb9b-225">Konfigurowanie serwera autoryzacji usługi API Management OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="3eb9b-225">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="3eb9b-226">Witaj następnym krokiem jest tooconfigure serwera autoryzacji OAuth 2.0 w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-226">hello next step is tooconfigure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="3eb9b-227">Ten krok jest przedstawiona w hello wideo, zaczynając od 9:43.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-227">This step is demonstrated in hello video starting at 9:43.</span></span>

<span data-ttu-id="3eb9b-228">Kliknij przycisk **zabezpieczeń** hello zarządzanie interfejsami API menu po lewej stronie powitania kliknij **OAuth 2.0**, a następnie kliknij przycisk **dodać autoryzacji** serwera.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-228">Click **Security** from hello API Management menu on hello left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server]

<span data-ttu-id="3eb9b-230">Wprowadź nazwę i opcjonalny opis w hello **nazwa** i **opis** pola.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-230">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> <span data-ttu-id="3eb9b-231">Te pola są używane tooidentify serwera autoryzacji hello OAuth 2.0 w wystąpieniu usługi Zarządzanie interfejsami API hello.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-231">These fields are used tooidentify hello OAuth 2.0 authorization server within hello API Management service instance.</span></span> <span data-ttu-id="3eb9b-232">W tym przykładzie **pokaz serwera autoryzacji** jest używany.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-232">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="3eb9b-233">Później podczas określania toobe serwera OAuth 2.0, używany do uwierzytelniania dla interfejsu API, możesz wybrać tej nazwy.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-233">Later when you specify an OAuth 2.0 server toobe used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="3eb9b-234">Dla hello **adres URL strony rejestracji klienta** wprowadź wartość symbolu zastępczego, takich jak `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-234">For hello **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="3eb9b-235">Witaj **adres URL strony rejestracji klienta** punktów toohello strony przez użytkowników, można użyć toocreate i skonfiguruj swoje własne konta dla dostawcy OAuth 2.0, które obsługują zarządzanie kontami użytkowników.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-235">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="3eb9b-236">W tym przykładzie użytkowników nie tworzyć i konfigurować własne konta, więc symbol zastępczy jest używany.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-236">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-1]

<span data-ttu-id="3eb9b-238">Następnie określ **adres URL punktu końcowego autoryzacji** i **adres URL punktu końcowego tokenu**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-238">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Serwer autoryzacji][api-management-add-authorization-server-1a]

<span data-ttu-id="3eb9b-240">Te wartości można pobrać z hello **punkty końcowe aplikacji** strony hello utworzona dla portalu dla deweloperów hello aplikacji usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-240">These values can be retrieved from hello **App Endpoints** page of hello AAD application you created for hello developer portal.</span></span> <span data-ttu-id="3eb9b-241">punkty końcowe hello tooaccess Przejdź toohello **Konfiguruj** hello usługi AAD aplikacji i kliknij polecenie **wyświetlić punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-241">tooaccess hello endpoints navigate toohello **Configure** tab for hello AAD application and click **View endpoints**.</span></span>

![Aplikacja][api-management-aad-devportal-application]

![Wyświetl punkty końcowe][api-management-aad-view-endpoints]

<span data-ttu-id="3eb9b-244">Kopiuj hello **punktu końcowego autoryzacji OAuth 2.0** i wklej go do hello **adres URL punktu końcowego autoryzacji** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-244">Copy hello **OAuth 2.0 authorization endpoint** and paste it into hello **Authorization endpoint URL** textbox.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-2]

<span data-ttu-id="3eb9b-246">Kopiuj hello **punkt końcowy tokenu OAuth 2.0** i wklej go do hello **tokenu końcowego adresu URL** pole tekstowe.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-246">Copy hello **OAuth 2.0 token endpoint** and paste it into hello **Token endpoint URL** textbox.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-2a]

<span data-ttu-id="3eb9b-248">Ponadto toopasting w punktu końcowego tokena hello, Dodaj parametr treści dodatkowe o nazwie **zasobów** i wartości hello Użyj hello **identyfikator URI aplikacji** z hello usługi AAD aplikacji hello usługi wewnętrznej bazy danych, który został utworzenia projektu Visual Studio hello został opublikowany.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-248">In addition toopasting in hello token endpoint, add an additional body parameter named **resource** and for hello value use hello **App Id URI** from hello AAD application for hello backend service that was created when hello Visual Studio project was published.</span></span>

![Identyfikator URI. Identyfikator aplikacji][api-management-aad-sso-uri]

<span data-ttu-id="3eb9b-250">Następnie określ hello poświadczeń klienta.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-250">Next, specify hello client credentials.</span></span> <span data-ttu-id="3eb9b-251">Są to poświadczenia hello zasobu hello tooaccess, w tym przypadku hello portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-251">These are hello credentials for hello resource you want tooaccess, in this case hello developer portal.</span></span>

![Poświadczenia klienta][api-management-client-credentials]

<span data-ttu-id="3eb9b-253">Witaj tooget **identyfikator klienta**, przejdź toohello **Konfiguruj** kartę hello aplikację AAD dla deweloperów hello hello portalu i skopiuj **identyfikator klienta**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-253">tooget hello **Client Id**, navigate toohello **Configure** tab of hello AAD application for hello developer portal and copy hello **Client Id**.</span></span>

<span data-ttu-id="3eb9b-254">Witaj tooget **klucz tajny klienta** kliknij hello **wybierz czas trwania** listy rozwijanej w hello **klucze** sekcji i określ interwał.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-254">tooget hello **Client Secret** click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="3eb9b-255">W tym przykładzie używany jest 1 rok.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-255">In this example 1 year is used.</span></span>

![Identyfikator klienta][api-management-aad-client-id]

<span data-ttu-id="3eb9b-257">Kliknij przycisk **zapisać** toosave hello konfiguracji oraz wyświetlania hello klucza.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-257">Click **Save** toosave hello configuration and display hello key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3eb9b-258">Zanotuj tego klucza.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-258">Make a note of this key.</span></span> <span data-ttu-id="3eb9b-259">Po zamknięciu okna konfiguracji usługi Azure Active Directory hello hello klucza nie może ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-259">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="3eb9b-260">Kopiuj hello klucza toohello Schowka, portal wydawcy wstecz toohello przełącznika, Wklej klucz hello do hello **klucz tajny klienta** polem tekstowym i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-260">Copy hello key toohello clipboard, switch back toohello publisher portal, paste hello key into hello **Client Secret** textbox, and click **Save**.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-3]

<span data-ttu-id="3eb9b-262">Bezpośrednio po poświadczeń klienta hello jest udzielania kodu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-262">Immediately following hello client credentials is an authorization code grant.</span></span> <span data-ttu-id="3eb9b-263">Skopiuj ten kod autoryzacji i tooyour tyłu przełącznika aplikacji portalu dewelopera usługi Azure AD skonfigurować stronę i wkleić udzielania autoryzacji hello hello **adres URL odpowiedzi** , a następnie kliknij przycisk **zapisać** ponownie.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-263">Copy this authorization code and switch back tooyour Azure AD developer portal application configure page, and paste hello authorization grant into hello **Reply URL** field, and click **Save** again.</span></span>

![Adres URL odpowiedzi][api-management-aad-reply-url]

<span data-ttu-id="3eb9b-265">Witaj następnym krokiem jest tooconfigure hello uprawnienia do portalu dla deweloperów hello usługi AAD aplikacji.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-265">hello next step is tooconfigure hello permissions for hello developer portal AAD application.</span></span> <span data-ttu-id="3eb9b-266">Kliknij przycisk **uprawnienia aplikacji** i zaznacz pole hello **odczytuj dane katalogu**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-266">Click **Application Permissions** and check hello box for **Read directory data**.</span></span> <span data-ttu-id="3eb9b-267">Kliknij przycisk **zapisać** toosave to zmienić, a następnie kliknij przycisk **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-267">Click **Save** toosave this change, and then click **Add application**.</span></span>

![Dodaj uprawnienia][api-management-add-devportal-permissions]

<span data-ttu-id="3eb9b-269">Kliknij ikonę wyszukiwania hello, typ **APIM** do hello począwszy od, wybierz **APIMAADDemo**i kliknij przycisk hello toosave znacznik wyboru.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-269">Click hello search icon, type **APIM** into hello Starting with box, select **APIMAADDemo**, and click hello check mark toosave.</span></span>

![Dodaj uprawnienia][api-management-aad-add-app-permissions]

<span data-ttu-id="3eb9b-271">Kliknij przycisk **delegowane uprawnienia** dla **APIMAADDemo** i zaznacz pole hello **APIMAADDemo dostępu**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-271">Click **Delegated Permissions** for **APIMAADDemo** and check hello box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="3eb9b-272">Dzięki temu deweloper hello usługi zaplecza hello tooaccess aplikacji portalu.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-272">This allows hello developer portal application tooaccess hello backend service.</span></span>

![Dodaj uprawnienia][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-hello-calculator-api"></a><span data-ttu-id="3eb9b-274">Włącz autoryzację użytkownika OAuth 2.0 na powitania Kalkulator interfejsu API</span><span class="sxs-lookup"><span data-stu-id="3eb9b-274">Enable OAuth 2.0 user authorization for hello Calculator API</span></span>
<span data-ttu-id="3eb9b-275">Teraz, gdy hello OAuth 2.0 serwer jest skonfigurowany, możesz je określić w hello ustawienia zabezpieczeń dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-275">Now that hello OAuth 2.0 server is configured, you can specify it in hello security settings for your API.</span></span> <span data-ttu-id="3eb9b-276">Ten krok jest przedstawiona w hello wideo, zaczynając od 14:30.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-276">This step is demonstrated in hello video starting at 14:30.</span></span>

<span data-ttu-id="3eb9b-277">Kliknij przycisk **interfejsów API** w hello menu po lewej stronie i kliknij przycisk **Kalkulator** tooview i jego ustawień.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-277">Click **APIs** in hello left menu, and click  **Calculator** tooview and configure its settings.</span></span>

![Kalkulator interfejsu API][api-management-calc-api]

<span data-ttu-id="3eb9b-279">Przejdź toohello **zabezpieczeń** pozycję Sprawdź hello **OAuth 2.0** pole wyboru, wybierz powitania serwera autoryzacji żądany z hello **serwera autoryzacji** listy rozwijanej i kliknij przycisk **Zapisać**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-279">Navigate toohello **Security** tab, check hello **OAuth 2.0** checkbox, select hello desired authorization server from hello **Authorization server** drop-down, and click **Save**.</span></span>

![Kalkulator interfejsu API][api-management-enable-aad-calculator]

## <a name="successfully-call-hello-calculator-api-from-hello-developer-portal"></a><span data-ttu-id="3eb9b-281">Pomyślne wywołanie hello Kalkulator interfejsu API z portalu dla deweloperów hello</span><span class="sxs-lookup"><span data-stu-id="3eb9b-281">Successfully call hello Calculator API from hello developer portal</span></span>
<span data-ttu-id="3eb9b-282">Teraz, gdy autoryzacji OAuth 2.0 hello jest skonfigurowany na powitania interfejsu API, jego operacji może pomyślnie wywołana z Centrum deweloperów hello.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-282">Now that hello OAuth 2.0 authorization is configured on hello API, its operations can be successfully called from hello developer center.</span></span> <span data-ttu-id="3eb9b-283">Ten krok jest przedstawiona w hello wideo, zaczynając od 15:00.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-283">THis step is demonstrated in hello video starting at 15:00.</span></span>

<span data-ttu-id="3eb9b-284">Przejdź wstecz toohello **Dodaj dwie liczb całkowitych** operacji usługi Kalkulator hello w portalu dla deweloperów hello i kliknij **wypróbuj**.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-284">Navigate back toohello **Add two integers** operation of hello calculator service in hello developer portal and click **Try it**.</span></span> <span data-ttu-id="3eb9b-285">Uwaga hello nowy element hello **autoryzacji** sekcji odpowiedniego serwera autoryzacji toohello właśnie został dodany.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-285">Note hello new item in hello **Authorization** section corresponding toohello authorization server you just added.</span></span>

![Kalkulator interfejsu API][api-management-calc-authorization-server]

<span data-ttu-id="3eb9b-287">Wybierz **kod autoryzacji** z autoryzacji hello listy rozwijanej liście, a następnie wprowadź poświadczenia hello hello toouse konta.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-287">Select **Authorization code** from hello authorization drop-down list and enter hello credentials of hello account toouse.</span></span> <span data-ttu-id="3eb9b-288">Jeśli nastąpiło już zalogowanie się przy użyciu konta hello może nie być wyświetlony monit.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-288">If you are already signed in with hello account you may not be prompted.</span></span>

![Kalkulator interfejsu API][api-management-devportal-authorization-code]

<span data-ttu-id="3eb9b-290">Kliknij przycisk **wysyłania** i hello Uwaga **stanu odpowiedzi** z **200 OK** i hello wyniki operacji hello hello zawartości odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-290">Click **Send** and note hello **Response status** of **200 OK** and hello results of hello operation in hello response content.</span></span>

![Kalkulator interfejsu API][api-management-devportal-response]

## <a name="configure-a-desktop-application-toocall-hello-api"></a><span data-ttu-id="3eb9b-292">Konfigurowanie aplikacji komputerowych hello toocall interfejsu API</span><span class="sxs-lookup"><span data-stu-id="3eb9b-292">Configure a desktop application toocall hello API</span></span>
<span data-ttu-id="3eb9b-293">Witaj następnej procedury w hello wideo rozpoczyna się od 16:30 i konfiguruje prostą aplikację pulpitu hello toocall interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-293">hello next procedure in hello video starts at 16:30 and configures a simple desktop application toocall hello API.</span></span> <span data-ttu-id="3eb9b-294">pierwszym krokiem Hello jest tooregister hello aplikację w usłudze Azure AD i nadaj mu dostępu toohello katalogu i toohello usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-294">hello first step is tooregister hello desktop application in Azure AD and give it access toohello directory and toohello backend service.</span></span> <span data-ttu-id="3eb9b-295">Na 18:25 istnieje Przykładowa aplikacja hello podczas wywoływania operacji na powitania Kalkulator interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-295">At 18:25 there is a demonstration of hello desktop application calling an operation on hello calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-toopre-authorize-requests"></a><span data-ttu-id="3eb9b-296">Skonfiguruj toopre zasady sprawdzania poprawności tokenu JWT-autoryzować żądania</span><span class="sxs-lookup"><span data-stu-id="3eb9b-296">Configure a JWT validation policy toopre-authorize requests</span></span>
<span data-ttu-id="3eb9b-297">Witaj ostatnia procedura hello wideo rozpoczyna się od 20:48 i pokazano, jak toouse hello [JWT do zweryfikowania](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) toopre zasad-autoryzować żądania weryfikując hello tokenów dostępu dla każdego żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-297">hello final procedure in hello video starts at 20:48 and shows you how toouse hello [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy toopre-authorize requests by validating hello access tokens of each incoming request.</span></span> <span data-ttu-id="3eb9b-298">Jeśli Żądanie hello nie jest weryfikowany przez hello zasady sprawdzania poprawności tokenów JWT, Żądanie hello jest blokowany przez interfejs API zarządzania i nie są przekazywane toohello wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-298">If hello request is not validated by hello Validate JWT policy, hello request is blocked by API Management and is not passed along toohello backend.</span></span>

```xml
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">
    <openid-config url="https://login.microsoftonline.com/DemoAPIM.onmicrosoft.com/.well-known/openid-configuration" />
    <required-claims>
        <claim name="aud">
            <value>https://DemoAPIM.NOTonmicrosoft.com/APIMAADDemo</value>
        </claim>
    </required-claims>
</validate-jwt>
```

<span data-ttu-id="3eb9b-299">Aby innego demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji interfejsu API zarządzania](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybko przewinąć do przodu too13:50.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-299">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="3eb9b-300">Szybkie przewijanie do przodu too15:00 zasady hello toosee skonfigurowane w edytorze zasad hello, a następnie too18:50 dla pokaz wywołanie operacji z portalu dla deweloperów hello zarówno z i bez hello wymagany token autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-300">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3eb9b-301">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3eb9b-301">Next steps</span></span>
* <span data-ttu-id="3eb9b-302">Zapoznaj się z kilku [wideo](https://azure.microsoft.com/documentation/videos/index/?services=api-management) o zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="3eb9b-302">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="3eb9b-303">Dla innych sposobów toosecure usługi wewnętrznej bazy danych, zobacz [uwierzytelnianie wzajemne certyfikatu](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="3eb9b-303">For other ways toosecure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-protect-backend-with-aad/api-management-management-console.png

[api-management-import-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-import-new-api.png
[api-management-create-aad-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad-menu.png
[api-management-create-aad]: ./media/api-management-howto-protect-backend-with-aad/api-management-create-aad.png
[api-management-new-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-web-app.png
[api-management-new-project]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project.png
[api-management-new-project-cloud]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-project-cloud.png
[api-management-change-authentication]: ./media/api-management-howto-protect-backend-with-aad/api-management-change-authentication.png
[api-management-sign-in-vidual-studio]: ./media/api-management-howto-protect-backend-with-aad/api-management-sign-in-vidual-studio.png
[api-management-configure-web-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-configure-web-app.png
[api-management-aad-domains]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-domains.png
[api-management-add-controller]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-controller.png
[api-management-web-publish]: ./media/api-management-howto-protect-backend-with-aad/api-management-web-publish.png
[api-management-aad-backend-app]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-backend-app.png
[api-management-aad-add-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-permissions.png
[api-management-developer-portal-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-developer-portal-menu.png
[api-management-dev-portal-apis]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-apis.png
[api-management-dev-portal-try-it]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-try-it.png
[api-management-dev-portal-send-401]: ./media/api-management-howto-protect-backend-with-aad/api-management-dev-portal-send-401.png
[api-management-aad-new-application-devportal]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal.png
[api-management-aad-new-application-devportal-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-1.png
[api-management-aad-new-application-devportal-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-new-application-devportal-2.png
[api-management-aad-devportal-application]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-devportal-application.png
[api-management-add-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server.png
[api-management-aad-sso-uri]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-sso-uri.png
[api-management-aad-view-endpoints]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-view-endpoints.png
[api-management-aad-client-id]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-client-id.png
[api-management-add-authorization-server-1]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1.png
[api-management-add-authorization-server-2]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2.png
[api-management-add-authorization-server-2a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-2a.png
[api-management-add-authorization-server-3]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-3.png
[api-management-aad-reply-url]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-reply-url.png
[api-management-add-devportal-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-devportal-permissions.png
[api-management-aad-add-app-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-app-permissions.png
[api-management-aad-add-delegated-permissions]: ./media/api-management-howto-protect-backend-with-aad/api-management-aad-add-delegated-permissions.png
[api-management-calc-api]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-api.png
[api-management-enable-aad-calculator]: ./media/api-management-howto-protect-backend-with-aad/api-management-enable-aad-calculator.png
[api-management-devportal-authorization-code]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-authorization-code.png
[api-management-devportal-response]: ./media/api-management-howto-protect-backend-with-aad/api-management-devportal-response.png
[api-management-calc-authorization-server]: ./media/api-management-howto-protect-backend-with-aad/api-management-calc-authorization-server.png
[api-management-add-authorization-server-1a]: ./media/api-management-howto-protect-backend-with-aad/api-management-add-authorization-server-1a.png
[api-management-client-credentials]: ./media/api-management-howto-protect-backend-with-aad/api-management-client-credentials.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-protect-backend-with-aad/api-management-new-aad-application-menu.png

[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Manage your first API]: api-management-get-started.md
