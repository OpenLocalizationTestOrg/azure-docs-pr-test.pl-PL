---
title: "Usługa Azure Active Directory B2C: Q konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami q w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 18c2cf94-8004-4de1-81c2-e45be65ce12d
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 896d6221e01d15de1652a5717cf1f65619101e0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-qq-accounts"></a><span data-ttu-id="9f69b-103">Usługa Azure Active Directory B2C: Udostępnianie kont q tooconsumers rejestracji i logowania</span><span class="sxs-lookup"><span data-stu-id="9f69b-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with QQ accounts</span></span>

> [!NOTE]
> <span data-ttu-id="9f69b-104">Ta funkcja jest dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="9f69b-104">This feature is in preview.</span></span>
> 

## <a name="create-a-qq-application"></a><span data-ttu-id="9f69b-105">Tworzenie aplikacji q</span><span class="sxs-lookup"><span data-stu-id="9f69b-105">Create a QQ application</span></span>

<span data-ttu-id="9f69b-106">toouse q jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji q i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="9f69b-106">toouse QQ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a QQ application and supply it with hello right parameters.</span></span> <span data-ttu-id="9f69b-107">Toodo konta q to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9f69b-107">You need a QQ account toodo this.</span></span> <span data-ttu-id="9f69b-108">Jeśli nie masz, możesz ją uzyskać, w [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span><span class="sxs-lookup"><span data-stu-id="9f69b-108">If you don’t have one, you can get one at [https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033](https://ssl.zc.qq.com/en/index.html?type=1&ptlang=1033).</span></span>

### <a name="register-for-hello-qq-developer-program"></a><span data-ttu-id="9f69b-109">Zarejestruj w programie dla deweloperów q hello</span><span class="sxs-lookup"><span data-stu-id="9f69b-109">Register for hello QQ developer program</span></span>

