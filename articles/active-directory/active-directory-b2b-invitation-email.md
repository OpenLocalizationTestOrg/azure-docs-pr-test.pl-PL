---
title: "Elementy wiadomość e-mail z zaproszeniem Azure Active Directory B2B współpracy | Dokumentacja firmy Microsoft"
description: "Azure Active Directory B2B współpracy zaproszenia szablon wiadomości e-mail"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="b72e8-103">Elementy współpracy B2B zaproszenie</span><span class="sxs-lookup"><span data-stu-id="b72e8-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="b72e8-104">Wiadomości e-mail z zaproszeniem jest składnikiem krytycznym, aby przenieść do partnerów na statku jako użytkownicy współpracy B2B w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b72e8-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="b72e8-105">Można używać ich, aby zwiększyć zaufanie adresata.</span><span class="sxs-lookup"><span data-stu-id="b72e8-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="b72e8-106">Umożliwia dodanie legalności i doświadczenia z zaznaczenie tak społecznościowych dowód do wiadomości e-mail, aby upewnić się, że odbiorca **wprowadzenie** przycisk o zaakceptowanie zaproszenia.</span><span class="sxs-lookup"><span data-stu-id="b72e8-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="b72e8-107">Zaufanie jest klucza oznacza, że zmniejszyć tarcia udostępniania.</span><span class="sxs-lookup"><span data-stu-id="b72e8-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="b72e8-108">A także ma być e-mail wygląda świetnie!</span><span class="sxs-lookup"><span data-stu-id="b72e8-108">And you also want to make the email look great!</span></span>

