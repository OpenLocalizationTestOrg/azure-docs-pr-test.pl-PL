---
title: "Azure AD Connect: Bezproblemowe logowanie jednokrotne — jak działa | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak działa hello Azure Active Directory bezproblemowe logowanie jednokrotne funkcji."
services: active-directory
keywords: "Co to jest usługa Azure AD Connect, zainstaluj usługę Active Directory, wymaganych składników dla usługi Azure AD, SSO, Single Sign-on"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 17ce35b32832d241068ab878cf7aac42deab74ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-technical-deep-dive"></a><span data-ttu-id="28c9c-104">Azure Active Directory bezproblemowe logowanie jednokrotne: techniczne nowości</span><span class="sxs-lookup"><span data-stu-id="28c9c-104">Azure Active Directory Seamless Single Sign-On: Technical deep dive</span></span>

<span data-ttu-id="28c9c-105">Ten artykuł zawiera szczegółowe informacje techniczne, w sposób działania hello Azure Active Directory bezproblemowe rejestracji jednokrotnej (SSO bezproblemowe) funkcji.</span><span class="sxs-lookup"><span data-stu-id="28c9c-105">This article gives you technical details into how hello Azure Active Directory Seamless Single Sign-On (Seamless SSO) feature works.</span></span>

>[!IMPORTANT]
><span data-ttu-id="28c9c-106">funkcja logowania jednokrotnego bezproblemowe Hello jest obecnie w przeglądzie.</span><span class="sxs-lookup"><span data-stu-id="28c9c-106">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="how-does-seamless-sso-work"></a><span data-ttu-id="28c9c-107">Jak działa bezproblemowe logowanie Jednokrotne</span><span class="sxs-lookup"><span data-stu-id="28c9c-107">How does Seamless SSO work?</span></span>

<span data-ttu-id="28c9c-108">Ta sekcja zawiera dwa tooit części:</span><span class="sxs-lookup"><span data-stu-id="28c9c-108">This section has two parts tooit:</span></span>
1. <span data-ttu-id="28c9c-109">Ustawienia funkcji logowania jednokrotnego bezproblemowe hello Hello.</span><span class="sxs-lookup"><span data-stu-id="28c9c-109">hello setup of hello Seamless SSO feature.</span></span>
2. <span data-ttu-id="28c9c-110">Jak pojedynczego użytkownika logowania transakcji współpracuje z bezproblemowe logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="28c9c-110">How a single user sign-in transaction works with Seamless SSO.</span></span>

### <a name="how-does-set-up-work"></a><span data-ttu-id="28c9c-111">Jak skonfigurować pracy?</span><span class="sxs-lookup"><span data-stu-id="28c9c-111">How does set up work?</span></span>

