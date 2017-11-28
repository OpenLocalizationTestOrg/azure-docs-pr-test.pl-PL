---
title: "Instalowanie aaaProblem hello łącznika Agent serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot problemów może hello po zainstalowaniu łącznika Agent serwera Proxy aplikacji"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 07ac366a429083af0c9b87aa9df9cf3876132b90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-installing-hello-application-proxy-agent-connector"></a><span data-ttu-id="4b28b-103">Problem podczas instalowania hello łącznika Agent serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4b28b-103">Problem installing hello Application Proxy Agent Connector</span></span>

<span data-ttu-id="4b28b-104">Łącznik serwera Proxy aplikacji usługi Microsoft AAD jest składnik domeny wewnętrznej, który używa połączenia wychodzące tooestablish hello łączności z domeny wewnętrznej toohello hello chmury dostępnego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="4b28b-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections tooestablish hello connectivity from hello cloud available endpoint toohello internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="4b28b-105">Ogólne obszarów problemów z instalacją łącznika</span><span class="sxs-lookup"><span data-stu-id="4b28b-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="4b28b-106">W przypadku niepowodzenia instalacji hello łącznika hello głównego przyczyną jest zazwyczaj jedną z następujących obszarów hello:</span><span class="sxs-lookup"><span data-stu-id="4b28b-106">When hello installation of a connector fails, hello root cause is usually one of hello following areas:</span></span>

1.  <span data-ttu-id="4b28b-107">**Łączność** — toocomplete udanej instalacji hello nowy łącznik potrzeb tooregister i ustanowienia zaufania przyszłych właściwości.</span><span class="sxs-lookup"><span data-stu-id="4b28b-107">**Connectivity** – toocomplete a successful installation, hello new connector needs tooregister and establish future trust properties.</span></span> <span data-ttu-id="4b28b-108">Jest to realizowane łącząc toohello usługi w chmurze serwera Proxy aplikacji usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="4b28b-108">This is done by connecting toohello AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="4b28b-109">**Tworzenie relacji zaufania** — nowy łącznik hello tworzy samopodpisany certyfikat i rejestruje toohello usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4b28b-109">**Trust Establishment** – hello new connector creates a self-signed cert and registers toohello cloud service.</span></span>

3.  <span data-ttu-id="4b28b-110">**Uwierzytelnianie Witaj, Administratorze** — podczas instalacji, hello użytkownik musi podać poświadczenia administratora toocomplete hello łącznika instalacji.</span><span class="sxs-lookup"><span data-stu-id="4b28b-110">**Authentication of hello admin** – during installation, hello user must provide admin credentials toocomplete hello Connector installation.</span></span>

## <a name="verify-connectivity-toohello-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="4b28b-111">Sprawdź łączność toohello serwera Proxy aplikacji w chmurze usługi i strony Login firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="4b28b-111">Verify connectivity toohello Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="4b28b-112">**Cel:** sprawdzić, czy maszyna łącznika hello łączy punktu końcowego rejestracji serwera Proxy aplikacji usługi AAD toohello, a także strony logowania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4b28b-112">**Objective:** Verify that hello connector machine can connect toohello AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="4b28b-113">Otwórz przeglądarkę i przejdź toohello, następujące strony sieci web: <https://aadap-portcheck.connectorporttest.msappproxy.net> , sprawdź tego tooCentral łączności hello USA i działają centrów danych wschodnie stany USA z portami 9090 i 9091.</span><span class="sxs-lookup"><span data-stu-id="4b28b-113">Open a browser and go toohello following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that hello connectivity tooCentral US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="4b28b-114">Jeśli żadnego z tych portów zakończy się niepowodzeniem (nie ma zielonym znacznikiem wyboru), sprawdź, że hello zapory lub serwera proxy wewnętrznej bazy danych ma \*. msappproxy.net z portami 9090 i 9091 poprawnie zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="4b28b-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that hello Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="4b28b-115">Otwórz w przeglądarce (osobnej karcie) i przejdź toohello następujące strony sieci web: <https://login.microsoftonline.com>, upewnij się, że możesz zalogować się toothat strony.</span><span class="sxs-lookup"><span data-stu-id="4b28b-115">Open a browser (separate tab) and go toohello following web page: <https://login.microsoftonline.com>, make sure that you can login toothat page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="4b28b-116">Sprawdź, czy składniki maszyny i wewnętrznej bazy danych obsługuje dla certyfikatu relacji zaufania serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="4b28b-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="4b28b-117">**Cel:** Sprawdź, czy hello łącznika maszyny, wewnętrznej bazy danych serwera proxy i zapory można obsługiwać certyfikatu hello utworzonego przez łącznik powitania dla przyszłych zaufania.</span><span class="sxs-lookup"><span data-stu-id="4b28b-117">**Objective:** Verify that hello connector machine, backend proxy and firewall can support hello certificate created by hello connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="4b28b-118">Łącznik Hello próbuje toocreate cert SHA512, która jest obsługiwana przez TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="4b28b-118">hello connector tries toocreate a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="4b28b-119">Jeśli maszyna hello lub hello zaporę wewnętrznej bazy danych i serwera proxy nie obsługuje TLS1.2 hello instalacja się nie powieść.</span><span class="sxs-lookup"><span data-stu-id="4b28b-119">If hello machine or hello backend firewall and proxy does not support TLS1.2, hello installation fail.</span></span>
>
>

