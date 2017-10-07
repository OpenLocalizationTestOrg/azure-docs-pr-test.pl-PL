---
title: wyniki modelu aaaInterpret w uczeniu maszynowym | Dokumentacja firmy Microsoft
description: "Parametr optymalne hello toochoose konfiguracji dla algorytmu przy użyciu i wizualizacja danych wyjściowych modelu wynik."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a>Interpretowanie wyników modelu w usłudze Azure Machine Learning
W tym temacie opisano sposób toovisualize i interpretować wyniki prognozowania w usłudze Azure Machine Learning Studio. Po uczony model i gotowe prognoz na nim ("oceniane hello modelu") należy toounderstand i interpretować hello przewidywania wyników.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Istnieją cztery główne rodzaje modeli w usłudze Azure Machine Learning uczenia maszynowego:

* Klasyfikacja
* Klaster
* Regresja
* Systemy polecania

Moduły Hello używane do prognozowania na podstawie tych modeli są:

* [Score Model] [ score-model] modułu dla klasyfikacji i regresji
* [Przypisz tooClusters] [ assign-to-clusters] modułu do klastrowania
* [Wynik polecania Matchbox] [ score-matchbox-recommender] dla systemów zalecenia

W tym dokumencie opisano, jak toointerpret przewidywania wyników dla każdego z tych modułów. Omówienie tych modułów, zobacz [jak toooptimize parametry toochoose algorytmy w usłudze Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).

Ten temat dotyczy interpretacji prognozowania, ale nie oceny modelu. Aby uzyskać więcej informacji o tym, jak tooevaluate modelu, zobacz [jak tooevaluate modelu wydajności w usłudze Azure Machine Learning](machine-learning-evaluate-model-performance.md).

Jeśli się nowych tooAzure uczenia maszynowego i potrzebujesz pomocy, tworzenie tooget prostego eksperymentu, pracy, zobacz [Tworzenie prostego eksperymentu w usłudze Azure Machine Learning Studio](machine-learning-create-experiment.md) w usłudze Azure Machine Learning Studio.

## <a name="classification"></a>Klasyfikacja
Istnieją dwie podkategorie klasyfikacji problemów:

* Problemy z klasami tylko dwa (Klasyfikacja dwuklasowych lub binarny)
* Problemy z więcej niż dwóch klas (Klasyfikacja wielu klas)

Usługa Azure Machine Learning ma toodeal różnych modułach z każdym z tych typów klasyfikacji, ale metody hello interpretowanie ich wyniki prognozowania są podobne.

### <a name="two-class-classification"></a>Klasyfikacja dwa — klasa
**Przykład eksperymentu**

