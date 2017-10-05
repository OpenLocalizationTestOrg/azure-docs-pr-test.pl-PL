---
title: "Co to jest współpraca z usługi Azure Active Directory B2B? | Microsoft Docs"
description: "Współpraca z usługą Azure Active Directory B2B obsługuje relacji między firmami, umożliwiając partnerom biznesowym selektywne uzyskiwanie dostępu do aplikacji firmowych."
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 1464387b-ee8b-4c7c-94b3-2c5567224c27
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 06/27/2017
ms.author: curtand
ms.custom: aaddev
ms.reviewer: sasubram
ms.openlocfilehash: fbc12a52555b190d43b5e953fd4d19923a25b0ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-b2b-collaboration"></a><span data-ttu-id="e29eb-104">Czym jest współpraca B2B w usłudze Azure AD?</span><span class="sxs-lookup"><span data-stu-id="e29eb-104">What is Azure AD B2B collaboration?</span></span>

<iframe width="560" height="315" src="https://www.youtube.com/embed/AhwrweCBdsc" frameborder="0" allowfullscreen></iframe>

<span data-ttu-id="e29eb-105">Azure AD business-to-business (B2B) możliwości współpracy Włącz każdej przy użyciu usługi Azure AD do pracy bezpiecznie z użytkowników z dowolnej innej organizacji, małych i dużych organizacji.</span><span class="sxs-lookup"><span data-stu-id="e29eb-105">Azure AD business-to-business (B2B) collaboration capabilities enable any organization using Azure AD to work safely and securely with users from any other organization, small or large.</span></span> <span data-ttu-id="e29eb-106">Te organizacje mogą być z usługą Azure AD lub bez, lub nawet w przypadku organizacji IT lub bez.</span><span class="sxs-lookup"><span data-stu-id="e29eb-106">Those organizations can be with Azure AD or without, or even with an IT organization or without.</span></span> 

<span data-ttu-id="e29eb-107">Organizacje przy użyciu usługi Azure AD umożliwia dostęp do dokumentów, zasobów i aplikacji do ich partnerów, zachowując pełną kontrolę nad ich danymi firmowymi.</span><span class="sxs-lookup"><span data-stu-id="e29eb-107">Organizations using Azure AD can provide access to documents, resources, and applications to their partners, while maintaining complete control over their own corporate data.</span></span> <span data-ttu-id="e29eb-108">Deweloperzy mogą używać usługi Azure AD business-to-business interfejsy API do programowania aplikacji, które sobą dwie organizacje bardziej bezpieczne.</span><span class="sxs-lookup"><span data-stu-id="e29eb-108">Developers can use the Azure AD business-to-business APIs to write applications that bring two organizations together in more securely.</span></span> <span data-ttu-id="e29eb-109">Ponadto jest dość łatwe nawigowania.</span><span class="sxs-lookup"><span data-stu-id="e29eb-109">Also, it's pretty easy for end users to navigate.</span></span>

<span data-ttu-id="e29eb-110">97% klientów zwracali naszą uwagę, że współpracy B2B usługi Azure AD jest bardzo ważne, aby je.</span><span class="sxs-lookup"><span data-stu-id="e29eb-110">97% of our customers have told us Azure AD B2B collaboration is very important to them.</span></span>

![Wykres kołowy](media/active-directory-b2b-what-is-azure-ad-b2b/97-percent-support.png)

<span data-ttu-id="e29eb-112">Począwszy od początku kwietnia 2017 r. było około 3 milionów użytkowników już za pomocą funkcji współpracy B2B usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e29eb-112">As of early April 2017, we had about 3 million users already using Azure AD B2B collaboration capabilities.</span></span> <span data-ttu-id="e29eb-113">I więcej niż 23% organizacji usługi Azure AD, które mają więcej niż 10 użytkownikami są już korzystających z tych funkcji.</span><span class="sxs-lookup"><span data-stu-id="e29eb-113">And more than 23% of Azure AD organizations that have more than 10 users are already benefiting from these capabilities.</span></span>