<span data-ttu-id="28c9c-112">Bezproblemowe rejestracji Jednokrotnej jest włączone, za pomocą usługi Azure AD Connect, jak pokazano [tutaj](active-directory-aadconnect-sso-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="28c9c-112">Seamless SSO is enabled using Azure AD Connect as shown [here](active-directory-aadconnect-sso-quick-start.md).</span></span> <span data-ttu-id="28c9c-113">Podczas włączania funkcji hello, wykonywane hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="28c9c-113">While enabling hello feature, hello following steps occur:</span></span>
- <span data-ttu-id="28c9c-114">Konto komputera o nazwie `AZUREADSSOACCT` (reprezentuje usługi Azure AD) jest tworzony w lokalnej usłudze Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="28c9c-114">A computer account named `AZUREADSSOACCT` (which represents Azure AD) is created in your on-premises Active Directory (AD).</span></span>
- <span data-ttu-id="28c9c-115">klucz odszyfrowujący Kerberos konta komputera Hello jest udostępniony w bezpieczny sposób z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28c9c-115">hello computer account's Kerberos decryption key is shared securely with Azure AD.</span></span>
- <span data-ttu-id="28c9c-116">Ponadto dwóch Kerberos głównej nazwy usługi (SPN) są tworzone toorepresent dwa adresy URL, które są używane podczas logowania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28c9c-116">In addition, two Kerberos service principal names (SPNs) are created toorepresent two URLs that are used during Azure AD sign-in.</span></span>

>[!NOTE]
> <span data-ttu-id="28c9c-117">Hello konto komputera i nazwy SPN Kerberos hello są tworzone w każdym lesie usługi AD synchronizacji tooAzure AD (za pomocą usługi Azure AD Connect) oraz dla użytkowników, którzy mają bezproblemowe logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="28c9c-117">hello computer account and hello Kerberos SPNs are created in each AD forest you synchronize tooAzure AD (using Azure AD Connect) and for whose users you want Seamless SSO.</span></span> <span data-ttu-id="28c9c-118">Przenieś hello `AZUREADSSOACCT` tooan konta komputera jednostkę organizacji (OU) gdzie innych kont komputerów są przechowywane tooensure, który jest zarządzany w hello sam sposób i nie zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="28c9c-118">Move hello `AZUREADSSOACCT` computer account tooan Organization Unit (OU) where other computer accounts are stored tooensure that it is managed in hello same way and is not deleted.</span></span>

>[!IMPORTANT]
><span data-ttu-id="28c9c-119">Zdecydowanie zalecamy, aby użytkownik [Przerzuć klucz odszyfrowujący Kerberos hello](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) z hello `AZUREADSSOACCT` konta komputera co najmniej 30 dni.</span><span class="sxs-lookup"><span data-stu-id="28c9c-119">We highly recommend that you [roll over hello Kerberos decryption key](active-directory-aadconnect-sso-faq.md#how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account) of hello `AZUREADSSOACCT` computer account at least every 30 days.</span></span>

### <a name="how-does-sign-in-with-seamless-sso-work"></a><span data-ttu-id="28c9c-120">Jak logowanie SSO bezproblemowe pracy?</span><span class="sxs-lookup"><span data-stu-id="28c9c-120">How does sign-in with Seamless SSO work?</span></span>

<span data-ttu-id="28c9c-121">Po zakończeniu konfigurowania hello bezproblemowe logowanie Jednokrotne działa hello sam sposób jak inne logowania, która używa zintegrowanego uwierzytelniania systemu Windows (IWA).</span><span class="sxs-lookup"><span data-stu-id="28c9c-121">Once hello set-up is complete, Seamless SSO works hello same way as any other sign-in that uses Integrated Windows Authentication (IWA).</span></span> <span data-ttu-id="28c9c-122">przebieg Hello jest następujący:</span><span class="sxs-lookup"><span data-stu-id="28c9c-122">hello flow is as follows:</span></span>

1. <span data-ttu-id="28c9c-123">Witaj użytkownik spróbuje tooaccess aplikacji (na przykład Witaj aplikacji Outlook Web App - https://outlook.office365.com/owa/) z urządzenia firmowe przyłączonych do domeny w sieci firmowej.</span><span class="sxs-lookup"><span data-stu-id="28c9c-123">hello user tries tooaccess an application (for example, hello Outlook Web App - https://outlook.office365.com/owa/) from a domain-joined corporate device inside your corporate network.</span></span>
2. <span data-ttu-id="28c9c-124">Jeśli użytkownik hello nie jest już zalogowany, użytkownika hello jest strony logowania usługi Azure AD toohello przekierowane.</span><span class="sxs-lookup"><span data-stu-id="28c9c-124">If hello user is not already signed in, hello user is redirected toohello Azure AD sign-in page.</span></span>

  >[!NOTE]
  ><span data-ttu-id="28c9c-125">Jeśli żądanie logowania hello Azure AD zawiera `domain_hint` (identyfikowanie dzierżawy — na przykład, contoso.onmicrosoft.com) lub `login_hint` (identyfikacji użytkownika hello — na przykład user@contoso.onmicrosoft.com lub user@contoso.com) parametr, a następnie w kroku 2 jest pomijana.</span><span class="sxs-lookup"><span data-stu-id="28c9c-125">If hello Azure AD sign-in request includes a `domain_hint` (identifying your tenant- for example, contoso.onmicrosoft.com) or `login_hint` (identifying hello user - for example, user@contoso.onmicrosoft.com or user@contoso.com) parameter, then step 2 is skipped.</span></span>

3. <span data-ttu-id="28c9c-126">użytkownik wpisze Hello nazwy użytkownika do strony logowania hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="28c9c-126">hello user types in their user name into hello Azure AD sign-in page.</span></span>
4. <span data-ttu-id="28c9c-127">Przy użyciu języka JavaScript w tle hello, usługi Azure AD będzie wymagał hello przeglądarki, za pomocą odpowiedzi 401 nieautoryzowane, tooprovide biletu protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="28c9c-127">Using JavaScript in hello background, Azure AD challenges hello browser, via a 401 Unauthorized response, tooprovide a Kerberos ticket.</span></span>
5. <span data-ttu-id="28c9c-128">Przeglądarka Hello z kolei żąda biletu z usługi Active Directory dla hello `AZUREADSSOACCT` konta komputera (co reprezentuje usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="28c9c-128">hello browser, in turn, requests a ticket from Active Directory for hello `AZUREADSSOACCT` computer account (which represents Azure AD).</span></span>
6. <span data-ttu-id="28c9c-129">Usługi Active Directory lokalizuje hello konto komputera i zwraca przeglądarki toohello biletu Kerberos zaszyfrowane za pomocą konta komputera hello klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="28c9c-129">Active Directory locates hello computer account and returns a Kerberos ticket toohello browser encrypted with hello computer account's secret.</span></span>
7. <span data-ttu-id="28c9c-130">Przeglądarka Hello przekazuje on uzyskane z usługi Active Directory tooAzure AD biletu Kerberos hello (na jednym z hello [Azure AD adresy URL wcześniej dodane ustawienia strefy Intranet w przeglądarce toohello](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span><span class="sxs-lookup"><span data-stu-id="28c9c-130">hello browser forwards hello Kerberos ticket it acquired from Active Directory tooAzure AD (on one of hello [Azure AD URLs previously added toohello browser's Intranet zone settings](active-directory-aadconnect-sso-quick-start.md#step-3-roll-out-the-feature)).</span></span>
8. <span data-ttu-id="28c9c-131">Azure AD odszyfrowywane hello biletu Kerberos, obejmujące hello tożsamości użytkownika hello zalogowaniem się do urządzeń firmowych hello wcześniej przy użyciu hello wspólny klucz.</span><span class="sxs-lookup"><span data-stu-id="28c9c-131">Azure AD decrypts hello Kerberos ticket, which includes hello identity of hello user signed into hello corporate device, using hello previously shared key.</span></span>
9. <span data-ttu-id="28c9c-132">Po dokonaniu oceny usługi Azure AD zwraca aplikacji toohello tyłu tokenu lub zapyta tooperform użytkownika hello dodatkowe dowody, takich jak uwierzytelnianie wieloskładnikowe.</span><span class="sxs-lookup"><span data-stu-id="28c9c-132">After evaluation, Azure AD either returns a token back toohello application or asks hello user tooperform additional proofs, such as Multi-Factor Authentication.</span></span>
10. <span data-ttu-id="28c9c-133">Jeśli logowanie użytkownika hello zakończy się pomyślnie, użytkownik hello jest aplikacji hello tooaccess stanie.</span><span class="sxs-lookup"><span data-stu-id="28c9c-133">If hello user sign-in is successful, hello user is able tooaccess hello application.</span></span>

<span data-ttu-id="28c9c-134">Witaj poniższym diagramie przedstawiono wszystkie składniki hello i hello etapy.</span><span class="sxs-lookup"><span data-stu-id="28c9c-134">hello following diagram illustrates all hello components and hello steps involved.</span></span>

![Bezproblemowe logowanie jednokrotne](./media/active-directory-aadconnect-sso/sso2.png)

<span data-ttu-id="28c9c-136">Bezproblemowe rejestracji Jednokrotnej jest oportunistyczne, co oznacza, że w przypadku niepowodzenia hello logowania powraca zachowanie regularne tooits - tj, hello użytkownik powinien tooenter toosign ich haseł w.</span><span class="sxs-lookup"><span data-stu-id="28c9c-136">Seamless SSO is opportunistic, which means if it fails, hello sign-in experience falls back tooits regular behavior - i.e, hello user needs tooenter their password toosign in.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28c9c-137">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28c9c-137">Next steps</span></span>

- <span data-ttu-id="28c9c-138">[**Szybki Start** ](active-directory-aadconnect-sso-quick-start.md) — Uzyskaj i systemem Azure AD bezproblemowe Usługa rejestracji Jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="28c9c-138">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="28c9c-139">[**Często zadawane pytania** ](active-directory-aadconnect-sso-faq.md) -odpowiedzi toofrequently zadawane pytania.</span><span class="sxs-lookup"><span data-stu-id="28c9c-139">[**Frequently Asked Questions**](active-directory-aadconnect-sso-faq.md) - Answers toofrequently asked questions.</span></span>
- <span data-ttu-id="28c9c-140">[**Rozwiązywanie problemów z** ](active-directory-aadconnect-troubleshoot-sso.md) — Dowiedz się, jak tooresolve typowe problemy związane z funkcją hello.</span><span class="sxs-lookup"><span data-stu-id="28c9c-140">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="28c9c-141">[**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) — w przypadku zgłoszenia żądania nowych funkcji.</span><span class="sxs-lookup"><span data-stu-id="28c9c-141">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
