---
title: "wydajność modelu aaaEvaluate w uczeniu maszynowym | Dokumentacja firmy Microsoft"
description: "W tym artykule wyjaśniono, jak tooevaluate modelu wydajności w usłudze Azure Machine Learning."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 5dc5348a-4488-4536-99eb-ff105be9b160
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bradsev;garye
ms.openlocfilehash: 03477368758dbb13aa6f54c5d27fb215615d1f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooevaluate-model-performance-in-azure-machine-learning"></a>Jak tooevaluate modelu wydajności w usłudze Azure Machine Learning
W tym artykule pokazano, jak tooevaluate hello wydajności modelu w usłudze Azure Machine Learning Studio i zawiera krótki opis metryki hello dostępne dla tego zadania. Dostępne są trzy typowe scenariusze uczenia nadzorowanego: 

* Regresja
* klasyfikacji binarnej 
* wieloklasowej klasyfikacji

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Ocena wydajności hello modelu jest jednym z hello core etapów w procesie nauki danych hello. Wskazuje, jak pomyślnie hello oceniania (prognoz) zestawu danych została przez uczonego modelu. 

Azure Machine Learning obsługuje oceny modelu za pomocą dwóch jego głównej maszynie modułów szkoleniowych: [Evaluate Model] [ evaluate-model] i [krzyżowa Weryfikacja modelu][cross-validate-model]. Te moduły umożliwiają toosee sposób wykonywania modelu pod względem liczba metryki, które są często używane w uczeniu maszynowym i statystyki.

## <a name="evaluation-vs-cross-validation"></a>Ocena programu vs. Krzyżowe sprawdzanie poprawności
Ocena i krzyżowego sprawdzania poprawności są standardowe metody toomeasure hello wydajności modelu. Oba generować metryki oceny można sprawdzić lub porównać tych innych modeli.

[Ocena modelu] [ evaluate-model] oczekuje scored zestawu danych jako dane wejściowe (lub 2 w przypadku chcesz toocompare wydajność hello różne modele 2). Oznacza to, że konieczne tootrain modelu za pomocą hello [Train Model] [ train-model] modułu i dokonywać prognoz dla niektórych zestawu danych za pomocą hello [Score Model] [ score-model] modułu, zanim będziesz w stanie ocenić hello wyników. Witaj oceny opiera się na powitania oceniane etykiety/prawdopodobieństwa wraz z hello true etykiety, które są danymi wyjściowymi hello [Score Model] [ score-model] modułu.

Alternatywnie można użyć tooperform krzyżowego sprawdzania poprawności wielu ocenić train wynik operacji (złożeń 10) automatycznie na różnych podzestawy hello danych wejściowych. dane wejściowe Hello jest podzielony na 10 części, która jest zarezerwowany do testowania i hello innych 9 szkolenia. Ten proces jest powtarzany 10 razy, a metryki oceny hello zostały uśrednione. Pomaga to w określeniu, jak model czy generalize toonew zestawów danych. Witaj [krzyżowa Weryfikacja modelu] [ cross-validate-model] moduł przyjmuje w modelu nieprzeszkolonych i niektóre z etykietą elementu dataset i dane wyjściowe wyniki oceny hello każdego hello 10 złożeń, oprócz toohello średnio wyników.

W hello następujące sekcje zawierają informacje, firma Microsoft będzie utworzyć prosty modele regresji i klasyfikacji i oceny ich wydajności, za pomocą obu hello [Evaluate Model] [ evaluate-model] i hello [krzyżowa Weryfikacja Model] [ cross-validate-model] modułów.

