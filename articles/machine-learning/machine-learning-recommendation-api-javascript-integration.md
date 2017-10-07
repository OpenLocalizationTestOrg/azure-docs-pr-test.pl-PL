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
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a>Zalecenia dotyczące usługi Azure Machine Learning — integracja JavaScript
> [!NOTE]
> Należy rozpocząć za pomocą hello usługi kognitywnych zalecenia dotyczące interfejsu API, zamiast tej wersji. Hello kognitywnych usługę rekomendacji spowoduje zastąpienie tej usługi, a opracowane zostaną wszystkie hello nowe funkcje. Ma on nowe funkcje, takie jak przetwarzanie wsadowe pomocy technicznej, lepiej Explorer interfejsu API, czyszczący środowisko signup/rozliczeń powierzchni, bardziej spójny interfejs API,... itd.
> Dowiedz się więcej o [toohello Migrowanie nową usługę kognitywnych](http://aka.ms/recomigrate)
> 
> 

Ten dokument przedstawiać jak toointegrate witryny przy użyciu języka JavaScript. Hello JavaScript umożliwia toosend pozyskiwania danych zdarzeń i zalecenia tooconsume po utworzeniu modelu zalecenia. Wszystkie operacje wykonywane za pośrednictwem JS jest również możliwe po stronie serwera.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Ogólne omówienie
Integrowanie witryny z usługi Azure ML zalecenia składają się na fazy 2:

1. Wysyłanie zdarzeń do usługi Azure ML zalecenia. Spowoduje to włączenie toobuild modelu zalecenia.
2. Używać hello zalecenia. Po utworzeniu modelu hello mogą zużywać hello zalecenia. (Ten dokument nie wyjaśniono, jak toobuild modelu, przeczytaj hello tooget Przewodnik Szybki start więcej informacji na temat).

<ins>Faza I</ins>

Hello pierwszą fazę wstawić na stronach html małych biblioteka języka JavaScript, która umożliwia hello strony toosend zdarzenia występujące na stronie html hello na serwerach Azure ML zalecenia (za pośrednictwem rynku danych):

![Drawing1][1]

<ins>Faza II</ins>

W hello drugiej fazy, kiedy zechcesz zalecenia hello tooshow na stronie powitania wybraniu jednej z hello następujące opcje:

1. serwer (na etapie hello renderowania stron) wywołuje zalecenia tooget Azure ML zalecenia serwera (za pośrednictwem rynku danych). Witaj wyniki obejmują listę elementów id. Serwer musi tooenrich hello wyników z elementami hello metadanych (np. obrazów, opis) i wysłać hello utworzona strona toohello przeglądarki.

![Drawing2][2]

2. Witaj druga opcja to toouse hello mały plik JavaScript z fazy jeden tooget to prosta lista elementów zalecane. w tym miejscu odebrane dane Hello jest leaner niż jeden hello w pierwszej opcji hello.

![Drawing3][3]

## <a name="2-prerequisites"></a>2. Wymagania wstępne
1. Utwórz nowy model przy użyciu hello interfejsów API. Zobacz Przewodnik Szybki start hello na temat toodo go.
2. Kodowanie z &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; z formatu base64. (Ten będzie służyć do hello uwierzytelnianie podstawowe tooenable hello JS kodu toocall hello interfejsów API).

## <a name="3-send-data-acquisition-events-using-javascript"></a>3. Wysyłanie zdarzeń danych przy użyciu języka JavaScript
Witaj następujące kroki ułatwiają wysyłanie zdarzeń:

1. Uwzględnij biblioteki JQuery w kodzie. Można go pobrać z nuget w hello następującego adresu URL.
   
     http://www.nuget.org/Packages/jQuery/1.8.2
2. Zawierają hello skryptów Java zalecenia biblioteki z następującego adresu URL hello: http://aka.ms/RecoJSLib1
3. Zainicjowanie biblioteki Azure ML zalecenia z odpowiednimi parametrami hello.
   
     <script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Odpowiednie zdarzenie hello wysyłania. Zobacz poniższą sekcję szczegółowe na wszystkich typów zdarzeń (Zdarzenie kliknięcia przykład) <script> Jeśli (typeof AzureMLRecommendationsEvent == "undefined") {         
                     AzureMLRecommendationsEvent =] } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script>

### <a name="31----limitations-and-browser-support"></a>3.1.    Ograniczenia i obsługa przeglądarek
Jest to implementacja odwołania i jest on podawany jest. Należy go obsługuje wszystkie główne przeglądarki.

### <a name="32----type-of-events"></a>3.2.    Typ zdarzenia
Istnieje 5 typy zdarzeń, które obsługuje biblioteki hello: kliknij pozycję zalecenie, Dodaj tooShop koszyka, Usuń z koszyka produkcyjny i zakupu. Brak dodatkowych zdarzenie kontekstu użytkownika hello używane tooset o nazwie logowania.

#### <a name="321-click-event"></a>3.2.1. Zdarzenie kliknięcia
To zdarzenie powinny być używane w dowolnym momencie, a użytkownik kliknął element. Zwykle, gdy użytkownik kliknie element Nowa strona zostanie otwarty z szczegóły elementu hello; na tej stronie to zdarzenie jest wyzwalane.

Parametry:

* zdarzenia (ciąg, obowiązkowe) "kliknij"
* Unikatowy identyfikator elementu hello (ciąg, obowiązkowe) — element
* Nazwa elementu (ciąg, opcjonalnie) nazwa hello elementu hello
* itemDescription (ciąg, opcjonalny) hello opis elementu hello
* itemCategory (ciąg, opcjonalny) kategorii hello hello elementu
  
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
To zdarzenie powinny być używane w dowolnym momencie, a użytkownik kliknął element otrzymanego od zaleceń uczenia Maszynowego Azure jako element zalecane. Zwykle, gdy użytkownik kliknie element Nowa strona zostanie otwarty z szczegóły elementu hello; na tej stronie to zdarzenie jest wyzwalane.

