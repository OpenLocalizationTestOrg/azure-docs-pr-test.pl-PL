---
title: "Usługa Azure Active Directory B2C: Twitter konfiguracji | Dokumentacja firmy Microsoft"
description: "Podaj tooconsumers rejestracji i logowania z kontami usługi Twitter w aplikacjach, które są zabezpieczone przez usługi Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 579a6841-9329-45b8-a351-da4315a6634e
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/06/2017
ms.author: parakhj
ms.openlocfilehash: 275c5c73fd5e8e5075e77fee942cbc1b5e1586cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-provide-sign-up-and-sign-in-tooconsumers-with-twitter-accounts"></a><span data-ttu-id="2a8a8-103">Usługa Azure Active Directory B2C: Podaj tooconsumers rejestracji i logowania z kontami usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="2a8a8-103">Azure Active Directory B2C: Provide sign-up and sign-in tooconsumers with Twitter accounts</span></span>

> [!NOTE]
> <span data-ttu-id="2a8a8-104">Ta funkcja jest dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-104">This feature is in preview.</span></span>
> 

## <a name="create-a-twitter-application"></a><span data-ttu-id="2a8a8-105">Utwórz aplikację usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="2a8a8-105">Create a Twitter application</span></span>
<span data-ttu-id="2a8a8-106">toouse usługi Twitter jako dostawca tożsamości w usłudze Azure Active Directory (Azure AD) B2C należy toocreate aplikacji Twitter i dostarczyć hello prawo parametrów.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-106">toouse Twitter as an identity provider in Azure Active Directory (Azure AD) B2C, you need toocreate a Twitter application and supply it with hello right parameters.</span></span> <span data-ttu-id="2a8a8-107">Toodo konta dewelopera Twitter to konieczne.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-107">You need a Twitter developer account toodo this.</span></span> <span data-ttu-id="2a8a8-108">Jeśli nie masz, możesz pobrać go w [https://dev.twitter.com/](https://dev.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="2a8a8-108">If you don’t have one, you can get it at [https://dev.twitter.com/](https://dev.twitter.com/).</span></span>

1. <span data-ttu-id="2a8a8-109">Przejdź toohello [dewelopera witryny sieci Web w usłudze Twitter](https://dev.twitter.com/) i zaloguj się przy użyciu poświadczeń.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-109">Go toohello [Twitter developer's website](https://dev.twitter.com/) and sign in with your credentials.</span></span>
2. <span data-ttu-id="2a8a8-110">Kliknij przycisk **Moje aplikacje** w obszarze **narzędzia i pomoc techniczna** , a następnie kliknij przycisk **Utwórz nową aplikację**.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-110">Click **My apps** under **Tools & Support** and then click **Create New App**.</span></span> 
3. <span data-ttu-id="2a8a8-111">W formularzu hello, podaj wartość hello **nazwa**, **opis**, i **witryny sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-111">In hello form, provide a value for hello **Name**, **Description**, and **Website**.</span></span>
4. <span data-ttu-id="2a8a8-112">Dla hello **wywołania zwrotnego adresu URL**, wprowadź `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-112">For hello **Callback URL**, enter `https://login.microsoftonline.com/te/{tenant}/oauth2/authresp`.</span></span> <span data-ttu-id="2a8a8-113">Upewnij się, że tooreplace **{dzierżawa}** nazwą Twojej dzierżawy (na przykład contosob2c.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="2a8a8-113">Make sure tooreplace **{tenant}** with your tenant's name (for example, contosob2c.onmicrosoft.com).</span></span>
5. <span data-ttu-id="2a8a8-114">Sprawdź hello pole tooagree toohello **umowy Developer** i kliknij przycisk **tworzenie aplikacji Twitter**.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-114">Check hello box tooagree toohello **Developer Agreement** and click **Create your Twitter application**.</span></span>
6. <span data-ttu-id="2a8a8-115">Po utworzeniu aplikacji hello kliknij **kluczy i tokenów dostępu**.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-115">Once hello app is created, click **Keys and Access Tokens**.</span></span>
7. <span data-ttu-id="2a8a8-116">Skopiuj wartość hello **konsumenta** i **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-116">Copy hello value of **Consumer Key** and **Consumer Secret**.</span></span> <span data-ttu-id="2a8a8-117">Konieczne będzie ich tooconfigure Twitter jako dostawca tożsamości w dzierżawie.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-117">You will need both of them tooconfigure Twitter as an identity provider in your tenant.</span></span>

## <a name="configure-twitter-as-an-identity-provider-in-your-tenant"></a><span data-ttu-id="2a8a8-118">Skonfiguruj funkcję dostawcy tożsamości w dzierżawie usługi Twitter</span><span class="sxs-lookup"><span data-stu-id="2a8a8-118">Configure Twitter as an identity provider in your tenant</span></span>
1. <span data-ttu-id="2a8a8-119">Wykonaj następujące kroki zbyt[przejdź do bloku funkcji toohello B2C](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) na powitania portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-119">Follow these steps too[navigate toohello B2C features blade](active-directory-b2c-app-registration.md#navigate-to-b2c-settings) on hello Azure portal.</span></span>
2. <span data-ttu-id="2a8a8-120">W bloku funkcji hello B2C, kliknij polecenie **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-120">On hello B2C features blade, click **Identity providers**.</span></span>
3. <span data-ttu-id="2a8a8-121">Kliknij przycisk **+ Dodaj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-121">Click **+Add** at hello top of hello blade.</span></span>
4. <span data-ttu-id="2a8a8-122">Podaj przyjazną nazwę w polu **nazwa** hello tożsamości dostawcy konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-122">Provide a friendly **Name** for hello identity provider configuration.</span></span> <span data-ttu-id="2a8a8-123">Wprowadź na przykład "Twitter".</span><span class="sxs-lookup"><span data-stu-id="2a8a8-123">For example, enter "Twitter".</span></span>
5. <span data-ttu-id="2a8a8-124">Kliknij przycisk **typ dostawcy tożsamości**, wybierz pozycję **Twitter**i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-124">Click **Identity provider type**, select **Twitter**, and click **OK**.</span></span>
6. <span data-ttu-id="2a8a8-125">Kliknij przycisk **skonfigurować ten dostawca tożsamości** , a następnie wprowadź hello Twitter **konsumenta** dla hello **identyfikator klienta** i hello Twitter **klucz tajny klienta**dla hello **klucz tajny klienta**.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-125">Click **Set up this identity provider** and enter hello Twitter **Consumer Key** for hello **Client id** and hello Twitter **Consumer Secret** for hello **Client secret**.</span></span>
7. <span data-ttu-id="2a8a8-126">Kliknij przycisk **OK**, a następnie kliknij przycisk **Utwórz** toosave konfigurację usługi Twitter.</span><span class="sxs-lookup"><span data-stu-id="2a8a8-126">Click **OK**, and then click **Create** toosave your Twitter configuration.</span></span>

