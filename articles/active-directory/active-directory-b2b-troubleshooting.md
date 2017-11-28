---
title: "aaaTroubleshooting współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="bacdb-103">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="bacdb-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="bacdb-104">Poniżej przedstawiono niektóre środki zaradcze dla typowych problemów z współpracy B2B usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bacdb-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="bacdb-105">Chcę dodano użytkownika zewnętrznego, ale nie ma ich w książce adresowej globalne lub selektora osób hello</span><span class="sxs-lookup"><span data-stu-id="bacdb-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="bacdb-106">W przypadkach, gdy użytkownicy zewnętrzni nie zostały wypełnione na liście hello obiektu hello może potrwać kilka minut tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="bacdb-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="bacdb-107">Użytkownik-Gość B2B nie pojawia się w selektorze użytkowników usługi SharePoint Online/OneDrive</span><span class="sxs-lookup"><span data-stu-id="bacdb-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="bacdb-108">Witaj toosearch możliwości istniejących użytkowników gościa w selektora osób hello SharePoint Online (SPO) został WYŁĄCZONY przez domyślne zachowanie starszych toomatch.</span><span class="sxs-lookup"><span data-stu-id="bacdb-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="bacdb-109">Aby włączyć tę funkcję, należy za pomocą hello ustawienie "ShowPeoplePickerSuggestionsForGuestUsers" na poziomie hello dzierżawy i zbioru witryn.</span><span class="sxs-lookup"><span data-stu-id="bacdb-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="bacdb-110">Można ustawić opcję hello przy użyciu hello SPOTenant zestawu i SPOSite zestaw poleceń cmdlet, która zezwala na elementy członkowskie toosearch wszyscy istniejący użytkownicy gościa w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="bacdb-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="bacdb-111">Zmiany w zakresie dzierżawy hello nie wpływają na lokacje SPO już zainicjowaną.</span><span class="sxs-lookup"><span data-stu-id="bacdb-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="bacdb-112">Wyłączono zaproszeń do skorzystania z katalogu</span><span class="sxs-lookup"><span data-stu-id="bacdb-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="bacdb-113">Jeśli zostanie wyświetlone powiadomienie, że nie masz uprawnienia tooinvite użytkowników, sprawdź, czy konto użytkownika jest tooinvite autoryzowanych użytkowników zewnętrznych, w obszarze Ustawienia użytkownika:</span><span class="sxs-lookup"><span data-stu-id="bacdb-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="bacdb-114">Jeśli niedawno zmieniono te ustawienia lub przypisany hello zapraszającej gościa roli tooa użytkownik, mogą wystąpić opóźnienia 15 – 60 minut przed wprowadzeniem zmian hello.</span><span class="sxs-lookup"><span data-stu-id="bacdb-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="bacdb-115">Użytkownik Hello I zaproszenie otrzymuje wystąpił błąd podczas realizacji</span><span class="sxs-lookup"><span data-stu-id="bacdb-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="bacdb-116">Typowe błędy:</span><span class="sxs-lookup"><span data-stu-id="bacdb-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="bacdb-117">Zaproszonej administrator nie zezwolił użytkowników EmailVerified utworzenie w swojej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="bacdb-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="bacdb-118">Jeśli zaproszenie użytkowników, których organizacja korzysta z usługi Azure Active Directory, ale których hello konta określonego użytkownika nie istnieje (na przykład hello użytkownik nie istnieje w usłudze Azure AD w domenie contoso.com).</span><span class="sxs-lookup"><span data-stu-id="bacdb-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="bacdb-119">administrator Hello contoso.com może mieć zasady w miejscu uniemożliwia tworzone przez użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bacdb-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="bacdb-120">Hello użytkownika musi skontaktuj się z ich toodetermine administratora, jeśli użytkownicy zewnętrzni są dozwolone.</span><span class="sxs-lookup"><span data-stu-id="bacdb-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="bacdb-121">Witaj użytkownika zewnętrznego administratora może być konieczne tooallow zweryfikować poczty E-mail użytkowników w swojej domenie (zobacz [artykułu](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) na zezwolenie użytkownikom zweryfikować poczty E-mail).</span><span class="sxs-lookup"><span data-stu-id="bacdb-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="bacdb-122">Użytkownik zewnętrzny nie istnieje już w domenie federacyjnych</span><span class="sxs-lookup"><span data-stu-id="bacdb-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="bacdb-123">Jeśli używasz uwierzytelniania federacyjnego i użytkownik hello nie istnieje już w usłudze Azure Active Directory, nie mogą być zapraszani hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bacdb-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="bacdb-124">Ten problem, hello tooresolve użytkownika zewnętrznego administratora musi zsynchronizować tooAzure konta hello użytkownika usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bacdb-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="bacdb-125">Jak jest\#", która nie jest zwykle prawidłowym znakiem synchronizacji z usługą Azure AD?</span><span class="sxs-lookup"><span data-stu-id="bacdb-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="bacdb-126">"\#" jest zarezerwowany znak w UPN współpracy B2B usługi Azure AD lub użytkowników zewnętrznych, ponieważ hello zaproszenie konta user@contoso.com staje się user_contoso.com#EXT@fabrikam.onmicrosoft.com. W związku z tym \# w pochodzące z lokalnymi nazwy UPN nie są dozwolone toosign w toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="bacdb-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="bacdb-127">Dodawanie użytkowników zewnętrznych tooa synchronizowane grupy, wystąpi błąd</span><span class="sxs-lookup"><span data-stu-id="bacdb-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="bacdb-128">Użytkownicy zewnętrzni można dodać tylko za "przypisane" lub "Zabezpieczenia" grup i nie toogroups, który jest zarządzany lokalnie.</span><span class="sxs-lookup"><span data-stu-id="bacdb-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="bacdb-129">Moje użytkownika zewnętrznego nie otrzymały tooredeem poczty e-mail</span><span class="sxs-lookup"><span data-stu-id="bacdb-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="bacdb-130">osoby zaproszonej Hello skontaktować się z Usługodawcą lub tooensure filtru spamu, który hello następującego adresu są niedozwolone:Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="bacdb-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="bacdb-131">I należy zauważyć, że wiadomości powitania niestandardowych nie można uzyskać dołączana do komunikatów zaproszenia w czasie</span><span class="sxs-lookup"><span data-stu-id="bacdb-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="bacdb-132">toocomply z przepisów dotyczących prywatności, naszych interfejsów API, nie dołączaj niestandardowych komunikatów w wiadomości e-mail z zaproszeniem powitania po:</span><span class="sxs-lookup"><span data-stu-id="bacdb-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="bacdb-133">zapraszającej Hello nie ma adresu e-mail w hello zapraszanie dzierżawy</span><span class="sxs-lookup"><span data-stu-id="bacdb-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="bacdb-134">Gdy podmiot zabezpieczeń appservice wysyła hello zaproszenie</span><span class="sxs-lookup"><span data-stu-id="bacdb-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="bacdb-135">Ten scenariusz jest ważne tooyou, można pominąć naszych wiadomość e-mail z zaproszeniem interfejsu API i wysłać go za pomocą mechanizmu e-mail hello wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bacdb-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="bacdb-136">Zapoznaj się w organizacji korzystania z pomocy prawnej toomake się, że wszystkie wiadomości e-mail wysyłanych w ten sposób również spełnia przepisów dotyczących prywatności.</span><span class="sxs-lookup"><span data-stu-id="bacdb-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bacdb-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bacdb-137">Next steps</span></span>

<span data-ttu-id="bacdb-138">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="bacdb-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="bacdb-139">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="bacdb-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="bacdb-140">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="bacdb-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="bacdb-141">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="bacdb-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="bacdb-142">elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="bacdb-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="bacdb-143">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="bacdb-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="bacdb-144">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="bacdb-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="bacdb-145">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="bacdb-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="bacdb-146">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="bacdb-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="bacdb-147">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="bacdb-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="bacdb-148">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="bacdb-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="bacdb-149">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bacdb-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
