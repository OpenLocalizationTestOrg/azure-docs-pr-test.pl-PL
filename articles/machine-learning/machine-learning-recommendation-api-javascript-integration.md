---
title: 'Machine Learning zalecenia: Integracja JavaScript | Dokumentacja firmy Microsoft'
description: "Dokumentację platformy Azure zalecenia dotyczące — integracja JavaScript - Learning maszyny"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Zalecenia dotyczące usługi Azure Machine Learning — integracja JavaScript
> [!NOTE]
> Należy rozpocząć korzystanie z usługi kognitywnych interfejsu API zalecenia zamiast tej wersji. Kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną nowe funkcje. Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.
> Dowiedz się więcej o [migracji do nowej usługi kognitywnych](http://aka.ms/recomigrate)
> 
> 

Ten dokument przedstawiać integrowanie witryny przy użyciu języka JavaScript. JavaScript umożliwia wysyłanie danych zdarzeń i zużywać zalecenia po utworzeniu modelu zalecenie. Wszystkie operacje wykonywane za pośrednictwem JS jest również możliwe po stronie serwera.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Ogólne omówienie
Integrowanie witryny z usługi Azure ML zalecenia składają się na fazy 2:

1. Wysyłanie zdarzeń do usługi Azure ML zalecenia. Spowoduje to włączenie do tworzenia modelu zalecenia.
2. Używać zalecenia. Po utworzeniu modelu może wykorzystać zalecenia. (Ten dokument nie wyjaśniono, jak do tworzenia modelu, przeczytaj Przewodnik Szybki start, aby uzyskać więcej informacji na temat).

<ins>Faza I</ins>

W pierwszej fazie należy wstawić na stronach html małych biblioteki JavaScript, która umożliwia stronę, aby wysyłać zdarzenia występujące na stronie html do serwerów usługi Azure ML zalecenia (za pośrednictwem rynku danych):

![Drawing1][1]

<ins>Faza II</ins>

W drugim etapie, gdy chcesz pokazać zalecenia na stronie wybierz jedną z następujących opcji:

1. serwera (na etapie renderowania stron) wywołuje Azure ML zalecenia dotyczące serwera (za pośrednictwem rynku danych) można uzyskać zalecenia. Wyniki obejmują listę elementów id. Serwer musi wzbogacić wyników z elementami metadanych (np. obrazów, opis) i wysyłany do przeglądarki, utworzonej strony.

![Drawing2][2]

2. druga opcja to na mały plik JavaScript z pierwszą fazę prosta lista elementów zalecane. Dane otrzymane w tym miejscu jest leaner niż ten, w pierwszej opcji.

![Drawing3][3]

## <a name="2-prerequisites"></a>2. Wymagania wstępne
1. Utwórz nowy model przy użyciu interfejsów API. Jak to zrobić, zobacz Przewodnik Szybki start.
2. Kodowanie z &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; z formatu base64. (Ten będzie służyć do uwierzytelniania podstawowego do włączenia kodu Javascript do wywołania interfejsów API).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Wysyłanie zdarzeń danych przy użyciu języka JavaScript
Poniższe kroki ułatwiają wysyłanie zdarzeń:

1. Uwzględnij biblioteki JQuery w kodzie. Można go pobrać z nuget następujący adres URL.
   
     http://www.nuget.org/Packages/jQuery/1.8.2
2. Obejmują biblioteki skryptów Java zalecenia z następującego adresu URL: http://aka.ms/RecoJSLib1
3. Zainicjowanie biblioteki Azure ML zalecenia z odpowiednimi parametrami.
   
     <script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Wysłać odpowiednie zdarzenia. Zobacz poniższą sekcję szczegółowe na wszystkich typów zdarzeń (Zdarzenie kliknięcia przykład) <script> Jeśli (typeof AzureMLRecommendationsEvent == "undefined") {         
                     AzureMLRecommendationsEvent =] } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Ograniczenia i obsługa przeglądarek
Jest to implementacja odwołania i jest on podawany jest. Należy go obsługuje wszystkie główne przeglądarki.

### <a name="32----type-of-events"></a>3.2.    Typ zdarzenia
Istnieje 5 typów zdarzeń, które obsługuje biblioteki: kliknij przycisk, kliknij zalecenie, Dodaj do koszyka sklep, Usuń z koszyka produkcyjny i zakupu. Brak dodatkowych zdarzeń, która jest używana do ustawiania kontekstu użytkownika o nazwie logowania.

#### <a name="321-click-event"></a>3.2.1. Zdarzenie kliknięcia
To zdarzenie powinny być używane w dowolnym momencie, a użytkownik kliknął element. Zwykle, gdy użytkownik kliknie element Nowa strona zostanie otwarty z szczegóły elementu; na tej stronie to zdarzenie jest wyzwalane.

Parametry:

* zdarzenia (ciąg, obowiązkowe) "kliknij"
* Unikatowy identyfikator elementu (ciąg, obowiązkowe) — element
* Nazwa elementu (ciąg, opcjonalnie) nazwa elementu
* itemDescription (ciąg, opcjonalny) - opis elementu
* itemCategory (ciąg, opcjonalny) kategorii elementu
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

