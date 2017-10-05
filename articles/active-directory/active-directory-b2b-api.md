---
title: "Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API | Dokumentacja firmy Microsoft"
description: "Współpraca B2B usługi Azure Active Directory wspiera relacje między firmami, umożliwiając partnerom biznesowym selektywne uzyskiwanie dostępu do Twoich aplikacji firmowych"
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
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="47822-103">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="47822-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="47822-104">Firma Microsoft zakończonej wielu klientów, powiedz nam, że chcą dostosowania procesu zaproszenia w taki sposób, który najlepiej pasuje do organizacji.</span><span class="sxs-lookup"><span data-stu-id="47822-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="47822-105">O interfejsie API możesz to zrobić tylko.</span><span class="sxs-lookup"><span data-stu-id="47822-105">With our API, you can do just that.</span></span> [<span data-ttu-id="47822-106">https://Developer.microsoft.com/Graph/docs/API-Reference/V1.0/Resources/invitation</span><span class="sxs-lookup"><span data-stu-id="47822-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="47822-107">Możliwości zaproszenia do interfejsu API</span><span class="sxs-lookup"><span data-stu-id="47822-107">Capabilities of the invitation API</span></span>
<span data-ttu-id="47822-108">Interfejs API oferuje następujące możliwości:</span><span class="sxs-lookup"><span data-stu-id="47822-108">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="47822-109">Zaproś użytkownika zewnętrznego z *żadnych* adres e-mail.</span><span class="sxs-lookup"><span data-stu-id="47822-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="47822-110">Dostosowywanie miejscu użytkownikom przejście po zaakceptowaniu zaproszenia ich.</span><span class="sxs-lookup"><span data-stu-id="47822-110">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="47822-111">Wysyłanie poczty standardowe zaproszenia przez nas</span><span class="sxs-lookup"><span data-stu-id="47822-111">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="47822-112">komunikat do adresata, który można dostosować</span><span class="sxs-lookup"><span data-stu-id="47822-112">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="47822-113">I wybierz opcję DW: osób, które mają być zachowane w pętli o tym współpracownika zaproszenie.</span><span class="sxs-lookup"><span data-stu-id="47822-113">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="47822-114">Lub całkowicie dostosować, wybierając pozycję nie wysłać powiadomienia za pomocą usługi Azure AD Twojego zaproszenia i przepływ pracy dołączania.</span><span class="sxs-lookup"><span data-stu-id="47822-114">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="47822-115">W takim przypadku można odzyskać realizacji adres URL z interfejsu API, który można osadzić w szablonu wiadomości e-mail, wiadomości Błyskawicznych lub innej metody dystrybucji wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="47822-115">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="47822-116">Ponadto jeśli jesteś administratorem, można zaprosić użytkowników jako elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="47822-116">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="47822-117">Modelu autoryzacji</span><span class="sxs-lookup"><span data-stu-id="47822-117">Authorization model</span></span>
<span data-ttu-id="47822-118">Interfejs API mogą być uruchamiane w następujących trybach autoryzacji:</span><span class="sxs-lookup"><span data-stu-id="47822-118">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="47822-119">Aplikacja + trybu użytkownika</span><span class="sxs-lookup"><span data-stu-id="47822-119">App + User mode</span></span>
<span data-ttu-id="47822-120">W tym trybie, kto korzysta na potrzeby interfejsu API uprawnienia można utworzyć B2B zaproszeń do skorzystania z.</span><span class="sxs-lookup"><span data-stu-id="47822-120">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="47822-121">Tryb tylko do aplikacji</span><span class="sxs-lookup"><span data-stu-id="47822-121">App only mode</span></span>
<span data-ttu-id="47822-122">W kontekście tylko aplikacji Aplikacja musi User.ReadWrite.All lub Directory.ReadWrite.All zakresów w zaproszeniu powiodło się.</span><span class="sxs-lookup"><span data-stu-id="47822-122">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="47822-123">Aby uzyskać więcej informacji, zapoznaj się: https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="47822-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="47822-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="47822-124">PowerShell</span></span>
<span data-ttu-id="47822-125">Obecnie istnieje możliwość dodania i łatwo zaprosić użytkowników zewnętrznych do organizacji przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47822-125">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="47822-126">Tworzenie zaproszenia, za pomocą polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="47822-126">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="47822-127">Można użyć następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="47822-127">You can use the following options:</span></span>

* <span data-ttu-id="47822-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="47822-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="47822-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="47822-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="47822-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="47822-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="47822-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="47822-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="47822-132">Można również wyewidencjonować odwołania zaproszenia interfejsu API w [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="47822-132">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="47822-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47822-133">Next steps</span></span>

<span data-ttu-id="47822-134">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="47822-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="47822-135">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="47822-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="47822-136">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="47822-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="47822-137">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="47822-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="47822-138">Elementy współpracy B2B zaproszenie</span><span class="sxs-lookup"><span data-stu-id="47822-138">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="47822-139">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="47822-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="47822-140">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="47822-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="47822-141">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="47822-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="47822-142">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="47822-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="47822-143">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="47822-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="47822-144">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="47822-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="47822-145">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47822-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