Przykład problemu klasyfikacji dwuklasowych to klasyfikacji hello kwiatów iris. zadanie Hello jest kwiatów iris tooclassify na podstawie ich funkcji. Hello Iris zestaw danych dostępnych w usłudze Azure Machine Learning jest podzbiorem hello popularnych [zestawu danych Iris](http://en.wikipedia.org/wiki/Iris_flower_data_set) zawierający wystąpień tylko dwa kwiaty określa (klasy 0 i 1). Istnieją cztery funkcje dla każdego kwiat (długość sepal, szerokość sepal Motyw Płatek długości i szerokości Motyw Płatek).

![Zrzut ekranu przedstawiający iris eksperymentu](./media/machine-learning-interpret-model-results/1.png)

Rysunek 1. Iris dwuklasowych klasyfikacji problemu eksperymentu

Eksperyment został wykonywane toosolve ten problem, jak pokazano na rysunku 1. Model drzewa decyzji boosted dwuklasowych został uczenia i oceny. Teraz można zwizualizować wyniki prognozowania hello hello [Score Model] [ score-model] modułu, klikając portem wyjściowym hello hello [Score Model] [ score-model]modułu, a następnie klikając pozycję **Visualize**.

![Moduł score model](./media/machine-learning-interpret-model-results/1_1.png)

Spowoduje to wyświetlenie hello oceniania wyniki, jak pokazano na rysunku 2.

![Wyniki iris doświadczenia klasyfikacji dwa — klasa](./media/machine-learning-interpret-model-results/2.png)

Rysunek 2. Wizualizuj wynik score model klasyfikacji dwa — klasa

**Interpretacja wyników**

Brak sześć kolumn w tabeli wyników hello. po lewej stronie cztery kolumny Hello są funkcje cztery hello. Hello prawo dwie kolumny, etykiety oceniane i oceniane prawdopodobieństwa są wyniki prognozowania hello. Witaj wynik prawdopodobieństwa kolumny pokazuje hello prawdopodobieństwo że kwiatu należy toohello klasy dodatnią (Klasa 1). Na przykład Witaj pierwszy numer hello kolumny (0.028571) oznacza, że istnieje 0.028571 prawdopodobieństwo, że hello pierwszy kwiat należy tooClass 1. Hello oceniane etykiety kolumn pokazuje hello przewidzieć klasy dla każdego kwiat. To jest oparta na powitania wynik prawdopodobieństwa kolumny. Jeśli wynik prawdopodobieństwa kwiatu hello jest większy niż 0,5, jest obliczana jako klasy 1. W przeciwnym razie wartość jest obliczana jako klasa 0.

**Publikowania usług sieci Web**

Po uwzględnione wyniki prognozowania hello i ocenić dźwięku hello eksperymentu mogą być publikowane jako usługę sieci web tak, aby można go wdrożyć w różnych aplikacji i wywołać go tooobtain klasy prognoz dla nowego kwiatem iris. toolearn toochange szkoleniowego eksperymentu w eksperymencie oceniania i opublikujesz je jako usługi sieci web, zobacz [opublikować usługi sieci web Azure Machine Learning hello](machine-learning-walkthrough-5-publish-web-service.md). Ta procedura umożliwia eksperyment oceniania jak pokazano na rysunku 3.

![Zrzut ekranu przedstawiający oceniania eksperymentu](./media/machine-learning-interpret-model-results/3.png)

Rysunek 3. Ocenianie hello iris dwuklasowych klasyfikacji problemu eksperymentu

Teraz należy tooset hello wejścia i wyjścia usługi sieci web hello. Witaj dane wejściowe są hello prawy port wejściowy z [Score Model][score-model], który jest hello Iris kwiat funkcje w danych wejściowych. Witaj wybór danych wyjściowych hello zależy od tego, czy jesteś zainteresowany w hello przewidzieć klasy (etykieta scored), hello wynik prawdopodobieństwa lub oba. W tym przykładzie zakłada się, że jesteś zainteresowany zarówno w. tooselect hello potrzeby kolumn wyjściowych, użyj [Wybieranie kolumn w zestawie danych] [ select-columns] modułu. Kliknij przycisk [Wybieranie kolumn w zestawie danych][select-columns], kliknij przycisk **Uruchom selektor kolumn**i wybierz **oceniane etykiety** i **wynik prawdopodobieństwa**. Po ustawieniu portem wyjściowym hello [Wybieranie kolumn w zestawie danych] [ select-columns] i uruchomić ponownie, powinno być gotowe toopublish hello oceniania eksperymentu jako usługę sieci web, klikając **publikowanie w sieci WEB Usługa**. końcowy eksperyment Hello wygląda jak rysunek 4.

![Witaj iris klasyfikacji dwuklasowych eksperymentu](./media/machine-learning-interpret-model-results/4.png)

Rysunek 4. Końcowy eksperyment oceniania iris dwuklasowych klasyfikacji problemu

Po uruchomieniu usługi sieci web hello i wprowadź wartości niektórych funkcji wystąpienia testu, wynik hello zwraca dwóch liczb. Pierwsza liczba Hello jest hello oceniane etykiety, a hello jest drugi hello wynik prawdopodobieństwa. Ta kwiat jest przewidzieć jako klasy 1 z 0.9655 prawdopodobieństwa.

![Model interpretowania wynik testu](./media/machine-learning-interpret-model-results/4_1.png)

![Ocenianie wyników testu](./media/machine-learning-interpret-model-results/5.png)

Rysunek 5. Wynik usługi sieci Web iris dwuklasowych klasyfikacji

### <a name="multi-class-classification"></a>Klasa usługi klasyfikacji
**Przykład eksperymentu**

W tym eksperymencie możesz wykonać zadania rozpoznawania litery jako przykład wieloklasowej klasyfikacji. Witaj klasyfikatora prób toopredict określony litery (klasa) na podstawie niektórych odręcznego wartości atrybutu wyodrębniony z hello odręcznego obrazów.

![Przykład rozpoznawania list](./media/machine-learning-interpret-model-results/5_1.png)

W danych szkoleniowych hello są funkcje 16 wyodrębniony z odręcznego list obrazów. Witaj 26 liter tworzą naszych 26 klasy. Zorientować się, że 6 przedstawia eksperymentu, która będzie uczenia wieloklasowej klasyfikacji modelu rozpoznawania litery i prognozowania na powitania sam funkcji zestawu na testowego zestawu danych.

![Litera rozpoznawania wieloklasowej klasyfikacji eksperymentu](./media/machine-learning-interpret-model-results/6.png)

Rysunek 6. Litera rozpoznawania wieloklasowej klasyfikacji problemu eksperymentu

Wizualizacja wyników hello hello [Score Model] [ score-model] modułu, klikając portem wyjściowym hello [Score Model] [ score-model] modułu, a następnie Kliknięcie przycisku **Visualize**, jak pokazano na rysunku 7 powinna zostać wyświetlona zawartość.

![Score model wyników](./media/machine-learning-interpret-model-results/7.png)

Rysunek 7. Wizualizacja wyników klasyfikacji modelu w klasyfikacji wielu — klasa

**Interpretacja wyników**

16 kolumn po lewej stronie powitania reprezentują wartości funkcji hello hello zestawu testów. Witaj kolumny o nazwach takich jak wynik prawdopodobieństwa dla klasy "XX" są tak samo jak hello wynik prawdopodobieństwa kolumny w przypadku dwóch klasy hello. Pokaż one hello prawdopodobieństwo, że hello odpowiadający mu wpis należące do niektórych klasy. Na przykład dla pierwszej pozycji hello istnieje 0.003571 prawdopodobieństwo, że jest "A," 0.000451 prawdopodobieństwo, że jest "B" i tak dalej. Ostatnia kolumna Hello (Scored etykiety) jest hello taki sam jak oceniane etykiet w przypadku dwóch klasy hello. Klasa hello z największą hello wynik prawdopodobieństwa jako hello przewidywanych klasy hello odpowiadający mu wpis zostanie wybrana. Na przykład dla pierwszej pozycji hello hello oceniane etykiety jest "F" ponieważ ma ona hello największy prawdopodobieństwo toobe "F" (0.916995).

**Publikowania usług sieci Web**

Można również uzyskać hello oceniane etykiety dla każdego wpisu i hello prawdopodobieństwo hello oceniane etykiety. podstawowa logika Hello jest toofind hello największy prawdopodobieństwo wśród wszystkich hello wynik prawdopodobieństwa. toodo, to należy toouse hello [wykonanie skryptu języka R] [ execute-r-script] modułu. Witaj R kodu przedstawiono na rysunku 8, a hello wynikiem eksperymentu hello jest pokazano na rysunku 9.

![Przykład kodu języka R](./media/machine-learning-interpret-model-results/8.png)

Rysunek 8. Kod języka R wyodrębniania oceniane etykiety i hello skojarzone prawdopodobieństwa hello etykiety

![Wynikiem eksperymentu](./media/machine-learning-interpret-model-results/9.png)

Rysunek 9. Końcowy eksperyment oceniania hello rozpoznawania litery wieloklasowej klasyfikacji problemu

Po opublikowaniu i uruchom usługę sieci web hello oraz wprowadzić niektóre wartości wejściowe funkcji hello zwrócił wynik prawdopodobnie rysunek 10. Ta odręcznego litera, z wyodrębnionego funkcjami 16, jest przewidywane toobe "T" z 0.9715 prawdopodobieństwa.

![Moduł interpretowania wynik testu](./media/machine-learning-interpret-model-results/9_1.png)

![Wynik testu](./media/machine-learning-interpret-model-results/10.png)

Rysunek 10. Wynik usługi sieci Web wieloklasowej klasyfikacji

## <a name="regression"></a>Regresja
Regresja problemów różnią się od klasyfikacji problemów. W klasyfikacji problemu że próbujesz toopredict odrębny klas, takich jak klasy, które kwiat iris należy do. Jednak jak widać w hello poniższy przykład problem regresji, że próbujesz toopredict zmiennej ciągłego, takich jak hello ceny samochodu.

**Przykład eksperymentu**

Używanie Prognozowanie cen samochodów jako przykład Twoje regresji. Próbujesz toopredict hello ceny samochodu oparte na jej funkcje, takie jak upewnij, typu paliwa typem treści i pokrętła stacji. Rysunek 11 pokazano Hello eksperymentu.

![Eksperymentu opartego na regresji cen samochodów](./media/machine-learning-interpret-model-results/11.png)

Rysunek 11. Cen samochodów regresji problem eksperymentu

Środek wywołujący hello [Score Model] [ score-model] modułu, wynik hello wygląda jak rysunek 12.

![Wyników oceniania problemu prognozowania cen samochodów](./media/machine-learning-interpret-model-results/12.png)

Rysunek 12. Ocenianie wyniku problemu prognozowania cen samochodów hello

**Interpretacja wyników**

Scored etykiety jest kolumną wynik hello oceniania wynik. numery Hello są hello przewidywane ceny dla każdego samochodu.

**Publikowania usług sieci Web**

Można opublikować eksperymentu opartego na regresji hello do usługi sieci web i wywołać go do prognozowania cen samochodów w hello tak samo jak Klasyfikacja dwuklasowych hello przypadek użycia.

![Ocenianie eksperymentu cen samochodów regresji problemu](./media/machine-learning-interpret-model-results/13.png)

Rysunek 13. Ocenianie eksperymentu problem regresji cen samochodów

Uruchomiona usługa sieci web hello, hello zwrócił wynik prawdopodobnie rysunku 14. Cena przewidywane Hello ten samochód jest 15,085.52 $.

![Moduł interpretowania wyników testu](./media/machine-learning-interpret-model-results/13_1.png)

![Wyników oceniania modułu](./media/machine-learning-interpret-model-results/14.png)

Rysunek 14. Wynik usługi sieci Web wystąpił problem regresji cen samochodów

## <a name="clustering"></a>Klaster
**Przykład eksperymentu**

Użyjmy hello zestawu danych Iris ponownie toobuild klastrowania eksperymentu. W tym miejscu można odfiltrować hello klasy etykiet w zestawie danych hello tak, aby tylko ma funkcje i może służyć do klastra. W tym iris przypadek użycia, określ liczbę hello klastrów toobe dwa podczas procesu szkolenia hello, co oznacza, że należy umieścić klastrze kwiatów hello na dwie klasy. eksperymentu Hello pokazano na rys. 15.

![Problem klastrowania Iris eksperymentu](./media/machine-learning-interpret-model-results/15.png)

Rysunek 15. Problem klastrowania Iris eksperymentu

Klastrowanie różni się od klasyfikacji, w tym hello szkoleniowy zestaw danych nie ma podstaw prawdy etykiety samodzielnie. Grupy klastrowania hello wystąpień zestawu danych szkoleniowych w różnych klastrach. W trakcie szkolenia hello etykiet modelu hello hello wpisy przez uczenia hello różnice między ich funkcje. Po wykonaniu tej hello uczonego modelu może służyć toofurther klasyfikowania przyszłych wpisów. Istnieją dwie części wynik hello Dbamy o w ramach klastrowania problem. Pierwsza część Hello jest etykietowania hello szkoleniowy zestaw danych i drugi hello jest klasyfikowanie nowy zestaw danych z hello trenowanego modelu.

Witaj pierwsza część wyniku hello można można zwizualizować, hello port wyjściowy w lewo klikając [Train Model klastrowanie] [ train-clustering-model] , a następnie klikając polecenie **wizualizacja**. Wizualizacja Hello przedstawiono na rysunku 16.

![Wynik klastrowania](./media/machine-learning-interpret-model-results/16.png)

Rysunek 16. Wizualizowanie klastra wynik hello szkoleniowy zestaw danych

wynik Hello hello drugiej części, nowe wpisy hello uczonego modelu klastrowania z klastra jest wyświetlana w rysunek 17.

![Wizualizowanie klastra wyników](./media/machine-learning-interpret-model-results/17.png)

Rysunek 17. Wizualizowanie klastra wyników na nowym zestawie danych

**Interpretacja wyników**

Mimo że wyniki hello Witaj dwie części jest wynikiem eksperymentu różne etapy, wyglądają hello takie same i interpretowania w hello tak samo. Witaj pierwsze cztery kolumny są funkcje. Hello ostatnia kolumna przydziałów, jest hello przewidywania wyników. Witaj Witaj wpisy przypisane przewidzieć są takie same numery toobe w hello sam klastra, oznacza to, że mają podobieństwa w jakiś sposób (odległość euklidesowa metrykę hello używa tego eksperymentu). Ponieważ określona liczba hello toobe klastrów 2 hello wpisów w przypisaniach są oznaczone 0 lub 1.

**Publikowania usług sieci Web**

Można opublikować hello klastrowanie eksperymentu w usłudze sieci web i wywołać ją dla prognoz klastrowania hello sam sposób jak w klasyfikacji dwuklasowych hello przypadek użycia.

![Ocenianie eksperymentu iris klastrowania problemu](./media/machine-learning-interpret-model-results/18.png)

Rysunek 18. Ocenianie eksperymentu iris problem klastrowania

Po uruchomieniu usługi sieci web hello hello zwrócił wynik prawdopodobnie rysunek 19. Ta kwiat jest przewidywane toobe w klastrze 0.

![Moduł oceny zinterpretować testu](./media/machine-learning-interpret-model-results/18_1.png)

![Ocenianie wynik modułu](./media/machine-learning-interpret-model-results/19.png)

Rysunek 19. Wynik usługi sieci Web iris dwuklasowych klasyfikacji

## <a name="recommender-system"></a>System polecania
**Przykład eksperymentu**

Dla systemów polecania hello restauracji zalecenie problem można użyć na przykład: można zalecić restauracji dla klientów w oparciu o historię ich klasyfikacji. dane wejściowe Hello składa się z trzech części:

* Klasyfikacje restauracji od klientów
* Dane funkcji klienta
* Dane funkcji restauracji

Istnieje kilka sposobów, możemy hello [polecania Matchbox pociągu] [ train-matchbox-recommender] modułu w usłudze Azure Machine Learning:

* Przewidywanie oceny dla określonego użytkownika i elementu
* Zaleca się tooa elementy danego użytkownika
* Znajdź użytkowników tooa pokrewne danego użytkownika
* Znajdź elementy tooa pokrewne danego elementu

Można wybrać, co ma toodo, wybierając opcję hello czterech z hello **rodzaj prognozowania polecania** menu. W tym miejscu można przeprowadzenie wszystkie cztery scenariusze.

![Matchbox polecania](./media/machine-learning-interpret-model-results/19_1.png)

Typowy eksperymentu uczenia maszynowego Azure dla systemu polecania wygląda na rysunku 20. Aby uzyskać informacje o toouse moduły polecania systemu, zobacz temat [polecania matchbox pociągu] [ train-matchbox-recommender] i [polecania matchbox wynik] [ score-matchbox-recommender].

![Polecania systemu eksperymentu](./media/machine-learning-interpret-model-results/20.png)

Rysunek 20. Polecania systemu eksperymentu

**Interpretacja wyników**

**Przewidywanie oceny dla określonego użytkownika i elementu**

Wybierając **prognozowania klasyfikacji** w obszarze **rodzaj prognozowania polecania**, są pytaniem polecania hello hello toopredict systemu klasyfikacji dla danego użytkownika i elementu. Witaj wizualizacji hello [polecania Matchbox wynik] [ score-matchbox-recommender] dane wyjściowe wyglądają następująco rysunek 21.

![Wynik wynik systemu polecania hello — ocena prognozowania](./media/machine-learning-interpret-model-results/21.png)

Rysunek 21. Wizualizacja wyników oceny hello hello polecania systemu — prognozowania klasyfikacji

Hello dwóch pierwszych kolumn są hello par element użytkownika przez hello danych wejściowych. trzecia kolumna Hello jest hello przewidywane klasyfikacji użytkownika dla danego elementu. Na przykład w pierwszym wierszu hello klienta, który jest U1048 przewidzieć restauracji toorate 135026 2.

**Zaleca się tooa elementy danego użytkownika**

Wybierając **zalecenie elementu** w obszarze **rodzaj prognozowania polecania**, jest wysyłane żądanie polecania hello tooa elementów toorecommend systemu danego użytkownika. Witaj ostatniego parametru toochoose w tym scenariuszu jest *zaleca wybór elementu*. Witaj opcja **z oceną elementy (ocena modelu)** jest przeznaczone głównie dla modelu procesu szkolenia hello wersji ewaluacyjnej. Dla tego etapu prognozowania wybieramy opcję **z wszystkich elementów**. Witaj wizualizacji hello [polecania Matchbox wynik] [ score-matchbox-recommender] dane wyjściowe wyglądają następująco rysunek 22.

![Wynik oceny systemu polecania — zalecenia elementu](./media/machine-learning-interpret-model-results/22.png)

Rysunek 22. Wizualizacja wyników oceny hello polecania systemu — zalecenia elementu

Witaj pierwszy hello reprezentuje kolumn hello sześciu podane elementy toorecommend identyfikatorów użytkownika, zgodnie z danych wejściowych hello. Witaj innych pięć kolumny reprezentują elementy hello zalecane toohello użytkownika w kolejności malejącej istotne. Na przykład w pierwszym wierszu hello, hello najbardziej zalecamy restauracji dla klienta U1048 jest 134986, a następnie 135018, 134975 135021 i 132862.

**Znajdź użytkowników tooa pokrewne danego użytkownika**

Wybierając **powiązanych użytkowników** w obszarze **rodzaj prognozowania polecania**, jest wysyłane żądanie polecania hello systemu toofind powiązanych użytkowników tooa danego użytkownika. Powiązanych użytkowników są hello użytkowników, którzy mają podobne preferencje. Witaj ostatniego parametru toochoose w tym scenariuszu jest *powiązane wybór użytkownika*. Witaj opcja **od użytkowników czy oceną elementy (ocena modelu)** jest przeznaczone głównie dla modelu procesu szkolenia hello wersji ewaluacyjnej. Wybierz **od wszystkich użytkowników** etap prognozowania. Witaj wizualizacji hello [polecania Matchbox wynik] [ score-matchbox-recommender] dane wyjściowe wyglądają następująco rysunku 23.

![Wynik oceny systemu polecania — powiązanych użytkowników](./media/machine-learning-interpret-model-results/23.png)

Rysunek 23. Wizualizacja wyników klasyfikacji hello polecania systemu — powiązanych użytkowników

Witaj najpierw z hello pokazuje kolumn hello sześciu podane toofind identyfikatorów potrzeby użytkownika dotyczące użytkowników, określone dane wejściowe. Witaj innym magazynie pięć kolumn hello przewidywane powiązanych użytkowników użytkownika hello w kolejności malejącej istotne. Na przykład w pierwszym wierszu hello, powitania klienta najbardziej odpowiednie dla klienta U1048 jest U1051, a następnie U1066, U1044 U1017 i U1072.

**Znajdź elementy tooa pokrewne danego elementu**

Wybierając **elementy pokrewne** w obszarze **rodzaj prognozowania polecania**, są pytaniem polecania hello systemu toofind elementy pokrewne tooa danego elementu. Powiązane elementy są toobe najbardziej prawdopodobne elementy hello zbędne przez hello sam użytkownika. Witaj ostatniego parametru toochoose w tym scenariuszu jest *powiązane Wybór elementu*. Witaj opcja **z oceną elementy (ocena modelu)** jest przeznaczone głównie dla modelu procesu szkolenia hello wersji ewaluacyjnej. Wybrany **z wszystkich elementów** dla tego etapu prognozowania. Witaj wizualizacji hello [polecania Matchbox wynik] [ score-matchbox-recommender] dane wyjściowe wyglądają następująco 24 rysunku.

![Wynik oceny systemu polecania — elementy pokrewne](./media/machine-learning-interpret-model-results/24.png)

Rysunek 24. Wizualizacja wyników klasyfikacji hello polecania systemu — elementy pokrewne

Witaj pierwszy hello reprezentuje kolumn hello sześciu podane identyfikatory elementów potrzebne toofind elementów pokrewnych, zgodnie z hello danych wejściowych. Witaj innym magazynie pięć kolumn hello przewidywane elementy pokrewne elementu hello w kolejności malejącej pod względem istotności. Na przykład w pierwszym wierszu hello, hello elementu najbardziej odpowiednie dla elementu 135026 jest 135074, a następnie 135035, 132875 135055 i 134992.

**Publikowania usług sieci Web**

Witaj proces publikowania tych eksperymenty jako prognoz tooget usług sieci web jest podobny dla każdego z czterech scenariuszy hello. W tym miejscu traktujemy hello drugi scenariusz (tooa elementów zalecamy danego użytkownika), na przykład. Możesz wykonać hello tę samą procedurę z hello innych trzy.

Zapisywanie hello uczony systemu polecania jako uczonego modelu i filtrowania hello tooa danych wejściowych w kolumnie Identyfikator pojedynczego użytkownika jako pobrany, może Podłączanie eksperymentu hello jak rysunek 25 i opublikujesz je jako usługi sieci web.

![Ocenianie eksperymentu hello restauracji zalecenie problem](./media/machine-learning-interpret-model-results/25.png)

Rysunek 25. Ocenianie eksperymentu hello restauracji zalecenie problem

Uruchomiona usługa sieci web hello, hello zwrócił wynik prawdopodobnie 26 rysunku. Witaj pięć restauracji zalecane dla użytkownika U1048 są 134986, 135018 134975, 135021 i 132862.

![Przykładowe usługa systemowa polecania](./media/machine-learning-interpret-model-results/25_1.png)

![Przykładowe wyniki eksperymentu](./media/machine-learning-interpret-model-results/26.png)

Rysunek 26. Wynikiem usługi sieci Web restauracji zalecenie problemu

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