1. <span data-ttu-id="9f69b-110">Przejdź toohello [portalu dla deweloperów q](http://open.qq.com) i zaloguj się przy użyciu poświadczeń konta q.</span><span class="sxs-lookup"><span data-stu-id="9f69b-110">Go toohello [QQ developer portal](http://open.qq.com) and sign in with your QQ account credentials.</span></span>
2. <span data-ttu-id="9f69b-111">Po zalogowaniu Przejdź zbyt[http://open.qq.com/reg](http://open.qq.com/reg) tooregister samodzielnie dewelopera.</span><span class="sxs-lookup"><span data-stu-id="9f69b-111">After signing in, go too[http://open.qq.com/reg](http://open.qq.com/reg) tooregister yourself as a developer.</span></span>
3. <span data-ttu-id="9f69b-112">Wybierz hello menu**个人**(poszczególnych deweloperów).</span><span class="sxs-lookup"><span data-stu-id="9f69b-112">In hello menu, select **个人** (individual developer).</span></span>
4. <span data-ttu-id="9f69b-113">Wprowadź informacje wymagane hello do postaci hello i kliknij**下一步**(następny krok).</span><span class="sxs-lookup"><span data-stu-id="9f69b-113">Enter hello required information into hello form and click **下一步** (next step).</span></span>
5. <span data-ttu-id="9f69b-114">Ukończ proces weryfikacji wiadomości e-mail hello.</span><span class="sxs-lookup"><span data-stu-id="9f69b-114">Complete hello email verification process.</span></span>

> [!NOTE]
> <span data-ttu-id="9f69b-115">Konieczne będzie toowait kilka toobe dni zatwierdzone po zarejestrowaniu dewelopera.</span><span class="sxs-lookup"><span data-stu-id="9f69b-115">You will need toowait a few days toobe approved after registering as a developer.</span></span> 

### <a name="register-a-qq-application"></a><span data-ttu-id="9f69b-116">Zarejestrować aplikację q</span><span class="sxs-lookup"><span data-stu-id="9f69b-116">Register a QQ application</span></span>

1. <span data-ttu-id="9f69b-117">Przejdź za[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span><span class="sxs-lookup"><span data-stu-id="9f69b-117">Go too[https://connect.qq.com/index.html](https://connect.qq.com/index.html).</span></span>
2. <span data-ttu-id="9f69b-118">Polecenie**应用管理**(Zarządzanie aplikacjami).</span><span class="sxs-lookup"><span data-stu-id="9f69b-118">Click on **应用管理** (app management).</span></span>
3. <span data-ttu-id="9f69b-119">Polecenie**创建应用**(Tworzenie aplikacji).</span><span class="sxs-lookup"><span data-stu-id="9f69b-119">Click on **创建应用** (create app).</span></span>
4. <span data-ttu-id="9f69b-120">Wprowadź informacje niezbędne aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="9f69b-120">Enter hello necessary app information.</span></span>
5. <span data-ttu-id="9f69b-121">Polecenie**创建应用**(Tworzenie aplikacji).</span><span class="sxs-lookup"><span data-stu-id="9f69b-121">Click on **创建应用** (create app).</span></span>
6. <span data-ttu-id="9f69b-122">Wprowadź informacje wymagane hello.</span><span class="sxs-lookup"><span data-stu-id="9f69b-122">Enter hello required information.</span></span>
7. <span data-ttu-id="9f69b-123">Dla hello**授权回调域**(adres URL wywołania zwrotnego) wprowadź `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="9f69b-123">For hello **授权回调域** (callback URL) field, enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="9f69b-124">Na przykład jeśli Twoje `tenant_name` jest contoso.onmicrosoft.com, zestaw hello adresu URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="9f69b-124">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
8. <span data-ttu-id="9f69b-125">Polecenie**创建应用**(Tworzenie aplikacji).</span><span class="sxs-lookup"><span data-stu-id="9f69b-125">Click on **创建应用** (create app).</span></span>
9. <span data-ttu-id="9f69b-126">Na stronie potwierdzenia hello, kliknij**应用管理**strony zarządzania aplikacji toohello tooreturn (Zarządzanie aplikacjami).</span><span class="sxs-lookup"><span data-stu-id="9f69b-126">On hello confirmation page, click on **应用管理** (app management) tooreturn toohello app management page.</span></span>
10. <span data-ttu-id="9f69b-127">Polecenie**查看**dalej aplikacji toohello (Widok), został utworzony.</span><span class="sxs-lookup"><span data-stu-id="9f69b-127">Click on **查看** (view) next toohello app you just created.</span></span>
11. <span data-ttu-id="9f69b-128">Polecenie**修改**(Edycja).</span><span class="sxs-lookup"><span data-stu-id="9f69b-128">Click on **修改** (edit).</span></span>
12. <span data-ttu-id="9f69b-129">Z góry hello hello strony, skopiuj hello **identyfikator aplikacji** i **klucz aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="9f69b-129">From hello top of hello page, copy hello **APP ID** and **APP KEY**.</span></span>

## <a name="configure-qq-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="9f69b-130">Skonfiguruj funkcję dostawcy tożsamości w dzierżawie q</span><span class="sxs-lookup"><span data-stu-id="9f69b-130">Configure QQ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="9f69b-131">Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9f69b-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="9f69b-132">W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="9f69b-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="9f69b-133">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="9f69b-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="9f69b-134">Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9f69b-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="9f69b-135">Wprowadź na przykład "Q".</span><span class="sxs-lookup"><span data-stu-id="9f69b-135">For example, enter "QQ".</span></span>
5. <span data-ttu-id="9f69b-136">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **q**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f69b-136">Click **Identity provider type**, select **QQ**, and click **OK**.</span></span>
6. <span data-ttu-id="9f69b-137">Kliknij przycisk **skonfigurować ten dostawca tożsamości**</span><span class="sxs-lookup"><span data-stu-id="9f69b-137">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="9f69b-138">Wprowadź hello **klucz aplikacji** skopiowanego wcześniej jako hello **identyfikator klienta**.</span><span class="sxs-lookup"><span data-stu-id="9f69b-138">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="9f69b-139">Wprowadź hello **klucz tajny aplikacji** skopiowanego wcześniej jako hello **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="9f69b-139">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="9f69b-140">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfigurację q.</span><span class="sxs-lookup"><span data-stu-id="9f69b-140">Click **OK** and then click **Create** toosave your QQ configuration.</span></span>

