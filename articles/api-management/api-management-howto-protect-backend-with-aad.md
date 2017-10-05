---
title: "Ochrona interfejsu API sieci Web wewnętrznej bazy danych z usługi Azure Active Directory i zarządzanie interfejsami API | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zabezpieczyć interfejs API sieci Web wewnętrznej bazy danych z usługi Azure Active Directory i zarządzanie interfejsami API."
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
ms.openlocfilehash: 0dfb4102904c2e972e6617fd3851fb1c50147357
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-protect-a-web-api-backend-with-azure-active-directory-and-api-management"></a><span data-ttu-id="5088e-103">Jak zabezpieczyć interfejs API sieci Web wewnętrznej bazy danych z usługi Azure Active Directory i zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="5088e-103">How to protect a Web API backend with Azure Active Directory and API Management</span></span>
<span data-ttu-id="5088e-104">Poniższe wideo przedstawia sposób tworzenia zaplecza interfejsu API sieci Web i chronić go przy użyciu protokołu OAuth 2.0 z usługą Azure Active Directory i zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="5088e-104">The following video shows how to build a Web API backend and protect it using OAuth 2.0 protocol with Azure Active Directory and API Management.</span></span>  <span data-ttu-id="5088e-105">Ten artykuł zawiera omówienie i dodatkowe informacje dotyczące czynności w wideo.</span><span class="sxs-lookup"><span data-stu-id="5088e-105">This article provides an overview and additional information for the steps in the video.</span></span> <span data-ttu-id="5088e-106">To 24 minutę wideo pokazuje, jak do:</span><span class="sxs-lookup"><span data-stu-id="5088e-106">This 24 minute video shows you how to:</span></span>

* <span data-ttu-id="5088e-107">Tworzenie zaplecza interfejsu API sieci Web i zabezpiecz ją przy użyciu usługi AAD — począwszy od 1:30</span><span class="sxs-lookup"><span data-stu-id="5088e-107">Build a Web API backend and secure it with AAD - starting at 1:30</span></span>
* <span data-ttu-id="5088e-108">Importowanie interfejsu API zarządzanie interfejsami API — począwszy od 7:10</span><span class="sxs-lookup"><span data-stu-id="5088e-108">Import the API into API Management - starting at 7:10</span></span>
* <span data-ttu-id="5088e-109">Konfigurowanie portalu dla deweloperów do wywołania interfejsu API — począwszy od 9:09</span><span class="sxs-lookup"><span data-stu-id="5088e-109">Configure the Developer portal to call the API - starting at 9:09</span></span>
* <span data-ttu-id="5088e-110">Konfigurowanie aplikacji pulpitu do wywołania interfejsu API — począwszy od 18:08</span><span class="sxs-lookup"><span data-stu-id="5088e-110">Configure a desktop application to call the API - starting at 18:08</span></span>
* <span data-ttu-id="5088e-111">Skonfiguruj zasady sprawdzania poprawności tokenu JWT wstępnie autoryzować żądania — począwszy od 20:47</span><span class="sxs-lookup"><span data-stu-id="5088e-111">Configure a JWT validation policy to pre-authorize requests - starting at 20:47</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

