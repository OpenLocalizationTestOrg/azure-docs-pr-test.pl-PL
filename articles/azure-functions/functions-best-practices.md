---
title: "aaaBest wskazówki dotyczące usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Dowiedz się najlepsze rozwiązania i wzorce dla usługi Azure Functions."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "środowisko Azure functions, wzorce, najlepszym rozwiązaniem, funkcji, przetwarzania elementów webhook, dynamiczne obliczeń, architektura niekorzystającą zdarzeń"
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a>Optymalizacja hello wydajności i niezawodności usługi Azure Functions

Ten artykuł zawiera wskazówki dotyczące tooimprove hello wydajności i niezawodności aplikacji funkcji. 


## <a name="avoid-long-running-functions"></a>Unikaj długotrwałe funkcji

Funkcje dużych, długotrwałą mogą powodować problemy nieoczekiwany limitu czasu. Funkcja może stać się duża powodu toomany Node.js zależności. Importowanie zależności mogą powodować zwiększone obciążenie uruchomień spowodować nieoczekiwane przekroczeń limitu czasu. Zależności są ładowane zarówno jawnie i niejawnie. Moduł pojedynczego załadowane przez kod może załadować własną dodatkowych modułów.  

Jeśli to możliwe, zrefaktoryzuj długie funkcje na mniejsze funkcja ustawia które współpracują ze sobą i szybko powrócić odpowiedzi. Na przykład elementu webhook lub funkcja wyzwalacza HTTP może wymagać potwierdzenia odpowiedzi w określonym terminie. bardzo często toorequire elementów webhook natychmiastowej reakcji. Ładunek wyzwalacza HTTP hello można przekazać do toobe kolejki, przetwarzane przez funkcję wyzwalacza kolejki. Takie podejście pozwala toodefer hello rzeczywistą pracę i zwracać natychmiastowej reakcji.


## <a name="cross-function-communication"></a>Funkcja komunikacji między

Integrowanie wiele funkcji, jest zazwyczaj najlepsze praktyki toouse kolejek magazynu dla wielu funkcji komunikacji.  Witaj główną przyczyną jest kolejki magazynu są tańsze i znacznie łatwiejsze tooprovision. 

Poszczególne wiadomości w kolejce magazynu jest ograniczona too64 rozmiar KB. Toopass większych wiadomości między funkcji, należy kolejki usługi Azure Service Bus można rozmiary wiadomości używanych toosupport się too256 KB.

Tematy usługi Service Bus są przydatne, jeśli potrzebujesz filtrowania przed rozpoczęciem przetwarzania komunikatu.

Centra zdarzeń są przydatne toosupport dużą komunikacji.


## <a name="write-functions-toobe-stateless"></a>Pisanie funkcji toobe bezstanowych 

Funkcje powinny być bezstanowych i idempotentności, jeśli to możliwe. Kojarzenie żadnych informacji o stanie wymagane z danymi. Na przykład kolejność przetwarzania prawdopodobnie byłyby skojarzony `state` elementu członkowskiego. Funkcja może przetworzyć zamówienia na podstawie tego stanu funkcja hello pozostaje bezstanowe. 

Funkcje idempotentności są szczególnie zalecane z wyzwalaczy czasomierza. Na przykład jeśli coś, co należy bezwzględnie uruchom raz dziennie, Zapisz, można je uruchomić czasie hello dnia z hello takie same wyniki. Funkcja Hello można zamknąć po żadnej pracy dla danego dnia. Także jeśli poprzedniego uruchomienia nie powiodła się toocomplete, hello kolejnego uruchomienia powinien wybierz miejsca, w którym.


## <a name="write-defensive-functions"></a>Pisanie funkcji obrony

Załóżmy, że funkcja może wystąpić wyjątek w dowolnym momencie. Projektowanie funkcje za pomocą toocontinue możliwości powitania od poprzedniego punktu kończyć się niepowodzeniem podczas wykonywania dalej hello. Rozważ scenariusz, który wymaga hello następujące akcje:

1. Zapytanie o 10 000 wierszy w bazie danych.
2. Tworzenie komunikatu w kolejce dla każdego tooprocess tych wierszy do dalszego w hello wiersz w dół.
 
W zależności od tego, jak złożoność system jest, może być: zachowuje nieprawidłowo zaangażowany usługami podrzędnymi, awarii sieci lub limit przydziału ogranicza osiągnęło itp. Wszystkie te mogą wpływać na funkcji w dowolnym momencie. Należy toodesign Twojego toobe funkcje przygotowany dla niego.

Jak kodu reagować, jeśli wystąpi błąd po wstawieniu 5000 tych elementów w kolejce do przetworzenia? Śledzenie elementów w zestawie, które zostały zakończone. W przeciwnym razie możesz wstawić je ponownie po następnym. Może to mieć poważny wpływ na Twoje przepływu pracy. 

Jeśli element kolejki został już przetworzony, Zezwalaj toobe Twojego funkcja zerowa.

Skorzystaj z środków obrony już dostarczona dla składników, używanych na platformie Azure Functions hello. Na przykład, zobacz **obsługi wiadomości w kolejce skażone** w dokumentacji hello [wyzwala kolejki magazynu Azure](functions-bindings-storage-queue.md#trigger).
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a>Nie testu mieszanego i produkcji kod hello sama aplikacja — funkcja

Funkcje w obrębie aplikacji funkcji udostępniania zasobów. Na przykład pamięci jest udostępniony. Jeśli używasz aplikacji funkcji w środowisku produkcyjnym, nie dodawaj funkcji związanych z testu i tooit zasobów. Może spowodować nieoczekiwane obciążenie podczas wykonywania kodu produkcyjnego.

Należy zachować ostrożność ładowanie w aplikacjach funkcji produkcji. Pamięć jest uśredniana dla każdej funkcji aplikacji hello.

Jeśli masz współużytkowanego zespołu, do którego odwołuje się wiele funkcji .net, umieść ją w typowych folderu udostępnionego. Odwołanie do zestawu hello z instrukcji toohello podobne, poniższy przykład: 

    #r "..\Shared\MyAssembly.dll". 

W przeciwnym razie jest łatwe tooaccidentally wdrażania wielu wersji testu hello tego samego pliku binarnego, które zachowują się inaczej między funkcji.

Nie używaj pełnego rejestrowania w kodzie produkcyjnym. Ma ona negatywny wpływ na wydajność.



## <a name="use-async-code-but-avoid-blocking-calls"></a>Użyj kodu asynchroniczne, ale unikania blokowania połączeń

Programowanie asynchroniczne jest zalecanym najlepszym rozwiązaniem. Jednak zawsze uniknąć odwołujące się do hello `Result` właściwość lub wywołanie `Wait` metoda `Task` wystąpienia. Takie podejście może spowodować wyczerpanie toothread.


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji zobacz następujące zasoby hello:

Ponieważ usługi Azure Functions używa usługi Azure App Service, należy wziąć pod uwagę wskazówki dotyczące usługi aplikacji.
* [Wzorce i praktyki optymalizacji wydajności HTTP](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

