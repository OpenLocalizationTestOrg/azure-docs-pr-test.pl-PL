---
title: aaaAzure AD v2 ASP.NET Web Server wprowadzenie - Config | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="2e118-103">Tworzenie aplikacji (Express)</span><span class="sxs-lookup"><span data-stu-id="2e118-103">Create an application (Express)</span></span>
<span data-ttu-id="2e118-104">Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="2e118-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="2e118-105">Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="2e118-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="2e118-106">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="2e118-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="2e118-107">Upewnij się, że jest zaznaczona opcja hello z przewodnikiem instalacji</span><span class="sxs-lookup"><span data-stu-id="2e118-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="2e118-108">Postępuj zgodnie z tooadd instrukcje hello aplikacji tooyour adresem URL przekierowania</span><span class="sxs-lookup"><span data-stu-id="2e118-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="2e118-109">Dodawanie rozwiązania tooyour informacji o rejestracji aplikacji (zaawansowane)</span><span class="sxs-lookup"><span data-stu-id="2e118-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="2e118-110">Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="2e118-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="2e118-111">Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister aplikacji</span><span class="sxs-lookup"><span data-stu-id="2e118-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="2e118-112">Wprowadź nazwę aplikacji i poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="2e118-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="2e118-113">Upewnij się, że jest zaznaczona opcja hello instrukcje konfiguracji</span><span class="sxs-lookup"><span data-stu-id="2e118-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="2e118-114">Kliknij przycisk `Add Platform`, a następnie wybierz pozycję`Web`</span><span class="sxs-lookup"><span data-stu-id="2e118-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="2e118-115">Przejdź wstecz tooVisual Studio, w Eksploratorze rozwiązań wybierz projekt hello i przyjrzyj się okno właściwości hello (Jeśli nie widzisz okna właściwości, naciśnij klawisz F4)</span><span class="sxs-lookup"><span data-stu-id="2e118-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="2e118-116">Zmień zbyt włączony protokół SSL`True`</span><span class="sxs-lookup"><span data-stu-id="2e118-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="2e118-117">Skopiuj hello adresu URL protokołu SSL i dodać ten adres URL toohello listę adresów URL przekierowań w portalu rejestracji hello listę adresów URL przekierowań:</span><span class="sxs-lookup"><span data-stu-id="2e118-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Właściwości projektu](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="2e118-119">Dodaj następujące hello w `web.config` znajduje się w folderze głównym hello sekcji hello `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="2e118-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="2e118-120">Zastąp `ClientId` z hello został zarejestrowany identyfikator aplikacji</span><span class="sxs-lookup"><span data-stu-id="2e118-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="2e118-121">Zastąp `redirectUri` z hello SSL adres URL projektu</span><span class="sxs-lookup"><span data-stu-id="2e118-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
