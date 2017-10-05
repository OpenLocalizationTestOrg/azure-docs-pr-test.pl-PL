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
ms.openlocfilehash: 8a1650a65e7980f4a13fa4edc7918b0099bb5464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a><span data-ttu-id="41ced-103">Konfigurowanie aplikacji sieci Web platformy ASP.NET z aplikacji informacje rejestracyjne</span><span class="sxs-lookup"><span data-stu-id="41ced-103">Configure your ASP.NET Web App with the application's registration information</span></span>

<span data-ttu-id="41ced-104">W tym kroku zostanie skonfigurować projekt do używania protokołu SSL, a następnie użyć adresu URL protokołu SSL do skonfigurowania informacji o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41ced-104">In this step, you will configure your project to use SSL, and then use the SSL URL to configure your application’s registration information.</span></span> <span data-ttu-id="41ced-105">Następnie dodaj aplikację "informacje rejestracyjne do rozwiązania za pośrednictwem *web.config*.</span><span class="sxs-lookup"><span data-stu-id="41ced-105">After this, add the application’ registration information to your solution via *web.config*.</span></span>

1.  <span data-ttu-id="41ced-106">W Eksploratorze rozwiązań wybierz projekt i przyjrzyj się `Properties` okna (Jeśli nie widzisz okna właściwości, naciśnij klawisz F4)</span><span class="sxs-lookup"><span data-stu-id="41ced-106">In Solution Explorer, select the project and look at the `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="41ced-107">Zmień `SSL Enabled` do`True`</span><span class="sxs-lookup"><span data-stu-id="41ced-107">Change `SSL Enabled` to `True`</span></span>
3.  <span data-ttu-id="41ced-108">Skopiuj wartości z `SSL URL` powyżej i wklej go w `Redirect URL` pola w górnej części strony, a następnie kliknij przycisk *aktualizacji*:</span><span class="sxs-lookup"><span data-stu-id="41ced-108">Copy the value from `SSL URL` above and paste it in the `Redirect URL` field on the top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="41ced-109">![Właściwości projektu](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="41ced-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="41ced-110">Dodaj następujący kod w `web.config` plik znajdujący się w folderze elementu głównego sekcji `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="41ced-110">Add the following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
