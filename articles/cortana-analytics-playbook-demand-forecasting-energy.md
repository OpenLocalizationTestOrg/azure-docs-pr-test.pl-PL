---
title: "aaaCortana Podręcznikowym szablonie rozwiązania analizy prognozowania żądanie energii | Dokumentacja firmy Microsoft"
description: "Szablon rozwiązania z analizy Cortana firmy Microsoft, które pomaga prognozy zapotrzebowania na energię narzędzie firmy."
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>Cortana Intelligence rozwiązania szablonu Podręcznikowym żądanie prognozowania energii
## <a name="executive-summary"></a>Podsumowanie dla kierownictwa
W hello poza kilku lat, Internetu rzeczy (IoT), alternatywnych źródeł energii i danych big data scalonym możliwości przeważająca toocreate narzędzie hello i domeny energii. Na powitania tym samym czasie, narzędzie hello i sektora energetycznego całego hello przejrzane zużycie spłaszczanie z konsumentami wymagających lepszego toocontrol sposoby ich wykorzystania energii. W związku z tym hello narzędzia i siatki inteligentnych firmy znajdują się w doskonałe potrzeby tooinnovate i odnawiania się. Ponadto wiele siatki zasilania i narzędzie stają się nieaktualne i bardzo kosztowna toomaintain i zarządzaj nimi. Podczas ostatniego roku hello hello zespół pracuje w liczba promujących zaangażowanie w domenie energii hello. Podczas rejestrowania tych transakcji napotkano wielu przypadkach, w których hello narzędzia lub niezależnym dostawcom oprogramowania (niezależni dostawcy oprogramowania) zostały wyszukiwania do prognozowania dla zapotrzebowania na energię w przyszłości. Te prognozy odgrywa ważną rolę w bieżących i przyszłych firmy i stały się hello foundation dla różnych zastosowań. Należą do zasilania krótko- i długoterminowe obciążenia prognozy, handlu, równoważenia obciążenia, optymalizacji siatki itp. Dane big data i zaawansowane analizy AA metody takie jak Learning maszyny (ML) są kluczowych czynników istnienie hello do produkcji dokładne i niezawodne prognozy.  

W tym podręcznikowym testujemy razem hello działalności biznesowej i analitycznego wskazówki potrzebne do pomyślnego tworzenia i wdrażania zapotrzebowania na energię prognozy rozwiązania. Te wytyczne proponowanych może pomóc narzędzia i inżynierów danych w ustalaniu rozwiązań pełni operationalized, oparte na chmurze, funkcja prognozowania żądanie analityków danych. Dla przedsiębiorstw, które właśnie uruchamiają swoje dane big data i przebieg zaawansowane metody analizy takie rozwiązanie może reprezentować hello początkowej inicjatora w ich długoterminowej strategii inteligentne siatki.

> [!TIP]
> toodownload diagram, który zawiera omówienie architektury tego szablonu, zobacz [architektura szablon rozwiązania Cortana Intelligence żądanie prognozowania energii](cortana-analytics-architecture-demand-forecasting-energy.md).  
> 
> 

## <a name="overview"></a>Omówienie
W tym dokumencie opisano hello business, danych i aspektów technicznych przy użyciu Cortana Intelligence i w określonego Azure Machine Learning (AML) hello implementacji i wdrażania rozwiązań prognozowania energii. dokument Hello obejmuje trzy główne części:  

1. Poznawanie firmy  
2. Opis danych  
3. Implementacja techniczna

Witaj **opis firm** części przedstawiono hello jeden toounderstand potrzeb biznesowych aspekt i należy wziąć pod uwagę przed toomaking decyzji inwestycji. Wyjaśniono, jak tooqualify hello problem biznesowy w tooensure ręcznie czy analizy predykcyjnej i uczenia maszynowego są rzeczywiście skuteczne i stosowane. dalsze dokumencie Hello opisano podstawy hello uczenia maszynowego i jak jest używane tooaddress prognozowania energii problemów. Go opisano wymagania wstępne hello i kryteria kwalifikacyjne hello w przypadku użycia. Niektóre przykładowe Użyj przypadków i w przypadku scenariuszy są również dostępne.

Dane są hello głównego składnika dla dowolnej maszyny uczenia rozwiązania. Witaj **opis danych** części niniejszego dokumentu opisano niektóre ważne kwestie związane z hello danych. Przedstawia go hello rodzaj danych niezbędnych do prognozowania energii, wymagania dotyczące jakości danych i jakie źródła danych zwykle istnieje. Również zasady, jak dane pierwotne hello jest tooprepare używane funkcje danych, które faktycznie dysków hello modelowania części.

trzeci części dokumentu hello Hello obejmuje hello **implementacji technicznej** aspekt rozwiązania. Funkcja inżynieryjne i modelowania na powitania core hello danych nauki procesu i w związku z tym jest omówiono szczegółowo. Obejmuje ona hello koncepcji usług sieci web, które to ważny do chmury wdrażania rozwiązań analizy predykcyjnej. Możemy również konspektu typowe architektury rozwiązania operationalized end-to-end.

Ponadto hello dokumentu zawiera materiały dodatkowe, pomocne toogain dalsze opis hello domeny i technologii.

