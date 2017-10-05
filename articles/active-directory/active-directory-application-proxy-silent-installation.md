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
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="9a43a-103">Instalacji dyskretnej łącznika serwera Proxy aplikacji Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a43a-103">Silently install the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="9a43a-104">Chcesz mieć możliwość wysyłania skrypt instalacji na wielu serwerach z systemem Windows lub serwerów systemu Windows, które nie mają włączone interfejsu użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9a43a-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="9a43a-105">Ten temat ułatwia tworzenie skryptu programu Windows PowerShell, która umożliwia instalacji nienadzorowanej i rejestracji dla platformy Azure łącznika serwera Proxy aplikacji usługi AD.</span><span class="sxs-lookup"><span data-stu-id="9a43a-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="9a43a-106">Ta funkcja jest przydatna, gdy chcesz:</span><span class="sxs-lookup"><span data-stu-id="9a43a-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="9a43a-107">Zainstaluj łącznik na maszynach z warstwą nie interfejsu użytkownika lub nie RDP na maszynie.</span><span class="sxs-lookup"><span data-stu-id="9a43a-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span></span>
* <span data-ttu-id="9a43a-108">Zainstaluj i zarejestruj wiele łączników na raz.</span><span class="sxs-lookup"><span data-stu-id="9a43a-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="9a43a-109">Integracja instalacja łącznika i rejestracji w ramach innej procedury.</span><span class="sxs-lookup"><span data-stu-id="9a43a-109">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="9a43a-110">Utworzyć obraz serwera standardowe zawierającą bitów łącznika, ale nie jest zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="9a43a-110">Create a standard server image that contains the connector bits but is not registered.</span></span>

<span data-ttu-id="9a43a-111">Serwer Proxy aplikacji działa przez zainstalowanie cienki usługi systemu Windows Server o nazwie łącznika w sieci.</span><span class="sxs-lookup"><span data-stu-id="9a43a-111">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span></span> <span data-ttu-id="9a43a-112">Dla łącznika serwera Proxy aplikacji do pracy go musi być zarejestrowany w usłudze Azure AD w katalogu za pomocą administratora globalnego i hasło.</span><span class="sxs-lookup"><span data-stu-id="9a43a-112">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="9a43a-113">Zwykle te informacje są wprowadzane podczas instalacji łącznika w oknie dialogowym wyskakujących.</span><span class="sxs-lookup"><span data-stu-id="9a43a-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="9a43a-114">Jednak można użyć programu Windows PowerShell do tworzenia obiektu poświadczenia, aby wprowadzić informacje o rejestracji.</span><span class="sxs-lookup"><span data-stu-id="9a43a-114">However, you can use Windows PowerShell to create a credential object to enter your registration information.</span></span> <span data-ttu-id="9a43a-115">Lub można utworzyć własny token i użyj go, aby wprowadzić swoje informacje rejestracyjne.</span><span class="sxs-lookup"><span data-stu-id="9a43a-115">Or you can create your own token and use it to enter your registration information.</span></span>

## <a name="install-the-connector"></a><span data-ttu-id="9a43a-116">Instalowanie łącznika</span><span class="sxs-lookup"><span data-stu-id="9a43a-116">Install the connector</span></span>
<span data-ttu-id="9a43a-117">Zainstaluj łącznik msi bez rejestrowania łącznika w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9a43a-117">Install the Connector MSIs without registering the Connector as follows:</span></span>

1. <span data-ttu-id="9a43a-118">Otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="9a43a-118">Open a command prompt.</span></span>
2. <span data-ttu-id="9a43a-119">Uruchom następujące polecenie, w którym instalację cichą oznacza/q - instalacji nie Monituj, należy zaakceptować umowę licencyjną użytkownika oprogramowania.</span><span class="sxs-lookup"><span data-stu-id="9a43a-119">Run the following command in which the /q means quiet installation - the installation doesn't prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a><span data-ttu-id="9a43a-120">Zarejestrowanie łącznika z usługą Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a43a-120">Register the connector with Azure AD</span></span>
<span data-ttu-id="9a43a-121">Istnieją dwie metody, który umożliwia zarejestrowanie łącznika:</span><span class="sxs-lookup"><span data-stu-id="9a43a-121">There are two methods you can use to register the connector:</span></span>

* <span data-ttu-id="9a43a-122">Zarejestrowanie łącznika przy użyciu obiektu poświadczeń programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a43a-122">Register the connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="9a43a-123">Zarejestrowanie łącznika za pomocą tokenu utworzony w trybie offline</span><span class="sxs-lookup"><span data-stu-id="9a43a-123">Register the connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="9a43a-124">Zarejestrowanie łącznika przy użyciu obiektu poświadczeń programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a43a-124">Register the connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="9a43a-125">Utwórz obiekt poświadczeń programu Windows PowerShell, uruchamiając poniższe polecenie.</span><span class="sxs-lookup"><span data-stu-id="9a43a-125">Create the Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="9a43a-126">Zastąp  *\<username\>*  i  *\<hasło\>*  przy użyciu nazwy użytkownika i hasła dla katalogu:</span><span class="sxs-lookup"><span data-stu-id="9a43a-126">Replace *\<username\>* and *\<password\>* with the username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="9a43a-127">Przejdź do **łącznika serwera Proxy aplikacji C:\Program Files\Microsoft AAD** i uruchom skrypt przy użyciu programu PowerShell poświadczenia obiekt został utworzony.</span><span class="sxs-lookup"><span data-stu-id="9a43a-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created.</span></span> <span data-ttu-id="9a43a-128">Zastąp *$cred* o nazwie programu PowerShell utworzony obiekt poświadczeń:</span><span class="sxs-lookup"><span data-stu-id="9a43a-128">Replace *$cred* with the name of the PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="9a43a-129">Zarejestrowanie łącznika za pomocą tokenu utworzony w trybie offline</span><span class="sxs-lookup"><span data-stu-id="9a43a-129">Register the connector using a token created offline</span></span>
1. <span data-ttu-id="9a43a-130">Utwórz token w trybie offline za pomocą klasy kontekst AuthenticationContext przy użyciu wartości we fragmencie kodu:</span><span class="sxs-lookup"><span data-stu-id="9a43a-130">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span></span>

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


2. <span data-ttu-id="9a43a-131">Po utworzeniu token, Utwórz SecureString, przy użyciu tokenu:</span><span class="sxs-lookup"><span data-stu-id="9a43a-131">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="9a43a-132">Uruchom następujące polecenie programu Windows PowerShell, zastępując \<identyfikator GUID dzierżawy\> za pomocą Identyfikatora katalogu:</span><span class="sxs-lookup"><span data-stu-id="9a43a-132">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="9a43a-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9a43a-133">Next steps</span></span> 
* [<span data-ttu-id="9a43a-134">Publikowanie aplikacji przy użyciu własnej nazwy domeny</span><span class="sxs-lookup"><span data-stu-id="9a43a-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="9a43a-135">Włączanie logowania jednokrotnego</span><span class="sxs-lookup"><span data-stu-id="9a43a-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="9a43a-136">Rozwiązywanie problemów, które masz problem z serwerem Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="9a43a-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