## <a name="create-an-azure-ad-directory"></a><span data-ttu-id="5088e-112">Utwórz katalog usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5088e-112">Create an Azure AD directory</span></span>
<span data-ttu-id="5088e-113">Aby zabezpieczyć interfejs API sieci Web kopii przy użyciu usługi Azure Active Directory, musisz najpierw mieć dzierżawę usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="5088e-113">To secure your Web API backed using Azure Active Directory you must first have a an AAD tenant.</span></span> <span data-ttu-id="5088e-114">W tym wideo dzierżawa o nazwie **APIMDemo** jest używany.</span><span class="sxs-lookup"><span data-stu-id="5088e-114">In this video a tenant named **APIMDemo** is used.</span></span> <span data-ttu-id="5088e-115">Aby utworzyć dzierżawę usługi AAD, zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com) i kliknij przycisk **nowy**->**usługi aplikacji**->**usługi Active Directory**->**katalogu**->**Utwórz niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="5088e-115">To create an AAD tenant, sign-in to the [Azure Classic Portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Active Directory**->**Directory**->**Custom Create**.</span></span> 

![Usługa Azure Active Directory][api-management-create-aad-menu]

<span data-ttu-id="5088e-117">W tym przykładzie katalog o nazwie **APIMDemo** jest tworzony z domyślnej domeny o nazwie **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="5088e-117">In this example a directory named **APIMDemo** is created with a default domain named **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="5088e-118">Ten katalog jest używany w całym wideo.</span><span class="sxs-lookup"><span data-stu-id="5088e-118">This directory is used throughout the video.</span></span>

![Usługa Azure Active Directory][api-management-create-aad]

## <a name="create-a-web-api-service-secured-by-azure-active-directory"></a><span data-ttu-id="5088e-120">Tworzenie usługi interfejsu API sieci Web zabezpieczonych przez usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5088e-120">Create a Web API service secured by Azure Active Directory</span></span>
<span data-ttu-id="5088e-121">W tym kroku zaplecza interfejsu API sieci Web jest tworzony przy użyciu programu Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="5088e-121">In this step, a Web API backend is created using Visual Studio 2013.</span></span> <span data-ttu-id="5088e-122">W tym kroku wideo rozpoczyna się od 1:30.</span><span class="sxs-lookup"><span data-stu-id="5088e-122">This step of the video starts at 1:30.</span></span> <span data-ttu-id="5088e-123">Do tworzenia projektu zaplecza interfejsu API sieci Web w programie Visual Studio, kliknij **pliku**->**nowy**->**projektu**i wybierz polecenie **aplikacji sieci Web ASP.NET** z **Web** listy szablonów.</span><span class="sxs-lookup"><span data-stu-id="5088e-123">To create Web API backend project in Visual Studio click **File**->**New**->**Project**, and choose **ASP.NET Web Application** from the **Web** templates list.</span></span> <span data-ttu-id="5088e-124">W tym wideo projektu o nazwie **APIMAADDemo**.</span><span class="sxs-lookup"><span data-stu-id="5088e-124">In this video the project is named **APIMAADDemo**.</span></span> <span data-ttu-id="5088e-125">Kliknij przycisk **OK**, aby utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="5088e-125">Click **OK** to create the project.</span></span> 

![Visual Studio][api-management-new-web-app]

<span data-ttu-id="5088e-127">Kliknij przycisk **interfejsu API sieci Web** z **wybierz listę szablonów** do tworzenia projektu interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5088e-127">Click **Web API** from the **Select a template list** to create a Web API project.</span></span> <span data-ttu-id="5088e-128">Aby skonfigurować uwierzytelnianie katalogu Azure kliknij **Zmień uwierzytelnianie**.</span><span class="sxs-lookup"><span data-stu-id="5088e-128">To configure Azure Directory Authentication click **Change Authentication**.</span></span>

![Nowy projekt][api-management-new-project]

<span data-ttu-id="5088e-130">Kliknij przycisk **konta organizacyjne**, a następnie określ **domeny** dzierżawy usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="5088e-130">Click **Organizational Accounts**, and specify the **Domain** of your AAD tenant.</span></span> <span data-ttu-id="5088e-131">W tym przykładzie domena jest **DemoAPIM.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="5088e-131">In this example the domain is **DemoAPIM.onmicrosoft.com**.</span></span> <span data-ttu-id="5088e-132">Domeny katalogu można je uzyskać z **domen** katalogu.</span><span class="sxs-lookup"><span data-stu-id="5088e-132">The domain of your directory can be obtained from the **Domains** tab of your directory.</span></span>

![Domeny][api-management-aad-domains]

<span data-ttu-id="5088e-134">Skonfiguruj odpowiednie ustawienia w **Zmień uwierzytelnianie** okno dialogowe i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5088e-134">Configure the desired settings in the **Change Authentication** dialog box and click **OK**.</span></span>

![Zmienianie uwierzytelniania][api-management-change-authentication]

<span data-ttu-id="5088e-136">Po kliknięciu **OK** programu Visual Studio będzie próbował zarejestrować aplikację w usłudze Azure AD w katalogu i może pojawić się prośba do logowania przez program Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5088e-136">When you click **OK** Visual Studio will attempt to register your application with your Azure AD directory and you may be prompted to sign in by Visual Studio.</span></span> <span data-ttu-id="5088e-137">Zaloguj się przy użyciu konta administracyjnego dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="5088e-137">Sign in using an administrative account for your directory.</span></span>

![Zaloguj się do programu Visual Studio][api-management-sign-in-vidual-studio]

<span data-ttu-id="5088e-139">Aby skonfigurować ten projekt jako interfejs API sieci Web Azure pole wyboru dla **Hostuj w chmurze** , a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="5088e-139">To configure this project as an Azure Web API check the box for **Host in the cloud** and then click **OK**.</span></span>

![Nowy projekt][api-management-new-project-cloud]

<span data-ttu-id="5088e-141">Monit logowanie do platformy Azure, a następnie można skonfigurować aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5088e-141">You may be prompted to sign in to Azure, and then you can configure the Web App.</span></span>

![Konfigurowanie][api-management-configure-web-app]

<span data-ttu-id="5088e-143">W tym przykładzie nowy **planu usługi aplikacji** o nazwie **APIMAADDemo** jest określona.</span><span class="sxs-lookup"><span data-stu-id="5088e-143">In this example a new **App Service plan** named **APIMAADDemo** is specified.</span></span>

<span data-ttu-id="5088e-144">Kliknij przycisk **OK** do skonfigurowania aplikacji sieci Web i utworzyć projekt.</span><span class="sxs-lookup"><span data-stu-id="5088e-144">Click **OK** to configure the Web App and create the project.</span></span>

## <a name="add-the-code-to-the-web-api-project"></a><span data-ttu-id="5088e-145">Dodaj kod do projektu interfejsu API sieci Web</span><span class="sxs-lookup"><span data-stu-id="5088e-145">Add the code to the Web API project</span></span>
<span data-ttu-id="5088e-146">Następny krok w wideo dodaje kod do projektu interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5088e-146">The next step in the video adds the code to the Web API project.</span></span> <span data-ttu-id="5088e-147">Ten krok zostanie uruchomiony na 4:35.</span><span class="sxs-lookup"><span data-stu-id="5088e-147">This step starts at 4:35.</span></span>

<span data-ttu-id="5088e-148">Interfejs API sieci Web, w tym przykładzie implementuje Kalkulator podstawowe usługi przy użyciu modelu i kontrolera.</span><span class="sxs-lookup"><span data-stu-id="5088e-148">The Web API in this example implements a basic calculator service using a model and a controller.</span></span> <span data-ttu-id="5088e-149">Aby dodać model dla usługi, kliknij prawym przyciskiem myszy **modele** w **Eksploratora rozwiązań** i wybierz polecenie **Dodaj**, **klasy**.</span><span class="sxs-lookup"><span data-stu-id="5088e-149">To add the model for the service, right-click **Models** in **Solution Explorer** and choose **Add**, **Class**.</span></span> <span data-ttu-id="5088e-150">Nazwa klasy `CalcInput` i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5088e-150">Name the class `CalcInput` and click **Add**.</span></span>

<span data-ttu-id="5088e-151">Dodaj następujące `using` instrukcji na początku `CalcInput.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="5088e-151">Add the following `using` statement to the top of the `CalcInput.cs` file.</span></span>

```c#
using Newtonsoft.Json;
```

<span data-ttu-id="5088e-152">Zastąp następujący kod wygenerowanej klasy.</span><span class="sxs-lookup"><span data-stu-id="5088e-152">Replace the generated class with the following code.</span></span>

```c#
public class CalcInput
{
    [JsonProperty(PropertyName = "a")]
    public int a;

    [JsonProperty(PropertyName = "b")]
    public int b;
}
```

<span data-ttu-id="5088e-153">Kliknij prawym przyciskiem myszy **kontrolerów** w **Eksploratora rozwiązań** i wybierz polecenie **Dodaj**->**kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="5088e-153">Right-click **Controllers** in **Solution Explorer** and choose **Add**->**Controller**.</span></span> <span data-ttu-id="5088e-154">Wybierz **kontrolera 2 interfejsu API sieci Web — pusty** i kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5088e-154">Choose **Web API 2 Controller - Empty** and click **Add**.</span></span> <span data-ttu-id="5088e-155">Typ **CalcController** kontrolera nazwę, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5088e-155">Type **CalcController** for the Controller name and click **Add**.</span></span>

![Dodawanie kontrolera][api-management-add-controller]

<span data-ttu-id="5088e-157">Dodaj następujące `using` instrukcji na początku `CalcController.cs` pliku.</span><span class="sxs-lookup"><span data-stu-id="5088e-157">Add the following `using` statement to the top of the `CalcController.cs` file.</span></span>

```c#
using System.IO;
using System.Web;
using APIMAADDemo.Models;
```

<span data-ttu-id="5088e-158">Zastąp następujący kod klasy wygenerowanym kontrolerze.</span><span class="sxs-lookup"><span data-stu-id="5088e-158">Replace the generated controller class with the following code.</span></span> <span data-ttu-id="5088e-159">Implementuje ten kod `Add`, `Subtract`, `Multiply`, i `Divide` operacji podstawowe Kalkulator interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5088e-159">This code implements the `Add`, `Subtract`, `Multiply`, and `Divide` operations of the Basic Calculator API.</span></span>

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

<span data-ttu-id="5088e-160">Naciśnij klawisz **F6** do tworzenia i Zweryfikuj rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="5088e-160">Press **F6** to build and verify the solution.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="5088e-161">Publikowanie projektu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="5088e-161">Publish the project to Azure</span></span>
<span data-ttu-id="5088e-162">W tym kroku programu Visual Studio projektu została opublikowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5088e-162">In this step the Visual Studio project is published to Azure.</span></span> <span data-ttu-id="5088e-163">W tym kroku wideo rozpoczyna się od 5:45.</span><span class="sxs-lookup"><span data-stu-id="5088e-163">This step of the video starts at 5:45.</span></span>

<span data-ttu-id="5088e-164">Aby opublikować projekt na platformie Azure, kliknij prawym przyciskiem myszy **APIMAADDemo** projekt w programie Visual Studio i wybierz pozycję **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="5088e-164">To publish the project to Azure, right-click the **APIMAADDemo** project in Visual Studio and choose **Publish**.</span></span> <span data-ttu-id="5088e-165">Zachowaj ustawienia domyślne **publikowanie w sieci Web** okno dialogowe i kliknij przycisk **publikowania**.</span><span class="sxs-lookup"><span data-stu-id="5088e-165">Keep the default settings in the **Publish Web** dialog box and click **Publish**.</span></span>

![Publikowanie w sieci Web][api-management-web-publish]

## <a name="grant-permissions-to-the-azure-ad-backend-service-application"></a><span data-ttu-id="5088e-167">Udzielanie uprawnień do wewnętrznej bazy danych aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5088e-167">Grant permissions to the Azure AD backend service application</span></span>
<span data-ttu-id="5088e-168">Nową aplikację usługi wewnętrznej bazy danych jest tworzony w katalogu usługi Azure AD jako część procesu konfigurowania i publikowania projektu interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5088e-168">A new application for the backend service is created in your Azure AD directory as part of the configuring and publishing process of your Web API project.</span></span> <span data-ttu-id="5088e-169">W tym kroku wideo, zaczynając od 6:13 przyznano uprawnienia do zaplecza interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5088e-169">In this step of the video, starting at 6:13, permissions are granted to the Web API backend.</span></span>

![Aplikacja][api-management-aad-backend-app]

<span data-ttu-id="5088e-171">Kliknij nazwę aplikacji do konfigurowania wymaganych uprawnień.</span><span class="sxs-lookup"><span data-stu-id="5088e-171">Click the name of the application to configure the required permissions.</span></span> <span data-ttu-id="5088e-172">Przejdź do **Konfiguruj** karcie i przewiń w dół do **uprawnień dotyczących innych aplikacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="5088e-172">Navigate to the **Configure** tab and scroll down to the **permissions to other applications** section.</span></span> <span data-ttu-id="5088e-173">Kliknij przycisk **uprawnienia aplikacji** listy rozwijanej obok **Windows** **usługi Azure Active Directory**, pole wyboru dla **odczytuj dane katalogu**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5088e-173">Click the **Application Permissions** drop-down beside **Windows** **Azure Active Directory**, check the box for **Read directory data**, and click **Save**.</span></span>

![Dodaj uprawnienia][api-management-aad-add-permissions]

> [!NOTE]
> <span data-ttu-id="5088e-175">Jeśli **Windows** **usługi Azure Active Directory** jest niewymienione w obszarze uprawnienia do innych aplikacji, kliknij przycisk **dodać aplikację** i dodaj go do listy.</span><span class="sxs-lookup"><span data-stu-id="5088e-175">If **Windows** **Azure Active Directory** is not listed under permissions to other applications, click **Add application** and add it from the list.</span></span>
> 
> 

<span data-ttu-id="5088e-176">Zanotuj **identyfikator URI aplikacji** do użycia w kolejnym kroku po skonfigurowaniu aplikacji usługi Azure AD do portalu dla deweloperów usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="5088e-176">Make a note of the **App Id URI** for use in a subsequent step when an Azure AD application is configured for the API Management developer portal.</span></span>

![Identyfikator URI. Identyfikator aplikacji][api-management-aad-sso-uri]

## <a name="import-the-web-api-into-api-management"></a><span data-ttu-id="5088e-178">Importowanie interfejsu API sieci Web do zarządzania interfejsem API</span><span class="sxs-lookup"><span data-stu-id="5088e-178">Import the Web API into API Management</span></span>
<span data-ttu-id="5088e-179">Interfejsy API są skonfigurowane z portalu wydawcy interfejsu API, który jest dostępny za pośrednictwem portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5088e-179">APIs are configured from the API publisher portal, which is accessed through the Azure Portal.</span></span> <span data-ttu-id="5088e-180">Aby uzyskać do niej dostęp, kliknij przycisk **portal wydawcy** na pasku narzędzi usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="5088e-180">To reach it, click **Publisher portal** from the toolbar of your API Management service.</span></span> <span data-ttu-id="5088e-181">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w [pierwszy interfejs API zarządzania] [ Manage your first API] samouczka.</span><span class="sxs-lookup"><span data-stu-id="5088e-181">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Manage your first API][Manage your first API] tutorial.</span></span>

![Portal wydawcy][api-management-management-console]

<span data-ttu-id="5088e-183">Operacje mogą być [ręcznie dodawać do interfejsów API](api-management-howto-add-operations.md), lub mogą być importowane.</span><span class="sxs-lookup"><span data-stu-id="5088e-183">Operations can be [added to APIs manually](api-management-howto-add-operations.md), or they can be imported.</span></span> <span data-ttu-id="5088e-184">W tym wideo operacje są importowane w formacie struktury Swagger, zaczynając od 6:40.</span><span class="sxs-lookup"><span data-stu-id="5088e-184">In this video, operations are imported in Swagger format starting at 6:40.</span></span>

<span data-ttu-id="5088e-185">Utwórz plik o nazwie `calcapi.json` z następującą zawartość, a następnie zapisz go na komputerze.</span><span class="sxs-lookup"><span data-stu-id="5088e-185">Create a file named `calcapi.json` with following contents and save it to your computer.</span></span> <span data-ttu-id="5088e-186">Upewnij się, że `host` atrybutu punktów z wewnętrzną bazą danych interfejsu API sieci Web.</span><span class="sxs-lookup"><span data-stu-id="5088e-186">Ensure that the `host` attribute points to your Web API backend.</span></span> <span data-ttu-id="5088e-187">W tym przykładzie `"host": "apimaaddemo.azurewebsites.net"` jest używany.</span><span class="sxs-lookup"><span data-stu-id="5088e-187">In this example `"host": "apimaaddemo.azurewebsites.net"` is used.</span></span>

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

<span data-ttu-id="5088e-188">Aby zaimportować interfejs API kalkulatora, kliknij opcję **Interfejsy API** w menu **API Management** po lewej stronie, a następnie kliknij przycisk **Importuj interfejs API**.</span><span class="sxs-lookup"><span data-stu-id="5088e-188">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Przycisk do importowania interfejsu API][api-management-import-api]

<span data-ttu-id="5088e-190">Wykonaj poniższe kroki, aby skonfigurować Kalkulator interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5088e-190">Perform the following steps to configure the calculator API.</span></span>

1. <span data-ttu-id="5088e-191">Kliknij przycisk **z pliku**, przejdź do `calculator.json` można zapisać pliku, a następnie kliknij przycisk **Swagger** przycisk radiowy.</span><span class="sxs-lookup"><span data-stu-id="5088e-191">Click **From file**, browse to the `calculator.json` file you saved, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="5088e-192">Typ **obliczenia** do **sufiks adresu URL interfejsu API sieci Web** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5088e-192">Type **calc** into the **Web API URL suffix** textbox.</span></span>
3. <span data-ttu-id="5088e-193">Kliknij pole **Produkty (opcjonalne)** i wybierz produkt **Starter**.</span><span class="sxs-lookup"><span data-stu-id="5088e-193">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="5088e-194">Kliknij przycisk **Zapisz**, aby zaimportować interfejs API.</span><span class="sxs-lookup"><span data-stu-id="5088e-194">Click **Save** to import the API.</span></span>

![Dodawanie nowego interfejsu API][api-management-import-new-api]

<span data-ttu-id="5088e-196">Po zaimportowaniu interfejsu API w portalu wydawcy zostanie wyświetlona strona podsumowania dotycząca interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5088e-196">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

## <a name="call-the-api-unsuccessfully-from-the-developer-portal"></a><span data-ttu-id="5088e-197">Wywołanie interfejsu API niepomyślnie z portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="5088e-197">Call the API unsuccessfully from the developer portal</span></span>
<span data-ttu-id="5088e-198">W tym momencie interfejsu API został zaimportowany do interfejsu API zarządzania, ale nie jeszcze można wywołać pomyślnie z portalu dla deweloperów, ponieważ usługi wewnętrznej bazy danych jest chroniony za pomocą uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5088e-198">At this point, the API has been imported into API Management, but cannot yet be called successfully from the developer portal because the backend service is protected with Azure AD authentication.</span></span> <span data-ttu-id="5088e-199">To jest przedstawiona w wideo, zaczynając od 7:40, wykonując następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="5088e-199">This is demonstrated in the video starting at 7:40 using the following steps.</span></span>

<span data-ttu-id="5088e-200">Kliknij przycisk **portalu dla deweloperów** z prawym górnym rogu strony portalu wydawcy.</span><span class="sxs-lookup"><span data-stu-id="5088e-200">Click **Developer portal** from the top-right side of the publisher portal.</span></span>

![Portal dla deweloperów][api-management-developer-portal-menu]

<span data-ttu-id="5088e-202">Kliknij przycisk **interfejsów API** i kliknij przycisk **Kalkulator** interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5088e-202">Click **APIs** and click the **Calculator** API.</span></span>

![Portal dla deweloperów][api-management-dev-portal-apis]

<span data-ttu-id="5088e-204">Kliknij przycisk **wypróbuj**.</span><span class="sxs-lookup"><span data-stu-id="5088e-204">Click **Try it**.</span></span>

![Wypróbuj][api-management-dev-portal-try-it]

<span data-ttu-id="5088e-206">Kliknij przycisk **wysyłania** i zwróć uwagę na stan odpowiedzi **401 nieautoryzowane**.</span><span class="sxs-lookup"><span data-stu-id="5088e-206">Click **Send** and note the response status of **401 Unauthorized**.</span></span>

![Send][api-management-dev-portal-send-401]

<span data-ttu-id="5088e-208">Nie ma autoryzacji żądania, ponieważ interfejs API zaplecza jest chroniony przez usługę Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5088e-208">The request is unauthorized because the backend API is protected by Azure Active Directory.</span></span> <span data-ttu-id="5088e-209">Przed pomyślnym wywołanie interfejsu API dewelopera portal musi być skonfigurowana do autoryzowania deweloperów korzystających z protokołu OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="5088e-209">Before successfully calling the API the developer portal must be configured to authorize developers using OAuth 2.0.</span></span> <span data-ttu-id="5088e-210">Ten proces jest opisane w poniższych sekcjach.</span><span class="sxs-lookup"><span data-stu-id="5088e-210">This process is described in the following sections.</span></span>

## <a name="register-the-developer-portal-as-an-aad-application"></a><span data-ttu-id="5088e-211">Zarejestruj portalu dla deweloperów jako aplikację AAD</span><span class="sxs-lookup"><span data-stu-id="5088e-211">Register the developer portal as an AAD application</span></span>
<span data-ttu-id="5088e-212">Pierwszym etapem konfigurowania portalu dla deweloperów do autoryzacji deweloperów korzystających z protokołu OAuth 2.0 jest zarejestrowanie go jako aplikację AAD portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="5088e-212">The first step in configuring the developer portal to authorize developers using OAuth 2.0 is to register the developer portal as an AAD application.</span></span> <span data-ttu-id="5088e-213">Jest to wykazać, zaczynając od 8:27 wideo.</span><span class="sxs-lookup"><span data-stu-id="5088e-213">This is demonstrated starting at 8:27 in the video.</span></span>

<span data-ttu-id="5088e-214">Przejdź do dzierżawy usługi Azure AD z pierwszym krokiem ten film, w tym przykładzie **APIMDemo** i przejdź do **aplikacji** kartę.</span><span class="sxs-lookup"><span data-stu-id="5088e-214">Navigate to the Azure AD tenant from the first step of this video, in this example **APIMDemo** and navigate to the **Applications** tab.</span></span>

![Nowa aplikacja][api-management-aad-new-application-devportal]

<span data-ttu-id="5088e-216">Kliknij przycisk **Dodaj** przycisk, aby utworzyć nową aplikację usługi Azure Active Directory, a następnie wybierz pozycję **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="5088e-216">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Nowa aplikacja][api-management-new-aad-application-menu]

<span data-ttu-id="5088e-218">Wybierz **sieci Web, aplikacji i/lub interfejs API sieci Web**, wprowadź nazwę i kliknij strzałkę dalej.</span><span class="sxs-lookup"><span data-stu-id="5088e-218">Choose **Web application and/or Web API**, enter a name, and click the next arrow.</span></span> <span data-ttu-id="5088e-219">W tym przykładzie **APIMDeveloperPortal** jest używany.</span><span class="sxs-lookup"><span data-stu-id="5088e-219">In this example **APIMDeveloperPortal** is used.</span></span>

![Nowa aplikacja][api-management-aad-new-application-devportal-1]

<span data-ttu-id="5088e-221">Aby uzyskać **adres URL logowania** wprowadź adres URL usługi API Management i Dołącz `/signin`.</span><span class="sxs-lookup"><span data-stu-id="5088e-221">For **Sign-on URL** enter the URL of your API Management service and append `/signin`.</span></span> <span data-ttu-id="5088e-222">W tym przykładzie `https://contoso5.portal.azure-api.net/signin` jest używany.</span><span class="sxs-lookup"><span data-stu-id="5088e-222">In this example `https://contoso5.portal.azure-api.net/signin` is used.</span></span>

<span data-ttu-id="5088e-223">Aby uzyskać **adres URL identyfikatora aplikacji** wprowadź adres URL usługi API Management i Dołącz niektóre unikatowe znaki.</span><span class="sxs-lookup"><span data-stu-id="5088e-223">For **App Id URL** enter the URL of your API Management service and append some unique characters.</span></span> <span data-ttu-id="5088e-224">Mogą to być wszystkie odpowiednie znaki w tym przykładzie `https://contoso5.portal.azure-api.net/dp` jest używany.</span><span class="sxs-lookup"><span data-stu-id="5088e-224">These can be any desired characters and in this example `https://contoso5.portal.azure-api.net/dp` is used.</span></span> <span data-ttu-id="5088e-225">Gdy żądane **właściwości aplikacji** są skonfigurowane, kliknij znacznik wyboru, aby utworzyć aplikację.</span><span class="sxs-lookup"><span data-stu-id="5088e-225">When the  desired **App properties** are configured, click the check mark to create the application.</span></span>

![Nowa aplikacja][api-management-aad-new-application-devportal-2]

## <a name="configure-an-api-management-oauth-20-authorization-server"></a><span data-ttu-id="5088e-227">Konfigurowanie serwera autoryzacji usługi API Management OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="5088e-227">Configure an API Management OAuth 2.0 authorization server</span></span>
<span data-ttu-id="5088e-228">Następnym krokiem jest skonfigurowanie serwera autoryzacji OAuth 2.0 w usłudze API Management.</span><span class="sxs-lookup"><span data-stu-id="5088e-228">The next step is to configure an OAuth 2.0 authorization server in API Management.</span></span> <span data-ttu-id="5088e-229">Ten krok jest przedstawiona w wideo, zaczynając od 9:43.</span><span class="sxs-lookup"><span data-stu-id="5088e-229">This step is demonstrated in the video starting at 9:43.</span></span>

<span data-ttu-id="5088e-230">Kliknij przycisk **zabezpieczeń** z interfejsu API zarządzania menu po lewej stronie, kliknij przycisk **OAuth 2.0**, a następnie kliknij przycisk **dodać autoryzacji** serwera.</span><span class="sxs-lookup"><span data-stu-id="5088e-230">Click **Security** from the API Management menu on the left, click **OAuth 2.0**, and then click **Add authorization** server.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server]

