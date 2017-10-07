---
title: "aaaUpgrade z narzędzia DirSync i Azure AD Sync | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooupgrade z narzędzia DirSync i Azure AD Sync tooAzure AD Connect."
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
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Uaktualnienia usługi synchronizacji usługi Windows Azure Active Directory i Azure synchronizacji usługi Active Directory
Azure AD Connect jest hello najlepsze sposób tooconnect katalogu lokalnego z usługą Azure AD i Office 365. Jest to doskonały moment tooAzure tooupgrade AD Connect z systemu Windows synchronizacji Azure Active Directory (DirSync) lub Azure AD Sync, jak te narzędzia są teraz przestarzałe i osiągną wsparcie dla 13 kwietnia 2017 r.

Witaj dwie tożsamości synchronizacji narzędzia, które zostały uznane za przestarzałe zostały zaoferowane dla klientów z pojedynczym lasem (DirSync) i obejmującego wiele lasów i inne zaawansowane klientów (Azure AD Sync). Narzędzia te starsze zostały zamienione na pojedyncze rozwiązanie, która jest dostępna we wszystkich scenariuszach: Azure AD Connect. Oferuje nową funkcję, ulepszone funkcje i obsługę nowych scenariuszy. toosynchronize stanie toocontinue toobe tooAzure danych tożsamości lokalnej usługi AD i Office 365, zdecydowanie zaleca się uaktualnienie tooAzure AD Connect.

Witaj ostatniej wersji narzędzia DirSync został wydany w lipca 2014 i hello ostatniej wersji programu Azure AD Sync został wydany w maja 2015.

## <a name="what-is-azure-ad-connect"></a>Co to jest program Azure AD Connect
Azure AD Connect jest tooDirSync następnika hello i Azure AD Sync. Łączy wszystkie scenariusze te dwa obsługiwane. Więcej informacji w [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>Amortyzacja harmonogramu
| Date | Komentarz |
| --- | --- |
| 13 kwietnia 2016 r. |Windows Azure Active Directory synchronizacji ("DirSync") i Microsoft Azure synchronizacji usługi Active Directory ("Azure AD Sync") są ogłoszone jako przestarzałe. |
| 13 kwietnia 2017 r. |Obsługa kończy się. Klienci nie będą już mogli tooopen sprawy pomocy technicznej, bez uaktualniania tooAzure AD Połącz najpierw. |
|31 grudnia 2017 r.|Usługi Azure AD, nie będzie akceptował komunikację z systemu Windows Azure Active Directory synchronizacji ("DirSync") i Microsoft Azure synchronizacji usługi Active Directory ("Azure AD Sync").

## <a name="how-tootransition-tooazure-ad-connect"></a>Jak tootransition tooAzure AD Connect
Jeśli używasz narzędzia DirSync, istnieją dwa sposoby, możesz uaktualnić: uaktualnienia i równoległych wdrożeń w miejscu. Uaktualnienie w miejscu jest zalecane dla większości klientów i czy masz ostatnie operacyjnego i mniej niż 50 000 obiektów. W pozostałych przypadkach zaleca się, że toodo wdrożenie równoległe, gdy konfiguracja narzędzia DirSync jest przenoszone tooa nowy serwer z systemem Azure AD Connect.

Jeśli używasz usługi Azure AD Sync, jest zalecane jest uaktualnienie w miejscu. Jeśli chcesz, jest możliwe tooinstall nowy serwer Azure AD Connect równolegle i przeprowadzić migrację zasięg z programu Azure AD Sync tooAzure serwera AD Connect.

| Rozwiązanie | Scenariusz |
| --- | --- |
| [Uaktualnianie z narzędzia DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Jeśli masz istniejące już działający serwer DirSync.</li> |
| [Uaktualnianie programu Azure AD Sync](active-directory-aadconnect-upgrade-previous-version.md) |<li>Jeśli przenosisz z narzędzia Azure AD Sync.</li> |

Jeśli chcesz toosee jak toodo w miejscu, Uaktualnij z narzędzia DirSync tooAzure AD Connect, a następnie zobacz ten film Channel 9:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>Często zadawane pytania
**Pytanie: czy wiadomość e-mail z powiadomieniem mogę otrzymany od hello Azure zespołu i/lub komunikat z Centrum wiadomości powitania usługi Office 365, ale używam Connect.**  
powiadomienie Hello została wysłana toocustomers za pomocą usługi Azure AD Connect przy użyciu numeru kompilacji 1.0. \*.0 (przy użyciu wersji pre-1.1). Firma Microsoft zaleca klientów zwalnia toostay bieżącego z programem Azure AD Connect. Witaj [automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md) funkcja wprowadzona w wersji 1.1 umożliwia łatwe tooalways ma najnowszej wersji programu Azure AD Connect.

**Pytanie: stop będzie DirSync/usługi Azure AD Sync pracuje 13 kwietnia 2017?**  
Narzędzie DirSync/usługi Azure AD Sync będzie toowork na kwietnia 2017 13.  Jednak usługi Azure AD, nie będzie akceptował komunikację z narzędzia DirSync/usługi Azure AD Sync na 2017 31 grudnia.

**Pytanie: które wersje narzędzia DirSync można uaktualnić z?**  
Jest obsługiwane tooupgrade z dowolną wersją narzędzia DirSync, w obecnie używane.

**Pytanie: jak hello łącznika usługi Azure AD dla programu FIM/MIM?**  
Witaj łącznika usługi Azure AD dla programu FIM/MIM ma **nie** zostały ogłoszone jako przestarzałe. W **funkcja blokowania**; dodaje się nie nowych funkcji i odbiera nie poprawki. Firma Microsoft zaleca klientów korzystających z jej toomove tooplan z niego tooAzure AD Connect. Jest zdecydowanie zalecane toonot start każde nowe wdrożenie przy jej użyciu. Ten łącznik będą ogłaszane uznane za przestarzałe w przyszłych hello.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