Parametry:

* zdarzenia (ciąg, obowiązkowe) "recommendationclick"
* Unikatowy identyfikator elementu hello (ciąg, obowiązkowe) — element
* Nazwa elementu (ciąg, opcjonalnie) nazwa hello elementu hello
* itemDescription (ciąg, opcjonalny) hello opis elementu hello
* itemCategory (ciąg, opcjonalny) kategorii hello hello elementu
* ziarna (tablicy ciągów, opcjonalny) — Witaj ziarna wygenerowanych hello zalecenie zapytania.
* recoList (tablicy ciągów, opcjonalny) — Witaj wynik żądania zalecenie hello, generowany hello elementu, który został kliknięty.
  
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
To zdarzenie powinna być używana podczas użytkownika hello dodać toohello elementu koszyka.
Parametry:

* zdarzenia (ciąg, obowiązkowe) "addshopcart"
* Unikatowy identyfikator elementu hello (ciąg, obowiązkowe) — element
* Nazwa elementu (ciąg, opcjonalnie) nazwa hello elementu hello
* itemDescription (ciąg, opcjonalny) hello opis elementu hello
* itemCategory (ciąg, opcjonalny) kategorii hello hello elementu
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a>3.2.4. Usuń zdarzenia z koszyka zakupów
To zdarzenie powinien być używany, gdy użytkownik hello usuwa element toohello koszyk.

Parametry:

* zdarzenia (ciąg, obowiązkowe) "removeshopcart"
* Unikatowy identyfikator elementu hello (ciąg, obowiązkowe) — element
* Nazwa elementu (ciąg, opcjonalnie) nazwa hello elementu hello
* itemDescription (ciąg, opcjonalny) hello opis elementu hello
* itemCategory (ciąg, opcjonalny) kategorii hello hello elementu
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a>3.2.5. Zdarzenie zakupu
To zdarzenie powinien być używany, gdy użytkownik hello kupił jego koszyk.

Parametry:

* zdarzenia (ciąg) "Kup"
* elementy (zakupione []) - zawierający wpis dla każdego elementu zakupionych tablicy.<br><br>
  Format zakupionych:
  * element (string) — Unikatowy identyfikator elementu hello.
  * Liczba (int lub string) — liczba elementów, które zostały zakupione.
  * Cena (float lub string) — pole opcjonalne — hello cena elementu hello.

przykład Witaj poniżej przedstawia zakupu 3 elementy (33, 34, 35), dwa wszystkich pól (element, count, cena) oraz jedną (element 34) bez ceny.

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a>3.2.6. Zdarzenia logowania użytkownika
Azure zdarzeń zalecenia dotyczące uczenia Maszynowego tworzy biblioteki i używanie plików cookie w kolejności tooidentify zdarzenia, które nadeszły z hello tę samą przeglądarkę. W modelu hello tooimprove kolejność wyników Azure ML zalecenia umożliwia tooset Unikatowy identyfikator użytkownika, który zastąpi hello użycia plików cookie.

To zdarzenie powinny być używane po hello użytkownika logowania tooyour lokacji.

Parametry:

* zdarzenia (ciąg) "userlogin"
* Użytkownik (string) — Unikatowy identyfikator hello użytkownika.
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a>4. Korzystanie z zalecenia za pośrednictwem kodu JavaScript
Hello kod, który zużywa zalecenie hello jest wyzwalany przez zdarzenie JavaScript przez powitania klienta strony sieci Web. odpowiedź zalecenie Hello zawiera hello zalecane identyfikatory elementów, ich nazwy i ich klasyfikacji. Jest najlepszym toouse, który tę opcję tylko w przypadku wyświetlania listy hello zalecane elementów - bardziej złożonej obsługi (takie jak dodanie metadanych elementu hello) ma się odbywać na powitania serwera po stronie integracji.

### <a name="41-consume-recommendations"></a>4.1 korzystać zalecenia
zalecenia tooconsume potrzebne tooinclude hello wymaganych bibliotek JavaScript na stronie i w toocall AzureMLRecommendationsStart. W sekcji 2.

tooconsume zalecenia dla jednego lub więcej elementów należy wywołać metodę toocall: AzureMLRecommendationsGetI2IRecommendation.

Parametry:

* elementy jeden lub więcej elementów tooget zalecenia dotyczące (Tablica ciągów -). Jeśli zostaną zużyte na kompilację zmianie wysokości progów, można ustawić tutaj tylko jeden element.
* numberOfResults (int) - liczba wymaganych wyników.
* includeMetadata (wartość logiczna, opcjonalny) — Jeśli ustawić too'true "wskazuje tego pola metadanych hello powinno zostać zapełnione w wyniku hello.
* Funkcja przetwarzania — funkcja, która będzie obsługiwać zalecenia hello zwracane. Witaj, dane są zwracane jako tablica:
  * Identyfikator unikatowy element — element
  * Nazwa — Nazwa elementu (jeśli istnieje w katalogu)
  * Ocena — zaleceniem klasyfikacji
  * metadane — ciąg reprezentujący hello metadanych elementu hello

Przykład: hello następującego kodu żądań 8 zalecenia dla elementu "64f6eb0d-947a-4c18-a16c-888da9e228ba" (bez określania includeMetadata - niejawnie wskazanego czy metadanych nie jest wymagane), następnie połącz hello wyniki do buforu.

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
