---
title: "aaaAzure dostępu warunkowego w usłudze Active Directory — często zadawane pytania | Dokumentacja firmy Microsoft"
description: "Uzyskaj odpowiedzi toofrequently zadawane pytania dotyczące dostępu warunkowego w usłudze Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Dostęp warunkowy usługi Azure Active Directory — często zadawane pytania

## <a name="which-applications-work-with-conditional-access-policies"></a>Aplikacje, które współpracuje z zasad dostępu warunkowego?

Aby uzyskać informacje o aplikacjach, które współpracują z zasadami dostępu warunkowego, zobacz [aplikacji i przeglądarki, które używały zasady dostępu warunkowego w usłudze Azure Active Directory](active-directory-conditional-access-supported-apps.md).

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>Zasady dostępu warunkowego są wymuszane dla współpracy B2B i gości?

Zasady są wymuszane dla biznesowych między firmami (B2B) współpracy użytkowników. Jednak w niektórych przypadkach użytkownik nie może być wymagań zasad hello toosatisfy stanie. Na przykład organizacja użytkownika gościa mogą nie obsługiwać uwierzytelnianie wieloskładnikowe. 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>Zasady usługi SharePoint Online również dotyczy tooOneDrive dla firm?

Tak. Zasady usługi SharePoint Online ma również zastosowanie tooOneDrive dla firm.


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>Dlaczego nie można ustawić zasad w aplikacjach klienckich, takich jak Word i Outlook?

Zasady dostępu warunkowego Ustawia wymagania dotyczące uzyskiwania dostępu do usługi. Te funkcje są wprowadzane podczas uwierzytelniania toothat usługi. Nie ustawiono zasad Hello bezpośrednio w aplikacji klienta. Zamiast tego jest stosowana, gdy klient wywołuje usługę. Na przykład zasadami ustawionymi w usłudze SharePoint dotyczy tooclients wywoływania programu SharePoint. Zestaw na serwerze Exchange zasad dotyczy tooOutlook.

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>Zasady dostępu warunkowego dotyczy tooservice kont?

Zasady dostępu warunkowego są stosowane tooall kont użytkowników. Obejmuje to konta użytkowników, które są używane jako konta usługi. Często konta usługi, który uruchamia instalacji nienadzorowanej nie spełnia wymagania hello zasady dostępu warunkowego. Na przykład uwierzytelnianie wieloskładnikowe może być wymagane. Konta usług można wykluczyć z zasady przy użyciu ustawień zarządzania zasad dostępu warunkowego. 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>Interfejsy API Graph są dostępne do konfigurowania zasad dostępu warunkowego?

Aktualnie nie. 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>Co to jest hello domyślne wykluczenia zasady dla platform nieobsługiwanego urządzenia?

Obecnie zasady dostępu warunkowego selektywnie są wymuszane dla użytkowników urządzeń iOS i Android. Aplikacje na innych platformach urządzeń domyślnie nie dotyczy hello zasady dostępu warunkowego dla urządzeń iOS i Android. Administrator dzierżawy można wybrać toooverride hello globalne zasady toodisallow dostępu toousers na platformach, które nie są obsługiwane.


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>Jak działają zasady dostępu warunkowego dla Teams firmy Microsoft?  

Microsoft Teams zależy od silnie usługi Exchange Online i SharePoint Online w podstawowe scenariusze wydajności, takich jak spotkania, kalendarzy i udostępnianie plików. Zasady dostępu warunkowego, które są ustawione dla tych aplikacji w chmurze zastosować tooMicrosoft zespołów po zalogowaniu użytkownika.

Teams Microsoft również jest obsługiwane oddzielnie jako aplikacji w chmurze w usłudze Azure Active Directory zasady dostępu warunkowego. Zasady urzędu certyfikatów, które są ustawione dla aplikacji w chmurze zastosować tooMicrosoft zespołów po zalogowaniu użytkownika.

Klienci usług pulpitu Teams firmy Microsoft dla systemu Windows i Mac obsługuje nowoczesnego uwierzytelniania. Nowoczesne uwierzytelniane umożliwia logowanie oparte na aplikacje klienckie pakietu Office tooMicrosoft interfejsów Azure Active Directory Authentication Library (ADAL) hello na platformach. 
