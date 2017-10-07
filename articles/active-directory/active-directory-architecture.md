---
title: "Architektura usługi Azure Active Directory aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, co to jest dzierżawa usługi Azure AD, jak i toomanage Azure za pomocą usługi Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
writer: v-lorisc
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: markvi
ms.openlocfilehash: 799943c012dcc309907ed3c36372038a0aad222a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-active-directory-architecture"></a>Informacje na temat architektury usługi Azure Active Directory
Azure Active Directory (Azure AD) umożliwia toosecurely możesz zarządzać dostępu tooAzure usług i zasobów dla użytkowników. W ramach usługi Azure AD można skorzystać z pełnego zestawu możliwości zarządzania tożsamościami. Aby uzyskać więcej informacji na temat funkcji usługi Azure AD, zobacz [Co to jest usługa Azure Active Directory?](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-whatis)

Z usługą Azure AD można utworzyć i zarządzać użytkownikami i grupami i Włącz tooallow uprawnienia i odmowa dostępu tooenterprise zasobów. Informacji o zarządzaniu tożsamości, zobacz [hello podstawowe informacje na temat funkcji zarządzania tożsamościami Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity).

## <a name="azure-ad-architecture"></a>Architektura usługi Azure AD
Architektura geograficznie rozproszonych usługi Azure AD łączy szeroką gamę monitorowanie, automatycznego ponownego routingu, trybu failover i możliwości odzyskiwania Włącz nam toodeliver przedsiębiorstw dostępności i wydajności tooour klientów.

następujące elementy architektury Hello zostały omówione w tym artykule:
 *  Projekt architektury usługi
 *  Skalowalność 
 *  Ciągła dostępność
 *  Centra danych

### <a name="service-architecture-design"></a>Projekt architektury usługi
jednostki skalowania Hello system skalowalne, wysokiej dostępności i sformatowany danych odbywa się za pośrednictwem niezależnych bloków konstrukcyjnych lub jednostek skalowania dla warstwy danych hello Azure AD najczęściej toobuild sposób, są nazywane *partycji*. 

Warstwa danych Hello ma kilka usług frontonu, które zapewniają możliwości odczytu i zapisu. Poniższy diagram Hello pokazuje, jak składniki hello partycji katalogu pojedynczej są dystrybuowane w całym geograficznie distrubuted centrach danych. 

  ![Partycje pojedynczego katalogu](./media/active-directory-architecture/active-directory-architecture.png)

składniki Hello architektury usługi Azure AD zawierają replikę podstawową i repliki pomocniczej.

**Replika podstawowa**

Witaj *repliki podstawowej* odbiera wszystkie *zapisuje* dla partycji hello należy. Wszelkie zapisu operacji jest natychmiastowe replikowane tooa repliki pomocniczej w różnych centrach danych przed zwróceniem wywołującego toohello sukces, w związku z tym zapewnienia trwałości geograficznie nadmiarowego zapisów.

**Repliki pomocnicze**

Wszystkie operacje *odczytu* z katalogu są obsługiwane przez *repliki pomocnicze* w centrach danych, które fizycznie znajdują się w różnych lokalizacjach geograficznych. Istnieje wiele replik pomocniczych, ponieważ dane są replikowane w sposób asynchroniczny. Odczyty katalogu, takich jak żądania uwierzytelniania są obsługiwane z centrów danych, które są klientami tooour Zamknij. replik pomocniczych Hello są zobowiązani do odczytu skalowalności.

### <a name="scalability"></a>Skalowalność

Skalowalność to możliwość hello toomeet tooexpand usługi, coraz większej wydajności. Jest to osiągane przez partycjonowanie danych hello skalowalność zapisu. Skalowalność odczytu uzyskuje się poprzez replikację danych z jednej partycji toomultiple replikach pomocniczych dystrybuowane w całym hello world.

Żądania z katalogu aplikacji są zazwyczaj routingiem toohello centrum danych, które znajdują się najbliżej fizycznie. Zapisy są spójności odczytu i zapisu tooprovide repliki podstawowej toohello przekierowanych w sposób niewidoczny dla użytkownika. Replik pomocniczych znacznie rozszerzyć skalę hello partycji, ponieważ hello katalogi są zwykle obsługujących odczytów w większości przypadków hello.

