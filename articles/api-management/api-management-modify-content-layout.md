---
title: "zawartość strony aaaModify w portalu dla deweloperów hello w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooedit strony zawartości w portalu dla deweloperów hello w usłudze Azure API Management."
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>Modyfikowanie hello zawartość i układ strony w portalu dla deweloperów hello w usłudze Azure API Management
Istnieją trzy podstawowe sposoby toocustomize hello portalu dla deweloperów usługi Azure API Management:

* [Edytuj zawartość hello strony statyczne i elementy układ strony] [ modify-content-layout] (co omówiono w tym przewodniku)
* [Aktualizuj style hello używany do elementów strony w portalu dla deweloperów hello][customize-styles]
* [Modyfikowanie szablonów hello używany dla stron wygenerowanych przez hello portal] [ portal-templates] (Dokumentacja interfejsu API, produktów, uwierzytelnianie użytkowników, itp.)

## <a name="page-structure"> </a>Struktura stron portalu deweloperów

portalu dla deweloperów Hello jest oparta na system zarządzania zawartością. Układ Hello każdej strony jest tworzona na podstawie zestawu elementów strony małe znany jako elementy widget:

![Struktura stron portalu deweloperów][api-management-customization-widget-structure]

Wszystkie widżety można edytować. 
* Witaj core zawartość określonego tooeach pojedynczej strony znajdują się w widżet "Zawartość" hello. Edycji strony oznacza edycji hello zawartość tego elementu widget.
* Wszystkie elementy na stronie układu znajdują się hello pozostałych widżetów. Elementy widget toothese zmiany zostaną zastosowane tooall stron. Będą one określonej tooas "elementy widget układu".

Na stronie codziennych tylko edycji jedną zwykle modyfikuje hello widget zawartości, który będzie miał inną zawartość dla każdej strony.

## <a name="modify-layout-widget"></a>Modyfikowanie hello zawartość elementu widget układu

Zawartość w portalu dla deweloperów hello jest modyfikowana za pośrednictwem portalu wydawcy hello, która jest dostępna z hello portalu Azure. tooreach, kliknij przycisk **wydawcy portalu** z paska narzędzi usługi hello wystąpienia interfejsu API zarządzania.

![Portal wydawcy][api-management-management-console]

tooedit hello zawartość tego elementu widget, kliknij przycisk **elementy widget** z hello **portalu dla deweloperów** menu po lewej stronie powitania. Dla tego przykładu umożliwia modyfikowanie zawartości hello hello widżetu nagłówka. Wybierz hello **nagłówka** widżet z listy hello.

![Widżety — nagłówek][api-management-widgets-header]

Witaj zawartość nagłówka hello jest edytowalny z wewnątrz hello **treści** pola. Zmień tekst hello zgodnie z potrzebami, a następnie kliknij przycisk **zapisać** u dołu hello hello strony.

Teraz powinno być możliwe toosee hello nowego nagłówka na każdej stronie w portalu dla deweloperów hello.

> portalu dla deweloperów hello tooopen znajduje się w portalu wydawcy hello, kliknij przycisk **portalu dla deweloperów** w górnym pasku hello.
> 
> 

## <a name="edit-page-contents"></a>Edytować hello zawartości strony

toosee hello lista wszystkich istniejących stron zawartości, kliknij przycisk **zawartości** z hello **portalu dla deweloperów** menu w portalu wydawcy hello.

![Zarządzanie zawartością][api-management-customization-manage-content]

Kliknij przycisk hello **powitalnej** strony tooedit wyświetlanych na stronie głównej portalu dla deweloperów hello hello. Wprowadź zmiany hello, przeglądać je w razie potrzeby, a następnie kliknij przycisk **opublikować teraz** toomake je tooeveryone widoczne.

> Strona główna Hello używa specjalnego układu umożliwiająca toodisplay transparentu u góry hello. Transparent to nie jest edytowalny z hello **zawartości** sekcji. Kliknij tooedit tym transparent **elementy widget** z hello **portalu dla deweloperów** menu, wybierz **strony głównej** z hello **bieżącej warstwy** listy rozwijanej listy, a następnie otwórz hello **transparent** elementu pod hello **umieszczony sekcji**. Zawartość tego elementu widget Hello są edytowalne podobnie jak inne strony.
> 
> 

## <a name="next-steps"> </a>Następne kroki
* [Aktualizuj style hello używany do elementów strony w portalu dla deweloperów hello][customize-styles]
* [Modyfikowanie szablonów hello używany dla stron wygenerowanych przez hello portal] [ portal-templates] (Dokumentacja interfejsu API, produktów, uwierzytelnianie użytkowników, itp.)

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
