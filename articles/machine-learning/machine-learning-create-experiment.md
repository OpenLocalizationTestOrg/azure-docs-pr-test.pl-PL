---
title: "aaaA prostego eksperymentu w usłudze Machine Learning Studio | Dokumentacja firmy Microsoft"
description: "Ten samouczek uczenia maszynowego przeprowadzi Cię przez łatwy eksperyment dotyczący przetwarzania danych. Firma Microsoft będzie prognozowania hello ceny samochodu przy użyciu algorytmu regresji."
keywords: experiment,linear regression,machine learning algorithms,machine learning tutorial,predictive modeling techniques,data science experiment
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>Samouczek dotyczący uczenia maszynowego: tworzenie pierwszego eksperymentu związanego z przetwarzaniem danych w usłudze Azure Machine Learning Studio

Ten samouczek jest przeznaczony dla osób, którym nie zdarzyło się korzystać z usługi **Azure Machine Learning Studio**.

W tym samouczku zostanie omówiony sposób toouse Studio na powitania po raz pierwszy toocreate eksperymentu uczenia maszynowego. Witaj eksperymentu przetestuje analitycznych modelu, który prognozuje cenę samochodów na podstawie różnych zmiennych, takich jak marka i specyfikacja techniczna hello.

> [!NOTE]
> W tym samouczku przedstawiono hello podstawy modułów jak toodrag i upuść na eksperymentu, je połączyć ze sobą, uruchom eksperyment hello i przyjrzyj się hello wyników. Nie chcemy się, że toodiscuss hello ogólny temat uczenia maszynowego lub jak tooselect i użyj hello 100 + wbudowanych algorytmów i danych manipulowania modułów zawarte w Studio.
>
>Jeśli nowy learning toomachine hello seria filmów [nauki danych dla początkujących](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) może być toostart dobrym miejscem. Ta seria wideo jest doskonały wprowadzenie learning toomachine, przy użyciu języka codzienne oraz pojęcia.
>
>Jeśli znasz uczenia maszynowego, ale szukasz bardziej ogólne informacje o usłudze Machine Learning Studio i algorytmów, które zawiera uczenia maszynowego hello, Przedstawiamy materiały, dobrym:
>
- [Co to jest Machine Learning Studio?](machine-learning-what-is-ml-studio.md) — ogólne omówienie usługi Studio.
- [Machine learning podstawy wraz z przykładami algorytmu](machine-learning-basics-infographic-with-algorithm-examples.md) -tego infographic jest przydatne w przypadku toolearn więcej o różnych typach hello algorytmów uczenia maszynowego uwzględnionych w usłudze Machine Learning Studio.
- [Przewodnik Learning maszyny](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) — w tym przewodniku dotyczą podobne informacje jako infographic hello powyżej, ale w format interakcyjny.
- [Machine learning algorytmu ściągawka](machine-learning-algorithm-cheat-sheet.md) i [jak algorytmów toochoose Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) — tym plakat do pobrania i towarzyszące artykułu omówiono w nim algorytmów Studio hello szczegółowo.
- [Usługi Machine Learning Studio: Algorytm i pomóc modułu](https://msdn.microsoft.com/library/azure/dn905974.aspx) — jest to hello pełną dokumentację dla wszystkich modułów Studio, w tym algorytmów uczenia maszynowego,

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>W czym pomaga usługa Machine Learning Studio?

Usługa Machine Learning Studio umożliwia łatwe tooset się przy użyciu modułów przeciągania i upuszczania wcześniej zaplanowane techniki modelowania predykcyjnego eksperymentu.

Przy użyciu wizualnego interfejsu można przeciągać ***zestawy danych*** oraz ***moduły*** analiz i upuszczać je na interakcyjny obszar roboczy. Podłącz je razem tooform ***eksperymentu*** uruchomionymi w usłudze Machine Learning Studio.
Możesz ***utworzyć model***, ***uczenia modelu hello***, i ***oceny i testowania hello modelu***.

Można wykonać iterację projektu modelu edycji eksperymentu hello i uruchomić je, dopóki zapewnia hello wyników, którego szukasz. Gotowy model można opublikować jako ***usługę sieci Web***. Pozwoli to innym osobom uzyskiwać prognozy na podstawie nowych danych.

## <a name="open-machine-learning-studio"></a>Otwieranie usługi Machine Learning Studio

tooget wprowadzenie Studio Przejdź zbyt[https://studio.azureml.net](https://studio.azureml.net). Jeśli logujesz się w usłudze Machine Learning Studio nie po raz pierwszy, kliknij pozycję **Sign in** (Zaloguj się). W przeciwnym razie kliknij pozycję **Sign up here** (Zarejestruj się) i wybierz opcję darmową lub płatną.

![Zaloguj się tooMachine Learning Studio][sign-in-to-studio]
<br/>
***Zaloguj się tooMachine Learning Studio***

## <a name="five-steps-toocreate-an-experiment"></a>Pięć kroków toocreate eksperymentu

W tym samouczek dotyczący uczenia maszynowego możesz wykonać pięć podstawowych kroków toobuild eksperymentu w usłudze Machine Learning Studio toocreate, pociągu i score model:

- **Tworzenie modelu**
    - [Krok 1. Pobieranie danych]
    - [Krok 2: Przygotowanie hello danych]
    - [Krok 3. Definiowanie funkcji]
- **Train hello model**
    - [Krok 4. Wybieranie i stosowanie algorytmu uczenia]
- **Oceny i testowania hello modelu**
    - [Krok 5. Przewidywanie nowych cen samochodów]

[Krok 1. Pobieranie danych]: #step-1-get-data
[Krok 2: Przygotowanie hello danych]: #step-2-prepare-the-data
[Krok 3. Definiowanie funkcji]: #step-3-define-features
[Krok 4. Wybieranie i stosowanie algorytmu uczenia]: #step-4-choose-and-apply-a-learning-algorithm
[Krok 5. Przewidywanie nowych cen samochodów]: #step-5-predict-new-automobile-prices

> [!TIP] 
> Kopia robocza hello można znaleźć następujących eksperymentu w hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com). Przejdź za**[pierwsze połączenie analiz danych eksperymentu - Prognozowanie cen samochodów](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  i kliknij przycisk **Otwórz w Studio** toodownload kopię hello eksperymentu w Twojej uczenia maszynowego Obszar roboczy Studio.


## <a name="step-1-get-data"></a>Krok 1. Pobieranie danych

najpierw Hello należy uczenia maszynowego tooperform są dane.
Usługa Machine Learning Studio udostępnia wiele przykładowych zestawów danych do wyboru. Dane można również importować z wielu źródeł. W tym przykładzie użyjemy hello przykładowego zestawu danych, **samochodów price data (Raw)**, który znajduje się w obszarze roboczym.
Zestaw ten zawiera dane różnych modeli samochodów, na przykład informacje dotyczące marki, ceny czy specyfikacji technicznej.

Oto, jak tooget hello zestawu danych do eksperymentu.

1. Utwórz nowy eksperyment, klikając **+ nowy** u dołu okna Machine Learning Studio hello hello, wybierz **EKSPERYMENTU**, a następnie wybierz **puste eksperymentu**.

2. Witaj eksperymentu znajduje się domyślną nazwę wyświetlaną u góry hello hello kanwy. Wybierz ten tekst i zmień jego nazwę toosomething opisowy, na przykład **Prognozowanie cen samochodów**. Nazwa Hello nie wymaga toobe unikatowy.

    ![Zmień nazwę eksperymentu hello][rename-experiment]

2. po lewej toohello kanwy eksperymentu hello znajduje się paleta zawierająca zestawy danych i moduły. Typ **samochodów** w polu wyszukiwania hello na powitania górnej części tej palety toofind hello zestaw danych z etykietą **samochodów price data (Raw)**. Przeciągnij kanwy eksperymentu toohello tego zestawu danych.

    ![Znajdź hello samochodów zestawu danych i przeciągnij go na kanwie eksperymentu hello][type-automobile]
    <br/>
    ***Znajdź hello samochodów zestawu danych i przeciągnij go na kanwie eksperymentu hello***

toosee co dane wygląda na to, kliknij port wyjściowy hello u dołu hello hello samochodów zestawu danych, a następnie wybierz **Visualize**.

![Kliknij port wyjściowy hello i wybierz pozycję "Wizualizacja"][select-visualize]
<br/>
***Kliknij port wyjściowy hello i wybierz pozycję "Wizualizacja"***

> [!TIP]
> Zestawy danych i moduły mają wejściowe i porty wyjścia reprezentowany przez małe okręgi — porty wejściowe u góry hello wyjściowe porty u dołu hello.
toocreate przepływu danych eksperymentu, uzyskasz połączenie portem wyjściowym port wejściowy tooan jeden moduł innego.
W dowolnym momencie możesz kliknąć portem wyjściowym hello toosee dataset lub moduł danych hello wygląda w tym momencie hello przepływu danych.

W tym przykładowego zestawu danych każdego wystąpienia modeli samochodów występuje jako wiersz i hello zmiennych skojarzonych z każdym samochodów są wyświetlane jako kolumny. Mając hello zmienne dla określonego samochód, chcemy tootry toopredict hello cen w skrajna prawa kolumna (kolumna 26 zatytułowana "price").

![Wyświetl dane samochodów hello okno wizualizacji danych hello][visualize-auto-data]
<br/>
***Wyświetl dane samochodów hello okno wizualizacji danych hello***

Hello Zamknij okno wizualizacji, klikając hello "**x**" w prawym górnym rogu hello.

## <a name="step-2-prepare-hello-data"></a>Krok 2: Przygotowanie hello danych

Zestawy danych zwykle wymagają przetworzenia wstępnego przed rozpoczęciem analizy. Na przykład można zauważyć hello brakujących wartości w kolumnach hello różnych wierszy. Te brakujące wartości muszą toobe wyczyszczone, aby umożliwić hello modelu można analizować dane hello poprawnie. W naszym przykładzie usuniemy wszystkie wiersze z brakującymi wartościami. Ponadto hello **kolumny znormalizowane straty** kolumna ma dużą część brakujące wartości, dlatego firma Microsoft będzie wykluczyć tę kolumnę z modelu hello całkowicie.

> [!TIP]
> Czyszczenia hello brakujących wartości w danych wejściowych jest wymaganiem wstępnym większość modułów hello.

Najpierw dodamy moduł, który usuwa hello **kolumny znormalizowane straty** kolumny całkowicie, a następnie możemy dodać inny moduł, która usuwa wszystkie wiersze z brakującymi danymi.

1. Typ **wybierz kolumny** w polu wyszukiwania hello u góry hello hello modułu palety toofind hello [Select Columns in Dataset] [ select-columns] modułu, przeciągnij je toohello kanwy eksperymentu . Ten moduł pozwala nam tooselect kolumny danych, firma Microsoft ma tooinclude lub do wykluczenia w hello modelu.

2. Połącz port wyjściowy hello hello **samochodów price data (Raw)** toohello zestawu danych wejściowych portu hello [Select Columns in Dataset] [ select-columns] modułu.

    ![Dodaj roboczego eksperymentu toohello modułu "Wybieranie kolumn w zestawie danych" hello i podłącz go][type-select-columns]
    <br/>
    ***Dodaj roboczego eksperymentu toohello modułu "Wybieranie kolumn w zestawie danych" hello i podłącz go***

3. Kliknij przycisk hello [Select Columns in Dataset] [ select-columns] modułu i kliknij przycisk **Uruchom selektor kolumn** w hello **właściwości** okienka.

    - Powitania po lewej stronie, kliknij przycisk **przy użyciu reguł**
    - W obszarze **Begin With** (Rozpocznij od) kliknij pozycję **All columns** (Wszystkie kolumny). Dzięki temu [Select Columns in Dataset] [ select-columns] toopass za pośrednictwem wszystkich kolumn hello (z wyjątkiem tych kolumn jesteśmy o tooexclude).
    - Wybierz z listy hello rozwijane, **wykluczyć** i **nazwy kolumn**, a następnie kliknij wewnątrz pola tekstowego hello. Zostanie wyświetlona lista kolumn. Wybierz **kolumny znormalizowane straty**, i jest dodany toohello pola tekstowego.
    - Kliknij przycisk hello znacznika wyboru (OK) przycisk tooclose hello selektora kolumn (w prawym dolnym hello).

    ![Uruchom selektor kolumn hello i wykluczyć kolumnę hello "kolumny znormalizowane straty"][launch-column-selector]
    <br/>
    ***Uruchom selektor kolumn hello i wykluczyć kolumnę hello "kolumny znormalizowane straty"***

    Teraz hello okienka właściwości modułu **Select Columns in Dataset** wskazuje, że zostaną przetworzone wszystkie kolumny z hello zestawu danych, z wyjątkiem **kolumny znormalizowane straty**.

    ![w okienku właściwości Hello pokazuje tej kolumny hello "kolumny znormalizowane straty" jest wyłączona][showing-excluded-column]
    <br/>
    ***w okienku właściwości Hello pokazuje tej kolumny hello "kolumny znormalizowane straty" jest wyłączona***

    > [!TIP]
    Można dodać moduł tooa komentarza, klikając dwukrotnie pozycję modułu hello i wprowadzanie tekstu. Może to ułatwić jednym rzutem oka ocenić zadań jakie hello modułu w eksperymencie. W takim przypadku kliknij dwukrotnie hello [Select Columns in Dataset] [ select-columns] moduł i wpisz tekst hello komentarz "Wyklucz znormalizowane straty".
    >
    >


    ![Kliknij dwukrotnie moduł tooadd komentarz][add-comment]
    <br/>
    ***Kliknij dwukrotnie moduł tooadd komentarz***

3. Przeciągnij hello [Clean Missing Data] [ clean-missing-data] toohello modułu obszaru roboczego eksperymentu i połącz go toohello [Select Columns in Dataset] [ select-columns] modułu. W hello **właściwości** okienku wybierz **Usuń cały wiersz** w obszarze **tryb czyszczenia**. Dzięki temu [Clean Missing Data] [ clean-missing-data] tooclean hello dane przez usunięcie wierszy, które nie mają żadnych wartości. Kliknij dwukrotnie hello moduł i wpisz hello komentarz "Usunięcie wierszy z brakującymi wartościami".

    ![Ustaw tryb czyszczenia hello zbyt "Usuń cały wiersz" dla modułu "Clean Missing Data" hello][set-remove-entire-row]
    <br/>
    ***Ustaw tryb czyszczenia hello zbyt "Usuń cały wiersz" dla modułu "Clean Missing Data" hello***

4. Uruchom eksperyment hello klikając **Uruchom** u dołu hello hello strony.

    Po zakończeniu eksperymentu hello uruchomione wszystkie moduły hello ma tooindicate zielony znacznik wyboru, które zakończyło się pomyślnie. Zwróć uwagę, również hello **zakończeniu działania** stan w prawym górnym rogu hello.

![Po jej uruchomieniu, hello eksperyment powinien wyglądać mniej więcej tak][early-experiment-run]
<br/>
***Po jej uruchomieniu, hello eksperyment powinien wyglądać mniej więcej tak***

> [!TIP]
> Dlaczego przeprowadzana eksperymentu hello teraz? Przez uruchomione hello eksperymentu, hello definicje kolumn dla danych przekazywania z hello zestawu danych, za pomocą hello [Select Columns in Dataset] [ select-columns] modułu, za pośrednictwem hello [Clean Missing Data] [ clean-missing-data] modułu. Oznacza to, że wszystkie moduły połączymy zbyt[Clean Missing Data] [ clean-missing-data] będą także mieć te same informacje.

Firma Microsoft to zostało zrobione w eksperymencie hello się toothis punktu będzie czystą hello danych. Zestaw tooview hello czyszczenia danych, kliknij przycisk hello pozostałych portem wyjściowym hello [Clean Missing Data] [ clean-missing-data] moduł i zaznacz **Visualize**. Zwróć uwagę, że hello **kolumny znormalizowane straty** kolumna nie jest już uwzględniana i nie znajdują się brakujące wartości.

Teraz, dane hello jest czysty, jest gotowy toospecify funkcji firma Microsoft, które ma toouse w model predykcyjny hello.

## <a name="step-3-define-features"></a>Krok 3. Definiowanie cech

W uczeniu maszynowym *cechy* to poszczególne mierzalne właściwości określonych informacji. W naszym zestawie danych poszczególne wiersze odpowiadają różnym samochodom, a kolumny — cechom tych samochodów.

Znajdowanie dobrej zestaw funkcji do tworzenia modelu predykcyjnego, wymaga eksperymentowania oraz wiedzą na temat problemu hello ma toosolve. Niektóre funkcje są lepsze do prognozowania danych docelowych powitania od innych. Ponadto niektóre cechy są ściśle powiązane z innymi, dlatego można je usunąć. Na przykład miasto mpg i paliwa są ściśle powiązane, firma Microsoft może zachować jedną i usunąć hello innych bez znaczącego wpływu na powitania prognozowania.

Utworzymy model, który korzysta z podzbioru cech hello w naszym zestawie danych. Można później i wybrać różne funkcje, ponownie uruchom eksperyment hello i zobacz, jeśli możesz uzyskać lepsze wyniki. Ale toostart, spróbujmy hello następujące funkcje:

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. Przeciągnij kolejny [Select Columns in Dataset] [ select-columns] kanwy eksperymentu toohello modułu. Połącz hello pozostałych portem wyjściowym hello [Clean Missing Data] [ clean-missing-data] danych wejściowych toohello modułu hello [Select Columns in Dataset] [ select-columns] modułu.

    ![Połącz moduł "Clean Missing Data" toohello dla hello "Wybieranie kolumn w zestawie danych"][connect-clean-to-select]
    <br/>
    ***Połącz moduł "Clean Missing Data" toohello dla hello "Wybieranie kolumn w zestawie danych"***

2. Kliknij dwukrotnie hello moduł i wpisz "Wybieranie cech w celu prognozowania."

2. Kliknij przycisk **Uruchom selektor kolumn** w hello **właściwości** okienka.

3. Kliknij pozycję **With rules** (Za pomocą reguł).

4. W obszarze **Begin With** (Rozpocznij od) kliknij pozycję **No columns** (Brak kolumn). W wierszu filtru hello, wybierz **Include** i **nazwy kolumn** i wybierz w polu tekstowym hello naszą listę nazw kolumn. Kieruje hello modułu toonot przekazywania żadnych kolumn (funkcje), z wyjątkiem tych, które określono hello.

5. Kliknij przycisk znacznika wyboru (OK) hello.

    ![Wybierz prognozowania hello hello tooinclude kolumn (funkcje)][select-columns-to-include]
    <br/>
    ***Wybierz prognozowania hello hello tooinclude kolumn (funkcje)***

Daje to filtrowanego zestawu danych zawierającego tylko funkcje hello chcemy toohello toopass uczenia algorytmu, który zostanie użyta w następnym kroku hello. Możesz później wrócić do tego kroku i wybrać inny zbiór cech.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>Krok 4. Wybieranie i stosowanie algorytmu uczenia

Teraz, dane hello jest gotowy, konstruowania modelu predykcyjnego obejmuje uczenie i testowanie. Użyjemy naszego modelu hello tootrain danych, a następnie przetestujemy toosee modelu hello jak blisko jest ceny toopredict stanie.
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

Algorytmy *klasyfikacji* i *regresji* to dwa typy nadzorowanego uczenia maszynowego. Klasyfikacja przewiduje odpowiedź na podstawie zdefiniowanego zestawu kategorii, takich jak kolory (czerwony, niebieski lub zielony). Regresja jest używane toopredict liczbą.

Ponieważ chcemy ceny toopredict, która jest liczbą, użyjemy algorytm regresji. W tym przykładzie użyjemy prostego modelu *regresji liniowej*.

> [!TIP]
> Toolearn więcej o różnych typach algorytmów uczenia maszynowego i gdy toouse ich może wyświetlić wideo pierwszy hello w hello nauki danych serii początkujących [hello pięciu pytania dotyczące danych nauki odpowiedzi](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md). Może też przyjrzeć hello infographic [Machine learning podstawy wraz z przykładami algorytmu](machine-learning-basics-infographic-with-algorithm-examples.md), lub sprawdź hello [Machine learning arkusz ze wskazówkami dotyczącymi algorytmu](machine-learning-algorithm-cheat-sheet.md).

Firma Microsoft uczenia modelu hello przez nadanie mu zestaw danych, który zawiera cen hello. Hello model skanuje hello danych i wyszukać korelacji między samochodów funkcji i jej cenę. Następnie przetestujemy modelu hello — firma Microsoft będzie nadaj zestaw funkcji dla samochodów, który jest zapoznać się z i zobacz, jak blisko hello modelu pochodzi cen znane hello toopredicting.

Użyjemy danych zarówno uczenie modelu hello i testowanie go przez podział danych hello na oddzielnych celów szkoleniowych i testów zestawów danych.

1. Wybierz i przeciągnij hello [podziału danych] [ split] toohello modułu obszaru roboczego eksperymentu i połącz go toohello ostatnio [Select Columns in Dataset] [ select-columns] Moduł.

2. Kliknij przycisk hello [podziału danych] [ split] tooselect modułu go. Znajdź hello **ułamek wierszy w hello najpierw wyjściowy zestaw danych** (w hello **właściwości** toohello okienko prawo do kanwy hello) i ustaw dla niej too0.75. Dzięki temu firma Microsoft będzie przy użyciu 75 procent hello danych tootrain hello modelu, a pozostałe 25% do testowania (później możesz eksperymentować z różnych wartości procentowych).

    ![Zestaw hello podzielić część too0.75 modułu "Podziel dane" hello][set-split-data-percentage]
    <br/>
    ***Zestaw hello podzielić część too0.75 modułu "Podziel dane" hello***

    > [!TIP]
    > Zmieniając hello **Random seed** parametru, można uzyskać różne próbki losowe do celów szkoleniowych i testów. Ten parametr określa hello wstępne wypełnianie hello pseudolosowego generatora liczb.

2. Uruchom eksperyment hello. Uruchomienie eksperymentu hello hello [Select Columns in Dataset] [ select-columns] i [podziału danych] [ split] modułów przekazać toohello definicje kolumn Moduły możemy będą dodawane później.  

3. Algorytm uczenia hello tooselect rozwiń hello **Machine Learning** kategorii w lewej toohello palety modułu hello z hello obszaru roboczego, a następnie rozwiń **zainicjować modelu**. Zostaną wyświetlone różne kategorie modułów, które mogą być algorytmów uczenia maszynowego tooinitialize używane. W tym eksperymencie wybierz hello [regresji liniowej] [ linear-regression] moduł hello **regresji** , kategoria i przeciągnij go toohello kanwy eksperymentu.
(Można również znaleźć modułu hello, wpisując "linear regression" w polu wyszukiwania palety hello.)

4. Znajdź i przeciągnij hello [Train Model] [ train-model] kanwy eksperymentu toohello modułu. Połącz dane wyjściowe hello hello [regresji liniowej] [ linear-regression] toohello modułu pozostałych danych wejściowych hello [Train Model] [ train-model] modułu i połącz hello uczenie danych dane wyjściowe (po lewej portu) hello [podziału danych] [ split] modułu toohello dane wejściowe z hello [Train Model] [ train-model] Moduł.

    ![Połącz hello "Train Model" moduł tooboth hello "Linear Regression" i "Podział dane" modułów][connect-train-model]
    <br/>
    ***Połącz hello "Train Model" moduł tooboth hello "Linear Regression" i "Podział dane" modułów***

5. Kliknij przycisk hello [Train Model] [ train-model] modułu, kliknij przycisk **Uruchom selektor kolumn** w hello **właściwości** okienka, a następnie wybierz opcję hello **cen** kolumny. Jest to nasz model toopredict będzie wartość hello.

    Wybierz hello **cen** kolumny selektora kolumn hello przez przeniesienie ich z hello **dostępne kolumny** listy toohello **wybrane kolumny** listy.

    ![Wybierz kolumnę cen powitania dla modułu "Train Model" hello][select-price-column]
    <br/>
    ***Wybierz kolumnę cen powitania dla modułu "Train Model" hello***

6. Uruchom eksperyment hello.

Mamy teraz nauczony model regresji, który może być używane tooscore nowych danych samochodów toomake cen prognoz.

![Po uruchomieniu, eksperymentu hello powinna wyglądać mniej więcej tak][second-experiment-run]
<br/>
***Po uruchomieniu, eksperymentu hello powinna wyglądać mniej więcej tak***

## <a name="step-5-predict-new-automobile-prices"></a>Krok 5. Przewidywanie nowych cen samochodów

Teraz, gdy udało się nauczyć model hello przy użyciu 75% danych, firma Microsoft może być używany tooscore hello pozostałe 25 procent toosee danych hello, jak dobrze funkcjonowania modelu.

1. Znajdź i przeciągnij hello [Score Model] [ score-model] kanwy eksperymentu toohello modułu. Połącz dane wyjściowe hello hello [Train Model] [ train-model] toohello modułu pozostałych port wejściowy z [Score Model][score-model]. Połącz hello danymi wyjściowymi testów (prawy port) z hello [podziału danych] [ split] port wejściowy prawo toohello modułu [Score Model][score-model].

    ![Połącz hello "Score Model" moduł tooboth hello "Train Model" i "Podział dane" modułów][connect-score-model]
    <br/>
    ***Połącz hello "Score Model" moduł tooboth hello "Train Model" i "Podział dane" modułów***

2. Uruchom eksperyment hello i wyświetlić dane wyjściowe hello hello [Score Model] [ score-model] modułu (kliknij port wyjściowy hello [Score Model] [ score-model] i wybierz pozycję **Wizualizacji**). przedstawia dane wyjściowe Hello hello przewidywane wartości cen i znane wartości z danych testowych hello hello.  

    ![Dane wyjściowe z modułu "Score Model" hello][score-model-output]
    <br/>
    ***Dane wyjściowe z modułu "Score Model" hello***

3. Ponadto firma Microsoft testuje hello jakość hello wyników. Wybierz i przeciągnij hello [Evaluate Model] [ evaluate-model] toohello modułu obszaru roboczego eksperymentu i połącz dane wyjściowe hello hello [Score Model] [ score-model] Moduł toohello pozostałych danych wejściowych [Evaluate Model][evaluate-model].

    > [!TIP]
    > Istnieją dwa porty wejściowe na powitania [Evaluate Model] [ evaluate-model] moduł może być używane toocompare dwa modele obok siebie. Później można dodać innego eksperymentu toohello algorytmu i używać [Evaluate Model] [ evaluate-model] toosee, co zapewnia lepsze wyniki.

4. Uruchom eksperyment hello.

dane wyjściowe hello tooview hello [Evaluate Model] [ evaluate-model] modułu, kliknij port wyjściowy hello, a następnie wybierz **Visualize**.

![Wyniki oceny do eksperymentu hello][evaluation-results]
<br/>
***Wyniki oceny do eksperymentu hello***

Witaj następujące statystyki są wyświetlane dla naszego modelu:

- **Oznacza błąd absolutny** (MAE): hello średnia bezwzględnych błędów ( *błąd* hello różnic między hello przewidzieć wartość i wartością rzeczywistą hello).
- **Błąd kwadratów oznacza główny** (RMSE): pierwiastek kwadratowy hello hello średniej kwadratów błędów prognoz dla zestawu danych testowych hello.
- **Względny błąd absolutny**: hello średniej błędów absolutnych względną toohello bezwzględnej wartości różnicy między wartościami rzeczywistymi a średnią wszystkich wartości rzeczywistych hello.
- **Błąd względny Średniokwadratowy**: hello średniej kwadratów błędów względną toohello kwadrat różnica między wartościami rzeczywistymi hello i hello średnią wszystkich wartości rzeczywistych.
- **Współczynnik determinacji**: nazywane również hello **wartość R-kwadrat**, jest miarą statystyczną stopień dopasowania hello danych modelu.

Dla każdego błędu hello statystyk mniejsze wartości oznaczają lepszą. Mniejsze wartości błędów wskazują, że prognoz hello ściślejsze dopasowanie hello rzeczywiste wartości. Aby uzyskać **współczynnika determinacji**, hello bliżej jego wartość wynosi tooone (1.0) hello lepsze hello prognoz.

## <a name="final-experiment"></a>Eksperyment końcowy

Witaj końcowy eksperyment powinien wyglądać następująco:

![końcowy eksperyment Hello][complete-linear-regression-experiment]
<br/>
***końcowy eksperyment Hello***

## <a name="next-steps"></a>Następne kroki

Po ukończeniu hello pierwszy samouczek dotyczący uczenia maszynowego i mieć skonfigurowanego eksperymentu można kontynuować tooimprove hello modelu i wdrożyć go jako usługę sieci web predykcyjnej.

- **Iterowanie modelu hello tooimprove tootry** — na przykład można zmienić funkcji hello używane do prognozowania. Można też zmodyfikować właściwości hello hello [regresji liniowej] [ linear-regression] algorytm lub spróbuj całkowicie innego algorytmu. Można dodać wiele maszyny eksperymentu tooyour algorytmów uczenia w tym samym czasie i porównać dwa z nich przy użyciu hello [Evaluate Model] [ evaluate-model] modułu.
Przykład toocompare wielu modeli w jednym eksperymentu, zobacz temat [porównania Regresorów](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) w hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).

    > [!TIP]
    > toocopy dowolną iterację eksperymentu, użyj hello **SAVE AS** przycisk u dołu hello hello strony. Wszystkie iteracje eksperymentu hello można wyświetlić, klikając **WYŚWIETL HISTORIĘ URUCHAMIANIA** u dołu hello hello strony. Aby uzyskać bardziej szczegółowe informacje, zobacz [Manage experiment iterations in Azure Machine Learning Studio][runhistory] (Zarządzanie iteracjami eksperymentów w usłudze Azure Machine Learning Studio).

[runhistory]: machine-learning-manage-experiment-iterations.md

- **Wdróż model hello jako usługę sieci web predykcyjnej** — po zakończeniu z danym modelem, możesz go wdrożyć jako toobe usługi sieci web używaną cen samochodów toopredict przy użyciu nowych danych. Aby uzyskać dodatkowe informacje, zobacz [Deploy an Azure Machine Learning web service][publish] (Wdrażanie usługi sieci Web Azure Machine Learning).

[publish]: machine-learning-publish-a-machine-learning-web-service.md

Potrzebujesz więcej toolearn? Aby uzyskać bardziej rozbudowanym i szczegółowym przewodnikiem hello proces tworzenia, szkolenia, ocenianie i wdrażanie modelu, zobacz [tworzenie rozwiązania predykcyjnego za pomocą usługi Azure Machine Learning][walkthrough].

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
