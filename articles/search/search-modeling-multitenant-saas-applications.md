---
title: "aaaModeling Wielodostępności w usłudze Azure Search | Dokumentacja firmy Microsoft"
description: "Poznaj typowe wzorce projektowe dla wielodostępnych aplikacji SaaS przy użyciu usługi Azure Search."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 72e9696a-553b-47dc-9e05-a82db0ebf094
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/26/2016
ms.author: ashmaka
ms.openlocfilehash: dd46cda772d32566b9aaa18d407f12fdf178bd43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="design-patterns-for-multitenant-saas-applications-and-azure-search"></a>Projektowanie wzorce dla wielodostępnych aplikacji SaaS i usługi Azure Search
Wielodostępna aplikacji to taki, który udostępnia hello tej samej usługi i możliwości tooany liczby dzierżawców, którzy nie można wyświetlić dane lub udostępniać hello z innymi dzierżawami. W tym dokumencie omówiono strategii izolacji dzierżawy dla wielodostępnych aplikacji skompilowanej za pomocą usługi Azure Search.

## <a name="azure-search-concepts"></a>Pojęcia wyszukiwanie Azure
Jako rozwiązaniem wyszukiwanie jako usługa Azure Search umożliwia deweloperom tooadd sformatowanego wyszukiwania napotka tooapplications bez dowolnej infrastruktury zarządzania i staje się eksperta w wyszukiwaniu. Dane są przekazywane toohello usługi i następnie przechowywane w chmurze hello. Przy użyciu prostych żądań toohello interfejsu API usługi Azure Search, dane hello następnie można modyfikować i przeszukiwane. Omówienie usługi hello znajdują się w [w tym artykule](http://aka.ms/whatisazsearch). Przed omówieniem wzorce projektowe, jest ważne toounderstand niektóre pojęcia dotyczące usługi Azure Search.

### <a name="search-services-indexes-fields-and-documents"></a>Wyszukiwanie w usługach, indeksów, pól i dokumentów
Podczas korzystania z usługi Azure Search, jeden subskrybuje tooa *usługi wyszukiwania*. Ponieważ dane są przekazane tooAzure wyszukiwania, jest ona przechowywana w *indeksu* w ramach hello usługi wyszukiwania. Może to być liczba indeksów w ramach jednej usługi. toouse hello znane pojęcia baz danych usługi wyszukiwania hello można przyrównać tooa bazy danych indeksów hello w ramach usługi mogą być przyrównać tootables w bazie danych.

Każdy indeks w ramach usługi wyszukiwania ma własny schemat, który jest zdefiniowany przez liczbę można dostosowywać *pola*. Dodanie indeksu usługi Azure Search tooan danych w formie hello indywidualnego *dokumenty*. Każdy dokument musi być przekazana tooa określonego indeksu i musi znajdować się w tym Indeksuj schemat. Podczas wyszukiwania danych przy użyciu usługi Azure Search, zapytania wyszukiwania pełnotekstowego hello są wystawiony na podstawie określonego indeksu.  toocompare te pojęcia toothose bazy danych, pola można przyrównać toocolumns w tabeli, a także dokumenty mogą być przyrównać toorows.

### <a name="scalability"></a>Skalowalność
Wszystkie usługi Azure Search w hello Standard [warstwy cenowej](https://azure.microsoft.com/pricing/details/search/) można skalować w dwóch wymiarów: magazynu i dostępności.

* *Partycje* można dodać tooincrease hello magazynu usługi wyszukiwania.
* *Repliki* można dodać tooa usługi tooincrease hello przepływności żądań, jaką może obsłużyć usługi wyszukiwania.

Dodawanie i usuwanie partycji i replik w umożliwi hello pojemność toogrow usługi wyszukiwania hello z hello ilość danych i ruchu hello przez aplikację. W celu dla tooachieve usługi wyszukiwania odczytu [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), wymaga dwóch replik. W celu dla tooachieve usługi odczytu i zapisu [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), wymaga trzech replik.

### <a name="service-and-index-limits-in-azure-search"></a>Limity usług i indeksu w usłudze Azure Search
Istnieje kilka różnych [warstw cenowych](https://azure.microsoft.com/pricing/details/search/) w usłudze Azure Search, każdy z warstw hello ma inną [limity i przydziały](search-limits-quotas-capacity.md). Niektóre z tych limitów są na powitania poziomu usług, niektóre są na poziomie indeksu hello i niektóre są na poziomie partycji hello.

|  | Podstawowa | Standard1 | Standard2 | Standard3 | Standard3 HD |
| --- | --- | --- | --- | --- | --- |
| Maksymalna replik dla usługi |3 |12 |12 |12 |12 |
| Maksymalna partycji dla usługi |1 |12 |12 |12 |1 |
| Jednostek wyszukiwania maksymalną (replik * partycje) dla usługi |3 |36 |36 |36 |36 (max partycji 3) |
| Maksymalna dokumentów dla usługi |1 mln |180 milionów |720 milionów |1.4 mld |600 mln |
| Maksymalna przestrzeń magazynowa dla usługi |2 GB |300 GB |1,2 TB |2,4 TB |600 GB |
| Maksymalna dokumentów na partycję |1 mln |15 milionów |60 milionów |120 milionów |200 milionów |
| Maksymalna przestrzeń magazynowa dla każdej partycji |2 GB |25 GB |100 GB |200 GB |200 GB |
| Maksymalna indeksów dla usługi |5 |50 |200 |200 |3000 (max 1000 indeksów/partycji) |

#### <a name="s3-high-density"></a>S3 o wysokiej gęstości "
W usłudze Azure Search S3 warstwę cenową istnieje opcja trybu wysokiej gęstości (HD) hello zaprojektowane specjalnie dla scenariuszy wielodostępnym. W wielu przypadkach jest konieczne toosupport dużą liczbą mniejszą dzierżaw w jednej usługi tooachieve hello zalet prostotę i koszt wydajności.

S3 HD umożliwia hello wiele indeksów małych toobe pakowane w obszarze Zarządzanie hello usługi wyszukiwania pojedynczego przez handlowymi tooscale możliwości hello limit indeksów przy partycje toohost możliwości hello więcej indeksów w jednej usługi.

Konkretnie usługa S3 może mieć od 1 do 200 indeksów, które razem może udostępniać too1.4 miliarda dokumentów. HD S3 hello drugiej umożliwiałyby tooonly poszczególnych indeksów Przejdź too1 milionów dokumentów, ale może obsłużyć się too1000 indeksów dla partycji (w górę too3000 poszczególnych usług) wraz z liczbą całkowitą dokumentu 200 milionów dla każdej partycji (się too600 milionów usługi).

## <a name="considerations-for-multitenant-applications"></a>Zagadnienia dotyczące aplikacji wielodostępnego
Aplikacje wielodostępne musi efektywnie dystrybuuje zasobów między dzierżawcami hello przy zachowaniu pewnego poziomu prywatności między hello różnych dzierżaw. Istnieje kilka zagadnień podczas projektowania architektury powitania dla takich aplikacji:

* *Odizolowania dzierżawców:* deweloperzy aplikacji muszą tootake odpowiednie środki tooensure czy dzierżawcy nie mają nieautoryzowane lub niechcianego dostępu do danych toohello innych dzierżawców. Poza perspektywy hello prywatność danych strategii izolacji dzierżawcy wymagają efektywne zarządzanie udostępnionymi zasobami oraz ochrony przed zakłócenia sąsiadów.
* *Koszt zasobów w chmurze:* zgodnie z innej aplikacji, rozwiązania w zakresie oprogramowania muszą pozostać koszt konkurencyjnych jako składnik wielodostępnych aplikacji.
* *Łatwość operacji:* podczas opracowywania architektura wielodostępnej, hello wpływ na operacje aplikacji hello i ważną kwestią jest złożoności. Usługa wyszukiwanie Azure ma [SLA 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
* *Globalne zużycie:* wielodostępnych aplikacji może być konieczne tooeffectively służą dzierżawcami, które są rozproszone na Witaj świecie.
* *Skalowalność:* deweloperzy aplikacji muszą tooconsider jak uzgodnienia między utrzymanie wystarczająco niski poziom złożoności aplikacji i projektowania tooscale aplikacji hello z liczby dzierżawców i hello rozmiar danych dzierżawców i Obciążenie pracą.

Usługa Azure Search udostępnia kilka granice, które mogą być dzierżaw tooisolate używanych danych i obciążenia.

## <a name="modeling-multitenancy-with-azure-search"></a>Obsługa wielu podmiotów modelowania z usługi Azure Search
W przypadku hello scenariusza wielodostępnym Deweloper aplikacji hello zużywa co najmniej jednej usługi wyszukiwania i dzielenia dzierżawcom między usługi i/lub indeksy. Usługa wyszukiwanie Azure ma kilka typowych wzorców podczas modelowania wielodostępnym scenariusza:

1. *Indeks dla poszczególnych dzierżawców:* każdy dzierżawca ma własnych indeksu w usłudze wyszukiwania, która jest współdzielony z innymi dzierżawcami.
2. *Usługi dla poszczególnych dzierżawców:* poszczególne dzierżawy zawierają własne dedykowane usługi Azure Search oferty najwyższy poziom separacji danych i jego obciążenie.
3. *Kombinacja obu:* większych i bardziej aktywny dzierżawcy przypisano dedykowanych usług podczas mniejszych dzierżaw są przypisane poszczególnych indeksy w ramach usług udostępnionych.

## <a name="1-index-per-tenant"></a>1. Indeks dla każdego dzierżawcy
![Wizerunku hello indeksu na dzierżawy modelu](./media/search-modeling-multitenant-saas-applications/azure-search-index-per-tenant.png)

W modelu indeksu na dzierżawy wielu dzierżawców zajmują jednej usługi Azure Search gdzie każdy dzierżawca ma własnych indeksu.

Dzierżawcy osiągnąć izolacji danych, ponieważ wszystkie żądania wyszukiwania, a operacje dokumentu są wydawane na poziomie indeksu w usłudze Azure Search. W warstwie aplikacji hello Brak świadomości potrzeby hello toodirect hello różnych dzierżaw ruchu toohello odpowiednie indeksy podczas również zarządzanie zasobami na poziomie usługi hello wszystkich dzierżawców.

Atrybutu klucza w modelu indeksu na dzierżawy hello jest zdolność hello pojemności dewelopera aplikacji hello hello toooversubscribe między aplikacji hello dzierżaw usługi wyszukiwania. Jeśli hello dzierżawy mają nierówny rozkład obciążenia, hello optymalnego połączenia dzierżawcy mogą być rozproszone na usługi wyszukiwania indeksowania tooaccommodate liczba wysokiej dzierżaw aktywnych, użyciem zasobów jednocześnie służąc długi koniec mniej aktywne dzierżawcy. rozwiązanie Hello jest brakiem hello hello modelu toohandle sytuacje, w której poszczególne dzierżawy jest jednocześnie wysokiej aktywna.

model indeksu na dzierżawy Hello stanowi podstawę hello modelu koszt zmiennej, gdzie są kupowane ponoszonych z góry całej usługi Azure Search, a następnie wypełnione z dzierżawcami. Dzięki temu wyznaczony prób i konta bezpłatne toobe nieużywane miejsce.

Dla aplikacji z globalnego wpływ hello indeksu na dzierżawy modelu nie może być najbardziej efektywne hello. Jeśli dzierżawcy aplikacji są rozproszone na Witaj świecie, oddzielne usługi może być konieczne dla każdego regionu, w którym mogą Zduplikuj kosztów na każdej z nich.

Usługa wyszukiwanie Azure umożliwia skali hello hello poszczególnych indeksy i hello łączna liczba indeksów toogrow. Jeśli odpowiednie ceny warstwy wybrano, partycji i replik można dodać toohello całego wyszukiwania usługi podczas konkretnego indeksu w usłudze hello zbytnio się rozrośnie pod względem ruchu lub magazynu.

Jeśli łączna liczba indeksów hello zbytnio się rozrośnie dla jednej usługi, innej usługi ma tooaccommodate toobe elastycznie hello nowi dzierżawcy. Jeśli indeksy toobe przenosić między usługi wyszukiwania w miarę dodawania nowych usług, danych powitania od indeksu hello ma toobe ręcznie skopiowane z jednego indeksu toohello innych zgodnie z usługi Azure Search nie zezwala na toobe indeksu przeniesiony.

## <a name="2-service-per-tenant"></a>2. Usługi dla poszczególnych dzierżawców
![Wizerunku hello modelu usług dla dzierżawców](./media/search-modeling-multitenant-saas-applications/azure-search-service-per-tenant.png)

W architekturze usługi na dzierżawy każdy dzierżawca ma własną usługę wyszukiwania.

W tym modelu aplikacji hello osiąga hello maksymalny poziom izolacji dla swoich dzierżaw. Każda usługa ma dedykowany Magazyn oraz przepustowość do obsługi żądania wyszukiwania, a także osobne klucze interfejsu API.

Dla aplikacji, w której poszczególne dzierżawy zawierają duże zużycie lub hello obciążenie ma mało zmienności z tootenant dzierżawy modelu usług dla dzierżawy hello jest rzeczywistą możliwość wyboru zasobów nie są współdzielone przez różnych dzierżaw obciążeń.

Usługa na modelu dzierżawy oferuje również korzyści hello modelu koszt przewidywalne, stały. Nie jest brak początkowych inwestycji w usłudze całego wyszukiwania do momentu toofill dzierżawy, jednak hello koszt na dzierżawy jest wyższy niż model indeksu dla dzierżawy.

model usługi dla dzierżawy Hello jest wydajne wybór dla aplikacji z globalnego zużycie. Dzierżawcom rozproszonej geograficznie, usługa ta jest łatwe toohave każdego dzierżawcy w hello odpowiedniego regionu.

wyzwania Hello skalowania tego wzorca wystąpić, gdy poszczególnych dzierżaw pokonać usługi. Usługa Azure Search nie obsługuje obecnie uaktualnianie hello cenowym usługi wyszukiwania, dlatego wszystkie dane byłyby toobe ręcznie skopiowane tooa nowej usługi.

## <a name="3-mixing-both-models"></a>3. Mieszanie obu modeli
Wzorzec innego modelowania wielodostępności jest mieszanie strategii zarówno indeksu na dzierżawy i usług na dzierżawy.

Przez mieszanie hello dwa wzorce, dzierżaw największy aplikacji może być dedykowany usług podczas hello długo tail z mniej dzierżaw aktywnych, mniejsze może zajmować indeksów w udostępnionej usłudze. Ten model gwarantuje, że największy dzierżaw hello spójnie wysokiej wydajności z usługi hello jednocześnie dbając o tooprotect hello mniejszych dzierżaw z dowolnym zakłócenia sąsiadów.

Jednak implementacja tej strategii polega prognozowania w przewidywania dzierżawcami, które wymaga dedykowanego usługę indeksu w usług udostępnionych. Złożoność aplikacji zwiększa się wraz z hello potrzeby toomanage obu tych modeli wielodostępności.

## <a name="achieving-even-finer-granularity"></a>Obsługiwanie jeszcze bardziej szczegółowy
Witaj powyżej scenariuszy wielodostępnym toomodel wzorce projektowania w usłudze Azure Search założono uniform zakresu, w której poszczególne dzierżawy jest całego wystąpienia aplikacji. Jednak aplikacje czasami może obsługiwać wiele zakresów mniejsze.

Jeśli dzierżawa na usługi i indeksu na dzierżawy modele nie są wystarczająco małych zakresów, jest możliwe toomodel tooachieve indeksu jeszcze bardziej precyzyjną stopień szczegółowości.

toohave jeden indeks zachowywać się inaczej dla różnych klientów punktów końcowych, pola może być dodany tooan indeksu, który wyznacza wartość dla każdego klienta możliwe. Zawsze, klient wywołuje tooquery usługi Azure Search lub zmodyfikuj indeks, hello kod z aplikacji klienckiej hello określa hello odpowiednią wartość dla tego pola przy użyciu usługi Azure Search [filtru](https://msdn.microsoft.com/library/azure/dn798921.aspx) możliwości podczas przeszukiwania.

Ta metoda może być używane tooachieve funkcjonalność oddzielnych kont użytkowników, poziomy uprawnień oddzielne i nawet osobny aplikacji.

> [!NOTE]
> Podejście hello opisany powyżej tooconfigure tooserve indeks wiele dzierżaw wpływa na powitania znaczenie wyników wyszukiwania. Znaczenie w wyszukiwaniu są obliczane w zakresie poziomu indeksu, a nie zakresu poziomie dzierżawy, więc dzierżawcy wszystkich danych oceny przydatności hello podstawowej statystyk, takich jak częstotliwość termin jest włączona.
> 
> 

## <a name="next-steps"></a>Następne kroki
Usługa Azure Search jest atrakcyjnych wybór dla wielu aplikacji [Dowiedz się więcej o możliwości przeprowadzania hello usługi](http://aka.ms/whatisazsearch). Podczas obliczania hello różnych projektu wzorce dla wielodostępnych aplikacji, należy wziąć pod uwagę hello [różnych warstw cenowych](https://azure.microsoft.com/pricing/details/search/) i hello odpowiednich [usługi limity](search-limits-quotas-capacity.md) toobest dostosować toofit usługi Azure Search obciążeń aplikacji i architektur różnej wielkości.

Pytania dotyczące usługi Azure Search i scenariusze wielodostępnym może zostać skierowany tooazuresearch_contact@microsoft.com.

