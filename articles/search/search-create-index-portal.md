---
title: "AAA \"Tworzenie indeksu (portal — usługi Azure Search) | Dokumentacja firmy Microsoft\""
description: "Tworzenie indeksu za pomocą hello portalu Azure."
services: search
manager: jhubbard
author: heidisteen
documentationcenter: 
ms.assetid: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/20/2017
ms.author: heidist
ms.openlocfilehash: 4c5d663499bf73a8883690aa9482b6ba59d1ddf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-azure-portal"></a>Tworzenie indeksu usługi Azure Search przy użyciu hello portalu Azure
> [!div class="op_single_selector"]
> * [Omówienie](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Za pomocą projektanta wbudowanych indeksu hello w tooprototype portalu Azure lub Utwórz [indeksu wyszukiwania](search-what-is-an-index.md) toorun w usłudze Azure Search. 

## <a name="prerequisites"></a>Wymagania wstępne

W tym artykule przyjęto [subskrypcji platformy Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) i [usługi Azure Search](search-create-service-portal.md).  

## <a name="find-your-search-service"></a>Znajdowanie usługi wyszukiwania
1. Zaloguj się toohello strony portalu systemu Azure i przejrzyj hello [wyszukiwania usługi dla subskrypcji](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. Wybierz swoją usługę Azure Search.

## <a name="name-hello-index"></a>Nazwa indeksu hello

1. Kliknij przycisk hello **Dodaj indeks** przycisk na pasku poleceń hello u góry hello hello strony.
2. Nazwa indeksu usługi Azure Search. 
   * Zaczynać się literą.
   * Użyj tylko małe litery, cyfry i łączniki ("-").
   * Ogranicz hello nazwa too60 znaków.

  Nazwa indeksu Hello staje się częścią adresu URL punktu końcowego hello używane w indeksie toohello połączeń i wysyłania żądań HTTP w hello interfejsu API REST wyszukiwanie Azure.

## <a name="define-hello-fields-of-your-index"></a>Definiowanie pól hello indeksu

Skład indeksu obejmuje *pola kolekcji* definiuje hello danych z możliwością wyszukiwania w indeksie. W szczególności określa struktury hello dokumentów, które można przekazać oddzielnie. Kolekcja pól Hello zawiera wymagane i opcjonalne pola o nazwie i wypełniana sposób używania pola hello toodetermine atrybuty indeksu.

1. W hello **Dodawanie indeksu** bloku, kliknij przycisk **pola >** tooslide otwarcie bloku definicji pola hello. 

2. Zaakceptuj hello wygenerowany *klucza* pola typu typem Edm.String. Domyślnie program hello pola o nazwie *identyfikator* , ale można ją zmienić, tak długo, jak spełnia ciąg hello [reguły nazewnictwa](https://docs.microsoft.com/rest/api/searchservice/Naming-rules). Pole klucza jest wymagana dla każdego indeksu usługi Azure Search i musi być ciągiem.

3. Dodaj toofully Określ hello dokumentów, które można przekazać pól. Jeśli dokumenty składają się z *identyfikator*, *nazwa hoteli*, *adres*, *miasta*, i *region*, Utwórz odpowiednie pole dla każdej z nich hello indeksu. Przejrzyj hello [projektowania wskazówki zawarte w poniższej sekcji hello](#design) pomocy podczas ustawiania atrybutów.

4. Opcjonalnie dodaj pola, które są używane wewnętrznie w wyrażeniach filtru. Atrybuty pól hello można ustawić pola tooexclude operacji wyszukiwania.

5. Gdy skończysz, kliknij przycisk **OK** toosave i tworzenie hello indeksu.

## <a name="tips-for-adding-fields"></a>Porady dotyczące — Dodawanie pól

Tworzenie indeksu w portalu hello jest znacznym klawiatury. Wykonując ten przepływ pracy, należy zminimalizować kroki:

1. Najpierw należy utworzyć hello pola listy, wpisując nazwy i ustawianie typów danych.

2. Następnie użyj pól wyboru hello u góry każdego atrybutu toobulk hello ustawienie hello we wszystkich polach, a następnie selektywnie wyczyść pola hello kilka pól, które nie wymagają. Na przykład ciąg pola są zazwyczaj można wyszukiwać. Tak, można kliknąć **pobieranie** i **wyszukiwanie** tooboth hello zwracanych wartości hello pola w wynikach wyszukiwania, a także umożliwia wyszukiwanie pełnotekstowe pola hello. 

<a name="design"></a>
## <a name="design-guidance-for-setting-attributes"></a>Wskazówki dotyczące projektowania do ustawiania atrybutów

Chociaż w dowolnym momencie można dodawać nowe pola, istniejące definicje pól są zablokowane na czas ich istnienia hello hello indeksu. Z tego powodu Deweloperzy zazwyczaj używać portalu hello Tworzenie prostego indeksów, testowanie pomysłów lub przy użyciu hello na stronach portalu toolook ustawienie. Częste iteracji w projekt indeksu jest bardziej wydajne, jeśli wykonujesz podejście oparte na kodzie, dzięki czemu można łatwo odtworzyć indeksu hello.

Analizatory i sugestorów są skojarzone z polami przed zapisaniem hello indeksu. Można tooclick się za pośrednictwem każdej strony z kartami tooadd języka analizatorów lub sugestorów tooyour definicję indeksu.

Pól ciągów często są oznaczone jako **wyszukiwanie** i **pobieranie**.

Wyniki wyszukiwania toonarrow pola używane zawierają **sortowanie**, **Filterable**, i **aspektów**.

Atrybuty pól określają, jak używane pola, np. czy jest używana w wyszukiwania pełnotekstowego, nawigacji aspektowej, sortowanie i tak dalej. Witaj w poniższej tabeli opisano każdy atrybut.

|Atrybut|Opis|  
|---------------|-----------------|  
|**Wyszukiwanie**|Pełnotekstowe wyszukiwanie, podmiotu toolexical analizy takich jak dzielenia wyrazów podczas indeksowania. Jeśli ustawisz wartość tooa wyszukiwanie pola, takie jak "day słoneczna" wewnętrznie go zostanie podzielony na powitania poszczególnych tokeny "Słoneczna" i "day". Aby uzyskać więcej informacji, zobacz [jak Pełna działa wyszukiwania tekstu](search-lucene-query-architecture.md).|  
|**Filtrowanie**|Zawartymi w **$filter** zapytania. Można filtrować polami typu `Edm.String` lub `Collection(Edm.String)` nie zostały poddane dzielenia wyrazów, więc porównania dla tylko dokładne dopasowania. Na przykład, jeśli zostanie ustawiona zbyt takiego pola f "słoneczna day", `$filter=f eq 'sunny'` zostanie ustalone, nie są zgodne, ale `$filter=f eq 'sunny day'` zostanie. |  
|**Sortowanie**|Domyślnie hello system sortujące wyniki według wyników, ale można skonfigurować na podstawie pól w dokumentach hello sortowania. Pola typu `Collection(Edm.String)` nie może być **sortowanie**. |  
|**Tworzenie aspektów**|Zwykle używanych w prezentacji wyników wyszukiwania, która zawiera liczby trafień według kategorii (na przykład hotele w określonym mieście). Nie można użyć tej opcji z polami typu `Edm.GeographyPoint`. Pola typu `Edm.String` , które są **filtrowanie**, **sortowanie**, lub **aspektów** może mieć maksymalnie 32 kilobajty długości. Aby uzyskać więcej informacji, zobacz [Create Index (interfejsu API REST)](https://docs.microsoft.com/rest/api/searchservice/create-index).|  
|**klucz**|Unikatowy identyfikator dla dokumentów w ramach hello indeksu. Należy wybrać dokładnie jedno pole jako pole klucza hello i musi być typu `Edm.String`.|  
|**Pobieranie**|Określa, czy pole hello może być zwracany w wynikach wyszukiwania. Jest to przydatne, jeśli chcesz toouse pola (takich jak *marża*) jako filtru, sortowania lub oceniania mechanizmu, ale, czy nie chcesz, aby hello pola toobe widoczne toohello użytkownika końcowego. Ten atrybut musi być `true` dla `key` pola.|  

## <a name="create-hello-hotels-index-used-in-example-api-sections"></a>Tworzenie indeksu hotels hello używane w sekcjach interfejsu API przykład

Azure dokumentacji interfejsu API Search przykłady kodu, oferujący funkcje prostą *hotele* indeksu. Poniższe zrzuty ekranu hello, zawiera definicję indeksu hello, łącznie z analizatora języka francuskiego hello określone w definicji indeksu, który można odtworzyć jako ćwiczenia, w portalu hello.

![](./media/search-create-index-portal/field-definitions.png)

![](./media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a>Następne kroki

Po utworzeniu indeksu usługi Azure Search, możesz przenieść toohello następnego kroku: [przekazywanie danych z możliwością wyszukiwania do indeksu hello](search-what-is-data-import.md).

Alternatywnie możesz można również Przyjrzyjmy się głębiej indeksów. Ponadto toohello kolekcji pól, indeks określa również analizatory, sugestorów oceniania profile i ustawienia specyfikacji CORS. Hello portal zawiera karty do definiowania często spotykanych elementów hello: pola, analizatory i sugestorów. toocreate lub zmodyfikuj inne elementy, możesz użyć hello interfejsu API REST lub zestawu .NET SDK.

## <a name="see-also"></a>Zobacz też

 [Jak działa wyszukiwanie pełnotekstowe](search-lucene-query-architecture.md)  
 [Usługi interfejsu API REST wyszukiwania](https://docs.microsoft.com/rest/api/searchservice/) [zestawu .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/search?view=azure-dotnet)

