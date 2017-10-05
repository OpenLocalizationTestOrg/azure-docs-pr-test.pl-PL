---
title: "Aplikacje obsługujące oświadczenia — serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak opublikować lokalnej aplikacji ASP.NET, które akceptują oświadczenia usług AD FS dla bezpieczny dostęp zdalny przez użytkowników."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 5784222608b01509fc4ff84b1a8792cbcfea89e6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="f4de5-103">Praca z aplikacji obsługujących oświadczenia w serwer Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="f4de5-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="f4de5-104">[Aplikacje obsługujące oświadczenia](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) wykonania przekierowania do zabezpieczenia usługi tokenów (STS).</span><span class="sxs-lookup"><span data-stu-id="f4de5-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection to the Security Token Service (STS).</span></span> <span data-ttu-id="f4de5-105">Usługi STS żąda poświadczeń użytkownika w zamian tokenu, a następnie przekierowuje użytkownika do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4de5-105">The STS requests credentials from the user in exchange for a token and then redirects the user to the application.</span></span> <span data-ttu-id="f4de5-106">Istnieje kilka sposobów, aby włączyć serwer Proxy aplikacji do pracy z tymi przekierowania.</span><span class="sxs-lookup"><span data-stu-id="f4de5-106">There are a few ways to enable Application Proxy to work with these redirects.</span></span> <span data-ttu-id="f4de5-107">W tym artykule umożliwiają konfigurowanie wdrożenia dla aplikacji obsługujących oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="f4de5-107">Use this article to configure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f4de5-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f4de5-108">Prerequisites</span></span>
<span data-ttu-id="f4de5-109">Upewnij się, że usługa tokenu Zabezpieczającego, które przekierowuje aplikacji obsługującej oświadczenia jest dostępny poza siecią lokalną.</span><span class="sxs-lookup"><span data-stu-id="f4de5-109">Make sure that the STS that the claims-aware app redirects to is available outside of your on-premises network.</span></span> <span data-ttu-id="f4de5-110">Można udostępnić usługi STS ujawnienie go za pośrednictwem serwera proxy lub zezwala na zewnętrzne połączenia.</span><span class="sxs-lookup"><span data-stu-id="f4de5-110">You can make the STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="f4de5-111">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f4de5-111">Publish your application</span></span>

1. <span data-ttu-id="f4de5-112">Publikowanie aplikacji zgodnie z instrukcjami opisanego w [publikowania aplikacji za pomocą serwera Proxy aplikacji](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f4de5-112">Publish your application according to the instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="f4de5-113">Przejdź do strony aplikacji w portalu i wybierz **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f4de5-113">Navigate to the application page in the portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="f4de5-114">Jeśli została wybrana opcja **usługi Azure Active Directory** jako sieci **metoda uwierzytelniania wstępnego**, wybierz pozycję **usługi Azure AD rejestracji jednokrotnej wyłączone** jako sieci **wewnętrzne Metoda uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="f4de5-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="f4de5-115">Jeśli została wybrana opcja **Passthrough** jako sieci **metoda uwierzytelniania wstępnego**, nie jest konieczne wprowadzanie zmian.</span><span class="sxs-lookup"><span data-stu-id="f4de5-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need to change anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="f4de5-116">Konfigurowanie usług AD FS</span><span class="sxs-lookup"><span data-stu-id="f4de5-116">Configure ADFS</span></span>

<span data-ttu-id="f4de5-117">Usługi AD FS można skonfigurować dla aplikacji obsługujących oświadczenia w jeden z dwóch sposobów.</span><span class="sxs-lookup"><span data-stu-id="f4de5-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="f4de5-118">Pierwsza to przy użyciu domen niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="f4de5-118">The first is by using custom domains.</span></span> <span data-ttu-id="f4de5-119">Drugim jest z protokołu WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="f4de5-119">The second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="f4de5-120">Opcja 1: Domen niestandardowych</span><span class="sxs-lookup"><span data-stu-id="f4de5-120">Option 1: Custom domains</span></span>

<span data-ttu-id="f4de5-121">Jeśli wszystkie wewnętrzne adresy URL dla aplikacji są w pełni kwalifikowanej nazwy domeny (FQDN), a następnie można skonfigurować [domen niestandardowych](active-directory-application-proxy-custom-domains.md) dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4de5-121">If all the internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="f4de5-122">Użyj domeny niestandardowe, aby utworzyć zewnętrzne adresy URL, które są takie same jak wewnętrzne adresy URL.</span><span class="sxs-lookup"><span data-stu-id="f4de5-122">Use the custom domains to create external URLs that are the same as the internal URLs.</span></span> <span data-ttu-id="f4de5-123">W przypadku sieci zewnętrzne adresy URL zgodne z wewnętrznych adresów URL, przekierowań STS pracować, czy użytkownicy są lokalnego lub zdalnego.</span><span class="sxs-lookup"><span data-stu-id="f4de5-123">When your external URLs match your internal URLs, then the STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="f4de5-124">Opcja 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="f4de5-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="f4de5-125">Otwórz przystawkę Zarządzanie usługi AD FS.</span><span class="sxs-lookup"><span data-stu-id="f4de5-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="f4de5-126">Przejdź do **zaufania jednostek uzależnionych**, kliknij prawym przyciskiem myszy w aplikacji są publikowanie za pomocą serwera Proxy aplikacji i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f4de5-126">Go to **Relying Party Trusts**, right-click on the app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Zaufania jednostek uzależnionych kliknij prawym przyciskiem myszy nazwę aplikacji — zrzut ekranu](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="f4de5-128">Na **punkty końcowe** , w obszarze **typ punktu końcowego**, wybierz pozycję **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="f4de5-128">On the **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="f4de5-129">W obszarze **URL zaufanych**, wprowadź adres URL wprowadzony w serwer Proxy aplikacji w obszarze **zewnętrzny adres URL** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4de5-129">Under **Trusted URL**, enter the URL you entered in the Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Dodawanie punktu końcowego — ustaw wartość adres URL z zaufanych — zrzut ekranu](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="f4de5-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4de5-131">Next steps</span></span>
* <span data-ttu-id="f4de5-132">[Włącz jednokrotnego](application-proxy-sso-overview.md) dla aplikacji, które nie są obsługujących oświadczenia</span><span class="sxs-lookup"><span data-stu-id="f4de5-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="f4de5-133">Włącz aplikacji klienta natywnego wchodzić w interakcje z serwera proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="f4de5-133">Enable native client apps to interact with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


