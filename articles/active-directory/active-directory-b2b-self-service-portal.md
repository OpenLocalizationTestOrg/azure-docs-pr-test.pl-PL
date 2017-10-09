---
title: "portalu tworzenia konta usługi aaaSelf współpracy usługi Azure Active Directory B2B | Dokumentacja firmy Microsoft"
description: "Współpraca z usługą Azure Active Directory B2B obsługuje relacji między firmami przez włączenie dostępu tooselectively partnerów biznesowych aplikacji firmowych"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a>Portal samoobsługowy do zapisywania do współpracy B2B usługi Azure AD

Klienci mogą wykonywanie wielu hello wbudowane funkcje, które są dostępne za pośrednictwem naszego administrator IT [portalu Azure](https://portal.azure.com) i naszych [panelu dostępu aplikacji](https://myapps.microsoft.com) dla użytkowników końcowych. Ale możemy również pamiętać, że firmy muszą przepływ pracy dołączania hello toocustomize dla toofit użytkowników B2B potrzeb organizacji. Można wykonać z [interfejsach API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).

W dyskusjach ze specjalistami z naszych klientów widzimy się, że jeden wspólny wjazd należy przede wszystkim innym. Witaj zapraszanie organizacji może nie wiedzieć wcześniejsze kto hello poszczególnych zewnętrznych współpracowników są, który muszą uzyskać dostęp do zasobów tootheir. Chcieli sposób dla użytkowników z firm partnerskich zbyt Zarejestruj się z zestawem zasad tego hello zapraszanie formanty organizacji. Ten scenariusz jest możliwe za pośrednictwem naszych interfejsów API, dlatego firma Microsoft opublikowane projektu w witrynie Github, która została właśnie tę: [przykładowy projekt Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).

Nasze projektu Github pokazano, jak organizacji można użyć naszych interfejsów API i podaj opartych na zasadach, Samoobsługowe możliwość zapisywania do zaufanych partnerów z zasad określających hello aplikacje, które mogą uzyskiwać dostęp do. Użytkowników z firm partnerskich można uzyskać dostępu tooresources, gdy to konieczne, bezpieczne, bez konieczności hello zapraszanie dołączyć toomanually organizacji je. Możesz z łatwością wdrożyć hello projektu do subskrypcji platformy Azure wybranych przez użytkownika.

## <a name="as-is-code"></a>Jako — kod

Należy pamiętać, ten kod jest udostępniana jako przykładowe zastosowanie toodemonstrate zaproszenia hello Azure Active Directory B2B interfejsu API. Powinny zostać dostosowane przez zespół deweloperów lub partnera i należy ją sprawdzić przed wdrożeniem w środowisku produkcyjnym.

## <a name="next-steps"></a>Następne kroki

Zobacz nasze inne artykuły dotyczące współpracy B2B w usłudze Azure AD:
* [Czym jest współpraca B2B w usłudze Azure AD?](active-directory-b2b-what-is-azure-ad-b2b.md)
* [Jak Administratorzy usługi Azure Active Directory dodać użytkowników współpracy B2B?](active-directory-b2b-admin-add-users.md)
* [Jak pracownicy przetwarzający informacje dodać użytkowników współpracy B2B?](active-directory-b2b-iw-add-users.md)
* [elementy Hello hello wiadomość e-mail z zaproszeniem współpracy B2B](active-directory-b2b-invitation-email.md)
* [Realizacji zaproszenia współpracy B2B](active-directory-b2b-redemption-experience.md)
* [Azure licencjonowania współpracy B2B usługi AD](active-directory-b2b-licensing.md)
* [Rozwiązywanie problemów z współpracy usługi Azure Active Directory B2B](active-directory-b2b-troubleshooting.md)
* [Azure współpracy B2B usługi Active Directory — często zadawane pytania (FAQ)](active-directory-b2b-faq.md)
* [Usługa Multi-Factor Authentication dla użytkowników współpracy B2B](active-directory-b2b-mfa-instructions.md)
* [Dodawanie użytkowników współpracy B2B bez zaproszenia](active-directory-b2b-add-user-without-invite.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)