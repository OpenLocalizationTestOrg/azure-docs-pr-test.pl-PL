---
title: "Synchronizacja programu Azure AD Connect: zrozumienie i dostosować synchronizację | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak działa synchronizacja programu Azure AD Connect i jak toocustomize."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ee4bf802-045b-4da0-986e-90aba2de58d6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2016
ms.author: markvi
ms.openlocfilehash: 97e4bd9904b077f2628e5f8dcbaa6f1a76168a12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understand-and-customize-synchronization"></a>Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji
usługi synchronizacji usługi Azure Active Directory Connect Hello (synchronizacja programu Azure AD Connect) jest głównym składnikiem programu Azure AD Connect. Odpowiada on za wszystkie operacje hello, które są powiązane toosynchronize danych tożsamości między środowiskiem lokalnym i usługą Azure AD. Synchronizacja programu Azure AD Connect jest następnika hello narzędzia DirSync, Azure AD Sync i Forefront Identity Manager z hello skonfigurować łącznika usługi Azure Active Directory.

Ten temat jest hello macierzystego dla **synchronizacja programu Azure AD Connect** (nazywane również **aparatu synchronizacji**) i list łączy tooall innych tooit powiązanych tematów. Dla łącza tooAzure AD Connect, zobacz [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

Usługa synchronizacji Hello zawiera dwa składniki, lokalne powitania **synchronizacja programu Azure AD Connect** składnika i powitania po stronie usługi w usłudze Azure AD o nazwie **usługi synchronizacji programu Azure AD Connect**. Usługa Hello jest typowe dla narzędzia DirSync, Azure AD Sync i Azure AD Connect.

## <a name="azure-ad-connect-sync-topics"></a>Tematy synchronizacji usługi Azure AD Connect
| Temat | Co obejmuje i kiedy tooread |
| --- | --- |
| **Podstawy synchronizacji usługi Azure AD Connect** | |
| [Opis architektury hello](active-directory-aadconnectsync-understanding-architecture.md) |Dla osób, które który są nowy aparat synchronizacji toohello i mają toolearn o architekturze hello i hello terminów używanych. |
| [Zagadnienia techniczne](active-directory-aadconnectsync-technical-concepts.md) |Krótka wersja hello architektura tematu i krótko opisano hello terminów używanych. |
| [Topologie obsługiwane w programie Azure AD Connect](active-directory-aadconnect-topologies.md) |W tym artykule opisano hello różnych scenariuszy i topologii hello synchronizacji aparat obsługuje. |
| **Konfiguracja niestandardowa** | |
| [Uruchomione hello Kreatora instalacji ponownie](active-directory-aadconnectsync-installation-wizard.md) |Opisano opcje ma dostępne po uruchomieniu Kreatora instalacji hello Azure AD Connect ponownie. |
| [Opis Aprowizacją deklaratywną](active-directory-aadconnectsync-understanding-declarative-provisioning.md) |W tym artykule opisano model konfiguracji hello o nazwie aprowizacją deklaratywną. |
| [Opis deklaratywne wyrażenia inicjowania obsługi administracyjnej](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md) |W tym artykule opisano składnię hello hello wyrażenia języka używanego w aprowizacją deklaratywną. |
| [Opis hello domyślnej konfiguracji](active-directory-aadconnectsync-understanding-default-configuration.md) |Opisuje zasady out-of-box hello i hello domyślnej konfiguracji. Opisano również zasady hello współdziałania dla hello toowork scenariusze out-of-box. |
| [Opis użytkowników i kontaktów](active-directory-aadconnectsync-understanding-users-and-contacts.md) |Jest kontynuowane od poprzedniego tematu hello i opisuje sposób konfiguracji powitania dla użytkowników i kontaktów działania ze sobą, w szczególności w środowisku wielu lasów. |
| [Jak toomake toohello zmiany domyślną konfigurację](active-directory-aadconnectsync-change-the-configuration.md) |Przedstawiono sposób przepływu toomake wspólnej tooattribute zmiany konfiguracji. |
| [Najlepsze rozwiązania dotyczące zmieniania konfiguracji domyślnej hello](active-directory-aadconnectsync-best-practices-changing-default-configuration.md) |Ograniczenia obsługi i dokonywania zmian toohello out-of-box konfiguracji. |
| [Konfigurowanie filtrowania](active-directory-aadconnectsync-configure-filtering.md) |W tym artykule opisano różne opcje hello synchronizowanie toolimit, które obiekty są tooAzure AD i instrukcje krok po kroku tooconfigure tych opcji. |
| **Scenariusze i funkcje** | |
| [Zapobieganie przypadkowemu usuwaniu](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) |W tym artykule opisano hello *Zapobieganie przypadkowemu usuwaniu* funkcji i w jaki sposób tooconfigure go. |
| [Scheduler](active-directory-aadconnectsync-feature-scheduler.md) |W tym artykule opisano hello wbudowanych harmonogramu, który importowania, synchronizowania i eksportowanie danych. |
| [Implementowanie synchronizacji haseł](active-directory-aadconnectsync-implement-password-synchronization.md) |Opisuje sposób działania synchronizacji haseł, jak tooimplement i w jaki sposób toooperate i rozwiązywanie problemów. |
| [Zapisywanie zwrotne urządzeń](active-directory-aadconnect-feature-device-writeback.md) |W tym artykule opisano, jak działa zapisu zwrotnego urządzeń w programie Azure AD Connect. |
| [Rozszerzenia katalogów](active-directory-aadconnectsync-feature-directory-extensions.md) |W tym artykule opisano, jak tooextend hello schemat usługi Azure AD z własnych niestandardowych atrybutów. |
| **Usługa synchronizacji** | |
| [Funkcje usługi synchronizacji programu Azure AD Connect](active-directory-aadconnectsyncservice-features.md) |Opisuje po stronie usługi synchronizacji hello i jak toochange synchronizacji ustawień w usłudze Azure AD. |
| [Zduplikowany atrybut odporności](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md) |Opisuje sposób tooenable i użyj **userPrincipalName** i **proxyAddresses** odporności wartości zduplikowany atrybut. |
| **Operacje i interfejsu użytkownika** | |
| [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) |W tym artykule opisano hello interfejsu użytkownika Menedżera usługi synchronizacji, w tym [operacji](active-directory-aadconnectsync-service-manager-ui-operations.md), [łączniki](active-directory-aadconnectsync-service-manager-ui-connectors.md), [Metaverse Designer](active-directory-aadconnectsync-service-manager-ui-mvdesigner.md), i [wyszukiwanie Metaverse](active-directory-aadconnectsync-service-manager-ui-mvsearch.md) karty. |
| [Zagadnienia i zadania operacyjne](active-directory-aadconnectsync-operations.md) |W tym artykule opisano problemy operacyjne, takie jak odzyskiwania po awarii. |
| **Jak...** | |
| [Resetuj konta hello Azure AD](active-directory-aadconnectsync-howto-azureadaccount.md) |Jak tooconnect z tooAzure synchronizacji Azure AD Connect AD używane poświadczenia hello tooreset hello konta usługi. |
| **Więcej informacji i odwołań** | |
| [Porty](active-directory-aadconnect-ports.md) |List, które porty należy muszą tooopen między aparatem synchronizacji hello i katalogów lokalnych i usługi Azure AD. |
| [Atrybuty są synchronizowane tooAzure usługi Active Directory](active-directory-aadconnectsync-attributes-synchronized.md) |Wyświetla listę wszystkich atrybutów synchronizacji między lokalnymi AD i Azure AD. |
| [Informacje ogólne o funkcjach](active-directory-aadconnectsync-functions-reference.md) |Wyświetla listę wszystkich funkcji dostępnych w aprowizacją deklaratywną. |

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)

