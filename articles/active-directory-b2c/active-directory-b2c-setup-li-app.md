---
title: "Usługa Azure Active Directory B2C: LinkedIn konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami LinkedIn w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: fa51a16b-9ce9-4e27-9eff-0869b4c4f0ef
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 6c5233ef48b24968fd6383f470b5d8a969a78ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-linkedin-accounts"></a><span data-ttu-id="80bc5-103">Usługa Azure Active Directory B2C: Udostępnianie kont LinkedIn tooconsumers rejestracji i logowania</span><span class="sxs-lookup"><span data-stu-id="80bc5-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="80bc5-104">Tworzenie aplikacji LinkedIn</span><span class="sxs-lookup"><span data-stu-id="80bc5-104">Create a LinkedIn application</span></span>
<span data-ttu-id="80bc5-105">toouse LinkedIn jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji LinkedIn i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="80bc5-105">toouse LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a LinkedIn application and supply it with hello right parameters.</span></span> <span data-ttu-id="80bc5-106">Toodo konta LinkedIn to konieczne.</span><span class="sxs-lookup"><span data-stu-id="80bc5-106">You need a LinkedIn account toodo this.</span></span> <span data-ttu-id="80bc5-107">Jeśli nie masz, możesz pobrać go w [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="80bc5-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="80bc5-108">Przejdź toohello [deweloperzy LinkedIn witryny sieci Web](https://www.developer.linkedin.com/) i zaloguj się przy użyciu poświadczeń konta LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="80bc5-108">Go toohello [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="80bc5-109">Kliknij przycisk **Moje aplikacje** w hello paska menu u góry, a następnie kliknij przycisk **tworzenie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="80bc5-109">Click **My Apps** in hello top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn — nowej aplikacji](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="80bc5-111">W hello **Utwórz nową aplikację** tworzą, wprowadź odpowiednie informacje hello (**nazwa firmy**, **nazwa**, **opis**, **Adres URL Logo aplikacji**, **stosowania**, **adres URL witryny sieci Web**, **służbowy adres E-mail** i **Telefon służbowy**).</span><span class="sxs-lookup"><span data-stu-id="80bc5-111">In hello **Create a New Application** form, fill in hello relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="80bc5-112">Akceptuję toohello **LinkedIn interfejsu API warunki użytkowania** i kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="80bc5-112">Agree toohello **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - rejestrowania aplikacji](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="80bc5-114">Skopiuj wartości hello **identyfikator klienta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="80bc5-114">Copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="80bc5-115">(Można znaleźć je w obszarze **klucze uwierzytelniania**.) Konieczne będzie ich tooconfigure LinkedIn funkcję dostawcy tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="80bc5-115">(You can find them under **Authentication Keys**.) You will need both of them tooconfigure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="80bc5-116">**Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="80bc5-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="80bc5-117">Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **autoryzacji adresów URL przekierowań** pola (w obszarze **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="80bc5-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="80bc5-118">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (np. contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="80bc5-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="80bc5-119">Kliknij przycisk **Dodaj**, a następnie kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="80bc5-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="80bc5-120">Witaj **{dzierżawa}** wartość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="80bc5-120">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn — ustawienia aplikacji](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="80bc5-122">Skonfiguruj LinkedIn funkcję dostawcy tożsamości w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="80bc5-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="80bc5-123">Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="80bc5-123">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="80bc5-124">W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="80bc5-124">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="80bc5-125">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="80bc5-125">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="80bc5-126">Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="80bc5-126">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="80bc5-127">Wprowadź na przykład "LI".</span><span class="sxs-lookup"><span data-stu-id="80bc5-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="80bc5-128">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **LinkedIn**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="80bc5-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="80bc5-129">Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello identyfikator i klienta klucz tajny klienta hello LinkedIn aplikacji, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="80bc5-129">Click **Set up this identity provider** and enter hello client ID and client secret of hello LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="80bc5-130">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfiguracji LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="80bc5-130">Click **OK** and then click **Create** toosave your LinkedIn configuration.</span></span>

