---
title: aaaAzure AD v2 ASP.NET Web Server wprowadzenie - Test | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 99c7525b9146605142180962fc2a61b3c953c064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testowanie kodu

Naciśnij klawisz `F5` toorun projektu w programie Visual Studio. Witaj przeglądarki będą otwierane i przekierować użytkownika za*http://localhost: {port}* gdzie zobaczysz hello *Zaloguj się przy użyciu programu Microsoft* przycisku. Przejdź dalej i kliknij ją toosign w.

Gdy wszystko będzie gotowe tootest, użyj służbowego (Azure Active Directory) służbowe lub osobiste (live.com, outlook.com) konta toosign w. 

![Zaloguj się przy okna przeglądarki Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin.png)

![Zaloguj się przy okna przeglądarki Microsoft](media/active-directory-serversidewebapp-aspnetwebappowin-test/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a>Oczekiwanych rezultatów
Po zalogowaniu użytkownik hello jest przekierowane toohello strony głównej witryny sieci web, czyli hello URL HTTPS określony w aplikacji informacje rejestracyjne w hello portalu rejestracji aplikacji firmy Microsoft. Ta strona zawiera obecnie *Hello {użytkownika}* i wychodzący toosign łącza, a łącze toosee hello oświadczenia użytkownika — które kontroler autoryzacji toohello łącze jest utworzony wcześniej.

### <a name="see-users-claims"></a>Zobacz oświadczenia użytkownika
Wybierz hello hyperlink toosee hello oświadczeń użytkownika. To poprowadzą toohello kontrolera i widoku, który jest tylko dostępne toousers, które są uwierzytelniane.

#### <a name="expected-results"></a>Oczekiwanych rezultatów
 Powinny pojawić się tabelę zawierającą hello podstawowe właściwości użytkowników hello rejestrowane:

| Właściwość | Wartość | Opis|
|---|---|---|
| Nazwa | {Pełna nazwa użytkownika} | Użytkownik Hello na imię i nazwisko
|Nazwa użytkownika | <span>user@domain.com</span>| używana nazwa Hello tooidentify hello zalogowany użytkownik
| Temat| {Podmiotu}|Toouniquely ciąg identyfikacji hello logowania użytkownika w różnych hello sieci web|
| Identyfikator dzierżawy| {Guid}| A *guid* toouniquely reprezentowania hello użytkownika usługi Azure Active Directory organizacji.|

Ponadto zobaczysz tabeli, w tym wszystkie oświadczenia użytkownika dołączana do uwierzytelniania żądań. Aby uzyskać listę wszystkich oświadczeń w identyfikator tokenu wyjaśnienie i zapoznaj [artykułu](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "lista oświadczeń w identyfikatorze tokenu").


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a>Test podczas uzyskiwania dostępu do metody, która ma *[Authorize]* atrybutu (opcjonalnie)
W tym kroku zostanie testu podczas uzyskiwania dostępu do kontrolera uwierzytelniany hello jako użytkownik anonimowy:<br/>
Wybierz hello Połącz hello poza toosign użytkownika i hello pełną proces wylogowywania.<br/>
Teraz w przeglądarce, wpisz http://localhost: {port} / uwierzytelniony tooaccess kontrolerze, który jest chroniony za pomocą hello `[Authorize]` atrybutu

#### <a name="expected-results"></a>Oczekiwanych rezultatów
Powinien zostać wyświetlony monit hello żądający tooauthenticate toosee hello widoku.

## <a name="additional-information"></a>Dodatkowe informacje

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a>Ochrona całej witryny sieci web
tooprotect całej witryny sieci web, Dodaj hello `AuthorizeAttribute` za`GlobalFilters` w `Global.asax` `Application_Start` metody:

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

> [!NOTE]
> **Jak użytkownicy toorestrict z toosign tylko jednej z organizacji w aplikacji tooyour**

> Domyślnie konta osobiste (takie jak outlook.com, live.com i inne), a także kont służbowych z firmy lub organizacji, która ma być zintegrowane z usługą Azure Active Directory można logowania tooyour aplikacji. 

> Twojej aplikacji tooaccept logowania z usługi Azure Active Directory tylko jednej z organizacji, Zamień hello `Tenant` parametru w *web.config* z `Common` toohello nazwa dzierżawy organizacji hello — przykład *contoso.onmicrosoft.com*. Po wykonaniu tej zmiany hello `ValidateIssuer` argumentu w Twojej *klasy początkowej OWIN* zbyt`true`.

> Ustaw tooallow użytkownikom tylko listę określonym organizacjom `ValidateIssuer` hello tootrue i użyj `ValidIssuers` toospecify parametru wykaz organizacji.

> Inną opcją jest wystawców hello toovalidate za pomocą parametru IssuerValidator tooimplement metody niestandardowej. Aby uzyskać więcej informacji na temat `TokenValidationParameters`, można znaleźć pod adresem [to](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "artykuł w witrynie MSDN TokenValidationParameters") artykuł w witrynie MSDN.

