---
title: "algorytmów uczenia maszynowego toochoose aaaHow | Dokumentacja firmy Microsoft"
description: "Jak toochoose Azure Machine Learning algorytmów uczenie nadzorowane i nienadzorowane klastrów, klasyfikacji lub regresji eksperymentów."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a3b23d7f-f083-49c4-b6b1-3911cd69f1b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/25/2017
ms.author: garye
ms.openlocfilehash: 367b2278acc2435f27f9d24ead8199db58aca283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-algorithms-for-microsoft-azure-machine-learning"></a>Jak toochoose algorytmów uczenia maszynowego Microsoft Azure
Witaj odpowiedzi na pytanie toohello "jakie machine learning algorithm należy używać?" jest zawsze "Zależy." To zależy od rozmiaru hello, jakości i rodzaj hello danych. Co chcesz dodać toodo hello odpowiedzi. To zależy od sposobu matematyczne hello algorytmu hello został przetłumaczyć instrukcje dotyczące komputera hello, którego używasz. I jest ono zależne na czas, jaki ma. Nawet najbardziej wystąpił hello do analityków danych nie wiadomo, który algorytm będzie wykonywać najlepiej przed podjęciem próby je.

## <a name="hello-machine-learning-algorithm-cheat-sheet"></a>Witaj maszyny Learning Algorithm Cheat arkusza
Witaj **Microsoft Azure Machine Learning algorytmu Cheat arkusza** pomaga wybrać prawa hello komputera Algorytm uczenia dla rozwiązań analizy predykcyjnej z biblioteki Microsoft Azure Machine Learning hello algorytmów.
W tym artykule przedstawiono sposób toouse go.

> [!NOTE]
> Arkusz ze wskazówkami dotyczącymi hello toodownload i wykonaj, wraz z tym artykułem go za[Machine learning arkusz ze wskazówkami dotyczącymi algorytmu dla programu Microsoft Azure Machine Learning Studio](machine-learning-algorithm-cheat-sheet.md).
> 
> 

Ten arkusz ze wskazówkami dotyczącymi ma odbiorców bardzo na uwadze: początku danych naukowca przy użyciu poziomu Absolwenci bez tytułu machine learning, w trakcie toochoose toostart algorytmu o w usłudze Azure Machine Learning Studio. Oznacza to ułatwia niektóre generalizacji i oversimplifications, że jego punktów w kierunku bezpieczne. Oznacza to również, że istnieje wiele algorytmów niewymienione w tym miejscu. Wraz z usługi Azure Machine Learning rozwojem tooencompass bardziej szczegółowy zestaw dostępnych metod, dodamy je.

Te zalecenia są skompilowane opinii i porad z wielu analityków danych, a machine learning ekspertów. Nie możemy zaakceptować wszystkie, ale podejmowano tooharmonize opinie naszych do nierównej konsensu. Większość instrukcji hello zastrzeżeń rozpoczynać się od "Zależy..."

### <a name="how-toouse-hello-cheat-sheet"></a>Jak ściągawka toouse hello
Przeczytaj hello ścieżkę i algorytmu etykiet na wykresie hello jako "dla  *&lt;etykieta ścieżki&gt;*, użyj  *&lt;algorytm&gt;*." Na przykład "dla *szybkości*, użyj *dwie klasy Regresja logistyczna*." Czasami więcej niż jedna gałąź ma zastosowanie.
Czasami żaden z nich nie jest dokładne dopasowanie. One jest zamierzone toobe reguły z thumb zalecenia, więc nie martw się o dokładnie.
Kilka analityków danych I zawsze mówię z powiedział tego hello tylko się, że sposób znaleźć algorytmu bardzo najlepsze hello jest tootry wszystkich z nich.