## <a name="the-key-benefits-of-azure-ad-b2b-collaboration-to-your-organization"></a><span data-ttu-id="e29eb-114">Najważniejsze zalety współpracy B2B usługi Azure AD dla Twojej organizacji</span><span class="sxs-lookup"><span data-stu-id="e29eb-114">The key benefits of Azure AD B2B collaboration to your organization</span></span>

### <a name="work-with-any-user-from-any-partner"></a><span data-ttu-id="e29eb-115">Praca z żadnym użytkownikiem od dowolnego partnera</span><span class="sxs-lookup"><span data-stu-id="e29eb-115">Work with any user from any partner</span></span>

* <span data-ttu-id="e29eb-116">Partnerzy użyć własnych poświadczeń</span><span class="sxs-lookup"><span data-stu-id="e29eb-116">Partners use their own credentials</span></span>

* <span data-ttu-id="e29eb-117">Nie jest wymagany dla partnerów przy użyciu usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e29eb-117">No requirement for partners to use Azure AD</span></span>

* <span data-ttu-id="e29eb-118">Nie zewnętrznych katalogów lub skomplikowane wymagane</span><span class="sxs-lookup"><span data-stu-id="e29eb-118">No external directories or complex set-up required</span></span>

### <a name="simple-and-secure-collaboration"></a><span data-ttu-id="e29eb-119">Proste i bezpiecznej współpracy</span><span class="sxs-lookup"><span data-stu-id="e29eb-119">Simple and secure collaboration</span></span>

* <span data-ttu-id="e29eb-120">Dostęp do dowolnej aplikacji firmowych lub danych, podczas stosowania zaawansowane, Azure zasad zasilania AD autoryzacji</span><span class="sxs-lookup"><span data-stu-id="e29eb-120">Provide access to any corporate app or data, while applying sophisticated, Azure AD-powered authorization policies</span></span>

* <span data-ttu-id="e29eb-121">Użytkownicy mogą łatwo</span><span class="sxs-lookup"><span data-stu-id="e29eb-121">Easy for users</span></span>

* <span data-ttu-id="e29eb-122">Zabezpieczenia korporacyjnej dla aplikacji i danych</span><span class="sxs-lookup"><span data-stu-id="e29eb-122">Enterprise-grade security for apps and data</span></span>

### <a name="no-management-overhead"></a><span data-ttu-id="e29eb-123">Nie nakład pracy</span><span class="sxs-lookup"><span data-stu-id="e29eb-123">No management overhead</span></span>

* <span data-ttu-id="e29eb-124">Nie zewnętrznych zarządzania konto lub hasło</span><span class="sxs-lookup"><span data-stu-id="e29eb-124">No external account or password management</span></span>

* <span data-ttu-id="e29eb-125">Nie synchronizacji lub ręcznego zarządzania cyklem życia konta</span><span class="sxs-lookup"><span data-stu-id="e29eb-125">No sync or manual account lifecycle management</span></span>

* <span data-ttu-id="e29eb-126">Nie zewnętrznych koszty administracyjne</span><span class="sxs-lookup"><span data-stu-id="e29eb-126">No external administrative overhead</span></span>

## <a name="you-can-easily-add-b2b-collaboration-users-to-your-organization"></a><span data-ttu-id="e29eb-127">Łatwo można dodawać użytkowników współpracy B2B organizacji</span><span class="sxs-lookup"><span data-stu-id="e29eb-127">You can easily add B2B collaboration users to your organization</span></span>

<span data-ttu-id="e29eb-128">Administratorzy mogą dodać użytkowników (Gość) współpracy B2B w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e29eb-128">Admins can add B2B collaboration (guest) users in the [Azure portal](https://portal.azure.com).</span></span>

![Dodaj gości](media/active-directory-b2b-what-is-azure-ad-b2b/adding-b2b-users-admin.png)

### <a name="enable-your-collaborators-to-bring-their-own-identity"></a><span data-ttu-id="e29eb-130">Włącz Twojej współpracowników do ich własnych tożsamości</span><span class="sxs-lookup"><span data-stu-id="e29eb-130">Enable your collaborators to bring their own identity</span></span>

