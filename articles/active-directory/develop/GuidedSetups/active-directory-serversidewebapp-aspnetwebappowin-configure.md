---
title: "ASP.NET w wersji 2 usługi Azure AD w sieci Web serwera pobieranie rozpoczęte — Config | Dokumentacja firmy Microsoft"
description: "Implementowanie logowania firmy Microsoft dla rozwiązania ASP.NET z aplikacji opartych na przeglądarce sieci web tradycyjnych przy użyciu standardowego protokołu OpenID Connect"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0c627802ccfba230dcde2dafffee26cb1c895791
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="87752-103">Tworzenie aplikacji (Express)</span><span class="sxs-lookup"><span data-stu-id="87752-103">Create an application (Express)</span></span>
<span data-ttu-id="87752-104">Teraz musisz zarejestrować aplikację w *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="87752-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="87752-105">Zarejestrować aplikację za pośrednictwem [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="87752-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="87752-106">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="87752-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="87752-107">Upewnij się, że zaznaczono opcję instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="87752-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="87752-108">Postępuj zgodnie z instrukcjami, aby dodać adres URL przekierowania do aplikacji</span><span class="sxs-lookup"><span data-stu-id="87752-108">Follow the instructions to add a Redirect URL to your application</span></span>

## <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="87752-109">Dodaj swoje informacje rejestracyjne aplikacji do rozwiązania (zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="87752-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="87752-110">Teraz musisz zarejestrować aplikację w *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="87752-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="87752-111">Przejdź do [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) do rejestrowania aplikacji</span><span class="sxs-lookup"><span data-stu-id="87752-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="87752-112">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="87752-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="87752-113">Upewnij się, że jest zaznaczona opcja instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="87752-113">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="87752-114">Kliknij przycisk `Add Platform`, a następnie wybierz pozycję`Web`</span><span class="sxs-lookup"><span data-stu-id="87752-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="87752-115">Przejdź do programu Visual Studio i, w Eksploratorze rozwiązań wybierz projekt i przyjrzyj się okna właściwości (Jeśli nie widzisz okna właściwości, naciśnij klawisz F4)</span><span class="sxs-lookup"><span data-stu-id="87752-115">Go back to Visual Studio and, in Solution Explorer, select the project and look at the Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="87752-116">Zmiany, aby włączyć protokół SSL`True`</span><span class="sxs-lookup"><span data-stu-id="87752-116">Change SSL Enabled to `True`</span></span>
7.  <span data-ttu-id="87752-117">Skopiuj adres URL protokołu SSL i dodać ten adres URL do listy adresów URL przekierowań w portalu rejestracji listę adresów URL przekierowań:</span><span class="sxs-lookup"><span data-stu-id="87752-117">Copy the SSL URL and add this URL to the list of Redirect URLs in the Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Właściwości projektu](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="87752-119">Dodaj następujący kod w `web.config` znajduje się w folderze głównym w sekcji `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="87752-119">Add the following in `web.config` located in the root folder under the section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="87752-120">Zastąp `ClientId` wraz z identyfikatorem aplikacji został zarejestrowany</span><span class="sxs-lookup"><span data-stu-id="87752-120">Replace `ClientId` with the Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="87752-121">Zastąp `redirectUri` z adresem URL protokołu SSL projektu</span><span class="sxs-lookup"><span data-stu-id="87752-121">Replace `redirectUri` with the SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