Oto przykład z hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) eksperymentu, która próbuje kilka algorytmów przed hello tych samych danych i porównuje hello wyniki: [porównania klasyfikatory wielu klas: list rozpoznawania ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

> [!TIP]
> toodownload i Drukuj diagram, który zawiera omówienie funkcji hello usługi Machine Learning Studio, zobacz [diagram przeglądowy możliwości usługi Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
> 
> 

## <a name="flavors-of-machine-learning"></a>Odmian uczenia maszynowego
### <a name="supervised"></a>Nadzorowane
Algorytmy uczenia nadzorowanego tworzenia prognoz na podstawie zestawu przykładów. Na przykład historycznych giełdowych może być używane toohazard prób w przyszłości. Każdy przykład używany do trenowania etykietą hello wartości istotnej — w takim przypadku hello giełdowy. Algorytm uczenia nadzorowanego wyszukuje wzorce w etykiety tych wartości. Można używać żadnych informacji, które mogą być użyteczne — hello dzień tygodnia hello, sezonu hello, danych finansowych firmy hello, typ hello branży, obecności hello destrukcyjne zdarzeń geograficznymi — oraz każdy algorytm szuka różnego rodzaju wzorce. Po znaleziono algorytm hello hello wzorzec najlepsze może używa czy wzorzec toomake prognoz dotyczących bez etykiety danych testowych — ceny w przyszłości.

Uczenia nadzorowanego jest typem popularnych i przydatne uczenia maszynowego. Z jednym wyjątkiem wszystkie moduły hello w usłudze Azure Machine Learning są uczenia nadzorowanego algorytmów. Istnieje kilka określonych typów uczenia nadzorowanego, które są przedstawiane w ramach usługi Azure Machine Learning: wykrywania anomalii, klasyfikacji i regresji.

* **Klasyfikacja**. Dane hello są używane toopredict kategorii, uczenia nadzorowanego jest również nazywany klasyfikacji. Dotyczy hello podczas przypisywania obrazu jako obraz "kot" lub "dog". Gdy istnieją tylko dwa wybory, jest nazywany **dwuklasowych** lub **dwumianu klasyfikacji**. Jeśli ma więcej kategorii jako podczas przewidywania wygrał hello użytkownik z turnieju NCAA marca Madness hello, ten problem jest nazywany **klasyfikacji wielu klasy**.
* **Regresja**. Gdy jest on przewidzieć wartości podobnie jak w przypadku giełdowych, uczenia nadzorowanego nosi nazwę regresji.
* **Wykrywanie anomalii**. Czasami hello celem jest tooidentify punktów danych, które są po prostu niezwykłe. W wykrywaniu oszukańczych transakcji na przykład wszystkie wzorce wydatków wyjątkowa karty kredytowej są podejrzane. ewentualne zmiany Hello są tak wiele i hello przykłady szkolenia tak kilka, jest toolearn nie jest możliwe jakie działanie fałszywych wygląda następująco. Podejście, które przyjmuje wykrywania anomalii jest toosimply Dowiedz się, jakie normalne działanie wygląda (przy użyciu transakcji fałszywych historii) i zidentyfikować wszystko, co znacznie różni się.

### <a name="unsupervised"></a>Nienadzorowane
Uczenie nienadzorowane punktów danych, musi bez etykiet skojarzonych z nimi. Zamiast tego celem hello nienadzorowanych uczenia się, że algorytm jest organizowania danych hello w niektórych toodescribe lub sposób jego struktury. Oznacza to, grupowanie go w klastrach lub znajdowania różne sposoby patrzeć dane złożone, aby był wyświetlany prostszy i bardziej zorganizowany.

### <a name="reinforcement-learning"></a>Wzmocnienie learning
W uczeniu wzmocnienie algorytm hello pobiera toochoose akcji w punkcie danych tooeach odpowiedzi. Algorytm uczenia Hello również odbiera sygnał osób trzecich, to chwilę później, wskazującą, jaka hello decyzji.
Oparte na to, algorytm hello modyfikuje jego strategii w kolejności tooachieve hello najwyższy osób trzecich. Obecnie nie ma żadnych wzmocnienie learning algorithm moduły w usłudze Azure Machine Learning. Wzmocnienie learning jest typowe w przypadku robotics, gdzie hello zbiór odczyty czujników w jednym punkcie w czasie jest punkt danych, a algorytm hello należy wybrać robota hello następnej akcji. Jest to również fizyczną nadające się do Internet rzeczy aplikacji.

## <a name="considerations-when-choosing-an-algorithm"></a>Zagadnienia dotyczące wybierania algorytmów
### <a name="accuracy"></a>Dokładność
Uzyskiwanie odpowiedzi najdokładniejszych hello możliwe nie zawsze jest konieczne.
Czasami zbliżenia jest odpowiednia, w zależności od tego, co ma być używany dla. Jeśli to przypadek hello, może być możliwe toocut znacznie przez spełni więcej metod przybliżonej czasu przetwarzania. Inną zaletą więcej metod przybliżonej jest, że naturalnie charakteryzują się uniknąć [overfitting](https://youtu.be/DQWI1kvmwRg).

### <a name="training-time"></a>Czas szkolenia
Witaj liczbę minut lub godziny niezbędne tootrain modelu zmienia się znacznie między algorytmów. Uczenie czasu jest często ściśle związany dokładność — jeden zwykle dołączony hello innych. Ponadto niektóre algorytmy są bardziej poufnego toohello liczby punktów danych niż inne.
Gdy czas jest ograniczona można dysku hello wybór algorytmu, szczególnie w przypadku hello zestaw danych jest duży.

### <a name="linearity"></a>Liniowości
Wiele algorytmów uczenia maszynowego, należy użyć liniowości. Algorytmy liniowej klasyfikacji założono, że klasy mogą być oddzielone prostej (lub jej wielowymiarowego analogowy). Te obejmują Regresja logistyczna i obsługuje wektor maszyny (zgodnie z implementacją w usłudze Azure Machine Learning).
Algorytmy regresji liniowej przyjęto założenie, skorzystaj z prostej trendów w danych. Te wartości domyślne nie są nieprawidłowe dla niektórych problemów, ale na innych dokładność one Przenieś w dół.

![Klasa inne niż liniowy granic][1]

***Granicą liniową inne niż klasa*** *-zależne algorytm klasyfikacji liniowej spowodowałoby niski dokładności*

![Dane z rożne trend][2]

***Dane z rożne trend*** *— za pomocą metody regresji liniowej wygenerowanie dużo błędów większe niż to konieczne*

Niezależnie od ich zagrożenia liniowej algorytmy są bardzo popularny jako pierwszy wiersz ataku. Często toobe algorithmically proste i szybkie do uczenia.

### <a name="number-of-parameters"></a>Liczba parametrów
Parametry są pokrętła hello naukowca danych pobiera tooturn podczas konfigurowania algorytmu. Są one numery, które mają wpływ na zachowanie hello algorytmu, takie jak błąd uszkodzenia lub liczby iteracji lub opcji między wariantów zachowania hello algorytmu. czasu szkoleń Hello i dokładność algorytmu hello czasami mogą być bardzo poufne toogetting hello tylko odpowiednich ustawień. Zwykle algorytmów z dużą liczbą parametrów wymagają hello najbardziej wersji próbnej i toofind błąd dobre połączenie.

Alternatywnie istnieje [kominów parametru](machine-learning-algorithm-parameters-optimize.md) blok modułu z usługi Azure Machine Learning, która automatycznie podejmie wszystkie kombinacje parametrów o dowolnym możesz wybrać. Jest to doskonały sposób toomake się, że zostały objęte hello parametr miejsca, tootrain czas hello modelu zwiększa wykładniczo hello liczby parametrów.

Witaj Odwróć jest czy mających wiele parametrów zwykle oznacza, że algorytm ma większą elastyczność. Często można uzyskać bardzo dobre dokładności. Pod warunkiem, że można znaleźć odpowiednie połączenie hello ustawienia parametru.

### <a name="number-of-features"></a>Wiele funkcji
Dla niektórych typów danych hello liczbę funkcji może być bardzo duże toohello porównaniu liczby punktów danych. Jest to często hello z genetyka lub danych tekstowych. Witaj dużą liczbę funkcji można bog dół niektórych algorytmów uczenia, co szkolenia czasu unfeasibly długo. Maszyny wektor pomocy technicznej są szczególnie dobrze nadają się toothis przypadku (patrz poniżej).

### <a name="special-cases"></a>Specjalne przypadki
Niektóre algorytmów uczenia zakładają określonego hello struktury danych hello lub hello potrzeby wyników. Jeśli znajdziesz taki, który odpowiada potrzebom użytkownika, jego możesz nadać bardziej przydatne wyniki, dokładniejszych prognoz lub szybsze szkolenia.

| **Algorytm** | **Dokładność** | **Czas szkolenia** | **Liniowości** | **Parametry** | **Uwagi** |
| --- |:---:|:---:|:---:|:---:| --- |
| **Klasyfikacja dwa — klasa** | | | | | |
| [Regresja logistyczna](https://msdn.microsoft.com/library/azure/dn905994.aspx) | |● |● |5 | |
| [decyzja lasu](https://msdn.microsoft.com/library/azure/dn906008.aspx) |● |○ | |6 | |
| [Dżungla decyzji](https://msdn.microsoft.com/library/azure/dn905976.aspx) |● |○ | |6 |Mało pamięci |
| [drzewo decyzyjne boosted](https://msdn.microsoft.com/library/azure/dn906025.aspx) |● |○ | |6 |Zużycie pamięci |
| [sieć neuronowa](https://msdn.microsoft.com/library/azure/dn905947.aspx) |● | | |9 |[Możliwe jest dodatkowe dostosowanie](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [perceptron uśrednionej](https://msdn.microsoft.com/library/azure/dn906036.aspx) |○ |○ |● |4 | |
| [Obsługa maszyny wektora](https://msdn.microsoft.com/library/azure/dn905835.aspx) | |○ |● |5 |Nadaje się do funkcji dużych zestawów |
| [Obsługa lokalnie głębokie wektor maszyny](https://msdn.microsoft.com/library/azure/dn913070.aspx) |○ | | |8 |Nadaje się do funkcji dużych zestawów |
| [Maszyna punktu Bayesa](https://msdn.microsoft.com/library/azure/dn905930.aspx) | |○ |● |3 | |
| **Klasa usługi klasyfikacji** | | | | | |
| [Regresja logistyczna](https://msdn.microsoft.com/library/azure/dn905853.aspx) | |● |● |5 | |
| [decyzja lasu](https://msdn.microsoft.com/library/azure/dn906015.aspx) |● |○ | |6 | |
| [Dżungla decyzji](https://msdn.microsoft.com/library/azure/dn905963.aspx) |● |○ | |6 |Mało pamięci |
| [sieć neuronowa](https://msdn.microsoft.com/library/azure/dn906030.aspx) |● | | |9 |[Możliwe jest dodatkowe dostosowanie](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [jedna v wszystkie](https://msdn.microsoft.com/library/azure/dn905887.aspx) |- |- |- |- |Wyświetlić właściwości wybranej metody dwuklasowych hello |
| **Regresja** | | | | | |
| [liniowy](https://msdn.microsoft.com/library/azure/dn905978.aspx) | |● |● |4 | |
| [Estymacja Bayesian liniowy](https://msdn.microsoft.com/library/azure/dn906022.aspx) | |○ |● |2 | |
| [decyzja lasu](https://msdn.microsoft.com/library/azure/dn905862.aspx) |● |○ | |6 | |
| [drzewo decyzyjne boosted](https://msdn.microsoft.com/library/azure/dn905801.aspx) |● |○ | |5 |Zużycie pamięci |
| [kwantyl szybkiego lasu](https://msdn.microsoft.com/library/azure/dn913093.aspx) |● |○ | |9 |Zamiast prognoz punktu dystrybucji |
| [sieć neuronowa](https://msdn.microsoft.com/library/azure/dn905924.aspx) |● | | |9 |[Możliwe jest dodatkowe dostosowanie](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [Poissona](https://msdn.microsoft.com/library/azure/dn905988.aspx) | | |● |5 |Technicznie dziennika liniowej. Do przewidywania liczby |
| [{numer porządkowy](https://msdn.microsoft.com/library/azure/dn906029.aspx) | | | |0 |Do przewidywania porządkowanie ranga |
| **Wykrywanie anomalii** | | | | | |
| [Obsługa maszyny wektora](https://msdn.microsoft.com/library/azure/dn913103.aspx) |○ |○ | |2 |Szczególnie przydatne dla funkcji dużych zestawów |
| [Wykrywanie anomalii oparte na PCA](https://msdn.microsoft.com/library/azure/dn913102.aspx) | |○ |● |3 | |
| [K-średnich](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/) | |○ |● |4 |Algorytm klastrowanie |

**Właściwości algorytmu:**

**●** -pokazuje znakomity dokładność, szkolenia szybkiego godziny i użyj hello liniowości

**(○)** — przedstawia dobrą dokładność i czasy umiarkowane szkolenia

## <a name="algorithm-notes"></a>Uwagi dotyczące algorytmu
### <a name="linear-regression"></a>Regresja liniowa
Jak wspomniano wcześniej, [regresji liniowej](https://msdn.microsoft.com/library/azure/dn905978.aspx) pasuje do zestawu danych wiersza (lub płaszczyzny lub hyperplane) toohello. Jest najważniejszą metodą roboczą, proste i szybkie, ale może być nadmiernie simplistic dla niektórych problemów.
Wyszukaj tutaj [samouczek regresji liniowej](machine-learning-linear-regression-in-azure.md).

![Dane z trendu liniowego][3]

***Dane z trendu liniowego***

### <a name="logistic-regression"></a>Regresja logistyczna
Chociaż zawiera złudzenia "regresji" w nazwie hello, Regresja logistyczna jest rzeczywiście zaawansowane narzędzie [dwuklasowych](https://msdn.microsoft.com/library/azure/dn905994.aspx) i [multiklasa](https://msdn.microsoft.com/library/azure/dn905853.aspx) klasyfikacji. To szybki i prosty. Witaj fakt, że używa w "-kształcie krzywej zamiast prostej ułatwia fizycznych dopasowanie rozdzielania danych w grupach. Regresja logistyczna zapewnia liniowej klasy granice, więc gdy jest używany, upewnij się, że liniowej zbliżenia się coś, co może współdziałać z.

![Regresja logistyczna tootwo klasy danych za pomocą tylko jednej funkcji][4]

***Regresja logistyczna klasy tootwo dane z tylko jedną funkcję*** *-granic klasy jest punkt hello, w których hello logistyczna krzywej jest po prostu jako Zamknij klasy tooboth*

### <a name="trees-forests-and-jungles"></a>Drzewa, lasów i dżungle
Decyzja lasów ([regresji](https://msdn.microsoft.com/library/azure/dn905862.aspx), [dwuklasowych](https://msdn.microsoft.com/library/azure/dn906008.aspx), i [multiklasa](https://msdn.microsoft.com/library/azure/dn906015.aspx)), decyzja dżungle ([dwuklasowych](https://msdn.microsoft.com/library/azure/dn905976.aspx) i [ multiklasa](https://msdn.microsoft.com/library/azure/dn905963.aspx)), a boosted drzew decyzyjnych ([regresji](https://msdn.microsoft.com/library/azure/dn905801.aspx) i [dwuklasowych](https://msdn.microsoft.com/library/azure/dn906025.aspx)) są wszystkie na podstawie drzew decyzyjnych, maszynę podstawowych koncepcji learning. Istnieje wiele odmian drzew decyzyjnych, ale wszystkie one tak samo postąpić — podzielić hello funkcji miejsca w regionach przede wszystkim hello samą etykietę. Mogą to być regionów spójne kategorii lub stałą wartość, w zależności od tego, czy podczas klasyfikacji lub regresji.

![Drzewo decyzyjne dzieli obszar funkcji][5]

***Drzewo decyzyjne dzieli miejsca funkcji w regionach około uniform wartości***

Ponieważ miejsca funkcji można podzielić na arbitralnie małych regionów, jest łatwe tooimagine podzielenie go precyzyjne za mało toohave jednego punktu danych na region. Jest to przykład extreme overfitting. W kolejności tooavoid to duży zbiór drzew opracowano przy szczególną matematyczne podjęte nie skorelowanych hello drzewa. Średnia Hello tego "lasu decyzji" jest drzewa, który pozwala uniknąć overfitting. Lasy decyzji mogą za pomocą dużej ilości pamięci. Dżungle decyzyjne są variant, który zużywa mniej pamięci na powitania koszt nieznacznie dłuższy czas szkolenia.

Drzewa decyzyjne boosted uniknąć overfitting poprzez ograniczenie, ile razy można podzielić one i jak najmniejszej liczby punktów danych są dozwolone w każdym regionie. Algorytm tworzy sekwencję drzew, z których każdy uzyskuje informacje o kompensacji błąd hello w drzewie hello przed. wynik Hello jest bardzo dokładne uczeń, który zwykle toouse dużej ilości pamięci. Dla hello pełny opis techniczny, zapoznaj się z [Friedman w oryginalnym papieru](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf).

[Szybkie regresji kwantyl lasu](https://msdn.microsoft.com/library/azure/dn913093.aspx) jest odmianą drzew decyzyjnych dla szczególnych przypadkach hello, którym chcesz wiedzieć, nie tylko hello typowe () wartość mediany hello danych w regionie, ale jej dystrybucji w postaci hello quantiles.

### <a name="neural-networks-and-perceptrons"></a>Sieci neuronowe i perceptrons
Sieci neuronowe są inteligencji inspirowana obejmujące algorytmów uczenia [multiklasa](https://msdn.microsoft.com/library/azure/dn906030.aspx), [dwuklasowych](https://msdn.microsoft.com/library/azure/dn905947.aspx), i [regresji](https://msdn.microsoft.com/library/azure/dn905924.aspx) problemów. Pochodzą nieskończone różne, ale hello sieci neuronowe w usłudze Azure Machine Learning są wszystkie hello formę ukierunkowanego wykresu acyklicznego.. Oznacza to, że wejściowy funkcji są przekazywane do przodu (nigdy nie wstecz) sekwencję warstwy przed są przekształcane w danych wyjściowych. W każdej warstwie danych wejściowych ważone są w różnych kombinacjach, sumowane i przekazywane do następnej warstwy hello. Ta kombinacja prostych obliczeń powoduje toolearn możliwości zaawansowane trendów granic i danych klasy pozornie przez magic. Wielu warstw sieci tego rodzaju wykonać hello "głębokiego learning", który paliwa wiele technologii raportowania i fikcja nauki.

Ten wysokiej wydajności nie zawiera bezpłatnie, ale. Sieci neuronowe może zająć tootrain długo, szczególnie w przypadku dużych zestawów danych z dużą ilością funkcji. Mają one również więcej parametrów niż większość algorytmy, które oznacza, że parametr kominów znacznie rozszerza hello szkolenia czasu.
I dla tych overachievers, którzy chcą zbyt[określić własne struktury sieci](http://go.microsoft.com/fwlink/?LinkId=402867), możliwości są inexhaustible.

![Granice rozpoznawane przez sieci neuronowe][6]
***granice hello rozpoznawane przez sieci neuronowe może być złożona i nieregularne***

Witaj [dwuklasowych średnio perceptron](https://msdn.microsoft.com/library/azure/dn906036.aspx) jest sieci neuronowe odpowiedzi tooskyrocketing szkolenia razy. Struktura sieci, która zapewnia granice liniowej klasy jest używany. Jest prawie pierwotnych przez obecnie standardów, ale ma ona długą historię pracy niezawodnie i duże toolearn szybko.

### <a name="svms"></a>SVMs
Obsługa wektor maszyny (SVMs) odnaleźć granic hello oddziela klasy przez jako szeroki margines, jak to możliwe. Gdy Witaj dwie klasy nie może być wyraźnie oddzielone, algorytmy hello znaleźć hello najlepsze granicę, którą mogą. Podczas zapisywania w usłudze Azure Machine Learning, hello [SVM dwuklasowych](https://msdn.microsoft.com/library/azure/dn905835.aspx) robi to tylko prosta linia. (W SVM mowy używa on liniowej jądra). Ponieważ pozwala to zbliżenia liniowego, jest możliwe toorun stosunkowo szybko. Gdzie naprawdę źródło jest za pomocą funkcji intensywny danych, takich jak tekst lub genomicznej. W takich przypadkach SVMs są klasy tooseparate mogli szybciej i z mniej overfitting niż większość inne algorytmy dodatkowo toorequiring niewielkie ilości pamięci.

![Wektor granicę klasy pomocy technicznej][7]

***Granicę techniczną wektor maszyny klasy maksymalizuje hello margin oddzielenie dwie klasy***

Innego produktu programu Microsoft Research hello [SVM lokalnie głębokie dwuklasowych](https://msdn.microsoft.com/library/azure/dn913070.aspx) jest-liniowej wariant SVM, który zachowuje większość hello szybkość i pamięci wydajności hello liniowej wersji. Jest idealny dla przypadków, w którym podejście liniowej hello nie zapewnia wystarczająco dokładne odpowiedzi. Deweloperzy Hello przechowywane fast dzieląc hello problem do licznych drobne problemy SVM liniowej. Witaj odczytu [pełny opis](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf) hello szczegółowe informacje na temat sposobu pobierane poza ta procedura.

Przy użyciu inteligentne rozszerzenie rożne SVMs, hello [SVM jednej klasy](https://msdn.microsoft.com/library/azure/dn913103.aspx) rysuje obramowanie ściśle przedstawiono hello cały zestaw danych. Jest to przydatne w przypadku wykrywania anomalii. Wszystkie nowe punkty danych należących do tej pory poza tę granicę są wystarczająco nietypowe toobe warte wymienienia.

### <a name="bayesian-methods"></a>Metody Estymacja Bayesian
Metody Estymacja Bayesian mają pożądane wysokiej jakości: eliminują overfitting. One to robić przez założenie wcześniej informacji o hello prawdopodobnie dystrybucji hello odpowiedzi. Inny byproduct tego podejścia jest, że bardzo mało parametrów. Usługa Azure Machine Learning zawiera oba algorytmy Estymacja Bayesian zarówno klasyfikacji ([maszyna punktu Bayesa Two-class](https://msdn.microsoft.com/library/azure/dn905930.aspx)) i regresji ([regresji liniowej Estymacja Bayesian](https://msdn.microsoft.com/library/azure/dn906022.aspx)).
Należy pamiętać, że te wniosku, że dane hello można podzielić lub dopasowania z prostej.

Na notatkę historycznych maszyny punktu Bayesa zostały opracowane w Microsoft Research. Mają one niektóre wyjątkowo doskonałych Praca teoretyczna za nimi. uczniów zainteresowanych Hello jest bezpośrednie toohello [oryginalny artykuł w JMLR](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf) i [interesującego blogu przez Bishop Krzysztof](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx).

### <a name="specialized-algorithms"></a>Algorytmy specjalne
Jeśli masz bardzo określonego celu, który może być szczęście. W ramach hello kolekcji usługi Azure Machine Learning istnieją algorytmów specialize w:

- Rank — prognozowania ([Regresja porządkowa](https://msdn.microsoft.com/library/azure/dn906029.aspx)),
- Liczba prognozowania ([regresji Poissona](https://msdn.microsoft.com/library/azure/dn905988.aspx)),
- wykrywanie anomalii (jedną na podstawie [analizy głównych składników](https://msdn.microsoft.com/library/azure/dn913102.aspx) i jeden na podstawie [maszyny wektorowa obsługa](https://msdn.microsoft.com/library/azure/dn913103.aspx)s)
- klaster ([K-średnich](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/))

![Wykrywanie anomalii oparte na PCA][8]

***Wykrywanie anomalii oparte na PCA*** *-hello większość danych hello należące do dystrybucji stereotypical; punkty różniących się znacząco od dystrybucji są podejrzane*

![Zestaw danych zgrupowane za pomocą K-średnich][9]

***Zestaw danych są grupowane w pięciu klastrów za pomocą K-średnich***

Istnieje również zespół [wieloklasowej klasyfikatora jedna v wszystkie](https://msdn.microsoft.com/library/azure/dn905887.aspx), jaki problem podziały hello klasy N klasyfikacji do N-1 dwuklasowych klasyfikacji problemów. dokładność Hello, czas szkolenia i właściwości liniowości są określane przez klasyfikatory dwuklasowych hello używane.

![Klasyfikatory dwuklasowych łączyć tooform klasyfikatora trzech — klasa][10]

***Para klasyfikatory dwuklasowych połączyć tooform klasyfikatora trzech — klasa***

Azure Machine Learning obejmuje również dostęp do uczenia maszynowego zaawansowanych tooa framework pod tytułem hello [Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf).
VW powinny kategoryzacji, ponieważ mogą dowiedzieć się, zarówno klasyfikacji i regresji problemów, a nawet można uzyskać z częściowo bez etykiety danych. Można go skonfigurować toouse jedno liczby szkoleniowe dotyczące algorytmów, funkcje utraty i algorytmy optymalizacji. Została zaprojektowana z hello tła się toobe wydajne, równoległe i bardzo szybkiego działania. Obsługuje on funkcji było bardzo dużych zestawów przy minimalnym nakładzie pracy oczywista.
Uruchomiona i przez Microsoft Research jego własnej Jan Langford, VW jest formuła jednego wpisu w polu algorytmów samochodu zapasów. Nie każdy problem pasujące VW, ale jeśli nie należy do Ciebie, może być zdobycie tooclimb naukę na interfejsie. Jest również dostępny jako [kod autonomicznej typu open source](https://github.com/JohnLangford/vowpal_wabbit) w wielu językach.

## <a name="more-help-with-algorithms"></a>Więcej informacji o algorytmy
* Aby infographic do pobrania, opisujący algorytmów i przykłady, zobacz [Infographic do pobrania: Machine learning podstawy wraz z przykładami algorytmu](machine-learning-basics-infographic-with-algorithm-examples.md).
* Aby uzyskać listę według kategorii algorytmów uczenia maszynowego hello wszystkie dostępne w usłudze Azure Machine Learning Studio, zobacz [zainicjować modelu] [ initialize-model] hello Machine Learning Studio algorytmu i pomóc w Module.
* Aby uzyskać alfabetyczną listę wszystkich algorytmów i modułów w usłudze Azure Machine Learning Studio, zobacz [A — Z listy modułów usługi Machine Learning Studio] [ a-z-list] algorytmu Studio uczenia maszynowego i pomóc w Module.
* toodownload i Drukuj diagram, który zawiera omówienie funkcji hello usługi Azure Machine Learning Studio, zobacz [diagram przeglądowy możliwości usługi Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).


<!-- Reference links -->
[initialize-model]: https://msdn.microsoft.com/library/azure/dn905812.aspx
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx

<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
