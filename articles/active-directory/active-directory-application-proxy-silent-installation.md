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
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="1c347-103">Instalacji dyskretnej hello łącznika serwera Proxy aplikacji w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c347-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="1c347-104">Ma toobe toosend stanie instalacji skryptu toomultiple systemów Windows Server lub tooWindows serwerów, które nie mają włączone interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1c347-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="1c347-105">Ten temat ułatwia tworzenie skryptu programu Windows PowerShell, która umożliwia instalacji nienadzorowanej i rejestracji dla platformy Azure łącznika serwera Proxy aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="1c347-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="1c347-106">Ta funkcja jest przydatna, gdy chcesz:</span><span class="sxs-lookup"><span data-stu-id="1c347-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="1c347-107">Zainstaluj łącznik hello na maszynach z warstwą nie interfejsu użytkownika lub nie RDP toohello maszyny.</span><span class="sxs-lookup"><span data-stu-id="1c347-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="1c347-108">Zainstaluj i zarejestruj wiele łączników na raz.</span><span class="sxs-lookup"><span data-stu-id="1c347-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="1c347-109">Integracja hello instalacja łącznika i rejestracji w ramach innej procedury.</span><span class="sxs-lookup"><span data-stu-id="1c347-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="1c347-110">Utworzyć obraz serwera standardowe zawierającą hello łącznika bits, ale nie jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="1c347-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="1c347-111">Serwer Proxy aplikacji działa przez zainstalowanie cienki usługi systemu Windows Server o nazwie hello łącznika w sieci.</span><span class="sxs-lookup"><span data-stu-id="1c347-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="1c347-112">Toowork łącznika serwera Proxy aplikacji hello ma on toobe zarejestrowana w usłudze Azure AD w katalogu za pomocą administratora globalnego i hasło.</span><span class="sxs-lookup"><span data-stu-id="1c347-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="1c347-113">Zwykle te informacje są wprowadzane podczas instalacji łącznika w oknie dialogowym wyskakujących.</span><span class="sxs-lookup"><span data-stu-id="1c347-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="1c347-114">Jednak można użyć programu Windows PowerShell toocreate tooenter obiekt poświadczeń informacji rejestracyjnych.</span><span class="sxs-lookup"><span data-stu-id="1c347-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="1c347-115">Lub można utworzyć własny token i używać go tooenter informacji rejestracyjnych.</span><span class="sxs-lookup"><span data-stu-id="1c347-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="1c347-116">Instalowanie łącznika hello</span><span class="sxs-lookup"><span data-stu-id="1c347-116">Install hello connector</span></span>
<span data-ttu-id="1c347-117">Zainstaluj msi łącznika hello bez rejestrowania hello łącznika w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="1c347-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="1c347-118">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="1c347-118">Open a command prompt.</span></span>
2. <span data-ttu-id="1c347-119">Uruchom następujące polecenie, w którym hello/q oznacza instalację cichą hello — Witaj instalacji nie monit hello tooaccept umowę licencyjną użytkownika oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="1c347-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="1c347-120">Zarejestruj hello łącznika usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1c347-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="1c347-121">Istnieją dwie metody mogą używać łącznika hello tooregister:</span><span class="sxs-lookup"><span data-stu-id="1c347-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="1c347-122">Zarejestruj łącznik hello za pomocą obiektu poświadczenia programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c347-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="1c347-123">Zarejestruj łącznika hello za pomocą tokenu utworzony w trybie offline</span><span class="sxs-lookup"><span data-stu-id="1c347-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="1c347-124">Zarejestruj łącznik hello za pomocą obiektu poświadczenia programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="1c347-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="1c347-125">Utwórz obiekt poświadczeń programu Windows PowerShell hello przez uruchomienie tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="1c347-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="1c347-126">Zastąp  *\<username\>*  i  *\<hasło\>*  hello nazwy użytkownika i hasło dla katalogu:</span><span class="sxs-lookup"><span data-stu-id="1c347-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="1c347-127">Przejdź za**łącznika serwera Proxy aplikacji C:\Program Files\Microsoft AAD** i uruchom skrypt hello przy użyciu programu PowerShell hello poświadczenia obiekt został utworzony.</span><span class="sxs-lookup"><span data-stu-id="1c347-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="1c347-128">Zastąp *$cred* o nazwie hello hello środowiska PowerShell obiektu utworzony poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="1c347-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="1c347-129">Zarejestruj łącznika hello za pomocą tokenu utworzony w trybie offline</span><span class="sxs-lookup"><span data-stu-id="1c347-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="1c347-130">Utwórz token w trybie offline za pomocą hello klasy kontekst AuthenticationContext przy użyciu wartości hello we fragmencie kodu hello:</span><span class="sxs-lookup"><span data-stu-id="1c347-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

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


2. <span data-ttu-id="1c347-131">Po uzyskaniu tokenu hello Utwórz SecureString, za pomocą tokenu hello:</span><span class="sxs-lookup"><span data-stu-id="1c347-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="1c347-132">Witaj uruchom następujące polecenia programu Windows PowerShell, zastępując \<identyfikator GUID dzierżawy\> za pomocą Identyfikatora katalogu:</span><span class="sxs-lookup"><span data-stu-id="1c347-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="1c347-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c347-133">Next steps</span></span> 
* [<span data-ttu-id="1c347-134">Publikowanie aplikacji przy użyciu własnej nazwy domeny</span><span class="sxs-lookup"><span data-stu-id="1c347-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="1c347-135">Włączanie logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="1c347-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="1c347-136">Rozwiązywanie problemów, które masz problem z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="1c347-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


