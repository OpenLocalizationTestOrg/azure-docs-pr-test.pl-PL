---
title: "Usługi Azure Active Directory B2C: Weryfikacja adresu E-mail, podczas tworzenia konta użytkownika wyłączyć | Dokumentacja firmy Microsoft"
description: "Temat prezentacja jak toodisable e-mail weryfikacji podczas tworzenia konta w usłudze Azure Active Directory B2C konsumenta"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="e97f2-103">Usługa Azure Active Directory B2C: Weryfikacja adresu e-mail Wyłącz podczas tworzenia konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="e97f2-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="e97f2-104">Po włączeniu usługi Azure Active Directory (Azure AD) B2C umożliwia a konsumenta hello toosign możliwości dla aplikacji, zapewniając adres e-mail i tworzenia konta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="e97f2-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="e97f2-105">Usługa Azure AD B2C zapewnia prawidłowe adresy e-mail, wymagając tooverify konsumentów ich podczas procesu tworzenia konta hello.</span><span class="sxs-lookup"><span data-stu-id="e97f2-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="e97f2-106">Również uniemożliwia złośliwego zautomatyzowany proces generowania fałszywych kont dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e97f2-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="e97f2-107">Niektórzy deweloperzy aplikacji preferowane jest Weryfikacja adresu e-mail tooskip podczas procesu tworzenia konta hello i zamiast tego ma użytkowników weryfikacji adresu e-mail hello później.</span><span class="sxs-lookup"><span data-stu-id="e97f2-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="e97f2-108">toosupport to usługi Azure AD B2C może być skonfigurowany toodisable Weryfikacja adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="e97f2-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="e97f2-109">Należy utworzyć płynniejszy procesu tworzenia konta i zapewnia deweloperom hello elastyczność toodifferentiate hello konsumentów, które sprawdzeniu swój adres e-mail z tych klientów, które nie mają.</span><span class="sxs-lookup"><span data-stu-id="e97f2-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="e97f2-110">Zasady rejestracji mają domyślnie włączona Weryfikacja adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="e97f2-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="e97f2-111">Użyj hello następujące kroki tooturn go wyłączyć:</span><span class="sxs-lookup"><span data-stu-id="e97f2-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="e97f2-112">[Wykonaj te bloku funkcji toohello B2C toonavigate kroki na powitania portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="e97f2-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="e97f2-113">Kliknij przycisk **zasady rejestracji** lub **zasad rejestracji i logowania** w zależności od konfiguracji dla rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e97f2-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="e97f2-114">Kliknij przycisk tooopen Twojego zasady (na przykład "B2C_1_SiUp") go.</span><span class="sxs-lookup"><span data-stu-id="e97f2-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="e97f2-115">Kliknij przycisk **Edytuj** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="e97f2-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="e97f2-116">Kliknij przycisk **dostosowywania interfejsu użytkownika strony**.</span><span class="sxs-lookup"><span data-stu-id="e97f2-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="e97f2-117">Kliknij przycisk **stronę tworzenia konta lokalnego konta**.</span><span class="sxs-lookup"><span data-stu-id="e97f2-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="e97f2-118">Kliknij przycisk **adres E-mail** w hello **nazwa** kolumnie hello **atrybuty rejestracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e97f2-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="e97f2-119">Przełącz hello **Żądaj weryfikacji** opcję zbyt**nr**.</span><span class="sxs-lookup"><span data-stu-id="e97f2-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="e97f2-120">Kliknij przycisk **OK** u dołu hello aż hello **edytować zasady** bloku.</span><span class="sxs-lookup"><span data-stu-id="e97f2-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="e97f2-121">Kliknij przycisk **zapisać** u góry bloku hello hello.</span><span class="sxs-lookup"><span data-stu-id="e97f2-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="e97f2-122">Gotowe!</span><span class="sxs-lookup"><span data-stu-id="e97f2-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="e97f2-123">Wyłączanie Weryfikacja adresu e-mail w procesie rejestracji hello może prowadzić toospam.</span><span class="sxs-lookup"><span data-stu-id="e97f2-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="e97f2-124">Jeśli wyłączysz domyślny hello, zaleca się dodawania systemu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="e97f2-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="e97f2-125">Jesteśmy zawsze toofeedback otwarte i sugestie!</span><span class="sxs-lookup"><span data-stu-id="e97f2-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="e97f2-126">Jeśli masz trudności w tym temacie lub mają zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="e97f2-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="e97f2-127">Funkcja żądań, dodaj ich zbyt[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="e97f2-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
