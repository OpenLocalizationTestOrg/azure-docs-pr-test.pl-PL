---
title: "style aaaCustomize w portalu dla deweloperów hello w usłudze Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używane style hello toomodify dla dowolnej strony w portalu dla deweloperów hello w usłudze Azure API Management."
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
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>Dostosowywanie stylów hello portalu deweloperów hello w usłudze Azure API Management
Istnieją trzy podstawowe sposoby toocustomize hello portalu dla deweloperów usługi Azure API Management:

* [Edytuj zawartość hello strony statyczne i elementy układ strony][modify-content-layout]
* [Aktualizuj style hello używany do elementów strony w portalu dla deweloperów hello] [ customize-styles] (co omówiono w tym przewodniku)
* [Modyfikowanie szablonów hello używany dla stron wygenerowanych przez hello portal] [ portal-templates] (Dokumentacja interfejsu API, produktów, uwierzytelnianie użytkowników, itp.)

## <a name="change-headers-styling"></a>Zmienianie stylów hello elementów na stronie

Witaj kolory, czcionki rozmiary, długości i inne elementy style związane z dowolnej strony w portalu hello są definiowane przez reguły stylu. 

Edytowanie reguły stylu hello jest wykonywane od hello **portalu dla deweloperów** podczas jest zalogowany jako administrator. Brak tooget najpierw otwórz hello portalu Azure i kliknij polecenie **wydawcy portalu** z paska narzędzi usługi hello wystąpienia interfejsu API zarządzania.

![Portal wydawcy][api-management-management-console]

Następnie kliknij polecenie **portalu dla deweloperów** na powitania prawym górnym rogu. 

![Łącze portalu dewelopera na hello wydawcy portalu][api-management-pp-dp-link]

tooopen hello Dostosowywanie narzędzi myszą ikony dostosowania hello (lub wybierz ją) i następnie kliknij przycisk "style" hello narzędzi.

![Przycisk paska narzędzi do dostosowywania][api-management-customization-toolbar-button]

Istnieją dwa główne sposób edycji reguły stylów — można przeglądać hello listy wszystkich reguł stylu hello używane w dowolnym miejscu, co jest wyświetlane domyślnie i modyfikowanie stylu, zgodnie z potrzebami, lub możesz wybrać **wybierz element na stronie powitania** , a następnie Kliknij w dowolnym miejscu na powitania strony toosee tylko hello style dla tego elementu.

![Pasek narzędzi do dostosowywania][api-management-customization-toolbar]

Kliknij przycisk hello **wybierz element na stronie powitania** opcji, w tym przykładzie.  Elementy teraz wyróżniony po aktywowaniu nad nimi z toosignify myszy hello jakie elementu style, należy uruchomić, edytowania, jeśli kliknięto. Witaj Przenieś wskaźnik myszy na hello tekst w nagłówku hello (zazwyczaj użytkownik ma nazwę firmy hello tutaj), a następnie kliknij go. Zestaw reguł stylów nazwane i kategorie pojawia się w edytorze stylów hello. Każda reguła reprezentuje właściwość style hello wybranego elementu. Na przykład dla hello tekst nagłówka wybranej powyżej, hello rozmiar tekstu hello jest @font-size-h1 w trakcie hello nazwę czcionki hello z alternatyw @headings-font-family.

> Jeśli znasz [bootstrap][bootstrap], te reguły są w istocie [mniej zmienne] [ LESS variables] w hello motywu bootstrap używane przez hello portalu dla deweloperów.
> 
> 

Zmieńmy hello kolor tekstu nagłówka hello. Zaznacz wpis hello hello  **@headings-color**  pole i wpisz **#000000**. To jest kod szesnastkowych hello hello kolor czarny. Zgodnie z tym, możesz sprawdzić, czy wskaźnik koloru kwadratowych jest wyświetlany na końcu hello hello pola tekstowego. Jeśli klikniesz ten wskaźnik próbnika kolorów umożliwia toochoose koloru.

![Selektor kolorów][api-management-customization-toolbar-color-picker]

Zmiany są przeglądany w czasie rzeczywistym, jak to zrobić, ale są widoczne tylko tooadministrators. toomake te zmiany tooeveryone widoczne, kliknij przycisk hello **publikowania** przycisk w edytorze stylów hello i Potwierdź hello zmiany.

![Menu Publikowanie][api-management-customization-toolbar-publish-form]

> toochange hello stylu reguł, które są stosowane tooany innego elementu na stronie powitania, wykonaj hello same procedury jak została ona hello nagłówka. Kliknij przycisk **wybierz element na stronie powitania** z edytora stylów hello, hello wybierz element w i zmodyfikowanie wartości hello reguł stylu hello wyświetlany na ekranie powitania start.
> 
> 


## <a name="next-steps"> </a>Następne kroki
* Dowiedz się, jak zawartość hello toocustomize portalu dla deweloperów strony przy użyciu [szablony portalu deweloperów](api-management-developer-portal-templates.md).

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
