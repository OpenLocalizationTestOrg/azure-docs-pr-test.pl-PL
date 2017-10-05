---
title: "Usługa Azure Active Directory B2C: LinkedIn konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj rejestracji i logowania klientom korzystającym z kontami LinkedIn w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C"
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
ms.openlocfilehash: 1a6c4b19261aa34e668554ccad2b6340cddf9bf5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-linkedin-accounts"></a><span data-ttu-id="dddc2-103">Azure Active Directory B2C: Umożliwiają tworzenie kont i logowania użytkowników z kontami LinkedIn</span><span class="sxs-lookup"><span data-stu-id="dddc2-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with LinkedIn accounts</span></span>
## <a name="create-a-linkedin-application"></a><span data-ttu-id="dddc2-104">Tworzenie aplikacji LinkedIn</span><span class="sxs-lookup"><span data-stu-id="dddc2-104">Create a LinkedIn application</span></span>
<span data-ttu-id="dddc2-105">Aby użyć LinkedIn jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy utworzyć aplikację LinkedIn i dostarczyć prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="dddc2-105">To use LinkedIn as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create a LinkedIn application and supply it with the right parameters.</span></span> <span data-ttu-id="dddc2-106">Należy to zrobić przy użyciu konta LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="dddc2-106">You need a LinkedIn account to do this.</span></span> <span data-ttu-id="dddc2-107">Jeśli nie masz, możesz pobrać go w [https://www.linkedin.com/](https://www.linkedin.com/).</span><span class="sxs-lookup"><span data-stu-id="dddc2-107">If you don’t have one, you can get it at [https://www.linkedin.com/](https://www.linkedin.com/).</span></span>

1. <span data-ttu-id="dddc2-108">Przejdź do [deweloperzy LinkedIn witryny sieci Web](https://www.developer.linkedin.com/) i zaloguj się przy użyciu poświadczeń konta LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="dddc2-108">Go to the [LinkedIn Developers website](https://www.developer.linkedin.com/) and sign in with your LinkedIn account credentials.</span></span>
2. <span data-ttu-id="dddc2-109">Kliknij przycisk **Moje aplikacje** paska menu u góry, a następnie kliknij polecenie **tworzenie aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="dddc2-109">Click **My Apps** in the top menu bar and then click **Create Application**.</span></span>
   
    ![LinkedIn — nowej aplikacji](./media/active-directory-b2c-setup-li-app/linkedin-new-app.png)
3. <span data-ttu-id="dddc2-111">W **Utwórz nową aplikację** tworzą, wprowadź odpowiednie informacje (**nazwa firmy**, **nazwa**, **opis**, **Adres URL Logo aplikacji**, **stosowania**, **adres URL witryny sieci Web**, **służbowy adres E-mail** i **Telefon służbowy**).</span><span class="sxs-lookup"><span data-stu-id="dddc2-111">In the **Create a New Application** form, fill in the relevant information (**Company Name**, **Name**, **Description**, **Application Logo URL**, **Application Use**, **Website URL**, **Business Email** and **Business Phone**).</span></span>
4. <span data-ttu-id="dddc2-112">Zgadzam się **LinkedIn interfejsu API warunki użytkowania** i kliknij przycisk **przesyłania**.</span><span class="sxs-lookup"><span data-stu-id="dddc2-112">Agree to the **LinkedIn API Terms of Use** and click **Submit**.</span></span>
   
    ![LinkedIn - rejestrowania aplikacji](./media/active-directory-b2c-setup-li-app/linkedin-register-app.png)
5. <span data-ttu-id="dddc2-114">Skopiuj wartości z **identyfikator klienta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="dddc2-114">Copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="dddc2-115">(Można znaleźć je w obszarze **klucze uwierzytelniania**.) Należy ich skonfigurowanie LinkedIn funkcję dostawcy tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="dddc2-115">(You can find them under **Authentication Keys**.) You will need both of them to configure LinkedIn as an identity provider in your tenant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dddc2-116">**Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="dddc2-116">**Client Secret** is an important security credential.</span></span>
   > 
   > 
6. <span data-ttu-id="dddc2-117">Wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w **autoryzacji adresów URL przekierowań** pola (w obszarze **OAuth 2.0**).</span><span class="sxs-lookup"><span data-stu-id="dddc2-117">Enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Authorized Redirect URLs** field (under **OAuth 2.0**).</span></span> <span data-ttu-id="dddc2-118">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (np. contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="dddc2-118">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="dddc2-119">Kliknij przycisk **Dodaj**, a następnie kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="dddc2-119">Click **Add**, and then click **Update**.</span></span> <span data-ttu-id="dddc2-120">**{Dzierżawa}** wartość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="dddc2-120">The **{tenant}** value is case-sensitive.</span></span>
   
    ![LinkedIn — ustawienia aplikacji](./media/active-directory-b2c-setup-li-app/linkedin-setup.png)

## <a name="configure-linkedin-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="dddc2-122">Skonfiguruj LinkedIn funkcję dostawcy tożsamości w Twojej dzierżawie</span><span class="sxs-lookup"><span data-stu-id="dddc2-122">Configure LinkedIn as an identity provider in your tenant</span></span>
1. <span data-ttu-id="dddc2-123">Wykonaj następujące kroki, aby [przejdź do bloku funkcji B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dddc2-123">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="dddc2-124">W bloku funkcji B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="dddc2-124">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="dddc2-125">Kliknij pozycję **+Dodaj** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="dddc2-125">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="dddc2-126">Podaj przyjazną nazwę w polu **nazwa** konfiguracji dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="dddc2-126">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="dddc2-127">Wprowadź na przykład "LI".</span><span class="sxs-lookup"><span data-stu-id="dddc2-127">For example, enter "LI".</span></span>
5. <span data-ttu-id="dddc2-128">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **LinkedIn**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="dddc2-128">Click **Identity provider type**, select **LinkedIn**, and click **OK**.</span></span>
6. <span data-ttu-id="dddc2-129">Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź identyfikator klienta i klucz tajny klienta aplikacji LinkedIn, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="dddc2-129">Click **Set up this identity provider** and enter the client ID and client secret of the LinkedIn application that you created earlier.</span></span>
7. <span data-ttu-id="dddc2-130">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** Aby zapisać konfigurację LinkedIn.</span><span class="sxs-lookup"><span data-stu-id="dddc2-130">Click **OK** and then click **Create** to save your LinkedIn configuration.</span></span>