## <a name="evaluating-a-regression-model"></a>Ocena modelu regresji
Załóżmy, że chcemy toopredict cen samochodów korzystanie z niektórych funkcji, takich jak wymiary, moc, aparat specyfikacji i tak dalej. Jest to problem typowe regresji, gdzie hello Zmienna docelowa (*cen*) ciągłego wartość liczbową. Firma Microsoft może składać się, że podany funkcji hello wartości samochodu można przewidzieć hello cen samochodów tego modelu prostego regresji liniowej. Ten model regresji może służyć tooscore hello możemy uczony na tym samym zestawem danych. Gdy będziemy mieć hello prognozowane ceny dla wszystkich samochodów hello, możemy ocenić wydajność hello modelu hello analizując ile prognoz hello różni się od rzeczywistej ceny hello średnio. tooillustrate, używamy hello *Automobile price data (Raw) dataset* dostępne w hello **zapisane zestawów danych** sekcji w usłudze Azure Machine Learning Studio.

### <a name="creating-hello-experiment"></a>Tworzenie hello eksperymentu
Dodaj powitania po obszarze roboczym tooyour moduły w usłudze Azure Machine Learning Studio:

* Cen samochodów, data (Raw)
* [Regresja liniowa][linear-regression]
* [Train Model][train-model]
* [Score Model][score-model]
* [Ocena modelu][evaluate-model]

Połącz porty hello, jak przedstawionym poniżej na rysunku 1 i zestaw hello etykiety kolumnę hello [Train Model] [ train-model] modułu zbyt*cen*.

![Ocena modelu regresji](media/machine-learning-evaluate-model-performance/1.png)

Rysunek 1. Ocena modelu regresji.

### <a name="inspecting-hello-evaluation-results"></a>Sprawdzanie wyników oceny hello
Po uruchomionych hello eksperymentu, możesz kliknąć portem wyjściowym hello hello [Evaluate Model] [ evaluate-model] moduł i zaznacz *wizualizacja* wyniki oceny hello toosee. Witaj metryki oceny dostępna dla modeli regresji są: *oznacza błąd absolutny*, *głównego oznacza błąd absolutny*, *względny błąd absolutny*,  *Błąd względny kwadrat*i hello *współczynnika determinacji*.

Witaj Hello termin "błąd" w tym miejscu reprezentuje hello różnicy między wartością prognozowaną a hello wartość true. wartość bezwzględna Hello lub hello kwadratowy tej różnicy są zazwyczaj obliczona toocapture hello całkowita wielkość błędu we wszystkich wystąpieniach hello różnicę między hello przewidzieć i wartości true może być liczbą ujemną, w niektórych przypadkach. Witaj błąd metryki pomiaru wydajności predykcyjnej hello modelu regresji pod względem odchylenie średniej hello jego prognoz hello wartości true. Niższe wartości błąd oznacza, że hello model jest dokładniejszych prognoz zgłoszenia. Metryka ogólny błąd 0 oznacza, że hello modelu dopasowany hello danych.

Hello współczynnik determinacji, który jest również nazywany R-kwadrat, jest również standardowy sposób pomiaru, jak hello model dopasowanie hello danych. Mogą być interpretowane jako część hello odmiany wyjaśnione przy użyciu modelu hello. Wyższy udział jest lepszym rozwiązaniem w przypadku gdzie 1 oznacza, dokładne dopasowanie.

![Metryki oceny regresji liniowej](media/machine-learning-evaluate-model-performance/2.png)

Rysunek 2. Metryki oceny regresji liniowej.

### <a name="using-cross-validation"></a>Za pomocą innej sprawdzania poprawności
Jak wspomniano wcześniej, można przeprowadzić szkolenie powtarzane, ocenianie i oceny automatycznie za pomocą hello [krzyżowa Weryfikacja modelu] [ cross-validate-model] modułu. W takim przypadku wystarczy zestawu danych, model nieprzeszkolonych i [krzyżowa Weryfikacja modelu] [ cross-validate-model] modułu (zobacz rysunek poniżej). Uwaga zbyt muszą tooset hello etykiety kolumn*cen* w hello [krzyżowa Weryfikacja modelu] [ cross-validate-model] właściwości modułu.

![Krzyżowe sprawdzanie modelu regresji](media/machine-learning-evaluate-model-performance/3.png)

Rysunek 3. Weryfikowanie między modelu regresji.

