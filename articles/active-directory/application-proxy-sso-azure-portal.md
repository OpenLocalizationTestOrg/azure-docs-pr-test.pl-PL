---
title: "Logowanie jednokrotne do aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Włącz pojedynczego logowania do aplikacji opublikowanych lokalnymi przy użyciu aplikacji serwera Proxy Azure AD w portalu Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 9ddc0c1bd5f2cbb24f6761cfd041b820ee6464b8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="810f1-103">Hasło vaulting dla logowania jednokrotnego przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="810f1-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="810f1-104">Azure Active Directory serwera Proxy aplikacji pomaga zwiększyć wydajność przez publikowanie aplikacji lokalnych, dzięki czemu pracowników zdalnych można bezpiecznie uzyskiwać do nich dostęp, zbyt.</span><span class="sxs-lookup"><span data-stu-id="810f1-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="810f1-105">W portalu Azure można również skonfigurowaniu rejestracji jednokrotnej (SSO) do tych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="810f1-105">In the Azure portal, you can also set up single sign-on (SSO) to these apps.</span></span> <span data-ttu-id="810f1-106">Użytkownicy potrzebują tylko do uwierzytelniania za pomocą usługi Azure AD i uzyskać dostęp do aplikacji przedsiębiorstwa bez konieczności ponownego logowania się.</span><span class="sxs-lookup"><span data-stu-id="810f1-106">Your users only need to authenticate with Azure AD, and they can access your enterprise application without having to sign in again.</span></span>

<span data-ttu-id="810f1-107">Serwer Proxy aplikacji obsługuje kilka [pojedynczy logowania jednokrotnego tryby](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="810f1-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="810f1-108">Na podstawie hasła logowania jest przeznaczony dla aplikacji, które używają kombinacja nazwy użytkownika i hasła do uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="810f1-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="810f1-109">Po skonfigurowaniu opartego na hasłach logowania jednokrotnego dla aplikacji, użytkownicy muszą zalogować się do aplikacji lokalnych raz.</span><span class="sxs-lookup"><span data-stu-id="810f1-109">When you configure password-based sign-on for your application, your users have to sign in to the on-premises application once.</span></span> <span data-ttu-id="810f1-110">Po wykonaniu tej usługi Azure Active Directory są przechowywane informacje logowania i automatycznie gwarantuje on aplikacji przez użytkowników dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="810f1-110">After that, Azure Active Directory stores the sign-in information and automatically provides it to the application when your users access it remotely.</span></span> 

<span data-ttu-id="810f1-111">Należy już zostały opublikowane i przetestować aplikację przy użyciu serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="810f1-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="810f1-112">Jeśli nie, postępuj zgodnie z instrukcjami [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-publish-azure-portal.md) następnie potem wróć tutaj.</span><span class="sxs-lookup"><span data-stu-id="810f1-112">If not, follow the steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="810f1-113">Ustawianie hasła vaulting aplikacji</span><span class="sxs-lookup"><span data-stu-id="810f1-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="810f1-114">Zaloguj się do witryny [Azure Portal](https://portal.azure.com) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="810f1-114">Sign in to the [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="810f1-115">Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="810f1-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="810f1-116">Z listy wybierz aplikację, którą chcesz skonfigurować przy użyciu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="810f1-116">From the list, select the app that you want to set up with SSO.</span></span>  
4. <span data-ttu-id="810f1-117">Wybierz **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="810f1-117">Select **Single sign-on**.</span></span>

   ![Wybierz rejestracji jednokrotnej](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="810f1-119">W trybie logowania jednokrotnego, wybierz opcję **opartego na hasłach logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="810f1-119">For the SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="810f1-120">Adres URL logowania wprowadź adres URL strony, gdzie użytkownicy wprowadzić swoją nazwę i hasło do logowania do aplikacji spoza sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="810f1-120">For the Sign-on URL, enter the URL for the page where users enter their username and password to sign in to your app outside of the corporate network.</span></span> <span data-ttu-id="810f1-121">Może to być zewnętrzny adres URL, który został utworzony podczas publikowania aplikacji za pośrednictwem serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="810f1-121">This may be the External URL that you created when you published the app through Application Proxy.</span></span> 

   ![Wybierz opartego na hasłach logowania jednokrotnego, a następnie wprowadź adres URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="810f1-123">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="810f1-123">Select **Save**.</span></span>

<!-- Need to repro?
7. The page should tell you that a sign-in form was successfully detected at the provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow the instructions to point out where the sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="810f1-124">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="810f1-124">Test your app</span></span>

<span data-ttu-id="810f1-125">Przejdź do zewnętrznego adresu URL skonfigurowanego dla dostępu zdalnego do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="810f1-125">Go to external URL that you configured for remote access to your application.</span></span> <span data-ttu-id="810f1-126">Zaloguj się przy użyciu poświadczeń dla danej aplikacji (lub poświadczenia dla konta testu, które można skonfigurować przy użyciu dostępu).</span><span class="sxs-lookup"><span data-stu-id="810f1-126">Sign in with your credentials for that app (or the credentials for a test account that you set up with access).</span></span> <span data-ttu-id="810f1-127">Po zalogowaniu pomyślnie, można pozostawić aplikacji i wrócić bez konieczności ponownego wprowadzania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="810f1-127">Once you sign in successfully, you should be able to leave the app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="810f1-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="810f1-128">Next steps</span></span>

- <span data-ttu-id="810f1-129">Przeczytaj informacje o innych sposobach zaimplementować [rejestracji jednokrotnej z serwerem Proxy aplikacji](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="810f1-129">Read about other ways to implement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="810f1-130">Dowiedz się więcej o [zagadnienia dotyczące zabezpieczeń w celu uzyskania dostępu do aplikacji zdalnie z serwera Proxy aplikacji usługi Azure AD](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="810f1-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>