<span data-ttu-id="e29eb-131">B2B współpracownicy mogą zalogować się przy użyciu tożsamości siebie.</span><span class="sxs-lookup"><span data-stu-id="e29eb-131">B2B collaborators can sign in with an identity of their choice.</span></span> <span data-ttu-id="e29eb-132">Jeśli użytkownik nie ma konta Microsoft lub konta usługi Azure AD — utworzenia dla nich bezproblemowo w czasie na realizację oferty.</span><span class="sxs-lookup"><span data-stu-id="e29eb-132">If the user doesn’t have a Microsoft account or an Azure AD account – one is created for them seamlessly at the time for offer redemption.</span></span>

![Wybór logowania tożsamości](media/active-directory-b2b-what-is-azure-ad-b2b/sign-in-identity-choice.png)

### <a name="delegate-to-application-and-group-owners"></a><span data-ttu-id="e29eb-134">Deleguj do aplikacji i właścicieli grupy</span><span class="sxs-lookup"><span data-stu-id="e29eb-134">Delegate to application and group owners</span></span> 
<span data-ttu-id="e29eb-135">Aplikacji i właścicieli grupy można dodać B2B użytkowników bezpośrednio do dowolnej aplikacji, która Cię interesuje, czy nie jest on aplikacji firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e29eb-135">Application and group owners can add B2B users directly to any application that you care about, whether it is a Microsoft application or not.</span></span> <span data-ttu-id="e29eb-136">Administratorzy mogą delegować uprawnienia do dodawania użytkowników B2B do innych niż administratorzy.</span><span class="sxs-lookup"><span data-stu-id="e29eb-136">Admins can delegate permission to add B2B users to non-admins.</span></span> <span data-ttu-id="e29eb-137">Użytkownicy inni niż administratorzy mogą używać [Panel dostępu do aplikacji w usłudze Azure AD](https://myapps.microsoft.com) do dodawania użytkowników współpracy B2B do aplikacji lub grupy.</span><span class="sxs-lookup"><span data-stu-id="e29eb-137">Non-admins can use the [Azure AD Application Access Panel](https://myapps.microsoft.com) to add B2B collaboration users to applications or groups.</span></span>

![panel dostępu](media/active-directory-b2b-what-is-azure-ad-b2b/access-panel.png)

