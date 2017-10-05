---
title: "Protokoły uwierzytelniania usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Omówienie protokoły obsługiwane przez usługi Azure Active Directory (AD)"
documentationcenter: dev-center-name
author: priyamohanram
services: active-directory
manager: mbaldwin
editor: 
ms.assetid: 7a838ae2-c24c-4304-b6c0-e77fb888e6c0
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 91416669281aa8eeef5916db008f9b0cbcbf77e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# Protokoły uwierzytelniania usługi Azure Active Directory
Azure Active Directory (Azure AD) obsługuje niektóre z najczęściej używanych protokołów uwierzytelniania i autoryzacji. W tematach w tej sekcji opisano obsługiwane protokoły i ich implementacji w usłudze Azure AD. Tematy zawarte Przegląd obsługiwane typy oświadczeń, wprowadzenie do używania w metadanych Federacji, szczegółowe OAuth 2.0. i dokumentację referencyjną protokołu SAML 2.0 i w sekcji rozwiązywania problemów.

## Protokoły uwierzytelniania artykułów i odwołania
* [Ważne informacje dotyczące podpisywania klucza przerzucania w usłudze Azure AD](active-directory-signing-key-rollover.md) — Dowiedz się więcej na temat usługi Azure AD podpisywania okresach Przerzucanie klucza, zmiany można automatycznie zaktualizować klucza oraz omówienie aktualizacji najbardziej typowych scenariuszy aplikacji.
* [Obsługiwane tokeny i oświadczenia](active-directory-token-and-claims.md) — więcej informacji dotyczących oświadczeń, w których usługa Azure AD wystawia tokeny.
* [Metadane Federacji](active-directory-federation-metadata.md) — Dowiedz się, jak znaleźć i interpretować dokumentów metadanych, które generuje usługi Azure AD.
* [OAuth 2.0 w usłudze Azure AD](active-directory-protocols-oauth-code.md) — Dowiedz się więcej o implementacji protokołu OAuth 2.0 w usłudze Azure AD.
* [OpenID Connect 1.0](active-directory-protocols-openid-connect-code.md) — Dowiedz się, jak jest używany do uwierzytelniania OAuth 2.0, protokół autoryzacji.
* [Wywołania usług przy użyciu poświadczeń klienta](active-directory-protocols-oauth-service-to-service.md) — używanie przepływ przyznania poświadczeń klienta OAuth 2.0 w wywołaniach usług.
* [Wywołania usług z przepływem On-Behalf-Of](active-directory-protocols-oauth-on-behalf-of.md) — Dowiedz się, jak używać przepływu OAuth 2.0 On-Behalf-Of w wywołaniach usług.
* [Referencyjne protokołu SAML](active-directory-saml-protocol-reference.md) — Dowiedz się więcej o rejestracji jednokrotnej i jednym SAML Sign-out profilów usługi Azure AD.

## Zobacz też
[Przewodnik dewelopera usługi Azure Active Directory](active-directory-developers-guide.md)

[Używanie programu Azure AD do uwierzytelniania](../../app-service-web/web-sites-authentication-authorization.md)

[Przykłady kodu usługi Active Directory](active-directory-code-samples.md)
