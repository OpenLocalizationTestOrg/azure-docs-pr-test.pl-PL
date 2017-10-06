---
title: "aplikacje świadome aaaClaims - serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak toopublish lokalnej aplikacji ASP.NET, które akceptują oświadczenia usług AD FS dla bezpieczny dostęp zdalny przez użytkowników."
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
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a><span data-ttu-id="f7b91-103">Praca z aplikacji obsługujących oświadczenia w serwer Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="f7b91-103">Working with claims-aware apps in Application Proxy</span></span>
<span data-ttu-id="f7b91-104">[Aplikacje obsługujące oświadczenia](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) wykonania przekierowania toohello zabezpieczeń usługi tokenów (STS).</span><span class="sxs-lookup"><span data-stu-id="f7b91-104">[Claims-aware apps](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) perform a redirection toohello Security Token Service (STS).</span></span> <span data-ttu-id="f7b91-105">Hello STS żądania poświadczeń użytkownika hello zamian token i następnie przekierowuje hello użytkownika toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7b91-105">hello STS requests credentials from hello user in exchange for a token and then redirects hello user toohello application.</span></span> <span data-ttu-id="f7b91-106">Istnieje kilka sposobów tooenable serwera Proxy aplikacji toowork z tych przekierowania.</span><span class="sxs-lookup"><span data-stu-id="f7b91-106">There are a few ways tooenable Application Proxy toowork with these redirects.</span></span> <span data-ttu-id="f7b91-107">Użyj tego artykułu tooconfigure wdrożenia dla aplikacji obsługujących oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="f7b91-107">Use this article tooconfigure your deployment for claims-aware apps.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f7b91-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f7b91-108">Prerequisites</span></span>
<span data-ttu-id="f7b91-109">Upewnij się, że ten hello STS hello aplikacji obsługującej oświadczenia przekierowuje toois dostępne spoza sieci lokalnej.</span><span class="sxs-lookup"><span data-stu-id="f7b91-109">Make sure that hello STS that hello claims-aware app redirects toois available outside of your on-premises network.</span></span> <span data-ttu-id="f7b91-110">Można udostępnić hello STS ujawnienie go za pośrednictwem serwera proxy lub zezwalając poza połączenia.</span><span class="sxs-lookup"><span data-stu-id="f7b91-110">You can make hello STS available by exposing it through a proxy or by allowing outside connections.</span></span> 

## <a name="publish-your-application"></a><span data-ttu-id="f7b91-111">Publikowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="f7b91-111">Publish your application</span></span>

