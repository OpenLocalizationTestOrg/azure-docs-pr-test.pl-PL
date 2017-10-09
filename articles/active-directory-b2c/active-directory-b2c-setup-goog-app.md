---
title: "Usługa Azure Active Directory B2C: Google + konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z konta Google + w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 4dcca66f-29e4-4b4d-8840-50baad736bd7
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6ef66eb17777acd95b5f4745ed6097c77e37663b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-google-accounts"></a><span data-ttu-id="d0a66-103">Usługa Azure Active Directory B2C: Udostępnianie kont Google + tooconsumers rejestracji i logowania</span><span class="sxs-lookup"><span data-stu-id="d0a66-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="d0a66-104">Tworzenie aplikacji Google +</span><span class="sxs-lookup"><span data-stu-id="d0a66-104">Create a Google+ application</span></span>
<span data-ttu-id="d0a66-105">toouse Google + jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji Google + i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="d0a66-105">toouse Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Google+ application and supply it with hello right parameters.</span></span> <span data-ttu-id="d0a66-106">Toodo konto Google + to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d0a66-106">You need a Google+ account toodo this.</span></span> <span data-ttu-id="d0a66-107">Jeśli nie masz, możesz pobrać go w [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="d0a66-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="d0a66-108">Przejdź toohello [konsoli deweloperów Google](https://console.developers.google.com/) i zaloguj się przy użyciu poświadczeń konta Google +.</span><span class="sxs-lookup"><span data-stu-id="d0a66-108">Go toohello [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="d0a66-109">Kliknij przycisk **Tworzenie projektu**, wprowadź **Nazwa projektu**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google + — wprowadzenie](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google + — nowy projekt](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="d0a66-112">Kliknij przycisk **Menedżer interfejsu API** , a następnie kliknij przycisk **poświadczenia** w hello lewy pasek nawigacyjny.</span><span class="sxs-lookup"><span data-stu-id="d0a66-112">Click **API Manager** and then click **Credentials** in hello left navigation.</span></span>
4. <span data-ttu-id="d0a66-113">Kliknij przycisk hello **ekranu zgoda OAuth** u góry hello.</span><span class="sxs-lookup"><span data-stu-id="d0a66-113">Click hello **OAuth consent screen** tab at hello top.</span></span>
   
    ![Google + - poświadczeń](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="d0a66-115">Wybierz lub określ prawidłowe **adres E-mail**, podaj **nazwa produktu**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google + - ekranu zgoda OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="d0a66-117">Kliknij przycisk **nowe poświadczenia** , a następnie wybierz **identyfikator klienta OAuth**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google + - ekranu zgoda OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="d0a66-119">W obszarze **typu aplikacji**, wybierz pozycję **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google + - ekranu zgoda OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="d0a66-121">Podaj **nazwa** dla aplikacji, wprowadź `https://login.microsoftonline.com` w hello **źródeł autoryzowany JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **autoryzowanych przekierowania URI**pola.</span><span class="sxs-lookup"><span data-stu-id="d0a66-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in hello **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized redirect URIs** field.</span></span> <span data-ttu-id="d0a66-122">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="d0a66-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="d0a66-123">Witaj **{dzierżawa}** wartość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d0a66-123">hello **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="d0a66-124">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-124">Click **Create**.</span></span>
   
    ![Google + - Utwórz identyfikator klienta](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="d0a66-126">Skopiuj wartości hello **identyfikator klienta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-126">Copy hello values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="d0a66-127">Konieczne będzie ich tooconfigure Google + funkcję dostawcy tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="d0a66-127">You will need both of them tooconfigure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="d0a66-128">**Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d0a66-128">**Client secret** is an important security credential.</span></span>
   
    ![Google + - klucz tajny klienta](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d0a66-130">Skonfiguruj Google + funkcję dostawcy tożsamości w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="d0a66-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d0a66-131">Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d0a66-131">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="d0a66-132">W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-132">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d0a66-133">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="d0a66-133">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="d0a66-134">Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d0a66-134">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="d0a66-135">Na przykład wprowadź "G +".</span><span class="sxs-lookup"><span data-stu-id="d0a66-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="d0a66-136">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Google**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d0a66-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="d0a66-137">Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello identyfikator i klienta klucz tajny klienta hello Google + aplikacji, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d0a66-137">Click **Set up this identity provider** and enter hello client ID and client secret of hello Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="d0a66-138">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfiguracji Google +.</span><span class="sxs-lookup"><span data-stu-id="d0a66-138">Click **OK** and then click **Create** toosave your Google+ configuration.</span></span>

