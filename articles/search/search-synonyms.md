---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Wstępne dokumentacji funkcji synonimy (wersja zapoznawcza) hello w hello interfejsu API REST wyszukiwanie Azure."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a>Synonimy w usłudze Azure Search (wersja zapoznawcza)

Synonimy w wyszukiwarkach skojarzyć równoważnego niejawnie rozszerzające zakres hello kwerendy, bez hello użytkownika mającego tooactually Podaj hello terminu. Na przykład danego hello termin "dog" i skojarzenia synonim "pies" i "puppy" dokumenty zawierające "kot", "pies" lub "puppy" będzie mieścić się w zakresie hello hello zapytania.

W usłudze Azure Search rozszerzenia synonim odbywa się na etapie zapytania. Można dodać usługi tooa mapy synonim z operacjami tooexisting nie przerw w działaniu. Możesz dodać **synonymMaps** definicji pola tooa właściwości bez konieczności toorebuild hello indeksu. Aby uzyskać więcej informacji, zobacz [Aktualizuj indeks](https://docs.microsoft.com/rest/api/searchservice/update-index).

## <a name="feature-availability"></a>Dostępność funkcji

synonimy Hello funkcja jest aktualnie Podgląd i obsługiwana w tylko hello najnowszej wersji zapoznawczej wersji interfejsu api (interfejs api-version = 2016-09-01-Preview). Obecnie witryna Azure Portal nie jest obsługiwana. Ponieważ w żądaniu hello jest określona wersja interfejsu API hello, jest ogólnie dostępna możliwe toocombine (GA) i Podgląd interfejsów API w hello tej samej aplikacji. Jednak Podgląd interfejsów API nie są w ramach umowy dotyczącej poziomu usług i funkcji mogą ulec zmianie, dlatego nie zaleca się stosowanie ich w aplikacjach produkcyjnych.

## <a name="how-toouse-synonyms-in-azure-search"></a>Sposób wyszukiwania synonimy toouse na platformie Azure

W usłudze Azure Search synonim pomocy technicznej jest oparta na mapy synonim zdefiniowaniu i usługa tooyour przekazywania. Mapy te stanowią niezależnym zasobem (jak indeksy lub źródeł danych) i mogą być używane przez wszystkie pola można wyszukiwać w indeksu w swojej usłudze wyszukiwania.

Synonim map i indeksów są przechowywane niezależnie od siebie. Po zdefiniowaniu mapy synonim i usługa tooyour przekazywania, można włączyć funkcję synonim hello na pole, dodając nową właściwość o nazwie **synonymMaps** w definicji pola hello. Tworzenie, aktualizowanie i usuwanie mapy synonim zawsze jest operacją całego dokumentu, co oznacza, że nie można utworzyć, zaktualizować lub usunąć elementy mapy synonim hello przyrostowo. Aktualizowanie nawet pojedynczy wpis wymaga ponowne załadowanie.

Dołączanie do aplikacji wyszukiwania synonimy jest procesem dwuetapowym:

1.  Dodaj usługę wyszukiwania synonim mapy tooyour za pośrednictwem hello interfejsów API poniżej.  

2.  W definicji indeksu hello, należy skonfigurować mapę synonim hello toouse pola wyszukiwania.

### <a name="synonymmaps-resource-apis"></a>Interfejsy API SynonymMaps zasobów

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>Dodać lub zaktualizować synonimu mapy w ramach usługi, za pomocą POST i PUT.

Synonim mapy są przekazywane toohello usługi za pośrednictwem POST i PUT. Każda reguła muszą być rozdzielane przy hello znaku nowego wiersza ("\n"). Można zdefiniować too5, 000 reguł na mapie synonim w bezpłatnej usługi i 10 000 reguł w innych jednostki SKU. Każda reguła może zawierać maksymalnie too20 rozszerzenia.

W tej wersji zapoznawczej synonimu mapy musi być w formacie Apache Solr hello, który znajduje się poniżej. Jeśli masz istniejący słownik synonim w innym formacie i chcesz toouse go bezpośrednio, prosimy o kontakt na [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

Można utworzyć nowej mapy synonim przy użyciu protokołu HTTP POST, tak jak hello poniższy przykład:

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

Alternatywnie można użyć PUT i określ nazwę mapy synonim hello na powitania identyfikatora URI. Mapa synonim hello nie istnieje, zostanie utworzona.

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Format synonim Apache Solr

Hello Solr format obsługuje synonim równoważne i jawnego mapowania. Reguły mapowania odpowiednia toohello typu open source synonim specyfikację filtru Apache Solr, w tym dokumencie opisano: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter). Poniżej znajduje się przykładowa reguła synonimy równoważne.
```
              USA, United States, United States of America
```

Z regułą hello powyżej, zapytania wyszukiwania "USA" rozwinie zbyt "USA" lub "Stany Zjednoczone" lub "Stany Zjednoczone".

Jawne mapowanie jest oznaczona za pomocą strzałki "= >". Gdy jest określony, sekwencji termin zapytania wyszukiwania, które odpowiada hello lewą "= >" zostanie zamieniony alternatyw hello na powitania po prawej stronie. Podana reguła hello poniżej, wyszukaj zapytania "W stanie Waszyngton", "Wash." lub "WA" będą wszystkie ponownego napisania zbyt "WA". Jawne mapowanie tylko ma zastosowanie w kierunku hello określony i nie przepisywania hello zapytania "WA" za "Waszyngton" w tym przypadku.
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>Synonim listy mapy w ramach usługi.

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>Uzyskać synonim mapy w ramach usługi.

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>Usuń synonimy mapy w ramach usługi.

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>W definicji indeksu hello, należy skonfigurować mapę synonim hello toouse pola wyszukiwania.

Nowe właściwości pola **synonymMaps** mogą być używane toospecify synonim toouse mapy dla pola wyszukiwania. Synonim mapy zasobów poziomu usługi i mogą odwoływać się do dowolnego pola indeksu w ramach usługi hello.

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

**synonymMaps** można określić w przypadku pól z możliwością wyszukiwania hello typu "Z typem Edm.String" lub "Collection(Edm.String)".

> [!NOTE]
> W tej wersji zapoznawczej może mieć tylko jeden synonim mapy jednym polu. Jeśli chcesz toouse wielu map synonim, prosimy o kontakt na [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="impact-of-synonyms-on-other-search-features"></a>Wpływ synonimy dla innych funkcji wyszukiwania

Funkcja synonimy Hello ponownie zapisuje hello oryginalne zapytanie z synonimy z hello operatora OR. Z tego powodu wyróżnianie trafień i oceniania profile traktować hello pierwotny termin i synonimy jako równoważne.

Funkcja synonim stosuje zapytania toosearch i nie ma zastosowania toofilters lub aspektami. Podobnie sugestie dotyczą tylko hello pierwotny termin; synonim dopasowań nie są wyświetlane w hello odpowiedzi.

Synonim rozszerzenia nie są stosowane terminy wyszukiwania toowildcard; Prefiks rozmytego oraz postanowienia wyrażenia regularnego nie są rozwinięte.

## <a name="tips-for-building-a-synonym-map"></a>Wskazówki dotyczące tworzenia mapy synonim

- Mapa synonim zwięzły, dobrze zaprojektowanego jest bardziej efektywne niż pełny wykaz możliwe dopasowania. Bardzo dużych lub złożonych słowniki trwać dłużej tooparse i wpływać na hello zapytania opóźnienia, jeśli zapytanie hello rozszerza synonimy toomany. Zamiast dopasowanie warunki mogą być używane, można uzyskać rzeczywiste warunki hello za pośrednictwem [raport analizy ruchu wyszukiwania](search-traffic-analytics.md).

- Jako wykonywania zarówno wersja wstępna i sprawdzania poprawności, należy włączyć, a następnie użyj tego raportu tooprecisely określić terminów będzie korzystać z dopasowanie synonim, a następnie kontynuuj toouse go jako że mapy synonim jest tworzenie lepsze wyniki sprawdzania poprawności. W raporcie wstępnie zdefiniowane hello hello Kafelki "najbardziej typowe zapytania wyszukiwania" i "Zero wynik zapytania wyszukiwania" zapewni hello niezbędne informacje.

- Można utworzyć wielu map synonim aplikacji wyszukiwania (np. według języka, jeśli aplikacja obsługuje wielu języków bazy klientów). Obecnie pola można używać tylko jeden z nich. W dowolnym momencie możesz zaktualizować właściwość synonymMaps pola.

## <a name="next-steps"></a>Następne kroki

- Jeśli masz istniejący indeks w środowisku projektowym (z systemem innym niż środowisko produkcyjne) eksperymentować toosee małych słownika jak dodanie hello synonimy zmienia hello środowiska wyszukiwania, włączając wpływ na oceniania profile trafień wyróżnianie i sugestie.

- [Włącz analizy ruchu wyszukiwania](search-traffic-analytics.md) i hello Użyj wstępnie zdefiniowanych raportów usługi Power BI toolearn, których terminy są używane Witaj, większości i które te zwracane dokumentów. Dzięki te szczegółowe informacje, sprawdź, czy hello słownika tooinclude synonimy nieproduktywne zapytań, które powinny być rozpoznawania toodocuments w indeksie.