<span data-ttu-id="5088e-232">Wprowadź nazwę i opcjonalny opis w **nazwa** i **opis** pola.</span><span class="sxs-lookup"><span data-stu-id="5088e-232">Enter a name and an optional description in the **Name** and **Description** fields.</span></span> <span data-ttu-id="5088e-233">Te pola są używane do identyfikowania serwera autoryzacji OAuth 2.0 w wystąpieniu usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="5088e-233">These fields are used to identify the OAuth 2.0 authorization server within the API Management service instance.</span></span> <span data-ttu-id="5088e-234">W tym przykładzie **pokaz serwera autoryzacji** jest używany.</span><span class="sxs-lookup"><span data-stu-id="5088e-234">In this example **Authorization server demo** is used.</span></span> <span data-ttu-id="5088e-235">Później podczas określania serwera OAuth 2.0, który będzie używany do uwierzytelniania dla interfejsu API, możesz wybrać tej nazwy.</span><span class="sxs-lookup"><span data-stu-id="5088e-235">Later when you specify an OAuth 2.0 server to be used for authentication for an API, you will select this name.</span></span>

<span data-ttu-id="5088e-236">Aby uzyskać **adres URL strony rejestracji klienta** wprowadź wartość symbolu zastępczego, takich jak `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="5088e-236">For the **Client registration page URL** enter a placeholder value such as `http://localhost`.</span></span>  <span data-ttu-id="5088e-237">**Adres URL strony rejestracji klienta** wskazuje strona, do której użytkownicy mogą używać, aby utworzyć i skonfigurować swoje własne konta dla dostawcy OAuth 2.0, które obsługują zarządzanie kontami użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5088e-237">The **Client registration page URL** points to the page that users can use to create and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="5088e-238">W tym przykładzie użytkowników nie tworzyć i konfigurować własne konta, więc symbol zastępczy jest używany.</span><span class="sxs-lookup"><span data-stu-id="5088e-238">In this example users do not create and configure their own accounts so a placeholder is used.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-1]

