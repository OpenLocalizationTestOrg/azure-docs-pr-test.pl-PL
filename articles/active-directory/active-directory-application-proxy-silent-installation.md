---
title: "Instalację łącznika serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Uwzględniono również sposób przeprowadzenia instalacji nienadzorowanej programu Azure łącznika serwera Proxy aplikacji usługi AD, aby zapewnić bezpieczny zdalny dostęp do aplikacji lokalnych."
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
ms.openlocfilehash: 9e28c89d8f64f0ae3d4150017ca544e606075c45
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a>Instalacji dyskretnej łącznika serwera Proxy aplikacji Azure AD
Chcesz mieć możliwość wysyłania skrypt instalacji na wielu serwerach z systemem Windows lub serwerów systemu Windows, które nie mają włączone interfejsu użytkownika. Ten temat ułatwia tworzenie skryptu programu Windows PowerShell, która umożliwia instalacji nienadzorowanej i rejestracji dla platformy Azure łącznika serwera Proxy aplikacji usługi AD.

Ta funkcja jest przydatna, gdy chcesz:

* Zainstaluj łącznik na maszynach z warstwą nie interfejsu użytkownika lub nie RDP na maszynie.
* Zainstaluj i zarejestruj wiele łączników na raz.
* Integracja instalacja łącznika i rejestracji w ramach innej procedury.
* Utworzyć obraz serwera standardowe zawierającą bitów łącznika, ale nie jest zarejestrowany.

Serwer Proxy aplikacji działa przez zainstalowanie cienki usługi systemu Windows Server o nazwie łącznika w sieci. Dla łącznika serwera Proxy aplikacji do pracy go musi być zarejestrowany w usłudze Azure AD w katalogu za pomocą administratora globalnego i hasło. Zwykle te informacje są wprowadzane podczas instalacji łącznika w oknie dialogowym wyskakujących. Jednak można użyć programu Windows PowerShell do tworzenia obiektu poświadczenia, aby wprowadzić informacje o rejestracji. Lub można utworzyć własny token i użyj go, aby wprowadzić swoje informacje rejestracyjne.

## <a name="install-the-connector"></a>Instalowanie łącznika
Zainstaluj łącznik msi bez rejestrowania łącznika w następujący sposób:

1. Otwórz wiersz polecenia.
2. Uruchom następujące polecenie, w którym instalację cichą oznacza/q - instalacji nie Monituj, należy zaakceptować umowę licencyjną użytkownika oprogramowania.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a>Zarejestrowanie łącznika z usługą Azure AD
Istnieją dwie metody, który umożliwia zarejestrowanie łącznika:

* Zarejestrowanie łącznika przy użyciu obiektu poświadczeń programu Windows PowerShell
* Zarejestrowanie łącznika za pomocą tokenu utworzony w trybie offline

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a>Zarejestrowanie łącznika przy użyciu obiektu poświadczeń programu Windows PowerShell
1. Utwórz obiekt poświadczeń programu Windows PowerShell, uruchamiając poniższe polecenie. Zastąp  *\<username\>*  i  *\<hasło\>*  przy użyciu nazwy użytkownika i hasła dla katalogu:
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Przejdź do **łącznika serwera Proxy aplikacji C:\Program Files\Microsoft AAD** i uruchom skrypt przy użyciu programu PowerShell poświadczenia obiekt został utworzony. Zastąp *$cred* o nazwie programu PowerShell utworzony obiekt poświadczeń:
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a>Zarejestrowanie łącznika za pomocą tokenu utworzony w trybie offline
1. Utwórz token w trybie offline za pomocą klasy kontekst AuthenticationContext przy użyciu wartości we fragmencie kodu:

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// The application ID of the connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// The reply address of the connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// The AppIdUri of the registration service in AAD
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


2. Po utworzeniu token, Utwórz SecureString, przy użyciu tokenu:

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Uruchom następujące polecenie programu Windows PowerShell, zastępując \<identyfikator GUID dzierżawy\> za pomocą Identyfikatora katalogu:

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Następne kroki 
* [Publikowanie aplikacji przy użyciu własnej nazwy domeny](active-directory-application-proxy-custom-domains.md)
* [Włączanie logowania jednokrotnego](active-directory-application-proxy-sso-using-kcd.md)
* [Rozwiązywanie problemów, które masz problem z serwerem Proxy aplikacji](active-directory-application-proxy-troubleshoot.md)


