---
title: "Usługa Azure Active Directory B2C: WeChat konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami WeChat w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: d2424c66-ba68-4d82-847e-d137683527b0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/26/2017
ms.author: parakhj
ms.openlocfilehash: 92cc3579d818d2379a503ccc695138b33a34466d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-wechat-accounts"></a><span data-ttu-id="b2a7b-103">Usługa Azure Active Directory B2C: Udostępnianie kont WeChat tooconsumers rejestracji i logowania</span><span class="sxs-lookup"><span data-stu-id="b2a7b-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with WeChat accounts</span></span>

> [!NOTE]
> <span data-ttu-id="b2a7b-104">Ta funkcja jest dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-104">This feature is in preview.</span></span>
> 

## <a name="create-a-wechat-application"></a><span data-ttu-id="b2a7b-105">Tworzenie aplikacji WeChat</span><span class="sxs-lookup"><span data-stu-id="b2a7b-105">Create a WeChat application</span></span>

<span data-ttu-id="b2a7b-106">toouse WeChat jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji WeChat i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-106">toouse WeChat as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a WeChat application and supply it with hello right parameters.</span></span> <span data-ttu-id="b2a7b-107">Toodo konta WeChat to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-107">You need a WeChat account toodo this.</span></span> <span data-ttu-id="b2a7b-108">Jeśli nie masz, możesz ją uzyskać, po zarejestrowaniu się za pomocą jednego z ich aplikacji mobilnych lub za pomocą numeru q.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-108">If you don’t have one, you can get one by signing up through one of their mobile apps or by using your QQ number.</span></span> <span data-ttu-id="b2a7b-109">Po wykonaniu tej Pobierz konta w zarejestrowany w programie dla deweloperów WeChat hello.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-109">After that, get your account registered with hello WeChat developer program.</span></span> <span data-ttu-id="b2a7b-110">Więcej informacji można znaleźć [tutaj](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span><span class="sxs-lookup"><span data-stu-id="b2a7b-110">You can find more information [here](http://kf.qq.com/faq/161220Brem2Q161220uUjERB.html).</span></span>

### <a name="register-a-wechat-application"></a><span data-ttu-id="b2a7b-111">Zarejestrować aplikację WeChat</span><span class="sxs-lookup"><span data-stu-id="b2a7b-111">Register a WeChat application</span></span>

1. <span data-ttu-id="b2a7b-112">Przejdź za[https://open.weixin.qq.com/](https://open.weixin.qq.com/) i zaloguj się.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-112">Go too[https://open.weixin.qq.com/](https://open.weixin.qq.com/) and log in.</span></span>
2. <span data-ttu-id="b2a7b-113">Polecenie**管理中心**(management center).</span><span class="sxs-lookup"><span data-stu-id="b2a7b-113">Click on **管理中心** (management center).</span></span>
3. <span data-ttu-id="b2a7b-114">Wykonaj tooregister niezbędne kroki hello nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-114">Follow hello necessary steps tooregister a new application.</span></span>
4. <span data-ttu-id="b2a7b-115">Aby uzyskać**授权回调域**(adres URL wywołania zwrotnego), wprowadź `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-115">For **授权回调域** (callback URL), enter `https://login.microsoftonline.com/te/{tenant_name}/oauth2/authresp`.</span></span> <span data-ttu-id="b2a7b-116">Na przykład jeśli Twoje `tenant_name` jest contoso.onmicrosoft.com, zestaw hello adresu URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-116">For example, if your `tenant_name` is contoso.onmicrosoft.com, set hello URL toobe `https://login.microsoftonline.com/te/contoso.onmicrosoft.com/oauth2/authresp`.</span></span>
5. <span data-ttu-id="b2a7b-117">Znajdź i skopiuj hello **identyfikator aplikacji** i **klucz aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-117">Find and copy hello **APP ID** and **APP KEY**.</span></span> <span data-ttu-id="b2a7b-118">Możesz będą one potrzebne później.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-118">You will need these later.</span></span>

## <a name="configure-wechat-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b2a7b-119">Skonfiguruj WeChat funkcję dostawcy tożsamości w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="b2a7b-119">Configure WeChat as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b2a7b-120">Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-120">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="b2a7b-121">W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-121">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b2a7b-122">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-122">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="b2a7b-123">Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-123">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="b2a7b-124">Wprowadź na przykład "WeChat".</span><span class="sxs-lookup"><span data-stu-id="b2a7b-124">For example, enter "WeChat".</span></span>
5. <span data-ttu-id="b2a7b-125">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **WeChat**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-125">Click **Identity provider type**, select **WeChat**, and click **OK**.</span></span>
6. <span data-ttu-id="b2a7b-126">Kliknij przycisk **skonfigurować ten dostawca tożsamości**</span><span class="sxs-lookup"><span data-stu-id="b2a7b-126">Click **Set up this identity provider**</span></span>
7. <span data-ttu-id="b2a7b-127">Wprowadź hello **klucz aplikacji** skopiowanego wcześniej jako hello **identyfikator klienta**.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-127">Enter hello **App Key** that you copied earlier as hello **Client ID**.</span></span>
8. <span data-ttu-id="b2a7b-128">Wprowadź hello **klucz tajny aplikacji** skopiowanego wcześniej jako hello **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-128">Enter hello **App Secret** that you copied earlier as hello **Client Secret**.</span></span>
9. <span data-ttu-id="b2a7b-129">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave WeChat konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b2a7b-129">Click **OK** and then click **Create** toosave your WeChat configuration.</span></span>

