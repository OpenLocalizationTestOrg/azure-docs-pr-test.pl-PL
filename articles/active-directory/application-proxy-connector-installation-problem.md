---
title: "Problem podczas instalowania agenta łącznika serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Jak rozwiązywać problemy, które może sprostać podczas instalowania agenta łącznika serwera Proxy aplikacji"
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
ms.openlocfilehash: 91b3f6f3c8339647f568a509e9efd8e1fffb13dd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="problem-installing-the-application-proxy-agent-connector"></a><span data-ttu-id="f8533-103">Problem podczas instalowania agenta łącznika serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="f8533-103">Problem installing the Application Proxy Agent Connector</span></span>

<span data-ttu-id="f8533-104">Łącznik serwera Proxy aplikacji usługi Microsoft AAD jest składnik domeny wewnętrznej, który używa połączenia wychodzące do nawiązywania łączności z dostępnego punktu końcowego chmury do domeny wewnętrznej.</span><span class="sxs-lookup"><span data-stu-id="f8533-104">Microsoft AAD Application Proxy Connector is an internal domain component that uses outbound connections to establish the connectivity from the cloud available endpoint to the internal domain.</span></span>

## <a name="general-problem-areas-with-connector-installation"></a><span data-ttu-id="f8533-105">Ogólne obszarów problemów z instalacją łącznika</span><span class="sxs-lookup"><span data-stu-id="f8533-105">General Problem Areas with Connector installation</span></span>

<span data-ttu-id="f8533-106">Podczas instalacji łącznika nie powiedzie się, przyczynę zwykle jest jednym z następujących obszarów:</span><span class="sxs-lookup"><span data-stu-id="f8533-106">When the installation of a connector fails, the root cause is usually one of the following areas:</span></span>

1.  <span data-ttu-id="f8533-107">**Łączność** — w celu ukończenia instalacja przebiegła pomyślnie, nowych potrzeb łącznika do rejestracji i ustanowienia zaufania przyszłych właściwości.</span><span class="sxs-lookup"><span data-stu-id="f8533-107">**Connectivity** – to complete a successful installation, the new connector needs to register and establish future trust properties.</span></span> <span data-ttu-id="f8533-108">Jest to realizowane przez nawiązanie połączenia usługi w chmurze serwera Proxy aplikacji usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="f8533-108">This is done by connecting to the AAD Application Proxy cloud service.</span></span>

2.  <span data-ttu-id="f8533-109">**Tworzenie relacji zaufania** — nowy łącznik tworzy samopodpisany certyfikat i rejestruje do usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f8533-109">**Trust Establishment** – the new connector creates a self-signed cert and registers to the cloud service.</span></span>

3.  <span data-ttu-id="f8533-110">**Uwierzytelnianie Admin** — podczas instalacji, użytkownik musi podać poświadczenia administratora, aby ukończyć instalację łącznika.</span><span class="sxs-lookup"><span data-stu-id="f8533-110">**Authentication of the admin** – during installation, the user must provide admin credentials to complete the Connector installation.</span></span>

## <a name="verify-connectivity-to-the-cloud-application-proxy-service-and-microsoft-login-page"></a><span data-ttu-id="f8533-111">Sprawdź łączność z usługi serwera Proxy aplikacji w chmurze i strony Login firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="f8533-111">Verify connectivity to the Cloud Application Proxy service and Microsoft Login page</span></span>

<span data-ttu-id="f8533-112">**Cel:** upewnij się, że maszyna łącznika można łączyć do punktu końcowego rejestracji serwera Proxy aplikacji usługi AAD, jak również strony logowania firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f8533-112">**Objective:** Verify that the connector machine can connect to the AAD Application Proxy registration endpoint as well as Microsoft login page.</span></span>

1.  <span data-ttu-id="f8533-113">Otwórz przeglądarkę i przejdź do następnej strony sieci web: <https://aadap-portcheck.connectorporttest.msappproxy.net> i sprawdź, czy łączność środkowe stany USA i wschodnie stany USA centrów danych z portami 9090 i 9091 działa.</span><span class="sxs-lookup"><span data-stu-id="f8533-113">Open a browser and go to the following web page: <https://aadap-portcheck.connectorporttest.msappproxy.net> , and verify that the connectivity to Central US and East US datacenters with ports 9090 and 9091 is working.</span></span>

2.  <span data-ttu-id="f8533-114">Jeśli żadnego z tych portów zakończy się niepowodzeniem (nie ma zielonym znacznikiem wyboru), sprawdź, czy zapora lub zaplecza serwer proxy ma \*. msappproxy.net z portami 9090 i 9091 poprawnie zdefiniowany.</span><span class="sxs-lookup"><span data-stu-id="f8533-114">If any of those ports is not successful (doesn’t have a green checkmark), verify that the Firewall or backend proxy has \*.msappproxy.net with ports 9090 and 9091 defined correctly.</span></span>

3.  <span data-ttu-id="f8533-115">Otwórz w przeglądarce (osobnej karcie) i przejdź do następnej strony sieci web: <https://login.microsoftonline.com>, upewnij się, że możesz zalogować się do tej strony.</span><span class="sxs-lookup"><span data-stu-id="f8533-115">Open a browser (separate tab) and go to the following web page: <https://login.microsoftonline.com>, make sure that you can login to that page.</span></span>

