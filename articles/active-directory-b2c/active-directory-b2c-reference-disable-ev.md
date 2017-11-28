---
title: "Usługi Azure Active Directory B2C: Weryfikacja adresu E-mail, podczas tworzenia konta użytkownika wyłączyć | Dokumentacja firmy Microsoft"
description: "Temat pokazująca, jak wyłączyć Weryfikacja adresu e-mail, podczas tworzenia konta w usłudze Azure Active Directory B2C konsumenta"
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
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="437ed-103">Usługa Azure Active Directory B2C: Weryfikacja adresu e-mail Wyłącz podczas tworzenia konta użytkownika</span><span class="sxs-lookup"><span data-stu-id="437ed-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="437ed-104">Po włączeniu usługi Azure Active Directory (Azure AD) B2C umożliwia konsumenta zalogowania się do aplikacji, zapewniając adres e-mail i tworzenia konta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="437ed-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="437ed-105">Usługa Azure AD B2C zapewnia prawidłowe adresy e-mail, wymagając od użytkowników w celu weryfikacji w procesie rejestracji.</span><span class="sxs-lookup"><span data-stu-id="437ed-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="437ed-106">Również uniemożliwia złośliwego zautomatyzowany proces generowania fałszywych kont dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="437ed-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="437ed-107">Niektórzy deweloperzy aplikacji preferowane może pominąć weryfikacji wiadomości e-mail w procesie rejestracji, a zamiast tego konsumentów później zweryfikować adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="437ed-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="437ed-108">Aby to obsłużyć, można skonfigurować usługi Azure AD B2C wyłączyć Weryfikacja adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="437ed-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="437ed-109">Należy utworzyć płynniejszy procesu tworzenia konta i zapewnia elastyczność do odróżnienia konsumentów, które sprawdzeniu swój adres e-mail z tych klientów, które nie mają.</span><span class="sxs-lookup"><span data-stu-id="437ed-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="437ed-110">Zasady rejestracji mają domyślnie włączona Weryfikacja adresu e-mail.</span><span class="sxs-lookup"><span data-stu-id="437ed-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="437ed-111">Aby ją wyłączyć, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="437ed-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="437ed-112">[Wykonaj następujące kroki, aby przejść do bloku funkcji B2C w portalu Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="437ed-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="437ed-113">Kliknij przycisk **zasady rejestracji** lub **zasad rejestracji i logowania** w zależności od konfiguracji dla rejestracji.</span><span class="sxs-lookup"><span data-stu-id="437ed-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="437ed-114">Kliknij zasady (na przykład "B2C_1_SiUp"), aby go otworzyć.</span><span class="sxs-lookup"><span data-stu-id="437ed-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="437ed-115">Kliknij przycisk **Edytuj** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="437ed-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="437ed-116">Kliknij przycisk **dostosowywania interfejsu użytkownika strony**.</span><span class="sxs-lookup"><span data-stu-id="437ed-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="437ed-117">Kliknij przycisk **stronę tworzenia konta lokalnego konta**.</span><span class="sxs-lookup"><span data-stu-id="437ed-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="437ed-118">Kliknij przycisk **adres E-mail** w **nazwa** kolumnie **atrybuty rejestracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="437ed-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="437ed-119">Przełącz **Żądaj weryfikacji** opcji w celu **nr**.</span><span class="sxs-lookup"><span data-stu-id="437ed-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="437ed-120">Kliknij przycisk **OK** u dołu, aż dojdziesz **edytować zasady** bloku.</span><span class="sxs-lookup"><span data-stu-id="437ed-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="437ed-121">Kliknij przycisk **zapisać** w górnej części bloku.</span><span class="sxs-lookup"><span data-stu-id="437ed-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="437ed-122">Gotowe!</span><span class="sxs-lookup"><span data-stu-id="437ed-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="437ed-123">Wyłączanie Weryfikacja adresu e-mail w procesie rejestracji może prowadzić do wysyłania spamu.</span><span class="sxs-lookup"><span data-stu-id="437ed-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="437ed-124">Jeśli wyłączysz domyślny, zaleca się dodawania systemu weryfikacji.</span><span class="sxs-lookup"><span data-stu-id="437ed-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="437ed-125">Firma Microsoft zawsze są otwarte na opinie i sugestie!</span><span class="sxs-lookup"><span data-stu-id="437ed-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="437ed-126">Jeśli masz trudności w tym temacie lub mają zalecenia dotyczące poprawy tej zawartości, prosimy o wyrażenie opinii na dole strony.</span><span class="sxs-lookup"><span data-stu-id="437ed-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="437ed-127">Funkcja żądań, dodaj je do [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="437ed-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>