![Azure wiadomość e-mail z zaproszeniem AD B2b](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="b72e8-110">Wyjaśniający wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="b72e8-110">Explaining the email</span></span>
<span data-ttu-id="b72e8-111">Oto kilka elementów wiadomości e-mail, aby wiedzieć, jak najlepiej używać ich funkcji.</span><span class="sxs-lookup"><span data-stu-id="b72e8-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="b72e8-112">Temat</span><span class="sxs-lookup"><span data-stu-id="b72e8-112">Subject</span></span>
<span data-ttu-id="b72e8-113">Temat wiadomości e-mail jest zgodny ze wzorcem następujące: Zapraszamy &lt;tenantname&gt; organizacji</span><span class="sxs-lookup"><span data-stu-id="b72e8-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="b72e8-114">Adres nadawcy</span><span class="sxs-lookup"><span data-stu-id="b72e8-114">From address</span></span>
<span data-ttu-id="b72e8-115">Używamy wzorzec przypominającej LinkedIn dla adres nadawcy.</span><span class="sxs-lookup"><span data-stu-id="b72e8-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="b72e8-116">Powinien być Wyczyść, który jest zapraszającej i adres e-mail od firmy oraz wyjaśnić, że wiadomość e-mail pochodzi od firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b72e8-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="b72e8-117">Format: &lt;nazwę wyświetlaną zapraszającej&gt; z &lt;tenantname&gt; (za pośrednictwem firmy Microsoft) <invites@microsoft.com&gt;</span><span class="sxs-lookup"><span data-stu-id="b72e8-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="b72e8-118">Udzielenie odpowiedzi na</span><span class="sxs-lookup"><span data-stu-id="b72e8-118">Reply To</span></span>
<span data-ttu-id="b72e8-119">Odpowiedz na wiadomość e-mail ma ustawioną zapraszającej poczty e-mail, jeśli jest dostępna, tak, aby podczas odpowiadania na wiadomości e-mail wysyła wiadomość e-mail z powrotem do zapraszającej.</span><span class="sxs-lookup"><span data-stu-id="b72e8-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="b72e8-120">Znakowania.</span><span class="sxs-lookup"><span data-stu-id="b72e8-120">Branding</span></span>
<span data-ttu-id="b72e8-121">Wiadomości e-mail zaproszenia użyciu dzierżawy firmy znakowania, które można zdefiniować dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="b72e8-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="b72e8-122">Jeśli chcesz skorzystać z zalet tej możliwości [tutaj](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) znajdują się szczegółowe informacje na temat konfigurowania go.</span><span class="sxs-lookup"><span data-stu-id="b72e8-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="b72e8-123">Baner logo jest wyświetlany w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="b72e8-123">The banner logo appears in the email.</span></span> <span data-ttu-id="b72e8-124">Postępuj zgodnie z rozmiarem obrazu i instrukcje jakości [tutaj](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) dla uzyskania najlepszych wyników.</span><span class="sxs-lookup"><span data-stu-id="b72e8-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="b72e8-125">Ponadto nazwa firmy również zostaną wyświetlone w wywołaniu akcji.</span><span class="sxs-lookup"><span data-stu-id="b72e8-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="b72e8-126">Wywołanie akcji</span><span class="sxs-lookup"><span data-stu-id="b72e8-126">Call to action</span></span>
<span data-ttu-id="b72e8-127">Wywołanie akcji składa się z dwóch części: wyjaśniający, dlaczego odbiorca odebrał wiadomość i co odbiorca jest pytany, rozwiązanie.</span><span class="sxs-lookup"><span data-stu-id="b72e8-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="b72e8-128">W sekcji "Dlaczego" może zostać zlikwidowane przy użyciu następującego wzorca: zaproszonych do uzyskania dostępu do aplikacji w &lt;tenantname&gt; organizacji</span><span class="sxs-lookup"><span data-stu-id="b72e8-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="b72e8-129">I "co użytkownik jest pytany, zrobić" sekcja jest określane przez obecności **wprowadzenie** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b72e8-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="b72e8-130">Po dodaniu odbiorca bez konieczności zaproszeń do skorzystania z tego przycisku nie pojawiają się.</span><span class="sxs-lookup"><span data-stu-id="b72e8-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="b72e8-131">Informacje w zapraszającej</span><span class="sxs-lookup"><span data-stu-id="b72e8-131">Inviter's information</span></span>
<span data-ttu-id="b72e8-132">Nazwa wyświetlana zapraszającej jest dołączany do wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="b72e8-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="b72e8-133">I dodatkowo, jeśli ustawiono obraz profilu konta usługi Azure AD, zaproszenia wiadomości e-mail zawierają również obraz.</span><span class="sxs-lookup"><span data-stu-id="b72e8-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="b72e8-134">Zarówno mają na celu zwiększenie zaufania z odbiorców w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="b72e8-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="b72e8-135">Jeśli jeszcze nie skonfigurowano obraz profilu, jest wyświetlana ikona inicjały zapraszającej zamiast obrazu:</span><span class="sxs-lookup"><span data-stu-id="b72e8-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![Wyświetlanie inicjały zapraszającej](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="b72e8-137">Treść</span><span class="sxs-lookup"><span data-stu-id="b72e8-137">Body</span></span>
<span data-ttu-id="b72e8-138">Treść zawiera komunikat, który zapraszającej Redaguj lub jest przekazywana zaproszenia interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="b72e8-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="b72e8-139">Jest obszaru tekstu, więc nie przetwarza tagów HTML ze względów bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="b72e8-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="b72e8-140">Stopki</span><span class="sxs-lookup"><span data-stu-id="b72e8-140">Footer section</span></span>
<span data-ttu-id="b72e8-141">Stopki zawiera marki firmy Microsoft i umożliwia tym adresata, jeśli wiadomość e-mail została wysłana z niemonitorowanego alias.</span><span class="sxs-lookup"><span data-stu-id="b72e8-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="b72e8-142">Szczególnych przypadkach:</span><span class="sxs-lookup"><span data-stu-id="b72e8-142">Special cases:</span></span>

- <span data-ttu-id="b72e8-143">Zapraszającej nie ma adresu e-mail w zaproszenia dzierżawy</span><span class="sxs-lookup"><span data-stu-id="b72e8-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![Obraz zapraszającej nie ma adresu e-mail w dzierżawy zaproszenia](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="b72e8-145">Odbiorca nie wymaga zrealizować zaproszenia</span><span class="sxs-lookup"><span data-stu-id="b72e8-145">The recipient doesn't need to redeem the invitation</span></span>

  ![Kiedy adresat nie trzeba zrealizować zaproszenia](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="b72e8-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b72e8-147">Next steps</span></span>

<span data-ttu-id="b72e8-148">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b72e8-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="b72e8-149">Co to jest współpraca B2B usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b72e8-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="b72e8-150">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="b72e8-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="b72e8-151">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="b72e8-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="b72e8-152">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="b72e8-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="b72e8-153">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="b72e8-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="b72e8-154">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="b72e8-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="b72e8-155">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="b72e8-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="b72e8-156">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="b72e8-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="b72e8-157">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="b72e8-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="b72e8-158">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="b72e8-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="b72e8-159">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b72e8-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