<span data-ttu-id="5088e-240">Następnie określ **adres URL punktu końcowego autoryzacji** i **adres URL punktu końcowego tokenu**.</span><span class="sxs-lookup"><span data-stu-id="5088e-240">Next, specify **Authorization endpoint URL** and **Token endpoint URL**.</span></span>

![Serwer autoryzacji][api-management-add-authorization-server-1a]

<span data-ttu-id="5088e-242">Te wartości można pobrać z **punkty końcowe aplikacji** strony aplikacji AAD utworzona dla portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="5088e-242">These values can be retrieved from the **App Endpoints** page of the AAD application you created for the developer portal.</span></span> <span data-ttu-id="5088e-243">Aby uzyskać dostęp do punktów końcowych, przejdź do **Konfigurowanie** aplikacji AAD i kliknij polecenie **wyświetlić punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="5088e-243">To access the endpoints navigate to the **Configure** tab for the AAD application and click **View endpoints**.</span></span>

![Aplikacja][api-management-aad-devportal-application]

![Wyświetl punkty końcowe][api-management-aad-view-endpoints]

<span data-ttu-id="5088e-246">Kopiuj **punktu końcowego autoryzacji OAuth 2.0** i wklej ją do **adres URL punktu końcowego autoryzacji** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5088e-246">Copy the **OAuth 2.0 authorization endpoint** and paste it into the **Authorization endpoint URL** textbox.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-2]

