---
title: "Dodawanie do magazynu obiektów Blob Azure Search | Dokumentacja firmy Microsoft"
description: "Tworzenie indeksu za pomocą kodu przy użyciu interfejsu API REST protokołu HTTP usługi Azure Search"
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: 0cd0cbb05c465d32a9ef02f9350ebdf9ccea36c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Przeszukiwanie magazynu obiektów blob za pomocą usługi Azure Search

Wyszukiwanie w różnych typów zawartości, przechowywane w magazynie obiektów Blob platformy Azure może być trudne problem do rozwiązania. Można jednak indeksu i wyszukiwanie zawartości obiektów blob za pomocą kilku kliknięć za pomocą usługi Azure Search. Wyszukiwanie w magazynie obiektów Blob wymaga inicjowania obsługi usługi Azure Search. Różne ograniczenia usługi i warstw cenowych usługi Azure Search znajduje się na [cennikiem](https://aka.ms/azspricing).

## <a name="what-is-azure-search"></a>Co to jest usługa Azure Search?
[Usługa Azure Search](https://aka.ms/whatisazsearch) jest rozwiązaniem wyszukiwania, która ułatwia deweloperom Dodaj niezawodne wyszukiwania pełnotekstowego napotyka sieci web i aplikacji dla urządzeń przenośnych. Jako usługa, usługi Azure Search eliminuje konieczność zarządzania dowolnej infrastruktury wyszukiwania podczas oferty [dostępności 99,9% SLA](https://aka.ms/azuresearchsla).

Zaawansowana obsługa języków w 56 usługi Azure Search można analizować zawartości i inteligentnie obsługi konstrukcje specyficzny dla języka. Usługa Azure Search udostępnia narzędzia umożliwiające tworzenie środowiska użytkownika sformatowanego wyszukiwania. To proste dodać funkcje, takie jak nawigacji aspektowej typeahead sugestie dotyczące wyszukiwania i wyróżnianie interfejsy użytkownika przy użyciu usługi Azure Search trafień. Aby dowiedzieć się więcej o funkcjach usługi Azure Search, możesz przeczytać usługi [dokumentacji](https://aka.ms/azsearchdocs).

## <a name="crack-open-and-search-through-the-content-of-enterprise-document-formats"></a>Otwórz złamać i wyszukiwanie w zawartości formatowania dokumentu enterprise
Z obsługą [dokumentu wyodrębniania](https://aka.ms/azsblobindexer) w magazynie obiektów Blob platformy Azure, Azure Search może indeksować zawartość różnych typów plików przechowywanych w obiektach blob:
- PLIK PDF
- Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT MSG (wiadomości e-mail programu Outlook)
- HTML
- Pliki w formacie zwykłego tekstu

Wyodrębnianie tekstu i metadanych tych typów plików, to ułatwia wyszukiwanie w wielu formatach z pojedynczego zapytania można znaleźć najbardziej odpowiednie dokumenty niezależnie od tego typu. Indeksowanie zawartości i metadanych, dokumentów, plików PDF i wiadomości e-mail programu Microsoft Office, istnieje możliwość rozwiązania do zarządzania zawartością niezawodne przedsiębiorstwa przy użyciu magazynu obiektów Blob i usługi Azure Search.

## <a name="search-through-your-blob-metadata"></a>Przeszukaj metadane obiektu blob
Typowy scenariusz, który ułatwia sortowanie za pośrednictwem obiektów blob typu zawartości jest indeksu dla każdego z obiektów blob metadane obiektu blob niestandardowych, definiowanych przez użytkownika, jak również właściwości systemu. W ten sposób informacje dotyczące każdego obiektu blob jest indeksowany niezależnie od typu dokumentu w obiektów blob, dlatego łatwo można sortować i aspekt we wszystkich zawartości magazynu obiektów Blob.

[Dowiedz się więcej na temat indeksowania metadane obiektu blob.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>Obraz wyszukiwania
Wyszukiwanie pełnotekstowe wyszukiwanie Azure, nawigacji aspektowej i funkcje sortowania teraz mogą być stosowane do metadanych obrazy przechowywane w obiektach blob.

Jeśli te obrazy są wstępnie przetwarzane przy użyciu [komputera wizji API](https://www.microsoft.com/cognitive-services/computer-vision-api) z kognitywnych usług firmy Microsoft, jest możliwość indeksu visual zawartości każdego obrazu, w tym Rozpoznawania i pisma ręcznego. Pracujemy nad dodaniem Rozpoznawania i innych możliwości przetwarzania obrazu bezpośrednio do usługi Azure Search, jeśli planuje się te możliwości Prześlij żądanie na naszych [UserVoice](https://aka.ms/azsuv) lub [Napisz do nas](mailto:azscustquestions@microsoft.com).

## <a name="index-and-search-through-json-blobs"></a>Indeks i wyszukiwania za pomocą obiektów blob JSON
Usługa wyszukiwanie Azure można skonfigurować do wyodrębniania zawartości strukturalnych znaleziono w obiektach blob, które zawierają JSON. Usługa Azure Search może odczytywać obiekty BLOB JSON i przeanalizować uporządkowana zawartość w odpowiednich polach dokument usługi Azure Search. Usługa wyszukiwanie Azure można również wykonać obiektów blob, które zawiera tablicę obiektów JSON i mapowanie każdy element na oddzielnych dokumentu usługi Azure Search.

Należy pamiętać, że analiza kodu JSON nie jest obecnie można konfigurować za pośrednictwem portalu. [Dowiedz się więcej na temat analizowania JSON w usłudze Azure Search.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>Szybki start
Usługa wyszukiwanie Azure można dodać do obiektów blob bezpośrednio z bloku portalu magazynu obiektów Blob.

![](./media/search-blob-storage-integration/blob-blade.png)

Kliknięcie opcji "Dodaj usługi Azure Search" uruchamia przepływ, w którym można wybrać istniejącą usługę Azure Search lub Utwórz nową usługę. Jeśli utworzysz nową usługę zostanie otwarta możliwości portalu konta magazynu. Konieczne będzie ponowne przejdź do bloku portalu magazynu i ponownie wybierz opcję "Dodaj usługi Azure Search", w którym można wybrać istniejącą usługę.

### <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o indeksatora obiektów Blob Azure wyszukiwania z pełnym [dokumentacji](https://aka.ms/azsblobindexer).
