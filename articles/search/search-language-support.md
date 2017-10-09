---
title: "aaaAzure wyszukiwania Obsługa wielu języków | Dokumentacja firmy Microsoft"
description: "Usługa Azure Search obsługuje języki 56 wykorzystaniu analizatorów języka z Lucene i przetwarzania języka naturalnego technologii firmy Microsoft."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Tworzenie indeksu dla dokumentów w wielu językach w usłudze Azure Search
> [!div class="op_single_selector"]
>
> * [Portal](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing moc hello analizatorów języka jest tak proste, jak jedną właściwość ustawienia w polu wyszukiwania w definicji indeksu hello. Teraz można wykonać ten krok w portalu hello.

Poniżej przedstawiono zrzuty ekranu hello bloków portalu Azure do usługi Azure Search, która pozwala toodefine użytkowników schematu indeksu. W tym bloku użytkownicy mogą tworzyć wszystkich pól hello i ustaw właściwość analizatora powitania dla każdego z nich.

> [!IMPORTANT]
> Można ustawić tylko analizatora języka podczas definicję pola, podobnie jak w podczas tworzenia nowego indeksu z hello tła w lub podczas dodawania nowego pola tooan istniejącego indeksu. Upewnij się, że w pełni określić wszystkie atrybuty, w tym analizatora hello podczas tworzenia hello pola. Nie można tooedit stanie atrybuty hello lub zmień typ analizatora hello po zapisaniu zmian.
>
>

## <a name="define-a-new-field-definition"></a>Zdefiniuj nową definicję pola
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) i otwórz hello bloku usługi usługi wyszukiwania.
2. Kliknij przycisk **Dodaj indeks** w poleceniu hello pasek u góry hello toostart pulpitu nawigacyjnego usługi hello nowego indeksu lub Otwórz istniejący tooset indeksu analizatora na nowe pola, które dodajesz tooan istniejący indeks.
3. zostanie wyświetlony blok pola Hello, opcjami do definiowania schematu hello indeksu hello, w tym karty analizatora hello używany do wybierania analizatora języka.
4. W polach należy uruchomić definicja pola podanie nazwy, wybierając typ danych hello i ustawienie pola hello toomark atrybuty jako pełnotekstowe wyszukiwanie, pobieranie w wynikach wyszukiwania, można go użyć w strukturach nawigacji zestawu reguł, można sortować itd.
5. Przed przejściem dalej pola toohello, otwórz hello **analizator** kartę.

![][1]
*tooselect analizatora, kliknij kartę analizatora hello na powitania pola bloku*

## <a name="choose-an-analyzer"></a>Wybierz analizatora
1. Przewiń toofind hello pola, które są definiowane.
2. Jeśli pole hello jako wyszukiwanie nie jest zaznaczone, kliknij przycisk toomark teraz wyboru hello go jako **wyszukiwanie**.
3. Kliknij hello analizatora obszaru toodisplay hello listę dostępnych analizatorów.
4. Wybierz hello analyzer ma toouse.

![][2]
*Wybierz jedną z analizatorów hello obsługiwane dla każdego pola*

Domyślnie wszystkie pola z możliwością przeszukiwania używają hello [analizator standardowe Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) którego jest niezależny od języka. tooview hello pełną listę obsługiwanych analizatorów, zobacz [Obsługa języków w usłudze Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Po wybraniu hello analizatora języków dla pola będzie używany przy każdym żądaniu indeksowanie i wyszukiwania dla tego pola. Jeśli zapytanie jest wystawiony na podstawie wielu pól za pomocą różnych analizatorów, hello zapytania będą przetwarzane niezależnie przez hello analizatorów prawo dla każdego pola.

Wiele sieci web i aplikacji dla urządzeń przenośnych obsługiwać użytkowników na całym świecie hello przy użyciu różnych języków. Jest to możliwe toodefine indeksu dla scenariusza, takich jak ta, tworząc pola dla każdego z języków obsługiwanych.

![][3]
*Definicja indeksu za pomocą pola Opis dla każdego z języków obsługiwanych*

Jeśli język hello agenta hello zapytania jest znany, żądania wyszukiwania może być zakresami tooa określonego pola, używając hello **searchFields** parametr zapytania. Hello następującej kwerendy będą wystawiane tylko względem opis hello w Polski:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

Można zbadać indeksu z portalu hello przy użyciu **Eksplorator wyszukiwania** toopaste w toohello podobne zapytania pokazano powyżej. Eksplorator wyszukiwania jest dostępna z hello paska poleceń w bloku usługi hello. Zobacz [tworzenie zapytań względem indeksu usługi Azure Search w portalu hello](search-explorer.md) szczegółowe informacje.

Czasami hello języka agenta hello zapytania nie jest znany, w których wielkość hello zapytania mogą być wystawiane dla wszystkich pól jednocześnie. W razie potrzeby preferencji wyników w niektórych języku mogą być definiowane przy użyciu [oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx). W poniższym przykładzie hello dopasowań w opisie hello w języku angielskim będą oceniane wyższej toomatches względne w Polski i francuskim:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

Jeśli jesteś deweloperem .NET, należy pamiętać, że można skonfigurować przy użyciu hello analizatorów języka [zestawu .NET SDK usługi Azure Search](http://www.nuget.org/packages/Microsoft.Azure.Search). Najnowsza wersja Hello obsługuje również analizatorów języka Microsoft hello.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
