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
ms.openlocfilehash: ffcebee572a9ba2840e81250651dea45599d65d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-technical-deep-dive"></a><span data-ttu-id="cefa6-105">Azure przekazywanego uwierzytelnianie usługi Active Directory: Techniczne nowości</span><span class="sxs-lookup"><span data-stu-id="cefa6-105">Azure Active Directory Pass-through Authentication: Technical deep dive</span></span>

>[!IMPORTANT]
><span data-ttu-id="cefa6-106">Azure AD przekazywanego uwierzytelniania jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="cefa6-106">Azure AD Pass-through Authentication is currently in preview.</span></span> 

## <a name="how-does-azure-active-directory-pass-through-authentication-work"></a><span data-ttu-id="cefa6-107">Jak działa uwierzytelniania przekazywanego Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cefa6-107">How does Azure Active Directory Pass-through Authentication work?</span></span>

<span data-ttu-id="cefa6-108">Gdy użytkownik próbuje toosign do aplikacji zabezpieczonej przez usługi Azure Active Directory (Azure AD) i włączenie uwierzytelniania przekazywanego dzierżawcy hello hello są wykonywane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cefa6-108">When a user attempts toosign into an application secured by Azure Active Directory (Azure AD), and if Pass-through Authentication is enabled on hello tenant, hello following steps occur:</span></span>

1. <span data-ttu-id="cefa6-109">Witaj użytkownik spróbuje tooaccess aplikacji (na przykład Witaj aplikacji Outlook Web App - https://outlook.office365.com/owa/).</span><span class="sxs-lookup"><span data-stu-id="cefa6-109">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/).</span></span>
2. <span data-ttu-id="cefa6-110">Jeśli użytkownik hello nie jest już zalogowany, użytkownika hello jest strony logowania usługi Azure AD toohello przekierowane.</span><span class="sxs-lookup"><span data-stu-id="cefa6-110">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>
3. <span data-ttu-id="cefa6-111">Hello użytkownik wprowadza nazwę użytkownika i hasło do strony logowania usługi Azure AD hello i kliknie przycisk "Zaloguj" hello.</span><span class="sxs-lookup"><span data-stu-id="cefa6-111">hello user enters their username and password into hello Azure AD sign-in page and clicks hello "Sign in" button.</span></span>
4. <span data-ttu-id="cefa6-112">Usługi Azure AD na powitania logowania żądania odbierania umieszcza hello nazwy użytkownika i hasła (zaszyfrowane przy użyciu klucza publicznego) w kolejce.</span><span class="sxs-lookup"><span data-stu-id="cefa6-112">Azure AD, on receiving hello sign-in request, places hello username and password (encrypted  using a public key) on a queue.</span></span>
5. <span data-ttu-id="cefa6-113">Agent uwierzytelniania przekazywanego lokalnymi sprawia, że kolejka toohello wywołań wychodzących i pobiera hello nazwy użytkownika i hasła szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="cefa6-113">An on-premises Pass-through Authentication agent makes an outbound call toohello queue and retrieves hello username and encrypted password.</span></span>
6. <span data-ttu-id="cefa6-114">Hello agent odszyfrowuje hello hasła przy użyciu jego klucz prywatny.</span><span class="sxs-lookup"><span data-stu-id="cefa6-114">hello agent decrypts hello password using its private key.</span></span>
7. <span data-ttu-id="cefa6-115">Hello agent sprawdza następnie hello nazwy użytkownika i hasła w usłudze Active Directory przy użyciu standardowych interfejsów API systemu Windows (podobne toowhat mechanizm jest używany przez usługi federacyjne Active Directory).</span><span class="sxs-lookup"><span data-stu-id="cefa6-115">hello agent then validates hello username and password against Active Directory using standard Windows APIs (a similar mechanism toowhat is used by Active Directory Federation Services).</span></span> <span data-ttu-id="cefa6-116">Witaj nazwa użytkownika może być albo hello lokalnymi domyślna nazwa użytkownika (zwykle `userPrincipalName`) lub inny atrybut skonfigurowane w programie Azure AD Connect (nazywane `Alternate ID`).</span><span class="sxs-lookup"><span data-stu-id="cefa6-116">hello username can be either hello on-premises default username (usually `userPrincipalName`) or another attribute configured in Azure AD Connect (known as `Alternate ID`).</span></span>
8. <span data-ttu-id="cefa6-117">Witaj lokalnego kontrolera domeny Active Directory (DC), a następnie oblicza hello żądania i zwraca hello właściwą odpowiedź (Powodzenie, Niepowodzenie, hasło wygasło lub użytkownika zablokowane) toohello agenta.</span><span class="sxs-lookup"><span data-stu-id="cefa6-117">hello on-premises Active Directory Domain Controller (DC) then evaluates hello request and returns hello appropriate response (success, failure, password expired or user locked out) toohello agent.</span></span>
9. <span data-ttu-id="cefa6-118">Hello agent zwraca z kolei tej odpowiedzi tooAzure wstecz AD.</span><span class="sxs-lookup"><span data-stu-id="cefa6-118">hello agent, in turn, returns this response back tooAzure AD.</span></span>
10. <span data-ttu-id="cefa6-119">Usługi Azure AD ocenia hello odpowiedzi i odpowiada toohello użytkowników zależnie od potrzeb — na przykład jego zalogowaniu użytkownika hello natychmiast albo żądań uwierzytelniania wieloskładnikowego (MFA).</span><span class="sxs-lookup"><span data-stu-id="cefa6-119">Azure AD evaluates hello response and responds toohello user as appropriate - for example, it either signs hello user in immediately or requests for Multi-Factor Authentication (MFA).</span></span>
11. <span data-ttu-id="cefa6-120">Jeśli logowanie użytkownika hello zakończy się pomyślnie, użytkownik hello jest aplikacji hello tooaccess stanie.</span><span class="sxs-lookup"><span data-stu-id="cefa6-120">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="cefa6-121">Witaj poniższym diagramie przedstawiono wszystkie składniki hello i hello etapy.</span><span class="sxs-lookup"><span data-stu-id="cefa6-121">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Uwierzytelnianie przekazywane](./media/active-directory-aadconnect-pass-through-authentication/pta2.png)