<span data-ttu-id="5088e-248">Kopiuj **punkt końcowy tokenu OAuth 2.0** i wklej ją do **tokenu końcowego adresu URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5088e-248">Copy the **OAuth 2.0 token endpoint** and paste it into the **Token endpoint URL** textbox.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-2a]

<span data-ttu-id="5088e-250">Oprócz wklejenie punktu końcowego tokenu, Dodaj parametr treści dodatkowe o nazwie **zasobów** i wykorzystanie wartości **identyfikator URI aplikacji** z usługi AAD aplikacji dla usługi wewnętrznej bazy danych, który został utworzony, gdy projekt programu Visual Studio został opublikowany.</span><span class="sxs-lookup"><span data-stu-id="5088e-250">In addition to pasting in the token endpoint, add an additional body parameter named **resource** and for the value use the **App Id URI** from the AAD application for the backend service that was created when the Visual Studio project was published.</span></span>

![Identyfikator URI. Identyfikator aplikacji][api-management-aad-sso-uri]

<span data-ttu-id="5088e-252">Następnie określ poświadczenia klienta.</span><span class="sxs-lookup"><span data-stu-id="5088e-252">Next, specify the client credentials.</span></span> <span data-ttu-id="5088e-253">Są to poświadczenia dla zasobu, który ma dostęp, w tym przypadku portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="5088e-253">These are the credentials for the resource you want to access, in this case the developer portal.</span></span>

