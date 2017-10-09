---
title: 'Azure Active Directory B2C: Konfiguracja konta Microsoft | Dokumentacja firmy Microsoft'
description: "Podaj tooconsumers rejestracji i logowania z konta Microsoft w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 06407322-142c-4cb3-9106-a8d752c4c853
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: bec4777f003c459030f68c35b24f0e4bcddf84ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-microsoft-accounts"></a><span data-ttu-id="b26c5-103">Usługa Azure Active Directory B2C: Udostępnianie tooconsumers rejestracji i logowania kont Microsoft</span><span class="sxs-lookup"><span data-stu-id="b26c5-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="b26c5-104">Tworzenie aplikacji konta Microsoft</span><span class="sxs-lookup"><span data-stu-id="b26c5-104">Create a Microsoft account application</span></span>
<span data-ttu-id="b26c5-105">toouse konta Microsoft, funkcję dostawcy tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji konta Microsoft i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="b26c5-105">toouse Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Microsoft account application and supply it with hello right parameters.</span></span> <span data-ttu-id="b26c5-106">Toodo konto Microsoft to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b26c5-106">You need a Microsoft account toodo this.</span></span> <span data-ttu-id="b26c5-107">Jeśli nie masz, możesz pobrać go w [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="b26c5-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="b26c5-108">Przejdź toohello [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) i zaloguj się przy użyciu poświadczeń konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b26c5-108">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="b26c5-109">Kliknij przycisk **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="b26c5-109">Click **Add an app**.</span></span>
   
    ![Microsoft konta — Dodawanie nowej aplikacji](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="b26c5-111">Podaj **nazwa** dla aplikacji i kliknij przycisk **tworzenie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="b26c5-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Konto Microsoft — Nazwa aplikacji](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="b26c5-113">Skopiuj wartość hello **identyfikator aplikacji**. Będzie potrzebny tooconfigure konto Microsoft jako dostawca tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="b26c5-113">Copy hello value of **Application Id**. You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Konto Microsoft — identyfikator aplikacji](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="b26c5-115">Polecenie **platformy Dodaj** i wybierz polecenie **Web**.</span><span class="sxs-lookup"><span data-stu-id="b26c5-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft konta — Dodawanie platformy](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Konto Microsoft — sieci Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="b26c5-118">Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **identyfikator URI przekierowania** pola.</span><span class="sxs-lookup"><span data-stu-id="b26c5-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Redirect URIs** field.</span></span> <span data-ttu-id="b26c5-119">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="b26c5-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Konto Microsoft — adres URL przekierowania](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="b26c5-121">Polecenie **wygenerować nowe hasło** w obszarze hello **klucze tajne aplikacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b26c5-121">Click on **Generate New Password** under hello **Application Secrets** section.</span></span> <span data-ttu-id="b26c5-122">Skopiuj nowe hasło hello wyświetlany na ekranie.</span><span class="sxs-lookup"><span data-stu-id="b26c5-122">Copy hello new password displayed on screen.</span></span> <span data-ttu-id="b26c5-123">Będzie potrzebny tooconfigure konto Microsoft jako dostawca tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="b26c5-123">You will need it tooconfigure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="b26c5-124">To hasło jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="b26c5-124">This password is an important security credential.</span></span>
   
    ![Microsoft konta — wygenerować nowe hasło](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Konto Microsoft — nowe hasło](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="b26c5-127">Witaj opcję **Obsługa zestaw Live SDK** w obszarze hello **zaawansowane opcje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b26c5-127">Check hello box that says **Live SDK support** under hello **Advanced Options** section.</span></span> <span data-ttu-id="b26c5-128">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b26c5-128">Click **Save**.</span></span>
   
    ![Konto Microsoft — Obsługa zestaw Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="b26c5-130">Skonfiguruj konto Microsoft jako dostawca tożsamości w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="b26c5-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="b26c5-131">Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b26c5-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="b26c5-132">W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="b26c5-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="b26c5-133">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="b26c5-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="b26c5-134">Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b26c5-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="b26c5-135">Wprowadź na przykład "MSA".</span><span class="sxs-lookup"><span data-stu-id="b26c5-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="b26c5-136">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **konta Microsoft**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b26c5-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="b26c5-137">Kliknij przycisk **skonfigurować ten dostawca tożsamości** i wprowadź identyfikator aplikacji hello oraz hasło hello aplikacji konta Microsoft, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="b26c5-137">Click **Set up this identity provider** and enter hello Application Id and password of hello Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="b26c5-138">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfiguracji konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b26c5-138">Click **OK** and then click **Create** toosave your Microsoft account configuration.</span></span>

