---
title: "Usługa Azure Active Directory B2C: Amazon konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers zapisywania się i zaloguj się przy użyciu usługi Amazon kont w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 77c099bb-a005-4d75-87f9-f61e3de48725
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 60d7c4b76d9d3e86ed535765329abed07f1e5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-amazon-accounts"></a><span data-ttu-id="630f8-103">Usługa Azure Active Directory B2C: Udostępnianie konta Amazon tooconsumers rejestracji i logowania</span><span class="sxs-lookup"><span data-stu-id="630f8-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="630f8-104">Tworzenie aplikacji usługi Amazon</span><span class="sxs-lookup"><span data-stu-id="630f8-104">Create an Amazon application</span></span>
<span data-ttu-id="630f8-105">toouse Amazon jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy toocreate aplikacji Amazon i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="630f8-105">toouse Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate an Amazon application and supply it with hello right parameters.</span></span> <span data-ttu-id="630f8-106">Toodo konta Amazon to konieczne.</span><span class="sxs-lookup"><span data-stu-id="630f8-106">You need an Amazon account toodo this.</span></span> <span data-ttu-id="630f8-107">Jeśli nie masz, możesz pobrać go w [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="630f8-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="630f8-108">Przejdź toohello [Centrum deweloperów firmy Amazon](https://login.amazon.com/) i zaloguj się przy użyciu poświadczeń konta Amazon.</span><span class="sxs-lookup"><span data-stu-id="630f8-108">Go toohello [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="630f8-109">Jeśli nie zostało to jeszcze zrobione, kliknij przycisk **Utwórz konto**, wykonaj kroki rejestracji developer hello i zaakceptuj zasady hello.</span><span class="sxs-lookup"><span data-stu-id="630f8-109">If you have not already done so, click **Sign Up**, follow hello developer registration steps, and accept hello policy.</span></span>
3. <span data-ttu-id="630f8-110">Kliknij przycisk **zarejestrować nową aplikację**.</span><span class="sxs-lookup"><span data-stu-id="630f8-110">Click **Register new application**.</span></span>
   
    ![Rejestrowanie nowych aplikacji w witrynie sieci Web hello Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="630f8-112">Podaj informacje o aplikacji (**nazwa**, **opis**, i **adres URL powiadomienia prywatności**) i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="630f8-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Udostępnia informacje o aplikacji do rejestrowania nowych aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="630f8-114">W hello **ustawień sieci Web** sekcji kopiowania wartości hello **identyfikator klienta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="630f8-114">In hello **Web Settings** section, copy hello values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="630f8-115">(Należy tooclick hello **Pokaż klucz tajny** to przycisk toosee.) Należy ich tooconfigure Amazon funkcję dostawcy tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="630f8-115">(You need tooclick hello **Show Secret** button toosee this.) You need both of them tooconfigure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="630f8-116">Kliknij przycisk **Edytuj** u dołu hello hello sekcji.</span><span class="sxs-lookup"><span data-stu-id="630f8-116">Click **Edit** at hello bottom of hello section.</span></span> <span data-ttu-id="630f8-117">**Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="630f8-117">**Client Secret** is an important security credential.</span></span>
   
    ![Podanie Identyfikatora klienta i klucz tajny klienta dla nowej aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="630f8-119">Wprowadź `https://login.microsoftonline.com` w hello **dozwolone źródła JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w hello **mogą zwracać adresów URL** pola.</span><span class="sxs-lookup"><span data-stu-id="630f8-119">Enter `https://login.microsoftonline.com` in hello **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in hello **Allowed Return URLs** field.</span></span> <span data-ttu-id="630f8-120">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (np. contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="630f8-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="630f8-121">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="630f8-121">Click **Save**.</span></span> <span data-ttu-id="630f8-122">Witaj **{dzierżawa}** wartość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="630f8-122">hello **{tenant}** value is case-sensitive.</span></span>
   
    ![Zapewnienie źródeł JavaScript i zwracać adresów URL dla nowej aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="630f8-124">Skonfiguruj funkcję dostawcy tożsamości w dzierżawie usługi Amazon</span><span class="sxs-lookup"><span data-stu-id="630f8-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="630f8-125">Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="630f8-125">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="630f8-126">W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="630f8-126">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="630f8-127">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="630f8-127">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="630f8-128">Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="630f8-128">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="630f8-129">Wprowadź na przykład "Amzn".</span><span class="sxs-lookup"><span data-stu-id="630f8-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="630f8-130">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Amazon**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="630f8-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="630f8-131">Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello identyfikator i klienta klucz tajny klienta hello aplikacji Amazon, który został utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="630f8-131">Click **Set up this identity provider** and enter hello client ID and client secret of hello Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="630f8-132">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** toosave konfigurację Amazon.</span><span class="sxs-lookup"><span data-stu-id="630f8-132">Click **OK** and then click **Create** toosave your Amazon configuration.</span></span>

