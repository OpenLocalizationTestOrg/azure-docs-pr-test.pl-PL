---
title: "tooget aaaHow AppSource certyfikowane dla usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Szczegółowe informacje o sposobie tooget aplikacji AppSource certyfikowane dla usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e9f07e9220afcba1120b987122fe770fe5225eed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-appsource-certified-for-azure-active-directory"></a>W jaki sposób tooget AppSource certyfikowane dla usługi Azure Active Directory
[Microsoft AppSource](https://appsource.microsoft.com/) jest miejsce docelowe dla firm użytkowników toodiscover, spróbuj, aplikacji i zarządzanie nimi z biznesowych SaaS (produktów Microsoft SaaS autonomiczny SaaS i dodatek tooexisting).

toolist autonomicznej aplikacji SaaS na AppSource, aplikacja musi akceptować rejestracji jednokrotnej z konta służbowego z firmy lub organizacji, która ma usługę Azure Active Directory. Witaj procesu logowania, należy użyć hello [OpenID Connect](./active-directory-protocols-openid-connect-code.md) lub [OAuth 2.0](./active-directory-protocols-oauth-code.md) protokołów. Integrację SAML nie jest akceptowane AppSource certyfikacji.

## <a name="guides-and-code-samples"></a>Wskazówek i przykładów kodu
Jeśli chcesz toolearn o jak toointegrate aplikacji w usłudze Azure Active Directory za pomocą Identyfikatora otwarte połączenia, wykonaj nasze wskazówki i przykłady w hello kodu [przewodnik dewelopera usługi Azure Active Directory](./active-directory-developers-guide.md#get-started "wprowadzenie Azure AD dla deweloperów").

## <a name="multi-tenant-applications"></a>Aplikacje wielodostępne

Aplikacja, która akceptuje logowania użytkowników z firmy lub organizacji mających usługi Azure Active Directory bez konieczności oddzielnego wystąpienia, konfiguracji lub wdrożenia jest znany jako *wielodostępnych aplikacji*. AppSource zaleca się, że aplikacje wdrożyć hello tooenable wielodostępność *jednym kliknięciem* wolne środowisko wersji próbnej.

W kolejności tooenable wielu dzierżawców w swojej aplikacji:
- Ustaw `Multi-Tenanted` właściwości zbyt`Yes` na informacje o rejestracji aplikacji w hello [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (domyślnie aplikacje utworzone w portalu Azure hello są skonfigurowane jako *pojedynczego dzierżawcy*)
- Aktualizacja Twojego toohello żądań toosend kodu '`common`"punktu końcowego (zaktualizować punktu końcowego hello z *https://login.microsoftonline.com/ {yourtenant}* za*https://login.microsoftonline.com/common*)
- Dla niektórych platform, takich jak ASP.NET, należy również tooupdate Twojego tooaccept kodu wielu wystawców

Aby uzyskać więcej informacji na temat obsługi wielu dzierżawców, zobacz: [jak toosign w dowolnej usługi Azure Active Directory (AD) użytkownika za pomocą hello wzorzec wielodostępnych aplikacji](./active-directory-devhowto-multi-tenant-overview.md).

### <a name="single-tenant-applications"></a>Aplikacje pojedynczej dzierżawy
Aplikacje, które akceptują tylko logowania użytkowników zdefiniowanych wystąpienia usługi Azure Active Directory są określane jako *aplikacji pojedynczej dzierżawy*. Użytkownicy zewnętrzni (łącznie z konta służbowego z innych organizacji lub osobiste konto) można zalogować tooa pojedynczej dzierżawy aplikacji po dodaniu każdego użytkownika jako *konta gościa* wystąpienie toohello usługi Azure Active Directory Aplikacja Hello jest zarejestrowana. Możesz dodać użytkowników jako gość tooan kont usługi Azure Active Directory za pośrednictwem hello [ *współpracy B2B usługi Azure AD* ](../active-directory-b2b-what-is-azure-ad-b2b.md) - i mogą to robić [programowo](../active-directory-b2b-code-samples.md). Gdy użytkownik zostanie dodany jako gość tooan konta usługi Azure Active Directory, wiadomość e-mail z zaproszeniem są wysyłane toohello użytkownik, który ma tooaccept hello zaproszenia, klikając łącze hello w hello wiadomość e-mail z zaproszeniem. Zaproszeń do skorzystania z wysyłanych użytkownika dodatkowe tooan zaproszenia organizacji, która jest również członkiem organizacji partnerskiej hello są tooaccept nie jest wymagane toosign zaproszenia w.

Aplikacje pojedynczego dzierżawcy można włączyć hello *kontaktu mnie* środowisko, ale tooenable hello jednym kliknięciem / bezpłatnej wersji próbnej środowisko, które zaleca AppSource, należy włączyć wielodostępność na aplikacji zamiast tego.


## <a name="appsource-trial-experiences"></a>Napotyka AppSource wersji próbnej

### <a name="free-trial-customer-led-trial-experience"></a>Bezpłatna wersja próbna (środowisko wersji próbnej doprowadziły klienta) 
Witaj *doprowadziły klienta wersji próbnej* to środowisko hello, które AppSource zaleca jak oferuje aplikacji tooyour dostępu jednym kliknięciem. Poniżej w jaki sposób to środowisko wygląda następująco:<br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li>Użytkownik wyszukuje aplikacji w witrynie sieci Web AppSource</li><li>Wybiera opcję "Bezpłatnej wersji próbnej"</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li>AppSource przekierowuje użytkownika tooa adres URL witryny sieci web</li><li>Witryny sieci web uruchamia hello <i>single-sign-on</i> proces automatycznie (ładowania strony)</li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li>Użytkownik jest strona przekierowywania tooMicrosoft logowania</li><li>Użytkownik podaje toosign poświadczeń w</li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li>Użytkownik wyrazi zgodę dla aplikacji</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Logowanie kończy i użytkownik jest przekierowane tooyour wstecz witryny sieci web</li><li>Użytkownik uruchamia hello bezpłatnej wersji próbnej</li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a>Skontaktować się ze mną (doprowadziły partnera środowisko wersji próbnej)
Witaj *partnera środowisko wersji próbnej* można użyć w przypadku ręcznego lub długoterminowej operacja wymaga toohappen tooprovision hello użytkownika / firmę: na przykład, aplikacja musi tooprovision maszyn wirtualnych, wystąpień bazy danych lub operacje, które przyjmują toocomplete dużo czasu. W takim przypadku po użytkownik wybiera hello *"Żądania wersji próbnej"* przycisk i wypełnia formularz, AppSource wysyła hello informacje kontaktowe użytkownika. Po otrzymaniu tych informacji, następnie udostępnić hello środowiska i wysłać hello instrukcje toohello użytkownika, w jaki sposób tooaccess hello środowisko wersji próbnej:<br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li>Użytkownik wyszukuje aplikacji w witrynie sieci web AppSource</li><li>Wybiera opcję "Skontaktuj się z Me"</li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li>Wypełnia formularz informacje kontaktowe</li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td>Odbieranie informacji o użytkowniku</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td>Konfigurowanie środowiska</td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td>Skontaktuj się z użytkownikiem z informacjami o wersji próbnej</td>
        </tr>
        </table><br/><br/>
        <ul><li>Odbieranie informacji i wersji próbnej wystąpienia ustawienia użytkownika</li><li>Wyślij hello hyperlink tooaccess użytkownika toohello aplikacji</li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li>Użytkownik uzyskuje dostęp do aplikacji i pełne hello single-sign-on procesu</li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li>Użytkownik wyrazi zgodę dla aplikacji</li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li>Logowanie kończy i użytkownik jest przekierowane tooyour wstecz witryny sieci web</li><li>Użytkownik uruchamia hello bezpłatnej wersji próbnej</li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a>Więcej informacji
Aby uzyskać więcej informacji na temat środowisko wersji próbnej AppSource hello zobacz [ten film](https://aka.ms/trialexperienceforwebapps). 
 
## <a name="next-steps"></a>Następne kroki

- Aby uzyskać więcej informacji dotyczących tworzenia aplikacji, które obsługują usługi Azure Active Directory logowania, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios) 

- Aby uzyskać informacje dotyczące sposobu toolist aplikacji SaaS w AppSource, zobacz [informacje o partnerze AppSource](https://appsource.microsoft.com/partners)


## <a name="get-support"></a>Uzyskaj pomoc techniczną
Integracja usługi Azure Active Directory, używamy [przepełnienie stosu](http://stackoverflow.com/questions/tagged/azure-active-directory) z obsługą tooprovide społeczności hello. 

Zdecydowanie zaleca się najpierw zadać pytania w witrynie Stack Overflow i Przeglądaj istniejących toosee problemów, jeśli ktoś poprosił pytanie przed. Upewnij się, że pytania lub komentarze są oznaczane `[azure-active-directory]`.

Użyj powitania po opinii tooprovide sekcji komentarzy i pomóc nam dostosować i kształtu zawartość.

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->