![Poświadczenia klienta][api-management-client-credentials]

<span data-ttu-id="5088e-255">Aby uzyskać **identyfikator klienta**, przejdź do **Konfiguruj** aplikacji AAD w portalu dla deweloperów i kopia **identyfikator klienta**.</span><span class="sxs-lookup"><span data-stu-id="5088e-255">To get the **Client Id**, navigate to the **Configure** tab of the AAD application for the developer portal and copy the **Client Id**.</span></span>

<span data-ttu-id="5088e-256">Aby uzyskać **klucz tajny klienta** kliknij **wybierz czas trwania** listy rozwijanej w **klucze** sekcji i określ interwał.</span><span class="sxs-lookup"><span data-stu-id="5088e-256">To get the **Client Secret** click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="5088e-257">W tym przykładzie używany jest 1 rok.</span><span class="sxs-lookup"><span data-stu-id="5088e-257">In this example 1 year is used.</span></span>

![Identyfikator klienta][api-management-aad-client-id]

<span data-ttu-id="5088e-259">Kliknij przycisk **zapisać** do zapisania konfiguracji, a następnie wyświetlić klucz.</span><span class="sxs-lookup"><span data-stu-id="5088e-259">Click **Save** to save the configuration and display the key.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="5088e-260">Zanotuj tego klucza.</span><span class="sxs-lookup"><span data-stu-id="5088e-260">Make a note of this key.</span></span> <span data-ttu-id="5088e-261">Po zamknięciu okna konfiguracji usługi Azure Active Directory, klucz nie może ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="5088e-261">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

