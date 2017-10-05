---
title: "Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Środki zaradcze dla typowych problemów z współpracy usługi Azure Active Directory B2B"
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
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 2009cfc956a2703e268c9364996aa2d0fbd8f279
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="601ea-103">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="601ea-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="601ea-104">Poniżej przedstawiono niektóre środki zaradcze dla typowych problemów z współpracy B2B usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="601ea-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="601ea-105">Chcę dodano użytkownika zewnętrznego, ale nie ma ich w książce adresowej globalnych lub selektora osób</span><span class="sxs-lookup"><span data-stu-id="601ea-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="601ea-106">W przypadkach, gdy użytkownicy zewnętrzni nie zostały wypełnione na liście obiekt może potrwać kilka minut, aby replikować.</span><span class="sxs-lookup"><span data-stu-id="601ea-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="601ea-107">Użytkownik-Gość B2B nie pojawia się w selektorze użytkowników usługi SharePoint Online/OneDrive</span><span class="sxs-lookup"><span data-stu-id="601ea-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="601ea-108">Domyślnie, aby dopasować starsze zachowanie możliwość wyszukiwania istniejących użytkowników gościa w selektorze użytkowników programu SharePoint Online (SPO) ma wartość OFF.</span><span class="sxs-lookup"><span data-stu-id="601ea-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="601ea-109">Można włączyć tę funkcję za pomocą ustawienia "ShowPeoplePickerSuggestionsForGuestUsers" na poziomie kolekcji dzierżawy i witryny.</span><span class="sxs-lookup"><span data-stu-id="601ea-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="601ea-110">Można ustawić funkcji za pośrednictwem poleceń cmdlet Set SPOTenant i Set-SPOSite, która zezwala na elementy członkowskie wyszukać wszystkich istniejących użytkowników gościa w katalogu.</span><span class="sxs-lookup"><span data-stu-id="601ea-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="601ea-111">Zmiany w zakresie dzierżawy nie wpływają na lokacje SPO już zainicjowaną.</span><span class="sxs-lookup"><span data-stu-id="601ea-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="601ea-112">Wyłączono zaproszeń do skorzystania z katalogu</span><span class="sxs-lookup"><span data-stu-id="601ea-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="601ea-113">Jeśli zostanie wyświetlone powiadomienie, że nie masz uprawnień do zapraszania użytkowników, należy sprawdzić, czy Twoje konto użytkownika jest autoryzowany z zaproszeniem dla użytkowników zewnętrznych, w obszarze Ustawienia użytkownika:</span><span class="sxs-lookup"><span data-stu-id="601ea-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="601ea-114">Jeśli niedawno zmieniono te ustawienia lub rolą Gość zapraszającej przypisana do użytkownika, mogą wystąpić opóźnienia 15 – 60 minut przed wprowadzeniem zmian.</span><span class="sxs-lookup"><span data-stu-id="601ea-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="601ea-115">Użytkownik, który zaproszenie I otrzymuje wystąpił błąd podczas realizacji</span><span class="sxs-lookup"><span data-stu-id="601ea-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="601ea-116">Typowe błędy:</span><span class="sxs-lookup"><span data-stu-id="601ea-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="601ea-117">Zaproszonej administrator nie zezwolił użytkowników EmailVerified utworzenie w swojej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="601ea-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="601ea-118">Gdy zapraszanie użytkowników, których organizacja korzysta z usługi Azure Active Directory, ale gdy konta określonego użytkownika nie istnieje (na przykład użytkownik nie istnieje w usłudze Azure AD w domenie contoso.com).</span><span class="sxs-lookup"><span data-stu-id="601ea-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="601ea-119">Administrator domeny contoso.com może mieć zasady w miejscu uniemożliwia tworzone przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="601ea-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="601ea-120">Użytkownik musi skontaktować się z ich administratora, aby określić, czy użytkownicy zewnętrzni są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="601ea-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="601ea-121">Użytkownika zewnętrznego administratora może być konieczne użytkownicy zweryfikować poczty E-mail w swojej domenie (zobacz [artykułu](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) na zezwolenie użytkownikom zweryfikować poczty E-mail).</span><span class="sxs-lookup"><span data-stu-id="601ea-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="601ea-122">Użytkownik zewnętrzny nie istnieje już w domenie federacyjnych</span><span class="sxs-lookup"><span data-stu-id="601ea-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="601ea-123">Jeśli używasz uwierzytelniania federacyjnego i użytkownik nie istnieje już w usłudze Azure Active Directory, nie mogą być zapraszani użytkownika.</span><span class="sxs-lookup"><span data-stu-id="601ea-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="601ea-124">Aby rozwiązać ten problem, administrator użytkownika zewnętrznego należy zsynchronizować konta użytkownika do usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="601ea-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="601ea-125">Jak jest\#", która nie jest zwykle prawidłowym znakiem synchronizacji z usługą Azure AD?</span><span class="sxs-lookup"><span data-stu-id="601ea-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="601ea-126">"\#" jest zarezerwowany znak w UPN współpracy B2B usługi Azure AD lub użytkowników zewnętrznych, ponieważ konto zaproszonych user@contoso.com staje się user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="601ea-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="601ea-127">W związku z tym \# w UPN pochodzące z lokalnymi nie mogą logować się do portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="601ea-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="601ea-128">Przy dodawaniu użytkowników zewnętrznych do grupy synchronizowane komunikat o błędzie</span><span class="sxs-lookup"><span data-stu-id="601ea-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="601ea-129">Użytkownicy zewnętrzni mogą być dodawane tylko dla grup "Zabezpieczenia" lub "przypisane", a nie do grup, które są lokalne zarządzanego.</span><span class="sxs-lookup"><span data-stu-id="601ea-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="601ea-130">Moje użytkownika zewnętrznego nie odebrał wiadomość e-mail, aby zrealizować</span><span class="sxs-lookup"><span data-stu-id="601ea-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="601ea-131">Osoby zaproszonej skontaktować się z ich usługodawcy internetowego lub spamu filtru, aby upewnić się, czy następujący adres może:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="601ea-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="601ea-132">I Zwróć uwagę, że niestandardowy komunikat nie można uzyskać dołączana do komunikatów zaproszenia w czasie</span><span class="sxs-lookup"><span data-stu-id="601ea-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="601ea-133">Do wykonania przepisów dotyczących prywatności, naszych interfejsów API, nie dołączaj niestandardowych komunikatów w wiadomości e-mail z zaproszeniem po:</span><span class="sxs-lookup"><span data-stu-id="601ea-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="601ea-134">Zapraszającej nie ma adresu e-mail w dzierżawie zaproszenia</span><span class="sxs-lookup"><span data-stu-id="601ea-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="601ea-135">Jeśli podmiot zabezpieczeń appservice wysyła zaproszenia</span><span class="sxs-lookup"><span data-stu-id="601ea-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="601ea-136">Ten scenariusz jest istotne dla Ciebie, można pominąć naszych wiadomość e-mail z zaproszeniem interfejsu API i wysłać go za pośrednictwem poczty e-mail mechanizmu wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="601ea-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="601ea-137">Zapoznaj się w organizacji korzystania z pomocy prawnej się upewnić się, że każdej wiadomości e-mail, wysyłania, że ten sposób również spełnia przepisów dotyczących prywatności.</span><span class="sxs-lookup"><span data-stu-id="601ea-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="601ea-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="601ea-138">Next steps</span></span>

<span data-ttu-id="601ea-139">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="601ea-139">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="601ea-140">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="601ea-140">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="601ea-141">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="601ea-141">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="601ea-142">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="601ea-142">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="601ea-143">Elementy współpracy B2B zaproszenie</span><span class="sxs-lookup"><span data-stu-id="601ea-143">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="601ea-144">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="601ea-144">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="601ea-145">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="601ea-145">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="601ea-146">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="601ea-146">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="601ea-147">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="601ea-147">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="601ea-148">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="601ea-148">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="601ea-149">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="601ea-149">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="601ea-150">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="601ea-150">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
