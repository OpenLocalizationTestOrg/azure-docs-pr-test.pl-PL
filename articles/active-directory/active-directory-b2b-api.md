---
title: "aaaAzure Active Directory B2B współpracy interfejsu API i dostosowywania | Dokumentacja firmy Microsoft"
description: "Współpraca z usługą Azure Active Directory B2B obsługuje relacji między firmami przez włączenie dostępu tooselectively partnerów biznesowych aplikacji firmowych"
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="dfa90-103">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="dfa90-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="dfa90-104">Firma Microsoft zakończonej wielu klientów, poinformuj nas, czy chcą toocustomize hello zaproszenia procesu w taki sposób, który działa najlepiej w organizacji.</span><span class="sxs-lookup"><span data-stu-id="dfa90-104">We've had many customers tell us that they want toocustomize hello invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="dfa90-105">O interfejsie API możesz to zrobić tylko.</span><span class="sxs-lookup"><span data-stu-id="dfa90-105">With our API, you can do just that.</span></span> [<span data-ttu-id="dfa90-106">https://Developer.microsoft.com/Graph/docs/API-Reference/V1.0/Resources/invitation</span><span class="sxs-lookup"><span data-stu-id="dfa90-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a><span data-ttu-id="dfa90-107">Możliwości zaproszenia hello interfejsu API</span><span class="sxs-lookup"><span data-stu-id="dfa90-107">Capabilities of hello invitation API</span></span>
<span data-ttu-id="dfa90-108">Witaj interfejsu API zapewniają hello następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="dfa90-108">hello API offers hello following capabilities:</span></span>

1. <span data-ttu-id="dfa90-109">Zaproś użytkownika zewnętrznego z *żadnych* adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="dfa90-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="dfa90-110">Dostosowywanie miejscu tooland Twojego użytkowników po zaakceptowaniu zaproszenia ich.</span><span class="sxs-lookup"><span data-stu-id="dfa90-110">Customize where you want your users tooland after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="dfa90-111">Wybierz toosend hello standardowe zaproszeniu przez nas</span><span class="sxs-lookup"><span data-stu-id="dfa90-111">Choose toosend hello standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="dfa90-112">z adresata toohello komunikat, który można dostosować</span><span class="sxs-lookup"><span data-stu-id="dfa90-112">with a message toohello recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="dfa90-113">I wybierz polecenie toocc: osób, które mają tookeep w hello pętli o tym współpracownika zaproszenie.</span><span class="sxs-lookup"><span data-stu-id="dfa90-113">And choose toocc: people you want tookeep in hello loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="dfa90-114">Lub całkowicie dostosować, wybierając nie toosend powiadomienia za pomocą usługi Azure AD Twojego zaproszenia i przepływ pracy dołączania.</span><span class="sxs-lookup"><span data-stu-id="dfa90-114">Or completely customize your invitation and onboarding workflow by choosing not toosend notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="dfa90-115">W takim przypadku wracając realizacji adres URL z hello interfejs API, który można osadzić w szablonu wiadomości e-mail, wiadomości Błyskawicznych lub innej metody dystrybucji wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="dfa90-115">In this case, you get back a redemption URL from hello API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="dfa90-116">Ponadto jeśli jesteś administratorem, możesz tooinvite hello użytkownika jako element członkowski.</span><span class="sxs-lookup"><span data-stu-id="dfa90-116">Finally, if you are an admin, you can choose tooinvite hello user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="dfa90-117">Modelu autoryzacji</span><span class="sxs-lookup"><span data-stu-id="dfa90-117">Authorization model</span></span>
<span data-ttu-id="dfa90-118">Witaj interfejsu API mogą być uruchamiane w hello następujące tryby autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="dfa90-118">hello API can be run in hello following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="dfa90-119">Aplikacja + trybu użytkownika</span><span class="sxs-lookup"><span data-stu-id="dfa90-119">App + User mode</span></span>
<span data-ttu-id="dfa90-120">W tym trybie, kto korzysta potrzeb hello interfejsu API toohave hello uprawnienia toobe Tworzenie zaproszeń do skorzystania z B2B.</span><span class="sxs-lookup"><span data-stu-id="dfa90-120">In this mode, whoever is using hello API needs toohave hello permissions toobe create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="dfa90-121">Tryb tylko do aplikacji</span><span class="sxs-lookup"><span data-stu-id="dfa90-121">App only mode</span></span>
<span data-ttu-id="dfa90-122">W kontekście tylko aplikacji hello aplikacja potrzebuje hello User.ReadWrite.All lub Directory.ReadWrite.All zakresów dla toosucceed zaproszenia hello.</span><span class="sxs-lookup"><span data-stu-id="dfa90-122">In app only context, hello app needs hello User.ReadWrite.All or Directory.ReadWrite.All scopes for hello invitation toosucceed.</span></span>

<span data-ttu-id="dfa90-123">Aby uzyskać więcej informacji, zapoznaj się: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="dfa90-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="dfa90-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dfa90-124">PowerShell</span></span>
<span data-ttu-id="dfa90-125">Łatwo jest teraz możliwe toouse środowiska PowerShell tooadd i zaprosić użytkowników zewnętrznych tooan organizacji.</span><span class="sxs-lookup"><span data-stu-id="dfa90-125">It is now possible toouse PowerShell tooadd and invite external users tooan organization easily.</span></span> <span data-ttu-id="dfa90-126">Utwórz zaproszenia przy użyciu polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="dfa90-126">Create an invitation using hello cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="dfa90-127">Program hello następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="dfa90-127">You can use hello following options:</span></span>

* <span data-ttu-id="dfa90-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="dfa90-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="dfa90-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="dfa90-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="dfa90-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="dfa90-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="dfa90-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="dfa90-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="dfa90-132">Można również wyewidencjonować hello odwołanie zaproszenia interfejsu API w [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="dfa90-132">You can also check out hello invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfa90-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dfa90-133">Next steps</span></span>

<span data-ttu-id="dfa90-134">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="dfa90-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="dfa90-135">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="dfa90-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="dfa90-136">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="dfa90-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="dfa90-137">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="dfa90-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="dfa90-138">elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="dfa90-138">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="dfa90-139">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="dfa90-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="dfa90-140">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="dfa90-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="dfa90-141">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="dfa90-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="dfa90-142">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="dfa90-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="dfa90-143">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="dfa90-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="dfa90-144">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="dfa90-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="dfa90-145">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dfa90-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