<span data-ttu-id="5088e-262">Kopiuj do Schowka klucz, przełączyć się do portalu wydawcy, Wklej klucz do **klucz tajny klienta** polem tekstowym i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5088e-262">Copy the key to the clipboard, switch back to the publisher portal, paste the key into the **Client Secret** textbox, and click **Save**.</span></span>

![Dodawanie serwera autoryzacji][api-management-add-authorization-server-3]

<span data-ttu-id="5088e-264">Bezpośrednio po poświadczeń klienta jest udzielania kodu autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="5088e-264">Immediately following the client credentials is an authorization code grant.</span></span> <span data-ttu-id="5088e-265">Ten kod autoryzacji i przełącznika z powrotem do aplikacji portalu dewelopera usługi Azure AD kopiowania skonfigurować stronę i Wklej udzielania autoryzacji do **adres URL odpowiedzi** , a następnie kliknij przycisk **zapisać** ponownie.</span><span class="sxs-lookup"><span data-stu-id="5088e-265">Copy this authorization code and switch back to your Azure AD developer portal application configure page, and paste the authorization grant into the **Reply URL** field, and click **Save** again.</span></span>

![Adres URL odpowiedzi][api-management-aad-reply-url]

<span data-ttu-id="5088e-267">Następnym krokiem jest skonfigurowanie uprawnień dla portalu dla deweloperów usługi AAD aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5088e-267">The next step is to configure the permissions for the developer portal AAD application.</span></span> <span data-ttu-id="5088e-268">Kliknij przycisk **uprawnienia aplikacji** i pole wyboru dla **odczytuj dane katalogu**.</span><span class="sxs-lookup"><span data-stu-id="5088e-268">Click **Application Permissions** and check the box for **Read directory data**.</span></span> <span data-ttu-id="5088e-269">Kliknij przycisk **zapisać** zapisać tę zmianę, a następnie kliknij przycisk **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="5088e-269">Click **Save** to save this change, and then click **Add application**.</span></span>

![Dodaj uprawnienia][api-management-add-devportal-permissions]

<span data-ttu-id="5088e-271">Kliknij ikonę wyszukiwania typu **APIM** na uruchamianie z polem, wybierz **APIMAADDemo**i kliknij znacznik wyboru, aby zapisać.</span><span class="sxs-lookup"><span data-stu-id="5088e-271">Click the search icon, type **APIM** into the Starting with box, select **APIMAADDemo**, and click the check mark to save.</span></span>

![Dodaj uprawnienia][api-management-aad-add-app-permissions]

<span data-ttu-id="5088e-273">Kliknij przycisk **delegowane uprawnienia** dla **APIMAADDemo** i pole wyboru dla **APIMAADDemo dostępu**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5088e-273">Click **Delegated Permissions** for **APIMAADDemo** and check the box for **Access APIMAADDemo**, and click **Save**.</span></span> <span data-ttu-id="5088e-274">Dzięki temu deweloper aplikacji portalu do uzyskania dostępu do usługi zaplecza.</span><span class="sxs-lookup"><span data-stu-id="5088e-274">This allows the developer portal application to access the backend service.</span></span>

![Dodaj uprawnienia][api-management-aad-add-delegated-permissions]

## <a name="enable-oauth-20-user-authorization-for-the-calculator-api"></a><span data-ttu-id="5088e-276">Włączanie autoryzacji użytkownika OAuth 2.0 dla interfejsu API Kalkulator</span><span class="sxs-lookup"><span data-stu-id="5088e-276">Enable OAuth 2.0 user authorization for the Calculator API</span></span>
<span data-ttu-id="5088e-277">Teraz, gdy serwer protokołu OAuth 2.0 jest skonfigurowany, możesz je określić ustawienia zabezpieczeń dla interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5088e-277">Now that the OAuth 2.0 server is configured, you can specify it in the security settings for your API.</span></span> <span data-ttu-id="5088e-278">Ten krok jest przedstawiona w wideo, zaczynając od 14:30.</span><span class="sxs-lookup"><span data-stu-id="5088e-278">This step is demonstrated in the video starting at 14:30.</span></span>

<span data-ttu-id="5088e-279">Kliknij przycisk **interfejsów API** w menu po lewej stronie, a następnie kliknij przycisk **Kalkulator** Aby wyświetlić i skonfigurować jego ustawienia.</span><span class="sxs-lookup"><span data-stu-id="5088e-279">Click **APIs** in the left menu, and click  **Calculator** to view and configure its settings.</span></span>

![Kalkulator interfejsu API][api-management-calc-api]

<span data-ttu-id="5088e-281">Przejdź do **zabezpieczeń** karcie wyboru **OAuth 2.0** pole wyboru, wybierz serwer autoryzacji żądaną z **serwera autoryzacji** listy rozwijanej i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5088e-281">Navigate to the **Security** tab, check the **OAuth 2.0** checkbox, select the desired authorization server from the **Authorization server** drop-down, and click **Save**.</span></span>

![Kalkulator interfejsu API][api-management-enable-aad-calculator]