1. <span data-ttu-id="f7b91-112">Publikowanie aplikacji zgodnie z instrukcjami toohello opisanego w [publikowania aplikacji za pomocą serwera Proxy aplikacji](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f7b91-112">Publish your application according toohello instructions described in [Publish applications with Application Proxy](application-proxy-publish-azure-portal.md).</span></span>
2. <span data-ttu-id="f7b91-113">Przejdź do strony aplikacji hello portalu i wybierz pozycję toohello **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-113">Navigate toohello application page in hello portal and select **Single sign-on**.</span></span>
3. <span data-ttu-id="f7b91-114">Jeśli została wybrana opcja **usługi Azure Active Directory** jako sieci **metoda uwierzytelniania wstępnego**, wybierz pozycję **usługi Azure AD rejestracji jednokrotnej wyłączone** jako sieci **wewnętrzne Metoda uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-114">If you chose **Azure Active Directory** as your **Preauthentication Method**, select **Azure AD single sign-on disabled** as your **Internal Authentication Method**.</span></span> <span data-ttu-id="f7b91-115">Jeśli została wybrana opcja **Passthrough** jako sieci **metoda uwierzytelniania wstępnego**, nie potrzebujesz cokolwiek toochange.</span><span class="sxs-lookup"><span data-stu-id="f7b91-115">If you chose **Passthrough** as your **Preauthentication Method**, you don't need toochange anything.</span></span>

## <a name="configure-adfs"></a><span data-ttu-id="f7b91-116">Konfigurowanie usług AD FS</span><span class="sxs-lookup"><span data-stu-id="f7b91-116">Configure ADFS</span></span>

<span data-ttu-id="f7b91-117">Usługi AD FS można skonfigurować dla aplikacji obsługujących oświadczenia w jeden z dwóch sposobów.</span><span class="sxs-lookup"><span data-stu-id="f7b91-117">You can configure ADFS for claims-aware apps in one of two ways.</span></span> <span data-ttu-id="f7b91-118">Hello jest najpierw przy użyciu domen niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="f7b91-118">hello first is by using custom domains.</span></span> <span data-ttu-id="f7b91-119">Hello jest drugi z protokołu WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="f7b91-119">hello second is with WS-Federation.</span></span> 

### <a name="option-1-custom-domains"></a><span data-ttu-id="f7b91-120">Opcja 1: Domen niestandardowych</span><span class="sxs-lookup"><span data-stu-id="f7b91-120">Option 1: Custom domains</span></span>

<span data-ttu-id="f7b91-121">Jeśli wszystkie hello wewnętrzne adresy URL dla aplikacji są w pełni kwalifikowanej nazwy domen (FQDN), a następnie można skonfigurować [domen niestandardowych](active-directory-application-proxy-custom-domains.md) dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f7b91-121">If all hello internal URLs for your applications are fully qualified domain names (FQDNs), then you can configure [custom domains](active-directory-application-proxy-custom-domains.md) for your applications.</span></span> <span data-ttu-id="f7b91-122">Użyj hello domen niestandardowych toocreate zewnętrznych adresów URL, które są takie same jak hello wewnętrzne adresy URL hello.</span><span class="sxs-lookup"><span data-stu-id="f7b91-122">Use hello custom domains toocreate external URLs that are hello same as hello internal URLs.</span></span> <span data-ttu-id="f7b91-123">W przypadku sieci zewnętrzne adresy URL zgodne z wewnętrznych adresów URL, przekierowań STS hello pracować, czy użytkownicy są lokalnego lub zdalnego.</span><span class="sxs-lookup"><span data-stu-id="f7b91-123">When your external URLs match your internal URLs, then hello STS redirections work whether your users are on-premises or remote.</span></span> 

### <a name="option-2-ws-federation"></a><span data-ttu-id="f7b91-124">Opcja 2: WS-Federation</span><span class="sxs-lookup"><span data-stu-id="f7b91-124">Option 2: WS-Federation</span></span>

1. <span data-ttu-id="f7b91-125">Otwórz przystawkę Zarządzanie usługi AD FS.</span><span class="sxs-lookup"><span data-stu-id="f7b91-125">Open ADFS Management.</span></span>
2. <span data-ttu-id="f7b91-126">Przejdź za**zaufania jednostek uzależnionych**, kliknij prawym przyciskiem myszy w aplikacji hello są publikowanie za pomocą serwera Proxy aplikacji i wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-126">Go too**Relying Party Trusts**, right-click on hello app you are publishing with Application Proxy, and choose **Properties**.</span></span>  

   ![Zaufania jednostek uzależnionych kliknij prawym przyciskiem myszy nazwę aplikacji — zrzut ekranu](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. <span data-ttu-id="f7b91-128">Na powitania **punkty końcowe** , w obszarze **typ punktu końcowego**, wybierz pozycję **WS-Federation**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-128">On hello **Endpoints** tab, under **Endpoint type**, select **WS-Federation**.</span></span>
4. <span data-ttu-id="f7b91-129">W obszarze **URL zaufanych**, wprowadź adres URL hello wprowadzony w powitania serwera Proxy aplikacji w obszarze **zewnętrzny adres URL** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f7b91-129">Under **Trusted URL**, enter hello URL you entered in hello Application Proxy under **External URL** and click **OK**.</span></span>  

   ![Dodawanie punktu końcowego — ustaw wartość adres URL z zaufanych — zrzut ekranu](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a><span data-ttu-id="f7b91-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f7b91-131">Next steps</span></span>
* <span data-ttu-id="f7b91-132">[Włącz jednokrotnego](application-proxy-sso-overview.md) dla aplikacji, które nie są obsługujących oświadczenia</span><span class="sxs-lookup"><span data-stu-id="f7b91-132">[Enable single-sign on](application-proxy-sso-overview.md) for applications that aren't claims-aware</span></span>
* [<span data-ttu-id="f7b91-133">Włącz toointeract aplikacji natywnej klienta z serwera proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="f7b91-133">Enable native client apps toointeract with proxy applications</span></span>](active-directory-application-proxy-native-client.md)