Jest ważne toonote, że nie zamierzamy toocover tego dokumentu hello głębiej danych nauki procesu, aspektów matematycznych i technicznych. Te informacje można znaleźć w [dokumentacji usługi Azure ML](http://azure.microsoft.com/services/machine-learning/) i [blogi](http://blogs.microsoft.com/blog/tag/azure-machine-learning/).

### <a name="target-audience"></a>Odbiorcy docelowi
Witaj docelowymi odbiorcami tego dokumentu jest biznesowych i techniczne pracowników, którzy chcą toogain wiedzy i wiedzę na temat usługi Machine Learning na podstawie rozwiązania oraz jak te są używane w szczególności w ramach domeny prognozowania energii hello.

Analityków danych można również korzystać z odczytywania lepszego zrozumienia hello wysokiego poziomu ładowania czy dyski hello wdrożenia energii, funkcja prognozowania rozwiązania toogain tego dokumentu. W tym kontekście może być również używane tooestablish dobrej linii bazowej i punkt początkowy, aby uzyskać więcej szczegółowych i zaawansowane materiału.

### <a name="industry-trends"></a>Trendów w branży
W hello poza kilku lat IoT, alternatywnych źródeł energii i danych big data scalonym możliwości przeważająca toocreate narzędzie hello i energii. Na powitania tym samym czasie, narzędzie hello i sektorów energii całego hello przejrzane zużycie spłaszczanie z konsumentami wymagających lepszego toocontrol sposoby ich wykorzystania energii.

Wiele narzędzia i firm energii inteligentne ma zostały pioneering hello [inteligentne siatki](https://en.wikipedia.org/wiki/Smart_grid) przez wdrożenie wielu Użyj przypadków, które należy użyć hello danych wygenerowanych przez siatkę hello. Wiele przypadków użycia obracać wokół hello charakterystyki własnej produkcji energii elektrycznej: nie zebranych ani Odłóż przechowywane jako magazynu. Tak co jest generowany musi być używany. Narzędzia, które mają toobecome efektywniejsze należy po prostu zużycie energii tooforecast ponieważ który da im większe możliwości zbyt**saldo i podaży**, wibracjom energii, zapobiegając w ten **zmniejszyć cieplarnianych gaz emisji**i kontrolować koszty.

W przypadku kosztów, istnieje inny istotnym elementem, który jest cena. Nowe możliwości zasilania tootrade między narzędzia wprowadzenia w doskonałe musi zbyt**przewidywania przyszłego zapotrzebowania, przyszłych cen energii elektrycznej**. Może to ułatwić firm ustalić ich wielkości produkcji.

Użycie hello word "inteligentne", firma Microsoft faktycznie można znaleźć tooa siatki, które można dowiedzieć się, a następnie tworzenia prognoz. Można przewiduje się zmian okresach zużycia oraz **przewidywany jest tymczasowe przeciążenie sytuacji i automatycznie Dostosuj go**. Zdalnie regulacji zużycie (za pomocą hello tych liczników inteligentne), można obsługiwać przeciążeń zlokalizowane sytuacji. **Przewidywanie najpierw, a następnie działające**, siatki hello sprawia, że sama inteligentny wraz z upływem czasu.

Witaj pozostałej części tego dokumentu, możemy koncentruje się na określonej rodziny przypadków użycia, które obejmują prognozowania w przyszłości krótko- i długoterminowej zapotrzebowania na energię. Firma Microsoft pracy w tych obszarach przez kilka miesięcy i uzyskały niektórych wiedzy i umiejętności, która zezwolić nam tooproduce branży klasy wyników. Inne przypadki użycia zostanie również omówiona w dokumencie hello hello Najbliższa przyszłość.

## <a name="business-understanding"></a>Poznawanie firmy
### <a name="business-goals"></a>Cele biznesowe
Witaj **pokaz energii** celem jest toodemonstrate typowe analizy predykcyjnej i rozwiązania, które można wdrożyć w krótkim przedziale czasu uczenia maszynowego. W szczególności naszych bieżącego skoncentrować się na włączenie energii żądanie prognozy rozwiązania, aby jego wartości biznesowej można szybko zrealizowane i wykorzystać na. Witaj informacje w tym podręcznika dotyczącego mogą pomóc w powitania klienta służącymi hello następujące cele:

* Krótki czas toovalue machine learning na podstawie rozwiązania
* Możliwość tooexpand tooother przypadków użycia pilotażowego Użyj przypadków lub tooa szerszy zakres zależności od ich potrzeb firmy
* Szybko uzyskać informacje o produkcie pakietu Cortana Intelligence Suite

Z tych celów pamiętać tego podręcznika dotyczącego ma na celu dostarczania hello biznesowych i wiedzy technicznej, który pomoże osiągnięcie tych celów.

### <a name="power-load-and-demand-forecasting"></a>Obciążenia zasilania i prognozowanie żądanie
W ramach sektora energetycznego hello może istnieć wiele sposobów popytu prognozowania mogą pomóc w rozwiązywaniu problemów o krytycznym znaczeniu dla firmy. W rzeczywistości Prognozowanie żądanie jest uznawana za hello foundation dla wielu przypadki użycia rdzeni w branży hello. Ogólnie rzecz biorąc, możemy należy wziąć pod uwagę dwa typy prognoz popytu na energię: krótko- i długoterminowej. Każdy z nich może służą do różnych celów i wykorzystania inny sposób. Witaj podstawowa różnica między Witaj dwie jest hello prognozowania typu horizon, co oznacza hello zakres czasu do przyszłych hello, dla którego możemy prognozy.

#### <a name="short-term-load-forecasting"></a>Krótka obciążenia termin prognozowania
W kontekście hello zapotrzebowania na energię krótki okres załadować prognozowania (STLF) jest zdefiniowany jako hello zagregowane obciążenia, które jest prognozowanych w hello Najbliższa przyszłość na różne części hello siatki (lub siatki hello jako całość). W tym kontekście krótkoterminowa jest zakres czasu toobe zdefiniowanego w zakresie hello too24 1 godz. W niektórych przypadkach zakres 48 godzin jest także możliwa. W związku z tym STLF jest często w przypadku użycia operacyjne hello siatki. Oto kilka przykładów STLF zmiennych przypadki użycia:

* I podaży równoważenia
* Obsługa handlowym zasilania
* Tworzenie rynku (ustawienia zasilania cena)
* Optymalizacja operacyjne siatki
* [Odpowiedzi na żądanie](https://en.wikipedia.org/wiki/Demand_response)
* Szczytowy prognozowania żądanie
* Żądanie strony zarządzania
* Równoważenie obciążenia i zapobiegania przeciążenia
* Długoterminowych prognozowania obciążenia
* Wykrywanie błędów i anomalii
* Ograniczenie/bilansowanie godzinami szczytu 

STLF model najczęściej są oparte na powitania pobliżu poza (ostatniego dnia lub tygodnia) dane dotyczące zużycia i użyj prognozowanych temperatury jako ważne predykcyjne. Uzyskiwania dokładnych temperatury prognozy hello następnej godziny oraz godziny too24 staje się coraz mniejsze żądanie teraz dni. Te modele są mniej wrażliwych wzorce tooseasonal lub długoterminowej trendów zużycia.

Rozwiązania SLTF są również prawdopodobnie toogenerate dużej liczby wywołań prognozowania (żądania obsługi) od czasu ich trwa wywołania co godzinę, a w niektórych przypadkach nawet z częstotliwością wyższy. Możliwe jest również często zagnieżdżenia toosee gdzie każdego poszczególnych podstacji lub transformatora jest reprezentowany jako model autonomicznych i dlatego hello odebranej liczby żądań prognozowania są lepsze.

#### <a name="long-term-load-forecasting"></a>Długoterminowych prognozowania obciążenia
Celem Hello o długie termin obciążenia prognozowania (LTLF) jest żądanie zasilania tooforecast przy zakres czasu, w zakresie od 1 tydzień toomultiple miesięcy (i w niektórych przypadkach przez liczbę lat). Ten zakres typu horizon dotyczy przede wszystkim dotyczące planowania i przypadki użycia inwestycji.

W przypadku scenariuszy długoterminowej jest ważne toohave wysokiej jakości danych, które obejmuje zakres wielu lat (minimalna 3 lata). Te modele będzie zazwyczaj wyodrębniania wzorce sezonowości hello danych historycznych i korzystają z zewnętrznego predicators takie jako pogodą i klimatyzacja wzorce.

Ważne jest tooclarify, który hello dłużej hello prognozowania typu horizon hello mniej dokładne hello prognozy mogą być jest. Dlatego jest ważne tooproduce, przez niektóre interwały zaufania wraz z rzeczywistego hello prognozy, która umożliwiałaby ludzi toofactor hello odmiany możliwych do procesu planowania.

Ponieważ scenariusz użycia hello LTLF przede wszystkim jest planowanie, oczekujemy może znacznie niższe woluminów prognozowania (w porównaniu tooSTLF). Firma Microsoft zwykle zobaczyć te przewidywania osadzone w narzędzi wizualizacji, takich jak Excel lub Power Bi i można wywołać ręcznie przez użytkownika hello.

### <a name="short-term-vs-long-term-prediction"></a>Krótki okres programu vs. Długoterminowe prognozowania
Witaj w poniższej tabeli porównano STLF i LTLF w zakresie toohello najważniejsze atrybuty:

| Atrybut | Prognozy obciążenia krótkoterminowa | Długoterminowych prognozy obciążenia |
| --- | --- | --- |
| Prognozy typu Horizon |Od 1 godziny too48 godzin |Z miesięcy 1 too6 lub więcej |
| Poziom szczegółowości danych |Co godzinę |Co godzinę lub codziennie |
| Typowe zastosowania |<ul><li>Żądanie/dostaw równoważenia</li><li>Wybierz godzinę prognozowania</li><li>Odpowiedzi na żądanie</li></ul> |<ul><li>Długoterminowych planowania</li><li>Planowanie zasobów siatki</li><li>Planowanie zasobów</li></ul> |
| Zmienne typowych predykcyjne |<ul><li>Dnia lub tygodnia</li><li>Godzina dnia</li><li>Co godzinę temperatury</li></ul> |<ul><li>Miesiąc roku.</li><li>Dzień miesiąca</li><li>Temperatury długoterminowej i klimatyzacja</li></ul> |
| Zakres danych historycznych |Dwa toothree lat. danych |Pięć too10 lat. danych |
| Typowy dokładności |MAPE * 5% lub niższa |MAPE * 25% lub niższa |
| Prognozy częstotliwości |Tworzone co godzinę lub co 24 godziny |Utworzone po miesiąc, co kwartał lub roczne |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error) — oznacza średni procent błędów

Jak wynika z tej tabeli, jest bardzo ważne toodistinguish między hello krótki i długoterminowej hello prognozowania scenariuszy, jak te reprezentują potrzeb innej firmy i może mieć inne wdrożenie i wzorców użycia.

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>Przypadek użycia przykład 1: eSmart systemów — optymalizacji przeciążenia
Istotne znaczenie [inteligentne siatki](https://en.wikipedia.org/wiki/Smart_grid) jest toodynamically i stale zoptymalizować oraz dostosować hello zmiana wzorców użycia. Krótkoterminowej zmiany, które są głównie spowodowane zmianami temperatury może mieć wpływ na zużycie energii (*np.*, więcej mocy jest używana dla warunku lotniczego lub grzejników). At hello sam zużycie czasu, zasilanie również ma wpływ długoterminowych trendów. Mogą one obejmować sezonowości efekty, national święta długoterminowej wzrost zużycia i nawet ekonomiczne czynników, takich jak indeksu konsumenta, ceny wydobycie ropy naftowej i PKB.

W tym przypadku [eSmart](http://www.esmartsystems.com/) chciał toodeploy oparte na chmurze rozwiązanie, które umożliwia prognozowanie większego ukierunkowania hello sytuacji przeciążenia, w dowolnym danym podstacji hello siatki. W szczególności eSmart chciał podstacji tooidentify, znajdujące się prawdopodobnie toooverload w hello godzinę, więc natychmiastowych akcji można podjąć tooavoid lub rozwiązać takiej sytuacji.

Dokładne i szybkie prognozowania wymaga wykonania trzech modeli predykcyjnych:

* Czas terminu modelu czy umożliwia prognozowanie zużycia energii w każdym podstacji podczas hello dalej kilka tygodnie lub miesiące
* Krótkoterminowe modelu, który umożliwia prognozowanie sytuacja na danym podstacji podczas hello godzinę
* Model temperatury, który umożliwia prognozowanie przyszłych temperatury w wielu scenariuszach

Celem Hello modelu długoterminowej hello jest podstacji hello toorank przez ich toooverload większego ukierunkowania (podane ich transmisji moc) podczas hello dalej tygodnia lub miesiąca. Dzięki temu tworzenie hello krótką listę podstacji służących jako dane wejściowe do przewidywania krótkoterminowej hello. Temperatury jest ważne Prognoza modelu długoterminowej hello, istnieje temperatury wielu scenariusz produktu tooconstantly potrzeby prognozy i źródła je jako dane wejściowe do długoterminowego modelu toohello. krótkoterminowe Hello prognozy, następnie jest wywoływana toopredict które podstacji jest prawdopodobnie toooverload za pośrednictwem hello godzinę.

modele krótko- i długoterminowej Hello są wdrażane pojedynczo na każdym podstacji. W związku z tym hello praktyczne wykonanie tych modeli wymaga szeroką gamę aranżacji. toogain większej dokładności przewidywania w hello krótkoterminowego, bardziej szczegółowego model jest przeznaczony dla każdej godziny, dnia hello. Te modele są wykonywane co godzinę i Zakończ działanie w kilka minut tooallow wystarczający czas toorespond i podjąć działania zapobiegawcze, jeśli to konieczne. Ta kolekcja modeli są stale aktualizowane przez okresowe ponownego trenowania przy użyciu hello najnowszych danych.

Więcej informacji na temat tego przypadku użycia można znaleźć [tutaj](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945).

#### <a name="use-case-qualification-criteria--prerequisites"></a>Użyj kryteria kwalifikacyjne Case — wymagania wstępne
Hello głównego siła Cortana Intelligence jest toodeploy zaawansowanych możliwości i skali maszyny uczenie na rozwiązania. Jest zaprojektowana toosupport tysięcy z prognoz, które są wykonywane jednocześnie. Może automatycznie skalować toomeet zmiany wzorca użycia. Rozwiązania w związku z tym koncentruje się na niezawodność i wydajność obliczeniową. Na przykład firmę jest zainteresowana produkujących prognozy dla hello godzinę i dla każdej godziny, dnia hello zapotrzebowania na energię dokładne. Na hello drugiej strony, Dbamy mniej o udzielenie odpowiedzi na pytanie hello, dlaczego Żądanie hello jest przewidywane toobe jest (samego modelu hello zajmie się tym).

Dlatego jest ważne toorealize, że nie wszystkie przypadki użycia i problemów biznesowych mogą skutecznie rozwiązane, za pomocą uczenia maszynowego.

Cortana Intelligence i uczenia maszynowego mogą być bardzo wydajny w rozwiązaniu problemu biznesowego danego po spełnieniu hello następujące kryteria:

* Witaj problem biznesowy w ręcznie jest **predykcyjnej** charakter. W przykładzie przypadków użycia predykcyjnej jest firmy narzędzie, które toopredict power obciążenie danego podstacji podczas hello godzinę. Na hello drugiej strony, będzie analizowanie i klasyfikacji sterowników historycznych żądanie **opisową** charakter i w związku z tym mniejszej stosowane.
* Brak wyraźnego **ścieżkę akcji** toobe raz wykonane prognozowania hello jest dostępna. Na przykład przewidywanie przeciążenia na podstacji podczas następnej godziny hello może wyzwolić aktywnego akcji zmniejszenie obciążenia, który jest skojarzony z tym podstacji i w związku z tym potencjalnie uniemożliwia przeciążenia.
* przypadek użycia Hello reprezentuje **typowy typ problemu** tak, aby podczas rozwiązać go można Pave – toosolving sposób hello inne podobne przypadki użycia.
* powitania klienta można ustawić **cele ilościowe i jakościowe** toodemonstrate implementacji pomyślne rozwiązanie. Na przykład, dobrym ilościowy cel prognozy żądanie energii będzie hello wymaganej dokładności próg (*np.*, zapasowej too5% błąd jest dozwolone) lub gdy przewidywania podstacji przeciążenia, a następnie hello precision (liczba alarmów true) i odwołania (stopień alarmów true) powinna być większa niż wartość progowa w danym. Tych celów powinien pochodzić od celów biznesowych powitania klienta.
* Brak wyraźnego **scenariusza integracji** z firmy hello biznesowego przepływu pracy. Na przykład hello podstacji obciążenia prognozy można zintegrować działań związanych z zapobieganiem przeciążenia tooallow Centrum hello siatki formantu.
* powitania klienta ma gotowe toouse **danych za pomocą odpowiedniej jakości** toosupport hello przypadek użycia (Zobacz więcej informacji, zobacz następną sekcję hello **jakości danych**, z tego podręcznika dotyczącego).
* Witaj Architektura danych na chmurze obejmuje klienta lub **uczenie maszynowe oparte na chmurze**, w tym uczenie Maszynowe Azure i innych składników pakietu Cortana Intelligence Suite.
* powitania klienta jest gotowa tooestablish **przepływ danych tooend zakończenia** urządzeń hello dostarczania danych do chmury hello na bieżąco i jest gotowa zbyt**operacjonalizacji** hello rozwiązania.
* powitania klienta gotowa jest zbyt**dedykować zasoby** kto będzie można aktywnie zaangażowane podczas początkowej wdrożenia pilotażowego hello tak, aby wiedzy i własność hello rozwiązania mogą być przekazywane toohello klienta po pomyślnym ukończenia.
* powitania klienta zasób powinien być **danych wykwalifikowanych specjalistów**, najlepiej naukowca danych.

Kwalifikacji przypadek użycia oparte na powitania powyższymi kryteriami może znacznie poprawić odsetka pomyślnych hello przypadek użycia i ustanowienia dobrej beachhead dla implementacji hello przypadków użycia w przyszłości.

### <a name="cloud-based-solutions"></a>Rozwiązań w chmurze
Pakietu Cortana Intelligence Suite na platformie Azure jest zintegrowane środowisko, która znajduje się w chmurze hello. Witaj wdrażania rozwiązania zaawansowana analityka w środowisku chmury zawiera istotne korzyści dla firm i na powitania tym samym czasie może oznaczać duże zmiany dla firm, że nadal wykorzystanie lokalnych rozwiązań IT. W ramach sektora energetycznego hello Brak wyczyść trend Stopniowa migracja operacji w chmurze hello. Tego trendu idzie w parze wraz z programowanie hello siatki inteligentne hello jak wspomniano powyżej, w **trendów w branży**. Tego podręcznika dotyczącego koncentruje się na rozwiązanie oparte na chmurze w domenie energii hello, jest ważne tooexplain hello korzyści i innych kwestii związanych z wdrożeniem rozwiązania w chmurze.

Być może hello Największą zaletą rozwiązanie oparte na chmurze jest koszt hello. Jako rozwiązanie sprawia, że użycie składników wdrożonych w chmurze, nie istnieje kosztów góry lub kst (koszt z towarów sprzedanych) składnik kosztów skojarzonych z nim. Oznacza to, nie konieczności tooinvest sprzętu, oprogramowania i konserwację IT nie istnieje, czy w związku z tym jest znaczny spadek ryzyko.

Inną zaletą ważne jest hello struktury kosztów z rozwiązań w chmurze. Serwerów opartych na chmurze obliczeniowych i magazynu można wdrożyć i skalować na just zgodnie z potrzebami. Reprezentuje hello koszt korzyści rozwiązanie oparte na chmurze.

Ponadto nie istnieje potrzeba inwestowania w konserwacji IT lub infrastruktury przyszłego rozwoju wszystkich jest częścią hello oferta oparta na chmurze. zakres toothat, pakietu Cortana Intelligence Suite obejmuje hello najlepiej klasy usługi, a jego mapy drogowej śledzi zmieniających się. Nowe funkcje, składników i możliwości są stale wprowadzane i rozwijać.

Dla firmy, która jest uruchamiana jego przejścia do chmury hello wysokiej zalecamy tootake podejście stopniowe zaimplementowanie mapy drogowej migracji chmury. Mamy nadzieję, narzędzia i firmy w domenie energii hello przypadki użycia hello omówionych w tym podręcznika dotyczącego reprezentują doskonała okazja dla wdrażania pilotażowego rozwiązania analizy predykcyjnej w chmurze hello.

#### <a name="business-case-justification-considerations"></a>Względy biznesowe uzasadnienie wielkość
W wielu przypadkach powitania klienta mogą być zainteresowani biznesowego wyjaśnienia przypadek użycia danego, w którym są ważne składniki rozwiązania w chmurze i uczenia maszynowego. W przeciwieństwie do rozwiązania lokalnego, w przypadku hello rozwiązania oparte na chmurze składnik kosztów góry hello jest minimalny i większość elementów kosztów hello są skojarzone z rzeczywistego użycia. Po przejściu do toodeploying energii, funkcja prognozowania rozwiązania na pakietu Cortana Intelligence Suite, wielu usług można zintegrować z jednej wspólnej struktury kosztów. Na przykład baz danych (*np.*, SQL Azure) mogą być używane toostore hello nieprzetworzone dane i następnie dla hello rzeczywiste prognozy uczenie Maszynowe Azure jest używane toohost hello prognozowania usług. W tym przykładzie hello struktury kosztów mogą obejmować magazynu i składników transakcyjnych.

Na powitania drugiej strony, na jeden powinien dysponować dobrą znajomością hello wartościach biznesowych systemu operacyjnego zapotrzebowania na energię prognozowania (warunek krótko- i). W rzeczywistości jest ważne toorealize hello biznesu każdej operacji prognozy. Na przykład dokładnie prognozowania następne 24 godziny obciążenia zasilania dla hello może uniemożliwić nadprodukcji lub mogą pomagać w zapobieganiu przeciążenia na powitania siatki i to można określić pod względem oszczędności finansowe codziennie.

Podstawowa formuła obliczania hello finansowych zaletą żądanie prognozy rozwiązaniem byłoby: ![Podstawowa formuła obliczania hello finansowych zaletą żądanie prognozy rozwiązania](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

Ponieważ pakietu Cortana Intelligence Suite udostępnia z modelu cenowego, nie jest ponoszenia formuły toothis koszt stały składnik nie jest konieczne. Formuły można obliczyć na podstawie codziennie, miesięcznego lub rocznego.

Można znaleźć bieżącego pakietu Cortana Intelligence Suite i Azure ML planów cenowych [tutaj](http://azure.microsoft.com/pricing/details/machine-learning/).

### <a name="solution-development-process"></a>Proces tworzenia rozwiązania
cyklu programowanie Hello zapotrzebowania na energię prognozowania rozwiązania, które zwykle obejmuje 4 fazy, w które wykonujemy przy użyciu technologii opartych na chmurze, a usług w ramach hello pakietu Cortana Intelligence Suite.

Jest to zilustrowane w powitania po diagramu:

![Cykl inteligentne siatki](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

powitania po akapitu opisano proces ten krok 4:

1. **Zbieranie danych** — wszystkie zaawansowane analizy na podstawie rozwiązanie opiera się na danych (zobacz **opis danych**). W szczególności po przejściu do analizy toopredictive i prognozowania, możemy polegają na stałe, dynamiczne przepływu danych. W przypadku hello prognozowania żądanie energii tych danych można ustalić źródło bezpośrednio z liczników inteligentnych lub już agregowane w lokalnej bazie danych. Możemy również zależne od innych zewnętrznych źródeł danych, takich jak pogodą i temperatury. Ten przepływ bieżących danych należy zorkiestrowana, zaplanowane i przechowywać. [Fabryka danych Azure](http://azure.microsoft.com/services/data-factory/) (ADF) jest naszym głównym najważniejszą metodą roboczą do wykonywania tego zadania.
2. **Modelowanie** — dla prognoz energii dokładne i niezawodne jedną opracowanie (pociąg) i zachować dużą modelu, który sprawia, że wykorzystanie danych historycznych hello i wyodrębnia hello łatwy do rozpoznania i wzorce predykcyjnych w hello danych. obszar Hello Machine Learning (ML) ma zostały szybko rośnie z bardziej zaawansowane algorytmy rutynowo opracowywanych. Azure ML Studio udostępnia środowisko użytkowników, które pozwala korzystać z najbardziej zaawansowanych algorytmów uczenia Maszynowego w ramach przepływu pracy nad hello. Przepływ pracy przedstawia intuicyjne diagram przepływu i obejmuje przygotowanie danych hello, wyodrębniania funkcji modelowania i oceny modelu. Witaj użytkownika można ściągnąć setki różne modele, które znajdują się w tym środowisku. Witaj koniec tej fazy naukowca danych mają model pracy, które jest obliczane i gotowa do wdrożenia.
   
   powitania po diagramu jest Ilustracja typowego przepływu pracy:
   
   ![Modelowanie przepływu pracy](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **Wdrożenie** — w przypadku modelu pracy w strony hello następnym krokiem jest wdrożenie. W tym miejscu modelu hello jest konwertowany na usługi sieci web, która uwidacznia interfejs API RESTful, który można wywołać jednocześnie za pośrednictwem hello Internet od różnych klientów zużycia. Uczenie Maszynowe Azure zapewnia prosty sposób wdrażania modelu bezpośrednio z hello Azure ML Studio za pomocą jednego kliknięcia przycisku. pod maską hello odbywa się Hello cały proces wdrażania. To rozwiązanie może automatycznie skalować toomeet hello wymagane zużycia.
4. **Zużycie** — na tym etapie firma Microsoft faktycznie wprowadzać użycie hello prognozowania prognoz tooproduce modelu. zużycie Hello mogą być określane w aplikacji użytkownika (*np.*, pulpitu nawigacyjnego) lub bezpośrednio z systemu operacyjnego, takich jak żądanie/Podaj systemu lub rozwiązanie optymalizacji siatki. Wiele zastosowań, mogą być określane z pojedynczego modelu.

## <a name="data-understanding"></a>Opis danych
Po obejmujące względy biznesowe hello (zobacz **opis firm**) prognozowania rozwiązania zapotrzebowania na energię, firma Microsoft są teraz gotowe toodiscuss hello części danych. Wszystkie rozwiązania analizy predykcyjnej opiera się na danych. Energii prognozowania żądanie, możemy polegają na zużycie historycznych danych z różnych poziomów szczegółowości. Czy dane historyczne jest używana jako hello raw materiału. Będzie ona przechodzą dokładnych analiz, w których hello naukowca danych określi zmienne predykcyjne (również funkcje określonego tooas), które można umieścić w modelu, który ostatecznie wygeneruje prognoz hello wymagane.

W hello reszty w tej sekcji zostaną przedstawione hello różne procedury i zagadnienia, aby zrozumieć hello danych i w jaki sposób toobring on tooa użytecznej postaci.

### <a name="hello-model-development-cycle"></a>Witaj cyklu projektowanie modelu
Tworzenie dobrej prognozowania wymaga, aby pewne przygotowania dokładne modeli i planowania. Niszczy hello modelowania procesu do wielu kroków i koncentrujących się na jednym kroku w czasie znacznie może poprawić hello wynik hello całego procesu.

Witaj poniższym diagramie przedstawiono sposób hello modelowania procesu można podzielić na wiele kroków:

![Model programowania cyklu](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

Jak widać hello cykl składa się z sześciu kroków:

* Formułowanie problem
* Wprowadzanie danych i eksploracja danych
* Przygotowanie danych i inżynieria funkcji
* Modelowanie
* Ocena modelu
* Opracowywanie zawartości

W hello pozostałej części tej sekcji możemy opisano poszczególne kroki hello i tooconsider elementy w każdym kroku.

### <a name="problem-formulation"></a>Formułowanie problem
Firma Microsoft może formułowanie problem hello wziąć pod uwagę hello najważniejszych pierwszy krok wymaga uprzedniego tooimplementing tootake dowolnego rozwiązania analizy predykcyjnej. W tym miejscu możemy spowoduje przekształcenie hello problem biznesowy i Rozłóż go toospecific elementy, które mogą zostać rozwiązane przez przy użyciu danych i technik modelowania. Jest to problem hello tooformulate dobrym rozwiązaniem jako zestaw pytań chcielibyśmy tooanswer. Poniżej przedstawiono niektóre możliwe pytania, które mogą być stosowane w zakresie hello prognozowania żądanie energii:

* Co to jest hello oczekiwano obciążenie poszczególnych podstacji w hello następnej godziny lub dnia?
* Porę dnia, hello Moje siatki doświadczy szczytowego zapotrzebowania?
* Jakie jest prawdopodobieństwo obciążenia szczytowego Moje siatki toosustain hello oczekiwano?
* Podczas każdej godziny, dnia hello potrzebną moc powinna generować stacji zasilania hello?

Formułowanie te pytania pozwala nam toofocus na pobieranie danych po prawej stronie powitania i wdrażania rozwiązania, w pełni wyrównany hello wykonywanego problem biznesowy. Ponadto firma Microsoft, ustawić kilka kluczowych metryk możemy wydajności hello tooevaluate hello modelu. Na przykład jak dokładny czy hello prognozy być i co to jest zakres hello błędów, które nadal będą akceptowane przez firm hello?

### <a name="data-sources"></a>Źródła danych
Nowoczesne siatki inteligentne Hello zbiera dane z różnych części i składników hello siatki. Te dane reprezentuje różnych aspektów hello operacji i użycie hello hello zasilania siatki. W zakresie hello zapotrzebowania na energię hello prognozy możemy są ograniczanie hello omówione źródeł danych, które odzwierciedlać hello rzeczywiste żądanie zużycia. Jedno źródło ważne zużycia energii są inteligentne liczników. Narzędzia na całym świecie hello są szybkiego wdrażania inteligentne liczników dla swoich klientów. Inteligentne liczników Rejestruj hello faktyczne zużycie energii i stale przekazywania tej firmy narzędzie wstecz toohello danych. Dane są zbierane i wysłane w stałych interwałach, począwszy od godziny too1 co 5 minut. Bardziej zaawansowane liczników inteligentne mogą być programowane zdalnie toocontrol i saldo hello rzeczywiste użycie w gospodarstwo domowe. Dane inteligentnych meter jest stosunkowo niezawodne i zawiera sygnaturę czasową. Dzięki temu ważne składnika żądanie prognozy. Dane licznika można agregować (równy określonemu procentowi górę) na różnych poziomach topologii siatki hello: transformatora, podstacji, region, *itp*. Firma Microsoft może następnie wybrać toobuild poziomu agregacji hello wymagane modelu prognozowania można używać dla niego. Na przykład jeśli hello narzędzie firmy będzie jak tooforecast przyszłych obciążenia na wszystkich jego podstacji siatki następnie wszystkie liczniki danych można agregowane dla każdego poszczególnych podstacji i używane jako dane wejściowe dla hello prognozowania modelu. Firma Microsoft można znaleźć liczników toosmart jako źródło danych wewnętrznych.

Prognozy niezawodnej energii będzie używana również innych zewnętrznych źródeł danych. Jeden istotny czynnik, który ma wpływ na zużycie energii jest pogody hello lub bardziej precyzyjnie hello temperatury. Dane historyczne pokazuje silne powiązania między temperatury na zewnątrz i zużycie energii. Dni gorące lato konsumentów należy użyć ich klimatyzacja i podczas włączania zima hello grzewczych. Wiarygodnego źródła historycznych temperatur w lokalizacji siatki hello jest w związku z tym kluczem. Ponadto firma Microsoft również polegać na dokładne prognozy temperatury jako predykcyjne zużycia energii.

Inne zewnętrznych źródeł danych może również pomóc w budowania modeli prognozowania żądanie energii. Mogą one obejmować długoterminowe klimatyzacja zmiany, ekonomiczny indeksów (*np.*, PKB) i inne. W tym dokumencie firma Microsoft nie będzie zawierał te inne źródła danych.

### <a name="data-structure"></a>Struktury danych
Po identyfikacji hello wymagane źródeł danych, firma Microsoft będzie jak tooensure że nieprzetworzone dane, które zostały zebrane zawiera hello Popraw funkcje związane z danymi. toobuild niezawodnej żądanie modelu prognozy, czy musimy elementów danych, które mogą pomóc przewidywania przyszłego zapotrzebowania hello obejmuje tooensure, który hello zebranych danych. Poniżej przedstawiono niektóre podstawowe wymagania dotyczące struktury danych hello (schemat) hello nieprzetworzone dane.

dane pierwotne Hello składa się z wierszy i kolumn. Każda miara jest reprezentowany jako pojedynczy wiersz danych. Każdy wiersz danych zawiera wiele kolumn (również tooas określonej funkcji lub pól).

1. **Sygnatura czasowa** — pola sygnatury czasowej hello reprezentuje rzeczywisty czas hello, gdy zarejestrowano hello miary. Powinny być zgodne z jednym z hello typowe formaty daty/godziny. Części zarówno data i godzina powinny być włączone. W większości przypadków nie jest konieczne dla toobe czasu hello zarejestrowane do hello drugiego poziomu szczegółowości. Jest strefa czasowa hello toospecify ważne w którym dane hello są rejestrowane.
2. **Pomiarowe identyfikator** — to pole określa licznik hello lub hello pomiaru urządzenia. Jest zmienną podzielone na kategorie i może być kombinacja cyfr i znaków.
3. **Wartość zużycia** — jest to rzeczywiste zużycie hello w danym daty/godziny. zużycie Hello można mierzony w kWh (kilowatt-hour) lub innych preferowanym jednostki. Jest ważne przez wszystkie miary w danych hello toonote, który hello jednostkę miary musi pozostaną niezmienione. W niektórych przypadkach użycia mogą być dostarczane ponad 3 fazy zasilania. W takim przypadku czy potrzebujemy toocollect wszystkich faz niezależne zużycie hello.
4. **Temperatury** — temperatury hello zwykle są zbierane z niezależne źródło. Jednak powinny być zgodne z hello dane dotyczące zużycia. Powinna zawierać znacznik czasowy zgodnie z powyższym opisem, co umożliwi jej toobe zsynchronizowane z danymi rzeczywistego zużycia hello. wartość temperatury Hello można określić w stopniach c lub f, ale powinny pozostać spójna we wszystkich pomiarów.
5. **Lokalizacja —** pole lokalizacji hello jest zazwyczaj skojarzony z hello miejscu, gdzie hello temperatury dane zostały zebrane. Może być reprezentowany, jako liczbę kodu pocztowego lub w formacie (lat/long) szerokości geograficznej/długości.

następujące tabele Hello przedstawiono przykłady dobrej konsumenckich i temperatury format danych:

| **Data** | **Czas** | **Identyfikator miernika** | **Faza 1** | **Faza 2** | **Faza 3** |
| --- | --- | --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |ABC1234 |7.0 |2.1 |5.3 |
| 7/1/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3 |
| 7/1/2015 |10:00:02 |ABC1234 |6.0 |2.1 |4.0 |

| **Data** | **Czas** | **Lokalizacja** | **Temperatury** |
| --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |11242 |24.4 |
| 7/1/2015 |10:00:01 |11242 |24.4 |
| 7/1/2015 |10:00:02 |11242 |24.5 |

Jak podano powyżej, w tym przykładzie obejmuje 3 różne wartości zużycia skojarzone z 3 fazy zasilania. Należy również zauważyć, że hello pól daty i godziny są rozdzielone, jednak można także je łączyć w jednej kolumnie. W takim przypadku hello lokalizacji kolumna jest wyświetlana w formacie 5-cyfrowy kod i temperatury hello w formacie c stopnia.

### <a name="data-format"></a>Format danych
Pakietu Cortana Intelligence Suite może obsługiwać hello najbardziej typowych formatów danych, takich jak CSV, TSV, JSON, *itp*. Należy tego formatu danych hello pozostaje spójna dla hello cały cykl życia hello projektu.

### <a name="data-ingestion"></a>Wprowadzanie danych
Ponieważ energii prognozy jest stale i często przewidzieć, Upewniamy się, że nieprzetworzone dane hello jest przepływu za pomocą procesu wprowadzanie danych stałych i niezawodne. proces wprowadzanie Hello musi gwarancji, że dane pierwotne hello jest dostępne dla hello prognozowania procesu w czasie hello wymagane. Oznacza to, że hello danych wprowadzanie częstotliwości powinna być większa niż hello prognozowania częstotliwości.

Na przykład: naszych żądanie prognozowania rozwiązanie powoduje wygenerowanie nowej prognozy o 8:00 codziennie, a następnie potrzebujemy tooensure, że wszystkie dane hello, które zostały zebrane podczas ostatniej hello 24 godzin zostały całkowicie pozyskanych do tego punktu i czy przypisano tooeven obejmują hello Ostatnia godzina danych.

W celu tooaccomplish tego pakietu Cortana Intelligence Suite udostępnia różne sposoby toosupport procesu wprowadzanie danych. To spowoduje dalsze omówione w hello **wdrożenia** sekcji tego dokumentu.

### <a name="data-quality"></a>Jakość danych
źródła danych pierwotnych Hello, które jest wymagane do wykonywania żądanie niezawodnych i precyzyjne prognozowania musi spełniać kryteria jakości niektóre podstawowe dane. Mimo że zaawansowane metody statystyczne mogą być używane toocompensate problemu jakości niektórych danych, potrzebujemy nadal tooensure, że są możemy przekraczających próg jakości niektóre podstawowe dane podczas wprowadzania nowych danych. Poniżej przedstawiono kilka zagadnienia dotyczące jakości danych pierwotnych:

* **Brak wartości** — odnosi się toohello sytuacji, gdy nie zostały zebrane, określony rozmiar. Witaj w tym miejscu podstawowy wymóg jest tym hello Brak szybkość wartość nie powinna być większa niż 10% dowolnego danego okresu. W przypadku pojedynczej wartości nie ma on należy wskazać przy użyciu wstępnie zdefiniowanych wartości (na przykład: "9999"), a nie "0", który może być nieprawidłowa.
* **Dokładność pomiaru** — wartość rzeczywista hello zużycia lub temperatury powinny być dokładnie zarejestrowane. Pomiary niedokładne utworzy prognoz niedokładne. Zazwyczaj błąd pomiaru hello powinna być niższa od wartości true względną toohello 1%.
* **Czas pomiaru** — jest to wymagane zbieranych danych hello rzeczywiste sygnatura czasowa tego hello nie może odbiegać o więcej niż 10 sekund toohello względna wartość true, czas pomiaru rzeczywiste hello.
* **Synchronizacji** — po wielu źródeł danych są używane (*np.*, konsumenckich i temperatury) musi zapewnić, że nie istnieją żadne synchronizacja czasu między nimi. Oznacza to, czasie hello różnica między sygnatury czasowej hello zebrane z dowolnym dwóch niezależnych źródeł danych nie może przekraczać więcej niż 10 sekund.
* **Czas oczekiwania** — jak wspomniano powyżej, w **wprowadzanie danych**, możemy zależą od procesu przepływu i wprowadzanie danych. toocontrol, że firma Microsoft musi zapewnić, że firma Microsoft kontroluje hello opóźnienia przesyłania danych. To jest określony jako hello odstęp czasu między hello pomiar hello została wykonana i hello jaką zostało załadowane do hello pakietu Cortana Intelligence Suite magazynu i jest gotowy do użycia. Krótkoterminowe obciążenia prognozowania opóźnienie całkowite hello nie powinna być większa niż 30 minut. Długoterminowe obciążenia prognozowania opóźnienie całkowite hello nie mogą zawierać więcej niż 1 dzień.

### <a name="data-preparation-and-feature-engineering"></a>Przygotowanie danych i inżynieria funkcji
Po hello nieprzetworzone dane zostały pozyskanych (zobacz **wprowadzanie danych**) i został bezpiecznie przechowywane, jest gotowy toobe przetworzone. Hello fazie przygotowywania danych jest zasadniczo pobierania danych pierwotnych hello i konwertowanie (Przekształcanie, przekształcanie) go w formie dla hello modelowania fazy. Który może obejmować proste operacje, takie jak przy użyciu kolumny danych pierwotnych hello tak jak jego rzeczywista wartość zmierzona, wartości standardowych, bardziej złożonych operacji takich jak [czasu mniej rozwiniętych](https://en.wikipedia.org/wiki/Lag_operator)i inne. kolumny danych Hello nowo utworzony są określonego tooas danych funkcji i hello proces generowania te jest tooas określonej funkcji engineering. Przez hello zakończenie tego procesu czy mamy nowy zestaw danych, które zostały uzyskane z hello nieprzetworzone dane i może służyć do modelowania. Ponadto musi tootake nad brakujące wartości w fazie przygotowywania danych hello (zobacz **jakości danych**) i je skorygować. W niektórych przypadkach firma Microsoft również musi toonormalize hello danych tooensure, że wszystkie wartości są reprezentowane w hello samej skali.

W tej sekcji niektóre hello typowe funkcje danych, które znajdują się w energii hello na listę modele prognozy żądanie.

**Czas pracy funkcji:** te funkcje są obliczane na podstawie danych Data/sygnatura czasowa hello. Są wyodrębniane i przekonwertowane na podzielone na kategorie funkcji, takich jak:

* Godzina dnia — jest to hello godzinę dnia hello pobierający wartości z 0 too23
* Dzień tygodnia — to reprezentuje hello dzień tygodnia hello i pobiera wartości 1 (niedziela) too7 (sobota)
* Dzień miesiąca — to reprezentuje hello rzeczywista data i może przyjmować wartości z 1 too31
* Miesiąc roku — to reprezentuje hello miesiąca i pobiera wartości 1 (styczeń) too12 (grudzień)
* Weekendowe — jest to funkcja wartość binarną, która przyjmuje hello wartości 0 dni tygodnia lub 1 dla weekendowe
* Święto — jest to funkcja wartość binarną, która przyjmuje hello wartości 0 dla regularnych dzień lub 1 dla dniem wolnym od pracy
* Warunki transformaty — Witaj transformaty warunki są wagi, pochodzących z sygnatury czasowej hello i są używane toocapture hello sezonowości (cykle) hello danych. Ponieważ firma Microsoft może mieć wiele okresów w zestawie danych Firma Microsoft może wymagać wiele warunków transformaty. Na przykład wartości żądanie może być roczne, co tydzień i codzienne okresów/cykle skutkujących 3 warunki transformaty.

**Funkcje miary niezależne:** hello niezależne funkcje obejmują wszystkie elementy danych hello, że jako zmienne predykcyjne chcielibyśmy toouse w modelu. W tym miejscu możemy wykluczyć hello funkcji zależnych, która będzie potrzebujemy toopredict.

* Funkcja Lag — są to czas przesunięte wartości hello rzeczywiste żądanie. Na przykład funkcji lag 1 będą przechowywane wartości Żądanie hello w bieżącą sygnaturę czasową hello poprzedniej godziny (przy założeniu danych co godzinę) toohello względną. Podobnie, możemy dodać opóźnienie 2, lag 3, *itp*. hello rzeczywiste kombinacją funkcji lag, które są używane są określane podczas modelowania fazy hello przez ocenę hello wyniki modelu.
* Długoterminowych trendów — ta funkcja reprezentuje liniowy wzrostu popytu latach hello.

**Funkcja zależnych:** funkcji zależnych hello jest hello kolumny danych, którego chcemy naszych toopredict modelu. Z [nadzorowanego uczenia maszynowego](https://en.wikipedia.org/wiki/Supervised_learning), należy najpierw uczenia modelu hello przy użyciu funkcji zależnych hello, (która jest również tooas określonej etykiety). Dzięki temu wzorców hello toolearn modelu hello w hello dane skojarzone z hello funkcji zależnych. W zapotrzebowania na energię prognozy chcemy zwykle toopredict hello rzeczywiste żądanie i dlatego firma Microsoft może używać go jako hello funkcji zależnych.

**Obsługa brakujących wartości:** w fazie przygotowywania danych hello, potrzebujemy czy toodetermine hello najlepszych strategii toohandle brakujące wartości. Jest to przede wszystkim za pomocą hello różnych statystyczne [metod przypisywania danych](https://en.wikipedia.org/wiki/Imputation_\(statistics\)). W przypadku hello zapotrzebowania na energię prognozowania możemy zazwyczaj przypisują brakujące wartości przy użyciu średniej ruchomej z poprzednich punktów danych.

**Normalizacji danych:** normalizacji danych jest innego typu przemian, które jest używane toobring wszystkie dane liczbowe, takie jak żądanie prognozy do podobnych skali. Zazwyczaj poprawia to hello modelu dokładność i precyzja. Firma Microsoft będzie zwykle w tym celu dzielenia wartości rzeczywistej hello przez zakres hello hello danych.
Powoduje to skalowanie hello oryginalnej wartości w dół do mniejszego zakresu, zazwyczaj z zakresu od -1 do 1.

## <a name="modeling"></a>Modelowanie
modelowanie fazy Hello jest których odbywa się hello konwersja hello danych do modelu. W hello core tego procesu są zaawansowane algorytmy, które skanowania hello dane historyczne (dane szkoleniowe), Wyodrębnij wzorców i tworzenia modelu. Ten model można później toopredict używanych na nowe dane, które nie było używane toobuild hello modelu.

Gdy mamy działającego niezawodnej modelu następnie wykorzystamy je tooscore nowe dane strukturalne tooinclude hello wymagane funkcje (X). Użyj modelu utrwalonego hello (obiekt z fazy szkolenia hello) i przewidywanie hello Zmienna docelowa, która jest oznaczona Ŷ spowoduje, że Hello oceniania procesu.

### <a name="demand-forecasting-modeling-techniques"></a>Żądanie prognozowania technik modelowania
W przypadku hello żądanie prognozowania wykonujemy korzystanie z danych historycznych, który jest uporządkowany według czasu. Ogólnie określane toodata zawierający wymiar czasu hello jako [czasu serii](https://en.wikipedia.org/wiki/Time_series). Celem Hello w czasie serii modelowania jest czas toofind powiązane trendów sezonowości, auto korelacji (korelacji wraz z upływem czasu) i sformułować ich na modelu.

W ostatnich latach zaawansowane algorytmy zostały rozwinięte tooaccommodate czasu serii prognozowania i tooimprove dokładność prognozowania. Pokrótce omówiono niektóre z nich w tym miejscu.

> [!NOTE]
> W tej sekcji nie jest zamierzone toobe używane jako machine learning i prognozowanie Przegląd, ale raczej krótką ankietę modelowania techniki, które są często używane do prognozowania żądanie. Aby uzyskać więcej informacji i materiały edukacyjne o prognozowania szeregu czasu, zdecydowanie zaleca się książki online hello [Prognozowanie: zasady i praktyki](https://www.otexts.org/book/fpp).
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**MA (średnia)**](https://www.otexts.org/fpp/6/2)
Średniej ruchomej jest jednym z hello pierwszy techniki analityczne używane do prognozowania serie czasu i nadal jest jednym z techniki hello najczęściej używane obecnie. Jest również podstawą hello bardziej zaawansowane techniki prognozowania. O średniej ruchomej przez uśrednianie punktów najnowszych hello K, gdzie K określa kolejność hello hello średniej ruchomej możemy są Prognozowanie hello następnego punktu danych.

Przenoszenie technika średni Hello hello powoduje wygładzanie hello prognozy i w związku z tym nie może obsłużyć również dużej zmienności hello danych.

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**ETS (Wygładzanie wykładnicze)**](https://www.otexts.org/fpp/7/5)
Wykładniczej Wygładzanie (ETS) to rodzina różnych metod, które używają średnią ważoną ostatnie punktów danych w kolejności toopredict hello następnego punktu danych. pomysł Hello jest wyższe wagi tooassign toomore ostatnie wartości i stopniowo zmniejszyć to waga dla starszych mierzone wartości. Istnieje wiele różnych metod z tej rodziny, niektóre z nich obejmują, takich jak obsługa sezonowości hello danych [Holt Winters okresach metody](https://www.otexts.org/fpp/7/5).

Niektóre z tych metod również współczynnik sezonowości hello hello danych.

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**ARIMA (Regresja automatycznie zintegrowany przeniesienie średniej)**](https://www.otexts.org/fpp/8)
Automatycznie regresji zintegrowane przeniesienie średniej (ARIMA) jest innej rodziny metod, który jest powszechnie używany do prognozowania szeregów czasowych. Łączy praktycznie metody automatycznego regresji przy średniej ruchomej. Metody regresji automatycznie używać modeli regresji wykonując poprzedniej wartości szeregu czasu w kolejności toocompute hello dalej daty punktu. Metody ARIMA mają zastosowanie również różnicowych metody, które obejmują obliczanie hello różnica między punktami danych i używanie zamiast oryginalnej wartości zmierzona hello. Na koniec ARIMA również sprawia, że użycie hello przeniesienie średniej techniki, które opisano powyżej. Kombinacja Hello wszystkie te metody na różne sposoby jest, jakie konstrukcje hello rodziny metody ARIMA.

ETS i ARIMA są powszechnie używany w tej chwili prognozowania żądanie energii i wiele innych problemów prognozowania. W wielu przypadkach są połączone ze sobą toodeliver bardzo dokładne wyniki.

**Ogólne regresja wielokrotna** regresji modeli może być hello najważniejszych metoda modelowania w domenie hello uczenia maszynowego i statystyki. W kontekście hello szeregów czasowych używamy regresji toopredict hello przyszłych wartości (*np.*, popytu). W regresji możemy zająć liniowy kombinację zmienne predykcyjne hello i Dowiedz się hello wagi (również określonego tooas współczynników) te zmienne predykcyjne podczas procesu szkolenia hello. Celem Hello jest tooproduce regresji, który będzie prognozy naszych przewidywane wartości. Metody regresji są odpowiednie, gdy zmienna docelowa hello jest liczbą i w związku z tym również pasuje do prognozowania szeregu czasu. Istnieje szereg metod regresji, w tym modele regresji bardzo proste, takich jak [regresji liniowej](https://en.wikipedia.org/wiki/Linear_regression) i bardziej zaawansowane te, takich jak drzew decyzyjnych [lasach losowa](https://en.wikipedia.org/wiki/Random_forest), [Neural Sieci](https://en.wikipedia.org/wiki/Artificial_neural_network)i Boosted drzewa decyzyjnego.

Konstruowanie zapotrzebowania na energię prognozowania jako problem regresji daje dużą elastyczność w wyborze funkcji naszych danych, które mogą być łączone z hello rzeczywiste żądanie czasu serii danych i czynniki zewnętrzne, takie jak temperatury. Więcej informacji na temat hello wybrane funkcje zostały omówione w hello funkcji Engineering (zobacz **Przygotowanie danych i funkcji Engineering**) części tego podręcznika dotyczącego.

Naszym doświadczeniu z implementacji i wdrożenia pilotażowego prognoz żądanie energii znaleźliśmy hello modeli regresji zaawansowane, które są dostępne w usłudze Azure ML często tooproduce hello najlepsze wyniki, a wykonujemy korzystać z nich.

## <a name="model-evaluation"></a>Ocena modelu
Ocena modelu ma kluczową rolę w hello **modelu programowania cyklu**. W tym kroku opisano do sprawdzania poprawności modelu hello i jej wydajności z rzeczywistych danych. Podczas modelowania krok hello używamy część hello dostępnych danych do uczenia modelu hello. W fazie oceny hello traktujemy hello pozostałej części hello danych tootest hello modelu. Praktycznie oznacza, że firma Microsoft hello modelu nowe dane, które zostały restrukturyzacji i zawiera takie same funkcje jako zestawu danych szkoleniowych hello hello są zasilania. Jednak w trakcie weryfikacji hello firma Microsoft hello modelu toopredict hello docelowy zmienna zamiast Podaj hello Zmienna docelowa dostępne. Firma Microsoft często można znaleźć procesu toothis jako oceniania modelu. Następnie użyje firma Microsoft hello wartości true docelowych i porównaj je z hello tych przewidzieć. Celem Hello jest toomeasure i zminimalizować hello prognozowania błąd, oznacza hello różnica między prognoz hello i hello wartość true. Kwantyfikacja pomiaru błędów hello jest klucza, ponieważ będziemy chcesz toofine strojenia hello modelu i sprawdź, czy błąd hello faktycznie jest zmniejszenie. Dostosowawczych modelu hello może odbywać się przez zmodyfikowanie modelu parametrów, które kontrolują hello uczenia proces lub przez dodanie lub usunięcie funkcji danych (określonego tooas [odchylenia parametry](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep)). Praktycznie który oznacza że firma Microsoft może muszą tooiterate między hello funkcji zespołu inżynieryjnego, modelowania, model fazy oceny wielokrotnie, dopóki nie jesteśmy w stanie tooreduce hello błąd toohello wymagany poziom.

Jest ważne tooemphasis Błąd prognozowania hello nigdy nie będą zero, ponieważ nie jest nigdy modelu, który można dokładnie przewidzieć co wynik. Istnieje jednak wielkość błędu, który jest akceptowane przez hello biznesowych. W procesie weryfikacji hello chcielibyśmy tooensure czy naszych Błąd prognozowania modelu jest na powitania poziom lub lepszą niż tolerancji firm hello poziomu. Ważne jest, w związku z tym tooset poziom hello hello dopuszczalna błędu początku hello hello cykl podczas hello **formułowanie Problem** fazy.

### <a name="typical-evaluation-techniques"></a>Ocena typowe techniki
Istnieją różne sposoby, w których prognozowania błąd może być mierzony i wyliczone. W tej sekcji możemy koncentruje się hello dyskusji w serii tootime odpowiednich technik oceny i specyficzne dla zapotrzebowania na energię prognozy.

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE oznacza oznacza błąd absolutny procent. Z MAPE możemy są obliczania różnicy hello każdego punktu prognozowanych i wartością rzeczywistą hello tego punktu. Następnie możemy określenie błąd hello na punkt obliczanie hello część hello różnica względną toohello rzeczywistej wartości. W ostatnim kroku będziemy średni tych wartości. Formuła matematyczne Hello używany dla MAPE jest hello poniżej:

![Formuła MAPE](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*gdzie A<sub>t</sub> jest wartość rzeczywista hello, F<sub>t</sub> hello przewidywane wartości, a n jest hello prognozy zakresu.*

## <a name="deployment"></a>Wdrożenie
Po możemy zająć hello modelowania fazy i zweryfikować hello modelu wydajności możemy toogo gotowy do hello faza wdrożenia. W tym kontekście wdrożenia oznacza włączenie powitania klienta tooconsume hello modelu przez rzeczywiste prognoz na nim uruchomione w dużej skali. koncepcja Hello wdrożenia to klucz w uczenie Maszynowe Azure, ponieważ naszym głównym celem jest tooconstantly wywołania prognoz jako min. toojust uzyskiwanie hello wgląd w dane hello. Faza wdrożenia Hello wchodzi w skład hello gdy włączysz toobe modelu hello używane na dużą skalę.

W kontekście hello zapotrzebowania na energię prognozy naszym celem jest tooinvoke ciągły i okresowe prognoz przy jednoczesnym zapewnieniu, że świeże dane są dostępne dla modelu hello i tym hello prognozowanych się, że dane są przesyłane z tyłu toohello odbierającą klienta.

### <a name="web-services-deployment"></a>Wdrażanie usługi sieci Web
Hello głównego można wdrożyć bloków konstrukcyjnych w uczenie Maszynowe Azure to usługa sieci web hello. Jest to hello najbardziej efektywny sposób tooenable zużycia modelu predykcyjnego w chmurze hello. Hello usługi sieci Web hermetyzuje hello modelu i otacza go z [RESTful](http://www.restapitutorial.com/) interfejsu API (Application Programming Interface). Witaj interfejsu API może służyć jako część żadnego kodu klienta, jak pokazano na poniższym diagramie hello.

![Firma Microsoft wdrażania usługi i zużycia](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

Jak widać, usługa sieci web hello jest wdrożona w hello pakietu Cortana Intelligence Suite chmury i może być wywoływany za pośrednictwem jej narażonych punkt końcowy interfejsu API REST. Innego typu klientów w różnych domenach można wywołać jednocześnie hello usługi za pośrednictwem hello interfejsu API sieci Web. Usługa sieci web Hello jest także skalowanie do obsługi wielu współbieżnych wywołań.

### <a name="a-typical-solution-architecture"></a>Architektura rozwiązania typowych
W przypadku wdrażania rozwiązania prognozowania zapotrzebowania na energię, Dbamy o wdrażanie tooend rozwiązanie, wykracza poza usługi sieci web hello prognozowania, który ułatwia hello przepływu danych. W czasie hello możemy wywołania nowej prognozy potrzebujemy czy toomake się, że modelu hello są przekazywane z funkcjami aktualne dane. Oznacza to, że hello nowo zebranych danych pierwotnych jest stale pozyskanych, przetwarzane i przekształceniu hello wymagany zestaw na powitania model, który został utworzony funkcji. At hello sama godzina, firma Microsoft ma toomake hello prognozowanych dostępnych danych dla hello kończyć odbierającą klientów. Hello poniższym diagramie przedstawiono przykład danych cyklu przepływu (lub potoku danych):

![Zapotrzebowania na energię prognozy tooEnd zakończenia przepływu danych](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

Są to hello kroki, które w ramach cyklu prognozy hello energii żądanie:

1. Miliony wdrożonej danych liczników stale generują dane dotyczące zużycia energii w czasie rzeczywistym.
2. Te dane są zbierane i przekazane do repozytorium chmury (*np.*, obiektów Blob platformy Azure).
3. Przed przetworzeniem, hello nieprzetworzone dane jest podstacji zagregowane tooa lub regionalnym zdefiniowane przez hello biznesowych.
4. Witaj funkcji przetwarzania (zobacz **Przygotowanie danych i przetwarzania funkcja**) ma miejsce i tworzy hello danych, które są wymagane do modelu uczenia lub oceniania — Witaj funkcji zestawu dane są przechowywane w bazie danych (*np.*, SQL Azure).
5. Witaj ponownie szkolenia usługi jest wywoływany hello toore train model — zaktualizowanej wersji hello modelu prognozowania jest trwały, dzięki czemu mogą służyć przez hello oceniania usługi sieci web.
6. harmonogram, który pasuje do prognozowania częstotliwość hello wymagane jest wywoływana Hello oceniania usługi sieci web.
7. Witaj prognozowanych się, że dane są przechowywane w bazie danych, którego mogą uzyskać dostęp przez hello zakończenia przez klienta.
8. powitania klienta zużycie pobiera hello prognoz, stosuje je do siatki hello i wykorzystuje ona zgodnie z przypadek użycia hello wymagane.

Jest ważne toonote, że cały cykl jest w pełni zautomatyzowany i uruchamia zgodnie z harmonogramem. Hello aranżacji całego cyklu danych może odbywać się za pomocą narzędzi takich jak [fabryki danych Azure](http://azure.microsoft.com/services/data-factory/).

### <a name="end-tooend-deployment-architecture"></a>Zakończenie tooEnd architektura wdrażania
W kolejności toopractically wdrożyć rozwiązanie prognozy żądanie energii na funkcję Cortana Intelligence, potrzebujemy tooensure czy hello wymagane składniki są połączenia i poprawnie skonfigurowana.

Witaj poniższym diagramie przedstawiono typowe architektura Cortana Intelligence na podstawie, które implementuje i organizuje hello cykl przepływu danych, opisanej powyżej:

![Zakończenie tooEnd architektura wdrażania](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

Aby uzyskać więcej informacji o poszczególnych składników hello i hello całej architektury można znaleźć toohello szablon rozwiązania energii.

