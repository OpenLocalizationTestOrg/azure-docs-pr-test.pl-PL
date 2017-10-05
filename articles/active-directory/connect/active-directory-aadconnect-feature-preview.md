---
title: 'Azure AD Connect: Funkcje w wersji zapoznawczej | Dokumentacja firmy Microsoft'
description: "W tym temacie opisano więcej funkcji szczegóły, które są w wersji zapoznawczej w programie Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: cbf8f729d0ebfb271bb0d8702ac043442b42c262
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="more-details-about-features-in-preview"></a>Więcej informacji na temat funkcji w wersji zapoznawczej
W tym temacie opisano sposób użycia funkcji obecnie w wersji zapoznawczej.

## <a name="group-writeback"></a>Zapisywanie zwrotne grup
Opcja dla zapisu zwrotnego grup w funkcji opcjonalnych służy do zapisywania zwrotnego **grupy usługi Office 365** do lasu za pomocą programu Exchange jest zainstalowany. To jest grupa, która zawsze jest zarządzany w chmurze. Jeśli masz lokalnego programu Exchange, następnie można napisać ponownie te grupy do lokalnego, wysyłanie i odbieranie wiadomości e-mail z następujących grup użytkowników z skrzynki pocztowej programu Exchange lokalnie.

Więcej informacji na temat grupy usługi Office 365 i sposobu ich użycia można znaleźć [tutaj](http://aka.ms/O365g).

Grupy usługi Office 365 jest reprezentowany jako grupy dystrybucji w lokalnej instalacji usług AD DS. Z lokalnym programem Exchange server musi być na aktualizację zbiorczą programu Exchange 2013 8 (wydane w marca 2015) lub programów Exchange 2016 rozpoznać ten nowy typ grupy.

**Informacje w wersji zapoznawczej**

* Atrybut książki adresu jest obecnie pusta w wersji zapoznawczej. Bez tego atrybutu grupy nie jest widoczny w globalnej. Najprostszym sposobem wypełniania tego atrybutu jest użycie polecenia cmdlet programu PowerShell usługi Exchange `update-recipient`.
* Tylko lasy ze schematem Exchange są prawidłowe elementy docelowe dla grup. Jeśli Exchange nie został wykryty, zapisu zwrotnego grup nie jest możliwe do włączenia.
* Tylko jeden las wdrożenia organizacji programu Exchange są obecnie obsługiwane. Jeśli masz więcej niż jednej organizacji do lokalnego programu Exchange, należy lokalnego rozwiązania usługi GALSync dla tych grup, które mają być widoczne w Twojej innych lasach.
* Nie obsługuje funkcji zapisywania zwrotnego grup, grup zabezpieczeń lub grup dystrybucji.

> [!NOTE]
> Subskrypcja usługi Azure AD Premium jest wymagana dla zapisu zwrotnego grup.
> 
>

## <a name="user-writeback"></a>Zapisywanie zwrotne użytkowników
> [!IMPORTANT]
> Funkcja zapisywania zwrotnego użytkowników w wersji zapoznawczej został usunięty w sierpnia 2015 aktualizacji do programu Azure AD Connect. Jeśli zostanie włączona, należy wyłączyć tę funkcję.
>
>

## <a name="next-steps"></a>Następne kroki
Kontynuuj Twojej [Instalacja niestandardowa programu Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
