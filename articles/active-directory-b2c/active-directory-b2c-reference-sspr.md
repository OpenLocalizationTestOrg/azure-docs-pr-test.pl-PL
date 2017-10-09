---
title: "Usługa Azure Active Directory B2C: Samoobsługowego resetowania hasła | Dokumentacja firmy Microsoft"
description: "Temat prezentacja sposób resetowania tooset samoobsługi hasła przez użytkowników w usłudze Azure Active Directory B2C"
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
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a><span data-ttu-id="3ebf1-103">Usługa Azure Active Directory B2C: Konfigurowanie samoobsługowego resetowania haseł dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="3ebf1-103">Azure Active Directory B2C: Set up self-service password reset for your consumers</span></span>
<span data-ttu-id="3ebf1-104">Z hello samoobsługowego resetowania hasła funkcji, użytkownikach (którzy utworzyli konto dla kont lokalnych), można zresetować hasła na ich własnych.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-104">With hello self-service password reset feature, your consumers (who have signed up for local accounts) can reset their passwords on their own.</span></span> <span data-ttu-id="3ebf1-105">Pozwala to znacznie ograniczyć hello obciążeń personelowi pomocy technicznej, zwłaszcza, jeśli aplikacja ma miliony użytkowników przy użyciu go na bieżąco.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-105">This significantly reduces hello burden on your support staff, especially if your application has millions of consumers using it on a regular basis.</span></span> <span data-ttu-id="3ebf1-106">Aktualnie obsługiwany jest tylko metoda odzyskiwania przy użyciu ze zweryfikowanym adresem e-mail.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-106">Currently, we only support using a verified email address as a recovery method.</span></span> <span data-ttu-id="3ebf1-107">W przyszłości hello dodamy metody dodatkowe odzyskiwania (numer telefonu zweryfikowane, pytań zabezpieczających, itp.).</span><span class="sxs-lookup"><span data-stu-id="3ebf1-107">We will add additional recovery methods (verified phone number, security questions, etc.) in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="3ebf1-108">Ten artykuł dotyczy hasło usługi tooself resetowania używane w kontekście hello zasad logowania.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-108">This article applies tooself-service password reset used in hello context of a sign-in policy.</span></span> <span data-ttu-id="3ebf1-109">Jeśli potrzebujesz zasady resetowania hasła można swobodnie dostosowywać wywoływane z aplikacji, zobacz [w tym artykule](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span><span class="sxs-lookup"><span data-stu-id="3ebf1-109">If you need fully customizable password reset policies invoked from your app, see [this article](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).</span></span>
> 
> 

<span data-ttu-id="3ebf1-110">Domyślnie katalogu nie będzie miał hasła Samoobsługowe Resetowanie włączona.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-110">By default, your directory will not have self-service password reset turned on.</span></span> <span data-ttu-id="3ebf1-111">Użyj hello następujące kroki tooturn go na:</span><span class="sxs-lookup"><span data-stu-id="3ebf1-111">Use hello following steps tooturn it on:</span></span>

1. <span data-ttu-id="3ebf1-112">Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) jako hello administratorem subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-112">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) as hello Subscription Administrator.</span></span> <span data-ttu-id="3ebf1-113">Jest to hello tej samej pracy lub konta służbowego lub hello tego samego konta Microsoft użyty toocreate katalogu.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-113">This is hello same work or school account or hello same Microsoft account that you used toocreate your directory.</span></span>
2. <span data-ttu-id="3ebf1-114">Przejdź toohello rozszerzenie usługi Active Directory na powitania pasku nawigacyjnym po lewej stronie powitania.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-114">Navigate toohello Active Directory extension on hello navigation bar on hello left side.</span></span>
3. <span data-ttu-id="3ebf1-115">Znajdź katalogu, w obszarze hello **katalogu** i kliknij ją.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-115">Find your directory under hello **Directory** tab and click it.</span></span>
4. <span data-ttu-id="3ebf1-116">Kliknij przycisk hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-116">Click hello **Configure** tab.</span></span>
5. <span data-ttu-id="3ebf1-117">Przewiń w dół toohello **zasady resetowania hasła użytkownika** hello sekcji, a następnie **użytkownicy włączeni do resetowania hasła** opcję zbyt**tak**.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-117">Scroll down toohello **User password reset policy** section and toggle hello **Users enabled for password reset** option too**YES**.</span></span> <span data-ttu-id="3ebf1-118">Zwróć uwagę, że hello **alternatywny adres E-mail** zaznaczono opcję; pozostaw, ponieważ jest on.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-118">Notice that hello **Alternate Email Address** option is checked; leave it as it is.</span></span>
   
    ![Samoobsługowe resetowanie haseł](./media/active-directory-b2c-reference-sspr/sspr.png)
6. <span data-ttu-id="3ebf1-120">Kliknij przycisk **zapisać** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-120">Click **Save** at hello bottom of hello page.</span></span> <span data-ttu-id="3ebf1-121">Gotowe!</span><span class="sxs-lookup"><span data-stu-id="3ebf1-121">You're done!</span></span>

<span data-ttu-id="3ebf1-122">tootest, użyj hello "Uruchom teraz" funkcji na żadnych zasad logowania z kontami lokalnymi funkcję dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-122">tootest, use hello "Run now" feature on any sign-in policy that has local accounts as an identity provider.</span></span> <span data-ttu-id="3ebf1-123">Na logowanie lokalne konto hello strony (gdzie należy wprowadzić adres e-mail i hasło lub nazwę użytkownika i hasło), kliknij przycisk **nie może uzyskać dostępu do konta?** tooverify powitania klienta środowiska.</span><span class="sxs-lookup"><span data-stu-id="3ebf1-123">On hello local account sign-in page (where you enter an email address and password, or a username and password), click **Can't access your account?** tooverify hello consumer experience.</span></span>

> [!NOTE]
> <span data-ttu-id="3ebf1-124">Witaj strony resetowania hasła samoobsługi można dostosować za pomocą hello [firmowe funkcji](../active-directory/active-directory-add-company-branding.md).</span><span class="sxs-lookup"><span data-stu-id="3ebf1-124">hello self-service password reset pages can be customized by using hello [company branding feature](../active-directory/active-directory-add-company-branding.md).</span></span>
> 
> 

