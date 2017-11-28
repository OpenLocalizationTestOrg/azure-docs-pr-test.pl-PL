---
title: "aaaSingle logowania jednokrotnego tooapps z serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Włącz logowanie jednokrotne dla aplikacji opublikowanych lokalnymi przy użyciu aplikacji serwera Proxy Azure AD w hello portalu Azure."
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
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a><span data-ttu-id="62bae-103">Hasło vaulting dla logowania jednokrotnego przy użyciu serwera Proxy aplikacji</span><span class="sxs-lookup"><span data-stu-id="62bae-103">Password vaulting for single sign-on with Application Proxy</span></span>

<span data-ttu-id="62bae-104">Azure Active Directory serwera Proxy aplikacji pomaga zwiększyć wydajność przez publikowanie aplikacji lokalnych, dzięki czemu pracowników zdalnych można bezpiecznie uzyskiwać do nich dostęp, zbyt.</span><span class="sxs-lookup"><span data-stu-id="62bae-104">Azure Active Directory Application Proxy helps you improve productivity by publishing on-premises applications so that remote employees can securely access them, too.</span></span> <span data-ttu-id="62bae-105">W portalu Azure hello można skonfigurować pojedynczy logowania jednokrotnego (SSO) toothese aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62bae-105">In hello Azure portal, you can also set up single sign-on (SSO) toothese apps.</span></span> <span data-ttu-id="62bae-106">Użytkownicy potrzebują tylko tooauthenticate z usługą Azure AD, a ich dostęp do aplikacji przedsiębiorstwa bez toosign ponownie.</span><span class="sxs-lookup"><span data-stu-id="62bae-106">Your users only need tooauthenticate with Azure AD, and they can access your enterprise application without having toosign in again.</span></span>

<span data-ttu-id="62bae-107">Serwer Proxy aplikacji obsługuje kilka [pojedynczy logowania jednokrotnego tryby](application-proxy-sso-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62bae-107">Application Proxy supports several [single sign-on modes](application-proxy-sso-overview.md).</span></span> <span data-ttu-id="62bae-108">Na podstawie hasła logowania jest przeznaczony dla aplikacji, które używają kombinacja nazwy użytkownika i hasła do uwierzytelnienia.</span><span class="sxs-lookup"><span data-stu-id="62bae-108">Password-based sign-on is intended for applications that use a username/password combination for authentication.</span></span> <span data-ttu-id="62bae-109">Po skonfigurowaniu opartego na hasłach logowania jednokrotnego dla aplikacji, użytkownicy mają toosign w toohello lokalną aplikację tylko raz.</span><span class="sxs-lookup"><span data-stu-id="62bae-109">When you configure password-based sign-on for your application, your users have toosign in toohello on-premises application once.</span></span> <span data-ttu-id="62bae-110">Po wykonaniu tej usługi Azure Active Directory przechowuje informacje logowania hello i automatycznie udostępnia on toohello aplikacji podczas użytkowników dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="62bae-110">After that, Azure Active Directory stores hello sign-in information and automatically provides it toohello application when your users access it remotely.</span></span> 

<span data-ttu-id="62bae-111">Należy już zostały opublikowane i przetestować aplikację przy użyciu serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62bae-111">You should already have published and tested your app with Application Proxy.</span></span> <span data-ttu-id="62bae-112">Jeśli nie, wykonaj kroki hello w [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-publish-azure-portal.md) następnie potem wróć tutaj.</span><span class="sxs-lookup"><span data-stu-id="62bae-112">If not, follow hello steps in [Publish applications using Azure AD Application Proxy](application-proxy-publish-azure-portal.md) then come back here.</span></span> 

## <a name="set-up-password-vaulting-for-your-application"></a><span data-ttu-id="62bae-113">Ustawianie hasła vaulting aplikacji</span><span class="sxs-lookup"><span data-stu-id="62bae-113">Set up password vaulting for your application</span></span>

1. <span data-ttu-id="62bae-114">Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator.</span><span class="sxs-lookup"><span data-stu-id="62bae-114">Sign in toohello [Azure portal](https://portal.azure.com) as an administrator.</span></span>
2. <span data-ttu-id="62bae-115">Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="62bae-115">Select **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="62bae-116">Z listy hello wybierz hello aplikacji, które mają tooset się z logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="62bae-116">From hello list, select hello app that you want tooset up with SSO.</span></span>  
4. <span data-ttu-id="62bae-117">Wybierz **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="62bae-117">Select **Single sign-on**.</span></span>

   ![Wybierz rejestracji jednokrotnej](./media/application-proxy-sso-azure-portal/select-sso.png)

5. <span data-ttu-id="62bae-119">W trybie logowania jednokrotnego hello, wybierz opcję **opartego na hasłach logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="62bae-119">For hello SSO mode, choose **Password-based Sign-on**.</span></span>
6. <span data-ttu-id="62bae-120">Witaj adres URL logowania wprowadź hello URL strony hello gdzie użytkownicy wprowadź ich toosign nazwy użytkownika i hasła w aplikacji tooyour poza siecią firmową hello.</span><span class="sxs-lookup"><span data-stu-id="62bae-120">For hello Sign-on URL, enter hello URL for hello page where users enter their username and password toosign in tooyour app outside of hello corporate network.</span></span> <span data-ttu-id="62bae-121">Może to być hello zewnętrzny adres URL, które utworzono podczas publikowania aplikacji hello za pośrednictwem serwera Proxy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62bae-121">This may be hello External URL that you created when you published hello app through Application Proxy.</span></span> 

   ![Wybierz opartego na hasłach logowania jednokrotnego, a następnie wprowadź adres URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. <span data-ttu-id="62bae-123">Wybierz pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="62bae-123">Select **Save**.</span></span>

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a><span data-ttu-id="62bae-124">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="62bae-124">Test your app</span></span>

<span data-ttu-id="62bae-125">Przejdź tooexternal adres URL skonfigurowany dla aplikacji tooyour dostępu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="62bae-125">Go tooexternal URL that you configured for remote access tooyour application.</span></span> <span data-ttu-id="62bae-126">Zaloguj się przy użyciu poświadczeń dla danej aplikacji (lub hello poświadczenia dla konta testowego skonfigurowanego przy użyciu dostępu).</span><span class="sxs-lookup"><span data-stu-id="62bae-126">Sign in with your credentials for that app (or hello credentials for a test account that you set up with access).</span></span> <span data-ttu-id="62bae-127">Po zalogowaniu pomyślnie należy aplikacji hello tooleave może być i wrócić bez konieczności ponownego wprowadzania poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="62bae-127">Once you sign in successfully, you should be able tooleave hello app and come back without entering your credentials again.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="62bae-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="62bae-128">Next steps</span></span>

- <span data-ttu-id="62bae-129">Przeczytaj informacje o innych sposobów tooimplement [rejestracji jednokrotnej z serwerem Proxy aplikacji](application-proxy-sso-overview.md)</span><span class="sxs-lookup"><span data-stu-id="62bae-129">Read about other ways tooimplement [Single sign-on with Application Proxy](application-proxy-sso-overview.md)</span></span>
- <span data-ttu-id="62bae-130">Dowiedz się więcej o [zagadnienia dotyczące zabezpieczeń w celu uzyskania dostępu do aplikacji zdalnie z serwera Proxy aplikacji usługi Azure AD](application-proxy-security-considerations.md)</span><span class="sxs-lookup"><span data-stu-id="62bae-130">Learn about [Security considerations for accessing apps remotely with Azure AD Application Proxy](application-proxy-security-considerations.md)</span></span>