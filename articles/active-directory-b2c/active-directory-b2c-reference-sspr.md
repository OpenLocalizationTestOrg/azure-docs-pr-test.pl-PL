---
title: "Usługa Azure Active Directory B2C: Samoobsługowego resetowania hasła | Dokumentacja firmy Microsoft"
description: "Temat pokazująca, jak skonfigurować samoobsługowego resetowania haseł dla użytkowników w usłudze Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 0508868e3b00c5771cc26038a3dd71fde6625a84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="c2168-103">Usługa Azure Active Directory B2C: Konfigurowanie samoobsługowego resetowania haseł dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="c2168-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="c2168-104">Dzięki funkcji resetowania hasła samoobsługi użytkowników (którzy utworzyli konto dla kont lokalnych) można zresetować hasła na ich własnych.</span><span class="sxs-lookup"><span data-stu-id="c2168-104">With the self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="c2168-105">Pozwala to znacznie ograniczyć obciążenie działu pomocy technicznej, zwłaszcza, jeśli aplikacja ma miliony użytkowników przy użyciu go na bieżąco.</span><span class="sxs-lookup"><span data-stu-id="c2168-105">This significantly reduces the burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="c2168-106">Aktualnie obsługiwany jest tylko metoda odzyskiwania przy użyciu ze zweryfikowanym adresem e-mail.</span><span class="sxs-lookup"><span data-stu-id="c2168-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="c2168-107">Teraz dodamy metody dodatkowe odzyskiwania (numer telefonu zweryfikowane, pytań zabezpieczających, itp.) w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c2168-107">We will add additional recovery methods (verified phone number, security questions, etc.) in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="c2168-108">Ten artykuł dotyczy hasła Samoobsługowe Resetowanie używane w kontekście zasad logowania.</span><span class="sxs-lookup"><span data-stu-id="c2168-108">This article applies to self-service password reset used in the context of a sign-in policy.</span></span> <span data-ttu-id="c2168-109">Jeśli potrzebujesz zasady resetowania hasła można swobodnie dostosowywać wywoływane z aplikacji, zobacz [w tym artykule](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="c2168-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="c2168-110">Domyślnie katalogu nie będzie miał hasła Samoobsługowe Resetowanie włączona.</span><span class="sxs-lookup"><span data-stu-id="c2168-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="c2168-111">Aby włączyć tę funkcję, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="c2168-111">Use the following steps to turn it on:</span></span>

1. <span data-ttu-id="c2168-112">Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com/) jako administrator subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="c2168-112">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) as the Subscription Administrator.</span></span> <span data-ttu-id="c2168-113">To jest tej samej pracy lub konta służbowego lub tego samego konta Microsoft, który został użyty do utworzenia katalogu.</span><span class="sxs-lookup"><span data-stu-id="c2168-113">This is the same work or school account or the same Microsoft account that you used to create your directory.</span></span>
2. <span data-ttu-id="c2168-114">Przejdź do rozszerzenia usługi Active Directory na pasku nawigacyjnym po lewej stronie.</span><span class="sxs-lookup"><span data-stu-id="c2168-114">Navigate to the Active Directory extension on the navigation bar on the left side.</span></span>
3. <span data-ttu-id="c2168-115">Znajdź katalogu, w obszarze **katalogu** i kliknij ją.</span><span class="sxs-lookup"><span data-stu-id="c2168-115">Find your directory under the **Directory** tab and click it.</span></span>
4. <span data-ttu-id="c2168-116">Kliknij kartę **Konfiguracja**.</span><span class="sxs-lookup"><span data-stu-id="c2168-116">Click the **Configure** tab.</span></span>
5. <span data-ttu-id="c2168-117">Przewiń w dół do **zasady resetowania hasła użytkownika** sekcji, a następnie **użytkownicy włączeni do resetowania hasła** opcji w celu **tak**.</span><span class="sxs-lookup"><span data-stu-id="c2168-117">Scroll down to the **User password reset policy** section and toggle the **Users enabled for password reset** option to **YES**.</span></span> <span data-ttu-id="c2168-118">Zwróć uwagę, że **alternatywny adres E-mail** zaznaczono opcję; pozostaw, ponieważ jest on.</span><span class="sxs-lookup"><span data-stu-id="c2168-118">Notice that the **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Samoobsługowe resetowanie haseł](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="c2168-120">Kliknij przycisk **Zapisz** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="c2168-120">Click **Save** at the bottom of the page.</span></span> <span data-ttu-id="c2168-121">Gotowe!</span><span class="sxs-lookup"><span data-stu-id="c2168-121">You're done!</span></span>

<span data-ttu-id="c2168-122">Aby przetestować, funkcja "Uruchom teraz" na żadnych zasad logowania z kontami lokalnymi funkcję dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="c2168-122">To test, use the "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="c2168-123">Na logowanie lokalne konto strony (gdzie należy wprowadzić adres e-mail i hasło lub nazwę użytkownika i hasło), kliknij przycisk **nie może uzyskać dostępu do konta?** można zweryfikować środowiska użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c2168-123">On the local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** to verify the consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="c2168-124">Strony resetowania hasła samoobsługi można dostosować za pomocą [firmowe funkcji](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="c2168-124">The self-service password reset pages can be customized by using the [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

