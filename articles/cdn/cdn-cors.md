---
title: aaaUsing Azure CDN z CORS | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello Azure sieci dostarczania zawartości (CDN) toowith udostępniania zasobów między źródłami (CORS)."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a>Przy użyciu usługi Azure CDN z CORS
## <a name="what-is-cors"></a>Co to jest CORS?
CORS (Cross źródła Resource Sharing) to funkcja HTTP, która umożliwia aplikacja sieci web w jednej domenie tooaccess zasobów w innej domenie. W kolejności tooreduce hello możliwości ataków skryptów między witrynami, wszystkie nowoczesne przeglądarki zaimplementować ograniczenia zabezpieczeń znany jako [zasad samego pochodzenia](http://www.w3.org/Security/wiki/Same_Origin_Policy).  Zapobiega to strony sieci web na podstawie wywoływania interfejsów API w innej domenie.  Mechanizm CORS zapewnia bezpieczny sposób tooallow jedno źródło (hello domeny pochodzenia) toocall interfejsów API w innego źródła.

## <a name="how-it-works"></a>Jak to działa
Istnieją dwa typy żądań CORPS *prostych żądań* i *złożonych żądań.*

### <a name="for-simple-requests"></a>Proste żądań:

1. Przeglądarka Hello wysyła żądanie CORS hello z dodatkowymi **pochodzenia** nagłówek żądania HTTP. wartość Hello tego nagłówka jest pochodzenia hello, który obsłużył Strona nadrzędna hello, która jest zdefiniowana jako kombinacja hello *protokołu,* *domeny,* i *portu.*  Jeśli strony z https://www.contoso.com próbuje tooaccess danych użytkownika w hello fabrikam.com pochodzenia, powitania po nagłówek żądania wysłania toofabrikam.com:

   `Origin: https://www.contoso.com`

2. Serwer Hello mogą odpowiadać za pomocą dowolnego z następujących hello:

   * **Access-Control-Allow-Origin** nagłówka w swojej odpowiedzi wskazujący lokacji pochodzenia, do której jest dozwolona. Na przykład:

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * Błąd HTTP code takich jak 403, jeśli powitania serwera nie zezwala na żądania cross-origin hello po sprawdzeniu hello źródła nagłówka

   * **Access-Control-Allow-Origin** nagłówka z symbolem wieloznacznym, który zezwala na wszystkie pochodzenia:

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a>Złożonych żądań:

Złożonych żądanie jest żądaniem CORS, w których przeglądarka hello jest wymagane toosend *żądania wstępnego* (tj. wstępne badanie) przed wysłaniem hello rzeczywiste żądanie CORS. Hello żądania wstępnego żąda uprawnienia serwera hello czy hello oryginalne żądanie CORS można kontynuować i jest `OPTIONS` żądania toohello tego samego adresu URL.

> [!TIP]
> Więcej szczegółów na przepływów mechanizmu CORS i typowych problemów, należy wyświetlić hello [przewodniku tooCORS interfejsów API REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).
>
>

## <a name="wildcard-or-single-origin-scenarios"></a>Symbol wieloznaczny lub scenariuszy pojedynczego źródła
CORS w sieci CDN w warstwie Azure będą działać automatycznie bez konieczności dodatkowej konfiguracji, gdy hello **Access-Control-Allow-Origin** ustawiono nagłówka toowildcard (*) lub jednego źródła.  Hello CDN będą buforowane hello pierwszej odpowiedzi i kolejne żądania użyje hello tego samego nagłówka.

Jeśli żądań zostały już wprowadzone toohello CDN tooCORS wcześniejszego ustawiania hello źródła, konieczne będzie toopurge zawartości na powitania tooreload zawartości z punktu końcowego zawartości z hello **Access-Control-Allow-Origin** nagłówka.

## <a name="multiple-origin-scenarios"></a>Wiele scenariuszy źródła
Tooallow do określonej listy źródeł toobe dozwolone dla mechanizmu CORS należy rzeczy Pobierz nieco bardziej skomplikowane. Witaj problem występuje, gdy hello CDN buforuje hello **Access-Control-Allow-Origin** nagłówek hello pierwsze źródło CORS.  Gdy inny źródło CORS sprawia, że kolejne żądania, hello CDN posłuży hello buforowane **Access-Control-Allow-Origin** nagłówek, który nie odpowiada.  Istnieje kilka sposobów toocorrect to.

### <a name="azure-cdn-premium-from-verizon"></a>Usługa Azure CDN w warstwie Premium firmy Verizon
Najlepszym sposobem tooenable Hello jest toouse **Azure CDN Premium from Verizon**, który ujawnia niektóre zaawansowane funkcje. 

Będziesz potrzebować zbyt[utworzyć regułę](cdn-rules-engine.md) toocheck hello **pochodzenia** nagłówka w żądaniu hello.  Jeśli istnieje prawidłowy punkt początkowy reguły ustawi hello **Access-Control-Allow-Origin** nagłówek z pochodzenia hello podany w żądaniu hello.  Jeśli określono pochodzenia hello hello **pochodzenia** nagłówka nie jest dozwolona, reguła musi pominąć hello **Access-Control-Allow-Origin** nagłówka, co spowoduje hello przeglądarki tooreject hello żądania. 

Istnieją dwa sposoby toodo to hello aparatu reguł.  W obu przypadkach hello **Access-Control-Allow-Origin** nagłówka z serwera pochodzenia pliku hello całkowicie jest ignorowany, aparat reguł hello CDN w pełni zarządza hello dozwolone źródła CORS.

#### <a name="one-regular-expression-with-all-valid-origins"></a>Jednego wyrażenia regularnego z wszystkie prawidłowe źródła
W takim przypadku utworzysz wyrażenie regularne, które zawiera wszystkie źródła hello ma tooallow: 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> **Usługi Azure CDN from Verizon** używa [zgodne wyrażeń regularnych języka Perl](http://pcre.org/) jako jego aparat wyrażeń regularnych.  Można użyć narzędzia, takiego jak [101 wyrażeń regularnych](https://regex101.com/) toovalidate wyrażenie regularnego.  Należy pamiętać, że Witaj "/" znak jest nieprawidłowe w wyrażeniach regularnych i nie wymaga toobe wyjściowym, jednak anulowanie ten znak jest traktowane jako najlepsze rozwiązanie i jest oczekiwane przez niektóre moduły weryfikacji wyrażenia regularnego.
> 
> 

Jeśli pasuje do wyrażenia regularnego hello, reguły zastąpi hello **Access-Control-Allow-Origin** nagłówka (jeśli istnieją) z hello źródła z pochodzenia hello, który wysłał żądanie hello.  Możesz także dodać dodatkowe nagłówki CORS, takich jak **dostępu-formant-Allow-Methods**.

![Przykład reguły z wyrażeniem regularnym](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a>Reguła nagłówka żądania dla każdego źródła.
Zamiast wyrażeń regularnych, możesz zamiast tego utworzyć oddzielne reguły dla każdego źródła mają tooallow przy użyciu hello **wieloznaczny nagłówka żądania** [dopasować stan](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1). Jako przy użyciu metody wyrażenia regularnego hello reguły hello aparat samodzielnie ustawia nagłówki CORS hello. 

![Przykład reguły bez wyrażeń regularnych](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> W powyższym przykładzie hello, hello Użyj hello wieloznaczny * informuje reguły hello aparat toomatch protokołów HTTP i HTTPS.
> 
> 

### <a name="azure-cdn-standard"></a>Usługi Azure CDN Standard
Na platformie Azure CDN Standard profile hello tylko tooallow mechanizm dla wielu źródeł bez użycia hello pochodzenia symbolu wieloznacznego hello jest toouse [buforowanie ciągu zapytania](cdn-query-string.md).  Ustawienie parametrów zapytania tooenable dla punktu końcowego CDN hello a następnie za pomocą ciąg zapytania unikatowy dla żądań z każdej domeny, dozwolone. W ten sposób spowoduje hello CDN buforowanie oddzielny obiekt dla każdego ciągu zapytania unikatowy. Ta metoda nie jest idealnym rozwiązaniem, jednak zgodnie z spowoduje utworzenie wielu kopii hello tego samego pliku pamięci podręcznej na powitania CDN.  

