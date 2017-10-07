---
title: "aaaDedicated grup w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Przegląd grup jak dedykowanych działają w usłudze Azure Active Directory oraz sposób ich tworzenia."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Grupy dedykowane w usłudze Azure Active Directory
W usłudze Azure Active Directory (Azure AD) funkcja grupy dedykowane hello automatycznie tworzy i wypełnia członkostwa w grupach usługi Azure AD, wstępnie zdefiniowane. Nie można dodać członków grupy dedykowane lub usuniętych za pomocą hello klasycznym portalu, programu Windows PowerShell polecenia cmdlet systemu Azure, lub programowo.

> [!NOTE]
> Grupy dedykowane wymagają przypisania do licencji Azure AD Premium
>
> * Witaj administratora, który zarządza hello regułą grupy
> * Wszyscy użytkownicy, którzy na podstawie hello reguły toobe hello grupy
>
>

**grupy tooenable w wersji dedykowanej**

1. W hello [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.
2. Wybierz hello **grup** kartę, a następnie otwórz hello grupę tooedit.
3. Wybierz hello **Konfiguruj** karcie, a następnie ustaw **Włącz grupy dedykowane** za**tak**.

Po ustawieniu hello przełącznika włączyć grupy dedykowane zbyt**tak**, dodatkowo można włączyć tooautomatically katalogu hello Tworzenie grupy dedykowane wszyscy użytkownicy hello przez ustawienie hello **włączyć "Wszyscy użytkownicy" grupy** Przełącz zbyt**tak**. Następnie można również edytować hello nazwę tej grupy dedykowane przez wpisanie jej w hello **"Wszyscy użytkownicy" Nazwa wyświetlana grupy** pola.

Witaj grupy Wszyscy użytkownicy mogą służyć tooassign hello tych samych uprawnień tooall hello użytkowników w katalogu. Na przykład można przyznać wszyscy użytkownicy w Twojej tooa dostępu do katalogu aplikacji SaaS, przypisując dostępu dla wszystkich użytkowników grupy dedykowane toothis aplikacji hello.

Witaj w wersji dedykowanej wszystkich użytkowników grupy należą wszyscy użytkownicy w katalogu hello, w tym gości i użytkowników zewnętrznych. Jeśli potrzebujesz grupy który wyklucza użytkowników zewnętrznych, a następnie można to zrobić, tworząc grupy z opartych na atrybutach dynamiczne reguły, takie jak następujące hello:

                (user.userPrincipalName -notContains "#EXT#@")

Grupy, która nie obejmuje wszystkich gości należy użyć reguły, takie jak następujące hello:

                (user.userType -ne "Guest")

toolearn o tym, jak toocreate *zaawansowane* reguły (zasady, które mogą zawierać więcej niż jedno porównanie) na dynamiczne członkostwo w grupie, zobacz [przy użyciu atrybutów toocreate zaawansowane zasady](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Co to jest usługa Azure Active Directory?](active-directory-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
