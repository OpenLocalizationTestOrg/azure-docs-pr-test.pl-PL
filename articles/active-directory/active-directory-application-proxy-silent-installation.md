---
title: "aaaSilent zainstalować łącznik serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Opisano sposób tooperform instalacji nienadzorowanej łącznika serwera Proxy aplikacji w usłudze Azure AD tooprovide bezpieczny dostęp zdalny tooyour lokalnej aplikacji."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a>Instalacji dyskretnej hello łącznika serwera Proxy aplikacji w usłudze Azure AD
Ma toobe toosend stanie instalacji skryptu toomultiple systemów Windows Server lub tooWindows serwerów, które nie mają włączone interfejsu użytkownika. Ten temat ułatwia tworzenie skryptu programu Windows PowerShell, która umożliwia instalacji nienadzorowanej i rejestracji dla platformy Azure łącznika serwera Proxy aplikacji usługi AD.

Ta funkcja jest przydatna, gdy chcesz:

* Zainstaluj łącznik hello na maszynach z warstwą nie interfejsu użytkownika lub nie RDP toohello maszyny.
* Zainstaluj i zarejestruj wiele łączników na raz.
* Integracja hello instalacja łącznika i rejestracji w ramach innej procedury.
* Utworzyć obraz serwera standardowe zawierającą hello łącznika bits, ale nie jest zarejestrowany.

Serwer Proxy aplikacji działa przez zainstalowanie cienki usługi systemu Windows Server o nazwie hello łącznika w sieci. Toowork łącznika serwera Proxy aplikacji hello ma on toobe zarejestrowana w usłudze Azure AD w katalogu za pomocą administratora globalnego i hasło. Zwykle te informacje są wprowadzane podczas instalacji łącznika w oknie dialogowym wyskakujących. Jednak można użyć programu Windows PowerShell toocreate tooenter obiekt poświadczeń informacji rejestracyjnych. Lub można utworzyć własny token i używać go tooenter informacji rejestracyjnych.

## <a name="install-hello-connector"></a>Instalowanie łącznika hello
Zainstaluj msi łącznika hello bez rejestrowania hello łącznika w następujący sposób:

1. Otwórz wiersz polecenia.
2. Uruchom następujące polecenie, w którym hello/q oznacza instalację cichą hello — Witaj instalacji nie monit hello tooaccept umowę licencyjną użytkownika oprogramowania.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a>Zarejestruj hello łącznika usługi Azure AD
Istnieją dwie metody mogą używać łącznika hello tooregister:

* Zarejestruj łącznik hello za pomocą obiektu poświadczenia programu Windows PowerShell
* Zarejestruj łącznika hello za pomocą tokenu utworzony w trybie offline

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a>Zarejestruj łącznik hello za pomocą obiektu poświadczenia programu Windows PowerShell
1. Utwórz obiekt poświadczeń programu Windows PowerShell hello przez uruchomienie tego polecenia. Zastąp  *\<username\>*  i  *\<hasło\>*  hello nazwy użytkownika i hasło dla katalogu:
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Przejdź za**łącznika serwera Proxy aplikacji C:\Program Files\Microsoft AAD** i uruchom skrypt hello przy użyciu programu PowerShell hello poświadczenia obiekt został utworzony. Zastąp *$cred* o nazwie hello hello środowiska PowerShell obiektu utworzony poświadczeń:
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a>Zarejestruj łącznika hello za pomocą tokenu utworzony w trybie offline
1. Utwórz token w trybie offline za pomocą hello klasy kontekst AuthenticationContext przy użyciu wartości hello we fragmencie kodu hello:

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. Po uzyskaniu tokenu hello Utwórz SecureString, za pomocą tokenu hello:

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Witaj uruchom następujące polecenia programu Windows PowerShell, zastępując \<identyfikator GUID dzierżawy\> za pomocą Identyfikatora katalogu:

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Następne kroki 
* [Publikowanie aplikacji przy użyciu własnej nazwy domeny](active-directory-application-proxy-custom-domains.md)
* [Włączanie logowania jednokrotnego](active-directory-application-proxy-sso-using-kcd.md)
* [Rozwiązywanie problemów, które masz problem z serwerem Proxy aplikacji](active-directory-application-proxy-troubleshoot.md)


