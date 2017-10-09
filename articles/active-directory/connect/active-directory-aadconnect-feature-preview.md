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
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>Więcej informacji na temat funkcji w wersji zapoznawczej
W tym temacie opisano, jak toouse obecnie funkcje w wersji zapoznawczej.

## <a name="group-writeback"></a>Zapisywanie zwrotne grup
Opcja powitania dla zapisu zwrotnego grup w funkcji opcjonalnych umożliwia toowriteback **grupy usługi Office 365** tooa lasu za pomocą programu Exchange jest zainstalowany. To jest grupa, która zawsze jest zarządzany w chmurze hello. Jeśli masz lokalnego programu Exchange, następnie można napisać ponownie lokalnych tooon tych grup, wysyłanie i odbieranie wiadomości e-mail z następujących grup użytkowników z skrzynki pocztowej programu Exchange lokalnie.

Więcej informacji na temat grupy usługi Office 365 i jak toouse je można znaleźć [tutaj](http://aka.ms/O365g).

Grupy usługi Office 365 jest reprezentowany jako grupy dystrybucji w lokalnej instalacji usług AD DS. Z lokalnym programem Exchange server musi być na aktualizację zbiorczą programu Exchange 2013 8 (wydane w marca 2015) lub programów Exchange 2016 toorecognize ten nowy typ grupy.

**Informacje o wersji zapoznawczej hello**

* Atrybut książki adresu Hello obecnie jest pusta w wersji zapoznawczej hello. Bez tego atrybutu hello grupy nie jest widoczny w hello usługi GAL. Najprostszym sposobem toopopulate Hello ten atrybut to polecenie cmdlet programu PowerShell usługi Exchange hello toouse `update-recipient`.
* Tylko lasy ze schematem Exchange hello są prawidłowe elementy docelowe dla grup. Jeśli wykryto nie programu Exchange, następnie zapisu zwrotnego grup nie jest możliwe tooenable.
* Tylko jeden las wdrożenia organizacji programu Exchange są obecnie obsługiwane. Jeśli masz więcej niż jednej organizacji do lokalnego programu Exchange, wymagana będzie używane rozwiązanie lokalne usługi GALSync dla tych grup tooappear w sieci w innych lasach.
* funkcji zapisywania zwrotnego grupy Hello nie obsługuje grup zabezpieczeń lub grup dystrybucji.

> [!NOTE]
> Subskrypcja tooAzure AD — wersja Premium jest wymagana dla zapisu zwrotnego grup.
> 
>

## <a name="user-writeback"></a>Zapisywanie zwrotne użytkowników
> [!IMPORTANT]
> Witaj użytkownika funkcja zapisywania zwrotnego w wersji zapoznawczej została usunięta w hello sierpnia 2015 aktualizacja tooAzure AD Connect. Jeśli zostanie włączona, należy wyłączyć tę funkcję.
>
>

## <a name="next-steps"></a>Następne kroki
Kontynuuj Twojej [Instalacja niestandardowa programu Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
