---
ms.assetid: 
title: "aaaAzure wskazówki dotyczące ograniczania przepustowości usługi Key Vault | Dokumentacja firmy Microsoft"
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a>Usługa Azure Key Vault ograniczania wskazówki

Ograniczanie jest procesem zainicjowanych przez ogranicza liczbę hello nadmierne zużycie tooprevent usługi Azure toohello równoczesnych wywołań zasobów. Magazyn kluczy Azure (AKV) jest zaprojektowana toohandle dużą liczbę żądań. W przypadku utrudnione liczba żądań ograniczanie żądań klienta pomaga utrzymać optymalną wydajność i niezawodność hello AKV usługi.

Limity ograniczania przepustowości różnić w zależności od scenariusza hello. Na przykład jeśli przeprowadzasz dużą liczbę operacji zapisu, ograniczanie możliwości hello jest wyższa niż jeśli tylko wykonywana odczyty.

## <a name="how-does-key-vault-handle-its-limits"></a>Jak usługi Key Vault obsługuje limit?

Ograniczenia usługi Key Vault istnieją tooprevent nieprawidłowe użycie zasobów i zapewnienia jakości usług dla wszystkich klientów usługi Key Vault. Po przekroczeniu progu usługi Key Vault ogranicza żadnych dalszych żądań z tego klienta w danym okresie czasu. W takim przypadku magazyn kluczy zwraca kod stanu HTTP 429 (zbyt wiele żądań), oraz hello żądania kończyć się niepowodzeniem. Ponadto nie żądań zwracających 429 liczba kierunku limity przepustowości hello śledzone przez magazyn kluczy. 

Jeśli masz prawidłowe firm przypadku wyższe limity przepustowości, skontaktuj się z nami.


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a>Jak toothrottle aplikacji w odpowiedzi tooservice ogranicza

Witaj poniżej przedstawiono **najlepsze rozwiązania** dla ograniczania aplikacji:
- Ogranicz liczbę hello operacji na żądanie.
- Zmniejsz częstotliwość hello żądań.
- Należy unikać bezpośredniego ponownych prób. 
    - Wszystkie żądania są naliczane względem limitów do użycia.

Podczas implementowania obsługi błędów aplikacji, użyj hello HTTP Błąd kodu 429 toodetect hello potrzebę ograniczania po stronie klienta. Jeśli Żądanie hello nie powiedzie się ponownie z kodem błędu HTTP 429, pojawiły się nadal limit usług Azure. Kontynuować toouse hello zalecana metoda ograniczania przepustowości po stronie klienta, ponawianie próby hello żądania do skutku.

### <a name="recommended-client-side-throttling-method"></a>Zalecana metoda ograniczania przepustowości po stronie klienta

Na kod błędu HTTP 429 Rozpocznij ograniczanie klienta przy użyciu podejścia wykładniczego wycofywania:

1. Poczekaj 1 sekundę, ponów próbę wykonania żądania
2. Jeśli nadal ograniczany poczekaj 2 sekundy, ponów próbę wykonania żądania
3. Jeśli nadal ograniczany oczekiwania 4 sekundy, ponów próbę wykonania żądania
4. Jeśli nadal ograniczany oczekiwania 8 sekund, ponów próbę wykonania żądania
5. Jeśli nadal ograniczany oczekiwania w sekundach 16, ponów próbę wykonania żądania

W tym momencie możesz powinien nie uzyskać kody odpowiedzi HTTP 429.

## <a name="see-also"></a>Zobacz też

Uzyskać lepszy orientacji ograniczania przepustowości na powitania Microsoft Cloud, zobacz [ograniczania wzorzec](https://docs.microsoft.com/azure/architecture/patterns/throttling).

