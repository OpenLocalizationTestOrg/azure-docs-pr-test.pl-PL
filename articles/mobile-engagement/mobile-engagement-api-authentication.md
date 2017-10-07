---
title: "aaaAuthenticate z interfejsów API REST usługi Engagement Mobile"
description: "Opisuje sposób tooauthenticate z interfejsów API REST usługi Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: da82cb36-957a-4e19-a805-b44733cf6597
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/05/2016
ms.author: wesmc;ricksal
ms.openlocfilehash: 9b54aa5ec3da4bcf55ffe5b7e8d1759095d0c486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis"></a>Uwierzytelniania za pomocą interfejsów API REST usługi Mobile Engagement
## <a name="overview"></a>Omówienie
W tym dokumencie opisano, jak tooget prawidłowy Oauth AAD token tooauthenticate z hello interfejsów API REST usługi Engagement Mobile. 

Zakłada się, że masz ważnej subskrypcji platformy Azure i utworzono aplikację usługi Mobile Engagement, przy użyciu jednej z naszych [samouczki Developer](mobile-engagement-windows-store-dotnet-get-started.md).

## <a name="authentication"></a>Authentication
Microsoft Azure Active Directory na podstawie tokenu jest używany do uwierzytelniania OAuth. 

Zamówienie tooauthentication interfejsu API nagłówek uwierzytelnienia muszą zostać dodane tooevery żądania, które jest hello następującej postaci:

    Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGmJlNmV2ZWJPamg2TTNXR1E...

> [!NOTE]
> Azure Active Directory tokeny wygaśnie w ciągu godziny.
> 
> 

Istnieje kilka sposobów tooget tokenu. Ponieważ powitalne interfejsy API są zwykle nazywane z usługi w chmurze ma toouse klucz interfejsu API. Klucz interfejsu API w terminologii Azure jest nazywany hasło główną usługi. Witaj Poniższa procedura opisuje jednokierunkowej toosetting go ręcznie w górę.

### <a name="one-time-setup-using-script"></a>Jednorazowej konfiguracji (przy użyciu skryptu)
Należy stosować hello zestaw instrukcji poniżej tooperform hello Instalatora za pomocą skryptu programu PowerShell, który przyjmuje hello minimalny czas instalacji, ale używa hello najbardziej dopuszczalnej wartości domyślnych. Opcjonalnie można również wykonać instrukcje hello hello [instalacji ręcznej](mobile-engagement-api-authentication-manual.md) Aby to zrobić z hello bezpośrednio portalu Azure i są bardziej precyzyjną konfiguracji. 