## <a name="verify-machine-and-backend-components-support-for-application-proxy-trust-cert"></a><span data-ttu-id="f8533-116">Sprawdź, czy składniki maszyny i wewnętrznej bazy danych obsługuje dla certyfikatu relacji zaufania serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="f8533-116">Verify Machine and backend components support for Application Proxy trust cert</span></span>

<span data-ttu-id="f8533-117">**Cel:** Sprawdź, czy łącznik maszyny, wewnętrznej bazy danych serwera proxy i zapory można obsługiwać certyfikat utworzony przez łącznik dla przyszłych zaufania.</span><span class="sxs-lookup"><span data-stu-id="f8533-117">**Objective:** Verify that the connector machine, backend proxy and firewall can support the certificate created by the connector for future trust.</span></span>

>[!NOTE]
><span data-ttu-id="f8533-118">Łącznik próbuje utworzyć certyfikatu SHA512, która jest obsługiwana przez TLS1.2.</span><span class="sxs-lookup"><span data-stu-id="f8533-118">The connector tries to create a SHA512 cert that is supported by TLS1.2.</span></span> <span data-ttu-id="f8533-119">Jeśli komputer lub zaporę wewnętrznej bazy danych i serwera proxy nie obsługuje TLS1.2, instalacja się nie powieść.</span><span class="sxs-lookup"><span data-stu-id="f8533-119">If the machine or the backend firewall and proxy does not support TLS1.2, the installation fail.</span></span>
>
>

<span data-ttu-id="f8533-120">**Aby rozwiązać ten problem:**</span><span class="sxs-lookup"><span data-stu-id="f8533-120">**To resolve the issue:**</span></span>

1.  <span data-ttu-id="f8533-121">Sprawdź komputer obsługuje TLS1.2 — wersje wszystkich okien po 2012 R2 powinny obsługiwać protokół TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="f8533-121">Verify the machine supports TLS1.2 – All Windows versions after 2012 R2 should support TLS 1.2.</span></span> <span data-ttu-id="f8533-122">W przypadku komputera łącznika z wersji 2012 R2 lub wcześniej, upewnij się, czy na komputerze są zainstalowane następujące KB/s: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span><span class="sxs-lookup"><span data-stu-id="f8533-122">If your connector machine is from a version of 2012 R2 or prior, make sure that the following KBs are installed on the machine: <https://support.microsoft.com/help/2973337/sha512-is-disabled-in-windows-when-you-use-tls-1.2></span></span>

2.  <span data-ttu-id="f8533-123">Skontaktuj się z administratorem sieci i poproś o Sprawdź, czy wewnętrznej bazy danych serwera proxy i zapory nie blokują SHA512 dla ruchu wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="f8533-123">Contact your network admin and ask to verify that the backend proxy and firewall do not block SHA512 for outgoing traffic.</span></span>

## <a name="verify-admin-is-used-to-install-the-connector"></a><span data-ttu-id="f8533-124">Sprawdź, czy administrator służy do instalowania łącznika</span><span class="sxs-lookup"><span data-stu-id="f8533-124">Verify admin is used to install the connector</span></span>

<span data-ttu-id="f8533-125">**Cel:** Sprawdź, czy administrator z prawidłowymi poświadczeniami użytkownika, który próbuje zainstalować łącznik.</span><span class="sxs-lookup"><span data-stu-id="f8533-125">**Objective:** Verify that the user who tries to install the connector is an administrator with correct credentials.</span></span> <span data-ttu-id="f8533-126">Obecnie użytkownik musi być administratorem globalnym dla instalacji powiodło się.</span><span class="sxs-lookup"><span data-stu-id="f8533-126">Currently, the user must be a global administrator for the installation to succeed.</span></span>

<span data-ttu-id="f8533-127">**Aby sprawdzić, czy poświadczenia są prawidłowe:**</span><span class="sxs-lookup"><span data-stu-id="f8533-127">**To verify the credentials are correct:**</span></span>

<span data-ttu-id="f8533-128">Połączyć się z <https://login.microsoftonline.com> i użyć tych samych poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="f8533-128">Connect to <https://login.microsoftonline.com> and use the same credentials.</span></span> <span data-ttu-id="f8533-129">Upewnij się, że użytkownik zaloguje się ponownie.</span><span class="sxs-lookup"><span data-stu-id="f8533-129">Make sure the login is successful.</span></span> <span data-ttu-id="f8533-130">Rola użytkownika można sprawdzić, przechodząc do **usługi Azure Active Directory**  - &gt; **użytkowników i grup**  - &gt; **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="f8533-130">You can check the user role by going to **Azure Active Directory** -&gt; **Users and Groups** -&gt; **All Users**.</span></span> 

<span data-ttu-id="f8533-131">Wybierz konto użytkownika, następnie "Directory Role" w menu wynikowy.</span><span class="sxs-lookup"><span data-stu-id="f8533-131">Select your user account, then “Directory Role” in the resulting menu.</span></span> <span data-ttu-id="f8533-132">Sprawdź, czy wybraną rolę "Administrator globalny".</span><span class="sxs-lookup"><span data-stu-id="f8533-132">Verify that the selected role is “Global administrator”.</span></span> <span data-ttu-id="f8533-133">Jeśli nie można uzyskać dostępu do żadnych stron wzdłuż następujące kroki, nie jesteś administratorem globalnym.</span><span class="sxs-lookup"><span data-stu-id="f8533-133">If you are unable to access any of the pages along these steps, you are not a global administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8533-134">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f8533-134">Next steps</span></span>
[<span data-ttu-id="f8533-135">Zrozumienie łączniki serwera Proxy aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="f8533-135">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