Katalog aplikacji połączyć toohello najbliższej centrów danych. Powoduje to zwiększenie wydajności, co umożliwia przeprowadzenie skalowania w poziomie. Ponieważ partycji katalogu może mieć wiele replik pomocniczych, replikach pomocniczych można umieścić bliżej toohello katalogu klientów. Tylko wewnętrzny katalogu usługi składników, które są aktywne repliki podstawowej hello docelowym intensywnie wykonujących operacje zapisu bezpośrednio.

### <a name="continuous-availability"></a>Ciągła dostępność

Dostępność (lub pracy) definiuje hello zdolność nieprzerwaną tooperform systemu. tooAzure klucza Hello Directory wysokiej dostępności jest, że naszych usług można szybko przesunięcia ruchu w wielu centrach danych geograficznie rozproszonych. Każde centrum danych jest niezależne, co umożliwia wystąpienie nieskorelowanych trybów awarii.

Projekt partycji usługi Azure AD jest uproszczone toohello porównaniu enterprise projektowania usług AD, co jest szczególnie ważne dla skalowaniu hello systemu. Zaadoptowaliśmy projekt pojedynczego elementu głównego, który obejmuje starannie zorganizowany i deterministyczny proces pracy w trybie failover repliki podstawowej.

**Odporność na uszkodzenia**

System jest bardziej dostępny jest odporna na awarie toohardware, sieci i oprogramowania. Dla każdej partycji katalogu hello istnieje wysokiej dostępności repliki wzorca: hello repliki podstawowej. Tylko zapisy toohello partycji są wykonywane w tej replice. Ta replika jest natychmiast przesuniętych tooanother repliki mogą być nieustannie i ściśle monitorowanym i zapisów (które stają się hello nową podstawową) w przypadku wykrycia awarii. Podczas pracy w trybie failover może to być związane z utratą dostępności do zapisu trwającą zwykle od 1 do 2 minut. Taka sytuacja nie ma wpływu na dostępność do odczytu.

Operacje odczytu, (które outnumber zapisów przez wiele rzędów) postępować tylko toosecondary repliki. Ponieważ replikach pomocniczych idempotentności, utrata wszelkich jedna replika w danej partycji łatwo jest równoważone kierowanie hello odczyty tooanother repliki, zwykle w hello tym samym centrum danych.

**Trwałość danych**

Zapis jest trwale zatwierdzone tooat co najmniej dwóch danych centrów wcześniejsze tooit przyjęte. Dzieje się najpierw zatwierdzania zapisu hello na powitania podstawowego, a następnie natychmiast replikowanie hello zapisu tooat co najmniej jednego innego centrum danych. Gwarantuje to, że na potencjalnie krytycznego utraty hello data center hostingu hello podstawowego nie powoduje utraty danych.

