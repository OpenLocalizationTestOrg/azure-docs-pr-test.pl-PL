---
title: "ustawienia zasad i zarządzania urządzeniami Przenośnymi aaaGroup | Dokumentacja firmy Microsoft"
description: "Zawiera informacje dotyczące zasad grupy i urządzeń przenośnych ustawień zarządzania urządzeniami Przenośnymi, które powinny być używane na urządzeniach należących do firmy. Te zasady są stosowane toohello użytkownika wszystkich danych z urządzenia."
services: active-directory
keywords: "Co to są zasady grupy i ustawień zarządzania urządzeniami Przenośnymi roamingu stanu przedsiębiorstwa, roamingu stanu przedsiębiorstwa, chmury systemu windows"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: 6471a9b3-8dd4-4237-89d1-bfbeca9f8252
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: 762419b47014b1fb4d92ac528785e20078afe689
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="group-policy-and-mdm-settings"></a>Ustawienia zasad grupy i zarządzania urządzeniami Przenośnymi
Użyj tych zasad grupy i ustawienia zarządzania urządzeniami Przenośnymi dla urządzeń przenośnych tylko na urządzeniach należących do firmy, ponieważ te zasady są stosowane toohello użytkownika wszystkich danych z urządzenia. Stosowanie synchronizacji ustawień zarządzania urządzeniami Przenośnymi zasad toodisable do osobistego, urządzenia należące do użytkownika będzie negatywny wpływ na powitania korzystanie z tego urządzenia. Ponadto inne konta użytkownika na urządzeniu hello będzie również zostaną objęte hello zasad.

Przedsiębiorstw, które chcesz użyć toomanage mobilność urządzenia osobiste (niezarządzany) hello tooenable portalu Azure lub wyłączyć mobilnych, a nie za pomocą zasad grupy lub zarządzania urządzeniami przenośnymi.
następujące tabele Hello opisano hello dostępnych ustawień zasad.

## <a name="mdm-settings"></a>Ustawienia zarządzania urządzeniami Przenośnymi
ustawienia zasad zarządzania urządzeniami Przenośnymi Hello stosowane tooboth systemu Windows 10 i Windows 10 Mobile.  Obsługa systemu Windows 10 Mobile istnieje tylko w przypadku konta Microsoft na podstawie mobilnych za pomocą konta usługi OneDrive użytkownika.  Zobacz zbyt sekcji "Urządzeń i punkty końcowe" Aby uzyskać szczegółowe informacje, na które urządzenia są obsługiwane dla usługi Azure AD na podstawie synchronizacji.

| Nazwa | Opis |
| --- | --- |
| Zezwalaj na połączenie konta Microsoft |Umożliwia tooauthenticate użytkowników za pomocą konta Microsoft na urządzeniu hello |
| Zezwalaj na synchronizację ustawień |Umożliwia użytkownikom tooroam Windows ustawień i danych aplikacji; Wyłączenie tych zasad spowoduje wyłączenie synchronizacji, a także kopie zapasowe na urządzeniach przenośnych |

## <a name="group-policy-settings"></a>Ustawienia zasad grupy
ustawienia zasad grupy Hello zastosować tooWindows 10 urządzenia, które są tooan przyłączone do domeny usługi Active Directory. Tabela Hello także starszej wersji ustawienia które pojawią się ustawienia synchronizacji toomanage, ale nie działają dla przedsiębiorstwa stanu mobilnych dla systemu Windows 10, które są oznaczane przy użyciu "Nie należy używać" w opisie hello.

| Nazwa | Opis |
| --- | --- |
| Konta: Blokowanie kont Microsoft |To ustawienie zasad uniemożliwia użytkownikom dodawanie nowych kont Microsoft na tym komputerze |
| Nie Synchronizuj |Uniemożliwia użytkownikom tooroam Windows ustawień i danych aplikacji |
| Nie Synchronizuj spersonalizować |Wyłącza synchronizację hello motywów grupy |
| Nie synchronizować ustawienia przeglądarki |Wyłącza synchronizację hello grupy programu Internet Explorer |
| Nie synchronizuje haseł |Wyłącza synchronizację haseł grupy |
| Nie Synchronizuj inne ustawienia systemu Windows |Wyłącza synchronizację inne okna Ustawienia grupy |
| Nie Synchronizuj personalizacja pulpitu |Nie używaj; nie ma wpływu |
| Synchronizacji w przypadku mierzonych połączeń |Wyłącza mobilnego na mierzonych połączeń, takich jak komórkowej sieci 3 G |
| Nie Synchronizuj aplikacje |Nie używaj; nie ma wpływu |
| Nie Synchronizuj ustawienia aplikacji |Wyłącza roaming danych aplikacji |
| Nie Synchronizuj ustawienia uruchamiania |Nie używaj; nie ma wpływu |

## <a name="related-topics"></a>Powiązane tematy
* [Opis roamingu stanu przedsiębiorstwa](active-directory-windows-enterprise-state-roaming-overview.md)
* [Włącz roaming stanu przedsiębiorstwa w usłudze Azure Active Directory](active-directory-windows-enterprise-state-roaming-enable.md)
* [Ustawienia i dane mobilne — często zadawane pytania](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Informacje dotyczące ustawień roamingu systemu Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Rozwiązywanie problemów](active-directory-windows-enterprise-state-roaming-troubleshooting.md)