## <a name="successfully-call-the-calculator-api-from-the-developer-portal"></a><span data-ttu-id="5088e-283">Pomyślne wywołanie interfejsu API programu Kalkulator z portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="5088e-283">Successfully call the Calculator API from the developer portal</span></span>
<span data-ttu-id="5088e-284">Teraz, gdy autoryzacji OAuth 2.0 został skonfigurowany w interfejsie API, jego operacji może pomyślnie wywołana z Centrum deweloperów.</span><span class="sxs-lookup"><span data-stu-id="5088e-284">Now that the OAuth 2.0 authorization is configured on the API, its operations can be successfully called from the developer center.</span></span> <span data-ttu-id="5088e-285">Ten krok jest przedstawiona w wideo, zaczynając od 15:00.</span><span class="sxs-lookup"><span data-stu-id="5088e-285">THis step is demonstrated in the video starting at 15:00.</span></span>

<span data-ttu-id="5088e-286">Przejdź z powrotem do **Dodaj dwie liczb całkowitych** operacji usługi Kalkulator w portalu dla deweloperów i kliknij **wypróbuj**.</span><span class="sxs-lookup"><span data-stu-id="5088e-286">Navigate back to the **Add two integers** operation of the calculator service in the developer portal and click **Try it**.</span></span> <span data-ttu-id="5088e-287">Należy pamiętać, nowy element w **autoryzacji** sekcji odpowiadający właśnie dodano serwer autoryzacji.</span><span class="sxs-lookup"><span data-stu-id="5088e-287">Note the new item in the **Authorization** section corresponding to the authorization server you just added.</span></span>

![Kalkulator interfejsu API][api-management-calc-authorization-server]

<span data-ttu-id="5088e-289">Wybierz **kod autoryzacji** z autoryzacji listy rozwijanej liście, a następnie wprowadź poświadczenia konta, które będzie używane.</span><span class="sxs-lookup"><span data-stu-id="5088e-289">Select **Authorization code** from the authorization drop-down list and enter the credentials of the account to use.</span></span> <span data-ttu-id="5088e-290">Jeśli nastąpiło już zalogowanie się przy użyciu konta, które nie mogą być potrzebne.</span><span class="sxs-lookup"><span data-stu-id="5088e-290">If you are already signed in with the account you may not be prompted.</span></span>

![Kalkulator interfejsu API][api-management-devportal-authorization-code]

<span data-ttu-id="5088e-292">Kliknij przycisk **wysyłania** i zanotuj **stanu odpowiedzi** z **200 OK** i wyniki operacji w zawartości odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="5088e-292">Click **Send** and note the **Response status** of **200 OK** and the results of the operation in the response content.</span></span>

![Kalkulator interfejsu API][api-management-devportal-response]

## <a name="configure-a-desktop-application-to-call-the-api"></a><span data-ttu-id="5088e-294">Konfigurowanie aplikacji pulpitu do wywołania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5088e-294">Configure a desktop application to call the API</span></span>
<span data-ttu-id="5088e-295">Następna procedura wideo rozpoczyna się od 16:30 i konfiguruje prostą aplikację pulpitu do wywołania interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5088e-295">The next procedure in the video starts at 16:30 and configures a simple desktop application to call the API.</span></span> <span data-ttu-id="5088e-296">Pierwszym krokiem jest zarejestrować aplikację w usłudze Azure AD i nadaj mu dostęp do katalogu i usługi wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5088e-296">The first step is to register the desktop application in Azure AD and give it access to the directory and to the backend service.</span></span> <span data-ttu-id="5088e-297">Na 18:25 istnieje pokaz pulpitu aplikacji podczas wywoływania operacji na Kalkulator interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5088e-297">At 18:25 there is a demonstration of the desktop application calling an operation on the calculator API.</span></span>

## <a name="configure-a-jwt-validation-policy-to-pre-authorize-requests"></a><span data-ttu-id="5088e-298">Skonfiguruj zasady sprawdzania poprawności tokenu JWT wstępnie autoryzować żądania</span><span class="sxs-lookup"><span data-stu-id="5088e-298">Configure a JWT validation policy to pre-authorize requests</span></span>
<span data-ttu-id="5088e-299">Ostatnia procedura wideo rozpoczyna się od 20:48 i przedstawiono sposób użycia [JWT do zweryfikowania](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) zasad do wstępnie autoryzacji żądania, sprawdzając poprawność tokenów dostępu dla każdego żądania przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="5088e-299">The final procedure in the video starts at 20:48 and shows you how to use the [Validate JWT](https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT) policy to pre-authorize requests by validating the access tokens of each incoming request.</span></span> <span data-ttu-id="5088e-300">Jeśli żądanie nie jest weryfikowany przez zasady sprawdzania poprawności tokenów JWT, żądanie jest blokowany przez interfejs API zarządzania i nie jest przekazywane do wewnętrznej bazy danych.</span><span class="sxs-lookup"><span data-stu-id="5088e-300">If the request is not validated by the Validate JWT policy, the request is blocked by API Management and is not passed along to the backend.</span></span>

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

<span data-ttu-id="5088e-301">Aby innego demonstracyjne konfigurowania i korzystania z tych zasad, zobacz [177 epizodu obejmują chmury: więcej funkcji interfejsu API zarządzania](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) i szybkie przewijanie do przodu do 13:50.</span><span class="sxs-lookup"><span data-stu-id="5088e-301">For another demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="5088e-302">Szybko przewiń do przodu do 15:00, aby wyświetlić zasady skonfigurowane w edytorze zasad, a następnie do 18:50 dla pokaz wywołanie operacji z portalu dla deweloperów zarówno z i bez tokenu autoryzacji wymagane.</span><span class="sxs-lookup"><span data-stu-id="5088e-302">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5088e-303">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5088e-303">Next steps</span></span>
* <span data-ttu-id="5088e-304">Zapoznaj się z kilku [wideo](https://azure.microsoft.com/documentation/videos/index/?services=api-management) o zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="5088e-304">Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.</span></span>
* <span data-ttu-id="5088e-305">Aby uzyskać inne metody zabezpieczania usługi wewnętrznej bazy danych, zobacz [uwierzytelnianie wzajemne certyfikatu](api-management-howto-mutual-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="5088e-305">For other ways to secure your backend service, see [Mutual Certificate authentication](api-management-howto-mutual-certificates.md).</span></span>

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
