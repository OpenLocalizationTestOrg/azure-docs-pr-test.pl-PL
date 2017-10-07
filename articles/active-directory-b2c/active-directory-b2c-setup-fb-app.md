---
title: "Usługa Azure Active Directory B2C: Konfiguracja usługi Facebook | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami usługi Facebook w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: sromeroz
manager: krassk
editor: sromeroz
ms.assetid: b875f235-a1d2-4abb-b9f0-b89beac38a32
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/7/2017
ms.author: sromeroz
ms.openlocfilehash: 4c3b79c7248bd1e789bf33fc467abb27d0170edd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-facebook-accounts"></a><span data-ttu-id="d2ae8-103">Usługa Azure Active Directory B2C: Podaj tooconsumers rejestracji i logowania z kontami usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="d2ae8-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Facebook accounts</span></span>
## <a name="create-a-facebook-application"></a><span data-ttu-id="d2ae8-104">Tworzenie aplikacji usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="d2ae8-104">Create a Facebook application</span></span>
<span data-ttu-id="d2ae8-105">toouse usługi Facebook jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji usługi Facebook i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-105">toouse Facebook as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Facebook application and supply it with hello right parameters.</span></span> <span data-ttu-id="d2ae8-106">Niezbędne toodo konto serwisu Facebook.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-106">You need a Facebook account toodo this.</span></span> <span data-ttu-id="d2ae8-107">Jeśli nie masz, możesz pobrać go w [https://www.facebook.com/](https://www.facebook.com/).</span><span class="sxs-lookup"><span data-stu-id="d2ae8-107">If you don’t have one, you can get it at [https://www.facebook.com/](https://www.facebook.com/).</span></span>

1. <span data-ttu-id="d2ae8-108">Przejdź toohello [Facebook dla deweloperów](https://developers.facebook.com/) poświadczenia konta witryny sieci Web i zaloguj się przy użyciu Twojej usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-108">Go toohello [Facebook for developers](https://developers.facebook.com/) website and sign in with your Facebook account credentials.</span></span>
2. <span data-ttu-id="d2ae8-109">Jeśli nie zostało to jeszcze zrobione, należy tooregister jako deweloper usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-109">If you have not already done so, you need tooregister as a Facebook developer.</span></span> <span data-ttu-id="d2ae8-110">toodo tego, kliknij **zarejestrować** (na powitania prawym górnym rogu strony hello), Zaakceptuj zasady w serwisie Facebook i wykonaj kroki rejestracji hello.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-110">toodo this, click **Register** (on hello upper-right corner of hello page), accept Facebook's policies, and complete hello registration steps.</span></span>
3. <span data-ttu-id="d2ae8-111">Kliknij przycisk **Moje aplikacje** , a następnie kliknij przycisk **Dodaj nową aplikację**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-111">Click **My Apps** and then click **Add a New App**.</span></span> 
4. <span data-ttu-id="d2ae8-112">W formularzu hello podaj **Nazwa wyświetlana** i prawidłowy **E-mail kontaktu**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-112">In hello form, provide a **Display Name** and a valid **Contact Email**.</span></span>
5. <span data-ttu-id="d2ae8-113">Kliknij przycisk **utworzyć identyfikator aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-113">Click **Create App ID**.</span></span> <span data-ttu-id="d2ae8-114">Może wymagać tooaccept Facebook platformy zasad i ukończyć sprawdzania zabezpieczeń w trybie online.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-114">This may require you tooaccept Facebook platform policies and complete an online security check.</span></span>
6. <span data-ttu-id="d2ae8-115">W kolumnie po lewej stronie powitania kliknij **ustawienia** , a następnie wybierz **podstawowe** Jeśli nie jest już wybrana.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-115">In hello left column, click **Settings** and then select **Basic** if not selected already.</span></span>
7. <span data-ttu-id="d2ae8-116">Wybierz **kategorii**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-116">Select a **Category**.</span></span> 
8. <span data-ttu-id="d2ae8-117">Kliknij przycisk **+ Dodaj platformy** i wybierz **witryny sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-117">Click **+ Add Platform** and select **Website**.</span></span>
   
    ![Facebook — ustawienia](./media/active-directory-b2c-setup-fb-app/fb-settings.png)
   
    ![Facebook — ustawienia — witryny sieci Web](./media/active-directory-b2c-setup-fb-app/fb-website.png)
9. <span data-ttu-id="d2ae8-120">Wprowadź `https://login.microsoftonline.com/` w hello **adres URL witryny** pola, a następnie kliknij przycisk **Zapisz zmiany** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-120">Enter `https://login.microsoftonline.com/` in hello **Site URL** field and then click **Save Changes** at hello bottom of hello page.</span></span>
   
    ![Facebook — adres URL witryny](./media/active-directory-b2c-setup-fb-app/fb-site-url.png)

10. <span data-ttu-id="d2ae8-122">Skopiuj wartość hello **identyfikator aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-122">Copy hello value of **App ID**.</span></span> <span data-ttu-id="d2ae8-123">Kliknij przycisk **Pokaż** i skopiuj wartość hello **klucz tajny aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-123">Click **Show** and copy hello value of **App Secret**.</span></span> <span data-ttu-id="d2ae8-124">Konieczne będzie ich tooconfigure usługi Facebook jako dostawca tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-124">You will need both of them tooconfigure Facebook as an identity provider in your tenant.</span></span> <span data-ttu-id="d2ae8-125">**Klucz tajny aplikacji** jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-125">**App Secret** is an important security credential.</span></span>
   
    ![Facebook - ID aplikacji i klucz tajny aplikacji](./media/active-directory-b2c-setup-fb-app/fb-app-id-app-secret.png)
11. <span data-ttu-id="d2ae8-127">Kliknij przycisk **+ Dodaj produktu** na hello nawigacji po lewej stronie, a następnie hello **Set Up** przycisk dla **logowania serwisu Facebook**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-127">Click **+ Add Product** on hello left navigation and then hello **Set Up** button for **Facebook Login**.</span></span>
   
    ![Facebook - logowania usługi Facebook](./media/active-directory-b2c-setup-fb-app/fb-login.png)
12. <span data-ttu-id="d2ae8-129">Kliknij przycisk **ustawienia** na powitania prawo nawigacji w obszarze **logowania usługi Facebook**</span><span class="sxs-lookup"><span data-stu-id="d2ae8-129">Click **Settings** on hello right nav under **Facebook Login**</span></span>

    ![Facebook — ustawienia logowania usługi Facebook](./media/active-directory-b2c-setup-fb-app/fb-login-settings.png)
13. <span data-ttu-id="d2ae8-131">Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **prawidłowy OAuth przekierowania URI** w hello **ustawień klienta OAuth** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-131">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Valid OAuth redirect URIs** field in hello **Client OAuth Settings** section.</span></span> <span data-ttu-id="d2ae8-132">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="d2ae8-132">Replace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span> <span data-ttu-id="d2ae8-133">Kliknij przycisk **Zapisz zmiany** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-133">Click **Save Changes** at hello bottom of hello page.</span></span>
    
    ![Facebook — identyfikator URI przekierowania uwierzytelniania OAuth](./media/active-directory-b2c-setup-fb-app/fb-oauth-redirect-uri.png)
14. <span data-ttu-id="d2ae8-135">toomake aplikacji usługi Facebook mogą być używane przez usługi Azure AD B2C, należy toomake go publicznie dostępne.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-135">toomake your Facebook application usable by Azure AD B2C, you need toomake it publicly available.</span></span> <span data-ttu-id="d2ae8-136">Można to zrobić, klikając **aplikacji przejrzyj** hello lewy pasek nawigacyjny i przez włączenie hello przełącznika u góry strony hello hello zbyt**tak** i klikając **Potwierdź**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-136">You can do this by clicking **App Review** on hello left navigation and by turning hello switch at hello top of hello page too**YES** and clicking **Confirm**.</span></span>
    
    ![Facebook - publicznego aplikacji](./media/active-directory-b2c-setup-fb-app/fb-app-public.png)

## <a name="configure-facebook-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="d2ae8-138">Skonfiguruj funkcję dostawcy tożsamości w dzierżawie usługi Facebook</span><span class="sxs-lookup"><span data-stu-id="d2ae8-138">Configure Facebook as an identity provider in your tenant</span></span>
1. <span data-ttu-id="d2ae8-139">Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-139">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="d2ae8-140">W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-140">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="d2ae8-141">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-141">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="d2ae8-142">Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-142">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="d2ae8-143">Wprowadź na przykład "Facebook".</span><span class="sxs-lookup"><span data-stu-id="d2ae8-143">For example, enter "Facebook".</span></span>
5. <span data-ttu-id="d2ae8-144">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Facebook**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-144">Click **Identity provider type**, select **Facebook**, and click **OK**.</span></span>
6. <span data-ttu-id="d2ae8-145">Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello identyfikator i aplikacji klucz tajny aplikacji (of hello aplikacji usługi Facebook, który został utworzony wcześniej) w hello **identyfikator klienta** i **klucz tajny klienta**odpowiednio pola.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-145">Click **Set up this identity provider** and enter hello app ID and app secret (of hello Facebook application that you created earlier) in hello **Client ID** and **Client secret** fields respectively.</span></span>
7. <span data-ttu-id="d2ae8-146">Kliknij przycisk **OK**, a następnie kliknij przycisk **Utwórz** toosave konfigurację usługi Facebook.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-146">Click **OK**, and then click **Create** toosave your Facebook configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="d2ae8-147">Dodawanie **dostawcy tożsamości** tooyour dzierżawy nie modyfikuje istniejących zasad.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-147">Adding an **Identity provider** tooyour tenant does not modify your existing policies.</span></span> <span data-ttu-id="d2ae8-148">Należy pamiętać tooupdate zasad, umieszczając w niej hello dostawcy tożsamości, utworzony.</span><span class="sxs-lookup"><span data-stu-id="d2ae8-148">Remember tooupdate your policies by including hello identity provider you just created.</span></span>
>