---
title: "Usługa Azure Active Directory B2C: Weibo konfiguracji | Dokumentacja firmy Microsoft"
description: "Umożliwiają tworzenie kont i logowania użytkowników z kontami Weibo w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
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
ms.openlocfilehash: 00c5d3781455c80b33bdbb4c872ae354531baf3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-weibo-accounts"></a><span data-ttu-id="0d583-103">Usługa Azure Active Directory B2C: Umożliwiają rejestracji i logowania użytkowników z kontami Weibo</span><span class="sxs-lookup"><span data-stu-id="0d583-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Weibo accounts</span></span>

> [!NOTE]
> <span data-ttu-id="0d583-104">Ta funkcja jest dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="0d583-104">This feature is in preview.</span></span> <span data-ttu-id="0d583-105">Ten dostawca tożsamości nie należy używać w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="0d583-105">Do not use this identity provider in your production environment.</span></span>
> 

## <a name="create-a-weibo-application"></a><span data-ttu-id="0d583-106">Tworzenie aplikacji Weibo</span><span class="sxs-lookup"><span data-stu-id="0d583-106">Create a Weibo application</span></span>

<span data-ttu-id="0d583-107">Aby użyć Weibo jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy utworzyć aplikację Weibo i dostarczyć prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="0d583-107">To use Weibo as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Weibo application and supply it with the right parameters.</span></span> <span data-ttu-id="0d583-108">Należy to zrobić przy użyciu konta Weibo.</span><span class="sxs-lookup"><span data-stu-id="0d583-108">You need a Weibo account to do this.</span></span> <span data-ttu-id="0d583-109">Jeśli nie masz, możesz ją uzyskać, w [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span><span class="sxs-lookup"><span data-stu-id="0d583-109">If you don’t have one, you can get one at [http://weibo.com/signup/signup.php?lang=en-us](http://weibo.com/signup/signup.php?lang=en-us).</span></span>

### <a name="register-for-the-weibo-developer-program"></a><span data-ttu-id="0d583-110">Zarejestruj w programie dla deweloperów Weibo</span><span class="sxs-lookup"><span data-stu-id="0d583-110">Register for the Weibo developer program</span></span>

1. <span data-ttu-id="0d583-111">Przejdź do [portalu dla deweloperów Weibo](http://open.weibo.com/) i zaloguj się przy użyciu poświadczeń konta Weibo.</span><span class="sxs-lookup"><span data-stu-id="0d583-111">Go to the [Weibo developer portal](http://open.weibo.com/) and sign in with your Weibo account credentials.</span></span>
2. <span data-ttu-id="0d583-112">Po zalogowaniu kliknij swoją nazwę wyświetlaną w prawym górnym rogu.</span><span class="sxs-lookup"><span data-stu-id="0d583-112">After signing in, click on your display name in the top-right corner.</span></span>
3. <span data-ttu-id="0d583-113">Na liście rozwijanej wybierz**编辑开发者信息**(Edytuj informacje dla deweloperów).</span><span class="sxs-lookup"><span data-stu-id="0d583-113">In the dropdown, select **编辑开发者信息** (edit developer information).</span></span>
4. <span data-ttu-id="0d583-114">Wprowadź informacje wymagane do formularza, a następnie kliknij przycisk**提交**(Prześlij).</span><span class="sxs-lookup"><span data-stu-id="0d583-114">Enter the required information into the form and click **提交** (submit).</span></span>
5. <span data-ttu-id="0d583-115">Ukończ proces weryfikacji wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="0d583-115">Complete the email verification process.</span></span>
6. <span data-ttu-id="0d583-116">Przejdź do [strony weryfikacji tożsamości](http://open.weibo.com/developers/identity/edit).</span><span class="sxs-lookup"><span data-stu-id="0d583-116">Go to the [identity verification page](http://open.weibo.com/developers/identity/edit).</span></span>
7. <span data-ttu-id="0d583-117">Wprowadź informacje wymagane do formularza, a następnie kliknij przycisk**提交**(Prześlij).</span><span class="sxs-lookup"><span data-stu-id="0d583-117">Enter the required information into the form and click **提交** (submit).</span></span>

### <a name="register-a-weibo-application"></a><span data-ttu-id="0d583-118">Zarejestrować aplikację Weibo</span><span class="sxs-lookup"><span data-stu-id="0d583-118">Register a Weibo application</span></span>

1. <span data-ttu-id="0d583-119">Przejdź do [nowej strony rejestracji aplikacji Weibo](http://open.weibo.com/apps/new).</span><span class="sxs-lookup"><span data-stu-id="0d583-119">Go to the [new Weibo app registration page](http://open.weibo.com/apps/new).</span></span>
2. <span data-ttu-id="0d583-120">Wprowadź informacje niezbędne aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0d583-120">Enter the necessary application information.</span></span>
3. <span data-ttu-id="0d583-121">Kliknij przycisk**创建**(Utwórz).</span><span class="sxs-lookup"><span data-stu-id="0d583-121">Click **创建** (create).</span></span>
4. <span data-ttu-id="0d583-122">Skopiuj wartości z **klucz aplikacji** i **klucz tajny aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="0d583-122">Copy the values of **App Key** and **App Secret**.</span></span> <span data-ttu-id="0d583-123">Będzie on potrzebny później.</span><span class="sxs-lookup"><span data-stu-id="0d583-123">You will need this later.</span></span>
5. <span data-ttu-id="0d583-124">Przekazywanie wymaganych zdjęć i wprowadź wymagane informacje.</span><span class="sxs-lookup"><span data-stu-id="0d583-124">Upload the required photos and enter the necessary information.</span></span>
6. <span data-ttu-id="0d583-125">Kliknij przycisk**保存以上信息**(Zapisz).</span><span class="sxs-lookup"><span data-stu-id="0d583-125">Click **保存以上信息** (save).</span></span>
7. <span data-ttu-id="0d583-126">Kliknij przycisk**高级信息**(zaawansowane informacje).</span><span class="sxs-lookup"><span data-stu-id="0d583-126">Click **高级信息** (advanced information).</span></span>
8. <span data-ttu-id="0d583-127">Kliknij przycisk**编辑**(Edytuj) obok pola dla OAuth2.0**授权设置**(adres URL przekierowania).</span><span class="sxs-lookup"><span data-stu-id="0d583-127">Click **编辑** (edit) next to the field for OAuth2.0 **授权设置** (redirect URL).</span></span>
9. <span data-ttu-id="0d583-128">Wprowadź `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` dla OAuth2.0**授权设置**(adres URL przekierowania).</span><span class="sxs-lookup"><span data-stu-id="0d583-128">Enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp` for OAuth2.0 **授权设置** (redirect URL).</span></span> <span data-ttu-id="0d583-129">Na przykład jeśli Twoje `tenant_name` jest adres URL, który można ustawić contoso.onmicrosoft.com, `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="0d583-129">For example, if your `tenant_name` is contoso.onmicrosoft.com, set the URL to be `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
10. <span data-ttu-id="0d583-130">Kliknij przycisk**提交**(Prześlij).</span><span class="sxs-lookup"><span data-stu-id="0d583-130">Click **提交** (submit).</span></span>  

## <a name="configure-weibo-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="0d583-131">Skonfiguruj Weibo funkcję dostawcy tożsamości w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="0d583-131">Configure Weibo as an identity provider in your tenant</span></span>
1. <span data-ttu-id="0d583-132">Wykonaj następujące kroki, aby [przejdź do bloku funkcji B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0d583-132">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="0d583-133">W bloku funkcji B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="0d583-133">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="0d583-134">Kliknij pozycję **+Dodaj** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="0d583-134">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="0d583-135">Podaj przyjazną nazwę w polu **nazwa** konfiguracji dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="0d583-135">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="0d583-136">Wprowadź na przykład "Weibo".</span><span class="sxs-lookup"><span data-stu-id="0d583-136">For example, enter "Weibo".</span></span>
5. <span data-ttu-id="0d583-137">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Weibo**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0d583-137">Click **Identity provider type**, select **Weibo**, and click **OK**.</span></span>
6. <span data-ttu-id="0d583-138">Kliknij przycisk **skonfigurować ten dostawca tożsamości**</span><span class="sxs-lookup"><span data-stu-id="0d583-138">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="0d583-139">Wprowadź **klucz aplikacji** skopiowanego wcześniej jako **identyfikator klienta**.</span><span class="sxs-lookup"><span data-stu-id="0d583-139">Enter the **App Key** that you copied earlier as the **Client ID**.</span></span>
8. <span data-ttu-id="0d583-140">Wprowadź **klucz tajny aplikacji** skopiowanego wcześniej jako **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="0d583-140">Enter the **App Secret** that you copied earlier as the **Client Secret**.</span></span>
9. <span data-ttu-id="0d583-141">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** Aby zapisać konfigurację Weibo.</span><span class="sxs-lookup"><span data-stu-id="0d583-141">Click **OK** and then click **Create** to save your Weibo configuration.</span></span>

