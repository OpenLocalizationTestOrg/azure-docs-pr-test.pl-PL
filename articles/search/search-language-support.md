---
title: "Usługa Azure Search Obsługa wielu języków | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: dbbab31bac66ce73dbf9883992713a2c16581e19
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/21/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Tworzenie indeksu dla dokumentów w wielu językach w usłudze Azure Search
> [!div class="op_single_selector"]
>
> * [Portal](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing zasilania analizatorów języka jest tak proste, jak jedną właściwość ustawienia w polu wyszukiwania w definicji indeksu. Teraz można wykonać ten krok w portalu.

Poniżej przedstawiono zrzuty ekranu bloków portalu Azure do usługi Azure Search, która pozwala użytkownikom na definiowanie schematu indeksu. W tym bloku użytkownicy mogą tworzyć wszystkich pól i ustaw właściwość analizatora dla każdego z nich.

> [!IMPORTANT]
> Można ustawić tylko analizatora języka podczas definicję pola, jak podczas tworzenia nowego indeksu od podstaw w górę lub dodając nowe pole do istniejącego indeksu. Upewnij się, że w pełni określić wszystkie atrybuty, włączając analizator, podczas tworzenia w polu. Nie można edytować atrybutów lub zmień typ analizator po zapisaniu zmian.
>
>

## <a name="define-a-new-field-definition"></a>Zdefiniuj nową definicję pola
1. Zaloguj się do [portalu Azure](https://portal.azure.com) i otwórz blok usługi z usługą wyszukiwania.
2. Kliknij przycisk **Dodaj indeks** na pasku poleceń, w górnej części pulpitu nawigacyjnego usługi, aby uruchomić nowego indeksu lub Otwórz istniejący indeks, aby ustawić analizator na nowe pola, które dodajesz do istniejącego indeksu.
3. Zostanie wyświetlony blok pola, opcjami do definiowania schematu indeksu, w tym karty analizator używany do wybierania analizatora języka.
4. W polach należy uruchomić definicja pola podanie nazwy, wybierając typ danych i ustawienie atrybuty pole jako pełnotekstowe wyszukiwanie, pobieranie w wynikach wyszukiwania, można go użyć w strukturach nawigacji zestawu reguł, można sortować itd.
5. Przed przejściem do następnego pola, otwórz **analizator** kartę.

![][1]
*Aby wybrać analizatora, kliknij kartę analizator w bloku pól*

## <a name="choose-an-analyzer"></a>Wybierz analizatora
1. Przewiń do pola, które są definiowane.
2. Jeśli nie zostało oznaczone jako wyszukiwanie, kliknij pole wyboru teraz, aby oznaczyć go jako **wyszukiwanie**.
3. Kliknij obszar analizatora, aby wyświetlić listę dostępnych analizatorów.
4. Wybierz analizator, którego chcesz użyć.

![][2]
*Wybierz jedną z obsługiwanych analizatorów dla każdego pola*

Domyślnie używają wszystkie pola z możliwością przeszukiwania [analizator standardowe Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) którego jest niezależny od języka. Aby wyświetlić pełną listę obsługiwanych analizatorów, zobacz [Obsługa języków w usłudze Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Po wybraniu analizatora języków dla pola będzie używany przy każdym żądaniu indeksowanie i wyszukiwania dla tego pola. Jeśli zapytanie jest wystawiony na podstawie wielu pól za pomocą różnych analizatorów, zapytania będą przetwarzane niezależnie przez prawo analizatorów dla każdego pola.

Wiele sieci web i aplikacji dla urządzeń przenośnych obsługiwać użytkowników na całym świecie przy użyciu różnych języków. Istnieje możliwość definiowania indeksu dla scenariusza następująco tworząc pola dla każdego z języków obsługiwanych.

![][3]
*Definicja indeksu za pomocą pola Opis dla każdego z języków obsługiwanych*

Jeśli język agenta zapytania jest znany, żądania wyszukiwania może należeć do zakresu określonego pola przy użyciu **searchFields** parametr zapytania. Następujące zapytanie będą wystawiane tylko względem opis w Polski:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

Można zbadać indeksu z portalu, za pomocą **Eksplorator wyszukiwania** wkleić w zapytaniu podobny do przedstawionego powyżej. Eksplorator wyszukiwania jest dostępna z paska poleceń w bloku usługi. Zobacz [tworzenie zapytań względem indeksu usługi Azure Search w portalu](search-explorer.md) szczegółowe informacje.

Czasami język agenta zapytania nie jest znany, w którym to przypadku zapytania mogą być wystawiane dla wszystkich pól jednocześnie. W razie potrzeby preferencji wyników w niektórych języku mogą być definiowane przy użyciu [oceniania profile](https://msdn.microsoft.com/library/azure/dn798928.aspx). W poniższym przykładzie dopasowań w opisie w języku angielskim będą oceniane wyższy względem dopasowań w Polski i francuskim:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

Jeśli jesteś deweloperem .NET, należy pamiętać, że można skonfigurować za pomocą analizatorów języka [zestawu .NET SDK usługi Azure Search](http://www.nuget.org/packages/Microsoft.Azure.Search). Najnowsza wersja obsługuje również analizatorów języka Microsoft.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