Usługi Azure AD obsługuje zero [celu czasu odzyskiwania (RTO)](https://en.wikipedia.org/wiki/Recovery_time_objective) wydawania tokenów i katalog odczytuje i w kolejności hello minut (~ 5 minut) RTO katalog zapisuje. Obsługujemy również zerowy [cel punktu odzyskiwania (RPO, Recovery Point Objective)](https://en.wikipedia.org/wiki/Recovery_point_objective) i zapewniamy, że dane nie zostaną utracone podczas przechodzenia w tryb failover.

### <a name="data-centers"></a>Centra danych

Repliki usługi Azure AD są przechowywane w centrach danych znajdujących się na hello world. Aby uzyskać więcej informacji, zobacz [Centra danych platformy Azure](https://azure.microsoft.com/en-us/overview/datacenters).

Usługi Azure AD obsługuje między centrami danych hello następujące cechy:

 * Uwierzytelnianie, wykres i inne usługi AD znajdują się za hello Usługa bramy. Witaj bramy zarządza Równoważenie obciążenia tych usług. Automatycznie przejdzie ona w tryb failover, jeśli za pomocą transakcyjnych sond kondycji wykryte zostaną serwery w złej kondycji. W oparciu o te sondy kondycji, hello brama kieruje dynamicznie centrów danych toohealthy ruchu.
 * Aby uzyskać *odczytuje*, katalog hello ma replik pomocniczych i odpowiednie usługi frontonu w konfiguracji aktywny aktywny działających w wielu centrach danych. W przypadku awarii całym centrum danych ruch zostanie automatycznie routingiem tooa różnych centrach danych.
 *  Dla *zapisuje*, planowane hello katalogu zostanie pracy awaryjnej (master) repliki podstawowej między centrami danych za pośrednictwem (nową podstawową jest synchronizowane tooold podstawowego) lub procedury awaryjnego trybu failover. Trwałość danych uzyskuje się poprzez replikację żadnych centrów danych tooat co najmniej dwa zatwierdzania.

**Spójność danych**

model katalogu Hello jest jednym z spójność ostateczna. Typowy problemem z systemów rozproszonych asynchronicznie replikacji jest, że hello dane zwrócone w wyniku repliki "konkretnego" może nie być się toodate. 

Usługa Azure AD zapewnia spójność odczytu i zapisu dla aplikacji przeznaczonych dla repliki pomocniczej przez jego zapisów repliki podstawowej toohello routingu i synchronicznie ściąganie hello powrotem zapisuje toohello repliki pomocniczej.

Aplikacja zapisuje przy użyciu hello Graph API Azure AD są pobieranej utrzymanie repliki katalogu tooa koligacji spójności odczytu i zapisu. Hello usługi Azure AD Graph utrzymuje sesję logiczna ma koligacji tooa replika pomocnicza używana dla odczytów; koligacji są przechwytywane w "token repliki", który hello przy użyciu rozproszonej pamięci podręcznej usługi wykresu w pamięci podręcznej. Token ten jest następnie używany dla kolejnych operacji w hello tej samej logicznej sesji. 

 >[!NOTE]
 >Zapisy natychmiast są replikowane wydano odczyty toohello repliki pomocniczej toowhich hello logicznej sesji.
 >

**Ochrona kopii zapasowych**

katalog Hello implementuje usuwania nietrwałego, zamiast usuwania twardych, dla użytkowników i dzierżaw łatwe odzyskiwania w przypadku przypadkowemu usuwaniu przez klienta. Jeśli przypadkowo administratorem dzierżawy usuwa użytkowników, mogą łatwo cofnąć i przywrócić hello usunąć użytkowników. 

Usługa Azure AD implementuje codzienne tworzenie kopii zapasowych wszystkich danych i w związku z tym umożliwia autorytatywne przywrócenie danych w przypadku wykonania jakichkolwiek logicznych operacji usuwania lub uszkodzenia danych. Nasze warstwy danych korzystają z kodu służącego do korygowania błędów, dzięki czemu możliwe jest wykonanie sprawdzenia w poszukiwaniu błędów i automatyczne naprawienie określonych rodzajów błędów na dysku.

**Metryki i monitory**

Uruchamianie usługi o wysokiej dostępności wymaga światowej klasy metryk i możliwości monitorowania. Usługa Azure AD stale analizuje i raportuje kluczowe metryki kondycji usługi i kryteria powodzenia dla każdej ze swoich usług. Nieustannie opracowujemy i dostrajamy metryki, monitorowanie i alerty dla poszczególnych scenariuszy w ramach każdej z usług Azure AD i wszystkich innych usług.

Jeśli usługi Azure AD nie działa zgodnie z oczekiwaniami, natychmiast traktujemy akcji toorestore funkcji tak szybko jak to możliwe. Hello najważniejszych śledzi metryki usługi Azure AD jest jak szybko firma Microsoft może wykryć i ograniczyć klienta lub live problem lokacji. Możemy inwestycji w dużym stopniu monitorowanie i alerty toominimize czasu toodetect (docelowy TTD: < 5 minut) i gotowość do działania toominimize czasu toomitigate (docelowy TTM: < 30 minut).

**Zabezpieczanie operacji**

Stosujemy kontrole operacyjne, takie jak uwierzytelnianie wieloskładnikowe (MFA) dla każdej operacji, a także inspekcję wszystkich operacji. Ponadto używamy podniesienia uprawnień w czasie systemu toogrant niezbędne tymczasowego dostępu dla dowolnego operacyjne zadanie na żądanie w sposób ciągły. Aby uzyskać więcej informacji, zobacz [hello zaufane chmury](https://azure.microsoft.com/en-us/support/trust-center).

## <a name="next-steps"></a>Następne kroki
[Przewodnik dewelopera usługi Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-developers-guide)

