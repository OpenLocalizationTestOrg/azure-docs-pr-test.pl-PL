---
title: "Azure AD Connect: Uwierzytelniania przekazywanego — jak to działa? | Microsoft Docs"
description: "W tym artykule opisano, jak działa uwierzytelniania przekazywanego Azure Active Directory."
services: active-directory
keywords: "Azure AD Connect przekazywanego uwierzytelniania, instalacji usługi Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: d34ccd40082edbe036d963ad548bff648119bdd4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="a6fa7-105">Azure przekazywanego uwierzytelnianie usługi Active Directory: Techniczne nowości</span><span class="sxs-lookup"><span data-stu-id="a6fa7-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="a6fa7-106">Azure AD przekazywanego uwierzytelniania jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="a6fa7-107">Jak działa uwierzytelniania przekazywanego Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6fa7-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="a6fa7-108">Gdy użytkownik próbuje zalogować się do aplikacji zabezpieczonej przez usługi Azure Active Directory (Azure AD) i przekazywanego uwierzytelniania jest włączona w ramach dzierżawy, zostaną wykonane następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="a6fa7-108">When a user attempts to sign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on the tenant, the following steps occur:</span></span>

1. <span data-ttu-id="a6fa7-109">Użytkownik próbuje uzyskać dostęp do aplikacji (na przykład Outlook Web App - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="a6fa7-109">The user tries to access an application (for example, the Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="a6fa7-110">Jeśli użytkownik nie jest już zalogowany, użytkownik jest przekierowany do strony logowania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-110">If the user is not already signed in, the user is redirected to the Azure AD sign-in page.</span></span>
3. <span data-ttu-id="a6fa7-111">Użytkownik wprowadza nazwę użytkownika i hasło do strony logowania usługi Azure AD i kliknie przycisk "Zaloguj".</span><span class="sxs-lookup"><span data-stu-id="a6fa7-111">The user enters their username and password into the Azure AD sign-in page and clicks the "Sign in" button.</span></span>
4. <span data-ttu-id="a6fa7-112">Azure AD, po otrzymaniu żądania logowania umieszcza nazwy użytkownika i hasła (zaszyfrowane przy użyciu klucza publicznego) w kolejce.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-112">Azure AD, on receiving the sign-in request, places the username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="a6fa7-113">Agent przekazywanego uwierzytelniania lokalnego wykonuje wychodzące wywołanie do kolejki i pobiera nazwę użytkownika i hasło zaszyfrowane.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-113">An on-premises Pass-through Authentication agent makes an outbound call to the queue and retrieves the username and encrypted password.</span></span>
6. <span data-ttu-id="a6fa7-114">Agent odszyfrowuje hasła, używając swojego klucza prywatnego.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-114">The agent decrypts the password using its private key.</span></span>
7. <span data-ttu-id="a6fa7-115">Agent następnie weryfikuje nazwy użytkownika i hasła w usłudze Active Directory przy użyciu standardowych interfejsów API systemu Windows (podobny mechanizm co to jest używany przez usługi federacyjne Active Directory).</span><span class="sxs-lookup"><span data-stu-id="a6fa7-115">The agent then validates the username and password against Active Directory using standard Windows APIs (a similar mechanism to what is used by Active Directory Federation Services).</span></span> <span data-ttu-id="a6fa7-116">Nazwa użytkownika może być albo lokalnymi domyślna nazwa użytkownika (zwykle `userPrincipalName`) lub inny atrybut skonfigurowane w programie Azure AD Connect (nazywane `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="a6fa7-116">The username can be either the on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="a6fa7-117">Lokalnymi Active Directory domeny kontrolera (kontroler domeny), następnie ocenia żądanie i zwraca właściwą odpowiedź (Powodzenie, Niepowodzenie, hasło wygasło lub użytkownika zablokowane) do agenta.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-117">The on-premises Active Directory Domain Controller (DC) then evaluates the request and returns the appropriate response (success, failure, password expired or user locked out) to the agent.</span></span>
9. <span data-ttu-id="a6fa7-118">Agent, zwraca z kolei, to odpowiedź z powrotem do usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-118">The agent, in turn, returns this response back to Azure AD.</span></span>
10. <span data-ttu-id="a6fa7-119">Usługi Azure AD ocenia odpowiedzi i odpowiada użytkowników zależnie od potrzeb — na przykład jego loguje się użytkownik natychmiast albo żądań uwierzytelniania wieloskładnikowego (MFA).</span><span class="sxs-lookup"><span data-stu-id="a6fa7-119">Azure AD evaluates the response and responds to the user as appropriate - for example, it either signs the user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="a6fa7-120">Jeśli logowanie użytkowników zostanie nawiązane, użytkownik jest w stanie uzyskać dostęp do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-120">If the user sign-in is successful, the user is able to access the application.</span></span>

<span data-ttu-id="a6fa7-121">Na poniższym diagramie przedstawiono wszystkie składniki i kroki do wykonania.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-121">The following diagram illustrates all the components and the steps involved.</span></span>

![Przekazywanego uwierzytelniania](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="a6fa7-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a6fa7-123">Next steps</span></span>
- <span data-ttu-id="a6fa7-124">[**Bieżące ograniczenia** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) — ta funkcja jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="a6fa7-125">Dowiedz się, jakie scenariusze są obsługiwane i zostały.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="a6fa7-126">[**Szybki Start** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) — Uzyskaj i systemem Azure AD przekazywanego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="a6fa7-127">[**Często zadawane pytania** ](active-directory-aadconnect-pass-through-authentication-faq.md) — odpowiedzi na często zadawane pytania.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers to frequently asked questions.</span></span>
- <span data-ttu-id="a6fa7-128">[**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) — Dowiedz się, jak rozwiązać typowe problemy z funkcją.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="a6fa7-129">[**Azure AD SSO bezproblemowe** ](active-directory-aadconnect-sso.md) — Dowiedz się więcej o tej funkcji uzupełniające.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="a6fa7-130">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="a6fa7-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
