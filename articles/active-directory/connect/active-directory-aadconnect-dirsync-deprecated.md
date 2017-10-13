---
title: "Uaktualnianie z narzędzia DirSync i Azure AD Sync | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób uaktualniania z narzędzia DirSync i Azure AD Sync do programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3674670e10500d2992539ab60fbdb31b666fcf9a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Uaktualnienia usługi synchronizacji usługi Windows Azure Active Directory i Azure synchronizacji usługi Active Directory
Użycie programu Azure AD Connect to najlepszy sposób na połączenie katalogu lokalnego z usługami Azure AD i Office 365. Jest to doskonały moment na uaktualnienie do programu Azure AD Connect z narzędzia Windows Azure Active Directory Sync (DirSync) lub Azure AD Sync, ponieważ są one przestarzałe, a wsparcie dla nich zakończy się 13 kwietnia 2017 r.

Narzędzia synchronizacji dwóch tożsamości, które zostały uznane za przestarzałe były oferowane dla klientów z pojedynczym lasem (DirSync) i dla wielu lasów i inne zaawansowane klientów (Azure AD Sync). Narzędzia te starsze zostały zamienione na pojedyncze rozwiązanie, która jest dostępna we wszystkich scenariuszach: Azure AD Connect. Oferuje nową funkcję, ulepszone funkcje i obsługę nowych scenariuszy. Aby można było kontynuować synchronizowanie danych tożsamości lokalnych z usługą Azure AD i Office 365, zdecydowanie zaleca się uaktualniania do programu Azure AD Connect.

W ostatniej wersji narzędzia DirSync został wydany w lipca 2014 i ostatniej wersji programu Azure AD Sync został wydany w maja 2015.

## <a name="what-is-azure-ad-connect"></a>Co to jest program Azure AD Connect
Azure AD Connect jest zastępuje narzędzie DirSync i Azure AD Sync. Łączy wszystkie scenariusze te dwa obsługiwane. Więcej informacji w [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>Amortyzacja harmonogramu
| Date | Komentarz |
| --- | --- |
| 13 kwietnia 2016 r. |Windows Azure Active Directory synchronizacji ("DirSync") i Microsoft Azure synchronizacji usługi Active Directory ("Azure AD Sync") są ogłoszone jako przestarzałe. |
| 13 kwietnia 2017 r. |Obsługa kończy się. Klientów nie będą już mogli otworzyć sprawę pomocy technicznej bez przeprowadzenia uaktualnienia do programu Azure AD Connect. |
|31 grudnia 2017 r.|Usługi Azure AD, nie będzie akceptował komunikację z systemu Windows Azure Active Directory synchronizacji ("DirSync") i Microsoft Azure synchronizacji usługi Active Directory ("Azure AD Sync").

## <a name="how-to-transition-to-azure-ad-connect"></a>Temat przechodzenia do usługi Azure AD Connect
Jeśli używasz narzędzia DirSync, istnieją dwa sposoby, możesz uaktualnić: uaktualnienia i równoległych wdrożeń w miejscu. Uaktualnienie w miejscu jest zalecane dla większości klientów i czy masz ostatnie operacyjnego i mniej niż 50 000 obiektów. W pozostałych przypadkach zaleca się przeprowadzić wdrożenie równoległe, w którym konfiguracji narzędzia DirSync jest przenoszona do nowego serwera z systemem Azure AD Connect.

Jeśli używasz usługi Azure AD Sync, jest zalecane jest uaktualnienie w miejscu. Jeśli chcesz, to można zainstalować nowy serwer Azure AD Connect równolegle i przeprowadzić migrację zasięg między serwerem programu Azure AD Sync do programu Azure AD Connect.

| Rozwiązanie | Scenariusz |
| --- | --- |
| [Uaktualnianie z narzędzia DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Jeśli masz istniejące już działający serwer DirSync.</li> |
| [Uaktualnianie programu Azure AD Sync](active-directory-aadconnect-upgrade-previous-version.md) |<li>Jeśli przenosisz z narzędzia Azure AD Sync.</li> |

Jeśli chcesz zobaczyć, jak przeprowadzić uaktualnienie w miejscu z narzędzia DirSync do programu Azure AD Connect, zobacz temat to wideo z witryny Channel 9:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>Często zadawane pytania
**Pytanie: czy mogę otrzymali wiadomość e-mail z powiadomieniem od zespołu Azure i/lub komunikat z Centrum wiadomości usługi Office 365, ale używam Connect.**  
Również wysłano powiadomienia do klientów za pomocą usługi Azure AD Connect przy użyciu numeru kompilacji 1.0. \*.0 (przy użyciu wersji pre-1.1). Firma Microsoft zaleca klientom aktualne informacje o wersji Azure AD Connect. [Automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md) funkcja wprowadzona w wersji 1.1 ułatwia zawsze mieć najnowszej wersji programu Azure AD Connect.

**Pytanie: stop będzie DirSync/usługi Azure AD Sync pracuje 13 kwietnia 2017?**  
Narzędzie DirSync/usługi Azure AD Sync będą nadal działać na kwietnia 2017 13.  Jednak usługi Azure AD, nie będzie akceptował komunikację z narzędzia DirSync/usługi Azure AD Sync na 2017 31 grudnia.

**Pytanie: które wersje narzędzia DirSync można uaktualnić z?**  
Możliwe jest uaktualnienie z dowolnej wersji narzędzia DirSync aktualnie używany.

**Pytanie: jak Azure AD Connector dla usługi FIM/MIM?**  
Łącznik usługi Azure AD dla programu FIM/MIM ma **nie** zostały ogłoszone jako przestarzałe. W **funkcja blokowania**; dodaje się nie nowych funkcji i odbiera nie poprawki. Firma Microsoft zaleca klientów za jego pomocą ma zostać przeniesiona z jej do usługi Azure AD Connect. Zdecydowanie zaleca się nie uruchomić wszystkie wdrożenia nowej używa go. Ten łącznik będą ogłaszane przestarzałe w przyszłości.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
