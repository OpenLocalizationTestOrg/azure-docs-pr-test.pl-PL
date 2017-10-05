---
title: "Usługa Azure Active Directory B2C: Google + konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj rejestracji i logowania klientom korzystającym z konta Google + w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
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
ms.openlocfilehash: 6ab73e5c79742ab548733f5712dee1e28461db9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-google-accounts"></a><span data-ttu-id="4ac09-103">Usługa Azure Active Directory B2C: Umożliwiają rejestracji i logowania użytkowników z konta Google +</span><span class="sxs-lookup"><span data-stu-id="4ac09-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Google+ accounts</span></span>
## <a name="create-a-google-application"></a><span data-ttu-id="4ac09-104">Tworzenie aplikacji Google +</span><span class="sxs-lookup"><span data-stu-id="4ac09-104">Create a Google+ application</span></span>
<span data-ttu-id="4ac09-105">Aby użyć Google + jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy do utworzenia aplikacji Google + i dostarczyć prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="4ac09-105">To use Google+ as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a Google+ application and supply it with the right parameters.</span></span> <span data-ttu-id="4ac09-106">Musisz mieć konto Google + w tym celu.</span><span class="sxs-lookup"><span data-stu-id="4ac09-106">You need a Google+ account to do this.</span></span> <span data-ttu-id="4ac09-107">Jeśli nie masz, możesz pobrać go w [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span><span class="sxs-lookup"><span data-stu-id="4ac09-107">If you don’t have one, you can get it at [https://accounts.google.com/SignUp](https://accounts.google.com/SignUp).</span></span>

1. <span data-ttu-id="4ac09-108">Przejdź do [konsoli deweloperów Google](https://console.developers.google.com/) i zaloguj się przy użyciu poświadczeń konta Google +.</span><span class="sxs-lookup"><span data-stu-id="4ac09-108">Go to the [Google Developers Console](https://console.developers.google.com/) and sign in with your Google+ account credentials.</span></span>
2. <span data-ttu-id="4ac09-109">Kliknij przycisk **Tworzenie projektu**, wprowadź **Nazwa projektu**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4ac09-109">Click **Create project**, enter a **Project name**, and then click **Create**.</span></span>
   
    ![Google + — wprowadzenie](./media/active-directory-b2c-setup-goog-app/google-get-started.png)
   
    ![Google + — nowy projekt](./media/active-directory-b2c-setup-goog-app/google-new-project.png)
3. <span data-ttu-id="4ac09-112">Kliknij przycisk **Menedżer interfejsu API** , a następnie kliknij przycisk **poświadczenia** na lewym pasku nawigacyjnym.</span><span class="sxs-lookup"><span data-stu-id="4ac09-112">Click **API Manager** and then click **Credentials** in the left navigation.</span></span>
4. <span data-ttu-id="4ac09-113">Kliknij przycisk **ekranu zgoda OAuth** u góry.</span><span class="sxs-lookup"><span data-stu-id="4ac09-113">Click the **OAuth consent screen** tab at the top.</span></span>
   
    ![Google + - poświadczeń](./media/active-directory-b2c-setup-goog-app/google-add-cred.png)
5. <span data-ttu-id="4ac09-115">Wybierz lub określ prawidłowe **adres E-mail**, podaj **nazwa produktu**i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="4ac09-115">Select or specify a valid **Email address**, provide a **Product name**, and click **Save**.</span></span>
   
    ![Google + - ekranu zgoda OAuth](./media/active-directory-b2c-setup-goog-app/google-consent-screen.png)
6. <span data-ttu-id="4ac09-117">Kliknij przycisk **nowe poświadczenia** , a następnie wybierz **identyfikator klienta OAuth**.</span><span class="sxs-lookup"><span data-stu-id="4ac09-117">Click **New credentials** and then choose **OAuth client ID**.</span></span>
   
    ![Google + - ekranu zgoda OAuth](./media/active-directory-b2c-setup-goog-app/google-add-oauth2-client-id.png)
7. <span data-ttu-id="4ac09-119">W obszarze **typu aplikacji**, wybierz pozycję **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="4ac09-119">Under **Application type**, select **Web application**.</span></span>
   
    ![Google + - ekranu zgoda OAuth](./media/active-directory-b2c-setup-goog-app/google-web-app.png)
8. <span data-ttu-id="4ac09-121">Podaj **nazwa** dla aplikacji, wprowadź `https://login.microsoftonline.com` w **źródeł autoryzowany JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w **autoryzowanych przekierowania URI** pola.</span><span class="sxs-lookup"><span data-stu-id="4ac09-121">Provide a **Name** for your application, enter `https://login.microsoftonline.com` in the **Authorized JavaScript origins** field, and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized redirect URIs** field.</span></span> <span data-ttu-id="4ac09-122">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="4ac09-122">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="4ac09-123">**{Dzierżawa}** wartość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="4ac09-123">The **{tenant}** value is case-sensitive.</span></span> <span data-ttu-id="4ac09-124">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4ac09-124">Click **Create**.</span></span>
   
    ![Google + - Utwórz identyfikator klienta](./media/active-directory-b2c-setup-goog-app/google-create-client-id.png)
9. <span data-ttu-id="4ac09-126">Skopiuj wartości z **identyfikator klienta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="4ac09-126">Copy the values of **Client ID** and **Client secret**.</span></span> <span data-ttu-id="4ac09-127">Należy ich skonfigurowanie Google + funkcję dostawcy tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="4ac09-127">You will need both of them to configure Google+ as an identity provider in your tenant.</span></span> <span data-ttu-id="4ac09-128">**Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4ac09-128">**Client secret** is an important security credential.</span></span>
   
    ![Google + - klucz tajny klienta](./media/active-directory-b2c-setup-goog-app/google-client-secret.png)

## <a name="configure-google-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="4ac09-130">Skonfiguruj Google + funkcję dostawcy tożsamości w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="4ac09-130">Configure Google+ as an identity provider in your tenant</span></span>
1. <span data-ttu-id="4ac09-131">Wykonaj następujące kroki, aby [przejdź do bloku funkcji B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="4ac09-131">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="4ac09-132">W bloku funkcji B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="4ac09-132">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="4ac09-133">Kliknij pozycję **+Dodaj** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="4ac09-133">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="4ac09-134">Podaj przyjazną nazwę w polu **nazwa** konfiguracji dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="4ac09-134">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="4ac09-135">Na przykład wprowadź "G +".</span><span class="sxs-lookup"><span data-stu-id="4ac09-135">For example, enter "G+".</span></span>
5. <span data-ttu-id="4ac09-136">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Google**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ac09-136">Click **Identity provider type**, select **Google**, and click **OK**.</span></span>
6. <span data-ttu-id="4ac09-137">Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź identyfikator klienta i klucz tajny klienta aplikacji Google + utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="4ac09-137">Click **Set up this identity provider** and enter the client ID and client secret of the Google+ application that you created earlier.</span></span>
7. <span data-ttu-id="4ac09-138">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** Aby zapisać konfigurację Google +.</span><span class="sxs-lookup"><span data-stu-id="4ac09-138">Click **OK** and then click **Create** to save your Google+ configuration.</span></span>

