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
## <a name="create-an-application-express"></a>Tworzenie aplikacji (Express)
Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:
1. Zarejestrować aplikację za pośrednictwem hello [portalu rejestracji aplikacji firmy Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  Wprowadź nazwę aplikacji i poczty e-mail
3.  Upewnij się, że jest zaznaczona opcja hello z przewodnikiem instalacji
4.  Postępuj zgodnie z tooadd instrukcje hello aplikacji tooyour adresem URL przekierowania

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Dodawanie rozwiązania tooyour informacji o rejestracji aplikacji (zaawansowane)
Teraz należy tooregister aplikacji hello *portalu rejestracji aplikacji Microsoft*:
1. Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister aplikacji
2. Wprowadź nazwę aplikacji i poczty e-mail 
3.  Upewnij się, że jest zaznaczona opcja hello instrukcje konfiguracji
4.  Kliknij przycisk `Add Platform`, a następnie wybierz pozycję`Web`
5.  Przejdź wstecz tooVisual Studio, w Eksploratorze rozwiązań wybierz projekt hello i przyjrzyj się okno właściwości hello (Jeśli nie widzisz okna właściwości, naciśnij klawisz F4)
6.  Zmień zbyt włączony protokół SSL`True`
7.  Skopiuj hello adresu URL protokołu SSL i dodać ten adres URL toohello listę adresów URL przekierowań w portalu rejestracji hello listę adresów URL przekierowań:<br/><br/>![Właściwości projektu](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Dodaj następujące hello w `web.config` znajduje się w folderze głównym hello sekcji hello `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
Zastąp `ClientId` z hello został zarejestrowany identyfikator aplikacji
</li>
<li>
Zastąp `redirectUri` z hello SSL adres URL projektu
</li>
</ol>
<!-- End Docs -->
