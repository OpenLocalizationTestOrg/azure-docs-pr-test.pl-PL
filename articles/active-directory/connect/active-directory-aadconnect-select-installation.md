---
title: 'Azure AD Connect: Wybierz typ instalacji | Dokumentacja firmy Microsoft'
description: "W tym temacie przedstawiono sposób instalacji hello tooselect wpisz toouse programu Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a>Wybierz które toouse typu instalacji programu Azure AD Connect
Azure AD Connect ma dwa typy instalacji nowej instalacji: Express i niestandardowych. Ten temat ułatwia toodecide, która opcja toouse podczas instalacji.

## <a name="express"></a>Express
Express jest najbardziej typowych opcji hello i jest używany przez wszystkie nowe instalacje około 90%. Został zaprojektowany tooprovide konfigurację, która działa w przypadku najbardziej typowych scenariuszy hello.

Zakłada się:

- Masz pojedynczego Active Directory lasu lokalnego.
- Masz konto administratora przedsiębiorstwa, używanej do instalacji hello.
- Masz mniej niż 100 000 obiektów w usłudze Active Directory lokalnymi.

Pobierz:

- [Synchronizacja haseł](active-directory-aadconnectsync-implement-password-synchronization.md) z lokalnymi tooAzure AD dla logowania jednokrotnego.
- Konfiguracja, która synchronizuje [użytkowników, grup, kontaktów i komputerach z systemem Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).
- Synchronizacja wszystkich kwalifikujących się obiekty w wszystkie domeny i wszystkich jednostkach organizacyjnych.
- [Automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md) jest włączone toomake się, że zawsze używaj hello najnowszej dostępnej wersji.

Opcje, których można nadal używać Express:

- Jeśli nie chcesz toosynchronize wszystkich jednostkach organizacyjnych, można nadal używać Express i na ostatniej stronie powitania, usuń zaznaczenie **Uruchom proces synchronizacji hello...** *. A następnie ponownie uruchom Kreatora instalacji hello i zmienić jednostek organizacyjnych hello w [opcje konfiguracji](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) i Włącz synchronizację według harmonogramu.
- Ma tooenable hello funkcji w usłudze Azure AD Premium, takie jak zapisywanie zwrotne haseł. Najpierw należy przeprowadzić express tooget hello początkowej instalacja została zakończona. A następnie ponownie uruchom Kreatora instalacji hello i zmienić hello [opcje konfiguracji](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).

## <a name="custom"></a>Niestandardowy
Ścieżka dostosowane Hello umożliwia wiele więcej opcji niż express. Stosuje we wszystkich przypadkach, gdy hello konfiguracji opisanych w poprzedniej sekcji Express nie jest reprezentatywna dla Twojej organizacji.

Zastosowania:

- Nie masz konta administratora przedsiębiorstwa tooan dostępu w usłudze Active Directory.
- Masz więcej niż jednym lesie lub planujesz toosynchronize więcej niż jednym lesie w przyszłości hello.
- Masz domen w lesie nieosiągalny z serwera Connect hello.
- Planujesz toouse Federacji lub przekazywanego uwierzytelniania dla logowania użytkownika.
- Masz więcej niż 100 000 obiektów i muszą toouse pełnego serwera SQL.
- Planujesz filtrowanie na podstawie grupy toouse i nie tylko domeny lub filtrowanie na podstawie jednostki Organizacyjnej.

## <a name="upgrade-from-dirsync"></a>Uaktualnianie przy użyciu narzędzia DirSync
Jeśli obecnie używasz narzędzia DirSync, a następnie wykonaj kroki hello [uaktualnienia narzędzia DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade istniejącej konfiguracji. Istnieją dwa różne opcje uaktualniania:

- Tooinstall uaktualnienia w miejscu na połączenie hello sam serwer.
- Równoległe wdrożenia tooinstall Connect na nowym serwerze, gdy serwer DirSync hello jest nadal działa.

## <a name="upgrade-from-azure-ad-sync"></a>Uaktualnianie programu Azure AD Sync
Jeśli aktualnie używasz usługi Azure AD Sync, a następnie wykonać hello [te same czynności](active-directory-aadconnect-upgrade-previous-version.md) jako po uaktualnieniu z jednego połączenia wersji tooa nowszej. Istnieją dwa różne opcje uaktualniania:

- Tooinstall uaktualnienia w miejscu na połączenie hello sam serwer.
- Zasięg migracji tooinstall Connect na nowym serwerze podczas istniejącego serwera Azure AD Sync hello jest nadal działa.

## <a name="migrate-from-fim2010-or-mim2016"></a>Migrowanie z usługi FIM2010 lub MIM2016
Jeśli używasz obecnie programu Forefront Identity Manager 2010 lub Microsoft Identity Manager 2016 z hello łącznika usługi Azure AD, jedyną opcją jest migracji. Wykonaj kroki hello opisanego w [migracji zasięg](active-directory-aadconnect-upgrade-previous-version.md#swing-migration). W krokach hello Zastąp FIM2010/MIM2016 wszelkie uwagi Azure AD Sync.

## <a name="next-steps"></a>Następne kroki
W zależności od opcji hello wybrano toouse, użyj hello tabelę z zawartości toohello toofind po lewej stronie artykułu z hello szczegółowe kroki.