## <a name="next-steps"></a><span data-ttu-id="cefa6-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cefa6-123">Next steps</span></span>
- <span data-ttu-id="cefa6-124">[**Bieżące ograniczenia** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) — ta funkcja jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="cefa6-124">[**Current limitations**](active-directory-aadconnect-pass-through-authentication-current-limitations.md) - This feature is currently in preview.</span></span> <span data-ttu-id="cefa6-125">Dowiedz się, jakie scenariusze są obsługiwane i zostały.</span><span class="sxs-lookup"><span data-stu-id="cefa6-125">Learn which scenarios are supported and which ones are not.</span></span>
- <span data-ttu-id="cefa6-126">[**Szybki Start** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) — Uzyskaj i systemem Azure AD przekazywanego uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="cefa6-126">[**Quick Start**](active-directory-aadconnect-pass-through-authentication-quick-start.md) - Get up and running Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="cefa6-127">[**Często zadawane pytania** ](active-directory-aadconnect-pass-through-authentication-faq.md) -odpowiedzi toofrequently zadawane pytania.</span><span class="sxs-lookup"><span data-stu-id="cefa6-127">[**Frequently Asked Questions**](active-directory-aadconnect-pass-through-authentication-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="cefa6-128">[**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.</span><span class="sxs-lookup"><span data-stu-id="cefa6-128">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="cefa6-129">[**Azure AD SSO bezproblemowe** ](active-directory-aadconnect-sso.md) — Dowiedz się więcej o tej funkcji uzupełniające.</span><span class="sxs-lookup"><span data-stu-id="cefa6-129">[**Azure AD Seamless SSO**](active-directory-aadconnect-sso.md) - Learn more about this complementary feature.</span></span>
- <span data-ttu-id="cefa6-130">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="cefa6-130">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