Po uruchomionych hello eksperymentu, możesz sprawdzić wyniki oceny hello, kliknij port wyjściowy prawo hello hello [krzyżowa Weryfikacja modelu] [ cross-validate-model] modułu. Zapewni to szczegółowy widok hello metryki dla każdej iteracji (składanie), a hello średnio wyniki każdego z metryki hello (4 rysunek).

![Wyników krzyżowego sprawdzania poprawności modelu regresji](media/machine-learning-evaluate-model-performance/4.png)

Rysunek 4. Wyników krzyżowego sprawdzania poprawności modelu regresji.

## <a name="evaluating-a-binary-classification-model"></a>Ocena modelu klasyfikacji binarnej
W przypadku klasyfikacji binarnej hello Zmienna docelowa ma tylko dwa możliwe wyniki, na przykład: {0, 1} lub {false, wartość true}, {ujemną, dodatnią}. Załóżmy, można skorzystać z zestawu danych dla dorosłych pracowników z niektórych demograficznych i zatrudnienia zmienne i zostanie wyświetlona prośba toopredict hello dochodu poziom, binary zmiennej o wartości hello {"< = 50K", "> 50K"}. Innymi słowy, klasa ujemna hello reprezentuje hello pracowników, którzy tworzą mniejsza lub równa too50K rocznie i hello dodatnią, klasa reprezentuje wszystkich innych pracowników. Jak hello scenariuszu regresji firma Microsoft będzie uczenie modelu przy użyciu wynik niektóre dane i ocena wyników hello. Witaj za główną różnicą jest wybór hello metryki, który oblicza uczenie maszynowe Azure i danych wyjściowych. tooillustrate hello dochodu poziomu prognozowania scenariuszu będziemy używać hello [dla dorosłych](http://archive.ics.uci.edu/ml/datasets/Adult) toocreate zestawu danych usługi Azure Machine Learning eksperymentu i ocena wydajności hello modelu Regresja logistyczna dwuklasowych, często używane dane binarne Klasyfikator.

### <a name="creating-hello-experiment"></a>Tworzenie hello eksperymentu
Dodaj powitania po obszarze roboczym tooyour moduły w usłudze Azure Machine Learning Studio:

* Dla dorosłych klasyfikacji binarnej dochodu spisu zestawu danych.
* [Regresja logistyczna Two-Class][two-class-logistic-regression]
* [Train Model][train-model]
* [Score Model][score-model]
* [Ocena modelu][evaluate-model]

Połącz porty hello, jak przedstawionym poniżej na rysunku 5 i zestaw hello etykiety kolumnę hello [Train Model] [ train-model] modułu zbyt*dochodu*.

![Ocena modelu klasyfikacji binarnej](media/machine-learning-evaluate-model-performance/5.png)

Rysunek 5. Ocena modelu klasyfikacji binarnej.

### <a name="inspecting-hello-evaluation-results"></a>Sprawdzanie wyników oceny hello
Po uruchomionych hello eksperymentu, możesz kliknąć portem wyjściowym hello hello [Evaluate Model] [ evaluate-model] moduł i zaznacz *wizualizacja* wyniki oceny hello toosee (rysunek 7). Witaj metryki oceny dostępne są modele klasyfikacji binarnej: *dokładność*, *dokładności*, *odwołania*, *F1 oceny*, i *AUC*. Ponadto moduł hello generuje macierzy pomyłek przedstawiający hello liczba alarmów wartość true, fałszywych wyników negatywnych fałszywych alarmów i negatywów wartość true, a także *ROC*, *dokładności/wycofania*i *Podnieś* krzywych.

Dokładność jest po prostu hello część poprawnie klasyfikowane wystąpień. Zazwyczaj jest hello pierwszy metrykę, które można przyjrzeć się podczas obliczania klasyfikatora. Jednakże, gdy dane testowe hello jest niezrównoważone (gdzie większość wystąpień hello należą tooone klasy hello) lub więcej planuje hello wydajności na jedną z klas hello, dokładność naprawdę nie przechwytuje hello skuteczności klasyfikatora. W scenariuszu poziomu klasyfikacji dochodu hello założono podczas testowania niektórych danych, w którym 99% wystąpień hello reprezentują osoby, tym mniejsza lub równa too50K rocznie. Jest możliwe tooachieve 0.99 dokładność przez klasy Witaj "< = 50K" dla wszystkich wystąpień. klasyfikatora Hello pojawia się w tym przypadku toobe wysoki poziom ogólnej, ale w rzeczywistości nie jest on tooclassify poszczególnych osób high-income hello (hello 1%) poprawnie.

Z tego powodu jest przydatne toocompute dodatkowe metryki, które przechwytywania dokładniej aspektów hello oceny. Przed przejściem do szczegółów hello takie metryki, jest ważne toounderstand hello pomyłek macierzy oceny klasyfikacji binarnej. klasy Hello etykiet w zestawie szkolenia hello może przybrać tylko 2 możliwych wartości, które firma Microsoft zwykle można znaleźć tooas dodatnią lub ujemną. Hello dodatnie i ujemne wystąpieniom klasyfikatora prognozuje poprawnie są nazywane odpowiednio alarmów true (TP) i true negatywów (TN). Podobnie wystąpień hello nieprawidłowo sklasyfikowane są nazywane fałszywych alarmów (FP) i fałszywych wyników negatywnych (FN). Macierz pomyłek Hello jest po prostu tabelę przedstawiającą hello liczba wystąpień, które są objęte każdej z tych kategorii 4. Usługa Azure Machine Learning automatycznie decyduje, które Witaj dwie klasy w zestawie danych hello jest klasa dodatnią hello. Jeśli hello klasy etykiety są logiczną lub liczb całkowitych, a następnie hello wystąpień etykietą "prawda" lub "1" jest przypisywana hello dodatnią klasy. Jeśli hello etykiety są ciągami, tak jak przypadku hello hello dochodu dataset, etykiety hello jest sortowana alfabetycznie, i pierwszy poziom hello jest wybierany klasy ujemna hello toobe podczas drugiego poziomu hello jest klasa dodatnią hello.

![Macierz pomyłek klasyfikacji binarnej](media/machine-learning-evaluate-model-performance/6a.png)

Rysunek 6. Macierz pomyłek klasyfikacji binarnej.

Cofnięcie toohello dochodu klasyfikacji problemu, czy chcemy tooask kilka oceny pytania, które pomagają nam zrozumieć wydajności hello klasyfikatora hello używane. Jest bardzo fizycznych zapytania: "poza hello osób, którym hello modelu zdobywanie przewidywane toobe > 50 K (TP + FP), ile zostały poprawnie klasyfikowane (TP)?" To pytanie można udzielić odpowiedzi, analizując hello **dokładności** modelu hello jest hello część alarmów, które są poprawnie klasyfikowane: TP/(TP+FP). Jest inny, często zadawane pytania "poza wszystkich hello wysokiej wartości pracowników z dochodu > 50 k (TP + FN), ile hello klasyfikatora klasyfikowania poprawnie (TP)". Jest rzeczywiście hello **odwołania**, lub wartość true, szybkość dodatnią hello: TP/(TP+FN) hello klasyfikatora. Może się okazać, czy znajduje się oczywiste kompromis między precision i odwołania. Na przykład podana stosunkowo zrównoważonym zestawu danych, klasyfikatora, który prognozuje przede wszystkim dodatnią wystąpień byłyby wysokiej odwołania, ale raczej niski dokładności jako wiele wystąpień ujemna hello będzie można nieprawidłowo klasyfikowana powodujące dużą liczbę fałszywych alarmów. toosee wykres jak w zależności od tych dwóch metryk, możesz kliknąć krzywej "Dokładności/odwołania" hello hello obliczania wyniku dane wyjściowe strony (u góry po lewej części rysunek 7).

![Wyniki oceny klasyfikacji binarnej](media/machine-learning-evaluate-model-performance/7.png)

Rysunek 7. Wyniki oceny klasyfikacji binarnej.

Inny powiązane metryki, która jest często używana jest hello **F1 oceny**, który przyjmuje zarówno precision i odwołania pod uwagę. Jest hello harmoniczną tych metryk 2 i jest obliczana tak: F1 = 2 (precyzja x odwołania) / (precyzja + odwołania). wynik F1 Hello jest ocena hello toosummarize dobrym sposobem, w jeden numer, ale jest zawsze toolook dobrym rozwiązaniem, zarówno na poziomie dokładność i odwołania razem toobetter zrozumieć, jak ma zachowywać się klasyfikatora.

Ponadto jedną sprawdzić hello szybkość dodatnią wartość true, a false szybkość dodatnią hello w hello **odbiornika operacyjnego cechy (ROC)** krzywą i hello odpowiadającego **hello obszaru w krzywej (AUC)** wartość. Witaj bliżej krzywej toohello górnym lewym rogu, wydajności klasyfikatora hello lepsze hello jest (czyli DSI oznacza optymalne wykorzystanie hello true dodatnią szybkość przy jednoczesnym zmniejszeniu hello false szybkość dodatnią). Krzywych przekątnej Zamknij toohello hello kreślenia, w wyniku klasyfikatory, które zwykle toomake prognoz, które są zamknięcie, odgadnięcie toorandom.

### <a name="using-cross-validation"></a>Za pomocą innej sprawdzania poprawności
Co w przykładzie regresji hello możemy przeprowadzić krzyżowego sprawdzania poprawności toorepeatedly pociągu, wynik i automatycznie oceny różnych podzbiór danych hello. Analogicznie, można użyć hello [krzyżowa Weryfikacja modelu] [ cross-validate-model] modułu, model nieprzeszkolonych Regresja logistyczna i zestawu danych. Witaj etykiety kolumn musi być ustawiona zbyt*dochodu* w hello [krzyżowa Weryfikacja modelu] [ cross-validate-model] właściwości modułu. Po systemem eksperymentu hello i klikając prawym hello output portu hello [krzyżowa Weryfikacja modelu] [ cross-validate-model] modułu, zobaczysz metryki klasyfikacji binarnej hello wartości dla każdego złożenia dodatkowo toohello Średnia i odchylenie standardowe każdego z nich. 

![Cross-sprawdzanie poprawności modelu klasyfikacji binarnej](media/machine-learning-evaluate-model-performance/8.png)

Rysunek 8. Weryfikowanie między Model klasyfikacji binarnej.

![Krzyżowe sprawdzanie poprawności wyniki klasyfikatora binarne](media/machine-learning-evaluate-model-performance/9.png)

Rysunek 9. Krzyżowe sprawdzanie poprawności wyniki binarne klasyfikatora.

## <a name="evaluating-a-multiclass-classification-model"></a>Ocena modelu Wieloklasowej klasyfikacji
W tym eksperymencie używamy hello popularnych [Iris](http://archive.ics.uci.edu/ml/datasets/Iris "Iris") zestawu danych zawierającego wystąpienia 3 różne rodzaje (klasy) roślin iris hello. Istnieją 4 wartości funkcji (sepal długości do szerokości i długości Motyw Płatek do szerokości) dla każdego wystąpienia. W poprzednim doświadczeniach hello możemy uczenia i modeli hello przetestowany przy użyciu hello tego samego zestawów danych. W tym miejscu użyjemy hello [podziału danych] [ split] modułu toocreate 2 podzbiór danych hello uczenia na powitania najpierw wynik i ocenić na powitania drugiego. Witaj Iris zestaw danych jest ogólnie dostępna w hello [UCI Machine Learning repozytorium](http://archive.ics.uci.edu/ml/index.html)i może zostać pobrany przy użyciu [i zaimportuj dane] [ import-data] modułu.

### <a name="creating-hello-experiment"></a>Tworzenie hello eksperymentu
Dodaj powitania po obszarze roboczym tooyour moduły w usłudze Azure Machine Learning Studio:

* [Importowanie danych][import-data]
* [Multiklasa decyzji lasu][multiclass-decision-forest]
* [Podział danych][split]
* [Train Model][train-model]
* [Score Model][score-model]
* [Ocena modelu][evaluate-model]

Połącz porty hello, jak pokazano poniżej na rysunku nr 10.

Ustaw indeks kolumny etykiety hello hello [Train Model] [ train-model] too5 modułu. Hello dataset zawiera bez wiersza nagłówka, ale wiemy klasy hello etykiety są podawane w kolumnie piątym powitania.

Polecenie hello [i zaimportuj dane] [ import-data] modułu i zestaw hello *źródła danych* właściwości zbyt*adres URL sieci Web za pośrednictwem protokołu HTTP*i hello *adresu URL*  toohttp://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data.

Zestaw hello część toobe wystąpień używane do szkolenia w hello [podziału danych] [ split] modułu (0,7 na przykład).

![Ocena Wieloklasowej klasyfikatora](media/machine-learning-evaluate-model-performance/10.png)

Rysunek 10. Ocena Wieloklasowej klasyfikatora

### <a name="inspecting-hello-evaluation-results"></a>Sprawdzanie wyników oceny hello
Uruchom eksperyment hello i kliknij port wyjściowy hello [Evaluate Model][evaluate-model]. wyniki oceny Hello są prezentowane w postaci hello macierzy pomyłek, w tym przypadku. Macierz Hello pokazuje hello rzeczywiste a przewidywane wystąpień dla wszystkich klas 3.

![Wyniki oceny wieloklasowej klasyfikacji](media/machine-learning-evaluate-model-performance/11.png)

Rysunek 11. Wyniki oceny wieloklasowej klasyfikacji.

### <a name="using-cross-validation"></a>Za pomocą innej sprawdzania poprawności
Jak wspomniano wcześniej, można przeprowadzić szkolenie powtarzane, ocenianie i oceny automatycznie za pomocą hello [krzyżowa Weryfikacja modelu] [ cross-validate-model] modułu. Będzie potrzebny zestawu danych, model nieprzeszkolonych i [krzyżowa Weryfikacja modelu] [ cross-validate-model] modułu (zobacz rysunek poniżej). Ponownie należy tooset hello etykiety kolumny hello [krzyżowa Weryfikacja modelu] [ cross-validate-model] modułu (indeks kolumny 5 w tym przypadku). Po systemem hello eksperymentu, a następnie klikając polecenie prawo hello output portu hello [krzyżowa Weryfikacja modelu][cross-validate-model], możesz sprawdzić hello wartości metryki dla każdej fold, a także hello średniej i odchylenia standardowego. metryki Hello tutaj wyświetlane są podobne toohello hello omówione w przypadku klasyfikacji binarnej hello z nich. Jednak należy pamiętać, że w wieloklasowej klasyfikacji, obliczeniowych hello true alarmów/negatywów i fałszywych alarmów/wyników negatywnych polega na zliczania na podstawie według klasy, ponieważ nie ma żadnych klasy ogólnej dodatnią lub ujemną. Na przykład podczas przetwarzania danych dokładności hello lub odwołania klasy "Iris setosa" hello, zakłada się to hello dodatnią klasy i wszystkie inne negatywne.

![Krzyżowe sprawdzanie modelu Wieloklasowej klasyfikacji](media/machine-learning-evaluate-model-performance/12.png)

Rysunek 12. Weryfikowanie między modelu Wieloklasowej klasyfikacji.

![Wyników krzyżowego sprawdzania poprawności modelu Wieloklasowej klasyfikacji](media/machine-learning-evaluate-model-performance/13.png)

Rysunek 13. Wyników krzyżowego sprawdzania poprawności modelu Wieloklasowej klasyfikacji.

<!-- Module References -->
[cross-validate-model]: https://msdn.microsoft.com/library/azure/75fb875d-6b86-4d46-8bcc-74261ade5826/
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[multiclass-decision-forest]: https://msdn.microsoft.com/library/azure/5e70108d-2e44-45d9-86e8-94f37c68fe86/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-logistic-regression]: https://msdn.microsoft.com/library/azure/b0fd7660-eeed-43c5-9487-20d9cc79ed5d/

