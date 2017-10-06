---
title: "Usługa Azure Active Directory B2C: Weibo konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami Weibo w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 1860de34-94cb-4ceb-851e-102f930f7230
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: c0648620f318046c1d9d24feb92a0c5f19c6a91a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-weibo-accounts"></a><span data-ttu-id="11692-103">Usługa Azure Active Directory B2C: Udostępnianie kont Weibo tooconsumers rejestracji i logowania</span><span class="sxs-lookup"><span data-stu-id="11692-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="11692-104">Ta funkcja jest dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="11692-104">This feature is in preview.</span></span> <span data-ttu-id="11692-105">Ten dostawca tożsamości nie należy używać w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="11692-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="11692-106">Tworzenie aplikacji Weibo</span><span class="sxs-lookup"><span data-stu-id="11692-106">Create a Weibo application</span></span>

<span data-ttu-id="11692-107">toouse Weibo jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji Weibo i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="11692-107">toouse Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Weibo application and supply it with hello right parameters.</span></span> <span data-ttu-id="11692-108">Toodo konta Weibo to konieczne.</span><span class="sxs-lookup"><span data-stu-id="11692-108">You need a Weibo account toodo this.</span></span> <span data-ttu-id="11692-109">Jeśli nie masz, możesz ją uzyskać, w [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="11692-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-hello-weibo-developer-program"></a><span data-ttu-id="11692-110">Zarejestruj w programie dla deweloperów Weibo hello</span><span class="sxs-lookup"><span data-stu-id="11692-110">Register for hello Weibo developer program</span></span>

1. <span data-ttu-id="11692-111">Przejdź toohello [portalu dla deweloperów Weibo](http://open.weibo.com/) i zaloguj się przy użyciu poświadczeń konta Weibo.</span><span class="sxs-lookup"><span data-stu-id="11692-111">Go toohello [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="11692-112">Po zalogowaniu kliknij swoją nazwę wyświetlaną w hello prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="11692-112">After signing in, click on your display name in hello top-right corner.</span></span>
3. <span data-ttu-id="11692-113">Z listy rozwijanej hello, wybierz**编辑开发者信息**(Edytuj informacje dla deweloperów).</span><span class="sxs-lookup"><span data-stu-id="11692-113">In hello dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="11692-114">Wprowadź informacje wymagane hello do postaci hello i kliknij**提交**(Prześlij).</span><span class="sxs-lookup"><span data-stu-id="11692-114">Enter hello required information into hello form and click **提交** (submit).</span></span>
5. <span data-ttu-id="11692-115">Ukończ proces weryfikacji wiadomości e-mail hello.</span><span class="sxs-lookup"><span data-stu-id="11692-115">Complete hello email verification process.</span></span>
6. <span data-ttu-id="11692-116">Przejdź toohello [strony weryfikacji tożsamości](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="11692-116">Go toohello [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="11692-117">Wprowadź informacje wymagane hello do postaci hello i kliknij**提交**(Prześlij).</span><span class="sxs-lookup"><span data-stu-id="11692-117">Enter hello required information into hello form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="11692-118">Zarejestrować aplikację Weibo</span><span class="sxs-lookup"><span data-stu-id="11692-118">Register a Weibo application</span></span>

1. <span data-ttu-id="11692-119">Przejdź toohello [nowej strony rejestracji aplikacji Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="11692-119">Go toohello [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="11692-120">Wprowadź informacje niezbędne aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="11692-120">Enter hello necessary application information.</span></span>
3. <span data-ttu-id="11692-121">Kliknij przycisk**创建**(Utwórz).</span><span class="sxs-lookup"><span data-stu-id="11692-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="11692-122">Skopiuj wartości hello **klucz aplikacji** i **klucz tajny aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="11692-122">Copy hello values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="11692-123">Będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="11692-123">You will need this later.</span></span>
5. <span data-ttu-id="11692-124">Przekaż zdjęć hello wymagane, a następnie wprowadź niezbędne informacje hello.</span><span class="sxs-lookup"><span data-stu-id="11692-124">Upload hello required photos and enter hello necessary information.</span></span>
6. <span data-ttu-id="11692-125">Kliknij przycisk**保存以上信息**(Zapisz).</span><span class="sxs-lookup"><span data-stu-id="11692-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="11692-126">Kliknij przycisk**高级信息**(zaawansowane informacje).</span><span class="sxs-lookup"><span data-stu-id="11692-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="11692-127">Kliknij przycisk**编辑**(Edytuj) następnego toohello pola OAuth2.0**授权设置**(adres URL przekierowania).</span><span class="sxs-lookup"><span data-stu-id="11692-127">Click **编辑** (edit) next toohello field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="11692-128">Wprowadź `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` dla OAuth2.0**授权设置**(adres URL przekierowania).</span><span class="sxs-lookup"><span data-stu-id="11692-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="11692-129">Na przykład jeśli Twoje `tenant_name` jest contoso.onmicrosoft.com, zestaw hello adresu URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="11692-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="11692-130">Kliknij przycisk**提交**(Prześlij).</span><span class="sxs-lookup"><span data-stu-id="11692-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="11692-131">Skonfiguruj Weibo funkcję dostawcy tożsamości w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="11692-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="11692-132">Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="11692-132">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="11692-133">W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="11692-133">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="11692-134">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="11692-134">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="11692-135">Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="11692-135">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="11692-136">Wprowadź na przykład "Weibo".</span><span class="sxs-lookup"><span data-stu-id="11692-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="11692-137">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Weibo**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="11692-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="11692-138">Kliknij przycisk **skonfigurować ten dostawca tożsamości**</span><span class="sxs-lookup"><span data-stu-id="11692-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="11692-139">Wprowadź hello **klucz aplikacji** skopiowanego wcześniej jako hello **identyfikator klienta**.</span><span class="sxs-lookup"><span data-stu-id="11692-139">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="11692-140">Wprowadź hello **klucz tajny aplikacji** skopiowanego wcześniej jako hello **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="11692-140">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="11692-141">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave Weibo konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="11692-141">Click **OK** and then click **Create** toosave your Weibo configuration.</span></span>

