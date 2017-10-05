---
title: "Usługa Azure Active Directory B2C: Amazon konfiguracji | Dokumentacja firmy Microsoft"
description: "Umożliwiają tworzenie kont i logowania użytkowników z kontami usługi Amazon w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
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
ms.openlocfilehash: dcc97e1b7f6287bd7692c52bf068950065a26572
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-to-consumers-with-amazon-accounts"></a><span data-ttu-id="70dcd-103">Azure Active Directory B2C: Umożliwiają tworzenie kont i logowania użytkowników z kontami usługi Amazon</span><span class="sxs-lookup"><span data-stu-id="70dcd-103">Azure Active Directory B2C: Provide sign-up and sign-in to consumers with Amazon accounts</span></span>
## <a name="create-an-amazon-application"></a><span data-ttu-id="70dcd-104">Tworzenie aplikacji usługi Amazon</span><span class="sxs-lookup"><span data-stu-id="70dcd-104">Create an Amazon application</span></span>
<span data-ttu-id="70dcd-105">Aby używać usługi Amazon funkcję dostawcy tożsamości w usłudze Azure Active Directory (Azure AD) B2C, należy utworzyć aplikację usługi Amazon i dostarczyć prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="70dcd-105">To use Amazon as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an Amazon application and supply it with the right parameters.</span></span> <span data-ttu-id="70dcd-106">Musisz mieć konto Amazon, w tym celu.</span><span class="sxs-lookup"><span data-stu-id="70dcd-106">You need an Amazon account to do this.</span></span> <span data-ttu-id="70dcd-107">Jeśli nie masz, możesz pobrać go w [http://www.amazon.com/](http://www.amazon.com/).</span><span class="sxs-lookup"><span data-stu-id="70dcd-107">If you don’t have one, you can get it at [http://www.amazon.com/](http://www.amazon.com/).</span></span>

1. <span data-ttu-id="70dcd-108">Przejdź do [Centrum deweloperów firmy Amazon](https://login.amazon.com/) i zaloguj się przy użyciu poświadczeń konta Amazon.</span><span class="sxs-lookup"><span data-stu-id="70dcd-108">Go to the [Amazon Developer Center](https://login.amazon.com/) and sign in with your Amazon account credentials.</span></span>
2. <span data-ttu-id="70dcd-109">Jeśli nie zostało to jeszcze zrobione, kliknij przycisk **Utwórz konto**, wykonaj kroki rejestracji deweloperów i zaakceptuj zasady.</span><span class="sxs-lookup"><span data-stu-id="70dcd-109">If you have not already done so, click **Sign Up**, follow the developer registration steps, and accept the policy.</span></span>
3. <span data-ttu-id="70dcd-110">Kliknij przycisk **zarejestrować nową aplikację**.</span><span class="sxs-lookup"><span data-stu-id="70dcd-110">Click **Register new application**.</span></span>
   
    ![Rejestrowanie nowych aplikacji w witrynie sieci Web firmy Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-new-app.png)
4. <span data-ttu-id="70dcd-112">Podaj informacje o aplikacji (**nazwa**, **opis**, i **adres URL powiadomienia prywatności**) i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="70dcd-112">Provide application information (**Name**, **Description**, and **Privacy Notice URL**) and click **Save**.</span></span>
   
    ![Udostępnia informacje o aplikacji do rejestrowania nowych aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-register-app.png)
5. <span data-ttu-id="70dcd-114">W **ustawień sieci Web** sekcji, skopiowanie wartości **identyfikator klienta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="70dcd-114">In the **Web Settings** section, copy the values of **Client ID** and **Client Secret**.</span></span> <span data-ttu-id="70dcd-115">(Należy kliknąć przycisk **Pokaż klucz tajny** przycisk, aby wyświetlić to.) Należy dysponować je, aby skonfigurować funkcję dostawcy tożsamości w dzierżawie usługi Amazon.</span><span class="sxs-lookup"><span data-stu-id="70dcd-115">(You need to click the **Show Secret** button to see this.) You need both of them to configure Amazon as an identity provider in your tenant.</span></span> <span data-ttu-id="70dcd-116">Kliknij przycisk **Edytuj** w dolnej części sekcji.</span><span class="sxs-lookup"><span data-stu-id="70dcd-116">Click **Edit** at the bottom of the section.</span></span> <span data-ttu-id="70dcd-117">**Klucz tajny klienta** jest ważne poświadczenie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="70dcd-117">**Client Secret** is an important security credential.</span></span>
   
    ![Podanie Identyfikatora klienta i klucz tajny klienta dla nowej aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-client-secret.png)
6. <span data-ttu-id="70dcd-119">Wprowadź `https://login.microsoftonline.com` w **dozwolone źródła JavaScript** pola i `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` w **mogą zwracać adresów URL** pola.</span><span class="sxs-lookup"><span data-stu-id="70dcd-119">Enter `https://login.microsoftonline.com` in the **Allowed JavaScript Origins** field and `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp` in the **Allowed Return URLs** field.</span></span> <span data-ttu-id="70dcd-120">Zastąp **{dzierżawa}** nazwą Twojej dzierżawy (np. contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="70dcd-120">Replace **{tenant}** with your tenant's name (for example, contoso.onmicrosoft.com).</span></span> <span data-ttu-id="70dcd-121">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="70dcd-121">Click **Save**.</span></span> <span data-ttu-id="70dcd-122">**{Dzierżawa}** wartość jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="70dcd-122">The **{tenant}** value is case-sensitive.</span></span>
   
    ![Zapewnienie źródeł JavaScript i zwracać adresów URL dla nowej aplikacji w portalu Amazon](./media/active-directory-b2c-setup-amzn-app/amzn-urls.png)

## <a name="configure-amazon-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="70dcd-124">Skonfiguruj funkcję dostawcy tożsamości w dzierżawie usługi Amazon</span><span class="sxs-lookup"><span data-stu-id="70dcd-124">Configure Amazon as an identity provider in your tenant</span></span>
1. <span data-ttu-id="70dcd-125">Wykonaj następujące kroki, aby [przejdź do bloku funkcji B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="70dcd-125">Follow these steps to [navigate to the B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on the Azure portal.</span></span>
2. <span data-ttu-id="70dcd-126">W bloku funkcji B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="70dcd-126">On the B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="70dcd-127">Kliknij pozycję **+Dodaj** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="70dcd-127">Click **+Add** at the top of the blade.</span></span>
4. <span data-ttu-id="70dcd-128">Podaj przyjazną nazwę w polu **nazwa** konfiguracji dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="70dcd-128">Provide a friendly **Name** for the identity provider configuration.</span></span> <span data-ttu-id="70dcd-129">Wprowadź na przykład "Amzn".</span><span class="sxs-lookup"><span data-stu-id="70dcd-129">For example, enter "Amzn".</span></span>
5. <span data-ttu-id="70dcd-130">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Amazon**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="70dcd-130">Click **Identity provider type**, select **Amazon**, and click **OK**.</span></span>
6. <span data-ttu-id="70dcd-131">Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź identyfikator klienta i klucz tajny klienta aplikacji Amazon, utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="70dcd-131">Click **Set up this identity provider** and enter the client ID and client secret of the Amazon application that you created earlier.</span></span>
7. <span data-ttu-id="70dcd-132">Kliknij przycisk **OK** , a następnie kliknij przycisk **Utwórz** Aby zapisać konfigurację Amazon.</span><span class="sxs-lookup"><span data-stu-id="70dcd-132">Click **OK** and then click **Create** to save your Amazon configuration.</span></span>

