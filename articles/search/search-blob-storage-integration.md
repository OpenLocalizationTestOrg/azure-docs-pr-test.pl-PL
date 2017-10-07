---
title: "aaaAdding usługi Azure Search tooBlob magazynu | Dokumentacja firmy Microsoft"
description: "Tworzenie indeksu za pomocą interfejsu API REST usługi Azure Search HTTP hello kodu."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: a3801790067bf169693b500e83799286b7387a77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Przeszukiwanie magazynu obiektów blob za pomocą usługi Azure Search

Wyszukiwanie w hello różnych typów zawartości, przechowywane w magazynie obiektów Blob platformy Azure można toosolve problem trudne. Jednak indeksu i wyszukiwania hello zawartości obiektów blob za pomocą kilku kliknięć przy użyciu usługi Azure Search. Wyszukiwanie w magazynie obiektów Blob wymaga inicjowania obsługi usługi Azure Search. Witaj różne ograniczenia usługi i ceny warstw usługi Azure Search znajduje się na powitania [cennikiem](https://aka.ms/azspricing).

## <a name="what-is-azure-search"></a>Co to jest usługa Azure Search?
[Usługa Azure Search](https://aka.ms/whatisazsearch) jest rozwiązaniem wyszukiwania, która ułatwia deweloperom tooadd niezawodne wyszukiwania pełnotekstowego napotyka tooweb i aplikacji dla urządzeń przenośnych. Jako usługa, usługi Azure Search usuwa toomanage potrzeby hello dowolnej infrastruktury wyszukiwania podczas oferty [dostępności 99,9% SLA](https://aka.ms/azuresearchsla).

Zaawansowana obsługa języków w 56 usługi Azure Search można analizować zawartości i inteligentnie obsługi konstrukcje specyficzny dla języka. Wyszukiwanie Azure udostępnia hello narzędzia toobuild środowisko użytkownika sformatowanego wyszukiwania. To proste tooadd funkcje, takie jak nawigacji aspektowej, typeahead sugestie dotyczące wyszukiwania i trafień wyróżnienia interfejsy toouser przy użyciu usługi Azure Search. toolearn funkcje usługi Azure Search, możesz przeczytać hello usługi [dokumentacji](https://aka.ms/azsearchdocs).

## <a name="crack-open-and-search-through-hello-content-of-enterprise-document-formats"></a>Otwórz złamać i wyszukiwania za pomocą zawartości hello formatów dokumentu enterprise
Z obsługą [dokumentu wyodrębniania](https://aka.ms/azsblobindexer) w magazynie obiektów Blob platformy Azure, Azure Search może indeksować zawartość hello różnych typów plików przechowywanych w obiektach blob:
- PLIK PDF
- Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT MSG (wiadomości e-mail programu Outlook)
- HTML
- Pliki w formacie zwykłego tekstu

Wyodrębniając tekstu i metadanych tych typów plików, jest łatwe toosearch przez wiele formatów plików z jednego zapytania toofind hello najistotniejsza dokumentami niezależnie od tego typu. Przez indeksowanie metadanych zawartości i hello hello dokumentów Microsoft Office, plików PDF i wiadomości e-mail, jego toobuild możliwe rozwiązania zarządzania zawartością niezawodne przedsiębiorstwa przy użyciu magazynu obiektów Blob i usługi Azure Search.

## <a name="search-through-your-blob-metadata"></a>Przeszukaj metadane obiektu blob
Typowy scenariusz, który umożliwia łatwe toosort za pośrednictwem obiektów blob typu zawartości jest metadane obiektu blob niestandardowych, definiowanych przez użytkownika hello tooindex, jak również hello właściwości systemu dla każdego z obiektów blob. W ten sposób informacje dotyczące każdego obiektu blob jest indeksowany niezależnie od typu hello dokumentu w hello obiektów blob, dlatego łatwo można sortować i aspekt we wszystkich zawartości magazynu obiektów Blob.

[Dowiedz się więcej na temat indeksowania metadane obiektu blob.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>Obraz wyszukiwania
Usługa Azure Search wyszukiwania pełnotekstowego, nawigacji aspektowej i sortowanie możliwości można teraz toohello zastosowane metadane przechowywane w obiektach blob obrazów.

Jeśli te obrazy są wstępnie przetwarzane przy użyciu hello [komputera wizji API](https://www.microsoft.com/cognitive-services/computer-vision-api) z kognitywnych usług firmy Microsoft, będzie ona wówczas możliwe tooindex hello graficznej zawartości w każdym obrazu, w tym Rozpoznawania i pisma ręcznego. Pracujemy nad Dodawanie Rozpoznawania i inne obrazu możliwości przetwarzania bezpośrednio tooAzure wyszukiwania, jeśli planuje się te możliwości Prześlij żądanie na naszych [UserVoice](https://aka.ms/azsuv) lub [Napisz do nas](mailto:azscustquestions@microsoft.com).

## <a name="index-and-search-through-json-blobs"></a>Indeks i wyszukiwania za pomocą obiektów blob JSON
Usługa Azure Search może być skonfigurowany tooextract strukturę zawartość w obiektach blob, które zawierają JSON. Usługa Azure Search może odczytywać obiekty BLOB JSON i przeanalizować hello strukturę zawartości do odpowiednich pól hello dokumentu usługi Azure Search. Usługa wyszukiwanie Azure można również wykonać obiektów blob, które zawiera tablicę obiektów JSON i mapowanie każdego elementu tooa oddzielne usługi Azure Search dokumentu.

Należy pamiętać, że analiza kodu JSON nie jest obecnie można konfigurować za pośrednictwem portalu hello. [Dowiedz się więcej na temat analizowania JSON w usłudze Azure Search.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>Szybki start
Usługa wyszukiwanie Azure można dodać tooblobs bezpośrednio z hello bloku portalu magazynu obiektów Blob.

![](./media/search-blob-storage-integration/blob-blade.png)

Kliknięcie opcji "Dodaj usługi Azure Search" hello uruchamia przepływ, w którym można wybrać istniejącą usługę Azure Search lub Utwórz nową usługę. Jeśli utworzysz nową usługę zostanie otwarta możliwości portalu konta magazynu. Konieczne będzie toore-przejdź do bloku portalu toohello magazynu i ponownie wybierz opcję "Dodaj usługi Azure Search" hello, którym można wybrać istniejącą usługę hello.

### <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o hello Azure Search Blob indeksatora w hello pełne [dokumentacji](https://aka.ms/azsblobindexer).