<span data-ttu-id="4b28b-120">**problem hello tooresolve:**</span><span class="sxs-lookup"><span data-stu-id="4b28b-120">**tooresolve hello issue:**</span></span>

1.  <span data-ttu-id="4b28b-121">Sprawdź komputer hello obsługuje TLS1.2 — wersje wszystkich okien po 2012 R2 powinny obsługiwać protokół TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="4b28b-121">Verify hello machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="4b28b-122">W przypadku komputera łącznika z wersji 2012 R2 lub wcześniej, upewnij się, że hello następujące KB/s są zainstalowane na komputerze hello: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="4b28b-122">If your connector machine is from a version of 2012 R2 or prior, make sure that hello following KBs are installed on hello machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="4b28b-123">Skontaktuj się z administratorem sieci i tooverify że hello wewnętrznej bazy danych z serwera proxy i zapory nie blokują SHA512 dla ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="4b28b-123">Contact your network admin and ask tooverify that hello backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-tooinstall-hello-connector"></a><span data-ttu-id="4b28b-124">Sprawdź, czy administratora jest używane tooinstall hello łącznika</span><span class="sxs-lookup"><span data-stu-id="4b28b-124">Verify admin is used tooinstall hello connector</span></span>

<span data-ttu-id="4b28b-125">**Cel:** Sprawdź, że hello użytkownika, który próbuje tooinstall hello łącznika jest administratorem z prawidłowymi poświadczeniami.</span><span class="sxs-lookup"><span data-stu-id="4b28b-125">**Objective:** Verify that hello user who tries tooinstall hello connector is an administrator with correct credentials.</span></span> <span data-ttu-id="4b28b-126">Obecnie użytkownik hello musi być administratorem globalnym dla hello toosucceed instalacji.</span><span class="sxs-lookup"><span data-stu-id="4b28b-126">Currently, hello user must be a global administrator for hello installation toosucceed.</span></span>

<span data-ttu-id="4b28b-127">**tooverify hello poświadczenia są prawidłowe:**</span><span class="sxs-lookup"><span data-stu-id="4b28b-127">**tooverify hello credentials are correct:**</span></span>

<span data-ttu-id="4b28b-128">Połącz za<https://login.microsoftonline.com> i użyj hello tych samych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="4b28b-128">Connect too<https://login.microsoftonline.com> and use hello same credentials.</span></span> <span data-ttu-id="4b28b-129">Upewnij się, że hello użytkownik zaloguje się ponownie.</span><span class="sxs-lookup"><span data-stu-id="4b28b-129">Make sure hello login is successful.</span></span> <span data-ttu-id="4b28b-130">Sprawdź hello roli użytkownika, przechodząc zbyt**usługi Azure Active Directory**  - &gt; **użytkowników i grup**  - &gt; **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4b28b-130">You can check hello user role by going too**Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="4b28b-131">Wybierz konto użytkownika, następnie "Directory Role" w menu wynikowy hello.</span><span class="sxs-lookup"><span data-stu-id="4b28b-131">Select your user account, then “Directory Role” in hello resulting menu.</span></span> <span data-ttu-id="4b28b-132">Sprawdź, czy ta rola wybranego hello jest "Administrator globalny".</span><span class="sxs-lookup"><span data-stu-id="4b28b-132">Verify that hello selected role is “Global administrator”.</span></span> <span data-ttu-id="4b28b-133">Jeśli tooaccess żadnego hello strony wraz z tych kroków, nie jesteś administratorem globalnym.</span><span class="sxs-lookup"><span data-stu-id="4b28b-133">If you are unable tooaccess any of hello pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b28b-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4b28b-134">Next steps</span></span>
[<span data-ttu-id="4b28b-135">Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4b28b-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