Lub z opcjonalnymi danymi:

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a>3.2.2. Zalecenie Zdarzenie kliknięcia
To zdarzenie powinny być używane w dowolnym momencie, a użytkownik kliknął element otrzymanego od zaleceń uczenia Maszynowego Azure jako element zalecane. Zwykle, gdy użytkownik kliknie element Nowa strona zostanie otwarty z szczegóły elementu; na tej stronie to zdarzenie jest wyzwalane.

Parametry:

* zdarzenia (ciąg, obowiązkowe) "recommendationclick"
* Unikatowy identyfikator elementu (ciąg, obowiązkowe) — element
* Nazwa elementu (ciąg, opcjonalnie) nazwa elementu
* itemDescription (ciąg, opcjonalny) - opis elementu
* itemCategory (ciąg, opcjonalny) kategorii elementu
* nasiona (tablicy ciągów, opcjonalny) - ziarna wygenerowanych zapytania zalecenia.
* recoList (tablicy ciągów, opcjonalny) - wynik żądania zalecenie, który wygenerował element, który został kliknięty.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

Lub z opcjonalnymi danymi:

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a>3.2.3. Dodawanie zdarzeń koszyka zakupów
To zdarzenie powinna być używana podczas użytkownika dodania elementu do koszyka.
Parametry:

* zdarzenia (ciąg, obowiązkowe) "addshopcart"
* Unikatowy identyfikator elementu (ciąg, obowiązkowe) — element
* Nazwa elementu (ciąg, opcjonalnie) nazwa elementu
* itemDescription (ciąg, opcjonalny) - opis elementu
* itemCategory (ciąg, opcjonalny) kategorii elementu
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Usuń zdarzenia z koszyka zakupów
To zdarzenie powinien być używany, gdy użytkownik usuwa element do koszyka.

Parametry:

* zdarzenia (ciąg, obowiązkowe) "removeshopcart"
* Unikatowy identyfikator elementu (ciąg, obowiązkowe) — element
* Nazwa elementu (ciąg, opcjonalnie) nazwa elementu
* itemDescription (ciąg, opcjonalny) - opis elementu
* itemCategory (ciąg, opcjonalny) kategorii elementu
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Zdarzenie zakupu
To zdarzenie powinien być używany, gdy użytkownik zakupionych jego koszyk.

Parametry:

* zdarzenia (ciąg) "Kup"
* elementy (zakupione []) - zawierający wpis dla każdego elementu zakupionych tablicy.<br><br>
  Format zakupionych:
  * element (string) — Unikatowy identyfikator elementu.
  * Liczba (int lub string) — liczba elementów, które zostały zakupione.
  * Cena (float lub string) — pole opcjonalne - cen elementu.

W poniższym przykładzie pokazano zakupu 3 elementy (33, 34, 35), dwa wszystkich pól (element, count, cena) oraz jedną (element 34) bez ceny.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Zdarzenia logowania użytkownika
Biblioteki zdarzeń zalecenia dotyczące uczenia Maszynowego Azure tworzy i korzystania z pliku cookie w celu identyfikacji zdarzenia, które pochodzą z tej samej przeglądarce. W celu ulepszania wyniki modelu zalecenia dotyczące uczenia Maszynowego Azure umożliwia ustalenie Unikatowy identyfikator użytkownika, który zastąpi użycia plików cookie.

To zdarzenie powinny być używane po logowaniu użytkownika do witryny.

Parametry:

* zdarzenia (ciąg) "userlogin"
* Użytkownik (string) — Unikatowy identyfikator użytkownika.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Korzystanie z zalecenia za pośrednictwem kodu JavaScript
Kod, który wykorzystuje zalecenie jest wyzwalany przez zdarzenie JavaScript przez klienta strony sieci Web. Odpowiedź zalecenie zawiera identyfikatory elementów zalecane, ich nazwy i ich klasyfikacji. Najlepiej użyć tej opcji tylko w przypadku wyświetlania listy elementów zalecane — Obsługa bardziej złożonych (takie jak dodanie metadanych elementu) ma się odbywać na integracji po stronie serwera.

### <a name="41-consume-recommendations"></a>4.1 korzystać zalecenia
Korzystać z zaleceń, które należy uwzględnić wymaganych bibliotek JavaScript na stronie oraz wywołanie AzureMLRecommendationsStart. W sekcji 2.

Użycie zalecenia dla jednego lub więcej elementów, należy wywołać metodę o nazwie: AzureMLRecommendationsGetI2IRecommendation.

Parametry:

* elementy (tablicę ciągów) — co najmniej jeden element, aby uzyskać zalecenia dotyczące. Jeśli zostaną zużyte na kompilację zmianie wysokości progów, można ustawić tutaj tylko jeden element.
* numberOfResults (int) - liczba wymaganych wyników.
* includeMetadata (wartość logiczna, opcjonalny) — Jeśli ma wartość "true" wskazuje, czy pole metadanych powinno zostać zapełnione w wyniku.
* Funkcja przetwarzania — funkcja, która będzie obsługiwać zalecenia zwracane. Dane są zwracane jako tablica:
  * Identyfikator unikatowy element — element
  * Nazwa — Nazwa elementu (jeśli istnieje w katalogu)
  * Ocena — zaleceniem klasyfikacji
  * metadane — ciąg reprezentujący metadanych elementu

Przykład: Następujący kod żądań 8 zalecenia dla elementu "64f6eb0d-947a-4c18-a16c-888da9e228ba" (bez określania includeMetadata - niejawnie wskazanego czy metadanych nie jest wymagane), następnie połącz wyniki do buforu.

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
