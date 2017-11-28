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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a><span data-ttu-id="fc198-103">Konfigurowanie aplikacji sieci Web platformy ASP.NET z informacjami o rejestracji aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="fc198-103">Configure your ASP.NET Web App with hello application's registration information</span></span>

<span data-ttu-id="fc198-104">W tym kroku zostanie skonfigurować toouse Twojego projektu protokołu SSL, a następnie użyć hello tooconfigure SSL adres URL informacji o rejestracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fc198-104">In this step, you will configure your project toouse SSL, and then use hello SSL URL tooconfigure your application’s registration information.</span></span> <span data-ttu-id="fc198-105">Po to, dodania aplikacji hello "rejestracji rozwiązanie tooyour informacji za pośrednictwem *web.config*.</span><span class="sxs-lookup"><span data-stu-id="fc198-105">After this, add hello application’ registration information tooyour solution via *web.config*.</span></span>

1.  <span data-ttu-id="fc198-106">W Eksploratorze rozwiązań wybierz projekt hello i przyjrzyj się hello `Properties` okna (Jeśli nie widzisz okna właściwości, naciśnij klawisz F4)</span><span class="sxs-lookup"><span data-stu-id="fc198-106">In Solution Explorer, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="fc198-107">Zmień `SSL Enabled` zbyt`True`</span><span class="sxs-lookup"><span data-stu-id="fc198-107">Change `SSL Enabled` too`True`</span></span>
3.  <span data-ttu-id="fc198-108">Skopiuj wartość hello z `SSL URL` powyżej i wklej go w hello `Redirect URL` pól na powitania początku tej strony, a następnie kliknij przycisk *aktualizacji*:</span><span class="sxs-lookup"><span data-stu-id="fc198-108">Copy hello value from `SSL URL` above and paste it in hello `Redirect URL` field on hello top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="fc198-109">![Właściwości projektu](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="fc198-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="fc198-110">Dodaj następujące hello w `web.config` plik znajdujący się w folderze elementu głównego sekcji `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="fc198-110">Add hello following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
