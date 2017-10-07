---
title: "zasady aaaAzure usługi Active Directory dostępu warunkowego urządzeń dla usług Office 365 | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat sposobu tooprovision dostępu warunkowego urządzeń zasady toohelp zasobów firmowych lepiej zabezpieczyć, przy zachowaniu tooservices zgodności i dostęp użytkownika."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8664c0bb-bba1-4012-b321-e9c8363080a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 38229a8d9766efbf0e6b17875b3018011c6b4ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="active-directory-conditional-access-device-policies-for-office-365-services"></a>Active Directory dostępu warunkowego zasady urządzeń dla usług Office 365

Dostęp warunkowy wymaga wielu toowork części. Obejmuje usługi Multi-Factor uwierzytelnianego użytkownika uwierzytelnionego urządzenia i zgodnych urządzeń, między innymi. W tym artykule firma Microsoft głównie skupić się na warunki oparta na urządzeniach, że organizacja może używać toohelp kontroli dostępu do usług 365 tooOffice. 

Firmy użytkownicy mają usługi tooaccess usługi Office 365, takie jak Exchange i SharePoint Online w pracy lub nauki z urządzeń osobistych. Witaj toobe dostępu ma bezpiecznego. Można udostępnić dostępu warunkowego urządzeń zasady toohelp upewnij zasobów firmowych bezpieczniejsze jednocześnie udzielać dostępu tooservices dla użytkowników, którzy korzystają ze zgodnych urządzeń. TooOffice zasady dostępu warunkowego 365 można ustawić w hello Microsoft Intune warunkowego dostępu do portalu.

Azure Active Directory (Azure AD) wymusza stosowanie dostępu warunkowego zasady toohelp bezpiecznego dostępu tooOffice 365 usług. Można utworzyć zasady dostępu warunkowego, która blokuje użytkownika, który używa urządzenia niezgodne z uzyskiwanie dostępu do usługi Office 365. przed uzyskaniem dostępu do usługi toohello Hello użytkownika muszą być zgodne zasady urządzeń toohello firmy. Alternatywnie można utworzyć zasadę, która wymaga tooenroll użytkowników tooan dostęp do swoich urządzeń toogain usługi Office 365. Zasady mogą być zastosowane tooall użytkowników w organizacji lub ograniczone tooa kilka grup docelowych. Wraz z upływem czasu, można dodać więcej zasad tooa grup docelowych.

Wymagane w przypadku wymuszania zasad urządzeń to użytkownicy muszą zarejestrować swoje urządzenia przy użyciu usługi rejestracji urządzeń hello Azure AD. Można włączyć tooturn na uwierzytelnianie wieloskładnikowe dla urządzeń, które rejestrują z hello usługi rejestracji urządzeń usługi Azure AD. Uwierzytelnianie wieloskładnikowe jest zalecane hello usługi rejestracji urządzeń usługi Azure Active Directory. Po włączeniu usługi Multi-Factor authentication dla uwierzytelniania dwuskładnikowego wąskie użytkownikom rejestrowanie swoich urządzeń w hello usługi rejestracji urządzeń usługi Azure AD.

## <a name="how-does-a-conditional-access-policy-work"></a>Jak działa zasady dostępu warunkowego?

Gdy użytkownik zażąda tooan dostępu do usługi Office 365 z platform obsługiwanych urządzeń, usługi Azure AD uwierzytelnia użytkownika hello i hello urządzenia. Usługa Azure AD udziela dostępu toohello tylko wtedy, gdy hello użytkownika spełnia zasady toohello ustawione hello usługi. Użytkownicy na urządzeniach, które nie są zarejestrowane otrzymuje instrukcje na temat tooenroll i stać się zgodne tooaccess firmowych usługi Office 365. Użytkownicy w systemach iOS i urządzeniach z systemem Android są wymagane tooenroll urządzeń przy użyciu aplikacji Portal firmy usługi Intune hello. Gdy użytkownik rejestruje urządzenia, hello urządzenie jest zarejestrowane w usłudze Azure AD i jest ono zarejestrowane na potrzeby zarządzania urządzeniami i zgodności. Należy użyć usługi rejestracji urządzeń usługi Azure AD hello usłudze Microsoft Intune do zarządzania urządzeniami przenośnymi dla usługi Office 365. Rejestracja urządzeń jest wymagane dla tooaccess użytkowników usługi Office 365, gdy urządzenie zasady są wymuszane.

Gdy użytkownik pomyślnie rejestruje urządzenia, urządzenia hello staje się zaufany. Usługi Azure AD zapewnia hello uwierzytelniony użytkownik dostępu rejestracji jednokrotnej toocompany aplikacji. Usługi Azure AD wymusza stosowanie dostępu warunkowego zasad toogrant dostępu tooa usługi nie tylko hello pierwszego czasu hello użytkownik żąda dostępu, ale każdy użytkownik hello czasu odnawia na żądanie dostępu. Podczas poświadczenia logowania są zmieniane, utraty lub kradzieży urządzenia hello lub w czasie hello żądania odnowienia nie są spełnione warunki hello hello zasad, Hello użytkownik otrzyma odmowę dostępu tooservices.

## <a name="deployment-considerations"></a>Zagadnienia dotyczące wdrażania

Należy użyć urządzenia tooregister usługi rejestracji urządzeń usługi Azure AD hello.

Kiedy są lokalnych użytkowników o uwierzytelnieniu toobe Active Directory Federation Services (AD FS) (w wersji 1.0 lub nowszym) jest wymagana. Uwierzytelnianie wieloskładnikowe dla dołączania nie powiedzie się, gdy hello dostawcy tożsamości nie jest zdolny do usługi Multi-Factor Authentication. Na przykład nie można użyć uwierzytelniania wieloskładnikowego z usługami AD FS 2.0. Upewnij się, że hello lokalnych usług AD FS działa przy użyciu uwierzytelniania wieloskładnikowego i czy metoda prawidłowy uwierzytelnianie wieloskładnikowe jest w miejscu przed włączeniem uwierzytelniania wieloskładnikowego dla usługi rejestracji urządzeń usługi Azure AD hello. Na przykład usługi AD FS w systemie Windows Server 2012 R2 ma funkcje usługi Multi-Factor authentication. Należy również ustawić metodę dodatkowe prawidłowy uwierzytelniania (uwierzytelnianie wieloskładnikowe) na serwerze usług AD FS hello przed włączeniem uwierzytelniania wieloskładnikowego dla usługi rejestracji urządzeń hello Azure AD. Aby uzyskać więcej informacji na temat metod obsługiwanych uwierzytelnianie wieloskładnikowe w usługach AD FS, zobacz [Konfigurowanie dodatkowych metod uwierzytelniania usług AD FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs).

## <a name="next-steps"></a>Następne kroki

*   Aby uzyskać odpowiedzi na pytania toocommon, zobacz [dostępu warunkowego w usłudze Azure Active Directory — często zadawane pytania](active-directory-conditional-faqs.md).
