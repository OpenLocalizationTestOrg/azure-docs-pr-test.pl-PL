---
title: 'Azure Active Directory B2C: Konfiguracja konta Microsoft | Dokumentacja firmy Microsoft'
description: "Przedstawić rejestracji i logowania użytkowników z kontami Microsoft w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
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
ms.openlocfilehash: 59879dc0b3fc1d7af3e2a1f67f1701f451de9126
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-microsoft-accounts"></a><span data-ttu-id="1cf74-103">Usługa Azure Active Directory B2C: Umożliwiają rejestracji i logowania użytkowników z kontami Microsoft</span><span class="sxs-lookup"><span data-stu-id="1cf74-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Microsoft accounts</span></span>
## <a name="create-a-microsoft-account-application"></a><span data-ttu-id="1cf74-104">Tworzenie aplikacji konta Microsoft</span><span class="sxs-lookup"><span data-stu-id="1cf74-104">Create a Microsoft account application</span></span>
<span data-ttu-id="1cf74-105">Do używania konta Microsoft jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy utworzyć aplikację konta Microsoft i dostarczyć prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="1cf74-105">To use Microsoft account as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Microsoft account application and supply it with the right parameters.</span></span> <span data-ttu-id="1cf74-106">Musisz mieć konto Microsoft, w tym celu.</span><span class="sxs-lookup"><span data-stu-id="1cf74-106">You need a Microsoft account to do this.</span></span> <span data-ttu-id="1cf74-107">Jeśli nie masz, możesz pobrać go w [https://www.live.com/](https://www.live.com/).</span><span class="sxs-lookup"><span data-stu-id="1cf74-107">If you don’t have one, you can get it at [https://www.live.com/](https://www.live.com/).</span></span>

1. <span data-ttu-id="1cf74-108">Przejdź do [portalu rejestracji aplikacji Microsoft](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) i zaloguj się przy użyciu poświadczeń konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1cf74-108">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) and sign in with your Microsoft account credentials.</span></span>
2. <span data-ttu-id="1cf74-109">Kliknij przycisk **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="1cf74-109">Click **Add an app**.</span></span>
   
    ![Microsoft konta — Dodawanie nowej aplikacji](./media/active-directory-b2c-setup-msa-app/msa-add-new-app.png)
3. <span data-ttu-id="1cf74-111">Podaj **nazwa** dla aplikacji i kliknij przycisk **tworzenie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1cf74-111">Provide a **Name** for your application and click **Create application**.</span></span>
   
    ![Konto Microsoft — Nazwa aplikacji](./media/active-directory-b2c-setup-msa-app/msa-app-name.png)
4. <span data-ttu-id="1cf74-113">Skopiuj wartość **identyfikator aplikacji**. Należy go skonfigurować konto Microsoft jako dostawca tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="1cf74-113">Copy the value of **Application Id**. You will need it to configure Microsoft account as an identity provider in your tenant.</span></span>
   
    ![Konto Microsoft — identyfikator aplikacji](./media/active-directory-b2c-setup-msa-app/msa-app-id.png)
5. <span data-ttu-id="1cf74-115">Polecenie **platformy Dodaj** i wybierz polecenie **Web**.</span><span class="sxs-lookup"><span data-stu-id="1cf74-115">Click on **Add platform** and choose **Web**.</span></span>
   
    ![Microsoft konta — Dodawanie platformy](./media/active-directory-b2c-setup-msa-app/msa-add-platform.png)
   
    ![Konto Microsoft — sieci Web](./media/active-directory-b2c-setup-msa-app/msa-web.png)
6. <span data-ttu-id="1cf74-118">Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w **identyfikator URI przekierowania** pola.</span><span class="sxs-lookup"><span data-stu-id="1cf74-118">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Redirect URIs** field.</span></span> <span data-ttu-id="1cf74-119">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="1cf74-119">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
   
    ![Konto Microsoft — adres URL przekierowania](./media/active-directory-b2c-setup-msa-app/msa-redirect-url.png)
7. <span data-ttu-id="1cf74-121">Polecenie **wygenerować nowe hasło** w obszarze **klucze tajne aplikacji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1cf74-121">Click on **Generate New Password** under the **Application Secrets** section.</span></span> <span data-ttu-id="1cf74-122">Skopiuj nowe hasło, które są wyświetlane na ekranie.</span><span class="sxs-lookup"><span data-stu-id="1cf74-122">Copy the new password displayed on screen.</span></span> <span data-ttu-id="1cf74-123">Należy go skonfigurować konto Microsoft jako dostawca tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="1cf74-123">You will need it to configure Microsoft account as an identity provider in your tenant.</span></span> <span data-ttu-id="1cf74-124">To hasło jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="1cf74-124">This password is an important security credential.</span></span>
   
    ![Microsoft konta — wygenerować nowe hasło](./media/active-directory-b2c-setup-msa-app/msa-generate-new-password.png)
   
    ![Konto Microsoft — nowe hasło](./media/active-directory-b2c-setup-msa-app/msa-new-password.png)
8. <span data-ttu-id="1cf74-127">Sprawdź pole **Obsługa zestaw Live SDK** w obszarze **zaawansowane opcje** sekcji.</span><span class="sxs-lookup"><span data-stu-id="1cf74-127">Check the box that says **Live SDK support** under the **Advanced Options** section.</span></span> <span data-ttu-id="1cf74-128">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="1cf74-128">Click **Save**.</span></span>
   
    ![Konto Microsoft — Obsługa zestaw Live SDK](./media/active-directory-b2c-setup-msa-app/msa-live-sdk-support.png)

## <a name="configure-microsoft-account-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="1cf74-130">Skonfiguruj konto Microsoft jako dostawca tożsamości w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="1cf74-130">Configure Microsoft account as an identity provider in your tenant</span></span>
1. <span data-ttu-id="1cf74-131">Wykonaj następujące kroki, aby [przejdź do bloku funkcji B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1cf74-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="1cf74-132">W bloku funkcji B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="1cf74-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="1cf74-133">Kliknij pozycję **+Dodaj** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="1cf74-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="1cf74-134">Podaj przyjazną nazwę w polu **nazwa** konfiguracji dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="1cf74-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="1cf74-135">Wprowadź na przykład "MSA".</span><span class="sxs-lookup"><span data-stu-id="1cf74-135">For example, enter "MSA".</span></span>
5. <span data-ttu-id="1cf74-136">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **konta Microsoft**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1cf74-136">Click **Identity provider type**, select **Microsoft account**, and click **OK**.</span></span>
6. <span data-ttu-id="1cf74-137">Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź identyfikator aplikacji i hasło utworzone wcześniej aplikacji konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1cf74-137">Click **Set up this identity provider** and enter the Application Id and password of the Microsoft account application that you created earlier.</span></span>
7. <span data-ttu-id="1cf74-138">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** można zapisać konfiguracji konta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="1cf74-138">Click **OK** and then click **Create** to save your Microsoft account configuration.</span></span>