1. Pobierz najnowszą wersję programu Azure PowerShell z hello [tutaj](http://aka.ms/webpi-azps). Aby uzyskać więcej informacji na powitania instrukcje pobierania widać to [łącze](/powershell/azure/overview).  
2. Po zainstalowaniu programu Azure PowerShell, użyj następujących hello polecenia tooensure, że masz hello **modułu Azure** zainstalowane:
   
    a. Upewnij się, że hello modułu Azure PowerShell jest dostępny w hello listę dostępnych modułów. 
   
        Get-Module –ListAvailable 
   
    ![Dostępne moduły Azure][1]
   
    b. Jeśli nie znajdziesz modułu Azure PowerShell hello hello powyżej listy należy toorun hello poniżej:
   
        Import-Module Azure 
3. Toohello logowania usługi Azure Resource Manager z programu PowerShell, uruchamiając hello następujące polecenia i podając nazwę użytkownika i hasło dla konta platformy Azure: 
   
        Login-AzureRmAccount
4. Jeśli masz wiele subskrypcji należy uruchomić następujące hello:
   
    a. Pobierz listę subskrypcji i hello kopii subskrypcji o identyfikatorze subskrypcji hello, który ma toouse. Upewnij się, że ta subskrypcja jest hello takie same, który ma hello Mobile Engagement aplikacji, która ma toointeract przy użyciu hello interfejsów API. 
   
        Get-AzureRmSubscription
   
    b. Witaj uruchom następujące polecenie udostępnienie hello SubscriptionId tooconfigure hello subskrypcji toobe używane.
   
        Select-AzureRmSubscription –SubscriptionId <subscriptionId>
5. Skopiuj tekst hello hello [AzureRmServicePrincipalOwner.ps1 nowy](https://raw.githubusercontent.com/matt-gibbs/azbits/master/src/New-AzureRmServicePrincipalOwner.ps1) skryptu tooyour komputera lokalnego i zapisz go jako polecenia cmdlet programu PowerShell (np. `APIAuth.ps1`) i wykonaj go `.\APIAuth.ps1`. 
6. Witaj skrypt wyświetli monit tooprovide jako dane wejściowe dla **principalName**. Podaj odpowiednią nazwę mają toouse toocreate aplikacji usługi Active Directory (np. APIAuth). 
7. Po ukończeniu działania skryptu hello zostaną wyświetlone następujące cztery wartości, które będą potrzebne hello tooauthenticate programowo z usługą Active Directory, dlatego upewnij się, że toocopy je. 
   
    **TenantId**, **SubscriptionId**, **ApplicationId**, i **klucz tajny**.
   
    Użyje TenantId jako `{TENANT_ID}`, identyfikator aplikacji jako `{CLIENT_ID}` i tajne jako `{CLIENT_SECRET}`.
   
   > [!NOTE]
   > Domyślne zasady zabezpieczeń blokują uruchomionych skryptów PowerShell. Jeśli tak, należy skonfigurować tymczasowo z zasad wykonywania tooallow wykonywanie skryptu za pomocą następującego polecenia hello:
   > 
   > Set-ExecutionPolicy RemoteSigned
   > 
   > 
8. Oto jak będzie wyglądać hello zestaw poleceń cmdlet środowiska PS. 
   
    ![][3]
9. Sprawdź w portalu zarządzania Azure hello nową aplikację usługi AD utworzenia o nazwie hello zostanie podane nazywany toohello skryptu **principalName** w obszarze **Pokaż aplikacje Moja firma jest właścicielem**.
   
    ![][4]

#### <a name="steps-tooget-a-valid-token"></a>Kroki tooget prawidłowy token
1. Wywołanie interfejsu API hello z hello następujące parametry i upewnij się, że tooreplace hello dzierżawy\_identyfikator, klient\_identyfikator i klienta\_klucz TAJNY:
   
   * **Adres URL żądania** jako *https://login.microsoftonline.com/ {dzierżawy\_identyfikator} / oauth2/token.*
   * **Nagłówek HTTP Content-Type** jako *application/x--www-form-urlencoded*
   * **Treść żądania HTTP** jako *przyznać\_typu = klient\_poświadczenia & client_id = {klienta\_identyfikator} & client_secret = {klienta\_klucz TAJNY} & resource=https%3A%2F%2Fmanagement.core.windows.net%2F*
     
     Witaj poniżej przedstawiono przykładowe żądanie:
     
       POST / {TENANT_ID} / oauth2/token hostów protokołu HTTP/1.1: login.microsoftonline.com Content-Type: application/x--www-form-urlencoded typ grant_type = client_credentials & client_id = {CLIENT_ID} & client_secret = {CLIENT_SECRET} & staw nazw = https % 3A % 2f%2Fmanagement.Core.Windows.NET%2f
     
     Oto przykład odpowiedzi:
     
       HTTP/1.1 200 OK Content-Type: application/json; charset = utf-8 Content-Length: 1234
     
       {"token_type": "Bearer", "expires_in": "3599", "expires_on": "1445395811", "not_before": "144 5391911 zasobu","": "https://management.core.windows.net/", "' access_token '": {' access_token '}}
     
     W tym przykładzie uwzględnione hello parametrów POST, podczas kodowania adresu URL `resource` wartość jest rzeczywiście `https://management.core.windows.net/`. Należy zachować ostrożność, kodowania adresu URL tooalso `{CLIENT_SECRET}` jako może zawierać znaków specjalnych.
     
     > [!NOTE]
     > Do testowania, można użyć narzędzia klienta HTTP, takiego jak [Fiddler](http://www.telerik.com/fiddler) lub [rozszerzenia Chrome Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop) 
     > 
     > 
2. W każdym wywołaniu interfejsu API zawierają teraz nagłówek żądania autoryzacji hello:
   
        Authorization: Bearer {ACCESS_TOKEN}
   
    Jeśli zostanie wyświetlony kod stanu 401 zwrócone, sprawdź treść odpowiedzi hello, jego może poinformować użytkownika hello token utracił ważność. W takim przypadku należy uzyskać nowy token.

## <a name="using-hello-apis"></a>Przy użyciu hello interfejsów API
Użytkownik ma prawidłowy token, użytkownik jest gotowy toomake wywołania hello interfejsu API.

1. W poszczególnych żądań interfejsu API konieczne będzie toopass prawidłowych, niewygasłych tokenem, który został uzyskany w poprzedniej sekcji hello.
2. Należy tooplug w niektórych parametrów do żądania hello identyfikator URI, który identyfikuje aplikację. Identyfikator URI żądania Hello wygląda hello
   
        https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/
        providers/Microsoft.MobileEngagement/appcollections/{app-collection}/apps/{app-resource-name}/
   
    Parametry hello tooget, kliknij nazwę aplikacji i kliknij pozycję pulpit nawigacyjny i zostanie wyświetlona strona, takie jak następujące hello ze wszystkimi hello 3 parametry.
   
   * **1** `{subscription-id}`
   * **2** `{app-collection}`
   * **3** `{app-resource-name}`
   * **4** nazwy grupy zasobów your będzie toobe **MobileEngagement** chyba że zostaną utworzone nowe. 
     
     ![Parametry identyfikatora URI interfejsu API usługi Engagement Mobile][2]

> [!NOTE]
> <br/>
> 
> 1. Ignoruj hello adres głównego interfejsu API, jak to uzyskać hello poprzedniej interfejsów API.<br/>
> 2. Jeśli utworzono aplikację hello przy użyciu klasycznego portalu Azure należy nazwy zasobu usługi Application hello toouse, która jest inna niż nazwa aplikacji hello samej siebie. Jeśli utworzono aplikację hello w hello portalu Azure należy używać hello Nazwa aplikacji (brak rozróżnienia między nazwa zasobów aplikacji i nazwy aplikacji dla aplikacji utworzonych w hello nowego portalu).  
> 
> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication/azure-module.png
[2]: ./media/mobile-engagement-api-authentication/mobile-engagement-api-uri-params.png
[3]: ./media/mobile-engagement-api-authentication/ps-cmdlets.png
[4]: ./media/mobile-engagement-api-authentication/ad-app-creation.png



