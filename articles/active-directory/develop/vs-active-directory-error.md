---
title: "błędy toodiagnose aaaHow hello Kreator połączenia usługi Azure Active Directory"
description: "Kreator połączenia usługi active directory Hello wykryto typ uwierzytelniania niezgodne"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: f71c5b41457c0c8db05042e8d5f723e58ad11844
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="diagnosing-errors-with-hello-azure-active-directory-connection-wizard"></a>Diagnozowanie błędów przy użyciu hello Kreator połączenia usługi Azure Active Directory
Podczas wykrywania poprzedni kod uwierzytelniania, Kreator hello wykrył typ uwierzytelniania niezgodne.   

## <a name="what-is-being-checked"></a>Co to jest sprawdzany?
**Uwaga:** toocorrectly wykryć poprzedni kod uwierzytelniania w projekcie, hello projektu muszą zostać skompilowane.  Jeśli wystąpił błąd i nie masz poprzedni kod uwierzytelniania w projekcie, skompiluj ponownie i spróbuj ponownie.

### <a name="project-types"></a>Typy projektów
Witaj, Kreator sprawdza, czy hello typ projektu, który projektujesz tak go wstrzyknąć hello logika uwierzytelniania prawo do projektu hello.  W przypadku dowolnego kontrolera, która jest pochodną `ApiController` w projekcie hello projektu hello jest uznawany za WebAPI projektu.  Jeśli występują tylko te kontrolery, które pochodzą z `MVC.Controller` w projekcie hello projektu hello jest uznawany za projekt platformy MVC.  Cokolwiek innego nie jest obsługiwana przez kreatora hello.

### <a name="compatible-authentication-code"></a>Kod uwierzytelniania zgodne
Kreator Hello również sprawdza, czy ustawienia uwierzytelniania, które zostały wcześniej skonfigurowane przy użyciu Kreatora hello lub są zgodne z hello kreatora.  Jeśli wszystkie ustawienia są obecne, jest on uznawany za przypadek wielobieżnej otworzy się Kreator hello hello ustawienia i.  Jeśli tylko niektóre ustawienia hello są obecne, jest uznawane za przypadek błędu.

W projekcie MVC hello Kreator sprawdza jakichkolwiek hello następujące ustawienia, które w wyniku poprzedniego użycia kreatora hello:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

Ponadto Kreator hello sprawdza dla żadnego z następujących ustawień w projekcie interfejsu API sieci Web, wynikające z poprzedniego użycia kreatora hello hello:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Kod uwierzytelniania niezgodne
Ponadto Kreator hello prób toodetect wersji kodu uwierzytelniania, które zostały skonfigurowane z poprzednich wersji programu Visual Studio. Jeśli wystąpił ten błąd, oznacza to, że projekt zawiera typ uwierzytelniania niezgodne. Kreator Hello wykrywa hello następujące typy uwierzytelniania z poprzednich wersji programu Visual Studio:

* Uwierzytelnianie systemu Windows 
* Indywidualne konta użytkowników 
* Konta organizacyjne 

toodetect uwierzytelniania systemu Windows w projekcie programu MVC, Kreator hello szuka hello `authentication` element na podstawie Twojej **web.config** pliku.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

toodetect uwierzytelniania systemu Windows w projekcie interfejsu API sieci Web, Kreator hello szuka hello `IISExpressWindowsAuthentication` element z projektu **.csproj** pliku:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

toodetect uwierzytelniania indywidualnych kont użytkowników, Kreator hello wygląda hello elementu pakietu z sieci **Packages.config** pliku.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

toodetect stare formy uwierzytelniania konto organizacyjne, Kreator hello szuka hello następującego elementu z **web.config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

Typ uwierzytelniania hello toochange, Usuń typ uwierzytelniania niezgodne hello i uruchom ponownie kreatora hello.

Aby uzyskać więcej informacji, zobacz [scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Następne kroki
- [Scenariusze uwierzytelniania dla usługi Azure AD](active-directory-authentication-scenarios.md)