![Dodawanie elementu członkowskiego](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="authorization-policies-protect-your-corporate-content"></a><span data-ttu-id="e29eb-140">Zasady autoryzacji ochrony zawartości w sieci firmowej</span><span class="sxs-lookup"><span data-stu-id="e29eb-140">Authorization policies protect your corporate content</span></span>

<span data-ttu-id="e29eb-141">Zasady dostępu warunkowego, takich jak uwierzytelnianie wieloskładnikowe, można wymusić:</span><span class="sxs-lookup"><span data-stu-id="e29eb-141">Conditional access policies, such as multi-factor authentication, can be enforced:</span></span>
- <span data-ttu-id="e29eb-142">Na poziomie dzierżawy</span><span class="sxs-lookup"><span data-stu-id="e29eb-142">At the tenant level</span></span>
- <span data-ttu-id="e29eb-143">Na poziomie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e29eb-143">At the application level</span></span>
- <span data-ttu-id="e29eb-144">Dla określonych użytkowników dotyczące ochrony danych i aplikacji firmowych</span><span class="sxs-lookup"><span data-stu-id="e29eb-144">For specific users to protect corporate apps and data</span></span>

![Dodawanie elementu członkowskiego](media/active-directory-b2b-what-is-azure-ad-b2b/add-member.png)

### <a name="use-our-apis-and-sample-code-to-easily-build-applications-to-onboard"></a><span data-ttu-id="e29eb-146">Przy użyciu naszych interfejsów API, a przykładowy kod umożliwia łatwe tworzenie aplikacji do dołączenia</span><span class="sxs-lookup"><span data-stu-id="e29eb-146">Use our APIs and sample code to easily build applications to onboard</span></span>
<span data-ttu-id="e29eb-147">Przełącz z partnerami zewnętrznymi na statku w sposób dostosowany do potrzeb organizacji.</span><span class="sxs-lookup"><span data-stu-id="e29eb-147">Bring your external partners on board in ways customized to your organization’s needs.</span></span>

<span data-ttu-id="e29eb-148">Przy użyciu [zaproszenia współpracy B2B interfejsów API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), można dostosować komfort dołączania, w tym tworzenie portale Samoobsługowe dla rejestracji.</span><span class="sxs-lookup"><span data-stu-id="e29eb-148">Using the [B2B collaboration invitation APIs](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation), you can customize your onboarding experiences, including creating self-service sign-up portals.</span></span> <span data-ttu-id="e29eb-149">Firma Microsoft udostępnia kodu do portal samoobsługowy [w serwisie Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="e29eb-149">We provide sample code for a self-service portal [on Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

![portal rejestracji](media/active-directory-b2b-what-is-azure-ad-b2b/sign-up-portal.png)

<span data-ttu-id="e29eb-151">Współpracy B2B usługi Azure AD możesz uzyskać pełną moc usługi Azure AD, aby chronić Twoje relacje z partnerami w taki sposób, aby znaleźć użytkownikom końcowym proste i intuicyjne.</span><span class="sxs-lookup"><span data-stu-id="e29eb-151">With Azure AD B2B collaboration, you can get the full power of Azure AD to protect your partner relationships in a way that end users find easy and intuitive.</span></span> <span data-ttu-id="e29eb-152">Dlatego dalej, Dołącz do tysięcy organizacji, które już używają B2B usługi Azure AD dla ich współpracy zewnętrznej!</span><span class="sxs-lookup"><span data-stu-id="e29eb-152">So go ahead, join the thousands of organizations that are already using Azure AD B2B for their external collaboration!</span></span>

## <a name="next-steps"></a><span data-ttu-id="e29eb-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e29eb-153">Next steps</span></span>

* <span data-ttu-id="e29eb-154">Administrator środowiska znajdują się w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e29eb-154">Administrator experiences are found in the [Azure portal](https://portal.azure.com).</span></span>

* <span data-ttu-id="e29eb-155">Informacje środowiska roboczego są dostępne w [panelu dostępu](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="e29eb-155">Information worker experiences are available in the [Access Panel](https://myapps.microsoft.com).</span></span>

* <span data-ttu-id="e29eb-156">I jak zawsze Uzyskuj dostęp do zespołu produktu, opinii, dyskusji i sugestie za pośrednictwem naszego [społeczność techniczna Microsoft](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span><span class="sxs-lookup"><span data-stu-id="e29eb-156">And, as always, connect with the product team for any feedback, discussions, and suggestions through our [Microsoft Tech Community](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-B2B/bd-p/AzureAD_B2b).</span></span>

<span data-ttu-id="e29eb-157">Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e29eb-157">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="e29eb-158">Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="e29eb-158">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="e29eb-159">Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?</span><span class="sxs-lookup"><span data-stu-id="e29eb-159">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="e29eb-160">Elementy współpracy B2B zaproszenie</span><span class="sxs-lookup"><span data-stu-id="e29eb-160">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="e29eb-161">Realizacji zaproszenia współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="e29eb-161">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="e29eb-162">Azure licencjonowania współpracy B2B usługi AD</span><span class="sxs-lookup"><span data-stu-id="e29eb-162">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="e29eb-163">Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="e29eb-163">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="e29eb-164">Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)</span><span class="sxs-lookup"><span data-stu-id="e29eb-164">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="e29eb-165">Dostosowywanie i Azure Active Directory B2B współpracy interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e29eb-165">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="e29eb-166">Usługa Multi-Factor Authentication dla użytkowników współpracy B2B</span><span class="sxs-lookup"><span data-stu-id="e29eb-166">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="e29eb-167">Dodawanie użytkowników współpracy B2B bez zaproszenia</span><span class="sxs-lookup"><span data-stu-id="e29eb-167">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="e29eb-168">Użytkownik współpracy B2B inspekcji i raportowanie</span><span class="sxs-lookup"><span data-stu-id="e29eb-168">B2B collaboration user auditing and reporting</span></span>](active-directory-b2b-auditing-and-reporting.md)
* [<span data-ttu-id="e29eb-169">Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e29eb-169">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
